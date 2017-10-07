---
title: App aaaConnect e integrare i dati con i flussi di lavoro - App Azure per la logica | Documenti Microsoft
description: Creare flussi di lavoro e automatizzare i processi connettendo app e integrando dati con App per la logica di Azure.
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 07765c05-72a6-4169-a8ab-f6420bfbaf07
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: klam
ms.openlocfilehash: 53d4e165bb2205ddd56c1950719389725267ddea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-logic-apps"></a>Cosa sono le app per la logica?
App per la logica forniscono un modo toosimplify e implementare flussi di lavoro e integrazioni scalabile nel cloud hello. Fornisce un visual toomodel della finestra di progettazione e automatizzare il processo come una serie di passaggi noto come un flusso di lavoro.  Esistono [molti connettori](../connectors/apis-list.md) tra hello cloud e locali tooquickly integrare tra servizi e protocolli.  Un'app logica inizia con un trigger (like 'quando un account viene aggiunto tooDynamics CRM') e dopo l'attivazione può iniziare molte combinazioni di azioni, conversioni e la condizione logica.

esempio hello vantaggi di Hello d'uso delle App logica:  

* Risparmiare tempo con la progettazione di processi complessi utilizzando strumenti di progettazione semplice toounderstand
* Implementazione di modelli e i flussi di lavoro senza problemi, che altrimenti sarebbe difficile tooimplement nel codice
* Possibilità di iniziare subito la progettazione dai modelli
* Personalizzazione dell'app per la logica con API, azioni e codice personalizzati
* La connessione e sincronizzare i sistemi locali e cloud hello
* Possibilità di sfruttare BizTalk Server, Gestione API, Funzioni di Azure e il bus di servizio di Azure con supporto ottimale dell'integrazione

Logica App è un iPaaS completamente gestito (integrazione di piattaforma come servizio) consentendo agli sviluppatori non toohave tooworry sulla compilazione di hosting, scalabilità, disponibilità e gestione.  Logica App verrà scalare automaticamente toomeet richiesta.

![Finestra di progettazione del flusso di app](media/logic-apps-what-are-logic-apps/LogicAppCapture2.png)

Come indicato, le app per la logica consentono di automatizzare i processi aziendali. Ecco alcuni esempi:  

* Spostare i file caricati server FTP tooan nell'archiviazione di Azure
* Elaborazione e instradamento di ordini in sistemi locali e cloud
* Monitorare tutti i TWEET su un determinato argomento, analizzare sentiment hello e creare avvisi e alle attività per gli elementi che richiedono il completamento.

È possibile configurare questi scenari tutti dalla finestra di progettazione visiva hello e senza scrivere una singola riga di codice. È possibile iniziare subito a [creare la propria app per la logica][create].  Dopo che è stata scritta, un'app per la logica può essere [distribuita e riconfigurata rapidamente](../logic-apps/logic-apps-create-deploy-template.md) in più ambienti e aree.

## <a name="why-logic-apps"></a>Perché usare le app per la logica?
Logica App consente la scalabilità e velocità hello integrazione aziendali.  facilità di Hello di utilizzo di progettazione di hello, ampia gamma di potenti strumenti di gestione, trigger e azioni rendere centralizzare le API più semplice che mai.  Le aziende lo spostamento verso digitalization, App per la logica consente i sistemi legacy e all'avanguardia tooconnect insieme.

Inoltre, con il nostro [Enterprise Integration Account] [ biztalk] è possibile scalare toomature scenari di integrazione con la potenza di hello un [messaggistica XML] [ xml], [Gestione partner commerciali][tpm]e altro ancora.

* **Strumenti di progettazione semplice toouse** -App per la logica può essere progettata end-to-end nel browser hello o con strumenti di Visual Studio. Iniziare con un trigger: da toowhen una pianificazione semplice e che viene creato un problema di GitHub. Quindi orchestrare qualsiasi numero di azioni tramite hello raccolta avanzati dei connettori.
* **Connettersi con facilità le API** -attività di composizione anche facile toodescribe sono tooimplement difficile nel codice. Logica App rende facile tooconnect diversi sistemi. Desidera tooconnect cloud marketing soluzione tooyour locale sistema di fatturazione? Scegliere se toocentralize su sistemi con un Bus di servizio dell'organizzazione e le API di messaggistica. Logica App sono hello il modo più veloce e più affidabile toodeliver soluzioni toothese ai problemi.
* **Per iniziare rapidamente dai modelli** -toohelp iniziare è stato fornito un [raccolta di modelli] [ templates] che consentono di toorapidly creare alcune soluzioni comuni. Da avanzate soluzioni B2B connettività SaaS toosimple e anche alcuni sono solo 'for 'fun - raccolta hello è tooget modo più rapido hello avviato con la potenza di hello di App per la logica.
* **Estendibilità baked in** -non viene visualizzato il connettore di hello è necessario? Logica App è progettato toowork con le API e codice. è possibile creare la propria toouse app API come un connettore personalizzato, o chiamare un [funzione Azure](https://functions.azure.com) tooexecute frammenti di codice su richiesta. 
* **Straordinaria potenza di integrazione reale** : è possibile iniziare facilmente e svilupparsi secondo le necessità. Logica App può sfruttare facilmente potenza hello di BizTalk, settore iniziali integrazione soluzione tooenable professionisti toobuild hello soluzioni di integrazione Microsoft necessari. Ulteriori informazioni su hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).

## <a name="logic-app-concepts"></a>Concetti delle app per la logica
di seguito Hello sono alcuni dei componenti chiave hello che costituiscono l'esperienza di App per la logica di hello. 

* **Flusso di lavoro** -App per la logica fornisce toomodel una rappresentazione grafica dei processi aziendali come una serie di passaggi o di un flusso di lavoro.
* **Gestito connettori** -App per la logica è necessario accedere ai servizi e toodata. Connettori gestiti vengono creati in modo specifico tooaid quando ci si connette tooand utilizzo dei dati. Vedere l'elenco hello dei connettori ora disponibili in [gestiti connettori][managedapis].
* **Trigger** : alcuni connettori gestiti possono fungere anche da trigger. Un trigger avvia una nuova istanza del flusso di lavoro in base a un evento specifico, ad esempio hello arrivo del messaggio di posta elettronica o una modifica nell'account di archiviazione di Azure.
* **Azioni** -ogni passaggio dopo la chiamata di un'azione trigger hello in un flusso di lavoro. Ogni azione in genere viene eseguito il mapping operazione tooan sul connettore gestito o App per le API personalizzate.
* **Enterprise Integration Pack** : per scenari di integrazione più avanzati, le app per la logica includono funzionalità di BizTalk. BizTalk è la piattaforma di integrazione leader del settore di Microsoft. i connettori di Hello Enterprise Integration Pack consentono di tooeasily includono la convalida, trasformazione e più flussi di lavoro logica App tooyour.

## <a name="getting-started"></a>Introduzione
* iniziare con le app di logica, tooget seguire hello [creare un'App di logica] [ create] esercitazione.  
* [Visualizzare esempi e scenari comuni](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Le app per la logica consentono di automatizzare i processi aziendali](http://channel9.msdn.com/Events/Build/2016/T694) 
* [Informazioni su come tooIntegrate i sistemi con logica App](http://channel9.msdn.com/Events/Build/2016/P462)

[biztalk]: logic-apps-enterprise-integration-accounts.md
[appservice]: ../app-service/app-service-value-prop-what-is.md
[create]: logic-apps-create-a-logic-app.md
[managedapis]: ../connectors/apis-list.md
[tpm]: logic-apps-enterprise-integration-accounts.md
[xml]: logic-apps-enterprise-integration-b2b.md
[templates]: logic-apps-use-logic-app-templates.md
