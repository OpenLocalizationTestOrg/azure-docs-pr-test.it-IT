---
title: aaaCreate un server Jenkins in Azure
description: Installare Jenkins su una macchina virtuale Linux di Azure dal modello di soluzione Jenkins hello e compilare un'applicazione di esempio Java.
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 82ab2ac52594acba131414b449b608978591d4b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a>Creare un server Jenkins in una macchina virtuale Linux di Azure dal portale di Azure hello

Questa Guida introduttiva viene illustrato come tooinstall [Jenkins](https://jenkins.io) in una macchina virtuale Linux Ubuntu con gli strumenti di hello e toowork plug-in configurato con Azure. Al termine, si avrà un server Jenkins in esecuzione in Azure che compila un'app Java di esempio da [GitHub](https://github.com).

## <a name="prerequisites"></a>Prerequisiti

* Una sottoscrizione di Azure.
* Accesso tooSSH nella riga di comando del computer (ad esempio hello Bash shell o [PuTTY](http://www.putty.org/))

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a>Creare VM Jenkins hello dal modello di soluzione hello

Aprire hello [un'immagine del marketplace per Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) nel browser web e selezionare **ottenere IT ora** dalla parte sinistra della pagina hello hello. Hello revisione dei prezzi di dettagli e selezionare **continua**, quindi selezionare **crea** tooconfigure hello Jenkins server hello portale di Azure. 
   
![Finestra di dialogo del portale di Azure](./media/install-jenkins-solution-template/ap-create.png)

In hello **configurare impostazioni di base** scheda, compilare hello seguenti campi:

![Configurare le impostazioni di base](./media/install-jenkins-solution-template/ap-basic.png)

* Usare **Jenkins** come **Nome**.
* Immettere un valore in **Nome utente**. nome utente Hello deve soddisfare [requisiti specifici](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).
* Selezionare **Password** come hello **tipo di autenticazione** e immettere una password. Hello password deve contenere un carattere maiuscolo, un numero e un carattere speciale.
* Utilizzare **myJenkinsResourceGroup** per hello **gruppo di risorse**.
* Scegliere hello **Stati Uniti orientali** [area Azure](https://azure.microsoft.com/regions/) da hello **percorso** elenco a discesa.

Selezionare **OK** tooproceed toohello **configurare le opzioni aggiuntive** scheda. Immettere un server di dominio univoci nome tooidentify hello Jenkins e selezionare **OK**.

![Configurare le opzioni aggiuntive](./media/install-jenkins-solution-template/ap-addtional.png)  

 Dopo la convalida viene eseguita, selezionare **OK** nuovamente da hello **riepilogo** scheda. Infine, selezionare **acquisto** toocreate hello Jenkins VM. Quando il server è pronto, si riceve una notifica in hello portale di Azure:   

![Notifica che informa che Jenkins è pronto](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a>Connettersi tooJenkins

Passare una macchina virtuale tooyour (ad esempio, http://jenkins2517454.eastus.cloudapp.azure.com/) nel web browser. console di Jenkins Hello è accessibile tramite il protocollo HTTP non protette in modo vengono fornite istruzioni sulla console hello pagina tooaccess hello Jenkins in modo sicuro dal computer tramite un tunnel SSH.

![Sbloccare Jenkins](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

Impostare i tunnel hello utilizzando hello `ssh` comando nella pagina di hello dalla riga di comando hello, sostituendo `username` con nome hello di utente amministratore di macchina virtuale hello scelto in precedenza durante la configurazione di macchina virtuale hello dal modello di soluzione hello.

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

Dopo aver avviato il tunnel hello, passare toohttp://localhost:8080 / sul computer locale. 

Ottenere la password iniziale hello eseguendo hello comando nella riga di comando hello connesso tramite SSH toohello Jenkins VM seguente.

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

Sbloccare dashboard Jenkins hello per hello come primo accesso tramite la password iniziale.

![Sbloccare Jenkins](./media/install-jenkins-solution-template/jenkins-unlock.png)

Selezionare **installare suggeriti i plug-in** hello pagina successiva e quindi creare un dashboard di Jenkins Jenkins amministrazione utente utilizzato tooaccess hello.

![Jenkins è pronto per l'uso.](./media/install-jenkins-solution-template/jenkins-welcome.png)

server Jenkins Hello è ora pronto toobuild codice.

## <a name="create-your-first-job"></a>Creare il primo processo

Selezionare **creare nuovi processi** dalla console di Jenkins hello, quindi denominarlo **mySampleApp** e selezionare **progetto Freestyle**, quindi selezionare **OK**.

![Creare un nuovo processo](./media/install-jenkins-solution-template/jenkins-new-job.png) 

Seleziona hello **gestione del codice sorgente** scheda, abilitare **Git**e immettere l'URL nel seguente hello **URL del Repository** campo:`https://github.com/spring-guides/gs-spring-boot.git`

![Definire i repository Git hello](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

Seleziona hello **compilare** tab, quindi selezionare **istruzione di compilazione Aggiungi**, **script richiamare Gradle**. Selezionare **Use Gradle Wrapper** (Usa wrapper di Gradle) e quindi immettere `complete` in **Wrapper location** (Percorso wrapper) e `build` in **Tasks** (Attività).

![Utilizzare toobuild wrapper di Gradle hello](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

Selezionare **Advanced** (Avanzate) e quindi immettere `complete` in hello **radice compilazione script** campo. Selezionare **Salva**.

![Impostare le impostazioni avanzate in fase di compilazione hello Gradle wrapper](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a>Compilare il codice hello

Selezionare **compilare ora** toocompile hello codice e i pacchetti hello app di esempio. Al termine della compilazione, selezionare hello **dell'area di lavoro** collegamento per un progetto di hello.

![Sfoglia file JAR da compilazione hello toohello dell'area di lavoro tooget hello](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

Passare troppo`complete/build/libs` e verificare hello `gs-spring-boot-0.1.0.jar` esiste tooverify la riuscita della compilazione. Il server è diventato di Jenkins pronto toobuild progetti in Azure.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Aggiungere VM di Azure come agenti di Jenkins](jenkins-azure-vm-agents.md)
