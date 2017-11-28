---
title: sicurezza di rete aaaAnalyze con visualizzazione gruppo di sicurezza di controllo di rete di Azure - CLI di Azure 2.0 | Documenti Microsoft
description: In questo articolo viene descritto come tooanalyze toouse CLI di Azure 2.0 a virtuale macchine protezione con visualizzazione del gruppo di sicurezza.
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
ms.openlocfilehash: 31a4cd628f54d7548f495251fd275f099e79a060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-20"></a><span data-ttu-id="45ec2-103">Analizzare la sicurezza della macchina virtuale con la visualizzazione del gruppo di sicurezza usando l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="45ec2-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="45ec2-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="45ec2-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="45ec2-105">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="45ec2-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="45ec2-106">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="45ec2-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="45ec2-107">API REST</span><span class="sxs-lookup"><span data-stu-id="45ec2-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="45ec2-108">Visualizzazione del gruppo di sicurezza restituisce regole di sicurezza di rete configurate ed efficace di macchina virtuale tooa applicato.</span><span class="sxs-lookup"><span data-stu-id="45ec2-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="45ec2-109">Questa funzionalità è utile tooaudit e diagnosticare i gruppi di sicurezza di rete e le regole configurate per il traffico tooensure una macchina virtuale viene correttamente consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="45ec2-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="45ec2-110">In questo articolo viene illustrata la modalità di configurazione tooretrieve hello e la macchina virtuale di sicurezza efficace regole tooa mediante Azure CLI</span><span class="sxs-lookup"><span data-stu-id="45ec2-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using Azure CLI</span></span>


<span data-ttu-id="45ec2-111">In questo articolo utilizza la nuova generazione CLI per modello di distribuzione Gestione risorse hello, CLI di Azure 2.0, che è disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="45ec2-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="45ec2-112">hello tooperform i passaggi in questo articolo, è necessario troppo[installare hello interfaccia della riga di comando di Azure per Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="45ec2-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="45ec2-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="45ec2-113">Before you begin</span></span>

<span data-ttu-id="45ec2-114">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="45ec2-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="45ec2-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="45ec2-115">Scenario</span></span>

<span data-ttu-id="45ec2-116">scenario di Hello illustrato in questo articolo recupera hello configurato e le regole di sicurezza efficace per una macchina virtuale specificata.</span><span class="sxs-lookup"><span data-stu-id="45ec2-116">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="45ec2-117">Ottenere una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="45ec2-117">Get a VM</span></span>

<span data-ttu-id="45ec2-118">Una macchina virtuale è obbligatorio toorun hello `vm list` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="45ec2-118">A virtual machine is required toorun hello `vm list` cmdlet.</span></span> <span data-ttu-id="45ec2-119">Hello comando riportato di seguito sono elencate hello le macchine virtuali in un gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="45ec2-119">hello following command lists hello virtual machines in a resource group:</span></span>

```azurecli
az vm list -resource-group resourceGroupName
```

<span data-ttu-id="45ec2-120">Quando si è certi di macchina virtuale hello, è possibile utilizzare hello `vm show` tooget cmdlet relativi Id di risorsa:</span><span class="sxs-lookup"><span data-stu-id="45ec2-120">Once you know hello virtual machine, you can use hello `vm show` cmdlet tooget its resource Id:</span></span>

```azurecli
az vm show -resource-group resourceGroupName -name virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="45ec2-121">Recuperare la visualizzazione del gruppo di sicurezza</span><span class="sxs-lookup"><span data-stu-id="45ec2-121">Retrieve security group view</span></span>

<span data-ttu-id="45ec2-122">passaggio successivo Hello è tooretrieve hello sicurezza gruppo Visualizza il risultato.</span><span class="sxs-lookup"><span data-stu-id="45ec2-122">hello next step is tooretrieve hello security group view result.</span></span>

```azurecli
az network watcher show-security-group-view --resource-group resourceGroupName --vm vmName
```

## <a name="viewing-hello-results"></a><span data-ttu-id="45ec2-123">Visualizzazione dei risultati hello</span><span class="sxs-lookup"><span data-stu-id="45ec2-123">Viewing hello results</span></span>

<span data-ttu-id="45ec2-124">Hello seguito è riportata una risposta abbreviata di hello risultati restituiti.</span><span class="sxs-lookup"><span data-stu-id="45ec2-124">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="45ec2-125">Hello risultati mostrano tutte le regole di sicurezza efficace e applicato hello nella macchina virtuale hello suddiviso in gruppi di **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, e  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="45ec2-125">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="45ec2-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45ec2-126">Next steps</span></span>

<span data-ttu-id="45ec2-127">Visitare [il controllo di sicurezza gruppi (rete) con Watcher di rete](network-watcher-nsg-auditing-powershell.md) toolearn come tooautomate convalida dei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="45ec2-127">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>

<span data-ttu-id="45ec2-128">Ulteriori informazioni sulle regole di sicurezza hello che sono risorse di rete applicati tooyour visitando [Visualizza panoramica gruppo di sicurezza](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="45ec2-128">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
