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
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a>Uso di un'immagine Docker personalizzata per App Web di Azure in Linux #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Il servizio app fornisce stack di applicazioni predefiniti in Linux con il supporto per versioni specifiche, ad esempio PHP 7.0 e Node.js 4.5. Servizio App in Linux Usa i contenitori di Docker toohost questi predefinite stack di applicazioni. È anche possibile utilizzare un personalizzato toodeploy immagine Docker nello stack di applicazione tooan di app web che non è già stato definito in Azure. Le immagini Docker personalizzate possono essere ospitate in un repository Docker pubblico o privato.


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a>Procedura: Impostare un'immagine Docker personalizzata per un'app Web
È possibile impostare l'immagine Docker personalizzata hello per le nuove e applicazioni Web esistenti. Quando si crea un'app web in Linux in hello [portale di Azure](https://portal.azure.com/#create/Microsoft.AppSvcLinux), fare clic su **Configura contenitore** tooset un'immagine Docker personalizzata:

![Immagine Docker personalizzata per una nuova app Web in Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a>Procedura: usare un'immagine Docker personalizzata dall'hub Docker ##
un'immagine Docker personalizzata dall'Hub Docker toouse:

1. In hello [portale di Azure](https://portal.azure.com), individuare l'app web in Linux, quindi **impostazioni** fare clic su **contenitore Docker**.

2.  Selezionare **Hub Docker** come hello **origine dell'immagine**, quindi fare clic su **pubblica** o **privata** e hello tipo **immagine e nome del tag facoltativo**, ad esempio `node:4.5`. Hello **comando di avvio** è impostato automaticamente in base alle definizione nel file di immagine Docker hello, ma è possibile impostare i comandi.  

    ![Configurare l'immagine del repository pubblico dell'hub Docker][2]

    Quando l'immagine è da un archivio privato, è necessario anche tooenter hello Hub Docker credenziali (**nome utente account di accesso** e **Password**) per il repository di hello privato Hub Docker.

    ![Configurare l'immagine del repository privato dell'hub Docker][3]

3. Dopo aver configurato il contenitore di hello, fare clic su **salvare**.

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a>Come immagine di toouse una Docker da un registro di sistema immagine privata ##
toouse un'immagine personalizzata di Docker dal Registro di sistema immagine privata:

1. In hello [portale di Azure](https://portal.azure.com), individuare l'app web in Linux, quindi **impostazioni** fare clic su **contenitore Docker**.

2.  Fare clic su **registro privata** come hello **origine dell'immagine**. Immettere hello **immagine e il nome di tag facoltativo**, **URL del Server** per hello privato del Registro di sistema, insieme alle credenziali hello (**nome utente account di accesso** e **Password** ). Fare clic su **Salva**.

    ![Configurare l'immagine Docker dal registro di sistema privato][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a>Procedura: impostare hello porta utilizzata dall'immagine Docker ##

Quando si utilizza un'immagine Docker personalizzata per l'app web, è possibile utilizzare hello `WEBSITES_PORT` variabile di ambiente nel Dockerfile che viene aggiunto toohello generato contenitore. Prendere in considerazione hello esempio di un file di docker per un'applicazione Ruby seguente:

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

Ultima riga di comando hello, è possibile visualizzare che tale variabile di ambiente WEBSITES_PORT hello viene passato in fase di esecuzione. Tenere presente che la distinzione tra maiuscole e minuscole è importante nei comandi.

In precedenza si utilizzava piattaforma hello `PORT` app impostazione, si intende utilizzare hello toodeprecate questa impostazione di app e spostare toousing `WEBSITES_PORT` in modo esclusivo.

Quando si utilizza un'immagine Docker esistente compilata da un altro utente, potrebbe essere necessario toospecify una porta diversa dalla porta 80 per un'applicazione hello. tooconfigure hello porta, aggiungere un'impostazione dell'applicazione denominata `WEBSITES_PORT` con valore hello, come illustrato di seguito:

![Configurare l'impostazione app PORT per l'immagine Docker personalizzata][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a>Procedura: impostare l'ora di avvio hello per l'immagine di Docker ##

Per impostazione predefinita, se il contenitore non viene avviato prima di 230 secondi, piattaforma hello riavvierà il contenitore. Se l'immagine personalizzata di Docker viene avviato in più di 230 secondi, è possibile utilizzare hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app impostazione, il valore di hello per questa impostazione è espresso in secondi, in questo modo sarà hello piattaforma tenere il contenitore in esecuzione prima di riavviarlo. valore predefinito di Hello è 230 secondi e max hello consentito è 600 secondi.

## <a name="how-to-unmount-hello-platform-provided-storage"></a>Procedura: smontare archiviazione fornita dalla piattaforma hello ##

Per impostazione predefinita, la piattaforma hello esegue il montaggio di toohello di condivisione di un archivio permanente `\home\` directory. Se l'immagine del contenitore non necessita di una condivisione persistente, è possibile disabilitare il montaggio che l'archiviazione per l'impostazione hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app impostazione troppo`false`. Sarà comunque possibile archiviazione toothat access dal sito scm hello e tutti i log di Docker (se abilitati) verranno scritto il file di log toohello generati dalla piattaforma hello.

## <a name="how-to-switch-back-toousing-a-built-in-image"></a>Procedura: tornare toousing un'immagine incorporata ##

tooswitch da toousing un'immagine personalizzata un'immagine incorporata tramite:

1. In hello [portale di Azure](https://portal.azure.com), individuare l'app web in Linux, quindi **impostazioni** fare clic su **servizio App**.

2. Selezionare il **Stack di Runtime** toouse per immagine incorporata hello, quindi fare clic su **salvare**. 

![Configurare l'immagine Docker predefinita][5]


## <a name="troubleshooting"></a>Risoluzione dei problemi ##

Quando l'applicazione non riesce toostart con l'immagine personalizzata di Docker, controllare hello che docker log nella directory LogFiles hello. È possibile accedere a questa directory tramite il sito SCM o tramite FTP.
hello toolog `stdout` e `stderr` dal contenitore, è necessario tooenable **registrazione contenitore Docker** in **log di diagnostica**.

![Abilitazione della registrazione][8]

![Utilizzo dei registri di Docker tooview Kudu][7]

È possibile accedere hello SCM sito da **strumenti avanzati** in hello **gli strumenti di sviluppo** menu.

## <a name="next-steps"></a>Passaggi successivi ##

Seguire i seguenti collegamenti tooget avviato con l'App Web in Linux hello.   

* [Introduzione tooAzure App Web in Linux](./app-service-linux-intro.md)
* [Uso della configurazione PM2 per Node.js in App Web su Linux](./app-service-linux-using-nodejs-pm2.md)
* [Domande frequenti su App Web del Servizio app di Azure su Linux](app-service-linux-faq.md)

Pubblicare domande e dubbi nel [forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
