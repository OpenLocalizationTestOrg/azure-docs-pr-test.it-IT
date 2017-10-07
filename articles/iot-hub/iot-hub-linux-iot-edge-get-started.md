---
title: aaaGet avviato con Azure IoT Edge (Linux) | Documenti Microsoft
description: Come toobuild un gateway in Linux del computer e avere informazioni sui concetti chiave di Azure IoT bordo, ad esempio moduli e i file di configurazione JSON.
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: cf537bdd-2352-4bb1-96cd-a283fcd3d6cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40aa9c8ddca6a974c361cbb0b453c7d0ddc71b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-linux"></a>Esplorare l'architettura di Azure IoT Edge in Linux

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a>Come toorun hello esempio

Hello **build.sh** script genera l'output di hello **compilare** cartella nella copia locale di hello **iot edge** repository. Questo output include hello due IoT Edge moduli utilizzati in questo esempio.

posizioni di script di compilazione Hello **liblogger.so** in hello **compilazione/moduli/logger/** cartella e **libhello\_world.so** in hello **compilare / imoduli/hello_world/** cartella. Usare questi percorsi per hello **percorso modulo** valori come illustrato nel seguente file di impostazioni JSON di esempio hello.

hello Hello\_world\_processo esempio accetta file di configurazione JSON tooa percorso hello un argomento della riga di comando. Hello file JSON di esempio seguente viene fornito nel repository SDK hello in **esempi/hello\_src/ambiente/hello\_world\_lin.json**. Questo funzionamento di file della configurazione come se non si modifica hello compilare hello tooplace script IoT Edge moduli o file eseguibili presenti in percorsi non predefiniti di esempio.

> [!NOTE]
> percorsi dei moduli Hello sono toohello relativa directory di lavoro corrente da cui hello hello\_world\_viene avviato l'eseguibile dell'esempio, non hello directory in cui si trova hello eseguibile. esempio Hello JSON configurazione file predefinite toowriting 'txt' nella directory di lavoro corrente.

```json
{
    "modules" :
    [
        {
            "name" : "logger",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args" : {"filename":"log.txt"}
        },
        {
            "name" : "hello_world",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/hello_world/libhello_world.so"
            }
            },
            "args" : null
        }
    ],
    "links":
    [
        {
            "source": "hello_world",
            "sink": "logger"
        }
    ]
}
```

1. Passare toohello **compilare** cartella nella radice di hello della copia locale di hello **iot edge** repository.

1. Eseguire hello comando seguente:

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

