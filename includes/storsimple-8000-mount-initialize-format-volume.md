<!--author=SharS last changed: 9/17/15-->

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount, inizializzare e formattare un volume
1. Avviare l'iniziatore iSCSI Microsoft di hello.
2. In hello **iniziatore iSCSI-proprietà** finestra hello **individuazione** scheda, fare clic su **individua portale**.
3. In hello **individua portale destinazione** nella finestra di dialogo specificare hello di indirizzo IP dell'interfaccia di rete abilitata per iSCSI e quindi fare clic su **OK**. 
4. In hello **iniziatore iSCSI-proprietà** finestra hello **destinazioni** , individuare hello **individuati destinazioni**. stato del dispositivo Hello dovrebbe essere visualizzato come **inattivo**.
5. Selezionare il dispositivo di destinazione hello e quindi fare clic su **Connetti**. Dopo che hello dispositivo è connesso, lo stato di hello deve modificare troppo**connesso**. (Per ulteriori informazioni sull'uso dell'iniziatore iSCSI Microsoft di hello, vedere [installazione e configurazione iniziatore iSCSI Microsoft][1]).
6. Nell'host di Windows, premere tasto Logo Windows hello + X e quindi fare clic su **eseguire**. 
7. In hello **eseguire** della finestra di dialogo tipo **Diskmgmt.msc**. Fare clic su **OK**, hello e **Gestione disco** verrà visualizzata la finestra di dialogo. riquadro di destra Hello mostrerà volumi hello sull'host.
8. In hello **Gestione disco** finestra hello volumi montati vengono visualizzati come mostrato nella seguente figura hello. Mouse sul volume hello individuato (fare clic su nome hello del disco), quindi fare clic su **Online**.
   
     ![Avvia formattazione volume](./media/storsimple-8000-mount-initialize-format-volume/step7initializeformatvolume.png) 
9. Mouse sul volume hello (scegliere il nome del disco hello), quindi fare clic su **inizializzare**.
10. tooformat un volume semplice, eseguire hello alla procedura seguente:
    
    1. Selezionare il volume di hello, farvi clic scegliendo area hello a destra, fare clic su **nuovo Volume semplice**.
    2. Nella procedura guidata nuovo Volume semplice hello, specificare una lettera di unità e delle dimensioni del volume hello e configurare il volume di hello come un file system NTFS.
    3. Specificare una dimensione unità di allocazione pari a 64 KB. Questa dimensione di unità di allocazione funziona bene con gli algoritmi di deduplicazione hello utilizzati nella soluzione StorSimple hello.
    4. Eseguire una formattazione veloce.

<!--Link references-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx
