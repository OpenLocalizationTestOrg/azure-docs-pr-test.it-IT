---
title: aaaExamples & comuni scenari - App Azure per la logica | Documenti Microsoft
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
ms.openlocfilehash: 17caa8539ec6a57726b9c6c07a71fb74caa07ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="examples-and-common-scenarios-for-azure-logic-apps"></a>Esempi e scenari comuni per le app per la logica di Azure

altre informazioni, vedere toohelp hello molti modelli e funzionalità in app di logica di Azure, di seguito sono esempi e scenari comuni.

## <a name="key-scenarios-for-logic-apps"></a>Scenari principali per le app per la logica

Le app per la logica di Azure forniscono l'orchestrazione e l'integrazione resilienti per diversi servizi. servizio App per la logica di Hello è "senza server", in modo non si dispone di tooworry sulla scala o istanze - si hanno toodo è definire hello flusso di lavoro (trigger e azioni). la piattaforma sottostante Hello gestisce scalabilità, disponibilità e prestazioni. Qualsiasi scenario in cui è necessario toocoordinate più azioni, soprattutto in più sistemi operativi, è un ottimo caso d'uso per le app di logica di Azure. Ecco alcuni modelli ed esempi.

## <a name="respond-tootriggers-and-extend-actions"></a>Rispondere tootriggers ed estendere le azioni

Ogni app per la logica inizia con un trigger. Ad esempio, il flusso di lavoro può iniziare con un evento pianificato, una chiamata a manuale o un evento da un sistema esterno, ad esempio hello "quando un file viene aggiunto il server FTP tooan" trigger. Le app di logica di Azure supporta attualmente più di 100 connettori di pronto all'uso, compreso tooMicrosoft SAP locale servizi cognitivi. Per i sistemi e i servizi che non potrebbero non avere connettori pubblicati, è anche possibile estendere le app per la logica.

* [Creare trigger o azioni personalizzate](../logic-apps/logic-apps-create-api-app.md)
* [Configurare azioni con esecuzione prolungata per l'esecuzione dei flussi di lavoro](../logic-apps/logic-apps-create-api-app.md)
* [Rispondere a eventi tooexternal e le azioni con webhook](../logic-apps/logic-apps-create-api-app.md)
* [Chiamare, trigger, o nidificare i flussi di lavoro con le risposte sincrone tooHTTP richieste](../logic-apps/logic-apps-http-endpoint.md)
* [Esercitazione: Rispondere tooTwilio SMS webhook e inviare una risposta di testo](https://channel9.msdn.com/Blogs/Windows-Azure/Azure-Logic-Apps-Walkthrough-Webhook-Functions-and-an-SMS-Bot)
* [Esercitazione: Creare un dashboard social basato su AI in pochi minuti con le app per la logica e Power BI](http://aka.ms/logicappsdemo)

## <a name="error-handling-logging-and-control-flow-capabilities"></a>Funzionalità di gestione degli errori, registrazione e flusso di controllo

Le app per la logica includono funzionalità sofisticate per il flusso di controllo avanzato, come condizioni, istruzioni switch, cicli e ambiti. soluzioni resilienti tooensure, è anche possibile implementare errore e le eccezioni nei flussi di lavoro. Per i log di notifica e di diagnostica per lo stato di esecuzione dei flussi di lavoro, le app per la logica di Azure forniscono inoltre monitoraggio e avvisi.

* [Eseguire azioni differenti con le istruzioni switch](../logic-apps/logic-apps-switch-case.md)
* [Elaborare elementi in matrici e raccolte con cicli e batch nelle app per la logica](../logic-apps/logic-apps-loops-and-scopes.md)
* [Creare la gestione degli errori e delle eccezioni in un flusso di lavoro](../logic-apps/logic-apps-exception-handling.md)
* [Attivare il monitoraggio, la registrazione e gli avvisi per le app per la logica esistenti](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Abilitare il monitoraggio e la registrazione diagnostica durante la creazione di app per la logica](../logic-apps/logic-apps-monitor-your-logic-apps-oms.md)
* [Caso d'uso: come un'organizzazione sanitaria usa la gestione delle eccezioni delle app per la logica per i flussi di lavoro HL7 FHIR](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)

## <a name="deploy-and-manage-logic-apps"></a>Distribuire e gestire app per la logica

È possibile sviluppare e distribuire interamente app per la logica con Visual Studio, Visual Studio Team Services o qualsiasi altro strumento di controllo del codice sorgente e compilazione automatica. toosupport distribuzione per flussi di lavoro e le connessioni di dipendenti in un modello di risorsa, App per la logica di utilizzare modelli di distribuzione delle risorse di Azure. Strumenti di Visual Studio generano automaticamente i modelli, che è possibile controllare nel controllo toosource per il controllo delle versioni.

* [Creare un modello di distribuzione automatizzato](../logic-apps/logic-apps-create-deploy-template.md)
* [Compilare e distribuire app per la logica in Visual Studio](../logic-apps/logic-apps-deploy-from-vs.md)
* [Monitoraggio integrità hello di App per la logica](../logic-apps/logic-apps-monitor-your-logic-apps.md)

## <a name="content-types-conversions-and-transformations-within-a-run"></a>Tipi di contenuto, conversioni e trasformazioni durante un'esecuzione

È possibile accedere, convertire e trasformare più tipi di contenuto tramite hello molte funzioni hello Azure logica app [il linguaggio di definizione del flusso di lavoro](http://aka.ms/logicappsdocs). Ad esempio, è possibile convertire tra una stringa JSON e XML con hello `@json()` e `@xml()` espressioni del flusso di lavoro. motore di App per la logica di Hello mantiene il trasferimento del contenuto toosupport tipi di contenuto in modo senza perdita di dati tra servizi.

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
- [Creare definizioni di flusso di lavoro con il linguaggio di definizione del flusso di lavoro hello](../logic-apps/logic-apps-author-definitions.md)
- [Inviare domande, commenti o suggerimenti su come migliorare le app per la logica di Azure](https://feedback.azure.com/forums/287593-logic-apps)