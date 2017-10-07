---
title: aaaHow toodebug un'app web Node.js in Azure App Service
description: Informazioni su come toodebug un Node.js web app in Azure App Service.
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
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a>Come toodebug un Node.js web app in Azure App Service
Azure offre tooassist di diagnostica con il debug di applicazioni Node.js ospitate in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) App Web. In questo articolo si apprenderà come registrazione tooenable di stdout e stderr, informazioni di errore visualizzato nel browser hello e la modalità di toodownload e visualizzare i file di log.

La diagnostica per le applicazioni Node.js ospitate in Azure viene fornita da [IISNode]. Anche se in questo articolo illustra le impostazioni più comuni di hello per raccogliere le informazioni di diagnostica, non fornisce un riferimento completo per l'utilizzo di IISNode. Per ulteriori informazioni sull'uso di IISNode, vedere hello [IISNode Readme] su GitHub.

<a id="enablelogging"></a>

## <a name="enable-logging"></a>Abilitazione della registrazione
Per impostazione predefinita, un'app web servizio App acquisisce solo le informazioni di diagnostica relative distribuzioni, ad esempio quando si distribuisce un'app web utilizzando Git. Tali informazioni sono utili in caso di problemi durante la distribuzione, ad esempio quando non si riesce a installare un modulo cui viene fatto riferimento in **package.json**oppure se si usa uno script di distribuzione personalizzato.

hello tooenable registrazione di flussi di stdout e stderr, è necessario creare un **IISNode.yml** file alla radice dell'applicazione Node.js hello e aggiungere hello seguenti:

    loggingEnabled: true

In questo modo la registrazione di hello di stderr e stdout dall'applicazione Node.js.

Hello **IISNode.yml** file può anche essere toocontrol utilizzati se descrittivi errori o per sviluppatori restituiti toohello browser quando si verifica un errore. individuare errori degli sviluppatori tooenable, aggiungere hello seguente riga toohello **IISNode.yml** file:

    devErrorsEnabled: true

Dopo aver abilitata questa opzione, IISNode restituirà hello ultimo 64 KB di informazioni inviate toostderr anziché un errore descrittivo, ad esempio "si è verificato un errore interno del server".

> [!NOTE]
> Anche devErrorsEnabled è utile quando si diagnosticano problemi durante lo sviluppo, abilitarlo in un ambiente di produzione può comportare errori di sviluppo inviati agli utenti di tooend.
> 
> 

Se hello **IISNode.yml** file non esiste già all'interno dell'applicazione, è necessario riavviare l'app web dopo la pubblicazione di un'applicazione hello aggiornato. Se si intende solo modificare le impostazioni in un file **IISNode.yml** già pubblicato, il riavvio non è richiesto.

> [!NOTE]
> Se l'app web è stato creato utilizzando gli strumenti da riga di comando di hello Azure o i cmdlet PowerShell di Azure, valore predefinito è **IISNode.yml** file viene creato automaticamente.
> 
> 

toorestart hello web app, app web selezionare hello in hello [portale Azure](https://portal.azure.com), quindi fare clic su **riavviare** pulsante:

![Pulsante Restart][restart-button]

Se gli strumenti da riga di comando di hello Azure sono installati nell'ambiente di sviluppo, è possibile utilizzare hello comando toorestart hello web app seguenti:

    azure site restart [sitename]

> [!NOTE]
> Mentre loggingEnabled e devErrorsEnabled sono le opzioni di configurazione IISNode.yml hello più comunemente usato per l'acquisizione di informazioni di diagnostica, IISNode.yml può essere utilizzato tooconfigure un'ampia gamma di opzioni per l'ambiente di hosting. Per un elenco completo delle opzioni di configurazione di hello, vedere hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a>Accesso ai log
I log di diagnostica possono avvenire in tre modi; Utilizzando hello protocollo FTP (File Transfer), il download di un archivio Zip, o come attivo aggiornato flusso del log hello (noto anche come finale). Download di archivio di Zip hello hello dei file di log o la visualizzazione flusso live hello richiedono strumenti da riga di comando di hello Azure. È possibile installarli utilizzando hello comando seguente:

    npm install azure-cli -g

Una volta installato, è possano accedere agli strumenti di hello comando hello 'azure'. Hello strumenti da riga di comando deve essere innanzitutto configurato toouse la sottoscrizione di Azure. Per informazioni su come tooaccomplish questa attività, vedere hello **come di toodownload e importare le impostazioni di pubblicazione** sezione di hello [come tooUse hello strumenti da riga di comando di Azure](../xplat-cli-connect.md) articolo.

### <a name="ftp"></a>FTP
informazioni di diagnostica hello tooaccess tramite FTP, visitare hello [portale Azure](https://portal.azure.com), selezionare l'app web, quindi hello **DASHBOARD**. In hello **collegamenti rapidi** sezione hello **registri di diagnostica FTP** e **registri di diagnostica FTPS** collegamenti forniscono accesso toohello log utilizzando il protocollo FTP hello.

> [!NOTE]
> Se non è stato precedentemente configurato nome utente e password per il FTP o distribuzione, è possibile farlo da hello **delle Guide rapide** pagina di gestione selezionando **impostare le credenziali di distribuzione**.
> 
> 

Hello FTP URL restituito nel dashboard di hello è per hello **LogFiles** directory, che conterrà hello seguente sottodirectory:

* [Metodo di distribuzione](web-sites-deploy.md) -se si utilizza un metodo di distribuzione, ad esempio Git, una directory di hello stesso nome, verrà creato e contiene le informazioni correlate toodeployments.
* nodejs: contiene le informazioni di stdout e stderr acquisite da tutte le istanze dell'applicazione, quando loggingEnabled è impostato su true.

### <a name="zip-archive"></a>Archivio ZIP
un archivio Zip dei log di diagnostica hello, utilizzare hello comando seguente da strumenti da riga di comando di Azure hello toodownload:

    azure site log download [sitename]

Questo verrà scaricato un **diagnostics.zip** nella directory corrente hello. Questo archivio contiene hello seguente struttura di directory:

* deployments: log delle informazioni sulle distribuzioni dell'applicazione
* LogFiles
  
  * [Metodo di distribuzione](web-sites-deploy.md) -se si utilizza un metodo di distribuzione, ad esempio Git, una directory di hello stesso nome, verrà creato e contiene le informazioni correlate toodeployments.
  * nodejs: contiene le informazioni di stdout e stderr acquisite da tutte le istanze dell'applicazione, quando loggingEnabled è impostato su true.

### <a name="live-stream-tail"></a>Flusso in diretta (tail)
tooview un flusso di informazioni di log di diagnostica, utilizzare hello comando seguente da strumenti da riga di comando di Azure hello in tempo reale:

    azure site log tail [sitename]

Verrà restituito un flusso di eventi di log che vengono aggiornate quando si verificano nel server di hello. Questo flusso restituirà le informazioni relative alla distribuzione, oltre alle informazioni di stdout e stderr, quando loggingEnabled è impostato su true.

<a id="nextsteps"></a>

## <a name="next-steps"></a>Passaggi successivi
In questo articolo si è appreso come tooenable e alle informazioni di diagnostica per Azure. Mentre questo è utile per informazioni sui problemi con l'applicazione, può puntare tooa problema con un modulo in uso o la versione di hello di Node.js utilizzato dal servizio App dell'App Web è diverso da quello hello quello utilizzato nella distribuzione ambiente.

Per informazioni sull'uso di moduli in Azure, vedere [Uso di moduli Node.js con applicazioni Azure](../nodejs-use-node-modules-azure-apps.md).

Per informazioni sulla specifica di una versione di Node.js per l'applicazione, vedere [Specifica di una versione di Node.js in un'applicazione Azure].

Per ulteriori informazioni, vedere anche hello [Centro per sviluppatori di Node.js](/develop/nodejs/).

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[Specifica di una versione di Node.js in un'applicazione Azure]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

