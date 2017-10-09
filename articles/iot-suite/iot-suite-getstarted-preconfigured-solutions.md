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
# <a name="get-started-with-hello-preconfigured-solutions"></a><span data-ttu-id="9f058-103">Introduzione a soluzioni hello preconfigurato</span><span class="sxs-lookup"><span data-stu-id="9f058-103">Get started with hello preconfigured solutions</span></span>

<span data-ttu-id="9f058-104">Azure IoT Suite [preconfigurato soluzioni] [ lnk-preconfigured-solutions] combinare più Azure IoT servizi toodeliver end-to-end soluzioni che implementano i comuni scenari di business IoT.</span><span class="sxs-lookup"><span data-stu-id="9f058-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="9f058-105">Hello *monitoraggio remoto* soluzione preconfigurata si connette tooand monitoraggi dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="9f058-105">hello *remote monitoring* preconfigured solution connects tooand monitors your devices.</span></span> <span data-ttu-id="9f058-106">È possibile utilizzare hello soluzione tooanalyze hello flusso di dati dal risultati business tooimprove e dispositivi, eseguendo i processi di rispondere automaticamente toothat flusso di dati.</span><span class="sxs-lookup"><span data-stu-id="9f058-106">You can use hello solution tooanalyze hello stream of data from your devices and tooimprove business outcomes by making processes respond automatically toothat stream of data.</span></span>

<span data-ttu-id="9f058-107">Questa esercitazione viene illustrato come il monitoraggio remoto hello tooprovision preconfigurato soluzione.</span><span class="sxs-lookup"><span data-stu-id="9f058-107">This tutorial shows you how tooprovision hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="9f058-108">Illustra anche funzionalità di base della soluzione hello preconfigurato hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="9f058-109">Molte di queste funzionalità accessibili dalla soluzione hello *dashboard* che distribuisce come parte della soluzione preconfigurata hello:</span><span class="sxs-lookup"><span data-stu-id="9f058-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![Dashboard della soluzione preconfigurata per il monitoraggio remoto][img-dashboard]

<span data-ttu-id="9f058-111">toocomplete questa esercitazione, è necessaria una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="9f058-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="9f058-112">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="9f058-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9f058-113">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="9f058-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="9f058-114">Panoramica dello scenario</span><span class="sxs-lookup"><span data-stu-id="9f058-114">Scenario overview</span></span>

<span data-ttu-id="9f058-115">Quando si distribuisce hello soluzione preconfigurata di monitoraggio remoto, si viene prepopolato con le risorse che consentono di toostep tramite uno scenario comune di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="9f058-115">When you deploy hello remote monitoring preconfigured solution, it is prepopulated with resources that enable you toostep through a common remote monitoring scenario.</span></span> <span data-ttu-id="9f058-116">In questo scenario, diversi dispositivi connessi toohello soluzione segnalano i valori della temperatura imprevisto.</span><span class="sxs-lookup"><span data-stu-id="9f058-116">In this scenario, several devices connected toohello solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="9f058-117">Hello nelle sezioni seguenti illustrano come fare per:</span><span class="sxs-lookup"><span data-stu-id="9f058-117">hello following sections show you how to:</span></span>

* <span data-ttu-id="9f058-118">Identificare i dispositivi hello l'invio di valori di temperatura imprevisto.</span><span class="sxs-lookup"><span data-stu-id="9f058-118">Identify hello devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="9f058-119">Configurare le periferiche toosend più dettagliato di telemetria.</span><span class="sxs-lookup"><span data-stu-id="9f058-119">Configure these devices toosend more detailed telemetry.</span></span>
* <span data-ttu-id="9f058-120">Risolvere il problema di hello, aggiornare il firmware hello in questi dispositivi.</span><span class="sxs-lookup"><span data-stu-id="9f058-120">Fix hello problem by updating hello firmware on these devices.</span></span>
* <span data-ttu-id="9f058-121">Verificare che l'azione ha risolto il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-121">Verify that your action has resolved hello issue.</span></span>

<span data-ttu-id="9f058-122">Una funzionalità chiave di questo scenario è che è possibile eseguire in modalità remota tutte queste azioni dal dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-122">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="9f058-123">Non è necessario dispositivi toohello accesso fisico.</span><span class="sxs-lookup"><span data-stu-id="9f058-123">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="9f058-124">Dashboard di soluzione hello View</span><span class="sxs-lookup"><span data-stu-id="9f058-124">View hello solution dashboard</span></span>

<span data-ttu-id="9f058-125">dashboard di soluzione Hello consente soluzione hello distribuito toomanage.</span><span class="sxs-lookup"><span data-stu-id="9f058-125">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="9f058-126">Ad esempio, è possibile visualizzare dati di telemetria, aggiungere dispositivi e configurare regole.</span><span class="sxs-lookup"><span data-stu-id="9f058-126">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="9f058-127">Quando il provisioning di hello è completato e riquadro hello per la soluzione preconfigurata indica **pronto**, scegliere **avviare** tooopen il portale soluzione di monitoraggio remoto in una nuova scheda.</span><span class="sxs-lookup"><span data-stu-id="9f058-127">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![Avviare la soluzione hello preconfigurato][img-launch-solution]

1. <span data-ttu-id="9f058-129">Per impostazione predefinita, il portale di soluzione hello Mostra hello *dashboard*.</span><span class="sxs-lookup"><span data-stu-id="9f058-129">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="9f058-130">È possibile passare tooother aree del portale di soluzione hello utilizzando il menu di hello nella parte sinistra della pagina hello hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-130">You can navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![Dashboard della soluzione preconfigurata per il monitoraggio remoto][img-menu]

<span data-ttu-id="9f058-132">dashboard Hello Visualizza hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="9f058-132">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="9f058-133">Mappa che visualizza il percorso di hello di ogni dispositivo connesso toohello soluzione.</span><span class="sxs-lookup"><span data-stu-id="9f058-133">A map that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="9f058-134">Quando si esegue prima soluzione hello, sono presenti dispositivi simulati 25.</span><span class="sxs-lookup"><span data-stu-id="9f058-134">When you first run hello solution, there are 25 simulated devices.</span></span> <span data-ttu-id="9f058-135">Hello dispositivi simulati vengono implementati come processi Web di Azure, le soluzioni hello hello API di Bing mappe tooplot informazioni sulla mappa hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-135">hello simulated devices are implemented as Azure WebJobs, and hello solution uses hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="9f058-136">Vedere hello [domande frequenti su] [ lnk-faq] toolearn come toomake hello dinamici della mappa.</span><span class="sxs-lookup"><span data-stu-id="9f058-136">See hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="9f058-137">Un pannello **Cronologia telemetria** che traccia la telemetria di umidità e temperatura da un dispositivo selezionato in tempo quasi reale e visualizza i dati aggregati, ad esempio l'umidità massima, minima e media.</span><span class="sxs-lookup"><span data-stu-id="9f058-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="9f058-138">Un pannello **Cronologia avvisi** che mostra recenti eventi di avviso relativi a valori di telemetria che hanno superato il limite soglia.</span><span class="sxs-lookup"><span data-stu-id="9f058-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="9f058-139">Negli esempi di toohello inoltre creati dalla soluzione hello preconfigurato, è possibile definire i propri avvisi.</span><span class="sxs-lookup"><span data-stu-id="9f058-139">You can define your own alarms in addition toohello examples created by hello preconfigured solution.</span></span>
* <span data-ttu-id="9f058-140">Un pannello **Processi** che visualizza informazioni sui processi pianificati.</span><span class="sxs-lookup"><span data-stu-id="9f058-140">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="9f058-141">È possibile pianificare i propri processi nella pagina **Processi di gestione**.</span><span class="sxs-lookup"><span data-stu-id="9f058-141">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="9f058-142">Visualizzare gli avvisi</span><span class="sxs-lookup"><span data-stu-id="9f058-142">View alarms</span></span>

<span data-ttu-id="9f058-143">pannello della cronologia di allarme Hello mostra che i report di cinque dispositivi superiore rispetto a valori di dati di telemetria previsto.</span><span class="sxs-lookup"><span data-stu-id="9f058-143">hello alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![Cronologia di allarme TODO nel dashboard di soluzione hello][img-alarms]

> [!NOTE]
> <span data-ttu-id="9f058-145">Questi avvisi vengono generati da una regola che è incluso nella soluzione hello preconfigurato.</span><span class="sxs-lookup"><span data-stu-id="9f058-145">These alarms are generated by a rule that is included in hello preconfigured solution.</span></span> <span data-ttu-id="9f058-146">Questa regola genera un avviso quando il valore di temperatura hello inviato da un dispositivo supera 60.</span><span class="sxs-lookup"><span data-stu-id="9f058-146">This rule generates an alert when hello temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="9f058-147">È possibile definire regole e azioni scegliendo [regole](#add-a-rule) e [azioni](#add-an-action) nel menu a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in hello left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="9f058-148">Visualizzare i dispositivi</span><span class="sxs-lookup"><span data-stu-id="9f058-148">View devices</span></span>

<span data-ttu-id="9f058-149">Hello *dispositivi* sono elencati tutti i dispositivi registrato hello nella soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-149">hello *devices* list shows all hello registered devices in hello solution.</span></span> <span data-ttu-id="9f058-150">Dall'elenco di dispositivi hello è possibile visualizzare e modificare i metadati del dispositivo, è possibile aggiungere o rimuovere i dispositivi e richiamare i metodi nei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="9f058-150">From hello device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="9f058-151">È possibile filtrare e ordinare elenco hello dei dispositivi nell'elenco di dispositivi hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-151">You can filter and sort hello list of devices in hello device list.</span></span> <span data-ttu-id="9f058-152">È inoltre possibile personalizzare le colonne di hello visualizzate nell'elenco di dispositivi hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-152">You can also customize hello columns shown in hello device list.</span></span>

1. <span data-ttu-id="9f058-153">Scegliere **dispositivi** elenco dei dispositivi hello tooshow per questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="9f058-153">Choose **Devices** tooshow hello device list for this solution.</span></span>

   ![Elenco di dispositivi di visualizzazione hello nel portale di soluzione hello][img-devicelist]

1. <span data-ttu-id="9f058-155">elenco dei dispositivi Hello viene inizialmente 25 dispositivi simulati creati dal processo di provisioning hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-155">hello device list initially shows 25 simulated devices created by hello provisioning process.</span></span> <span data-ttu-id="9f058-156">È possibile aggiungere soluzioni toohello altri dispositivi simulati e fisico.</span><span class="sxs-lookup"><span data-stu-id="9f058-156">You can add additional simulated and physical devices toohello solution.</span></span>

1. <span data-ttu-id="9f058-157">i dettagli di hello tooview di un dispositivo, scegliere un dispositivo nell'elenco di dispositivi hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-157">tooview hello details of a device, choose a device in hello device list.</span></span>

   ![Visualizzare i dettagli dispositivo hello nel portale di soluzione hello][img-devicedetails]

<span data-ttu-id="9f058-159">Hello **dettagli dispositivo** pannello contiene sei sezioni:</span><span class="sxs-lookup"><span data-stu-id="9f058-159">hello **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="9f058-160">Una raccolta di collegamenti che abilitano si toocustomize hello dispositivo icona, disattivare la periferica hello, aggiungere una regola, richiamano un metodo o inviare un comando.</span><span class="sxs-lookup"><span data-stu-id="9f058-160">A collection of links that enable you toocustomize hello device icon, disable hello device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="9f058-161">Per un confronto dei comandi (messaggi da dispositivo a cloud) e dei metodi (metodi diretti), vedere [Indicazioni sulle comunicazioni da cloud a dispositivo][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="9f058-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="9f058-162">Hello **dispositivo doppi - tag** sezione consente valori di tag tooedit per dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-162">hello **Device Twin - Tags** section enables you tooedit tag values for hello device.</span></span> <span data-ttu-id="9f058-163">È possibile visualizzare i valori di tag nell'elenco di dispositivi hello e utilizzare l'elenco dei dispositivi hello toofilter valori tag.</span><span class="sxs-lookup"><span data-stu-id="9f058-163">You can display tag values in hello device list and use tag values toofilter hello device list.</span></span>
* <span data-ttu-id="9f058-164">Hello **dispositivo doppi - proprietà Desired** sezione consente tooset proprietà valori toobe inviati toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9f058-164">hello **Device Twin - Desired Properties** section enables you tooset property values toobe sent toohello device.</span></span>
* <span data-ttu-id="9f058-165">Hello **dispositivo doppi - proprietà segnalati** sezione mostra i valori delle proprietà inviati dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-165">hello **Device Twin - Reported Properties** section shows property values sent from hello device.</span></span>
* <span data-ttu-id="9f058-166">Hello **delle proprietà del dispositivo** sezione Mostra informazioni dal Registro di sistema di hello identità, ad esempio dispositivo hello chiavi id e l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9f058-166">hello **Device Properties** section shows information from hello identity registry such as hello device id and authentication keys.</span></span>
* <span data-ttu-id="9f058-167">Hello **processi recenti** sezione mostra le informazioni su tutti i processi che sono utilizzati di recente come destinazione di questo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9f058-167">hello **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-hello-device-list"></a><span data-ttu-id="9f058-168">Filtrare l'elenco dei dispositivi hello</span><span class="sxs-lookup"><span data-stu-id="9f058-168">Filter hello device list</span></span>

<span data-ttu-id="9f058-169">È possibile utilizzare un filtro toodisplay solo i dispositivi che inviano i valori della temperatura imprevisto.</span><span class="sxs-lookup"><span data-stu-id="9f058-169">You can use a filter toodisplay only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="9f058-170">soluzione preconfigurata di monitoraggio remoto Hello include hello **dispositivi integro** filtrare tooshow i dispositivi con un valore di temperatura media maggiore di 60.</span><span class="sxs-lookup"><span data-stu-id="9f058-170">hello remote monitoring preconfigured solution includes hello **Unhealthy devices** filter tooshow devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="9f058-171">È possibile anche [creare filtri personalizzati](#add-a-filter).</span><span class="sxs-lookup"><span data-stu-id="9f058-171">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="9f058-172">Scegliere **Apri salvato filtro** toodisplay un elenco dei filtri disponibili.</span><span class="sxs-lookup"><span data-stu-id="9f058-172">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="9f058-173">Scegliere quindi **dispositivi integro** filtro hello tooapply:</span><span class="sxs-lookup"><span data-stu-id="9f058-173">Then choose **Unhealthy devices** tooapply hello filter:</span></span>

    ![Visualizza l'elenco di filtri hello][img-unhealthy-filter]

1. <span data-ttu-id="9f058-175">elenco dei dispositivi Hello verranno visualizzati solo i dispositivi con un valore della temperatura media maggiore di 60.</span><span class="sxs-lookup"><span data-stu-id="9f058-175">hello device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![Elenco dei dispositivi filtrato hello visualizzazione che mostra i dispositivi non integro][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="9f058-177">Aggiornare le proprietà desiderate</span><span class="sxs-lookup"><span data-stu-id="9f058-177">Update desired properties</span></span>

<span data-ttu-id="9f058-178">È stato identificato un set di dispositivi per i quali può essere necessaria un'azione correttiva.</span><span class="sxs-lookup"><span data-stu-id="9f058-178">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="9f058-179">Tuttavia, si decide che frequenza dati hello di 15 secondi non è sufficiente per una diagnosi del problema hello chiara.</span><span class="sxs-lookup"><span data-stu-id="9f058-179">However, you decide that hello data frequency of 15 seconds is not sufficient for a clear diagnosis of hello issue.</span></span> <span data-ttu-id="9f058-180">Modifica hello telemetria frequenza toofive secondi tooprovide si con ulteriori dati punti toobetter diagnosticare il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-180">Changing hello telemetry frequency toofive seconds tooprovide you with more data points toobetter diagnose hello issue.</span></span> <span data-ttu-id="9f058-181">È possibile distribuire questa configurazione modifica tooyour remota dei dispositivi dal portale di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-181">You can push this configuration change tooyour remote devices from hello solution portal.</span></span> <span data-ttu-id="9f058-182">È possibile modificare hello una volta, valutare l'impatto hello e quindi agire sui risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-182">You can make hello change once, evaluate hello impact, and then act on hello results.</span></span>

<span data-ttu-id="9f058-183">Seguire questi toorun passaggi un processo che modifica hello **TelemetryInterval** proprietà per i dispositivi interessato hello desiderata.</span><span class="sxs-lookup"><span data-stu-id="9f058-183">Follow these steps toorun a job that changes hello **TelemetryInterval** desired property for hello affected devices.</span></span> <span data-ttu-id="9f058-184">Quando i dispositivi di hello ricevono hello nuovo **TelemetryInterval** valore della proprietà, cambiano i dati di telemetria toosend configurazione ogni cinque secondi anziché ogni 15 secondi:</span><span class="sxs-lookup"><span data-stu-id="9f058-184">When hello devices receive hello new **TelemetryInterval** property value, they change their configuration toosend telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="9f058-185">Durante la visualizzazione elenco hello dei dispositivi non integro nell'elenco di dispositivi hello, scegliere **pianificatore di processi**, quindi **Modifica dispositivo doppi**.</span><span class="sxs-lookup"><span data-stu-id="9f058-185">While you are showing hello list of unhealthy devices in hello device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="9f058-186">Chiamare il processo di hello **Modifica intervallo di dati di telemetria**.</span><span class="sxs-lookup"><span data-stu-id="9f058-186">Call hello job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="9f058-187">Modificare il valore di hello di hello **proprietà desiderata** nome **desiderato. Config.TelemetryInterval** toofive secondi.</span><span class="sxs-lookup"><span data-stu-id="9f058-187">Change hello value of hello **Desired Property** name **desired.Config.TelemetryInterval** toofive seconds.</span></span>

1. <span data-ttu-id="9f058-188">Scegliere **Pianifica**.</span><span class="sxs-lookup"><span data-stu-id="9f058-188">Choose **Schedule**.</span></span>

    ![Cambiare hello TelemetryInterval proprietà toofive secondi][img-change-interval]

1. <span data-ttu-id="9f058-190">È possibile monitorare lo stato di avanzamento hello hello del processo di su hello **Gestione processi** hello portale.</span><span class="sxs-lookup"><span data-stu-id="9f058-190">You can monitor hello progress of hello job on hello **Management Jobs** page in hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="9f058-191">Se si desidera toochange un valore della proprietà desiderata per un singolo dispositivo, utilizzare hello **proprietà desiderate** sezione hello **dettagli dispositivo** pannello invece di eseguire un processo.</span><span class="sxs-lookup"><span data-stu-id="9f058-191">If you want toochange a desired property value for an individual device, use hello **Desired Properties** section in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="9f058-192">Questo processo Imposta valore hello hello **TelemetryInterval** proprietà in un doppio dispositivo hello desiderata per tutti i dispositivi selezionati dal filtro hello di hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-192">This job sets hello value of hello **TelemetryInterval** desired property in hello device twin for all hello devices selected by hello filter.</span></span> <span data-ttu-id="9f058-193">dispositivi di Hello recupero questo valore da un doppio dispositivo hello e aggiornare il relativo comportamento.</span><span class="sxs-lookup"><span data-stu-id="9f058-193">hello devices retrieve this value from hello device twin and update their behavior.</span></span> <span data-ttu-id="9f058-194">Quando un dispositivo recupera ed elabora una proprietà desiderata da un doppio di un dispositivo, viene impostata hello corrispondente valore indicato.</span><span class="sxs-lookup"><span data-stu-id="9f058-194">When a device retrieves and processes a desired property from a device twin, it sets hello corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="9f058-195">Richiamare i metodi</span><span class="sxs-lookup"><span data-stu-id="9f058-195">Invoke methods</span></span>

<span data-ttu-id="9f058-196">Durante l'esecuzione di processo hello, noterai nell'elenco di hello dei dispositivi non integro che tutti questi dispositivi dispongono di firmware di precedente (minore di versione 1.6) versioni.</span><span class="sxs-lookup"><span data-stu-id="9f058-196">While hello job runs, you notice in hello list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![Hello Vista ha segnalato la versione del firmware per i dispositivi non integro hello][img-old-firmware]

<span data-ttu-id="9f058-198">Questa versione del firmware potrebbe essere causa radice di hello di hello imprevisto perché si prevede che altri dispositivi integro sono stati aggiornati di recente tooversion 2.0 i valori della temperatura.</span><span class="sxs-lookup"><span data-stu-id="9f058-198">This firmware version may be hello root cause of hello unexpected temperature values because you know that other healthy devices were recently updated tooversion 2.0.</span></span> <span data-ttu-id="9f058-199">È possibile utilizzare predefinito hello **dispositivi firmware precedente** filtrare tooidentify tutti i dispositivi con le versioni precedenti del firmware.</span><span class="sxs-lookup"><span data-stu-id="9f058-199">You can use hello built-in **Old firmware devices** filter tooidentify any devices with old firmware versions.</span></span> <span data-ttu-id="9f058-200">Dal portale di hello, è possibile aggiornare in remoto tutti i dispositivi di hello ancora in esecuzione versioni precedenti di firmware:</span><span class="sxs-lookup"><span data-stu-id="9f058-200">From hello portal, you can then remotely update all hello devices still running old firmware versions:</span></span>

1. <span data-ttu-id="9f058-201">Scegliere **Apri salvato filtro** toodisplay un elenco dei filtri disponibili.</span><span class="sxs-lookup"><span data-stu-id="9f058-201">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="9f058-202">Scegliere quindi **dispositivi firmware precedente** filtro hello tooapply:</span><span class="sxs-lookup"><span data-stu-id="9f058-202">Then choose **Old firmware devices** tooapply hello filter:</span></span>

    ![Visualizza l'elenco di filtri hello][img-old-filter]

1. <span data-ttu-id="9f058-204">elenco dei dispositivi Hello verranno visualizzati solo i dispositivi con le versioni precedenti del firmware.</span><span class="sxs-lookup"><span data-stu-id="9f058-204">hello device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="9f058-205">Questo elenco include cinque dispositivi hello identificati da hello **dispositivi integro** filtro e tre i dispositivi aggiuntivi:</span><span class="sxs-lookup"><span data-stu-id="9f058-205">This list includes hello five devices identified by hello **Unhealthy devices** filter and three additional devices:</span></span>

    ![Elenco dei dispositivi filtrato hello visualizzazione che mostra i dispositivi precedenti][img-filtered-old-list]

1. <span data-ttu-id="9f058-207">Scegliere **Pianificatore di processi** e quindi **Richiama metodo**.</span><span class="sxs-lookup"><span data-stu-id="9f058-207">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="9f058-208">Impostare **nome del processo** troppo**tooversion aggiornamento Firmware 2.0**.</span><span class="sxs-lookup"><span data-stu-id="9f058-208">Set **Job Name** too**Firmware update tooversion 2.0**.</span></span>

1. <span data-ttu-id="9f058-209">Scegliere **InitiateFirmwareUpdate** come hello **metodo**.</span><span class="sxs-lookup"><span data-stu-id="9f058-209">Choose **InitiateFirmwareUpdate** as hello **Method**.</span></span>

1. <span data-ttu-id="9f058-210">Set hello **FwPackageUri** parametro troppo**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span><span class="sxs-lookup"><span data-stu-id="9f058-210">Set hello **FwPackageUri** parameter too**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="9f058-211">Scegliere **Pianifica**.</span><span class="sxs-lookup"><span data-stu-id="9f058-211">Choose **Schedule**.</span></span> <span data-ttu-id="9f058-212">valore predefinito di Hello è ora toorun processo hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-212">hello default is for hello job toorun now.</span></span>

    ![Crea processo tooupdate hello firmware dispositivi hello selezionato][img-method-update]

> [!NOTE]
> <span data-ttu-id="9f058-214">Se si desidera tooinvoke un metodo su un dispositivo specifico, scegliere **metodi** in hello **dettagli dispositivo** pannello invece di eseguire un processo.</span><span class="sxs-lookup"><span data-stu-id="9f058-214">If you want tooinvoke a method on an individual device, choose **Methods** in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="9f058-215">Questo processo richiama hello **InitiateFirmwareUpdate** metodo diretto per tutti i dispositivi di hello selezionati dal filtro hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-215">This job invokes hello **InitiateFirmwareUpdate** direct method on all hello devices selected by hello filter.</span></span> <span data-ttu-id="9f058-216">Dispositivi rispondono immediatamente tooIoT Hub e quindi avviano processo di aggiornamento del firmware hello in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="9f058-216">Devices respond immediately tooIoT Hub and then initiate hello firmware update process asynchronously.</span></span> <span data-ttu-id="9f058-217">i dispositivi di Hello fornire informazioni sullo stato relative al processo di aggiornamento del firmware hello tramite valori di proprietà restituito, come illustrato nella seguente schermate hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-217">hello devices provide status information about hello firmware update process through reported property values, as shown in hello following screenshots.</span></span> <span data-ttu-id="9f058-218">Scegliere hello **aggiornamento** informazioni di hello icona tooupdate negli elenchi di dispositivo e processo hello:</span><span class="sxs-lookup"><span data-stu-id="9f058-218">Choose hello **Refresh** icon tooupdate hello information in hello device and job lists:</span></span>

<span data-ttu-id="9f058-219">![Elenco di processi con esecuzione elenco aggiornamento firmware di hello][img-update-1]
![elenco dei dispositivi che mostra lo stato di aggiornamento del firmware][img-update-2]
![processo elenco visualizzazione hello firmware aggiornamento dell'elenco completo][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="9f058-219">![Job list showing hello firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing hello firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="9f058-220">In un ambiente di produzione, è possibile pianificare processi toorun durante una finestra di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="9f058-220">In a production environment, you can schedule jobs toorun during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="9f058-221">Analisi dello scenario</span><span class="sxs-lookup"><span data-stu-id="9f058-221">Scenario review</span></span>

<span data-ttu-id="9f058-222">In questo scenario, è stato identificato un potenziale problema con alcuni dispositivi in uso remoti utilizzando la cronologia di allarme hello in dashboard hello e un filtro.</span><span class="sxs-lookup"><span data-stu-id="9f058-222">In this scenario, you identified a potential issue with some of your remote devices using hello alarm history on hello dashboard and a filter.</span></span> <span data-ttu-id="9f058-223">È quindi il filtro utilizzato hello e tooremotely un processo configurare hello dispositivi tooprovide più informazioni toohelp diagnosticare il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-223">You then used hello filter and a job tooremotely configure hello devices tooprovide more information toohelp diagnose hello issue.</span></span> <span data-ttu-id="9f058-224">Infine, è stato utilizzato un filtro e una manutenzione tooschedule processo per dispositivi hello interessato.</span><span class="sxs-lookup"><span data-stu-id="9f058-224">Finally, you used a filter and a job tooschedule maintenance on hello affected devices.</span></span> <span data-ttu-id="9f058-225">Se si restituisce toohello dashboard, è possibile controllare che non sono più presenti eventuali avvisi provenienti da dispositivi nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="9f058-225">If you return toohello dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="9f058-226">È possibile utilizzare un filtro tooverify che hello firmware viene aggiornato in tutti i dispositivi di hello nella soluzione e che sono presenti dispositivi non è più integri:</span><span class="sxs-lookup"><span data-stu-id="9f058-226">You can use a filter tooverify that hello firmware is up-to-date on all hello devices in your solution and that there are no more unhealthy devices:</span></span>

![Filtro che mostra come il firmware di tutti i dispositivi sia aggiornato][img-updated]

![Filtro che mostra come tutti i dispositivi siano integri][img-healthy]

## <a name="other-features"></a><span data-ttu-id="9f058-229">Altre funzionalità</span><span class="sxs-lookup"><span data-stu-id="9f058-229">Other features</span></span>

<span data-ttu-id="9f058-230">Hello nelle sezioni seguenti vengono descrivono alcune funzionalità aggiuntive di hello soluzione preconfigurata di monitoraggio remoto che non sono descritte come parte dello scenario precedente hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-230">hello following sections describe some additional features of hello remote monitoring preconfigured solution that are not described as part of hello previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="9f058-231">Personalizzare le colonne</span><span class="sxs-lookup"><span data-stu-id="9f058-231">Customize columns</span></span>

<span data-ttu-id="9f058-232">È possibile personalizzare hello informazioni visualizzate nell'elenco di dispositivi hello scegliendo **editor colonna**.</span><span class="sxs-lookup"><span data-stu-id="9f058-232">You can customize hello information shown in hello device list by choosing **Column editor**.</span></span> <span data-ttu-id="9f058-233">È possibile aggiungere e rimuovere colonne che visualizzano i valori dei tag e delle proprietà segnalate,</span><span class="sxs-lookup"><span data-stu-id="9f058-233">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="9f058-234">nonché riordinare e rinominare le colonne:</span><span class="sxs-lookup"><span data-stu-id="9f058-234">You can also reorder and rename columns:</span></span>

   ![Elenco di colonne editor ion hello dispositivo][img-columneditor]

### <a name="customize-hello-device-icon"></a><span data-ttu-id="9f058-236">Personalizzare l'icona di dispositivi hello</span><span class="sxs-lookup"><span data-stu-id="9f058-236">Customize hello device icon</span></span>

<span data-ttu-id="9f058-237">È possibile personalizzare l'icona di dispositivi hello visualizzato nell'elenco di dispositivi hello da hello **dettagli dispositivo** pannello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9f058-237">You can customize hello device icon displayed in hello device list from hello **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="9f058-238">Scegliere hello di hello matita icona tooopen **Modifica immagine** pannello per un dispositivo:</span><span class="sxs-lookup"><span data-stu-id="9f058-238">Choose hello pencil icon tooopen hello **Edit image** panel for a device:</span></span>

   ![Editor di immagini per il dispositivo: apertura][img-startimageedit]

1. <span data-ttu-id="9f058-240">Caricare una nuova immagine o utilizzare una delle immagini esistenti hello e quindi scegliere **salvare**:</span><span class="sxs-lookup"><span data-stu-id="9f058-240">Either upload a new image or use one of hello existing images and then choose **Save**:</span></span>

   ![Editor di immagini per il dispositivo: modifica][img-imageedit]

1. <span data-ttu-id="9f058-242">Hello selezionati sono ora viene visualizzata in hello **icona** colonna per il dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-242">hello image you selected now displays in hello **Icon** column for hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="9f058-243">immagine di Hello viene archiviata nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="9f058-243">hello image is stored in blob storage.</span></span> <span data-ttu-id="9f058-244">Un tag in un doppio dispositivo hello contiene un'immagine di toohello collegamento nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="9f058-244">A tag in hello device twin contains a link toohello image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="9f058-245">Aggiungere un dispositivo</span><span class="sxs-lookup"><span data-stu-id="9f058-245">Add a device</span></span>

<span data-ttu-id="9f058-246">Quando si distribuisce la soluzione hello preconfigurato, automaticamente effettuato il provisioning di 25 dispositivi di esempio che è possibile visualizzare nell'elenco di dispositivi hello</span><span class="sxs-lookup"><span data-stu-id="9f058-246">When you deploy hello preconfigured solution, you automatically provision 25 sample devices that you can see in hello device list.</span></span> <span data-ttu-id="9f058-247">Si tratta di *dispositivi simulati* in esecuzione in un processo Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="9f058-247">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="9f058-248">Dispositivi simulati semplificano automaticamente tooexperiment con la soluzione hello preconfigurato senza hello necessità toodeploy reale fisico i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="9f058-248">Simulated devices make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical devices.</span></span> <span data-ttu-id="9f058-249">Se si desidera tooconnect una soluzione di toohello dispositivo reale, vedere hello [connettersi toohello il dispositivo remoto monitoraggio soluzione preconfigurata] [ lnk-connect-rm] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="9f058-249">If you do want tooconnect a real device toohello solution, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="9f058-250">Hello passaggi seguenti viene illustrato come una soluzione di toohello dispositivo simulato tooadd:</span><span class="sxs-lookup"><span data-stu-id="9f058-250">hello following steps show you how tooadd a simulated device toohello solution:</span></span>

1. <span data-ttu-id="9f058-251">Passare l'elenco dei dispositivi toohello indietro.</span><span class="sxs-lookup"><span data-stu-id="9f058-251">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="9f058-252">Scegliere un dispositivo, tooadd **+ Aggiungi dispositivi** nell'angolo inferiore sinistro di hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-252">tooadd a device, choose **+ Add A Device** in hello bottom left corner.</span></span>

   ![Aggiunta di una soluzione di toohello preconfigurato dispositivo][img-adddevice]

1. <span data-ttu-id="9f058-254">Scegliere **Aggiungi nuovo** su hello **dispositivo simulato** riquadro.</span><span class="sxs-lookup"><span data-stu-id="9f058-254">Choose **Add New** on hello **Simulated Device** tile.</span></span>

   ![Impostare i dettagli del nuovo dispositivo nel dashboard][img-addnew]

   <span data-ttu-id="9f058-256">In aggiunta toocreating un nuovo dispositivo simulato, è anche possibile aggiungere un dispositivo fisico se si sceglie toocreate un **dispositivo personalizzato**.</span><span class="sxs-lookup"><span data-stu-id="9f058-256">In addition toocreating a new simulated device, you can also add a physical device if you choose toocreate a **Custom Device**.</span></span> <span data-ttu-id="9f058-257">toolearn più sulla connessione soluzione toohello dispositivi fisici, vedere [connettersi il toohello dispositivo IoT Suite soluzione preconfigurata di monitoraggio remoto][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="9f058-257">toolearn more about connecting physical devices toohello solution, see [Connect your device toohello IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="9f058-258">Selezionare **Let me define my own Device ID** (Definire l'ID dispositivo personale) e immettere un nome di ID dispositivo univoco, ad esempio **mydevice_01**.</span><span class="sxs-lookup"><span data-stu-id="9f058-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="9f058-259">Scegliere **Create**.</span><span class="sxs-lookup"><span data-stu-id="9f058-259">Choose **Create**.</span></span>

   ![Salvare un nuovo dispositivo][img-definedevice]

1. <span data-ttu-id="9f058-261">Nel passaggio 3 di **aggiunge un dispositivo simulato**, scegliere **eseguita** tooreturn toohello elenco dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="9f058-261">In step 3 of **Add a simulated device**, choose **Done** tooreturn toohello device list.</span></span>

1. <span data-ttu-id="9f058-262">È possibile visualizzare il dispositivo **esecuzione** nell'elenco di dispositivi hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-262">You can view your device **Running** in hello device list.</span></span>

    ![Visualizzare il nuovo dispositivo nell'elenco dei dispositivi][img-runningnew]

1. <span data-ttu-id="9f058-264">È inoltre possibile visualizzare hello simulato telemetria dal dispositivo nuovo dashboard hello:</span><span class="sxs-lookup"><span data-stu-id="9f058-264">You can also view hello simulated telemetry from your new device on hello dashboard:</span></span>

    ![Visualizzare i dati di telemetria dal nuovo dispositivo][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="9f058-266">Disabilitare e rimuovere un dispositivo</span><span class="sxs-lookup"><span data-stu-id="9f058-266">Disable and delete a device</span></span>

<span data-ttu-id="9f058-267">È possibile disabilitare un dispositivo e dopo aver disabilitato è possibile rimuoverlo:</span><span class="sxs-lookup"><span data-stu-id="9f058-267">You can disable a device, and after it is disabled you can remove it:</span></span>

![Disabilitare e rimuovere un dispositivo][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="9f058-269">Aggiungere una regola</span><span class="sxs-lookup"><span data-stu-id="9f058-269">Add a rule</span></span>

<span data-ttu-id="9f058-270">Non esistono regole per il nuovo dispositivo di hello che appena aggiunto.</span><span class="sxs-lookup"><span data-stu-id="9f058-270">There are no rules for hello new device you just added.</span></span> <span data-ttu-id="9f058-271">In questa sezione aggiungere una regola che attiva un avviso quando la temperatura hello restituite da hello nuovo dispositivo supera gradi 47.</span><span class="sxs-lookup"><span data-stu-id="9f058-271">In this section, you add a rule that triggers an alarm when hello temperature reported by hello new device exceeds 47 degrees.</span></span> <span data-ttu-id="9f058-272">Prima di iniziare, si noti che hello telemetria per nuovo dispositivo di hello dashboard hello dimostra temperatura dispositivo hello non superi mai il 45 gradi.</span><span class="sxs-lookup"><span data-stu-id="9f058-272">Before you start, notice that hello telemetry history for hello new device on hello dashboard shows hello device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="9f058-273">Passare l'elenco dei dispositivi toohello indietro.</span><span class="sxs-lookup"><span data-stu-id="9f058-273">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="9f058-274">tooadd una regola per il dispositivo di hello, selezionare il nuovo dispositivo in hello **elenco dispositivi**, quindi scegliere **Aggiungi regola**.</span><span class="sxs-lookup"><span data-stu-id="9f058-274">tooadd a rule for hello device, select your new device in hello **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="9f058-275">Creare una regola che utilizza **temperatura** come campo di dati hello e utilizza **AlarmTemp** come output di hello quando temperatura hello supera gradi 47:</span><span class="sxs-lookup"><span data-stu-id="9f058-275">Create a rule that uses **Temperature** as hello data field and uses **AlarmTemp** as hello output when hello temperature exceeds 47 degrees:</span></span>

    ![Aggiungere una regola per il dispositivo][img-adddevicerule]

1. <span data-ttu-id="9f058-277">Scegliere le modifiche, toosave **salvare e visualizzare le regole**.</span><span class="sxs-lookup"><span data-stu-id="9f058-277">toosave your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="9f058-278">Scegliere **comandi** nel riquadro dei dettagli dispositivo hello per il nuovo dispositivo di hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-278">Choose **Commands** in hello device details pane for hello new device.</span></span>

    ![Aggiungere una regola per il dispositivo][img-adddevicerule2]

1. <span data-ttu-id="9f058-280">Selezionare **ChangeSetPointTemp** dall'elenco di comandi hello e set **SetPointTemp** too45.</span><span class="sxs-lookup"><span data-stu-id="9f058-280">Select **ChangeSetPointTemp** from hello command list and set **SetPointTemp** too45.</span></span> <span data-ttu-id="9f058-281">Scegliere quindi **Invia comando**.</span><span class="sxs-lookup"><span data-stu-id="9f058-281">Then choose **Send Command**:</span></span>

    ![Aggiungere una regola per il dispositivo][img-adddevicerule3]

1. <span data-ttu-id="9f058-283">Spostarsi indietro toohello dashboard.</span><span class="sxs-lookup"><span data-stu-id="9f058-283">Navigate back toohello dashboard.</span></span> <span data-ttu-id="9f058-284">Dopo un breve periodo di tempo, si vedrà una nuova voce di hello **cronologia allarme** riquadro quando temperatura hello segnalato dal nuovo dispositivo supera la soglia di 47 gradi hello:</span><span class="sxs-lookup"><span data-stu-id="9f058-284">After a short time, you will see a new entry in hello **Alarm History** pane when hello temperature reported by your new device exceeds hello 47-degree threshold:</span></span>

    ![Aggiungere una regola per il dispositivo][img-adddevicerule4]

1. <span data-ttu-id="9f058-286">È possibile esaminare e modificare tutte le regole in hello **regole** pagina del dashboard hello:</span><span class="sxs-lookup"><span data-stu-id="9f058-286">You can review and edit all your rules on hello **Rules** page of hello dashboard:</span></span>

    ![Elenco delle regole per il dispositivo][img-rules]

1. <span data-ttu-id="9f058-288">È possibile esaminare e modificare tutte le azioni che possono essere eseguite nella regola tooa risposta su hello hello **azioni** pagina del dashboard hello:</span><span class="sxs-lookup"><span data-stu-id="9f058-288">You can review and edit all hello actions that can be taken in response tooa rule on hello **Actions** page of hello dashboard:</span></span>

    ![Elenco delle azioni per il dispositivo][img-actions]

> [!NOTE]
> <span data-ttu-id="9f058-290">È possibile toodefine azioni che è possono inviare un messaggio di posta elettronica o SMS nella risposta tooa regola o integrare con un sistema line-of-business tramite un [logica App][lnk-logic-apps].</span><span class="sxs-lookup"><span data-stu-id="9f058-290">It is possible toodefine actions that can send an email message or SMS in response tooa rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="9f058-291">Per ulteriori informazioni, vedere hello [tooyour connessione logica App monitoraggio remoto di Azure IoT Suite preconfigurato soluzione][lnk-logicapptutorial].</span><span class="sxs-lookup"><span data-stu-id="9f058-291">For more information, see hello [Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="9f058-292">Gestire i filtri</span><span class="sxs-lookup"><span data-stu-id="9f058-292">Manage filters</span></span>

<span data-ttu-id="9f058-293">Nell'elenco di dispositivi hello, è possibile creare, salvare e ricaricare i filtri toodisplay un elenco personalizzato di hub tooyour connessi i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="9f058-293">In hello device list, you can create, save, and reload filters toodisplay a customized list of devices connected tooyour hub.</span></span> <span data-ttu-id="9f058-294">toocreate un filtro:</span><span class="sxs-lookup"><span data-stu-id="9f058-294">toocreate a filter:</span></span>

1. <span data-ttu-id="9f058-295">Scegliere l'icona di filtro modifica hello sopra l'elenco di hello dei dispositivi:</span><span class="sxs-lookup"><span data-stu-id="9f058-295">Choose hello edit filter icon above hello list of devices:</span></span>

    ![Editor filtri hello aperto][img-editfiltericon]

1. <span data-ttu-id="9f058-297">In hello **editor filtri**, aggiungere i campi di hello, operatori e valori toofilter hello dispositivo elenco.</span><span class="sxs-lookup"><span data-stu-id="9f058-297">In hello **Filter editor**, add hello fields, operators, and values toofilter hello device list.</span></span> <span data-ttu-id="9f058-298">È possibile aggiungere più clausole toorefine il filtro.</span><span class="sxs-lookup"><span data-stu-id="9f058-298">You can add multiple clauses toorefine your filter.</span></span> <span data-ttu-id="9f058-299">Scegliere **filtro** filtro hello tooapply:</span><span class="sxs-lookup"><span data-stu-id="9f058-299">Choose **Filter** tooapply hello filter:</span></span>

    ![Creare un filtro][img-filtereditor]

1. <span data-ttu-id="9f058-301">In questo esempio hello viene filtrato dal produttore e il numero di modello:</span><span class="sxs-lookup"><span data-stu-id="9f058-301">In this example, hello list is filtered by manufacturer and model number:</span></span>

    ![Elenco filtrato][img-filterelist]

1. <span data-ttu-id="9f058-303">toosave il filtro con un nome personalizzato, scegliere hello **salvare come** icona:</span><span class="sxs-lookup"><span data-stu-id="9f058-303">toosave your filter with a custom name, choose hello **Save as** icon:</span></span>

    ![Salvare un filtro][img-savefilter]

1. <span data-ttu-id="9f058-305">tooreapply un filtro è stato salvato in precedenza, scegliere hello **Apri salvato filtro** icona:</span><span class="sxs-lookup"><span data-stu-id="9f058-305">tooreapply a filter you saved previously, choose hello **Open saved filter** icon:</span></span>

    ![Aprire un filtro][img-openfilter]

<span data-ttu-id="9f058-307">È possibile creare filtri basati sull'ID dispositivo, sullo stato del dispositivo, sulle proprietà desiderate, sulle proprietà segnalate e sui tag.</span><span class="sxs-lookup"><span data-stu-id="9f058-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="9f058-308">Aggiungere il proprio dispositivo tooa tag personalizzati in hello **tag** sezione di hello **dettagli dispositivo** pannello oppure eseguire un processo tooupdate tag su più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="9f058-308">You add your own custom tags tooa device in hello **Tags** section of hello **Device Details** panel, or run a job tooupdate tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="9f058-309">In hello **editor filtri**, è possibile utilizzare hello **visualizzazione avanzata** direttamente testo della query hello tooedit.</span><span class="sxs-lookup"><span data-stu-id="9f058-309">In hello **Filter editor**, you can use hello **Advanced view** tooedit hello query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="9f058-310">Comandi:</span><span class="sxs-lookup"><span data-stu-id="9f058-310">Commands</span></span>

<span data-ttu-id="9f058-311">Da hello **dettagli dispositivo** pannello, è possibile inviare dispositivo toohello comandi.</span><span class="sxs-lookup"><span data-stu-id="9f058-311">From hello **Device Details** panel, you can send commands toohello device.</span></span> <span data-ttu-id="9f058-312">Al primo avvio di un dispositivo invia informazioni hello comandi che supporta toohello soluzione.</span><span class="sxs-lookup"><span data-stu-id="9f058-312">When a device first starts, it sends information about hello commands it supports toohello solution.</span></span> <span data-ttu-id="9f058-313">Per una descrizione delle differenze di hello tra i comandi e i metodi, vedere [opzioni cloud a dispositivo IoT Hub Azure][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="9f058-313">For a discussion of hello differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="9f058-314">Scegliere **comandi** in hello **dettagli dispositivo** pannello per il dispositivo selezionato hello:</span><span class="sxs-lookup"><span data-stu-id="9f058-314">Choose **Commands** in hello **Device Details** panel for hello selected device:</span></span>

   ![Comandi del dispositivo nel dashboard][img-devicecommands]

1. <span data-ttu-id="9f058-316">Selezionare **PingDevice** dall'elenco di comandi hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-316">Select **PingDevice** from hello command list.</span></span>

1. <span data-ttu-id="9f058-317">Scegliere **Invia comando**.</span><span class="sxs-lookup"><span data-stu-id="9f058-317">Choose **Send Command**.</span></span>

1. <span data-ttu-id="9f058-318">È possibile visualizzare lo stato di hello del comando hello nella cronologia del comando hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-318">You can see hello status of hello command in hello command history.</span></span>

   ![Stato dei comandi nel dashboard][img-pingcommand]

<span data-ttu-id="9f058-320">soluzione Hello tiene traccia dello stato di hello di ogni comando che viene inviato.</span><span class="sxs-lookup"><span data-stu-id="9f058-320">hello solution tracks hello status of each command it sends.</span></span> <span data-ttu-id="9f058-321">Risultato hello è inizialmente **in sospeso**.</span><span class="sxs-lookup"><span data-stu-id="9f058-321">Initially hello result is **Pending**.</span></span> <span data-ttu-id="9f058-322">Quando il dispositivo di hello segnala che è eseguita comando hello, risultato hello viene impostato troppo**successo**.</span><span class="sxs-lookup"><span data-stu-id="9f058-322">When hello device reports that it has executed hello command, hello result is set too**Success**.</span></span>

## <a name="behind-hello-scenes"></a><span data-ttu-id="9f058-323">Background hello</span><span class="sxs-lookup"><span data-stu-id="9f058-323">Behind hello scenes</span></span>

<span data-ttu-id="9f058-324">Quando si distribuisce una soluzione preconfigurata, il processo di distribuzione hello crea più risorse hello Azure sottoscrizione selezionata.</span><span class="sxs-lookup"><span data-stu-id="9f058-324">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="9f058-325">È possibile visualizzare queste risorse in Azure hello [portale][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="9f058-325">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="9f058-326">il processo di distribuzione Hello crea un **gruppo di risorse** con un nome basato sul nome hello scelto per la soluzione preconfigurata:</span><span class="sxs-lookup"><span data-stu-id="9f058-326">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Soluzione preconfigurata in hello portale di Azure][img-portal]

<span data-ttu-id="9f058-328">È possibile visualizzare le impostazioni di hello di ogni risorsa selezionandolo nell'elenco di hello delle risorse nel gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-328">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="9f058-329">È anche possibile visualizzare il codice sorgente hello per soluzione hello preconfigurato.</span><span class="sxs-lookup"><span data-stu-id="9f058-329">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="9f058-330">il codice sorgente soluzione preconfigurata di monitoraggio remoto Hello è hello [azure iot-remoto monitoraggio] [ lnk-rmgithub] repository GitHub:</span><span class="sxs-lookup"><span data-stu-id="9f058-330">hello remote monitoring preconfigured solution source code is in hello [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="9f058-331">Hello **DeviceAdministration** cartella contiene il codice sorgente hello per dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-331">hello **DeviceAdministration** folder contains hello source code for hello dashboard.</span></span>
* <span data-ttu-id="9f058-332">Hello **simulatore** cartella contiene il codice sorgente hello per dispositivo simulato hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-332">hello **Simulator** folder contains hello source code for hello simulated device.</span></span>
* <span data-ttu-id="9f058-333">Hello **EventProcessor** cartella contiene il codice sorgente hello per il processo di back-end hello che gestisce i dati di telemetria hello in arrivo.</span><span class="sxs-lookup"><span data-stu-id="9f058-333">hello **EventProcessor** folder contains hello source code for hello back-end process that handles hello incoming telemetry.</span></span>

<span data-ttu-id="9f058-334">Al termine, è possibile eliminare la soluzione hello preconfigurato dalla sottoscrizione di Azure su hello [azureiotsuite.com] [ lnk-azureiotsuite] sito.</span><span class="sxs-lookup"><span data-stu-id="9f058-334">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="9f058-335">Questo sito consente tooeasily Elimina che tutte le risorse che è sono eseguito il provisioning durante la creazione di soluzioni hello preconfigurato di hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-335">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="9f058-336">tooensure di eliminare tutti gli elementi correlati soluzione toohello preconfigurato, l'eliminazione hello [azureiotsuite.com] [ lnk-azureiotsuite] del sito e non viene eliminato il gruppo di risorse hello nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="9f058-336">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site and do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f058-337">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9f058-337">Next Steps</span></span>

<span data-ttu-id="9f058-338">Dopo aver distribuito una soluzione appropriata preconfigurato, è possibile continuare introduzione IoT Suite leggendo hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="9f058-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="9f058-339">[Procedura dettagliata della soluzione preconfigurata per il monitoraggio remoto][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="9f058-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="9f058-340">[Connettere la soluzione preconfigurata di monitoraggio remoto toohello di dispositivo][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="9f058-340">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="9f058-341">[Autorizzazioni nel sito azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="9f058-341">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

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