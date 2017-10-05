---
title: "Risoluzione dei problemi di connettività tra macchine virtuali di Azure | Documenti Microsoft"
description: "Informazioni su come risolvere i problemi di connettività tra macchine virtuali di Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: fd0f25c07cb3f385d3e8480ce1e33dec1ae0a214
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a><span data-ttu-id="c7fe7-103">Risoluzione dei problemi di connettività tra macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="c7fe7-103">Troubleshooting connectivity problems between Azure VMs</span></span>

<span data-ttu-id="c7fe7-104">Si potrebbero riscontrare problemi di connettività tra macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-104">You might experience connectivity problems between Azure VMs.</span></span> <span data-ttu-id="c7fe7-105">Questo articolo illustra la procedura per risolvere questo tipo di problema.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a><span data-ttu-id="c7fe7-106">Sintomo</span><span class="sxs-lookup"><span data-stu-id="c7fe7-106">Symptom</span></span>

<span data-ttu-id="c7fe7-107">Una macchina virtuale di Azure non è possibile connettersi a un'altra macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-107">An Azure VM cannot connect to another Azure VM.</span></span>

## <a name="troubleshooting-guidance"></a><span data-ttu-id="c7fe7-108">Guida alla risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="c7fe7-108">Troubleshooting guidance</span></span> 

1. [<span data-ttu-id="c7fe7-109">Controllare se NIC non è configurato correttamente</span><span class="sxs-lookup"><span data-stu-id="c7fe7-109">Check if NIC is misconfigured</span></span>](#step-1-check-if-nic-is-misconfigured)
2. [<span data-ttu-id="c7fe7-110">Verificare se il traffico di rete è bloccato da NSG o UDR</span><span class="sxs-lookup"><span data-stu-id="c7fe7-110">Check if network traffic is blocked by NSG or UDR</span></span>](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [<span data-ttu-id="c7fe7-111">Verificare se il traffico di rete è bloccato dal firewall della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c7fe7-111">Check if network traffic is blocked by VM firewall</span></span>](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [<span data-ttu-id="c7fe7-112">Controllare se un'applicazione o un servizio della macchina virtuale sono in ascolto sulla porta</span><span class="sxs-lookup"><span data-stu-id="c7fe7-112">Check whether VM app or service is listening on the port</span></span>](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [<span data-ttu-id="c7fe7-113">Controllare se il problema è causato dall'architettura SNAT</span><span class="sxs-lookup"><span data-stu-id="c7fe7-113">Check whether the problem is caused by SNAT</span></span>](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [<span data-ttu-id="c7fe7-114">Controllare se il traffico è bloccato da ACL per la macchina virtuale classica</span><span class="sxs-lookup"><span data-stu-id="c7fe7-114">Check whether traffic is blocked by ACLs for the classic VM</span></span>](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [<span data-ttu-id="c7fe7-115">Controllare che l'endpoint per la macchina virtuale classica sia stato creato</span><span class="sxs-lookup"><span data-stu-id="c7fe7-115">Check whether the endpoint is created for the classic VM</span></span>](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [<span data-ttu-id="c7fe7-116">Impossibile connettersi a una condivisione di rete VM</span><span class="sxs-lookup"><span data-stu-id="c7fe7-116">Unable to connect to a VM network share</span></span>](#step-8-unable-to-connect-to-a-vm-network-share)
9. [<span data-ttu-id="c7fe7-117">Connettività tra reti tra reti virtuali</span><span class="sxs-lookup"><span data-stu-id="c7fe7-117">Inter-Vnet connectivity</span></span>](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a><span data-ttu-id="c7fe7-118">Passaggi per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="c7fe7-118">Troubleshooting steps</span></span>

<span data-ttu-id="c7fe7-119">Seguire questa procedura per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-119">Follow these steps to troubleshoot the problem.</span></span> <span data-ttu-id="c7fe7-120">Controllare se il problema è risolto dopo ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-120">Check whether the problem is resolved after each step.</span></span> 

### <a name="step-1-check-if-nic-is-misconfigured"></a><span data-ttu-id="c7fe7-121">Passaggio 1: Verificare se NIC non è configurato correttamente</span><span class="sxs-lookup"><span data-stu-id="c7fe7-121">Step 1: Check if NIC is misconfigured</span></span>

<span data-ttu-id="c7fe7-122">Seguire [come reimpostare l'interfaccia di rete per la macchina virtuale Windows Azure](../virtual-machines/windows/reset-network-interface.md).</span><span class="sxs-lookup"><span data-stu-id="c7fe7-122">Follow [How to reset network interface for Azure Windows VM](../virtual-machines/windows/reset-network-interface.md).</span></span> 

<span data-ttu-id="c7fe7-123">Se il problema si verifica dopo aver modificato l'interfaccia di rete, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="c7fe7-123">If the problem occurs after you modify the network interface (NIC), follow these steps:</span></span>

<span data-ttu-id="c7fe7-124">**Macchine virtuali multi-NIC**</span><span class="sxs-lookup"><span data-stu-id="c7fe7-124">**Mulit-NIC VMs**</span></span>

1. <span data-ttu-id="c7fe7-125">Aggiungere un NIC.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-125">Add a NIC.</span></span>
2. <span data-ttu-id="c7fe7-126">Risolvere i problemi nella scheda di rete non valida o rimuovere una scheda di rete non valido.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-126">Fix the problems in the bad NIC or remove bad NIC.</span></span>  <span data-ttu-id="c7fe7-127">Readd quindi la scheda NIC.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-127">Then readd the NIC.</span></span>

<span data-ttu-id="c7fe7-128">Per altre informazioni, vedere [Aggiungere o rimuovere interfacce di rete da macchine virtuali](virtual-network-network-interface-vm.md).</span><span class="sxs-lookup"><span data-stu-id="c7fe7-128">For more information, see [Add network interfaces to or remove from virtual machines](virtual-network-network-interface-vm.md).</span></span>

<span data-ttu-id="c7fe7-129">**Macchina virtuale con una sola scheda di rete**</span><span class="sxs-lookup"><span data-stu-id="c7fe7-129">**Single-NIC VM**</span></span> 

- [<span data-ttu-id="c7fe7-130">Ridistribuire una VM Windows</span><span class="sxs-lookup"><span data-stu-id="c7fe7-130">Redeploy Windows VM</span></span>](../virtual-machines/windows/redeploy-to-new-node.md)
- [<span data-ttu-id="c7fe7-131">Ridistribuire una VM Linux</span><span class="sxs-lookup"><span data-stu-id="c7fe7-131">Redeploy Linux VM</span></span>](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a><span data-ttu-id="c7fe7-132">Passaggio 2: Verificare se il traffico di rete è bloccato da NSG o UDR</span><span class="sxs-lookup"><span data-stu-id="c7fe7-132">Step 2: Check if network traffic is blocked by NSG or UDR</span></span>

<span data-ttu-id="c7fe7-133">Utilizzare [del flusso di rete IP Watcher verificare](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG flusso registrazione](../network-watcher/network-watcher-nsg-flow-logging-overview.md) per identificare se è presente un gruppo di sicurezza di rete o di una Route definite dall'utente che interferisce con il flusso del traffico.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-133">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) to identify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span>

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a><span data-ttu-id="c7fe7-134">Passaggio 3: Verificare se il traffico di rete è bloccato dal firewall della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c7fe7-134">Step 3: Check if network traffic is blocked by VM firewall</span></span>

<span data-ttu-id="c7fe7-135">Disattivare il firewall, quindi testare i risultati.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-135">Disable the firewall, and then test the result.</span></span> <span data-ttu-id="c7fe7-136">Se il problema viene risolto, verificare le impostazioni del firewall e abilitare di nuovo.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-136">If the problem is resolved, validate the settings in the firewall and re-enable.</span></span>

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-the-port"></a><span data-ttu-id="c7fe7-137">Passaggio 4: Controllare se un'applicazione o un servizio della macchina virtuale sono in ascolto sulla porta</span><span class="sxs-lookup"><span data-stu-id="c7fe7-137">Step 4: Check whether VM app or service is listening on the port</span></span>

<span data-ttu-id="c7fe7-138">È possibile utilizzare uno dei metodi seguenti per controllare se applicazione della macchina virtuale o il servizio è in attesa sulla porta</span><span class="sxs-lookup"><span data-stu-id="c7fe7-138">You can use one of the following methods to check whether VM Application or Service is listening on the port</span></span>

- <span data-ttu-id="c7fe7-139">Eseguire i comandi seguenti per verificare se il server è in ascolto su quella porta.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-139">Run the following commands to check whether the server is listening on that port.</span></span>

<span data-ttu-id="c7fe7-140">**VM Windows**</span><span class="sxs-lookup"><span data-stu-id="c7fe7-140">**Windows VM**</span></span>

    netstat –ano

<span data-ttu-id="c7fe7-141">**VM Linux**</span><span class="sxs-lookup"><span data-stu-id="c7fe7-141">**Linux VM**</span></span>

    netstat -l

- <span data-ttu-id="c7fe7-142">Eseguire il **Telnet** comando nella macchina virtuale a se stessa per testare la porta.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-142">Run the **Telnet** command on the VM to itself to test the port.</span></span> <span data-ttu-id="c7fe7-143">Se il test non riesce, applicazione o il servizio non è configurato per restare in attesa sulla porta.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-143">If the test fails, application or service is not configured to listen on the port.</span></span>

### <a name="step-5-check-whether-the-problem-is-caused-by-snat"></a><span data-ttu-id="c7fe7-144">Passaggio 5: Controllare se il problema è causato dall'architettura SNAT</span><span class="sxs-lookup"><span data-stu-id="c7fe7-144">Step 5: Check whether the problem is caused by SNAT</span></span>

<span data-ttu-id="c7fe7-145">In alcuni scenari, la macchina virtuale è posizionata dietro una soluzione di bilanciamento di carico che presenta una dipendenza sulle risorse all'esterno di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-145">In some scenarios, the VM is placed behind a Load balance solution that has a dependency on resources outside of Azure.</span></span> <span data-ttu-id="c7fe7-146">In questi scenari, eventuali problemi di connessione intermittenti possono essere causati dall'[esaurimento delle porte SNAT](../load-balancer/load-balancer-outbound-connections.md).</span><span class="sxs-lookup"><span data-stu-id="c7fe7-146">In these scenarios, if you experience intermittent connection problems, the problem may be caused by [SNAT port exhaustion](../load-balancer/load-balancer-outbound-connections.md).</span></span> <span data-ttu-id="c7fe7-147">Per risolvere il problema, creare un indirizzo VIP (o ILPIP per classica) per ogni macchina virtuale che si trova dietro il bilanciamento del carico e protetta con ACL o di gruppo.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-147">To resolve the issue, create a VIP (or ILPIP for classic) for each VM that is behind the Load balancer and secure with NSG or ACL.</span></span> 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm"></a><span data-ttu-id="c7fe7-148">Passaggio 6: Controllare se il traffico è bloccato da ACL per la macchina virtuale classica</span><span class="sxs-lookup"><span data-stu-id="c7fe7-148">Step 6: Check whether traffic is blocked by ACLs for the classic VM</span></span>

<span data-ttu-id="c7fe7-149">Offre la possibilità di consentire o negare in modo selettivo il traffico per un endpoint di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-149">An ACL provides the ability to selectively permit or deny traffic for a virtual machine endpoint.</span></span> <span data-ttu-id="c7fe7-150">Per altre informazioni, vedere [Gestire l'elenco di controllo di accesso su un endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span><span class="sxs-lookup"><span data-stu-id="c7fe7-150">For more information, see [Manage the ACL on an endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

### <a name="step-7-check-whether-the-endpoint-is-created-for-the-classic-vm"></a><span data-ttu-id="c7fe7-151">Passaggio 7: Controllare che l'endpoint per la macchina virtuale classica sia stato creato</span><span class="sxs-lookup"><span data-stu-id="c7fe7-151">Step 7: Check whether the endpoint is created for the classic VM</span></span>

<span data-ttu-id="c7fe7-152">Tutte le macchine virtuali create in Azure utilizzando il modello di distribuzione classica possono comunicare automaticamente tramite un canale di rete privata con altre macchine virtuali nella rete virtuale o nello stesso servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-152">All VMs that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="c7fe7-153">Tuttavia, i computer in altre reti virtuali richiedono degli endpoint per indirizzare il traffico di rete in ingresso a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-153">However, computers on other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="c7fe7-154">Per altre informazioni, vedere [Come configurare gli endpoint](../virtual-machines/windows/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="c7fe7-154">For more information, see [How to set up endpoints](../virtual-machines/windows/classic/setup-endpoints.md).</span></span>

### <a name="step-8-unable-to-connect-to-a-vm-network-share"></a><span data-ttu-id="c7fe7-155">Passaggio 8: Impossibile connettersi a una condivisione di rete VM</span><span class="sxs-lookup"><span data-stu-id="c7fe7-155">Step 8: Unable to connect to a VM network share</span></span>

<span data-ttu-id="c7fe7-156">Se non si riesce a connettersi a una condivisione di rete VM, il problema può essere causato da schede di rete non disponibile nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-156">If you are unable to connect to a VM network share, the problem can be caused by unavailable NICs in the VM.</span></span> <span data-ttu-id="c7fe7-157">Per eliminare le schede di interfaccia non disponibili, vedere [Eliminare le schede di interfaccia non disponibili](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span><span class="sxs-lookup"><span data-stu-id="c7fe7-157">To delete the unavailable NICs, see [How to delete the unavailable NICs](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span></span>

### <a name="step-9-inter-vnet-connectivity"></a><span data-ttu-id="c7fe7-158">Passaggio 9: Connettività di rete virtuale tra</span><span class="sxs-lookup"><span data-stu-id="c7fe7-158">Step 9: Inter-Vnet connectivity</span></span>

<span data-ttu-id="c7fe7-159">Utilizzare [del flusso di rete IP Watcher verificare](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG flusso registrazione](../network-watcher/network-watcher-nsg-flow-logging-overview.md) per identificare se è presente un gruppo di sicurezza di rete o di una Route definite dall'utente che interferisce con il flusso del traffico.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-159">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) to identify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span> <span data-ttu-id="c7fe7-160">È inoltre possibile convalidare la configurazione della rete virtuale tra [qui](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span><span class="sxs-lookup"><span data-stu-id="c7fe7-160">You can also validate your Inter-Vnet configuration [here](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span></span>

### <a name="need-help-contact-support"></a><span data-ttu-id="c7fe7-161">Richiesta di assistenza</span><span class="sxs-lookup"><span data-stu-id="c7fe7-161">Need help?</span></span> <span data-ttu-id="c7fe7-162">Contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-162">Contact support.</span></span>
<span data-ttu-id="c7fe7-163">Se si necessita ancora di assistenza, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) per ottenere una rapida risoluzione del problema.</span><span class="sxs-lookup"><span data-stu-id="c7fe7-163">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>