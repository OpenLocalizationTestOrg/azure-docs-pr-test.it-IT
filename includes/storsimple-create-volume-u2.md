<!--author=alkohli last changed: 08/16/2016-->

#### <a name="toocreate-a-volume"></a>toocreate un volume
1. Nel dispositivo hello **avvio rapido** pagina, fare clic su **aggiungere un volume** toostart hello Aggiunta guidata volume.
2. In hello Aggiungi un volume, in **le impostazioni di base**:
   
   1. Digitare un **Nome** per il volume.
   2. Nell'elenco a discesa hello selezionare hello **tipo di utilizzo** per il volume. Per carichi di lavoro che richiedono garanzie locali, latenze basse e prestazioni più elevate, selezionare un volume **aggiunto in locale** . Per tutti gli altri dati, selezionare un volume **a livelli** . Se si usa questo volume per dati di archivio, selezionare la casella di controllo **Usare questo volume per i dati di archivio a cui si accede non di frequente**. 
      
       Un volume aggiunto in locale stati sottoposti a thick provisioning e garantisce che i dati primario hello sul volume hello rimangono dispositivo toohello locale e non spill toohello cloud.  Se si crea un volume aggiunto in locale, lo spazio disponibile nei livelli locale hello dei controlli dispositivo di hello volume hello tooprovision di hello dimensione richiesta. operazione Hello di creazione di un volume aggiunto in locale potrebbe comportare la distribuzione di dati esistenti dal cloud di toohello dispositivo hello e hello impiegato volume hello toocreate potrebbe richiedere tempo. tempo totale di Hello dipende dalle dimensioni hello del volume hello il provisioning, della larghezza di banda di rete disponibile e dati hello nel dispositivo. 
      
       Per un volume a livelli viene effettuato il thin provisioning e la creazione può essere rapida. Selezione **usare questo volume per i dati dell'archivio si accede di frequente** per il volume a livelli per i dati di archiviazione modifiche hello deduplicazione dimensioni del blocco per il volume di destinazione too512 KB. Se questo campo non è selezionato, volume a livelli corrispondente hello utilizza una dimensione del blocco di 64 KB. Dimensioni del blocco più grande deduplicazione consentono trasferimento di hello dispositivi tooexpedite hello del cloud toohello dati dell'archivio di grandi dimensioni.
   3. Specificare hello **capacità fornita** per il volume. Prendere nota della capacità di hello che è disponibile in base al tipo di volume hello selezionato. Hello specificato di dimensioni del volume non devono superare lo spazio disponibile hello.
      
       È possibile eseguire il provisioning di volumi aggiunti in locale fino too8.5 TB o i volumi a livelli di too200 TB sul dispositivo 8100 hello. Nel dispositivo 8600 hello più grande, è possibile eseguire il provisioning di volumi aggiunti in locale fino too22.5 TB o i volumi a livelli di too500 TB. Lo spazio locale nel dispositivo hello è hello toohost richiesto l'utilizzo di set di volumi a livelli, la creazione di volumi aggiunti in locale influisce sulle spazio hello disponibile per il provisioning dei volumi a livelli. Pertanto, creando un volume aggiunto in locale verrà ridotto lo spazio disponibile per la creazione di volumi a livelli. Analogamente, se viene creato un volume a livelli, lo spazio disponibile di hello per la creazione di volumi aggiunti in locale viene ridotto.
      
       Se si esegue il provisioning di un volume aggiunto in locale di 8,5 TB (dimensione massima consentita) sul dispositivo 8100, aver esaurito tutti hello lo spazio locale disponibile nel dispositivo hello. Non sarà in grado di toocreate qualsiasi volume a livelli da che punto in poi pari al numero di sia alcun spazio locale nel working set di hello dispositivo toohost hello di hello a livelli a volume. I volumi a livelli esistenti influiscono spazio hello disponibile. Ad esempio, se nel dispositivo 8100 sono già presenti volumi a livelli di circa 106 TB, saranno disponibili solo 4 TB di spazio per i volumi aggiunti in locale.
      
       Hello immagine seguente viene illustrato hello **le impostazioni di base** la finestra di dialogo per un volume aggiunto in locale.
      
        ![Aggiungere un volume locale](./media/storsimple-create-volume-u2/add-local-volume-include.png)
      
       Hello immagine seguente viene illustrato hello **le impostazioni di base** la finestra di dialogo per un volume a livelli.
      
        ![Aggiungere un volume locale](./media/storsimple-create-volume-u2/add-tiered-volume-include.png)
   
   1. Fare clic sull'icona di freccia hello ![icona a forma di freccia](./media/storsimple-create-volume-u2/HCS_ArrowIcon-include.png) toogo toohello la pagina successiva.
3. In hello **impostazioni aggiuntive** nella finestra di dialogo, aggiungere un nuovo record di controllo di accesso (ACR):
   
   1. Fornire un **Nome** per l'ACR.
   2. In **nome iniziatore iSCSI**, fornire hello iSCSI nome qualificato dell'host Windows. Se non si dispone di hello IQN, andare troppo[Get hello nome qualificato iSCSI di un host Windows Server](#get-the-iqn-of-a-windows-server-host).
   3. In **backup predefinito per questo volume?**selezionare hello **abilitare** casella di controllo. Hello predefinita viene creato un criterio che viene eseguita alle 22.30 ogni giorno (ora del dispositivo) e crea uno snapshot cloud del volume.
      
      > [!NOTE]
      > Backup di hello è abilitato in questo caso, non può essere ripristinato. È necessario tooedit hello volume toomodify questa impostazione.
      > 
      > 
      
      ![Aggiungi volume](./media/storsimple-create-volume-u2/AddVolumeAdditionalSettings1.png)
4. Fare clic sull'icona di controllo hello ![icona del segno di spunta](./media/storsimple-create-volume-u2/HCS_CheckIcon-include.png). Viene creato un volume con hello specificato le impostazioni.

