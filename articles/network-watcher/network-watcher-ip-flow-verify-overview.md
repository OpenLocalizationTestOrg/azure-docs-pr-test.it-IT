---
title: flusso tooIP aaaIntroduction verificare in Watcher di rete di Azure | Documenti Microsoft
description: "Questa pagina viene fornita una panoramica di hello IP Watcher di rete di flusso di verificare la funzionalità"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="62b1f-103">Flusso tooIP introduzione verificare in Watcher di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="62b1f-103">Introduction tooIP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="62b1f-104">Flusso IP verificare controlla se un pacchetto è consentito o negato tooor da una macchina virtuale in base alle informazioni di 5 tuple.</span><span class="sxs-lookup"><span data-stu-id="62b1f-104">IP flow verify checks if a packet is allowed or denied tooor from a virtual machine based on 5-tuple information.</span></span> <span data-ttu-id="62b1f-105">Tali informazioni sono costituite da direzione, protocollo, indirizzo IP locale, indirizzo IP remoto, porta locale e porta remota.</span><span class="sxs-lookup"><span data-stu-id="62b1f-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="62b1f-106">Se i pacchetti hello viene negato da un gruppo di sicurezza, viene restituito il nome di hello della regola hello negato pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="62b1f-106">If hello packet is denied by a security group, hello name of hello rule that denied hello packet is returned.</span></span> <span data-ttu-id="62b1f-107">Mentre è possibile scegliere qualsiasi indirizzo IP di origine o destinazione, questa funzionalità consente agli amministratori di diagnosticare rapidamente i problemi di connettività da o toohello internet e da o toohello nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="62b1f-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or toohello internet and from or toohello on-premises environment.</span></span>

<span data-ttu-id="62b1f-108">La verifica del flusso IP esamina l'interfaccia di rete di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="62b1f-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="62b1f-109">Il flusso del traffico viene quindi verificata in base a tooor impostazioni hello configurato dall'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="62b1f-109">Traffic flow is then verified based on hello configured settings tooor from that network interface.</span></span> <span data-ttu-id="62b1f-110">Questa funzionalità è utile per confermare se una regola in un gruppo di sicurezza di rete sta bloccando tooor di traffico in ingresso o in uscita da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="62b1f-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic tooor from a virtual machine.</span></span>

<span data-ttu-id="62b1f-111">Un'istanza di toobe esigenze Watcher di rete creato in tutte le aree che si prevede di flusso IP toorun verificare.</span><span class="sxs-lookup"><span data-stu-id="62b1f-111">An instance of Network Watcher needs toobe created in all regions that you plan toorun IP flow verify.</span></span> <span data-ttu-id="62b1f-112">Watcher di rete è un servizio regionale e possono essere eseguiti solo sulle risorse in hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="62b1f-112">Network Watcher is a regional service and can only be ran against resources in hello same region.</span></span> <span data-ttu-id="62b1f-113">Questa operazione non influenza hello risultati del flusso IP verificare come route hello associato hello che NIC verrà comunque restituito.</span><span class="sxs-lookup"><span data-stu-id="62b1f-113">This does not affect hello results of IP flow verify as hello route associated with hello NIC will still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="62b1f-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="62b1f-115">Next steps</span></span>

<span data-ttu-id="62b1f-116">Visitare il seguente articolo toolearn se un pacchetto è consentito o negato per una macchina virtuale specifica tramite il portale di hello hello.</span><span class="sxs-lookup"><span data-stu-id="62b1f-116">Visit hello following article toolearn if a packet is allowed or denied for a specific virtual machine through hello portal.</span></span> [<span data-ttu-id="62b1f-117">Controllare se il traffico è consentito in una macchina virtuale con flusso verificare IP tramite il portale di hello</span><span class="sxs-lookup"><span data-stu-id="62b1f-117">Check if traffic is allowed on a VM with IP Flow Verify using hello portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












