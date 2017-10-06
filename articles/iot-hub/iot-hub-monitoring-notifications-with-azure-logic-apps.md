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
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a>Monitoraggio remoto e notifiche di IoT con App per la logica di Azure tramite la connessione all'hub IoT e alla cassetta postale

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Le app di logica di Azure fornisce un modo tooautomate processi come una serie di passaggi. Un'app per la logica può connettersi tramite diversi servizi e protocolli. Inizia con un trigger, ad esempio "When an account is added" (Quando si aggiunge un account), seguito da una combinazione di azioni, come "sending a push notification" (invio di una notifica push). Questa caratteristica rende App per la logica una soluzione IoT perfetta per il monitoraggio IoT, ad esempio per stare in allerta in caso di anomalie, tra altri scenari di uso.

## <a name="what-you-learn"></a>Contenuto dell'esercitazione

Si apprenderà come toocreate un'app di logica che si connette l'hub IoT e cassetta postale per il monitoraggio della temperatura e notifiche. Quando la temperatura hello è superiore a 30 C, hello client applicazione segni `temperatureAlert = "true"` invia il messaggio hello tooyour IoT hub. il messaggio Hello trigger hello logica app toosend è una notifica di posta elettronica.

## <a name="what-you-do"></a>Operazioni da fare

* Creare uno spazio dei nomi di service bus e aggiungere tooit una coda.
* Aggiungere un endpoint e un hub IoT di routing regola tooyour.
* Creare, configurare e testare un'app per la logica.

## <a name="what-you-need"></a>Elementi necessari

* Esercitazione [configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completato che copre hello seguenti requisiti:
  * Una sottoscrizione di Azure attiva.
  * Un hub IoT di Azure nella sottoscrizione.
  * Un'applicazione client che invia l'hub IoT di Azure tooyour messaggi.

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a>Creare lo spazio dei nomi di service bus e aggiungere un tooit coda

### <a name="create-a-service-bus-namespace"></a>Creare uno spazio dei nomi del bus di servizio

1. In hello [portale di Azure](https://portal.azure.com/), fare clic su **New** > **Enterprise Integration** > **Bus di servizio**.
1. Fornire hello le seguenti informazioni:

   **Nome**: nome hello del bus di servizio hello.

   **Piano tariffario**: fare clic su **Base** > **Seleziona**. livello Basic Hello è sufficiente per questa esercitazione.

   **Gruppo di risorse**: utilizzare hello stesso gruppo di risorse che usa l'hub IoT.

   **Percorso**: utilizzare hello stesso percorso utilizzato per l'hub IoT.
1. Fare clic su **Crea**.

   ![Creare uno spazio dei nomi di service bus in hello portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a>Aggiungere una coda del bus di servizio

1. Aprire lo spazio dei nomi di hello service bus e quindi fare clic su **+ coda**.
1. Immettere un nome per la coda hello e quindi fare clic su **crea**.
1. Aprire una coda del bus di servizio hello e quindi fare clic su **criteri di accesso condiviso** > **+ Aggiungi**.
1. Immettere un nome per i criteri di hello, controllo **Gestisci**, quindi fare clic su **crea**.

   ![Aggiungere una coda del bus di servizio nel portale di Azure hello](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a>Aggiungere un endpoint e un hub IoT di routing regola tooyour

### <a name="add-an-endpoint"></a>Aggiungere un endpoint

1. Aprire l'hub IoT, fare clic su Endpoint > + Add (+ Aggiungi).
1. Immettere hello le seguenti informazioni:

   **Nome**: nome hello dell'endpoint di hello.

   **Tipo di endpoint**: selezionare **Coda del bus di servizio**.

   **Spazio dei nomi Service Bus**: selezionare spazio dei nomi hello è stato creato.

   **Coda di Service Bus**: coda hello selezionare creata.
1. Fare clic su **OK**.

   ![Aggiungere un hub IoT tooyour di endpoint in hello portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a>Aggiungere una regola di routing

1. Nell'hub IoT fare clic su **Route**  > **+ Add** (+ Aggiungi).
1. Immettere hello le seguenti informazioni:

   **Nome**: nome hello della regola di routing hello.

   **Origine dati**: selezionare **DeviceMessages**.

   **Endpoint**: selezionare hello endpoint creato.

   **Stringa di query**: inserire `temperatureAlert = "true"`.
1. Fare clic su **Salva**.

   ![Aggiungere una regola di routing in hello portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a>Creare e configurare un'app per la logica

### <a name="create-a-logic-app"></a>Creare un'app per la logica

1. In hello [portale di Azure](https://portal.azure.com/), fare clic su **New** > **Enterprise Integration** > **logica App**.
1. Immettere hello le seguenti informazioni:

   **Nome**: nome hello di hello logica app.

   **Gruppo di risorse**: utilizzare hello stesso gruppo di risorse che usa l'hub IoT.

   **Percorso**: utilizzare hello stesso percorso utilizzato per l'hub IoT.
1. Fare clic su **Crea**.

### <a name="configure-hello-logic-app"></a>Configurare hello logica app

1. Aprire hello logica app che viene aperta in hello logica di progettazione di App.
1. Nella finestra di progettazione logica App hello, fare clic su **App vuota per la logica**.

   ![Iniziare con un'applicazione logica vuoto in hello portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. Fare clic su **Bus di servizio**.

   ![Selezionare il Bus di servizio toostart creazione dell'applicazione la logica nel portale di Azure hello](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. Fare clic su **Service Bus – When one or more messages arrive in a queue (auto-complete)** (Bus di servizio: all'arrivo di uno o più messaggi in una coda, completamento automatico).
1. Creare una connessione per il bus di servizio.
   1. Immettere un nome di connessione.
   1. Fare clic su hello service bus namespace > hello criteri bus di servizio > **crea**.

      ![Creare una connessione di bus di servizio per l'app logica in hello portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. Fare clic su **continua** dopo la creazione di connessione del bus di servizio hello.
   1. Selezionare una coda hello creata e immettere `175` per **numero massimo di messaggi**

      ![Specificare il conteggio massima del messaggio hello per la connessione del bus di servizio hello nell'app logica](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. Fare clic su "Salva" pulsante toosave hello cambia.

1. Creare una connessione del servizio SMTP.
   1. Fare clic su **Nuovo passaggio** > **Aggiungi un'azione**.
   1. Tipo `SMTP`, fare clic su hello **SMTP** nei risultati di ricerca hello del servizio e quindi fare clic su **SMTP - invio di posta elettronica**.

      ![Creare una connessione SMTP nell'app logica in hello portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. Immettere le informazioni della cassetta postale SMTP hello e quindi fare clic su **crea**.

      ![Immettere le informazioni di connessione SMTP nell'app logica in hello portale di Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      Ottenere informazioni hello SMTP per [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), e [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).
   1. Immettere l'indirizzo di posta elettronica per **From** (Da) e **To** (A)e `High temperature detected` per **Oggetto** e **Corpo**.
   1. Fare clic su **Salva**.

Quando si salva, Hello logica app è in ordine di lavoro.

## <a name="test-hello-logic-app"></a>Test hello logica app

1. Avviare un'applicazione hello client che si distribuisce il dispositivo tooyour in [tooAzure ESP8266 connessione IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).
1. Aumentare la temperatura ambiente hello intorno hello SensorTag toobe sopra c di 30. Ad esempio chiaro una candela intorno il SensorTag.
1. Dovresti ricevere una notifica di posta elettronica inviata da hello logica app.

   > [!NOTE]
   > Il provider di servizi di posta elettronica potrebbe essere necessario che sia utenti che invia un messaggio e-mail hello toomake identità mittente hello tooverify.

## <a name="next-steps"></a>Passaggi successivi

È stata creata correttamente un'app per la logica che connette l'hub IoT e la cassetta postale per il monitoraggio della temperatura e le notifiche.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
