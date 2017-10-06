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
# <a name="explore-azure-iot-edge-architecture-on-windows"></a><span data-ttu-id="47b56-103">Esplorare l'architettura di Azure IoT Edge in Windows</span><span class="sxs-lookup"><span data-stu-id="47b56-103">Explore Azure IoT Edge architecture on Windows</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="47b56-104">Come toorun hello esempio</span><span class="sxs-lookup"><span data-stu-id="47b56-104">How toorun hello sample</span></span>

<span data-ttu-id="47b56-105">Hello **build.cmd** script genera l'output di hello **compilare** cartella nella copia locale di hello **iot edge** repository.</span><span class="sxs-lookup"><span data-stu-id="47b56-105">hello **build.cmd** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="47b56-106">Questo output include hello due IoT Edge moduli utilizzati in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="47b56-106">This output includes hello two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="47b56-107">posizioni di script di compilazione Hello **logger.dll** in hello **compilare\\moduli\\logger\\Debug** cartella e **hello\_world.dll**  in hello **compilare\\moduli\\hello_world\\Debug** cartella.</span><span class="sxs-lookup"><span data-stu-id="47b56-107">hello build script places **logger.dll** in hello **build\\modules\\logger\\Debug** folder and **hello\_world.dll** in hello **build\\modules\\hello_world\\Debug** folder.</span></span> <span data-ttu-id="47b56-108">Usare questi percorsi per hello **percorso modulo** valori come illustrato nel seguente file di impostazioni JSON hello.</span><span class="sxs-lookup"><span data-stu-id="47b56-108">Use these paths for hello **module path** values as shown in hello following JSON settings file.</span></span>

<span data-ttu-id="47b56-109">hello Hello\_world\_esempio dura hello percorso tooa file di configurazione JSON come argomento della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="47b56-109">hello hello\_world\_sample process takes hello path tooa JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="47b56-110">Hello file JSON di esempio seguente viene fornito nel repository SDK hello in **esempi\\hello\_world\\src\\hello\_world\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="47b56-110">hello following example JSON file is provided in hello SDK repository at **samples\\hello\_world\\src\\hello\_world\_win.json**.</span></span> <span data-ttu-id="47b56-111">Questo funzionamento di file della configurazione come se non si modifica hello compilare hello tooplace script IoT Edge moduli o file eseguibili presenti in percorsi non predefiniti di esempio.</span><span class="sxs-lookup"><span data-stu-id="47b56-111">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="47b56-112">percorsi dei moduli Hello sono toohello relativa directory dove hello hello\_world\_sample.exe si trova.</span><span class="sxs-lookup"><span data-stu-id="47b56-112">hello module paths are relative toohello directory where hello hello\_world\_sample.exe is located.</span></span> <span data-ttu-id="47b56-113">esempio Hello JSON configurazione file predefinite toowriting 'txt' nella directory di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="47b56-113">hello sample JSON configuration file defaults toowriting 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="47b56-114">Passare toohello **compilare** cartella nella radice di hello della copia locale di hello **iot edge** repository.</span><span class="sxs-lookup"><span data-stu-id="47b56-114">Navigate toohello **build** folder in hello root of your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="47b56-115">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="47b56-115">Run hello following command:</span></span>

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
