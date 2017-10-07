---
title: aaaLocal distribuzione Git tooAzure servizio App
description: Informazioni su come tooenable locale Git distribuzione tooAzure servizio App.
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a>TooAzure distribuzione Git locale del servizio App
In questa esercitazione illustra come toodeploy app troppo[Azure App Service] da un archivio Git nel computer locale. Servizio App supporta questo approccio con hello **Git locale** opzione di distribuzione in hello [portale Azure].  
Molti dei comandi Git hello descritti in questo articolo vengono eseguite automaticamente durante la creazione di un'applicazione di servizio App utilizzando hello [interfaccia della riga di comando di Azure] come descritto [qui](app-service-web-get-started.md).

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa esercitazione, è necessario:

* Git. È possibile scaricare installazione hello binario [qui](http://www.git-scm.com/downloads).  
* Conoscenze di base di Git.
* Un account Microsoft Azure. Se non si ha un account, è possibile [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial) oppure [attivare i vantaggi per i sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.  
> 
> 

## <a name="Step1"></a>Passaggio 1: Creare un repository locale
Eseguire hello seguenti attività toocreate un nuovo repository Git.

1. Avviare uno strumento da riga di comando, ad esempio **GitBash** (Windows) o **Bash** (shell Unix). Nei sistemi di OS X è possibile accedere hello della riga di comando tramite hello **Terminal** dell'applicazione.
2. Passare toohello directory in cui deve essere collocato toodeploy contenuto hello.
3. Utilizzare hello comando tooinitialize un nuovo repository Git di seguito:

```bash  
git init
```

## <a name="Step2"></a>Passaggio 2: Eseguire il commit del contenuto
Il servizio app supporta applicazioni create in diversi linguaggi di programmazione. 

1. Se il repository include già contenuto ignorare questo punto e spostare toopoint 2 di seguito. Se non include ancora il contenuto, popolare il repository con un file HTML statico come indicato di seguito: 
   
   * Utilizzando un editor di testo, creare un nuovo file denominato **index.html** nella radice di hello del repository Git hello
   * Aggiungere hello dopo il testo contenuto hello per index.html hello del file e salvarlo: *Git Hello!*
2. Da hello della riga di comando, verificare che nella directory radice di hello del repository Git. Utilizzare quindi hello repository tooyour file tooadd di comando seguente:

```bash  
git add -A
```
3. Successivamente, eseguire il commit del repository di hello modifiche toohello utilizzando hello comando seguente:

```bash  
git commit -m "Hello Azure App Service"
```  

## <a name="Step3"></a>Passaggio 3: Abilitare hello repository di applicazione di servizio App
Eseguire hello seguendo i passaggi tooenable un repository Git per l'applicazione di servizio App.

1. Accedi toohello [portale Azure].
2. Nel pannello dell'app del servizio app fare clic su **Impostazioni > Origine distribuzione**. Fare clic su **Scegliere l'origine**, quindi su **Repository Git locale** e infine su **OK**.  
   
    ![Repository Git locale](./media/app-service-deploy-local-git/local_git_selection.png)
3. Se questa è la prima impostazione del tempo di un archivio in Azure, è necessario toocreate le credenziali di accesso per tale. Utilizzare li toolog in hello Azure repository e push delle modifiche dall'archivio Git locale. Dal pannello dell'app fare clic su **Impostazioni > Credenziali per la distribuzione**, quindi configurare il nome utente e la password per la distribuzione. Al termine, fare clic su **Salva**.
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <a name="Step4"></a>Passaggio 4: Distribuire il progetto
Utilizzare hello seguendo i passaggi toopublish il tooApp app servizio tramite Git locale.

1. Nel pannello dell'app nel portale di Azure hello, fare clic su **Impostazioni > proprietà** per hello **URL Git**.
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    **URL GIT** è hello riferimento remoto toodeploy toofrom il repository locale. Utilizzare questo URL in hello alla procedura seguente.
2. Utilizzando hello della riga di comando, verificare che trovano nella radice di hello del repository Git locale.
3. Utilizzare `git remote` riferimento remoto hello tooadd elencato in **URL Git** ottenuto al passaggio 1. Il comando avrà un aspetto simile toohello seguenti:
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > Hello **remoto** comando aggiunge un repository remoto tooa di riferimento con nome. In questo esempio viene creato un riferimento denominato 'azure' per il repository dell'app Web.
   > 
   > 
4. Eseguire il push del contenuto tooApp servizio utilizzando hello nuovo **azure** remoto appena creato.

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. Tornare tooyour app nel portale di Azure hello. Una voce di log il push più recente deve essere visualizzata in hello **distribuzioni** blade. 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. Fare clic su hello **Sfoglia** pulsante nella parte superiore di hello di hello di tooverify pannello hello dell'app contenuto è stato distribuito. 

## <a name="Step5"></a>Risoluzione dei problemi
di seguito Hello sono errori o problemi comunemente riscontrati durante l'uso di Git toopublish tooan app del servizio App in Azure:

- - -
**Sintomo**: Impossibile tooaccess [siteURL]: Impossibile troppo tooconnect [scmAddress]

**Causa**: questo errore può verificarsi se l'applicazione hello non è in esecuzione.

**Risoluzione**: inizio hello app nel portale di Azure hello. Distribuzione GIT non funzionerà a meno che non è in esecuzione app hello. 

- - -
**Sintomo**: non è possibile risolvere il nome dell'host 'nomehost'.

**Causa**: questo errore può verificarsi se le informazioni sull'indirizzo hello immessi durante la creazione di hello 'azure' remoto non è corretta.

**Risoluzione**: hello utilizzare `git remote -v` comando toolist tutti i componenti remoti, insieme a URL hello associata. Verificare che l'URL di hello per hello 'azure' remoto sia corretto. Se necessario, rimuovere e ricreare questo remoto hello URL sia corretto.

- - -
**Sintomo**: non sono stati trovati riferimenti in comune e non ne sono stati specificati. Non viene eseguita alcuna operazione. Forse è necessario specificare un ramo, ad esempio 'master'.

**Causa**: questo errore può verificarsi se non si specifica un ramo, quando si esegue un'operazione di push git e non set hello push.default valore utilizzato da Git.

**Risoluzione**: operazione hello push nuovamente specificando ramo master hello. ad esempio:

```bash  
git push azure master
```
- - -
**Sintomo**: non sono state trovate corrispondenze per src refspec [nomeramo].

**Causa**: questo errore può verificarsi se si tenta di ramo tooa toopush diverso da quello master in hello 'azure' remoto.

**Risoluzione**: operazione hello push nuovamente specificando ramo master hello. ad esempio:

```bash  
git push azure master
```
- - -
**Sintomo**: RPC non riuscita; risultato = 22, codice HTTP = 502.

**Causa**: questo errore può verificarsi se si tenta di toopush un repository git di grandi dimensioni tramite HTTPS.

**Risoluzione**: modificare la configurazione di git hello in più grande successivo hello toomake macchina locale hello

```bash  
git config --global http.postBuffer 524288000
```
- - -
**Sintomo**: errore - repository tooremote eseguito il commit di modifiche ma l'app web non è stato aggiornato.

**Causa**: questo errore può verificarsi se si distribuisce un'app Node.js contenente un file package.json che specifica altri moduli necessari.

**Risoluzione**: i messaggi aggiuntivi contenenti 'npm ERR!' deve essere connesso toothis precedente errore e può fornire contesto aggiuntivo in caso di errore hello. esempio Hello è note le cause di questo errore e hello corrispondente 'npm ERR!' messaggio:

* **File package.json in formato non corretto**: npm ERR! Non è stato possibile leggere le dipendenze.
* **Modulo nativo senza una distribuzione binaria per Windows**:
  
  * npm ERR! Si è verificato un errore di \`cmd "/c" "node-gyp rebuild"\` con 1
    
      OPPURE
  * npm ERR! [modulename@version] preinstall: \`make || gmake\`

## <a name="additional-resources"></a>Risorse aggiuntive
* [Documentazione su Git](http://git-scm.com/documentation)
* [Documentazione del progetto Kudu](https://github.com/projectkudu/kudu/wiki)
* [La distribuzione continua tooAzure servizio App](app-service-continuous-deployment.md)
* [Come toouse PowerShell per Azure](/powershell/azure/overview)
* [Come toouse hello interfaccia della riga di comando di Azure](../cli-install-nodejs.md)

[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[portale Azure]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[interfaccia della riga di comando di Azure]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
