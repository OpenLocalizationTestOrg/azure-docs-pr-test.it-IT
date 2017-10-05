---
title: Introduzione alla verifica del flusso IP in Azure Network Watcher | Microsoft Docs
description: "Questa pagina fornisce una panoramica della funzionalità di verifica del flusso IP di Network Watcher"
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
ms.openlocfilehash: 9c0dfc449b3d93d8aa4551ce16476c8313d731fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-ip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="b5acb-103">Introduzione alla verifica del flusso IP in Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="b5acb-103">Introduction to IP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="b5acb-104">La verifica del flusso IP controlla se un pacchetto viene accettato o rifiutato in ingresso o in uscita da una macchina virtuale in base a informazioni a 5 tuple.</span><span class="sxs-lookup"><span data-stu-id="b5acb-104">IP flow verify checks if a packet is allowed or denied to or from a virtual machine based on 5-tuple information.</span></span> <span data-ttu-id="b5acb-105">Tali informazioni sono costituite da direzione, protocollo, indirizzo IP locale, indirizzo IP remoto, porta locale e porta remota.</span><span class="sxs-lookup"><span data-stu-id="b5acb-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="b5acb-106">Se il pacchetto viene rifiutato da un gruppo di sicurezza, viene restituito il nome della regola che ha rifiutato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b5acb-106">If the packet is denied by a security group, the name of the rule that denied the packet is returned.</span></span> <span data-ttu-id="b5acb-107">Anche se è possibile scegliere qualsiasi indirizzo IP di origine o di destinazione, questa funzionalità permette agli amministratori di diagnosticare rapidamente problemi di connettività in ingresso o in uscita da Internet e in ingresso o in uscita dall'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="b5acb-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or to the internet and from or to the on-premises environment.</span></span>

<span data-ttu-id="b5acb-108">La verifica del flusso IP esamina l'interfaccia di rete di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b5acb-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="b5acb-109">Il flusso di traffico in ingresso o in uscita dall'interfaccia di rete viene quindi verificato in base alle impostazioni configurate.</span><span class="sxs-lookup"><span data-stu-id="b5acb-109">Traffic flow is then verified based on the configured settings to or from that network interface.</span></span> <span data-ttu-id="b5acb-110">Questa funzionalità permette di confermare se una regola di un gruppo di sicurezza di rete sta bloccando il traffico in ingresso o in uscita da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b5acb-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic to or from a virtual machine.</span></span>

<span data-ttu-id="b5acb-111">È necessario creare un'istanza di Network Watcher in tutte le aree in cui è prevista l'esecuzione della verifica del flusso IP.</span><span class="sxs-lookup"><span data-stu-id="b5acb-111">An instance of Network Watcher needs to be created in all regions that you plan to run IP flow verify.</span></span> <span data-ttu-id="b5acb-112">Network Watcher è un servizio a livello di area e può essere eseguito solo su risorse nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="b5acb-112">Network Watcher is a regional service and can only be ran against resources in the same region.</span></span> <span data-ttu-id="b5acb-113">Non influisce sui risultati della verifica del flusso IP, perché verrà comunque restituita la route associata alla scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="b5acb-113">This does not affect the results of IP flow verify as the route associated with the NIC will still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="b5acb-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b5acb-115">Next steps</span></span>

<span data-ttu-id="b5acb-116">Per informazioni su come stabilire se un pacchetto viene accettato o rifiutato per una macchina virtuale specifica tramite il portale, vedere l'articolo seguente.</span><span class="sxs-lookup"><span data-stu-id="b5acb-116">Visit the following article to learn if a packet is allowed or denied for a specific virtual machine through the portal.</span></span> [<span data-ttu-id="b5acb-117">Controllare se il traffico da o verso una macchina virtuale è consentito o negato con la verifica del flusso IP tramite il portale</span><span class="sxs-lookup"><span data-stu-id="b5acb-117">Check if traffic is allowed on a VM with IP Flow Verify using the portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












