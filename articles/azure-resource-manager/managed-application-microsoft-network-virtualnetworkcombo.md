---
title: Elemento VirtualNetworkCombo dell'interfaccia utente di Applicazione gestita di Azure | Microsoft Docs
description: Illustra l'elemento Microsoft.Network.VirtualNetworkCombo dell'interfaccia utente per le applicazioni gestite di Azure
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 8bb255b76ac5c3de570fa569a1cfb3ee953f9687
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="0093c-103">Elemento Microsoft.Network.VirtualNetworkCombo dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="0093c-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="0093c-104">Gruppo di controlli per la selezione di una rete virtuale nuova o esistente.</span><span class="sxs-lookup"><span data-stu-id="0093c-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="0093c-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="0093c-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="0093c-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="0093c-106">UI sample</span></span>
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="0093c-108">Nel wireframe in alto l'utente ha selezionato una nuova rete virtuale, quindi può personalizzare il nome e il prefisso dell'indirizzo di ogni subnet.</span><span class="sxs-lookup"><span data-stu-id="0093c-108">In the top wireframe, the user has picked a new virtual network, so the user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="0093c-109">In questo caso la configurazione delle subnet è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="0093c-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="0093c-110">Nel wireframe in basso l'utente ha selezionato una rete virtuale esistente, quindi deve eseguire il mapping di ogni subnet necessaria per il modello di distribuzione a una subnet esistente.</span><span class="sxs-lookup"><span data-stu-id="0093c-110">In the bottom wireframe, the user has picked an existing virtual network, so the user must map each subnet the deployment template requires to an existing subnet.</span></span> <span data-ttu-id="0093c-111">In questo caso la configurazione delle subnet è obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="0093c-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="0093c-112">Schema</span><span class="sxs-lookup"><span data-stu-id="0093c-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="0093c-113">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="0093c-113">Remarks</span></span>
- <span data-ttu-id="0093c-114">Se specificato, il primo prefisso di indirizzo non sovrapposto di dimensioni pari a `defaultValue.addressPrefixSize` viene determinato automaticamente in base alle reti virtuali esistenti nella sottoscrizione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="0093c-114">If specified, the first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in the user's subscription.</span></span>
- <span data-ttu-id="0093c-115">Il valore predefinito per `defaultValue.name` e `defaultValue.addressPrefixSize` è **null**.</span><span class="sxs-lookup"><span data-stu-id="0093c-115">The default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="0093c-116">Specificare `constraints.minAddressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="0093c-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="0093c-117">Le reti virtuali esistenti con uno spazio indirizzi inferiore al valore specificato non sono disponibili per la selezione.</span><span class="sxs-lookup"><span data-stu-id="0093c-117">Any existing virtual networks with an address space smaller than the specified value are unavailable for selection.</span></span>
- <span data-ttu-id="0093c-118">Specificare `subnets` e specificare `constraints.minAddressPrefixSize` per ogni subnet.</span><span class="sxs-lookup"><span data-stu-id="0093c-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="0093c-119">Quando si crea una nuova rete virtuale, il prefisso dell'indirizzo di ogni subnet viene calcolato automaticamente in base al prefisso dell'indirizzo della rete virtuale e al rispettivo `addressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="0093c-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on the virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="0093c-120">Quando si usa una rete virtuale esistente, le subnet di dimensioni inferiori al rispettivo `constraints.minAddressPrefixSize` non sono disponibili per la selezione.</span><span class="sxs-lookup"><span data-stu-id="0093c-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="0093c-121">Inoltre, se specificato, le subnet che non contengono almeno `minAddressCount` indirizzi disponibili non sono disponibili per la selezione.</span><span class="sxs-lookup"><span data-stu-id="0093c-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="0093c-122">Il valore predefinito è **0**.</span><span class="sxs-lookup"><span data-stu-id="0093c-122">The default value is **0**.</span></span> <span data-ttu-id="0093c-123">Per assicurarsi che gli indirizzi disponibili siano contigui, specificare **true** per `requireContiguousAddresses`.</span><span class="sxs-lookup"><span data-stu-id="0093c-123">To ensure that the available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="0093c-124">Il valore predefinito è **true**.</span><span class="sxs-lookup"><span data-stu-id="0093c-124">The default value is **true**.</span></span>
- <span data-ttu-id="0093c-125">La creazione di subnet in una rete virtuale esistente non è supportata.</span><span class="sxs-lookup"><span data-stu-id="0093c-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="0093c-126">Se `options.hideExisting` è **true**, l'utente non può scegliere una rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="0093c-126">If `options.hideExisting` is **true**, the user can't choose an existing virtual network.</span></span> <span data-ttu-id="0093c-127">Il valore predefinito è **false**.</span><span class="sxs-lookup"><span data-stu-id="0093c-127">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="0093c-128">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="0093c-128">Sample output</span></span>
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="0093c-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0093c-129">Next steps</span></span>
* <span data-ttu-id="0093c-130">Per un'introduzione alle applicazioni gestite, vedere [Panoramica di Applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0093c-130">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="0093c-131">Per un'introduzione alla creazione delle definizioni dell'interfaccia utente, vedere [Introduzione a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0093c-131">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="0093c-132">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="0093c-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
