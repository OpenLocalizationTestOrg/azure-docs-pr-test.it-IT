---
title: soluzioni aaaCreate B2B - App Azure per la logica | Documenti Microsoft
description: "Ricevere i dati nella logica App usando le funzionalità di hello B2B di hello Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a>La ricezione dei dati nella logica di applicazioni con funzionalità B2B hello hello Enterprise Integration Pack

Dopo aver creato un account di integrazione con partner e contratti, si è pronti toocreate un flusso di lavoro di business (B2B) toobusiness per l'app logica con hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).

## <a name="prerequisites"></a>Prerequisiti

toouse hello X12 e AS2 azioni, è necessario disporre di un Account di integrazione aziendale. Informazioni su [come toocreate un'integrazione Enterprise Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).

## <a name="create-a-logic-app-with-b2b-connectors"></a>Creare un'app per la logica con connettori B2B

Seguire queste app per la logica toocreate un B2B passaggi che utilizza hello AS2 e X12 dati tooreceive azioni da un partner commerciale:

1. Creare un'applicazione di logica, quindi [collegare l'account di integrazione di app tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md).

2. Aggiungere un **richiesta - viene ricevuta la richiesta HTTP quando** trigger tooyour logica app.

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. hello tooadd **decodifica AS2** azione, selezionare **aggiungere un'azione**.

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. toofilter toohello azioni tutto quello che si desidera, immettere la parola hello **as2** nella casella di ricerca hello.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. Seleziona hello **AS2 - messaggio AS2 decodificare** azione.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. Aggiungere hello **corpo** che si desidera toouse come input. In questo esempio, selezionare corpo hello della richiesta HTTP hello che trigger hello logica app. Oppure immettere un'espressione che inserisce le intestazioni di hello in hello **intestazioni** campo:

    @triggerOutputs()['headers']

7. Aggiungere hello necessario **intestazioni** per AS2, è possibile trovare nelle intestazioni di richiesta HTTP hello. In questo esempio, selezionare le intestazioni di hello della richiesta HTTP hello trigger hello logica app.

8. Ora aggiungere l'azione del messaggio hello Decode X12. Selezionare **Aggiungi un'azione**.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. toofilter toohello azioni tutto quello che si desidera, immettere la parola hello **x12** nella casella di ricerca hello.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. Seleziona hello **X12-decodificare X12 messaggio** azione.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. Ora è necessario specificare l'azione di input toothis hello. Questo input è l'output di hello dall'azione AS2 precedente hello.

    contenuto del messaggio effettivo Hello è in un oggetto JSON e codificato in base64, pertanto è necessario specificare un'espressione come input hello. 
    Immettere l'espressione in hello seguente hello **X12 FLAT FILE messaggio tooDECODE** campo di input:
    
    @base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])

    Aggiungere i passaggi dati hello X12 toodecode ricevuto dal partner commerciale hello e gli elementi in un oggetto JSON di output. 
    partner hello toonotify hello dati è stato ricevuto, è possibile restituire una risposta contenente hello AS2 notifica MDN (Message Disposition) in un'azione di risposta HTTP.

12. hello tooadd **risposta** azione, scegliere **aggiungere un'azione**.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. toofilter toohello azioni tutto quello che si desidera, immettere la parola hello **risposta** nella casella di ricerca hello.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. Seleziona hello **risposta** azione.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. tooaccess hello MDN dall'output di hello di hello **messaggio X12 Decode** azione, set hello risposta **corpo** campo con questa espressione:

    @base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. Salvare il lavoro.

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

La configurazione dell'app per la logica B2B è completata. In un'applicazione reale, è opportuno toostore hello decodificati X12 dati in un archivio line-of-business (LOB) app o i dati. tooconnect delle applicazioni LOB e usare queste API nell'app logica, è possibile aggiungere ulteriori azioni o le API personalizzate di scrittura.

## <a name="features-and-use-cases"></a>Funzionalità e casi d'uso

* Hello AS2 e X12 decodificare e codificare azioni consentono scambiare dati tra partner commerciali tramite protocolli standard del settore in App per la logica.
* dati tooexchange con partner commerciali, è possibile utilizzare AS2 e X12 con o senza di loro.
* azioni B2B Hello consentono di creare facilmente i partner e contratti nell'account di integrazione e utilizzarli in un'app di logica.
* Quando si estende la propria app per la logica con altre azioni, è possibile inviare e ricevere dati tra altre applicazioni e altri servizi come SalesForce.

## <a name="learn-more"></a>Altre informazioni
[Altre informazioni su hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md)
