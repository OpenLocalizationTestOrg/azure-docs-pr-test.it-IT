---
title: un'app in Visual Studio senza aaaBuild | Documenti Microsoft
description: Iniziare a usare l'app senza prima in questa Guida sulla creazione, distribuzione e gestione hello app in Visual Studio.
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
ms.openlocfilehash: 74530eea6060ffe2139f7c9d6daab8a46f808162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-serverless-app-in-visual-studio-with-logic-apps-and-functions"></a>Compilare un'app senza server in Visual Studio con App per la logica e Funzioni

Gli strumenti e le funzionalità senza server disponibili in Azure consentono di sviluppare e distribuire applicazioni cloud.  Questo documento è incentrato sulla tooget avviato in Visual Studio compila un'applicazione senza server.  In [questo articolo](logic-apps-serverless-overview.md) è contenuta una panoramica degli strumenti senza server disponibili in Azure.

## <a name="getting-everything-ready"></a>Preparazione

Di seguito sono hello prerequisiti necessari toobuild un'applicazione da Visual Studio senza server:

* [Visual Studio 2017](https://www.visualstudio.com/vs/) o Visual Studio 2015 - Community, Professional o Enterprise
* [Strumenti di App per la logica per Visual Studio](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551)
* [Versione più recente di Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 o versione successiva)
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* [Strumenti di Azure funzioni base](https://www.npmjs.com/package/azure-functions-core-tools) toodebug funzioni localmente
* Web toohello Access quando si utilizza hello incorporato progettazione logica App

## <a name="getting-started-with-a-deployment-template"></a>Introduzione a un modello di distribuzione

La gestione delle risorse viene eseguita in Azure all'interno di un gruppo di risorse,  ovvero in un raggruppamento logico di risorse.  I gruppi di risorse consentono la distribuzione e la gestione di una raccolta di risorse.  Per un'applicazione senza server in Azure, il gruppo di risorse contiene sia App per la logica di Azure sia Funzioni di Azure.  Con project gruppo di risorse di hello all'interno di Visual Studio, siamo in grado di toodevelop, gestire e distribuire un'applicazione hello intera come un singolo asset.

### <a name="create-a-resource-group-project-in-visual-studio"></a>Creare un progetto Gruppo di risorse in Visual Studio

1. In Visual Studio, fare clic su tooadd un **nuovo progetto**
1. In hello **Cloud** categoria, selezionare toocreate di Azure **gruppo di risorse** progetto  
 * Se non viene visualizzata la categoria hello o progetto elencato, assicurarsi di avere hello Azure SDK per Visual Studio installati
1. Assegnare il progetto di hello un nome e il percorso e selezionare **Ok** toocreate Visual Studio richiede tooselect un modello.  È possibile selezionare toostart vuoto, iniziare con una logica di App o un'altra risorsa.  Tuttavia, in questo caso è utilizzare tooget un modello di avvio rapido di Azure che ci avviati con un'applicazione senza server.
1. Selezionare i modelli di tooshow da **Guida introduttiva di Azure** ![modelli selezionare avvio rapido di Azure][1]
1. Modello di avvio rapido senza selezionare hello: **101-logic-app-and-function-app** e fare clic su **Ok**

modello di avvio rapido Hello crea un modello di distribuzione del progetto di gruppo di risorse.  modello di Hello contiene una semplice App di logica che chiama un funzioni di Azure e restituisce il risultato di hello.  Se si apre hello `azuredeploy.json` hello di file in Esplora soluzioni, è possibile visualizzare le risorse di hello per app senza hello.

## <a name="deploying-hello-serverless-application"></a>Distribuzione di un'applicazione hello senza server

Prima di poter aprire finestra di progettazione visiva di hello logica App in Visual Studio, è necessario toobe un gruppo di risorse di Azure già distribuita.  In questo modo hello logica app toocreate progettazione hello e utilizzare connessioni tooresources e servizi.  tooget avviato, è necessario semplicemente soluzione hello toodeploy creata.

1. Progetto di hello pulsante destro del mouse in Visual Studio, selezionare **Distribuisci**e creare un **New** distribuzione ![selezionando una nuova distribuzione di risorse][2]
1. Selezionare una sottoscrizione di Azure valida e un gruppo di risorse
1. Selezionare troppo**Distribuisci** hello soluzione
1. Immettere in nome hello hello App per la logica e hello Azure funzione App.  nome della funzione Azure Hello necessario toobe univoco globale

soluzione senza Hello distribuisce nel gruppo di risorse specificato hello.  Se si osserva hello **Output** in Visual Studio è possibile visualizzare lo stato di hello della distribuzione hello.

## <a name="editing-hello-logic-app-in-visual-studio"></a>Modifica hello logica app in Visual Studio

Dopo la distribuzione di soluzioni hello in qualsiasi gruppo di risorse, finestra di progettazione visiva hello sono utilizzati tooedit e apportare le modifiche toohello logica app.

1. Pulsante destro del mouse hello `azuredeploy.json` file hello Esplora soluzioni e selezionare **Apri con logica App finestra di progettazione**
1. Seleziona hello **gruppo di risorse** e **percorso** hello soluzione è stata distribuita selezionare tooand **OK**

finestra di progettazione visiva la logica App Hello dovrebbe ora essere visibile con Visual Studio.  Possono continuare tooadd passaggi, modificare hello flusso di lavoro e salvare le modifiche.  È possibile anche creare app per la logica da Visual Studio.  Se si fa clic su hello **risorse** nello strumento di navigazione di hello modello, è possibile scegliere tooadd un **logica App** toohello progetto.  App vuota logica caricare nella finestra di progettazione visiva hello senza una pre-distribuzione in un gruppo di risorse.

### <a name="managing-and-viewing-run-history-for-a-deployed-logic-app"></a>Gestione e visualizzazione della cronologia di esecuzione di un'app per la logica distribuita

È anche possibile gestire e visualizzare la cronologia di esecuzione hello per App per la logica distribuito in Azure.  Se si apre hello **Cloud Explorer** strumento in Visual Studio, è possibile fare doppio clic su qualsiasi App per la logica e scegliere tooedit, disabilitare, visualizzare le proprietà o visualizzazione cronologia di esecuzione.  Facendo clic su Modifica consente inoltre toodownload un'app logica pubblicato in un progetto di Visual Studio risorse gruppo.  Ciò significa che anche se è stata avviata la logica app nel portale di Azure hello, è ancora possibile importare e gestire da Visual Studio.

## <a name="developing-an-azure-function-in-visual-studio"></a>Sviluppo di una funzione di Azure in Visual Studio

modello di distribuzione Hello distribuisce le funzioni di Azure che sono contenuti nella soluzione hello per il repository git hello specificato in hello `azuredeploy.json` variabili.  Se si crea un progetto di funzione all'interno di soluzione hello, archiviarla nel controllo del codice sorgente (GitHub, Visual Studio Team Services e così via) e aggiornare hello `repo` variabile, il modello di hello distribuirà hello Azure funzione.

### <a name="creating-an-azure-function-project"></a>Creazione di un progetto funzione di Azure

Se si utilizza JavaScript, Python, F #, Bash, Batch o PowerShell, seguire hello [passaggi hello funzioni CLI](../azure-functions/functions-run-local.md) toocreate un progetto.  Se lo sviluppo di una funzione in c#, è possibile utilizzare un [libreria di classi c#](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/) nella soluzione corrente hello hello Azure funzione.

## <a name="next-steps"></a>Passaggi successivi

* [Informazioni su come toobuild un dashboard di social networking senza server](logic-apps-scenario-social-serverless.md)
* [Gestire un'app per la logica da Visual Studio Cloud Explorer](logic-apps-manage-from-vs.md)
* [Linguaggio di definizione del flusso di lavoro delle app per la logica](logic-apps-workflow-definition-language.md)

<!-- Image references -->
[1]: ./media/logic-apps-serverless-get-started-vs/select-template.png
[2]: ./media/logic-apps-serverless-get-started-vs/deploy.png
