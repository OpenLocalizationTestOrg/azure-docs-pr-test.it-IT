---
title: aaaPrepare tooAzure di tooupload un disco rigido virtuale di Windows | Documenti Microsoft
description: Come tooprepare un disco rigido virtuale di Windows o VHDX prima del caricamento tooAzure
services: virtual-machines-windows
documentationcenter: 
author: glimoli
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7802489d-33ec-4302-82a4-91463d03887a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: genli
ms.openlocfilehash: 530390e4c6a4f66ddfd4da23338f9bb3708c299f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-windows-vhd-or-vhdx-tooupload-tooazure"></a>Preparare un tooAzure tooupload Windows VHD o VHDX
Prima di caricare una macchina virtuale Windows (VM) da on-premise tooMicrosoft Azure, è necessario preparare hello disco virtuale (VHD o VHDX). Azure supporta solo macchine virtuali di generazione 1 nel formato di file VHD hello e dispongono di un disco di dimensione fissato. dimensione massima di Hello consentite per hello che VHD è 1023 GB. È possibile convertire una generazione 1 macchina virtuale da hello VHDX file tooVHD di sistema e da una a espansione dinamica toofixed dimensioni su disco. Non è tuttavia possibile modificare la generazione di una macchina virtuale. Per altre informazioni, vedere [Should I create a generation 1 or 2 VM in Hyper-V](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v) (Creare una macchina virtuale di prima o seconda generazione in Hyper-V).

Per ulteriori informazioni sui criteri di supporto hello per la macchina virtuale di Azure, vedere [supporto del software server Microsoft per le macchine virtuali di Microsoft Azure](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).

> [!Note]
> istruzioni di Hello in questo articolo si applicano toohello versione a 64 bit di Windows Server 2008 R2 e versioni successive sistema operativo di Windows server. Per informazioni sull'esecuzione di sistemi operativi a 32 bit in Azure, vedere [Support for 32-bit operating systems in Azure virtual machines](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines) (Supporto per sistemi operativi a 32 bit in macchine virtuali di Azure).

## <a name="convert-hello-virtual-disk-toovhd-and-fixed-size-disk"></a>Convertire hello tooVHD di disco virtuale e disco di dimensioni fisse 
Se è necessario tooconvert formato toohello il disco virtuale necessaria per Azure, utilizzare uno dei metodi di hello in questa sezione. Eseguire il backup hello VM prima di eseguire processo di conversione del disco virtuale hello e assicurarsi che tale disco rigido virtuale di Windows funziona correttamente sul server locale hello di hello. Prima di provare tooconvert o caricarlo tooAzure, risolvere eventuali problemi all'interno di hello macchina virtuale stessa.

Dopo aver convertito il disco di hello, creare una macchina virtuale che utilizza disco hello convertito. Avviare ed eseguire l'accesso toohello VM toofinish preparazione hello VM per il caricamento.

### <a name="convert-disk-using-hyper-v-manager"></a>Convertire il disco tramite la console di gestione di Hyper-V
1. Aprire Gestione di Hyper-V e selezionare il computer locale a sinistra di hello. Nel menu di hello sopra l'elenco di computer hello, fare clic su **azione** > **modifica disco**.
2. In hello **percorso disco rigido virtuale** schermata, individuare e selezionare il disco virtuale.
3. In hello **scelta azione** schermata e quindi selezionare **convertire** e **Avanti**.
4. Se è necessario tooconvert formato vhdx, selezionare **VHD** e quindi fare clic su **successivo**
5. Se è necessario tooconvert da un disco a espansione dinamica, selezionare **dimensioni fisse** e quindi fare clic su **successivo**
6. Individuare e selezionare un percorso toosave hello nuovo file VHD.
7. Fare clic su **Finish**.

>[!NOTE]
>comandi Hello in questo articolo devono essere eseguiti in una sessione di PowerShell con privilegi elevata.

### <a name="convert-disk-by-using-powershell"></a>Convertire il disco tramite PowerShell
È possibile convertire un disco virtuale utilizzando hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) comando in Windows PowerShell. Selezionare **Esegui come amministratore** quando si avvia PowerShell. 

Hello comando di esempio seguente converte da tooVHD VHDX e da un'ad espansione dinamica toofixed-dimensioni disco:

```Powershell
Convert-VHD –Path c:\test\MY-VM.vhdx –DestinationPath c:\test\MY-NEW-VM.vhd -VHDType Fixed
```
In questo comando, sostituire il valore di hello per "-Path" con hello percorso toohello disco rigido virtuale che si desidera tooconvert e hello valore per "-DestinationPath" con hello nuovo percorso e nome di hello convertito il disco.

### <a name="convert-from-vmware-vmdk-disk-format"></a>Conversione dal formato VMware VMDK
Se si dispone di un'immagine di macchina virtuale Windows in hello [il formato di file VMDK](https://en.wikipedia.org/wiki/VMDK), convertirlo tooa VHD utilizzando hello [Microsoft VM convertitore](https://www.microsoft.com/download/details.aspx?id=42497). Per ulteriori informazioni, vedere l'articolo di blog hello [come un disco rigido virtuale tooHyper V VMDK di VMware tooConvert](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx).

## <a name="set-windows-configurations-for-azure"></a>Impostare le configurazioni di Windows per Azure

Nella macchina virtuale che si prevede di hello tooAzure tooupload, eseguire tutti i comandi seguenti di hello i passaggi da un [finestra prompt dei comandi con privilegi elevati](https://technet.microsoft.com/library/cc947813.aspx):

1. Rimuovere le route statiche permanente nella tabella di routing hello:
   
   * tabella di route hello tooview, eseguire `route print` al prompt dei comandi di hello.
   * Controllare hello **persistenza route** sezioni. Se esiste una route permanente, utilizzare [delete route](https://technet.microsoft.com/library/cc739598.apx) tooremove è.
2. Rimuovere proxy WinHTTP hello:
   
    ```PowerShell
    netsh winhttp reset proxy
    ```
3. Impostare criteri di hello disco SAN troppo[Onlineall](https://technet.microsoft.com/library/gg252636.aspx). 
   
    ```PowerShell
    diskpart 
    ```
    Nella finestra del prompt dei comandi aprire hello, digitare hello seguenti comandi:

     ```DISKPART
    san policy=onlineall
    exit   
    ```

4. Impostare ora Coordinated Universal Time (UTC) per Windows e hello tipo di avvio del servizio ora di Windows (w32time) hello troppo**automaticamente**:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\TimeZoneInformation' -name "RealTimeIsUniversal" 1 -Type DWord

    Set-Service -Name w32time -StartupType Auto
    ```
5. Impostare hello power profilo toohello **ad alte prestazioni**:

    ```PowerShell
    powercfg /setactive SCHEME_MIN
    ```

## <a name="check-hello-windows-services"></a>Verificare i servizi di Windows hello
Verificare che ognuno dei seguenti servizi di Windows hello è impostato toohello **i valori predefiniti di Windows**. Si tratta di numero minimo di hello di servizi che devono essere impostati toomake che tale hello macchina virtuale disponga di connettività. impostazioni di avvio di hello di tooreset, eseguire hello seguenti comandi:
   
```PowerShell
Set-Service -Name bfe -StartupType Auto
Set-Service -Name dhcp -StartupType Auto
Set-Service -Name dnscache -StartupType Auto
Set-Service -Name IKEEXT -StartupType Auto
Set-Service -Name iphlpsvc -StartupType Auto
Set-Service -Name netlogon -StartupType Manual
Set-Service -Name netman -StartupType Manual
Set-Service -Name nsi -StartupType Auto
Set-Service -Name termService -StartupType Manual
Set-Service -Name MpsSvc -StartupType Auto
Set-Service -Name RemoteRegistry -StartupType Auto
```

## <a name="update-remote-desktop-registry-settings"></a>Aggiornare le impostazioni del registro di Desktop remoto
Verificare che tale hello seguenti impostazioni sono configurate correttamente per connessione desktop remoto:

>[!Note] 
>Si potrebbe ricevere un messaggio di errore quando si esegue hello **Set-ItemProperty-Path ' servizi HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal - nome &lt;nome dell'oggetto&gt; &lt;valore&gt;** in questa procedura. messaggio di errore Hello può essere tranquillamente ignorato. Significa che solo quel dominio hello non viene eseguita la configurazione tramite un oggetto Criteri di gruppo.
>
>

1. Remote Desktop Protocol (RDP) è abilitato:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDenyTSConnections" -Value 0 -Type DWord
    ```
   
2. Hello porta RDP sia impostato correttamente (impostazione predefinita la porta 3389):
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "PortNumber" 3389 -Type DWord
    ```
    Quando si distribuisce una macchina virtuale, vengono create le regole predefinite di hello porta 3389. Se si desidera il numero di porta hello toochange, eseguire questa operazione dopo aver distribuito hello VM in Azure.

3. Hello listener è in ascolto in ogni interfaccia di rete:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "LanAdapter" 0 -Type DWord
   ```
4. Configurare la modalità di autenticazione a livello di rete hello per le connessioni RDP hello:
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SecurityLayer" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "fAllowSecProtocolNegotiation" 1 -Type DWord
     ```

5. Impostare valore keep-alive hello:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveEnable" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveInterval" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "KeepAliveTimeout" 1 -Type DWord
    ```
6. Ristabilire la connessione:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDisableAutoReconnect" 0 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fInheritReconnectSame" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fReconnectSame" 0 -Type DWord
    ```
7. Numero di hello limite di connessioni simultanee:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "MaxInstanceCount" 4294967295 -Type DWord
    ```
8. Se sono presenti i certificati autofirmati collegata listener RDP toohello, rimuoverli:
    
    ```PowerShell
    Remove-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SSLCertificateSHA1Hash"
    ```
    Si tratta di toomake assicurarsi che sia possibile connettersi all'inizio di hello quando si distribuisce hello macchina virtuale. È anche possibile esaminare questa in una fase successiva dopo hello che macchina virtuale viene distribuita in Azure, se necessario.

9. Se hello VM farà parte di un dominio, controllare che tutti hello seguente toomake impostazioni assicurarsi che le impostazioni precedenti hello non vengono ripristinate. criteri di Hello che devono essere controllati sono seguente hello:
    
    - RDP è abilitato:

         Configurazione computer\Criteri\Impostazioni di Windows \Modelli amministrativi\ Componenti\Servizi Desktop remoto\Host sessione Desktop remoto\Connessioni:
         
         **Consenti tooconnect gli utenti in modalità remota tramite Desktop remoto**

    - Criteri di gruppo NLA:

        Impostazioni\Modelli amministrativi\ Componenti\Servizi Desktop remoto\Host sessione Desktop remoto\Sicurezza: 
        
        **Richiedi autenticazione utente tramite Autenticazione a livello di rete per le connessioni remote**
    
    - Impostazioni Keep-alive:

        Configurazione computer\Criteri\Impostazioni di Windows \Modelli amministrativi\ Componenti di Windows\Servizi Desktop remoto\Host sessione Desktop remoto\Connessioni: 
        
        **Configura intervallo keep-alive della connessione**

    - Impostazioni di riconnessione:

        Configurazione computer\Criteri\Impostazioni di Windows \Modelli amministrativi\ Componenti di Windows\Servizi Desktop remoto\Host sessione Desktop remoto\Connessioni: 
        
        **Riconnessione automatica**

    - Limita il numero di hello di impostazioni di connessione:

        Configurazione computer\Criteri\Impostazioni di Windows \Modelli amministrativi\ Componenti di Windows\Servizi Desktop remoto\Host sessione Desktop remoto\Connessioni: 
        
        **Limita il numero di connessioni**

## <a name="configure-windows-firewall-rules"></a>Configurare le regole del firewall di Windows
1. Attiva Windows Firewall sui profili hello tre (dominio, Standard e pubblico):

   ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\DomainProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\PublicProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\Standardprofile' -name "EnableFirewall" -Value 1 -Type DWord
   ```

2. Eseguire hello seguente comando PowerShell tooallow WinRM tramite i profili del firewall hello tre (dominio, privato e pubblico) e abilitare hello assistenza remota di PowerShell:
   
   ```PowerShell
    Enable-PSRemoting -force
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
   ```
3. Abilitare hello seguendo il traffico RDP firewall regole tooallow hello 

   ```PowerShell
    netsh advfirewall firewall set rule group="Remote Desktop" new enable=yes
   ```   
4. Abilitare la regola di condivisione stampanti e File hello in modo che hello VM può rispondere comando ping tooa all'interno di hello rete virtuale:

   ```PowerShell
    netsh advfirewall firewall set rule dir=in name="File and Printer Sharing (Echo Request - ICMPv4-In)" new enable=yes
   ``` 
5. Se hello VM farà parte di un dominio, è possibile controllare hello seguente toomake impostazioni assicurarsi che le impostazioni precedenti hello non vengono ripristinate. criteri Hello AD che devono essere controllati sono seguente hello:

    - Abilitare i profili del Firewall di Windows hello

        Configurazione computer\Criteri\Impostazioni di Windows\Modelli amministrativi\Rete\Connessione di rete\Windows Firewall\Profilo di dominio\Windows Firewall: **proteggi tutte le connessioni di rete**

       Configurazione computer\Criteri\Impostazioni di Windows\Modelli amministrativi\Rete\Connessione di rete\Windows Firewall\Profilo standard\Windows Firewall: **proteggi tutte le connessioni di rete**

    - Abilitare RDP 

        Configurazione computer\Criteri\Impostazioni di Windows\Modelli amministrativi\Rete\Connessione di rete\Windows Firewall\Profilo di dominio\Windows Firewall: **consenti eccezioni per Desktop remoto in ingresso**

        Configurazione computer\Criteri\Impostazioni di Windows\Modelli amministrativi\Rete\Connessione di rete\Windows Firewall\Profilo standard\Windows Firewall: **consenti eccezioni per Desktop remoto in ingresso**

    - Abilitare ICMP V4

        Configurazione computer\Criteri\Impostazioni di Windows\Modelli amministrativi\Rete\Connessione di rete\Windows Firewall\Profilo di dominio\Windows Firewall: **consenti eccezioni ICMP**

        Configurazione computer\Criteri\Impostazioni di Windows\Modelli amministrativi\Rete\Connessione di rete\Windows Firewall\Profilo standard\Windows Firewall: **consenti eccezioni ICMP**

## <a name="verify-vm-is-healthy-secure-and-accessible-with-rdp"></a>Verificare che la macchina virtuale sia integra, sicura e accessibile con RDP 
1. disco hello che toomake sia integro e coerente, eseguire un'operazione del disco di controllo al successivo riavvio VM hello:

    ```PowerShell
    Chkdsk /f
    ```
    Assicurarsi che i report di hello Mostra un disco integro e pulito.

2. Configurare le impostazioni di dati di configurazione di avvio (BCD) hello. 

    > [!Note]
    > Assicurarsi che questi comandi vengano eseguiti in una finestra dei comandi con privilegi elevati e **NON** in PowerShell:
   
   ```CMD
   bcdedit /set {bootmgr} integrityservices enable
   
   bcdedit /set {default} device partition=C:
   
   bcdedit /set {default} integrityservices enable
   
   bcdedit /set {default} recoveryenabled Off
   
   bcdedit /set {default} osdevice partition=C:
   
   bcdedit /set {default} bootstatuspolicy IgnoreAllFailures
   ```
3. Verificare che il repository di Strumentazione gestione Windows hello sia coerenza. tooperform, hello esecuzione comando seguente:

    ```PowerShell
    winmgmt /verifyrepository
    ```
    Se il repository di hello è danneggiato, vedere [WMI: archivio danneggiato, o non](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not).

4. Assicurarsi che qualsiasi altra applicazione non utilizza la porta 3389 hello. Questa porta viene utilizzata per hello servizio RDP in Azure. È possibile eseguire **netstat - anob** toosee le porte in uso nel hello VM:

    ```PowerShell
    netstat -anob
    ```

5. Se il disco rigido virtuale di Windows che si desidera tooupload hello è un controller di dominio, attenersi alla seguente procedura:

    R. Seguire [questi passaggi aggiuntivi](https://support.microsoft.com/kb/2904015) disco hello tooprepare.

    B. Assicurarsi di conoscere la password DSRM hello nel caso in cui si toostart hello macchina virtuale in modalità ripristino servizi directory in un determinato momento. È possibile toorefer toothis collegamento hello tooset [password modalità ripristino servizi directory](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx).

6. Assicurarsi che la password e account Administrator predefinito hello sono note tooyou. È possibile desidera password dell'amministratore locale corrente tooreset hello e assicurarsi che è possibile utilizzare questo account toosign in tooWindows tramite hello connessione RDP. Questa autorizzazione di accesso è controllata dall'oggetto Criteri di gruppo "Consenti accesso tramite Servizi Desktop remoto" hello. È possibile visualizzare questo oggetto in Editor criteri di gruppo locali hello in:

    Configurazione computer\Impostazioni di Windows\Impostazioni di sicurezza\Criteri locali\Assegnazione diritti utente

7. Controllare criteri di hello seguente AD assicurarsi che non siano bloccate l'accesso RDP tramite RDP né dalla rete hello toomake:

    - Computer Configurazione computer\Impostazioni di Windows\Impostazioni sicurezza\Criteri locali\Assegnazione diritti Assignment\Deny accesso toothis computer hello rete

    - Configurazione computer\Impostazioni di Windows\Impostazioni protezione\Criteri locali\Assegnazione diritti utente\Impedisci accesso tramite Servizi Desktop remoto


8. Riavvio hello VM toomake che Windows sia ancora integro può essere raggiunto tramite la connessione RDP hello. A questo punto, è possibile desiderata del locale Hyper-V toomake che hello che VM avvio completamente toocreate una macchina virtuale e quindi verificare se si tratta di RDP raggiungibile.

9. Rimuovere qualsiasi filtro TDI (Transport Driver Interface) aggiuntivo, ad esempio il software che analizza i pacchetti TCP o altri firewall. È anche possibile esaminare questa in una fase successiva dopo hello che macchina virtuale viene distribuita in Azure, se necessario.

10. Disinstallare eventuali altri software di terze parti e driver che i componenti correlati toophysical o qualsiasi altra tecnologia di virtualizzazione.

### <a name="install-windows-updates"></a>Installare gli aggiornamenti di Windows
configurazione ideale Hello è troppo**disporre del livello di patch hello di computer più recenti hello hello**. In caso contrario, verificare che tale hello dopo gli aggiornamenti vengono installati:

|                       |                   |           |                                       Versione minima del file x64       |                                      |                                      |                            |
|-------------------------|-------------------|------------------------------------|---------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|
| Componente               | Binary            | Windows 7 e Windows Server 2008 R2 | Windows 8 e Windows Server 2012             | Windows 8.1 e Windows Server 2012 R2 | Windows 10 e Windows Server 2016 RS1 | Windows 10 RS2             |
| Archiviazione                 | disk.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17638 / 6.2.9200.21757 - KB3137061 | 6.3.9600.18203 - KB3137061           | -                                    | -                          |
|                         | storport.sys      | 6.1.7601.23403 - KB3125574         | 6.2.9200.17188 / 6.2.9200.21306 - KB3018489 | 6.3.9600.18573 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.332             |
|                         | ntfs.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17623 / 6.2.9200.21743 - KB3121255 | 6.3.9600.18654 - KB4022726           | 10.0.14393.1198 - KB4022715          | 10.0.15063.447             |
|                         | Iologmsg.dll      | 6.1.7601.23403 - KB3125574         | 6.2.9200.16384 - KB2995387                  | -                                    | -                                    | -                          |
|                         | Classpnp.sys      | 6.1.7601.23403 - KB3125574         | 6.2.9200.17061 / 6.2.9200.21180 - KB2995387 | 6.3.9600.18334 - KB3172614           | 10.0.14393.953 - KB4022715           | -                          |
|                         | Volsnap.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.17047 / 6.2.9200.21165 - KB2975331 | 6.3.9600.18265 - KB3145384           | -                                    | 10.0.15063.0               |
|                         | partmgr.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.16681 - KB2877114                  | 6.3.9600.17401 - KB3000850           | 10.0.14393.953 - KB4022715           | 10.0.15063.0               |
|                         | volmgr.sys        |                                    |                                             |                                      |                                      | 10.0.15063.0               |
|                         | Volmgrx.sys       | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | 10.0.15063.0               |
|                         | Msiscsi.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.21006 - KB2955163                  | 6.3.9600.18624 - KB4022726           | 10.0.14393.1066 - KB4022715          | 10.0.15063.447             |
|                         | Msdsm.sys         | 6.1.7601.23403 - KB3125574         | 6.2.9200.21474 - KB3046101                  | 6.3.9600.18592 - KB4022726           | -                                    | -                          |
|                         | Mpio.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.21190 - KB3046101                  | 6.3.9600.18616 - KB4022726           | 10.0.14393.1198 - KB4022715          | -                          |
|                         | Fveapi.dll        | 6.1.7601.23311 - KB3125574         | 6.2.9200.20930 - KB2930244                  | 6.3.9600.18294 - KB3172614           | 10.0.14393.576 - KB4022715           | -                          |
|                         | Fveapibase.dll    | 6.1.7601.23403 - KB3125574         | 6.2.9200.20930 - KB2930244                  | 6.3.9600.17415 - KB3172614           | 10.0.14393.206 - KB4022715           | -                          |
| Rete                 | netvsc.sys        | -                                  | -                                           | -                                    | 10.0.14393.1198 - KB4022715          | 10.0.15063.250 - KB4020001 |
|                         | mrxsmb10.sys      | 6.1.7601.23816 - KB4022722         | 6.2.9200.22108 - KB4022724                  | 6.3.9600.18603 - KB4022726           | 10.0.14393.479 - KB4022715           | 10.0.15063.483             |
|                         | mrxsmb20.sys      | 6.1.7601.23816 - KB4022722         | 6.2.9200.21548 - KB4022724                  | 6.3.9600.18586 - KB4022726           | 10.0.14393.953 - KB4022715           | 10.0.15063.483             |
|                         | mrxsmb.sys        | 6.1.7601.23816 - KB4022722         | 6.2.9200.22074 - KB4022724                  | 6.3.9600.18586 - KB4022726           | 10.0.14393.953 - KB4022715           | 10.0.15063.0               |
|                         | tcpip.sys         | 6.1.7601.23761 - KB4022722         | 6.2.9200.22070 - KB4022724                  | 6.3.9600.18478 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.447             |
|                         | http.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17285 - KB3042553                  | 6.3.9600.18574 - KB4022726           | 10.0.14393.251 - KB4022715           | 10.0.15063.483             |
|                         | vmswitch.sys      | 6.1.7601.23727 - KB4022719         | 6.2.9200.22117 - KB4022724                  | 6.3.9600.18654 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.138             |
| Core                    | ntoskrnl.exe      | 6.1.7601.23807 - KB4022719         | 6.2.9200.22170 - KB4022718                  | 6.3.9600.18696 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.483             |
| Servizi Desktop remoto | rdpcorets.dll     | 6.2.9200.21506 - KB4022719         | 6.2.9200.22104 - KB4022724                  | 6.3.9600.18619 - KB4022726           | 10.0.14393.1198 - KB4022715          | 10.0.15063.0               |
|                         | termsrv.dll       | 6.1.7601.23403 - KB3125574         | 6.2.9200.17048 - KB2973501                  | 6.3.9600.17415 - KB3000850           | 10.0.14393.0 - KB4022715             | 10.0.15063.0               |
|                         | termdd.sys        | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | win32k.sys        | 6.1.7601.23807 - KB4022719         | 6.2.9200.22168 - KB4022718                  | 6.3.9600.18698 - KB4022726           | 10.0.14393.594 - KB4022715           | -                          |
|                         | rdpdd.dll         | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | rdpwd.sys         | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
| Sicurezza                | Scadenza tooWannaCrypt | KB4012212                          | KB4012213                                   | KB4012213                            | KB4012606                            | KB4012606                  |
|                         |                   |                                    | KB4012216                                   |                                      | KB4013198                            | KB4013198                  |
|                         |                   | KB4012215                          | KB4012214                                   | KB4012216                            | KB4013429                            | KB4013429                  |
|                         |                   |                                    | KB4012217                                   |                                      | KB4013429                            | KB4013429                  |
       
### Quando toouse sysprep<a id="step23"></a>    

Sysprep è un processo che è possibile eseguire in un'installazione di windows che verrà reimpostato installazione hello del sistema di hello e fornirà un "configurazione hello guidata" rimuovendo tutti i dati personali e la reimpostazione di diversi componenti. In genere questa operazione è se si desidera toocreate un modello da cui è possibile distribuire diverse altre macchine virtuali che hanno una configurazione specifica. Il modello è denominato **immagine generalizzata**.

Se, invece, si desidera toocreate solo una macchina virtuale da un disco, non è toouse sysprep. In questo caso, è possibile creare hello macchina virtuale da cosa è noto come un **immagine specializzata**.

Per ulteriori informazioni su come toocreate una macchina virtuale da un disco specializzato, vedere:

- [Creare una macchina virtuale da un disco specializzato](create-vm-specialized.md)
- [Creare una macchina virtuale da un disco rigido virtuale specializzato](https://azure.microsoft.com/resources/templates/201-vm-specialized-vhd/)

Se si desidera un'immagine generalizzata toocreate, è necessario toorun sysprep. Per ulteriori informazioni su Sysprep, vedere [come tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx). 

Non tutti i ruoli o le applicazioni installate in un computer basato su Windows supportano questa generalizzazione. Pertanto, prima eseguire questa procedura, vedere toohello seguente articolo toomake assicurarsi che tale ruolo hello del computer è supportata da sysprep. Per altre informazioni, vedere [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles) (Supporto Sysprep per i ruoli server).

### <a name="steps-toogeneralize-a-vhd"></a>Passaggi toogeneralize un disco rigido virtuale

>[!NOTE]
> Dopo aver eseguito sysprep.exe hello specificato nella procedura seguente, disattivare la macchina virtuale hello e non riattivarla finché non si crea un'immagine da esso in Azure.

1. Accedi toohello macchina virtuale di Windows.
2. Eseguire il **prompt dei comandi** come amministratore. 
3. Passare alla directory hello: **%windir%\system32\sysprep**, quindi eseguire **sysprep.exe**.
3. In hello **System Preparation Tool** nella finestra di dialogo **immettere sistema Out-of-Box guidata**e assicurarsi che tale hello **Generalize** casella di controllo è selezionata.

    ![Utilità preparazione sistema](media/prepare-for-upload-vhd-image/syspre.png)
4. In **Opzioni di arresto del sistema** selezionare **Arresta il sistema**.
5. Fare clic su **OK**.
6. Al termine di Sysprep, arrestare hello macchina virtuale. Non utilizzare **riavviare** tooshut verso il basso hello macchina virtuale.
7. Hello disco rigido virtuale è ora pronto toobe caricato. Per ulteriori informazioni su come toocreate una macchina virtuale da un disco, vedere [caricare un disco rigido virtuale generalizzato e usarlo toocreate un nuove macchine virtuali in Azure](sa-upload-generalized.md).


## <a name="complete-recommended-configurations"></a>Completare le configurazioni consigliate
Hello seguenti impostazioni non influisce il caricamento di disco rigido virtuale. È tuttavia fortemente consigliabile configurarle.

* Installare hello [agente di macchine virtuali di Azure](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Sarà quindi possibile abilitare le estensioni delle VM. le estensioni VM Hello implementare la maggior parte delle funzionalità di hello critiche che si toouse con le macchine virtuali, ad esempio la reimpostazione delle password, la configurazione RDP e così via. Per altre informazioni, vedere:

    - [Agente ed estensioni delle VM - Parte 1](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-1/)
    - [Agente ed estensioni delle VM - Parte 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/)
* log di Dump Hello può essere utile nella risoluzione dei problemi di arresto anomalo del sistema di Windows. Abilitare la raccolta di log Dump hello:
  
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "AutoReboot" -Value 0 -Type DWord
    New-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps'
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
    Se si ricevono errori durante le procedure hello i passaggi in questo articolo, ciò significa che le chiavi del Registro di sistema hello esiste già. In questo caso, utilizzare hello seguente invece di comandi:

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
*  Dopo aver creato hello VM in Azure, è consigliabile archiviare file di paging hello in hello "temporale" volume tooimprove le prestazioni. A tale scopo, procedere come segue:

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management' -name "PagingFiles" -Value "D:\pagefile"
    ```
Se è presente qualsiasi disco dati collegato toohello macchina virtuale, la lettera di unità del volume di unità temporali hello è in genere "d". Tale designazione potrebbe essere diverso, in base al numero di hello di unità disponibili e le impostazioni di hello apportate.

## <a name="next-steps"></a>Passaggi successivi
* [Caricare un tooAzure immagine di macchina virtuale di Windows per le distribuzioni di gestione risorse](upload-generalized-managed.md)

