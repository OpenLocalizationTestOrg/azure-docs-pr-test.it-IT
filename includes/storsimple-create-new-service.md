<!--author=alkohli last changed:01/14/2016-->


#### <a name="toocreate-a-new-service"></a>toocreate un nuovo servizio
1. Utilizzando le credenziali dell'account Microsoft, accedere toohello portale di Azure classico in corrispondenza dell'URL: [https://manage.windowsazure.com/](https://manage.windowsazure.com/).
2. Nel portale di Azure classico hello, fare clic su **New** > **Data Services** > **StorSimple Manager** > **rapido Creare**.
3. Nel modulo hello visualizzato hello seguenti:
   
   1. Fornire un **Nome** univoco per il servizio. Si tratta di un nome descrittivo che può essere utilizzato il servizio di hello tooidentify. nome di Hello può essere compresa tra 2 e 50 caratteri che possono essere lettere, numeri e trattini. nome Hello deve iniziare e terminare con una lettera o un numero.
   2. Fornire una **Località** per il servizio. In generale, scegliere una posizione più vicina toohello area geografica in cui si desidera toodeploy il dispositivo. È inoltre possibile toofactor seguenti hello: 
      
      * Se si dispone di carichi di lavoro esistente in cui si prevede inoltre toodeploy con il dispositivo StorSimple di Azure, è necessario utilizzare il Data Center.
      * Il servizio StorSimple Manager e la risorsa di archiviazione di Azure possono trovarsi in due posizioni distinte. In tal caso, sono necessari toocreate hello StorSimple Manager e account di archiviazione Azure separatamente. toocreate un account di archiviazione di Azure, andare toohello servizio di archiviazione di Azure nel portale di Azure classico hello e seguire i passaggi di hello in [creare un account di archiviazione di Azure](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account). Dopo aver creato questo account, aggiungere il servizio StorSimple Manager toohello seguendo i passaggi di hello in [configurare un nuovo account di archiviazione per il servizio hello](../articles/storsimple/storsimple-deployment-walkthrough.md#configure-a-new-storage-account-for-the-service).
   3. Scegliere un **sottoscrizione** dall'elenco a discesa hello. sottoscrizione di Hello è collegato tooyour account di fatturazione. Questo campo non è presente se si dispone di una sola sottoscrizione.
   4. Selezionare **creare un nuovo account di archiviazione** tooautomatically creare un account di archiviazione con il servizio di hello. Questo account di archiviazione avrà un nome speciale, ad esempio "storsimplebwv8c6dcnf". Se è necessario che i dati siano in un percorso diverso, deselezionare questa casella. 
   5. Fare clic su **Crea servizio StorSimple Manager** servizio hello toocreate.
   
   ![Crea StorSimple Manager](./media/storsimple-create-new-service/HCS_CreateAService-include.png)
   
   Sarà indirizzato toohello **servizio** pagina di destinazione. creazione del servizio Hello richiederà alcuni minuti. Dopo che il servizio di hello è stato creato, riceverà una notifica in modo appropriato e stato hello del servizio hello cambia troppo**Active**.
   
   ![Creazione del servizio](./media/storsimple-create-new-service/HCS_StorSimpleManagerServicePage-include.png)

![Video disponibile](./media/storsimple-create-new-service/Video_icon.png)**Video disponibile**

toowatch un video che illustra come toocreate un nuovo servizio StorSimple Manager, fare clic su [qui](https://azure.microsoft.com/documentation/videos/create-a-storsimple-manager-service/).

