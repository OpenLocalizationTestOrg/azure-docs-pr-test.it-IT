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
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a>Visualizzare i dati in tempo reale sensore l'hub IoT di Azure utilizzando hello App Web di servizio App di Azure

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Contenuto dell'esercitazione

In questa esercitazione viene illustrato come dati del sensore in tempo reale toovisualize che riceve l'hub IoT mediante l'esecuzione di un'applicazione web che sono ospitati in un'app web. Se si desiderano dati di hello toovisualize tootry nell'hub IoT con Power BI, vedere [dati di un sensore in tempo reale toovisualize Usa Power BI dall'IoT Hub Azure](iot-hub-live-data-visualization-in-power-bi.md).

## <a name="what-you-do"></a>Operazioni da fare

- Creare un'app web nel portale di Azure hello.
- Preparare l'hub IoT per l'accesso dei dati mediante l'aggiunta di un gruppo di consumer.
- Configurare hello tooread sensore dati dell'app web dall'hub IoT.
- Caricare un toobe di applicazione web ospitata da app web hello.
- Aprire hello toosee in tempo reale temperatura e umidità dati dell'app web dall'hub IoT.

## <a name="what-you-need"></a>Elementi necessari

- [Configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md), in cui rientra hello seguenti requisiti:
  - Una sottoscrizione di Azure attiva
  - Un hub IoT nella sottoscrizione
  - Un'applicazione client che invia l'hub Iot tooyour messaggi
- [Scaricare Git](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a>Creare un'app Web

1. In hello [portale di Azure](https://ms.portal.azure.com/), fare clic su **New** > **Web e dispositivi mobili** > **App Web**.
2. Immettere un nome univoco di processo, verificare la sottoscrizione hello, specificare un gruppo di risorse e il percorso, seleziona **Pin toodashboard**, quindi fare clic su **crea**.

   È consigliabile selezionare hello stesso percorso del gruppo di risorse. In questo modo è di aiuto con velocità di elaborazione e consente di ridurre il costo di hello di trasferimento dei dati.

   ![Creare un'app Web](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a>Configurare hello web tooread i dati delle app per l'hub IoT

1. Aprire l'app web hello che appena effettuato il provisioning.
2. Fare clic su **le impostazioni dell'applicazione**e quindi in **impostazioni App**, aggiungere hello coppie chiave/valore seguenti:

   | Chiave                                   | Valore                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | Azure.IoT.IoTHub.ConnectionString     | Ottenuto da iothub-explorer                                |
   | Azure.IoT.IoTHub.ConsumerGroup        | nome Hello del gruppo di consumer hello aggiungere tooyour IoT hub  |

   ![Aggiungere impostazioni tooyour web app con coppie chiave/valore](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. Fare clic su **le impostazioni dell'applicazione**in **impostazioni generali**, hello attiva/disattiva **Web socket** opzione e quindi fare clic su **salvare**.

   ![Attiva o disattiva hello Web socket](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a>Caricare un toobe di applicazione web ospitata da app web hello

Su GitHub è disponibile un'applicazione Web che consente di visualizzare i dati del sensore in tempo reale dall'hub IoT. È sufficiente toodo configurare hello web app toowork con un repository Git, scaricare l'applicazione web hello da GitHub e quindi caricarla tooAzure per hello web app toohost.

1. Nell'app web hello, fare clic su **opzioni di distribuzione** > **Scegli origine** > **Git Repository locale**, quindi fare clic su **OK**.

   ![Configurare il web app distribuzione toouse hello repository Git locale](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. Fare clic su **le credenziali di distribuzione**, creare un utente nome e la password toouse tooconnect toohello repository Git in Azure e quindi fare clic su **salvare**.

3. Fare clic su **Panoramica**e prendere nota del valore di hello **url clone Git**.

   ![Ottenere l'URL del clone Git hello dell'app web](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. Aprire una finestra del comando o del terminale nel computer locale.

5. Scaricare l'app web hello da GitHub e caricarlo tooAzure per hello web app toohost. toodo in tal caso, eseguire hello seguenti comandi:

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > \<URL clone GIT\> hello URL del repository Git hello trovato in hello **Panoramica** pagina dell'app web hello.

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a>Aprire hello toosee in tempo reale temperatura e umidità dati dell'app web dall'hub IoT

In hello **Panoramica** pagina dell'app web, fare clic su hello URL tooopen hello web app.

![Ottenere hello URL dell'app web](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

Si noterà temperatura in tempo reale hello e dati umidità dall'hub IoT.

![Pagina dell'app Web che mostra temperatura e umidità in tempo reale](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> Verificare che l'applicazione di esempio hello è in esecuzione sul dispositivo. Se non si otterrà un grafico vuoto, è possibile fare riferimento a esercitazioni toohello in [configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md).

## <a name="next-steps"></a>Passaggi successivi
Utilizzati correttamente i dati in tempo reale sensore toovisualize dell'app web dall'hub IoT.

Per i dati di toovisualize un modo alternativo provenienti dall'IoT Hub di Azure, vedere [dati di un sensore in tempo reale toovisualize Usa Power BI dall'hub IoT](iot-hub-live-data-visualization-in-power-bi.md).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
