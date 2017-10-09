<!--author=SharS last changed: 12/01/15-->

### <a name="step-1-authorize-a-device-toochange-hello-service-data-encryption-key-in-hello-azure-classic-portal"></a>Passaggio 1: Autorizzare una dispositivo toochange hello chiave DEK del servizio nel portale di Azure classico hello
Amministratore del dispositivo hello richiede in genere, tale amministratore del servizio hello autorizzare un dispositivo toochange crittografia le chiavi del servizio. amministratore del servizio Hello autorizza quindi chiave hello toochange del dispositivo hello.

Questo passaggio viene eseguito nel portale di Azure classico hello. amministratore del servizio Hello è possibile selezionare un dispositivo di un elenco dei dispositivi hello idonei toobe autorizzato. dispositivo di Hello è quindi il processo di modifica della chiave DEK del servizio autorizzato toostart hello.

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>Quali dispositivi possono essere autorizzate toochange chiavi DEK del servizio?
Un dispositivo deve soddisfare i seguenti criteri prima di poter essere autorizzato tooinitiate servizio modifica della chiave DEK hello:

* dispositivo di Hello deve essere online toobe idonei per l'autorizzazione di modifica della chiave di servizio dati crittografia.
* È possibile autorizzare hello stesso dispositivo nuovamente dopo 30 minuti se la chiave hello modifica non è stato avviato.
* È possibile autorizzare un dispositivo diverso, purché modifica della chiave hello non è stata avviata dal dispositivo autorizzato in precedenza hello. Dopo che è stato autorizzato alla nuova periferica hello, dispositivo precedente hello Impossibile iniziare la modifica di hello.
* Non è possibile autorizzare un dispositivo mentre è in corso hello rollover della chiave DEK del servizio hello.
* È possibile autorizzare un dispositivo quando alcuni dispositivi hello registrati con il servizio hello hanno eseguito il rollover crittografia hello ma non per altri utenti. In questi casi, i dispositivi idonei hello sono quelli che hanno completato hello servizio modifica della chiave DEK hello.

> [!NOTE]
> Nel portale di Azure classico hello, nell'elenco di hello dei dispositivi che possono non essere vengono visualizzati i dispositivi virtuali StorSimple autorizzato modifica della chiave toostart hello.
> 
> 

Eseguire i seguenti passaggi tooselect hello e autorizzare una dispositivo tooinitiate hello servizio modifica della chiave DEK.

#### <a name="tooauthorize-a-device-toochange-hello-key"></a>una chiave di hello toochange dispositivo tooauthorize
1. Nella pagina dashboard del servizio hello, fare clic su **Modifica chiave DEK del servizio**.
   
    ![Modificare la chiave di crittografia del servizio](./media/storsimple-change-data-encryption-key/HCS_ChangeServiceDataEncryptionKey-include.png)
2. In hello **Modifica chiave DEK del servizio** finestra di dialogo, selezionare e autorizzare una dispositivo tooinitiate hello servizio modifica della chiave DEK. elenco di riepilogo a discesa Hello contiene tutti i dispositivi idonei hello che possono essere autorizzati.
3. Fare clic sull'icona di controllo hello ![icona del segno di spunta](./media/storsimple-change-data-encryption-key/HCS_CheckIcon-include.png).

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>Passaggio 2: Utilizzo di Windows PowerShell per StorSimple tooinitiate hello servizio modifica della chiave DEK
Questo passaggio viene eseguito in hello Windows PowerShell per StorSimple interfaccia hello autorizzato dispositivo StorSimple.

> [!NOTE]
> Alcun operazioni non possono essere eseguite nel portale di Azure classico del servizio StorSimple Manager hello fino al completamento di rollover della chiave hello.
> 
> 

Se si utilizza l'interfaccia di Windows PowerShell toohello hello dispositivo console seriale tooconnect, eseguire hello alla procedura seguente.

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>modifica della chiave DEK del servizio tooinitiate hello
1. Selezionare l'opzione 1 toolog nella con accesso completo.
2. Al prompt dei comandi di hello, digitare:
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Al termine hello cmdlet, si otterrà una nuova chiave DEK del servizio. Copiare e salvare la chiave per l'uso nel passaggio 3 di questo processo. Questa chiave verrà usata tooupdate hello tutti i dispositivi registrati con il servizio StorSimple Manager hello rimanenti.
   
   > [!NOTE]
   > Questo processo deve essere avviato entro quattro ore dall'autorizzazione di un dispositivo StorSimple.
   > 
   > 
   
   La nuova chiave viene quindi inviata toohello servizio toobe inserito tooall hello di dispositivi registrati con il servizio di hello. Un avviso verrà quindi visualizzati nel dashboard del servizio hello. servizio Hello disabiliterà tutte le operazioni di hello nei dispositivi registrato hello e amministratore del dispositivo hello sarà quindi necessario tooupdate hello chiave DEK del servizio su hello altri dispositivi. Tuttavia, hello i/o (host di invio di dati nel cloud toohello) non verranno compromesse.
   
   Se dispone di un singolo dispositivo registrato tooyour servizio, il processo di rollover hello è stato completato ed è possibile ignorare il passaggio di hello. Se si dispone di più dispositivi registrati tooyour servizio, procedere toostep 3.

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>Passaggio 3: Aggiornare hello chiave DEK del servizio su altri dispositivi StorSimple
Se si dispone di più dispositivi registrati tooyour StorSimple Manager servizio, è necessario effettuare questi passaggi nell'interfaccia di Windows PowerShell hello del dispositivo StorSimple. chiave Hello ottenuta nel passaggio 2: utilizzo di Windows PowerShell per StorSimple tooinitiate hello servizio modifica della chiave DEK deve essere utilizzato tooupdate tutti hello rimanenti dispositivo StorSimple registrato con hello servizio StorSimple Manager.

Eseguire hello dopo la crittografia dei dati di passaggi tooupdate hello servizio nel dispositivo.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>chiave di crittografia tooupdate hello servizio dati
1. Usare Windows PowerShell per StorSimple tooconnect toohello console. Selezionare l'opzione 1 toolog nella con accesso completo.
2. Al prompt dei comandi di hello, digitare:
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Fornire hello chiave DEK del servizio ottenuta nel [passaggio 2: utilizzo di Windows PowerShell per StorSimple tooinitiate hello servizio modifica della chiave DEK](#to-initiate-the-service-data-encryption-key-change).

