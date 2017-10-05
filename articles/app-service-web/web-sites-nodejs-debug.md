---
title: Come eseguire il debug di un'app Web Node.js nel servizio app di Azure
description: Informazioni su come eseguire il debug di un'app Web Node.js nel servizio app di Azure.
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5e302a4c58a171d40e43a22c34c724e868019ec8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-debug-a-nodejs-web-app-in-azure-app-service"></a>Come eseguire il debug di un'app Web Node.js nel servizio app di Azure
Azure offre diagnostica integrata per agevolare il debug di applicazioni Node.js ospitate in App Web del [servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) . In questo articolo verrà illustrato come abilitare la registrazione di stdout e stderr, visualizzare informazioni sugli errori nel browser, nonché come scaricare e visualizzare i file di log.

La diagnostica per le applicazioni Node.js ospitate in Azure viene fornita da [IISNode]. In questo articolo vengono illustrate le impostazioni più comuni per la raccolta delle informazioni di diagnostica; non sono invece incluse informazioni dettagliate sull'utilizzo di IISNode. Per ulteriori informazioni sull'utilizzo di IISNode, vedere il [file Readme di IISNode] su GitHub.

<a id="enablelogging"></a>

## <a name="enable-logging"></a>Abilitazione della registrazione
Per impostazione predefinita, un'app web servizio App acquisisce solo le informazioni di diagnostica relative distribuzioni, ad esempio quando si distribuisce un'app web utilizzando Git. Tali informazioni sono utili in caso di problemi durante la distribuzione, ad esempio quando non si riesce a installare un modulo cui viene fatto riferimento in **package.json**oppure se si usa uno script di distribuzione personalizzato.

Per abilitare la registrazione di flussi stdout e stderr, è necessario creare un file **IISNode.yml** nella radice dell'applicazione Node.js e aggiungere quanto segue:

    loggingEnabled: true

In tal modo la registrazione di stderr e stdout dall'applicazione Node.js verrà abilitata.

È inoltre possibile utilizzare il file **IISNode.yml** per controllare se in caso di errore al browser vengono restituiti errori descrittivi o dello sviluppatore. Per abilitare gli errori dello sviluppatore, aggiungere la riga seguente al file **IISNode.yml** :

    devErrorsEnabled: true

Dopo aver abilitato questa opzione, IISNode restituirà gli ultimi 64 KB di informazioni inviate a stderr anziché un errore descrittivo, quale "si è verificato un errore interno del server".

> [!NOTE]
> devErrorsEnabled è utile per diagnosticare problemi che si verificano durante lo sviluppo, tuttavia se viene abilitato in un ambiente di produzione è possibile che gli eventuali errori di sviluppo vengano inviati agli utenti finali.
> 
> 

Se il **IISNode.yml** non esisteva già nell'applicazione, sarà necessario riavviare il sito Web dopo aver pubblicato l'applicazione aggiornata. Se si intende solo modificare le impostazioni in un file **IISNode.yml** già pubblicato, il riavvio non è richiesto.

> [!NOTE]
> Se il sito Web è stato creato con gli strumenti da riga di comando di Azure o i cmdlet di Azure PowerShell, verrà creato automaticamente un file **IISNode.yml** predefinito.
> 
> 

Per riavviare l'app Web, selezionarla nel [portale di Azure](https://portal.azure.com)e quindi fare clic sul pulsante **RIAVVIA** :

![Pulsante Restart][restart-button]

Se nell'ambiente di sviluppo sono installati gli strumenti da riga di comando di Azure, è possibile utilizzare il comando seguente per riavviare il sito Web:

    azure site restart [sitename]

> [!NOTE]
> Anche se loggingEnabled e devErrorsEnabled sono le opzioni di configurazione più utilizzate di IISNode.yml per acquisire informazioni diagnostiche, è possibile utilizzare IISNode.yml per configurare numerose opzioni per l'ambiente host. Per un elenco completo delle opzioni di configurazione, vedere il file [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml).
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a>Accesso ai log
È possibile accedere ai log di diagnostica in tre modi, ovvero utilizzando il protocollo FTP (File Transfer Protocol), scaricando un archivio ZIP oppure sotto forma di flusso aggiornato in diretta del log (noto anche come tail). Per il download dell'archivio ZIP dei file di log o per la visualizzazione del flusso in diretta sono necessari gli strumenti da riga di comando di Azure, che è possibile installare tramite il comando seguente:

    npm install azure-cli -g

Dopo l'installazione, è possibile accedere agli strumenti tramite il comando 'azure'. È prima necessario configurare gli strumenti da riga di comando per l'uso della sottoscrizione di Azure. Per informazioni su come eseguire questa attività, vedere la sezione **Come scaricare e importare impostazioni di pubblicazione** dell'articolo [Come utilizzare gli strumenti da riga di comando](../xplat-cli-connect.md) .

### <a name="ftp"></a>FTP
Per accedere alle informazioni diagnostiche tramite FTP, visitare il [portale di Azure](https://portal.azure.com), selezionare l’app Web e scegliere **DASHBOARD**. Nella sezione relativa ai **collegamenti rapidi** fare clic sui collegamenti **REGISTRI DI DIAGNOSTICA FTP** e **REGISTRI DI DIAGNOSTICA FTPS** per accedere ai log tramite il protocollo FTP.

> [!NOTE]
> Se in precedenza non sono stati configurati nome utente e password per FTP o per la distribuzione, è possibile eseguire questa operazione nella pagina di gestione **Avvio rapido** selezionando **Imposta credenziali di distribuzione**.
> 
> 

L'URL FTP restituito nel dashboard si riferisce alla directory **LogFiles** , che conterrà le seguenti sottodirectory:

* [Metodo di distribuzione](web-sites-deploy.md) : se si utilizza un metodo di distribuzione, ad esempio Git, verrà creata una directory con lo stesso nome, che conterrà le informazioni correlate alle distribuzioni.
* nodejs: contiene le informazioni di stdout e stderr acquisite da tutte le istanze dell'applicazione, quando loggingEnabled è impostato su true.

### <a name="zip-archive"></a>Archivio ZIP
Per scaricare un archivio ZIP dei log di diagnostica, utilizzare il seguente comando degli strumenti da riga di comando di Azure:

    azure site log download [sitename]

Nella directory corrente verrà scaricato un file **diagnostics.zip** . Questo archivio contiene la seguente struttura di directory:

* deployments: log delle informazioni sulle distribuzioni dell'applicazione
* LogFiles
  
  * [Metodo di distribuzione](web-sites-deploy.md) : se si utilizza un metodo di distribuzione, ad esempio Git, verrà creata una directory con lo stesso nome, che conterrà le informazioni correlate alle distribuzioni.
  * nodejs: contiene le informazioni di stdout e stderr acquisite da tutte le istanze dell'applicazione, quando loggingEnabled è impostato su true.

### <a name="live-stream-tail"></a>Flusso in diretta (tail)
Per visualizzare un flusso in diretta delle informazioni dei log di diagnostica, usare il seguente comando degli strumenti da riga di comando di Azure:

    azure site log tail [sitename]

Verrà restituito un flusso di eventi log che vengono aggiornati non appena si verificano nel server. Questo flusso restituirà le informazioni relative alla distribuzione, oltre alle informazioni di stdout e stderr, quando loggingEnabled è impostato su true.

<a id="nextsteps"></a>

## <a name="next-steps"></a>Passaggi successivi
In questo articolo è stato illustrato come abilitare e accedere alle informazioni di diagnostica in Azure. Queste informazioni sono utili per comprendere problemi che si verificano nell'applicazione, tuttavia è possibile che indichino un problema relativo a un modulo in uso oppure che segnalino che la versione di Node.js utilizzata in Siti Web di Azure è diversa da quella dell'ambiente di distribuzione.

Per informazioni sull'uso di moduli in Azure, vedere [Uso di moduli Node.js con applicazioni Azure](../nodejs-use-node-modules-azure-apps.md).

Per informazioni sulla specifica di una versione di Node.js per l'applicazione, vedere [Specifica di una versione di Node.js in un'applicazione Azure].

Per ulteriori informazioni, vedere anche il [Centro per sviluppatori di Node.js](/develop/nodejs/).

## <a name="whats-changed"></a>Modifiche apportate
* Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Per iniziare a usare Servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[file Readme di IISNode]: https://github.com/tjanczuk/iisnode#readme
[How to Use The Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[Specifica di una versione di Node.js in un'applicazione Azure]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

