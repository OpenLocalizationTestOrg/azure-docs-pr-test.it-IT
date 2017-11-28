---
title: aaaRun un Hadoop processo utilizzando Azure Cosmos DB e HDInsight | Documenti Microsoft
description: Informazioni su come toorun un semplice Hive, Pig e MapReduce processo con DB Cosmos Azure e Azure HDInsight.
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="1e16b-103"><a name="Azure Cosmos DB-HDInsight"></a>Eseguire un processo Apache Hive, Pig o Hadoop usando Azure Cosmos DB e HDInsight</span><span class="sxs-lookup"><span data-stu-id="1e16b-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="1e16b-104">In questa esercitazione illustra come toorun [Apache Hive][apache-hive], [Pig Apache][apache-pig], e [Apache Hadoop] [ apache-hadoop] Processi MapReduce in Azure HDInsight con connettore Hadoop Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1e16b-104">This tutorial shows you how toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="1e16b-105">Connettore Hadoop COSMOS DB consente tooact DB Cosmos come origine e sink per i processi Hive, Pig e MapReduce.</span><span class="sxs-lookup"><span data-stu-id="1e16b-105">Cosmos DB's Hadoop connector allows Cosmos DB tooact as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="1e16b-106">In questa esercitazione verrà utilizzato DB Cosmos come origine dati hello e di destinazione per i processi di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="1e16b-106">This tutorial will use Cosmos DB as both hello data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="1e16b-107">Dopo aver completato questa esercitazione, sarà in grado di tooanswer hello seguenti domande:</span><span class="sxs-lookup"><span data-stu-id="1e16b-107">After completing this tutorial, you'll be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="1e16b-108">Come si caricano i dati da Cosmos DB usando un processo Hive, Pig o MapReduce?</span><span class="sxs-lookup"><span data-stu-id="1e16b-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="1e16b-109">Come si archiviano i dati in Cosmos DB usando un processo Hive, Pig o MapReduce?</span><span class="sxs-lookup"><span data-stu-id="1e16b-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="1e16b-110">Si consiglia di iniziare, è possibile guardare hello seguente video, in cui è eseguito tramite un processo Hive usando DB Cosmos e HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e16b-110">We recommend getting started by watching hello following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="1e16b-111">Tornare quindi toothis articolo, in cui si riceverà i dettagli completi hello su come eseguire processi analitica sui dati Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1e16b-111">Then, return toothis article, where you'll receive hello full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="1e16b-112">Questa esercitazione presume che l'utente abbia una precedente esperienza nell'uso di Apache Hadoop, Hive e/o Pig.</span><span class="sxs-lookup"><span data-stu-id="1e16b-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="1e16b-113">Se si tooApache nuova Hadoop, Hive e Pig, si consiglia di visitare hello [documentazione di Apache Hadoop][apache-hadoop-doc].</span><span class="sxs-lookup"><span data-stu-id="1e16b-113">If you are new tooApache Hadoop, Hive, and Pig, we recommend visiting hello [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="1e16b-114">Questa esercitazione presuppone che si abbia esperienza con Cosmos DB e che sia disponibile un account Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1e16b-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="1e16b-115">Se si è tooCosmos nuovo database o non è un account Cosmos DB, estrarre il nostro [Introduzione] [ getting-started] pagina.</span><span class="sxs-lookup"><span data-stu-id="1e16b-115">If you are new tooCosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="1e16b-116">Non si dispone ora toocomplete hello esercitazione e visualizzare solo gli script di PowerShell per un esempio completo di hello tooget per Hive, Pig e MapReduce?</span><span class="sxs-lookup"><span data-stu-id="1e16b-116">Don't have time toocomplete hello tutorial and just want tooget hello full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="1e16b-117">È possibile ottenerli [qui][hdinsight-samples].</span><span class="sxs-lookup"><span data-stu-id="1e16b-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="1e16b-118">download di Hello contiene anche file hql, pig e java di hello per questi esempi.</span><span class="sxs-lookup"><span data-stu-id="1e16b-118">hello download also contains hello hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="1e16b-119"><a name="NewestVersion"></a>Versione più recente</span><span class="sxs-lookup"><span data-stu-id="1e16b-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="1e16b-120">Versione di Hadoop Connector</span><span class="sxs-lookup"><span data-stu-id="1e16b-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="1e16b-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="1e16b-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="1e16b-122">URI script</span><span class="sxs-lookup"><span data-stu-id="1e16b-122">Script Uri</span></span></th>
        <td><span data-ttu-id="1e16b-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="1e16b-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="1e16b-124">Data ultima modifica</span><span class="sxs-lookup"><span data-stu-id="1e16b-124">Date Modified</span></span></th>
        <td><span data-ttu-id="1e16b-125">26/04/2016</span><span class="sxs-lookup"><span data-stu-id="1e16b-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="1e16b-126">Versioni supportate di HDInsight</span><span class="sxs-lookup"><span data-stu-id="1e16b-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="1e16b-127">3.1, 3.2.</span><span class="sxs-lookup"><span data-stu-id="1e16b-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="1e16b-128">Registro modifiche</span><span class="sxs-lookup"><span data-stu-id="1e16b-128">Change Log</span></span></th>
        <td><span data-ttu-id="1e16b-129">Aggiornare Azure Cosmos DB Java SDK too1.6.0</span><span class="sxs-lookup"><span data-stu-id="1e16b-129">Updated Azure Cosmos DB Java SDK too1.6.0</span></span></br>
            <span data-ttu-id="1e16b-130">Aggiunta del supporto per le raccolte partizionate come origine e sink</span><span class="sxs-lookup"><span data-stu-id="1e16b-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="1e16b-131"><a name="Prerequisites"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1e16b-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="1e16b-132">Prima di seguire le istruzioni di hello in questa esercitazione, assicurarsi di aver seguito hello:</span><span class="sxs-lookup"><span data-stu-id="1e16b-132">Before following hello instructions in this tutorial, ensure that you have hello following:</span></span>

* <span data-ttu-id="1e16b-133">Un account Cosmos DB, un database e una raccolta di documenti all'interno.</span><span class="sxs-lookup"><span data-stu-id="1e16b-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="1e16b-134">Per altre informazioni, vedere l'[introduzione a Cosmos DB][getting-started].</span><span class="sxs-lookup"><span data-stu-id="1e16b-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="1e16b-135">Importare i dati di esempio al tuo account DB Cosmos con hello [lo strumento di importazione Cosmos DB][import-data].</span><span class="sxs-lookup"><span data-stu-id="1e16b-135">Import sample data into your Cosmos DB account with hello [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="1e16b-136">Velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="1e16b-136">Throughput.</span></span> <span data-ttu-id="1e16b-137">Le letture e le scritture da HDInsight verranno conteggiate rispetto alle unità di richiesta dell'unità di capacità.</span><span class="sxs-lookup"><span data-stu-id="1e16b-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="1e16b-138">Capacità di una stored procedure aggiuntiva all'interno di ciascun insieme di output.</span><span class="sxs-lookup"><span data-stu-id="1e16b-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="1e16b-139">Hello stored procedure vengono utilizzate per il trasferimento di documenti risultanti.</span><span class="sxs-lookup"><span data-stu-id="1e16b-139">hello stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="1e16b-140">Capacità per i documenti risultante hello dai processi di hello Hive, Pig e MapReduce.</span><span class="sxs-lookup"><span data-stu-id="1e16b-140">Capacity for hello resulting documents from hello Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="1e16b-141">*Facoltativo*Capacità per una raccolta aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="1e16b-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="1e16b-142">Ordine tooavoid hello creazione di una nuova raccolta durante uno dei processi di hello, è possibile stampare hello risultati toostdout, salvare contenitore WASB tooyour output di hello oppure specificare una raccolta già esistente.</span><span class="sxs-lookup"><span data-stu-id="1e16b-142">In order tooavoid hello creation of a new collection during any of hello jobs, you can either print hello results toostdout, save hello output tooyour WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="1e16b-143">In caso hello della specifica di una raccolta esistente, verranno creati nuovi documenti all'interno di hello e documenti già esistenti saranno interessati solo se si verifica un conflitto in *ID*.</span><span class="sxs-lookup"><span data-stu-id="1e16b-143">In hello case of specifying an existing collection, new documents will be created inside hello collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="1e16b-144">**connettore Hello sovrascrive automaticamente i documenti esistenti con conflitti tra id**.</span><span class="sxs-lookup"><span data-stu-id="1e16b-144">**hello connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="1e16b-145">È possibile disattivare questa funzionalità impostando hello upsert opzione toofalse.</span><span class="sxs-lookup"><span data-stu-id="1e16b-145">You can turn off this feature by setting hello upsert option toofalse.</span></span> <span data-ttu-id="1e16b-146">Se si verifica un conflitto upsert è false, avrà esito negativo del processo Hadoop hello; viene rilevato un errore di conflitto di id.</span><span class="sxs-lookup"><span data-stu-id="1e16b-146">If upsert is false and a conflict occurs, hello Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="1e16b-147"><a name="ProvisionHDInsight"></a>Passaggio 1: Creare un nuovo cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="1e16b-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="1e16b-148">Questa esercitazione Usa genera Script azione da hello Azure Portal toocustomize cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e16b-148">This tutorial uses Script Action from hello Azure Portal toocustomize your HDInsight cluster.</span></span> <span data-ttu-id="1e16b-149">In questa esercitazione si utilizzerà hello Azure Portal toocreate cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e16b-149">In this tutorial, we will use hello Azure Portal toocreate your HDInsight cluster.</span></span> <span data-ttu-id="1e16b-150">Per istruzioni su come i cmdlet di PowerShell toouse o hello HDInsight .NET SDK, vedere il [HDInsight personalizzare cluster tramite Script azione] [ hdinsight-custom-provision] articolo.</span><span class="sxs-lookup"><span data-stu-id="1e16b-150">For instructions on how toouse PowerShell cmdlets or hello HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="1e16b-151">Accedi toohello [portale Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="1e16b-151">Sign in toohello [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="1e16b-152">Fare clic su **+ nuovo** nella parte superiore di hello del riquadro di spostamento sinistro hello, Cerca **HDInsight** sulla barra di ricerca principale hello nuovo pannello hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-152">Click **+ New** on hello top of hello left navigation, search for **HDInsight** in hello top search bar on hello New blade.</span></span>
3. <span data-ttu-id="1e16b-153">**HDInsight** pubblicati da **Microsoft** verrà visualizzato nella parte superiore di hello dei risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-153">**HDInsight** published by **Microsoft** will appear at hello top of hello Results.</span></span> <span data-ttu-id="1e16b-154">Fare clic sulla voce e selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1e16b-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="1e16b-155">Nel nuovo HDInsight Cluster hello creare pannello, immettere il **nome Cluster** e seleziona hello **sottoscrizione** desiderato tooprovision questa risorsa in.</span><span class="sxs-lookup"><span data-stu-id="1e16b-155">On hello New HDInsight Cluster create blade, enter your **Cluster Name** and select hello **Subscription** you want tooprovision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="1e16b-156">Nome del cluster</span><span class="sxs-lookup"><span data-stu-id="1e16b-156">Cluster name</span></span></td><td><span data-ttu-id="1e16b-157">Cluster hello nome.</span><span class="sxs-lookup"><span data-stu-id="1e16b-157">Name hello cluster.</span></span><br/>
<span data-ttu-id="1e16b-158">Il nome DNS deve iniziare e finire con un carattere alfanumerico e può contenere trattini.</span><span class="sxs-lookup"><span data-stu-id="1e16b-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="1e16b-159">campo Hello deve essere una stringa di lunghezza compresa tra 3 e 63 caratteri.</span><span class="sxs-lookup"><span data-stu-id="1e16b-159">hello field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="1e16b-160">Nome sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="1e16b-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="1e16b-161">Se si dispone di più di una sottoscrizione di Azure, selezionare una sottoscrizione di hello che ospiterà il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e16b-161">If you have more than one Azure Subscription, select hello subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="1e16b-162">
5.Fare clic su **Seleziona tipo di Cluster** e hello set seguenti toohello di proprietà specificati.</span><span class="sxs-lookup"><span data-stu-id="1e16b-162">
5. Click **Select Cluster Type** and set hello following properties toohello specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="1e16b-163">Tipo di cluster</span><span class="sxs-lookup"><span data-stu-id="1e16b-163">Cluster type</span></span></td><td><span data-ttu-id="1e16b-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="1e16b-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="1e16b-165">Livello cluster</span><span class="sxs-lookup"><span data-stu-id="1e16b-165">Cluster tier</span></span></td><td><span data-ttu-id="1e16b-166"><strong>Standard</strong></span><span class="sxs-lookup"><span data-stu-id="1e16b-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="1e16b-167">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="1e16b-167">Operating System</span></span></td><td><span data-ttu-id="1e16b-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="1e16b-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="1e16b-169">Versione</span><span class="sxs-lookup"><span data-stu-id="1e16b-169">Version</span></span></td><td><span data-ttu-id="1e16b-170">versione più recente</span><span class="sxs-lookup"><span data-stu-id="1e16b-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="1e16b-171">A questo punto fare clic su **SELEZIONA**.</span><span class="sxs-lookup"><span data-stu-id="1e16b-171">Now, click **SELECT**.</span></span>

    ![Fornire i dettagli di iniziale del cluster Hadoop HDInsight][image-customprovision-page1]
6. <span data-ttu-id="1e16b-173">Fare clic su **credenziali** tooset le credenziali di accesso remoto e l'account di accesso.</span><span class="sxs-lookup"><span data-stu-id="1e16b-173">Click on **Credentials** tooset your login and remote access credentials.</span></span> <span data-ttu-id="1e16b-174">Scegliere il **nome utente dell'account di accesso del cluster** e la **password dell'account di accesso del cluster**.</span><span class="sxs-lookup"><span data-stu-id="1e16b-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="1e16b-175">Se si desidera tooremote in cluster, selezionare *Sì* nella parte inferiore di hello del pannello hello e fornire un nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="1e16b-175">If you want tooremote into your cluster, select *yes* at hello bottom of hello blade and provide a username and password.</span></span>
7. <span data-ttu-id="1e16b-176">Fare clic su **origine dati** tooset la posizione principale per i dati di accesso.</span><span class="sxs-lookup"><span data-stu-id="1e16b-176">Click on **Data Source** tooset your primary location for data access.</span></span> <span data-ttu-id="1e16b-177">Scegliere hello **Selezione metodo** e specificare un account di archiviazione già esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="1e16b-177">Choose hello **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="1e16b-178">In hello pannello stesso, specificare un **contenitore predefinito** e **percorso**.</span><span class="sxs-lookup"><span data-stu-id="1e16b-178">On hello same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="1e16b-179">Fare quindi clic su **SELEZIONA**.</span><span class="sxs-lookup"><span data-stu-id="1e16b-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1e16b-180">Selezionare un tooyour Chiudi percorso area dell'account DB Cosmos per migliorare le prestazioni</span><span class="sxs-lookup"><span data-stu-id="1e16b-180">Select a location close tooyour Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="1e16b-181">Fare clic su **prezzi** tooselect hello numero e tipo di nodi.</span><span class="sxs-lookup"><span data-stu-id="1e16b-181">Click on **Pricing** tooselect hello number and type of nodes.</span></span> <span data-ttu-id="1e16b-182">È possibile mantenere configurazione predefinita di hello e scala hello numero di nodi di lavoro in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="1e16b-182">You can keep hello default configuration and scale hello number of Worker nodes later on.</span></span>
10. <span data-ttu-id="1e16b-183">Fare clic su **configurazione facoltativa**, quindi **azioni Script** in hello pannello configurazione facoltativa.</span><span class="sxs-lookup"><span data-stu-id="1e16b-183">Click **Optional Configuration**, then **Script Actions** in hello Optional Configuration Blade.</span></span>

     <span data-ttu-id="1e16b-184">Nel riquadro azioni Script immettere hello toocustomize informazioni seguendo il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e16b-184">In Script Actions, enter hello following information toocustomize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="1e16b-185">Proprietà</span><span class="sxs-lookup"><span data-stu-id="1e16b-185">Property</span></span></th><th><span data-ttu-id="1e16b-186">Valore</span><span class="sxs-lookup"><span data-stu-id="1e16b-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="1e16b-187">Nome</span><span class="sxs-lookup"><span data-stu-id="1e16b-187">Name</span></span></td>
             <td><span data-ttu-id="1e16b-188">Specificare un nome per l'azione script hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-188">Specify a name for hello script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="1e16b-189">URI script</span><span class="sxs-lookup"><span data-stu-id="1e16b-189">Script URI</span></span></td>
             <td><span data-ttu-id="1e16b-190">Specificare hello URI toohello script che è richiamato toocustomize hello cluster.</span><span class="sxs-lookup"><span data-stu-id="1e16b-190">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span></br></br>
<span data-ttu-id="1e16b-191">Immettere:</span><span class="sxs-lookup"><span data-stu-id="1e16b-191">Please enter:</span></span> </br> <span data-ttu-id="1e16b-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="1e16b-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="1e16b-193">Head</span><span class="sxs-lookup"><span data-stu-id="1e16b-193">Head</span></span></td>
             <td><span data-ttu-id="1e16b-194">Fare clic sulla casella di controllo di prova toorun prova script di PowerShell nel nodo Head hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-194">Click hello checkbox toorun hello PowerShell script onto hello Head node.</span></span></br></br><span data-ttu-id="1e16b-195">
             <strong>Selezionare questa casella di controllo</strong>.</span><span class="sxs-lookup"><span data-stu-id="1e16b-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="1e16b-196">Worker</span><span class="sxs-lookup"><span data-stu-id="1e16b-196">Worker</span></span></td>
             <td><span data-ttu-id="1e16b-197">Fare clic su script PowerShell hello hello casella di controllo toorun nel nodo lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-197">Click hello checkbox toorun hello PowerShell script onto hello Worker node.</span></span></br></br><span data-ttu-id="1e16b-198">
             <strong>Selezionare questa casella di controllo</strong>.</span><span class="sxs-lookup"><span data-stu-id="1e16b-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="1e16b-199">Zookeeper</span><span class="sxs-lookup"><span data-stu-id="1e16b-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="1e16b-200">Fare clic su script PowerShell su hello Zookeeper hello casella di controllo toorun hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-200">Click hello checkbox toorun hello PowerShell script onto hello Zookeeper.</span></span></br></br><span data-ttu-id="1e16b-201">
             <strong>Non necessario</strong>.</span><span class="sxs-lookup"><span data-stu-id="1e16b-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="1e16b-202">parameters</span><span class="sxs-lookup"><span data-stu-id="1e16b-202">Parameters</span></span></td>
             <td><span data-ttu-id="1e16b-203">Specificare i parametri di hello, se richiesti dallo script hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-203">Specify hello parameters, if required by hello script.</span></span></br></br><span data-ttu-id="1e16b-204">
             <strong>Nessun parametro necessario</strong>.</span><span class="sxs-lookup"><span data-stu-id="1e16b-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="1e16b-205">
11. Creare un nuovo **gruppo di risorse** o usarne uno esistente nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e16b-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="1e16b-206">12.</span><span class="sxs-lookup"><span data-stu-id="1e16b-206">12.</span></span> <span data-ttu-id="1e16b-207">A questo punto, controllare **Pin toodashboard** tootrack la distribuzione e fare clic su **crea**!</span><span class="sxs-lookup"><span data-stu-id="1e16b-207">Now, check **Pin toodashboard** tootrack its deployment and click **Create**!</span></span>

## <span data-ttu-id="1e16b-208"><a name="InstallCmdlets"></a>Passaggio 2: Installare e configurare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e16b-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="1e16b-209">Installare Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e16b-209">Install Azure PowerShell.</span></span> <span data-ttu-id="1e16b-210">Le istruzioni sono consultabili [qui][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="1e16b-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="1e16b-211">In alternativa, solo per le query Hive, è possibile usare l'Editor Hive online di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e16b-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="1e16b-212">toodo accedere in tal caso, toohello [portale Azure][azure-portal], fare clic su **HDInsight** tooview riquadro sinistro di hello in un elenco dei cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e16b-212">toodo so, sign in toohello [Azure Portal][azure-portal], click **HDInsight** on hello left pane tooview a list of your HDInsight clusters.</span></span> <span data-ttu-id="1e16b-213">Fare clic su cluster hello si desidera che le query Hive toorun su e quindi fare clic su **Console Query**.</span><span class="sxs-lookup"><span data-stu-id="1e16b-213">Click hello cluster you want toorun Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="1e16b-214">Aprire Azure PowerShell Integrated Scripting Environment hello:</span><span class="sxs-lookup"><span data-stu-id="1e16b-214">Open hello Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="1e16b-215">In un computer che eseguono Windows 8 o Windows Server 2012 o versioni successive, è possibile utilizzare predefinito di hello ricerca.</span><span class="sxs-lookup"><span data-stu-id="1e16b-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use hello built-in Search.</span></span> <span data-ttu-id="1e16b-216">Dalla schermata Start hello digitare **powershell ise** e fare clic su **invio**.</span><span class="sxs-lookup"><span data-stu-id="1e16b-216">From hello Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="1e16b-217">In un computer che eseguono una versione precedente a Windows 8 o Windows Server 2012, utilizzare il menu di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use hello Start menu.</span></span> <span data-ttu-id="1e16b-218">Dal menu di avvio hello, digitare **prompt dei comandi** nella casella di ricerca hello, quindi nell'elenco di hello dei risultati, fare clic su **prompt dei comandi**.</span><span class="sxs-lookup"><span data-stu-id="1e16b-218">From hello Start menu, type **Command Prompt** in hello search box, then in hello list of results, click **Command Prompt**.</span></span> <span data-ttu-id="1e16b-219">In hello prompt dei comandi, digitare **powershell_ise** e fare clic su **invio**.</span><span class="sxs-lookup"><span data-stu-id="1e16b-219">In hello Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="1e16b-220">Aggiungere il proprio Account Azure.</span><span class="sxs-lookup"><span data-stu-id="1e16b-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="1e16b-221">Nel riquadro della Console hello, digitare **Add-AzureAccount** e fare clic su **invio**.</span><span class="sxs-lookup"><span data-stu-id="1e16b-221">In hello Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="1e16b-222">Digitare l'indirizzo di posta elettronica hello associati alla sottoscrizione Azure e fare clic su **continua**.</span><span class="sxs-lookup"><span data-stu-id="1e16b-222">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="1e16b-223">Digitare la password hello per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e16b-223">Type in hello password for your Azure subscription.</span></span>
   4. <span data-ttu-id="1e16b-224">Fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="1e16b-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="1e16b-225">Hello diagramma seguente identifica le parti importanti di hello dell'ambiente di Scripting PowerShell Azure.</span><span class="sxs-lookup"><span data-stu-id="1e16b-225">hello following diagram identifies hello important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Diagramma per Azure PowerShell][azure-powershell-diagram]

## <span data-ttu-id="1e16b-227"><a name="RunHive"></a>Passaggio 3: Eseguire un processo Hive usando Cosmos DB e HDInsight</span><span class="sxs-lookup"><span data-stu-id="1e16b-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1e16b-228">Tutte le variabili indicate da < > devono essere compilate usando le proprie impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1e16b-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="1e16b-229">Impostare hello seguenti variabili nel riquadro di Script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e16b-229">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="1e16b-230">Si inizia a costruire la stringa di query.</span><span class="sxs-lookup"><span data-stu-id="1e16b-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="1e16b-231">Da scrivere una query Hive che accetta i timestamp generati dal sistema ( TS) e un ID univoco ( RID) da una raccolta di Azure Cosmos DB tutti i documenti, conta tutti i documenti di minuto hello e quindi Archivia i risultati di hello in una nuova raccolta di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1e16b-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="1e16b-232">Creare prima di tutto una tabella Hive dalla raccolta Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1e16b-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="1e16b-233">Aggiungere hello seguente frammento di codice toohello riquadro di Script PowerShell <strong>dopo</strong> frammento di codice hello #1.</span><span class="sxs-lookup"><span data-stu-id="1e16b-233">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="1e16b-234">Assicurarsi di includere hello facoltativo DocumentDB.query parametro t trim nostri TS toojust di documenti e RID.</span><span class="sxs-lookup"><span data-stu-id="1e16b-234">Make sure you include hello optional DocumentDB.query parameter t trim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="1e16b-235">**La denominazione DocumentDB.inputCollections non è stata un errore.**</span><span class="sxs-lookup"><span data-stu-id="1e16b-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="1e16b-236">È effettivamente possibile aggiungere più raccolte come input:</span><span class="sxs-lookup"><span data-stu-id="1e16b-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="1e16b-237">Successivamente, creare una tabella Hive per la raccolta di output di hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-237">Next, let's create a Hive table for hello output collection.</span></span> <span data-ttu-id="1e16b-238">proprietà del documento di output di Hello sarà mese hello, giorno, ora, minuti e il numero totale di hello di occorrenze.</span><span class="sxs-lookup"><span data-stu-id="1e16b-238">hello output document properties will be hello month, day, hour, minute, and hello total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1e16b-239">**Ancora una volta, la denominazione di DocumentDB.outputCollections non è un errore.**</span><span class="sxs-lookup"><span data-stu-id="1e16b-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="1e16b-240">È effettivamente possibile aggiungere più raccolte come output:</span><span class="sxs-lookup"><span data-stu-id="1e16b-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="1e16b-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span><span class="sxs-lookup"><span data-stu-id="1e16b-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="1e16b-242">i nomi di raccolta Hello sono separati senza spazi, utilizzare solo una singola virgola.</span><span class="sxs-lookup"><span data-stu-id="1e16b-242">hello collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="1e16b-243">Verrà eseguita la distribuzione round robin dei documenti tra più raccolte.</span><span class="sxs-lookup"><span data-stu-id="1e16b-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="1e16b-244">Un batch di documenti verrà archiviato in una raccolta, quindi un secondo batch dei documenti verrà archiviato nella raccolta di hello successivo e così via.</span><span class="sxs-lookup"><span data-stu-id="1e16b-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="1e16b-245">Infine, si conteggio hello documenti per mese, giorno, ora e minuto e all'inserimento risultati hello in hello output tabella Hive.</span><span class="sxs-lookup"><span data-stu-id="1e16b-245">Finally, let's tally hello documents by month, day, hour, and minute and insert hello results back into hello output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="1e16b-246">Aggiungere hello seguente frammento di script toocreate la definizione di un processo Hive dalla query precedente hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-246">Add hello following script snippet toocreate a Hive job definition from hello previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="1e16b-247">È inoltre possibile utilizzare hello - File passare toospecify un file di script HiveQL in HDFS.</span><span class="sxs-lookup"><span data-stu-id="1e16b-247">You can also use hello -File switch toospecify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="1e16b-248">Aggiungere hello dopo l'ora di inizio hello toosave frammento di codice e inviare il processo Hive hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-248">Add hello following snippet toosave hello start time and submit hello Hive job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="1e16b-249">Aggiungere i seguenti toowait per hello Hive processo toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-249">Add hello following toowait for hello Hive job toocomplete.</span></span>

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="1e16b-250">Aggiungere hello segue tooprint hello standard hello e output inizio e ora di fine.</span><span class="sxs-lookup"><span data-stu-id="1e16b-250">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="1e16b-251">**Eseguire** il nuovo script.</span><span class="sxs-lookup"><span data-stu-id="1e16b-251">**Run** your new script!</span></span> <span data-ttu-id="1e16b-252">**Fare clic su** verde hello pulsante Esegui.</span><span class="sxs-lookup"><span data-stu-id="1e16b-252">**Click** hello green execute button.</span></span>
8. <span data-ttu-id="1e16b-253">Controllare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-253">Check hello results.</span></span> <span data-ttu-id="1e16b-254">Sign in hello [portale Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="1e16b-254">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="1e16b-255">Fare clic su <strong>Sfoglia</strong> nel Pannello di sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-255">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
   2. <span data-ttu-id="1e16b-256">Fare clic su <strong>tutto</strong> in alto a destra di hello del pannello Sfoglia hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-256">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
   3. <span data-ttu-id="1e16b-257">Trovare e fare clic su <strong>Account Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="1e16b-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="1e16b-258">Successivamente, individuare il <strong>Azure Cosmos DB Account</strong>, quindi <strong>Azure Cosmos DB Database</strong> e <strong>Azure Cosmos DB raccolta</strong> associato specificato nella raccolta di output di hello la query Hive.</span><span class="sxs-lookup"><span data-stu-id="1e16b-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="1e16b-259">Infine, fare clic su <strong>Esplora documenti</strong> sotto <strong>Strumenti di sviluppo</strong>.</span><span class="sxs-lookup"><span data-stu-id="1e16b-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="1e16b-260">Vengono visualizzati hello risultati della query Hive.</span><span class="sxs-lookup"><span data-stu-id="1e16b-260">You will see hello results of your Hive query.</span></span>

   ![Risultati della query relativa alla tabella][image-hive-query-results]

## <span data-ttu-id="1e16b-262"><a name="RunPig"></a>Passaggio 4: Eseguire un processo Pig usando Cosmos DB e HDInsight</span><span class="sxs-lookup"><span data-stu-id="1e16b-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1e16b-263">Tutte le variabili indicate da < > devono essere compilate usando le proprie impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1e16b-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="1e16b-264">Impostare hello seguenti variabili nel riquadro di Script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e16b-264">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="1e16b-265">Si inizia a costruire la stringa di query.</span><span class="sxs-lookup"><span data-stu-id="1e16b-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="1e16b-266">Da scrivere una query Pig che accetta i timestamp generati dal sistema ( TS) e un ID univoco ( RID) da una raccolta di Azure Cosmos DB tutti i documenti, conta tutti i documenti di minuto hello e quindi Archivia i risultati di hello in una nuova raccolta di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1e16b-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="1e16b-267">In primo luogo, caricare i documenti da Cosmos DB in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e16b-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="1e16b-268">Aggiungere hello seguente frammento di codice toohello riquadro di Script PowerShell <strong>dopo</strong> frammento di codice hello #1.</span><span class="sxs-lookup"><span data-stu-id="1e16b-268">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="1e16b-269">Assicurarsi che tooadd un DocumentDB query toohello facoltativo DocumentDB query parametro tootrim nostri TS toojust di documenti e RID.</span><span class="sxs-lookup"><span data-stu-id="1e16b-269">Make sure tooadd a DocumentDB query toohello optional DocumentDB query parameter tootrim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="1e16b-270">È effettivamente possibile aggiungere più raccolte come input:</span><span class="sxs-lookup"><span data-stu-id="1e16b-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="1e16b-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span><span class="sxs-lookup"><span data-stu-id="1e16b-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="1e16b-272">i nomi di raccolta Hello sono separati senza spazi, utilizzare solo una singola virgola.</span><span class="sxs-lookup"><span data-stu-id="1e16b-272">hello collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="1e16b-273">Verrà eseguita la distribuzione round robin dei documenti tra più raccolte.</span><span class="sxs-lookup"><span data-stu-id="1e16b-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="1e16b-274">Un batch di documenti verrà archiviato in una raccolta, quindi un secondo batch dei documenti verrà archiviato nella raccolta di hello successivo e così via.</span><span class="sxs-lookup"><span data-stu-id="1e16b-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="1e16b-275">Successivamente, consente di calcolare documenti hello dal mese di hello, giorno, ora, minuti e il numero totale di hello di occorrenze.</span><span class="sxs-lookup"><span data-stu-id="1e16b-275">Next, let's tally hello documents by hello month, day, hour, minute, and hello total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="1e16b-276">Infine, si archiviare i risultati di hello nella nuova raccolta di output.</span><span class="sxs-lookup"><span data-stu-id="1e16b-276">Finally, let's store hello results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1e16b-277">È effettivamente possibile aggiungere più raccolte come output:</span><span class="sxs-lookup"><span data-stu-id="1e16b-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="1e16b-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span><span class="sxs-lookup"><span data-stu-id="1e16b-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="1e16b-279">i nomi di raccolta Hello sono separati senza spazi, utilizzare solo una singola virgola.</span><span class="sxs-lookup"><span data-stu-id="1e16b-279">hello collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="1e16b-280">Documenti verrà essere distribuito round robin tra hello più raccolte.</span><span class="sxs-lookup"><span data-stu-id="1e16b-280">Documents will be distributed round-robin across hello multiple collections.</span></span> <span data-ttu-id="1e16b-281">Un batch di documenti verrà archiviato in una raccolta, quindi un secondo batch dei documenti verrà archiviato nella raccolta di hello successivo e così via.</span><span class="sxs-lookup"><span data-stu-id="1e16b-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="1e16b-282">Aggiungere hello seguente frammento di script toocreate la definizione di un processo Pig dalla query precedente hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-282">Add hello following script snippet toocreate a Pig job definition from hello previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="1e16b-283">È inoltre possibile utilizzare hello - File passare toospecify un file di script Pig in HDFS.</span><span class="sxs-lookup"><span data-stu-id="1e16b-283">You can also use hello -File switch toospecify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="1e16b-284">Aggiungere hello dopo l'ora di inizio hello toosave frammento di codice e inviare il processo Pig hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-284">Add hello following snippet toosave hello start time and submit hello Pig job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="1e16b-285">Aggiungere i seguenti toowait per hello Pig processo toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-285">Add hello following toowait for hello Pig job toocomplete.</span></span>

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="1e16b-286">Aggiungere hello segue tooprint hello standard hello e output inizio e ora di fine.</span><span class="sxs-lookup"><span data-stu-id="1e16b-286">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="1e16b-287">**Eseguire** il nuovo script.</span><span class="sxs-lookup"><span data-stu-id="1e16b-287">**Run** your new script!</span></span> <span data-ttu-id="1e16b-288">**Fare clic su** verde hello pulsante Esegui.</span><span class="sxs-lookup"><span data-stu-id="1e16b-288">**Click** hello green execute button.</span></span>
10. <span data-ttu-id="1e16b-289">Controllare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-289">Check hello results.</span></span> <span data-ttu-id="1e16b-290">Sign in hello [portale Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="1e16b-290">Sign into hello [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="1e16b-291">Fare clic su <strong>Sfoglia</strong> nel Pannello di sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-291">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
    2. <span data-ttu-id="1e16b-292">Fare clic su <strong>tutto</strong> in alto a destra di hello del pannello Sfoglia hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-292">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
    3. <span data-ttu-id="1e16b-293">Trovare e fare clic su <strong>Account Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="1e16b-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="1e16b-294">Successivamente, individuare il <strong>Azure Cosmos DB Account</strong>, quindi <strong>Azure Cosmos DB Database</strong> e <strong>Azure Cosmos DB raccolta</strong> associato specificato nella raccolta di output di hello la query Pig.</span><span class="sxs-lookup"><span data-stu-id="1e16b-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="1e16b-295">Infine, fare clic su <strong>Esplora documenti</strong> sotto <strong>Strumenti di sviluppo</strong>.</span><span class="sxs-lookup"><span data-stu-id="1e16b-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="1e16b-296">Vengono visualizzati hello risultati della query Pig.</span><span class="sxs-lookup"><span data-stu-id="1e16b-296">You will see hello results of your Pig query.</span></span>

    ![Risultati della query SQL][image-pig-query-results]

## <span data-ttu-id="1e16b-298"><a name="RunMapReduce"></a>Passaggio 5: Eseguire un processo MapReduce usando Azure Cosmos DB e HDInsight</span><span class="sxs-lookup"><span data-stu-id="1e16b-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="1e16b-299">Impostare hello seguenti variabili nel riquadro di Script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e16b-299">Set hello following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="1e16b-300">Verrà verrà eseguito un processo MapReduce che conta il numero di hello di occorrenze per ogni proprietà di documento dalla raccolta di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1e16b-300">We'll execute a MapReduce job that tallies hello number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="1e16b-301">Aggiungere questo frammento di script **dopo** frammento hello precedente.</span><span class="sxs-lookup"><span data-stu-id="1e16b-301">Add this script snippet **after** hello snippet above.</span></span>

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="1e16b-302">TallyProperties v01.jar viene fornito con installazione personalizzata di hello di hello connettore Hadoop di DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="1e16b-302">TallyProperties-v01.jar comes with hello custom installation of hello Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="1e16b-303">Aggiungere hello processo MapReduce hello toosubmit il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="1e16b-303">Add hello following command toosubmit hello MapReduce job.</span></span>

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="1e16b-304">Inoltre toohello definizione processo MapReduce, è inoltre fornire nome del cluster HDInsight hello in cui si desidera il processo MapReduce toorun hello e le credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-304">In addition toohello MapReduce job definition, you also provide hello HDInsight cluster name where you want toorun hello MapReduce job, and hello credentials.</span></span> <span data-ttu-id="1e16b-305">Start-AzureHDInsightJob Hello è una chiamata asincrona.</span><span class="sxs-lookup"><span data-stu-id="1e16b-305">hello Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="1e16b-306">completamento di hello toocheck del processo di hello, utilizzare hello *Wait-AzureHDInsightJob* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1e16b-306">toocheck hello completion of hello job, use hello *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="1e16b-307">Aggiungere hello successivo comando toocheck tutti gli errori con il processo MapReduce hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1e16b-307">Add hello following command toocheck any errors with running hello MapReduce job.</span></span>

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="1e16b-308">**Eseguire** il nuovo script.</span><span class="sxs-lookup"><span data-stu-id="1e16b-308">**Run** your new script!</span></span> <span data-ttu-id="1e16b-309">**Fare clic su** verde hello pulsante Esegui.</span><span class="sxs-lookup"><span data-stu-id="1e16b-309">**Click** hello green execute button.</span></span>
6. <span data-ttu-id="1e16b-310">Controllare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-310">Check hello results.</span></span> <span data-ttu-id="1e16b-311">Sign in hello [portale Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="1e16b-311">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="1e16b-312">Fare clic su <strong>Sfoglia</strong> nel Pannello di sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-312">Click <strong>Browse</strong> on hello left-side panel.</span></span>
   2. <span data-ttu-id="1e16b-313">Fare clic su <strong>tutto</strong> in alto a destra di hello del pannello Sfoglia hello.</span><span class="sxs-lookup"><span data-stu-id="1e16b-313">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span>
   3. <span data-ttu-id="1e16b-314">Trovare e fare clic su <strong>Account Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="1e16b-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="1e16b-315">Successivamente, individuare il <strong>Azure Cosmos DB Account</strong>, quindi <strong>Azure Cosmos DB Database</strong> e <strong>Azure Cosmos DB raccolta</strong> associato specificato nella raccolta di output di hello il processo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="1e16b-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="1e16b-316">Infine, fare clic su <strong>Esplora documenti</strong> sotto <strong>Strumenti di sviluppo</strong>.</span><span class="sxs-lookup"><span data-stu-id="1e16b-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="1e16b-317">Vengono visualizzati risultati hello del processo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="1e16b-317">You will see hello results of your MapReduce job.</span></span>

      ![Risultati della query MapReduce][image-mapreduce-query-results]

## <span data-ttu-id="1e16b-319"><a name="NextSteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1e16b-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="1e16b-320">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="1e16b-320">Congratulations!</span></span> <span data-ttu-id="1e16b-321">Sono stati eseguiti i primi processi Hive, Pig e MapReduce usando Azure Cosmos DB e HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e16b-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="1e16b-322">Abbiamo reso Open Source il connettore Hadoop.</span><span class="sxs-lookup"><span data-stu-id="1e16b-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="1e16b-323">Se si è interessati, è possibile contribuire in [GitHub][github].</span><span class="sxs-lookup"><span data-stu-id="1e16b-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="1e16b-324">toolearn informazioni, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="1e16b-324">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="1e16b-325">[Sviluppare un'applicazione Java con Documentdb][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="1e16b-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="1e16b-326">[Sviluppare programmi MapReduce Java per Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="1e16b-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="1e16b-327">[Introduzione all'uso di Hadoop con Hive in uso di HDInsight tooanalyze palmari mobili][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="1e16b-327">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="1e16b-328">[Usare MapReduce con HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="1e16b-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="1e16b-329">[Usare Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="1e16b-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="1e16b-330">[Usare Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="1e16b-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="1e16b-331">[Personalizzare cluster HDInsight mediante l'azione script][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="1e16b-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
