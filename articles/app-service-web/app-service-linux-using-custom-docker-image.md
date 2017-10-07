---
title: aaaHow toouse un'immagine Docker personalizzata per l'App Web di Azure in Linux | Documenti Microsoft
description: Toouse una Docker personalizzata come immagine per l'App Web di Azure in Linux.
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
ms.openlocfilehash: 8853095d0e1067cfea4297bbd23b622fe4a0d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a><span data-ttu-id="edfa3-104">Uso di un'immagine Docker personalizzata per App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="edfa3-104">Using a custom Docker image for Azure Web App on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="edfa3-105">Il servizio app fornisce stack di applicazioni predefiniti in Linux con il supporto per versioni specifiche, ad esempio PHP 7.0 e Node.js 4.5.</span><span class="sxs-lookup"><span data-stu-id="edfa3-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="edfa3-106">Servizio App in Linux Usa i contenitori di Docker toohost questi predefinite stack di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="edfa3-106">App Service on Linux uses Docker containers toohost these pre-built application stacks.</span></span> <span data-ttu-id="edfa3-107">È anche possibile utilizzare un personalizzato toodeploy immagine Docker nello stack di applicazione tooan di app web che non è già stato definito in Azure.</span><span class="sxs-lookup"><span data-stu-id="edfa3-107">You can also use a custom Docker image toodeploy your web app tooan application stack that is not already defined in Azure.</span></span> <span data-ttu-id="edfa3-108">Le immagini Docker personalizzate possono essere ospitate in un repository Docker pubblico o privato.</span><span class="sxs-lookup"><span data-stu-id="edfa3-108">Custom Docker images can be hosted on either a public or private Docker repository.</span></span>


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a><span data-ttu-id="edfa3-109">Procedura: Impostare un'immagine Docker personalizzata per un'app Web</span><span class="sxs-lookup"><span data-stu-id="edfa3-109">How to: set a custom Docker image for a web app</span></span>
<span data-ttu-id="edfa3-110">È possibile impostare l'immagine Docker personalizzata hello per le nuove e applicazioni Web esistenti.</span><span class="sxs-lookup"><span data-stu-id="edfa3-110">You can set hello custom Docker image for both new and existing webs apps.</span></span> <span data-ttu-id="edfa3-111">Quando si crea un'app web in Linux in hello [portale di Azure](https://portal.azure.com/#create/Microsoft.AppSvcLinux), fare clic su **Configura contenitore** tooset un'immagine Docker personalizzata:</span><span class="sxs-lookup"><span data-stu-id="edfa3-111">When you create a web app on Linux in hello [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), click **Configure container** tooset a custom Docker image:</span></span>

![Immagine Docker personalizzata per una nuova app Web in Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a><span data-ttu-id="edfa3-113">Procedura: usare un'immagine Docker personalizzata dall'hub Docker</span><span class="sxs-lookup"><span data-stu-id="edfa3-113">How to: use a custom Docker image from Docker Hub</span></span> ##
<span data-ttu-id="edfa3-114">un'immagine Docker personalizzata dall'Hub Docker toouse:</span><span class="sxs-lookup"><span data-stu-id="edfa3-114">toouse a custom Docker image from Docker Hub:</span></span>

1. <span data-ttu-id="edfa3-115">In hello [portale di Azure](https://portal.azure.com), individuare l'app web in Linux, quindi **impostazioni** fare clic su **contenitore Docker**.</span><span class="sxs-lookup"><span data-stu-id="edfa3-115">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="edfa3-116">Selezionare **Hub Docker** come hello **origine dell'immagine**, quindi fare clic su **pubblica** o **privata** e hello tipo **immagine e nome del tag facoltativo**, ad esempio `node:4.5`.</span><span class="sxs-lookup"><span data-stu-id="edfa3-116">Select **Docker Hub** as hello **Image source**, then click either **Public** or **Private** and type hello **Image and optional tag name**, such as `node:4.5`.</span></span> <span data-ttu-id="edfa3-117">Hello **comando di avvio** è impostato automaticamente in base alle definizione nel file di immagine Docker hello, ma è possibile impostare i comandi.</span><span class="sxs-lookup"><span data-stu-id="edfa3-117">hello **Startup command** is set automatically based on what is defined in hello Docker image file, but you can set your own commands.</span></span>  

    ![Configurare l'immagine del repository pubblico dell'hub Docker][2]

    <span data-ttu-id="edfa3-119">Quando l'immagine è da un archivio privato, è necessario anche tooenter hello Hub Docker credenziali (**nome utente account di accesso** e **Password**) per il repository di hello privato Hub Docker.</span><span class="sxs-lookup"><span data-stu-id="edfa3-119">When your image is from a private repository, you also need tooenter hello Docker Hub credentials as (**Login username** and **Password**) for hello private Docker Hub repository.</span></span>

    ![Configurare l'immagine del repository privato dell'hub Docker][3]

3. <span data-ttu-id="edfa3-121">Dopo aver configurato il contenitore di hello, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="edfa3-121">After you have configured hello container, click **Save**.</span></span>

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a><span data-ttu-id="edfa3-122">Come immagine di toouse una Docker da un registro di sistema immagine privata</span><span class="sxs-lookup"><span data-stu-id="edfa3-122">How toouse a Docker image from a private image registry</span></span> ##
<span data-ttu-id="edfa3-123">toouse un'immagine personalizzata di Docker dal Registro di sistema immagine privata:</span><span class="sxs-lookup"><span data-stu-id="edfa3-123">toouse a custom Docker image from a private image registry:</span></span>

1. <span data-ttu-id="edfa3-124">In hello [portale di Azure](https://portal.azure.com), individuare l'app web in Linux, quindi **impostazioni** fare clic su **contenitore Docker**.</span><span class="sxs-lookup"><span data-stu-id="edfa3-124">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="edfa3-125">Fare clic su **registro privata** come hello **origine dell'immagine**.</span><span class="sxs-lookup"><span data-stu-id="edfa3-125">Click **Private registry** as hello **Image source**.</span></span> <span data-ttu-id="edfa3-126">Immettere hello **immagine e il nome di tag facoltativo**, **URL del Server** per hello privato del Registro di sistema, insieme alle credenziali hello (**nome utente account di accesso** e **Password** ).</span><span class="sxs-lookup"><span data-stu-id="edfa3-126">Enter hello **Image and optional tag name**, **Server URL** for hello private registry, along with hello credentials (**Login username** and **Password**).</span></span> <span data-ttu-id="edfa3-127">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="edfa3-127">Click **Save**.</span></span>

    ![Configurare l'immagine Docker dal registro di sistema privato][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a><span data-ttu-id="edfa3-129">Procedura: impostare hello porta utilizzata dall'immagine Docker</span><span class="sxs-lookup"><span data-stu-id="edfa3-129">How to: set hello port used by your Docker image</span></span> ##

<span data-ttu-id="edfa3-130">Quando si utilizza un'immagine Docker personalizzata per l'app web, è possibile utilizzare hello `WEBSITES_PORT` variabile di ambiente nel Dockerfile che viene aggiunto toohello generato contenitore.</span><span class="sxs-lookup"><span data-stu-id="edfa3-130">When you use a custom Docker image for your web app, you can use hello `WEBSITES_PORT` environment variable in your Dockerfile, which gets added toohello generated container.</span></span> <span data-ttu-id="edfa3-131">Prendere in considerazione hello esempio di un file di docker per un'applicazione Ruby seguente:</span><span class="sxs-lookup"><span data-stu-id="edfa3-131">Consider hello following example of a docker file for a Ruby application:</span></span>

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

<span data-ttu-id="edfa3-132">Ultima riga di comando hello, è possibile visualizzare che tale variabile di ambiente WEBSITES_PORT hello viene passato in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="edfa3-132">On last line of hello command, you can see that hello WEBSITES_PORT environment variable is passed at runtime.</span></span> <span data-ttu-id="edfa3-133">Tenere presente che la distinzione tra maiuscole e minuscole è importante nei comandi.</span><span class="sxs-lookup"><span data-stu-id="edfa3-133">Remember that casing matters in commands.</span></span>

<span data-ttu-id="edfa3-134">In precedenza si utilizzava piattaforma hello `PORT` app impostazione, si intende utilizzare hello toodeprecate questa impostazione di app e spostare toousing `WEBSITES_PORT` in modo esclusivo.</span><span class="sxs-lookup"><span data-stu-id="edfa3-134">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="edfa3-135">Quando si utilizza un'immagine Docker esistente compilata da un altro utente, potrebbe essere necessario toospecify una porta diversa dalla porta 80 per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="edfa3-135">When you use an existing Docker image built by someone else, you may need toospecify a port other than port 80 for hello application.</span></span> <span data-ttu-id="edfa3-136">tooconfigure hello porta, aggiungere un'impostazione dell'applicazione denominata `WEBSITES_PORT` con valore hello, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="edfa3-136">tooconfigure hello port, add an application setting named `WEBSITES_PORT` with hello value as shown below:</span></span>

![Configurare l'impostazione app PORT per l'immagine Docker personalizzata][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a><span data-ttu-id="edfa3-138">Procedura: impostare l'ora di avvio hello per l'immagine di Docker</span><span class="sxs-lookup"><span data-stu-id="edfa3-138">How to: set hello startup time for your Docker image</span></span> ##

<span data-ttu-id="edfa3-139">Per impostazione predefinita, se il contenitore non viene avviato prima di 230 secondi, piattaforma hello riavvierà il contenitore.</span><span class="sxs-lookup"><span data-stu-id="edfa3-139">By default, if your container does not start before 230 seconds, hello platform will restart your container.</span></span> <span data-ttu-id="edfa3-140">Se l'immagine personalizzata di Docker viene avviato in più di 230 secondi, è possibile utilizzare hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app impostazione, il valore di hello per questa impostazione è espresso in secondi, in questo modo sarà hello piattaforma tenere il contenitore in esecuzione prima di riavviarlo.</span><span class="sxs-lookup"><span data-stu-id="edfa3-140">If your custom Docker image starts in more than 230 seconds, you can use hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting, hello value for this setting is in seconds, this will allow hello platform keep your container running before restarting it.</span></span> <span data-ttu-id="edfa3-141">valore predefinito di Hello è 230 secondi e max hello consentito è 600 secondi.</span><span class="sxs-lookup"><span data-stu-id="edfa3-141">hello default value is 230 seconds, and hello max allowed value is 600 seconds.</span></span>

## <a name="how-to-unmount-hello-platform-provided-storage"></a><span data-ttu-id="edfa3-142">Procedura: smontare archiviazione fornita dalla piattaforma hello</span><span class="sxs-lookup"><span data-stu-id="edfa3-142">How to: unmount hello platform provided storage</span></span> ##

<span data-ttu-id="edfa3-143">Per impostazione predefinita, la piattaforma hello esegue il montaggio di toohello di condivisione di un archivio permanente `\home\` directory.</span><span class="sxs-lookup"><span data-stu-id="edfa3-143">By default, hello platform will mount a persistent storage share toohello `\home\` directory.</span></span> <span data-ttu-id="edfa3-144">Se l'immagine del contenitore non necessita di una condivisione persistente, è possibile disabilitare il montaggio che l'archiviazione per l'impostazione hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app impostazione troppo`false`.</span><span class="sxs-lookup"><span data-stu-id="edfa3-144">If your container image does not need a persistent share, you can disable mounting that storage by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span> <span data-ttu-id="edfa3-145">Sarà comunque possibile archiviazione toothat access dal sito scm hello e tutti i log di Docker (se abilitati) verranno scritto il file di log toohello generati dalla piattaforma hello.</span><span class="sxs-lookup"><span data-stu-id="edfa3-145">You will still have access toothat storage from hello scm site, and all Docker logs (if enabled) will be written toohello log files generated by hello platform.</span></span>

## <a name="how-to-switch-back-toousing-a-built-in-image"></a><span data-ttu-id="edfa3-146">Procedura: tornare toousing un'immagine incorporata</span><span class="sxs-lookup"><span data-stu-id="edfa3-146">How to: Switch back toousing a built-in image</span></span> ##

<span data-ttu-id="edfa3-147">tooswitch da toousing un'immagine personalizzata un'immagine incorporata tramite:</span><span class="sxs-lookup"><span data-stu-id="edfa3-147">tooswitch from using a custom image toousing a built-in image:</span></span>

1. <span data-ttu-id="edfa3-148">In hello [portale di Azure](https://portal.azure.com), individuare l'app web in Linux, quindi **impostazioni** fare clic su **servizio App**.</span><span class="sxs-lookup"><span data-stu-id="edfa3-148">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span></span>

2. <span data-ttu-id="edfa3-149">Selezionare il **Stack di Runtime** toouse per immagine incorporata hello, quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="edfa3-149">Select your **Runtime Stack** toouse for hello built-in image, then click **Save**.</span></span> 

![Configurare l'immagine Docker predefinita][5]


## <a name="troubleshooting"></a><span data-ttu-id="edfa3-151">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="edfa3-151">Troubleshooting</span></span> ##

<span data-ttu-id="edfa3-152">Quando l'applicazione non riesce toostart con l'immagine personalizzata di Docker, controllare hello che docker log nella directory LogFiles hello.</span><span class="sxs-lookup"><span data-stu-id="edfa3-152">When your application fails toostart with your custom Docker image, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="edfa3-153">È possibile accedere a questa directory tramite il sito SCM o tramite FTP.</span><span class="sxs-lookup"><span data-stu-id="edfa3-153">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="edfa3-154">hello toolog `stdout` e `stderr` dal contenitore, è necessario tooenable **registrazione contenitore Docker** in **log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="edfa3-154">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Abilitazione della registrazione][8]

![Utilizzo dei registri di Docker tooview Kudu][7]

<span data-ttu-id="edfa3-157">È possibile accedere hello SCM sito da **strumenti avanzati** in hello **gli strumenti di sviluppo** menu.</span><span class="sxs-lookup"><span data-stu-id="edfa3-157">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="edfa3-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="edfa3-158">Next Steps</span></span> ##

<span data-ttu-id="edfa3-159">Seguire i seguenti collegamenti tooget avviato con l'App Web in Linux hello.</span><span class="sxs-lookup"><span data-stu-id="edfa3-159">Follow hello following links tooget started with Web App on Linux.</span></span>   

* [<span data-ttu-id="edfa3-160">Introduzione tooAzure App Web in Linux</span><span class="sxs-lookup"><span data-stu-id="edfa3-160">Introduction tooAzure Web App on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="edfa3-161">Uso della configurazione PM2 per Node.js in App Web su Linux</span><span class="sxs-lookup"><span data-stu-id="edfa3-161">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](./app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="edfa3-162">Domande frequenti su App Web del Servizio app di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="edfa3-162">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<span data-ttu-id="edfa3-163">Pubblicare domande e dubbi nel [forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="edfa3-163">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
