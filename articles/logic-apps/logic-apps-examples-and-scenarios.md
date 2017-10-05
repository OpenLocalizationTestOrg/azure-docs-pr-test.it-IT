---
title: Esempi e scenari comuni- App per la logica di Azure | Microsoft Docs
description: Altre informazioni sulle app per la logica con esempi, scenari ed esercitazioni
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: e06311bc-29eb-49df-9273-1f05bbb2395c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/9/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 50df1e3db239a6aa34ac91bfbd582625c5b0041b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="examples-and-common-scenarios-for-azure-logic-apps"></a>Esempi e scenari comuni per le app per la logica di Azure

Per fornire maggiori informazioni sui numerosi modelli e sulle funzionalità delle app per la logica di Azure, di seguito sono elencati alcuni esempi e scenari comuni.

## <a name="key-scenarios-for-logic-apps"></a>Scenari principali per le app per la logica

Le app per la logica di Azure forniscono l'orchestrazione e l'integrazione resilienti per diversi servizi. Il servizio delle app per la logica è "senza server", quindi non è necessario preoccuparsi di scalabilità o istanze, tutto quello che l'utente deve fare è definire il flusso di lavoro (trigger e azioni). La piattaforma sottostante gestisce scalabilità, disponibilità e prestazioni. Qualsiasi scenario in cui occorra coordinare più azioni, soprattutto fra più sistemi, è un caso d'uso ottimale per le app per la logica di Azure. Ecco alcuni modelli ed esempi.

## <a name="respond-to-triggers-and-extend-actions"></a>Rispondere ai trigger ed estendere le azioni

Ogni app per la logica inizia con un trigger. Ad esempio, il flusso di lavoro può iniziare con un evento pianificato, una chiamata manuale o un evento da un sistema esterno, ad esempio il trigger "quando un file viene aggiunto a un server FTP". App per la logica di Azure supporta attualmente oltre 100 connettori pronti per l'uso, che vanno da sistemi SAP locali a Servizi cognitivi Microsoft. Per i sistemi e i servizi che non potrebbero non avere connettori pubblicati, è anche possibile estendere le app per la logica.

* [Creare trigger o azioni personalizzate](../logic-apps/logic-apps-create-api-app.md)
* [Configurare azioni con esecuzione prolungata per l'esecuzione dei flussi di lavoro](../logic-apps/logic-apps-create-api-app.md)
* [Rispondere ad azioni ed eventi esterni con webhook](../logic-apps/logic-apps-create-api-app.md)
* [Chiamare, attivare o annidare flussi di lavoro con risposte sincrone alle richieste HTTP](../logic-apps/logic-apps-http-endpoint.md)
* [Esercitazione: Rispondere ai webhook SMS di Twilio e inviare una risposta di testo](https://channel9.msdn.com/Blogs/Windows-Azure/Azure-Logic-Apps-Walkthrough-Webhook-Functions-and-an-SMS-Bot)
* [Esercitazione: Creare un dashboard social basato su AI in pochi minuti con le app per la logica e Power BI](http://aka.ms/logicappsdemo)

## <a name="error-handling-logging-and-control-flow-capabilities"></a>Funzionalità di gestione degli errori, registrazione e flusso di controllo

Le app per la logica includono funzionalità sofisticate per il flusso di controllo avanzato, come condizioni, istruzioni switch, cicli e ambiti. Per garantire soluzioni resilienti, è anche possibile implementare la gestione degli errori e delle eccezioni nei flussi di lavoro. Per i log di notifica e di diagnostica per lo stato di esecuzione dei flussi di lavoro, le app per la logica di Azure forniscono inoltre monitoraggio e avvisi.

* [Eseguire azioni differenti con le istruzioni switch](../logic-apps/logic-apps-switch-case.md)
* [Elaborare elementi in matrici e raccolte con cicli e batch nelle app per la logica](../logic-apps/logic-apps-loops-and-scopes.md)
* [Creare la gestione degli errori e delle eccezioni in un flusso di lavoro](../logic-apps/logic-apps-exception-handling.md)
* [Attivare il monitoraggio, la registrazione e gli avvisi per le app per la logica esistenti](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Abilitare il monitoraggio e la registrazione diagnostica durante la creazione di app per la logica](../logic-apps/logic-apps-monitor-your-logic-apps-oms.md)
* [Caso d'uso: come un'organizzazione sanitaria usa la gestione delle eccezioni delle app per la logica per i flussi di lavoro HL7 FHIR](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)

## <a name="deploy-and-manage-logic-apps"></a>Distribuire e gestire app per la logica

È possibile sviluppare e distribuire interamente app per la logica con Visual Studio, Visual Studio Team Services o qualsiasi altro strumento di controllo del codice sorgente e compilazione automatica. Per supportare la distribuzione per i flussi di lavoro e le connessioni dipendenti in un modello di risorse, le app per la logica usano i modelli di distribuzione delle risorse di Azure. Gli strumenti di Visual Studio generano automaticamente questi modelli, che è possibile archiviare per il controllo del codice sorgente finalizzato al controllo delle versioni.

* [Creare un modello di distribuzione automatizzato](../logic-apps/logic-apps-create-deploy-template.md)
* [Compilare e distribuire app per la logica in Visual Studio](../logic-apps/logic-apps-deploy-from-vs.md)
* [Verificare l'integrità delle app per la logica](../logic-apps/logic-apps-monitor-your-logic-apps.md)

## <a name="content-types-conversions-and-transformations-within-a-run"></a>Tipi di contenuto, conversioni e trasformazioni durante un'esecuzione

È possibile accedere, convertire e trasformare più tipi di contenuto usando le numerose funzioni del [linguaggio di definizione del flusso di lavoro](http://aka.ms/logicappsdocs) delle app per la logica di Azure. Ad esempio, è possibile eseguire la conversione tra una stringa, il formato JSON e il formato XML con le espressioni del flusso di lavoro `@json()` e `@xml()`. Il motore delle app per la logica mantiene i tipi di contenuto per supportare il trasferimento del contenuto senza perdita di dati tra i servizi.

* [Gestire i tipi di contenuto non JSON](../logic-apps/logic-apps-content-type.md), come `application/xml`, `application/octet-stream` e `multipart/formdata`
* [Funzionamento delle espressioni del flusso di lavoro nelle app per la logica](../logic-apps/logic-apps-author-definitions.md)
* [Riferimento: Azure Logic Apps workflow definition language](http://aka.ms/logicappsdocs) (Linguaggio di definizione del flusso di lavoro delle app per la logica di Azure)

## <a name="other-integrations-and-capabilities"></a>Altre integrazioni e funzionalità

Le app per la logica offrono inoltre l'integrazione con molti servizi, come Funzioni di Azure, Gestione API di Azure, Servizi app di Azure e gli endpoint HTTP personalizzati, ad esempio REST e SOAP.

* [Create a real-time social dashboard with Azure Serverless](../logic-apps/logic-apps-scenario-social-serverless.md) (Creare un dashboard di social networking in tempo reale senza server di Azure)
* [Chiamare Funzioni di Azure da app per la logica](../logic-apps/logic-apps-azure-functions.md)
* [Scenario: Attivare app per la logica con Funzioni di Azure](../logic-apps/logic-apps-scenario-function-sb-trigger.md)
* [Blog: Call SOAP endpoints from logic apps](https://blogs.msdn.microsoft.com/logicapps/2016/04/07/using-soap-services-with-logic-apps/) (Chiamare endpoint SOAP da app per la logica)

## <a name="end-to-end-scenarios"></a>Scenari end-to-end

* [Whitepaper: Enterprise integration end-to-end case management with Azure services, like Logic Apps](https://aka.ms/enterprise-integration-e2e-case-management-utilities-logic-apps) (White paper: gestione dei casi end-to-end di integrazione aziendale con i servizi di Azure, ad esempio App per la logica)

## <a name="next-steps"></a>Passaggi successivi

- [Gestire errori ed eccezioni nelle app per la logica](../logic-apps/logic-apps-exception-handling.md)
- [Creare definizioni dei flussi di lavoro con il linguaggio di definizione del flusso di lavoro](../logic-apps/logic-apps-author-definitions.md)
- [Inviare domande, commenti o suggerimenti su come migliorare le app per la logica di Azure](https://feedback.azure.com/forums/287593-logic-apps)