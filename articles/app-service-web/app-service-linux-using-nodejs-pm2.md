---
title: Uso della configurazione PM2 per Node.js in App Web di Azure su Linux | Microsoft Docs
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
ms.openlocfilehash: 5002400a673e2c5cc4290bab488b839fb2282966
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a><span data-ttu-id="2a7f6-104">Usare la configurazione PM2 per Node.js in App Web di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="2a7f6-104">Use PM2 configuration for Node.js in Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="2a7f6-105">Se si imposta lo stack di applicazioni su Node.js per App Web di Azure in Linux, è possibile ottenere l'opzione per impostare un file di avvio in Node.js, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="2a7f6-105">If you set the application stack to Node.js for Azure Web App on Linux, you get the option to set a Node.js startup file as shown in the following image:</span></span>

![Impostare un file di avvio Node.js][1]

<span data-ttu-id="2a7f6-107">È possibile usare questa opzione per una delle attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a7f6-107">You can use this option to do one of the following tasks:</span></span>

* <span data-ttu-id="2a7f6-108">Specificare lo script di avvio per l'app Node.js (ad esempio: /bin/server.js).</span><span class="sxs-lookup"><span data-stu-id="2a7f6-108">Specify the startup script for your Node.js app (for example: /bin/server.js).</span></span>
* <span data-ttu-id="2a7f6-109">Specificare il file di configurazione PM2 da usare per l'app Node.js (ad esempio: /foo/process.json).</span><span class="sxs-lookup"><span data-stu-id="2a7f6-109">Specify the PM2 configuration file to use for your Node.js app (for example: /foo/process.json).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="2a7f6-110">Per riavviare automaticamente i processi Node.js quando vengono modificati determinati file, usare la configurazione PM2.</span><span class="sxs-lookup"><span data-stu-id="2a7f6-110">If you want your Node.js processes to restart automatically when certain files are modified, use the PM2 configuration.</span></span> <span data-ttu-id="2a7f6-111">In caso contrario, l'applicazione non verrà riavviata quando riceve notifiche di modifica, ad esempio quando viene modificato il codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2a7f6-111">Otherwise, your application won't restart when it receives change notifications (for example, when your application code changes).</span></span>
  > 
  > 

<span data-ttu-id="2a7f6-112">È possibile vedere la [documentazione del file di processo](http://pm2.keymetrics.io/docs/usage/application-declaration/) per tutte le opzioni. Il seguente è un esempio di codice che è possibile usare come file process.json:</span><span class="sxs-lookup"><span data-stu-id="2a7f6-112">You can check the Node.js [process file documentation](http://pm2.keymetrics.io/docs/usage/application-declaration/) for all the options, but following is a sample of what you can use as your process.json file:</span></span>

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

<span data-ttu-id="2a7f6-113">In questa configurazione è importante notare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="2a7f6-113">Important things to note in this configuration are:</span></span>

* <span data-ttu-id="2a7f6-114">La proprietà "script" specifica lo script di avvio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2a7f6-114">The "script" property specifies your application's start script.</span></span>
* <span data-ttu-id="2a7f6-115">La proprietà "instances" specifica quante istanze del processo del nodo avviare.</span><span class="sxs-lookup"><span data-stu-id="2a7f6-115">The "instances" property specifies how many instances of the node process to launch.</span></span> <span data-ttu-id="2a7f6-116">Se si esegue l'applicazione in VM di dimensioni maggiori con più core, è consigliabile ottimizzare le risorse impostando un valore più elevato qui.</span><span class="sxs-lookup"><span data-stu-id="2a7f6-116">If you are running your application on larger VMs that have multiple cores, it's a good idea to maximize your resources by setting a higher value here.</span></span>
* <span data-ttu-id="2a7f6-117">La matrice "watch" specifica tutti i file per cui si vuole riavviare il processo del nodo quando vengono modificati.</span><span class="sxs-lookup"><span data-stu-id="2a7f6-117">The "watch" array specifies all files that you want to restart the node process for when they change.</span></span>
* <span data-ttu-id="2a7f6-118">Per "watch_options", attualmente è necessario impostare "usePolling" su true a causa del modo in cui viene montato il contenuto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2a7f6-118">For the "watch_options", you currently need to specify "usePolling" as true because of the way your application content is mounted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a7f6-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2a7f6-119">Next steps</span></span>
* [<span data-ttu-id="2a7f6-120">Definizione di App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="2a7f6-120">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="2a7f6-121">Domande frequenti su App Web del Servizio app di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="2a7f6-121">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
