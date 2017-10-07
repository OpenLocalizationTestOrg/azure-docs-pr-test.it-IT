---
title: aaaSpecifying una versione di Node. js
description: Informazioni su come toospecify hello versione di Node. js utilizzato da siti Web di Azure e servizi Cloud
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a>Specifica di una versione di Node.js in un'applicazione Azure
Quando si ospita un'applicazione Node.js, è consigliabile che l'applicazione usa una versione specifica di Node.js tooensure. Esistono diversi modi tooaccomplish ciò per le applicazioni ospitate in Azure.

## <a name="default-versions"></a>Versioni predefinite
versioni di Node.js Hello fornite da Azure vengono aggiornate continuamente. Se non diversamente specificato, hello versione predefinita specificata nella hello `WEBSITE_NODE_DEFAULT_VERSION` variabile di ambiente da utilizzare. toooverride il valore predefinito, seguire la procedura seguente hello nelle sezioni seguenti di questo articolo

> [!NOTE]
> Se si ospitano l'applicazione in un servizio Cloud di Azure (ruolo web o di lavoro) ed è hello prima volta che è stato distribuito l'applicazione hello, Azure tenterà toouse hello stessa versione di Node. js, come è stato installato l'ambiente di sviluppo se si corrisponde a una delle versioni di hello predefinite disponibili in Azure.
>
>

## <a name="versioning-with-packagejson"></a>Controllo delle versioni con package.json
È possibile specificare una versione di hello di Node.js toobe utilizzata aggiungendo hello seguente tooyour **package. JSON** file:

    "engines":{"node":version}

Dove *versione* è toouse numero versione specifica di hello. È possibile specificare condizioni più complesse per la versione, ad esempio:

    "engines":{"node": "0.6.22 || 0.8.x"}

Poiché 0.6.22 non è una delle versioni di hello disponibili nell'ambiente di hosting hello, hello versione più recente di hello 0,8 serie disponibile sarà utilizzato - 0.8.4.

## <a name="versioning-websites-with-app-settings"></a>Controllo delle versioni di Siti Web con Impostazioni app
Se si ospita un'applicazione hello in un sito Web, è possibile impostare la variabile di ambiente hello **WEBSITE_NODE_DEFAULT_VERSION** versione desiderata di toohello.

## <a name="versioning-cloud-services-with-powershell"></a>Controllo delle versioni dei servizi cloud con PowerShell
Se si ospita un'applicazione hello in un servizio Cloud e si distribuisce un'applicazione hello con Azure PowerShell, è possibile eseguire l'override di versione di Node. js hello predefinita utilizzando hello **Set AzureServiceProjectRole** cmdlet di PowerShell. ad esempio:

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

Parametri di hello nota in hello sopra istruzione maiuscole e minuscole.  È possibile verificare versione corretta di hello di Node.js è stata selezionata per il controllo hello **motori** proprietà del ruolo **package. JSON**.

È inoltre possibile utilizzare hello **Get AzureServiceProjectRoleRuntime** tooretrieve un elenco delle versioni di Node.js disponibili per le applicazioni ospitate come un servizio Cloud.  Verificare sempre la versione di hello di Node.js dipende il progetto in questo elenco.

## <a name="using-a-custom-version-with-azure-websites"></a>Uso di una versione personalizzata con i siti Web di Azure
Sebbene Azure fornisce le diverse versioni predefinite di Node.js, è consigliabile toouse una versione che non viene fornita per impostazione predefinita. Se l'applicazione è ospitato come un sito Web di Azure, è possibile effettuare questa operazione utilizzando hello **iisnode.yml** file. Hello passaggi seguenti descrivono il processo di hello di utilizzo di una versione personalizzata di Node. js con un sito Web di Azure:

1. Creare una nuova directory e quindi creare un **server.js** file all'interno di directory hello. Hello **server.js** file deve contenere i seguenti hello:

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    Verrà visualizzata una versione di Node. js hello utilizzata durante l'esplorazione del sito Web hello.
2. Creare un nuovo sito Web e il nome del sito hello hello della nota. Ad esempio, il seguente hello Usa hello [gli strumenti da riga di comando di Azure] toocreate un nuovo sito Web Azure denominato **mywebsite**e quindi abilitare un repository Git per il sito Web di hello.

        azure site create mywebsite --git
3. Creare una nuova directory denominata **bin** come elemento figlio della directory hello contenente hello **server.js** file.
4. Scaricare una versione specifica di hello di **node.exe** (versione di Windows hello) che si desidera toouse con l'applicazione. Ad esempio, hello seguenti utilizza **curl** versione toodownload 0.8.1:

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    Salvare hello **node.exe** file hello **bin** cartella creata in precedenza.
5. Creare un **iisnode.yml** file hello stessa directory come hello **server.js** file e quindi aggiungere hello seguente toohello contenuto **iisnode.yml** file:

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    Questo percorso è dove hello **node.exe** file all'interno del progetto sarà posizionato dopo aver pubblicato il toohello applicazione sito Web di Azure.
6. Pubblicare l'applicazione. Ad esempio, poiché è stata creata in precedenza un nuovo sito Web con il parametro - git hello, hello comandi riportati di seguito verranno aggiungere hello applicazione file toomy repository Git locale e quindi inviarli repository del sito Web toohello:

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    Dopo aver pubblicato l'applicazione hello, Apri sito Web di hello in un browser. Dovrebbe essere visualizzato il messaggio "Hello from Azure running node version: v0.8.1".

## <a name="next-steps"></a>Passaggi successivi
Dopo aver compreso come versione di hello toospecify di Node.js utilizzati dall'applicazione, consultare come troppo[funzionano con i moduli], [compilare e distribuire un sito Web Node.js](app-service-web/app-service-web-get-started-nodejs.md), e [come toouse hello Azure Strumenti da riga di comando per Mac e Linux].

Per ulteriori informazioni, vedere hello [Centro per sviluppatori di Node.js](https://azure.microsoft.com/develop/nodejs/).

[come toouse hello Azure Strumenti da riga di comando per Mac e Linux]:cli-install-nodejs.md
[gli strumenti da riga di comando di Azure]:cli-install-nodejs.md
[funzionano con i moduli]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
