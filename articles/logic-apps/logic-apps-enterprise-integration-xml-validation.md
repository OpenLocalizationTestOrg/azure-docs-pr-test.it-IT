---
title: aaaValidate XML - App Azure per la logica | Documenti Microsoft
description: Convalida XML con schemi per le app di logica di Azure e gli scenari B2B usando hello Enterprise Integration Pack
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a><span data-ttu-id="3c697-103">Enterprise Integration con convalida XML</span><span class="sxs-lookup"><span data-stu-id="3c697-103">Validate XML for enterprise integration</span></span>

<span data-ttu-id="3c697-104">Spesso in scenari B2B, partner hello in un contratto deve assicurarsi che i messaggi hello che dello scambio siano validi prima di poter avviare l'elaborazione dati.</span><span class="sxs-lookup"><span data-stu-id="3c697-104">Often in B2B scenarios, hello partners in an agreement must make sure that hello messages they exchange are valid before data processing can start.</span></span> <span data-ttu-id="3c697-105">È possibile convalidare documenti rispetto a uno schema predefinito utilizzando hello usare hello convalida XML connettore in hello Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="3c697-105">You can validate documents against a predefined schema by using hello use hello XML Validation connector in hello Enterprise Integration Pack.</span></span>

## <a name="validate-a-document-with-hello-xml-validation-connector"></a><span data-ttu-id="3c697-106">Convalidare un documento con il connettore di convalida XML hello</span><span class="sxs-lookup"><span data-stu-id="3c697-106">Validate a document with hello XML Validation connector</span></span>

1. <span data-ttu-id="3c697-107">Creare un'applicazione, la logica e [collegare l'account di integrazione di hello app toohello](../logic-apps/logic-apps-enterprise-integration-accounts.md "informazioni toolink un'app di logica di integrazione account tooa") con schema hello desiderate toouse per la convalida dei dati XML.</span><span class="sxs-lookup"><span data-stu-id="3c697-107">Create a logic app, and [link hello app toohello integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app") that has hello schema you want toouse for validating XML data.</span></span>

2. <span data-ttu-id="3c697-108">Aggiungere un **richiesta - viene ricevuta la richiesta HTTP quando** trigger tooyour logica app.</span><span class="sxs-lookup"><span data-stu-id="3c697-108">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. <span data-ttu-id="3c697-109">hello tooadd **convalida XML** azione, scegliere **aggiungere un'azione**.</span><span class="sxs-lookup"><span data-stu-id="3c697-109">tooadd hello **XML Validation** action, choose **Add an action**.</span></span>

4. <span data-ttu-id="3c697-110">toofilter tutti hello toohello azioni quello che si desidera, immettere *xml* nella casella di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="3c697-110">toofilter all hello actions toohello one that you want, enter *xml* in hello search box.</span></span> <span data-ttu-id="3c697-111">Selezionare **Convalida XML**.</span><span class="sxs-lookup"><span data-stu-id="3c697-111">Choose **XML Validation**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. <span data-ttu-id="3c697-112">Selezionare toospecify hello contenuto XML che si desidera toovalidate, **contenuto**.</span><span class="sxs-lookup"><span data-stu-id="3c697-112">toospecify hello XML content that you want toovalidate, select **CONTENT**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. <span data-ttu-id="3c697-113">Selezionare i tag body hello come contenuto che si desidera toovalidate hello.</span><span class="sxs-lookup"><span data-stu-id="3c697-113">Select hello body tag as hello content that you want toovalidate.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. <span data-ttu-id="3c697-114">schema di hello toospecify desiderato toouse per la convalida di hello precedente *contenuto* di input, scegliere **nome dello SCHEMA**.</span><span class="sxs-lookup"><span data-stu-id="3c697-114">toospecify hello schema you want toouse for validating hello previous *content* input, choose **SCHEMA NAME**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. <span data-ttu-id="3c697-115">Salvare il lavoro </span><span class="sxs-lookup"><span data-stu-id="3c697-115">Save your work</span></span>  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

<span data-ttu-id="3c697-116">A questo punto, la configurazione del connettore di convalida è completa.</span><span class="sxs-lookup"><span data-stu-id="3c697-116">You are now done with setting up your validation connector.</span></span> <span data-ttu-id="3c697-117">In un'applicazione reale, è possibile che i dati di hello convalidato toostore in un'app di line-of-business (LOB) come SalesForce.</span><span class="sxs-lookup"><span data-stu-id="3c697-117">In a real world application, you might want toostore hello validated data in a line-of-business (LOB) app like SalesForce.</span></span> <span data-ttu-id="3c697-118">toosend hello tooSalesforce output convalidato, aggiungere un'azione.</span><span class="sxs-lookup"><span data-stu-id="3c697-118">toosend hello validated output tooSalesforce, add an action.</span></span>

<span data-ttu-id="3c697-119">tootest l'azione di convalida, creare un endpoint HTTP toohello richiesta.</span><span class="sxs-lookup"><span data-stu-id="3c697-119">tootest your validation action, make a request toohello HTTP endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c697-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3c697-120">Next steps</span></span>
[<span data-ttu-id="3c697-121">Altre informazioni su Enterprise Integration Pack hello</span><span class="sxs-lookup"><span data-stu-id="3c697-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack")   

