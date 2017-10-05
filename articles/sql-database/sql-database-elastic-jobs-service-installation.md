---
title: Installazione dei processi di database elastici | Documentazione Microsoft
description: "Installazione dettagliata della funzionalità dei processi elastici."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: e7a2d6dbcefbb31d76257eaf96ccc235d7a29416
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="315cf-103">Installazione dei processi di database elastici (panoramica)</span><span class="sxs-lookup"><span data-stu-id="315cf-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="315cf-104">I [**Processi di database elastici**](sql-database-elastic-jobs-overview.md) possono essere installati tramite PowerShell o tramite il portale di Azure classico. È possibile ottenere l'accesso solo per creare e gestire processi utilizzando l'API PowerShell solo se si installa il pacchetto di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="315cf-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through the Azure Classic Portal.You can gain access to create and manage jobs using the PowerShell API only if you install the PowerShell package.</span></span> <span data-ttu-id="315cf-105">Inoltre, le API PowerShell forniscono molte più funzionalità rispetto al portale in questo momento.</span><span class="sxs-lookup"><span data-stu-id="315cf-105">Additionally, the PowerShell APIs provide significantly more functionality than the portal at this point in time.</span></span>

<span data-ttu-id="315cf-106">Se sono già stati installati i **processi di database elastici** tramite il portale da un **pool elastico**, l'ultima anteprima di Powershell include gli script per aggiornare l'installazione esistente.</span><span class="sxs-lookup"><span data-stu-id="315cf-106">If you have already installed **Elastic Database jobs** through the Portal from an existing **elastic pool**, the latest Powershell preview includes scripts to upgrade your existing installation.</span></span> <span data-ttu-id="315cf-107">È consigliabile aggiornare l'installazione alla versione più recente dei componenti dei **Processi di database elastici** per trarre vantaggio dalle nuove funzionalità esposte tramite le API di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="315cf-107">It is highly recommended to upgrade your installation to the latest **Elastic Database jobs** components in order to take advantage of new functionality exposed via the PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="315cf-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="315cf-108">Prerequisites</span></span>
* <span data-ttu-id="315cf-109">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="315cf-109">An Azure subscription.</span></span> <span data-ttu-id="315cf-110">Per una versione di valutazione gratuita, vedere [Versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="315cf-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="315cf-111">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="315cf-111">Azure PowerShell.</span></span> <span data-ttu-id="315cf-112">Installare la versione più recente tramite l’ [installazione guidata piattaforma Web](http://go.microsoft.com/fwlink/p/?linkid=320376).</span><span class="sxs-lookup"><span data-stu-id="315cf-112">Install the latest version using the [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="315cf-113">Per informazioni dettagliate, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="315cf-113">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="315cf-114">[Utilità della riga di comando NuGet](https://nuget.org/nuget.exe) viene utilizzata per installare il pacchetto dei processi di database elastici.</span><span class="sxs-lookup"><span data-stu-id="315cf-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used to install the Elastic Database jobs package.</span></span> <span data-ttu-id="315cf-115">Per altre informazioni, vedere http://docs.nuget.org/docs/start-here/installing-nuget.</span><span class="sxs-lookup"><span data-stu-id="315cf-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-the-elastic-database-jobs-powershell-package"></a><span data-ttu-id="315cf-116">Scaricare e importare il pacchetto di PowerShell dei processi di database elastici</span><span class="sxs-lookup"><span data-stu-id="315cf-116">Download and import the Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="315cf-117">Avviare la finestra di comando Microsoft Azure PowerShell e passare alla directory in cui è stato scaricata l’utilità della riga di comando NuGet (nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="315cf-117">Launch Microsoft Azure PowerShell command window and navigate to the directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="315cf-118">Scaricare e importare il pacchetto **Processi di database elastici** nella directory corrente con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="315cf-118">Download and import **Elastic Database jobs** package into the current directory with the following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="315cf-119">I file **Processi di database elastici**vengono inseriti in una directory locale in una cartella denominata **Microsoft.Azure.SqlDatabase.Processi.x.x.xxxx.x** dove *x.x.xxxx.x* rappresenta il numero di versione.</span><span class="sxs-lookup"><span data-stu-id="315cf-119">The **Elastic Database jobs** files are placed in the local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects the version number.</span></span> <span data-ttu-id="315cf-120">I cmdlet di PowerShell (inclusi i client .dlls richiesti) si trovano nella sottodirectory **Strumenti\ProcessiDatabaseElastici** e gli script di PowerShell per installare, aggiornare e disinstallare si trovano anch’essi nella sottodirectory **Strumenti**.</span><span class="sxs-lookup"><span data-stu-id="315cf-120">The PowerShell cmdlets (including required client .dlls) are located in the **tools\ElasticDatabaseJobs** sub-directory and the PowerShell scripts to install, upgrade and uninstall also reside in the **tools** sub-directory.</span></span>
3. <span data-ttu-id="315cf-121">Passare alla sottodirectory strumenti sotto la cartella Microsoft.Azure.SqlDatabase.Processi.x.x.xxx.x digitando strumenti cd, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="315cf-121">Navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="315cf-122">Eseguire lo script .\InstallElasticDatabaseJobsCmdlets.ps1 per copiare la directory ProcessiDatabaseElastici in $home\Documenti\WindowsPowerShell\Moduli.</span><span class="sxs-lookup"><span data-stu-id="315cf-122">Execute the .\InstallElasticDatabaseJobsCmdlets.ps1 script to copy the ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="315cf-123">Il modulo da utilizzare, verrà automaticamente importato, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="315cf-123">This will also automatically import the module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-the-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="315cf-124">Installare i componenti dei processi di database elastici utilizzando PowerShell</span><span class="sxs-lookup"><span data-stu-id="315cf-124">Install the Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="315cf-125">Avviare una finestra di comando di Microsoft Azure PowerShell e passare alla \sottodirectory strumenti sotto la cartella Microsoft.Azure.SqlDatabase.Processi.x.x.xxx.x: digitare cd\strumenti</span><span class="sxs-lookup"><span data-stu-id="315cf-125">Launch a Microsoft Azure PowerShell command window and navigate to the \tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="315cf-126">Eseguire lo script PowerShell .\InstallElasticDatabaseJobs.ps1 e fornire valori per le variabili richieste.</span><span class="sxs-lookup"><span data-stu-id="315cf-126">Execute the .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="315cf-127">Questo script crea i componenti descritti in [Componenti e prezzi dei processi di database elastici](sql-database-elastic-jobs-overview.md#components-and-pricing) con la configurazione del servizio Cloud di Azure per utilizzare correttamente i componenti dipendenti.</span><span class="sxs-lookup"><span data-stu-id="315cf-127">This script will create the components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring the Azure Cloud Service to appropriately use the dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="315cf-128">Quando si esegue questo comando, viene visualizzata una finestra in cui vengono richiesti **Nome utente** e **Password**.</span><span class="sxs-lookup"><span data-stu-id="315cf-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="315cf-129">Non si tratta delle credenziali di Azure. Immettere il nome utente e password che saranno le credenziali di amministratore che si desidera creare per il nuovo server.</span><span class="sxs-lookup"><span data-stu-id="315cf-129">This is not your Azure credentials, enter the user name and password that will be the administrator credentials you want to create for the new server.</span></span>

<span data-ttu-id="315cf-130">I parametri forniti in questa chiamata di esempio possono essere modificati per le impostazioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="315cf-130">The parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="315cf-131">Di seguito vengono fornite ulteriori informazioni sul comportamento di ciascun parametro:</span><span class="sxs-lookup"><span data-stu-id="315cf-131">The following provides more information on the behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="315cf-132">Parametro</span><span class="sxs-lookup"><span data-stu-id="315cf-132">Parameter</span></span></th>
    <th><span data-ttu-id="315cf-133">Description</span><span class="sxs-lookup"><span data-stu-id="315cf-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="315cf-134">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="315cf-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="315cf-135">Fornisce il nome del gruppo di risorse di Azure creato per contenere i componenti di Azure appena creati.</span><span class="sxs-lookup"><span data-stu-id="315cf-135">Provides the Azure resource group name created to contain the newly created Azure components.</span></span> <span data-ttu-id="315cf-136">Questo parametro viene impostato su "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="315cf-136">This parameter defaults to “__ElasticDatabaseJob”.</span></span> <span data-ttu-id="315cf-137">È consigliabile non modificare questo valore.</span><span class="sxs-lookup"><span data-stu-id="315cf-137">It is not recommended to change this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="315cf-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="315cf-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="315cf-139">Fornisce la posizione di Azure da utilizzare per i componenti di Azure appena creati.</span><span class="sxs-lookup"><span data-stu-id="315cf-139">Provides the Azure location to be used for the newly created Azure components.</span></span> <span data-ttu-id="315cf-140">Questo parametro viene impostato per il percorso Stati Uniti centrali.</span><span class="sxs-lookup"><span data-stu-id="315cf-140">This parameter defaults to the Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="315cf-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="315cf-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="315cf-142">Fornisce il numero di ruoli di lavoro del servizio da installare.</span><span class="sxs-lookup"><span data-stu-id="315cf-142">Provides the number of service workers to install.</span></span> <span data-ttu-id="315cf-143">Questo parametro viene impostato su 1.</span><span class="sxs-lookup"><span data-stu-id="315cf-143">This parameter defaults to 1.</span></span> <span data-ttu-id="315cf-144">Per ridimensionare il servizio e per garantire un'elevata disponibilità, è possibile utilizzare un numero maggiore di ruoli di lavoro.</span><span class="sxs-lookup"><span data-stu-id="315cf-144">A higher number of workers can be used to scale out the service and to provide high availability.</span></span> <span data-ttu-id="315cf-145">È consigliabile utilizzare "2" per le distribuzioni che richiedono un'elevata disponibilità del servizio.</span><span class="sxs-lookup"><span data-stu-id="315cf-145">It is recommended to use “2” for deployments that require high availability of the service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="315cf-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="315cf-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="315cf-147">Fornisce le dimensioni della macchina virtuale per l'utilizzo all'interno del servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="315cf-147">Provides the VM size for usage within the Cloud Service.</span></span> <span data-ttu-id="315cf-148">Questo parametro viene impostato su A0.</span><span class="sxs-lookup"><span data-stu-id="315cf-148">This parameter defaults to A0.</span></span> <span data-ttu-id="315cf-149">Sono accettati valori di parametri di A0/A1/A2/A3 che fanno si che il ruolo di lavoro utilizzi una dimensione Extrapiccola/Piccola/Media/Grande, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="315cf-149">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="315cf-150">Per altre informazioni sulle dimensioni dei ruoli di lavoro, vedere [Componenti e prezzi dei processi di database elastici](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="315cf-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="315cf-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="315cf-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="315cf-152">Fornisce l'obiettivo del livello di servizio per un'edizione Standard.</span><span class="sxs-lookup"><span data-stu-id="315cf-152">Provides the service level objective for a Standard edition.</span></span> <span data-ttu-id="315cf-153">Questo parametro viene impostato su S0.</span><span class="sxs-lookup"><span data-stu-id="315cf-153">This parameter defaults to S0.</span></span> <span data-ttu-id="315cf-154">Sono accettati i valori dei parametri S0/S1/S2/S3 che fanno si che il Database SQL di Azure utilizzi il rispettivo SLO.</span><span class="sxs-lookup"><span data-stu-id="315cf-154">Parameter values of S0/S1/S2/S3 are accepted which cause the Azure SQL Database to use the respective SLO.</span></span> <span data-ttu-id="315cf-155">Per ulteriori informazioni sugli SLO del database SQL, vedere [Componenti e prezzi dei processi di database elastici](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="315cf-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="315cf-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="315cf-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="315cf-157">Fornisce il nome utente dell’amministratore per il server del Database SQL di Azure appena creato.</span><span class="sxs-lookup"><span data-stu-id="315cf-157">Provides the admin user name for the newly created Azure SQL Database server.</span></span> <span data-ttu-id="315cf-158">Se omesso, si aprirà una finestra di credenziali di PowerShell per la richiesta di credenziali.</span><span class="sxs-lookup"><span data-stu-id="315cf-158">When not specified, a PowerShell credentials window will open to prompt for the credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="315cf-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="315cf-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="315cf-160">Fornisce la password dell’amministratore per il server del Database SQL di Azure appena creato.</span><span class="sxs-lookup"><span data-stu-id="315cf-160">Provides the admin password for the newly created Azure SQL Database server.</span></span> <span data-ttu-id="315cf-161">Se omesso, si aprirà una finestra di credenziali di PowerShell per richiedere le credenziali.</span><span class="sxs-lookup"><span data-stu-id="315cf-161">When not provided, a PowerShell credentials window will open to prompt for the credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="315cf-162">Per i sistemi che mirano ad avere un numero elevato di processi in esecuzione in parallelo su un numero elevato di database, si consiglia di specificare  parametri come ad esempio: ServiceWorkerCount - 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.</span><span class="sxs-lookup"><span data-stu-id="315cf-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended to specify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="315cf-163">Aggiornare un'installazione dei componenti dei processi di database elastici esistente tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="315cf-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="315cf-164">**Processi di database elastici** possono essere aggiornati all'interno di un'installazione esistente per la scalabilità e la disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="315cf-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="315cf-165">Questo processo consente aggiornamenti futuri del codice del servizio senza dover eliminare e ricreare il database di controllo.</span><span class="sxs-lookup"><span data-stu-id="315cf-165">This process allows for future upgrades of service code without having to drop and recreate the control database.</span></span> <span data-ttu-id="315cf-166">Questo processo può anche essere utilizzato all'interno della stessa versione per modificare la dimensione della macchina virtuale di servizio o il numero del ruolo di lavoro del server.</span><span class="sxs-lookup"><span data-stu-id="315cf-166">This process can also be used within the same version to modify the service VM size or the server worker count.</span></span>

<span data-ttu-id="315cf-167">Per aggiornare la dimensione della macchina virtuale di un'installazione, eseguire lo script seguente con i parametri aggiornati ai valori di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="315cf-167">To update the VM size of an installation, run the following script with parameters updated to the values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="315cf-168">Parametro</span><span class="sxs-lookup"><span data-stu-id="315cf-168">Parameter</span></span></th>
  <th><span data-ttu-id="315cf-169">Description</span><span class="sxs-lookup"><span data-stu-id="315cf-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="315cf-170">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="315cf-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="315cf-171">Identifica il nome del gruppo di risorse di Azure utilizzato quando i componenti dei processi di database elastici sono stati inizialmente installati.</span><span class="sxs-lookup"><span data-stu-id="315cf-171">Identifies the Azure resource group name used when the Elastic Database job components were initially installed.</span></span> <span data-ttu-id="315cf-172">Questo parametro viene impostato su "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="315cf-172">This parameter defaults to “__ElasticDatabaseJob”.</span></span> <span data-ttu-id="315cf-173">Poiché non è consigliabile modificare questo valore, non è necessario specificare questo parametro.</span><span class="sxs-lookup"><span data-stu-id="315cf-173">Since it is not recommended to change this value, you shouldn't have to specify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="315cf-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="315cf-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="315cf-175">Fornisce il numero di ruoli di lavoro del servizio da installare.</span><span class="sxs-lookup"><span data-stu-id="315cf-175">Provides the number of service workers to install.</span></span>  <span data-ttu-id="315cf-176">Questo parametro viene impostato su 1.</span><span class="sxs-lookup"><span data-stu-id="315cf-176">This parameter defaults to 1.</span></span>  <span data-ttu-id="315cf-177">Per ridimensionare il servizio e per garantire un'elevata disponibilità, è possibile utilizzare un numero maggiore di ruoli di lavoro.</span><span class="sxs-lookup"><span data-stu-id="315cf-177">A higher number of workers can be used to scale out the service and to provide high availability.</span></span>  <span data-ttu-id="315cf-178">È consigliabile utilizzare "2" per le distribuzioni che richiedono un'elevata disponibilità del servizio.</span><span class="sxs-lookup"><span data-stu-id="315cf-178">It is recommended to use “2” for deployments that require high availability of the service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="315cf-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="315cf-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="315cf-180">Fornisce le dimensioni della macchina virtuale per l'utilizzo all'interno del servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="315cf-180">Provides the VM size for usage within the Cloud Service.</span></span> <span data-ttu-id="315cf-181">Questo parametro viene impostato su A0.</span><span class="sxs-lookup"><span data-stu-id="315cf-181">This parameter defaults to A0.</span></span> <span data-ttu-id="315cf-182">Sono accettati valori di parametri di A0/A1/A2/A3 che fanno si che il ruolo di lavoro utilizzi una dimensione Extrapiccola/Piccola/Media/Grande, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="315cf-182">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="315cf-183">Per altre informazioni sulle dimensioni dei ruoli di lavoro, vedere [Componenti e prezzi dei processi di database elastici](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="315cf-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-the-elastic-database-jobs-components-using-the-portal"></a><span data-ttu-id="315cf-184">Installare i componenti dei processi di database elastici utilizzando il portale</span><span class="sxs-lookup"><span data-stu-id="315cf-184">Install the Elastic Database jobs components using the Portal</span></span>
<span data-ttu-id="315cf-185">Dopo aver creato un [pool elastico](sql-database-elastic-pool-manage-portal.md), è possibile installare componenti dei **processi di database elastici** per abilitare l'esecuzione di attività amministrative su ogni database nel pool elastico.</span><span class="sxs-lookup"><span data-stu-id="315cf-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components to enable execution of administrative tasks against each database in the elastic pool.</span></span> <span data-ttu-id="315cf-186">A differenza di quando si utilizzano le API PowerShell dei **processi di database elastici** , l'interfaccia del portale è attualmente limitata solamente all’esecuzione su un pool esistente.</span><span class="sxs-lookup"><span data-stu-id="315cf-186">Unlike when using the **Elastic Database jobs** PowerShell APIs, the portal interface is currently restricted to only executing against an existing pool.</span></span>

<span data-ttu-id="315cf-187">**Tempo previsto per il completamento:** 10 minuti</span><span class="sxs-lookup"><span data-stu-id="315cf-187">**Estimated time to complete:** 10 minutes.</span></span>

1. <span data-ttu-id="315cf-188">Nella vista dashboard del pool elastico, tramite il [portale di Azure](https://portal.azure.com/#) fare clic su **Crea processo**.</span><span class="sxs-lookup"><span data-stu-id="315cf-188">From the dashboard view of the elastic pool via the [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="315cf-189">Se si sta creando un processo per la prima volta, è necessario installare **processi di database elastici** facendo clic su **ANTEPRIMA TERMINI**.</span><span class="sxs-lookup"><span data-stu-id="315cf-189">If you are creating a job for the first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="315cf-190">Accettare i termini selezionando la casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="315cf-190">Accept the terms by clicking the checkbox.</span></span>
4. <span data-ttu-id="315cf-191">Nella vista "Installa servizi", fare clic su **CREDENZIALI PROCESSO**.</span><span class="sxs-lookup"><span data-stu-id="315cf-191">In the "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![Installazione dei servizi][1]
5. <span data-ttu-id="315cf-193">Digitare un nome utente e una password per un amministratore del database.</span><span class="sxs-lookup"><span data-stu-id="315cf-193">Type a user name and password for a database admin.</span></span> <span data-ttu-id="315cf-194">Come parte dell'installazione, viene creato un nuovo server di database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="315cf-194">As part of the installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="315cf-195">All'interno di questo nuovo server, viene creato un nuovo database, noto come database di controllo, che viene utilizzato per contenere i metadati per i processi di database elastici.</span><span class="sxs-lookup"><span data-stu-id="315cf-195">Within this new server, a new database, known as the control database, is created and used to contain the meta data for Elastic Database jobs.</span></span> <span data-ttu-id="315cf-196">Il nome utente e la password creati in questo caso vengono utilizzati per l'accesso al database di controllo.</span><span class="sxs-lookup"><span data-stu-id="315cf-196">The user name and password created here are used for the purpose of logging in to the control database.</span></span> <span data-ttu-id="315cf-197">Una credenziale separata viene utilizzata per l'esecuzione di script sui database all'interno del pool.</span><span class="sxs-lookup"><span data-stu-id="315cf-197">A separate credential is used for script execution against the databases within the pool.</span></span>
   
    ![Creare nome utente e password][2]
6. <span data-ttu-id="315cf-199">Fare clic sul pulsante OK.</span><span class="sxs-lookup"><span data-stu-id="315cf-199">Click the OK button.</span></span> <span data-ttu-id="315cf-200">I componenti vengono creati automaticamente in pochi minuti in un nuovo [gruppo di risorse](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="315cf-200">The components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="315cf-201">Il nuovo gruppo di risorse viene bloccato sulla schermata iniziale, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="315cf-201">The new resource group is pinned to the start board, as shown below.</span></span> <span data-ttu-id="315cf-202">Una volta creati, i processi di database elastici (Servizio cloud, database SQL, Bus di servizio e Archiviazione) vengono creati tutti nel gruppo.</span><span class="sxs-lookup"><span data-stu-id="315cf-202">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in the group.</span></span>
   
    ![gruppo di risorse nella schermata iniziale][3]
7. <span data-ttu-id="315cf-204">Se si tenta di creare o gestire un processo mentre si installano i processi di database elastici, nel momento in cui vengono fornite le **credenziali** verrà visualizzato il messaggio seguente.</span><span class="sxs-lookup"><span data-stu-id="315cf-204">If you attempt to create or manage a job while elastic database jobs is installing, when providing **Credentials** you will see the following message.</span></span>
   
    ![Distribuzione ancora in corso][4]

<span data-ttu-id="315cf-206">Se è necessaria la disinstallazione, eliminare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="315cf-206">If uninstallation is required, delete the resource group.</span></span> <span data-ttu-id="315cf-207">Vedere [Come disinstallare i componenti dei processi di database elastici](sql-database-elastic-jobs-uninstall.md).</span><span class="sxs-lookup"><span data-stu-id="315cf-207">See [How to uninstall the Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="315cf-208">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="315cf-208">Next steps</span></span>
<span data-ttu-id="315cf-209">Assicurarsi che una credenziale con i diritti appropriati per l'esecuzione di script venga creata in ogni database nel gruppo e vedere [Protezione del Database SQL](sql-database-manage-logins.md)per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="315cf-209">Ensure a credential with the appropriate rights for script execution is created on each database in the group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="315cf-210">Per un’introduzione, vedere [Creazione e gestione di processi di database elastici](sql-database-elastic-jobs-create-and-manage.md) .</span><span class="sxs-lookup"><span data-stu-id="315cf-210">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) to get started.</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
