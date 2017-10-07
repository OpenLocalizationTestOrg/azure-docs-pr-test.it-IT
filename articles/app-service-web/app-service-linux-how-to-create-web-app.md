---
title: aaaCreate di Azure web app in esecuzione in Linux | Documenti Microsoft
description: Flusso di lavoro per la creazione di un'app Web per App Web di Aure in Linux.
keywords: Servizio app di Azure, app Web, Linux, OSS
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: de1bd030345d5e2a8024012067b5bcaa2cca09dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a>Creare un'app Web di Azure eseguita in Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a>Usare l'app web di hello toocreate portale di Azure
È possibile iniziare a creare app web in Linux hello [portale di Azure](https://portal.azure.com) come illustrato nella seguente immagine hello:

![Avviare la creazione di un'app web nel portale di Azure hello][1]

Successivamente, hello **pannello Crea** verrà visualizzata come illustrato nella seguente immagine hello:

![pannello Crea Hello][2]

1. Assegnare all'app Web un nome.
2. Scegliere un gruppo di risorse esistente oppure crearne uno nuovo. (Vedere le aree disponibili in hello [sezione limitazioni](app-service-linux-intro.md).)
3. Scegliere un piano di servizio app di Azure esistente o crearne uno nuovo. (Vedere le note di piano di servizio App in hello [sezione limitazioni](app-service-linux-intro.md).)
4. Scegliere un'applicazione hello stack che si desidera toouse. È possibile scegliere tra diverse versioni di Node.js, PHP, .Net Core e Ruby.

Dopo aver creato l'applicazione hello, è possibile modificare stack dell'applicazione hello da impostazioni applicazione hello, come illustrato nella seguente immagine hello:

![Impostazioni dell'applicazione][3]

## <a name="deploy-your-web-app"></a>Distribuire l'app Web
Scelta di **opzioni di distribuzione** da offre portale di gestione hello hello opzione toouse locale Git o GitHub repository toodeploy l'applicazione. Hello restanti istruzioni hello sono simili toothose per un'app web non Linux. È possibile seguire le istruzioni hello [distribuzione Git locale](app-service-deploy-local-git.md) o [distribuzione continua](app-service-continuous-deployment.md) toodeploy l'app.

È anche possibile utilizzare tooupload FTP del sito tooyour applicazione. È possibile ottenere endpoint FTP hello per le app web da diagnostica di hello sezione registri come illustrato nella seguente immagine hello:

![Log di diagnostica][4]

## <a name="next-steps"></a>Passaggi successivi
* [Definizione di App Web di Azure in Linux](app-service-linux-intro.md)
* [Uso della configurazione PM2 per Node.js in App Web su Linux](app-service-linux-using-nodejs-pm2.md)
* [Uso di Ruby in App Web del Servizio app di Azure in Linux](app-service-linux-ruby-get-started.md)
* [Domande frequenti su App Web del Servizio app di Azure su Linux](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
