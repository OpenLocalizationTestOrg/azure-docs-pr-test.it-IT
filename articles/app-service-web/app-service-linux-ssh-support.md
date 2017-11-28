---
title: il supporto per l'App Web di Azure App Service in Linux aaaSSH | Documenti Microsoft
description: Informazioni sull'uso di SSH con App Web di Azure in Linux.
keywords: Servizio app di Azure, app Web, Linux, OSS
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 66f9988f-8ffa-414a-9137-3a9b15a5573c
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: wesmc
ms.openlocfilehash: e00be6d4631e8936a2a8bc106da1fc06237a4b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="46cc5-104">Supporto SSH per App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="46cc5-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="46cc5-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="46cc5-105">Overview</span></span>

<span data-ttu-id="46cc5-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) è un protocollo di rete di crittografia per l'uso di servizi di rete in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="46cc5-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="46cc5-107">È toolog più comunemente usate in un sistema in modalità remota in modo sicuro da una riga di comando ed eseguire i comandi amministrativi in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="46cc5-107">It is most commonly used toolog into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="46cc5-108">Web App in Linux fornisce il supporto SSH nel contenitore di app hello con ciascuna delle immagini Docker incorporate hello utilizzate per hello dello Stack di Runtime di nuove app web.</span><span class="sxs-lookup"><span data-stu-id="46cc5-108">Web App on Linux provides SSH support into hello app container with each of hello built-in Docker images used for hello Runtime Stack of new web apps.</span></span> 

![Stack di runtime](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="46cc5-110">È possibile utilizzare anche SSH con immagini Docker personalizzate tra cui server SSH hello come parte dell'immagine di hello e configurarlo come descritto in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="46cc5-110">You can also use SSH with your custom Docker images by including hello SSH server as part of hello image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="46cc5-111">Creare una connessione client</span><span class="sxs-lookup"><span data-stu-id="46cc5-111">Making a client connection</span></span>

<span data-ttu-id="46cc5-112">una connessione di client SSH, del sito principale hello toomake deve essere avviato.</span><span class="sxs-lookup"><span data-stu-id="46cc5-112">toomake an SSH client connection, hello main site must be started.</span></span> 

<span data-ttu-id="46cc5-113">Incollare l'endpoint di gestione di controllo di origine (SCM) hello per le app web nel browser utilizzando hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="46cc5-113">Paste hello Source Control Management (SCM) endpoint for your web app into your browser using hello following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="46cc5-114">Se non già autenticato, è necessario tooauthenticate tooconnect la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="46cc5-114">If you are not already authenticated, you are required tooauthenticate with your Azure subscription tooconnect.</span></span>

![Connessione SSH](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="46cc5-116">Supporto SSH con immagini Docker personalizzate</span><span class="sxs-lookup"><span data-stu-id="46cc5-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="46cc5-117">Affinché una personalizzate Docker immagine toosupport SSH di comunicazione tra il contenitore di hello e client hello in hello portale di Azure, eseguire hello alla procedura seguente per l'immagine di Docker.</span><span class="sxs-lookup"><span data-stu-id="46cc5-117">In order for a custom Docker image toosupport SSH communication between hello container and hello client in hello Azure portal, perform hello following steps for your Docker image.</span></span> 

<span data-ttu-id="46cc5-118">Questi passaggi sono presenti in hello repository di servizio App di Azure ad esempio [qui](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span><span class="sxs-lookup"><span data-stu-id="46cc5-118">These steps are are shown in hello Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="46cc5-119">Includere hello `openssh-server` installazione in [ `RUN` istruzione](https://docs.docker.com/engine/reference/builder/#run) in hello Dockerfile per l'immagine e hello password per l'account radice hello troppo`"Docker!"`.</span><span class="sxs-lookup"><span data-stu-id="46cc5-119">Include hello `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in hello Dockerfile for your image and set hello password for hello root account too`"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="46cc5-120">Questa configurazione non contenitore toohello connessioni esterne.</span><span class="sxs-lookup"><span data-stu-id="46cc5-120">This configuration does not allow external connections toohello container.</span></span> <span data-ttu-id="46cc5-121">SSH è accessibile solo tramite hello Kudu / hello di sito di Gestione controllo servizi, che viene autenticato utilizzando le credenziali di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="46cc5-121">SSH can only be accessed via hello Kudu / SCM Site, which is authenticated using hello publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="46cc5-122">Aggiungere un [ `COPY` istruzione](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy un [sshd_config](http://man.openbsd.org/sshd_config) file toohello *e così viassh/* directory.</span><span class="sxs-lookup"><span data-stu-id="46cc5-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy a [sshd_config](http://man.openbsd.org/sshd_config) file toohello */etc/ssh/* directory.</span></span> <span data-ttu-id="46cc5-123">Il file di configurazione deve essere basato sul nostro file sshd_config nel repository GitHub di servizio App di Azure hello [qui](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span><span class="sxs-lookup"><span data-stu-id="46cc5-123">Your configuration file should be based on our sshd_config file in hello Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="46cc5-124">Hello *sshd_config* file deve includere il seguente hello o hello connessione ha esito negativo:</span><span class="sxs-lookup"><span data-stu-id="46cc5-124">hello *sshd_config* file must include hello following or hello connection fails:</span></span> 
    > * <span data-ttu-id="46cc5-125">`Ciphers`deve includere almeno una delle seguenti hello: `aes128-cbc,3des-cbc,aes256-cbc`.</span><span class="sxs-lookup"><span data-stu-id="46cc5-125">`Ciphers` must include at least one of hello following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="46cc5-126">`MACs`deve includere almeno una delle seguenti hello: `hmac-sha1,hmac-sha1-96`.</span><span class="sxs-lookup"><span data-stu-id="46cc5-126">`MACs` must include at least one of hello following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="46cc5-127">Includere porta 2222 nell'hello [ `EXPOSE` istruzione](https://docs.docker.com/engine/reference/builder/#expose) per hello Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="46cc5-127">Include port 2222 in hello [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for hello Dockerfile.</span></span> <span data-ttu-id="46cc5-128">Anche se la password radice hello è noto, non è possibile accedere da hello porta 2222 internet.</span><span class="sxs-lookup"><span data-stu-id="46cc5-128">Although hello root password is known, port 2222 cannot be accessed from hello internet.</span></span> <span data-ttu-id="46cc5-129">Si tratta di un'unica porta interna accessibile solo dai contenitori all'interno di un bridge di rete hello di una rete virtuale privata.</span><span class="sxs-lookup"><span data-stu-id="46cc5-129">It is an internal only port accessible only by containers within hello bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="46cc5-130">Verificare che hello toostart ssh del servizio.</span><span class="sxs-lookup"><span data-stu-id="46cc5-130">Make sure toostart hello ssh service.</span></span> <span data-ttu-id="46cc5-131">esempio Hello [qui](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) utilizza uno script della shell in */bin* directory.</span><span class="sxs-lookup"><span data-stu-id="46cc5-131">hello example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="46cc5-132">Hello Dockerfile utilizza hello [ `CMD` istruzione](https://docs.docker.com/engine/reference/builder/#cmd) script hello toorun.</span><span class="sxs-lookup"><span data-stu-id="46cc5-132">hello Dockerfile uses hello [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="46cc5-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="46cc5-133">Next steps</span></span>
<span data-ttu-id="46cc5-134">Vedere i seguenti collegamenti per ulteriori informazioni sull'App Web in Linux hello.</span><span class="sxs-lookup"><span data-stu-id="46cc5-134">See hello following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="46cc5-135">È possibile pubblicare domande e dubbi nel [forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="46cc5-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="46cc5-136">Come immagine di toouse una Docker personalizzata per l'App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="46cc5-136">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="46cc5-137">Uso della configurazione PM2 per Node.js in App Web su Linux</span><span class="sxs-lookup"><span data-stu-id="46cc5-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="46cc5-138">Uso di .NET Core in App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="46cc5-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="46cc5-139">Uso di Ruby in App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="46cc5-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="46cc5-140">Domande frequenti su App Web del Servizio app di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="46cc5-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

