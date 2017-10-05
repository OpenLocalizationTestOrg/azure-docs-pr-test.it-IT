---
title: Introduzione ad Azure IoT Edge (Windows) | Microsoft Docs
description: Come creare un gateway di Azure IoT Edge in un computer Windows e ottenere informazioni sui concetti chiave in Azure IoT Edge, ad esempio moduli e file di configurazione di JSON.
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
ms.openlocfilehash: 5db39bab8e31a8e7026b34e72b4614b0f6f57772
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="explore-azure-iot-edge-architecture-on-windows"></a><span data-ttu-id="fe045-103">Esplorare l'architettura di Azure IoT Edge in Windows</span><span class="sxs-lookup"><span data-stu-id="fe045-103">Explore Azure IoT Edge architecture on Windows</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="fe045-104">Per eseguire l'esempio</span><span class="sxs-lookup"><span data-stu-id="fe045-104">How to run the sample</span></span>

<span data-ttu-id="fe045-105">Lo script **build.cmd** genera l'output nella cartella **build** nella copia locale dell'archivio **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="fe045-105">The **build.cmd** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="fe045-106">Questo output include anche i due moduli di IoT Edge usati in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="fe045-106">This output includes the two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="fe045-107">Lo script di compilazione inserisce **logger.dll** nella cartella **build\\modules\\logger\\Debug** e **hello\_world.dll** nella cartella **build\\modules\\hello_world\\Debug**.</span><span class="sxs-lookup"><span data-stu-id="fe045-107">The build script places **logger.dll** in the **build\\modules\\logger\\Debug** folder and **hello\_world.dll** in the **build\\modules\\hello_world\\Debug** folder.</span></span> <span data-ttu-id="fe045-108">Usare questi percorsi per i valori **module path**, come illustrato nel file di impostazioni JSON seguente.</span><span class="sxs-lookup"><span data-stu-id="fe045-108">Use these paths for the **module path** values as shown in the following JSON settings file.</span></span>

<span data-ttu-id="fe045-109">Il processo hello\_world\_sample accetta il percorso di un file di configurazione JSON come argomento della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="fe045-109">The hello\_world\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="fe045-110">Il file JSON di esempio seguente è disponibile nel repository dell'SDK in **samples\\hello\_world\\src\\hello\_world\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="fe045-110">The following example JSON file is provided in the SDK repository at **samples\\hello\_world\\src\\hello\_world\_win.json**.</span></span> <span data-ttu-id="fe045-111">Questo file di configurazione funziona così com'è, a meno che non si modifichi lo script di compilazione per inserire moduli di IoT Edge o file eseguibili di esempio in percorsi non predefiniti.</span><span class="sxs-lookup"><span data-stu-id="fe045-111">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="fe045-112">I percorsi dei moduli sono relativi alla directory in cui si trova il file hello\_world\_sample.exe.</span><span class="sxs-lookup"><span data-stu-id="fe045-112">The module paths are relative to the directory where the hello\_world\_sample.exe is located.</span></span> <span data-ttu-id="fe045-113">Per impostazione predefinita, il file di configurazione JSON di esempio prevede la scrittura del file "log.txt" nella directory di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="fe045-113">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="fe045-114">Accedere alla cartella **build** nella radice della copia locale dell'archivio **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="fe045-114">Navigate to the **build** folder in the root of your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="fe045-115">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fe045-115">Run the following command:</span></span>

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
