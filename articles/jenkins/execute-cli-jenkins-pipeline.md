---
title: hello aaaExecute CLI di Azure con Jenkins | Documenti Microsoft
description: Informazioni su come toouse CLI di Azure toodeploy un Java web app tooAzure nella Pipeline di Jenkins
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: jenkins
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 4bd1e12e6de1f010453ff51c835f84e7361962f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a>Distribuire il servizio App con Jenkins tooAzure e hello CLI di Azure
toodeploy un tooAzure di app web Java, è possibile utilizzare l'interfaccia CLI di Azure in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/). In questa esercitazione viene creata una pipeline CI/CD in una macchina virtuale di Azure e viene illustrato come:

> [!div class="checklist"]
> * Creare una macchina virtuale Jenkins
> * Configurare Jenkins
> * Creare un'app Web in Azure
> * Preparare un repository GitHub
> * Creare una pipeline Jenkins
> * Eseguire la pipeline hello e verificare hello web app

Questa esercitazione richiede hello Azure CLI versione 2.0.4 o versioni successive. versione di hello toofind, eseguire `az --version`. Se è necessario tooupgrade, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a>Creare e configurare un'istanza di Jenkins
Se si dispone già di un master Jenkins, iniziare con hello [modello di soluzione](install-jenkins-solution-template.md), che include hello necessario [le credenziali di Azure](https://plugins.jenkins.io/azure-credentials) plug-in per impostazione predefinita. 

plug-in credenziali di Azure Hello consente credenziali dell'entità servizio di Microsoft Azure toostore Jenkins. Nella versione 1.2, viene aggiunto il supporto di hello pertanto Jenkins Pipeline ottenere hello le credenziali di Azure. 

Assicurarsi di disporre della versione 1.2 o versioni successive:
* Nel dashboard di Jenkins hello, fare clic su **Jenkins Gestisci -> Gestione plug-in ->** e cercare **credenziali di Azure**. 
* Aggiornare i plug-in hello se hello versione è precedente a 1.2.

Java JDK e Maven sono inoltre necessari nel database master di Jenkins hello. tooinstall, di log nel database master tooJenkins tramite SSH ed eseguire hello seguenti comandi:
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a>Aggiungere credenziali tooJenkins dell'entità servizio di Azure

Una credenziale di Azure è necessario tooexecute CLI di Azure.

* Nel dashboard di Jenkins hello, fare clic su **credenziali -> sistema ->**. Fare clic su **Global credentials(unrestricted)**.
* Fare clic su **Aggiungi credenziali** tooadd un [dell'entità servizio di Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) compilando hello ID sottoscrizione, l'ID Client, segreto Client ed Endpoint Token OAuth 2.0. Indicare un ID per l'uso nel passaggio successivo.

![Add Credentials](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a>Creare un servizio App di Azure per la distribuzione di app web Java di hello

Creare un piano di servizio App di Azure con hello **libero** tariffario utilizzando hello [crea piano di servizio App az](/cli/azure/appservice/plan#create) comando CLI. piano di servizio App Hello definisce hello risorse fisiche utilizzate toohost app. Tutte le applicazioni assegnate piano di servizio App tooan condividono tali risorse, consentendo di costo toosave quando si ospitano più applicazioni. 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

Quando il piano di hello è pronto, hello che CLI di Azure viene illustrato simile output toohello di esempio seguente:

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a>Creare un'app Web di Azure

 Hello utilizzare [az webapp creare](/cli/azure/appservice/web#create) toocreate comando CLI una definizione di applicazione web in hello `myAppServicePlan` piano di servizio App. definizione dell'app web Hello fornisce un tooaccess URL all'applicazione e consente di configurare diverse opzioni toodeploy tooAzure il codice. 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

Hello Substitute `<app_name>` segnaposto con il proprio nome applicazione univoco. Questo nome univoco fa parte del nome di dominio hello predefinito per l'app web hello, quindi nome hello deve toobe univoco tra tutte le App in Azure. È possibile eseguire il mapping di un'app web di toohello voce di nome di dominio personalizzato prima di esporre tooyour utenti.

Quando la definizione di applicazione web hello è pronta, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente: 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a>Configurare Java 

Impostare la configurazione di runtime Java hello necessari all'app con hello [aggiornamento configurazione web di az appservice](/cli/azure/appservice/web/config#update) comando.

Hello comando seguente consente di configurare hello web app toorun in una versione recente di Java 8 JDK e [Apache Tomcat](http://tomcat.apache.org/) 8.0.

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a>Preparare un repository GitHub
Aprire hello [semplice Java Web App per Azure](https://github.com/azure-devops/javawebappsample) repository. toofork hello repository tooyour proprietari di account GitHub, fare clic su hello **Fork** pulsante nell'angolo superiore destro di hello.

* Nell'interfaccia utente Web di GitHub, aprire il file **Jenkinsfile**. Fare clic su hello matita icona tooedit il gruppo di risorse di file tooupdate hello e il nome dell'app web nella riga 20 e 21 rispettivamente.

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* Modificare l'ID di riga tooupdate 23 credenziale nell'istanza di Jenkins

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a>Creare una pipeline Jenkins
Aprire Jenkins in un Web browser, fare clic su **New Item**. 

* Specificare un nome per il processo di hello e selezionare **Pipeline**. Fare clic su **OK**.
* Fare clic su hello **Pipeline** scheda accanto. 
* Per **Definition** selezionare **Pipeline script from SCM**.
* Per **SCM** selezionare **Git**.
* Immettere hello GitHub URL per il repository con fork: https:\<repository di scenari\>GIT
* Fare clic su **Save**

## <a name="test-your-pipeline"></a>Testare la pipeline
* Pipeline toohello è stato creato, quindi scegliere **compilare ora**
* Una build dovrebbe avere esito positivo in pochi secondi, ed è possibile passare toohello compilazione e fare clic su **Output di Console** dettagli hello toosee

## <a name="verify-your-web-app"></a>Verificare l'app Web
file WAR di hello tooverify venga distribuito correttamente tooyour web app. Aprire un Web browser:

* Passare toohttp: / /&lt;nome_app >.azurewebsites.net/api/calculator/ping  
Verranno visualizzati:

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* Passare toohttp: / /&lt;nome_app >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (sostituire &lt;x > e &lt;y > con tutti i numeri) somma hello tooget di x e y

![Calcolatrice: aggiungi](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a>Distribuire tooAzure App Web in Linux
Ora che si conosce la modalità di pipeline toouse CLI di Azure nel Jenkins, è possibile modificare hello script toodeploy tooan App Web di Azure in Linux.

Web App in Linux supporta una distribuzione di hello toodo modo diverso, ovvero toouse Docker. toodeploy, è necessario tooprovide un Dockerfile utilizzate dai pacchetti di app web con runtime del servizio in un'immagine di Docker. plug-in Hello verrà quindi compilato immagine hello, spingerla del Registro di sistema di tooa Docker e distribuito hello immagine tooyour web app.

* Seguire i passaggi di hello [qui](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate un'App Web di Azure in esecuzione in Linux.
* Installare Docker sull'istanza Jenkins seguendo le istruzioni di hello in questo [articolo](https://docs.docker.com/engine/installation/linux/ubuntu/).
* Creare un contenitore del Registro di sistema nel portale di Azure hello attenendosi alla procedura hello [qui](/azure/container-registry/container-registry-get-started-azure-cli).
* In hello stesso [semplice Java Web App per Azure](https://github.com/azure-devops/javawebappsample) repository è duplicato, modificare hello **Jenkinsfile2** file:
    * Riga 18-21, aggiornare i nomi di toohello del gruppo di risorse e app web, ACR rispettivamente. 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * Riga 24, aggiornamento \<azsrvprincipal\> ID delle credenziali tooyour
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* Creare una nuova pipeline di Jenkins seguendo durante la distribuzione in Windows, solo questa volta, utilizzare l'app web tooAzure **Jenkinsfile2** invece.
* Eseguire il nuovo processo.
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
In questa esercitazione, è configurata una pipeline di Jenkins che consente di estrarre il codice sorgente hello nel repository GitHub. Esecuzione di un file war toobuild Maven e quindi utilizza tooAzure toodeploy CLI di Azure App Service. Si è appreso come:

> [!div class="checklist"]
> * Creare una macchina virtuale Jenkins
> * Configurare Jenkins
> * Creare un'app Web in Azure
> * Preparare un repository GitHub
> * Creare una pipeline Jenkins
> * Eseguire la pipeline hello e verificare hello web app
