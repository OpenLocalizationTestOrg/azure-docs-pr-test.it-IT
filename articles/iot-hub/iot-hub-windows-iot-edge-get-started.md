---
title: aaaGet avviato con bordo IoT di Azure (Windows) | Documenti Microsoft
description: Come toobuild un gateway Azure IoT in un Windows del computer e avere informazioni sui concetti chiave di Azure IoT bordo, ad esempio moduli e i file di configurazione JSON.
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 9aff3724-5e4e-40ec-b95a-d00df4f590c5
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5dd13cbfc02eeb55d9f2dbffca5021f2624acf14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-windows"></a>Esplorare l'architettura di Azure IoT Edge in Windows

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a>Come toorun hello esempio

Hello **build.cmd** script genera l'output di hello **compilare** cartella nella copia locale di hello **iot edge** repository. Questo output include hello due IoT Edge moduli utilizzati in questo esempio.

posizioni di script di compilazione Hello **logger.dll** in hello **compilare\\moduli\\logger\\Debug** cartella e **hello\_world.dll**  in hello **compilare\\moduli\\hello_world\\Debug** cartella. Usare questi percorsi per hello **percorso modulo** valori come illustrato nel seguente file di impostazioni JSON hello.

hello Hello\_world\_esempio dura hello percorso tooa file di configurazione JSON come argomento della riga di comando. Hello file JSON di esempio seguente viene fornito nel repository SDK hello in **esempi\\hello\_world\\src\\hello\_world\_win.json**. Questo funzionamento di file della configurazione come se non si modifica hello compilare hello tooplace script IoT Edge moduli o file eseguibili presenti in percorsi non predefiniti di esempio.

> [!NOTE]
> percorsi dei moduli Hello sono toohello relativa directory dove hello hello\_world\_sample.exe si trova. esempio Hello JSON configurazione file predefinite toowriting 'txt' nella directory di lavoro corrente.

```json
{
  "modules": [
    {
      "name": "logger",
      "loader": {
        "name": "native",
        "entrypoint": {
          "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
        }
      },
      "args": { "filename": "log.txt" }
    },
    {
      "name": "hello_world",
      "loader": {
        "name": "native",
        "entrypoint": {
          "module.path": "..\\..\\..\\modules\\hello_world\\Debug\\hello_world.dll"
        }
      },
      "args": null
      }
  ],
  "links": [
    {
      "source": "hello_world",
      "sink": "logger"
    }
  ]
}
```

1. Passare toohello **compilare** cartella nella radice di hello della copia locale di hello **iot edge** repository.

1. Eseguire hello comando seguente:

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
