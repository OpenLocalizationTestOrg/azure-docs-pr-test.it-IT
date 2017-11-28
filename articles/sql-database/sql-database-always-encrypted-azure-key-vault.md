---
title: 'Always Encrypted: database SQL - Azure Key Vault | Documentazione Microsoft'
description: Questo articolo illustra come i dati sensibili in un database SQL con i dati utilizzando la crittografia toosecure hello guidata su Always Encrypted in SQL Server Management Studio. Include inoltre istruzioni verranno illustrato come toostore ogni chiave di crittografia nell'insieme di credenziali chiave di Azure.
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
ms.openlocfilehash: 8226bfef584e979643f5bb0747d4df16569f8204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a><span data-ttu-id="40002-105">Crittografia sempre attiva: Proteggere i dati sensibili nel database SQL e archiviare le chiavi di crittografia nell'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="40002-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in Azure Key Vault</span></span>

<span data-ttu-id="40002-106">Questo articolo illustra come toosecure dati sensibili in un SQL database con la crittografia dei dati utilizzando hello [procedura guidata Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="40002-106">This article shows you how toosecure sensitive data in a SQL database with data encryption using hello [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="40002-107">Include inoltre istruzioni verranno illustrato come toostore ogni chiave di crittografia nell'insieme di credenziali chiave di Azure.</span><span class="sxs-lookup"><span data-stu-id="40002-107">It also includes instructions that will show you how toostore each encryption key in Azure Key Vault.</span></span>

<span data-ttu-id="40002-108">Always Encrypted è una nuova tecnologia di crittografia di dati in Database SQL di Azure e SQL Server che consente di proteggere i dati sensibili archiviati nel server di hello, durante lo spostamento tra client e server, mentre i dati di hello sono in uso.</span><span class="sxs-lookup"><span data-stu-id="40002-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on hello server, during movement between client and server, and while hello data is in use.</span></span> <span data-ttu-id="40002-109">Sempre crittografato assicura che i dati sensibili mai viene visualizzato come testo non crittografato hello sistema di database.</span><span class="sxs-lookup"><span data-stu-id="40002-109">Always Encrypted ensures that sensitive data never appears as plaintext inside hello database system.</span></span> <span data-ttu-id="40002-110">Dopo aver configurato la crittografia dei dati, solo le applicazioni client o server applicazioni che dispongono di chiavi di accesso toohello possibile accedere a dati in testo normale.</span><span class="sxs-lookup"><span data-stu-id="40002-110">After you configure data encryption, only client applications or app servers that have access toohello keys can access plaintext data.</span></span> <span data-ttu-id="40002-111">Per informazioni dettagliate, vedere l'articolo relativo alla [crittografia sempre attiva (motore di database)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="40002-111">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="40002-112">Dopo aver configurato hello database toouse Always Encrypted, si creerà un'applicazione client in c# con Visual Studio toowork con dati crittografato hello.</span><span class="sxs-lookup"><span data-stu-id="40002-112">After you configure hello database toouse Always Encrypted, you will create a client application in C# with Visual Studio toowork with hello encrypted data.</span></span>

<span data-ttu-id="40002-113">Seguire i passaggi di hello in questo articolo e informazioni su come tooset di crittografia sempre attiva per un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="40002-113">Follow hello steps in this article and learn how tooset up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="40002-114">In questo articolo si apprenderà come hello tooperform seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="40002-114">In this article you will learn how tooperform hello following tasks:</span></span>

* <span data-ttu-id="40002-115">Utilizzare guidata sempre crittografato hello in SSMS toocreate [chiavi Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="40002-115">Use hello Always Encrypted wizard in SSMS toocreate [Always Encrypted keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="40002-116">Creare una [chiave master di colonna (CMK, Column Master Key)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="40002-116">Create a [column master key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="40002-117">Creare una [chiave di crittografia di colonna (CEK, Column Encryption Key)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="40002-117">Create a [column encryption key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="40002-118">Creare una tabella di database e crittografare le colonne.</span><span class="sxs-lookup"><span data-stu-id="40002-118">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="40002-119">Creare un'applicazione che inserisce, seleziona e visualizza i dati dalle colonne crittografato hello.</span><span class="sxs-lookup"><span data-stu-id="40002-119">Create an application that inserts, selects, and displays data from hello encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40002-120">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="40002-120">Prerequisites</span></span>
<span data-ttu-id="40002-121">Per questa esercitazione occorrono:</span><span class="sxs-lookup"><span data-stu-id="40002-121">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="40002-122">Un account e una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="40002-122">An Azure account and subscription.</span></span> <span data-ttu-id="40002-123">Nel caso in cui non siano disponibili, è possibile usare una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="40002-123">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="40002-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versione 13.0.700.242 o successive.</span><span class="sxs-lookup"><span data-stu-id="40002-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="40002-125">[.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) o versione successiva (computer hello client).</span><span class="sxs-lookup"><span data-stu-id="40002-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on hello client computer).</span></span>
* <span data-ttu-id="40002-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="40002-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>
* <span data-ttu-id="40002-127">[Azure PowerShell](/powershell/azure/overview) versione 1.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="40002-127">[Azure PowerShell](/powershell/azure/overview), version  1.0 or later.</span></span> <span data-ttu-id="40002-128">Tipo **(Get-Module - ListAvailable azure). Versione** toosee quale versione di PowerShell in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="40002-128">Type **(Get-Module azure -ListAvailable).Version** toosee what version of PowerShell you are running.</span></span>

## <a name="enable-your-client-application-tooaccess-hello-sql-database-service"></a><span data-ttu-id="40002-129">Abilitare il servizio di Database SQL client applicazione tooaccess hello</span><span class="sxs-lookup"><span data-stu-id="40002-129">Enable your client application tooaccess hello SQL Database service</span></span>
<span data-ttu-id="40002-130">È necessario abilitare il servizio Database SQL di hello tooaccess di applicazione client tramite la configurazione di autenticazione richiesto hello e hello durante l'acquisizione dei *ClientId* e *Secret* che sarà necessario tooauthenticate l'applicazione nel seguente codice hello.</span><span class="sxs-lookup"><span data-stu-id="40002-130">You must enable your client application tooaccess hello SQL Database service by setting up hello required authentication and acquiring hello *ClientId* and *Secret* that you will need tooauthenticate your application in hello following code.</span></span>

1. <span data-ttu-id="40002-131">Aprire hello [portale di Azure classico](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="40002-131">Open hello [Azure classic portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="40002-132">Selezionare **Active Directory** e fare clic sull'istanza hello Active Directory che verrà utilizzato dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="40002-132">Select **Active Directory** and click hello Active Directory instance that your application will use.</span></span>
3. <span data-ttu-id="40002-133">Fare clic su **Applicazioni** e quindi su **AGGIUNGI**.</span><span class="sxs-lookup"><span data-stu-id="40002-133">Click **Applications**, and then click **ADD**.</span></span>
4. <span data-ttu-id="40002-134">Digitare un nome per l'applicazione (ad esempio: *myClientApp*), selezionare **applicazione WEB**, fare clic su toocontinue freccia hello.</span><span class="sxs-lookup"><span data-stu-id="40002-134">Type a name for your application (for example: *myClientApp*), select **WEB APPLICATION**, and click hello arrow toocontinue.</span></span>
5. <span data-ttu-id="40002-135">Per hello **URL accesso** e **URI ID APP** è possibile digitare un URL valido (ad esempio, *http://myClientApp*) e continuare.</span><span class="sxs-lookup"><span data-stu-id="40002-135">For hello **SIGN-ON URL** and **APP ID URI** you can type a valid URL (for example, *http://myClientApp*) and continue.</span></span>
6. <span data-ttu-id="40002-136">Fare clic su **CONFIGURA**.</span><span class="sxs-lookup"><span data-stu-id="40002-136">Click **CONFIGURE**.</span></span>
7. <span data-ttu-id="40002-137">Copiare l' **ID CLIENT**.</span><span class="sxs-lookup"><span data-stu-id="40002-137">Copy your **CLIENT ID**.</span></span> <span data-ttu-id="40002-138">Sarà necessario immettere questo valore nel codice in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="40002-138">(You will need this value in your code later.)</span></span>
8. <span data-ttu-id="40002-139">In hello **chiavi** selezionare **1 anno** da hello **Seleziona durata** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="40002-139">In hello **keys** section, select **1 year** from hello  **Select duration** drop-down list.</span></span> <span data-ttu-id="40002-140">(Verrà copiato chiave hello dopo aver salvato nel passaggio 13.)</span><span class="sxs-lookup"><span data-stu-id="40002-140">(You will copy hello key after you save in step 13.)</span></span>
9. <span data-ttu-id="40002-141">Scorrere verso il basso e fare clic su **Aggiungi applicazione**.</span><span class="sxs-lookup"><span data-stu-id="40002-141">Scroll down and click **Add application**.</span></span>
10. <span data-ttu-id="40002-142">Lasciare **Mostra** impostare troppo**Microsoft Apps** e selezionare **servizio Gestione API di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="40002-142">Leave **SHOW** set too**Microsoft Apps** and select **Microsoft Azure Service Management API**.</span></span> <span data-ttu-id="40002-143">Fare clic su hello toocontinue di segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="40002-143">Click hello checkmark toocontinue.</span></span>
11. <span data-ttu-id="40002-144">Selezionare **accedere a Gestione servizi di Azure... ** da hello **autorizzazioni delegate** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="40002-144">Select **Access Azure Service Management...** from hello **Delegated Permissions** drop-down list.</span></span>
12. <span data-ttu-id="40002-145">Fare clic su **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="40002-145">Click **SAVE**.</span></span>
13. <span data-ttu-id="40002-146">Dopo aver hello Salva al termine, copiare valore chiave hello hello **chiavi** sezione.</span><span class="sxs-lookup"><span data-stu-id="40002-146">After hello save finishes, copy hello key value in hello **keys** section.</span></span> <span data-ttu-id="40002-147">Sarà necessario immettere questo valore nel codice in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="40002-147">(You will need this value in your code later.)</span></span>

## <a name="create-a-key-vault-toostore-your-keys"></a><span data-ttu-id="40002-148">Creare un insieme di credenziali chiave di toostore delle chiavi</span><span class="sxs-lookup"><span data-stu-id="40002-148">Create a key vault toostore your keys</span></span>
<span data-ttu-id="40002-149">Ora che è configurato l'app client e si ha l'ID client, è ora toocreate un insieme di credenziali chiave e configurare i criteri di accesso, pertanto si e l'applicazione può accedere a informazioni riservate dell'insieme di credenziali di hello (le chiavi sempre crittografato hello).</span><span class="sxs-lookup"><span data-stu-id="40002-149">Now that your client app is configured and you have your client ID, it's time toocreate a key vault and configure its access policy so you and your application can access hello vault's secrets (hello Always Encrypted keys).</span></span> <span data-ttu-id="40002-150">Hello *creare*, *ottenere*, *elenco*, *sign*, *verificare*, *wrapKey*, e *unwrapKey* le autorizzazioni sono necessarie per la creazione di una nuova chiave master di colonna e per la configurazione di crittografia con SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="40002-150">hello *create*, *get*, *list*, *sign*, *verify*, *wrapKey*, and *unwrapKey* permissions are required for creating a new column master key and for setting up encryption with SQL Server Management Studio.</span></span>

<span data-ttu-id="40002-151">È possibile creare rapidamente un insieme di credenziali chiave eseguendo lo script seguente hello.</span><span class="sxs-lookup"><span data-stu-id="40002-151">You can quickly create a key vault by running hello following script.</span></span> <span data-ttu-id="40002-152">Per una spiegazione dettagliata di questi cmdlet e altre informazioni sulla creazione e la configurazione di un insieme di credenziali delle chiavi, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="40002-152">For a detailed explanation of these cmdlets and more information about creating and configuring a key vault, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>

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




## <a name="create-a-blank-sql-database"></a><span data-ttu-id="40002-153">Creare un database SQL vuoto</span><span class="sxs-lookup"><span data-stu-id="40002-153">Create a blank SQL database</span></span>
1. <span data-ttu-id="40002-154">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="40002-154">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="40002-155">Andare troppo**New** > **dati e archiviazione** > **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="40002-155">Go too**New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="40002-156">Creare un database **vuoto** denominato **Clinic** in un server nuovo o esistente.</span><span class="sxs-lookup"><span data-stu-id="40002-156">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="40002-157">Per istruzioni su come toocreate un database nel portale di Azure hello visualizzato [di un database SQL di Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="40002-157">For detailed directions about how toocreate a database in hello Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Creazione di un database vuoto](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

<span data-ttu-id="40002-159">Si sarà necessario hello stringa di connessione in un secondo momento nell'esercitazione di hello, dopo aver creato il database di hello, selezionare toohello nuova Clinic database e la copia hello stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="40002-159">You will need hello connection string later in hello tutorial, so after you create hello database, browse toohello new  Clinic database and copy hello connection string.</span></span> <span data-ttu-id="40002-160">È possibile ottenere la stringa di connessione hello in qualsiasi momento, ma è facile toocopy in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="40002-160">You can get hello connection string at any time, but it's easy toocopy it in hello Azure portal.</span></span>

1. <span data-ttu-id="40002-161">Andare troppo**database SQL** > **Clinic** > **Mostra le stringhe di connessione di database**.</span><span class="sxs-lookup"><span data-stu-id="40002-161">Go too**SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="40002-162">Copiare la stringa di connessione hello per **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="40002-162">Copy hello connection string for **ADO.NET**.</span></span>
   
    ![Copiare la stringa di connessione hello](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="40002-164">La connessione a database toohello con SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="40002-164">Connect toohello database with SSMS</span></span>
<span data-ttu-id="40002-165">Aprire SQL Server Management Studio e connettersi toohello server con database Clinic hello.</span><span class="sxs-lookup"><span data-stu-id="40002-165">Open SSMS and connect toohello server with hello Clinic database.</span></span>

1. <span data-ttu-id="40002-166">Aprire SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="40002-166">Open SSMS.</span></span> <span data-ttu-id="40002-167">(Vai troppo**Connetti** > **motore di Database** tooopen hello **connettersi tooServer** finestra se non è aperto.)</span><span class="sxs-lookup"><span data-stu-id="40002-167">(Go too**Connect** > **Database Engine** tooopen hello **Connect tooServer** window if it isn't open.)</span></span>
2. <span data-ttu-id="40002-168">Immettere il nome e le credenziali del server.</span><span class="sxs-lookup"><span data-stu-id="40002-168">Enter your server name and credentials.</span></span> <span data-ttu-id="40002-169">nome del server Hello sono disponibili nel Pannello di database SQL di hello e nella stringa di connessione hello copiato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="40002-169">hello server name can be found on hello SQL database blade and in hello connection string you copied earlier.</span></span> <span data-ttu-id="40002-170">Nome completo del server di tipo hello, tra cui *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="40002-170">Type hello complete server name, including *database.windows.net*.</span></span>
   
    ![Copiare la stringa di connessione hello](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

<span data-ttu-id="40002-172">Se hello **nuova regola Firewall** viene visualizzata la finestra Accedi tooAzure e consentono di SQL Server Management Studio creare una nuova regola firewall per l'utente.</span><span class="sxs-lookup"><span data-stu-id="40002-172">If hello **New Firewall Rule** window opens, sign in tooAzure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="40002-173">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="40002-173">Create a table</span></span>
<span data-ttu-id="40002-174">In questa sezione si creerà un pazienti toohold di tabella.</span><span class="sxs-lookup"><span data-stu-id="40002-174">In this section, you will create a table toohold patient data.</span></span> <span data-ttu-id="40002-175">Non è inizialmente crittografati, si configurerà la crittografia nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="40002-175">It's not initially encrypted--you will configure encryption in hello next section.</span></span>

1. <span data-ttu-id="40002-176">Espandere **Database**.</span><span class="sxs-lookup"><span data-stu-id="40002-176">Expand **Databases**.</span></span>
2. <span data-ttu-id="40002-177">Pulsante destro del mouse hello **Clinic** database e fare clic su **nuova Query**.</span><span class="sxs-lookup"><span data-stu-id="40002-177">Right-click hello **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="40002-178">Hello Incolla seguente Transact-SQL (T-SQL) in nuova finestra query di hello e **Execute** è.</span><span class="sxs-lookup"><span data-stu-id="40002-178">Paste hello following Transact-SQL (T-SQL) into hello new query window and **Execute** it.</span></span>

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


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="40002-179">Crittografare le colonne configurando la crittografia sempre attiva</span><span class="sxs-lookup"><span data-stu-id="40002-179">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="40002-180">SQL Server Management Studio fornisce una procedura guidata che consente di configurare facilmente Always Encrypted tramite la configurazione di hello chiave master della colonna chiave di crittografia di colonna e le colonne crittografate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="40002-180">SSMS provides a wizard that helps you easily configure Always Encrypted by setting up hello column master key, column encryption key, and encrypted columns for you.</span></span>

1. <span data-ttu-id="40002-181">Espandere **Database** > **Clinic** > **Tabelle**.</span><span class="sxs-lookup"><span data-stu-id="40002-181">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="40002-182">Pulsante destro del mouse hello **pazienti** tabella e selezionare **crittografa colonne** guidata sempre crittografato hello di tooopen:</span><span class="sxs-lookup"><span data-stu-id="40002-182">Right-click hello **Patients** table and select **Encrypt Columns** tooopen hello Always Encrypted wizard:</span></span>
   
    ![Crittografa colonne](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

<span data-ttu-id="40002-184">Creazione guidata sempre crittografato Hello include hello le sezioni seguenti: **selezione colonna**, **configurazione chiave Master**, **convalida**, e **riepilogo **.</span><span class="sxs-lookup"><span data-stu-id="40002-184">hello Always Encrypted wizard includes hello following sections: **Column Selection**, **Master Key Configuration**, **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="40002-185">Selezione colonne</span><span class="sxs-lookup"><span data-stu-id="40002-185">Column Selection</span></span>
<span data-ttu-id="40002-186">Fare clic su **Avanti** su hello **Introduzione** hello tooopen pagina **selezione colonna** pagina.</span><span class="sxs-lookup"><span data-stu-id="40002-186">Click **Next** on hello **Introduction** page tooopen hello **Column Selection** page.</span></span> <span data-ttu-id="40002-187">In questa pagina, verranno selezionate le colonne desiderate tooencrypt, [hello tipo di crittografia e specificare la chiave di crittografia di colonna (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span><span class="sxs-lookup"><span data-stu-id="40002-187">On this page, you will select which columns you want tooencrypt, [hello type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span></span>

<span data-ttu-id="40002-188">Crittografare il **CF** e la **data di nascita** per ogni paziente.</span><span class="sxs-lookup"><span data-stu-id="40002-188">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="40002-189">colonna SSN Hello utilizzerà la crittografia deterministica, che supporta le ricerche di uguaglianza, join e group by.</span><span class="sxs-lookup"><span data-stu-id="40002-189">hello SSN column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="40002-190">colonna BirthDate Hello utilizzerà la crittografia casuale, che non supporta le operazioni.</span><span class="sxs-lookup"><span data-stu-id="40002-190">hello BirthDate column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="40002-191">Set hello **tipo di crittografia** per la colonna SSN hello troppo**deterministica** e hello colonna BirthDate troppo**casuale**.</span><span class="sxs-lookup"><span data-stu-id="40002-191">Set hello **Encryption Type** for hello SSN column too**Deterministic** and hello BirthDate column too**Randomized**.</span></span> <span data-ttu-id="40002-192">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="40002-192">Click **Next**.</span></span>

![Crittografa colonne](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="40002-194">Configurazione della chiave master</span><span class="sxs-lookup"><span data-stu-id="40002-194">Master Key Configuration</span></span>
<span data-ttu-id="40002-195">Hello **configurazione chiave Master** pagina è in cui impostare la CMK e provider dell'archivio chiavi hello selezionare dove hello CMK verranno archiviati.</span><span class="sxs-lookup"><span data-stu-id="40002-195">hello **Master Key Configuration** page is where you set up your CMK and select hello key store provider where hello CMK will be stored.</span></span> <span data-ttu-id="40002-196">Attualmente, è possibile archiviare una chiave CMK nell'archivio certificati di Windows hello, insieme di credenziali chiave di Azure o un modulo di protezione hardware (HSM).</span><span class="sxs-lookup"><span data-stu-id="40002-196">Currently, you can store a CMK in hello Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span>

<span data-ttu-id="40002-197">Questa esercitazione viene illustrato come toostore le chiavi nell'insieme di credenziali chiave di Azure.</span><span class="sxs-lookup"><span data-stu-id="40002-197">This tutorial shows how toostore your keys in Azure Key Vault.</span></span>

1. <span data-ttu-id="40002-198">Selezionare **Insieme di credenziali delle chiavi di Azure**.</span><span class="sxs-lookup"><span data-stu-id="40002-198">Select **Azure Key Vault**.</span></span>
2. <span data-ttu-id="40002-199">Selezionare hello desiderato insieme di credenziali chiave dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="40002-199">Select hello desired key vault from hello drop-down list.</span></span>
3. <span data-ttu-id="40002-200">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="40002-200">Click **Next**.</span></span>

![Configurazione della chiave master](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="40002-202">Convalida</span><span class="sxs-lookup"><span data-stu-id="40002-202">Validation</span></span>
<span data-ttu-id="40002-203">È possibile crittografare colonne hello ora o salvare un toorun di script di PowerShell in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="40002-203">You can encrypt hello columns now or save a PowerShell script toorun later.</span></span> <span data-ttu-id="40002-204">Per questa esercitazione, selezionare **procedere ora toofinish** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="40002-204">For this tutorial, select **Proceed toofinish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="40002-205">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="40002-205">Summary</span></span>
<span data-ttu-id="40002-206">Verificare che le impostazioni di hello siano tutti corrette e fare clic su **fine** installazione hello toocomplete per Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="40002-206">Verify that hello settings are all correct and click **Finish** toocomplete hello setup for Always Encrypted.</span></span>

![Riepilogo](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-hello-wizards-actions"></a><span data-ttu-id="40002-208">Verificare le azioni della procedura guidata di hello</span><span class="sxs-lookup"><span data-stu-id="40002-208">Verify hello wizard's actions</span></span>
<span data-ttu-id="40002-209">Al termine procedura hello, il database è configurato per Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="40002-209">After hello wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="40002-210">Hello hello di guidata eseguito le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="40002-210">hello wizard performed hello following actions:</span></span>

* <span data-ttu-id="40002-211">È stata creata una chiave master di colonna ed è stata archiviata nell'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="40002-211">Created a column master key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="40002-212">È stata creata una chiave di crittografia di colonna ed è stata archiviata nell'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="40002-212">Created a column encryption key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="40002-213">Hello configurato selezionate colonne per la crittografia.</span><span class="sxs-lookup"><span data-stu-id="40002-213">Configured hello selected columns for encryption.</span></span> <span data-ttu-id="40002-214">tabella pazienti Hello attualmente non dispone di dati, ma i dati esistenti nelle colonne selezionata hello ora sono crittografati.</span><span class="sxs-lookup"><span data-stu-id="40002-214">hello Patients table currently has no data, but any existing data in hello selected columns is now encrypted.</span></span>

<span data-ttu-id="40002-215">È possibile verificare la creazione di hello di chiavi hello in SQL Server Management Studio espandere **Clinic** > **sicurezza** > **le chiavi Always Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="40002-215">You can verify hello creation of hello keys in SSMS by expanding **Clinic** > **Security** > **Always Encrypted Keys**.</span></span>

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a><span data-ttu-id="40002-216">Creare un'applicazione client che interagisce con i dati crittografato hello</span><span class="sxs-lookup"><span data-stu-id="40002-216">Create a client application that works with hello encrypted data</span></span>
<span data-ttu-id="40002-217">Ora che Always Encrypted è configurato, è possibile compilare un'applicazione che esegue *inserisce* e *seleziona* su hello colonne crittografate.</span><span class="sxs-lookup"><span data-stu-id="40002-217">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on hello encrypted columns.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="40002-218">L'applicazione deve usare [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) oggetti quando si passa server toohello dati di testo normale con colonne con crittografia sempre attiva.</span><span class="sxs-lookup"><span data-stu-id="40002-218">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data toohello server with Always Encrypted columns.</span></span> <span data-ttu-id="40002-219">Il trasferimento di valori letterali senza usare oggetti SqlParameter genererà un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="40002-219">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="40002-220">Aprire Visual Studio e creare una nuova **Applicazione console** C# (Visual Studio 2015 e versioni precedenti) o **App console (.NET Framework)** (Visual Studio 2017 e versioni successive).</span><span class="sxs-lookup"><span data-stu-id="40002-220">Open Visual Studio and create a new C# **Console Application** (Visual Studio 2015 and earlier) or **Console App (.NET Framework)** (Visual Studio 2017 and later).</span></span> <span data-ttu-id="40002-221">Verificare che il progetto è stato impostato troppo**.NET Framework 4.6** o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="40002-221">Make sure your project is set too**.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="40002-222">Progetto hello nome **AlwaysEncryptedConsoleAKVApp** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="40002-222">Name hello project **AlwaysEncryptedConsoleAKVApp** and click **OK**.</span></span>
3. <span data-ttu-id="40002-223">Installare i seguenti pacchetti NuGet passando troppo hello**strumenti** > **Gestione pacchetti NuGet** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="40002-223">Install hello following NuGet packages by going too**Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="40002-224">Nella Console di gestione pacchetti hello, eseguire le due righe di codice.</span><span class="sxs-lookup"><span data-stu-id="40002-224">Run these two lines of code in hello Package Manager Console.</span></span>

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-tooenable-always-encrypted"></a><span data-ttu-id="40002-225">Modificare il tooenable di stringa di connessione Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="40002-225">Modify your connection string tooenable Always Encrypted</span></span>
<span data-ttu-id="40002-226">Questa sezione viene illustrato come tooenable sempre crittografato nella stringa di connessione di database.</span><span class="sxs-lookup"><span data-stu-id="40002-226">This section  explains how tooenable Always Encrypted in your database connection string.</span></span>

<span data-ttu-id="40002-227">tooenable Always Encrypted, è necessario hello tooadd **Column Encryption Setting** connessione tooyour parola chiave di stringa e impostarlo troppo**abilitato**.</span><span class="sxs-lookup"><span data-stu-id="40002-227">tooenable Always Encrypted, you need tooadd hello **Column Encryption Setting** keyword tooyour connection string and set it too**Enabled**.</span></span>

<span data-ttu-id="40002-228">È possibile impostare questo valore direttamente nella stringa di connessione hello oppure è possibile impostarlo utilizzando [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="40002-228">You can set this directly in hello connection string, or you can set it by using [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="40002-229">applicazione di esempio Hello hello sezione successiva viene illustrato come toouse **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="40002-229">hello sample application in hello next section shows how toouse **SqlConnectionStringBuilder**.</span></span>

### <a name="enable-always-encrypted-in-hello-connection-string"></a><span data-ttu-id="40002-230">Abilita sempre crittografato nella stringa di connessione hello</span><span class="sxs-lookup"><span data-stu-id="40002-230">Enable Always Encrypted in hello connection string</span></span>
<span data-ttu-id="40002-231">Aggiungere hello seguente stringa di connessione tooyour (parola chiave).</span><span class="sxs-lookup"><span data-stu-id="40002-231">Add hello following keyword tooyour connection string.</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a><span data-ttu-id="40002-232">Abilitare la crittografia sempre attiva con SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="40002-232">Enable Always Encrypted with SqlConnectionStringBuilder</span></span>
<span data-ttu-id="40002-233">Hello seguente codice mostra come tooenable Always Encrypted impostando [Columnencryptionsetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) troppo[abilitato](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="40002-233">hello following code shows how tooenable Always Encrypted by setting [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) too[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-hello-azure-key-vault-provider"></a><span data-ttu-id="40002-234">Registrare il provider di credenziali chiave hello</span><span class="sxs-lookup"><span data-stu-id="40002-234">Register hello Azure Key Vault provider</span></span>
<span data-ttu-id="40002-235">Hello codice seguente viene illustrato come tooregister hello provider insieme credenziali chiavi Azure con driver ADO.NET hello.</span><span class="sxs-lookup"><span data-stu-id="40002-235">hello following code shows how tooregister hello Azure Key Vault provider with hello ADO.NET driver.</span></span>

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



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="40002-236">Applicazione console di esempio della crittografia sempre attiva</span><span class="sxs-lookup"><span data-stu-id="40002-236">Always Encrypted sample console application</span></span>
<span data-ttu-id="40002-237">Questo esempio dimostra come:</span><span class="sxs-lookup"><span data-stu-id="40002-237">This sample demonstrates how to:</span></span>

* <span data-ttu-id="40002-238">Modificare il tooenable di stringa di connessione Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="40002-238">Modify your connection string tooenable Always Encrypted.</span></span>
* <span data-ttu-id="40002-239">La registrazione insieme credenziali chiavi Azure hello provider dell'archivio chiavi dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="40002-239">Register Azure Key Vault as hello application's key store provider.</span></span>  
* <span data-ttu-id="40002-240">Inserire i dati in colonne crittografato hello.</span><span class="sxs-lookup"><span data-stu-id="40002-240">Insert data into hello encrypted columns.</span></span>
* <span data-ttu-id="40002-241">Selezionare un record filtrando in base a un valore specifico in una colonna crittografata.</span><span class="sxs-lookup"><span data-stu-id="40002-241">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="40002-242">Sostituire il contenuto di hello di **Program.cs** con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="40002-242">Replace hello contents of **Program.cs** with hello following code.</span></span> <span data-ttu-id="40002-243">Sostituire la stringa di connessione hello per la variabile globale connectionString hello nella riga hello che precede direttamente il metodo Main hello con la stringa di connessione valida da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="40002-243">Replace hello connection string for hello global connectionString variable in hello line that directly precedes hello Main method with your valid connection string from hello Azure portal.</span></span> <span data-ttu-id="40002-244">Si tratta di modifica di hello solo se è necessario codice toothis toomake.</span><span class="sxs-lookup"><span data-stu-id="40002-244">This is hello only change you need toomake toothis code.</span></span>

<span data-ttu-id="40002-245">Eseguire hello app toosee Always Encrypted in azione.</span><span class="sxs-lookup"><span data-stu-id="40002-245">Run hello app toosee Always Encrypted in action.</span></span>

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
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"<connection string from hello portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

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
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
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
                throw new InvalidOperationException("Failed tooobtain hello access token");
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



## <a name="verify-that-hello-data-is-encrypted"></a><span data-ttu-id="40002-246">Verificare che siano crittografati dati hello</span><span class="sxs-lookup"><span data-stu-id="40002-246">Verify that hello data is encrypted</span></span>
<span data-ttu-id="40002-247">È possibile controllare rapidamente che i dati effettivi di hello nel server di hello sono crittografati eseguendo una query su dati di pazienti hello con SQL Server Management Studio (tramite la connessione corrente in cui **Column Encryption Setting** non è ancora abilitato).</span><span class="sxs-lookup"><span data-stu-id="40002-247">You can quickly check that hello actual data on hello server is encrypted by querying hello Patients data with SSMS (using your current connection where **Column Encryption Setting** is not yet enabled).</span></span>

<span data-ttu-id="40002-248">Eseguire hello seguente query sul database Clinic hello.</span><span class="sxs-lookup"><span data-stu-id="40002-248">Run hello following query on hello Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="40002-249">È possibile vedere che le colonne crittografato hello non contengano i dati di testo normale.</span><span class="sxs-lookup"><span data-stu-id="40002-249">You can see that hello encrypted columns do not contain any plaintext data.</span></span>

   ![Nuova applicazione console](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

<span data-ttu-id="40002-251">toouse SSMS tooaccess hello dati in testo normale, è possibile aggiungere hello *Column Encryption Setting = abilitata* connessione toohello di parametro.</span><span class="sxs-lookup"><span data-stu-id="40002-251">toouse SSMS tooaccess hello plaintext data, you can add hello *Column Encryption Setting=enabled* parameter toohello connection.</span></span>

1. <span data-ttu-id="40002-252">In SSMS fare clic con il pulsante destro del mouse sul server in **Esplora oggetti** e scegliere **Disconnetti**.</span><span class="sxs-lookup"><span data-stu-id="40002-252">In SSMS, right-click your server in **Object Explorer** and choose **Disconnect**.</span></span>
2. <span data-ttu-id="40002-253">Fare clic su **Connetti** > **motore di Database** tooopen hello **connettersi tooServer** finestra e fare clic su **opzioni**.</span><span class="sxs-lookup"><span data-stu-id="40002-253">Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window and click **Options**.</span></span>
3. <span data-ttu-id="40002-254">Fare clic su **Parametri aggiuntivi per la connessione** e digitare **Column Encryption Setting=Enabled**.</span><span class="sxs-lookup"><span data-stu-id="40002-254">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Nuova applicazione console](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. <span data-ttu-id="40002-256">Eseguire hello seguente query sul database Clinic hello.</span><span class="sxs-lookup"><span data-stu-id="40002-256">Run hello following query on hello Clinic database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="40002-257">È ora possibile visualizzare dati in formato testo hello nelle colonne crittografato hello.</span><span class="sxs-lookup"><span data-stu-id="40002-257">You can now see hello plaintext data in hello encrypted columns.</span></span>

    ![Nuova applicazione console](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a><span data-ttu-id="40002-259">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="40002-259">Next steps</span></span>
<span data-ttu-id="40002-260">Dopo aver creato un database che Usa crittografia sempre attiva, è necessario seguente hello toodo:</span><span class="sxs-lookup"><span data-stu-id="40002-260">After you create a database that uses Always Encrypted, you may want toodo hello following:</span></span>

* <span data-ttu-id="40002-261">[Ruotare e pulire le chiavi](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="40002-261">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="40002-262">[Eseguire la migrazione dei dati già crittografati con la crittografia sempre attiva](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="40002-262">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>

## <a name="related-information"></a><span data-ttu-id="40002-263">Informazioni correlate</span><span class="sxs-lookup"><span data-stu-id="40002-263">Related information</span></span>
* [<span data-ttu-id="40002-264">Crittografia sempre attiva (sviluppo di client)</span><span class="sxs-lookup"><span data-stu-id="40002-264">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="40002-265">Transparent Data Encryption</span><span class="sxs-lookup"><span data-stu-id="40002-265">Transparent data encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="40002-266">Crittografia di SQL Server</span><span class="sxs-lookup"><span data-stu-id="40002-266">SQL Server encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="40002-267">Procedura guidata per la crittografia sempre attiva</span><span class="sxs-lookup"><span data-stu-id="40002-267">Always Encrypted wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="40002-268">Blog della crittografia sempre attiva</span><span class="sxs-lookup"><span data-stu-id="40002-268">Always Encrypted blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

