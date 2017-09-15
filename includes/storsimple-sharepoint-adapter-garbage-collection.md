<!--author=SharS last changed: 9/17/15-->

<span data-ttu-id="98608-101">In questa procedura, si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="98608-101">In this procedure, you will:</span></span>

1. <span data-ttu-id="98608-102">[Prepararsi a eseguire il Maintainer eseguibile](#to-prepare-to-run-the-maintainer) .</span><span class="sxs-lookup"><span data-stu-id="98608-102">[Prepare to run the Maintainer executable](#to-prepare-to-run-the-maintainer) .</span></span>
2. <span data-ttu-id="98608-103">[Preparare il database del contenuto e il Cestino per l'eliminazione immediata dei BLOB orfani](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span><span class="sxs-lookup"><span data-stu-id="98608-103">[Prepare the content database and Recycle Bin for immediate deletion of orphaned BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span></span>
3. <span data-ttu-id="98608-104">[Eseguire Maintainer.exe](#to-run-the-maintainer).</span><span class="sxs-lookup"><span data-stu-id="98608-104">[Run Maintainer.exe](#to-run-the-maintainer).</span></span>
4. <span data-ttu-id="98608-105">[Ripristinare il database del contenuto e le impostazioni del Cestino](#to-revert-the-content-database-and-recycle-bin-settings).</span><span class="sxs-lookup"><span data-stu-id="98608-105">[Revert the content database and Recycle Bin settings](#to-revert-the-content-database-and-recycle-bin-settings).</span></span>

#### <a name="to-prepare-to-run-the-maintainer"></a><span data-ttu-id="98608-106">Per preparare l'esecuzione di Maintainer</span><span class="sxs-lookup"><span data-stu-id="98608-106">To prepare to run the Maintainer</span></span>
1. <span data-ttu-id="98608-107">Sul server front-end web, aprire la Shell di gestione di SharePoint 2013 come amministratore.</span><span class="sxs-lookup"><span data-stu-id="98608-107">On the Web front-end server, open the SharePoint 2013 Management Shell as an administrator.</span></span>
2. <span data-ttu-id="98608-108">Passare alla cartella *unità di avvio*:\Programmi\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span><span class="sxs-lookup"><span data-stu-id="98608-108">Navigate to the folder *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span></span>
3. <span data-ttu-id="98608-109">Rinominare **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** in **web.config**.</span><span class="sxs-lookup"><span data-stu-id="98608-109">Rename **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** to **web.config**.</span></span>
4. <span data-ttu-id="98608-110">Utilizzare `aspnet_regiis -pdf connectionStrings` per decrittografare il file web.config.</span><span class="sxs-lookup"><span data-stu-id="98608-110">Use `aspnet_regiis -pdf connectionStrings` to decrypt the web.config file.</span></span>
5. <span data-ttu-id="98608-111">Nel file web.config decrittografato sotto al nodo `connectionStrings` , aggiungere la stringa di connessione per l'istanza del server SQL e il nome del database del contenuto.</span><span class="sxs-lookup"><span data-stu-id="98608-111">In the decrypted web.config file, under the `connectionStrings` node, add the connection string for your SQL server instance and the content database name.</span></span> <span data-ttu-id="98608-112">Vedere l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="98608-112">See the following example.</span></span>
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. <span data-ttu-id="98608-113">Utilizzare `aspnet_regiis –pef connectionStrings` per crittografare nuovamente il file web.config.</span><span class="sxs-lookup"><span data-stu-id="98608-113">Use `aspnet_regiis –pef connectionStrings` to re-encrypt the web.config file.</span></span> 
7. <span data-ttu-id="98608-114">Rinominare web.config con Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span><span class="sxs-lookup"><span data-stu-id="98608-114">Rename web.config to Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span></span> 

#### <a name="to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs"></a><span data-ttu-id="98608-115">Per preparare il database del contenuto e il Cestino per l'eliminazione immediata dei BLOB orfani.</span><span class="sxs-lookup"><span data-stu-id="98608-115">To prepare the content database and Recycle Bin to immediately delete orphaned BLOBs</span></span>
1. <span data-ttu-id="98608-116">In SQL Server in SQL Management Studio, eseguire le query di aggiornamento seguenti per il database del contenuto di destinazione:</span><span class="sxs-lookup"><span data-stu-id="98608-116">On the SQL Server, in SQL Management Studio, run the following update queries for the target content database:</span></span> 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. <span data-ttu-id="98608-117">Sul server Web front-end, in **Amministrazione centrale** modificare **Impostazioni generali applicazione Web** per il database del contenuto per disabilitare temporaneamente il Cestino.</span><span class="sxs-lookup"><span data-stu-id="98608-117">On the web front-end server, under **Central Administration**, edit the **Web Application General Settings** for the desired content database to temporarily disable the Recycle Bin.</span></span> <span data-ttu-id="98608-118">Questa azione svuoterà inoltre il Cestino per le relative raccolte siti.</span><span class="sxs-lookup"><span data-stu-id="98608-118">This action will also empty the Recycle Bin for any related site collections.</span></span> <span data-ttu-id="98608-119">A tale scopo, fare clic su **Amministrazione centrale** -> **Gestione dell'applicazione** -> **Applicazioni Web (Gestisci applicazioni web)** -> **SharePoint - 80** -> **Impostazioni generali applicazione**.</span><span class="sxs-lookup"><span data-stu-id="98608-119">To do this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="98608-120">Impostare **Stato Cestino** su **NO**.</span><span class="sxs-lookup"><span data-stu-id="98608-120">Set the **Recycle Bin Status** to **OFF**.</span></span>
   
    ![Impostazioni generali applicazione Web](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="to-run-the-maintainer"></a><span data-ttu-id="98608-122">Per eseguire Maintainer</span><span class="sxs-lookup"><span data-stu-id="98608-122">To run the Maintainer</span></span>
* <span data-ttu-id="98608-123">Sul server web front-end, nella Shell di gestione di SharePoint 2013, eseguire Maintainer come segue:</span><span class="sxs-lookup"><span data-stu-id="98608-123">On the web front-end server, in the SharePoint 2013 Management Shell, run the Maintainer as follows:</span></span>
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > <span data-ttu-id="98608-124">Solo l’operazione`GarbageCollection`è supportata per StorSimple in questo momento.</span><span class="sxs-lookup"><span data-stu-id="98608-124">Only the `GarbageCollection` operation is supported for StorSimple at this time.</span></span> <span data-ttu-id="98608-125">Si noti inoltre che i parametri per Microsoft.Data.SqlRemoteBlobs.Maintainer.exe distinguono tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="98608-125">Also note that the parameters issued for Microsoft.Data.SqlRemoteBlobs.Maintainer.exe are case sensitive.</span></span> 
  > 
  > 

#### <a name="to-revert-the-content-database-and-recycle-bin-settings"></a><span data-ttu-id="98608-126">Per ripristinare il database del contenuto e le impostazioni del Cestino</span><span class="sxs-lookup"><span data-stu-id="98608-126">To revert the content database and Recycle Bin settings</span></span>
1. <span data-ttu-id="98608-127">In SQL Server in SQL Management Studio, eseguire le query di aggiornamento seguenti per il database del contenuto di destinazione:</span><span class="sxs-lookup"><span data-stu-id="98608-127">On the SQL Server, in SQL Management Studio, run the following update queries for the target content database:</span></span>
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. <span data-ttu-id="98608-128">Sul server Web front-end, in **Amministrazione centrale** modificare **Impostazioni generali applicazione Web** per il database del contenuto per riabilitare il Cestino.</span><span class="sxs-lookup"><span data-stu-id="98608-128">On the web front-end server, in **Central Administration**, edit the **Web Application General Settings** for the desired content database to re-enable the Recycle Bin.</span></span> <span data-ttu-id="98608-129">A tale scopo, fare clic su **Amministrazione centrale** -> **Gestione dell'applicazione** -> **Applicazioni Web (Gestisci applicazioni web)** -> **SharePoint - 80** -> **Impostazioni generali applicazione**.</span><span class="sxs-lookup"><span data-stu-id="98608-129">To do this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="98608-130">Impostare lo stato del Cestino su **ON**.</span><span class="sxs-lookup"><span data-stu-id="98608-130">Set the Recycle Bin Status to **ON**.</span></span>

