---
title: Uso di Ruby in App Web del Servizio app di Azure in Linux | Microsoft Docs
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
ms.openlocfilehash: 56105d1bc153e552e12c0c408c8f6075e4eff9d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="40dd4-104">Uso di Ruby in App Web in Linux</span><span class="sxs-lookup"><span data-stu-id="40dd4-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="40dd4-105">Con l'aggiornamento più recente al back-end è stato aggiunto il supporto per Ruby v.2.3.</span><span class="sxs-lookup"><span data-stu-id="40dd4-105">With the latest update to our backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="40dd4-106">Definendo la configurazione dell'app Web Linux è possibile modificare lo stack di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="40dd4-106">By setting the configuration of your Linux web app, you can change the application stack.</span></span>

## <a name="using-the-azure-portal"></a><span data-ttu-id="40dd4-107">Uso del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="40dd4-107">Using the Azure portal</span></span> ##

<span data-ttu-id="40dd4-108">Dal menu Nuovo nel [portale di Azure](https://portal.azure.com), è possibile scegliere di creare un'app Web in Linux dall'opzione Web e dispositivi mobili come illustrato nella figura seguente:</span><span class="sxs-lookup"><span data-stu-id="40dd4-108">From the new menu in the [Azure portal](https://portal.azure.com), you can choose to create a Web App on Linux from the Web + Mobile option as shown in the following image:</span></span>

![Avviare la creazione di un'app Web nel portale di Azure][1]

<span data-ttu-id="40dd4-110">Viene quindi aperto il **pannello Crea**, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="40dd4-110">Next, the **Create blade** opens as shown in the following image:</span></span>

![Pannello Crea][2]

1. <span data-ttu-id="40dd4-112">Assegnare all'app Web un nome.</span><span class="sxs-lookup"><span data-stu-id="40dd4-112">Give your web app a name.</span></span>
2. <span data-ttu-id="40dd4-113">Scegliere un gruppo di risorse esistente oppure crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="40dd4-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="40dd4-114">Vedere le aree disponibili nella [sezione sulle limitazioni](app-service-linux-intro.md).</span><span class="sxs-lookup"><span data-stu-id="40dd4-114">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="40dd4-115">Scegliere un piano di servizio app di Azure esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="40dd4-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="40dd4-116">Vedere le note sul piano di servizio app nella [sezione sulle limitazioni](app-service-linux-intro.md).</span><span class="sxs-lookup"><span data-stu-id="40dd4-116">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="40dd4-117">Scegliere Ruby tra gli stack di runtime predefiniti.</span><span class="sxs-lookup"><span data-stu-id="40dd4-117">Choose the Ruby from the Built-in Runtime stacks.</span></span>

<span data-ttu-id="40dd4-118">Dopo aver creato un'applicazione Web Ruby, è possibile distribuirla tramite Git o FTP.</span><span class="sxs-lookup"><span data-stu-id="40dd4-118">After your Ruby web app gets created, you can deploy to it using Git or FTP.</span></span>

<span data-ttu-id="40dd4-119">Per altre informazioni sulla creazione di un'app Ruby, vedere la [guida introduttiva](app-service-linux-ruby-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="40dd4-119">To learn more about creating a Ruby app, check the [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="40dd4-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="40dd4-120">Next steps</span></span>
* [<span data-ttu-id="40dd4-121">Definizione di App Web in Linux</span><span class="sxs-lookup"><span data-stu-id="40dd4-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="40dd4-122">Distribuzione dell'archivio Git locale nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="40dd4-122">Local Git Deployment to Azure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="40dd4-123">Domande frequenti su App Web del Servizio app di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="40dd4-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="40dd4-124">Creare un'app Ruby con App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="40dd4-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png