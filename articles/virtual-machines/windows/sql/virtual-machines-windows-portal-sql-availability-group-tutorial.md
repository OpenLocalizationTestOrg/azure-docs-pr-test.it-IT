---
title: "Gruppi di disponibilità Server - macchine virtuali di Azure - esercitazione aaaSQL | Documenti Microsoft"
description: "Questa esercitazione viene illustrato come toocreate un SQL Server gruppo di disponibilità AlwaysOn in macchine virtuali di Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="16e28-103">Configurare manualmente un gruppo di disponibilità AlwaysOn in VM di Azure</span><span class="sxs-lookup"><span data-stu-id="16e28-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="16e28-104">Questa esercitazione viene illustrato come toocreate un SQL Server gruppo di disponibilità AlwaysOn in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="16e28-104">This tutorial shows how toocreate a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="16e28-105">esercitazione completa Hello crea un gruppo di disponibilità con una replica di database in due computer SQL Server.</span><span class="sxs-lookup"><span data-stu-id="16e28-105">hello complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="16e28-106">**Tempo stimato**: accetta toocomplete circa 30 minuti, una volta soddisfatti i prerequisiti di hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-106">**Time estimate**: Takes about 30 minutes toocomplete once hello prerequisites are met.</span></span>

<span data-ttu-id="16e28-107">diagramma di Hello illustra ciò che si compila in esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-107">hello diagram illustrates what you build in hello tutorial.</span></span>

![Gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="16e28-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="16e28-109">Prerequisites</span></span>

<span data-ttu-id="16e28-110">esercitazione Hello presuppone di che avere una conoscenza di base di SQL Server di gruppi di disponibilità AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="16e28-110">hello tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="16e28-111">Se sono necessarie altre informazioni, vedere [Panoramica di Gruppi di disponibilità AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span><span class="sxs-lookup"><span data-stu-id="16e28-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="16e28-112">Hello nella tabella seguente elenca i prerequisiti di hello che è necessario toocomplete prima di iniziare questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="16e28-112">hello following table lists hello prerequisites that you need toocomplete before starting this tutorial:</span></span>

|  |<span data-ttu-id="16e28-113">Requisito</span><span class="sxs-lookup"><span data-stu-id="16e28-113">Requirement</span></span> |<span data-ttu-id="16e28-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="16e28-114">Description</span></span> |
|----- |----- |----- |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="16e28-116">Due istanze di SQL Server</span><span class="sxs-lookup"><span data-stu-id="16e28-116">Two SQL Servers</span></span> | <span data-ttu-id="16e28-117">- In un set di disponibilità di Azure</span><span class="sxs-lookup"><span data-stu-id="16e28-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="16e28-118">- In un dominio singolo</span><span class="sxs-lookup"><span data-stu-id="16e28-118">- In a single domain</span></span> <br/> <span data-ttu-id="16e28-119">- Con la funzionalità Clustering di failover installata</span><span class="sxs-lookup"><span data-stu-id="16e28-119">- With Failover Clustering feature installed</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="16e28-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="16e28-121">Windows Server</span></span> | <span data-ttu-id="16e28-122">Controllo di condivisione file per il cluster</span><span class="sxs-lookup"><span data-stu-id="16e28-122">File share for cluster witness</span></span> |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="16e28-124">Account del servizio SQL Server</span><span class="sxs-lookup"><span data-stu-id="16e28-124">SQL Server service account</span></span> | <span data-ttu-id="16e28-125">Account di dominio</span><span class="sxs-lookup"><span data-stu-id="16e28-125">Domain account</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="16e28-127">Account del servizio SQL Server Agent</span><span class="sxs-lookup"><span data-stu-id="16e28-127">SQL Server Agent service account</span></span> | <span data-ttu-id="16e28-128">Account di dominio</span><span class="sxs-lookup"><span data-stu-id="16e28-128">Domain account</span></span> |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="16e28-130">Porte del firewall aperte</span><span class="sxs-lookup"><span data-stu-id="16e28-130">Firewall ports open</span></span> | <span data-ttu-id="16e28-131">- SQL Server: **1433** per l'istanza predefinita</span><span class="sxs-lookup"><span data-stu-id="16e28-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="16e28-132">- Endpoint del mirroring del database: **5022** o qualsiasi porta disponibile</span><span class="sxs-lookup"><span data-stu-id="16e28-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="16e28-133">- Probe di bilanciamento del carico di Azure: **59999** o qualsiasi porta disponibile</span><span class="sxs-lookup"><span data-stu-id="16e28-133">- Azure load balancer probe: **59999** or any available port</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="16e28-135">Aggiunta della funzionalità Clustering di failover</span><span class="sxs-lookup"><span data-stu-id="16e28-135">Add Failover Clustering Feature</span></span> | <span data-ttu-id="16e28-136">Questa funzionalità è necessaria per entrambe le istanze di SQL Server</span><span class="sxs-lookup"><span data-stu-id="16e28-136">Both SQL Servers require this feature</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="16e28-138">Account di dominio dell'installazione</span><span class="sxs-lookup"><span data-stu-id="16e28-138">Installation domain account</span></span> | <span data-ttu-id="16e28-139">- Amministratore locale in ogni istanza di SQL Server</span><span class="sxs-lookup"><span data-stu-id="16e28-139">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="16e28-140">- Membro del ruolo predefinito del server sysadmin di SQL Server per ogni istanza di SQL Server</span><span class="sxs-lookup"><span data-stu-id="16e28-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="16e28-141">Prima di iniziare l'esercitazione hello, è necessario troppo[completare i prerequisiti per la creazione di gruppi di disponibilità AlwaysOn in macchine virtuali di Azure](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span><span class="sxs-lookup"><span data-stu-id="16e28-141">Before you begin hello tutorial, you need too[Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="16e28-142">Se questi prerequisiti sono già completati, è possibile passare troppo[crea Cluster](#CreateCluster).</span><span class="sxs-lookup"><span data-stu-id="16e28-142">If these prerequisites are completed already, you can jump too[Create Cluster](#CreateCluster).</span></span>


<span data-ttu-id="16e28-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Creare il cluster hello</span><span class="sxs-lookup"><span data-stu-id="16e28-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## Create hello cluster</span></span>

<span data-ttu-id="16e28-144">Dopo aver hello vengono soddisfatti i prerequisiti, hello primo passaggio consiste toocreate un Cluster di Failover di Windows Server che include due SQL Server e un server di controllo.</span><span class="sxs-lookup"><span data-stu-id="16e28-144">After hello prerequisites are completed, hello first step is toocreate a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>  

1. <span data-ttu-id="16e28-145">RDP toohello prima di SQL Server utilizzando un account di dominio che un amministratore del server SQL sia il server di controllo di hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-145">RDP toohello first SQL Server using a domain account that is an administrator on both SQL Servers and hello witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="16e28-146">Se si sono seguite hello [documento prerequisiti](virtual-machines-windows-portal-sql-availability-group-prereq.md), è stato creato un account denominato **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="16e28-146">If you followed hello [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="16e28-147">Usare questo account.</span><span class="sxs-lookup"><span data-stu-id="16e28-147">Use this account.</span></span>

2. <span data-ttu-id="16e28-148">In hello **Server Manager** dashboard, selezionare **strumenti**, quindi fare clic su **gestione Cluster di Failover**.</span><span class="sxs-lookup"><span data-stu-id="16e28-148">In hello **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="16e28-149">Nel riquadro di sinistra hello, fare doppio clic su **gestione Cluster di Failover**, quindi fare clic su **creare un Cluster**.</span><span class="sxs-lookup"><span data-stu-id="16e28-149">In hello left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="16e28-150">![Creare un cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="16e28-150">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="16e28-151">In Creazione guidata Cluster hello, creare un cluster a un nodo avanzando pagine hello con le impostazioni di hello in hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="16e28-151">In hello Create Cluster Wizard, create a one-node cluster by stepping through hello pages with hello settings in hello following table:</span></span>

   | <span data-ttu-id="16e28-152">Page</span><span class="sxs-lookup"><span data-stu-id="16e28-152">Page</span></span> | <span data-ttu-id="16e28-153">Impostazioni</span><span class="sxs-lookup"><span data-stu-id="16e28-153">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="16e28-154">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="16e28-154">Before You Begin</span></span> |<span data-ttu-id="16e28-155">Valori predefiniti</span><span class="sxs-lookup"><span data-stu-id="16e28-155">Use defaults</span></span> |
   | <span data-ttu-id="16e28-156">Selezione dei server</span><span class="sxs-lookup"><span data-stu-id="16e28-156">Select Servers</span></span> |<span data-ttu-id="16e28-157">Prima di SQL Server nome in hello di tipo **immettere il nome del server** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="16e28-157">Type hello first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="16e28-158">Avviso di convalida</span><span class="sxs-lookup"><span data-stu-id="16e28-158">Validation Warning</span></span> |<span data-ttu-id="16e28-159">Selezionare **Nr I non è necessario supporto da Microsoft per questo cluster e pertanto non si desidera che la convalida di hello toorun test. Quando fa clic su Avanti, continuare con la creazione di cluster hello**.</span><span class="sxs-lookup"><span data-stu-id="16e28-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want toorun hello validation tests. When I click Next, continue Creating hello cluster**.</span></span> |
   | <span data-ttu-id="16e28-160">Punto di accesso per hello amministrazione Cluster</span><span class="sxs-lookup"><span data-stu-id="16e28-160">Access Point for Administering hello Cluster</span></span> |<span data-ttu-id="16e28-161">Digitare un nome di cluster, ad esempio **SQLAGCluster1**, in **Nome cluster**.</span><span class="sxs-lookup"><span data-stu-id="16e28-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="16e28-162">Conferma</span><span class="sxs-lookup"><span data-stu-id="16e28-162">Confirmation</span></span> |<span data-ttu-id="16e28-163">Usare le impostazioni predefinite a meno a meno che non si usino spazi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="16e28-163">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="16e28-164">Vedere la nota di hello segue questa tabella.</span><span class="sxs-lookup"><span data-stu-id="16e28-164">See hello note following this table.</span></span> |

### <a name="set-hello-cluster-ip-address"></a><span data-ttu-id="16e28-165">Impostare l'indirizzo IP del cluster hello</span><span class="sxs-lookup"><span data-stu-id="16e28-165">Set hello cluster IP address</span></span>

1. <span data-ttu-id="16e28-166">In **gestione Cluster di Failover**, scorrere verso il basso troppo**risorse principali del Cluster** ed espandere i dettagli del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-166">In **Failover Cluster Manager**, scroll down too**Cluster Core Resources** and expand hello cluster details.</span></span> <span data-ttu-id="16e28-167">Dovrebbe essere entrambi hello **nome** hello e **indirizzo IP** risorse hello **Failed** stato.</span><span class="sxs-lookup"><span data-stu-id="16e28-167">You should see both hello **Name** and hello **IP Address** resources in hello **Failed** state.</span></span> <span data-ttu-id="16e28-168">Hello risorsa indirizzo IP non può essere portata online perché il cluster di hello è assegnato hello stesso indirizzo IP come macchina hello stessa, pertanto è un indirizzo duplicato.</span><span class="sxs-lookup"><span data-stu-id="16e28-168">hello IP address resource cannot be brought online because hello cluster is assigned hello same IP address as hello machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="16e28-169">Hello pulsante destro del mouse non è stato possibile **indirizzo IP** risorsa e quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="16e28-169">Right-click hello failed **IP Address** resource, and then click **Properties**.</span></span>

   ![Proprietà del cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="16e28-171">Selezionare **indirizzo IP statico** e specificare un indirizzo disponibile dalla subnet in cui SQL Server hello è nella casella di testo indirizzo hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-171">Select **Static IP Address** and specify an available address from subnet where hello SQL Server is in hello Address text box.</span></span> <span data-ttu-id="16e28-172">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="16e28-172">Then, click **OK**.</span></span>
4. <span data-ttu-id="16e28-173">In hello **risorse principali del Cluster** sezione, fare doppio clic su nome cluster e fare clic su **in linea**.</span><span class="sxs-lookup"><span data-stu-id="16e28-173">In hello **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="16e28-174">Attendere finché entrambe le risorse non sono online</span><span class="sxs-lookup"><span data-stu-id="16e28-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="16e28-175">Quando risorsa del nome cluster hello torna online, il server di controller di dominio hello viene aggiornato con un nuovo account computer di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16e28-175">When hello cluster name resource comes online, it updates hello DC server with a new AD computer account.</span></span> <span data-ttu-id="16e28-176">Utilizzare questo hello toorun di AD account servizio di gruppo di disponibilità in cluster in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="16e28-176">Use this AD account toorun hello Availability Group clustered service later.</span></span>

### <span data-ttu-id="16e28-177"><a name="addNode"></a>Aggiungere hello altri toocluster di SQL Server</span><span class="sxs-lookup"><span data-stu-id="16e28-177"><a name="addNode"></a>Add hello other SQL Server toocluster</span></span>

<span data-ttu-id="16e28-178">Aggiungere altri cluster di SQL Server toohello hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-178">Add hello other SQL Server toohello cluster.</span></span>

1. <span data-ttu-id="16e28-179">Nell'albero di browser hello, fare doppio clic su cluster hello e fare clic su **aggiunta del nodo**.</span><span class="sxs-lookup"><span data-stu-id="16e28-179">In hello browser tree, right-click hello cluster and click **Add Node**.</span></span>

    ![Aggiungere toohello nodo Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="16e28-181">In hello **Aggiunta guidata nodi**, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-181">In hello **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="16e28-182">In hello **selezione dei server** pagina, aggiungere hello secondo computer SQL Server.</span><span class="sxs-lookup"><span data-stu-id="16e28-182">In hello **Select Servers** page, add hello second SQL Server.</span></span> <span data-ttu-id="16e28-183">Nome del server di tipo hello in **immettere il nome del server** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="16e28-183">Type hello server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="16e28-184">Al termine dell'operazione, scegliere **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="16e28-185">In hello **avviso di convalida** pagina, fare clic su **n** (in uno scenario di produzione è necessario eseguire il test di convalida hello).</span><span class="sxs-lookup"><span data-stu-id="16e28-185">In hello **Validation Warning** page, click **No** (in a production scenario you should perform hello validation tests).</span></span> <span data-ttu-id="16e28-186">Quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="16e28-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="16e28-187">In hello **conferma** pagina se si utilizza spazi di archiviazione, con l'etichetta casella di controllo crittografato hello **aggiungere tutte le risorse di archiviazione idonee toohello cluster.**</span><span class="sxs-lookup"><span data-stu-id="16e28-187">In hello **Confirmation** page if you are using Storage Spaces, clear hello checkbox labeled **Add all eligible storage toohello cluster.**</span></span>

   ![Confermare l'aggiunta del nodo](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="16e28-189">Se si utilizza spazi di archiviazione e non si deseleziona **aggiungere tutte le risorse di archiviazione idonee toohello cluster**, Windows consente di scollegare i dischi virtuali hello durante il processo di clustering hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage toohello cluster**, Windows detaches hello virtual disks during hello clustering process.</span></span> <span data-ttu-id="16e28-190">Di conseguenza, essi non vengono visualizzati in Gestione disco o Esplora fino a quando non vengono rimossi gli spazi di archiviazione di hello dal cluster hello e ricollegati tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="16e28-190">As a result, they do not appear in Disk Manager or Explorer until hello storage spaces are removed from hello cluster and reattached using PowerShell.</span></span> <span data-ttu-id="16e28-191">Spazi di archiviazione consente di raggruppare più dischi nel pool di toostorage.</span><span class="sxs-lookup"><span data-stu-id="16e28-191">Storage Spaces groups multiple disks in toostorage pools.</span></span> <span data-ttu-id="16e28-192">Per altre informazioni, vedere [Spazi di archiviazione](https://technet.microsoft.com/library/hh831739).</span><span class="sxs-lookup"><span data-stu-id="16e28-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="16e28-193">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-193">Click **Next**.</span></span>

1. <span data-ttu-id="16e28-194">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="16e28-194">Click **Finish**.</span></span>

   <span data-ttu-id="16e28-195">Gestione Cluster di failover mostra che il cluster dispone di un nuovo nodo ed elencato in hello **nodi** contenitore.</span><span class="sxs-lookup"><span data-stu-id="16e28-195">Failover Cluster Manager shows that your cluster has a new node and lists it in hello **Nodes** container.</span></span>

10. <span data-ttu-id="16e28-196">Disconnettersi dalla sessione desktop remoto hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-196">Log out of hello remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="16e28-197">Aggiungere una condivisione file di quorum del cluster</span><span class="sxs-lookup"><span data-stu-id="16e28-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="16e28-198">In questo esempio il cluster di Windows hello Usa un toocreate di condivisione di un quorum di cluster di file.</span><span class="sxs-lookup"><span data-stu-id="16e28-198">In this example hello Windows cluster uses a file share toocreate a cluster quorum.</span></span> <span data-ttu-id="16e28-199">Questa esercitazione usa un quorum Maggioranza dei nodi e delle condivisioni file.</span><span class="sxs-lookup"><span data-stu-id="16e28-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="16e28-200">Per altre informazioni, vedere [Informazioni sulle configurazioni quorum in un cluster di failover](http://technet.microsoft.com/library/cc731739.aspx).</span><span class="sxs-lookup"><span data-stu-id="16e28-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="16e28-201">Connettere i server membro di controllo della condivisione file toohello con una sessione desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="16e28-201">Connect toohello file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="16e28-202">In **Server Manager** fare clic su **Strumenti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="16e28-203">Aprire **Gestione computer**.</span><span class="sxs-lookup"><span data-stu-id="16e28-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="16e28-204">Fare clic su **Cartelle condivise**.</span><span class="sxs-lookup"><span data-stu-id="16e28-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="16e28-205">Fare clic con il pulsante destro del mouse su **Condivisioni** e scegliere **Nuova condivisione**.</span><span class="sxs-lookup"><span data-stu-id="16e28-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Nuova condivisione](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="16e28-207">Utilizzare **creare una cartella condivisa** toocreate una condivisione.</span><span class="sxs-lookup"><span data-stu-id="16e28-207">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="16e28-208">In **percorso della cartella**, fare clic su **Sfoglia** e individuare o creare un percorso per la cartella condivisa di hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-208">On **Folder Path**, click **Browse** and locate or create a path for hello shared folder.</span></span> <span data-ttu-id="16e28-209">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-209">Click **Next**.</span></span>

1. <span data-ttu-id="16e28-210">In **nome, descrizione e le impostazioni** verificare il nome di condivisione hello e il percorso.</span><span class="sxs-lookup"><span data-stu-id="16e28-210">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="16e28-211">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-211">Click **Next**.</span></span>

1. <span data-ttu-id="16e28-212">In **Autorizzazioni cartella condivisa** impostare **Personalizza autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="16e28-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="16e28-213">Fare clic su **Personalizza**.</span><span class="sxs-lookup"><span data-stu-id="16e28-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="16e28-214">In **Personalizza autorizzazioni** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="16e28-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="16e28-215">Verificare che il cluster di hello hello toocreate account utilizzato dispone del controllo completo.</span><span class="sxs-lookup"><span data-stu-id="16e28-215">Make sure that hello account used toocreate hello cluster has full control.</span></span>

   ![Nuova condivisione](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="16e28-217">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="16e28-217">Click **OK**.</span></span>

1. <span data-ttu-id="16e28-218">In **Autorizzazioni cartella condivisa** fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="16e28-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="16e28-219">Fare di nuovo clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="16e28-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="16e28-220">Disconnettersi da server hello</span><span class="sxs-lookup"><span data-stu-id="16e28-220">Log out of hello server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="16e28-221">Configurare il quorum del cluster</span><span class="sxs-lookup"><span data-stu-id="16e28-221">Configure cluster quorum</span></span>

<span data-ttu-id="16e28-222">Quindi, impostare quorum del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-222">Next, set hello cluster quorum.</span></span>

1. <span data-ttu-id="16e28-223">Connettere toohello primo nodo del cluster con desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="16e28-223">Connect toohello first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="16e28-224">In **gestione Cluster di Failover**, fare doppio clic su cluster hello, scegliere troppo**altre azioni**, fare clic su **Configura impostazioni Quorum del Cluster...** .</span><span class="sxs-lookup"><span data-stu-id="16e28-224">In **Failover Cluster Manager**, right-click hello cluster, point too**More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![Nuova condivisione](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="16e28-226">In **Configurazione guidata quorum del cluster** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="16e28-227">In **selezione opzione configurazione Quorum**, scegliere **selezione quorum di controllo hello**, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-227">In **Select Quorum Configuration Option**, choose **Select hello quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="16e28-228">In **Selezione quorum di controllo** fare clic su **Configura condivisione file di controllo**.</span><span class="sxs-lookup"><span data-stu-id="16e28-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="16e28-229">Windows Server 2016 supporta un cloud di controllo.</span><span class="sxs-lookup"><span data-stu-id="16e28-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="16e28-230">Se si sceglie questo tipo di controllo, non è necessario un controllo di condivisione file.</span><span class="sxs-lookup"><span data-stu-id="16e28-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="16e28-231">Per altre informazioni, vedere [Distribuire un cloud di controllo per un cluster di failover](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="16e28-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="16e28-232">Questa esercitazione usa un controllo di condivisione file, supportato dai sistemi operativi precedenti.</span><span class="sxs-lookup"><span data-stu-id="16e28-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="16e28-233">In **configurazione Witness di condivisione File**, percorso hello del tipo per la condivisione di hello creata.</span><span class="sxs-lookup"><span data-stu-id="16e28-233">On **Configure File Share Witness**, type hello path for hello share you created.</span></span> <span data-ttu-id="16e28-234">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-234">Click **Next**.</span></span>

1. <span data-ttu-id="16e28-235">Verificare le impostazioni di hello in **conferma**.</span><span class="sxs-lookup"><span data-stu-id="16e28-235">Verify hello settings on **Confirmation**.</span></span> <span data-ttu-id="16e28-236">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-236">Click **Next**.</span></span>

1. <span data-ttu-id="16e28-237">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="16e28-237">Click **Finish**.</span></span>

<span data-ttu-id="16e28-238">risorse principali del cluster Hello vengono configurate con una condivisione file di controllo.</span><span class="sxs-lookup"><span data-stu-id="16e28-238">hello cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="16e28-239">Abilitare i gruppi di disponibilità</span><span class="sxs-lookup"><span data-stu-id="16e28-239">Enable Availability Groups</span></span>

<span data-ttu-id="16e28-240">Successivamente, abilitare hello **gruppi di disponibilità AlwaysOn** funzionalità.</span><span class="sxs-lookup"><span data-stu-id="16e28-240">Next, enable hello **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="16e28-241">Eseguire questi passaggi in entrambe le istanze di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="16e28-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="16e28-242">Da hello **avviare** schermata, avviare **Gestione configurazione SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="16e28-242">From hello **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="16e28-243">Nella struttura di browser hello, fare clic su **servizi di SQL Server**, quindi fare doppio clic su hello **SQL Server (MSSQLSERVER)** del servizio e fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="16e28-243">In hello browser tree, click **SQL Server Services**, then right-click hello **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="16e28-244">Fare clic su hello **disponibilità elevata AlwaysOn** tab, quindi selezionare **Abilita gruppi di disponibilità AlwaysOn**, come segue:</span><span class="sxs-lookup"><span data-stu-id="16e28-244">Click hello **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![Abilitare Gruppi di disponibilità AlwaysOn in Azure](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="16e28-246">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="16e28-246">Click **Apply**.</span></span> <span data-ttu-id="16e28-247">Fare clic su **OK** nella finestra di dialogo popup hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-247">Click **OK** in hello pop-up dialog.</span></span>

5. <span data-ttu-id="16e28-248">Riavviare il servizio di SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-248">Restart hello SQL Server service.</span></span>

<span data-ttu-id="16e28-249">Ripetere questi passaggi in hello altro SQL Server.</span><span class="sxs-lookup"><span data-stu-id="16e28-249">Repeat these steps on hello other SQL Server.</span></span>

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a><span data-ttu-id="16e28-250">Creare un database in hello prima di SQL Server</span><span class="sxs-lookup"><span data-stu-id="16e28-250">Create a database on hello first SQL Server</span></span>

1. <span data-ttu-id="16e28-251">Avvio hello RDP file toohello prima di SQL Server con un dominio dell'account che è un membro del ruolo sysadmin ruolo del server.</span><span class="sxs-lookup"><span data-stu-id="16e28-251">Launch hello RDP file toohello first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="16e28-252">Aprire SQL Server Management Studio e connettersi toohello prima di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="16e28-252">Open SQL Server Management Studio and connect toohello first SQL Server.</span></span>
7. <span data-ttu-id="16e28-253">In **Esplora oggetti** fare clic con il pulsante destro del mouse su **Database** e scegliere **Nuovo database**.</span><span class="sxs-lookup"><span data-stu-id="16e28-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="16e28-254">In **Nome database** digitare **MyDB1**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="16e28-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <span data-ttu-id="16e28-255"><a name="backupshare"></a> Creare una condivisione di backup</span><span class="sxs-lookup"><span data-stu-id="16e28-255"><a name="backupshare"></a> Create a backup share</span></span>

1. <span data-ttu-id="16e28-256">In hello prima di SQL Server in **Server Manager**, fare clic su **strumenti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-256">On hello first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="16e28-257">Aprire **Gestione computer**.</span><span class="sxs-lookup"><span data-stu-id="16e28-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="16e28-258">Fare clic su **Cartelle condivise**.</span><span class="sxs-lookup"><span data-stu-id="16e28-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="16e28-259">Fare clic con il pulsante destro del mouse su **Condivisioni** e scegliere **Nuova condivisione**.</span><span class="sxs-lookup"><span data-stu-id="16e28-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Nuova condivisione](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="16e28-261">Utilizzare **creare una cartella condivisa** toocreate una condivisione.</span><span class="sxs-lookup"><span data-stu-id="16e28-261">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="16e28-262">In **percorso della cartella**, fare clic su **Sfoglia** e individuare o creare un percorso della cartella condivisa backup database hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-262">On **Folder Path**, click **Browse** and locate or create a path for hello database backup shared folder.</span></span> <span data-ttu-id="16e28-263">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-263">Click **Next**.</span></span>

1. <span data-ttu-id="16e28-264">In **nome, descrizione e le impostazioni** verificare il nome di condivisione hello e il percorso.</span><span class="sxs-lookup"><span data-stu-id="16e28-264">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="16e28-265">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-265">Click **Next**.</span></span>

1. <span data-ttu-id="16e28-266">In **Autorizzazioni cartella condivisa** impostare **Personalizza autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="16e28-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="16e28-267">Fare clic su **Personalizza**.</span><span class="sxs-lookup"><span data-stu-id="16e28-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="16e28-268">In **Personalizza autorizzazioni** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="16e28-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="16e28-269">Assicurarsi di disporre di un account di servizio di SQL Server e SQL Server Agent hello per entrambi i server di controllo completo.</span><span class="sxs-lookup"><span data-stu-id="16e28-269">Make sure that hello SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![Nuova condivisione](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="16e28-271">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="16e28-271">Click **OK**.</span></span>

1. <span data-ttu-id="16e28-272">In **Autorizzazioni cartella condivisa** fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="16e28-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="16e28-273">Fare di nuovo clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="16e28-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-hello-database"></a><span data-ttu-id="16e28-274">Eseguire un backup del database hello completo</span><span class="sxs-lookup"><span data-stu-id="16e28-274">Take a full backup of hello database</span></span>

<span data-ttu-id="16e28-275">È necessario tooback backup hello nuova database tooinitialize hello catena di log.</span><span class="sxs-lookup"><span data-stu-id="16e28-275">You need tooback up hello new database tooinitialize hello log chain.</span></span> <span data-ttu-id="16e28-276">Se non si adotta un backup del database nuovo hello, non può essere inclusa in un gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="16e28-276">If you do not take a backup of hello new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="16e28-277">In **Esplora oggetti**, fare doppio clic su database hello, scegliere troppo**attività...** , fare clic su **backup**.</span><span class="sxs-lookup"><span data-stu-id="16e28-277">In **Object Explorer**, right-click hello database, point too**Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="16e28-278">Fare clic su **OK** tootake un percorso di backup predefinito toohello backup completo.</span><span class="sxs-lookup"><span data-stu-id="16e28-278">Click **OK** tootake a full backup toohello default backup location.</span></span>

## <a name="create-hello-availability-group"></a><span data-ttu-id="16e28-279">Creare il gruppo di disponibilità hello</span><span class="sxs-lookup"><span data-stu-id="16e28-279">Create hello Availability Group</span></span>
<span data-ttu-id="16e28-280">Si è ora pronto tooconfigure un gruppo di disponibilità utilizzando hello seguendo i passaggi:</span><span class="sxs-lookup"><span data-stu-id="16e28-280">You are now ready tooconfigure an Availability Group using hello following steps:</span></span>

* <span data-ttu-id="16e28-281">Creare un database in hello prima di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="16e28-281">Create a database on hello first SQL Server.</span></span>
* <span data-ttu-id="16e28-282">Eseguire un backup completo e un backup del log delle transazioni del database hello</span><span class="sxs-lookup"><span data-stu-id="16e28-282">Take both a full backup and a transaction log backup of hello database</span></span>
* <span data-ttu-id="16e28-283">Hello ripristino completo e toohello backup log secondo SQL Server con hello **NORECOVERY** opzione</span><span class="sxs-lookup"><span data-stu-id="16e28-283">Restore hello full and log backups toohello second SQL Server with hello **NORECOVERY** option</span></span>
* <span data-ttu-id="16e28-284">Creare il gruppo di disponibilità hello (**AG1**) con commit sincrono, il failover automatico e repliche secondarie leggibili</span><span class="sxs-lookup"><span data-stu-id="16e28-284">Create hello Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-hello-availability-group"></a><span data-ttu-id="16e28-285">Creare il gruppo di disponibilità hello:</span><span class="sxs-lookup"><span data-stu-id="16e28-285">Create hello Availability Group:</span></span>

1. <span data-ttu-id="16e28-286">Nella sessione desktop remoto toohello prima di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="16e28-286">On remote desktop session toohello first SQL Server.</span></span> <span data-ttu-id="16e28-287">In **Esplora oggetti** in SSMS fare clic con il pulsante destro del mouse su **Disponibilità elevata AlwaysOn**, quindi scegliere **Creazione guidata Gruppo di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="16e28-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![Avviare la creazione guidata nuovo gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="16e28-289">In hello **Introduzione** pagina, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-289">In hello **Introduction** page, click **Next**.</span></span> <span data-ttu-id="16e28-290">In hello **Specifica nome del gruppo di disponibilità** , digitare un nome per hello gruppo di disponibilità, ad esempio **AG1**nella **nome gruppo di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="16e28-290">In hello **Specify Availability Group Name** page, type a name for hello Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="16e28-291">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-291">Click **Next**.</span></span>

    ![Creazione guidata nuovo gruppo di disponibilità: specificare il nome di gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="16e28-293">In hello **Seleziona database** pagina, selezionare il database e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-293">In hello **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="16e28-294">database Hello soddisfi i prerequisiti di hello per un gruppo di disponibilità perché non si è effettuato almeno un backup completo sulla replica primaria prevista hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-294">hello database meets hello prerequisites for an Availability Group because you have taken at least one full backup on hello intended primary replica.</span></span>

   ![Creazione guidata nuovo gruppo di disponibilità: selezionare i database](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="16e28-296">In hello **specifica repliche** pagina, fare clic su **Aggiungi Replica**.</span><span class="sxs-lookup"><span data-stu-id="16e28-296">In hello **Specify Replicas** page, click **Add Replica**.</span></span>

   ![Creazione guidata nuovo gruppo di disponibilità: specificare le repliche](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="16e28-298">Hello **connettersi tooServer** visualizzata la finestra di.</span><span class="sxs-lookup"><span data-stu-id="16e28-298">hello **Connect tooServer** dialog pops up.</span></span> <span data-ttu-id="16e28-299">Nome del secondo server di hello in hello di tipo **nome Server**.</span><span class="sxs-lookup"><span data-stu-id="16e28-299">Type hello name of hello second server in **Server name**.</span></span> <span data-ttu-id="16e28-300">Fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-300">Click **Connect**.</span></span>

   <span data-ttu-id="16e28-301">In hello **specifica repliche** pagina, dovrebbe essere secondo server hello elencati in **le repliche di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="16e28-301">Back in hello **Specify Replicas** page, you should now see hello second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="16e28-302">Configurare le repliche di hello come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="16e28-302">Configure hello replicas as follows.</span></span>

   ![Creazione guidata nuovo gruppo di disponibilità: specificare le repliche (complete)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="16e28-304">Fare clic su **endpoint** toosee hello endpoint del mirroring per questo gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="16e28-304">Click **Endpoints** toosee hello database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="16e28-305">Hello utilizzare stessa porta utilizzata quando si imposta hello [regola del firewall per endpoint di mirroring del database](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="16e28-305">Use hello same port that you used when you set hello [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![Creazione guidata nuovo gruppo di disponibilità: selezionare la sincronizzazione dati iniziale](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="16e28-307">In hello **seleziona sincronizzazione dati iniziale** selezionare **completo** e specificare un percorso di rete condivisa.</span><span class="sxs-lookup"><span data-stu-id="16e28-307">In hello **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="16e28-308">Per il percorso di hello, utilizzare hello [condivisione di backup creato](#backupshare).</span><span class="sxs-lookup"><span data-stu-id="16e28-308">For hello location, use hello [backup share that you created](#backupshare).</span></span> <span data-ttu-id="16e28-309">Nell'esempio hello è **\\\\\<prima di SQL Server\>\Backup\**.</span><span class="sxs-lookup"><span data-stu-id="16e28-309">In hello example it was, **\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="16e28-310">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="16e28-311">Sincronizzazione completa richiede un backup completo del database hello in prima istanza di SQL Server del hello e ripristinarlo toohello seconda istanza.</span><span class="sxs-lookup"><span data-stu-id="16e28-311">Full synchronization takes a full backup of hello database on hello first instance of SQL Server and restores it toohello second instance.</span></span> <span data-ttu-id="16e28-312">Per i database di grandi dimensioni, la sincronizzazione completa non è consigliabile perché può richiedere diverso tempo.</span><span class="sxs-lookup"><span data-stu-id="16e28-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="16e28-313">Per ridurre questo momento, eseguire un backup del database hello manualmente e il ripristino con `NO RECOVERY`.</span><span class="sxs-lookup"><span data-stu-id="16e28-313">You can reduce this time by manually taking a backup of hello database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="16e28-314">Se il database di hello è già ripristinato con `NO RECOVERY` su hello secondo SQL Server prima di configurare il gruppo di disponibilità hello, scegliere **solo Join**.</span><span class="sxs-lookup"><span data-stu-id="16e28-314">If hello database is already restored with `NO RECOVERY` on hello second SQL Server before configuring hello Availability Group, choose **Join only**.</span></span> <span data-ttu-id="16e28-315">Se si desidera backup hello tootake dopo aver configurato il gruppo di disponibilità hello, scegliere **Ignora sincronizzazione dati iniziale**.</span><span class="sxs-lookup"><span data-stu-id="16e28-315">If you want tootake hello backup after configuring hello Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![Creazione guidata nuovo gruppo di disponibilità: selezionare la sincronizzazione dati iniziale](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="16e28-317">In hello **convalida** pagina, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="16e28-317">In hello **Validation** page, click **Next**.</span></span> <span data-ttu-id="16e28-318">Questa pagina dovrebbe essere simile toohello seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="16e28-318">This page should look similar toohello following image:</span></span>

    ![Creazione guidata nuovo gruppo di disponibilità: convalida](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="16e28-320">Si verifica un avviso per la configurazione del listener hello poiché non è stato configurato un listener del gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="16e28-320">There is a warning for hello listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="16e28-321">È possibile ignorare questo avviso perché in macchine virtuali di Azure crea listener hello dopo la creazione di bilanciamento del carico Azure hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-321">You can ignore this warning because on Azure virtual machines you create hello listener after creating hello Azure load balancer.</span></span>

10. <span data-ttu-id="16e28-322">In hello **riepilogo** pagina, fare clic su **fine**, quindi attendere la procedura guidata hello Configura hello nuovo gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="16e28-322">In hello **Summary** page, click **Finish**, then wait while hello wizard configures hello new Availability Group.</span></span> <span data-ttu-id="16e28-323">In hello **lo stato di avanzamento** pagina, è possibile fare clic su **ulteriori dettagli** tooview hello dettagliate lo stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="16e28-323">In hello **Progress** page, you can click **More details** tooview hello detailed progress.</span></span> <span data-ttu-id="16e28-324">La procedura guidata hello termine, controllare hello **risultati** tooverify pagina che hello gruppo di disponibilità è stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="16e28-324">Once hello wizard is finished, inspect hello **Results** page tooverify that hello Availability Group is successfully created.</span></span>

     ![Creazione guidata nuovo gruppo di disponibilità: risultati](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="16e28-326">Fare clic su **Chiudi** guidata hello tooexit.</span><span class="sxs-lookup"><span data-stu-id="16e28-326">Click **Close** tooexit hello wizard.</span></span>

### <a name="check-hello-availability-group"></a><span data-ttu-id="16e28-327">Hello controllo gruppo di disponibilità</span><span class="sxs-lookup"><span data-stu-id="16e28-327">Check hello Availability Group</span></span>

1. <span data-ttu-id="16e28-328">In **Esplora oggetti** espandere **Disponibilità elevata AlwaysOn**, quindi espandere **Gruppi di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="16e28-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="16e28-329">Dovrebbe essere hello nuovo gruppo di disponibilità in questo contenitore.</span><span class="sxs-lookup"><span data-stu-id="16e28-329">You should now see hello new Availability Group in this container.</span></span> <span data-ttu-id="16e28-330">Fare doppio clic su hello gruppo di disponibilità e fare clic su **Mostra Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="16e28-330">Right-click hello Availability Group and click **Show Dashboard**.</span></span>

   ![Mostrare dashboard gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="16e28-332">Il **AlwaysOn Dashboard** dovrebbe essere simile toothis.</span><span class="sxs-lookup"><span data-stu-id="16e28-332">Your **AlwaysOn Dashboard** should look similar toothis.</span></span>

   ![Dashboard gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="16e28-334">È possibile visualizzare le repliche hello, la modalità di failover di ogni stato di sincronizzazione di replica e hello hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-334">You can see hello replicas, hello failover mode of each replica and hello synchronization state.</span></span>

2. <span data-ttu-id="16e28-335">In **Gestione cluster di failover** fare clic sul cluster.</span><span class="sxs-lookup"><span data-stu-id="16e28-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="16e28-336">Selezionare **Ruoli**.</span><span class="sxs-lookup"><span data-stu-id="16e28-336">Select **Roles**.</span></span> <span data-ttu-id="16e28-337">Nome gruppo di disponibilità Hello utilizzato è un ruolo nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-337">hello Availability Group name you used is a role on hello cluster.</span></span> <span data-ttu-id="16e28-338">Tale gruppo di disponibilità non ha un indirizzo IP per le connessioni client, perché non è stato configurato un listener.</span><span class="sxs-lookup"><span data-stu-id="16e28-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="16e28-339">Dopo aver creato un servizio di bilanciamento del carico di Azure, sarà necessario configurare il listener hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-339">You will configure hello listener after you create an Azure load balancer.</span></span>

   ![Gruppo di disponibilità in Gestione cluster di failover](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="16e28-341">Non tentare toofail su hello gruppo di disponibilità da hello gestione Cluster di Failover.</span><span class="sxs-lookup"><span data-stu-id="16e28-341">Do not try toofail over hello Availability Group from hello Failover Cluster Manager.</span></span> <span data-ttu-id="16e28-342">È consigliabile eseguire tutte le operazioni di failover nel **Dashboard AlwaysOn** in SSMS.</span><span class="sxs-lookup"><span data-stu-id="16e28-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="16e28-343">Per ulteriori informazioni, vedere [le restrizioni sull'utilizzo hello gestione Cluster di Failover con gruppi di disponibilità](https://msdn.microsoft.com/library/ff929171.aspx).</span><span class="sxs-lookup"><span data-stu-id="16e28-343">For more information, see [Restrictions on Using hello Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="16e28-344">A questo punto, è presente un gruppo di disponibilità con repliche in due istanze di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="16e28-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="16e28-345">È possibile spostare hello gruppo di disponibilità tra istanze.</span><span class="sxs-lookup"><span data-stu-id="16e28-345">You can move hello Availability Group between instances.</span></span> <span data-ttu-id="16e28-346">Non si dispone di un listener non è possibile connettersi ancora toohello gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="16e28-346">You cannot connect toohello Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="16e28-347">In macchine virtuali di Azure, il listener hello richiede un bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="16e28-347">In Azure virtual machines, hello listener requires a load balancer.</span></span> <span data-ttu-id="16e28-348">passaggio successivo Hello è bilanciamento del carico di hello toocreate in Azure.</span><span class="sxs-lookup"><span data-stu-id="16e28-348">hello next step is toocreate hello load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="16e28-349">Creare un servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="16e28-349">Create an Azure load balancer</span></span>

<span data-ttu-id="16e28-350">Nelle macchine virtuali di Azure un gruppo di disponibilità SQL Server richiede un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="16e28-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="16e28-351">servizio di bilanciamento del carico Hello contiene l'indirizzo IP hello per listener del gruppo di disponibilità di hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-351">hello load balancer holds hello IP address for hello Availability Group listener.</span></span> <span data-ttu-id="16e28-352">Questa sezione vengono riepilogati come hello toocreate bilanciamento del carico in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="16e28-352">This section summarizes how toocreate hello load balancer in hello Azure portal.</span></span>

1. <span data-ttu-id="16e28-353">Nel portale di Azure hello, passare toohello gruppo di risorse in cui i computer SQL Server e fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="16e28-353">In hello Azure portal, go toohello resource group where your SQL Servers are and click **+ Add**.</span></span>
2. <span data-ttu-id="16e28-354">Cercare **Servizio di bilanciamento del carico**.</span><span class="sxs-lookup"><span data-stu-id="16e28-354">Search for **Load Balancer**.</span></span> <span data-ttu-id="16e28-355">Scegliere di bilanciamento del carico hello pubblicato da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="16e28-355">Choose hello load balancer published by Microsoft.</span></span>

   ![Gruppo di disponibilità in Gestione cluster di failover](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  <span data-ttu-id="16e28-357">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="16e28-357">Click **Create**.</span></span>
3. <span data-ttu-id="16e28-358">Configurare i seguenti parametri di bilanciamento del carico hello hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-358">Configure hello following parameters for hello load balancer.</span></span>

   | <span data-ttu-id="16e28-359">Impostazione</span><span class="sxs-lookup"><span data-stu-id="16e28-359">Setting</span></span> | <span data-ttu-id="16e28-360">Campo</span><span class="sxs-lookup"><span data-stu-id="16e28-360">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="16e28-361">**Nome**</span><span class="sxs-lookup"><span data-stu-id="16e28-361">**Name**</span></span> |<span data-ttu-id="16e28-362">Utilizzare un nome di bilanciamento del carico hello, ad esempio **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="16e28-362">Use a text name for hello load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="16e28-363">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="16e28-363">**Type**</span></span> |<span data-ttu-id="16e28-364">Interno</span><span class="sxs-lookup"><span data-stu-id="16e28-364">Internal</span></span> |
   | <span data-ttu-id="16e28-365">**Rete virtuale**</span><span class="sxs-lookup"><span data-stu-id="16e28-365">**Virtual network**</span></span> |<span data-ttu-id="16e28-366">Utilizzare il nome di hello di hello rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="16e28-366">Use hello name of hello Azure virtual network.</span></span> |
   | <span data-ttu-id="16e28-367">**Subnet**</span><span class="sxs-lookup"><span data-stu-id="16e28-367">**Subnet**</span></span> |<span data-ttu-id="16e28-368">Utilizza il nome di hello di subnet hello hello macchina virtuale è in.</span><span class="sxs-lookup"><span data-stu-id="16e28-368">Use hello name of hello subnet that hello virtual machine is in.</span></span>  |
   | <span data-ttu-id="16e28-369">**Assegnazione indirizzi IP**</span><span class="sxs-lookup"><span data-stu-id="16e28-369">**IP address assignment**</span></span> |<span data-ttu-id="16e28-370">Static</span><span class="sxs-lookup"><span data-stu-id="16e28-370">Static</span></span> |
   | <span data-ttu-id="16e28-371">**Indirizzo IP**</span><span class="sxs-lookup"><span data-stu-id="16e28-371">**IP address**</span></span> |<span data-ttu-id="16e28-372">Usare un indirizzo disponibile nella subnet.</span><span class="sxs-lookup"><span data-stu-id="16e28-372">Use an available address from subnet.</span></span> |
   | <span data-ttu-id="16e28-373">**Sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="16e28-373">**Subscription**</span></span> |<span data-ttu-id="16e28-374">Utilizzare hello stessa sottoscrizione come macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-374">Use hello same subscription as hello virtual machine.</span></span> |
   | <span data-ttu-id="16e28-375">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="16e28-375">**Location**</span></span> |<span data-ttu-id="16e28-376">Utilizzare hello stesso percorso come macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-376">Use hello same location as hello virtual machine.</span></span> |

   <span data-ttu-id="16e28-377">portale di Azure-blade Hello dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="16e28-377">hello Azure portal blade should look like this:</span></span>

   ![Crea servizio di bilanciamento del carico](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="16e28-379">Fare clic su **crea**, servizio di bilanciamento del carico toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-379">Click **Create**, toocreate hello load balancer.</span></span>

<span data-ttu-id="16e28-380">servizio di bilanciamento del carico hello tooconfigure occorre toocreate un pool back-end, un probe e regole di bilanciamento del carico di set hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-380">tooconfigure hello load balancer, you need toocreate a backend pool, a probe, and set hello load balancing rules.</span></span> <span data-ttu-id="16e28-381">Eseguire le operazioni seguenti nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-381">Do these in hello Azure portal.</span></span>

### <a name="add-backend-pool"></a><span data-ttu-id="16e28-382">Aggiungere un pool back-end</span><span class="sxs-lookup"><span data-stu-id="16e28-382">Add backend pool</span></span>

1. <span data-ttu-id="16e28-383">Nel portale di Azure hello, passare tooyour gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="16e28-383">In hello Azure portal, go tooyour availability group.</span></span> <span data-ttu-id="16e28-384">Potrebbe essere necessario bilanciamento del carico di toorefresh hello vista toosee hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="16e28-384">You might need toorefresh hello view toosee hello newly created load balancer.</span></span>

   ![Trovare il servizio di bilanciamento del carico nel gruppo di risorse](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="16e28-386">Fare clic su servizio di bilanciamento del carico hello, fare clic su **pool back-end**, fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="16e28-386">Click hello load balancer, click **Backend pools**, and click **+Add**.</span></span> <span data-ttu-id="16e28-387">Impostare il pool di back-end hello come segue:</span><span class="sxs-lookup"><span data-stu-id="16e28-387">Set hello backend pool as follows:</span></span>

   | <span data-ttu-id="16e28-388">Impostazione</span><span class="sxs-lookup"><span data-stu-id="16e28-388">Setting</span></span> | <span data-ttu-id="16e28-389">Descrizione</span><span class="sxs-lookup"><span data-stu-id="16e28-389">Description</span></span> | <span data-ttu-id="16e28-390">Esempio</span><span class="sxs-lookup"><span data-stu-id="16e28-390">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="16e28-391">**Nome**</span><span class="sxs-lookup"><span data-stu-id="16e28-391">**Name**</span></span> | <span data-ttu-id="16e28-392">Digitare un nome in formato testo</span><span class="sxs-lookup"><span data-stu-id="16e28-392">Type a text name</span></span> | <span data-ttu-id="16e28-393">SQLLBBE</span><span class="sxs-lookup"><span data-stu-id="16e28-393">SQLLBBE</span></span>
   | <span data-ttu-id="16e28-394">**Associato a**</span><span class="sxs-lookup"><span data-stu-id="16e28-394">**Associated to**</span></span> | <span data-ttu-id="16e28-395">Selezionare dall'elenco</span><span class="sxs-lookup"><span data-stu-id="16e28-395">Pick from list</span></span> | <span data-ttu-id="16e28-396">Set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="16e28-396">Availability set</span></span>
   | <span data-ttu-id="16e28-397">**Set di disponibilità**</span><span class="sxs-lookup"><span data-stu-id="16e28-397">**Availability set**</span></span> | <span data-ttu-id="16e28-398">Utilizzare un nome del gruppo di disponibilità hello che si trovano le macchine virtuali di SQL Server in</span><span class="sxs-lookup"><span data-stu-id="16e28-398">Use a name of hello availability set that your SQL Server VMs are in</span></span> | <span data-ttu-id="16e28-399">sqlAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="16e28-399">sqlAvailabilitySet</span></span> |
   | <span data-ttu-id="16e28-400">**Macchine virtuali**</span><span class="sxs-lookup"><span data-stu-id="16e28-400">**Virtual machines**</span></span> |<span data-ttu-id="16e28-401">Hello due nomi di macchina virtuale di Azure SQL Server</span><span class="sxs-lookup"><span data-stu-id="16e28-401">hello two Azure SQL Server VM names</span></span> | <span data-ttu-id="16e28-402">sqlserver-0, sqlserver-1</span><span class="sxs-lookup"><span data-stu-id="16e28-402">sqlserver-0, sqlserver-1</span></span>

1. <span data-ttu-id="16e28-403">Digitare il nome di hello per pool back-end hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-403">Type hello name for hello back end pool.</span></span>

1. <span data-ttu-id="16e28-404">Fare clic su **+ Aggiungi una macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="16e28-404">Click **+ Add a virtual machine**.</span></span>

1. <span data-ttu-id="16e28-405">Per i set di disponibilità hello, scegliere disponibilità hello impostare tale hello presenti istanze di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="16e28-405">For hello availability set, choose hello availability set that hello SQL Servers are in.</span></span>

1. <span data-ttu-id="16e28-406">Per le macchine virtuali, inclusi sia di hello istanze di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="16e28-406">For virtual machines, include both of hello SQL Servers.</span></span> <span data-ttu-id="16e28-407">Non includere server di controllo di condivisione file hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-407">Do not include hello file share witness server.</span></span>

1. <span data-ttu-id="16e28-408">Fare clic su **OK** pool back-end di toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-408">Click **OK** toocreate hello backend pool.</span></span>

### <a name="set-hello-probe"></a><span data-ttu-id="16e28-409">Set hello probe</span><span class="sxs-lookup"><span data-stu-id="16e28-409">Set hello probe</span></span>

1. <span data-ttu-id="16e28-410">Fare clic su servizio di bilanciamento del carico hello, fare clic su **probe di integrità**, fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="16e28-410">Click hello load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="16e28-411">Impostare i probe di integrità hello come segue:</span><span class="sxs-lookup"><span data-stu-id="16e28-411">Set hello health probe as follows:</span></span>

   | <span data-ttu-id="16e28-412">Impostazione</span><span class="sxs-lookup"><span data-stu-id="16e28-412">Setting</span></span> | <span data-ttu-id="16e28-413">Descrizione</span><span class="sxs-lookup"><span data-stu-id="16e28-413">Description</span></span> | <span data-ttu-id="16e28-414">Esempio</span><span class="sxs-lookup"><span data-stu-id="16e28-414">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="16e28-415">**Nome**</span><span class="sxs-lookup"><span data-stu-id="16e28-415">**Name**</span></span> | <span data-ttu-id="16e28-416">Text</span><span class="sxs-lookup"><span data-stu-id="16e28-416">Text</span></span> | <span data-ttu-id="16e28-417">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="16e28-417">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="16e28-418">**Protocollo**</span><span class="sxs-lookup"><span data-stu-id="16e28-418">**Protocol**</span></span> | <span data-ttu-id="16e28-419">Scegliere TCP</span><span class="sxs-lookup"><span data-stu-id="16e28-419">Choose TCP</span></span> | <span data-ttu-id="16e28-420">TCP</span><span class="sxs-lookup"><span data-stu-id="16e28-420">TCP</span></span> |
   | <span data-ttu-id="16e28-421">**Porta**</span><span class="sxs-lookup"><span data-stu-id="16e28-421">**Port**</span></span> | <span data-ttu-id="16e28-422">Qualsiasi porta non usata</span><span class="sxs-lookup"><span data-stu-id="16e28-422">Any unused port</span></span> | <span data-ttu-id="16e28-423">59999</span><span class="sxs-lookup"><span data-stu-id="16e28-423">59999</span></span> |
   | <span data-ttu-id="16e28-424">**Interval**</span><span class="sxs-lookup"><span data-stu-id="16e28-424">**Interval**</span></span>  | <span data-ttu-id="16e28-425">Hello tempo tra probe tentativi espresso in secondi</span><span class="sxs-lookup"><span data-stu-id="16e28-425">hello amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="16e28-426">5</span><span class="sxs-lookup"><span data-stu-id="16e28-426">5</span></span> |
   | <span data-ttu-id="16e28-427">**Soglia non integra**</span><span class="sxs-lookup"><span data-stu-id="16e28-427">**Unhealthy threshold**</span></span> | <span data-ttu-id="16e28-428">numero di errori di probe consecutivi che devono verificarsi per una macchina virtuale di toobe considerato non integro Hello</span><span class="sxs-lookup"><span data-stu-id="16e28-428">hello number of consecutive probe failures that must occur for a virtual machine toobe considered unhealthy</span></span>  | <span data-ttu-id="16e28-429">2</span><span class="sxs-lookup"><span data-stu-id="16e28-429">2</span></span> |

1. <span data-ttu-id="16e28-430">Fare clic su **OK** tooset probe di integrità hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-430">Click **OK** tooset hello health probe.</span></span>

### <a name="set-hello-load-balancing-rules"></a><span data-ttu-id="16e28-431">Impostare regole di bilanciamento del carico di hello</span><span class="sxs-lookup"><span data-stu-id="16e28-431">Set hello load balancing rules</span></span>

1. <span data-ttu-id="16e28-432">Fare clic su servizio di bilanciamento del carico hello, fare clic su **regole di bilanciamento del carico**, fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="16e28-432">Click hello load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="16e28-433">Impostare hello bilanciamento del carico regole come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="16e28-433">Set hello load balancing rules as follows.</span></span>
   | <span data-ttu-id="16e28-434">Impostazione</span><span class="sxs-lookup"><span data-stu-id="16e28-434">Setting</span></span> | <span data-ttu-id="16e28-435">Descrizione</span><span class="sxs-lookup"><span data-stu-id="16e28-435">Description</span></span> | <span data-ttu-id="16e28-436">Esempio</span><span class="sxs-lookup"><span data-stu-id="16e28-436">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="16e28-437">**Nome**</span><span class="sxs-lookup"><span data-stu-id="16e28-437">**Name**</span></span> | <span data-ttu-id="16e28-438">Text</span><span class="sxs-lookup"><span data-stu-id="16e28-438">Text</span></span> | <span data-ttu-id="16e28-439">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="16e28-439">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="16e28-440">**Indirizzo IP front-end IP**</span><span class="sxs-lookup"><span data-stu-id="16e28-440">**Frontend IP address**</span></span> | <span data-ttu-id="16e28-441">Scegliere un indirizzo</span><span class="sxs-lookup"><span data-stu-id="16e28-441">Choose an address</span></span> |<span data-ttu-id="16e28-442">Usa indirizzo hello creato al momento della creazione del bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-442">Use hello address that you created when you created hello load balancer.</span></span> |
   | <span data-ttu-id="16e28-443">**Protocollo**</span><span class="sxs-lookup"><span data-stu-id="16e28-443">**Protocol**</span></span> | <span data-ttu-id="16e28-444">Scegliere TCP</span><span class="sxs-lookup"><span data-stu-id="16e28-444">Choose TCP</span></span> |<span data-ttu-id="16e28-445">TCP</span><span class="sxs-lookup"><span data-stu-id="16e28-445">TCP</span></span> |
   | <span data-ttu-id="16e28-446">**Porta**</span><span class="sxs-lookup"><span data-stu-id="16e28-446">**Port**</span></span> | <span data-ttu-id="16e28-447">Utilizzare la porta hello hello istanza di SQL Server</span><span class="sxs-lookup"><span data-stu-id="16e28-447">Use hello port for hello SQL Server instance</span></span> | <span data-ttu-id="16e28-448">1433</span><span class="sxs-lookup"><span data-stu-id="16e28-448">1433</span></span> |
   | <span data-ttu-id="16e28-449">**Porta back-end**</span><span class="sxs-lookup"><span data-stu-id="16e28-449">**Backend Port**</span></span> | <span data-ttu-id="16e28-450">Questo campo non viene usato quando l'indirizzo IP mobile è impostato per Direct Server Return</span><span class="sxs-lookup"><span data-stu-id="16e28-450">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="16e28-451">1433</span><span class="sxs-lookup"><span data-stu-id="16e28-451">1433</span></span> |
   | <span data-ttu-id="16e28-452">**Probe**</span><span class="sxs-lookup"><span data-stu-id="16e28-452">**Probe**</span></span> |<span data-ttu-id="16e28-453">nome Hello specificato per il probe hello</span><span class="sxs-lookup"><span data-stu-id="16e28-453">hello name you specified for hello probe</span></span> | <span data-ttu-id="16e28-454">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="16e28-454">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="16e28-455">**Persistenza della sessione**</span><span class="sxs-lookup"><span data-stu-id="16e28-455">**Session Persistence**</span></span> | <span data-ttu-id="16e28-456">Elenco a discesa</span><span class="sxs-lookup"><span data-stu-id="16e28-456">Drop down list</span></span> | <span data-ttu-id="16e28-457">**Nessuno**</span><span class="sxs-lookup"><span data-stu-id="16e28-457">**None**</span></span> |
   | <span data-ttu-id="16e28-458">**Timeout di inattività**</span><span class="sxs-lookup"><span data-stu-id="16e28-458">**Idle Timeout**</span></span> | <span data-ttu-id="16e28-459">Minuti tookeep aprire una connessione TCP</span><span class="sxs-lookup"><span data-stu-id="16e28-459">Minutes tookeep a TCP connection open</span></span> | <span data-ttu-id="16e28-460">4</span><span class="sxs-lookup"><span data-stu-id="16e28-460">4</span></span> |
   | <span data-ttu-id="16e28-461">**IP mobile (Direct Server Return)**</span><span class="sxs-lookup"><span data-stu-id="16e28-461">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="16e28-462">Enabled</span><span class="sxs-lookup"><span data-stu-id="16e28-462">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="16e28-463">Direct Server Return viene impostato durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="16e28-463">Direct server return is set during creation.</span></span> <span data-ttu-id="16e28-464">Non può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="16e28-464">It cannot be changed.</span></span>

1. <span data-ttu-id="16e28-465">Fare clic su **OK** tooset hello bilanciamento del carico regole.</span><span class="sxs-lookup"><span data-stu-id="16e28-465">Click **OK** tooset hello load balancing rules.</span></span>

## <span data-ttu-id="16e28-466"><a name="configure-listener"></a>Configurare il listener hello</span><span class="sxs-lookup"><span data-stu-id="16e28-466"><a name="configure-listener"></a> Configure hello listener</span></span>

<span data-ttu-id="16e28-467">Hello Avanti cosa toodo è tooconfigure un listener del gruppo di disponibilità nel cluster di failover hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-467">hello next thing toodo is tooconfigure an Availability Group listener on hello failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="16e28-468">Questa esercitazione viene illustrato come un listener single - con un IP ILB toocreate indirizzo.</span><span class="sxs-lookup"><span data-stu-id="16e28-468">This tutorial shows how toocreate a single listener - with one ILB IP address.</span></span> <span data-ttu-id="16e28-469">toocreate uno o più listener utilizzando uno o più indirizzi IP, vedere [listener Crea gruppo di disponibilità e bilanciamento del carico | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="16e28-469">toocreate one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="16e28-470">Impostare la porta del listener</span><span class="sxs-lookup"><span data-stu-id="16e28-470">Set listener port</span></span>

<span data-ttu-id="16e28-471">In SQL Server Management Studio, impostare la porta di attesa hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-471">In SQL Server Management Studio, set hello listener port.</span></span>

1. <span data-ttu-id="16e28-472">Avviare SQL Server Management Studio e connettersi toohello la replica primaria.</span><span class="sxs-lookup"><span data-stu-id="16e28-472">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="16e28-473">Passare troppo**disponibilità elevata AlwaysOn** | **gruppi di disponibilità** | **listener del gruppo di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="16e28-473">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="16e28-474">Viene visualizzato il nome del listener hello creati in Gestione Cluster di Failover.</span><span class="sxs-lookup"><span data-stu-id="16e28-474">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="16e28-475">Il nome del listener hello destro e fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="16e28-475">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="16e28-476">In hello **porta** , specificare il numero di porta hello del listener del gruppo di disponibilità hello utilizzando hello $EndpointPort utilizzato in precedenza (1433 è predefinito hello), quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="16e28-476">In hello **Port** box, specify hello port number for hello Availability Group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

<span data-ttu-id="16e28-477">Ora si ha un gruppo di disponibilità di SQL Server nelle macchine virtuali di Azure in esecuzione in modalità Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="16e28-477">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-toolistener"></a><span data-ttu-id="16e28-478">Test connessione toolistener</span><span class="sxs-lookup"><span data-stu-id="16e28-478">Test connection toolistener</span></span>

<span data-ttu-id="16e28-479">connessione hello tootest:</span><span class="sxs-lookup"><span data-stu-id="16e28-479">tootest hello connection:</span></span>

1. <span data-ttu-id="16e28-480">RDP tooa SQL Server in hello stesso virtuale di rete, ma non non replica hello personalizzati.</span><span class="sxs-lookup"><span data-stu-id="16e28-480">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="16e28-481">È possibile utilizzare altri Server SQL cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-481">You can use hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="16e28-482">Utilizzare **sqlcmd** connessione hello tootest di utilità.</span><span class="sxs-lookup"><span data-stu-id="16e28-482">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="16e28-483">Ad esempio, lo script seguente hello stabilisce un **sqlcmd** replica primaria toohello di connessione tramite il listener hello con l'autenticazione di Windows:</span><span class="sxs-lookup"><span data-stu-id="16e28-483">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>

    ```
    sqlcmd -S <listenerName> -E
    ```

    <span data-ttu-id="16e28-484">Se il listener di hello utilizza una porta diversa da hello predefinita (1433) di porta, specificare la porta hello nella stringa di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="16e28-484">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="16e28-485">Ad esempio, hello comando sqlcmd riportato di seguito si connette tooa listener a porta 1435:</span><span class="sxs-lookup"><span data-stu-id="16e28-485">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span>

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="16e28-486">connessione SQLCMD Hello si connette automaticamente toowhichever istanza di SQL Server ospitata hello la replica primaria.</span><span class="sxs-lookup"><span data-stu-id="16e28-486">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="16e28-487">Assicurarsi che sia aperta nel firewall hello di entrambi i server SQL porta hello specificata.</span><span class="sxs-lookup"><span data-stu-id="16e28-487">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="16e28-488">Entrambi i server richiedono una regola in ingresso per hello la porta TCP in uso.</span><span class="sxs-lookup"><span data-stu-id="16e28-488">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="16e28-489">Per altre informazioni, vedere [Aggiungere o modificare una regola del firewall](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="16e28-489">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a><span data-ttu-id="16e28-490">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="16e28-490">Next steps</span></span>

- <span data-ttu-id="16e28-491">[Aggiungere un bilanciamento del carico IP indirizzo tooa per un gruppo di disponibilità secondo](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span><span class="sxs-lookup"><span data-stu-id="16e28-491">[Add an IP address tooa load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>
