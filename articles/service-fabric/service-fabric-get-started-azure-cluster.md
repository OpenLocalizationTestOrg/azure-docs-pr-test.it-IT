---
title: aaaSet di un cluster di Azure Service Fabric | Documenti Microsoft
description: Guida introduttiva. Creare un cluster Windows o Linux di Service Fabric in Azure.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a><span data-ttu-id="93060-103">Creare il primo cluster di Service Fabric di Azure</span><span class="sxs-lookup"><span data-stu-id="93060-103">Create your first Service Fabric cluster on Azure</span></span>
<span data-ttu-id="93060-104">Un [cluster di Service Fabric](service-fabric-deploy-anywhere.md) è un set di computer fisici o macchine virtuali connesse tramite rete in cui vengono distribuiti e gestiti i microservizi.</span><span class="sxs-lookup"><span data-stu-id="93060-104">A [Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual or physical machines into which your microservices are deployed and managed.</span></span> <span data-ttu-id="93060-105">Questa Guida rapida consente di un cluster di cinque nodi, in esecuzione su Windows o Linux, tramite hello toocreate [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) o [portale di Azure](http://portal.azure.com) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="93060-105">This quickstart helps you toocreate a five-node cluster, running on either Windows or Linux, through hello [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) or [Azure portal](http://portal.azure.com) in just a few minutes.</span></span>  

<span data-ttu-id="93060-106">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="93060-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


## <a name="use-hello-azure-portal"></a><span data-ttu-id="93060-107">Utilizzare hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="93060-107">Use hello Azure portal</span></span>

<span data-ttu-id="93060-108">Accedere al portale di Azure toohello [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="93060-108">Log in toohello Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

### <a name="create-hello-cluster"></a><span data-ttu-id="93060-109">Creare il cluster hello</span><span class="sxs-lookup"><span data-stu-id="93060-109">Create hello cluster</span></span>

1. <span data-ttu-id="93060-110">Fare clic su hello **New** pulsante disponibile nella hello angolo superiore sinistro del portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="93060-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>
2. <span data-ttu-id="93060-111">Selezionare **calcolo** da hello **New** blade e quindi selezionare **Cluster di Service Fabric** da hello **calcolo** blade.</span><span class="sxs-lookup"><span data-stu-id="93060-111">Select **Compute** from hello **New** blade and then select **Service Fabric Cluster** from hello **Compute** blade.</span></span>
3. <span data-ttu-id="93060-112">Compilare hello Service Fabric **nozioni di base** form.</span><span class="sxs-lookup"><span data-stu-id="93060-112">Fill out hello Service Fabric **Basics** form.</span></span> <span data-ttu-id="93060-113">Per **del sistema operativo**, selezionare la versione hello di Windows o Linux desiderato hello toorun i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="93060-113">For **Operating system**, select hello version of Windows or Linux you want hello cluster nodes toorun.</span></span> <span data-ttu-id="93060-114">nome utente Hello e la password immessa in questo caso è toolog utilizzati nella macchina virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="93060-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="93060-115">Per **Gruppo di risorse** creare un nuovo gruppo.</span><span class="sxs-lookup"><span data-stu-id="93060-115">For **Resource group**, create a new one.</span></span> <span data-ttu-id="93060-116">Un gruppo di risorse è un contenitore logico in cui vengono create e gestite collettivamente le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="93060-116">A resource group is a logical container into which Azure resources are created and collectively managed.</span></span> <span data-ttu-id="93060-117">Al termine fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="93060-117">When complete, click **OK**.</span></span>

    ![Output installazione del cluster][cluster-setup-basics]

4. <span data-ttu-id="93060-119">Compilare hello **configurazione Cluster** form.</span><span class="sxs-lookup"><span data-stu-id="93060-119">Fill out hello **Cluster configuration** form.</span></span>  <span data-ttu-id="93060-120">Per **Numero di tipi di nodo** immettere "1".</span><span class="sxs-lookup"><span data-stu-id="93060-120">For **Node type count**, enter "1".</span></span>

5. <span data-ttu-id="93060-121">Selezionare **il tipo di nodo 1 (principale)** e compilare hello **configurazione del tipo di nodo** form.</span><span class="sxs-lookup"><span data-stu-id="93060-121">Select **Node type 1 (Primary)** and fill out hello **Node type configuration** form.</span></span>  <span data-ttu-id="93060-122">Immettere un nome di tipo di nodo e impostare hello [il livello di durabilità](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) troppo "Bronze".</span><span class="sxs-lookup"><span data-stu-id="93060-122">Enter a node type name and set hello [Durability tier](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) too"Bronze."</span></span>  <span data-ttu-id="93060-123">Selezionare una dimensione di VM.</span><span class="sxs-lookup"><span data-stu-id="93060-123">Select a VM size.</span></span>

    <span data-ttu-id="93060-124">Dimensioni VM hello, il numero di macchine virtuali, gli endpoint personalizzati, di definire tipi di nodo e altre impostazioni per le macchine virtuali di quel tipo di hello.</span><span class="sxs-lookup"><span data-stu-id="93060-124">Node types define hello VM size, number of VMs, custom endpoints, and other settings for hello VMs of that type.</span></span> <span data-ttu-id="93060-125">Ogni tipo di nodo definito è configurato come un set di scalabilità della macchina virtuale separata, ovvero toodeploy usato e le macchine virtuali gestite come un set.</span><span class="sxs-lookup"><span data-stu-id="93060-125">Each node type defined is set up as a separate virtual machine scale set, which is used toodeploy and managed virtual machines as a set.</span></span> <span data-ttu-id="93060-126">Ogni tipo di nodo può essere aumentato o ridotto in modo indipendente, avere diversi set di porte aperte e avere metriche per la capacità diverse.</span><span class="sxs-lookup"><span data-stu-id="93060-126">Each node type can be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>  <span data-ttu-id="93060-127">Hello prima o primario, tipo di nodo è in servizi di sistema di Service Fabric sono ospitati e devono avere cinque o più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="93060-127">hello first, or primary, node type is where Service Fabric system services are hosted and must have five or more VMs.</span></span>

    <span data-ttu-id="93060-128">La [pianificazione della capacità](service-fabric-cluster-capacity.md) è un passaggio importante per qualsiasi distribuzione di produzione.</span><span class="sxs-lookup"><span data-stu-id="93060-128">For any production deployment, [capacity planning](service-fabric-cluster-capacity.md) is an important step.</span></span>  <span data-ttu-id="93060-129">Per questa Guida introduttiva, tuttavia, non vengono eseguite applicazioni, quindi selezionare una VM con dimensioni *DS1_v2 Standard*.</span><span class="sxs-lookup"><span data-stu-id="93060-129">For this quick start, however, you aren't running applications so select a *DS1_v2 Standard* VM size.</span></span>  <span data-ttu-id="93060-130">Selezionare "Argento" per hello [livello di affidabilità](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) e una scala di macchina virtuale iniziale imposta la capacità di 5.</span><span class="sxs-lookup"><span data-stu-id="93060-130">Select "Silver" for hello [reliability tier](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) and an initial virtual machine scale set capacity of 5.</span></span>  

    <span data-ttu-id="93060-131">Endpoint personalizzati aprono le porte nel servizio di bilanciamento carico di Azure hello in modo che sia possibile connettersi ad applicazioni in esecuzione nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="93060-131">Custom endpoints open up ports in hello Azure load balancer so that you can connect with applications running on hello cluster.</span></span>  <span data-ttu-id="93060-132">Immettere "80, 8172" tooopen le porte 80 e 8172.</span><span class="sxs-lookup"><span data-stu-id="93060-132">Enter "80, 8172" tooopen up ports 80 and 8172.</span></span>

    <span data-ttu-id="93060-133">Non archiviare hello **configurare le impostazioni avanzate** nella quale viene utilizzata per la personalizzazione di endpoint di gestione di TCP o HTTP, gli intervalli di porte di applicazione, [vincoli di posizionamento](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), e [capacità proprietà](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="93060-133">Do not check hello **Configure advanced settings** box, which is used for customizing TCP/HTTP management endpoints, application port ranges, [placement constraints](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), and [capacity properties](service-fabric-cluster-resource-manager-metrics.md).</span></span>    

    <span data-ttu-id="93060-134">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="93060-134">Select **OK**.</span></span>

6. <span data-ttu-id="93060-135">In hello **configurazione Cluster** modulo, impostare **diagnostica** troppo**su**.</span><span class="sxs-lookup"><span data-stu-id="93060-135">In hello **Cluster configuration** form, set **Diagnostics** too**On**.</span></span>  <span data-ttu-id="93060-136">Per questa Guida rapida, non è necessario tooenter qualsiasi [infrastruttura impostazione](service-fabric-cluster-fabric-settings.md) proprietà.</span><span class="sxs-lookup"><span data-stu-id="93060-136">For this quickstart, you do not need tooenter any [fabric setting](service-fabric-cluster-fabric-settings.md) properties.</span></span>  <span data-ttu-id="93060-137">In **versione di Fabric**selezionare **automatica** modalità di aggiornamento in modo che Microsoft aggiorna automaticamente la versione hello hello dell'infrastruttura di esecuzione del codice cluster hello.</span><span class="sxs-lookup"><span data-stu-id="93060-137">In **Fabric version**, select **Automatic** upgrade mode so that Microsoft automatically updates hello version of hello fabric code running hello cluster.</span></span>  <span data-ttu-id="93060-138">Impostare la modalità di hello troppo**manuale** se si desidera troppo[scegliere una versione supportata](service-fabric-cluster-upgrade.md) tooupgrade per.</span><span class="sxs-lookup"><span data-stu-id="93060-138">Set hello mode too**Manual** if you want too[choose a supported version](service-fabric-cluster-upgrade.md) tooupgrade to.</span></span> 

    ![Configurazione del tipo di nodo][node-type-config]

    <span data-ttu-id="93060-140">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="93060-140">Select **OK**.</span></span>

7. <span data-ttu-id="93060-141">Compilare hello **sicurezza** form.</span><span class="sxs-lookup"><span data-stu-id="93060-141">Fill out hello **Security** form.</span></span>  <span data-ttu-id="93060-142">Per questa Guida introduttiva selezionare **Senza protezione**.</span><span class="sxs-lookup"><span data-stu-id="93060-142">For this quick start select **Unsecure**.</span></span>  <span data-ttu-id="93060-143">È altamente consigliabile toocreate un cluster protetto per i carichi di lavoro, tuttavia, poiché chiunque in modo anonimo può connettersi cluster non sicuri tooan ed eseguire operazioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="93060-143">It is highly recommended toocreate a secure cluster for production workloads, however, since anyone can anonymously connect tooan unsecure cluster and perform management operations.</span></span>  

    <span data-ttu-id="93060-144">I certificati vengono usati in Service Fabric tooprovide autenticazione e crittografia toosecure vari aspetti di un cluster e le relative applicazioni.</span><span class="sxs-lookup"><span data-stu-id="93060-144">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="93060-145">Per altre informazioni sull'uso dei certificati in Service Fabric, vedere [Scenari di sicurezza di un cluster di Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="93060-145">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md).</span></span>  <span data-ttu-id="93060-146">mediante Azure Active Directory o tooset i certificati per la protezione delle applicazioni, l'autenticazione utente tooenable [creare un cluster da un modello di gestione risorse](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="93060-146">tooenable user authentication using Azure Active Directory or tooset up certificates for application security, [create a cluster from a Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span>

    <span data-ttu-id="93060-147">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="93060-147">Select **OK**.</span></span>

8. <span data-ttu-id="93060-148">Riepilogo hello di revisione.</span><span class="sxs-lookup"><span data-stu-id="93060-148">Review hello summary.</span></span>  <span data-ttu-id="93060-149">Se si desidera toodownload un modello di gestione delle risorse compilato in base alle impostazioni di hello immesso, selezionare **Scarica modello e i parametri**.</span><span class="sxs-lookup"><span data-stu-id="93060-149">If you'd like toodownload a Resource Manager template built from hello settings you entered, select **Download template and parameters**.</span></span>  <span data-ttu-id="93060-150">Selezionare **crea** cluster hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="93060-150">Select **Create** toocreate hello cluster.</span></span>

    <span data-ttu-id="93060-151">È possibile visualizzare lo stato di avanzamento di hello creazione nelle notifiche hello.</span><span class="sxs-lookup"><span data-stu-id="93060-151">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="93060-152">(Fare clic sull'icona di campanello"hello" nella barra di stato hello in alto hello destra dello schermo). Se fa clic su **Pin tooStartboard** durante la creazione di cluster hello, vedrai **la distribuzione di Cluster di Service Fabric** bloccato toohello **avviare** Lavagna.</span><span class="sxs-lookup"><span data-stu-id="93060-152">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-cluster-status"></a><span data-ttu-id="93060-153">Visualizzare lo stato del cluster</span><span class="sxs-lookup"><span data-stu-id="93060-153">View cluster status</span></span>
<span data-ttu-id="93060-154">Una volta creato il cluster, è possibile controllare il cluster in hello **Panoramica** pannello nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="93060-154">Once your cluster is created, you can inspect your cluster in hello **Overview** blade in hello portal.</span></span> <span data-ttu-id="93060-155">È ora possibile visualizzare i dettagli di hello del cluster nel dashboard di hello, tra cui endpoint pubblico del cluster hello e tooService un collegamento Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="93060-155">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

![Stato del cluster][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a><span data-ttu-id="93060-157">Visualizzare i cluster hello tramite Service Fabric explorer</span><span class="sxs-lookup"><span data-stu-id="93060-157">Visualize hello cluster using Service Fabric explorer</span></span>
<span data-ttu-id="93060-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) rappresenta un ottimo strumento per la visualizzazione del cluster e la gestione delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="93060-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="93060-159">Service Fabric Explorer è un servizio in esecuzione nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="93060-159">Service Fabric Explorer is a service that runs in hello cluster.</span></span>  <span data-ttu-id="93060-160">Diritti di accesso usando un browser web, fare clic su hello **Service Fabric Explorer** collegamento del cluster hello **Panoramica** hello portale.</span><span class="sxs-lookup"><span data-stu-id="93060-160">Access it using a web browser by clicking hello **Service Fabric Explorer** link of hello cluster **Overview** page in hello portal.</span></span>  <span data-ttu-id="93060-161">È inoltre possibile immettere l'indirizzo hello direttamente nel browser hello: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span><span class="sxs-lookup"><span data-stu-id="93060-161">You can also enter hello address directly into hello browser: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span></span>

<span data-ttu-id="93060-162">dashboard del cluster Hello viene fornita una panoramica del cluster, incluso un riepilogo dell'applicazione e l'integrità del nodo.</span><span class="sxs-lookup"><span data-stu-id="93060-162">hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="93060-163">visualizzazione del nodo Hello Mostra struttura fisica di hello del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="93060-163">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="93060-164">Per un determinato nodo, è possibile esaminare le applicazioni con il codice distribuito in quel nodo.</span><span class="sxs-lookup"><span data-stu-id="93060-164">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a><span data-ttu-id="93060-166">Connettere il cluster toohello tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="93060-166">Connect toohello cluster using PowerShell</span></span>
<span data-ttu-id="93060-167">Verificare che tale cluster hello è in esecuzione tramite la connessione tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="93060-167">Verify that hello cluster is running by connecting using PowerShell.</span></span>  <span data-ttu-id="93060-168">Hello modulo ServiceFabric di PowerShell viene installato con hello [Service Fabric SDK](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="93060-168">hello ServiceFabric PowerShell module is installed with hello [Service Fabric SDK](service-fabric-get-started.md).</span></span>  <span data-ttu-id="93060-169">Hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet stabilisce un cluster di toohello di connessione.</span><span class="sxs-lookup"><span data-stu-id="93060-169">hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection toohello cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
<span data-ttu-id="93060-170">Vedere [Connetti tooa sicura cluster](service-fabric-connect-to-secure-cluster.md) per altri esempi di connessione tooa cluster.</span><span class="sxs-lookup"><span data-stu-id="93060-170">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting tooa cluster.</span></span> <span data-ttu-id="93060-171">Dopo la connessione toohello cluster, utilizzare hello [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay cmdlet un elenco di nodi nelle informazioni del cluster e lo stato di hello per ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="93060-171">After connecting toohello cluster, use hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay a list of nodes in hello cluster and status information for each node.</span></span> <span data-ttu-id="93060-172">**HealthState** deve essere *OK* per ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="93060-172">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-hello-cluster"></a><span data-ttu-id="93060-173">Rimuovere il cluster hello</span><span class="sxs-lookup"><span data-stu-id="93060-173">Remove hello cluster</span></span>
<span data-ttu-id="93060-174">Un cluster di Service Fabric è costituito da altre risorse di Azure inoltre toohello risorsa del cluster stesso.</span><span class="sxs-lookup"><span data-stu-id="93060-174">A Service Fabric cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="93060-175">In modo toocompletely eliminare un cluster di Service Fabric è inoltre necessario toodelete che tutti hello è composto di risorse.</span><span class="sxs-lookup"><span data-stu-id="93060-175">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span> <span data-ttu-id="93060-176">cluster di Hello più semplice modo toodelete hello e tutte le risorse di hello che consuma è gruppo di risorse toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="93060-176">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> <span data-ttu-id="93060-177">Per altri modi toodelete un cluster o toodelete alcune risorse, ma non tutte, hello in un gruppo di risorse, vedere [eliminare un cluster](service-fabric-cluster-delete.md)</span><span class="sxs-lookup"><span data-stu-id="93060-177">For other ways toodelete a cluster or toodelete some (but not all) hello resources in a resource group, see [Delete a cluster](service-fabric-cluster-delete.md)</span></span>

<span data-ttu-id="93060-178">Eliminare un gruppo di risorse nel portale di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="93060-178">Delete a resource group in hello Azure portal:</span></span>
1. <span data-ttu-id="93060-179">Passare il cluster di Service Fabric toohello da toodelete.</span><span class="sxs-lookup"><span data-stu-id="93060-179">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
2. <span data-ttu-id="93060-180">Fare clic su hello **gruppo di risorse** nome nella pagina di essentials hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="93060-180">Click hello **Resource Group** name on hello cluster essentials page.</span></span>
3. <span data-ttu-id="93060-181">In hello **risorse gruppo Essentials** pagina, fare clic su **Elimina gruppo di risorse** e seguire le istruzioni di hello l'eliminazione di hello toocomplete pagina hello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="93060-181">In hello **Resource Group Essentials** page, click **Delete resource group** and follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>
    <span data-ttu-id="93060-182">![Eliminare il gruppo di risorse hello][cluster-delete]</span><span class="sxs-lookup"><span data-stu-id="93060-182">![Delete hello resource group][cluster-delete]</span></span>


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a><span data-ttu-id="93060-183">Usare Azure Powershell toodeploy un cluster protetto</span><span class="sxs-lookup"><span data-stu-id="93060-183">Use Azure Powershell toodeploy a secure cluster</span></span>
1. <span data-ttu-id="93060-184">Scaricare hello [Azure Powershell versione 4.0 o versione successiva del modulo](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) nel computer.</span><span class="sxs-lookup"><span data-stu-id="93060-184">Download hello [Azure Powershell module version 4.0 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) on your machine.</span></span>

2. <span data-ttu-id="93060-185">Aprire una finestra di Windows PowerShell, hello esecuzione comando seguente.</span><span class="sxs-lookup"><span data-stu-id="93060-185">Open a Windows PowerShell window, Run hello following command.</span></span> 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    <span data-ttu-id="93060-186">Viene visualizzata un output simile toohello.</span><span class="sxs-lookup"><span data-stu-id="93060-186">You should see an output similar toohello following.</span></span>

    ![Elenco PS][ps-list]

3. <span data-ttu-id="93060-188">Account di accesso tooAzure e toowhich sottoscrizione selezionare hello si desidera toocreate hello cluster</span><span class="sxs-lookup"><span data-stu-id="93060-188">Login tooAzure and Select hello subscription toowhich you want toocreate hello cluster</span></span>

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. <span data-ttu-id="93060-189">Esecuzione hello successivo comando toonow creare un cluster protetto.</span><span class="sxs-lookup"><span data-stu-id="93060-189">Run hello following command toonow create a secure cluster.</span></span> <span data-ttu-id="93060-190">Non dimenticare parametri hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="93060-190">Do not forget toocustomize hello parameters.</span></span> 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    <span data-ttu-id="93060-191">comando Hello può richiedere da toocomplete minuti too30 di 10 minuti, alla fine di hello di esso, è necessario ottenere una simile toohello seguenti di output.</span><span class="sxs-lookup"><span data-stu-id="93060-191">hello command can take anywhere from 10 minutes too30 minutes toocomplete, at hello end of it, you should get an output similar toohello following.</span></span> <span data-ttu-id="93060-192">output di Hello dispone di informazioni sul certificato hello, KeyVault in cui sono stati caricati, hello e hello cartella locale in cui copiare il certificato di hello.</span><span class="sxs-lookup"><span data-stu-id="93060-192">hello output has information about hello certificate, hello KeyVault where it was uploaded to, and hello local folder where hello certificate is copied.</span></span> 

    ![Output PS][ps-out]

5. <span data-ttu-id="93060-194">Copia output intero hello e salvare il file di testo tooa dobbiamo toorefer tooit.</span><span class="sxs-lookup"><span data-stu-id="93060-194">Copy hello entire output and save tooa text file as we need toorefer tooit.</span></span> <span data-ttu-id="93060-195">Prendere nota di hello dall'output di hello le seguenti informazioni.</span><span class="sxs-lookup"><span data-stu-id="93060-195">Make a note of hello following information from hello output.</span></span> 

    - <span data-ttu-id="93060-196">**CertificateSavedLocalPath**: c:\mycertificates\mycluster20170504141137.pfx</span><span class="sxs-lookup"><span data-stu-id="93060-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span></span>
    - <span data-ttu-id="93060-197">**CertificateThumbprint**: C4C1E541AD512B8065280292A8BA6079C3F26F10</span><span class="sxs-lookup"><span data-stu-id="93060-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span></span>
    - <span data-ttu-id="93060-198">**ManagementEndpoint**: https://mycluster.southcentralus.cloudapp.azure.com:19080</span><span class="sxs-lookup"><span data-stu-id="93060-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span></span>
    - <span data-ttu-id="93060-199">**ClientConnectionEndpointPort**: 19000</span><span class="sxs-lookup"><span data-stu-id="93060-199">**ClientConnectionEndpointPort** : 19000</span></span>

### <a name="install-hello-certificate-on-your-local-machine"></a><span data-ttu-id="93060-200">Installare il certificato di hello sul computer locale</span><span class="sxs-lookup"><span data-stu-id="93060-200">Install hello certificate on your local machine</span></span>
  
<span data-ttu-id="93060-201">tooconnect toohello cluster, è necessario il certificato di hello tooinstall nell'archivio personale (My) hello dell'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="93060-201">tooconnect toohello cluster, you need tooinstall hello certificate into hello Personal (My) store of hello current user.</span></span> 

<span data-ttu-id="93060-202">Eseguire hello seguente PowerShell</span><span class="sxs-lookup"><span data-stu-id="93060-202">Run hello following PowerShell</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

<span data-ttu-id="93060-203">Si è ora pronto tooconnect tooyour sicura cluster.</span><span class="sxs-lookup"><span data-stu-id="93060-203">You are now ready tooconnect tooyour secure cluster.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="93060-204">Connettere il cluster protetto di tooa</span><span class="sxs-lookup"><span data-stu-id="93060-204">Connect tooa secure cluster</span></span> 

<span data-ttu-id="93060-205">Eseguire hello cluster sicuro tooa tooconnect comando PowerShell seguente.</span><span class="sxs-lookup"><span data-stu-id="93060-205">Run hello following PowerShell command tooconnect tooa secure cluster.</span></span> <span data-ttu-id="93060-206">dettagli del certificato Hello devono corrispondere a un certificato che è stato utilizzato tooset di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="93060-206">hello certificate details must match a certificate that was used tooset up hello cluster.</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


<span data-ttu-id="93060-207">Hello seguente esempio mostra hello parametri completed:</span><span class="sxs-lookup"><span data-stu-id="93060-207">hello following example shows hello completed parameters:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="93060-208">Eseguire hello seguente toocheck comando che si è connessi e hello cluster è integro.</span><span class="sxs-lookup"><span data-stu-id="93060-208">Run hello following command toocheck that you are connected and hello cluster is healthy.</span></span>

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a><span data-ttu-id="93060-209">Pubblicare il cluster tooyour app da Visual Studio</span><span class="sxs-lookup"><span data-stu-id="93060-209">Publish your apps tooyour cluster from Visual Studio</span></span>

<span data-ttu-id="93060-210">Ora che configuri un cluster di Azure, è possibile pubblicare il tooit di applicazioni da Visual Studio dal seguente hello [pubblica tooan cluster](service-fabric-publish-app-remote-cluster.md) documento.</span><span class="sxs-lookup"><span data-stu-id="93060-210">Now that you have set up an Azure cluster, you can publish your applications tooit from Visual Studio by following hello [Publish tooan cluster](service-fabric-publish-app-remote-cluster.md) document.</span></span> 

### <a name="remove-hello-cluster"></a><span data-ttu-id="93060-211">Rimuovere il cluster hello</span><span class="sxs-lookup"><span data-stu-id="93060-211">Remove hello cluster</span></span>
<span data-ttu-id="93060-212">Un cluster è costituito da altre risorse di Azure inoltre toohello risorsa del cluster stesso.</span><span class="sxs-lookup"><span data-stu-id="93060-212">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="93060-213">cluster di Hello più semplice modo toodelete hello e tutte le risorse di hello che consuma è gruppo di risorse toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="93060-213">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a><span data-ttu-id="93060-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="93060-214">Next steps</span></span>
<span data-ttu-id="93060-215">Una volta impostati un cluster di sviluppo, provare seguente hello:</span><span class="sxs-lookup"><span data-stu-id="93060-215">Now that you have set up a development cluster, try hello following:</span></span>
* [<span data-ttu-id="93060-216">Creare un cluster sicuro nel portale di hello</span><span class="sxs-lookup"><span data-stu-id="93060-216">Create a secure cluster in hello portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="93060-217">Creare un cluster da un modello</span><span class="sxs-lookup"><span data-stu-id="93060-217">Create a cluster from a template</span></span>](service-fabric-cluster-creation-via-arm.md) 
* [<span data-ttu-id="93060-218">Distribuire le app tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="93060-218">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
