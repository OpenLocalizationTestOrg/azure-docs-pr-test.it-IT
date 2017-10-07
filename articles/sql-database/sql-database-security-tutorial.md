---
title: aaaSecure il database SQL di Azure | Documenti Microsoft
description: "Informazioni sulle tecniche e funzionalità toosecure del database SQL di Azure."
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
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a><span data-ttu-id="6494a-103">Proteggere il database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="6494a-103">Secure your Azure SQL Database</span></span>

<span data-ttu-id="6494a-104">Database SQL protegge i dati tramite la limitazione di database di access tooyour utilizzando le regole firewall, richiedere agli utenti tooprove loro identità e autorizzazione toodata tramite appartenenza basata su ruoli e autorizzazioni, nonché tramite i meccanismi di autenticazione la sicurezza a livello di riga e la maschera dati dinamica.</span><span class="sxs-lookup"><span data-stu-id="6494a-104">SQL Database secures your data by limiting access tooyour database using firewall rules, authentication mechanisms requiring users tooprove their identity, and authorization toodata through role-based memberships and permissions, as well as through row-level security and dynamic data masking.</span></span>

<span data-ttu-id="6494a-105">È possibile migliorare la protezione hello del database rispetto a utenti malintenzionati o di accesso non autorizzato con pochi semplici passaggi.</span><span class="sxs-lookup"><span data-stu-id="6494a-105">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="6494a-106">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="6494a-106">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="6494a-107">Impostare le regole firewall di livello server per il server in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6494a-107">Set up server-level firewall rules for your server in hello Azure portal</span></span>
> * <span data-ttu-id="6494a-108">Configurare regole del firewall a livello di database per il database con SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="6494a-108">Set up database-level firewall rules for your database using SSMS</span></span>
> * <span data-ttu-id="6494a-109">La connessione a database tooyour utilizzando una stringa di connessione protetta</span><span class="sxs-lookup"><span data-stu-id="6494a-109">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="6494a-110">Gestire l'accesso utente</span><span class="sxs-lookup"><span data-stu-id="6494a-110">Manage user access</span></span>
> * <span data-ttu-id="6494a-111">Proteggere i dati con la crittografia</span><span class="sxs-lookup"><span data-stu-id="6494a-111">Protect your data with encryption</span></span>
> * <span data-ttu-id="6494a-112">Abilitare il controllo del database SQL</span><span class="sxs-lookup"><span data-stu-id="6494a-112">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="6494a-113">Abilitare il rilevamento delle minacce per il database SQL</span><span class="sxs-lookup"><span data-stu-id="6494a-113">Enable SQL Database threat detection</span></span>

<span data-ttu-id="6494a-114">Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="6494a-114">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6494a-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6494a-115">Prerequisites</span></span>

<span data-ttu-id="6494a-116">toocomplete questa esercitazione, verificare che si dispone hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="6494a-116">toocomplete this tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="6494a-117">Versione più recente di hello installato di [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="6494a-117">Installed hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> 
- <span data-ttu-id="6494a-118">Installato Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="6494a-118">Installed Microsoft Excel</span></span>
- <span data-ttu-id="6494a-119">Creato un server SQL di Azure e un database, vedere [creare un database SQL di Azure nel portale di Azure hello](sql-database-get-started-portal.md), [creare un singolo database di SQL Azure mediante Azure CLI hello](sql-database-get-started-cli.md), e [creare un singolo SQL Azure database con PowerShell](sql-database-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6494a-119">Created an Azure SQL server and database - See [Create an Azure SQL database in hello Azure portal](sql-database-get-started-portal.md), [Create a single Azure SQL database using hello Azure CLI](sql-database-get-started-cli.md), and [Create a single Azure SQL database using PowerShell](sql-database-get-started-powershell.md).</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="6494a-120">Accedi toohello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6494a-120">Log in toohello Azure portal</span></span>

<span data-ttu-id="6494a-121">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6494a-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="6494a-122">Creare una regola del firewall a livello di server nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="6494a-122">Create a server-level firewall rule in hello Azure portal</span></span>

<span data-ttu-id="6494a-123">I database SQL sono protetti da un firewall in Azure.</span><span class="sxs-lookup"><span data-stu-id="6494a-123">SQL databases are protected by a firewall in Azure.</span></span> <span data-ttu-id="6494a-124">Per impostazione predefinita, tutte le connessioni toohello database e server hello all'interno di server hello vengono rifiutati, ad eccezione delle connessioni da altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="6494a-124">By default, all connections toohello server and hello databases inside hello server are rejected except for connections from other Azure services.</span></span> <span data-ttu-id="6494a-125">Per altre informazioni, vedere [Regole firewall a livello di server e di database per il database SQL di Azure](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="6494a-125">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="6494a-126">la configurazione più sicura di Hello è tooset 'Consenti l'accesso tooAzure servizi' tooOFF.</span><span class="sxs-lookup"><span data-stu-id="6494a-126">hello most secure configuration is tooset 'Allow access tooAzure services' tooOFF.</span></span> <span data-ttu-id="6494a-127">Se è necessario tooconnect toohello database da un macchina virtuale di Azure o un servizio cloud, è necessario creare un [IP riservato](../virtual-network/virtual-networks-reserved-public-ip.md) e consente solo hello riservato IP indirizzo l'accesso attraverso il firewall hello.</span><span class="sxs-lookup"><span data-stu-id="6494a-127">If you need tooconnect toohello database from an Azure VM or cloud service, you should create a [Reserved IP](../virtual-network/virtual-networks-reserved-public-ip.md) and allow only hello reserved IP address access through hello firewall.</span></span> 

<span data-ttu-id="6494a-128">Seguire questi passaggi toocreate un [regola del firewall a livello di server SQL Database](sql-database-firewall-configure.md) per le connessioni tooallow server da un indirizzo IP specifico.</span><span class="sxs-lookup"><span data-stu-id="6494a-128">Follow these steps toocreate a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server tooallow connections from a specific IP address.</span></span> 

> [!NOTE]
> <span data-ttu-id="6494a-129">Se è stato creato un database di esempio in Azure utilizzando una delle esercitazioni precedenti hello o Guide rapide e sono l'esecuzione di questa esercitazione su un computer con hello stesso indirizzo IP che si trovava al momento è esaminato in dettaglio le esercitazioni, è possibile ignorare questo passaggio poiché sarà necessario già creato una regola del firewall a livello di server.</span><span class="sxs-lookup"><span data-stu-id="6494a-129">If you have created a sample database in Azure using one of hello previous tutorials or quickstarts and are performing this tutorial on a computer with hello same IP address that it had when you walked through those tutorials, you can skip this step as you will have already created a server-level firewall rule.</span></span>
>

1. <span data-ttu-id="6494a-130">Fare clic su **database SQL** dal database hello dal menu a sinistra hello desideri tooconfigure hello regola firewall per in hello **database SQL** pagina.</span><span class="sxs-lookup"><span data-stu-id="6494a-130">Click **SQL databases** from hello left-hand menu and click hello database you would like tooconfigure hello firewall rule for on hello **SQL databases** page.</span></span> <span data-ttu-id="6494a-131">pagina di panoramica per l'apertura del database, che mostra hello completamente Hello completo del server (ad esempio **mynewserver 20170313.database.windows.net**) e offre opzioni per un'ulteriore configurazione.</span><span class="sxs-lookup"><span data-stu-id="6494a-131">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![Regola del firewall del server](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. <span data-ttu-id="6494a-133">Fare clic su **impostare firewall server** sulla barra degli strumenti hello, come illustrato nella figura precedente hello.</span><span class="sxs-lookup"><span data-stu-id="6494a-133">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="6494a-134">Hello **le impostazioni del Firewall** verrà visualizzata la pagina per il server di Database SQL di hello.</span><span class="sxs-lookup"><span data-stu-id="6494a-134">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

3. <span data-ttu-id="6494a-135">Fare clic su **Aggiungi indirizzo IP del client** hello barra degli strumenti tooadd hello indirizzo IP pubblico del portale di toohello connesso hello computer con o immettere manualmente regola del firewall hello e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="6494a-135">Click **Add client IP** on hello toolbar tooadd hello public IP address of hello computer connected toohello portal with or enter hello firewall rule manually and then click **Save**.</span></span>

      ![Impostare la regola del firewall del server](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. <span data-ttu-id="6494a-137">Fare clic su **OK** e quindi fare clic su hello **X** tooclose hello **le impostazioni del Firewall** pagina.</span><span class="sxs-lookup"><span data-stu-id="6494a-137">Click **OK** and then click hello **X** tooclose hello **Firewall settings** page.</span></span>

<span data-ttu-id="6494a-138">È ora possibile connettersi a database tooany nel server di hello con hello specificato intervallo di indirizzi IP o l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="6494a-138">You can now connect tooany database in hello server with hello specified IP address or IP address range.</span></span>

> [!NOTE]
> <span data-ttu-id="6494a-139">Il database SQL comunica attraverso la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="6494a-139">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="6494a-140">Se si sta tentando di tooconnect da una rete aziendale, può non essere consentito il traffico in uscita sulla porta 1433 dal firewall della rete.</span><span class="sxs-lookup"><span data-stu-id="6494a-140">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="6494a-141">In questo caso, non sarà server di Database SQL di Azure in grado di tooconnect tooyour, a meno che il reparto IT consente di aprire la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="6494a-141">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a><span data-ttu-id="6494a-142">Creare una regola del firewall a livello di database con SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="6494a-142">Create a database-level firewall rule using SSMS</span></span>

<span data-ttu-id="6494a-143">Le regole del firewall a livello di database consentono di impostazioni di firewall diverso toocreate per database diversi all'interno di hello stesso firewall logico di server e toocreate regole che possono essere trasferiti, vale a dire che seguono database hello durante un [failover ](sql-database-geo-replication-overview.md) invece di essere archiviate sul server SQL hello.</span><span class="sxs-lookup"><span data-stu-id="6494a-143">Database-level firewall rules enable you toocreate different firewall settings for different databases within hello same logical server and toocreate firewall rules that are portable - meaning that they follow hello database during a [failover](sql-database-geo-replication-overview.md) rather than being stored on hello SQL server.</span></span> <span data-ttu-id="6494a-144">Le regole del firewall a livello di database possono essere solo configurata utilizzando istruzioni Transact-SQL e solo dopo aver configurato prima regola del firewall di livello server hello.</span><span class="sxs-lookup"><span data-stu-id="6494a-144">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured hello first server-level firewall rule.</span></span> <span data-ttu-id="6494a-145">Per altre informazioni, vedere [Regole firewall a livello di server e di database per il database SQL di Azure](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="6494a-145">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="6494a-146">Di seguito questi toocreate passaggi una regola del firewall specifico del database.</span><span class="sxs-lookup"><span data-stu-id="6494a-146">Follows these steps toocreate a database-specific firewall rule.</span></span>

1. <span data-ttu-id="6494a-147">La connessione a database tooyour, ad esempio usando [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="6494a-147">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span></span>

2. <span data-ttu-id="6494a-148">In Esplora oggetti fare clic sul database hello da tooadd un firewall della regola e fare clic su **nuova Query**.</span><span class="sxs-lookup"><span data-stu-id="6494a-148">In Object Explorer, right-click on hello database you want tooadd a firewall rule for and click **New Query**.</span></span> <span data-ttu-id="6494a-149">Query vuota viene visualizzata una finestra che è connesso tooyour database.</span><span class="sxs-lookup"><span data-stu-id="6494a-149">A blank query window opens that is connected tooyour database.</span></span>

3. <span data-ttu-id="6494a-150">Nella finestra query hello modificare hello tooyour pubblica indirizzo IP ed eseguire hello seguente query:</span><span class="sxs-lookup"><span data-stu-id="6494a-150">In hello query window, modify hello IP address tooyour public IP address and then execute hello following query:</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. <span data-ttu-id="6494a-151">Sulla barra degli strumenti hello, fare clic su **Execute** regola del firewall toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="6494a-151">On hello toolbar, click **Execute** toocreate hello firewall rule.</span></span>

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a><span data-ttu-id="6494a-152">Visualizzare come tooconnect tooyour un'applicazione di database utilizzando una stringa di connessione protetta</span><span class="sxs-lookup"><span data-stu-id="6494a-152">View how tooconnect an application tooyour database using a secure connection string</span></span>

<span data-ttu-id="6494a-153">tooensure una connessione crittografata protetta tra un'applicazione client e il Database SQL, la stringa di connessione hello è toobe configurato per:</span><span class="sxs-lookup"><span data-stu-id="6494a-153">tooensure a secure, encrypted connection between a client application and SQL Database, hello connection string has toobe configured to:</span></span>

- <span data-ttu-id="6494a-154">Richiedere una connessione crittografata, e</span><span class="sxs-lookup"><span data-stu-id="6494a-154">Request an encrypted connection, and</span></span>
- <span data-ttu-id="6494a-155">toonot hello un certificato server attendibile.</span><span class="sxs-lookup"><span data-stu-id="6494a-155">toonot trust hello server certificate.</span></span> 

<span data-ttu-id="6494a-156">Si stabilisce una connessione utilizzando Transport Layer Security (TLS) e si riduce il rischio di hello di attacchi man-in-the-middle.</span><span class="sxs-lookup"><span data-stu-id="6494a-156">This establishes a connection using Transport Layer Security (TLS) and reduces hello risk of man-in-the-middle attacks.</span></span> <span data-ttu-id="6494a-157">È possibile ottenere stringhe di connessione configurati correttamente per il Database SQL per client supportati i driver da hello portale di Azure come illustrato per ADO.net in questa schermata.</span><span class="sxs-lookup"><span data-stu-id="6494a-157">You can obtain correctly configured connection strings for your SQL Database for supported client drivers from hello Azure portal as shown for ADO.net in this screenshot.</span></span>

1. <span data-ttu-id="6494a-158">Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina.</span><span class="sxs-lookup"><span data-stu-id="6494a-158">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span>

2. <span data-ttu-id="6494a-159">In hello **Panoramica** pagina per il database, fare clic su **Mostra le stringhe di connessione di database**.</span><span class="sxs-lookup"><span data-stu-id="6494a-159">On hello **Overview** page for your database, click **Show database connection strings**.</span></span>

3. <span data-ttu-id="6494a-160">Hello revisione completa **ADO.NET** stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="6494a-160">Review hello complete **ADO.NET** connection string.</span></span>

    ![Stringa di connessione ADO.NET](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a><span data-ttu-id="6494a-162">Creazione degli utenti del database</span><span class="sxs-lookup"><span data-stu-id="6494a-162">Creating database users</span></span>

<span data-ttu-id="6494a-163">Prima di creare gli utenti, è innanzitutto necessario scegliere uno dei due tipi di autenticazione supportati dal database SQL di Azure:</span><span class="sxs-lookup"><span data-stu-id="6494a-163">Before creating any users, you must first choose from one of two authentication types supported by Azure SQL Database:</span></span> 

<span data-ttu-id="6494a-164">**L'autenticazione di SQL**, che utilizza il nome utente e password per gli account di accesso e gli utenti che sono validi solo in hello contesto di un database specifico all'interno di un server logico.</span><span class="sxs-lookup"><span data-stu-id="6494a-164">**SQL Authentication**, which uses username and password for logins and users that are valid only in hello context of a specific database within a logical server.</span></span> 

<span data-ttu-id="6494a-165">**Autenticazione di Azure Active Directory**, che usa identità gestite da Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6494a-165">**Azure Active Directory Authentication**, which uses identities managed by Azure Active Directory.</span></span> 

<span data-ttu-id="6494a-166">Se si desidera toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate sul Database SQL, deve esistere un popolato Azure Active Directory prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="6494a-166">If you want toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate against SQL Database, a populated Azure Active Directory must exist before you can proceed.</span></span>

<span data-ttu-id="6494a-167">Seguire questi passaggi toocreate un utente tramite l'autenticazione di SQL:</span><span class="sxs-lookup"><span data-stu-id="6494a-167">Follow these steps toocreate a user using SQL Authentication:</span></span>

1. <span data-ttu-id="6494a-168">La connessione a database tooyour, ad esempio usando [SQL Server Management Studio](./sql-database-connect-query-ssms.md) utilizzando le credenziali di amministratore del server.</span><span class="sxs-lookup"><span data-stu-id="6494a-168">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) using your server admin credentials.</span></span>

2. <span data-ttu-id="6494a-169">In Esplora oggetti fare clic sul database hello desiderata tooadd un nuovo utente nella, quindi scegliere **nuova Query**.</span><span class="sxs-lookup"><span data-stu-id="6494a-169">In Object Explorer, right-click on hello database you want tooadd a new user on and click **New Query**.</span></span> <span data-ttu-id="6494a-170">Query vuota viene visualizzata una finestra che è connesso toohello di database selezionato.</span><span class="sxs-lookup"><span data-stu-id="6494a-170">A blank query window opens that is connected toohello selected database.</span></span>

3. <span data-ttu-id="6494a-171">Nella finestra query hello immettere hello seguente query:</span><span class="sxs-lookup"><span data-stu-id="6494a-171">In hello query window, enter hello following query:</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. <span data-ttu-id="6494a-172">Sulla barra degli strumenti hello, fare clic su **Execute** utente hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="6494a-172">On hello toolbar, click **Execute** toocreate hello user.</span></span>

5. <span data-ttu-id="6494a-173">Per impostazione predefinita, utente hello può connettersi toohello database, ma non dispone di autorizzazioni tooread o scrittura dati.</span><span class="sxs-lookup"><span data-stu-id="6494a-173">By default, hello user can connect toohello database, but has no permissions tooread or write data.</span></span> <span data-ttu-id="6494a-174">toogrant toohello queste autorizzazioni utente appena creato, eseguire hello seguenti due comandi in una nuova finestra query</span><span class="sxs-lookup"><span data-stu-id="6494a-174">toogrant these permissions toohello newly created user, execute hello following two commands in a new query window</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

<span data-ttu-id="6494a-175">È migliore toocreate pratica questi account non amministratore in tooyour tooconnect livello di database hello del database a meno che non è necessario tooexecute di attività amministrative quali la creazione di nuovi utenti.</span><span class="sxs-lookup"><span data-stu-id="6494a-175">It is best practice toocreate these non-administrator accounts at hello database level tooconnect tooyour database unless you need tooexecute administrator tasks like creating new users.</span></span> <span data-ttu-id="6494a-176">Consultare hello [esercitazione di Azure Active Directory](./sql-database-aad-authentication-configure.md) sulla tooauthenticate tramite Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6494a-176">Please review hello [Azure Active Directory tutorial](./sql-database-aad-authentication-configure.md) on how tooauthenticate using Azure Active Directory.</span></span>


## <a name="protect-your-data-with-encryption"></a><span data-ttu-id="6494a-177">Proteggere i dati con la crittografia</span><span class="sxs-lookup"><span data-stu-id="6494a-177">Protect your data with encryption</span></span>

<span data-ttu-id="6494a-178">Crittografia trasparente dei dati del Database di SQL Azure (TDE) crittografa automaticamente i dati inattivi, senza eventuali modifiche toohello applicazione accesso hello database crittografato.</span><span class="sxs-lookup"><span data-stu-id="6494a-178">Azure SQL Database transparent data encryption (TDE) automatically encrypts your data at rest, without requiring any changes toohello application accessing hello encrypted database.</span></span> <span data-ttu-id="6494a-179">Per i nuovi database creati, la crittografia TDE è attiva per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="6494a-179">For newly created databases, TDE is on by default.</span></span> <span data-ttu-id="6494a-180">tooenable TDE per il database o tooverify che TDE è attivo, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="6494a-180">tooenable TDE for your database or tooverify that TDE is on, follow these steps:</span></span>

1. <span data-ttu-id="6494a-181">Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina.</span><span class="sxs-lookup"><span data-stu-id="6494a-181">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="6494a-182">Fare clic su **crittografia dati trasparente** pagina di configurazione di hello tooopen per Transparent Data Encryption.</span><span class="sxs-lookup"><span data-stu-id="6494a-182">Click on **Transparent data encryption** tooopen hello configuration page for TDE.</span></span>

    ![Transparent Data Encryption](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. <span data-ttu-id="6494a-184">Se necessario, impostare **la crittografia dei dati** tooON e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="6494a-184">If necessary, set **Data encryption** tooON and click **Save**.</span></span>

<span data-ttu-id="6494a-185">il processo di crittografia Hello viene avviato in background hello.</span><span class="sxs-lookup"><span data-stu-id="6494a-185">hello encryption process starts in hello background.</span></span> <span data-ttu-id="6494a-186">È possibile monitorare lo stato di avanzamento hello tramite connessione tooSQL Database [SQL Server Management Studio](./sql-database-connect-query-ssms.md) eseguendo una query sulla colonna encryption_state hello di hello `sys.dm_database_encryption_keys` visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="6494a-186">You can monitor hello progress by connecting tooSQL Database using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) by querying hello encryption_state column of hello `sys.dm_database_encryption_keys` view.</span></span>

## <a name="enable-sql-database-auditing-if-necessary"></a><span data-ttu-id="6494a-187">Abilitare il controllo del database SQL, se necessario</span><span class="sxs-lookup"><span data-stu-id="6494a-187">Enable SQL Database auditing, if necessary</span></span>

<span data-ttu-id="6494a-188">Controllo del Database SQL Azure tiene traccia degli eventi di database e li scrive i log di controllo tooan nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6494a-188">Azure SQL Database Auditing tracks database events and writes them tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="6494a-189">Il controllo consente di agevolare la conformità alle normative, comprendere le attività del database e ottenere informazioni su eventuali discrepanze e anomalie che potrebbero indicare potenziali violazioni della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="6494a-189">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate potential security violations.</span></span> <span data-ttu-id="6494a-190">Seguire questi toocreate passaggi un criterio di controllo predefinito per il database SQL:</span><span class="sxs-lookup"><span data-stu-id="6494a-190">Follow these steps toocreate a default auditing policy for your SQL database:</span></span>

1. <span data-ttu-id="6494a-191">Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina.</span><span class="sxs-lookup"><span data-stu-id="6494a-191">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="6494a-192">Nel pannello impostazioni hello, selezionare **controllo e rilevamento minacce**.</span><span class="sxs-lookup"><span data-stu-id="6494a-192">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> <span data-ttu-id="6494a-193">Si noti che il controllo a livello di server è /bGli e che sia presente un **visualizzare impostazioni del server** collegamento che consente di tooview o modifica le impostazioni controllo hello server da questo contesto.</span><span class="sxs-lookup"><span data-stu-id="6494a-193">Notice that sever-level auditing is diabled and that there is a **View server settings** link that allows you tooview or modify hello server auditing settings from this context.</span></span>

    ![Pannello di controllo](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. <span data-ttu-id="6494a-195">Se si preferisce tooenable un controllo tipo (percorso o?) diverso da hello uno specificato a livello di server hello, attivare **ON** controllo, scegliere hello **Blob** tipo di controllo.</span><span class="sxs-lookup"><span data-stu-id="6494a-195">If you prefer tooenable an Audit type (or location?) different from hello one specified at hello server level, turn **ON** Auditing, and choose hello **Blob** Auditing Type.</span></span> <span data-ttu-id="6494a-196">Se il servizio controllo Blob server è abilitato, controllo del database configurate hello esisterà in modo affiancato con controllo del Blob hello server.</span><span class="sxs-lookup"><span data-stu-id="6494a-196">If server Blob auditing is enabled, hello database configured audit will exist side by side with hello server Blob audit.</span></span>

    ![Attivare il controllo](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. <span data-ttu-id="6494a-198">Selezionare **dettagli archiviazione** hello tooopen Pannello di controllo log di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6494a-198">Select **Storage Details** tooopen hello Audit Logs Storage Blade.</span></span> <span data-ttu-id="6494a-199">Account di archiviazione di Azure selezionare hello in cui verranno salvati i log e il periodo di memorizzazione hello, dopo il quale hello verranno eliminati i log precedenti, quindi fare clic su **OK** nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="6494a-199">Select hello Azure storage account where logs will be saved, and hello retention period, after which hello old logs will be deleted, then click **OK** at hello bottom.</span></span> 

   > [!TIP]
   > <span data-ttu-id="6494a-200">Utilizzare hello stesso account di archiviazione per tutti i hello di tooget database controllati meglio hello controllo modelli di report.</span><span class="sxs-lookup"><span data-stu-id="6494a-200">Use hello same storage account for all audited databases tooget hello most out of hello auditing reports templates.</span></span>
   > 

5. <span data-ttu-id="6494a-201">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="6494a-201">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6494a-202">Se si desidera che gli eventi controllato hello toocustomize, è possibile farlo tramite PowerShell o l'API REST, vedere hello [automazione (PowerShell / API REST)](sql-database-auditing.md#subheading-7) sezione per ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="6494a-202">If you want toocustomize hello audited events, you can do this via PowerShell or REST API - see hello [Automation (PowerShell / REST API)](sql-database-auditing.md#subheading-7) section for more details.</span></span>
>

## <a name="enable-sql-database-threat-detection"></a><span data-ttu-id="6494a-203">Abilitare il rilevamento delle minacce per il database SQL</span><span class="sxs-lookup"><span data-stu-id="6494a-203">Enable SQL Database threat detection</span></span>

<span data-ttu-id="6494a-204">Rilevamento minacce fornisce un nuovo livello di sicurezza, che consente ai clienti toodetect e risposta toopotential minacce che si verificano fornendo gli avvisi di sicurezza sull'attività anomale.</span><span class="sxs-lookup"><span data-stu-id="6494a-204">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="6494a-205">Agli utenti di esplorare gli eventi di hello sospette tramite controllo del Database SQL toodetermine se ottenuto tooaccess un tentativo, violazione o sfruttare i dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="6494a-205">Users can explore hello suspicious events using SQL Database Auditing toodetermine if they result from an attempt tooaccess, breach or exploit data in hello database.</span></span> <span data-ttu-id="6494a-206">Rilevamento minacce rende semplice tooaddress potenziali minacce toohello database di senza necessità di hello toobe un esperto della sicurezza o gestire i sistemi di monitoraggio di sicurezza avanzata.</span><span class="sxs-lookup"><span data-stu-id="6494a-206">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>
<span data-ttu-id="6494a-207">Ad esempio, la funzionalità di rilevamento delle minacce individua determinate attività anomale nel database che indicano potenziali tentativi di attacco SQL injection.</span><span class="sxs-lookup"><span data-stu-id="6494a-207">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="6494a-208">Attacchi SQL injection è uno dei hello Web sicurezza problemi delle applicazioni su Internet, le applicazioni utilizzate tooattack basati sui dati hello.</span><span class="sxs-lookup"><span data-stu-id="6494a-208">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="6494a-209">Gli utenti malintenzionati sfruttano applicazione vulnerabilità tooinject dannoso istruzioni SQL in campi di immissione di applicazione, per sugli o la modifica dei dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="6494a-209">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

1. <span data-ttu-id="6494a-210">Passare a pannello di configurazione toohello di database SQL da toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="6494a-210">Navigate toohello configuration blade of hello SQL database you want toomonitor.</span></span> <span data-ttu-id="6494a-211">Nel pannello impostazioni hello, selezionare **controllo e rilevamento minacce**.</span><span class="sxs-lookup"><span data-stu-id="6494a-211">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>

    ![Riquadro di spostamento](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. <span data-ttu-id="6494a-213">In hello **controllo e rilevamento minacce** configurazione pannello turn **ON** controllo, che visualizza le impostazioni di rilevamento minacce hello.</span><span class="sxs-lookup"><span data-stu-id="6494a-213">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello threat detection settings.</span></span>

3. <span data-ttu-id="6494a-214">Impostare il rilevamento delle minacce su **SÌ**.</span><span class="sxs-lookup"><span data-stu-id="6494a-214">Turn **ON** threat detection.</span></span>

4. <span data-ttu-id="6494a-215">Configurare l'elenco di hello di messaggi di posta elettronica che riceveranno gli avvisi di sicurezza al rilevamento di attività del database anomale.</span><span class="sxs-lookup"><span data-stu-id="6494a-215">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>

5. <span data-ttu-id="6494a-216">Fare clic su **salvare** in hello **rilevamento controllo & minaccia** toosave pannello hello nuovi o aggiornati criteri di rilevamento di controllo e minacce.</span><span class="sxs-lookup"><span data-stu-id="6494a-216">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection policy.</span></span>

    ![Riquadro di spostamento](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    <span data-ttu-id="6494a-218">Se vengono rilevate attività anomale del database, si riceverà una notifica tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="6494a-218">If anomalous database activities are detected, you will receive an email notification upon detection of anomalous database activities.</span></span> <span data-ttu-id="6494a-219">messaggio di posta elettronica Hello verrà fornite informazioni sull'evento sospetti hello inclusi natura hello di attività anomale hello, nome del database, l'ora dell'evento hello nome e il server.</span><span class="sxs-lookup"><span data-stu-id="6494a-219">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="6494a-220">Inoltre, verranno fornite informazioni sulle possibili cause e consigliabile tooinvestigate azioni e ridurre database toohello minaccia potenziale di hello.</span><span class="sxs-lookup"><span data-stu-id="6494a-220">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span> <span data-ttu-id="6494a-221">percorso passaggi successiva Hello tramite quali toodo occorre si ricevono un messaggio di posta di questo tipo:</span><span class="sxs-lookup"><span data-stu-id="6494a-221">hello next steps walk you through what toodo should you receive such an email:</span></span>

    ![Messaggio di posta elettronica sul rilevamento delle minacce](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. <span data-ttu-id="6494a-223">Nel messaggio di posta elettronica di hello, fare clic su hello **Log di controllo di SQL Azure** collegamento, che consente di avviare hello portale di Azure e visualizzare i record di controllo pertinente hello alla ora hello di eventi sospetti hello.</span><span class="sxs-lookup"><span data-stu-id="6494a-223">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure portal and show hello relevant auditing records around hello time of hello suspicious event.</span></span>

    ![Record di controllo](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. <span data-ttu-id="6494a-225">Fare clic su tooview record di controllo hello ulteriori informazioni sulle attività sospette database hello, ad esempio l'istruzione SQL, IP client e motivo di errore.</span><span class="sxs-lookup"><span data-stu-id="6494a-225">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>

    ![Dettagli sui record](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. <span data-ttu-id="6494a-227">Nel Pannello di controllo Registra hello, fare clic su **Apri in Excel** tooopen preconfigurata che excel tooimport modello e eseguire un'analisi più approfondita del log di controllo hello alla ora hello di eventi sospetti hello.</span><span class="sxs-lookup"><span data-stu-id="6494a-227">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6494a-228">In Excel 2010 o versioni successive Power Query e hello **combinazione rapida** impostazione è obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="6494a-228">In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required.</span></span>

    ![Aprire i record in Excel](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. <span data-ttu-id="6494a-230">hello tooconfigure **combinazione rapida** impostazione - hello **POWER QUERY** scheda della barra multifunzione selezionare **opzioni** finestra di dialogo Opzioni toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="6494a-230">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="6494a-231">Selezionare hello Privacy sezione e scegliere l'opzione secondo hello - 'Ignora i livelli di Privacy hello e potenziale miglioramento delle prestazioni':</span><span class="sxs-lookup"><span data-stu-id="6494a-231">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>

    ![Combinazione rapida di Excel](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. <span data-ttu-id="6494a-233">log di controllo SQL tooload, assicurarsi che i parametri di hello nella scheda Impostazioni hello siano impostati correttamente e quindi selezionare barra multifunzione 'Data' hello e fare clic sul pulsante 'Aggiorna tutto' hello.</span><span class="sxs-lookup"><span data-stu-id="6494a-233">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>

    ![Parametri di Excel](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. <span data-ttu-id="6494a-235">Hello risultati vengono visualizzati in hello **i log di controllo SQL** foglio che consente l'analisi più approfondita di toorun di attività anomale di hello che sono stati rilevati e ridurre l'impatto hello di eventi di protezione hello nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6494a-235">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6494a-236">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6494a-236">Next steps</span></span>
<span data-ttu-id="6494a-237">È possibile migliorare la protezione hello del database rispetto a utenti malintenzionati o di accesso non autorizzato con pochi semplici passaggi.</span><span class="sxs-lookup"><span data-stu-id="6494a-237">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="6494a-238">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="6494a-238">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="6494a-239">Configurare le regole del firewall per il server e/o il database</span><span class="sxs-lookup"><span data-stu-id="6494a-239">Set up firewall rules for your sever and or database</span></span>
> * <span data-ttu-id="6494a-240">La connessione a database tooyour utilizzando una stringa di connessione protetta</span><span class="sxs-lookup"><span data-stu-id="6494a-240">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="6494a-241">Gestire l'accesso utente</span><span class="sxs-lookup"><span data-stu-id="6494a-241">Manage user access</span></span>
> * <span data-ttu-id="6494a-242">Proteggere i dati con la crittografia</span><span class="sxs-lookup"><span data-stu-id="6494a-242">Protect your data with encryption</span></span>
> * <span data-ttu-id="6494a-243">Abilitare il controllo del database SQL</span><span class="sxs-lookup"><span data-stu-id="6494a-243">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="6494a-244">Abilitare il rilevamento delle minacce per il database SQL</span><span class="sxs-lookup"><span data-stu-id="6494a-244">Enable SQL Database threat detection</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="6494a-245">Migliorare le prestazioni del database SQL</span><span class="sxs-lookup"><span data-stu-id="6494a-245">Improve SQL Database performance</span></span>](sql-database-performance-tutorial.md)

