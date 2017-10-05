---
title: Convalida XML - App per la logica di Azure | Microsoft Docs
description: Convalida XML con gli schemi per le app per la logica di Azure e negli scenari B2B usando Enterprise Integration Pack
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
ms.openlocfilehash: 8558efffa354cc4bb93820c837077ee997924c95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="validate-xml-for-enterprise-integration"></a><span data-ttu-id="75faf-103">Enterprise Integration con convalida XML</span><span class="sxs-lookup"><span data-stu-id="75faf-103">Validate XML for enterprise integration</span></span>

<span data-ttu-id="75faf-104">Spesso negli scenari B2B i partner di un contratto devono accertarsi che i messaggi scambiati siano validi prima di avviare l'elaborazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="75faf-104">Often in B2B scenarios, the partners in an agreement must make sure that the messages they exchange are valid before data processing can start.</span></span> <span data-ttu-id="75faf-105">In Enterprise Integration Pack, è possibile usare il connettore di convalida XML per convalidare i documenti in base a uno schema predefinito.</span><span class="sxs-lookup"><span data-stu-id="75faf-105">You can validate documents against a predefined schema by using the use the XML Validation connector in the Enterprise Integration Pack.</span></span>

## <a name="validate-a-document-with-the-xml-validation-connector"></a><span data-ttu-id="75faf-106">Come convalidare un documento con il connettore di convalida XML</span><span class="sxs-lookup"><span data-stu-id="75faf-106">Validate a document with the XML Validation connector</span></span>

1. <span data-ttu-id="75faf-107">Creare un'app per la logica e [collegarla all'account di integrazione](../logic-apps/logic-apps-enterprise-integration-accounts.md "Informazioni su come collegare un account di integrazione a un'app per la logica") che contiene lo schema che verrà usato per convalidare i dati XML.</span><span class="sxs-lookup"><span data-stu-id="75faf-107">Create a logic app, and [link the app to the integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that has the schema you want to use for validating XML data.</span></span>

2. <span data-ttu-id="75faf-108">Aggiungere un trigger **Richiesta - Alla ricezione di una richiesta HTTP** all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="75faf-108">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. <span data-ttu-id="75faf-109">Aggiungere l'azione **Convalida XML** selezionando **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="75faf-109">To add the **XML Validation** action, choose **Add an action**.</span></span>

4. <span data-ttu-id="75faf-110">Immettere *xml* nella casella di ricerca per filtrare tutte le azioni su quella che si desidera.</span><span class="sxs-lookup"><span data-stu-id="75faf-110">To filter all the actions to the one that you want, enter *xml* in the search box.</span></span> <span data-ttu-id="75faf-111">Selezionare **Convalida XML**.</span><span class="sxs-lookup"><span data-stu-id="75faf-111">Choose **XML Validation**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. <span data-ttu-id="75faf-112">Per specificare il contenuto XML che si desidera convalidare, selezionare **CONTENUTO**.</span><span class="sxs-lookup"><span data-stu-id="75faf-112">To specify the XML content that you want to validate, select **CONTENT**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. <span data-ttu-id="75faf-113">Selezionare il tag del corpo come contenuto che si desidera convalidare.</span><span class="sxs-lookup"><span data-stu-id="75faf-113">Select the body tag as the content that you want to validate.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. <span data-ttu-id="75faf-114">Per specificare lo schema che desidera usare per convalidare il *contenuto* immesso in precedenza, scegliere **NOME SCHEMA**.</span><span class="sxs-lookup"><span data-stu-id="75faf-114">To specify the schema you want to use for validating the previous *content* input, choose **SCHEMA NAME**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. <span data-ttu-id="75faf-115">Salvare il lavoro </span><span class="sxs-lookup"><span data-stu-id="75faf-115">Save your work</span></span>  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

<span data-ttu-id="75faf-116">A questo punto, la configurazione del connettore di convalida è completa.</span><span class="sxs-lookup"><span data-stu-id="75faf-116">You are now done with setting up your validation connector.</span></span> <span data-ttu-id="75faf-117">In un'applicazione reale è possibile archiviare i dati convalidati in un'app line-of-business (LOB), ad esempio SalesForce.</span><span class="sxs-lookup"><span data-stu-id="75faf-117">In a real world application, you might want to store the validated data in a line-of-business (LOB) app like SalesForce.</span></span> <span data-ttu-id="75faf-118">Per inviare l'output della convalida a Salesforce, aggiungere un'azione.</span><span class="sxs-lookup"><span data-stu-id="75faf-118">To send the validated output to Salesforce, add an action.</span></span>

<span data-ttu-id="75faf-119">Per testare l'azione di convalida, eseguire una richiesta all'endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="75faf-119">To test your validation action, make a request to the HTTP endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75faf-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="75faf-120">Next steps</span></span>
[<span data-ttu-id="75faf-121">Altre informazioni su Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="75faf-121">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Informazioni su Enterprise Integration Pack")   

