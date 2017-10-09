---
title: i messaggi EDIFACT aaaEncode - App Azure per la logica | Documenti Microsoft
description: Convalida EDI e generare codice XML con il codificatore di messaggi EDIFACT in hello Enterprise Integration Pack per le app di logica di Azure
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: b3799dbd2492adef597022d017cf28f5ceb1085c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Codificare i messaggi EDIFACT per le app di Azure logica con hello Enterprise Integration Pack

Con connettore di messaggi hello codifica EDIFACT, è possibile convalidare EDI e proprietà specifiche del partner, generare un documento XML per ogni set di transazioni e richiedere un riconoscimento tecnico, il riconoscimento funzionale o entrambi.
toouse questo connettore, è necessario aggiungere hello connettore tooan trigger nell'app logica esistente.

## <a name="before-you-start"></a>Prima di iniziare

Ecco gli elementi di hello che è necessario:

* Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)
* Un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md) già definito e associato alla sottoscrizione di Azure. È necessario disporre di un connettore di messaggio integrazione account toouse hello codifica EDIFACT. 
* Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.
* Un [contratto EDIFACT](logic-apps-enterprise-integration-edifact.md) già definito nell'account di integrazione.

## <a name="encode-edifact-messages"></a>Codificare messaggi EDIFACT

1. [Creare un'app per la logica](logic-apps-create-a-logic-app.md).

2. connettore di messaggi Hello codifica EDIFACT non dispone di trigger, pertanto è necessario aggiungere un trigger per avviare l'app di logica, ad esempio un trigger di richiesta. Nella finestra di progettazione logica App hello, aggiungere un trigger e quindi aggiungere un'app di logica di azione tooyour.

3.  Nella casella di ricerca hello, immettere "EDIFACT" come filtro. Selezionare l'opzione **codificare messaggio EDIFACT in base al nome di contratto** o **Encode tooEDIFACT messaggio dalle identità**.
   
    ![ricerca di EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. Se è stato creato in precedenza tutte le connessioni tooyour account di integrazione, viene chiesto toocreate ora tale connessione. Nome della connessione, quindi selezionare account di integrazione hello che si desidera tooconnect.

    ![creare connessione all'account di integrazione](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    Le proprietà con l'asterisco sono obbligatorie.

    | Proprietà | Dettagli |
    | --- | --- |
    | Nome connessione * |Immettere un nome per la connessione. |
    | Account di integrazione * |Immettere un nome per l'account di integrazione. Assicurarsi che l'app di account e la logica di integrazione siano hello nello stesso percorso di Azure. |

5.  Al termine, i dettagli relativi alla connessione dovrebbero essere simile toothis esempio. toofinish della creazione della connessione, scegliere **crea**.

    ![dettagli della connessione all'account di integrazione](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    La connessione è stata creata.

    ![connessione all'account di integrazione creata](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a>Encode EDIFACT Message by agreement name

Se si sceglie tooencode messaggi EDIFACT in base al nome di contratto, aprire hello **contratto nome di EDIFACT** elenco, immettere o selezionare il nome del contratto EDIFACT. Immettere tooencode di messaggio hello XML.

![Immettere il nome di contratto EDIFACT e tooencode messaggio XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a>Encode EDIFACT Message by identities

Se si sceglie tooencode messaggi EDIFACT per le identità, immettere l'identificatore hello del mittente, qualificatore mittente, identificatore del ricevitore e qualificatore ricevitore come configurato nel contratto EDIFACT. Selezionare tooencode di messaggio hello XML.

![Fornire le identità per il mittente e destinatario, selezionare tooencode messaggio XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a>Dettagli della codifica EDIFACT

connettore di codifica EDIFACT Hello esegue queste attività: 

* Risoluzione hello accordo mediante corrispondenza hello qualificatore e identificatore e qualificatore ricevitore e identificatore mittente
* Serializza l'interscambio EDI hello, conversione dei messaggi con codifica XML in set di transazioni EDI nell'interscambio hello.
* Si applica ai segmenti di intestazione e finali del set di transazioni.
* Genera un numero di controllo di interscambio, un numero di controllo di gruppo e un numero di controllo del set di transazioni per ogni interscambio in uscita.
* Sostituisce i separatori nei dati di payload hello
* Convalida le proprietà EDI e specifiche del partner.
  * Convalida dello schema di elementi di dati di set di transazioni hello rispetto allo schema di messaggio hello.
  * Convalida EDI eseguita sugli elementi dati del set di transazioni.
  * Convalida estesa eseguita sugli elementi dati del set di transazioni.
* Genera un documento XML per ogni set di transazioni.
* Richiede un riconoscimento tecnico e/o funzionale (se configurata).
  * Riconoscimento tecnico, il messaggio CONTRL hello indica ricezione di un interscambio.
  * Come un riconoscimento funzionale, il messaggio CONTRL hello indica l'accettazione o rifiuto dell'interscambio ricevuto hello, gruppo o messaggio, con un elenco di errori o funzionalità non supportate

## <a name="view-swagger-file"></a>Visualizzare il file Swagger
vedere i dettagli di Swagger hello tooview per connettore EDIFACT hello, [EDIFACT](/connectors/edifact/).

## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni su Enterprise Integration Pack hello](logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack") 

