---
title: i messaggi per l'integrazione di enterprise B2B - App Azure per la logica aaaX12 | Documenti Microsoft
description: Scambiare messaggi X12 in formato EDI per l'integrazione aziendale B2B con App per la logica di Azure
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 7422d2d5-b1c7-4a11-8c9b-0d8cfa463164
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 20a077b299875a16ada66a500d5f1c8f9972d309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-x12-messages-for-enterprise-integration-with-logic-apps"></a>Scambiare messaggi X12 per l'integrazione aziendale con le app per la logica

Per poter scambiare messaggi X12 con App per la logica di Azure, è necessario creare un contratto X12 e archiviarlo nell'account di integrazione. Ecco la procedura relativa hello toocreate un X12 contratto.

> [!NOTE]
> Questa pagina vengono illustrate le funzionalità di hello X12 per le app di logica di Azure. Per altre informazioni, vedere [EDIFACT](logic-apps-enterprise-integration-edifact.md).

## <a name="before-you-start"></a>Prima di iniziare

Ecco gli elementi di hello che è necessario:

* Un [account di integrazione](../logic-apps/logic-apps-enterprise-integration-accounts.md) già definito e associato alla sottoscrizione di Azure.
* Almeno due [partner](../logic-apps/logic-apps-enterprise-integration-partners.md) che vengono definite nell'account di integrazione e configurate con l'identificatore hello X12 in **identità di Business**    
* Richiesta [schema](../logic-apps/logic-apps-enterprise-integration-schemas.md) per il caricamento tooyour [account di integrazione](../logic-apps/logic-apps-enterprise-integration-accounts.md)

Dopo aver [creare un account di integrazione](../logic-apps/logic-apps-enterprise-integration-accounts.md), [aggiungere partner](logic-apps-enterprise-integration-partners.md)e hanno un [schema](../logic-apps/logic-apps-enterprise-integration-schemas.md) che si desidera toouse, è possibile creare un X12 contratto attenendosi alla procedura seguente.

## <a name="create-an-x12-agreement"></a>Creare un contratto X12

1.  Accedi toohello [portale di Azure](http://portal.azure.com "portale di Azure"). Scegliere dal menu a sinistra hello **più servizi**. 

    > [!TIP]
    > Se non viene visualizzato **più servizi**, è necessario innanzitutto menu hello tooexpand. Nella parte superiore di hello del menu hello compresso, selezionare **menu Mostra**.

    ![Fare clic su "Altri servizi" nel menu a sinistra](./media/logic-apps-enterprise-integration-x12/account-1.png)

2.  Nella casella di ricerca hello, digitare "integrazione" come filtro. Selezionare dall'elenco risultati hello **account di integrazione**.  

    ![Filtro su "integrazione", selezionare "Account di integrazione"](./media/logic-apps-enterprise-integration-x12/account-2.png)

3. In hello **account di integrazione** blade che viene aperta, l'account di integrazione hello select in cui si desidera contratto hello tooadd.
Se non viene visualizzato alcun account di integrazione, [crearne prima uno](../logic-apps/logic-apps-enterprise-integration-accounts.md "Tutte le informazioni sugli account di integrazione").

    ![Selezionare account di integrazione in toocreate hello contratto](./media/logic-apps-enterprise-integration-x12/account-3.png)

4. Selezionare **Panoramica**, quindi selezionare hello **contratti** riquadro. Se non si dispone di un riquadro contratti, è innanzitutto necessario aggiungere il riquadro hello. 

    ![Selezionare il riquadro "Contratti"](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. Nel pannello contratti hello visualizzato, scegliere **Aggiungi**.

    ![Selezionare "Aggiungi"](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)     

6. In **Aggiungi**, digitare un **nome** per il contratto. Tipo di contratto hello selezionare **X12**. Seleziona hello **Partner Host**, **identità Host**, **Partner Guest**, e **identità Guest** per il contratto. Per ulteriori dettagli delle proprietà, vedere la tabella hello in questo passaggio.

    ![Fornire i dettagli relativi al contratto](./media/logic-apps-enterprise-integration-x12/x12-1.png)  

    | Proprietà | Descrizione |
    | --- | --- |
    | Nome |Nome del contratto hello |
    | Tipo di contratto | Deve essere X12 |
    | Host Partner (Partner host) |Un contratto prevede un partner host e un partner guest. partner host Hello rappresenta organizzazione hello che configura l'accordo hello. |
    | Host Identity (Identità host) |Un identificatore per il partner host hello |
    | Guest Partner (Partner guest) |Un contratto prevede un partner host e un partner guest. partner guest Hello rappresenta organizzazione hello usato per esegue attività con partner host hello. |
    | identità guest |Un identificatore per il partner guest hello |
    | Receive Settings (Impostazioni di ricezione) |Queste proprietà si applicano tooall ricevuti da un contratto. |
    | Send Settings (Impostazioni di invio) |Queste proprietà si applicano tooall i messaggi inviati da un contratto. |  

  > [!NOTE]
  > Risoluzione dell'accordo dipende dalla corrispondenza hello qualificatore e identificatore e qualificatore ricevitore hello e identificatore mittente definiti nel messaggio in ingresso e di partner hello X12. Se questi valori vengono modificati per il partner, è possibile aggiornare troppo contratto hello.

## <a name="configure-how-your-agreement-handles-received-messages"></a>Configurare il modo in cui il contratto riceve i messaggi

Ora che sono state impostate proprietà di contratto hello, è possibile configurare come contratto identifica e gestisce i messaggi in ingresso ricevuti dal partner mediante il presente contratto.

1.  In **Aggiungi**, selezionare **Impostazioni di ricezione**.
Configurare queste proprietà in base al contratto con partner hello che scambia messaggi con l'utente. Per le relative proprietà, vedere le tabelle di hello in questa sezione.

    Il controllo **Impostazioni di ricezione** è suddiviso nelle sezioni seguenti: Identificatori, Riconoscimento, Schemi, Buste, Numeri di controllo, Convalide e Impostazioni interne.

2. Al termine, assicurarsi che toosave le impostazioni scegliendo **OK**.

A questo punto il contratto toohandle pronto in ingresso le impostazioni di messaggi conformi tooyour selezionate.

### <a name="identifiers"></a>Identificatori

![Impostare le proprietà degli identificatori](./media/logic-apps-enterprise-integration-x12/x12-2.png)  

| Proprietà | Descrizione |
| --- | --- |
| ISA1 (Qualificatore di autorizzazione) |Selezionare valore qualificatore di autorizzazione hello dall'elenco a discesa hello. |
| ISA2 |Facoltativo. Immettere il valore relativo alle informazioni di autorizzazione. Se il valore di hello che immesso per ISA1 è diverso da 00, immettere un minimo di un carattere alfanumerico e un massimo di 10. |
| Qualificatore di sicurezza (ISA3) |Selezionare valore qualificatore di sicurezza hello dall'elenco a discesa hello. |
| ISA4 |Facoltativo. Immettere il valore di informazioni di hello sicurezza. Se il valore di hello che immesso per ISA3 è diverso da 00, immettere un minimo di un carattere alfanumerico e un massimo di 10. |

### <a name="acknowledgment"></a>Acknowledgment (Riconoscimento)

![Impostare le proprietà di riconoscimento](./media/logic-apps-enterprise-integration-x12/x12-3.png) 

| Proprietà | Descrizione |
| --- | --- |
| TA1 expected (Previsto TA1) |Restituisce un mittente di interscambio toohello riconoscimento tecnico |
| FA expected (Previsto FA) |Restituisce un mittente di interscambio toohello riconoscimento funzionale. Quindi selezionare se si desidera che i riconoscimenti hello 997 o 999, in base nella versione dello schema hello |
| Include AK2/IK2 Loop (Includi ciclo AK2/IK2) |Abilita la generazione di cicli AK2 nei riconoscimenti funzionali per i set di transazioni accettati |

### <a name="schemas"></a>Schemi

Scegliere uno schema per ogni tipo di transazione (ST1) e di applicazione mittente (GS2). Hello ricezione messaggio in arrivo hello disassemblato dalla pipeline mediante hello valori corrispondenti per ST1 e GS2 hello messaggio in ingresso con hello valori è impostato in questa casella e schema hello del messaggio in ingresso a hello impostata qui.

![Selezionare lo schema](./media/logic-apps-enterprise-integration-x12/x12-33.png) 

| Proprietà | Descrizione |
| --- | --- |
| Versione |Selezionare la versione di hello X12 |
| Tipo di transazione (ST01) |Selezionare il tipo di transazione hello |
| Sender Application (GS02) (Applicazione mittente (GS02)) |Selezionare un'applicazione hello mittente |
| Schema |Selezionare il file di schema hello da toouse. Gli schemi vengono aggiunti tooyour account di integrazione. |

> [!NOTE]
> Configurare hello necessario [Schema](../logic-apps/logic-apps-enterprise-integration-schemas.md) ovvero caricato tooyour [account integrazione](../logic-apps/logic-apps-enterprise-integration-accounts.md).

### <a name="envelopes"></a>Buste

![Specificare il separatore di hello in un set di transazioni: scegliere un identificatore Standard o un separatore di ripetizioni](./media/logic-apps-enterprise-integration-x12/x12-34.png)

| Proprietà | Descrizione |
| --- | --- |
| Utilizzo ISA11 |Specifica toouse separatore hello in un set di transazioni: <p>Selezionare **identificatore Standard** toouse un punto (.) per la notazione decimale, anziché la notazione decimale del documento in ingresso di hello in hello EDI hello pipeline di ricezione. <p>Selezionare **separatore di ripetizioni** separatore hello toospecify occorrenze ripetute di un elemento dati semplice o una struttura dati ripetuta. Ad esempio, in genere hello accento circonflesso (^) viene utilizzato come separatore di ripetizioni hello. Per gli schemi HIPAA, è possibile utilizzare solo l'accento circonflesso hello. |

### <a name="control-numbers"></a>Numeri di controllo

![Selezionare una modalità di controllo duplicati di numeri toohandle](./media/logic-apps-enterprise-integration-x12/x12-35.png) 

| Proprietà | Descrizione |
| --- | --- |
| Disallow Interchange Control Number duplicates (Non consentire duplicati di numeri di controllo interscambio) |Consente di bloccare gli interscambi duplicati. Controlla hello numero di controllo interscambio (ISA13) per il numero di controllo interscambio hello ricevuto. Se viene rilevata una corrispondenza, hello ricezione pipeline non viene elaborato interscambio hello. È possibile specificare hello numero di giorni per l'esecuzione di hello controllo assegnando un valore per *verifica isa13 duplicato ogni (giorni)*. |
| Disallow Group control number duplicates (Non consentire duplicati di numeri di controllo di gruppo) |Consente di bloccare gli interscambi con numeri di controllo di gruppo duplicati. |
| Disallow Transaction set control number duplicates (Non consentire duplicati di numeri di controllo set di transazioni) |Consente di bloccare gli interscambi con numeri di controllo di set di transazioni duplicati. |

### <a name="validations"></a>Convalide

![Impostare le proprietà di convalida dei messaggi ricevuti](./media/logic-apps-enterprise-integration-x12/x12-36.png) 

Dopo aver completato ogni riga di convalida, ne viene aggiunta automaticamente un'altra. Se non si specifica alcuna regola, convalida Usa riga "Default" hello.

| Proprietà | Descrizione |
| --- | --- |
| Tipo messaggio |Selezionare il tipo di messaggio EDI hello. |
| EDI Validation (Convalida EDI) |Eseguire la convalida EDI sui tipi di dati definiti da schema hello EDI proprietà, le restrizioni di lunghezza, gli elementi dati vuoti e separatori finali. |
| Convalida estesa |Se non è di tipo di dati hello EDI, la convalida è sul requisito elemento dati di hello e ripetizione, enumerazioni e dati di convalida della lunghezza dell'elemento (min/max) è consentito. |
| Consenti zeri iniziali e finali |Tutti gli zero iniziali e finali e i caratteri di spazio vengono mantenuti e non vengono rimossi. |
| Rimuovi zero iniziali e finali |Tutti gli zero iniziali e finali e i caratteri di spazio vengono rimossi. |
| Criterio separatori finali |Consente di generare separatori finali. <p>Selezionare **non è consentito** tooprohibit i delimitatori finali e il separatore nel hello ricevuto l'interscambio. Se l'interscambio di hello presenta delimitatori e separatori finali, interscambio hello viene dichiarato non valido. <p>Selezionare **facoltativo** tooaccept gli interscambi con o senza delimitatori e separatori finali. <p>Selezionare **obbligatorio** quando necessario interscambio hello delimitatori e separatori finali. |

### <a name="internal-settings"></a>Impostazioni interne

![Selezionare le impostazioni interne](./media/logic-apps-enterprise-integration-x12/x12-37.png) 

| Proprietà | Descrizione |
| --- | --- |
| Converti formato decimale implicito "Nn" tooa base 10 valore numerico |Converte un numero EDI specificato hello formato "Nn" in un valore numerico in base 10 |
| Crea tag XML vuoti se sono consentiti separatori finali |Selezionare questo mittente di interscambio hello toohave casella di controllo includono vuoto tag XML per i separatori finali. |
| Suddividi interscambio in set di transazioni - Sospendi set di transazioni in caso di errore|Consente di analizzare ogni set di transazioni in un interscambio in un documento XML separato applicando i set di transazioni toohello hello busta appropriata. Sospende solo le transazioni di hello in cui la convalida di hello ha esito negativo. |
| Suddividi interscambio in set di transazioni - Sospendi interscambio in caso di errore|Consente di analizzare ogni set di transazioni in un interscambio in un documento XML separato applicando la busta appropriata hello. Sospende l'intero interscambio quando uno o più set di transazioni nell'interscambio hello convalida ha esito negativo. | 
| Mantieni interscambio - Sospendi set transazioni in caso di errore |Lascia intatto l'interscambio hello, crea un documento XML per l'intero interscambio in batch hello. Sospende solo i set di transazioni di hello convalida non riesce, pur continuando tooprocess tutti gli altri set di transazioni. |
| Mantieni interscambio - Sospendi interscambio in caso di errore |Lascia intatto l'interscambio hello, crea un documento XML per l'intero interscambio in batch hello. Sospende l'intero interscambio hello quando uno o più set di transazioni nell'interscambio hello convalida ha esito negativo. |

## <a name="configure-how-your-agreement-sends-messages"></a>Configurare il modo in cui il contratto invia messaggi

È possibile configurare come contratto identifica e gestisce i messaggi in uscita inviati partner tooyour attraverso il presente contratto.

1.  In **Aggiungi**, selezionare **Impostazioni di avvio**.
Configurare queste proprietà in base al contratto con il partner con cui si scambiano i messaggi. Per le relative proprietà, vedere le tabelle di hello in questa sezione.

    Il controllo **Impostazioni di invio** è suddiviso nelle sezioni seguenti: Identificatori, Riconoscimento, Schemi, Buste, Set di caratteri e separatori, Numeri di controllo e Convalida.

2. Al termine, assicurarsi che toosave le impostazioni scegliendo **OK**.

Il contratto è ora pronto toohandle messaggi conformi a impostazioni tooyour selezionata in uscita.

### <a name="identifiers"></a>Identificatori

![Impostare le proprietà degli identificatori](./media/logic-apps-enterprise-integration-x12/x12-4.png)  

| Proprietà | Descrizione |
| --- | --- |
| ISA1 (Qualificatore di autorizzazione) |Selezionare valore qualificatore di autorizzazione hello dall'elenco a discesa hello. |
| ISA2 |Immettere il valore relativo alle informazioni di autorizzazione. Se questo valore è diverso da 00, immettere almeno uno e al massimo 10 caratteri alfanumerici. |
| ISA3 (Qualificatore di sicurezza) |Selezionare valore qualificatore di sicurezza hello dall'elenco a discesa hello. |
| ISA4 |Immettere il valore di informazioni di hello sicurezza. Se questo valore è diverso da 00, per la casella di testo hello valore (ISA4) immettere un minimo di un valore alfanumerico e un massimo di 10. |

### <a name="acknowledgment"></a>Acknowledgment (Riconoscimento)

![Impostare le proprietà di riconoscimento](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| Proprietà | Descrizione |
| --- | --- |
| TA1 expected (Previsto TA1) |Restituisce un mittente di interscambio toohello riconoscimento tecnico (TA1). Questa impostazione specifica di tale partner host hello che invia le richieste dei messaggi hello un acknowledgment dal partner guest hello nell'accordo hello. Questi acknowledgment sono attesi dal partner host hello in base alle impostazioni di ricezione hello del contratto hello. |
| FA expected (Previsto FA) |Restituisce un mittente di interscambio toohello riconoscimento funzionale (FA). Selezionare se si desidera acknowledgment hello 997 o 999, in base alle versioni dello schema hello in uso. Questi acknowledgment sono attesi dal partner host hello in base alle impostazioni di ricezione hello del contratto hello. |
| Versione FA |Selezionare la versione di hello cespiti |

### <a name="schemas"></a>Schemi

![Selezionare toouse dello schema](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| Proprietà | Descrizione |
| --- | --- |
| Versione |Selezionare la versione di hello X12 |
| Tipo di transazione (ST01) |Selezionare il tipo di transazione hello |
| Schema |Selezionare toouse schema hello. Gli schemi si trovano nell'account di integrazione. Se si seleziona prima lo schema, viene automaticamente configurata la versione e il tipo di transizione  |

> [!NOTE]
> Configurare hello necessario [Schema](../logic-apps/logic-apps-enterprise-integration-schemas.md) ovvero caricato tooyour [account integrazione](../logic-apps/logic-apps-enterprise-integration-accounts.md).

### <a name="envelopes"></a>Buste

![Specificare il separatore di hello in un set di transazioni: scegliere un identificatore Standard o un separatore di ripetizioni](./media/logic-apps-enterprise-integration-x12/x12-6.png) 

| Proprietà | Descrizione |
| --- | --- |
| Utilizzo ISA11 |Specifica toouse separatore hello in un set di transazioni: <p>Selezionare **identificatore Standard** toouse un punto (.) per la notazione decimale, anziché la notazione decimale del documento in ingresso di hello in hello EDI hello pipeline di ricezione. <p>Selezionare **separatore di ripetizioni** separatore hello toospecify occorrenze ripetute di un elemento dati semplice o una struttura dati ripetuta. Ad esempio, in genere hello accento circonflesso (^) viene utilizzato come separatore di ripetizioni hello. Per gli schemi HIPAA, è possibile utilizzare solo l'accento circonflesso hello. |

### <a name="control-numbers"></a>Numeri di controllo

![Specificare le proprietà del numero di controllo](./media/logic-apps-enterprise-integration-x12/x12-8.png) 

| Proprietà | Descrizione |
| --- | --- |
| Numero versione controllo (ISA12) |Selezionare una versione di hello di hello standard X12 |
| Indicatore di utilizzo (ISA15) |Selezionare hello contesto di un interscambio.  i valori Hello sono informazioni, dati di produzione o dati di test |
| Schema |Genera l'errore hello GS e ST segmenti per un interscambio con codifica X12 che invia toohello Pipeline di trasmissione |
| GS1 |Facoltativo, selezionare un valore per il codice funzionale hello dall'elenco a discesa hello |
| GS2 |Facoltativo, mittente dell'applicazione |
| GS3 |Facoltativo, ricevente dell'applicazione |
| GS4 |Facoltativo, selezionare CCYYMMDD o YYMMDD |
| GS5 |Facoltativo, selezionare HHMM, HHMMSS o HHMMSSdd |
| GS7 |Facoltativo, selezionare un valore per hello agenzia responsabile dall'elenco a discesa hello |
| GS8 |Facoltativa, versione del documento hello |
| Numero di controllo interscambio (ISA13) |Richiesto, immettere un intervallo di valori per il numero di controllo interscambio hello. Immettere un valore numerico compreso tra 1 e 999999999 |
| Numero di controllo gruppo (GS06) |Richiesto, immettere un intervallo di numeri per il numero di controllo gruppo hello. Immettere un valore numerico compreso tra 1 e 999999999 |
| Numero di controllo set transazioni (ST02) |Richiesto, immettere un intervallo di numeri per il numero di controllo Set transazioni hello. Immettere un intervallo di valori numerici compreso tra 1 e 999999999 |
| Prefisso |Facoltativo, designato per l'intervallo di hello di numeri di controllo set transazioni utilizzati nel riconoscimento. Immettere un valore numerico per i due campi centrali hello e un valore alfanumerico (se desiderato) per i campi di prefisso e suffisso hello. campi intermedi Hello sono obbligatori e contengono hello valori minimo e massimo per il numero di controllo di hello |
| Suffisso |Facoltativo, designato per l'intervallo di hello di numeri di controllo set transazioni utilizzati in un riconoscimento. Immettere un valore numerico per i due campi centrali hello e un valore alfanumerico (se desiderato) per i campi di prefisso e suffisso hello. campi intermedi Hello sono obbligatori e contengono hello valori minimo e massimo per il numero di controllo di hello |

### <a name="character-sets-and-separators"></a>Character Sets and Separators (Set di caratteri e separatori)

Diverso da set di caratteri hello, è possibile immettere un diverso set di delimitatori per ogni tipo di messaggio. Se per un determinato schema del messaggio non è specificato un set di caratteri, viene utilizzato il set di caratteri predefinito hello.

![Specificare i delimitatori per i tipi di messaggio](./media/logic-apps-enterprise-integration-x12/x12-9.png) 

| Proprietà | Descrizione |
| --- | --- |
| Toobe di Set di caratteri utilizzato |toovalidate hello proprietà set di caratteri hello selezionare X12. opzioni di Hello sono Basic, esteso e UTF8. |
| Schema |Selezionare uno schema dall'elenco a discesa hello. Dopo aver completato ogni riga, viene aggiunta automaticamente una nuova riga. Per lo schema selezionato hello, separatori hello selezionare set che si desidera toouse, in base alle seguenti descrizioni separatore hello. |
| Tipo di input |Selezionare un tipo di input dall'elenco a discesa hello. |
| Component Separator |gli elementi dati compositi tooseparate, immettere un singolo carattere. |
| Data Element Separator |gli elementi dati semplici tooseparate negli elementi dati compositi, immettere un singolo carattere. |
| Replacement Character |Immettere un carattere di sostituzione utilizzato per la sostituzione di tutti i caratteri separatori nei dati di payload hello durante la generazione di messaggi hello X12 in uscita. |
| Segment Terminator |fine hello tooindicate di un segmento EDI, immettere un singolo carattere. |
| Suffisso |Selezionare carattere hello utilizzato con l'identificatore di segmento hello. Se si specifica un suffisso, hello elemento di dati carattere di terminazione segmento può essere vuoto. Se il carattere di terminazione di hello segmento viene lasciato vuoto, è necessario specificare un suffisso. |

> [!TIP]
> tooprovide i valori di carattere speciale, modificare il contratto di hello come JSON e fornire valore ASCII hello per carattere speciale hello.

### <a name="validation"></a>Convalida

![Impostare le proprietà di convalida per l'invio di messaggi](./media/logic-apps-enterprise-integration-x12/x12-10.png) 

Dopo aver completato ogni riga di convalida, ne viene aggiunta automaticamente un'altra. Se non si specifica alcuna regola, convalida Usa riga "Default" hello.

| Proprietà | Descrizione |
| --- | --- |
| Tipo messaggio |Selezionare il tipo di messaggio EDI hello. |
| EDI Validation (Convalida EDI) |Eseguire la convalida EDI sui tipi di dati definiti da schema hello EDI proprietà, le restrizioni di lunghezza, gli elementi dati vuoti e separatori finali. |
| Convalida estesa |Se non è di tipo di dati hello EDI, la convalida è sul requisito elemento dati di hello e ripetizione, enumerazioni e dati di convalida della lunghezza dell'elemento (min/max) è consentito. |
| Consenti zeri iniziali e finali |Tutti gli zero iniziali e finali e i caratteri di spazio vengono mantenuti e non vengono rimossi. |
| Rimuovi zero iniziali e finali |Tutti gli zero iniziali o finali vengono rimossi. |
| Criterio separatori finali |Consente di generare separatori finali. <p>Selezionare **non è consentito** tooprohibit finali delimitatori e separatori di hello inviato l'interscambio. Se l'interscambio di hello presenta delimitatori e separatori finali, interscambio hello viene dichiarato non valido. <p>Selezionare **facoltativo** toosend gli interscambi con o senza delimitatori e separatori finali. <p>Selezionare **obbligatorio** se interscambio inviato hello deve disporre di delimitatori e separatori finali. |

## <a name="find-your-created-agreement"></a>Individuare il contratto creato

1.  Al termine dell'impostazione di tutte le proprietà dell'accordo, in hello **Aggiungi** pannello, scegliere **OK** toofinish la creazione di contratto e il pannello di account di integrazione tooyour restituito.

    Il contratto appena aggiunto viene visualizzato nell'elenco **Contratti**.

2.  È anche possibile visualizzare i contratti nella panoramica dell'account di Integrazione. Scegliere il pannello di account di integrazione, **Panoramica**, quindi selezionare hello **contratti** riquadro.

    ![Scegliere tooview riquadro "Accordi di" tutti i contratti](./media/logic-apps-enterprise-integration-x12/x12-1-5.png)   

## <a name="view-hello-swagger"></a>Swagger hello vista
Vedere hello [swagger dettagli](/connectors/x12/). 

## <a name="learn-more"></a>Altre informazioni
* [Altre informazioni su Enterprise Integration Pack hello](../logic-apps/logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack")  

