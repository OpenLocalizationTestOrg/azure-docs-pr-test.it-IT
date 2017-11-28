---
title: aaaSave l'hub IoT messaggi archiviazione dei dati tooAzure | Documenti Microsoft
description: Utilizzare un toosave app Azure funzione tooyour di messaggi l'hub IoT archiviazione tabelle di Azure. messaggi di hub IoT Hello contengono informazioni, ad esempio dati del sensore, che viene inviati dal dispositivo IoT.
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
ms.openlocfilehash: be72d9ba9a781822926364351b50f58f5d96e94a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a><span data-ttu-id="8dd66-105">Salvare i messaggi di hub IoT contenenti sensore dati tooyour archiviazione tabelle Azure</span><span class="sxs-lookup"><span data-stu-id="8dd66-105">Save IoT hub messages that contain sensor data tooyour Azure table storage</span></span>

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="8dd66-107">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="8dd66-107">What you learn</span></span>

<span data-ttu-id="8dd66-108">Viene illustrato come toocreate un account di archiviazione di Azure e un Azure funzione messaggi dell'hub IoT toostore app nell'archiviazione tabella.</span><span class="sxs-lookup"><span data-stu-id="8dd66-108">You learn how toocreate an Azure storage account and an Azure function app toostore IoT hub messages in your table storage.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="8dd66-109">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="8dd66-109">What you do</span></span>

- <span data-ttu-id="8dd66-110">Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="8dd66-110">Create an Azure storage account.</span></span>
- <span data-ttu-id="8dd66-111">Preparare l'hub IoT messaggi tooread di connessione.</span><span class="sxs-lookup"><span data-stu-id="8dd66-111">Prepare your IoT hub connection tooread messages.</span></span>
- <span data-ttu-id="8dd66-112">Creare e distribuire un'app per le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="8dd66-112">Create and deploy an Azure function app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8dd66-113">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="8dd66-113">What you need</span></span>

- <span data-ttu-id="8dd66-114">[Configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) hello toocover seguenti requisiti:</span><span class="sxs-lookup"><span data-stu-id="8dd66-114">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) toocover hello following requirements:</span></span>
  - <span data-ttu-id="8dd66-115">Una sottoscrizione di Azure attiva</span><span class="sxs-lookup"><span data-stu-id="8dd66-115">An active Azure subscription</span></span>
  - <span data-ttu-id="8dd66-116">Un hub IoT nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="8dd66-116">An IoT hub under your subscription</span></span> 
  - <span data-ttu-id="8dd66-117">Un'applicazione in esecuzione che invia l'hub IoT tooyour messaggi</span><span class="sxs-lookup"><span data-stu-id="8dd66-117">A running application that sends messages tooyour IoT hub</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="8dd66-118">Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="8dd66-118">Create an Azure storage account</span></span>

1. <span data-ttu-id="8dd66-119">In hello [portale di Azure](https://portal.azure.com/), fare clic su **New** > **archiviazione** > **account di archiviazione**  >   **Creare**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-119">In hello [Azure portal](https://portal.azure.com/), click **New** > **Storage** > **Storage account** > **Create**.</span></span>

2. <span data-ttu-id="8dd66-120">Immettere le informazioni necessarie per l'account di archiviazione hello hello:</span><span class="sxs-lookup"><span data-stu-id="8dd66-120">Enter hello necessary information for hello storage account:</span></span>

   ![Creare un account di archiviazione nel portale di Azure hello](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * <span data-ttu-id="8dd66-122">**Nome**: nome hello hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8dd66-122">**Name**: hello name of hello storage account.</span></span> <span data-ttu-id="8dd66-123">nome Hello deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="8dd66-123">hello name must be globally unique.</span></span>

   * <span data-ttu-id="8dd66-124">**Gruppo di risorse**: utilizzare hello stesso gruppo di risorse che usa l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8dd66-124">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="8dd66-125">**PIN toodashboard**: selezionare questa opzione per l'hub IoT tooyour di facile accesso dal dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="8dd66-125">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

3. <span data-ttu-id="8dd66-126">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-126">Click **Create**.</span></span>

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a><span data-ttu-id="8dd66-127">Preparare l'hub IoT messaggi tooread connessione</span><span class="sxs-lookup"><span data-stu-id="8dd66-127">Prepare your IoT hub connection tooread messages</span></span>

<span data-ttu-id="8dd66-128">Hub IoT espone un evento incorporato endpoint compatibile con hub tooenable applicazioni tooread IoT hub dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="8dd66-128">IoT hub exposes a built-in event hub-compatible endpoint tooenable applications tooread IoT hub messages.</span></span> <span data-ttu-id="8dd66-129">Nel frattempo, le applicazioni utilizzano dati tooread gruppi di consumer dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8dd66-129">Meanwhile, applications use consumer groups tooread data from your IoT hub.</span></span> <span data-ttu-id="8dd66-130">Prima di creare un dati tooread app di Azure (funzione) dall'hub IoT, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8dd66-130">Before you create an Azure function app tooread data from your IoT hub, do hello following:</span></span>

- <span data-ttu-id="8dd66-131">Ottenere la stringa di connessione hello dell'endpoint hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8dd66-131">Get hello connection string of your IoT hub endpoint.</span></span>
- <span data-ttu-id="8dd66-132">Creare un gruppo di consumer per l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8dd66-132">Create a consumer group for your IoT hub.</span></span>

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a><span data-ttu-id="8dd66-133">Ottiene la stringa di connessione hello dell'endpoint hub IoT</span><span class="sxs-lookup"><span data-stu-id="8dd66-133">Get hello connection string of your IoT hub endpoint</span></span>

1. <span data-ttu-id="8dd66-134">Aprire l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8dd66-134">Open your IoT hub.</span></span>

2. <span data-ttu-id="8dd66-135">In hello **IoT Hub** riquadro, in **messaggistica**, fare clic su **endpoint**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-135">On hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="8dd66-136">In hello destro in riquadro **gli endpoint predefiniti**, fare clic su **eventi**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-136">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="8dd66-137">In hello **proprietà** riquadro, hello nota seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="8dd66-137">In hello **Properties** pane, note hello following values:</span></span>
   - <span data-ttu-id="8dd66-138">Endpoint compatibile con l'hub eventi</span><span class="sxs-lookup"><span data-stu-id="8dd66-138">Event hub-compatible endpoint</span></span>
   - <span data-ttu-id="8dd66-139">Nome compatibile con l'hub eventi</span><span class="sxs-lookup"><span data-stu-id="8dd66-139">Event hub-compatible name</span></span>

   ![Ottenere la stringa di connessione hello dell'endpoint hub IoT in hello portale di Azure](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. <span data-ttu-id="8dd66-141">In hello **IoT Hub** riquadro, in **impostazioni**, fare clic su **criteri di accesso condiviso**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-141">In hello **IoT Hub** pane, under **Settings**, click **Shared access policies**.</span></span>

6. <span data-ttu-id="8dd66-142">Fare clic su **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-142">Click **iothubowner**.</span></span>

7. <span data-ttu-id="8dd66-143">Hello nota **chiave primaria** valore.</span><span class="sxs-lookup"><span data-stu-id="8dd66-143">Note hello **Primary key** value.</span></span>

8. <span data-ttu-id="8dd66-144">Creare la stringa di connessione hello dell'endpoint hub IoT come segue:</span><span class="sxs-lookup"><span data-stu-id="8dd66-144">Create hello connection string of your IoT hub endpoint as follows:</span></span>

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > <span data-ttu-id="8dd66-145">Sostituire `<Event Hub-compatible endpoint>` e `<Primary key>` con i valori hello annotati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8dd66-145">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with hello values that you noted earlier.</span></span>

### <a name="create-a-consumer-group-for-your-iot-hub"></a><span data-ttu-id="8dd66-146">Creare un gruppo di consumer per l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="8dd66-146">Create a consumer group for your IoT hub</span></span>

1. <span data-ttu-id="8dd66-147">Aprire l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8dd66-147">Open your IoT hub.</span></span>

2. <span data-ttu-id="8dd66-148">In hello **IoT Hub** riquadro, in **messaggistica**, fare clic su **endpoint**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-148">In hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="8dd66-149">In hello destro in riquadro **gli endpoint predefiniti**, fare clic su **eventi**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-149">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="8dd66-150">In hello **proprietà** riquadro, in **gruppi di Consumer**, immettere un nome e quindi prendere nota di esso.</span><span class="sxs-lookup"><span data-stu-id="8dd66-150">In hello **Properties** pane, under **Consumer groups**, enter a name, and then make a note of it.</span></span>

5. <span data-ttu-id="8dd66-151">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-151">Click **Save**.</span></span>

## <a name="create-and-deploy-an-azure-function-app"></a><span data-ttu-id="8dd66-152">Creare e distribuire un'app per le funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="8dd66-152">Create and deploy an Azure function app</span></span>

1. <span data-ttu-id="8dd66-153">In hello [portale di Azure](https://portal.azure.com/), fare clic su **New** > **calcolo** > **funzione App**  >   **Creare**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-153">In hello [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App** > **Create**.</span></span>

2. <span data-ttu-id="8dd66-154">Immettere le informazioni necessarie per app di funzione hello hello.</span><span class="sxs-lookup"><span data-stu-id="8dd66-154">Enter hello necessary information for hello function app.</span></span>

   ![Creare un'app di funzione in hello portale di Azure](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * <span data-ttu-id="8dd66-156">**Nome dell'app**: nome hello di hello funzione app.</span><span class="sxs-lookup"><span data-stu-id="8dd66-156">**App name**: hello name of hello function app.</span></span> <span data-ttu-id="8dd66-157">nome Hello deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="8dd66-157">hello name must be globally unique.</span></span>

   * <span data-ttu-id="8dd66-158">**Gruppo di risorse**: utilizzare hello stesso gruppo di risorse che usa l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8dd66-158">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="8dd66-159">**Account di archiviazione**: hello account di archiviazione creato.</span><span class="sxs-lookup"><span data-stu-id="8dd66-159">**Storage Account**: hello storage account that you created.</span></span>

   * <span data-ttu-id="8dd66-160">**PIN toodashboard**: selezionare questa opzione per accedere facilmente toohello funzione app dal dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="8dd66-160">**Pin toodashboard**: Check this option for easy access toohello function app from hello dashboard.</span></span>

3. <span data-ttu-id="8dd66-161">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-161">Click **Create**.</span></span>

4. <span data-ttu-id="8dd66-162">Dopo la funzione hello app è stata creata, aprirlo.</span><span class="sxs-lookup"><span data-stu-id="8dd66-162">After hello function app has been created, open it.</span></span>

5. <span data-ttu-id="8dd66-163">Nell'app di funzione hello, creare una nuova funzione eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8dd66-163">In hello function app, create a new function by doing hello following:</span></span>

   <span data-ttu-id="8dd66-164">a.</span><span class="sxs-lookup"><span data-stu-id="8dd66-164">a.</span></span> <span data-ttu-id="8dd66-165">Fare clic su **Nuova funzione**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-165">Click **New Function**.</span></span>

   <span data-ttu-id="8dd66-166">b.</span><span class="sxs-lookup"><span data-stu-id="8dd66-166">b.</span></span> <span data-ttu-id="8dd66-167">Selezionare **JavaScript** per **Linguaggio** ed **Elaborazione dati** per **Scenario**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-167">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span></span>

   <span data-ttu-id="8dd66-168">c.</span><span class="sxs-lookup"><span data-stu-id="8dd66-168">c.</span></span> <span data-ttu-id="8dd66-169">Fare clic su **Creare questa funzione** e quindi su **Nuova funzione**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-169">Click **Create this function**, and then click **New Function**.</span></span>

   <span data-ttu-id="8dd66-170">d.</span><span class="sxs-lookup"><span data-stu-id="8dd66-170">d.</span></span> <span data-ttu-id="8dd66-171">Selezionare **JavaScript** per Java hello e **l'elaborazione dati** per scenario hello.</span><span class="sxs-lookup"><span data-stu-id="8dd66-171">Select **JavaScript** for hello language, and **Data Processing** for hello scenario.</span></span>

   <span data-ttu-id="8dd66-172">e.</span><span class="sxs-lookup"><span data-stu-id="8dd66-172">e.</span></span> <span data-ttu-id="8dd66-173">Fare clic su hello **EventHubTrigger JavaScript** modello.</span><span class="sxs-lookup"><span data-stu-id="8dd66-173">Click hello **EventHubTrigger-JavaScript** template.</span></span>

   <span data-ttu-id="8dd66-174">f.</span><span class="sxs-lookup"><span data-stu-id="8dd66-174">f.</span></span> <span data-ttu-id="8dd66-175">Immettere le informazioni necessarie per il modello di hello hello.</span><span class="sxs-lookup"><span data-stu-id="8dd66-175">Enter hello necessary information for hello template.</span></span>

      * <span data-ttu-id="8dd66-176">**Nome funzione di**: nome hello della funzione hello.</span><span class="sxs-lookup"><span data-stu-id="8dd66-176">**Name your function**: hello name of hello function.</span></span>

      * <span data-ttu-id="8dd66-177">**Nome dell'Hub eventi**: nome compatibile con hub di eventi hello annotato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8dd66-177">**Event Hub name**: hello event hub-compatible name that you noted earlier.</span></span>

      * <span data-ttu-id="8dd66-178">**Connessione dell'Hub eventi**: stringa di connessione tooadd hello dell'endpoint hub IoT hello a cui è stato creato, fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-178">**Event Hub connection**: tooadd hello connection string of hello IoT hub endpoint that you created, click **New**.</span></span>

   <span data-ttu-id="8dd66-179">g.</span><span class="sxs-lookup"><span data-stu-id="8dd66-179">g.</span></span> <span data-ttu-id="8dd66-180">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-180">Click **Create**.</span></span>

6. <span data-ttu-id="8dd66-181">Configurare un output di hello funzione eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8dd66-181">Configure an output of hello function by doing hello following:</span></span>

   <span data-ttu-id="8dd66-182">a.</span><span class="sxs-lookup"><span data-stu-id="8dd66-182">a.</span></span> <span data-ttu-id="8dd66-183">Fare clic su **Integrazione** > **Nuovo output** > **Archiviazione tabelle di Azure** > **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-183">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

      ![Aggiungi tabella archiviazione tooyour funzione app nel portale di Azure hello](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   <span data-ttu-id="8dd66-185">b.</span><span class="sxs-lookup"><span data-stu-id="8dd66-185">b.</span></span> <span data-ttu-id="8dd66-186">Immettere le informazioni necessarie hello.</span><span class="sxs-lookup"><span data-stu-id="8dd66-186">Enter hello necessary information.</span></span>

      * <span data-ttu-id="8dd66-187">**Nome del parametro tabella**: utilizzare `outputTable`, che verrà utilizzata in hello Azure codice della funzione.</span><span class="sxs-lookup"><span data-stu-id="8dd66-187">**Table parameter name**: Use `outputTable`, which will be used in hello Azure function's code.</span></span>
      
      * <span data-ttu-id="8dd66-188">**Nome tabella**: usare `deviceData`.</span><span class="sxs-lookup"><span data-stu-id="8dd66-188">**Table name**: Use `deviceData`.</span></span>

      * <span data-ttu-id="8dd66-189">**Connessione dell'account di archiviazione**: fare clic su **nuovo** e selezionare o immettere l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8dd66-189">**Storage account connection**: Click **New**, and then select or enter your storage account.</span></span> <span data-ttu-id="8dd66-190">Se l'account di archiviazione hello non viene visualizzata, vedere [requisiti dell'account di archiviazione](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="8dd66-190">If hello storage account is not displayed, see [Storage account requirements](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span></span>
      
   <span data-ttu-id="8dd66-191">c.</span><span class="sxs-lookup"><span data-stu-id="8dd66-191">c.</span></span> <span data-ttu-id="8dd66-192">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-192">Click **Save**.</span></span>

7. <span data-ttu-id="8dd66-193">In **Trigger** fare clic su **Hub eventi di Azure (eventHubMessages)**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-193">Under **Triggers**, click **Azure Event Hub (eventHubMessages)**.</span></span>

8. <span data-ttu-id="8dd66-194">In **gruppo di consumer dell'Hub eventi**, immettere il nome di hello del gruppo di consumer hello è creato e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-194">Under **Event Hub consumer group**, enter hello name of hello consumer group that you created, and then click **Save**.</span></span>

9. <span data-ttu-id="8dd66-195">Fare clic su funzione hello creato in hello a sinistra e quindi fare clic su **Visualizza file** su hello destra.</span><span class="sxs-lookup"><span data-stu-id="8dd66-195">Click hello function you've created on hello left and then click **View Files** on hello right.</span></span>

10. <span data-ttu-id="8dd66-196">Sostituire il codice hello in `index.js` con seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="8dd66-196">Replace hello code in `index.js` with hello following:</span></span>

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in hello IoT hub.
   // hello message payload is persisted in an Azure storage table
 
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

11. <span data-ttu-id="8dd66-197">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-197">Click **Save**.</span></span>

<span data-ttu-id="8dd66-198">App di funzione hello è stata creata.</span><span class="sxs-lookup"><span data-stu-id="8dd66-198">You have now created hello function app.</span></span> <span data-ttu-id="8dd66-199">che archivia i messaggi ricevuti dall'hub IoT nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="8dd66-199">It stores messages that your IoT hub receives in your table storage.</span></span>

> [!NOTE]
> <span data-ttu-id="8dd66-200">È possibile utilizzare hello **eseguire** pulsante tootest hello funzione app.</span><span class="sxs-lookup"><span data-stu-id="8dd66-200">You can use hello **Run** button tootest hello function app.</span></span> <span data-ttu-id="8dd66-201">Quando fa clic su **eseguire**, il messaggio di prova hello viene inviato l'hub IoT tooyour.</span><span class="sxs-lookup"><span data-stu-id="8dd66-201">When you click **Run**, hello test message is sent tooyour IoT hub.</span></span> <span data-ttu-id="8dd66-202">all'arrivo di Hello del messaggio hello deve attivare hello funzione app toostart e quindi salvare archiviazione tabelle di tooyour messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="8dd66-202">hello arrival of hello message should trigger hello function app toostart and then save hello message tooyour table storage.</span></span> <span data-ttu-id="8dd66-203">Hello **registri** riquadro registra informazioni dettagliate di hello del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="8dd66-203">hello **Logs** pane records hello details of hello process.</span></span>

## <a name="verify-your-message-in-your-table-storage"></a><span data-ttu-id="8dd66-204">Verificare il messaggio nell'archivio tabelle</span><span class="sxs-lookup"><span data-stu-id="8dd66-204">Verify your message in your table storage</span></span>

1. <span data-ttu-id="8dd66-205">Eseguire l'applicazione di esempio hello in hub IoT tooyour di messaggi toosend di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8dd66-205">Run hello sample application on your device toosend messages tooyour IoT hub.</span></span>

2. <span data-ttu-id="8dd66-206">[Scaricare e installare Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="8dd66-206">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span></span>

3. <span data-ttu-id="8dd66-207">Aprire Esplora risorse di archiviazione, fare clic su **aggiungere un Account Azure** > **Accedi**, quindi accedi tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="8dd66-207">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in tooyour Azure account.</span></span>

4. <span data-ttu-id="8dd66-208">Fare clic sulla sottoscrizione di Azure > **Account di archiviazione** > account di archiviazione > **Tabelle** > **deviceData**.</span><span class="sxs-lookup"><span data-stu-id="8dd66-208">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span></span>

   <span data-ttu-id="8dd66-209">Si dovrebbero essere visualizzati i messaggi inviati dall'hub IoT di tooyour dispositivo connesso hello `deviceData` tabella.</span><span class="sxs-lookup"><span data-stu-id="8dd66-209">You should see messages sent from your device tooyour IoT hub logged in hello `deviceData` table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8dd66-210">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8dd66-210">Next steps</span></span>

<span data-ttu-id="8dd66-211">Sono stati creati l'account di archiviazione di Azure e l'app per le funzioni di Azure, che archivia i messaggi ricevuti dall'hub IoT nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="8dd66-211">You’ve successfully created your Azure storage account and Azure function app, which stores messages that your IoT hub receives in your table storage.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
