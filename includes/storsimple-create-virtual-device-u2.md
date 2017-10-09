#### <a name="toocreate-a-virtual-device"></a>toocreate un dispositivo virtuale
1. Nel portale di Azure hello, passare toohello **StorSimple Manager** servizio.
2. Passare toohello **dispositivi** pagina. Fare clic su **dispositivo virtuale crea** nella parte inferiore di hello di hello **dispositivi** pagina.
3. In hello **la finestra di dialogo Crea dispositivo virtuale**, specificare i seguenti dettagli hello.
   
    ![StorSimple crea dispositivo virtuale](./media/storsimple-create-virtual-device-u2/CreatePremiumsva1.png)
   
   1. **Nome** : un nome univoco per il dispositivo virtuale.
   2. **Modello** -scegliere il modello di hello del dispositivo virtuale hello. Questo campo viene visualizzato solo se si esegue Update 2 o versione successiva. Un modello di dispositivo 8010 offre 30 TB di spazio di archiviazione Standard mentre 8020 dispone di 64 TB di spazio di archiviazione Premium. Specificare 8010
   3. scenari di recupero di livello elemento toodeploy dai backup. Selezionare 8020 toodeploy ad alte prestazioni, i carichi di lavoro di latenza bassa o utilizzato come un dispositivo per il ripristino di emergenza secondario.
   4. **Versione** -scegliere la versione di hello del dispositivo virtuale hello. Se un modello di dispositivo 8020 è selezionato, quindi il campo della versione hello non verrà presentato toohello utente. Questa opzione non è presente se tutti hello fisico dispositivi registrati con questo servizio esegue Update 1 (o versione successiva). Questo campo viene visualizzato solo se si dispone di una combinazione di pre-aggiornamento 1 e l'aggiornamento 1 di dispositivi fisici registrati con hello stesso servizio. Versione del dispositivo virtuale hello specificato hello determina quale dispositivo fisico, è possibile failover o la clonazione da, è importante creare una versione appropriata del dispositivo virtuale hello. Selezionare:
      
      * Update 0.3 se si prevede di eseguire il failover o il ripristino di emergenza da un dispositivo fisico che esegue Update 0.3 o versione precedente. 
      * Update 1 se si prevede di eseguire il failover o la clonazione da un dispositivo fisico che esegue Update1 (o versione successiva). 
   5. **Rete virtuale** : specificare una rete virtuale che si desidera toouse con questo dispositivo virtuale. Se si utilizza l'archiviazione Premium (Update 2 o versione successiva), è necessario selezionare una rete virtuale è supportata con l'account di archiviazione Premium hello. reti virtuali Hello non supportato è disponibile nell'elenco a discesa hello. Verrà visualizzato un avviso se si seleziona una rete virtuale non supportata. 
   6. **Account di archiviazione per la creazione di un dispositivo virtuale** -selezionare un'immagine hello toohold account di archiviazione del dispositivo virtuale hello durante il provisioning. Questo account di archiviazione deve trovarsi in hello stessa area dispositivo virtuale hello e una rete virtuale. Non deve essere usato per archiviazione di dati da hello fisico o dispositivo virtuale hello. Per effettuare questa operazione, verrà creato un nuovo account di archiviazione (impostazione predefinita). Tuttavia, se si conosce l'hai già un account di archiviazione che è adatto a questo scopo, è possibile selezionarlo hello elenco. Se la creazione di un dispositivo virtuale premium, l'elenco a discesa hello verrà visualizzati solo gli account di archiviazione Premium. 
      
      > [!NOTE]
      > dispositivo virtuale Hello funzionano solo con gli account di archiviazione di Azure hello. Altri provider di servizi cloud come Amazon, HP e OpenStack (che sono supportati per il dispositivo fisico hello) non sono supportati per il dispositivo virtuale StorSimple di hello.
      > 
      > 
   7. Fare clic su tooindicate segno di spunta hello è comprendere che i dati di hello archiviati nel dispositivo virtuale hello verranno ospitati in un Data Center Microsoft. Quando si utilizza soltanto un dispositivo fisico, la chiave di crittografia viene conservata nel dispositivo; di conseguenza, Microsoft non può decrittografarli. 
      
       Quando si utilizza un dispositivo virtuale, la chiave di crittografia hello sia la chiave di decrittografia hello vengono archiviati in Microsoft Azure. Per altre informazioni, vedere le [considerazioni relative alla sicurezza per l'uso di un dispositivo virtuale](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security).
   8. Fare clic su dispositivo virtuale di hello controllo icona toocreate hello. dispositivo Hello potrebbe richiedere circa 30 minuti toobe, che il provisioning.
      
      ![Dispositivo virtuale StorSimple fase di creazione](./media/storsimple-create-virtual-device-u2/StorSimple_VirtualDeviceCreating1M.png)

