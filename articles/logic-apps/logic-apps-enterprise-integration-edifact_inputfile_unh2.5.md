---
title: aaaLogic B2B App edifact decodificare risolvere UNH 2.5 - App Azure per la logica | Documenti Microsoft
description: La decodifica edifact delle app per la logica di Azure B2B risolve UNH2.5
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 6d85242d0f828fa52cdc9689938f3ba1e51b1183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a>Come i documenti con UNH 2.5 toohandle EDIFACT segmento
Se UNH 2.5 è presente nel documento EDIFACT hello, utilizzato per la ricerca dello schema. 

Esempio: campo UNH hello è **EAN008** nel messaggio EDIFACT hello  
UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'  

Messaggio hello toohandle toofollow di passaggi 
1. Aggiornare lo schema di hello
2. Controllare le impostazioni dell'accordo hello  

## <a name="update-hello-schema"></a>Aggiornare lo schema di hello
messaggio hello tooprocess, è necessario toodeploy uno schema con nome del nodo radice hello UNH 2.5.  Per un esempio, nome radice dello schema di hello sarebbe **EFACT_D03B_ORDERS_EAN008**  

Per ogni D03B_ORDERS con un altro segmento UNH 2.5, sarebbe necessario toodeploy un singolo schema.  

## <a name="add-schema-toohello-edifact-agreement"></a>Aggiungere un contratto EDIFACT toohello dello schema
### <a name="edifact-decode"></a>Decodifica EDIFACT
tooDecode hello messaggio in arrivo, configurare schema hello in hello EDIFACT contratto impostazioni di ricezione
1. Aggiungere account di integrazione di hello schema toohello    
2. Configurare schema hello in hello EDIFACT contratto impostazioni di ricezione. 
3. Selezionare il contratto EDIFACT e fare clic su **Modifica come JSON**.  Aggiungere il valore di UNH 2.5 nel contratto di ricezione hello **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)

### <a name="edifact-encode"></a>Codifica EDIFACT
tooEncode hello messaggio in arrivo, configurare impostazioni di invio contratto EDIFACT hello schema hello
1. Aggiungere account di integrazione di hello schema toohello    
2. Configurare schema hello in impostazioni di invio contratto EDIFACT hello. 
3. Selezionare il contratto EDIFACT e fare clic su **Modifica come JSON**.  Aggiungere il valore di UNH 2.5 in hello Invia contratto **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)

## <a name="next-steps"></a>Passaggi successivi
* [Altre informazioni sui contratti degli account di integrazione](../logic-apps/logic-apps-enterprise-integration-agreements.md "Informazioni sui contratti di Enterprise Integration")  