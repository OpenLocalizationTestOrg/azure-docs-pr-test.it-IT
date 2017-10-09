#### <a name="toocreate-a-new-service"></a>toocreate un nuovo servizio

1.  Utilizzando le credenziali dell'account Microsoft, accedere toohello portale di Azure a questo URL: <https://portal.azure.com/>. Se la distribuzione dispositivo hello nel portale amministrativo, accedere all'indirizzo: <https://portal.azure.us/>

2.  Nel portale di Azure hello, fare clic su **+ nuovo** &gt; **archiviazione** &gt; **serie virtuale StorSimple**.

    ![Creare un nuovo servizio](./media/storsimple-virtual-array-create-new-service/createnewservice2.png) 

3.  In hello **dispositivo StorSimple Manager** pannello in cui è visualizzata, hello seguenti:

    1.  Specificare un **Nome della risorsa** univoco per il servizio. nome della risorsa Hello è un nome descrittivo che può essere utilizzato il servizio di hello tooidentify. nome di Hello può essere compresa tra 2 e 50 caratteri che possono essere lettere, numeri e trattini. nome Hello deve iniziare e terminare con una lettera o un numero.

    2.  Scegliere un **sottoscrizione** dall'elenco a discesa hello. sottoscrizione di Hello è collegato tooyour account di fatturazione. Questo campo non è presente se si dispone di una sola sottoscrizione.

    3.  Per **Gruppo di risorse** selezionare un gruppo esistente o creare un nuovo gruppo. Per altre informazioni, vedere [Azure resource groups](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/) (Gruppi di risorse di Azure).

    4.  Fornire una **Località** per il servizio. Per altre informazioni sui servizi disponibili in aree specifiche, vedere [Aree di Azure](https://azure.microsoft.com/regions/#services) . In generale, scegliere un **percorso** area geografica più vicina toohello in cui si desidera toodeploy il dispositivo. È inoltre possibile toofactor seguenti hello:

        -   Se si dispone di carichi di lavoro esistente in cui si prevede inoltre toodeploy con il dispositivo StorSimple di Azure, è consigliabile usare Data Center in questione.

        -   Gestione dispositivi StorSimple e Archiviazione di Azure possono trovarsi in due posizioni distinte. In tal caso, sono necessari toocreate hello dispositivo StorSimple Manager e account di archiviazione Azure separatamente. toocreate un account di archiviazione di Azure, andare toohello servizio di archiviazione di Azure nel portale di Azure hello e seguire i passaggi di hello in [creare un account di archiviazione di Azure](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/#create-a-storage-account). Dopo aver creato questo account, aggiungerlo di servizio di gestione di dispositivi StorSimple toohello seguendo procedure hello [configurare un nuovo account di archiviazione per il servizio hello](https://azure.microsoft.com/en-us/documentation/articles/storsimple-deployment-walkthrough/#configure-a-new-storage-account-for-the-service).

        -   Se la distribuzione di periferica virtuale hello hello portale amministrativo, hello del servizio di gestione di dispositivi StorSimple è disponibile nelle posizioni ci Iowa e noi Virginia.

    5.  Selezionare **creare un nuovo account di archiviazione di Azure** tooautomatically creare un account di archiviazione con il servizio di hello. Specificare un **Nome dell'account di archiviazione**. Se è necessario che i dati siano in un percorso diverso, deselezionare questa casella.

    6.  Controllare **toodashboard Pin** se si desidera un servizio di collegamento rapido toothis nel dashboard.

    7.  Fare clic su **crea** toocreate hello dispositivo StorSimple Manager.

        ![Creare un nuovo servizio](./media/storsimple-virtual-array-create-new-service/createnewservice4.png)  

Si è diretto toohello **servizio** pagina di destinazione. creazione del servizio Hello richiede alcuni minuti. Dopo che il servizio di hello è stato creato, riceverà una notifica in modo appropriato e stato hello del servizio hello cambia troppo**Active**.


