---
title: i messaggi X12 aaaEncode - App Azure per la logica | Documenti Microsoft
description: Convalida EDI e convertire codificata in formato XML con X12 di messaggio del codificatore in hello Enterprise Integration Pack per le app di logica di Azure
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>La codifica X12 i messaggi per le app di Azure logica con hello Enterprise Integration Pack

Con connettore di messaggi hello codifica X12, è possibile convalidare EDI e proprietà specifiche del partner, convertire i messaggi con codifica XML in set di transazioni EDI nell'interscambio hello e richiedere un riconoscimento tecnico, il riconoscimento funzionale o entrambi.
toouse questo connettore, è necessario aggiungere hello connettore tooan trigger nell'app logica esistente.

## <a name="before-you-start"></a>Prima di iniziare

Ecco gli elementi di hello che è necessario:

* Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)
* Un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md) già definito e associato alla sottoscrizione di Azure. È necessario disporre di un connettore di messaggio integrazione account toouse hello codifica X12.
* Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.
* Un [contratto X12](logic-apps-enterprise-integration-x12.md) già definito nell'account di integrazione.

## <a name="encode-x12-messages"></a>Messaggi Encode X12

1. [Creare un'app per la logica](logic-apps-create-a-logic-app.md).

2. connettore di messaggi Hello codifica X12 non dispone di trigger, pertanto è necessario aggiungere un trigger per avviare l'app di logica, ad esempio un trigger di richiesta. Nella finestra di progettazione logica App hello, aggiungere un trigger e quindi aggiungere un'app di logica di azione tooyour.

3.  Nella casella di ricerca hello, immettere "x12" per il filtro. Selezionare l'opzione **X12-codificare tooX12 messaggio in base al nome di contratto** o **X12-codificare il messaggio tooX12 dalle identità**.
   
    ![Cercare "X12"](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. Se è stato creato in precedenza tutte le connessioni tooyour account di integrazione, viene chiesto toocreate ora tale connessione. Nome della connessione, quindi selezionare account di integrazione hello che si desidera tooconnect. 
   
    ![connessione all'account di integrazione](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    Le proprietà con l'asterisco sono obbligatorie.

    | Proprietà | Dettagli |
    | --- | --- |
    | Nome connessione * |Immettere un nome per la connessione. |
    | Account di integrazione * |Immettere un nome per l'account di integrazione. Assicurarsi che l'app di account e la logica di integrazione siano hello nello stesso percorso di Azure. |

5.  Al termine, i dettagli relativi alla connessione dovrebbero essere simile toothis esempio. toofinish della creazione della connessione, scegliere **crea**.

    ![connessione all'account di integrazione creata](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    La connessione è stata creata.

    ![dettagli della connessione all'account di integrazione](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a>Encode X12 Message by agreement name (Messaggio Encode X12 per nome contratto)

Se si sceglie tooencode X12 messaggi in base al nome di contratto, aprire hello **nome X12 contratto** elenco, immettere o selezionare il X12 esistente contratto. Immettere tooencode di messaggio hello XML.

![Immettere X12 tooencode dei messaggi XML e nome contratto](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a>Encode X12 Message by identities (Messaggio Encode X12 per identità)

Se si sceglie tooencode X12 messaggi dalle identità, immettere l'identificatore hello del mittente, qualificatore mittente, identificatore del ricevitore e qualificatore ricevitore come configurato nel X12 contratto. Selezionare tooencode di messaggio hello XML.
   
![Fornire le identità per il mittente e destinatario, selezionare tooencode messaggio XML](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a>Dettagli di Encode X12

connettore di codifica X12 Hello esegue queste attività:

* Risoluzione del contratto associando le proprietà del contesto di mittente e del destinatario.
* Serializza l'interscambio EDI hello, conversione dei messaggi con codifica XML in set di transazioni EDI nell'interscambio hello.
* Si applica ai segmenti di intestazione e finali del set di transazioni.
* Genera un numero di controllo di interscambio, un numero di controllo di gruppo e un numero di controllo del set di transazioni per ogni interscambio in uscita.
* Sostituisce i separatori nei dati di payload hello
* Convalida le proprietà EDI e specifiche del partner.
  * Convalida dello schema di elementi di dati di set di transazioni hello rispetto al messaggio hello dello Schema
  * Convalida EDI eseguita sugli elementi dati del set di transazioni.
  * Convalida estesa eseguita sugli elementi dati del set di transazioni.
* Richiede un riconoscimento tecnico e/o funzionale (se configurata).
  * Un riconoscimento tecnico viene generato in seguito alla convalida dell'intestazione. Hello riconoscimento tecnico segnala hello lo stato di elaborazione hello di un'intestazione di interscambio e trailer da ricevitore dell'indirizzo hello
  * Un riconoscimento funzionale viene generato in seguito alla convalida del corpo. riconoscimento funzionale Hello segnala ogni errore rilevato durante l'elaborazione di hello ricevuto documento

## <a name="view-hello-swagger"></a>Swagger hello vista
Vedere hello [swagger dettagli](/connectors/x12/). 

## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni su Enterprise Integration Pack hello](logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack") 

