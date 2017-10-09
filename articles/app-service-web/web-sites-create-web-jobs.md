---
title: "aaaRun attività in Background con processi Web"
description: "Informazioni su come attività in background toorun in Azure web app."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: af01771e-54eb-4aea-af5f-f883ff39572b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/27/2016
ms.author: glenga
ms.openlocfilehash: 96a3d977a806e7192207f0f4da79dfd248694336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-background-tasks-with-webjobs"></a>Eseguire attività in background con processi Web
## <a name="overview"></a>Panoramica
È possibile eseguire programmi o script in Processi Web nell'app Web del [servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) in tre modi: su richiesta, sempre, in base a una pianificazione. Non vi è alcun toouse costi aggiuntivi processi Web.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Questo articolo illustra come toodeploy processi Web usando hello [portale Azure](https://portal.azure.com). Per informazioni su come toodeploy utilizzando Visual Studio o in un processo di distribuzione continua, vedere [come tooDeploy processi Web di Azure tooWeb app](websites-dotnet-deploy-webjobs.md).

Hello Azure WebJobs SDK semplifica molte attività di programmazione di processi Web. Per ulteriori informazioni, vedere [novità hello WebJobs SDK](websites-dotnet-webjobs-sdk.md).

 Funzioni di Azure fornisce un altro toorun programmi e script da un ambiente senza server o da un'applicazione di servizio App. Per altre informazioni, vedere [Panoramica di Funzioni di Azure](../azure-functions/functions-overview.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="acceptablefiles"></a>Tipi di file consentiti per script e programmi
viene accettato i seguenti tipi di file Hello:

* .cmd, .bat, .exe (Prompt dei comandi di Windows)
* .ps1 (PowerShell)
* .sh (Bash)
* .php (PHP)
* .py (Python)
* .js (Node)
* JAR (Java)

## <a name="CreateOnDemand"></a>Creare un processo Web report su richiesta nel portale di hello
1. In hello **App Web** blade di hello [portale Azure](https://portal.azure.com), fare clic su **tutte le impostazioni > processi Web** tooshow hello **processi Web** blade.
   
    ![Pannello Processi Web](./media/web-sites-create-web-jobs/wjblade.png)
2. Fare clic su **Aggiungi**. Hello **Aggiungi processo Web** viene visualizzata la finestra.
   
    ![Pannello Aggiungi processo Web](./media/web-sites-create-web-jobs/addwjblade.png)
3. In **nome**, specificare un nome per hello processo Web. nome di Hello deve iniziare con una lettera o un numero e può contenere caratteri speciali diversi da "-" e "_".
4. In hello **come tooRun** scegliere **eseguiti su richiesta**.
5. In hello **caricamento File** fare clic sull'icona di cartella hello e individuare i file zip toohello contenente lo script. file zip Hello deve contenere il file eseguibile (.exe cmd. bat. sh. PHP. py. js) nonché eventuali file di supporto necessari toorun hello programmi o script.
6. Controllare **crea** tooupload hello script tooyour web app. 
   
    Hello nome specificato per hello processo Web viene visualizzato nell'elenco hello hello **processi Web** blade.
7. hello toorun processo Web, mouse sul nome nell'elenco di hello e fare clic su **eseguire**.
   
    ![Eseguire un processo Web](./media/web-sites-create-web-jobs/runondemand.png)

## <a name="CreateContinuous"></a>Creare un processo Web con esecuzione continua
1. toocreate un processo Web continuamente in esecuzione, seguire hello stessi passaggi per la creazione di un processo Web che viene eseguito una volta, ma in hello **come tooRun** scegliere **continuo**.
2. toostart o arrestare un processo Web continuo, fare doppio clic su hello processo Web nell'elenco di hello e fare clic su **avviare** o **arrestare**.

> [!NOTE]
> Se l'app Web è in esecuzione su più di un'istanza, il processo Web con esecuzione continua verrà eseguito su tutte le istanze. I processi Web su richiesta e pianificati vengono eseguiti su una singola istanza selezionata per il bilanciamento del carico da Microsoft Azure.
> 
> Per i processi Web continui toorun in modo affidabile e in tutte le istanze, abilitare hello Always On * impostazione di configurazione per hello app web in caso contrario è possibile interrompere l'esecuzione quando il sito di host SCM hello è rimasto inattivo per troppo tempo.
> 
> 

## <a name="CreateScheduledCRON"></a>Creare un processo Web pianificato utilizzando un'espressione CRON
Questa tecnica è disponibile tooWeb App in esecuzione in modalità Basic, Standard o Premium e richiede hello **Always On** impostazione toobe attivata app hello.

tooturn sul processo Web richiesta in un processo Web pianificato, includere semplicemente un `settings.job` file alla radice di hello del file zip processo Web. Questo file JSON deve includere una `schedule` proprietà con un [espressione CRON](https://en.wikipedia.org/wiki/Cron), per esempio quanto riportato di seguito.

espressione CRON Hello è costituita da 6 campi: `{second} {minute} {hour} {day} {month} {day of hello week}`.

Ad esempio, tootrigger del processo Web ogni 15 minuti, il `settings.job` sarebbe:

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

Altri esempi di programmazione CRON:

* Ogni ora (ad esempio ogni volta che il numero di hello di minuti è 0):`0 0 * * * *` 
* Ogni ora da too5 09: 00 PM:`0 0 9-17 * * *` 
* Alle 9:30 di mattina ogni giorno: `0 30 9 * * *`
* Alle 9:30 di mattina ogni giorno della settimana: `0 30 9 * * 1-5`

**Nota**: quando si distribuisce un processo Web da Visual Studio, assicurarsi che toomark il `settings.job` proprietà file come 'Copia se più recente'.

## <a name="CreateScheduled"></a>Creare un processo Web pianificato usando hello dell'utilità di pianificazione di Azure
Hello tecnica alternativa seguente si avvalgono di hello dell'utilità di pianificazione di Azure. In questo caso, il processo Web ha alcuna conoscenza diretta della pianificazione hello. Al contrario, hello dell'utilità di pianificazione di Azure Ottiene tootrigger configurato del processo Web su una pianificazione. 

Hello portale di Azure non dispone ancora di hello possibilità toocreate un processo Web pianificato, ma solo dopo l'aggiunta di tale funzionalità è possibile farlo tramite hello [portale classico](http://manage.windowsazure.com).

1. In hello [portale classico](http://manage.windowsazure.com) toohello processo Web pagina, fare clic su **Aggiungi**.
2. In hello **come tooRun** scegliere **eseguita in una pianificazione**.
   
    ![Nuovo processo pianificato][NewScheduledJob]
3. Scegliere hello **area dell'utilità di pianificazione** per il processo, quindi fare clic sulla freccia di hello in hello basso a destra hello finestra di dialogo tooproceed toohello nella schermata successiva.
4. In hello **Crea processo** finestra di dialogo, scegliere il tipo di hello di **ricorrenza** desiderato: **processo occasionale** o **processo ricorrente**.
   
    ![Pianificare la ricorrenza][SchdRecurrence]
5. Scegliere un'ora di **inizio**: **Ora** o **A un orario specifico**.
   
    ![Pianificare l'ora di inizio][SchdStart]
6. Se si desidera toostart in un momento specifico, scegliere i valori di ora iniziale in **avvio su**.
   
    ![Pianificare l'avvio a un'ora specifica][SchdStartOn]
7. Se si sceglie un processo ricorrente, è necessario hello **ricorre ogni** opzione frequenza hello toospecify di occorrenza e hello **che terminano in** toospecify opzione un'ora di fine.
   
    ![Pianificare la ricorrenza][SchdRecurEvery]
8. Se si sceglie **settimane**, è possibile selezionare hello **su una determinata pianificazione** e specificare hello giorni hello che si desidera hello toorun di processo.
   
    ![Giorni di pianificazione di hello settimana][SchdWeeksOnParticular]
9. Se si sceglie **mesi** e seleziona hello **su una determinata pianificazione** casella, è possibile impostare toorun processo hello in particolare numerati **giorni** nel mese di hello. 
   
    ![Pianificare le date particolare hello mese][SchdMonthsOnPartDays]
10. Se si sceglie **giorni della settimana**, è possibile selezionare quale giorno o giorni della settimana hello desiderato hello toorun processo nel mese di hello.
    
     ![Pianificare giorni della settimana specifici in un mese][SchdMonthsOnPartWeekDays]
11. Infine, è inoltre possibile utilizzare hello **occorrenze** opzione toochoose la settimana del mese hello (primo, secondo, terzo e così via) si desidera toorun processo hello in hello giorni della settimana specificato.
    
    ![Pianificare giorni della settimana specifici per determinate settimane in un mese][SchdMonthsOnPartWeekDaysOccurences]
12. Dopo aver creato uno o più processi, i relativi nomi verranno visualizzati nella scheda processi Web hello con relativo stato, il tipo di pianificazione e altre informazioni. Informazioni cronologiche per hello ultimi 30 processi Web viene mantenute.
    
    ![Elenco processi][WebJobsListWithSeveralJobs]

### <a name="Scheduler"></a>Processi pianificati e Utilità di pianificazione di Azure
I processi pianificati possono essere ulteriormente configurati nelle pagine di pianificazione di Azure hello di hello [portale classico](http://manage.windowsazure.com).

1. Nella pagina processi Web hello, fare clic su del processo di hello **pianificazione** pagina del portale di collegamento toonavigate toohello dell'utilità di pianificazione di Azure. 
   
   ![Collegamento tooAzure dell'utilità di pianificazione][LinkToScheduler]
2. Nella pagina di hello dell'utilità di pianificazione, fare clic su processo hello.
   
    ![Processo nella pagina del portale di hello dell'utilità di pianificazione][SchedulerPortal]
3. Hello **azione del processo** pagina visualizzata, in cui è possibile configurare ulteriormente il processo di hello. 
   
    ![Pagina Job Action nell'Utilità di pianificazione][JobActionPageInScheduler]

## <a name="ViewJobHistory"></a>Visualizza cronologia processi hello
1. cronologia di esecuzione hello tooview di un processo, inclusi i processi creati con hello WebJobs SDK, fare clic sul collegamento corrispondente in hello **registri** colonna del Pannello di processi Web hello. (È possibile utilizzare URL hello toocopy hello Appunti icona degli Appunti toohello di hello log file pagina se si desidera).
   
    ![Collegamento Log](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. Facendo clic su collegamento hello verrà visualizzata la pagina dei dettagli hello per hello processo Web. Viene illustrata questa pagina hello nome dell'esecuzione del comando hello, hello ora dell'ultima esecuzione, e il relativo esito positivo o negativo. In **processi recenti**, fare clic su un toosee di tempo ulteriori dettagli.
   
    ![WebJobDetails][WebJobDetails]
3. Hello **Dettagli esecuzione attività** verrà visualizzata la pagina. Fare clic su **attiva/disattiva Output** testo hello toosee del contenuto del log hello. log di output di Hello è in formato testo. 
   
    ![Dettagli dell'esecuzione del processo Web][WebJobRunDetails]
4. testo di output di hello toosee in una finestra distinta del browser, fare clic su hello **scaricare** collegamento. testo hello toodownload, fare doppio clic su collegamento hello e utilizzare il contenuto del file hello toosave opzioni del browser.
   
    ![Download dell'output del log][DownloadLogOutput]
5. Hello **processi Web** collegamento nella parte superiore di hello della pagina hello fornisce un elenco di tooa tooget di pratica di processi Web nel dashboard di cronologia hello.
   
    ![Elenco di collegamenti tooWebJobs][WebJobsLinkToDashboardList]
   
    ![Elenco dei processi nel dashboard della cronologia][WebJobsListInJobsDashboard]
   
    Fare clic su uno di questi collegamenti accetta pagina dettagli attività toohello per processo hello selezionato.

## <a name="WHPNotes"></a>Note
* App Web in modalità disponibile può causare il timeout dopo 20 minuti se sono non presenti Nessun sito di richieste toohello scm (distribuzione) e portale hello app web non è aperta in Azure. Del sito effettivo di richieste toohello non verrà reimpostate questo.
* Il codice per un processo continuo deve toobe scritto toorun in un ciclo infinito.
* I processi continui eseguiti continuamente solo quando l'applicazione web hello è attiva.
* Base e la modalità Standard offerta hello sempre nella funzionalità che, se abilitata, impedisce alle App web di diventa inattivo.
* È possibile solo eseguire il debug di processi Web con esecuzione continua. Il debug di processi Web pianificati o su richiesta non è supportato.

## <a name="NextSteps"></a>Passaggi successivi
Per altre informazioni, vedere l'articolo relativo alle [risorse consigliate per i processi Web di Azure][WebJobsRecommendedResources].

[PSonWebJobs]:http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx
[WebJobsRecommendedResources]:http://go.microsoft.com/fwlink/?LinkId=390226

[OnDemandWebJob]: ./media/web-sites-create-web-jobs/01aOnDemandWebJob.png
[WebJobsList]: ./media/web-sites-create-web-jobs/02aWebJobsList.png
[NewContinuousJob]: ./media/web-sites-create-web-jobs/03aNewContinuousJob.png
[NewScheduledJob]: ./media/web-sites-create-web-jobs/04aNewScheduledJob.png
[SchdRecurrence]: ./media/web-sites-create-web-jobs/05SchdRecurrence.png
[SchdStart]: ./media/web-sites-create-web-jobs/06SchdStart.png
[SchdStartOn]: ./media/web-sites-create-web-jobs/07SchdStartOn.png
[SchdRecurEvery]: ./media/web-sites-create-web-jobs/08SchdRecurEvery.png
[SchdWeeksOnParticular]: ./media/web-sites-create-web-jobs/09SchdWeeksOnParticular.png
[SchdMonthsOnPartDays]: ./media/web-sites-create-web-jobs/10SchdMonthsOnPartDays.png
[SchdMonthsOnPartWeekDays]: ./media/web-sites-create-web-jobs/11SchdMonthsOnPartWeekDays.png
[SchdMonthsOnPartWeekDaysOccurences]: ./media/web-sites-create-web-jobs/12SchdMonthsOnPartWeekDaysOccurences.png
[RunOnce]: ./media/web-sites-create-web-jobs/13RunOnce.png
[WebJobsListWithSeveralJobs]: ./media/web-sites-create-web-jobs/13WebJobsListWithSeveralJobs.png
[WebJobLogs]: ./media/web-sites-create-web-jobs/14WebJobLogs.png
[WebJobDetails]: ./media/web-sites-create-web-jobs/15WebJobDetails.png
[WebJobRunDetails]: ./media/web-sites-create-web-jobs/16WebJobRunDetails.png
[DownloadLogOutput]: ./media/web-sites-create-web-jobs/17DownloadLogOutput.png
[WebJobsLinkToDashboardList]: ./media/web-sites-create-web-jobs/18WebJobsLinkToDashboardList.png
[WebJobsListInJobsDashboard]: ./media/web-sites-create-web-jobs/19WebJobsListInJobsDashboard.png
[LinkToScheduler]: ./media/web-sites-create-web-jobs/31LinkToScheduler.png
[SchedulerPortal]: ./media/web-sites-create-web-jobs/32SchedulerPortal.png
[JobActionPageInScheduler]: ./media/web-sites-create-web-jobs/33JobActionPageInScheduler.png

