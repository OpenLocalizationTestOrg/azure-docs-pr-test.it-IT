<!--author=alkohli last changed:01/14/2016-->


#### <a name="to-create-a-new-service"></a>Per creare un nuovo servizio
1. Usare le credenziali dell'account Microsoft e accedere al portale di Azure classico all'URL seguente: [https://manage.windowsazure.com/](https://manage.windowsazure.com/).
2. Nel portale di Azure classico fare clic su **Nuovo** > **Servizi dati** > **StorSimple Manager** > **Creazione rapida**.
3. Nel modulo visualizzato, procedere come segue:
   
   1. Fornire un **Nome** univoco per il servizio. Si tratta di un nome descrittivo che può essere utilizzato per identificare il servizio. Il nome può contenere da 2 a 50 caratteri che possono essere lettere, numeri e trattini. Il nome deve iniziare e terminare con una lettera o un numero.
   2. Fornire una **Località** per il servizio. In generale, scegliere un percorso più vicino all'area geografica in cui si desidera distribuire il dispositivo. È inoltre possibile tenere in considerazione quanto segue: 
      
      * Se si dispone di carichi di lavoro esistenti in Azure che si intende distribuire con il dispositivo StorSimple, usare tale data center.
      * Il servizio StorSimple Manager e la risorsa di archiviazione di Azure possono trovarsi in due posizioni distinte. In tal caso, è necessario creare il servizio StorSimple Manager e l'account di archiviazione di Azure separatamente. Per creare un account di archiviazione di Azure, passare al servizio Archiviazione di Azure nel portale di Azure classico e seguire la procedura descritta in [Creare un account di archiviazione](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account). Dopo aver creato questo account, aggiungerlo al servizio StorSimple Manager seguendo la procedura per [configurare un nuovo account di archiviazione per il servizio](../articles/storsimple/storsimple-deployment-walkthrough.md#configure-a-new-storage-account-for-the-service).
   3. Scegliere una **Sottoscrizione** dall'elenco a discesa. La sottoscrizione viene collegata all'account di fatturazione. Questo campo non è presente se si dispone di una sola sottoscrizione.
   4. Selezionare **Crea un nuovo account di archiviazione** per creare automaticamente un account di archiviazione con il servizio. Questo account di archiviazione avrà un nome speciale, ad esempio "storsimplebwv8c6dcnf". Se è necessario che i dati siano in un percorso diverso, deselezionare questa casella. 
   5. Fare clic su **Crea StorSimple Manager** per creare il servizio.
   
   ![Crea StorSimple Manager](./media/storsimple-create-new-service/HCS_CreateAService-include.png)
   
   Si verrà indirizzati alla pagina di destinazione del **Servizio** . La creazione del servizio richiederà alcuni minuti. Dopo che il servizio è stato creato, l'utente verrà informato in modo appropriato e lo stato del servizio verrà modificato in **Attivo**.
   
   ![Creazione del servizio](./media/storsimple-create-new-service/HCS_StorSimpleManagerServicePage-include.png)

![Video disponibile](./media/storsimple-create-new-service/Video_icon.png)**Video disponibile**

Per guardare un video che illustra come creare un nuovo servizio StorSimple Manager, fare clic [qui](https://azure.microsoft.com/documentation/videos/create-a-storsimple-manager-service/).

