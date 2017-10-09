---
title: aaaCI/CD da Jenkins tooAzure le macchine virtuali con Team Services | Documenti Microsoft
description: Configurare l'integrazione continua (CI) e la distribuzione continua (CD) di un'app Node.js tramite Jenkins tooAzure VM da Release Management in Visual Studio Team Services (VSTS) o Microsoft Team Foundation Server (TFS)
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a>Distribuire le macchine virtuali di tooLinux app con Jenkins e Team Services

Integrazione continua (CI) e distribuzione continua (CD) sono una pipeline con cui è possibile compilare, rilasciare e distribuire codice. Team Services fornisce un set completo, completo di strumenti di automazione CI/CD-ROM per tooAzure di distribuzione. Jenkins è uno strumento di terze parti diffuso basato su server per CI/CD che offre anche l'automazione CI/CD. È possibile utilizzare entrambi toocustomize contemporaneamente la modalità di recapito di applicazione cloud o nel servizio.

In questa esercitazione è utilizzare Jenkins toobuild un **app web Node. js**, toodeploy di Visual Studio Team Services e si tooa [gruppo distribuzione](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) contenente macchine virtuali Linux.

Si apprenderà come:

> [!div class="checklist"]
> * Creare l'app in Jenkins
> * Configurare Jenkins per l'integrazione con Team Services
> * Creare un gruppo di distribuzione per hello macchine virtuali di Azure
> * Creare una definizione di versione che consente di configurare le macchine virtuali hello e distribuisce l'applicazione hello

## <a name="before-you-begin"></a>Prima di iniziare

* È necessario l'account di accesso tooa Jenkins. Se non è ancora stato creato un server Jenkins, vedere la [documentazione di Jenkins](https://jenkins.io/doc/). 

* Accedi tooyour account Team Services (`https://{youraccount}.visualstudio.com`). 
  È possibile ottenere un [account di Team Services gratuito](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).

  > [!NOTE]
  > Per ulteriori informazioni, vedere [connettere servizi tooTeam](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).

* Se non si dispone di un token di accesso personale nell'account di Team Services, crearne uno. Jenkins richiede questa tooaccess informazioni dell'account Team Services.
  Lettura [come creare un token di accesso personale per Team Services e TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn come toogenerate uno.

## <a name="get-hello-sample-app"></a>Ottenere app di esempio hello

È necessario un toodeploy app archiviati in un repository Git.
Per questa esercitazione, si consiglia di usare [questa app di esempio disponibile da GitHub](https://github.com/azooinmyluggage/fabrikam-node).

1. Creare un fork di questa app e prendere nota del percorso di hello (URL) per l'utilizzo nei passaggi successivi di questa esercitazione.

1. Rendere fork hello **pubblica** toosimplify connessione tooGitHub in seguito.

> [!NOTE]
> Per ulteriori informazioni, vedere [Fork a repo](https://help.github.com/articles/fork-a-repo/) (Biforcazione di un repository) e [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/) (Rendere pubblico un repository privato).

> [!NOTE]
> app Hello è stato compilato utilizzando [Yeoman](http://yeoman.io/learning/index.html); Usa **Express**, **bower**, e **grunt**; e ha alcuni **npm**pacchetti come dipendenze.
> app di esempio Hello contiene un set di [modelli di gestione risorse di Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) che vengono utilizzati toodynamically creare hello macchine virtuali per la distribuzione in Azure. Questi modelli vengono utilizzati dalle attività di hello [definizione di versione di Team Services](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).
> modello principale Hello consente di creare un gruppo di sicurezza di rete, una macchina virtuale e una rete virtuale. Assegna un indirizzo IP pubblico e apre la porta 80 in ingresso. Verrà inoltre aggiunto un tag che viene utilizzato dalla distribuzione di hello distribuzione gruppo hello troppo selezionare macchine tooreceive hello.
>
> esempio Hello contiene anche uno script che configura Nginx e distribuisce l'applicazione hello. Viene eseguita in ognuna delle macchine virtuali hello. In particolare, script hello installa nodo, Nginx e PM2; Configura Nginx e PM2; Avvia quindi hello nodo app.

## <a name="configure-jenkins-plugins"></a>Configurare i plug-in di Jenkins

In primo luogo è necessario configurare due plug-in di Jenkins per **NodeJS** e l'**integrazione con Team Services**.

1. Aprire l'account di Jenkins e scegliere **Manage Jenkins** (Gestisci Jenkins).

1. In hello **gestire Jenkins** pagina, scegliere **gestire plug-in**.

1. Hello di filtro hello elenco toolocate **NodeJS** plug-in e l'installazione senza riavviare.

   ![Aggiunta di hello NodeJS plug-in tooJenkins](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. Hello di filtro hello elenco toofind **Team Foundation Server** plug-in e installarlo. (questo plug-in funziona sia con Team Services che con Team Foundation Server). Il riavvio di Jenkins non è necessario.

## <a name="configure-jenkins-build-for-nodejs"></a>Configurare la compilazione di Jenkins per Node.js

In Jenkins creare un nuovo progetto di compilazione e configurarlo come segue:

1. In hello **generale** , immettere un nome per il progetto di compilazione.

1. In hello **gestione del codice sorgente** , selezionare **Git** e immettere i dettagli di hello del repository di hello e ramo hello contenente il codice dell'app.

   ![Aggiungere una compilazione tooyour repository](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > Se il repository non è pubblico, scegliere **Aggiungi** e fornire le credenziali tooconnect tooit.

1. In hello **trigger di compilazione** , selezionare **polling SCM** e immettere pianificazione hello `H/03 * * * *` repository Git di hello toopoll modifiche ogni tre minuti. 

1. In hello **ambiente Build** , selezionare **fornire nodo &amp; npm bin / percorso cartella** e immettere `NodeJS` per hello valore JS installazione del nodo. Lasciare **npmrc file** impostato su "use system default" (usa impostazioni predefinite di sistema).

1. In hello **compilare** , immettere il comando hello `npm install` tooensure vengono aggiornate tutte le dipendenze.

## <a name="configure-jenkins-for-team-services-integration"></a>Configurare Jenkins per l'integrazione con Team Services

1. In hello **azioni post-compilazione** scheda per **file tooarchive**, immettere `**/*` tooinclude tutti i file.

1. Per **attivare rilascio in TFS/Team Services**, immettere l'URL completo di hello del tuo account (ad esempio `https://your-account-name.visualstudio.com`), nome del progetto, un nome per la definizione di versione di hello (creato in un secondo momento), hello e hello account tooyour tooconnect di credenziali.
   È necessario il nome utente e hello PAT creato in precedenza. 

   ![Configurazione delle azioni di post-compilazione in Jenkins](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. Salvare il progetto di compilazione hello.

## <a name="create-a-jenkins-service-endpoint"></a>Creare un endpoint servizio di Jenkins

Un endpoint del servizio consente tooJenkins tooconnect Team Services.

1. Aprire hello **servizi** pagina Team Services, aprire hello **nuovo Endpoint del servizio** elenco e scegliere **Jenkins**.

   ![Aggiungere un endpoint di Jenkins](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. Immettere un nome che verrà utilizzato toorefer toothis connessione.

1. Immettere l'URL di hello del server Jenkins e segni di graduazione hello **accettare certificati SSL non attendibili** opzione.

1. Immettere nome utente hello e una password per l'account di Jenkins.

1. Scegliere **verificare connessione** toocheck che hello informazioni sia corretto.

1. Scegliere **OK** endpoint del servizio toocreate hello.

## <a name="create-a-deployment-group"></a>Creare un gruppo di distribuzione

È necessario un [gruppo distribuzione](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) troppo contengono le macchine virtuali hello.

1. Aprire hello **versioni** scheda di hello **compilare &amp; versione** hub, quindi aprire hello **gruppi di distribuzione** scheda e scegliere **+ nuovo**.

1. Immettere un nome per il gruppo di distribuzione hello e una descrizione facoltativa.
   quindi scegliere **Crea**.

attività di distribuzione di gruppo di risorse di Azure Hello crea e registra le macchine virtuali hello quando viene eseguita utilizzando il modello di gestione risorse di Azure hello.
Non necessari toocreate e registrare le macchine virtuali hello manualmente.

## <a name="create-a-release-definition"></a>Creare una definizione di versione

Definizione di una versione specifica eseguirà l'applicazione hello toodeploy processo hello Team Services.
definizione di versione toocreate hello in Team Services:

1. Aprire hello **versioni** scheda di hello **compilare &amp; versione** hub, aprire hello  **+**  giù nell'elenco di hello di definizioni di versione e scegliere Hello **Crea definizione di versione**. 

1. Seleziona hello **vuoto** modello e scegliere **Avanti**.

1. In hello **elementi** sezione, fare clic su **collegare un elemento** e scegliere **Jenkins**. Selezionare la connessione all'endpoint servizio Jenkins, Quindi selezionare hello Jenkins origine processo e scegliere **crea**. 

1. In hello nuova definizione di versione, scegliere **+ Aggiungi attività** e aggiungere un **distribuzione gruppo di risorse di Azure** ambiente predefinito toohello di attività.

1. Scegliere toohello avanti sulla freccia a discesa hello **+ Aggiungi attività** collegare e aggiungere una definizione di toohello fase di distribuzione gruppo.

   ![Aggiunta di una fase di gruppo di distribuzione](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. Nel catalogo di attività hello, aprire hello **utilità** sezione e aggiungere un'istanza di hello **Script della Shell** attività.

1. set di modelli di parametri di Hello utilizzato nell'attività di distribuzione di gruppo di risorse di Azure hello hello admin password utilizzata tooconnect toohello macchine virtuali.
   Fornire la password con variabile hello **$(adminpassword)**:
   
   - Aprire hello **variabili** scheda e hello **variabili** sezione, immettere il nome di hello `adminpassword`.

   - Immettere la password dell'amministratore di hello.

   - Scegliere hello "lucchetto" icona Avanti toohello valore textbox tooprotect hello password. 

## <a name="configure-hello-azure-resource-group-deployment-task"></a>Configurare l'attività di distribuzione di gruppo di risorse di Azure hello

Hello **distribuzione gruppo di risorse di Azure** attività è gruppo di distribuzione utilizzato toocreate hello. Configurare l'app come segue:

* **Sottoscrizione di Azure:** selezionare una connessione dall'elenco di hello in **connessioni del servizio di Azure disponibili**. 
  Se viene visualizzata alcuna connessione, scegliere **Gestisci**selezionare **nuovo Endpoint del servizio** quindi **Azure Resource Manager**e seguire le istruzioni di hello.
  Restituire la definizione di tipo versione tooyour, hello aggiornamento **sottoscrizione di Azure Resource Manager** elenco hello selezionare la connessione e creato.

* **Gruppo di risorse**: immettere un nome del gruppo di risorse hello creato in precedenza.

* **Percorso**: selezionare un'area per la distribuzione di hello.

  ![Creare un nuovo gruppo di risorse](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* **Percorso del modelli**:`URL of hello file`

* **Collegamento al modello**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.json`

* **Collegamento ai parametri del modello**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`

* **Eseguire l'override di parametri di modello**: un elenco di hello eseguire l'override di valori, ad esempio: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.<br />Inserire i propri valori specifici per hello {segnaposto}. 

* **Abilita i prerequisiti**: `Configure with Deployment Group agent`

* **Endpoint TFS/VSTS**: scegliere **Aggiungi** e, nella finestra di dialogo "Aggiungi nuova connessione a servizi/Team Server Team Foundation" hello, selezionare **autenticazione basata su Token**. Immettere un nome di connessione hello e l'URL di hello del progetto team. Quindi generare e immettere un [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) il progetto team tooyour di tooauthenticate hello connessione.

  ![Creare un token di accesso personale](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* **Progetto team**: selezionare il progetto corrente.

* **Gruppo di distribuzione**: immettere hello stesso nome del gruppo di distribuzione che si utilizzi per hello **gruppo di risorse** parametro.

le impostazioni predefinite di Hello per attività di distribuzione di gruppo di risorse di Azure hello sono toocreate o aggiorneranno una risorsa e toodo in modo incrementale. attività Hello crea hello macchine virtuali hello prima volta che viene eseguito e successivamente semplicemente aggiornarli.

## <a name="configure-hello-shell-script-task"></a>Configurare l'attività Script della Shell hello

Hello **Script della Shell** attività è una configurazione di hello tooprovide utilizzati per un toorun di script in ogni server tooinstall Node.js e avviare hello App Windows. Configurare l'app come segue:

* **Percorso script**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`

* **Specifica directory di lavoro**: `Checked`

* **Directory di lavoro**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`
   
## <a name="rename-and-save-hello-release-definition"></a>Rinominare e salvare la definizione di versione hello

1. Modificare il nome di hello del nome di hello versione definizione toohello specificato nel **azioni post-compilazione** scheda della compilazione hello in Jenkins. Quando vengono aggiornati gli elementi di origine hello, Jenkins richiede questo nome toobe in grado di tootrigger una nuova versione.

1. Facoltativamente, modificare il nome di hello dell'ambiente di hello facendo clic sul nome hello. 

1. Scegliere **Salva** e quindi **OK**.

## <a name="start-a-manual-deployment"></a>Avviare una distribuzione manuale

1. Scegliere **+ Versione** e selezionare **Crea versione**.

1. Selezionare una compilazione hello è completato nell'elenco a discesa evidenziato hello e scegliere **crea**.

1. Scegliere il collegamento di rilascio hello nel messaggio popup di hello. Ad esempio: "Versione **Versione-1** creata."

1. Aprire hello **registri** scheda output della console toowatch hello versione.

1. Nel browser aprire hello URL di uno dei server hello è stato aggiunto il gruppo di distribuzione tooyour. Ad esempio, immettere `http://{your-server-ip-address}`

## <a name="start-a-cicd-deployment"></a>Avviare una distribuzione CI/CD

1. Definizione di versione di hello, deselezionare hello **abilitato** casella di controllo in hello **le opzioni di controllo** sezione delle impostazioni di hello per attività di distribuzione di gruppo di risorse di Azure hello.
   Per le distribuzioni future toohello distribuzione gruppo di esistente, non è necessario toore-eseguire questa attività.

1. Passare repository Git di origine toohello e modificare contenuto hello di hello **h1** intestazione nel file hello [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).

1. Eseguire il commit delle modifiche.

1. Dopo alcuni minuti, si noterà una nuova versione creata in hello **versioni** pagina di Team Services o TFS. Aprire hello versione toosee hello distribuzione in corso. Congratulazioni.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si automatizzata hello di tooAzure un'app tramite servizi di Team per il rilascio e di compilazione Jenkins. Si è appreso come:

> [!div class="checklist"]
> * Creare l'app in Jenkins
> * Configurare Jenkins per l'integrazione con Team Services
> * Creare un gruppo di distribuzione per hello macchine virtuali di Azure
> * Creare una definizione di versione che consente di configurare le macchine virtuali hello e distribuisce l'applicazione hello

Spostare toolearn esercitazione successiva toohello ulteriori informazioni su come dello stack toodeploy una luce (Linux Apache, MySQL e PHP).

> [!div class="nextstepaction"]
> [Distribuire lo stack LAMP](tutorial-lamp-stack.md)