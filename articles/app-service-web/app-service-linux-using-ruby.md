---
title: aaaUsing Ruby in App Azure del servizio Web App in Linux | Documenti Microsoft
description: Uso di Ruby in App Web del Servizio app di Azure in Linux.
keywords: Servizio app di Azure, app Web, domande frequenti, Linux, OSS, Ruby
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 45692cb3bf1da9ff65b9466055029bfaef8b7d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="5be2d-104">Uso di Ruby in App Web in Linux</span><span class="sxs-lookup"><span data-stu-id="5be2d-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="5be2d-105">Con hello più recente aggiornamento tooour back-end, è stato introdotto il supporto per v.2.3 Ruby.</span><span class="sxs-lookup"><span data-stu-id="5be2d-105">With hello latest update tooour backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="5be2d-106">Impostazione di configurazione hello dell'app web Linux, è possibile modificare stack dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5be2d-106">By setting hello configuration of your Linux web app, you can change hello application stack.</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="5be2d-107">Utilizzo di hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5be2d-107">Using hello Azure portal</span></span> ##

<span data-ttu-id="5be2d-108">Menu nuovo di hello di hello [portale di Azure](https://portal.azure.com), è possibile scegliere toocreate un'App Web in Linux da hello Web + opzione cellulare come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="5be2d-108">From hello new menu in hello [Azure portal](https://portal.azure.com), you can choose toocreate a Web App on Linux from hello Web + Mobile option as shown in hello following image:</span></span>

![Avviare la creazione di un'app web nel portale di Azure hello][1]

<span data-ttu-id="5be2d-110">Successivamente, hello **pannello Crea** verrà visualizzata come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="5be2d-110">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![pannello Crea Hello][2]

1. <span data-ttu-id="5be2d-112">Assegnare all'app Web un nome.</span><span class="sxs-lookup"><span data-stu-id="5be2d-112">Give your web app a name.</span></span>
2. <span data-ttu-id="5be2d-113">Scegliere un gruppo di risorse esistente oppure crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="5be2d-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="5be2d-114">(Vedere le aree disponibili in hello [sezione limitazioni](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="5be2d-114">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="5be2d-115">Scegliere un piano di servizio app di Azure esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="5be2d-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="5be2d-116">(Vedere le note di piano di servizio App in hello [sezione limitazioni](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="5be2d-116">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="5be2d-117">Scegliere gli stack di Runtime incorporata hello hello Ruby.</span><span class="sxs-lookup"><span data-stu-id="5be2d-117">Choose hello Ruby from hello Built-in Runtime stacks.</span></span>

<span data-ttu-id="5be2d-118">Dopo aver creato l'app web Ruby, è possibile distribuire tooit utilizzando Git o FTP.</span><span class="sxs-lookup"><span data-stu-id="5be2d-118">After your Ruby web app gets created, you can deploy tooit using Git or FTP.</span></span>

<span data-ttu-id="5be2d-119">toolearn altre informazioni sulla creazione di un'app Ruby, controllare hello [Guida introduttiva get](app-service-linux-ruby-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="5be2d-119">toolearn more about creating a Ruby app, check hello [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5be2d-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5be2d-120">Next steps</span></span>
* [<span data-ttu-id="5be2d-121">Definizione di App Web in Linux</span><span class="sxs-lookup"><span data-stu-id="5be2d-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="5be2d-122">TooAzure distribuzione Git locale del servizio App</span><span class="sxs-lookup"><span data-stu-id="5be2d-122">Local Git Deployment tooAzure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="5be2d-123">Domande frequenti su App Web del Servizio app di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="5be2d-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="5be2d-124">Creare un'app Ruby con App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="5be2d-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png