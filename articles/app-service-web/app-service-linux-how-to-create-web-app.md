---
title: Creare un'app Web di Azure eseguita in Linux | Documentazione Microsoft
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
ms.openlocfilehash: 49091d4a85bed23927850f9c0bbc5ea8b6e8c9e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="568ef-104">Creare un'app Web di Azure eseguita in Linux</span><span class="sxs-lookup"><span data-stu-id="568ef-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-the-azure-portal-to-create-your-web-app"></a><span data-ttu-id="568ef-105">Usare il portale di Azure per creare l'app Web</span><span class="sxs-lookup"><span data-stu-id="568ef-105">Use the Azure portal to create your web app</span></span>
<span data-ttu-id="568ef-106">È possibile avviare la creazione dell'app Web in Linux dal [portale di Azure](https://portal.azure.com), come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="568ef-106">You can start creating your web app on Linux from the [Azure portal](https://portal.azure.com) as shown in the following image:</span></span>

![Avviare la creazione di un'app Web nel portale di Azure][1]

<span data-ttu-id="568ef-108">Viene quindi aperto il **pannello Crea**, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="568ef-108">Next, the **Create blade** opens as shown in the following image:</span></span>

![Pannello Crea][2]

1. <span data-ttu-id="568ef-110">Assegnare all'app Web un nome.</span><span class="sxs-lookup"><span data-stu-id="568ef-110">Give your web app a name.</span></span>
2. <span data-ttu-id="568ef-111">Scegliere un gruppo di risorse esistente oppure crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="568ef-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="568ef-112">Vedere le aree disponibili nella [sezione sulle limitazioni](app-service-linux-intro.md).</span><span class="sxs-lookup"><span data-stu-id="568ef-112">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="568ef-113">Scegliere un piano di servizio app di Azure esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="568ef-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="568ef-114">Vedere le note sul piano di servizio app nella [sezione sulle limitazioni](app-service-linux-intro.md).</span><span class="sxs-lookup"><span data-stu-id="568ef-114">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="568ef-115">Scegliere lo stack di applicazioni che si intende da usare.</span><span class="sxs-lookup"><span data-stu-id="568ef-115">Choose the application stack that you intend to use.</span></span> <span data-ttu-id="568ef-116">È possibile scegliere tra diverse versioni di Node.js, PHP, .Net Core e Ruby.</span><span class="sxs-lookup"><span data-stu-id="568ef-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="568ef-117">Dopo avere creato l'app, è possibile cambiare lo stack di applicazioni dalle impostazioni dell'applicazione, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="568ef-117">Once you have created the app, you can change the application stack from the application settings as shown in the following image:</span></span>

![Impostazioni dell'applicazione][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="568ef-119">Distribuire l'app Web</span><span class="sxs-lookup"><span data-stu-id="568ef-119">Deploy your web app</span></span>
<span data-ttu-id="568ef-120">Scegliendo le **opzioni di distribuzione** dal portale di gestione è possibile usare un repository Git o GitHub locale per distribuire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="568ef-120">Choosing **deployment options** from the management portal gives you the option to use local Git or GitHub repository to deploy your application.</span></span> <span data-ttu-id="568ef-121">Le istruzioni rimanenti sono analoghe a quelle per un'app Web non Linux.</span><span class="sxs-lookup"><span data-stu-id="568ef-121">The rest of the instructions are similar to those for a non-Linux web app.</span></span> <span data-ttu-id="568ef-122">Per distribuire l'app, è possibile seguire le istruzioni indicate nella [distribuzione Git locale](app-service-deploy-local-git.md) o nella [distribuzione continua](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="568ef-122">You can follow the instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) to deploy your app.</span></span>

<span data-ttu-id="568ef-123">È anche possibile usare l'FTP per caricare l'applicazione nel sito.</span><span class="sxs-lookup"><span data-stu-id="568ef-123">You can also use FTP to upload your application to your site.</span></span> <span data-ttu-id="568ef-124">È possibile ottenere l'endpoint FTP per l'app Web dalla sezione Log di diagnostica, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="568ef-124">You can get the FTP endpoint for your web app from the diagnostics logs section as shown in the following image:</span></span>

![Log di diagnostica][4]

## <a name="next-steps"></a><span data-ttu-id="568ef-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="568ef-126">Next steps</span></span>
* [<span data-ttu-id="568ef-127">Definizione di App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="568ef-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="568ef-128">Uso della configurazione PM2 per Node.js in App Web su Linux</span><span class="sxs-lookup"><span data-stu-id="568ef-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="568ef-129">Uso di Ruby in App Web del Servizio app di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="568ef-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="568ef-130">Domande frequenti su App Web del Servizio app di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="568ef-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
