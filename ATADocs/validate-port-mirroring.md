---
title: Verifiera portspegling i Advanced Threat Analytics | Microsoft Docs
description: Beskriver hur du verifierar att portspegling har konfigurerats korrekt
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: ebd41719-c91a-4fdd-bcab-2affa2a2cace
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 8ebc7598128abe1fbebd10418bada5d68d9df9a1
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/22/2018
ms.locfileid: "30009810"
---
*Gäller för: Advanced Threat Analytics version 1.9.*



# <a name="validate-port-mirroring"></a>Verifiera portspegling
> [!NOTE] 
> Den här artikeln gäller bara om du distribuerar ATA Gateway i stället för ATA Lightweight Gateway. Mer information om hur du tar reda på om du behöver använda ATA Gateway finns i [Välja rätt gatewayer för distributionen](ata-capacity-planning.md#choosing-the-right-gateway-type-for-your-deployment).
 
Följande steg vägleder dig genom processen för att verifiera att portspegling har konfigurerats korrekt. Om ATA ska fungera ordentligt måste ATA Gateway kunna se trafiken till och från domänkontrollanten. Den huvudsakliga datakälla som ATA använder är djup paketinspektion för nätverkstrafiken till och från dina domänkontrollanter. Om ATA ska kunna se nätverkstrafiken måste portspegling vara konfigurerad. Portspegling kopierar trafiken från en port (källport) till en annan port (målport).

## <a name="validate-port-mirroring-using-a-windows-powershell-script"></a>Validera portspegling med ett Windows PowerShell-skript

1. Spara texten i det här skriptet i en fil med namnet *ATAdiag.ps1*.
2. Kör skriptet på den ATA-gateway som du vill validera.
Skriptet genererar ICMP-trafik från ATA Gateway till domänkontrollanten och söker efter den trafiken på avbildningsnätverkskortet på domänkontrollanten.
Om ATA Gateway ser ICMP-trafik med en destinations-IP-adress som är samma som den DC IP-adress du angav i ATA-konsolen bedömer den att portspegling har konfigurerats. 

Exempel på körning av skriptet:

    # ATAdiag.ps1 -CaptureIP n.n.n.n -DCIP n.n.n.n -TestCount n
    
    param([parameter(Mandatory=$true)][string]$CaptureIP, [parameter(Mandatory=$true)][string]$DCIP, [int]$PingCount = 10)

    # Set variables
    
        $ErrorActionPreference = "stop"
    $starttime = get-date
    $byteIn = new-object byte[] 4
    $byteOut = new-object byte[] 4
    $byteData = new-object byte[] 4096  # size of data
    
    $byteIn[0] = 1  # for promiscuous mode
    $byteIn[1-3] = 0
    $byteOut[0-3] = 0



    # Convert network data to host format
        function NetworkToHostUInt16 ($value)
        {
        [Array]::Reverse($value)
        [BitConverter]::ToUInt16($value,0)
        }
    
    function NetworkToHostUInt32 ($value)
        {
        [Array]::Reverse($value)
        [BitConverter]::ToUInt32($value,0)
        }
    
    function ByteToString ($value)
        {
        $AsciiEncoding = new-object system.text.asciiencoding
        $AsciiEncoding.GetString($value)
            }
    
    Write-Host "Testing Port Mirroring..." -ForegroundColor Yellow
    Write-Host ""
    Write-Host "Here is a summary of the connection we will test." -ForegroundColor Yellow

    # Initialize a first ping connection
    Test-Connection -Count 1 -ComputerName $DCIP -ea SilentlyContinue
    Write-Host ""
    
    Write-Host "Press any key to continue..." -ForegroundColor Red
    [void][System.Console]::ReadKey($true)
    Write-Host ""
    Write-Host "Sending ICMP and Capturing data..." -ForegroundColor Yellow
    
    # Open a socket
    
    $socket = new-object system.net.sockets.socket([Net.Sockets.AddressFamily]::InterNetwork,[Net.Sockets.SocketType]::Raw,[Net.Sockets.ProtocolType]::IP)
    
    # Include the IP header
    $socket.setsocketoption("IP","HeaderIncluded",$true)
    
    $socket.ReceiveBufferSize = 10000
    
    $ipendpoint = new-object system.net.ipendpoint([net.ipaddress]"$CaptureIP",0)
    $socket.bind($ipendpoint)
    
    # Enable promiscuous mode
    [void]$socket.iocontrol([net.sockets.iocontrolcode]::ReceiveAll,$byteIn,$byteOut)
    
    # Initialize test variables
    $tests = 0
    $TestResult = "Noise"
    $OneSuccess = 0
    
    while ($tests -le $PingCount)
        {
        if (!$socket.Available)  # see if any packets are in the queue
            {
            start-sleep -milliseconds 500
            continue
            }
    
    # Capture traffic
        $rcv = $socket.receive($byteData,0,$byteData.length,[net.sockets.socketflags]::None)
    
    # Decode the header so we can read ICMP
    
        $MemoryStream = new-object System.IO.MemoryStream($byteData,0,$rcv)
        $BinaryReader = new-object System.IO.BinaryReader($MemoryStream)
    
    # Set IP version & header length
        $VersionAndHeaderLength = $BinaryReader.ReadByte()
    
        # TOS
        $TypeOfService= $BinaryReader.ReadByte()
    
        # More values, and the Protocol Number for ICMP traffic
        # Convert network format of big-endian to host format of little-endian 
        $TotalLength = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
    
        $Identification = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
        $FlagsAndOffset = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
        $TTL = $BinaryReader.ReadByte()
        $ProtocolNumber = $BinaryReader.ReadByte()
        $Checksum = [Net.IPAddress]::NetworkToHostOrder($BinaryReader.ReadInt16())
    
        # The source and destination IP addresses
        $SourceIPAddress = $BinaryReader.ReadUInt32()
        $DestinationIPAddress = $BinaryReader.ReadUInt32()
    
        # The source and destimation ports
        $sourcePort = [uint16]0
        $destPort = [uint16]0
            
        # Close the stream reader
        $BinaryReader.Close()
        $memorystream.Close()
    
        # Cast DCIP into an IPaddress type
        $DCIPP = [ipaddress] $DCIP
        $DestinationIPAddressP = [ipaddress] $DestinationIPAddress
    
        #Ping the DC at the end after starting the capture
        Test-Connection -Count 1 -ComputerName $DCIP -ea SilentlyContinue | Out-Null
            
        # This is the match logic - check to see if Destination IP from the Ping sent matches the DCIP entered by in the ATA Console  
        # The only way the ATA Gateway should see a destination of the DC is if Port Spanning is configured
        
            if ($DestinationIPAddressP -eq $DCIPP)  # is the destination IP eq to the DC IP? 
            {
            $TestResult = "Port Spanning success!"
            $OneSuccess = 1
            } else {
                $TestResult = "Noise"
            }
        
        # Put source, destination, test result in Powershell object
        
        new-object psobject | add-member -pass noteproperty CaptureSource $([system.net.ipaddress]$SourceIPAddress) | add-member -pass noteproperty CaptureDestination $([system.net.ipaddress]$DestinationIPAddress) | Add-Member -pass NoteProperty Result $TestResult | Format-List | Out-Host
        #Count tests
        $tests ++
        }
    
        If ($OneSuccess -eq 1){
            Write-Host "Port Spanning Success!" -ForegroundColor Green
            Write-Host ""
            Write-Host "At least one packet which was addressed to the DC, was picked up by the Gateway." -ForegroundColor Yellow
            Write-Host "A little noise is OK, but if you don't see a majority of successes, you might want to re-run." -ForegroundColor Yellow
        } Else {
            Write-Host "No joy, all noise.  You may want to re-run, increase the number of Ping Counts, or check your config." -ForegroundColor Red
        }
    
    Write-Host ""
    Write-Host "Press any key to continue..." -ForegroundColor Red
    [void][System.Console]::ReadKey($true)
    
    
## <a name="validate-port-mirroring-using-net-mon"></a>Validera portspegling med Net Mon
1.  Installera [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865) på ATA Gateway som du vill validera.

    > [!IMPORTANT]
    > Installera inte Microsoft Analysverktyg för meddelanden eller någon annan programvara för trafikinsamling på ATA Gateway.

2.  Öppna Network Monitor och skapa en ny avbildningsflik.

    1.  Välj endast nätverkskortet att **avbilda** eller nätverkskortet som är anslutet till växelporten som har konfigurerats som portspeglingsmål.

    2.  Se till att P-Mode har aktiverats.

    3.  Klicka på **Ny avbildning**.

        ![Bild för fliken skapa ny avbildning](media/ATA-Port-Mirroring-Capture.jpg)

3.  I fönstret Visa filter anger du filtret **KerberosV5 OR LDAP** och klickar sedan på **Verkställ**.

    ![Bild för att använda KerberosV5 or LDAP-filter](media/ATA-Port-Mirroring-filter-settings.jpg)

4.  Klicka på **Starta** för att starta avbildningssessionen. Om du inte ser trafik till och från domänkontrollanten kontrollerar du konfigurationen av portspeglingen.

    ![Bild för att starta avbildningssession](media/ATA-Port-Mirroring-Capture-traffic.jpg)

    > [!NOTE]
    > Det är viktigt att du kan se trafiken till och från domänkontrollanterna.
    

5.  Om du bara ser trafik i en riktning bör du arbeta med nätverks- eller virtualiseringsteamen för att felsöka konfigurationen av portspeglingen.

## <a name="see-also"></a>Se även

- [Konfigurera portspegling](configure-port-mirroring.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
