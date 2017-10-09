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
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a>Panoramica: Scenari B2B e la comunicazione con hello Enterprise Integration Pack

Per i flussi di lavoro di business-to-business (B2B) e la comunicazione trasparente con le app di logica di Azure, è possibile abilitare scenari di integrazione aziendale di Microsoft basato su cloud soluzione hello Enterprise Integration Pack. Le organizzazioni saranno in grado di scambiarsi messaggi elettronicamente anche se usano formati e protocolli diversi. pack Hello Trasforma formati diversi in un formato che è in grado di interpretare ed elaborare i sistemi delle organizzazioni. Le organizzazioni possono scambiarsi messaggi grazie ai protocolli standard del settore tra cui [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md) ed [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md). È inoltre possibile proteggere i messaggi con firme digitali e crittografia.

Se si ha familiarità con BizTalk Server o servizi BizTalk di Microsoft Azure, le funzionalità di integrazione di Enterprise hello sono toouse semplice quanto la maggior parte dei concetti sono simili. La principale differenza è che Enterprise Integration utilizza integrazione account toosimplify hello archiviazione e la gestione degli elementi utilizzati nelle comunicazioni B2B. 

L'architettura hello Enterprise Integration Pack si basa su "account di integrazione". Questi account sono contenitori basati sul cloud che archiviano elementi quali schemi, partner, certificati, mappe e contratti. È possibile utilizzare toodesign questi elementi, distribuire e gestire le app B2B e anche i flussi di lavoro toobuild B2B per App per la logica. Ma prima di poter utilizzare questi elementi, è innanzitutto necessario collegare l'applicazione di integrazione account tooyour logica. Successivamente, l'app per la logica può accedere agli elementi dell'account di integrazione.

## <a name="why-should-you-use-enterprise-integration"></a>Perché usare Enterprise Integration

* Grazie all'integrazione aziendale, è possibile archiviare tutti gli elementi in un'unica posizione, ovvero nell'account di integrazione.
* È possibile creare flussi di lavoro B2B e integrare con App di terze parti software come servizio (SaaS), applicazioni locali e le applicazioni personalizzate tramite il motore di App per la logica Azure hello e tutti i connettori.
* Grazie alle funzioni di Azure, è possibile creare un codice personalizzato per le app per la logica.

## <a name="how-tooget-started-with-enterprise-integration"></a>La modalità di avvio con l'integrazione di enterprise tooget?

È possibile creare e gestire le app B2B con hello Enterprise Integration Pack tramite Progettazione applicazione logica Ciao hello **portale di Azure**. Le app per la logica possono essere gestite anche usando [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Argomenti relativi alle app per la logica in PowerShell").

Ecco i passaggi di alto livello hello che è necessario eseguire prima di poter creare le app nel portale di Azure hello:

![immagine di panoramica](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a>Alcuni scenari comuni

Enterprise Integration supporta gli standard del settore seguenti:

* EDI: Electronic Data Interchange
* EAI: Enterprise Application Integration

## <a name="heres-what-you-need-tooget-started"></a>Ecco cosa occorre tooget avviato

* Una sottoscrizione ad Azure con account di integrazione
* Visual Studio 2015 toocreate mappe e schemi
* [Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0 (Strumenti di Enterprise Integration per le app per la logica di Microsoft Azure per Visual Studio 2015 2.0)](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a>Da provare subito

[Distribuire una trasmissione AS2 esempio completamente operativo e app per la logica di ricezione](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) che utilizza le funzionalità B2B hello per le app di logica di Azure.

## <a name="learn-more"></a>Altre informazioni
* [Contratti](../logic-apps/logic-apps-enterprise-integration-agreements.md "Informazioni sui contratti di Enterprise Integration")
* [Scenari di business (B2B) tooBusiness](../logic-apps/logic-apps-enterprise-integration-b2b.md "informazioni come toocreate logica App con funzionalità B2B")  
* [Certificati](logic-apps-enterprise-integration-certificates.md "Informazioni sui certificati di Enterprise Integration")
* [Flat file codifica/decodifica](logic-apps-enterprise-integration-flatfile.md "informazioni come tooencode e decodificare il contenuto del file flat")  
* [Account di integrazione](../logic-apps/logic-apps-enterprise-integration-accounts.md "Informazioni sugli account di integrazione")
* [Mappe](../logic-apps/logic-apps-enterprise-integration-maps.md "Informazioni sulle mappe di Enterprise Integration")
* [Partner](logic-apps-enterprise-integration-partners.md "Informazioni sui partner di Enterprise Integration")
* [Schemi](logic-apps-enterprise-integration-schemas.md "Informazioni sugli schemi di Enterprise Integration")
* [Convalida del messaggio XML](logic-apps-enterprise-integration-xml.md "informazioni su come i messaggi con la logica App toovalidate XML")
* [Trasformazione XML](logic-apps-enterprise-integration-transform.md "Informazioni sulle mappe di Enterprise Integration")
* [Connettori di integrazione aziendale](../connectors/apis-list.md "Informazioni sui connettori di Enterprise Integration Pack")
* [Metadati dell'account di integrazione](../logic-apps/logic-apps-enterprise-integration-metadata.md "Informazioni sui metadati dell'account di integrazione")
* [Monitoraggio dei messaggi B2B](logic-apps-monitor-b2b-message.md "Altre informazioni sul monitoraggio dei messaggi B2B")
* [Rilevamento dei messaggi B2B nel portale OMS](logic-apps-track-b2b-messages-omsportal.md "Altre informazioni sul rilevamento dei messaggi B2B nel portale OMS")

