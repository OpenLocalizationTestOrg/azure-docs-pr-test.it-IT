---
title: Risolvere i problemi relativi al gateway di rete virtuale e alle connessioni di Azure - Interfaccia della riga di comando di Azure 1.0 | Microsoft Docs
description: Questa pagina spiega come usare l'interfaccia della riga di comando di Azure 1.0 per risolvere i problemi in Network Watcher di Azure
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: 9de4b2a0bdda7ffbd269883877a708d67312092f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a><span data-ttu-id="4ea85-103">Risolvere i problemi relativi al gateway di rete virtuale e alle connessioni tramite l'interfaccia della riga di comando 1.0 di Azure in Network Watcher di Azure</span><span class="sxs-lookup"><span data-stu-id="4ea85-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="4ea85-104">Portale</span><span class="sxs-lookup"><span data-stu-id="4ea85-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="4ea85-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ea85-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="4ea85-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="4ea85-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="4ea85-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="4ea85-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="4ea85-108">API REST</span><span class="sxs-lookup"><span data-stu-id="4ea85-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="4ea85-109">Network Watcher offre numerose funzionalità che consentono di comprendere le risorse di rete in Azure.</span><span class="sxs-lookup"><span data-stu-id="4ea85-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="4ea85-110">Una di queste funzionalità è la risoluzione dei problemi riscontrati con le risorse.</span><span class="sxs-lookup"><span data-stu-id="4ea85-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="4ea85-111">La funzionalità può essere chiamata dal portale, da PowerShell, dall'interfaccia della riga di comando o dall'API REST.</span><span class="sxs-lookup"><span data-stu-id="4ea85-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="4ea85-112">Quando chiamata, Network Watcher controlla l'integrità di un gateway di rete virtuale o di una connessione e restituisce i risultati.</span><span class="sxs-lookup"><span data-stu-id="4ea85-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="4ea85-113">Questo articolo usa l'interfaccia della riga di comando di Azure 1.0 multipiattaforma, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="4ea85-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="4ea85-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="4ea85-114">Before you begin</span></span>

<span data-ttu-id="4ea85-115">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="4ea85-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="4ea85-116">Per un elenco dei tipi di gateway supportati, consultare i [tipi di gateway supportati](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="4ea85-116">For a list of supported gateway types visit, [Supported Gateway types](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="4ea85-117">Panoramica</span><span class="sxs-lookup"><span data-stu-id="4ea85-117">Overview</span></span>

<span data-ttu-id="4ea85-118">La risoluzione dei problemi delle risorse consente di risolvere i problemi che si verificano con i gateway di rete virtuale e le connessioni.</span><span class="sxs-lookup"><span data-stu-id="4ea85-118">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="4ea85-119">Quando viene inviata una richiesta di risoluzione dei problemi delle risorse, i log vengono sottoposti a query e controllati.</span><span class="sxs-lookup"><span data-stu-id="4ea85-119">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="4ea85-120">Dopo aver completato l'ispezione, vengono restituiti i risultati.</span><span class="sxs-lookup"><span data-stu-id="4ea85-120">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="4ea85-121">Le richieste di risoluzione dei problemi delle risorse sono richieste a esecuzione prolungata, che possono richiedere anche diversi minuti per restituire un risultato.</span><span class="sxs-lookup"><span data-stu-id="4ea85-121">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="4ea85-122">I log risultati vengono archiviati in un contenitore in un account di archiviazione specificato.</span><span class="sxs-lookup"><span data-stu-id="4ea85-122">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="4ea85-123">Recuperare una connessione e un gateway di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="4ea85-123">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="4ea85-124">In questo esempio la risoluzione dei problemi delle risorse viene eseguita su una connessione.</span><span class="sxs-lookup"><span data-stu-id="4ea85-124">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="4ea85-125">È anche possibile passare il comando a un gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4ea85-125">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="4ea85-126">Il cmdlet seguente elenca le connessioni VPN in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="4ea85-126">The following cmdlet lists the vpn-connections in a resource group.</span></span>

```azurecli
azure network vpn-connection list -g resourceGroupName
```

<span data-ttu-id="4ea85-127">È anche possibile eseguire il comando per visualizzare le connessioni di una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="4ea85-127">You can also run the command to see the connections in a subscription.</span></span>

```azurecli
azure network vpn-connection list -s subscription
```

<span data-ttu-id="4ea85-128">Dopo aver ottenuto il nome della connessione, è possibile eseguire questo comando per ottenere il relativo ID della risorsa:</span><span class="sxs-lookup"><span data-stu-id="4ea85-128">Once you have the name of the connection, you can run this command to get its resource Id:</span></span>

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a><span data-ttu-id="4ea85-129">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4ea85-129">Create a storage account</span></span>

<span data-ttu-id="4ea85-130">Il comando per la risoluzione dei problemi delle risorse restituisce i dati sullo stato della risorsa e salva i log in un account di archiviazione, per la successiva revisione.</span><span class="sxs-lookup"><span data-stu-id="4ea85-130">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="4ea85-131">In questo passaggio viene creato un account di archiviazione. È anche possibile usare un account di archiviazione già esistente.</span><span class="sxs-lookup"><span data-stu-id="4ea85-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="4ea85-132">Creare l'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4ea85-132">Create the storage account</span></span>

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. <span data-ttu-id="4ea85-133">Ottenere le chiavi dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4ea85-133">Get the storage account keys</span></span>

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. <span data-ttu-id="4ea85-134">Creare il contenitore</span><span class="sxs-lookup"><span data-stu-id="4ea85-134">Create the container</span></span>

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="4ea85-135">Eseguire il comando per la risoluzione dei problemi delle risorse di Network Watcher</span><span class="sxs-lookup"><span data-stu-id="4ea85-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="4ea85-136">Per risolvere i problemi relativi alle risorse eseguire il cmdlet `network watcher troubleshoot`.</span><span class="sxs-lookup"><span data-stu-id="4ea85-136">You troubleshoot resources with the `network watcher troubleshoot` cmdlet.</span></span> <span data-ttu-id="4ea85-137">Al cmdlet viene passato il gruppo di risorse, il nome del servizio Network Watcher, l'ID della connessione, l'ID dell'account di archiviazione, e il percorso del BLOB nel quale archiviare i risultati ottenuti.</span><span class="sxs-lookup"><span data-stu-id="4ea85-137">We pass the cmdlet the resource group, the name of the Network Watcher, the Id of the connection, the Id of the storage account, and the path to the blob to store the troubleshoot results in.</span></span>

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

<span data-ttu-id="4ea85-138">Dopo aver eseguito il cmdlet, Network Watcher esamina la risorsa per verificarne l'integrità.</span><span class="sxs-lookup"><span data-stu-id="4ea85-138">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="4ea85-139">Restituisce quindi i risultati alla shell e archivia i log dei risultati nell'account di archiviazione specificato.</span><span class="sxs-lookup"><span data-stu-id="4ea85-139">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="4ea85-140">Informazioni sui risultati</span><span class="sxs-lookup"><span data-stu-id="4ea85-140">Understanding the results</span></span>

<span data-ttu-id="4ea85-141">Il testo dell'azione offre indicazioni generiche su come risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="4ea85-141">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="4ea85-142">Se è possibile eseguire un'azione per il problema, viene fornito un collegamento con altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="4ea85-142">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="4ea85-143">Nel caso in cui non siano presenti altre indicazioni, la risposta include l'URL per aprire una richiesta di assistenza.</span><span class="sxs-lookup"><span data-stu-id="4ea85-143">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="4ea85-144">Per altre informazioni sulle proprietà della risposta e ciò che vie è incluso, consultare la [panoramica sulla risoluzione dei problemi in Network Watcher](network-watcher-troubleshoot-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4ea85-144">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="4ea85-145">Per istruzioni sul download di file dall'account di archiviazione di Azure, consultare [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="4ea85-145">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="4ea85-146">Un altro strumento che può essere usato è Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="4ea85-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="4ea85-147">Altre informazioni su Storage Explorer sono reperibili facendo clic sul collegamento seguente: [Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="4ea85-147">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ea85-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4ea85-148">Next steps</span></span>

<span data-ttu-id="4ea85-149">Se sono state modificate le impostazioni che arrestano la connettività VPN, vedere [Gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) per tenere traccia del gruppo di sicurezza di rete e delle regole di sicurezza in questione.</span><span class="sxs-lookup"><span data-stu-id="4ea85-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
