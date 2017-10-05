---
title: Supporto SSH per App Web del Servizio app di Azure in Linux | Microsoft Docs
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
ms.openlocfilehash: feee7a5c91d213a6b0bfdaf264a4da4d9e79cbe7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="0e35d-104">Supporto SSH per App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="0e35d-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="0e35d-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0e35d-105">Overview</span></span>

<span data-ttu-id="0e35d-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) è un protocollo di rete di crittografia per l'uso di servizi di rete in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="0e35d-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="0e35d-107">Più comunemente viene usato per accedere in modo sicuro a un sistema da una riga di comando ed eseguire comandi amministrativi in remoto.</span><span class="sxs-lookup"><span data-stu-id="0e35d-107">It is most commonly used to log into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="0e35d-108">App Web in Linux offre il supporto SSH nel contenitore di app con ognuna delle immagini Docker predefinite usate per lo stack di runtime di nuove app web.</span><span class="sxs-lookup"><span data-stu-id="0e35d-108">Web App on Linux provides SSH support into the app container with each of the built-in Docker images used for the Runtime Stack of new web apps.</span></span> 

![Stack di runtime](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="0e35d-110">È anche possibile usare SSH con le immagini Docker personalizzate includendo il server SSH come parte dell'immagine e configurandolo come descritto in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="0e35d-110">You can also use SSH with your custom Docker images by including the SSH server as part of the image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="0e35d-111">Creare una connessione client</span><span class="sxs-lookup"><span data-stu-id="0e35d-111">Making a client connection</span></span>

<span data-ttu-id="0e35d-112">Per creare una connessione client SSH, è necessario avviare il sito principale.</span><span class="sxs-lookup"><span data-stu-id="0e35d-112">To make an SSH client connection, the main site must be started.</span></span> 

<span data-ttu-id="0e35d-113">Incollare l'endpoint di Gestione controllo codice sorgente, SCM, per l'app Web nel browser tramite il modulo seguente:</span><span class="sxs-lookup"><span data-stu-id="0e35d-113">Paste the Source Control Management (SCM) endpoint for your web app into your browser using the following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="0e35d-114">Se non lo si è già fatto, è necessario eseguire l'autenticazione con la sottoscrizione di Azure per la connessione.</span><span class="sxs-lookup"><span data-stu-id="0e35d-114">If you are not already authenticated, you are required to authenticate with your Azure subscription to connect.</span></span>

![Connessione SSH](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="0e35d-116">Supporto SSH con immagini Docker personalizzate</span><span class="sxs-lookup"><span data-stu-id="0e35d-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="0e35d-117">Affinché un'immagine Docker personalizzata supporti la comunicazione SSH tra il contenitore e il client nel portale di Azure, eseguire la procedura seguente per l'immagine Docker.</span><span class="sxs-lookup"><span data-stu-id="0e35d-117">In order for a custom Docker image to support SSH communication between the container and the client in the Azure portal, perform the following steps for your Docker image.</span></span> 

<span data-ttu-id="0e35d-118">Questa procedura viene mostrata nell'archivio del Servizio app di Azure come esempio [qui](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span><span class="sxs-lookup"><span data-stu-id="0e35d-118">These steps are are shown in the Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="0e35d-119">Includere l'installazione `openssh-server` nell'[istruzione `RUN`](https://docs.docker.com/engine/reference/builder/#run) in Dockerfile per l'immagine e impostare la password per l'account radice su `"Docker!"`.</span><span class="sxs-lookup"><span data-stu-id="0e35d-119">Include the `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in the Dockerfile for your image and set the password for the root account to `"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="0e35d-120">Questa configurazione non consente connessioni esterne al contenitore.</span><span class="sxs-lookup"><span data-stu-id="0e35d-120">This configuration does not allow external connections to the container.</span></span> <span data-ttu-id="0e35d-121">SSH è accessibile solo tramite il sito Kudu/sito, che viene autenticato tramite le credenziali di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="0e35d-121">SSH can only be accessed via the Kudu / SCM Site, which is authenticated using the publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="0e35d-122">Aggiungere un'[istruzione `COPY`](https://docs.docker.com/engine/reference/builder/#copy) a Dockerfile per copiare un file [sshd_config](http://man.openbsd.org/sshd_config) nella directory */etc/ssh/*.</span><span class="sxs-lookup"><span data-stu-id="0e35d-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) to the Dockerfile to copy a [sshd_config](http://man.openbsd.org/sshd_config) file to the */etc/ssh/* directory.</span></span> <span data-ttu-id="0e35d-123">Il file di configurazione deve essere basato sul file sshd_config nell'archivio GitHub di Azure-App-Service [qui](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span><span class="sxs-lookup"><span data-stu-id="0e35d-123">Your configuration file should be based on our sshd_config file in the Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0e35d-124">Per fare in modo che la connessione abbia esito positivo, il file *sshd_config* deve includere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="0e35d-124">The *sshd_config* file must include the following or the connection fails:</span></span> 
    > * <span data-ttu-id="0e35d-125">`Ciphers` deve includere almeno uno dei seguenti: `aes128-cbc,3des-cbc,aes256-cbc`.</span><span class="sxs-lookup"><span data-stu-id="0e35d-125">`Ciphers` must include at least one of the following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="0e35d-126">`MACs` deve includere almeno uno dei seguenti: `hmac-sha1,hmac-sha1-96`.</span><span class="sxs-lookup"><span data-stu-id="0e35d-126">`MACs` must include at least one of the following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="0e35d-127">Includere la porta 2222 nell'[istruzione `EXPOSE`](https://docs.docker.com/engine/reference/builder/#expose) per Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="0e35d-127">Include port 2222 in the [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for the Dockerfile.</span></span> <span data-ttu-id="0e35d-128">Anche se la password radice è nota, la porta 2222 non è accessibile da Internet.</span><span class="sxs-lookup"><span data-stu-id="0e35d-128">Although the root password is known, port 2222 cannot be accessed from the internet.</span></span> <span data-ttu-id="0e35d-129">È una porta interna accessibile solo dai contenitori all'interno della rete bridge di una rete virtuale privata.</span><span class="sxs-lookup"><span data-stu-id="0e35d-129">It is an internal only port accessible only by containers within the bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="0e35d-130">Assicurarsi di avviare il servizio SSH.</span><span class="sxs-lookup"><span data-stu-id="0e35d-130">Make sure to start the ssh service.</span></span> <span data-ttu-id="0e35d-131">Nell'esempio [qui](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) viene usato uno script della shell nella directory */bin*.</span><span class="sxs-lookup"><span data-stu-id="0e35d-131">The example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="0e35d-132">Dockerfile usa l'[istruzione `CMD`](https://docs.docker.com/engine/reference/builder/#cmd) per eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="0e35d-132">The Dockerfile uses the [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) to run the script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="0e35d-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0e35d-133">Next steps</span></span>
<span data-ttu-id="0e35d-134">Per altre informazioni su App Web in Linux, vedere i collegamenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="0e35d-134">See the following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="0e35d-135">È possibile pubblicare domande e dubbi nel [forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="0e35d-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="0e35d-136">Come usare un'immagine Docker personalizzata per App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="0e35d-136">How to use a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="0e35d-137">Uso della configurazione PM2 per Node.js in App Web su Linux</span><span class="sxs-lookup"><span data-stu-id="0e35d-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="0e35d-138">Uso di .NET Core in App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="0e35d-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="0e35d-139">Uso di Ruby in App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="0e35d-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="0e35d-140">Domande frequenti su App Web del Servizio app di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="0e35d-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

