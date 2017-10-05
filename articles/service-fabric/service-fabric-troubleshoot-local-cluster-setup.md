---
title: Risoluzione dei problemi di installazione locale del cluster di Service Fabric | Documentazione Microsoft
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
ms.openlocfilehash: aa393f884b564cee81fcf75cc2eff895efea9471
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="3afcf-103">Risolvere i problemi di configurazione del cluster di sviluppo locale</span><span class="sxs-lookup"><span data-stu-id="3afcf-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="3afcf-104">Se si verifica un problema durante l'interazione con il cluster di sviluppo di Service Fabric di Azure locale, esaminare i suggerimenti seguenti per possibili soluzioni.</span><span class="sxs-lookup"><span data-stu-id="3afcf-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review the following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="3afcf-105">Errori di configurazione del cluster</span><span class="sxs-lookup"><span data-stu-id="3afcf-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="3afcf-106">Impossibile pulire i log di Infrastruttura di servizi</span><span class="sxs-lookup"><span data-stu-id="3afcf-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="3afcf-107">Problema</span><span class="sxs-lookup"><span data-stu-id="3afcf-107">Problem</span></span>
<span data-ttu-id="3afcf-108">Quando si esegue lo script DevClusterSetup, viene visualizzato un errore simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3afcf-108">While running the DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held to items in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="3afcf-109">Soluzione</span><span class="sxs-lookup"><span data-stu-id="3afcf-109">Solution</span></span>
<span data-ttu-id="3afcf-110">Chiudere la finestra di PowerShell corrente e aprire una nuova finestra di PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="3afcf-110">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="3afcf-111">Ora dovrebbe essere possibile eseguire correttamente lo script.</span><span class="sxs-lookup"><span data-stu-id="3afcf-111">You should now be able to successfully run the script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="3afcf-112">Errori di connessione del cluster</span><span class="sxs-lookup"><span data-stu-id="3afcf-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="3afcf-113">Cmdlet di PowerShell di Service Fabric non sono riconosciute in Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3afcf-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="3afcf-114">Problema</span><span class="sxs-lookup"><span data-stu-id="3afcf-114">Problem</span></span>
<span data-ttu-id="3afcf-115">Se si tenta di eseguire cmdlet di PowerShell di Service Fabric, ad esempio `Connect-ServiceFabricCluster` in una finestra di Azure PowerShell, l'operazione non va a buon fine e si viene informati del mancato riconoscimento del cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3afcf-115">If you try to run any of the Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that the cmdlet is not recognized.</span></span> <span data-ttu-id="3afcf-116">Il motivo è che Azure PowerShell utilizza la versione a 32 bit di Windows PowerShell (anche le versioni del sistema operativo a 64 bit), mentre i cmdlet di Service Fabric funzionano solo in ambienti a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="3afcf-116">The reason for this is that Azure PowerShell uses the 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas the Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="3afcf-117">Soluzione</span><span class="sxs-lookup"><span data-stu-id="3afcf-117">Solution</span></span>
<span data-ttu-id="3afcf-118">Eseguire sempre i cmdlet di Service Fabric direttamente da Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3afcf-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="3afcf-119">La versione più recente di Azure PowerShell non crea un collegamento speciale, pertanto questa situazione non dovrebbe più verificarsi.</span><span class="sxs-lookup"><span data-stu-id="3afcf-119">The latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="3afcf-120">Eccezione di inizializzazione del tipo</span><span class="sxs-lookup"><span data-stu-id="3afcf-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="3afcf-121">Problema</span><span class="sxs-lookup"><span data-stu-id="3afcf-121">Problem</span></span>
<span data-ttu-id="3afcf-122">Quando ci si connette al cluster in PowerShell, viene visualizzato l'errore TypeInitializationException per System.Fabric.Common.AppTrace.</span><span class="sxs-lookup"><span data-stu-id="3afcf-122">When you are connecting to the cluster in PowerShell, you see the error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="3afcf-123">Soluzione</span><span class="sxs-lookup"><span data-stu-id="3afcf-123">Solution</span></span>
<span data-ttu-id="3afcf-124">La variabile di percorso non è stata impostata correttamente durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="3afcf-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="3afcf-125">Disconnettersi da Windows e accedere nuovamente.</span><span class="sxs-lookup"><span data-stu-id="3afcf-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="3afcf-126">Il percorso risulterà aggiornato.</span><span class="sxs-lookup"><span data-stu-id="3afcf-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="3afcf-127">La connessione del cluster ha esito negativo con il messaggio "L’oggetto è chiuso"</span><span class="sxs-lookup"><span data-stu-id="3afcf-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="3afcf-128">Problema</span><span class="sxs-lookup"><span data-stu-id="3afcf-128">Problem</span></span>
<span data-ttu-id="3afcf-129">Una chiamata a Connect-ServiceFabricCluster ha esito negativo con un errore simile a quello indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3afcf-129">A call to Connect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : The object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="3afcf-130">Soluzione</span><span class="sxs-lookup"><span data-stu-id="3afcf-130">Solution</span></span>
<span data-ttu-id="3afcf-131">Chiudere la finestra di PowerShell corrente e aprire una nuova finestra di PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="3afcf-131">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="3afcf-132">Ora dovrebbe essere possibile effettuare la connessione.</span><span class="sxs-lookup"><span data-stu-id="3afcf-132">You should now be able to successfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="3afcf-133">Eccezione di connessione a Fabric negata</span><span class="sxs-lookup"><span data-stu-id="3afcf-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="3afcf-134">Problema</span><span class="sxs-lookup"><span data-stu-id="3afcf-134">Problem</span></span>
<span data-ttu-id="3afcf-135">Durante il debug da Visual Studio, si verifica un errore FabricConnectionDeniedException.</span><span class="sxs-lookup"><span data-stu-id="3afcf-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="3afcf-136">Soluzione</span><span class="sxs-lookup"><span data-stu-id="3afcf-136">Solution</span></span>
<span data-ttu-id="3afcf-137">Questo errore si verifica in genere quando si tenta di avviare manualmente un processo host del servizio, anziché consentirne l'avvio automatico dal runtime di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3afcf-137">This error usually occurs when you try to start a service host process manually, rather than allowing the Service Fabric runtime to start it for you.</span></span>

<span data-ttu-id="3afcf-138">Assicurarsi di non disporre di progetti di servizio impostati come progetti di avvio nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="3afcf-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="3afcf-139">Solo i progetti di applicazione di Infrastruttura di servizi devono essere impostati come progetti di avvio.</span><span class="sxs-lookup"><span data-stu-id="3afcf-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="3afcf-140">Se, in seguito alla configurazione, il cluster locale inizia a presentare un comportamento anomalo, può essere ripristinato con l'applicazione dell'area di notifica Local Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="3afcf-140">If, following setup, your local cluster begins to behave abnormally, you can reset it using the local cluster manager system tray application.</span></span> <span data-ttu-id="3afcf-141">In questo modo viene rimosso il cluster esistente e ne viene configurato uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="3afcf-141">This removes the existing cluster and set up a new one.</span></span> <span data-ttu-id="3afcf-142">Tenere presente che verranno rimosse anche tutte le applicazioni distribuite e i dati associati.</span><span class="sxs-lookup"><span data-stu-id="3afcf-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3afcf-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3afcf-143">Next steps</span></span>
* [<span data-ttu-id="3afcf-144">Comprendere e risolvere i problemi del cluster con report di integrità del sistema</span><span class="sxs-lookup"><span data-stu-id="3afcf-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="3afcf-145">Visualizzare il cluster con Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="3afcf-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

