<!--author=SharS last changed: 02/04/2016-->

#### <a name="toocreate-a-volume"></a>toocreate un volume
1. Nel dispositivo hello **avvio rapido** pagina, fare clic su **aggiungere un volume**. Verrà avviata l'aggiunta guidata volume hello.
2. In hello Aggiungi un volume, in **le impostazioni di base**, hello seguenti:
   
   1. Digitare un **Nome** per il volume.
   2. Specificare hello **capacità fornita** per il volume in GB o TB. capacità del volume Hello deve essere compreso tra 1 GB e 64 TB per un dispositivo fisico.
   3. Nell'elenco a discesa hello selezionare hello **tipo di utilizzo** per il volume. 
   4. Se si utilizza questo volume per i dati di archiviazione, selezionare hello **usare questo volume per i dati dell'archivio si accede di frequente** casella di controllo. Per tutti gli altri casi, selezionare semplicemente **Volume a livelli**. I volumi a livelli erano in precedenza denominati volumi primari.
      
        ![Aggiungi volume](./media/storsimple-create-volume/ScreenshotUpdate1VolumeFlow.png)
      
      1. Fare clic sull'icona di freccia hello ![icona a forma di freccia](./media/storsimple-create-volume/HCS_ArrowIcon-include.png) toogo toohello la pagina successiva.
3. In hello **impostazioni aggiuntive** nella finestra di dialogo, aggiungere un nuovo record di controllo di accesso (ACR):
   
   1. Fornire un **Nome** per l'ACR.
   2. In **nome iniziatore iSCSI**, fornire hello iSCSI nome qualificato dell'host Windows. Se non si dispone di hello IQN, andare troppo[Get hello nome qualificato iSCSI di un host Windows Server](#get-the-iqn-of-a-windows-server-host).
   3. Si consiglia di abilitare un backup predefinito selezionando hello **abilitare un backup predefinito per questo volume** casella di controllo. backup predefinito Hello creerà un criterio che viene eseguita alle 22.30 ogni giorno (ora del dispositivo) e crea uno snapshot cloud del volume.
      
      > [!NOTE]
      > Backup di hello è abilitato in questo caso, non può essere ripristinato. È necessario tooedit hello volume toomodify questa impostazione.
      > 
      > 
      
        ![Aggiungi volume](./media/storsimple-create-volume/AddVolume2-include.png)
4. Fare clic sull'icona di controllo hello ![icona del segno di spunta](./media/storsimple-create-volume/HCS_CheckIcon-include.png). Verrà creato un volume con hello specificato le impostazioni.

![Video disponibile](./media/storsimple-create-volume/Video_icon.png)**Video disponibile**

toowatch un video che illustra come toocreate un volume StorSimple, fare clic su [qui](https://azure.microsoft.com/documentation/videos/create-a-storsimple-volume/).

