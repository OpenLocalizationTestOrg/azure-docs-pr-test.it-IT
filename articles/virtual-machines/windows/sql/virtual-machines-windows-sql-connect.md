---
title: Connettersi a una macchina virtuale di SQL Server (Gestione risorse) | Documentazione Microsoft
description: Informazioni su come connettersi a SQL Server in esecuzione su una macchina virtuale di Azure. In questo argomento viene usato il modello di distribuzione classica. Gli scenari variano a seconda della configurazione di rete e della posizione del client.
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
ms.openlocfilehash: 67ba43f9456bbeffbf602067586143c4c68af672
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-a-sql-server-virtual-machine-on-azure-resource-manager"></a><span data-ttu-id="a69e3-105">Connettersi a una macchina virtuale di SQL Server in Azure (Gestione risorse)</span><span class="sxs-lookup"><span data-stu-id="a69e3-105">Connect to a SQL Server Virtual Machine on Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a69e3-106">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="a69e3-106">Resource Manager</span></span>](virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="a69e3-107">Classico</span><span class="sxs-lookup"><span data-stu-id="a69e3-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="a69e3-108">Overview</span><span class="sxs-lookup"><span data-stu-id="a69e3-108">Overview</span></span>

<span data-ttu-id="a69e3-109">Questo argomento descrive la modalità di connessione all'istanza di SQL Server in esecuzione su una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a69e3-109">This topic describes how to connect to your SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="a69e3-110">Illustra alcuni [scenari di connettività generali](#connection-scenarios) e quindi descrive la [procedura dettagliata per la configurazione della connettività di SQL Server in una macchina virtuale di Azure](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="a69e3-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="a69e3-111">Per una procedura dettagliata completa del provisioning e della connettività, vedere [Provisioning di una macchina virtuale di SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="a69e3-111">If you would rather have a full walk-through of both provisioning and connectivity, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="a69e3-112">Scenari di connessione</span><span class="sxs-lookup"><span data-stu-id="a69e3-112">Connection scenarios</span></span>

<span data-ttu-id="a69e3-113">La modalità di connessione di un client a SQL Server in esecuzione in una macchina virtuale varia a seconda della posizione del client e della configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="a69e3-113">The way a client connects to SQL Server running on a Virtual Machine differs depending on the location of the client and the networking configuration.</span></span>

<span data-ttu-id="a69e3-114">Se si esegue il provisioning di una VM di SQL Server nel portale di Azure, è possibile specificare il tipo di **connettività SQL**.</span><span class="sxs-lookup"><span data-stu-id="a69e3-114">If you provision a SQL Server VM in the Azure portal, you have the option of specifying the type of **SQL connectivity**.</span></span>

![Opzione di connettività SQL pubblica durante il provisioning](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

<span data-ttu-id="a69e3-116">Le opzioni per la connettività sono:</span><span class="sxs-lookup"><span data-stu-id="a69e3-116">Your options for connectivity include:</span></span>

| <span data-ttu-id="a69e3-117">Opzione</span><span class="sxs-lookup"><span data-stu-id="a69e3-117">Option</span></span> | <span data-ttu-id="a69e3-118">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a69e3-118">Description</span></span> |
|---|---|
| <span data-ttu-id="a69e3-119">**Pubblica**</span><span class="sxs-lookup"><span data-stu-id="a69e3-119">**Public**</span></span> | <span data-ttu-id="a69e3-120">Connettersi a SQL Server tramite Internet</span><span class="sxs-lookup"><span data-stu-id="a69e3-120">Connect to SQL Server over the internet</span></span> |
| <span data-ttu-id="a69e3-121">**Privata**</span><span class="sxs-lookup"><span data-stu-id="a69e3-121">**Private**</span></span> | <span data-ttu-id="a69e3-122">Connettersi a SQL Server nella stessa rete virtuale</span><span class="sxs-lookup"><span data-stu-id="a69e3-122">Connect to SQL Server in the same virtual network</span></span> |
| <span data-ttu-id="a69e3-123">**Locale**</span><span class="sxs-lookup"><span data-stu-id="a69e3-123">**Local**</span></span> | <span data-ttu-id="a69e3-124">Connettersi a SQL Server localmente sulla stessa macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a69e3-124">Connect to SQL Server locally on the same virtual machine</span></span> | 

<span data-ttu-id="a69e3-125">Le sezioni seguenti illustrano le opzioni **Pubblica** e **Privata** in modo più dettagliato.</span><span class="sxs-lookup"><span data-stu-id="a69e3-125">The following sections explain the **Public** and **Private** options in more detail.</span></span>

## <a name="connect-to-sql-server-over-the-internet"></a><span data-ttu-id="a69e3-126">Connettersi a SQL Server tramite Internet</span><span class="sxs-lookup"><span data-stu-id="a69e3-126">Connect to SQL Server over the Internet</span></span>

<span data-ttu-id="a69e3-127">Se ci si vuole connettere al motore di database di SQL Server da Internet, durante il provisioning selezionare il tipo di **Connettività SQL** **Pubblica** nel portale.</span><span class="sxs-lookup"><span data-stu-id="a69e3-127">If you want to connect to your SQL Server database engine from the Internet, select **Public** for the **SQL connectivity** type in the portal during provisioning.</span></span> <span data-ttu-id="a69e3-128">Il portale esegue automaticamente la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a69e3-128">The portal automatically does the following steps:</span></span>

* <span data-ttu-id="a69e3-129">Abilita il protocollo TCP/IP per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a69e3-129">Enables the TCP/IP protocol for SQL Server.</span></span>
* <span data-ttu-id="a69e3-130">Configura una regola del firewall per l'apertura della porta TCP di SQL Server (valore predefinito 1433).</span><span class="sxs-lookup"><span data-stu-id="a69e3-130">Configures a firewall rule to open the SQL Server TCP port (default 1433).</span></span>
* <span data-ttu-id="a69e3-131">Abilita l'autenticazione di SQL Server, necessaria per l'accesso pubblico.</span><span class="sxs-lookup"><span data-stu-id="a69e3-131">Enables SQL Server Authentication, required for public access.</span></span>
* <span data-ttu-id="a69e3-132">Configura il gruppo di sicurezza di rete nella VM su tutto il traffico TCP sulla porta di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a69e3-132">Configures the network security group on the VM to all TCP traffic on the SQL Server port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a69e3-133">Le immagini delle macchine virtuali per SQL Server Express Edition e SQL Server Developer Edition non abilitano automaticamente il protocollo TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="a69e3-133">The virtual machine images for the SQL Server Developer and Express editions do not automatically enable the TCP/IP protocol.</span></span> <span data-ttu-id="a69e3-134">Per Developer Edition ed Express Edition è necessario usare Gestione configurazione SQL Server per [abilitare manualmente il protocollo TCP/IP](#manualtcp) dopo avere creato la VM.</span><span class="sxs-lookup"><span data-stu-id="a69e3-134">For Developer and Express editions, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#manualtcp) after creating the VM.</span></span>

<span data-ttu-id="a69e3-135">Tutti i client con accesso a Internet potranno connettersi all'istanza di SQL Server specificando l'indirizzo IP pubblico della macchina virtuale o l'eventuale etichetta DNS assegnata a tale indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="a69e3-135">Any client with internet access can connect to the SQL Server instance by specifying either the public IP address of the virtual machine or any DNS label assigned to that IP address.</span></span> <span data-ttu-id="a69e3-136">Se la porta di SQL Server è 1433, non è necessario specificarla nella stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="a69e3-136">If the SQL Server port is 1433, you do not need to specify it in the connection string.</span></span> <span data-ttu-id="a69e3-137">La stringa di connessione seguente consente la connessione a una VM SQL con etichetta DNS corrispondente a `sqlvmlabel.eastus.cloudapp.azure.com` tramite l'autenticazione SQL (è anche possibile usare l'indirizzo IP pubblico).</span><span class="sxs-lookup"><span data-stu-id="a69e3-137">The following connection string connects to a SQL VM with a DNS label of `sqlvmlabel.eastus.cloudapp.azure.com` using SQL Authentication (you could also use the public IP address).</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

<span data-ttu-id="a69e3-138">Sebbene in questo modo venga abilitata la connettività per i client tramite Internet, ciò non significa che chiunque può connettersi all'istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a69e3-138">Although this enables connectivity for clients over the internet, this does not imply that anyone can connect to your SQL Server.</span></span> <span data-ttu-id="a69e3-139">I client esterni dovranno disporre del nome utente e della password corretti.</span><span class="sxs-lookup"><span data-stu-id="a69e3-139">Outside clients have to the correct username and password.</span></span> <span data-ttu-id="a69e3-140">Per maggiore sicurezza, tuttavia, è possibile evitare la porta 1433 nota.</span><span class="sxs-lookup"><span data-stu-id="a69e3-140">However, for additional security, you can avoid the well-known port 1433.</span></span> <span data-ttu-id="a69e3-141">Se, ad esempio, SQL Server è configurato per l'ascolto sulla porta 1500 e sono state stabilite regole del gruppo di sicurezza di rete e del firewall corrette, è possibile connettersi aggiungendo il numero di porta al nome del server.</span><span class="sxs-lookup"><span data-stu-id="a69e3-141">For example, if you configured SQL Server to listen on port 1500 and established proper firewall and network security group rules, you could connect by appending the port number to the Server name.</span></span> <span data-ttu-id="a69e3-142">L'esempio seguente modifica il precedente tramite l'aggiunta del numero di porta personalizzato **1500** al nome del server:</span><span class="sxs-lookup"><span data-stu-id="a69e3-142">The following example alters the previous one by adding a custom port number, **1500**, to the server name:</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> <span data-ttu-id="a69e3-143">Quando si invia una query a SQL Server in una VM via Internet, tutti i dati in uscita dal centro dati di Azure sono soggetti ai normali [prezzi dei trasferimenti di dati in uscita](https://azure.microsoft.com/pricing/details/data-transfers/).</span><span class="sxs-lookup"><span data-stu-id="a69e3-143">When you query SQL Server in a VM over the internet, all outgoing data from the Azure datacenter is subject to normal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>

## <a name="connect-to-sql-server-within-a-virtual-network"></a><span data-ttu-id="a69e3-144">Connettersi a SQL Server all'interno di una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="a69e3-144">Connect to SQL Server within a virtual network</span></span>

<span data-ttu-id="a69e3-145">Se nel portale si sceglie **Privata** in **Connettività SQL**, Azure configura la maggior parte delle impostazioni in modo identico rispetto a **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="a69e3-145">When you choose **Private** for the **SQL connectivity** type in the portal, Azure configures most of the settings identical to **Public**.</span></span> <span data-ttu-id="a69e3-146">L'unica differenza è l'assenza di una regola del gruppo di sicurezza di rete che consente il traffico esterno sulla porta di SQL Server (valore predefinito 1433).</span><span class="sxs-lookup"><span data-stu-id="a69e3-146">The one difference is that there is no network security group rule to allow outside traffic on the SQL Server port (default 1433).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a69e3-147">Le immagini delle macchine virtuali per SQL Server Express Edition e SQL Server Developer Edition non abilitano automaticamente il protocollo TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="a69e3-147">The virtual machine images for the SQL Server Developer and Express editions do not automatically enable the TCP/IP protocol.</span></span> <span data-ttu-id="a69e3-148">Per Developer Edition ed Express Edition è necessario usare Gestione configurazione SQL Server per [abilitare manualmente il protocollo TCP/IP](#manualtcp) dopo avere creato la VM.</span><span class="sxs-lookup"><span data-stu-id="a69e3-148">For Developer and Express editions, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#manualtcp) after creating the VM.</span></span>

<span data-ttu-id="a69e3-149">La connettività privata viene spesso usata in combinazione con una [rete virtuale](../../../virtual-network/virtual-networks-overview.md), che consente diversi scenari.</span><span class="sxs-lookup"><span data-stu-id="a69e3-149">Private connectivity is often used in conjunction with [Virtual Network](../../../virtual-network/virtual-networks-overview.md), which enables several scenarios.</span></span> <span data-ttu-id="a69e3-150">È possibile connettere le VM nella stessa rete virtuale, anche se si trovano in gruppi di risorse diversi.</span><span class="sxs-lookup"><span data-stu-id="a69e3-150">You can connect VMs in the same virtual network, even if those VMs exist in different resource groups.</span></span> <span data-ttu-id="a69e3-151">Con una [VPN da sito a sito](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)è possibile creare un'architettura ibrida che connette le macchine virtuali a computer e reti locali.</span><span class="sxs-lookup"><span data-stu-id="a69e3-151">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="a69e3-152">Le reti virtuali consentono inoltre di aggiungere le macchine virtuali di Azure a un dominio.</span><span class="sxs-lookup"><span data-stu-id="a69e3-152">Virtual networks also enable     you to join your Azure VMs to a domain.</span></span> <span data-ttu-id="a69e3-153">Si tratta dell'unico modo per usare l'autenticazione di Windows per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a69e3-153">This is the only way to use Windows Authentication to SQL Server.</span></span> <span data-ttu-id="a69e3-154">Gli altri scenari di connessione richiedono l'autenticazione SQL con nomi utente e password.</span><span class="sxs-lookup"><span data-stu-id="a69e3-154">The other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="a69e3-155">Presupponendo che il DNS sia stato configurato nella rete virtuale, è possibile connettersi all'istanza di SQL Server specificando il nome computer della VM di SQL Server nella stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="a69e3-155">Assuming that you have configured DNS in your virtual network, you can connect to your SQL Server instance by specifying the SQL Server VM computer name in the connection string.</span></span> <span data-ttu-id="a69e3-156">L'esempio seguente presuppone che sia stata configurata anche l'autenticazione di Windows e che all'utente sia stato concesso l'accesso all'istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a69e3-156">The following example also assumes that Windows Authentication has also been configured and that the user has been granted access to the SQL Server instance.</span></span>

```
Server=mysqlvm;Integrated Security=true
```

## <span data-ttu-id="a69e3-157"><a id="change"></a>Modificare le impostazioni di connettività SQL</span><span class="sxs-lookup"><span data-stu-id="a69e3-157"><a id="change"></a> Change SQL connectivity settings</span></span>

<span data-ttu-id="a69e3-158">È possibile modificare le impostazioni di connettività per la macchina virtuale di SQL Server nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a69e3-158">You can change the connectivity settings for your SQL Server virtual machine in the Azure portal.</span></span>

1. <span data-ttu-id="a69e3-159">Nel portale di Azure selezionare **Macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="a69e3-159">In the Azure portal, select **Virtual Machines**.</span></span>

2. <span data-ttu-id="a69e3-160">Selezionare la VM di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a69e3-160">Select your SQL Server VM.</span></span>

3. <span data-ttu-id="a69e3-161">In **Impostazioni** fare clic su **Configurazione di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a69e3-161">Under **Settings**, click **SQL Server configuration**.</span></span>

4. <span data-ttu-id="a69e3-162">Modificare il valore di **Livello di connettività SQL** sull'impostazione necessaria.</span><span class="sxs-lookup"><span data-stu-id="a69e3-162">Change the **SQL connectivity level** to your required setting.</span></span> <span data-ttu-id="a69e3-163">Facoltativamente, è possibile usare quest'area per modificare la porta di SQL Server o le impostazioni di autenticazione SQL.</span><span class="sxs-lookup"><span data-stu-id="a69e3-163">You can optionally use this area to change the SQL Server port or the SQL Authentication settings.</span></span>

   ![Modificare la connettività SQL](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. <span data-ttu-id="a69e3-165">Attendere qualche minuto che l'aggiornamento venga completato.</span><span class="sxs-lookup"><span data-stu-id="a69e3-165">Wait several minutes for the update to complete.</span></span>

   ![Notifica dell'aggiornamento della VM SQL](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <span data-ttu-id="a69e3-167"><a id="manualtcp"></a>Abilitare TCP/IP per SQL Server Developer Edition ed Express Edition</span><span class="sxs-lookup"><span data-stu-id="a69e3-167"><a id="manualtcp"></a> Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="a69e3-168">Quando si modificano le impostazioni di connettività di SQL Server, per SQL Server Developer Edition ed Express Edition Azure non abilita automaticamente il protocollo TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="a69e3-168">When changing SQL Server connectivity settings, Azure does not automatically enable the TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="a69e3-169">La procedura seguente illustra come abilitare manualmente TCP/IP per potersi connettere in remoto in base all'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="a69e3-169">The steps below explain how to manually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="a69e3-170">Connettersi prima al computer di SQL Server tramite Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="a69e3-170">First, connect to the SQL Server machine with remote desktop.</span></span>

> [!INCLUDE [Connect to SQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="a69e3-171">Abilitare quindi il protocollo TCP/IP con **Gestione configurazione SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a69e3-171">Next, enable the TCP/IP protocol with **SQL Server Configuration Manager**.</span></span>

> [!INCLUDE [Connect to SQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a><span data-ttu-id="a69e3-172">Connettersi con SSMS</span><span class="sxs-lookup"><span data-stu-id="a69e3-172">Connect with SSMS</span></span>

<span data-ttu-id="a69e3-173">La procedura seguente illustra come creare un'etichetta DNS facoltativa per la VM di Azure e quindi come connettersi con SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="a69e3-173">The following steps show how to create an optional DNS Label for your Azure VM and then connect with SQL Server Management Studio (SSMS).</span></span>

[!INCLUDE [Connect to SQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="a69e3-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a69e3-174">Next Steps</span></span>

<span data-ttu-id="a69e3-175">Per la procedura di configurazione della connettività e del provisioning, vedere [Provisioning di una macchina virtuale di SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="a69e3-175">To see provisioning instructions along with these connectivity steps, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

<span data-ttu-id="a69e3-176">Per altri argomenti relativi all'esecuzione di SQL Server nelle macchine virtuali di Azure, vedere [SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a69e3-176">For other topics related to running SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>