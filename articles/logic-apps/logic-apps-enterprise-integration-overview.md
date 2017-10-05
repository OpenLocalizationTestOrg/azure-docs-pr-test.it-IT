---
title: Enterprise Integration per B2B - App per la logica di Azure | Microsoft Docs
description: Compilare flussi di lavoro B2B e supportare scenari di integrazione aziendale per le app per la logica con Enterprise Integration Pack
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
ms.openlocfilehash: 9462707db03ecfcc3d5186ce7ded8655ad3bdcc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-the-enterprise-integration-pack"></a><span data-ttu-id="1232b-103">Panoramica: scenari B2B e comunicazione con Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="1232b-103">Overview: B2B scenarios and communication with the Enterprise Integration Pack</span></span>

<span data-ttu-id="1232b-104">Per i flussi di lavoro Business to Business (B2B) e una fluida comunicazione con le app per la logica di Azure, è possibile abilitare gli scenari di integrazione aziendale grazie alla soluzione basata sul cloud di Microsoft, Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="1232b-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, the Enterprise Integration Pack.</span></span> <span data-ttu-id="1232b-105">Le organizzazioni saranno in grado di scambiarsi messaggi elettronicamente anche se usano formati e protocolli diversi.</span><span class="sxs-lookup"><span data-stu-id="1232b-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="1232b-106">Il pacchetto trasforma i diversi formati in un formato che i sistemi delle organizzazioni possano interpretare ed elaborare.</span><span class="sxs-lookup"><span data-stu-id="1232b-106">The pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="1232b-107">Le organizzazioni possono scambiarsi messaggi grazie ai protocolli standard del settore tra cui [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md) ed [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="1232b-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="1232b-108">È inoltre possibile proteggere i messaggi con firme digitali e crittografia.</span><span class="sxs-lookup"><span data-stu-id="1232b-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="1232b-109">Se si ha familiarità con BizTalk Server o con i Servizi BizTalk di Microsoft Azure, risulterà facile usare le funzionalità di Enterprise Integration grazie alla somiglianza della maggior parte dei concetti.</span><span class="sxs-lookup"><span data-stu-id="1232b-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, the Enterprise Integration features are easy to use because most concepts are similar.</span></span> <span data-ttu-id="1232b-110">La principale differenza consiste nel fatto che Enterprise Integration usa gli account di integrazione per semplificare l'archiviazione e la gestione degli elementi nelle comunicazioni B2B.</span><span class="sxs-lookup"><span data-stu-id="1232b-110">One major difference is that Enterprise Integration uses integration accounts to simplify the storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="1232b-111">Dal punto di vista dell'architettura, Enterprise Integration Pack si basa sugli "account di integrazione".</span><span class="sxs-lookup"><span data-stu-id="1232b-111">Architecturally, the Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="1232b-112">Questi account sono contenitori basati sul cloud che archiviano elementi quali schemi, partner, certificati, mappe e contratti.</span><span class="sxs-lookup"><span data-stu-id="1232b-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="1232b-113">È possibile usare questi elementi per progettare, distribuire e gestire le app B2B, nonché per creare flussi di lavoro B2B per le app per la logica.</span><span class="sxs-lookup"><span data-stu-id="1232b-113">You can use these artifacts to design, deploy, and maintain your B2B apps and also to build B2B workflows for logic apps.</span></span> <span data-ttu-id="1232b-114">Prima di poter usare questi elementi però, è necessario collegare l'account di integrazione all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="1232b-114">But before you can use these artifacts, you must first link your integration account to your logic app.</span></span> <span data-ttu-id="1232b-115">Successivamente, l'app per la logica può accedere agli elementi dell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="1232b-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="1232b-116">Perché usare Enterprise Integration</span><span class="sxs-lookup"><span data-stu-id="1232b-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="1232b-117">Grazie all'integrazione aziendale, è possibile archiviare tutti gli elementi in un'unica posizione, ovvero nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="1232b-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="1232b-118">È possibile creare flussi di lavoro B2B ed eseguire l'integrazione con app SaaS (Software as a Service) di terze parti, app locali e app personalizzate usando il motore delle app per la logica di Azure e tutti i relativi connettori.</span><span class="sxs-lookup"><span data-stu-id="1232b-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using the Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="1232b-119">Grazie alle funzioni di Azure, è possibile creare un codice personalizzato per le app per la logica.</span><span class="sxs-lookup"><span data-stu-id="1232b-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-to-get-started-with-enterprise-integration"></a><span data-ttu-id="1232b-120">Introduzione all'uso di Enterprise Integration</span><span class="sxs-lookup"><span data-stu-id="1232b-120">How to get started with enterprise integration?</span></span>

<span data-ttu-id="1232b-121">È possibile compilare e gestire le app B2B in Enterprise Integration Pack tramite la finestra di progettazione dell'app per la logica del **portale di Azure**.</span><span class="sxs-lookup"><span data-stu-id="1232b-121">You can build and manage B2B apps with the Enterprise Integration Pack through the Logic App Designer in the **Azure portal**.</span></span> <span data-ttu-id="1232b-122">Le app per la logica possono essere gestite anche usando [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Argomenti relativi alle app per la logica in PowerShell").</span><span class="sxs-lookup"><span data-stu-id="1232b-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="1232b-123">Di seguito vengono illustrati i passaggi più importanti della procedura da eseguire prima di creare le app nel Portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="1232b-123">Here are the high-level steps you must take before you can create apps in the Azure portal:</span></span>

![immagine di panoramica](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="1232b-125">Alcuni scenari comuni</span><span class="sxs-lookup"><span data-stu-id="1232b-125">What are some common scenarios?</span></span>

<span data-ttu-id="1232b-126">Enterprise Integration supporta gli standard del settore seguenti:</span><span class="sxs-lookup"><span data-stu-id="1232b-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="1232b-127">EDI: Electronic Data Interchange</span><span class="sxs-lookup"><span data-stu-id="1232b-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="1232b-128">EAI: Enterprise Application Integration</span><span class="sxs-lookup"><span data-stu-id="1232b-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-to-get-started"></a><span data-ttu-id="1232b-129">Elementi necessari per iniziare</span><span class="sxs-lookup"><span data-stu-id="1232b-129">Here's what you need to get started</span></span>

* <span data-ttu-id="1232b-130">Una sottoscrizione ad Azure con account di integrazione</span><span class="sxs-lookup"><span data-stu-id="1232b-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="1232b-131">Visual Studio 2015 per creare mappe e schemi</span><span class="sxs-lookup"><span data-stu-id="1232b-131">Visual Studio 2015 to create maps and schemas</span></span>
* [<span data-ttu-id="1232b-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0 (Strumenti di Enterprise Integration per le app per la logica di Microsoft Azure per Visual Studio 2015 2.0)</span><span class="sxs-lookup"><span data-stu-id="1232b-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="1232b-133">Da provare subito</span><span class="sxs-lookup"><span data-stu-id="1232b-133">Try it now</span></span>

<span data-ttu-id="1232b-134">[Distribuire un'app per la logica di invio e ricezione AS2 di esempio completamente operativa](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) che usi le funzionalità B2B per le app per la logica di Azure.</span><span class="sxs-lookup"><span data-stu-id="1232b-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses the B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="1232b-135">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="1232b-135">Learn more</span></span>
* [<span data-ttu-id="1232b-136">Contratti</span><span class="sxs-lookup"><span data-stu-id="1232b-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Informazioni sui contratti di Enterprise Integration")
* [<span data-ttu-id="1232b-137">Scenari Business to Business (B2B)</span><span class="sxs-lookup"><span data-stu-id="1232b-137">Business to Business (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "Informazioni su come creare app per la logica con funzionalità B2B")  
* [<span data-ttu-id="1232b-138">Certificati</span><span class="sxs-lookup"><span data-stu-id="1232b-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "Informazioni sui certificati di Enterprise Integration")
* [<span data-ttu-id="1232b-139">Codifica/decodifica dei file flat</span><span class="sxs-lookup"><span data-stu-id="1232b-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "Informazioni su come codificare e decodificare il contenuto dei file flat")  
* [<span data-ttu-id="1232b-140">Account di integrazione</span><span class="sxs-lookup"><span data-stu-id="1232b-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "Informazioni sugli account di integrazione")
* [<span data-ttu-id="1232b-141">Mappe</span><span class="sxs-lookup"><span data-stu-id="1232b-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Informazioni sulle mappe di Enterprise Integration")
* [<span data-ttu-id="1232b-142">Partner</span><span class="sxs-lookup"><span data-stu-id="1232b-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "Informazioni sui partner di Enterprise Integration")
* [<span data-ttu-id="1232b-143">Schemi</span><span class="sxs-lookup"><span data-stu-id="1232b-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "Informazioni sugli schemi di Enterprise Integration")
* [<span data-ttu-id="1232b-144">Convalida dei messaggi XML</span><span class="sxs-lookup"><span data-stu-id="1232b-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "Informazioni su come convalidare i messaggi XML con le app per la logica")
* [<span data-ttu-id="1232b-145">Trasformazione XML</span><span class="sxs-lookup"><span data-stu-id="1232b-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "Informazioni sulle mappe di Enterprise Integration")
* [<span data-ttu-id="1232b-146">Connettori di integrazione aziendale</span><span class="sxs-lookup"><span data-stu-id="1232b-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "Informazioni sui connettori di Enterprise Integration Pack")
* [<span data-ttu-id="1232b-147">Metadati dell'account di integrazione</span><span class="sxs-lookup"><span data-stu-id="1232b-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "Informazioni sui metadati dell'account di integrazione")
* [<span data-ttu-id="1232b-148">Monitoraggio dei messaggi B2B</span><span class="sxs-lookup"><span data-stu-id="1232b-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "Altre informazioni sul monitoraggio dei messaggi B2B")
* [<span data-ttu-id="1232b-149">Rilevamento dei messaggi B2B nel portale OMS</span><span class="sxs-lookup"><span data-stu-id="1232b-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "Altre informazioni sul rilevamento dei messaggi B2B nel portale OMS")

