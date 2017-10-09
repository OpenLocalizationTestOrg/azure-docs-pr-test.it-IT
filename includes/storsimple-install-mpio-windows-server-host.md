#### <a name="tooinstall-mpio-on-hello-host"></a>tooinstall MPIO nell'host di hello
1. Aprire Server Manager nell'host Windows Server. Per impostazione predefinita, Server Manager viene avviato quando un membro del gruppo Administrators hello accede tooa computer che esegue Windows Server 2012 R2 o Windows Server 2012. Se hello Server Manager non è già aperto, fare clic su **Start > Server Manager**.
   
    ![Server Manager](./media/storsimple-install-mpio-windows-server/IC740997.png)
2. Fare clic su **Server Manager > Dashboard > Aggiungi ruoli e funzionalità**. Verrà avviata hello **Aggiungi ruoli e funzionalità** procedura guidata.
   
    ![Aggiunta guidata ruoli e funzionalità 1](./media/storsimple-install-mpio-windows-server/IC740998.png)
3. In hello **Aggiungi ruoli e funzionalità** guidata hello seguenti:
   
   * In hello **prima di iniziare** pagina, fare clic su **Avanti**.
   * In hello **Selezione tipo di installazione** accettare l'impostazione predefinita hello **basata su ruoli o basata su funzionalità** installazione. Fare clic su **Avanti**.
     
       ![Aggiunta guidata ruoli e funzionalità 2](./media/storsimple-install-mpio-windows-server/IC740999.png)
   * In hello **Selezione server di destinazione** pagina, scegliere **selezionare un server dal pool di server hello**. Il server host deve essere rilevato automaticamente. Fare clic su **Avanti**.
   * In hello **Selezione ruoli server** pagina, fare clic su **Avanti**.
   * In hello **Selezione funzionalità** selezionare **Multipath i/o**, fare clic su **Avanti**.
     
       ![Aggiunta guidata ruoli e funzionalità 5](./media/storsimple-install-mpio-windows-server/IC741000.png)
   * In hello **Conferma selezioni per l'installazione** pagina, confermare la selezione di hello e quindi selezionare **riavvio del server di destinazione hello automaticamente se necessario**, come illustrato di seguito. Fare clic su **Installa**.
     
       ![Aggiunta guidata ruoli e funzionalità 8](./media/storsimple-install-mpio-windows-server/IC741001.png)
   * Riceverà la notifica al termine dell'installazione di hello. Fare clic su **Chiudi** guidata hello tooclose.
     
       ![Aggiunta guidata ruoli e funzionalità 9](./media/storsimple-install-mpio-windows-server/IC741002.png)

