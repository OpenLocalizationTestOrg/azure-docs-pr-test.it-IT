---
title: 'visualizzazione dei dati di sensore dall''hub IoT di Azure: Web App aaaReal ora | Documenti Microsoft'
description: "Utilizzare funzionalità di hello App Web di Microsoft Azure App Service toovisualize temperatura e umidità dati raccolti dal sensore hello e inviati tooyour Iot hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: visualizzazione dei dati in tempo reale, visualizzazione dei dati dal vivo, visualizzazione dei dati del sensore
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a><span data-ttu-id="f4509-104">Visualizzare i dati in tempo reale sensore l'hub IoT di Azure utilizzando hello App Web di servizio App di Azure</span><span class="sxs-lookup"><span data-stu-id="f4509-104">Visualize real-time sensor data from your Azure IoT hub by using hello Web Apps feature of Azure App Service</span></span>

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="f4509-106">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="f4509-106">What you learn</span></span>

<span data-ttu-id="f4509-107">In questa esercitazione viene illustrato come dati del sensore in tempo reale toovisualize che riceve l'hub IoT mediante l'esecuzione di un'applicazione web che sono ospitati in un'app web.</span><span class="sxs-lookup"><span data-stu-id="f4509-107">In this tutorial, you learn how toovisualize real-time sensor data that your IoT hub receives by running a web application that is hosted on a web app.</span></span> <span data-ttu-id="f4509-108">Se si desiderano dati di hello toovisualize tootry nell'hub IoT con Power BI, vedere [dati di un sensore in tempo reale toovisualize Usa Power BI dall'IoT Hub Azure](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="f4509-108">If you want tootry toovisualize hello data in your IoT hub by using Power BI, see [Use Power BI toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="f4509-109">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="f4509-109">What you do</span></span>

- <span data-ttu-id="f4509-110">Creare un'app web nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f4509-110">Create a web app in hello Azure portal.</span></span>
- <span data-ttu-id="f4509-111">Preparare l'hub IoT per l'accesso dei dati mediante l'aggiunta di un gruppo di consumer.</span><span class="sxs-lookup"><span data-stu-id="f4509-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="f4509-112">Configurare hello tooread sensore dati dell'app web dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f4509-112">Configure hello web app tooread sensor data from your IoT hub.</span></span>
- <span data-ttu-id="f4509-113">Caricare un toobe di applicazione web ospitata da app web hello.</span><span class="sxs-lookup"><span data-stu-id="f4509-113">Upload a web application toobe hosted by hello web app.</span></span>
- <span data-ttu-id="f4509-114">Aprire hello toosee in tempo reale temperatura e umidità dati dell'app web dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f4509-114">Open hello web app toosee real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f4509-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="f4509-115">What you need</span></span>

- <span data-ttu-id="f4509-116">[Configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md), in cui rientra hello seguenti requisiti:</span><span class="sxs-lookup"><span data-stu-id="f4509-116">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md), which covers hello following requirements:</span></span>
  - <span data-ttu-id="f4509-117">Una sottoscrizione di Azure attiva</span><span class="sxs-lookup"><span data-stu-id="f4509-117">An active Azure subscription</span></span>
  - <span data-ttu-id="f4509-118">Un hub IoT nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="f4509-118">An Iot hub under your subscription</span></span>
  - <span data-ttu-id="f4509-119">Un'applicazione client che invia l'hub Iot tooyour messaggi</span><span class="sxs-lookup"><span data-stu-id="f4509-119">A client application that sends messages tooyour Iot hub</span></span>
- [<span data-ttu-id="f4509-120">Scaricare Git</span><span class="sxs-lookup"><span data-stu-id="f4509-120">Download Git</span></span>](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a><span data-ttu-id="f4509-121">Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="f4509-121">Create a web app</span></span>

1. <span data-ttu-id="f4509-122">In hello [portale di Azure](https://ms.portal.azure.com/), fare clic su **New** > **Web e dispositivi mobili** > **App Web**.</span><span class="sxs-lookup"><span data-stu-id="f4509-122">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
2. <span data-ttu-id="f4509-123">Immettere un nome univoco di processo, verificare la sottoscrizione hello, specificare un gruppo di risorse e il percorso, seleziona **Pin toodashboard**, quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="f4509-123">Enter a unique job name, verify hello subscription, specify a resource group and a location, select **Pin toodashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="f4509-124">È consigliabile selezionare hello stesso percorso del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f4509-124">We recommend that you select hello same location as that of your resource group.</span></span> <span data-ttu-id="f4509-125">In questo modo è di aiuto con velocità di elaborazione e consente di ridurre il costo di hello di trasferimento dei dati.</span><span class="sxs-lookup"><span data-stu-id="f4509-125">Doing so assists with processing speed and reduces hello cost of data transfer.</span></span>

   ![Creare un'app Web](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a><span data-ttu-id="f4509-127">Configurare hello web tooread i dati delle app per l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="f4509-127">Configure hello web app tooread data from your IoT hub</span></span>

1. <span data-ttu-id="f4509-128">Aprire l'app web hello che appena effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="f4509-128">Open hello web app you’ve just provisioned.</span></span>
2. <span data-ttu-id="f4509-129">Fare clic su **le impostazioni dell'applicazione**e quindi in **impostazioni App**, aggiungere hello coppie chiave/valore seguenti:</span><span class="sxs-lookup"><span data-stu-id="f4509-129">Click **Application settings**, and then, under **App settings**, add hello following key/value pairs:</span></span>

   | <span data-ttu-id="f4509-130">Chiave</span><span class="sxs-lookup"><span data-stu-id="f4509-130">Key</span></span>                                   | <span data-ttu-id="f4509-131">Valore</span><span class="sxs-lookup"><span data-stu-id="f4509-131">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="f4509-132">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="f4509-132">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="f4509-133">Ottenuto da iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="f4509-133">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="f4509-134">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="f4509-134">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="f4509-135">nome Hello del gruppo di consumer hello aggiungere tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="f4509-135">hello name of hello consumer group that you add tooyour IoT hub</span></span>  |

   ![Aggiungere impostazioni tooyour web app con coppie chiave/valore](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. <span data-ttu-id="f4509-137">Fare clic su **le impostazioni dell'applicazione**in **impostazioni generali**, hello attiva/disattiva **Web socket** opzione e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="f4509-137">Click **Application settings**, under **General settings**, toggle hello **Web sockets** option, and then click **Save**.</span></span>

   ![Attiva o disattiva hello Web socket](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a><span data-ttu-id="f4509-139">Caricare un toobe di applicazione web ospitata da app web hello</span><span class="sxs-lookup"><span data-stu-id="f4509-139">Upload a web application toobe hosted by hello web app</span></span>

<span data-ttu-id="f4509-140">Su GitHub è disponibile un'applicazione Web che consente di visualizzare i dati del sensore in tempo reale dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f4509-140">On GitHub, we've made available a web application that displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="f4509-141">È sufficiente toodo configurare hello web app toowork con un repository Git, scaricare l'applicazione web hello da GitHub e quindi caricarla tooAzure per hello web app toohost.</span><span class="sxs-lookup"><span data-stu-id="f4509-141">All you need toodo is configure hello web app toowork with a Git repository, download hello web application from GitHub, and then upload it tooAzure for hello web app toohost.</span></span>

1. <span data-ttu-id="f4509-142">Nell'app web hello, fare clic su **opzioni di distribuzione** > **Scegli origine** > **Git Repository locale**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="f4509-142">In hello web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**, and then click **OK**.</span></span>

   ![Configurare il web app distribuzione toouse hello repository Git locale](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. <span data-ttu-id="f4509-144">Fare clic su **le credenziali di distribuzione**, creare un utente nome e la password toouse tooconnect toohello repository Git in Azure e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="f4509-144">Click **Deployment Credentials**, create a user name and password toouse tooconnect toohello Git repository in Azure, and then click **Save**.</span></span>

3. <span data-ttu-id="f4509-145">Fare clic su **Panoramica**e prendere nota del valore di hello **url clone Git**.</span><span class="sxs-lookup"><span data-stu-id="f4509-145">Click **Overview**, and note hello value of **Git clone url**.</span></span>

   ![Ottenere l'URL del clone Git hello dell'app web](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. <span data-ttu-id="f4509-147">Aprire una finestra del comando o del terminale nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="f4509-147">Open a command or terminal window on your local computer.</span></span>

5. <span data-ttu-id="f4509-148">Scaricare l'app web hello da GitHub e caricarlo tooAzure per hello web app toohost.</span><span class="sxs-lookup"><span data-stu-id="f4509-148">Download hello web app from GitHub, and upload it tooAzure for hello web app toohost.</span></span> <span data-ttu-id="f4509-149">toodo in tal caso, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="f4509-149">toodo so, run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > <span data-ttu-id="f4509-150">\<URL clone GIT\> hello URL del repository Git hello trovato in hello **Panoramica** pagina dell'app web hello.</span><span class="sxs-lookup"><span data-stu-id="f4509-150">\<Git clone URL\> is hello URL of hello Git repository found on hello **Overview** page of hello web app.</span></span>

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="f4509-151">Aprire hello toosee in tempo reale temperatura e umidità dati dell'app web dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="f4509-151">Open hello web app toosee real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="f4509-152">In hello **Panoramica** pagina dell'app web, fare clic su hello URL tooopen hello web app.</span><span class="sxs-lookup"><span data-stu-id="f4509-152">On hello **Overview** page of your web app, click hello URL tooopen hello web app.</span></span>

![Ottenere hello URL dell'app web](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="f4509-154">Si noterà temperatura in tempo reale hello e dati umidità dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f4509-154">You should see hello real-time temperature and humidity data from your IoT hub.</span></span>

![Pagina dell'app Web che mostra temperatura e umidità in tempo reale](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> <span data-ttu-id="f4509-156">Verificare che l'applicazione di esempio hello è in esecuzione sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f4509-156">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="f4509-157">Se non si otterrà un grafico vuoto, è possibile fare riferimento a esercitazioni toohello in [configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f4509-157">If not, you will get a blank chart, you can refer toohello tutorials under [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4509-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f4509-158">Next steps</span></span>
<span data-ttu-id="f4509-159">Utilizzati correttamente i dati in tempo reale sensore toovisualize dell'app web dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f4509-159">You've successfully used your web app toovisualize real-time sensor data from your IoT hub.</span></span>

<span data-ttu-id="f4509-160">Per i dati di toovisualize un modo alternativo provenienti dall'IoT Hub di Azure, vedere [dati di un sensore in tempo reale toovisualize Usa Power BI dall'hub IoT](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="f4509-160">For an alternative way toovisualize data from Azure IoT Hub, see [Use Power BI toovisualize real-time sensor data from your IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
