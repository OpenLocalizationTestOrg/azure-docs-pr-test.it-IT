---
title: aaaBuild un'app web Java e MySQL in Azure
description: Informazioni su come tooget un'applicazione Java che consente la connessione del servizio di database MySQL Azure toohello utilizzo di servizio app di Azure.
services: app-service\web
documentationcenter: Java
author: bbenz
manager: jeffsand
editor: jasonwhowell
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: tutorial
ms.date: 05/22/2017
ms.author: bbenz
ms.custom: mvc
ms.openlocfilehash: 0820ee9c2b7bf8fcaa22287c27a7ab848a1c4927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a>Creare un'app Web Java e MySQL in Azure

Questa esercitazione viene illustrato come un linguaggio toocreate web app in Azure e connetterla database MySQL tooa. Al termine, verrà creata un'applicazione [Spring Boot](https://projects.spring.io/spring-boot/) che archivia i dati in [Database di Azure per MySQL](https://docs.microsoft.com/azure/mysql/overview) in esecuzione in [App Web del servizio app di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

![App Java in esecuzione nel Servizio app di Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare un database MySQL in Azure
> * La connessione a un database di esempio app toohello
> * Distribuire hello app tooAzure
> * Aggiornare e ridistribuire l'applicazione hello
> * Eseguire lo streaming dei log di diagnostica in Azure
> * Monitoraggio dell'app hello in hello portale di Azure


## <a name="prerequisites"></a>Prerequisiti

1. [Scaricare e installare Git](https://git-scm.com/)
1. [Scaricare e installare hello Java JDK 7 o versione successiva](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [Scaricare, installare e avviare MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-local-mysql"></a>Preparare MySQL in locale 

In questo passaggio si crea un database in un server MySQL locale da usare nell'app hello test in locale nel computer.

### <a name="connect-toomysql-server"></a>Connessione server tooMySQL

In una finestra terminale, connettersi tooyour locale MySQL server. In questa esercitazione, è possibile utilizzare questa finestra terminale di toorun tutti i comandi di hello.

```bash
mysql -u root -p
```

Se viene chiesto di immettere una password, immettere la password di hello per hello `root` account. Se non si ricorda la password dell'account radice, vedere [MySQL: modalità tooReset hello Password Root](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).

Se il comando viene eseguito correttamente, il server MySQL è già in esecuzione. In caso contrario, assicurarsi che il server MySQL locale viene eseguito da hello seguente [passaggi successivi all'installazione di MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).

### <a name="create-a-database"></a>Creare un database 

In hello `mysql` richiedono, creare un database e una tabella per hello attività da svolgere.

```sql
CREATE DATABASE tododb;
```

Chiudere la connessione al server digitando `quit`.

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a>Creare ed eseguire app di esempio hello 

In questo passaggio, clonare app di esempio Spring avvio, configurarlo come database di MySQL locale toouse hello ed eseguirlo nel computer in uso. 

### <a name="clone-hello-sample"></a>Esempio hello clone

Nella finestra terminal hello passare tooa repository di esempio hello clone e di directory di lavoro. 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a>Configurare il database MySQL hello di hello app toouse

Hello aggiornamento `spring.datasource.password` e un valore nel *spring-boot-mysql-todo/src/main/resources/application.properties* con hello stessa password radice utilizzato prompt dei comandi di tooopen hello MySQL:

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a>Compilare ed eseguire l'esempio hello

Compilare ed eseguire l'esempio hello usare wrapper di Maven hello incluso nel repository di hello:

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

Aprire il toosee toohttp://localhost:8080 browser nell'esempio hello in azione. Quando si aggiunta toohello elenco delle attività, utilizzare i comandi SQL seguente in hello MySQL dati hello tooview prompt archiviati in MySQL hello.

```SQL
use testdb;
select * from todo_item;
```

Arrestare l'applicazione hello premendo `Ctrl` + `C` in hello terminal. 

## <a name="create-an-azure-mysql-database"></a>Creare un database MySQL di Azure

In questo passaggio si crea un [Database di Azure per MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) istanza utilizzando hello [CLI di Azure](https://docs.microsoft.com/cli/azure/install-azure-cli). Configurare toouse applicazione di esempio hello questo database in un secondo momento nell'esercitazione hello.

Hello utilizzare Azure CLI 2.0 nelle risorse di hello toocreate finestra terminale necessaria toohost applicazione Java nel servizio app di Azure. Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando e seguire hello le direzioni. 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) con hello [gruppo az creare](/cli/azure/group#create) comando. Un gruppo di risorse di Azure è un contenitore logico in cui vengono distribuite e gestite le risorse correlate, ad esempio app Web, database e account di archiviazione. 

Hello esempio seguente viene creato un gruppo di risorse nell'area Europa settentrionale hello:

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

toosee hello i valori possibili utilizzabili per `--location`, utilizzare hello [az appservice elenco posizioni](/cli/azure/appservice#list-locations) comando.

### <a name="create-a-mysql-server"></a>Creare un server MySQL

Creare un server nel Database di Azure per MySQL (anteprima) con hello [creare server mysql az](/cli/azure/mysql/server#create) comando.    
Sostituire con il proprio nome di server MySQL univoco in cui si vedere hello `<mysql_server_name>` segnaposto. Questo nome fa parte del nome host del server MySQL, `<mysql_server_name>.mysql.database.azure.com`, pertanto è necessario toobe univoco globale. Sostituire anche `<admin_user>` e `<admin_password>` con i valori desiderati.

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

Creazione di server MySQL hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:

```json
{
  "administratorLogin": "admin_user",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mysql_server_name.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/mysql_server_name",
  "location": "northeurope",
  "name": "mysql_server_name",
  "resourceGroup": "mysqlJavaResourceGroup",
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a>Configurare il firewall del server

Creare una regola del firewall per il client di MySQL server tooallow connessioni tramite hello [az mysql regola firewall del server-creare](/cli/azure/mysql/server/firewall-rule#create) comando. 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> Database di Azure per MySQL (anteprima) per il momento non consente di abilitare automaticamente le connessioni dai servizi di Azure. Come vengono assegnati dinamicamente agli indirizzi IP in Azure, è preferibile tooenable tutti gli indirizzi IP per ora. Poiché il servizio di hello continua l'anteprima, verranno attivati metodi migliori per la protezione del database.

## <a name="configure-hello-azure-mysql-database"></a>Configurare il database MySQL Azure hello

Nella finestra terminal hello nel computer in uso, è possibile connettersi toohello MySQL server in Azure. Utilizzare il valore di hello specificato in precedenza per `<admin_user>` e `<mysql_server_name>`.

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a>Creare un database 

In hello `mysql` richiedono, creare un database e una tabella per hello attività da svolgere.

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a>Creare un utente con autorizzazioni

Creare un utente del database e assegnare tutti i privilegi in hello `tododb` database. Sostituire i segnaposto hello `<Javaapp_user>` e `<Javaapp_password>` con il proprio nome applicazione univoco.

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

Chiudere la connessione al server digitando `quit`.

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a>Distribuire tooAzure esempio hello servizio App

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

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a>Configurare il database SQL di Azure hello di hello app toouse

Prima di eseguire l'applicazione di esempio hello, impostare le impostazioni dell'applicazione hello web app toouse hello Azure MySQL database creato in Azure. Queste proprietà vengono esposte toohello di applicazione web come variabili di ambiente ed eseguire l'override di valori hello impostati in application.properties hello all'interno di app in pacchetto web hello. 

Set di impostazioni dell'applicazione utilizzando [az webapp configurazione appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in hello CLI:

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL="jdbc:mysql://<mysql_server_name>.mysql.database.azure.com:3306/tododb?verifyServerCertificate=true&useSSL=true&requireSSL=false" \
    --resource-group myResourceGroup \
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_USERNAME=Javaapp_user@mysql_server_name  \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL=Javaapp_password \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

### <a name="get-ftp-deployment-credentials"></a>Ottenere le credenziali di distribuzione FTP 
È possibile distribuire il servizio App tooAzure applicazione in vari modi, tra cui FTP, Git locale, GitHub, il Visual Studio Team Services e BitBucket. Per questo esempio, hello toodeploy FTP. File WAR compilato in precedenza in del servizio App di tooAzure computer locale.

toodetermine quali credenziali toopass lungo in un toohello comando ftp App Web, utilizzare [az servizio App web di distribuzione elenco-pubblicazione-profili](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) comando: 

```azurecli-interactive
az webapp deployment list-publishing-profiles \ 
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" \ 
    --output json
```

```JSON
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-069.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "app_name\\$app_name"
  }
]
```

### <a name="upload-hello-app-using-ftp"></a>Caricare l'applicazione hello tramite FTP

Utilizzare i Preferiti hello di toodeploy strumento FTP. Toohello file WAR */site/wwwroot/webapps* cartella indirizzo server hello prelevati hello `URL` campo nel comando precedente hello. Rimuovere la directory di applicazione hello esistente predefinito (radice) e sostituire hello esistente ROOT.war con hello. File WAR incorporato hello in precedenza nell'esercitazione hello.

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected toowaws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-hello-web-app"></a>Test hello web app

Sfoglia troppo`http://<app_name>.azurewebsites.net/` e aggiungere alcune attività toohello elenco. 

![App Java in esecuzione nel Servizio app di Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

**Congratulazioni.** L'app Java basata su dati è in esecuzione in Servizio app di Azure.

## <a name="update-hello-app-and-redeploy"></a>Ridistribuzione e l'applicazione hello aggiornamento

Aggiornare tooinclude applicazione hello un'altra colonna nell'elenco di attività hello per selezionare l'elemento hello giorno è stato creato. Avvio Spring gestisce l'aggiornamento dello schema del database hello automaticamente come hello le modifiche al modello di dati senza modificare i record del database esistente.

1. Nel sistema locale, aprire *src/main/java/com/example/fabrikam/TodoItem.java* e aggiungere il seguente hello Importa toohello classe:   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. Aggiungere un `String` proprietà `timeCreated` troppo*src/main/java/com/example/fabrikam/TodoItem.java*, inizializzandola con un timestamp al momento della creazione di oggetti. Aggiungere getter/setter per hello nuovo `timeCreated` proprietà durante la modifica di questo file.

    ```java
    private String name;
    private boolean complete;
    private String timeCreated;
    ...

    public TodoItem(String category, String name) {
       this.category = category;
       this.name = name;
       this.complete = false;
       this.timeCreated = new SimpleDateFormat("MMMM dd, YYYY").format(Calendar.getInstance().getTime());
    }
    ...
    public void setTimeCreated(String timeCreated) {
       this.timeCreated = timeCreated;
    }

    public String getTimeCreated() {
        return timeCreated;
    }
    ```

3. Aggiornamento *src/main/java/com/example/fabrikam/TodoDemoController.java* con una riga hello `updateTodo` metodo tooset hello timestamp:

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. Aggiungere il supporto per il nuovo campo di hello nel modello Thymeleaf hello. Aggiornamento *src/main/resources/templates/index.html* con una nuova intestazione di tabella per hello timestamp e il nuovo campo toodisplay hello valore timestamp hello in ogni riga di dati della tabella.

    ```html
    <th>Name</th>
    <th>Category</th>
    <th>Time Created</th>
    <th>Complete</th>
    ...
    <td th:text="${item.category}">item_category</td><input type="hidden" th:field="*{todoList[__${i.index}__].category}"/>
    <td th:text="${item.timeCreated}">item_time_created</td><input type="hidden" th:field="*{todoList[__${i.index}__].timeCreated}"/>
    <td><input type="checkbox" th:checked="${item.complete} == true" th:field="*{todoList[__${i.index}__].complete}"/></td>
    ```

5. Ricompilare l'applicazione hello:

    ```bash
    mvnw clean package 
    ```

6. FTP hello aggiornato. WAR come prima, la rimozione di hello esistente */wwwroot del sito/ROOT WebApp* directory e *ROOT.war*, quindi caricare hello aggiornato. File WAR come ROOT.war. 

Quando si aggiorna l'applicazione hello, un **ora di creazione** colonna è ora visibile. Quando si aggiunge una nuova attività, hello app verrà popolato automaticamente hello timestamp. Le attività esistenti rimangono invariati e possono essere utilizzati con l'applicazione hello anche se hello modello di dati sottostante è stata modificata. 

![App Java aggiornata con una nuova colonna](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a>Eseguire lo streaming dei log di diagnostica 

Mentre l'applicazione Java in esecuzione in Azure App Service, è possibile ottenere console hello log inviati tramite pipe direttamente tooyour terminal. In questo modo, è possibile ottenere hello stessi messaggi di diagnostica toohelp si esegue il debug di errori dell'applicazione.

log toostart streaming, usare hello [della parte finale del log di az webapp](/cli/azure/appservice/web/log#tail) comando.

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a>Gestire l'app Web di Azure

Passare toohello toosee portale Azure hello app web che è stato creato.

toodo, accedi troppo[https://portal.azure.com](https://portal.azure.com).

Scegliere dal menu a sinistra hello **servizio App**, quindi fare clic su nome hello dell'app web di Azure.

![Spostamento del portale tooAzure web app](./media/app-service-web-tutorial-java-mysql/access-portal.png)

Per impostazione predefinita, il pannello dell'app web illustra hello **Panoramica** pagina. che offre una visualizzazione dello stato dell'app. In questa pagina è anche possibile eseguire attività di gestione come arrestare, avviare, riavviare ed eliminare. le schede di Hello sul lato sinistro di hello del pannello hello mostrano è possibile aprire le pagine di configurazione diverso hello.

![Pannello del servizio app nel portale di Azure](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

Queste schede nel pannello hello mostrano hello numerose funzionalità è possibile aggiungere tooyour web app. Hello elenco seguente offre solo alcune delle possibilità hello:
* Eseguire il mapping di un nome DNS personalizzato
* Associare un certificato SSL personalizzato
* Configurare la distribuzione continua
* Aumentare le prestazioni e il numero di istanze
* Aggiungere l'autenticazione utente

## <a name="clean-up-resources"></a>Pulire le risorse

Se non è necessario queste risorse per un'altra esercitazione (vedere [passaggi successivi](#next)), è possibile eliminarle eseguendo hello comando seguente: 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a>Passaggi successivi

> [!div class="checklist"]
> * Creare un database MySQL in Azure
> * Connettersi a un toohello di app di esempio Java MySQL
> * Distribuire hello app tooAzure
> * Aggiornare e ridistribuire l'applicazione hello
> * Eseguire lo streaming dei log di diagnostica in Azure
> * Gestire app hello in hello portale di Azure

Spostare toolearn esercitazione successiva toohello come assegnare un nome app toohello toomap un DNS personalizzato.

> [!div class="nextstepaction"] 
> [Eseguire il mapping di un esistente personalizzato DNS nome tooAzure App Web](app-service-web-tutorial-custom-domain.md)
