1. Accedere all'indirizzo hello [portale Azure].
2. Fare clic su **+NUOVO** > **Web e dispositivi mobili** > **App per dispositivi mobili** e quindi specificare un nome per il back-end dell'app per dispositivi mobili.
3. Per hello **gruppo di risorse**, selezionare un gruppo di risorse esistente o crearne uno nuovo (utilizzando hello stesso nome dell'app). 
   
    È possibile selezionare un altro piano del servizio app o crearne uno nuovo. Per ulteriori informazioni sui piani di servizi App e come toocreate un nuovo piano di un prezzo diversi livelli e nella propria posizione desiderata, vedere [piani di servizio App di Azure ad approfondimenti su](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
4. Per hello **piano di servizio App**, il piano predefinito hello (in hello [livello Standard](https://azure.microsoft.com/pricing/details/app-service/)) sia selezionata. È anche possibile selezionare un piano diverso oppure [crearne uno nuovo](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan). le impostazioni del piano di servizio App Hello determinano hello [posizione, funzionalità, costo e le risorse di calcolo](https://azure.microsoft.com/pricing/details/app-service/) associati all'app. 
   
    Dopo avere stabilito il piano di hello, fare clic su **crea**. Crea back-end di hello App per dispositivi mobili. 
5. In hello **impostazioni** pannello hello nuovo back-end App Mobile, fare clic su **introduttiva** > la piattaforma di app client > **la connessione a un database**. 
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-data-connection.png)
6. In hello **aggiungere una connessione dati** pannello, fare clic su **Database SQL** > **creare un nuovo database**, database di tipo hello **nome**, Scegliere un piano tariffario, quindi fare clic su **Server**.  È possibile riutilizzare questo nuovo database. Se si dispone già di un database in hello stesso percorso, è invece possibile scegliere **utilizza un database esistente**. a causa dei costi toobandwidth e latenza più elevata non è consigliabile usare Hello un database in un percorso diverso.
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-db.png)
7. In hello **nuovo server** pannello, digitare un nome univoco in hello **nome Server** campo, specificare un account di accesso e una password, controllare **server tooaccess di servizi di azure Consenti**, fare clic su **OK**. Questo crea hello nuovo database.
8. In hello **aggiungere una connessione dati** pannello, fare clic su **stringa di connessione**, digitare i valori hello di account di accesso e la password per il database e fare clic su **OK**. Attendere alcuni minuti per hello database toobe distribuito correttamente prima di procedere.

<!-- URLs. -->
[portale Azure]: https://portal.azure.com/
