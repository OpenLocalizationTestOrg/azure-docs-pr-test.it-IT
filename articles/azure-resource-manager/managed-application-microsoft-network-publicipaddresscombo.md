---
title: elemento gestita dell'interfaccia utente dell'applicazione PublicIpAddressCombo aaaAzure | Documenti Microsoft
description: Descrive l'elemento dell'interfaccia utente Microsoft.Network.PublicIpAddressCombo hello per le applicazioni gestite di Azure
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
ms.openlocfilehash: 8ba689005c0eccda0a57bf628de4b5197886a950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="fe59f-103">Elemento Microsoft.Network.PublicIpAddressCombo dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="fe59f-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="fe59f-104">Gruppo di controlli per la selezione di un indirizzo IP pubblico nuovo o esistente.</span><span class="sxs-lookup"><span data-stu-id="fe59f-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="fe59f-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="fe59f-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="fe59f-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="fe59f-106">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="fe59f-108">Se l'utente di hello seleziona 'None' per l'indirizzo IP pubblico, casella di testo etichetta nome dominio hello è nascosto.</span><span class="sxs-lookup"><span data-stu-id="fe59f-108">If hello user selects 'None' for public IP address, hello domain name label text box is hidden.</span></span>
- <span data-ttu-id="fe59f-109">Se l'utente di hello seleziona un indirizzo IP pubblico esistente, casella di testo etichetta nome dominio hello è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="fe59f-109">If hello user selects an existing public IP address, hello domain name label text box is disabled.</span></span> <span data-ttu-id="fe59f-110">Il valore è l'etichetta del nome di dominio dell'indirizzo IP selezionato hello hello.</span><span class="sxs-lookup"><span data-stu-id="fe59f-110">Its value is hello domain name label of hello selected IP address.</span></span>
- <span data-ttu-id="fe59f-111">aggiornamenti (ad esempio, westus.cloudapp.azure.com) suffisso nome dominio Hello automaticamente in base alla posizione di hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="fe59f-111">hello domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on hello selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="fe59f-112">Schema</span><span class="sxs-lookup"><span data-stu-id="fe59f-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="fe59f-113">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="fe59f-113">Remarks</span></span>
- <span data-ttu-id="fe59f-114">Se `constraints.required.domainNameLabel` è troppo**true**, utente di hello deve fornire un'etichetta del nome di dominio quando si crea un nuovo indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="fe59f-114">If `constraints.required.domainNameLabel` is set too**true**, hello user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="fe59f-115">Gli indirizzi IP pubblici esistenti senza etichetta non sono disponibili per la selezione.</span><span class="sxs-lookup"><span data-stu-id="fe59f-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="fe59f-116">Se `options.hideNone` è troppo**true**, quindi hello opzione tooselect **Nessuno** per indirizzo IP pubblico hello indirizzo è nascosto.</span><span class="sxs-lookup"><span data-stu-id="fe59f-116">If `options.hideNone` is set too**true**, then hello option tooselect **None** for hello public IP address is hidden.</span></span> <span data-ttu-id="fe59f-117">valore predefinito di Hello è **false**.</span><span class="sxs-lookup"><span data-stu-id="fe59f-117">hello default value is **false**.</span></span>
- <span data-ttu-id="fe59f-118">Se `options.hideDomainNameLabel` è troppo**true**, quindi la casella di testo hello per l'etichetta del nome di dominio è nascosto.</span><span class="sxs-lookup"><span data-stu-id="fe59f-118">If `options.hideDomainNameLabel` is set too**true**, then hello text box for domain name label is hidden.</span></span> <span data-ttu-id="fe59f-119">valore predefinito di Hello è **false**.</span><span class="sxs-lookup"><span data-stu-id="fe59f-119">hello default value is **false**.</span></span>
- <span data-ttu-id="fe59f-120">Se `options.hideExisting` è true, l'utente hello non sarà in grado di toochoose un indirizzo IP pubblico esistente.</span><span class="sxs-lookup"><span data-stu-id="fe59f-120">If `options.hideExisting` is true, then hello user is not able toochoose an existing public IP address.</span></span> <span data-ttu-id="fe59f-121">valore predefinito di Hello è **false**.</span><span class="sxs-lookup"><span data-stu-id="fe59f-121">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="fe59f-122">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="fe59f-122">Sample output</span></span>
<span data-ttu-id="fe59f-123">Se l'utente di hello non seleziona alcun indirizzo IP pubblico, hello viene visualizzato output seguente:</span><span class="sxs-lookup"><span data-stu-id="fe59f-123">If hello user selects no public IP address, hello following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="fe59f-124">Se l'utente di hello seleziona un indirizzo IP nuovo o esistente, hello viene visualizzato output seguente:</span><span class="sxs-lookup"><span data-stu-id="fe59f-124">If hello user selects a new or existing IP address, hello following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="fe59f-125">Quando `options.hideNone` è specificato, `newOrExistingOrNone` restituisce sempre **none**.</span><span class="sxs-lookup"><span data-stu-id="fe59f-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="fe59f-126">Quando `options.hideDomainNameLabel` è specificato, `domainNameLabel` non viene dichiarato.</span><span class="sxs-lookup"><span data-stu-id="fe59f-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe59f-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fe59f-127">Next steps</span></span>
* <span data-ttu-id="fe59f-128">Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fe59f-128">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="fe59f-129">Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fe59f-129">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="fe59f-130">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="fe59f-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
