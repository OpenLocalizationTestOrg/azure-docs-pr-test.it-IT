---
title: Progettare il primo Database di Azure per il database MySQL - Portale di Azure | Microsoft Docs
description: In questa esercitazione viene illustrato come creare e gestire il database di Azure per il server e il database MySQL tramite il portale di Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: c7b76cacbdc4e483353f64cc4e50c974867bb5b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="dc9e5-103">Progettare il primo database di Azure per il database MySQL</span><span class="sxs-lookup"><span data-stu-id="dc9e5-103">Design your first Azure Database for MySQL database</span></span>
<span data-ttu-id="dc9e5-104">Il database di Azure per MySQL è un servizio gestito che consente di eseguire, gestire e scalare dei database MySQL a disponibilità elevata nel cloud.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-104">Azure Database for MySQL is a managed service that enables you to run, manage, and scale highly available MySQL databases in the cloud.</span></span> <span data-ttu-id="dc9e5-105">Tramite il portale di Azure, è possibile gestire facilmente il server e progettare un database.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-105">Using the Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="dc9e5-106">In questa esercitazione si userà il portale di Azure per imparare a:</span><span class="sxs-lookup"><span data-stu-id="dc9e5-106">In this tutorial, you use the Azure portal to learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dc9e5-107">Creare un database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="dc9e5-107">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="dc9e5-108">Configurare il firewall del server</span><span class="sxs-lookup"><span data-stu-id="dc9e5-108">Configure the server firewall</span></span>
> * <span data-ttu-id="dc9e5-109">Usare lo strumento da riga di comando mysql per creare un database</span><span class="sxs-lookup"><span data-stu-id="dc9e5-109">Use mysql command-line tool to create a database</span></span>
> * <span data-ttu-id="dc9e5-110">Caricare dati di esempio</span><span class="sxs-lookup"><span data-stu-id="dc9e5-110">Load sample data</span></span>
> * <span data-ttu-id="dc9e5-111">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="dc9e5-111">Query data</span></span>
> * <span data-ttu-id="dc9e5-112">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="dc9e5-112">Update data</span></span>
> * <span data-ttu-id="dc9e5-113">Ripristinare i dati</span><span class="sxs-lookup"><span data-stu-id="dc9e5-113">Restore data</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="dc9e5-114">Accedere al portale di Azure</span><span class="sxs-lookup"><span data-stu-id="dc9e5-114">Sign in to the Azure portal</span></span>
<span data-ttu-id="dc9e5-115">Aprire il Web browser preferito e visitare il [portale di Microsoft Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="dc9e5-115">Open your favorite web browser, and visit the [Microsoft Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="dc9e5-116">Immettere le credenziali per accedere al portale.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-116">Enter your credentials to sign in to the portal.</span></span> <span data-ttu-id="dc9e5-117">La visualizzazione predefinita è il dashboard del servizio.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-117">The default view is your service dashboard.</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="dc9e5-118">Creare un database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="dc9e5-118">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="dc9e5-119">Verrà creato un database di Azure per MySQL con un set definito di [risorse di calcolo e di archiviazione](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="dc9e5-119">An Azure Database for MySQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="dc9e5-120">Il server viene creato all'interno di un [gruppo di risorse di Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="dc9e5-120">The server is created within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

1. <span data-ttu-id="dc9e5-121">Passare a **database** > **Database di Azure per MySQL**.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-121">Navigate to **Databases** > **Azure Database for MySQL**.</span></span> <span data-ttu-id="dc9e5-122">Se non si trova MySQL Server nella categoria **Database**, fare clic su **Visualizza tutto** per mostrare tutti i servizi di database disponibili.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-122">If you cannot find MySQL Server under **Databases** category, click **See all** to show all available database services.</span></span> <span data-ttu-id="dc9e5-123">È possibile anche digitare **Database di Azure per MySQL** nella casella di ricerca per trovare rapidamente il servizio.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-123">You can also type **Azure Database for MySQL** in the search box to quickly find the service.</span></span>
<span data-ttu-id="dc9e5-124">![2-1 Passare a MySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span><span class="sxs-lookup"><span data-stu-id="dc9e5-124">![2-1 Navigate to MySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span></span>

2. <span data-ttu-id="dc9e5-125">Fare clic sul riquadro **Database di Azure per MySQL** e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-125">Click **Azure Database for MySQL** tile, and then click **Create**.</span></span>

<span data-ttu-id="dc9e5-126">Nel nostro esempio, compilare il modulo Database di Azure per MySQL con le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="dc9e5-126">In our example, fill out the Azure Database for MySQL form with the following information:</span></span>

| <span data-ttu-id="dc9e5-127">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="dc9e5-127">**Setting**</span></span> | <span data-ttu-id="dc9e5-128">**Valore consigliato**</span><span class="sxs-lookup"><span data-stu-id="dc9e5-128">**Suggested value**</span></span> | <span data-ttu-id="dc9e5-129">**Descrizione campo**</span><span class="sxs-lookup"><span data-stu-id="dc9e5-129">**Field Description**</span></span> |
|---|---|---|
| <span data-ttu-id="dc9e5-130">*Server name* (Nome server)</span><span class="sxs-lookup"><span data-stu-id="dc9e5-130">*Server name*</span></span> | <span data-ttu-id="dc9e5-131">myserver4demo</span><span class="sxs-lookup"><span data-stu-id="dc9e5-131">myserver4demo</span></span>  | <span data-ttu-id="dc9e5-132">Il nome del server deve essere univoco a livello globale.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-132">Server name has to be globally unique.</span></span> |
| <span data-ttu-id="dc9e5-133">*Sottoscrizione*</span><span class="sxs-lookup"><span data-stu-id="dc9e5-133">*Subscription*</span></span> | <span data-ttu-id="dc9e5-134">mysubscription</span><span class="sxs-lookup"><span data-stu-id="dc9e5-134">mysubscription</span></span> | <span data-ttu-id="dc9e5-135">Selezionare la sottoscrizione dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-135">Select your subscription from the drop-down.</span></span> |
| <span data-ttu-id="dc9e5-136">*Gruppo di risorse*</span><span class="sxs-lookup"><span data-stu-id="dc9e5-136">*Resource group*</span></span> | <span data-ttu-id="dc9e5-137">myresourcegroup</span><span class="sxs-lookup"><span data-stu-id="dc9e5-137">myresourcegroup</span></span> | <span data-ttu-id="dc9e5-138">Creare un gruppo di risorse o usarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-138">Create a resource group or use an existing one.</span></span> |
| <span data-ttu-id="dc9e5-139">*Nome di accesso amministratore server*</span><span class="sxs-lookup"><span data-stu-id="dc9e5-139">*Server admin login*</span></span> | <span data-ttu-id="dc9e5-140">myadmin</span><span class="sxs-lookup"><span data-stu-id="dc9e5-140">myadmin</span></span> | <span data-ttu-id="dc9e5-141">Configurare il nome dell'account amministratore.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-141">Setup admin account name.</span></span> |
| <span data-ttu-id="dc9e5-142">*Password*</span><span class="sxs-lookup"><span data-stu-id="dc9e5-142">*Password*</span></span> |  | <span data-ttu-id="dc9e5-143">Impostare una password complessa per l'account amministratore.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-143">Set a strong admin account password.</span></span> |
| <span data-ttu-id="dc9e5-144">*Conferma password*</span><span class="sxs-lookup"><span data-stu-id="dc9e5-144">*Confirm password*</span></span> |  | <span data-ttu-id="dc9e5-145">Confermare la password dell'account amministratore.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-145">Confirm the admin account password.</span></span> |
| <span data-ttu-id="dc9e5-146">*Posizione*</span><span class="sxs-lookup"><span data-stu-id="dc9e5-146">*Location*</span></span> |  | <span data-ttu-id="dc9e5-147">Selezionare un'area disponibile.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-147">Select an available region.</span></span> |
| <span data-ttu-id="dc9e5-148">*Versione*</span><span class="sxs-lookup"><span data-stu-id="dc9e5-148">*Version*</span></span> | <span data-ttu-id="dc9e5-149">5.7</span><span class="sxs-lookup"><span data-stu-id="dc9e5-149">5.7</span></span> | <span data-ttu-id="dc9e5-150">Scegliere la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-150">Choose the latest version.</span></span> |
| <span data-ttu-id="dc9e5-151">*Configura prestazioni*</span><span class="sxs-lookup"><span data-stu-id="dc9e5-151">*Configure performance*</span></span> | <span data-ttu-id="dc9e5-152">Base con 50 unità di calcolo, 50 GB</span><span class="sxs-lookup"><span data-stu-id="dc9e5-152">Basic, 50 compute units, 50 GB</span></span>  | <span data-ttu-id="dc9e5-153">Scegliere **Piano tariffario**, **Unità di calcolo**, **Archiviazione (GB)** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-153">Choose **Pricing tier**, **Compute Units**, **Storage (GB)**, and then click **OK**.</span></span> |
| <span data-ttu-id="dc9e5-154">*Aggiungi al dashboard*</span><span class="sxs-lookup"><span data-stu-id="dc9e5-154">*Pin to Dashboard*</span></span> | <span data-ttu-id="dc9e5-155">Controllo</span><span class="sxs-lookup"><span data-stu-id="dc9e5-155">Check</span></span> | <span data-ttu-id="dc9e5-156">È consigliabile selezionare questa casella per trovare facilmente il server in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-156">Recommended to check this box so you may find the server easily later on</span></span> |
<span data-ttu-id="dc9e5-157">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-157">Then, click **Create**.</span></span> <span data-ttu-id="dc9e5-158">Dopo pochi minuti, un nuovo database di Azure per il server MySQL sarà in esecuzione nel cloud.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-158">In a minute or two, a new Azure Database for MySQL server is running in the cloud.</span></span> <span data-ttu-id="dc9e5-159">È possibile fare clic sul pulsante **Notifiche** sulla barra degli strumenti per monitorare il processo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-159">You can click **Notifications** button on the toolbar to monitor the deployment process.</span></span>

## <a name="configure-firewall"></a><span data-ttu-id="dc9e5-160">Configurare il firewall</span><span class="sxs-lookup"><span data-stu-id="dc9e5-160">Configure firewall</span></span>
<span data-ttu-id="dc9e5-161">I database di Azure per MySQL sono protetti da un firewall.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-161">Azure Databases for MySQL are protected by a firewall.</span></span> <span data-ttu-id="dc9e5-162">Per impostazione predefinita, vengono rifiutate tutte le connessioni al server e ai database all'interno del server.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-162">By default, all connections to the server and the databases inside the server are rejected.</span></span> <span data-ttu-id="dc9e5-163">Prima di connettersi per la prima volta al database di Azure per MySQL, configurare il firewall per aggiungere l'indirizzo IP della rete pubblica del computer client (o un intervallo di indirizzi IP).</span><span class="sxs-lookup"><span data-stu-id="dc9e5-163">Before connecting to Azure Database for MySQL for the first time, configure the firewall to add the client machine's public network IP address (or IP address range).</span></span>

1. <span data-ttu-id="dc9e5-164">Fare clic sul server appena creato e quindi fare clic su **Sicurezza connessione**.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-164">Click your newly created server, and then click **Connection security**.</span></span>
   <span data-ttu-id="dc9e5-165">![3-1 Sicurezza della connessione](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span><span class="sxs-lookup"><span data-stu-id="dc9e5-165">![3-1 Connection security](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span></span>
2. <span data-ttu-id="dc9e5-166">È possibile scegliere **Aggiungi indirizzo IP corrente** o configurare le regole del firewall qui.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-166">You can **Add My IP**, or configure firewall rules here.</span></span> <span data-ttu-id="dc9e5-167">Ricordarsi di fare clic su **Salva** dopo aver creato le regole.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-167">Remember to click **Save** after you have created the rules.</span></span>
<span data-ttu-id="dc9e5-168">È ora possibile connettersi al server usando lo strumento da riga di comando mysql o lo strumento MySQL Workbench GUI.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-168">You can now connect to the server using mysql command-line tool or MySQL Workbench GUI tool.</span></span>

> [!TIP]
> <span data-ttu-id="dc9e5-169">Il Database di Azure per il server MySQL comunica sulla porta 3306.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-169">Azure Database for MySQL server communicates over port 3306.</span></span> <span data-ttu-id="dc9e5-170">Se si sta tentando di connettersi da una rete aziendale, il traffico in uscita attraverso la porta 3306 potrebbe non essere autorizzato dal firewall della rete.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-170">If you are trying to connect from within a corporate network, outbound traffic over port 3306 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="dc9e5-171">In questo caso non è possibile connettersi al server MySQL di Azure, a meno che il reparto IT non apra la porta 3306.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-171">If so, you cannot connect to Azure MySQL server unless your IT department opens port 3306.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="dc9e5-172">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="dc9e5-172">Get connection information</span></span>
<span data-ttu-id="dc9e5-173">Ottenere il **Nome server** completo e il **Nome di accesso dell'amministratore server** per il database di Azure per il server MySQL dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-173">Get the fully qualified **Server name** and **Server admin login name** for your Azure Database for MySQL server from the Azure portal.</span></span> <span data-ttu-id="dc9e5-174">Usare il nome completo del server per connettersi al server tramite lo strumento da riga di comando mysql.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-174">You use the fully qualified server name to connect to your server using mysql command-line tool.</span></span> 

1. <span data-ttu-id="dc9e5-175">Nel [portale di Azure](https://portal.azure.com/) fare clic su **Tutte le risorse** nel menu a sinistra, digitare il nome e cercare il database di Azure per il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-175">In [Azure portal](https://portal.azure.com/), click **All resources** from the left-hand menu, type the name, and search for your Azure Database for MySQL server.</span></span> <span data-ttu-id="dc9e5-176">Selezionare il nome del server per visualizzare i dettagli.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-176">Select the server name to view the details.</span></span>

2. <span data-ttu-id="dc9e5-177">Nell'intestazione Impostazioni fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-177">Under the Settings heading, click **Properties**.</span></span> <span data-ttu-id="dc9e5-178">Prendere nota del **NOME SERVER** e del **NOME DI ACCESSO DELL'AMMINISTRATORE SERVER**.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-178">Note down **SERVER NAME** and **SERVER ADMIN LOGIN NAME**.</span></span> <span data-ttu-id="dc9e5-179">È possibile fare clic sul pulsante Copia accanto a ogni campo per copiarlo negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-179">You may click the copy button next to each field to copy to the clipboard.</span></span>
   <span data-ttu-id="dc9e5-180">![4-2 Proprietà del server](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span><span class="sxs-lookup"><span data-stu-id="dc9e5-180">![4-2 server properties](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span></span>

<span data-ttu-id="dc9e5-181">In questo esempio il nome del server è *myserver4demo.mysql.database.azure.com* e l'account di accesso dell'amministratore del server è *myadmin@myserver4demo*.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-181">In this example, the server name is *myserver4demo.mysql.database.azure.com*, and the server admin login is *myadmin@myserver4demo*.</span></span>

## <a name="connect-to-the-server-using-mysql"></a><span data-ttu-id="dc9e5-182">Connettersi al server usando mysql</span><span class="sxs-lookup"><span data-stu-id="dc9e5-182">Connect to the server using mysql</span></span>
<span data-ttu-id="dc9e5-183">Usare lo [strumento da riga di comando mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) per stabilire una connessione al database di Azure per il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-183">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span></span> <span data-ttu-id="dc9e5-184">È possibile eseguire lo strumento da riga di comando mysql nel browser usando Azure Cloud Shell o avviarlo dal computer tramite gli strumenti mysql installati localmente.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-184">You can run the mysql command-line tool from the Azure Cloud Shell in the browser or from your own machine using mysql tools installed locally.</span></span> <span data-ttu-id="dc9e5-185">Per avviare Azure Cloud Shell, fare clic sul pulsante `Try It` in un blocco di codice in questo articolo oppure visitare il portale di Azure e fare clic sull'icona `>_` nella barra degli strumenti in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-185">To launch the Azure Cloud Shell, click the `Try It` button on a code block in this article, or visit the Azure portal and click the `>_` icon in the top right toolbar.</span></span> 

<span data-ttu-id="dc9e5-186">Digitare il comando per la connessione:</span><span class="sxs-lookup"><span data-stu-id="dc9e5-186">Type the command to connect:</span></span>
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="dc9e5-187">Creazione di un database vuoto</span><span class="sxs-lookup"><span data-stu-id="dc9e5-187">Create a blank database</span></span>
<span data-ttu-id="dc9e5-188">Dopo aver eseguito la connessione al server, creare un database vuoto con cui lavorare.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-188">Once you’re connected to the server, create a blank database to work with.</span></span>
```sql
CREATE DATABASE mysampledb;
```

<span data-ttu-id="dc9e5-189">Nel prompt eseguire il comando seguente per cambiare la connessione nel database appena creato:</span><span class="sxs-lookup"><span data-stu-id="dc9e5-189">At the prompt, run the following command to switch connection to this newly created database:</span></span>
```sql
USE mysampledb;
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="dc9e5-190">Creare tabelle nel database</span><span class="sxs-lookup"><span data-stu-id="dc9e5-190">Create tables in the database</span></span>
<span data-ttu-id="dc9e5-191">Dopo aver appreso come connettersi al database di Azure per il database MySQL, si può passare al completamento di alcune attività di base.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-191">Now that you know how to connect to the Azure Database for MySQL database, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="dc9e5-192">In primo luogo, è possibile creare una tabella e caricarla con alcuni dati.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-192">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="dc9e5-193">Creare una tabella che contenga le informazioni riguardanti l'inventario.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-193">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="dc9e5-194">Caricare i dati nelle tabelle</span><span class="sxs-lookup"><span data-stu-id="dc9e5-194">Load data into the tables</span></span>
<span data-ttu-id="dc9e5-195">Ora che abbiamo una tabella, possiamo inserire alcuni dati al suo interno.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-195">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="dc9e5-196">Nella finestra del prompt dei comandi aperta, eseguire la query seguente per inserire alcune righe di dati.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-196">At the open command prompt window, run the following query to insert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="dc9e5-197">A questo punto, ci sono due righe di dati di esempio nella tabella creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-197">Now you have two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="dc9e5-198">Eseguire una query e aggiornare i dati nelle tabelle</span><span class="sxs-lookup"><span data-stu-id="dc9e5-198">Query and update the data in the tables</span></span>
<span data-ttu-id="dc9e5-199">Eseguire la query seguente per recuperare informazioni dalla tabella del database.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-199">Execute the following query to retrieve information from the database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="dc9e5-200">Si possono anche aggiornare query e aggiornare i dati nelle tabelle.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-200">You can also update the data in the tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="dc9e5-201">La riga viene aggiornata di conseguenza quando si recuperano dati.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-201">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="dc9e5-202">Ripristinare un database a un momento precedente</span><span class="sxs-lookup"><span data-stu-id="dc9e5-202">Restore a database to a previous point in time</span></span>
<span data-ttu-id="dc9e5-203">Si supponga di avere eliminato un'importante tabella di database e di non poter ripristinare i dati facilmente.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-203">Imagine you have accidentally deleted an important database table, and cannot recover the data easily.</span></span> <span data-ttu-id="dc9e5-204">Il servizio Database di Azure per MySQL consente di ripristinare il server a un punto nel tempo, creando una copia dei database in un nuovo server.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-204">Azure Database for MySQL allows you to restore the server to a point in time, creating a copy of the databases into new server.</span></span> <span data-ttu-id="dc9e5-205">È possibile usare questo nuovo server per ripristinare i dati eliminati.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-205">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="dc9e5-206">La procedura seguente consente di ripristinare il server di esempio in un punto precedente all'aggiunta della tabella.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-206">The following steps restore the sample server to a point before the table was added.</span></span>

1. <span data-ttu-id="dc9e5-207">Nel portale di Azure individuare il database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-207">In the Azure portal, locate your Azure Database for MySQL.</span></span> <span data-ttu-id="dc9e5-208">Nella pagina **Panoramica** fare clic su **Ripristina** nella barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-208">On the **Overview** page, click **Restore** on the toolbar.</span></span> <span data-ttu-id="dc9e5-209">Verrà visualizzata la pagina Ripristina.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-209">The Restore page opens.</span></span>

   ![10-1 Ripristinare un database](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. <span data-ttu-id="dc9e5-211">Compilare il modulo **Ripristina** con le informazioni richieste.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-211">Fill out the **Restore** form with the required information.</span></span>
   
   ![10-2 Modulo di ripristino](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - <span data-ttu-id="dc9e5-213">**Punto di ripristino**: selezionare un punto nel tempo a cui si vuole ripristinare, entro l'intervallo di tempo elencato.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-213">**Restore point**: Select a point-in-time that you want to restore to, within the timeframe listed.</span></span> <span data-ttu-id="dc9e5-214">Assicurarsi di convertire il fuso orario locale in ora UTC.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-214">Make sure to convert your local timezone to UTC.</span></span>
   - <span data-ttu-id="dc9e5-215">**Ripristina nel nuovo server**: fornire il nome del nuovo server in cui si vuole memorizzare il database da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-215">**Restore to new server**: Provide a new server name you want to restore to.</span></span>
   - <span data-ttu-id="dc9e5-216">**Posizione**: l'area è identica a quella del server di origine e non può essere modificata.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-216">**Location**: The region is same as the source server, and cannot be changed.</span></span>
   - <span data-ttu-id="dc9e5-217">**Piano tariffario**: il piano tariffario è identico a quello del server di origine e non può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-217">**Pricing tier**: The pricing tier is the same as the source server, and cannot be changed.</span></span>
   
3. <span data-ttu-id="dc9e5-218">Fare clic su **OK** per ripristinare il server da [ripristinare in un punto nel tempo](./howto-restore-server-portal.md) precedente all'eliminazione della tabella.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-218">Click **OK** to restore the server to [restore to a point in time](./howto-restore-server-portal.md) before the table was deleted.</span></span> <span data-ttu-id="dc9e5-219">Il ripristino di un server crea una nuova copia del server, a partire dal momento nel tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="dc9e5-219">Restoring a server creates a new copy of the server, as of the point in time you specify.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="dc9e5-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dc9e5-220">Next steps</span></span>
<span data-ttu-id="dc9e5-221">In questa esercitazione si userà il portale di Azure per imparare a:</span><span class="sxs-lookup"><span data-stu-id="dc9e5-221">In this tutorial, you use the Azure portal to learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dc9e5-222">Creare un database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="dc9e5-222">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="dc9e5-223">Configurare il firewall del server</span><span class="sxs-lookup"><span data-stu-id="dc9e5-223">Configure the server firewall</span></span>
> * <span data-ttu-id="dc9e5-224">Usare lo strumento da riga di comando mysql per creare un database</span><span class="sxs-lookup"><span data-stu-id="dc9e5-224">Use mysql command-line tool to create a database</span></span>
> * <span data-ttu-id="dc9e5-225">Caricare dati di esempio</span><span class="sxs-lookup"><span data-stu-id="dc9e5-225">Load sample data</span></span>
> * <span data-ttu-id="dc9e5-226">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="dc9e5-226">Query data</span></span>
> * <span data-ttu-id="dc9e5-227">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="dc9e5-227">Update data</span></span>
> * <span data-ttu-id="dc9e5-228">Ripristinare i dati</span><span class="sxs-lookup"><span data-stu-id="dc9e5-228">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dc9e5-229">Come connettere le applicazioni a Database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="dc9e5-229">How to connect applications to Azure Database for MySQL</span></span>](./howto-connection-string.md)
