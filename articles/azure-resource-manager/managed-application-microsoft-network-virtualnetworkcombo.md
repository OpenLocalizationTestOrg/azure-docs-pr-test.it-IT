---
title: elemento gestita dell'interfaccia utente dell'applicazione VirtualNetworkCombo aaaAzure | Documenti Microsoft
description: Descrive l'elemento dell'interfaccia utente Microsoft.Network.VirtualNetworkCombo hello per le applicazioni gestite di Azure
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
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="f4cec-103">Elemento Microsoft.Network.VirtualNetworkCombo dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="f4cec-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="f4cec-104">Gruppo di controlli per la selezione di una rete virtuale nuova o esistente.</span><span class="sxs-lookup"><span data-stu-id="f4cec-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="f4cec-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="f4cec-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="f4cec-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="f4cec-106">UI sample</span></span>
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="f4cec-108">In wireframe superiore hello, utente hello ha selezionato una nuova rete virtuale, in modo da Personalizza il prefisso di nome e l'indirizzo della subnet, ogni utente hello.</span><span class="sxs-lookup"><span data-stu-id="f4cec-108">In hello top wireframe, hello user has picked a new virtual network, so hello user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="f4cec-109">In questo caso la configurazione delle subnet è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="f4cec-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="f4cec-110">In hello inferiore wireframe, utente hello è selezionato di una rete virtuale esistente, pertanto è necessario eseguire il mapping utente hello ogni modello di distribuzione hello subnet richiede tooan esistente subnet.</span><span class="sxs-lookup"><span data-stu-id="f4cec-110">In hello bottom wireframe, hello user has picked an existing virtual network, so hello user must map each subnet hello deployment template requires tooan existing subnet.</span></span> <span data-ttu-id="f4cec-111">In questo caso la configurazione delle subnet è obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="f4cec-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="f4cec-112">Schema</span><span class="sxs-lookup"><span data-stu-id="f4cec-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="f4cec-113">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="f4cec-113">Remarks</span></span>
- <span data-ttu-id="f4cec-114">Se specificato, hello prima non sovrapposti prefisso dell'indirizzo dimensioni `defaultValue.addressPrefixSize` viene determinato automaticamente in base alle reti virtuali esistenti nella sottoscrizione hello dell'utente.</span><span class="sxs-lookup"><span data-stu-id="f4cec-114">If specified, hello first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in hello user's subscription.</span></span>
- <span data-ttu-id="f4cec-115">il valore predefinito per Hello `defaultValue.name` e `defaultValue.addressPrefixSize` è **null**.</span><span class="sxs-lookup"><span data-stu-id="f4cec-115">hello default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="f4cec-116">Specificare `constraints.minAddressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="f4cec-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="f4cec-117">Qualsiasi rete virtuale esistente con uno spazio di indirizzi più piccolo di quelli hello valore specificato non sono disponibili per la selezione.</span><span class="sxs-lookup"><span data-stu-id="f4cec-117">Any existing virtual networks with an address space smaller than hello specified value are unavailable for selection.</span></span>
- <span data-ttu-id="f4cec-118">Specificare `subnets` e specificare `constraints.minAddressPrefixSize` per ogni subnet.</span><span class="sxs-lookup"><span data-stu-id="f4cec-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="f4cec-119">Quando si crea una nuova rete virtuale, viene calcolato automaticamente in base prefisso dell'indirizzo della subnet ogni sul prefisso dell'indirizzo della rete virtuale hello e la rispettiva `addressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="f4cec-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on hello virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="f4cec-120">Quando si usa una rete virtuale esistente, le subnet di dimensioni inferiori al rispettivo `constraints.minAddressPrefixSize` non sono disponibili per la selezione.</span><span class="sxs-lookup"><span data-stu-id="f4cec-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="f4cec-121">Inoltre, se specificato, le subnet che non contengono almeno `minAddressCount` indirizzi disponibili non sono disponibili per la selezione.</span><span class="sxs-lookup"><span data-stu-id="f4cec-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="f4cec-122">valore predefinito di Hello è **0**.</span><span class="sxs-lookup"><span data-stu-id="f4cec-122">hello default value is **0**.</span></span> <span data-ttu-id="f4cec-123">tooensure che hello indirizzi disponibili sono contigui, specificare **true** per `requireContiguousAddresses`.</span><span class="sxs-lookup"><span data-stu-id="f4cec-123">tooensure that hello available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="f4cec-124">valore predefinito di Hello è **true**.</span><span class="sxs-lookup"><span data-stu-id="f4cec-124">hello default value is **true**.</span></span>
- <span data-ttu-id="f4cec-125">La creazione di subnet in una rete virtuale esistente non è supportata.</span><span class="sxs-lookup"><span data-stu-id="f4cec-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="f4cec-126">Se `options.hideExisting` è **true**, utente hello non è possibile scegliere una rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="f4cec-126">If `options.hideExisting` is **true**, hello user can't choose an existing virtual network.</span></span> <span data-ttu-id="f4cec-127">valore predefinito di Hello è **false**.</span><span class="sxs-lookup"><span data-stu-id="f4cec-127">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="f4cec-128">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="f4cec-128">Sample output</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="f4cec-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f4cec-129">Next steps</span></span>
* <span data-ttu-id="f4cec-130">Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4cec-130">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="f4cec-131">Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4cec-131">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="f4cec-132">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="f4cec-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
