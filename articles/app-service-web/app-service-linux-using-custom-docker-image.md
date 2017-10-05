---
title: Come usare un'immagine Docker personalizzata per App Web di Azure in Linux | Microsoft Docs
description: Come usare un'immagine Docker personalizzata per App Web di Azure in Linux.
keywords: Servizio app di Azure, app Web, Linux, Docker, contenitore
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: b97bd4e6-dff0-4976-ac20-d5c109a559a8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 1458217a31c4781b28877c030a665f5b22819e13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a><span data-ttu-id="be81b-104">Uso di un'immagine Docker personalizzata per App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="be81b-104">Using a custom Docker image for Azure Web App on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="be81b-105">Il servizio app fornisce stack di applicazioni predefiniti in Linux con il supporto per versioni specifiche, ad esempio PHP 7.0 e Node.js 4.5.</span><span class="sxs-lookup"><span data-stu-id="be81b-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="be81b-106">Il servizio app in Linux usa i contenitori Docker per ospitare questi stack di applicazioni predefiniti.</span><span class="sxs-lookup"><span data-stu-id="be81b-106">App Service on Linux uses Docker containers to host these pre-built application stacks.</span></span> <span data-ttu-id="be81b-107">È anche possibile usare un'immagine Docker personalizzata per distribuire l'app Web in uno stack di applicazioni non ancora definito in Azure.</span><span class="sxs-lookup"><span data-stu-id="be81b-107">You can also use a custom Docker image to deploy your web app to an application stack that is not already defined in Azure.</span></span> <span data-ttu-id="be81b-108">Le immagini Docker personalizzate possono essere ospitate in un repository Docker pubblico o privato.</span><span class="sxs-lookup"><span data-stu-id="be81b-108">Custom Docker images can be hosted on either a public or private Docker repository.</span></span>


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a><span data-ttu-id="be81b-109">Procedura: Impostare un'immagine Docker personalizzata per un'app Web</span><span class="sxs-lookup"><span data-stu-id="be81b-109">How to: set a custom Docker image for a web app</span></span>
<span data-ttu-id="be81b-110">È possibile impostare l'immagine Docker personalizzata per app Web sia nuove che esistenti.</span><span class="sxs-lookup"><span data-stu-id="be81b-110">You can set the custom Docker image for both new and existing webs apps.</span></span> <span data-ttu-id="be81b-111">Quando si crea un'app Web in Linux nel [portale di Azure](https://portal.azure.com/#create/Microsoft.AppSvcLinux), fare clic su **Configura contenitore** per impostare un'immagine Docker personalizzata:</span><span class="sxs-lookup"><span data-stu-id="be81b-111">When you create a web app on Linux in the [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), click **Configure container** to set a custom Docker image:</span></span>

![Immagine Docker personalizzata per una nuova app Web in Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a><span data-ttu-id="be81b-113">Procedura: usare un'immagine Docker personalizzata dall'hub Docker</span><span class="sxs-lookup"><span data-stu-id="be81b-113">How to: use a custom Docker image from Docker Hub</span></span> ##
<span data-ttu-id="be81b-114">Per usare un'immagine Docker personalizzata dall'hub Docker:</span><span class="sxs-lookup"><span data-stu-id="be81b-114">To use a custom Docker image from Docker Hub:</span></span>

1. <span data-ttu-id="be81b-115">Nel [portale di Azure](https://portal.azure.com) trovare l'app Web in Linux, quindi in **Impostazioni** fare clic su **Contenitore Docker**.</span><span class="sxs-lookup"><span data-stu-id="be81b-115">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="be81b-116">Selezionare **Docker Hub** (Hub Docker) come **Origine immagine**, quindi fare clic su **Pubblico** o **Privato** e digitare il **nome Immagine e tag facoltativo**, ad esempio `node:4.5`.</span><span class="sxs-lookup"><span data-stu-id="be81b-116">Select **Docker Hub** as the **Image source**, then click either **Public** or **Private** and type the **Image and optional tag name**, such as `node:4.5`.</span></span> <span data-ttu-id="be81b-117">Il **Comando Avvia** viene impostato automaticamente in base al contenuto definito nel file di immagine Docker, ma è possibile impostare i propri comandi.</span><span class="sxs-lookup"><span data-stu-id="be81b-117">The **Startup command** is set automatically based on what is defined in the Docker image file, but you can set your own commands.</span></span>  

    ![Configurare l'immagine del repository pubblico dell'hub Docker][2]

    <span data-ttu-id="be81b-119">Quando l'immagine proviene da un repository privato, è anche necessario immettere le credenziali dell'hub Docker (**Nome utente di accesso** e **Password**) per il repository dell'hub Docker privato.</span><span class="sxs-lookup"><span data-stu-id="be81b-119">When your image is from a private repository, you also need to enter the Docker Hub credentials as (**Login username** and **Password**) for the private Docker Hub repository.</span></span>

    ![Configurare l'immagine del repository privato dell'hub Docker][3]

3. <span data-ttu-id="be81b-121">Dopo avere configurato il contenitore, fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="be81b-121">After you have configured the container, click **Save**.</span></span>

## <a name="how-to-use-a-docker-image-from-a-private-image-registry"></a><span data-ttu-id="be81b-122">Come usare un'immagine Docker da un registro di sistema di immagini privato</span><span class="sxs-lookup"><span data-stu-id="be81b-122">How to use a Docker image from a private image registry</span></span> ##
<span data-ttu-id="be81b-123">Per usare un'immagine Docker personalizzata proveniente da un registro di sistema di immagini privato:</span><span class="sxs-lookup"><span data-stu-id="be81b-123">To use a custom Docker image from a private image registry:</span></span>

1. <span data-ttu-id="be81b-124">Nel [portale di Azure](https://portal.azure.com) trovare l'app Web in Linux, quindi in **Impostazioni** fare clic su **Contenitore Docker**.</span><span class="sxs-lookup"><span data-stu-id="be81b-124">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="be81b-125">Fare clic su **Registro di sistema privato** come **Origine immagine**.</span><span class="sxs-lookup"><span data-stu-id="be81b-125">Click **Private registry** as the **Image source**.</span></span> <span data-ttu-id="be81b-126">Immettere il **Image and optional tag name** (Nome tag opzionale e immagine), l'**URL server** del registro di sistema privato, insieme alle credenziali (**nome utente di accesso** e **password**).</span><span class="sxs-lookup"><span data-stu-id="be81b-126">Enter the **Image and optional tag name**, **Server URL** for the private registry, along with the credentials (**Login username** and **Password**).</span></span> <span data-ttu-id="be81b-127">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="be81b-127">Click **Save**.</span></span>

    ![Configurare l'immagine Docker dal registro di sistema privato][4]


## <a name="how-to-set-the-port-used-by-your-docker-image"></a><span data-ttu-id="be81b-129">Procedura: Impostare la porta usata dall'immagine Docker</span><span class="sxs-lookup"><span data-stu-id="be81b-129">How to: set the port used by your Docker image</span></span> ##

<span data-ttu-id="be81b-130">Quando si usa un'immagine Docker personalizzata per l'app Web, è possibile usare la variabile di ambiente `WEBSITES_PORT` nel file Docker, che viene aggiunta al contenitore generato.</span><span class="sxs-lookup"><span data-stu-id="be81b-130">When you use a custom Docker image for your web app, you can use the `WEBSITES_PORT` environment variable in your Dockerfile, which gets added to the generated container.</span></span> <span data-ttu-id="be81b-131">Considerare l'esempio seguente di file Docker per un'applicazione Ruby:</span><span class="sxs-lookup"><span data-stu-id="be81b-131">Consider the following example of a docker file for a Ruby application:</span></span>

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

<span data-ttu-id="be81b-132">Nell'ultima riga del comando è possibile osservare che la variabile di ambiente WEBSITES_PORT viene passata in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="be81b-132">On last line of the command, you can see that the WEBSITES_PORT environment variable is passed at runtime.</span></span> <span data-ttu-id="be81b-133">Tenere presente che la distinzione tra maiuscole e minuscole è importante nei comandi.</span><span class="sxs-lookup"><span data-stu-id="be81b-133">Remember that casing matters in commands.</span></span>

<span data-ttu-id="be81b-134">In precedenza, la piattaforma usava l'impostazione dell'app `PORT`. È previsto che l'uso di questa impostazione dell'app venga deprecato per passare all'uso esclusivo di `WEBSITES_PORT`.</span><span class="sxs-lookup"><span data-stu-id="be81b-134">Previously the platform was using `PORT` app setting, we are planning to deprecate the use this app setting and move to using `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="be81b-135">Quando si usa un'immagine Docker esistente compilata da un altro utente, potrebbe essere necessario specificare una porta diversa dalla porta 80 per l'immagine.</span><span class="sxs-lookup"><span data-stu-id="be81b-135">When you use an existing Docker image built by someone else, you may need to specify a port other than port 80 for the application.</span></span> <span data-ttu-id="be81b-136">Per configurare la porta, aggiungere un'impostazione di applicazione denominata `WEBSITES_PORT` con il valore come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="be81b-136">To configure the port, add an application setting named `WEBSITES_PORT` with the value as shown below:</span></span>

![Configurare l'impostazione app PORT per l'immagine Docker personalizzata][6]

## <a name="how-to-set-the-startup-time-for-your-docker-image"></a><span data-ttu-id="be81b-138">Procedura: impostare l'ora di avvio per l'immagine Docker</span><span class="sxs-lookup"><span data-stu-id="be81b-138">How to: set the startup time for your Docker image</span></span> ##

<span data-ttu-id="be81b-139">Per impostazione predefinita, se il contenitore non viene avviato prima di 230 secondi, la piattaforma riavvierà il contenitore.</span><span class="sxs-lookup"><span data-stu-id="be81b-139">By default, if your container does not start before 230 seconds, the platform will restart your container.</span></span> <span data-ttu-id="be81b-140">Se l'immagine Docker personalizzata viene avviata in più di 230 secondi, è possibile usare l'impostazione di app `WEBSITES_CONTAINER_START_TIME_LIMIT`; il valore di questa impostazione è espresso in secondi e in questo modo la piattaforma potrà mantenere il contenitore in esecuzione prima del riavvio.</span><span class="sxs-lookup"><span data-stu-id="be81b-140">If your custom Docker image starts in more than 230 seconds, you can use the `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting, the value for this setting is in seconds, this will allow the platform keep your container running before restarting it.</span></span> <span data-ttu-id="be81b-141">Il valore predefinito è 230 secondi e il valore massimo consentito è 600 secondi.</span><span class="sxs-lookup"><span data-stu-id="be81b-141">The default value is 230 seconds, and the max allowed value is 600 seconds.</span></span>

## <a name="how-to-unmount-the-platform-provided-storage"></a><span data-ttu-id="be81b-142">Procedura: effettuare lo smontaggio della risorsa di archiviazione fornita dalla piattaforma</span><span class="sxs-lookup"><span data-stu-id="be81b-142">How to: unmount the platform provided storage</span></span> ##

<span data-ttu-id="be81b-143">Per impostazione predefinita, la piattaforma esegue il montaggio di una condivisione di archiviazione permanente nella directory `\home\`.</span><span class="sxs-lookup"><span data-stu-id="be81b-143">By default, the platform will mount a persistent storage share to the `\home\` directory.</span></span> <span data-ttu-id="be81b-144">Se l'immagine del contenitore non necessita di una condivisione persistente, è possibile disabilitare il montaggio di tale archiviazione specificando l'impostazione di app `WEBSITES_ENABLE_APP_SERVICE_STORAGE` su `false`.</span><span class="sxs-lookup"><span data-stu-id="be81b-144">If your container image does not need a persistent share, you can disable mounting that storage by setting the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting to `false`.</span></span> <span data-ttu-id="be81b-145">Sarà comunque possibile accedere a tale risorsa di archiviazione dal sito scm e tutti i log Docker, se abilitati, verranno scritti nei file di log generati dalla piattaforma.</span><span class="sxs-lookup"><span data-stu-id="be81b-145">You will still have access to that storage from the scm site, and all Docker logs (if enabled) will be written to the log files generated by the platform.</span></span>

## <a name="how-to-switch-back-to-using-a-built-in-image"></a><span data-ttu-id="be81b-146">Procedura: Usare di nuovo un'immagine predefinita</span><span class="sxs-lookup"><span data-stu-id="be81b-146">How to: Switch back to using a built-in image</span></span> ##

<span data-ttu-id="be81b-147">Per passare da un'immagine personalizzata a un'immagine predefinita:</span><span class="sxs-lookup"><span data-stu-id="be81b-147">To switch from using a custom image to using a built-in image:</span></span>

1. <span data-ttu-id="be81b-148">Nel [portale di Azure](https://portal.azure.com) trovare l'app Web in Linux, quindi in **Impostazioni** fare clic su **Servizio app**.</span><span class="sxs-lookup"><span data-stu-id="be81b-148">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span></span>

2. <span data-ttu-id="be81b-149">Selezionare lo **Stack di runtime** da usare per l'immagine predefinita, quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="be81b-149">Select your **Runtime Stack** to use for the built-in image, then click **Save**.</span></span> 

![Configurare l'immagine Docker predefinita][5]


## <a name="troubleshooting"></a><span data-ttu-id="be81b-151">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="be81b-151">Troubleshooting</span></span> ##

<span data-ttu-id="be81b-152">Quando non è possibile avviare l'applicazione con l'immagine Docker personalizzata, controllare i log di Docker nella directory LogFiles.</span><span class="sxs-lookup"><span data-stu-id="be81b-152">When your application fails to start with your custom Docker image, check the Docker logs in the LogFiles directory.</span></span> <span data-ttu-id="be81b-153">È possibile accedere a questa directory tramite il sito SCM o tramite FTP.</span><span class="sxs-lookup"><span data-stu-id="be81b-153">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="be81b-154">Per registrare `stdout` e `stderr` dal contenitore, è necessario abilitare **Registrazione del contenitore Docker** in **Log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="be81b-154">To log the `stdout` and `stderr` from your container, you need to enable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Abilitazione della registrazione][8]

![Uso di Kudu per visualizzare i log di Docker][7]

<span data-ttu-id="be81b-157">È possibile accedere al sito SCM da **Strumenti avanzati** nel menu **Strumenti di sviluppo**.</span><span class="sxs-lookup"><span data-stu-id="be81b-157">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be81b-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="be81b-158">Next Steps</span></span> ##

<span data-ttu-id="be81b-159">Fare clic sui collegamenti seguenti per iniziare a usare App Web in Linux.</span><span class="sxs-lookup"><span data-stu-id="be81b-159">Follow the following links to get started with Web App on Linux.</span></span>   

* [<span data-ttu-id="be81b-160">Introduzione ad App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="be81b-160">Introduction to Azure Web App on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="be81b-161">Uso della configurazione PM2 per Node.js in App Web su Linux</span><span class="sxs-lookup"><span data-stu-id="be81b-161">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](./app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="be81b-162">Domande frequenti su App Web del Servizio app di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="be81b-162">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<span data-ttu-id="be81b-163">Pubblicare domande e dubbi nel [forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="be81b-163">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
