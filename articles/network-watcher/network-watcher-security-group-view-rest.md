---
title: Analizzare la protezione di rete con la visualizzazione del gruppo di sicurezza di rete di Network Watcher di Azure - API REST | Documentazione Microsoft
description: Questo articolo descrive come usare PowerShell per analizzare la protezione di macchine virtuali con la visualizzazione di un gruppo di sicurezza.
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
ms.openlocfilehash: afced52b3ae6f3b7f400364f5ec7d049aa166590
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a><span data-ttu-id="f3ea5-103">Analizzare la protezione della macchina virtuale visualizzando un gruppo di sicurezza con l'API REST</span><span class="sxs-lookup"><span data-stu-id="f3ea5-103">Analyze your Virtual Machine security with Security Group View using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f3ea5-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3ea5-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="f3ea5-105">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="f3ea5-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="f3ea5-106">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="f3ea5-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="f3ea5-107">API REST</span><span class="sxs-lookup"><span data-stu-id="f3ea5-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="f3ea5-108">La visualizzazione di un gruppo di sicurezza consente di recuperare le regole di sicurezza di rete configurate ed effettive applicate a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f3ea5-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="f3ea5-109">Questa funzionalità è utile per controllare e diagnosticare i gruppi di sicurezza di rete e le regole configurate in una macchina virtuale per verificare che il traffico viene consentito o negato in modo corretto.</span><span class="sxs-lookup"><span data-stu-id="f3ea5-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="f3ea5-110">Questo articolo illustra come recuperare le regole di sicurezza effettive ed applicate a una macchina virtuale tramite l'API REST</span><span class="sxs-lookup"><span data-stu-id="f3ea5-110">In this article, we show you how to retrieve the effective and applied security rules to a virtual machine using REST API</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f3ea5-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="f3ea5-111">Before you begin</span></span>

<span data-ttu-id="f3ea5-112">In questo scenario, si chiama l'API REST di Network Watcher per ottenere la visualizzazione del gruppo di sicurezza per una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f3ea5-112">In this scenario, you call the Network Watcher Rest API to get the security group view for a virtual machine.</span></span> <span data-ttu-id="f3ea5-113">ARMclient viene usato per chiamare l'API REST con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3ea5-113">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="f3ea5-114">ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)</span><span class="sxs-lookup"><span data-stu-id="f3ea5-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="f3ea5-115">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="f3ea5-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="f3ea5-116">Lo scenario presuppone inoltre che esista e possa essere usato un gruppo di risorse con una macchina virtuale valida.</span><span class="sxs-lookup"><span data-stu-id="f3ea5-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="f3ea5-117">Scenario</span><span class="sxs-lookup"><span data-stu-id="f3ea5-117">Scenario</span></span>

<span data-ttu-id="f3ea5-118">Lo scenario illustrato in questo articolo recupera le regole di sicurezza effettive e applicate a una determinata macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f3ea5-118">The scenario covered in this article retrieves the effective and applied security rules for a given virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="f3ea5-119">Accedere con ARMClient</span><span class="sxs-lookup"><span data-stu-id="f3ea5-119">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="f3ea5-120">Recuperare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f3ea5-120">Retrieve a virtual machine</span></span>

<span data-ttu-id="f3ea5-121">Eseguire lo script seguente per restituire una macchina virtuale Il codice seguente necessita delle variabili:</span><span class="sxs-lookup"><span data-stu-id="f3ea5-121">Run the following script to return a virtual machineThe following code needs variables:</span></span>

- <span data-ttu-id="f3ea5-122">**subscriptionId**: l'ID sottoscrizione può essere recuperato anche con il cmdlet **Get-AzureRMSubscription**.</span><span class="sxs-lookup"><span data-stu-id="f3ea5-122">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="f3ea5-123">**resourceGroupName**: il nome di un gruppo di risorse contenente le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f3ea5-123">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="f3ea5-124">Le informazioni necessarie sono l'**id** sotto il tipo di `Microsoft.Compute/virtualMachines` in risposta, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f3ea5-124">The information that is needed is the **id** under the type `Microsoft.Compute/virtualMachines` in response, as seen in the following example:</span></span>

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

## <a name="get-security-group-view-for-virtual-machine"></a><span data-ttu-id="f3ea5-125">Ottenere la visualizzazione del gruppo di sicurezza per la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f3ea5-125">Get security group view for virtual machine</span></span>

<span data-ttu-id="f3ea5-126">Nell'esempio seguente viene richiesta la visualizzazione del gruppo di sicurezza di una macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="f3ea5-126">The following example requests the security group view of a targeted virtual machine.</span></span> <span data-ttu-id="f3ea5-127">I risultati di questo esempio possono essere usati per confrontare le regole e la sicurezza definite dall'origine per cercare la deviazione della configurazione.</span><span class="sxs-lookup"><span data-stu-id="f3ea5-127">The results from this example can be used to compare to the rules and security defined by the origination to look for configuration drift.</span></span>

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

## <a name="view-the-response"></a><span data-ttu-id="f3ea5-128">Visualizzare la risposta</span><span class="sxs-lookup"><span data-stu-id="f3ea5-128">View the response</span></span>

<span data-ttu-id="f3ea5-129">L'esempio seguente costituisce la risposta del comando precedente.</span><span class="sxs-lookup"><span data-stu-id="f3ea5-129">The following sample is the response returned from the preceding command.</span></span> <span data-ttu-id="f3ea5-130">I risultati mostrano tutte le regole di sicurezza effettive e applicate alla macchina virtuale, suddivise nei gruppi **NetworkInterfaceSecurityRules**, **DefaultSecurityRules** e **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="f3ea5-130">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f3ea5-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f3ea5-131">Next steps</span></span>

<span data-ttu-id="f3ea5-132">Consultare [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) (Verifica dei gruppi di sicurezza di rete con Network Watcher) per informazioni su come automatizzare la verifica dei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="f3ea5-132">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>


