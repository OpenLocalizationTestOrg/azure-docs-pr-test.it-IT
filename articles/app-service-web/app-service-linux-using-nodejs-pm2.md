---
title: configurazione aaaUsing PM2 per Node.js in Azure Web App in Linux | Documenti Microsoft
description: Uso della configurazione PM2 per Node.js in App Web di Azure su Linux
keywords: Servizio app di Azure, app Web, nodejs, PM2, Linux, OSS
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: fb420f32-6d74-49c7-992f-0ed5616e66e7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 923783ffe656e01c43318899d1a656b553ebb5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a><span data-ttu-id="767d6-104">Usare la configurazione PM2 per Node.js in App Web di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="767d6-104">Use PM2 configuration for Node.js in Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="767d6-105">Se si imposta hello applicazione stack tooNode.js per l'App Web di Azure in Linux, viene visualizzato hello opzione tooset un file di avvio Node.js come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="767d6-105">If you set hello application stack tooNode.js for Azure Web App on Linux, you get hello option tooset a Node.js startup file as shown in hello following image:</span></span>

![Impostare un file di avvio Node.js][1]

<span data-ttu-id="767d6-107">È possibile utilizzare questa opzione toodo uno di hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="767d6-107">You can use this option toodo one of hello following tasks:</span></span>

* <span data-ttu-id="767d6-108">Specificare uno script di avvio hello per l'app Node.js (ad esempio: /bin/server.js).</span><span class="sxs-lookup"><span data-stu-id="767d6-108">Specify hello startup script for your Node.js app (for example: /bin/server.js).</span></span>
* <span data-ttu-id="767d6-109">Specificare toouse di file di configurazione di hello PM2 per l'app Node.js (ad esempio: /foo/process.json).</span><span class="sxs-lookup"><span data-stu-id="767d6-109">Specify hello PM2 configuration file toouse for your Node.js app (for example: /foo/process.json).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="767d6-110">Se si desidera il toorestart processi Node.js automaticamente quando vengono modificate di determinati file, utilizzare configurazione PM2 hello.</span><span class="sxs-lookup"><span data-stu-id="767d6-110">If you want your Node.js processes toorestart automatically when certain files are modified, use hello PM2 configuration.</span></span> <span data-ttu-id="767d6-111">In caso contrario, l'applicazione non verrà riavviata quando riceve notifiche di modifica, ad esempio quando viene modificato il codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="767d6-111">Otherwise, your application won't restart when it receives change notifications (for example, when your application code changes).</span></span>
  > 
  > 

<span data-ttu-id="767d6-112">È possibile controllare hello Node.js [elaborare documentazione file](http://pm2.keymetrics.io/docs/usage/application-declaration/) per tutte le opzioni di hello, ma di seguito è riportato un esempio di ciò che è possibile utilizzare come file di process.json:</span><span class="sxs-lookup"><span data-stu-id="767d6-112">You can check hello Node.js [process file documentation](http://pm2.keymetrics.io/docs/usage/application-declaration/) for all hello options, but following is a sample of what you can use as your process.json file:</span></span>

        {
          "name"        : "worker",
          "script"      : "./bin/server.js",
          "instances"   : 1,
          "merge_logs"  : true,
          "log_date_format" : "YYYY-MM-DD HH:mm Z",
          "watch": ["./bin/server.js", "foo.txt"],
          "watch_options": {
            "followSymlinks": true,
            "usePolling"   : true,
            "interval"    : 5
          }
        }

<span data-ttu-id="767d6-113">Toonote aspetti importanti in questa configurazione sono:</span><span class="sxs-lookup"><span data-stu-id="767d6-113">Important things toonote in this configuration are:</span></span>

* <span data-ttu-id="767d6-114">proprietà "script" Hello specifica script di avvio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="767d6-114">hello "script" property specifies your application's start script.</span></span>
* <span data-ttu-id="767d6-115">proprietà di "instances" Hello specifica il numero di istanze di hello nodo processo toolaunch.</span><span class="sxs-lookup"><span data-stu-id="767d6-115">hello "instances" property specifies how many instances of hello node process toolaunch.</span></span> <span data-ttu-id="767d6-116">Se si esegue l'applicazione in macchine virtuali di dimensioni maggiori con più core, è una buona idea toomaximize delle risorse impostando un valore più alto qui.</span><span class="sxs-lookup"><span data-stu-id="767d6-116">If you are running your application on larger VMs that have multiple cores, it's a good idea toomaximize your resources by setting a higher value here.</span></span>
* <span data-ttu-id="767d6-117">Hello "controllo" matrice specifica tutti i file che si desidera che toorestart hello nodo processo per quando vengono modificate.</span><span class="sxs-lookup"><span data-stu-id="767d6-117">hello "watch" array specifies all files that you want toorestart hello node process for when they change.</span></span>
* <span data-ttu-id="767d6-118">Per "watch_options" hello, è attualmente necessario toospecify "usePolling" come true a causa delle modalità di hello che è montato il contenuto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="767d6-118">For hello "watch_options", you currently need toospecify "usePolling" as true because of hello way your application content is mounted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="767d6-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="767d6-119">Next steps</span></span>
* [<span data-ttu-id="767d6-120">Definizione di App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="767d6-120">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="767d6-121">Domande frequenti su App Web del Servizio app di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="767d6-121">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
