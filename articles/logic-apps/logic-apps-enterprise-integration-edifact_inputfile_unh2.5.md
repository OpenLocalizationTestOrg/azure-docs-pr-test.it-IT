---
title: La decodifica edifact delle app per la logica B2B risolve UNH2.5 - App per la logica di Azure | Microsoft Docs
description: La decodifica edifact delle app per la logica di Azure B2B risolve UNH2.5
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 62ad8183cc6e9f56255b2729a04ee7710d00a21a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-handle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="964fb-103">Come gestire documenti EDIFACT con un segmento UNH2.5</span><span class="sxs-lookup"><span data-stu-id="964fb-103">How to handle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="964fb-104">Quando nel documento EDIFACT è presente un segmento UNH 2.5, viene usato per la ricerca dello schema.</span><span class="sxs-lookup"><span data-stu-id="964fb-104">When UNH2.5 is present in the EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="964fb-105">Esempio: il campo UNH è **EAN008** nel messaggio EDIFACT</span><span class="sxs-lookup"><span data-stu-id="964fb-105">Example: The UNH field is **EAN008** in the EDIFACT message</span></span>  
<span data-ttu-id="964fb-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span><span class="sxs-lookup"><span data-stu-id="964fb-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="964fb-107">Procedura da seguire per gestire il messaggio</span><span class="sxs-lookup"><span data-stu-id="964fb-107">Steps to follow to handle the message</span></span> 
1. <span data-ttu-id="964fb-108">Aggiornare lo schema</span><span class="sxs-lookup"><span data-stu-id="964fb-108">Update the schema</span></span>
2. <span data-ttu-id="964fb-109">Controllare le impostazioni del contratto</span><span class="sxs-lookup"><span data-stu-id="964fb-109">Check the agreement settings</span></span>  

## <a name="update-the-schema"></a><span data-ttu-id="964fb-110">Aggiornare lo schema</span><span class="sxs-lookup"><span data-stu-id="964fb-110">Update the schema</span></span>
<span data-ttu-id="964fb-111">Per elaborare il messaggio, è necessario distribuire uno schema con il nome del nodo radice UNH 2.5.</span><span class="sxs-lookup"><span data-stu-id="964fb-111">To process the message, you need to deploy a schema with the UNH2.5 root node name.</span></span>  <span data-ttu-id="964fb-112">Il nome radice dello schema ad esempio sarebbe **EFACT_D03B_ORDERS_EAN008**</span><span class="sxs-lookup"><span data-stu-id="964fb-112">For given an example, the schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="964fb-113">Per ogni D03B_ORDERS con un diverso segmento UNH2.5, è necessario distribuire uno schema individuale.</span><span class="sxs-lookup"><span data-stu-id="964fb-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have to deploy an individual schema.</span></span>  

## <a name="add-schema-to-the-edifact-agreement"></a><span data-ttu-id="964fb-114">Aggiungere lo schema al contratto EDIFACT</span><span class="sxs-lookup"><span data-stu-id="964fb-114">Add schema to the EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="964fb-115">Decodifica EDIFACT</span><span class="sxs-lookup"><span data-stu-id="964fb-115">EDIFACT Decode</span></span>
<span data-ttu-id="964fb-116">Per decodificare il messaggio in arrivo, configurare lo schema nelle impostazioni di ricezione del contratto EDIFACT</span><span class="sxs-lookup"><span data-stu-id="964fb-116">To Decode the incoming message, configure the schema in the EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="964fb-117">Aggiungere lo schema all'account di integrazione</span><span class="sxs-lookup"><span data-stu-id="964fb-117">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="964fb-118">Configurare lo schema nelle impostazioni di ricezione del contratto EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="964fb-118">Configure the schema in the EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="964fb-119">Selezionare il contratto EDIFACT e fare clic su **Modifica come JSON**.</span><span class="sxs-lookup"><span data-stu-id="964fb-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="964fb-120">Aggiungere il valore UNH2.5 nel contratto di ricezione **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span><span class="sxs-lookup"><span data-stu-id="964fb-120">Add UNH2.5 value in the Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="964fb-121">Codifica EDIFACT</span><span class="sxs-lookup"><span data-stu-id="964fb-121">EDIFACT Encode</span></span>
<span data-ttu-id="964fb-122">Per codificare il messaggio in arrivo, configurare lo schema nelle impostazioni di invio del contratto EDIFACT</span><span class="sxs-lookup"><span data-stu-id="964fb-122">To Encode the incoming message, configure the schema in the EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="964fb-123">Aggiungere lo schema all'account di integrazione</span><span class="sxs-lookup"><span data-stu-id="964fb-123">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="964fb-124">Configurare lo schema nelle impostazioni di invio del contratto EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="964fb-124">Configure the schema in the EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="964fb-125">Selezionare il contratto EDIFACT e fare clic su **Modifica come JSON**.</span><span class="sxs-lookup"><span data-stu-id="964fb-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="964fb-126">Aggiungere il valore UNH2.5 nel contratto di invio **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span><span class="sxs-lookup"><span data-stu-id="964fb-126">Add UNH2.5 value in the Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="964fb-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="964fb-127">Next Steps</span></span>
* [<span data-ttu-id="964fb-128">Altre informazioni sui contratti degli account di integrazione</span><span class="sxs-lookup"><span data-stu-id="964fb-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Informazioni sui contratti di Enterprise Integration")  