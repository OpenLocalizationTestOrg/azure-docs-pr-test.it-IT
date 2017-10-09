---
title: Cache Redis di Azure mediante Azure CLI aaaManage | Documenti Microsoft
description: "Informazioni su come tooinstall hello Azure CLI su qualsiasi piattaforma, come toouse è tooconnect tooyour account Azure e come toocreate e gestire una cache Redis da hello CLI di Azure."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 964ff245-859d-4bc1-bccf-62e4b3c1169f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: e8ee30090133e6b4edea93dcd13fd171e75989bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="21cac-103">Come toocreate e gestire Cache Redis di Azure utilizzando hello interfaccia della riga di comando di Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="21cac-103">How toocreate and manage Azure Redis Cache using hello Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="21cac-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="21cac-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="21cac-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="21cac-105">Azure CLI</span></span>](cache-manage-cli.md)
>
>

<span data-ttu-id="21cac-106">Hello CLI di Azure è un ottimo modo toomanage dell'infrastruttura di Azure da qualsiasi piattaforma.</span><span class="sxs-lookup"><span data-stu-id="21cac-106">hello Azure CLI is a great way toomanage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="21cac-107">In questo articolo illustra come toocreate e gestire le istanze di Cache Redis di Azure mediante Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="21cac-107">This article shows you how toocreate and manage your Azure Redis Cache instances using hello Azure CLI.</span></span>

> [!NOTE]
> <span data-ttu-id="21cac-108">Questo articolo riguarda tooa precedente versione di CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="21cac-108">This article applies tooa previous version of Azure CLI.</span></span> <span data-ttu-id="21cac-109">Per script di esempio 2.0 CLI di Azure più recenti hello, vedere [esempi per cache Redis di Azure CLI](cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="21cac-109">For hello latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="21cac-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="21cac-110">Prerequisites</span></span>
<span data-ttu-id="21cac-111">toocreate e gestire le istanze di Cache Redis di Azure utilizzando l'interfaccia CLI di Azure, è necessario completare hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="21cac-111">toocreate and manage Azure Redis Cache instances using Azure CLI, you must complete hello following steps.</span></span>

* <span data-ttu-id="21cac-112">È necessario disporre di un account Azure.</span><span class="sxs-lookup"><span data-stu-id="21cac-112">You must have an Azure account.</span></span> <span data-ttu-id="21cac-113">Se non è disponibile, è possibile creare un [account gratuito](https://azure.microsoft.com/pricing/free-trial/) in pochi istanti.</span><span class="sxs-lookup"><span data-stu-id="21cac-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="21cac-114">[Installare hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="21cac-114">[Install hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="21cac-115">Connettere l'installazione di CLI di Azure con un account di Azure personale, o con un lavoro o scuola account Azure e accedere da hello CLI di Azure utilizzando hello `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="21cac-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from hello Azure CLI using hello `azure login` command.</span></span> <span data-ttu-id="21cac-116">toounderstand hello differenze e scegliere, vedere [connettersi tooan sottoscrizione di Azure da hello interfaccia della riga di comando di Azure (Azure CLI)](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="21cac-116">toounderstand hello differences and choose, see [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="21cac-117">Prima di eseguire uno dei seguenti comandi hello, passare hello CLI di Azure in modalità di gestione delle risorse eseguendo hello `azure config mode arm` comando.</span><span class="sxs-lookup"><span data-stu-id="21cac-117">Before running any of hello following commands, switch hello Azure CLI into Resource Manager mode by running hello `azure config mode arm` command.</span></span> <span data-ttu-id="21cac-118">Per ulteriori informazioni, vedere [toomanage CLI di Azure hello Azure usare risorse e gruppi di risorse](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="21cac-118">For more information, see [Use hello Azure CLI toomanage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="21cac-119">Proprietà di Cache Redis</span><span class="sxs-lookup"><span data-stu-id="21cac-119">Redis Cache properties</span></span>
<span data-ttu-id="21cac-120">le proprietà seguenti Hello vengono utilizzate durante la creazione e aggiornamento di istanze di Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="21cac-120">hello following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="21cac-121">Proprietà</span><span class="sxs-lookup"><span data-stu-id="21cac-121">Property</span></span> | <span data-ttu-id="21cac-122">Switch</span><span class="sxs-lookup"><span data-stu-id="21cac-122">Switch</span></span> | <span data-ttu-id="21cac-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="21cac-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21cac-124">name</span><span class="sxs-lookup"><span data-stu-id="21cac-124">name</span></span> |<span data-ttu-id="21cac-125">-n, --name</span><span class="sxs-lookup"><span data-stu-id="21cac-125">-n, --name</span></span> |<span data-ttu-id="21cac-126">Nome della Cache Redis hello.</span><span class="sxs-lookup"><span data-stu-id="21cac-126">Name of hello Redis Cache.</span></span> |
| <span data-ttu-id="21cac-127">gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="21cac-127">resource group</span></span> |<span data-ttu-id="21cac-128">-g, --resource-group</span><span class="sxs-lookup"><span data-stu-id="21cac-128">-g, --resource-group</span></span> |<span data-ttu-id="21cac-129">Nome del gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="21cac-129">Name of hello Resource Group.</span></span> |
| <span data-ttu-id="21cac-130">location</span><span class="sxs-lookup"><span data-stu-id="21cac-130">location</span></span> |<span data-ttu-id="21cac-131">-l, --location</span><span class="sxs-lookup"><span data-stu-id="21cac-131">-l, --location</span></span> |<span data-ttu-id="21cac-132">Cache toocreate del percorso.</span><span class="sxs-lookup"><span data-stu-id="21cac-132">Location toocreate cache.</span></span> |
| <span data-ttu-id="21cac-133">size</span><span class="sxs-lookup"><span data-stu-id="21cac-133">size</span></span> |<span data-ttu-id="21cac-134">-z, --size</span><span class="sxs-lookup"><span data-stu-id="21cac-134">-z, --size</span></span> |<span data-ttu-id="21cac-135">Dimensione della Cache Redis hello.</span><span class="sxs-lookup"><span data-stu-id="21cac-135">Size of hello Redis Cache.</span></span> <span data-ttu-id="21cac-136">Valori validi: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="21cac-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="21cac-137">sku</span><span class="sxs-lookup"><span data-stu-id="21cac-137">sku</span></span> |<span data-ttu-id="21cac-138">-x, sku:</span><span class="sxs-lookup"><span data-stu-id="21cac-138">-x, --sku</span></span> |<span data-ttu-id="21cac-139">SKU di Redis.</span><span class="sxs-lookup"><span data-stu-id="21cac-139">Redis SKU.</span></span> <span data-ttu-id="21cac-140">Deve essere uno di: [Basic, Standard, Premium]</span><span class="sxs-lookup"><span data-stu-id="21cac-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="21cac-141">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="21cac-141">EnableNonSslPort</span></span> |<span data-ttu-id="21cac-142">-e, --enable-non-ssl-port</span><span class="sxs-lookup"><span data-stu-id="21cac-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="21cac-143">Proprietà EnableNonSslPort di hello Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="21cac-143">EnableNonSslPort property of hello Redis Cache.</span></span> <span data-ttu-id="21cac-144">Aggiungere questo flag se si desidera tooenable hello Non SSL porta per la cache</span><span class="sxs-lookup"><span data-stu-id="21cac-144">Add this flag if you want tooenable hello Non SSL Port for your cache</span></span> |
| <span data-ttu-id="21cac-145">Configurazione di Redis</span><span class="sxs-lookup"><span data-stu-id="21cac-145">Redis Configuration</span></span> |<span data-ttu-id="21cac-146">-c, --redis-configuration</span><span class="sxs-lookup"><span data-stu-id="21cac-146">-c, --redis-configuration</span></span> |<span data-ttu-id="21cac-147">Configurazione di Redis.</span><span class="sxs-lookup"><span data-stu-id="21cac-147">Redis Configuration.</span></span> <span data-ttu-id="21cac-148">Immettere qui una stringa in formato JSON di chiavi di configurazione e valori.</span><span class="sxs-lookup"><span data-stu-id="21cac-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="21cac-149">Formato: "{"":"","":""}"</span><span class="sxs-lookup"><span data-stu-id="21cac-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="21cac-150">Configurazione di Redis</span><span class="sxs-lookup"><span data-stu-id="21cac-150">Redis Configuration</span></span> |<span data-ttu-id="21cac-151">-f, --redis-configuration-file</span><span class="sxs-lookup"><span data-stu-id="21cac-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="21cac-152">Configurazione di Redis.</span><span class="sxs-lookup"><span data-stu-id="21cac-152">Redis Configuration.</span></span> <span data-ttu-id="21cac-153">Immettere il percorso di hello di un file contenente le chiavi di configurazione e i valori qui.</span><span class="sxs-lookup"><span data-stu-id="21cac-153">Enter hello path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="21cac-154">Formato per la voce del file hello: {"": "","": ""}</span><span class="sxs-lookup"><span data-stu-id="21cac-154">Format for hello file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="21cac-155">Numero di partizioni</span><span class="sxs-lookup"><span data-stu-id="21cac-155">Shard Count</span></span> |<span data-ttu-id="21cac-156">-r, --shard-count</span><span class="sxs-lookup"><span data-stu-id="21cac-156">-r, --shard-count</span></span> |<span data-ttu-id="21cac-157">Numero di partizioni toocreate in una Cache di Cluster Premium con il clustering.</span><span class="sxs-lookup"><span data-stu-id="21cac-157">Number of Shards toocreate on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="21cac-158">Rete virtuale</span><span class="sxs-lookup"><span data-stu-id="21cac-158">Virtual Network</span></span> |<span data-ttu-id="21cac-159">-v, --virtual-network</span><span class="sxs-lookup"><span data-stu-id="21cac-159">-v, --virtual-network</span></span> |<span data-ttu-id="21cac-160">Quando la cache in una rete virtuale, di hosting specifica hello esatta ARM ID della risorsa hello toodeploy di rete virtuale hello redis cache.</span><span class="sxs-lookup"><span data-stu-id="21cac-160">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="21cac-161">Formato di esempio: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="21cac-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="21cac-162">tipo di chiave</span><span class="sxs-lookup"><span data-stu-id="21cac-162">key type</span></span> |<span data-ttu-id="21cac-163">-t, --key-type</span><span class="sxs-lookup"><span data-stu-id="21cac-163">-t, --key-type</span></span> |<span data-ttu-id="21cac-164">Tipo di chiave toorenew.</span><span class="sxs-lookup"><span data-stu-id="21cac-164">Type of key toorenew.</span></span> <span data-ttu-id="21cac-165">Valori validi: [primario, secondario]</span><span class="sxs-lookup"><span data-stu-id="21cac-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="21cac-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="21cac-166">StaticIP</span></span> |<span data-ttu-id="21cac-167">-p, --static-ip <static-ip></span><span class="sxs-lookup"><span data-stu-id="21cac-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="21cac-168">Quando si ospita la cache in una rete virtuale, specifica l'indirizzo IP nella subnet hello per cache di hello.</span><span class="sxs-lookup"><span data-stu-id="21cac-168">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="21cac-169">Se omesso, automaticamente dalla subnet hello viene scelto uno.</span><span class="sxs-lookup"><span data-stu-id="21cac-169">If not provided, one is chosen for you from hello subnet.</span></span> |
| <span data-ttu-id="21cac-170">Subnet</span><span class="sxs-lookup"><span data-stu-id="21cac-170">Subnet</span></span> |<span data-ttu-id="21cac-171">t, --subnet <subnet></span><span class="sxs-lookup"><span data-stu-id="21cac-171">t, --subnet <subnet></span></span> |<span data-ttu-id="21cac-172">Quando si ospita la cache in una rete virtuale, specifica il nome di hello della subnet hello nella cache di hello quali toodeploy.</span><span class="sxs-lookup"><span data-stu-id="21cac-172">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> |
| <span data-ttu-id="21cac-173">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="21cac-173">VirtualNetwork</span></span> |<span data-ttu-id="21cac-174">-v, --virtual-network <virtual-network></span><span class="sxs-lookup"><span data-stu-id="21cac-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="21cac-175">Quando la cache in una rete virtuale, di hosting specifica hello esatta ARM ID della risorsa hello toodeploy di rete virtuale hello redis cache.</span><span class="sxs-lookup"><span data-stu-id="21cac-175">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="21cac-176">Formato di esempio: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="21cac-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="21cac-177">Subscription</span><span class="sxs-lookup"><span data-stu-id="21cac-177">Subscription</span></span> |<span data-ttu-id="21cac-178">-s, --subscription</span><span class="sxs-lookup"><span data-stu-id="21cac-178">-s, --subscription</span></span> |<span data-ttu-id="21cac-179">Identificatore della sottoscrizione Hello.</span><span class="sxs-lookup"><span data-stu-id="21cac-179">hello subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="21cac-180">Vedere tutti i comandi di Cache Redis</span><span class="sxs-lookup"><span data-stu-id="21cac-180">See all Redis Cache commands</span></span>
<span data-ttu-id="21cac-181">toosee tutti i comandi di Cache Redis e i relativi parametri, utilizzare hello `azure rediscache -h` comando.</span><span class="sxs-lookup"><span data-stu-id="21cac-181">toosee all Redis Cache commands and their parameters, use hello `azure rediscache -h` command.</span></span>

    C:\>azure rediscache -h
    help:    Commands toomanage your Azure Redis Cache(s)
    help:
    help:    Create a Redis Cache
    help:      rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Delete an existing Redis Cache
    help:      rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    List all Redis Caches within your Subscription or Resource Group
    help:      rediscache list [options]
    help:
    help:    Show properties of an existing Redis Cache
    help:      rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Change settings of an existing Redis Cache
    help:      rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Renew hello authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a><span data-ttu-id="21cac-182">Creare una Cache Redis</span><span class="sxs-lookup"><span data-stu-id="21cac-182">Create a Redis Cache</span></span>
<span data-ttu-id="21cac-183">toocreate una Cache Redis, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="21cac-183">toocreate a Redis Cache, use hello following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="21cac-184">Per ulteriori informazioni su questo comando, eseguire hello `azure rediscache create -h` comando.</span><span class="sxs-lookup"><span data-stu-id="21cac-184">For more information about this command, run hello `azure rediscache create -h` command.</span></span>

    C:\>azure rediscache create -h
    help:    Create a Redis Cache
    help:
    help:    Usage: rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -l, --location <location>                                Location toocreate cache.
    help:      -z, --size <size>                                        Size of hello Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of hello Redis Cache. Add this flag if you want tooenable hello Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here. Format for hello file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards toocreate on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="21cac-185">Eliminare una Cache Redis esistente</span><span class="sxs-lookup"><span data-stu-id="21cac-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="21cac-186">toodelete una Cache Redis, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="21cac-186">toodelete a Redis Cache, use hello following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="21cac-187">Per ulteriori informazioni su questo comando, eseguire hello `azure rediscache delete -h` comando.</span><span class="sxs-lookup"><span data-stu-id="21cac-187">For more information about this command, run hello `azure rediscache delete -h` command.</span></span>

    C:\>azure rediscache delete -h
    help:    Delete an existing Redis Cache
    help:
    help:    Usage: rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which hello cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="21cac-188">Elenco di tutte le Cache Redis all'interno della sottoscrizione o di un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="21cac-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="21cac-189">utilizzare tutte le cache Redis all'interno della sottoscrizione o un gruppo di risorse, toolist hello il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="21cac-189">toolist all Redis Caches within your Subscription or Resource Group, use hello following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="21cac-190">Per ulteriori informazioni su questo comando, eseguire hello `azure rediscache list -h` comando.</span><span class="sxs-lookup"><span data-stu-id="21cac-190">For more information about this command, run hello `azure rediscache list -h` command.</span></span>

    C:\>azure rediscache list -h
    help:    List all Redis Caches within your Subscription or Resource Group
    help:
    help:    Usage: rediscache list [options]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="21cac-191">Visualizzare le proprietà di una Cache Redis esistente</span><span class="sxs-lookup"><span data-stu-id="21cac-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="21cac-192">proprietà tooshow di una Cache Redis esistente, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="21cac-192">tooshow properties of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="21cac-193">Per ulteriori informazioni su questo comando, eseguire hello `azure rediscache show -h` comando.</span><span class="sxs-lookup"><span data-stu-id="21cac-193">For more information about this command, run hello `azure rediscache show -h` command.</span></span>

    C:\>azure rediscache show -h
    help:    Show properties of an existing Redis Cache
    help:
    help:    Usage: rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="21cac-194">Modificare le impostazioni di una Cache Redis esistente</span><span class="sxs-lookup"><span data-stu-id="21cac-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="21cac-195">impostazioni toochange di una Cache Redis esistente, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="21cac-195">toochange settings of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="21cac-196">Per ulteriori informazioni su questo comando, eseguire hello `azure rediscache set -h` comando.</span><span class="sxs-lookup"><span data-stu-id="21cac-196">For more information about this command, run hello `azure rediscache set -h` command.</span></span>

    C:\>azure rediscache set -h
    help:    Change settings of an existing Redis Cache
    help:
    help:    Usage: rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="21cac-197">Rinnova la chiave di autenticazione hello per una Cache Redis esistente</span><span class="sxs-lookup"><span data-stu-id="21cac-197">Renew hello authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="21cac-198">chiave di autenticazione hello toorenew per una Redis Cache esistente, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="21cac-198">toorenew hello authentication key for an existing Redis Cache, use hello following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="21cac-199">Specificare `Primary` o `Secondary` per `key-type`.</span><span class="sxs-lookup"><span data-stu-id="21cac-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="21cac-200">Per ulteriori informazioni su questo comando, eseguire hello `azure rediscache renew-key -h` comando.</span><span class="sxs-lookup"><span data-stu-id="21cac-200">For more information about this command, run hello `azure rediscache renew-key -h` command.</span></span>

    C:\>azure rediscache renew-key -h
    help:    Renew hello authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key toorenew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="21cac-201">Chiavi di elenco primario e secondario di una Cache Redis esistente</span><span class="sxs-lookup"><span data-stu-id="21cac-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="21cac-202">le chiavi primari e secondari toolist di una Cache Redis esistente, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="21cac-202">toolist Primary and Secondary keys of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="21cac-203">Per ulteriori informazioni su questo comando, eseguire hello `azure rediscache list-keys -h` comando.</span><span class="sxs-lookup"><span data-stu-id="21cac-203">For more information about this command, run hello `azure rediscache list-keys -h` command.</span></span>

    C:\>azure rediscache list-keys -h
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:
    help:    Usage: rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
