---
title: aaaCreate di Azure web app in esecuzione in Linux | Documenti Microsoft
description: Flusso di lavoro per la creazione di un'app Web per App Web di Aure in Linux.
keywords: Servizio app di Azure, app Web, Linux, OSS
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: de1bd030345d5e2a8024012067b5bcaa2cca09dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="c757e-104">Creare un'app Web di Azure eseguita in Linux</span><span class="sxs-lookup"><span data-stu-id="c757e-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a><span data-ttu-id="c757e-105">Usare l'app web di hello toocreate portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c757e-105">Use hello Azure portal toocreate your web app</span></span>
<span data-ttu-id="c757e-106">È possibile iniziare a creare app web in Linux hello [portale di Azure](https://portal.azure.com) come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="c757e-106">You can start creating your web app on Linux from hello [Azure portal](https://portal.azure.com) as shown in hello following image:</span></span>

![Avviare la creazione di un'app web nel portale di Azure hello][1]

<span data-ttu-id="c757e-108">Successivamente, hello **pannello Crea** verrà visualizzata come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="c757e-108">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![pannello Crea Hello][2]

1. <span data-ttu-id="c757e-110">Assegnare all'app Web un nome.</span><span class="sxs-lookup"><span data-stu-id="c757e-110">Give your web app a name.</span></span>
2. <span data-ttu-id="c757e-111">Scegliere un gruppo di risorse esistente oppure crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="c757e-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="c757e-112">(Vedere le aree disponibili in hello [sezione limitazioni](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="c757e-112">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="c757e-113">Scegliere un piano di servizio app di Azure esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="c757e-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="c757e-114">(Vedere le note di piano di servizio App in hello [sezione limitazioni](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="c757e-114">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="c757e-115">Scegliere un'applicazione hello stack che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="c757e-115">Choose hello application stack that you intend toouse.</span></span> <span data-ttu-id="c757e-116">È possibile scegliere tra diverse versioni di Node.js, PHP, .Net Core e Ruby.</span><span class="sxs-lookup"><span data-stu-id="c757e-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="c757e-117">Dopo aver creato l'applicazione hello, è possibile modificare stack dell'applicazione hello da impostazioni applicazione hello, come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="c757e-117">Once you have created hello app, you can change hello application stack from hello application settings as shown in hello following image:</span></span>

![Impostazioni dell'applicazione][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="c757e-119">Distribuire l'app Web</span><span class="sxs-lookup"><span data-stu-id="c757e-119">Deploy your web app</span></span>
<span data-ttu-id="c757e-120">Scelta di **opzioni di distribuzione** da offre portale di gestione hello hello opzione toouse locale Git o GitHub repository toodeploy l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c757e-120">Choosing **deployment options** from hello management portal gives you hello option toouse local Git or GitHub repository toodeploy your application.</span></span> <span data-ttu-id="c757e-121">Hello restanti istruzioni hello sono simili toothose per un'app web non Linux.</span><span class="sxs-lookup"><span data-stu-id="c757e-121">hello rest of hello instructions are similar toothose for a non-Linux web app.</span></span> <span data-ttu-id="c757e-122">È possibile seguire le istruzioni hello [distribuzione Git locale](app-service-deploy-local-git.md) o [distribuzione continua](app-service-continuous-deployment.md) toodeploy l'app.</span><span class="sxs-lookup"><span data-stu-id="c757e-122">You can follow hello instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) toodeploy your app.</span></span>

<span data-ttu-id="c757e-123">È anche possibile utilizzare tooupload FTP del sito tooyour applicazione.</span><span class="sxs-lookup"><span data-stu-id="c757e-123">You can also use FTP tooupload your application tooyour site.</span></span> <span data-ttu-id="c757e-124">È possibile ottenere endpoint FTP hello per le app web da diagnostica di hello sezione registri come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="c757e-124">You can get hello FTP endpoint for your web app from hello diagnostics logs section as shown in hello following image:</span></span>

![Log di diagnostica][4]

## <a name="next-steps"></a><span data-ttu-id="c757e-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c757e-126">Next steps</span></span>
* [<span data-ttu-id="c757e-127">Definizione di App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="c757e-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="c757e-128">Uso della configurazione PM2 per Node.js in App Web su Linux</span><span class="sxs-lookup"><span data-stu-id="c757e-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="c757e-129">Uso di Ruby in App Web del Servizio app di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="c757e-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="c757e-130">Domande frequenti su App Web del Servizio app di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="c757e-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
