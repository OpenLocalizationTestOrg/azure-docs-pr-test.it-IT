---
title: aaaConnect tooan locale sistema SAP in Azure logica App | Documenti Microsoft
description: La connessione di sistema SAP locale di tooan dal flusso di lavoro logica app tramite gateway dati locale di hello
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a>Connettersi sistema SAP di tooan locale da App per la logica con connettore SAP hello 

gateway dati locale di Hello consente dati toomanage e accedere in modo sicuro le risorse in locale. In questo argomento viene illustrato come collegare il sistema SAP locale di logica App tooan. In questo esempio, la logica app richiede un IDOC su HTTP e Invia risposta hello.    

> [!NOTE]
> Limitazioni correnti: 
> - Logica app timeout se tutti i passaggi necessari per la risposta hello non completano entro hello [il limite di timeout della richiesta](./logic-apps-limits-and-config.md). In questo scenario, è possibile che le richieste vengano bloccate. 
> - selettore file Hello non vengono visualizzati tutti i campi disponibili hello. In questo scenario, è possibile aggiungere manualmente i percorsi.

## <a name="prerequisites"></a>Prerequisiti

- Installare e configurare più recente hello [gateway dati locale](https://www.microsoft.com/download/details.aspx?id=53127) versione 1.15.6150.1 o versione successiva. [Come tooconnect toohello sul gateway dati locale in un'app di logica](http://aka.ms/logicapps-gateway) elenchi hello passaggi. gateway di Hello deve essere installato in un computer locale prima di procedere.

- Download e installazione hello più recente SAP libreria client in hello stesso computer in cui è installato gateway dati hello. Utilizzare una delle seguenti versioni SAP hello: 
    - Server SAP
        - Qualsiasi Server SAP che hello supporto .NET Connector (NCo) 3.0
 
    - Client SAP
        - SAP Connettore .NET (NCo) 3.0

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a>Aggiungere i trigger e le azioni per la connessione del sistema SAP tooyour

connettore SAP Hello ha azioni, ma non i trigger. In tal caso, abbiamo toouse un altro trigger all'inizio di hello del flusso di lavoro hello. 

1. Aggiungere trigger di richiesta/risposta hello e quindi selezionare **nuovo passaggio**.

2. Selezionare **aggiungere un'azione**, quindi selezionare il connettore SAP hello digitando `SAP` nel campo di ricerca hello:    

     ![Selezionare il server applicazioni o il server di messaggistica SAP](media/logic-apps-using-sap-connector/sap-action.png)

3. Selezionare il [**server applicazioni SAP**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) o il [**server di messaggistica SAP**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), in base alla configurazione SAP. Se non si dispone di una connessione esistente, verrà richiesta toocreate uno.

   1. Selezionare **Connetti tramite il gateway dati locale**e immettere i dettagli di hello per il sistema SAP:   

       ![Aggiungere tooSAP di stringa di connessione](media/logic-apps-using-sap-connector/picture2.png)  

   2. In **Gateway**, selezionare un gateway esistente o un nuovo gateway tooinstall, **installare Gateway**.

        ![Installare un nuovo gateway](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. Dopo avere immesso tutti i dettagli di hello, selezionare **crea**. 
   Logica App Configura e testa connessione hello, assicurandosi che la connessione hello funziona correttamente.

4. Inserire un nome per la connessione SAP.

5. diverse opzioni di SAP Hello sono ora disponibili. toofind la categoria IDOC, seleziona dall'elenco di hello. O digitare manualmente il percorso di hello e risposta hello selezionare HTTP nell'hello **corpo** campo:

     ![Azione SAP](media/logic-apps-using-sap-connector/picture3.png)

6. Aggiungere l'azione di hello per la creazione di un **risposta HTTP**. messaggio di risposta Hello deve essere dall'output di hello SAP.

7. Salvare l'app per la logica. Test inviando un IDOC tramite URL trigger hello HTTP. Dopo la hello che viene inviato l'IDOC, attendere la risposta hello da hello logica app:   

     > [!TIP]
     > Estrarre come troppo[monitorare App per la logica](../logic-apps/logic-apps-monitor-your-logic-apps.md).

Connettore SAP hello viene aggiunta la tooyour logica app, iniziare a esplorare altre funzionalità:

- BAPI
- RFC

## <a name="get-help"></a>Ottenere aiuto

rispondere alle domande di domande tooask, e informazioni su quali altri logica app di Azure in caso di utenti, visitare hello [forum di Azure logica app](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp migliorare Azure logica App e connettori, votare o inviare idee in hello [sito commenti e suggerimenti dell'utente di Azure logica app](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Passaggi successivi

- Informazioni su come toovalidate, trasformazione e altre funzioni simili a BizTalk hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md). 
- [Connettere i dati locali tooon](../logic-apps/logic-apps-gateway-connection.md) da logica App
