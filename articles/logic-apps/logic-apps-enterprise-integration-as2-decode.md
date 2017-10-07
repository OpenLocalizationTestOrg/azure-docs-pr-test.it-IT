---
title: i messaggi AS2 aaaDecode - App Azure per la logica | Documenti Microsoft
description: Come toouse hello decodificatore AS2 nella hello Enterprise Integration Pack per le app di logica di Azure
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
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Decodificare i messaggi AS2 per le app di Azure logica con hello Enterprise Integration Pack 

tooestablish protezione e affidabilità durante la trasmissione di messaggi, utilizzare connettore di messaggi hello decodifica AS2. Questo connettore offre funzionalità di firma digitale, decrittografia e riconoscimenti tramite notifiche sulla ricezione di messaggi.

## <a name="before-you-start"></a>Prima di iniziare

Ecco gli elementi di hello che è necessario:

* Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)
* Un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md) già definito e associato alla sottoscrizione di Azure. È necessario disporre di un connettore di messaggio integrazione account toouse hello decodifica AS2.
* Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.
* Un [contratto AS2](logic-apps-enterprise-integration-as2.md) già definito nell'account di integrazione.

## <a name="decode-as2-messages"></a>Decodificare i messaggi AS2

1. [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).

2. connettore di messaggi Hello decodifica AS2 non dispone di trigger, pertanto è necessario aggiungere un trigger per avviare l'app di logica, ad esempio un trigger di richiesta. Nella finestra di progettazione logica App hello, aggiungere un trigger e quindi aggiungere un'app di logica di azione tooyour.

3.  Nella casella di ricerca hello, immettere "AS2" per il filtro. Selezionare **AS2 - Decodifica il messaggio AS2**.
   
    ![Cercare "AS2"](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. Se è stato creato in precedenza tutte le connessioni tooyour account di integrazione, viene chiesto toocreate ora tale connessione. Nome della connessione, quindi selezionare account di integrazione hello che si desidera tooconnect.
   
    ![Create una connessione di integrazione](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    Le proprietà con l'asterisco sono obbligatorie.

    | Proprietà | Dettagli |
    | --- | --- |
    | Nome connessione * |Immettere un nome per la connessione. |
    | Account di integrazione * |Immettere un nome per l'account di integrazione. Assicurarsi che l'app di account e la logica di integrazione siano hello nello stesso percorso di Azure. |

5.  Al termine, i dettagli relativi alla connessione dovrebbero essere simile toothis esempio. toofinish della creazione della connessione, scegliere **crea**.

    ![Dettagli della connessione di integrazione](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. Dopo aver creata la connessione, come illustrato in questo esempio, selezionare **corpo** e **intestazioni** hello richiedere output.
   
    ![connessione di integrazione creata](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    ad esempio:

    ![Selezionare Corpo e Intestazioni dagli output della richiesta](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a>Dettagli del decodificatore AS2

connettore di decodifica AS2 Hello esegue queste attività: 

* Elabora le intestazioni AS2/HTTP
* Verifica firma hello (se configurata)
* Consente di decrittografare i messaggi hello (se configurata)
* Decomprime il messaggio hello (se configurata)
* Riconcilia un MDN ricevuto con un messaggio in uscita originale hello
* Aggiorna e correla i record nel database di non ripudio hello
* Scrive i record per la creazione di report di stato su AS2
* il contenuto del payload di output hello è con codificata base64
* Determina se un messaggio MDN è obbligatorio, se hello MDN deve essere sincrona o asincrona in base alla configurazione nell'accordo AS2
* Genera una notifica sulla ricezione del messaggio sincrona o asincrona, in base alle configurazioni nel contratto
* Imposta proprietà e i token di correlazione hello in hello MDN

## <a name="try-this-sample"></a>Provare questo esempio

tootry la distribuzione di uno scenario di AS2 app ed esempio logica completamente operativo, vedere hello [AS2 scenario e il modello di applicazione logica](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).

## <a name="view-hello-swagger"></a>Swagger hello vista
Vedere hello [swagger dettagli](/connectors/as2/). 

## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni su hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md) 

