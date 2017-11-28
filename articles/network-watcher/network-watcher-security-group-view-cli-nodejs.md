---
title: sicurezza di rete aaaAnalyze con visualizzazione gruppo di sicurezza di controllo di rete di Azure - CLI di Azure 1.0 | Documenti Microsoft
description: In questo articolo viene descritto come tooanalyze toouse CLI di Azure 1.0 a virtuale macchine protezione con visualizzazione del gruppo di sicurezza.
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
ms.openlocfilehash: 96383a734b94d215d5b0f3d47339e46940d700b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a><span data-ttu-id="b8648-103">Analizzare la sicurezza della macchina virtuale con la visualizzazione del gruppo di sicurezza usando l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="b8648-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="b8648-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8648-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="b8648-105">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="b8648-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="b8648-106">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="b8648-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="b8648-107">API REST</span><span class="sxs-lookup"><span data-stu-id="b8648-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="b8648-108">Visualizzazione del gruppo di sicurezza restituisce regole di sicurezza di rete configurate ed efficace di macchina virtuale tooa applicato.</span><span class="sxs-lookup"><span data-stu-id="b8648-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="b8648-109">Questa funzionalità è utile tooaudit e diagnosticare i gruppi di sicurezza di rete e le regole configurate per il traffico tooensure una macchina virtuale viene correttamente consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="b8648-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="b8648-110">In questo articolo viene illustrata la modalità di configurazione tooretrieve hello e la macchina virtuale di sicurezza efficace regole tooa mediante Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b8648-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using Azure CLI</span></span>

<span data-ttu-id="b8648-111">Questo articolo usa l'interfaccia della riga di comando di Azure 1.0 multipiattaforma, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="b8648-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="b8648-112">Network Watcher usa attualmente l'interfaccia della riga di comando di Azure 1.0 per il supporto dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="b8648-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b8648-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="b8648-113">Before you begin</span></span>

<span data-ttu-id="b8648-114">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="b8648-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="b8648-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="b8648-115">Scenario</span></span>

<span data-ttu-id="b8648-116">scenario di Hello illustrato in questo articolo recupera hello configurato e le regole di sicurezza efficace per una macchina virtuale specificata.</span><span class="sxs-lookup"><span data-stu-id="b8648-116">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="b8648-117">Ottenere una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b8648-117">Get a VM</span></span>

<span data-ttu-id="b8648-118">Una macchina virtuale è obbligatorio toorun hello `vm list` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b8648-118">A virtual machine is required toorun hello `vm list` cmdlet.</span></span> <span data-ttu-id="b8648-119">Hello comando riportato di seguito sono elencate hello machinese virtuale in un gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="b8648-119">hello following command lists hello virtual machinese in a resource group:</span></span>

```azurecli
azure vm list -g resourceGroupName
```

<span data-ttu-id="b8648-120">Quando si è certi di macchina virtuale hello, è possibile utilizzare hello `vm show` tooget cmdlet relativi Id di risorsa:</span><span class="sxs-lookup"><span data-stu-id="b8648-120">Once you know hello virtual machine, you can use hello `vm show` cmdlet tooget its resource Id:</span></span>

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="b8648-121">Recuperare la visualizzazione del gruppo di sicurezza</span><span class="sxs-lookup"><span data-stu-id="b8648-121">Retrieve security group view</span></span>

<span data-ttu-id="b8648-122">passaggio successivo Hello è tooretrieve hello sicurezza gruppo Visualizza il risultato.</span><span class="sxs-lookup"><span data-stu-id="b8648-122">hello next step is tooretrieve hello security group view result.</span></span> <span data-ttu-id="b8648-123">Aggiunta di hello "--json" flag verrà formattare i risultati di hello in json.</span><span class="sxs-lookup"><span data-stu-id="b8648-123">Adding hello "--json" flag will format hello results in json.</span></span>

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-hello-results"></a><span data-ttu-id="b8648-124">Visualizzazione dei risultati hello</span><span class="sxs-lookup"><span data-stu-id="b8648-124">Viewing hello results</span></span>

<span data-ttu-id="b8648-125">Hello seguito è riportata una risposta abbreviata di hello risultati restituiti.</span><span class="sxs-lookup"><span data-stu-id="b8648-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="b8648-126">Hello risultati mostrano tutte le regole di sicurezza efficace e applicato hello nella macchina virtuale hello suddiviso in gruppi di **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, e  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="b8648-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b8648-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b8648-127">Next steps</span></span>

<span data-ttu-id="b8648-128">Visitare [il controllo di sicurezza gruppi (rete) con Watcher di rete](network-watcher-nsg-auditing-powershell.md) toolearn come tooautomate convalida dei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="b8648-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>

<span data-ttu-id="b8648-129">Ulteriori informazioni sulle regole di sicurezza hello che sono risorse di rete applicati tooyour visitando [Visualizza panoramica gruppo di sicurezza](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b8648-129">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
