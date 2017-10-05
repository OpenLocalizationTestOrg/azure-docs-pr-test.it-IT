---
title: Analizzare la sicurezza di rete con la visualizzazione del gruppo di sicurezza di Azure Network Watcher - Interfaccia della riga di comando di Azure 2.0 | Microsoft Docs
description: Questo articolo descrive come usare l'interfaccia della riga di comando di Azure 2.0 per analizzare la sicurezza di una macchina virtuale con la visualizzazione del gruppo di sicurezza.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a986ff4f-7e0c-4994-95e1-4ac824986500
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 1756e14819e3b7c79361c193413a1fcd7f24a4e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-20"></a><span data-ttu-id="00616-103">Analizzare la sicurezza della macchina virtuale con la visualizzazione del gruppo di sicurezza usando l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="00616-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="00616-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="00616-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="00616-105">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="00616-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="00616-106">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="00616-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="00616-107">API REST</span><span class="sxs-lookup"><span data-stu-id="00616-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="00616-108">La visualizzazione di un gruppo di sicurezza consente di recuperare le regole di sicurezza di rete configurate ed effettive applicate a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="00616-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="00616-109">Questa funzionalità è utile per controllare e diagnosticare i gruppi di sicurezza di rete e le regole configurate in una macchina virtuale per verificare che il traffico viene consentito o negato in modo corretto.</span><span class="sxs-lookup"><span data-stu-id="00616-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="00616-110">Questo articolo illustra come recuperare le regole di sicurezza configurate ed effettive applicate a una macchina virtuale tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="00616-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using Azure CLI</span></span>


<span data-ttu-id="00616-111">Questo articolo usa l'interfaccia della riga di comando di nuova generazione per il modello di distribuzione di gestione delle risorse, ovvero l'interfaccia della riga di comando di Azure 2.0, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="00616-111">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="00616-112">Per eseguire i passaggi indicati in questo articolo è necessario [installare l'interfaccia della riga di comando di Azure per Mac, Linux e Windows (interfaccia della riga di comando di Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="00616-112">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="00616-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="00616-113">Before you begin</span></span>

<span data-ttu-id="00616-114">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="00616-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="00616-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="00616-115">Scenario</span></span>

<span data-ttu-id="00616-116">Lo scenario illustrato in questo articolo recupera le regole di sicurezza configurate ed effettive applicate a una determinata macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="00616-116">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="00616-117">Ottenere una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="00616-117">Get a VM</span></span>

<span data-ttu-id="00616-118">È necessario che una macchina virtuale esegua il cmdlet `vm list`.</span><span class="sxs-lookup"><span data-stu-id="00616-118">A virtual machine is required to run the `vm list` cmdlet.</span></span> <span data-ttu-id="00616-119">Il comando seguente elenca le macchine virtuali in un gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="00616-119">The following command lists the virtual machines in a resource group:</span></span>

```azurecli
az vm list -resource-group resourceGroupName
```

<span data-ttu-id="00616-120">Se la macchina virtuale è nota, è possibile usare il cmdlet `vm show` per ottenere il relativo ID della risorsa:</span><span class="sxs-lookup"><span data-stu-id="00616-120">Once you know the virtual machine, you can use the `vm show` cmdlet to get its resource Id:</span></span>

```azurecli
az vm show -resource-group resourceGroupName -name virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="00616-121">Recuperare la visualizzazione del gruppo di sicurezza</span><span class="sxs-lookup"><span data-stu-id="00616-121">Retrieve security group view</span></span>

<span data-ttu-id="00616-122">Il passaggio successivo prevede il recupero del risultato della visualizzazione del gruppo di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="00616-122">The next step is to retrieve the security group view result.</span></span>

```azurecli
az network watcher show-security-group-view --resource-group resourceGroupName --vm vmName
```

## <a name="viewing-the-results"></a><span data-ttu-id="00616-123">Visualizzazione dei risultati</span><span class="sxs-lookup"><span data-stu-id="00616-123">Viewing the results</span></span>

<span data-ttu-id="00616-124">L'esempio seguente è una risposta abbreviata dei risultati restituiti.</span><span class="sxs-lookup"><span data-stu-id="00616-124">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="00616-125">I risultati mostrano tutte le regole di sicurezza effettive e applicate alla macchina virtuale, suddivise nei gruppi **NetworkInterfaceSecurityRules**, **DefaultSecurityRules** e **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="00616-125">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
      "resourceGroup": "{resourceGroupName}",
      "securityRuleAssociations": {
        "defaultSecurityRules": [
          {
            "access": "Allow",
            "description": "Allow inbound traffic from all VMs in VNET",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "*",
            "direction": "Inbound",
            "etag": null,
            "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups//providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/AllowVnetInBound",
            "name": "AllowVnetInBound",
            "priority": 65000,
            "protocol": "*",
            "provisioningState": "Succeeded",
            "resourceGroup": "",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "*"
          }...
        ],
        "effectiveSecurityRules": [
          {
            "access": "Deny",
            "destinationAddressPrefix": "*",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": null,
            "expandedSourceAddressPrefix": null,
            "name": "DefaultOutboundDenyAll",
            "priority": 65500,
            "protocol": "All",
            "sourceAddressPrefix": "*",
            "sourcePortRange": "0-65535"
          },
          {
            "access": "Allow",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "expandedSourceAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "name": "DefaultRule_AllowVnetOutBound",
            "priority": 65000,
            "protocol": "All",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "0-65535"
          },...
        ],
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "resourceGroup": "{resourceGroupName}",
          "securityRules": [
            {
              "access": "Allow",
              "description": null,
              "destinationAddressPrefix": "*",
              "destinationPortRange": "3389",
              "direction": "Inbound",
              "etag": "W/\"efb606c1-2d54-475a-ab20-da3f80393577\"",
              "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "name": "default-allow-rdp",
              "priority": 1000,
              "protocol": "TCP",
              "provisioningState": "Succeeded",
              "resourceGroup": "{resourceGroupName}",
              "sourceAddressPrefix": "*",
              "sourcePortRange": "*"
            }
          ]
        },
        "subnetAssociation": null
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="00616-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="00616-126">Next steps</span></span>

<span data-ttu-id="00616-127">Consultare [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) (Verifica dei gruppi di sicurezza di rete con Network Watcher) per informazioni su come automatizzare la verifica dei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="00616-127">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>

<span data-ttu-id="00616-128">Per altre informazioni sulle regole di sicurezza applicate alle risorse di rete, leggere la [panoramica sulla visualizzazione di gruppo di sicurezza](network-watcher-security-group-view-overview.md).</span><span class="sxs-lookup"><span data-stu-id="00616-128">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
