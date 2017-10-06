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
# <a name="ssh-support-for-azure-web-app-on-linux"></a>Supporto SSH per App Web di Azure in Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Panoramica

[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) è un protocollo di rete di crittografia per l'uso di servizi di rete in modo sicuro. È toolog più comunemente usate in un sistema in modalità remota in modo sicuro da una riga di comando ed eseguire i comandi amministrativi in modalità remota.

Web App in Linux fornisce il supporto SSH nel contenitore di app hello con ciascuna delle immagini Docker incorporate hello utilizzate per hello dello Stack di Runtime di nuove app web. 

![Stack di runtime](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

È possibile utilizzare anche SSH con immagini Docker personalizzate tra cui server SSH hello come parte dell'immagine di hello e configurarlo come descritto in questo argomento.



## <a name="making-a-client-connection"></a>Creare una connessione client

una connessione di client SSH, del sito principale hello toomake deve essere avviato. 

Incollare l'endpoint di gestione di controllo di origine (SCM) hello per le app web nel browser utilizzando hello seguente formato:

        https://<your sitename>.scm.azurewebsites.net/webssh/host

Se non già autenticato, è necessario tooauthenticate tooconnect la sottoscrizione di Azure.

![Connessione SSH](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a>Supporto SSH con immagini Docker personalizzate

Affinché una personalizzate Docker immagine toosupport SSH di comunicazione tra il contenitore di hello e client hello in hello portale di Azure, eseguire hello alla procedura seguente per l'immagine di Docker. 

Questi passaggi sono presenti in hello repository di servizio App di Azure ad esempio [qui](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).

1. Includere hello `openssh-server` installazione in [ `RUN` istruzione](https://docs.docker.com/engine/reference/builder/#run) in hello Dockerfile per l'immagine e hello password per l'account radice hello troppo`"Docker!"`. 

    > [!NOTE] 
    > Questa configurazione non contenitore toohello connessioni esterne. SSH è accessibile solo tramite hello Kudu / hello di sito di Gestione controllo servizi, che viene autenticato utilizzando le credenziali di pubblicazione.

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. Aggiungere un [ `COPY` istruzione](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy un [sshd_config](http://man.openbsd.org/sshd_config) file toohello *e così viassh/* directory. Il file di configurazione deve essere basato sul nostro file sshd_config nel repository GitHub di servizio App di Azure hello [qui](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).

    > [!NOTE] 
    > Hello *sshd_config* file deve includere il seguente hello o hello connessione ha esito negativo: 
    > * `Ciphers`deve includere almeno una delle seguenti hello: `aes128-cbc,3des-cbc,aes256-cbc`.
    > * `MACs`deve includere almeno una delle seguenti hello: `hmac-sha1,hmac-sha1-96`.

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. Includere porta 2222 nell'hello [ `EXPOSE` istruzione](https://docs.docker.com/engine/reference/builder/#expose) per hello Dockerfile. Anche se la password radice hello è noto, non è possibile accedere da hello porta 2222 internet. Si tratta di un'unica porta interna accessibile solo dai contenitori all'interno di un bridge di rete hello di una rete virtuale privata.

    ```docker
    EXPOSE 2222 80
    ```

4. Verificare che hello toostart ssh del servizio. esempio Hello [qui](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) utilizza uno script della shell in */bin* directory.

    ```bash
    #!/bin/bash
    service ssh start
    ```

    Hello Dockerfile utilizza hello [ `CMD` istruzione](https://docs.docker.com/engine/reference/builder/#cmd) script hello toorun.

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a>Passaggi successivi
Vedere i seguenti collegamenti per ulteriori informazioni sull'App Web in Linux hello. È possibile pubblicare domande e dubbi nel [forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Come immagine di toouse una Docker personalizzata per l'App Web di Azure in Linux](app-service-linux-using-custom-docker-image.md)
* [Uso della configurazione PM2 per Node.js in App Web su Linux](app-service-linux-using-nodejs-pm2.md)
* [Uso di .NET Core in App Web di Azure in Linux](app-service-linux-using-dotnetcore.md)
* [Uso di Ruby in App Web di Azure in Linux](app-service-linux-ruby-get-started.md)
* [Domande frequenti su App Web del Servizio app di Azure su Linux](app-service-linux-faq.md)

