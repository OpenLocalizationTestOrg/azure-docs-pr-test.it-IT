---
title: "problemi di connettività aaaTroubleshooting tra macchine virtuali di Azure | Documenti Microsoft"
description: "Informazioni su come tooTroubleshoot hello problemi di connettività tra macchine virtuali di Azure."
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
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a><span data-ttu-id="a1723-103">Risoluzione dei problemi di connettività tra macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="a1723-103">Troubleshooting connectivity problems between Azure VMs</span></span>

<span data-ttu-id="a1723-104">Si potrebbero riscontrare problemi di connettività tra macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="a1723-104">You might experience connectivity problems between Azure VMs.</span></span> <span data-ttu-id="a1723-105">Questo articolo fornisce la risoluzione dei problemi toohelp passaggi risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="a1723-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a><span data-ttu-id="a1723-106">Sintomo</span><span class="sxs-lookup"><span data-stu-id="a1723-106">Symptom</span></span>

<span data-ttu-id="a1723-107">Una macchina virtuale di Azure non può connettersi tooanother macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a1723-107">An Azure VM cannot connect tooanother Azure VM.</span></span>

## <a name="troubleshooting-guidance"></a><span data-ttu-id="a1723-108">Guida alla risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="a1723-108">Troubleshooting guidance</span></span> 

1. [<span data-ttu-id="a1723-109">Controllare se NIC non è configurato correttamente</span><span class="sxs-lookup"><span data-stu-id="a1723-109">Check if NIC is misconfigured</span></span>](#step-1-check-if-nic-is-misconfigured)
2. [<span data-ttu-id="a1723-110">Verificare se il traffico di rete è bloccato da NSG o UDR</span><span class="sxs-lookup"><span data-stu-id="a1723-110">Check if network traffic is blocked by NSG or UDR</span></span>](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [<span data-ttu-id="a1723-111">Verificare se il traffico di rete è bloccato dal firewall della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a1723-111">Check if network traffic is blocked by VM firewall</span></span>](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [<span data-ttu-id="a1723-112">Controllare se VM app o un servizio è in attesa sulla porta hello</span><span class="sxs-lookup"><span data-stu-id="a1723-112">Check whether VM app or service is listening on hello port</span></span>](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [<span data-ttu-id="a1723-113">Controllare se il problema di hello è causato da SNAT</span><span class="sxs-lookup"><span data-stu-id="a1723-113">Check whether hello problem is caused by SNAT</span></span>](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [<span data-ttu-id="a1723-114">Verifica se il traffico viene bloccato per gli elenchi ACL per hello VM classico</span><span class="sxs-lookup"><span data-stu-id="a1723-114">Check whether traffic is blocked by ACLs for hello classic VM</span></span>](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [<span data-ttu-id="a1723-115">Controllare se viene creato endpoint hello per hello VM classico</span><span class="sxs-lookup"><span data-stu-id="a1723-115">Check whether hello endpoint is created for hello classic VM</span></span>](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [<span data-ttu-id="a1723-116">Condivisione di rete VM non è possibile tooconnect tooa</span><span class="sxs-lookup"><span data-stu-id="a1723-116">Unable tooconnect tooa VM network share</span></span>](#step-8-unable-to-connect-to-a-vm-network-share)
9. [<span data-ttu-id="a1723-117">Connettività tra reti tra reti virtuali</span><span class="sxs-lookup"><span data-stu-id="a1723-117">Inter-Vnet connectivity</span></span>](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a><span data-ttu-id="a1723-118">Passaggi per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="a1723-118">Troubleshooting steps</span></span>

<span data-ttu-id="a1723-119">Seguire questi problema hello tootroubleshoot di passaggi.</span><span class="sxs-lookup"><span data-stu-id="a1723-119">Follow these steps tootroubleshoot hello problem.</span></span> <span data-ttu-id="a1723-120">Controllare se il problema di hello è risolto dopo ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="a1723-120">Check whether hello problem is resolved after each step.</span></span> 

### <a name="step-1-check-if-nic-is-misconfigured"></a><span data-ttu-id="a1723-121">Passaggio 1: Verificare se NIC non è configurato correttamente</span><span class="sxs-lookup"><span data-stu-id="a1723-121">Step 1: Check if NIC is misconfigured</span></span>

<span data-ttu-id="a1723-122">Seguire [come tooreset interfaccia di rete per la macchina virtuale Windows Azure](../virtual-machines/windows/reset-network-interface.md).</span><span class="sxs-lookup"><span data-stu-id="a1723-122">Follow [How tooreset network interface for Azure Windows VM](../virtual-machines/windows/reset-network-interface.md).</span></span> 

<span data-ttu-id="a1723-123">Se il problema di hello si verifica dopo aver modificato l'interfaccia di rete (NIC) hello, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="a1723-123">If hello problem occurs after you modify hello network interface (NIC), follow these steps:</span></span>

<span data-ttu-id="a1723-124">**Macchine virtuali multi-NIC**</span><span class="sxs-lookup"><span data-stu-id="a1723-124">**Mulit-NIC VMs**</span></span>

1. <span data-ttu-id="a1723-125">Aggiungere un NIC.</span><span class="sxs-lookup"><span data-stu-id="a1723-125">Add a NIC.</span></span>
2. <span data-ttu-id="a1723-126">Risolvere i problemi di hello nelle hello errato NIC o rimuovere errato scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="a1723-126">Fix hello problems in hello bad NIC or remove bad NIC.</span></span>  <span data-ttu-id="a1723-127">Quindi readd hello scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="a1723-127">Then readd hello NIC.</span></span>

<span data-ttu-id="a1723-128">Per ulteriori informazioni, vedere [tooor interfacce di rete Aggiungi rimuovere dalle macchine virtuali](virtual-network-network-interface-vm.md).</span><span class="sxs-lookup"><span data-stu-id="a1723-128">For more information, see [Add network interfaces tooor remove from virtual machines](virtual-network-network-interface-vm.md).</span></span>

<span data-ttu-id="a1723-129">**Macchina virtuale con una sola scheda di rete**</span><span class="sxs-lookup"><span data-stu-id="a1723-129">**Single-NIC VM**</span></span> 

- [<span data-ttu-id="a1723-130">Ridistribuire una VM Windows</span><span class="sxs-lookup"><span data-stu-id="a1723-130">Redeploy Windows VM</span></span>](../virtual-machines/windows/redeploy-to-new-node.md)
- [<span data-ttu-id="a1723-131">Ridistribuire una VM Linux</span><span class="sxs-lookup"><span data-stu-id="a1723-131">Redeploy Linux VM</span></span>](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a><span data-ttu-id="a1723-132">Passaggio 2: Verificare se il traffico di rete è bloccato da NSG o UDR</span><span class="sxs-lookup"><span data-stu-id="a1723-132">Step 2: Check if network traffic is blocked by NSG or UDR</span></span>

<span data-ttu-id="a1723-133">Utilizzare [del flusso di rete IP Watcher verificare](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG flusso registrazione](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify se è presente un gruppo di sicurezza di rete o di una Route definite dall'utente che interferisce con il flusso del traffico.</span><span class="sxs-lookup"><span data-stu-id="a1723-133">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span>

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a><span data-ttu-id="a1723-134">Passaggio 3: Verificare se il traffico di rete è bloccato dal firewall della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a1723-134">Step 3: Check if network traffic is blocked by VM firewall</span></span>

<span data-ttu-id="a1723-135">Disattivare il firewall hello e quindi il risultato di hello del test.</span><span class="sxs-lookup"><span data-stu-id="a1723-135">Disable hello firewall, and then test hello result.</span></span> <span data-ttu-id="a1723-136">Se viene risolto il problema di hello, convalidare le impostazioni di hello firewall hello e abilitare di nuovo.</span><span class="sxs-lookup"><span data-stu-id="a1723-136">If hello problem is resolved, validate hello settings in hello firewall and re-enable.</span></span>

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a><span data-ttu-id="a1723-137">Passaggio 4: Controllare se VM app o un servizio è in attesa sulla porta hello</span><span class="sxs-lookup"><span data-stu-id="a1723-137">Step 4: Check whether VM app or service is listening on hello port</span></span>

<span data-ttu-id="a1723-138">È possibile utilizzare uno dei seguenti metodi toocheck se l'applicazione della macchina virtuale o il servizio è in ascolto sulla porta hello hello</span><span class="sxs-lookup"><span data-stu-id="a1723-138">You can use one of hello following methods toocheck whether VM Application or Service is listening on hello port</span></span>

- <span data-ttu-id="a1723-139">Eseguire hello seguenti comandi toocheck se hello server è in ascolto su tale porta.</span><span class="sxs-lookup"><span data-stu-id="a1723-139">Run hello following commands toocheck whether hello server is listening on that port.</span></span>

<span data-ttu-id="a1723-140">**VM Windows**</span><span class="sxs-lookup"><span data-stu-id="a1723-140">**Windows VM**</span></span>

    netstat –ano

<span data-ttu-id="a1723-141">**VM Linux**</span><span class="sxs-lookup"><span data-stu-id="a1723-141">**Linux VM**</span></span>

    netstat -l

- <span data-ttu-id="a1723-142">Eseguire hello **Telnet** comando hello porta hello tootest tooitself di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a1723-142">Run hello **Telnet** command on hello VM tooitself tootest hello port.</span></span> <span data-ttu-id="a1723-143">Se hello test non riesce, applicazione o il servizio non è configurato toolisten sulla porta hello.</span><span class="sxs-lookup"><span data-stu-id="a1723-143">If hello test fails, application or service is not configured toolisten on hello port.</span></span>

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a><span data-ttu-id="a1723-144">Passaggio 5: Verificare se il problema di hello è causato da SNAT</span><span class="sxs-lookup"><span data-stu-id="a1723-144">Step 5: Check whether hello problem is caused by SNAT</span></span>

<span data-ttu-id="a1723-145">In alcuni scenari, hello VM è posizionato dietro una soluzione di bilanciamento di carico che presenta una dipendenza sulle risorse all'esterno di Azure.</span><span class="sxs-lookup"><span data-stu-id="a1723-145">In some scenarios, hello VM is placed behind a Load balance solution that has a dependency on resources outside of Azure.</span></span> <span data-ttu-id="a1723-146">In questi scenari, se si verificano problemi di connessione intermittenti, hello problema potrebbe essere causato da [esaurimento delle porte SNAT](../load-balancer/load-balancer-outbound-connections.md).</span><span class="sxs-lookup"><span data-stu-id="a1723-146">In these scenarios, if you experience intermittent connection problems, hello problem may be caused by [SNAT port exhaustion](../load-balancer/load-balancer-outbound-connections.md).</span></span> <span data-ttu-id="a1723-147">problema hello tooresolve, creare un VIP (o ILPIP per classica) per ogni macchina virtuale di bilanciamento del carico hello e proteggere con ACL o di gruppo.</span><span class="sxs-lookup"><span data-stu-id="a1723-147">tooresolve hello issue, create a VIP (or ILPIP for classic) for each VM that is behind hello Load balancer and secure with NSG or ACL.</span></span> 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a><span data-ttu-id="a1723-148">Passaggio 6: Verificare se il traffico viene bloccato per gli elenchi ACL per hello classic VM</span><span class="sxs-lookup"><span data-stu-id="a1723-148">Step 6: Check whether traffic is blocked by ACLs for hello classic VM</span></span>

<span data-ttu-id="a1723-149">Un ACL fornisce hello possibilità tooselectively consentire o negare il traffico per un endpoint della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a1723-149">An ACL provides hello ability tooselectively permit or deny traffic for a virtual machine endpoint.</span></span> <span data-ttu-id="a1723-150">Per ulteriori informazioni, vedere [Gestisci hello ACL su un endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span><span class="sxs-lookup"><span data-stu-id="a1723-150">For more information, see [Manage hello ACL on an endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a><span data-ttu-id="a1723-151">Passaggio 7: Verifica se viene creato endpoint hello per hello VM classico</span><span class="sxs-lookup"><span data-stu-id="a1723-151">Step 7: Check whether hello endpoint is created for hello classic VM</span></span>

<span data-ttu-id="a1723-152">Tutte le macchine virtuali create in Azure utilizzando il modello di distribuzione classica hello possono comunicare automaticamente tramite un canale di rete privata con altre macchine virtuali in hello che stesso servizio o della rete virtuale del cloud.</span><span class="sxs-lookup"><span data-stu-id="a1723-152">All VMs that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="a1723-153">Tuttavia, i computer in altre reti virtuali richiedono endpoint toodirect hello rete in ingresso traffico tooa computer macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a1723-153">However, computers on other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="a1723-154">Per ulteriori informazioni, vedere [come tooset degli endpoint](../virtual-machines/windows/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="a1723-154">For more information, see [How tooset up endpoints](../virtual-machines/windows/classic/setup-endpoints.md).</span></span>

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a><span data-ttu-id="a1723-155">Passaggio 8: Condivisione di rete VM tooa tooconnect Impossibile</span><span class="sxs-lookup"><span data-stu-id="a1723-155">Step 8: Unable tooconnect tooa VM network share</span></span>

<span data-ttu-id="a1723-156">Nel caso di condivisione di rete VM non è possibile tooconnect tooa, problema di hello può essere causato da schede di rete non disponibile in hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a1723-156">If you are unable tooconnect tooa VM network share, hello problem can be caused by unavailable NICs in hello VM.</span></span> <span data-ttu-id="a1723-157">toodelete hello schede di rete non disponibile, vedere [come toodelete hello schede di rete non disponibile](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span><span class="sxs-lookup"><span data-stu-id="a1723-157">toodelete hello unavailable NICs, see [How toodelete hello unavailable NICs](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span></span>

### <a name="step-9-inter-vnet-connectivity"></a><span data-ttu-id="a1723-158">Passaggio 9: Connettività di rete virtuale tra</span><span class="sxs-lookup"><span data-stu-id="a1723-158">Step 9: Inter-Vnet connectivity</span></span>

<span data-ttu-id="a1723-159">Utilizzare [del flusso di rete IP Watcher verificare](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG flusso registrazione](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify se è presente un gruppo di sicurezza di rete o di una Route definite dall'utente che interferisce con il flusso del traffico.</span><span class="sxs-lookup"><span data-stu-id="a1723-159">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span> <span data-ttu-id="a1723-160">È inoltre possibile convalidare la configurazione della rete virtuale tra [qui](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span><span class="sxs-lookup"><span data-stu-id="a1723-160">You can also validate your Inter-Vnet configuration [here](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span></span>

### <a name="need-help-contact-support"></a><span data-ttu-id="a1723-161">Richiesta di assistenza</span><span class="sxs-lookup"><span data-stu-id="a1723-161">Need help?</span></span> <span data-ttu-id="a1723-162">Contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="a1723-162">Contact support.</span></span>
<span data-ttu-id="a1723-163">Se è ancora necessario della Guida, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.</span><span class="sxs-lookup"><span data-stu-id="a1723-163">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
