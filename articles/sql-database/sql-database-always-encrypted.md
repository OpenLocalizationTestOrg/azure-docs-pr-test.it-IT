---
title: 'Always Encrypted: database SQL di Azure - Archivio certificati di Windows | Documentazione Microsoft'
description: Questo articolo illustra come proteggere i dati sensibili in un database SQL con la crittografia del database usando la procedura guidata Always Encrypted di SQL Server Management Studio (SSMS). Descrive anche l'archiviazione delle chiavi di crittografia nell'archivio certificati di Windows.
keywords: crittografia dati, crittografia sql, crittografia database, dati sensibili, crittografia sempre attiva
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: ce7e052e-8bf6-4d7c-9204-4c6f4afeba4b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: sstein
ms.openlocfilehash: d1fdfc4f739e65ff532b159eefaffe1622ad0963
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-the-windows-certificate-store"></a><span data-ttu-id="49af7-105">Crittografia sempre attiva: Proteggere i dati sensibili nel database SQL e archiviare le chiavi di crittografia nell'archivio certificati di Windows</span><span class="sxs-lookup"><span data-stu-id="49af7-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in the Windows certificate store</span></span>

<span data-ttu-id="49af7-106">Questo articolo illustra come proteggere i dati sensibili in un database SQL con la crittografia del database tramite la [procedura guidata Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) di [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="49af7-106">This article shows you how to secure sensitive data in a SQL database with database encryption by using the [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="49af7-107">Descrive anche l'archiviazione delle chiavi di crittografia nell'archivio certificati di Windows.</span><span class="sxs-lookup"><span data-stu-id="49af7-107">It also shows you how to store your encryption keys in the Windows certificate store.</span></span>

<span data-ttu-id="49af7-108">La crittografia sempre attiva è una nuova tecnologia di crittografia dei dati del database SQL di Azure e di SQL Server, che protegge i dati sensibili inattivi sul server durante lo spostamento tra client e server e durante l'uso, assicurando che i dati sensibili non vengano mai visualizzati come testo non crittografato all'interno del sistema di database.</span><span class="sxs-lookup"><span data-stu-id="49af7-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on the server, during movement between client and server, and while the data is in use, ensuring that sensitive data never appears as plaintext inside the database system.</span></span> <span data-ttu-id="49af7-109">Dopo avere crittografato i dati solo le applicazioni client o i server applicazioni, che hanno accesso alle chiavi, possono accedere ai dati di testo non crittografato.</span><span class="sxs-lookup"><span data-stu-id="49af7-109">After you encrypt data, only client applications or app servers that have access to the keys can access plaintext data.</span></span> <span data-ttu-id="49af7-110">Per informazioni dettagliate, vedere l'articolo relativo alla [crittografia sempre attiva (motore di database)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="49af7-110">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="49af7-111">Dopo avere configurato il database per usare la crittografia sempre attiva, viene creata un'applicazione client in C# con Visual Studio per lavorare con i dati crittografati.</span><span class="sxs-lookup"><span data-stu-id="49af7-111">After configuring the database to use Always Encrypted, you will create a client application in C# with Visual Studio to work with the encrypted data.</span></span>

<span data-ttu-id="49af7-112">Seguire i passaggi in questo articolo per imparare come configurare la crittografia sempre attiva per un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="49af7-112">Follow the steps in this article to learn how to set up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="49af7-113">Questo articolo spiega come eseguire le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="49af7-113">In this article, you will learn how to perform the following tasks:</span></span>

* <span data-ttu-id="49af7-114">Usare la procedura guidata per la crittografia sempre attiva in SSMS per creare [chiavi con crittografia sempre attiva](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="49af7-114">Use the Always Encrypted wizard in SSMS to create [Always Encrypted Keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="49af7-115">Creare una [chiave master di colonna (CMK, Column Master Key)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="49af7-115">Create a [Column Master Key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="49af7-116">Creare una [chiave di crittografia di colonna (CEK, Column Encryption Key)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="49af7-116">Create a [Column Encryption Key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="49af7-117">Creare una tabella di database e crittografare le colonne.</span><span class="sxs-lookup"><span data-stu-id="49af7-117">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="49af7-118">Creare un'applicazione che inserisce, seleziona e visualizza i dati delle colonne crittografate.</span><span class="sxs-lookup"><span data-stu-id="49af7-118">Create an application that inserts, selects, and displays data from the encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49af7-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="49af7-119">Prerequisites</span></span>
<span data-ttu-id="49af7-120">Per questa esercitazione occorrono:</span><span class="sxs-lookup"><span data-stu-id="49af7-120">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="49af7-121">Un account e una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="49af7-121">An Azure account and subscription.</span></span> <span data-ttu-id="49af7-122">Nel caso in cui non siano disponibili, è possibile usare una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49af7-122">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="49af7-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versione 13.0.700.242 o successive.</span><span class="sxs-lookup"><span data-stu-id="49af7-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="49af7-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) o versioni successive (nel computer client).</span><span class="sxs-lookup"><span data-stu-id="49af7-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on the client computer).</span></span>
* <span data-ttu-id="49af7-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="49af7-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="49af7-126">Creare un database SQL vuoto</span><span class="sxs-lookup"><span data-stu-id="49af7-126">Create a blank SQL database</span></span>
1. <span data-ttu-id="49af7-127">Accedere al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="49af7-127">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="49af7-128">Fare clic su **Nuovo** > **Dati e archiviazione** > **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="49af7-128">Click **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="49af7-129">Creare un database **vuoto** denominato **Clinic** in un server nuovo o esistente.</span><span class="sxs-lookup"><span data-stu-id="49af7-129">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="49af7-130">Per istruzioni dettagliate sulla creazione di un database nel portale di Azure, vedere [Primo database SQL di Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="49af7-130">For detailed instructions about creating a database in the Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Creazione di un database vuoto](./media/sql-database-always-encrypted/create-database.png)

<span data-ttu-id="49af7-132">La stringa di connessione sarà necessaria più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="49af7-132">You will need the connection string later in the tutorial.</span></span> <span data-ttu-id="49af7-133">Dopo avere creato il database passare al nuovo database Clinic e copiare la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="49af7-133">After the database is created, go to the new Clinic database and copy the connection string.</span></span> <span data-ttu-id="49af7-134">È possibile ottenere la stringa di connessione in qualsiasi momento, ma è facile copiarla quando ci si trova nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="49af7-134">You can get the connection string at any time, but it's easy to copy it when you're in the Azure portal.</span></span>

1. <span data-ttu-id="49af7-135">Fare clic su **Database SQL** > **Clinic** > **Mostra stringhe di connessione del database**.</span><span class="sxs-lookup"><span data-stu-id="49af7-135">Click **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="49af7-136">Copiare la stringa di connessione per **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="49af7-136">Copy the connection string for **ADO.NET**.</span></span>
   
    ![Copia della stringa di connessione](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-to-the-database-with-ssms"></a><span data-ttu-id="49af7-138">Connettersi al database con SSMS</span><span class="sxs-lookup"><span data-stu-id="49af7-138">Connect to the database with SSMS</span></span>
<span data-ttu-id="49af7-139">Aprire SSMS e connettersi al server con il database Clinic.</span><span class="sxs-lookup"><span data-stu-id="49af7-139">Open SSMS and connect to the server with the Clinic database.</span></span>

1. <span data-ttu-id="49af7-140">Aprire SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="49af7-140">Open SSMS.</span></span> <span data-ttu-id="49af7-141">Fare clic su **Connetti** > **Motore di database** per aprire la finestra **Connetti al server**, se non è già aperta.</span><span class="sxs-lookup"><span data-stu-id="49af7-141">(Click **Connect** > **Database Engine** to open the **Connect to Server** window if it is not open).</span></span>
2. <span data-ttu-id="49af7-142">Immettere il nome e le credenziali del server.</span><span class="sxs-lookup"><span data-stu-id="49af7-142">Enter your server name and credentials.</span></span> <span data-ttu-id="49af7-143">Il nome del server è disponibile nel pannello del database SQL e nella stringa di connessione copiata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="49af7-143">The server name can be found on the SQL database blade and in the connection string you copied earlier.</span></span> <span data-ttu-id="49af7-144">Digitare il nome completo del server, compreso *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="49af7-144">Type the complete server name including *database.windows.net*.</span></span>
   
    ![Copia della stringa di connessione](./media/sql-database-always-encrypted/ssms-connect.png)

<span data-ttu-id="49af7-146">Se viene visualizzata la finestra **Nuova regola firewall** , accedere ad Azure e lasciare che SSMS crei una nuova regola firewall per l'utente.</span><span class="sxs-lookup"><span data-stu-id="49af7-146">If the **New Firewall Rule** window opens, sign in to Azure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="49af7-147">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="49af7-147">Create a table</span></span>
<span data-ttu-id="49af7-148">Questa sezione contiene istruzioni per creare una tabella con i dati dei pazienti.</span><span class="sxs-lookup"><span data-stu-id="49af7-148">In this section, you will create a table to hold patient data.</span></span> <span data-ttu-id="49af7-149">Sarà una normale tabella inizialmente; la crittografia verrà configurata nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="49af7-149">This will be a normal table initially--you will configure encryption in the next section.</span></span>

1. <span data-ttu-id="49af7-150">Espandere **Database**.</span><span class="sxs-lookup"><span data-stu-id="49af7-150">Expand **Databases**.</span></span>
2. <span data-ttu-id="49af7-151">Fare clic con il pulsante destro del mouse sul database **Clinic** e fare clic su **Nuova query**.</span><span class="sxs-lookup"><span data-stu-id="49af7-151">Right-click the **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="49af7-152">Incollare il comando Transact-SQL (T-SQL) seguente nella finestra della nuova query ed **eseguirlo** .</span><span class="sxs-lookup"><span data-stu-id="49af7-152">Paste the following Transact-SQL (T-SQL) into the new query window and **Execute** it.</span></span>

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="49af7-153">Crittografare le colonne configurando la crittografia sempre attiva</span><span class="sxs-lookup"><span data-stu-id="49af7-153">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="49af7-154">SSMS offre una procedura guidata per configurare facilmente la crittografia sempre attiva impostando la chiave master di colonna (CMK), la chiave di crittografia di colonna (CEK) e le colonne crittografate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="49af7-154">SSMS provides a wizard to easily configure Always Encrypted by setting up the CMK, CEK, and encrypted columns for you.</span></span>

1. <span data-ttu-id="49af7-155">Espandere **Database** > **Clinic** > **Tabelle**.</span><span class="sxs-lookup"><span data-stu-id="49af7-155">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="49af7-156">Fare clic con il pulsante destro del mouse sulla tabella **Patients** e selezionare **Crittografa colonne** per aprire la procedura guidata Always Encrypted:</span><span class="sxs-lookup"><span data-stu-id="49af7-156">Right-click the **Patients** table and select **Encrypt Columns** to open the Always Encrypted wizard:</span></span>
   
    ![Crittografa colonne](./media/sql-database-always-encrypted/encrypt-columns.png)

<span data-ttu-id="49af7-158">La procedura guidata Always Encrypted include le sezioni seguenti: **Selezione colonne**, **Configurazione della chiave master** (CMK), **Convalida** e **Riepilogo**.</span><span class="sxs-lookup"><span data-stu-id="49af7-158">The Always Encrypted wizard includes the following sections: **Column Selection**, **Master Key Configuration** (CMK), **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="49af7-159">Selezione colonne</span><span class="sxs-lookup"><span data-stu-id="49af7-159">Column Selection</span></span>
<span data-ttu-id="49af7-160">Fare clic su **Avanti** nella pagina **Introduzione** per aprire la pagina **Selezione colonne**.</span><span class="sxs-lookup"><span data-stu-id="49af7-160">Click **Next** on the **Introduction** page to open the **Column Selection** page.</span></span> <span data-ttu-id="49af7-161">In questa pagina verranno selezionate le colonne da crittografare, [il tipo di crittografia e la chiave di crittografia di colonna (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) da usare.</span><span class="sxs-lookup"><span data-stu-id="49af7-161">On this page, you will select which columns you want to encrypt, [the type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) to use.</span></span>

<span data-ttu-id="49af7-162">Crittografare il **CF** e la **data di nascita** per ogni paziente.</span><span class="sxs-lookup"><span data-stu-id="49af7-162">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="49af7-163">La colonna relativa al **CF** usa la crittografia deterministica, che supporta ricerche di uguaglianza, join e raggruppamenti.</span><span class="sxs-lookup"><span data-stu-id="49af7-163">The **SSN** column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="49af7-164">La colonna relativa alla **data di nascita** usa la crittografia casuale, che non supporta le operazioni.</span><span class="sxs-lookup"><span data-stu-id="49af7-164">The **BirthDate** column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="49af7-165">Impostare il **Tipo di crittografia** per la colonna **CF** su **Deterministica** e la colonna **Data di nascita** su **Casuale**.</span><span class="sxs-lookup"><span data-stu-id="49af7-165">Set the **Encryption Type** for the **SSN** column to **Deterministic** and the **BirthDate** column to **Randomized**.</span></span> <span data-ttu-id="49af7-166">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="49af7-166">Click **Next**.</span></span>

![Crittografa colonne](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="49af7-168">Configurazione della chiave master</span><span class="sxs-lookup"><span data-stu-id="49af7-168">Master Key Configuration</span></span>
<span data-ttu-id="49af7-169">La pagina **Configurazione della chiave master** consente di impostare la CMK e selezionare il provider dell'archivio chiavi in cui verrà archiviata la CMK.</span><span class="sxs-lookup"><span data-stu-id="49af7-169">The **Master Key Configuration** page is where you set up your CMK and select the key store provider where the CMK will be stored.</span></span> <span data-ttu-id="49af7-170">Attualmente è possibile archiviare una chiave master di colonna nell'archivio certificati di Windows, nell'insieme di credenziali delle chiavi di Azure o in un modulo di protezione hardware.</span><span class="sxs-lookup"><span data-stu-id="49af7-170">Currently, you can store a CMK in the Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span> <span data-ttu-id="49af7-171">Questa esercitazione illustra come archiviare le chiavi nell'archivio certificati di Windows.</span><span class="sxs-lookup"><span data-stu-id="49af7-171">This tutorial shows how to store your keys in the Windows certificate store.</span></span>

<span data-ttu-id="49af7-172">Verificare che l'**archivio certificati di Windows** sia selezionato e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="49af7-172">Verify that **Windows certificate store** is selected and click **Next**.</span></span>

![Configurazione della chiave master](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="49af7-174">Convalida</span><span class="sxs-lookup"><span data-stu-id="49af7-174">Validation</span></span>
<span data-ttu-id="49af7-175">È attualmente possibile crittografare le colonne o salvare uno script di PowerShell da eseguire in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="49af7-175">You can encrypt the columns now or save a PowerShell script to run later.</span></span> <span data-ttu-id="49af7-176">Per questa esercitazione selezionare **Procedi per completare ora** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="49af7-176">For this tutorial, select **Proceed to finish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="49af7-177">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="49af7-177">Summary</span></span>
<span data-ttu-id="49af7-178">Verificare che tutte le impostazioni siano corrette e fare clic su **Fine** per completare la configurazione della crittografia sempre attiva.</span><span class="sxs-lookup"><span data-stu-id="49af7-178">Verify that the settings are all correct and click **Finish** to complete the setup for Always Encrypted.</span></span>

![Riepilogo](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-the-wizards-actions"></a><span data-ttu-id="49af7-180">Confermare le azioni della procedura guidata</span><span class="sxs-lookup"><span data-stu-id="49af7-180">Verify the wizard's actions</span></span>
<span data-ttu-id="49af7-181">Al termine della procedura guidata, il database è configurato per la crittografia sempre attiva.</span><span class="sxs-lookup"><span data-stu-id="49af7-181">After the wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="49af7-182">La procedura guidata esegue le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="49af7-182">The wizard performed the following actions:</span></span>

* <span data-ttu-id="49af7-183">Creare una chiave CMK.</span><span class="sxs-lookup"><span data-stu-id="49af7-183">Created a CMK.</span></span>
* <span data-ttu-id="49af7-184">Creare una chiave di crittografia di colonna (CEK).</span><span class="sxs-lookup"><span data-stu-id="49af7-184">Created a CEK.</span></span>
* <span data-ttu-id="49af7-185">Configurazione delle colonne selezionate per la crittografia.</span><span class="sxs-lookup"><span data-stu-id="49af7-185">Configured the selected columns for encryption.</span></span> <span data-ttu-id="49af7-186">La tabella **Patients** attualmente è vuota, ma eventuali dati esistenti nelle colonne selezionate sono ora crittografati.</span><span class="sxs-lookup"><span data-stu-id="49af7-186">Your **Patients** table currently has no data, but any existing data in the selected columns is now encrypted.</span></span>

<span data-ttu-id="49af7-187">È possibile verificare la creazione di chiavi in SSMS facendo clic su **Clinic** > **Sicurezza** > **Chiavi Always Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="49af7-187">You can verify the creation of the keys in SSMS by going to **Clinic** > **Security** > **Always Encrypted Keys**.</span></span> <span data-ttu-id="49af7-188">Sono ora visibili le nuove chiavi generate dalla procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="49af7-188">You can now see the new keys that the wizard generated for you.</span></span>

## <a name="create-a-client-application-that-works-with-the-encrypted-data"></a><span data-ttu-id="49af7-189">Creare un'applicazione client che funziona con i dati crittografati</span><span class="sxs-lookup"><span data-stu-id="49af7-189">Create a client application that works with the encrypted data</span></span>
<span data-ttu-id="49af7-190">Ora che la crittografia Always Encrypted è configurata, è possibile creare un'applicazione che esegua alcuni *inserimenti* e *selezioni* nelle colonne crittografate.</span><span class="sxs-lookup"><span data-stu-id="49af7-190">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on the encrypted columns.</span></span> <span data-ttu-id="49af7-191">Per eseguire correttamente l'applicazione di esempio, è necessario avviarla nello stesso computer in cui è stata eseguita la procedura guidata per la crittografia sempre attiva.</span><span class="sxs-lookup"><span data-stu-id="49af7-191">To successfully run the sample application, you must run it on the same computer where you ran the Always Encrypted wizard.</span></span> <span data-ttu-id="49af7-192">Per eseguire l'applicazione in un altro computer è necessario distribuire i certificati della crittografia sempre attiva nel computer che esegue l'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="49af7-192">To run the application on another computer, you must deploy your Always Encrypted certificates to the computer running the client app.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="49af7-193">L'applicazione deve usare oggetti [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) per trasferire dati di testo non crittografato al server con colonne con la crittografia sempre attiva.</span><span class="sxs-lookup"><span data-stu-id="49af7-193">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data to the server with Always Encrypted columns.</span></span> <span data-ttu-id="49af7-194">Il trasferimento di valori letterali senza usare oggetti SqlParameter genererà un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="49af7-194">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="49af7-195">Aprire Visual Studio e creare un'applicazione console C#.</span><span class="sxs-lookup"><span data-stu-id="49af7-195">Open Visual Studio and create a new C# console application.</span></span> <span data-ttu-id="49af7-196">Verificare che il progetto sia impostato su **.NET Framework 4.6** o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="49af7-196">Make sure your project is set to **.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="49af7-197">Denominare il progetto **AlwaysEncryptedConsoleApp** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="49af7-197">Name the project **AlwaysEncryptedConsoleApp** and click **OK**.</span></span>

![Nuova applicazione console](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-to-enable-always-encrypted"></a><span data-ttu-id="49af7-199">Modificare la stringa di connessione per abilitare la crittografia sempre attiva</span><span class="sxs-lookup"><span data-stu-id="49af7-199">Modify your connection string to enable Always Encrypted</span></span>
<span data-ttu-id="49af7-200">Questa sezione descrive come abilitare la crittografia sempre attiva nella stringa di connessione del database.</span><span class="sxs-lookup"><span data-stu-id="49af7-200">This section explains how to enable Always Encrypted in your database connection string.</span></span> <span data-ttu-id="49af7-201">Si modificherà l'app console appena creata nella sezione successiva "Applicazione console di esempio della crittografia sempre attiva".</span><span class="sxs-lookup"><span data-stu-id="49af7-201">You will modify the console app you just created in the next section, "Always Encrypted sample console application."</span></span>

<span data-ttu-id="49af7-202">Per abilitare la crittografia Always Encrypted è necessario aggiungere la parola chiave **Column Encryption Setting** alla stringa di connessione e impostarla su **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="49af7-202">To enable Always Encrypted, you need to add the **Column Encryption Setting** keyword to your connection string and set it to **Enabled**.</span></span>

<span data-ttu-id="49af7-203">È possibile impostarla direttamente nella stringa di connessione o tramite [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="49af7-203">You can set this directly in the connection string, or you can set it by using a [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="49af7-204">L'applicazione di esempio nella sezione successiva mostra come usare **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="49af7-204">The sample application in the next section shows how to use **SqlConnectionStringBuilder**.</span></span>

> [!NOTE]
> <span data-ttu-id="49af7-205">Questa è l'unica modifica specifica della crittografia sempre attiva da apportare a un'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="49af7-205">This is the only change required in a client application specific to Always Encrypted.</span></span> <span data-ttu-id="49af7-206">Se è presente un'applicazione esistente che archivia la stringa di connessione esternamente, ad esempio in un file di configurazione, è possibile abilitare la crittografia sempre attiva senza modificare il codice.</span><span class="sxs-lookup"><span data-stu-id="49af7-206">If you have an existing application that stores its connection string externally (that is, in a config file), you might be able to enable Always Encrypted without changing any code.</span></span>
> 
> 

### <a name="enable-always-encrypted-in-the-connection-string"></a><span data-ttu-id="49af7-207">Abilitare la crittografia sempre attiva nella stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="49af7-207">Enable Always Encrypted in the connection string</span></span>
<span data-ttu-id="49af7-208">Aggiungere la parola chiave seguente alla stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="49af7-208">Add the following keyword to your connection string:</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a><span data-ttu-id="49af7-209">Abilitare la crittografia sempre attiva con SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="49af7-209">Enable Always Encrypted with a SqlConnectionStringBuilder</span></span>
<span data-ttu-id="49af7-210">Il codice seguente mostra come abilitare la crittografia Always Encrypted tramite l'impostazione di [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) su [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="49af7-210">The following code shows how to enable Always Encrypted by setting the [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) to [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="49af7-211">Applicazione console di esempio della crittografia sempre attiva</span><span class="sxs-lookup"><span data-stu-id="49af7-211">Always Encrypted sample console application</span></span>
<span data-ttu-id="49af7-212">Questo esempio dimostra come:</span><span class="sxs-lookup"><span data-stu-id="49af7-212">This sample demonstrates how to:</span></span>

* <span data-ttu-id="49af7-213">Modificare la stringa di connessione per abilitare la crittografia sempre attiva.</span><span class="sxs-lookup"><span data-stu-id="49af7-213">Modify your connection string to enable Always Encrypted.</span></span>
* <span data-ttu-id="49af7-214">Inserire dati nelle colonne crittografate.</span><span class="sxs-lookup"><span data-stu-id="49af7-214">Insert data into the encrypted columns.</span></span>
* <span data-ttu-id="49af7-215">Selezionare un record filtrando in base a un valore specifico in una colonna crittografata.</span><span class="sxs-lookup"><span data-stu-id="49af7-215">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="49af7-216">Sostituire il contenuto del file **Program.cs** con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="49af7-216">Replace the contents of **Program.cs** with the following code.</span></span> <span data-ttu-id="49af7-217">Sostituire la stringa di connessione per la variabile globale connectionString nella riga immediatamente sopra il metodo Main con la stringa di connessione valida del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="49af7-217">Replace the connection string for the global connectionString variable in the line directly above the Main method with your valid connection string from the Azure portal.</span></span> <span data-ttu-id="49af7-218">Questa è l'unica modifica che è necessario apportare al codice.</span><span class="sxs-lookup"><span data-stu-id="49af7-218">This is the only change you need to make to this code.</span></span>

<span data-ttu-id="49af7-219">Eseguire l'app per vedere in azione la crittografia sempre attiva.</span><span class="sxs-lookup"><span data-stu-id="49af7-219">Run the app to see Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;

    namespace AlwaysEncryptedConsoleApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from the Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
            Console.WriteLine("Original connection string copied from the Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for the connection.
            // This is the only change specific to Always Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update the connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign the updated connection string to our global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records to restart this demo app.
            ResetPatientsTable();

            // Add sample data to the Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data to the database...");

            InsertPatient(new Patient() {
                SSN = "999-99-0001", FirstName = "Orlando", LastName = "Gee", BirthDate = DateTime.Parse("01/04/1964") });
            InsertPatient(new Patient() {
                SSN = "999-99-0002", FirstName = "Keith", LastName = "Harris", BirthDate = DateTime.Parse("06/20/1977") });
            InsertPatient(new Patient() {
                SSN = "999-99-0003", FirstName = "Donna", LastName = "Carreras", BirthDate = DateTime.Parse("02/09/1973") });
            InsertPatient(new Patient() {
                SSN = "999-99-0004", FirstName = "Janet", LastName = "Gates", BirthDate = DateTime.Parse("08/31/1985") });
            InsertPatient(new Patient() {
                SSN = "999-99-0005", FirstName = "Lucy", LastName = "Harrington", BirthDate = DateTime.Parse("05/06/1993") });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All the records currently in the Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching the encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that the user entered 11 characters.
            // In production be sure to check all user input and use the best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // The example allows duplicate SSN entries so we will return all records
            // that match the provided value and store the results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter to exit...");
            Console.ReadLine();
        }


        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
         VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("The following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key to exit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in the Patients table to reset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }


## <a name="verify-that-the-data-is-encrypted"></a><span data-ttu-id="49af7-220">Verificare che i dati siano crittografati</span><span class="sxs-lookup"><span data-stu-id="49af7-220">Verify that the data is encrypted</span></span>
<span data-ttu-id="49af7-221">È possibile verificare rapidamente che i dati effettivi nel server siano crittografati eseguendo una query dei dati della tabella **Patients** con SSMS.</span><span class="sxs-lookup"><span data-stu-id="49af7-221">You can quickly check that the actual data on the server is encrypted by querying the **Patients** data with SSMS.</span></span> <span data-ttu-id="49af7-222">Usare la connessione corrente in cui l'impostazione di crittografia della colonna non è ancora abilitata.</span><span class="sxs-lookup"><span data-stu-id="49af7-222">(Use your current connection where the column encryption setting is not yet enabled.)</span></span>

<span data-ttu-id="49af7-223">Eseguire la query seguente nel database Clinic.</span><span class="sxs-lookup"><span data-stu-id="49af7-223">Run the following query on the Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="49af7-224">È possibile osservare che le colonne crittografate non contengono dati di testo non crittografato.</span><span class="sxs-lookup"><span data-stu-id="49af7-224">You can see that the encrypted columns do not contain any plaintext data.</span></span>

   ![Nuova applicazione console](./media/sql-database-always-encrypted/ssms-encrypted.png)

<span data-ttu-id="49af7-226">Per usare SSMS per accedere ai dati di testo non crittografato, aggiungere il parametro **Column Encryption Setting=Enabled** alla connessione.</span><span class="sxs-lookup"><span data-stu-id="49af7-226">To use SSMS to access the plaintext data, you can add the **Column Encryption Setting=enabled** parameter to the connection.</span></span>

1. <span data-ttu-id="49af7-227">In SSMS fare clic con il pulsante destro del mouse sul server in **Esplora oggetti** e quindi fare clic su **Disconnetti**.</span><span class="sxs-lookup"><span data-stu-id="49af7-227">In SSMS, right-click your server in **Object Explorer**, and then click **Disconnect**.</span></span>
2. <span data-ttu-id="49af7-228">Fare clic su **Connetti** > **Motore di database** per aprire la finestra **Connetti al server** e quindi fare clic su **Opzioni**.</span><span class="sxs-lookup"><span data-stu-id="49af7-228">Click **Connect** > **Database Engine** to open the **Connect to Server** window, and then click **Options**.</span></span>
3. <span data-ttu-id="49af7-229">Fare clic su **Parametri aggiuntivi per la connessione** e digitare **Column Encryption Setting=Enabled**.</span><span class="sxs-lookup"><span data-stu-id="49af7-229">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Nuova applicazione console](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. <span data-ttu-id="49af7-231">Eseguire la query seguente nel database **Clinic** .</span><span class="sxs-lookup"><span data-stu-id="49af7-231">Run the following query on the **Clinic** database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="49af7-232">È ora possibile visualizzare i dati non crittografati nelle colonne crittografate.</span><span class="sxs-lookup"><span data-stu-id="49af7-232">You can now see the plaintext data in the encrypted columns.</span></span>

    ![Nuova applicazione console](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> <span data-ttu-id="49af7-234">Se ci si connette a SSMS (o a un client qualsiasi) da un altro computer, il computer non avrà accesso alle chiavi di crittografia e quindi non sarà in grado di decrittografare i dati.</span><span class="sxs-lookup"><span data-stu-id="49af7-234">If you connect with SSMS (or any client) from a different computer, it will not have access to the encryption keys and will not be able to decrypt the data.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="49af7-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="49af7-235">Next steps</span></span>
<span data-ttu-id="49af7-236">Dopo avere creato un database che usa la crittografia sempre attiva, è possibile eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="49af7-236">After you create a database that uses Always Encrypted, you may want to do the following:</span></span>

* <span data-ttu-id="49af7-237">Eseguire questo esempio da un altro computer.</span><span class="sxs-lookup"><span data-stu-id="49af7-237">Run this sample from a different computer.</span></span> <span data-ttu-id="49af7-238">Non avrà accesso alle chiavi di crittografia e quindi non avrà accesso ai dati non crittografati e non verrà eseguito correttamente.</span><span class="sxs-lookup"><span data-stu-id="49af7-238">It won't have access to the encryption keys, so it will not have access to the plaintext data and will not run successfully.</span></span>
* <span data-ttu-id="49af7-239">[Ruotare e pulire le chiavi](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="49af7-239">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="49af7-240">[Eseguire la migrazione dei dati già crittografati con la crittografia sempre attiva](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="49af7-240">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>
* <span data-ttu-id="49af7-241">[Distribuire certificati con crittografia Always Encrypted in altri computer client](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1). Vedere la sezione Rendere disponibili i certificati a utenti e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="49af7-241">[Deploy Always Encrypted certificates to other client machines](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (see the "Making Certificates Available to Applications and Users" section).</span></span>

## <a name="related-information"></a><span data-ttu-id="49af7-242">Informazioni correlate</span><span class="sxs-lookup"><span data-stu-id="49af7-242">Related information</span></span>
* [<span data-ttu-id="49af7-243">Crittografia sempre attiva (sviluppo di client)</span><span class="sxs-lookup"><span data-stu-id="49af7-243">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="49af7-244">Transparent Data Encryption</span><span class="sxs-lookup"><span data-stu-id="49af7-244">Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="49af7-245">Crittografia di SQL Server</span><span class="sxs-lookup"><span data-stu-id="49af7-245">SQL Server Encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="49af7-246">Procedura guidata della crittografia sempre attiva</span><span class="sxs-lookup"><span data-stu-id="49af7-246">Always Encrypted Wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="49af7-247">Blog della crittografia sempre attiva</span><span class="sxs-lookup"><span data-stu-id="49af7-247">Always Encrypted Blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

