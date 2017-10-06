---
title: aaaValidate XML - App Azure per la logica | Documenti Microsoft
description: Convalida XML con schemi per le app di logica di Azure e gli scenari B2B usando hello Enterprise Integration Pack
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a>Enterprise Integration con convalida XML

Spesso in scenari B2B, partner hello in un contratto deve assicurarsi che i messaggi hello che dello scambio siano validi prima di poter avviare l'elaborazione dati. È possibile convalidare documenti rispetto a uno schema predefinito utilizzando hello usare hello convalida XML connettore in hello Enterprise Integration Pack.

## <a name="validate-a-document-with-hello-xml-validation-connector"></a>Convalidare un documento con il connettore di convalida XML hello

1. Creare un'applicazione, la logica e [collegare l'account di integrazione di hello app toohello](../logic-apps/logic-apps-enterprise-integration-accounts.md "informazioni toolink un'app di logica di integrazione account tooa") con schema hello desiderate toouse per la convalida dei dati XML.

2. Aggiungere un **richiesta - viene ricevuta la richiesta HTTP quando** trigger tooyour logica app.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. hello tooadd **convalida XML** azione, scegliere **aggiungere un'azione**.

4. toofilter tutti hello toohello azioni quello che si desidera, immettere *xml* nella casella di ricerca hello. Selezionare **Convalida XML**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. Selezionare toospecify hello contenuto XML che si desidera toovalidate, **contenuto**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. Selezionare i tag body hello come contenuto che si desidera toovalidate hello.

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. schema di hello toospecify desiderato toouse per la convalida di hello precedente *contenuto* di input, scegliere **nome dello SCHEMA**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. Salvare il lavoro   

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

A questo punto, la configurazione del connettore di convalida è completa. In un'applicazione reale, è possibile che i dati di hello convalidato toostore in un'app di line-of-business (LOB) come SalesForce. toosend hello tooSalesforce output convalidato, aggiungere un'azione.

tootest l'azione di convalida, creare un endpoint HTTP toohello richiesta.

## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni su Enterprise Integration Pack hello](../logic-apps/logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack")   

