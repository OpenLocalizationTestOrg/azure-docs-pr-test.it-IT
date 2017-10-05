---
title: "Visualizzazione in tempo reale dei dati del sensore dall'hub IoT di Azure – App Web | Microsoft Docs"
description: "Usare la funzionalità App Web di Azure del Servizio app di Microsoft Azure per visualizzare i dati su temperatura e umidità raccolti tramite il sensore e inviati all'hub IoT di Azure."
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
ms.openlocfilehash: e037f5c29cabf8e5d0d3e7ded187280a0652d5c3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-the-web-apps-feature-of-azure-app-service"></a><span data-ttu-id="0b845-104">Visualizzare i dati del sensore in tempo reale dall'hub IoT di Azure usando la funzionalità App Web del Servizio App di Azure</span><span class="sxs-lookup"><span data-stu-id="0b845-104">Visualize real-time sensor data from your Azure IoT hub by using the Web Apps feature of Azure App Service</span></span>

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="0b845-106">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="0b845-106">What you learn</span></span>

<span data-ttu-id="0b845-107">In questa esercitazione si imparerà a visualizzare i dati del sensore in tempo reale che l'hub IoT riceve eseguendo un'applicazione Web ospitata in un'app Web.</span><span class="sxs-lookup"><span data-stu-id="0b845-107">In this tutorial, you learn how to visualize real-time sensor data that your IoT hub receives by running a web application that is hosted on a web app.</span></span> <span data-ttu-id="0b845-108">Se si desidera provare a visualizzare i dati nell'hub IoT con Power BI, vedere [Usare Power BI per visualizzare i dati del sensore in tempo reale dall'hub IoT di Azure](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="0b845-108">If you want to try to visualize the data in your IoT hub by using Power BI, see [Use Power BI to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="0b845-109">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="0b845-109">What you do</span></span>

- <span data-ttu-id="0b845-110">Creare un'app Web nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b845-110">Create a web app in the Azure portal.</span></span>
- <span data-ttu-id="0b845-111">Preparare l'hub IoT per l'accesso dei dati mediante l'aggiunta di un gruppo di consumer.</span><span class="sxs-lookup"><span data-stu-id="0b845-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="0b845-112">Configurare l'app Web per leggere i dati del sensore dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0b845-112">Configure the web app to read sensor data from your IoT hub.</span></span>
- <span data-ttu-id="0b845-113">Caricare un'applicazione Web che deve essere ospitata dall'app Web.</span><span class="sxs-lookup"><span data-stu-id="0b845-113">Upload a web application to be hosted by the web app.</span></span>
- <span data-ttu-id="0b845-114">Aprire l'app Web per visualizzare i dati di temperatura e umidità in tempo reale dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0b845-114">Open the web app to see real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0b845-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="0b845-115">What you need</span></span>

- <span data-ttu-id="0b845-116">[Configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) che presenta i seguenti requisiti:</span><span class="sxs-lookup"><span data-stu-id="0b845-116">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md), which covers the following requirements:</span></span>
  - <span data-ttu-id="0b845-117">Una sottoscrizione di Azure attiva</span><span class="sxs-lookup"><span data-stu-id="0b845-117">An active Azure subscription</span></span>
  - <span data-ttu-id="0b845-118">Un hub IoT nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="0b845-118">An Iot hub under your subscription</span></span>
  - <span data-ttu-id="0b845-119">Un'applicazione client che invia messaggi all'hub IoT</span><span class="sxs-lookup"><span data-stu-id="0b845-119">A client application that sends messages to your Iot hub</span></span>
- [<span data-ttu-id="0b845-120">Scaricare Git</span><span class="sxs-lookup"><span data-stu-id="0b845-120">Download Git</span></span>](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a><span data-ttu-id="0b845-121">Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="0b845-121">Create a web app</span></span>

1. <span data-ttu-id="0b845-122">Nel [portale di Azure](https://ms.portal.azure.com/) fare clic su **Nuovo** > **Web e dispositivi mobili** > **App Web**.</span><span class="sxs-lookup"><span data-stu-id="0b845-122">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
2. <span data-ttu-id="0b845-123">Immettere un nome univoco del processo, verificare la sottoscrizione, specificare un gruppo di risorse e il percorso, selezionare **Aggiungi al dashboard**, quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0b845-123">Enter a unique job name, verify the subscription, specify a resource group and a location, select **Pin to dashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="0b845-124">È consigliabile selezionare la stessa posizione in cui si trova il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0b845-124">We recommend that you select the same location as that of your resource group.</span></span> <span data-ttu-id="0b845-125">In questo modo, si aumenta la velocità di elaborazione e si riducono i costi del trasferimento dati.</span><span class="sxs-lookup"><span data-stu-id="0b845-125">Doing so assists with processing speed and reduces the cost of data transfer.</span></span>

   ![Creare un'app Web](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-the-web-app-to-read-data-from-your-iot-hub"></a><span data-ttu-id="0b845-127">Configurare l'app Web per leggere i dati dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="0b845-127">Configure the web app to read data from your IoT hub</span></span>

1. <span data-ttu-id="0b845-128">Aprire l'app Web di cui è stato appena effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="0b845-128">Open the web app you’ve just provisioned.</span></span>
2. <span data-ttu-id="0b845-129">Fare clic su **Impostazioni applicazione**, quindi aggiungere le seguenti coppie chiave/valore in **Impostazioni app**:</span><span class="sxs-lookup"><span data-stu-id="0b845-129">Click **Application settings**, and then, under **App settings**, add the following key/value pairs:</span></span>

   | <span data-ttu-id="0b845-130">Chiave</span><span class="sxs-lookup"><span data-stu-id="0b845-130">Key</span></span>                                   | <span data-ttu-id="0b845-131">Valore</span><span class="sxs-lookup"><span data-stu-id="0b845-131">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="0b845-132">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="0b845-132">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="0b845-133">Ottenuto da iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="0b845-133">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="0b845-134">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="0b845-134">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="0b845-135">Il nome del gruppo di consumer che si aggiunge all'hub IoT</span><span class="sxs-lookup"><span data-stu-id="0b845-135">The name of the consumer group that you add to your IoT hub</span></span>  |

   ![Aggiungere impostazioni all'app Web di Azure con coppie chiave/valore](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. <span data-ttu-id="0b845-137">Fare clic su **Impostazioni applicazione**, in **Impostazioni generali**, attivare/disattivare l'opzione **Web Socket**, quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0b845-137">Click **Application settings**, under **General settings**, toggle the **Web sockets** option, and then click **Save**.</span></span>

   ![Attivare/disattivare l'opzione Web Socket](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-to-be-hosted-by-the-web-app"></a><span data-ttu-id="0b845-139">Caricare un'applicazione Web che deve essere ospitata dall'app Web</span><span class="sxs-lookup"><span data-stu-id="0b845-139">Upload a web application to be hosted by the web app</span></span>

<span data-ttu-id="0b845-140">Su GitHub è disponibile un'applicazione Web che consente di visualizzare i dati del sensore in tempo reale dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0b845-140">On GitHub, we've made available a web application that displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="0b845-141">È sufficiente configurare l'app Web che dovrà usare un repository Git, scaricare l'applicazione Web da GitHub e caricarla in Azure affinché l'applicazione Web possa ospitarla.</span><span class="sxs-lookup"><span data-stu-id="0b845-141">All you need to do is configure the web app to work with a Git repository, download the web application from GitHub, and then upload it to Azure for the web app to host.</span></span>

1. <span data-ttu-id="0b845-142">Nell'app Web fare clic su **Opzioni di distribuzione** > **Scegli origine** > **Repository Git locale**, quindi scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="0b845-142">In the web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**, and then click **OK**.</span></span>

   ![Configurare la distribuzione dell'app Web per l'uso del repository Git](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. <span data-ttu-id="0b845-144">Fare clic su **Credenziali per la distribuzione**, creare un nome utente e una password da usare per connettersi al repository Git in Azure, quindi scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0b845-144">Click **Deployment Credentials**, create a user name and password to use to connect to the Git repository in Azure, and then click **Save**.</span></span>

3. <span data-ttu-id="0b845-145">Fare clic su **Panoramica** e prendere nota del valore di **URL clone GIT**.</span><span class="sxs-lookup"><span data-stu-id="0b845-145">Click **Overview**, and note the value of **Git clone url**.</span></span>

   ![Ottenere l'URL clone Git dell'app Web](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. <span data-ttu-id="0b845-147">Aprire una finestra del comando o del terminale nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="0b845-147">Open a command or terminal window on your local computer.</span></span>

5. <span data-ttu-id="0b845-148">Scaricare l'app Web da GitHub e caricarla in Azure affinché ospiti l'app Web.</span><span class="sxs-lookup"><span data-stu-id="0b845-148">Download the web app from GitHub, and upload it to Azure for the web app to host.</span></span> <span data-ttu-id="0b845-149">A tale scopo, eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0b845-149">To do so, run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > <span data-ttu-id="0b845-150">\<URL clone GIT\> è l'URL del repository Git che si trova nella pagina **Panoramica** dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="0b845-150">\<Git clone URL\> is the URL of the Git repository found on the **Overview** page of the web app.</span></span>

## <a name="open-the-web-app-to-see-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="0b845-151">Aprire l'app Web per visualizzare i dati di temperatura e umidità in tempo reale dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="0b845-151">Open the web app to see real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="0b845-152">Nella pagina **Panoramica** dell'app Web fare clic sull'URL per aprire l'app Web.</span><span class="sxs-lookup"><span data-stu-id="0b845-152">On the **Overview** page of your web app, click the URL to open the web app.</span></span>

![Ottenere l'URL dell'app Web](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="0b845-154">Vengono visualizzati i dati di temperatura e umidità in tempo reale dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0b845-154">You should see the real-time temperature and humidity data from your IoT hub.</span></span>

![Pagina dell'app Web che mostra temperatura e umidità in tempo reale](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> <span data-ttu-id="0b845-156">Verificare che l'applicazione di esempio sia in esecuzione nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b845-156">Ensure the sample application is running on your device.</span></span> <span data-ttu-id="0b845-157">Se non lo fosse, si otterrà un grafico vuoto, ed è possibile fare riferimento alle esercitazioni descritte in [Configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0b845-157">If not, you will get a blank chart, you can refer to the tutorials under [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b845-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0b845-158">Next steps</span></span>
<span data-ttu-id="0b845-159">L'app Web è stata usata correttamente per visualizzare i dati del sensore in tempo reale dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0b845-159">You've successfully used your web app to visualize real-time sensor data from your IoT hub.</span></span>

<span data-ttu-id="0b845-160">Per un modo alternativo di visualizzare i dati dall'hub IoT di Azure, vedere [Usare Power BI per visualizzare i dati del sensore in tempo reale dall'hub IoT](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="0b845-160">For an alternative way to visualize data from Azure IoT Hub, see [Use Power BI to visualize real-time sensor data from your IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
