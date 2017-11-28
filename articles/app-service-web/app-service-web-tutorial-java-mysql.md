---
title: Creare un'app Web Java e MySQL in Azure
description: Informazioni su come ottenere un'app Java che si connette al servizio di database MySQL di Azure e funziona nel Servizio app di Azure.
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
ms.openlocfilehash: eb2d59939c4e4486bb14bb143a4a18f9bc1478e1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="9343c-103">Creare un'app Web Java e MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="9343c-103">Build a Java and MySQL web app in Azure</span></span>

<span data-ttu-id="9343c-104">Questa esercitazione illustra come creare un'app Web Java in Azure e connetterla a un database MySQL.</span><span class="sxs-lookup"><span data-stu-id="9343c-104">This tutorial shows you how to create a Java web app in Azure and connect it to a MySQL database.</span></span> <span data-ttu-id="9343c-105">Al termine, verrà creata un'applicazione [Spring Boot](https://projects.spring.io/spring-boot/) che archivia i dati in [Database di Azure per MySQL](https://docs.microsoft.com/azure/mysql/overview) in esecuzione in [App Web del servizio app di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span><span class="sxs-lookup"><span data-stu-id="9343c-105">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span></span>

![App Java in esecuzione nel Servizio app di Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="9343c-107">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="9343c-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9343c-108">Creare un database MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="9343c-108">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="9343c-109">Connettere un'app di esempio al database</span><span class="sxs-lookup"><span data-stu-id="9343c-109">Connect a sample app to the database</span></span>
> * <span data-ttu-id="9343c-110">Distribuire l'app in Azure</span><span class="sxs-lookup"><span data-stu-id="9343c-110">Deploy the app to Azure</span></span>
> * <span data-ttu-id="9343c-111">Aggiornare e ridistribuire l'app</span><span class="sxs-lookup"><span data-stu-id="9343c-111">Update and redeploy the app</span></span>
> * <span data-ttu-id="9343c-112">Eseguire lo streaming dei log di diagnostica in Azure</span><span class="sxs-lookup"><span data-stu-id="9343c-112">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="9343c-113">Monitorare l'app nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9343c-113">Monitor the app in the Azure portal</span></span>


## <a name="prerequisites"></a><span data-ttu-id="9343c-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9343c-114">Prerequisites</span></span>

1. [<span data-ttu-id="9343c-115">Scaricare e installare Git</span><span class="sxs-lookup"><span data-stu-id="9343c-115">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="9343c-116">Scaricare e installare Java 7 JDK o versione successiva</span><span class="sxs-lookup"><span data-stu-id="9343c-116">Download and install the Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [<span data-ttu-id="9343c-117">Scaricare, installare e avviare MySQL</span><span class="sxs-lookup"><span data-stu-id="9343c-117">Download, install, and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9343c-118">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="9343c-118">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9343c-119">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="9343c-119">Run `az --version` to find the version.</span></span> <span data-ttu-id="9343c-120">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9343c-120">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-local-mysql"></a><span data-ttu-id="9343c-121">Preparare MySQL in locale</span><span class="sxs-lookup"><span data-stu-id="9343c-121">Prepare local MySQL</span></span> 

<span data-ttu-id="9343c-122">In questo passaggio si crea un database in un server locale di MySQL da usare per il test dell'app in locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="9343c-122">In this step, you create a database in a local MySQL server for use in testing the app locally on your machine.</span></span>

### <a name="connect-to-mysql-server"></a><span data-ttu-id="9343c-123">Connettersi al server MySQL</span><span class="sxs-lookup"><span data-stu-id="9343c-123">Connect to MySQL server</span></span>

<span data-ttu-id="9343c-124">In una finestra terminale connettersi al server MySQL locale.</span><span class="sxs-lookup"><span data-stu-id="9343c-124">In a terminal window, connect to your local MySQL server.</span></span> <span data-ttu-id="9343c-125">È possibile usare questa finestra del terminale per eseguire tutti i comandi presenti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="9343c-125">You can use this terminal window to run all the commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="9343c-126">Se viene richiesto di immettere una password, immettere la password per l'account `root`.</span><span class="sxs-lookup"><span data-stu-id="9343c-126">If you're prompted for a password, enter the password for the `root` account.</span></span> <span data-ttu-id="9343c-127">Se non si ricorda la password dell'account radice, vedere [MySQL: procedura per reimpostare la password radice](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="9343c-127">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="9343c-128">Se il comando viene eseguito correttamente, il server MySQL è già in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9343c-128">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="9343c-129">In caso contrario, assicurarsi che il server MySQL locale sia stato avviato seguendo la [procedura successiva all'installazione di MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="9343c-129">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="9343c-130">Creare un database</span><span class="sxs-lookup"><span data-stu-id="9343c-130">Create a database</span></span> 

<span data-ttu-id="9343c-131">Nel prompt `mysql` creare un database e una tabella per gli elementi attività.</span><span class="sxs-lookup"><span data-stu-id="9343c-131">In the `mysql` prompt, create a database and a table for the to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="9343c-132">Chiudere la connessione al server digitando `quit`.</span><span class="sxs-lookup"><span data-stu-id="9343c-132">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-the-sample-app"></a><span data-ttu-id="9343c-133">Creare ed eseguire l'app di esempio</span><span class="sxs-lookup"><span data-stu-id="9343c-133">Create and run the sample app</span></span> 

<span data-ttu-id="9343c-134">In questo passaggio si clona l'app Spring Boot di esempio, la si configura per l'uso del database MySQL locale e la si esegue nel computer.</span><span class="sxs-lookup"><span data-stu-id="9343c-134">In this step, you clone sample Spring boot app, configure it to use the local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-the-sample"></a><span data-ttu-id="9343c-135">Clonare l'esempio</span><span class="sxs-lookup"><span data-stu-id="9343c-135">Clone the sample</span></span>

<span data-ttu-id="9343c-136">Nella finestra del terminale passare alla directory di lavoro e clonare il repository di esempio.</span><span class="sxs-lookup"><span data-stu-id="9343c-136">In the terminal window, navigate to a working directory and clone the sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-the-app-to-use-the-mysql-database"></a><span data-ttu-id="9343c-137">Configurare l'app per l'uso del database MySQL</span><span class="sxs-lookup"><span data-stu-id="9343c-137">Configure the app to use the MySQL database</span></span>

<span data-ttu-id="9343c-138">Aggiornare `spring.datasource.password` e il valore in *spring-boot-mysql-todo/src/main/resources/application.properties* con la stessa password radice usata per aprire il prompt MySQL:</span><span class="sxs-lookup"><span data-stu-id="9343c-138">Update the `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with the same root password used to open the MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-the-sample"></a><span data-ttu-id="9343c-139">Compilare ed eseguire l'esempio</span><span class="sxs-lookup"><span data-stu-id="9343c-139">Build and run the sample</span></span>

<span data-ttu-id="9343c-140">Compilare ed eseguire l'esempio usando il wrapper Maven incluso nel repository:</span><span class="sxs-lookup"><span data-stu-id="9343c-140">Build and run the sample using the Maven wrapper included in the repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="9343c-141">Inserire nel browser l'indirizzo http://localhost:8080 per vedere l'esempio in azione.</span><span class="sxs-lookup"><span data-stu-id="9343c-141">Open your browser to http://localhost:8080 to see in the sample in action.</span></span> <span data-ttu-id="9343c-142">Quando si aggiungono attività all'elenco, usare i comandi SQL seguenti nel prompt MySQL per visualizzare i dati archiviati in MySQL.</span><span class="sxs-lookup"><span data-stu-id="9343c-142">As you add tasks to the list,  use the following SQL commands in the MySQL prompt to view the data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="9343c-143">Arrestare l'applicazione premendo `Ctrl`+`C` nel terminale.</span><span class="sxs-lookup"><span data-stu-id="9343c-143">Stop the application by hitting `Ctrl`+`C` in the terminal.</span></span> 

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="9343c-144">Creare un database MySQL di Azure</span><span class="sxs-lookup"><span data-stu-id="9343c-144">Create an Azure MySQL database</span></span>

<span data-ttu-id="9343c-145">In questo passaggio si crea un'istanza di [Database di Azure per MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) usando l'[interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9343c-145">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="9343c-146">Si configura l'applicazione di esempio per usare questo database più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="9343c-146">You configure the sample application to use this database later on in the tutorial.</span></span>

<span data-ttu-id="9343c-147">Usare l'interfaccia della riga di comando di Azure 2.0 in una finestra terminale per creare le risorse necessarie per ospitare l'applicazione Java nel Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="9343c-147">Use the Azure CLI 2.0 in a terminal window to create the resources needed to host your Java application in Azure appservice.</span></span> <span data-ttu-id="9343c-148">Accedere alla sottoscrizione di Azure con il comando [az login](/cli/azure/#login) e seguire le istruzioni visualizzate.</span><span class="sxs-lookup"><span data-stu-id="9343c-148">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="9343c-149">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="9343c-149">Create a resource group</span></span>

<span data-ttu-id="9343c-150">Creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="9343c-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="9343c-151">Un gruppo di risorse di Azure è un contenitore logico in cui vengono distribuite e gestite le risorse correlate, ad esempio app Web, database e account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9343c-151">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="9343c-152">L'esempio seguente crea un gruppo di risorse nell'area Europa settentrionale:</span><span class="sxs-lookup"><span data-stu-id="9343c-152">The following example creates a resource group in the North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="9343c-153">Per visualizzare i possibili valori utilizzabili per `--location`, usare il comando [az appservice list-locations](/cli/azure/appservice#list-locations).</span><span class="sxs-lookup"><span data-stu-id="9343c-153">To see the possible values you can use for `--location`, use the [az appservice list-locations](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="9343c-154">Creare un server MySQL</span><span class="sxs-lookup"><span data-stu-id="9343c-154">Create a MySQL server</span></span>

<span data-ttu-id="9343c-155">Creare un server nel database di Azure per MySQL (anteprima) con il comando [az mysql server create](/cli/azure/mysql/server#create).</span><span class="sxs-lookup"><span data-stu-id="9343c-155">Create a server in Azure Database for MySQL (Preview) with the [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>    
<span data-ttu-id="9343c-156">Sostituire il segnaposto `<mysql_server_name>` con il nome univoco del proprio server MySQL.</span><span class="sxs-lookup"><span data-stu-id="9343c-156">Substitute your own unique MySQL server name where you see the `<mysql_server_name>` placeholder.</span></span> <span data-ttu-id="9343c-157">Questo nome fa parte del nome host del server MySQL, `<mysql_server_name>.mysql.database.azure.com`, pertanto deve essere univoco a livello globale.</span><span class="sxs-lookup"><span data-stu-id="9343c-157">This name is part of your MySQL server's hostname, `<mysql_server_name>.mysql.database.azure.com`, so it needs to be globally unique.</span></span> <span data-ttu-id="9343c-158">Sostituire anche `<admin_user>` e `<admin_password>` con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="9343c-158">Also substitute `<admin_user>` and `<admin_password>` with your own values.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

<span data-ttu-id="9343c-159">Al termine della creazione del server MySQL, l'interfaccia della riga di comando di Azure mostra informazioni simili all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="9343c-159">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="9343c-160">Configurare il firewall del server</span><span class="sxs-lookup"><span data-stu-id="9343c-160">Configure server firewall</span></span>

<span data-ttu-id="9343c-161">Creare una regola del firewall per il server MySQL per consentire le connessioni client tramite il comando [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="9343c-161">Create a firewall rule for your MySQL server to allow client connections by using the [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="9343c-162">Database di Azure per MySQL (anteprima) per il momento non consente di abilitare automaticamente le connessioni dai servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="9343c-162">Azure Database for MySQL (Preview) does not currently automatically enable connections from Azure services.</span></span> <span data-ttu-id="9343c-163">Poiché gli indirizzi IP in Azure vengono assegnati dinamicamente, per il momento è preferibile abilitarli tutti.</span><span class="sxs-lookup"><span data-stu-id="9343c-163">As IP addresses in Azure are dynamically assigned, it is better to enable all IP addresses for now.</span></span> <span data-ttu-id="9343c-164">Il servizio è ancora in anteprima, ma presto verranno abilitati metodi migliori per la protezione del database.</span><span class="sxs-lookup"><span data-stu-id="9343c-164">As the service continues its preview, better methods for securing your database will be enabled.</span></span>

## <a name="configure-the-azure-mysql-database"></a><span data-ttu-id="9343c-165">Configurare il database MySQL di Azure</span><span class="sxs-lookup"><span data-stu-id="9343c-165">Configure the Azure MySQL database</span></span>

<span data-ttu-id="9343c-166">Nella finestra del terminale sul computer connettersi al server MySQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="9343c-166">In the terminal window on your computer, connect to the MySQL server in Azure.</span></span> <span data-ttu-id="9343c-167">Usare il valore specificato precedentemente per `<admin_user>` e `<mysql_server_name>`.</span><span class="sxs-lookup"><span data-stu-id="9343c-167">Use the value you specified previously for `<admin_user>` and `<mysql_server_name>`.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="9343c-168">Creare un database</span><span class="sxs-lookup"><span data-stu-id="9343c-168">Create a database</span></span> 

<span data-ttu-id="9343c-169">Nel prompt `mysql` creare un database e una tabella per gli elementi attività.</span><span class="sxs-lookup"><span data-stu-id="9343c-169">In the `mysql` prompt, create a database and a table for the to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="9343c-170">Creare un utente con autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="9343c-170">Create a user with permissions</span></span>

<span data-ttu-id="9343c-171">Creare un utente del database e concedergli tutti i privilegi nel database `tododb`.</span><span class="sxs-lookup"><span data-stu-id="9343c-171">Create a database user and give it all privileges in the `tododb` database.</span></span> <span data-ttu-id="9343c-172">Sostituire i segnaposto `<Javaapp_user>` e `<Javaapp_password>` con il proprio nome univoco dell'app.</span><span class="sxs-lookup"><span data-stu-id="9343c-172">Replace the placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* TO '<Javaapp_user>';
```

<span data-ttu-id="9343c-173">Chiudere la connessione al server digitando `quit`.</span><span class="sxs-lookup"><span data-stu-id="9343c-173">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-the-sample-to-azure-app-service"></a><span data-ttu-id="9343c-174">Distribuire l'esempio in Servizio App di Azure</span><span class="sxs-lookup"><span data-stu-id="9343c-174">Deploy the sample to Azure App Service</span></span>

<span data-ttu-id="9343c-175">Creare un piano di servizio app di Azure con il piano tariffario **GRATUITO** usando il comando dell'interfaccia della riga di comando [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="9343c-175">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="9343c-176">Il piano di servizio app definisce le risorse fisiche usate per ospitare le app.</span><span class="sxs-lookup"><span data-stu-id="9343c-176">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="9343c-177">Tutte le applicazioni assegnate a un piano di servizio app condividono queste risorse, per poter consentire un risparmio sui costi quando si ospitano più app.</span><span class="sxs-lookup"><span data-stu-id="9343c-177">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="9343c-178">Quando il piano è pronto, l'output dell'interfaccia della riga di comando di Azure è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="9343c-178">When the plan is ready, the Azure CLI shows similar output to the following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="9343c-179">Creare un'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="9343c-179">Create an Azure Web app</span></span>

 <span data-ttu-id="9343c-180">Usare il comando dell'interfaccia della riga di comando [az webapp create](/cli/azure/appservice/web#create) per creare la definizione di un'app Web nel piano di servizio app `myAppServicePlan`.</span><span class="sxs-lookup"><span data-stu-id="9343c-180">Use the [az webapp create](/cli/azure/appservice/web#create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="9343c-181">La definizione dell'app Web fornisce un URL con cui accedere all'applicazione e configura diverse opzioni per distribuire il codice in Azure.</span><span class="sxs-lookup"><span data-stu-id="9343c-181">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="9343c-182">Sostituire il segnaposto `<app_name>` con il nome univoco dell'app.</span><span class="sxs-lookup"><span data-stu-id="9343c-182">Substitute the `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="9343c-183">Questo nome univoco fa parte del nome di dominio predefinito per l'app Web, quindi è necessario che sia univoco rispetto a tutte le app presenti in Azure.</span><span class="sxs-lookup"><span data-stu-id="9343c-183">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="9343c-184">È possibile eseguire il mapping di una voce di nome di dominio personalizzata all'app Web prima di esporla agli utenti.</span><span class="sxs-lookup"><span data-stu-id="9343c-184">You can map a custom domain name entry to the web app before you expose it to your users.</span></span>

<span data-ttu-id="9343c-185">Quando la definizione dell'app Web è pronta, l'interfaccia della riga di comando di Azure visualizza informazioni simili all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="9343c-185">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="9343c-186">Configurare Java</span><span class="sxs-lookup"><span data-stu-id="9343c-186">Configure Java</span></span> 

<span data-ttu-id="9343c-187">Impostare la configurazione del runtime Java necessaria per l'app con il comando [az appservice web config update](/cli/azure/appservice/web/config#update).</span><span class="sxs-lookup"><span data-stu-id="9343c-187">Set up the Java runtime configuration that your app needs with the  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="9343c-188">Il comando seguente configura l'app Web per l'esecuzione in un'istanza recente di Java 8 JDK e in [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="9343c-188">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-the-app-to-use-the-azure-sql-database"></a><span data-ttu-id="9343c-189">Configurare l'app per l'uso del database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="9343c-189">Configure the app to use the Azure SQL database</span></span>

<span data-ttu-id="9343c-190">Prima di eseguire l'app di esempio, configurare le impostazioni dell'applicazione nell'app Web per l'uso del database MySQL di Azure creato in Azure.</span><span class="sxs-lookup"><span data-stu-id="9343c-190">Before running the sample app, set application settings on the web app to use the Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="9343c-191">Queste proprietà vengono esposte all'applicazione Web come variabili di ambiente ed eseguono l'override dei valori impostati in application.properties nell'app Web inclusa nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9343c-191">These properties are exposed to the web application as environment variables and override the values set in the application.properties inside the packaged web app.</span></span> 

<span data-ttu-id="9343c-192">Configurare le impostazioni dell'applicazione usando [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) nell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="9343c-192">Set application settings using [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in the CLI:</span></span>

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

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="9343c-193">Ottenere le credenziali di distribuzione FTP</span><span class="sxs-lookup"><span data-stu-id="9343c-193">Get FTP deployment credentials</span></span> 
<span data-ttu-id="9343c-194">È possibile distribuire l'applicazione nel Servizio app di Azure attraverso varie soluzioni, tra cui FTP, Git locale, GitHub, Visual Studio Team Services e BitBucket.</span><span class="sxs-lookup"><span data-stu-id="9343c-194">You can deploy your application to Azure appservice in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="9343c-195">In questo esempio viene usato FTP per distribuire in Servizio app di Azure il file WAR compilato prima sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="9343c-195">For this example, FTP to deploy the .WAR file built previously on your local machine to Azure App Service.</span></span>

<span data-ttu-id="9343c-196">Per determinare quali credenziali passare in un comando FTP per l'app Web, usare il comando [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles):</span><span class="sxs-lookup"><span data-stu-id="9343c-196">To determine what credentials to pass along in an ftp command to the Web App, Use [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) command:</span></span> 

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

### <a name="upload-the-app-using-ftp"></a><span data-ttu-id="9343c-197">Caricare l'app usando FTP</span><span class="sxs-lookup"><span data-stu-id="9343c-197">Upload the app using FTP</span></span>

<span data-ttu-id="9343c-198">Usare lo strumento FTP preferito per distribuire il file WAR nella cartella */site/wwwroot/webapps* all'indirizzo server ottenuto dal campo `URL` nel comando precedente.</span><span class="sxs-lookup"><span data-stu-id="9343c-198">Use your favorite FTP tool to deploy the .WAR file to the */site/wwwroot/webapps* folder on the server address taken from the `URL` field in the previous command.</span></span> <span data-ttu-id="9343c-199">Rimuovere la directory dell'applicazione predefinita esistente (ROOT) e sostituire il file ROOT.war esistente con il file WAR compilato prima nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="9343c-199">Remove the existing default (ROOT) application directory and replace the existing ROOT.war with the .WAR file built in the earlier in the tutorial.</span></span>

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected to waws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-the-web-app"></a><span data-ttu-id="9343c-200">Testare l'app Web</span><span class="sxs-lookup"><span data-stu-id="9343c-200">Test the web app</span></span>

<span data-ttu-id="9343c-201">Passare a `http://<app_name>.azurewebsites.net/` e aggiungere alcune attività all'elenco.</span><span class="sxs-lookup"><span data-stu-id="9343c-201">Browse to `http://<app_name>.azurewebsites.net/` and add a few tasks to the list.</span></span> 

![App Java in esecuzione nel Servizio app di Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="9343c-203">**Congratulazioni.**</span><span class="sxs-lookup"><span data-stu-id="9343c-203">**Congratulations!**</span></span> <span data-ttu-id="9343c-204">L'app Java basata su dati è in esecuzione in Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="9343c-204">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-the-app-and-redeploy"></a><span data-ttu-id="9343c-205">Aggiornare e ridistribuire l'app</span><span class="sxs-lookup"><span data-stu-id="9343c-205">Update the app and redeploy</span></span>

<span data-ttu-id="9343c-206">Aggiornare l'applicazione per includere una colonna aggiuntiva nell'elenco attività, indicante il giorno in cui l'elemento è stato creato.</span><span class="sxs-lookup"><span data-stu-id="9343c-206">Update the application to include an additional column in the todo list for what day the item was created.</span></span> <span data-ttu-id="9343c-207">Spring Boot gestisce automaticamente lo schema del database quando il modello di dati cambia senza modificare i record di database esistenti.</span><span class="sxs-lookup"><span data-stu-id="9343c-207">Spring Boot handles updating the database schema for you as the data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="9343c-208">Nel sistema locale aprire *src/main/java/com/example/fabrikam/TodoItem.java* e aggiungere le importazioni seguenti alla classe:</span><span class="sxs-lookup"><span data-stu-id="9343c-208">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add the following imports to the class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="9343c-209">Aggiungere una proprietà `timeCreated` di tipo `String` a *src/main/java/com/example/fabrikam/TodoItem.java*, inizializzandola con un timestamp al momento della creazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9343c-209">Add a `String` property `timeCreated` to *src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="9343c-210">Aggiungere getter/setter per la nuova proprietà `timeCreated` mentre si modifica questo file.</span><span class="sxs-lookup"><span data-stu-id="9343c-210">Add getters/setters for the new `timeCreated` property while you are editing this file.</span></span>

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

3. <span data-ttu-id="9343c-211">Aggiornare *src/main/java/com/example/fabrikam/TodoDemoController.java* con una riga nel metodo `updateTodo` per impostare il timestamp:</span><span class="sxs-lookup"><span data-stu-id="9343c-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in the `updateTodo` method to set the timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="9343c-212">Aggiungere il supporto per il nuovo campo nel modello Thymeleaf.</span><span class="sxs-lookup"><span data-stu-id="9343c-212">Add support for the new field in the Thymeleaf template.</span></span> <span data-ttu-id="9343c-213">Aggiornare *src/main/resources/templates/index.html* con una nuova intestazione della tabella per il timestamp e un nuovo campo per visualizzare il valore del timestamp in ogni riga di dati della tabella.</span><span class="sxs-lookup"><span data-stu-id="9343c-213">Update *src/main/resources/templates/index.html* with a new table header for the timestamp, and a new field to display the value of the timestamp in each table data row.</span></span>

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

5. <span data-ttu-id="9343c-214">Ricompilare l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="9343c-214">Rebuild the application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="9343c-215">Distribuire tramite FTP il file WAR aggiornato come prima, rimuovendo la directory *site/wwwroot/webapps/ROOT* e il file *ROOT.war* esistenti, quindi caricando il file WAR aggiornato come ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="9343c-215">FTP the updated .WAR as before, removing the existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading the updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="9343c-216">Quando si aggiorna l'app, è ora visibile una colonna **Time Created** (Ora di creazione).</span><span class="sxs-lookup"><span data-stu-id="9343c-216">When you refresh the app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="9343c-217">Quando si aggiunge una nuova attività, l'app popolerà il timestamp automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9343c-217">When you add a new task, the app will populate the timestamp automatically.</span></span> <span data-ttu-id="9343c-218">Le attività esistenti rimangono invariate e usano l'app anche se il modello di dati sottostante è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="9343c-218">Your existing tasks remain unchanged and work with the app even though the underlying data model has changed.</span></span> 

![App Java aggiornata con una nuova colonna](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="9343c-220">Eseguire lo streaming dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="9343c-220">Stream diagnostic logs</span></span> 

<span data-ttu-id="9343c-221">Mentre l'applicazione Java è in esecuzione in Servizio app di Azure, è possibile fare in modo che i log della console siano inviati tramite pipe direttamente al terminale.</span><span class="sxs-lookup"><span data-stu-id="9343c-221">While your Java application runs in Azure App Service, you can get the console logs piped directly to your terminal.</span></span> <span data-ttu-id="9343c-222">Ciò consente di ottenere gli stessi messaggi di diagnostica per il debug degli errori dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9343c-222">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="9343c-223">Per avviare lo streaming dei log, usare il comando [az webapp log tail](/cli/azure/appservice/web/log#tail).</span><span class="sxs-lookup"><span data-stu-id="9343c-223">To start log streaming, use the [az webapp log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="9343c-224">Gestire l'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="9343c-224">Manage your Azure web app</span></span>

<span data-ttu-id="9343c-225">Accedere al portale di Azure per visualizzare l'app Web creata.</span><span class="sxs-lookup"><span data-stu-id="9343c-225">Go to the Azure portal to see the web app you created.</span></span>

<span data-ttu-id="9343c-226">A tale scopo, accedere a [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9343c-226">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="9343c-227">Nel menu a sinistra fare clic su **Servizi app** e quindi sul nome dell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="9343c-227">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Passare all'app Web di Azure nel portale](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="9343c-229">Per impostazione predefinita, nel pannello dell'app Web viene aperta la pagina **Panoramica**,</span><span class="sxs-lookup"><span data-stu-id="9343c-229">By default, your web app's blade shows the **Overview** page.</span></span> <span data-ttu-id="9343c-230">che offre una visualizzazione dello stato dell'app.</span><span class="sxs-lookup"><span data-stu-id="9343c-230">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="9343c-231">In questa pagina è anche possibile eseguire attività di gestione come arrestare, avviare, riavviare ed eliminare.</span><span class="sxs-lookup"><span data-stu-id="9343c-231">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="9343c-232">Le schede sul lato sinistro del pannello mostrano le diverse pagine di configurazione che è possibile aprire.</span><span class="sxs-lookup"><span data-stu-id="9343c-232">The tabs on the left side of the blade show the different configuration pages you can open.</span></span>

![Pannello del servizio app nel portale di Azure](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="9343c-234">Queste schede del pannello mostrano le numerose utili funzionalità che è possibile aggiungere all'app Web.</span><span class="sxs-lookup"><span data-stu-id="9343c-234">These tabs in the blade show the many great features you can add to your web app.</span></span> <span data-ttu-id="9343c-235">Nell'elenco seguente sono riportate solo alcune delle possibilità:</span><span class="sxs-lookup"><span data-stu-id="9343c-235">The following list gives you just a few of the possibilities:</span></span>
* <span data-ttu-id="9343c-236">Eseguire il mapping di un nome DNS personalizzato</span><span class="sxs-lookup"><span data-stu-id="9343c-236">Map a custom DNS name</span></span>
* <span data-ttu-id="9343c-237">Associare un certificato SSL personalizzato</span><span class="sxs-lookup"><span data-stu-id="9343c-237">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="9343c-238">Configurare la distribuzione continua</span><span class="sxs-lookup"><span data-stu-id="9343c-238">Configure continuous deployment</span></span>
* <span data-ttu-id="9343c-239">Aumentare le prestazioni e il numero di istanze</span><span class="sxs-lookup"><span data-stu-id="9343c-239">Scale up and out</span></span>
* <span data-ttu-id="9343c-240">Aggiungere l'autenticazione utente</span><span class="sxs-lookup"><span data-stu-id="9343c-240">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="9343c-241">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="9343c-241">Clean up resources</span></span>

<span data-ttu-id="9343c-242">Se queste risorse non sono necessarie per un'altra esercitazione (vedere [Passaggi successivi](#next)), è possibile eliminarle eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="9343c-242">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running the following command:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="9343c-243">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9343c-243">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9343c-244">Creare un database MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="9343c-244">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="9343c-245">Connettere un'app Java di esempio a MySQL</span><span class="sxs-lookup"><span data-stu-id="9343c-245">Connect a sample Java app to the MySQL</span></span>
> * <span data-ttu-id="9343c-246">Distribuire l'app in Azure</span><span class="sxs-lookup"><span data-stu-id="9343c-246">Deploy the app to Azure</span></span>
> * <span data-ttu-id="9343c-247">Aggiornare e ridistribuire l'app</span><span class="sxs-lookup"><span data-stu-id="9343c-247">Update and redeploy the app</span></span>
> * <span data-ttu-id="9343c-248">Eseguire lo streaming dei log di diagnostica in Azure</span><span class="sxs-lookup"><span data-stu-id="9343c-248">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="9343c-249">Gestire l'app nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9343c-249">Manage the app in the Azure portal</span></span>

<span data-ttu-id="9343c-250">Passare all'esercitazione successiva per apprendere come eseguire il mapping di un nome DNS personalizzato all'app.</span><span class="sxs-lookup"><span data-stu-id="9343c-250">Advance to the next tutorial to learn how to map a custom DNS name to the app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="9343c-251">Eseguire il mapping di un nome DNS personalizzato esistente ad app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="9343c-251">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)