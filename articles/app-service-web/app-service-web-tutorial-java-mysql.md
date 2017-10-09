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
# <a name="build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="115e6-103">Creare un'app Web Java e MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="115e6-103">Build a Java and MySQL web app in Azure</span></span>

<span data-ttu-id="115e6-104">Questa esercitazione viene illustrato come un linguaggio toocreate web app in Azure e connetterla database MySQL tooa.</span><span class="sxs-lookup"><span data-stu-id="115e6-104">This tutorial shows you how toocreate a Java web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="115e6-105">Al termine, verrà creata un'applicazione [Spring Boot](https://projects.spring.io/spring-boot/) che archivia i dati in [Database di Azure per MySQL](https://docs.microsoft.com/azure/mysql/overview) in esecuzione in [App Web del servizio app di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span><span class="sxs-lookup"><span data-stu-id="115e6-105">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span></span>

![App Java in esecuzione nel Servizio app di Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="115e6-107">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="115e6-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="115e6-108">Creare un database MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="115e6-108">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="115e6-109">La connessione a un database di esempio app toohello</span><span class="sxs-lookup"><span data-stu-id="115e6-109">Connect a sample app toohello database</span></span>
> * <span data-ttu-id="115e6-110">Distribuire hello app tooAzure</span><span class="sxs-lookup"><span data-stu-id="115e6-110">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="115e6-111">Aggiornare e ridistribuire l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="115e6-111">Update and redeploy hello app</span></span>
> * <span data-ttu-id="115e6-112">Eseguire lo streaming dei log di diagnostica in Azure</span><span class="sxs-lookup"><span data-stu-id="115e6-112">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="115e6-113">Monitoraggio dell'app hello in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="115e6-113">Monitor hello app in hello Azure portal</span></span>


## <a name="prerequisites"></a><span data-ttu-id="115e6-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="115e6-114">Prerequisites</span></span>

1. [<span data-ttu-id="115e6-115">Scaricare e installare Git</span><span class="sxs-lookup"><span data-stu-id="115e6-115">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="115e6-116">Scaricare e installare hello Java JDK 7 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="115e6-116">Download and install hello Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [<span data-ttu-id="115e6-117">Scaricare, installare e avviare MySQL</span><span class="sxs-lookup"><span data-stu-id="115e6-117">Download, install, and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="115e6-118">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="115e6-118">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="115e6-119">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="115e6-119">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="115e6-120">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="115e6-120">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-local-mysql"></a><span data-ttu-id="115e6-121">Preparare MySQL in locale</span><span class="sxs-lookup"><span data-stu-id="115e6-121">Prepare local MySQL</span></span> 

<span data-ttu-id="115e6-122">In questo passaggio si crea un database in un server MySQL locale da usare nell'app hello test in locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="115e6-122">In this step, you create a database in a local MySQL server for use in testing hello app locally on your machine.</span></span>

### <a name="connect-toomysql-server"></a><span data-ttu-id="115e6-123">Connessione server tooMySQL</span><span class="sxs-lookup"><span data-stu-id="115e6-123">Connect tooMySQL server</span></span>

<span data-ttu-id="115e6-124">In una finestra terminale, connettersi tooyour locale MySQL server.</span><span class="sxs-lookup"><span data-stu-id="115e6-124">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="115e6-125">In questa esercitazione, è possibile utilizzare questa finestra terminale di toorun tutti i comandi di hello.</span><span class="sxs-lookup"><span data-stu-id="115e6-125">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="115e6-126">Se viene chiesto di immettere una password, immettere la password di hello per hello `root` account.</span><span class="sxs-lookup"><span data-stu-id="115e6-126">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="115e6-127">Se non si ricorda la password dell'account radice, vedere [MySQL: modalità tooReset hello Password Root](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="115e6-127">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="115e6-128">Se il comando viene eseguito correttamente, il server MySQL è già in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="115e6-128">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="115e6-129">In caso contrario, assicurarsi che il server MySQL locale viene eseguito da hello seguente [passaggi successivi all'installazione di MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="115e6-129">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="115e6-130">Creare un database</span><span class="sxs-lookup"><span data-stu-id="115e6-130">Create a database</span></span> 

<span data-ttu-id="115e6-131">In hello `mysql` richiedono, creare un database e una tabella per hello attività da svolgere.</span><span class="sxs-lookup"><span data-stu-id="115e6-131">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="115e6-132">Chiudere la connessione al server digitando `quit`.</span><span class="sxs-lookup"><span data-stu-id="115e6-132">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a><span data-ttu-id="115e6-133">Creare ed eseguire app di esempio hello</span><span class="sxs-lookup"><span data-stu-id="115e6-133">Create and run hello sample app</span></span> 

<span data-ttu-id="115e6-134">In questo passaggio, clonare app di esempio Spring avvio, configurarlo come database di MySQL locale toouse hello ed eseguirlo nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="115e6-134">In this step, you clone sample Spring boot app, configure it toouse hello local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="115e6-135">Esempio hello clone</span><span class="sxs-lookup"><span data-stu-id="115e6-135">Clone hello sample</span></span>

<span data-ttu-id="115e6-136">Nella finestra terminal hello passare tooa repository di esempio hello clone e di directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="115e6-136">In hello terminal window, navigate tooa working directory and clone hello sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a><span data-ttu-id="115e6-137">Configurare il database MySQL hello di hello app toouse</span><span class="sxs-lookup"><span data-stu-id="115e6-137">Configure hello app toouse hello MySQL database</span></span>

<span data-ttu-id="115e6-138">Hello aggiornamento `spring.datasource.password` e un valore nel *spring-boot-mysql-todo/src/main/resources/application.properties* con hello stessa password radice utilizzato prompt dei comandi di tooopen hello MySQL:</span><span class="sxs-lookup"><span data-stu-id="115e6-138">Update hello `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with hello same root password used tooopen hello MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a><span data-ttu-id="115e6-139">Compilare ed eseguire l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="115e6-139">Build and run hello sample</span></span>

<span data-ttu-id="115e6-140">Compilare ed eseguire l'esempio hello usare wrapper di Maven hello incluso nel repository di hello:</span><span class="sxs-lookup"><span data-stu-id="115e6-140">Build and run hello sample using hello Maven wrapper included in hello repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="115e6-141">Aprire il toosee toohttp://localhost:8080 browser nell'esempio hello in azione.</span><span class="sxs-lookup"><span data-stu-id="115e6-141">Open your browser toohttp://localhost:8080 toosee in hello sample in action.</span></span> <span data-ttu-id="115e6-142">Quando si aggiunta toohello elenco delle attività, utilizzare i comandi SQL seguente in hello MySQL dati hello tooview prompt archiviati in MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="115e6-142">As you add tasks toohello list,  use hello following SQL commands in hello MySQL prompt tooview hello data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="115e6-143">Arrestare l'applicazione hello premendo `Ctrl` + `C` in hello terminal.</span><span class="sxs-lookup"><span data-stu-id="115e6-143">Stop hello application by hitting `Ctrl`+`C` in hello terminal.</span></span> 

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="115e6-144">Creare un database MySQL di Azure</span><span class="sxs-lookup"><span data-stu-id="115e6-144">Create an Azure MySQL database</span></span>

<span data-ttu-id="115e6-145">In questo passaggio si crea un [Database di Azure per MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) istanza utilizzando hello [CLI di Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="115e6-145">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using hello [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="115e6-146">Configurare toouse applicazione di esempio hello questo database in un secondo momento nell'esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="115e6-146">You configure hello sample application toouse this database later on in hello tutorial.</span></span>

<span data-ttu-id="115e6-147">Hello utilizzare Azure CLI 2.0 nelle risorse di hello toocreate finestra terminale necessaria toohost applicazione Java nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="115e6-147">Use hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost your Java application in Azure appservice.</span></span> <span data-ttu-id="115e6-148">Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando e seguire hello le direzioni.</span><span class="sxs-lookup"><span data-stu-id="115e6-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="115e6-149">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="115e6-149">Create a resource group</span></span>

<span data-ttu-id="115e6-150">Creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="115e6-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="115e6-151">Un gruppo di risorse di Azure è un contenitore logico in cui vengono distribuite e gestite le risorse correlate, ad esempio app Web, database e account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="115e6-151">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="115e6-152">Hello esempio seguente viene creato un gruppo di risorse nell'area Europa settentrionale hello:</span><span class="sxs-lookup"><span data-stu-id="115e6-152">hello following example creates a resource group in hello North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="115e6-153">toosee hello i valori possibili utilizzabili per `--location`, utilizzare hello [az appservice elenco posizioni](/cli/azure/appservice#list-locations) comando.</span><span class="sxs-lookup"><span data-stu-id="115e6-153">toosee hello possible values you can use for `--location`, use hello [az appservice list-locations](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="115e6-154">Creare un server MySQL</span><span class="sxs-lookup"><span data-stu-id="115e6-154">Create a MySQL server</span></span>

<span data-ttu-id="115e6-155">Creare un server nel Database di Azure per MySQL (anteprima) con hello [creare server mysql az](/cli/azure/mysql/server#create) comando.</span><span class="sxs-lookup"><span data-stu-id="115e6-155">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>    
<span data-ttu-id="115e6-156">Sostituire con il proprio nome di server MySQL univoco in cui si vedere hello `<mysql_server_name>` segnaposto.</span><span class="sxs-lookup"><span data-stu-id="115e6-156">Substitute your own unique MySQL server name where you see hello `<mysql_server_name>` placeholder.</span></span> <span data-ttu-id="115e6-157">Questo nome fa parte del nome host del server MySQL, `<mysql_server_name>.mysql.database.azure.com`, pertanto è necessario toobe univoco globale.</span><span class="sxs-lookup"><span data-stu-id="115e6-157">This name is part of your MySQL server's hostname, `<mysql_server_name>.mysql.database.azure.com`, so it needs toobe globally unique.</span></span> <span data-ttu-id="115e6-158">Sostituire anche `<admin_user>` e `<admin_password>` con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="115e6-158">Also substitute `<admin_user>` and `<admin_password>` with your own values.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

<span data-ttu-id="115e6-159">Creazione di server MySQL hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="115e6-159">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="115e6-160">Configurare il firewall del server</span><span class="sxs-lookup"><span data-stu-id="115e6-160">Configure server firewall</span></span>

<span data-ttu-id="115e6-161">Creare una regola del firewall per il client di MySQL server tooallow connessioni tramite hello [az mysql regola firewall del server-creare](/cli/azure/mysql/server/firewall-rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="115e6-161">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="115e6-162">Database di Azure per MySQL (anteprima) per il momento non consente di abilitare automaticamente le connessioni dai servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="115e6-162">Azure Database for MySQL (Preview) does not currently automatically enable connections from Azure services.</span></span> <span data-ttu-id="115e6-163">Come vengono assegnati dinamicamente agli indirizzi IP in Azure, è preferibile tooenable tutti gli indirizzi IP per ora.</span><span class="sxs-lookup"><span data-stu-id="115e6-163">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses for now.</span></span> <span data-ttu-id="115e6-164">Poiché il servizio di hello continua l'anteprima, verranno attivati metodi migliori per la protezione del database.</span><span class="sxs-lookup"><span data-stu-id="115e6-164">As hello service continues its preview, better methods for securing your database will be enabled.</span></span>

## <a name="configure-hello-azure-mysql-database"></a><span data-ttu-id="115e6-165">Configurare il database MySQL Azure hello</span><span class="sxs-lookup"><span data-stu-id="115e6-165">Configure hello Azure MySQL database</span></span>

<span data-ttu-id="115e6-166">Nella finestra terminal hello nel computer in uso, è possibile connettersi toohello MySQL server in Azure.</span><span class="sxs-lookup"><span data-stu-id="115e6-166">In hello terminal window on your computer, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="115e6-167">Utilizzare il valore di hello specificato in precedenza per `<admin_user>` e `<mysql_server_name>`.</span><span class="sxs-lookup"><span data-stu-id="115e6-167">Use hello value you specified previously for `<admin_user>` and `<mysql_server_name>`.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="115e6-168">Creare un database</span><span class="sxs-lookup"><span data-stu-id="115e6-168">Create a database</span></span> 

<span data-ttu-id="115e6-169">In hello `mysql` richiedono, creare un database e una tabella per hello attività da svolgere.</span><span class="sxs-lookup"><span data-stu-id="115e6-169">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="115e6-170">Creare un utente con autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="115e6-170">Create a user with permissions</span></span>

<span data-ttu-id="115e6-171">Creare un utente del database e assegnare tutti i privilegi in hello `tododb` database.</span><span class="sxs-lookup"><span data-stu-id="115e6-171">Create a database user and give it all privileges in hello `tododb` database.</span></span> <span data-ttu-id="115e6-172">Sostituire i segnaposto hello `<Javaapp_user>` e `<Javaapp_password>` con il proprio nome applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="115e6-172">Replace hello placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

<span data-ttu-id="115e6-173">Chiudere la connessione al server digitando `quit`.</span><span class="sxs-lookup"><span data-stu-id="115e6-173">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a><span data-ttu-id="115e6-174">Distribuire tooAzure esempio hello servizio App</span><span class="sxs-lookup"><span data-stu-id="115e6-174">Deploy hello sample tooAzure App Service</span></span>

<span data-ttu-id="115e6-175">Creare un piano di servizio App di Azure con hello **libero** tariffario utilizzando hello [crea piano di servizio App az](/cli/azure/appservice/plan#create) comando CLI.</span><span class="sxs-lookup"><span data-stu-id="115e6-175">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="115e6-176">piano di servizio App Hello definisce hello risorse fisiche utilizzate toohost app.</span><span class="sxs-lookup"><span data-stu-id="115e6-176">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="115e6-177">Tutte le applicazioni assegnate piano di servizio App tooan condividono tali risorse, consentendo di costo toosave quando si ospitano più applicazioni.</span><span class="sxs-lookup"><span data-stu-id="115e6-177">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="115e6-178">Quando il piano di hello è pronto, hello che CLI di Azure viene illustrato simile output toohello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="115e6-178">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="115e6-179">Creare un'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="115e6-179">Create an Azure Web app</span></span>

 <span data-ttu-id="115e6-180">Hello utilizzare [az webapp creare](/cli/azure/appservice/web#create) toocreate comando CLI una definizione di applicazione web in hello `myAppServicePlan` piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="115e6-180">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="115e6-181">definizione dell'app web Hello fornisce un tooaccess URL all'applicazione e consente di configurare diverse opzioni toodeploy tooAzure il codice.</span><span class="sxs-lookup"><span data-stu-id="115e6-181">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="115e6-182">Hello Substitute `<app_name>` segnaposto con il proprio nome applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="115e6-182">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="115e6-183">Questo nome univoco fa parte del nome di dominio hello predefinito per l'app web hello, quindi nome hello deve toobe univoco tra tutte le App in Azure.</span><span class="sxs-lookup"><span data-stu-id="115e6-183">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="115e6-184">È possibile eseguire il mapping di un'app web di toohello voce di nome di dominio personalizzato prima di esporre tooyour utenti.</span><span class="sxs-lookup"><span data-stu-id="115e6-184">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="115e6-185">Quando la definizione di applicazione web hello è pronta, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="115e6-185">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="115e6-186">Configurare Java</span><span class="sxs-lookup"><span data-stu-id="115e6-186">Configure Java</span></span> 

<span data-ttu-id="115e6-187">Impostare la configurazione di runtime Java hello necessari all'app con hello [aggiornamento configurazione web di az appservice](/cli/azure/appservice/web/config#update) comando.</span><span class="sxs-lookup"><span data-stu-id="115e6-187">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="115e6-188">Hello comando seguente consente di configurare hello web app toorun in una versione recente di Java 8 JDK e [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="115e6-188">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a><span data-ttu-id="115e6-189">Configurare il database SQL di Azure hello di hello app toouse</span><span class="sxs-lookup"><span data-stu-id="115e6-189">Configure hello app toouse hello Azure SQL database</span></span>

<span data-ttu-id="115e6-190">Prima di eseguire l'applicazione di esempio hello, impostare le impostazioni dell'applicazione hello web app toouse hello Azure MySQL database creato in Azure.</span><span class="sxs-lookup"><span data-stu-id="115e6-190">Before running hello sample app, set application settings on hello web app toouse hello Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="115e6-191">Queste proprietà vengono esposte toohello di applicazione web come variabili di ambiente ed eseguire l'override di valori hello impostati in application.properties hello all'interno di app in pacchetto web hello.</span><span class="sxs-lookup"><span data-stu-id="115e6-191">These properties are exposed toohello web application as environment variables and override hello values set in hello application.properties inside hello packaged web app.</span></span> 

<span data-ttu-id="115e6-192">Set di impostazioni dell'applicazione utilizzando [az webapp configurazione appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in hello CLI:</span><span class="sxs-lookup"><span data-stu-id="115e6-192">Set application settings using [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in hello CLI:</span></span>

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

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="115e6-193">Ottenere le credenziali di distribuzione FTP</span><span class="sxs-lookup"><span data-stu-id="115e6-193">Get FTP deployment credentials</span></span> 
<span data-ttu-id="115e6-194">È possibile distribuire il servizio App tooAzure applicazione in vari modi, tra cui FTP, Git locale, GitHub, il Visual Studio Team Services e BitBucket.</span><span class="sxs-lookup"><span data-stu-id="115e6-194">You can deploy your application tooAzure appservice in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="115e6-195">Per questo esempio, hello toodeploy FTP. File WAR compilato in precedenza in del servizio App di tooAzure computer locale.</span><span class="sxs-lookup"><span data-stu-id="115e6-195">For this example, FTP toodeploy hello .WAR file built previously on your local machine tooAzure App Service.</span></span>

<span data-ttu-id="115e6-196">toodetermine quali credenziali toopass lungo in un toohello comando ftp App Web, utilizzare [az servizio App web di distribuzione elenco-pubblicazione-profili](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) comando:</span><span class="sxs-lookup"><span data-stu-id="115e6-196">toodetermine what credentials toopass along in an ftp command toohello Web App, Use [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) command:</span></span> 

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

### <a name="upload-hello-app-using-ftp"></a><span data-ttu-id="115e6-197">Caricare l'applicazione hello tramite FTP</span><span class="sxs-lookup"><span data-stu-id="115e6-197">Upload hello app using FTP</span></span>

<span data-ttu-id="115e6-198">Utilizzare i Preferiti hello di toodeploy strumento FTP. Toohello file WAR */site/wwwroot/webapps* cartella indirizzo server hello prelevati hello `URL` campo nel comando precedente hello.</span><span class="sxs-lookup"><span data-stu-id="115e6-198">Use your favorite FTP tool toodeploy hello .WAR file toohello */site/wwwroot/webapps* folder on hello server address taken from hello `URL` field in hello previous command.</span></span> <span data-ttu-id="115e6-199">Rimuovere la directory di applicazione hello esistente predefinito (radice) e sostituire hello esistente ROOT.war con hello. File WAR incorporato hello in precedenza nell'esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="115e6-199">Remove hello existing default (ROOT) application directory and replace hello existing ROOT.war with hello .WAR file built in hello earlier in hello tutorial.</span></span>

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

### <a name="test-hello-web-app"></a><span data-ttu-id="115e6-200">Test hello web app</span><span class="sxs-lookup"><span data-stu-id="115e6-200">Test hello web app</span></span>

<span data-ttu-id="115e6-201">Sfoglia troppo`http://<app_name>.azurewebsites.net/` e aggiungere alcune attività toohello elenco.</span><span class="sxs-lookup"><span data-stu-id="115e6-201">Browse too`http://<app_name>.azurewebsites.net/` and add a few tasks toohello list.</span></span> 

![App Java in esecuzione nel Servizio app di Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="115e6-203">**Congratulazioni.**</span><span class="sxs-lookup"><span data-stu-id="115e6-203">**Congratulations!**</span></span> <span data-ttu-id="115e6-204">L'app Java basata su dati è in esecuzione in Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="115e6-204">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="115e6-205">Ridistribuzione e l'applicazione hello aggiornamento</span><span class="sxs-lookup"><span data-stu-id="115e6-205">Update hello app and redeploy</span></span>

<span data-ttu-id="115e6-206">Aggiornare tooinclude applicazione hello un'altra colonna nell'elenco di attività hello per selezionare l'elemento hello giorno è stato creato.</span><span class="sxs-lookup"><span data-stu-id="115e6-206">Update hello application tooinclude an additional column in hello todo list for what day hello item was created.</span></span> <span data-ttu-id="115e6-207">Avvio Spring gestisce l'aggiornamento dello schema del database hello automaticamente come hello le modifiche al modello di dati senza modificare i record del database esistente.</span><span class="sxs-lookup"><span data-stu-id="115e6-207">Spring Boot handles updating hello database schema for you as hello data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="115e6-208">Nel sistema locale, aprire *src/main/java/com/example/fabrikam/TodoItem.java* e aggiungere il seguente hello Importa toohello classe:</span><span class="sxs-lookup"><span data-stu-id="115e6-208">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add hello following imports toohello class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="115e6-209">Aggiungere un `String` proprietà `timeCreated` troppo*src/main/java/com/example/fabrikam/TodoItem.java*, inizializzandola con un timestamp al momento della creazione di oggetti.</span><span class="sxs-lookup"><span data-stu-id="115e6-209">Add a `String` property `timeCreated` too*src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="115e6-210">Aggiungere getter/setter per hello nuovo `timeCreated` proprietà durante la modifica di questo file.</span><span class="sxs-lookup"><span data-stu-id="115e6-210">Add getters/setters for hello new `timeCreated` property while you are editing this file.</span></span>

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

3. <span data-ttu-id="115e6-211">Aggiornamento *src/main/java/com/example/fabrikam/TodoDemoController.java* con una riga hello `updateTodo` metodo tooset hello timestamp:</span><span class="sxs-lookup"><span data-stu-id="115e6-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in hello `updateTodo` method tooset hello timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="115e6-212">Aggiungere il supporto per il nuovo campo di hello nel modello Thymeleaf hello.</span><span class="sxs-lookup"><span data-stu-id="115e6-212">Add support for hello new field in hello Thymeleaf template.</span></span> <span data-ttu-id="115e6-213">Aggiornamento *src/main/resources/templates/index.html* con una nuova intestazione di tabella per hello timestamp e il nuovo campo toodisplay hello valore timestamp hello in ogni riga di dati della tabella.</span><span class="sxs-lookup"><span data-stu-id="115e6-213">Update *src/main/resources/templates/index.html* with a new table header for hello timestamp, and a new field toodisplay hello value of hello timestamp in each table data row.</span></span>

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

5. <span data-ttu-id="115e6-214">Ricompilare l'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="115e6-214">Rebuild hello application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="115e6-215">FTP hello aggiornato. WAR come prima, la rimozione di hello esistente */wwwroot del sito/ROOT WebApp* directory e *ROOT.war*, quindi caricare hello aggiornato. File WAR come ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="115e6-215">FTP hello updated .WAR as before, removing hello existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading hello updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="115e6-216">Quando si aggiorna l'applicazione hello, un **ora di creazione** colonna è ora visibile.</span><span class="sxs-lookup"><span data-stu-id="115e6-216">When you refresh hello app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="115e6-217">Quando si aggiunge una nuova attività, hello app verrà popolato automaticamente hello timestamp.</span><span class="sxs-lookup"><span data-stu-id="115e6-217">When you add a new task, hello app will populate hello timestamp automatically.</span></span> <span data-ttu-id="115e6-218">Le attività esistenti rimangono invariati e possono essere utilizzati con l'applicazione hello anche se hello modello di dati sottostante è stata modificata.</span><span class="sxs-lookup"><span data-stu-id="115e6-218">Your existing tasks remain unchanged and work with hello app even though hello underlying data model has changed.</span></span> 

![App Java aggiornata con una nuova colonna](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="115e6-220">Eseguire lo streaming dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="115e6-220">Stream diagnostic logs</span></span> 

<span data-ttu-id="115e6-221">Mentre l'applicazione Java in esecuzione in Azure App Service, è possibile ottenere console hello log inviati tramite pipe direttamente tooyour terminal.</span><span class="sxs-lookup"><span data-stu-id="115e6-221">While your Java application runs in Azure App Service, you can get hello console logs piped directly tooyour terminal.</span></span> <span data-ttu-id="115e6-222">In questo modo, è possibile ottenere hello stessi messaggi di diagnostica toohelp si esegue il debug di errori dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="115e6-222">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="115e6-223">log toostart streaming, usare hello [della parte finale del log di az webapp](/cli/azure/appservice/web/log#tail) comando.</span><span class="sxs-lookup"><span data-stu-id="115e6-223">toostart log streaming, use hello [az webapp log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="115e6-224">Gestire l'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="115e6-224">Manage your Azure web app</span></span>

<span data-ttu-id="115e6-225">Passare toohello toosee portale Azure hello app web che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="115e6-225">Go toohello Azure portal toosee hello web app you created.</span></span>

<span data-ttu-id="115e6-226">toodo, accedi troppo[https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="115e6-226">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="115e6-227">Scegliere dal menu a sinistra hello **servizio App**, quindi fare clic su nome hello dell'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="115e6-227">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![Spostamento del portale tooAzure web app](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="115e6-229">Per impostazione predefinita, il pannello dell'app web illustra hello **Panoramica** pagina.</span><span class="sxs-lookup"><span data-stu-id="115e6-229">By default, your web app's blade shows hello **Overview** page.</span></span> <span data-ttu-id="115e6-230">che offre una visualizzazione dello stato dell'app.</span><span class="sxs-lookup"><span data-stu-id="115e6-230">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="115e6-231">In questa pagina è anche possibile eseguire attività di gestione come arrestare, avviare, riavviare ed eliminare.</span><span class="sxs-lookup"><span data-stu-id="115e6-231">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="115e6-232">le schede di Hello sul lato sinistro di hello del pannello hello mostrano è possibile aprire le pagine di configurazione diverso hello.</span><span class="sxs-lookup"><span data-stu-id="115e6-232">hello tabs on hello left side of hello blade show hello different configuration pages you can open.</span></span>

![Pannello del servizio app nel portale di Azure](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="115e6-234">Queste schede nel pannello hello mostrano hello numerose funzionalità è possibile aggiungere tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="115e6-234">These tabs in hello blade show hello many great features you can add tooyour web app.</span></span> <span data-ttu-id="115e6-235">Hello elenco seguente offre solo alcune delle possibilità hello:</span><span class="sxs-lookup"><span data-stu-id="115e6-235">hello following list gives you just a few of hello possibilities:</span></span>
* <span data-ttu-id="115e6-236">Eseguire il mapping di un nome DNS personalizzato</span><span class="sxs-lookup"><span data-stu-id="115e6-236">Map a custom DNS name</span></span>
* <span data-ttu-id="115e6-237">Associare un certificato SSL personalizzato</span><span class="sxs-lookup"><span data-stu-id="115e6-237">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="115e6-238">Configurare la distribuzione continua</span><span class="sxs-lookup"><span data-stu-id="115e6-238">Configure continuous deployment</span></span>
* <span data-ttu-id="115e6-239">Aumentare le prestazioni e il numero di istanze</span><span class="sxs-lookup"><span data-stu-id="115e6-239">Scale up and out</span></span>
* <span data-ttu-id="115e6-240">Aggiungere l'autenticazione utente</span><span class="sxs-lookup"><span data-stu-id="115e6-240">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="115e6-241">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="115e6-241">Clean up resources</span></span>

<span data-ttu-id="115e6-242">Se non è necessario queste risorse per un'altra esercitazione (vedere [passaggi successivi](#next)), è possibile eliminarle eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="115e6-242">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running hello following command:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="115e6-243">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="115e6-243">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="115e6-244">Creare un database MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="115e6-244">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="115e6-245">Connettersi a un toohello di app di esempio Java MySQL</span><span class="sxs-lookup"><span data-stu-id="115e6-245">Connect a sample Java app toohello MySQL</span></span>
> * <span data-ttu-id="115e6-246">Distribuire hello app tooAzure</span><span class="sxs-lookup"><span data-stu-id="115e6-246">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="115e6-247">Aggiornare e ridistribuire l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="115e6-247">Update and redeploy hello app</span></span>
> * <span data-ttu-id="115e6-248">Eseguire lo streaming dei log di diagnostica in Azure</span><span class="sxs-lookup"><span data-stu-id="115e6-248">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="115e6-249">Gestire app hello in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="115e6-249">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="115e6-250">Spostare toolearn esercitazione successiva toohello come assegnare un nome app toohello toomap un DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="115e6-250">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="115e6-251">Eseguire il mapping di un esistente personalizzato DNS nome tooAzure App Web</span><span class="sxs-lookup"><span data-stu-id="115e6-251">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
