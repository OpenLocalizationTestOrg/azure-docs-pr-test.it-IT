---
title: aaaTroubleshoot connessioni - PowerShell e il Gateway di rete virtuale di Azure | Documenti Microsoft
description: Questa pagina viene illustrato come toouse hello Watcher di rete di Azure risolvere i cmdlet di PowerShell
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
ms.openlocfilehash: b7dbe6e44e0fa1ea0481223a84098d7a57c068a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="d0d50-103">Risolvere i problemi relativi al gateway di rete virtuale e alle connessioni di Azure tramite PowerShell in Network Watcher di Azure</span><span class="sxs-lookup"><span data-stu-id="d0d50-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d0d50-104">Portale</span><span class="sxs-lookup"><span data-stu-id="d0d50-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="d0d50-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0d50-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="d0d50-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="d0d50-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="d0d50-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="d0d50-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="d0d50-108">API REST</span><span class="sxs-lookup"><span data-stu-id="d0d50-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="d0d50-109">Watcher di rete fornisce numerose funzionalità toounderstanding in relazione le risorse di rete in Azure.</span><span class="sxs-lookup"><span data-stu-id="d0d50-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="d0d50-110">Una di queste funzionalità è la risoluzione dei problemi riscontrati con le risorse.</span><span class="sxs-lookup"><span data-stu-id="d0d50-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="d0d50-111">Risoluzione dei problemi di risorse può essere chiamato tramite il portale di hello, PowerShell, CLI o API REST.</span><span class="sxs-lookup"><span data-stu-id="d0d50-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="d0d50-112">Quando viene chiamato, Watcher di rete Controlla integrità hello di un Gateway di rete virtuale o una connessione e restituisce i risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="d0d50-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d0d50-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="d0d50-113">Before you begin</span></span>

<span data-ttu-id="d0d50-114">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="d0d50-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="d0d50-115">Per un elenco dei tipi di gateway supportati, consultare i [tipi di gateway supportati](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="d0d50-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="d0d50-116">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d0d50-116">Overview</span></span>

<span data-ttu-id="d0d50-117">Risoluzione dei problemi di risorse consente di hello risolvere i problemi che si verificano con gateway di rete virtuale e le connessioni.</span><span class="sxs-lookup"><span data-stu-id="d0d50-117">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="d0d50-118">Quando viene effettuata una richiesta di risoluzione dei problemi tooresource, i registri vengono eseguite query e controllato.</span><span class="sxs-lookup"><span data-stu-id="d0d50-118">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="d0d50-119">Una volta completato controllo, vengono restituiti risultati hello.</span><span class="sxs-lookup"><span data-stu-id="d0d50-119">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="d0d50-120">Richieste di risorse, le richieste di risoluzione dei problemi sono a esecuzione prolungata, che potrebbe richiedere più minuti tooreturn un risultato.</span><span class="sxs-lookup"><span data-stu-id="d0d50-120">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="d0d50-121">i log di Hello dalla risoluzione dei problemi vengono archiviati in un contenitore in un account di archiviazione specificato.</span><span class="sxs-lookup"><span data-stu-id="d0d50-121">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="d0d50-122">Recuperare Network Watcher</span><span class="sxs-lookup"><span data-stu-id="d0d50-122">Retrieve Network Watcher</span></span>

<span data-ttu-id="d0d50-123">innanzitutto Hello è l'istanza di tooretrieve hello Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="d0d50-123">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="d0d50-124">Hello `$networkWatcher` variabile viene passata toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet nel passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="d0d50-124">hello `$networkWatcher` variable is passed toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="d0d50-125">Recuperare una connessione e un gateway di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="d0d50-125">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="d0d50-126">In questo esempio la risoluzione dei problemi delle risorse viene eseguita su una connessione.</span><span class="sxs-lookup"><span data-stu-id="d0d50-126">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="d0d50-127">È anche possibile passare il comando a un gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d0d50-127">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="d0d50-128">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="d0d50-128">Create a storage account</span></span>

<span data-ttu-id="d0d50-129">Risoluzione dei problemi di risorse restituisce i dati sull'integrità hello della risorsa hello, consentono inoltre di salvare i registri tooa storage account toobe esaminato.</span><span class="sxs-lookup"><span data-stu-id="d0d50-129">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="d0d50-130">In questo passaggio viene creato un account di archiviazione. È anche possibile usare un account di archiviazione già esistente.</span><span class="sxs-lookup"><span data-stu-id="d0d50-130">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="d0d50-131">Eseguire il comando per la risoluzione dei problemi delle risorse di Network Watcher</span><span class="sxs-lookup"><span data-stu-id="d0d50-131">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="d0d50-132">Risolvere i problemi relativi alle risorse con hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d0d50-132">You troubleshoot resources with hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="d0d50-133">Passiamo hello cmdlet hello Watcher di rete oggetto, Id di connessione hello hello o Gateway di rete virtuale, id di account di archiviazione hello e hello percorso toostore hello comporta.</span><span class="sxs-lookup"><span data-stu-id="d0d50-133">We pass hello cmdlet hello Network Watcher object, hello Id of hello Connection or Virtual Network Gateway, hello storage account id, and hello path toostore hello results.</span></span>

> [!NOTE]
> <span data-ttu-id="d0d50-134">Hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet è a esecuzione prolungata e potrebbe richiedere alcuni minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="d0d50-134">hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes toocomplete.</span></span>

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="d0d50-135">Dopo aver eseguito i cmdlet di hello, Watcher di rete esamina integrità hello tooverify delle risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="d0d50-135">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="d0d50-136">Restituisce i risultati di hello toohello shell e archivia i log dei risultati di hello in hello account di archiviazione specificato.</span><span class="sxs-lookup"><span data-stu-id="d0d50-136">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="d0d50-137">Informazioni sui risultati hello</span><span class="sxs-lookup"><span data-stu-id="d0d50-137">Understanding hello results</span></span>

<span data-ttu-id="d0d50-138">testo dell'azione Hello vengono fornite indicazioni generali su come tooresolve hello problema.</span><span class="sxs-lookup"><span data-stu-id="d0d50-138">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="d0d50-139">Se è possibile eseguire un'azione per il problema di hello, viene fornito un collegamento con informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="d0d50-139">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="d0d50-140">In caso di hello in cui è presente alcun altro materiale sussidiario, risposta hello fornisce hello url tooopen un caso di supporto.</span><span class="sxs-lookup"><span data-stu-id="d0d50-140">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="d0d50-141">Per ulteriori informazioni sulle proprietà hello di risposta hello e cosa è inclusa, visitare [Panoramica monitoraggio risolvere i problemi di rete](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d0d50-141">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="d0d50-142">Per istruzioni sul download di file dall'account di archiviazione di azure, consultare troppo[Introduzione all'archiviazione Blob di Azure usando .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="d0d50-142">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="d0d50-143">Un altro strumento che può essere usato è Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="d0d50-143">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="d0d50-144">Ulteriori informazioni su soluzioni di archiviazione sono reperibile qui in hello seguente collegamento: [Esplora archivi](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="d0d50-144">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0d50-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d0d50-145">Next steps</span></span>

<span data-ttu-id="d0d50-146">Se le impostazioni sono state modificate che arresta la connettività VPN, vedere [gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack verso il basso hello rete sicurezza e gruppo di regole di sicurezza che possono essere in questione.</span><span class="sxs-lookup"><span data-stu-id="d0d50-146">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
