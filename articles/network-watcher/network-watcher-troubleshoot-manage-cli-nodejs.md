---
title: aaaTroubleshoot connessioni - CLI di Azure 1.0 e il Gateway di rete virtuale di Azure | Documenti Microsoft
description: Questa pagina viene illustrato come toouse hello Watcher di rete di Azure risolvere i problemi di Azure CLI 1.0
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
ms.openlocfilehash: a0511689d773f9c7216b0fe5470e27f754eb600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a><span data-ttu-id="64b70-103">Risolvere i problemi relativi al gateway di rete virtuale e alle connessioni tramite l'interfaccia della riga di comando 1.0 di Azure in Network Watcher di Azure</span><span class="sxs-lookup"><span data-stu-id="64b70-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="64b70-104">Portale</span><span class="sxs-lookup"><span data-stu-id="64b70-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="64b70-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="64b70-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="64b70-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="64b70-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="64b70-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="64b70-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="64b70-108">API REST</span><span class="sxs-lookup"><span data-stu-id="64b70-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="64b70-109">Watcher di rete fornisce numerose funzionalità toounderstanding in relazione le risorse di rete in Azure.</span><span class="sxs-lookup"><span data-stu-id="64b70-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="64b70-110">Una di queste funzionalità è la risoluzione dei problemi riscontrati con le risorse.</span><span class="sxs-lookup"><span data-stu-id="64b70-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="64b70-111">Risoluzione dei problemi di risorse può essere chiamato tramite il portale di hello, PowerShell, CLI o API REST.</span><span class="sxs-lookup"><span data-stu-id="64b70-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="64b70-112">Quando viene chiamato, Watcher di rete Controlla integrità hello di un Gateway di rete virtuale o una connessione e restituisce i risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="64b70-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="64b70-113">Questo articolo usa l'interfaccia della riga di comando di Azure 1.0 multipiattaforma, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="64b70-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="64b70-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="64b70-114">Before you begin</span></span>

<span data-ttu-id="64b70-115">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="64b70-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="64b70-116">Per un elenco dei tipi di gateway supportati, consultare i [tipi di gateway supportati](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="64b70-116">For a list of supported gateway types visit, [Supported Gateway types](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="64b70-117">Panoramica</span><span class="sxs-lookup"><span data-stu-id="64b70-117">Overview</span></span>

<span data-ttu-id="64b70-118">Risoluzione dei problemi di risorse consente di hello risolvere i problemi che si verificano con gateway di rete virtuale e le connessioni.</span><span class="sxs-lookup"><span data-stu-id="64b70-118">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="64b70-119">Quando viene effettuata una richiesta di risoluzione dei problemi tooresource, i registri vengono eseguite query e controllato.</span><span class="sxs-lookup"><span data-stu-id="64b70-119">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="64b70-120">Una volta completato controllo, vengono restituiti risultati hello.</span><span class="sxs-lookup"><span data-stu-id="64b70-120">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="64b70-121">Richieste di risorse, le richieste di risoluzione dei problemi sono a esecuzione prolungata, che potrebbe richiedere più minuti tooreturn un risultato.</span><span class="sxs-lookup"><span data-stu-id="64b70-121">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="64b70-122">i log di Hello dalla risoluzione dei problemi vengono archiviati in un contenitore in un account di archiviazione specificato.</span><span class="sxs-lookup"><span data-stu-id="64b70-122">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="64b70-123">Recuperare una connessione e un gateway di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="64b70-123">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="64b70-124">In questo esempio la risoluzione dei problemi delle risorse viene eseguita su una connessione.</span><span class="sxs-lookup"><span data-stu-id="64b70-124">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="64b70-125">È anche possibile passare il comando a un gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="64b70-125">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="64b70-126">Hello cmdlet riportato di seguito sono elencati hello connessioni vpn in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="64b70-126">hello following cmdlet lists hello vpn-connections in a resource group.</span></span>

```azurecli
azure network vpn-connection list -g resourceGroupName
```

<span data-ttu-id="64b70-127">È anche possibile eseguire hello comando toosee connessioni hello in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="64b70-127">You can also run hello command toosee hello connections in a subscription.</span></span>

```azurecli
azure network vpn-connection list -s subscription
```

<span data-ttu-id="64b70-128">Dopo aver creato il nome di hello della connessione di hello, è possibile eseguire questo comando tooget relativi Id di risorsa:</span><span class="sxs-lookup"><span data-stu-id="64b70-128">Once you have hello name of hello connection, you can run this command tooget its resource Id:</span></span>

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a><span data-ttu-id="64b70-129">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="64b70-129">Create a storage account</span></span>

<span data-ttu-id="64b70-130">Risoluzione dei problemi di risorse restituisce i dati sull'integrità hello della risorsa hello, consentono inoltre di salvare i registri tooa storage account toobe esaminato.</span><span class="sxs-lookup"><span data-stu-id="64b70-130">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="64b70-131">In questo passaggio viene creato un account di archiviazione. È anche possibile usare un account di archiviazione già esistente.</span><span class="sxs-lookup"><span data-stu-id="64b70-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="64b70-132">Creare account di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="64b70-132">Create hello storage account</span></span>

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. <span data-ttu-id="64b70-133">Ottiene le chiavi account di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="64b70-133">Get hello storage account keys</span></span>

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. <span data-ttu-id="64b70-134">Creare il contenitore di hello</span><span class="sxs-lookup"><span data-stu-id="64b70-134">Create hello container</span></span>

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="64b70-135">Eseguire il comando per la risoluzione dei problemi delle risorse di Network Watcher</span><span class="sxs-lookup"><span data-stu-id="64b70-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="64b70-136">Risolvere i problemi relativi alle risorse con hello `network watcher troubleshoot` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="64b70-136">You troubleshoot resources with hello `network watcher troubleshoot` cmdlet.</span></span> <span data-ttu-id="64b70-137">Viene passato a gruppo di risorse di hello cmdlet hello, nome di hello Watcher di rete, Id di connessione hello, hello hello hello Id dell'account di archiviazione hello e hello di hello percorso toohello blob toostore di risolvere i risultati in.</span><span class="sxs-lookup"><span data-stu-id="64b70-137">We pass hello cmdlet hello resource group, hello name of hello Network Watcher, hello Id of hello connection, hello Id of hello storage account, and hello path toohello blob toostore hello troubleshoot results in.</span></span>

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

<span data-ttu-id="64b70-138">Dopo aver eseguito i cmdlet di hello, Watcher di rete esamina integrità hello tooverify delle risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="64b70-138">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="64b70-139">Restituisce i risultati di hello toohello shell e archivia i log dei risultati di hello in hello account di archiviazione specificato.</span><span class="sxs-lookup"><span data-stu-id="64b70-139">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="64b70-140">Informazioni sui risultati hello</span><span class="sxs-lookup"><span data-stu-id="64b70-140">Understanding hello results</span></span>

<span data-ttu-id="64b70-141">testo dell'azione Hello vengono fornite indicazioni generali su come tooresolve hello problema.</span><span class="sxs-lookup"><span data-stu-id="64b70-141">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="64b70-142">Se è possibile eseguire un'azione per il problema di hello, viene fornito un collegamento con informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="64b70-142">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="64b70-143">In caso di hello in cui è presente alcun altro materiale sussidiario, risposta hello fornisce hello url tooopen un caso di supporto.</span><span class="sxs-lookup"><span data-stu-id="64b70-143">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="64b70-144">Per ulteriori informazioni sulle proprietà hello di risposta hello e cosa è inclusa, visitare [Panoramica monitoraggio risolvere i problemi di rete](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="64b70-144">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="64b70-145">Per istruzioni sul download di file dall'account di archiviazione di azure, consultare troppo[Introduzione all'archiviazione Blob di Azure usando .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="64b70-145">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="64b70-146">Un altro strumento che può essere usato è Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="64b70-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="64b70-147">Ulteriori informazioni su soluzioni di archiviazione sono reperibile qui in hello seguente collegamento: [Esplora archivi](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="64b70-147">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="64b70-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="64b70-148">Next steps</span></span>

<span data-ttu-id="64b70-149">Se le impostazioni sono state modificate che arresta la connettività VPN, vedere [gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack verso il basso hello rete sicurezza e gruppo di regole di sicurezza che possono essere in questione.</span><span class="sxs-lookup"><span data-stu-id="64b70-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
