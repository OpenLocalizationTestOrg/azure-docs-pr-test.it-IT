---
title: 'Azure PowerShell: creare un database SQL | Microsoft Docs'
description: Informazioni su come toocreate un server logico di Database SQL regola del firewall a livello di server e database hello portale di Azure.
keywords: esercitazione sul database sql, creare un database sql
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: e89f68b44083a3b64e61f95117dbbedfa6647ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a><span data-ttu-id="12f35-104">Creare un singolo database SQL di Azure usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="12f35-104">Create a single Azure SQL database using PowerShell</span></span>

<span data-ttu-id="12f35-105">PowerShell viene utilizzato toocreate e gestire le risorse di Azure dalla riga di comando hello o negli script.</span><span class="sxs-lookup"><span data-stu-id="12f35-105">PowerShell is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="12f35-106">Un database SQL di Azure in questa Guida. dettagli utilizzando PowerShell toodeploy un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) in un [server logico di Database SQL di Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="12f35-106">This guide details using PowerShell toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="12f35-107">Se non si ha una sottoscrizione di Azure, creare un account [gratuito](https://azure.microsoft.com/free/) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="12f35-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

<span data-ttu-id="12f35-108">Questa esercitazione richiede hello Azure PowerShell versione 4.0 o versione successiva del modulo.</span><span class="sxs-lookup"><span data-stu-id="12f35-108">This tutorial requires hello Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="12f35-109">Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="12f35-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="12f35-110">Se è necessario tooinstall o l'aggiornamento, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="12f35-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="12f35-111">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="12f35-111">Log in tooAzure</span></span>

<span data-ttu-id="12f35-112">Accedi tooyour sottoscrizione di Azure utilizzando hello [Aggiungi AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) comando e seguire hello le direzioni.</span><span class="sxs-lookup"><span data-stu-id="12f35-112">Log in tooyour Azure subscription using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command and follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a><span data-ttu-id="12f35-113">Creare le variabili</span><span class="sxs-lookup"><span data-stu-id="12f35-113">Create variables</span></span>

<span data-ttu-id="12f35-114">Definire le variabili da usare negli script hello in questa Guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="12f35-114">Define variables for use in hello scripts in this quick start.</span></span>

```powershell
# hello data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# hello login information for hello server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# hello ip address range that you want tooallow tooaccess your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# hello database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="12f35-115">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="12f35-115">Create a resource group</span></span>

<span data-ttu-id="12f35-116">Creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) utilizzando hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) comando.</span><span class="sxs-lookup"><span data-stu-id="12f35-116">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="12f35-117">Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite come gruppo.</span><span class="sxs-lookup"><span data-stu-id="12f35-117">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="12f35-118">esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `westeurope` percorso.</span><span class="sxs-lookup"><span data-stu-id="12f35-118">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="12f35-119">Creare un server logico</span><span class="sxs-lookup"><span data-stu-id="12f35-119">Create a logical server</span></span>

<span data-ttu-id="12f35-120">Creare un [server logico di Database SQL di Azure](sql-database-features.md) utilizzando hello [New AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) comando.</span><span class="sxs-lookup"><span data-stu-id="12f35-120">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) command.</span></span> <span data-ttu-id="12f35-121">Un server logico contiene un gruppo di database gestiti come gruppo.</span><span class="sxs-lookup"><span data-stu-id="12f35-121">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="12f35-122">Hello seguente viene creato un server denominato in modo casuale nel gruppo di risorse con un account di accesso amministratore denominato `ServerAdmin` e la password `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="12f35-122">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="12f35-123">Sostituire questi valori predefiniti con quelli desiderati.</span><span class="sxs-lookup"><span data-stu-id="12f35-123">Replace these pre-defined values as desired.</span></span>

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="12f35-124">Configurare una regola del firewall del server</span><span class="sxs-lookup"><span data-stu-id="12f35-124">Configure a server firewall rule</span></span>

<span data-ttu-id="12f35-125">Creare un [regola del firewall a livello di server Database SQL di Azure](sql-database-firewall-configure.md) utilizzando hello [New AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) comando.</span><span class="sxs-lookup"><span data-stu-id="12f35-125">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) command.</span></span> <span data-ttu-id="12f35-126">Una regola del firewall a livello di server consente a un'applicazione esterna, ad esempio SQL Server Management Studio o hello SQLCMD utility tooconnect tooa database SQL tramite firewall del servizio Database SQL hello.</span><span class="sxs-lookup"><span data-stu-id="12f35-126">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="12f35-127">Nell'esempio seguente di hello, firewall hello è aperta solo per le altre risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="12f35-127">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="12f35-128">connettività esterna tooenable, modifica hello tooan appropriato indirizzo per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="12f35-128">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="12f35-129">tooopen tutti gli indirizzi IP, utilizzare 0.0.0.0 come hello avvio indirizzo IP e 255.255.255.255 come hello indirizzo finale.</span><span class="sxs-lookup"><span data-stu-id="12f35-129">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> <span data-ttu-id="12f35-130">Il database SQL comunica attraverso la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="12f35-130">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="12f35-131">Se si sta tentando di tooconnect da una rete aziendale, può non essere consentito il traffico in uscita sulla porta 1433 dal firewall della rete.</span><span class="sxs-lookup"><span data-stu-id="12f35-131">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="12f35-132">In questo caso, non sarà server di Database SQL di Azure in grado di tooconnect tooyour, a meno che il reparto IT consente di aprire la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="12f35-132">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="12f35-133">Creare un database in server hello con dati di esempio</span><span class="sxs-lookup"><span data-stu-id="12f35-133">Create a database in hello server with sample data</span></span>

<span data-ttu-id="12f35-134">Creare un database con un [livello di prestazioni S0](sql-database-service-tiers.md) nel server di hello tramite hello [New AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) comando.</span><span class="sxs-lookup"><span data-stu-id="12f35-134">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) command.</span></span> <span data-ttu-id="12f35-135">esempio Hello crea un database denominato `mySampleDatabase` e carica i dati di esempio AdventureWorksLT di hello in questo database.</span><span class="sxs-lookup"><span data-stu-id="12f35-135">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="12f35-136">Sostituire questi predefiniti i valori in base alle esigenze (altre guide introduttive in questa compilazione insieme ai valori hello in questa Guida introduttiva).</span><span class="sxs-lookup"><span data-stu-id="12f35-136">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a><span data-ttu-id="12f35-137">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="12f35-137">Clean up resources</span></span>

<span data-ttu-id="12f35-138">Altre guide introduttive di questa raccolta si basano sui valori di questa guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="12f35-138">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="12f35-139">Se si intende toocontinue toowork con avvio rapido successive, non pulire le risorse di hello create in questa Guida introduttiva avviato.</span><span class="sxs-lookup"><span data-stu-id="12f35-139">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="12f35-140">Se non si prevede toocontinue, utilizzare hello seguendo i passaggi toodelete tutte le risorse create da questa Guida introduttiva in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="12f35-140">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="12f35-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="12f35-141">Next steps</span></span>

<span data-ttu-id="12f35-142">Dopo aver creato un database, è possibile connettersi ed eseguire query usando gli strumenti preferiti.</span><span class="sxs-lookup"><span data-stu-id="12f35-142">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="12f35-143">Per altre informazioni, scegliere uno strumento di seguito:</span><span class="sxs-lookup"><span data-stu-id="12f35-143">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="12f35-144">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="12f35-144">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="12f35-145">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="12f35-145">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="12f35-146">.NET</span><span class="sxs-lookup"><span data-stu-id="12f35-146">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="12f35-147">PHP</span><span class="sxs-lookup"><span data-stu-id="12f35-147">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="12f35-148">Node.JS</span><span class="sxs-lookup"><span data-stu-id="12f35-148">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="12f35-149">Java</span><span class="sxs-lookup"><span data-stu-id="12f35-149">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="12f35-150">Python</span><span class="sxs-lookup"><span data-stu-id="12f35-150">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="12f35-151">Ruby</span><span class="sxs-lookup"><span data-stu-id="12f35-151">Ruby</span></span>](sql-database-connect-query-ruby.md)

