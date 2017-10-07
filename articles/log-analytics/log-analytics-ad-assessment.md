---
title: aaaOptimize l'ambiente Active Directory con Azure Log Analitica | Documenti Microsoft
description: "È possibile utilizzare hello Active Directory Assessment tooassess soluzione hello rischio e l'integrità degli ambienti server a intervalli regolari."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 81eb41b8-eb62-4eb2-9f7b-fde5c89c9b47
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 63290d95302a9e1d243cd993ac50556ed42b97bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-active-directory-environment-with-hello-active-directory-assessment-solution-in-log-analytics"></a>Ottimizzare l'ambiente Active Directory con hello soluzione Active Directory Assessment in Log Analitica

![Simbolo di Valutazione AD](./media/log-analytics-ad-assessment/ad-assessment-symbol.png)

È possibile utilizzare hello Active Directory Assessment tooassess soluzione hello rischio e l'integrità degli ambienti server a intervalli regolari. In questo articolo consente di installare e utilizzare soluzioni hello in modo che sia possibile eseguire azioni correttive per problemi potenziali.

Questa soluzione fornisce un elenco di infrastruttura distribuita dei server di indicazioni specifiche tooyour priorità. Hello raccomandazioni vengono classificate in stato attivo di quattro aree, che consentono di rapidamente comprendere hello rischio e intraprendere l'azione.

Hello indicazioni si basano sulla conoscenza hello e l'esperienza acquisite dai tecnici Microsoft migliaia di visite dei clienti. Ogni raccomandazione fornisce informazioni aggiuntive sui motivi per cui un problema potrebbe essere rilevante tooyou e come tooimplement hello suggerite modifiche.

È possibile scegliere le aree di interesse più importanti tooyour organizzazione e tenere traccia dello stato di avanzamento verso la realizzazione di un ambiente integro ed esente da rischi.

Dopo aver aggiunto la soluzione hello e una valutazione è completato, riepilogo vengono visualizzate informazioni per aree di interesse in hello **AD Assessment** dashboard per l'infrastruttura di hello nell'ambiente in uso. Hello nelle sezioni seguenti descrivono come toouse hello informazioni su hello **AD Assessment** dashboard, in cui è possibile visualizzare e quindi intraprendere le azioni consigliate per l'infrastruttura di server di Active Directory.

![immagine del riquadro  SQL Assessment](./media/log-analytics-ad-assessment/ad-tile.png)

![Immagine del dashboard SQL Assessment ](./media/log-analytics-ad-assessment/ad-assessment.png)

## <a name="installing-and-configuring-hello-solution"></a>Installazione e configurazione di soluzione hello
Utilizzare hello tooinstall le informazioni seguenti e configurare soluzioni hello.

* Installare gli agenti nei controller di dominio che sono membri di hello dominio toobe valutata.
* Hello Active Directory Assessment soluzione richiede una versione supportata di .NET Framework 4 (4.5.2 o versione successiva) installato in ogni computer che dispone di un agente OMS.
* Aggiungere hello Active Directory Assessment soluzione tooyour area di lavoro OMS da [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ADAssessmentOMS?tab=Overview) o tramite il processo di hello descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).  Non è richiesta alcuna ulteriore configurazione.

  > [!NOTE]
  > Dopo aver aggiunto la soluzione hello, file AdvisorAssessment.exe hello viene aggiunto tooservers con gli agenti. Dati di configurazione sono di lettura e quindi inviati servizio OMS toohello nel cloud hello per l'elaborazione. Logica è applicato toohello ha ricevuto dati e dati hello vengono registrati nel servizio cloud di hello.
  >
  >

## <a name="active-directory-assessment-data-collection-details"></a>Informazioni dettagliate sulla raccolta dei dati per Active Directory Assessment

Active Directory Assessment raccoglie i dati da hello seguenti origini usano agenti hello che è stata abilitata:

- Agenti di raccolta del Registro di sistema
- Agenti di raccolta LDAP
- .NET Framework
- Agenti di raccolta del registro eventi
- Active Directory Service Interfaces (ADSI)
- Windows PowerShell
- Agenti di raccolta dei dati di file
- Strumentazione gestione Windows (WMI)
- API dello strumento DCDIAG
- API di File Replication Service (NTFRS)
- Codice personalizzato in C#


Hello nella tabella seguente illustra i metodi di raccolta dati per gli agenti, se Operations Manager (SCOM) è obbligatorio e, come spesso i dati vengono raccolti da un agente.

| Piattaforma | Agente diretto | Agente SCOM | Archiviazione di Azure | SCOM obbligatorio? | Dati dell'agente SCOM inviati con il gruppo di gestione | frequenza della raccolta |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |7 giorni |

## <a name="understanding-how-recommendations-are-prioritized"></a>Informazioni sulla classificazione in ordine di priorità delle raccomandazioni
Ogni raccomandazione generata viene assegnato un valore di ponderazione che identifica hello importanza relativa della raccomandazione hello. Vengono visualizzate solo raccomandazioni più importanti di hello 10.

### <a name="how-weights-are-calculated"></a>Come vengono calcolate le ponderazioni
Le ponderazioni sono valori aggregati che si basano su tre fattori chiave:

* Hello *probabilità* che un problema identificato sia causa problemi. Una probabilità più elevata equivale tooa punteggio complessivamente maggiore per la raccomandazione hello.
* Hello *impatto* del problema di hello per l'organizzazione se causa effettivamente un problema. Un impatto più elevato equivale tooa punteggio complessivamente maggiore per la raccomandazione hello.
* Hello *sforzo* raccomandazione hello tooimplement richiesto. Un lavoro richiesto più elevato equivale tooa punteggio complessivamente inferiore per la raccomandazione hello.

Hello ponderazione per ogni raccomandazione è espressa come percentuale del punteggio totale hello disponibile per ogni area di interesse. Ad esempio, se una raccomandazione hello sicurezza e le aree di interesse conformità ha un punteggio pari al 5%, implementazione della raccomandazione aumenta la % di punteggio da 5 sicurezza e conformità complessiva.

### <a name="focus-areas"></a>Aree di interesse
**Sicurezza e conformità** : quest'area di interesse descrive raccomandazioni relative alle potenziali minacce e violazioni della sicurezza, ai criteri aziendali e ai requisiti di conformità tecnici, legali e normativi.

**Disponibilità e continuità aziendale** : quest'area di interesse descrive raccomandazioni relative alla disponibilità del servizio, alla resilienza dell'infrastruttura e alla protezione aziendale.

**Prestazioni e scalabilità** -questa area di interesse Mostra toohelp indicazioni dell'organizzazione infrastruttura IT aumento delle dimensioni, assicurarsi che soddisfi i requisiti delle prestazioni correnti dell'ambiente IT ed è in grado di toorespond toochanging necessità dell'infrastruttura.

**Aggiornamento, migrazione e distribuzione** - questa area di interesse Mostra toohelp indicazioni si esegue l'aggiornamento, eseguire la migrazione e distribuire l'infrastruttura esistente di Active Directory tooyour.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>È consigliabile mirare ottenere tooscore 100% in tutte le aree di interesse?
Non necessariamente. Hello indicazioni si basano sulla conoscenza hello e l'esperienza acquisite dai tecnici Microsoft attraverso migliaia di visite dei clienti. Tuttavia, non due infrastrutture di server sono hello uguali e raccomandazioni specifiche possono essere più o meno pertinenti tooyou. Ad esempio, alcune raccomandazioni sulla sicurezza potrebbero risultare meno pertinenti se le macchine virtuali non sono esposto toohello Internet. Alcune raccomandazioni sulla disponibilità possono risultare meno pertinenti per i servizi che forniscono creazione di report e raccolta dei dati ad hoc a bassa priorità. I problemi che azienda collaudata tooa importante potrebbero essere meno importante tooa avvio. È possibile desidera tooidentify quali aree di interesse sono le priorità e quindi osservare il cambiamento i punteggi nel tempo.

Ogni raccomandazione include informazioni aggiuntive sui motivi per cui potrebbe essere importante. Se l'implementazione hello raccomandazione è appropriata, data la natura hello delle esigenze di business hello e servizi IT dell'organizzazione, è consigliabile utilizzare tooevaluate questa Guida.

## <a name="use-assessment-focus-area-recommendations"></a>Usare le raccomandazioni relative all'area di interesse della valutazione
Prima di poter utilizzare una soluzione antimalware in OMS, è necessario disporre di soluzione hello installata. tooread più sull'installazione di soluzioni, vedere [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md). Dopo l'installazione, è possibile visualizzare il riepilogo di hello delle raccomandazioni usando il riquadro Assessment hello nella pagina di panoramica hello in OMS.

Hello visualizzazione Riepilogo valutazione di conformità per l'infrastruttura, quindi analizzare i consigli.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>indicazioni tooview per lo stato attivo per area e intraprendere azione correttiva
1. In hello **Panoramica** pagina, fare clic su hello **valutazione** riquadro per l'infrastruttura server.
2. In hello **valutazione** pagina, esaminare le informazioni di riepilogo hello in uno dei pannelli di area hello lo stato attivo e quindi fare clic su uno tooview indicazioni di interesse.
3. In una delle pagine relative alle aree di hello lo stato attivo, è possibile visualizzare raccomandazioni hello priorità per l'ambiente. Fare clic su una raccomandazione in **Affected Objects** tooview dettagli sul motivo per cui hello è stata generata.  
    ![immagine delle raccomandazioni di Assessment (Valutazione)](./media/log-analytics-ad-assessment/ad-focus.png)
4. È possibile eseguire le azioni correttive suggerite in **Suggested Actions**(Azioni suggerite). Quando è stato risolto l'elemento hello, record le valutazioni successive che le azioni consigliate sono state effettuate e il punteggio relativo alla conformità aumenterà. Gli elementi corretti vengono visualizzati come **Passed Objects**.

## <a name="ignore-recommendations"></a>Ignorare le raccomandazioni
Se sono disponibili raccomandazioni che si desidera tooignore, è possibile creare un file di testo che verrà usato da OMS indicazioni tooprevent vengano visualizzati nei risultati della valutazione.

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>indicazioni tooidentify che verranno ignorata
1. Accedi tooyour dell'area di lavoro e aprire ricerca dei registri. Utilizzare hello seguendo i consigli toolist query non riuscite per i computer nell'ambiente.

   ```
   Type=ADAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi hello sopra query modificherebbe toohello seguente.
>
> `ADAssessmentRecommendation | where RecommendationResult == "Failed" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

   Ecco una query di ricerca nei Log di cattura di schermata hello: ![non riuscito di indicazioni](./media/log-analytics-ad-assessment/ad-failed-recommendations.png)
2. Scegliere le raccomandazioni che si desidera tooignore. Si useranno i valori hello per RecommendationId nella procedura descritta di seguito hello.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate e utilizzare un file di testo IgnoreRecommendations.txt
1. Creare un file denominato IgnoreRecommendations.txt.
2. Incollare o digitare ogni RecommendationId per ogni raccomandazione che si desidera tooignore Analitica di Log in una riga separata e quindi salvare e chiudere file hello.
3. Inserire file hello nella seguente cartella su ogni computer in cui si desidera indicazioni tooignore OMS hello.
   * Nei computer con Microsoft Monitoring Agent (connesso direttamente attraverso Operations Manager) - hello *SystemDrive*: \Programmi\Microsoft Monitoring Agent\Agent
   * Nel server di gestione di Operations Manager hello - *SystemDrive*: \Programmi\Microsoft System Center 2012 R2\Operations Manager\Server

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify che le raccomandazioni vengano ignorate
Dopo aver eseguito hello valutazione pianificata successiva, per impostazione predefinita ogni 7 giorni, hello specifica indicazioni sono contrassegnate *ignorato* e non verranno visualizzati nel dashboard di valutazione di hello.

1. È possibile utilizzare hello toolist query di ricerca nei Log seguente tutte le indicazioni hello ignorato.

    ```
    Type=ADAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```
>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi hello sopra query modificherebbe toohello seguente.
>
> `ADAssessmentRecommendation | where RecommendationResult == "Ignored" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

2. Se in seguito si decide che si desidera indicazioni toosee ignorate, rimuovere eventuali file IgnoreRecommendations.txt oppure rimuovere i Recommendationid dagli stessi.

## <a name="ad-assessment-solutions-faq"></a>Domande frequenti sulle soluzioni AD Assessment
*Con quale frequenza viene eseguita la valutazione?*

* valutazione Hello viene eseguita ogni 7 giorni.

*Esiste un modo tooconfigure la frequenza di esecuzione valutazione hello?*

* Attualmente non è possibile.

*Se viene rilevato un altro server dopo l'aggiunta della soluzione per la valutazione, il server verrà valutato?*

* Sì, a partire dal rilevamento verrà valutato ogni 7 giorni.

*Se viene rimosso un server, quando sarà rimosso dalla valutazione di hello?*

* Se un server non invia dati per 3 settimane, verrà rimosso.

*Che cos'è il nome di hello del processo di hello hello la raccolta dei dati?*

* AdvisorAssessment.exe

*Quanto tempo occorre per toobe dati raccolti?*

* raccolta di dati effettiva Hello Server hello richiede circa 1 ora. Potrebbe essere necessario più tempo nei server in cui è presente un numero elevato di server di Active Directory.

*Esiste un modo tooconfigure la raccolta dei dati?*

* Attualmente non è possibile.

*Perché vengono visualizzate solo hello prime 10 raccomandazioni?*

* Invece di esaminare un lunghissimo elenco completo delle attività, è consigliabile concentrare l'attenzione sulle raccomandazioni con priorità hello. Dopo la verifica delle raccomandazioni principali, verranno rese disponibili raccomandazioni aggiuntive. Se si preferisce toosee elenco dettagliato di hello, è possibile visualizzare tutte le indicazioni con ricerca di Log.

*Esiste un modo tooignore una raccomandazione?*

* Sì, vedere la sezione [Ignorare le raccomandazioni](#ignore-recommendations) sopra.

## <a name="next-steps"></a>Passaggi successivi
* Utilizzare [Accedi ricerche Log Analitica](log-analytics-log-searches.md) tooview dettagliato i dati di AD Assessment e indicazioni.
