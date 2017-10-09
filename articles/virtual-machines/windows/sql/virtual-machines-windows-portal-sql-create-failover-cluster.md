---
title: aaaSQL FCI Server - macchine virtuali di Azure | Documenti Microsoft
description: Questo articolo viene illustrato come toocreate istanza di Cluster di Failover SQL Server in macchine virtuali di Azure.
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a><span data-ttu-id="4a6f4-103">Configurare l'istanza del cluster di failover di SQL Server nelle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="4a6f4-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span></span>

<span data-ttu-id="4a6f4-104">Questo articolo viene illustrato come toocreate un SQL Server del Cluster di Failover (FCI) di istanza su macchine virtuali nel modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-104">This article explains how toocreate a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="4a6f4-105">Questa soluzione Usa [spazi di archiviazione diretta di Windows Server 2016 Datacenter edition \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) come una SAN virtuale basata su software che sincronizza l'archiviazione hello (dischi di dati) tra i nodi hello (macchine virtuali di Azure) in un Cluster di Windows.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes hello storage (data disks) between hello nodes (Azure VMs) in a Windows Cluster.</span></span> <span data-ttu-id="4a6f4-106">S2D è una novità di Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-106">S2D is new in Windows Server 2016.</span></span>

<span data-ttu-id="4a6f4-107">Hello diagramma seguente illustra la soluzione completa di hello in macchine virtuali di Azure:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-107">hello following diagram shows hello complete solution on Azure virtual machines:</span></span>

![Gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

<span data-ttu-id="4a6f4-109">Hello precedente diagramma illustra:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-109">hello preceding diagram shows:</span></span>

- <span data-ttu-id="4a6f4-110">Due macchine virtuali di Azure in un cluster di failover di Windows.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-110">Two Azure virtual machines in a Windows Failover Cluster.</span></span> <span data-ttu-id="4a6f4-111">Una macchina virtuale in un cluster di failover è detta anche *nodo del cluster* o *nodo*.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span></span>
- <span data-ttu-id="4a6f4-112">Ogni macchina virtuale ha due o più dischi dati.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-112">Each virtual machine has two or more data disks.</span></span>
- <span data-ttu-id="4a6f4-113">S2D Sincronizza i dati di hello nel disco dati hello e presenta una risorsa di archiviazione hello sincronizzato con un pool di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-113">S2D synchronizes hello data on hello data disk and presents hello synchronized storage as a storage pool.</span></span>
- <span data-ttu-id="4a6f4-114">pool di archiviazione Hello presenta un cluster di failover cluster toohello volume condiviso (CSV).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-114">hello storage pool presents a cluster shared volume (CSV) toohello failover cluster.</span></span>
- <span data-ttu-id="4a6f4-115">ruolo del cluster di SQL Server FCI Hello Usa CSV hello per le unità dati hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-115">hello SQL Server FCI cluster role uses hello CSV for hello data drives.</span></span>
- <span data-ttu-id="4a6f4-116">Un carico di Azure del servizio di bilanciamento toohold hello indirizzo IP per hello istanza cluster di failover di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-116">An Azure load balancer toohold hello IP address for hello SQL Server FCI.</span></span>
- <span data-ttu-id="4a6f4-117">Un set di disponibilità di Azure contiene tutte le risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-117">An Azure availability set holds all hello resources.</span></span>

   >[!NOTE]
   ><span data-ttu-id="4a6f4-118">Tutte le risorse di Azure sono nel diagramma hello in hello stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-118">All Azure resources are in hello diagram are in hello same resource group.</span></span>

<span data-ttu-id="4a6f4-119">Per informazioni dettagliate su S2D, vedere l'articolo relativo a [Spazi di archiviazione diretta \(S2D\) in Windows Server 2016 Datacenter Edition](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span></span>

<span data-ttu-id="4a6f4-120">S2D supporta due tipi di architettura: con convergenza e con iperconvergenza.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-120">S2D supports two types of architectures - converged and hyper-converged.</span></span> <span data-ttu-id="4a6f4-121">architettura di Hello in questo documento è iperconvergente.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-121">hello architecture in this document is hyper-converged.</span></span> <span data-ttu-id="4a6f4-122">Un archivio di hello iperconvergente infrastruttura posizioni in hello stessi server applicazione hello cluster host.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-122">A hyper-converged infrastructure places hello storage on hello same servers that host hello clustered application.</span></span> <span data-ttu-id="4a6f4-123">In questa architettura, archiviazione hello è in ogni nodo dell'istanza cluster di failover di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-123">In this architecture, hello storage is on each SQL Server FCI node.</span></span>

### <a name="example-azure-template"></a><span data-ttu-id="4a6f4-124">Modello di Azure di esempio</span><span class="sxs-lookup"><span data-stu-id="4a6f4-124">Example Azure template</span></span>

<span data-ttu-id="4a6f4-125">È possibile creare l'intera soluzione hello in Azure da un modello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-125">You can create hello entire solution in Azure from a template.</span></span> <span data-ttu-id="4a6f4-126">Un esempio di un modello è disponibile in GitHub hello [modelli di avvio rapido di Azure](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-126">An example of a template is available in hello GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span></span> <span data-ttu-id="4a6f4-127">Questo esempio non è progettato né testato per carichi di lavoro specifici.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-127">This example is not designed or tested for any specific workload.</span></span> <span data-ttu-id="4a6f4-128">È possibile eseguire hello modello toocreate una FCI di SQL Server con dominio di S2D archiviazione tooyour connesso.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-128">You can run hello template toocreate a SQL Server FCI with S2D storage connected tooyour domain.</span></span> <span data-ttu-id="4a6f4-129">È possibile valutare il modello di hello e modificarla in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-129">You can evaluate hello template, and modify it for your purposes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4a6f4-130">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="4a6f4-130">Before you begin</span></span>

<span data-ttu-id="4a6f4-131">Ci sono alcuni aspetti che occorre tooknow e un paio di aspetti che è necessario presenti prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-131">There are a few things you need tooknow and a couple of things that you need in place before you proceed.</span></span>

### <a name="what-tooknow"></a><span data-ttu-id="4a6f4-132">Quali tooknow</span><span class="sxs-lookup"><span data-stu-id="4a6f4-132">What tooknow</span></span>
<span data-ttu-id="4a6f4-133">È necessario avere una conoscenza operativa di hello seguenti tecnologie:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-133">You should have an operational understanding of hello following technologies:</span></span>

- [<span data-ttu-id="4a6f4-134">Tecnologie cluster di Windows</span><span class="sxs-lookup"><span data-stu-id="4a6f4-134">Windows cluster technologies</span></span>](http://technet.microsoft.com/library/hh831579.aspx)
-  <span data-ttu-id="4a6f4-135">[Istanze del cluster di failover di SQL Server](http://msdn.microsoft.com/library/ms189134.aspx)</span><span class="sxs-lookup"><span data-stu-id="4a6f4-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span></span>

<span data-ttu-id="4a6f4-136">Inoltre, si deve avere una conoscenza generale di hello seguenti tecnologie:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-136">Also, you should have a general understanding of hello following technologies:</span></span>

- [<span data-ttu-id="4a6f4-137">Soluzione iperconvergente che usa Spazi di archiviazione diretta in Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="4a6f4-137">Hyper-converged solution using Storage Spaces Direct in Windows Server 2016</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [<span data-ttu-id="4a6f4-138">Gruppi di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="4a6f4-138">Azure resource groups</span></span>](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a><span data-ttu-id="4a6f4-139">Quali toohave</span><span class="sxs-lookup"><span data-stu-id="4a6f4-139">What toohave</span></span>

<span data-ttu-id="4a6f4-140">Prima di seguire le istruzioni di hello in questo articolo, dovrebbe già disporre:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-140">Before following hello instructions in this article, you should already have:</span></span>

- <span data-ttu-id="4a6f4-141">Una sottoscrizione di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-141">A Microsoft Azure subscription.</span></span>
- <span data-ttu-id="4a6f4-142">Un dominio Windows in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-142">A Windows domain on Azure virtual machines.</span></span>
- <span data-ttu-id="4a6f4-143">Un account con gli oggetti di autorizzazione toocreate in hello macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-143">An account with permission toocreate objects in hello Azure virtual machine.</span></span>
- <span data-ttu-id="4a6f4-144">Una rete virtuale di Azure e una subnet con sufficiente spazio degli indirizzi IP per hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-144">An Azure virtual network and subnet with sufficient IP address space for hello following components:</span></span>
   - <span data-ttu-id="4a6f4-145">Entrambe le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-145">Both virtual machines.</span></span>
   - <span data-ttu-id="4a6f4-146">indirizzo IP del cluster failover Hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-146">hello failover cluster IP address.</span></span>
   - <span data-ttu-id="4a6f4-147">Indirizzo IP per ogni istanza del cluster di failover.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-147">An IP address for each FCI.</span></span>
- <span data-ttu-id="4a6f4-148">DNS configurato nella rete di Azure, verso i controller di dominio toohello hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-148">DNS configured on hello Azure Network, pointing toohello domain controllers.</span></span>

<span data-ttu-id="4a6f4-149">Dopo aver soddisfatto questi prerequisiti, è possibile procedere con la creazione del cluster di failover.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-149">With these prerequisites in place, you can proceed with building your failover cluster.</span></span> <span data-ttu-id="4a6f4-150">primo passaggio Hello è toocreate hello le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-150">hello first step is toocreate hello virtual machines.</span></span>

## <a name="step-1-create-virtual-machines"></a><span data-ttu-id="4a6f4-151">Passaggio 1: Creare le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="4a6f4-151">Step 1: Create virtual machines</span></span>

1. <span data-ttu-id="4a6f4-152">Accedi toohello [portale di Azure](http://portal.azure.com) con la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-152">Log in toohello [Azure portal](http://portal.azure.com) with your subscription.</span></span>

1. <span data-ttu-id="4a6f4-153">[Creare un set di disponibilità di Azure](../tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-153">[Create an Azure availability set](../tutorial-availability-sets.md).</span></span>

   <span data-ttu-id="4a6f4-154">disponibilità Hello impostare macchine virtuali in domini di errore e domini di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-154">hello availability set groups virtual machines across fault domains and update domains.</span></span> <span data-ttu-id="4a6f4-155">set di disponibilità Hello garantiscono che l'applicazione non è influenzata da singoli punti di errore, ad esempio switch di rete hello o unità di alimentazione hello di un rack di server.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-155">hello availability set makes sure that your application is not affected by single points of failure, like hello network switch or hello power unit of a rack of servers.</span></span>

   <span data-ttu-id="4a6f4-156">Se non è stato creato il gruppo di risorse hello per le macchine virtuali, è possibile farlo quando si crea un set di disponibilità di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-156">If you have not created hello resource group for your virtual machines, do it when you create an Azure availability set.</span></span> <span data-ttu-id="4a6f4-157">Se si utilizza set di disponibilità hello hello toocreate portale Azure, hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-157">If you're using hello Azure portal toocreate hello availability set, do hello following steps:</span></span>

   - <span data-ttu-id="4a6f4-158">Nel portale di Azure hello, fare clic su  **+**  tooopen hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-158">In hello Azure portal, click **+** tooopen hello Azure Marketplace.</span></span> <span data-ttu-id="4a6f4-159">Cercare **Set di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-159">Search for **Availability set**.</span></span>
   - <span data-ttu-id="4a6f4-160">Fare clic su **Set di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-160">Click **Availability set**.</span></span>
   - <span data-ttu-id="4a6f4-161">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-161">Click **Create**.</span></span>
   - <span data-ttu-id="4a6f4-162">In hello **creare set di disponibilità** pannello hello set seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-162">On hello **Create availability set** blade, set hello following values:</span></span>
      - <span data-ttu-id="4a6f4-163">**Nome**: un nome per il set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-163">**Name**: A name for hello availability set.</span></span>
      - <span data-ttu-id="4a6f4-164">**Sottoscrizione**: sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-164">**Subscription**: Your Azure subscription.</span></span>
      - <span data-ttu-id="4a6f4-165">**Gruppo di risorse**: toouse un gruppo esistente, fare clic su **utilizzare esistente** e gruppo hello selezionare dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-165">**Resource group**: If you want toouse an existing group, click **Use existing** and select hello group from hello drop-down list.</span></span> <span data-ttu-id="4a6f4-166">In caso contrario scegliere **Crea nuovo** e digitare un nome per il gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-166">Otherwise choose **Create New** and type a name for hello group.</span></span>
      - <span data-ttu-id="4a6f4-167">**Percorso**: impostare il percorso di hello in cui si prevede di toocreate le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-167">**Location**: Set hello location where you plan toocreate your virtual machines.</span></span>
      - <span data-ttu-id="4a6f4-168">**Domini di errore**: hello predefinito (3).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-168">**Fault domains**: Use hello default (3).</span></span>
      - <span data-ttu-id="4a6f4-169">**Domini di aggiornamento**: hello predefinito (5).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-169">**Update domains**: Use hello default (5).</span></span>
   - <span data-ttu-id="4a6f4-170">Fare clic su **crea** toocreate hello set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-170">Click **Create** toocreate hello availability set.</span></span>

1. <span data-ttu-id="4a6f4-171">Creare macchine virtuali hello in set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-171">Create hello virtual machines in hello availability set.</span></span>

   <span data-ttu-id="4a6f4-172">Eseguire il provisioning di due macchine virtuali di SQL Server nel set di disponibilità di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-172">Provision two SQL Server virtual machines in hello Azure availability set.</span></span> <span data-ttu-id="4a6f4-173">Per istruzioni, vedere [il provisioning di una macchina virtuale di SQL Server nel portale di Azure hello](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-173">For instructions, see [Provision a SQL Server virtual machine in hello Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

   <span data-ttu-id="4a6f4-174">Inserire entrambe le macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-174">Place both virtual machines:</span></span>

   - <span data-ttu-id="4a6f4-175">In hello stesso gruppo di risorse di Azure imposta la disponibilità è.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-175">In hello same Azure resource group that your availability set is in.</span></span>
   - <span data-ttu-id="4a6f4-176">In hello nella stessa rete del controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-176">On hello same network as your domain controller.</span></span>
   - <span data-ttu-id="4a6f4-177">In una subnet con spazio indirizzi IP sufficiente per entrambe le macchine virtuali e tutte le istanze del cluster di failover che si potrebbero usare nel cluster.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span></span>
   - <span data-ttu-id="4a6f4-178">Nel set di disponibilità di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-178">In hello Azure availability set.</span></span>   

      >[!IMPORTANT]
      ><span data-ttu-id="4a6f4-179">Non è possibile impostare o modificare il set di disponibilità dopo che è stata creata una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-179">You cannot set or change availability set after a virtual machine has been created.</span></span>

   <span data-ttu-id="4a6f4-180">Scegliere un'immagine da hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-180">Choose an image from hello Azure Marketplace.</span></span> <span data-ttu-id="4a6f4-181">È possibile utilizzare un Marketplace immagine con che include solo hello Windows Server e SQL Server o Windows Server.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just hello Windows Server.</span></span> <span data-ttu-id="4a6f4-182">Per informazioni dettagliate, vedere [Panoramica di SQL Server in macchine virtuali di Azure](../../virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span></span>

   <span data-ttu-id="4a6f4-183">immagini di SQL Server in hello raccolta Azure ufficiale Hello includono un'istanza di SQL Server installata, oltre a software di installazione di SQL Server hello e chiave obbligatoria hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-183">hello official SQL Server images in hello Azure Gallery include an installed SQL Server instance, plus hello SQL Server installation software, and hello required key.</span></span>

   <span data-ttu-id="4a6f4-184">Scegliere l'immagine a destra hello in base a toohow desiderato toopay di licenza di SQL Server hello:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-184">Choose hello right image according toohow you want toopay for hello SQL Server license:</span></span>

   - <span data-ttu-id="4a6f4-185">**Pagare le licenze di utilizzo per**: costo al minuto hello di queste immagini include hello licenza di SQL Server:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-185">**Pay per usage licensing**: hello per-minute cost of these images includes hello SQL Server licensing:</span></span>
      - <span data-ttu-id="4a6f4-186">**SQL Server 2016 Enterprise in Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="4a6f4-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="4a6f4-187">**SQL Server 2016 Standard in Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="4a6f4-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="4a6f4-188">**SQL Server 2016 Developer in Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="4a6f4-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span></span>

   - <span data-ttu-id="4a6f4-189">**BYOL (Bring Your Own License)**</span><span class="sxs-lookup"><span data-stu-id="4a6f4-189">**Bring-your-own-license (BYOL)**</span></span>

      - <span data-ttu-id="4a6f4-190">**{BYOL} SQL Server 2016 Enterprise in Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="4a6f4-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="4a6f4-191">**{BYOL} SQL Server 2016 Standard in Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="4a6f4-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="4a6f4-192">Dopo aver creato una macchina virtuale hello, rimuovere l'istanza di SQL Server hello pre-installata in modalità autonoma.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-192">After you create hello virtual machine, remove hello pre-installed standalone SQL Server instance.</span></span> <span data-ttu-id="4a6f4-193">Dopo aver configurato il cluster di failover di hello e S2D, si utilizzerà hello pre-installato SQL Server supporti toocreate hello istanza cluster di failover di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-193">You will use hello pre-installed SQL Server media toocreate hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span>

   <span data-ttu-id="4a6f4-194">In alternativa, è possibile utilizzare le immagini di Azure Marketplace con solo hello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-194">Alternatively, you can use Azure Marketplace images with just hello operating system.</span></span> <span data-ttu-id="4a6f4-195">Scegliere un **Data Center di Windows Server 2016** installa hello istanza cluster di failover di SQL Server dopo aver configurato il cluster di failover di hello e S2D e immagini.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-195">Choose a **Windows Server 2016 Datacenter** image and install hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span> <span data-ttu-id="4a6f4-196">Un'immagine di questo tipo non contiene i supporti di installazione di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-196">This image does not contain SQL Server installation media.</span></span> <span data-ttu-id="4a6f4-197">Inserire il supporto di installazione di hello in una posizione in cui è possibile eseguire l'installazione di SQL Server hello per ogni server.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-197">Place hello installation media in a location where you can run hello SQL Server installation for each server.</span></span>

1. <span data-ttu-id="4a6f4-198">Dopo la creazione delle macchine virtuali di Azure, è possibile connettere macchina virtuale tooeach con RDP.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-198">After Azure creates your virtual machines, connect tooeach virtual machine with RDP.</span></span>

   <span data-ttu-id="4a6f4-199">Quando ci si connette prima macchina virtuale tooa con RDP, computer hello chiede se si desidera tooallow toobe questo PC individuabile in rete hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-199">When you first connect tooa virtual machine with RDP, hello computer asks if you want tooallow this PC toobe discoverable on hello network.</span></span> <span data-ttu-id="4a6f4-200">Fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-200">Click **Yes**.</span></span>

1. <span data-ttu-id="4a6f4-201">Se si utilizza una delle immagini di macchina virtuale basata su SQL Server hello, rimuovere l'istanza di SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-201">If you are using one of hello SQL Server-based virtual machine images, remove hello SQL Server instance.</span></span>

   - <span data-ttu-id="4a6f4-202">In **Programmi e funzionalità** fare clic con il pulsante destro del mouse su **Microsoft SQL Server 2016 (64 bit)** e scegliere **Disinstalla/Cambia**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span></span>
   - <span data-ttu-id="4a6f4-203">Fare clic su **Rimuovi**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-203">Click **Remove**.</span></span>
   - <span data-ttu-id="4a6f4-204">Selezionare l'istanza predefinita di hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-204">Select hello default instance.</span></span>
   - <span data-ttu-id="4a6f4-205">Rimuovere tutte le funzionalità in **Servizi motore di database**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-205">Remove all features under **Database Engine Services**.</span></span> <span data-ttu-id="4a6f4-206">Non rimuovere **Funzionalità condivise**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-206">Do not remove **Shared Features**.</span></span> <span data-ttu-id="4a6f4-207">Vedere hello seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-207">See hello following picture:</span></span>

      ![Rimuovere le funzionalità](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - <span data-ttu-id="4a6f4-209">Fare clic su **Avanti** e quindi su **Rimuovi**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-209">Click **Next**, and then click **Remove**.</span></span>

1. <span data-ttu-id="4a6f4-210"><a name="ports"></a>Aprire le porte del firewall hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-210"><a name="ports"></a>Open hello firewall ports.</span></span>

   <span data-ttu-id="4a6f4-211">In ogni macchina virtuale, aprire hello seguendo porte hello Windows Firewall.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-211">On each virtual machine, open hello following ports on hello Windows Firewall.</span></span>

   | <span data-ttu-id="4a6f4-212">Scopo</span><span class="sxs-lookup"><span data-stu-id="4a6f4-212">Purpose</span></span> | <span data-ttu-id="4a6f4-213">Porta TCP</span><span class="sxs-lookup"><span data-stu-id="4a6f4-213">TCP Port</span></span> | <span data-ttu-id="4a6f4-214">Note</span><span class="sxs-lookup"><span data-stu-id="4a6f4-214">Notes</span></span>
   | ------ | ------ | ------
   | <span data-ttu-id="4a6f4-215">SQL Server</span><span class="sxs-lookup"><span data-stu-id="4a6f4-215">SQL Server</span></span> | <span data-ttu-id="4a6f4-216">1433</span><span class="sxs-lookup"><span data-stu-id="4a6f4-216">1433</span></span> | <span data-ttu-id="4a6f4-217">Porta normale per le istanze predefinite di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-217">Normal port for default instances of SQL Server.</span></span> <span data-ttu-id="4a6f4-218">Se si utilizza un'immagine dalla raccolta di hello, questa porta viene aperta automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-218">If you used an image from hello gallery, this port is automatically opened.</span></span>
   | <span data-ttu-id="4a6f4-219">Probe di integrità</span><span class="sxs-lookup"><span data-stu-id="4a6f4-219">Health probe</span></span> | <span data-ttu-id="4a6f4-220">59999</span><span class="sxs-lookup"><span data-stu-id="4a6f4-220">59999</span></span> | <span data-ttu-id="4a6f4-221">Qualsiasi porta TCP aperta.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-221">Any open TCP port.</span></span> <span data-ttu-id="4a6f4-222">In un passaggio successivo, configurare il bilanciamento del carico di hello [probe di integrità](#probe) e hello cluster toouse questa porta.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-222">In a later step, configure hello load balancer [health probe](#probe) and hello cluster toouse this port.</span></span>  

1. <span data-ttu-id="4a6f4-223">Aggiungere una macchina virtuale di archiviazione toohello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-223">Add storage toohello virtual machine.</span></span> <span data-ttu-id="4a6f4-224">Per informazioni dettagliate, vedere l'articolo relativo all'[aggiunta dell'archiviazione](../../../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-224">For detailed information, see [add storage](../../../storage/common/storage-premium-storage.md).</span></span>

   <span data-ttu-id="4a6f4-225">Entrambe le macchine virtuali necessitano di almeno due dischi dati.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-225">Both virtual machines need at least two data disks.</span></span>

   <span data-ttu-id="4a6f4-226">Collegare dischi non formattati, ossia senza formattazione NTFS.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-226">Attach raw disks - not NTFS formatted disks.</span></span>
      >[!NOTE]
      ><span data-ttu-id="4a6f4-227">Se si collegano dischi con formattazione NTFS, è possibile abilitare S2D solo senza controllo dell'idoneità del disco.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span></span>  

   <span data-ttu-id="4a6f4-228">Collegare un minimo di due archiviazione Premium (dischi SSD) tooeach macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-228">Attach a minimum of two Premium Storage (SSD disks) tooeach VM.</span></span> <span data-ttu-id="4a6f4-229">È consigliabile usare almeno dischi P30 (da 1 TB).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-229">We recommend at least P30 (1 TB) disks.</span></span>

   <span data-ttu-id="4a6f4-230">Host di impostare la memorizzazione nella cache troppo**Read-only**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-230">Set host caching too**Read-only**.</span></span>

   <span data-ttu-id="4a6f4-231">capacità di archiviazione Hello che è usare negli ambienti di produzione dipende dal carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-231">hello storage capacity you use in production environments depends on your workload.</span></span> <span data-ttu-id="4a6f4-232">i valori Hello descritti in questo articolo sono per la dimostrazione e test.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-232">hello values described in this article are for demonstration and testing.</span></span>

1. <span data-ttu-id="4a6f4-233">[Aggiungere hello macchine virtuali tooyour preesistente dominio](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-233">[Add hello virtual machines tooyour pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

<span data-ttu-id="4a6f4-234">Dopo che le macchine virtuali hello create e configurate, è possibile configurare cluster di failover hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-234">After hello virtual machines are created and configured, you can configure hello failover cluster.</span></span>

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a><span data-ttu-id="4a6f4-235">Passaggio 2: Configurare il Cluster di Failover di Windows hello con S2D</span><span class="sxs-lookup"><span data-stu-id="4a6f4-235">Step 2: Configure hello Windows Failover Cluster with S2D</span></span>

<span data-ttu-id="4a6f4-236">passaggio successivo Hello è di tipo cluster di failover di hello tooconfigure con S2D.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-236">hello next step is tooconfigure hello failover cluster with S2D.</span></span> <span data-ttu-id="4a6f4-237">In questo passaggio si eseguiranno hello seguenti passaggi:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-237">In this step, you will do hello following substeps:</span></span>

1. <span data-ttu-id="4a6f4-238">Aggiungere la funzionalità Clustering di failover di Windows</span><span class="sxs-lookup"><span data-stu-id="4a6f4-238">Add Windows Failover Clustering feature</span></span>
1. <span data-ttu-id="4a6f4-239">Convalida cluster hello</span><span class="sxs-lookup"><span data-stu-id="4a6f4-239">Validate hello cluster</span></span>
1. <span data-ttu-id="4a6f4-240">Creare il cluster di failover di hello</span><span class="sxs-lookup"><span data-stu-id="4a6f4-240">Create hello failover cluster</span></span>
1. <span data-ttu-id="4a6f4-241">Creare server di controllo di hello cloud</span><span class="sxs-lookup"><span data-stu-id="4a6f4-241">Create hello cloud witness</span></span>
1. <span data-ttu-id="4a6f4-242">Aggiungere le risorse di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4a6f4-242">Add storage</span></span>

### <a name="add-windows-failover-clustering-feature"></a><span data-ttu-id="4a6f4-243">Aggiungere la funzionalità Clustering di failover di Windows</span><span class="sxs-lookup"><span data-stu-id="4a6f4-243">Add Windows Failover Clustering feature</span></span>

1. <span data-ttu-id="4a6f4-244">toobegin, connettersi toohello prima macchina virtuale con RDP utilizzando un account di dominio membro del gruppo administrators locale, che contiene oggetti toocreate di autorizzazioni in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-244">toobegin, connect toohello first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions toocreate objects in Active Directory.</span></span> <span data-ttu-id="4a6f4-245">Utilizzare questo account per il resto di hello della configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-245">Use this account for hello rest of hello configuration.</span></span>

1. <span data-ttu-id="4a6f4-246">[Aggiungere il Clustering di Failover di macchina virtuale tooeach funzionalità](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-246">[Add Failover Clustering feature tooeach virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

   <span data-ttu-id="4a6f4-247">funzionalità Clustering di Failover tooinstall dall'interfaccia utente, hello hello in entrambe le macchine virtuali come segue.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-247">tooinstall Failover Clustering feature from hello UI, do hello following steps on both virtual machines.</span></span>
   - <span data-ttu-id="4a6f4-248">In **Server Manager** fare clic su **Gestione** e quindi su **Aggiungi ruoli e funzionalità**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span></span>
   - <span data-ttu-id="4a6f4-249">In **Aggiunta guidata ruoli e funzionalità**, fare clic su **Avanti** fino a ottenere troppo**Seleziona funzionalità**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-249">In **Add Roles and Features Wizard**, click **Next** until you get too**Select Features**.</span></span>
   - <span data-ttu-id="4a6f4-250">In **Selezione funzionalità** selezionare **Clustering di failover**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-250">In **Select Features**, click **Failover Clustering**.</span></span> <span data-ttu-id="4a6f4-251">Includere tutti gli strumenti di gestione di hello e le funzionalità necessarie.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-251">Include all required features and hello management tools.</span></span> <span data-ttu-id="4a6f4-252">Fare clic su **Aggiungi funzionalità**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-252">Click **Add Features**.</span></span>
   - <span data-ttu-id="4a6f4-253">Fare clic su **Avanti** e quindi fare clic su **fine** funzionalità hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-253">Click **Next** and then click **Finish** tooinstall hello features.</span></span>

   <span data-ttu-id="4a6f4-254">tooinstall hello funzionalità Clustering di Failover con PowerShell, eseguire lo script da una sessione di PowerShell amministratore seguente in una delle macchine virtuali hello hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-254">tooinstall hello Failover Clustering feature with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

<span data-ttu-id="4a6f4-255">Per riferimento, i passaggi successivi hello seguono le istruzioni di hello nel passaggio 3 di [soluzione convergente Hyper tramite spazi di archiviazione diretta in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-255">For reference, hello next steps follow hello instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span></span>

### <a name="validate-hello-cluster"></a><span data-ttu-id="4a6f4-256">Convalida cluster hello</span><span class="sxs-lookup"><span data-stu-id="4a6f4-256">Validate hello cluster</span></span>

<span data-ttu-id="4a6f4-257">Questa guida si riferisce tooinstructions in [convalida cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-257">This guide refers tooinstructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span></span>

<span data-ttu-id="4a6f4-258">Convalida cluster hello in hello dell'interfaccia utente o con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-258">Validate hello cluster in hello UI or with PowerShell.</span></span>

<span data-ttu-id="4a6f4-259">cluster di hello toovalidate con interfaccia utente, hello hello seguendo i passaggi da una delle macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-259">toovalidate hello cluster with hello UI, do hello following steps from one of hello virtual machines.</span></span>

1. <span data-ttu-id="4a6f4-260">In **Server Manager** fare clic su **Strumenti** e quindi su **Gestione cluster di failover**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span></span>
1. <span data-ttu-id="4a6f4-261">In **Gestione cluster di failover** fare clic su **Azione** e quindi su **Convalida configurazione**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span></span>
1. <span data-ttu-id="4a6f4-262">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-262">Click **Next**.</span></span>
1. <span data-ttu-id="4a6f4-263">In **selezionare Server o un Cluster**, nome del tipo hello di entrambe le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-263">On **Select Servers or a Cluster**, type hello name of both virtual machines.</span></span>
1. <span data-ttu-id="4a6f4-264">In **Opzioni di testing** scegliere **Esegui solo test selezionati**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-264">On **Testing options**, choose **Run only tests I select**.</span></span> <span data-ttu-id="4a6f4-265">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-265">Click **Next**.</span></span>
1. <span data-ttu-id="4a6f4-266">In **Selezione dei test** includere tutti i test tranne **Archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-266">On **Test selection**, include all tests except **Storage**.</span></span> <span data-ttu-id="4a6f4-267">Vedere hello seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-267">See hello following picture:</span></span>

   ![Test di convalida](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. <span data-ttu-id="4a6f4-269">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-269">Click **Next**.</span></span>
1. <span data-ttu-id="4a6f4-270">In **Conferma** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-270">On **Confirmation**, click **Next**.</span></span>

<span data-ttu-id="4a6f4-271">Hello **convalida guidata configurazione** hello di esecuzioni di test di convalida.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-271">hello **Validate a Configuration Wizard** runs hello validation tests.</span></span>

<span data-ttu-id="4a6f4-272">cluster di hello toovalidate con PowerShell, eseguire lo script da una sessione di PowerShell amministratore seguente in una delle macchine virtuali hello hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-272">toovalidate hello cluster with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

<span data-ttu-id="4a6f4-273">Dopo la convalida del cluster di hello, creare il cluster di failover di hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-273">After you validate hello cluster, create hello failover cluster.</span></span>

### <a name="create-hello-failover-cluster"></a><span data-ttu-id="4a6f4-274">Creare il cluster di failover di hello</span><span class="sxs-lookup"><span data-stu-id="4a6f4-274">Create hello failover cluster</span></span>

<span data-ttu-id="4a6f4-275">Questa guida si riferisce troppo[Crea cluster di failover hello](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-275">This guide refers too[Create hello failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span></span>

<span data-ttu-id="4a6f4-276">cluster di failover hello toocreate, è necessario:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-276">toocreate hello failover cluster, you need:</span></span>
- <span data-ttu-id="4a6f4-277">i nomi di Hello delle macchine virtuali hello che diventano hello i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-277">hello names of hello virtual machines that become hello cluster nodes.</span></span>
- <span data-ttu-id="4a6f4-278">Un nome per il cluster di failover di hello</span><span class="sxs-lookup"><span data-stu-id="4a6f4-278">A name for hello failover cluster</span></span>
- <span data-ttu-id="4a6f4-279">Un indirizzo IP per il cluster di failover di hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-279">An IP address for hello failover cluster.</span></span> <span data-ttu-id="4a6f4-280">È possibile utilizzare un indirizzo IP non usato in hello stessa rete virtuale e subnet come hello i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-280">You can use an IP address that is not used on hello same Azure virtual network and subnet as hello cluster nodes.</span></span>

<span data-ttu-id="4a6f4-281">Hello PowerShell seguente crea un cluster di failover.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-281">hello following PowerShell creates a failover cluster.</span></span> <span data-ttu-id="4a6f4-282">Aggiornare lo script hello con nomi di hello dei nodi di hello (nomi di macchina virtuale hello) e un indirizzo IP disponibile da hello rete virtuale di Azure:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-282">Update hello script with hello names of hello nodes (hello virtual machine names) and an available IP address from hello Azure VNET:</span></span>

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a><span data-ttu-id="4a6f4-283">Creare un cloud di controllo</span><span class="sxs-lookup"><span data-stu-id="4a6f4-283">Create a cloud witness</span></span>

<span data-ttu-id="4a6f4-284">Il cloud di controllo è un nuovo tipo di quorum di controllo del cluster archiviato in un BLOB del servizio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span></span> <span data-ttu-id="4a6f4-285">Ciò consente di rimuovere hello necessità di una macchina virtuale separata che ospita una condivisione di controllo.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-285">This removes hello need of a separate VM hosting a witness share.</span></span>

1. <span data-ttu-id="4a6f4-286">[Creare un cloud di controllo per il cluster di failover di hello](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-286">[Create a cloud witness for hello failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span>

1. <span data-ttu-id="4a6f4-287">Creare un contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-287">Create a blob container.</span></span>

1. <span data-ttu-id="4a6f4-288">Salvare le chiavi di accesso hello e hello URL del contenitore.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-288">Save hello access keys and hello container URL.</span></span>

1. <span data-ttu-id="4a6f4-289">Configurare hello del quorum di cluster di failover cluster controllo.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-289">Configure hello failover cluster cluster quorum witness.</span></span> <span data-ttu-id="4a6f4-290">Vedere [Configura hello quorum di controllo nell'interfaccia utente di hello]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in hello dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-290">See, [Configure hello quorum witness in hello user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in hello UI.</span></span>

### <a name="add-storage"></a><span data-ttu-id="4a6f4-291">Aggiungere le risorse di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4a6f4-291">Add storage</span></span>

<span data-ttu-id="4a6f4-292">i dischi di Hello per S2D devono toobe vuoto e senza partizioni o altri dati.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-292">hello disks for S2D need toobe empty and without partitions or other data.</span></span> <span data-ttu-id="4a6f4-293">seguono i dischi tooclean [hello i passaggi in questa Guida](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-293">tooclean disks follow [hello steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span></span>

1. <span data-ttu-id="4a6f4-294">[Abilitare Spazi di archiviazione diretta \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span></span>

   <span data-ttu-id="4a6f4-295">Hello PowerShell seguente consente di spazi di archiviazione diretti.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-295">hello following PowerShell enables storage spaces direct.</span></span>  

   ```PowerShell
   Enable-ClusterS2D
   ```

   <span data-ttu-id="4a6f4-296">In **gestione Cluster di Failover**, è ora possibile visualizzare i pool di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-296">In **Failover Cluster Manager**, you can now see hello storage pool.</span></span>

1. <span data-ttu-id="4a6f4-297">[Creare un volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span></span>

   <span data-ttu-id="4a6f4-298">Una delle funzionalità di hello di S2D è che viene creato automaticamente un pool di archiviazione quando si attiva un.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-298">One of hello features of S2D is that it automatically creates a storage pool when you enable it.</span></span> <span data-ttu-id="4a6f4-299">Si è ora pronto toocreate un volume.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-299">You are now ready toocreate a volume.</span></span> <span data-ttu-id="4a6f4-300">cmdlet PowerShell di Hello `New-Volume` automatizza hello volume creazione processo, tra cui la formattazione, aggiunta toohello cluster e la creazione di un volume condiviso cluster (CSV).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-300">hello PowerShell commandlet `New-Volume` automates hello volume creation process, including formatting, adding toohello cluster, and creating a cluster shared volume (CSV).</span></span> <span data-ttu-id="4a6f4-301">Hello di esempio seguente crea un 800 gigabyte (GB) CSV.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-301">hello following example creates an 800 gigabyte (GB) CSV.</span></span>

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   <span data-ttu-id="4a6f4-302">Al termine dell'esecuzione del comando, un volume di 800 GB viene montato come risorsa cluster.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span></span> <span data-ttu-id="4a6f4-303">volume Hello è `C:\ClusterStorage\Volume1\`.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-303">hello volume is at `C:\ClusterStorage\Volume1\`.</span></span>

   <span data-ttu-id="4a6f4-304">Hello seguente diagramma viene illustrato un volume condiviso cluster con S2D:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-304">hello following diagram shows a cluster shared volume with S2D:</span></span>

   ![Volume condiviso cluster](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a><span data-ttu-id="4a6f4-306">Passaggio 3: Testare il failover del cluster di failover</span><span class="sxs-lookup"><span data-stu-id="4a6f4-306">Step 3: Test failover cluster failover</span></span>

<span data-ttu-id="4a6f4-307">In Gestione Cluster di Failover, verificare che è possibile spostare toohello risorse di archiviazione hello altro nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-307">In Failover Cluster Manager, verify that you can move hello storage resource toohello other cluster node.</span></span> <span data-ttu-id="4a6f4-308">Se è possibile connettere i cluster di failover toohello con **gestione Cluster di Failover** e spostare archiviazione hello da un nodo toohello altre, si è pronti tooconfigure hello FCI.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-308">If you can connect toohello failover cluster with **Failover Cluster Manager** and move hello storage from one node toohello other, you are ready tooconfigure hello FCI.</span></span>

## <a name="step-4-create-sql-server-fci"></a><span data-ttu-id="4a6f4-309">Passaggio 4: Creare l'istanza del cluster di failover di SQL Server</span><span class="sxs-lookup"><span data-stu-id="4a6f4-309">Step 4: Create SQL Server FCI</span></span>

<span data-ttu-id="4a6f4-310">Dopo aver configurato il cluster di failover di hello e tutti i componenti di cluster, inclusa l'archiviazione, è possibile creare hello istanza cluster di failover di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-310">After you have configured hello failover cluster and all cluster components including storage, you can create hello SQL Server FCI.</span></span>

1. <span data-ttu-id="4a6f4-311">Connettere toohello prima macchina virtuale con il protocollo RDP.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-311">Connect toohello first virtual machine with RDP.</span></span>

1. <span data-ttu-id="4a6f4-312">In **gestione Cluster di Failover**, assicurarsi che tutte le risorse principali del cluster siano presenti hello prima macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-312">In **Failover Cluster Manager**, make sure all cluster core resources are on hello first virtual machine.</span></span> <span data-ttu-id="4a6f4-313">Se necessario, spostare una macchina virtuale di tutte le risorse toothis.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-313">If necessary, move all resources toothis virtual machine.</span></span>

1. <span data-ttu-id="4a6f4-314">Individuare il supporto di installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-314">Locate hello installation media.</span></span> <span data-ttu-id="4a6f4-315">Se usato nella macchina virtuale hello delle immagini di Azure Marketplace hello, si trova in media hello `C:\SQLServer_<version number>_Full`.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-315">If hello virtual machine uses one of hello Azure Marketplace images, hello media is located at `C:\SQLServer_<version number>_Full`.</span></span> <span data-ttu-id="4a6f4-316">Fare clic su **Configura**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-316">Click **Setup**.</span></span>

1. <span data-ttu-id="4a6f4-317">In hello **Centro installazione SQL Server**, fare clic su **installazione**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-317">In hello **SQL Server Installation Center**, click **Installation**.</span></span>

1. <span data-ttu-id="4a6f4-318">Fare clic su **Installazione di un nuovo cluster di failover di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-318">Click **New SQL Server failover cluster installation**.</span></span> <span data-ttu-id="4a6f4-319">Seguire le istruzioni hello hello tooinstall tramite procedura guidata hello istanza cluster di failover di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-319">Follow hello instructions in hello wizard tooinstall hello SQL Server FCI.</span></span>

   <span data-ttu-id="4a6f4-320">directory dei dati dell'istanza FCI Hello necessario toobe nell'archiviazione cluster.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-320">hello FCI data directories need toobe on clustered storage.</span></span> <span data-ttu-id="4a6f4-321">Con S2D, non è un disco condiviso, ma un volume tooa punto di montaggio in ogni server.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-321">With S2D, it's not a shared disk, but a mount point tooa volume on each server.</span></span> <span data-ttu-id="4a6f4-322">S2D Sincronizza volume hello tra entrambi i nodi.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-322">S2D synchronizes hello volume between both nodes.</span></span> <span data-ttu-id="4a6f4-323">volume Hello viene presentato toohello cluster come volume condiviso cluster.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-323">hello volume is presented toohello cluster as a cluster shared volume.</span></span> <span data-ttu-id="4a6f4-324">Utilizzo di punto di montaggio CSV hello per le directory dati hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-324">Use hello CSV mount point for hello data directories.</span></span>

   ![Directory di dati](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. <span data-ttu-id="4a6f4-326">Dopo aver completato la procedura guidata hello, verrà installato nel primo nodo hello una FCI di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-326">After you complete hello wizard, Setup will install a SQL Server FCI on hello first node.</span></span>

1. <span data-ttu-id="4a6f4-327">Dopo l'installazione hello FCI nel primo nodo hello correttamente, è possibile connettere toohello secondo nodo con RDP.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-327">After Setup successfully installs hello FCI on hello first node, connect toohello second node with RDP.</span></span>

1. <span data-ttu-id="4a6f4-328">Aprire hello **Centro installazione SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-328">Open hello **SQL Server Installation Center**.</span></span> <span data-ttu-id="4a6f4-329">Fare clic su **Installazione**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-329">Click **Installation**.</span></span>

1. <span data-ttu-id="4a6f4-330">Fare clic su **cluster di failover di SQL Server di Aggiungi nodo tooa**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-330">Click **Add node tooa SQL Server failover cluster**.</span></span> <span data-ttu-id="4a6f4-331">Seguire le istruzioni hello del server SQL tooinstall guidata hello e aggiungere questo toohello server FCI.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-331">Follow hello instructions in hello wizard tooinstall SQL server and add this server toohello FCI.</span></span>

   >[!NOTE]
   ><span data-ttu-id="4a6f4-332">Se si utilizza un'immagine della raccolta Azure Marketplace con SQL Server, strumenti di SQL Server sono stati inclusi con l'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with hello image.</span></span> <span data-ttu-id="4a6f4-333">Se non è stata utilizzata questa immagine, è possibile installare separatamente gli strumenti di SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-333">If you did not use this image, install hello SQL Server tools separately.</span></span> <span data-ttu-id="4a6f4-334">Vedere [Scaricare SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="step-5-create-azure-load-balancer"></a><span data-ttu-id="4a6f4-335">Passaggio 5: Creare un servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="4a6f4-335">Step 5: Create Azure load balancer</span></span>

<span data-ttu-id="4a6f4-336">Macchine virtuali di Azure, i cluster utilizzano un toohold del servizio di bilanciamento carico di un indirizzo IP che deve toobe su un nodo cluster alla volta.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-336">On Azure virtual machines, clusters use a load balancer toohold an IP address that needs toobe on one cluster node at a time.</span></span> <span data-ttu-id="4a6f4-337">In questa soluzione, bilanciamento del carico hello contiene l'indirizzo IP hello hello istanza cluster di failover di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-337">In this solution, hello load balancer holds hello IP address for hello SQL Server FCI.</span></span>

<span data-ttu-id="4a6f4-338">[Creare e configurare un servizio di bilanciamento del carico di Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="4a6f4-339">Creare servizio di bilanciamento del carico hello in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4a6f4-339">Create hello load balancer in hello Azure portal</span></span>

<span data-ttu-id="4a6f4-340">bilanciamento del carico di hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-340">toocreate hello load balancer:</span></span>

1. <span data-ttu-id="4a6f4-341">Nel portale di Azure hello, passare toohello gruppo di risorse con le macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-341">In hello Azure portal, go toohello Resource Group with hello virtual machines.</span></span>

1. <span data-ttu-id="4a6f4-342">Fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-342">Click **+ Add**.</span></span> <span data-ttu-id="4a6f4-343">Hello ricerca Marketplace per **bilanciamento del carico**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-343">Search hello Marketplace for **Load Balancer**.</span></span> <span data-ttu-id="4a6f4-344">Fare clic su **Servizio di bilanciamento del carico**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-344">Click **Load Balancer**.</span></span>

1. <span data-ttu-id="4a6f4-345">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-345">Click **Create**.</span></span>

1. <span data-ttu-id="4a6f4-346">Configurare il bilanciamento del carico hello con:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-346">Configure hello load balancer with:</span></span>

   - <span data-ttu-id="4a6f4-347">**Nome**: un nome che identifichi bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-347">**Name**: A name that identifies hello load balancer.</span></span>
   - <span data-ttu-id="4a6f4-348">**Tipo**: servizio di bilanciamento del carico hello possa essere pubblici o privati.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-348">**Type**: hello load balancer can be either public or private.</span></span> <span data-ttu-id="4a6f4-349">Un servizio di bilanciamento del carico privato è accessibile dall'interno hello stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-349">A private load balancer can be accessed from within hello same VNET.</span></span> <span data-ttu-id="4a6f4-350">La maggior parte delle applicazioni Azure può usare un servizio di bilanciamento del carico privato.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-350">Most Azure applications can use a private load balancer.</span></span> <span data-ttu-id="4a6f4-351">Se l'applicazione deve accedere tooSQL Server direttamente su Internet hello, utilizzare un servizio di bilanciamento del carico pubblico.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-351">If your application needs access tooSQL Server directly over hello Internet, use a public load balancer.</span></span>
   - <span data-ttu-id="4a6f4-352">**Rete virtuale**: hello stessa rete hello le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-352">**Virtual Network**: hello same network as hello virtual machines.</span></span>
   - <span data-ttu-id="4a6f4-353">**Subnet**: hello stessa subnet hello le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-353">**Subnet**: hello same subnet as hello virtual machines.</span></span>
   - <span data-ttu-id="4a6f4-354">**Indirizzo IP privato**: hello stesso indirizzo IP assegnato risorsa di rete cluster toohello istanza cluster di failover di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-354">**Private IP address**: hello same IP address that you assigned toohello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="4a6f4-355">**Sottoscrizione**: sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-355">**subscription**: Your Azure subscription.</span></span>
   - <span data-ttu-id="4a6f4-356">**Gruppo di risorse**: utilizzare hello stesso gruppo di risorse come le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-356">**Resource Group**: Use hello same resource group as your virtual machines.</span></span>
   - <span data-ttu-id="4a6f4-357">**Percorso**: utilizzare hello stesso percorso di Azure le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-357">**Location**: Use hello same Azure location as your virtual machines.</span></span>
   <span data-ttu-id="4a6f4-358">Vedere hello seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-358">See hello following picture:</span></span>

   ![Creare il servizio di bilanciamento del carico](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a><span data-ttu-id="4a6f4-360">Configurare i pool back-end di bilanciamento del carico hello</span><span class="sxs-lookup"><span data-stu-id="4a6f4-360">Configure hello load balancer backend pool</span></span>

1. <span data-ttu-id="4a6f4-361">Restituire toohello il gruppo di risorse di Azure con le macchine virtuali hello e individuare di nuovo bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-361">Return toohello Azure Resource Group with hello virtual machines and locate hello new load balancer.</span></span> <span data-ttu-id="4a6f4-362">È possibile visualizzare hello toorefresh su hello gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-362">You may have toorefresh hello view on hello Resource Group.</span></span> <span data-ttu-id="4a6f4-363">Fare clic su servizio di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-363">Click hello load balancer.</span></span>

1. <span data-ttu-id="4a6f4-364">Nel pannello del servizio di bilanciamento carico di hello, fare clic su **pool back-end**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-364">On hello load balancer blade, click **Backend pools**.</span></span>

1. <span data-ttu-id="4a6f4-365">Fare clic su **+ Aggiungi** tooadd un pool back-end.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-365">Click **+ Add** tooadd a backend pool.</span></span>

1. <span data-ttu-id="4a6f4-366">Digitare un nome per il pool back-end hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-366">Type a name for hello backend pool.</span></span>

1. <span data-ttu-id="4a6f4-367">Fare clic su **Aggiungi una macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-367">Click **Add a virtual machine**.</span></span>

1. <span data-ttu-id="4a6f4-368">In hello **scegliere macchine virtuali** pannello, fare clic su **scegliere un set di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-368">On hello **Choose virtual machines** blade, click **Choose an availability set**.</span></span>

1. <span data-ttu-id="4a6f4-369">Scegliere set di disponibilità di hello è inserito di macchine virtuali di SQL Server hello in.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-369">Choose hello availability set that you placed hello SQL Server virtual machines in.</span></span>

1. <span data-ttu-id="4a6f4-370">In hello **scegliere macchine virtuali** pannello, fare clic su **scegliere macchine virtuali hello**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-370">On hello **Choose virtual machines** blade, click **Choose hello virtual machines**.</span></span>

   <span data-ttu-id="4a6f4-371">Il portale di Azure dovrebbe essere simile hello seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-371">Your Azure portal should look like hello following picture:</span></span>

   ![Creare il back-end del servizio di bilanciamento di carico](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. <span data-ttu-id="4a6f4-373">Fare clic su **selezionare** su hello **scegliere macchine virtuali** blade.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-373">Click **Select** on hello **Choose virtual machines** blade.</span></span>

1. <span data-ttu-id="4a6f4-374">Fare clic su **OK** due volte.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-374">Click **OK** twice.</span></span>

### <a name="configure-a-load-balancer-health-probe"></a><span data-ttu-id="4a6f4-375">Configurare un probe di integrità per il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="4a6f4-375">Configure a load balancer health probe</span></span>

1. <span data-ttu-id="4a6f4-376">Nel pannello del servizio di bilanciamento carico di hello, fare clic su **probe di integrità**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-376">On hello load balancer blade, click **Health probes**.</span></span>

1. <span data-ttu-id="4a6f4-377">Fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-377">Click **+ Add**.</span></span>

1. <span data-ttu-id="4a6f4-378">In hello **probe di integrità Aggiungi** pannello <a name="probe"> </a>impostare i parametri di probe di integrità hello:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-378">On hello **Add health probe** blade, <a name="probe"></a>Set hello health probe parameters:</span></span>

   - <span data-ttu-id="4a6f4-379">**Nome**: un nome per il probe di integrità hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-379">**Name**: A name for hello health probe.</span></span>
   - <span data-ttu-id="4a6f4-380">**Protocollo**: TCP.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-380">**Protocol**: TCP.</span></span>
   - <span data-ttu-id="4a6f4-381">**Porta**: impostare tooan porta TCP disponibile.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-381">**Port**: Set tooan available TCP port.</span></span> <span data-ttu-id="4a6f4-382">È necessaria una porta del firewall aperta.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-382">This port requires an open firewall port.</span></span> <span data-ttu-id="4a6f4-383">Hello utilizzare [stessa porta](#ports) viene impostata per il probe di integrità hello in firewall hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-383">Use hello [same port](#ports) you set for hello health probe at hello firewall.</span></span>
   - <span data-ttu-id="4a6f4-384">**Intervallo**: 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-384">**Interval**: 5 Seconds.</span></span>
   - <span data-ttu-id="4a6f4-385">**Soglia di non integrità**: 2 errori consecutivi.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-385">**Unhealthy threshold**: 2 consecutive failures.</span></span>

1. <span data-ttu-id="4a6f4-386">Fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-386">Click OK.</span></span>

### <a name="set-load-balancing-rules"></a><span data-ttu-id="4a6f4-387">Impostare le regole di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="4a6f4-387">Set load balancing rules</span></span>

1. <span data-ttu-id="4a6f4-388">Nel pannello del servizio di bilanciamento carico di hello, fare clic su **regole di bilanciamento del carico**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-388">On hello load balancer blade, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="4a6f4-389">Fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-389">Click **+ Add**.</span></span>

1. <span data-ttu-id="4a6f4-390">Impostare hello i parametri regole di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-390">Set hello load balancing rules parameters:</span></span>

   - <span data-ttu-id="4a6f4-391">**Nome**: un nome per le regole di bilanciamento del carico di hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-391">**Name**: A name for hello load balancing rules.</span></span>
   - <span data-ttu-id="4a6f4-392">**Indirizzo IP Frontend**: utilizzare l'indirizzo IP hello per hello risorsa di rete del cluster di failover di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-392">**Frontend IP address**: Use hello IP address for hello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="4a6f4-393">**Porta**: impostare per la porta TCP di SQL Server FCI hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-393">**Port**: Set for hello SQL Server FCI TCP port.</span></span> <span data-ttu-id="4a6f4-394">porta dell'istanza Hello predefinita è 1433.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-394">hello default instance port is 1433.</span></span>
   - <span data-ttu-id="4a6f4-395">**Porta back-end**: questo valore utilizza hello stessa porta come hello **porta** valore quando si abilita **IP mobile (direct server restituito)**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-395">**Backend port**: This value uses hello same port as hello **Port** value when you enable **Floating IP (direct server return)**.</span></span>
   - <span data-ttu-id="4a6f4-396">**Pool back-end**: utilizzare hello back-end nome del pool configurata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-396">**Backend pool**: Use hello backend pool name that you configured earlier.</span></span>
   - <span data-ttu-id="4a6f4-397">**Probe di integrità**: probe di integrità hello utilizzare configurata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-397">**Health probe**: Use hello health probe that you configured earlier.</span></span>
   - <span data-ttu-id="4a6f4-398">**Salvataggio permanente sessione**: Nessuno.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-398">**Session persistence**: None.</span></span>
   - <span data-ttu-id="4a6f4-399">**Timeout di inattività (minuti)**: 4.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-399">**Idle timeout (minutes)**: 4.</span></span>
   - <span data-ttu-id="4a6f4-400">**IP mobile (Direct Server Return)**: Abilitato.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-400">**Floating IP (direct server return)**: Enabled</span></span>

1. <span data-ttu-id="4a6f4-401">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-401">Click **OK**.</span></span>

## <a name="step-6-configure-cluster-for-probe"></a><span data-ttu-id="4a6f4-402">Passaggio 6: Configurare il cluster per il probe</span><span class="sxs-lookup"><span data-stu-id="4a6f4-402">Step 6: Configure cluster for probe</span></span>

<span data-ttu-id="4a6f4-403">Impostare parametro porta probe di cluster hello in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-403">Set hello cluster probe port parameter in PowerShell.</span></span>

<span data-ttu-id="4a6f4-404">tooset hello parametro porta probe di cluster, aggiornare le variabili in hello lo script seguente dall'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-404">tooset hello cluster probe port parameter, update variables in hello following script from your environment.</span></span>

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a><span data-ttu-id="4a6f4-405">Passaggio 7: Eseguire il failover dell'istanza del cluster di failover</span><span class="sxs-lookup"><span data-stu-id="4a6f4-405">Step 7: Test FCI failover</span></span>

<span data-ttu-id="4a6f4-406">Failover di test della funzionalità cluster di failover toovalidate hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-406">Test failover of hello FCI toovalidate cluster functionality.</span></span> <span data-ttu-id="4a6f4-407">Hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a6f4-407">Do hello following steps:</span></span>

1. <span data-ttu-id="4a6f4-408">Connettere tooone dei nodi del cluster di failover di SQL Server hello con RDP.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-408">Connect tooone of hello SQL Server FCI cluster nodes with RDP.</span></span>

1. <span data-ttu-id="4a6f4-409">Aprire **Gestione cluster di failover**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-409">Open **Failover Cluster Manager**.</span></span> <span data-ttu-id="4a6f4-410">Fare clic su **Ruoli**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-410">Click **Roles**.</span></span> <span data-ttu-id="4a6f4-411">Nota: il nodo detiene il ruolo di SQL Server FCI hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-411">Notice which node owns hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="4a6f4-412">Fare clic sul ruolo di hello istanza cluster di failover di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-412">Right-click hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="4a6f4-413">Scegliere **Sposta** e quindi fare clic su **Miglior nodo possibile**.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-413">Click **Move** and click **Best Possible Node**.</span></span>

<span data-ttu-id="4a6f4-414">**Gestione Cluster di failover** Mostra hello ruolo e le relative risorse offline.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-414">**Failover Cluster Manager** shows hello role and its resources go offline.</span></span> <span data-ttu-id="4a6f4-415">Hello risorse spostare e portare in linea in hello altro nodo.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-415">hello resources then move and come online on hello other node.</span></span>

### <a name="test-connectivity"></a><span data-ttu-id="4a6f4-416">Testare la connettività</span><span class="sxs-lookup"><span data-stu-id="4a6f4-416">Test connectivity</span></span>

<span data-ttu-id="4a6f4-417">connettività tootest, log nella macchina virtuale tooanother hello stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-417">tootest connectivity, log in tooanother virtual machine in hello same virtual network.</span></span> <span data-ttu-id="4a6f4-418">Aprire **SQL Server Management Studio** e connettersi toohello nome di istanza cluster di failover di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-418">Open **SQL Server Management Studio** and connect toohello SQL Server FCI name.</span></span>

>[!NOTE]
><span data-ttu-id="4a6f4-419">Se necessario, è possibile [scaricare SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="limitations"></a><span data-ttu-id="4a6f4-420">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="4a6f4-420">Limitations</span></span>
<span data-ttu-id="4a6f4-421">Nelle macchine virtuali di Azure, Microsoft Distributed Transaction Coordinator (DTC) non è supportata nella FCI perché hello porta RPC non è supportato dal servizio di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="4a6f4-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because hello RPC port is not supported by hello load balancer.</span></span>

## <a name="see-also"></a><span data-ttu-id="4a6f4-422">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="4a6f4-422">See Also</span></span>

[<span data-ttu-id="4a6f4-423">Configurare S2D con Desktop remoto (Azure)</span><span class="sxs-lookup"><span data-stu-id="4a6f4-423">Setup S2D with remote desktop (Azure)</span></span>](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

<span data-ttu-id="4a6f4-424">[Soluzione iperconvergente che usa Spazi di archiviazione diretta](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="4a6f4-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span></span>

[<span data-ttu-id="4a6f4-425">Panoramica di Spazi di archiviazione diretta</span><span class="sxs-lookup"><span data-stu-id="4a6f4-425">Storage Space Direct Overview</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[<span data-ttu-id="4a6f4-426">Supporto di SQL Server per S2D</span><span class="sxs-lookup"><span data-stu-id="4a6f4-426">SQL Server support for S2D</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
