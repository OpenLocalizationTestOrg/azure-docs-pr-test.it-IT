---
title: messaggi nei flussi di lavoro - App Azure per la logica di aaaWorking con XML | Documenti Microsoft
description: Elaborare, convalidare, trasformare e arricchire XML messaggi in App per la logica e l'utilizzo di business tooscenarios hello Enterprise Integration Pack
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 47672dc4-1caa-44e5-b8cb-68ec3a76b7dc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 02/27/2017
ms.author: LADocs; mandia
ms.openlocfilehash: f90ae89fef0a4bd17286adbce398e573940bb790
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a>Convalidare e trasformare il linguaggio XML, codificare e decodificare file flat e migliorare le funzionalità di messaggi nelle app per la logica

Usare la logica App, è necessario hello possibilità tooprocess messaggi XML inviati e ricevuti. Questa funzionalità è inclusa con hello Enterprise Integration Pack. Per gli utenti con uno sfondo di BizTalk Server, hello Enterprise Integration Pack offre tootransform funzionalità simili e convalidare i messaggi, utilizzare i file flat e anche utilizzare XPath tooenrich o estrarre le proprietà specifiche da un messaggio. 

Per gli utenti che sono di nuovo spazio toothis, queste funzionalità espandere la modalità di elaborazione messaggi all'interno del flusso di lavoro. Ad esempio, se sono in uno scenario business-to-business e lavorare con schemi XML specifici, è possibile utilizzare hello Enterprise Integration Pack tooenhance come la società elabora questi messaggi. 

Hello Enterprise Integration Pack include: 

* [Convalida dei messaggi XML](logic-apps-enterprise-integration-xml-validation.md "Informazioni sulla convalida dei messaggi XML"): consente di convalidare un messaggio XML in entrata o in uscita rispetto a uno schema specifico.
* [Trasformazione XML](../logic-apps/logic-apps-enterprise-integration-transform.md "ulteriori informazioni sulle trasformazioni di messaggi XML e mappe") : convertire o personalizzare un messaggio XML basato su requisiti o requisiti hello di un partner.
* [Codifica e decodifica del file flat](logic-apps-enterprise-integration-flatfile.md "Informazioni sulla codifica o decodifica del file flat"): consente di codificare o decodificare un file flat. Ad esempio, SAP accetta e invia file IDOC in formato file flat. Molte piattaforme di integrazione creano messaggi XML, tra cui App per la logica. In tal caso, è possibile creare un'app di logica che utilizza hello file flat codificatore troppo "conversione" file tooflat di file XML. 
* [XPath](https://msdn.microsoft.com/library/mt643789.aspx) - arricchire il messaggio ed estrarre le proprietà specifiche dal messaggio hello. È possibile quindi utilizzare hello estratti destinazione tooa dei messaggi hello tooroute proprietà o un endpoint intermedio.

## <a name="try-it-out"></a>Provare il servizio
[Distribuire un'app logica completamente operativa ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (esempio di GitHub) utilizzando le funzionalità XML hello nelle app di logica di Azure.

## <a name="learn-more"></a>Altre informazioni
[Altre informazioni su Enterprise Integration Pack hello](../logic-apps/logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack")
