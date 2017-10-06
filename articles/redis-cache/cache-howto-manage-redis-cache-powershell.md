---
title: Cache Redis di Azure con Azure PowerShell aaaManage | Documenti Microsoft
description: "Informazioni su come le attività amministrative di tooperform per Cache Redis di Azure con Azure PowerShell."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a><span data-ttu-id="3a856-103">Gestire Cache Redis di Azure con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a856-103">Manage Azure Redis Cache with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3a856-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a856-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="3a856-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="3a856-105">Azure CLI</span></span>](cache-manage-cli.md)
> 
> 

<span data-ttu-id="3a856-106">Questo argomento viene illustrato come tooperform comuni attività, ad esempio creare, aggiornare e ridimensionare le istanze di Cache Redis di Azure, come chiavi di accesso tooregenerate e come tooview informazioni delle cache.</span><span class="sxs-lookup"><span data-stu-id="3a856-106">This topic shows you how tooperform common tasks such as create, update, and scale your Azure Redis Cache instances, how tooregenerate access keys, and how tooview information about your caches.</span></span> <span data-ttu-id="3a856-107">Per un elenco completo dei cmdlet PowerShell di Cache Redis di Azure, vedere [Cmdlet di Cache Redis di Azure](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span><span class="sxs-lookup"><span data-stu-id="3a856-107">For a complete list of Azure Redis Cache PowerShell cmdlets, see [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="3a856-108">Per ulteriori informazioni sul modello di distribuzione classica hello, vedere [Azure Resource Manager e distribuzione classica: comprendere i modelli di distribuzione e lo stato delle risorse di hello](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span><span class="sxs-lookup"><span data-stu-id="3a856-108">For more information about hello classic deployment model, see [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a856-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3a856-109">Prerequisites</span></span>
<span data-ttu-id="3a856-110">Se è già installato PowerShell di Microsoft Azure, è necessario installare Azure PowerShell versione 1.0.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="3a856-110">If you have already installed Azure PowerShell, you must have Azure PowerShell version 1.0.0 or later.</span></span> <span data-ttu-id="3a856-111">È possibile controllare la versione hello di Azure PowerShell che è stato installato con questo comando al prompt dei comandi di Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="3a856-111">You can check hello version of Azure PowerShell that you have installed with this command at hello Azure PowerShell command prompt.</span></span>

    Get-Module azure | format-table version


<span data-ttu-id="3a856-112">In primo luogo, è necessario accedere tooAzure con questo comando.</span><span class="sxs-lookup"><span data-stu-id="3a856-112">First, you must log in tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="3a856-113">Specificare l'indirizzo di posta elettronica hello del proprio account Azure e la relativa password nella finestra di dialogo hello accesso di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3a856-113">Specify hello email address of your Azure account and its password in hello Microsoft Azure sign-in dialog.</span></span>

<span data-ttu-id="3a856-114">Successivamente, se si dispone di più sottoscrizioni di Azure, è necessario tooset la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a856-114">Next, if you have multiple Azure subscriptions, you need tooset your Azure subscription.</span></span> <span data-ttu-id="3a856-115">toosee un elenco delle sottoscrizioni correnti, eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="3a856-115">toosee a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="3a856-116">toospecify hello sottoscrizione eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="3a856-116">toospecify hello subscription, run hello following command.</span></span> <span data-ttu-id="3a856-117">Nell'esempio seguente di hello, nome della sottoscrizione hello è `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="3a856-117">In hello following example, hello subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

<span data-ttu-id="3a856-118">Prima di poter utilizzare Windows PowerShell con Gestione risorse di Azure, è necessario hello segue:</span><span class="sxs-lookup"><span data-stu-id="3a856-118">Before you can use Windows PowerShell with Azure Resource Manager, you need hello following:</span></span>

* <span data-ttu-id="3a856-119">Windows PowerShell, versione 3.0 o 4.0.</span><span class="sxs-lookup"><span data-stu-id="3a856-119">Windows PowerShell, Version 3.0 or 4.0.</span></span> <span data-ttu-id="3a856-120">versione di hello toofind di Windows PowerShell, digitare:`$PSVersionTable` e verificare il valore di hello `PSVersion` è 3.0 o 4.0.</span><span class="sxs-lookup"><span data-stu-id="3a856-120">toofind hello version of Windows PowerShell, type:`$PSVersionTable` and verify hello value of `PSVersion` is 3.0 or 4.0.</span></span> <span data-ttu-id="3a856-121">tooinstall una versione compatibile, vedere [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) o [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="3a856-121">tooinstall a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

<span data-ttu-id="3a856-122">tooget dettagliate della Guida per qualsiasi cmdlet che viene visualizzato in questa esercitazione, il cmdlet Get-Help hello di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="3a856-122">tooget detailed help for any cmdlet you see in this tutorial, use hello Get-Help cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="3a856-123">Ad esempio, la Guida di tooget per hello `New-AzureRmRedisCache` cmdlet, digitare:</span><span class="sxs-lookup"><span data-stu-id="3a856-123">For example, tooget help for hello `New-AzureRmRedisCache` cmdlet, type:</span></span>

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a><span data-ttu-id="3a856-124">Come tooconnect tooother cloud</span><span class="sxs-lookup"><span data-stu-id="3a856-124">How tooconnect tooother clouds</span></span>
<span data-ttu-id="3a856-125">Ambiente hello predefinito Azure è `AzureCloud`, che rappresenta hello istanza globale cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a856-125">By default hello Azure environment is `AzureCloud`, which represents hello global Azure cloud instance.</span></span> <span data-ttu-id="3a856-126">tooconnect tooa istanza diversa, utilizzare hello `Add-AzureRmAccount` con hello `-Environment` o -`EnvironmentName` opzione della riga di comando con l'ambiente desiderato hello o nome dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="3a856-126">tooconnect tooa different instance, use hello `Add-AzureRmAccount` command with hello `-Environment` or -`EnvironmentName` command line switch with hello desired environment or environment name.</span></span>

<span data-ttu-id="3a856-127">elenco di hello toosee degli ambienti disponibili, eseguire hello `Get-AzureRmEnvironment` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3a856-127">toosee hello list of available environments, run hello `Get-AzureRmEnvironment` cmdlet.</span></span>

### <a name="tooconnect-toohello-azure-government-cloud"></a><span data-ttu-id="3a856-128">tooconnect toohello Cloud di Azure per enti pubblici</span><span class="sxs-lookup"><span data-stu-id="3a856-128">tooconnect toohello Azure Government Cloud</span></span>
<span data-ttu-id="3a856-129">tooconnect toohello Cloud di Azure per enti pubblici, utilizzare uno dei seguenti comandi hello.</span><span class="sxs-lookup"><span data-stu-id="3a856-129">tooconnect toohello Azure Government Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

<span data-ttu-id="3a856-130">oppure</span><span class="sxs-lookup"><span data-stu-id="3a856-130">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

<span data-ttu-id="3a856-131">toocreate una cache di hello Cloud di Azure per enti pubblici, utilizzare una delle posizioni seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="3a856-131">toocreate a cache in hello Azure Government Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="3a856-132">Governo degli Stati Uniti - Virginia</span><span class="sxs-lookup"><span data-stu-id="3a856-132">USGov Virginia</span></span>
* <span data-ttu-id="3a856-133">Governo degli Stati Uniti - Iowa</span><span class="sxs-lookup"><span data-stu-id="3a856-133">USGov Iowa</span></span>

<span data-ttu-id="3a856-134">Per ulteriori informazioni su hello Cloud di Azure per enti pubblici, vedere [Microsoft Azure per enti pubblici](https://azure.microsoft.com/features/gov/) e [Guida per sviluppatori di Microsoft Azure per enti pubblici](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="3a856-134">For more information about hello Azure Government Cloud, see [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) and [Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>

### <a name="tooconnect-toohello-azure-china-cloud"></a><span data-ttu-id="3a856-135">tooconnect toohello Cloud Cina di Azure</span><span class="sxs-lookup"><span data-stu-id="3a856-135">tooconnect toohello Azure China Cloud</span></span>
<span data-ttu-id="3a856-136">tooconnect toohello Cloud Cina di Azure, utilizzare uno dei seguenti comandi hello.</span><span class="sxs-lookup"><span data-stu-id="3a856-136">tooconnect toohello Azure China Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

<span data-ttu-id="3a856-137">oppure</span><span class="sxs-lookup"><span data-stu-id="3a856-137">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

<span data-ttu-id="3a856-138">toocreate una cache di hello Cloud Cina di Azure, utilizzare una delle posizioni seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="3a856-138">toocreate a cache in hello Azure China Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="3a856-139">Cina orientale</span><span class="sxs-lookup"><span data-stu-id="3a856-139">China East</span></span>
* <span data-ttu-id="3a856-140">Cina settentrionale</span><span class="sxs-lookup"><span data-stu-id="3a856-140">China North</span></span>

<span data-ttu-id="3a856-141">Per ulteriori informazioni su hello Cloud Cina di Azure, vedere [AzureChinaCloud per Azure gestito da 21Vianet in Cina](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="3a856-141">For more information about hello Azure China Cloud, see [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span>

### <a name="tooconnect-toomicrosoft-azure-germany"></a><span data-ttu-id="3a856-142">tooconnect tooMicrosoft Azure in Germania</span><span class="sxs-lookup"><span data-stu-id="3a856-142">tooconnect tooMicrosoft Azure Germany</span></span>
<span data-ttu-id="3a856-143">tooconnect tooMicrosoft Azure in Germania, utilizzare uno dei seguenti comandi hello.</span><span class="sxs-lookup"><span data-stu-id="3a856-143">tooconnect tooMicrosoft Azure Germany, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


<span data-ttu-id="3a856-144">oppure</span><span class="sxs-lookup"><span data-stu-id="3a856-144">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

<span data-ttu-id="3a856-145">toocreate una cache in Microsoft Azure in Germania, utilizzare una delle posizioni seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="3a856-145">toocreate a cache in Microsoft Azure Germany, use one of hello following locations.</span></span>

* <span data-ttu-id="3a856-146">Germania centrale</span><span class="sxs-lookup"><span data-stu-id="3a856-146">Germany Central</span></span>
* <span data-ttu-id="3a856-147">Germania nord-orientale</span><span class="sxs-lookup"><span data-stu-id="3a856-147">Germany Northeast</span></span>

<span data-ttu-id="3a856-148">Per altre informazioni su Microsoft Azure Germania, vedere [Microsoft Azure Germania](https://azure.microsoft.com/overview/clouds/germany/).</span><span class="sxs-lookup"><span data-stu-id="3a856-148">For more information about Microsoft Azure Germany, see [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span></span>

### <a name="properties-used-for-azure-redis-cache-powershell"></a><span data-ttu-id="3a856-149">Proprietà usate per PowerShell nella Cache Redis di Azure </span><span class="sxs-lookup"><span data-stu-id="3a856-149">Properties used for Azure Redis Cache PowerShell</span></span>
<span data-ttu-id="3a856-150">Hello nella tabella seguente contiene le proprietà e le descrizioni per i parametri utilizzati durante la creazione e gestire le istanze di Cache Redis di Azure con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3a856-150">hello following table contains properties and descriptions for commonly used parameters when creating and managing your Azure Redis Cache instances using Azure PowerShell.</span></span>

| <span data-ttu-id="3a856-151">.</span><span class="sxs-lookup"><span data-stu-id="3a856-151">Parameter</span></span> | <span data-ttu-id="3a856-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3a856-152">Description</span></span> | <span data-ttu-id="3a856-153">Default</span><span class="sxs-lookup"><span data-stu-id="3a856-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a856-154">Nome</span><span class="sxs-lookup"><span data-stu-id="3a856-154">Name</span></span> |<span data-ttu-id="3a856-155">Nome della cache di hello</span><span class="sxs-lookup"><span data-stu-id="3a856-155">Name of hello cache</span></span> | |
| <span data-ttu-id="3a856-156">Percorso</span><span class="sxs-lookup"><span data-stu-id="3a856-156">Location</span></span> |<span data-ttu-id="3a856-157">Percorso della cache di hello</span><span class="sxs-lookup"><span data-stu-id="3a856-157">Location of hello cache</span></span> | |
| <span data-ttu-id="3a856-158">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="3a856-158">ResourceGroupName</span></span> |<span data-ttu-id="3a856-159">Nome gruppo di risorse nella cache di hello quali toocreate</span><span class="sxs-lookup"><span data-stu-id="3a856-159">Resource group name in which toocreate hello cache</span></span> | |
| <span data-ttu-id="3a856-160">Dimensione</span><span class="sxs-lookup"><span data-stu-id="3a856-160">Size</span></span> |<span data-ttu-id="3a856-161">dimensione Hello della cache di hello.</span><span class="sxs-lookup"><span data-stu-id="3a856-161">hello size of hello cache.</span></span> <span data-ttu-id="3a856-162">I valori validi sono: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250 MB, 1 GB, 2,5 GB, 6 GB, 13 GB, 26 GB, 53 GB</span><span class="sxs-lookup"><span data-stu-id="3a856-162">Valid values are: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span></span> |<span data-ttu-id="3a856-163">1 GB</span><span class="sxs-lookup"><span data-stu-id="3a856-163">1GB</span></span> |
| <span data-ttu-id="3a856-164">ShardCount</span><span class="sxs-lookup"><span data-stu-id="3a856-164">ShardCount</span></span> |<span data-ttu-id="3a856-165">numero di Hello di partizioni toocreate quando si crea una cache premium con clustering abilitato.</span><span class="sxs-lookup"><span data-stu-id="3a856-165">hello number of shards toocreate when creating a premium cache with clustering enabled.</span></span> <span data-ttu-id="3a856-166">I valori validi sono: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span><span class="sxs-lookup"><span data-stu-id="3a856-166">Valid values are: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span></span> | |
| <span data-ttu-id="3a856-167">SKU</span><span class="sxs-lookup"><span data-stu-id="3a856-167">SKU</span></span> |<span data-ttu-id="3a856-168">Specifica hello SKU della cache di hello.</span><span class="sxs-lookup"><span data-stu-id="3a856-168">Specifies hello SKU of hello cache.</span></span> <span data-ttu-id="3a856-169">I valori validi sono: Basic, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="3a856-169">Valid values are: Basic, Standard, Premium</span></span> |<span data-ttu-id="3a856-170">Standard</span><span class="sxs-lookup"><span data-stu-id="3a856-170">Standard</span></span> |
| <span data-ttu-id="3a856-171">RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="3a856-171">RedisConfiguration</span></span> |<span data-ttu-id="3a856-172">Specifica le impostazioni di configurazione di Redis.</span><span class="sxs-lookup"><span data-stu-id="3a856-172">Specifies Redis configuration settings.</span></span> <span data-ttu-id="3a856-173">Per informazioni dettagliate su ogni impostazione, vedere l'esempio hello [RedisConfiguration proprietà](#redisconfiguration-properties) tabella.</span><span class="sxs-lookup"><span data-stu-id="3a856-173">For details on each setting, see hello following [RedisConfiguration properties](#redisconfiguration-properties) table.</span></span> | |
| <span data-ttu-id="3a856-174">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="3a856-174">EnableNonSslPort</span></span> |<span data-ttu-id="3a856-175">Indica se la porta non SSL hello è abilitata.</span><span class="sxs-lookup"><span data-stu-id="3a856-175">Indicates whether hello non-SSL port is enabled.</span></span> |<span data-ttu-id="3a856-176">False</span><span class="sxs-lookup"><span data-stu-id="3a856-176">False</span></span> |
| <span data-ttu-id="3a856-177">MaxMemoryPolicy</span><span class="sxs-lookup"><span data-stu-id="3a856-177">MaxMemoryPolicy</span></span> |<span data-ttu-id="3a856-178">Questo parametro è stato deprecato, usare invece RedisConfiguration.</span><span class="sxs-lookup"><span data-stu-id="3a856-178">This parameter has been deprecated - use RedisConfiguration instead.</span></span> | |
| <span data-ttu-id="3a856-179">StaticIP</span><span class="sxs-lookup"><span data-stu-id="3a856-179">StaticIP</span></span> |<span data-ttu-id="3a856-180">Quando si ospita la cache in una rete virtuale, specifica l'indirizzo IP nella subnet hello per cache di hello.</span><span class="sxs-lookup"><span data-stu-id="3a856-180">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="3a856-181">Se omesso, automaticamente dalla subnet hello viene scelto uno.</span><span class="sxs-lookup"><span data-stu-id="3a856-181">If not provided, one is chosen for you from hello subnet.</span></span> | |
| <span data-ttu-id="3a856-182">Subnet</span><span class="sxs-lookup"><span data-stu-id="3a856-182">Subnet</span></span> |<span data-ttu-id="3a856-183">Quando si ospita la cache in una rete virtuale, specifica il nome di hello della subnet hello nella cache di hello quali toodeploy.</span><span class="sxs-lookup"><span data-stu-id="3a856-183">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="3a856-184">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="3a856-184">VirtualNetwork</span></span> |<span data-ttu-id="3a856-185">Quando si ospita la cache in una rete virtuale, specifica l'ID della risorsa hello hello rete virtuale nella cache di hello quali toodeploy.</span><span class="sxs-lookup"><span data-stu-id="3a856-185">When hosting your cache in a VNET, specifies hello resource ID of hello VNET in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="3a856-186">KeyType</span><span class="sxs-lookup"><span data-stu-id="3a856-186">KeyType</span></span> |<span data-ttu-id="3a856-187">Specifica la chiave di accesso tooregenerate durante il rinnovo di chiavi di accesso.</span><span class="sxs-lookup"><span data-stu-id="3a856-187">Specifies which access key tooregenerate when renewing access keys.</span></span> <span data-ttu-id="3a856-188">Valori validi: Primario, Secondario</span><span class="sxs-lookup"><span data-stu-id="3a856-188">Valid values are: Primary, Secondary</span></span> | |

### <a name="redisconfiguration-properties"></a><span data-ttu-id="3a856-189">Proprietà di RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="3a856-189">RedisConfiguration properties</span></span>
| <span data-ttu-id="3a856-190">Proprietà</span><span class="sxs-lookup"><span data-stu-id="3a856-190">Property</span></span> | <span data-ttu-id="3a856-191">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3a856-191">Description</span></span> | <span data-ttu-id="3a856-192">Piani tariffari</span><span class="sxs-lookup"><span data-stu-id="3a856-192">Pricing tiers</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a856-193">rdb-backup-enabled</span><span class="sxs-lookup"><span data-stu-id="3a856-193">rdb-backup-enabled</span></span> |<span data-ttu-id="3a856-194">Indica se la [persistenza dei dati Redis](cache-how-to-premium-persistence.md) è abilitata</span><span class="sxs-lookup"><span data-stu-id="3a856-194">Whether [Redis data persistence](cache-how-to-premium-persistence.md) is enabled</span></span> |<span data-ttu-id="3a856-195">Solo Premium</span><span class="sxs-lookup"><span data-stu-id="3a856-195">Premium only</span></span> |
| <span data-ttu-id="3a856-196">rdb-storage-connection-string</span><span class="sxs-lookup"><span data-stu-id="3a856-196">rdb-storage-connection-string</span></span> |<span data-ttu-id="3a856-197">account di archiviazione toohello di stringa di connessione per Hello [Redis persistenza dei dati](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="3a856-197">hello connection string toohello storage account for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="3a856-198">Solo Premium</span><span class="sxs-lookup"><span data-stu-id="3a856-198">Premium only</span></span> |
| <span data-ttu-id="3a856-199">rdb-backup-frequency</span><span class="sxs-lookup"><span data-stu-id="3a856-199">rdb-backup-frequency</span></span> |<span data-ttu-id="3a856-200">frequenza di backup per Hello [Redis persistenza dei dati](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="3a856-200">hello backup frequency for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="3a856-201">Solo Premium</span><span class="sxs-lookup"><span data-stu-id="3a856-201">Premium only</span></span> |
| <span data-ttu-id="3a856-202">maxmemory-reserved</span><span class="sxs-lookup"><span data-stu-id="3a856-202">maxmemory-reserved</span></span> |<span data-ttu-id="3a856-203">Configura hello [memoria riservata](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) per i processi non cache</span><span class="sxs-lookup"><span data-stu-id="3a856-203">Configures hello [memory reserved](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for non-cache processes</span></span> |<span data-ttu-id="3a856-204">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="3a856-204">Standard and Premium</span></span> |
| <span data-ttu-id="3a856-205">maxmemory-policy</span><span class="sxs-lookup"><span data-stu-id="3a856-205">maxmemory-policy</span></span> |<span data-ttu-id="3a856-206">Configura hello [criteri di rimozione](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) per cache di hello</span><span class="sxs-lookup"><span data-stu-id="3a856-206">Configures hello [eviction policy](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for hello cache</span></span> |<span data-ttu-id="3a856-207">Tutti i piani tariffari</span><span class="sxs-lookup"><span data-stu-id="3a856-207">All pricing tiers</span></span> |
| <span data-ttu-id="3a856-208">notify-keyspace-events</span><span class="sxs-lookup"><span data-stu-id="3a856-208">notify-keyspace-events</span></span> |<span data-ttu-id="3a856-209">Configura le [notifiche keyspace](cache-configure.md#keyspace-notifications-advanced-settings)</span><span class="sxs-lookup"><span data-stu-id="3a856-209">Configures [keyspace notifications](cache-configure.md#keyspace-notifications-advanced-settings)</span></span> |<span data-ttu-id="3a856-210">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="3a856-210">Standard and Premium</span></span> |
| <span data-ttu-id="3a856-211">hash-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="3a856-211">hash-max-ziplist-entries</span></span> |<span data-ttu-id="3a856-212">Configura l' [ottimizzazione della memoria](http://redis.io/topics/memory-optimization) per tipi di dati aggregati di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="3a856-212">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3a856-213">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="3a856-213">Standard and Premium</span></span> |
| <span data-ttu-id="3a856-214">hash-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="3a856-214">hash-max-ziplist-value</span></span> |<span data-ttu-id="3a856-215">Configura l' [ottimizzazione della memoria](http://redis.io/topics/memory-optimization) per tipi di dati aggregati di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="3a856-215">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3a856-216">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="3a856-216">Standard and Premium</span></span> |
| <span data-ttu-id="3a856-217">set-max-intset-entries</span><span class="sxs-lookup"><span data-stu-id="3a856-217">set-max-intset-entries</span></span> |<span data-ttu-id="3a856-218">Configura l' [ottimizzazione della memoria](http://redis.io/topics/memory-optimization) per tipi di dati aggregati di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="3a856-218">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3a856-219">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="3a856-219">Standard and Premium</span></span> |
| <span data-ttu-id="3a856-220">zset-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="3a856-220">zset-max-ziplist-entries</span></span> |<span data-ttu-id="3a856-221">Configura l' [ottimizzazione della memoria](http://redis.io/topics/memory-optimization) per tipi di dati aggregati di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="3a856-221">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3a856-222">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="3a856-222">Standard and Premium</span></span> |
| <span data-ttu-id="3a856-223">zset-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="3a856-223">zset-max-ziplist-value</span></span> |<span data-ttu-id="3a856-224">Configura l' [ottimizzazione della memoria](http://redis.io/topics/memory-optimization) per tipi di dati aggregati di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="3a856-224">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3a856-225">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="3a856-225">Standard and Premium</span></span> |
| <span data-ttu-id="3a856-226">database</span><span class="sxs-lookup"><span data-stu-id="3a856-226">databases</span></span> |<span data-ttu-id="3a856-227">Configura il numero di hello di database.</span><span class="sxs-lookup"><span data-stu-id="3a856-227">Configures hello number of databases.</span></span> <span data-ttu-id="3a856-228">Questa proprietà può essere configurata solo durante la creazione della cache.</span><span class="sxs-lookup"><span data-stu-id="3a856-228">This property can be configured only at cache creation.</span></span> |<span data-ttu-id="3a856-229">Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="3a856-229">Standard and Premium</span></span> |

## <a name="toocreate-a-redis-cache"></a><span data-ttu-id="3a856-230">toocreate una Cache Redis</span><span class="sxs-lookup"><span data-stu-id="3a856-230">toocreate a Redis Cache</span></span>
<span data-ttu-id="3a856-231">Le nuove istanze di Cache Redis di Azure vengono create utilizzando hello [New AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3a856-231">New Azure Redis Cache instances are created using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3a856-232">Hello prima volta che si crea una cache Redis in una sottoscrizione utilizzando il portale di Azure, hello portale hello registra hello `Microsoft.Cache` dello spazio dei nomi per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3a856-232">hello first time you create a Redis cache in a subscription using hello Azure portal, hello portal registers hello `Microsoft.Cache` namespace for that subscription.</span></span> <span data-ttu-id="3a856-233">Se si tenta hello toocreate innanzitutto Redis cache in una sottoscrizione tramite PowerShell, è innanzitutto necessario registrare tale spazio dei nomi utilizzando hello comando; seguente i cmdlet in caso contrario, ad esempio `New-AzureRmRedisCache` e `Get-AzureRmRedisCache` esito negativo.</span><span class="sxs-lookup"><span data-stu-id="3a856-233">If you attempt toocreate hello first Redis cache in a subscription using PowerShell, you must first register that namespace using hello following command; otherwise cmdlets such as `New-AzureRmRedisCache` and `Get-AzureRmRedisCache` fail.</span></span>
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

<span data-ttu-id="3a856-234">un elenco dei parametri disponibili e le relative descrizioni per toosee `New-AzureRmRedisCache`, eseguire hello il seguente comando.</span><span class="sxs-lookup"><span data-stu-id="3a856-234">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3a856-235">toocreate una cache con i parametri predefiniti, eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="3a856-235">toocreate a cache with default parameters, run hello following command.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

<span data-ttu-id="3a856-236">`ResourceGroupName`, `Name`, e `Location` sono parametri obbligatori, ma il resto di hello sono facoltativo e includono i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="3a856-236">`ResourceGroupName`, `Name`, and `Location` are required parameters, but hello rest are optional and have default values.</span></span> <span data-ttu-id="3a856-237">Esecuzione hello precedente comando crea un'istanza di Cache Redis Azure SKU Standard con nome specificato hello, percorso e il gruppo di risorse, da 1 GB di dimensioni con la porta non SSL hello disabilitata.</span><span class="sxs-lookup"><span data-stu-id="3a856-237">Running hello previous command creates a Standard SKU Azure Redis Cache instance with hello specified name, location, and resource group, that is 1 GB in size with hello non-SSL port disabled.</span></span>

<span data-ttu-id="3a856-238">toocreate una cache premium, specificare una dimensione di P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), o P4 (53 GB - 530 GB).</span><span class="sxs-lookup"><span data-stu-id="3a856-238">toocreate a premium cache, specify a size of P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), or P4 (53 GB - 530 GB).</span></span> <span data-ttu-id="3a856-239">tooenable clustering, specificare un numero di partizioni utilizzando hello `ShardCount` parametro.</span><span class="sxs-lookup"><span data-stu-id="3a856-239">tooenable clustering, specify a shard count using hello `ShardCount` parameter.</span></span> <span data-ttu-id="3a856-240">Hello esempio seguente viene creata una cache premium P1 con 3 partizioni.</span><span class="sxs-lookup"><span data-stu-id="3a856-240">hello following example creates a P1 premium cache with 3 shards.</span></span> <span data-ttu-id="3a856-241">Una cache premium P1 è 6 GB di dimensioni e poiché sono state specificate tre partizioni hello dimensione totale è 18 GB (3 x 6 GB).</span><span class="sxs-lookup"><span data-stu-id="3a856-241">A P1 premium cache is 6 GB in size, and since we specified three shards hello total size is 18 GB (3 x 6 GB).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

<span data-ttu-id="3a856-242">i valori toospecify per hello `RedisConfiguration` parametro, racchiudere i valori hello `{}` come chiave/valore come coppie `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span><span class="sxs-lookup"><span data-stu-id="3a856-242">toospecify values for hello `RedisConfiguration` parameter, enclose hello values inside `{}` as key/value pairs like `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span></span> <span data-ttu-id="3a856-243">esempio Hello crea una cache standard di 1 GB con `allkeys-random` le notifiche di spazio delle chiavi e i criteri di maxmemory configurate con `KEA`.</span><span class="sxs-lookup"><span data-stu-id="3a856-243">hello following example creates a standard 1 GB cache with `allkeys-random` maxmemory policy and keyspace notifications configured with `KEA`.</span></span> <span data-ttu-id="3a856-244">Per altre informazioni, vedere [Notifiche di Keyspace (impostazioni avanzate)](cache-configure.md#keyspace-notifications-advanced-settings) e [Criteri per la memoria](cache-configure.md#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="3a856-244">For more information, see [Keyspace notifications (advanced settings)](cache-configure.md#keyspace-notifications-advanced-settings) and [Memory policies](cache-configure.md#memory-policies).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a><span data-ttu-id="3a856-245">database hello tooconfigure impostazione durante la creazione della cache</span><span class="sxs-lookup"><span data-stu-id="3a856-245">tooconfigure hello databases setting during cache creation</span></span>
<span data-ttu-id="3a856-246">Hello `databases` impostazione può essere configurata solo durante la creazione della cache.</span><span class="sxs-lookup"><span data-stu-id="3a856-246">hello `databases` setting can be configured only during cache creation.</span></span> <span data-ttu-id="3a856-247">esempio Hello crea P3 premium (26 GB) di cache con i 48 database utilizzando hello [New AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3a856-247">hello following example creates a premium P3 (26 GB) cache with 48 databases using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

<span data-ttu-id="3a856-248">Per ulteriori informazioni su hello `databases` proprietà, vedere [configurazione server di Cache Redis di Azure predefinito](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="3a856-248">For more information on hello `databases` property, see [Default Azure Redis Cache server configuration](cache-configure.md#default-redis-server-configuration).</span></span> <span data-ttu-id="3a856-249">Per ulteriori informazioni sulla creazione di una cache di hello [New AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, vedere hello precedente [toocreate una Cache Redis](#to-create-a-redis-cache) sezione.</span><span class="sxs-lookup"><span data-stu-id="3a856-249">For more information on creating a cache using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, see hello previous [toocreate a Redis Cache](#to-create-a-redis-cache) section.</span></span>

## <a name="tooupdate-a-redis-cache"></a><span data-ttu-id="3a856-250">tooupdate una cache Redis</span><span class="sxs-lookup"><span data-stu-id="3a856-250">tooupdate a Redis cache</span></span>
<span data-ttu-id="3a856-251">Istanze di Cache Redis di Azure vengono aggiornate utilizzando hello [Set AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3a856-251">Azure Redis Cache instances are updated using hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span></span>

<span data-ttu-id="3a856-252">un elenco dei parametri disponibili e le relative descrizioni per toosee `Set-AzureRmRedisCache`, eseguire hello il seguente comando.</span><span class="sxs-lookup"><span data-stu-id="3a856-252">toosee a list of available parameters and their descriptions for `Set-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3a856-253">Hello `Set-AzureRmRedisCache` cmdlet può essere utilizzato tooupdate proprietà, ad esempio `Size`, `Sku`, `EnableNonSslPort`, hello e `RedisConfiguration` valori.</span><span class="sxs-lookup"><span data-stu-id="3a856-253">hello `Set-AzureRmRedisCache` cmdlet can be used tooupdate properties such as `Size`, `Sku`, `EnableNonSslPort`, and hello `RedisConfiguration` values.</span></span> 

<span data-ttu-id="3a856-254">Hello il comando seguente aggiornamenti hello criteri di maxmemory per Cache Redis hello denominato myCache.</span><span class="sxs-lookup"><span data-stu-id="3a856-254">hello following command updates hello maxmemory-policy for hello Redis Cache named myCache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a><span data-ttu-id="3a856-255">tooscale una cache Redis</span><span class="sxs-lookup"><span data-stu-id="3a856-255">tooscale a Redis cache</span></span>
<span data-ttu-id="3a856-256">`Set-AzureRmRedisCache`può essere un'istanza di cache Redis di Azure quando hello tooscale utilizzati `Size`, `Sku`, o `ShardCount` si modificano le proprietà.</span><span class="sxs-lookup"><span data-stu-id="3a856-256">`Set-AzureRmRedisCache` can be used tooscale an Azure Redis cache instance when hello `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> 

> [!NOTE]
> <span data-ttu-id="3a856-257">Scalabilità di una cache tramite PowerShell, è soggetto toohello stessi limiti e alle linee guida di scalabilità di una cache di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a856-257">Scaling a cache using PowerShell is subject toohello same limits and guidelines as scaling a cache from hello Azure portal.</span></span> <span data-ttu-id="3a856-258">È possibile ridimensionare tooa diverso livello di prezzo con hello seguenti restrizioni.</span><span class="sxs-lookup"><span data-stu-id="3a856-258">You can scale tooa different pricing tier with hello following restrictions.</span></span>
> 
> * <span data-ttu-id="3a856-259">Non è possibile scalare da un piano tariffario superiore tooa livello inferiore a livello di prezzo.</span><span class="sxs-lookup"><span data-stu-id="3a856-259">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
> * <span data-ttu-id="3a856-260">Non è possibile scalare da un **Premium** cache verso il basso tooa **Standard** o **base** della cache.</span><span class="sxs-lookup"><span data-stu-id="3a856-260">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
> * <span data-ttu-id="3a856-261">Non è possibile scalare da un **Standard** cache verso il basso tooa **base** della cache.</span><span class="sxs-lookup"><span data-stu-id="3a856-261">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
> * <span data-ttu-id="3a856-262">È possibile scalare da un **base** cache tooa **Standard** cache ma è Impossibile modificare la dimensione di hello in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="3a856-262">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="3a856-263">Se è necessario dimensioni diverse, è possibile eseguire una successiva dimensione toohello desiderato operazione.</span><span class="sxs-lookup"><span data-stu-id="3a856-263">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
> * <span data-ttu-id="3a856-264">Non è possibile scalare da un **base** memorizzare nella cache direttamente tooa **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="3a856-264">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="3a856-265">È necessario applicare la scalabilità da **base** troppo**Standard** in un'unica operazione di ridimensionamento e quindi da **Standard** troppo**Premium** una scalabilità successivi operazione.</span><span class="sxs-lookup"><span data-stu-id="3a856-265">You must scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
> * <span data-ttu-id="3a856-266">Non è possibile scalare da una dimensione maggiore verso il basso toohello **C0 (250 MB)** dimensioni.</span><span class="sxs-lookup"><span data-stu-id="3a856-266">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>
> 
> <span data-ttu-id="3a856-267">Per ulteriori informazioni, vedere [la modalità di Cache Redis di Azure di tooScale](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="3a856-267">For more information, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>
> 
> 

<span data-ttu-id="3a856-268">Hello esempio seguente viene illustrato come tooscale una cache denominata `myCache` tooa 2,5 GB cache.</span><span class="sxs-lookup"><span data-stu-id="3a856-268">hello following example shows how tooscale a cache named `myCache` tooa 2.5 GB cache.</span></span> <span data-ttu-id="3a856-269">Si noti che questo comando funziona sia con una cache Basic che una cache Standard.</span><span class="sxs-lookup"><span data-stu-id="3a856-269">Note that this command works for both a Basic or a Standard cache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="3a856-270">Dopo che viene eseguito questo comando, viene restituito lo stato di hello della cache di hello (simile toocalling `Get-AzureRmRedisCache`).</span><span class="sxs-lookup"><span data-stu-id="3a856-270">After this command is issued, hello status of hello cache is returned (similar toocalling `Get-AzureRmRedisCache`).</span></span> <span data-ttu-id="3a856-271">Si noti che hello `ProvisioningState` è `Scaling`.</span><span class="sxs-lookup"><span data-stu-id="3a856-271">Note that hello `ProvisioningState` is `Scaling`.</span></span>

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

<span data-ttu-id="3a856-272">Una volta completata l'operazione di ridimensionamento hello, hello `ProvisioningState` cambia troppo`Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="3a856-272">When hello scaling operation is complete, hello `ProvisioningState` changes too`Succeeded`.</span></span> <span data-ttu-id="3a856-273">Se è necessario toomake un'operazione di ridimensionamento successiva, ad esempio la modifica da tooStandard base e quindi modifica la dimensione di hello, è necessario attendere hello precedente operazione è stata completata o viene visualizzato un seguente toohello simile di errore.</span><span class="sxs-lookup"><span data-stu-id="3a856-273">If you need toomake a subsequent scaling operation, such as changing from Basic tooStandard and then changing hello size, you must wait until hello previous operation is complete or you receive an error similar toohello following.</span></span>

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a><span data-ttu-id="3a856-274">informazioni tooget su una cache Redis</span><span class="sxs-lookup"><span data-stu-id="3a856-274">tooget information about a Redis cache</span></span>
<span data-ttu-id="3a856-275">È possibile recuperare informazioni su una cache di hello [Get AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3a856-275">You can retrieve information about a cache using hello [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span></span>

<span data-ttu-id="3a856-276">un elenco dei parametri disponibili e le relative descrizioni per toosee `Get-AzureRmRedisCache`, eseguire hello il seguente comando.</span><span class="sxs-lookup"><span data-stu-id="3a856-276">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3a856-277">informazioni tooreturn su tutte le cache nella sottoscrizione corrente hello, eseguire `Get-AzureRmRedisCache` senza parametri.</span><span class="sxs-lookup"><span data-stu-id="3a856-277">tooreturn information about all caches in hello current subscription, run `Get-AzureRmRedisCache` without any parameters.</span></span>

    Get-AzureRmRedisCache

<span data-ttu-id="3a856-278">informazioni tooreturn su tutte le cache in un gruppo di risorse specifico, eseguire `Get-AzureRmRedisCache` con hello `ResourceGroupName` parametro.</span><span class="sxs-lookup"><span data-stu-id="3a856-278">tooreturn information about all caches in a specific resource group, run `Get-AzureRmRedisCache` with hello `ResourceGroupName` parameter.</span></span>

    Get-AzureRmRedisCache -ResourceGroupName myGroup

<span data-ttu-id="3a856-279">informazioni tooreturn su una cache specifica, eseguire `Get-AzureRmRedisCache` con hello `Name` parametro contenente il nome di hello della cache di hello e hello `ResourceGroupName` parametro con il gruppo di risorse hello contenente tale cache.</span><span class="sxs-lookup"><span data-stu-id="3a856-279">tooreturn information about a specific cache, run `Get-AzureRmRedisCache` with hello `Name` parameter containing hello name of hello cache, and hello `ResourceGroupName` parameter with hello resource group containing that cache.</span></span>

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a><span data-ttu-id="3a856-280">chiavi di accesso di hello tooretrieve per una cache Redis</span><span class="sxs-lookup"><span data-stu-id="3a856-280">tooretrieve hello access keys for a Redis cache</span></span>
<span data-ttu-id="3a856-281">tooretrieve hello tasti di scelta per la cache, è possibile utilizzare hello [Get AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3a856-281">tooretrieve hello access keys for your cache, you can use hello [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span></span>

<span data-ttu-id="3a856-282">un elenco dei parametri disponibili e le relative descrizioni per toosee `Get-AzureRmRedisCacheKey`, eseguire hello il seguente comando.</span><span class="sxs-lookup"><span data-stu-id="3a856-282">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3a856-283">hello tooretrieve chiavi per la cache, chiamata hello `Get-AzureRmRedisCacheKey` cmdlet e passare il nome di hello della cache di hello Nome hello del gruppo di risorse che contiene una cache di hello.</span><span class="sxs-lookup"><span data-stu-id="3a856-283">tooretrieve hello keys for your cache, call hello `Get-AzureRmRedisCacheKey` cmdlet and pass in hello name of your cache hello name of hello resource group that contains hello cache.</span></span>

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a><span data-ttu-id="3a856-284">tooregenerate chiavi di accesso per la cache Redis</span><span class="sxs-lookup"><span data-stu-id="3a856-284">tooregenerate access keys for your Redis cache</span></span>
<span data-ttu-id="3a856-285">tooregenerate hello tasti di scelta per la cache, è possibile utilizzare hello [New AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3a856-285">tooregenerate hello access keys for your cache, you can use hello [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span></span>

<span data-ttu-id="3a856-286">un elenco dei parametri disponibili e le relative descrizioni per toosee `New-AzureRmRedisCacheKey`, eseguire hello il seguente comando.</span><span class="sxs-lookup"><span data-stu-id="3a856-286">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3a856-287">chiave tooregenerate hello primaria o secondaria per la cache, chiamata hello `New-AzureRmRedisCacheKey` cmdlet e passare hello nome, il gruppo di risorse e specificare il parametro `Primary` o `Secondary` per hello `KeyType` parametro.</span><span class="sxs-lookup"><span data-stu-id="3a856-287">tooregenerate hello primary or secondary key for your cache, call hello `New-AzureRmRedisCacheKey` cmdlet and pass in hello name, resource group, and specify either `Primary` or `Secondary` for hello `KeyType` parameter.</span></span> <span data-ttu-id="3a856-288">Nell'esempio seguente di hello, chiave di accesso secondaria hello per una cache viene rigenerato.</span><span class="sxs-lookup"><span data-stu-id="3a856-288">In hello following example, hello secondary access key for a cache is regenerated.</span></span>

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a><span data-ttu-id="3a856-289">toodelete una cache Redis</span><span class="sxs-lookup"><span data-stu-id="3a856-289">toodelete a Redis cache</span></span>
<span data-ttu-id="3a856-290">toodelete una cache Redis, utilizzare hello [Remove AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3a856-290">toodelete a Redis cache, use hello [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span></span>

<span data-ttu-id="3a856-291">un elenco dei parametri disponibili e le relative descrizioni per toosee `Remove-AzureRmRedisCache`, eseguire hello il seguente comando.</span><span class="sxs-lookup"><span data-stu-id="3a856-291">toosee a list of available parameters and their descriptions for `Remove-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3a856-292">Nell'esempio seguente di hello, hello cache denominata `myCache` viene rimosso.</span><span class="sxs-lookup"><span data-stu-id="3a856-292">In hello following example, hello cache named `myCache` is removed.</span></span>

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a><span data-ttu-id="3a856-293">tooimport una cache Redis</span><span class="sxs-lookup"><span data-stu-id="3a856-293">tooimport a Redis cache</span></span>
<span data-ttu-id="3a856-294">È possibile importare dati in un'istanza di Cache Redis di Azure utilizzando hello `Import-AzureRmRedisCache` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3a856-294">You can import data into an Azure Redis Cache instance using hello `Import-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3a856-295">La funzionalità Importazione/Esportazione è disponibile solo per le cache del [piano Premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="3a856-295">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="3a856-296">Per altre informazioni sull'importazione/esportazione, vedere [Importare ed esportare dati in Cache Redis di Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="3a856-296">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="3a856-297">un elenco dei parametri disponibili e le relative descrizioni per toosee `Import-AzureRmRedisCache`, eseguire hello il seguente comando.</span><span class="sxs-lookup"><span data-stu-id="3a856-297">toosee a list of available parameters and their descriptions for `Import-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="3a856-298">Hello comando riportato di seguito Importa i dati da blob hello specificato dall'uri di firma di accesso condiviso hello in Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a856-298">hello following command imports data from hello blob specified by hello SAS uri into Azure Redis Cache.</span></span>

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a><span data-ttu-id="3a856-299">tooexport una cache Redis</span><span class="sxs-lookup"><span data-stu-id="3a856-299">tooexport a Redis cache</span></span>
<span data-ttu-id="3a856-300">È possibile esportare dati da un'istanza di Cache Redis di Azure utilizzando hello `Export-AzureRmRedisCache` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3a856-300">You can export data from an Azure Redis Cache instance using hello `Export-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3a856-301">La funzionalità Importazione/Esportazione è disponibile solo per le cache del [piano Premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="3a856-301">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="3a856-302">Per altre informazioni sull'importazione/esportazione, vedere [Importare ed esportare dati in Cache Redis di Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="3a856-302">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="3a856-303">un elenco dei parametri disponibili e le relative descrizioni per toosee `Export-AzureRmRedisCache`, eseguire hello il seguente comando.</span><span class="sxs-lookup"><span data-stu-id="3a856-303">toosee a list of available parameters and their descriptions for `Export-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="3a856-304">Hello seguente comando Esporta i dati da un'istanza di Cache Redis di Azure in contenitore hello specificato dall'uri SAS hello.</span><span class="sxs-lookup"><span data-stu-id="3a856-304">hello following command exports data from an Azure Redis Cache instance into hello container specified by hello SAS uri.</span></span>

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a><span data-ttu-id="3a856-305">tooreboot una cache Redis</span><span class="sxs-lookup"><span data-stu-id="3a856-305">tooreboot a Redis cache</span></span>
<span data-ttu-id="3a856-306">È possibile riavviare l'istanza di Cache Redis di Azure utilizzando hello `Reset-AzureRmRedisCache` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3a856-306">You can reboot your Azure Redis Cache instance using hello `Reset-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3a856-307">La funzionalità di riavvio è disponibile solo per le cache del [piano Premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="3a856-307">Reboot is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="3a856-308">Per altre informazioni sul riavvio della cache, vedere [Come amministrare Cache Redis di Azure - Riavviare](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="3a856-308">For more information about rebooting your cache, see [Cache administration - reboot](cache-administration.md#reboot).</span></span>
> 
> 

<span data-ttu-id="3a856-309">un elenco dei parametri disponibili e le relative descrizioni per toosee `Reset-AzureRmRedisCache`, eseguire hello il seguente comando.</span><span class="sxs-lookup"><span data-stu-id="3a856-309">toosee a list of available parameters and their descriptions for `Reset-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="3a856-310">il comando seguente Hello riavvia entrambi i nodi di hello specificato della cache.</span><span class="sxs-lookup"><span data-stu-id="3a856-310">hello following command reboots both nodes of hello specified cache.</span></span>

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a><span data-ttu-id="3a856-311">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3a856-311">Next steps</span></span>
<span data-ttu-id="3a856-312">toolearn ulteriori informazioni sull'utilizzo di Windows PowerShell con Azure, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="3a856-312">toolearn more about using Windows PowerShell with Azure, see hello following resources:</span></span>

* [<span data-ttu-id="3a856-313">Documentazione del cmdlet della cache Redis di Azure su MSDN</span><span class="sxs-lookup"><span data-stu-id="3a856-313">Azure Redis Cache cmdlet documentation on MSDN</span></span>](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* <span data-ttu-id="3a856-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): informazioni sui cmdlet di hello toouse nel modulo di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3a856-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): Learn toouse hello cmdlets in hello Azure Resource Manager module.</span></span>
* <span data-ttu-id="3a856-315">[Utilizzo risorse gruppi toomanage le risorse di Azure](../azure-resource-manager/resource-group-template-deploy-portal.md): informazioni su come toocreate e gestire gruppi di risorse nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3a856-315">[Using Resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md): Learn how toocreate and manage resource groups in hello Azure portal.</span></span>
* <span data-ttu-id="3a856-316">[Blog di Azure](http://blogs.msdn.com/windowsazure): informazioni sulle nuove funzionalità di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a856-316">[Azure blog](http://blogs.msdn.com/windowsazure): Learn about new features in Azure.</span></span>
* <span data-ttu-id="3a856-317">[Blog di Windows PowerShell](http://blogs.msdn.com/powershell): informazioni sulle nuove funzionalità di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3a856-317">[Windows PowerShell blog](http://blogs.msdn.com/powershell): Learn about new features in Windows PowerShell.</span></span>
* <span data-ttu-id="3a856-318">[Blog "Hey, Scripting Blog](http://blogs.technet.com/b/heyscriptingguy/): ottenere suggerimenti reali da hello community di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3a856-318">["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Get real-world tips and tricks from hello Windows PowerShell community.</span></span>

