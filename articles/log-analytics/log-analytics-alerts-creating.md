---
title: aaaCreating gli avvisi in OMS Log Analitica | Documenti Microsoft
description: Gli avvisi nel registro Analitica identificare importanti informazioni nel repository OMS e in modo proattivo ricevere una notifica di problemi o richiamare azioni tooattempt toocorrect li.  In questo articolo viene descritto come toocreate una regola di avviso e azioni diverse a dettagli hello possono assumere.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: 3d035b2426dda9645b19e6c993dc26a2d95a2a78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-alert-rules-in-log-analytics"></a>Utilizzo delle regole di avviso in Log Analytics
Gli avvisi vengono creati da regole di avviso che eseguono automaticamente ricerche log a intervalli regolari.  Creano un record di avviso se i risultati di hello corrispondono a determinati criteri.  regola Hello quindi eseguire automaticamente uno o più azioni tooproactively ricevere una notifica di avviso hello o richiamare un altro processo.   

In questo articolo descrive toocreate processi hello e modificare le regole di avviso tramite il portale di OMS hello.  Per informazioni dettagliate sulle diverse impostazioni hello e come tooimplement necessaria logica, vedere [informazioni sugli avvisi nel registro Analitica](log-analytics-alerts.md).

>[!NOTE]
> Attualmente, è possibile creare o modificare una regola di avviso utilizzando hello portale di Azure. 

## <a name="create-an-alert-rule"></a>Creare una regola di avviso

toocreate una regola di avviso tramite il portale di OMS hello, iniziare creando una ricerca di log per i record che deve richiamare avviso hello hello.  Hello **avviso** pulsante verrà reso disponibile in modo è possibile creare e configurare una regola di avviso hello.

>[!NOTE]
> Attualmente, è possibile creare un massimo di 250 regole di avviso in un'area di lavoro OMS. 

1. Dalla pagina Overview di OMS hello, fare clic su **ricerca nei Log**.
2. Creare una nuova query di ricerca nei log o selezionarne una salvata. 
3. Fare clic su **avviso** nella parte superiore di hello di hello di hello pagina tooopen **Aggiungi regola di avviso** dello schermo.
4. Configurare una regola di avviso hello utilizzando le informazioni in [dettagli delle regole di avviso](#details-of-alert-rules) sotto.
6. Fare clic su **salvare** toocomplete regola di avviso hello.  Verrà avviata immediatamente l'esecuzione.


## <a name="edit-an-alert-rule"></a>Modificare una regola di avviso
È possibile ottenere un elenco di tutte le regole di avviso in hello **avvisi** dal menu Registro Analitica **impostazioni**.  

![Gestisci avvisi](./media/log-analytics-alerts/configure.png)

1. In hello seleziona console OMS hello **impostazioni** riquadro.
2. Selezionare **Avvisi**.

Da questa visualizzazione è possibile eseguire più azioni.

* Disabilitare una regola selezionando **Off** tooit successivo.
* Modificare una regola di avviso facendo clic su Avanti tooit di hello matita icona.
* Rimuovere una regola di avviso facendo clic su hello **X** tooit Avanti icona. 

## <a name="details-of-alert-rules"></a>Dettagli delle regole di avviso
Quando si crea o si modifica una regola di avviso nel portale OMS hello, si utilizzano hello **Aggiungi regola di avviso** o **Modifica regola di avviso** pagina.  Hello le tabelle seguenti vengono descritti i campi di hello in questa schermata.

![Regola di avviso](media/log-analytics-alerts/add-alert-rule.png)

### <a name="alert-information"></a>Informazioni sull'avviso
Si tratta di impostazioni di base per la regola di avviso hello e crea gli avvisi di hello.

| Proprietà | Descrizione |
|:--- |:---|
| Nome | Univoco nome tooidentify hello regola di avviso. Questo nome è incluso in tutti gli avvisi creati dalla regola hello.  |
| Descrizione | Descrizione facoltativa della regola di avviso hello. |
| Severity |Livello di gravità di tutti gli avvisi creati da questa regola. |

### <a name="search-query-and-time-window"></a>Finestra della query di ricerca e dell'intervallo di tempo
finestra di query e l'ora di ricerca Hello che restituisce record hello che vengono valutate toodetermine se tutti gli avvisi devono essere creati.

| Proprietà | Descrizione |
|:--- |:---|
| Query di ricerca | Si tratta di query hello che verranno eseguite.  record Hello restituito dalla query, sarà usato toodetermine se viene creato un avviso.<br><br>Selezionare **query di ricerca corrente utilizzare** toouse hello query corrente o selezionare una ricerca salvata dall'elenco hello esistente.  sintassi delle query Hello viene fornita nella casella di testo hello in cui è possibile modificarlo se necessario. |
| Intervallo di tempo |Specifica l'intervallo di tempo hello per query hello.  Hello query restituisce solo i record che sono stati creati all'interno dell'intervallo di hello ora corrente.  Può essere un valore qualsiasi compreso tra 5 minuti e 24 ore.  Deve essere maggiore o uguale toohello avviso frequenza.  <br><br> Ad esempio, se hello finestra è impostata too60 minuti e query hello esecuzione 1:15 PM, verranno restituiti solo i record creati tra 12:15 PM e 1:15 PM. |

Quando si specifica l'intervallo di tempo hello per regola di avviso hello, verrà visualizzato il numero di hello dei record esistenti che soddisfano i criteri di ricerca hello per tale intervallo di tempo.  Questo può aiutare a determinare la frequenza di hello in grado di offrire hello numero di risultati previsti.

### <a name="schedule"></a>Pianificazione
Definisce la frequenza con cui hello query di ricerca viene eseguita.

| Proprietà | Descrizione |
|:--- |:---|
| Frequenza di avviso | Specifica la frequenza con cui hello è necessario eseguire query. Può essere un valore qualsiasi compreso tra 5 minuti e 24 ore. Deve essere uguale tooor minore di intervallo di tempo hello.  Se il valore di hello è maggiore di intervallo di tempo hello, si rischia record viene ignorato.<br><br>Si considerino ad esempio un intervallo di tempo di 30 minuti e una frequenza pari a 60 minuti.  Se l'esecuzione di query di hello 1:00, restituisce i record compresi tra 12:30 e 1:00 PM.  Hello successivo hello verrebbe eseguita è 2:00 quando il risultato restituito sarebbe i record compresi tra 1:30 alle 2:00.  Qualsiasi record creato tra le 13:00 e 13:30 non verrà mai valutato. |


### <a name="generate-alert-based-on"></a>Genera l'avviso in base a
Definisce i criteri che verranno valutate rispetto ai risultati di hello di hello toodetermine query di ricerca se un avviso devono essere creati hello.  Questi dettagli saranno diversi a seconda della regola di avviso che si seleziona tipo di hello.  È possibile ottenere i dettagli per hello tipi di regola di avviso diversa da [informazioni sugli avvisi nel registro Analitica](log-analytics-alerts.md).

| Proprietà | Descrizione |
|:--- |:---|
| Elimina avvisi | Quando si attiva la soppressione per la regola di avviso hello, azioni per la regola hello sono disabilitate per un periodo di tempo dopo la creazione di un nuovo avviso definito. regola di Hello è ancora in esecuzione e verrà creato il record di avviso se viene soddisfatto il criterio di hello. Si tratta di tooallow tempo problema hello toocorrect senza eseguire azioni duplicate. |

#### <a name="number-of-results-alert-rules"></a>Regole di avviso Numero di risultati

| Proprietà | Descrizione |
|:--- |:---|
| Numero di risultati |Viene creato un avviso se il numero di hello di record restituiti dalla query hello **maggiore** o **minore** hello valore fornito.  |

#### <a name="metric-measurement-alert-rules"></a>Regole di avviso Unità di misura della metrica

| Proprietà | Descrizione |
|:--- |:---|
| Valore di aggregazione | Il valore di soglia che ogni valore di aggregazione nei risultati di hello deve superare toobe considerato una violazione di sicurezza. |
| Attiva l'avviso in base a | numero di Hello di violazioni della sicurezza per un avviso toobe creato.  È possibile specificare **totale di violazioni della sicurezza** per qualsiasi combinazione di violazioni della sicurezza tra i risultati di hello impostato o **violazioni consecutivi** toorequire che hello violazioni deve trovarsi in campioni consecutivi. |

### <a name="actions"></a>Azioni
Le regole di avviso creerà sempre un [avviso record](#alert-records) quando viene raggiunta la soglia di hello.  È inoltre possibile definire uno o più risposte toobe eseguire, ad esempio l'invio di un messaggio di posta elettronica o l'avvio di un runbook.



#### <a name="email-actions"></a>Azioni di posta elettronica
Azioni di posta elettronica Invia messaggio di posta elettronica con i dettagli di hello di hello avviso tooone o altri destinatari.

| Proprietà | Descrizione |
|:--- |:---|
| Notifica tramite posta elettronica |Specificare **Sì** se si desidera toobe un messaggio di posta elettronica inviati quando viene attivato l'avviso hello. |
| Oggetto |Nel messaggio di posta elettronica hello del soggetto.  È possibile modificare il corpo di hello del messaggio di posta elettronica hello. |
| Destinatari |Indirizzi di tutti i destinatari di posta elettronica.  Se si specifica più di un indirizzo, quindi gli indirizzi di hello separato con un punto e virgola (;). |

#### <a name="webhook-actions"></a>Azioni webhook
Le azioni Webhook consentono tooinvoke un processo esterno tramite una singola richiesta HTTP POST.

| Proprietà | Descrizione |
|:--- |:---|
| webhook |Specificare **Sì** se si desidera un webhook toocall quando viene attivato l'avviso hello. |
| URL webhook |Hello l'URL del webhook hello. |
| Includi payload JSON personalizzato |Selezionare questa opzione se si desidera che i payload di tooreplace hello predefinito con un payload personalizzato. |
| Specificare il payload JSON personalizzato |payload personalizzato di Hello per hello webhook.  Per informazioni dettagliate, vedere la sezione precedente. |

#### <a name="runbook-actions"></a>Azioni runbook
Le azioni runbook avviano un runbook in Automazione di Azure. 

>[!NOTE]
> È necessario disporre di soluzione di automazione hello installato nell'area di lavoro per questo toobe azione attivata. 


| Proprietà | Descrizione |
|:--- |:---|
| Runbook | Specificare **Sì** se si desidera toostart un runbook di automazione di Azure quando viene attivato l'avviso hello.  |
| Account di Automazione | Specifica l'account di automazione runbook selezionati dall'hello.  Si tratta dell'account azione hello è collegata l'area di lavoro toohello. |
| Selezionare un runbook | Selezionare hello runbook che si desidera toostart quando viene creato un avviso. |
| Esegui in | Selezionare **Azure** toorun hello runbook nel cloud hello.  Selezionare **worker ibrido** toorun hello runbook su un agente con [Runbook Worker ibrido](../automation/automation-hybrid-runbook-worker.md ) installato.  |




## <a name="next-steps"></a>Passaggi successivi
* Installare hello [soluzione Alert Management](log-analytics-solution-alert-management.md) avvisi tooanalyze creati nel Log Analitica con avvisi raccolti da System Center Operations Manager (SCOM).
* Altre informazioni sulle [ricerche nei log](log-analytics-log-searches.md) che possono generare avvisi.
* Completare una procedura dettagliata per la [configurazione di un webhook](log-analytics-alerts-webhooks.md) con una regola di avviso.  
* Informazioni su come toowrite [i runbook in automazione di Azure](https://azure.microsoft.com/documentation/services/automation) tooremediate problemi identificati tramite gli avvisi.

