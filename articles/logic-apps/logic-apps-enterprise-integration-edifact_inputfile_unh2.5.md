---
title: aaaLogic B2B App edifact decodificare risolvere UNH 2.5 - App Azure per la logica | Documenti Microsoft
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
ms.openlocfilehash: 6d85242d0f828fa52cdc9689938f3ba1e51b1183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="998a6-103">Come i documenti con UNH 2.5 toohandle EDIFACT segmento</span><span class="sxs-lookup"><span data-stu-id="998a6-103">How toohandle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="998a6-104">Se UNH 2.5 è presente nel documento EDIFACT hello, utilizzato per la ricerca dello schema.</span><span class="sxs-lookup"><span data-stu-id="998a6-104">When UNH2.5 is present in hello EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="998a6-105">Esempio: campo UNH hello è **EAN008** nel messaggio EDIFACT hello</span><span class="sxs-lookup"><span data-stu-id="998a6-105">Example: hello UNH field is **EAN008** in hello EDIFACT message</span></span>  
<span data-ttu-id="998a6-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span><span class="sxs-lookup"><span data-stu-id="998a6-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="998a6-107">Messaggio hello toohandle toofollow di passaggi</span><span class="sxs-lookup"><span data-stu-id="998a6-107">Steps toofollow toohandle hello message</span></span> 
1. <span data-ttu-id="998a6-108">Aggiornare lo schema di hello</span><span class="sxs-lookup"><span data-stu-id="998a6-108">Update hello schema</span></span>
2. <span data-ttu-id="998a6-109">Controllare le impostazioni dell'accordo hello</span><span class="sxs-lookup"><span data-stu-id="998a6-109">Check hello agreement settings</span></span>  

## <a name="update-hello-schema"></a><span data-ttu-id="998a6-110">Aggiornare lo schema di hello</span><span class="sxs-lookup"><span data-stu-id="998a6-110">Update hello schema</span></span>
<span data-ttu-id="998a6-111">messaggio hello tooprocess, è necessario toodeploy uno schema con nome del nodo radice hello UNH 2.5.</span><span class="sxs-lookup"><span data-stu-id="998a6-111">tooprocess hello message, you need toodeploy a schema with hello UNH2.5 root node name.</span></span>  <span data-ttu-id="998a6-112">Per un esempio, nome radice dello schema di hello sarebbe **EFACT_D03B_ORDERS_EAN008**</span><span class="sxs-lookup"><span data-stu-id="998a6-112">For given an example, hello schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="998a6-113">Per ogni D03B_ORDERS con un altro segmento UNH 2.5, sarebbe necessario toodeploy un singolo schema.</span><span class="sxs-lookup"><span data-stu-id="998a6-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have toodeploy an individual schema.</span></span>  

## <a name="add-schema-toohello-edifact-agreement"></a><span data-ttu-id="998a6-114">Aggiungere un contratto EDIFACT toohello dello schema</span><span class="sxs-lookup"><span data-stu-id="998a6-114">Add schema toohello EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="998a6-115">Decodifica EDIFACT</span><span class="sxs-lookup"><span data-stu-id="998a6-115">EDIFACT Decode</span></span>
<span data-ttu-id="998a6-116">tooDecode hello messaggio in arrivo, configurare schema hello in hello EDIFACT contratto impostazioni di ricezione</span><span class="sxs-lookup"><span data-stu-id="998a6-116">tooDecode hello incoming message, configure hello schema in hello EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="998a6-117">Aggiungere account di integrazione di hello schema toohello</span><span class="sxs-lookup"><span data-stu-id="998a6-117">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="998a6-118">Configurare schema hello in hello EDIFACT contratto impostazioni di ricezione.</span><span class="sxs-lookup"><span data-stu-id="998a6-118">Configure hello schema in hello EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="998a6-119">Selezionare il contratto EDIFACT e fare clic su **Modifica come JSON**.</span><span class="sxs-lookup"><span data-stu-id="998a6-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="998a6-120">Aggiungere il valore di UNH 2.5 nel contratto di ricezione hello **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span><span class="sxs-lookup"><span data-stu-id="998a6-120">Add UNH2.5 value in hello Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="998a6-121">Codifica EDIFACT</span><span class="sxs-lookup"><span data-stu-id="998a6-121">EDIFACT Encode</span></span>
<span data-ttu-id="998a6-122">tooEncode hello messaggio in arrivo, configurare impostazioni di invio contratto EDIFACT hello schema hello</span><span class="sxs-lookup"><span data-stu-id="998a6-122">tooEncode hello incoming message, configure hello schema in hello EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="998a6-123">Aggiungere account di integrazione di hello schema toohello</span><span class="sxs-lookup"><span data-stu-id="998a6-123">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="998a6-124">Configurare schema hello in impostazioni di invio contratto EDIFACT hello.</span><span class="sxs-lookup"><span data-stu-id="998a6-124">Configure hello schema in hello EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="998a6-125">Selezionare il contratto EDIFACT e fare clic su **Modifica come JSON**.</span><span class="sxs-lookup"><span data-stu-id="998a6-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="998a6-126">Aggiungere il valore di UNH 2.5 in hello Invia contratto **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span><span class="sxs-lookup"><span data-stu-id="998a6-126">Add UNH2.5 value in hello Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="998a6-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="998a6-127">Next Steps</span></span>
* [<span data-ttu-id="998a6-128">Altre informazioni sui contratti degli account di integrazione</span><span class="sxs-lookup"><span data-stu-id="998a6-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Informazioni sui contratti di Enterprise Integration")  