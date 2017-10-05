---
title: Verificare il traffico con la verifica del flusso IP di Network Watcher di Azure - Interfaccia della riga di comando di Azure | Documentazione Microsoft
description: "Questo articolo descrive come verificare se il traffico da o verso una macchina virtuale è consentito o negato usando l'interfaccia della riga di comando di Azure"
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
ms.openlocfilehash: 0b52257a6c38a4392573672b7190d2269c2f145a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="bfe5e-103">Controllare se il traffico da o verso una macchina virtuale è consentito o negato con la verifica del flusso IP, una funzionalità di Network Watcher di Azure</span><span class="sxs-lookup"><span data-stu-id="bfe5e-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="bfe5e-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="bfe5e-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="bfe5e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfe5e-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="bfe5e-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="bfe5e-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="bfe5e-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="bfe5e-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="bfe5e-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="bfe5e-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="bfe5e-109">La verifica del flusso IP è una funzionalità di Network Watcher che consente di verificare se il traffico da o verso una macchina virtuale è consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-109">IP Flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="bfe5e-110">Questo scenario è utile per stabilire se una macchina virtuale può comunicare con una risorsa esterna o back-end.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="bfe5e-111">La funzionalità può essere usata per verificare se le regole del gruppo di sicurezza di rete sono configurate correttamente e per risolvere i problemi dei flussi bloccati da tali regole.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="bfe5e-112">La verifica del flusso IP consente inoltre di verificare che il traffico che si vuole bloccare sia correttamente bloccato dal gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

<span data-ttu-id="bfe5e-113">Questo articolo usa l'interfaccia della riga di comando di nuova generazione per il modello di distribuzione di gestione delle risorse, ovvero l'interfaccia della riga di comando di Azure 2.0, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-113">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="bfe5e-114">Per eseguire i passaggi indicati in questo articolo è necessario [installare l'interfaccia della riga di comando di Azure per Mac, Linux e Windows (interfaccia della riga di comando di Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="bfe5e-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bfe5e-115">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="bfe5e-115">Before you begin</span></span>

<span data-ttu-id="bfe5e-116">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher o aprire un'istanza esistente di Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-116">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="bfe5e-117">Lo scenario presuppone inoltre che esista e possa essere usato un gruppo di risorse con una macchina virtuale valida.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-117">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="bfe5e-118">Scenario</span><span class="sxs-lookup"><span data-stu-id="bfe5e-118">Scenario</span></span>

<span data-ttu-id="bfe5e-119">Questo scenario usa la verifica del flusso IP per verificare se una macchina virtuale può comunicare con un indirizzo IP Bing noto.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-119">This scenario uses IP Flow Verify to verify if a virtual machine can talk to a known Bing IP address.</span></span> <span data-ttu-id="bfe5e-120">Se il traffico viene negato, restituisce la regola di sicurezza che nega il traffico.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-120">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="bfe5e-121">Per altre informazioni sulla verifica del flusso IP, leggere la [panoramica sulla verifica del flusso IP](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bfe5e-121">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="bfe5e-122">Ottenere una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="bfe5e-122">Get a VM</span></span>

<span data-ttu-id="bfe5e-123">La verifica del flusso IP esegue il test del traffico da o verso un indirizzo IP su una macchina virtuale da o verso una destinazione remota.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-123">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span></span> <span data-ttu-id="bfe5e-124">Il cmdlet richiede un ID di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-124">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="bfe5e-125">Se l'ID della macchina virtuale da usare è già noto, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-125">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-the-nics"></a><span data-ttu-id="bfe5e-126">Ottenere le schede NIC</span><span class="sxs-lookup"><span data-stu-id="bfe5e-126">Get the NICS</span></span>

<span data-ttu-id="bfe5e-127">È necessario l'indirizzo IP di una scheda di rete nella macchina virtuale. In questo esempio vengono recuperate le schede NIC in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-127">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="bfe5e-128">Se l'indirizzo IP da testare nella macchina virtuale è già noto, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-128">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="bfe5e-129">Eseguire la verifica del flusso IP</span><span class="sxs-lookup"><span data-stu-id="bfe5e-129">Run IP flow verify</span></span>

<span data-ttu-id="bfe5e-130">Dopo aver ottenuto le informazioni necessarie per eseguire il cmdlet, eseguire il cmdlet `az network watcher test-ip-flow` per testare il traffico.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-130">Now that we have the information needed to run the cmdlet, we run the `az network watcher test-ip-flow` cmdlet to test the traffic.</span></span> <span data-ttu-id="bfe5e-131">In questo esempio, viene usato il primo indirizzo IP nella prima scheda NIC.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-131">In this example, we are using the first IP address on the first NIC.</span></span>

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> <span data-ttu-id="bfe5e-132">Per eseguire la verifica del flusso IP è necessario che la risorsa della macchina virtuale sia allocata.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-132">IP Flow verify requires that the VM resource is allocated to run.</span></span>

## <a name="review-results"></a><span data-ttu-id="bfe5e-133">Esaminare i risultati</span><span class="sxs-lookup"><span data-stu-id="bfe5e-133">Review Results</span></span>

<span data-ttu-id="bfe5e-134">Dopo aver eseguito `az network watcher test-ip-flow` vengono restituiti i risultati. L'esempio seguente mostra i risultati restituiti nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-134">After running `az network watcher test-ip-flow` the results are returned, the following example is the results returned from the preceding step.</span></span>

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a><span data-ttu-id="bfe5e-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bfe5e-135">Next steps</span></span>

<span data-ttu-id="bfe5e-136">Se il traffico risulta bloccato e non dovrebbe esserlo, vedere [Gestire i gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) per individuare il gruppo di sicurezza di rete e le relative regole di sicurezza definite.</span><span class="sxs-lookup"><span data-stu-id="bfe5e-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

<span data-ttu-id="bfe5e-137">Informazioni su come controllare le impostazioni del gruppo sicurezza di rete sono disponibili in [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) (Verifica dei gruppi di sicurezza di rete con Network Watcher).</span><span class="sxs-lookup"><span data-stu-id="bfe5e-137">Learn to audit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
