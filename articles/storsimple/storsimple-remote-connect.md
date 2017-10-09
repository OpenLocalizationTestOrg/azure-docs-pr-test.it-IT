---
title: aaaConnect in remoto il dispositivo di StorSimple tooyour | Documenti Microsoft
description: Viene illustrato come tooconfigure il dispositivo per la gestione remota e come tooconnect tooWindows PowerShell per StorSimple tramite HTTP o HTTPS.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 55ed8fcdd997901301e0adc164a302216cde0332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a>Connettersi in remoto il dispositivo di serie StorSimple 8000 tooyour

## <a name="overview"></a>Panoramica
È possibile utilizzare il dispositivo StorSimple tooyour di Windows PowerShell remoting tooconnect. Quando ci si connette in questo modo, non verrà visualizzato un menu. (Verrà visualizzato un menu solo se si utilizza la console seriale hello in hello dispositivo tooconnect). Con la comunicazione remota di Windows PowerShell, è connettersi tooa spazio di esecuzione specifico. È inoltre possibile specificare la lingua di visualizzazione hello. 

Per ulteriori informazioni sull'utilizzo toomanage di comunicazione remota di Windows PowerShell del dispositivo, andare troppo[utilizzare Windows PowerShell per StorSimple tooadminister dispositivo StorSimple](storsimple-windows-powershell-administration.md).

In questa esercitazione viene illustrato come tooconfigure del dispositivo per la gestione remota e come quindi tooconnect tooWindows PowerShell per StorSimple. È possibile utilizzare HTTP o HTTPS tooconnect tramite comunicazione remota di Windows PowerShell. Tuttavia, quando si decide come tooconnect tooWindows PowerShell per StorSimple, considerare l'esempio hello: 

* La connessione diretta toohello console seriale del dispositivo è protetto, ma connessione toohello console seriale tramite commutatori di rete non è. Prestare attenzione hello rischi di sicurezza durante la connessione toohello console seriale del dispositivo tramite commutatori di rete. 
* Connessione tramite una sessione HTTP può offrire maggiore sicurezza rispetto alla connessione tramite la console seriale hello su hello. Anche se non si tratta metodo più sicuro hello, è accettabile su reti attendibili. 
* Connessione tramite una sessione HTTPS con un certificato autofirmato è hello più sicura e hello opzione consigliata.

È possibile connettersi in remoto toohello interfaccia di Windows PowerShell. Dispositivo StorSimple tooyour di accesso remoto tramite l'interfaccia di Windows PowerShell hello, tuttavia, non è abilitato per impostazione predefinita. Necessario tooenable gestione remota sul dispositivo hello prima e quindi su hello client tooaccess usato il dispositivo.

passaggi di Hello descritti in questo articolo sono stati eseguiti in un sistema host che esegue Windows Server 2012 R2.

## <a name="connect-through-http"></a>Connessione tramite HTTP
La connessione tooWindows PowerShell per StorSimple tramite una sessione HTTP offre maggiore sicurezza rispetto alla connessione tramite hello console seriale del dispositivo StorSimple. Anche se non si tratta metodo più sicuro hello, è accettabile su reti attendibili.

È possibile utilizzare hello portale di Azure classico o la gestione remota di hello console seriale tooconfigure. Selezionare hello seguire le procedure seguenti:

* [Usare la gestione remota di hello Azure tooenable portale classico su HTTP](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [Usare la gestione remota di hello console seriale tooenable su HTTP](#use-the-serial-console-to-enable-remote-management-over-http)

Dopo aver abilitato la gestione remota, utilizzare hello seguenti client di hello tooprepare procedure per una connessione remota.

* [Preparare il client di hello per la connessione remota](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-http"></a>Usare la gestione remota di hello Azure tooenable portale classico su HTTP
Eseguire hello seguendo i passaggi nella gestione remota di hello Azure tooenable portale classico tramite HTTP.

#### <a name="tooenable-remote-management-through-hello-azure-classic-portal"></a>gestione remota di tooenable tramite hello portale di Azure classico
1. Accedere a **Dispositivi** > **Configura** per il dispositivo.
2. Scorrere verso il basso toohello **gestione remota** sezione.
3. Impostare **abilitare gestione remota** troppo**Sì**.
4. È ora possibile scegliere tooconnect tramite HTTP. (valore predefinito di hello è tooconnect su HTTPS). Assicurarsi che HTTP sia selezionato.
   
   > [!NOTE]
   > La connessione tramite HTTP dovrebbe essere eseguita solo su reti attendibili.
   > 
   > 
5. Fare clic su **salvare** nella parte inferiore di hello della pagina hello.

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a>Usare la gestione remota di hello console seriale tooenable su HTTP
Eseguire hello seguendo i passaggi per la gestione remota tooenable hello dispositivo console seriale.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>gestione remota tramite console seriale del dispositivo hello tooenable
1. Nel menu della console seriale hello, selezionare l'opzione 1. Per ulteriori informazioni sull'utilizzo della console seriale hello sul dispositivo hello, andare troppo[connessione tooWindows PowerShell per StorSimple tramite console seriale del dispositivo](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. Al prompt dei comandi hello, digitare:`Enable-HcsRemoteManagement –AllowHttp`
3. Si riceverà la notifica sulle vulnerabilità della sicurezza hello di utilizzo di HTTP tooconnect toohello dispositivo. Quando richiesto, confermare digitando **Y**.
4. Verificare che HTTP sia abilitato digitando: `Get-HcsSystem`
5. Verificare che hello **RemoteManagementMode** campo **HttpsAndHttpEnabled**.hello seguente figura illustra queste impostazioni in PuTTY.
   
     ![Seriali HTTPS e HTTP abilitati](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a>Preparare il client di hello per la connessione remota
Eseguire hello seguendo i passaggi per la gestione remota di hello client tooenable.

#### <a name="tooprepare-hello-client-for-remote-connection"></a>client hello tooprepare per la connessione remota
1. Avviare una sessione di Windows PowerShell come amministratore.
2. Indirizzo IP di hello tooadd dell'elenco di host attendibili del client di hello StorSimple dispositivo toohello dei comandi digitare quanto segue di hello: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     Sostituire <*device_ip*> con l'indirizzo IP di hello del dispositivo, ad esempio: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Credenziali del dispositivo toosave hello in una variabile di comando che segue hello di tipo: 
   
    ```
    $cred = Get-Credential
    ```
    
4. Nella finestra di dialogo hello che viene visualizzata:
   
   1. Digitare il nome utente hello in questo formato: *device_ip\SSAdmin*.
   2. Tipo hello password amministratore del dispositivo che è stata impostata quando il dispositivo di hello è stato configurato con l'installazione guidata di hello. password predefinita Hello è *Password1*.
5. Avviare una sessione di Windows PowerShell nel dispositivo hello digitando questo comando:
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > toocreate una sessione di Windows PowerShell per l'utilizzo con dispositivo virtuale StorSimple hello, accodare hello `–Port` parametro e specificare la porta pubblica hello configurati in servizi remoti per il dispositivo virtuale StorSimple.
   > 
   > 
   
     A questo punto, è necessario disporre di un dispositivo di toohello attivo di remoto Windows PowerShell sessione.
   
    ![Comunicazione remota PowerShell tramite HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a>Connessione tramite HTTPS
Connessione tooWindows PowerShell per StorSimple tramite una sessione HTTPS, è più sicuro hello e metodo di connessione in remoto i dispositivi di Microsoft Azure StorSimple tooyour consigliato. Hello, seguire le procedure seguenti spiegano come tooset backup hello seriali console e i computer client in modo che è possibile utilizzare HTTPS tooconnect tooWindows PowerShell per StorSimple.

È possibile utilizzare hello portale di Azure classico o la gestione remota di hello console seriale tooconfigure. Selezionare hello seguire le procedure seguenti:

* [Utilizzare la gestione remota di hello Azure tooenable portale classico su HTTPS](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [Utilizzare la gestione remota di hello console seriale tooenable su HTTPS](#use-the-serial-console-to-enable-remote-management-over-https)

Dopo aver abilitato la gestione remota, utilizzare hello seguenti host hello tooprepare di procedure per la gestione remota e connettere il dispositivo toohello dall'host remoto hello.

* [Preparare l'host di hello per la gestione remota](#prepare-the-host-for-remote-management)
* [Connettere il dispositivo di toohello dall'host remoto hello](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-https"></a>Utilizzare la gestione remota di hello Azure tooenable portale classico su HTTPS
Eseguire hello seguendo i passaggi nella gestione remota di hello Azure tooenable portale classico tramite HTTPS.

#### <a name="tooenable-remote-management-over-https-from-hello-azure-classic-portal"></a>gestione remota su HTTPS tooenable dal portale di Azure classico hello
1. Accedere a **Dispositivi** > **Configura** per il dispositivo.
2. Scorrere verso il basso toohello **gestione remota** sezione.
3. Impostare **abilitare gestione remota** troppo**Sì**.
4. È ora possibile scegliere tooconnect tramite HTTPS. (valore predefinito di hello è tooconnect su HTTPS). Assicurarsi che HTTPS sia selezionato. 
5. Fare clic su **Scarica certificato di gestione remota**. Specificare un percorso toosave questo file. È necessario tooinstall questo certificato nel computer client o host hello che si utilizzerà tooconnect toohello dispositivo.
6. Fare clic su **salvare** nella parte inferiore di hello della pagina hello.

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a>Utilizzare la gestione remota di hello console seriale tooenable su HTTPS
Eseguire hello seguendo i passaggi per la gestione remota tooenable hello dispositivo console seriale.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>gestione remota tramite console seriale del dispositivo hello tooenable
1. Nel menu della console seriale hello, selezionare l'opzione 1. Per ulteriori informazioni sull'utilizzo della console seriale hello sul dispositivo hello, andare troppo[connessione tooWindows PowerShell per StorSimple tramite console seriale del dispositivo](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. Al prompt dei comandi hello, digitare: 
   
     `Enable-HcsRemoteManagement`
   
    Ciò dovrebbe abilitare HTTPS sul dispositivo.
3. Verificare che HTTPS sia abilitato digitando: 
   
     `Get-HcsSystem`
   
    Verificare che tale hello **RemoteManagementMode** campo **HttpsEnabled**.hello seguente figura illustra queste impostazioni in PuTTY.
   
     ![Seriale HTTPS abilitato](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. Output di hello del `Get-HcsSystem`, copiare hello numero di serie del dispositivo hello e salvarlo per un uso successivo.
   
   > [!NOTE]
   > numero di serie Hello esegue il mapping nome CN toohello nel certificato hello.
   > 
   > 
5. Ottenere un certificato di gestione remota digitando: 
   
     `Get-HcsRemoteManagementCert`
   
    Verrà visualizzato un seguente toohello simile certificato.
   
    ![Ottenimento del certificato di gestione remota](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. Copiare le informazioni di hello certificato hello da **---BEGIN CERTIFICATE---** troppo**---END CERTIFICATE---** in un editor di testo quale Blocco note e salvarlo come file con estensione cer. (Verrà copiato l'host remoto tooyour di file quando si prepara l'host di hello.)
   
   > [!NOTE]
   > toogenerate un nuovo certificato, utilizzare hello `Set-HcsRemoteManagementCert` cmdlet.
   > 
   > 

### <a name="prepare-hello-host-for-remote-management"></a>Preparare l'host di hello per la gestione remota
computer host di hello tooprepare per una connessione remota che utilizza una sessione HTTPS, eseguire hello seguire le procedure seguenti:

* [File con estensione cer hello importazione nell'archivio radice hello del client hello o dell'host remoto](#to-import-the-certificate-on-the-remote-host).
* [Aggiungere file hosts toohello hello dispositivo numeri di serie dell'host remoto](#to-add-device-serial-numbers-to-the-remote-host).

Ognuna di queste procedure è descritta di seguito.

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a>certificato di hello tooimport nell'host remoto hello
1. Fare clic sul file con estensione cer hello e selezionare **Installa certificato**. Verrà avviata hello importazione guidata certificati.
   
    ![Impostazione guidata del certificato 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. Per **Percorso archivio**, selezionare **Computer locale**, quindi fare clic su **Avanti**.
3. Selezionare **colloca tutti i certificati nel seguente archivio hello**, quindi fare clic su **Sfoglia**. Passare l'archivio radice toohello dell'host remoto e quindi fare clic su **Avanti**.
   
    ![Impostazione guidata del certificato 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. Fare clic su **Finish**. Viene visualizzato un messaggio che indica che l'importazione di hello ha esito positivo.
   
    ![Impostazione guidata del certificato 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a>host remoto toohello tooadd dispositivo numeri di serie
1. Avviare Blocco note come amministratore e quindi aprire file hosts hello in \WINDOWS\system32\drivers\etc..
2. Aggiungere i seguenti tre voci tooyour host file hello: **indirizzo IP DATA 0**, **indirizzo IP fisso Controller 0**, e **indirizzo IP fisso Controller 1**.
3. Numero di serie hello dispositivo salvato in precedenza. Eseguire il mapping di questo indirizzo IP toohello come illustrato nella seguente immagine hello. Per Controller 0 e Controller 1, aggiungere **Controller0** e **Controller1** alla fine di hello del numero di serie hello (nome comune).
   
    ![Aggiunta del file toohosts nome CN](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. Salva file di host hello.

### <a name="connect-toohello-device-from-hello-remote-host"></a>Connettere il dispositivo di toohello dall'host remoto hello
Uso di Windows PowerShell e SSL tooenter una sessione SSAdmin nel dispositivo da un host remoto o un client. esegue il mapping di sessione SSAdmin Hello toooption 1 in hello [console seriale](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu del dispositivo.

Eseguire hello procedura nel computer di hello da cui si desidera toomake hello connessione remota di Windows PowerShell.

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a>tooenter una sessione SSAdmin nel dispositivo hello usando Windows PowerShell e SSL
1. Avviare una sessione di Windows PowerShell come amministratore.
2. Aggiungere hello dispositivo IP indirizzo toohello host attendibili del client, digitare:
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    Dove <*device_ip*> è l'indirizzo IP di hello del dispositivo, ad esempio: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Creare una nuova credenziale digitando: 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    Dove <*IP del dispositivo di destinazione*> è l'indirizzo IP hello di DATA 0 per il dispositivo; ad esempio, **10.126.173.90** come mostrato nella precedente immagine del file host hello hello. Fornire hello password di amministratore per il dispositivo.
4. Creare una sessione digitando:
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    Per il parametro - ComputerName hello nel cmdlet hello, fornire hello <*numero di serie del dispositivo di destinazione*>. È stato eseguito il mapping di questo numero di serie toohello di indirizzo IP di DATA 0 nel file hosts hello sull'host remoto; ad esempio, **SHX0991003G44MT** come illustrato nella seguente immagine hello.
5. Digitare: 
   
     `Enter-PSSession $session`
6. Sarà necessario toowait qualche minuto e quindi sarà tooyour connesso al dispositivo tramite HTTPS su SSL. Verrà visualizzato un messaggio che indica che si è connessi tooyour dispositivo.
   
    ![Comunicazione remota PowerShell tramite HTTPS e SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni, vedere [utilizzando tooadminister di Windows PowerShell del dispositivo StorSimple](storsimple-windows-powershell-administration.md).
* Altre informazioni, vedere [utilizzando hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

