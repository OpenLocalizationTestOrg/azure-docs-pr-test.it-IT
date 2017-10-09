---
title: aaaDeploy del servizio App di tooAzure app | Documenti Microsoft
description: Informazioni su come toodeploy il tooAzure app servizio App.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: f1464f71-2624-400e-86a2-e687e385804f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: 5c84e4ca502874209d750c94efeb86a59aa71a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service"></a>Distribuire il servizio App di tooAzure app
In questo articolo consente di determinare hello migliore opzione toodeploy hello file per l'app web back-end dell'app mobile o app per le API troppo[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)e viene quindi tooappropriate risorse con le istruzioni specifiche tooyour opzione preferita.

## <a name="overview"></a>Panoramica della distribuzione nel servizio app di Azure
Servizio App di Azure gestisce i framework dell'applicazione hello automaticamente (ASP.NET, PHP, Node.js e così via). Alcuni Framework che sono abilitati per impostazione predefinita, mentre altri, come Java e Python, potrebbe essere necessario un tooenable configurazione semplice segno di spunta è. Inoltre, è possibile personalizzare il framework applicazione, ad esempio la versione di PHP hello o bit hello del runtime. Per altre informazioni, vedere [Configurare le app Web nel servizio app di Azure](web-sites-configure.md).

Poiché non si dispone di tooworry su framework di server o un'applicazione web hello, la distribuzione del servizio di tooApp app, è necessario distribuire il codice, i file binari, i file di contenuto e la struttura di directory corrispondente, toohello [   **/sito /wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (o hello **/sito/wwwroot/App_Data/processi/** directory per i processi Web). Il servizio app supporta tre processi di distribuzione diversi. Tutti i metodi di distribuzione hello in questo articolo utilizzano uno dei seguenti processi hello: 

* [FTP o FTPS](https://en.wikipedia.org/wiki/File_Transfer_Protocol): usare i Preferiti FTP o FTPS abilitata strumento toomove tooAzure il file, da [FileZilla](https://filezilla-project.org) in primo piano toofull IDE come [NetBeans](https://netbeans.org). Si tratta esclusivamente di un processo di caricamento di file. Non vengono forniti altri servizi dal servizio app, ad esempio controllo della versione, gestione della struttura di file e così via. 
* [Kudu (Git o Mercurial o OneDrive o Dropbox)](https://github.com/projectkudu/kudu/wiki/Deployment): Kudu è hello [motore di distribuzione](https://github.com/projectkudu/kudu/wiki) nel servizio App. Push tooKudu il codice direttamente da un repository. Kudu offre servizi aggiunti ogni volta che tooit, tra cui il controllo della versione, ripristino del pacchetto, MSBuild, push del codice e [web hook](https://github.com/projectkudu/kudu/wiki/Web-hooks) per la distribuzione continua e altre attività di automazione. motore di distribuzione Kudu Hello supporta 3 diversi tipi di origini di distribuzione:   
  
  * Sincronizzazione del contenuto da OneDrive e Dropbox   
  * Distribuzione continua basata su repository con sincronizzazione automatica da GitHub, Bitbucket e Visual Studio Team Services  
  * Distribuzione basata su repository con sincronizzazione manuale da archivio Git locale  
* [Web Deploy](http://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy): degli strumenti, ad esempio Visual Studio usando hello stesso strumento che consente di automatizzare i server di distribuzione tooIIS Distribuisci codice tooApp servizio direttamente da Microsoft preferito. Questo strumento supporta la distribuzione solo delle differenze, la creazione di database, le trasformazioni delle stringhe di connessione e così via. Distribuzione Web diversa da Kudu in applicazione i file binari compilati prima di essere distribuita tooAzure. TooFTP simile, nessun servizi aggiuntivi vengono forniti dal servizio App.

Gli strumenti di sviluppo Web più diffusi supportano uno o più di questi processi di distribuzione. Mentre si sceglie lo strumento hello determina i processi di distribuzione hello è possibile usare, hello funzionalità DevOps effettiva a disposizione dipende dalla combinazione di hello del processo di distribuzione hello e hello strumenti specifici si sceglie. Ad esempio, se si esegue Distribuzione Web da [Visual Studio con Azure SDK](#vspros), anche se non si usufruisce dell'automazione tramite Kudu, si ottiene l'automazione del ripristino del pacchetto e di MSBuild in Visual Studio. 

> [!NOTE]
> Questi processi di distribuzione non effettivamente [provisioning hello risorse di Azure](../azure-resource-manager/resource-group-template-deploy-portal.md) che potrebbe essere necessario l'app. Tuttavia, la maggior parte delle hello collegato come-tooarticles mostrano come tooprovision hello app e distribuire il codice tooit end-to-end. È anche possibile trovare altre opzioni per il provisioning delle risorse di Azure in hello [automatizzare la distribuzione utilizzando gli strumenti da riga di comando](#automate) sezione.
> 
> 

## <a name="ftp"></a>Eseguire manualmente la distribuzione caricando file con il protocollo FTP
Se si toomanually utilizzato la copia di server web tooa contenuto web, è possibile utilizzare un [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol) file toocopy dell'utilità, ad esempio Esplora risorse o [FileZilla](https://filezilla-project.org/).

i professionisti Hello di copia manuale dei file sono:

* Possibilità di usare strumenti familiari quali gli strumenti FTP e minima complessità di questi. 
* Conoscenza esatta della destinazione dei file.
* Maggiore sicurezza con FTPS.

gli svantaggi di Hello della copia manuale dei file sono:

* Con tooknow come toodeploy toohello corretto delle directory dei file nel servizio App. 
* Nessun controllo della versione per il ripristino dello stato precedente quando si verificano errori.
* Nessuna cronologia di distribuzione per la risoluzione d eventuali problemi nel corso di questa operazione.
* Distribuzione lungo potenziali volte perché molti strumenti FTP non fornire la copia solo delle differenze e semplicemente copiare tutti i file hello.  

### <a name="howtoftp"></a>Modalità tooupload in file con FTP
Hello [portale Azure](https://portal.azure.com) offre tutte le informazioni di hello occorre directory dell'applicazione tooyour tooconnect tramite FTP o FTPS.

* [Distribuire il servizio App di tooAzure app tramite FTP](app-service-deploy-ftp.md)

## <a name="dropbox"></a>Distribuire tramite sincronizzazione con una cartella nel cloud
Una buona alternativa troppo[la copia manuale dei file](#ftp) esegue la sincronizzazione di file e cartelle tooApp servizio da un servizio di archiviazione cloud come OneDrive e dell'area di sincronizzazione. La sincronizzazione con una cartella di cloud utilizza il processo Kudu hello per la distribuzione (vedere [panoramica dei processi di distribuzione](#overview)).

i professionisti Hello di sincronizzazione con una cartella cloud sono:

* Semplicità di distribuzione. Servizi come OneDrive e Dropbox forniscono client di sincronizzazione desktop, quindi la directory di lavoro locale è anche la directory di distribuzione.
* Distribuzione con un clic.
* Tutte le funzionalità nel motore di distribuzione Kudu hello sono disponibile (ad esempio, ripristino del pacchetto, automazione).

gli svantaggi di Hello della sincronizzazione con una cartella cloud sono:

* Nessun controllo della versione per il ripristino dello stato precedente quando si verificano errori.
* Nessuna distribuzione automatizzata. È necessaria la sincronizzazione manuale.

### <a name="howtodropbox"></a>Come toodeploy per la sincronizzazione con una cartella di cloud
In hello [portale Azure](https://portal.azure.com), è possibile specificare una cartella per la sincronizzazione del contenuto nella memoria cloud OneDrive o Dropbox, con il codice dell'app e il contenuto della cartella di lavoro e fare clic su sincronizzazione tooApp servizio con hello di un pulsante.

* [Sincronizzare il contenuto di un tooAzure di cartella servizio App cloud](app-service-deploy-content-sync.md). 

## <a name="continuousdeployment"></a>Eseguire una distribuzione continua da un servizio di controllo del codice sorgente basato sul cloud
Se il team di sviluppo Usa un servizio di Gestione (controllo servizi SCM) codice di origine basato su cloud come [Visual Studio Team Services](http://www.visualstudio.com/), [GitHub](https://www.github.com), o [BitBucket](https://bitbucket.org/), è possibile configurare App Servizio toointegrate con il repository e distribuire in modo continuo. 

i professionisti Hello della distribuzione da un servizio di controllo basato su cloud di origine sono:

* Rollback tooenable controllo di versione.
* Capacità tooconfigure la distribuzione continua per Git (e Mercurial dove applicabile) repository. 
* Distribuzione di ramo specifico, è possibile distribuire diversi rami toodifferent [slot](web-sites-staged-publishing.md).
* Tutte le funzionalità nel motore di distribuzione Kudu hello sono disponibile (ad esempio, il controllo delle versioni di distribuzione, eseguire il rollback, ripristino del pacchetto, automazione).

con Hello della distribuzione da un servizio di controllo basato su cloud di origine è:

* Conoscenza di hello rispettivi SCM i servizi necessari.

### <a name="vsts"></a>Modalità di controllo servizio toodeploy continuamente da un'origine basata su cloud
In hello [portale Azure](https://portal.azure.com), è possibile configurare la distribuzione continua da GitHub, Bitbucket e Visual Studio Team Services.

* [La distribuzione continua tooAzure servizio App](app-service-continuous-deployment.md). 

toofind out come la distribuzione continua tooconfigure manualmente da un repository di cloud non elencata hello portale di Azure (ad esempio [GitLab](https://gitlab.com/)), vedere [configurazione di distribuzione continua tramite i passaggi manuali](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="localgitdeployment"></a>Distribuire dall'archivio Git locale
Se il team di sviluppo Usa un servizio di Gestione (controllo servizi SCM) codice di origine locale locale in base a Git, è possibile configurare come un tooApp di origine di distribuzione del servizio. 

Vantaggi della distribuzione da un archivio Git locale:

* Rollback tooenable controllo di versione.
* Distribuzione di ramo specifico, è possibile distribuire diversi rami toodifferent [slot](web-sites-staged-publishing.md).
* Tutte le funzionalità nel motore di distribuzione Kudu hello sono disponibile (ad esempio, il controllo delle versioni di distribuzione, eseguire il rollback, ripristino del pacchetto, automazione).

Svantaggi della distribuzione da un archivio Git locale:

* Conoscenza di sistema SCM rispettivo hello richiesto.
* Nessuna soluzione chiavi in mano per la distribuzione continua. 

### <a name="vsts"></a>Come toodeploy da Git locale
In hello [portale Azure](https://portal.azure.com), è possibile configurare la distribuzione Git locale.

* [TooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md). 
* [Pubblicazione di App tooWeb da qualsiasi repository git/hg](http://blog.davidebbo.com/2013/04/publishing-to-azure-web-sites-from-any.html).  

## <a name="deploy-using-an-ide"></a>Distribuire tramite un IDE
Se si sta già utilizzando [Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) con un [Azure SDK](https://azure.microsoft.com/downloads/), o altri gruppi di IDE, ad esempio [Xcode](https://developer.apple.com/xcode/), [Eclipse](https://www.eclipse.org), e [ IDEA IntelliJ](https://www.jetbrains.com/idea/), è possibile distribuire tooAzure direttamente dall'interno dell'IDE. Questa opzione è ideale per un singolo sviluppatore.

Visual Studio supporta tutti i tre processi di distribuzione (FTP, Git e distribuzione Web), in base alle preferenze, mentre altri IDE è possibile distribuire tooApp servizio se dispongono di integrazione Git o FTP (vedere [panoramica dei processi di distribuzione](#overview)).

i professionisti Hello della distribuzione con l'IDE sono:

* Ridurre potenzialmente hello gli strumenti per il ciclo di vita dell'applicazione end-to-end. Sviluppare, eseguire il debug, traccia e distribuire tooAzure l'app senza dover spostare all'esterno dell'IDE. 

gli svantaggi di Hello della distribuzione con l'IDE sono:

* Complessità aggiuntiva degli strumenti.
* Richiede comunque un sistema di controllo del codice sorgente per un progetto team.

<a name="vspros"></a> Altri vantaggi della distribuzione tramite Visual Studio con Azure SDK:

* Azure SDK rende le risorse di Azure elementi di primaria importanza in Visual Studio. Creare, eliminare, modificare, avviare e arrestare l'App, database SQL di query hello back-end, hello in tempo reale di debug dell'app di Azure e molto altro ancora. 
* Modifica in tempo reale dei file di codice in Azure.
* Debug in tempo reale di app in Azure.
* Azure Explorer integrato.
* Distribuzione solo delle differenze. 

### <a name="vs"></a>Come toodeploy direttamente da Visual Studio
* [Introduzione ad Azure e ASP.NET](app-service-web-get-started-dotnet.md). Come toocreate e distribuire un progetto web ASP.NET MVC semplice utilizzando Visual Studio e distribuzione Web.
* [Come processi Web di Azure con Visual Studio tooDeploy](websites-dotnet-deploy-webjobs.md). Come applicazione Console tooconfigure progetti in modo che la distribuzione come processi Web.  
* [Distribuzione di Web ASP.NET con Visual Studio](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/introduction). Una serie di esercitazioni 12 parti che copre un intervallo più completo di attività di distribuzione rispetto ad altri utenti hello in questo elenco. Alcune funzionalità di distribuzione di Azure sono stati aggiunti dall'esercitazione hello è stato scritto, ma note aggiunte in seguito viene illustrato cosa manca.
* [Distribuzione tooAzure un sito Web ASP.NET in Visual Studio 2012, da un Git Repository direttamente](http://www.dotnetcurry.com/ShowArticle.aspx?ID=881). Viene illustrato come progetto di toodeploy un web ASP.NET in Visual Studio, usando hello Git toocommit plug-in hello codice tooGit e connettendosi repository Git toohello Azure. A partire da Visual Studio 2013, il supporto per Git è integrato, pertanto non è più necessario installare un plug-in.

### <a name="aztk"></a>Come toodeploy utilizzando hello Azure Toolkit per Eclipse e IDEA IntelliJ
Microsoft rende possibile toodeploy tooAzure di applicazioni Web direttamente da Eclipse e IntelliJ tramite hello [Azure Toolkit per Eclipse](../azure-toolkit-for-eclipse.md) e [Azure Toolkit per IntelliJ](../azure-toolkit-for-intellij.md). Hello esercitazioni seguenti illustrano hello passaggi coinvolti nella distribuzione tooAzure App Web di world semplice un "Hello" utilizzando l'IDE:

* [Creare un'app Web Hello World per Azure in Eclipse](app-service-web-eclipse-create-hello-world-web-app.md). In questa esercitazione Mostra come toouse hello Azure Toolkit per Eclipse toocreate e distribuire un'App Web di Hello World per Azure.
* [Creare un'app Web Hello World per Azure in IntelliJ](app-service-web-intellij-create-hello-world-web-app.md). In questa esercitazione Mostra come toouse hello Azure Toolkit per IntelliJ toocreate e distribuire un'App Web di Hello World per Azure.

## <a name="automate"></a>Automatizzare la distribuzione con strumenti da riga di comando
Se si preferisce terminal della riga di comando hello come ambiente di sviluppo hello scelta, è possibile creare script delle attività di distribuzione per l'applicazione di servizio App utilizzando gli strumenti da riga di comando. 

Di seguito vengono indicati i vantaggi della distribuzione tramite gli strumenti da riga di comando:

* Possibilità di creare script per gli scenari di distribuzione.
* Integrazione del provisioning di risorse di Azure e della distribuzione di codice.
* Integrazione della distribuzione di Azure con script di integrazione continua esistenti.

Gli svantaggi della distribuzione tramite gli strumenti da riga di comando sono i seguenti:

* Approccio non adatto agli sviluppatori che preferiscono l'interfaccia utente grafica.

### <a name="automatehow"></a>Come distribuzione tooautomate con gli strumenti da riga di comando

Vedere [automatizzare la distribuzione dell'applicazione Azure con gli strumenti da riga di comando](app-service-deploy-command-line.md) per un elenco di tootutorials collegamenti e gli strumenti da riga di comando. 

## <a name="nextsteps"></a>Passaggi successivi
In alcuni scenari potrebbe essere toobe tooeasily in grado di passare avanti e indietro di gestione temporanea e una versione di produzione dell'app. Per ulteriori informazioni, vedere [Distribuzione temporanea su App Web](web-sites-staged-publishing.md).

La definizione di un piano di backup e ripristino è una parte importante di un flusso di distribuzione. Per informazioni su backup di servizio App di hello e funzionalità di ripristino, vedere [Web App backup](web-sites-backup.md).  

Per informazioni sulla modalità di accesso di distribuzione del servizio tooApp toomanage Role-Based Access Control di Azure toouse, vedere [RBAC pubblicazione sul Web e App](https://azure.microsoft.com/blog/2015/01/05/rbac-and-azure-websites-publishing/).

