<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> <span data-ttu-id="f5737-101">Quando si apportano modifiche toohello adattatore StorSimple per la configurazione di SharePoint RBS, è necessario essere connessi con un account utente appartenente al gruppo Domain Admins toohello.</span><span class="sxs-lookup"><span data-stu-id="f5737-101">When making changes toohello StorSimple Adapter for SharePoint RBS configuration, you must be logged on with a user account that belongs toohello Domain Admins group.</span></span> <span data-ttu-id="f5737-102">Inoltre, è necessario accedere pagina Configurazione hello da un browser in esecuzione su hello stesso host di amministrazione centrale.</span><span class="sxs-lookup"><span data-stu-id="f5737-102">Additionally, you must access hello configuration page from a browser running on hello same host as Central Administration.</span></span>
> 
> 

#### <a name="tooconfigure-rbs"></a><span data-ttu-id="f5737-103">tooconfigure RBS</span><span class="sxs-lookup"><span data-stu-id="f5737-103">tooconfigure RBS</span></span>
1. <span data-ttu-id="f5737-104">Aprire la pagina di amministrazione centrale SharePoint hello e passare troppo**le impostazioni di sistema**.</span><span class="sxs-lookup"><span data-stu-id="f5737-104">Open hello SharePoint Central Administration page, and browse too**System Settings**.</span></span> 
2. <span data-ttu-id="f5737-105">In hello **Azure StorSimple** fare clic su **configura l'adattatore StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="f5737-105">In hello **Azure StorSimple** section, click **Configure StorSimple Adapter**.</span></span>
   
    ![Configurare hello adattatore StorSimple](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. <span data-ttu-id="f5737-107">In hello **configura l'adattatore StorSimple** pagina:</span><span class="sxs-lookup"><span data-stu-id="f5737-107">On hello **Configure StorSimple Adapter** page:</span></span>
   
   1. <span data-ttu-id="f5737-108">Verificare che tale hello **Abilita Modifica percorso** casella di controllo è selezionata.</span><span class="sxs-lookup"><span data-stu-id="f5737-108">Make sure that hello **Enable editing path** check box is selected.</span></span>
   2. <span data-ttu-id="f5737-109">Nella casella di testo hello, digitare il percorso UNC Universal Naming Convention () hello dell'archivio BLOB hello.</span><span class="sxs-lookup"><span data-stu-id="f5737-109">In hello text box, type hello Universal Naming Convention (UNC) path of hello BLOB store.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="f5737-110">volume dell'archivio BLOB Hello deve essere ospitato in un volume iSCSI configurato sul dispositivo StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="f5737-110">hello BLOB store volume must be hosted on an iSCSI volume configured on hello StorSimple device.</span></span>

   3. <span data-ttu-id="f5737-111">Fare clic su hello **abilitare** pulsante sotto ogni hello database del contenuto che si desidera tooconfigure per l'archiviazione remota.</span><span class="sxs-lookup"><span data-stu-id="f5737-111">Click hello **Enable** button below each of hello content databases that you want tooconfigure for remote storage.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="f5737-112">archivio BLOB Hello deve essere condiviso e raggiungibile da tutti i server (WFE) front-end web e account utente hello è configurato per la server farm di SharePoint hello deve avere condivisione toohello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f5737-112">hello BLOB store must be shared and reachable by all web front-end (WFE) servers, and hello user account that is configured for hello SharePoint server farm must have access toohello share.</span></span>
      
      ![Abilitare i provider RBS hello](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      <span data-ttu-id="f5737-114">Quando si abilita o disabilita RBS, si verifica anche segue messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="f5737-114">When you enable or disable RBS, you will also see hello following message.</span></span>
      
      ![Configurare l’adattatore StorSimple Adapter Attivazione Disattivazione](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. <span data-ttu-id="f5737-116">Fare clic su hello **aggiornamento** configurazione hello tooapply dei pulsanti.</span><span class="sxs-lookup"><span data-stu-id="f5737-116">Click hello **Update** button tooapply hello configuration.</span></span> <span data-ttu-id="f5737-117">Quando si fa clic su hello **aggiornamento** pulsante, verrà aggiornato lo stato di configurazione di RBS hello in tutti i server front-end Web e intera farm hello sarà abilitata per RBS.</span><span class="sxs-lookup"><span data-stu-id="f5737-117">When you click hello **Update** button, hello RBS configuration status will be updated on all WFE servers, and hello entire farm will be RBS-enabled.</span></span> <span data-ttu-id="f5737-118">verrà visualizzata la seguente messaggio Hello.</span><span class="sxs-lookup"><span data-stu-id="f5737-118">hello following message appears.</span></span>
      
      ![Messaggio di configurazione dell’adattatore](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > <span data-ttu-id="f5737-120">Se si configura RBS per una farm di SharePoint con un numero molto elevato di database (maggiori di 200), pagina web di amministrazione centrale SharePoint hello potrebbe scadere. In questo caso, aggiornare la pagina hello.</span><span class="sxs-lookup"><span data-stu-id="f5737-120">If you are configuring RBS for a SharePoint farm with a very large number of databases (greater than 200), hello SharePoint Central Administration web page might time out. If that occurs, refresh hello page.</span></span> <span data-ttu-id="f5737-121">Questa operazione non influenza il processo di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="f5737-121">This does not affect hello configuration process.</span></span>

4. <span data-ttu-id="f5737-122">Verificare la configurazione di hello:</span><span class="sxs-lookup"><span data-stu-id="f5737-122">Verify hello configuration:</span></span>
   
   1. <span data-ttu-id="f5737-123">Accedere al sito Web Amministrazione centrale SharePoint toohello e passare toohello **configura l'adattatore StorSimple** pagina.</span><span class="sxs-lookup"><span data-stu-id="f5737-123">Log on toohello SharePoint Central Administration website, and browse toohello **Configure StorSimple Adapter** page.</span></span>
   2. <span data-ttu-id="f5737-124">Controllare hello toomake dettagli di configurazione corrispondenza impostazioni hello immesso.</span><span class="sxs-lookup"><span data-stu-id="f5737-124">Check hello configuration details toomake sure that they match hello settings that you entered.</span></span> 
5. <span data-ttu-id="f5737-125">Verificare che RBS funzioni correttamente:</span><span class="sxs-lookup"><span data-stu-id="f5737-125">Verify that RBS works correctly:</span></span>
   
   1. <span data-ttu-id="f5737-126">Caricare un documento tooSharePoint.</span><span class="sxs-lookup"><span data-stu-id="f5737-126">Upload a document tooSharePoint.</span></span> 
   2. <span data-ttu-id="f5737-127">Percorso UNC toohello Sfoglia configurata.</span><span class="sxs-lookup"><span data-stu-id="f5737-127">Browse toohello UNC path that you configured.</span></span> <span data-ttu-id="f5737-128">Assicurarsi che sia stato creato struttura di directory RBS hello e che contenga oggetti hello caricato.</span><span class="sxs-lookup"><span data-stu-id="f5737-128">Make sure that hello RBS directory structure was created and that it contains hello uploaded object.</span></span>
6. <span data-ttu-id="f5737-129">(Facoltativo) È possibile utilizzare Microsoft RBS hello `Migrate()` cmdlet di PowerShell incluso con SharePoint toomigrate esistente BLOB toohello contenuto dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f5737-129">(Optional) You can use hello Microsoft RBS `Migrate()` PowerShell cmdlet included with SharePoint toomigrate existing BLOB content toohello StorSimple device.</span></span> <span data-ttu-id="f5737-130">Per ulteriori informazioni, vedere [la migrazione del contenuto da o verso RBS in SharePoint 2013] [ 6] o [la migrazione del contenuto e verso RBS (SharePoint Foundation 2010)] [7].</span><span class="sxs-lookup"><span data-stu-id="f5737-130">For more information, see [Migrate content into or out of RBS in SharePoint 2013][6] or [Migrate content into or out of RBS (SharePoint Foundation 2010)][7].</span></span>
7. <span data-ttu-id="f5737-131">(Facoltativo) Nelle installazioni di prova, è possibile verificare che hello BLOB sono stati spostati dal database del contenuto hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f5737-131">(Optional) On test installations, you can verify that hello BLOBs were moved out of hello content database as follows:</span></span> 
   
   1. <span data-ttu-id="f5737-132">Avviare SQL Management Studio.</span><span class="sxs-lookup"><span data-stu-id="f5737-132">Start SQL Management Studio.</span></span>
   2. <span data-ttu-id="f5737-133">Eseguire query ListBlobsInDB_2010.sql o ListBlobsInDB_2013.sql di hello, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="f5737-133">Run hello ListBlobsInDB_2010.sql or ListBlobsInDB_2013.sql query, as follows.</span></span>
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      <span data-ttu-id="f5737-134">Se RBS è stato configurato correttamente, verrà visualizzato un valore NULL nella colonna SizeOfContentInDB hello per qualsiasi oggetto che è stato caricato e quindi esternalizzato con RBS.</span><span class="sxs-lookup"><span data-stu-id="f5737-134">If RBS was configured correctly, a NULL value should appear in hello SizeOfContentInDB column for any object that was uploaded and successfully externalized with RBS.</span></span>
8. <span data-ttu-id="f5737-135">(Facoltativo) Dopo aver configurato RBS e spostare tutti i BLOB toohello contenuto dispositivo StorSimple, è possibile spostare dispositivo toohello di hello database del contenuto.</span><span class="sxs-lookup"><span data-stu-id="f5737-135">(Optional) After you configure RBS and move all BLOB content toohello StorSimple device, you can move hello content database toohello device.</span></span> <span data-ttu-id="f5737-136">Se si sceglie di database del contenuto hello toomove, è consigliabile configurare hello archiviazione del database del contenuto nel dispositivo hello come volume principale.</span><span class="sxs-lookup"><span data-stu-id="f5737-136">If you choose toomove hello content database, we recommend that you configure hello content database storage on hello device as a primary volume.</span></span> <span data-ttu-id="f5737-137">Quindi, utilizzare stabilito di che SQL Server best practices il dispositivo StorSimple toohello di toomigrate hello database del contenuto.</span><span class="sxs-lookup"><span data-stu-id="f5737-137">Then, use established SQL Server best practices toomigrate hello content database toohello StorSimple device.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f5737-138">Mobile device toohello database del contenuto di hello è supportato solo per serie StorSimple 8000 hello (non è supportata per la serie hello 5000 o 7000).</span><span class="sxs-lookup"><span data-stu-id="f5737-138">Moving hello content database toohello device is only supported for hello StorSimple 8000 series (it is not supported for hello 5000 or 7000 series).</span></span>
   
   <span data-ttu-id="f5737-139">Se si archiviano i BLOB e database del contenuto hello in volumi separati nel dispositivo StorSimple hello, si consiglia di configurarli in hello stesso contenitore di volumi.</span><span class="sxs-lookup"><span data-stu-id="f5737-139">If you store BLOBs and hello content database in separate volumes on hello StorSimple device, we recommend that you configure them in hello same volume container.</span></span> <span data-ttu-id="f5737-140">Ciò garantisce che essi saranno sottoposti insieme al backup.</span><span class="sxs-lookup"><span data-stu-id="f5737-140">This ensures that they will be backed up together.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="f5737-141">Se RBS non è stato abilitato, è preferibile non spostare dispositivo StorSimple toohello di hello database del contenuto.</span><span class="sxs-lookup"><span data-stu-id="f5737-141">If you have not enabled RBS, we do not recommend moving hello content database toohello StorSimple device.</span></span> <span data-ttu-id="f5737-142">Si tratta di una configurazione non testata.</span><span class="sxs-lookup"><span data-stu-id="f5737-142">This is an untested configuration.</span></span>
   
9. <span data-ttu-id="f5737-143">Passaggio successivo toohello passare: [configurare garbage collection](#configure-garbage-collection).</span><span class="sxs-lookup"><span data-stu-id="f5737-143">Go toohello next step: [Configure garbage collection](#configure-garbage-collection).</span></span>

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
