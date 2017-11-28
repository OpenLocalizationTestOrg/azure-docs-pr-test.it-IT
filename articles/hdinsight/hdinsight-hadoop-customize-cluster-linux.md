---
title: cluster di HDInsight aaaCustomize usando le azioni script - Azure | Documenti Microsoft
description: "Aggiungere i componenti personalizzati che basati su tooLinux HDInsight cluster usando le azioni di Script. Le azioni script sono script Bash che è possibile configurazione del cluster utilizzati toocustomize hello o aggiungere altri servizi e le utilità come tonalità, Solr o R."
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
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="cbb0f-104">Personalizzare cluster HDInsight basati su Linux tramite Azione script</span><span class="sxs-lookup"><span data-stu-id="cbb0f-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="cbb0f-105">HDInsight fornisce un'opzione di configurazione denominata **genera Script azione** che richiama script personalizzati che consentono di personalizzare cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize hello cluster.</span></span> <span data-ttu-id="cbb0f-106">Questi script vengono utilizzati tooinstall i componenti aggiuntivi e modificare le impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-106">These scripts are used tooinstall additional components and change configuration settings.</span></span> <span data-ttu-id="cbb0f-107">Le azioni script possono essere utilizzate durante o dopo la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbb0f-108">azioni di Hello possibilità toouse script in un cluster già in esecuzione è disponibile solo per i cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-108">hello ability toouse script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="cbb0f-109">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cbb0f-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="cbb0f-111">Le azioni script possono anche essere pubblicata toohello Azure Marketplace come un'applicazione di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-111">Script actions can also be published toohello Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="cbb0f-112">Alcuni degli esempi di hello in questo documento Mostra come installare un'applicazione di HDInsight utilizzando i comandi di azione di script di PowerShell e hello .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-112">Some of hello examples in this document show how you can install an HDInsight application using script action commands from PowerShell and hello .NET SDK.</span></span> <span data-ttu-id="cbb0f-113">Per ulteriori informazioni sulle applicazioni di HDInsight, vedere [HDInsight pubblicare applicazioni in Azure Marketplace hello](hdinsight-apps-publish-applications.md).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-113">For more information on HDInsight applications, see [Publish HDInsight applications into hello Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="cbb0f-114">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="cbb0f-114">Permissions</span></span>

<span data-ttu-id="cbb0f-115">Se si utilizza un cluster di HDInsight appartenenti a un dominio, sono disponibili due Ambari le autorizzazioni necessarie quando si utilizzano le azioni script con cluster hello:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-115">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with hello cluster:</span></span>

* <span data-ttu-id="cbb0f-116">**AMBARI. ESEGUIRE\_personalizzato\_comando**: il ruolo di amministratore Ambari hello dispone dell'autorizzazione per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: hello Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="cbb0f-117">**CLUSTER. ESEGUIRE\_personalizzato\_comando**: entrambi hello amministrazione Cluster HDInsight e Ambari amministratore dispongono di questa autorizzazione per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both hello HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="cbb0f-118">Per altre informazioni sull'uso delle autorizzazioni con HDInsight aggiunto a un dominio, vedere [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Gestire cluster HDInsight aggiunti al dominio).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-118">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="cbb0f-119">Controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="cbb0f-119">Access control</span></span>

<span data-ttu-id="cbb0f-120">Se non si è amministratore hello/proprietario della sottoscrizione Azure, l'account deve disporre almeno **collaboratore** gruppo di risorse toohello di accesso che contiene il cluster di HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-120">If you are not hello administrator/owner of your Azure subscription, your account must have at least **Contributor** access toohello resource group that contains hello HDInsight cluster.</span></span>

<span data-ttu-id="cbb0f-121">Inoltre, se si sta creando un cluster HDInsight, un utente con almeno **collaboratore** toohello accesso sottoscrizione di Azure deve registrato in precedenza provider hello per HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-121">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access toohello Azure subscription must have previously registered hello provider for HDInsight.</span></span> <span data-ttu-id="cbb0f-122">Registrazione del provider si verifica quando un utente con sottoscrizione di collaboratore accesso toohello crea una risorsa per hello prima sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-122">Provider registration happens when a user with Contributor access toohello subscription creates a resource for hello first time on hello subscription.</span></span> <span data-ttu-id="cbb0f-123">Può essere eseguita anche senza creare una risorsa [registrando un provider tramite REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-123">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="cbb0f-124">Per ulteriori informazioni sull'utilizzo di gestione degli accessi, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-124">For more information on working with access management, see hello following documents:</span></span>

* [<span data-ttu-id="cbb0f-125">Introduzione alla gestione di accesso nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="cbb0f-125">Get started with access management in hello Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="cbb0f-126">Utilizzare le risorse di sottoscrizione di Azure tooyour accesso toomanage assegnazioni ruolo</span><span class="sxs-lookup"><span data-stu-id="cbb0f-126">Use role assignments toomanage access tooyour Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="cbb0f-127">Informazioni sulle azioni script</span><span class="sxs-lookup"><span data-stu-id="cbb0f-127">Understanding Script Actions</span></span>

<span data-ttu-id="cbb0f-128">Un'azione script è semplicemente uno script Bash a cui si forniscono parametri e un URI.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-128">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="cbb0f-129">script di Hello viene eseguito in nodi di cluster di HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-129">hello script runs on nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="cbb0f-130">di seguito Hello sono caratteristiche e funzionalità delle azioni di scripting.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-130">hello following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="cbb0f-131">Devono essere archiviati in un URI che sia accessibile dal cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-131">Must be stored on a URI that is accessible from hello HDInsight cluster.</span></span> <span data-ttu-id="cbb0f-132">di seguito Hello sono possibili percorsi di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-132">hello following are possible storage locations:</span></span>

    * <span data-ttu-id="cbb0f-133">Un **archivio Azure Data Lake** account che sia accessibile dal cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-133">An **Azure Data Lake Store** account that is accessible by hello HDInsight cluster.</span></span> <span data-ttu-id="cbb0f-134">Per informazioni sull'uso di Azure Data Lake Store con HDInsight, vedere [Creare un cluster HDInsight con Data Lake Store usando il portale](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-134">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="cbb0f-135">Quando si utilizza uno script archiviato nell'archivio Data Lake, il formato dell'URI hello è `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-135">When using a script stored in Data Lake Store, hello URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="cbb0f-136">Hello servizio principale HDInsight utilizza tooaccess archivio Data Lake deve avere accesso in lettura toohello script.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-136">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

    * <span data-ttu-id="cbb0f-137">Un blob in un **account di archiviazione Azure** che è uno di questi account di archiviazione primario o altre hello per il cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-137">A blob in an **Azure Storage account** that is either hello primary or additional storage account for hello HDInsight cluster.</span></span> <span data-ttu-id="cbb0f-138">HDInsight è concesso l'accesso tooboth di questi tipi di account di archiviazione durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-138">HDInsight is granted access tooboth of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="cbb0f-139">Un servizio di condivisione file pubblico, ad esempio BLOB di Azure, GitHub, OneDrive, Dropbox e così via.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-139">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="cbb0f-140">Ad esempio URI, vedere hello [script azione script di esempio](#example-script-action-scripts) sezione.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-140">For example URIs, see hello [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="cbb0f-141">HDInsight supporta solo account di archiviazione di Azure __per uso generico__.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-141">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="cbb0f-142">Non supporta attualmente hello __nell'archiviazione Blob__ tipo di account.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-142">It does not currently support hello __Blob storage__ account type.</span></span>

* <span data-ttu-id="cbb0f-143">Può essere limitata troppo**eseguiti solo alcuni tipi di nodi**, ad esempio head nodi o di lavoro.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-143">Can be restricted too**run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="cbb0f-144">Se utilizzato con HDInsight Premium, è possibile specificare che devono essere utilizzati script di hello sul nodo del bordo hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-144">When used with HDInsight Premium, you can specify that hello script should be used on hello edge node.</span></span>

* <span data-ttu-id="cbb0f-145">Possono essere **persistenti** o **ad hoc**.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-145">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="cbb0f-146">**Persistente** gli script sono cluster toohello aggiunta di nodi tooworker applicato dopo l'esecuzione di script hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-146">**Persisted** scripts are applied tooworker nodes added toohello cluster after hello script runs.</span></span> <span data-ttu-id="cbb0f-147">Ad esempio, la scalabilità del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-147">For example, when scaling up hello cluster.</span></span>

    <span data-ttu-id="cbb0f-148">Uno script persistente potrebbe anche applicare tipo di nodo tooanother modifiche, ad esempio un nodo head.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-148">A persisted script might also apply changes tooanother node type, such as a head node.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="cbb0f-149">Le azioni script persistenti devono avere un nome univoco.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-149">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="cbb0f-150">Gli script **ad hoc** non sono persistenti.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-150">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="cbb0f-151">Non sono cluster toohello aggiunta di nodi tooworker applicato dopo script hello è stato eseguito.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-151">They are not applied tooworker nodes added toohello cluster after hello script has ran.</span></span> <span data-ttu-id="cbb0f-152">Successivamente è possibile alzare di livello un tooa script ad hoc persistente script o abbassare di livello uno script di script con salvataggio permanente tooan ad hoc.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-152">You can subsequently promote an ad hoc script tooa persisted script, or demote a persisted script tooan ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="cbb0f-153">Le azioni script usate durante la creazione di un cluster vengono automaticamente rese persistenti.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-153">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="cbb0f-154">Gli script che hanno esito negativo non vengono resi persistenti, anche in presenza di indicazioni specifiche in tal senso.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-154">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="cbb0f-155">Può accettare **parametri** utilizzati dallo script hello durante l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-155">Can accept **parameters** that are used by hello script during execution.</span></span>
* <span data-ttu-id="cbb0f-156">Eseguire con **privilegi al livello radice** nei nodi del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-156">Run with **root level privileges** on hello cluster nodes.</span></span>
* <span data-ttu-id="cbb0f-157">Può essere utilizzato tramite hello **portale di Azure**, **Azure PowerShell**, **CLI di Azure**, o **HDInsight .NET SDK**</span><span class="sxs-lookup"><span data-stu-id="cbb0f-157">Can be used through hello **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="cbb0f-158">cluster Hello mantiene una cronologia di tutti gli script sono stati eseguiti.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-158">hello cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="cbb0f-159">cronologia Hello è utile quando è necessario toofind hello ID di uno script per le operazioni di innalzamento o abbassamento di livello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-159">hello history is useful when you need toofind hello ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbb0f-160">Non è tooundo alcun metodo automatico hello le modifiche apportate da un'azione di script.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-160">There is no automatic way tooundo hello changes made by a script action.</span></span> <span data-ttu-id="cbb0f-161">È possibile annullare manualmente le modifiche di hello oppure fornire uno script che li inverte.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-161">Either manually reverse hello changes or provide a script that reverses them.</span></span>


### <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="cbb0f-162">Genera script azione nel processo di creazione di cluster hello</span><span class="sxs-lookup"><span data-stu-id="cbb0f-162">Script Action in hello cluster creation process</span></span>

<span data-ttu-id="cbb0f-163">Le azioni script usate durante la creazione del cluster sono leggermente diverse da quelle eseguite in un cluster esistente:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-163">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="cbb0f-164">script Hello è **automaticamente persistente**.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-164">hello script is **automatically persisted**.</span></span>
* <span data-ttu-id="cbb0f-165">Oggetto **errore** in hello script può causare hello cluster creazione processo toofail.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-165">A **failure** in hello script can cause hello cluster creation process toofail.</span></span>

<span data-ttu-id="cbb0f-166">Hello diagramma seguente illustra quando viene eseguita l'azione di Script durante il processo di creazione di hello:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-166">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="cbb0f-167">![Personalizzazione di cluster HDInsight e fasi durante la creazione di un cluster][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="cbb0f-167">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="cbb0f-168">script di Hello viene eseguito quando viene configurato HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-168">hello script runs while HDInsight is being configured.</span></span> <span data-ttu-id="cbb0f-169">In questa fase, viene eseguito lo script hello in parallelo in tutte hello i nodi specificati nel cluster hello e viene eseguito con privilegi radice nodi hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-169">At this stage, hello script runs in parallel on all hello specified nodes in hello cluster, and runs with root privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="cbb0f-170">Poiché nei nodi del cluster hello, script di hello viene eseguito con privilegi di livello radice, è possibile eseguire operazioni come l'arresto e avvio di servizi, inclusi i servizi correlati a Hadoop.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-170">Because hello script runs with root level privilege on hello cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="cbb0f-171">Se si arresta i servizi, è necessario assicurarsi che il servizio di Ambari hello e altri servizi correlati a Hadoop siano in esecuzione prima di script hello al termine dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-171">If you stop services, you must ensure that hello Ambari service and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="cbb0f-172">Questi servizi sono necessari toosuccessfully determinare hello integrità e dello stato del cluster hello durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-172">These services are required toosuccessfully determine hello health and state of hello cluster while it is being created.</span></span>


<span data-ttu-id="cbb0f-173">Durante la creazione del cluster, è possibile usare più azioni di script alla volta.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-173">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="cbb0f-174">Questi script vengono richiamati nell'ordine di hello in cui sono stati specificati.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-174">These scripts are invoked in hello order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbb0f-175">Le azioni di script devono essere completate entro 60 minuti; in caso contrario si verifica un timeout.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-175">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="cbb0f-176">Durante il provisioning del cluster, script di hello viene eseguito contemporaneamente ad altri processi di installazione e configurazione.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-176">During cluster provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="cbb0f-177">Contesa per le risorse, ad esempio larghezza di banda della CPU ora o di rete potrebbe essere hello script tootake più toofinish rispetto a quello usato nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-177">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>
>
> <span data-ttu-id="cbb0f-178">hello toominimize tempo accetta toorun hello script, evitare di attività, ad esempio il download e la compilazione di applicazioni dall'origine.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-178">toominimize hello time it takes toorun hello script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="cbb0f-179">Precompilazione di applicazioni e archiviare file binario hello in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-179">Pre-compile applications and store hello binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="cbb0f-180">Azione script in un cluster in esecuzione</span><span class="sxs-lookup"><span data-stu-id="cbb0f-180">Script action on a running cluster</span></span>

<span data-ttu-id="cbb0f-181">A differenza degli script azioni utilizzate durante la creazione del cluster, un errore in uno script eseguite su un cluster già in esecuzione non determina automaticamente lo stato di hello cluster toochange tooa non riuscita.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-181">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause hello cluster toochange tooa failed state.</span></span> <span data-ttu-id="cbb0f-182">Al termine del processo di uno script, cluster hello deve restituire lo stato "running" tooa.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-182">Once a script completes, hello cluster should return tooa "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbb0f-183">Anche se il cluster hello presenta uno stato 'in esecuzione', hello script non riuscito potrebbe essere interrotto operazioni.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-183">Even if hello cluster has a 'running' state, hello failed script may have broken things.</span></span> <span data-ttu-id="cbb0f-184">Ad esempio, uno script è stato possibile eliminare i file necessari per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-184">For example, a script could delete files needed by hello cluster.</span></span>
>
> <span data-ttu-id="cbb0f-185">Le azioni di script eseguite con privilegi di radice, pertanto è necessario assicurarsi di comprendere cosa uno script prima di applicarla tooyour cluster.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-185">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it tooyour cluster.</span></span>

<span data-ttu-id="cbb0f-186">Quando l'applicazione di un cluster di tooa script, lo stato del cluster hello cambia toofrom **esecuzione** troppo**accettato**, quindi **HDInsight configurazione**e infine di nuovo troppo**Esecuzione** per gli script ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-186">When applying a script tooa cluster, hello cluster state changes toofrom **Running** too**Accepted**, then **HDInsight configuration**, and finally back too**Running** for successful scripts.</span></span> <span data-ttu-id="cbb0f-187">stato dello script Hello viene registrato nella cronologia dell'azione script hello ed è possibile utilizzare questo toodetermine informazioni script hello è riuscita o meno.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-187">hello script status is logged in hello script action history, and you can use this information toodetermine whether hello script succeeded or failed.</span></span> <span data-ttu-id="cbb0f-188">Ad esempio, hello `Get-AzureRmHDInsightScriptActionHistory` cmdlet di PowerShell può essere utilizzato tooview hello stato di uno script.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-188">For example, hello `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used tooview hello status of a script.</span></span> <span data-ttu-id="cbb0f-189">Restituisce toohello di informazioni simili seguente testo:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-189">It returns information similar toohello following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="cbb0f-190">Se è stata modificata la password utente (amministrazione) di hello cluster dopo la creazione del cluster hello, script azioni è state eseguite su questo cluster potrebbe non riuscire.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-190">If you have changed hello cluster user (admin) password after hello cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="cbb0f-191">Se si dispone di eventuali azioni script persistenti di nodi di lavoro di destinazione, questi script potrebbero non riuscire quando si aumenta il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-191">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale hello cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="cbb0f-192">Script di Azione script di esempio</span><span class="sxs-lookup"><span data-stu-id="cbb0f-192">Example Script Action scripts</span></span>

<span data-ttu-id="cbb0f-193">Script delle azioni di script può essere utilizzato tramite hello utilità seguenti:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-193">Script Action scripts can be used through hello following utilities:</span></span>

* <span data-ttu-id="cbb0f-194">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cbb0f-194">Azure portal</span></span>
* <span data-ttu-id="cbb0f-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbb0f-195">Azure PowerShell</span></span>
* <span data-ttu-id="cbb0f-196">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="cbb0f-196">Azure CLI</span></span>
* <span data-ttu-id="cbb0f-197">HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="cbb0f-197">HDInsight .NET SDK</span></span>

<span data-ttu-id="cbb0f-198">HDInsight fornisce hello tooinstall gli script seguenti componenti nei cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-198">HDInsight provides scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="cbb0f-199">Nome</span><span class="sxs-lookup"><span data-stu-id="cbb0f-199">Name</span></span> | <span data-ttu-id="cbb0f-200">Script</span><span class="sxs-lookup"><span data-stu-id="cbb0f-200">Script</span></span> |
| --- | --- |
| <span data-ttu-id="cbb0f-201">**Aggiungere un account di archiviazione di Azure**</span><span class="sxs-lookup"><span data-stu-id="cbb0f-201">**Add an Azure Storage account**</span></span> |<span data-ttu-id="cbb0f-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. Vedere [cluster HDInsight di aggiungere ulteriore spazio di archiviazione tooan](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage tooan HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="cbb0f-203">**Installare Hue.**</span><span class="sxs-lookup"><span data-stu-id="cbb0f-203">**Install Hue**</span></span> |<span data-ttu-id="cbb0f-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. Vedere [Installare e usare Hue in cluster HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="cbb0f-205">**Installare Presto**</span><span class="sxs-lookup"><span data-stu-id="cbb0f-205">**Install Presto**</span></span> |<span data-ttu-id="cbb0f-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. Vedere [Installare e usare Presto nei cluster HDInsight Hadoop](hdinsight-hadoop-install-presto.md).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="cbb0f-207">**Installare Solr**</span><span class="sxs-lookup"><span data-stu-id="cbb0f-207">**Install Solr**</span></span> |<span data-ttu-id="cbb0f-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. Vedere [Installare e usare Solr nei cluster Hadoop di HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="cbb0f-209">**Installare Giraph**</span><span class="sxs-lookup"><span data-stu-id="cbb0f-209">**Install Giraph**</span></span> |<span data-ttu-id="cbb0f-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Vedere [Installare Giraph nei cluster HDInsight Hadoop](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="cbb0f-211">**Precaricare le librerie Hive**</span><span class="sxs-lookup"><span data-stu-id="cbb0f-211">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="cbb0f-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. Vedere l'articolo relativo all' [aggiunta di librerie Hive in cluster HDInsight](hdinsight-hadoop-add-hive-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="cbb0f-213">**Installare o aggiornare Mono**</span><span class="sxs-lookup"><span data-stu-id="cbb0f-213">**Install or update Mono**</span></span> | <span data-ttu-id="cbb0f-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="cbb0f-215">Vedere [Installare o aggiornare Mono in HDInsight](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-215">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="cbb0f-216">Usare un'azione script durante la creazione di un cluster</span><span class="sxs-lookup"><span data-stu-id="cbb0f-216">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="cbb0f-217">In questa sezione vengono forniti esempi in modi diversi di hello che è possibile usare azioni script durante la creazione di un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-217">This section provides examples on hello different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a><span data-ttu-id="cbb0f-218">Utilizzare un'azione di Script durante la creazione del cluster da hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cbb0f-218">Use a Script Action during cluster creation from hello Azure portal</span></span>

1. <span data-ttu-id="cbb0f-219">Avviare la creazione di un cluster come descritto in [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-219">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="cbb0f-220">Fermarsi quando si raggiunge hello __riepilogo Cluster__ sezione.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-220">Stop when you reach hello __Cluster summary__ section.</span></span>

2. <span data-ttu-id="cbb0f-221">Da hello __riepilogo Cluster__ sezione, seleziona hello __modifica__ dei collegamenti per __impostazioni avanzate__.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-221">From hello __Cluster summary__ section, select hello __edit__ link for __Advanced settings__.</span></span>

    ![Collegamento impostazioni avanzate](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="cbb0f-223">Da hello __impostazioni avanzate__ selezionare __Script azioni__.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-223">From hello __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="cbb0f-224">Da hello __Script azioni__ selezionare __+ nuovo invio__</span><span class="sxs-lookup"><span data-stu-id="cbb0f-224">From hello __Script actions__ section, select __+ Submit new__</span></span>

    ![Inviare una nuova azione script](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="cbb0f-226">Hello utilizzare __selezionare uno script__ tooselect voce uno script di pre-effettuato.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-226">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="cbb0f-227">toouse uno script personalizzato, selezionare __personalizzato__ e quindi fornire hello __nome__ e __l'URI dello script Bash__ per lo script.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-227">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Aggiungere uno script nel modulo di script selezionare hello](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="cbb0f-229">Hello nella tabella seguente vengono descritti gli elementi di hello in form di hello:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-229">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="cbb0f-230">Proprietà</span><span class="sxs-lookup"><span data-stu-id="cbb0f-230">Property</span></span> | <span data-ttu-id="cbb0f-231">Valore</span><span class="sxs-lookup"><span data-stu-id="cbb0f-231">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="cbb0f-232">Selezionare uno script</span><span class="sxs-lookup"><span data-stu-id="cbb0f-232">Select a script</span></span> | <span data-ttu-id="cbb0f-233">toouse lo script, seleziona __personalizzato__.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-233">toouse your own script, select __Custom__.</span></span> <span data-ttu-id="cbb0f-234">In caso contrario, selezionare uno degli script hello fornito.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-234">Otherwise, select one of hello provided scripts.</span></span> |
    | <span data-ttu-id="cbb0f-235">Nome</span><span class="sxs-lookup"><span data-stu-id="cbb0f-235">Name</span></span> |<span data-ttu-id="cbb0f-236">Specificare un nome per l'azione script hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-236">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="cbb0f-237">URI script Bash</span><span class="sxs-lookup"><span data-stu-id="cbb0f-237">Bash script URI</span></span> |<span data-ttu-id="cbb0f-238">Specificare hello URI toohello script che è richiamato toocustomize hello cluster.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-238">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="cbb0f-239">Head/Worker/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="cbb0f-239">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="cbb0f-240">Specificare i nodi di hello (**Head**, **lavoro**, o **ZooKeeper**) in cui personalizzazione hello viene eseguito uno script.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-240">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="cbb0f-241">parameters</span><span class="sxs-lookup"><span data-stu-id="cbb0f-241">Parameters</span></span> |<span data-ttu-id="cbb0f-242">Specificare i parametri di hello, se richiesti dallo script hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-242">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="cbb0f-243">Hello utilizzare __mantenere questa azione script__ tooensure voce che hello script viene applicato durante le operazioni di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-243">Use hello __Persist this script action__ entry tooensure that hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="cbb0f-244">Selezionare __crea__ script hello toosave.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-244">Select __Create__ toosave hello script.</span></span> <span data-ttu-id="cbb0f-245">È quindi possibile utilizzare __+ invia di nuovo__ tooadd un altro script.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-245">You can then use __+ Submit new__ tooadd another script.</span></span>

    ![Azioni script multiple](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="cbb0f-247">Una volta aggiunta di script, utilizzare hello __selezionare__ pulsante e quindi hello __Avanti__ pulsante tooreturn toohello __riepilogo Cluster__ sezione.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-247">When you are done adding scripts, use hello __Select__ button, and then hello __Next__ button tooreturn toohello __Cluster summary__ section.</span></span>

3. <span data-ttu-id="cbb0f-248">cluster di hello toocreate, selezionare __crea__ da hello __riepilogo Cluster__ selezione.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-248">toocreate hello cluster, select __Create__ from hello __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="cbb0f-249">Usare Azione di script dai modelli di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="cbb0f-249">Use a Script Action from Azure Resource Manager templates</span></span>

<span data-ttu-id="cbb0f-250">esempi di Hello in questa sezione illustrano come toouse script azioni con modelli di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-250">hello examples in this section demonstrate how toouse script actions with Azure Resource Manager templates.</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="cbb0f-251">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="cbb0f-251">Before you begin</span></span>

* <span data-ttu-id="cbb0f-252">Per informazioni sulla configurazione di un toorun workstation, i cmdlet HDInsight Powershell, vedere [installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-252">For information about configuring a workstation toorun HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="cbb0f-253">Per istruzioni su come toocreate modelli, vedere [modelli Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-253">For instructions on how toocreate templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="cbb0f-254">Se Azure PowerShell non è stato usato in precedenza con Gestione risorse, vedere [Uso di Azure PowerShell con Gestione risorse di Azure](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-254">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="cbb0f-255">Creare cluster usando l'azione script</span><span class="sxs-lookup"><span data-stu-id="cbb0f-255">Create clusters using Script Action</span></span>

1. <span data-ttu-id="cbb0f-256">Copiare hello seguente percorso tooa modelli nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-256">Copy hello following template tooa location on your computer.</span></span> <span data-ttu-id="cbb0f-257">Questo modello consente di installare Giraph in hello headnodes e lavoro i nodi del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-257">This template installs Giraph on hello headnodes and worker nodes in hello cluster.</span></span> <span data-ttu-id="cbb0f-258">È inoltre possibile verificare se il modello JSON hello è valido.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-258">You can also verify if hello JSON template is valid.</span></span> <span data-ttu-id="cbb0f-259">Incollare il contenuto del modello in [JSONLint](http://jsonlint.com/), uno strumento di convalida JSON disponibile online.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-259">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

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
2. <span data-ttu-id="cbb0f-260">Avviare PowerShell di Azure e accedere tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-260">Start Azure PowerShell and Log in tooyour Azure account.</span></span> <span data-ttu-id="cbb0f-261">Dopo aver fornito le credenziali, hello comando restituisce le informazioni relative all'account.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-261">After providing your credentials, hello command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="cbb0f-262">Se si dispone di più sottoscrizioni, fornire l'ID sottoscrizione hello desiderato toouse per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-262">If you have multiple subscriptions, provide hello subscription ID you wish toouse for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="cbb0f-263">È possibile utilizzare `Get-AzureRmSubscription` tooget un elenco di tutte le sottoscrizioni associate all'account, che include l'ID sottoscrizione hello per ognuno di essi.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-263">You can use `Get-AzureRmSubscription` tooget a list of all subscriptions associated with your account, which includes hello subscription ID for each one.</span></span>

4. <span data-ttu-id="cbb0f-264">Se non è già disponibile un gruppo di risorse, crearne uno.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-264">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="cbb0f-265">Specificare il nome di hello del gruppo di risorse hello e il percorso che è necessario per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-265">Provide hello name of hello resource group and location that you need for your solution.</span></span> <span data-ttu-id="cbb0f-266">Viene restituito un riepilogo del nuovo gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-266">A summary of hello new resource group is returned.</span></span>

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

5. <span data-ttu-id="cbb0f-267">una distribuzione per il gruppo di risorse, eseguire hello toocreate **New AzureRmResourceGroupDeployment** comando e specificare i parametri necessari hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-267">toocreate a deployment for your resource group, run hello **New-AzureRmResourceGroupDeployment** command and provide hello necessary parameters.</span></span> <span data-ttu-id="cbb0f-268">i parametri di Hello includono hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-268">hello parameters include hello following data:</span></span>

    * <span data-ttu-id="cbb0f-269">Nome per la distribuzione</span><span class="sxs-lookup"><span data-stu-id="cbb0f-269">A name for your deployment</span></span>
    * <span data-ttu-id="cbb0f-270">nome di Hello del gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="cbb0f-270">hello name of your resource group</span></span>
    * <span data-ttu-id="cbb0f-271">percorso di Hello o modello di URL toohello creato.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-271">hello path or URL toohello template you created.</span></span>

  <span data-ttu-id="cbb0f-272">Passare anche gli eventuali altri parametri richiesti dal modello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-272">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="cbb0f-273">In questo caso, hello script azione tooinstall R nel cluster hello non richiede alcun parametro.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-273">In this case, hello script action tooinstall R on hello cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="cbb0f-274">Sono valori tooprovide richiesta per i parametri di hello definiti nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-274">You are prompted tooprovide values for hello parameters defined in hello template.</span></span>

1. <span data-ttu-id="cbb0f-275">Quando il gruppo di risorse hello è stato distribuito, viene visualizzato un riepilogo della distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-275">When hello resource group has been deployed, a summary of hello deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="cbb0f-276">Se la distribuzione non riesce, è possibile utilizzare i seguenti cmdlet tooget informazioni sugli errori di hello hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-276">If your deployment fails, you can use hello following cmdlets tooget information about hello failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="cbb0f-277">Usare un'azione script durante la creazione di un cluster da Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbb0f-277">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="cbb0f-278">In questa sezione, utilizziamo hello [Aggiungi AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke script utilizzando l'azione Script toocustomize un cluster.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-278">In this section, we use hello [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts by using Script Action toocustomize a cluster.</span></span> <span data-ttu-id="cbb0f-279">Prima di procedere, assicurarsi di aver installato e configurato Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-279">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="cbb0f-280">Per informazioni sulla configurazione di un toorun workstation, i cmdlet HDInsight PowerShell, vedere [installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-280">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="cbb0f-281">Hello script riportato di seguito viene illustrato come tooapply un'azione di script durante la creazione di un cluster con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-281">hello following script demonstrates how tooapply a script action when creating a cluster using PowerShell:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

<span data-ttu-id="cbb0f-282">Può richiedere alcuni minuti prima che venga creato il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-282">It can take several minutes before hello cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="cbb0f-283">Utilizzare un'azione di Script durante la creazione del cluster da hello HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="cbb0f-283">Use a Script Action during cluster creation from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="cbb0f-284">Hello HDInsight .NET SDK fornisce librerie client che rende più semplice toowork con HDInsight da un'applicazione .NET.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-284">hello HDInsight .NET SDK provides client libraries that makes it easier toowork with HDInsight from a .NET application.</span></span> <span data-ttu-id="cbb0f-285">Per un esempio di codice, vedere [basati su Linux creare cluster HDInsight con hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-285">For a code sample, see [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-tooa-running-cluster"></a><span data-ttu-id="cbb0f-286">Applicare un tooa genera Script azione in esecuzione del cluster</span><span class="sxs-lookup"><span data-stu-id="cbb0f-286">Apply a Script Action tooa running cluster</span></span>

<span data-ttu-id="cbb0f-287">In questa sezione, informazioni su come tooapply script tooa azioni in esecuzione del cluster.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-287">In this section, learn how tooapply script actions tooa running cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a><span data-ttu-id="cbb0f-288">Applicare un tooa genera Script azione in esecuzione del cluster da hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cbb0f-288">Apply a Script Action tooa running cluster from hello Azure portal</span></span>

1. <span data-ttu-id="cbb0f-289">Da hello [portale di Azure](https://portal.azure.com), selezionare il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-289">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="cbb0f-290">Panoramica del cluster HDInsight hello, selezionare hello **azioni Script** riquadro.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-290">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![Riquadro Azioni script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="cbb0f-292">È inoltre possibile selezionare **tutte le impostazioni** e quindi selezionare **azioni Script** da hello sezione Impostazioni.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-292">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

3. <span data-ttu-id="cbb0f-293">Dall'alto hello di hello sezione azioni Script, selezionare **invia di nuovo**.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-293">From hello top of hello Script Actions section, select **Submit new**.</span></span>

    ![Aggiungere un tooa di script in esecuzione del cluster](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="cbb0f-295">Hello utilizzare __selezionare uno script__ tooselect voce uno script di pre-effettuato.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-295">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="cbb0f-296">toouse uno script personalizzato, selezionare __personalizzato__ e quindi fornire hello __nome__ e __l'URI dello script Bash__ per lo script.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-296">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Aggiungere uno script nel modulo di script selezionare hello](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="cbb0f-298">Hello nella tabella seguente vengono descritti gli elementi di hello in form di hello:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-298">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="cbb0f-299">Proprietà</span><span class="sxs-lookup"><span data-stu-id="cbb0f-299">Property</span></span> | <span data-ttu-id="cbb0f-300">Valore</span><span class="sxs-lookup"><span data-stu-id="cbb0f-300">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="cbb0f-301">Selezionare uno script</span><span class="sxs-lookup"><span data-stu-id="cbb0f-301">Select a script</span></span> | <span data-ttu-id="cbb0f-302">toouse lo script, seleziona __personalizzato__.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-302">toouse your own script, select __custom__.</span></span> <span data-ttu-id="cbb0f-303">In caso contrario, selezionare uno degli script disponibili.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-303">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="cbb0f-304">Nome</span><span class="sxs-lookup"><span data-stu-id="cbb0f-304">Name</span></span> |<span data-ttu-id="cbb0f-305">Specificare un nome per l'azione script hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-305">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="cbb0f-306">URI script Bash</span><span class="sxs-lookup"><span data-stu-id="cbb0f-306">Bash script URI</span></span> |<span data-ttu-id="cbb0f-307">Specificare hello URI toohello script che è richiamato toocustomize hello cluster.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-307">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="cbb0f-308">Head/Worker/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="cbb0f-308">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="cbb0f-309">Specificare i nodi di hello (**Head**, **lavoro**, o **ZooKeeper**) in cui personalizzazione hello viene eseguito uno script.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-309">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="cbb0f-310">parameters</span><span class="sxs-lookup"><span data-stu-id="cbb0f-310">Parameters</span></span> |<span data-ttu-id="cbb0f-311">Specificare i parametri di hello, se richiesti dallo script hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-311">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="cbb0f-312">Hello utilizzare __mantenere questa azione script__ voce toomake che hello script viene applicato durante le operazioni di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-312">Use hello __Persist this script action__ entry toomake sure hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="cbb0f-313">Infine, utilizzare hello **crea** cluster toohello di pulsante tooapply hello script.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-313">Finally, use hello **Create** button tooapply hello script toohello cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a><span data-ttu-id="cbb0f-314">Applicare un tooa genera Script azione in esecuzione i cluster di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbb0f-314">Apply a Script Action tooa running cluster from Azure PowerShell</span></span>

<span data-ttu-id="cbb0f-315">Prima di procedere, assicurarsi di aver installato e configurato Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-315">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="cbb0f-316">Per informazioni sulla configurazione di un toorun workstation, i cmdlet HDInsight PowerShell, vedere [installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-316">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="cbb0f-317">Hello esempio seguente viene illustrato come un cluster in esecuzione di script azione tooa tooapply:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-317">hello following example demonstrates how tooapply a script action tooa running cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

<span data-ttu-id="cbb0f-318">Al termine dell'operazione di hello, viene visualizzato toohello di informazioni simili seguente testo:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-318">Once hello operation completes, you receive information similar toohello following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a><span data-ttu-id="cbb0f-319">Applicare un tooa genera Script azione in esecuzione del cluster da hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="cbb0f-319">Apply a Script Action tooa running cluster from hello Azure CLI</span></span>

<span data-ttu-id="cbb0f-320">Prima di procedere, assicurarsi di avere installato e configurato hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-320">Before proceeding, make sure you have installed and configured hello Azure CLI.</span></span> <span data-ttu-id="cbb0f-321">Per ulteriori informazioni, vedere [installazione hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-321">For more information, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="cbb0f-322">tooswitch tooAzure modalità di gestione delle risorse, utilizzare hello comando hello riga di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-322">tooswitch tooAzure Resource Manager mode, use hello following command at hello command line:</span></span>

        azure config mode arm

2. <span data-ttu-id="cbb0f-323">Utilizzare hello seguente tooauthenticate tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-323">Use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="cbb0f-324">Utilizzare hello successivo comando tooapply un tooa azione script in esecuzione del cluster</span><span class="sxs-lookup"><span data-stu-id="cbb0f-324">Use hello following command tooapply a script action tooa running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="cbb0f-325">Se non vengono specificati alcuni parametri per il comando, verrà richiesto di specificarli.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-325">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="cbb0f-326">Se hello script specificare con `-u` accetta parametri, è possibile specificare tali utilizzando hello `-p` parametro.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-326">If hello script you specify with `-u` accepts parameters, you can specify them using hello `-p` parameter.</span></span>

    <span data-ttu-id="cbb0f-327">I tipi di nodo validi sono `headnode`, `workernode`, e `zookeeper`.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-327">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="cbb0f-328">Se script hello devono essere tipi di nodo toomultiple applicato, specificare i tipi di hello separati da un ';'.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-328">If hello script should be applied toomultiple node types, specify hello types separated by a ';'.</span></span> <span data-ttu-id="cbb0f-329">ad esempio `-n headnode;workernode`.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-329">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="cbb0f-330">toopersist hello script, aggiungere hello `--persistOnSuccess`.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-330">toopersist hello script, add hello `--persistOnSuccess`.</span></span> <span data-ttu-id="cbb0f-331">È inoltre possibile mantenere in un secondo momento script hello utilizzando `azure hdinsight script-action persisted set`.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-331">You can also persist hello script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="cbb0f-332">Al termine del processo di hello, viene visualizzato toohello simili di output il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-332">Once hello job completes, you receive output similar toohello following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a><span data-ttu-id="cbb0f-333">Applicare un tooa genera Script azione in esecuzione tramite l'API REST di cluster</span><span class="sxs-lookup"><span data-stu-id="cbb0f-333">Apply a Script Action tooa running cluster using REST API</span></span>

<span data-ttu-id="cbb0f-334">Vedere l'articolo su come [eseguire azioni script in un cluster in esecuzione](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-334">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="cbb0f-335">Applicare un tooa genera Script azione in esecuzione del cluster da hello HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="cbb0f-335">Apply a Script Action tooa running cluster from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="cbb0f-336">Per un esempio di utilizzo di hello .NET SDK tooapply script tooa cluster, vedere [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-336">For an example of using hello .NET SDK tooapply scripts tooa cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="cbb0f-337">Visualizzare la cronologia, alzare e abbassare di livello le azioni script</span><span class="sxs-lookup"><span data-stu-id="cbb0f-337">View history, promote, and demote Script Actions</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="cbb0f-338">Utilizzo di hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cbb0f-338">Using hello Azure portal</span></span>

1. <span data-ttu-id="cbb0f-339">Da hello [portale di Azure](https://portal.azure.com), selezionare il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-339">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="cbb0f-340">Panoramica del cluster HDInsight hello, selezionare hello **azioni Script** riquadro.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-340">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![Riquadro Azioni script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="cbb0f-342">È inoltre possibile selezionare **tutte le impostazioni** e quindi selezionare **azioni Script** da hello sezione Impostazioni.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-342">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

4. <span data-ttu-id="cbb0f-343">Una cronologia degli script per il cluster viene visualizzata nella sezione azioni Script hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-343">A history of scripts for this cluster is displayed on hello Script Actions section.</span></span> <span data-ttu-id="cbb0f-344">Queste informazioni includono un elenco degli script persistenti.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-344">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="cbb0f-345">Nella schermata di hello riportata di seguito, è possibile visualizzare tale hello Solr script è stato eseguito nel cluster.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-345">In hello screenshot below, you can see that hello Solr script has been ran on this cluster.</span></span> <span data-ttu-id="cbb0f-346">schermata di Hello non sono presenti eventuali script persistenti.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-346">hello screenshot does not show any persisted scripts.</span></span>

    ![Sezione Azioni script](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="cbb0f-348">Selezione di uno script dalla cronologia hello Visualizza sezione proprietà hello per questo script.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-348">Selecting a script from hello history displays hello Properties section for this script.</span></span> <span data-ttu-id="cbb0f-349">Dall'alto hello della schermata di hello, è possibile eseguire di nuovo script hello o alzare di livello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-349">From hello top of hello screen, you can rerun hello script or promote it.</span></span>

    ![Proprietà delle azioni script](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="cbb0f-351">È inoltre possibile utilizzare hello **...**  toohello a destra delle voci sulle azioni di tooperform sezione azioni Script hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-351">You can also use hello **...** toohello right of entries on hello Script Actions section tooperform actions.</span></span>

    ![Uso di ... nelle azioni script](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="cbb0f-353">Uso di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbb0f-353">Using Azure PowerShell</span></span>

| <span data-ttu-id="cbb0f-354">Utilizzare la seguente hello...</span><span class="sxs-lookup"><span data-stu-id="cbb0f-354">Use hello following...</span></span> | <span data-ttu-id="cbb0f-355">Anche...</span><span class="sxs-lookup"><span data-stu-id="cbb0f-355">too...</span></span> |
| --- | --- |
| <span data-ttu-id="cbb0f-356">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="cbb0f-356">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="cbb0f-357">Recuperare informazioni sulle azioni script persistenti</span><span class="sxs-lookup"><span data-stu-id="cbb0f-357">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="cbb0f-358">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="cbb0f-358">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="cbb0f-359">Recuperare una cronologia dei cluster toohello applicare azioni di script o i dettagli per uno script specifico</span><span class="sxs-lookup"><span data-stu-id="cbb0f-359">Retrieve a history of script actions applied toohello cluster, or details for a specific script</span></span> |
| <span data-ttu-id="cbb0f-360">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="cbb0f-360">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="cbb0f-361">Alza di livello un ad hoc tooa azioni script persistenti genera script azione</span><span class="sxs-lookup"><span data-stu-id="cbb0f-361">Promotes an ad hoc script action tooa persisted script action</span></span> |
| <span data-ttu-id="cbb0f-362">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="cbb0f-362">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="cbb0f-363">Abbassa di livello un'azione di script con salvataggio permanente azione tooan ad hoc</span><span class="sxs-lookup"><span data-stu-id="cbb0f-363">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="cbb0f-364">Utilizzando `Remove-AzureRmHDInsightPersistedScriptAction` non vengono annullate le azioni di hello eseguite da uno script.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-364">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="cbb0f-365">Questo cmdlet rimuove solo flag persistente hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-365">This cmdlet only removes hello persisted flag.</span></span>

<span data-ttu-id="cbb0f-366">Hello lo script di esempio seguente viene illustrato come utilizzare toopromote cmdlet hello e abbassare di livello uno script.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-366">hello following example script demonstrates using hello cmdlets toopromote, then demote a script.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a><span data-ttu-id="cbb0f-367">Utilizzo di hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="cbb0f-367">Using hello Azure CLI</span></span>

| <span data-ttu-id="cbb0f-368">Utilizzare la seguente hello...</span><span class="sxs-lookup"><span data-stu-id="cbb0f-368">Use hello following...</span></span> | <span data-ttu-id="cbb0f-369">Anche...</span><span class="sxs-lookup"><span data-stu-id="cbb0f-369">too...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="cbb0f-370">Recuperare un elenco di azioni script con salvataggio permanente</span><span class="sxs-lookup"><span data-stu-id="cbb0f-370">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="cbb0f-371">Recuperare informazioni su una specifica azione script con salvataggio permanente</span><span class="sxs-lookup"><span data-stu-id="cbb0f-371">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="cbb0f-372">Recuperare una cronologia dei cluster toohello applicare azioni di script</span><span class="sxs-lookup"><span data-stu-id="cbb0f-372">Retrieve a history of script actions applied toohello cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="cbb0f-373">Recuperare informazioni su un'azione script specifica</span><span class="sxs-lookup"><span data-stu-id="cbb0f-373">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="cbb0f-374">Alza di livello un ad hoc tooa azioni script persistenti genera script azione</span><span class="sxs-lookup"><span data-stu-id="cbb0f-374">Promotes an ad hoc script action tooa persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="cbb0f-375">Abbassa di livello un'azione di script con salvataggio permanente azione tooan ad hoc</span><span class="sxs-lookup"><span data-stu-id="cbb0f-375">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="cbb0f-376">Utilizzando `azure hdinsight script-action persisted delete` non vengono annullate le azioni di hello eseguite da uno script.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-376">Using `azure hdinsight script-action persisted delete` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="cbb0f-377">Questo cmdlet rimuove solo flag persistente hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-377">This cmdlet only removes hello persisted flag.</span></span>

### <a name="using-hello-hdinsight-net-sdk"></a><span data-ttu-id="cbb0f-378">Utilizzo di hello HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="cbb0f-378">Using hello HDInsight .NET SDK</span></span>

<span data-ttu-id="cbb0f-379">Per un esempio dell'utilizzo di cronologia di hello .NET SDK tooretrieve script da un cluster, alzare di livello o abbassare di livello gli script, vedere [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-379">For an example of using hello .NET SDK tooretrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="cbb0f-380">Questo esempio viene illustrato come un'applicazione di HDInsight mediante tooinstall hello .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-380">This example also demonstrates how tooinstall an HDInsight application using hello .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="cbb0f-381">Supporto per software open source usato nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="cbb0f-381">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="cbb0f-382">servizio Microsoft Azure HDInsight Hello utilizza un ecosistema di tecnologie open source in corrispondenza di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-382">hello Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="cbb0f-383">Microsoft Azure offre un livello di supporto generale per le tecnologie open source.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-383">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="cbb0f-384">Per ulteriori informazioni, vedere hello **ambito supporto** sezione di hello [sito Web di Azure Support FAQ](https://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-384">For more information, see hello **Support Scope** section of hello [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="cbb0f-385">servizio HDInsight Hello fornisce un ulteriore livello di supporto per i componenti predefiniti.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-385">hello HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="cbb0f-386">Esistono due tipi di componenti open source che sono disponibili nel servizio HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-386">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="cbb0f-387">**I componenti predefiniti** -questi componenti sono pre-installati nei cluster HDInsight e forniscono funzionalità di base del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-387">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="cbb0f-388">Ad esempio, ResourceManager YARN, linguaggio di query Hive hello (HiveQL) e libreria Mahout hello appartenere toothis categoria.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-388">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="cbb0f-389">È disponibile in un elenco completo dei componenti cluster [novità introdotta nelle versioni di cluster Hadoop hello fornite da HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-389">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="cbb0f-390">**I componenti personalizzati** -, come un utente del cluster di hello, puoi installare o utilizzare nel carico di lavoro qualsiasi componente disponibile nella community hello o creato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-390">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="cbb0f-391">I componenti forniti con i cluster di HDInsight hello sono completamente supportati.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-391">Components provided with hello HDInsight cluster are fully supported.</span></span> <span data-ttu-id="cbb0f-392">Il supporto di Microsoft consente tooisolate e risolvere i problemi correlati toothese componenti.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-392">Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="cbb0f-393">I componenti personalizzati ricevano supporto commercialmente ragionevole toohelp toofurther per risolvere il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-393">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="cbb0f-394">Supporto tecnico Microsoft potrebbe essere in grado di tooresolve problema di hello o si potrebbero chiedere i canali disponibili tooengage per tecnologie open source hello in cui si trova esperienza completa per tale tecnologia.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-394">Microsoft support may be able tooresolve hello issue OR they may ask you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="cbb0f-395">È ad esempio possibile ricorrere a molti siti di community, come il [forum MSDN per HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com). Anche per i progetti Apache sono disponibili siti specifici in [http://apache.org](http://apache.org), ad esempio [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-395">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="cbb0f-396">servizio HDInsight Hello modi diversi componenti personalizzati toouse.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-396">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="cbb0f-397">Hello si applica allo stesso livello di supporto, indipendentemente da come un componente viene utilizzato o installato nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-397">hello same level of support applies, regardless of how a component is used or installed on hello cluster.</span></span> <span data-ttu-id="cbb0f-398">Hello elenco seguente vengono descritti modi più comuni di hello che i componenti personalizzati possono essere utilizzati nei cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-398">hello following list describes hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="cbb0f-399">Invio di processi - Hadoop o altri tipi di processi che utilizzano componenti personalizzati di esecuzione può essere inviato toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-399">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>

2. <span data-ttu-id="cbb0f-400">Personalizzazione del cluster - durante la creazione del cluster, è possibile specificare impostazioni aggiuntive e i componenti personalizzati che vengono installati nei nodi del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-400">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on hello cluster nodes.</span></span>

3. <span data-ttu-id="cbb0f-401">Esempi - per componenti personalizzati più diffusi, Microsoft e altri utenti possono fornire esempi di come utilizzare questi componenti nei cluster di HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-401">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="cbb0f-402">Questi esempi vengono forniti senza supporto.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-402">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="cbb0f-403">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="cbb0f-403">Troubleshooting</span></span>

<span data-ttu-id="cbb0f-404">È possibile utilizzare Ambari web UI tooview informazioni registrate dalle azioni di script.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-404">You can use Ambari web UI tooview information logged by script actions.</span></span> <span data-ttu-id="cbb0f-405">Se lo script hello non riesce durante la creazione del cluster, sono disponibili nell'account di archiviazione predefinito hello associato hello cluster anche hello log.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-405">If hello script fails during cluster creation, hello logs are also available in hello default storage account associated with hello cluster.</span></span> <span data-ttu-id="cbb0f-406">In questa sezione vengono fornite informazioni sul funzionamento dei registri tooretrieve hello utilizzando entrambe queste opzioni.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-406">This section provides information on how tooretrieve hello logs using both these options.</span></span>

### <a name="using-hello-ambari-web-ui"></a><span data-ttu-id="cbb0f-407">Utilizzo dell'interfaccia utente Web Ambari hello</span><span class="sxs-lookup"><span data-stu-id="cbb0f-407">Using hello Ambari Web UI</span></span>

1. <span data-ttu-id="cbb0f-408">Nel browser passare toohttps://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-408">In your browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="cbb0f-409">Sostituire CLUSTERNAME con nome hello del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-409">Replace CLUSTERNAME with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="cbb0f-410">Quando richiesto, immettere nome dell'account admin hello (amministratore) e la password per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-410">When prompted, enter hello admin account name (admin) and password for hello cluster.</span></span> <span data-ttu-id="cbb0f-411">Credenziali di amministratore hello tooreenter potrebbe essere in un web form.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-411">You may have tooreenter hello admin credentials in a web form.</span></span>

2. <span data-ttu-id="cbb0f-412">Selezionare hello hello barra nella parte superiore di hello della pagina hello **ops** voce.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-412">From hello bar at hello top of hello page, select hello **ops** entry.</span></span> <span data-ttu-id="cbb0f-413">Viene visualizzato un elenco delle operazioni correnti e precedenti eseguite su cluster hello tramite Ambari.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-413">A list of current and previous operations performed on hello cluster through Ambari is displayed.</span></span>

    ![Barra nell'interfaccia utente di Ambari con selezionato ops](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="cbb0f-415">Trovare le voci di hello associate **eseguire\_customscriptaction** in hello **operazioni** colonna.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-415">Find hello entries that have **run\_customscriptaction** in hello **Operations** column.</span></span> <span data-ttu-id="cbb0f-416">Queste voci vengono create quando esegue le azioni Script hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-416">These entries are created when hello Script Actions run.</span></span>

    ![Schermata delle operazioni](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="cbb0f-418">hello tooview STDOUT e STDERR uscita, selezionare una voce run\customscriptaction hello e drill-down tramite collegamenti hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-418">tooview hello STDOUT and STDERR output, select hello run\customscriptaction entry and drill down through hello links.</span></span> <span data-ttu-id="cbb0f-419">Questo output viene generato quando l'esecuzione dello script hello e possono contenere informazioni utili.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-419">This output is generated when hello script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-hello-default-storage-account"></a><span data-ttu-id="cbb0f-420">Registri di accesso dall'account di archiviazione predefinito hello</span><span class="sxs-lookup"><span data-stu-id="cbb0f-420">Access logs from hello default storage account</span></span>

<span data-ttu-id="cbb0f-421">Se la creazione del cluster di hello non riesce a causa di errore script tooa, hello registri sono accessibili dall'account di archiviazione cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-421">If hello cluster creation fails due tooa script action error, hello logs can be accessed from hello cluster storage account.</span></span>

* <span data-ttu-id="cbb0f-422">Hello i log di archiviazione sono disponibili in `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-422">hello storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![Schermata delle operazioni](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="cbb0f-424">In questa directory, hello registri sono organizzati per nodo head, workernode e nodi zookeeper separatamente.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-424">Under this directory, hello logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="cbb0f-425">Di seguito sono riportati alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-425">Some examples are:</span></span>

    * <span data-ttu-id="cbb0f-426">**Nodo head** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="cbb0f-426">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="cbb0f-427">**Nodo del ruolo di lavoro** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="cbb0f-427">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="cbb0f-428">**Nodo Zookeeper** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="cbb0f-428">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="cbb0f-429">Tutti i stdout e stderr dell'host corrispondente hello è caricato toohello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-429">All stdout and stderr of hello corresponding host is uploaded toohello storage account.</span></span> <span data-ttu-id="cbb0f-430">Per ogni azione script esiste un file **output-\*.txt** e un file **errors-\*.txt**.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-430">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="cbb0f-431">file txt di output di Hello contiene informazioni su hello URI dello script hello che è stata eseguita sull'host hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-431">hello output-*.txt file contains information about hello URI of hello script that got run on hello host.</span></span> <span data-ttu-id="cbb0f-432">Ad esempio</span><span class="sxs-lookup"><span data-stu-id="cbb0f-432">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="cbb0f-433">È possibile creare un cluster di azione script ripetutamente con hello stesso nome.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-433">It's possible that you repeatedly create a script action cluster with hello same name.</span></span> <span data-ttu-id="cbb0f-434">In tal caso, è possibile distinguere i log rilevanti di hello in base al nome di cartella Data hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-434">In such case, you can distinguish hello relevant logs based on hello DATE folder name.</span></span> <span data-ttu-id="cbb0f-435">Ad esempio, la struttura di cartelle hello per un cluster (mycluster) creato in date diverse appare simile toohello seguenti voci di log:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-435">For example, hello folder structure for a cluster (mycluster) created on different dates appears similar toohello following log entries:</span></span>

    <span data-ttu-id="cbb0f-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04``\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="cbb0f-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="cbb0f-437">Se si crea un cluster di azione di script con hello stesso nome in hello stesso giorno, è possibile utilizzare file di log desiderati hello tooidentify hello prefisso univoco.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-437">If you create a script action cluster with hello same name on hello same day, you can use hello unique prefix tooidentify hello relevant log files.</span></span>

* <span data-ttu-id="cbb0f-438">Se si crea un cluster quasi 12:00 (mezzanotte), è possibile che i file di log hello estendersi attraverso due giorni.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-438">If you create a cluster near 12:00AM (midnight), it's possible that hello log files span across two days.</span></span> <span data-ttu-id="cbb0f-439">In questi casi, vedrai due cartelle data diversi per hello dello stesso cluster.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-439">In such cases, you see two different date folders for hello same cluster.</span></span>

* <span data-ttu-id="cbb0f-440">Contenitore predefinito di toohello i file di registro caricamento può richiedere too5 minuti, in particolare per i cluster di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-440">Uploading log files toohello default container can take up too5 mins, especially for large clusters.</span></span> <span data-ttu-id="cbb0f-441">In tal caso, se si desidera registri hello tooaccess, è necessario non immediatamente eliminare cluster hello se ha esito negativo di un'azione di script.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-441">So, if you want tooaccess hello logs, you should not immediately delete hello cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="cbb0f-442">Watchdog Ambari</span><span class="sxs-lookup"><span data-stu-id="cbb0f-442">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="cbb0f-443">Non modificare la password di hello per hello Ambari Watchdog (hdinsightwatchdog) il cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-443">Do not change hello password for hello Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="cbb0f-444">La modifica della password per questo account hello interruzioni hello possibilità toorun nuove azioni di script nel cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-444">Changing hello password for this account breaks hello ability toorun new script actions on hello HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="cbb0f-445">Non è possibile importare il nome BlobService</span><span class="sxs-lookup"><span data-stu-id="cbb0f-445">Can't import name BlobService</span></span>

<span data-ttu-id="cbb0f-446">__Sintomi__: hello script azione non riuscita.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-446">__Symptoms__: hello script action fails.</span></span> <span data-ttu-id="cbb0f-447">Quando si visualizza l'operazione di hello in Ambari, viene visualizzato toohello simile a testo errore seguente:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-447">Text similar toohello following error is displayed when you view hello operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="cbb0f-448">__Causa__: questo errore si verifica se si esegue l'aggiornamento del client di archiviazione di Azure Python hello incluso con i cluster di HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-448">__Cause__: This error occurs if you upgrade hello Python Azure Storage client that is included with hello HDInsight cluster.</span></span> <span data-ttu-id="cbb0f-449">HDInsight prevede l'uso della versione 0.20.0 del client di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-449">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="cbb0f-450">__Risoluzione__: tooresolve questo errore, connettersi manualmente dei nodi del cluster utilizzando tooeach `ssh` e utilizzare hello seguendo versione client corretta archiviazione di comando tooreinstall hello:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-450">__Resolution__: tooresolve this error, manually connect tooeach cluster node using `ssh` and use hello following command tooreinstall hello correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="cbb0f-451">Per informazioni sulla connessione toohello cluster con SSH, vedere [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cbb0f-451">For information on connecting toohello cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="cbb0f-452">La cronologia non mostra gli script usati durante la creazione di un cluster</span><span class="sxs-lookup"><span data-stu-id="cbb0f-452">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="cbb0f-453">Se il cluster è stato creato prima del 15 marzo 2016, potrebbe non essere visualizzata una voce nella cronologia delle azioni script.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-453">If your cluster was created before March 15, 2016, you may not see an entry in Script Action history.</span></span> <span data-ttu-id="cbb0f-454">Se si ridimensiona cluster hello dopo 15 marzo 2016, hello script utilizzando durante la creazione del cluster vengono visualizzati nella cronologia applicate toonew nodi nel cluster di hello come parte di hello operazione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-454">If you resize hello cluster after March 15, 2016, hello scripts using during cluster creation appear in history as they are applied toonew nodes in hello cluster as part of hello resize operation.</span></span>

<span data-ttu-id="cbb0f-455">Sussistono due eccezioni:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-455">There are two exceptions:</span></span>

* <span data-ttu-id="cbb0f-456">Se il cluster è stato creato prima del 1° settembre 2015.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-456">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="cbb0f-457">Le azioni script sono state introdotte in questa data.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-457">This date is when Script Actions were introduced.</span></span> <span data-ttu-id="cbb0f-458">Per i cluster creati prima di tale data non possono quindi essere state usate le azioni script.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-458">Any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="cbb0f-459">Se è usato più azioni di Script durante la creazione del cluster e hello stesso nome per più script o hello stesso nome, stesso URI, ma parametri diversi per più script.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-459">If you used multiple Script Actions during cluster creation, and used hello same name for multiple scripts, or hello same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="cbb0f-460">In questi casi, viene visualizzato il seguente errore hello:</span><span class="sxs-lookup"><span data-stu-id="cbb0f-460">In these cases, you receive hello following error:</span></span>

    <span data-ttu-id="cbb0f-461">Nessun nuovo script azioni possono essere eseguito su questo cluster a causa di nomi di script tooconflicting negli script esistenti.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-461">No new script actions can be ran on this cluster due tooconflicting script names in existing scripts.</span></span> <span data-ttu-id="cbb0f-462">I nomi di script forniti durante la creazione del cluster devono essere tutti univoci.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-462">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="cbb0f-463">Gli script esistenti vengono eseguiti durante il ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="cbb0f-463">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbb0f-464">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cbb0f-464">Next steps</span></span>

* [<span data-ttu-id="cbb0f-465">Sviluppare script di Azione script per HDInsight</span><span class="sxs-lookup"><span data-stu-id="cbb0f-465">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="cbb0f-466">Installare e usare Solr nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="cbb0f-466">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="cbb0f-467">Installare e usare Giraph nei cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="cbb0f-467">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="cbb0f-468">Aggiungere ulteriore spazio di archiviazione tooan HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="cbb0f-468">Add additional storage tooan HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Fasi durante la creazione di un cluster"
