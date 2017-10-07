---
title: conversione di aaaData nel gateway IoT con bordo IoT di Azure | Documenti Microsoft
description: Utilizzare IoT gateway tooconvert hello il formato di dati del sensore tramite un modulo personalizzato dal bordo IoT di Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: conversione dei dati del gateway iot, trasformazione dei dati del gateway iot
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a>Usare il gateway IoT per la trasformazione dei dati del sensore con Azure IoT Edge

> [!NOTE]
> Prima di iniziare questa esercitazione, assicurarsi di che aver completato hello seguente lezioni in sequenza:
> * [Configurare Intel NUC come gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [Utilizzare il cloud IoT gateway tooconnect operazioni toohello - SensorTag tooAzure IoT Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

Un solo scopo di un gateway Iot è tooprocess raccolti dati prima di inviarlo toohello cloud. Azure IoT Edge introduce i moduli che possono essere flusso di lavoro creati e assemblati tooform hello l'elaborazione dei dati. Un modulo riceve un messaggio, esegue un'azione su di esso e quindi spostarla per tooprocess altri moduli.

## <a name="what-you-learn"></a>Contenuto dell'esercitazione

Viene illustrato come i messaggi toocreate tooconvert un modulo da hello SensorTag in un formato diverso.

## <a name="what-you-do"></a>Operazioni da fare

* Creare un modulo tooconvert un messaggio ricevuto in formato JSON hello.
* Compilare il modulo di hello.
* Aggiungere l'applicazione di esempio hello modulo toohello BILITA dal bordo IoT di Azure.
* Eseguire l'applicazione di esempio hello.

## <a name="what-you-need"></a>Elementi necessari

* Hello seguenti esercitazioni completate in sequenza:
  * [Configurare Intel NUC come gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [Utilizzare il cloud IoT gateway tooconnect operazioni toohello - SensorTag tooAzure IoT Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* Un client SSH in esecuzione nel computer host. Si consiglia l'uso di PuTTY in Windows. Linux e macOS sono già dotati di un client SSH.
* indirizzo IP Hello e hello nome utente e password tooaccess hello gateway dal client SSH hello.
* Una connessione Internet.

## <a name="create-a-module"></a>Creare un modulo

1. Nel computer host hello, eseguire client SSH hello e toohello IoT gateway di connessione.
1. Clonare il file di origine hello del modulo di conversione hello da GitHub toohello home directory di gateway IoT hello eseguendo hello seguenti comandi:

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   Si tratta di un modulo di Azure Edge nativo scritto in linguaggio di programmazione C hello. modulo Hello converte formato hello di messaggi ricevuti in hello uno seguenti:

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a>Compilare il modulo hello

modulo hello toocompile, eseguire hello seguenti comandi:

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

Ottenere un `libmy_module.so` file dopo aver completata la compilazione hello. Prendere nota del percorso assoluto di hello di questo file.

## <a name="add-hello-module-toohello-ble-sample-application"></a>Aggiungere l'applicazione di esempio BILITA toohello hello modulo

1. Cartella di esempi di passare toohello eseguendo hello comando seguente:

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. Aprire il file di configurazione di hello eseguendo hello comando seguente:

   ```bash
   vi ble_gateway.json
   ```

1. Aggiungere un modulo inserendo hello seguente codice toohello `modules` sezione.

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. Sostituire `[Your libmy_module.so path]` nel codice hello con percorso assoluto di hello del libmy_module.so hello' file.
1. Sostituire il codice hello in hello `links` sezione con hello uno seguenti:

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. Premere `ESC`, quindi digitare `:wq` file hello toosave.

## <a name="run-hello-sample-application"></a>Eseguire l'applicazione di esempio hello

1. Accensione hello SensorTag.
1. Impostare una variabile di ambiente SSL_CERT_FILE hello eseguendo hello comando seguente:

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. Eseguire l'applicazione di esempio hello con modulo aggiunto hello eseguendo hello comando seguente:

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>Passaggi successivi

Hai correttamente utilizzare hello IoT gateway tooconvert messaggio hello da SensorTag in formato JSON hello.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
