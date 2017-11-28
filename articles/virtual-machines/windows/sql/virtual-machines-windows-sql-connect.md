---
title: aaaConnect tooa macchina virtuale di SQL Server (gestione delle risorse) | Documenti Microsoft
description: Informazioni su come tooconnect tooSQL Server in esecuzione in una macchina virtuale in Azure. Questo argomento viene utilizzato il modello di distribuzione classica hello. scenari di Hello diversi a seconda della configurazione di rete hello e il percorso di hello del client hello.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a><span data-ttu-id="e0db3-105">Connettersi tooa macchina virtuale di SQL Server in Azure (gestione delle risorse)</span><span class="sxs-lookup"><span data-stu-id="e0db3-105">Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0db3-106">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="e0db3-106">Resource Manager</span></span>](virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="e0db3-107">Classico</span><span class="sxs-lookup"><span data-stu-id="e0db3-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="e0db3-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e0db3-108">Overview</span></span>

<span data-ttu-id="e0db3-109">In questo argomento viene descritto come tooconnect tooyour SQL Server dell'istanza in esecuzione in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e0db3-109">This topic describes how tooconnect tooyour SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="e0db3-110">Illustra alcuni [scenari di connettività generali](#connection-scenarios) e quindi descrive la [procedura dettagliata per la configurazione della connettività di SQL Server in una macchina virtuale di Azure](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="e0db3-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="e0db3-111">Per una procedura dettagliata completa del provisioning e della connettività, vedere [Provisioning di una macchina virtuale di SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="e0db3-111">If you would rather have a full walk-through of both provisioning and connectivity, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="e0db3-112">Scenari di connessione</span><span class="sxs-lookup"><span data-stu-id="e0db3-112">Connection scenarios</span></span>

<span data-ttu-id="e0db3-113">modo Hello un client si connette a Server in esecuzione in una macchina virtuale varia a seconda della posizione di hello del client hello e configurazione di rete hello tooSQL.</span><span class="sxs-lookup"><span data-stu-id="e0db3-113">hello way a client connects tooSQL Server running on a Virtual Machine differs depending on hello location of hello client and hello networking configuration.</span></span>

<span data-ttu-id="e0db3-114">Se si esegue il provisioning di una VM SQL Server in hello portale di Azure, è possibile hello che specifica il tipo di hello di **connettività SQL**.</span><span class="sxs-lookup"><span data-stu-id="e0db3-114">If you provision a SQL Server VM in hello Azure portal, you have hello option of specifying hello type of **SQL connectivity**.</span></span>

![Opzione di connettività SQL pubblica durante il provisioning](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

<span data-ttu-id="e0db3-116">Le opzioni per la connettività sono:</span><span class="sxs-lookup"><span data-stu-id="e0db3-116">Your options for connectivity include:</span></span>

| <span data-ttu-id="e0db3-117">Opzione</span><span class="sxs-lookup"><span data-stu-id="e0db3-117">Option</span></span> | <span data-ttu-id="e0db3-118">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e0db3-118">Description</span></span> |
|---|---|
| <span data-ttu-id="e0db3-119">**Pubblica**</span><span class="sxs-lookup"><span data-stu-id="e0db3-119">**Public**</span></span> | <span data-ttu-id="e0db3-120">Connettersi tooSQL Server su hello internet</span><span class="sxs-lookup"><span data-stu-id="e0db3-120">Connect tooSQL Server over hello internet</span></span> |
| <span data-ttu-id="e0db3-121">**Privata**</span><span class="sxs-lookup"><span data-stu-id="e0db3-121">**Private**</span></span> | <span data-ttu-id="e0db3-122">Connettersi tooSQL Server in hello stessa rete virtuale</span><span class="sxs-lookup"><span data-stu-id="e0db3-122">Connect tooSQL Server in hello same virtual network</span></span> |
| <span data-ttu-id="e0db3-123">**Locale**</span><span class="sxs-lookup"><span data-stu-id="e0db3-123">**Local**</span></span> | <span data-ttu-id="e0db3-124">Connettersi tooSQL Server in locale hello stessa macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e0db3-124">Connect tooSQL Server locally on hello same virtual machine</span></span> | 

<span data-ttu-id="e0db3-125">Nelle sezioni seguenti Hello viene hello **pubblica** e **privata** opzioni in modo più dettagliato.</span><span class="sxs-lookup"><span data-stu-id="e0db3-125">hello following sections explain hello **Public** and **Private** options in more detail.</span></span>

## <a name="connect-toosql-server-over-hello-internet"></a><span data-ttu-id="e0db3-126">Connettersi tooSQL Server su Internet hello</span><span class="sxs-lookup"><span data-stu-id="e0db3-126">Connect tooSQL Server over hello Internet</span></span>

<span data-ttu-id="e0db3-127">Se si desidera motore di database di SQL Server tooconnect tooyour da hello Internet, selezionare **pubblica** per hello **connettività SQL** nel portale di hello durante il provisioning del tipo.</span><span class="sxs-lookup"><span data-stu-id="e0db3-127">If you want tooconnect tooyour SQL Server database engine from hello Internet, select **Public** for hello **SQL connectivity** type in hello portal during provisioning.</span></span> <span data-ttu-id="e0db3-128">portale Hello hello automaticamente i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e0db3-128">hello portal automatically does hello following steps:</span></span>

* <span data-ttu-id="e0db3-129">Abilita protocollo TCP/IP hello per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0db3-129">Enables hello TCP/IP protocol for SQL Server.</span></span>
* <span data-ttu-id="e0db3-130">Configura hello di tooopen una regola firewall la porta TCP di SQL Server (valore predefinito 1433).</span><span class="sxs-lookup"><span data-stu-id="e0db3-130">Configures a firewall rule tooopen hello SQL Server TCP port (default 1433).</span></span>
* <span data-ttu-id="e0db3-131">Abilita l'autenticazione di SQL Server, necessaria per l'accesso pubblico.</span><span class="sxs-lookup"><span data-stu-id="e0db3-131">Enables SQL Server Authentication, required for public access.</span></span>
* <span data-ttu-id="e0db3-132">Configura gruppo di sicurezza di rete hello hello traffico TCP tooall delle macchine Virtuali su hello porta SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0db3-132">Configures hello network security group on hello VM tooall TCP traffic on hello SQL Server port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0db3-133">le immagini di macchina virtuale Hello per SQL Server Developer hello e le edizioni Express non abilitano automaticamente il protocollo TCP/IP hello.</span><span class="sxs-lookup"><span data-stu-id="e0db3-133">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="e0db3-134">Per le edizioni Developer ed Express, è necessario utilizzare Gestione configurazione SQL Server troppo[abilitare manualmente il protocollo TCP/IP hello](#manualtcp) dopo la creazione di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e0db3-134">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="e0db3-135">Qualsiasi client con accesso a internet può connettersi toohello istanza di SQL Server specificando l'indirizzo IP pubblico hello della macchina virtuale hello o qualsiasi etichetta DNS assegnato l'indirizzo IP toothat.</span><span class="sxs-lookup"><span data-stu-id="e0db3-135">Any client with internet access can connect toohello SQL Server instance by specifying either hello public IP address of hello virtual machine or any DNS label assigned toothat IP address.</span></span> <span data-ttu-id="e0db3-136">Se la porta di SQL Server hello è 1433, non è necessario toospecify nella stringa di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="e0db3-136">If hello SQL Server port is 1433, you do not need toospecify it in hello connection string.</span></span> <span data-ttu-id="e0db3-137">Hello seguente stringa di connessione si connette tooa VM SQL con un'etichetta DNS di `sqlvmlabel.eastus.cloudapp.azure.com` utilizzando l'autenticazione di SQL (è anche possibile usare indirizzi IP pubblici hello).</span><span class="sxs-lookup"><span data-stu-id="e0db3-137">hello following connection string connects tooa SQL VM with a DNS label of `sqlvmlabel.eastus.cloudapp.azure.com` using SQL Authentication (you could also use hello public IP address).</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

<span data-ttu-id="e0db3-138">Sebbene in questo modo la connettività per i client su internet di hello, ciò non implica che tutti gli utenti possono connettersi tooyour SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0db3-138">Although this enables connectivity for clients over hello internet, this does not imply that anyone can connect tooyour SQL Server.</span></span> <span data-ttu-id="e0db3-139">I client esterni avere toohello correttezza del nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="e0db3-139">Outside clients have toohello correct username and password.</span></span> <span data-ttu-id="e0db3-140">Tuttavia, per maggiore sicurezza, è possibile evitare la porta 1433 noto hello.</span><span class="sxs-lookup"><span data-stu-id="e0db3-140">However, for additional security, you can avoid hello well-known port 1433.</span></span> <span data-ttu-id="e0db3-141">Ad esempio, se è stato configurato toolisten di SQL Server sulla porta 1500 e stabilito firewall appropriate e regole di gruppo di sicurezza di rete, è Impossibile connettersi aggiungendo hello porta numero toohello nome del Server.</span><span class="sxs-lookup"><span data-stu-id="e0db3-141">For example, if you configured SQL Server toolisten on port 1500 and established proper firewall and network security group rules, you could connect by appending hello port number toohello Server name.</span></span> <span data-ttu-id="e0db3-142">Hello esempio seguente viene modificato hello precedente tramite l'aggiunta di un numero di porta personalizzato, **1500**, nome del server toohello:</span><span class="sxs-lookup"><span data-stu-id="e0db3-142">hello following example alters hello previous one by adding a custom port number, **1500**, toohello server name:</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> <span data-ttu-id="e0db3-143">Quando si esegue una query SQL Server in una macchina virtuale su hello internet, tutti i dati in uscita da hello Azure datacenter è soggetto toonormal [prezzi sui trasferimenti di dati in uscita](https://azure.microsoft.com/pricing/details/data-transfers/).</span><span class="sxs-lookup"><span data-stu-id="e0db3-143">When you query SQL Server in a VM over hello internet, all outgoing data from hello Azure datacenter is subject toonormal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>

## <a name="connect-toosql-server-within-a-virtual-network"></a><span data-ttu-id="e0db3-144">Connettersi tooSQL Server all'interno di una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="e0db3-144">Connect tooSQL Server within a virtual network</span></span>

<span data-ttu-id="e0db3-145">Quando si sceglie **privata** per hello **connettività SQL** tipo nel portale di hello Azure consente di configurare la maggior parte delle impostazioni di hello identiche troppo**pubblica**.</span><span class="sxs-lookup"><span data-stu-id="e0db3-145">When you choose **Private** for hello **SQL connectivity** type in hello portal, Azure configures most of hello settings identical too**Public**.</span></span> <span data-ttu-id="e0db3-146">Hello una differenza è che non sia presente alcuna regola tooallow di rete sicurezza gruppo di fuori del traffico sulla porta di SQL Server hello (valore predefinito 1433).</span><span class="sxs-lookup"><span data-stu-id="e0db3-146">hello one difference is that there is no network security group rule tooallow outside traffic on hello SQL Server port (default 1433).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0db3-147">le immagini di macchina virtuale Hello per SQL Server Developer hello e le edizioni Express non abilitano automaticamente il protocollo TCP/IP hello.</span><span class="sxs-lookup"><span data-stu-id="e0db3-147">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="e0db3-148">Per le edizioni Developer ed Express, è necessario utilizzare Gestione configurazione SQL Server troppo[abilitare manualmente il protocollo TCP/IP hello](#manualtcp) dopo la creazione di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e0db3-148">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="e0db3-149">La connettività privata viene spesso usata in combinazione con una [rete virtuale](../../../virtual-network/virtual-networks-overview.md), che consente diversi scenari.</span><span class="sxs-lookup"><span data-stu-id="e0db3-149">Private connectivity is often used in conjunction with [Virtual Network](../../../virtual-network/virtual-networks-overview.md), which enables several scenarios.</span></span> <span data-ttu-id="e0db3-150">È possibile connettere le macchine virtuali nella stessa rete virtuale, anche se tali macchine virtuali presenti in diversi gruppi di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="e0db3-150">You can connect VMs in hello same virtual network, even if those VMs exist in different resource groups.</span></span> <span data-ttu-id="e0db3-151">Con una [VPN da sito a sito](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)è possibile creare un'architettura ibrida che connette le macchine virtuali a computer e reti locali.</span><span class="sxs-lookup"><span data-stu-id="e0db3-151">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="e0db3-152">Reti virtuali abilitare anche toojoin è il dominio di tooa macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="e0db3-152">Virtual networks also enable     you toojoin your Azure VMs tooa domain.</span></span> <span data-ttu-id="e0db3-153">Si tratta di hello solo modo toouse l'autenticazione di Windows tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0db3-153">This is hello only way toouse Windows Authentication tooSQL Server.</span></span> <span data-ttu-id="e0db3-154">Hello altri scenari di connessione richiedono l'autenticazione di SQL con nomi utente e password.</span><span class="sxs-lookup"><span data-stu-id="e0db3-154">hello other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="e0db3-155">Supponendo che è stato configurato DNS nella rete virtuale, è possibile connettersi tooyour istanza di SQL Server specificando il nome del computer hello macchina virtuale SQL Server nella stringa di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="e0db3-155">Assuming that you have configured DNS in your virtual network, you can connect tooyour SQL Server instance by specifying hello SQL Server VM computer name in hello connection string.</span></span> <span data-ttu-id="e0db3-156">Hello di esempio seguente, inoltre si presuppone che anche l'autenticazione di Windows è stata configurata e tale utente di hello è stata concessa l'istanza di SQL Server di accesso toohello.</span><span class="sxs-lookup"><span data-stu-id="e0db3-156">hello following example also assumes that Windows Authentication has also been configured and that hello user has been granted access toohello SQL Server instance.</span></span>

```
Server=mysqlvm;Integrated Security=true
```

## <span data-ttu-id="e0db3-157"><a id="change"></a>Modificare le impostazioni di connettività SQL</span><span class="sxs-lookup"><span data-stu-id="e0db3-157"><a id="change"></a> Change SQL connectivity settings</span></span>

<span data-ttu-id="e0db3-158">È possibile modificare le impostazioni di connettività hello per la macchina virtuale di SQL Server nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e0db3-158">You can change hello connectivity settings for your SQL Server virtual machine in hello Azure portal.</span></span>

1. <span data-ttu-id="e0db3-159">Nel portale di Azure hello, selezionare **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="e0db3-159">In hello Azure portal, select **Virtual Machines**.</span></span>

2. <span data-ttu-id="e0db3-160">Selezionare la VM di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0db3-160">Select your SQL Server VM.</span></span>

3. <span data-ttu-id="e0db3-161">In **Impostazioni** fare clic su **Configurazione di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e0db3-161">Under **Settings**, click **SQL Server configuration**.</span></span>

4. <span data-ttu-id="e0db3-162">Hello modifica **il livello di connettività SQL** tooyour necessaria l'impostazione.</span><span class="sxs-lookup"><span data-stu-id="e0db3-162">Change hello **SQL connectivity level** tooyour required setting.</span></span> <span data-ttu-id="e0db3-163">Facoltativamente, è possibile utilizzare questo hello toochange area porta SQL Server o le impostazioni di autenticazione di SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="e0db3-163">You can optionally use this area toochange hello SQL Server port or hello SQL Authentication settings.</span></span>

   ![Modificare la connettività SQL](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. <span data-ttu-id="e0db3-165">Attendere alcuni minuti per hello toocomplete di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="e0db3-165">Wait several minutes for hello update toocomplete.</span></span>

   ![Notifica dell'aggiornamento della VM SQL](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <span data-ttu-id="e0db3-167"><a id="manualtcp"></a>Abilitare TCP/IP per SQL Server Developer Edition ed Express Edition</span><span class="sxs-lookup"><span data-stu-id="e0db3-167"><a id="manualtcp"></a> Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="e0db3-168">Quando si modificano le impostazioni di connettività di SQL Server, Azure non si attiva automaticamente il protocollo TCP/IP hello per le edizioni Express e SQL Server Developer Edition.</span><span class="sxs-lookup"><span data-stu-id="e0db3-168">When changing SQL Server connectivity settings, Azure does not automatically enable hello TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="e0db3-169">passaggi Hello riportati di seguito viene illustrato come toomanually abilitare TCP/IP in modo che è possibile connettersi in remoto utilizzando un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="e0db3-169">hello steps below explain how toomanually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="e0db3-170">Connettere innanzitutto il computer di SQL Server toohello con desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="e0db3-170">First, connect toohello SQL Server machine with remote desktop.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="e0db3-171">Successivamente, abilitare il protocollo TCP/IP hello con **Gestione configurazione SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e0db3-171">Next, enable hello TCP/IP protocol with **SQL Server Configuration Manager**.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a><span data-ttu-id="e0db3-172">Connettersi con SSMS</span><span class="sxs-lookup"><span data-stu-id="e0db3-172">Connect with SSMS</span></span>

<span data-ttu-id="e0db3-173">Hello passaggi seguenti mostrano come toocreate etichetta di un DNS facoltativo per la macchina virtuale di Azure e connettono con SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="e0db3-173">hello following steps show how toocreate an optional DNS Label for your Azure VM and then connect with SQL Server Management Studio (SSMS).</span></span>

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="e0db3-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e0db3-174">Next Steps</span></span>

<span data-ttu-id="e0db3-175">istruzioni di provisioning toosee insieme a questi passaggi di connettività, vedere [Provisioning di una macchina virtuale di SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="e0db3-175">toosee provisioning instructions along with these connectivity steps, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

<span data-ttu-id="e0db3-176">Per altri argomenti correlati toorunning SQL Server in macchine virtuali di Azure, vedere [SQL Server in macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e0db3-176">For other topics related toorunning SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
