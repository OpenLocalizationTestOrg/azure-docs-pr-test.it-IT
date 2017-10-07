---
title: "aaaStart o arrestare le macchine virtuali durante periodi di inattività [anteprima] soluzione | Documenti Microsoft"
description: soluzioni di gestione delle macchine Virtuali Hello avvia e arresta le macchine virtuali di gestione risorse di Azure in una pianificazione e il monitoraggio proattivo da Analitica di Log.
services: automation
documentationCenter: 
authors: mgoedtel
manager: carmonm
editor: 
ms.assetid: 06c27f72-ac4c-4923-90a6-21f46db21883
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: magoedte
ms.openlocfilehash: 6cbe16dfb40bf13f29d9e58ca0bc8c5c7979879d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="startstop-vms-during-off-hours-preview-solution-in-automation"></a>Soluzione Avvio/Arresto di macchine virtuali durante gli orari di minore attività (anteprima) in Automazione di Azure

Hello macchine virtuali di avvio/arresto durante soluzione orario di lavoro [anteprima] avvia e arresta le macchine virtuali di Azure Resource Manager in una pianificazione definita dall'utente e fornisce informazioni approfondite riuscita hello dei processi di automazione di hello che avviare e arrestare le macchine virtuali con OMS Log Analitica.  

## <a name="prerequisites"></a>Prerequisiti

- utilizzano i runbook Hello un [account RunAs di Azure](automation-offering-get-started.md#authentication-methods).  Hello account RunAs è il metodo di autenticazione preferito hello poiché utilizza l'autenticazione del certificato anziché una password che può scadere o modificati di frequente.  

- Questa soluzione è possibile gestire solo macchine virtuali che sono in hello stessa sottoscrizione in cui risiede l'account di automazione hello.  

- Questa soluzione consente di distribuire solo toohello seguenti aree di Azure - Europa occidentale, Stati Uniti orientali, Asia sudorientale e Australia sudorientale.  i runbook Hello gestire hello VM pianificazione possono essere destinati a macchine virtuali in qualsiasi area.  

- notifiche di posta elettronica toosend quando hello avviare e arrestare i runbook VM completa, una sottoscrizione di classe aziendale di Office 365 è obbligatorio.  

## <a name="solution-components"></a>Componenti della soluzione

Questa soluzione è costituita da hello seguendo le risorse che verranno importate e aggiunti tooyour account di automazione.

### <a name="runbooks"></a>Runbook

Runbook | Descrizione|
--------|------------|
CleanSolution-MS-Mgmt-VM | Questo runbook rimuove tutti i contenuti di risorse e pianificazioni quando si passa soluzione hello toodelete dalla sottoscrizione.|  
SendMailO365-MS-Mgmt | Questo runbook invia un messaggio di posta elettronica tramite Office 365 Exchange.|
StartByResourceGroup-MS-Mgmt-VM | Questo runbook è macchine virtuali toostart previsto (entrambi classica e ARM basato su macchine virtuali) che si trova in un elenco di gruppi di risorse di Azure specificato.
StopByResourceGroup-MS-Mgmt-VM | Questo runbook è macchine virtuali toostop previsto (entrambi classica e ARM basato su macchine virtuali) che si trova in un elenco di gruppi di risorse di Azure specificato.|
<br>

### <a name="variables"></a>variables

Variabile | Descrizione|
---------|------------|
Runbook **SendMailO365-MS-Mgmt** ||
SendMailO365-IsSendEmail-MS-Mgmt | Specifica se i runbook StartByResourceGroup-MS-Mgmt-VM e StopByResourceGroup-MS-Mgmt-VM possono inviare notifiche tramite posta elettronica al termine dell'operazione.  Selezionare **True** tooenable e **False** toodisable avvisi di posta elettronica. Il valore predefinito è **False**.| 
Runbook **StartByResourceGroup-MS-Mgmt-VM** ||
StartByResourceGroup-ExcludeList-MS-Mgmt-VM | Immettere toobe nomi VM escluso dall'operazione di gestione. separare i nomi utilizzando semi-colon(;) senza spazi. I valori fanno distinzione tra maiuscole e minuscole ed è supportato il carattere jolly asterisco.|
StartByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | Testo che può essere aggiunto toohello inizio del corpo del messaggio di posta elettronica hello.|
StartByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | Specifica il nome di hello dell'Account di automazione che contenga un runbook di posta elettronica hello hello.  **Non modificare questa variabile.**|
StartByResourceGroup-SendMailO365-EmailRunbookName-MS-Mgmt | Specifica il nome di hello del runbook di posta elettronica hello.  Viene utilizzato da hello StartByResourceGroup-MS-Mgmt-VM e messaggio di posta elettronica toosend runbook StopByResourceGroup-MS-Mgmt-VM.  **Non modificare questa variabile.**|
StartByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | Specifica il nome di hello hello del gruppo di risorse che contenga un runbook di posta elettronica hello.  **Non modificare questa variabile.**|
StartByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | Specifica il testo hello riga dell'oggetto del messaggio di posta elettronica hello hello.|  
StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | Specifica i destinatari hello del messaggio di posta elettronica hello.  Immettere i nomi separati da un punto e virgola (;) senza spazi.|
StartByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | Immettere toobe nomi VM escluso dall'operazione di gestione. separare i nomi utilizzando semi-colon(;) senza spazi. I valori fanno distinzione tra maiuscole e minuscole ed è supportato il carattere jolly asterisco.  Il valore predefinito (asterisco) includerà tutti i gruppi di risorse nella sottoscrizione hello.|
StartByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | Specifica sottoscrizione hello contenente toobe macchine virtuali gestiti da questa soluzione.  Deve trattarsi di hello stessa sottoscrizione in cui risiede l'account di automazione di questa soluzione hello.|
Runbook **StopByResourceGroup-MS-Mgmt-VM** ||
StopByResourceGroup-ExcludeList-MS-Mgmt-VM | Immettere toobe nomi VM escluso dall'operazione di gestione. separare i nomi utilizzando semi-colon(;) senza spazi. I valori fanno distinzione tra maiuscole e minuscole ed è supportato il carattere jolly asterisco.|
StopByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | Testo che può essere aggiunto toohello inizio del corpo del messaggio di posta elettronica hello.|
StopByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | Specifica il nome di hello dell'Account di automazione che contenga un runbook di posta elettronica hello hello.  **Non modificare questa variabile.**|
StopByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | Specifica il nome di hello hello del gruppo di risorse che contenga un runbook di posta elettronica hello.  **Non modificare questa variabile.**|
StopByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | Specifica il testo hello riga dell'oggetto del messaggio di posta elettronica hello hello.|  
StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | Specifica i destinatari hello del messaggio di posta elettronica hello.  Immettere i nomi separati da un punto e virgola (;) senza spazi.|
StopByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | Immettere toobe nomi VM escluso dall'operazione di gestione. separare i nomi utilizzando semi-colon(;) senza spazi. I valori fanno distinzione tra maiuscole e minuscole ed è supportato il carattere jolly asterisco.  Il valore predefinito (asterisco) includerà tutti i gruppi di risorse nella sottoscrizione hello.|
StopByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | Specifica sottoscrizione hello contenente toobe macchine virtuali gestiti da questa soluzione.  Deve trattarsi di hello stessa sottoscrizione in cui risiede l'account di automazione di questa soluzione hello.|  
<br>

### <a name="schedules"></a>Pianificazioni

Pianificazione | Descrizione|
---------|------------|
StartByResourceGroup-Schedule-MS-Mgmt | Pianificazione per il runbook StartByResourceGroup, che esegue l'avvio hello di macchine virtuali gestite da questa soluzione. Creazione, il valore predefinito tooUTC fuso orario.|
StopByResourceGroup-Schedule-MS-Mgmt | Pianificazione per il runbook StopByResourceGroup, che esegue hello arresto delle macchine virtuali gestiti da questa soluzione. Creazione, il valore predefinito tooUTC fuso orario.|

### <a name="credentials"></a>Credenziali

Credenziali | Descrizione|
-----------|------------|
O365Credential | Specifica un valido Office 365 utente toosend posta elettronica dell'account.  Necessario solo se variabile SendMailO365-IsSendEmail-MS-Mgmt viene impostato troppo**True**.

## <a name="configuration"></a>Configurazione

Eseguire i seguenti passaggi tooadd hello macchine virtuali di avvio/arresto durante l'orario di lavoro [anteprima] soluzione tooyour account di automazione hello e quindi configurare hello variabili toocustomize hello soluzione.

1. Hello-schermata home hello portale di Azure, selezionare hello **Marketplace** riquadro.  Se il riquadro hello non è più bloccato tooyour-schermata, dal riquadro di spostamento a sinistra di hello, selezionare **New**.  
2. Nel Pannello di Marketplace hello, digitare **avvia macchina virtuale** nella casella di ricerca hello e quindi selezionare hello soluzione **macchine virtuali di avviare o arrestare l'orario di ufficio [anteprima]** dai risultati della ricerca hello.  
3. In hello **macchine virtuali di avviare o arrestare l'orario di ufficio [anteprima]** pannello hello selezionata soluzione, esaminare le informazioni di riepilogo hello e quindi fare clic su **crea**.  
4. Hello **Aggiungi soluzione** pannello viene visualizzato in cui ti trovi tooconfigure richiesta hello soluzione prima di poter importare alla sottoscrizione di automazione.<br><br> ![Pannello Aggiungi soluzione di Virtual Machine Management](media/automation-solution-vm-management/vm-management-solution-add-solution-blade.png)<br><br>
5.  In hello **Aggiungi soluzione** pannello seleziona **dell'area di lavoro** e consente di selezionare un'area di lavoro OMS che è collegato toohello stessa sottoscrizione di Azure che hello account di automazione è in o crea una nuova area di lavoro OMS.  Se non si dispone di un'area di lavoro OMS, è possibile selezionare **Crea nuova area di lavoro** e hello **area di lavoro OMS** pannello eseguire l'esempio hello: 
   - Specificare un nome per hello nuovo **area di lavoro OMS**.
   - Selezionare un **sottoscrizione** toolink tooby selezionare dall'elenco a discesa hello se predefinito hello selezionato non è appropriato.
   - Per il **gruppo di risorse**, è possibile selezionare un gruppo di risorse esistente o crearne uno nuovo.  
   - Selezionare un **percorso**.  Non sono attualmente forniti per la selezione in base ai soli percorsi hello **Australia sudorientale**, **Stati Uniti orientali**, **Asia sudorientale**, e **Europa occidentale**.
   - Selezionare un **Piano tariffario**.  soluzione Hello viene offerto con due livelli: libero e OMS a pagamento di livello.  livello gratuito Hello pone un limite sulla quantità di hello di dati raccolti giornalmente, periodo di memorizzazione e runbook processo runtime minuti.  Hello OMS a pagamento di livello prevede un limite alla quantità di hello di dati raccolti giornalmente.  

        > [!NOTE]
        > Mentre hello autonomo a pagamento di livello viene visualizzato come un'opzione, non è applicabile.  Se si seleziona e procedere con la creazione di hello di questa soluzione nella sottoscrizione, avrà esito negativo.  Questo problema sarà risolto al momento del rilascio ufficiale della soluzione.<br>Se si usa la soluzione, questa usa solo l'inserimento di log e i minuti di esecuzione dei processi di automazione.  soluzione Hello non aggiunge aggiuntive dell'ambiente OMS tooyour nodi.  

6. Dopo aver specificato le informazioni necessarie hello in hello **area di lavoro OMS** pannello, fare clic su **crea**.  Mentre viene verificate le informazioni di hello e viene creato l'area di lavoro hello, è possibile tenere traccia dello stato di avanzamento in **notifiche** dal menu di hello.  Verrà restituito toohello **Aggiungi soluzione** blade.  
7. In hello **Aggiungi soluzione** pannello seleziona **Account di automazione**.  Se si sta creando una nuova area di lavoro OMS, sarà necessario tooalso creare un nuovo account di automazione che verrà associato con hello nuova area di lavoro OMS specificato in precedenza, inclusa la sottoscrizione di Azure, un gruppo di risorse e area.  È possibile selezionare **creare un account di automazione** e hello **account di automazione aggiungere** pannello fornire seguente hello: 
  - In hello **nome** immettere nome hello di hello account di automazione.

    Tutte le altre opzioni vengono popolati automaticamente in base a area di lavoro OMS hello selezionata e non è possibile modificare queste opzioni.  Un account RunAs di Azure è metodo di autenticazione hello predefinito per i runbook hello inclusi in questa soluzione.  Quando si fa clic su **OK**, opzioni di configurazione hello vengono convalidate e viene creato l'account di automazione hello.  È possibile tenere traccia dello stato di avanzamento in **notifiche** dal menu di hello. 

    In alternativa, è possibile selezionare un account RunAs di Automazione esistente.  Si noti che l'account hello selezionato non può essere già collegato tooanother area di lavoro OMS, in caso contrario un messaggio verrà visualizzato in tooinform pannello hello è.  Se è già collegato, è necessario un diverso account RunAs automazione tooselect o se crearne uno nuovo.<br><br> ![Automazione Account già collegato tooOMS dell'area di lavoro](media/automation-solution-vm-management/vm-management-solution-add-solution-blade-autoacct-warning.png)<br>

8. Infine nel hello **Aggiungi soluzione** pannello seleziona **configurazione** hello e **parametri** pannello viene visualizzato.  In hello **parametri** pannello, viene chiesto di:  
   - Specificare hello **nomi di gruppo di risorse di destinazione**, ovvero un nome di gruppo di risorse contenente toobe macchine virtuali gestiti da questa soluzione.  È possibile immettere più nomi, separati da un punto e virgola. I valori fanno distinzione tra maiuscole e minuscole.  I caratteri jolly è supportato se si desidera tootarget le macchine virtuali in tutti i gruppi di risorse nella sottoscrizione hello.
   - Selezionare un **pianificazione** che è ricorrente data e ora per l'avvio e arresto hello della macchina virtuale in hello di gruppi di risorse di destinazione.  Per impostazione predefinita, la pianificazione di hello è fuso orario configurato toohello UTC e selezionare un'altra area non è disponibile.  Se si desidera tooconfigure hello pianificazione tooyour fuso orario specifico dopo la configurazione di soluzione hello, vedere [pianificazione di avvio e arresto di hello modifica](#modifying-the-startup-and-shutdown-schedule) sotto.    

10. Dopo aver completato la configurazione impostazioni iniziale di hello necessarie per la soluzione hello, selezionare **crea**.  Tutte le impostazioni verranno convalidate e quindi verrà eseguito un tentativo soluzione hello toodeploy nella sottoscrizione.  Questo processo può richiedere alcuni secondi toocomplete ed è possibile tenere traccia dello stato di avanzamento in **notifiche** dal menu di hello. 

## <a name="collection-frequency"></a>Frequenza della raccolta

Automazione del log e processo di flusso dati del processo vengono acquisiti nel repository OMS hello ogni cinque minuti.  

## <a name="using-hello-solution"></a>Utilizzo di soluzione hello

Quando si aggiunta soluzione di gestione delle macchine Virtuali hello, nel hello dell'area di lavoro OMS **StartStopVM vista** riquadro verrà aggiunto il dashboard OMS tooyour.  Questo riquadro Visualizza un numero e la rappresentazione grafica dei processi di runbook di hello per soluzione hello che sono stati avviati e completati.<br><br> ![Riquadro StartStopVM View (Visualizzazione di avvio e arresto di VM) di Virtual Machine Management](media/automation-solution-vm-management/vm-management-solution-startstopvm-view-tile.png)  

Nell'account di automazione, è possibile accedere e gestire soluzioni hello selezionando hello **soluzioni** riquadro e quindi da hello **soluzioni** pannello selezione soluzione hello **[inizio-Stop-VM Area di lavoro]** dall'elenco di hello.<br><br> ![Elenco delle soluzioni di automazione](media/automation-solution-vm-management/vm-management-solution-autoaccount-solution-list.png)  

Selezione di soluzione hello visualizzerà hello **Start-Stop-VM [area]** pannello soluzione, in cui è possibile rivedere le informazioni importanti, ad esempio hello **StartStopVM** riquadro, ad esempio nell'area di lavoro OMS, che Visualizza un numero e la rappresentazione grafica dei processi di runbook di hello per soluzione hello che sono stati avviati e completati.<br><br> ![Pannello delle soluzioni di automazione delle macchine virtuali](media/automation-solution-vm-management/vm-management-solution-solution-blade.png)  

Da qui è anche possibile aprire l'area di lavoro OMS ed eseguire un'ulteriore analisi hello di record del processo.  Fare clic su **tutte le impostazioni**e in hello **impostazioni** pannello seleziona **avvio rapido** e quindi in hello **avvio rapido** selezionare pannello ** Portale di OMS**.   Verrà aperta una nuova scheda o una nuova sessione del browser e verrà visualizzata l'area di lavoro OMS associata alla sottoscrizione e all'account di Automazione.  


### <a name="configuring-e-mail-notifications"></a>Configurazione delle notifiche tramite posta elettronica

le notifiche di posta elettronica tooenable quando hello avviano e arrestare i runbook VM completa, sarà necessario hello toomodify **O365Credential** credenziali e come minimo, hello seguenti variabili:

 - SendMailO365-IsSendEmail-MS-Mgmt
 - StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt
 - StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt

hello tooconfigure **O365Credential** credenziali, eseguire hello alla procedura seguente:

1. Scegliere l'account di automazione, **tutte le impostazioni** nella parte superiore di hello della finestra hello. 
2. In hello **impostazioni** pannello sezione hello **risorse di automazione**selezionare **asset**. 
3. In hello **asset** blade, seleziona hello **credenziali** riquadro e da hello **credenziali** blade, seleziona hello **O365Credential**.  
4. Immettere un nome utente di Office 365 valido e una password e quindi fare clic su **salvare** toosave le modifiche.  

le variabili di hello tooconfigure evidenziate in precedenza, eseguire hello alla procedura seguente:

1. Scegliere l'account di automazione, **tutte le impostazioni** nella parte superiore di hello della finestra hello. 
2. In hello **impostazioni** pannello sezione hello **risorse di automazione**selezionare **asset**. 
3. In hello **asset** blade, seleziona hello **variabili** riquadro e da hello **variabili** pannello selezionare variabile hello sopra elencati e quindi modificare il relativo valore successivo hello descrizione relativa all'hello [variabile](##variables) sezione precedente.  
4. Fare clic su **salvare** variabile toohello di toosave hello le modifiche.   

### <a name="modifying-hello-startup-and-shutdown-schedule"></a>Pianificazione di avvio e arresto hello modifica

Gestione pianificazione di avvio e arresto hello in questa soluzione segue hello stesso i passaggi indicati [pianificazione di un runbook in automazione di Azure](automation-schedules.md).  Tenere presente che non è possibile modificare la configurazione di pianificazione hello.  Sarà necessario toodisable hello pianificazione esistente e quindi crearne uno nuovo e quindi collegare toohello **StartByResourceGroup-MS-Mgmt-VM** o **StopByResourceGroup-MS-Mgmt-VM** runbook che si desidera hello pianificare tooapply per.   

## <a name="log-analytics-records"></a>Record di Log Analytics

Automazione crea due tipi di record nel repository OMS hello.

### <a name="job-logs"></a>Log di processo

Proprietà | Descrizione|
----------|----------|
Chiamante |  Che ha iniziato l'operazione di hello.  I valori possibili sono un indirizzo di posta elettronica o il sistema per i processi pianificati.|
Categoria | Classificazione del tipo di hello dei dati.  Per l'automazione, il valore di hello è JobLogs.|
CorrelationId | GUID che rappresenta l'Id di correlazione di processo del runbook hello hello.|
JobId | GUID che rappresenta l'Id di processo del runbook hello hello.|
operationName | Specifica il tipo di hello di operazione eseguita in Azure.  Per l'automazione, il valore di hello sarà processo.|
resourceId | Specifica il tipo di risorsa hello in Azure.  Per l'automazione, valore hello è l'account di automazione hello associato hello runbook.|
ResourceGroup | Specifica nome del processo del runbook hello gruppo di risorse hello.|
ResourceProvider | Specifica hello servizio Azure che fornisce risorse hello è possibile distribuire e gestire.  Per l'automazione, il valore di hello è automazione di Azure.|
ResourceType | Specifica il tipo di risorsa hello in Azure.  Per l'automazione, valore hello è l'account di automazione hello associato hello runbook.|
resultType | stato di Hello del processo del runbook hello.  I valori possibili sono:<br>- Avviato<br>- Interrotto<br>- Sospeso<br>- Non riuscito<br>- Completato|
resultDescription | Descrive lo stato del risultato processo runbook hello.  I valori possibili sono:<br>- Processo avviato<br>- Processo non riuscito<br>- Processo completato|
RunbookName | Specifica il nome di hello di hello runbook.|
SourceSystem | Specifica il sistema di origine hello per dati hello inviati.  Per l'automazione, il valore di hello sarà: Operations Manager|
StreamType | Specifica il tipo di hello dell'evento. I valori possibili sono:<br>- Dettagliato<br>- Output<br>- Errore<br>- Avviso|
SubscriptionId | Specifica l'ID sottoscrizione hello del processo di hello.
Tempo | Data e ora esecuzione processo del runbook hello.|


### <a name="job-streams"></a>Flussi di processo

Proprietà | Descrizione|
----------|----------|
Chiamante |  Che ha iniziato l'operazione di hello.  I valori possibili sono un indirizzo di posta elettronica o il sistema per i processi pianificati.|
Categoria | Classificazione del tipo di hello dei dati.  Per l'automazione, il valore di hello è JobStreams.|
JobId | GUID che rappresenta l'Id di processo del runbook hello hello.|
operationName | Specifica il tipo di hello di operazione eseguita in Azure.  Per l'automazione, il valore di hello sarà processo.|
ResourceGroup | Specifica nome del processo del runbook hello gruppo di risorse hello.|
resourceId | Specifica l'Id della risorsa hello in Azure.  Per l'automazione, valore hello è l'account di automazione hello associato hello runbook.|
ResourceProvider | Specifica hello servizio Azure che fornisce risorse hello è possibile distribuire e gestire.  Per l'automazione, il valore di hello è automazione di Azure.|
ResourceType | Specifica il tipo di risorsa hello in Azure.  Per l'automazione, valore hello è l'account di automazione hello associato hello runbook.|
resultType | risultato Hello di processo del runbook hello all'evento di hello hello time è stato generato.  I valori possibili sono:<br>- InProgress|
resultDescription | Include il flusso di output di hello da hello runbook.|
RunbookName | nome Hello di hello runbook.|
SourceSystem | Specifica il sistema di origine hello per dati hello inviati.  Per l'automazione, il valore di hello sarà Operations Manager|
StreamType | tipo di Hello del flusso di processo. I valori possibili sono:<br>- Avanzamento<br>- Output<br>- Avviso<br>- Errore<br>- Debug<br>- Dettagliato|
Tempo | Data e ora esecuzione processo del runbook hello.|

Quando si eseguono tutte le ricerche log che restituisce i record di categoria di **JobLogs** o **JobStreams**, è possibile selezionare hello **JobLogs** o **JobStreams** visualizzazione che consente di visualizzare un set di sezioni di riepilogo degli aggiornamenti di hello restituiti dalla ricerca hello.

## <a name="sample-log-searches"></a>Ricerche di log di esempio

Hello nella tabella seguente fornisce ricerche log di esempio per i record dei processi raccolti da questa soluzione. 

Query | Descrizione|
----------|----------|
Trova i processi completati per il runbook StartVM | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Succeeded &#124; measure count() by JobId_g|
Trova i processi completati per il runbook StopVM | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Failed &#124; measure count() by JobId_g
Visualizza lo stato dei processi nel tempo per i runbook StartVM e StopVM | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" OR "StopByResourceGroup-MS-Mgmt-VM" NOT(ResultType="started") | measure Count() by ResultType interval 1day|

## <a name="removing-hello-solution"></a>Rimozione di soluzioni hello

Se si decide di che non è più necessario soluzione hello toouse qualsiasi ulteriore, è possibile eliminarlo dal hello account di automazione.  L'eliminazione della soluzione hello rimuoverà solo i runbook hello, non eliminerà le pianificazioni di hello o le variabili che sono state create quando è stata aggiunta la soluzione hello.  Tali risorse occorre toodelete manualmente se non vengono utilizzati con altri runbook.  

toodelete hello soluzione, eseguire hello alla procedura seguente:

1.  Selezionare l'account di automazione, hello **soluzioni** riquadro.  
2.  In hello **soluzioni** pannello, la soluzione hello selezionare **Start-Stop-VM [area]**.  In hello **VMManagementSolution [area]** pannello da fare clic su menu hello **eliminare**.<br><br> ![Eliminare una soluzione di gestione di macchine virtuali](media/automation-solution-vm-management/vm-management-solution-delete.png)
3.  In hello **Elimina soluzione** finestra di conferma soluzione hello toodelete.
4.  Mentre viene verificate informazioni hello e soluzione hello viene eliminata, è possibile tenere traccia dello stato di avanzamento in **notifiche** dal menu di hello.  Verrà restituito toohello **VMManagementSolution [area]** pannello dopo l'avvio di soluzione tooremove dei processi di hello.  

area di lavoro OMS e account di automazione Hello non vengono eliminati come parte di questo processo.  Se si desidera tooretain area di lavoro OMS hello, sarà necessario eliminarlo toomanually.  Può essere eseguita anche dal portale di Azure hello.   Hello-schermata home hello portale di Azure, selezionare **Log Analitica** e quindi su hello **Log Analitica** pannello area di lavoro selezionare hello e fare clic su **eliminare** dal menu hello pannello delle impostazioni dell'area di lavoro di Hello.  
      
## <a name="next-steps"></a>Passaggi successivi

- toolearn ulteriori informazioni su come query di ricerca diverso tooconstruct e revisione hello automazione del processo di log con Log Analitica, vedere [Accedi ricerche Log Analitica](../log-analytics/log-analytics-log-searches.md)
- ulteriori sull'esecuzione di runbook, come i processi del runbook toomonitor e altri dettagli tecnici, vedere toolearn [tenere traccia di un processo del runbook](automation-runbook-execution.md)
- toolearn ulteriori informazioni su OMS Log Analitica e origini di raccolta dati, vedere [dati di archiviazione di Azure la raccolta in panoramica Log Analitica](../log-analytics/log-analytics-azure-storage.md)






   

