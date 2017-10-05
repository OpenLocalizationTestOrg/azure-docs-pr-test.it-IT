---
title: Eseguire un processo Hadoop usando Azure Cosmos DB e HDInsight | Microsoft Docs
description: Informazioni su come eseguire un semplice processo Hive, Pig e MapReduce con Azure Cosmos DB e Azure HDInsight.
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
ms.openlocfilehash: 427864fc4e494c19fcda4cfd454a9923499f6337
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="47c83-103"><a name="Azure Cosmos DB-HDInsight"></a>Eseguire un processo Apache Hive, Pig o Hadoop usando Azure Cosmos DB e HDInsight</span><span class="sxs-lookup"><span data-stu-id="47c83-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="47c83-104">Questa esercitazione illustra come eseguire processi [Apache Hive][apache-hive], [Apache Pig][apache-pig] e [Apache Hadoop][apache-hadoop] MapReduce in Azure HDInsight con il connettore Hadoop di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47c83-104">This tutorial shows you how to run [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="47c83-105">Il connettore Hadoop di Cosmos DB consente a quest'ultimo di fungere da origine e sink per i processi Hive, Pig e MapReduce.</span><span class="sxs-lookup"><span data-stu-id="47c83-105">Cosmos DB's Hadoop connector allows Cosmos DB to act as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="47c83-106">Questa esercitazione userà Cosmos DB come origine dati e destinazione per i processi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="47c83-106">This tutorial will use Cosmos DB as both the data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="47c83-107">Dopo aver completato questa esercitazione, si potrà rispondere alle domande seguenti:</span><span class="sxs-lookup"><span data-stu-id="47c83-107">After completing this tutorial, you'll be able to answer the following questions:</span></span>

* <span data-ttu-id="47c83-108">Come si caricano i dati da Cosmos DB usando un processo Hive, Pig o MapReduce?</span><span class="sxs-lookup"><span data-stu-id="47c83-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="47c83-109">Come si archiviano i dati in Cosmos DB usando un processo Hive, Pig o MapReduce?</span><span class="sxs-lookup"><span data-stu-id="47c83-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="47c83-110">Per iniziare, è consigliabile guardare il video seguente che illustra un processo Hive usando Cosmos DB e HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47c83-110">We recommend getting started by watching the following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="47c83-111">Tornare quindi a questo articolo, che illustra in modo dettagliato come eseguire processi di analisi sui dati di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47c83-111">Then, return to this article, where you'll receive the full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="47c83-112">Questa esercitazione presume che l'utente abbia una precedente esperienza nell'uso di Apache Hadoop, Hive e/o Pig.</span><span class="sxs-lookup"><span data-stu-id="47c83-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="47c83-113">Se non si conoscono Apache Hadoop, Hive e Pig, si consiglia di vedere la pagina relativa alla [documentazione di Apache Hadoop][apache-hadoop-doc].</span><span class="sxs-lookup"><span data-stu-id="47c83-113">If you are new to Apache Hadoop, Hive, and Pig, we recommend visiting the [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="47c83-114">Questa esercitazione presuppone che si abbia esperienza con Cosmos DB e che sia disponibile un account Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47c83-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="47c83-115">Se non si conosce Cosmos DB o non si ha un account Cosmos DB, vedere la pagina [Per iniziare][getting-started].</span><span class="sxs-lookup"><span data-stu-id="47c83-115">If you are new to Cosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="47c83-116">Se non si ha tempo di completare l'esercitazione e si vogliono ottenere gli script PowerShell completi di esempio per Hive, Pig e MapReduce,</span><span class="sxs-lookup"><span data-stu-id="47c83-116">Don't have time to complete the tutorial and just want to get the full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="47c83-117">È possibile ottenerli [qui][hdinsight-samples].</span><span class="sxs-lookup"><span data-stu-id="47c83-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="47c83-118">Il download contiene anche i file hql, pig e java per questi esempi.</span><span class="sxs-lookup"><span data-stu-id="47c83-118">The download also contains the hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="47c83-119"><a name="NewestVersion"></a>Versione più recente</span><span class="sxs-lookup"><span data-stu-id="47c83-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="47c83-120">Versione di Hadoop Connector</span><span class="sxs-lookup"><span data-stu-id="47c83-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="47c83-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="47c83-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="47c83-122">URI script</span><span class="sxs-lookup"><span data-stu-id="47c83-122">Script Uri</span></span></th>
        <td><span data-ttu-id="47c83-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="47c83-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="47c83-124">Data ultima modifica</span><span class="sxs-lookup"><span data-stu-id="47c83-124">Date Modified</span></span></th>
        <td><span data-ttu-id="47c83-125">26/04/2016</span><span class="sxs-lookup"><span data-stu-id="47c83-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="47c83-126">Versioni supportate di HDInsight</span><span class="sxs-lookup"><span data-stu-id="47c83-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="47c83-127">3.1, 3.2.</span><span class="sxs-lookup"><span data-stu-id="47c83-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="47c83-128">Registro modifiche</span><span class="sxs-lookup"><span data-stu-id="47c83-128">Change Log</span></span></th>
        <td><span data-ttu-id="47c83-129">Aggiornamento di Azure Cosmos DB Java SDK alla versione 1.6.0</span><span class="sxs-lookup"><span data-stu-id="47c83-129">Updated Azure Cosmos DB Java SDK to 1.6.0</span></span></br>
            <span data-ttu-id="47c83-130">Aggiunta del supporto per le raccolte partizionate come origine e sink</span><span class="sxs-lookup"><span data-stu-id="47c83-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="47c83-131"><a name="Prerequisites"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="47c83-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="47c83-132">Prima di seguire le istruzioni di questa esercitazione, verificare che siano disponibili gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="47c83-132">Before following the instructions in this tutorial, ensure that you have the following:</span></span>

* <span data-ttu-id="47c83-133">Un account Cosmos DB, un database e una raccolta di documenti all'interno.</span><span class="sxs-lookup"><span data-stu-id="47c83-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="47c83-134">Per altre informazioni, vedere l'[introduzione a Cosmos DB][getting-started].</span><span class="sxs-lookup"><span data-stu-id="47c83-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="47c83-135">Importare dati di esempio nell'account Cosmos DB con lo [strumento di importazione di Cosmos DB][import-data].</span><span class="sxs-lookup"><span data-stu-id="47c83-135">Import sample data into your Cosmos DB account with the [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="47c83-136">Velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="47c83-136">Throughput.</span></span> <span data-ttu-id="47c83-137">Le letture e le scritture da HDInsight verranno conteggiate rispetto alle unità di richiesta dell'unità di capacità.</span><span class="sxs-lookup"><span data-stu-id="47c83-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="47c83-138">Capacità di una stored procedure aggiuntiva all'interno di ciascun insieme di output.</span><span class="sxs-lookup"><span data-stu-id="47c83-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="47c83-139">Le stored procedure vengono usate per trasferire i documenti risultanti.</span><span class="sxs-lookup"><span data-stu-id="47c83-139">The stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="47c83-140">Capacità per i documenti risultanti da processi Hive, Pig o MapReduce.</span><span class="sxs-lookup"><span data-stu-id="47c83-140">Capacity for the resulting documents from the Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="47c83-141">*Facoltativo*Capacità per una raccolta aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="47c83-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="47c83-142">Per evitare la creazione di una nuova raccolta durante uno qualsiasi dei processi è possibile stampare i risultati in stdout, salvare l'output nel contenitore WASB oppure specificare una raccolta già esistente.</span><span class="sxs-lookup"><span data-stu-id="47c83-142">In order to avoid the creation of a new collection during any of the jobs, you can either print the results to stdout, save the output to your WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="47c83-143">Nel caso in cui venga specificata una raccolta esistente, verranno creati nuovi documenti all'interno della raccolta, mentre i documenti esistenti verranno interessati solo se si verifica un conflitto tra gli *ids*.</span><span class="sxs-lookup"><span data-stu-id="47c83-143">In the case of specifying an existing collection, new documents will be created inside the collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="47c83-144">**Il connettore sovrascriverà automaticamente i documenti esistenti con conflitti tra ID**.</span><span class="sxs-lookup"><span data-stu-id="47c83-144">**The connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="47c83-145">È possibile disattivare questa funzionalità impostando l'opzione upsert su false.</span><span class="sxs-lookup"><span data-stu-id="47c83-145">You can turn off this feature by setting the upsert option to false.</span></span> <span data-ttu-id="47c83-146">Se upsert è impostato su false e si verifica un conflitto, il processo Hadoop avrà esito negativo, indicando un errore di conflitto tra ID.</span><span class="sxs-lookup"><span data-stu-id="47c83-146">If upsert is false and a conflict occurs, the Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="47c83-147"><a name="ProvisionHDInsight"></a>Passaggio 1: Creare un nuovo cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="47c83-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="47c83-148">Questa esercitazione usa Azioni script del portale di Azure per personalizzare il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47c83-148">This tutorial uses Script Action from the Azure Portal to customize your HDInsight cluster.</span></span> <span data-ttu-id="47c83-149">In questa esercitazione si userà il portale di Azure per creare un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47c83-149">In this tutorial, we will use the Azure Portal to create your HDInsight cluster.</span></span> <span data-ttu-id="47c83-150">Per istruzioni su come usare i cmdlet di PowerShell oppure HDInsight .NET SDK, vedere l'articolo [Personalizzare cluster HDInsight mediante Azione script][hdinsight-custom-provision].</span><span class="sxs-lookup"><span data-stu-id="47c83-150">For instructions on how to use PowerShell cmdlets or the HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="47c83-151">Accedere al [portale di Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="47c83-151">Sign in to the [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="47c83-152">Fare clic su **+ Nuovo** nella parte superiore del riquadro di spostamento a sinistra e cercare **HDInsight** nella barra di ricerca in alto nel pannello Nuovo.</span><span class="sxs-lookup"><span data-stu-id="47c83-152">Click **+ New** on the top of the left navigation, search for **HDInsight** in the top search bar on the New blade.</span></span>
3. <span data-ttu-id="47c83-153">**HDInsight** pubblicato da **Microsoft** verrà visualizzato in cima ai risultati.</span><span class="sxs-lookup"><span data-stu-id="47c83-153">**HDInsight** published by **Microsoft** will appear at the top of the Results.</span></span> <span data-ttu-id="47c83-154">Fare clic sulla voce e selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="47c83-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="47c83-155">Nel pannello Nuovo cluster HDInsight immettere un nome in **Nome cluster** e selezionare la **sottoscrizione** in cui effettuare il provisioning della risorsa.</span><span class="sxs-lookup"><span data-stu-id="47c83-155">On the New HDInsight Cluster create blade, enter your **Cluster Name** and select the **Subscription** you want to provision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="47c83-156">Nome del cluster</span><span class="sxs-lookup"><span data-stu-id="47c83-156">Cluster name</span></span></td><td><span data-ttu-id="47c83-157">Assegnare un nome al cluster.</span><span class="sxs-lookup"><span data-stu-id="47c83-157">Name the cluster.</span></span><br/>
<span data-ttu-id="47c83-158">Il nome DNS deve iniziare e finire con un carattere alfanumerico e può contenere trattini.</span><span class="sxs-lookup"><span data-stu-id="47c83-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="47c83-159">Il campo deve essere una stringa composta da un minimo di 3 a un massimo di 63 caratteri.</span><span class="sxs-lookup"><span data-stu-id="47c83-159">The field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="47c83-160">Nome sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="47c83-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="47c83-161">Se sono disponibili più sottoscrizioni di Azure, selezionare quella che ospiterà il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47c83-161">If you have more than one Azure Subscription, select the subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="47c83-162">
5. Fare clic su **Selezionare il tipo di cluster** e impostare le seguenti proprietà sui valori specificati.</span><span class="sxs-lookup"><span data-stu-id="47c83-162">
5. Click **Select Cluster Type** and set the following properties to the specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="47c83-163">Tipo di cluster</span><span class="sxs-lookup"><span data-stu-id="47c83-163">Cluster type</span></span></td><td><span data-ttu-id="47c83-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="47c83-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="47c83-165">Livello cluster</span><span class="sxs-lookup"><span data-stu-id="47c83-165">Cluster tier</span></span></td><td><span data-ttu-id="47c83-166"><strong>Standard</strong></span><span class="sxs-lookup"><span data-stu-id="47c83-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="47c83-167">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="47c83-167">Operating System</span></span></td><td><span data-ttu-id="47c83-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="47c83-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="47c83-169">Versione</span><span class="sxs-lookup"><span data-stu-id="47c83-169">Version</span></span></td><td><span data-ttu-id="47c83-170">versione più recente</span><span class="sxs-lookup"><span data-stu-id="47c83-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="47c83-171">A questo punto fare clic su **SELEZIONA**.</span><span class="sxs-lookup"><span data-stu-id="47c83-171">Now, click **SELECT**.</span></span>

    ![Fornire i dettagli di iniziale del cluster Hadoop HDInsight][image-customprovision-page1]
6. <span data-ttu-id="47c83-173">Fare clic su **Credenziali** per impostare le credenziali di accesso e di accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="47c83-173">Click on **Credentials** to set your login and remote access credentials.</span></span> <span data-ttu-id="47c83-174">Scegliere il **nome utente dell'account di accesso del cluster** e la **password dell'account di accesso del cluster**.</span><span class="sxs-lookup"><span data-stu-id="47c83-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="47c83-175">Se si intende accedere al cluster in modalità remota, selezionare *Sì* nella parte inferiore del pannello e specificare un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="47c83-175">If you want to remote into your cluster, select *yes* at the bottom of the blade and provide a username and password.</span></span>
7. <span data-ttu-id="47c83-176">Fare clic su **Origine dati** per impostare la posizione primaria per l'accesso ai dati.</span><span class="sxs-lookup"><span data-stu-id="47c83-176">Click on **Data Source** to set your primary location for data access.</span></span> <span data-ttu-id="47c83-177">Scegliere un'opzione in **Metodo di selezione** e specificare un account di archiviazione già esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="47c83-177">Choose the **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="47c83-178">Nello stesso pannello specificare un **contenitore predefinito** e una **località**.</span><span class="sxs-lookup"><span data-stu-id="47c83-178">On the same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="47c83-179">Fare quindi clic su **SELEZIONA**.</span><span class="sxs-lookup"><span data-stu-id="47c83-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="47c83-180">Per ottenere prestazioni migliori, selezionare una località vicina all'area dell'account Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47c83-180">Select a location close to your Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="47c83-181">Fare clic su **Prezzi** per selezionare numero e tipo di nodi.</span><span class="sxs-lookup"><span data-stu-id="47c83-181">Click on **Pricing** to select the number and type of nodes.</span></span> <span data-ttu-id="47c83-182">È possibile mantenere la configurazione predefinita e ridimensionare il numero di nodi del ruolo di lavoro in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="47c83-182">You can keep the default configuration and scale the number of Worker nodes later on.</span></span>
10. <span data-ttu-id="47c83-183">Fare clic su **Configurazione facoltativa** e quindi selezionare **Azioni script** nel pannello Configurazione facoltativa.</span><span class="sxs-lookup"><span data-stu-id="47c83-183">Click **Optional Configuration**, then **Script Actions** in the Optional Configuration Blade.</span></span>

     <span data-ttu-id="47c83-184">In Azioni script immettere le informazioni seguenti per personalizzare il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47c83-184">In Script Actions, enter the following information to customize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="47c83-185">Proprietà</span><span class="sxs-lookup"><span data-stu-id="47c83-185">Property</span></span></th><th><span data-ttu-id="47c83-186">Valore</span><span class="sxs-lookup"><span data-stu-id="47c83-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="47c83-187">Nome</span><span class="sxs-lookup"><span data-stu-id="47c83-187">Name</span></span></td>
             <td><span data-ttu-id="47c83-188">Specificare un nome per l'azione script.</span><span class="sxs-lookup"><span data-stu-id="47c83-188">Specify a name for the script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="47c83-189">URI script</span><span class="sxs-lookup"><span data-stu-id="47c83-189">Script URI</span></span></td>
             <td><span data-ttu-id="47c83-190">Specificare l'URI dello script da richiamare per personalizzare il cluster.</span><span class="sxs-lookup"><span data-stu-id="47c83-190">Specify the URI to the script that is invoked to customize the cluster.</span></span></br></br>
<span data-ttu-id="47c83-191">Immettere:</span><span class="sxs-lookup"><span data-stu-id="47c83-191">Please enter:</span></span> </br> <span data-ttu-id="47c83-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="47c83-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="47c83-193">Head</span><span class="sxs-lookup"><span data-stu-id="47c83-193">Head</span></span></td>
             <td><span data-ttu-id="47c83-194">Selezionare la casella di controllo per eseguire lo script di PowerShell nel nodo head.</span><span class="sxs-lookup"><span data-stu-id="47c83-194">Click the checkbox to run the PowerShell script onto the Head node.</span></span></br></br><span data-ttu-id="47c83-195">
             <strong>Selezionare questa casella di controllo</strong>.</span><span class="sxs-lookup"><span data-stu-id="47c83-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="47c83-196">Worker</span><span class="sxs-lookup"><span data-stu-id="47c83-196">Worker</span></span></td>
             <td><span data-ttu-id="47c83-197">Selezionare la casella di controllo per eseguire lo script di PowerShell nel nodo del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="47c83-197">Click the checkbox to run the PowerShell script onto the Worker node.</span></span></br></br><span data-ttu-id="47c83-198">
             <strong>Selezionare questa casella di controllo</strong>.</span><span class="sxs-lookup"><span data-stu-id="47c83-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="47c83-199">Zookeeper</span><span class="sxs-lookup"><span data-stu-id="47c83-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="47c83-200">Selezionare la casella di controllo per eseguire lo script di PowerShell nel nodo Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="47c83-200">Click the checkbox to run the PowerShell script onto the Zookeeper.</span></span></br></br><span data-ttu-id="47c83-201">
             <strong>Non necessario</strong>.</span><span class="sxs-lookup"><span data-stu-id="47c83-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="47c83-202">Parametri</span><span class="sxs-lookup"><span data-stu-id="47c83-202">Parameters</span></span></td>
             <td><span data-ttu-id="47c83-203">Specificare i parametri, se richiesti dallo script.</span><span class="sxs-lookup"><span data-stu-id="47c83-203">Specify the parameters, if required by the script.</span></span></br></br><span data-ttu-id="47c83-204">
             <strong>Nessun parametro necessario</strong>.</span><span class="sxs-lookup"><span data-stu-id="47c83-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="47c83-205">
11. Creare un nuovo **gruppo di risorse** o usarne uno esistente nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="47c83-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="47c83-206">12.</span><span class="sxs-lookup"><span data-stu-id="47c83-206">12.</span></span> <span data-ttu-id="47c83-207">Selezionare ora **Aggiungi al dashboard** per tenere traccia della distribuzione e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="47c83-207">Now, check **Pin to dashboard** to track its deployment and click **Create**!</span></span>

## <span data-ttu-id="47c83-208"><a name="InstallCmdlets"></a>Passaggio 2: Installare e configurare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="47c83-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="47c83-209">Installare Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47c83-209">Install Azure PowerShell.</span></span> <span data-ttu-id="47c83-210">Le istruzioni sono consultabili [qui][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="47c83-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="47c83-211">In alternativa, solo per le query Hive, è possibile usare l'Editor Hive online di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47c83-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="47c83-212">A tale scopo, accedere al [portale di Azure][azure-portal], fare clic su **HDInsight** nel riquadro sinistro per visualizzare un elenco dei cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47c83-212">To do so, sign in to the [Azure Portal][azure-portal], click **HDInsight** on the left pane to view a list of your HDInsight clusters.</span></span> <span data-ttu-id="47c83-213">Fare clic sul cluster che sul quale si vogliono eseguire le query Hive e quindi fare clic su **Console Query**.</span><span class="sxs-lookup"><span data-stu-id="47c83-213">Click the cluster you want to run Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="47c83-214">Aprire Integrated Scripting Environment di Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="47c83-214">Open the Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="47c83-215">In un computer che esegue Windows 8 o Windows Server 2012 o versione successiva, è possibile usare la funzionalità di ricerca incorporata.</span><span class="sxs-lookup"><span data-stu-id="47c83-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use the built-in Search.</span></span> <span data-ttu-id="47c83-216">Dalla schermata Start digitare **powershell ise** e fare clic su **Invio**.</span><span class="sxs-lookup"><span data-stu-id="47c83-216">From the Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="47c83-217">In un computer che esegue una versione di Windows precedente a Windows 8 o Windows Server 2012 è possibile usare il menu Start.</span><span class="sxs-lookup"><span data-stu-id="47c83-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use the Start menu.</span></span> <span data-ttu-id="47c83-218">Dal menu Start, digitare **Prompt dei comandi** nella casella di ricerca, quindi nell'elenco dei risultati, fare clic su **Prompt dei comandi**.</span><span class="sxs-lookup"><span data-stu-id="47c83-218">From the Start menu, type **Command Prompt** in the search box, then in the list of results, click **Command Prompt**.</span></span> <span data-ttu-id="47c83-219">Al prompt dei comandi digitare **powershell_ise** e fare clic su **Invio**.</span><span class="sxs-lookup"><span data-stu-id="47c83-219">In the Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="47c83-220">Aggiungere il proprio Account Azure.</span><span class="sxs-lookup"><span data-stu-id="47c83-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="47c83-221">Nel riquadro console digitare **Add-AzureAccount** e fare clic su **Invio**.</span><span class="sxs-lookup"><span data-stu-id="47c83-221">In the Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="47c83-222">Digitare l'indirizzo di posta elettronica associato alla sottoscrizione di Azure e fare clic su **Continua**.</span><span class="sxs-lookup"><span data-stu-id="47c83-222">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="47c83-223">Digitare la password per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="47c83-223">Type in the password for your Azure subscription.</span></span>
   4. <span data-ttu-id="47c83-224">Fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="47c83-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="47c83-225">Il diagramma seguente identifica le parti importanti dell'ambiente di Scripting PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="47c83-225">The following diagram identifies the important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Diagramma per Azure PowerShell][azure-powershell-diagram]

## <span data-ttu-id="47c83-227"><a name="RunHive"></a>Passaggio 3: Eseguire un processo Hive usando Cosmos DB e HDInsight</span><span class="sxs-lookup"><span data-stu-id="47c83-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="47c83-228">Tutte le variabili indicate da < > devono essere compilate usando le proprie impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="47c83-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="47c83-229">Impostare le variabili seguenti nel riquadro di script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47c83-229">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, the Azure Storage account and container that is used for the default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide the HDInsight cluster name where you want to run the Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="47c83-230">Si inizia a costruire la stringa di query.</span><span class="sxs-lookup"><span data-stu-id="47c83-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="47c83-231">Verrà scritta una query Hive che accetta i timestamp generati dal sistema di tutti i documenti (_ts) e ID univoci (_rid) da una raccolta di Azure Cosmos DB, calcola tutti i documenti in base al minuto e quindi archivia i risultati in una nuova raccolta di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47c83-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by the minute, and then stores the results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="47c83-232">Creare prima di tutto una tabella Hive dalla raccolta Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47c83-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="47c83-233">Aggiungere il seguente frammento di codice nel riquadro di script di PowerShell <strong>dopo</strong> il frammento di codice da #1.</span><span class="sxs-lookup"><span data-stu-id="47c83-233">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="47c83-234">Assicurarsi di includere il parametro DocumentDB.query facoltativo per ridurre i documenti semplicemente a _ts e _rid.</span><span class="sxs-lookup"><span data-stu-id="47c83-234">Make sure you include the optional DocumentDB.query parameter t trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="47c83-235">**La denominazione DocumentDB.inputCollections non è stata un errore.**</span><span class="sxs-lookup"><span data-stu-id="47c83-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="47c83-236">È effettivamente possibile aggiungere più raccolte come input:</span><span class="sxs-lookup"><span data-stu-id="47c83-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> The collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB the query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="47c83-237">Successivamente, si passa alla creazione di una tabella Hive per la raccolta di output.</span><span class="sxs-lookup"><span data-stu-id="47c83-237">Next, let's create a Hive table for the output collection.</span></span> <span data-ttu-id="47c83-238">Le proprietà del documento di output saranno mese, giorno, ora, minuti e numero totale di occorrenze.</span><span class="sxs-lookup"><span data-stu-id="47c83-238">The output document properties will be the month, day, hour, minute, and the total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="47c83-239">**Ancora una volta, la denominazione di DocumentDB.outputCollections non è un errore.**</span><span class="sxs-lookup"><span data-stu-id="47c83-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="47c83-240">È effettivamente possibile aggiungere più raccolte come output:</span><span class="sxs-lookup"><span data-stu-id="47c83-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="47c83-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span><span class="sxs-lookup"><span data-stu-id="47c83-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="47c83-242">I nomi di raccolta sono separati senza spazi, mediante una singola virgola.</span><span class="sxs-lookup"><span data-stu-id="47c83-242">The collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="47c83-243">Verrà eseguita la distribuzione round robin dei documenti tra più raccolte.</span><span class="sxs-lookup"><span data-stu-id="47c83-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="47c83-244">Un batch di documenti verrà archiviato in una raccolta, quindi un secondo batch dei documenti verrà archiviato nella raccolta successiva e così via.</span><span class="sxs-lookup"><span data-stu-id="47c83-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for the output data to DocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="47c83-245">Infine, si calcoleranno i documenti per mese, giorno, ora e minuto e si inseriranno i risultati nuovamente nell'output della tabella Hive.</span><span class="sxs-lookup"><span data-stu-id="47c83-245">Finally, let's tally the documents by month, day, hour, and minute and insert the results back into the output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="47c83-246">Aggiungere il frammento di script seguente per creare una definizione processo Hive dalla query precedente.</span><span class="sxs-lookup"><span data-stu-id="47c83-246">Add the following script snippet to create a Hive job definition from the previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="47c83-247">È anche possibile usare l'opzione -File per specificare un file di script HiveQL in HDFS.</span><span class="sxs-lookup"><span data-stu-id="47c83-247">You can also use the -File switch to specify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="47c83-248">Aggiungere il frammento seguente per salvare l'ora di inizio e inviare il processo Hive.</span><span class="sxs-lookup"><span data-stu-id="47c83-248">Add the following snippet to save the start time and submit the Hive job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="47c83-249">Aggiungere quanto segue per attendere il completamento del processo Hive.</span><span class="sxs-lookup"><span data-stu-id="47c83-249">Add the following to wait for the Hive job to complete.</span></span>

        # Wait for the Hive job to complete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="47c83-250">Aggiungere il comando seguente per stampare l'output standard e l'ora di inizio e fine.</span><span class="sxs-lookup"><span data-stu-id="47c83-250">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="47c83-251">**Eseguire** il nuovo script.</span><span class="sxs-lookup"><span data-stu-id="47c83-251">**Run** your new script!</span></span> <span data-ttu-id="47c83-252">**Fare clic** sul pulsante di esecuzione verde.</span><span class="sxs-lookup"><span data-stu-id="47c83-252">**Click** the green execute button.</span></span>
8. <span data-ttu-id="47c83-253">Verificare i risultati.</span><span class="sxs-lookup"><span data-stu-id="47c83-253">Check the results.</span></span> <span data-ttu-id="47c83-254">Accedere al [Portale di Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="47c83-254">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="47c83-255">Fare clic su <strong>Sfoglia</strong> nel riquadro a sinistra.</span><span class="sxs-lookup"><span data-stu-id="47c83-255">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
   2. <span data-ttu-id="47c83-256">Fare clic su <strong>tutto</strong> in alto a destra del riquadro di esplorazione.</span><span class="sxs-lookup"><span data-stu-id="47c83-256">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
   3. <span data-ttu-id="47c83-257">Trovare e fare clic su <strong>Account Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="47c83-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="47c83-258">Trovare quindi l'<strong>account Azure Cosmos DB</strong>, il <strong>database Azure Cosmos DB</strong> e la <strong>raccolta Azure Cosmos DB</strong> associati alla raccolta di output specificata nella query Hive.</span><span class="sxs-lookup"><span data-stu-id="47c83-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="47c83-259">Infine, fare clic su <strong>Esplora documenti</strong> sotto <strong>Strumenti di sviluppo</strong>.</span><span class="sxs-lookup"><span data-stu-id="47c83-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="47c83-260">Verranno visualizzati i risultati della query Hive.</span><span class="sxs-lookup"><span data-stu-id="47c83-260">You will see the results of your Hive query.</span></span>

   ![Risultati della query relativa alla tabella][image-hive-query-results]

## <span data-ttu-id="47c83-262"><a name="RunPig"></a>Passaggio 4: Eseguire un processo Pig usando Cosmos DB e HDInsight</span><span class="sxs-lookup"><span data-stu-id="47c83-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="47c83-263">Tutte le variabili indicate da < > devono essere compilate usando le proprie impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="47c83-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="47c83-264">Impostare le variabili seguenti nel riquadro di script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47c83-264">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want to run the Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="47c83-265">Si inizia a costruire la stringa di query.</span><span class="sxs-lookup"><span data-stu-id="47c83-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="47c83-266">Verrà scritta una query Pig che accetta i timestamp generati dal sistema di tutti i documenti (_ts) e ID univoci (_rid) da una raccolta di Azure Cosmos DB, calcola tutti i documenti in base al minuto e quindi archivia i risultati in una nuova raccolta di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47c83-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by the minute, and then stores the results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="47c83-267">In primo luogo, caricare i documenti da Cosmos DB in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47c83-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="47c83-268">Aggiungere il seguente frammento di codice nel riquadro di script di PowerShell <strong>dopo</strong> il frammento di codice da #1.</span><span class="sxs-lookup"><span data-stu-id="47c83-268">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="47c83-269">Assicurarsi di aggiungere una query di DocumentDB al parametro di query DocumentDB facoltativo per ridurre i documenti semplicemente a _ts e _rid.</span><span class="sxs-lookup"><span data-stu-id="47c83-269">Make sure to add a DocumentDB query to the optional DocumentDB query parameter to trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="47c83-270">È effettivamente possibile aggiungere più raccolte come input:</span><span class="sxs-lookup"><span data-stu-id="47c83-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="47c83-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span><span class="sxs-lookup"><span data-stu-id="47c83-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="47c83-272">I nomi di raccolta sono separati senza spazi, mediante una singola virgola.</span><span class="sxs-lookup"><span data-stu-id="47c83-272">The collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="47c83-273">Verrà eseguita la distribuzione round robin dei documenti tra più raccolte.</span><span class="sxs-lookup"><span data-stu-id="47c83-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="47c83-274">Un batch di documenti verrà archiviato in una raccolta, quindi un secondo batch dei documenti verrà archiviato nella raccolta successiva e così via.</span><span class="sxs-lookup"><span data-stu-id="47c83-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="47c83-275">Successivamente, verranno calcolati i documenti in base a mese, giorno, ora, minuti e numero totale di occorrenze.</span><span class="sxs-lookup"><span data-stu-id="47c83-275">Next, let's tally the documents by the month, day, hour, minute, and the total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="47c83-276">Infine, si archivieranno i risultati nella nuova raccolta di output.</span><span class="sxs-lookup"><span data-stu-id="47c83-276">Finally, let's store the results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="47c83-277">È effettivamente possibile aggiungere più raccolte come output:</span><span class="sxs-lookup"><span data-stu-id="47c83-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="47c83-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span><span class="sxs-lookup"><span data-stu-id="47c83-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="47c83-279">I nomi di raccolta sono separati senza spazi, mediante una singola virgola.</span><span class="sxs-lookup"><span data-stu-id="47c83-279">The collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="47c83-280">Verrà eseguita la distribuzione round robin dei documenti tra più raccolte.</span><span class="sxs-lookup"><span data-stu-id="47c83-280">Documents will be distributed round-robin across the multiple collections.</span></span> <span data-ttu-id="47c83-281">Un batch di documenti verrà archiviato in una raccolta, quindi un secondo batch dei documenti verrà archiviato nella raccolta successiva e così via.</span><span class="sxs-lookup"><span data-stu-id="47c83-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

        # Store output data to Cosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="47c83-282">Aggiungere il frammento di script seguente per creare una definizione processo Pig dalla query precedente.</span><span class="sxs-lookup"><span data-stu-id="47c83-282">Add the following script snippet to create a Pig job definition from the previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="47c83-283">È anche possibile usare l'opzione -File per specificare un file di script Pig in HDFS.</span><span class="sxs-lookup"><span data-stu-id="47c83-283">You can also use the -File switch to specify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="47c83-284">Aggiungere il frammento seguente per salvare l'ora di inizio e inviare il processo Pig.</span><span class="sxs-lookup"><span data-stu-id="47c83-284">Add the following snippet to save the start time and submit the Pig job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="47c83-285">Aggiungere quanto segue per attendere il completamento del processo Pig.</span><span class="sxs-lookup"><span data-stu-id="47c83-285">Add the following to wait for the Pig job to complete.</span></span>

        # Wait for the Pig job to complete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="47c83-286">Aggiungere il comando seguente per stampare l'output standard e l'ora di inizio e fine.</span><span class="sxs-lookup"><span data-stu-id="47c83-286">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="47c83-287">**Eseguire** il nuovo script.</span><span class="sxs-lookup"><span data-stu-id="47c83-287">**Run** your new script!</span></span> <span data-ttu-id="47c83-288">**Fare clic** sul pulsante di esecuzione verde.</span><span class="sxs-lookup"><span data-stu-id="47c83-288">**Click** the green execute button.</span></span>
10. <span data-ttu-id="47c83-289">Verificare i risultati.</span><span class="sxs-lookup"><span data-stu-id="47c83-289">Check the results.</span></span> <span data-ttu-id="47c83-290">Accedere al [Portale di Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="47c83-290">Sign into the [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="47c83-291">Fare clic su <strong>Sfoglia</strong> nel riquadro a sinistra.</span><span class="sxs-lookup"><span data-stu-id="47c83-291">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
    2. <span data-ttu-id="47c83-292">Fare clic su <strong>tutto</strong> in alto a destra del riquadro di esplorazione.</span><span class="sxs-lookup"><span data-stu-id="47c83-292">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
    3. <span data-ttu-id="47c83-293">Trovare e fare clic su <strong>Account Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="47c83-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="47c83-294">Trovare quindi l'<strong>account Azure Cosmos DB</strong>, il <strong>database Azure Cosmos DB</strong> e la <strong>raccolta Azure Cosmos DB</strong> associati alla raccolta di output specificata nella query Pig.</span><span class="sxs-lookup"><span data-stu-id="47c83-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="47c83-295">Infine, fare clic su <strong>Esplora documenti</strong> sotto <strong>Strumenti di sviluppo</strong>.</span><span class="sxs-lookup"><span data-stu-id="47c83-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="47c83-296">Verranno visualizzati i risultati della query Pig.</span><span class="sxs-lookup"><span data-stu-id="47c83-296">You will see the results of your Pig query.</span></span>

    ![Risultati della query SQL][image-pig-query-results]

## <span data-ttu-id="47c83-298"><a name="RunMapReduce"></a>Passaggio 5: Eseguire un processo MapReduce usando Azure Cosmos DB e HDInsight</span><span class="sxs-lookup"><span data-stu-id="47c83-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="47c83-299">Impostare le variabili seguenti nel riquadro di script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47c83-299">Set the following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="47c83-300">È possibile eseguire un processo MapReduce che calcola il numero di occorrenze per ogni proprietà di documento dalla raccolta Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47c83-300">We'll execute a MapReduce job that tallies the number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="47c83-301">Aggiungere questo frammento di script **dopo** il frammento di codice riportato sopra.</span><span class="sxs-lookup"><span data-stu-id="47c83-301">Add this script snippet **after** the snippet above.</span></span>

        # Define the MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="47c83-302">Il file TallyProperties-v01.jar viene fornito con l'installazione personalizzata del connettore Hadoop di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47c83-302">TallyProperties-v01.jar comes with the custom installation of the Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="47c83-303">Per inviare il processo MapReduce, aggiungere il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="47c83-303">Add the following command to submit the MapReduce job.</span></span>

        # Save the start time and submit the job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="47c83-304">Oltre alla definizione del processo MapReduce, è necessario specificare anche il nome del cluster HDInsight in cui si desidera eseguire il processo MapReduce e le credenziali.</span><span class="sxs-lookup"><span data-stu-id="47c83-304">In addition to the MapReduce job definition, you also provide the HDInsight cluster name where you want to run the MapReduce job, and the credentials.</span></span> <span data-ttu-id="47c83-305">Start-AzureHDInsightJob è una chiamata non sincronizzata.</span><span class="sxs-lookup"><span data-stu-id="47c83-305">The Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="47c83-306">Per verificare il completamento del processo, usare il cmdlet *Wait-AzureHDInsightJob* .</span><span class="sxs-lookup"><span data-stu-id="47c83-306">To check the completion of the job, use the *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="47c83-307">Per controllare se si sono verificati errori nel processo MapReduce, aggiungere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="47c83-307">Add the following command to check any errors with running the MapReduce job.</span></span>

        # Get the job output and print the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="47c83-308">**Eseguire** il nuovo script.</span><span class="sxs-lookup"><span data-stu-id="47c83-308">**Run** your new script!</span></span> <span data-ttu-id="47c83-309">**Fare clic** sul pulsante di esecuzione verde.</span><span class="sxs-lookup"><span data-stu-id="47c83-309">**Click** the green execute button.</span></span>
6. <span data-ttu-id="47c83-310">Verificare i risultati.</span><span class="sxs-lookup"><span data-stu-id="47c83-310">Check the results.</span></span> <span data-ttu-id="47c83-311">Accedere al [Portale di Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="47c83-311">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="47c83-312">Fare clic su <strong>Sfoglia</strong> nel riquadro a sinistra.</span><span class="sxs-lookup"><span data-stu-id="47c83-312">Click <strong>Browse</strong> on the left-side panel.</span></span>
   2. <span data-ttu-id="47c83-313">Fare clic su <strong>tutto</strong> in alto a destra del riquadro di esplorazione.</span><span class="sxs-lookup"><span data-stu-id="47c83-313">Click <strong>everything</strong> at the top-right of the browse panel.</span></span>
   3. <span data-ttu-id="47c83-314">Trovare e fare clic su <strong>Account Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="47c83-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="47c83-315">Trovare quindi l'<strong>account Azure Cosmos DB</strong>, il <strong>database Azure Cosmos DB</strong> e la <strong>raccolta Azure Cosmos DB</strong> associati alla raccolta di output specificata nel processo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="47c83-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="47c83-316">Infine, fare clic su <strong>Esplora documenti</strong> sotto <strong>Strumenti di sviluppo</strong>.</span><span class="sxs-lookup"><span data-stu-id="47c83-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="47c83-317">Verranno visualizzati i risultati del processo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="47c83-317">You will see the results of your MapReduce job.</span></span>

      ![Risultati della query MapReduce][image-mapreduce-query-results]

## <span data-ttu-id="47c83-319"><a name="NextSteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="47c83-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="47c83-320">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="47c83-320">Congratulations!</span></span> <span data-ttu-id="47c83-321">Sono stati eseguiti i primi processi Hive, Pig e MapReduce usando Azure Cosmos DB e HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47c83-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="47c83-322">Abbiamo reso Open Source il connettore Hadoop.</span><span class="sxs-lookup"><span data-stu-id="47c83-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="47c83-323">Se si è interessati, è possibile contribuire in [GitHub][github].</span><span class="sxs-lookup"><span data-stu-id="47c83-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="47c83-324">Per altre informazioni, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="47c83-324">To learn more, see the following articles:</span></span>

* <span data-ttu-id="47c83-325">[Sviluppare un'applicazione Java con Documentdb][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="47c83-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="47c83-326">[Sviluppare programmi MapReduce Java per Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="47c83-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="47c83-327">[Introduzione all'uso di Hadoop con Hive in HDInsight per analizzare l'uso di telefoni cellulari][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="47c83-327">[Get started using Hadoop with Hive in HDInsight to analyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="47c83-328">[Usare MapReduce con HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="47c83-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="47c83-329">[Usare Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="47c83-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="47c83-330">[Usare Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="47c83-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="47c83-331">[Personalizzare cluster HDInsight mediante l'azione script][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="47c83-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

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
