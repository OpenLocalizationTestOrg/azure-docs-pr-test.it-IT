---
title: aaaConnect un dispositivo utilizzando C su mbed | Documenti Microsoft
description: Viene descritto come tooconnect toohello un dispositivo Azure IoT Suite preconfigurati con un'applicazione scritta in C in esecuzione in un dispositivo mbed soluzione di monitoraggio remoto.
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a><span data-ttu-id="11847-103">Connettersi toohello il dispositivo remoto monitoraggio soluzione preconfigurata (mbed)</span><span class="sxs-lookup"><span data-stu-id="11847-103">Connect your device toohello remote monitoring preconfigured solution (mbed)</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="11847-104">Panoramica dello scenario</span><span class="sxs-lookup"><span data-stu-id="11847-104">Scenario overview</span></span>
<span data-ttu-id="11847-105">In questo scenario, si crea un dispositivo che invia hello seguendo il monitoraggio remoto di dati di telemetria toohello [preconfigurato soluzione][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="11847-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="11847-106">Temperatura esterna</span><span class="sxs-lookup"><span data-stu-id="11847-106">External temperature</span></span>
* <span data-ttu-id="11847-107">Temperatura interna</span><span class="sxs-lookup"><span data-stu-id="11847-107">Internal temperature</span></span>
* <span data-ttu-id="11847-108">Umidità</span><span class="sxs-lookup"><span data-stu-id="11847-108">Humidity</span></span>

<span data-ttu-id="11847-109">Per semplicità, codice hello sul dispositivo hello genera valori di esempio, ma che incoraggia la collaborazione è tooextend: esempio hello connettendosi dispositivo tooyour sensori reale e l'invio di dati di telemetria reale.</span><span class="sxs-lookup"><span data-stu-id="11847-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="11847-110">dispositivo Hello è anche toomethods toorespond in grado di richiamata dal dashboard di soluzione hello e valori di proprietà impostati in dashboard soluzione hello desiderati.</span><span class="sxs-lookup"><span data-stu-id="11847-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="11847-111">toocomplete questa esercitazione, è necessario un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="11847-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="11847-112">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="11847-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="11847-113">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="11847-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="11847-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="11847-114">Before you start</span></span>
<span data-ttu-id="11847-115">Prima di scrivere un codice per il dispositivo, occorre eseguire la soluzione preconfigurata di monitoraggio remoto e poi effettuare il provisioning di un nuovo dispositivo personalizzato all'interno della soluzione in questione.</span><span class="sxs-lookup"><span data-stu-id="11847-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="11847-116">Eseguire il provisioning della soluzione preconfigurata per il monitoraggio remoto</span><span class="sxs-lookup"><span data-stu-id="11847-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="11847-117">dispositivo Hello si creerà in questa esercitazione invia istanza tooan dati hello [monitoraggio remoto] [ lnk-remote-monitoring] preconfigurato soluzione.</span><span class="sxs-lookup"><span data-stu-id="11847-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="11847-118">Se non hai già effettuato il provisioning hello soluzione preconfigurata nell'account di Azure di monitoraggio remoto, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="11847-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="11847-119">In hello <https://www.azureiotsuite.com/> pagina, fare clic su  **+**  toocreate una soluzione.</span><span class="sxs-lookup"><span data-stu-id="11847-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="11847-120">Fare clic su **selezionare** su hello **monitoraggio remoto** pannello toocreate la soluzione.</span><span class="sxs-lookup"><span data-stu-id="11847-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="11847-121">In hello **creare il monitoraggio remoto soluzione** pagina, immettere un **Nome soluzione** di propria scelta, selezionare hello **area** toodeploy per desiderati e selezionare hello Azure toouse toowant di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="11847-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="11847-122">Fare clic su **Crea soluzione**.</span><span class="sxs-lookup"><span data-stu-id="11847-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="11847-123">Attendere il completamento di hello processo di provisioning.</span><span class="sxs-lookup"><span data-stu-id="11847-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="11847-124">le soluzioni di Hello preconfigurato utilizzano fatturabili servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="11847-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="11847-125">Verificare tooremove hello soluzione preconfigurata dalla sottoscrizione di una volta con esso tooavoid eventuali addebiti non necessari.</span><span class="sxs-lookup"><span data-stu-id="11847-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="11847-126">È possibile rimuovere completamente una soluzione preconfigurata dalla sottoscrizione, visitare hello <https://www.azureiotsuite.com/> pagina.</span><span class="sxs-lookup"><span data-stu-id="11847-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="11847-127">Termine del processo per la soluzione di monitoraggio remoto hello di provisioning hello, fare clic su **avviare** dashboard di soluzione hello tooopen nel browser.</span><span class="sxs-lookup"><span data-stu-id="11847-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![Dashboard della soluzione][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="11847-129">Eseguire il provisioning del dispositivo nella soluzione di monitoraggio remoto hello</span><span class="sxs-lookup"><span data-stu-id="11847-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="11847-130">Se è già stato eseguito il provisioning di un dispositivo nella soluzione, è possibile saltare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="11847-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="11847-131">Quando si crea un'applicazione client hello, sono necessarie le credenziali di dispositivo di tooknow hello.</span><span class="sxs-lookup"><span data-stu-id="11847-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="11847-132">Per una soluzione di dispositivo tooconnect toohello preconfigurato, deve identificarsi tooIoT Hub usando credenziali valide.</span><span class="sxs-lookup"><span data-stu-id="11847-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="11847-133">È possibile recuperare le credenziali di dispositivo hello dal dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="11847-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="11847-134">Includere le credenziali di dispositivo hello nell'applicazione client più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="11847-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="11847-135">tooadd una soluzione di monitoraggio remoto tooyour di dispositivo, hello completo seguendo i passaggi nel dashboard di soluzione hello:</span><span class="sxs-lookup"><span data-stu-id="11847-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="11847-136">Hello angolo in basso a sinistra del dashboard hello, fare clic su **aggiunge un dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="11847-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![Aggiungere un dispositivo][1]
2. <span data-ttu-id="11847-138">In hello **dispositivo personalizzato** pannello, fare clic su **Aggiungi nuovo**.</span><span class="sxs-lookup"><span data-stu-id="11847-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![Aggiungere un dispositivo personalizzato][2]
3. <span data-ttu-id="11847-140">Scegliere **Let me define my own Device ID** (Desidero definire il mio ID dispositivo).</span><span class="sxs-lookup"><span data-stu-id="11847-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="11847-141">Immettere un ID dispositivo, ad esempio **mydevice**, fare clic su **ID controllo** tooverify tale nome è già in uso e quindi fare clic su **crea** dispositivo hello tooprovision.</span><span class="sxs-lookup"><span data-stu-id="11847-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![Aggiungere un ID dispositivo][3]
4. <span data-ttu-id="11847-143">Rendere un dispositivo di hello nota le credenziali (ID dispositivo, nome host di Hub IoT e chiave del dispositivo).</span><span class="sxs-lookup"><span data-stu-id="11847-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="11847-144">L'applicazione client deve questi toohello tooconnect valori soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="11847-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="11847-145">Fare quindi clic su **Done**.</span><span class="sxs-lookup"><span data-stu-id="11847-145">Then click **Done**.</span></span>
   
    ![Vedere le credenziali del dispositivo][4]
5. <span data-ttu-id="11847-147">Selezionare il dispositivo nell'elenco di dispositivi hello nel dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="11847-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="11847-148">Quindi, nel hello **dettagli dispositivo** pannello, fare clic su **Abilita periferica**.</span><span class="sxs-lookup"><span data-stu-id="11847-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="11847-149">lo stato di Hello del dispositivo è ora **esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="11847-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="11847-150">soluzione di monitoraggio remoto Hello possa ora ricevere i dati di telemetria dal dispositivo e richiamare metodi sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="11847-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a><span data-ttu-id="11847-151">Compilare ed eseguire la soluzione di esempio hello C</span><span class="sxs-lookup"><span data-stu-id="11847-151">Build and run hello C sample solution</span></span>

<span data-ttu-id="11847-152">Hello istruzioni seguenti vengono descritti hello passaggi per la connessione di un [FRDM-K64F abilitato mbed Freescale] [ lnk-mbed-home] toohello dispositivo remoto nella soluzione di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="11847-152">hello following instructions describe hello steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device toohello remote monitoring solution.</span></span>

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a><span data-ttu-id="11847-153">La connessione di rete tooyour di hello mbed dispositivi e computer desktop</span><span class="sxs-lookup"><span data-stu-id="11847-153">Connect hello mbed device tooyour network and desktop machine</span></span>

1. <span data-ttu-id="11847-154">Connettere hello mbed dispositivo tooyour rete tramite un cavo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="11847-154">Connect hello mbed device tooyour network using an Ethernet cable.</span></span> <span data-ttu-id="11847-155">Questo passaggio è necessario perché l'applicazione di esempio hello richiede l'accesso a internet.</span><span class="sxs-lookup"><span data-stu-id="11847-155">This step is necessary because hello sample application requires internet access.</span></span>

1. <span data-ttu-id="11847-156">Vedere [introduzione mbed] [ lnk-mbed-getstarted] tooconnect desktop tooyour mbed dispositivo PC.</span><span class="sxs-lookup"><span data-stu-id="11847-156">See [Getting Started with mbed][lnk-mbed-getstarted] tooconnect your mbed device tooyour desktop PC.</span></span>

1. <span data-ttu-id="11847-157">Se il PC è in esecuzione Windows, vedere [configurazione PC] [ lnk-mbed-pcconnect] dispositivo mbed tooyour di tooconfigure porta seriale accesso.</span><span class="sxs-lookup"><span data-stu-id="11847-157">If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] tooconfigure serial port access tooyour mbed device.</span></span>

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a><span data-ttu-id="11847-158">Creare un progetto mbed e importare il codice di esempio hello</span><span class="sxs-lookup"><span data-stu-id="11847-158">Create an mbed project and import hello sample code</span></span>

<span data-ttu-id="11847-159">Seguire questi passaggi tooadd un progetto di esempio codice tooan mbed.</span><span class="sxs-lookup"><span data-stu-id="11847-159">Follow these steps tooadd some sample code tooan mbed project.</span></span> <span data-ttu-id="11847-160">Importare il progetto di avvio di hello remoto monitoraggio e quindi modificare hello toouse di hello progetto protocollo MQTT anziché hello protocollo AMQP.</span><span class="sxs-lookup"><span data-stu-id="11847-160">You import hello remote monitoring starter project and then change hello project toouse hello MQTT protocol instead of hello AMQP protocol.</span></span> <span data-ttu-id="11847-161">Attualmente, è necessario toouse hello MQTT protocollo toouse hello dispositivo funzionalità di gestione di IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="11847-161">Currently, you need toouse hello MQTT protocol toouse hello device management features of IoT Hub.</span></span>

1. <span data-ttu-id="11847-162">Nel web browser, visitare toohello mbed.org [sito per sviluppatori](https://developer.mbed.org/).</span><span class="sxs-lookup"><span data-stu-id="11847-162">In your web browser, go toohello mbed.org [developer site](https://developer.mbed.org/).</span></span> <span data-ttu-id="11847-163">Se si è ancora iscritti, viene visualizzato un toocreate opzione account (è disponibile).</span><span class="sxs-lookup"><span data-stu-id="11847-163">If you haven't signed up, you see an option toocreate an account (it's free).</span></span> <span data-ttu-id="11847-164">In caso contrario, accedere con le credenziali dell'account.</span><span class="sxs-lookup"><span data-stu-id="11847-164">Otherwise, log in with your account credentials.</span></span> <span data-ttu-id="11847-165">Quindi fare clic su **compilatore** in hello nell'angolo superiore destro della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="11847-165">Then click **Compiler** in hello upper right-hand corner of hello page.</span></span> <span data-ttu-id="11847-166">Questa azione consente di toohello *dell'area di lavoro* interfaccia.</span><span class="sxs-lookup"><span data-stu-id="11847-166">This action brings you toohello *Workspace* interface.</span></span>

1. <span data-ttu-id="11847-167">Assicurarsi che piattaforma hardware hello in uso nella hello nell'angolo superiore destro della finestra hello, oppure fare clic sull'icona di hello in hello nell'angolo destro tooselect la piattaforma hardware.</span><span class="sxs-lookup"><span data-stu-id="11847-167">Make sure hello hardware platform you're using appears in hello upper right-hand corner of hello window, or click hello icon in hello right-hand corner tooselect your hardware platform.</span></span>

1. <span data-ttu-id="11847-168">Fare clic su **importazione** nel menu principale di hello.</span><span class="sxs-lookup"><span data-stu-id="11847-168">Click **Import** on hello main menu.</span></span> <span data-ttu-id="11847-169">Quindi fare clic su **fare clic qui tooimport dall'URL**.</span><span class="sxs-lookup"><span data-stu-id="11847-169">Then click **Click here tooimport from URL**.</span></span>
   
    ![Avviare l'importazione dell'area di lavoro toombed][6]

1. <span data-ttu-id="11847-171">Nella finestra popup hello, immettere il collegamento hello per hello esempio codice https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/, quindi fare clic su **importazione**.</span><span class="sxs-lookup"><span data-stu-id="11847-171">In hello pop-up window, enter hello link for hello sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.</span></span>
   
    ![Importare l'area di lavoro di esempio codice toombed][7]

1. <span data-ttu-id="11847-173">È possibile visualizzare nella finestra di hello mbed del compilatore che l'importazione di questo progetto Importa anche diverse librerie.</span><span class="sxs-lookup"><span data-stu-id="11847-173">You can see in hello mbed compiler window that importing this project also imports various libraries.</span></span> <span data-ttu-id="11847-174">Alcuni sono forniti e gestiti dal team di Azure IoT hello ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), mentre altri sono disponibili nel catalogo di librerie mbed hello librerie di terze parti.</span><span class="sxs-lookup"><span data-stu-id="11847-174">Some are provided and maintained by hello Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in hello mbed libraries catalog.</span></span>
   
    ![Visualizzare il progetto mbed][8]

1. <span data-ttu-id="11847-176">In hello **programma dell'area di lavoro**, hello rapida **hub IOT\_amqp\_trasporto** libreria, fare clic su **eliminare**, quindi fare clic su **OK** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="11847-176">In hello **Program Workspace**, right-click hello **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="11847-177">In hello **programma dell'area di lavoro**, hello rapida **azure\_amqp\_c** libreria, fare clic su **eliminare**, quindi fare clic su **OK**  tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="11847-177">In hello **Program Workspace**, right-click hello **azure\_amqp\_c** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="11847-178">Pulsante destro del mouse hello **remote_monitoring** progetto in hello **programma dell'area di lavoro**selezionare **libreria di importazione**, quindi selezionare **From URL**.</span><span class="sxs-lookup"><span data-stu-id="11847-178">Right-click hello **remote_monitoring** project in hello **Program Workspace**, select **Import Library**, then select **From URL**.</span></span>
   
    ![Avviare l'area di lavoro toombed importazione libreria][6]

1. <span data-ttu-id="11847-180">Nella finestra popup hello, immettere il collegamento hello per hello MQTT trasporto libreria https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_trasporto / quindi fare clic su **importazione**.</span><span class="sxs-lookup"><span data-stu-id="11847-180">In hello pop-up window, enter hello link for hello MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.</span></span>
   
    ![Importare l'area di lavoro libreria toombed][12]

1. <span data-ttu-id="11847-182">Hello ripetere il passaggio tooadd hello MQTT libreria precedente da https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.</span><span class="sxs-lookup"><span data-stu-id="11847-182">Repeat hello previous step tooadd hello MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span></span>

1. <span data-ttu-id="11847-183">L'area di lavoro è ora simile hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="11847-183">Your workspace now looks like hello following:</span></span>

    ![Visualizzare l'area di lavoro mbed][13]

1. <span data-ttu-id="11847-185">Aprire hello remoto\_monitoring\remote_monitoring.c file e sostituire hello esistente `#include` istruzioni con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="11847-185">Open hello remote\_monitoring\remote_monitoring.c file and replace hello existing `#include` statements with hello following code:</span></span>

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. <span data-ttu-id="11847-186">Eliminare tutti hello rimanenti codice hello remoto\_monitoring\remote\_monitoring.c file.</span><span class="sxs-lookup"><span data-stu-id="11847-186">Delete all hello remaining code in hello remote\_monitoring\remote\_monitoring.c file.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="11847-187">Compilare ed eseguire l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="11847-187">Build and run hello sample</span></span>

<span data-ttu-id="11847-188">Aggiungere hello tooinvoke codice **remoto\_monitoraggio\_eseguire** funzione e quindi compilare ed eseguire un'applicazione hello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="11847-188">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="11847-189">Aggiungere un **principale** funzione con il codice seguente alla fine hello hello remoto\_hello tooinvoke di file monitoring.c **remoto\_monitoraggio\_eseguire** funzione:</span><span class="sxs-lookup"><span data-stu-id="11847-189">Add a **main** function with following code at hello end of hello remote\_monitoring.c file tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="11847-190">Fare clic su **compilare** programma hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="11847-190">Click **Compile** toobuild hello program.</span></span> <span data-ttu-id="11847-191">È possibile in modo sicuro ignorare eventuali avvisi, ma se la compilazione hello genera errori, risolverli prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="11847-191">You can safely ignore any warnings, but if hello build generates errors, fix them before proceeding.</span></span>

1. <span data-ttu-id="11847-192">Se la compilazione hello ha esito positivo, sito Web di hello mbed del compilatore genera un file con estensione bin con il nome di hello del progetto e lo scarica tooyour di computer locale.</span><span class="sxs-lookup"><span data-stu-id="11847-192">If hello build is successful, hello mbed compiler website generates a .bin file with hello name of your project and downloads it tooyour local machine.</span></span> <span data-ttu-id="11847-193">Dispositivo di toohello file con estensione bin hello copia.</span><span class="sxs-lookup"><span data-stu-id="11847-193">Copy hello .bin file toohello device.</span></span> <span data-ttu-id="11847-194">Il salvataggio di dispositivo toohello di file con estensione bin hello causa toorestart dispositivo hello ed esegue il programma hello contenuto nel file con estensione bin hello.</span><span class="sxs-lookup"><span data-stu-id="11847-194">Saving hello .bin file toohello device causes hello device toorestart and run hello program contained in hello .bin file.</span></span> <span data-ttu-id="11847-195">È possibile riavviare manualmente il programma hello in qualsiasi momento premendo il pulsante di reimpostazione hello sul dispositivo mbed hello.</span><span class="sxs-lookup"><span data-stu-id="11847-195">You can manually restart hello program at any time by pressing hello reset button on hello mbed device.</span></span>

1. <span data-ttu-id="11847-196">Connettere il dispositivo toohello usando un'applicazione client SSH, ad esempio PuTTY.</span><span class="sxs-lookup"><span data-stu-id="11847-196">Connect toohello device using an SSH client application, such as PuTTY.</span></span> <span data-ttu-id="11847-197">È possibile determinare il dispositivo utilizza controllando Gestione dispositivi di Windows della porta seriale hello.</span><span class="sxs-lookup"><span data-stu-id="11847-197">You can determine hello serial port your device uses by checking Windows Device Manager.</span></span>
   
    ![][11]

1. <span data-ttu-id="11847-198">In PuTTY, fare clic su hello **seriale** tipo di connessione.</span><span class="sxs-lookup"><span data-stu-id="11847-198">In PuTTY, click hello **Serial** connection type.</span></span> <span data-ttu-id="11847-199">in genere si connette il dispositivo Hello 9600 baud, quindi immettere 9600 hello **velocità** casella.</span><span class="sxs-lookup"><span data-stu-id="11847-199">hello device typically connects at 9600 baud, so enter 9600 in hello **Speed** box.</span></span> <span data-ttu-id="11847-200">Fare quindi clic su **Apri**.</span><span class="sxs-lookup"><span data-stu-id="11847-200">Then click **Open**.</span></span>

1. <span data-ttu-id="11847-201">programma Hello avvia l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="11847-201">hello program starts executing.</span></span> <span data-ttu-id="11847-202">È possibile che Lavagna hello tooreset (premere CTRL + INTERR o un pulsante di reimpostazione della Lavagna hello premere) se il programma di hello non viene avviato automaticamente quando ci si connette.</span><span class="sxs-lookup"><span data-stu-id="11847-202">You may have tooreset hello board (press CTRL+Break or press hello board's reset button) if hello program does not start automatically when you connect.</span></span>
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
