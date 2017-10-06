---
title: traffico aaaVerify con Azure rete Watcher IP flusso verificare - CLI di Azure | Documenti Microsoft
description: "Questo articolo viene descritto come toocheck se tooor il traffico da una macchina virtuale è consentito o negato tramite l'interfaccia CLI di Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 128a00b4296994551e7e17838a51e6d9de180e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="e38da-103">Verifica se il traffico non è consentito o negato tooor da una macchina virtuale con IP flusso verificare un componente del controllo di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="e38da-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="e38da-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e38da-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="e38da-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e38da-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="e38da-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="e38da-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="e38da-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="e38da-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="e38da-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="e38da-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="e38da-109">Flusso di IP verificare è una funzionalità di controllo di rete che consente tooverify se il traffico consentito tooor da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e38da-109">IP Flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="e38da-110">Questo scenario è utile tooget uno stato corrente di fatto una macchina virtuale possono comunicare con la risorsa esterna tooan o back-end.</span><span class="sxs-lookup"><span data-stu-id="e38da-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="e38da-111">Verificare di flusso IP può essere utilizzato tooverify se le regole di sicurezza gruppo (rete) sono configurate correttamente e risolvere i problemi di flussi che sono bloccati dalle regole di gruppo.</span><span class="sxs-lookup"><span data-stu-id="e38da-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="e38da-112">Un altro motivo per l'uso di IP flusso verificare tooensure che si desidera bloccare il traffico viene bloccato correttamente dal gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="e38da-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

<span data-ttu-id="e38da-113">In questo articolo utilizza la nuova generazione CLI per modello di distribuzione Gestione risorse hello, CLI di Azure 2.0, che è disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="e38da-113">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="e38da-114">hello tooperform i passaggi in questo articolo, è necessario troppo[installare hello interfaccia della riga di comando di Azure per Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="e38da-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e38da-115">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="e38da-115">Before you begin</span></span>

<span data-ttu-id="e38da-116">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete o dispone di un'istanza esistente del controllo di rete.</span><span class="sxs-lookup"><span data-stu-id="e38da-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="e38da-117">scenario di Hello si suppone inoltre che un gruppo di risorse con una macchina virtuale valida toobe utilizzato.</span><span class="sxs-lookup"><span data-stu-id="e38da-117">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="e38da-118">Scenario</span><span class="sxs-lookup"><span data-stu-id="e38da-118">Scenario</span></span>

<span data-ttu-id="e38da-119">Questo scenario Usa tooverify IP flusso verificare se una macchina virtuale possono comunicare con tooa noti indirizzo IP di Bing.</span><span class="sxs-lookup"><span data-stu-id="e38da-119">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="e38da-120">Regola di sicurezza hello che nega il traffico viene restituito se il traffico hello viene negato.</span><span class="sxs-lookup"><span data-stu-id="e38da-120">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="e38da-121">toolearn ulteriori informazioni su IP flusso verificare, visitare [IP Flow verificare Overview](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e38da-121">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="e38da-122">Ottenere una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e38da-122">Get a VM</span></span>

<span data-ttu-id="e38da-123">Flusso IP verificare tooor il traffico di test da un indirizzo IP su tooor una macchina virtuale da una destinazione remota.</span><span class="sxs-lookup"><span data-stu-id="e38da-123">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="e38da-124">Un Id di una macchina virtuale è obbligatorio per i cmdlet di hello.</span><span class="sxs-lookup"><span data-stu-id="e38da-124">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="e38da-125">Se si conosce già ID hello di hello toouse di macchina virtuale, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="e38da-125">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-hello-nics"></a><span data-ttu-id="e38da-126">Ottenere hello NIC</span><span class="sxs-lookup"><span data-stu-id="e38da-126">Get hello NICS</span></span>

<span data-ttu-id="e38da-127">è necessario l'indirizzo IP Hello di una scheda di rete nella macchina virtuale hello, in questo esempio vengono recuperate le schede NIC hello in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e38da-127">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="e38da-128">Se si conosce già hello IP indirizzo che si desidera tootest sulla macchina virtuale hello, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="e38da-128">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="e38da-129">Eseguire la verifica del flusso IP</span><span class="sxs-lookup"><span data-stu-id="e38da-129">Run IP flow verify</span></span>

<span data-ttu-id="e38da-130">Ora che si dispone di informazioni hello necessari toorun hello cmdlet, eseguiamo hello `az network watcher test-ip-flow` traffico hello tootest di cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e38da-130">Now that we have hello information needed toorun hello cmdlet, we run hello `az network watcher test-ip-flow` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="e38da-131">In questo esempio, utilizziamo primo indirizzo IP di hello in hello prima scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="e38da-131">In this example, we are using hello first IP address on hello first NIC.</span></span>

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> <span data-ttu-id="e38da-132">Flusso di IP verificare richiede che risorsa macchina virtuale hello è allocato toorun.</span><span class="sxs-lookup"><span data-stu-id="e38da-132">IP Flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="e38da-133">Esaminare i risultati</span><span class="sxs-lookup"><span data-stu-id="e38da-133">Review Results</span></span>

<span data-ttu-id="e38da-134">Dopo aver eseguito `az network watcher test-ip-flow` hello risultati vengono restituiti, esempio hello è risultato hello restituito da hello passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="e38da-134">After running `az network watcher test-ip-flow` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a><span data-ttu-id="e38da-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e38da-135">Next steps</span></span>

<span data-ttu-id="e38da-136">Se il traffico viene bloccato e non può essere, vedere [gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack verso il basso hello rete sicurezza e gruppo di regole di sicurezza definiti.</span><span class="sxs-lookup"><span data-stu-id="e38da-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<span data-ttu-id="e38da-137">Informazioni su impostazioni gruppo tooaudit visitando [il controllo di sicurezza gruppi (rete) con Watcher di rete](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e38da-137">Learn tooaudit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
