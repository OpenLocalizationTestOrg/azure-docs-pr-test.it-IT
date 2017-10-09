---
title: i messaggi per l'integrazione di enterprise B2B - App Azure per la logica aaaAS2 | Documenti Microsoft
description: Scambiare messaggi AS2 per l'integrazione aziendale B2B con App per la logica di Azure
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c9b7e1a9-4791-474c-855f-988bd7bf4b7f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 23f9d74dd0ad807e9cdaedb320d60496cfef9bc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-as2-messages-for-enterprise-integration-with-logic-apps"></a>Scambiare messaggi AS2 per l'integrazione aziendale con le app per la logica di Azure

Per poter scambiare messaggi AS2 con App per la logica di Azure, è necessario creare un contratto AS2 e archiviarlo nell'account di integrazione. Ecco i passaggi hello sull'accordo toocreate un AS2.

## <a name="before-you-start"></a>Prima di iniziare

Ecco gli elementi di hello che è necessario:

* Un [account di integrazione](../logic-apps/logic-apps-enterprise-integration-accounts.md) già definito e associato alla sottoscrizione di Azure.
* Almeno due [partner](logic-apps-enterprise-integration-partners.md) che sono già definite nell'account di integrazione e configurate con qualificatore hello AS2 in **identità di Business**

> [!NOTE]
> Quando si crea un contratto, il contenuto di hello nel file di contratto hello deve corrispondere il tipo di contratto hello.    

Dopo aver [creato un account di integrazione](../logic-apps/logic-apps-enterprise-integration-accounts.md) e [aggiunto i partner](logic-apps-enterprise-integration-partners.md), è possibile creare un contratto AS2 attenendosi alla procedura seguente.

## <a name="create-an-as2-agreement"></a>Creare un contratto AS2

1.  Accedi toohello [portale di Azure](http://portal.azure.com "portale di Azure").  

2.  Scegliere dal menu a sinistra hello **più servizi**. Nella casella di ricerca hello, immettere **integrazione** come filtro. Selezionare dall'elenco risultati hello **account di integrazione**.

    > [!TIP]
    > Se non viene visualizzato **più servizi**, è necessario innanzitutto menu hello tooexpand. Nella parte superiore di hello del menu hello compresso, selezionare **menu Mostra**.

    ![Altri servizi, filtro su "integrazione", selezionare "Account di integrazione"](./media/logic-apps-enterprise-integration-agreements/overview-1.png)

3. In hello **account di integrazione** blade che viene aperta, l'account di integrazione hello select in cui si desidera contratto hello toocreate.
Se non viene visualizzato alcun account di integrazione, [crearne prima uno](../logic-apps/logic-apps-enterprise-integration-accounts.md "Tutte le informazioni sugli account di integrazione").  

    ![Selezionare account di integrazione hello in toocreate hello contratto](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Scegliere hello **contratti** riquadro. Se non si dispone di un riquadro contratti, è innanzitutto necessario aggiungere il riquadro hello.

    ![Selezionare il riquadro "Contratti"](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. Nel pannello contratti hello visualizzato, scegliere **Aggiungi**.

    ![Selezionare "Aggiungi"](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)

6. In **Aggiungi**, digitare un **nome** per il contratto. In **Tipo di contratto**selezionare **AS2**. Seleziona hello **Partner Host**, **identità Host**, **Partner Guest**, e **identità Guest** per il contratto.

    ![Fornire i dettagli relativi al contratto](./media/logic-apps-enterprise-integration-agreements/agreement-3.png)  

    | Proprietà | Descrizione |
    | --- | --- |
    | Nome |Nome del contratto hello |
    | Tipo di contratto | Deve essere AS2 |
    | Host Partner (Partner host) |Un contratto prevede un partner host e un partner guest. partner host Hello rappresenta organizzazione hello che configura l'accordo hello. |
    | Host Identity (Identità host) |Un identificatore per il partner host hello |
    | Guest Partner (Partner guest) |Un contratto prevede un partner host e un partner guest. partner guest Hello rappresenta organizzazione hello usato per esegue attività con partner host hello. |
    | identità guest |Un identificatore per il partner guest hello |
    | Receive Settings (Impostazioni di ricezione) |Queste proprietà si applicano tooall ricevuti da un contratto. |
    | Send Settings (Impostazioni di invio) |Queste proprietà si applicano tooall i messaggi inviati da un contratto. |

## <a name="configure-how-your-agreement-handles-received-messages"></a>Configurare il modo in cui il contratto riceve i messaggi

Ora che sono state impostate proprietà di contratto hello, è possibile configurare come contratto identifica e gestisce i messaggi in ingresso ricevuti dal partner mediante il presente contratto.

1.  In **Aggiungi**, selezionare **Impostazioni di ricezione**.
Configurare queste proprietà in base al contratto con partner hello che scambia messaggi con l'utente. Per le relative proprietà, vedere la tabella hello in questa sezione.

    ![Configurare "Impostazioni di ricezione"](./media/logic-apps-enterprise-integration-agreements/agreement-4.png)

2. Facoltativamente, è possibile eseguire l'override di proprietà hello dei messaggi in ingresso selezionando **Ignora proprietà del messaggio**.

3. toorequire tutti toobe messaggi in ingresso firmato, selezionare **messaggio deve essere firmato**. Da hello **certificato** selezionare esistente [certificato pubblico partner guest](../logic-apps/logic-apps-enterprise-integration-certificates.md) per la convalida della firma hello nei messaggi hello. Oppure creare il certificato di hello, se non si dispone di uno.

4.  Selezionare tutti toobe messaggi in ingresso crittografati, toorequire **messaggio deve essere crittografato**. Da hello **certificato** selezionare esistente [certificato privato partner host](../logic-apps/logic-apps-enterprise-integration-certificates.md) per la decrittografia dei messaggi in arrivo. Oppure creare il certificato di hello, se non si dispone di uno.

5. Selezionare toorequire messaggi toobe compresso, **messaggio deve essere compresso**.

6. Selezionare una notifica di messaggio sincrono disposizione (MDN) per i messaggi ricevuti, toosend **invia MDN**.

7. toosend firma MDN per i messaggi ricevuti, selezionare **invia MDN firmato**.

8. Selezionare MSN asincroni per i messaggi ricevuti, toosend **invio di MDN asincroni**.

9. Al termine, assicurarsi che toosave le impostazioni scegliendo **OK**.

A questo punto il contratto toohandle pronto in ingresso le impostazioni di messaggi conformi tooyour selezionate.

| Proprietà | Descrizione |
| --- | --- |
| Override message properties |Indica che è possibile eseguire l'override delle proprietà nei messaggi ricevuti. |
| Il messaggio deve essere firmato |Richiede toobe messaggi firmati. Configurare hello certificato pubblico partner guest per la verifica della firma.  |
| Il messaggio deve essere crittografato |Richiede toobe messaggi crittografati. I messaggi non crittografati vengono rifiutati. Configurare hello host partner certificato privato per la decrittografia dei messaggi hello.  |
| Il messaggio deve essere compresso |Richiede toobe messaggi compressi. I messaggi non compressi vengono rifiutati. |
| Testo MDN |Hello predefinito disposition notifica (MDN) toobe toohello inviato messaggio mittente del messaggio. |
| Send MDN (Invia MDN) |Richiede toobe MDN inviato. |
| Send signed MDN (Invia MDN firmato) |Richiede toobe MDN firmato. |
| MIC Algorithm (Algoritmo MIC) |Selezionare hello algoritmo toouse per firmare i messaggi. |
| Send asynchronous MDN (Invia MDN asincrono) | Richiede toobe i messaggi inviati in modo asincrono. |
| URL | Specificare l'URL di hello in toosend hello MDN. |

## <a name="configure-how-your-agreement-sends-messages"></a>Configurare il modo in cui il contratto invia messaggi

È possibile configurare come contratto identifica e gestisce i messaggi in uscita inviati partner tooyour mediante il presente contratto.

1.  In **Aggiungi**, selezionare **Impostazioni di avvio**.
Configurare queste proprietà in base al contratto con partner hello che scambia messaggi con l'utente. Per le relative proprietà, vedere la tabella hello in questa sezione.

    ![Impostare le proprietà di "Impostazioni di invio" hello](./media/logic-apps-enterprise-integration-agreements/agreement-51.png)

2. toosend messaggi firmati tooyour partner, selezionare **Abilita firma messaggi**. Per firmare i messaggi hello, in hello **algoritmo MIC** elenco, seleziona hello *certificato privato partner host algoritmo MIC*. E in hello **certificato** selezionare esistente [certificato privato partner host](../logic-apps/logic-apps-enterprise-integration-certificates.md).

3. toosend messaggi crittografati toohello partner, selezionare **abilitare la crittografia dei messaggi**. Per crittografare i messaggi hello, in hello **algoritmo di crittografia** elenco, seleziona hello *algoritmo del certificato pubblico partner guest*.
E in hello **certificato** selezionare esistente [certificato pubblico partner guest](../logic-apps/logic-apps-enterprise-integration-certificates.md).

4. messaggio hello toocompress, seleziona **Abilita compressione messaggi**.

5. intestazione content-type HTTP hello di toounfold in una singola riga, seleziona **Espandi intestazioni HTTP**.

6. tooreceive MDN sincroni per hello inviati i messaggi, selezionare **Richiedi MDN**.

7. tooreceive firma MDN per i messaggi hello inviato, selezionare **Richiedi MDN firmato**.

8. tooreceive MSN asincroni per hello inviati i messaggi, selezionare **Richiedi MDN asincrono**. Se si seleziona questa opzione, immettere l'URL di hello per dove toosend hello MDN.

9. toorequire non ripudio della ricezione, selezionare **Abilita NRR**.  

10. Selezionare toospecify algoritmo formato toouse in hello MIC o l'accesso in uscita di intestazioni del messaggio AS2 o MDN, hello **formato di algoritmo SHA2**.  

11. Al termine, assicurarsi che toosave le impostazioni scegliendo **OK**.

Il contratto è ora pronto toohandle messaggi conformi a impostazioni tooyour selezionata in uscita.

| Proprietà | Descrizione |
| --- | --- |
| Enable message signing (Abilita la firma dei messaggi) |Richiede tutti i messaggi inviati da hello contratto toobe firmato. |
| MIC Algorithm (Algoritmo MIC) |Hello toouse algoritmo per la firma dei messaggi. Configura certificato privato di partner host hello algoritmo MIC per firmare i messaggi hello. |
| Certificate |Selezionare hello toouse di certificato per firmare i messaggi. Configura certificato privato hello host partner per firmare i messaggi hello. |
| Enable message encryption (Abilita la crittografia dei messaggi) |Richiede la crittografia di tutti i messaggi inviati da questo contratto. Configura l'algoritmo del certificato pubblico partner guest hello per crittografare i messaggi hello. |
| Algoritmo di crittografia |Hello toouse algoritmo di crittografia per la crittografia dei messaggi. Configura certificato pubblico partner guest di hello per crittografare i messaggi hello. |
| Certificate |messaggi Hello certificato toouse tooencrypt. Configura certificato privato hello guest partner per la crittografia dei messaggi hello. |
| Abilita compressione messaggio |Richiede la compressione di tutti i messaggi inviati da questo contratto. |
| Espandi intestazioni HTTP |Inserisce l'intestazione content-type HTTP di hello in una singola riga. |
| Richiedi MDN |Richiede un MDN per tutti i messaggi inviati da questo contratto. |
| Richiedi MDN firmato |Richiede che tutti i messaggi MDN inviati contratto toothis toobe firmato. |
| Richiedi MDN asincrono |Richiede l'accordo di toothis toobe inviati MDN asincrono. |
| URL |Specificare l'URL di hello in toosend hello MDN. |
| Enable NRR (Attiva NRR) |Richiede di non ripudio della ricezione (NRR), un attributo di comunicazione che fornisce una prova dati hello è stato ricevuto come risolti. |
| Formato di algoritmo SHA2 |Selezionare toouse formato algoritmo MIC hello o l'accesso hello intestazioni del messaggio AS2 o MDN in uscita |

## <a name="find-your-created-agreement"></a>Individuare il contratto creato

1.  Al termine dell'impostazione di tutte le proprietà dell'accordo, in hello **Aggiungi** pannello, scegliere **OK** toofinish la creazione di contratto e il pannello di account di integrazione tooyour restituito.

    Il contratto appena aggiunto viene visualizzato nell'elenco **Contratti**.

2.  È anche possibile visualizzare i contratti nella panoramica dell'account di Integrazione. Scegliere il pannello di account di integrazione, **Panoramica**, quindi selezionare hello **contratti** riquadro. 

    ![Scegliere tooview riquadro "Accordi di" tutti i contratti](./media/logic-apps-enterprise-integration-agreements/agreement-6.png)

## <a name="view-hello-swagger"></a>Swagger hello vista
Vedere hello [swagger dettagli](/connectors/as2/). 

## <a name="next-steps"></a>Passaggi successivi
* [Altre informazioni su Enterprise Integration Pack hello](logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack")  
