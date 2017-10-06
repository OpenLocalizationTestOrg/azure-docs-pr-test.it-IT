---
title: i messaggi per l'integrazione di enterprise B2B - App Azure per la logica aaaEDIFACT | Documenti Microsoft
description: Scambiare messaggi EDIFACT in formato EDI per l'integrazione aziendale B2B con App per la logica di Azure
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 2257d2c8-1929-4390-b22c-f96ca8b291bc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/26/2016
ms.author: LADocs; jonfan
ms.openlocfilehash: 496fadcda58de2d36459202b839b0a63c9e5857c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-edifact-messages-for-enterprise-integration-with-logic-apps"></a>Scambiare messaggi EDIFACT per l'integrazione Enterprise con le app per la logica

Per poter scambiare messaggi EDIFACT con App per la logica di Azure, è necessario creare un contratto EDIFACT e archiviarlo nell'account di integrazione. Ecco la procedura relativa hello toocreate un accordo EDIFACT.

> [!NOTE]
> Questa pagina vengono illustrate le funzionalità EDIFACT di hello per le app di logica di Azure. Per altre informazioni, vedere [X12](logic-apps-enterprise-integration-x12.md).

## <a name="before-you-start"></a>Prima di iniziare

Ecco gli elementi di hello che è necessario:

* Un [account di integrazione](../logic-apps/logic-apps-enterprise-integration-accounts.md) già definito e associato alla sottoscrizione di Azure.  
* Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.

> [!NOTE]
> Quando si crea un contratto, il contenuto di hello nei messaggi hello ricevuti o inviati tooand dal partner hello deve corrispondere il tipo di contratto hello.

Dopo aver [creato un account di integrazione](../logic-apps/logic-apps-enterprise-integration-accounts.md) e [aggiunto i partner](logic-apps-enterprise-integration-partners.md), è possibile creare un contratto EDIFACT attenendosi alla procedura seguente.

## <a name="create-an-edifact-agreement"></a>Creare un contratto EDIFACT 

1.  Accedi toohello [portale di Azure](http://portal.azure.com "portale di Azure"). Scegliere dal menu a sinistra hello **più servizi**.

    > [!TIP]
    > Se non viene visualizzato **più servizi**, è necessario innanzitutto menu hello tooexpand. Nella parte superiore di hello del menu hello compresso, selezionare **menu Mostra**.

    ![Fare clic su "Altri servizi" nel menu a sinistra](./media/logic-apps-enterprise-integration-edifact/edifact-0.png)

2. Nella casella di ricerca hello, digitare "integrazione" per il filtro. Selezionare dall'elenco risultati hello **account di integrazione**.

    ![Filtro su "integrazione", selezionare "Account di integrazione"](./media/logic-apps-enterprise-integration-edifact/edifact-1-3.png)

3. In hello **account di integrazione** blade che viene aperta, l'account di integrazione hello select in cui si desidera contratto hello toocreate.
Se non viene visualizzato alcun account di integrazione, [crearne prima uno](../logic-apps/logic-apps-enterprise-integration-accounts.md "Tutte le informazioni sugli account di integrazione").  

    ![Selezionare account di integrazione in toocreate hello contratto](./media/logic-apps-enterprise-integration-edifact/edifact-1-4.png)

4. Scegliere hello **contratti** riquadro. Se non si dispone di un riquadro contratti, è innanzitutto necessario aggiungere il riquadro hello.   

    ![Selezionare il riquadro "Contratti"](./media/logic-apps-enterprise-integration-edifact/edifact-1-5.png)

5. Nel pannello contratti hello visualizzato, scegliere **Aggiungi**.

    ![Selezionare "Aggiungi"](./media/logic-apps-enterprise-integration-edifact/edifact-agreement-2.png)

6. In **Aggiungi**, digitare un **nome** per il contratto. In **Tipo di contratto**selezionare **EDIFACT**. Seleziona hello **Partner Host**, **identità Host**, **Partner Guest**, e **identità Guest** per il contratto.

    ![Fornire i dettagli relativi al contratto](./media/logic-apps-enterprise-integration-edifact/edifact-1.png)

    | Proprietà | Descrizione |
    | --- | --- |
    | Nome |Nome del contratto hello |
    | Tipo di contratto | Deve essere EDIFACT |
    | Host Partner (Partner host) |Un contratto prevede un partner host e un partner guest. partner host Hello rappresenta organizzazione hello che configura l'accordo hello. |
    | Host Identity (Identità host) |Un identificatore per il partner host hello |
    | Guest Partner (Partner guest) |Un contratto prevede un partner host e un partner guest. partner guest Hello rappresenta organizzazione hello usato per esegue attività con partner host hello. |
    | identità guest |Un identificatore per il partner guest hello |
    | Receive Settings (Impostazioni di ricezione) |Queste proprietà si applicano tooall ricevuti da un contratto. |
    | Send Settings (Impostazioni di invio) |Queste proprietà si applicano tooall i messaggi inviati da un contratto. |

## <a name="configure-how-your-agreement-handles-received-messages"></a>Configurare il modo in cui il contratto riceve i messaggi

Ora che sono state impostate proprietà di contratto hello, è possibile configurare come contratto identifica e gestisce i messaggi in ingresso ricevuti dal partner mediante il presente contratto.

1.  In **Aggiungi**, selezionare **Impostazioni di ricezione**.
Configurare queste proprietà in base al contratto con partner hello che scambia messaggi con l'utente. Per le relative proprietà, vedere le tabelle di hello in questa sezione.

    Il controllo **Impostazioni di ricezione** è suddiviso nelle sezioni seguenti: Identificatori, Riconoscimento, Schemi, Numeri di controllo, Convalide e Impostazioni interne.

    ![Configurare "Impostazioni di ricezione"](./media/logic-apps-enterprise-integration-edifact/edifact-2.png)  

2. Al termine, assicurarsi che toosave le impostazioni scegliendo **OK**.

A questo punto il contratto toohandle pronto in ingresso le impostazioni di messaggi conformi tooyour selezionate.

### <a name="identifiers"></a>Identificatori

| Proprietà | Descrizione |
| --- | --- |
| UNB6.1 (password di riferimento destinatario) |Immettere un valore alfanumerico costituito da un numero di caratteri compreso tra 1 e 14. |
| UNB6.2 (qualificatore di riferimento destinatario) |Immettere un valore alfanumerico costituito da almeno un carattere e al massimo due. |

### <a name="acknowledgments"></a>Ringraziamenti

| Proprietà | Descrizione |
| --- | --- |
| Conferma recapito messaggi (CONTRL) |Selezionare questo tooreturn casella di controllo, un tecnico mittente dell'interscambio toohello riconoscimento (CONTRL). riconoscimento Hello viene inviato il mittente di interscambio toohello in base alle hello impostazioni di invio per il contratto di hello. |
| Acknowledgement (CONTRL) |Selezionare questa casella di controllo tooreturn che toohello mittente dell'interscambio in base a hello impostazioni di invio per il contratto di hello viene inviato da un riconoscimento hello di mittente di funzionale (CONTRL) riconoscimento toohello interscambio. |

### <a name="schemas"></a>Schemi

| Proprietà | Descrizione |
| --- | --- |
| UNH2.1 (tipo) |Selezionare un tipo di set di transazioni. |
| UNH2.2 (versione) |Immettere il numero di versione messaggio hello. (da un minimo di un carattere a un massimo di tre). |
| UNH2.3 (versione) |Immettere il numero di rilascio messaggio hello. (da un minimo di un carattere a un massimo di tre). |
| UNH2.5 (codice assegnato associazione) |Immettere il codice hello assegnato. (deve contenere al massimo sei caratteri, che devono essere alfanumerici). |
| UNH2.1 (ID mittente APP) |Immettere un valore alfanumerico costituito da almeno un carattere e al massimo 35. |
| UNH2.2 (qualificatore codice mittente APP) |Immettere un valore alfanumerico con lunghezza massima di quattro caratteri. |
| Schema |Seleziona hello caricato in precedenza schema desiderato toouse dall'account di integrazione associato. |

### <a name="control-numbers"></a>Numeri di controllo
| Proprietà | Descrizione |
| --- | --- |
| Disallow Interchange Control Number duplicates (Non consentire duplicati di numeri di controllo interscambio) |gli interscambi duplicati tooblock, selezionare questa proprietà. Se selezionata, hello EDIFACT decodificare azione controlla che hello numero di controllo interscambio (UNB5) per l'interscambio ricevuto hello non corrisponde a un numero di controllo interscambio elaborati in precedenza. Se viene rilevata una corrispondenza, non viene elaborato interscambio hello. |
| Verifica UNB5 duplicati ogni (giorni) |Se si sceglie di numeri di controllo interscambio duplicato toodisallow, è possibile specificare il numero di hello di giorni quando hello tooperform controllo assegnando il valore appropriato hello per questa impostazione. |
| Disallow Group control number duplicates (Non consentire duplicati di numeri di controllo di gruppo) |Selezionare questa proprietà tooblock gli interscambi con numeri di controllo gruppo duplicati (UNG5). |
| Disallow Transaction set control number duplicates (Non consentire duplicati di numeri di controllo set di transazioni) |tooblock gli interscambi con set controllo numeri di transazioni duplicati (UNH1), selezionare questa proprietà. |
| Numero di controllo acknowledgement EDIFACT |i numeri di riferimento per l'utilizzo del set di transazioni di hello toodesignate in un riconoscimento, immettere un valore per il prefisso di hello, un intervallo di numeri di riferimento e un suffisso. |

### <a name="validations"></a>Convalide

Dopo aver completato ogni riga di convalida, ne viene aggiunta automaticamente un'altra. Se non si specifica alcuna regola, convalida Usa riga "Default" hello.

| Proprietà | Descrizione |
| --- | --- |
| Tipo messaggio |Selezionare il tipo di messaggio EDI hello. |
| EDI Validation (Convalida EDI) |Eseguire la convalida EDI sui tipi di dati definiti da schema hello EDI proprietà, le restrizioni di lunghezza, gli elementi dati vuoti e separatori finali. |
| Convalida estesa |Se non è di tipo di dati hello EDI, la convalida è sul requisito elemento dati di hello e ripetizione, enumerazioni e dati di convalida della lunghezza dell'elemento (min/max) è consentito. |
| Consenti zeri iniziali e finali |Tutti gli zero iniziali e finali e i caratteri di spazio vengono mantenuti e non vengono rimossi. |
| Rimuovi zero iniziali e finali |Tutti gli zero iniziali e finali e i caratteri di spazio vengono rimossi. |
| Criterio separatori finali |Consente di generare separatori finali. <p>Selezionare **non è consentito** tooprohibit i delimitatori finali e il separatore nel hello ricevuto l'interscambio. Se l'interscambio di hello presenta delimitatori e separatori finali, interscambio hello viene dichiarato non valido. <p>Selezionare **facoltativo** tooaccept gli interscambi con o senza delimitatori e separatori finali. <p>Selezionare **obbligatorio** quando necessario interscambio ricevuto hello delimitatori e separatori finali. |

### <a name="internal-settings"></a>Impostazioni interne

| Proprietà | Descrizione |
| --- | --- |
| Crea tag XML vuoti se sono consentiti separatori finali |Selezionare questo mittente di interscambio hello toohave casella di controllo includono vuoto tag XML per i separatori finali. |
| Suddividi interscambio in set di transazioni - Sospendi set di transazioni in caso di errore|Consente di analizzare ogni set di transazioni in un interscambio in un documento XML separato applicando i set di transazioni toohello hello busta appropriata. Sospendere solo hello set di transazioni che non superano la convalida. |
| Suddividi interscambio in set di transazioni - Sospendi interscambio in caso di errore|Consente di analizzare ogni set di transazioni in un interscambio in un documento XML separato applicando la busta appropriata hello. Sospendere l'intero interscambio hello quando uno o più set di transazioni nell'interscambio hello convalida ha esito negativo. | 
| Mantieni interscambio - Sospendi set transazioni in caso di errore |Lascia intatto l'interscambio hello, crea un documento XML per l'intero interscambio in batch hello. Sospendere solo hello set di transazioni che non superano la convalida, pur continuando tooprocess set di tutte le altre transazioni. |
| Mantieni interscambio - Sospendi interscambio in caso di errore |Lascia intatto l'interscambio hello, crea un documento XML per l'intero interscambio in batch hello. Sospendere l'intero interscambio hello quando uno o più set di transazioni nell'interscambio hello convalida ha esito negativo. |

## <a name="configure-how-your-agreement-sends-messages"></a>Configurare il modo in cui il contratto invia messaggi

È possibile configurare come contratto identifica e gestisce i messaggi in uscita inviati partner tooyour mediante il presente contratto.

1.  In **Aggiungi**, selezionare **Impostazioni di avvio**.
Configurare queste proprietà in base al contratto con il partner con cui si scambiano i messaggi. Per le relative proprietà, vedere le tabelle di hello in questa sezione.

    Il controllo **Impostazioni di invio** è suddiviso nelle sezioni seguenti: Identificatori, Riconoscimento, Schemi, Buste, Set di caratteri e separatori, Numeri di controllo e Convalida.

    ![Configurare "Impostazioni di invio"](./media/logic-apps-enterprise-integration-edifact/edifact-3.png)    

2. Al termine, assicurarsi che toosave le impostazioni scegliendo **OK**.

Il contratto è ora pronto toohandle messaggi conformi a impostazioni tooyour selezionata in uscita.

### <a name="identifiers"></a>Identificatori

| Proprietà | Descrizione |
| --- | --- |
| UNB1.2 (versione sintassi) |Selezionare un valore compreso tra **1** e **4**. |
| UNB2.3 (indirizzo di routing inverso mittente) |Immettere un valore alfanumerico costituito da almeno un carattere e al massimo 14. |
| UNB3.3 (indirizzo di routing inverso destinatario) |Immettere un valore alfanumerico costituito da almeno un carattere e al massimo 14. |
| UNB6.1 (password di riferimento destinatario) |Immettere un valore alfanumerico costituito da almeno un carattere e al massimo 14. |
| UNB6.2 (qualificatore di riferimento destinatario) |Immettere un valore alfanumerico costituito da almeno un carattere e al massimo due. |
| UNB7 (ID riferimento applicazione) |Immettere un valore alfanumerico costituito da almeno un carattere e al massimo 14. |

### <a name="acknowledgment"></a>Acknowledgment (Riconoscimento)
| Proprietà | Descrizione |
| --- | --- |
| Conferma recapito messaggi (CONTRL) |Selezionare questa casella di controllo se il partner ospitato hello prevede tooreceive un riconoscimento tecnico (CONTRL). Questa impostazione specifica di tale partner ospitato hello, che invia il messaggio hello, richiede un acknowledgment dal partner guest hello. |
| Acknowledgement (CONTRL) |Selezionare questa casella di controllo se il partner ospitato hello prevede tooreceive un riconoscimento funzionale (CONTRL). Questa impostazione specifica di tale partner ospitato hello, che invia il messaggio hello, richiede un acknowledgment dal partner guest hello. |
| Genera il ciclo SG1/SG4 per i set di transazioni accettate |Se si sceglie toorequest un riconoscimento funzionale, selezionare la generazione di tooforce casella di controllo di cicli SG1/SG4 in acknowledgment funzionali CONTRL per set transazioni accettati. |

### <a name="schemas"></a>Schemi
| Proprietà | Descrizione |
| --- | --- |
| UNH2.1 (tipo) |Selezionare un tipo di set di transazioni. |
| UNH2.2 (versione) |Immettere il numero di versione messaggio hello. |
| UNH2.3 (versione) |Immettere il numero di rilascio messaggio hello. |
| Schema |Selezionare toouse schema hello. Gli schemi si trovano nell'account di integrazione. tooaccess gli schemi, prima di collegare l'applicazione di integrazione account tooyour logica. |

### <a name="envelopes"></a>Buste
| Proprietà | Descrizione |
| --- | --- |
| UNB8 (codice di priorità elaborazione) |Immettere un valore alfabetico di lunghezza non superiore a un carattere. |
| UNB10 (contratto comunicazioni) |Immettere un valore alfanumerico costituito da almeno un carattere e al massimo 40. |
| UNB11 (indicatore test) |Selezionare questa casella di controllo tooindicate che hello interscambio generato dati di test |
| Applica segmento UNA (avviso stringa servizio) |Selezionare questo toogenerate casella di controllo, un segmento UNA per hello toobe di interscambio inviato. |
| Applica segmenti UNG (intestazione gruppo funzionale) |Selezionare questa casella di controllo toocreate raggruppamento dei segmenti nell'intestazione gruppo funzionale hello in partner guest toohello di hello i messaggi inviati. Hello sono i seguenti valori segmenti UNG di hello toocreate utilizzati: <p>Per **UNG1**, immettere un valore alfanumerico costituito da almeno un carattere e al massimo sei. <p>Per **UNG2.1**, immettere un valore alfanumerico costituito da almeno un carattere e al massimo 35. <p>Per **UNG2.2** immettere un valore alfanumerico con lunghezza massima di quattro caratteri. <p>Per **UNG3.1**, immettere un valore alfanumerico costituito da almeno un carattere e al massimo 35. <p>Per **UNG3.2** immettere un valore alfanumerico con lunghezza massima di quattro caratteri. <p>Per **UNG6** immettere un valore alfanumerico costituito da almeno un carattere e al massimo tre. <p>Per **UNG7.1** immettere un valore alfanumerico costituito da almeno un carattere e al massimo tre. <p>Per **UNG7.2** immettere un valore alfanumerico costituito da almeno un carattere e al massimo tre. <p>Per **UNG7.3** immettere un valore alfanumerico costituito da almeno 1 carattere e al massimo 6. <p>Per **UNG8**, immettere un valore alfanumerico costituito da almeno un carattere e al massimo 14. |

### <a name="character-sets-and-separators"></a>Character Sets and Separators (Set di caratteri e separatori)

Diverso da set di caratteri hello, è possibile immettere un diverso set di delimitatori toobe utilizzato per ogni tipo di messaggio. Se per un determinato schema del messaggio non è specificato un set di caratteri, viene utilizzato il set di caratteri predefinito hello.

| Proprietà | Descrizione |
| --- | --- |
| UNB1.1 (identificatore di sistema) |Seleziona hello di caratteri EDIFACT imposta toobe applicato su hello in uscita di interscambio. |
| Schema |Selezionare uno schema dall'elenco a discesa hello. Dopo aver completato ogni riga, viene aggiunta automaticamente una nuova riga. Per lo schema selezionato hello, separatori hello selezionare set che si desidera toouse, in base alle seguenti descrizioni separatore hello. |
| Tipo di input |Selezionare un tipo di input dall'elenco a discesa hello. |
| Component Separator |gli elementi dati compositi tooseparate, immettere un singolo carattere. |
| Data Element Separator |gli elementi dati semplici tooseparate negli elementi dati compositi, immettere un singolo carattere. |
| Segment Terminator |fine hello tooindicate di un segmento EDI, immettere un singolo carattere. |
| Suffisso |Selezionare carattere hello utilizzato con l'identificatore di segmento hello. Se si specifica un suffisso, hello elemento di dati carattere di terminazione segmento può essere vuoto. Se il carattere di terminazione di hello segmento viene lasciato vuoto, è necessario specificare un suffisso. |

### <a name="control-numbers"></a>Numeri di controllo
| Proprietà | Descrizione |
| --- | --- |
| UNB5 (numero di controllo interscambio) |Immettere un prefisso, un intervallo di valori per il numero di controllo interscambio hello e un suffisso. Questi valori vengono utilizzati toogenerate un interscambio in uscita. suffisso e prefisso hello sono facoltativi, mentre il numero di controllo hello è obbligatorio. numero di controllo Hello viene incrementato per ogni nuovo messaggio; prefisso Hello e il suffisso restano hello stesso. |
| UNG5 (numero di controllo gruppo) |Immettere un prefisso, un intervallo di valori per il numero di controllo interscambio hello e un suffisso. Questi valori vengono utilizzati numero di controllo gruppo toogenerate hello. suffisso e prefisso hello sono facoltativi, mentre il numero di controllo hello è obbligatorio. numero di controllo Hello viene incrementato per ogni nuovo messaggio finché non viene raggiunto il valore massimo hello; prefisso Hello e il suffisso restano hello stesso. |
| UNH1 (numero di riferimento intestazione messaggio) |Immettere un prefisso, un intervallo di valori per il numero di controllo interscambio hello e un suffisso. Questi valori vengono utilizzati numero di riferimento intestazione messaggio hello toogenerate. suffisso e prefisso hello sono facoltativi, mentre il numero di riferimento hello è obbligatorio. numero di riferimento Hello viene incrementato per ogni nuovo messaggio; prefisso Hello e il suffisso restano hello stesso. |

### <a name="validations"></a>Convalide

Dopo aver completato ogni riga di convalida, ne viene aggiunta automaticamente un'altra. Se non si specifica alcuna regola, convalida Usa riga "Default" hello.

| Proprietà | Descrizione |
| --- | --- |
| Tipo messaggio |Selezionare il tipo di messaggio EDI hello. |
| EDI Validation (Convalida EDI) |Eseguire la convalida EDI sui tipi di dati secondo quanto definito dalle proprietà EDI di hello dello schema di hello, le restrizioni di lunghezza, gli elementi dati vuoti e separatori finali. |
| Convalida estesa |Se non è di tipo di dati hello EDI, la convalida è sul requisito elemento dati di hello e ripetizione, enumerazioni e dati di convalida della lunghezza dell'elemento (min/max) è consentito. |
| Consenti zeri iniziali e finali |Tutti gli zero iniziali e finali e i caratteri di spazio vengono mantenuti e non vengono rimossi. |
| Rimuovi zero iniziali e finali |Tutti gli zero iniziali o finali vengono rimossi. |
| Criterio separatori finali |Consente di generare separatori finali. <p>Selezionare **non è consentito** tooprohibit finali delimitatori e separatori di hello inviato l'interscambio. Se l'interscambio di hello presenta delimitatori e separatori finali, interscambio hello viene dichiarato non valido. <p>Selezionare **facoltativo** toosend gli interscambi con o senza delimitatori e separatori finali. <p>Selezionare **obbligatorio** se interscambio inviato hello deve disporre di delimitatori e separatori finali. |

## <a name="find-your-created-agreement"></a>Individuare il contratto creato

1.  Al termine dell'impostazione di tutte le proprietà dell'accordo, in hello **Aggiungi** pannello, scegliere **OK** toofinish la creazione di contratto e il pannello di account di integrazione tooyour restituito.

    Il contratto appena aggiunto viene visualizzato nell'elenco **Contratti**.

2.  È anche possibile visualizzare i contratti nella panoramica dell'account di Integrazione. Scegliere il pannello di account di integrazione, **Panoramica**, quindi selezionare hello **contratti** riquadro. 

    ![Scegliere tooview riquadro "Accordi di" tutti i contratti](./media/logic-apps-enterprise-integration-edifact/edifact-4.png)   

## <a name="view-swagger-file"></a>Visualizzare il file Swagger
vedere i dettagli di Swagger hello tooview per connettore EDIFACT hello, [EDIFACT](/connectors/edifact/).

## <a name="learn-more"></a>Altre informazioni
* [Altre informazioni su Enterprise Integration Pack hello](logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack")  

