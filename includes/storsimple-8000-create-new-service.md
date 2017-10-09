<!--author=alkohli last changed:02/10/2017-->


#### <a name="toocreate-a-new-service"></a>toocreate un nuovo servizio

1. Utilizzare il toolog le credenziali di account Microsoft su toohello [portale di Azure](https://portal.azure.com/).

2. Nel portale di Azure hello, fare clic su  **+**  e quindi in marketplace hello, fare clic su **tutti**.

    ![Creare Gestione dispositivi StorSimple](./media/storsimple-8000-create-new-service/createssdevman1.png)

    Cercare _StorSimple Physical_ (Dispositivi fisici StorSimple). Selezionare e fare clic su **Serie di dispositivi fisici StorSimple** e quindi fare clic su **Crea**. In alternativa, fare clic nel portale di Azure hello  **+**  e quindi in **archiviazione**, fare clic su **serie dispositivo fisico StorSimple**.

    ![Creare Gestione dispositivi StorSimple](./media/storsimple-8000-create-new-service/createssdevman11.png)

3. In hello **dispositivo StorSimple Manager** pannello hello i passaggi seguenti:
   
   1. Specificare un **Nome della risorsa** univoco per il servizio. Questo nome è un nome descrittivo che può essere utilizzato il servizio di hello tooidentify. nome di Hello può essere compresa tra 2 e 50 caratteri che possono essere lettere, numeri e trattini. nome Hello deve iniziare e terminare con una lettera o un numero.

   2. Scegliere un **sottoscrizione** dall'elenco a discesa hello. sottoscrizione di Hello è collegato tooyour account di fatturazione. Questo campo non è presente se si dispone di una sola sottoscrizione.

   3. Per **Gruppo di risorse**, selezionare **Usa esistente** o **Crea nuovo**. Per altre informazioni, vedere [Azure resource groups](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/) (Gruppi di risorse di Azure).
   
   4. Fornire una **Località** per il servizio. In generale, scegliere una posizione più vicina toohello area geografica in cui si desidera toodeploy il dispositivo. È inoltre possibile toofactor in hello seguenti considerazioni: 
      
      * Se si dispone di carichi di lavoro esistente in cui si prevede inoltre toodeploy con il dispositivo StorSimple di Azure, è necessario utilizzare il Data Center.
      * Il servizio Gestione dispositivi StorSimple e la risorsa di archiviazione di Azure possono trovarsi in due posizioni distinte. In tal caso, sono necessari toocreate hello dispositivo StorSimple Manager e account di archiviazione Azure separatamente. toocreate un account di archiviazione di Azure, andare toohello servizio di archiviazione di Azure nel portale di Azure hello e seguire i passaggi di hello in [creare un account di archiviazione di Azure](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account). Dopo aver creato questo account, aggiungerlo di servizio di gestione di dispositivi StorSimple toohello seguendo procedure hello [configurare un nuovo account di archiviazione per il servizio hello](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#configure-a-new-storage-account-for-the-service).

   5. Selezionare **creare un nuovo account di archiviazione** tooautomatically creare un account di archiviazione con il servizio di hello. Specificare un nome per questo account di archiviazione. Se è necessario che i dati siano in un percorso diverso, deselezionare questa casella.

   6. Controllare **toodashboard Pin** se si desidera un servizio di collegamento rapido toothis nel dashboard.
      
   7. Fare clic su **crea** toocreate hello dispositivo StorSimple Manager.

       ![Creare Gestione dispositivi StorSimple](./media/storsimple-8000-create-new-service/createssdevman2.png)
   
creazione del servizio Hello richiede alcuni minuti. Dopo che il servizio hello viene creato correttamente, verrà visualizzata una notifica e viene aperta pannello servizio nuova hello.
   
![Creare Gestione dispositivi StorSimple](./media/storsimple-8000-create-new-service/createssdevman5.png)


