---
title: Usare i messaggi XML nei flussi di lavoro - App per la logica di Azure | Microsoft Docs
description: Elaborare, convalidare, trasformare e migliorare i messaggi XML nelle app per la logica e negli scenari aziendali usando Enterprise Integration Pack
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
ms.openlocfilehash: 3fec4935f5317be4bf8c9e05f1c24a7c05381b1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="6dfa9-103">Convalidare e trasformare il linguaggio XML, codificare e decodificare file flat e migliorare le funzionalità di messaggi nelle app per la logica</span><span class="sxs-lookup"><span data-stu-id="6dfa9-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="6dfa9-104">Grazie all'uso delle app per la logica, è possibile elaborare i messaggi XML che si inviano e si ricevono.</span><span class="sxs-lookup"><span data-stu-id="6dfa9-104">Using logic apps, you have the ability to process XML messages that you send and receive.</span></span> <span data-ttu-id="6dfa9-105">Questa funzionalità è inclusa in Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="6dfa9-105">This feature is included with the Enterprise Integration Pack.</span></span> <span data-ttu-id="6dfa9-106">Per gli utenti con uno sfondo a BizTalk Server, Enterprise Integration Pack offre funzionalità simili per trasformare e convalidare i messaggi, usare i file flat e persino servirsi di XPath per migliorare o estrarre le proprietà specifiche di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="6dfa9-106">For those users with a BizTalk Server background, the Enterprise Integration Pack gives you similar abilities to transform and validate messages, work with flat files, and even use XPath to enrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="6dfa9-107">Per gli utenti che non hanno familiarità con questo spazio, queste funzionalità ampliano le modalità di elaborazione dei messaggi nel flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6dfa9-107">For those users who are new to this space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="6dfa9-108">Ad esempio, in uno scenario Business-to-Business in cui si usano schemi XML specifici, è possibile usare Enterprise Integration Pack per migliorare le modalità di elaborazione aziendale dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="6dfa9-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use the Enterprise Integration Pack to enhance how your company processes these messages.</span></span> 

<span data-ttu-id="6dfa9-109">Enterprise Integration Pack include:</span><span class="sxs-lookup"><span data-stu-id="6dfa9-109">The Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="6dfa9-110">[Convalida dei messaggi XML](logic-apps-enterprise-integration-xml-validation.md "Informazioni sulla convalida dei messaggi XML"): consente di convalidare un messaggio XML in entrata o in uscita rispetto a uno schema specifico.</span><span class="sxs-lookup"><span data-stu-id="6dfa9-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="6dfa9-111">[Trasformazione dei messaggi XML](../logic-apps/logic-apps-enterprise-integration-transform.md "Informazioni sulle mappe e le trasformazioni di messaggi XML"): consente di convertire o personalizzare un messaggio XML in base ai propri requisiti o a quelli di un partner.</span><span class="sxs-lookup"><span data-stu-id="6dfa9-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or the requirements of a partner.</span></span>
* <span data-ttu-id="6dfa9-112">[Codifica e decodifica del file flat](logic-apps-enterprise-integration-flatfile.md "Informazioni sulla codifica o decodifica del file flat"): consente di codificare o decodificare un file flat.</span><span class="sxs-lookup"><span data-stu-id="6dfa9-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="6dfa9-113">Ad esempio, SAP accetta e invia file IDOC in formato file flat.</span><span class="sxs-lookup"><span data-stu-id="6dfa9-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="6dfa9-114">Molte piattaforme di integrazione creano messaggi XML, tra cui App per la logica.</span><span class="sxs-lookup"><span data-stu-id="6dfa9-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="6dfa9-115">Pertanto, è possibile creare un'app per la logica che usi il codificatore di file flat per "convertire" i file XML in file flat.</span><span class="sxs-lookup"><span data-stu-id="6dfa9-115">So, you can create a logic app that uses the flat file encoder to "convert" XML files to flat files.</span></span> 
* <span data-ttu-id="6dfa9-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx): consente di arricchire un messaggio ed estrarre le proprietà specifiche del messaggio.</span><span class="sxs-lookup"><span data-stu-id="6dfa9-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from the message.</span></span> <span data-ttu-id="6dfa9-117">È possibile quindi usare le proprietà estratte per indirizzare il messaggio a un endpoint intermedio o di destinazione.</span><span class="sxs-lookup"><span data-stu-id="6dfa9-117">You can then use the extracted properties to route the message to a destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="6dfa9-118">Provare il servizio</span><span class="sxs-lookup"><span data-stu-id="6dfa9-118">Try it out</span></span>
<span data-ttu-id="6dfa9-119">[Distribuire un'app per la logica completamente operativa](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (campione di GitHub) usando le funzionalità XML di App per la logica di Azure.</span><span class="sxs-lookup"><span data-stu-id="6dfa9-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using the XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="6dfa9-120">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="6dfa9-120">Learn more</span></span>
[<span data-ttu-id="6dfa9-121">Altre informazioni su Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="6dfa9-121">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Informazioni su Enterprise Integration Pack")
