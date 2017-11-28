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
# <a name="explore-azure-iot-edge-architecture-on-linux"></a><span data-ttu-id="81d44-103">Esplorare l'architettura di Azure IoT Edge in Linux</span><span class="sxs-lookup"><span data-stu-id="81d44-103">Explore Azure IoT Edge architecture on Linux</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="81d44-104">Come toorun hello esempio</span><span class="sxs-lookup"><span data-stu-id="81d44-104">How toorun hello sample</span></span>

<span data-ttu-id="81d44-105">Hello **build.sh** script genera l'output di hello **compilare** cartella nella copia locale di hello **iot edge** repository.</span><span class="sxs-lookup"><span data-stu-id="81d44-105">hello **build.sh** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="81d44-106">Questo output include hello due IoT Edge moduli utilizzati in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="81d44-106">This output includes hello two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="81d44-107">posizioni di script di compilazione Hello **liblogger.so** in hello **compilazione/moduli/logger/** cartella e **libhello\_world.so** in hello **compilare / imoduli/hello_world/** cartella.</span><span class="sxs-lookup"><span data-stu-id="81d44-107">hello build script places **liblogger.so** in hello **build/modules/logger/** folder and **libhello\_world.so** in hello **build/modules/hello_world/** folder.</span></span> <span data-ttu-id="81d44-108">Usare questi percorsi per hello **percorso modulo** valori come illustrato nel seguente file di impostazioni JSON di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="81d44-108">Use these paths for hello **module path** values as shown in hello following example JSON settings file.</span></span>

<span data-ttu-id="81d44-109">hello Hello\_world\_processo esempio accetta file di configurazione JSON tooa percorso hello un argomento della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="81d44-109">hello hello\_world\_sample process takes hello path tooa JSON configuration file a command-line argument.</span></span> <span data-ttu-id="81d44-110">Hello file JSON di esempio seguente viene fornito nel repository SDK hello in **esempi/hello\_src/ambiente/hello\_world\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="81d44-110">hello following example JSON file is provided in hello SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span></span> <span data-ttu-id="81d44-111">Questo funzionamento di file della configurazione come se non si modifica hello compilare hello tooplace script IoT Edge moduli o file eseguibili presenti in percorsi non predefiniti di esempio.</span><span class="sxs-lookup"><span data-stu-id="81d44-111">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="81d44-112">percorsi dei moduli Hello sono toohello relativa directory di lavoro corrente da cui hello hello\_world\_viene avviato l'eseguibile dell'esempio, non hello directory in cui si trova hello eseguibile.</span><span class="sxs-lookup"><span data-stu-id="81d44-112">hello module paths are relative toohello current working directory from where hello hello\_world\_sample executable is launched, not hello directory where hello executable is located.</span></span> <span data-ttu-id="81d44-113">esempio Hello JSON configurazione file predefinite toowriting 'txt' nella directory di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="81d44-113">hello sample JSON configuration file defaults toowriting 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="81d44-114">Passare toohello **compilare** cartella nella radice di hello della copia locale di hello **iot edge** repository.</span><span class="sxs-lookup"><span data-stu-id="81d44-114">Navigate toohello **build** folder in hello root of your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="81d44-115">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="81d44-115">Run hello following command:</span></span>

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

