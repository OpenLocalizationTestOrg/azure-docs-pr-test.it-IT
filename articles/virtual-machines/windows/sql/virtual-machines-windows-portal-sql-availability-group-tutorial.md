---
title: "Gruppi di disponibilità di SQL Server: Macchine virtuali di Azure: esercitazione | Microsoft Docs"
description: "Questa esercitazione illustra come creare un gruppo di disponibilità SQL Server AlwaysOn in Macchine virtuali di Azure."
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
ms.openlocfilehash: 228ca9ca5fddc493d27bfd6a40df5ee7306d6aa9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="2fa4d-103">Configurare manualmente un gruppo di disponibilità AlwaysOn in VM di Azure</span><span class="sxs-lookup"><span data-stu-id="2fa4d-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="2fa4d-104">Questa esercitazione illustra come creare un gruppo di disponibilità SQL Server AlwaysOn in Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-104">This tutorial shows how to create a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="2fa4d-105">L'esercitazione completa crea un gruppo di disponibilità con una replica di database in due istanze di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-105">The complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="2fa4d-106">**Tempo stimato**: per completare l'esercitazione, sono necessari circa 30 minuti dopo avere soddisfatto i prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-106">**Time estimate**: Takes about 30 minutes to complete once the prerequisites are met.</span></span>

<span data-ttu-id="2fa4d-107">Il diagramma illustra le operazioni di compilazione nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-107">The diagram illustrates what you build in the tutorial.</span></span>

![Gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="2fa4d-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2fa4d-109">Prerequisites</span></span>

<span data-ttu-id="2fa4d-110">Nell'esercitazione si presuppone una conoscenza di base dei gruppi di disponibilità di SQL Server AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-110">The tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="2fa4d-111">Se sono necessarie altre informazioni, vedere [Panoramica di Gruppi di disponibilità AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span><span class="sxs-lookup"><span data-stu-id="2fa4d-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="2fa4d-112">La tabella seguente elenca i prerequisiti da completare prima di iniziare l'esercitazione:</span><span class="sxs-lookup"><span data-stu-id="2fa4d-112">The following table lists the prerequisites that you need to complete before starting this tutorial:</span></span>

|  |<span data-ttu-id="2fa4d-113">Requisito</span><span class="sxs-lookup"><span data-stu-id="2fa4d-113">Requirement</span></span> |<span data-ttu-id="2fa4d-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2fa4d-114">Description</span></span> |
|----- |----- |----- |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="2fa4d-116">Due istanze di SQL Server</span><span class="sxs-lookup"><span data-stu-id="2fa4d-116">Two SQL Servers</span></span> | <span data-ttu-id="2fa4d-117">- In un set di disponibilità di Azure</span><span class="sxs-lookup"><span data-stu-id="2fa4d-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="2fa4d-118">- In un dominio singolo</span><span class="sxs-lookup"><span data-stu-id="2fa4d-118">- In a single domain</span></span> <br/> <span data-ttu-id="2fa4d-119">- Con la funzionalità Clustering di failover installata</span><span class="sxs-lookup"><span data-stu-id="2fa4d-119">- With Failover Clustering feature installed</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="2fa4d-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="2fa4d-121">Windows Server</span></span> | <span data-ttu-id="2fa4d-122">Controllo di condivisione file per il cluster</span><span class="sxs-lookup"><span data-stu-id="2fa4d-122">File share for cluster witness</span></span> |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="2fa4d-124">Account del servizio SQL Server</span><span class="sxs-lookup"><span data-stu-id="2fa4d-124">SQL Server service account</span></span> | <span data-ttu-id="2fa4d-125">Account di dominio</span><span class="sxs-lookup"><span data-stu-id="2fa4d-125">Domain account</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="2fa4d-127">Account del servizio SQL Server Agent</span><span class="sxs-lookup"><span data-stu-id="2fa4d-127">SQL Server Agent service account</span></span> | <span data-ttu-id="2fa4d-128">Account di dominio</span><span class="sxs-lookup"><span data-stu-id="2fa4d-128">Domain account</span></span> |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="2fa4d-130">Porte del firewall aperte</span><span class="sxs-lookup"><span data-stu-id="2fa4d-130">Firewall ports open</span></span> | <span data-ttu-id="2fa4d-131">- SQL Server: **1433** per l'istanza predefinita</span><span class="sxs-lookup"><span data-stu-id="2fa4d-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="2fa4d-132">- Endpoint del mirroring del database: **5022** o qualsiasi porta disponibile</span><span class="sxs-lookup"><span data-stu-id="2fa4d-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="2fa4d-133">- Probe di bilanciamento del carico di Azure: **59999** o qualsiasi porta disponibile</span><span class="sxs-lookup"><span data-stu-id="2fa4d-133">- Azure load balancer probe: **59999** or any available port</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="2fa4d-135">Aggiunta della funzionalità Clustering di failover</span><span class="sxs-lookup"><span data-stu-id="2fa4d-135">Add Failover Clustering Feature</span></span> | <span data-ttu-id="2fa4d-136">Questa funzionalità è necessaria per entrambe le istanze di SQL Server</span><span class="sxs-lookup"><span data-stu-id="2fa4d-136">Both SQL Servers require this feature</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="2fa4d-138">Account di dominio dell'installazione</span><span class="sxs-lookup"><span data-stu-id="2fa4d-138">Installation domain account</span></span> | <span data-ttu-id="2fa4d-139">- Amministratore locale in ogni istanza di SQL Server</span><span class="sxs-lookup"><span data-stu-id="2fa4d-139">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="2fa4d-140">- Membro del ruolo predefinito del server sysadmin di SQL Server per ogni istanza di SQL Server</span><span class="sxs-lookup"><span data-stu-id="2fa4d-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="2fa4d-141">Prima di iniziare l'esercitazione, è necessario [completare i prerequisiti per la creazione di gruppi di disponibilità AlwaysOn in Macchine virtuali di Azure](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span><span class="sxs-lookup"><span data-stu-id="2fa4d-141">Before you begin the tutorial, you need to [Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="2fa4d-142">Se questi prerequisiti sono già stati completati, è possibile passare a [Creare il cluster](#CreateCluster).</span><span class="sxs-lookup"><span data-stu-id="2fa4d-142">If these prerequisites are completed already, you can jump to [Create Cluster](#CreateCluster).</span></span>


<span data-ttu-id="2fa4d-143"><!--**Procedure**: *This is the first “step”. Make titles H2’s and short and clear – H2’s appear in the right pane on the web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Creare il cluster</span><span class="sxs-lookup"><span data-stu-id="2fa4d-143"><!--**Procedure**: *This is the first “step”. Make titles H2’s and short and clear – H2’s appear in the right pane on the web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## Create the cluster</span></span>

<span data-ttu-id="2fa4d-144">Dopo avere completato i prerequisiti, il primo passaggio prevede la creazione di un cluster di failover Windows Server con due istanze di SQL Server e un server di controllo.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-144">After the prerequisites are completed, the first step is to create a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>  

1. <span data-ttu-id="2fa4d-145">Stabilire una connessione RDP alla prima istanza di SQL Server usando un account di dominio che sia amministratore in entrambe le istanze di SQL Server e nel server di controllo.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-145">RDP to the first SQL Server using a domain account that is an administrator on both SQL Servers and the witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="2fa4d-146">Se si è seguito il [documento sui prerequisiti](virtual-machines-windows-portal-sql-availability-group-prereq.md), è stato creato un account denominato **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-146">If you followed the [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="2fa4d-147">Usare questo account.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-147">Use this account.</span></span>

2. <span data-ttu-id="2fa4d-148">Nel dashboard **Server Manager** selezionare **Strumenti** e quindi fare clic su **Gestione cluster di failover**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-148">In the **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="2fa4d-149">Nel riquadro sinistro fare clic con il pulsante destro del mouse su **Gestione cluster di failover** e quindi scegliere **Crea cluster**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-149">In the left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="2fa4d-150">![Creare un cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="2fa4d-150">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="2fa4d-151">Nella Creazione guidata Cluster creare un cluster a un nodo procedendo nelle pagine con le impostazioni della tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="2fa4d-151">In the Create Cluster Wizard, create a one-node cluster by stepping through the pages with the settings in the following table:</span></span>

   | <span data-ttu-id="2fa4d-152">Page</span><span class="sxs-lookup"><span data-stu-id="2fa4d-152">Page</span></span> | <span data-ttu-id="2fa4d-153">Impostazioni</span><span class="sxs-lookup"><span data-stu-id="2fa4d-153">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="2fa4d-154">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="2fa4d-154">Before You Begin</span></span> |<span data-ttu-id="2fa4d-155">Valori predefiniti</span><span class="sxs-lookup"><span data-stu-id="2fa4d-155">Use defaults</span></span> |
   | <span data-ttu-id="2fa4d-156">Selezione dei server</span><span class="sxs-lookup"><span data-stu-id="2fa4d-156">Select Servers</span></span> |<span data-ttu-id="2fa4d-157">Digitare il nome della prima istanza di SQL Server in **Immettere il nome del server** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-157">Type the first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="2fa4d-158">Avviso di convalida</span><span class="sxs-lookup"><span data-stu-id="2fa4d-158">Validation Warning</span></span> |<span data-ttu-id="2fa4d-159">Selezionare **No. Non è necessario il supporto di Microsoft per il cluster e pertanto non desidero eseguire i test di convalida. Facendo clic su Avanti, si proseguirà con la creazione del cluster**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want to run the validation tests. When I click Next, continue Creating the cluster**.</span></span> |
   | <span data-ttu-id="2fa4d-160">Punto di accesso per l'amministrazione del cluster</span><span class="sxs-lookup"><span data-stu-id="2fa4d-160">Access Point for Administering the Cluster</span></span> |<span data-ttu-id="2fa4d-161">Digitare un nome di cluster, ad esempio **SQLAGCluster1**, in **Nome cluster**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="2fa4d-162">Conferma</span><span class="sxs-lookup"><span data-stu-id="2fa4d-162">Confirmation</span></span> |<span data-ttu-id="2fa4d-163">Usare le impostazioni predefinite a meno a meno che non si usino spazi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-163">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="2fa4d-164">Vedere la nota che segue questa tabella.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-164">See the note following this table.</span></span> |

### <a name="set-the-cluster-ip-address"></a><span data-ttu-id="2fa4d-165">Impostare l'indirizzo IP del cluster</span><span class="sxs-lookup"><span data-stu-id="2fa4d-165">Set the cluster IP address</span></span>

1. <span data-ttu-id="2fa4d-166">In **Gestione cluster di failover** scorrere verso il basso fino a **Risorse principali del cluster** ed espandere i dettagli del cluster.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-166">In **Failover Cluster Manager**, scroll down to **Cluster Core Resources** and expand the cluster details.</span></span> <span data-ttu-id="2fa4d-167">Lo stato visualizzato di entrambe le risorse **Nome** e **Indirizzo IP** deve essere **Operazione non riuscita**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-167">You should see both the **Name** and the **IP Address** resources in the **Failed** state.</span></span> <span data-ttu-id="2fa4d-168">La risorsa indirizzo IP non può essere portata online perché al cluster è assegnato lo stesso indirizzo IP del computer, quindi si tratta di un indirizzo duplicato.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-168">The IP address resource cannot be brought online because the cluster is assigned the same IP address as the machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="2fa4d-169">Fare clic con il pulsante destro del mouse sulla risorsa **Indirizzo IP** non riuscita, quindi scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-169">Right-click the failed **IP Address** resource, and then click **Properties**.</span></span>

   ![Proprietà del cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="2fa4d-171">Selezionare **Indirizzo IP statico** e nella casella di testo Indirizzo specificare un indirizzo disponibile dalla subnet in cui si trova l'istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-171">Select **Static IP Address** and specify an available address from subnet where the SQL Server is in the Address text box.</span></span> <span data-ttu-id="2fa4d-172">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-172">Then, click **OK**.</span></span>
4. <span data-ttu-id="2fa4d-173">Nella sezione **Risorse principali del cluster** fare clic con il pulsante destro del mouse sul nome del cluster e scegliere **Porta online**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-173">In the **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="2fa4d-174">Attendere finché entrambe le risorse non sono online</span><span class="sxs-lookup"><span data-stu-id="2fa4d-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="2fa4d-175">Quando la risorsa del nome cluster torna online, il server del controller di dominio viene aggiornato con un nuovo account del computer Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-175">When the cluster name resource comes online, it updates the DC server with a new AD computer account.</span></span> <span data-ttu-id="2fa4d-176">Usare l'account Active Directory per eseguire il servizio del cluster del gruppo di disponibilità in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-176">Use this AD account to run the Availability Group clustered service later.</span></span>

### <span data-ttu-id="2fa4d-177"><a name="addNode"></a>Aggiungere l'altra istanza di SQL Server al cluster</span><span class="sxs-lookup"><span data-stu-id="2fa4d-177"><a name="addNode"></a>Add the other SQL Server to cluster</span></span>

<span data-ttu-id="2fa4d-178">Aggiungere l'altra istanza di SQL Server al cluster.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-178">Add the other SQL Server to the cluster.</span></span>

1. <span data-ttu-id="2fa4d-179">Nell'albero del browser fare clic con il pulsante destro del mouse sul cluster e scegliere **Aggiungi nodo**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-179">In the browser tree, right-click the cluster and click **Add Node**.</span></span>

    ![Aggiungere un nodo al cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="2fa4d-181">In **Aggiunta guidata nodi** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-181">In the **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="2fa4d-182">Nella pagina **Seleziona server** aggiungere la seconda istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-182">In the **Select Servers** page, add the second SQL Server.</span></span> <span data-ttu-id="2fa4d-183">Digitare il nome del server in **Immettere il nome del server** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-183">Type the server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="2fa4d-184">Al termine dell'operazione, scegliere **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="2fa4d-185">Nella pagina **Avviso di convalida** fare clic su **No**. In uno scenario di produzione è necessario eseguire i test di convalida.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-185">In the **Validation Warning** page, click **No** (in a production scenario you should perform the validation tests).</span></span> <span data-ttu-id="2fa4d-186">Quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="2fa4d-187">Nella pagina **Conferma**, se si usa la funzionalità Spazi di archiviazione, deselezionare la casella di controllo **Aggiungi tutte le risorse di archiviazione idonee al cluster**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-187">In the **Confirmation** page if you are using Storage Spaces, clear the checkbox labeled **Add all eligible storage to the cluster.**</span></span>

   ![Confermare l'aggiunta del nodo](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="2fa4d-189">Se si usa Spazi di archiviazione e non si deseleziona **Aggiungi tutte le risorse di archiviazione idonee al cluster**, Windows rende non visibili i dischi virtuali durante il processo di clustering.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage to the cluster**, Windows detaches the virtual disks during the clustering process.</span></span> <span data-ttu-id="2fa4d-190">Di conseguenza, tali dischi non vengono visualizzati in Gestione disco o in Esplora risorse fino a quando gli spazi di archiviazione non vengono rimossi dal cluster e ricollegati usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-190">As a result, they do not appear in Disk Manager or Explorer until the storage spaces are removed from the cluster and reattached using PowerShell.</span></span> <span data-ttu-id="2fa4d-191">Spazi di archiviazione consente di raggruppare più dischi in pool di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-191">Storage Spaces groups multiple disks in to storage pools.</span></span> <span data-ttu-id="2fa4d-192">Per altre informazioni, vedere [Spazi di archiviazione](https://technet.microsoft.com/library/hh831739).</span><span class="sxs-lookup"><span data-stu-id="2fa4d-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="2fa4d-193">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-193">Click **Next**.</span></span>

1. <span data-ttu-id="2fa4d-194">Fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-194">Click **Finish**.</span></span>

   <span data-ttu-id="2fa4d-195">A questo punto, Gestione cluster di failover visualizza il cluster con un nuovo nodo elencato nel contenitore **Nodi**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-195">Failover Cluster Manager shows that your cluster has a new node and lists it in the **Nodes** container.</span></span>

10. <span data-ttu-id="2fa4d-196">Disconnettersi dalla sessione desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-196">Log out of the remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="2fa4d-197">Aggiungere una condivisione file di quorum del cluster</span><span class="sxs-lookup"><span data-stu-id="2fa4d-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="2fa4d-198">In questo esempio il cluster Windows usa una condivisione file per creare un quorum del cluster.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-198">In this example the Windows cluster uses a file share to create a cluster quorum.</span></span> <span data-ttu-id="2fa4d-199">Questa esercitazione usa un quorum Maggioranza dei nodi e delle condivisioni file.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="2fa4d-200">Per altre informazioni, vedere [Informazioni sulle configurazioni quorum in un cluster di failover](http://technet.microsoft.com/library/cc731739.aspx).</span><span class="sxs-lookup"><span data-stu-id="2fa4d-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="2fa4d-201">Connettersi al server membro di controllo della condivisione file con una sessione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-201">Connect to the file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="2fa4d-202">In **Server Manager** fare clic su **Strumenti**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="2fa4d-203">Aprire **Gestione computer**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="2fa4d-204">Fare clic su **Cartelle condivise**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="2fa4d-205">Fare clic con il pulsante destro del mouse su **Condivisioni** e scegliere **Nuova condivisione**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Nuova condivisione](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="2fa4d-207">Usare **Creazione guidata cartella condivisa** per creare una condivisione.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-207">Use **Create a Shared Folder Wizard** to create a share.</span></span>

1. <span data-ttu-id="2fa4d-208">In **Percorso cartella** fare clic su **Sfoglia** e individuare o creare un percorso per la cartella condivisa.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-208">On **Folder Path**, click **Browse** and locate or create a path for the shared folder.</span></span> <span data-ttu-id="2fa4d-209">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-209">Click **Next**.</span></span>

1. <span data-ttu-id="2fa4d-210">In **Nome, descrizione e impostazioni** verificare il nome e il percorso della condivisione.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-210">In **Name, Description, and Settings** verify the share name and path.</span></span> <span data-ttu-id="2fa4d-211">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-211">Click **Next**.</span></span>

1. <span data-ttu-id="2fa4d-212">In **Autorizzazioni cartella condivisa** impostare **Personalizza autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="2fa4d-213">Fare clic su **Personalizza**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="2fa4d-214">In **Personalizza autorizzazioni** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="2fa4d-215">Verificare che l'account usato per creare il cluster abbia il controllo completo.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-215">Make sure that the account used to create the cluster has full control.</span></span>

   ![Nuova condivisione](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="2fa4d-217">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-217">Click **OK**.</span></span>

1. <span data-ttu-id="2fa4d-218">In **Autorizzazioni cartella condivisa** fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="2fa4d-219">Fare di nuovo clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="2fa4d-220">Disconnettersi dal server</span><span class="sxs-lookup"><span data-stu-id="2fa4d-220">Log out of the server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="2fa4d-221">Configurare il quorum del cluster</span><span class="sxs-lookup"><span data-stu-id="2fa4d-221">Configure cluster quorum</span></span>

<span data-ttu-id="2fa4d-222">Impostare ora il quorum del cluster.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-222">Next, set the cluster quorum.</span></span>

1. <span data-ttu-id="2fa4d-223">Connettersi al primo nodo del cluster con Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-223">Connect to the first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="2fa4d-224">In **Gestione cluster di failover** fare clic con il pulsante destro del mouse sul cluster, scegliere **Altre azioni** e fare clic su **Configura impostazioni quorum del cluster**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-224">In **Failover Cluster Manager**, right-click the cluster, point to **More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![Nuova condivisione](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="2fa4d-226">In **Configurazione guidata quorum del cluster** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="2fa4d-227">In **Selezione opzione configurazione quorum** scegliere **Seleziona il quorum di controllo** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-227">In **Select Quorum Configuration Option**, choose **Select the quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="2fa4d-228">In **Selezione quorum di controllo** fare clic su **Configura condivisione file di controllo**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="2fa4d-229">Windows Server 2016 supporta un cloud di controllo.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="2fa4d-230">Se si sceglie questo tipo di controllo, non è necessario un controllo di condivisione file.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="2fa4d-231">Per altre informazioni, vedere [Distribuire un cloud di controllo per un cluster di failover](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="2fa4d-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="2fa4d-232">Questa esercitazione usa un controllo di condivisione file, supportato dai sistemi operativi precedenti.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="2fa4d-233">In **Configurazione condivisione file di controllo** digitare il percorso per la condivisione creata.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-233">On **Configure File Share Witness**, type the path for the share you created.</span></span> <span data-ttu-id="2fa4d-234">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-234">Click **Next**.</span></span>

1. <span data-ttu-id="2fa4d-235">Verificare le impostazioni in **Conferma**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-235">Verify the settings on **Confirmation**.</span></span> <span data-ttu-id="2fa4d-236">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-236">Click **Next**.</span></span>

1. <span data-ttu-id="2fa4d-237">Fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-237">Click **Finish**.</span></span>

<span data-ttu-id="2fa4d-238">Le risorse principali del cluster vengono configurate con un controllo di condivisione file.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-238">The cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="2fa4d-239">Abilitare i gruppi di disponibilità</span><span class="sxs-lookup"><span data-stu-id="2fa4d-239">Enable Availability Groups</span></span>

<span data-ttu-id="2fa4d-240">Abilitare ora la funzionalità **Gruppi di disponibilità AlwaysOn**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-240">Next, enable the **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="2fa4d-241">Eseguire questi passaggi in entrambe le istanze di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="2fa4d-242">Dalla schermata **Start** avviare **Gestione configurazione SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-242">From the **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="2fa4d-243">Nella struttura del browser fare clic su **Servizi di SQL Server**, fare clic con il pulsante destro del mouse sul servizio **SQL Server (MSSQLSERVER)**, quindi scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-243">In the browser tree, click **SQL Server Services**, then right-click the **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="2fa4d-244">Fare clic sulla scheda **Disponibilità elevata AlwaysOn**, selezionare **Abilita gruppi di disponibilità AlwaysOn**, come segue:</span><span class="sxs-lookup"><span data-stu-id="2fa4d-244">Click the **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![Abilitare Gruppi di disponibilità AlwaysOn in Azure](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="2fa4d-246">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-246">Click **Apply**.</span></span> <span data-ttu-id="2fa4d-247">Fare clic su **OK** nella finestra di dialogo popup.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-247">Click **OK** in the pop-up dialog.</span></span>

5. <span data-ttu-id="2fa4d-248">Riavviare il servizio SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-248">Restart the SQL Server service.</span></span>

<span data-ttu-id="2fa4d-249">Ripetere questi passaggi per l'altra istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-249">Repeat these steps on the other SQL Server.</span></span>

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for the database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for the instance of SQL Server that is used to synchronize the database replicas in the Availability Groups on that instance.

On both SQL Servers, open the firewall for the TCP port for the database mirroring endpoint.

1. On the first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In the left pane, select **Inbound Rules**. On the right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For the port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In the **Action** page, keep **Allow the connection** selected and click **Next**.
6. In the **Profile** page, accept the default settings and click **Next**.
7. In the **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in the **Name** text box, then click **Finish**.

Repeat these steps on the second SQL Server.
-------------------------->

## <a name="create-a-database-on-the-first-sql-server"></a><span data-ttu-id="2fa4d-250">Creare un database nella prima istanza di SQL Server</span><span class="sxs-lookup"><span data-stu-id="2fa4d-250">Create a database on the first SQL Server</span></span>

1. <span data-ttu-id="2fa4d-251">Avviare il file RDP nella prima istanza di SQL Server con un account di dominio che sia membro del ruolo predefinito del server sysadmin.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-251">Launch the RDP file to the first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="2fa4d-252">Aprire SQL Server Management Studio e connettersi alla prima istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-252">Open SQL Server Management Studio and connect to the first SQL Server.</span></span>
7. <span data-ttu-id="2fa4d-253">In **Esplora oggetti** fare clic con il pulsante destro del mouse su **Database** e scegliere **Nuovo database**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="2fa4d-254">In **Nome database** digitare **MyDB1**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <span data-ttu-id="2fa4d-255"><a name="backupshare"></a> Creare una condivisione di backup</span><span class="sxs-lookup"><span data-stu-id="2fa4d-255"><a name="backupshare"></a> Create a backup share</span></span>

1. <span data-ttu-id="2fa4d-256">In **Server Manager** nella prima istanza di SQL Server fare clic su **Strumenti**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-256">On the first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="2fa4d-257">Aprire **Gestione computer**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="2fa4d-258">Fare clic su **Cartelle condivise**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="2fa4d-259">Fare clic con il pulsante destro del mouse su **Condivisioni** e scegliere **Nuova condivisione**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Nuova condivisione](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="2fa4d-261">Usare **Creazione guidata cartella condivisa** per creare una condivisione.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-261">Use **Create a Shared Folder Wizard** to create a share.</span></span>

1. <span data-ttu-id="2fa4d-262">In **Percorso cartella** fare clic su **Sfoglia** e individuare o creare un percorso per la cartella condivisa del backup del database.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-262">On **Folder Path**, click **Browse** and locate or create a path for the database backup shared folder.</span></span> <span data-ttu-id="2fa4d-263">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-263">Click **Next**.</span></span>

1. <span data-ttu-id="2fa4d-264">In **Nome, descrizione e impostazioni** verificare il nome e il percorso della condivisione.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-264">In **Name, Description, and Settings** verify the share name and path.</span></span> <span data-ttu-id="2fa4d-265">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-265">Click **Next**.</span></span>

1. <span data-ttu-id="2fa4d-266">In **Autorizzazioni cartella condivisa** impostare **Personalizza autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="2fa4d-267">Fare clic su **Personalizza**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="2fa4d-268">In **Personalizza autorizzazioni** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="2fa4d-269">Verificare che gli account del servizio SQL Server e SQL Server Agent per entrambi i server abbiano il controllo completo.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-269">Make sure that the SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![Nuova condivisione](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="2fa4d-271">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-271">Click **OK**.</span></span>

1. <span data-ttu-id="2fa4d-272">In **Autorizzazioni cartella condivisa** fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="2fa4d-273">Fare di nuovo clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-the-database"></a><span data-ttu-id="2fa4d-274">Eseguire un backup completo del database</span><span class="sxs-lookup"><span data-stu-id="2fa4d-274">Take a full backup of the database</span></span>

<span data-ttu-id="2fa4d-275">È necessario eseguire il backup del nuovo database per inizializzare la catena di log.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-275">You need to back up the new database to initialize the log chain.</span></span> <span data-ttu-id="2fa4d-276">Il nuovo database non può essere incluso in un gruppo di disponibilità se non se ne esegue un backup.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-276">If you do not take a backup of the new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="2fa4d-277">In **Esplora oggetti** fare clic con il pulsante destro del mouse sul database, scegliere **Attività** e fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-277">In **Object Explorer**, right-click the database, point to **Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="2fa4d-278">Fare clic su **OK** per eseguire un backup completo nel percorso di backup predefinito.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-278">Click **OK** to take a full backup to the default backup location.</span></span>

## <a name="create-the-availability-group"></a><span data-ttu-id="2fa4d-279">Creare il gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-279">Create the Availability Group</span></span>
<span data-ttu-id="2fa4d-280">A questo punto, è possibile procedere con la configurazione di un gruppo di disponibilità seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2fa4d-280">You are now ready to configure an Availability Group using the following steps:</span></span>

* <span data-ttu-id="2fa4d-281">Creare un database nella prima istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-281">Create a database on the first SQL Server.</span></span>
* <span data-ttu-id="2fa4d-282">Eseguire sia un backup completo, sia un backup del log delle transazioni del database.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-282">Take both a full backup and a transaction log backup of the database</span></span>
* <span data-ttu-id="2fa4d-283">Ripristinare i backup completi e del log nella seconda istanza di SQL Server con l'opzione **NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-283">Restore the full and log backups to the second SQL Server with the **NORECOVERY** option</span></span>
* <span data-ttu-id="2fa4d-284">Creare il gruppo di disponibilità (**AG1**) con commit sincrono, failover automatico e repliche secondarie leggibili.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-284">Create the Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-the-availability-group"></a><span data-ttu-id="2fa4d-285">Creare il gruppo di disponibilità:</span><span class="sxs-lookup"><span data-stu-id="2fa4d-285">Create the Availability Group:</span></span>

1. <span data-ttu-id="2fa4d-286">Nella sessione Desktop remoto per la prima istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-286">On remote desktop session to the first SQL Server.</span></span> <span data-ttu-id="2fa4d-287">In **Esplora oggetti** in SSMS fare clic con il pulsante destro del mouse su **Disponibilità elevata AlwaysOn**, quindi scegliere **Creazione guidata Gruppo di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![Avviare la creazione guidata nuovo gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="2fa4d-289">Nella pagina **Introduzione** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-289">In the **Introduction** page, click **Next**.</span></span> <span data-ttu-id="2fa4d-290">Nella pagina **Specifica nome del gruppo di disponibilità** digitare un nome per il gruppo di disponibilità, ad esempio **AG1**, in **Nome gruppo di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-290">In the **Specify Availability Group Name** page, type a name for the Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="2fa4d-291">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-291">Click **Next**.</span></span>

    ![Creazione guidata nuovo gruppo di disponibilità: specificare il nome di gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="2fa4d-293">Nella pagina **Seleziona database** selezionare il database e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-293">In the **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="2fa4d-294">Il database soddisfa i prerequisiti per un gruppo di disponibilità perché è stato eseguito almeno un backup completo sulla replica primaria usata.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-294">The database meets the prerequisites for an Availability Group because you have taken at least one full backup on the intended primary replica.</span></span>

   ![Creazione guidata nuovo gruppo di disponibilità: selezionare i database](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="2fa4d-296">Nella pagina **Specifica repliche** fare clic su **Aggiungi replica**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-296">In the **Specify Replicas** page, click **Add Replica**.</span></span>

   ![Creazione guidata nuovo gruppo di disponibilità: specificare le repliche](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="2fa4d-298">Viene visualizzata la finestra di dialogo **Connetti al server** .</span><span class="sxs-lookup"><span data-stu-id="2fa4d-298">The **Connect to Server** dialog pops up.</span></span> <span data-ttu-id="2fa4d-299">Digitare il nome del secondo server in **Nome server**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-299">Type the name of the second server in **Server name**.</span></span> <span data-ttu-id="2fa4d-300">Fare clic su **Connect**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-300">Click **Connect**.</span></span>

   <span data-ttu-id="2fa4d-301">Nella pagina **Specifica repliche** verrà ora visualizzato il secondo server elencato in **Repliche di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-301">Back in the **Specify Replicas** page, you should now see the second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="2fa4d-302">Configurare le repliche come segue.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-302">Configure the replicas as follows.</span></span>

   ![Creazione guidata nuovo gruppo di disponibilità: specificare le repliche (complete)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="2fa4d-304">Fare clic su **Endpoint** per visualizzare l'endpoint di mirroring del database per questo gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-304">Click **Endpoints** to see the database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="2fa4d-305">Usare la stessa porta usata quando si è impostata la [regola del firewall per gli endpoint del mirroring del database ](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="2fa4d-305">Use the same port that you used when you set the [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![Creazione guidata nuovo gruppo di disponibilità: selezionare la sincronizzazione dati iniziale](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="2fa4d-307">Nella pagina **Seleziona sincronizzazione dei dati iniziale** selezionare **Completa** e specificare un percorso di rete condiviso.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-307">In the **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="2fa4d-308">Per il percorso, usare la [condivisione di backup creata](#backupshare).</span><span class="sxs-lookup"><span data-stu-id="2fa4d-308">For the location, use the [backup share that you created](#backupshare).</span></span> <span data-ttu-id="2fa4d-309">Nell'esempio era **\\\\\<Prima istanza di SQL Server\>\Backup\**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-309">In the example it was, **\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="2fa4d-310">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="2fa4d-311">La sincronizzazione completa acquisisce un backup completo del database nella prima istanza di SQL Server e lo ripristina nella seconda istanza.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-311">Full synchronization takes a full backup of the database on the first instance of SQL Server and restores it to the second instance.</span></span> <span data-ttu-id="2fa4d-312">Per i database di grandi dimensioni, la sincronizzazione completa non è consigliabile perché può richiedere diverso tempo.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="2fa4d-313">È possibile ridurre manualmente il tempo necessario acquisendo un backup del database e ripristinandolo con `NO RECOVERY`.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-313">You can reduce this time by manually taking a backup of the database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="2fa4d-314">Se il database è già stato ripristinato con `NO RECOVERY` nella seconda istanza di SQL Server prima di configurare il gruppo di disponibilità, scegliere **Solo join**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-314">If the database is already restored with `NO RECOVERY` on the second SQL Server before configuring the Availability Group, choose **Join only**.</span></span> <span data-ttu-id="2fa4d-315">Per acquisire il backup dopo la configurazione del gruppo di disponibilità, scegliere **Ignora sincronizzazione dei dati iniziale**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-315">If you want to take the backup after configuring the Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![Creazione guidata nuovo gruppo di disponibilità: selezionare la sincronizzazione dati iniziale](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="2fa4d-317">Nella pagina **Convalida** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-317">In the **Validation** page, click **Next**.</span></span> <span data-ttu-id="2fa4d-318">La pagina dovrebbe essere simile all'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="2fa4d-318">This page should look similar to the following image:</span></span>

    ![Creazione guidata nuovo gruppo di disponibilità: convalida](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="2fa4d-320">È presente un avviso per la configurazione del listener perché non è stato configurato un listener del gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-320">There is a warning for the listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="2fa4d-321">È possibile ignorare questo avviso perché nelle macchine virtuali di Azure si crea il listener dopo la creazione del servizio di bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-321">You can ignore this warning because on Azure virtual machines you create the listener after creating the Azure load balancer.</span></span>

10. <span data-ttu-id="2fa4d-322">Nella pagina **Riepilogo** fare clic su **Fine**, quindi attendere il completamento della configurazione del nuovo gruppo di disponibilità tramite la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-322">In the **Summary** page, click **Finish**, then wait while the wizard configures the new Availability Group.</span></span> <span data-ttu-id="2fa4d-323">Per visualizzare lo stato dettagliato è possibile fare clic su **Altri dettagli** nella pagina **Stato**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-323">In the **Progress** page, you can click **More details** to view the detailed progress.</span></span> <span data-ttu-id="2fa4d-324">Al termine della procedura guidata, controllare la pagina **Risultati** per verificare che il gruppo di disponibilità sia stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-324">Once the wizard is finished, inspect the **Results** page to verify that the Availability Group is successfully created.</span></span>

     ![Creazione guidata nuovo gruppo di disponibilità: risultati](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="2fa4d-326">Fare clic su **Chiudi** per uscire dalla procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-326">Click **Close** to exit the wizard.</span></span>

### <a name="check-the-availability-group"></a><span data-ttu-id="2fa4d-327">Controllare il gruppo di disponibilità</span><span class="sxs-lookup"><span data-stu-id="2fa4d-327">Check the Availability Group</span></span>

1. <span data-ttu-id="2fa4d-328">In **Esplora oggetti** espandere **Disponibilità elevata AlwaysOn**, quindi espandere **Gruppi di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="2fa4d-329">A questo punto viene visualizzato il nuovo gruppo di disponibilità in questo contenitore.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-329">You should now see the new Availability Group in this container.</span></span> <span data-ttu-id="2fa4d-330">Fare clic con il pulsante destro del mouse sul gruppo di disponibilità e scegliere **Mostra dashboard**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-330">Right-click the Availability Group and click **Show Dashboard**.</span></span>

   ![Mostrare dashboard gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="2fa4d-332">L'aspetto del **Dashboard AlwaysOn** dovrebbe essere simile a questo.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-332">Your **AlwaysOn Dashboard** should look similar to this.</span></span>

   ![Dashboard gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="2fa4d-334">È possibile visualizzare le repliche, la modalità di failover di ciascuna replica e lo stato di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-334">You can see the replicas, the failover mode of each replica and the synchronization state.</span></span>

2. <span data-ttu-id="2fa4d-335">In **Gestione cluster di failover** fare clic sul cluster.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="2fa4d-336">Selezionare **Ruoli**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-336">Select **Roles**.</span></span> <span data-ttu-id="2fa4d-337">Il nome del gruppo di disponibilità usato è un ruolo nel cluster.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-337">The Availability Group name you used is a role on the cluster.</span></span> <span data-ttu-id="2fa4d-338">Tale gruppo di disponibilità non ha un indirizzo IP per le connessioni client, perché non è stato configurato un listener.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="2fa4d-339">Il listener verrà configurato dopo avere creato un servizio di bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-339">You will configure the listener after you create an Azure load balancer.</span></span>

   ![Gruppo di disponibilità in Gestione cluster di failover](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="2fa4d-341">Non provare a eseguire il failover del gruppo di disponibilità da Gestione cluster di failover.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-341">Do not try to fail over the Availability Group from the Failover Cluster Manager.</span></span> <span data-ttu-id="2fa4d-342">È consigliabile eseguire tutte le operazioni di failover nel **Dashboard AlwaysOn** in SSMS.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="2fa4d-343">Per altre informazioni, vedere [Restrictions on Using The Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx) (Limitazioni sull'uso di Gestione cluster di failover con i gruppi di disponibilità).</span><span class="sxs-lookup"><span data-stu-id="2fa4d-343">For more information, see [Restrictions on Using The Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="2fa4d-344">A questo punto, è presente un gruppo di disponibilità con repliche in due istanze di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="2fa4d-345">È possibile spostare il gruppo di disponibilità tra le istanze.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-345">You can move the Availability Group between instances.</span></span> <span data-ttu-id="2fa4d-346">Non è ancora possibile connettersi al gruppo di disponibilità perché non si ha un listener.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-346">You cannot connect to the Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="2fa4d-347">Nelle macchine virtuali di Azure il listener richiede un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-347">In Azure virtual machines, the listener requires a load balancer.</span></span> <span data-ttu-id="2fa4d-348">Il passaggio successivo consiste nel creare il servizio di bilanciamento del carico in Azure.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-348">The next step is to create the load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="2fa4d-349">Creare un servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="2fa4d-349">Create an Azure load balancer</span></span>

<span data-ttu-id="2fa4d-350">Nelle macchine virtuali di Azure un gruppo di disponibilità SQL Server richiede un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="2fa4d-351">Il servizio di bilanciamento del carico contiene l'indirizzo IP per il listener del gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-351">The load balancer holds the IP address for the Availability Group listener.</span></span> <span data-ttu-id="2fa4d-352">Questa sezione è un riepilogo della creazione del servizio di bilanciamento del carico nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-352">This section summarizes how to create the load balancer in the Azure portal.</span></span>

1. <span data-ttu-id="2fa4d-353">Nel portale di Azure andare al gruppo di risorse in cui si trovano le istanze di SQL Server e fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-353">In the Azure portal, go to the resource group where your SQL Servers are and click **+ Add**.</span></span>
2. <span data-ttu-id="2fa4d-354">Cercare **Servizio di bilanciamento del carico**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-354">Search for **Load Balancer**.</span></span> <span data-ttu-id="2fa4d-355">Scegliere il servizio di bilanciamento del carico pubblicato da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-355">Choose the load balancer published by Microsoft.</span></span>

   ![Gruppo di disponibilità in Gestione cluster di failover](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  <span data-ttu-id="2fa4d-357">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-357">Click **Create**.</span></span>
3. <span data-ttu-id="2fa4d-358">Configurare i parametri seguenti per il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-358">Configure the following parameters for the load balancer.</span></span>

   | <span data-ttu-id="2fa4d-359">Impostazione</span><span class="sxs-lookup"><span data-stu-id="2fa4d-359">Setting</span></span> | <span data-ttu-id="2fa4d-360">Campo</span><span class="sxs-lookup"><span data-stu-id="2fa4d-360">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="2fa4d-361">**Nome**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-361">**Name**</span></span> |<span data-ttu-id="2fa4d-362">Usare un nome in formato testo per il servizio di bilanciamento del carico, ad esempio **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-362">Use a text name for the load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="2fa4d-363">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-363">**Type**</span></span> |<span data-ttu-id="2fa4d-364">Interno</span><span class="sxs-lookup"><span data-stu-id="2fa4d-364">Internal</span></span> |
   | <span data-ttu-id="2fa4d-365">**Rete virtuale**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-365">**Virtual network**</span></span> |<span data-ttu-id="2fa4d-366">Usare il nome della rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-366">Use the name of the Azure virtual network.</span></span> |
   | <span data-ttu-id="2fa4d-367">**Subnet**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-367">**Subnet**</span></span> |<span data-ttu-id="2fa4d-368">Usare il nome della subnet in cui si trova la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-368">Use the name of the subnet that the virtual machine is in.</span></span>  |
   | <span data-ttu-id="2fa4d-369">**Assegnazione indirizzi IP**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-369">**IP address assignment**</span></span> |<span data-ttu-id="2fa4d-370">Static</span><span class="sxs-lookup"><span data-stu-id="2fa4d-370">Static</span></span> |
   | <span data-ttu-id="2fa4d-371">**Indirizzo IP**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-371">**IP address**</span></span> |<span data-ttu-id="2fa4d-372">Usare un indirizzo disponibile nella subnet.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-372">Use an available address from subnet.</span></span> |
   | <span data-ttu-id="2fa4d-373">**Sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-373">**Subscription**</span></span> |<span data-ttu-id="2fa4d-374">Usare la stessa sottoscrizione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-374">Use the same subscription as the virtual machine.</span></span> |
   | <span data-ttu-id="2fa4d-375">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-375">**Location**</span></span> |<span data-ttu-id="2fa4d-376">Usare la stessa posizione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-376">Use the same location as the virtual machine.</span></span> |

   <span data-ttu-id="2fa4d-377">Il pannello del portale di Azure dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="2fa4d-377">The Azure portal blade should look like this:</span></span>

   ![Crea servizio di bilanciamento del carico](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="2fa4d-379">Al termine, fare clic su **Crea** per creare il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-379">Click **Create**, to create the load balancer.</span></span>

<span data-ttu-id="2fa4d-380">Per configurare il servizio di bilanciamento del carico, è necessario creare un pool back-end e un probe e impostare le regole di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-380">To configure the load balancer, you need to create a backend pool, a probe, and set the load balancing rules.</span></span> <span data-ttu-id="2fa4d-381">Eseguire queste operazioni nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-381">Do these in the Azure portal.</span></span>

### <a name="add-backend-pool"></a><span data-ttu-id="2fa4d-382">Aggiungere un pool back-end</span><span class="sxs-lookup"><span data-stu-id="2fa4d-382">Add backend pool</span></span>

1. <span data-ttu-id="2fa4d-383">Nel portale di Azure andare al gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-383">In the Azure portal, go to your availability group.</span></span> <span data-ttu-id="2fa4d-384">Potrebbe essere necessario aggiornare la visualizzazione per vedere il servizio di bilanciamento del carico appena creato.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-384">You might need to refresh the view to see the newly created load balancer.</span></span>

   ![Trovare il servizio di bilanciamento del carico nel gruppo di risorse](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="2fa4d-386">Fare clic sul servizio di bilanciamento del carico, quindi su **Pool back-end** e infine su **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-386">Click the load balancer, click **Backend pools**, and click **+Add**.</span></span> <span data-ttu-id="2fa4d-387">Impostare il pool back-end come segue:</span><span class="sxs-lookup"><span data-stu-id="2fa4d-387">Set the backend pool as follows:</span></span>

   | <span data-ttu-id="2fa4d-388">Impostazione</span><span class="sxs-lookup"><span data-stu-id="2fa4d-388">Setting</span></span> | <span data-ttu-id="2fa4d-389">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2fa4d-389">Description</span></span> | <span data-ttu-id="2fa4d-390">Esempio</span><span class="sxs-lookup"><span data-stu-id="2fa4d-390">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="2fa4d-391">**Nome**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-391">**Name**</span></span> | <span data-ttu-id="2fa4d-392">Digitare un nome in formato testo</span><span class="sxs-lookup"><span data-stu-id="2fa4d-392">Type a text name</span></span> | <span data-ttu-id="2fa4d-393">SQLLBBE</span><span class="sxs-lookup"><span data-stu-id="2fa4d-393">SQLLBBE</span></span>
   | <span data-ttu-id="2fa4d-394">**Associato a**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-394">**Associated to**</span></span> | <span data-ttu-id="2fa4d-395">Selezionare dall'elenco</span><span class="sxs-lookup"><span data-stu-id="2fa4d-395">Pick from list</span></span> | <span data-ttu-id="2fa4d-396">Set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="2fa4d-396">Availability set</span></span>
   | <span data-ttu-id="2fa4d-397">**Set di disponibilità**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-397">**Availability set**</span></span> | <span data-ttu-id="2fa4d-398">Usare un nome del set di disponibilità in cui si trovano le VM di SQL Server</span><span class="sxs-lookup"><span data-stu-id="2fa4d-398">Use a name of the availability set that your SQL Server VMs are in</span></span> | <span data-ttu-id="2fa4d-399">sqlAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="2fa4d-399">sqlAvailabilitySet</span></span> |
   | <span data-ttu-id="2fa4d-400">**Macchine virtuali**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-400">**Virtual machines**</span></span> |<span data-ttu-id="2fa4d-401">I nomi delle due VM di SQL Server</span><span class="sxs-lookup"><span data-stu-id="2fa4d-401">The two Azure SQL Server VM names</span></span> | <span data-ttu-id="2fa4d-402">sqlserver-0, sqlserver-1</span><span class="sxs-lookup"><span data-stu-id="2fa4d-402">sqlserver-0, sqlserver-1</span></span>

1. <span data-ttu-id="2fa4d-403">Digitare il nome per il pool back-end.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-403">Type the name for the back end pool.</span></span>

1. <span data-ttu-id="2fa4d-404">Fare clic su **+ Aggiungi una macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-404">Click **+ Add a virtual machine**.</span></span>

1. <span data-ttu-id="2fa4d-405">Per il set di disponibilità, scegliere quello in cui si trovano le istanze di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-405">For the availability set, choose the availability set that the SQL Servers are in.</span></span>

1. <span data-ttu-id="2fa4d-406">Per le macchine virtuali, includere entrambe le istanze di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-406">For virtual machines, include both of the SQL Servers.</span></span> <span data-ttu-id="2fa4d-407">Non includere il server di controllo della condivisione file.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-407">Do not include the file share witness server.</span></span>

1. <span data-ttu-id="2fa4d-408">Fare clic su **OK** per creare il pool back-end.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-408">Click **OK** to create the backend pool.</span></span>

### <a name="set-the-probe"></a><span data-ttu-id="2fa4d-409">Impostare il probe</span><span class="sxs-lookup"><span data-stu-id="2fa4d-409">Set the probe</span></span>

1. <span data-ttu-id="2fa4d-410">Fare clic sul servizio di bilanciamento del carico, quindi su **Probe integrità** e infine su **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-410">Click the load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="2fa4d-411">Impostare il probe di integrità nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="2fa4d-411">Set the health probe as follows:</span></span>

   | <span data-ttu-id="2fa4d-412">Impostazione</span><span class="sxs-lookup"><span data-stu-id="2fa4d-412">Setting</span></span> | <span data-ttu-id="2fa4d-413">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2fa4d-413">Description</span></span> | <span data-ttu-id="2fa4d-414">Esempio</span><span class="sxs-lookup"><span data-stu-id="2fa4d-414">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="2fa4d-415">**Nome**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-415">**Name**</span></span> | <span data-ttu-id="2fa4d-416">Text</span><span class="sxs-lookup"><span data-stu-id="2fa4d-416">Text</span></span> | <span data-ttu-id="2fa4d-417">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="2fa4d-417">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="2fa4d-418">**Protocollo**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-418">**Protocol**</span></span> | <span data-ttu-id="2fa4d-419">Scegliere TCP</span><span class="sxs-lookup"><span data-stu-id="2fa4d-419">Choose TCP</span></span> | <span data-ttu-id="2fa4d-420">TCP</span><span class="sxs-lookup"><span data-stu-id="2fa4d-420">TCP</span></span> |
   | <span data-ttu-id="2fa4d-421">**Porta**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-421">**Port**</span></span> | <span data-ttu-id="2fa4d-422">Qualsiasi porta non usata</span><span class="sxs-lookup"><span data-stu-id="2fa4d-422">Any unused port</span></span> | <span data-ttu-id="2fa4d-423">59999</span><span class="sxs-lookup"><span data-stu-id="2fa4d-423">59999</span></span> |
   | <span data-ttu-id="2fa4d-424">**Interval**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-424">**Interval**</span></span>  | <span data-ttu-id="2fa4d-425">Intervallo di tempo tra i tentativi del probe, in secondi</span><span class="sxs-lookup"><span data-stu-id="2fa4d-425">The amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="2fa4d-426">5</span><span class="sxs-lookup"><span data-stu-id="2fa4d-426">5</span></span> |
   | <span data-ttu-id="2fa4d-427">**Soglia non integra**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-427">**Unhealthy threshold**</span></span> | <span data-ttu-id="2fa4d-428">Numero di errori consecutivi del probe che devono verificarsi per considerare non integra una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="2fa4d-428">The number of consecutive probe failures that must occur for a virtual machine to be considered unhealthy</span></span>  | <span data-ttu-id="2fa4d-429">2</span><span class="sxs-lookup"><span data-stu-id="2fa4d-429">2</span></span> |

1. <span data-ttu-id="2fa4d-430">Fare clic su **OK** per impostare il probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-430">Click **OK** to set the health probe.</span></span>

### <a name="set-the-load-balancing-rules"></a><span data-ttu-id="2fa4d-431">Impostare le regole di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="2fa4d-431">Set the load balancing rules</span></span>

1. <span data-ttu-id="2fa4d-432">Fare clic sul servizio di bilanciamento del carico, quindi su **Regole di bilanciamento del carico** e infine su **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-432">Click the load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="2fa4d-433">Impostare le regole di bilanciamento del carico come segue.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-433">Set the load balancing rules as follows.</span></span>
   | <span data-ttu-id="2fa4d-434">Impostazione</span><span class="sxs-lookup"><span data-stu-id="2fa4d-434">Setting</span></span> | <span data-ttu-id="2fa4d-435">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2fa4d-435">Description</span></span> | <span data-ttu-id="2fa4d-436">Esempio</span><span class="sxs-lookup"><span data-stu-id="2fa4d-436">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="2fa4d-437">**Nome**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-437">**Name**</span></span> | <span data-ttu-id="2fa4d-438">Text</span><span class="sxs-lookup"><span data-stu-id="2fa4d-438">Text</span></span> | <span data-ttu-id="2fa4d-439">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="2fa4d-439">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="2fa4d-440">**Indirizzo IP front-end IP**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-440">**Frontend IP address**</span></span> | <span data-ttu-id="2fa4d-441">Scegliere un indirizzo</span><span class="sxs-lookup"><span data-stu-id="2fa4d-441">Choose an address</span></span> |<span data-ttu-id="2fa4d-442">Usare l'indirizzo creato quando si è creato il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-442">Use the address that you created when you created the load balancer.</span></span> |
   | <span data-ttu-id="2fa4d-443">**Protocollo**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-443">**Protocol**</span></span> | <span data-ttu-id="2fa4d-444">Scegliere TCP</span><span class="sxs-lookup"><span data-stu-id="2fa4d-444">Choose TCP</span></span> |<span data-ttu-id="2fa4d-445">TCP</span><span class="sxs-lookup"><span data-stu-id="2fa4d-445">TCP</span></span> |
   | <span data-ttu-id="2fa4d-446">**Porta**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-446">**Port**</span></span> | <span data-ttu-id="2fa4d-447">Usare la porta per l'istanza di SQL Server</span><span class="sxs-lookup"><span data-stu-id="2fa4d-447">Use the port for the SQL Server instance</span></span> | <span data-ttu-id="2fa4d-448">1433</span><span class="sxs-lookup"><span data-stu-id="2fa4d-448">1433</span></span> |
   | <span data-ttu-id="2fa4d-449">**Porta back-end**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-449">**Backend Port**</span></span> | <span data-ttu-id="2fa4d-450">Questo campo non viene usato quando l'indirizzo IP mobile è impostato per Direct Server Return</span><span class="sxs-lookup"><span data-stu-id="2fa4d-450">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="2fa4d-451">1433</span><span class="sxs-lookup"><span data-stu-id="2fa4d-451">1433</span></span> |
   | <span data-ttu-id="2fa4d-452">**Probe**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-452">**Probe**</span></span> |<span data-ttu-id="2fa4d-453">Il nome specificato per il probe</span><span class="sxs-lookup"><span data-stu-id="2fa4d-453">The name you specified for the probe</span></span> | <span data-ttu-id="2fa4d-454">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="2fa4d-454">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="2fa4d-455">**Persistenza della sessione**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-455">**Session Persistence**</span></span> | <span data-ttu-id="2fa4d-456">Elenco a discesa</span><span class="sxs-lookup"><span data-stu-id="2fa4d-456">Drop down list</span></span> | <span data-ttu-id="2fa4d-457">**Nessuno**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-457">**None**</span></span> |
   | <span data-ttu-id="2fa4d-458">**Timeout di inattività**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-458">**Idle Timeout**</span></span> | <span data-ttu-id="2fa4d-459">Minuti in cui tenere aperta una connessione TCP</span><span class="sxs-lookup"><span data-stu-id="2fa4d-459">Minutes to keep a TCP connection open</span></span> | <span data-ttu-id="2fa4d-460">4</span><span class="sxs-lookup"><span data-stu-id="2fa4d-460">4</span></span> |
   | <span data-ttu-id="2fa4d-461">**IP mobile (Direct Server Return)**</span><span class="sxs-lookup"><span data-stu-id="2fa4d-461">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="2fa4d-462">Enabled</span><span class="sxs-lookup"><span data-stu-id="2fa4d-462">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="2fa4d-463">Direct Server Return viene impostato durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-463">Direct server return is set during creation.</span></span> <span data-ttu-id="2fa4d-464">Non può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-464">It cannot be changed.</span></span>

1. <span data-ttu-id="2fa4d-465">Fare clic su **OK** per impostare le regole di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-465">Click **OK** to set the load balancing rules.</span></span>

## <span data-ttu-id="2fa4d-466"><a name="configure-listener"></a> Configurare il listener</span><span class="sxs-lookup"><span data-stu-id="2fa4d-466"><a name="configure-listener"></a> Configure the listener</span></span>

<span data-ttu-id="2fa4d-467">A questo punto, è necessario configurare il listener del gruppo di disponibilità nel cluster di failover.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-467">The next thing to do is to configure an Availability Group listener on the failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa4d-468">Questa esercitazione illustra come creare un singolo listener, con un indirizzo IP del servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-468">This tutorial shows how to create a single listener - with one ILB IP address.</span></span> <span data-ttu-id="2fa4d-469">Per creare uno o più listener usando uno o più indirizzi IP, vedere [Create availability group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Creare un servizio di bilanciamento del carico e un listener per il gruppo di disponibilità | Azure).</span><span class="sxs-lookup"><span data-stu-id="2fa4d-469">To create one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="2fa4d-470">Impostare la porta del listener</span><span class="sxs-lookup"><span data-stu-id="2fa4d-470">Set listener port</span></span>

<span data-ttu-id="2fa4d-471">In SQL Server Management Studio impostare la porta del listener.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-471">In SQL Server Management Studio, set the listener port.</span></span>

1. <span data-ttu-id="2fa4d-472">Avviare SQL Server Management Studio e connettersi alla replica primaria.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-472">Launch SQL Server Management Studio and connect to the primary replica.</span></span>

1. <span data-ttu-id="2fa4d-473">Passare a **Disponibilità elevata AlwaysOn** | **Gruppi di disponibilità** | **Listener gruppo di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-473">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="2fa4d-474">Viene visualizzato il nome del listener creato in Gestione Cluster di Failover.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-474">You should now see the listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="2fa4d-475">Fare clic con il pulsante destro del mouse sul nome del listener e quindi su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-475">Right-click the listener name and click **Properties**.</span></span>

1. <span data-ttu-id="2fa4d-476">Nella casella **Porta** specificare il numero di porta per il listener del gruppo di disponibilità usando il valore di $EndpointPort usato in precedenza (l'impostazione predefinita era 1433), quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-476">In the **Port** box, specify the port number for the Availability Group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.</span></span>

<span data-ttu-id="2fa4d-477">Ora si ha un gruppo di disponibilità di SQL Server nelle macchine virtuali di Azure in esecuzione in modalità Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-477">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-to-listener"></a><span data-ttu-id="2fa4d-478">Testare la connessione al listener</span><span class="sxs-lookup"><span data-stu-id="2fa4d-478">Test connection to listener</span></span>

<span data-ttu-id="2fa4d-479">Per testare la connessione:</span><span class="sxs-lookup"><span data-stu-id="2fa4d-479">To test the connection:</span></span>

1. <span data-ttu-id="2fa4d-480">Usare RDP per connettersi a un'istanza di SQL Server che si trova nella stessa rete virtuale, ma non è proprietaria della replica.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-480">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span></span> <span data-ttu-id="2fa4d-481">È possibile usare l'altra istanza di SQL Server nel cluster.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-481">You can use the other SQL Server in the cluster.</span></span>

1. <span data-ttu-id="2fa4d-482">Usare l'utilità **sqlcmd** per testare la connessione.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-482">Use **sqlcmd** utility to test the connection.</span></span> <span data-ttu-id="2fa4d-483">Lo script seguente, ad esempio, stabilisce una connessione **sqlcmd** alla replica primaria tramite il listener con l'autenticazione di Windows:</span><span class="sxs-lookup"><span data-stu-id="2fa4d-483">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span></span>

    ```
    sqlcmd -S <listenerName> -E
    ```

    <span data-ttu-id="2fa4d-484">Se il listener usa una porta diversa da quella predefinita (1433), specificare la porta nella stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-484">If the listener is using a port other than the default port (1433), specify the port in the connection string.</span></span> <span data-ttu-id="2fa4d-485">Il seguente comando sqlcmd, ad esempio, si connette a un listener nella porta 1435:</span><span class="sxs-lookup"><span data-stu-id="2fa4d-485">For example, the following sqlcmd command connects to a listener at port 1435:</span></span>

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="2fa4d-486">La connessione SQLCMD si connette automaticamente a qualsiasi istanza di SQL Server ospiti la replica primaria.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-486">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="2fa4d-487">Verificare che la porta specificata sia aperta nel firewall di entrambe le istanze di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-487">Make sure that the port you specify is open on the firewall of both SQL Servers.</span></span> <span data-ttu-id="2fa4d-488">Per entrambi i server è necessaria una regola in ingresso per la porta TCP usata.</span><span class="sxs-lookup"><span data-stu-id="2fa4d-488">Both servers require an inbound rule for the TCP port that you use.</span></span> <span data-ttu-id="2fa4d-489">Per altre informazioni, vedere [Aggiungere o modificare una regola del firewall](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="2fa4d-489">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by the way” info, an Important is info users need to complete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is the second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note the format for documenting the UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult to maintain. Highlight areas you are referring to in red.*-->

<!--**No. of steps**: *Make sure the number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want to go on.*-->

## <a name="next-steps"></a><span data-ttu-id="2fa4d-490">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2fa4d-490">Next steps</span></span>

- <span data-ttu-id="2fa4d-491">[Add an IP address to a load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP) (Aggiungere un indirizzo IP a un servizio di bilanciamento del carico per un secondo gruppo di disponibilità).</span><span class="sxs-lookup"><span data-stu-id="2fa4d-491">[Add an IP address to a load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>
