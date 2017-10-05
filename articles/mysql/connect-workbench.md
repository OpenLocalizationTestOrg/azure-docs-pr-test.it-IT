---
title: Connettersi al database di Azure per MySQL da MySQL Workbench | Microsoft Docs
description: Questa guida introduttiva illustra come usare MySQL Workbench per connettersi ed eseguire query sui dati dal database di Azure per MySQL.
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: 20a1f31ce42abb924504c4008f85420fc49aec89
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-to-connect-and-query-data"></a><span data-ttu-id="65917-103">Database di Azure per MySQL: usare MySQL Workbench per connettersi ed eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="65917-103">Azure Database for MySQL: Use MySQL Workbench to connect and query data</span></span>
<span data-ttu-id="65917-104">Questa guida introduttiva illustra come connettersi a un database di Azure per MySQL usando un'applicazione MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="65917-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using the MySQL Workbench application.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="65917-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="65917-105">Prerequisites</span></span>
<span data-ttu-id="65917-106">Questa guida introduttiva usa le risorse create in una delle guide seguenti come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="65917-106">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="65917-107">Creare un database di Azure per il server MySQL tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="65917-107">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="65917-108">Creare un database di Azure per il server MySQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="65917-108">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a><span data-ttu-id="65917-109">Installare MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="65917-109">Install MySQL Workbench</span></span>
<span data-ttu-id="65917-110">Scaricare e installare MySQL Workbench nel computer dal [sito Web di MySQL](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="65917-110">Download and install MySQL Workbench on your computer from [the MySQL website](https://dev.mysql.com/downloads/workbench/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="65917-111">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="65917-111">Get connection information</span></span>
<span data-ttu-id="65917-112">Ottenere le informazioni di connessione necessarie per connettersi al database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="65917-112">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="65917-113">Sono necessari il nome del server completo e le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="65917-113">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="65917-114">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="65917-114">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="65917-115">Nel menu a sinistra nel portale di Azure fare clic su **Tutte le risorse** e cercare il server creato, ad esempio **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="65917-115">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **myserver4demo**.</span></span>

3. <span data-ttu-id="65917-116">Fare clic sul nome del server.</span><span class="sxs-lookup"><span data-stu-id="65917-116">Click the server name.</span></span>

4. <span data-ttu-id="65917-117">Selezionare la pagina **Proprietà** del server.</span><span class="sxs-lookup"><span data-stu-id="65917-117">Select the server's **Properties** page.</span></span> <span data-ttu-id="65917-118">Annotare il **Nome server** e il **nome di accesso dell'amministratore del server**.</span><span class="sxs-lookup"><span data-stu-id="65917-118">Make a note of the **Server name** and **Server admin login name**.</span></span>

 ![Nome del server del database di Azure per MySQL](./media/connect-workbench/1-server-properties-name-login.png)
 
5. <span data-ttu-id="65917-120">Se si dimenticano le informazioni di accesso per il server, passare alla pagina **Panoramica** per visualizzare il nome di accesso dell'amministratore del server e, se necessario, reimpostare la password.</span><span class="sxs-lookup"><span data-stu-id="65917-120">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-to-the-server-using-mysql-workbench"></a><span data-ttu-id="65917-121">Connettersi al server con MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="65917-121">Connect to the server using MySQL Workbench</span></span> 
<span data-ttu-id="65917-122">Per connettersi al server MySQL di Azure con lo strumento dell'interfaccia utente grafica MySQL Workbench:</span><span class="sxs-lookup"><span data-stu-id="65917-122">To connect to Azure MySQL server using the GUI tool MySQL Workbench:</span></span>

1.  <span data-ttu-id="65917-123">Avviare l'applicazione MySQL Workbench nel computer.</span><span class="sxs-lookup"><span data-stu-id="65917-123">Launch the MySQL Workbench application on your computer.</span></span> 

2.  <span data-ttu-id="65917-124">Nella finestra di dialogo **Setup New Connection** (Configura nuova connessione) immettere le informazioni seguenti nella scheda **Parameters** (Parametri):</span><span class="sxs-lookup"><span data-stu-id="65917-124">In **Setup New Connection** dialog box, enter the following information on the **Parameters** tab:</span></span>

    ![Setup New Connection (Configura nuova connessione)](./media/connect-workbench/2-setup-new-connection.png)

    | <span data-ttu-id="65917-126">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="65917-126">**Setting**</span></span> | <span data-ttu-id="65917-127">**Valore consigliato**</span><span class="sxs-lookup"><span data-stu-id="65917-127">**Suggested value**</span></span> | <span data-ttu-id="65917-128">**Descrizione campo**</span><span class="sxs-lookup"><span data-stu-id="65917-128">**Field description**</span></span> |
    |---|---|---|
    |   <span data-ttu-id="65917-129">Connection Name (Nome connessione)</span><span class="sxs-lookup"><span data-stu-id="65917-129">Connection Name</span></span> | <span data-ttu-id="65917-130">Demo Connection</span><span class="sxs-lookup"><span data-stu-id="65917-130">Demo Connection</span></span> | <span data-ttu-id="65917-131">Specificare un'etichetta per la connessione.</span><span class="sxs-lookup"><span data-stu-id="65917-131">Specify a label for this connection.</span></span> |
    | <span data-ttu-id="65917-132">Connection Method (Metodo di connessione)</span><span class="sxs-lookup"><span data-stu-id="65917-132">Connection Method</span></span> | <span data-ttu-id="65917-133">Standard (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="65917-133">Standard (TCP/IP)</span></span> | <span data-ttu-id="65917-134">Standard (TCP/IP) è sufficiente.</span><span class="sxs-lookup"><span data-stu-id="65917-134">Standard (TCP/IP) is sufficient.</span></span> |
    | <span data-ttu-id="65917-135">Nome host</span><span class="sxs-lookup"><span data-stu-id="65917-135">Hostname</span></span> | <span data-ttu-id="65917-136">*nome del server*</span><span class="sxs-lookup"><span data-stu-id="65917-136">*server name*</span></span> | <span data-ttu-id="65917-137">Specificare il valore del nome del server usato in precedenza al momento della creazione del database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="65917-137">Specify the server name value that was used when you created the Azure Database for MySQL earlier.</span></span> <span data-ttu-id="65917-138">Il server di esempio visualizzato è myserver4demo.mysql.database.azure.com. Usare il nome di dominio completo (\*.mysql.database.azure.com) come nell'esempio.</span><span class="sxs-lookup"><span data-stu-id="65917-138">Our example server shown is myserver4demo.mysql.database.azure.com. Use the fully qualified domain name (\*.mysql.database.azure.com) as shown in the example.</span></span> <span data-ttu-id="65917-139">Se non si ricorda il nome del server, seguire la procedura illustrata nella sezione precedente per ottenere le informazioni di connessione.</span><span class="sxs-lookup"><span data-stu-id="65917-139">Follow the steps in the previous section to get the connection information if you do not remember your server name.</span></span>  |
    | <span data-ttu-id="65917-140">Porta</span><span class="sxs-lookup"><span data-stu-id="65917-140">Port</span></span> | <span data-ttu-id="65917-141">3306</span><span class="sxs-lookup"><span data-stu-id="65917-141">3306</span></span> | <span data-ttu-id="65917-142">Usare sempre la porta 3306 per la connessione al database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="65917-142">Always use port 3306 when connecting to Azure Database for MySQL.</span></span> |
    | <span data-ttu-id="65917-143">Username</span><span class="sxs-lookup"><span data-stu-id="65917-143">Username</span></span> |  <span data-ttu-id="65917-144">*nome di accesso amministratore server*</span><span class="sxs-lookup"><span data-stu-id="65917-144">*server admin login name*</span></span> | <span data-ttu-id="65917-145">Digitare il nome utente di accesso amministratore server specificato in precedenza al momento della creazione del database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="65917-145">Type in the server admin login username supplied when you created the Azure Database for MySQL earlier.</span></span> <span data-ttu-id="65917-146">Il nome utente dell'esempio è myadmin@myserver4demo.</span><span class="sxs-lookup"><span data-stu-id="65917-146">Our example username is myadmin@myserver4demo.</span></span> <span data-ttu-id="65917-147">Se non si ricorda il nome utente, seguire la procedura illustrata nella sezione precedente per ottenere le informazioni di connessione.</span><span class="sxs-lookup"><span data-stu-id="65917-147">Follow the steps in the previous section to get the connection information if you do not remember the username.</span></span> <span data-ttu-id="65917-148">Il formato è *username@servername*.</span><span class="sxs-lookup"><span data-stu-id="65917-148">The format is *username@servername*.</span></span>
    | <span data-ttu-id="65917-149">Password</span><span class="sxs-lookup"><span data-stu-id="65917-149">Password</span></span> | <span data-ttu-id="65917-150">Immettere la password.</span><span class="sxs-lookup"><span data-stu-id="65917-150">your password</span></span> | <span data-ttu-id="65917-151">Fare clic sul pulsante **Store in Vault...** (Archivia nell'insieme di credenziali) per salvare la password.</span><span class="sxs-lookup"><span data-stu-id="65917-151">Click **Store in Vault...** button to save the password.</span></span> |

3.   <span data-ttu-id="65917-152">Fare clic su **Test Connection** (Test connessione) per verificare che tutti i parametri siano configurati correttamente.</span><span class="sxs-lookup"><span data-stu-id="65917-152">Click **Test Connection** to test if all parameters are correctly configured.</span></span> 

4.   <span data-ttu-id="65917-153">Fare clic su **OK** per salvare la connessione.</span><span class="sxs-lookup"><span data-stu-id="65917-153">Click **OK** to save the connection.</span></span> 

5.   <span data-ttu-id="65917-154">Nell'elenco delle **connessioni MySQL** fare clic sul riquadro corrispondente al server e attendere che venga stabilita la connessione.</span><span class="sxs-lookup"><span data-stu-id="65917-154">In the listing of **MySQL Connections**, click the tile corresponding to your server and wait for the connection to be established.</span></span>

6.   <span data-ttu-id="65917-155">Verrà visualizzata una nuova scheda SQL con un editor vuoto in cui è possibile digitare le query.</span><span class="sxs-lookup"><span data-stu-id="65917-155">A new SQL tab opens with a blank editor where you can type your queries.</span></span>

    > [!NOTE]
    > <span data-ttu-id="65917-156">Per impostazione predefinita, in Database di Azure per il server MySQL è necessaria e viene applicata la sicurezza della connessione SSL.</span><span class="sxs-lookup"><span data-stu-id="65917-156">By default, SSL connection security is required and enforced on your Azure Database for MySQL server.</span></span> <span data-ttu-id="65917-157">Non sono in genere necessarie configurazioni aggiuntive con certificati SSL per la connessione di MySQL Workbench al server.</span><span class="sxs-lookup"><span data-stu-id="65917-157">Typically no additional configuration with SSL certificates is required for MySQL Workbench to connect to your server.</span></span> <span data-ttu-id="65917-158">Per altre informazioni su SSL, vedere [Configurare la connettività SSL nell'applicazione per la connessione sicura a Database di Azure per MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="65917-158">For more information on SSL, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span></span>  <span data-ttu-id="65917-159">Se è necessario disabilitare SSL, visitare il portale di Azure e fare clic sulla pagina Sicurezza connessione per disabilitare l'interruttore Imponi connessione SSL.</span><span class="sxs-lookup"><span data-stu-id="65917-159">If you need to disable SSL, visit the Azure portal and click the Connection security page to disable the Enforce SSL connection toggle button.</span></span>

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a><span data-ttu-id="65917-160">Creare una tabella e inserire, leggere, aggiornare ed eliminare dati</span><span class="sxs-lookup"><span data-stu-id="65917-160">Create a table, insert data, read data, update data, delete data</span></span>
1. <span data-ttu-id="65917-161">Copiare e incollare il codice SQL di esempio in una scheda SQL vuota per illustrare alcuni dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="65917-161">Copy and paste the sample SQL code into a blank SQL tab to illustrate some sample data.</span></span>

    <span data-ttu-id="65917-162">Il codice crea un database vuoto denominato quickstartdb, quindi crea una tabella di esempio denominata inventory.</span><span class="sxs-lookup"><span data-stu-id="65917-162">This code creates an empty database named quickstartdb, and then creates a sample table named inventory.</span></span> <span data-ttu-id="65917-163">Inserisce alcune righe e quindi le legge.</span><span class="sxs-lookup"><span data-stu-id="65917-163">It inserts some rows, then reads the rows.</span></span> <span data-ttu-id="65917-164">Modifica i dati con un'istruzione update e legge nuovamente le righe.</span><span class="sxs-lookup"><span data-stu-id="65917-164">It changes the data with an update statement, and reads the rows again.</span></span> <span data-ttu-id="65917-165">Infine, elimina una riga e legge nuovamente le righe.</span><span class="sxs-lookup"><span data-stu-id="65917-165">Finally it deletes a row, and reads the rows again.</span></span>
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    <span data-ttu-id="65917-166">Lo screenshot mostra un esempio di codice SQL in MySQL Workbench e l'output dopo l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="65917-166">The screenshot shows an example of the SQL code in SQL Workbench and the output after it has been run.</span></span>
    
    ![Scheda SQL in MySQL Workbench per l'esecuzione del codice SQL di esempio](media/connect-workbench/3-workbench-sql-tab.png)

2. <span data-ttu-id="65917-168">Per eseguire l'esempio di codice SQL, fare clic sull'icona saetta nella barra degli strumenti della scheda **File SQL**.</span><span class="sxs-lookup"><span data-stu-id="65917-168">To run the sample SQL Code, click the lightening bolt icon in the toolbar of the **SQL File** tab.</span></span>
3. <span data-ttu-id="65917-169">Si notino i tre risultati a schede nella sezione **Griglia risultati** nella parte centrale della pagina.</span><span class="sxs-lookup"><span data-stu-id="65917-169">Notice the three tabbed results in the **Result Grid** section in the middle of the page.</span></span> 
4. <span data-ttu-id="65917-170">Si noti l'elenco **Output** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="65917-170">Notice the **Output** list at the bottom of the page.</span></span> <span data-ttu-id="65917-171">Viene visualizzato lo stato di ogni comando.</span><span class="sxs-lookup"><span data-stu-id="65917-171">The status of each command is shown.</span></span> 

<span data-ttu-id="65917-172">A questo punto è stata stabilita la connessione al database di Azure per MySQL tramite MySQL Workbench ed è stata eseguita una query sui dati con il linguaggio SQL.</span><span class="sxs-lookup"><span data-stu-id="65917-172">Now, you have connected to Azure Database for MySQL using MySQL Workbench, and have queried data using the SQL language.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65917-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="65917-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="65917-174">Eseguire la migrazione del database usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="65917-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
