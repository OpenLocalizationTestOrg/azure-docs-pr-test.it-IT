---
title: aaaMonitor e gestire dati pipeline - Azure | Documenti Microsoft
description: Informazioni su come toouse hello monitoraggio e gestione toomonitor app e gestire le pipeline e data factory di Azure.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a>Monitorare e gestire le pipeline di Data Factory di Azure utilizzando app hello di monitoraggio e gestione
> [!div class="op_single_selector"]
> * [Con il portale di Azure/Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Con l'app di monitoraggio e gestione](data-factory-monitor-manage-app.md)
>
>

In questo articolo viene descritto come toouse hello toomonitor app di gestione e monitoraggio, gestire ed eseguire il debug le pipeline di Data Factory. Fornisce inoltre informazioni su come toocreate avvisi tooget notificata in caso di errori. È possibile iniziare con un'applicazione hello da hello guardando seguente video:

> [!NOTE]
> interfaccia utente di Hello illustrato hello video potrebbe non corrispondere esattamente ciò che viene visualizzato nel portale di hello. È leggermente meno recente, ma i concetti rimangono hello stesso. 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a>Avviare l'applicazione di monitoraggio e gestione hello
hello toolaunch monitoraggio e gestione app, fare clic su hello **monitoraggio e gestione** riquadro hello **Data Factory** pannello per il data factory.

![Monitoraggio delle sezione nella home page di hello Data Factory](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

Dovrebbe essere hello monitoraggio e gestione delle app aperte in una finestra separata.  

![App di monitoraggio e gestione](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> Se viene visualizzato il browser web hello è bloccata su "Autorizzazione …", deselezionare hello **bloccare i cookie di terze parti e i dati del sito** - casella di controllo o mantenere è selezionata, creare un'eccezione per **login.microsoftonline.com** , quindi riprovare a eseguire tooopen hello app.


Nell'elenco di attività Windows hello nel riquadro centrale di hello, verrà visualizzata una finestra di attività per ogni esecuzione di un'attività. Ad esempio, se hai hello attività pianificata toorun ogni ora per cinque ore, vedrai cinque windows attività associata a sezioni di dati di cinque. Se non viene visualizzato windows attività nell'elenco di hello nella parte inferiore di hello, hello seguenti:
 
- Hello aggiornamento **ora di inizio** e **ora di fine** filtri hello toomatch superiore hello avviare e fine della pipeline e quindi fare clic su hello **applica** pulsante.  
- elenco di attività Windows Hello non viene aggiornato automaticamente. Fare clic su hello **aggiornamento** pulsante sulla barra degli strumenti hello hello **attività Windows** elenco.  

Se non è un tootest applicazione Data Factory questi passaggi con, hello esercitazione: [copiare i dati da archiviazione Blob tooSQL Database tramite Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="understand-hello-monitoring-and-management-app"></a>Comprendere hello monitoraggio e Gestione applicazione
Sono disponibili tre schede a sinistra di hello: **Esplora inventario risorse**, **visualizzazioni di monitoraggio**, e **avvisi**. prima scheda Hello (**Esplora inventario risorse**) è selezionata per impostazione predefinita.

### <a name="resource-explorer"></a>Scheda Resource Explorer
Verrà visualizzata hello seguente:

* Esplora inventario risorse Hello **visualizzazione ad albero** nel riquadro di sinistra hello.
* Hello **vista diagramma** nella parte superiore di hello nel riquadro centrale hello.
* Hello **attività Windows** elenco nella parte inferiore di hello nel riquadro centrale hello.
* Hello **proprietà**, **attività finestra Esplora**, e **Script** schede nel riquadro di destra hello.

In Esplora inventario risorse, visualizzare tutte le risorse (pipeline, i set di dati, servizi collegati) nella data factory di hello in una visualizzazione albero. Quando si seleziona un oggetto in Esplora risorse:

* Hello associati Data Factory di entità viene evidenziata in vista diagramma hello.
* [Associata windows attività](data-factory-scheduling-and-execution.md) sono evidenziate nell'elenco di attività Windows hello nella parte inferiore di hello.  
* proprietà Hello dell'oggetto selezionato hello vengono visualizzate nella finestra Proprietà hello nel riquadro di destra hello.
* Hello definizione JSON dell'oggetto selezionato hello è visibile, se applicabile. Ad esempio: un servizio collegato, un set di dati o una pipeline.

![Scheda Resource Explorer](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

Vedere hello [pianificazione ed esecuzione](data-factory-scheduling-and-execution.md) articolo per informazioni dettagliate sulle finestre di attività.

### <a name="diagram-view"></a>Vista Diagramma
Vista diagramma di una data factory Hello offre un unico riquadro della finestra effetto cristallo toomonitor e gestire una data factory e delle relative risorse. Quando si seleziona un'entità di Data Factory (set di dati/pipeline) in vista diagramma hello:

* Hello data factory entità selezionata nella visualizzazione ad albero di hello.
* Hello associata l'attività di windows sono evidenziate nell'elenco di attività Windows hello.
* proprietà Hello dell'oggetto selezionato hello vengono visualizzate nella finestra Proprietà hello.

Quando la pipeline hello è attivata (non in pausa), questo viene visualizzato con una linea verde:

![Pipeline in esecuzione](./media/data-factory-monitor-manage-app/PipelineRunning.png)

È possibile sospendere, riprendere o terminare una pipeline selezionandolo nella vista diagramma hello e utilizzando i pulsanti di hello hello barra dei comandi.

![Sospendere o riprendere hello barra dei comandi](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
Esistono tre pulsanti della barra di comando per la pipeline di hello in vista diagramma hello. È possibile utilizzare pipeline hello toopause hello secondo pulsante. La sospensione non termina l'attività attualmente in esecuzione hello e consente loro di procedere toocompletion. il terzo pulsante Hello sospende pipeline hello e termina l'esecuzione di attività esistenti. primo pulsante Hello riprende pipeline hello. Quando la pipeline viene sospesa, il colore di hello della pipeline hello cambia. Ad esempio, una pipeline sospesa l'aspetto in hello seguente immagine: 

![Pipeline in pausa](./media/data-factory-monitor-manage-app/PipelinePaused.png)

È possibile selezionare più due o più pipeline tasto Ctrl hello. È possibile utilizzare toopause o ripresa di hello comando barra dei pulsanti più pipeline contemporaneamente.

È anche possibile fare doppio clic su una pipeline e selezionare le opzioni toosuspend, riprendere o terminare una pipeline. 

![Menu di scelta rapida per le pipeline](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

Fare clic su hello **pipeline aprire** opzione toosee tutte le attività di hello nella pipeline hello. 

![Menu Apri pipeline](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

Nella visualizzazione pipeline hello aperto, vedrai tutte le attività nella pipeline hello. In questo esempio è presente soltanto l'attività di copia. 

![Pipeline aperta](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

toogo nuovamente toohello visualizzazione precedente, fare clic sul nome di factory hello dati in menu di navigazione hello nella parte superiore di hello.

Nella visualizzazione pipeline hello, quando si seleziona un set di dati di output o quando si sposta il puntatore del mouse su set di dati con output di hello vedrai finestra popup di attività Windows hello per tale set di dati.

![Finestra popup di Activity Windows (Finestre attività)](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

È possibile fare clic una finestra toosee di attività per tale hello **proprietà** finestra nel riquadro di destra hello.

![Proprietà della finestra attività](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

Nel riquadro destro hello passare toohello **attività finestra Esplora** scheda toosee ulteriori dettagli.

![Esplora finestre attività](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

Anche possibile vedere **risolto variabili** a ogni tentativo di esecuzione per un'attività in hello **tentativi** sezione.

![Variabili risolte](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

Passare toohello **Script** scheda toosee hello JSON Crea script per definizione per l'oggetto selezionato hello.   

![Scheda Script](./media/data-factory-monitor-manage-app/ScriptTab.png)

Le finestre attività vengono visualizzate in tre posizioni:

* Hello Windows attività popup hello vista diagramma (riquadro centrale).
* nel riquadro di destra hello, Hello attività Esplora risorse.
* elenco di attività Windows Hello nel riquadro inferiore hello.

Nel messaggio popup di attività Windows hello e attività Esplora risorse, è possibile scorrere toohello settimana precedente e hello settimana successiva tramite hello frecce destra e sinistra.

![Freccia sinistra/destra in Activity Window Explorer (Esplora finestra attività)](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

Nella parte inferiore di hello di hello vista diagramma, vedrai questi pulsanti: Zoom avanti, Zoom indietro, tooFit Zoom, eseguire lo Zoom 100%, il layout di blocco. Hello **layout blocco** pulsante consente di spostare accidentalmente tabelle e pipeline in vista diagramma hello. È attivo per impostazione predefinita. È possibile disattivarla e spostare le entità nel diagramma hello. Quando si disattiva, è possibile utilizzare le pipeline e tabelle di hello ultimo pulsante tooautomatically posizione. È inoltre possibile ingrandire o ridurre utilizzando rotellina del mouse hello.

![Comandi di zoom nella visualizzazione diagramma](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a>Elenco Activity Windows (Finestre attività)
elenco di attività Windows Hello nella parte inferiore di hello del riquadro centrale hello Visualizza tutte le finestre attività per i set di dati di hello selezionato in Esplora inventario risorse hello o hello vista diagramma. Per impostazione predefinita, l'elenco di hello è in ordine decrescente, il che significa che vedere finestra attività hello più recente nella parte superiore di hello.

![Elenco Activity Windows (Finestre attività)](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

Questo elenco non vengono aggiornati automaticamente, quindi utilizzare hello aggiornamento pulsante hello barra degli strumenti toomanually aggiornarlo.  

Le finestre attività possono essere in uno dei seguenti stati hello:

<table>
<tr>
    <th align="left">Stato</th><th align="left">Stato secondario</th><th align="left">Descrizione</th>
</tr>
<tr>
    <td rowspan="8">Waiting</td><td>ScheduleTime</td><td>tempo di Hello non venga per toorun finestra attività di hello.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>le dipendenze upstream Hello non sono pronte.</td>
</tr>
<tr>
<td>ComputeResources</td><td>risorse di calcolo Hello non sono disponibili.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>Tutte le istanze di attività hello sono occupate in esecuzione altre attività di windows.</td>
</tr>
<tr>
<td>ActivityResume</td><td>attività di Hello è sospesa e non può eseguire windows attività hello fino a quando non viene ripreso.</td>
</tr>
<tr>
<td>Retry</td><td>l'esecuzione dell'attività Hello verrà riprovata.</td>
</tr>
<tr>
<td>Convalida</td><td>La convalida non è ancora stata avviata.</td>
</tr>
<tr>
<td>ValidationRetry</td><td>La convalida è in attesa toobe ripetuta.</td>
</tr>
<tr>
<tr>
<td rowspan="2">InProgress</td><td>Convalida in corso.</td><td>La convalida è in esecuzione.</td>
</tr>
<td>-</td>
<td>finestra attività Hello è stato elaborato.</td>
</tr>
<tr>
<td rowspan="4">Operazione non riuscita</td><td>TimedOut</td><td>l'esecuzione dell'attività Hello ha richiesto più tempo rispetto a quelle consentite dall'attività hello.</td>
</tr>
<tr>
<td>Canceled</td><td>finestra attività Hello è stata annullata dall'utente.</td>
</tr>
<tr>
<td>Convalida</td><td>Convalida non riuscita.</td>
</tr>
<tr>
<td>-</td><td>finestra attività Hello Impossibile toobe generato o convalidato.</td>
</tr>
<td>Ready</td><td>-</td><td>finestra attività Hello è pronto per l'utilizzo.</td>
</tr>
<tr>
<td>Skipped</td><td>-</td><td>finestra attività Hello non è stato elaborato.</td>
</tr>
<tr>
<td>Nessuno</td><td>-</td><td>Una finestra attività utilizzato tooexist con un altro stato, ma è stata reimpostata.</td>
</tr>
</table>


Quando si fa clic su una finestra delle attività nell'elenco di hello, vedrai dettagli in hello **attività Esplora** o hello **proprietà** finestra hello destra.

![Esplora finestre attività](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a>Aggiornare le finestre attività
Dettagli Hello non vengono aggiornati automaticamente, pertanto utilizzare il pulsante di aggiornamento hello (secondo pulsante hello) sulla barra toomanually Aggiorna hello attività windows elenco dei comandi hello.  

### <a name="properties-window"></a>Finestra Properties
finestra Proprietà Hello è nel riquadro di destra hello di hello monitoraggio e gestione delle app.

![Finestra Properties](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

Vengono visualizzate le proprietà per l'elemento hello selezionato in Esplora risorse (visualizzazione struttura ad albero), hello vista diagramma o elenco di attività Windows.

### <a name="activity-window-explorer"></a>Esplora finestre attività
Hello **attività finestra Esplora** finestra Trova nel riquadro di destra hello di hello monitoraggio e gestione delle app. Visualizza informazioni dettagliate su finestra hello attività selezionate nella finestra popup di attività Windows hello o un elenco di attività Windows hello.

![Esplora finestre attività](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

È possibile passare la finestra di attività tooanother facendo clic su di essa nella visualizzazione di calendario hello nella parte superiore di hello. È inoltre possibile utilizzare i tasti freccia sinistra/destra di hello Windows di attività superiore toosee hello da hello settimana precedente o hello settimana successiva.

È possibile utilizzare i pulsanti della barra degli strumenti hello nella finestra attività di hello inferiore riquadro toorerun hello o aggiornare i dettagli di hello nel riquadro di hello.

### <a name="script"></a>Script
È possibile utilizzare hello **Script** hello tooview scheda Definizione JSON di hello selezionato entità Data Factory (servizio collegato, set di dati o pipeline).

![Scheda Script](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a>Uso delle viste di sistema
Monitoraggio e gestione di app Hello include viste di sistema predefinito (**windows attività recente**, **attività windows non**, **finestre attività In corso**) che consentono di windows di recente o non è riuscita o in corso attività tooview per la data factory.

Passare toohello **visualizzazioni di monitoraggio** scheda sinistra hello facendovi clic sopra.

![Scheda Monitoring Views](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

Al momento sono disponibili tre viste di sistema supportate. Selezionare un'opzione toosee recenti attività windows, windows di attività non riuscita o in corso attività di windows nell'elenco di attività Windows hello (nella parte inferiore di hello del riquadro centrale hello).

Quando si seleziona hello **windows attività recente** opzione, viene visualizzato recente tutte le finestre attività in ordine decrescente di hello **ora dell'ultimo tentativo**.

È possibile utilizzare hello **attività windows non** visualizzare le finestre attività toosee tutti non riuscita nell'elenco di hello. Selezionare una finestra di attività non riuscita in hello elenco toosee dettagli in hello **proprietà** finestra o hello **attività finestra Esplora**. È anche possibile scaricare i log relativi a una finestra attività non riuscita.

## <a name="sort-and-filter-activity-windows"></a>Ordinamento e filtro delle finestre attività
Hello modifica **ora di inizio** e **ora di fine** impostazioni nel comando hello barra toofilter windows di attività. Dopo aver modificato hello ora di inizio e fine, fare clic su hello pulsante Avanti toohello fine ora toorefresh hello attività elenco di Windows.

![Ora di inizio e ora di fine](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> Tutte le volte in cui sono attualmente in formato UTC in app di gestione e monitoraggio hello.
>
>

In hello **elenco attività Windows**, fare clic sul nome di una colonna hello (ad esempio: stato).

![Menu della colonna nell'elenco Activity Windows (Finestre attività)](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

È possibile eseguire il seguente hello:

* Applicare l'ordinamento crescente.
* Applicare l'ordinamento decrescente.
* Filtrare in base a uno o più valori, ad esempio Pronto, In attesa e così via.

Quando si specifica un filtro su una colonna, verrà visualizzato il pulsante di filtro hello abilitato per la colonna, che indica che i valori nella colonna hello hello sono valori filtrati.

![Filtrare una colonna dell'elenco di attività Windows hello](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

È possibile utilizzare hello stessi filtri di tooclear finestra popup. tooclear tutti i filtri per l'elenco di attività Windows hello, fare clic su pulsante Cancella filtro hello hello barra dei comandi.

![Cancella tutti i filtri per l'elenco di attività Windows hello](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a>Esecuzione di azioni batch
### <a name="rerun-selected-activity-windows"></a>Rieseguire finestre attività selezionate
Selezionare una finestra attività, fare clic su hello freccia giù per hello primo pulsante e selezionare **Riesegui** / **eseguire di nuovo con monte nella pipeline**. Quando si seleziona hello **eseguire di nuovo con monte nella pipeline** , opzione consente di rieseguire anche tutte le finestre attività upstream.
    ![Rieseguire una finestra attività](./media/data-factory-monitor-manage-app/ReRunSlice.png)

È anche possibile selezionare più finestre di attività nell'elenco di hello ed eseguirli di nuovo in hello contemporaneamente. È possibile impostare toofilter attività in base allo stato hello (ad esempio: **non riuscito**) e quindi eseguire nuovamente windows attività hello non è riuscita dopo aver risolto il problema hello che causa toofail di windows hello attività. Vedere la seguente sezione per informazioni dettagliate sui filtri delle finestre di attività nell'elenco di hello hello.  

### <a name="pauseresume-multiple-pipelines"></a>Sospendere o riprendere l'esecuzione di più pipeline
È possibile multiselect due o più pipeline tasto Ctrl hello. È possibile utilizzare i pulsanti della barra di comando hello (che vengono evidenziati nel rettangolo rosso hello hello seguente immagine) o ripresa di toopause li.

![Sospendere o riprendere hello barra dei comandi](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a>Creare avvisi
Hello **avvisi** pagina consente di creare un avviso e gli avvisi esistenti Visualizza/Modifica/eliminazione. Permette anche di abilitare o disabilitare un avviso. toosee hello pagina avvisi, fare clic su hello **avvisi** scheda.

![Scheda Alerts](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a>toocreate un avviso
1. Fare clic su **Aggiungi avviso** tooadd un avviso. Vedrai hello **dettagli** pagina.

    ![Creazione di avvisi: pagina Details](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. Specificare hello **nome** e **descrizione** avviso hello e fare clic su **Avanti**. Dovrebbe essere hello **filtri** pagina.

    ![Creazione di avvisi: pagina Filters](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. Seleziona hello **evento**, **stato**, e **substatus** che si desidera toocreate (facoltativo) un servizio Data Factory di avviso per e fare clic su **Avanti**. Dovrebbe essere hello **destinatari** pagina.

    ![Creazione di avvisi: pagina Recipients](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. Seleziona hello **gli amministratori delle sottoscrizioni di posta elettronica** opzione e/o immettere un **e-mail amministratore aggiuntiva**, fare clic su **fine**. Verrà visualizzato l'avviso hello nell'elenco di hello.

    ![Elenco degli avvisi](./media/data-factory-monitor-manage-app/AlertsList.png)

Nell'elenco di avvisi hello, utilizzare i pulsanti di hello associati hello avviso tooedit/delete/Abilita/disabilita un avviso.

### <a name="eventstatussubstatus"></a>Evento, stato e stato secondario
Hello nella tabella seguente sono elencate per hello eventi disponibili e gli stati (e stati secondari).

| Nome evento | Stato | Stato secondario |
| --- | --- | --- |
| Esecuzione attività avviata |Started |Avvio in corso |
| Esecuzione attività terminata |Operazione completata |Operazione completata |
| Esecuzione attività terminata |Non riuscito |Allocazione risorse non riuscita<br/><br/>Esecuzione non riuscita<br/><br/>Timed Out<br/><br/>Failed Validation<br/><br/>Abbandonato |
| Creazione cluster HDI su richiesta avviata |Started |-|
| Creazione cluster HDI su richiesta completata |Operazione completata |-|
| Cluster HDI su richiesta eliminato |Operazione completata |-|

### <a name="tooedit-delete-or-disable-an-alert"></a>tooedit, eliminare o disabilitare un avviso

Utilizzare hello seguente tooedit pulsanti (evidenziati in rosso), eliminare o disabilitare un avviso.

![Pulsanti degli avvisi](./media/data-factory-monitor-manage-app/AlertButtons.png)
