---
title: un hub IoT mediante Azure CLI (azure.js) aaaCreate | Documenti Microsoft
description: Come un hub IoT di Azure mediante toocreate hello multipiattaforma CLI di Azure (azure.js).
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: boltean
ms.openlocfilehash: c2a7ea98500b0a0e55a39f4cdfea4605c92add94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli"></a>Creazione di un hub IoT utilizzando hello CLI di Azure

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Introduzione

È possibile utilizzare toocreate CLI di Azure (azure.js) e gestire hub IoT di Azure a livello di codice. Questo articolo illustra come toouse hello toocreate CLI di Azure (azure.js) un hub IoT.

È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

* CLI di Azure (azure.js): hello CLI per hello classic e modelli di distribuzione di gestione di risorse come descritto in questo articolo.
* [Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) -hello prossima generazione CLI per modello di distribuzione di gestione risorse hello.

toocomplete questa esercitazione, è necessario hello seguenti:

* Un account Azure attivo. Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.
* [Interfaccia della riga di comando di Azure 0.10.4][lnk-CLI-install] o versione successiva. Se si dispone già di hello Azure CLI installato, è possibile convalidare una versione corrente di hello al prompt dei comandi di hello con hello comando seguente:

```azurecli
azure --version
```

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [modello di distribuzione classica e Azure Resource Manager](../azure-resource-manager/resource-manager-deployment-model.md). Hello CLI di Azure deve essere in modalità di gestione risorse di Azure:
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a>Impostare l'account e la sottoscrizione di Azure

1. Al prompt dei comandi di hello, account di accesso digitando hello il comando seguente:

   ```azurecli
    azure login
   ```

   Utilizzare hello suggeriti i web browser e tooauthenticate di codice.
1. Se si dispone di più sottoscrizioni di Azure, la connessione tooAzure consenta l'accesso tooall hello le sottoscrizioni di Azure associate con le credenziali. È possibile visualizzare le sottoscrizioni di Azure hello e consente di identificare quello predefinito di hello, utilizzando il comando di hello:

   ```azurecli
    azure account list
   ```

   contesto di tooset hello sottoscrizione in cui si desidera utilizzare comandi hello restanti hello toorun:

   ```azurecli
    azure account set <subscription name>
   ```

1. Se non si dispone di un gruppo di risorse, è possibile crearne uno denominato **exampleResourceGroup**:

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> articolo Hello [toomanage CLI di Azure hello Azure usare risorse e gruppi di risorse] [ lnk-CLI-arm] fornisce ulteriori informazioni su come toouse hello Azure CLI toomanage Azure le risorse.

## <a name="create-an-iot-hub"></a>Creare un hub IoT

Parametri obbligatori:

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* **resource-group**. nome del gruppo di risorse Hello. formato Hello viene fatta distinzione tra maiuscole e minuscole caratteri alfanumerici, caratteri di sottolineatura e trattini, lunghezza di 1 a 64.
* **name**. nome Hello di hello IoT hub toobe creato. formato Hello viene fatta distinzione tra maiuscole e minuscole caratteri alfanumerici, caratteri di sottolineatura e trattino, lunghezza 3-50.
* **location**. Hello percorso (area o Data Center di azure) tooprovision hello hub IoT.
* **sku-name**. nome Hello dello sku di hello, uno di: [F1, S1, S2, S3]. Per l'elenco completo più recente hello, consultare toohello pagina dei prezzi per l'IoT Hub.
* **units**. numero di Hello di unità sottoposte a provisioning. Intervallo: F1 [1-1] : S1, S2 [1-200] : S3 [1-10]. Unità di IoT Hub sono basate sul numero totale di messaggi hello e di conteggio dei dispositivi desiderato tooconnect.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

toosee tutti hello parametri disponibili per la creazione, è possibile utilizzare il comando di help hello nel prompt dei comandi:

```azurecli
azure iothub create -h
```

Esempio semplice: chiamato di un IoT Hub toocreate **exampleIoTHubName** nel gruppo di risorse hello **exampleResourceGroup**, eseguire hello il seguente comando:

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> Attraverso questo comando dell'interfaccia della riga di comando di Azure viene creato un hub IoT S1 Standard che viene addebitato. È possibile eliminare l'hub IoT hello **exampleIoTHubName** tramite il seguente comando:
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a>Passaggi successivi

toolearn più sullo sviluppo per l'IoT Hub, vedere l'articolo seguente hello:

* [IoT SDKs][lnk-sdks] (SDK di IoT)

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Utilizzo di hello toomanage portale Azure IoT Hub][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
