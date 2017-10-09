<!--author=alkohli last changed: 9/17/15-->

#### <a name="tooadd-a-storage-account-in-storsimple-8000-series-update-10"></a>un account di archiviazione StorSimple 8000 Series aggiornamento 1.0 tooadd
1. Nel servizio StorSimple Manager hello pagina di destinazione, selezionare il servizio e fare doppio clic. L'operazione richiederà toohello **avvio rapido** pagina. Seleziona hello **configura** pagina.
2. Fare clic su **Aggiungi/modifica account di archiviazione**.
3. In hello **Aggiungi/modifica Account di archiviazione** la finestra di dialogo, fare clic su **Aggiungi nuovo**.
4. In hello **Provider** provider di servizi di hello selezionare il cloud appropriato. provider di Hello supportato sono Azure, S3 Amazon, Amazon S3 con record di risorse, HP e OpenStack. Specificare le credenziali di hello e posizione hello associata con l'account di archiviazione hello di fornitori di servizi cloud. campi di Hello presentati le credenziali saranno diversi in base al provider di servizi cloud hello che è stato specificato. 
   
   * Se si è scelto Azure come provider di servizi cloud, specificare hello **nome** e hello primario **chiave di accesso** per l'account di archiviazione di Microsoft Azure. Per un account Azure, il percorso di hello verrà popolato automaticamente.
     
        ![Account un account di archiviazione di Azure](./media/storsimple-configure-new-storage-account-u1/AddAzureStorageaccount-include.png)
   * Se è stato selezionato Amazon S3 o Amazon S3 con RRS, specificare un **nome account di archiviazione** descrittivo, una **chiave di accesso** e una **chiave privata**. Per S3 Amazon e S3 Amazon con record di risorse, supportato hello posizioni seguenti:
     
     * Stati Uniti Standard
     * Stati Uniti occidentali (Oregon)
     * Stati Uniti occidentali (California settentrionale)
     * Europa (Irlanda)
     * Asia Pacifico (Singapore)
     * Asia Pacifico (Sydney)
     * Asia Pacifico (Tokyo)
     * America meridionale (Sao Paulo)
       
       ![Account un account di archiviazione di Amazon](./media/storsimple-configure-new-storage-account-u1/AddAmazonStorageaccount-include.png)
   * Se è stato selezionato HP come provider di servizi cloud, specificare un **nome account di archiviazione** descrittivo, un **ID tenant**, un **nome utente** e una **password**. Per HP, è supportata hello posizioni seguenti:
     
     * Stati Uniti orientali
     * Stati Uniti occidentali
       
       ![Aggiungere un account di archiviazione di HP](./media/storsimple-configure-new-storage-account-u1/AddHPStorageaccount-include.png)
   * Se è stato selezionato **Openstack** come provider di servizi cloud, specificare un **nome host**, una **chiave di accesso** e una **chiave privata**.
     
     > [!NOTE]
     > Per tutti i provider del servizio cloud hello, esclusione di Azure, è consentito un nome descrittivo. È possibile utilizzare nomi descrittivi di diversi e creare più di un account di archiviazione con hello stesso insieme di credenziali.
     > 
     > 
     
        ![Aggiungere un account di archiviazione di Openstack](./media/storsimple-configure-new-storage-account-u1/AddOpenstackStorageaccount-include.png)
5. Selezionare **Abilita modalità SSL** toocreate un canale sicuro per la comunicazione di rete tra il dispositivo e hello di cloud. Crittografato hello **Abilita modalità SSL** casella di controllo solo se si sta operando all'interno di un cloud privato.
   
   > [!NOTE]
   > Se si usa HP come provider, SSL viene sempre abilitato.
   > 
   > 
6. Fare clic sull'icona di controllo hello ![icona del segno di spunta](./media/storsimple-configure-new-storage-account/HCS_CheckIcon-include.png). Dopo la creazione dell'account di archiviazione hello si riceverà la notifica.
7. Hello account di archiviazione appena creato verrà visualizzato nella hello **configura** pagina **gli account di archiviazione**. Fare clic su **salvare** toosave hello nuovo account di archiviazione. Fare clic su **OK** quando viene richiesto di confermare.

