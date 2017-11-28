---
title: Introduzione ad App Web di Azure in Linux | Microsoft Docs
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
ms.openlocfilehash: 0870f811845ec7c705da13f08abdfa762d25b209
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-azure-web-app-on-linux"></a><span data-ttu-id="e6b9c-104">Introduzione ad App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="e6b9c-104">Introduction to Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="e6b9c-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e6b9c-105">Overview</span></span>
<span data-ttu-id="e6b9c-106">I clienti possono usare App Web in Linux per ospitare app Web in modo nativo in Linux per stack di applicazioni supportate.</span><span class="sxs-lookup"><span data-stu-id="e6b9c-106">Customers can use Web App on Linux to host web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="e6b9c-107">La sezione seguente elenca gli stack di applicazioni attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="e6b9c-107">The following section lists the application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="e6b9c-108">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="e6b9c-108">Features</span></span>
<span data-ttu-id="e6b9c-109">App Web in Linux supporta attualmente gli stack di applicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e6b9c-109">Web App on Linux currently supports the following application stacks:</span></span>

* <span data-ttu-id="e6b9c-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="e6b9c-110">Node.js</span></span>
    * <span data-ttu-id="e6b9c-111">4.4</span><span class="sxs-lookup"><span data-stu-id="e6b9c-111">4.4</span></span>
    * <span data-ttu-id="e6b9c-112">4.5</span><span class="sxs-lookup"><span data-stu-id="e6b9c-112">4.5</span></span>
    * <span data-ttu-id="e6b9c-113">6.2</span><span class="sxs-lookup"><span data-stu-id="e6b9c-113">6.2</span></span>
    * <span data-ttu-id="e6b9c-114">6.6</span><span class="sxs-lookup"><span data-stu-id="e6b9c-114">6.6</span></span>
    * <span data-ttu-id="e6b9c-115">6.9</span><span class="sxs-lookup"><span data-stu-id="e6b9c-115">6.9</span></span>
    * <span data-ttu-id="e6b9c-116">6.10</span><span class="sxs-lookup"><span data-stu-id="e6b9c-116">6.10</span></span>
    * <span data-ttu-id="e6b9c-117">6.11</span><span class="sxs-lookup"><span data-stu-id="e6b9c-117">6.11</span></span>
    * <span data-ttu-id="e6b9c-118">8.0</span><span class="sxs-lookup"><span data-stu-id="e6b9c-118">8.0</span></span>
    * <span data-ttu-id="e6b9c-119">8.1</span><span class="sxs-lookup"><span data-stu-id="e6b9c-119">8.1</span></span>
* <span data-ttu-id="e6b9c-120">PHP</span><span class="sxs-lookup"><span data-stu-id="e6b9c-120">PHP</span></span>
    * <span data-ttu-id="e6b9c-121">5.6</span><span class="sxs-lookup"><span data-stu-id="e6b9c-121">5.6</span></span>
    * <span data-ttu-id="e6b9c-122">7.0</span><span class="sxs-lookup"><span data-stu-id="e6b9c-122">7.0</span></span>
* <span data-ttu-id="e6b9c-123">.Net Core</span><span class="sxs-lookup"><span data-stu-id="e6b9c-123">.Net Core</span></span>
    * <span data-ttu-id="e6b9c-124">1.0</span><span class="sxs-lookup"><span data-stu-id="e6b9c-124">1.0</span></span>
    * <span data-ttu-id="e6b9c-125">1.1</span><span class="sxs-lookup"><span data-stu-id="e6b9c-125">1.1</span></span>
* <span data-ttu-id="e6b9c-126">Ruby</span><span class="sxs-lookup"><span data-stu-id="e6b9c-126">Ruby</span></span>
    * <span data-ttu-id="e6b9c-127">2.3</span><span class="sxs-lookup"><span data-stu-id="e6b9c-127">2.3</span></span>

<span data-ttu-id="e6b9c-128">I clienti possono distribuire le applicazioni tramite:</span><span class="sxs-lookup"><span data-stu-id="e6b9c-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="e6b9c-129">FTP</span><span class="sxs-lookup"><span data-stu-id="e6b9c-129">FTP</span></span>
* <span data-ttu-id="e6b9c-130">Repository Git locale</span><span class="sxs-lookup"><span data-stu-id="e6b9c-130">Local Git</span></span>
* <span data-ttu-id="e6b9c-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="e6b9c-131">GitHub</span></span>
* <span data-ttu-id="e6b9c-132">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="e6b9c-132">Bitbucket</span></span>

<span data-ttu-id="e6b9c-133">Per il ridimensionamento delle applicazioni:</span><span class="sxs-lookup"><span data-stu-id="e6b9c-133">For application scaling:</span></span>

* <span data-ttu-id="e6b9c-134">I clienti possono aumentare e ridurre le prestazioni delle app Web modificando il livello nel piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="e6b9c-134">Customers can scale web apps up and down by changing the tier of their App Service plan</span></span>
* <span data-ttu-id="e6b9c-135">I clienti possono scalare orizzontalmente le applicazioni ed eseguire più istanze di un'app entro i confini dello SKU</span><span class="sxs-lookup"><span data-stu-id="e6b9c-135">Customers can scale out applications and run multiple app instances within the confines of their SKU</span></span>

<span data-ttu-id="e6b9c-136">Per Kudu, alcune delle funzionalità di base:</span><span class="sxs-lookup"><span data-stu-id="e6b9c-136">For Kudu, some of the basic functionality:</span></span>

* <span data-ttu-id="e6b9c-137">Ambienti</span><span class="sxs-lookup"><span data-stu-id="e6b9c-137">Environments</span></span>
* <span data-ttu-id="e6b9c-138">Deployments</span><span class="sxs-lookup"><span data-stu-id="e6b9c-138">Deployments</span></span>
* <span data-ttu-id="e6b9c-139">Console di base</span><span class="sxs-lookup"><span data-stu-id="e6b9c-139">Basic console</span></span>
* <span data-ttu-id="e6b9c-140">SSH</span><span class="sxs-lookup"><span data-stu-id="e6b9c-140">SSH</span></span>

<span data-ttu-id="e6b9c-141">Per DevOps:</span><span class="sxs-lookup"><span data-stu-id="e6b9c-141">For devops:</span></span>

* <span data-ttu-id="e6b9c-142">Ambienti di staging</span><span class="sxs-lookup"><span data-stu-id="e6b9c-142">Staging environments</span></span>
* <span data-ttu-id="e6b9c-143">ACR e implementazione continua/distribuzione continua di DockerHub</span><span class="sxs-lookup"><span data-stu-id="e6b9c-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="e6b9c-144">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="e6b9c-144">Limitations</span></span>
<span data-ttu-id="e6b9c-145">Il portale di Azure mostra solo le funzionalità che possono essere usate attualmente per App Web in Linux e nasconde le altre.</span><span class="sxs-lookup"><span data-stu-id="e6b9c-145">The Azure portal shows only features that currently work for Web App on Linux and hides the rest.</span></span> <span data-ttu-id="e6b9c-146">Man mano che verranno abilitate nuove funzionalità, queste diventeranno visibili nel portale.</span><span class="sxs-lookup"><span data-stu-id="e6b9c-146">As we enable more features, they will be visible on the portal.</span></span>

<span data-ttu-id="e6b9c-147">Alcune funzionalità, quali l'integrazione delle reti virtuali, l'autenticazione di Azure Active Directory o di terze parti o le estensioni del sito Kudu, non sono ancora disponibili.</span><span class="sxs-lookup"><span data-stu-id="e6b9c-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="e6b9c-148">Man mano che queste funzionalità dinvetano disponibili, la documentazione verrà aggiornata e le modifiche pubblicate nei blog.</span><span class="sxs-lookup"><span data-stu-id="e6b9c-148">Once these features are available, we will update our documentation and blog about the changes.</span></span>

<span data-ttu-id="e6b9c-149">Questa anteprima pubblica è attualmente disponibile solo nelle aree seguenti:</span><span class="sxs-lookup"><span data-stu-id="e6b9c-149">This public preview is currently only available in the following regions:</span></span>

* <span data-ttu-id="e6b9c-150">Stati Uniti occidentali</span><span class="sxs-lookup"><span data-stu-id="e6b9c-150">West US</span></span>
* <span data-ttu-id="e6b9c-151">Stati Uniti Orientali</span><span class="sxs-lookup"><span data-stu-id="e6b9c-151">East US</span></span>
* <span data-ttu-id="e6b9c-152">Europa occidentale</span><span class="sxs-lookup"><span data-stu-id="e6b9c-152">West Europe</span></span>
* <span data-ttu-id="e6b9c-153">Europa settentrionale</span><span class="sxs-lookup"><span data-stu-id="e6b9c-153">North Europe</span></span>
* <span data-ttu-id="e6b9c-154">Stati Uniti centro-meridionali</span><span class="sxs-lookup"><span data-stu-id="e6b9c-154">South Central US</span></span>
* <span data-ttu-id="e6b9c-155">Stati Uniti centro-settentrionali</span><span class="sxs-lookup"><span data-stu-id="e6b9c-155">North Central US</span></span>
* <span data-ttu-id="e6b9c-156">Asia sudorientale</span><span class="sxs-lookup"><span data-stu-id="e6b9c-156">Southeast Asia</span></span>
* <span data-ttu-id="e6b9c-157">Asia orientale</span><span class="sxs-lookup"><span data-stu-id="e6b9c-157">East Asia</span></span>
* <span data-ttu-id="e6b9c-158">Australia orientale</span><span class="sxs-lookup"><span data-stu-id="e6b9c-158">Australia East</span></span>
* <span data-ttu-id="e6b9c-159">Giappone orientale</span><span class="sxs-lookup"><span data-stu-id="e6b9c-159">Japan East</span></span>
* <span data-ttu-id="e6b9c-160">Brasile meridionale</span><span class="sxs-lookup"><span data-stu-id="e6b9c-160">Brazil South</span></span>
* <span data-ttu-id="e6b9c-161">India meridionale</span><span class="sxs-lookup"><span data-stu-id="e6b9c-161">South India</span></span>

<span data-ttu-id="e6b9c-162">App Web in Linux è supportato solo nei piani di servizio app dedicati e non ha un livello Gratuito o Condiviso.</span><span class="sxs-lookup"><span data-stu-id="e6b9c-162">Web Apps on Linux is only supported in the Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="e6b9c-163">I piani di servizio app per le app Web normali e di Linux si escludono a vicenda, quindi non è possibile creare un'app Web di Linux in un piano di servizio app non Linux.</span><span class="sxs-lookup"><span data-stu-id="e6b9c-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="e6b9c-164">Le app Web in Linux devono essere create in un gruppo di risorse che non contiene app Web non Linux nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="e6b9c-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in the same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e6b9c-165">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="e6b9c-165">Troubleshooting</span></span> ##

<span data-ttu-id="e6b9c-166">Quando non è possibile avviare l'applicazione o si desidera controllare il log dall'app, controllare i log di Docker nella directory LogFiles.</span><span class="sxs-lookup"><span data-stu-id="e6b9c-166">When your application fails to start or you want to check the logging from your app, check the Docker logs in the LogFiles directory.</span></span> <span data-ttu-id="e6b9c-167">È possibile accedere a questa directory tramite il sito SCM o tramite FTP.</span><span class="sxs-lookup"><span data-stu-id="e6b9c-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="e6b9c-168">Per registrare `stdout` e `stderr` dal contenitore, è necessario abilitare **Registrazione del contenitore Docker** in **Log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="e6b9c-168">To log the `stdout` and `stderr` from your container, you need to enable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Abilitazione della registrazione][2]

![Uso di Kudu per visualizzare i log di Docker][1]

<span data-ttu-id="e6b9c-171">È possibile accedere al sito SCM da **Strumenti avanzati** nel menu **Strumenti di sviluppo**.</span><span class="sxs-lookup"><span data-stu-id="e6b9c-171">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6b9c-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e6b9c-172">Next steps</span></span>
<span data-ttu-id="e6b9c-173">Vedere i collegamenti seguenti per iniziare a usare il servizio app in Linux.</span><span class="sxs-lookup"><span data-stu-id="e6b9c-173">See the following links to get started with App Service on Linux.</span></span> <span data-ttu-id="e6b9c-174">È possibile pubblicare domande e dubbi nel [forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="e6b9c-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="e6b9c-175">Come usare un'immagine Docker personalizzata per App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="e6b9c-175">How to use a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="e6b9c-176">Uso della configurazione PM2 per Node.js in App Web su Linux</span><span class="sxs-lookup"><span data-stu-id="e6b9c-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="e6b9c-177">Uso di .NET Core in App Web del Servizio app di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="e6b9c-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="e6b9c-178">Uso di Ruby in App Web del Servizio app di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="e6b9c-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="e6b9c-179">Domande frequenti su App Web del Servizio app di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="e6b9c-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* <span data-ttu-id="e6b9c-180">[SSH support for Azure Web App on Linux](./app-service-linux-ssh-support.md) (Supporto SSH per App Web di Azure in Linux)</span><span class="sxs-lookup"><span data-stu-id="e6b9c-180">[SSH support for Azure Web App on Linux](./app-service-linux-ssh-support.md)</span></span>
* [<span data-ttu-id="e6b9c-181">Configurare gli ambienti di gestione temporanea nel Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="e6b9c-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* <span data-ttu-id="e6b9c-182">[Docker Hub Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md) (Distribuzione continua dell'hub Docker con App Web di Azure in Linux)</span><span class="sxs-lookup"><span data-stu-id="e6b9c-182">[Docker Hub Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md)</span></span>

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png