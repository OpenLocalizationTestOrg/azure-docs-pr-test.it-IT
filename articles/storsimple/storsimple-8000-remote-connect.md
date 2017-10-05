---
title: Connessione remota al dispositivo StorSimple | Microsoft Docs
description: Viene illustrato come configurare il dispositivo per la gestione remota e come connettersi a Windows PowerShell per StorSimple tramite HTTP o HTTPS.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff76884f020a0fb8a1b48bd371c419bd65e85fd3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-remotely-to-your-storsimple-8000-series-device"></a>Connettersi in remoto al dispositivo StorSimple serie 8000

## <a name="overview"></a>Panoramica

È possibile connettersi in remoto al dispositivo tramite Windows PowerShell. Questo metodo di connessione non consente di visualizzare alcun menu. (Verrà visualizzato un menu solo se si utilizza la console seriale del dispositivo per la connessione.) Con la comunicazione remota di Windows PowerShell, ci si connette a uno specifico spazio di esecuzione. È inoltre possibile specificare la lingua di visualizzazione.

Per ulteriori informazioni sull'utilizzo della comunicazione remota di Windows PowerShell per gestire il dispositivo, andare a [Utilizzare Windows PowerShell per StorSimple per gestire il dispositivo StorSimple](storsimple-8000-windows-powershell-administration.md).

In questa esercitazione viene illustrato come configurare il dispositivo per la gestione remota, quindi come connettersi a Windows PowerShell per StorSimple. È possibile usare HTTP o HTTPS per connettersi in remoto tramite Windows PowerShell. Tuttavia, quando si decide come connettersi a Windows PowerShell per StorSimple, considerare quanto segue:

* La connessione diretta alla console seriale del dispositivo è protetta ma la connessione alla console seriale sugli switch di rete non lo è. Prestare attenzione al rischio di sicurezza quando ci si connette alla console seriale del dispositivo sugli switch di rete.
* La connessione tramite una sessione HTTP potrebbe offrire maggiore sicurezza rispetto alla connessione tramite la console seriale sulla rete. Sebbene non sia il metodo più sicuro, è accettabile su reti attendibili.
* La connessione tramite una sessione HTTPS con un certificato autofirmato è l'opzione più sicura e consigliata.

È possibile connettersi in remoto all'interfaccia di Windows PowerShell. Tuttavia, l'accesso remoto al dispositivo StorSimple tramite l'interfaccia di Windows PowerShell non è abilitato per impostazione predefinita. È necessario abilitare innanzitutto la gestione remota sul dispositivo, quindi sul client usato per l'accesso al dispositivo.

I passaggi descritti in questo articolo sono stati eseguiti in un sistema host che esegue Windows Server 2012 R2.

## <a name="connect-through-http"></a>Connessione tramite HTTP

La connessione a Windows PowerShell per StorSimple tramite una sessione HTTP offre una maggiore protezione rispetto alla connessione tramite la console seriale del dispositivo StorSimple. Sebbene non sia il metodo più sicuro, è accettabile su reti attendibili.

Per configurare la gestione remota, è possibile usare il portale di Azure o la console seriale. Selezionare una delle seguenti procedure:

* [Utilizzo del portale di Azure per abilitare la gestione remota su HTTP](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [Utilizzo della console seriale per abilitare la gestione remota su HTTP](#use-the-serial-console-to-enable-remote-management-over-http)

Dopo aver abilitato la gestione remota, utilizzare la procedura seguente per preparare il client per una connessione remota.

* [Preparazione del client per la connessione remota](#prepare-the-client-for-remote-connection)

### <a name="use-the-azure-portal-to-enable-remote-management-over-http"></a>Utilizzo del portale di Azure per abilitare la gestione remota su HTTP

Attenersi alla procedura seguente nel portale di Azure per abilitare la gestione remota su HTTP.

#### <a name="to-enable-remote-management-through-the-azure-portal"></a>Per abilitare la gestione remota tramite il portale di Azure

1. Passare al servizio Gestione dispositivi StorSimple. Selezionare **Dispositivi** e quindi fare clic sul dispositivo che si vuole configurare per la gestione remota. Passare a **Impostazioni dispositivo > Sicurezza**.
2. Nel pannello **Impostazioni di sicurezza** fare clic su **Gestione remota**.
3. Nel pannello **Gestione remota** impostare l'opzione **Abilita gestione remota** su **Sì**.
4. È ora possibile scegliere di connettersi tramite HTTP. (La connessione su HTTPS rappresenta la scelta predefinita.) Assicurarsi che HTTP sia selezionato.
   
   > [!NOTE]
   > La connessione tramite HTTP dovrebbe essere eseguita solo su reti attendibili.
   
5. Alla richiesta di conferma fare clic su **Salva** e quindi su **Sì**.

### <a name="use-the-serial-console-to-enable-remote-management-over-http"></a>Utilizzo della console seriale per abilitare la gestione remota su HTTP
Eseguire le operazioni seguenti nella console seriale del dispositivo per abilitare la gestione remota.

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a>Per abilitare la gestione remota tramite la console seriale del dispositivo:
1. Nel menu della console seriale, selezionare l'opzione 1. Per altre informazioni sull'uso della console seriale del dispositivo, vedere [Connessione a Windows PowerShell per StorSimple tramite la console seriale del dispositivo](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. Al prompt dei comandi, digitare: `Enable-HcsRemoteManagement –AllowHttp`
3. L'utente riceve una notifica sulle vulnerabilità di sicurezza relative all'utilizzo di HTTP per la connessione al dispositivo. Quando richiesto, confermare digitando **Y**.
4. Verificare che HTTP sia abilitato digitando: `Get-HcsSystem`
5. Verificare che il campo **RemoteManagementMode** mostri **HttpsAndHttpEnabled**. Nella figura seguente vengono illustrate queste impostazioni in PuTTY.
   
     ![Seriali HTTPS e HTTP abilitati](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-the-client-for-remote-connection"></a>Preparazione del client per la connessione remota
Eseguire le operazioni seguenti sul client per abilitare la gestione remota.

#### <a name="to-prepare-the-client-for-remote-connection"></a>Per preparare il client per la connessione remota:
1. Avviare una sessione di Windows PowerShell come amministratore.
2. Digitare il comando seguente per aggiungere l'indirizzo IP del dispositivo StorSimple all'elenco di host attendibili del client:
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     Sostituire <*ip_dispositivo*> con l'indirizzo IP del dispositivo, ad esempio: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Digitare il comando seguente per salvare le credenziali del dispositivo in una variabile: 
   
    ```
    $cred = Get-Credential
    ```
    
4. Nella finestra di dialogo visualizzata:
   
   1. Digitare il nome utente nel formato: *ip_dispositivo\SSAdmin*.
   2. Digitare la password di amministratore del dispositivo impostata quando il dispositivo è stato configurato con la configurazione guidata. La password predefinita è *Password1*.
5. Avviare una sessione di Windows PowerShell sul dispositivo digitando questo comando:
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > Per creare una sessione di Windows PowerShell per l'utilizzo con il dispositivo virtuale StorSimple, aggiungere il parametro `–Port` e specificare la porta pubblica configurata nella comunicazione remota per il dispositivo virtuale StorSimple.
   
   
A questo punto, è necessario disporre di una sessione remota attiva di Windows PowerShell sul dispositivo.
   
![Comunicazione remota PowerShell tramite HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a>Connessione tramite HTTPS

La connessione a Windows PowerShell per StorSimple tramite una sessione HTTPS è il metodo più sicuro e consigliato di connessione remota al dispositivo Microsoft Azure StorSimple. Nelle procedure seguenti viene illustrato come configurare la console seriale e i computer client, in modo che sia possibile utilizzare HTTPS per connettersi a Windows PowerShell per StorSimple.

Per configurare la gestione remota, è possibile usare il portale di Azure o la console seriale. Selezionare una delle seguenti procedure:

* [Utilizzo del portale di Azure per abilitare la gestione remota su HTTPS](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [Utilizzo della console seriale per abilitare la gestione remota su HTTPS](#use-the-serial-console-to-enable-remote-management-over-https)

Dopo aver abilitato la gestione remota, utilizzare le procedure seguenti per preparare l'host per la gestione remota e connettersi al dispositivo dall'host remoto.

* [Preparazione dell'host per la gestione remota](#prepare-the-host-for-remote-management)
* [Connessione al dispositivo dall'host remoto](#connect-to-the-device-from-the-remote-host)

### <a name="use-the-azure-portal-to-enable-remote-management-over-https"></a>Utilizzo del portale di Azure per abilitare la gestione remota su HTTPS

Attenersi alla procedura seguente nel portale di Azure per abilitare la gestione remota su HTTPS.

#### <a name="to-enable-remote-management-over-https-from-the-azure-portal"></a>Per abilitare la gestione remota su HTTPS dal portale di Azure

1. Passare al servizio Gestione dispositivi StorSimple. Selezionare **Dispositivi** e quindi fare clic sul dispositivo che si vuole configurare per la gestione remota. Passare a **Impostazioni dispositivo > Sicurezza**.
2. Nel pannello **Impostazioni di sicurezza** fare clic su **Gestione remota**.
3. Impostare **Abilita gestione remota** su **Sì**.
4. È ora possibile scegliere di connettersi tramite HTTPS. (La connessione su HTTPS rappresenta la scelta predefinita.) Assicurarsi che HTTPS sia selezionato.
5. Fare clic su **Scarica il certificato di gestione remota**. Specificare un percorso per salvare il file. Sarà necessario installare questo certificato nel computer client o host che si userà per connettersi al dispositivo.
6. Alla richiesta di conferma fare clic su **Salva** e quindi su **Sì**.

### <a name="use-the-serial-console-to-enable-remote-management-over-https"></a>Utilizzo della console seriale per abilitare la gestione remota su HTTPS

Eseguire le operazioni seguenti nella console seriale del dispositivo per abilitare la gestione remota.

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a>Per abilitare la gestione remota tramite la console seriale del dispositivo:
1. Nel menu della console seriale, selezionare l'opzione 1. Per altre informazioni sull'uso della console seriale del dispositivo, vedere [Connessione a Windows PowerShell per StorSimple tramite la console seriale del dispositivo](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. Al prompt dei comandi, digitare: 
   
     `Enable-HcsRemoteManagement`
   
    Ciò dovrebbe abilitare HTTPS sul dispositivo.
3. Verificare che HTTPS sia abilitato digitando: 
   
     `Get-HcsSystem`
   
    Assicurarsi che il campo **RemoteManagementMode** contenga **HttpsEnabled**. La figura seguente mostra queste impostazioni in PuTTY.
   
     ![Seriale HTTPS abilitato](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. Dall'output di `Get-HcsSystem`, copiare il numero di serie del dispositivo e salvarlo per un utilizzo successivo.
   
   > [!NOTE]
   > Il numero di serie esegue il mapping sul nome CN nel certificato.
   
5. Ottenere un certificato di gestione remota digitando: 
   
     `Get-HcsRemoteManagementCert`
   
    Verrà visualizzato un certificato simile al seguente.
   
    ![Ottenimento del certificato di gestione remota](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. Copiare le informazioni sul certificato da **-----BEGIN CERTIFICATE-----** a **-----END CERTIFICATE-----** in un editor di testo come Blocco note e salvarlo come file con estensione .cer. (Il file dovrà essere copiato sull'host remoto quando si prepara l'host.)
   
   > [!NOTE]
   > Per generare un nuovo certificato, utilizzare il cmdlet `Set-HcsRemoteManagementCert`.
   
### <a name="prepare-the-host-for-remote-management"></a>Preparazione dell'host per la gestione remota

Per preparare il computer host per una connessione remota che utilizza una sessione HTTPS, eseguire le procedure seguenti:

* [Importazione del file con estensione .cer nell'archivio radice del client o dell'host remoto](#to-import-the-certificate-on-the-remote-host)
* [Aggiunta dei numeri di serie del dispositivo al file hosts sull'host remoto](#to-add-device-serial-numbers-to-the-remote-host)

Ognuna di queste procedure è descritta di seguito.

#### <a name="to-import-the-certificate-on-the-remote-host"></a>Per importare il certificato nell'host remoto:
1. Fare clic con il pulsante destro del mouse sul file con estensione .cer e selezionare **Installa certificato**. Viene avviata l'Esportazione guidata certificati.
   
    ![Impostazione guidata del certificato 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. Per **Percorso archivio**, selezionare **Computer locale**, quindi fare clic su **Avanti**.
3. Selezionare **Colloca tutti i certificati nel seguente archivio**, quindi fare clic su **Sfoglia**. Passare all'archivio radice dell'host remoto, quindi fare clic su **Avanti**.
   
    ![Impostazione guidata del certificato 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. Fare clic su **Finish**. Viene visualizzato un messaggio indicante che l'importazione è avvenuta correttamente.
   
    ![Impostazione guidata del certificato 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="to-add-device-serial-numbers-to-the-remote-host"></a>Per aggiungere i numeri di serie del dispositivo all'host remoto:
1. Avviare Blocco note come amministratore, quindi aprire il file hosts che si trova in \Windows\System32\Drivers\etc.
2. Aggiungere le tre voci seguenti al file hosts: **DATA 0 IP address**, **Controller 0 Fixed IP address** e **Controller 1 Fixed IP address**.
3. Immettere il numero di serie salvato in precedenza. Eseguirne il mapping all'indirizzo IP come illustrato nella figura seguente. Per Controller 0 e Controller 1, aggiungere **Controller0** e **Controller1** alla fine del numero di serie (nome CN).
   
    ![Aggiunta del nome CN al file hosts](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. Salvare il file hosts.

### <a name="connect-to-the-device-from-the-remote-host"></a>Connessione al dispositivo dall'host remoto

Utilizzare Windows PowerShell e SSL per accedere a una sessione SSAdmin sul dispositivo da un client o un host remoto. Viene eseguito il mapping della sessione SSAdmin all'opzione 1 del menu [console seriale](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) del dispositivo.

Eseguire la procedura seguente sul computer da cui si desidera effettuare la connessione remota di Windows PowerShell.

#### <a name="to-enter-an-ssadmin-session-on-the-device-by-using-windows-powershell-and-ssl"></a>Per accedere a una sessione SSAdmin sul dispositivo tramite Windows PowerShell e SSL:
1. Avviare una sessione di Windows PowerShell come amministratore.
2. Aggiungere l'indirizzo IP del dispositivo agli host attendibili del client digitando:
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    Dove <*ip_dispositivo*> è l'indirizzo IP del dispositivo, ad esempio: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Per creare una nuova credenziale digitare:
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    Dove <*IP del dispositivo di destinazione*> è l'indirizzo IP di DATA 0 per il dispositivo, ad esempio, **10.126.173.90** come illustrato nell'immagine precedente del file hosts. Inoltre, fornire la password di amministratore per il dispositivo.
4. Creare una sessione digitando:
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    Per il parametro -ComputerName nel cmdlet, specificare il <*numero di serie del dispositivo di destinazione*>. Questo numero di serie è stato mappato all'indirizzo IP di DATA 0 nel file hosts sull'host remoto; ad esempio, **SHX0991003G44MT** come illustrato nella figura seguente.
5. Digitare:
   
     `Enter-PSSession $session`
6. Sarà necessario attendere alcuni minuti, quindi verrà effettuata la connessione al dispositivo tramite HTTPS su SSL. Verrà visualizzato un messaggio indicante che è stata effettuata la connessione al dispositivo.
   
    ![Comunicazione remota PowerShell tramite HTTPS e SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a>Passaggi successivi

* Leggere ulteriori informazioni sull' [utilizzo di Windows PowerShell per amministrare il dispositivo StorSimple](storsimple-8000-windows-powershell-administration.md).
* Altre informazioni sull'[utilizzo del servizio Gestione dispositivi StorSimple per la gestione del dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

