---
title: i messaggi AS2 aaaEncode - App Azure per la logica | Documenti Microsoft
description: Come toouse hello codificatore AS2 in hello Enterprise Integration Pack per le app di logica di Azure
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Codificare i messaggi AS2 per App di Azure logica con hello Enterprise Integration Pack

tooestablish protezione e affidabilità durante la trasmissione di messaggi, utilizzare connettore di messaggi hello codificare AS2. Questo connettore consente la firma digitale, crittografia e riconoscimenti tramite notifiche MDN (Message Disposition), che comporta anche la toosupport per il Non ripudio.

## <a name="before-you-start"></a>Prima di iniziare

Ecco gli elementi di hello che è necessario:

* Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)
* Un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md) già definito e associato alla sottoscrizione di Azure. È necessario disporre di un connettore di messaggi AS2 codificare integrazione account toouse hello.
* Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.
* Un [contratto AS2](logic-apps-enterprise-integration-as2.md) già definito nell'account di integrazione.

## <a name="encode-as2-messages"></a>Codificare i messaggi AS2

1. [Creare un'app per la logica](logic-apps-create-a-logic-app.md).

2. connettore di messaggi AS2 codificare Hello non dispone di trigger, pertanto è necessario aggiungere un trigger per avviare l'app di logica, ad esempio un trigger di richiesta. Nella finestra di progettazione logica App hello, aggiungere un trigger e quindi aggiungere un'app di logica di azione tooyour.

3.  Nella casella di ricerca hello, immettere "AS2" per il filtro. Selezionare **AS2 - Codifica in un messaggio AS2**.
   
    ![Cercare "AS2"](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. Se è stato creato in precedenza tutte le connessioni tooyour account di integrazione, viene chiesto toocreate ora tale connessione. Nome della connessione, quindi selezionare account di integrazione hello che si desidera tooconnect. 
   
    ![creare account di connessione toointegration](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    Le proprietà con l'asterisco sono obbligatorie.

    | Proprietà | Dettagli |
    | --- | --- |
    | Nome connessione * |Immettere un nome per la connessione. |
    | Account di integrazione * |Immettere un nome per l'account di integrazione. Assicurarsi che l'app di account e la logica di integrazione siano hello nello stesso percorso di Azure. |

5.  Al termine, i dettagli relativi alla connessione dovrebbero essere simile toothis esempio. toofinish della creazione della connessione, scegliere **crea**.
   
    ![Dettagli della connessione di integrazione](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. Dopo aver creata la connessione, come illustrato in questo esempio, fornire i dettagli per **AS2-da**, **AS2 tooidentifiers** come configurato nel contratto, e **corpo**, ovvero payload del messaggio Hello.
   
    ![specificare i campi obbligatori](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a>Dettagli codificatore AS2

connettore di codifica AS2 Hello esegue queste attività: 

* Elabora le intestazioni AS2/HTTP
* Firma i messaggi in uscita (se configurata)
* Crittografa i messaggi in uscita (se configurata)
* Comprime il messaggio hello (se configurata)

## <a name="try-this-sample"></a>Provare questo esempio

tootry la distribuzione di uno scenario di AS2 app ed esempio logica completamente operativo, vedere hello [AS2 scenario e il modello di applicazione logica](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).

## <a name="view-hello-swagger"></a>Swagger hello vista
Vedere hello [swagger dettagli](/connectors/as2/). 

## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni su Enterprise Integration Pack hello](logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack") 

