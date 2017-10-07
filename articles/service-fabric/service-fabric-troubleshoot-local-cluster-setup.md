---
title: aaaTroubleshoot l'installazione del cluster di Service Fabric locale | Documenti Microsoft
description: In questo articolo viene illustrata una serie di suggerimenti per la risoluzione dei problemi del cluster di sviluppo locale
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="b0187-103">Risolvere i problemi di configurazione del cluster di sviluppo locale</span><span class="sxs-lookup"><span data-stu-id="b0187-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="b0187-104">Se verifica un problema durante l'interazione con il cluster di sviluppo di Azure Service Fabric locale, esaminare hello seguenti suggerimenti per le soluzioni possibili.</span><span class="sxs-lookup"><span data-stu-id="b0187-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review hello following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="b0187-105">Errori di configurazione del cluster</span><span class="sxs-lookup"><span data-stu-id="b0187-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="b0187-106">Impossibile pulire i log di Infrastruttura di servizi</span><span class="sxs-lookup"><span data-stu-id="b0187-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="b0187-107">Problema</span><span class="sxs-lookup"><span data-stu-id="b0187-107">Problem</span></span>
<span data-ttu-id="b0187-108">Durante l'esecuzione di script DevClusterSetup hello, viene visualizzato un errore simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b0187-108">While running hello DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="b0187-109">Soluzione</span><span class="sxs-lookup"><span data-stu-id="b0187-109">Solution</span></span>
<span data-ttu-id="b0187-110">Finestra di PowerShell corrente hello, chiudere e aprire una nuova finestra di PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b0187-110">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="b0187-111">Dovrebbe ora essere toosuccessfully in grado di eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="b0187-111">You should now be able toosuccessfully run hello script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="b0187-112">Errori di connessione del cluster</span><span class="sxs-lookup"><span data-stu-id="b0187-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="b0187-113">Cmdlet di PowerShell di Service Fabric non sono riconosciute in Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0187-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="b0187-114">Problema</span><span class="sxs-lookup"><span data-stu-id="b0187-114">Problem</span></span>
<span data-ttu-id="b0187-115">Se si tenta toorun qualsiasi hello cmdlet PowerShell di Service Fabric, ad esempio `Connect-ServiceFabricCluster` in una finestra di PowerShell di Azure, ha esito negativo, indicante che tale cmdlet hello non è riconosciuto.</span><span class="sxs-lookup"><span data-stu-id="b0187-115">If you try toorun any of hello Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that hello cmdlet is not recognized.</span></span> <span data-ttu-id="b0187-116">motivo Hello è che Azure PowerShell utilizza versione a 32 bit hello di Windows PowerShell (anche in versioni del sistema operativo a 64 bit), mentre i cmdlet di Service Fabric hello funzionano solo in ambienti a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="b0187-116">hello reason for this is that Azure PowerShell uses hello 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas hello Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="b0187-117">Soluzione</span><span class="sxs-lookup"><span data-stu-id="b0187-117">Solution</span></span>
<span data-ttu-id="b0187-118">Eseguire sempre i cmdlet di Service Fabric direttamente da Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b0187-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="b0187-119">più recente di Azure PowerShell Hello non viene creato un collegamento speciale, pertanto questa situazione non dovrebbe verificarsi.</span><span class="sxs-lookup"><span data-stu-id="b0187-119">hello latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="b0187-120">Eccezione di inizializzazione del tipo</span><span class="sxs-lookup"><span data-stu-id="b0187-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="b0187-121">Problema</span><span class="sxs-lookup"><span data-stu-id="b0187-121">Problem</span></span>
<span data-ttu-id="b0187-122">Quando ci si connette toohello cluster in PowerShell, viene visualizzato l'errore hello TypeInitializationException per System.Fabric.Common.AppTrace.</span><span class="sxs-lookup"><span data-stu-id="b0187-122">When you are connecting toohello cluster in PowerShell, you see hello error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="b0187-123">Soluzione</span><span class="sxs-lookup"><span data-stu-id="b0187-123">Solution</span></span>
<span data-ttu-id="b0187-124">La variabile di percorso non è stata impostata correttamente durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="b0187-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="b0187-125">Disconnettersi da Windows e accedere nuovamente.</span><span class="sxs-lookup"><span data-stu-id="b0187-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="b0187-126">Il percorso risulterà aggiornato.</span><span class="sxs-lookup"><span data-stu-id="b0187-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="b0187-127">La connessione del cluster ha esito negativo con il messaggio "L’oggetto è chiuso"</span><span class="sxs-lookup"><span data-stu-id="b0187-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="b0187-128">Problema</span><span class="sxs-lookup"><span data-stu-id="b0187-128">Problem</span></span>
<span data-ttu-id="b0187-129">Una chiamata tooConnect-ServiceFabricCluster genera un errore simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b0187-129">A call tooConnect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="b0187-130">Soluzione</span><span class="sxs-lookup"><span data-stu-id="b0187-130">Solution</span></span>
<span data-ttu-id="b0187-131">Finestra di PowerShell corrente hello, chiudere e aprire una nuova finestra di PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b0187-131">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="b0187-132">A questo punto dovrebbe essere in grado di connettersi toosuccessfully.</span><span class="sxs-lookup"><span data-stu-id="b0187-132">You should now be able toosuccessfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="b0187-133">Eccezione di connessione a Fabric negata</span><span class="sxs-lookup"><span data-stu-id="b0187-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="b0187-134">Problema</span><span class="sxs-lookup"><span data-stu-id="b0187-134">Problem</span></span>
<span data-ttu-id="b0187-135">Durante il debug da Visual Studio, si verifica un errore FabricConnectionDeniedException.</span><span class="sxs-lookup"><span data-stu-id="b0187-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="b0187-136">Soluzione</span><span class="sxs-lookup"><span data-stu-id="b0187-136">Solution</span></span>
<span data-ttu-id="b0187-137">In genere questo errore si verifica quando si tenta un processo host del servizio toostart manualmente, anziché consentire hello Service Fabric runtime toostart per.</span><span class="sxs-lookup"><span data-stu-id="b0187-137">This error usually occurs when you try toostart a service host process manually, rather than allowing hello Service Fabric runtime toostart it for you.</span></span>

<span data-ttu-id="b0187-138">Assicurarsi di non disporre di progetti di servizio impostati come progetti di avvio nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="b0187-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="b0187-139">Solo i progetti di applicazione di Infrastruttura di servizi devono essere impostati come progetti di avvio.</span><span class="sxs-lookup"><span data-stu-id="b0187-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="b0187-140">Se, dopo l'installazione, il cluster locale inizia toobehave in modo anomalo, è possibile reimpostarlo utilizzando un'applicazione hello cluster locale manager sistema barra delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b0187-140">If, following setup, your local cluster begins toobehave abnormally, you can reset it using hello local cluster manager system tray application.</span></span> <span data-ttu-id="b0187-141">Questo rimuove hello cluster esistente e impostare uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="b0187-141">This removes hello existing cluster and set up a new one.</span></span> <span data-ttu-id="b0187-142">Tenere presente che verranno rimosse anche tutte le applicazioni distribuite e i dati associati.</span><span class="sxs-lookup"><span data-stu-id="b0187-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b0187-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b0187-143">Next steps</span></span>
* [<span data-ttu-id="b0187-144">Comprendere e risolvere i problemi del cluster con report di integrità del sistema</span><span class="sxs-lookup"><span data-stu-id="b0187-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="b0187-145">Visualizzare il cluster con Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="b0187-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

