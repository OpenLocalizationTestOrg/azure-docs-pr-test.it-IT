---
title: aaaOverview di Azure senza | Documenti Microsoft
description: Creare potenti soluzioni cloud hello senza toothink sull'infrastruttura.
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 7c9c09d96e472edd1631892982ac60aae97342a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-serverless-with-functions-and-logic-apps"></a>Panoramica dell'architettura senza server di Azure con Funzioni e App per la logica

Le applicazioni senza server offrono una serie di vantaggi, tra cui un aumento della velocità di sviluppo, una riduzione del codice necessario e una scalabilità più semplice.  In questo articolo vengono inseriti in hello diversi attributi senza soluzioni e le offerte di Azure senza server.

## <a name="what-is-serverless"></a>Cosa significa "senza server"?

Senza server non significa che non sono presenti server - significa semplicemente che non dispone di sviluppatori hello tooworry sui server.  Gran parte dello sviluppo di applicazioni tradizionale è rispondere alle domande sulla scalabilità, l'hosting e monitoraggio delle richieste di hello toomeet soluzioni dell'applicazione hello.  Con senza server, queste domande sono preso in considerazione come parte della soluzione hello.  Le applicazioni senza server, inoltre, prevedono una fatturazione in base al consumo.  Se un'applicazione hello non viene mai utilizzata, non si verifica mai un addebito.  Queste funzionalità consentono agli sviluppatori toofocus unicamente sulla logica di business hello della soluzione hello.

servizi di base Hello in Azure intorno senza server sono [Azure funzioni](https://azure.microsoft.com/services/functions/) e [Azure logica app](https://azure.microsoft.com/services/logic-apps/).  Queste soluzioni seguire principi hello precedente e consentono agli sviluppatori di applicazioni cloud affidabile toobuild con quantità minima di codice.

## <a name="what-are-azure-functions"></a>Che cos'è Funzioni di Azure?

Funzioni di Azure è una soluzione per l'esecuzione facilmente piccoli frammenti di codice, o "funzioni", nel cloud hello. È possibile scrivere solo il codice hello che è necessario per hello problema, senza preoccuparsi di un intero toorun di infrastruttura dell'applicazione o hello. Funzioni può rendere più produttiva l'attività di sviluppo e consente di usare il linguaggio di sviluppo preferito, ad esempio C#, F#, Node.js, Python o PHP. Paga per ora hello che il codice viene eseguito e Azure viene ridimensionata in base alle esigenze.

Se si desidera toojump destra e iniziare a utilizzare le funzioni di Azure, iniziare con [creare la prima funzione Azure](../azure-functions/functions-create-first-azure-function.md). Se si cercano informazioni più tecniche sulle funzioni, vedere hello [di riferimento per sviluppatori](../azure-functions/functions-reference.md).

## <a name="what-are-azure-logic-apps"></a>Che cos'è App per la logica di Azure?

Le app di logica di Azure fornisce un modo toosimplify e implementare integrazioni scalabile e flussi di lavoro nel cloud hello. Fornisce un visual toomodel della finestra di progettazione e automatizzare il processo come una serie di passaggi di un flusso di lavoro chiamato.  Esistono [molti connettori](../connectors/apis-list.md) in tutti i servizi cloud e locali tooquickly connettersi tooother un'app senza server API.  Un'app logica inizia con un trigger (like 'quando un account viene aggiunto tooDynamics CRM') e dopo l'attivazione è possibile iniziare molte azioni combinazioni, conversioni e la condizione logica.  Logica App è un'ottima scelta quando l'orchestrazione di diverse funzioni di Azure in un processo, in particolare quando il processo di hello richiede l'interazione con un sistema esterno o l'API.

tooget iniziare con le app di logica, iniziare con [la creazione della prima applicazione logica](logic-apps-create-a-logic-app.md).  Se si cercano informazioni più tecniche sull'App per la logica, vedere hello [di riferimento per sviluppatori](logic-apps-workflow-actions-triggers.md).

## <a name="how-can-i-build-and-deploy-serverless-applications-in-azure"></a>Come è possibile compilare e distribuire applicazioni senza server in Azure?

Azure offre un'ampia gamma di strumenti di sviluppo, distribuzione e gestione per app senza server.  Le app possono essere compilate direttamente nel portale di Azure hello o con [gli strumenti di Visual Studio](logic-apps-serverless-get-started-vs.md).  Dopo essere stata sviluppata, un'applicazione può essere [immediatamente distribuita](logic-apps-create-deploy-template.md).  Azure fornisce anche strumenti per il monitoraggio di app senza server,  Questo monitoraggio è possibile accedere dal portale di Azure tramite API hello o SDK o con Application Insights e gli strumenti integrata tooOMS hello.

## <a name="next-steps"></a>Passaggi successivi

* [Iniziare a compilare un'app senza server in Visual Studio](logic-apps-serverless-get-started-vs.md)
* [Creare un dashboard Customer Insights con app senza server](logic-apps-scenario-social-serverless.md)
* [Creare un modello di distribuzione per un'app per la logica](logic-apps-create-deploy-template.md)