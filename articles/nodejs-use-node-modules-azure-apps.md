---
title: aaaWorking con moduli Node.js
description: Informazioni su come toowork con moduli Node.js quando si utilizza servizio App di Azure o i servizi Cloud.
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c0e6cd3d-932d-433e-b72d-e513e23b4eb6
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 926358b7eb80a659dbc1015686b06a30d8c9b8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-nodejs-modules-with-azure-applications"></a>Utilizzo di moduli Node.js con le applicazioni Azure
In questo documento vengono fornite le linee guida per l'utilizzo dei moduli Node.js con le applicazioni ospitate in Azure. Queste indicazioni consentono di garantire che l'applicazione utilizzi una versione specifica di moduli, nonché di utilizzare i moduli nativi con Azure.

Se si ha già familiarità con l'utilizzo di moduli Node.js, **package. JSON** e **npm shrinkwrap.json** file, hello le seguenti informazioni fornisce un riepilogo rapido delle quali è descritto in questo articolo:

* Nel Servizio app di Azure vengono riconosciuti i file **package.json** e **npm-shrinkwrap.json** ed è possibile installare moduli in base alle voci incluse in tali file.

* Servizi Cloud di Azure prevede che tutti i moduli toobe installato in ambiente di sviluppo hello e hello **nodo\_moduli** toobe directory incluso come parte del pacchetto di distribuzione hello. È possibile tooenable supporto per l'installazione di moduli utilizzando **package. JSON** o **npm shrinkwrap.json** file nei servizi Cloud; tuttavia, questa configurazione richiede la personalizzazione del valore predefinito di hello script utilizzati dai progetti servizio Cloud. Per un esempio di come tooconfigure questo ambiente, vedere [npm toorun attività di avvio di Azure installare tooavoid i moduli del nodo di distribuzione](https://github.com/woloski/nodeonazure-blog/blob/master/articles/startup-task-to-run-npm-in-azure.markdown)

> [!NOTE]
> Macchine virtuali di Azure non vengono trattati in questo articolo, in quanto dipende dal sistema operativo hello ospitato da hello macchina virtuale hello esperienza di distribuzione in una macchina virtuale.
> 
> 

## <a name="nodejs-modules"></a>Moduli Node.js
I moduli sono pacchetti JavaScript caricabili che forniscono funzionalità specifiche per l'applicazione. I moduli vengono in genere installati utilizzando hello **npm** della riga di comando dello strumento, tuttavia alcuni moduli (ad esempio, un modulo http hello) vengono forniti come parte del pacchetto di hello core Node.js.

Quando vengono installati i moduli, sono archiviati in hello **nodo\_moduli** directory radice di hello della struttura di directory dell'applicazione. Ogni modulo all'interno di hello **nodo\_moduli** directory mantiene il proprio **nodo\_moduli** directory che contiene tutti i moduli che dipende, e questo comportamento viene ripetuto per ogni modulo tutti senso hello catena delle dipendenze hello. Questo ambiente consente toohave ogni modulo installato propri requisiti di versione per i moduli di hello che dipende, ma può causare una struttura di directory di grandi dimensioni.

Distribuzione hello **nodo\_moduli** directory come parte dell'applicazione comporta l'aumento di dimensioni hello della distribuzione di hello quando vengono confrontati toousing un **package. JSON** o  **npm shrinkwrap.json** file; tuttavia, garantisce che le versioni di hello dei moduli di hello utilizzati nell'ambiente di produzione sono hello stesso come moduli hello utilizzati in fase di sviluppo.

### <a name="native-modules"></a>Moduli nativi
Sebbene la maggior parte dei moduli sia semplicemente costituita da file JavaScript in testo normale, alcuni di essi sono immagini binarie specifiche della piattaforma. Questi moduli vengono compilati in fase di installazione, in genere tramite Python e node-gyp. Poiché i servizi Cloud di Azure si basano su hello **nodo\_moduli** cartella distribuito come parte di un'applicazione hello, qualsiasi modulo nativo, incluso come parte dei moduli installato hello dovrebbe funzionare in un servizio cloud, come era installato e compilato su un sistema di sviluppo di Windows.

Servizio app di Azure non supporta tutti i moduli nativi e potrebbe non riuscire a compilare i moduli con prerequisiti specifici. Mentre alcuni moduli più diffusi, come MongoDB, hanno dipendenze native facoltative e funzionano anche senza di esse, due soluzioni alternative hanno fornito risultati positivi con quasi tutti i moduli nativi disponibili attualmente:

* Eseguire **npm installare** in un computer Windows che siano installati i prerequisiti del modulo tutti hello nativo. Distribuire quindi hello creato **nodo\_moduli** cartella come parte di hello applicazione tooAzure servizio App.

  * Prima di compilare, verificare che l'installazione di Node.js locale è l'architettura corrispondente e versione di hello è il più vicino possibile toohello quello utilizzato in Azure (è possono verificare i valori correnti di hello sul runtime dalle proprietà **process.arch**e **process.version**).

* Servizio App di Azure può essere configurato tooexecute personalizzato bash o gli script della shell durante la distribuzione, offrendo hello comandi personalizzati tooexecute di opportunità e con precisione configurare hello modo **npm installare** è in esecuzione. Per un video mostra come tooconfigure tale ambiente, vedere [gli script di distribuzione del sito Web personalizzato con Kudu].

### <a name="using-a-packagejson-file"></a>Utilizzare un file package.json
Hello **package. JSON** file è un modo toospecify hello principale delle dipendenze richieste dall'applicazione in modo che hello piattaforma di hosting possa installare le dipendenze di hello, anziché richiedere hello tooinclude **nodo \_pacchetti** cartella come parte della distribuzione hello. Dopo la distribuzione di un'applicazione hello, hello **installare npm** comando viene utilizzato tooparse hello **package. JSON** file e installare tutte le dipendenze di hello elencate.

Durante lo sviluppo, è possibile utilizzare hello **-Salva**, **-save-dev**, o **-save-facoltativo** parametri durante l'installazione di moduli tooadd una voce per il modulo di hello tooyour **package. JSON** automaticamente file. Per ulteriori informazioni, vedere [npm-install](https://docs.npmjs.com/cli/install).

Uno dei potenziali problemi hello **package. JSON** file è specifica solo la versione di hello per le dipendenze di primo livello. Ogni modulo installato o non può specificare la versione di hello dei moduli di hello che dipende, e pertanto, è possibile che possono finire con una catena di dipendenze diverso rispetto a hello quello utilizzato in fase di sviluppo.

> [!NOTE]
> Quando si distribuiscono tooAzure servizio App, se il <b>package. JSON</b> file fa riferimento a un modulo nativo, è possibile visualizzare un toohello simile di errore quando si pubblica un'applicazione hello usando Git di esempio seguente:
> 
> npm ERR! module-name@0.6.0 install: 'node-gyp configure build'
> 
> npm ERR! 'cmd "/c" "node-gyp configure build"' failed with 1
> 
> 

### <a name="using-a-npm-shrinkwrapjson-file"></a>Utilizzare un file npm-shrinkwrap.json
Hello **npm shrinkwrap.json** file è un tentativo tooaddress hello modulo delle limitazioni di hello **package. JSON** file. Durante la hello **package. JSON** file include solo le versioni per i moduli di primo livello hello, hello **npm shrinkwrap.json** file contiene i requisiti di versione di hello per catena delle dipendenze hello modulo completo.

Quando l'applicazione è pronta per la produzione, è possibile bloccare i requisiti di versione e creare un **npm shrinkwrap.json** file utilizzando hello **confezione npm** comando. Questo comando utilizzerà le versioni di hello attualmente installate in hello **nodo\_moduli** cartella e registrare queste versioni toohello **npm shrinkwrap.json** file. Dopo l'applicazione hello è stato distribuito toohello ambiente di hosting, hello **installare npm** comando viene utilizzato tooparse hello **npm shrinkwrap.json** file e installare tutte le dipendenze di hello elencate. Per ulteriori informazioni, vedere [npm-shrinkwrap](https://docs.npmjs.com/cli/shrinkwrap).

> [!NOTE]
> Quando si distribuiscono tooAzure servizio App, se il <b>npm shrinkwrap.json</b> file fa riferimento a un modulo nativo, è possibile visualizzare un toohello simile di errore quando si pubblica un'applicazione hello usando Git di esempio seguente:
> 
> npm ERR! module-name@0.6.0 install: 'node-gyp configure build'
> 
> npm ERR! 'cmd "/c" "node-gyp configure build"' failed with 1
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Ora che è comprendere come moduli Node.js toouse con Azure, ottengono le informazioni come troppo[specificare la versione di Node. js hello], [compilare e distribuire un'app web Node. js](app-service-web/app-service-web-get-started-nodejs.md), e [come toouse hello Azure della riga di comando Interfaccia per Mac e Linux].

Per ulteriori informazioni, vedere hello [Centro per sviluppatori di Node.js](/nodejs/azure/).

[specificare la versione di Node. js hello]: nodejs-specify-node-version-azure-apps.md
[come toouse hello Azure della riga di comando Interfaccia per Mac e Linux]:cli-install-nodejs.md
[gli script di distribuzione del sito Web personalizzato con Kudu]: https://channel9.msdn.com/Shows/Azure-Friday/Custom-Web-Site-Deployment-Scripts-with-Kudu-with-David-Ebbo
