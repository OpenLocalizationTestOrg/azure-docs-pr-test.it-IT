---
title: aaaDeploy un tooLinux applicazione Node.js macchine virtuali in Azure
description: Informazioni su come toodeploy un Node.js applicazione tooLinux le macchine virtuali in Azure.
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a>Distribuire un tooLinux applicazione Node.js macchine virtuali in Azure
Questa esercitazione viene illustrato come un'applicazione Node.js tootake e distribuirlo tooLinux le macchine virtuali in esecuzione in Azure. istruzioni di Hello in questa esercitazione possono essere seguite su qualsiasi sistema operativo che è in grado di eseguire Node.js.

Si apprenderà come:

* Eseguire il fork e la clonazione di un repository GitHub contenente una semplice applicazione TODO;
* Creare e configurare due macchine virtuali Linux in un'applicazione hello Azure toorun;
* Eseguire l'iterazione in un'applicazione hello trasferendo la macchina virtuale aggiornamenti toohello web front-end.

> [!NOTE]
> toocomplete questa esercitazione, è necessario un account GitHub e un account di Microsoft Azure e hello possibilità toouse Git da un computer di sviluppo.
> 
> Se non si ha un account GitHub, è possibile iscriversi [qui](https://github.com/join).
> 
> Se non si ha un account [Microsoft Azure](https://azure.microsoft.com/), è possibile iscriversi [qui](https://azure.microsoft.com/pricing/free-trial/) per ottenere una versione di prova GRATUITA. Questo consentirà anche attraverso hello iscrizione processo per un [Account Microsoft](http://account.microsoft.com) se non hai già uno. In alternativa, se si è eseguita la sottoscrizione a Visual Studio, è possibile [attivare i vantaggi di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
> 
> Se sul computer di sviluppo non è presente GIT e si usa un sistema Macintosh o Windows, è possibile installarlo da [qui](http://www.git-scm.com). Se si utilizza Linux, installare git utilizzando il meccanismo di hello più appropriato, ad esempio `sudo apt-get install git`.
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a>Duplicazione e clonazione hello applicazione TODO
Hello applicazione TODO usata da questa esercitazione implementa un front-end web semplici su un'istanza di MongoDB che tiene traccia di un elenco di attività. Dopo avere effettuato l'accesso tooGitHub, andare [qui](https://github.com/stepro/node-todo) toofind hello applicazione e tramite il collegamento di hello in alto a destra hello fork. In questo modo verrà creato un repository nell'account denominato *nomeaccount*/node-todo.

A questo punto, clonare il repository nel computer di sviluppo:

    git clone https://github.com/accountname/node-todo.git

Si userà il clone del repository hello locale leggermente in un secondo momento quando si apportano modifiche di codice sorgente toohello.

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a>Creazione e configurazione di hello macchine virtuali Linux
Azure supporta il calcolo non elaborato mediante macchine virtuali Linux. Questa parte dei programmi di esercitazione hello come si può creare rapidamente due macchine virtuali Linux e distribuire facilmente hello TODO applicazione toothem, in esecuzione hello front-end web in uno e hello istanza MongoDB hello altri.

### <a name="creating-virtual-machines"></a>Creazione di macchine virtuali
toocreate modo più semplice di Hello una nuova macchina virtuale in Azure è toouse hello portale di Azure. Fare clic su [qui](https://portal.azure.com) toosign in e avviare hello portale di Azure nel web browser. Una volta caricate hello portale di Azure, completare hello alla procedura seguente:

* Fare clic su salve "+ nuovo" collegamento;
* Selezionare una categoria "Calcolo" hello e scegliere "Ubuntu Server 14.04 LTS";
* Seleziona modello di distribuzione di "gestione di risorse" hello e fare clic su "Crea";
* Compilare nozioni di base hello attenendosi alle linee guida:
  * Specificare un nome facilmente identificabile in un secondo momento
  * Per questa esercitazione, scegliere Autenticazione password
  * Creare un nuovo gruppo di risorse con un nome identificabile
* Per la dimensione della macchina virtuale hello, "A1 Standard" è una scelta ragionevole per questa esercitazione.
* Per le impostazioni aggiuntive, verificare il tipo di disco hello "Standard" e accettare che tutti hello impostazioni predefinite rimanenti.
* Avviare la creazione di hello nella pagina Riepilogo hello.

Eseguire hello precedente elaborare due volte toocreate due le macchine virtuali Linux, uno per front-end web hello e uno per l'istanza di MongoDB hello. Creazione di macchine virtuali hello richiederà circa 5-10 minuti.

### <a name="assigning-a-dns-entry-for-virtual-machines"></a>Assegnazione di una voce DNS per le macchine virtuali
Per impostazione predefinita, è possibile accedere alle macchine virtuali create in Azure solo mediante un indirizzo IP pubblico, ad esempio 1.2.3.4. Verifichiamo macchine hello più facilmente identificabili assegnando le voci DNS.

Una volta portale hello indica che le macchine virtuali hello siano state create, fare clic sul collegamento "Macchine virtuali" hello nella barra di spostamento sinistro hello e individuare i computer. Per ogni macchina virtuale:

* Scheda Essentials hello di individuare e fare clic su indirizzo IP pubblico; hello
* Nella configurazione degli indirizzi IP pubblici hello, assegnare un'etichetta del nome DNS e salvare.

portale Hello garantisce che si specifica il nome di hello sia disponibile. Dopo aver salvato la configurazione hello, le macchine virtuali avranno nomi host troppo`machinename.region.cloudapp.azure.com`.

### <a name="connecting-toohello-virtual-machines"></a>Connessione toohello macchine virtuali
Quando è stato eseguito il provisioning delle macchine virtuali, erano le connessioni remote tooallow preconfigurata su SSH. Questo è il meccanismo di hello utilizzeremo tooconfigure hello le macchine virtuali. Se si utilizza Windows per lo sviluppo, è necessario un client SSH tooget se non hai già uno. Una soluzione comune è usare PuTTY, scaricabile da [qui](http://www.chiark.greenend.org.uk/~sgtatham/putty/). I sistemi operativi Macintosh e Linux vengono forniti con una versione di SSH preinstallata.

### <a name="configuring-hello-web-frontend-virtual-machine"></a>Configurazione di macchina virtuale di front-end Web hello
Computer front-end web toohello SSH che è stato creato tramite PuTTY, ssh riga di comando o lo strumento SSH altri preferito. Verrà visualizzato un messaggio di benvenuto seguito da un prompt dei comandi:

Assicurarsi innanzitutto che GIT e il nodo siano entrambi installati:

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

Poiché front-end web dell'applicazione hello si basa su alcuni moduli Node.js nativi, è necessario anche set essenziale di hello tooinstall di strumenti di compilazione:

    sudo apt-get install -y build-essential

Infine, si installano un'applicazione di Node.js chiamata *forever*, che consente di toorun Node.js server applicazioni:

    sudo npm install -g forever

Questi sono tutte le dipendenze di hello necessarie nel front-end web dell'applicazione questa macchina virtuale toobe toorun in grado di hello, così possiamo procedere all'esecuzione di applicazioni. toodo, prima di tutto creata è un clone del repository GitHub hello è duplicato in precedenza in modo che è possibile pubblicare facilmente gli aggiornamenti macchina virtuale di toohello (verranno descritte in questo scenario di aggiornamento in un secondo momento) e quindi clonare hello clone bare tooprovide bare una versione di hello repository che in realtà può essere eseguito.

A partire dalla directory home (~) hello, eseguire hello comandi seguente (sostituendo *accountname* con il nome dell'account utente GitHub):

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

Ora immettere hello nodo todo directory ed eseguire questi comandi:

    npm install
    forever start server.js

Hello front-end web dell'applicazione è in esecuzione, tuttavia non esiste un altro passaggio prima di accedere a un'applicazione hello da un web browser. Hello macchina virtuale creata è protetta da una risorsa di Azure chiamata un *il gruppo di sicurezza di rete*, che è stato creato per quando è stato eseguito il provisioning hello macchina virtuale. Attualmente, questa risorsa consente solo le richieste esterne tooport toobe 22 indirizzato toohello macchina virtuale, che consente le comunicazioni SSH con hello macchina, ma nessun altro elemento. In hello tooview ordine applicazione TODO, vale a dire toorun configurato sulla porta 8080, pertanto questa porta deve anche toobe aperto.

Restituire toohello portale di Azure e completare hello alla procedura seguente:

* Fare clic su "Gruppi di risorse" nella barra di spostamento sinistro hello;
* Selezionare gruppo di risorse hello che contiene la macchina virtuale.
* Nell'elenco risultante di hello delle risorse, selezionare gruppo di sicurezza di rete hello (Buongiorno uno con un'icona dello scudo);
* Nelle proprietà hello, scegliere "regole di sicurezza in ingresso";
* Nella barra degli strumenti hello, fare clic su "Aggiungi".
* Specificare un nome, ad esempio "default-allow-todo"
* Impostare il protocollo hello troppo "TCP";
* Impostare l'intervallo di porte di destinazione hello troppo "8080;"
* Fare clic su OK e attendere hello toobe di regola di sicurezza creato.

Dopo aver creato la regola di sicurezza, è visibile pubblicamente su hello applicazione TODO hello internet ed è possibile esplorare tooit, ad esempio tramite un URL, ad esempio:

    http://machinename.region.cloudapp.azure.com:8080

Si noterà anche se non è stato ancora configurato macchina virtuale di MongoDB hello, hello applicazione TODO viene visualizzato toobe piuttosto funzionale. In questo modo il repository di codice sorgente hello è hardcoded toouse un'istanza di MongoDB già distribuita. Dopo che è stato configurato macchina virtuale di MongoDB hello, si verrà tornare indietro e modificare hello origine codice tooutilize dell'istanza di MongoDB privata invece.

### <a name="configuring-hello-mongodb-virtual-machine"></a>Configurazione di macchina virtuale di MongoDB hello
SSH toohello secondo computer che è stato creato tramite PuTTY, ssh riga di comando o lo strumento SSH altri preferito. Dopo aver visualizzato un messaggio di benvenuto hello e il prompt dei comandi, installare MongoDB (queste istruzioni sono state ricavate dalla [qui](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

Per impostazione predefinita, MongoDB è configurato in modo da essere accessibile solo in locale. Per questa esercitazione, MongoDB verrà configurato in modo è possibile accedere dalla macchina virtuale dell'applicazione hello. In un contesto di sudo, aprire il file /etc/mongod.conf hello e individuare hello `# network interfaces` sezione. Hello modifica `net.bindIp` configurazione valore troppo`0.0.0.0`.

> [!NOTE]
> Questa configurazione è per scopi di hello solo questa esercitazione. **NON** è una procedura di sicurezza consigliata e non deve essere usata in ambienti di produzione.
> 
> 

Verificare ora hello MongoDB servizio è stato avviato:

    sudo service mongod restart

Per impostazione predefinita, MongoDB è attivo sulla porta 27017. Pertanto, in hello allo stesso modo che era necessaria tooopen porta 8080 sulla macchina virtuale di hello web front-end, è necessario tooopen porta 27017 macchina virtuale di MongoDB hello.

Restituire toohello portale di Azure e completare hello alla procedura seguente:

* Fare clic su "Gruppi di risorse" nella barra di spostamento sinistro hello;
* Selezionare gruppo di risorse hello che contiene una macchina virtuale di MongoDB hello.
* Nell'elenco risultante di hello delle risorse, selezionare gruppo di sicurezza di rete hello (Buongiorno uno con un'icona dello scudo) con stesso nome assegnato macchina virtuale di MongoDB toohello; hello
* Nelle proprietà hello, scegliere "regole di sicurezza in ingresso";
* Nella barra degli strumenti hello, fare clic su "Aggiungi".
* Specificare un nome, ad esempio "default-allow-mongo"
* Impostare il protocollo hello troppo "TCP";
* Impostare l'intervallo di porte di destinazione hello troppo "27017";
* Fare clic su OK e attendere hello toobe di regola di sicurezza creato.

## <a name="iterating-on-hello-todo-application"></a>L'iterazione hello applicazione TODO
Finora è stato eseguito il provisioning due macchine virtuali Linux: uno che sia in esecuzione dell'applicazione hello front-end web e uno che esegue un'istanza di MongoDB. Ma si è verificato un problema - istanza MongoDB hello il provisioning non è effettivamente usando ancora front-end web hello. Errore verrà corretto nei aggiornando hello web front-end codice toouse una variabile di ambiente anziché un'istanza a livello di codice.

### <a name="changing-hello-todo-application"></a>La modifica di un'applicazione hello TODO
Nel computer di sviluppo in cui è stato clonato innanzitutto repository nodo todo hello, aprire hello `node-todo/config/database.js` file in un editor qualsiasi e modificare il valore di url hello da valore hardcoded hello come `mongodb://...` troppo`process.env.MONGODB`.

Eseguire il commit delle modifiche e push toohello GitHub master:

    git commit -am "Get MongoDB instance from env"
    git push origin master

Sfortunatamente, questo non pubblica macchina virtuale di hello modifica toohello web front-end. Verifichiamo alcuni ulteriori modifiche toothat macchina virtuale tooenable un meccanismo semplice ma efficace per la pubblicazione degli aggiornamenti in modo rapido, è possibile osservare effetto di hello di hello modifiche nell'ambiente di produzione hello.

### <a name="configuring-hello-web-frontend-virtual-machine"></a>Configurazione di macchina virtuale di front-end Web hello
Tenere presente che un clone del repository nodo todo hello bare abbiamo creato in precedenza nella macchina virtuale di hello web front-end. Si scopre che verrà creato un nuovo Git modifiche toowhich remoto possono essere inserite. Tuttavia, semplicemente push toothis remoto piuttosto non offre modello iterazione rapido hello che gli sviluppatori stanno cercando quando si utilizza il proprio codice.

Ciò che si desidera toodo in grado di toobe è garantire che, quando si verifica un repository remoto toohello di push nella macchina virtuale hello, in esecuzione un'applicazione TODO hello viene aggiornata automaticamente. Fortunatamente, questo è facile tooachieve con git.

GIT espone un numero di hook che vengono chiamati in determinati momenti tooreact tooactions eseguiti sul repository hello. Tali opzioni vengono specificate utilizzando gli script della shell del repository hello `hooks` cartella. hook di Hello che è più applicabile per uno scenario di aggiornamento automatico di hello è hello `post-update` evento.

In una SSH sessione toohello web front-end macchina virtuale, modificare toohello `~/node-todo.git/hooks` directory e aggiungere i seguenti file di contenuto tooa denominato hello `post-update` (sostituendo `machinename` e `region` con le informazioni della macchina virtuale MongoDB):

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

Assicurarsi che il file sia eseguibile eseguendo hello comando seguente:

    chmod 755 post-update

Questo script assicura che un'applicazione server hello corrente viene arrestata, codice hello nel repository clonato hello sia toohello aggiornata più recente, eventuali dipendenze aggiornate vengono soddisfatte, e hello server viene riavviato. Garantisce inoltre che tale ambiente hello è stato configurato in preparazione per la ricezione la prima istanza dell'applicazione aggiornamento tooget hello MongoDB dalla variabile di ambiente.

### <a name="configuring-your-development-machine"></a>Configurazione del computer di sviluppo
Ora entriamo nel computer di sviluppo agganciato toohello macchina virtuale del server front-end web. Questo è semplice come l'aggiunta di repository bare hello nella macchina virtuale hello come remota. Eseguire l'esempio hello toodo di comando seguente (sostituendo *utente* con il nome di accesso web front-end macchina virtuale e *machinename* e *area* a seconda dei casi):

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

Questo è tutto ciò che è necessario tooenable push o attiva la pubblicazione, modifiche di macchina virtuale di toohello web front-end.

### <a name="publishing-updates"></a>Pubblicazione degli aggiornamenti
Si pubblica una modifica hello che è stata effettuata fino a questo punto, in modo che un'applicazione hello userà la propria istanza MongoDB:

    git push azure master

Dovrebbe essere simile toothis di output:

    Counting objects: 4, done.
    Delta compression using up too4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

Dopo il completamento del comando, provare ad aggiornare un'applicazione hello in un web browser. È necessario essere in grado di toosee che elenco TODO hello presentata in questo documento è vuoto e non è più vincolata toohello condiviso distribuito istanza MongoDB.

esercitazione hello toocomplete verifichiamo modifica di un altro, è più visibile. Nel computer di sviluppo, aprire il file di node-todo/public/index.html hello usando l'editor preferito. Individuare l'intestazione jumbotron hello e modificare il titolo di hello da "Sono un Todo-aholic" troppo "sono un aholic Todo in Azure!".

A questo punto, eseguire il commit:

    git commit -am "Azurify hello title"

Questa volta, consente di pubblicare hello modifica tooAzure prima di pubblicarlo come repository di GitHub toohello tooback:

    git push azure master

Dopo il completamento del comando, pagina web hello di aggiornamento per visualizzare le modifiche di hello. Perché vengano visualizzate correttamente, push hello modifica toohello indietro origine remota: 

    git push origin master

## <a name="next-steps"></a>Passaggi successivi
In questo articolo è stato illustrato come un'applicazione Node.js tootake e distribuirlo tooLinux le macchine virtuali in esecuzione in Azure. toolearn informazioni sulle macchine virtuali Linux in Azure, vedere [tooLinux introduzione in Azure](/documentation/articles/virtual-machines-linux-introduction/).

Per ulteriori informazioni su come toodevelop delle applicazioni Node.js in Azure, vedere hello [Centro per sviluppatori di Node.js](/develop/nodejs/).

