---
title: Gestire Cache Redis di Azure con l'interfaccia della riga di comando di Azure | Documentazione Microsoft
description: Come installare l'interfaccia della riga di comando di Azure su qualsiasi piattaforma, come utilizzarla per connettersi all'account Azure e come creare e gestire una Cache Redis dall'interfaccia della riga di comando di Azure.
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
ms.openlocfilehash: ba078a870a3998568170cc197bd6698b97b7fadb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-manage-azure-redis-cache-using-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="99cef-103">Come creare e gestire Cache Redis di Azure tramite l'interfaccia della riga di comando di Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="99cef-103">How to create and manage Azure Redis Cache using the Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="99cef-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="99cef-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="99cef-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="99cef-105">Azure CLI</span></span>](cache-manage-cli.md)
>
>

<span data-ttu-id="99cef-106">L'interfaccia della riga di comando di Azure è un ottimo modo di gestire l'infrastruttura di Azure da qualsiasi piattaforma.</span><span class="sxs-lookup"><span data-stu-id="99cef-106">The Azure CLI is a great way to manage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="99cef-107">In questo articolo viene illustrato come creare e gestire le istanze di Cache Redis di Azure tramite la CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="99cef-107">This article shows you how to create and manage your Azure Redis Cache instances using the Azure CLI.</span></span>

> [!NOTE]
> <span data-ttu-id="99cef-108">Questo articolo si applica a una versione precedente dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="99cef-108">This article applies to a previous version of Azure CLI.</span></span> <span data-ttu-id="99cef-109">Per script di esempio della più recente interfaccia della riga di comando di Azure 2.0, vedere gli [esempi dell'interfaccia della riga di comando di Azure per Cache Redis](cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="99cef-109">For the latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="99cef-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="99cef-110">Prerequisites</span></span>
<span data-ttu-id="99cef-111">Per creare e gestire le istanze di Cache Redis di Azure utilizzando CLI di Azure, è necessario completare i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="99cef-111">To create and manage Azure Redis Cache instances using Azure CLI, you must complete the following steps.</span></span>

* <span data-ttu-id="99cef-112">È necessario disporre di un account Azure.</span><span class="sxs-lookup"><span data-stu-id="99cef-112">You must have an Azure account.</span></span> <span data-ttu-id="99cef-113">Se non è disponibile, è possibile creare un [account gratuito](https://azure.microsoft.com/pricing/free-trial/) in pochi istanti.</span><span class="sxs-lookup"><span data-stu-id="99cef-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="99cef-114">[Installare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="99cef-114">[Install the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="99cef-115">Connettere l'installazione dell’interfaccia della riga di comando di Azure con un account Azure personale o con un account di lavoro o scolastico di Azure, e accedere dall’interfaccia della riga di comando di Azure utilizzando il comando `azure login` .</span><span class="sxs-lookup"><span data-stu-id="99cef-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from the Azure CLI using the `azure login` command.</span></span> <span data-ttu-id="99cef-116">Per comprendere le differenze e scegliere, vedere [Connettersi a una sottoscrizione di Azure dall'interfaccia della riga di comando di Azure (Azure CLI)](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="99cef-116">To understand the differences and choose, see [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="99cef-117">Prima di eseguire uno dei seguenti comandi, passare l’interfaccia della riga di comando di Azure in modalità di Gestione delle risorse eseguendo il comando `azure config mode arm` .</span><span class="sxs-lookup"><span data-stu-id="99cef-117">Before running any of the following commands, switch the Azure CLI into Resource Manager mode by running the `azure config mode arm` command.</span></span> <span data-ttu-id="99cef-118">Per altre informazioni, vedere l'articolo su come [usare l'interfaccia della riga di comando di Azure per gestire risorse e gruppi di risorse di Azure](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="99cef-118">For more information, see [Use the Azure CLI to manage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="99cef-119">Proprietà di Cache Redis</span><span class="sxs-lookup"><span data-stu-id="99cef-119">Redis Cache properties</span></span>
<span data-ttu-id="99cef-120">Le seguenti proprietà vengono utilizzate durante la creazione e l’aggiornamento delle istanze di Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="99cef-120">The following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="99cef-121">Proprietà</span><span class="sxs-lookup"><span data-stu-id="99cef-121">Property</span></span> | <span data-ttu-id="99cef-122">Switch</span><span class="sxs-lookup"><span data-stu-id="99cef-122">Switch</span></span> | <span data-ttu-id="99cef-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="99cef-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="99cef-124">name</span><span class="sxs-lookup"><span data-stu-id="99cef-124">name</span></span> |<span data-ttu-id="99cef-125">-n, --name</span><span class="sxs-lookup"><span data-stu-id="99cef-125">-n, --name</span></span> |<span data-ttu-id="99cef-126">Nome della Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="99cef-126">Name of the Redis Cache.</span></span> |
| <span data-ttu-id="99cef-127">gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="99cef-127">resource group</span></span> |<span data-ttu-id="99cef-128">-g, --resource-group</span><span class="sxs-lookup"><span data-stu-id="99cef-128">-g, --resource-group</span></span> |<span data-ttu-id="99cef-129">Nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="99cef-129">Name of the Resource Group.</span></span> |
| <span data-ttu-id="99cef-130">location</span><span class="sxs-lookup"><span data-stu-id="99cef-130">location</span></span> |<span data-ttu-id="99cef-131">-l, --location</span><span class="sxs-lookup"><span data-stu-id="99cef-131">-l, --location</span></span> |<span data-ttu-id="99cef-132">Posizione in cui creare una cache.</span><span class="sxs-lookup"><span data-stu-id="99cef-132">Location to create cache.</span></span> |
| <span data-ttu-id="99cef-133">size</span><span class="sxs-lookup"><span data-stu-id="99cef-133">size</span></span> |<span data-ttu-id="99cef-134">-z, --size</span><span class="sxs-lookup"><span data-stu-id="99cef-134">-z, --size</span></span> |<span data-ttu-id="99cef-135">Dimensione della Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="99cef-135">Size of the Redis Cache.</span></span> <span data-ttu-id="99cef-136">Valori validi: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="99cef-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="99cef-137">sku</span><span class="sxs-lookup"><span data-stu-id="99cef-137">sku</span></span> |<span data-ttu-id="99cef-138">-x, sku:</span><span class="sxs-lookup"><span data-stu-id="99cef-138">-x, --sku</span></span> |<span data-ttu-id="99cef-139">SKU di Redis.</span><span class="sxs-lookup"><span data-stu-id="99cef-139">Redis SKU.</span></span> <span data-ttu-id="99cef-140">Deve essere uno di: [Basic, Standard, Premium]</span><span class="sxs-lookup"><span data-stu-id="99cef-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="99cef-141">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="99cef-141">EnableNonSslPort</span></span> |<span data-ttu-id="99cef-142">-e, --enable-non-ssl-port</span><span class="sxs-lookup"><span data-stu-id="99cef-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="99cef-143">Proprietà EnableNonSslPort della Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="99cef-143">EnableNonSslPort property of the Redis Cache.</span></span> <span data-ttu-id="99cef-144">Aggiungere questo flag se si desidera abilitare la porta SSL Non per la cache</span><span class="sxs-lookup"><span data-stu-id="99cef-144">Add this flag if you want to enable the Non SSL Port for your cache</span></span> |
| <span data-ttu-id="99cef-145">Configurazione di Redis</span><span class="sxs-lookup"><span data-stu-id="99cef-145">Redis Configuration</span></span> |<span data-ttu-id="99cef-146">-c, --redis-configuration</span><span class="sxs-lookup"><span data-stu-id="99cef-146">-c, --redis-configuration</span></span> |<span data-ttu-id="99cef-147">Configurazione di Redis.</span><span class="sxs-lookup"><span data-stu-id="99cef-147">Redis Configuration.</span></span> <span data-ttu-id="99cef-148">Immettere qui una stringa in formato JSON di chiavi di configurazione e valori.</span><span class="sxs-lookup"><span data-stu-id="99cef-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="99cef-149">Formato: "{"":"","":""}"</span><span class="sxs-lookup"><span data-stu-id="99cef-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="99cef-150">Configurazione di Redis</span><span class="sxs-lookup"><span data-stu-id="99cef-150">Redis Configuration</span></span> |<span data-ttu-id="99cef-151">-f, --redis-configuration-file</span><span class="sxs-lookup"><span data-stu-id="99cef-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="99cef-152">Configurazione di Redis.</span><span class="sxs-lookup"><span data-stu-id="99cef-152">Redis Configuration.</span></span> <span data-ttu-id="99cef-153">Immettere qui il percorso di un file contenente le chiavi di configurazione e i valori.</span><span class="sxs-lookup"><span data-stu-id="99cef-153">Enter the path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="99cef-154">Formato per l’immissione del file: {"": "","": ""}</span><span class="sxs-lookup"><span data-stu-id="99cef-154">Format for the file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="99cef-155">Numero di partizioni</span><span class="sxs-lookup"><span data-stu-id="99cef-155">Shard Count</span></span> |<span data-ttu-id="99cef-156">-r, --shard-count</span><span class="sxs-lookup"><span data-stu-id="99cef-156">-r, --shard-count</span></span> |<span data-ttu-id="99cef-157">Numero di partizioni da creare su una cache di cluster Premium con il clustering.</span><span class="sxs-lookup"><span data-stu-id="99cef-157">Number of Shards to create on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="99cef-158">Rete virtuale</span><span class="sxs-lookup"><span data-stu-id="99cef-158">Virtual Network</span></span> |<span data-ttu-id="99cef-159">-v, --virtual-network</span><span class="sxs-lookup"><span data-stu-id="99cef-159">-v, --virtual-network</span></span> |<span data-ttu-id="99cef-160">Quando si ospita la cache in una rete virtuale, specifica l'ID risorsa esatto ARM della rete virtuale in cui distribuire la cache Redis.</span><span class="sxs-lookup"><span data-stu-id="99cef-160">When hosting your cache in a VNET, specifies the exact ARM resource ID of the virtual network to deploy the redis cache in.</span></span> <span data-ttu-id="99cef-161">Formato di esempio: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="99cef-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="99cef-162">tipo di chiave</span><span class="sxs-lookup"><span data-stu-id="99cef-162">key type</span></span> |<span data-ttu-id="99cef-163">-t, --key-type</span><span class="sxs-lookup"><span data-stu-id="99cef-163">-t, --key-type</span></span> |<span data-ttu-id="99cef-164">Tipo di chiave per il rinnovo.</span><span class="sxs-lookup"><span data-stu-id="99cef-164">Type of key to renew.</span></span> <span data-ttu-id="99cef-165">Valori validi: [primario, secondario]</span><span class="sxs-lookup"><span data-stu-id="99cef-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="99cef-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="99cef-166">StaticIP</span></span> |<span data-ttu-id="99cef-167">-p, --static-ip <static-ip></span><span class="sxs-lookup"><span data-stu-id="99cef-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="99cef-168">Quando si ospita la cache in una rete virtuale, specifica l'indirizzo IP univoco nella subnet per la cache.</span><span class="sxs-lookup"><span data-stu-id="99cef-168">When hosting your cache in a VNET, specifies a unique IP address in the subnet for the cache.</span></span> <span data-ttu-id="99cef-169">Se non specificato, ne verrà scelto uno dalla subnet.</span><span class="sxs-lookup"><span data-stu-id="99cef-169">If not provided, one is chosen for you from the subnet.</span></span> |
| <span data-ttu-id="99cef-170">Subnet</span><span class="sxs-lookup"><span data-stu-id="99cef-170">Subnet</span></span> |<span data-ttu-id="99cef-171">t, --subnet <subnet></span><span class="sxs-lookup"><span data-stu-id="99cef-171">t, --subnet <subnet></span></span> |<span data-ttu-id="99cef-172">Quando si ospita la cache in una rete virtuale, specifica il nome della subnet in cui distribuire la cache.</span><span class="sxs-lookup"><span data-stu-id="99cef-172">When hosting your cache in a VNET, specifies the name of the subnet in which to deploy the cache.</span></span> |
| <span data-ttu-id="99cef-173">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="99cef-173">VirtualNetwork</span></span> |<span data-ttu-id="99cef-174">-v, --virtual-network <virtual-network></span><span class="sxs-lookup"><span data-stu-id="99cef-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="99cef-175">Quando si ospita la cache in una rete virtuale, specifica l'ID risorsa esatto ARM della rete virtuale in cui distribuire la cache Redis.</span><span class="sxs-lookup"><span data-stu-id="99cef-175">When hosting your cache in a VNET, specifies the exact ARM resource ID of the virtual network to deploy the redis cache in.</span></span> <span data-ttu-id="99cef-176">Formato di esempio: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="99cef-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="99cef-177">Subscription</span><span class="sxs-lookup"><span data-stu-id="99cef-177">Subscription</span></span> |<span data-ttu-id="99cef-178">-s, --subscription</span><span class="sxs-lookup"><span data-stu-id="99cef-178">-s, --subscription</span></span> |<span data-ttu-id="99cef-179">L'identificatore della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="99cef-179">The subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="99cef-180">Vedere tutti i comandi di Cache Redis</span><span class="sxs-lookup"><span data-stu-id="99cef-180">See all Redis Cache commands</span></span>
<span data-ttu-id="99cef-181">Per visualizzare tutti i comandi di Cache Redis e i relativi parametri, utilizzare il comando `azure rediscache -h` .</span><span class="sxs-lookup"><span data-stu-id="99cef-181">To see all Redis Cache commands and their parameters, use the `azure rediscache -h` command.</span></span>

    C:\>azure rediscache -h
    help:    Commands to manage your Azure Redis Cache(s)
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
    help:    Renew the authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a><span data-ttu-id="99cef-182">Creare una Cache Redis</span><span class="sxs-lookup"><span data-stu-id="99cef-182">Create a Redis Cache</span></span>
<span data-ttu-id="99cef-183">Per creare una Cache Redis, utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="99cef-183">To create a Redis Cache, use the following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="99cef-184">Per altre informazioni su questo comando, eseguire il comando `azure rediscache create -h` .</span><span class="sxs-lookup"><span data-stu-id="99cef-184">For more information about this command, run the `azure rediscache create -h` command.</span></span>

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
    help:      -n, --name <name>                                        Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of the Resource Group
    help:      -l, --location <location>                                Location to create cache.
    help:      -z, --size <size>                                        Size of the Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of the Redis Cache. Add this flag if you want to enable the Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter the path of a file containing configuration keys and values here. Format for the file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards to create on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  The exact ARM resource ID of the virtual network to deploy the redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="99cef-185">Eliminare una Cache Redis esistente</span><span class="sxs-lookup"><span data-stu-id="99cef-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="99cef-186">Per eliminare una Cache Redis, utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="99cef-186">To delete a Redis Cache, use the following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="99cef-187">Per altre informazioni su questo comando, eseguire il comando `azure rediscache delete -h` .</span><span class="sxs-lookup"><span data-stu-id="99cef-187">For more information about this command, run the `azure rediscache delete -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which the cache exists
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="99cef-188">Elenco di tutte le Cache Redis all'interno della sottoscrizione o di un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="99cef-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="99cef-189">Per elencare tutte le Cache Redis all'interno della sottoscrizione o un gruppo di risorse, utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="99cef-189">To list all Redis Caches within your Subscription or Resource Group, use the following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="99cef-190">Per altre informazioni su questo comando, eseguire il comando `azure rediscache list -h` .</span><span class="sxs-lookup"><span data-stu-id="99cef-190">For more information about this command, run the `azure rediscache list -h` command.</span></span>

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
    help:      -g, --resource-group <resource-group>  Name of the Resource Group
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="99cef-191">Visualizzare le proprietà di una Cache Redis esistente</span><span class="sxs-lookup"><span data-stu-id="99cef-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="99cef-192">Per visualizzare le proprietà di una Cache Redis esistente, utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="99cef-192">To show properties of an existing Redis Cache, use the following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="99cef-193">Per altre informazioni su questo comando, eseguire il comando `azure rediscache show -h` .</span><span class="sxs-lookup"><span data-stu-id="99cef-193">For more information about this command, run the `azure rediscache show -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="99cef-194">Modificare le impostazioni di una Cache Redis esistente</span><span class="sxs-lookup"><span data-stu-id="99cef-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="99cef-195">Per modificare le impostazioni di una Cache Redis esistente, utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="99cef-195">To change settings of an existing Redis Cache, use the following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="99cef-196">Per altre informazioni su questo comando, eseguire il comando `azure rediscache set -h` .</span><span class="sxs-lookup"><span data-stu-id="99cef-196">For more information about this command, run the `azure rediscache set -h` command.</span></span>

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
    help:      -n, --name <name>                                        Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of the Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter the path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-the-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="99cef-197">Rinnovare la chiave di autenticazione per una Cache Redis esistente</span><span class="sxs-lookup"><span data-stu-id="99cef-197">Renew the authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="99cef-198">Per rinnovare la chiave di autenticazione per una Cache Redis esistente, utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="99cef-198">To renew the authentication key for an existing Redis Cache, use the following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="99cef-199">Specificare `Primary` o `Secondary` per `key-type`.</span><span class="sxs-lookup"><span data-stu-id="99cef-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="99cef-200">Per altre informazioni su questo comando, eseguire il comando `azure rediscache renew-key -h`.</span><span class="sxs-lookup"><span data-stu-id="99cef-200">For more information about this command, run the `azure rediscache renew-key -h` command.</span></span>

    C:\>azure rediscache renew-key -h
    help:    Renew the authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key to renew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="99cef-201">Chiavi di elenco primario e secondario di una Cache Redis esistente</span><span class="sxs-lookup"><span data-stu-id="99cef-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="99cef-202">Per le chiavi di elenco primario o secondario di una Cache Redis esistente, utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="99cef-202">To list Primary and Secondary keys of an existing Redis Cache, use the following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="99cef-203">Per altre informazioni su questo comando, eseguire il comando `azure rediscache list-keys -h` .</span><span class="sxs-lookup"><span data-stu-id="99cef-203">For more information about this command, run the `azure rediscache list-keys -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
