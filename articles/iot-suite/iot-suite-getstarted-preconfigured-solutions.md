---
title: aaaGet introduttiva preconfigurato soluzioni | Documenti Microsoft
description: Seguire questa esercitazione toolearn come toodeploy un Azure IoT Suite preconfigurato soluzione.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: a7f46023d26b08de2e8ed48c34c5066a43e3fa38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-preconfigured-solutions"></a>Introduzione a soluzioni hello preconfigurato

Azure IoT Suite [preconfigurato soluzioni] [ lnk-preconfigured-solutions] combinare più Azure IoT servizi toodeliver end-to-end soluzioni che implementano i comuni scenari di business IoT. Hello *monitoraggio remoto* soluzione preconfigurata si connette tooand monitoraggi dei dispositivi. È possibile utilizzare hello soluzione tooanalyze hello flusso di dati dal risultati business tooimprove e dispositivi, eseguendo i processi di rispondere automaticamente toothat flusso di dati.

Questa esercitazione viene illustrato come il monitoraggio remoto hello tooprovision preconfigurato soluzione. Illustra anche funzionalità di base della soluzione hello preconfigurato hello. Molte di queste funzionalità accessibili dalla soluzione hello *dashboard* che distribuisce come parte della soluzione preconfigurata hello:

![Dashboard della soluzione preconfigurata per il monitoraggio remoto][img-dashboard]

toocomplete questa esercitazione, è necessaria una sottoscrizione di Azure attiva.

> [!NOTE]
> Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk_free_trial].

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a>Panoramica dello scenario

Quando si distribuisce hello soluzione preconfigurata di monitoraggio remoto, si viene prepopolato con le risorse che consentono di toostep tramite uno scenario comune di monitoraggio remoto. In questo scenario, diversi dispositivi connessi toohello soluzione segnalano i valori della temperatura imprevisto. Hello nelle sezioni seguenti illustrano come fare per:

* Identificare i dispositivi hello l'invio di valori di temperatura imprevisto.
* Configurare le periferiche toosend più dettagliato di telemetria.
* Risolvere il problema di hello, aggiornare il firmware hello in questi dispositivi.
* Verificare che l'azione ha risolto il problema di hello.

Una funzionalità chiave di questo scenario è che è possibile eseguire in modalità remota tutte queste azioni dal dashboard di soluzione hello. Non è necessario dispositivi toohello accesso fisico.

## <a name="view-hello-solution-dashboard"></a>Dashboard di soluzione hello View

dashboard di soluzione Hello consente soluzione hello distribuito toomanage. Ad esempio, è possibile visualizzare dati di telemetria, aggiungere dispositivi e configurare regole.

1. Quando il provisioning di hello è completato e riquadro hello per la soluzione preconfigurata indica **pronto**, scegliere **avviare** tooopen il portale soluzione di monitoraggio remoto in una nuova scheda.

    ![Avviare la soluzione hello preconfigurato][img-launch-solution]

1. Per impostazione predefinita, il portale di soluzione hello Mostra hello *dashboard*. È possibile passare tooother aree del portale di soluzione hello utilizzando il menu di hello nella parte sinistra della pagina hello hello.

    ![Dashboard della soluzione preconfigurata per il monitoraggio remoto][img-menu]

dashboard Hello Visualizza hello le seguenti informazioni:

* Mappa che visualizza il percorso di hello di ogni dispositivo connesso toohello soluzione. Quando si esegue prima soluzione hello, sono presenti dispositivi simulati 25. Hello dispositivi simulati vengono implementati come processi Web di Azure, le soluzioni hello hello API di Bing mappe tooplot informazioni sulla mappa hello. Vedere hello [domande frequenti su] [ lnk-faq] toolearn come toomake hello dinamici della mappa.
* Un pannello **Cronologia telemetria** che traccia la telemetria di umidità e temperatura da un dispositivo selezionato in tempo quasi reale e visualizza i dati aggregati, ad esempio l'umidità massima, minima e media.
* Un pannello **Cronologia avvisi** che mostra recenti eventi di avviso relativi a valori di telemetria che hanno superato il limite soglia. Negli esempi di toohello inoltre creati dalla soluzione hello preconfigurato, è possibile definire i propri avvisi.
* Un pannello **Processi** che visualizza informazioni sui processi pianificati. È possibile pianificare i propri processi nella pagina **Processi di gestione**.

## <a name="view-alarms"></a>Visualizzare gli avvisi

pannello della cronologia di allarme Hello mostra che i report di cinque dispositivi superiore rispetto a valori di dati di telemetria previsto.

![Cronologia di allarme TODO nel dashboard di soluzione hello][img-alarms]

> [!NOTE]
> Questi avvisi vengono generati da una regola che è incluso nella soluzione hello preconfigurato. Questa regola genera un avviso quando il valore di temperatura hello inviato da un dispositivo supera 60. È possibile definire regole e azioni scegliendo [regole](#add-a-rule) e [azioni](#add-an-action) nel menu a sinistra di hello.

## <a name="view-devices"></a>Visualizzare i dispositivi

Hello *dispositivi* sono elencati tutti i dispositivi registrato hello nella soluzione hello. Dall'elenco di dispositivi hello è possibile visualizzare e modificare i metadati del dispositivo, è possibile aggiungere o rimuovere i dispositivi e richiamare i metodi nei dispositivi. È possibile filtrare e ordinare elenco hello dei dispositivi nell'elenco di dispositivi hello. È inoltre possibile personalizzare le colonne di hello visualizzate nell'elenco di dispositivi hello.

1. Scegliere **dispositivi** elenco dei dispositivi hello tooshow per questa soluzione.

   ![Elenco di dispositivi di visualizzazione hello nel portale di soluzione hello][img-devicelist]

1. elenco dei dispositivi Hello viene inizialmente 25 dispositivi simulati creati dal processo di provisioning hello. È possibile aggiungere soluzioni toohello altri dispositivi simulati e fisico.

1. i dettagli di hello tooview di un dispositivo, scegliere un dispositivo nell'elenco di dispositivi hello.

   ![Visualizzare i dettagli dispositivo hello nel portale di soluzione hello][img-devicedetails]

Hello **dettagli dispositivo** pannello contiene sei sezioni:

* Una raccolta di collegamenti che abilitano si toocustomize hello dispositivo icona, disattivare la periferica hello, aggiungere una regola, richiamano un metodo o inviare un comando. Per un confronto dei comandi (messaggi da dispositivo a cloud) e dei metodi (metodi diretti), vedere [Indicazioni sulle comunicazioni da cloud a dispositivo][lnk-c2d-guidance].
* Hello **dispositivo doppi - tag** sezione consente valori di tag tooedit per dispositivo hello. È possibile visualizzare i valori di tag nell'elenco di dispositivi hello e utilizzare l'elenco dei dispositivi hello toofilter valori tag.
* Hello **dispositivo doppi - proprietà Desired** sezione consente tooset proprietà valori toobe inviati toohello dispositivo.
* Hello **dispositivo doppi - proprietà segnalati** sezione mostra i valori delle proprietà inviati dal dispositivo hello.
* Hello **delle proprietà del dispositivo** sezione Mostra informazioni dal Registro di sistema di hello identità, ad esempio dispositivo hello chiavi id e l'autenticazione.
* Hello **processi recenti** sezione mostra le informazioni su tutti i processi che sono utilizzati di recente come destinazione di questo dispositivo.

## <a name="filter-hello-device-list"></a>Filtrare l'elenco dei dispositivi hello

È possibile utilizzare un filtro toodisplay solo i dispositivi che inviano i valori della temperatura imprevisto. soluzione preconfigurata di monitoraggio remoto Hello include hello **dispositivi integro** filtrare tooshow i dispositivi con un valore di temperatura media maggiore di 60. È possibile anche [creare filtri personalizzati](#add-a-filter).

1. Scegliere **Apri salvato filtro** toodisplay un elenco dei filtri disponibili. Scegliere quindi **dispositivi integro** filtro hello tooapply:

    ![Visualizza l'elenco di filtri hello][img-unhealthy-filter]

1. elenco dei dispositivi Hello verranno visualizzati solo i dispositivi con un valore della temperatura media maggiore di 60.

    ![Elenco dei dispositivi filtrato hello visualizzazione che mostra i dispositivi non integro][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a>Aggiornare le proprietà desiderate

È stato identificato un set di dispositivi per i quali può essere necessaria un'azione correttiva. Tuttavia, si decide che frequenza dati hello di 15 secondi non è sufficiente per una diagnosi del problema hello chiara. Modifica hello telemetria frequenza toofive secondi tooprovide si con ulteriori dati punti toobetter diagnosticare il problema di hello. È possibile distribuire questa configurazione modifica tooyour remota dei dispositivi dal portale di soluzione hello. È possibile modificare hello una volta, valutare l'impatto hello e quindi agire sui risultati di hello.

Seguire questi toorun passaggi un processo che modifica hello **TelemetryInterval** proprietà per i dispositivi interessato hello desiderata. Quando i dispositivi di hello ricevono hello nuovo **TelemetryInterval** valore della proprietà, cambiano i dati di telemetria toosend configurazione ogni cinque secondi anziché ogni 15 secondi:

1. Durante la visualizzazione elenco hello dei dispositivi non integro nell'elenco di dispositivi hello, scegliere **pianificatore di processi**, quindi **Modifica dispositivo doppi**.

1. Chiamare il processo di hello **Modifica intervallo di dati di telemetria**.

1. Modificare il valore di hello di hello **proprietà desiderata** nome **desiderato. Config.TelemetryInterval** toofive secondi.

1. Scegliere **Pianifica**.

    ![Cambiare hello TelemetryInterval proprietà toofive secondi][img-change-interval]

1. È possibile monitorare lo stato di avanzamento hello hello del processo di su hello **Gestione processi** hello portale.

> [!NOTE]
> Se si desidera toochange un valore della proprietà desiderata per un singolo dispositivo, utilizzare hello **proprietà desiderate** sezione hello **dettagli dispositivo** pannello invece di eseguire un processo.

Questo processo Imposta valore hello hello **TelemetryInterval** proprietà in un doppio dispositivo hello desiderata per tutti i dispositivi selezionati dal filtro hello di hello. dispositivi di Hello recupero questo valore da un doppio dispositivo hello e aggiornare il relativo comportamento. Quando un dispositivo recupera ed elabora una proprietà desiderata da un doppio di un dispositivo, viene impostata hello corrispondente valore indicato.

## <a name="invoke-methods"></a>Richiamare i metodi

Durante l'esecuzione di processo hello, noterai nell'elenco di hello dei dispositivi non integro che tutti questi dispositivi dispongono di firmware di precedente (minore di versione 1.6) versioni.

![Hello Vista ha segnalato la versione del firmware per i dispositivi non integro hello][img-old-firmware]

Questa versione del firmware potrebbe essere causa radice di hello di hello imprevisto perché si prevede che altri dispositivi integro sono stati aggiornati di recente tooversion 2.0 i valori della temperatura. È possibile utilizzare predefinito hello **dispositivi firmware precedente** filtrare tooidentify tutti i dispositivi con le versioni precedenti del firmware. Dal portale di hello, è possibile aggiornare in remoto tutti i dispositivi di hello ancora in esecuzione versioni precedenti di firmware:

1. Scegliere **Apri salvato filtro** toodisplay un elenco dei filtri disponibili. Scegliere quindi **dispositivi firmware precedente** filtro hello tooapply:

    ![Visualizza l'elenco di filtri hello][img-old-filter]

1. elenco dei dispositivi Hello verranno visualizzati solo i dispositivi con le versioni precedenti del firmware. Questo elenco include cinque dispositivi hello identificati da hello **dispositivi integro** filtro e tre i dispositivi aggiuntivi:

    ![Elenco dei dispositivi filtrato hello visualizzazione che mostra i dispositivi precedenti][img-filtered-old-list]

1. Scegliere **Pianificatore di processi** e quindi **Richiama metodo**.

1. Impostare **nome del processo** troppo**tooversion aggiornamento Firmware 2.0**.

1. Scegliere **InitiateFirmwareUpdate** come hello **metodo**.

1. Set hello **FwPackageUri** parametro troppo**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.

1. Scegliere **Pianifica**. valore predefinito di Hello è ora toorun processo hello.

    ![Crea processo tooupdate hello firmware dispositivi hello selezionato][img-method-update]

> [!NOTE]
> Se si desidera tooinvoke un metodo su un dispositivo specifico, scegliere **metodi** in hello **dettagli dispositivo** pannello invece di eseguire un processo.

Questo processo richiama hello **InitiateFirmwareUpdate** metodo diretto per tutti i dispositivi di hello selezionati dal filtro hello. Dispositivi rispondono immediatamente tooIoT Hub e quindi avviano processo di aggiornamento del firmware hello in modo asincrono. i dispositivi di Hello fornire informazioni sullo stato relative al processo di aggiornamento del firmware hello tramite valori di proprietà restituito, come illustrato nella seguente schermate hello. Scegliere hello **aggiornamento** informazioni di hello icona tooupdate negli elenchi di dispositivo e processo hello:

![Elenco di processi con esecuzione elenco aggiornamento firmware di hello][img-update-1]
![elenco dei dispositivi che mostra lo stato di aggiornamento del firmware][img-update-2]
![processo elenco visualizzazione hello firmware aggiornamento dell'elenco completo][img-update-3]

> [!NOTE]
> In un ambiente di produzione, è possibile pianificare processi toorun durante una finestra di manutenzione.

## <a name="scenario-review"></a>Analisi dello scenario

In questo scenario, è stato identificato un potenziale problema con alcuni dispositivi in uso remoti utilizzando la cronologia di allarme hello in dashboard hello e un filtro. È quindi il filtro utilizzato hello e tooremotely un processo configurare hello dispositivi tooprovide più informazioni toohelp diagnosticare il problema di hello. Infine, è stato utilizzato un filtro e una manutenzione tooschedule processo per dispositivi hello interessato. Se si restituisce toohello dashboard, è possibile controllare che non sono più presenti eventuali avvisi provenienti da dispositivi nella soluzione. È possibile utilizzare un filtro tooverify che hello firmware viene aggiornato in tutti i dispositivi di hello nella soluzione e che sono presenti dispositivi non è più integri:

![Filtro che mostra come il firmware di tutti i dispositivi sia aggiornato][img-updated]

![Filtro che mostra come tutti i dispositivi siano integri][img-healthy]

## <a name="other-features"></a>Altre funzionalità

Hello nelle sezioni seguenti vengono descrivono alcune funzionalità aggiuntive di hello soluzione preconfigurata di monitoraggio remoto che non sono descritte come parte dello scenario precedente hello.

### <a name="customize-columns"></a>Personalizzare le colonne

È possibile personalizzare hello informazioni visualizzate nell'elenco di dispositivi hello scegliendo **editor colonna**. È possibile aggiungere e rimuovere colonne che visualizzano i valori dei tag e delle proprietà segnalate, nonché riordinare e rinominare le colonne:

   ![Elenco di colonne editor ion hello dispositivo][img-columneditor]

### <a name="customize-hello-device-icon"></a>Personalizzare l'icona di dispositivi hello

È possibile personalizzare l'icona di dispositivi hello visualizzato nell'elenco di dispositivi hello da hello **dettagli dispositivo** pannello come indicato di seguito:

1. Scegliere hello di hello matita icona tooopen **Modifica immagine** pannello per un dispositivo:

   ![Editor di immagini per il dispositivo: apertura][img-startimageedit]

1. Caricare una nuova immagine o utilizzare una delle immagini esistenti hello e quindi scegliere **salvare**:

   ![Editor di immagini per il dispositivo: modifica][img-imageedit]

1. Hello selezionati sono ora viene visualizzata in hello **icona** colonna per il dispositivo hello.

> [!NOTE]
> immagine di Hello viene archiviata nell'archiviazione blob. Un tag in un doppio dispositivo hello contiene un'immagine di toohello collegamento nell'archiviazione blob.

### <a name="add-a-device"></a>Aggiungere un dispositivo

Quando si distribuisce la soluzione hello preconfigurato, automaticamente effettuato il provisioning di 25 dispositivi di esempio che è possibile visualizzare nell'elenco di dispositivi hello Si tratta di *dispositivi simulati* in esecuzione in un processo Web di Azure. Dispositivi simulati semplificano automaticamente tooexperiment con la soluzione hello preconfigurato senza hello necessità toodeploy reale fisico i dispositivi. Se si desidera tooconnect una soluzione di toohello dispositivo reale, vedere hello [connettersi toohello il dispositivo remoto monitoraggio soluzione preconfigurata] [ lnk-connect-rm] esercitazione.

Hello passaggi seguenti viene illustrato come una soluzione di toohello dispositivo simulato tooadd:

1. Passare l'elenco dei dispositivi toohello indietro.

1. Scegliere un dispositivo, tooadd **+ Aggiungi dispositivi** nell'angolo inferiore sinistro di hello.

   ![Aggiunta di una soluzione di toohello preconfigurato dispositivo][img-adddevice]

1. Scegliere **Aggiungi nuovo** su hello **dispositivo simulato** riquadro.

   ![Impostare i dettagli del nuovo dispositivo nel dashboard][img-addnew]

   In aggiunta toocreating un nuovo dispositivo simulato, è anche possibile aggiungere un dispositivo fisico se si sceglie toocreate un **dispositivo personalizzato**. toolearn più sulla connessione soluzione toohello dispositivi fisici, vedere [connettersi il toohello dispositivo IoT Suite soluzione preconfigurata di monitoraggio remoto][lnk-connect-rm].

1. Selezionare **Let me define my own Device ID** (Definire l'ID dispositivo personale) e immettere un nome di ID dispositivo univoco, ad esempio **mydevice_01**.

1. Scegliere **Create**.

   ![Salvare un nuovo dispositivo][img-definedevice]

1. Nel passaggio 3 di **aggiunge un dispositivo simulato**, scegliere **eseguita** tooreturn toohello elenco dei dispositivi.

1. È possibile visualizzare il dispositivo **esecuzione** nell'elenco di dispositivi hello.

    ![Visualizzare il nuovo dispositivo nell'elenco dei dispositivi][img-runningnew]

1. È inoltre possibile visualizzare hello simulato telemetria dal dispositivo nuovo dashboard hello:

    ![Visualizzare i dati di telemetria dal nuovo dispositivo][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a>Disabilitare e rimuovere un dispositivo

È possibile disabilitare un dispositivo e dopo aver disabilitato è possibile rimuoverlo:

![Disabilitare e rimuovere un dispositivo][img-disable]

### <a name="add-a-rule"></a>Aggiungere una regola

Non esistono regole per il nuovo dispositivo di hello che appena aggiunto. In questa sezione aggiungere una regola che attiva un avviso quando la temperatura hello restituite da hello nuovo dispositivo supera gradi 47. Prima di iniziare, si noti che hello telemetria per nuovo dispositivo di hello dashboard hello dimostra temperatura dispositivo hello non superi mai il 45 gradi.

1. Passare l'elenco dei dispositivi toohello indietro.

1. tooadd una regola per il dispositivo di hello, selezionare il nuovo dispositivo in hello **elenco dispositivi**, quindi scegliere **Aggiungi regola**.

1. Creare una regola che utilizza **temperatura** come campo di dati hello e utilizza **AlarmTemp** come output di hello quando temperatura hello supera gradi 47:

    ![Aggiungere una regola per il dispositivo][img-adddevicerule]

1. Scegliere le modifiche, toosave **salvare e visualizzare le regole**.

1. Scegliere **comandi** nel riquadro dei dettagli dispositivo hello per il nuovo dispositivo di hello.

    ![Aggiungere una regola per il dispositivo][img-adddevicerule2]

1. Selezionare **ChangeSetPointTemp** dall'elenco di comandi hello e set **SetPointTemp** too45. Scegliere quindi **Invia comando**.

    ![Aggiungere una regola per il dispositivo][img-adddevicerule3]

1. Spostarsi indietro toohello dashboard. Dopo un breve periodo di tempo, si vedrà una nuova voce di hello **cronologia allarme** riquadro quando temperatura hello segnalato dal nuovo dispositivo supera la soglia di 47 gradi hello:

    ![Aggiungere una regola per il dispositivo][img-adddevicerule4]

1. È possibile esaminare e modificare tutte le regole in hello **regole** pagina del dashboard hello:

    ![Elenco delle regole per il dispositivo][img-rules]

1. È possibile esaminare e modificare tutte le azioni che possono essere eseguite nella regola tooa risposta su hello hello **azioni** pagina del dashboard hello:

    ![Elenco delle azioni per il dispositivo][img-actions]

> [!NOTE]
> È possibile toodefine azioni che è possono inviare un messaggio di posta elettronica o SMS nella risposta tooa regola o integrare con un sistema line-of-business tramite un [logica App][lnk-logic-apps]. Per ulteriori informazioni, vedere hello [tooyour connessione logica App monitoraggio remoto di Azure IoT Suite preconfigurato soluzione][lnk-logicapptutorial].

### <a name="manage-filters"></a>Gestire i filtri

Nell'elenco di dispositivi hello, è possibile creare, salvare e ricaricare i filtri toodisplay un elenco personalizzato di hub tooyour connessi i dispositivi. toocreate un filtro:

1. Scegliere l'icona di filtro modifica hello sopra l'elenco di hello dei dispositivi:

    ![Editor filtri hello aperto][img-editfiltericon]

1. In hello **editor filtri**, aggiungere i campi di hello, operatori e valori toofilter hello dispositivo elenco. È possibile aggiungere più clausole toorefine il filtro. Scegliere **filtro** filtro hello tooapply:

    ![Creare un filtro][img-filtereditor]

1. In questo esempio hello viene filtrato dal produttore e il numero di modello:

    ![Elenco filtrato][img-filterelist]

1. toosave il filtro con un nome personalizzato, scegliere hello **salvare come** icona:

    ![Salvare un filtro][img-savefilter]

1. tooreapply un filtro è stato salvato in precedenza, scegliere hello **Apri salvato filtro** icona:

    ![Aprire un filtro][img-openfilter]

È possibile creare filtri basati sull'ID dispositivo, sullo stato del dispositivo, sulle proprietà desiderate, sulle proprietà segnalate e sui tag. Aggiungere il proprio dispositivo tooa tag personalizzati in hello **tag** sezione di hello **dettagli dispositivo** pannello oppure eseguire un processo tooupdate tag su più dispositivi.

> [!NOTE]
> In hello **editor filtri**, è possibile utilizzare hello **visualizzazione avanzata** direttamente testo della query hello tooedit.

### <a name="commands"></a>Comandi:

Da hello **dettagli dispositivo** pannello, è possibile inviare dispositivo toohello comandi. Al primo avvio di un dispositivo invia informazioni hello comandi che supporta toohello soluzione. Per una descrizione delle differenze di hello tra i comandi e i metodi, vedere [opzioni cloud a dispositivo IoT Hub Azure][lnk-c2d-guidance].

1. Scegliere **comandi** in hello **dettagli dispositivo** pannello per il dispositivo selezionato hello:

   ![Comandi del dispositivo nel dashboard][img-devicecommands]

1. Selezionare **PingDevice** dall'elenco di comandi hello.

1. Scegliere **Invia comando**.

1. È possibile visualizzare lo stato di hello del comando hello nella cronologia del comando hello.

   ![Stato dei comandi nel dashboard][img-pingcommand]

soluzione Hello tiene traccia dello stato di hello di ogni comando che viene inviato. Risultato hello è inizialmente **in sospeso**. Quando il dispositivo di hello segnala che è eseguita comando hello, risultato hello viene impostato troppo**successo**.

## <a name="behind-hello-scenes"></a>Background hello

Quando si distribuisce una soluzione preconfigurata, il processo di distribuzione hello crea più risorse hello Azure sottoscrizione selezionata. È possibile visualizzare queste risorse in Azure hello [portale][lnk-portal]. il processo di distribuzione Hello crea un **gruppo di risorse** con un nome basato sul nome hello scelto per la soluzione preconfigurata:

![Soluzione preconfigurata in hello portale di Azure][img-portal]

È possibile visualizzare le impostazioni di hello di ogni risorsa selezionandolo nell'elenco di hello delle risorse nel gruppo di risorse hello.

È anche possibile visualizzare il codice sorgente hello per soluzione hello preconfigurato. il codice sorgente soluzione preconfigurata di monitoraggio remoto Hello è hello [azure iot-remoto monitoraggio] [ lnk-rmgithub] repository GitHub:

* Hello **DeviceAdministration** cartella contiene il codice sorgente hello per dashboard hello.
* Hello **simulatore** cartella contiene il codice sorgente hello per dispositivo simulato hello.
* Hello **EventProcessor** cartella contiene il codice sorgente hello per il processo di back-end hello che gestisce i dati di telemetria hello in arrivo.

Al termine, è possibile eliminare la soluzione hello preconfigurato dalla sottoscrizione di Azure su hello [azureiotsuite.com] [ lnk-azureiotsuite] sito. Questo sito consente tooeasily Elimina che tutte le risorse che è sono eseguito il provisioning durante la creazione di soluzioni hello preconfigurato di hello.

> [!NOTE]
> tooensure di eliminare tutti gli elementi correlati soluzione toohello preconfigurato, l'eliminazione hello [azureiotsuite.com] [ lnk-azureiotsuite] del sito e non viene eliminato il gruppo di risorse hello nel portale di hello.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver distribuito una soluzione appropriata preconfigurato, è possibile continuare introduzione IoT Suite leggendo hello seguenti articoli:

* [Procedura dettagliata della soluzione preconfigurata per il monitoraggio remoto][lnk-rm-walkthrough]
* [Connettere la soluzione preconfigurata di monitoraggio remoto toohello di dispositivo][lnk-connect-rm]
* [Autorizzazioni nel sito azureiotsuite.com hello][lnk-permissions]

[img-launch-solution]: media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md