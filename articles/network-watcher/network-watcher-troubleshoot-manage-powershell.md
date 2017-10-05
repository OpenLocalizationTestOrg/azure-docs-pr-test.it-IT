---
title: Risolvere i problemi relativi al gateway di rete virtuale e alle connessioni di Azure - PowerShell | Documentazione Microsoft
description: Questa pagina spiega come usare il cmdlet di PowerShell per risolvere i problemi in Network Watcher di Azure
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: 0bdffbac18d1d236b7674feed4dbc784e50e0ea8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="8c05f-103">Risolvere i problemi relativi al gateway di rete virtuale e alle connessioni di Azure tramite PowerShell in Network Watcher di Azure</span><span class="sxs-lookup"><span data-stu-id="8c05f-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8c05f-104">Portale</span><span class="sxs-lookup"><span data-stu-id="8c05f-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="8c05f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c05f-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="8c05f-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="8c05f-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="8c05f-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="8c05f-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="8c05f-108">API REST</span><span class="sxs-lookup"><span data-stu-id="8c05f-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="8c05f-109">Network Watcher offre numerose funzionalità che consentono di comprendere le risorse di rete in Azure.</span><span class="sxs-lookup"><span data-stu-id="8c05f-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="8c05f-110">Una di queste funzionalità è la risoluzione dei problemi riscontrati con le risorse.</span><span class="sxs-lookup"><span data-stu-id="8c05f-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="8c05f-111">La funzionalità può essere chiamata dal portale, da PowerShell, dall'interfaccia della riga di comando o dall'API REST.</span><span class="sxs-lookup"><span data-stu-id="8c05f-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="8c05f-112">Quando chiamata, Network Watcher controlla l'integrità di un gateway di rete virtuale o di una connessione e restituisce i risultati.</span><span class="sxs-lookup"><span data-stu-id="8c05f-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8c05f-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="8c05f-113">Before you begin</span></span>

<span data-ttu-id="8c05f-114">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="8c05f-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="8c05f-115">Per un elenco dei tipi di gateway supportati, consultare i [tipi di gateway supportati](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="8c05f-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="8c05f-116">Panoramica</span><span class="sxs-lookup"><span data-stu-id="8c05f-116">Overview</span></span>

<span data-ttu-id="8c05f-117">La risoluzione dei problemi delle risorse consente di risolvere i problemi che si verificano con i gateway di rete virtuale e le connessioni.</span><span class="sxs-lookup"><span data-stu-id="8c05f-117">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="8c05f-118">Quando viene inviata una richiesta di risoluzione dei problemi delle risorse, i log vengono sottoposti a query e controllati.</span><span class="sxs-lookup"><span data-stu-id="8c05f-118">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="8c05f-119">Dopo aver completato l'ispezione, vengono restituiti i risultati.</span><span class="sxs-lookup"><span data-stu-id="8c05f-119">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="8c05f-120">Le richieste di risoluzione dei problemi delle risorse sono richieste a esecuzione prolungata, che possono richiedere anche diversi minuti per restituire un risultato.</span><span class="sxs-lookup"><span data-stu-id="8c05f-120">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="8c05f-121">I log risultati vengono archiviati in un contenitore in un account di archiviazione specificato.</span><span class="sxs-lookup"><span data-stu-id="8c05f-121">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="8c05f-122">Recuperare Network Watcher</span><span class="sxs-lookup"><span data-stu-id="8c05f-122">Retrieve Network Watcher</span></span>

<span data-ttu-id="8c05f-123">Il primo passaggio consente di recuperare l'istanza di Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="8c05f-123">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="8c05f-124">La variabile `$networkWatcher` viene passata al cmdlet `Start-AzureRmNetworkWatcherResourceTroubleshooting` nel passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="8c05f-124">The `$networkWatcher` variable is passed to the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="8c05f-125">Recuperare una connessione e un gateway di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="8c05f-125">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="8c05f-126">In questo esempio la risoluzione dei problemi delle risorse viene eseguita su una connessione.</span><span class="sxs-lookup"><span data-stu-id="8c05f-126">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="8c05f-127">È anche possibile passare il comando a un gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="8c05f-127">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="8c05f-128">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="8c05f-128">Create a storage account</span></span>

<span data-ttu-id="8c05f-129">Il comando per la risoluzione dei problemi delle risorse restituisce i dati sullo stato della risorsa e salva i log in un account di archiviazione, per la successiva revisione.</span><span class="sxs-lookup"><span data-stu-id="8c05f-129">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="8c05f-130">In questo passaggio viene creato un account di archiviazione. È anche possibile usare un account di archiviazione già esistente.</span><span class="sxs-lookup"><span data-stu-id="8c05f-130">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="8c05f-131">Eseguire il comando per la risoluzione dei problemi delle risorse di Network Watcher</span><span class="sxs-lookup"><span data-stu-id="8c05f-131">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="8c05f-132">Per risolvere i problemi relativi alle risorse eseguire il cmdlet `Start-AzureRmNetworkWatcherResourceTroubleshooting`.</span><span class="sxs-lookup"><span data-stu-id="8c05f-132">You troubleshoot resources with the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="8c05f-133">Per archiviare i risultati, il cmdlet viene passato nell'oggetto Network Watcher, nell'ID della connessione o del gateway di rete virtuale, nell'ID dell'account di archiviazione e nel percorso.</span><span class="sxs-lookup"><span data-stu-id="8c05f-133">We pass the cmdlet the Network Watcher object, the Id of the Connection or Virtual Network Gateway, the storage account id, and the path to store the results.</span></span>

> [!NOTE]
> <span data-ttu-id="8c05f-134">Il cmdlet `Start-AzureRmNetworkWatcherResourceTroubleshooting` ha un'esecuzione prolungata e potrebbe richiedere alcuni minuti per il completamento.</span><span class="sxs-lookup"><span data-stu-id="8c05f-134">The `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes to complete.</span></span>

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="8c05f-135">Dopo aver eseguito il cmdlet, Network Watcher esamina la risorsa per verificarne l'integrità.</span><span class="sxs-lookup"><span data-stu-id="8c05f-135">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="8c05f-136">Restituisce quindi i risultati alla shell e archivia i log dei risultati nell'account di archiviazione specificato.</span><span class="sxs-lookup"><span data-stu-id="8c05f-136">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="8c05f-137">Informazioni sui risultati</span><span class="sxs-lookup"><span data-stu-id="8c05f-137">Understanding the results</span></span>

<span data-ttu-id="8c05f-138">Il testo dell'azione offre indicazioni generiche su come risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="8c05f-138">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="8c05f-139">Se è possibile eseguire un'azione per il problema, viene fornito un collegamento con altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="8c05f-139">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="8c05f-140">Nel caso in cui non siano presenti altre indicazioni, la risposta include l'URL per aprire una richiesta di assistenza.</span><span class="sxs-lookup"><span data-stu-id="8c05f-140">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="8c05f-141">Per altre informazioni sulle proprietà della risposta e ciò che vie è incluso, consultare la [panoramica sulla risoluzione dei problemi in Network Watcher](network-watcher-troubleshoot-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8c05f-141">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="8c05f-142">Per istruzioni sul download di file dall'account di archiviazione di Azure, consultare [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="8c05f-142">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="8c05f-143">Un altro strumento che può essere usato è Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="8c05f-143">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="8c05f-144">Altre informazioni su Storage Explorer sono reperibili facendo clic sul collegamento seguente: [Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="8c05f-144">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c05f-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8c05f-145">Next steps</span></span>

<span data-ttu-id="8c05f-146">Se sono state modificate le impostazioni che arrestano la connettività VPN, vedere [Gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) per tenere traccia del gruppo di sicurezza di rete e delle regole di sicurezza in questione.</span><span class="sxs-lookup"><span data-stu-id="8c05f-146">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
