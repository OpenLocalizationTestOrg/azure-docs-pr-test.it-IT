---
title: aaaDeploy tooAzure servizio App con Jenkins Plugin | Documenti Microsoft
description: Informazioni su come toodeploy di plug-in Azure App Service Jenkins toouse un Java web app tooAzure in Jenkins
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 7/24/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 080be7277555ce7d688dccdf38eef309e7a7b194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a>Distribuire tooAzure servizio App con plug-in di Jenkins 
toodeploy un tooAzure di app web Java, è possibile utilizzare l'interfaccia CLI di Azure in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) alternativa, è possibile utilizzare di hello [plug-in Azure App Service Jenkins](https://plugins.jenkins.io/azure-app-service). In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Configurare Jenkins toodeploy tooAzure servizio App tramite FTP 
> * Configurare Jenkins toodeploy tooAzure servizio App in Linux con Docker 

## <a name="create-and-configure-jenkins-instance"></a>Creare e configurare un'istanza di Jenkins
Se si dispone già di un master Jenkins, iniziare con hello [modello di soluzione](install-jenkins-solution-template.md), che include JDK8 e hello seguendo i plug-in obbligatorio:

* [Plug-in Git client Jenkins](https://plugins.jenkins.io/git-client) 2.4.6 
* [Plug-in Docker Commons](https://plugins.jenkins.io/docker-commons) 1.4.0
* [Azure Credentials](https://plugins.jenkins.io/azure-credentials) 1.2
* [Servizio app di Azure](https://plugins.jenkins.io/azure-app-server) versione 0.1

È possibile utilizzare hello toodeploy plug-in servizio App App Web in tutti i linguaggi (ad esempio, c#, PHP, Java e node.js e così via) supportato dal servizio App di Azure. In questa esercitazione, si sta usando app Java di esempio hello, [semplice Java Web App per Azure](https://github.com/azure-devops/javawebappsample). toofork hello repository tooyour proprietari di account GitHub, fare clic su hello **Fork** pulsante nell'angolo superiore destro di hello.  

Sono necessari per la compilazione progetto Java hello Java JDK e Maven. Assicurarsi di che installare i componenti di hello nel database master di Jenkins hello o agente VM hello se si utilizza uno per l'integrazione continua. 

tooinstall, di log nell'istanza di Jenkins toohello tramite SSH ed eseguire hello seguenti comandi:

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

Per la distribuzione tooApp servizio su Linux, è necessario anche tooinstall Docker nello schema di Jenkins hello o agente VM hello utilizzato per la compilazione. Vedere l'articolo di toothis tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.

## <a name="add-azure-service-principal-toojenkins-credential"></a>Aggiungere credenziali tooJenkins dell'entità servizio di Azure

Un'entità servizio di Azure è tooAzure toodeploy necessari. 

<ol>
<li>Utilizzare [CLI di Azure](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) o [portale di Azure](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate un'entità servizio di Azure</li>
<li>Nel dashboard di Jenkins hello, fare clic su **credenziali -> sistema ->**. Fare clic su **Global credentials(unrestricted)**.</li>
<li>Fare clic su **Aggiungi credenziali** tooadd un'entità servizio di Microsoft Azure compilando hello ID sottoscrizione, l'ID Client, segreto Client ed Endpoint Token OAuth 2.0. Indicare un ID, **mySp**, per l'uso nei passaggi successivi.</li>
</ol>

## <a name="azure-app-service-plugin"></a>Plug-in Servizio app di Azure

Versione 1.0 di plug-in Azure App Service supporta la distribuzione continua tooAzure App Web tramite:

* GIT e FTP
* Docker per App Web in Linux

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a>Configurare Jenkins toodeploy App Web tramite FTP tramite il dashboard di Jenkins hello

toodeploy il tooAzure di project Web App, è possibile caricare gli artefatti di compilazione (ad esempio, file .war in Java) utilizzando Git o FTP.

Prima di configurare il processo di hello in Jenkins, è necessario un piano di servizio App di Azure e un'App Web per app Java di hello in esecuzione.


1. Creare un piano di servizio App di Azure con hello **libero** tariffario utilizzando hello [crea piano di servizio App az](/cli/azure/appservice/plan#create) comando CLI. piano di servizio App Hello definisce hello risorse fisiche utilizzate toohost app. Tutte le applicazioni assegnate piano di servizio App tooan condividono tali risorse, consentendo di costo toosave quando si ospitano più applicazioni.
2. Creare un'app Web. È possibile l'uso hello [portale di Azure](/azure/app-service-web/web-sites-configure) o utilizzare hello successivo comando CLI Az:
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. Assicurarsi di impostare la configurazione di runtime Java hello necessari all'app. Hello comando CLI di Azure seguente configura hello web app toorun in una versione recente di Java 8 JDK e [Apache Tomcat](http://tomcat.apache.org/) 8.0.
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a>Consente di impostare il processo di Jenkins hello


1. Creare un nuovo progetto **freestyle** nel dashboard di Jenkins
2. Configurare **gestione del codice sorgente** toouse nel fork locale di [semplice Java Web App per Azure](https://github.com/azure-devops/javawebappsample) fornendo hello **URL del Repository**. Ad esempio: http://github.com/&lt;yourID>/javawebappsample.
3. Aggiungere un progetto di hello toobuild passaggio di compilazione Maven utilizzando. A tale scopo aggiungere un **Execute shell**. Per questo esempio, è necessario un file di *.war passaggio aggiuntivo toorename hello in tooROOT.war cartella di destinazione.   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. Aggiungere un'azione post-compilazione selezionando **Publish an Azure Web App** (Pubblica un'App Web di Azure).
5. Alimentatore, "mySp" hello Azure SPN archiviati al passaggio precedente.
6. In **configurazione delle App** , scegliere l'app web e il gruppo di risorse hello nella sottoscrizione. plug-in Hello rileva automaticamente se hello App Web è Windows o basata su Linux. Per un'App Web basati su Windows, viene visualizzata l'opzione hello "Pubblica file".
7. Inserire nel file hello desiderato toodeploy (ad esempio, un war pacchetto se si usa Java.) La directory di origine e quella di destinazione sono facoltative. i parametri di Hello consentono di cartelle di origine e destinazione toospecify durante il caricamento di file. L'app Web Java in Azure viene eseguita in un server Tomcat. Si carica il pacchetto war nella cartella webapps. Per questo esempio, impostare **Directory di origine** troppo "target" e specificare "webapps" **Directory di destinazione**.
8. Se si desidera toodeploy tooa slot diverso da produzione, è inoltre possibile impostare **Slot** nome.
9. Salvare il progetto hello e compilarlo. L'app web è distribuito tooAzure al completamento.

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a>Distribuire l'app Web tramite FTP usando la pipeline Jenkins

plug-in di Hello è pronto per pipeline. È possibile fare riferimento a esempio tooa nel repository GitHub hello.

1. Nell'interfaccia utente Web di GitHub aprire il file **Jenkinsfile_ftp_plugin**. Fare clic su hello matita icona tooedit il gruppo di risorse di file tooupdate hello e il nome dell'app web sulla riga 11 e 12 rispettivamente.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Modificare l'ID di riga tooupdate 14 credenziale nell'istanza di Jenkins.    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a>Creare una pipeline Jenkins

1. Aprire Jenkins in un Web browser, fare clic su **New Item**.
2. Specificare un nome per il processo di hello e selezionare **Pipeline**. Fare clic su **OK**.
3. Fare clic su hello **Pipeline** scheda accanto.
4. Per **Definition** selezionare **Pipeline script from SCM**.
5. Per **SCM** selezionare **Git**. Immettere hello GitHub URL per il repository con fork: https:&lt;repository di scenari > GIT
6. Aggiornamento **percorso dello Script** troppo "Jenkinsfile_ftp_plugin"
7. Fare clic su **salvare** e il processo di esecuzione hello.

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a>Configurare Jenkins toodeploy App Web in Linux con Docker

Oltre a Git o FTP, l'app Web in Linux supporta la distribuzione tramite Docker. toodeploy usando Docker, è necessario tooprovide un Dockerfile utilizzate dai pacchetti di app web con runtime del servizio in un'immagine di docker. Quindi plug-in hello Crea immagine hello, inserisce del Registro di sistema di tooa docker e distribuisce hello immagine tooyour web app.

Web App in Linux supporta anche modalità tradizionali come Git e FTP, ma solo per i linguaggi predefiniti come .NET Core, Node.js, PHP e Ruby. Per altre lingue, è necessario toopackage del runtime dell'applicazione di servizio e del codice insieme in un'immagine docker e usare docker toodeploy.

Prima di configurare il processo di hello in Jenkins, è necessario un servizio app di Azure in Linux. Un registro di sistema del contenitore è anche necessario toostore e gestire le immagini contenitore Docker private. È possibile usare DockerHub; per questo esempio viene usato Registro contenitori di Azure.

* È possibile seguire i passaggi di hello [qui](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate un'App Web in Linux 
* Registro di sistema di contenitore di Azure è un gestito [Docker Registro di sistema] (https://docs.docker.com/registry/) servizio basato su hello open source Docker del Registro di sistema 2.0. Procedura [qui] hello (/ azure/container-registry/container-registry-get-started-azure-cli) per maggiori informazioni su come toodo in modo. È anche possibile usare DockerHub.

### <a name="toodeploy-using-docker"></a>toodeploy usando docker:

1. Creare un nuovo progetto freestyle nel dashboard di Jenkins.
2. Configurare **gestione del codice sorgente** toouse nel fork locale di [semplice Java Web App per Azure](https://github.com/azure-devops/javawebappsample) fornendo hello **URL del Repository**. Ad esempio: http://github.com/&lt;yourID>/javawebappsample.
Aggiungere un progetto di hello toobuild passaggio di compilazione Maven utilizzando. A tale scopo, aggiungere un **eseguire shell** e aggiungere hello seguente riga **comando**:    
```bash
mvn clean package
```

3. Aggiungere un'azione post-compilazione selezionando **Publish an Azure Web App** (Pubblica un'App Web di Azure).
4. Fornire, **mySp**, entità servizio di Azure hello archiviati al passaggio precedente come credenziali di Azure.
5. In **configurazione delle App** , scegliere il gruppo di risorse di hello e un'app web di Linux nella sottoscrizione.
6. Scegliere Publish via Docker (Pubblica tramite Docker).
7. Compilare il percorso **Dockerfile**. È possibile mantenere predefinite hello "/ Dockerfile" per **Docker del Registro di sistema URL**, specificare il formato di hello https://&lt;myRegistry >. azurecr.io se si utilizza Azure contenitore Registro di sistema. Non specificare un valore se si usa DockerHub.
8. Per **le credenziali del Registro di sistema**, aggiungere la credenziale hello per hello del Registro di sistema contenitore di Azure. È possibile ottenere hello userid e password eseguendo hello seguenti comandi CLI di Azure. Hello primo comando Abilita account amministratore hello.    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. Hello nome immagine docker e tag in **avanzate** scheda sono facoltativi. Per impostazione predefinita, il nome di immagine viene ottenuto dall'immagine hello nome configurato nel tag Azure hello portale (nel contenitore Docker impostazione.) viene generato da $BUILD_NUMBER. Assicurarsi di specificare il nome di immagine hello in un portale di Azure o fornire un valore per **immagine Docker** in **avanzate** scheda. Per questo esempio, specificare "&lt;yourRegistry >.azurecr.io/calculator" per **immagine Docker** e lasciare vuoto il valore del **tag immagine Docker**.
10. Si noti che la distribuzione avrà esito negativo se si usa l'impostazione dell'immagine Docker predefinita. Assicurarsi di cambiare immagine personalizzata toouse configurazione di docker in base alle impostazioni contenitore Docker nel portale di Azure. Per immagine incorporata, utilizzare toodeploy approccio di caricamento file.
11. Approccio di caricamento toofile simile, è possibile scegliere un altro slot diverso da produzione.
12. Salvare e compilare il progetto hello. Viene visualizzata l'immagine del contenitore viene inserito tooyour del Registro di sistema e app web viene distribuito.

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a>Distribuire App in Linux tramite Docker tramite la pipeline di Jenkins tooWeb

1. Nell'interfaccia utente Web di GitHub aprire il file **Jenkinsfile_container_plugin**. Fare clic su hello matita icona tooedit il gruppo di risorse di file tooupdate hello e il nome dell'app web sulla riga 11 e 12 rispettivamente.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Modifica riga 13 tooyour contenitore del Registro di sistema server    
```java
def registryServer = '<registryURL>'
```    

3. Modificare l'ID di riga tooupdate 16 credenziale nell'istanza di Jenkins    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a>Creare una pipeline Jenkins    

1. Aprire Jenkins in un Web browser, fare clic su **New Item**.
2. Specificare un nome per il processo di hello e selezionare **Pipeline**. Fare clic su **OK**.
3. Fare clic su hello **Pipeline** scheda accanto.
4. Per **Definition** selezionare **Pipeline script from SCM**.
5. Per **SCM** selezionare **Git**.
6. Immettere hello GitHub URL per il repository con fork: https:&lt;repository di scenari > GIT</li>
Aggiornamento 7, **percorso dello Script** troppo "Jenkinsfile_container_plugin"
8. Fare clic su **salvare** e il processo di esecuzione hello.

## <a name="verify-your-web-app"></a>Verificare l'app Web

1. file WAR di hello tooverify venga distribuito correttamente tooyour web app. Aprire un Web browser.
2. Passare toohttp: / /&lt;nome_app >.azurewebsites.net/api/calculator/ping visualizzati:    
     Benvenuto tooJava App Web. indicante che l'aggiornamento è stato eseguito.
   Sun Jun 17 16:39:10 UTC 2017
3. Passare toohttp: / /&lt;nome_app >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (sostituire &lt;x > e &lt;y > con tutti i numeri) somma hello tooget di x e y        
    ![Calcolatrice: aggiungi](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a>Per il servizio app in Linux

* tooverify CLI di Azure, eseguire:

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    Si otterrà hello seguente risultato:
    
    ```
    [
    "calculator"
    ]
    ```
    
    Passare toohttp: / /&lt;nome_app >.azurewebsites.net/api/calculator/ping. Viene visualizzato il messaggio hello: 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    Passare toohttp: / /&lt;nome_app >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (sostituire &lt;x > e &lt;y > con tutti i numeri) somma hello tooget di x e y
    
## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, si utilizza tooAzure toodeploy plug-in di hello Azure App Service.

Si è appreso come:

> [!div class="checklist"]
> * Configurare Jenkins toodeploy servizio App di Azure tramite FTP 
> * Configurare Jenkins toodeploy tooAzure servizio App in Linux con Docker 
