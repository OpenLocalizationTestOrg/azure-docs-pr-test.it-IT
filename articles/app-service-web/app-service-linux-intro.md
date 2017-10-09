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
# <a name="introduction-tooazure-web-app-on-linux"></a>Introduzione tooAzure App Web in Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Panoramica
I clienti possono utilizzare App Web nelle App web toohost di Linux in modo nativo in Linux per gli stack di applicazioni supportate. Hello nella sezione seguente sono elencati gli stack di applicazione hello che sono attualmente supportati. 

## <a name="features"></a>Funzionalità
Web App in Linux supporta attualmente hello stack di applicazioni seguenti:

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

* I clienti adattabile alto e verso il basso le applicazioni web modificando il livello di hello del piano di servizio App
* I clienti possono scalabilità delle applicazioni ed eseguire più istanze di app entro confini hello della loro SKU

Per Kudu, alcune delle funzionalità di base hello:

* Ambienti
* Deployments
* Console di base
* SSH

Per DevOps:

* Ambienti di staging
* ACR e implementazione continua/distribuzione continua di DockerHub

## <a name="limitations"></a>Limitazioni
Hello portale di Azure Mostra solo le funzionalità utilizzabili per l'App Web in Linux e nasconde rest hello. Come si abilita più funzionalità, saranno visibili nel portale di hello.

Alcune funzionalità, quali l'integrazione delle reti virtuali, l'autenticazione di Azure Active Directory o di terze parti o le estensioni del sito Kudu, non sono ancora disponibili. Una volta queste funzionalità sono disponibili, Microsoft aggiornerà la documentazione e il blog sulle modifiche hello.

Questa versione di anteprima pubblica è attualmente disponibile solo in hello seguenti aree:

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

Web App in Linux è supportata solo nei piani di servizio app dedicato hello e non dispone di un livello condiviso o disponibile. I piani di servizio app per le app Web normali e di Linux si escludono a vicenda, quindi non è possibile creare un'app Web di Linux in un piano di servizio app non Linux.

App in Linux Web deve essere creata in un gruppo di risorse che non contiene App web non Linux in hello stessa area.

## <a name="troubleshooting"></a>Risoluzione dei problemi ##

Quando l'applicazione non riesce toostart o si desidera la registrazione di hello toocheck dall'app, controllare hello che docker log nella directory LogFiles hello. È possibile accedere a questa directory tramite il sito SCM o tramite FTP.
hello toolog `stdout` e `stderr` dal contenitore, è necessario tooenable **registrazione contenitore Docker** in **log di diagnostica**.

![Abilitazione della registrazione][2]

![Utilizzo dei registri di Docker tooview Kudu][1]

È possibile accedere hello SCM sito da **strumenti avanzati** in hello **gli strumenti di sviluppo** menu.

## <a name="next-steps"></a>Passaggi successivi
Vedere hello seguendo i collegamenti tooget avviato con il servizio App in Linux. È possibile pubblicare domande e dubbi nel [forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Come immagine di toouse una Docker personalizzata per l'App Web di Azure in Linux](app-service-linux-using-custom-docker-image.md)
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