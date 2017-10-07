---
title: Verificare il traffico aaaVerify con flusso di controllo indirizzo IP rete di Azure - portale di Azure | Documenti Microsoft
description: "Questo articolo viene descritto come toocheck se tooor il traffico da una macchina virtuale è consentito o negato"
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
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="fa85b-103">Verifica se il traffico non è consentito o negato tooor da una macchina virtuale con IP flusso verificare un componente del controllo di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="fa85b-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="fa85b-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="fa85b-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="fa85b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa85b-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="fa85b-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="fa85b-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="fa85b-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="fa85b-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="fa85b-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="fa85b-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="fa85b-109">Verificare di flusso IP è una funzionalità di controllo di rete che consente tooverify se il traffico consentito tooor da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fa85b-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="fa85b-110">è possibile eseguire la convalida di Hello per il traffico in ingresso o in uscita.</span><span class="sxs-lookup"><span data-stu-id="fa85b-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="fa85b-111">Questo scenario è utile tooget uno stato corrente di fatto una macchina virtuale possono comunicare con la risorsa esterna tooan o un'altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="fa85b-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or another resource.</span></span> <span data-ttu-id="fa85b-112">Verificare di flusso IP può essere utilizzato tooverify se le regole di sicurezza gruppo (rete) sono configurate correttamente e risolvere i problemi di flussi che sono bloccati dalle regole di gruppo.</span><span class="sxs-lookup"><span data-stu-id="fa85b-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="fa85b-113">Un altro motivo per l'uso di IP flusso verificare tooensure che si desidera bloccare il traffico viene bloccato correttamente dal gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="fa85b-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fa85b-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="fa85b-114">Before you begin</span></span>

<span data-ttu-id="fa85b-115">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete o dispone di un'istanza esistente del controllo di rete.</span><span class="sxs-lookup"><span data-stu-id="fa85b-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="fa85b-116">scenario di Hello si suppone inoltre che un gruppo di risorse con una macchina virtuale valida toobe utilizzato.</span><span class="sxs-lookup"><span data-stu-id="fa85b-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="fa85b-117">Scenario</span><span class="sxs-lookup"><span data-stu-id="fa85b-117">Scenario</span></span>

<span data-ttu-id="fa85b-118">Questo scenario Usa tooverify IP flusso verificare se una macchina virtuale possono comunicare con computer tooanother sulla porta 443.</span><span class="sxs-lookup"><span data-stu-id="fa85b-118">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="fa85b-119">Regola di sicurezza hello che nega il traffico viene restituito se il traffico hello viene negato.</span><span class="sxs-lookup"><span data-stu-id="fa85b-119">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="fa85b-120">toolearn ulteriori informazioni su IP flusso verificare, visitare [IP Flow verificare Overview](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="fa85b-120">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="fa85b-121">Eseguire la verifica del flusso IP</span><span class="sxs-lookup"><span data-stu-id="fa85b-121">Run IP flow verify</span></span>

<span data-ttu-id="fa85b-122">Passare tooyour Watcher di rete e fare clic su **flusso IP verificare**.</span><span class="sxs-lookup"><span data-stu-id="fa85b-122">Navigate tooyour Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="fa85b-123">Selezionare macchina virtuale hello e interfaccia di rete tooverify traffico da.</span><span class="sxs-lookup"><span data-stu-id="fa85b-123">Select hello virtual machine and network interface you want tooverify traffic from.</span></span> <span data-ttu-id="fa85b-124">Immettere le eventuali informazioni di filtro aggiuntive e fare clic su **Controlla**.</span><span class="sxs-lookup"><span data-stu-id="fa85b-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="fa85b-125">Quando si fa clic su **controllare**, flusso hello in base ai criteri di hello immessa è selezionato.</span><span class="sxs-lookup"><span data-stu-id="fa85b-125">Once you click **Check**, hello flow based on hello criteria you provided is checked.</span></span> <span data-ttu-id="fa85b-126">risultato Hello è **accesso consentito** o **accesso negato**.</span><span class="sxs-lookup"><span data-stu-id="fa85b-126">hello result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="fa85b-127">Se l'accesso è negato, hello gruppo di sicurezza (rete) e regola di sicurezza che bloccano il traffico è disponibile.</span><span class="sxs-lookup"><span data-stu-id="fa85b-127">If access is denied, hello Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="fa85b-128">Se un attacco denial hello del traffico è il comportamento previsto, la regola hello è riuscita.</span><span class="sxs-lookup"><span data-stu-id="fa85b-128">If hello denial of traffic is expected behavior, then hello rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="fa85b-129">Flusso IP verificare richiede che venga allocata risorsa macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="fa85b-129">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="fa85b-130">Come si può vedere dal hello seguente immagine, è consentito il traffico HTTPS in uscita hello.</span><span class="sxs-lookup"><span data-stu-id="fa85b-130">As you can see from hello following image, hello outbound HTTPS traffic was allowed.</span></span>

![Panoramica della verifica del flusso IP][1]

<span data-ttu-id="fa85b-132">Come mostrato nella seguente immagine hello, viene modificato il traffico tooinbound e hello in entrata too123 porta modificata.</span><span class="sxs-lookup"><span data-stu-id="fa85b-132">As seen in hello following image, traffic is changed tooinbound and hello inbound port changed too123.</span></span> <span data-ttu-id="fa85b-133">Traffico ora viene negato, il messaggio hello "Accesso negato" viene fornito insieme hello rete gruppo e sicurezza regola di sicurezza negare il traffico di hello.</span><span class="sxs-lookup"><span data-stu-id="fa85b-133">Traffic is now denied, hello message "Access denied" is provided along with hello network security group and security rule that deny hello traffic.</span></span>

![Risultati del flusso di IP][2]

## <a name="next-steps"></a><span data-ttu-id="fa85b-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fa85b-135">Next steps</span></span>

<span data-ttu-id="fa85b-136">Se il traffico viene bloccato e non può essere, vedere [gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack verso il basso hello rete sicurezza e gruppo di regole di sicurezza definiti.</span><span class="sxs-lookup"><span data-stu-id="fa85b-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













