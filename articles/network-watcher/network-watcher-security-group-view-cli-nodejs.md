---
title: Analizzare la sicurezza di rete con la visualizzazione del gruppo di sicurezza di Azure Network Watcher - Interfaccia della riga di comando di Azure 1.0 | Microsoft Docs
description: Questo articolo descrive come usare l'interfaccia della riga di comando di Azure 1.0 per analizzare la sicurezza di una macchina virtuale con la visualizzazione del gruppo di sicurezza.
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
ms.openlocfilehash: 2c4c494dcc4fe1a85c5feb29506c35fb03066479
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a><span data-ttu-id="a02b2-103">Analizzare la sicurezza della macchina virtuale con la visualizzazione del gruppo di sicurezza usando l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="a02b2-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a02b2-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a02b2-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="a02b2-105">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="a02b2-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="a02b2-106">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="a02b2-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="a02b2-107">API REST</span><span class="sxs-lookup"><span data-stu-id="a02b2-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="a02b2-108">La visualizzazione di un gruppo di sicurezza consente di recuperare le regole di sicurezza di rete configurate ed effettive applicate a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a02b2-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="a02b2-109">Questa funzionalità è utile per controllare e diagnosticare i gruppi di sicurezza di rete e le regole configurate in una macchina virtuale per verificare che il traffico viene consentito o negato in modo corretto.</span><span class="sxs-lookup"><span data-stu-id="a02b2-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="a02b2-110">Questo articolo illustra come recuperare le regole di sicurezza configurate ed effettive applicate a una macchina virtuale tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a02b2-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using Azure CLI</span></span>

<span data-ttu-id="a02b2-111">Questo articolo usa l'interfaccia della riga di comando di Azure 1.0 multipiattaforma, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="a02b2-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="a02b2-112">Network Watcher usa attualmente l'interfaccia della riga di comando di Azure 1.0 per il supporto dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="a02b2-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a02b2-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="a02b2-113">Before you begin</span></span>

<span data-ttu-id="a02b2-114">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="a02b2-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="a02b2-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="a02b2-115">Scenario</span></span>

<span data-ttu-id="a02b2-116">Lo scenario illustrato in questo articolo recupera le regole di sicurezza configurate ed effettive applicate a una determinata macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a02b2-116">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="a02b2-117">Ottenere una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a02b2-117">Get a VM</span></span>

<span data-ttu-id="a02b2-118">È necessario che una macchina virtuale esegua il cmdlet `vm list`.</span><span class="sxs-lookup"><span data-stu-id="a02b2-118">A virtual machine is required to run the `vm list` cmdlet.</span></span> <span data-ttu-id="a02b2-119">Il comando seguente elenca le macchine virtuali in un gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="a02b2-119">The following command lists the virtual machinese in a resource group:</span></span>

```azurecli
azure vm list -g resourceGroupName
```

<span data-ttu-id="a02b2-120">Se la macchina virtuale è nota, è possibile usare il cmdlet `vm show` per ottenere il relativo ID della risorsa:</span><span class="sxs-lookup"><span data-stu-id="a02b2-120">Once you know the virtual machine, you can use the `vm show` cmdlet to get its resource Id:</span></span>

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="a02b2-121">Recuperare la visualizzazione del gruppo di sicurezza</span><span class="sxs-lookup"><span data-stu-id="a02b2-121">Retrieve security group view</span></span>

<span data-ttu-id="a02b2-122">Il passaggio successivo prevede il recupero del risultato della visualizzazione del gruppo di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="a02b2-122">The next step is to retrieve the security group view result.</span></span> <span data-ttu-id="a02b2-123">L'aggiunta del flag "-json" restituisce un risultato in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="a02b2-123">Adding the "--json" flag will format the results in json.</span></span>

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-the-results"></a><span data-ttu-id="a02b2-124">Visualizzazione dei risultati</span><span class="sxs-lookup"><span data-stu-id="a02b2-124">Viewing the results</span></span>

<span data-ttu-id="a02b2-125">L'esempio seguente è una risposta abbreviata dei risultati restituiti.</span><span class="sxs-lookup"><span data-stu-id="a02b2-125">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="a02b2-126">I risultati mostrano tutte le regole di sicurezza effettive e applicate alla macchina virtuale, suddivise nei gruppi **NetworkInterfaceSecurityRules**, **DefaultSecurityRules** e **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="a02b2-126">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testnic",
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testvm",
          "securityRules": [
            {
              "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/test-nsg/securityRules/default-allow-rdp",
              "protocol": "TCP",
              "sourcePortRange": "*",
              "destinationPortRange": "3389",
              "sourceAddressPrefix": "*",
              "destinationAddressPrefix": "*",
              "access": "Allow",
              "priority": 1000,
              "direction": "Inbound",
              "provisioningState": "Succeeded",
              "name": "default-allow-rdp",
              "etag": "W/\"00000000-0000-0000-0000-000000000000\""
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/networkSecurityGroups//defaultSecurityRules/",
            "description": "Allow inbound traffic from all VMs in VNET",
            "protocol": "*",
            "sourcePortRange": "*",
            "destinationPortRange": "*",
            "sourceAddressPrefix": "VirtualNetwork",
            "destinationAddressPrefix": "VirtualNetwork",
            "access": "Allow",
            "priority": 65000,
            "direction": "Inbound",
            "provisioningState": "Succeeded",
            "name": "AllowVnetInBound"
          }
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="a02b2-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a02b2-127">Next steps</span></span>

<span data-ttu-id="a02b2-128">Consultare [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) (Verifica dei gruppi di sicurezza di rete con Network Watcher) per informazioni su come automatizzare la verifica dei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="a02b2-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>

<span data-ttu-id="a02b2-129">Per altre informazioni sulle regole di sicurezza applicate alle risorse di rete, leggere la [panoramica sulla visualizzazione di gruppo di sicurezza](network-watcher-security-group-view-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a02b2-129">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
