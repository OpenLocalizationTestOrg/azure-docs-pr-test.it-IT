---
title: aaaHow toouse io.js con App Web di servizio App di Azure
description: Informazioni su come un'app web nel servizio App di Azure con io.js toouse.
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
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a>Come io.js toouse con App Web di servizio App di Azure
divisione di nodo comuni Hello [io.js] funzionalità progetto Node.js di vari tooJoyent differenze, incluso un modello di controllo più aperto, un ciclo di rilascio più veloce e una più rapida adozione di nuove funzionalità JavaScript sperimentali.

Benché su [Siti Web di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) siano preinstallate molte versioni di Node.js, è consentito anche un file binario Node.js fornito dall'utente. In questo articolo vengono descritti due metodi di attivazione dell'utilizzo di hello di io.js nelle App Web di servizio App: hello utilizzo di uno script di distribuzione estesa, che configura automaticamente Azure toouse hello io.js disponibile più recente, nonché il caricamento manuale di un file binario io.js hello. 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a>Utilizzo di uno script di distribuzione
Durante la distribuzione di un'app Node.js App del servizio Web App esegue un numero di comandi di piccole dimensioni tooensure che hello ambiente è configurato correttamente. Tramite uno script di distribuzione, questo processo può essere personalizzato tooinclude hello download e configurazione di io.js.

Hello [io.js Script di distribuzione](https://github.com/felixrieseberg/iojs-azure) è disponibile su GitHub. io.js tooenable nell'app web, è sufficiente copiare **.deployment**, **deploy** e **IISNode.yml** toohello radice della cartella dell'applicazione e distribuire le app tooWeb.  

primo file Hello, **.deployment**, indica le applicazioni Web toorun **deploy** durante la distribuzione. Questo script esegue tutti i passaggi di solito hello per un'applicazione Node.js, ma anche Scarica hello versione io.js. Infine, **IISNode.yml** Configura App Web toouse hello appena scaricato io.js binario anziché un file binario Node.js di pre-installato.

> [!NOTE]
> hello tooupdate utilizzata io.js binario, eseguire nuovamente la distribuzione dell'applicazione - script hello verrà scaricato una nuova versione di io.js che viene distribuita un'applicazione hello ogni volta.
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a>Utilizzo dell'installazione manuale
l'installazione manuale di una versione personalizzata io.js Hello include solo due passaggi. Scaricare innanzitutto hello **win-x64** binario direttamente da hello [io.js distribuzione]. Sono necessari due file: **iojs.exe** e **iojs.lib**. Salva entrambi file tooa cartella all'interno di un'applicazione web, ad esempio **bin/iojs**.

tooconfigure App Web toouse **iojs.exe** anziché una versione di nodo pre-installata, è possibile creare un **IISNode.yml** file alla radice dell'applicazione hello e aggiungere hello successiva riga.

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a>Passaggi successivi
In questo articolo è stato descritto come io.js toouse con App del servizio Web App, utilizzando sia forniti gli script di distribuzione, nonché l'installazione manuale. 

> [!NOTE]
> io.js è in fase di intenso sviluppo e viene aggiornato più di frequente rispetto a Node.js. Una serie di moduli Node.js potrebbe non funzionare con [io.js; consultare io.js su GitHub] per la risoluzione dei problemi.
> 
> 

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

[io.js]: https://iojs.org
[io.js distribuzione]: https://iojs.org/dist/
[io.js; consultare io.js su GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
