---
title: Proteggere il database SQL di Azure | Microsoft Docs
description: "Informazioni sulle tecniche e le funzionalità per proteggere il database SQL di Azure."
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 4bc09ad13ed0c9dc9257e9c75ec6f9ff3d689a0b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="secure-your-azure-sql-database"></a><span data-ttu-id="72d3c-103">Proteggere il database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="72d3c-103">Secure your Azure SQL Database</span></span>

<span data-ttu-id="72d3c-104">Il database SQL protegge i dati limitando l'accesso al database usando regole del firewall, i meccanismi di autenticazione che richiedono agli utenti di dimostrare la propria identità e l'autorizzazione per i dati tramite le appartenenze basate sui ruoli e le autorizzazioni, oltre che tramite la sicurezza a livello di riga e la maschera dati dinamica.</span><span class="sxs-lookup"><span data-stu-id="72d3c-104">SQL Database secures your data by limiting access to your database using firewall rules, authentication mechanisms requiring users to prove their identity, and authorization to data through role-based memberships and permissions, as well as through row-level security and dynamic data masking.</span></span>

<span data-ttu-id="72d3c-105">È possibile migliorare la protezione del database contro utenti malintenzionati o accessi non autorizzati con pochi semplici passaggi.</span><span class="sxs-lookup"><span data-stu-id="72d3c-105">You can improve the protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="72d3c-106">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="72d3c-106">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="72d3c-107">Configurare regole del firewall a livello di server per il server nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="72d3c-107">Set up server-level firewall rules for your server in the Azure portal</span></span>
> * <span data-ttu-id="72d3c-108">Configurare regole del firewall a livello di database per il database con SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="72d3c-108">Set up database-level firewall rules for your database using SSMS</span></span>
> * <span data-ttu-id="72d3c-109">Connettersi al database usando una stringa di connessione protetta</span><span class="sxs-lookup"><span data-stu-id="72d3c-109">Connect to your database using a secure connection string</span></span>
> * <span data-ttu-id="72d3c-110">Gestire l'accesso utente</span><span class="sxs-lookup"><span data-stu-id="72d3c-110">Manage user access</span></span>
> * <span data-ttu-id="72d3c-111">Proteggere i dati con la crittografia</span><span class="sxs-lookup"><span data-stu-id="72d3c-111">Protect your data with encryption</span></span>
> * <span data-ttu-id="72d3c-112">Abilitare il controllo del database SQL</span><span class="sxs-lookup"><span data-stu-id="72d3c-112">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="72d3c-113">Abilitare il rilevamento delle minacce per il database SQL</span><span class="sxs-lookup"><span data-stu-id="72d3c-113">Enable SQL Database threat detection</span></span>

<span data-ttu-id="72d3c-114">Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="72d3c-114">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72d3c-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="72d3c-115">Prerequisites</span></span>

<span data-ttu-id="72d3c-116">Per completare questa esercitazione, accertarsi di avere:</span><span class="sxs-lookup"><span data-stu-id="72d3c-116">To complete this tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="72d3c-117">Installato la versione più recente di [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="72d3c-117">Installed the newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> 
- <span data-ttu-id="72d3c-118">Installato Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="72d3c-118">Installed Microsoft Excel</span></span>
- <span data-ttu-id="72d3c-119">Creato un server e un database SQL di Azure. Vedere [Creare un database SQL di Azure nel portale di Azure](sql-database-get-started-portal.md), [Creare un singolo database SQL di Azure usando l'interfaccia della riga di comando di Azure](sql-database-get-started-cli.md) e [Creare un singolo database SQL di Azure usando PowerShell](sql-database-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="72d3c-119">Created an Azure SQL server and database - See [Create an Azure SQL database in the Azure portal](sql-database-get-started-portal.md), [Create a single Azure SQL database using the Azure CLI](sql-database-get-started-cli.md), and [Create a single Azure SQL database using PowerShell](sql-database-get-started-powershell.md).</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="72d3c-120">Accedere al Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="72d3c-120">Log in to the Azure portal</span></span>

<span data-ttu-id="72d3c-121">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="72d3c-121">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="72d3c-122">Creare una regola del firewall a livello di server nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="72d3c-122">Create a server-level firewall rule in the Azure portal</span></span>

<span data-ttu-id="72d3c-123">I database SQL sono protetti da un firewall in Azure.</span><span class="sxs-lookup"><span data-stu-id="72d3c-123">SQL databases are protected by a firewall in Azure.</span></span> <span data-ttu-id="72d3c-124">Per impostazione predefinita, vengono rifiutate tutte le connessioni al server e ai database all'interno del server ad eccezione delle connessioni di altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="72d3c-124">By default, all connections to the server and the databases inside the server are rejected except for connections from other Azure services.</span></span> <span data-ttu-id="72d3c-125">Per altre informazioni, vedere [Regole firewall a livello di server e di database per il database SQL di Azure](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="72d3c-125">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="72d3c-126">La configurazione più sicura consiste nell'impostare "Consenti l'accesso a Servizi di Azure" su NON ATTIVO.</span><span class="sxs-lookup"><span data-stu-id="72d3c-126">The most secure configuration is to set 'Allow access to Azure services' to OFF.</span></span> <span data-ttu-id="72d3c-127">Se è necessario connettersi al database da un servizio cloud o da una macchina virtuale di Azure, è necessario creare un [indirizzo IP riservato](../virtual-network/virtual-networks-reserved-public-ip.md) e consentire solo a questo indirizzo l'accesso tramite firewall.</span><span class="sxs-lookup"><span data-stu-id="72d3c-127">If you need to connect to the database from an Azure VM or cloud service, you should create a [Reserved IP](../virtual-network/virtual-networks-reserved-public-ip.md) and allow only the reserved IP address access through the firewall.</span></span> 

<span data-ttu-id="72d3c-128">Seguire questa procedura per creare una [regola del firewall a livello di server del database SQL](sql-database-firewall-configure.md) per il server per consentire le connessioni dall'indirizzo IP specifico.</span><span class="sxs-lookup"><span data-stu-id="72d3c-128">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server to allow connections from a specific IP address.</span></span> 

> [!NOTE]
> <span data-ttu-id="72d3c-129">Se è stato creato un database di esempio in Azure usando una delle esercitazioni o guide rapide precedenti e si sta eseguendo questa esercitazione in un computer con lo stesso indirizzo IP assegnato durante l'esecuzione delle esercitazioni, è possibile ignorare questo passaggio perché la regola del firewall a livello di server è già stata creata.</span><span class="sxs-lookup"><span data-stu-id="72d3c-129">If you have created a sample database in Azure using one of the previous tutorials or quickstarts and are performing this tutorial on a computer with the same IP address that it had when you walked through those tutorials, you can skip this step as you will have already created a server-level firewall rule.</span></span>
>

1. <span data-ttu-id="72d3c-130">Fare clic su **Database SQL** nel menu a sinistra e scegliere il database in cui si desidera configurare la regola di firewall nella pagina **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="72d3c-130">Click **SQL databases** from the left-hand menu and click the database you would like to configure the firewall rule for on the **SQL databases** page.</span></span> <span data-ttu-id="72d3c-131">Si apre la pagina di panoramica per il database che visualizza il nome completo del server, ad esempio **mynewserver20170313.database.windows.net**, e offre altre opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="72d3c-131">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![Regola del firewall del server](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. <span data-ttu-id="72d3c-133">Fare clic su **Imposta firewall server** sulla barra degli strumenti, come illustrato nell'immagine precedente.</span><span class="sxs-lookup"><span data-stu-id="72d3c-133">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="72d3c-134">Si apre la pagina **Impostazioni del firewall** per il server del database SQL.</span><span class="sxs-lookup"><span data-stu-id="72d3c-134">The **Firewall settings** page for the SQL Database server opens.</span></span> 

3. <span data-ttu-id="72d3c-135">Fare clic su **Aggiungi IP client** sulla barra degli strumenti per aggiungere l'indirizzo IP pubblico del computer connesso al portale o immettere manualmente la regola del firewall e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="72d3c-135">Click **Add client IP** on the toolbar to add the public IP address of the computer connected to the portal with or enter the firewall rule manually and then click **Save**.</span></span>

      ![Impostare la regola del firewall del server](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. <span data-ttu-id="72d3c-137">Fare clic su **OK** e quindi sulla **X** per chiudere la pagina **Impostazioni del firewall**.</span><span class="sxs-lookup"><span data-stu-id="72d3c-137">Click **OK** and then click the **X** to close the **Firewall settings** page.</span></span>

<span data-ttu-id="72d3c-138">È ora possibile connettersi a qualsiasi database nel server con l'indirizzo IP specificato o con un intervallo di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="72d3c-138">You can now connect to any database in the server with the specified IP address or IP address range.</span></span>

> [!NOTE]
> <span data-ttu-id="72d3c-139">Il database SQL comunica attraverso la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="72d3c-139">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="72d3c-140">Se si sta tentando di connettersi da una rete aziendale, il traffico in uscita attraverso la porta 1433 potrebbe non essere autorizzato dal firewall della rete.</span><span class="sxs-lookup"><span data-stu-id="72d3c-140">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="72d3c-141">In questo caso, non sarà possibile connettersi al server del database SQL di Azure, a meno che il reparto IT non apra la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="72d3c-141">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a><span data-ttu-id="72d3c-142">Creare una regola del firewall a livello di database con SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="72d3c-142">Create a database-level firewall rule using SSMS</span></span>

<span data-ttu-id="72d3c-143">Le regole del firewall a livello di database consentono di creare impostazioni del firewall diverse per database differenti all'interno dello stesso server logico e di creare regole del firewall che possono essere trasferite, ovvero che seguono il database durante un [failover](sql-database-geo-replication-overview.md) anziché essere archiviate nel computer SQL Server.</span><span class="sxs-lookup"><span data-stu-id="72d3c-143">Database-level firewall rules enable you to create different firewall settings for different databases within the same logical server and to create firewall rules that are portable - meaning that they follow the database during a [failover](sql-database-geo-replication-overview.md) rather than being stored on the SQL server.</span></span> <span data-ttu-id="72d3c-144">Le regole del firewall a livello di database possono essere configurate solo usando le istruzioni Transact-SQL e solo dopo aver configurato la prima regola del firewall a livello di server.</span><span class="sxs-lookup"><span data-stu-id="72d3c-144">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured the first server-level firewall rule.</span></span> <span data-ttu-id="72d3c-145">Per altre informazioni, vedere [Regole firewall a livello di server e di database per il database SQL di Azure](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="72d3c-145">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="72d3c-146">Per creare una regola del firewall specifiche del database seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="72d3c-146">Follows these steps to create a database-specific firewall rule.</span></span>

1. <span data-ttu-id="72d3c-147">Connettersi al database, ad esempio usando [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="72d3c-147">Connect to your database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span></span>

2. <span data-ttu-id="72d3c-148">In Esplora oggetti fare clic con il tasto destro del mouse sul database a cui si desidera aggiungere una regola del firewall e fare clic su **Nuova query**.</span><span class="sxs-lookup"><span data-stu-id="72d3c-148">In Object Explorer, right-click on the database you want to add a firewall rule for and click **New Query**.</span></span> <span data-ttu-id="72d3c-149">Viene visualizzata una finestra di query vuota, connessa al database.</span><span class="sxs-lookup"><span data-stu-id="72d3c-149">A blank query window opens that is connected to your database.</span></span>

3. <span data-ttu-id="72d3c-150">Nella finestra di query sostituire l'indirizzo IP con l'indirizzo IP pubblico e quindi eseguire la query seguente:</span><span class="sxs-lookup"><span data-stu-id="72d3c-150">In the query window, modify the IP address to your public IP address and then execute the following query:</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. <span data-ttu-id="72d3c-151">Sulla barra degli strumenti fare clic su **Esegui** per creare la regola del firewall.</span><span class="sxs-lookup"><span data-stu-id="72d3c-151">On the toolbar, click **Execute** to create the firewall rule.</span></span>

## <a name="view-how-to-connect-an-application-to-your-database-using-a-secure-connection-string"></a><span data-ttu-id="72d3c-152">Come connettere un'applicazione al database usando una stringa di connessione protetta</span><span class="sxs-lookup"><span data-stu-id="72d3c-152">View how to connect an application to your database using a secure connection string</span></span>

<span data-ttu-id="72d3c-153">Per garantire una connessione crittografata e protetta tra l'applicazione client e il database SQL, la stringa di connessione deve essere configurata per:</span><span class="sxs-lookup"><span data-stu-id="72d3c-153">To ensure a secure, encrypted connection between a client application and SQL Database, the connection string has to be configured to:</span></span>

- <span data-ttu-id="72d3c-154">Richiedere una connessione crittografata, e</span><span class="sxs-lookup"><span data-stu-id="72d3c-154">Request an encrypted connection, and</span></span>
- <span data-ttu-id="72d3c-155">Non considerare attendibile il certificato del server.</span><span class="sxs-lookup"><span data-stu-id="72d3c-155">To not trust the server certificate.</span></span> 

<span data-ttu-id="72d3c-156">Questo consente di stabilire una connessione tramite Transport Layer Security (TLS) e di ridurre il rischio di attacco man-in-the-middle .</span><span class="sxs-lookup"><span data-stu-id="72d3c-156">This establishes a connection using Transport Layer Security (TLS) and reduces the risk of man-in-the-middle attacks.</span></span> <span data-ttu-id="72d3c-157">È possibile ottenere stringhe di connessione configurate correttamente per il database SQL per i driver di client supportati nel portale di Azure, come illustrato per ADO.net in questo screenshot.</span><span class="sxs-lookup"><span data-stu-id="72d3c-157">You can obtain correctly configured connection strings for your SQL Database for supported client drivers from the Azure portal as shown for ADO.net in this screenshot.</span></span>

1. <span data-ttu-id="72d3c-158">Scegliere **Database SQL** dal menu a sinistra, quindi fare clic sul database nella pagina **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="72d3c-158">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span>

2. <span data-ttu-id="72d3c-159">Nella pagina **Panoramica** del database fare clic su **Mostra stringhe di connessione del database**.</span><span class="sxs-lookup"><span data-stu-id="72d3c-159">On the **Overview** page for your database, click **Show database connection strings**.</span></span>

3. <span data-ttu-id="72d3c-160">Esaminare la stringa di connessione completa **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="72d3c-160">Review the complete **ADO.NET** connection string.</span></span>

    ![Stringa di connessione ADO.NET](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a><span data-ttu-id="72d3c-162">Creazione degli utenti del database</span><span class="sxs-lookup"><span data-stu-id="72d3c-162">Creating database users</span></span>

<span data-ttu-id="72d3c-163">Prima di creare gli utenti, è innanzitutto necessario scegliere uno dei due tipi di autenticazione supportati dal database SQL di Azure:</span><span class="sxs-lookup"><span data-stu-id="72d3c-163">Before creating any users, you must first choose from one of two authentication types supported by Azure SQL Database:</span></span> 

<span data-ttu-id="72d3c-164">**Autenticazione di SQL**, che usa nome utente e password per gli accessi e gli utenti che sono validi solo nel contesto di un database specifico all'interno di un server logico.</span><span class="sxs-lookup"><span data-stu-id="72d3c-164">**SQL Authentication**, which uses username and password for logins and users that are valid only in the context of a specific database within a logical server.</span></span> 

<span data-ttu-id="72d3c-165">**Autenticazione di Azure Active Directory**, che usa identità gestite da Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="72d3c-165">**Azure Active Directory Authentication**, which uses identities managed by Azure Active Directory.</span></span> 

<span data-ttu-id="72d3c-166">Se si desidera usare [Azure Active Directory](./sql-database-aad-authentication.md) per l'autenticazione nel database SQL, deve esistere un Azure Active Directory popolato prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="72d3c-166">If you want to use [Azure Active Directory](./sql-database-aad-authentication.md) to authenticate against SQL Database, a populated Azure Active Directory must exist before you can proceed.</span></span>

<span data-ttu-id="72d3c-167">Seguire questa procedura per creare un utente tramite l'autenticazione di SQL:</span><span class="sxs-lookup"><span data-stu-id="72d3c-167">Follow these steps to create a user using SQL Authentication:</span></span>

1. <span data-ttu-id="72d3c-168">Connettersi al database, ad esempio usando [SQL Server Management Studio](./sql-database-connect-query-ssms.md) con le credenziali di amministratore del server.</span><span class="sxs-lookup"><span data-stu-id="72d3c-168">Connect to your database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) using your server admin credentials.</span></span>

2. <span data-ttu-id="72d3c-169">In Esplora oggetti fare clic con il tasto destro del mouse sul database a cui si desidera aggiungere un nuovo utente e fare clic su **Nuova query**.</span><span class="sxs-lookup"><span data-stu-id="72d3c-169">In Object Explorer, right-click on the database you want to add a new user on and click **New Query**.</span></span> <span data-ttu-id="72d3c-170">Viene visualizzata una finestra di query vuota, connessa al database selezionato.</span><span class="sxs-lookup"><span data-stu-id="72d3c-170">A blank query window opens that is connected to the selected database.</span></span>

3. <span data-ttu-id="72d3c-171">Nella finestra delle query, immettere la query seguente:</span><span class="sxs-lookup"><span data-stu-id="72d3c-171">In the query window, enter the following query:</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. <span data-ttu-id="72d3c-172">Sulla barra degli strumenti fare clic su **Esegui** per creare l'utente.</span><span class="sxs-lookup"><span data-stu-id="72d3c-172">On the toolbar, click **Execute** to create the user.</span></span>

5. <span data-ttu-id="72d3c-173">Per impostazione predefinita, l'utente può connettersi al database, ma non dispone delle autorizzazioni per leggere o scrivere dati.</span><span class="sxs-lookup"><span data-stu-id="72d3c-173">By default, the user can connect to the database, but has no permissions to read or write data.</span></span> <span data-ttu-id="72d3c-174">Per concedere le autorizzazioni all'utente appena creato, eseguire i due comandi seguenti in una nuova finestra di query</span><span class="sxs-lookup"><span data-stu-id="72d3c-174">To grant these permissions to the newly created user, execute the following two commands in a new query window</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

<span data-ttu-id="72d3c-175">È consigliabile creare gli account non amministratore a livello di database per la connessione al database, a meno che non sia necessario eseguire le attività di amministrazione quali la creazione di nuovi utenti.</span><span class="sxs-lookup"><span data-stu-id="72d3c-175">It is best practice to create these non-administrator accounts at the database level to connect to your database unless you need to execute administrator tasks like creating new users.</span></span> <span data-ttu-id="72d3c-176">Rivedere l'[esercitazione di Azure Active Directory](./sql-database-aad-authentication-configure.md) su come eseguire l'autenticazione con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="72d3c-176">Please review the [Azure Active Directory tutorial](./sql-database-aad-authentication-configure.md) on how to authenticate using Azure Active Directory.</span></span>


## <a name="protect-your-data-with-encryption"></a><span data-ttu-id="72d3c-177">Proteggere i dati con la crittografia</span><span class="sxs-lookup"><span data-stu-id="72d3c-177">Protect your data with encryption</span></span>

<span data-ttu-id="72d3c-178">Transparent Data Encryption, ovvero TDE, di database SQL di Azure consente di crittografare automaticamente i dati inattivi, senza richiedere alcuna modifica all'applicazione che accede al database crittografato.</span><span class="sxs-lookup"><span data-stu-id="72d3c-178">Azure SQL Database transparent data encryption (TDE) automatically encrypts your data at rest, without requiring any changes to the application accessing the encrypted database.</span></span> <span data-ttu-id="72d3c-179">Per i nuovi database creati, la crittografia TDE è attiva per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="72d3c-179">For newly created databases, TDE is on by default.</span></span> <span data-ttu-id="72d3c-180">Per abilitare la crittografia TDE per il database oppure per verificare che sia attivata, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="72d3c-180">To enable TDE for your database or to verify that TDE is on, follow these steps:</span></span>

1. <span data-ttu-id="72d3c-181">Scegliere **Database SQL** dal menu a sinistra, quindi fare clic sul database nella pagina **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="72d3c-181">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 

2. <span data-ttu-id="72d3c-182">Fare clic su **Transparent Data Encryption** per aprire la pagina di configurazione di TDE.</span><span class="sxs-lookup"><span data-stu-id="72d3c-182">Click on **Transparent data encryption** to open the configuration page for TDE.</span></span>

    ![Transparent Data Encryption](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. <span data-ttu-id="72d3c-184">Se necessario, impostare **Crittografia dati** su Sì e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="72d3c-184">If necessary, set **Data encryption** to ON and click **Save**.</span></span>

<span data-ttu-id="72d3c-185">Il processo di crittografia viene avviato in background.</span><span class="sxs-lookup"><span data-stu-id="72d3c-185">The encryption process starts in the background.</span></span> <span data-ttu-id="72d3c-186">Per monitorare lo stato, connettersi al database SQL con [SQL Server Management Studio](./sql-database-connect-query-ssms.md) effettuando una query della colonna encryption_state nella visualizzazione `sys.dm_database_encryption_keys`.</span><span class="sxs-lookup"><span data-stu-id="72d3c-186">You can monitor the progress by connecting to SQL Database using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) by querying the encryption_state column of the `sys.dm_database_encryption_keys` view.</span></span>

## <a name="enable-sql-database-auditing-if-necessary"></a><span data-ttu-id="72d3c-187">Abilitare il controllo del database SQL, se necessario</span><span class="sxs-lookup"><span data-stu-id="72d3c-187">Enable SQL Database auditing, if necessary</span></span>

<span data-ttu-id="72d3c-188">Il controllo del database SQL di Azure tiene traccia degli eventi che si verificano nel database e li registra in un log di controllo nell'account di Archiviazione di Azure dell'utente.</span><span class="sxs-lookup"><span data-stu-id="72d3c-188">Azure SQL Database Auditing tracks database events and writes them to an audit log in your Azure Storage account.</span></span> <span data-ttu-id="72d3c-189">Il controllo consente di agevolare la conformità alle normative, comprendere le attività del database e ottenere informazioni su eventuali discrepanze e anomalie che potrebbero indicare potenziali violazioni della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="72d3c-189">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate potential security violations.</span></span> <span data-ttu-id="72d3c-190">Per creare un criterio di controllo predefinito per il database SQL, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="72d3c-190">Follow these steps to create a default auditing policy for your SQL database:</span></span>

1. <span data-ttu-id="72d3c-191">Scegliere **Database SQL** dal menu a sinistra, quindi fare clic sul database nella pagina **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="72d3c-191">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 

2. <span data-ttu-id="72d3c-192">Nel pannello Impostazioni selezionare **Controllo e rilevamento minacce**.</span><span class="sxs-lookup"><span data-stu-id="72d3c-192">In the Settings blade, select **Auditing & Threat Detection**.</span></span> <span data-ttu-id="72d3c-193">Si noti che il controllo a livello di server è disabilitato ed è disponibile un collegamento **Visualizza impostazioni del server** che consente di visualizzare o modificare le impostazioni di controllo del server da questo contesto.</span><span class="sxs-lookup"><span data-stu-id="72d3c-193">Notice that sever-level auditing is diabled and that there is a **View server settings** link that allows you to view or modify the server auditing settings from this context.</span></span>

    ![Pannello di controllo](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. <span data-ttu-id="72d3c-195">Se si preferisce abilitare un tipo di controllo (o una posizione) diverso da quello specificato a livello di server, **attivare** Controllo e scegliere il tipo di controllo **BLOB**.</span><span class="sxs-lookup"><span data-stu-id="72d3c-195">If you prefer to enable an Audit type (or location?) different from the one specified at the server level, turn **ON** Auditing, and choose the **Blob** Auditing Type.</span></span> <span data-ttu-id="72d3c-196">Se il controllo BLOB del server è abilitato, il controllo configurato del database coesisterà con il controllo BLOB del server.</span><span class="sxs-lookup"><span data-stu-id="72d3c-196">If server Blob auditing is enabled, the database configured audit will exist side by side with the server Blob audit.</span></span>

    ![Attivare il controllo](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. <span data-ttu-id="72d3c-198">Selezionare i **Dettagli di archiviazione** per aprire il pannello di archiviazione dei log di controllo.</span><span class="sxs-lookup"><span data-stu-id="72d3c-198">Select **Storage Details** to open the Audit Logs Storage Blade.</span></span> <span data-ttu-id="72d3c-199">Selezionare l'account di archiviazione di Azure in cui verranno salvati i log e il periodo di conservazione, dopo il quale verranno eliminati i vecchi log, quindi fare clic su **OK** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="72d3c-199">Select the Azure storage account where logs will be saved, and the retention period, after which the old logs will be deleted, then click **OK** at the bottom.</span></span> 

   > [!TIP]
   > <span data-ttu-id="72d3c-200">Per sfruttare al massimo i modelli di report di controllo, usare lo stesso account di archiviazione per tutti i database controllati.</span><span class="sxs-lookup"><span data-stu-id="72d3c-200">Use the same storage account for all audited databases to get the most out of the auditing reports templates.</span></span>
   > 

5. <span data-ttu-id="72d3c-201">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="72d3c-201">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72d3c-202">Se si vuole personalizzare gli eventi controllati, è possibile farlo tramite l'API di PowerShell o REST: per altre informazioni, vedere la sezione [Automazione (API di PowerShell/REST)](sql-database-auditing.md#subheading-7).</span><span class="sxs-lookup"><span data-stu-id="72d3c-202">If you want to customize the audited events, you can do this via PowerShell or REST API - see the [Automation (PowerShell / REST API)](sql-database-auditing.md#subheading-7) section for more details.</span></span>
>

## <a name="enable-sql-database-threat-detection"></a><span data-ttu-id="72d3c-203">Abilitare il rilevamento delle minacce per il database SQL</span><span class="sxs-lookup"><span data-stu-id="72d3c-203">Enable SQL Database threat detection</span></span>

<span data-ttu-id="72d3c-204">Il rilevamento delle minacce offre un nuovo livello di protezione, che consente ai clienti di rilevare e rispondere alle minacce potenziali non appena si verificano, fornendo avvisi di sicurezza sulle attività anomale.</span><span class="sxs-lookup"><span data-stu-id="72d3c-204">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="72d3c-205">Gli utenti possono esaminare gli eventi sospetti tramite il servizio di controllo del database SQL per determinare se sono il risultato di un tentativo di accesso, una violazione o un exploit dei dati del database.</span><span class="sxs-lookup"><span data-stu-id="72d3c-205">Users can explore the suspicious events using SQL Database Auditing to determine if they result from an attempt to access, breach or exploit data in the database.</span></span> <span data-ttu-id="72d3c-206">Il rilevamento delle minacce rende più semplice affrontare le minacce potenziali al database, senza dover essere esperti della sicurezza o gestire sistemi di controllo di sicurezza avanzati.</span><span class="sxs-lookup"><span data-stu-id="72d3c-206">Threat Detection makes it simple to address potential threats to the database without the need to be a security expert or manage advanced security monitoring systems.</span></span>
<span data-ttu-id="72d3c-207">Ad esempio, la funzionalità di rilevamento delle minacce individua determinate attività anomale nel database che indicano potenziali tentativi di attacco SQL injection.</span><span class="sxs-lookup"><span data-stu-id="72d3c-207">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="72d3c-208">L'attacco SQL injection è uno dei problemi di sicurezza comuni delle applicazioni Web su Internet, che viene usato per attaccare le applicazioni guidate dai dati.</span><span class="sxs-lookup"><span data-stu-id="72d3c-208">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="72d3c-209">Gli autori di attacchi sfruttano le vulnerabilità delle applicazioni per introdurre istruzioni SQL dannose nei campi di immissione dell'applicazione, per violare o modificare i dati nel database.</span><span class="sxs-lookup"><span data-stu-id="72d3c-209">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span></span>

1. <span data-ttu-id="72d3c-210">Passare al pannello di configurazione del database SQL che si vuole monitorare.</span><span class="sxs-lookup"><span data-stu-id="72d3c-210">Navigate to the configuration blade of the SQL database you want to monitor.</span></span> <span data-ttu-id="72d3c-211">Nel pannello Impostazioni selezionare **Controllo e rilevamento minacce**.</span><span class="sxs-lookup"><span data-stu-id="72d3c-211">In the Settings blade, select **Auditing & Threat Detection**.</span></span>

    ![Riquadro di spostamento](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. <span data-ttu-id="72d3c-213">Nel pannello di configurazione **Controllo e rilevamento minacce** impostare il controllo su **SÌ**, il che consentirà di visualizzare le impostazioni di rilevamento minacce.</span><span class="sxs-lookup"><span data-stu-id="72d3c-213">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the threat detection settings.</span></span>

3. <span data-ttu-id="72d3c-214">Impostare il rilevamento delle minacce su **SÌ**.</span><span class="sxs-lookup"><span data-stu-id="72d3c-214">Turn **ON** threat detection.</span></span>

4. <span data-ttu-id="72d3c-215">Configurare l'elenco di indirizzi di posta elettronica che riceveranno avvisi di sicurezza in caso di rilevamento di attività di database anomale.</span><span class="sxs-lookup"><span data-stu-id="72d3c-215">Configure the list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>

5. <span data-ttu-id="72d3c-216">Fare clic su **Salva** nel pannello di configurazione **Controllo e rilevamento minacce** per salvare il controllo nuovo o aggiornato e i criteri di rilevamento delle minacce.</span><span class="sxs-lookup"><span data-stu-id="72d3c-216">Click **Save** in the **Auditing & Threat detection** blade to save the new or updated auditing and threat detection policy.</span></span>

    ![Riquadro di spostamento](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    <span data-ttu-id="72d3c-218">Se vengono rilevate attività anomale del database, si riceverà una notifica tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="72d3c-218">If anomalous database activities are detected, you will receive an email notification upon detection of anomalous database activities.</span></span> <span data-ttu-id="72d3c-219">Il messaggio di posta elettronica fornirà informazioni sull'evento di sicurezza sospetto, inclusi la natura delle attività anomale, il nome del database, il nome del server e l'ora dell'evento.</span><span class="sxs-lookup"><span data-stu-id="72d3c-219">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span></span> <span data-ttu-id="72d3c-220">Verranno anche fornite informazioni sulle possibili cause e le azioni consigliate per analizzare e ridurre il rischio di una potenziale minaccia al database.</span><span class="sxs-lookup"><span data-stu-id="72d3c-220">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span> <span data-ttu-id="72d3c-221">I passaggi successivi illustrano la procedura consigliata per un utente che riceva un messaggio di posta simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="72d3c-221">The next steps walk you through what to do should you receive such an email:</span></span>

    ![Messaggio di posta elettronica sul rilevamento delle minacce](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. <span data-ttu-id="72d3c-223">Nel messaggio di posta elettronica fare clic sul collegamento al **log di controllo SQL di Azure** che avvierà il portale di Azure visualizzando i record di controllo pertinenti intorno all'ora dell'evento sospetto.</span><span class="sxs-lookup"><span data-stu-id="72d3c-223">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure portal and show the relevant auditing records around the time of the suspicious event.</span></span>

    ![Record di controllo](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. <span data-ttu-id="72d3c-225">Fare clic sui record di controllo per visualizzare altri dettagli sulle attività di database sospette, come l'istruzione SQL, il motivo dell'errore e l'indirizzo IP del client.</span><span class="sxs-lookup"><span data-stu-id="72d3c-225">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span></span>

    ![Dettagli sui record](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. <span data-ttu-id="72d3c-227">Nel pannello Auditing Records (Controllo record) fare clic su  **Apri in Excel** per aprire un modello Excel preconfigurato per importare ed eseguire un'analisi più approfondita del log di controllo sull'orario in cui si è verificato l'evento sospetto.</span><span class="sxs-lookup"><span data-stu-id="72d3c-227">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span></span>

    > [!NOTE]
    > <span data-ttu-id="72d3c-228">In Excel 2010 o in una versione successiva sono richiesti Power Query e l'impostazione **Combinazione rapida**.</span><span class="sxs-lookup"><span data-stu-id="72d3c-228">In Excel 2010 or later, Power Query and the **Fast Combine** setting is required.</span></span>

    ![Aprire i record in Excel](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. <span data-ttu-id="72d3c-230">Per configurare l'impostazione **Combinazione rapida**, nella scheda della barra multifunzione **POWER QUERY** selezionare **Opzioni** per visualizzare la finestra di dialogo Opzioni.</span><span class="sxs-lookup"><span data-stu-id="72d3c-230">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span></span> <span data-ttu-id="72d3c-231">Selezionare la sezione Privacy e scegliere la seconda opzione - "Ignora i livelli di privacy per un potenziale miglioramento delle prestazioni":</span><span class="sxs-lookup"><span data-stu-id="72d3c-231">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span></span>

    ![Combinazione rapida di Excel](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. <span data-ttu-id="72d3c-233">Per caricare i log di controllo SQL, assicurarsi che i parametri nella scheda Impostazioni siano configurati correttamente e quindi selezionare "Dati" sulla barra multifunzione e fare clic sul pulsante "Aggiorna tutto".</span><span class="sxs-lookup"><span data-stu-id="72d3c-233">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span></span>

    ![Parametri di Excel](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. <span data-ttu-id="72d3c-235">I risultati vengono visualizzati nel foglio dei **log di controllo SQL** che consente di eseguire un'analisi più approfondita delle attività anomale rilevate e di ridurre l'impatto dell'evento di sicurezza nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="72d3c-235">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span></span>


## <a name="next-steps"></a><span data-ttu-id="72d3c-236">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="72d3c-236">Next steps</span></span>
<span data-ttu-id="72d3c-237">È possibile migliorare la protezione del database contro utenti malintenzionati o accessi non autorizzati con pochi semplici passaggi.</span><span class="sxs-lookup"><span data-stu-id="72d3c-237">You can improve the protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="72d3c-238">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="72d3c-238">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="72d3c-239">Configurare le regole del firewall per il server e/o il database</span><span class="sxs-lookup"><span data-stu-id="72d3c-239">Set up firewall rules for your sever and or database</span></span>
> * <span data-ttu-id="72d3c-240">Connettersi al database usando una stringa di connessione protetta</span><span class="sxs-lookup"><span data-stu-id="72d3c-240">Connect to your database using a secure connection string</span></span>
> * <span data-ttu-id="72d3c-241">Gestire l'accesso utente</span><span class="sxs-lookup"><span data-stu-id="72d3c-241">Manage user access</span></span>
> * <span data-ttu-id="72d3c-242">Proteggere i dati con la crittografia</span><span class="sxs-lookup"><span data-stu-id="72d3c-242">Protect your data with encryption</span></span>
> * <span data-ttu-id="72d3c-243">Abilitare il controllo del database SQL</span><span class="sxs-lookup"><span data-stu-id="72d3c-243">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="72d3c-244">Abilitare il rilevamento delle minacce per il database SQL</span><span class="sxs-lookup"><span data-stu-id="72d3c-244">Enable SQL Database threat detection</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="72d3c-245">Migliorare le prestazioni del database SQL</span><span class="sxs-lookup"><span data-stu-id="72d3c-245">Improve SQL Database performance</span></span>](sql-database-performance-tutorial.md)

