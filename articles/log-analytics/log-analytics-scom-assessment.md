---
title: aaaOptimize l'ambiente System Center Operations Manager con Azure Log Analitica | Documenti Microsoft
description: "È possibile utilizzare hello System Center Operations Manager Assessment tooassess soluzione hello rischio e l'integrità degli ambienti server a intervalli regolari."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: tysonn
ms.assetid: 49aad8b1-3e05-4588-956c-6fdd7715cda1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c024e53826e91524c120bdb98ae7d96d6dc37d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-environment-with-hello-system-center-operations-manager-assessment-preview-solution"></a>Ottimizzare l'ambiente con hello soluzioni di System Center Operations Manager Assessment (anteprima)

![Simbolo di Valutazione System Center Operations Manager](./media/log-analytics-scom-assessment/scom-assessment-symbol.png)

È possibile utilizzare hello System Center Operations Manager Assessment tooassess soluzione hello rischio e l'integrità degli ambienti server System Center Operations Manager a intervalli regolari. In questo articolo consente di installare, configurare e utilizzare soluzioni hello in modo che sia possibile eseguire azioni correttive per problemi potenziali.

Questa soluzione fornisce un elenco di infrastruttura distribuita dei server di indicazioni specifiche tooyour priorità. Hello raccomandazioni vengono classificate in stato attivo di quattro aree, che consentono di rapidamente comprendere hello rischio e intraprendere azioni correttive.

raccomandazioni Hello fornite si basano sulla conoscenza hello e l'esperienza acquisite dai tecnici Microsoft migliaia di visite dei clienti. Ogni raccomandazione fornisce informazioni aggiuntive sui motivi per cui un problema potrebbe essere rilevante tooyou e come tooimplement hello suggerite modifiche.

È possibile scegliere le aree di interesse più importanti tooyour organizzazione e tenere traccia dello stato di avanzamento verso la realizzazione di un ambiente integro ed esente da rischi.

Dopo aver aggiunto la soluzione hello e una valutazione è completato, riepilogo vengono visualizzate informazioni per aree di interesse in hello **System Center Operations Manager Assessment** dashboard per l'infrastruttura. Hello nelle sezioni seguenti descrivono come toouse hello informazioni su hello **System Center Operations Manager Assessment** dashboard, in cui è possibile visualizzare e quindi intraprendere le azioni consigliate per l'infrastruttura SCOM.

![Riquadro della soluzione System Center Operations Manager](./media/log-analytics-scom-assessment/scom-tile.png)

![Dashboard di System Center Operations Manager Assessment](./media/log-analytics-scom-assessment/scom-dashboard01.png)

## <a name="installing-and-configuring-hello-solution"></a>Installazione e configurazione di soluzione hello

soluzione Hello funziona con Microsoft System Operations Manager 2012 R2 e 2012 SP1.

Utilizzare hello tooinstall le informazioni seguenti e configurare la soluzione hello.

 - Prima di poter utilizzare una soluzione antimalware in OMS, è necessario disporre di soluzione hello installata. Installare la soluzione hello da [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) o seguendo le istruzioni hello [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).

 - Dopo l'aggiunta dell'area di lavoro di hello soluzione toohello, riquadro di valutazione di System Center Operations Manager hello nel dashboard di hello Visualizza messaggio di richiesta di configurazione aggiuntive di hello. Fare clic sul riquadro hello e seguire i passaggi di configurazione hello indicati nella pagina hello

 ![Riquadro del dashboard di System Center Operations Manager](./media/log-analytics-scom-assessment/scom-configrequired-tile.png)

 Configurazione di hello System Center Operations Manager può essere eseguita tramite script hello seguendo i passaggi di hello indicati nella pagina di configurazione hello della soluzione hello in OMS.

 Al contrario, valutazione hello tooconfigure attraverso la Console di SCOM, seguire hello seguente di passaggi di hello stesso ordine
1. [Impostare l'account RunAs hello per la valutazione di System Center Operations Manager](#operations-manager-run-as-accounts-for-oms)  
2. [Configurare la regola di valutazione di System Center Operations Manager hello](#configure-the-assessment-rule)

## <a name="system-center-operations-manager-assessment-data-collection-details"></a>Dettagli della raccolta di dati della valutazione di System Center Operations Manager

Hello valutazione di System Center Operations Manager raccoglie i dati WMI, dati del Registro di sistema, dati registro eventi, dati di Operations Manager tramite Windows PowerShell, le query SQL, raccolta di informazioni File utilizza un server hello che è stata abilitata.

Hello nella tabella seguente illustra i metodi di raccolta dati per System Center Operations Manager Assessment e la frequenza con cui vengono raccolti dati da un agente.

| Piattaforma | Agente diretto | Agente SCOM | Archiviazione di Azure | SCOM obbligatorio? | Dati dell'agente SCOM inviati con il gruppo di gestione | frequenza della raccolta |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | | | | &#8226; | | 7 giorni |

## <a name="operations-manager-run-as-accounts-for-oms"></a>Account RunAs di Operations Manager per OMS

OMS si basa sui management pack per i carichi di lavoro tooprovide servizi a valore aggiunto. Ogni carico di lavoro richiede privilegi specifici del carico di lavoro toorun management pack per in un contesto di sicurezza diverso, ad esempio un account di dominio. Configurare un runas Operations Manager account tooprovide informazioni sulle credenziali.

Utilizzare le seguenti informazioni tooset hello account RunAs di Operations Manager per System Center Operations Manager Assessment hello.

### <a name="set-hello-run-as-account"></a>Set hello account RunAs

1. Nella Console di Operations Manager hello, passare toohello **amministrazione** scheda.
2. In hello **configurazione runas**, fare clic su **account**.
3. Creare Account runas, seguenti tramite procedura guidata, la creazione di un account di Windows hello hello. toouse account Hello è hello quello identificato e con tutti i prerequisiti di hello indicati di seguito:

    >[!NOTE]
    Hello account RunAs deve soddisfare i requisiti seguenti:
    - Un membro di account di dominio del gruppo Administrators locale hello in tutti i server nell'ambiente di hello (tutte le operazioni di gestione ruoli - Server di gestione, Database di Operations Manager, Data Warehouse, report, Console Web, Gateway)
    - Ruolo di amministratore di Manager di operazione per il gruppo di gestione hello valutato
    - Eseguire hello [script](#sql-script-to-grant-granular-permissions-to-the-run-as-account) account toohello di autorizzazioni granulari toogrant nell'istanza di SQL Server usato da Operations Manager.
      Nota: Se l'account con diritti sysadmin già, ignorare l'esecuzione dello script hello.

4. In **Sicurezza della distribuzione** selezionare **Più protetto**.
5. Specificare il server di gestione hello in cui è distribuito account hello.
3. Tornare indietro toohello configurazione runas e fare clic su **profili**.
4. Ricerca di hello *profilo Assessment SCOM*.
5. nome del profilo Hello deve essere: *Microsoft System Center Advisor SCOM valutazione profilo runas*.
6. Pulsante destro del mouse e aggiornare le relative proprietà e aggiungere hello di recente creata Account runas creato nel passaggio 3.

### <a name="sql-script-toogrant-granular-permissions-toohello-run-as-account"></a>SQL script toogrant autorizzazioni granulari toohello account RunAs

Eseguire hello seguente SQL script toogrant necessarie autorizzazioni toohello account RunAs nell'istanza di SQL Server hello usato da Operations Manager.

```
-- Replace <UserName> with hello actual user name being used as Run As Account.
USE master

-- Create login for hello user, comment this line if login is already created.
CREATE LOGIN [UserName] FROM WINDOWS


--GRANT permissions toouser.
GRANT VIEW SERVER STATE too[UserName]
GRANT VIEW ANY DEFINITION too[UserName]
GRANT VIEW ANY DATABASE too[UserName]

-- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
-- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
EXEC sp_msforeachdb N'USE [?]; CREATE USER [UserName] FOR LOGIN [UserName];'

Use msdb
GRANT SELECT too[UserName]
Go

--Give SELECT permission on all Operations Manager related Databases

--Replace hello Operations Manager database name with hello one in your environment
Use [OperationsManager];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager DatawareHouse database name with hello one in your environment
Use [OperationsManagerDW];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager Audit Collection database name with hello one in your environment
Use [OperationsManagerAC];
GRANT SELECT too[UserName]
GO

--Give db_owner on [OperationsManager] DB
--Replace hello Operations Manager database name with hello one in your environment
USE [OperationsManager]
GO
ALTER ROLE [db_owner] ADD MEMBER [UserName]

```


### <a name="configure-hello-assessment-rule"></a>Configurare la regola di valutazione di hello

Valutazione di System Center Operations Manager management pack di soluzione include una regola denominata Hello *Microsoft System Center Advisor SCOM valutazione eseguire valutazione regola*. Questa regola è responsabile per l'esecuzione di valutazione di hello. tooenable hello regola e configurare la frequenza di hello, utilizzare hello procedure seguenti.

Per impostazione predefinita, hello Microsoft System Center Advisor SCOM valutazione eseguire valutazione regola è disabilitata. valutazione hello toorun, è necessario abilitare la regola hello in un server di gestione. Utilizzare hello alla procedura seguente.

#### <a name="enable-hello-rule-for-a-specific-management-server"></a>Abilitare la regola di hello per un server di gestione specifico

1. In hello **Authoring** area di lavoro della console di Operations Manager hello, cercare la regola hello *Microsoft System Center Advisor SCOM valutazione eseguire valutazione regola* in hello **regole** riquadro.
2. Nei risultati della ricerca hello, che include testo hello hello selezionare *tipo: Server di gestione*.
3. Fare clic sulla regola hello e quindi fare clic su **esegue l'override** > **per un oggetto specifico della classe: Server di gestione**.
4.  Nell'elenco di server di gestione disponibili hello, selezionare il server di gestione hello in cui si desidera eseguire regola hello.
5.  È necessario modificare il valore di sostituzione troppo**True** per hello **abilitato** valore del parametro.  
    ![parametro di override](./media/log-analytics-scom-assessment/rule.png)

In questa finestra, configurare la frequenza di hello di hello eseguita utilizzando la procedura successiva hello.

#### <a name="configure-hello-run-frequency"></a>Configurare la frequenza di esecuzione hello

valutazione Hello è l'intervallo predefinito di hello toorun configurato ogni 10.080 minuti (o sette giorni). È possibile eseguire l'override di hello valore tooa minimo valore 1440 minuti (o un giorno). valore Hello rappresenta l'intervallo di tempo minimo hello necessaria tra le esecuzioni successive di valutazione. intervallo di hello toooverride, utilizzare hello passaggi riportati di seguito.

1. In hello **Authoring** area di lavoro della console di Operations Manager hello, cercare la regola hello *Microsoft System Center Advisor SCOM valutazione eseguire valutazione regola* in hello **regole** riquadro.
2. Nei risultati della ricerca hello, che include testo hello hello selezionare *tipo: Server di gestione*.
3. Fare clic sulla regola hello e quindi fare clic su **hello Override regola** > **per tutti gli oggetti della classe: Server di gestione**.
4. Hello modifica **intervallo** tooyour valore di parametro desiderato il valore dell'intervallo. Nel seguente esempio hello hello è impostato too1440 minuti (un giorno).  
    ![parametro interval](./media/log-analytics-scom-assessment/interval.png)  
    Se il valore di hello è impostato tooless 1440 minuti, regola hello viene eseguito in un intervallo di un giorno. In questo esempio hello regola ignora il valore dell'intervallo hello e una frequenza di un giorno.


## <a name="understanding-how-recommendations-are-prioritized"></a>Informazioni sulla classificazione in ordine di priorità delle raccomandazioni

Ogni raccomandazione generata viene assegnato un valore di ponderazione che identifica hello importanza relativa della raccomandazione hello. Vengono visualizzate solo raccomandazioni più importanti di hello 10.

### <a name="how-weights-are-calculated"></a>Come vengono calcolate le ponderazioni

Le ponderazioni sono valori aggregati che si basano su tre fattori chiave:

- Hello *probabilità* che un problema identificato causi inconvenienti. Una probabilità più elevata equivale tooa punteggio complessivamente maggiore per la raccomandazione hello.
- Hello *impatto* del problema di hello per l'organizzazione se causa effettivamente un problema. Un impatto più elevato equivale tooa punteggio complessivamente maggiore per la raccomandazione hello.
- Hello *sforzo* raccomandazione hello tooimplement richiesto. Un lavoro richiesto più elevato equivale tooa punteggio complessivamente inferiore per la raccomandazione hello.

Hello ponderazione per ogni raccomandazione è espressa come percentuale del punteggio totale hello disponibile per ogni area di interesse. Ad esempio, se una raccomandazione nell'area di interesse di disponibilità e continuità aziendale hello ha un punteggio pari al 5%, implementazione della raccomandazione aumenta la % di punteggio da 5 disponibilità e continuità aziendale complessivo.

### <a name="focus-areas"></a>Aree di interesse

**Disponibilità e continuità aziendale** : quest'area di interesse descrive raccomandazioni relative alla disponibilità del servizio, alla resilienza dell'infrastruttura e alla protezione aziendale.

**Prestazioni e scalabilità** -questa area di interesse Mostra toohelp indicazioni dell'organizzazione infrastruttura IT aumento delle dimensioni, assicurarsi che soddisfi i requisiti delle prestazioni correnti dell'ambiente IT ed è in grado di toorespond toochanging necessità dell'infrastruttura.

**L'aggiornamento, migrazione e distribuzione** - questa area di interesse Mostra toohelp indicazioni si esegue l'aggiornamento, eseguire la migrazione e distribuire l'infrastruttura esistente di SQL Server tooyour.

**Operazioni e monitoraggio** : questa area di interesse viene semplificata toohelp indicazioni operazioni IT e implementare manutenzione preventiva e ottimizzare le prestazioni.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>È consigliabile mirare ottenere tooscore 100% in tutte le aree di interesse?

Non necessariamente. Hello indicazioni si basano sulla conoscenza hello e l'esperienza acquisite dai tecnici Microsoft attraverso migliaia di visite dei clienti. Tuttavia, non due infrastrutture di server sono hello uguali e raccomandazioni specifiche possono essere più o meno pertinenti tooyou. Ad esempio, alcune raccomandazioni sulla sicurezza potrebbero risultare meno pertinenti se le macchine virtuali non sono esposto toohello Internet. Alcune raccomandazioni sulla disponibilità possono risultare meno pertinenti per i servizi che forniscono creazione di report e raccolta dei dati ad hoc a bassa priorità. I problemi che azienda collaudata tooa importante potrebbero essere meno importante tooa avvio. È possibile desidera tooidentify quali aree di interesse sono le priorità e quindi osservare il cambiamento i punteggi nel tempo.

Ogni raccomandazione include informazioni aggiuntive sui motivi per cui potrebbe essere importante. Utilizzare questo tooevaluate indicazioni se implementazione hello raccomandazione è appropriata, data la natura hello delle esigenze di business hello e servizi IT dell'organizzazione.

## <a name="use-assessment-focus-area-recommendations"></a>Usare le raccomandazioni relative all'area di interesse della valutazione

Prima di poter utilizzare una soluzione antimalware in OMS, è necessario disporre di soluzione hello installata. tooread più sull'installazione di soluzioni, vedere [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md). Dopo l'installazione, è possibile visualizzare il riepilogo di hello delle raccomandazioni usando il riquadro di valutazione di System Center Operations Manager hello nella pagina di panoramica hello in OMS.

Hello visualizzazione Riepilogo valutazione di conformità per l'infrastruttura, quindi analizzare i consigli.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>indicazioni tooview per lo stato attivo per area e intraprendere azione correttiva

1. In hello **Panoramica** pagina, fare clic su hello **System Center Operations Manager Assessment** riquadro.
2. In hello **System Center Operations Manager Assessment** pagina, esaminare le informazioni di riepilogo hello in uno dei pannelli di area hello lo stato attivo e quindi fare clic su uno tooview indicazioni di interesse.
3. In una delle pagine relative alle aree di hello lo stato attivo, è possibile visualizzare raccomandazioni hello priorità per l'ambiente. Fare clic su una raccomandazione in **Affected Objects** tooview dettagli sul motivo per cui hello è stata generata.  
    ![area di interesse](./media/log-analytics-scom-assessment/focus-area.png)
4. È possibile eseguire le azioni correttive suggerite in **Suggested Actions**(Azioni suggerite). Quando l'elemento hello è stato risolto, le valutazioni successive indicheranno che le azioni eseguite e il punteggio relativo alla conformità aumenterà consigliati. Gli elementi corretti vengono visualizzati come **Passed Objects**.

## <a name="ignore-recommendations"></a>Ignorare le raccomandazioni

Se sono disponibili raccomandazioni che si desidera tooignore, è possibile creare un file di testo che OMS Usa indicazioni tooprevent vengano visualizzati nei risultati della valutazione.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-want-tooignore"></a>indicazioni tooidentify che si desidera tooignore

1. Accedi tooyour dell'area di lavoro e aprire ricerca dei registri. Utilizzare hello seguendo i consigli toolist query non riuscite per i computer nell'ambiente.

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

    Ecco una query di ricerca nei Log hello schermata riportata di seguito:  
    ![ricerca log](./media/log-analytics-scom-assessment/scom-log-search.png)

2. Scegliere le raccomandazioni che si desidera tooignore. Si useranno i valori hello per RecommendationId nella procedura descritta di seguito hello.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate e utilizzare un file di testo IgnoreRecommendations.txt

1. Creare un file denominato IgnoreRecommendations.txt.
2. Incollare o digitare ogni RecommendationId per ogni raccomandazione che si desidera OMS tooignore su una riga separata e quindi salvare e chiudere il file hello.
3. Inserire file hello nella seguente cartella su ogni computer in cui si desidera indicazioni tooignore OMS hello.
4. Nel server di gestione di Operations Manager hello - *SystemDrive*: \Programmi\Microsoft System Center 2012 R2\Operations Manager\Server.

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify che le raccomandazioni vengano ignorate

1. Dopo aver eseguito hello valutazione pianificata successiva, per impostazione predefinita ogni sette giorni, hello specifica indicazioni sono contrassegnate come ignorate e non verranno visualizzati nel dashboard di valutazione di hello.
2. È possibile utilizzare hello toolist query di ricerca nei Log seguente tutte le indicazioni hello ignorato.

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

3. Se in seguito si decide che si desidera indicazioni toosee ignorate, rimuovere eventuali file IgnoreRecommendations.txt oppure rimuovere i Recommendationid dagli stessi.

## <a name="system-center-operations-manager-assessment-solution-faq"></a>Domande frequenti sulla soluzione System Center Operations Manager Assessment

*Area di lavoro OMS hello valutazione soluzione toomy aggiunto. Ma non è possibile visualizzare suggerimenti hello. Perché?* Dopo aver aggiunto la soluzione hello, utilizzare hello seguendo i passaggi visualizzare le indicazioni hello nel dashboard OMS hello.  

- [Impostare l'account RunAs hello per la valutazione di System Center Operations Manager](#operations-manager-run-as-accounts-for-oms)  
- [Configurare la regola di valutazione di System Center Operations Manager hello](#configure-the-assessment-rule)


*Esiste un modo tooconfigure la frequenza di esecuzione valutazione hello?* Sì. Vedere [hello Configura frequenza di esecuzione](#configure-the-run-frequency).

*Se non viene individuato un altro server dopo l'aggiunta soluzione per la valutazione di System Center Operations Manager hello, verrà valutato?* Sì, verrà valutato dal momento della rilevazione, per impostazione predefinita ogni sette giorni.

*Che cos'è il nome di hello del processo di hello hello la raccolta dei dati?* AdvisorAssessment.exe

*In cui viene eseguito il processo di AdvisorAssessment.exe hello?* AdvisorAssessment.exe viene eseguito con hello HealthService hello del server di gestione in cui regola valutazione hello è abilitato. Con questo processo, l'individuazione dell'intero ambiente avviene tramite la raccolta di dati remoti.

*Quanto tempo occorre per la raccolta di dati?* Raccolta di dati nel server di hello richiede circa un'ora. Potrebbe richiedere più tempo in ambienti con molte istanze o database di Operations Manager.

*Cosa accade se si imposta intervallo hello di tooless valutazione hello 1440 minuti?*  valutazione hello è preconfigurato toorun al massimo una volta al giorno. Se si esegue l'override hello intervallo valore tooa di valore inferiore a 1440 minuti, valutazione hello utilizza come valore dell'intervallo hello 1440 minuti.

*Come tooknow se sono presenti errori prerequisiti?* Se è stata eseguita la valutazione hello e risultati non viene visualizzata, è probabile che tra i prerequisiti per la valutazione di hello hello non è riuscita. È possibile eseguire query: `Type=Operation Solution=SCOMAssessment` e `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` in hello toosee ricerca dei registri non è stato possibile prerequisiti.

*È presente un messaggio `Failed tooconnect toohello SQL Instance (….).` negli errori relativi ai prerequisiti. Che cos'è il problema di hello?* AdvisorAssessment.exe, processo hello che raccoglie i dati, viene eseguito con hello HealthService hello del server di gestione. Come parte della valutazione di hello, il processo di hello tenta tooconnect toohello SQL Server in cui è presentano il database di Operations Manager hello. Questo errore può verificarsi quando le regole del firewall blocca l'istanza di SQL Server toohello connessione hello.

*Il tipo di dati viene raccolto?*  hello seguenti tipi di dati viene raccolti: dati di Operations Manager - EventLog dati - dati del Registro di sistema - dati WMI - tramite Windows PowerShell, le query SQL e File di informazioni dell'agente di raccolta.

*Motivo per cui è tooconfigure un Account runas?* Per un server di Operations Manager vengono eseguite diverse query SQL. Per permetterne toorun, è necessario utilizzare un Account RunAs con le autorizzazioni necessarie. Inoltre, le credenziali di amministratore locale sono necessari tooquery WMI.

*Perché vengono visualizzate solo hello prime 10 raccomandazioni?* Invece di esaminare un elenco completo, impegnativo di attività, è consigliabile concentrare l'attenzione sulle raccomandazioni con priorità hello. Dopo la verifica delle raccomandazioni principali, verranno rese disponibili raccomandazioni aggiuntive. Se si preferisce toosee elenco dettagliato di hello, è possibile visualizzare tutte le indicazioni con ricerca di Log.

*Esiste un modo tooignore una raccomandazione?* Sì, vedere hello [ignorare le raccomandazioni](#Ignore-recommendations).


## <a name="next-steps"></a>Passaggi successivi

- [Ricerca dei registri](log-analytics-log-searches.md) tooview dettagliate dati di valutazione di System Center Operations Manager e le indicazioni.
