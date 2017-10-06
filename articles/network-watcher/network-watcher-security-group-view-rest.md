---
title: sicurezza di rete aaaAnalyze con visualizzazione gruppo di sicurezza di controllo di rete di Azure - API REST | Documenti Microsoft
description: In questo articolo viene descritto come toouse PowerShell tooanalyze un virtuale macchine protezione con visualizzazione del gruppo di sicurezza.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a2f418fe-f5d2-43ed-8dc3-df0ed2a4d4ac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 0858a64a9454816e05f06dadb9536ad0c755e90e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a><span data-ttu-id="ba43a-103">Analizzare la protezione della macchina virtuale visualizzando un gruppo di sicurezza con l'API REST</span><span class="sxs-lookup"><span data-stu-id="ba43a-103">Analyze your Virtual Machine security with Security Group View using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ba43a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba43a-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="ba43a-105">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="ba43a-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="ba43a-106">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="ba43a-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="ba43a-107">API REST</span><span class="sxs-lookup"><span data-stu-id="ba43a-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="ba43a-108">Visualizzazione del gruppo di sicurezza restituisce regole di sicurezza di rete configurate ed efficace di macchina virtuale tooa applicato.</span><span class="sxs-lookup"><span data-stu-id="ba43a-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="ba43a-109">Questa funzionalità è utile tooaudit e diagnosticare i gruppi di sicurezza di rete e le regole configurate per il traffico tooensure una macchina virtuale viene correttamente consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="ba43a-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="ba43a-110">In questo articolo viene illustrata la funzionamento delle regole di sicurezza efficace e applicato di hello tooretrieve macchina virtuale tooa tramite l'API REST</span><span class="sxs-lookup"><span data-stu-id="ba43a-110">In this article, we show you how tooretrieve hello effective and applied security rules tooa virtual machine using REST API</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ba43a-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="ba43a-111">Before you begin</span></span>

<span data-ttu-id="ba43a-112">In questo scenario, chiamare visualizzazione del gruppo protezione tooget hello hello API Rest Watcher di rete per una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ba43a-112">In this scenario, you call hello Network Watcher Rest API tooget hello security group view for a virtual machine.</span></span> <span data-ttu-id="ba43a-113">ARMclient è l'API REST di hello toocall utilizzati tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ba43a-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="ba43a-114">ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)</span><span class="sxs-lookup"><span data-stu-id="ba43a-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="ba43a-115">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="ba43a-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="ba43a-116">scenario di Hello si suppone inoltre che un gruppo di risorse con una macchina virtuale valida toobe utilizzato.</span><span class="sxs-lookup"><span data-stu-id="ba43a-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="ba43a-117">Scenario</span><span class="sxs-lookup"><span data-stu-id="ba43a-117">Scenario</span></span>

<span data-ttu-id="ba43a-118">scenario Hello illustrato in questo articolo consente di recuperare le regole di sicurezza efficace e applicato hello per una determinata macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ba43a-118">hello scenario covered in this article retrieves hello effective and applied security rules for a given virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="ba43a-119">Accedere con ARMClient</span><span class="sxs-lookup"><span data-stu-id="ba43a-119">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="ba43a-120">Recuperare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ba43a-120">Retrieve a virtual machine</span></span>

<span data-ttu-id="ba43a-121">Eseguire i seguenti script tooreturn un machineThe virtuale hello seguente di codice deve variabili:</span><span class="sxs-lookup"><span data-stu-id="ba43a-121">Run hello following script tooreturn a virtual machineThe following code needs variables:</span></span>

- <span data-ttu-id="ba43a-122">**subscriptionId** -id sottoscrizione hello possono anche essere recuperati con hello **Get AzureRMSubscription** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ba43a-122">**subscriptionId** - hello subscription id can also be retrieved with hello **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="ba43a-123">**resourceGroupName** : hello nome di un gruppo di risorse contenente le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ba43a-123">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="ba43a-124">le informazioni necessarie Hello sono hello **id** in tipo hello `Microsoft.Compute/virtualMachines` in risposta, come illustrato nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="ba43a-124">hello information that is needed is hello **id** under hello type `Microsoft.Compute/virtualMachines` in response, as seen in hello following example:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft
.Network/networkInterfaces/{nicName}"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Com
pute/virtualMachines/{vmName}/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute
/virtualMachines/{vmName}",
      "name": "{vmName}"
    }
  ]
}
```

## <a name="get-security-group-view-for-virtual-machine"></a><span data-ttu-id="ba43a-125">Ottenere la visualizzazione del gruppo di sicurezza per la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ba43a-125">Get security group view for virtual machine</span></span>

<span data-ttu-id="ba43a-126">Hello di esempio seguente richiede vista gruppo di sicurezza hello di una macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="ba43a-126">hello following example requests hello security group view of a targeted virtual machine.</span></span> <span data-ttu-id="ba43a-127">risultati dell'esempio Hello possono essere utilizzato toocompare toohello regole e sicurezza definiti da hello origine toolook deviazione della configurazione.</span><span class="sxs-lookup"><span data-stu-id="ba43a-127">hello results from this example can be used toocompare toohello rules and security defined by hello origination toolook for configuration drift.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName

$requestBody = @"
{
    'targetResourceId': '${targetUri}'

}
"@
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/securityGroupView?api-version=2016-12-01" $requestBody -verbose
```

## <a name="view-hello-response"></a><span data-ttu-id="ba43a-128">Visualizzazione hello risposta</span><span class="sxs-lookup"><span data-stu-id="ba43a-128">View hello response</span></span>

<span data-ttu-id="ba43a-129">Dopo l'esempio Hello è risposta hello restituita dal comando precedente hello.</span><span class="sxs-lookup"><span data-stu-id="ba43a-129">hello following sample is hello response returned from hello preceding command.</span></span> <span data-ttu-id="ba43a-130">Hello risultati mostrano tutte le regole di sicurezza efficace e applicato hello nella macchina virtuale hello suddiviso in gruppi di **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, e  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="ba43a-130">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json

{
  "networkInterfaces": [
    {
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "securityRules": [
            {
              "name": "default-allow-rdp",
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
              "properties": {
                "provisioningState": "Succeeded",
                "protocol": "TCP",
                "sourcePortRange": "*",
                "destinationPortRange": "3389",
                "sourceAddressPrefix": "*",
                "destinationAddressPrefix": "*",
                "access": "Allow",
                "priority": 1000,
                "direction": "Inbound"
              }
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "name": "AllowVnetInBound",
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/",
            "properties": {
              "provisioningState": "Succeeded",
              "description": "Allow inbound traffic from all VMs in VNET",
              "protocol": "*",
              "sourcePortRange": "*",
              "destinationPortRange": "*",
              "sourceAddressPrefix": "VirtualNetwork",
              "destinationAddressPrefix": "VirtualNetwork",
              "access": "Allow",
              "priority": 65000,
              "direction": "Inbound"
            }
          },
          ...
        ],
        "effectiveSecurityRules": [
          {
            "name": "DefaultOutboundDenyAll",
            "protocol": "All",
            "sourcePortRange": "0-65535",
            "destinationPortRange": "0-65535",
            "sourceAddressPrefix": "*",
            "destinationAddressPrefix": "*",
            "access": "Deny",
            "priority": 65500,
            "direction": "Outbound"
          },
          ...
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="ba43a-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ba43a-131">Next steps</span></span>

<span data-ttu-id="ba43a-132">Visitare [il controllo di sicurezza gruppi (rete) con Watcher di rete](network-watcher-security-group-view-powershell.md) toolearn come tooautomate convalida dei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="ba43a-132">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


