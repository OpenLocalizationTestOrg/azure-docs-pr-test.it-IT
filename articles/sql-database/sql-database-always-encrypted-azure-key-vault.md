---
title: 'Always Encrypted: database SQL - Azure Key Vault | Documentazione Microsoft'
description: Questo articolo illustra come proteggere i dati sensibili in un database SQL con la crittografia dei dati usando la procedura guidata Always Encrypted di SQL Server Management Studio. Include anche le istruzioni che illustrano come archiviare ogni chiave di crittografia nell'insieme di credenziali delle chiavi di Azure.
keywords: crittografia dei dati, chiave di crittografia, crittografia del cloud
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: 6ca16644-5969-497b-a413-d28c3b835c9b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: sstein
ms.openlocfilehash: 61bfd420425b4740f6d4ebc01a403a88ff351382
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a><span data-ttu-id="383cb-105">Crittografia sempre attiva: Proteggere i dati sensibili nel database SQL e archiviare le chiavi di crittografia nell'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="383cb-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in Azure Key Vault</span></span>

<span data-ttu-id="383cb-106">Questo articolo illustra come proteggere i dati sensibili in un database SQL con la crittografia dei dati tramite la [procedura guidata Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) di [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="383cb-106">This article shows you how to secure sensitive data in a SQL database with data encryption using the [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="383cb-107">Include anche le istruzioni che illustrano come archiviare ogni chiave di crittografia nell'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="383cb-107">It also includes instructions that will show you how to store each encryption key in Azure Key Vault.</span></span>

<span data-ttu-id="383cb-108">La crittografia sempre attiva è una nuova tecnologia di crittografia dei dati del database SQL di Azure e di SQL Server, che protegge i dati sensibili inattivi sul server durante lo spostamento tra client e server e durante l'uso.</span><span class="sxs-lookup"><span data-stu-id="383cb-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on the server, during movement between client and server, and while the data is in use.</span></span> <span data-ttu-id="383cb-109">La crittografia sempre attiva garantisce che i dati sensibili non vengano mai visualizzati come testo non crittografato all'interno del sistema di database.</span><span class="sxs-lookup"><span data-stu-id="383cb-109">Always Encrypted ensures that sensitive data never appears as plaintext inside the database system.</span></span> <span data-ttu-id="383cb-110">Dopo avere configurato la crittografia dei dati solo le applicazioni client o i server applicazioni, che hanno accesso alle chiavi, possono accedere ai dati di testo non crittografato.</span><span class="sxs-lookup"><span data-stu-id="383cb-110">After you configure data encryption, only client applications or app servers that have access to the keys can access plaintext data.</span></span> <span data-ttu-id="383cb-111">Per informazioni dettagliate, vedere l'articolo relativo alla [crittografia sempre attiva (motore di database)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="383cb-111">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="383cb-112">Dopo avere configurato il database per usare la crittografia sempre attiva, viene creata un'applicazione client in C# con Visual Studio per lavorare con i dati crittografati.</span><span class="sxs-lookup"><span data-stu-id="383cb-112">After you configure the database to use Always Encrypted, you will create a client application in C# with Visual Studio to work with the encrypted data.</span></span>

<span data-ttu-id="383cb-113">Seguire i passaggi in questo articolo per imparare come configurare la crittografia sempre attiva per un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="383cb-113">Follow the steps in this article and learn how to set up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="383cb-114">Questo articolo spiega come eseguire le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="383cb-114">In this article you will learn how to perform the following tasks:</span></span>

* <span data-ttu-id="383cb-115">Usare la procedura guidata per la crittografia sempre attiva in SSMS per creare [chiavi con crittografia sempre attiva](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="383cb-115">Use the Always Encrypted wizard in SSMS to create [Always Encrypted keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="383cb-116">Creare una [chiave master di colonna (CMK, Column Master Key)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="383cb-116">Create a [column master key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="383cb-117">Creare una [chiave di crittografia di colonna (CEK, Column Encryption Key)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="383cb-117">Create a [column encryption key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="383cb-118">Creare una tabella di database e crittografare le colonne.</span><span class="sxs-lookup"><span data-stu-id="383cb-118">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="383cb-119">Creare un'applicazione che inserisce, seleziona e visualizza i dati delle colonne crittografate.</span><span class="sxs-lookup"><span data-stu-id="383cb-119">Create an application that inserts, selects, and displays data from the encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="383cb-120">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="383cb-120">Prerequisites</span></span>
<span data-ttu-id="383cb-121">Per questa esercitazione occorrono:</span><span class="sxs-lookup"><span data-stu-id="383cb-121">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="383cb-122">Un account e una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="383cb-122">An Azure account and subscription.</span></span> <span data-ttu-id="383cb-123">Nel caso in cui non siano disponibili, è possibile usare una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="383cb-123">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="383cb-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versione 13.0.700.242 o successive.</span><span class="sxs-lookup"><span data-stu-id="383cb-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="383cb-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) o versioni successive (nel computer client).</span><span class="sxs-lookup"><span data-stu-id="383cb-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on the client computer).</span></span>
* <span data-ttu-id="383cb-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="383cb-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>
* <span data-ttu-id="383cb-127">[Azure PowerShell](/powershell/azure/overview) versione 1.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="383cb-127">[Azure PowerShell](/powershell/azure/overview), version  1.0 or later.</span></span> <span data-ttu-id="383cb-128">Digitare **(Get-Module azure -ListAvailable).Version** per verificare quale versione di PowerShell è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="383cb-128">Type **(Get-Module azure -ListAvailable).Version** to see what version of PowerShell you are running.</span></span>

## <a name="enable-your-client-application-to-access-the-sql-database-service"></a><span data-ttu-id="383cb-129">Abilitare l'applicazione client per accedere al servizio di database SQL</span><span class="sxs-lookup"><span data-stu-id="383cb-129">Enable your client application to access the SQL Database service</span></span>
<span data-ttu-id="383cb-130">È necessario abilitare l'applicazione client per accedere al servizio del database SQL tramite la configurazione dell'autenticazione richiesta e l'acquisizione di *ClientId* e *Secret*, necessari per autenticare l'applicazione nel codice seguente.</span><span class="sxs-lookup"><span data-stu-id="383cb-130">You must enable your client application to access the SQL Database service by setting up the required authentication and acquiring the *ClientId* and *Secret* that you will need to authenticate your application in the following code.</span></span>

1. <span data-ttu-id="383cb-131">Aprire il [portale di Azure classico](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="383cb-131">Open the [Azure classic portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="383cb-132">Selezionare **Active Directory** e fare clic sull'istanza di Active Directory che verrà usata dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="383cb-132">Select **Active Directory** and click the Active Directory instance that your application will use.</span></span>
3. <span data-ttu-id="383cb-133">Fare clic su **Applicazioni** e quindi su **AGGIUNGI**.</span><span class="sxs-lookup"><span data-stu-id="383cb-133">Click **Applications**, and then click **ADD**.</span></span>
4. <span data-ttu-id="383cb-134">Digitare un nome per l'applicazione, ad esempio *myClientApp*, selezionare **APPLICAZIONE WEB**e fare clic sulla freccia per continuare.</span><span class="sxs-lookup"><span data-stu-id="383cb-134">Type a name for your application (for example: *myClientApp*), select **WEB APPLICATION**, and click the arrow to continue.</span></span>
5. <span data-ttu-id="383cb-135">Per l'**URL DI ACCESSO** e l'**URI ID APP** digitare un URL valido (ad esempio, *http://myClientApp*) e continuare.</span><span class="sxs-lookup"><span data-stu-id="383cb-135">For the **SIGN-ON URL** and **APP ID URI** you can type a valid URL (for example, *http://myClientApp*) and continue.</span></span>
6. <span data-ttu-id="383cb-136">Fare clic su **CONFIGURA**.</span><span class="sxs-lookup"><span data-stu-id="383cb-136">Click **CONFIGURE**.</span></span>
7. <span data-ttu-id="383cb-137">Copiare l' **ID CLIENT**.</span><span class="sxs-lookup"><span data-stu-id="383cb-137">Copy your **CLIENT ID**.</span></span> <span data-ttu-id="383cb-138">Sarà necessario immettere questo valore nel codice in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="383cb-138">(You will need this value in your code later.)</span></span>
8. <span data-ttu-id="383cb-139">Nella sezione relativa alle **chiavi** selezionare **1 anno** dall'elenco a discesa **Seleziona durata**.</span><span class="sxs-lookup"><span data-stu-id="383cb-139">In the **keys** section, select **1 year** from the  **Select duration** drop-down list.</span></span> <span data-ttu-id="383cb-140">La chiave verrà copiata dopo il salvataggio nel passaggio 13.</span><span class="sxs-lookup"><span data-stu-id="383cb-140">(You will copy the key after you save in step 13.)</span></span>
9. <span data-ttu-id="383cb-141">Scorrere verso il basso e fare clic su **Aggiungi applicazione**.</span><span class="sxs-lookup"><span data-stu-id="383cb-141">Scroll down and click **Add application**.</span></span>
10. <span data-ttu-id="383cb-142">Lasciare **MOSTRA** impostato su **App Microsoft** e selezionare **API di gestione del servizio Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="383cb-142">Leave **SHOW** set to **Microsoft Apps** and select **Microsoft Azure Service Management API**.</span></span> <span data-ttu-id="383cb-143">Fare clic sul segno di spunta per continuare.</span><span class="sxs-lookup"><span data-stu-id="383cb-143">Click the checkmark to continue.</span></span>
11. <span data-ttu-id="383cb-144">Nell'elenco a discesa **Autorizzazioni delegate** selezionare **Access Azure Service Management...** (Gestione servizio di accesso Azure).</span><span class="sxs-lookup"><span data-stu-id="383cb-144">Select **Access Azure Service Management...** from the **Delegated Permissions** drop-down list.</span></span>
12. <span data-ttu-id="383cb-145">Fare clic su **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="383cb-145">Click **SAVE**.</span></span>
13. <span data-ttu-id="383cb-146">Al termine del salvataggio copiare il valore della chiave nella sezione **Chiavi** .</span><span class="sxs-lookup"><span data-stu-id="383cb-146">After the save finishes, copy the key value in the **keys** section.</span></span> <span data-ttu-id="383cb-147">Sarà necessario immettere questo valore nel codice in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="383cb-147">(You will need this value in your code later.)</span></span>

## <a name="create-a-key-vault-to-store-your-keys"></a><span data-ttu-id="383cb-148">Creare un insieme di credenziali delle chiavi per archiviare le chiavi</span><span class="sxs-lookup"><span data-stu-id="383cb-148">Create a key vault to store your keys</span></span>
<span data-ttu-id="383cb-149">Quando l'app client è configurata e si dispone dell'ID client, è necessario creare un insieme di credenziali delle chiavi e configurare il criterio di accesso per consentire all'utente e all'applicazione di accedere alle chiavi private dell'insieme di credenziali, ovvero le chiavi con crittografia sempre attiva.</span><span class="sxs-lookup"><span data-stu-id="383cb-149">Now that your client app is configured and you have your client ID, it's time to create a key vault and configure its access policy so you and your application can access the vault's secrets (the Always Encrypted keys).</span></span> <span data-ttu-id="383cb-150">Sono necessarie le autorizzazioni *create*, *get*, *list*, *sign*, *verify*, *wrapKey* e *unwrapKey* per creare una nuova chiave master di colonna e per configurare la crittografia con SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="383cb-150">The *create*, *get*, *list*, *sign*, *verify*, *wrapKey*, and *unwrapKey* permissions are required for creating a new column master key and for setting up encryption with SQL Server Management Studio.</span></span>

<span data-ttu-id="383cb-151">È possibile creare rapidamente un insieme di credenziali delle chiavi eseguendo lo script seguente.</span><span class="sxs-lookup"><span data-stu-id="383cb-151">You can quickly create a key vault by running the following script.</span></span> <span data-ttu-id="383cb-152">Per una spiegazione dettagliata di questi cmdlet e altre informazioni sulla creazione e la configurazione di un insieme di credenziali delle chiavi, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="383cb-152">For a detailed explanation of these cmdlets and more information about creating and configuring a key vault, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>

    $subscriptionName = '<your Azure subscription name>'
    $userPrincipalName = '<username@domain.com>'
    $clientId = '<client ID that you copied in step 7 above>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $vaultName = 'AeKeyVault'


    Login-AzureRmAccount
    $subscriptionId = (Get-AzureRmSubscription -SubscriptionName $subscriptionName).Id
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $resourceGroupName -Location $location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
    Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list




## <a name="create-a-blank-sql-database"></a><span data-ttu-id="383cb-153">Creare un database SQL vuoto</span><span class="sxs-lookup"><span data-stu-id="383cb-153">Create a blank SQL database</span></span>
1. <span data-ttu-id="383cb-154">Accedere al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="383cb-154">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="383cb-155">Fare clic su **Nuovo** > **Dati e archiviazione** > **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="383cb-155">Go to **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="383cb-156">Creare un database **vuoto** denominato **Clinic** in un server nuovo o esistente.</span><span class="sxs-lookup"><span data-stu-id="383cb-156">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="383cb-157">Per istruzioni dettagliate su come creare un database nel portale di Azure, vedere [Primo database SQL di Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="383cb-157">For detailed directions about how to create a database in the Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Creazione di un database vuoto](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

<span data-ttu-id="383cb-159">La stringa di connessione sarà necessaria più avanti nell'esercitazione. Dopo avere creato il database selezionare quindi il nuovo database Clinic e copiare la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="383cb-159">You will need the connection string later in the tutorial, so after you create the database, browse to the new  Clinic database and copy the connection string.</span></span> <span data-ttu-id="383cb-160">È possibile ottenere la stringa di connessione in qualsiasi momento, ma è facile copiarla nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="383cb-160">You can get the connection string at any time, but it's easy to copy it in the Azure portal.</span></span>

1. <span data-ttu-id="383cb-161">Passare a **Database SQL** > **Clinic** > **Show database connection strings** (Mostra stringhe di connessione del database).</span><span class="sxs-lookup"><span data-stu-id="383cb-161">Go to **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="383cb-162">Copiare la stringa di connessione per **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="383cb-162">Copy the connection string for **ADO.NET**.</span></span>
   
    ![Copia della stringa di connessione](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-to-the-database-with-ssms"></a><span data-ttu-id="383cb-164">Connettersi al database con SSMS</span><span class="sxs-lookup"><span data-stu-id="383cb-164">Connect to the database with SSMS</span></span>
<span data-ttu-id="383cb-165">Aprire SSMS e connettersi al server con il database Clinic.</span><span class="sxs-lookup"><span data-stu-id="383cb-165">Open SSMS and connect to the server with the Clinic database.</span></span>

1. <span data-ttu-id="383cb-166">Aprire SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="383cb-166">Open SSMS.</span></span> <span data-ttu-id="383cb-167">Passare a **Connetti** > **Motore di database** per aprire la finestra **Connetti al server**, se non è già aperta.</span><span class="sxs-lookup"><span data-stu-id="383cb-167">(Go to **Connect** > **Database Engine** to open the **Connect to Server** window if it isn't open.)</span></span>
2. <span data-ttu-id="383cb-168">Immettere il nome e le credenziali del server.</span><span class="sxs-lookup"><span data-stu-id="383cb-168">Enter your server name and credentials.</span></span> <span data-ttu-id="383cb-169">Il nome del server è disponibile nel pannello del database SQL e nella stringa di connessione copiata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="383cb-169">The server name can be found on the SQL database blade and in the connection string you copied earlier.</span></span> <span data-ttu-id="383cb-170">Digitare il nome completo del server, compreso *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="383cb-170">Type the complete server name, including *database.windows.net*.</span></span>
   
    ![Copia della stringa di connessione](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

<span data-ttu-id="383cb-172">Se viene visualizzata la finestra **Nuova regola firewall** , accedere ad Azure e lasciare che SSMS crei una nuova regola firewall per l'utente.</span><span class="sxs-lookup"><span data-stu-id="383cb-172">If the **New Firewall Rule** window opens, sign in to Azure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="383cb-173">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="383cb-173">Create a table</span></span>
<span data-ttu-id="383cb-174">Questa sezione contiene istruzioni per creare una tabella con i dati dei pazienti.</span><span class="sxs-lookup"><span data-stu-id="383cb-174">In this section, you will create a table to hold patient data.</span></span> <span data-ttu-id="383cb-175">Non è crittografata inizialmente e la crittografia verrà configurata nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="383cb-175">It's not initially encrypted--you will configure encryption in the next section.</span></span>

1. <span data-ttu-id="383cb-176">Espandere **Database**.</span><span class="sxs-lookup"><span data-stu-id="383cb-176">Expand **Databases**.</span></span>
2. <span data-ttu-id="383cb-177">Fare clic con il pulsante destro del mouse sul database **Clinic** e fare clic su **Nuova query**.</span><span class="sxs-lookup"><span data-stu-id="383cb-177">Right-click the **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="383cb-178">Incollare il comando Transact-SQL (T-SQL) seguente nella finestra della nuova query ed **eseguirlo** .</span><span class="sxs-lookup"><span data-stu-id="383cb-178">Paste the following Transact-SQL (T-SQL) into the new query window and **Execute** it.</span></span>

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


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="383cb-179">Crittografare le colonne configurando la crittografia sempre attiva</span><span class="sxs-lookup"><span data-stu-id="383cb-179">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="383cb-180">SSMS offre una procedura guidata per configurare facilmente la crittografia sempre attiva impostando la chiave master di colonna, la chiave di crittografia di colonna e le colonne crittografate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="383cb-180">SSMS provides a wizard that helps you easily configure Always Encrypted by setting up the column master key, column encryption key, and encrypted columns for you.</span></span>

1. <span data-ttu-id="383cb-181">Espandere **Database** > **Clinic** > **Tabelle**.</span><span class="sxs-lookup"><span data-stu-id="383cb-181">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="383cb-182">Fare clic con il pulsante destro del mouse sulla tabella **Patients** e selezionare **Crittografa colonne** per aprire la procedura guidata Always Encrypted:</span><span class="sxs-lookup"><span data-stu-id="383cb-182">Right-click the **Patients** table and select **Encrypt Columns** to open the Always Encrypted wizard:</span></span>
   
    ![Crittografa colonne](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

<span data-ttu-id="383cb-184">La procedura guidata Always Encrypted include le sezioni seguenti: **Selezione colonne**, **Configurazione della chiave master**, **Convalida** e **Riepilogo**.</span><span class="sxs-lookup"><span data-stu-id="383cb-184">The Always Encrypted wizard includes the following sections: **Column Selection**, **Master Key Configuration**, **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="383cb-185">Selezione colonne</span><span class="sxs-lookup"><span data-stu-id="383cb-185">Column Selection</span></span>
<span data-ttu-id="383cb-186">Fare clic su **Avanti** nella pagina **Introduzione** per aprire la pagina **Selezione colonne**.</span><span class="sxs-lookup"><span data-stu-id="383cb-186">Click **Next** on the **Introduction** page to open the **Column Selection** page.</span></span> <span data-ttu-id="383cb-187">In questa pagina verranno selezionate le colonne da crittografare, [il tipo di crittografia e la chiave di crittografia di colonna (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) da usare.</span><span class="sxs-lookup"><span data-stu-id="383cb-187">On this page, you will select which columns you want to encrypt, [the type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) to use.</span></span>

<span data-ttu-id="383cb-188">Crittografare il **CF** e la **data di nascita** per ogni paziente.</span><span class="sxs-lookup"><span data-stu-id="383cb-188">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="383cb-189">La colonna relativa al codice fiscale usa la crittografia deterministica, che supporta ricerche di uguaglianza, join e raggruppamenti.</span><span class="sxs-lookup"><span data-stu-id="383cb-189">The SSN column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="383cb-190">La colonna relativa alla data di nascita usa la crittografia casuale, che non supporta le operazioni.</span><span class="sxs-lookup"><span data-stu-id="383cb-190">The BirthDate column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="383cb-191">Impostare il **Tipo di crittografia** per la colonna CF su **Deterministica** e per la colonna Data di nascita su **Casuale**.</span><span class="sxs-lookup"><span data-stu-id="383cb-191">Set the **Encryption Type** for the SSN column to **Deterministic** and the BirthDate column to **Randomized**.</span></span> <span data-ttu-id="383cb-192">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="383cb-192">Click **Next**.</span></span>

![Crittografa colonne](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="383cb-194">Configurazione della chiave master</span><span class="sxs-lookup"><span data-stu-id="383cb-194">Master Key Configuration</span></span>
<span data-ttu-id="383cb-195">La pagina **Configurazione della chiave master** consente di impostare la CMK e selezionare il provider dell'archivio chiavi in cui verrà archiviata la CMK.</span><span class="sxs-lookup"><span data-stu-id="383cb-195">The **Master Key Configuration** page is where you set up your CMK and select the key store provider where the CMK will be stored.</span></span> <span data-ttu-id="383cb-196">Attualmente è possibile archiviare una chiave master di colonna nell'archivio certificati di Windows, nell'insieme di credenziali delle chiavi di Azure o in un modulo di protezione hardware.</span><span class="sxs-lookup"><span data-stu-id="383cb-196">Currently, you can store a CMK in the Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span>

<span data-ttu-id="383cb-197">Questa esercitazione illustra come archiviare le chiavi nell'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="383cb-197">This tutorial shows how to store your keys in Azure Key Vault.</span></span>

1. <span data-ttu-id="383cb-198">Selezionare **Insieme di credenziali delle chiavi di Azure**.</span><span class="sxs-lookup"><span data-stu-id="383cb-198">Select **Azure Key Vault**.</span></span>
2. <span data-ttu-id="383cb-199">Selezionare l'insieme di credenziali delle chiavi desiderato dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="383cb-199">Select the desired key vault from the drop-down list.</span></span>
3. <span data-ttu-id="383cb-200">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="383cb-200">Click **Next**.</span></span>

![Configurazione della chiave master](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="383cb-202">Convalida</span><span class="sxs-lookup"><span data-stu-id="383cb-202">Validation</span></span>
<span data-ttu-id="383cb-203">È attualmente possibile crittografare le colonne o salvare uno script di PowerShell da eseguire in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="383cb-203">You can encrypt the columns now or save a PowerShell script to run later.</span></span> <span data-ttu-id="383cb-204">Per questa esercitazione selezionare **Procedi per completare ora** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="383cb-204">For this tutorial, select **Proceed to finish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="383cb-205">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="383cb-205">Summary</span></span>
<span data-ttu-id="383cb-206">Verificare che tutte le impostazioni siano corrette e fare clic su **Fine** per completare la configurazione della crittografia sempre attiva.</span><span class="sxs-lookup"><span data-stu-id="383cb-206">Verify that the settings are all correct and click **Finish** to complete the setup for Always Encrypted.</span></span>

![Riepilogo](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-the-wizards-actions"></a><span data-ttu-id="383cb-208">Confermare le azioni della procedura guidata</span><span class="sxs-lookup"><span data-stu-id="383cb-208">Verify the wizard's actions</span></span>
<span data-ttu-id="383cb-209">Al termine della procedura guidata, il database è configurato per la crittografia sempre attiva.</span><span class="sxs-lookup"><span data-stu-id="383cb-209">After the wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="383cb-210">La procedura guidata esegue le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="383cb-210">The wizard performed the following actions:</span></span>

* <span data-ttu-id="383cb-211">È stata creata una chiave master di colonna ed è stata archiviata nell'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="383cb-211">Created a column master key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="383cb-212">È stata creata una chiave di crittografia di colonna ed è stata archiviata nell'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="383cb-212">Created a column encryption key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="383cb-213">Configurazione delle colonne selezionate per la crittografia.</span><span class="sxs-lookup"><span data-stu-id="383cb-213">Configured the selected columns for encryption.</span></span> <span data-ttu-id="383cb-214">La tabella Patients attualmente è vuota, ma eventuali dati esistenti nelle colonne selezionate sono ora crittografati.</span><span class="sxs-lookup"><span data-stu-id="383cb-214">The Patients table currently has no data, but any existing data in the selected columns is now encrypted.</span></span>

<span data-ttu-id="383cb-215">È possibile verificare la creazione di chiavi in SSMS espandendo **Clinic** > **Sicurezza** > **Chiavi Always Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="383cb-215">You can verify the creation of the keys in SSMS by expanding **Clinic** > **Security** > **Always Encrypted Keys**.</span></span>

## <a name="create-a-client-application-that-works-with-the-encrypted-data"></a><span data-ttu-id="383cb-216">Creare un'applicazione client che funziona con i dati crittografati</span><span class="sxs-lookup"><span data-stu-id="383cb-216">Create a client application that works with the encrypted data</span></span>
<span data-ttu-id="383cb-217">Ora che la crittografia Always Encrypted è configurata, è possibile creare un'applicazione che esegua *inserimenti* e *selezioni* nelle colonne crittografate.</span><span class="sxs-lookup"><span data-stu-id="383cb-217">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on the encrypted columns.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="383cb-218">L'applicazione deve usare oggetti [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) per trasferire dati di testo non crittografato al server con colonne con la crittografia sempre attiva.</span><span class="sxs-lookup"><span data-stu-id="383cb-218">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data to the server with Always Encrypted columns.</span></span> <span data-ttu-id="383cb-219">Il trasferimento di valori letterali senza usare oggetti SqlParameter genererà un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="383cb-219">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="383cb-220">Aprire Visual Studio e creare una nuova **Applicazione console** C# (Visual Studio 2015 e versioni precedenti) o **App console (.NET Framework)** (Visual Studio 2017 e versioni successive).</span><span class="sxs-lookup"><span data-stu-id="383cb-220">Open Visual Studio and create a new C# **Console Application** (Visual Studio 2015 and earlier) or **Console App (.NET Framework)** (Visual Studio 2017 and later).</span></span> <span data-ttu-id="383cb-221">Verificare che il progetto sia impostato su **.NET Framework 4.6** o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="383cb-221">Make sure your project is set to **.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="383cb-222">Denominare il progetto **AlwaysEncryptedConsoleAKVApp** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="383cb-222">Name the project **AlwaysEncryptedConsoleAKVApp** and click **OK**.</span></span>
3. <span data-ttu-id="383cb-223">Installare i pacchetti NuGet seguenti facendo clic su **Strumenti** > **Gestione pacchetti NuGet** > **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="383cb-223">Install the following NuGet packages by going to **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="383cb-224">Eseguire queste 2 righe di codice nella Console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="383cb-224">Run these two lines of code in the Package Manager Console.</span></span>

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-to-enable-always-encrypted"></a><span data-ttu-id="383cb-225">Modificare la stringa di connessione per abilitare la crittografia sempre attiva</span><span class="sxs-lookup"><span data-stu-id="383cb-225">Modify your connection string to enable Always Encrypted</span></span>
<span data-ttu-id="383cb-226">Questa sezione descrive come abilitare Always Encrypted nella stringa di connessione del database.</span><span class="sxs-lookup"><span data-stu-id="383cb-226">This section  explains how to enable Always Encrypted in your database connection string.</span></span>

<span data-ttu-id="383cb-227">Per abilitare Always Encrypted è necessario aggiungere la parola chiave di **Column Encryption Setting** alla stringa di connessione e impostarla su **Abilitata**.</span><span class="sxs-lookup"><span data-stu-id="383cb-227">To enable Always Encrypted, you need to add the **Column Encryption Setting** keyword to your connection string and set it to **Enabled**.</span></span>

<span data-ttu-id="383cb-228">È possibile impostarla direttamente nella stringa di connessione o tramite [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="383cb-228">You can set this directly in the connection string, or you can set it by using [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="383cb-229">L'applicazione di esempio nella sezione successiva mostra come usare **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="383cb-229">The sample application in the next section shows how to use **SqlConnectionStringBuilder**.</span></span>

### <a name="enable-always-encrypted-in-the-connection-string"></a><span data-ttu-id="383cb-230">Abilitare la crittografia sempre attiva nella stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="383cb-230">Enable Always Encrypted in the connection string</span></span>
<span data-ttu-id="383cb-231">Aggiungere la parola chiave seguente alla stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="383cb-231">Add the following keyword to your connection string.</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a><span data-ttu-id="383cb-232">Abilitare la crittografia sempre attiva con SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="383cb-232">Enable Always Encrypted with SqlConnectionStringBuilder</span></span>
<span data-ttu-id="383cb-233">Il codice seguente mostra come abilitare Always Encrypted impostando [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) su [Abilitata](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="383cb-233">The following code shows how to enable Always Encrypted by setting [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) to [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-the-azure-key-vault-provider"></a><span data-ttu-id="383cb-234">Registrare il provider dell'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="383cb-234">Register the Azure Key Vault provider</span></span>
<span data-ttu-id="383cb-235">Il codice seguente mostra come registrare il provider dell'insieme di credenziali delle chiavi di Azure con il driver ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="383cb-235">The following code shows how to register the Azure Key Vault provider with the ADO.NET driver.</span></span>

    private static ClientCredential _clientCredential;

    static void InitializeAzureKeyVaultProvider()
    {
       _clientCredential = new ClientCredential(clientId, clientSecret);

       SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
          new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

       Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
          new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

       providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
       SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
    }



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="383cb-236">Applicazione console di esempio della crittografia sempre attiva</span><span class="sxs-lookup"><span data-stu-id="383cb-236">Always Encrypted sample console application</span></span>
<span data-ttu-id="383cb-237">Questo esempio dimostra come:</span><span class="sxs-lookup"><span data-stu-id="383cb-237">This sample demonstrates how to:</span></span>

* <span data-ttu-id="383cb-238">Modificare la stringa di connessione per abilitare la crittografia sempre attiva.</span><span class="sxs-lookup"><span data-stu-id="383cb-238">Modify your connection string to enable Always Encrypted.</span></span>
* <span data-ttu-id="383cb-239">Registrare l'insieme di credenziali delle chiavi di Azure come provider dell'archivio chiavi dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="383cb-239">Register Azure Key Vault as the application's key store provider.</span></span>  
* <span data-ttu-id="383cb-240">Inserire dati nelle colonne crittografate.</span><span class="sxs-lookup"><span data-stu-id="383cb-240">Insert data into the encrypted columns.</span></span>
* <span data-ttu-id="383cb-241">Selezionare un record filtrando in base a un valore specifico in una colonna crittografata.</span><span class="sxs-lookup"><span data-stu-id="383cb-241">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="383cb-242">Sostituire il contenuto del file **Program.cs** con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="383cb-242">Replace the contents of **Program.cs** with the following code.</span></span> <span data-ttu-id="383cb-243">Sostituire la stringa di connessione per la variabile globale connectionString nella riga che precede immediatamente il metodo Main con la stringa di connessione valida del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="383cb-243">Replace the connection string for the global connectionString variable in the line that directly precedes the Main method with your valid connection string from the Azure portal.</span></span> <span data-ttu-id="383cb-244">Questa è l'unica modifica che è necessario apportare al codice.</span><span class="sxs-lookup"><span data-stu-id="383cb-244">This is the only change you need to make to this code.</span></span>

<span data-ttu-id="383cb-245">Eseguire l'app per vedere in azione la crittografia sempre attiva.</span><span class="sxs-lookup"><span data-stu-id="383cb-245">Run the app to see Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider;

    namespace AlwaysEncryptedConsoleAKVApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from the Azure portal.
        static string connectionString = @"<connection string from the portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

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

            InsertPatient(new Patient()
            {
                SSN = "999-99-0001",
                FirstName = "Orlando",
                LastName = "Gee",
                BirthDate = DateTime.Parse("01/04/1964")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0002",
                FirstName = "Keith",
                LastName = "Harris",
                BirthDate = DateTime.Parse("06/20/1977")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0003",
                FirstName = "Donna",
                LastName = "Carreras",
                BirthDate = DateTime.Parse("02/09/1973")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0004",
                FirstName = "Janet",
                LastName = "Gates",
                BirthDate = DateTime.Parse("08/31/1985")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0005",
                FirstName = "Lucy",
                LastName = "Harrington",
                BirthDate = DateTime.Parse("05/06/1993")
            });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All the records currently in the Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching the encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that the user entered 11 characters.
            // In production be sure to check all user input and use the best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
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


        private static ClientCredential _clientCredential;

        static void InitializeAzureKeyVaultProvider()
        {

            _clientCredential = new ClientCredential(clientId, clientSecret);

            SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
              new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

            Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
              new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

            providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        }

        public async static Task<string> GetToken(string authority, string resource, string scope)
        {
            var authContext = new AuthenticationContext(authority);
            AuthenticationResult result = await authContext.AcquireTokenAsync(resource, _clientCredential);

            if (result == null)
                throw new InvalidOperationException("Failed to obtain the access token");
            return result.AccessToken;
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



## <a name="verify-that-the-data-is-encrypted"></a><span data-ttu-id="383cb-246">Verificare che i dati siano crittografati</span><span class="sxs-lookup"><span data-stu-id="383cb-246">Verify that the data is encrypted</span></span>
<span data-ttu-id="383cb-247">È possibile verificare rapidamente che i dati effettivi del server siano crittografati eseguendo una query dei dati della tabella Patients con SSMS tramite la connessione corrente in cui l'impostazione **Column Encryption Setting** non è ancora abilitata.</span><span class="sxs-lookup"><span data-stu-id="383cb-247">You can quickly check that the actual data on the server is encrypted by querying the Patients data with SSMS (using your current connection where **Column Encryption Setting** is not yet enabled).</span></span>

<span data-ttu-id="383cb-248">Eseguire la query seguente nel database Clinic.</span><span class="sxs-lookup"><span data-stu-id="383cb-248">Run the following query on the Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="383cb-249">È possibile osservare che le colonne crittografate non contengono dati di testo non crittografato.</span><span class="sxs-lookup"><span data-stu-id="383cb-249">You can see that the encrypted columns do not contain any plaintext data.</span></span>

   ![Nuova applicazione console](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

<span data-ttu-id="383cb-251">Per usare SSMS per accedere ai dati di testo non crittografato, aggiungere il parametro *Column Encryption Setting=Enabled* alla connessione.</span><span class="sxs-lookup"><span data-stu-id="383cb-251">To use SSMS to access the plaintext data, you can add the *Column Encryption Setting=enabled* parameter to the connection.</span></span>

1. <span data-ttu-id="383cb-252">In SSMS fare clic con il pulsante destro del mouse sul server in **Esplora oggetti** e scegliere **Disconnetti**.</span><span class="sxs-lookup"><span data-stu-id="383cb-252">In SSMS, right-click your server in **Object Explorer** and choose **Disconnect**.</span></span>
2. <span data-ttu-id="383cb-253">Fare clic su **Connetti** > **Motore di database** per aprire la finestra **Connetti al server** e quindi fare clic su **Opzioni**.</span><span class="sxs-lookup"><span data-stu-id="383cb-253">Click **Connect** > **Database Engine** to open the **Connect to Server** window and click **Options**.</span></span>
3. <span data-ttu-id="383cb-254">Fare clic su **Parametri aggiuntivi per la connessione** e digitare **Column Encryption Setting=Enabled**.</span><span class="sxs-lookup"><span data-stu-id="383cb-254">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Nuova applicazione console](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. <span data-ttu-id="383cb-256">Eseguire la query seguente nel database Clinic.</span><span class="sxs-lookup"><span data-stu-id="383cb-256">Run the following query on the Clinic database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="383cb-257">È ora possibile visualizzare i dati non crittografati nelle colonne crittografate.</span><span class="sxs-lookup"><span data-stu-id="383cb-257">You can now see the plaintext data in the encrypted columns.</span></span>

    ![Nuova applicazione console](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a><span data-ttu-id="383cb-259">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="383cb-259">Next steps</span></span>
<span data-ttu-id="383cb-260">Dopo avere creato un database che usa la crittografia sempre attiva, è possibile eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="383cb-260">After you create a database that uses Always Encrypted, you may want to do the following:</span></span>

* <span data-ttu-id="383cb-261">[Ruotare e pulire le chiavi](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="383cb-261">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="383cb-262">[Eseguire la migrazione dei dati già crittografati con la crittografia sempre attiva](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="383cb-262">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>

## <a name="related-information"></a><span data-ttu-id="383cb-263">Informazioni correlate</span><span class="sxs-lookup"><span data-stu-id="383cb-263">Related information</span></span>
* [<span data-ttu-id="383cb-264">Crittografia sempre attiva (sviluppo di client)</span><span class="sxs-lookup"><span data-stu-id="383cb-264">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="383cb-265">Transparent Data Encryption</span><span class="sxs-lookup"><span data-stu-id="383cb-265">Transparent data encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="383cb-266">Crittografia di SQL Server</span><span class="sxs-lookup"><span data-stu-id="383cb-266">SQL Server encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="383cb-267">Procedura guidata per la crittografia sempre attiva</span><span class="sxs-lookup"><span data-stu-id="383cb-267">Always Encrypted wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="383cb-268">Blog della crittografia sempre attiva</span><span class="sxs-lookup"><span data-stu-id="383cb-268">Always Encrypted blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

