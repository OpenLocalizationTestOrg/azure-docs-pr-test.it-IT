---
title: Distribuire l'app nel servizio app di Azure | Microsoft Docs
description: Informazioni su come distribuire l'app nel servizio app di Azure
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
ms.openlocfilehash: f41be4e00a9250b07ca260c2858e5fc45143f746
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-app-to-azure-app-service"></a>Distribuire l'app nel servizio app di Azure
Questo articolo consente di determinare l'opzione migliore per distribuire i file per l'app Web, il back-end dell'app per dispositivi mobili o l'app per le API nel [Servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714). L'articolo quindi descrive le risorse appropriate, con istruzioni sulle procedure specifiche per l'opzione scelta.

## <a name="overview"></a>Panoramica della distribuzione nel servizio app di Azure
Il framework applicazioni (ASP.NET, PHP, Node.js, e così via) viene gestito direttamente dal servizio app di Azure. Alcuni framework sono abilitati per impostazione predefinita, mentre altri, come Java e Python, possono richiedere una semplice configurazione con segni di spunta per abilitarli. È anche possibile personalizzare il framework applicazioni, ad esempio la versione PHP o il numero di bit del proprio runtime. Per altre informazioni, vedere [Configurare le app Web nel servizio app di Azure](web-sites-configure.md).

Non essendo necessario occuparsi del server Web o del framework applicazioni, per distribuire l'app al servizio app è sufficiente distribuire il codice, i file binari, i file di contenuto e le rispettive strutture di directory nella directory [**/site/wwwroot**](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure o, per i processi Web, nella directory **/site/wwwroot/App_Data/Jobs/**. Il servizio app supporta tre processi di distribuzione diversi. Tutti i metodi di distribuzione in questo articolo usano uno dei processi seguenti: 

* [FTP o FTPS](https://en.wikipedia.org/wiki/File_Transfer_Protocol): usare lo strumento abilitato per FTP o FTPS preferito per spostare i file in Azure da [FileZilla](https://filezilla-project.org) a IDE completi, come [NetBeans](https://netbeans.org). Si tratta esclusivamente di un processo di caricamento di file. Non vengono forniti altri servizi dal servizio app, ad esempio controllo della versione, gestione della struttura di file e così via. 
* [Kudu (Git/Mercurial o OneDrive/Dropbox)](https://github.com/projectkudu/kudu/wiki/Deployment): Kudu è il [motore di distribuzione](https://github.com/projectkudu/kudu/wiki) nel servizio app. Effettuare il push del codice direttamente in Kudu da qualsiasi repository. Kudu fornisce anche altri servizi ogni volta che viene effettuato il push di codice, inclusi controllo della versione, ripristino del pacchetto, MSBuild e [webhook](https://github.com/projectkudu/kudu/wiki/Web-hooks) per la distribuzione continua e altre attività di automazione. Il motore di distribuzione Kudu supporta 3 tipi diversi di origine distribuzione:   
  
  * Sincronizzazione del contenuto da OneDrive e Dropbox   
  * Distribuzione continua basata su repository con sincronizzazione automatica da GitHub, Bitbucket e Visual Studio Team Services  
  * Distribuzione basata su repository con sincronizzazione manuale da archivio Git locale  
* [Distribuzione Web](http://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy): distribuire il codice al servizio app direttamente dagli strumenti Microsoft preferiti, ad esempio Visual Studio, tramite gli stessi strumenti di automazione della distribuzione ai server IIS. Questo strumento supporta la distribuzione solo delle differenze, la creazione di database, le trasformazioni delle stringhe di connessione e così via. Distribuzione Web si differenzia da Kudu perché i file binari dell'applicazione vengono compilati prima della distribuzione in Azure. Come FTP, non vengono forniti servizi aggiuntivi dal servizio app.

Gli strumenti di sviluppo Web più diffusi supportano uno o più di questi processi di distribuzione. Mentre lo strumento scelto determina i processi di distribuzione che è possibile sfruttare, l'effettiva funzionalità DevOps disponibile dipende dalla combinazione del processo di distribuzione e degli strumenti specifici scelti. Ad esempio, se si esegue Distribuzione Web da [Visual Studio con Azure SDK](#vspros), anche se non si usufruisce dell'automazione tramite Kudu, si ottiene l'automazione del ripristino del pacchetto e di MSBuild in Visual Studio. 

> [!NOTE]
> Questi processi di distribuzione in realtà non [effettuano il provisioning delle risorse di Azure](../azure-resource-manager/resource-group-template-deploy-portal.md) che potrebbero essere necessarie per l'applicazione. La maggior parte degli articoli sulle procedure collegati mostra come effettuare il provisioning dell'app E distribuire il codice end-to-end. È anche possibile trovare altre opzioni per il provisioning delle risorse di Azure nella sezione [Automatizzare la distribuzione con gli strumenti da riga di comando](#automate) .
> 
> 

## <a name="ftp"></a>Eseguire manualmente la distribuzione caricando file con il protocollo FTP
Se di solito si copia il contenuto Web in un server Web manualmente, è possibile usare un'utilità [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol) per copiare i file, ad esempio Esplora risorse o [FileZilla](https://filezilla-project.org/).

Ecco i vantaggi della copia manuale dei file:

* Possibilità di usare strumenti familiari quali gli strumenti FTP e minima complessità di questi. 
* Conoscenza esatta della destinazione dei file.
* Maggiore sicurezza con FTPS.

Ecco gli svantaggi della copia manuale dei file:

* Necessità di conoscere come distribuire i file nelle directory corrette del servizio app. 
* Nessun controllo della versione per il ripristino dello stato precedente quando si verificano errori.
* Nessuna cronologia di distribuzione per la risoluzione d eventuali problemi nel corso di questa operazione.
* Possibilità di tempi lunghi di distribuzione, poiché molti strumenti FTP non sono dotati della funzione di copia delle sole differenze e copiano semplicemente tutti i file.  

### <a name="howtoftp"></a>Come caricare i file con il protocollo FTP
Nel [portale di Azure](https://portal.azure.com) sono disponibili tutte le informazioni necessarie per connettersi alle directory dell'app tramite il protocollo FTP o FTPS.

* [Distribuire l'app nel servizio app di Azure tramite il protocollo FTP](app-service-deploy-ftp.md)

## <a name="dropbox"></a>Distribuire tramite sincronizzazione con una cartella nel cloud
Una valida alternativa alla [copia manuale dei file](#ftp) è la sincronizzazione di file e cartelle con il servizio app da un servizio di archiviazione cloud, ad esempio OneDrive e Dropbox. La sincronizzazione con una cartella nel cloud usa il processo Kudu per la distribuzione. Vedere [Panoramica dei processi di distribuzione](#overview).

Ecco i vantaggi della sincronizzazione con una cartella nel cloud:

* Semplicità di distribuzione. Servizi come OneDrive e Dropbox forniscono client di sincronizzazione desktop, quindi la directory di lavoro locale è anche la directory di distribuzione.
* Distribuzione con un clic.
* Tutte le funzionalità del motore di distribuzione Kudu, ad esempio il ripristino dei pacchetti e l'automazione, sono disponibili.

Ecco gli svantaggi della sincronizzazione con una cartella nel cloud:

* Nessun controllo della versione per il ripristino dello stato precedente quando si verificano errori.
* Nessuna distribuzione automatizzata. È necessaria la sincronizzazione manuale.

### <a name="howtodropbox"></a>Come distribuire tramite sincronizzazione con una cartella nel cloud
Nel [portale di Azure](https://portal.azure.com)è possibile designare una cartella per la sincronizzazione del contenuto nel servizio di archiviazione cloud OneDrive o Dropbox, usare il codice e il contenuto dell'app disponibili in tale cartella e procedere alla sincronizzazione con il servizio app con un semplice clic.

* [Sincronizzare il contenuto da una cartella nel cloud al servizio app di Azure](app-service-deploy-content-sync.md) 

## <a name="continuousdeployment"></a>Eseguire una distribuzione continua da un servizio di controllo del codice sorgente basato sul cloud
Se il team di sviluppo usa un sistema di gestione del codice sorgente basato sul cloud, ad esempio [Visual Studio Team Services](http://www.visualstudio.com/), [GitHub](https://www.github.com) o [BitBucket](https://bitbucket.org/), è possibile configurare il servizio app in modo da integrarlo con il repository e consentire la distribuzione continua. 

Di seguito vengono indicati i vantaggi della distribuzione da un servizio di controllo del codice sorgente basato sul cloud:

* Controllo delle versioni e possibilità di eseguire il ripristino dello stato precedente.
* Possibilità di configurare la distribuzione continua per i repository Git, nonché per i repository Mercurial, quando applicabile. 
* Distribuzione specifica per ramo. Consente di distribuire rami diversi a [slot](web-sites-staged-publishing.md) diversi.
* Sono disponibili tutte le funzionalità del motore di distribuzione Kudu, ad esempio il controllo delle versioni di distribuzione, il ripristino dello stato precedente, il ripristino dei pacchetti, l'automazione.

Svantaggio della distribuzione da un servizio di controllo del codice sorgente basato sul cloud:

* È necessaria una certa conoscenza del relativo servizio di gestione del codice sorgente.

### <a name="vsts"></a>Come eseguire una distribuzione continua da un servizio di controllo del codice sorgente basato sul cloud
Nel [portale di Azure](https://portal.azure.com)è possibile configurare la distribuzione continua da GitHub, Bitbucket e Visual Studio Team Services.

* [Distribuzione continua nel servizio app di Azure](app-service-continuous-deployment.md). 

Per informazioni su come configurare manualmente la distribuzione continua da un repository cloud non elencato nel portale di Azure (ad esempio, [GitLab](https://gitlab.com/)), vedere [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps) (Configurazione manuale della distribuzione continua).

## <a name="localgitdeployment"></a>Distribuire dall'archivio Git locale
Se il team di sviluppo usa un servizio locale di gestione del codice sorgente locale basato su archivio Git, è possibile configurare questo servizio come origine di distribuzione al servizio app. 

Vantaggi della distribuzione da un archivio Git locale:

* Controllo delle versioni e possibilità di eseguire il ripristino dello stato precedente.
* Distribuzione specifica per ramo. Consente di distribuire rami diversi a [slot](web-sites-staged-publishing.md) diversi.
* Sono disponibili tutte le funzionalità del motore di distribuzione Kudu, ad esempio il controllo delle versioni di distribuzione, il ripristino dello stato precedente, il ripristino dei pacchetti, l'automazione.

Svantaggi della distribuzione da un archivio Git locale:

* È necessaria una certa conoscenza del relativo sistema di gestione del codice sorgente.
* Nessuna soluzione chiavi in mano per la distribuzione continua. 

### <a name="vsts"></a>Come distribuire dall'archivio Git locale
Nel [portale di Azure](https://portal.azure.com)è possibile configurare la distribuzione dell'archivio Git locale.

* [Distribuzione dell'archivio Git locale nel servizio app di Azure](app-service-deploy-local-git.md). 
* [Pubblicazione in App Web da qualsiasi repository Git/Hg](http://blog.davidebbo.com/2013/04/publishing-to-azure-web-sites-from-any.html).  

## <a name="deploy-using-an-ide"></a>Distribuire tramite un IDE
Se si usa già [Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) con un [Azure SDK](https://azure.microsoft.com/downloads/) o altri gruppi di IDE come [Xcode](https://developer.apple.com/xcode/), [Eclipse](https://www.eclipse.org) e [IntelliJ IDEA](https://www.jetbrains.com/idea/), è possibile eseguire la distribuzione in Azure direttamente dall'interno dell'IDE. Questa opzione è ideale per un singolo sviluppatore.

Visual Studio supporta tutti e tre i processi di distribuzione (FTP, Git e Distribuzione Web) secondo le preferenze dell'utente, mentre altri IDE possono eseguire la distribuzione al servizio app se includono l'integrazione con FTP o Git. Vedere [Panoramica dei processi di distribuzione](#overview).

Ecco i vantaggi della distribuzione con un IDE:

* Ridurre potenzialmente gli strumenti per il ciclo di vita dell'applicazione end-to-end. Sviluppare, eseguire il debug, tenere traccia e distribuire l'app in Azure senza uscire dall'IDE. 

Ecco gli svantaggi della distribuzione con un IDE:

* Complessità aggiuntiva degli strumenti.
* Richiede comunque un sistema di controllo del codice sorgente per un progetto team.

<a name="vspros"></a> Altri vantaggi della distribuzione tramite Visual Studio con Azure SDK:

* Azure SDK rende le risorse di Azure elementi di primaria importanza in Visual Studio. Creare, eliminare, modificare, avviare e arrestare app, eseguire query sul database SQL di back-end, live-debug applicazione Azure e molto altro ancora. 
* Modifica in tempo reale dei file di codice in Azure.
* Debug in tempo reale di app in Azure.
* Azure Explorer integrato.
* Distribuzione solo delle differenze. 

### <a name="vs"></a>Come distribuire direttamente da Visual Studio
* [Introduzione ad Azure e ASP.NET](app-service-web-get-started-dotnet.md). Come creare e distribuire un semplice Progetto Applicazione Web MVC ASP.NET utilizzando Visual Studio e Distribuzione Web.
* [Come eseguire la distribuzione nei processi Web di Azure utilizzando Visual Studio](websites-dotnet-deploy-webjobs.md). Come configurare i progetti di applicazioni console in modo da distribuirli come processi Web.  
* [Distribuzione di Web ASP.NET con Visual Studio](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/introduction). Una serie di esercitazioni in 12 parti in cui è trattata una gamma più completa di attività di distribuzione rispetto alle altre risorse in questo elenco. Sono state aggiunte alcune funzionalità di distribuzione di Azure dal momento in cui è stata creata l'esercitazione. Tuttavia, le note aggiunte successivamente descrivono gli elementi mancanti.
* Articolo relativo alla [distribuzione di un sito Web ASP.NET in Azure con Visual Studio 2012 direttamente da un repository Git](http://www.dotnetcurry.com/ShowArticle.aspx?ID=881). L'articolo contiene informazioni su come distribuire un progetto Web ASP.NET con Visual Studio, utilizzando il plugin Git per eseguire il commit del codice a Git e connettere Azure al repository Git. A partire da Visual Studio 2013, il supporto per Git è integrato, pertanto non è più necessario installare un plug-in.

### <a name="aztk"></a>Come distribuire usando i toolkit di Azure per Eclipse e IntelliJ IDEA
Microsoft consente la distribuzione di App Web in Azure direttamente da Eclipse e IntelliJ tramite il [toolkit di Azure per Eclipse](../azure-toolkit-for-eclipse.md) e il [toolkit di Azure per IntelliJ](../azure-toolkit-for-intellij.md). Le esercitazioni seguenti illustrano i passaggi coinvolti nella distribuzione di una semplice App Web "Hello World" in Azure mediante l'IDE:

* [Creare un'app Web Hello World per Azure in Eclipse](app-service-web-eclipse-create-hello-world-web-app.md). Questa esercitazione descrive come usare il toolkit di Azure per Eclipse per creare e distribuire un'App Web Hello World per Azure.
* [Creare un'app Web Hello World per Azure in IntelliJ](app-service-web-intellij-create-hello-world-web-app.md). Questa esercitazione descrive come usare il toolkit di Azure per IntelliJ per creare e distribuire un'App Web Hello World per Azure.

## <a name="automate"></a>Automatizzare la distribuzione con strumenti da riga di comando
Se come ambiente di sviluppo si preferisce un terminale da riga di comando, è possibile creare script delle attività di distribuzione per l'app del servizio app usando gli strumenti da riga di comando. 

Di seguito vengono indicati i vantaggi della distribuzione tramite gli strumenti da riga di comando:

* Possibilità di creare script per gli scenari di distribuzione.
* Integrazione del provisioning di risorse di Azure e della distribuzione di codice.
* Integrazione della distribuzione di Azure con script di integrazione continua esistenti.

Gli svantaggi della distribuzione tramite gli strumenti da riga di comando sono i seguenti:

* Approccio non adatto agli sviluppatori che preferiscono l'interfaccia utente grafica.

### <a name="automatehow"></a>Come automatizzare la distribuzione con gli strumenti da riga di comando

Per un elenco di strumenti da riga di comando e di collegamenti a esercitazioni, vedere [Automatizzare la distribuzione con strumenti da riga di comando](app-service-deploy-command-line.md). 

## <a name="nextsteps"></a>Passaggi successivi
In alcuni scenari potrebbe essere necessario passare facilmente da una versione temporanea a una versione di produzione dell'app e viceversa. Per ulteriori informazioni, vedere [Distribuzione temporanea su App Web](web-sites-staged-publishing.md).

La definizione di un piano di backup e ripristino è una parte importante di un flusso di distribuzione. Per informazioni sulla funzionalità di backup e ripristino del servizio app, vedere [Eseguire il backup di un'App Web nel servizio app di Azure](web-sites-backup.md).  

Per informazioni su come usare il controllo degli accessi in base al ruolo di Azure per gestire l'accesso alla distribuzione del servizio app, vedere [Controllo degli accessi in base al ruolo e pubblicazione di App Web](https://azure.microsoft.com/blog/2015/01/05/rbac-and-azure-websites-publishing/).

