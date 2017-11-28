---
title: 'Always Encrypted: database SQL di Azure - Archivio certificati di Windows | Documentazione Microsoft'
description: Questo articolo illustra come i dati sensibili in un database SQL con la crittografia del database tramite toosecure hello guidata su Always Encrypted in SQL Server Management Studio (SSMS). Viene inoltre visualizzato come toostore le chiavi di crittografia nel certificato di Windows hello archiviano.
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
ms.openlocfilehash: 483f9a2120cc42b732142fc07807d3d8830a0c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-hello-windows-certificate-store"></a><span data-ttu-id="b57c7-105">Always Encrypted: Proteggere i dati sensibili nel Database SQL e archiviare le chiavi di crittografia nell'archivio certificati di Windows hello</span><span class="sxs-lookup"><span data-stu-id="b57c7-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in hello Windows certificate store</span></span>

<span data-ttu-id="b57c7-106">Questo articolo illustra come toosecure dati sensibili in un database SQL del database con la crittografia del database tramite hello [procedura guidata Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="b57c7-106">This article shows you how toosecure sensitive data in a SQL database with database encryption by using hello [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="b57c7-107">Viene inoltre visualizzato come toostore le chiavi di crittografia nel certificato di Windows hello archiviano.</span><span class="sxs-lookup"><span data-stu-id="b57c7-107">It also shows you how toostore your encryption keys in hello Windows certificate store.</span></span>

<span data-ttu-id="b57c7-108">Always Encrypted è una nuova tecnologia di crittografia di dati in Database SQL di Azure e SQL Server che consente di proteggere i dati sensibili archiviati nel server di hello, durante lo spostamento tra il client e server, mentre i dati di hello sono in uso, garanzia che i dati sensibili non viene visualizzato come testo non crittografato hello sistema di database</span><span class="sxs-lookup"><span data-stu-id="b57c7-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on hello server, during movement between client and server, and while hello data is in use, ensuring that sensitive data never appears as plaintext inside hello database system.</span></span> <span data-ttu-id="b57c7-109">Dopo che i dati crittografati, solo le applicazioni client o server applicazioni che dispongono di chiavi di accesso toohello possibile accedere a dati in testo normale.</span><span class="sxs-lookup"><span data-stu-id="b57c7-109">After you encrypt data, only client applications or app servers that have access toohello keys can access plaintext data.</span></span> <span data-ttu-id="b57c7-110">Per informazioni dettagliate, vedere l'articolo relativo alla [crittografia sempre attiva (motore di database)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="b57c7-110">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="b57c7-111">Dopo aver configurato hello database toouse Always Encrypted, si creerà un'applicazione client in c# con Visual Studio toowork con dati crittografato hello.</span><span class="sxs-lookup"><span data-stu-id="b57c7-111">After configuring hello database toouse Always Encrypted, you will create a client application in C# with Visual Studio toowork with hello encrypted data.</span></span>

<span data-ttu-id="b57c7-112">Seguire i passaggi hello toolearn questo articolo come tooset di crittografia sempre attiva per un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="b57c7-112">Follow hello steps in this article toolearn how tooset up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="b57c7-113">In questo articolo si apprenderà come hello tooperform seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="b57c7-113">In this article, you will learn how tooperform hello following tasks:</span></span>

* <span data-ttu-id="b57c7-114">Utilizzare guidata sempre crittografato hello in SSMS toocreate [le chiavi Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="b57c7-114">Use hello Always Encrypted wizard in SSMS toocreate [Always Encrypted Keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="b57c7-115">Creare una [chiave master di colonna (CMK, Column Master Key)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="b57c7-115">Create a [Column Master Key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="b57c7-116">Creare una [chiave di crittografia di colonna (CEK, Column Encryption Key)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="b57c7-116">Create a [Column Encryption Key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="b57c7-117">Creare una tabella di database e crittografare le colonne.</span><span class="sxs-lookup"><span data-stu-id="b57c7-117">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="b57c7-118">Creare un'applicazione che inserisce, seleziona e visualizza i dati dalle colonne crittografato hello.</span><span class="sxs-lookup"><span data-stu-id="b57c7-118">Create an application that inserts, selects, and displays data from hello encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b57c7-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b57c7-119">Prerequisites</span></span>
<span data-ttu-id="b57c7-120">Per questa esercitazione occorrono:</span><span class="sxs-lookup"><span data-stu-id="b57c7-120">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="b57c7-121">Un account e una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b57c7-121">An Azure account and subscription.</span></span> <span data-ttu-id="b57c7-122">Nel caso in cui non siano disponibili, è possibile usare una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b57c7-122">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b57c7-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versione 13.0.700.242 o successive.</span><span class="sxs-lookup"><span data-stu-id="b57c7-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="b57c7-124">[.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) o versione successiva (computer hello client).</span><span class="sxs-lookup"><span data-stu-id="b57c7-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on hello client computer).</span></span>
* <span data-ttu-id="b57c7-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="b57c7-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="b57c7-126">Creare un database SQL vuoto</span><span class="sxs-lookup"><span data-stu-id="b57c7-126">Create a blank SQL database</span></span>
1. <span data-ttu-id="b57c7-127">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b57c7-127">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b57c7-128">Fare clic su **Nuovo** > **Dati e archiviazione** > **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="b57c7-128">Click **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="b57c7-129">Creare un database **vuoto** denominato **Clinic** in un server nuovo o esistente.</span><span class="sxs-lookup"><span data-stu-id="b57c7-129">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="b57c7-130">Per istruzioni dettagliate sulla creazione di un database in hello portale di Azure, vedere [di un database SQL di Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b57c7-130">For detailed instructions about creating a database in hello Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Creazione di un database vuoto](./media/sql-database-always-encrypted/create-database.png)

<span data-ttu-id="b57c7-132">Stringa di connessione hello sarà necessario più avanti nell'esercitazione di hello.</span><span class="sxs-lookup"><span data-stu-id="b57c7-132">You will need hello connection string later in hello tutorial.</span></span> <span data-ttu-id="b57c7-133">Dopo aver creato il database di hello, andare toohello nuova Clinic database e la copia hello stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="b57c7-133">After hello database is created, go toohello new Clinic database and copy hello connection string.</span></span> <span data-ttu-id="b57c7-134">È possibile ottenere la stringa di connessione hello in qualsiasi momento, ma è facile toocopy quando si utilizza hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b57c7-134">You can get hello connection string at any time, but it's easy toocopy it when you're in hello Azure portal.</span></span>

1. <span data-ttu-id="b57c7-135">Fare clic su **Database SQL** > **Clinic** > **Mostra stringhe di connessione del database**.</span><span class="sxs-lookup"><span data-stu-id="b57c7-135">Click **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="b57c7-136">Copiare la stringa di connessione hello per **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="b57c7-136">Copy hello connection string for **ADO.NET**.</span></span>
   
    ![Copiare la stringa di connessione hello](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="b57c7-138">La connessione a database toohello con SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="b57c7-138">Connect toohello database with SSMS</span></span>
<span data-ttu-id="b57c7-139">Aprire SQL Server Management Studio e connettersi toohello server con database Clinic hello.</span><span class="sxs-lookup"><span data-stu-id="b57c7-139">Open SSMS and connect toohello server with hello Clinic database.</span></span>

1. <span data-ttu-id="b57c7-140">Aprire SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="b57c7-140">Open SSMS.</span></span> <span data-ttu-id="b57c7-141">(Fare clic su **Connetti** > **motore di Database** tooopen hello **connettersi tooServer** finestra se non è aperto).</span><span class="sxs-lookup"><span data-stu-id="b57c7-141">(Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window if it is not open).</span></span>
2. <span data-ttu-id="b57c7-142">Immettere il nome e le credenziali del server.</span><span class="sxs-lookup"><span data-stu-id="b57c7-142">Enter your server name and credentials.</span></span> <span data-ttu-id="b57c7-143">nome del server Hello sono disponibili nel Pannello di database SQL di hello e nella stringa di connessione hello copiato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b57c7-143">hello server name can be found on hello SQL database blade and in hello connection string you copied earlier.</span></span> <span data-ttu-id="b57c7-144">Tra cui nome completo del server di tipo hello *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="b57c7-144">Type hello complete server name including *database.windows.net*.</span></span>
   
    ![Copiare la stringa di connessione hello](./media/sql-database-always-encrypted/ssms-connect.png)

<span data-ttu-id="b57c7-146">Se hello **nuova regola Firewall** viene visualizzata la finestra Accedi tooAzure e consentono di SQL Server Management Studio creare una nuova regola firewall per l'utente.</span><span class="sxs-lookup"><span data-stu-id="b57c7-146">If hello **New Firewall Rule** window opens, sign in tooAzure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="b57c7-147">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="b57c7-147">Create a table</span></span>
<span data-ttu-id="b57c7-148">In questa sezione si creerà un pazienti toohold di tabella.</span><span class="sxs-lookup"><span data-stu-id="b57c7-148">In this section, you will create a table toohold patient data.</span></span> <span data-ttu-id="b57c7-149">Questo sarà una normale tabella, inizialmente si configurerà la crittografia nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="b57c7-149">This will be a normal table initially--you will configure encryption in hello next section.</span></span>

1. <span data-ttu-id="b57c7-150">Espandere **Database**.</span><span class="sxs-lookup"><span data-stu-id="b57c7-150">Expand **Databases**.</span></span>
2. <span data-ttu-id="b57c7-151">Pulsante destro del mouse hello **Clinic** database e fare clic su **nuova Query**.</span><span class="sxs-lookup"><span data-stu-id="b57c7-151">Right-click hello **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="b57c7-152">Hello Incolla seguente Transact-SQL (T-SQL) in nuova finestra query di hello e **Execute** è.</span><span class="sxs-lookup"><span data-stu-id="b57c7-152">Paste hello following Transact-SQL (T-SQL) into hello new query window and **Execute** it.</span></span>

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


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="b57c7-153">Crittografare le colonne configurando la crittografia sempre attiva</span><span class="sxs-lookup"><span data-stu-id="b57c7-153">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="b57c7-154">SQL Server Management Studio include una procedura guidata tooeasily configurare Always Encrypted tramite la configurazione di hello CMK, CEK e le colonne crittografate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b57c7-154">SSMS provides a wizard tooeasily configure Always Encrypted by setting up hello CMK, CEK, and encrypted columns for you.</span></span>

1. <span data-ttu-id="b57c7-155">Espandere **Database** > **Clinic** > **Tabelle**.</span><span class="sxs-lookup"><span data-stu-id="b57c7-155">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="b57c7-156">Pulsante destro del mouse hello **pazienti** tabella e selezionare **crittografa colonne** guidata sempre crittografato hello di tooopen:</span><span class="sxs-lookup"><span data-stu-id="b57c7-156">Right-click hello **Patients** table and select **Encrypt Columns** tooopen hello Always Encrypted wizard:</span></span>
   
    ![Crittografa colonne](./media/sql-database-always-encrypted/encrypt-columns.png)

<span data-ttu-id="b57c7-158">Creazione guidata sempre crittografato Hello include hello le sezioni seguenti: **selezione colonna**, **configurazione chiave Master** (CMK), **convalida**, e ** Riepilogo**.</span><span class="sxs-lookup"><span data-stu-id="b57c7-158">hello Always Encrypted wizard includes hello following sections: **Column Selection**, **Master Key Configuration** (CMK), **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="b57c7-159">Selezione colonne</span><span class="sxs-lookup"><span data-stu-id="b57c7-159">Column Selection</span></span>
<span data-ttu-id="b57c7-160">Fare clic su **Avanti** su hello **Introduzione** hello tooopen pagina **selezione colonna** pagina.</span><span class="sxs-lookup"><span data-stu-id="b57c7-160">Click **Next** on hello **Introduction** page tooopen hello **Column Selection** page.</span></span> <span data-ttu-id="b57c7-161">In questa pagina, verranno selezionate le colonne desiderate tooencrypt, [hello tipo di crittografia e specificare la chiave di crittografia di colonna (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span><span class="sxs-lookup"><span data-stu-id="b57c7-161">On this page, you will select which columns you want tooencrypt, [hello type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span></span>

<span data-ttu-id="b57c7-162">Crittografare il **CF** e la **data di nascita** per ogni paziente.</span><span class="sxs-lookup"><span data-stu-id="b57c7-162">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="b57c7-163">Hello **SSN** colonna verrà usata la crittografia deterministica, che supporta le ricerche di uguaglianza, join e group by.</span><span class="sxs-lookup"><span data-stu-id="b57c7-163">hello **SSN** column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="b57c7-164">Hello **data di nascita** colonna utilizzerà la crittografia casuale, che non supporta le operazioni.</span><span class="sxs-lookup"><span data-stu-id="b57c7-164">hello **BirthDate** column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="b57c7-165">Set hello **tipo di crittografia** per hello **SSN** colonna troppo**deterministica** hello e **data di nascita** colonna troppo** Casuale**.</span><span class="sxs-lookup"><span data-stu-id="b57c7-165">Set hello **Encryption Type** for hello **SSN** column too**Deterministic** and hello **BirthDate** column too**Randomized**.</span></span> <span data-ttu-id="b57c7-166">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b57c7-166">Click **Next**.</span></span>

![Crittografa colonne](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="b57c7-168">Configurazione della chiave master</span><span class="sxs-lookup"><span data-stu-id="b57c7-168">Master Key Configuration</span></span>
<span data-ttu-id="b57c7-169">Hello **configurazione chiave Master** pagina è in cui impostare la CMK e provider dell'archivio chiavi hello selezionare dove hello CMK verranno archiviati.</span><span class="sxs-lookup"><span data-stu-id="b57c7-169">hello **Master Key Configuration** page is where you set up your CMK and select hello key store provider where hello CMK will be stored.</span></span> <span data-ttu-id="b57c7-170">Attualmente, è possibile archiviare una chiave CMK nell'archivio certificati di Windows hello, insieme di credenziali chiave di Azure o un modulo di protezione hardware (HSM).</span><span class="sxs-lookup"><span data-stu-id="b57c7-170">Currently, you can store a CMK in hello Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span> <span data-ttu-id="b57c7-171">Questa esercitazione illustra in che modo toostore le chiavi nel certificato di Windows hello archiviano.</span><span class="sxs-lookup"><span data-stu-id="b57c7-171">This tutorial shows how toostore your keys in hello Windows certificate store.</span></span>

<span data-ttu-id="b57c7-172">Verificare che l'**archivio certificati di Windows** sia selezionato e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b57c7-172">Verify that **Windows certificate store** is selected and click **Next**.</span></span>

![Configurazione della chiave master](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="b57c7-174">Convalida</span><span class="sxs-lookup"><span data-stu-id="b57c7-174">Validation</span></span>
<span data-ttu-id="b57c7-175">È possibile crittografare colonne hello ora o salvare un toorun di script di PowerShell in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="b57c7-175">You can encrypt hello columns now or save a PowerShell script toorun later.</span></span> <span data-ttu-id="b57c7-176">Per questa esercitazione, selezionare **procedere ora toofinish** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b57c7-176">For this tutorial, select **Proceed toofinish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="b57c7-177">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="b57c7-177">Summary</span></span>
<span data-ttu-id="b57c7-178">Verificare che le impostazioni di hello siano tutti corrette e fare clic su **fine** installazione hello toocomplete per Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="b57c7-178">Verify that hello settings are all correct and click **Finish** toocomplete hello setup for Always Encrypted.</span></span>

![Riepilogo](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-hello-wizards-actions"></a><span data-ttu-id="b57c7-180">Verificare le azioni della procedura guidata di hello</span><span class="sxs-lookup"><span data-stu-id="b57c7-180">Verify hello wizard's actions</span></span>
<span data-ttu-id="b57c7-181">Al termine procedura hello, il database è configurato per Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="b57c7-181">After hello wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="b57c7-182">Hello hello di guidata eseguito le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b57c7-182">hello wizard performed hello following actions:</span></span>

* <span data-ttu-id="b57c7-183">Creare una chiave CMK.</span><span class="sxs-lookup"><span data-stu-id="b57c7-183">Created a CMK.</span></span>
* <span data-ttu-id="b57c7-184">Creare una chiave di crittografia di colonna (CEK).</span><span class="sxs-lookup"><span data-stu-id="b57c7-184">Created a CEK.</span></span>
* <span data-ttu-id="b57c7-185">Hello configurato selezionate colonne per la crittografia.</span><span class="sxs-lookup"><span data-stu-id="b57c7-185">Configured hello selected columns for encryption.</span></span> <span data-ttu-id="b57c7-186">Il **pazienti** tabella non è attualmente disponibili dati, ma i dati esistenti nelle colonne selezionata hello ora sono crittografati.</span><span class="sxs-lookup"><span data-stu-id="b57c7-186">Your **Patients** table currently has no data, but any existing data in hello selected columns is now encrypted.</span></span>

<span data-ttu-id="b57c7-187">È possibile verificare la creazione di hello delle chiavi di hello in SSMS passando troppo**Clinic** > **sicurezza** > **le chiavi Always Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="b57c7-187">You can verify hello creation of hello keys in SSMS by going too**Clinic** > **Security** > **Always Encrypted Keys**.</span></span> <span data-ttu-id="b57c7-188">È ora possibile visualizzare hello le nuove chiavi hello generato automaticamente dalla procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="b57c7-188">You can now see hello new keys that hello wizard generated for you.</span></span>

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a><span data-ttu-id="b57c7-189">Creare un'applicazione client che interagisce con i dati crittografato hello</span><span class="sxs-lookup"><span data-stu-id="b57c7-189">Create a client application that works with hello encrypted data</span></span>
<span data-ttu-id="b57c7-190">Ora che Always Encrypted è configurato, è possibile compilare un'applicazione che esegue *inserisce* e *seleziona* su hello colonne crittografate.</span><span class="sxs-lookup"><span data-stu-id="b57c7-190">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on hello encrypted columns.</span></span> <span data-ttu-id="b57c7-191">toosuccessfully eseguire hello applicazione di esempio, è necessario eseguirlo su hello stesso computer in cui è stato eseguito guidata sempre crittografato hello.</span><span class="sxs-lookup"><span data-stu-id="b57c7-191">toosuccessfully run hello sample application, you must run it on hello same computer where you ran hello Always Encrypted wizard.</span></span> <span data-ttu-id="b57c7-192">un'applicazione hello toorun in un altro computer, è necessario distribuire Always Encrypted certificati toohello computer che esegue hello client app.</span><span class="sxs-lookup"><span data-stu-id="b57c7-192">toorun hello application on another computer, you must deploy your Always Encrypted certificates toohello computer running hello client app.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="b57c7-193">L'applicazione deve usare [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) oggetti quando si passa server toohello dati di testo normale con colonne con crittografia sempre attiva.</span><span class="sxs-lookup"><span data-stu-id="b57c7-193">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data toohello server with Always Encrypted columns.</span></span> <span data-ttu-id="b57c7-194">Il trasferimento di valori letterali senza usare oggetti SqlParameter genererà un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="b57c7-194">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="b57c7-195">Aprire Visual Studio e creare un'applicazione console C#.</span><span class="sxs-lookup"><span data-stu-id="b57c7-195">Open Visual Studio and create a new C# console application.</span></span> <span data-ttu-id="b57c7-196">Verificare che il progetto è stato impostato troppo**.NET Framework 4.6** o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="b57c7-196">Make sure your project is set too**.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="b57c7-197">Progetto hello nome **AlwaysEncryptedConsoleApp** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b57c7-197">Name hello project **AlwaysEncryptedConsoleApp** and click **OK**.</span></span>

![Nuova applicazione console](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-tooenable-always-encrypted"></a><span data-ttu-id="b57c7-199">Modificare il tooenable di stringa di connessione Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="b57c7-199">Modify your connection string tooenable Always Encrypted</span></span>
<span data-ttu-id="b57c7-200">Questa sezione viene illustrato come tooenable sempre crittografato nella stringa di connessione di database.</span><span class="sxs-lookup"><span data-stu-id="b57c7-200">This section explains how tooenable Always Encrypted in your database connection string.</span></span> <span data-ttu-id="b57c7-201">Si modificherà l'applicazione console hello che appena creata nella sezione successiva di hello, "Always Encrypted applicazione console di esempio".</span><span class="sxs-lookup"><span data-stu-id="b57c7-201">You will modify hello console app you just created in hello next section, "Always Encrypted sample console application."</span></span>

<span data-ttu-id="b57c7-202">tooenable Always Encrypted, è necessario hello tooadd **Column Encryption Setting** connessione tooyour parola chiave di stringa e impostarlo troppo**abilitato**.</span><span class="sxs-lookup"><span data-stu-id="b57c7-202">tooenable Always Encrypted, you need tooadd hello **Column Encryption Setting** keyword tooyour connection string and set it too**Enabled**.</span></span>

<span data-ttu-id="b57c7-203">È possibile impostare questo valore direttamente nella stringa di connessione hello oppure è possibile impostarlo utilizzando un [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="b57c7-203">You can set this directly in hello connection string, or you can set it by using a [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="b57c7-204">applicazione di esempio Hello hello sezione successiva viene illustrato come toouse **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="b57c7-204">hello sample application in hello next section shows how toouse **SqlConnectionStringBuilder**.</span></span>

> [!NOTE]
> <span data-ttu-id="b57c7-205">Questo è unica modifica hello necessaria in un client applicazione specifico tooAlways crittografato.</span><span class="sxs-lookup"><span data-stu-id="b57c7-205">This is hello only change required in a client application specific tooAlways Encrypted.</span></span> <span data-ttu-id="b57c7-206">Se si dispone di un'applicazione esistente che archivia la stringa di connessione esternamente (ovvero, in un file di configurazione), potrebbe essere in grado di tooenable Always Encrypted senza modificare il codice.</span><span class="sxs-lookup"><span data-stu-id="b57c7-206">If you have an existing application that stores its connection string externally (that is, in a config file), you might be able tooenable Always Encrypted without changing any code.</span></span>
> 
> 

### <a name="enable-always-encrypted-in-hello-connection-string"></a><span data-ttu-id="b57c7-207">Abilita sempre crittografato nella stringa di connessione hello</span><span class="sxs-lookup"><span data-stu-id="b57c7-207">Enable Always Encrypted in hello connection string</span></span>
<span data-ttu-id="b57c7-208">Aggiungere hello seguente stringa di connessione tooyour (parola chiave):</span><span class="sxs-lookup"><span data-stu-id="b57c7-208">Add hello following keyword tooyour connection string:</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a><span data-ttu-id="b57c7-209">Abilitare la crittografia sempre attiva con SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="b57c7-209">Enable Always Encrypted with a SqlConnectionStringBuilder</span></span>
<span data-ttu-id="b57c7-210">Hello codice seguente viene illustrato come impostando tooenable sempre crittografato hello [Columnencryptionsetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) troppo[abilitato](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="b57c7-210">hello following code shows how tooenable Always Encrypted by setting hello [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) too[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="b57c7-211">Applicazione console di esempio della crittografia sempre attiva</span><span class="sxs-lookup"><span data-stu-id="b57c7-211">Always Encrypted sample console application</span></span>
<span data-ttu-id="b57c7-212">Questo esempio dimostra come:</span><span class="sxs-lookup"><span data-stu-id="b57c7-212">This sample demonstrates how to:</span></span>

* <span data-ttu-id="b57c7-213">Modificare il tooenable di stringa di connessione Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="b57c7-213">Modify your connection string tooenable Always Encrypted.</span></span>
* <span data-ttu-id="b57c7-214">Inserire i dati in colonne crittografato hello.</span><span class="sxs-lookup"><span data-stu-id="b57c7-214">Insert data into hello encrypted columns.</span></span>
* <span data-ttu-id="b57c7-215">Selezionare un record filtrando in base a un valore specifico in una colonna crittografata.</span><span class="sxs-lookup"><span data-stu-id="b57c7-215">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="b57c7-216">Sostituire il contenuto di hello di **Program.cs** con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="b57c7-216">Replace hello contents of **Program.cs** with hello following code.</span></span> <span data-ttu-id="b57c7-217">Sostituire la stringa di connessione hello per la variabile globale connectionString hello nella riga hello direttamente sopra hello metodo Main con la stringa di connessione valida da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b57c7-217">Replace hello connection string for hello global connectionString variable in hello line directly above hello Main method with your valid connection string from hello Azure portal.</span></span> <span data-ttu-id="b57c7-218">Si tratta di modifica di hello solo se è necessario codice toothis toomake.</span><span class="sxs-lookup"><span data-stu-id="b57c7-218">This is hello only change you need toomake toothis code.</span></span>

<span data-ttu-id="b57c7-219">Eseguire hello app toosee Always Encrypted in azione.</span><span class="sxs-lookup"><span data-stu-id="b57c7-219">Run hello app toosee Always Encrypted in action.</span></span>

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
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

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
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
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

            Console.WriteLine("Press Enter tooexit...");
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
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
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


        // This method simply deletes all records in hello Patients table tooreset our demo.
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


## <a name="verify-that-hello-data-is-encrypted"></a><span data-ttu-id="b57c7-220">Verificare che siano crittografati dati hello</span><span class="sxs-lookup"><span data-stu-id="b57c7-220">Verify that hello data is encrypted</span></span>
<span data-ttu-id="b57c7-221">È possibile controllare rapidamente che i dati effettivi di hello nel server di hello sono crittografati eseguendo una query hello **pazienti** dati con SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="b57c7-221">You can quickly check that hello actual data on hello server is encrypted by querying hello **Patients** data with SSMS.</span></span> <span data-ttu-id="b57c7-222">(Utilizzare la connessione corrente in cui impostazione di crittografia di colonna hello non è ancora abilitato).</span><span class="sxs-lookup"><span data-stu-id="b57c7-222">(Use your current connection where hello column encryption setting is not yet enabled.)</span></span>

<span data-ttu-id="b57c7-223">Eseguire hello seguente query sul database Clinic hello.</span><span class="sxs-lookup"><span data-stu-id="b57c7-223">Run hello following query on hello Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="b57c7-224">È possibile vedere che le colonne crittografato hello non contengano i dati di testo normale.</span><span class="sxs-lookup"><span data-stu-id="b57c7-224">You can see that hello encrypted columns do not contain any plaintext data.</span></span>

   ![Nuova applicazione console](./media/sql-database-always-encrypted/ssms-encrypted.png)

<span data-ttu-id="b57c7-226">toouse SSMS tooaccess hello dati in testo normale, è possibile aggiungere hello **Column Encryption Setting = abilitata** connessione toohello di parametro.</span><span class="sxs-lookup"><span data-stu-id="b57c7-226">toouse SSMS tooaccess hello plaintext data, you can add hello **Column Encryption Setting=enabled** parameter toohello connection.</span></span>

1. <span data-ttu-id="b57c7-227">In SSMS fare clic con il pulsante destro del mouse sul server in **Esplora oggetti** e quindi fare clic su **Disconnetti**.</span><span class="sxs-lookup"><span data-stu-id="b57c7-227">In SSMS, right-click your server in **Object Explorer**, and then click **Disconnect**.</span></span>
2. <span data-ttu-id="b57c7-228">Fare clic su **Connetti** > **motore di Database** tooopen hello **connettersi tooServer** finestra e quindi fare clic su **opzioni**.</span><span class="sxs-lookup"><span data-stu-id="b57c7-228">Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window, and then click **Options**.</span></span>
3. <span data-ttu-id="b57c7-229">Fare clic su **Parametri aggiuntivi per la connessione** e digitare **Column Encryption Setting=Enabled**.</span><span class="sxs-lookup"><span data-stu-id="b57c7-229">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Nuova applicazione console](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. <span data-ttu-id="b57c7-231">Esecuzione hello query su hello riportata di seguito **Clinic** database.</span><span class="sxs-lookup"><span data-stu-id="b57c7-231">Run hello following query on hello **Clinic** database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="b57c7-232">È ora possibile visualizzare dati in formato testo hello nelle colonne crittografato hello.</span><span class="sxs-lookup"><span data-stu-id="b57c7-232">You can now see hello plaintext data in hello encrypted columns.</span></span>

    ![Nuova applicazione console](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> <span data-ttu-id="b57c7-234">Se ci si connette a SQL Server Management Studio (o qualsiasi client) da un computer diverso, non avrà accesso toohello chiavi di crittografia e non sarà in grado di toodecrypt dati di hello.</span><span class="sxs-lookup"><span data-stu-id="b57c7-234">If you connect with SSMS (or any client) from a different computer, it will not have access toohello encryption keys and will not be able toodecrypt hello data.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b57c7-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b57c7-235">Next steps</span></span>
<span data-ttu-id="b57c7-236">Dopo aver creato un database che Usa crittografia sempre attiva, è necessario seguente hello toodo:</span><span class="sxs-lookup"><span data-stu-id="b57c7-236">After you create a database that uses Always Encrypted, you may want toodo hello following:</span></span>

* <span data-ttu-id="b57c7-237">Eseguire questo esempio da un altro computer.</span><span class="sxs-lookup"><span data-stu-id="b57c7-237">Run this sample from a different computer.</span></span> <span data-ttu-id="b57c7-238">Non sarà possibile chiavi di crittografia toohello di accesso, in modo che non avrà accesso ai dati di testo normale toohello e non funzionerà correttamente.</span><span class="sxs-lookup"><span data-stu-id="b57c7-238">It won't have access toohello encryption keys, so it will not have access toohello plaintext data and will not run successfully.</span></span>
* <span data-ttu-id="b57c7-239">[Ruotare e pulire le chiavi](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="b57c7-239">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="b57c7-240">[Eseguire la migrazione dei dati già crittografati con la crittografia sempre attiva](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="b57c7-240">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>
* <span data-ttu-id="b57c7-241">[Distribuire macchine di Always Encrypted certificati tooother client](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (vedere la sezione "Rendendo tooApplications disponibili i certificati e gli utenti" hello).</span><span class="sxs-lookup"><span data-stu-id="b57c7-241">[Deploy Always Encrypted certificates tooother client machines](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (see hello "Making Certificates Available tooApplications and Users" section).</span></span>

## <a name="related-information"></a><span data-ttu-id="b57c7-242">Informazioni correlate</span><span class="sxs-lookup"><span data-stu-id="b57c7-242">Related information</span></span>
* [<span data-ttu-id="b57c7-243">Crittografia sempre attiva (sviluppo di client)</span><span class="sxs-lookup"><span data-stu-id="b57c7-243">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="b57c7-244">Transparent Data Encryption</span><span class="sxs-lookup"><span data-stu-id="b57c7-244">Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="b57c7-245">Crittografia di SQL Server</span><span class="sxs-lookup"><span data-stu-id="b57c7-245">SQL Server Encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="b57c7-246">Procedura guidata della crittografia sempre attiva</span><span class="sxs-lookup"><span data-stu-id="b57c7-246">Always Encrypted Wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="b57c7-247">Blog della crittografia sempre attiva</span><span class="sxs-lookup"><span data-stu-id="b57c7-247">Always Encrypted Blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

