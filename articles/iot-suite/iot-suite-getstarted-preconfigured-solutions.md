---
title: Introduzione alle soluzioni preconfigurate | Documentazione Microsoft
description: Seguire questa esercitazione per apprendere come distribuire una soluzione preconfigurata di Azure IoT Suite.
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
ms.openlocfilehash: 466825ab78a5ac9773d8beff69cca90ff9db6c01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-preconfigured-solutions"></a><span data-ttu-id="14cfe-103">Introduzione alle soluzioni preconfigurate</span><span class="sxs-lookup"><span data-stu-id="14cfe-103">Get started with the preconfigured solutions</span></span>

<span data-ttu-id="14cfe-104">Le [soluzioni preconfigurate][lnk-preconfigured-solutions] di Azure IoT Suite combinano più servizi IoT di Azure per fornire soluzioni end-to-end che implementano scenari aziendali IoT comuni.</span><span class="sxs-lookup"><span data-stu-id="14cfe-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services to deliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="14cfe-105">La soluzione preconfigurata per il *monitoraggio remoto* si connette ai dispositivi e li monitora.</span><span class="sxs-lookup"><span data-stu-id="14cfe-105">The *remote monitoring* preconfigured solution connects to and monitors your devices.</span></span> <span data-ttu-id="14cfe-106">È possibile usare la soluzione per analizzare il flusso di dati dai dispositivi e di migliorare i risultati aziendali facendo in modo che i processi rispondano automaticamente a quel flusso di dati.</span><span class="sxs-lookup"><span data-stu-id="14cfe-106">You can use the solution to analyze the stream of data from your devices and to improve business outcomes by making processes respond automatically to that stream of data.</span></span>

<span data-ttu-id="14cfe-107">Questa esercitazione illustra come effettuare il provisioning della soluzione preconfigurata per il monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="14cfe-107">This tutorial shows you how to provision the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="14cfe-108">Ne descrive anche le funzionalità di base.</span><span class="sxs-lookup"><span data-stu-id="14cfe-108">It also walks you through the basic features of the preconfigured solution.</span></span> <span data-ttu-id="14cfe-109">È possibile accedere a molte di queste funzionalità dal *dashboard* distribuito come parte della soluzione preconfigurata:</span><span class="sxs-lookup"><span data-stu-id="14cfe-109">You can access many of these features from the solution *dashboard* that deploys as part of the preconfigured solution:</span></span>

![Dashboard della soluzione preconfigurata per il monitoraggio remoto][img-dashboard]

<span data-ttu-id="14cfe-111">Per completare l'esercitazione, è necessaria una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="14cfe-111">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="14cfe-112">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="14cfe-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="14cfe-113">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="14cfe-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="14cfe-114">Panoramica dello scenario</span><span class="sxs-lookup"><span data-stu-id="14cfe-114">Scenario overview</span></span>

<span data-ttu-id="14cfe-115">Nel momento in cui viene distribuita, la soluzione preconfigurata per il monitoraggio remoto viene prepopolata con risorse che consentono di eseguire uno scenario di monitoraggio remoto comune.</span><span class="sxs-lookup"><span data-stu-id="14cfe-115">When you deploy the remote monitoring preconfigured solution, it is prepopulated with resources that enable you to step through a common remote monitoring scenario.</span></span> <span data-ttu-id="14cfe-116">In questo scenario, vari dispositivi connessi alla soluzione registrano valori di temperatura imprevisti.</span><span class="sxs-lookup"><span data-stu-id="14cfe-116">In this scenario, several devices connected to the solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="14cfe-117">Le sezioni seguenti mostrano come:</span><span class="sxs-lookup"><span data-stu-id="14cfe-117">The following sections show you how to:</span></span>

* <span data-ttu-id="14cfe-118">Identificare i dispositivi che inviano valori di temperatura imprevisti.</span><span class="sxs-lookup"><span data-stu-id="14cfe-118">Identify the devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="14cfe-119">Configurare i dispositivi per l'invio di dati di telemetria più dettagliati.</span><span class="sxs-lookup"><span data-stu-id="14cfe-119">Configure these devices to send more detailed telemetry.</span></span>
* <span data-ttu-id="14cfe-120">Risolvere il problema aggiornando il firmware dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="14cfe-120">Fix the problem by updating the firmware on these devices.</span></span>
* <span data-ttu-id="14cfe-121">Verificare che il problema sia stato risolto.</span><span class="sxs-lookup"><span data-stu-id="14cfe-121">Verify that your action has resolved the issue.</span></span>

<span data-ttu-id="14cfe-122">Una particolarità di questo scenario consiste nella possibilità di eseguire tutte queste azioni in remoto dal dashboard della soluzione,</span><span class="sxs-lookup"><span data-stu-id="14cfe-122">A key feature of this scenario is that you can perform all these actions remotely from the solution dashboard.</span></span> <span data-ttu-id="14cfe-123">senza dover accedere fisicamente ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="14cfe-123">You do not need physical access to the devices.</span></span>

## <a name="view-the-solution-dashboard"></a><span data-ttu-id="14cfe-124">Visualizzare il dashboard della soluzione</span><span class="sxs-lookup"><span data-stu-id="14cfe-124">View the solution dashboard</span></span>

<span data-ttu-id="14cfe-125">Il dashboard della soluzione consente di gestire la soluzione distribuita.</span><span class="sxs-lookup"><span data-stu-id="14cfe-125">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="14cfe-126">Ad esempio, è possibile visualizzare dati di telemetria, aggiungere dispositivi e configurare regole.</span><span class="sxs-lookup"><span data-stu-id="14cfe-126">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="14cfe-127">Al termine del provisioning, quando il riquadro della soluzione preconfigurata indica **Pronto**, scegliere **Avvia** per aprire il portale della soluzione di monitoraggio remoto in una nuova scheda.</span><span class="sxs-lookup"><span data-stu-id="14cfe-127">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span></span>

    ![Avviare la soluzione preconfigurata][img-launch-solution]

1. <span data-ttu-id="14cfe-129">Per impostazione predefinita, il portale della soluzione visualizza il *dashboard*.</span><span class="sxs-lookup"><span data-stu-id="14cfe-129">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="14cfe-130">È possibile passare ad altre aree del portale della soluzione usando il menu sul lato sinistro della pagina.</span><span class="sxs-lookup"><span data-stu-id="14cfe-130">You can navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span></span>

    ![Dashboard della soluzione preconfigurata per il monitoraggio remoto][img-menu]

<span data-ttu-id="14cfe-132">Il dashboard visualizza le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="14cfe-132">The dashboard displays the following information:</span></span>

* <span data-ttu-id="14cfe-133">Una mappa che visualizza la posizione di ogni dispositivo connesso alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="14cfe-133">A map that displays the location of each device connected to the solution.</span></span> <span data-ttu-id="14cfe-134">Quando si esegue la soluzione per la prima volta, sono disponibili 25 dispositivi simulati.</span><span class="sxs-lookup"><span data-stu-id="14cfe-134">When you first run the solution, there are 25 simulated devices.</span></span> <span data-ttu-id="14cfe-135">I dispositivi simulati vengono implementati come Processi Web di Azure e la soluzione usa l'API Bing Maps per tracciare le informazioni sulla mappa.</span><span class="sxs-lookup"><span data-stu-id="14cfe-135">The simulated devices are implemented as Azure WebJobs, and the solution uses the Bing Maps API to plot information on the map.</span></span> <span data-ttu-id="14cfe-136">Vedere le [domande frequenti][lnk-faq] per informazioni su come rendere dinamica la mappa.</span><span class="sxs-lookup"><span data-stu-id="14cfe-136">See the [FAQ][lnk-faq] to learn how to make the map dynamic.</span></span>
* <span data-ttu-id="14cfe-137">Un pannello **Cronologia telemetria** che traccia la telemetria di umidità e temperatura da un dispositivo selezionato in tempo quasi reale e visualizza i dati aggregati, ad esempio l'umidità massima, minima e media.</span><span class="sxs-lookup"><span data-stu-id="14cfe-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="14cfe-138">Un pannello **Cronologia avvisi** che mostra recenti eventi di avviso relativi a valori di telemetria che hanno superato il limite soglia.</span><span class="sxs-lookup"><span data-stu-id="14cfe-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="14cfe-139">È possibile definire i propri avvisi oltre agli esempi creati dalla soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="14cfe-139">You can define your own alarms in addition to the examples created by the preconfigured solution.</span></span>
* <span data-ttu-id="14cfe-140">Un pannello **Processi** che visualizza informazioni sui processi pianificati.</span><span class="sxs-lookup"><span data-stu-id="14cfe-140">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="14cfe-141">È possibile pianificare i propri processi nella pagina **Processi di gestione**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-141">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="14cfe-142">Visualizzare gli avvisi</span><span class="sxs-lookup"><span data-stu-id="14cfe-142">View alarms</span></span>

<span data-ttu-id="14cfe-143">Il pannello Cronologia avvisi indica che in cinque dispositivi sono stati registrati valori di telemetria più alti del previsto.</span><span class="sxs-lookup"><span data-stu-id="14cfe-143">The alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![Cronologia avvisi nel dashboard della soluzione][img-alarms]

> [!NOTE]
> <span data-ttu-id="14cfe-145">Questi avvisi vengono generati da una regola inclusa nella soluzione preconfigurata,</span><span class="sxs-lookup"><span data-stu-id="14cfe-145">These alarms are generated by a rule that is included in the preconfigured solution.</span></span> <span data-ttu-id="14cfe-146">che genera un avviso ogni volta che il valore di temperatura inviato da un dispositivo supera 60.</span><span class="sxs-lookup"><span data-stu-id="14cfe-146">This rule generates an alert when the temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="14cfe-147">È possibile definire regole e azioni personalizzate scegliendo [Regole](#add-a-rule) e [Azioni](#add-an-action) nel menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="14cfe-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in the left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="14cfe-148">Visualizzare i dispositivi</span><span class="sxs-lookup"><span data-stu-id="14cfe-148">View devices</span></span>

<span data-ttu-id="14cfe-149">L'elenco dei *dispositivi* mostra tutti i dispositivi registrati nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="14cfe-149">The *devices* list shows all the registered devices in the solution.</span></span> <span data-ttu-id="14cfe-150">Da tale elenco è possibile visualizzare e modificare i metadati dei dispositivi, aggiungere o rimuovere dispositivi e richiamare metodi su di essi.</span><span class="sxs-lookup"><span data-stu-id="14cfe-150">From the device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="14cfe-151">Nell'elenco dei dispositivi è possibile anche filtrare e ordinare l'elenco dei dispositivi,</span><span class="sxs-lookup"><span data-stu-id="14cfe-151">You can filter and sort the list of devices in the device list.</span></span> <span data-ttu-id="14cfe-152">nonché personalizzare le colonne visualizzate.</span><span class="sxs-lookup"><span data-stu-id="14cfe-152">You can also customize the columns shown in the device list.</span></span>

1. <span data-ttu-id="14cfe-153">Scegliere **Dispositivi** per visualizzare l'elenco dei dispositivi relativi alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="14cfe-153">Choose **Devices** to show the device list for this solution.</span></span>

   ![Visualizzare l'elenco dei dispositivi nel portale della soluzione][img-devicelist]

1. <span data-ttu-id="14cfe-155">L'elenco dei dispositivi mostra inizialmente 25 dispositivi simulati creati dal processo di provisioning.</span><span class="sxs-lookup"><span data-stu-id="14cfe-155">The device list initially shows 25 simulated devices created by the provisioning process.</span></span> <span data-ttu-id="14cfe-156">È possibile aggiungere altri dispositivi fisici e simulati alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="14cfe-156">You can add additional simulated and physical devices to the solution.</span></span>

1. <span data-ttu-id="14cfe-157">Scegliere un dispositivo dell'elenco per visualizzarne i dettagli.</span><span class="sxs-lookup"><span data-stu-id="14cfe-157">To view the details of a device, choose a device in the device list.</span></span>

   ![Visualizzare i dettagli di un dispositivo nel portale della soluzione][img-devicedetails]

<span data-ttu-id="14cfe-159">Il pannello **Dettagli dispositivo** contiene sei sezioni:</span><span class="sxs-lookup"><span data-stu-id="14cfe-159">The **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="14cfe-160">Una raccolta di collegamenti che consentono di personalizzare l'icona del dispositivo, disabilitare il dispositivo, aggiungere una regola, richiamare un metodo o inviare un comando.</span><span class="sxs-lookup"><span data-stu-id="14cfe-160">A collection of links that enable you to customize the device icon, disable the device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="14cfe-161">Per un confronto dei comandi (messaggi da dispositivo a cloud) e dei metodi (metodi diretti), vedere [Indicazioni sulle comunicazioni da cloud a dispositivo][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="14cfe-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="14cfe-162">La sezione **Device Twin (Dispositivo gemello) - Tag** consente di modificare i valori dei tag per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="14cfe-162">The **Device Twin - Tags** section enables you to edit tag values for the device.</span></span> <span data-ttu-id="14cfe-163">È possibile visualizzare i valori dei tag nell'elenco dei dispositivi e usarli per filtrare l'elenco.</span><span class="sxs-lookup"><span data-stu-id="14cfe-163">You can display tag values in the device list and use tag values to filter the device list.</span></span>
* <span data-ttu-id="14cfe-164">La sezione **Device Twin (Dispositivo gemello) - Proprietà desiderate** consente di impostare i valori delle proprietà da inviare al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="14cfe-164">The **Device Twin - Desired Properties** section enables you to set property values to be sent to the device.</span></span>
* <span data-ttu-id="14cfe-165">La sezione **Device Twin (Dispositivo gemello) - Proprietà segnalate** visualizza i valori delle proprietà inviati dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="14cfe-165">The **Device Twin - Reported Properties** section shows property values sent from the device.</span></span>
* <span data-ttu-id="14cfe-166">La sezione **Proprietà dispositivo** visualizza informazioni del registro di identità, come l'ID dispositivo e le chiavi di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="14cfe-166">The **Device Properties** section shows information from the identity registry such as the device id and authentication keys.</span></span>
* <span data-ttu-id="14cfe-167">La sezione **Processi recenti** visualizza informazioni sui processi recentemente indirizzati al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="14cfe-167">The **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-the-device-list"></a><span data-ttu-id="14cfe-168">Filtrare l'elenco dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="14cfe-168">Filter the device list</span></span>

<span data-ttu-id="14cfe-169">È possibile usare un filtro per visualizzare solo i dispositivi che inviano valori di temperatura imprevisti.</span><span class="sxs-lookup"><span data-stu-id="14cfe-169">You can use a filter to display only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="14cfe-170">La soluzione preconfigurata per il monitoraggio remoto include il filtro **Dispositivi non integri** che consente di visualizzare i dispositivi con un valore di temperatura media superiore a 60.</span><span class="sxs-lookup"><span data-stu-id="14cfe-170">The remote monitoring preconfigured solution includes the **Unhealthy devices** filter to show devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="14cfe-171">È possibile anche [creare filtri personalizzati](#add-a-filter).</span><span class="sxs-lookup"><span data-stu-id="14cfe-171">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="14cfe-172">Scegliere **Apri filtro salvato** per visualizzare un elenco dei filtri disponibili.</span><span class="sxs-lookup"><span data-stu-id="14cfe-172">Choose **Open saved filter** to display a list of available filters.</span></span> <span data-ttu-id="14cfe-173">Scegliere quindi **Dispositivi non integri** per applicare il filtro:</span><span class="sxs-lookup"><span data-stu-id="14cfe-173">Then choose **Unhealthy devices** to apply the filter:</span></span>

    ![Visualizzare l'elenco dei filtri][img-unhealthy-filter]

1. <span data-ttu-id="14cfe-175">Nell'elenco dei dispositivi sono ora visualizzati solo i dispositivi con un valore di temperatura media superiore a 60.</span><span class="sxs-lookup"><span data-stu-id="14cfe-175">The device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![Visualizzare l'elenco dei dispositivi filtrato in modo che siano riportati solo i dispositivi non integri][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="14cfe-177">Aggiornare le proprietà desiderate</span><span class="sxs-lookup"><span data-stu-id="14cfe-177">Update desired properties</span></span>

<span data-ttu-id="14cfe-178">È stato identificato un set di dispositivi per i quali può essere necessaria un'azione correttiva.</span><span class="sxs-lookup"><span data-stu-id="14cfe-178">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="14cfe-179">Si decide tuttavia che una frequenza dati pari a 15 secondi non è sufficiente per una diagnosi esatta del problema.</span><span class="sxs-lookup"><span data-stu-id="14cfe-179">However, you decide that the data frequency of 15 seconds is not sufficient for a clear diagnosis of the issue.</span></span> <span data-ttu-id="14cfe-180">Si imposta quindi la frequenza di telemetria su cinque secondi in modo da avere a disposizione una maggiore quantità di punti dati e diagnosticare meglio il problema.</span><span class="sxs-lookup"><span data-stu-id="14cfe-180">Changing the telemetry frequency to five seconds to provide you with more data points to better diagnose the issue.</span></span> <span data-ttu-id="14cfe-181">Questa modifica di configurazione può essere implementata nei dispositivi remoti dal portale della soluzione.</span><span class="sxs-lookup"><span data-stu-id="14cfe-181">You can push this configuration change to your remote devices from the solution portal.</span></span> <span data-ttu-id="14cfe-182">È possibile, ad esempio, apportare la modifica una volta, valutarne l'impatto e, in base ai risultati, intraprendere le azioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="14cfe-182">You can make the change once, evaluate the impact, and then act on the results.</span></span>

<span data-ttu-id="14cfe-183">Seguire questa procedura per eseguire un processo che consente di impostare la proprietà **TelemetryInterval** sul valore desiderato nei dispositivi interessati.</span><span class="sxs-lookup"><span data-stu-id="14cfe-183">Follow these steps to run a job that changes the **TelemetryInterval** desired property for the affected devices.</span></span> <span data-ttu-id="14cfe-184">Nel momento in cui dispositivi ricevono il nuovo valore della proprietà **TelemetryInterval**, modificano la propria configurazione in modo da inviare i dati di telemetria ogni cinque secondi anziché ogni 15 secondi.</span><span class="sxs-lookup"><span data-stu-id="14cfe-184">When the devices receive the new **TelemetryInterval** property value, they change their configuration to send telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="14cfe-185">Con l'elenco dei dispositivi impostato in modo da visualizzare solo i dispositivi non integri, scegliere **Pianificatore di processi** e quindi **Modifica dispositivo gemello**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-185">While you are showing the list of unhealthy devices in the device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="14cfe-186">Chiamare il processo **Change telemetry interval**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-186">Call the job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="14cfe-187">Impostare il valore di **Nome proprietà desiderata** **desired.Config.TelemetryInterval** su cinque secondi.</span><span class="sxs-lookup"><span data-stu-id="14cfe-187">Change the value of the **Desired Property** name **desired.Config.TelemetryInterval** to five seconds.</span></span>

1. <span data-ttu-id="14cfe-188">Scegliere **Pianifica**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-188">Choose **Schedule**.</span></span>

    ![Impostare la proprietà TelemetryInterval su cinque secondi][img-change-interval]

1. <span data-ttu-id="14cfe-190">È possibile monitorare lo stato di avanzamento del processo nella pagina **Processi di gestione** del portale.</span><span class="sxs-lookup"><span data-stu-id="14cfe-190">You can monitor the progress of the job on the **Management Jobs** page in the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="14cfe-191">Se si vuole modificare il valore di una proprietà desiderata per un singolo dispositivo, usare la sezione **Proprietà desiderate** disponibile nel pannello **Dettagli dispositivo** anziché eseguire un processo.</span><span class="sxs-lookup"><span data-stu-id="14cfe-191">If you want to change a desired property value for an individual device, use the **Desired Properties** section in the **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="14cfe-192">Questo processo imposta il valore della proprietà desiderata **TelemetryInterval** nel dispositivo gemello di tutti i dispositivi selezionati dal filtro.</span><span class="sxs-lookup"><span data-stu-id="14cfe-192">This job sets the value of the **TelemetryInterval** desired property in the device twin for all the devices selected by the filter.</span></span> <span data-ttu-id="14cfe-193">I dispositivi recuperano quindi questo valore dal rispettivo dispositivo gemello e aggiornano il proprio comportamento.</span><span class="sxs-lookup"><span data-stu-id="14cfe-193">The devices retrieve this value from the device twin and update their behavior.</span></span> <span data-ttu-id="14cfe-194">Quando un dispositivo recupera ed elabora una proprietà desiderata da un dispositivo gemello, imposta la proprietà del valore restituito corrispondente.</span><span class="sxs-lookup"><span data-stu-id="14cfe-194">When a device retrieves and processes a desired property from a device twin, it sets the corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="14cfe-195">Richiamare i metodi</span><span class="sxs-lookup"><span data-stu-id="14cfe-195">Invoke methods</span></span>

<span data-ttu-id="14cfe-196">Durante l'esecuzione del processo è possibile osservare come le versioni del firmware dei dispositivi non integri siano tutte non aggiornate (inferiori alla versione 1.6).</span><span class="sxs-lookup"><span data-stu-id="14cfe-196">While the job runs, you notice in the list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![Visualizzare la versione del firmware dei dispositivi non integri][img-old-firmware]

<span data-ttu-id="14cfe-198">La versione del firmware può essere la causa principale dei valori di temperatura imprevisti perché nel frattempo altri dispositivi integri sono stati aggiornati alla versione 2.0.</span><span class="sxs-lookup"><span data-stu-id="14cfe-198">This firmware version may be the root cause of the unexpected temperature values because you know that other healthy devices were recently updated to version 2.0.</span></span> <span data-ttu-id="14cfe-199">È possibile usare il filtro integrato **Old firmware devices** (Dispositivi con firmware non aggiornato) per identificare eventuali dispositivi con una versione del firmware non aggiornata.</span><span class="sxs-lookup"><span data-stu-id="14cfe-199">You can use the built-in **Old firmware devices** filter to identify any devices with old firmware versions.</span></span> <span data-ttu-id="14cfe-200">Dal portale è possibile aggiornare in remoto tutti i dispositivi che ancora eseguono versioni del firmware non aggiornate.</span><span class="sxs-lookup"><span data-stu-id="14cfe-200">From the portal, you can then remotely update all the devices still running old firmware versions:</span></span>

1. <span data-ttu-id="14cfe-201">Scegliere **Apri filtro salvato** per visualizzare un elenco dei filtri disponibili.</span><span class="sxs-lookup"><span data-stu-id="14cfe-201">Choose **Open saved filter** to display a list of available filters.</span></span> <span data-ttu-id="14cfe-202">Scegliere quindi **Old firmware devices** (Dispositivi con firmware non aggiornato) per applicare il filtro.</span><span class="sxs-lookup"><span data-stu-id="14cfe-202">Then choose **Old firmware devices** to apply the filter:</span></span>

    ![Visualizzare l'elenco dei filtri][img-old-filter]

1. <span data-ttu-id="14cfe-204">Nell'elenco dei dispositivi sono ora visualizzati solo i dispositivi con versioni del firmware non aggiornate,</span><span class="sxs-lookup"><span data-stu-id="14cfe-204">The device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="14cfe-205">inclusi i cinque dispositivi identificati dal filtro **Dispositivi non integri** e altri tre dispositivi.</span><span class="sxs-lookup"><span data-stu-id="14cfe-205">This list includes the five devices identified by the **Unhealthy devices** filter and three additional devices:</span></span>

    ![Visualizzare l'elenco dei dispositivi filtrato in modo che siano riportati solo i dispositivi con versioni del firmware non aggiornate][img-filtered-old-list]

1. <span data-ttu-id="14cfe-207">Scegliere **Pianificatore di processi** e quindi **Richiama metodo**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-207">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="14cfe-208">Impostare **Nome processo** su **Firmware update to version 2.0**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-208">Set **Job Name** to **Firmware update to version 2.0**.</span></span>

1. <span data-ttu-id="14cfe-209">Scegliere **InitiateFirmwareUpdate** come **Metodo**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-209">Choose **InitiateFirmwareUpdate** as the **Method**.</span></span>

1. <span data-ttu-id="14cfe-210">Impostare il parametro **FwPackageUri** su **https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-210">Set the **FwPackageUri** parameter to **https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="14cfe-211">Scegliere **Pianifica**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-211">Choose **Schedule**.</span></span> <span data-ttu-id="14cfe-212">Per impostazione predefinita, il processo viene eseguito ora.</span><span class="sxs-lookup"><span data-stu-id="14cfe-212">The default is for the job to run now.</span></span>

    ![Creare un processo per aggiornare il firmware dei dispositivi selezionati][img-method-update]

> [!NOTE]
> <span data-ttu-id="14cfe-214">Se si vuole richiamare un metodo su un singolo dispositivo, scegliere **Metodi** nel pannello **Dettagli dispositivo** anziché eseguire un processo.</span><span class="sxs-lookup"><span data-stu-id="14cfe-214">If you want to invoke a method on an individual device, choose **Methods** in the **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="14cfe-215">Con questo processo viene richiamato il metodo diretto **InitiateFirmwareUpdate** su tutti i dispositivi selezionati dal filtro.</span><span class="sxs-lookup"><span data-stu-id="14cfe-215">This job invokes the **InitiateFirmwareUpdate** direct method on all the devices selected by the filter.</span></span> <span data-ttu-id="14cfe-216">I dispositivi rispondono immediatamente all'hub IoT e quindi avviano il processo di aggiornamento del firmware in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="14cfe-216">Devices respond immediately to IoT Hub and then initiate the firmware update process asynchronously.</span></span> <span data-ttu-id="14cfe-217">I dispositivi usano inoltre i valori di proprietà restituiti per fornire informazioni sullo stato del processo di aggiornamento del firmware, come illustrato nelle schermate seguenti.</span><span class="sxs-lookup"><span data-stu-id="14cfe-217">The devices provide status information about the firmware update process through reported property values, as shown in the following screenshots.</span></span> <span data-ttu-id="14cfe-218">Scegliere l'icona **Aggiorna** per aggiornare le informazioni negli elenchi di processi e dispositivi.</span><span class="sxs-lookup"><span data-stu-id="14cfe-218">Choose the **Refresh** icon to update the information in the device and job lists:</span></span>

<span data-ttu-id="14cfe-219">![Elenco di processi con l'elenco degli aggiornamenti di firmware in esecuzione][img-update-1]
![Elenco di dispositivi con lo stato di aggiornamento del firmware][img-update-2]
![Elenco di processi con l'elenco degli aggiornamenti di firmware completati][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="14cfe-219">![Job list showing the firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing the firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="14cfe-220">In un ambiente di produzione è possibile pianificare i processi in modo che vengano eseguiti in un intervallo di manutenzione prestabilito.</span><span class="sxs-lookup"><span data-stu-id="14cfe-220">In a production environment, you can schedule jobs to run during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="14cfe-221">Analisi dello scenario</span><span class="sxs-lookup"><span data-stu-id="14cfe-221">Scenario review</span></span>

<span data-ttu-id="14cfe-222">In questo scenario è stato identificato un potenziale problema in alcuni dispositivi remoti usando la cronologia degli avvisi sul dashboard e un filtro.</span><span class="sxs-lookup"><span data-stu-id="14cfe-222">In this scenario, you identified a potential issue with some of your remote devices using the alarm history on the dashboard and a filter.</span></span> <span data-ttu-id="14cfe-223">Sono stati quindi usati il filtro e un processo per configurare in remoto i dispositivi in modo da fornire altre informazioni per facilitare la diagnosi del problema.</span><span class="sxs-lookup"><span data-stu-id="14cfe-223">You then used the filter and a job to remotely configure the devices to provide more information to help diagnose the issue.</span></span> <span data-ttu-id="14cfe-224">Sono stati usati infine un filtro e un processo per pianificare la manutenzione dei dispositivi interessati.</span><span class="sxs-lookup"><span data-stu-id="14cfe-224">Finally, you used a filter and a job to schedule maintenance on the affected devices.</span></span> <span data-ttu-id="14cfe-225">Se si torna al dashboard è possibile osservare che non è più presente alcun avviso proveniente da dispositivi inclusi nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="14cfe-225">If you return to the dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="14cfe-226">Con un apposito filtro è possibile anche verificare che il firmware sia aggiornato su tutti i dispositivi della soluzione e che non siano più presenti dispositivi non integri.</span><span class="sxs-lookup"><span data-stu-id="14cfe-226">You can use a filter to verify that the firmware is up-to-date on all the devices in your solution and that there are no more unhealthy devices:</span></span>

![Filtro che mostra come il firmware di tutti i dispositivi sia aggiornato][img-updated]

![Filtro che mostra come tutti i dispositivi siano integri][img-healthy]

## <a name="other-features"></a><span data-ttu-id="14cfe-229">Altre funzionalità</span><span class="sxs-lookup"><span data-stu-id="14cfe-229">Other features</span></span>

<span data-ttu-id="14cfe-230">Le sezioni seguenti descrivono alcune funzionalità aggiuntive della soluzione preconfigurata per il monitoraggio remoto non descritte nell'ambito dello scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="14cfe-230">The following sections describe some additional features of the remote monitoring preconfigured solution that are not described as part of the previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="14cfe-231">Personalizzare le colonne</span><span class="sxs-lookup"><span data-stu-id="14cfe-231">Customize columns</span></span>

<span data-ttu-id="14cfe-232">È possibile personalizzare le informazioni visualizzate nell'elenco dei dispositivi scegliendo **Editor di colonne**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-232">You can customize the information shown in the device list by choosing **Column editor**.</span></span> <span data-ttu-id="14cfe-233">È possibile aggiungere e rimuovere colonne che visualizzano i valori dei tag e delle proprietà segnalate,</span><span class="sxs-lookup"><span data-stu-id="14cfe-233">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="14cfe-234">nonché riordinare e rinominare le colonne:</span><span class="sxs-lookup"><span data-stu-id="14cfe-234">You can also reorder and rename columns:</span></span>

   ![Editor di colonne nell'elenco dei dispositivi][img-columneditor]

### <a name="customize-the-device-icon"></a><span data-ttu-id="14cfe-236">Personalizzare l'icona del dispositivo</span><span class="sxs-lookup"><span data-stu-id="14cfe-236">Customize the device icon</span></span>

<span data-ttu-id="14cfe-237">È possibile personalizzare l'icona del dispositivo visualizzata nell'elenco dei dispositivi dal pannello **Dettagli dispositivo**, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="14cfe-237">You can customize the device icon displayed in the device list from the **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="14cfe-238">Scegliere l'icona a forma di matita per aprire il pannello per la **modifica dell'immagine** per un dispositivo:</span><span class="sxs-lookup"><span data-stu-id="14cfe-238">Choose the pencil icon to open the **Edit image** panel for a device:</span></span>

   ![Editor di immagini per il dispositivo: apertura][img-startimageedit]

1. <span data-ttu-id="14cfe-240">Caricare una nuova immagine oppure usarne una esistente e quindi scegliere **Salva**:</span><span class="sxs-lookup"><span data-stu-id="14cfe-240">Either upload a new image or use one of the existing images and then choose **Save**:</span></span>

   ![Editor di immagini per il dispositivo: modifica][img-imageedit]

1. <span data-ttu-id="14cfe-242">L'immagine selezionata verrà visualizzata nella colonna **Icona** del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="14cfe-242">The image you selected now displays in the **Icon** column for the device.</span></span>

> [!NOTE]
> <span data-ttu-id="14cfe-243">L'immagine viene archiviata in un archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="14cfe-243">The image is stored in blob storage.</span></span> <span data-ttu-id="14cfe-244">Un tag nel dispositivo gemello contiene un collegamento all'immagine nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="14cfe-244">A tag in the device twin contains a link to the image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="14cfe-245">Aggiungere un dispositivo</span><span class="sxs-lookup"><span data-stu-id="14cfe-245">Add a device</span></span>

<span data-ttu-id="14cfe-246">Quando si distribuisce la soluzione preconfigurata, viene automaticamente effettuato il provisioning di 25 dispositivi che vengono visualizzati nell'elenco dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="14cfe-246">When you deploy the preconfigured solution, you automatically provision 25 sample devices that you can see in the device list.</span></span> <span data-ttu-id="14cfe-247">Si tratta di *dispositivi simulati* in esecuzione in un processo Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="14cfe-247">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="14cfe-248">I dispositivi simulati consentono di provare facilmente la soluzione preconfigurata senza la necessità di distribuire dispositivi fisici reali.</span><span class="sxs-lookup"><span data-stu-id="14cfe-248">Simulated devices make it easy for you to experiment with the preconfigured solution without the need to deploy real, physical devices.</span></span> <span data-ttu-id="14cfe-249">Per connettere un dispositivo reale alla soluzione, vedere l'esercitazione [Connettere il dispositivo alla soluzione preconfigurata per il monitoraggio remoto][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="14cfe-249">If you do want to connect a real device to the solution, see the [Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="14cfe-250">La procedura seguente illustra come aggiungere un dispositivo simulato alla soluzione:</span><span class="sxs-lookup"><span data-stu-id="14cfe-250">The following steps show you how to add a simulated device to the solution:</span></span>

1. <span data-ttu-id="14cfe-251">Tornare all'elenco dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="14cfe-251">Navigate back to the device list.</span></span>

1. <span data-ttu-id="14cfe-252">Per aggiungere un dispositivo, scegliere **Aggiungi un dispositivo** nell'angolo inferiore sinistro.</span><span class="sxs-lookup"><span data-stu-id="14cfe-252">To add a device, choose **+ Add A Device** in the bottom left corner.</span></span>

   ![Aggiungere un dispositivo alla soluzione preconfigurata][img-adddevice]

1. <span data-ttu-id="14cfe-254">Scegliere **Aggiungi nuovo** nel riquadro **Dispositivo simulato**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-254">Choose **Add New** on the **Simulated Device** tile.</span></span>

   ![Impostare i dettagli del nuovo dispositivo nel dashboard][img-addnew]

   <span data-ttu-id="14cfe-256">Oltre a creare un nuovo dispositivo simulato, è anche possibile aggiungere un dispositivo fisico se si sceglie di creare un **dispositivo personalizzato**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-256">In addition to creating a new simulated device, you can also add a physical device if you choose to create a **Custom Device**.</span></span> <span data-ttu-id="14cfe-257">Per altre informazioni sulla connessione di dispositivi fisici alla soluzione, vedere [Connettere il dispositivo alla soluzione preconfigurata per il monitoraggio remoto IoT Suite][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="14cfe-257">To learn more about connecting physical devices to the solution, see [Connect your device to the IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="14cfe-258">Selezionare **Let me define my own Device ID** (Definire l'ID dispositivo personale) e immettere un nome di ID dispositivo univoco, ad esempio **mydevice_01**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="14cfe-259">Scegliere **Create**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-259">Choose **Create**.</span></span>

   ![Salvare un nuovo dispositivo][img-definedevice]

1. <span data-ttu-id="14cfe-261">Nel passaggio 3 della procedura **Add a simulated device** (Aggiungi un dispositivo simulato) scegliere **Fatto** per tornare all'elenco dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="14cfe-261">In step 3 of **Add a simulated device**, choose **Done** to return to the device list.</span></span>

1. <span data-ttu-id="14cfe-262">Verificare che lo stato del dispositivo nell'elenco sia **In esecuzione** .</span><span class="sxs-lookup"><span data-stu-id="14cfe-262">You can view your device **Running** in the device list.</span></span>

    ![Visualizzare il nuovo dispositivo nell'elenco dei dispositivi][img-runningnew]

1. <span data-ttu-id="14cfe-264">È anche possibile visualizzare la telemetria simulata dal nuovo dispositivo nel dashboard:</span><span class="sxs-lookup"><span data-stu-id="14cfe-264">You can also view the simulated telemetry from your new device on the dashboard:</span></span>

    ![Visualizzare i dati di telemetria dal nuovo dispositivo][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="14cfe-266">Disabilitare e rimuovere un dispositivo</span><span class="sxs-lookup"><span data-stu-id="14cfe-266">Disable and delete a device</span></span>

<span data-ttu-id="14cfe-267">È possibile disabilitare un dispositivo e dopo aver disabilitato è possibile rimuoverlo:</span><span class="sxs-lookup"><span data-stu-id="14cfe-267">You can disable a device, and after it is disabled you can remove it:</span></span>

![Disabilitare e rimuovere un dispositivo][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="14cfe-269">Aggiungere una regola</span><span class="sxs-lookup"><span data-stu-id="14cfe-269">Add a rule</span></span>

<span data-ttu-id="14cfe-270">Non sono presenti regole per il nuovo dispositivo appena aggiunto.</span><span class="sxs-lookup"><span data-stu-id="14cfe-270">There are no rules for the new device you just added.</span></span> <span data-ttu-id="14cfe-271">In questa sezione si aggiunge una regola che attiva un avviso quando la temperatura segnalata dal nuovo dispositivo supera i 47 gradi.</span><span class="sxs-lookup"><span data-stu-id="14cfe-271">In this section, you add a rule that triggers an alarm when the temperature reported by the new device exceeds 47 degrees.</span></span> <span data-ttu-id="14cfe-272">Prima di iniziare, si noti che la cronologia della telemetria per il nuovo dispositivo nel dashboard indica che la temperatura del dispositivo non supera mai i 45 gradi.</span><span class="sxs-lookup"><span data-stu-id="14cfe-272">Before you start, notice that the telemetry history for the new device on the dashboard shows the device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="14cfe-273">Tornare all'elenco dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="14cfe-273">Navigate back to the device list.</span></span>

1. <span data-ttu-id="14cfe-274">Per aggiungere una regola per il dispositivo, selezionare il nuovo dispositivo nell'**elenco dei dispositivi** e quindi scegliere **Aggiungi regola**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-274">To add a rule for the device, select your new device in the **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="14cfe-275">Creare una regola che usa **Temperature** come campo dati e **AlarmTemp** come output quando la temperatura supera i 47 gradi:</span><span class="sxs-lookup"><span data-stu-id="14cfe-275">Create a rule that uses **Temperature** as the data field and uses **AlarmTemp** as the output when the temperature exceeds 47 degrees:</span></span>

    ![Aggiungere una regola per il dispositivo][img-adddevicerule]

1. <span data-ttu-id="14cfe-277">Per salvare le modifiche, scegliere **Salva e visualizza regole**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-277">To save your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="14cfe-278">Scegliere **Comandi** nel riquadro dei dettagli del nuovo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="14cfe-278">Choose **Commands** in the device details pane for the new device.</span></span>

    ![Aggiungere una regola per il dispositivo][img-adddevicerule2]

1. <span data-ttu-id="14cfe-280">Selezionare **ChangeSetPointTemp** nell'elenco dei comandi e impostare **SetPointTemp** su 45.</span><span class="sxs-lookup"><span data-stu-id="14cfe-280">Select **ChangeSetPointTemp** from the command list and set **SetPointTemp** to 45.</span></span> <span data-ttu-id="14cfe-281">Scegliere quindi **Invia comando**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-281">Then choose **Send Command**:</span></span>

    ![Aggiungere una regola per il dispositivo][img-adddevicerule3]

1. <span data-ttu-id="14cfe-283">Tornare al dashboard.</span><span class="sxs-lookup"><span data-stu-id="14cfe-283">Navigate back to the dashboard.</span></span> <span data-ttu-id="14cfe-284">Poco dopo verrà visualizzata una nuova voce nel riquadro **Cronologia avvisi** quando la temperatura segnalata dal nuovo dispositivo supera la soglia di 47 gradi:</span><span class="sxs-lookup"><span data-stu-id="14cfe-284">After a short time, you will see a new entry in the **Alarm History** pane when the temperature reported by your new device exceeds the 47-degree threshold:</span></span>

    ![Aggiungere una regola per il dispositivo][img-adddevicerule4]

1. <span data-ttu-id="14cfe-286">È possibile rivedere e modificare tutte le regole nella pagina **Regole** del dashboard:</span><span class="sxs-lookup"><span data-stu-id="14cfe-286">You can review and edit all your rules on the **Rules** page of the dashboard:</span></span>

    ![Elenco delle regole per il dispositivo][img-rules]

1. <span data-ttu-id="14cfe-288">È possibile rivedere e modificare tutte le azioni che possono essere eseguite in risposta a una regola nella pagina **Azioni** del dashboard:</span><span class="sxs-lookup"><span data-stu-id="14cfe-288">You can review and edit all the actions that can be taken in response to a rule on the **Actions** page of the dashboard:</span></span>

    ![Elenco delle azioni per il dispositivo][img-actions]

> [!NOTE]
> <span data-ttu-id="14cfe-290">È possibile definire azioni che possono inviare un messaggio di posta elettronica o un SMS in risposta a una regola oppure eseguire un'integrazione con un sistema line-of-business tramite un'[app per la logica][lnk-logic-apps].</span><span class="sxs-lookup"><span data-stu-id="14cfe-290">It is possible to define actions that can send an email message or SMS in response to a rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="14cfe-291">Per altre informazioni, vedere [Connettere l'app per la logica alla soluzione preconfigurata per il monitoraggio remoto Azure IoT Suite][lnk-logicapptutorial].</span><span class="sxs-lookup"><span data-stu-id="14cfe-291">For more information, see the [Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="14cfe-292">Gestire i filtri</span><span class="sxs-lookup"><span data-stu-id="14cfe-292">Manage filters</span></span>

<span data-ttu-id="14cfe-293">Nell'elenco dei dispositivi è possibile creare, salvare e ricaricare filtri per visualizzare un elenco personalizzato dei dispositivi connessi all'hub.</span><span class="sxs-lookup"><span data-stu-id="14cfe-293">In the device list, you can create, save, and reload filters to display a customized list of devices connected to your hub.</span></span> <span data-ttu-id="14cfe-294">Per creare un filtro:</span><span class="sxs-lookup"><span data-stu-id="14cfe-294">To create a filter:</span></span>

1. <span data-ttu-id="14cfe-295">Scegliere l'icona di modifica dei filtri sopra l'elenco dei dispositivi:</span><span class="sxs-lookup"><span data-stu-id="14cfe-295">Choose the edit filter icon above the list of devices:</span></span>

    ![Aprire l'editor dei filtri][img-editfiltericon]

1. <span data-ttu-id="14cfe-297">In **Editor dei filtri** aggiungere i campi, gli operatori e i valori per filtrare l'elenco dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="14cfe-297">In the **Filter editor**, add the fields, operators, and values to filter the device list.</span></span> <span data-ttu-id="14cfe-298">È possibile aggiungere più clausole per perfezionare il filtro.</span><span class="sxs-lookup"><span data-stu-id="14cfe-298">You can add multiple clauses to refine your filter.</span></span> <span data-ttu-id="14cfe-299">Scegliere **Filtra** per applicare il filtro:</span><span class="sxs-lookup"><span data-stu-id="14cfe-299">Choose **Filter** to apply the filter:</span></span>

    ![Creare un filtro][img-filtereditor]

1. <span data-ttu-id="14cfe-301">In questo esempio, l'elenco è filtrato in base al produttore e al numero di modello:</span><span class="sxs-lookup"><span data-stu-id="14cfe-301">In this example, the list is filtered by manufacturer and model number:</span></span>

    ![Elenco filtrato][img-filterelist]

1. <span data-ttu-id="14cfe-303">Per salvare il filtro con un nome personalizzato, scegliere l'icona **Salva con nome**:</span><span class="sxs-lookup"><span data-stu-id="14cfe-303">To save your filter with a custom name, choose the **Save as** icon:</span></span>

    ![Salvare un filtro][img-savefilter]

1. <span data-ttu-id="14cfe-305">Per riapplicare un filtro salvato in precedenza, scegliere l'icona **Apri filtro salvato**:</span><span class="sxs-lookup"><span data-stu-id="14cfe-305">To reapply a filter you saved previously, choose the **Open saved filter** icon:</span></span>

    ![Aprire un filtro][img-openfilter]

<span data-ttu-id="14cfe-307">È possibile creare filtri basati sull'ID dispositivo, sullo stato del dispositivo, sulle proprietà desiderate, sulle proprietà segnalate e sui tag.</span><span class="sxs-lookup"><span data-stu-id="14cfe-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="14cfe-308">Per aggiungere tag personalizzati a un dispositivo è possibile usare la sezione **Tag** del pannello **Dettagli dispositivo** oppure eseguire un processo per l'aggiornamento dei tag in più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="14cfe-308">You add your own custom tags to a device in the **Tags** section of the **Device Details** panel, or run a job to update tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="14cfe-309">In **Editor dei filtri** è possibile usare la **visualizzazione avanzata** per modificare direttamente il testo della query.</span><span class="sxs-lookup"><span data-stu-id="14cfe-309">In the **Filter editor**, you can use the **Advanced view** to edit the query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="14cfe-310">Comandi:</span><span class="sxs-lookup"><span data-stu-id="14cfe-310">Commands</span></span>

<span data-ttu-id="14cfe-311">Dal pannello **Dettagli dispositivo** è possibile inviare comandi al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="14cfe-311">From the **Device Details** panel, you can send commands to the device.</span></span> <span data-ttu-id="14cfe-312">Quando un dispositivo viene avviato per la prima volta, invia alla soluzione informazioni sui comandi che supporta.</span><span class="sxs-lookup"><span data-stu-id="14cfe-312">When a device first starts, it sends information about the commands it supports to the solution.</span></span> <span data-ttu-id="14cfe-313">Per un approfondimento sulle differenze tra comandi e metodi, vedere [Opzioni da cloud a dispositivo di Azure IoT Hub][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="14cfe-313">For a discussion of the differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="14cfe-314">Scegliere **Comandi** nel pannello **Dettagli dispositivo** del dispositivo selezionato:</span><span class="sxs-lookup"><span data-stu-id="14cfe-314">Choose **Commands** in the **Device Details** panel for the selected device:</span></span>

   ![Comandi del dispositivo nel dashboard][img-devicecommands]

1. <span data-ttu-id="14cfe-316">Selezionare **PingDevice** dall'elenco dei comandi.</span><span class="sxs-lookup"><span data-stu-id="14cfe-316">Select **PingDevice** from the command list.</span></span>

1. <span data-ttu-id="14cfe-317">Scegliere **Invia comando**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-317">Choose **Send Command**.</span></span>

1. <span data-ttu-id="14cfe-318">È possibile visualizzare lo stato del comando nella cronologia dei comandi.</span><span class="sxs-lookup"><span data-stu-id="14cfe-318">You can see the status of the command in the command history.</span></span>

   ![Stato dei comandi nel dashboard][img-pingcommand]

<span data-ttu-id="14cfe-320">La soluzione tiene traccia dello stato di ogni comando inviato.</span><span class="sxs-lookup"><span data-stu-id="14cfe-320">The solution tracks the status of each command it sends.</span></span> <span data-ttu-id="14cfe-321">All'inizio il risultato è **In sospeso**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-321">Initially the result is **Pending**.</span></span> <span data-ttu-id="14cfe-322">Quando il dispositivo segnala che il comando è stato eseguito, il risultato viene impostato su **Operazione riuscita**.</span><span class="sxs-lookup"><span data-stu-id="14cfe-322">When the device reports that it has executed the command, the result is set to **Success**.</span></span>

## <a name="behind-the-scenes"></a><span data-ttu-id="14cfe-323">Dietro le quinte</span><span class="sxs-lookup"><span data-stu-id="14cfe-323">Behind the scenes</span></span>

<span data-ttu-id="14cfe-324">Quando si distribuisce una soluzione preconfigurata, il processo di distribuzione crea più risorse nella sottoscrizione di Azure selezionata.</span><span class="sxs-lookup"><span data-stu-id="14cfe-324">When you deploy a preconfigured solution, the deployment process creates multiple resources in the Azure subscription you selected.</span></span> <span data-ttu-id="14cfe-325">È possibile visualizzare queste risorse nel [portale][lnk-portal] di Azure.</span><span class="sxs-lookup"><span data-stu-id="14cfe-325">You can view these resources in the Azure [portal][lnk-portal].</span></span> <span data-ttu-id="14cfe-326">Il processo di distribuzione crea un **gruppo di risorse** con un nome basato sul nome scelto per la soluzione preconfigurata:</span><span class="sxs-lookup"><span data-stu-id="14cfe-326">The deployment process creates a **resource group** with a name based on the name you choose for your preconfigured solution:</span></span>

![Soluzione preconfigurata nel portale di Azure][img-portal]

<span data-ttu-id="14cfe-328">È possibile visualizzare le impostazioni di ogni risorsa selezionandola nell'elenco di risorse nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="14cfe-328">You can view the settings of each resource by selecting it in the list of resources in the resource group.</span></span>

<span data-ttu-id="14cfe-329">È anche possibile visualizzare il codice sorgente per la soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="14cfe-329">You can also view the source code for the preconfigured solution.</span></span> <span data-ttu-id="14cfe-330">Il codice sorgente della soluzione preconfigurata per il monitoraggio remoto si trova nel repository GitHub [azure-iot-remote-monitoring][lnk-rmgithub]:</span><span class="sxs-lookup"><span data-stu-id="14cfe-330">The remote monitoring preconfigured solution source code is in the [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="14cfe-331">La cartella **DeviceAdministration** contiene il codice sorgente per il dashboard.</span><span class="sxs-lookup"><span data-stu-id="14cfe-331">The **DeviceAdministration** folder contains the source code for the dashboard.</span></span>
* <span data-ttu-id="14cfe-332">La cartella **Simulator** contiene il codice sorgente per il dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="14cfe-332">The **Simulator** folder contains the source code for the simulated device.</span></span>
* <span data-ttu-id="14cfe-333">La cartella **EventProcessor** contiene il codice sorgente per il processo back-end che gestisce la telemetria in ingresso.</span><span class="sxs-lookup"><span data-stu-id="14cfe-333">The **EventProcessor** folder contains the source code for the back-end process that handles the incoming telemetry.</span></span>

<span data-ttu-id="14cfe-334">Al termine, è possibile eliminare la soluzione preconfigurata dalla sottoscrizione di Azure nel sito [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="14cfe-334">When you are done, you can delete the preconfigured solution from your Azure subscription on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="14cfe-335">Questo sito consente di eliminare facilmente tutte le risorse di cui è stato effettuato il provisioning quando si è creata la soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="14cfe-335">This site enables you to easily delete all the resources that were provisioned when you created the preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="14cfe-336">Per assicurarsi di eliminare tutti gli elementi correlati alla soluzione preconfigurata, eliminarli dal sito [azureiotsuite.com][lnk-azureiotsuite] e non eliminare il gruppo di risorse nel portale.</span><span class="sxs-lookup"><span data-stu-id="14cfe-336">To ensure that you delete everything related to the preconfigured solution, delete it on the [azureiotsuite.com][lnk-azureiotsuite] site and do not delete the resource group in the portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14cfe-337">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="14cfe-337">Next Steps</span></span>

<span data-ttu-id="14cfe-338">Dopo aver distribuito una soluzione preconfigurata è possibile proseguire con l'introduzione a IoT Suite vedendo gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="14cfe-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="14cfe-339">[Procedura dettagliata della soluzione preconfigurata per il monitoraggio remoto][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="14cfe-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="14cfe-340">[Connettere il dispositivo alla soluzione preconfigurata per il monitoraggio remoto][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="14cfe-340">[Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="14cfe-341">[Autorizzazioni per il sito azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="14cfe-341">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

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