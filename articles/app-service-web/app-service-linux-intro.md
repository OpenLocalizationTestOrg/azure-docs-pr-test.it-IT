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
# <a name="introduction-to-azure-web-app-on-linux"></a>Introduzione ad App Web di Azure in Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Panoramica
I clienti possono usare App Web in Linux per ospitare app Web in modo nativo in Linux per stack di applicazioni supportate. La sezione seguente elenca gli stack di applicazioni attualmente supportati. 

## <a name="features"></a>Funzionalità
App Web in Linux supporta attualmente gli stack di applicazioni seguenti:

* Node.js
    * 4.4
    * 4.5
    * 6.2
    * 6.6
    * 6.9
    * 6.10
    * 6.11
    * 8.0
    * 8.1
* PHP
    * 5.6
    * 7.0
* .Net Core
    * 1.0
    * 1.1
* Ruby
    * 2.3

I clienti possono distribuire le applicazioni tramite:

* FTP
* Repository Git locale
* GitHub
* Bitbucket

Per il ridimensionamento delle applicazioni:

* I clienti possono aumentare e ridurre le prestazioni delle app Web modificando il livello nel piano di servizio app
* I clienti possono scalare orizzontalmente le applicazioni ed eseguire più istanze di un'app entro i confini dello SKU

Per Kudu, alcune delle funzionalità di base:

* Ambienti
* Deployments
* Console di base
* SSH

Per DevOps:

* Ambienti di staging
* ACR e implementazione continua/distribuzione continua di DockerHub

## <a name="limitations"></a>Limitazioni
Il portale di Azure mostra solo le funzionalità che possono essere usate attualmente per App Web in Linux e nasconde le altre. Man mano che verranno abilitate nuove funzionalità, queste diventeranno visibili nel portale.

Alcune funzionalità, quali l'integrazione delle reti virtuali, l'autenticazione di Azure Active Directory o di terze parti o le estensioni del sito Kudu, non sono ancora disponibili. Man mano che queste funzionalità dinvetano disponibili, la documentazione verrà aggiornata e le modifiche pubblicate nei blog.

Questa anteprima pubblica è attualmente disponibile solo nelle aree seguenti:

* Stati Uniti occidentali
* Stati Uniti Orientali
* Europa occidentale
* Europa settentrionale
* Stati Uniti centro-meridionali
* Stati Uniti centro-settentrionali
* Asia sudorientale
* Asia orientale
* Australia orientale
* Giappone orientale
* Brasile meridionale
* India meridionale

App Web in Linux è supportato solo nei piani di servizio app dedicati e non ha un livello Gratuito o Condiviso. I piani di servizio app per le app Web normali e di Linux si escludono a vicenda, quindi non è possibile creare un'app Web di Linux in un piano di servizio app non Linux.

Le app Web in Linux devono essere create in un gruppo di risorse che non contiene app Web non Linux nella stessa area.

## <a name="troubleshooting"></a>Risoluzione dei problemi ##

Quando non è possibile avviare l'applicazione o si desidera controllare il log dall'app, controllare i log di Docker nella directory LogFiles. È possibile accedere a questa directory tramite il sito SCM o tramite FTP.
Per registrare `stdout` e `stderr` dal contenitore, è necessario abilitare **Registrazione del contenitore Docker** in **Log di diagnostica**.

![Abilitazione della registrazione][2]

![Uso di Kudu per visualizzare i log di Docker][1]

È possibile accedere al sito SCM da **Strumenti avanzati** nel menu **Strumenti di sviluppo**.

## <a name="next-steps"></a>Passaggi successivi
Vedere i collegamenti seguenti per iniziare a usare il servizio app in Linux. È possibile pubblicare domande e dubbi nel [forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Come usare un'immagine Docker personalizzata per App Web di Azure in Linux](app-service-linux-using-custom-docker-image.md)
* [Uso della configurazione PM2 per Node.js in App Web su Linux](app-service-linux-using-nodejs-pm2.md)
* [Uso di .NET Core in App Web del Servizio app di Azure in Linux](app-service-linux-using-dotnetcore.md)
* [Uso di Ruby in App Web del Servizio app di Azure in Linux](app-service-linux-ruby-get-started.md)
* [Domande frequenti su App Web del Servizio app di Azure su Linux](app-service-linux-faq.md)
* [SSH support for Azure Web App on Linux](./app-service-linux-ssh-support.md) (Supporto SSH per App Web di Azure in Linux)
* [Configurare gli ambienti di gestione temporanea nel Servizio app di Azure](./web-sites-staged-publishing.md)
* [Docker Hub Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md) (Distribuzione continua dell'hub Docker con App Web di Azure in Linux)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png