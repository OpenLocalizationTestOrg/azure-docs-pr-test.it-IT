---
title: Connettere un dispositivo tramite C in mbed | Documentazione Microsoft
description: "Descrive come connettere un dispositivo alla soluzione di monitoraggio remoto preconfigurata Azure IoT Suite con un’applicazione scritta in C in esecuzione in un dispositivo mbed."
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
ms.openlocfilehash: ef7b78f85a787f8fbe22c0e26aa34f0cd1685d58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-mbed"></a><span data-ttu-id="8a3f6-103">Connettere il dispositivo alla soluzione preconfigurata per il monitoraggio remoto (mbed)</span><span class="sxs-lookup"><span data-stu-id="8a3f6-103">Connect your device to the remote monitoring preconfigured solution (mbed)</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="8a3f6-104">Panoramica dello scenario</span><span class="sxs-lookup"><span data-stu-id="8a3f6-104">Scenario overview</span></span>
<span data-ttu-id="8a3f6-105">In questo scenario, viene creato un dispositivo che invia la seguente telemetria alla [soluzione preconfigurata][lnk-what-are-preconfig-solutions] per il monitoraggio remoto:</span><span class="sxs-lookup"><span data-stu-id="8a3f6-105">In this scenario, you create a device that sends the following telemetry to the remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="8a3f6-106">Temperatura esterna</span><span class="sxs-lookup"><span data-stu-id="8a3f6-106">External temperature</span></span>
* <span data-ttu-id="8a3f6-107">Temperatura interna</span><span class="sxs-lookup"><span data-stu-id="8a3f6-107">Internal temperature</span></span>
* <span data-ttu-id="8a3f6-108">Umidità</span><span class="sxs-lookup"><span data-stu-id="8a3f6-108">Humidity</span></span>

<span data-ttu-id="8a3f6-109">Per semplicità, il codice nel dispositivo genera valori di esempio, ma si consiglia di estendere l'esempio connettendo i sensori reali al dispositivo e inviando i dati di telemetria reali.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-109">For simplicity, the code on the device generates sample values, but we encourage you to extend the sample by connecting real sensors to your device and sending real telemetry.</span></span>

<span data-ttu-id="8a3f6-110">Inoltre, il dispositivo è in grado di rispondere ai metodi richiamati dal dashboard di soluzione e ai valori di proprietà desiderati impostati nel dashboard di soluzione.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-110">The device is also able to respond to methods invoked from the solution dashboard and desired property values set in the solution dashboard.</span></span>

<span data-ttu-id="8a3f6-111">Per completare l'esercitazione, è necessario un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-111">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="8a3f6-112">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8a3f6-113">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="8a3f6-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="8a3f6-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="8a3f6-114">Before you start</span></span>
<span data-ttu-id="8a3f6-115">Prima di scrivere un codice per il dispositivo, occorre eseguire la soluzione preconfigurata di monitoraggio remoto e poi effettuare il provisioning di un nuovo dispositivo personalizzato all'interno della soluzione in questione.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="8a3f6-116">Eseguire il provisioning della soluzione preconfigurata per il monitoraggio remoto</span><span class="sxs-lookup"><span data-stu-id="8a3f6-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="8a3f6-117">Il dispositivo creato in questa esercitazione invia dati a un'istanza della soluzione preconfigurata per il [monitoraggio remoto][lnk-remote-monitoring].</span><span class="sxs-lookup"><span data-stu-id="8a3f6-117">The device you create in this tutorial sends data to an instance of the [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="8a3f6-118">Se nel proprio account Azure non è già stato eseguito il provisioning della soluzione preconfigurata per il monitoraggio remoto, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8a3f6-118">If you haven't already provisioned the remote monitoring preconfigured solution in your Azure account, use the following steps:</span></span>

1. <span data-ttu-id="8a3f6-119">Nella pagina <https://www.azureiotsuite.com/> fare clic su **+** per creare una soluzione.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-119">On the <https://www.azureiotsuite.com/> page, click **+** to create a solution.</span></span>
2. <span data-ttu-id="8a3f6-120">Fare clic su **Seleziona** nel pannello **Remote monitoring** (Monitoraggio remoto) per creare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-120">Click **Select** on the **Remote monitoring** panel to create your solution.</span></span>
3. <span data-ttu-id="8a3f6-121">Nella pagina per la **creazione della soluzione di monitoraggio remoto** immettere il nome desiderato in **Nome soluzione** e selezionare l'**area** in cui eseguire la distribuzione e quindi la sottoscrizione di Azure da usare.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-121">On the **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select the **Region** you want to deploy to, and select the Azure subscription to want to use.</span></span> <span data-ttu-id="8a3f6-122">Fare clic su **Crea soluzione**.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="8a3f6-123">Attendere finché non viene completato il processo di provisioning.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-123">Wait until the provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="8a3f6-124">Le soluzioni preconfigurate usano servizi di Azure fatturabili.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-124">The preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="8a3f6-125">Al termine, assicurarsi di rimuovere la soluzione preconfigurata dalla sottoscrizione per evitare eventuali addebiti non necessari.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-125">Be sure to remove the preconfigured solution from your subscription when you are done with it to avoid any unnecessary charges.</span></span> <span data-ttu-id="8a3f6-126">Per rimuovere completamente una soluzione preconfigurata dalla sottoscrizione, visitare la pagina <https://www.azureiotsuite.com/>.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-126">You can completely remove a preconfigured solution from your subscription by visiting the <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="8a3f6-127">Al termine del processo di provisioning della soluzione di monitoraggio remoto, fare clic su **Avvia** per aprire il dashboard della soluzione nel browser.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-127">When the provisioning process for the remote monitoring solution finishes, click **Launch** to open the solution dashboard in your browser.</span></span>

![Dashboard della soluzione][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a><span data-ttu-id="8a3f6-129">Effettuare il provisioning del dispositivo nella soluzione di monitoraggio remoto</span><span class="sxs-lookup"><span data-stu-id="8a3f6-129">Provision your device in the remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="8a3f6-130">Se è già stato eseguito il provisioning di un dispositivo nella soluzione, è possibile saltare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="8a3f6-131">È necessario conoscere le credenziali del dispositivo quando si crea l'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-131">You need to know the device credentials when you create the client application.</span></span>
> 
> 

<span data-ttu-id="8a3f6-132">Per connettere un dispositivo alla soluzione preconfigurata, è necessario che identifichi se stesso nell'hub IoT mediante delle credenziali valide.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-132">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="8a3f6-133">È possibile recuperare le credenziali del dispositivo dal dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-133">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="8a3f6-134">Le istruzioni per includere le credenziali del dispositivo nell'applicazione client sono illustrate più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-134">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="8a3f6-135">Per aggiungere un dispositivo alla soluzione per il monitoraggio remoto, completare i passaggi seguenti nel dashboard della soluzione:</span><span class="sxs-lookup"><span data-stu-id="8a3f6-135">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="8a3f6-136">Nell'angolo inferiore sinistro del dashboard fare clic su **Aggiungi un dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-136">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>
   
   ![Aggiungere un dispositivo][1]
2. <span data-ttu-id="8a3f6-138">Nel pannello **Dispositivo personalizzato** fare clic su **Aggiungi nuovo**.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-138">In the **Custom Device** panel, click **Add new**.</span></span>
   
   ![Aggiungere un dispositivo personalizzato][2]
3. <span data-ttu-id="8a3f6-140">Scegliere **Let me define my own Device ID** (Desidero definire il mio ID dispositivo).</span><span class="sxs-lookup"><span data-stu-id="8a3f6-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="8a3f6-141">Immettere un ID dispositivo, ad esempio **mydevice**, fare clic su **Controlla ID** per verificare che tale nome non sia già in uso e quindi fare clic su **Crea** per effettuare il provisioning del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-141">Enter a Device ID such as **mydevice**, click **Check ID** to verify that name isn't already in use, and then click **Create** to provision the device.</span></span>
   
   ![Aggiungere un ID dispositivo][3]
4. <span data-ttu-id="8a3f6-143">Annotare le credenziali del dispositivo (ID dispositivo, nome host dell'hub IoT e chiave dispositivo).</span><span class="sxs-lookup"><span data-stu-id="8a3f6-143">Make a note the device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="8a3f6-144">Questi valori sono necessari per consentire all'applicazione client di connettersi alla soluzione per il monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-144">Your client application needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="8a3f6-145">Fare quindi clic su **Done**.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-145">Then click **Done**.</span></span>
   
    ![Vedere le credenziali del dispositivo][4]
5. <span data-ttu-id="8a3f6-147">Selezionare il dispositivo nell'elenco dei dispositivi nel dashboard della soluzione.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-147">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="8a3f6-148">Nel pannello **Dettagli dispositivo** fare clic su **Attiva dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-148">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="8a3f6-149">Lo stato del dispositivo è ora **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-149">The status of your device is now **Running**.</span></span> <span data-ttu-id="8a3f6-150">La soluzione per il monitoraggio remoto può ora ricevere i dati di telemetria dal dispositivo e richiamare i metodi sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-150">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-the-c-sample-solution"></a><span data-ttu-id="8a3f6-151">Compilare ed eseguire la soluzione di esempio C</span><span class="sxs-lookup"><span data-stu-id="8a3f6-151">Build and run the C sample solution</span></span>

<span data-ttu-id="8a3f6-152">Le istruzioni seguenti descrivono i passaggi per connettere un dispositivo [Freescale FRDM-K64F abilitato per mbed][lnk-mbed-home] alla soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-152">The following instructions describe the steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device to the remote monitoring solution.</span></span>

### <a name="connect-the-mbed-device-to-your-network-and-desktop-machine"></a><span data-ttu-id="8a3f6-153">Connettere il dispositivo mbed alla rete e al computer desktop</span><span class="sxs-lookup"><span data-stu-id="8a3f6-153">Connect the mbed device to your network and desktop machine</span></span>

1. <span data-ttu-id="8a3f6-154">Connettere il dispositivo mbed alla rete con un cavo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-154">Connect the mbed device to your network using an Ethernet cable.</span></span> <span data-ttu-id="8a3f6-155">Questo passaggio è necessario perché l'applicazione di esempio richiede l'accesso a Internet.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-155">This step is necessary because the sample application requires internet access.</span></span>

1. <span data-ttu-id="8a3f6-156">Vedere [Getting Started with mbed][lnk-mbed-getstarted] (Guida introduttiva a mbed) per connettere il dispositivo mbed al PC desktop.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-156">See [Getting Started with mbed][lnk-mbed-getstarted] to connect your mbed device to your desktop PC.</span></span>

1. <span data-ttu-id="8a3f6-157">Se il PC desktop esegue Windows, vedere [PC Configuration][lnk-mbed-pcconnect] (Configurazione PC) per configurare l'accesso alla porta seriale al dispositivo mbed.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-157">If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] to configure serial port access to your mbed device.</span></span>

### <a name="create-an-mbed-project-and-import-the-sample-code"></a><span data-ttu-id="8a3f6-158">Creare un progetto mbed e importare il codice di esempio</span><span class="sxs-lookup"><span data-stu-id="8a3f6-158">Create an mbed project and import the sample code</span></span>

<span data-ttu-id="8a3f6-159">Seguire questa procedura per aggiungere il codice di esempio al progetto mbed.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-159">Follow these steps to add some sample code to an mbed project.</span></span> <span data-ttu-id="8a3f6-160">Importare il progetto iniziale di monitoraggio remoto e quindi modificare il progetto affinché usi il protocollo MQTT anziché il protocollo AMQP.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-160">You import the remote monitoring starter project and then change the project to use the MQTT protocol instead of the AMQP protocol.</span></span> <span data-ttu-id="8a3f6-161">Attualmente, è necessario il protocollo MQTT per usare le funzionalità di gestione dei dispositivi di hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-161">Currently, you need to use the MQTT protocol to use the device management features of IoT Hub.</span></span>

1. <span data-ttu-id="8a3f6-162">Nel Web browser passare al [sito per sviluppatori](https://developer.mbed.org/)mbed.org.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-162">In your web browser, go to the mbed.org [developer site](https://developer.mbed.org/).</span></span> <span data-ttu-id="8a3f6-163">Se non si è iscritti, viene visualizzata un'opzione per creare un account (gratuito).</span><span class="sxs-lookup"><span data-stu-id="8a3f6-163">If you haven't signed up, you see an option to create an account (it's free).</span></span> <span data-ttu-id="8a3f6-164">In caso contrario, accedere con le credenziali dell'account.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-164">Otherwise, log in with your account credentials.</span></span> <span data-ttu-id="8a3f6-165">Fare quindi clic su **Compiler** nell'angolo superiore destro della pagina.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-165">Then click **Compiler** in the upper right-hand corner of the page.</span></span> <span data-ttu-id="8a3f6-166">Questa azione consente di visualizzare l'interfaccia *Workspace* (Area di lavoro).</span><span class="sxs-lookup"><span data-stu-id="8a3f6-166">This action brings you to the *Workspace* interface.</span></span>

1. <span data-ttu-id="8a3f6-167">Verificare che la piattaforma hardware usata venga visualizzata nell'angolo superiore destro della finestra oppure fare clic sull'icona nell'angolo destro per selezionare la piattaforma hardware.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-167">Make sure the hardware platform you're using appears in the upper right-hand corner of the window, or click the icon in the right-hand corner to select your hardware platform.</span></span>

1. <span data-ttu-id="8a3f6-168">Fare clic su **Import** nel menu principale.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-168">Click **Import** on the main menu.</span></span> <span data-ttu-id="8a3f6-169">Quindi fare clic su **Click here to import from URL** (Fare clic qui per eseguire l'importazione dall'URL).</span><span class="sxs-lookup"><span data-stu-id="8a3f6-169">Then click **Click here to import from URL**.</span></span>
   
    ![Avviare l'importazione nell'area di lavoro mbed][6]

1. <span data-ttu-id="8a3f6-171">Nella finestra popup immettere il collegamento per il codice di esempio https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ e quindi fare clic su **Import** (Importa).</span><span class="sxs-lookup"><span data-stu-id="8a3f6-171">In the pop-up window, enter the link for the sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.</span></span>
   
    ![Importare il codice di esempio all'area di lavoro mbed][7]

1. <span data-ttu-id="8a3f6-173">Nella finestra del compilatore mbed è possibile osservare che l'importazione del progetto include anche diverse librerie.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-173">You can see in the mbed compiler window that importing this project also imports various libraries.</span></span> <span data-ttu-id="8a3f6-174">Alcune vengono messe a disposizione e gestite dal team IoT di Azure ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), altre invece sono librerie di terze parti disponibili nel catalogo delle librerie di mbed.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-174">Some are provided and maintained by the Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in the mbed libraries catalog.</span></span>
   
    ![Visualizzare il progetto mbed][8]

1. <span data-ttu-id="8a3f6-176">Nell'**area di lavoro del programma**, fare clic con il pulsante destro del mouse sulla libreria **iothub\_amqp\_transport**, fare clic su **Elimina**, quindi su **OK** per confermare.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-176">In the **Program Workspace**, right-click the **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** to confirm.</span></span>

1. <span data-ttu-id="8a3f6-177">Nell'**area di lavoro del programma**, fare clic con il pulsante destro del mouse sulla libreria **azure\_amqp\_c**, fare clic su **Elimina**, quindi su **OK** per confermare.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-177">In the **Program Workspace**, right-click the **azure\_amqp\_c** library, click **Delete**, and then click **OK** to confirm.</span></span>

1. <span data-ttu-id="8a3f6-178">Fare clic con il pulsante destro del mouse sul progetto **remote_monitoring** nell'**area di lavoro del programma**, selezionare **Import Library** (Importa libreria), quindi **From URL** (Da URL).</span><span class="sxs-lookup"><span data-stu-id="8a3f6-178">Right-click the **remote_monitoring** project in the **Program Workspace**, select **Import Library**, then select **From URL**.</span></span>
   
    ![Avviare l'importazione della libreria nell'area di lavoro mbed][6]

1. <span data-ttu-id="8a3f6-180">Nella finestra popup immettere il collegamento per la libreria di trasporto MQTT https://developer.mbed.org/users/AzureIoTClient/code/iothub/\_mqtt\_transport/ e quindi fare clic su **Import** (Importa).</span><span class="sxs-lookup"><span data-stu-id="8a3f6-180">In the pop-up window, enter the link for the MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.</span></span>
   
    ![Importare la libreria nell'area di lavoro mbed][12]

1. <span data-ttu-id="8a3f6-182">Ripetere il passaggio precedente per aggiungere la libreria MQTT da https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-182">Repeat the previous step to add the MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span></span>

1. <span data-ttu-id="8a3f6-183">L'area di lavoro dovrebbe ora apparire così:</span><span class="sxs-lookup"><span data-stu-id="8a3f6-183">Your workspace now looks like the following:</span></span>

    ![Visualizzare l'area di lavoro mbed][13]

1. <span data-ttu-id="8a3f6-185">Aprire il file remote\_monitoring\remote_monitoring.c e sostituire le dichiarazioni `#include` esistenti con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="8a3f6-185">Open the remote\_monitoring\remote_monitoring.c file and replace the existing `#include` statements with the following code:</span></span>

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
1. <span data-ttu-id="8a3f6-186">Eliminare tutto il restante codice nel file remote\_monitoring\remote\_monitoring.c.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-186">Delete all the remaining code in the remote\_monitoring\remote\_monitoring.c file.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="8a3f6-187">Compilare ed eseguire l'esempio</span><span class="sxs-lookup"><span data-stu-id="8a3f6-187">Build and run the sample</span></span>

<span data-ttu-id="8a3f6-188">Aggiungere codice per richiamare la funzione **remote\_monitoring\_run** e quindi creare ed eseguire l'applicazione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-188">Add code to invoke the **remote\_monitoring\_run** function and then build and run the device application.</span></span>

1. <span data-ttu-id="8a3f6-189">Aggiungere una funzione **main** con il codice seguente alla fine del file remote\_monitoring.c per richiamare la funzione **remote\_monitoring\_run**:</span><span class="sxs-lookup"><span data-stu-id="8a3f6-189">Add a **main** function with following code at the end of the remote\_monitoring.c file to invoke the **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="8a3f6-190">Fare clic su **Compila** per compilare il programma.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-190">Click **Compile** to build the program.</span></span> <span data-ttu-id="8a3f6-191">È possibile ignorare eventuali avvisi, ma, se la compilazione genera errori, correggerli prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-191">You can safely ignore any warnings, but if the build generates errors, fix them before proceeding.</span></span>

1. <span data-ttu-id="8a3f6-192">Se la compilazione ha esito positivo, il sito Web del compilatore mbed genera un file .bin con il nome del progetto che viene scaricato nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-192">If the build is successful, the mbed compiler website generates a .bin file with the name of your project and downloads it to your local machine.</span></span> <span data-ttu-id="8a3f6-193">Copiare il file bin sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-193">Copy the .bin file to the device.</span></span> <span data-ttu-id="8a3f6-194">Il salvataggio del file .bin nel dispositivo causa il riavvio del dispositivo e l'esecuzione del programma contenuto nel file .bin.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-194">Saving the .bin file to the device causes the device to restart and run the program contained in the .bin file.</span></span> <span data-ttu-id="8a3f6-195">È possibile riavviare manualmente il programma in qualsiasi momento facendo clic sul pulsante reset sul dispositivo mbed.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-195">You can manually restart the program at any time by pressing the reset button on the mbed device.</span></span>

1. <span data-ttu-id="8a3f6-196">Connettersi al dispositivo con un'applicazione client SSH, ad esempio PuTTY.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-196">Connect to the device using an SSH client application, such as PuTTY.</span></span> <span data-ttu-id="8a3f6-197">È possibile determinare la porta seriale usata dal dispositivo controllando Gestione dispositivi di Windows.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-197">You can determine the serial port your device uses by checking Windows Device Manager.</span></span>
   
    ![][11]

1. <span data-ttu-id="8a3f6-198">In PuTTY fare clic sul tipo di connessione **Serial** .</span><span class="sxs-lookup"><span data-stu-id="8a3f6-198">In PuTTY, click the **Serial** connection type.</span></span> <span data-ttu-id="8a3f6-199">Poiché il dispositivo si connette in genere a 9600 baud, immettere 9600 nella casella **Velocità** .</span><span class="sxs-lookup"><span data-stu-id="8a3f6-199">The device typically connects at 9600 baud, so enter 9600 in the **Speed** box.</span></span> <span data-ttu-id="8a3f6-200">Fare quindi clic su **Apri**.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-200">Then click **Open**.</span></span>

1. <span data-ttu-id="8a3f6-201">Inizia l'esecuzione del programma.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-201">The program starts executing.</span></span> <span data-ttu-id="8a3f6-202">Potrebbe essere necessario reimpostare la scheda (premere CTRL+INTERR o premere il pulsante reset della scheda) se il programma non viene avviato automaticamente alla connessione.</span><span class="sxs-lookup"><span data-stu-id="8a3f6-202">You may have to reset the board (press CTRL+Break or press the board's reset button) if the program does not start automatically when you connect.</span></span>
   
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
