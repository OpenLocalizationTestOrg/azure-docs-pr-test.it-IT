---
title: Connettore del servizio di gestione in OMS aaaIT | Documenti Microsoft
description: Utilizzare monitor di toocentrally hello connettore di gestione del servizio IT e gestire gli elementi di lavoro ITSM hello in OMS e risolvere rapidamente eventuali problemi.
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a>Gestire centralmente gli elementi di lavoro ITSM con IT Service Management Connector (anteprima)

![Simbolo di IT Service Management Connector](./media/log-analytics-itsmc/itsmc-symbol.png)

È possibile utilizzare hello IT servizio Gestione connettore (ITSMC) in OMS Log Analitica toocentrally monitoraggio e gestione degli elementi di lavoro tra i prodotti o servizi ITSM.

Connettore di gestione del servizio IT Hello integra i prodotti di Gestione servizio IT (ITSM) esistente e i servizi con Analitica di Log di OMS.  soluzione hello è bidirezionale l'integrazione con prodotti e servizi ITSM, dove fornisce hello gli utenti di OMS eventi imprevisti toocreate un'opzione, gli avvisi o eventi nella soluzione ITSM. connettore Hello Importa anche i dati, ad esempio eventi imprevisti e richieste di modifica da soluzione ITSM in OMS Log Analitica.

Con IT Service Management Connector è possibile:

  - Monitorare e gestire centralmente gli elementi di lavoro per i prodotti e i servizi ITSM usati nell'organizzazione.
  - Creare elementi di lavoro ITSM, ad esempio avvisi, eventi, eventi imprevisto, in ITSM dagli avvisi OMS e tramite la ricerca log.
  - Leggere gli eventi imprevisti e richieste di modifica dalla soluzione ITSM e correlare i dati di log rilevanti nell'area di lavoro di Log Analytics.
  - Individuare eventuali eventi imprevisti e non comuni e risolverli, anche prima che gli utenti finali di hello chiamare e li segnala toohello helpdesk.
  - Importare i dati degli elementi di lavoro in Log Analytics e creare report indicatori di prestazioni chiave.  Grazie all'uso di questi report, è possibile individuare, valutare e agire su diversi elementi importanti, ad esempio la valutazione della presenza di malware.
  - Visualizzare i dashboard curati per ottenere informazioni approfondite su eventi imprevisti, richieste di modifica e sistemi interessati.
  - Risolvere i problemi più velocemente, è possibile correlare con altre soluzioni di gestione nell'area di lavoro Log Analitica hello.


## <a name="prerequisites"></a>Prerequisiti

tooimport hello ITSM gli elementi di lavoro in OMS Log Analitica soluzione hello richiede una connessione tra hello connettore di gestione del servizio IT in OMS hello e hello SM IT prodotti o servizi da cui importare gli elementi di lavoro hello.


## <a name="configuration"></a>Configurazione

Aggiungi hello area di lavoro OMS tooyour soluzione connettore di gestione del servizio IT, hello processo descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).

Connettore di gestione del servizio IT riquadro come può vedere nella raccolta di soluzioni hello:

![riquadro connettore](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

Dopo l'aggiunta di esito positivo, verrà visualizzato hello connettore di gestione del servizio IT in **OMS** > **impostazioni** > **Connected Sources.**

![ITSMC connessi](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> Per impostazione predefinita, hello connettore di gestione del servizio IT Aggiorna i dati della connessione hello una volta in ogni 24 ore. toorefresh immediatamente per qualsiasi modello di modifiche o gli della connessione aggiornamenti dei dati apportate, fare clic su connessione tooyour avanti di hello aggiornamento pulsante visualizzato.

 ![Aggiornamento di ITSMC refresh](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a>Management Pack
Questa soluzione non richiede alcun pacchetto di gestione.

## <a name="connected-sources"></a>Origini connesse

Hello ITSM seguenti prodotti e servizi sono supportati dal connettore di gestione del servizio IT hello:

- [System Center Service Manager (SCSM)](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [ServiceNow](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [Provance](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [Cherwell](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a>Utilizzo di soluzione hello

Una volta che ci si connette hello connettore di gestione del servizio IT OMS con il servizio ITSM, servizi Log Analitica hello avvia la raccolta dati hello da hello connesso ITSM prodotti o servizi.

> [!NOTE]
> - I dati importati dalla soluzione IT Service Management Connector vengono visualizzati in Log Analytics come eventi denominati **ServiceDesk_CL**.
- L'evento contiene un campo denominato **ServiceDeskWorkItemType_s**. che il relativo valore come eventi imprevisti, richiedere o richiesta di modifica, a seconda di hello di elemento di lavoro dati contenuti in hello **ServiceDesk_CL** evento.

## <a name="input-data"></a>Dati di input
Gli elementi di lavoro importati da hello ITSM prodotti e servizi.

Hello informazioni riportate di seguito vengono illustrati esempi di dati raccolti dal connettore di gestione dei servizi IT hello:

> [!NOTE]
> A seconda di hello tipo elemento di lavoro importato nel Log Analitica, **ServiceDesk_CL** contiene hello seguenti campi:

**Elemento di lavoro:** **Eventi imprevisti**  
ServiceDeskWorkItemType_s="Incident"

**Fields**

- ServiceDeskConnectionName
- ID Service Desk
- Stato
- Urgenza
- Impatto
- Priorità
- Riassegnazione
- Created By (Creato da)
- Resolved By (Risolto da)
- Closed By (Chiuso da)
- Sorgente
- Assegnato a 
- Categoria
- Titolo
- Descrizione
- Data di creazione
- Data di chiusura
- Data di risoluzione
- Data ultima modifica
- Computer


**Elemento di lavoro:****Richieste di modifica**

ServiceDeskWorkItemType_s="ChangeRequest"

**Fields**
- ServiceDeskConnectionName
- ID Service Desk
- Created By (Creato da)
- Closed By (Chiuso da)
- Sorgente
- Assegnato a 
- Titolo
- Tipo
- Categoria
- Stato
- Riassegnazione
- Conflict Status (Stato di conflitto)
- Urgenza
- Priorità
- Rischio
- Impatto
- Assegnato a 
- Data di creazione
- Data di chiusura
- Data ultima modifica
- Data richiesta
- Planned Start Date (Data di inizio pianificata)
- Planned End Date (Data di fine pianificata)
- Work Start Date (Data di inizio lavoro)
- Work End Date (Data di fine pianificata)
- Descrizione
- Computer

## <a name="output-data-for-a-servicenow-incident"></a>Dati di output per un evento imprevisto ServiceNow

| Campo OMS | Campo ITSM |
|:--- |:--- |
| ServiceDeskId_s| Number |
| IncidentState_s | Stato |
| Urgency_s |Urgenza |
| Impact_s |Impatto|
| Priority_s | Priorità |
| CreatedBy_s | Aperto da |
| ResolvedBy_s | Risolto da|
| ClosedBy_s  | Chiuso da |
| Source_s| Tipo di contatto |
| AssignedTo_s | Troppo assegnato |
| Category_s | Categoria |
| Title_s|  Breve descrizione |
| Description_s|  Note |
| CreatedDate_t|  Aperto |
| ClosedDate_t| closed|
| ResolvedDate_t|Risolto|
| Computer  | Elemento di configurazione |

## <a name="output-data-for-a-servicenow-change-request"></a>Dati di output per una richiesta di modifica ServiceNow

| Campo OMS | Campo ITSM |
|:--- |:--- |
| ServiceDeskId_s| Number |
| CreatedBy_s | Richiesto da |
| ClosedBy_s | Chiuso da |
| AssignedTo_s | Troppo assegnato |
| Title_s|  Breve descrizione |
| Type_s|  Tipo |
| Category_s|  Categoria |
| CRState_s|  Stato|
| Urgency_s|  Urgenza |
| Priority_s| Priorità|
| Risk_s| Rischio|
| Impact_s| Impatto|
| RequestedDate_t  | Data richiesta |
| ClosedDate_t | Data di chiusura |
| PlannedStartDate_t  |     Data di inizio pianificata |
| PlannedEndDate_t  |   Data di fine pianificata |
| WorkStartDate_t  | Data di inizio effettiva |
| WorkEndDate_t | Data di fine effettiva|
| Description_s | Descrizione |
| Computer  | Elemento di configurazione |

**Schermata di esempio di Log Analytics per i dati ITSM:**

![Schermata di Log Analytics](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a>IT Service Management connector: integrazione con altre soluzioni OMS

Connettore di gestione del servizio IT, attualmente supporta l'integrazione con hello soluzione mappa del servizio.

Mappa del servizio individua automaticamente i componenti dell'applicazione in Windows hello e mappe e i sistemi Linux hello la comunicazione tra servizi. Consente di tooview i server come si immaginano – come sistemi interconnessi che offrono servizi critici. L'elenco dei servizi mostra le connessioni fra i server, i processi e le porte di tutte le architetture connesse via TCP senza il bisogno di alcuna configurazione a parte l'installazione di un agente. Altre informazioni: [Elenco dei servizi](../operations-management-suite/operations-management-suite-service-map.md).

L'integrazione, è possibile visualizzare hello service desk gli elementi creati in soluzioni ITSM hello come illustrato nell'esempio seguente hello:

![Soluzione integrata ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a>Creare elementi di lavoro ITSM per avvisi di OMS

Per gli avvisi OMS hello, è possibile creare elementi di lavoro associati in origini ITSM hello connesso.  toodo hello, questo uso seguente procedura:

1. Da **ricerca nei Log** finestra, eseguire una ricerca di log query tooview dati. Risultati della query sono l'origine hello per gli elementi di lavoro.
2. In **ricerca nei Log**, fare clic su **avviso** tooopen hello **Aggiungi regola di avviso** pagina.

    ![Schermata di Log Analytics](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. In hello **Aggiungi regola di avviso** finestra, fornire dettagli hello necessario per **nome**, **gravità**, **query di ricerca**, e  **Criteri di avviso** (misurazione finestra/metrica tempo).
4. Selezionare **Sì** per **Azioni ITSM**.
5. Selezionare la connessione ITSM hello **Seleziona connessione** elenco.
6. Fornire dettagli hello come richiesto.
7. un elemento di lavoro separata per ogni voce di log di hello questo avviso, seleziona toocreate **creare singoli elementi di lavoro per ogni voce di log** casella di controllo.

    Or

    lasciare questa casella di controllo deselezionata toocreate solo un elemento di lavoro per qualsiasi numero di voci di log in questo avviso.

7. Fare clic su **Salva**.

verrà creata nell'avviso OMS Hello **avvisi**. Hello lavoro della connessione corrispondente ITSM gli elementi vengono creati quando viene soddisfatta la condizione dell'avviso di hello specificato.

## <a name="create-itsm-work-items-from-oms-logs"></a>Creare elementi di lavoro ITSM da log di OMS

È possibile creare elementi di lavoro nelle origini ITSM hello connesso tramite una ricerca nei Log di OMS. toodo hello, questo uso seguente procedura:

1. Da **ricerca nei Log**, cercare i dati di hello richiesto, selezionare dettagli hello e fare clic su **Crea elemento di lavoro**.

    Hello **elemento di lavoro di ITSM creare** verrà visualizzata la finestra:

    ![Schermata di Log Analytics](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   Aggiungere i seguenti dettagli hello:

  - **Titolo elemento di lavoro**: titolo dell'elemento di lavoro hello.
  - **Descrizione elemento di lavoro**: descrizione per il nuovo elemento di lavoro hello.
  - **Computer interessati**: nome del computer hello in cui è stati trovati i dati di log.
  - **Selezionare connessione**: connessione ITSM in cui si desidera toocreate questo elemento di lavoro.
  - **Elemento di lavoro**: tipo di elemento di lavoro.

3. Fare clic su un modello di elemento di lavoro esistente per un evento imprevisto, toouse **Sì** in **elemento di lavoro genera basato sul modello di hello** opzione e quindi fare clic su **crea**.

    Oppure

    Fare clic su **n** se si desiderano tooprovide i valori personalizzati.

4. Specificare i valori appropriati di hello in hello **tipo contatto**, **impatto**, **urgenza**, **categoria**, e **Sub Category**  caselle di testo e quindi fare clic su **crea**.

verrà creato l'elemento di lavoro Hello in hello ITSM, che è anche possibile visualizzare in OMS.

## <a name="troubleshoot-itsm-connections-in-oms"></a>Risolvere i problemi delle connessioni ITSM in OMS
1.  Se si verifica un errore di connessione nell'interfaccia utente dell'origine connesso e viene visualizzato hello **errore durante il salvataggio di connessione** dei messaggi, hello seguenti:
 - In caso di connessioni a ServiceNow, Cherwell e Provance, assicurarsi di segreto di hello correttamente immesso nome utente/password e il client ID e client per ciascuna delle connessioni hello. Se l'errore hello persiste, controllare se si dispone di privilegi sufficienti nella connessione di hello corrispondente ITSM prodotto toomake hello.
 - In caso di Service Manager, verificare che hello Web app è stata distribuita correttamente e viene creata la connessione ibrida. connessione di hello tooverify è stata stabilita con il computer di Service Manager locale hello, visitare l'URL dell'app Web hello come descritto nella documentazione di hello per rendere hello [connessione ibrida](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).

2.  Se i dati da ServiceNow non sono recupero sincronizzati in OMS, verificare che tale istanza di ServiceNow hello non è sospeso. In questo momento potrebbe verificarsi in hello ServiceNow Dev casi, quando è inattivo. Else, segnala un problema di hello.
3.  Se gli avvisi vengono recupero generati da OMS ma non sono recupero creati elementi di lavoro nel prodotto ITSM o elementi di configurazione non ricevono gli elementi creati collegato toowork o per qualsiasi informazioni generiche, hello seguenti:
 -  Soluzione di connettore di gestione del servizio IT nel portale OMS è possibile tooget usato un riepilogo delle connessioni/lavoro gli elementi e i computer e così via. Scegliere il messaggio di errore hello nel pannello stato hello, passare troppo**ricerca nei Log** e visualizzare connessione hello con errore hello utilizzando i dettagli di hello nel messaggio di errore hello.
 - è possibile visualizzare direttamente le informazioni relative a errori/hello in hello **ricerca nei Log** pagina *tipo = ServiceDeskLog_CL*.

## <a name="troubleshoot-service-manager-web-app-deployment"></a>Risolvere i problemi di distribuzione dell’app Web Service Manager
1.  In caso di problemi con la distribuzione di app web, assicurarsi di disporre di autorizzazioni sufficienti nella sottoscrizione hello indicato toocreate/distribuire le risorse.
2.  Se **riferimento all'oggetto non impostato tooinstance di un oggetto** viene visualizzato il messaggio di errore durante l'esecuzione di hello [script](log-analytics-itsmc-service-manager-script.md) verificare di avere immesso i valori validi in **configurazione utente**sezione.
3.  Se non si toocreate service bus inoltro dello spazio dei nomi, verificare che hello necessarie a provider di risorse è registrato nella sottoscrizione hello. Se non è registrato, crearla manualmente dal portale di Azure hello. È inoltre possibile creare mentre [creazione connessione ibrida hello](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) da hello portale di Azure.


## <a name="contact-us"></a>Contatti

Per qualsiasi query o i commenti e suggerimenti su hello connettore di gestione del servizio IT, contattare Microsoft all'indirizzo [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).

## <a name="next-steps"></a>Passaggi successivi
[Aggiungere ITSM prodotti e servizi tooIT connettore del servizio di gestione](log-analytics-itsmc-connections.md).
