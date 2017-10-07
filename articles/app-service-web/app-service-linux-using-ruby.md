---
title: aaaUsing Ruby in App Azure del servizio Web App in Linux | Documenti Microsoft
description: Uso di Ruby in App Web del Servizio app di Azure in Linux.
keywords: Servizio app di Azure, app Web, domande frequenti, Linux, OSS, Ruby
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 45692cb3bf1da9ff65b9466055029bfaef8b7d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a>Uso di Ruby in App Web in Linux #

Con hello più recente aggiornamento tooour back-end, è stato introdotto il supporto per v.2.3 Ruby. Impostazione di configurazione hello dell'app web Linux, è possibile modificare stack dell'applicazione hello.

## <a name="using-hello-azure-portal"></a>Utilizzo di hello portale di Azure ##

Menu nuovo di hello di hello [portale di Azure](https://portal.azure.com), è possibile scegliere toocreate un'App Web in Linux da hello Web + opzione cellulare come illustrato nella seguente immagine hello:

![Avviare la creazione di un'app web nel portale di Azure hello][1]

Successivamente, hello **pannello Crea** verrà visualizzata come illustrato nella seguente immagine hello:

![pannello Crea Hello][2]

1. Assegnare all'app Web un nome.
2. Scegliere un gruppo di risorse esistente oppure crearne uno nuovo. (Vedere le aree disponibili in hello [sezione limitazioni](app-service-linux-intro.md).)
3. Scegliere un piano di servizio app di Azure esistente o crearne uno nuovo. (Vedere le note di piano di servizio App in hello [sezione limitazioni](app-service-linux-intro.md).)
4. Scegliere gli stack di Runtime incorporata hello hello Ruby.

Dopo aver creato l'app web Ruby, è possibile distribuire tooit utilizzando Git o FTP.

toolearn altre informazioni sulla creazione di un'app Ruby, controllare hello [Guida introduttiva get](app-service-linux-ruby-get-started.md)

## <a name="next-steps"></a>Passaggi successivi
* [Definizione di App Web in Linux](app-service-linux-intro.md)
* [TooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md)
* [Domande frequenti su App Web del Servizio app di Azure su Linux](app-service-linux-faq.md)
* [Creare un'app Ruby con App Web di Azure in Linux](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png