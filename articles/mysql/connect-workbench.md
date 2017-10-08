---
title: La connessione tooAzure Database MySQL da MySQL Workbench | Documenti Microsoft
description: Questa Guida rapida fornisce hello passaggi toouse MySQL Workbench tooconnect ed eseguire query sui dati dal Database di Azure per MySQL.
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: c64fcb9bb99ba06aa3a95eec420d5d5ef4a31d14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-tooconnect-and-query-data"></a><span data-ttu-id="a8835-103">Il Database di Azure per MySQL: dati di utilizzo MySQL Workbench tooconnect e query</span><span class="sxs-lookup"><span data-stu-id="a8835-103">Azure Database for MySQL: Use MySQL Workbench tooconnect and query data</span></span>
<span data-ttu-id="a8835-104">Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di MySQL hello applicazione Workbench di MySQL.</span><span class="sxs-lookup"><span data-stu-id="a8835-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using hello MySQL Workbench application.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a8835-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a8835-105">Prerequisites</span></span>
<span data-ttu-id="a8835-106">Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="a8835-106">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="a8835-107">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creare un database di Azure per il server MySQL usando il portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="a8835-107">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- [<span data-ttu-id="a8835-108">Creare un database di Azure per il server MySQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a8835-108">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a><span data-ttu-id="a8835-109">Installare MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="a8835-109">Install MySQL Workbench</span></span>
<span data-ttu-id="a8835-110">Scaricare e installare MySQL Workbench nel computer in uso da [sito Web di MySQL hello](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="a8835-110">Download and install MySQL Workbench on your computer from [hello MySQL website](https://dev.mysql.com/downloads/workbench/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="a8835-111">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="a8835-111">Get connection information</span></span>
<span data-ttu-id="a8835-112">Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="a8835-112">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="a8835-113">È necessario hello le credenziali di nome e l'account di accesso completo del server.</span><span class="sxs-lookup"><span data-stu-id="a8835-113">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="a8835-114">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a8835-114">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="a8835-115">Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello sia stato creato, ad esempio **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="a8835-115">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>

3. <span data-ttu-id="a8835-116">Fare clic su nome hello del server.</span><span class="sxs-lookup"><span data-stu-id="a8835-116">Click hello server name.</span></span>

4. <span data-ttu-id="a8835-117">Server di selezionare hello **proprietà** pagina.</span><span class="sxs-lookup"><span data-stu-id="a8835-117">Select hello server's **Properties** page.</span></span> <span data-ttu-id="a8835-118">Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.</span><span class="sxs-lookup"><span data-stu-id="a8835-118">Make a note of hello **Server name** and **Server admin login name**.</span></span>

 ![Nome del server del database di Azure per MySQL](./media/connect-workbench/1-server-properties-name-login.png)
 
5. <span data-ttu-id="a8835-120">Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="a8835-120">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-toohello-server-using-mysql-workbench"></a><span data-ttu-id="a8835-121">Connessione server toohello utilizzando Workbench di MySQL</span><span class="sxs-lookup"><span data-stu-id="a8835-121">Connect toohello server using MySQL Workbench</span></span> 
<span data-ttu-id="a8835-122">utilizzo dello strumento GUI hello Workbench di MySQL server tooconnect tooAzure MySQL:</span><span class="sxs-lookup"><span data-stu-id="a8835-122">tooconnect tooAzure MySQL server using hello GUI tool MySQL Workbench:</span></span>

1.  <span data-ttu-id="a8835-123">Avviare hello applicazione Workbench di MySQL nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="a8835-123">Launch hello MySQL Workbench application on your computer.</span></span> 

2.  <span data-ttu-id="a8835-124">In **il programma di installazione nuova connessione** finestra di dialogo immettere le seguenti informazioni su hello hello **parametri** scheda:</span><span class="sxs-lookup"><span data-stu-id="a8835-124">In **Setup New Connection** dialog box, enter hello following information on hello **Parameters** tab:</span></span>

    ![Setup New Connection (Configura nuova connessione)](./media/connect-workbench/2-setup-new-connection.png)

    | <span data-ttu-id="a8835-126">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="a8835-126">**Setting**</span></span> | <span data-ttu-id="a8835-127">**Valore consigliato**</span><span class="sxs-lookup"><span data-stu-id="a8835-127">**Suggested value**</span></span> | <span data-ttu-id="a8835-128">**Descrizione campo**</span><span class="sxs-lookup"><span data-stu-id="a8835-128">**Field description**</span></span> |
    |---|---|---|
    |   <span data-ttu-id="a8835-129">Connection Name (Nome connessione)</span><span class="sxs-lookup"><span data-stu-id="a8835-129">Connection Name</span></span> | <span data-ttu-id="a8835-130">Demo Connection</span><span class="sxs-lookup"><span data-stu-id="a8835-130">Demo Connection</span></span> | <span data-ttu-id="a8835-131">Specificare un'etichetta per la connessione.</span><span class="sxs-lookup"><span data-stu-id="a8835-131">Specify a label for this connection.</span></span> |
    | <span data-ttu-id="a8835-132">Connection Method (Metodo di connessione)</span><span class="sxs-lookup"><span data-stu-id="a8835-132">Connection Method</span></span> | <span data-ttu-id="a8835-133">Standard (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="a8835-133">Standard (TCP/IP)</span></span> | <span data-ttu-id="a8835-134">Standard (TCP/IP) è sufficiente.</span><span class="sxs-lookup"><span data-stu-id="a8835-134">Standard (TCP/IP) is sufficient.</span></span> |
    | <span data-ttu-id="a8835-135">Nome host</span><span class="sxs-lookup"><span data-stu-id="a8835-135">Hostname</span></span> | <span data-ttu-id="a8835-136">*nome del server*</span><span class="sxs-lookup"><span data-stu-id="a8835-136">*server name*</span></span> | <span data-ttu-id="a8835-137">Specificare hello server valore del nome è stato utilizzato durante la creazione hello Database di Azure per MySQL in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a8835-137">Specify hello server name value that was used when you created hello Azure Database for MySQL earlier.</span></span> <span data-ttu-id="a8835-138">Il server di esempio visualizzato è myserver4demo.mysql.database.azure.com. Utilizza il nome di dominio completo hello (\*. mysql.database.azure.com) come illustrato nell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="a8835-138">Our example server shown is myserver4demo.mysql.database.azure.com. Use hello fully qualified domain name (\*.mysql.database.azure.com) as shown in hello example.</span></span> <span data-ttu-id="a8835-139">Seguire i passaggi di hello in hello precedente sezione tooget hello le informazioni di connessione se non si ricorda il nome del server.</span><span class="sxs-lookup"><span data-stu-id="a8835-139">Follow hello steps in hello previous section tooget hello connection information if you do not remember your server name.</span></span>  |
    | <span data-ttu-id="a8835-140">Porta</span><span class="sxs-lookup"><span data-stu-id="a8835-140">Port</span></span> | <span data-ttu-id="a8835-141">3306</span><span class="sxs-lookup"><span data-stu-id="a8835-141">3306</span></span> | <span data-ttu-id="a8835-142">Utilizzare sempre porta 3306 durante la connessione di Database tooAzure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="a8835-142">Always use port 3306 when connecting tooAzure Database for MySQL.</span></span> |
    | <span data-ttu-id="a8835-143">Username</span><span class="sxs-lookup"><span data-stu-id="a8835-143">Username</span></span> |  <span data-ttu-id="a8835-144">*nome di accesso amministratore server*</span><span class="sxs-lookup"><span data-stu-id="a8835-144">*server admin login name*</span></span> | <span data-ttu-id="a8835-145">Digitare nome utente account di accesso amministratore server hello specificato durante la creazione del Database di Azure hello per MySQL in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a8835-145">Type in hello server admin login username supplied when you created hello Azure Database for MySQL earlier.</span></span> <span data-ttu-id="a8835-146">Il nome utente dell'esempio è myadmin@myserver4demo.</span><span class="sxs-lookup"><span data-stu-id="a8835-146">Our example username is myadmin@myserver4demo.</span></span> <span data-ttu-id="a8835-147">Seguire i passaggi di hello in hello precedente sezione tooget hello le informazioni di connessione se non si ricorda hello username.</span><span class="sxs-lookup"><span data-stu-id="a8835-147">Follow hello steps in hello previous section tooget hello connection information if you do not remember hello username.</span></span> <span data-ttu-id="a8835-148">formato hello è  *username@servername* .</span><span class="sxs-lookup"><span data-stu-id="a8835-148">hello format is *username@servername*.</span></span>
    | <span data-ttu-id="a8835-149">Password</span><span class="sxs-lookup"><span data-stu-id="a8835-149">Password</span></span> | <span data-ttu-id="a8835-150">Immettere la password.</span><span class="sxs-lookup"><span data-stu-id="a8835-150">your password</span></span> | <span data-ttu-id="a8835-151">Fare clic su **archivio nell'insieme di credenziali...**  password hello toosave di pulsante.</span><span class="sxs-lookup"><span data-stu-id="a8835-151">Click **Store in Vault...** button toosave hello password.</span></span> |

3.   <span data-ttu-id="a8835-152">Fare clic su **Test connessione** tootest se tutti i parametri siano configurati correttamente.</span><span class="sxs-lookup"><span data-stu-id="a8835-152">Click **Test Connection** tootest if all parameters are correctly configured.</span></span> 

4.   <span data-ttu-id="a8835-153">Fare clic su **OK** connessione hello toosave.</span><span class="sxs-lookup"><span data-stu-id="a8835-153">Click **OK** toosave hello connection.</span></span> 

5.   <span data-ttu-id="a8835-154">Nell'elenco di hello di **connessioni MySQL**, fare clic su server tooyour corrispondente di hello riquadro e attendere hello toobe di connessione stabilita.</span><span class="sxs-lookup"><span data-stu-id="a8835-154">In hello listing of **MySQL Connections**, click hello tile corresponding tooyour server and wait for hello connection toobe established.</span></span>

6.   <span data-ttu-id="a8835-155">Verrà visualizzata una nuova scheda SQL con un editor vuoto in cui è possibile digitare le query.</span><span class="sxs-lookup"><span data-stu-id="a8835-155">A new SQL tab opens with a blank editor where you can type your queries.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a8835-156">Per impostazione predefinita, in Database di Azure per il server MySQL è necessaria e viene applicata la sicurezza della connessione SSL.</span><span class="sxs-lookup"><span data-stu-id="a8835-156">By default, SSL connection security is required and enforced on your Azure Database for MySQL server.</span></span> <span data-ttu-id="a8835-157">In genere alcuna configurazione aggiuntiva con i certificati SSL non è necessario per tooyour tooconnect del Workbench di MySQL server.</span><span class="sxs-lookup"><span data-stu-id="a8835-157">Typically no additional configuration with SSL certificates is required for MySQL Workbench tooconnect tooyour server.</span></span> <span data-ttu-id="a8835-158">Per ulteriori informazioni su SSL, vedere [connettività configurare SSL in toosecurely l'applicazione connessione tooAzure Database MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="a8835-158">For more information on SSL, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>  <span data-ttu-id="a8835-159">Se è necessario toodisable SSL, visitare il portale di Azure hello e fare clic su hello connessione sicurezza pagina toodisable hello applicare SSL connessione interruttore.</span><span class="sxs-lookup"><span data-stu-id="a8835-159">If you need toodisable SSL, visit hello Azure portal and click hello Connection security page toodisable hello Enforce SSL connection toggle button.</span></span>

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a><span data-ttu-id="a8835-160">Creare una tabella e inserire, leggere, aggiornare ed eliminare dati</span><span class="sxs-lookup"><span data-stu-id="a8835-160">Create a table, insert data, read data, update data, delete data</span></span>
1. <span data-ttu-id="a8835-161">Copiare e incollare hello SQL esempio un vuoto tooillustrate scheda SQL alcuni dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="a8835-161">Copy and paste hello sample SQL code into a blank SQL tab tooillustrate some sample data.</span></span>

    <span data-ttu-id="a8835-162">Il codice crea un database vuoto denominato quickstartdb, quindi crea una tabella di esempio denominata inventory.</span><span class="sxs-lookup"><span data-stu-id="a8835-162">This code creates an empty database named quickstartdb, and then creates a sample table named inventory.</span></span> <span data-ttu-id="a8835-163">Consente di inserire alcune righe, quindi legge righe hello.</span><span class="sxs-lookup"><span data-stu-id="a8835-163">It inserts some rows, then reads hello rows.</span></span> <span data-ttu-id="a8835-164">Modifica dati hello con un'istruzione update e letture hello righe nuovamente.</span><span class="sxs-lookup"><span data-stu-id="a8835-164">It changes hello data with an update statement, and reads hello rows again.</span></span> <span data-ttu-id="a8835-165">Infine viene eliminata una riga e legge le righe di hello nuovamente.</span><span class="sxs-lookup"><span data-stu-id="a8835-165">Finally it deletes a row, and reads hello rows again.</span></span>
    
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

    <span data-ttu-id="a8835-166">schermata di Hello illustra un esempio di codice SQL hello nell'output di SQL Workbench e hello dopo che è stato eseguito.</span><span class="sxs-lookup"><span data-stu-id="a8835-166">hello screenshot shows an example of hello SQL code in SQL Workbench and hello output after it has been run.</span></span>
    
    ![Codice SQL di esempio toorun scheda SQL Workbench di MySQL](media/connect-workbench/3-workbench-sql-tab.png)

2. <span data-ttu-id="a8835-168">esempio hello toorun codice SQL, fare clic su hello schiarire sull'icona nella barra degli strumenti hello di hello **File SQL** scheda.</span><span class="sxs-lookup"><span data-stu-id="a8835-168">toorun hello sample SQL Code, click hello lightening bolt icon in hello toolbar of hello **SQL File** tab.</span></span>
3. <span data-ttu-id="a8835-169">Si noti hello tre risultati a schede in hello **griglia dei risultati** sezione della pagina hello intermedio hello.</span><span class="sxs-lookup"><span data-stu-id="a8835-169">Notice hello three tabbed results in hello **Result Grid** section in hello middle of hello page.</span></span> 
4. <span data-ttu-id="a8835-170">Hello preavviso **Output** elenco hello parte inferiore della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="a8835-170">Notice hello **Output** list at hello bottom of hello page.</span></span> <span data-ttu-id="a8835-171">viene visualizzato lo stato di Hello di ogni comando.</span><span class="sxs-lookup"><span data-stu-id="a8835-171">hello status of each command is shown.</span></span> 

<span data-ttu-id="a8835-172">A questo punto, si è connessi tooAzure Database per MySQL mediante MySQL Workbench e dati usando il linguaggio SQL hello sono sottoposti a query.</span><span class="sxs-lookup"><span data-stu-id="a8835-172">Now, you have connected tooAzure Database for MySQL using MySQL Workbench, and have queried data using hello SQL language.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8835-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a8835-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a8835-174">Eseguire la migrazione del database usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="a8835-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
