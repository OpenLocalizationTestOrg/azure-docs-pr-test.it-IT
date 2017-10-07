---
title: gli schemi di rilevamento per B2B aaaCustom monitoraggio - App Azure per la logica | Documenti Microsoft
description: Creare gli schemi di rilevamento personalizzato messaggi B2B toomonitor dalle transazioni nell'Account di integrazione di Azure.
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="97308-103">Abilitare il rilevamento toomonitor il flusso di lavoro completata, end-to-end</span><span class="sxs-lookup"><span data-stu-id="97308-103">Enable tracking toomonitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="97308-104">È disponibile un rilevamento predefinito che è possibile abilitare per diverse parti del flusso di lavoro Business to Business, ad esempio il rilevamento dei messaggi AS2 o X12.</span><span class="sxs-lookup"><span data-stu-id="97308-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="97308-105">Quando si creano flussi di lavoro che include una logica di applicazione, BizTalk Server, SQL Server o qualsiasi altro livello, è possibile abilitare il rilevamento personalizzato che registra gli eventi dalla fine di toohello hello inizio del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="97308-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from hello beginning toohello end of your workflow.</span></span> 

<span data-ttu-id="97308-106">In questo argomento fornisce codice personalizzato che è possibile utilizzare nei livelli di hello all'esterno dell'app logica.</span><span class="sxs-lookup"><span data-stu-id="97308-106">This topic provides custom code that you can use in hello layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="97308-107">Schema di rilevamento personalizzato</span><span class="sxs-lookup"><span data-stu-id="97308-107">Custom tracking schema</span></span>
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| <span data-ttu-id="97308-108">Proprietà</span><span class="sxs-lookup"><span data-stu-id="97308-108">Property</span></span> | <span data-ttu-id="97308-109">Tipo</span><span class="sxs-lookup"><span data-stu-id="97308-109">Type</span></span> | <span data-ttu-id="97308-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="97308-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="97308-111">sourceType</span><span class="sxs-lookup"><span data-stu-id="97308-111">sourceType</span></span> |   | <span data-ttu-id="97308-112">Tipo di origine eseguire hello.</span><span class="sxs-lookup"><span data-stu-id="97308-112">Type of hello run source.</span></span> <span data-ttu-id="97308-113">I valori consentiti sono **Microsoft.Logic/workflows** e **custom**.</span><span class="sxs-lookup"><span data-stu-id="97308-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="97308-114">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="97308-114">(Mandatory)</span></span> |
| <span data-ttu-id="97308-115">Sorgente</span><span class="sxs-lookup"><span data-stu-id="97308-115">Source</span></span> |   | <span data-ttu-id="97308-116">Se il tipo di origine hello **Microsoft.Logic/workflows**, necessita di informazioni di origine hello toofollow questo schema.</span><span class="sxs-lookup"><span data-stu-id="97308-116">If hello source type is **Microsoft.Logic/workflows**, hello source information needs toofollow this schema.</span></span> <span data-ttu-id="97308-117">Se il tipo di origine hello **personalizzato**, lo schema di hello è un JToken.</span><span class="sxs-lookup"><span data-stu-id="97308-117">If hello source type is **custom**, hello schema is a JToken.</span></span> <span data-ttu-id="97308-118">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="97308-118">(Mandatory)</span></span> |
| <span data-ttu-id="97308-119">systemId</span><span class="sxs-lookup"><span data-stu-id="97308-119">systemId</span></span> | <span data-ttu-id="97308-120">String</span><span class="sxs-lookup"><span data-stu-id="97308-120">String</span></span> | <span data-ttu-id="97308-121">ID di sistema dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="97308-121">Logic app system ID.</span></span> <span data-ttu-id="97308-122">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="97308-122">(Mandatory)</span></span> |
| <span data-ttu-id="97308-123">runId</span><span class="sxs-lookup"><span data-stu-id="97308-123">runId</span></span> | <span data-ttu-id="97308-124">String</span><span class="sxs-lookup"><span data-stu-id="97308-124">String</span></span> | <span data-ttu-id="97308-125">ID di esecuzione dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="97308-125">Logic app run ID.</span></span> <span data-ttu-id="97308-126">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="97308-126">(Mandatory)</span></span> |
| <span data-ttu-id="97308-127">operationName</span><span class="sxs-lookup"><span data-stu-id="97308-127">operationName</span></span> | <span data-ttu-id="97308-128">String</span><span class="sxs-lookup"><span data-stu-id="97308-128">String</span></span> | <span data-ttu-id="97308-129">Nome dell'operazione di hello (ad esempio, azione o trigger).</span><span class="sxs-lookup"><span data-stu-id="97308-129">Name of hello operation (for example, action or trigger).</span></span> <span data-ttu-id="97308-130">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="97308-130">(Mandatory)</span></span> |
| <span data-ttu-id="97308-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="97308-131">repeatItemScopeName</span></span> | <span data-ttu-id="97308-132">String</span><span class="sxs-lookup"><span data-stu-id="97308-132">String</span></span> | <span data-ttu-id="97308-133">Ripetere il nome dell'elemento se hello azione all'interno di un `foreach` / `until` ciclo.</span><span class="sxs-lookup"><span data-stu-id="97308-133">Repeat item name if hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="97308-134">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="97308-134">(Mandatory)</span></span> |
| <span data-ttu-id="97308-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="97308-135">repeatItemIndex</span></span> | <span data-ttu-id="97308-136">Integer</span><span class="sxs-lookup"><span data-stu-id="97308-136">Integer</span></span> | <span data-ttu-id="97308-137">Se l'azione di hello è all'interno di un `foreach` / `until` ciclo.</span><span class="sxs-lookup"><span data-stu-id="97308-137">Whether hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="97308-138">Indica l'indice dell'elemento ripetuto di hello.</span><span class="sxs-lookup"><span data-stu-id="97308-138">Indicates hello repeated item index.</span></span> <span data-ttu-id="97308-139">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="97308-139">(Mandatory)</span></span> |
| <span data-ttu-id="97308-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="97308-140">trackingId</span></span> | <span data-ttu-id="97308-141">String</span><span class="sxs-lookup"><span data-stu-id="97308-141">String</span></span> | <span data-ttu-id="97308-142">ID di traccia, messaggi hello toocorrelate.</span><span class="sxs-lookup"><span data-stu-id="97308-142">Tracking ID, toocorrelate hello messages.</span></span> <span data-ttu-id="97308-143">Facoltativa</span><span class="sxs-lookup"><span data-stu-id="97308-143">(Optional)</span></span> |
| <span data-ttu-id="97308-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="97308-144">correlationId</span></span> | <span data-ttu-id="97308-145">String</span><span class="sxs-lookup"><span data-stu-id="97308-145">String</span></span> | <span data-ttu-id="97308-146">ID di correlazione, messaggi hello toocorrelate.</span><span class="sxs-lookup"><span data-stu-id="97308-146">Correlation ID, toocorrelate hello messages.</span></span> <span data-ttu-id="97308-147">Facoltativa</span><span class="sxs-lookup"><span data-stu-id="97308-147">(Optional)</span></span> |
| <span data-ttu-id="97308-148">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="97308-148">clientRequestId</span></span> | <span data-ttu-id="97308-149">String</span><span class="sxs-lookup"><span data-stu-id="97308-149">String</span></span> | <span data-ttu-id="97308-150">Client popolarlo toocorrelate messaggi.</span><span class="sxs-lookup"><span data-stu-id="97308-150">Client can populate it toocorrelate messages.</span></span> <span data-ttu-id="97308-151">Facoltativa</span><span class="sxs-lookup"><span data-stu-id="97308-151">(Optional)</span></span> |
| <span data-ttu-id="97308-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="97308-152">eventLevel</span></span> |   | <span data-ttu-id="97308-153">Livello dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="97308-153">Level of hello event.</span></span> <span data-ttu-id="97308-154">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="97308-154">(Mandatory)</span></span> |
| <span data-ttu-id="97308-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="97308-155">eventTime</span></span> |   | <span data-ttu-id="97308-156">Ora dell'evento hello, in formato UTC AAAA-MM-DDTHH:MM:SS.00000Z.</span><span class="sxs-lookup"><span data-stu-id="97308-156">Time of hello event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="97308-157">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="97308-157">(Mandatory)</span></span> |
| <span data-ttu-id="97308-158">recordType</span><span class="sxs-lookup"><span data-stu-id="97308-158">recordType</span></span> |   | <span data-ttu-id="97308-159">Tipo di record di rilevamento hello.</span><span class="sxs-lookup"><span data-stu-id="97308-159">Type of hello track record.</span></span> <span data-ttu-id="97308-160">Il valore consentito è **custom**.</span><span class="sxs-lookup"><span data-stu-id="97308-160">Allowed value is **custom**.</span></span> <span data-ttu-id="97308-161">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="97308-161">(Mandatory)</span></span> |
| <span data-ttu-id="97308-162">record</span><span class="sxs-lookup"><span data-stu-id="97308-162">record</span></span> |   | <span data-ttu-id="97308-163">Tipo di record personalizzato.</span><span class="sxs-lookup"><span data-stu-id="97308-163">Custom record type.</span></span> <span data-ttu-id="97308-164">Il formato consentito è JToken.</span><span class="sxs-lookup"><span data-stu-id="97308-164">Allowed format is JToken.</span></span> <span data-ttu-id="97308-165">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="97308-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="97308-166">Schemi di rilevamento per il protocollo B2B</span><span class="sxs-lookup"><span data-stu-id="97308-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="97308-167">Per informazioni sugli schemi di rilevamento per il protocollo B2B, vedere:</span><span class="sxs-lookup"><span data-stu-id="97308-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="97308-168">Schemi di rilevamento AS2</span><span class="sxs-lookup"><span data-stu-id="97308-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="97308-169">Schemi di rilevamento X12</span><span class="sxs-lookup"><span data-stu-id="97308-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="97308-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="97308-170">Next steps</span></span>
* <span data-ttu-id="97308-171">Altre informazioni sul [monitoraggio dei messaggi B2B](logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="97308-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="97308-172">Informazioni su [rilevamento dei messaggi B2B nel portale di Operations Management Suite hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="97308-172">Learn about [tracking B2B messages in hello Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="97308-173">Altre informazioni su hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="97308-173">Learn more about hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
