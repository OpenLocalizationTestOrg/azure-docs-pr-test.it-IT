---
title: Elemento PublicIpAddressCombo dell'interfaccia utente di Applicazione gestita di Azure | Microsoft Docs
description: Illustra l'elemento Microsoft.Network.PublicIpAddressCombo dell'interfaccia utente per le applicazioni gestite di Azure
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
ms.openlocfilehash: 2eb773f5f0cf389fc39bc3a0f5fbf9ac726d1949
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="52136-103">Elemento Microsoft.Network.PublicIpAddressCombo dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="52136-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="52136-104">Gruppo di controlli per la selezione di un indirizzo IP pubblico nuovo o esistente.</span><span class="sxs-lookup"><span data-stu-id="52136-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="52136-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="52136-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="52136-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="52136-106">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="52136-108">Se l'utente seleziona "Nessuno" come indirizzo IP pubblico, la casella di testo dell'etichetta del nome di dominio viene nascosta.</span><span class="sxs-lookup"><span data-stu-id="52136-108">If the user selects 'None' for public IP address, the domain name label text box is hidden.</span></span>
- <span data-ttu-id="52136-109">Se l'utente seleziona un indirizzo IP pubblico esistente, la casella di testo dell'etichetta del nome di dominio viene disabilitata</span><span class="sxs-lookup"><span data-stu-id="52136-109">If the user selects an existing public IP address, the domain name label text box is disabled.</span></span> <span data-ttu-id="52136-110">e il valore corrisponderà all'etichetta del nome di dominio dell'indirizzo IP selezionato.</span><span class="sxs-lookup"><span data-stu-id="52136-110">Its value is the domain name label of the selected IP address.</span></span>
- <span data-ttu-id="52136-111">Il suffisso del nome di dominio (ad esempio, westus.cloudapp.azure.com) viene aggiornato automaticamente in base alla posizione selezionata.</span><span class="sxs-lookup"><span data-stu-id="52136-111">The domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on the selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="52136-112">Schema</span><span class="sxs-lookup"><span data-stu-id="52136-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.PublicIpAddressCombo",
  "label": {
    "publicIpAddress": "Public IP address",
    "domainNameLabel": "Domain name label"
  },
  "toolTip": {
    "publicIpAddress": "",
    "domainNameLabel": ""
  },
  "defaultValue": {
    "publicIpAddressName": "ip01",
    "domainNameLabel": "foobar"
  },
  "constraints": {
    "required": {
      "domainNameLabel": true
    }
  },
  "options": {
    "hideNone": false,
    "hideDomainNameLabel": false,
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="52136-113">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="52136-113">Remarks</span></span>
- <span data-ttu-id="52136-114">Se `constraints.required.domainNameLabel` è impostato su **true**, l'utente deve specificare un'etichetta di nome di dominio quando crea un nuovo indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="52136-114">If `constraints.required.domainNameLabel` is set to **true**, the user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="52136-115">Gli indirizzi IP pubblici esistenti senza etichetta non sono disponibili per la selezione.</span><span class="sxs-lookup"><span data-stu-id="52136-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="52136-116">Se `options.hideNone` è impostato su **true**, l'opzione per selezionare **Nessuno** per l'indirizzo IP pubblico viene nascosta.</span><span class="sxs-lookup"><span data-stu-id="52136-116">If `options.hideNone` is set to **true**, then the option to select **None** for the public IP address is hidden.</span></span> <span data-ttu-id="52136-117">Il valore predefinito è **false**.</span><span class="sxs-lookup"><span data-stu-id="52136-117">The default value is **false**.</span></span>
- <span data-ttu-id="52136-118">Se `options.hideDomainNameLabel` è impostato su **true**, la casella di testo per l'etichetta del nome di dominio viene nascosta.</span><span class="sxs-lookup"><span data-stu-id="52136-118">If `options.hideDomainNameLabel` is set to **true**, then the text box for domain name label is hidden.</span></span> <span data-ttu-id="52136-119">Il valore predefinito è **false**.</span><span class="sxs-lookup"><span data-stu-id="52136-119">The default value is **false**.</span></span>
- <span data-ttu-id="52136-120">Se `options.hideExisting` è true, l'utente non può scegliere un indirizzo IP pubblico esistente.</span><span class="sxs-lookup"><span data-stu-id="52136-120">If `options.hideExisting` is true, then the user is not able to choose an existing public IP address.</span></span> <span data-ttu-id="52136-121">Il valore predefinito è **false**.</span><span class="sxs-lookup"><span data-stu-id="52136-121">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="52136-122">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="52136-122">Sample output</span></span>
<span data-ttu-id="52136-123">Se l'utente non seleziona alcun indirizzo IP pubblico, è previsto l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="52136-123">If the user selects no public IP address, the following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="52136-124">Se l'utente seleziona un indirizzo IP pubblico nuovo o esistente, è previsto l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="52136-124">If the user selects a new or existing IP address, the following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="52136-125">Quando `options.hideNone` è specificato, `newOrExistingOrNone` restituisce sempre **none**.</span><span class="sxs-lookup"><span data-stu-id="52136-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="52136-126">Quando `options.hideDomainNameLabel` è specificato, `domainNameLabel` non viene dichiarato.</span><span class="sxs-lookup"><span data-stu-id="52136-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52136-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="52136-127">Next steps</span></span>
* <span data-ttu-id="52136-128">Per un'introduzione alle applicazioni gestite, vedere [Panoramica di Applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="52136-128">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="52136-129">Per un'introduzione alla creazione delle definizioni dell'interfaccia utente, vedere [Introduzione a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="52136-129">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="52136-130">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="52136-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
