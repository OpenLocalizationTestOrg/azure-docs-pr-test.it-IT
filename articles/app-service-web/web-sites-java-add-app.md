---
title: Distribuire l'applicazione di esempio nelle app Web di Servizio app di Azure
description: "In questa esercitazione viene illustrato come aggiungere una pagina o applicazione per l'istanza di Azure applicazione servizio Web App è già configurato per l'utilizzo di Java."
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
ms.openlocfilehash: c28e7c499ed02b759df580f4b14a971b6aec5b67
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-java-application-to-azure-app-service-web-apps"></a><span data-ttu-id="8376e-103">Distribuire l'applicazione di esempio nelle app Web di Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="8376e-103">Add a Java application to Azure App Service Web Apps</span></span>
<span data-ttu-id="8376e-104">Dopo aver inizializzato l'app Web Java nel [servizio app di Azure][Azure App Service] come indicato in [Creazione di un'app Web Java nel servizio app di Azure](web-sites-java-get-started.md), è possibile caricare l'applicazione inserendo il file WAR nella cartella **webapps**.</span><span class="sxs-lookup"><span data-stu-id="8376e-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md), you can upload your application by placing your WAR in the **webapps** folder.</span></span>

<span data-ttu-id="8376e-105">Il percorso della cartella **webapps** varia a seconda della configurazione del sito Web.</span><span class="sxs-lookup"><span data-stu-id="8376e-105">The navigation path to the **webapps** folder differs based on how you set up your Web Apps instance.</span></span>

* <span data-ttu-id="8376e-106">Se si configura il sito Web usando Azure Marketplace, il percorso della cartella **webapps** sarà nel formato **d:\home\site\wwwroot\bin\application\_server\webapps**, dove **application\_server** è il nome del server applicazioni usato per l'istanza di App Web.</span><span class="sxs-lookup"><span data-stu-id="8376e-106">If you set up your web app by using the Azure Marketplace, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is the name of the application server in effect for your Web Apps instance.</span></span> 
* <span data-ttu-id="8376e-107">Se si configura il sito Web usando l'interfaccia utente di configurazione di Azure, il percorso della cartella **webapps** sarà nel formato **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="8376e-107">If you set up your web app by using the Azure configuration UI, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\webapps**.</span></span> 

<span data-ttu-id="8376e-108">Si noti che è possibile usare il controllo del codice sorgente per caricare l'applicazione o le pagine Web, anche negli [scenari di integrazione continua](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="8376e-108">Note that you can use source control to upload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="8376e-109">È anche possibile usare l'FTP per caricare le pagine web o l'applicazione. Per altre informazioni sulla distribuzione delle applicazioni tramite FTP, vedere [Distribuire l'app nel Servizio app di Azure].</span><span class="sxs-lookup"><span data-stu-id="8376e-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app to Azure App Service].</span></span>

<span data-ttu-id="8376e-110">Dopo avere caricato il file WAR nella cartella **webapps** , il server applicazioni Tomcat ne rileverà l'aggiunta e lo caricherà automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8376e-110">Note for Tomcat web apps: Once you've uploaded your WAR file to the **webapps** folder, the Tomcat application server will detect that you've added it and will automatically load it.</span></span> <span data-ttu-id="8376e-111">Si noti che se vengono copiati file (eccetto i file WAR) nella directory ROOT, è necessario riavviare il server applicazioni per utilizzarli.</span><span class="sxs-lookup"><span data-stu-id="8376e-111">Note that if you copy files (other than WAR files) to the ROOT directory, the application server will need to be restarted before those files are used.</span></span> <span data-ttu-id="8376e-112">La funzionalità di caricamento automatico per i siti Web Java Tomcat in esecuzione in Azure si basa su un nuovo file WAR aggiunto o su nuovi file o nuove directory create nella cartella **webapps** .</span><span class="sxs-lookup"><span data-stu-id="8376e-112">The autoload functionality for the Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added to the **webapps** folder.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="8376e-113">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="8376e-113">See Also</span></span>
<span data-ttu-id="8376e-114">Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure].</span><span class="sxs-lookup"><span data-stu-id="8376e-114">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

[<span data-ttu-id="8376e-115">application-insights-app-insights-java-get-started</span><span class="sxs-lookup"><span data-stu-id="8376e-115">application-insights-app-insights-java-get-started</span></span>](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

<span data-ttu-id="8376e-116">[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="8376e-116">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
<span data-ttu-id="8376e-117">[Distribuire l'app nel Servizio app di Azure]: ./web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="8376e-117">[Deploy your app to Azure App Service]: ./web-sites-deploy.md</span></span>
