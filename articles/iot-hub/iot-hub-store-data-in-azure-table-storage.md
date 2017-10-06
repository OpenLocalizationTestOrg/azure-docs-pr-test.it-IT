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
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a>Salvare i messaggi di hub IoT contenenti sensore dati tooyour archiviazione tabelle Azure

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Contenuto dell'esercitazione

Viene illustrato come toocreate un account di archiviazione di Azure e un Azure funzione messaggi dell'hub IoT toostore app nell'archiviazione tabella.

## <a name="what-you-do"></a>Operazioni da fare

- Creare un account di archiviazione di Azure
- Preparare l'hub IoT messaggi tooread di connessione.
- Creare e distribuire un'app per le funzioni di Azure.

## <a name="what-you-need"></a>Elementi necessari

- [Configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) hello toocover seguenti requisiti:
  - Una sottoscrizione di Azure attiva
  - Un hub IoT nella sottoscrizione 
  - Un'applicazione in esecuzione che invia l'hub IoT tooyour messaggi

## <a name="create-an-azure-storage-account"></a>Creare un account di archiviazione di Azure

1. In hello [portale di Azure](https://portal.azure.com/), fare clic su **New** > **archiviazione** > **account di archiviazione**  >   **Creare**.

2. Immettere le informazioni necessarie per l'account di archiviazione hello hello:

   ![Creare un account di archiviazione nel portale di Azure hello](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * **Nome**: nome hello hello dell'account di archiviazione. nome Hello deve essere globalmente univoco.

   * **Gruppo di risorse**: utilizzare hello stesso gruppo di risorse che usa l'hub IoT.

   * **PIN toodashboard**: selezionare questa opzione per l'hub IoT tooyour di facile accesso dal dashboard hello.

3. Fare clic su **Crea**.

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a>Preparare l'hub IoT messaggi tooread connessione

Hub IoT espone un evento incorporato endpoint compatibile con hub tooenable applicazioni tooread IoT hub dei messaggi. Nel frattempo, le applicazioni utilizzano dati tooread gruppi di consumer dall'hub IoT. Prima di creare un dati tooread app di Azure (funzione) dall'hub IoT, hello seguenti:

- Ottenere la stringa di connessione hello dell'endpoint hub IoT.
- Creare un gruppo di consumer per l'hub IoT.

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a>Ottiene la stringa di connessione hello dell'endpoint hub IoT

1. Aprire l'hub IoT.

2. In hello **IoT Hub** riquadro, in **messaggistica**, fare clic su **endpoint**.

3. In hello destro in riquadro **gli endpoint predefiniti**, fare clic su **eventi**.

4. In hello **proprietà** riquadro, hello nota seguenti valori:
   - Endpoint compatibile con l'hub eventi
   - Nome compatibile con l'hub eventi

   ![Ottenere la stringa di connessione hello dell'endpoint hub IoT in hello portale di Azure](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. In hello **IoT Hub** riquadro, in **impostazioni**, fare clic su **criteri di accesso condiviso**.

6. Fare clic su **iothubowner**.

7. Hello nota **chiave primaria** valore.

8. Creare la stringa di connessione hello dell'endpoint hub IoT come segue:

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > Sostituire `<Event Hub-compatible endpoint>` e `<Primary key>` con i valori hello annotati in precedenza.

### <a name="create-a-consumer-group-for-your-iot-hub"></a>Creare un gruppo di consumer per l'hub IoT

1. Aprire l'hub IoT.

2. In hello **IoT Hub** riquadro, in **messaggistica**, fare clic su **endpoint**.

3. In hello destro in riquadro **gli endpoint predefiniti**, fare clic su **eventi**.

4. In hello **proprietà** riquadro, in **gruppi di Consumer**, immettere un nome e quindi prendere nota di esso.

5. Fare clic su **Salva**.

## <a name="create-and-deploy-an-azure-function-app"></a>Creare e distribuire un'app per le funzioni di Azure

1. In hello [portale di Azure](https://portal.azure.com/), fare clic su **New** > **calcolo** > **funzione App**  >   **Creare**.

2. Immettere le informazioni necessarie per app di funzione hello hello.

   ![Creare un'app di funzione in hello portale di Azure](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * **Nome dell'app**: nome hello di hello funzione app. nome Hello deve essere globalmente univoco.

   * **Gruppo di risorse**: utilizzare hello stesso gruppo di risorse che usa l'hub IoT.

   * **Account di archiviazione**: hello account di archiviazione creato.

   * **PIN toodashboard**: selezionare questa opzione per accedere facilmente toohello funzione app dal dashboard hello.

3. Fare clic su **Crea**.

4. Dopo la funzione hello app è stata creata, aprirlo.

5. Nell'app di funzione hello, creare una nuova funzione eseguendo hello seguenti:

   a. Fare clic su **Nuova funzione**.

   b. Selezionare **JavaScript** per **Linguaggio** ed **Elaborazione dati** per **Scenario**.

   c. Fare clic su **Creare questa funzione** e quindi su **Nuova funzione**.

   d. Selezionare **JavaScript** per Java hello e **l'elaborazione dati** per scenario hello.

   e. Fare clic su hello **EventHubTrigger JavaScript** modello.

   f. Immettere le informazioni necessarie per il modello di hello hello.

      * **Nome funzione di**: nome hello della funzione hello.

      * **Nome dell'Hub eventi**: nome compatibile con hub di eventi hello annotato in precedenza.

      * **Connessione dell'Hub eventi**: stringa di connessione tooadd hello dell'endpoint hub IoT hello a cui è stato creato, fare clic su **New**.

   g. Fare clic su **Crea**.

6. Configurare un output di hello funzione eseguendo hello seguenti:

   a. Fare clic su **Integrazione** > **Nuovo output** > **Archiviazione tabelle di Azure** > **Seleziona**.

      ![Aggiungi tabella archiviazione tooyour funzione app nel portale di Azure hello](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   b. Immettere le informazioni necessarie hello.

      * **Nome del parametro tabella**: utilizzare `outputTable`, che verrà utilizzata in hello Azure codice della funzione.
      
      * **Nome tabella**: usare `deviceData`.

      * **Connessione dell'account di archiviazione**: fare clic su **nuovo** e selezionare o immettere l'account di archiviazione. Se l'account di archiviazione hello non viene visualizzata, vedere [requisiti dell'account di archiviazione](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).
      
   c. Fare clic su **Salva**.

7. In **Trigger** fare clic su **Hub eventi di Azure (eventHubMessages)**.

8. In **gruppo di consumer dell'Hub eventi**, immettere il nome di hello del gruppo di consumer hello è creato e quindi fare clic su **salvare**.

9. Fare clic su funzione hello creato in hello a sinistra e quindi fare clic su **Visualizza file** su hello destra.

10. Sostituire il codice hello in `index.js` con seguenti hello:

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

11. Fare clic su **Salva**.

App di funzione hello è stata creata. che archivia i messaggi ricevuti dall'hub IoT nell'archiviazione tabelle di Azure.

> [!NOTE]
> È possibile utilizzare hello **eseguire** pulsante tootest hello funzione app. Quando fa clic su **eseguire**, il messaggio di prova hello viene inviato l'hub IoT tooyour. all'arrivo di Hello del messaggio hello deve attivare hello funzione app toostart e quindi salvare archiviazione tabelle di tooyour messaggio hello. Hello **registri** riquadro registra informazioni dettagliate di hello del processo di hello.

## <a name="verify-your-message-in-your-table-storage"></a>Verificare il messaggio nell'archivio tabelle

1. Eseguire l'applicazione di esempio hello in hub IoT tooyour di messaggi toosend di dispositivo.

2. [Scaricare e installare Azure Storage Explorer](http://storageexplorer.com/).

3. Aprire Esplora risorse di archiviazione, fare clic su **aggiungere un Account Azure** > **Accedi**, quindi accedi tooyour account Azure.

4. Fare clic sulla sottoscrizione di Azure > **Account di archiviazione** > account di archiviazione > **Tabelle** > **deviceData**.

   Si dovrebbero essere visualizzati i messaggi inviati dall'hub IoT di tooyour dispositivo connesso hello `deviceData` tabella.

## <a name="next-steps"></a>Passaggi successivi

Sono stati creati l'account di archiviazione di Azure e l'app per le funzioni di Azure, che archivia i messaggi ricevuti dall'hub IoT nell'archiviazione tabelle di Azure.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
