---
title: Integrazione per B2B - App Azure per la logica aaaEnterprise | Documenti Microsoft
description: Creare flussi di lavoro B2B e supportare scenari di integrazione aziendale per App per la logica con hello Enterprise Integration Pack
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: dd517c4d-1701-4247-b83c-183c4d8d8aae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8dc866533110b1d07f51cf446056d2ca5ce869ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a><span data-ttu-id="ccc62-103">Panoramica: Scenari B2B e la comunicazione con hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="ccc62-103">Overview: B2B scenarios and communication with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="ccc62-104">Per i flussi di lavoro di business-to-business (B2B) e la comunicazione trasparente con le app di logica di Azure, è possibile abilitare scenari di integrazione aziendale di Microsoft basato su cloud soluzione hello Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="ccc62-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, hello Enterprise Integration Pack.</span></span> <span data-ttu-id="ccc62-105">Le organizzazioni saranno in grado di scambiarsi messaggi elettronicamente anche se usano formati e protocolli diversi.</span><span class="sxs-lookup"><span data-stu-id="ccc62-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="ccc62-106">pack Hello Trasforma formati diversi in un formato che è in grado di interpretare ed elaborare i sistemi delle organizzazioni.</span><span class="sxs-lookup"><span data-stu-id="ccc62-106">hello pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="ccc62-107">Le organizzazioni possono scambiarsi messaggi grazie ai protocolli standard del settore tra cui [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md) ed [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="ccc62-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="ccc62-108">È inoltre possibile proteggere i messaggi con firme digitali e crittografia.</span><span class="sxs-lookup"><span data-stu-id="ccc62-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="ccc62-109">Se si ha familiarità con BizTalk Server o servizi BizTalk di Microsoft Azure, le funzionalità di integrazione di Enterprise hello sono toouse semplice quanto la maggior parte dei concetti sono simili.</span><span class="sxs-lookup"><span data-stu-id="ccc62-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, hello Enterprise Integration features are easy toouse because most concepts are similar.</span></span> <span data-ttu-id="ccc62-110">La principale differenza è che Enterprise Integration utilizza integrazione account toosimplify hello archiviazione e la gestione degli elementi utilizzati nelle comunicazioni B2B.</span><span class="sxs-lookup"><span data-stu-id="ccc62-110">One major difference is that Enterprise Integration uses integration accounts toosimplify hello storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="ccc62-111">L'architettura hello Enterprise Integration Pack si basa su "account di integrazione".</span><span class="sxs-lookup"><span data-stu-id="ccc62-111">Architecturally, hello Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="ccc62-112">Questi account sono contenitori basati sul cloud che archiviano elementi quali schemi, partner, certificati, mappe e contratti.</span><span class="sxs-lookup"><span data-stu-id="ccc62-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="ccc62-113">È possibile utilizzare toodesign questi elementi, distribuire e gestire le app B2B e anche i flussi di lavoro toobuild B2B per App per la logica.</span><span class="sxs-lookup"><span data-stu-id="ccc62-113">You can use these artifacts toodesign, deploy, and maintain your B2B apps and also toobuild B2B workflows for logic apps.</span></span> <span data-ttu-id="ccc62-114">Ma prima di poter utilizzare questi elementi, è innanzitutto necessario collegare l'applicazione di integrazione account tooyour logica.</span><span class="sxs-lookup"><span data-stu-id="ccc62-114">But before you can use these artifacts, you must first link your integration account tooyour logic app.</span></span> <span data-ttu-id="ccc62-115">Successivamente, l'app per la logica può accedere agli elementi dell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="ccc62-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="ccc62-116">Perché usare Enterprise Integration</span><span class="sxs-lookup"><span data-stu-id="ccc62-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="ccc62-117">Grazie all'integrazione aziendale, è possibile archiviare tutti gli elementi in un'unica posizione, ovvero nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="ccc62-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="ccc62-118">È possibile creare flussi di lavoro B2B e integrare con App di terze parti software come servizio (SaaS), applicazioni locali e le applicazioni personalizzate tramite il motore di App per la logica Azure hello e tutti i connettori.</span><span class="sxs-lookup"><span data-stu-id="ccc62-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using hello Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="ccc62-119">Grazie alle funzioni di Azure, è possibile creare un codice personalizzato per le app per la logica.</span><span class="sxs-lookup"><span data-stu-id="ccc62-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-tooget-started-with-enterprise-integration"></a><span data-ttu-id="ccc62-120">La modalità di avvio con l'integrazione di enterprise tooget?</span><span class="sxs-lookup"><span data-stu-id="ccc62-120">How tooget started with enterprise integration?</span></span>

<span data-ttu-id="ccc62-121">È possibile creare e gestire le app B2B con hello Enterprise Integration Pack tramite Progettazione applicazione logica Ciao hello **portale di Azure**.</span><span class="sxs-lookup"><span data-stu-id="ccc62-121">You can build and manage B2B apps with hello Enterprise Integration Pack through hello Logic App Designer in hello **Azure portal**.</span></span> <span data-ttu-id="ccc62-122">Le app per la logica possono essere gestite anche usando [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Argomenti relativi alle app per la logica in PowerShell").</span><span class="sxs-lookup"><span data-stu-id="ccc62-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="ccc62-123">Ecco i passaggi di alto livello hello che è necessario eseguire prima di poter creare le app nel portale di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="ccc62-123">Here are hello high-level steps you must take before you can create apps in hello Azure portal:</span></span>

![immagine di panoramica](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="ccc62-125">Alcuni scenari comuni</span><span class="sxs-lookup"><span data-stu-id="ccc62-125">What are some common scenarios?</span></span>

<span data-ttu-id="ccc62-126">Enterprise Integration supporta gli standard del settore seguenti:</span><span class="sxs-lookup"><span data-stu-id="ccc62-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="ccc62-127">EDI: Electronic Data Interchange</span><span class="sxs-lookup"><span data-stu-id="ccc62-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="ccc62-128">EAI: Enterprise Application Integration</span><span class="sxs-lookup"><span data-stu-id="ccc62-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-tooget-started"></a><span data-ttu-id="ccc62-129">Ecco cosa occorre tooget avviato</span><span class="sxs-lookup"><span data-stu-id="ccc62-129">Here's what you need tooget started</span></span>

* <span data-ttu-id="ccc62-130">Una sottoscrizione ad Azure con account di integrazione</span><span class="sxs-lookup"><span data-stu-id="ccc62-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="ccc62-131">Visual Studio 2015 toocreate mappe e schemi</span><span class="sxs-lookup"><span data-stu-id="ccc62-131">Visual Studio 2015 toocreate maps and schemas</span></span>
* [<span data-ttu-id="ccc62-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0 (Strumenti di Enterprise Integration per le app per la logica di Microsoft Azure per Visual Studio 2015 2.0)</span><span class="sxs-lookup"><span data-stu-id="ccc62-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="ccc62-133">Da provare subito</span><span class="sxs-lookup"><span data-stu-id="ccc62-133">Try it now</span></span>

<span data-ttu-id="ccc62-134">[Distribuire una trasmissione AS2 esempio completamente operativo e app per la logica di ricezione](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) che utilizza le funzionalità B2B hello per le app di logica di Azure.</span><span class="sxs-lookup"><span data-stu-id="ccc62-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses hello B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="ccc62-135">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="ccc62-135">Learn more</span></span>
* [<span data-ttu-id="ccc62-136">Contratti</span><span class="sxs-lookup"><span data-stu-id="ccc62-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Informazioni sui contratti di Enterprise Integration")
* [<span data-ttu-id="ccc62-137">Scenari di business (B2B) tooBusiness</span><span class="sxs-lookup"><span data-stu-id="ccc62-137">Business tooBusiness (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "informazioni come toocreate logica App con funzionalità B2B")  
* [<span data-ttu-id="ccc62-138">Certificati</span><span class="sxs-lookup"><span data-stu-id="ccc62-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "Informazioni sui certificati di Enterprise Integration")
* [<span data-ttu-id="ccc62-139">Flat file codifica/decodifica</span><span class="sxs-lookup"><span data-stu-id="ccc62-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "informazioni come tooencode e decodificare il contenuto del file flat")  
* [<span data-ttu-id="ccc62-140">Account di integrazione</span><span class="sxs-lookup"><span data-stu-id="ccc62-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "Informazioni sugli account di integrazione")
* [<span data-ttu-id="ccc62-141">Mappe</span><span class="sxs-lookup"><span data-stu-id="ccc62-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Informazioni sulle mappe di Enterprise Integration")
* [<span data-ttu-id="ccc62-142">Partner</span><span class="sxs-lookup"><span data-stu-id="ccc62-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "Informazioni sui partner di Enterprise Integration")
* [<span data-ttu-id="ccc62-143">Schemi</span><span class="sxs-lookup"><span data-stu-id="ccc62-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "Informazioni sugli schemi di Enterprise Integration")
* [<span data-ttu-id="ccc62-144">Convalida del messaggio XML</span><span class="sxs-lookup"><span data-stu-id="ccc62-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "informazioni su come i messaggi con la logica App toovalidate XML")
* [<span data-ttu-id="ccc62-145">Trasformazione XML</span><span class="sxs-lookup"><span data-stu-id="ccc62-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "Informazioni sulle mappe di Enterprise Integration")
* [<span data-ttu-id="ccc62-146">Connettori di integrazione aziendale</span><span class="sxs-lookup"><span data-stu-id="ccc62-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "Informazioni sui connettori di Enterprise Integration Pack")
* [<span data-ttu-id="ccc62-147">Metadati dell'account di integrazione</span><span class="sxs-lookup"><span data-stu-id="ccc62-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "Informazioni sui metadati dell'account di integrazione")
* [<span data-ttu-id="ccc62-148">Monitoraggio dei messaggi B2B</span><span class="sxs-lookup"><span data-stu-id="ccc62-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "Altre informazioni sul monitoraggio dei messaggi B2B")
* [<span data-ttu-id="ccc62-149">Rilevamento dei messaggi B2B nel portale OMS</span><span class="sxs-lookup"><span data-stu-id="ccc62-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "Altre informazioni sul rilevamento dei messaggi B2B nel portale OMS")

