---
title: Salvare i messaggi dell'hub IoT nell'archivio dati di Azure | Microsoft Docs
description: Usare l'app per le funzioni di Azure per salvare i messaggi dell'hub IoT nell'archiviazione tabelle di Azure. I messaggi dell'hub IoT contengono informazioni, come i dati di sensori, inviate dal dispositivo IoT.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: archiviazione dei dati IoT, archiviazione dei dati di sensori IoT
ms.assetid: 62fd14fd-aaaa-4b3d-8367-75c1111b6269
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 06503f9564e00ef62587d02f2da4778974e246c5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-to-your-azure-table-storage"></a><span data-ttu-id="55d8c-105">Salvare i messaggi dell'hub IoT che contengono dati di sensori nell'archiviazione tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="55d8c-105">Save IoT hub messages that contain sensor data to your Azure table storage</span></span>

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="55d8c-107">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="55d8c-107">What you learn</span></span>

<span data-ttu-id="55d8c-108">Si apprenderà come creare un account di archiviazione di Azure e un'app per le funzioni di Azure per archiviare i messaggi dell'hub IoT nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="55d8c-108">You learn how to create an Azure storage account and an Azure function app to store IoT hub messages in your table storage.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="55d8c-109">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="55d8c-109">What you do</span></span>

- <span data-ttu-id="55d8c-110">Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="55d8c-110">Create an Azure storage account.</span></span>
- <span data-ttu-id="55d8c-111">Preparare la connessione dell'hub IoT per la lettura dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="55d8c-111">Prepare your IoT hub connection to read messages.</span></span>
- <span data-ttu-id="55d8c-112">Creare e distribuire un'app per le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="55d8c-112">Create and deploy an Azure function app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="55d8c-113">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="55d8c-113">What you need</span></span>

- <span data-ttu-id="55d8c-114">[Configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) in modo da soddisfare i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="55d8c-114">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) to cover the following requirements:</span></span>
  - <span data-ttu-id="55d8c-115">Una sottoscrizione di Azure attiva</span><span class="sxs-lookup"><span data-stu-id="55d8c-115">An active Azure subscription</span></span>
  - <span data-ttu-id="55d8c-116">Un hub IoT nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="55d8c-116">An IoT hub under your subscription</span></span> 
  - <span data-ttu-id="55d8c-117">Un'applicazione in esecuzione che invia messaggi all'hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="55d8c-117">A running application that sends messages to your IoT hub</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="55d8c-118">Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="55d8c-118">Create an Azure storage account</span></span>

1. <span data-ttu-id="55d8c-119">Nel [portale di Azure](https://portal.azure.com/) fare clic su **Nuova** > **Archiviazione** > **Account di archiviazione** > **Crea**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-119">In the [Azure portal](https://portal.azure.com/), click **New** > **Storage** > **Storage account** > **Create**.</span></span>

2. <span data-ttu-id="55d8c-120">Immettere le informazioni necessarie per l'account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="55d8c-120">Enter the necessary information for the storage account:</span></span>

   ![Creare un account di archiviazione nel portale di Azure](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * <span data-ttu-id="55d8c-122">**Nome**: nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="55d8c-122">**Name**: The name of the storage account.</span></span> <span data-ttu-id="55d8c-123">Il nome deve essere univoco a livello globale.</span><span class="sxs-lookup"><span data-stu-id="55d8c-123">The name must be globally unique.</span></span>

   * <span data-ttu-id="55d8c-124">**Gruppo di risorse**: usare lo stesso gruppo di risorse usato da hub IoT.</span><span class="sxs-lookup"><span data-stu-id="55d8c-124">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="55d8c-125">**Aggiungi al dashboard**: selezionare questa opzione per semplificare l'accesso all'hub IoT dal dashboard.</span><span class="sxs-lookup"><span data-stu-id="55d8c-125">**Pin to dashboard**: Select this option for easy access to your IoT hub from the dashboard.</span></span>

3. <span data-ttu-id="55d8c-126">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-126">Click **Create**.</span></span>

## <a name="prepare-your-iot-hub-connection-to-read-messages"></a><span data-ttu-id="55d8c-127">Preparare la connessione dell'hub IoT per la lettura dei messaggi</span><span class="sxs-lookup"><span data-stu-id="55d8c-127">Prepare your IoT hub connection to read messages</span></span>

<span data-ttu-id="55d8c-128">L'hub IoT espone un endpoint predefinito compatibile con l'hub eventi per consentire alle applicazioni di leggere i messaggi dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="55d8c-128">IoT hub exposes a built-in event hub-compatible endpoint to enable applications to read IoT hub messages.</span></span> <span data-ttu-id="55d8c-129">Nel frattempo, le applicazioni usano gruppi di consumer per leggere i dati dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="55d8c-129">Meanwhile, applications use consumer groups to read data from your IoT hub.</span></span> <span data-ttu-id="55d8c-130">Prima di creare un'app per le funzioni di Azure per la lettura dei dati dall'hub IoT, è necessario:</span><span class="sxs-lookup"><span data-stu-id="55d8c-130">Before you create an Azure function app to read data from your IoT hub, do the following:</span></span>

- <span data-ttu-id="55d8c-131">Ottenere la stringa di connessione dell'endpoint dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="55d8c-131">Get the connection string of your IoT hub endpoint.</span></span>
- <span data-ttu-id="55d8c-132">Creare un gruppo di consumer per l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="55d8c-132">Create a consumer group for your IoT hub.</span></span>

### <a name="get-the-connection-string-of-your-iot-hub-endpoint"></a><span data-ttu-id="55d8c-133">Ottenere la stringa di connessione dell'endpoint dell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="55d8c-133">Get the connection string of your IoT hub endpoint</span></span>

1. <span data-ttu-id="55d8c-134">Aprire l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="55d8c-134">Open your IoT hub.</span></span>

2. <span data-ttu-id="55d8c-135">Nel riquadro **Hub IoT**, in **Messaggistica**, fare clic su **Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-135">On the **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="55d8c-136">Nel riquadro destro, in **Endpoint predefiniti**, fare clic su **Eventi**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-136">In the right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="55d8c-137">Nel riquadro **Proprietà** prendere nota dei valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="55d8c-137">In the **Properties** pane, note the following values:</span></span>
   - <span data-ttu-id="55d8c-138">Endpoint compatibile con l'hub eventi</span><span class="sxs-lookup"><span data-stu-id="55d8c-138">Event hub-compatible endpoint</span></span>
   - <span data-ttu-id="55d8c-139">Nome compatibile con l'hub eventi</span><span class="sxs-lookup"><span data-stu-id="55d8c-139">Event hub-compatible name</span></span>

   ![Ottenere la stringa di connessione dell'endpoint dell'hub IoT nel portale di Azure](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. <span data-ttu-id="55d8c-141">Nel riquadro **Hub IoT**, in **Impostazioni**, fare clic su **Criteri di accesso condivisi**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-141">In the **IoT Hub** pane, under **Settings**, click **Shared access policies**.</span></span>

6. <span data-ttu-id="55d8c-142">Fare clic su **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-142">Click **iothubowner**.</span></span>

7. <span data-ttu-id="55d8c-143">Prendere nota del valore presente in **Chiave primaria**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-143">Note the **Primary key** value.</span></span>

8. <span data-ttu-id="55d8c-144">Creare la stringa di connessione dell'endpoint dell'hub IoT nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="55d8c-144">Create the connection string of your IoT hub endpoint as follows:</span></span>

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > <span data-ttu-id="55d8c-145">Sostituire `<Event Hub-compatible endpoint>` e `<Primary key>` con i valori annotati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="55d8c-145">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with the values that you noted earlier.</span></span>

### <a name="create-a-consumer-group-for-your-iot-hub"></a><span data-ttu-id="55d8c-146">Creare un gruppo di consumer per l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="55d8c-146">Create a consumer group for your IoT hub</span></span>

1. <span data-ttu-id="55d8c-147">Aprire l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="55d8c-147">Open your IoT hub.</span></span>

2. <span data-ttu-id="55d8c-148">Nel riquadro **Hub IoT**, in **Messaggistica**, fare clic su **Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-148">In the **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="55d8c-149">Nel riquadro destro, in **Endpoint predefiniti**, fare clic su **Eventi**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-149">In the right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="55d8c-150">Nel riquadro **Proprietà** immettere un nome in **Gruppi di consumer** e prendere nota del nome.</span><span class="sxs-lookup"><span data-stu-id="55d8c-150">In the **Properties** pane, under **Consumer groups**, enter a name, and then make a note of it.</span></span>

5. <span data-ttu-id="55d8c-151">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-151">Click **Save**.</span></span>

## <a name="create-and-deploy-an-azure-function-app"></a><span data-ttu-id="55d8c-152">Creare e distribuire un'app per le funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="55d8c-152">Create and deploy an Azure function app</span></span>

1. <span data-ttu-id="55d8c-153">Nel [portale di Azure](https://portal.azure.com/) fare clic su **Nuovo** > **Calcolo** > **App per le funzioni** > **Crea**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-153">In the [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App** > **Create**.</span></span>

2. <span data-ttu-id="55d8c-154">Immettere le informazioni necessarie per l'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="55d8c-154">Enter the necessary information for the function app.</span></span>

   ![Creare un'app per le funzioni nel portale di Azure](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * <span data-ttu-id="55d8c-156">**Nome app**: nome dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="55d8c-156">**App name**: The name of the function app.</span></span> <span data-ttu-id="55d8c-157">Il nome deve essere univoco a livello globale.</span><span class="sxs-lookup"><span data-stu-id="55d8c-157">The name must be globally unique.</span></span>

   * <span data-ttu-id="55d8c-158">**Gruppo di risorse**: usare lo stesso gruppo di risorse usato da hub IoT.</span><span class="sxs-lookup"><span data-stu-id="55d8c-158">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="55d8c-159">**Account di archiviazione**: selezionare l'account di archiviazione creato.</span><span class="sxs-lookup"><span data-stu-id="55d8c-159">**Storage Account**: The storage account that you created.</span></span>

   * <span data-ttu-id="55d8c-160">**Aggiungi al dashboard**: selezionare questa opzione per semplificare l'accesso all'app per le funzioni dal dashboard.</span><span class="sxs-lookup"><span data-stu-id="55d8c-160">**Pin to dashboard**: Check this option for easy access to the function app from the dashboard.</span></span>

3. <span data-ttu-id="55d8c-161">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-161">Click **Create**.</span></span>

4. <span data-ttu-id="55d8c-162">Dopo aver creato l'app per le funzioni, aprirla.</span><span class="sxs-lookup"><span data-stu-id="55d8c-162">After the function app has been created, open it.</span></span>

5. <span data-ttu-id="55d8c-163">Nell'app per le funzioni creare una nuova funzione seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="55d8c-163">In the function app, create a new function by doing the following:</span></span>

   <span data-ttu-id="55d8c-164">a.</span><span class="sxs-lookup"><span data-stu-id="55d8c-164">a.</span></span> <span data-ttu-id="55d8c-165">Fare clic su **Nuova funzione**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-165">Click **New Function**.</span></span>

   <span data-ttu-id="55d8c-166">b.</span><span class="sxs-lookup"><span data-stu-id="55d8c-166">b.</span></span> <span data-ttu-id="55d8c-167">Selezionare **JavaScript** per **Linguaggio** ed **Elaborazione dati** per **Scenario**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-167">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span></span>

   <span data-ttu-id="55d8c-168">c.</span><span class="sxs-lookup"><span data-stu-id="55d8c-168">c.</span></span> <span data-ttu-id="55d8c-169">Fare clic su **Creare questa funzione** e quindi su **Nuova funzione**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-169">Click **Create this function**, and then click **New Function**.</span></span>

   <span data-ttu-id="55d8c-170">d.</span><span class="sxs-lookup"><span data-stu-id="55d8c-170">d.</span></span> <span data-ttu-id="55d8c-171">Selezionare **JavaScript** per il linguaggio e **Elaborazione dati** per lo scenario.</span><span class="sxs-lookup"><span data-stu-id="55d8c-171">Select **JavaScript** for the language, and **Data Processing** for the scenario.</span></span>

   <span data-ttu-id="55d8c-172">e.</span><span class="sxs-lookup"><span data-stu-id="55d8c-172">e.</span></span> <span data-ttu-id="55d8c-173">Fare clic sul modello **EventHubTrigger-JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-173">Click the **EventHubTrigger-JavaScript** template.</span></span>

   <span data-ttu-id="55d8c-174">f.</span><span class="sxs-lookup"><span data-stu-id="55d8c-174">f.</span></span> <span data-ttu-id="55d8c-175">Immettere le informazioni necessarie per il modello.</span><span class="sxs-lookup"><span data-stu-id="55d8c-175">Enter the necessary information for the template.</span></span>

      * <span data-ttu-id="55d8c-176">**Assegnare un nome alla funzione**: nome della funzione.</span><span class="sxs-lookup"><span data-stu-id="55d8c-176">**Name your function**: The name of the function.</span></span>

      * <span data-ttu-id="55d8c-177">**Nome hub eventi**: nome compatibile con l'hub eventi annotato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="55d8c-177">**Event Hub name**: The event hub-compatible name that you noted earlier.</span></span>

      * <span data-ttu-id="55d8c-178">**Connessione dell'hub eventi**: fare clic su **Nuovo** per aggiungere la stringa di connessione dell'endpoint dell'hub IoT creata.</span><span class="sxs-lookup"><span data-stu-id="55d8c-178">**Event Hub connection**: To add the connection string of the IoT hub endpoint that you created, click **New**.</span></span>

   <span data-ttu-id="55d8c-179">g.</span><span class="sxs-lookup"><span data-stu-id="55d8c-179">g.</span></span> <span data-ttu-id="55d8c-180">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-180">Click **Create**.</span></span>

6. <span data-ttu-id="55d8c-181">Configurare un output della funzione seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="55d8c-181">Configure an output of the function by doing the following:</span></span>

   <span data-ttu-id="55d8c-182">a.</span><span class="sxs-lookup"><span data-stu-id="55d8c-182">a.</span></span> <span data-ttu-id="55d8c-183">Fare clic su **Integrazione** > **Nuovo output** > **Archiviazione tabelle di Azure** > **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-183">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

      ![Aggiungere l'archiviazione tabelle all'app per le funzioni nel portale di Azure](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   <span data-ttu-id="55d8c-185">b.</span><span class="sxs-lookup"><span data-stu-id="55d8c-185">b.</span></span> <span data-ttu-id="55d8c-186">Immettere le informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="55d8c-186">Enter the necessary information.</span></span>

      * <span data-ttu-id="55d8c-187">**Nome del parametro della tabella**: usare `outputTable`, che verrà usato nel codice di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="55d8c-187">**Table parameter name**: Use `outputTable`, which will be used in the Azure function's code.</span></span>
      
      * <span data-ttu-id="55d8c-188">**Nome tabella**: usare `deviceData`.</span><span class="sxs-lookup"><span data-stu-id="55d8c-188">**Table name**: Use `deviceData`.</span></span>

      * <span data-ttu-id="55d8c-189">**Connessione dell'account di archiviazione**: fare clic su **nuovo** e selezionare o immettere l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="55d8c-189">**Storage account connection**: Click **New**, and then select or enter your storage account.</span></span> <span data-ttu-id="55d8c-190">Se l'account di archiviazione non viene visualizzato, vedere [Requisiti dell'account di archiviazione](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="55d8c-190">If the storage account is not displayed, see [Storage account requirements](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span></span>
      
   <span data-ttu-id="55d8c-191">c.</span><span class="sxs-lookup"><span data-stu-id="55d8c-191">c.</span></span> <span data-ttu-id="55d8c-192">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-192">Click **Save**.</span></span>

7. <span data-ttu-id="55d8c-193">In **Trigger** fare clic su **Hub eventi di Azure (eventHubMessages)**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-193">Under **Triggers**, click **Azure Event Hub (eventHubMessages)**.</span></span>

8. <span data-ttu-id="55d8c-194">In **Gruppo di consumer dell'hub eventi** immettere il nome del gruppo di consumer creato, quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-194">Under **Event Hub consumer group**, enter the name of the consumer group that you created, and then click **Save**.</span></span>

9. <span data-ttu-id="55d8c-195">Fare clic sulla funzione creata a sinistra e quindi fare clic su **Visualizza file** a destra.</span><span class="sxs-lookup"><span data-stu-id="55d8c-195">Click the function you've created on the left and then click **View Files** on the right.</span></span>

10. <span data-ttu-id="55d8c-196">Sostituire il codice in `index.js` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="55d8c-196">Replace the code in `index.js` with the following:</span></span>

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in the IoT hub.
   // The message payload is persisted in an Azure storage table
 
   module.exports = function (context, iotHubMessage) {
    context.log('Message received: ' + JSON.stringify(iotHubMessage));
    var date = Date.now();
    var partitionKey = Math.floor(date / (24 * 60 * 60 * 1000)) + '';
    var rowKey = date + '';
    context.bindings.outputTable = {
     "partitionKey": partitionKey,
     "rowKey": rowKey,
     "message": JSON.stringify(iotHubMessage)
    };
    context.done();
   };
   ```

11. <span data-ttu-id="55d8c-197">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-197">Click **Save**.</span></span>

<span data-ttu-id="55d8c-198">È stata creata l'app per le funzioni,</span><span class="sxs-lookup"><span data-stu-id="55d8c-198">You have now created the function app.</span></span> <span data-ttu-id="55d8c-199">che archivia i messaggi ricevuti dall'hub IoT nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="55d8c-199">It stores messages that your IoT hub receives in your table storage.</span></span>

> [!NOTE]
> <span data-ttu-id="55d8c-200">È possibile usare il pulsante **Esegui** per testare l'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="55d8c-200">You can use the **Run** button to test the function app.</span></span> <span data-ttu-id="55d8c-201">Quando fa clic su **Esegui**, il messaggio di test viene inviato all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="55d8c-201">When you click **Run**, the test message is sent to your IoT hub.</span></span> <span data-ttu-id="55d8c-202">All'arrivo del messaggio, l'app per le funzioni si avvia e salva il messaggio nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="55d8c-202">The arrival of the message should trigger the function app to start and then save the message to your table storage.</span></span> <span data-ttu-id="55d8c-203">Il riquadro **Log** registra i dettagli del processo.</span><span class="sxs-lookup"><span data-stu-id="55d8c-203">The **Logs** pane records the details of the process.</span></span>

## <a name="verify-your-message-in-your-table-storage"></a><span data-ttu-id="55d8c-204">Verificare il messaggio nell'archivio tabelle</span><span class="sxs-lookup"><span data-stu-id="55d8c-204">Verify your message in your table storage</span></span>

1. <span data-ttu-id="55d8c-205">Eseguire l'applicazione di esempio nel dispositivo per inviare messaggi all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="55d8c-205">Run the sample application on your device to send messages to your IoT hub.</span></span>

2. <span data-ttu-id="55d8c-206">[Scaricare e installare Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="55d8c-206">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span></span>

3. <span data-ttu-id="55d8c-207">Aprire Storage Explorer, fare clic su **Add an Azure Account** (Aggiungi un account Azure)  >  **Accedi** e quindi accedere all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="55d8c-207">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in to your Azure account.</span></span>

4. <span data-ttu-id="55d8c-208">Fare clic sulla sottoscrizione di Azure > **Account di archiviazione** > account di archiviazione > **Tabelle** > **deviceData**.</span><span class="sxs-lookup"><span data-stu-id="55d8c-208">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span></span>

   <span data-ttu-id="55d8c-209">Nella tabella `deviceData` saranno visibili i messaggi inviati dal dispositivo all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="55d8c-209">You should see messages sent from your device to your IoT hub logged in the `deviceData` table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55d8c-210">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="55d8c-210">Next steps</span></span>

<span data-ttu-id="55d8c-211">Sono stati creati l'account di archiviazione di Azure e l'app per le funzioni di Azure, che archivia i messaggi ricevuti dall'hub IoT nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="55d8c-211">You’ve successfully created your Azure storage account and Azure function app, which stores messages that your IoT hub receives in your table storage.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
