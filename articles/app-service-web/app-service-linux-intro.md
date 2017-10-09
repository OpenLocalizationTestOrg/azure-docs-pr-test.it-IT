---
title: aaaIntroduction tooAzure App Web in Linux | Documenti Microsoft
description: Informazioni su App Web di Azure in Linux.
keywords: Servizio app di Azure, Linux, OSS
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a><span data-ttu-id="9281f-104">Introduzione tooAzure App Web in Linux</span><span class="sxs-lookup"><span data-stu-id="9281f-104">Introduction tooAzure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="9281f-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9281f-105">Overview</span></span>
<span data-ttu-id="9281f-106">I clienti possono utilizzare App Web nelle App web toohost di Linux in modo nativo in Linux per gli stack di applicazioni supportate.</span><span class="sxs-lookup"><span data-stu-id="9281f-106">Customers can use Web App on Linux toohost web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="9281f-107">Hello nella sezione seguente sono elencati gli stack di applicazione hello che sono attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="9281f-107">hello following section lists hello application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="9281f-108">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="9281f-108">Features</span></span>
<span data-ttu-id="9281f-109">Web App in Linux supporta attualmente hello stack di applicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9281f-109">Web App on Linux currently supports hello following application stacks:</span></span>

* <span data-ttu-id="9281f-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="9281f-110">Node.js</span></span>
    * <span data-ttu-id="9281f-111">4.4</span><span class="sxs-lookup"><span data-stu-id="9281f-111">4.4</span></span>
    * <span data-ttu-id="9281f-112">4.5</span><span class="sxs-lookup"><span data-stu-id="9281f-112">4.5</span></span>
    * <span data-ttu-id="9281f-113">6.2</span><span class="sxs-lookup"><span data-stu-id="9281f-113">6.2</span></span>
    * <span data-ttu-id="9281f-114">6.6</span><span class="sxs-lookup"><span data-stu-id="9281f-114">6.6</span></span>
    * <span data-ttu-id="9281f-115">6.9</span><span class="sxs-lookup"><span data-stu-id="9281f-115">6.9</span></span>
    * <span data-ttu-id="9281f-116">6.10</span><span class="sxs-lookup"><span data-stu-id="9281f-116">6.10</span></span>
    * <span data-ttu-id="9281f-117">6.11</span><span class="sxs-lookup"><span data-stu-id="9281f-117">6.11</span></span>
    * <span data-ttu-id="9281f-118">8.0</span><span class="sxs-lookup"><span data-stu-id="9281f-118">8.0</span></span>
    * <span data-ttu-id="9281f-119">8.1</span><span class="sxs-lookup"><span data-stu-id="9281f-119">8.1</span></span>
* <span data-ttu-id="9281f-120">PHP</span><span class="sxs-lookup"><span data-stu-id="9281f-120">PHP</span></span>
    * <span data-ttu-id="9281f-121">5.6</span><span class="sxs-lookup"><span data-stu-id="9281f-121">5.6</span></span>
    * <span data-ttu-id="9281f-122">7.0</span><span class="sxs-lookup"><span data-stu-id="9281f-122">7.0</span></span>
* <span data-ttu-id="9281f-123">.Net Core</span><span class="sxs-lookup"><span data-stu-id="9281f-123">.Net Core</span></span>
    * <span data-ttu-id="9281f-124">1.0</span><span class="sxs-lookup"><span data-stu-id="9281f-124">1.0</span></span>
    * <span data-ttu-id="9281f-125">1.1</span><span class="sxs-lookup"><span data-stu-id="9281f-125">1.1</span></span>
* <span data-ttu-id="9281f-126">Ruby</span><span class="sxs-lookup"><span data-stu-id="9281f-126">Ruby</span></span>
    * <span data-ttu-id="9281f-127">2.3</span><span class="sxs-lookup"><span data-stu-id="9281f-127">2.3</span></span>

<span data-ttu-id="9281f-128">I clienti possono distribuire le applicazioni tramite:</span><span class="sxs-lookup"><span data-stu-id="9281f-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="9281f-129">FTP</span><span class="sxs-lookup"><span data-stu-id="9281f-129">FTP</span></span>
* <span data-ttu-id="9281f-130">Repository Git locale</span><span class="sxs-lookup"><span data-stu-id="9281f-130">Local Git</span></span>
* <span data-ttu-id="9281f-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="9281f-131">GitHub</span></span>
* <span data-ttu-id="9281f-132">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="9281f-132">Bitbucket</span></span>

<span data-ttu-id="9281f-133">Per il ridimensionamento delle applicazioni:</span><span class="sxs-lookup"><span data-stu-id="9281f-133">For application scaling:</span></span>

* <span data-ttu-id="9281f-134">I clienti adattabile alto e verso il basso le applicazioni web modificando il livello di hello del piano di servizio App</span><span class="sxs-lookup"><span data-stu-id="9281f-134">Customers can scale web apps up and down by changing hello tier of their App Service plan</span></span>
* <span data-ttu-id="9281f-135">I clienti possono scalabilità delle applicazioni ed eseguire più istanze di app entro confini hello della loro SKU</span><span class="sxs-lookup"><span data-stu-id="9281f-135">Customers can scale out applications and run multiple app instances within hello confines of their SKU</span></span>

<span data-ttu-id="9281f-136">Per Kudu, alcune delle funzionalità di base hello:</span><span class="sxs-lookup"><span data-stu-id="9281f-136">For Kudu, some of hello basic functionality:</span></span>

* <span data-ttu-id="9281f-137">Ambienti</span><span class="sxs-lookup"><span data-stu-id="9281f-137">Environments</span></span>
* <span data-ttu-id="9281f-138">Deployments</span><span class="sxs-lookup"><span data-stu-id="9281f-138">Deployments</span></span>
* <span data-ttu-id="9281f-139">Console di base</span><span class="sxs-lookup"><span data-stu-id="9281f-139">Basic console</span></span>
* <span data-ttu-id="9281f-140">SSH</span><span class="sxs-lookup"><span data-stu-id="9281f-140">SSH</span></span>

<span data-ttu-id="9281f-141">Per DevOps:</span><span class="sxs-lookup"><span data-stu-id="9281f-141">For devops:</span></span>

* <span data-ttu-id="9281f-142">Ambienti di staging</span><span class="sxs-lookup"><span data-stu-id="9281f-142">Staging environments</span></span>
* <span data-ttu-id="9281f-143">ACR e implementazione continua/distribuzione continua di DockerHub</span><span class="sxs-lookup"><span data-stu-id="9281f-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="9281f-144">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="9281f-144">Limitations</span></span>
<span data-ttu-id="9281f-145">Hello portale di Azure Mostra solo le funzionalità utilizzabili per l'App Web in Linux e nasconde rest hello.</span><span class="sxs-lookup"><span data-stu-id="9281f-145">hello Azure portal shows only features that currently work for Web App on Linux and hides hello rest.</span></span> <span data-ttu-id="9281f-146">Come si abilita più funzionalità, saranno visibili nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="9281f-146">As we enable more features, they will be visible on hello portal.</span></span>

<span data-ttu-id="9281f-147">Alcune funzionalità, quali l'integrazione delle reti virtuali, l'autenticazione di Azure Active Directory o di terze parti o le estensioni del sito Kudu, non sono ancora disponibili.</span><span class="sxs-lookup"><span data-stu-id="9281f-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="9281f-148">Una volta queste funzionalità sono disponibili, Microsoft aggiornerà la documentazione e il blog sulle modifiche hello.</span><span class="sxs-lookup"><span data-stu-id="9281f-148">Once these features are available, we will update our documentation and blog about hello changes.</span></span>

<span data-ttu-id="9281f-149">Questa versione di anteprima pubblica è attualmente disponibile solo in hello seguenti aree:</span><span class="sxs-lookup"><span data-stu-id="9281f-149">This public preview is currently only available in hello following regions:</span></span>

* <span data-ttu-id="9281f-150">Stati Uniti occidentali</span><span class="sxs-lookup"><span data-stu-id="9281f-150">West US</span></span>
* <span data-ttu-id="9281f-151">Stati Uniti Orientali</span><span class="sxs-lookup"><span data-stu-id="9281f-151">East US</span></span>
* <span data-ttu-id="9281f-152">Europa occidentale</span><span class="sxs-lookup"><span data-stu-id="9281f-152">West Europe</span></span>
* <span data-ttu-id="9281f-153">Europa settentrionale</span><span class="sxs-lookup"><span data-stu-id="9281f-153">North Europe</span></span>
* <span data-ttu-id="9281f-154">Stati Uniti centro-meridionali</span><span class="sxs-lookup"><span data-stu-id="9281f-154">South Central US</span></span>
* <span data-ttu-id="9281f-155">Stati Uniti centro-settentrionali</span><span class="sxs-lookup"><span data-stu-id="9281f-155">North Central US</span></span>
* <span data-ttu-id="9281f-156">Asia sudorientale</span><span class="sxs-lookup"><span data-stu-id="9281f-156">Southeast Asia</span></span>
* <span data-ttu-id="9281f-157">Asia orientale</span><span class="sxs-lookup"><span data-stu-id="9281f-157">East Asia</span></span>
* <span data-ttu-id="9281f-158">Australia orientale</span><span class="sxs-lookup"><span data-stu-id="9281f-158">Australia East</span></span>
* <span data-ttu-id="9281f-159">Giappone orientale</span><span class="sxs-lookup"><span data-stu-id="9281f-159">Japan East</span></span>
* <span data-ttu-id="9281f-160">Brasile meridionale</span><span class="sxs-lookup"><span data-stu-id="9281f-160">Brazil South</span></span>
* <span data-ttu-id="9281f-161">India meridionale</span><span class="sxs-lookup"><span data-stu-id="9281f-161">South India</span></span>

<span data-ttu-id="9281f-162">Web App in Linux è supportata solo nei piani di servizio app dedicato hello e non dispone di un livello condiviso o disponibile.</span><span class="sxs-lookup"><span data-stu-id="9281f-162">Web Apps on Linux is only supported in hello Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="9281f-163">I piani di servizio app per le app Web normali e di Linux si escludono a vicenda, quindi non è possibile creare un'app Web di Linux in un piano di servizio app non Linux.</span><span class="sxs-lookup"><span data-stu-id="9281f-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="9281f-164">App in Linux Web deve essere creata in un gruppo di risorse che non contiene App web non Linux in hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="9281f-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in hello same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9281f-165">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="9281f-165">Troubleshooting</span></span> ##

<span data-ttu-id="9281f-166">Quando l'applicazione non riesce toostart o si desidera la registrazione di hello toocheck dall'app, controllare hello che docker log nella directory LogFiles hello.</span><span class="sxs-lookup"><span data-stu-id="9281f-166">When your application fails toostart or you want toocheck hello logging from your app, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="9281f-167">È possibile accedere a questa directory tramite il sito SCM o tramite FTP.</span><span class="sxs-lookup"><span data-stu-id="9281f-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="9281f-168">hello toolog `stdout` e `stderr` dal contenitore, è necessario tooenable **registrazione contenitore Docker** in **log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="9281f-168">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Abilitazione della registrazione][2]

![Utilizzo dei registri di Docker tooview Kudu][1]

<span data-ttu-id="9281f-171">È possibile accedere hello SCM sito da **strumenti avanzati** in hello **gli strumenti di sviluppo** menu.</span><span class="sxs-lookup"><span data-stu-id="9281f-171">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9281f-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9281f-172">Next steps</span></span>
<span data-ttu-id="9281f-173">Vedere hello seguendo i collegamenti tooget avviato con il servizio App in Linux.</span><span class="sxs-lookup"><span data-stu-id="9281f-173">See hello following links tooget started with App Service on Linux.</span></span> <span data-ttu-id="9281f-174">È possibile pubblicare domande e dubbi nel [forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="9281f-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="9281f-175">Come immagine di toouse una Docker personalizzata per l'App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="9281f-175">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="9281f-176">Uso della configurazione PM2 per Node.js in App Web su Linux</span><span class="sxs-lookup"><span data-stu-id="9281f-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="9281f-177">Uso di .NET Core in App Web del Servizio app di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="9281f-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="9281f-178">Uso di Ruby in App Web del Servizio app di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="9281f-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="9281f-179">Domande frequenti su App Web del Servizio app di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="9281f-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* <span data-ttu-id="9281f-180">[SSH support for Azure Web App on Linux](./app-service-linux-ssh-support.md) (Supporto SSH per App Web di Azure in Linux)</span><span class="sxs-lookup"><span data-stu-id="9281f-180">[SSH support for Azure Web App on Linux](./app-service-linux-ssh-support.md)</span></span>
* [<span data-ttu-id="9281f-181">Configurare gli ambienti di gestione temporanea nel Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="9281f-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* <span data-ttu-id="9281f-182">[Docker Hub Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md) (Distribuzione continua dell'hub Docker con App Web di Azure in Linux)</span><span class="sxs-lookup"><span data-stu-id="9281f-182">[Docker Hub Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md)</span></span>

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png