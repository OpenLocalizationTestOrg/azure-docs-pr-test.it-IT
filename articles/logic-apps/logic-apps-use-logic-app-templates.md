---
title: i flussi di lavoro aaaCreate dai modelli - App Azure per la logica | Documenti Microsoft
description: 'Introduzione: creare rapidamente flussi di lavoro usando le app di Azure logica App modelli tooconnect e integrare i dati.'
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 3656acfb-eefd-4e75-b5d2-73da56c424c9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0127523662a12076772b52968f1e2f9cbad72a1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-workflow-using-a-pre-built-template-or-pattern-tooget-started-quickly"></a>Configurare un flusso di lavoro utilizzando un modello predefinito o un modello tooget in tempi brevi

## <a name="what-are-logic-app-templates"></a>Informazioni sui modelli di app per la logica
Un modello di applicazione logica è un'applicazione preesistente logica che è possibile utilizzare tooquickly iniziare a creare il proprio flusso di lavoro. 

Questi modelli sono toodiscover un buon metodo vari modelli che possono essere compilate tramite App per la logica. È possibile utilizzare questi modelli come-è o modificarle toofit lo scenario.

## <a name="overview-of-available-templates"></a>Panoramica dei modelli disponibili
Sono disponibili numerosi modelli disponibili attualmente pubblicati in hello logica app della piattaforma. Alcune categorie di esempio, come tipo hello di connettori utilizzati in esse, è elencato di seguito.

### <a name="enterprise-cloud-templates"></a>Modelli cloud dell'organizzazione
Modelli che si integrano Dynamics CRM, Salesforce, Box, BLOB di Azure e altri connettori per le esigenze cloud dell'organizzazione. Alcuni esempi di operazioni eseguibili con questi modelli includono l'organizzazione dei lead e il backup dei dati di file aziendali.

### <a name="enterprise-integration-pack-templates"></a>Modelli di Enterprise Integration Pack
Configurazioni di VETER (convalidare, estrarre, trasformare, arricchire, indirizzare) pipeline, ricezione X12 EDI tramite AS2 del documento e trasformandolo tooXML, come il messaggio X12 e AS2 gestione.

### <a name="protocol-pattern-templates"></a>Modelli di schema di protocollo
Questi modelli sono costituiti da app per la logica che contengono schemi di protocollo, ad esempio richiesta-risposta HTTP e integrazioni tra FTP e SFTP. È possibile usarli senza apportare modifiche oppure come base per creare schemi di protocollo più complessi.  

### <a name="personal-productivity-templates"></a>Modelli per la produttività personale
Modelli toohelp migliorare la produttività personale includono modelli che impostare promemoria giornalieri, trasformare gli elementi di lavoro importanti in elenchi di attività e automatizzare le attività di lunga durata verso il basso tooa passaggio di approvazione singolo utente.

### <a name="consumer-cloud-templates"></a>Modelli cloud di livello consumer
Modelli semplici che si integrano con servizi di social media come Twitter, Slack e posta elettronica, in grado di potenziare le iniziative di marketing sui social media. Includono anche modelli di copia per il cloud, che consentono di aumentare la produttività risparmiando il tempo necessario per attività tradizionalmente ripetitive. 

## <a name="how-toocreate-a-logic-app-using-a-template"></a>Come toocreate un'app di logica utilizzando un modello
tooget avviato utilizzando un modello di applicazione logica, andare nella finestra di progettazione di hello logica app. Se si immette progettazione hello aprendo un'app esistente di logica, hello logica app carica automaticamente nella visualizzazione della finestra di progettazione. Tuttavia, se si crea una nuova app di logica, vedrai schermata hello riportata di seguito.  
 ![](../../includes/media/app-service-logic-templates/template7.png)  

In questa schermata è possibile scegliere toostart con un'app logica vuoto o un modello predefinito. Se si seleziona uno dei modelli di hello, vengono fornite informazioni aggiuntive. In questo esempio, si usa hello *quando viene creato un nuovo file in Dropbox, copiarlo tooOneDrive* modello.  
 ![](../../includes/media/app-service-logic-templates/template2.png)  

Se si sceglie toouse hello modello, è sufficiente selezionare hello *utilizzare questo modello* pulsante. Verrà chiesto toosign tooyour conti in base a quale modello di hello connettori utilizza. Se è stata precedentemente stabilita una connessione con questi connettori, è anche possibile selezionare Continua come illustrato di seguito.  
 ![](../../includes/media/app-service-logic-templates/template3.png)  

Dopo avere stabilito la connessione hello e selezionando *continuare*, hello logica app viene aperto in visualizzazione progettazione.  
 ![](../../includes/media/app-service-logic-templates/template4.png)  

Nell'esempio hello sopra, come accade hello con molti modelli, alcuni hello obbligatorio dei campi delle proprietà possono essere compilati all'interno di connettori hello; alcuni, tuttavia, potrebbe essere necessario un valore prima di poter tooproperly distribuire app per la logica hello. Se si tenta di toodeploy senza dover immettere alcuni dei campi mancanti hello, riceve una notifica con un messaggio di errore.

Se si desidera visualizzatore modello di tooreturn toohello, selezionare hello *modelli* pulsante nella barra di spostamento superiore hello. Passando visualizzatore modello di toohello indietro, si perde alcun progresso non salvato. Tooswitching precedenti nel Visualizzatore di modello, si verrà visualizzato un messaggio di avviso di notifica di questo oggetto.  
 ![](../../includes/media/app-service-logic-templates/template5.png)  

## <a name="how-toodeploy-a-logic-app-created-from-a-template"></a>Come toodeploy una logica app è stato creato da un modello
Dopo aver caricato il modello e apportate le modifiche desiderate, selezionare hello pulsante Salva nell'angolo superiore sinistro di hello. In questo modo, l'app per la logica verrà salvata e pubblicata.  
 ![](../../includes/media/app-service-logic-templates/template6.png)  

Se ad esempio informazioni su come tooadd più passaggi in un modello di app logica esistente oppure apportare modifiche in generale, leggere informazioni, vedere [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).

