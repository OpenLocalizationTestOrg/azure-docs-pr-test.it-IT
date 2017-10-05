---
title: Monitoraggio remoto e notifiche di IoT con App per la logica di Azure | Microsoft Docs
description: Usare le app per la logica di Azure per il monitoraggio della temperatura IoT sull'hub IoT e inviare automaticamente notifiche tramite e-mail alla cassetta postale per eventuali anomalie rilevate.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Monitoraggio IoT, notifiche IoT, monitoraggio della temperatura IoT
ms.assetid: 43043067-2e1f-42c9-953d-e2dce8fd86df
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 7a611912ae55eb22103539dbba9f1a06aaa543b7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a><span data-ttu-id="c9cb1-104">Monitoraggio remoto e notifiche di IoT con App per la logica di Azure tramite la connessione all'hub IoT e alla cassetta postale</span><span class="sxs-lookup"><span data-stu-id="c9cb1-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span></span>

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="c9cb1-106">App per la logica di Azure offre un modo per automatizzare i processi come una serie di passaggi.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-106">Azure Logic Apps provides a way to automate processes as a series of steps.</span></span> <span data-ttu-id="c9cb1-107">Un'app per la logica può connettersi tramite diversi servizi e protocolli.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-107">A logic app can connect across various services and protocols.</span></span> <span data-ttu-id="c9cb1-108">Inizia con un trigger, ad esempio "When an account is added" (Quando si aggiunge un account), seguito da una combinazione di azioni, come "sending a push notification" (invio di una notifica push).</span><span class="sxs-lookup"><span data-stu-id="c9cb1-108">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span></span> <span data-ttu-id="c9cb1-109">Questa caratteristica rende App per la logica una soluzione IoT perfetta per il monitoraggio IoT, ad esempio per stare in allerta in caso di anomalie, tra altri scenari di uso.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-109">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="c9cb1-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="c9cb1-110">What you learn</span></span>

<span data-ttu-id="c9cb1-111">Informazioni su come creare un'app per la logica che connette l'hub IoT e la cassetta postale per il monitoraggio della temperatura e le notifiche.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-111">You learn how to create a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span> <span data-ttu-id="c9cb1-112">Quando la temperatura è superiore a 30°C, l'applicazione client contrassegna `temperatureAlert = "true"` nel messaggio inviato all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-112">When the temperature is above 30 C, the client application marks `temperatureAlert = "true"` in the message it sends to your IoT hub.</span></span> <span data-ttu-id="c9cb1-113">Il messaggio attiva l'app per la logica per l'invio di notifiche di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-113">The message triggers the logic app to send you an email notification.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="c9cb1-114">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="c9cb1-114">What you do</span></span>

* <span data-ttu-id="c9cb1-115">Creare uno spazio dei nomi del bus di servizio e aggiungere una coda.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-115">Create a service bus namespace and add a queue to it.</span></span>
* <span data-ttu-id="c9cb1-116">Aggiungere un endpoint e una regola di routing all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-116">Add an endpoint and a routing rule to your IoT hub.</span></span>
* <span data-ttu-id="c9cb1-117">Creare, configurare e testare un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-117">Create, configure, and test a logic app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c9cb1-118">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="c9cb1-118">What you need</span></span>

* <span data-ttu-id="c9cb1-119">Completare l'esercitazione [Configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) che prevede i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c9cb1-119">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  * <span data-ttu-id="c9cb1-120">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-120">An active Azure subscription.</span></span>
  * <span data-ttu-id="c9cb1-121">Un hub IoT di Azure nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-121">An Azure IoT hub under your subscription.</span></span>
  * <span data-ttu-id="c9cb1-122">Un'applicazione client che invia messaggi ad Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-122">A client application that sends messages to your Azure IoT hub.</span></span>

## <a name="create-service-bus-namespace-and-add-a-queue-to-it"></a><span data-ttu-id="c9cb1-123">Creare uno spazio dei nomi del bus di servizio e aggiungere una coda</span><span class="sxs-lookup"><span data-stu-id="c9cb1-123">Create service bus namespace and add a queue to it</span></span>

### <a name="create-a-service-bus-namespace"></a><span data-ttu-id="c9cb1-124">Creare uno spazio dei nomi del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="c9cb1-124">Create a service bus namespace</span></span>

1. <span data-ttu-id="c9cb1-125">Nel [portale di Azure](https://portal.azure.com/), fare clic su **Nuovo** > **Integrazione aziendale** > **Bus di servizio**.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-125">On the [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Service Bus**.</span></span>
1. <span data-ttu-id="c9cb1-126">Specificare le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c9cb1-126">Provide the following information:</span></span>

   <span data-ttu-id="c9cb1-127">**Nome**: il nome del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-127">**Name**: The name of the service bus.</span></span>

   <span data-ttu-id="c9cb1-128">**Piano tariffario**: fare clic su **Base** > **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-128">**Pricing tier**: Click **Basic** > **Select**.</span></span> <span data-ttu-id="c9cb1-129">Il livello Base è sufficiente per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-129">The Basic tier is sufficient for this tutorial.</span></span>

   <span data-ttu-id="c9cb1-130">**Gruppo di risorse**: usare lo stesso gruppo di risorse usato da hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-130">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="c9cb1-131">**Posizione**: usare la stessa posizione che usa l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-131">**Location**: Use the same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="c9cb1-132">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-132">Click **Create**.</span></span>

   ![Creare uno spazio dei nomi del bus di servizio nel portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a><span data-ttu-id="c9cb1-134">Aggiungere una coda del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="c9cb1-134">Add a service bus queue</span></span>

1. <span data-ttu-id="c9cb1-135">Aprire lo spazio dei nomi del bus di servizio e quindi fare clic su **+ Queue** (+ coda).</span><span class="sxs-lookup"><span data-stu-id="c9cb1-135">Open the service bus namespace, and then click **+ Queue**.</span></span>
1. <span data-ttu-id="c9cb1-136">Immettere un nome per la coda e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-136">Enter a name for the queue and then click **Create**.</span></span>
1. <span data-ttu-id="c9cb1-137">Aprire la coda del bus di servizio e fare clic su **Criteri di accesso condiviso** > **+ Add** (+ Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="c9cb1-137">Open the service bus queue, and then click **Shared access policies** > **+ Add**.</span></span>
1. <span data-ttu-id="c9cb1-138">Inserire un nome al criterio e selezionare **Gestisci** e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-138">Enter a name for the policy, check **Manage**, and then click **Create**.</span></span>

   ![Aggiungere una coda del bus di servizio nel portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-to-your-iot-hub"></a><span data-ttu-id="c9cb1-140">Aggiungere un endpoint e una regola di routing all'hub IoT</span><span class="sxs-lookup"><span data-stu-id="c9cb1-140">Add an endpoint and a routing rule to your IoT hub</span></span>

### <a name="add-an-endpoint"></a><span data-ttu-id="c9cb1-141">Aggiungere un endpoint</span><span class="sxs-lookup"><span data-stu-id="c9cb1-141">Add an endpoint</span></span>

1. <span data-ttu-id="c9cb1-142">Aprire l'hub IoT, fare clic su Endpoint > + Add (+ Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="c9cb1-142">Open your IoT hub, click Endpoints > + Add.</span></span>
1. <span data-ttu-id="c9cb1-143">Immettere le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="c9cb1-143">Enter the following information:</span></span>

   <span data-ttu-id="c9cb1-144">**Nome**: nome dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-144">**Name**: The name of the endpoint.</span></span>

   <span data-ttu-id="c9cb1-145">**Tipo di endpoint**: selezionare **Coda del bus di servizio**.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-145">**Endpoint type**: Select **Service Bus Queue**.</span></span>

   <span data-ttu-id="c9cb1-146">**Spazio dei nomi del bus di servizio**: selezionare lo spazio dei nomi creato.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-146">**Service Bus namespace**: Select the namespace you created.</span></span>

   <span data-ttu-id="c9cb1-147">**Coda del bus di servizio**: selezionare la coda creata.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-147">**Service Bus queue**: Select the queue you created.</span></span>
1. <span data-ttu-id="c9cb1-148">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-148">Click **OK**.</span></span>

   ![Aggiungere un endpoint all'hub IoT nel portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a><span data-ttu-id="c9cb1-150">Aggiungere una regola di routing</span><span class="sxs-lookup"><span data-stu-id="c9cb1-150">Add a routing rule</span></span>

1. <span data-ttu-id="c9cb1-151">Nell'hub IoT fare clic su **Route**  > **+ Add** (+ Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="c9cb1-151">In your IoT hub, click **Routes** > **+ Add**.</span></span>
1. <span data-ttu-id="c9cb1-152">Immettere le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="c9cb1-152">Enter the following information:</span></span>

   <span data-ttu-id="c9cb1-153">**Nome**: il nome della regola di routing.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-153">**Name**: The name of the routing rule.</span></span>

   <span data-ttu-id="c9cb1-154">**Origine dati**: selezionare **DeviceMessages**.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-154">**Data source**: Select **DeviceMessages**.</span></span>

   <span data-ttu-id="c9cb1-155">**Endpoint**: selezionare l'endpoint creato.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-155">**Endpoint**: Select the endpoint you created.</span></span>

   <span data-ttu-id="c9cb1-156">**Stringa di query**: inserire `temperatureAlert = "true"`.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-156">**Query string**: Enter `temperatureAlert = "true"`.</span></span>
1. <span data-ttu-id="c9cb1-157">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-157">Click **Save**.</span></span>

   ![Aggiungere una regola di routing nel portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a><span data-ttu-id="c9cb1-159">Creare e configurare un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="c9cb1-159">Create and configure a logic app</span></span>

### <a name="create-a-logic-app"></a><span data-ttu-id="c9cb1-160">Creare un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="c9cb1-160">Create a logic app</span></span>

1. <span data-ttu-id="c9cb1-161">Nel [portale di Azure](https://portal.azure.com/), fare clic su **Nuovo** > **Integrazione aziendale** > **App per la logica**.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-161">In the [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Logic App**.</span></span>
1. <span data-ttu-id="c9cb1-162">Immettere le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="c9cb1-162">Enter the following information:</span></span>

   <span data-ttu-id="c9cb1-163">**Nome**: il nome dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-163">**Name**: The name of the logic app.</span></span>

   <span data-ttu-id="c9cb1-164">**Gruppo di risorse**: usare lo stesso gruppo di risorse usato da hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-164">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="c9cb1-165">**Posizione**: usare la stessa posizione che usa l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-165">**Location**: Use the same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="c9cb1-166">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-166">Click **Create**.</span></span>

### <a name="configure-the-logic-app"></a><span data-ttu-id="c9cb1-167">Configurare l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="c9cb1-167">Configure the logic app</span></span>

1. <span data-ttu-id="c9cb1-168">Aprire l'app per la logica che viene visualizzata nella finestra di progettazione di App per la logica.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-168">Open the logic app that opens into the Logic Apps Designer.</span></span>
1. <span data-ttu-id="c9cb1-169">Nella finestra di progettazione di App per la logica, fare clic su **App per la logica vuota**.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-169">In the Logic Apps Designer, click **Blank Logic App**.</span></span>

   ![Nel portale di Azure iniziare con un'app per la logica vuota](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="c9cb1-171">Fare clic su **Bus di servizio**.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-171">Click **Service Bus**.</span></span>

   ![Selezionare il bus di servizio per avviare la creazione dell'app per la logica nel portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="c9cb1-173">Fare clic su **Service Bus – When one or more messages arrive in a queue (auto-complete)** (Bus di servizio: all'arrivo di uno o più messaggi in una coda, completamento automatico).</span><span class="sxs-lookup"><span data-stu-id="c9cb1-173">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span></span>
1. <span data-ttu-id="c9cb1-174">Creare una connessione per il bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-174">Create a service bus connection.</span></span>
   1. <span data-ttu-id="c9cb1-175">Immettere un nome di connessione.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-175">Enter a connection name.</span></span>
   1. <span data-ttu-id="c9cb1-176">Fare clic sullo spazio dei nomi del bus di servizio > sul criterio del bus di servizio > **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-176">Click the service bus namespace > the service bus policy > **Create**.</span></span>

      ![Creare una connessione del bus di servizio per l'app per la logica nel portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. <span data-ttu-id="c9cb1-178">Fare clic su **Continua** dopo aver creato la connessione del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-178">Click **Continue** after the service bus connection is created.</span></span>
   1. <span data-ttu-id="c9cb1-179">Selezionare la coda creata e immettere `175` per **Numero massimo di messaggi**</span><span class="sxs-lookup"><span data-stu-id="c9cb1-179">Select the queue that you created and enter `175` for **Maximum message count**</span></span>

      ![Specificare il numero massimo di messaggi per la connessione del bus di servizio nell'app per la logica](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. <span data-ttu-id="c9cb1-181">Fare clic sul pulsante "Salva" per salvare le modifiche apportate.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-181">Click "Save" button to save the changes.</span></span>

1. <span data-ttu-id="c9cb1-182">Creare una connessione del servizio SMTP.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-182">Create an SMTP service connection.</span></span>
   1. <span data-ttu-id="c9cb1-183">Fare clic su **Nuovo passaggio** > **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-183">Click **New step** > **Add an action**.</span></span>
   1. <span data-ttu-id="c9cb1-184">Tipo `SMTP`, fare clic sul servizio **SMTP** nei risultati della ricerca e quindi fare clic su **SMTP - Send Email** (SMTP: inviare un'email).</span><span class="sxs-lookup"><span data-stu-id="c9cb1-184">Type `SMTP`, click the **SMTP** service in the search result, and then click **SMTP - Send Email**.</span></span>

      ![Creare una connessione SMTP nell'app per la logica nel portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. <span data-ttu-id="c9cb1-186">Immettere le informazioni SMTP della cassetta postale e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-186">Enter the SMTP information of your mailbox, and then click **Create**.</span></span>

      ![Inserire le informazioni sulla connessione SMTP nell'app per la logica nel portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      <span data-ttu-id="c9cb1-188">Ottenere le informazioni di SMTP per [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en) e [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span><span class="sxs-lookup"><span data-stu-id="c9cb1-188">Get the SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span></span>
   1. <span data-ttu-id="c9cb1-189">Immettere l'indirizzo di posta elettronica per **From** (Da) e **To** (A)e `High temperature detected` per **Oggetto** e **Corpo**.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-189">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span></span>
   1. <span data-ttu-id="c9cb1-190">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-190">Click **Save**.</span></span>

<span data-ttu-id="c9cb1-191">L'app per la logica è in funzionamento durante il salvataggio.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-191">The logic app is in working order when you save it.</span></span>

## <a name="test-the-logic-app"></a><span data-ttu-id="c9cb1-192">Testare l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="c9cb1-192">Test the logic app</span></span>

1. <span data-ttu-id="c9cb1-193">Avviare l'applicazione client che si distribuisce nel dispositivo in [Connect ESP8266 to Azure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md) (Connettere ESP8266 all'Hub IoT di Azure).</span><span class="sxs-lookup"><span data-stu-id="c9cb1-193">Start the client application that you deploy to your device in [Connect ESP8266 to Azure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span></span>
1. <span data-ttu-id="c9cb1-194">Aumentare la temperatura dell'ambiente attorno a SensorTag affinché superi i 30°C. Ad esempio accendere una candela intorno a SensorTag.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-194">Increase the environment temperature around the SensorTag to be above 30 C. For example, light a candle around your SensorTag.</span></span>
1. <span data-ttu-id="c9cb1-195">Si dovrebbe ricevere una notifica tramite posta elettronica inviata dall'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-195">You should receive an email notification sent by the logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c9cb1-196">Il provider di servizi di posta elettronica potrebbe dover verificare l'identità del mittente per verificare che sia l'invio del messaggio di posta elettronica viene eseguito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-196">Your email service provider may need to verify the sender identity to make sure it is you who sends the email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9cb1-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c9cb1-197">Next steps</span></span>

<span data-ttu-id="c9cb1-198">È stata creata correttamente un'app per la logica che connette l'hub IoT e la cassetta postale per il monitoraggio della temperatura e le notifiche.</span><span class="sxs-lookup"><span data-stu-id="c9cb1-198">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
