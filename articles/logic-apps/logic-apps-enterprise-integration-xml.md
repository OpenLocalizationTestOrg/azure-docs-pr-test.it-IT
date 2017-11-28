---
title: messaggi nei flussi di lavoro - App Azure per la logica di aaaWorking con XML | Documenti Microsoft
description: Elaborare, convalidare, trasformare e arricchire XML messaggi in App per la logica e l'utilizzo di business tooscenarios hello Enterprise Integration Pack
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 47672dc4-1caa-44e5-b8cb-68ec3a76b7dc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 02/27/2017
ms.author: LADocs; mandia
ms.openlocfilehash: f90ae89fef0a4bd17286adbce398e573940bb790
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="a1c49-103">Convalidare e trasformare il linguaggio XML, codificare e decodificare file flat e migliorare le funzionalità di messaggi nelle app per la logica</span><span class="sxs-lookup"><span data-stu-id="a1c49-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="a1c49-104">Usare la logica App, è necessario hello possibilità tooprocess messaggi XML inviati e ricevuti.</span><span class="sxs-lookup"><span data-stu-id="a1c49-104">Using logic apps, you have hello ability tooprocess XML messages that you send and receive.</span></span> <span data-ttu-id="a1c49-105">Questa funzionalità è inclusa con hello Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="a1c49-105">This feature is included with hello Enterprise Integration Pack.</span></span> <span data-ttu-id="a1c49-106">Per gli utenti con uno sfondo di BizTalk Server, hello Enterprise Integration Pack offre tootransform funzionalità simili e convalidare i messaggi, utilizzare i file flat e anche utilizzare XPath tooenrich o estrarre le proprietà specifiche da un messaggio.</span><span class="sxs-lookup"><span data-stu-id="a1c49-106">For those users with a BizTalk Server background, hello Enterprise Integration Pack gives you similar abilities tootransform and validate messages, work with flat files, and even use XPath tooenrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="a1c49-107">Per gli utenti che sono di nuovo spazio toothis, queste funzionalità espandere la modalità di elaborazione messaggi all'interno del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a1c49-107">For those users who are new toothis space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="a1c49-108">Ad esempio, se sono in uno scenario business-to-business e lavorare con schemi XML specifici, è possibile utilizzare hello Enterprise Integration Pack tooenhance come la società elabora questi messaggi.</span><span class="sxs-lookup"><span data-stu-id="a1c49-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use hello Enterprise Integration Pack tooenhance how your company processes these messages.</span></span> 

<span data-ttu-id="a1c49-109">Hello Enterprise Integration Pack include:</span><span class="sxs-lookup"><span data-stu-id="a1c49-109">hello Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="a1c49-110">[Convalida dei messaggi XML](logic-apps-enterprise-integration-xml-validation.md "Informazioni sulla convalida dei messaggi XML"): consente di convalidare un messaggio XML in entrata o in uscita rispetto a uno schema specifico.</span><span class="sxs-lookup"><span data-stu-id="a1c49-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="a1c49-111">[Trasformazione XML](../logic-apps/logic-apps-enterprise-integration-transform.md "ulteriori informazioni sulle trasformazioni di messaggi XML e mappe") : convertire o personalizzare un messaggio XML basato su requisiti o requisiti hello di un partner.</span><span class="sxs-lookup"><span data-stu-id="a1c49-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or hello requirements of a partner.</span></span>
* <span data-ttu-id="a1c49-112">[Codifica e decodifica del file flat](logic-apps-enterprise-integration-flatfile.md "Informazioni sulla codifica o decodifica del file flat"): consente di codificare o decodificare un file flat.</span><span class="sxs-lookup"><span data-stu-id="a1c49-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="a1c49-113">Ad esempio, SAP accetta e invia file IDOC in formato file flat.</span><span class="sxs-lookup"><span data-stu-id="a1c49-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="a1c49-114">Molte piattaforme di integrazione creano messaggi XML, tra cui App per la logica.</span><span class="sxs-lookup"><span data-stu-id="a1c49-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="a1c49-115">In tal caso, è possibile creare un'app di logica che utilizza hello file flat codificatore troppo "conversione" file tooflat di file XML.</span><span class="sxs-lookup"><span data-stu-id="a1c49-115">So, you can create a logic app that uses hello flat file encoder too"convert" XML files tooflat files.</span></span> 
* <span data-ttu-id="a1c49-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - arricchire il messaggio ed estrarre le proprietà specifiche dal messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="a1c49-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from hello message.</span></span> <span data-ttu-id="a1c49-117">È possibile quindi utilizzare hello estratti destinazione tooa dei messaggi hello tooroute proprietà o un endpoint intermedio.</span><span class="sxs-lookup"><span data-stu-id="a1c49-117">You can then use hello extracted properties tooroute hello message tooa destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="a1c49-118">Provare il servizio</span><span class="sxs-lookup"><span data-stu-id="a1c49-118">Try it out</span></span>
<span data-ttu-id="a1c49-119">[Distribuire un'app logica completamente operativa ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (esempio di GitHub) utilizzando le funzionalità XML hello nelle app di logica di Azure.</span><span class="sxs-lookup"><span data-stu-id="a1c49-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using hello XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="a1c49-120">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="a1c49-120">Learn more</span></span>
[<span data-ttu-id="a1c49-121">Altre informazioni su Enterprise Integration Pack hello</span><span class="sxs-lookup"><span data-stu-id="a1c49-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack")
