---
title: monitoraggio remoto aaaIoT e notifiche con Azure logica App | Documenti Microsoft
description: Usare le app di logica di Azure per il monitoraggio della temperatura l'hub IoT e automaticamente inviare cassetta postale tooyour di notifiche di posta elettronica eventuali anomalie rilevato IoT.
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
ms.openlocfilehash: 89396528ed63c37258e1b49f342f0723e686ecb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a><span data-ttu-id="d78a3-104">Monitoraggio remoto e notifiche di IoT con App per la logica di Azure tramite la connessione all'hub IoT e alla cassetta postale</span><span class="sxs-lookup"><span data-stu-id="d78a3-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span></span>

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="d78a3-106">Le app di logica di Azure fornisce un modo tooautomate processi come una serie di passaggi.</span><span class="sxs-lookup"><span data-stu-id="d78a3-106">Azure Logic Apps provides a way tooautomate processes as a series of steps.</span></span> <span data-ttu-id="d78a3-107">Un'app per la logica può connettersi tramite diversi servizi e protocolli.</span><span class="sxs-lookup"><span data-stu-id="d78a3-107">A logic app can connect across various services and protocols.</span></span> <span data-ttu-id="d78a3-108">Inizia con un trigger, ad esempio "When an account is added" (Quando si aggiunge un account), seguito da una combinazione di azioni, come "sending a push notification" (invio di una notifica push).</span><span class="sxs-lookup"><span data-stu-id="d78a3-108">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span></span> <span data-ttu-id="d78a3-109">Questa caratteristica rende App per la logica una soluzione IoT perfetta per il monitoraggio IoT, ad esempio per stare in allerta in caso di anomalie, tra altri scenari di uso.</span><span class="sxs-lookup"><span data-stu-id="d78a3-109">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="d78a3-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="d78a3-110">What you learn</span></span>

<span data-ttu-id="d78a3-111">Si apprenderà come toocreate un'app di logica che si connette l'hub IoT e cassetta postale per il monitoraggio della temperatura e notifiche.</span><span class="sxs-lookup"><span data-stu-id="d78a3-111">You learn how toocreate a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span> <span data-ttu-id="d78a3-112">Quando la temperatura hello è superiore a 30 C, hello client applicazione segni `temperatureAlert = "true"` invia il messaggio hello tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d78a3-112">When hello temperature is above 30 C, hello client application marks `temperatureAlert = "true"` in hello message it sends tooyour IoT hub.</span></span> <span data-ttu-id="d78a3-113">il messaggio Hello trigger hello logica app toosend è una notifica di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="d78a3-113">hello message triggers hello logic app toosend you an email notification.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="d78a3-114">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="d78a3-114">What you do</span></span>

* <span data-ttu-id="d78a3-115">Creare uno spazio dei nomi di service bus e aggiungere tooit una coda.</span><span class="sxs-lookup"><span data-stu-id="d78a3-115">Create a service bus namespace and add a queue tooit.</span></span>
* <span data-ttu-id="d78a3-116">Aggiungere un endpoint e un hub IoT di routing regola tooyour.</span><span class="sxs-lookup"><span data-stu-id="d78a3-116">Add an endpoint and a routing rule tooyour IoT hub.</span></span>
* <span data-ttu-id="d78a3-117">Creare, configurare e testare un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="d78a3-117">Create, configure, and test a logic app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d78a3-118">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="d78a3-118">What you need</span></span>

* <span data-ttu-id="d78a3-119">Esercitazione [configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completato che copre hello seguenti requisiti:</span><span class="sxs-lookup"><span data-stu-id="d78a3-119">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  * <span data-ttu-id="d78a3-120">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="d78a3-120">An active Azure subscription.</span></span>
  * <span data-ttu-id="d78a3-121">Un hub IoT di Azure nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d78a3-121">An Azure IoT hub under your subscription.</span></span>
  * <span data-ttu-id="d78a3-122">Un'applicazione client che invia l'hub IoT di Azure tooyour messaggi.</span><span class="sxs-lookup"><span data-stu-id="d78a3-122">A client application that sends messages tooyour Azure IoT hub.</span></span>

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a><span data-ttu-id="d78a3-123">Creare lo spazio dei nomi di service bus e aggiungere un tooit coda</span><span class="sxs-lookup"><span data-stu-id="d78a3-123">Create service bus namespace and add a queue tooit</span></span>

### <a name="create-a-service-bus-namespace"></a><span data-ttu-id="d78a3-124">Creare uno spazio dei nomi del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="d78a3-124">Create a service bus namespace</span></span>

1. <span data-ttu-id="d78a3-125">In hello [portale di Azure](https://portal.azure.com/), fare clic su **New** > **Enterprise Integration** > **Bus di servizio**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-125">On hello [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Service Bus**.</span></span>
1. <span data-ttu-id="d78a3-126">Fornire hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="d78a3-126">Provide hello following information:</span></span>

   <span data-ttu-id="d78a3-127">**Nome**: nome hello del bus di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d78a3-127">**Name**: hello name of hello service bus.</span></span>

   <span data-ttu-id="d78a3-128">**Piano tariffario**: fare clic su **Base** > **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-128">**Pricing tier**: Click **Basic** > **Select**.</span></span> <span data-ttu-id="d78a3-129">livello Basic Hello è sufficiente per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d78a3-129">hello Basic tier is sufficient for this tutorial.</span></span>

   <span data-ttu-id="d78a3-130">**Gruppo di risorse**: utilizzare hello stesso gruppo di risorse che usa l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d78a3-130">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="d78a3-131">**Percorso**: utilizzare hello stesso percorso utilizzato per l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d78a3-131">**Location**: Use hello same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="d78a3-132">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-132">Click **Create**.</span></span>

   ![Creare uno spazio dei nomi di service bus in hello portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a><span data-ttu-id="d78a3-134">Aggiungere una coda del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="d78a3-134">Add a service bus queue</span></span>

1. <span data-ttu-id="d78a3-135">Aprire lo spazio dei nomi di hello service bus e quindi fare clic su **+ coda**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-135">Open hello service bus namespace, and then click **+ Queue**.</span></span>
1. <span data-ttu-id="d78a3-136">Immettere un nome per la coda hello e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-136">Enter a name for hello queue and then click **Create**.</span></span>
1. <span data-ttu-id="d78a3-137">Aprire una coda del bus di servizio hello e quindi fare clic su **criteri di accesso condiviso** > **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-137">Open hello service bus queue, and then click **Shared access policies** > **+ Add**.</span></span>
1. <span data-ttu-id="d78a3-138">Immettere un nome per i criteri di hello, controllo **Gestisci**, quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-138">Enter a name for hello policy, check **Manage**, and then click **Create**.</span></span>

   ![Aggiungere una coda del bus di servizio nel portale di Azure hello](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a><span data-ttu-id="d78a3-140">Aggiungere un endpoint e un hub IoT di routing regola tooyour</span><span class="sxs-lookup"><span data-stu-id="d78a3-140">Add an endpoint and a routing rule tooyour IoT hub</span></span>

### <a name="add-an-endpoint"></a><span data-ttu-id="d78a3-141">Aggiungere un endpoint</span><span class="sxs-lookup"><span data-stu-id="d78a3-141">Add an endpoint</span></span>

1. <span data-ttu-id="d78a3-142">Aprire l'hub IoT, fare clic su Endpoint > + Add (+ Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="d78a3-142">Open your IoT hub, click Endpoints > + Add.</span></span>
1. <span data-ttu-id="d78a3-143">Immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="d78a3-143">Enter hello following information:</span></span>

   <span data-ttu-id="d78a3-144">**Nome**: nome hello dell'endpoint di hello.</span><span class="sxs-lookup"><span data-stu-id="d78a3-144">**Name**: hello name of hello endpoint.</span></span>

   <span data-ttu-id="d78a3-145">**Tipo di endpoint**: selezionare **Coda del bus di servizio**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-145">**Endpoint type**: Select **Service Bus Queue**.</span></span>

   <span data-ttu-id="d78a3-146">**Spazio dei nomi Service Bus**: selezionare spazio dei nomi hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="d78a3-146">**Service Bus namespace**: Select hello namespace you created.</span></span>

   <span data-ttu-id="d78a3-147">**Coda di Service Bus**: coda hello selezionare creata.</span><span class="sxs-lookup"><span data-stu-id="d78a3-147">**Service Bus queue**: Select hello queue you created.</span></span>
1. <span data-ttu-id="d78a3-148">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-148">Click **OK**.</span></span>

   ![Aggiungere un hub IoT tooyour di endpoint in hello portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a><span data-ttu-id="d78a3-150">Aggiungere una regola di routing</span><span class="sxs-lookup"><span data-stu-id="d78a3-150">Add a routing rule</span></span>

1. <span data-ttu-id="d78a3-151">Nell'hub IoT fare clic su **Route**  > **+ Add** (+ Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="d78a3-151">In your IoT hub, click **Routes** > **+ Add**.</span></span>
1. <span data-ttu-id="d78a3-152">Immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="d78a3-152">Enter hello following information:</span></span>

   <span data-ttu-id="d78a3-153">**Nome**: nome hello della regola di routing hello.</span><span class="sxs-lookup"><span data-stu-id="d78a3-153">**Name**: hello name of hello routing rule.</span></span>

   <span data-ttu-id="d78a3-154">**Origine dati**: selezionare **DeviceMessages**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-154">**Data source**: Select **DeviceMessages**.</span></span>

   <span data-ttu-id="d78a3-155">**Endpoint**: selezionare hello endpoint creato.</span><span class="sxs-lookup"><span data-stu-id="d78a3-155">**Endpoint**: Select hello endpoint you created.</span></span>

   <span data-ttu-id="d78a3-156">**Stringa di query**: inserire `temperatureAlert = "true"`.</span><span class="sxs-lookup"><span data-stu-id="d78a3-156">**Query string**: Enter `temperatureAlert = "true"`.</span></span>
1. <span data-ttu-id="d78a3-157">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-157">Click **Save**.</span></span>

   ![Aggiungere una regola di routing in hello portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a><span data-ttu-id="d78a3-159">Creare e configurare un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="d78a3-159">Create and configure a logic app</span></span>

### <a name="create-a-logic-app"></a><span data-ttu-id="d78a3-160">Creare un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="d78a3-160">Create a logic app</span></span>

1. <span data-ttu-id="d78a3-161">In hello [portale di Azure](https://portal.azure.com/), fare clic su **New** > **Enterprise Integration** > **logica App**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-161">In hello [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Logic App**.</span></span>
1. <span data-ttu-id="d78a3-162">Immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="d78a3-162">Enter hello following information:</span></span>

   <span data-ttu-id="d78a3-163">**Nome**: nome hello di hello logica app.</span><span class="sxs-lookup"><span data-stu-id="d78a3-163">**Name**: hello name of hello logic app.</span></span>

   <span data-ttu-id="d78a3-164">**Gruppo di risorse**: utilizzare hello stesso gruppo di risorse che usa l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d78a3-164">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="d78a3-165">**Percorso**: utilizzare hello stesso percorso utilizzato per l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d78a3-165">**Location**: Use hello same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="d78a3-166">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-166">Click **Create**.</span></span>

### <a name="configure-hello-logic-app"></a><span data-ttu-id="d78a3-167">Configurare hello logica app</span><span class="sxs-lookup"><span data-stu-id="d78a3-167">Configure hello logic app</span></span>

1. <span data-ttu-id="d78a3-168">Aprire hello logica app che viene aperta in hello logica di progettazione di App.</span><span class="sxs-lookup"><span data-stu-id="d78a3-168">Open hello logic app that opens into hello Logic Apps Designer.</span></span>
1. <span data-ttu-id="d78a3-169">Nella finestra di progettazione logica App hello, fare clic su **App vuota per la logica**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-169">In hello Logic Apps Designer, click **Blank Logic App**.</span></span>

   ![Iniziare con un'applicazione logica vuoto in hello portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="d78a3-171">Fare clic su **Bus di servizio**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-171">Click **Service Bus**.</span></span>

   ![Selezionare il Bus di servizio toostart creazione dell'applicazione la logica nel portale di Azure hello](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="d78a3-173">Fare clic su **Service Bus – When one or more messages arrive in a queue (auto-complete)** (Bus di servizio: all'arrivo di uno o più messaggi in una coda, completamento automatico).</span><span class="sxs-lookup"><span data-stu-id="d78a3-173">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span></span>
1. <span data-ttu-id="d78a3-174">Creare una connessione per il bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="d78a3-174">Create a service bus connection.</span></span>
   1. <span data-ttu-id="d78a3-175">Immettere un nome di connessione.</span><span class="sxs-lookup"><span data-stu-id="d78a3-175">Enter a connection name.</span></span>
   1. <span data-ttu-id="d78a3-176">Fare clic su hello service bus namespace > hello criteri bus di servizio > **crea**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-176">Click hello service bus namespace > hello service bus policy > **Create**.</span></span>

      ![Creare una connessione di bus di servizio per l'app logica in hello portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. <span data-ttu-id="d78a3-178">Fare clic su **continua** dopo la creazione di connessione del bus di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d78a3-178">Click **Continue** after hello service bus connection is created.</span></span>
   1. <span data-ttu-id="d78a3-179">Selezionare una coda hello creata e immettere `175` per **numero massimo di messaggi**</span><span class="sxs-lookup"><span data-stu-id="d78a3-179">Select hello queue that you created and enter `175` for **Maximum message count**</span></span>

      ![Specificare il conteggio massima del messaggio hello per la connessione del bus di servizio hello nell'app logica](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. <span data-ttu-id="d78a3-181">Fare clic su "Salva" pulsante toosave hello cambia.</span><span class="sxs-lookup"><span data-stu-id="d78a3-181">Click "Save" button toosave hello changes.</span></span>

1. <span data-ttu-id="d78a3-182">Creare una connessione del servizio SMTP.</span><span class="sxs-lookup"><span data-stu-id="d78a3-182">Create an SMTP service connection.</span></span>
   1. <span data-ttu-id="d78a3-183">Fare clic su **Nuovo passaggio** > **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-183">Click **New step** > **Add an action**.</span></span>
   1. <span data-ttu-id="d78a3-184">Tipo `SMTP`, fare clic su hello **SMTP** nei risultati di ricerca hello del servizio e quindi fare clic su **SMTP - invio di posta elettronica**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-184">Type `SMTP`, click hello **SMTP** service in hello search result, and then click **SMTP - Send Email**.</span></span>

      ![Creare una connessione SMTP nell'app logica in hello portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. <span data-ttu-id="d78a3-186">Immettere le informazioni della cassetta postale SMTP hello e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-186">Enter hello SMTP information of your mailbox, and then click **Create**.</span></span>

      ![Immettere le informazioni di connessione SMTP nell'app logica in hello portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      <span data-ttu-id="d78a3-188">Ottenere informazioni hello SMTP per [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), e [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span><span class="sxs-lookup"><span data-stu-id="d78a3-188">Get hello SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span></span>
   1. <span data-ttu-id="d78a3-189">Immettere l'indirizzo di posta elettronica per **From** (Da) e **To** (A)e `High temperature detected` per **Oggetto** e **Corpo**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-189">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span></span>
   1. <span data-ttu-id="d78a3-190">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d78a3-190">Click **Save**.</span></span>

<span data-ttu-id="d78a3-191">Quando si salva, Hello logica app è in ordine di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d78a3-191">hello logic app is in working order when you save it.</span></span>

## <a name="test-hello-logic-app"></a><span data-ttu-id="d78a3-192">Test hello logica app</span><span class="sxs-lookup"><span data-stu-id="d78a3-192">Test hello logic app</span></span>

1. <span data-ttu-id="d78a3-193">Avviare un'applicazione hello client che si distribuisce il dispositivo tooyour in [tooAzure ESP8266 connessione IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d78a3-193">Start hello client application that you deploy tooyour device in [Connect ESP8266 tooAzure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span></span>
1. <span data-ttu-id="d78a3-194">Aumentare la temperatura ambiente hello intorno hello SensorTag toobe sopra c di 30. Ad esempio chiaro una candela intorno il SensorTag.</span><span class="sxs-lookup"><span data-stu-id="d78a3-194">Increase hello environment temperature around hello SensorTag toobe above 30 C. For example, light a candle around your SensorTag.</span></span>
1. <span data-ttu-id="d78a3-195">Dovresti ricevere una notifica di posta elettronica inviata da hello logica app.</span><span class="sxs-lookup"><span data-stu-id="d78a3-195">You should receive an email notification sent by hello logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d78a3-196">Il provider di servizi di posta elettronica potrebbe essere necessario che sia utenti che invia un messaggio e-mail hello toomake identità mittente hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="d78a3-196">Your email service provider may need tooverify hello sender identity toomake sure it is you who sends hello email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d78a3-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d78a3-197">Next steps</span></span>

<span data-ttu-id="d78a3-198">È stata creata correttamente un'app per la logica che connette l'hub IoT e la cassetta postale per il monitoraggio della temperatura e le notifiche.</span><span class="sxs-lookup"><span data-stu-id="d78a3-198">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
