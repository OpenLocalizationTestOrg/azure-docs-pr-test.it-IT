---
title: risorse della documentazione di processi Web aaaAzure
description: Risorse per l'apprendimento come toouse processi Web di Azure e hello Azure WebJobs SDK.
services: app-service
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: ed005e56-4334-4641-a5e5-15435c2be36b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/25/2017
ms.author: glenga
ms.openlocfilehash: 6616a9d97c9637ec64cb8743dded6ba409a521ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-webjobs-documentation-resources"></a>Risorse di documentazione di Processi Web di Azure
## <a name="overview"></a>Panoramica
Questo argomento include collegamenti a risorse toodocumentation sul toouse processi Web di Azure e hello Azure WebJobs SDK. Processi Web di Azure forniscono gli script toorun un modo semplice o nel contesto di hello di processi in background programmi come un [App del servizio web app, app per le API o app per dispositivi mobili](../app-service/app-service-value-prop-what-is.md). È infatti possibile caricare ed eseguire un file eseguibile in formato cmd, bat, exe (.NET), ps1, sh, php, py, js e jar. che verrà eseguito come processo Web in base a una pianificazione (cron) o senza interruzioni.

scopo di hello Hello [WebJobs SDK](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk) è toosimplify hello codice scritto per attività comuni che possono eseguire un processo Web, ad esempio l'elaborazione di immagini, l'elaborazione della coda, aggregazione RSS, manutenzione di file e l'invio di messaggi di posta elettronica. Hello WebJobs SDK include funzionalità per l'utilizzo di archiviazione di Azure e Bus di servizio per la pianificazione di attività e la gestione degli errori e per molti altri scenari comuni. Inoltre, ha progettato toobe estendibile e vi è un [repository del codice sorgente aperta per le estensioni](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview). [Funzioni di Azure](../azure-functions/functions-overview.md) (attualmente in anteprima) è basato su una versione di hello WebJobs SDK che funziona con c# script, Node.js e altri linguaggi. 

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Grazie agli strumenti integrati in Visual Studio, è inoltre semplice creare, distribuire e gestire processi Web. È possibile creare processi Web da modelli, nonché pubblicarli e gestirli, ovvero eseguirli/arrestarli/monitorarli/eseguirne il debug. 

dashboard di processi Web Hello in hello portale di Azure offre funzionalità di gestione potenti che consentono il controllo completo sull'esecuzione di hello di processi Web, tra cui hello possibilità tooinvoke singole funzioni all'interno di processi Web. dashboard Hello Visualizza anche l'output di registrazione e di runtime di funzione. 

## <a name="getstarted"></a>Guida introduttiva a hello WebJobs SDK e di processi Web
* [Introduzione tooAzure processi Web](http://www.hanselman.com/blog/IntroducingWindowsAzureWebJobs.aspx)
* [Post di blog sui vantaggi offerti da Processi Web di Azure](http://www.troyhunt.com/2015/01/azure-webjobs-are-awesome-and-you.html) (di Troy Hunt)
* [Funzionalità di Processi Web di Azure](https://azure.microsoft.com/blog/2014/10/22/webjobs-goes-into-full-production/)
* [Che cos'è hello WebJobs SDK](websites-dotnet-webjobs-sdk.md)
* [Indicazioni di processi di background Microsoft Patterns and Practices](https://docs.microsoft.com/azure/architecture/best-practices/background-jobs)
* [Annuncio hello 1.1.0 RTM di Microsoft Azure SDK processi Web](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/)
* [Introduzione a hello Azure WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md)
* [Coda di archiviazione con hello WebJobs SDK come toouse Azure](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [La modalità di archiviazione con blob di Azure toouse hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [La modalità di archiviazione con tabelle di Azure toouse hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [Come toouse del Bus di servizio di Azure con hello WebJobs SDK](websites-dotnet-webjobs-sdk-service-bus.md)
* [Riferimento rapido per Azure WebJobs SDK (download PDF)](https://go.microsoft.com/fwlink/p/?linkid=845558)
* [Documentazione sulle impostazioni di WebJobs in GitHub](https://github.com/projectkudu/kudu/wiki/Web-jobs).
* Video
  * [I processi Web, hello WebJobs SDK](http://channel9.msdn.com/Shows/Cloud+Cover/Episode-153-WebJobs-with-Pranav-Rastogi?utm_source=dlvr.it&utm_medium=twitter)
  * [Serie di video su Processi Web su Channel 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)
  * [Introduzione agli strumenti di Processi Web per Visual Studio](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [Strumenti di Processi Web e debug remoto](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster)
  * [Aggiornamento di Processi Web di Azure con Pranav Rastogi: estendibilità nella versione 1.1](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-183-Azure-WebJobs-Update-with-Pranav-Rastogi)

Vedere anche le sezioni seguenti hello [processi Web di distribuzione](#deploy) e [test e debug di processi Web](#debug).

## <a name="deploy"></a>Distribuzione di Processi Web
* [Come tooDeploy processi Web di Azure con Visual Studio](websites-dotnet-deploy-webjobs.md)
* [Come con processi Web toodeploy hello portale di Azure](web-sites-create-web-jobs.md)
* [Abilitazione della distribuzione da riga di comando o continua di processi Web di Azure](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/)
* [Distribuzione di un tooAzure di applicazione console .NET mediante processi Web di GIT](http://blog.amitapple.com/post/73574681678/git-deploy-console-app/)
* [Distribuzione di un tooAzure WebJob F #](http://blogs.msdn.com/b/dave_crooks_dev_blog/archive/2015/02/18/deploying-f-web-job-to-azure.aspx)
* [Distribuzione di servizi personalizzati come Azure Webjobs](http://withouttheloop.com/articles/2015-06-23-deploying-custom-services-as-azure-webjobs/)
* Video
  * [Introduzione agli strumenti di Processi Web per Visual Studio](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [Strumenti di Processi Web e debug remoto](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="schedule"></a>Pianificazione di Processi Web
* [Hello Aggiungi processo Web finestra Azure](websites-dotnet-deploy-webjobs.md#configure)
* [Creare un processo Web pianificato in hello portale di Azure](web-sites-create-web-jobs.md#CreateScheduled)
* [Associazione di un tooa di processo dell'utilità di pianificazione processo Web](http://blog.davidebbo.com/2015/05/scheduled-webjob.html)
* [Pianificazione dei processi Web di Azure con espressioni cron](http://blog.amitapple.com/post/2015/06/scheduling-azure-webjobs/)
* [Pianificazione delle singole funzioni processo Web con hello TimerTrigger SDK processi Web](websites-dotnet-webjobs-sdk.md#schedule)

## <a name="debug"></a>Verifica e debug di Processi Web
* [Nuove funzionalità per sviluppatori e debug di Processi Web di Azure in Visual Studio](http://blogs.msdn.com/b/webdev/archive/2014/11/12/new-developer-and-debugging-features-for-azure-webjobs-in-visual-studio.aspx)
* [Hello visualizzazione Dashboard di processi Web](websites-dotnet-webjobs-sdk-get-started.md#view-the-webjobs-sdk-dashboard)
* [Modalità di registrazione utilizzando toowrite hello WebJobs SDK e visualizzarli nel Dashboard hello](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)
* [Debug remoto di processi Web](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebugwj)
* [Come ottenere informazioni sull'autore del BLOB](http://blogs.msdn.com/b/jmstall/archive/2014/02/19/who-wrote-that-blob.aspx) 
* [Codice interattiva in hello Cloud di hosting](http://blogs.msdn.com/b/jmstall/archive/2014/04/26/hosting-interactive-code-in-the-cloud.aspx)
* [Aggiunta di traccia tooAzure processi Web](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)
* [Monitoraggio, diagnosi e risoluzione dei problemi del servizio di archiviazione di Microsoft Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md)
* Video
  * [Strumenti di Processi Web e debug remoto](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="scale"></a>Ridimensionamento di Processi Web
* [Ridimensionamento dell'applicazione Web con Siti Web di Azure](http://msdn.microsoft.com/magazine/dn786914.aspx)
* [Progettazione di app Web pronte per l'uso in ambito aziendale su vasta scala](https://channel9.msdn.com/Events/Build/2014/3-626). Vengono illustrate la scalabilità delle applicazioni web con processi Web, tra cui hello WebJobs SDK.
* Video
  * [Scalabilità orizzontale di Processi Web](http://channel9.msdn.com/Shows/Azure-Friday/Azure-WebJobs-105-Scaling-out-Web-Jobs)

## <a name="additional"></a>Risorse aggiuntive su Processi Web
* [Post di blog di Magnus Mårtensson sulla versione GA di Processi Web di Azure](http://magnusmartensson.com/azure-webjobs-ga)
* [Esecuzione di processi Web di Powershell in siti Web di Azure](http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx)
* [Ricevere notifiche quando i processi Web di Azure attivati vengono completati](http://blog.amitapple.com/post/2014/03/webjobs-notification/)
* [Criteri semplici di conservazione dei backup di siti Web con Processi Web](https://azure.microsoft.com/blog/2014/04/28/simple-web-site-backup-retention-policy-with-webjobs/)
* [Lentezza dei siti Web e dei servizi cloud di Microsoft Azure quando vengono richiesti per la prima volta](http://wp.sjkp.dk/windows-azure-websites-and-cloud-services-slow-on-first-request/). Viene illustrato come toouse processi Web toosimulate hello funzionalità AlwaysOn che è disponibile solo per il livello di prezzo Standard di hello.
* [Arresto normale di Processi Web](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.U72Il_5OWUl). Per l'arresto normale di WebJobs SDK, vedere [Arresto normale](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).
* [Automatizzazione di backup con Processi Web di Azure e AzCopy](http://markjbrown.com/azure-webjobs-azcopy/)
* Video
  * [Video di Magnus Mårtensson su Processi Web di Azure](https://www.youtube.com/playlist?list=PLqp1ZOYYUSd81yEzMYLTw8cz91wx_LU9r)
  * [Serie di video su Processi Web su Channel 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="additionalsdk"></a>Risorse aggiuntive su WebJobs SDK
* [Note sulla versione di WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes)
* [Codice sorgente WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk)
* [Codice sorgente estensioni WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk-extensions), con [modello di estendibilità di Guida dettagliata toohello](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).  
* [Codice sorgente di script WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk-script/) (usato per [Funzioni di Azure](../azure-functions/functions-overview.md))
* [Processo Web tooupload FREB file tooAzure archiviazione mediante hello WebJobs SDK](http://thenextdoorgeek.com/post/WAWS-WebJob-to-upload-FREB-files-to-Azure-Storage-using-the-WebJobs-SDK)
* [Hosting di processi Web di Azure all'esterno di Azure, ospitato processo Web con hello registrazione prestazioni da di Azure](http://bypassion.dk/?p=510)
* [Creazione di uno strumento di importazione dati con Processi Web di Azure](http://www.freshconsulting.com/building-data-import-tool-azure-webjobs/)
* [Panoramica di Funzioni di Azure](../azure-functions/functions-overview.md)
* Video
  * [Serie di video su Processi Web su Channel 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="samples"></a>Applicazioni Processi Web di esempio
* [Applicazioni di esempio fornite dal team di processi Web hello su GitHub](https://github.com/azure/azure-webjobs-sdk-samples)
* [Applicazione Web di Azure semplice con WebJobs Backend utilizzando hello WebJobs SDK](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb)
* [SiteMonitR](http://code.msdn.microsoft.com/SiteMonitR-dd4fcf77). Illustra l'uso di processi Web pianificati o guidati dagli eventi. Vedere post di blog hello [ricostruzione hello SiteMonitR con Azure SDK processi Web](http://www.bradygaster.com/post/rebuilding-the-sitemonitr-using-windows-azure-webjobs).

## <a name="blogs"></a>Blog
* [Blog di Azure](/blog)
* [Blog di Amit Apple](http://blog.amitapple.com/). Si concentra su processi Web (non hello SDK).
* [Blog di Magnus Mårtensson](http://magnusmartensson.com/)

## <a name="gethelp"></a>Guida per i Processi Web
* [StackOverflow per Processi Web](http://stackoverflow.com/questions/tagged/azure-webjobs)
* [Overflow dello stack per hello WebJobs SDK](http://stackoverflow.com/questions/tagged/azure-webjobssdk)
* [StackOverflow per Funzioni di Azure](http://stackoverflow.com/questions/tagged/azure-functions)
* [Forum su Azure e ASP.NET](http://forums.asp.net/1247.aspx)
* [Forum sulle app Web del servizio app di Azure](http://social.msdn.microsoft.com/Forums/azure/home?forum=windowsazurewebsitespreview)
* [Sito di Azure Web App utente vocale](https://feedback.azure.com/forums/169385-websites/)
* [Twitter](http://twitter.com/). Utilizzare hello hashtag #AzureWebJobs.
* [Segnalare un bug o un problema di Processi Web](https://github.com/projectkudu/kudu/wiki/Reporting-WebJobs-issues)

