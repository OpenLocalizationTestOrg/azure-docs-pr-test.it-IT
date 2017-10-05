---
title: Verificare il traffico con la verifica del flusso IP di Network Watcher di Azure - Portale di Azure | Documentazione Microsoft
description: "Questo articolo descrive come verificare se il traffico da o verso una macchina virtuale è consentito o negato"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7db29c186cf6e6f3b40a680ab76f1d2763f806ba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="5706d-103">Controllare se il traffico da o verso una macchina virtuale è consentito o negato con la verifica del flusso IP, una funzionalità di Network Watcher di Azure</span><span class="sxs-lookup"><span data-stu-id="5706d-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="5706d-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5706d-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="5706d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5706d-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="5706d-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="5706d-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="5706d-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="5706d-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="5706d-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="5706d-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="5706d-109">La verifica del flusso IP è una funzionalità di Network Watcher che consente di verificare se il traffico da o verso una macchina virtuale è consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="5706d-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="5706d-110">La convalida può essere eseguita per il traffico in ingresso o in uscita.</span><span class="sxs-lookup"><span data-stu-id="5706d-110">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="5706d-111">Questo scenario è utile per stabilire se una macchina virtuale può comunicare con una risorsa esterna o un'altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="5706d-111">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or another resource.</span></span> <span data-ttu-id="5706d-112">La funzionalità può essere usata per verificare se le regole del gruppo di sicurezza di rete sono configurate correttamente e per risolvere i problemi dei flussi bloccati da tali regole.</span><span class="sxs-lookup"><span data-stu-id="5706d-112">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="5706d-113">La verifica del flusso IP consente inoltre di verificare che il traffico che si vuole bloccare sia correttamente bloccato dal gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="5706d-113">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5706d-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="5706d-114">Before you begin</span></span>

<span data-ttu-id="5706d-115">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher o aprire un'istanza esistente di Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="5706d-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="5706d-116">Lo scenario presuppone inoltre che esista e possa essere usato un gruppo di risorse con una macchina virtuale valida.</span><span class="sxs-lookup"><span data-stu-id="5706d-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="5706d-117">Scenario</span><span class="sxs-lookup"><span data-stu-id="5706d-117">Scenario</span></span>

<span data-ttu-id="5706d-118">Questo scenario usa la verifica del flusso IP per verificare se una macchina virtuale può comunicare con un altro computer sulla porta 443.</span><span class="sxs-lookup"><span data-stu-id="5706d-118">This scenario uses IP Flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="5706d-119">Se il traffico viene negato, restituisce la regola di sicurezza che nega il traffico.</span><span class="sxs-lookup"><span data-stu-id="5706d-119">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="5706d-120">Per altre informazioni sulla verifica del flusso IP, leggere la [panoramica sulla verifica del flusso IP](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="5706d-120">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="5706d-121">Eseguire la verifica del flusso IP</span><span class="sxs-lookup"><span data-stu-id="5706d-121">Run IP flow verify</span></span>

<span data-ttu-id="5706d-122">Passare a Network Watcher e fare clic su **Verifica del flusso IP**.</span><span class="sxs-lookup"><span data-stu-id="5706d-122">Navigate to your Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="5706d-123">Selezionare la macchina virtuale e l'interfaccia di rete da cui si desidera verificare il traffico.</span><span class="sxs-lookup"><span data-stu-id="5706d-123">Select the virtual machine and network interface you want to verify traffic from.</span></span> <span data-ttu-id="5706d-124">Immettere le eventuali informazioni di filtro aggiuntive e fare clic su **Controlla**.</span><span class="sxs-lookup"><span data-stu-id="5706d-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="5706d-125">Dopo avere fatto clic **Controlla**, viene controllato il flusso in base ai criteri forniti.</span><span class="sxs-lookup"><span data-stu-id="5706d-125">Once you click **Check**, the flow based on the criteria you provided is checked.</span></span> <span data-ttu-id="5706d-126">Il risultato è **Accesso consentito** o **Accesso negato**.</span><span class="sxs-lookup"><span data-stu-id="5706d-126">The result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="5706d-127">Se l'accesso è negato, vengono forniti il gruppo di sicurezza di rete (NSG) e la regola di sicurezza che bloccano il traffico.</span><span class="sxs-lookup"><span data-stu-id="5706d-127">If access is denied, the Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="5706d-128">Se il comportamento atteso era la negazione del traffico, la regola ha funzionato.</span><span class="sxs-lookup"><span data-stu-id="5706d-128">If the denial of traffic is expected behavior, then the rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="5706d-129">La verifica del flusso IP richiede che la risorsa VM sia allocata.</span><span class="sxs-lookup"><span data-stu-id="5706d-129">IP flow verify requires that the VM resource is allocated.</span></span>

<span data-ttu-id="5706d-130">Come si può notare dalla figura seguente, il traffico HTTPS in uscita era consentito.</span><span class="sxs-lookup"><span data-stu-id="5706d-130">As you can see from the following image, the outbound HTTPS traffic was allowed.</span></span>

![Panoramica della verifica del flusso IP][1]

<span data-ttu-id="5706d-132">Come illustrato nella figura seguente, il traffico diventa in ingresso e la porta di ingresso a la 123.</span><span class="sxs-lookup"><span data-stu-id="5706d-132">As seen in the following image, traffic is changed to inbound and the inbound port changed to 123.</span></span> <span data-ttu-id="5706d-133">Il traffico ora è negato, viene fornito il messaggio "Accesso negato" insieme al gruppo di sicurezza di rete e alla regola di sicurezza che negano il traffico.</span><span class="sxs-lookup"><span data-stu-id="5706d-133">Traffic is now denied, the message "Access denied" is provided along with the network security group and security rule that deny the traffic.</span></span>

![Risultati del flusso di IP][2]

## <a name="next-steps"></a><span data-ttu-id="5706d-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5706d-135">Next steps</span></span>

<span data-ttu-id="5706d-136">Se il traffico risulta bloccato e non dovrebbe esserlo, vedere [Gestire i gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) per individuare il gruppo di sicurezza di rete e le relative regole di sicurezza definite.</span><span class="sxs-lookup"><span data-stu-id="5706d-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













