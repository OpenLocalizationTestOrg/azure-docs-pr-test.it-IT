---
title: aaaOptimize dell'ambiente di SQL Server con Azure Log Analitica | Documenti Microsoft
description: "Con Azure Log Analitica, è possibile utilizzare hello SQL Assessment tooassess soluzione hello rischio e l'integrità degli ambienti SQL server a intervalli regolari."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f31326d8cdad3ef5d5a190614d1a18c1dac826ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-sql-server-environment-with-hello-sql-assessment-solution-in-log-analytics"></a>Ottimizzare l'ambiente di SQL Server con la soluzione SQL Assessment in Log Analitica hello

![Simbolo di Valutazione SQL](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

È possibile utilizzare hello SQL Assessment tooassess soluzione hello rischio e l'integrità degli ambienti server a intervalli regolari. In questo articolo consentirà di installare la soluzione hello in modo che sia possibile eseguire azioni correttive per problemi potenziali.

Questa soluzione fornisce un elenco di infrastruttura distribuita dei server di indicazioni specifiche tooyour priorità. Hello raccomandazioni vengono classificate in sei messa a fuoco aree in modo da aumentare rapidamente comprendere hello rischio e intraprendere l'azione correttiva.

raccomandazioni Hello fornite si basano sulla conoscenza hello e l'esperienza acquisite dai tecnici Microsoft migliaia di visite dei clienti. Ogni raccomandazione fornisce informazioni aggiuntive sui motivi per cui un problema potrebbe essere rilevante tooyou e come tooimplement hello suggerite modifiche.

È possibile scegliere le aree di interesse più importanti tooyour organizzazione e tenere traccia dello stato di avanzamento verso la realizzazione di un ambiente integro ed esente da rischi.

Dopo aver aggiunto la soluzione hello e una valutazione è completato, riepilogo vengono visualizzate informazioni per aree di interesse in hello **SQL Assessment** dashboard per l'infrastruttura di hello nell'ambiente in uso. Hello nelle sezioni seguenti descrivono come toouse hello informazioni su hello **SQL Assessment** dashboard, in cui è possibile visualizzare e quindi intraprendere le azioni consigliate per l'infrastruttura SQL server.

![immagine del riquadro  SQL Assessment](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![Immagine del dashboard SQL Assessment ](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-hello-solution"></a>Installazione e configurazione di soluzione hello
SQL Assessment funziona con tutte le versioni attualmente supportate di SQL Server per le edizioni Standard, Developer ed Enterprise di hello.

Utilizzare hello tooinstall le informazioni seguenti e configurare la soluzione hello.

* Nei server in cui è installato SQL Server devono essere installati gli agenti.
* Hello soluzione SQL Assessment richiede una versione supportata di .NET Framework 4 sia installato in ogni computer che dispone di un agente OMS.
* Nella soluzione di ordine tooinstall hello utente hello deve essere un toohello amministratore o collaboratore di sottoscrizione di Azure quando utilizzando hello portale di Azure. Inoltre, utente hello deve essere un membro di hello OMS workspace collaboratore o amministratore del ruolo nel portale OMS hello.
* Quando si usa l'agente di Operations Manager hello con SQL Assessment, è necessario un account di Operations Manager Run-As toouse. Per altre informazioni, vedere di seguito [Account RunAs di Operations Manager per OMS](#operations-manager-run-as-accounts-for-oms) .

  > [!NOTE]
  > agente MMA Hello non supporta gli account di Operations Manager Run-As.
  >
  >
* Aggiungere hello SQL Assessment soluzione tooyour all'area di lavoro OMS tramite il processo di hello [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md). Non è richiesta alcuna ulteriore configurazione.

> [!NOTE]
> Dopo aver aggiunto la soluzione hello, file AdvisorAssessment.exe hello viene aggiunto tooservers con gli agenti. Dati di configurazione sono di lettura e quindi inviati servizio OMS toohello nel cloud hello per l'elaborazione. Logica è applicato toohello ha ricevuto dati e dati hello vengono registrati nel servizio cloud di hello.

## <a name="sql-assessment-data-collection-details"></a>Informazioni dettagliate sulla raccolta dei dati di SQL Assessment
SQL Assessment raccoglie i dati WMI, dati del Registro di sistema, i dati sulle prestazioni e SQL Server DMV visualizzare i risultati utilizzando agenti hello che è stata abilitata.

Hello nella tabella seguente illustra i metodi di raccolta dati per gli agenti, se Operations Manager (SCOM) è obbligatorio e, come spesso i dati vengono raccolti da un agente.

| Piattaforma | Agente diretto | Agente SCOM | Archiviazione di Azure | SCOM obbligatorio? | Dati dell'agente SCOM inviati con il gruppo di gestione | frequenza della raccolta |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | &#8226; | &#8226; |  |  | &#8226; |7 giorni |

## <a name="operations-manager-run-as-accounts-for-oms"></a>Account RunAs di Operations Manager per OMS
Analitica di log in OMS Usa hello agente Operations Manager e gestione gruppo toocollect e invia servizio OMS toohello di dati. OMS si basa su management pack per i carichi di lavoro tooprovide servizi a valore aggiunto. Ogni carico di lavoro richiede privilegi specifici del carico di lavoro toorun management pack per in un contesto di sicurezza diverso, ad esempio un account di dominio. È necessario tooprovide le informazioni sulle credenziali configurando un account RunAs Operations Manager.

Utilizzare hello seguente informazioni tooset hello runas account di Operations Manager per la valutazione di SQL.

### <a name="set-hello-run-as-account-for-sql-assessment"></a>Impostare hello account RunAs per SQL assessment
 Se si usa già hello management pack di SQL Server, utilizzare l'account RunAs.

#### <a name="tooconfigure-hello-sql-run-as-account-in-hello-operations-console"></a>hello tooconfigure account RunAs di SQL nella console operatore hello
> [!NOTE]
> Se si utilizza hello OMS direttamente agente, anziché agente SCOM hello, management pack di hello viene sempre eseguito nel contesto di sicurezza hello di hello account sistema locale. 1-5 seguito ed eseguire i passaggi di Skip hello di esempio T-SQL o Powershell, specificando NT AUTHORITY\SYSTEM come nome utente hello.
>
>

1. In Operations Manager, aprire console operatore hello e quindi fare clic su **amministrazione**.
2. In **Esegui come configurazione**, fare clic su **Profili** e aprire **Profilo RunAs di OMS SQL Assessment**.
3. In hello **account RunAs** pagina, fare clic su **Aggiungi**.
4. Selezionare un account RunAs Windows che contiene le credenziali di hello necessarie per SQL Server oppure fare clic su **New** toocreate uno.

   > [!NOTE]
   > tipo di account RunAs Hello deve essere Windows. Hello account RunAs deve appartenere anche del gruppo di amministratori locali in tutti i server di Windows che ospita le istanze di SQL Server.
   >
   >
5. Fare clic su **Salva**.
6. Modificare ed eseguire hello seguente esempio T-SQL in tooRun di obbligatorio ogni istanza di SQL Server toogrant autorizzazioni minime tooperform come Account SQL Assessment. Tuttavia, non è necessario toodo questo se un Account runas fa già parte del server sysadmin hello in istanze di SQL Server.

```
---
    -- Replace <UserName> with hello actual user name being used as Run As Account.
    USE master

    -- Create login for hello user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions toouser.
    GRANT VIEW SERVER STATE too[<UserName>]
    GRANT VIEW ANY DEFINITION too[<UserName>]
    GRANT VIEW ANY DATABASE too[<UserName>]

    -- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
    -- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="tooconfigure-hello-sql-run-as-account-using-windows-powershell"></a>hello tooconfigure account RunAs di SQL usando Windows PowerShell
Aprire una finestra di PowerShell ed eseguire lo script seguente dopo averlo aggiornato con le informazioni di hello:

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a>Informazioni sulla classificazione in ordine di priorità delle raccomandazioni
Ogni raccomandazione generata viene assegnato un valore di ponderazione che identifica hello importanza relativa della raccomandazione hello. Vengono visualizzati solo hello dieci raccomandazioni più importanti.

### <a name="how-weights-are-calculated"></a>Come vengono calcolate le ponderazioni
Le ponderazioni sono valori aggregati che si basano su tre fattori chiave:

* Hello *probabilità* che un problema identificato causi inconvenienti. Una probabilità più elevata equivale tooa punteggio complessivamente maggiore per la raccomandazione hello.
* Hello *impatto* del problema di hello per l'organizzazione se causa effettivamente un problema. Un impatto più elevato equivale tooa punteggio complessivamente maggiore per la raccomandazione hello.
* Hello *sforzo* raccomandazione hello tooimplement richiesto. Un lavoro richiesto più elevato equivale tooa punteggio complessivamente inferiore per la raccomandazione hello.

Hello ponderazione per ogni raccomandazione è espressa come percentuale del punteggio totale hello disponibile per ogni area di interesse. Ad esempio, se una raccomandazione hello sicurezza e le aree di interesse conformità ha un punteggio pari al 5%, implementazione della raccomandazione aumenterà il complessivo Security and Compliance punteggio da 5.

### <a name="focus-areas"></a>Aree di interesse
**Sicurezza e conformità** : quest'area di interesse descrive raccomandazioni relative alle potenziali minacce e violazioni della sicurezza, ai criteri aziendali e ai requisiti di conformità tecnici, legali e normativi.

**Disponibilità e continuità aziendale** : quest'area di interesse descrive raccomandazioni relative alla disponibilità del servizio, alla resilienza dell'infrastruttura e alla protezione aziendale.

**Prestazioni e scalabilità** -questa area di interesse Mostra toohelp indicazioni dell'organizzazione infrastruttura IT aumento delle dimensioni, assicurarsi che soddisfi i requisiti delle prestazioni correnti dell'ambiente IT ed è in grado di toorespond toochanging necessità dell'infrastruttura.

**Aggiornamento, migrazione e distribuzione** - questa area di interesse Mostra toohelp indicazioni si esegue l'aggiornamento, eseguire la migrazione e distribuire l'infrastruttura esistente di SQL Server tooyour.

**Operazioni e monitoraggio** : questa area di interesse viene semplificata toohelp indicazioni operazioni IT e implementare manutenzione preventiva e ottimizzare le prestazioni.

**Modifica e la gestione della configurazione** -questa area di interesse di seguito vengono fornite indicazioni toohelp proteggere le operazioni quotidiane, verificare che le modifiche non interessano l'infrastruttura con negativamente, stabilire procedure di controllo modifiche e tootrack e controllo configurazioni di sistema.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>È consigliabile mirare ottenere tooscore 100% in tutte le aree di interesse?
Non necessariamente. Hello indicazioni si basano sulla conoscenza hello e l'esperienza acquisite dai tecnici Microsoft attraverso migliaia di visite dei clienti. Tuttavia, non due infrastrutture di server sono hello uguali e raccomandazioni specifiche possono essere più o meno pertinenti tooyou. Ad esempio, alcune raccomandazioni sulla sicurezza potrebbero risultare meno pertinenti se le macchine virtuali non sono esposto toohello Internet. Alcune raccomandazioni sulla disponibilità possono risultare meno pertinenti per i servizi che forniscono creazione di report e raccolta dei dati ad hoc a bassa priorità. I problemi che azienda collaudata tooa importante potrebbero essere meno importante tooa avvio. È possibile desidera tooidentify quali aree di interesse sono le priorità e quindi osservare il cambiamento i punteggi nel tempo.

Ogni raccomandazione include informazioni aggiuntive sui motivi per cui potrebbe essere importante. Se l'implementazione hello raccomandazione è appropriata, data la natura hello delle esigenze di business hello e servizi IT dell'organizzazione, è consigliabile utilizzare tooevaluate questa Guida.

## <a name="use-assessment-focus-area-recommendations"></a>Usare le raccomandazioni relative all'area di interesse della valutazione
Prima di poter utilizzare una soluzione antimalware in OMS, è necessario disporre di soluzione hello installata. tooread più sull'installazione di soluzioni, vedere [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md). Dopo l'installazione, è possibile visualizzare il riepilogo di hello delle raccomandazioni usando il riquadro SQL Assessment hello nella pagina di panoramica hello in OMS.

Hello visualizzazione Riepilogo valutazione di conformità per l'infrastruttura, quindi analizzare i consigli.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>indicazioni tooview per lo stato attivo per area e intraprendere azione correttiva
1. In hello **Panoramica** pagina, fare clic su hello **SQL Assessment** riquadro.
2. In hello **SQL Assessment** pagina, esaminare le informazioni di riepilogo hello in uno dei pannelli di area hello lo stato attivo e quindi fare clic su uno tooview indicazioni di interesse.
3. In una delle pagine relative alle aree di hello lo stato attivo, è possibile visualizzare raccomandazioni hello priorità per l'ambiente. Fare clic su una raccomandazione in **Affected Objects** tooview dettagli sul motivo per cui hello è stata generata.  
    ![immagine delle raccomandazioni di SQL Assessment](./media/log-analytics-sql-assessment/sql-assess-focus.png)
4. È possibile eseguire le azioni correttive suggerite in **Suggested Actions**(Azioni suggerite). Quando l'elemento hello è stato risolto, le valutazioni successive indicheranno che le azioni eseguite e il punteggio relativo alla conformità aumenterà consigliati. Gli elementi corretti vengono visualizzati come **Passed Objects**.

## <a name="ignore-recommendations"></a>Ignorare le raccomandazioni
Se sono disponibili raccomandazioni che si desidera tooignore, è possibile creare un file di testo che verrà usato da OMS indicazioni tooprevent vengano visualizzati nei risultati della valutazione.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>indicazioni tooidentify che verranno ignorata
1. Accedi tooyour dell'area di lavoro e aprire ricerca dei registri. Utilizzare hello seguendo i consigli toolist query non riuscite per i computer nell'ambiente.

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   Ecco una query di ricerca nei Log di cattura di schermata hello: ![non riuscito di indicazioni](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)
2. Scegliere le raccomandazioni che si desidera tooignore. Si useranno i valori hello per RecommendationId nella procedura descritta di seguito hello.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate e utilizzare un file di testo IgnoreRecommendations.txt
1. Creare un file denominato IgnoreRecommendations.txt.
2. Incollare o digitare ogni RecommendationId per ogni raccomandazione che si desidera OMS tooignore su una riga separata e quindi salvare e chiudere il file hello.
3. Inserire file hello nella seguente cartella su ogni computer in cui si desidera indicazioni tooignore OMS hello.
   * Nei computer con Microsoft Monitoring Agent (connesso direttamente attraverso Operations Manager) - hello *SystemDrive*: \Programmi\Microsoft Monitoring Agent\Agent
   * Nel server di gestione di Operations Manager hello - *SystemDrive*: \Programmi\Microsoft System Center 2012 R2\Operations Manager\Server

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify che le raccomandazioni vengano ignorate
1. Dopo aver eseguito hello valutazione pianificata successiva, per impostazione predefinita ogni 7 giorni, hello specifica indicazioni sono contrassegnate come ignorate e non verranno visualizzati nel dashboard di valutazione di hello.
2. È possibile utilizzare hello toolist query di ricerca nei Log seguente tutte le indicazioni hello ignorato.

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. Se in seguito si decide che si desidera indicazioni toosee ignorate, rimuovere eventuali file IgnoreRecommendations.txt oppure rimuovere i Recommendationid dagli stessi.

## <a name="sql-assessment-solution-faq"></a>Domande frequenti sulla soluzione SQL Assessment
*Con quale frequenza viene eseguita la valutazione?*

* valutazione Hello viene eseguita ogni 7 giorni.

*Esiste un modo tooconfigure la frequenza di esecuzione valutazione hello?*

* Attualmente non è possibile.

*Se non viene individuato un altro server dopo l'aggiunta hello soluzioni di valutazione di SQL, verrà valutato?*

* Sì, a partire dal rilevamento verrà valutato ogni 7 giorni.

*Se viene rimosso un server, quando sarà rimosso dalla valutazione di hello?*

* Se un server non invia dati per 3 settimane, verrà rimosso.

*Che cos'è il nome di hello del processo di hello hello la raccolta dei dati?*

* AdvisorAssessment.exe

*Quanto tempo occorre per toobe dati raccolti?*

* raccolta di dati effettiva Hello Server hello richiede circa 1 ora. È possibile che sia necessario più tempo nei server in cui è presente un numero elevato di istanze o database SQL.

*Quali tipi di dati vengono raccolti?*

* Hello seguenti tipi di dati viene raccolti:
  * WMI
  * Registro
  * Contatori delle prestazioni
  * DMV (Dynamic Management View) di SQL.

*Esiste un modo tooconfigure la raccolta dei dati?*

* Attualmente non è possibile.

*Motivo per cui è tooconfigure un Account runas?*

* Per un server SQL vengono eseguite alcune SQL. Affinché sia necessario utilizzare toorun, un Account RunAs con tooSQL autorizzazioni VIEW SERVER STATE.  Inoltre, in ordine tooquery WMI, sono necessarie credenziali di amministratore locale.

*Perché vengono visualizzate solo hello prime 10 raccomandazioni?*

* Invece di esaminare un lunghissimo elenco completo delle attività, è consigliabile concentrare l'attenzione sulle raccomandazioni con priorità hello. Dopo la verifica delle raccomandazioni principali, verranno rese disponibili raccomandazioni aggiuntive. Se si preferisce toosee elenco dettagliato di hello, è possibile visualizzare tutte le indicazioni con ricerca di log OMS hello.

*Esiste un modo tooignore una raccomandazione?*

* Sì, vedere la sezione [Ignorare le raccomandazioni](#ignore-recommendations) sopra.

## <a name="next-steps"></a>Passaggi successivi
* [Ricerca dei registri](log-analytics-log-searches.md) tooview dettagliate dati di valutazione di SQL e le indicazioni.
