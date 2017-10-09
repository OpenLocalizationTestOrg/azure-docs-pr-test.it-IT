#### <a name="toocreate-a-cloud-appliance"></a>toocreate un'applicazione cloud

1. Nel portale di Azure hello, passare toohello **Gestione dispositivi StorSimple** servizio.
2. Passare toohello **dispositivi** blade. Dalla barra dei comandi hello nel Pannello di riepilogo servizio hello, fare clic su **appliance di cloud crea**.
    ![Creazione dell'appliance cloud di StorSimple](./media/storsimple-8000-create-cloud-appliance-u2/sca-create1.png)
3. In hello **appliance di cloud crea** pannello, specificare i seguenti dettagli hello.
   
    ![Creazione dell'appliance cloud di StorSimple](./media/storsimple-8000-create-cloud-appliance-u2/sca-create2m.png)
   
   1. **Nome**: nome univoco per l'appliance cloud.
   2. **Modello** -scegliere il modello di hello del dispositivo cloud hello. Un dispositivo 8010 offre 30 TB di spazio di archiviazione Standard mentre un dispositivo 8020 fornisce 64 TB di spazio di archiviazione Premium. Specificare 8010 scenari il recupero a livello di elemento di toodeploy dai backup. Selezionare 8020 toodeploy ad alte prestazioni, i carichi di lavoro a bassa latenza, o utilizzare come un dispositivo per il ripristino di emergenza secondario.
   3. **Versione** -scegliere la versione di hello del dispositivo cloud hello. versione di Hello corrisponde toohello versione dell'immagine del disco virtuale che è usato toocreate hello cloud accessorio hello. La versione di hello del cloud hello specificate dispositivo determina quale fisica dispositivo eseguire il failover o la clonazione da, è importante creare una versione appropriata di appliance di cloud hello.
   4. **Rete virtuale** : specificare una rete virtuale che si desidera toouse con applicazione cloud. Se si utilizza l'archiviazione Premium, è necessario selezionare una rete virtuale è supportata con l'account di archiviazione Premium hello. reti virtuali Hello non supportata sono inattive nell'elenco a discesa hello. Viene visualizzato un avviso se si seleziona una rete virtuale non supportata.
   5. **Subnet** -basate sulla rete virtuale di hello selezionato, elenco a discesa hello Visualizza subnet hello associata. Assegnare un'applicazione cloud tooyour di subnet.
   6. **Account di archiviazione** -selezionare un'immagine hello toohold account di archiviazione del dispositivo cloud hello durante il provisioning. Questo account di archiviazione deve trovarsi in hello stessa area appliance di cloud hello e una rete virtuale. Non deve essere usato per archiviazione di dati hello fisico o dispositivo cloud hello. Per impostazione predefinita, viene creato un nuovo account di archiviazione per questo scopo specifico. Tuttavia, se si conosce l'hai già un account di archiviazione che è adatto a questo scopo, è possibile selezionarlo hello elenco. Se la creazione di un'applicazione cloud premium, elenco a discesa hello Visualizza solo gli account di archiviazione Premium.
      
      > [!NOTE]
      > dispositivo cloud Hello funzionano solo con gli account di archiviazione di Azure hello.
    
   7. Selezionare hello tooindicate di casella di controllo che è comprendere che i dati di hello archiviati nel dispositivo cloud hello sono ospitati in un Data Center Microsoft.
       * Quando si utilizza soltanto un dispositivo fisico, la chiave di crittografia viene conservata nel dispositivo; di conseguenza, Microsoft non può decrittografarli.

       * Quando si usa un'applicazione cloud, sia la chiave di crittografia hello e chiave di decrittografia hello vengono archiviati in Microsoft Azure. Per altre informazioni, vedere le [considerazioni relative alla sicurezza per l'uso di un'appliance cloud](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security).
   8. Fare clic su **crea** appliance di cloud tooprovision hello. dispositivo Hello potrebbe richiedere circa 30 minuti toobe, che il provisioning. Ricevere notifiche quando il dispositivo di cloud hello viene creato correttamente. Andare a pannello tooDevices ed elenco hello dei dispositivi Aggiorna appliance di cloud toodisplay hello. è stato Hello del dispositivo hello **pronto tooset backup**.
      
      ![StorSimple Appliance di Cloud tooset pronto backup](./media/storsimple-8000-create-cloud-appliance-u2/sca-create3.png)

