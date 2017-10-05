---
title: Progettare il primo Database di Azure per PostgreSQL tramite il portale di Azure | Documentazione Microsoft
description: In questa esercitazione viene illustrato come progettare il primo Database di Azure per PostgreSQL tramite il portale di Azure.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: tutorial, mvc
ms.topic: tutorial
ms.date: 05/10/2017
ms.openlocfilehash: 2aa9d10749b54537495ad3e09566c43718f67a9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-the-azure-portal"></a><span data-ttu-id="4011b-103">Progettare il primo Database di Azure per PostgreSQL tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4011b-103">Design your first Azure Database for PostgreSQL using the Azure portal</span></span>

<span data-ttu-id="4011b-104">Il Database di Azure per PostgreSQL è un servizio gestito che consente di eseguire, gestire e scalare i database PostgreSQL a disponibilità elevata nel cloud.</span><span class="sxs-lookup"><span data-stu-id="4011b-104">Azure Database for PostgreSQL is a managed service that enables you to run, manage, and scale highly available PostgreSQL databases in the cloud.</span></span> <span data-ttu-id="4011b-105">Tramite il portale di Azure, è possibile gestire facilmente il server e progettare un database.</span><span class="sxs-lookup"><span data-stu-id="4011b-105">Using the Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="4011b-106">In questa esercitazione si userà il portale di Azure per imparare a:</span><span class="sxs-lookup"><span data-stu-id="4011b-106">In this tutorial, you use the Azure portal to learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="4011b-107">Creare un database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="4011b-107">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="4011b-108">Configurare il firewall del server</span><span class="sxs-lookup"><span data-stu-id="4011b-108">Configure the server firewall</span></span>
> * <span data-ttu-id="4011b-109">Usare l'utilità [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) per creare un database</span><span class="sxs-lookup"><span data-stu-id="4011b-109">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="4011b-110">Caricare dati di esempio</span><span class="sxs-lookup"><span data-stu-id="4011b-110">Load sample data</span></span>
> * <span data-ttu-id="4011b-111">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="4011b-111">Query data</span></span>
> * <span data-ttu-id="4011b-112">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="4011b-112">Update data</span></span>
> * <span data-ttu-id="4011b-113">Ripristinare i dati</span><span class="sxs-lookup"><span data-stu-id="4011b-113">Restore data</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4011b-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4011b-114">Prerequisites</span></span>
<span data-ttu-id="4011b-115">Se non si ha una sottoscrizione di Azure, creare un account [gratuito](https://azure.microsoft.com/free/) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="4011b-115">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="4011b-116">Accedere al Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4011b-116">Log in to the Azure portal</span></span>
<span data-ttu-id="4011b-117">Accedere al [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4011b-117">Log in to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-postgresql"></a><span data-ttu-id="4011b-118">Creare un database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="4011b-118">Create an Azure Database for PostgreSQL</span></span>

<span data-ttu-id="4011b-119">Verrà creato un database di Azure per il server PostgreSQL con un set definito di [risorse di calcolo e di archiviazione](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="4011b-119">An Azure Database for PostgreSQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="4011b-120">Il server viene creato all'interno di un [gruppo di risorse di Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4011b-120">The server is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="4011b-121">Seguire questi passaggi per creare un database di Azure per il server PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="4011b-121">Follow these steps to create an Azure Database for PostgreSQL server:</span></span>
1.  <span data-ttu-id="4011b-122">Fare clic sul pulsante **+ Nuovo** nell'angolo superiore sinistro del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4011b-122">Click the **+ New**  button found on the upper left-hand corner of the Azure portal.</span></span>
2.  <span data-ttu-id="4011b-123">Selezionare **Database** nella pagina **Nuovo** e selezionare il **Database di Azure per PostgreSQL** nella pagina **Database**.</span><span class="sxs-lookup"><span data-stu-id="4011b-123">Select **Databases** from the **New** page, and select **Azure Database for PostgreSQL** from the **Databases** page.</span></span>
 <span data-ttu-id="4011b-124">![Database di Azure per PostgreSQL - Creare il database](./media/tutorial-design-database-using-azure-portal/1-create-database.png)</span><span class="sxs-lookup"><span data-stu-id="4011b-124">![Azure Database for PostgreSQL - Create the database](./media/tutorial-design-database-using-azure-portal/1-create-database.png)</span></span>

3.  <span data-ttu-id="4011b-125">Compilare il modulo per i dettagli del nuovo server con le informazioni seguenti, come illustrato nell'immagine precedente:</span><span class="sxs-lookup"><span data-stu-id="4011b-125">Fill out the new server details form with the following information, as shown on the preceding image:</span></span>
    - <span data-ttu-id="4011b-126">Nome server: **mypgserver-20170401** (il nome di un server esegue il mapping al nome DNS e quindi deve essere univoco a livello globale)</span><span class="sxs-lookup"><span data-stu-id="4011b-126">Server name: **mypgserver-20170401** (name of a server maps to DNS name and is thus required to be globally unique)</span></span> 
    - <span data-ttu-id="4011b-127">Sottoscrizione: se si hanno più sottoscrizioni, scegliere la sottoscrizione appropriata in cui si trova o viene fatturata la risorsa.</span><span class="sxs-lookup"><span data-stu-id="4011b-127">Subscription: If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span>
    - <span data-ttu-id="4011b-128">Gruppo di risorse: **myresourcegroup**</span><span class="sxs-lookup"><span data-stu-id="4011b-128">Resource group: **myresourcegroup**</span></span>
    - <span data-ttu-id="4011b-129">L'accesso dell'amministratore del server e la password scelta</span><span class="sxs-lookup"><span data-stu-id="4011b-129">Server admin login and password of your choice</span></span>
    - <span data-ttu-id="4011b-130">Località</span><span class="sxs-lookup"><span data-stu-id="4011b-130">Location</span></span>
    - <span data-ttu-id="4011b-131">Versione di PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="4011b-131">PostgreSQL Version</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="4011b-132">L'account di accesso amministratore server e la password qui specificati sono necessari per accedere al server e ai relativi database più avanti in questa guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="4011b-132">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="4011b-133">Prendere nota di queste informazioni per usarle in seguito.</span><span class="sxs-lookup"><span data-stu-id="4011b-133">Remember or record this information for later use.</span></span>

4.  <span data-ttu-id="4011b-134">Fare clic su **Piano tariffario** per specificare il livello di servizio e il livello delle prestazioni per il nuovo database.</span><span class="sxs-lookup"><span data-stu-id="4011b-134">Click **Pricing tier** to specify the service tier and performance level for your new database.</span></span> <span data-ttu-id="4011b-135">Per questa guida di avvio rapido, selezionare il livello **Basic**, **50 unità di calcolo** e **50 GB** di spazio di archiviazione incluso.</span><span class="sxs-lookup"><span data-stu-id="4011b-135">For this quick start, select **Basic** Tier, **50 Compute Units** and **50 GB** of included storage.</span></span>
 <span data-ttu-id="4011b-136">![Database di Azure per PostgreSQL - Selezionare il livello del servizio](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)</span><span class="sxs-lookup"><span data-stu-id="4011b-136">![Azure Database for PostgreSQL - pick the service tier](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)</span></span>
5.  <span data-ttu-id="4011b-137">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4011b-137">Click **Ok**.</span></span>
6.  <span data-ttu-id="4011b-138">Fare clic su **Crea** per eseguire il provisioning del server.</span><span class="sxs-lookup"><span data-stu-id="4011b-138">Click **Create** to provision the server.</span></span> <span data-ttu-id="4011b-139">Il provisioning richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="4011b-139">Provisioning takes a few minutes.</span></span>

  > [!TIP]
  > <span data-ttu-id="4011b-140">Selezionare l'opzione **Aggiungi al dashboard** per tenere facilmente traccia delle distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="4011b-140">Check the **Pin to dashboard** option to allow easy tracking of your deployments.</span></span>

7.  <span data-ttu-id="4011b-141">Sulla barra degli strumenti fare clic su **Notifiche** per monitorare il processo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4011b-141">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>
 <span data-ttu-id="4011b-142">![Database di Azure per PostgreSQL - Vedere le notifiche](./media/tutorial-design-database-using-azure-portal/3-notifications.png)</span><span class="sxs-lookup"><span data-stu-id="4011b-142">![Azure Database for PostgreSQL - See notifications](./media/tutorial-design-database-using-azure-portal/3-notifications.png)</span></span>
   
  <span data-ttu-id="4011b-143">Per impostazione predefinita, il database **postgres** viene creato nel server.</span><span class="sxs-lookup"><span data-stu-id="4011b-143">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="4011b-144">Il database [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) è un database predefinito che può essere usato da utenti, utilità e applicazioni di terze parti.</span><span class="sxs-lookup"><span data-stu-id="4011b-144">The [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 

## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="4011b-145">Configurare una regola del firewall a livello di server</span><span class="sxs-lookup"><span data-stu-id="4011b-145">Configure a server-level firewall rule</span></span>

<span data-ttu-id="4011b-146">Il database di Azure per il servizio PostgreSQL crea un firewall a livello di server.</span><span class="sxs-lookup"><span data-stu-id="4011b-146">The Azure Database for PostgreSQL service creates a firewall at the server-level.</span></span> <span data-ttu-id="4011b-147">Questo firewall impedisce alle applicazioni e agli strumenti esterni di connettersi al server e ai database nel server, a meno che non venga creata una regola del firewall per aprire il firewall per indirizzi IP specifici.</span><span class="sxs-lookup"><span data-stu-id="4011b-147">This firewall prevents external applications and tools from connecting to the server and any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> 

1.  <span data-ttu-id="4011b-148">Al termine della distribuzione, fare clic su **Tutte le risorse** nel menu a sinistra e digitare il nome **mypgserver-20170401** per la ricerca del server appena creato.</span><span class="sxs-lookup"><span data-stu-id="4011b-148">After the deployment completes, click **All Resources** from the left-hand menu and type in the name **mypgserver-20170401** to search for your newly created server.</span></span> <span data-ttu-id="4011b-149">Fare clic sul nome del server elencato nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="4011b-149">Click the server name listed in the search result.</span></span> <span data-ttu-id="4011b-150">Si apre la pagina **Panoramica** del server in cui vengono fornite le opzioni per una configurazione aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="4011b-150">The **Overview** page for your server opens and provides options for further configuration.</span></span>
 
 ![<span data-ttu-id="4011b-151">Database di Azure per PostgreSQL - Cercare il server</span><span class="sxs-lookup"><span data-stu-id="4011b-151">Azure Database for PostgreSQL - Search for server</span></span> ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

2.  <span data-ttu-id="4011b-152">Nel pannello del server, selezionare **Sicurezza connessione**.</span><span class="sxs-lookup"><span data-stu-id="4011b-152">In the server blade, select **Connection Security**.</span></span> 
3.  <span data-ttu-id="4011b-153">Fare clic nella casella di testo in **Nome regola** e aggiungere una nuova regola firewall alla whitelist dell'intervallo IP per la connettività.</span><span class="sxs-lookup"><span data-stu-id="4011b-153">Click in the text box under **Rule Name,** and add a new firewall rule to whitelist the IP range for connectivity.</span></span> <span data-ttu-id="4011b-154">Per questa esercitazione, consentire tutti gli indirizzi IP digitando **Rule Name = AllowAllIps**, **IP iniziale = 0.0.0.0** e **IP finale = 255.255.255.255** e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="4011b-154">For this tutorial, let's allow all IPs by typing in **Rule Name = AllowAllIps**, **Start IP = 0.0.0.0** and **End IP = 255.255.255.255** and then click **Save**.</span></span> <span data-ttu-id="4011b-155">È possibile impostare una regola firewall che copra un intervallo IP che sia in grado di connettersi dalla rete.</span><span class="sxs-lookup"><span data-stu-id="4011b-155">You can set a firewall rule that covers an IP range to be able to connect from your network.</span></span>
 
 ![Database di Azure per PostgreSQL - Creare una regola del firewall](./media/tutorial-design-database-using-azure-portal/5-firewall-2.png)

4.  <span data-ttu-id="4011b-157">Fare clic su **Salva** e quindi fare clic su **X** per chiudere la pagina **Sicurezza connessione**.</span><span class="sxs-lookup"><span data-stu-id="4011b-157">Click **Save** and then click the **X** to close the **Connections Security** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="4011b-158">Il server PostgreSQL Azure comunica sulla porta 5432.</span><span class="sxs-lookup"><span data-stu-id="4011b-158">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="4011b-159">Se si sta cercando di connettersi da una rete aziendale, il traffico in uscita sulla porta 5432 potrebbe non essere consentito dal firewall della rete.</span><span class="sxs-lookup"><span data-stu-id="4011b-159">If you are trying to connect from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="4011b-160">In tal caso, non sarà possibile connettersi al server del database SQL di Azure, a meno che il reparto IT non apra la porta 5432.</span><span class="sxs-lookup"><span data-stu-id="4011b-160">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 5432.</span></span>
  >


## <a name="get-the-connection-information"></a><span data-ttu-id="4011b-161">Ottenere le informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="4011b-161">Get the connection information</span></span>

<span data-ttu-id="4011b-162">Quando si crea il database di Azure per il server PostgreSQL, viene creato anche il database **postgres** predefinito.</span><span class="sxs-lookup"><span data-stu-id="4011b-162">When we created our Azure Database for PostgreSQL server, the default **postgres** database also gets created.</span></span> <span data-ttu-id="4011b-163">Per connettersi al server del database, è necessario fornire le informazioni sull'host e le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="4011b-163">To connect to your database server, you need to provide host information and access credentials.</span></span>

1. <span data-ttu-id="4011b-164">Nel menu a sinistra nel portale di Azure fare clic su **Tutte le risorse** e cercare il server appena creato, **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="4011b-164">From the left-hand menu in Azure portal, click **All resources** and search for the server you just created **mypgserver-20170401**.</span></span>

  ![<span data-ttu-id="4011b-165">Database di Azure per PostgreSQL - Cercare il server</span><span class="sxs-lookup"><span data-stu-id="4011b-165">Azure Database for PostgreSQL - Search for server</span></span> ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

3. <span data-ttu-id="4011b-166">Fare clic sul nome del server **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="4011b-166">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="4011b-167">Selezionare la pagina **Panoramica** del server.</span><span class="sxs-lookup"><span data-stu-id="4011b-167">Select the server's **Overview** page.</span></span> <span data-ttu-id="4011b-168">Annotare il **Nome server** e il **nome di accesso dell'amministratore del server**.</span><span class="sxs-lookup"><span data-stu-id="4011b-168">Make a note of the **Server name** and **Server admin login name**.</span></span>

 ![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/tutorial-design-database-using-azure-portal/6-server-name.png)


## <a name="connect-to-postgresql-database-using-psql-in-cloud-shell"></a><span data-ttu-id="4011b-170">Connettersi al database PostgreSQL tramite psql in Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="4011b-170">Connect to PostgreSQL database using psql in Cloud Shell</span></span>

<span data-ttu-id="4011b-171">Si usi ora l'utilità della riga di comando psql per connettersi al Database di Azure per il server PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="4011b-171">Let's now use the psql command-line utility to connect to the Azure Database for PostgreSQL server.</span></span> 
1. <span data-ttu-id="4011b-172">Avviare Azure Cloud Shell tramite l'icona del terminale nel riquadro di spostamento in alto.</span><span class="sxs-lookup"><span data-stu-id="4011b-172">Launch the Azure Cloud Shell via the terminal icon on the top navigation pane.</span></span>

   ![Database di Azure per PostgreSQL - Icona del terminale di Azure Cloud Shell](./media/tutorial-design-database-using-azure-portal/7-cloud-shell.png)

2. <span data-ttu-id="4011b-174">Azure Cloud Shell si apre nel browser, consentendo di digitare i comandi bash.</span><span class="sxs-lookup"><span data-stu-id="4011b-174">The Azure Cloud Shell opens in your browser, enabling you to type bash commands.</span></span>

   ![Database di Azure per PostgreSQL - Prompt Bash di Azure Cloud Shell](./media/tutorial-design-database-using-azure-portal/8-bash.png)

3. <span data-ttu-id="4011b-176">Al prompt di Cloud Shell connettersi al database di Azure per il server PostgreSQL usando i comandi psql.</span><span class="sxs-lookup"><span data-stu-id="4011b-176">At the Cloud Shell prompt, connect to your Azure Database for PostgreSQL server using the psql commands.</span></span> <span data-ttu-id="4011b-177">Il formato seguente è usato per connettersi a un Database di Azure per il server PostgreSQL con l'utilità [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html):</span><span class="sxs-lookup"><span data-stu-id="4011b-177">The following format is used to connect to an Azure Database for PostgreSQL server with the [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility:</span></span>
   ```bash
   psql --host=<myserver> --port=<port> --username=<server admin login> --dbname=<database name>
   ```

   <span data-ttu-id="4011b-178">Ad esempio, il comando seguente consente di connettersi al database predefinito denominato **postgres** nel server PostgreSQL **mypgserver-20170401.postgres.database.azure.com** usando le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="4011b-178">For example, the following command connects to the default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="4011b-179">Immettere la password dell'amministratore del server quando viene richiesto.</span><span class="sxs-lookup"><span data-stu-id="4011b-179">Enter your server admin password when prompted.</span></span>

   ```bash
   psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
   ```

## <a name="create-a-new-database"></a><span data-ttu-id="4011b-180">Creare un nuovo database</span><span class="sxs-lookup"><span data-stu-id="4011b-180">Create a New Database</span></span>
<span data-ttu-id="4011b-181">Dopo aver eseguito la connessione al server, creare un database vuoto al prompt.</span><span class="sxs-lookup"><span data-stu-id="4011b-181">Once you're connected to the server, create a blank database at the prompt.</span></span>
```bash
CREATE DATABASE mypgsqldb;
```

<span data-ttu-id="4011b-182">Nel prompt, eseguire il comando seguente per cambiare la connessione nel database appena creato **mypgsqldb**.</span><span class="sxs-lookup"><span data-stu-id="4011b-182">At the prompt, execute the following command to switch connection to the newly created database **mypgsqldb**.</span></span>
```bash
\c mypgsqldb
```
## <a name="create-tables-in-the-database"></a><span data-ttu-id="4011b-183">Creare tabelle nel database</span><span class="sxs-lookup"><span data-stu-id="4011b-183">Create tables in the database</span></span>
<span data-ttu-id="4011b-184">Dopo aver appreso come connettersi al Database di Azure per PostgreSQL, si può passare al completamento di alcune attività di base.</span><span class="sxs-lookup"><span data-stu-id="4011b-184">Now that you know how to connect to the Azure Database for PostgreSQL, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="4011b-185">In primo luogo, è possibile creare una tabella e caricarla con alcuni dati.</span><span class="sxs-lookup"><span data-stu-id="4011b-185">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="4011b-186">Creare una tabella che tiene traccia delle informazioni riguardanti l'inventario.</span><span class="sxs-lookup"><span data-stu-id="4011b-186">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="4011b-187">È possibile visualizzare ora la tabella appena creata nell'elenco di tabelle digitando:</span><span class="sxs-lookup"><span data-stu-id="4011b-187">You can see the newly created table in the list of tabvles now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="4011b-188">Caricare i dati nelle tabelle</span><span class="sxs-lookup"><span data-stu-id="4011b-188">Load data into the tables</span></span>
<span data-ttu-id="4011b-189">Ora che abbiamo una tabella, possiamo inserire alcuni dati al suo interno.</span><span class="sxs-lookup"><span data-stu-id="4011b-189">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="4011b-190">Nella finestra del prompt dei comandi aperta, eseguire la query seguente per inserire alcune righe di dati</span><span class="sxs-lookup"><span data-stu-id="4011b-190">At the open command prompt window, run the following query to insert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="4011b-191">A questo punto, sono presenti due righe di dati di esempio nella tabella creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4011b-191">You have now two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="4011b-192">Eseguire una query e aggiornare i dati nelle tabelle</span><span class="sxs-lookup"><span data-stu-id="4011b-192">Query and update the data in the tables</span></span>
<span data-ttu-id="4011b-193">Eseguire la query seguente per recuperare informazioni dalla tabella del database.</span><span class="sxs-lookup"><span data-stu-id="4011b-193">Execute the following query to retrieve information from the database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="4011b-194">Si possono anche aggiornare i dati nelle tabelle</span><span class="sxs-lookup"><span data-stu-id="4011b-194">You can also update the data in the tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="4011b-195">La riga viene aggiornata di conseguenza quando si recuperano dati.</span><span class="sxs-lookup"><span data-stu-id="4011b-195">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-data-to-a-previous-point-in-time"></a><span data-ttu-id="4011b-196">Ripristinare i dati a un punto precedente nel tempo</span><span class="sxs-lookup"><span data-stu-id="4011b-196">Restore data to a previous point in time</span></span>
<span data-ttu-id="4011b-197">Si supponga di aver eliminato accidentalmente questa tabella.</span><span class="sxs-lookup"><span data-stu-id="4011b-197">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="4011b-198">Questa situazione non è facile da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="4011b-198">This situation is something you cannot easily recover from.</span></span> <span data-ttu-id="4011b-199">Il Database di Azure per PostgreSQL consente di tornare in qualsiasi punto nel tempo (negli ultimi 7 giorni (Basic) e 35 giorni (Standard)) e ripristinare questo punto nel tempo in un nuovo server.</span><span class="sxs-lookup"><span data-stu-id="4011b-199">Azure Database for PostgreSQL allows you to go back to any point-in-time (in the last up to 7 days (Basic) and 35 days (Standard)) and restore this point-in-time to a new server.</span></span> <span data-ttu-id="4011b-200">È possibile usare questo nuovo server per ripristinare i dati eliminati.</span><span class="sxs-lookup"><span data-stu-id="4011b-200">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="4011b-201">La procedura seguente consente di ripristinare il server di esempio in un punto precedente all'aggiunta della tabella.</span><span class="sxs-lookup"><span data-stu-id="4011b-201">The following steps restore the sample server to a point before the table was added.</span></span>

1.  <span data-ttu-id="4011b-202">Nel Database di Azure per la pagina PostgreSQL del server, fare clic su **Ripristina** sulla barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="4011b-202">On the Azure Database for PostgreSQL page for your server, click **Restore** on the toolbar.</span></span> <span data-ttu-id="4011b-203">Si apre la pagina **Ripristina** .</span><span class="sxs-lookup"><span data-stu-id="4011b-203">The **Restore** page opens.</span></span>
  <span data-ttu-id="4011b-204">![Portale di Azure - Opzioni del modulo di ripristino](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)</span><span class="sxs-lookup"><span data-stu-id="4011b-204">![Azure portal - Restore form options](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)</span></span>
2.  <span data-ttu-id="4011b-205">Compilare il modulo **Ripristina** con le informazioni obbligatorie:</span><span class="sxs-lookup"><span data-stu-id="4011b-205">Fill out the **Restore** form with the required information:</span></span>

  ![Portale di Azure - Opzioni del modulo di ripristino](./media/tutorial-design-database-using-azure-portal/10-azure-portal-restore.png)
  - <span data-ttu-id="4011b-207">**Punto di ripristino**: selezionare un punto nel tempo precedente alla modifica del server</span><span class="sxs-lookup"><span data-stu-id="4011b-207">**Restore point**: Select a point-in-time that occurs before the server was changed</span></span>
  - <span data-ttu-id="4011b-208">**Server di destinazione**: fornire un nuovo nome del server che si desidera ripristinare</span><span class="sxs-lookup"><span data-stu-id="4011b-208">**Target server**: Provide a new server name you want to restore to</span></span>
  - <span data-ttu-id="4011b-209">**Posizione**: non è possibile selezionare l'area, per impostazione predefinita è la stessa del server di origine</span><span class="sxs-lookup"><span data-stu-id="4011b-209">**Location**: You cannot select the region, by default it is same as the source server</span></span>
  - <span data-ttu-id="4011b-210">**Piano tariffario**: non è possibile modificare questo valore quando si ripristina un server.</span><span class="sxs-lookup"><span data-stu-id="4011b-210">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="4011b-211">È uguale al server di origine.</span><span class="sxs-lookup"><span data-stu-id="4011b-211">It is same as the source server.</span></span> 
3.  <span data-ttu-id="4011b-212">Fare clic su **OK** per ripristinare il server per [ripristinare in un punto nel tempo](./howto-restore-server-portal.md) precedente all'eliminazione delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="4011b-212">Click **OK** to restore the server to [restore to a point-in-time](./howto-restore-server-portal.md) before the tables was deleted.</span></span> <span data-ttu-id="4011b-213">Il ripristino di un server in un altro punto nel tempo crea un duplicato del nuovo server come il server originale nel punto nel tempo specificato, purché sia entro il periodo di conservazione per il [livello di servizio](./concepts-service-tiers.md) applicato.</span><span class="sxs-lookup"><span data-stu-id="4011b-213">Restoring a server to a different point in time creates a duplicate new server as the original server as of the point in time you specify, provided that it is within the retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4011b-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4011b-214">Next Steps</span></span>
<span data-ttu-id="4011b-215">In questa esercitazione si apprenderà come usare il portale di Azure e altre utilità per:</span><span class="sxs-lookup"><span data-stu-id="4011b-215">In this tutorial, you learned how to use the Azure portal and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="4011b-216">Creare un database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="4011b-216">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="4011b-217">Configurare il firewall del server</span><span class="sxs-lookup"><span data-stu-id="4011b-217">Configure the server firewall</span></span>
> * <span data-ttu-id="4011b-218">Usare l'utilità [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) per creare un database</span><span class="sxs-lookup"><span data-stu-id="4011b-218">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="4011b-219">Caricare dati di esempio</span><span class="sxs-lookup"><span data-stu-id="4011b-219">Load sample data</span></span>
> * <span data-ttu-id="4011b-220">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="4011b-220">Query data</span></span>
> * <span data-ttu-id="4011b-221">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="4011b-221">Update data</span></span>
> * <span data-ttu-id="4011b-222">Ripristinare i dati</span><span class="sxs-lookup"><span data-stu-id="4011b-222">Restore data</span></span>

<span data-ttu-id="4011b-223">Successivamente, per informazioni su come usare l'Interfaccia della riga di comando di Azure per eseguire attività simili, esaminare questa esercitazione: [Progettare il primo Database di Azure per PostgreSQL tramite l'Interfaccia della riga di comando di Azure](tutorial-design-database-using-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="4011b-223">Next, learn how to use Azure CLI to do similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using Azure CLI](tutorial-design-database-using-azure-cli.md)</span></span>
