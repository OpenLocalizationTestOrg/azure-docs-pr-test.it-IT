<!--author=alkohli last changed: 07/19/2017-->

#### <a name="toocreate-a-volume"></a>toocreate un volume
1. Dall'elenco in formato tabulare hello dispositivi hello in hello **dispositivi** pannello, selezionare il dispositivo. Fare clic su **+ Aggiungi volume**.

    ![Aggiungere un nuovo volume](./media/storsimple-8000-create-volume-u2/step5createvol1.png)

2. In hello **aggiungere un volume** pannello:
   
   1. Hello **seleziona dispositivo** campo viene popolato automaticamente con il dispositivo corrente.

   2. Dall'elenco a discesa hello, selezionare il contenitore di volumi hello in cui è necessario tooadd un volume. 

   3.  Digitare un **Nome** per il volume. Una volta creato il volume di hello non è possibile rinominare un volume.

   4. Nell'elenco a discesa hello selezionare hello **tipo** per il volume. Per carichi di lavoro che richiedono garanzie locali, latenze basse e prestazioni più elevate, selezionare un volume **aggiunto in locale** . Per tutti gli altri dati, selezionare un volume **a livelli** . Se si usa questo volume per dati di archivio, selezionare la casella di controllo **Usare questo volume per i dati di archivio a cui si accede non di frequente**.
      
       Per un volume a livelli viene effettuato il thin provisioning e la creazione può essere rapida. Selezione **usare questo volume per i dati dell'archivio si accede di frequente** per il volume a livelli per i dati di archiviazione modifiche hello deduplicazione dimensioni del blocco per il volume di destinazione too512 KB. Se questo campo non è selezionato, volume a livelli corrispondente hello utilizza una dimensione del blocco di 64 KB. Dimensioni del blocco più grande deduplicazione consentono trasferimento di hello dispositivi tooexpedite hello del cloud toohello dati dell'archivio di grandi dimensioni.
       
       Un volume aggiunto in locale stati sottoposti a thick provisioning e garantisce che i dati primario hello sul volume hello rimangono dispositivo toohello locale e non spill toohello cloud.  Se si crea un volume aggiunto in locale, lo spazio disponibile nei livelli locale hello dei controlli dispositivo di hello volume hello tooprovision di hello dimensione richiesta. operazione Hello di creazione di un volume aggiunto in locale potrebbe comportare la distribuzione di dati esistenti dal cloud di toohello dispositivo hello e hello impiegato volume hello toocreate potrebbe richiedere tempo. tempo totale di Hello dipende dalle dimensioni hello del volume hello il provisioning, della larghezza di banda di rete disponibile e dati hello nel dispositivo.

   5. Specificare hello **capacità fornita** per il volume. Prendere nota della capacità di hello che è disponibile in base al tipo di volume hello selezionato. Hello specificato di dimensioni del volume non devono superare lo spazio disponibile hello.
      
       È possibile eseguire il provisioning di volumi aggiunti in locale fino too8.5 TB o i volumi a livelli di too200 TB sul dispositivo 8100 hello. Nel dispositivo 8600 hello più grande, è possibile eseguire il provisioning di volumi aggiunti in locale fino too22.5 TB o i volumi a livelli di too500 TB. Lo spazio locale nel dispositivo hello è hello toohost richiesto l'utilizzo di set di volumi a livelli, la creazione di volumi aggiunti in locale influisce sulle spazio hello disponibile per il provisioning dei volumi a livelli. Creando un volume aggiunto in locale, viene quindi ridotto lo spazio disponibile per la creazione di volumi a livelli. Analogamente, se viene creato un volume a livelli, lo spazio disponibile di hello per la creazione di volumi aggiunti in locale viene ridotto.
      
       Se si esegue il provisioning di un volume aggiunto in locale di 8,5 TB (dimensione massima consentita) sul dispositivo 8100, aver esaurito tutti hello lo spazio locale disponibile nel dispositivo hello. Non è possibile creare qualsiasi volume a livelli da tale punto in poi, non è disponibile spazio locale nel working set di hello dispositivo toohost hello di hello a livelli a volume. I volumi a livelli esistenti influiscono spazio hello disponibile. Ad esempio, se nel dispositivo 8100 sono già presenti volumi a livelli di circa 106 TB, saranno disponibili solo 4 TB di spazio per i volumi aggiunti in locale.

    6. In hello **connesso host** campo, fare clic sulla freccia di hello. 

        ![Host connessi](./media/storsimple-8000-create-volume-u2/step5createvol2.png)

    7. In hello **connesso host** pannello, scegliere un record esistente o aggiungere un nuovo ACR eseguendo hello alla procedura seguente:

       1. Fornire un **Nome** per l'ACR.
       2. In **nome iniziatore iSCSI**, fornire hello iSCSI nome qualificato dell'host Windows. Se non si dispone di hello IQN, andare troppo[Get hello nome qualificato iSCSI di un host Windows Server](#get-the-iqn-of-a-windows-server-host).

    9. Fare clic su **Crea**. Viene creato un volume con hello specificato le impostazioni.

        ![Fare clic su Crea](./media/storsimple-8000-create-volume-u2/step5createvol3.png)

        > [!NOTE]
        > Tenere presente che il volume di hello che è stato creato in questo caso non è protetto. Sarà necessario toocreate e associare i criteri di backup con i backup pianificati tootake questo volume. 

