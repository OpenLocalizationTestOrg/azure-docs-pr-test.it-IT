---
title: aaaGet introduttiva a PowerShell per Azure Batch | Documenti Microsoft
description: "Toohello una rapida introduzione dei cmdlet di Azure PowerShell è possibile utilizzare le risorse di Batch toomanage."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: f9ad62c5-27bf-4e6b-a5bf-c5f5914e6199
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3e4d12e9c1e52a5b2db2dd44346edda93b7ef92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a><span data-ttu-id="47816-103">Gestire le risorse Batch con i cmdlet di PowerShell</span><span class="sxs-lookup"><span data-stu-id="47816-103">Manage Batch resources with PowerShell cmdlets</span></span>

<span data-ttu-id="47816-104">Con i cmdlet PowerShell di Azure Batch hello, è possibile eseguire e script molti hello stesse attività svolgere con le API di Batch, hello hello portale di Azure e hello Azure interfaccia della riga di comando (CLI).</span><span class="sxs-lookup"><span data-stu-id="47816-104">With hello Azure Batch PowerShell cmdlets, you can perform and script many of hello same tasks you carry out with hello Batch APIs, hello Azure portal, and hello Azure Command-Line Interface (CLI).</span></span> <span data-ttu-id="47816-105">Si tratta di un cmdlet toohello introduzione rapida è possibile usare toomanage gli account di Batch e lavorare con le risorse di Batch, ad esempio pool di processi e attività.</span><span class="sxs-lookup"><span data-stu-id="47816-105">This is a quick introduction toohello cmdlets you can use toomanage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span></span>

<span data-ttu-id="47816-106">Per un elenco completo dei cmdlet di Batch e sintassi del cmdlet dettagliate, vedere hello [riferimento ai cmdlet di Azure Batch](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="47816-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see hello [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>

<span data-ttu-id="47816-107">Questo articolo si basa sui cmdlet di Azure PowerShell versione 3.0.0.</span><span class="sxs-lookup"><span data-stu-id="47816-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span></span> <span data-ttu-id="47816-108">È consigliabile aggiornare il Azure PowerShell spesso tootake vantaggio di servizio aggiornamenti e miglioramenti.</span><span class="sxs-lookup"><span data-stu-id="47816-108">We recommend that you update your Azure PowerShell frequently tootake advantage of service updates and enhancements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47816-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="47816-109">Prerequisites</span></span>
<span data-ttu-id="47816-110">Eseguire hello dopo operazioni toouse Azure PowerShell toomanage le risorse di Batch.</span><span class="sxs-lookup"><span data-stu-id="47816-110">Perform hello following operations toouse Azure PowerShell toomanage your Batch resources.</span></span>

* [<span data-ttu-id="47816-111">Installare e configurare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="47816-111">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* <span data-ttu-id="47816-112">Eseguire hello **accesso AzureRmAccount** cmdlet tooconnect tooyour sottoscrizione (Buongiorno spedire i cmdlet di Azure Batch nel modulo di gestione risorse di Azure hello):</span><span class="sxs-lookup"><span data-stu-id="47816-112">Run hello **Login-AzureRmAccount** cmdlet tooconnect tooyour subscription (hello Azure Batch cmdlets ship in hello Azure Resource Manager module):</span></span>
  
    `Login-AzureRmAccount`
* <span data-ttu-id="47816-113">**Registrare con spazio dei nomi del provider di Batch hello**.</span><span class="sxs-lookup"><span data-stu-id="47816-113">**Register with hello Batch provider namespace**.</span></span> <span data-ttu-id="47816-114">Questa operazione è sufficiente eseguire toobe **una volta per ogni sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="47816-114">This operation only needs toobe performed **once per subscription**.</span></span>
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a><span data-ttu-id="47816-115">Gestire gli account e le chiavi Batch</span><span class="sxs-lookup"><span data-stu-id="47816-115">Manage Batch accounts and keys</span></span>
### <a name="create-a-batch-account"></a><span data-ttu-id="47816-116">Creare un account Batch</span><span class="sxs-lookup"><span data-stu-id="47816-116">Create a Batch account</span></span>
<span data-ttu-id="47816-117">**New-AzureRmBatchAccount** crea un account Batch in un gruppo di risorse specificato.</span><span class="sxs-lookup"><span data-stu-id="47816-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span></span> <span data-ttu-id="47816-118">Se si dispone già di un gruppo di risorse, crearne una eseguendo hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="47816-118">If you don't already have a resource group, create one by running hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span> <span data-ttu-id="47816-119">Specificare uno dei hello Azure aree in hello **percorso** parametro, ad esempio "Central US".</span><span class="sxs-lookup"><span data-stu-id="47816-119">Specify one of hello Azure regions in hello **Location** parameter, such as "Central US".</span></span> <span data-ttu-id="47816-120">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="47816-120">For example:</span></span>

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

<span data-ttu-id="47816-121">Quindi, creare un account Batch nel gruppo di risorse hello, specificando un nome per l'account di hello in <*account_name*> e il percorso di hello e nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="47816-121">Then, create a Batch account in hello resource group, specifying a name for hello account in <*account_name*> and hello location and name of your resource group.</span></span> <span data-ttu-id="47816-122">Creazione di account di Batch hello può richiedere alcuni toocomplete ora.</span><span class="sxs-lookup"><span data-stu-id="47816-122">Creating hello Batch account can take some time toocomplete.</span></span> <span data-ttu-id="47816-123">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="47816-123">For example:</span></span>

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> <span data-ttu-id="47816-124">account di Batch Hello nome deve essere univoco toohello area di Azure per il gruppo di risorse hello, essere compresa tra 3 e 24 caratteri e utilizzare solo lettere minuscole e numeri.</span><span class="sxs-lookup"><span data-stu-id="47816-124">hello Batch account name must be unique toohello Azure region for hello resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span></span>
> 
> 

### <a name="get-account-access-keys"></a><span data-ttu-id="47816-125">Ottenere le chiavi di accesso all'account</span><span class="sxs-lookup"><span data-stu-id="47816-125">Get account access keys</span></span>
<span data-ttu-id="47816-126">**Get-AzureRmBatchAccountKeys** Mostra chiavi di accesso hello associate a un account Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="47816-126">**Get-AzureRmBatchAccountKeys** shows hello access keys associated with an Azure Batch account.</span></span> <span data-ttu-id="47816-127">Ad esempio, eseguire hello seguenti chiavi tooget hello primaria e secondaria dell'account hello creato.</span><span class="sxs-lookup"><span data-stu-id="47816-127">For example, run hello following tooget hello primary and secondary keys of hello account you created.</span></span>

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a><span data-ttu-id="47816-128">Generare una nuova chiave di accesso</span><span class="sxs-lookup"><span data-stu-id="47816-128">Generate a new access key</span></span>
<span data-ttu-id="47816-129">**New-AzureRmBatchAccountKey** genera una nuova chiave dell'account primaria o secondaria per un account Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="47816-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span></span> <span data-ttu-id="47816-130">Ad esempio, toogenerate una nuova chiave primaria per l'account Batch, digitare:</span><span class="sxs-lookup"><span data-stu-id="47816-130">For example, toogenerate a new primary key for your Batch account, type:</span></span>

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> <span data-ttu-id="47816-131">toogenerate una nuova chiave secondaria, specificare "Secondario" per hello **KeyType** parametro.</span><span class="sxs-lookup"><span data-stu-id="47816-131">toogenerate a new secondary key, specify "Secondary" for hello **KeyType** parameter.</span></span> <span data-ttu-id="47816-132">Hai chiavi primarie e secondarie hello tooregenerate separatamente.</span><span class="sxs-lookup"><span data-stu-id="47816-132">You have tooregenerate hello primary and secondary keys separately.</span></span>
> 
> 

### <a name="delete-a-batch-account"></a><span data-ttu-id="47816-133">Eliminare un account Batch</span><span class="sxs-lookup"><span data-stu-id="47816-133">Delete a Batch account</span></span>
<span data-ttu-id="47816-134">**Remove-AzureRmBatchAccount** elimina un account Batch.</span><span class="sxs-lookup"><span data-stu-id="47816-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span></span> <span data-ttu-id="47816-135">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="47816-135">For example:</span></span>

    Remove-AzureRmBatchAccount -AccountName <account_name>

<span data-ttu-id="47816-136">Quando richiesto, confermare l'account di hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="47816-136">When prompted, confirm you want tooremove hello account.</span></span> <span data-ttu-id="47816-137">La rimozione di account può richiedere alcuni toocomplete ora.</span><span class="sxs-lookup"><span data-stu-id="47816-137">Account removal can take some time toocomplete.</span></span>

## <a name="create-a-batchaccountcontext-object"></a><span data-ttu-id="47816-138">Creare un oggetto BatchAccountContext</span><span class="sxs-lookup"><span data-stu-id="47816-138">Create a BatchAccountContext object</span></span>
<span data-ttu-id="47816-139">utilizzando tooauthenticate hello i cmdlet di PowerShell Batch quando si crea e Gestisci pool di Batch, i processi, attività, e altre risorse, creare innanzitutto un toostore oggetto BatchAccountContext il nome dell'account e le chiavi:</span><span class="sxs-lookup"><span data-stu-id="47816-139">tooauthenticate using hello Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object toostore your account name and keys:</span></span>

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

<span data-ttu-id="47816-140">Si passa l'oggetto di BatchAccountContext hello in cmdlet hello tale utilizzo **BatchContext** parametro.</span><span class="sxs-lookup"><span data-stu-id="47816-140">You pass hello BatchAccountContext object into cmdlets that use hello **BatchContext** parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="47816-141">Per impostazione predefinita, la chiave primaria dell'account hello viene utilizzata per l'autenticazione, ma è possibile selezionare esplicitamente toouse chiave hello modificando l'oggetto di BatchAccountContext **KeyInUse** proprietà: `$context.KeyInUse = "Secondary"`.</span><span class="sxs-lookup"><span data-stu-id="47816-141">By default, hello account's primary key is used for authentication, but you can explicitly select hello key toouse by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span></span>
> 
> 

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="47816-142">Creare e modificare le risorse Batch</span><span class="sxs-lookup"><span data-stu-id="47816-142">Create and modify Batch resources</span></span>
<span data-ttu-id="47816-143">Utilizzare i cmdlet, ad esempio **New AzureBatchPool**, **New AzureBatchJob**, e **New AzureBatchTask** toocreate risorse in un account di Batch.</span><span class="sxs-lookup"><span data-stu-id="47816-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** toocreate resources under a Batch account.</span></span> <span data-ttu-id="47816-144">Sono disponibili corrispondenti **Get -** e **Set -** proprietà hello tooupdate di cmdlet di risorse esistente, e **Remove -** cmdlet tooremove risorse con un account Batch.</span><span class="sxs-lookup"><span data-stu-id="47816-144">There are corresponding **Get-** and **Set-** cmdlets tooupdate hello properties of existing resources, and  **Remove-** cmdlets tooremove resources under a Batch account.</span></span>

<span data-ttu-id="47816-145">Quando si utilizza molti di questi cmdlet, toopassing inoltre un oggetto BatchContext, è necessario toocreate o passare gli oggetti che contengono le impostazioni dettagliate risorse, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="47816-145">When using many of these cmdlets, in addition toopassing a BatchContext object, you need toocreate or pass objects that contain detailed resource settings, as shown in hello following example.</span></span> <span data-ttu-id="47816-146">Vedere hello informazioni dettagliate della Guida per ciascun cmdlet per altri esempi.</span><span class="sxs-lookup"><span data-stu-id="47816-146">See hello detailed help for each cmdlet for additional examples.</span></span>

### <a name="create-a-batch-pool"></a><span data-ttu-id="47816-147">Creare un pool di Batch</span><span class="sxs-lookup"><span data-stu-id="47816-147">Create a Batch pool</span></span>
<span data-ttu-id="47816-148">Durante la creazione o l'aggiornamento di un pool di Batch, si seleziona la configurazione di macchina virtuale hello o della configurazione del servizio cloud hello per hello del sistema operativo su hello nodi di calcolo (vedere [Cenni preliminari sulle funzionalità di Batch](batch-api-basics.md#pool)).</span><span class="sxs-lookup"><span data-stu-id="47816-148">When creating or updating a Batch pool, you select either hello cloud service configuration or hello virtual machine configuration for hello operating system on hello compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span></span> <span data-ttu-id="47816-149">Se si specifica la configurazione del servizio cloud hello, i nodi di calcolo si crea un'immagine con uno di hello [versioni del sistema operativo Guest Azure](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span><span class="sxs-lookup"><span data-stu-id="47816-149">If you specify hello cloud service configuration, your compute nodes are imaged with one of hello [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span></span> <span data-ttu-id="47816-150">Se si specifica la configurazione della macchina virtuale hello, è possibile specificare uno dei hello è supportato Linux o immagini di macchina virtuale di Windows hello elencato in [macchine virtuali di Azure Marketplace][vm_marketplace], o fornire un oggetto personalizzato immagine preparata.</span><span class="sxs-lookup"><span data-stu-id="47816-150">If you specify hello virtual machine configuration, you can either specify one of hello supported Linux or Windows VM images listed in hello [Azure Virtual Machines Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span>

<span data-ttu-id="47816-151">Quando si esegue **New AzureBatchPool**, passare a impostazioni del sistema operativo hello in un oggetto PSCloudServiceConfiguration o PSVirtualMachineConfiguration.</span><span class="sxs-lookup"><span data-stu-id="47816-151">When you run **New-AzureBatchPool**, pass hello operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span></span> <span data-ttu-id="47816-152">Ad esempio, hello cmdlet seguente crea un nuovo pool di Batch con nodi di calcolo piccole dimensioni nella configurazione del servizio cloud hello, viene creata un'immagine con hello del sistema operativo più recente della famiglia 3 (Windows Server 2012).</span><span class="sxs-lookup"><span data-stu-id="47816-152">For example, hello following cmdlet creates a new Batch pool with size Small compute nodes in hello cloud service configuration, imaged with hello latest operating system version of family 3 (Windows Server 2012).</span></span> <span data-ttu-id="47816-153">In questo caso, hello **CloudServiceConfiguration** parametro specifica hello *$configuration* variabile come oggetto PSCloudServiceConfiguration hello.</span><span class="sxs-lookup"><span data-stu-id="47816-153">Here, hello **CloudServiceConfiguration** parameter specifies hello *$configuration* variable as hello PSCloudServiceConfiguration object.</span></span> <span data-ttu-id="47816-154">Hello **BatchContext** parametro specifica una variabile definita in precedenza *$context* come oggetto BatchAccountContext hello.</span><span class="sxs-lookup"><span data-stu-id="47816-154">hello **BatchContext** parameter specifies a previously defined variable *$context* as hello BatchAccountContext object.</span></span>

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

<span data-ttu-id="47816-155">numero di destinazione Hello dei nodi di calcolo nel nuovo pool di hello è determinato da una formula di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="47816-155">hello target number of compute nodes in hello new pool is determined by an autoscaling formula.</span></span> <span data-ttu-id="47816-156">In questo caso, la formula hello è semplicemente **$TargetDedicated = 4**, che indica il numero di hello dei nodi di calcolo nel pool di hello è al massimo 4.</span><span class="sxs-lookup"><span data-stu-id="47816-156">In this case, hello formula is simply **$TargetDedicated=4**, indicating hello number of compute nodes in hello pool is 4 at most.</span></span>

## <a name="query-for-pools-jobs-tasks-and-other-details"></a><span data-ttu-id="47816-157">Query per pool, processi, attività e altri dettagli</span><span class="sxs-lookup"><span data-stu-id="47816-157">Query for pools, jobs, tasks, and other details</span></span>
<span data-ttu-id="47816-158">Utilizzare i cmdlet, ad esempio **Get AzureBatchPool**, **Get AzureBatchJob**, e **Get AzureBatchTask** tooquery per le entità create con un account Batch.</span><span class="sxs-lookup"><span data-stu-id="47816-158">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** tooquery for entities created under a Batch account.</span></span>

### <a name="query-for-data"></a><span data-ttu-id="47816-159">Eseguire query per ottenere dati</span><span class="sxs-lookup"><span data-stu-id="47816-159">Query for data</span></span>
<span data-ttu-id="47816-160">Ad esempio, utilizzare **Get AzureBatchPools** toofind i pool.</span><span class="sxs-lookup"><span data-stu-id="47816-160">As an example, use **Get-AzureBatchPools** toofind your pools.</span></span> <span data-ttu-id="47816-161">Per impostazione predefinita, questo esegue una query per tutti i pool con l'account, presupponendo che sia già archiviato l'oggetto BatchAccountContext hello in *$context*:</span><span class="sxs-lookup"><span data-stu-id="47816-161">By default this queries for all pools under your account, assuming you already stored hello BatchAccountContext object in *$context*:</span></span>

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a><span data-ttu-id="47816-162">Usare un filtro OData</span><span class="sxs-lookup"><span data-stu-id="47816-162">Use an OData filter</span></span>
<span data-ttu-id="47816-163">È possibile specificare un filtro OData utilizzando hello **filtro** toofind parametro hello solo oggetti di cui si è interessati.</span><span class="sxs-lookup"><span data-stu-id="47816-163">You can supply an OData filter using hello **Filter** parameter toofind only hello objects you’re interested in.</span></span> <span data-ttu-id="47816-164">Ad esempio, è possibile trovare tutti i pool con nomi che iniziano con "myPool":</span><span class="sxs-lookup"><span data-stu-id="47816-164">For example, you can find all pools with ids starting with “myPool”:</span></span>

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

<span data-ttu-id="47816-165">Questo metodo non è flessibile come l'uso di "Where-Object" in una pipeline locale.</span><span class="sxs-lookup"><span data-stu-id="47816-165">This method is not as flexible as using “Where-Object” in a local pipeline.</span></span> <span data-ttu-id="47816-166">Tuttavia, query hello viene inviato toohello servizio Batch direttamente in modo che tutti i filtri avviene sul lato server hello, risparmiando larghezza di banda Internet.</span><span class="sxs-lookup"><span data-stu-id="47816-166">However, hello query gets sent toohello Batch service directly so that all filtering happens on hello server side, saving Internet bandwidth.</span></span>

### <a name="use-hello-id-parameter"></a><span data-ttu-id="47816-167">Utilizzare il parametro Id hello</span><span class="sxs-lookup"><span data-stu-id="47816-167">Use hello Id parameter</span></span>
<span data-ttu-id="47816-168">Un filtro di OData tooan alternativo è hello toouse **Id** parametro.</span><span class="sxs-lookup"><span data-stu-id="47816-168">An alternative tooan OData filter is toouse hello **Id** parameter.</span></span> <span data-ttu-id="47816-169">tooquery per un pool specifico con id "myPool":</span><span class="sxs-lookup"><span data-stu-id="47816-169">tooquery for a specific pool with id "myPool":</span></span>

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

<span data-ttu-id="47816-170">Hello **Id** parametro supporta solo la ricerca full-id, non i caratteri jolly o i filtri di stile di OData.</span><span class="sxs-lookup"><span data-stu-id="47816-170">hello **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span></span>

### <a name="use-hello-maxcount-parameter"></a><span data-ttu-id="47816-171">Utilizzare il parametro MaxCount hello</span><span class="sxs-lookup"><span data-stu-id="47816-171">Use hello MaxCount parameter</span></span>
<span data-ttu-id="47816-172">Per impostazione predefinita, ogni cmdlet restituisce un massimo di 1000 oggetti.</span><span class="sxs-lookup"><span data-stu-id="47816-172">By default, each cmdlet returns a maximum of 1000 objects.</span></span> <span data-ttu-id="47816-173">Se si raggiunge questo limite, ridefinire il filtro toobring nuovamente meno oggetti oppure impostare in modo esplicito un massimo di utilizzo hello **MaxCount** parametro.</span><span class="sxs-lookup"><span data-stu-id="47816-173">If you reach this limit, either refine your filter toobring back fewer objects, or explicitly set a maximum using hello **MaxCount** parameter.</span></span> <span data-ttu-id="47816-174">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="47816-174">For example:</span></span>

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

<span data-ttu-id="47816-175">limite superiore di hello tooremove, impostare **MaxCount** too0 o meno.</span><span class="sxs-lookup"><span data-stu-id="47816-175">tooremove hello upper bound, set **MaxCount** too0 or less.</span></span>

### <a name="use-hello-powershell-pipeline"></a><span data-ttu-id="47816-176">Utilizzare la pipeline di PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="47816-176">Use hello PowerShell pipeline</span></span>
<span data-ttu-id="47816-177">I cmdlet di batch possono sfruttare hello PowerShell pipeline toosend dei dati tra i cmdlet.</span><span class="sxs-lookup"><span data-stu-id="47816-177">Batch cmdlets can leverage hello PowerShell pipeline toosend data between cmdlets.</span></span> <span data-ttu-id="47816-178">Questa operazione ha lo stesso effetto dell'impostazione di un parametro, ma rende l'utilizzo con più entità hello.</span><span class="sxs-lookup"><span data-stu-id="47816-178">This has hello same effect as specifying a parameter, but makes working with multiple entities easier.</span></span>

<span data-ttu-id="47816-179">Ad esempio, per trovare e visualizzare tutte le attività dell'account:</span><span class="sxs-lookup"><span data-stu-id="47816-179">For example, find and display all tasks under your account:</span></span>

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

<span data-ttu-id="47816-180">Per riavviare ogni nodo di calcolo in un pool:</span><span class="sxs-lookup"><span data-stu-id="47816-180">Restart (reboot) every compute node in a pool:</span></span>

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a><span data-ttu-id="47816-181">Gestione dei pacchetti dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="47816-181">Application package management</span></span>
<span data-ttu-id="47816-182">Pacchetti di applicazioni forniscono un modo semplificato toodeploy applicazioni toohello nodi nei pool di calcolo.</span><span class="sxs-lookup"><span data-stu-id="47816-182">Application packages provide a simplified way toodeploy applications toohello compute nodes in your pools.</span></span> <span data-ttu-id="47816-183">Con i cmdlet di PowerShell Batch hello, è possibile caricare e gestire i pacchetti di applicazioni nell'account di Batch e distribuire i nodi toocompute di versioni di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="47816-183">With hello Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions toocompute nodes.</span></span>

<span data-ttu-id="47816-184">**Creare** un'applicazione:</span><span class="sxs-lookup"><span data-stu-id="47816-184">**Create** an application:</span></span>

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

<span data-ttu-id="47816-185">**Aggiungere** un pacchetto dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="47816-185">**Add** an application package:</span></span>

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

<span data-ttu-id="47816-186">Set hello **versione predefinita** per un'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="47816-186">Set hello **default version** for hello application:</span></span>

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

<span data-ttu-id="47816-187">**Elencare** i pacchetti dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="47816-187">**List** an application's packages</span></span>

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

<span data-ttu-id="47816-188">**Eliminare** un pacchetto dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="47816-188">**Delete** an application package</span></span>

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

<span data-ttu-id="47816-189">**Eliminare** un'applicazione</span><span class="sxs-lookup"><span data-stu-id="47816-189">**Delete** an application</span></span>

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> <span data-ttu-id="47816-190">È necessario eliminare tutte le versioni di pacchetto di applicazione di un'applicazione prima di eliminare un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="47816-190">You must delete all of an application's application package versions before you delete hello application.</span></span> <span data-ttu-id="47816-191">Se si tenta di toodelete un'applicazione che dispone attualmente di pacchetti di applicazioni, si riceverà un errore di 'Conflitto'.</span><span class="sxs-lookup"><span data-stu-id="47816-191">You will receive a 'Conflict' error if you try toodelete an application that currently has application packages.</span></span>
> 
> 

### <a name="deploy-an-application-package"></a><span data-ttu-id="47816-192">Distribuire un pacchetto dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="47816-192">Deploy an application package</span></span>
<span data-ttu-id="47816-193">Quando si crea un pool è possibile specificare uno o più pacchetti dell'applicazione da distribuire.</span><span class="sxs-lookup"><span data-stu-id="47816-193">You can specify one or more application packages for deployment when you create a pool.</span></span> <span data-ttu-id="47816-194">Quando si specifica un pacchetto in fase di creazione di pool, è il nodo tooeach distribuito come hello nodo join pool.</span><span class="sxs-lookup"><span data-stu-id="47816-194">When you specify a package at pool creation time, it is deployed tooeach node as hello node joins pool.</span></span> <span data-ttu-id="47816-195">I pacchetti vengono distribuiti anche quando un nodo viene riavviato o ne viene ricreata l'immagine.</span><span class="sxs-lookup"><span data-stu-id="47816-195">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="47816-196">Specificare hello `-ApplicationPackageReference` opzione quando si crea un pool toodeploy nodi di un pacchetto toohello del pool di applicazioni che si connettono pool hello.</span><span class="sxs-lookup"><span data-stu-id="47816-196">Specify hello `-ApplicationPackageReference` option when creating a pool toodeploy an application package toohello pool's nodes as they join hello pool.</span></span> <span data-ttu-id="47816-197">Creare innanzitutto un **PSApplicationPackageReference** dell'oggetto e configurarlo con hello Id pacchetto e la versione dell'applicazione si desidera toodeploy toohello pool nodi di calcolo:</span><span class="sxs-lookup"><span data-stu-id="47816-197">First, create a **PSApplicationPackageReference** object, and configure it with hello application Id and package version you want toodeploy toohello pool's compute nodes:</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

<span data-ttu-id="47816-198">A questo punto creare pool di hello e specificare l'oggetto di riferimento pacchetto hello hello argomento toohello `ApplicationPackageReferences` opzione:</span><span class="sxs-lookup"><span data-stu-id="47816-198">Now create hello pool, and specify hello package reference object as hello argument toohello `ApplicationPackageReferences` option:</span></span>

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

<span data-ttu-id="47816-199">È possibile trovare ulteriori informazioni sui pacchetti di applicazioni in [distribuire applicazioni toocompute nodi con i pacchetti di applicazione di Batch](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="47816-199">You can find more information on application packages in [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47816-200">È necessario [collegare un account di archiviazione di Azure](#linked-storage-account-autostorage) tooyour Batch account toouse pacchetti di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="47816-200">You must [link an Azure Storage account](#linked-storage-account-autostorage) tooyour Batch account toouse application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="47816-201">Aggiornare i pacchetti dell’applicazione di un pool</span><span class="sxs-lookup"><span data-stu-id="47816-201">Update a pool's application packages</span></span>
<span data-ttu-id="47816-202">applicazioni di hello tooupdate assegnate tooan pool esistente, creare innanzitutto un oggetto PSApplicationPackageReference con proprietà hello desiderato (Id pacchetto e la versione dell'applicazione):</span><span class="sxs-lookup"><span data-stu-id="47816-202">tooupdate hello applications assigned tooan existing pool, first create a PSApplicationPackageReference object with hello desired properties (application Id and package version):</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

<span data-ttu-id="47816-203">Successivamente, ottenere il pool di hello dal Batch, cancellare tutti i pacchetti esistenti, aggiungere il nuovo riferimento al pacchetto e aggiornare il servizio Batch hello con le nuove impostazioni del pool di hello:</span><span class="sxs-lookup"><span data-stu-id="47816-203">Next, get hello pool from Batch, clear out any existing packages, add our new package reference, and update hello Batch service with hello new pool settings:</span></span>

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

<span data-ttu-id="47816-204">Ora è effettuato l'aggiornamento delle proprietà del pool di hello nel servizio Batch hello.</span><span class="sxs-lookup"><span data-stu-id="47816-204">You've now updated hello pool's properties in hello Batch service.</span></span> <span data-ttu-id="47816-205">tooactually distribuire hello nuovo pacchetto toocompute nodi di applicazioni nel pool di hello, tuttavia, è necessario riavviare o ricreare l'immagine di tali nodi.</span><span class="sxs-lookup"><span data-stu-id="47816-205">tooactually deploy hello new application package toocompute nodes in hello pool, however, you must restart or reimage those nodes.</span></span> <span data-ttu-id="47816-206">È possibile riavviare ogni nodo di un pool con questo comando:</span><span class="sxs-lookup"><span data-stu-id="47816-206">You can restart every node in a pool with this command:</span></span>

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> <span data-ttu-id="47816-207">È possibile distribuire più applicazione pacchetti toohello nodi di calcolo in un pool.</span><span class="sxs-lookup"><span data-stu-id="47816-207">You can deploy multiple application packages toohello compute nodes in a pool.</span></span> <span data-ttu-id="47816-208">Se si desidera troppo*aggiungere* un pacchetto di applicazioni non sostituisce i pacchetti hello attualmente distribuita, omettere hello `$pool.ApplicationPackageReferences.Clear()` riga precedente.</span><span class="sxs-lookup"><span data-stu-id="47816-208">If you'd like too*add* an application package instead of replacing hello currently deployed packages, omit hello `$pool.ApplicationPackageReferences.Clear()` line above.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="47816-209">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="47816-209">Next steps</span></span>
* <span data-ttu-id="47816-210">Per la sintassi dettagliata ed esempi dei cmdlet, vedere le [informazioni di riferimento sui cmdlet per Azure Batch](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="47816-210">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>
* <span data-ttu-id="47816-211">Per ulteriori informazioni sulle applicazioni e pacchetti di applicazioni in Batch, vedere [distribuire applicazioni toocompute nodi con i pacchetti di applicazione di Batch](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="47816-211">For more information about applications and application packages in Batch, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/