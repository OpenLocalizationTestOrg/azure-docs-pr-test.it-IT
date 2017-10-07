---
title: aaaAdd un tooAzure applicazione Java App del servizio Web App
description: "Questa esercitazione viene illustrato come tooadd un'istanza tooyour pagina o un'applicazione Azure applicazione servizio Web App è già configurato toouse Java."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9b46528b-e2d0-4f26-b8d7-af94bd8c31ef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2feb464b2933921ad2887779a6b7589634e2e2f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-java-application-tooazure-app-service-web-apps"></a>Aggiungere un tooAzure applicazione Java App del servizio Web App
Dopo aver inizializzato l'app web Java in [Azure App Service] [ Azure App Service] come illustrato in [creare un'app web Java in Azure App Service](web-sites-java-get-started.md), è possibile caricare l'applicazione inserendo la GUERRA hello **webapps** cartella.

Hello toohello percorso di navigazione **webapps** cartella varia in base al come impostare l'istanza di App Web.

* Se si configura l'app web utilizzando hello Azure Marketplace, hello percorso toohello **webapps** cartella è nel formato di hello **d:\home\site\wwwroot\bin\application\_server\webapps**, dove **applicazione\_server** nome hello del server applicazioni hello attivo per l'istanza di App Web. 
* Se si configura l'app web utilizzando l'interfaccia utente di configurazione Azure hello, hello percorso toohello **webapps** cartella è nel formato di hello **d:\home\site\wwwroot\webapps**. 

Si noti che è possibile utilizzare tooupload di controllo di origine, l'applicazione o pagine web, tra cui [scenari di integrazione continua](app-service-continuous-deployment.md). FTP è anche un'opzione per caricare l'applicazione o pagine web. Per ulteriori informazioni sulla distribuzione delle applicazioni tramite FTP, vedere [distribuire il servizio App di tooAzure app].

Nota per le applicazioni web Tomcat: dopo aver caricato il toohello file WAR **webapps** cartella, il server applicazioni Tomcat hello rileverà che è stato aggiunto e verrà caricato automaticamente. Si noti che se si copia una directory radice dei file (ad eccezione dei file WAR) toohello, server applicazioni hello sarà necessario toobe riavviare tali file vengono utilizzati. funzionalità autoload Hello per le app web di Java Tomcat hello in esecuzione in Azure è basata su un nuovo file WAR da aggiungere oppure toohello di aggiungere nuovi file o directory **webapps** cartella. 

<a name="see-also"></a>

## <a name="see-also"></a>Vedere anche
Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure].

[application-insights-app-insights-java-get-started](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[distribuire il servizio App di tooAzure app]: ./web-sites-deploy.md
