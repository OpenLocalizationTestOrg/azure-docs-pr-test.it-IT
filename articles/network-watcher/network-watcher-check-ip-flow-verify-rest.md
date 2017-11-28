---
title: traffico aaaVerify con flusso di controllo indirizzo IP rete di Azure verifica - REST | Documenti Microsoft
description: "Questo articolo viene descritto come toocheck se tooor il traffico da una macchina virtuale è consentito o negato"
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
ms.openlocfilehash: 956db0d326db597c6c402a9e8d4a5522c47c02d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="2af86-103">Controllare se il traffico è consentito o negato con la verifica del flusso IP, una funzionalità di Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="2af86-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2af86-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2af86-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="2af86-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2af86-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="2af86-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="2af86-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="2af86-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="2af86-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="2af86-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="2af86-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="2af86-109">Verificare di flusso IP è una funzionalità di controllo di rete che consente tooverify se il traffico consentito tooor da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2af86-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="2af86-110">è possibile eseguire la convalida di Hello per il traffico in ingresso o in uscita.</span><span class="sxs-lookup"><span data-stu-id="2af86-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="2af86-111">Questo scenario è utile tooget uno stato corrente di fatto una macchina virtuale possono comunicare con la risorsa esterna tooan o back-end.</span><span class="sxs-lookup"><span data-stu-id="2af86-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="2af86-112">Verificare di flusso IP può essere utilizzato tooverify se le regole di sicurezza gruppo (rete) sono configurate correttamente e risolvere i problemi di flussi che sono bloccati dalle regole di gruppo.</span><span class="sxs-lookup"><span data-stu-id="2af86-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="2af86-113">Un altro motivo per l'uso di IP flusso verificare tooensure che si desidera bloccare il traffico viene bloccato correttamente dal gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="2af86-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2af86-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="2af86-114">Before you begin</span></span>

<span data-ttu-id="2af86-115">ARMclient è l'API REST di hello toocall utilizzati tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2af86-115">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="2af86-116">ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)</span><span class="sxs-lookup"><span data-stu-id="2af86-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="2af86-117">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="2af86-117">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="2af86-118">Scenario</span><span class="sxs-lookup"><span data-stu-id="2af86-118">Scenario</span></span>

<span data-ttu-id="2af86-119">Questo scenario Usa IP flusso verificare tooverify se una macchina virtuale possono comunicare con computer tooanother sulla porta 443.</span><span class="sxs-lookup"><span data-stu-id="2af86-119">This scenario uses IP flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="2af86-120">Regola di sicurezza hello che nega il traffico viene restituito se il traffico hello viene negato.</span><span class="sxs-lookup"><span data-stu-id="2af86-120">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="2af86-121">toolearn più sul flusso di IP verificare, visitare [flusso IP verificare Panoramica](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2af86-121">toolearn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span></span>

<span data-ttu-id="2af86-122">In questo scenario:</span><span class="sxs-lookup"><span data-stu-id="2af86-122">In this scenario, you:</span></span>

* <span data-ttu-id="2af86-123">Recuperare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="2af86-123">Retrieve a virtual machine</span></span>
* <span data-ttu-id="2af86-124">Chiamare la verifica del flusso IP</span><span class="sxs-lookup"><span data-stu-id="2af86-124">Call IP flow verify</span></span>
* <span data-ttu-id="2af86-125">Verificare i risultati</span><span class="sxs-lookup"><span data-stu-id="2af86-125">Verify results</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="2af86-126">Accedere con ARMClient</span><span class="sxs-lookup"><span data-stu-id="2af86-126">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="2af86-127">Recuperare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="2af86-127">Retrieve a virtual machine</span></span>

<span data-ttu-id="2af86-128">Eseguire hello seguenti script tooreturn una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2af86-128">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="2af86-129">Hello codice riportato di seguito deve valori per le variabili di hello:</span><span class="sxs-lookup"><span data-stu-id="2af86-129">hello following code needs values for hello variables:</span></span>

* <span data-ttu-id="2af86-130">**subscriptionId** -hello toouse Id sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="2af86-130">**subscriptionId** - hello subscription Id toouse.</span></span>
* <span data-ttu-id="2af86-131">**resourceGroupName** : hello nome di un gruppo di risorse contenente le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="2af86-131">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="2af86-132">le informazioni necessarie Hello sono id hello in tipo hello `Microsoft.Compute/virtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="2af86-132">hello information that is needed is hello id under hello type `Microsoft.Compute/virtualMachines`.</span></span> <span data-ttu-id="2af86-133">i risultati di Hello saranno simile toohello nell'esempio di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="2af86-133">hello results should be similar toohello following code sample:</span></span>

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

## <a name="call-ip-flow-verify"></a><span data-ttu-id="2af86-134">Chiamare la verifica del flusso IP</span><span class="sxs-lookup"><span data-stu-id="2af86-134">Call IP flow Verify</span></span>

<span data-ttu-id="2af86-135">Hello seguente viene creato un traffico di hello tooverify richiesta per una macchina virtuale specificata.</span><span class="sxs-lookup"><span data-stu-id="2af86-135">hello following example creates a request tooverify hello traffic for a specified virtual machine.</span></span> <span data-ttu-id="2af86-136">risposta Hello restituisce se il traffico di hello è consentito o negato traffico hello.</span><span class="sxs-lookup"><span data-stu-id="2af86-136">hello response returns if hello traffic is allowed or if hello traffic is denied.</span></span> <span data-ttu-id="2af86-137">Se il traffico viene negato il che operatore restituisce inoltre i blocchi di regole hello traffico.</span><span class="sxs-lookup"><span data-stu-id="2af86-137">If traffic is denied it also returns what rule blocks hello traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="2af86-138">Flusso IP verificare richiede che venga allocata risorsa macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="2af86-138">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="2af86-139">script Hello richiede risorse hello Id di una macchina virtuale e di una scheda di interfaccia di rete nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="2af86-139">hello script requires hello resource Id of a virtual machine and of a network interface card on hello virtual machine.</span></span> <span data-ttu-id="2af86-140">Questi valori vengono forniti dal hello output precedente.</span><span class="sxs-lookup"><span data-stu-id="2af86-140">These values are provided by hello preceding output.</span></span>

> [!Important]
> <span data-ttu-id="2af86-141">Per REST Watcher di rete tutte le chiamate hello Nome gruppo di risorse nella richiesta di hello che URI è hello contenente istanza Watcher di rete hello, non le risorse hello si eseguono operazioni di diagnostica hello in.</span><span class="sxs-lookup"><span data-stu-id="2af86-141">For all Network Watcher REST calls hello resource group name in hello request URI is hello one that contains hello Network Watcher instance, not hello resources you are performing hello diagnostic actions on.</span></span>

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

## <a name="understanding-hello-results"></a><span data-ttu-id="2af86-142">Informazioni sui risultati hello</span><span class="sxs-lookup"><span data-stu-id="2af86-142">Understanding hello results</span></span>

<span data-ttu-id="2af86-143">risposta Hello che verrà restituito indica se il traffico di hello è consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="2af86-143">hello response you get back tells you whether hello traffic is allowed or denied.</span></span> <span data-ttu-id="2af86-144">risposta Hello è simile a uno dei seguenti esempi hello:</span><span class="sxs-lookup"><span data-stu-id="2af86-144">hello response looks like one of hello following examples:</span></span>

<span data-ttu-id="2af86-145">**Consentito**</span><span class="sxs-lookup"><span data-stu-id="2af86-145">**Allowed**</span></span>

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

<span data-ttu-id="2af86-146">**Negato**</span><span class="sxs-lookup"><span data-stu-id="2af86-146">**Denied**</span></span>

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a><span data-ttu-id="2af86-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2af86-147">Next steps</span></span>

<span data-ttu-id="2af86-148">Se il traffico viene bloccato e non può essere, vedere [gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn ulteriori informazioni sui gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="2af86-148">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn more about Network Security Groups.</span></span>












