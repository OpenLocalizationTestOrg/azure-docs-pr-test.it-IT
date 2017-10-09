<!--author=SharS last changed: 9/17/15-->

<span data-ttu-id="b90aa-101">In questa procedura, si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="b90aa-101">In this procedure, you will:</span></span>

1. <span data-ttu-id="b90aa-102">[Preparare l'eseguibile del gestore di hello toorun](#to-prepare-to-run-the-maintainer) .</span><span class="sxs-lookup"><span data-stu-id="b90aa-102">[Prepare toorun hello Maintainer executable](#to-prepare-to-run-the-maintainer) .</span></span>
2. <span data-ttu-id="b90aa-103">[Preparare i database del contenuto hello e il Cestino per l'eliminazione immediata dei blob orfani](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span><span class="sxs-lookup"><span data-stu-id="b90aa-103">[Prepare hello content database and Recycle Bin for immediate deletion of orphaned BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span></span>
3. <span data-ttu-id="b90aa-104">[Eseguire Maintainer.exe](#to-run-the-maintainer).</span><span class="sxs-lookup"><span data-stu-id="b90aa-104">[Run Maintainer.exe](#to-run-the-maintainer).</span></span>
4. <span data-ttu-id="b90aa-105">[Ripristinare i database del contenuto hello e impostazioni del Cestino](#to-revert-the-content-database-and-recycle-bin-settings).</span><span class="sxs-lookup"><span data-stu-id="b90aa-105">[Revert hello content database and Recycle Bin settings](#to-revert-the-content-database-and-recycle-bin-settings).</span></span>

#### <a name="tooprepare-toorun-hello-maintainer"></a><span data-ttu-id="b90aa-106">tooprepare toorun hello del gestore</span><span class="sxs-lookup"><span data-stu-id="b90aa-106">tooprepare toorun hello Maintainer</span></span>
1. <span data-ttu-id="b90aa-107">Nel server front-end Web hello, aprire hello SharePoint 2013 Management Shell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b90aa-107">On hello Web front-end server, open hello SharePoint 2013 Management Shell as an administrator.</span></span>
2. <span data-ttu-id="b90aa-108">Esplorazione delle cartelle toohello *unità di avvio*: \Programmi\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span><span class="sxs-lookup"><span data-stu-id="b90aa-108">Navigate toohello folder *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span></span>
3. <span data-ttu-id="b90aa-109">Rinominare **Microsoft.Data.sqlremoteblobs.maintainer.exe. config** troppo**Web. config**.</span><span class="sxs-lookup"><span data-stu-id="b90aa-109">Rename **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** too**web.config**.</span></span>
4. <span data-ttu-id="b90aa-110">Utilizzare `aspnet_regiis -pdf connectionStrings` file Web. config di hello toodecrypt.</span><span class="sxs-lookup"><span data-stu-id="b90aa-110">Use `aspnet_regiis -pdf connectionStrings` toodecrypt hello web.config file.</span></span>
5. <span data-ttu-id="b90aa-111">Nel file Web. config decrittografata hello in hello `connectionStrings` nodo, aggiungere la stringa di connessione hello per l'istanza SQL server e hello Nome database del contenuto.</span><span class="sxs-lookup"><span data-stu-id="b90aa-111">In hello decrypted web.config file, under hello `connectionStrings` node, add hello connection string for your SQL server instance and hello content database name.</span></span> <span data-ttu-id="b90aa-112">Vedere hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="b90aa-112">See hello following example.</span></span>
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. <span data-ttu-id="b90aa-113">Utilizzare `aspnet_regiis –pef connectionStrings` toore-crittografare file Web. config hello.</span><span class="sxs-lookup"><span data-stu-id="b90aa-113">Use `aspnet_regiis –pef connectionStrings` toore-encrypt hello web.config file.</span></span> 
7. <span data-ttu-id="b90aa-114">Rinominare tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config Web. config.</span><span class="sxs-lookup"><span data-stu-id="b90aa-114">Rename web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span></span> 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a><span data-ttu-id="b90aa-115">database del contenuto hello tooprepare e tooimmediately Cestino eliminare BLOB orfani</span><span class="sxs-lookup"><span data-stu-id="b90aa-115">tooprepare hello content database and Recycle Bin tooimmediately delete orphaned BLOBs</span></span>
1. <span data-ttu-id="b90aa-116">In SQL Server, in SQL Management Studio, hello eseguire hello seguenti query di aggiornamento per il database del contenuto di destinazione hello:</span><span class="sxs-lookup"><span data-stu-id="b90aa-116">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span> 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. <span data-ttu-id="b90aa-117">In hello web in server front-end, **Amministrazione centrale**, modificare hello **impostazioni generali applicazione Web** per hello desiderato hello disable di database del contenuto tootemporarily Cestino.</span><span class="sxs-lookup"><span data-stu-id="b90aa-117">On hello web front-end server, under **Central Administration**, edit hello **Web Application General Settings** for hello desired content database tootemporarily disable hello Recycle Bin.</span></span> <span data-ttu-id="b90aa-118">Questa azione verrà inoltre hello vuota al Cestino per tutte le raccolte siti correlati.</span><span class="sxs-lookup"><span data-stu-id="b90aa-118">This action will also empty hello Recycle Bin for any related site collections.</span></span> <span data-ttu-id="b90aa-119">toodo, fare clic su **Amministrazione centrale** -> **Application Management** -> **applicazioni Web (Gestisci applicazioni web)**  ->  **SharePoint - 80** -> **impostazioni generali applicazione**.</span><span class="sxs-lookup"><span data-stu-id="b90aa-119">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="b90aa-120">Set hello **stato Cestino** troppo**OFF**.</span><span class="sxs-lookup"><span data-stu-id="b90aa-120">Set hello **Recycle Bin Status** too**OFF**.</span></span>
   
    ![Impostazioni generali applicazione Web](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a><span data-ttu-id="b90aa-122">toorun hello del gestore</span><span class="sxs-lookup"><span data-stu-id="b90aa-122">toorun hello Maintainer</span></span>
* <span data-ttu-id="b90aa-123">Nel server front-end web hello, in SharePoint 2013 Management Shell, hello eseguire hello del gestore come segue:</span><span class="sxs-lookup"><span data-stu-id="b90aa-123">On hello web front-end server, in hello SharePoint 2013 Management Shell, run hello Maintainer as follows:</span></span>
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > <span data-ttu-id="b90aa-124">Solo hello `GarbageCollection` operazione è supportata per StorSimple in questo momento.</span><span class="sxs-lookup"><span data-stu-id="b90aa-124">Only hello `GarbageCollection` operation is supported for StorSimple at this time.</span></span> <span data-ttu-id="b90aa-125">Si noti inoltre che i parametri di hello emessi per Microsoft.Data.SqlRemoteBlobs.Maintainer.exe sono tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="b90aa-125">Also note that hello parameters issued for Microsoft.Data.SqlRemoteBlobs.Maintainer.exe are case sensitive.</span></span> 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a><span data-ttu-id="b90aa-126">database del contenuto toorevert hello e impostazioni del Cestino</span><span class="sxs-lookup"><span data-stu-id="b90aa-126">toorevert hello content database and Recycle Bin settings</span></span>
1. <span data-ttu-id="b90aa-127">In SQL Server, in SQL Management Studio, hello eseguire hello seguenti query di aggiornamento per il database del contenuto di destinazione hello:</span><span class="sxs-lookup"><span data-stu-id="b90aa-127">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span>
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. <span data-ttu-id="b90aa-128">Nel server front-end web hello, in **Amministrazione centrale**, modificare hello **impostazioni generali applicazione Web** per hello desiderato hello toore enable database del contenuto del Cestino.</span><span class="sxs-lookup"><span data-stu-id="b90aa-128">On hello web front-end server, in **Central Administration**, edit hello **Web Application General Settings** for hello desired content database toore-enable hello Recycle Bin.</span></span> <span data-ttu-id="b90aa-129">toodo, fare clic su **Amministrazione centrale** -> **Application Management** -> **applicazioni Web (Gestisci applicazioni web)**  ->  **SharePoint - 80** -> **impostazioni generali applicazione**.</span><span class="sxs-lookup"><span data-stu-id="b90aa-129">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="b90aa-130">Impostare hello stato Cestino troppo**ON**.</span><span class="sxs-lookup"><span data-stu-id="b90aa-130">Set hello Recycle Bin Status too**ON**.</span></span>

