---
title: Come utilizzare io.js con Azure applicazione servizio Web App
description: Imparare a utilizzare un'applicazione web nel servizio di applicazione Azure con io.js.
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 4800504e1939a46842d15e8c9d4279a4b9cae787
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-iojs-with-azure-app-service-web-apps"></a>Come utilizzare io.js con Azure applicazione servizio Web App
Il popolare fork del nodo [io.js] presenta diverse differenze rispetto al progetto Node.js di Joyent, incluso un modello di governance più aperto, un ciclo di rilascio presumibilmente più veloce e un'adozione più rapida delle funzionalità JavaScript nuove e sperimentali.

Benché su [Siti Web di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) siano preinstallate molte versioni di Node.js, è consentito anche un file binario Node.js fornito dall'utente. In questo articolo vengono descritti due metodi consente l'utilizzo di io.js applicazione servizio Web App: l'utilizzo di uno script di distribuzione estesa, che configura automaticamente Azure per utilizzare la versione più recente di io.js disponibili, nonché il caricamento manuale di un io.js binario. 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a>Utilizzo di uno script di distribuzione
Durante la distribuzione di un'applicazione Node.js, Siti Web di Azure esegue una serie di piccoli comandi per garantire che l'ambiente sia configurato correttamente. Usando uno script di distribuzione, questo processo può essere personalizzato in modo da includere il download e la configurazione di io.js.

Lo [script di distribuzione io.js](https://github.com/felixrieseberg/iojs-azure) è disponibile su GitHub. Per abilitare io.js nel proprio sito Web, è sufficiente copiare **.deployment**, **deploy.cmd** e **IISNode.yml** nella radice della cartella dell'applicazione e distribuirli in App Web.  

Il primo file, **.deployment**, indica ad App Web di eseguire **deploy.cmd** durante la distribuzione. Questo script esegue tutti i passaggi abituali per un applicazione Node.js, ma scarica anche la versione più recente di io.js. Infine, **IISNode.yml** configura App Web in modo da usare il file binario io.js appena scaricato anziché un file binario Node.js preinstallato.

> [!NOTE]
> Per aggiornare il file binario io.js usato, eseguire nuovamente la distribuzione dell'applicazione; lo script scaricherà una nuova versione di io.js ogni volta che l'applicazione viene distribuita.
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a>Utilizzo dell'installazione manuale
L'installazione manuale di una versione personalizzata di io.js prevede solo due passaggi. Innanzitutto, scaricare il file binario **win-x64** direttamente dalla [distribuzione io.js]. Sono necessari due file: **iojs.exe** e **iojs.lib**. Salvare entrambi i file in una cartella all'interno del proprio sto Web, ad esempio in **bin/iojs**.

Per configurare App Web di Azure in modo da usare **iojs.exe** anziché una versione del nodo preinstallata, creare un file **IISNode.yml** nella directory principale dell'applicazione e aggiungere la riga seguente.

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a>Passaggi successivi
In questo articolo si è appreso come usare io.js con Siti Web di Azure, usando sia gli script di distribuzione forniti sia l'installazione manuale. 

> [!NOTE]
> io.js è in fase di intenso sviluppo e viene aggiornato più di frequente rispetto a Node.js. Una serie di moduli Node.js potrebbe non funzionare con [io.js; consultare io.js su GitHub] per la risoluzione dei problemi.
> 
> 

## <a name="whats-changed"></a>Modifiche apportate
* Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Per iniziare a usare Servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

[io.js]: https://iojs.org
[distribuzione io.js]: https://iojs.org/dist/
[io.js; consultare io.js su GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
