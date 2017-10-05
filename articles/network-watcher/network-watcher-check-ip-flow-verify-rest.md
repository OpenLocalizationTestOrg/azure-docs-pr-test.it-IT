---
title: 'Verificare il traffico con la verifica del flusso IP di Azure Network Watcher: REST | Microsoft Docs'
description: "Questo articolo descrive come verificare se il traffico da o verso una macchina virtuale è consentito o negato"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 6d3ce00a7d4f9c0cd57fa8815625a1065b03b5b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="25886-103">Controllare se il traffico è consentito o negato con la verifica del flusso IP, una funzionalità di Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="25886-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="25886-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="25886-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="25886-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="25886-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="25886-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="25886-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="25886-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="25886-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="25886-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="25886-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="25886-109">La verifica del flusso IP è una funzionalità di Network Watcher che consente di verificare se il traffico da o verso una macchina virtuale è consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="25886-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="25886-110">La convalida può essere eseguita per il traffico in ingresso o in uscita.</span><span class="sxs-lookup"><span data-stu-id="25886-110">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="25886-111">Questo scenario è utile per stabilire se una macchina virtuale può comunicare con una risorsa esterna o back-end.</span><span class="sxs-lookup"><span data-stu-id="25886-111">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="25886-112">La funzionalità può essere usata per verificare se le regole del gruppo di sicurezza di rete sono configurate correttamente e per risolvere i problemi dei flussi bloccati da tali regole.</span><span class="sxs-lookup"><span data-stu-id="25886-112">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="25886-113">La verifica del flusso IP consente inoltre di verificare che il traffico che si vuole bloccare sia correttamente bloccato dal gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="25886-113">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="25886-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="25886-114">Before you begin</span></span>

<span data-ttu-id="25886-115">ARMclient viene usato per chiamare l'API REST con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25886-115">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="25886-116">ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)</span><span class="sxs-lookup"><span data-stu-id="25886-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="25886-117">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="25886-117">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="25886-118">Scenario</span><span class="sxs-lookup"><span data-stu-id="25886-118">Scenario</span></span>

<span data-ttu-id="25886-119">Questo scenario usa la verifica del flusso IP per verificare se una macchina virtuale può comunicare con un altro computer sulla porta 443.</span><span class="sxs-lookup"><span data-stu-id="25886-119">This scenario uses IP flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="25886-120">Se il traffico viene negato, restituisce la regola di sicurezza che nega il traffico.</span><span class="sxs-lookup"><span data-stu-id="25886-120">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="25886-121">Per altre informazioni sulla verifica del flusso IP, leggere la [panoramica sulla verifica del flusso IP](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="25886-121">To learn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span></span>

<span data-ttu-id="25886-122">In questo scenario:</span><span class="sxs-lookup"><span data-stu-id="25886-122">In this scenario, you:</span></span>

* <span data-ttu-id="25886-123">Recuperare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="25886-123">Retrieve a virtual machine</span></span>
* <span data-ttu-id="25886-124">Chiamare la verifica del flusso IP</span><span class="sxs-lookup"><span data-stu-id="25886-124">Call IP flow verify</span></span>
* <span data-ttu-id="25886-125">Verificare i risultati</span><span class="sxs-lookup"><span data-stu-id="25886-125">Verify results</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="25886-126">Accedere con ARMClient</span><span class="sxs-lookup"><span data-stu-id="25886-126">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="25886-127">Recuperare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="25886-127">Retrieve a virtual machine</span></span>

<span data-ttu-id="25886-128">Eseguire lo script seguente per restituire la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="25886-128">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="25886-129">Il codice seguente richiede valori per le variabili:</span><span class="sxs-lookup"><span data-stu-id="25886-129">The following code needs values for the variables:</span></span>

* <span data-ttu-id="25886-130">**subscriptionId**: l'ID sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="25886-130">**subscriptionId** - The subscription Id to use.</span></span>
* <span data-ttu-id="25886-131">**resourceGroupName**: il nome di un gruppo di risorse contenente le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="25886-131">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="25886-132">L'informazione necessaria è l'ID, disponibile nel tipo `Microsoft.Compute/virtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="25886-132">The information that is needed is the id under the type `Microsoft.Compute/virtualMachines`.</span></span> <span data-ttu-id="25886-133">I risultati dovrebbero essere simili all'esempio di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="25886-133">The results should be similar to the following code sample:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a><span data-ttu-id="25886-134">Chiamare la verifica del flusso IP</span><span class="sxs-lookup"><span data-stu-id="25886-134">Call IP flow Verify</span></span>

<span data-ttu-id="25886-135">L'esempio seguente crea una richiesta per verificare il traffico per una macchina virtuale specificata.</span><span class="sxs-lookup"><span data-stu-id="25886-135">The following example creates a request to verify the traffic for a specified virtual machine.</span></span> <span data-ttu-id="25886-136">La risposta restituita indica se il traffico è consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="25886-136">The response returns if the traffic is allowed or if the traffic is denied.</span></span> <span data-ttu-id="25886-137">Se il traffico viene negato, restituisce anche la regola che blocca il traffico.</span><span class="sxs-lookup"><span data-stu-id="25886-137">If traffic is denied it also returns what rule blocks the traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="25886-138">La verifica del flusso IP richiede che la risorsa VM sia allocata.</span><span class="sxs-lookup"><span data-stu-id="25886-138">IP flow verify requires that the VM resource is allocated.</span></span>

<span data-ttu-id="25886-139">Lo script richiede l'ID risorsa di una macchina virtuale e di una scheda di interfaccia di rete nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="25886-139">The script requires the resource Id of a virtual machine and of a network interface card on the virtual machine.</span></span> <span data-ttu-id="25886-140">Questi valori sono disponibili nell'output precedente.</span><span class="sxs-lookup"><span data-stu-id="25886-140">These values are provided by the preceding output.</span></span>

> [!Important]
> <span data-ttu-id="25886-141">Per tutte le chiamate REST di Network Watcher, è il nome del gruppo di risorse nell'URI della richiesta che contiene l'istanza di Network Watcher, non le risorse su cui si eseguono le azioni di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="25886-141">For all Network Watcher REST calls the resource group name in the request URI is the one that contains the Network Watcher instance, not the resources you are performing the diagnostic actions on.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-the-results"></a><span data-ttu-id="25886-142">Informazioni sui risultati</span><span class="sxs-lookup"><span data-stu-id="25886-142">Understanding the results</span></span>

<span data-ttu-id="25886-143">La risposta che viene restituita indica se il traffico è consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="25886-143">The response you get back tells you whether the traffic is allowed or denied.</span></span> <span data-ttu-id="25886-144">La risposta ha un aspetto simile a uno degli esempi seguenti:</span><span class="sxs-lookup"><span data-stu-id="25886-144">The response looks like one of the following examples:</span></span>

<span data-ttu-id="25886-145">**Consentito**</span><span class="sxs-lookup"><span data-stu-id="25886-145">**Allowed**</span></span>

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

<span data-ttu-id="25886-146">**Negato**</span><span class="sxs-lookup"><span data-stu-id="25886-146">**Denied**</span></span>

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a><span data-ttu-id="25886-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25886-147">Next steps</span></span>

<span data-ttu-id="25886-148">Se il traffico risulta bloccato e non dovrebbe esserlo, vedere [Gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) per informazioni al riguardo.</span><span class="sxs-lookup"><span data-stu-id="25886-148">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to learn more about Network Security Groups.</span></span>












