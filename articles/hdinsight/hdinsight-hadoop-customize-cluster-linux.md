---
title: Personalizzare cluster HDInsight tramite l'azione script - Azure | Microsoft Docs
description: "Aggiungere componenti personalizzati in cluster HDInsight basati su Linux usando azioni di script. Le azioni script sono script bash utilizzabili per personalizzare la configurazione del cluster o aggiungere servizi e utilità, come Hue, Solr o R."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 0c5d00b6cb9f68a1a0e474f81c969eb1b5654c67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="a4286-104">Personalizzare cluster HDInsight basati su Linux tramite Azione script</span><span class="sxs-lookup"><span data-stu-id="a4286-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="a4286-105">HDInsight offre un'opzione di configurazione denominata **Azione script** che richiama script personalizzati per la personalizzazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize the cluster.</span></span> <span data-ttu-id="a4286-106">Questi script vengono utilizzati per installare i componenti aggiuntivi e modificare le impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="a4286-106">These scripts are used to install additional components and change configuration settings.</span></span> <span data-ttu-id="a4286-107">Le azioni script possono essere utilizzate durante o dopo la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4286-108">La possibilità di usare le azioni script in un cluster già in esecuzione è disponibile solo per i cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="a4286-108">The ability to use script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="a4286-109">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="a4286-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a4286-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a4286-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="a4286-111">Le azioni di script possono anche essere pubblicate in Azure Marketplace come applicazione HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4286-111">Script actions can also be published to the Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="a4286-112">Alcuni esempi in questo documento mostrano come è possibile installare un'applicazione HDInsight usando i comandi di azione script di PowerShell e .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="a4286-112">Some of the examples in this document show how you can install an HDInsight application using script action commands from PowerShell and the .NET SDK.</span></span> <span data-ttu-id="a4286-113">Per altre informazioni sulle applicazioni HDInsight, vedere [Pubblicare applicazioni HDInsight in Azure Marketplace](hdinsight-apps-publish-applications.md).</span><span class="sxs-lookup"><span data-stu-id="a4286-113">For more information on HDInsight applications, see [Publish HDInsight applications into the Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="a4286-114">autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="a4286-114">Permissions</span></span>

<span data-ttu-id="a4286-115">Se si usa un cluster HDInsight aggiunto a un dominio, sono necessarie due autorizzazioni Ambari per l'uso di azioni script con il cluster:</span><span class="sxs-lookup"><span data-stu-id="a4286-115">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with the cluster:</span></span>

* <span data-ttu-id="a4286-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: il ruolo di amministratore Ambari ha questa autorizzazione per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="a4286-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: The Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="a4286-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: sia l'amministratore cluster HDInsight che l'amministratore Ambari hanno questa autorizzazione per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="a4286-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both the HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="a4286-118">Per altre informazioni sull'uso delle autorizzazioni con HDInsight aggiunto a un dominio, vedere [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Gestire cluster HDInsight aggiunti al dominio).</span><span class="sxs-lookup"><span data-stu-id="a4286-118">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="a4286-119">Controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="a4286-119">Access control</span></span>

<span data-ttu-id="a4286-120">Se non si è l'amministratore o il proprietario della sottoscrizione di Azure, l'account deve disporre almeno dell'accesso **Collaboratore** al gruppo di risorse contenente il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4286-120">If you are not the administrator/owner of your Azure subscription, your account must have at least **Contributor** access to the resource group that contains the HDInsight cluster.</span></span>

<span data-ttu-id="a4286-121">Se si crea un cluster HDInsight, è necessario che un utente con almeno l'accesso **Collaboratore** alla sottoscrizione di Azure abbia registrato in precedenza il provider per HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4286-121">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access to the Azure subscription must have previously registered the provider for HDInsight.</span></span> <span data-ttu-id="a4286-122">La registrazione del provider viene eseguita quando un utente con accesso Collaboratore alla sottoscrizione crea una risorsa per la prima volta nella sottoscrizione stessa.</span><span class="sxs-lookup"><span data-stu-id="a4286-122">Provider registration happens when a user with Contributor access to the subscription creates a resource for the first time on the subscription.</span></span> <span data-ttu-id="a4286-123">Può essere eseguita anche senza creare una risorsa [registrando un provider tramite REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4286-123">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="a4286-124">Per altre informazioni sull'uso della gestione degli accessi, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4286-124">For more information on working with access management, see the following documents:</span></span>

* [<span data-ttu-id="a4286-125">Introduzione alla gestione degli accessi nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a4286-125">Get started with access management in the Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="a4286-126">Usare le assegnazioni di ruolo per gestire l'accesso alle risorse della sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="a4286-126">Use role assignments to manage access to your Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="a4286-127">Informazioni sulle azioni script</span><span class="sxs-lookup"><span data-stu-id="a4286-127">Understanding Script Actions</span></span>

<span data-ttu-id="a4286-128">Un'azione script è semplicemente uno script Bash a cui si forniscono parametri e un URI.</span><span class="sxs-lookup"><span data-stu-id="a4286-128">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="a4286-129">Lo script viene eseguito nei nodi del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4286-129">The script runs on nodes in the HDInsight cluster.</span></span> <span data-ttu-id="a4286-130">Di seguito sono riportate le caratteristiche e funzionalità delle azioni script.</span><span class="sxs-lookup"><span data-stu-id="a4286-130">The following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="a4286-131">Devono essere archiviate in un URI accessibile dal cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4286-131">Must be stored on a URI that is accessible from the HDInsight cluster.</span></span> <span data-ttu-id="a4286-132">Di seguito vengono indicate alcune tra le posizioni di archiviazione possibili:</span><span class="sxs-lookup"><span data-stu-id="a4286-132">The following are possible storage locations:</span></span>

    * <span data-ttu-id="a4286-133">Account **Azure Data Lake Store** accessibile dal cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4286-133">An **Azure Data Lake Store** account that is accessible by the HDInsight cluster.</span></span> <span data-ttu-id="a4286-134">Per informazioni sull'uso di Azure Data Lake Store con HDInsight, vedere [Creare un cluster HDInsight con Data Lake Store usando il portale](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a4286-134">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="a4286-135">Quando si usa uno script archiviato in Data Lake Store, il formato dell'URI è `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span><span class="sxs-lookup"><span data-stu-id="a4286-135">When using a script stored in Data Lake Store, the URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="a4286-136">L'entità servizio usata da HDInsight per accedere a Data Lake Store deve avere accesso in lettura allo script.</span><span class="sxs-lookup"><span data-stu-id="a4286-136">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

    * <span data-ttu-id="a4286-137">Un BLOB in un **account di archiviazione di Azure** che rappresenta l'account di archiviazione primario o aggiuntivo per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4286-137">A blob in an **Azure Storage account** that is either the primary or additional storage account for the HDInsight cluster.</span></span> <span data-ttu-id="a4286-138">HDInsight può accedere a entrambi i tipi di account di archiviazione durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-138">HDInsight is granted access to both of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="a4286-139">Un servizio di condivisione file pubblico, ad esempio BLOB di Azure, GitHub, OneDrive, Dropbox e così via.</span><span class="sxs-lookup"><span data-stu-id="a4286-139">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="a4286-140">Per gli URI di esempio, vedere la sezione [Script di Azione script di esempio](#example-script-action-scripts).</span><span class="sxs-lookup"><span data-stu-id="a4286-140">For example URIs, see the [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="a4286-141">HDInsight supporta solo account di archiviazione di Azure __per uso generico__.</span><span class="sxs-lookup"><span data-stu-id="a4286-141">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="a4286-142">Non supporta attualmente il tipo di account di __archiviazione BLOB__.</span><span class="sxs-lookup"><span data-stu-id="a4286-142">It does not currently support the __Blob storage__ account type.</span></span>

* <span data-ttu-id="a4286-143">Possono essere limitate all'**esecuzione solo in alcuni tipi di nodi**, ad esempio nodi head o del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a4286-143">Can be restricted to **run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="a4286-144">Se usato con HDInsight Premium, è possibile specificare che lo script deve essere usato nel nodo perimetrale.</span><span class="sxs-lookup"><span data-stu-id="a4286-144">When used with HDInsight Premium, you can specify that the script should be used on the edge node.</span></span>

* <span data-ttu-id="a4286-145">Possono essere **persistenti** o **ad hoc**.</span><span class="sxs-lookup"><span data-stu-id="a4286-145">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="a4286-146">Gli script **persistenti** vengono applicati a nodi di lavoro aggiunti al cluster dopo l'esecuzione degli script.</span><span class="sxs-lookup"><span data-stu-id="a4286-146">**Persisted** scripts are applied to worker nodes added to the cluster after the script runs.</span></span> <span data-ttu-id="a4286-147">Ad esempio, durante il ridimensionamento del cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-147">For example, when scaling up the cluster.</span></span>

    <span data-ttu-id="a4286-148">Uno script persistente potrebbe anche applicare modifiche apportate a un altro tipo di nodo, ad esempio un nodo head.</span><span class="sxs-lookup"><span data-stu-id="a4286-148">A persisted script might also apply changes to another node type, such as a head node.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="a4286-149">Le azioni script persistenti devono avere un nome univoco.</span><span class="sxs-lookup"><span data-stu-id="a4286-149">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="a4286-150">Gli script **ad hoc** non sono persistenti.</span><span class="sxs-lookup"><span data-stu-id="a4286-150">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="a4286-151">Non vengono infatti applicati ai nodi del ruolo di lavoro aggiunti al cluster dopo l'esecuzione dello script.</span><span class="sxs-lookup"><span data-stu-id="a4286-151">They are not applied to worker nodes added to the cluster after the script has ran.</span></span> <span data-ttu-id="a4286-152">È possibile alzare di livello uno script ad hoc in un secondo momento per renderlo persistente o abbassare di livello uno script persistente per renderlo ad hoc.</span><span class="sxs-lookup"><span data-stu-id="a4286-152">You can subsequently promote an ad hoc script to a persisted script, or demote a persisted script to an ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="a4286-153">Le azioni script usate durante la creazione di un cluster vengono automaticamente rese persistenti.</span><span class="sxs-lookup"><span data-stu-id="a4286-153">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="a4286-154">Gli script che hanno esito negativo non vengono resi persistenti, anche in presenza di indicazioni specifiche in tal senso.</span><span class="sxs-lookup"><span data-stu-id="a4286-154">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="a4286-155">Possono accettare **parametri** usati dallo script durante l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a4286-155">Can accept **parameters** that are used by the script during execution.</span></span>
* <span data-ttu-id="a4286-156">Eseguire lo script con **privilegi a livello radice** nei nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-156">Run with **root level privileges** on the cluster nodes.</span></span>
* <span data-ttu-id="a4286-157">Possono essere usate con il **portale di Azure**, **Azure PowerShell**, l'**interfaccia della riga di comando di Azure** o **HDInsight .NET SDK**.</span><span class="sxs-lookup"><span data-stu-id="a4286-157">Can be used through the **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="a4286-158">Il cluster mantiene una cronologia di tutti gli script eseguiti.</span><span class="sxs-lookup"><span data-stu-id="a4286-158">The cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="a4286-159">La cronologia è utile quando è necessario trovare l'ID di uno script per le operazioni di innalzamento o abbassamento di livello.</span><span class="sxs-lookup"><span data-stu-id="a4286-159">The history is useful when you need to find the ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4286-160">Non esiste un metodo automatico per annullare le modifiche apportate da un'azione script.</span><span class="sxs-lookup"><span data-stu-id="a4286-160">There is no automatic way to undo the changes made by a script action.</span></span> <span data-ttu-id="a4286-161">Annullare manualmente le modifiche o fornire uno script che le inverta.</span><span class="sxs-lookup"><span data-stu-id="a4286-161">Either manually reverse the changes or provide a script that reverses them.</span></span>


### <a name="script-action-in-the-cluster-creation-process"></a><span data-ttu-id="a4286-162">Azione di script nel processo di creazione di cluster</span><span class="sxs-lookup"><span data-stu-id="a4286-162">Script Action in the cluster creation process</span></span>

<span data-ttu-id="a4286-163">Le azioni script usate durante la creazione del cluster sono leggermente diverse da quelle eseguite in un cluster esistente:</span><span class="sxs-lookup"><span data-stu-id="a4286-163">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="a4286-164">Lo script viene **salvato automaticamente in modo permanente**.</span><span class="sxs-lookup"><span data-stu-id="a4286-164">The script is **automatically persisted**.</span></span>
* <span data-ttu-id="a4286-165">Un **errore** nello script può causare l'esito negativo del processo di creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-165">A **failure** in the script can cause the cluster creation process to fail.</span></span>

<span data-ttu-id="a4286-166">Il diagramma seguente illustra quando l'opzione Azione di script viene eseguita durante il processo di creazione:</span><span class="sxs-lookup"><span data-stu-id="a4286-166">The following diagram illustrates when Script Action is executed during the creation process:</span></span>

<span data-ttu-id="a4286-167">![Personalizzazione di cluster HDInsight e fasi durante la creazione di un cluster][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="a4286-167">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="a4286-168">Lo script viene eseguito durante la configurazione di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4286-168">The script runs while HDInsight is being configured.</span></span> <span data-ttu-id="a4286-169">In questa fase, lo script viene eseguito in parallelo in tutti i nodi specificati nel cluster e con privilegi a livello radice sui nodi.</span><span class="sxs-lookup"><span data-stu-id="a4286-169">At this stage, the script runs in parallel on all the specified nodes in the cluster, and runs with root privileges on the nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="a4286-170">Dato che lo script viene eseguito con privilegi a livello radice nei nodi del cluster, è possibile eseguire operazioni quali l'arresto e l'avvio dei servizi, inclusi quelli correlati ad Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a4286-170">Because the script runs with root level privilege on the cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="a4286-171">Se si arrestano i servizi, è necessario assicurarsi che i servizi di Ambari e altri servizi correlati ad Hadoop siano attivi prima che termini l'esecuzione dello script.</span><span class="sxs-lookup"><span data-stu-id="a4286-171">If you stop services, you must ensure that the Ambari service and other Hadoop-related services are up and running before the script finishes running.</span></span> <span data-ttu-id="a4286-172">Questi servizi sono necessari per determinare correttamente l'integrità e lo stato del cluster durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="a4286-172">These services are required to successfully determine the health and state of the cluster while it is being created.</span></span>


<span data-ttu-id="a4286-173">Durante la creazione del cluster, è possibile usare più azioni di script alla volta.</span><span class="sxs-lookup"><span data-stu-id="a4286-173">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="a4286-174">Questi script vengono richiamati nell'ordine in cui sono stati specificati.</span><span class="sxs-lookup"><span data-stu-id="a4286-174">These scripts are invoked in the order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4286-175">Le azioni di script devono essere completate entro 60 minuti; in caso contrario si verifica un timeout.</span><span class="sxs-lookup"><span data-stu-id="a4286-175">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="a4286-176">Durante il provisioning dei cluster, lo script viene eseguito contemporaneamente ad altri processi di installazione e configurazione.</span><span class="sxs-lookup"><span data-stu-id="a4286-176">During cluster provisioning, the script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="a4286-177">In caso di concorrenza per risorse come il tempo di CPU o la larghezza di banda di rete, lo script può richiedere più tempo per completare l'operazione rispetto al tempo che impiegherebbe in un ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="a4286-177">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>
>
> <span data-ttu-id="a4286-178">Per ridurre al minimo il tempo necessario per eseguire lo script, evitare attività come il download e la compilazione di applicazioni dall'origine.</span><span class="sxs-lookup"><span data-stu-id="a4286-178">To minimize the time it takes to run the script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="a4286-179">Precompilare le applicazioni e archiviare il file binario in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4286-179">Pre-compile applications and store the binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="a4286-180">Azione script in un cluster in esecuzione</span><span class="sxs-lookup"><span data-stu-id="a4286-180">Script action on a running cluster</span></span>

<span data-ttu-id="a4286-181">A differenza delle azioni script usate durante la creazione di un cluster, un errore in uno script eseguito in un cluster già in esecuzione non determina automaticamente uno stato di errore del cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-181">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause the cluster to change to a failed state.</span></span> <span data-ttu-id="a4286-182">Al termine di uno script, il cluster deve restituire uno stato In esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a4286-182">Once a script completes, the cluster should return to a "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4286-183">Anche se lo stato del cluster è "in esecuzione", lo script non riuscito potrebbe includere attività interrotte.</span><span class="sxs-lookup"><span data-stu-id="a4286-183">Even if the cluster has a 'running' state, the failed script may have broken things.</span></span> <span data-ttu-id="a4286-184">Ad esempio, uno script potrebbe eliminare file richiesti dal cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-184">For example, a script could delete files needed by the cluster.</span></span>
>
> <span data-ttu-id="a4286-185">Le azioni script vengono eseguite con privilegi a livello radice. Occorre quindi conoscere il comportamento di uno script prima di applicarlo al cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-185">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it to your cluster.</span></span>

<span data-ttu-id="a4286-186">Quando si applica uno script a un cluster, lo stato del cluster passa da **In esecuzione** ad **Accettato**, quindi a **Configurazione di HDInsight** e infine di nuovo a **In esecuzione** per gli script con esito positivo.</span><span class="sxs-lookup"><span data-stu-id="a4286-186">When applying a script to a cluster, the cluster state changes to from **Running** to **Accepted**, then **HDInsight configuration**, and finally back to **Running** for successful scripts.</span></span> <span data-ttu-id="a4286-187">Lo stato dello script viene registrato nella cronologia dell'azione script, che può essere usata per determinare l'esito positivo o negativo dello script.</span><span class="sxs-lookup"><span data-stu-id="a4286-187">The script status is logged in the script action history, and you can use this information to determine whether the script succeeded or failed.</span></span> <span data-ttu-id="a4286-188">Ad esempio, il cmdlet di PowerShell `Get-AzureRmHDInsightScriptActionHistory` può essere usato per visualizzare lo stato di uno script.</span><span class="sxs-lookup"><span data-stu-id="a4286-188">For example, the `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used to view the status of a script.</span></span> <span data-ttu-id="a4286-189">Verranno restituite informazioni simili al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="a4286-189">It returns information similar to the following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="a4286-190">Se è stata cambiata la password dell'utente del cluster (admin) dopo la creazione del cluster stesso, questo potrebbe causare l'esito negativo delle azioni script eseguite su questo cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-190">If you have changed the cluster user (admin) password after the cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="a4286-191">Nel caso in cui siano presenti azioni script persistenti che hanno come destinazione nodi del ruolo di lavoro diversi, questi script potrebbero avere esito negativo se si ridimensiona il cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-191">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale the cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="a4286-192">Script di Azione script di esempio</span><span class="sxs-lookup"><span data-stu-id="a4286-192">Example Script Action scripts</span></span>

<span data-ttu-id="a4286-193">Gli script di Azione script possono essere usati tramite le seguenti utilità:</span><span class="sxs-lookup"><span data-stu-id="a4286-193">Script Action scripts can be used through the following utilities:</span></span>

* <span data-ttu-id="a4286-194">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a4286-194">Azure portal</span></span>
* <span data-ttu-id="a4286-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4286-195">Azure PowerShell</span></span>
* <span data-ttu-id="a4286-196">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a4286-196">Azure CLI</span></span>
* <span data-ttu-id="a4286-197">HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="a4286-197">HDInsight .NET SDK</span></span>

<span data-ttu-id="a4286-198">HDInsight fornisce script di esempio per installare i componenti seguenti nei cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a4286-198">HDInsight provides scripts to install the following components on HDInsight clusters:</span></span>

| <span data-ttu-id="a4286-199">Nome</span><span class="sxs-lookup"><span data-stu-id="a4286-199">Name</span></span> | <span data-ttu-id="a4286-200">Script</span><span class="sxs-lookup"><span data-stu-id="a4286-200">Script</span></span> |
| --- | --- |
| <span data-ttu-id="a4286-201">**Aggiungere un account di archiviazione di Azure**</span><span class="sxs-lookup"><span data-stu-id="a4286-201">**Add an Azure Storage account**</span></span> |<span data-ttu-id="a4286-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. Vedere [Add additional storage to an HDInsight cluster](hdinsight-hadoop-add-storage.md) (Aggiungere altra memoria a un cluster HDInsight).</span><span class="sxs-lookup"><span data-stu-id="a4286-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage to an HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="a4286-203">**Installare Hue.**</span><span class="sxs-lookup"><span data-stu-id="a4286-203">**Install Hue**</span></span> |<span data-ttu-id="a4286-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. Vedere [Installare e usare Hue in cluster HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a4286-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="a4286-205">**Installare Presto**</span><span class="sxs-lookup"><span data-stu-id="a4286-205">**Install Presto**</span></span> |<span data-ttu-id="a4286-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. Vedere [Installare e usare Presto nei cluster HDInsight Hadoop](hdinsight-hadoop-install-presto.md).</span><span class="sxs-lookup"><span data-stu-id="a4286-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="a4286-207">**Installare Solr**</span><span class="sxs-lookup"><span data-stu-id="a4286-207">**Install Solr**</span></span> |<span data-ttu-id="a4286-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. Vedere [Installare e usare Solr nei cluster Hadoop di HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a4286-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="a4286-209">**Installare Giraph**</span><span class="sxs-lookup"><span data-stu-id="a4286-209">**Install Giraph**</span></span> |<span data-ttu-id="a4286-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Vedere [Installare Giraph nei cluster HDInsight Hadoop](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a4286-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="a4286-211">**Precaricare le librerie Hive**</span><span class="sxs-lookup"><span data-stu-id="a4286-211">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="a4286-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. Vedere l'articolo relativo all' [aggiunta di librerie Hive in cluster HDInsight](hdinsight-hadoop-add-hive-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="a4286-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="a4286-213">**Installare o aggiornare Mono**</span><span class="sxs-lookup"><span data-stu-id="a4286-213">**Install or update Mono**</span></span> | <span data-ttu-id="a4286-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span><span class="sxs-lookup"><span data-stu-id="a4286-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="a4286-215">Vedere [Installare o aggiornare Mono in HDInsight](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="a4286-215">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="a4286-216">Usare un'azione script durante la creazione di un cluster</span><span class="sxs-lookup"><span data-stu-id="a4286-216">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="a4286-217">In questa sezione vengono forniti esempi sulle diverse modalità di utilizzo delle azioni script durante la creazione di un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4286-217">This section provides examples on the different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-the-azure-portal"></a><span data-ttu-id="a4286-218">Usare un'azione script durante la creazione di un cluster dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a4286-218">Use a Script Action during cluster creation from the Azure portal</span></span>

1. <span data-ttu-id="a4286-219">Avviare la creazione di un cluster come descritto in [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="a4286-219">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="a4286-220">Fermarsi quando si raggiunge la sezione __Riepilogo del cluster__.</span><span class="sxs-lookup"><span data-stu-id="a4286-220">Stop when you reach the __Cluster summary__ section.</span></span>

2. <span data-ttu-id="a4286-221">Nella sezione __Riepilogo del cluster__ selezionare il collegamento __Modifica__ per __Impostazioni avanzate__.</span><span class="sxs-lookup"><span data-stu-id="a4286-221">From the __Cluster summary__ section, select the __edit__ link for __Advanced settings__.</span></span>

    ![Collegamento impostazioni avanzate](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="a4286-223">Nella sezione __Impostazioni avanzate__ selezionare __Azioni script__.</span><span class="sxs-lookup"><span data-stu-id="a4286-223">From the __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="a4286-224">Nella sezione __Azioni script__ selezionare __+ Invia nuova__</span><span class="sxs-lookup"><span data-stu-id="a4286-224">From the __Script actions__ section, select __+ Submit new__</span></span>

    ![Inviare una nuova azione script](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="a4286-226">Usare la voce __Seleziona uno script__ per selezionare uno script pronto.</span><span class="sxs-lookup"><span data-stu-id="a4286-226">Use the __Select a script__ entry to select a pre-made script.</span></span> <span data-ttu-id="a4286-227">Per usare uno script personalizzato, selezionare __Personalizzato__ e indicare __Nome__ e __URI script Bash__ per lo script.</span><span class="sxs-lookup"><span data-stu-id="a4286-227">To use a custom script, select __Custom__ and then provide the __Name__ and __Bash script URI__ for your script.</span></span>

    ![Aggiungere uno script nel modulo di selezione script](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="a4286-229">Nella tabella seguente vengono illustrati gli elementi nel modulo:</span><span class="sxs-lookup"><span data-stu-id="a4286-229">The following table describes the elements on the form:</span></span>

    | <span data-ttu-id="a4286-230">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a4286-230">Property</span></span> | <span data-ttu-id="a4286-231">Valore</span><span class="sxs-lookup"><span data-stu-id="a4286-231">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="a4286-232">Selezionare uno script</span><span class="sxs-lookup"><span data-stu-id="a4286-232">Select a script</span></span> | <span data-ttu-id="a4286-233">Per usare uno script personalizzato, selezionare __Personalizzato__.</span><span class="sxs-lookup"><span data-stu-id="a4286-233">To use your own script, select __Custom__.</span></span> <span data-ttu-id="a4286-234">In caso contrario, selezionare uno degli script disponibili.</span><span class="sxs-lookup"><span data-stu-id="a4286-234">Otherwise, select one of the provided scripts.</span></span> |
    | <span data-ttu-id="a4286-235">Nome</span><span class="sxs-lookup"><span data-stu-id="a4286-235">Name</span></span> |<span data-ttu-id="a4286-236">Specificare un nome per l'azione script.</span><span class="sxs-lookup"><span data-stu-id="a4286-236">Specify a name for the script action.</span></span> |
    | <span data-ttu-id="a4286-237">URI script Bash</span><span class="sxs-lookup"><span data-stu-id="a4286-237">Bash script URI</span></span> |<span data-ttu-id="a4286-238">Specificare l'URI dello script da richiamare per personalizzare il cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-238">Specify the URI to the script that is invoked to customize the cluster.</span></span> |
    | <span data-ttu-id="a4286-239">Head/Worker/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="a4286-239">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="a4286-240">Specificare i nodi **head**, **ruolo di lavoro** o **Zookeeper** in cui viene eseguito lo script di personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="a4286-240">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the customization script is run.</span></span> |
    | <span data-ttu-id="a4286-241">Parametri</span><span class="sxs-lookup"><span data-stu-id="a4286-241">Parameters</span></span> |<span data-ttu-id="a4286-242">Specificare i parametri, se richiesti dallo script.</span><span class="sxs-lookup"><span data-stu-id="a4286-242">Specify the parameters, if required by the script.</span></span> |

    <span data-ttu-id="a4286-243">Usare la voce __Salvare questa azione script in modo permanente__ per assicurarsi che lo script venga applicato durante le operazioni di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="a4286-243">Use the __Persist this script action__ entry to ensure that the script is applied during scaling operations.</span></span>

5. <span data-ttu-id="a4286-244">Selezionare __Crea__ per salvare lo script.</span><span class="sxs-lookup"><span data-stu-id="a4286-244">Select __Create__ to save the script.</span></span> <span data-ttu-id="a4286-245">È quindi possibile usare __+ Invia nuovo__ per aggiungere un altro script.</span><span class="sxs-lookup"><span data-stu-id="a4286-245">You can then use __+ Submit new__ to add another script.</span></span>

    ![Azioni script multiple](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="a4286-247">Dopo aver completato l'aggiunta degli script, usare il pulsante __Seleziona__ e quindi il pulsante __Avanti__ per tornare alla sezione __Riepilogo del cluster__.</span><span class="sxs-lookup"><span data-stu-id="a4286-247">When you are done adding scripts, use the __Select__ button, and then the __Next__ button to return to the __Cluster summary__ section.</span></span>

3. <span data-ttu-id="a4286-248">Per creare il cluster, selezionare __Crea__ nella sezione __Riepilogo del cluster__.</span><span class="sxs-lookup"><span data-stu-id="a4286-248">To create the cluster, select __Create__ from the __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="a4286-249">Usare Azione di script dai modelli di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="a4286-249">Use a Script Action from Azure Resource Manager templates</span></span>

<span data-ttu-id="a4286-250">Gli esempi in questa sezione mostrano come usare azioni script con modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a4286-250">The examples in this section demonstrate how to use script actions with Azure Resource Manager templates.</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="a4286-251">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="a4286-251">Before you begin</span></span>

* <span data-ttu-id="a4286-252">Per informazioni sulla configurazione di una workstation per l'esecuzione dei cmdlet PowerShell per HDInsight, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a4286-252">For information about configuring a workstation to run HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="a4286-253">Per istruzioni su come creare modelli, vedere [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a4286-253">For instructions on how to create templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="a4286-254">Se Azure PowerShell non è stato usato in precedenza con Gestione risorse, vedere [Uso di Azure PowerShell con Gestione risorse di Azure](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a4286-254">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="a4286-255">Creare cluster usando l'azione script</span><span class="sxs-lookup"><span data-stu-id="a4286-255">Create clusters using Script Action</span></span>

1. <span data-ttu-id="a4286-256">Copiare il modello seguente in un percorso di questo computer.</span><span class="sxs-lookup"><span data-stu-id="a4286-256">Copy the following template to a location on your computer.</span></span> <span data-ttu-id="a4286-257">Questo modello installa Giraph nei nodi head e nei nodi del ruolo di lavoro del cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-257">This template installs Giraph on the headnodes and worker nodes in the cluster.</span></span> <span data-ttu-id="a4286-258">È anche possibile verificare se il modello JSON è valido.</span><span class="sxs-lookup"><span data-stu-id="a4286-258">You can also verify if the JSON template is valid.</span></span> <span data-ttu-id="a4286-259">Incollare il contenuto del modello in [JSONLint](http://jsonlint.com/), uno strumento di convalida JSON disponibile online.</span><span class="sxs-lookup"><span data-stu-id="a4286-259">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. <span data-ttu-id="a4286-260">Avviare Azure PowerShell e accedere al proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="a4286-260">Start Azure PowerShell and Log in to your Azure account.</span></span> <span data-ttu-id="a4286-261">Una volta specificate le credenziali, il comando restituisce le informazioni relative all'account.</span><span class="sxs-lookup"><span data-stu-id="a4286-261">After providing your credentials, the command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="a4286-262">Se si hanno più sottoscrizioni, specificare l'ID sottoscrizione da usare per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a4286-262">If you have multiple subscriptions, provide the subscription ID you wish to use for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="a4286-263">È possibile usare `Get-AzureRmSubscription` per ottenere un elenco di tutte le sottoscrizioni associate all'account, con il rispettivo ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a4286-263">You can use `Get-AzureRmSubscription` to get a list of all subscriptions associated with your account, which includes the subscription ID for each one.</span></span>

4. <span data-ttu-id="a4286-264">Se non è già disponibile un gruppo di risorse, crearne uno.</span><span class="sxs-lookup"><span data-stu-id="a4286-264">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="a4286-265">Specificare il nome del gruppo di risorse e il percorso per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="a4286-265">Provide the name of the resource group and location that you need for your solution.</span></span> <span data-ttu-id="a4286-266">Viene restituito un riepilogo del nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a4286-266">A summary of the new resource group is returned.</span></span>

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. <span data-ttu-id="a4286-267">Per creare una distribuzione per il gruppo di risorse, eseguire il comando **New-AzureResourceGroupDeployment** e specificare i parametri necessari.</span><span class="sxs-lookup"><span data-stu-id="a4286-267">To create a deployment for your resource group, run the **New-AzureRmResourceGroupDeployment** command and provide the necessary parameters.</span></span> <span data-ttu-id="a4286-268">I parametri includono i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4286-268">The parameters include the following data:</span></span>

    * <span data-ttu-id="a4286-269">Nome per la distribuzione</span><span class="sxs-lookup"><span data-stu-id="a4286-269">A name for your deployment</span></span>
    * <span data-ttu-id="a4286-270">Nome del gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="a4286-270">The name of your resource group</span></span>
    * <span data-ttu-id="a4286-271">Percorso o URL del modello creato.</span><span class="sxs-lookup"><span data-stu-id="a4286-271">The path or URL to the template you created.</span></span>

  <span data-ttu-id="a4286-272">Passare anche gli eventuali altri parametri richiesti dal modello.</span><span class="sxs-lookup"><span data-stu-id="a4286-272">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="a4286-273">In questo caso, l'azione di script per installare R nel cluster non richiede parametri.</span><span class="sxs-lookup"><span data-stu-id="a4286-273">In this case, the script action to install R on the cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="a4286-274">Viene richiesto di fornire valori per i parametri definiti nel modello.</span><span class="sxs-lookup"><span data-stu-id="a4286-274">You are prompted to provide values for the parameters defined in the template.</span></span>

1. <span data-ttu-id="a4286-275">Quando il gruppo di risorse è stato distribuito, verrà visualizzato un riepilogo della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a4286-275">When the resource group has been deployed, a summary of the deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="a4286-276">Se la distribuzione non riesce, è possibile usare i cmdlet seguenti per ottenere informazioni relative agli errori.</span><span class="sxs-lookup"><span data-stu-id="a4286-276">If your deployment fails, you can use the following cmdlets to get information about the failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="a4286-277">Usare un'azione script durante la creazione di un cluster da Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4286-277">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="a4286-278">In questa sezione si userà il cmdlet [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) per richiamare script usando l'azione di script per personalizzare un cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-278">In this section, we use the [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet to invoke scripts by using Script Action to customize a cluster.</span></span> <span data-ttu-id="a4286-279">Prima di procedere, assicurarsi di aver installato e configurato Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4286-279">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="a4286-280">Per informazioni sulla configurazione di una workstation per l'esecuzione di cmdlet PowerShell per HDInsight, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a4286-280">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="a4286-281">Lo script seguente mostra come applicare un'azione script durante la creazione di un cluster con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a4286-281">The following script demonstrates how to apply a script action when creating a cluster using PowerShell:</span></span>

<span data-ttu-id="a4286-282">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]</span><span class="sxs-lookup"><span data-stu-id="a4286-282">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]</span></span>

<span data-ttu-id="a4286-283">La creazione del cluster può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="a4286-283">It can take several minutes before the cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-the-hdinsight-net-sdk"></a><span data-ttu-id="a4286-284">Usare un'azione script durante la creazione di un cluster da HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="a4286-284">Use a Script Action during cluster creation from the HDInsight .NET SDK</span></span>

<span data-ttu-id="a4286-285">HDInsight .NET SDK fornisce librerie client che semplificano l'uso di HDInsight da un'applicazione .NET.</span><span class="sxs-lookup"><span data-stu-id="a4286-285">The HDInsight .NET SDK provides client libraries that makes it easier to work with HDInsight from a .NET application.</span></span> <span data-ttu-id="a4286-286">Per un esempio di codice, vedere [Creare cluster basati su Linux in HDInsight tramite .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="a4286-286">For a code sample, see [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-to-a-running-cluster"></a><span data-ttu-id="a4286-287">Applicare un'azione script a un cluster in esecuzione</span><span class="sxs-lookup"><span data-stu-id="a4286-287">Apply a Script Action to a running cluster</span></span>

<span data-ttu-id="a4286-288">Questa sezione offre informazioni su come applicare azioni script a un cluster in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a4286-288">In this section, learn how to apply script actions to a running cluster.</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-portal"></a><span data-ttu-id="a4286-289">Applicare un'azione script a un cluster in esecuzione dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a4286-289">Apply a Script Action to a running cluster from the Azure portal</span></span>

1. <span data-ttu-id="a4286-290">Nel [portale di Azure](https://portal.azure.com)selezionare il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4286-290">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="a4286-291">Nella panoramica del cluster HDInsight selezionare il riquadro **Azioni script**.</span><span class="sxs-lookup"><span data-stu-id="a4286-291">From the HDInsight cluster overview, select the **Script Actions** tile.</span></span>

    ![Riquadro Azioni script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="a4286-293">È anche possibile selezionare **Tutte le impostazioni** e quindi **Azioni script** dalla sezione Impostazioni.</span><span class="sxs-lookup"><span data-stu-id="a4286-293">You can also select **All settings** and then select **Script Actions** from the Settings section.</span></span>

3. <span data-ttu-id="a4286-294">Nella parte superiore della sezione Azioni script selezionare **Invia nuova**.</span><span class="sxs-lookup"><span data-stu-id="a4286-294">From the top of the Script Actions section, select **Submit new**.</span></span>

    ![Aggiungere uno script a un cluster in esecuzione](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="a4286-296">Usare la voce __Seleziona uno script__ per selezionare uno script pronto.</span><span class="sxs-lookup"><span data-stu-id="a4286-296">Use the __Select a script__ entry to select a pre-made script.</span></span> <span data-ttu-id="a4286-297">Per usare uno script personalizzato, selezionare __Personalizzato__ e indicare __Nome__ e __URI script Bash__ per lo script.</span><span class="sxs-lookup"><span data-stu-id="a4286-297">To use a custom script, select __Custom__ and then provide the __Name__ and __Bash script URI__ for your script.</span></span>

    ![Aggiungere uno script nel modulo di selezione script](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="a4286-299">Nella tabella seguente vengono illustrati gli elementi nel modulo:</span><span class="sxs-lookup"><span data-stu-id="a4286-299">The following table describes the elements on the form:</span></span>

    | <span data-ttu-id="a4286-300">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a4286-300">Property</span></span> | <span data-ttu-id="a4286-301">Valore</span><span class="sxs-lookup"><span data-stu-id="a4286-301">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="a4286-302">Selezionare uno script</span><span class="sxs-lookup"><span data-stu-id="a4286-302">Select a script</span></span> | <span data-ttu-id="a4286-303">Per usare uno script personalizzato, selezionare __Personalizzato__.</span><span class="sxs-lookup"><span data-stu-id="a4286-303">To use your own script, select __custom__.</span></span> <span data-ttu-id="a4286-304">In caso contrario, selezionare uno degli script disponibili.</span><span class="sxs-lookup"><span data-stu-id="a4286-304">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="a4286-305">Nome</span><span class="sxs-lookup"><span data-stu-id="a4286-305">Name</span></span> |<span data-ttu-id="a4286-306">Specificare un nome per l'azione script.</span><span class="sxs-lookup"><span data-stu-id="a4286-306">Specify a name for the script action.</span></span> |
    | <span data-ttu-id="a4286-307">URI script Bash</span><span class="sxs-lookup"><span data-stu-id="a4286-307">Bash script URI</span></span> |<span data-ttu-id="a4286-308">Specificare l'URI dello script da richiamare per personalizzare il cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-308">Specify the URI to the script that is invoked to customize the cluster.</span></span> |
    | <span data-ttu-id="a4286-309">Head/Worker/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="a4286-309">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="a4286-310">Specificare i nodi **head**, **ruolo di lavoro** o **Zookeeper** in cui viene eseguito lo script di personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="a4286-310">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the customization script is run.</span></span> |
    | <span data-ttu-id="a4286-311">Parametri</span><span class="sxs-lookup"><span data-stu-id="a4286-311">Parameters</span></span> |<span data-ttu-id="a4286-312">Specificare i parametri, se richiesti dallo script.</span><span class="sxs-lookup"><span data-stu-id="a4286-312">Specify the parameters, if required by the script.</span></span> |

    <span data-ttu-id="a4286-313">Usare la voce __Salvare questa azione script in modo permanente__ per assicurarsi che lo script venga applicato durante le operazioni di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="a4286-313">Use the __Persist this script action__ entry to make sure the script is applied during scaling operations.</span></span>

5. <span data-ttu-id="a4286-314">Infine, usare il pulsante **Crea** per applicare lo script al cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-314">Finally, use the **Create** button to apply the script to the cluster.</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-azure-powershell"></a><span data-ttu-id="a4286-315">Applicare un'azione script a un cluster in esecuzione da Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4286-315">Apply a Script Action to a running cluster from Azure PowerShell</span></span>

<span data-ttu-id="a4286-316">Prima di procedere, assicurarsi di aver installato e configurato Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4286-316">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="a4286-317">Per informazioni sulla configurazione di una workstation per l'esecuzione di cmdlet PowerShell per HDInsight, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a4286-317">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="a4286-318">L'esempio seguente mostra come applicare un'azione script a un cluster in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="a4286-318">The following example demonstrates how to apply a script action to a running cluster:</span></span>

<span data-ttu-id="a4286-319">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]</span><span class="sxs-lookup"><span data-stu-id="a4286-319">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]</span></span>

<span data-ttu-id="a4286-320">Al termine dell'operazione, vengono visualizzate informazioni simili alle seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4286-320">Once the operation completes, you receive information similar to the following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-cli"></a><span data-ttu-id="a4286-321">Applicare un'azione script a un cluster in esecuzione dall'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a4286-321">Apply a Script Action to a running cluster from the Azure CLI</span></span>

<span data-ttu-id="a4286-322">Prima di procedere, assicurarsi di aver installato e configurato l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4286-322">Before proceeding, make sure you have installed and configured the Azure CLI.</span></span> <span data-ttu-id="a4286-323">Per altre informazioni, vedere [Installare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a4286-323">For more information, see [Install the Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="a4286-324">Per passare alla modalità Azure Resource Manager, usare il comando seguente nella riga di comando:</span><span class="sxs-lookup"><span data-stu-id="a4286-324">To switch to Azure Resource Manager mode, use the following command at the command line:</span></span>

        azure config mode arm

2. <span data-ttu-id="a4286-325">Usare il comando seguente per eseguire l'autenticazione nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4286-325">Use the following to authenticate to your Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="a4286-326">Usare il comando seguente per applicare un'azione script a un cluster in esecuzione</span><span class="sxs-lookup"><span data-stu-id="a4286-326">Use the following command to apply a script action to a running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="a4286-327">Se non vengono specificati alcuni parametri per il comando, verrà richiesto di specificarli.</span><span class="sxs-lookup"><span data-stu-id="a4286-327">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="a4286-328">Se lo script specificato con `-u` accetta parametri, è possibile specificarli usando il parametro `-p`.</span><span class="sxs-lookup"><span data-stu-id="a4286-328">If the script you specify with `-u` accepts parameters, you can specify them using the `-p` parameter.</span></span>

    <span data-ttu-id="a4286-329">I tipi di nodo validi sono `headnode`, `workernode`, e `zookeeper`.</span><span class="sxs-lookup"><span data-stu-id="a4286-329">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="a4286-330">Se lo script deve essere applicato a più tipi di nodo, specificare i tipi separati da ';'.</span><span class="sxs-lookup"><span data-stu-id="a4286-330">If the script should be applied to multiple node types, specify the types separated by a ';'.</span></span> <span data-ttu-id="a4286-331">Ad esempio: `-n headnode;workernode`.</span><span class="sxs-lookup"><span data-stu-id="a4286-331">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="a4286-332">Per salvare lo script in modo permanente, aggiungere `--persistOnSuccess`.</span><span class="sxs-lookup"><span data-stu-id="a4286-332">To persist the script, add the `--persistOnSuccess`.</span></span> <span data-ttu-id="a4286-333">È anche possibile salvare lo script in modo permanente in un secondo momento usando `azure hdinsight script-action persisted set`.</span><span class="sxs-lookup"><span data-stu-id="a4286-333">You can also persist the script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="a4286-334">Al termine del processo, viene visualizzato un output simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="a4286-334">Once the job completes, you receive output similar to the following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-to-a-running-cluster-using-rest-api"></a><span data-ttu-id="a4286-335">Applicare un'azione script a un cluster in esecuzione usando le API REST</span><span class="sxs-lookup"><span data-stu-id="a4286-335">Apply a Script Action to a running cluster using REST API</span></span>

<span data-ttu-id="a4286-336">Vedere l'articolo su come [eseguire azioni script in un cluster in esecuzione](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4286-336">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-the-hdinsight-net-sdk"></a><span data-ttu-id="a4286-337">Applicare un'azione script a un cluster in esecuzione da HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="a4286-337">Apply a Script Action to a running cluster from the HDInsight .NET SDK</span></span>

<span data-ttu-id="a4286-338">Per un esempio relativo all'uso di .NET SDK per applicare script a un cluster, vedere [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="a4286-338">For an example of using the .NET SDK to apply scripts to a cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="a4286-339">Visualizzare la cronologia, alzare e abbassare di livello le azioni script</span><span class="sxs-lookup"><span data-stu-id="a4286-339">View history, promote, and demote Script Actions</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="a4286-340">Uso del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a4286-340">Using the Azure portal</span></span>

1. <span data-ttu-id="a4286-341">Nel [portale di Azure](https://portal.azure.com)selezionare il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4286-341">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="a4286-342">Nella panoramica del cluster HDInsight selezionare il riquadro **Azioni script**.</span><span class="sxs-lookup"><span data-stu-id="a4286-342">From the HDInsight cluster overview, select the **Script Actions** tile.</span></span>

    ![Riquadro Azioni script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="a4286-344">È anche possibile selezionare **Tutte le impostazioni** e quindi **Azioni script** dalla sezione Impostazioni.</span><span class="sxs-lookup"><span data-stu-id="a4286-344">You can also select **All settings** and then select **Script Actions** from the Settings section.</span></span>

4. <span data-ttu-id="a4286-345">Una cronologia degli script per il cluster viene visualizzata nella sezione Azioni script.</span><span class="sxs-lookup"><span data-stu-id="a4286-345">A history of scripts for this cluster is displayed on the Script Actions section.</span></span> <span data-ttu-id="a4286-346">Queste informazioni includono un elenco degli script persistenti.</span><span class="sxs-lookup"><span data-stu-id="a4286-346">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="a4286-347">Nella schermata seguente si noterà che lo script Solr è stato eseguito nel cluster,</span><span class="sxs-lookup"><span data-stu-id="a4286-347">In the screenshot below, you can see that the Solr script has been ran on this cluster.</span></span> <span data-ttu-id="a4286-348">la schermata tuttavia non mostra script persistenti.</span><span class="sxs-lookup"><span data-stu-id="a4286-348">The screenshot does not show any persisted scripts.</span></span>

    ![Sezione Azioni script](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="a4286-350">Selezionando uno script nella cronologia, viene visualizzata la sezione Proprietà per lo script.</span><span class="sxs-lookup"><span data-stu-id="a4286-350">Selecting a script from the history displays the Properties section for this script.</span></span> <span data-ttu-id="a4286-351">Nella parte superiore della schermata è possibile eseguire di nuovo lo script o alzarlo di livello.</span><span class="sxs-lookup"><span data-stu-id="a4286-351">From the top of the screen, you can rerun the script or promote it.</span></span>

    ![Proprietà delle azioni script](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="a4286-353">È anche possibile usare i puntini di sospensione **...** a destra delle voci nella sezione Azioni script per eseguire alcune operazioni.</span><span class="sxs-lookup"><span data-stu-id="a4286-353">You can also use the **...** to the right of entries on the Script Actions section to perform actions.</span></span>

    ![Uso di ... nelle azioni script](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="a4286-355">Uso di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4286-355">Using Azure PowerShell</span></span>

| <span data-ttu-id="a4286-356">Usare</span><span class="sxs-lookup"><span data-stu-id="a4286-356">Use the following...</span></span> | <span data-ttu-id="a4286-357">Per</span><span class="sxs-lookup"><span data-stu-id="a4286-357">To ...</span></span> |
| --- | --- |
| <span data-ttu-id="a4286-358">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="a4286-358">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="a4286-359">Recuperare informazioni sulle azioni script persistenti</span><span class="sxs-lookup"><span data-stu-id="a4286-359">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="a4286-360">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="a4286-360">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="a4286-361">Recuperare una cronologia delle azioni script applicate al cluster o i dettagli di uno script specifico</span><span class="sxs-lookup"><span data-stu-id="a4286-361">Retrieve a history of script actions applied to the cluster, or details for a specific script</span></span> |
| <span data-ttu-id="a4286-362">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="a4286-362">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="a4286-363">Alzare di livello un'azione script ad hoc per renderla un'azione script persistente</span><span class="sxs-lookup"><span data-stu-id="a4286-363">Promotes an ad hoc script action to a persisted script action</span></span> |
| <span data-ttu-id="a4286-364">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="a4286-364">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="a4286-365">Abbassare di livello un'azione script persistente per renderla un'azione script ad hoc</span><span class="sxs-lookup"><span data-stu-id="a4286-365">Demotes a persisted script action to an ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="a4286-366">Usando `Remove-AzureRmHDInsightPersistedScriptAction` non vengono annullate le azioni eseguite da uno script.</span><span class="sxs-lookup"><span data-stu-id="a4286-366">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo the actions performed by a script.</span></span> <span data-ttu-id="a4286-367">Questo cmdlet rimuove solo il flag persistente.</span><span class="sxs-lookup"><span data-stu-id="a4286-367">This cmdlet only removes the persisted flag.</span></span>

<span data-ttu-id="a4286-368">Lo script di esempio seguente mostra come usare i cmdlet per alzare di livello e poi abbassare di livello uno script.</span><span class="sxs-lookup"><span data-stu-id="a4286-368">The following example script demonstrates using the cmdlets to promote, then demote a script.</span></span>

<span data-ttu-id="a4286-369">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]</span><span class="sxs-lookup"><span data-stu-id="a4286-369">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]</span></span>

### <a name="using-the-azure-cli"></a><span data-ttu-id="a4286-370">Uso dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a4286-370">Using the Azure CLI</span></span>

| <span data-ttu-id="a4286-371">Usare</span><span class="sxs-lookup"><span data-stu-id="a4286-371">Use the following...</span></span> | <span data-ttu-id="a4286-372">Per</span><span class="sxs-lookup"><span data-stu-id="a4286-372">To ...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="a4286-373">Recuperare un elenco di azioni script con salvataggio permanente</span><span class="sxs-lookup"><span data-stu-id="a4286-373">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="a4286-374">Recuperare informazioni su una specifica azione script con salvataggio permanente</span><span class="sxs-lookup"><span data-stu-id="a4286-374">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="a4286-375">Recuperare una cronologia delle azioni script applicate al cluster</span><span class="sxs-lookup"><span data-stu-id="a4286-375">Retrieve a history of script actions applied to the cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="a4286-376">Recuperare informazioni su un'azione script specifica</span><span class="sxs-lookup"><span data-stu-id="a4286-376">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="a4286-377">Alzare di livello un'azione script ad hoc per renderla un'azione script persistente</span><span class="sxs-lookup"><span data-stu-id="a4286-377">Promotes an ad hoc script action to a persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="a4286-378">Abbassare di livello un'azione script persistente per renderla un'azione script ad hoc</span><span class="sxs-lookup"><span data-stu-id="a4286-378">Demotes a persisted script action to an ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="a4286-379">Usando `azure hdinsight script-action persisted delete` non vengono annullate le azioni eseguite da uno script.</span><span class="sxs-lookup"><span data-stu-id="a4286-379">Using `azure hdinsight script-action persisted delete` does not undo the actions performed by a script.</span></span> <span data-ttu-id="a4286-380">Questo cmdlet rimuove solo il flag persistente.</span><span class="sxs-lookup"><span data-stu-id="a4286-380">This cmdlet only removes the persisted flag.</span></span>

### <a name="using-the-hdinsight-net-sdk"></a><span data-ttu-id="a4286-381">Uso di HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="a4286-381">Using the HDInsight .NET SDK</span></span>

<span data-ttu-id="a4286-382">Per un esempio relativo all'uso di .NET SDK per recuperare la cronologia degli script da un cluster e alzare o abbassare di livello gli script, vedere [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="a4286-382">For an example of using the .NET SDK to retrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="a4286-383">Questo esempio mostra anche come installare un'applicazione HDInsight mediante .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="a4286-383">This example also demonstrates how to install an HDInsight application using the .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="a4286-384">Supporto per software open source usato nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4286-384">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="a4286-385">Il servizio Microsoft Azure HDInsight usa un ecosistema di tecnologie open source ispirate ad Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a4286-385">The Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="a4286-386">Microsoft Azure offre un livello di supporto generale per le tecnologie open source.</span><span class="sxs-lookup"><span data-stu-id="a4286-386">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="a4286-387">Per altre informazioni, vedere la sezione **Ambito del supporto** nel [sito Web delle domande frequenti sul supporto tecnico di Azure](https://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="a4286-387">For more information, see the **Support Scope** section of the [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="a4286-388">Il servizio HDInsight offre un livello di supporto aggiuntivo per i componenti predefiniti.</span><span class="sxs-lookup"><span data-stu-id="a4286-388">The HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="a4286-389">Nel servizio HDInsight sono disponibili due tipi di componenti open source:</span><span class="sxs-lookup"><span data-stu-id="a4286-389">There are two types of open-source components that are available in the HDInsight service:</span></span>

* <span data-ttu-id="a4286-390">**Componenti predefiniti** - Questi componenti sono preinstallati nei cluster HDInsight e forniscono la funzionalità di base del cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-390">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span></span> <span data-ttu-id="a4286-391">Questa categoria include ad esempio il gestore risorse YARN, il linguaggio di query Hive (HiveQL) e la libreria Mahout.</span><span class="sxs-lookup"><span data-stu-id="a4286-391">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span></span> <span data-ttu-id="a4286-392">L'elenco completo dei componenti del cluster è disponibile in [Novità delle versioni cluster di Hadoop incluse in HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="a4286-392">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="a4286-393">**Componenti personalizzati** - Un utente del cluster può installare o usare nel carico di lavoro qualsiasi componente disponibile nella community o creato da lui stesso.</span><span class="sxs-lookup"><span data-stu-id="a4286-393">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="a4286-394">I componenti forniti con il cluster HDInsight sono completamente supportati.</span><span class="sxs-lookup"><span data-stu-id="a4286-394">Components provided with the HDInsight cluster are fully supported.</span></span> <span data-ttu-id="a4286-395">Il supporto tecnico Microsoft aiuta a isolare e risolvere i problemi legati a tali componenti.</span><span class="sxs-lookup"><span data-stu-id="a4286-395">Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="a4286-396">I componenti personalizzati ricevono supporto commercialmente ragionevole per semplificare la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="a4286-396">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="a4286-397">Il supporto tecnico Microsoft potrebbe essere in grado di risolvere il problema OPPURE richiedere di usare i canali disponibili per le tecnologie open source, in cui è possibile ottenere supporto estremamente competente per la tecnologia specifica.</span><span class="sxs-lookup"><span data-stu-id="a4286-397">Microsoft support may be able to resolve the issue OR they may ask you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="a4286-398">È ad esempio possibile ricorrere a molti siti di community, come il [forum MSDN per HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com). Anche per i progetti Apache sono disponibili siti specifici in [http://apache.org](http://apache.org), ad esempio [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="a4286-398">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="a4286-399">Il servizio HDInsight permette di usare i componenti personalizzati in molti modi.</span><span class="sxs-lookup"><span data-stu-id="a4286-399">The HDInsight service provides several ways to use custom components.</span></span> <span data-ttu-id="a4286-400">Indipendentemente dal modo in cui un componente viene usato o installato nel cluster, verrà applicato lo stesso livello di supporto.</span><span class="sxs-lookup"><span data-stu-id="a4286-400">The same level of support applies, regardless of how a component is used or installed on the cluster.</span></span> <span data-ttu-id="a4286-401">L'elenco seguente illustra i modi più comuni per usare i componenti personalizzati nei cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a4286-401">The following list describes the most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="a4286-402">Invio di processi - È possibile inviare al cluster processi Hadoop o di altro tipo che eseguono o usano componenti personalizzati.</span><span class="sxs-lookup"><span data-stu-id="a4286-402">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span></span>

2. <span data-ttu-id="a4286-403">Personalizzazione del cluster - Durante la creazione di un cluster, è possibile specificare impostazioni aggiuntive e componenti personalizzati, che verranno installati nei nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-403">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on the cluster nodes.</span></span>

3. <span data-ttu-id="a4286-404">Esempi - Microsoft e altri utenti possono fornire esempi relativi all'uso dei componenti personalizzati più diffusi nei cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4286-404">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span></span> <span data-ttu-id="a4286-405">Questi esempi vengono forniti senza supporto.</span><span class="sxs-lookup"><span data-stu-id="a4286-405">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a4286-406">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="a4286-406">Troubleshooting</span></span>

<span data-ttu-id="a4286-407">È possibile usare l'interfaccia utente Web Ambari per visualizzare le informazioni registrate dalle azioni script.</span><span class="sxs-lookup"><span data-stu-id="a4286-407">You can use Ambari web UI to view information logged by script actions.</span></span> <span data-ttu-id="a4286-408">Se lo script ha esito negativo durante la creazione del cluster, i log sono disponibili anche nell'account di archiviazione predefinito associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-408">If the script fails during cluster creation, the logs are also available in the default storage account associated with the cluster.</span></span> <span data-ttu-id="a4286-409">Questa sezione fornisce informazioni su come recuperare i registri usando entrambe le opzioni.</span><span class="sxs-lookup"><span data-stu-id="a4286-409">This section provides information on how to retrieve the logs using both these options.</span></span>

### <a name="using-the-ambari-web-ui"></a><span data-ttu-id="a4286-410">Utilizzo dell'interfaccia utente Web Ambari</span><span class="sxs-lookup"><span data-stu-id="a4286-410">Using the Ambari Web UI</span></span>

1. <span data-ttu-id="a4286-411">Nel browser passare a https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="a4286-411">In your browser, navigate to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="a4286-412">Sostituire CLUSTERNAME con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4286-412">Replace CLUSTERNAME with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="a4286-413">Quando richiesto, immettere il nome dell'account amministratore (admin) e la password per il cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-413">When prompted, enter the admin account name (admin) and password for the cluster.</span></span> <span data-ttu-id="a4286-414">Potrebbe essere necessario immettere di nuovo le credenziali di amministratore in un Web Form.</span><span class="sxs-lookup"><span data-stu-id="a4286-414">You may have to reenter the admin credentials in a web form.</span></span>

2. <span data-ttu-id="a4286-415">Nella barra nella parte superiore della pagina fare clic sulla voce **ops**.</span><span class="sxs-lookup"><span data-stu-id="a4286-415">From the bar at the top of the page, select the **ops** entry.</span></span> <span data-ttu-id="a4286-416">Verrà visualizzato un elenco delle operazioni correnti e precedenti eseguite nel cluster tramite Ambari.</span><span class="sxs-lookup"><span data-stu-id="a4286-416">A list of current and previous operations performed on the cluster through Ambari is displayed.</span></span>

    ![Barra nell'interfaccia utente di Ambari con selezionato ops](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="a4286-418">Trovare le voci con **run\_customscriptaction** nella colonna **Operations**.</span><span class="sxs-lookup"><span data-stu-id="a4286-418">Find the entries that have **run\_customscriptaction** in the **Operations** column.</span></span> <span data-ttu-id="a4286-419">Queste voci vengono create quando si eseguono le azioni script.</span><span class="sxs-lookup"><span data-stu-id="a4286-419">These entries are created when the Script Actions run.</span></span>

    ![Schermata delle operazioni](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="a4286-421">Selezionare la voce run\customscriptaction ed eseguire il drill-down dei collegamenti per visualizzare l'output di STDOUT e STDERR.</span><span class="sxs-lookup"><span data-stu-id="a4286-421">To view the STDOUT and STDERR output, select the run\customscriptaction entry and drill down through the links.</span></span> <span data-ttu-id="a4286-422">Questo output viene generato all'esecuzione dello script e può contenere informazioni utili.</span><span class="sxs-lookup"><span data-stu-id="a4286-422">This output is generated when the script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-the-default-storage-account"></a><span data-ttu-id="a4286-423">Accesso ai registri dall'account di archiviazione predefinito</span><span class="sxs-lookup"><span data-stu-id="a4286-423">Access logs from the default storage account</span></span>

<span data-ttu-id="a4286-424">Se la creazione del cluster non riesce a causa di un errore nell'azione script, i log sono accessibili dall'account di archiviazione cluster.</span><span class="sxs-lookup"><span data-stu-id="a4286-424">If the cluster creation fails due to a script action error, the logs can be accessed from the cluster storage account.</span></span>

* <span data-ttu-id="a4286-425">I registri di archiviazione sono disponibili in `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span><span class="sxs-lookup"><span data-stu-id="a4286-425">The storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![Schermata delle operazioni](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="a4286-427">In questa directory i registri sono organizzati per nodi head, nodi del ruolo di lavoro e nodi zookeeper.</span><span class="sxs-lookup"><span data-stu-id="a4286-427">Under this directory, the logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="a4286-428">Di seguito sono riportati alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="a4286-428">Some examples are:</span></span>

    * <span data-ttu-id="a4286-429">**Nodo head** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="a4286-429">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="a4286-430">**Nodo del ruolo di lavoro** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="a4286-430">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="a4286-431">**Nodo Zookeeper** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="a4286-431">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="a4286-432">Tutti i file stdout e stderr dell'host corrispondente vengono caricati nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a4286-432">All stdout and stderr of the corresponding host is uploaded to the storage account.</span></span> <span data-ttu-id="a4286-433">Per ogni azione script esiste un file **output-\*.txt** e un file **errors-\*.txt**.</span><span class="sxs-lookup"><span data-stu-id="a4286-433">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="a4286-434">Il file output-*.txt contiene informazioni relative all'URI dello script che è stato eseguito nell'host.</span><span class="sxs-lookup"><span data-stu-id="a4286-434">The output-*.txt file contains information about the URI of the script that got run on the host.</span></span> <span data-ttu-id="a4286-435">Ad esempio</span><span class="sxs-lookup"><span data-stu-id="a4286-435">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="a4286-436">È possibile creare più volte un cluster dell'azione di script con lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="a4286-436">It's possible that you repeatedly create a script action cluster with the same name.</span></span> <span data-ttu-id="a4286-437">In questo caso, è possibile distinguere i registri corrispondenti in base al nome della cartella della data.</span><span class="sxs-lookup"><span data-stu-id="a4286-437">In such case, you can distinguish the relevant logs based on the DATE folder name.</span></span> <span data-ttu-id="a4286-438">Ad esempio, la struttura di cartelle per un cluster (mycluster) creato in diverse date sarà simile alle seguenti voci di registro:</span><span class="sxs-lookup"><span data-stu-id="a4286-438">For example, the folder structure for a cluster (mycluster) created on different dates appears similar to the following log entries:</span></span>

    <span data-ttu-id="a4286-439">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="a4286-439">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="a4286-440">Se in uno stesso giorno si creano più cluster dell'azione di script con lo stesso nome, è possibile usare il prefisso univoco per identificare i file di registro corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="a4286-440">If you create a script action cluster with the same name on the same day, you can use the unique prefix to identify the relevant log files.</span></span>

* <span data-ttu-id="a4286-441">Se si crea un cluster verso le 00.00 (mezzanotte), è possibile che i file di log si estendano su due giorni.</span><span class="sxs-lookup"><span data-stu-id="a4286-441">If you create a cluster near 12:00AM (midnight), it's possible that the log files span across two days.</span></span> <span data-ttu-id="a4286-442">In questi casi, per lo stesso cluster vengono visualizzate due diverse cartelle della data.</span><span class="sxs-lookup"><span data-stu-id="a4286-442">In such cases, you see two different date folders for the same cluster.</span></span>

* <span data-ttu-id="a4286-443">Il caricamento dei file di registro nel contenitore predefinito può richiedere fino a 5 minuti, soprattutto per i cluster di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="a4286-443">Uploading log files to the default container can take up to 5 mins, especially for large clusters.</span></span> <span data-ttu-id="a4286-444">Se si desidera accedere ai file di registro, quindi, è opportuno non eliminare immediatamente il cluster in caso di esito negativo di un'azione di script.</span><span class="sxs-lookup"><span data-stu-id="a4286-444">So, if you want to access the logs, you should not immediately delete the cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="a4286-445">Watchdog Ambari</span><span class="sxs-lookup"><span data-stu-id="a4286-445">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="a4286-446">Non modificare la password del watchdog Ambari (hdinsightwatchdog) nel cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="a4286-446">Do not change the password for the Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="a4286-447">La modifica della password per questo account rende impossibile eseguire nuove azioni script nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4286-447">Changing the password for this account breaks the ability to run new script actions on the HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="a4286-448">Non è possibile importare il nome BlobService</span><span class="sxs-lookup"><span data-stu-id="a4286-448">Can't import name BlobService</span></span>

<span data-ttu-id="a4286-449">__Sintomi__: l'azione script non riesce.</span><span class="sxs-lookup"><span data-stu-id="a4286-449">__Symptoms__: The script action fails.</span></span> <span data-ttu-id="a4286-450">Quando si visualizza l'operazione in Ambari, viene restituito un errore simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a4286-450">Text similar to the following error is displayed when you view the operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="a4286-451">__Causa__: questo errore si verifica se si aggiorna il client di archiviazione di Azure Python incluso con il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4286-451">__Cause__: This error occurs if you upgrade the Python Azure Storage client that is included with the HDInsight cluster.</span></span> <span data-ttu-id="a4286-452">HDInsight prevede l'uso della versione 0.20.0 del client di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4286-452">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="a4286-453">__Risoluzione__: per risolvere questo problema, connettersi manualmente a ciascun nodo del cluster usando `ssh` e usare il comando seguente per reinstallare la versione corretta del client di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="a4286-453">__Resolution__: To resolve this error, manually connect to each cluster node using `ssh` and use the following command to reinstall the correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="a4286-454">Per informazioni sulla connessione al cluster tramite SSH, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a4286-454">For information on connecting to the cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="a4286-455">La cronologia non mostra gli script usati durante la creazione di un cluster</span><span class="sxs-lookup"><span data-stu-id="a4286-455">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="a4286-456">Se il cluster è stato creato prima del 15 marzo 2016, potrebbe non essere visualizzata una voce nella cronologia delle azioni script.</span><span class="sxs-lookup"><span data-stu-id="a4286-456">If your cluster was created before March 15, 2016, you may not see an entry in Script Action history.</span></span> <span data-ttu-id="a4286-457">Se il cluster è stato ridimensionato dopo il 15 marzo 2016, gli script usati durante la creazione del cluster verranno visualizzati nella cronologia man mano che vengono applicati a nuovi nodi nel cluster nell'ambito dell'operazione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="a4286-457">If you resize the cluster after March 15, 2016, the scripts using during cluster creation appear in history as they are applied to new nodes in the cluster as part of the resize operation.</span></span>

<span data-ttu-id="a4286-458">Sussistono due eccezioni:</span><span class="sxs-lookup"><span data-stu-id="a4286-458">There are two exceptions:</span></span>

* <span data-ttu-id="a4286-459">Se il cluster è stato creato prima del 1° settembre 2015.</span><span class="sxs-lookup"><span data-stu-id="a4286-459">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="a4286-460">Le azioni script sono state introdotte in questa data.</span><span class="sxs-lookup"><span data-stu-id="a4286-460">This date is when Script Actions were introduced.</span></span> <span data-ttu-id="a4286-461">Per i cluster creati prima di tale data non possono quindi essere state usate le azioni script.</span><span class="sxs-lookup"><span data-stu-id="a4286-461">Any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="a4286-462">Se sono state usate più azioni script durante la creazione del cluster ed è stato usato lo stesso nome per più script oppure lo stesso nome e lo stesso URI ma parametri diversi per più script.</span><span class="sxs-lookup"><span data-stu-id="a4286-462">If you used multiple Script Actions during cluster creation, and used the same name for multiple scripts, or the same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="a4286-463">In questi casi si riceve un errore simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a4286-463">In these cases, you receive the following error:</span></span>

    <span data-ttu-id="a4286-464">Non è possibile eseguire nuove azioni script nel cluster a causa di nomi di script in conflitto negli script esistenti.</span><span class="sxs-lookup"><span data-stu-id="a4286-464">No new script actions can be ran on this cluster due to conflicting script names in existing scripts.</span></span> <span data-ttu-id="a4286-465">I nomi di script forniti durante la creazione del cluster devono essere tutti univoci.</span><span class="sxs-lookup"><span data-stu-id="a4286-465">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="a4286-466">Gli script esistenti vengono eseguiti durante il ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="a4286-466">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4286-467">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4286-467">Next steps</span></span>

* [<span data-ttu-id="a4286-468">Sviluppare script di Azione script per HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4286-468">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="a4286-469">Installare e usare Solr nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4286-469">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="a4286-470">Installare e usare Giraph nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4286-470">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="a4286-471">[Add additional storage to an HDInsight cluster](hdinsight-hadoop-add-storage.md) (Aggiungere altra memoria a un cluster HDInsight)</span><span class="sxs-lookup"><span data-stu-id="a4286-471">[Add additional storage to an HDInsight cluster](hdinsight-hadoop-add-storage.md)</span></span>

<span data-ttu-id="a4286-472">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Fasi durante la creazione di un cluster"</span><span class="sxs-lookup"><span data-stu-id="a4286-472">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Stages during cluster creation"</span></span>
