---
title: i processi di database elastico aaaInstalling | Documenti Microsoft
description: "Eseguire l'installazione della funzionalità processi elastico hello."
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
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="15394-103">Installazione dei processi di database elastici (panoramica)</span><span class="sxs-lookup"><span data-stu-id="15394-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="15394-104">[**I processi di Database elastici** ](sql-database-elastic-jobs-overview.md) può essere installato tramite PowerShell o tramite hello Portal.You classico di Azure potrà accedere a toocreate e gestire processi mediante l'API di PowerShell hello solo se si installa il pacchetto di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="15394-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through hello Azure Classic Portal.You can gain access toocreate and manage jobs using hello PowerShell API only if you install hello PowerShell package.</span></span> <span data-ttu-id="15394-105">Inoltre, hello APIs di PowerShell fornisce molte più funzionalità rispetto a portale hello in questo momento.</span><span class="sxs-lookup"><span data-stu-id="15394-105">Additionally, hello PowerShell APIs provide significantly more functionality than hello portal at this point in time.</span></span>

<span data-ttu-id="15394-106">Se è già stato installato **i processi di Database elastico** tramite hello portale da un oggetto esistente **pool elastico**, anteprima più recente di Powershell hello include script tooupgrade l'installazione esistente.</span><span class="sxs-lookup"><span data-stu-id="15394-106">If you have already installed **Elastic Database jobs** through hello Portal from an existing **elastic pool**, hello latest Powershell preview includes scripts tooupgrade your existing installation.</span></span> <span data-ttu-id="15394-107">È altamente consigliabile tooupgrade toohello l'installazione più recente **i processi di Database elastico** componenti vantaggio tootake ordine delle nuove funzionalità vengono esposte tramite hello APIs di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15394-107">It is highly recommended tooupgrade your installation toohello latest **Elastic Database jobs** components in order tootake advantage of new functionality exposed via hello PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15394-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="15394-108">Prerequisites</span></span>
* <span data-ttu-id="15394-109">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="15394-109">An Azure subscription.</span></span> <span data-ttu-id="15394-110">Per una versione di valutazione gratuita, vedere [Versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="15394-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="15394-111">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15394-111">Azure PowerShell.</span></span> <span data-ttu-id="15394-112">Installare hello utilizzando la versione più recente hello [installazione guidata piattaforma Web](http://go.microsoft.com/fwlink/p/?linkid=320376).</span><span class="sxs-lookup"><span data-stu-id="15394-112">Install hello latest version using hello [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="15394-113">Per informazioni dettagliate, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="15394-113">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="15394-114">[Utilità della riga di comando di NuGet](https://nuget.org/nuget.exe) è usato tooinstall hello Database elastico processi pacchetto.</span><span class="sxs-lookup"><span data-stu-id="15394-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used tooinstall hello Elastic Database jobs package.</span></span> <span data-ttu-id="15394-115">Per altre informazioni, vedere http://docs.nuget.org/docs/start-here/installing-nuget.</span><span class="sxs-lookup"><span data-stu-id="15394-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a><span data-ttu-id="15394-116">Scaricare e importare hello Database elastico processi PowerShell pacchetto</span><span class="sxs-lookup"><span data-stu-id="15394-116">Download and import hello Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="15394-117">Avviare la finestra di comando di Microsoft Azure PowerShell e passare toohello directory in cui è stato scaricato NuGet utilità della riga di comando (nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="15394-117">Launch Microsoft Azure PowerShell command window and navigate toohello directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="15394-118">Scaricare e importare **i processi di Database elastico** pacchetto nella directory corrente di hello con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="15394-118">Download and import **Elastic Database jobs** package into hello current directory with hello following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="15394-119">Hello **i processi di Database elastico** i file si trovano nella directory locale di hello in una cartella denominata **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** in *x.x.xxxx.x* riflette il numero di versione di hello.</span><span class="sxs-lookup"><span data-stu-id="15394-119">hello **Elastic Database jobs** files are placed in hello local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects hello version number.</span></span> <span data-ttu-id="15394-120">cmdlet di PowerShell Hello (inclusi DLL client richieste) si trovano in hello **tools\ElasticDatabaseJobs** sottodirectory hello tooinstall gli script di PowerShell, aggiornare e disinstallare anche si trovano in hello  **strumenti** sottodirectory.</span><span class="sxs-lookup"><span data-stu-id="15394-120">hello PowerShell cmdlets (including required client .dlls) are located in hello **tools\ElasticDatabaseJobs** sub-directory and hello PowerShell scripts tooinstall, upgrade and uninstall also reside in hello **tools** sub-directory.</span></span>
3. <span data-ttu-id="15394-121">Passare sottodirectory strumenti toohello nella cartella Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x hello digitando cd strumenti, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="15394-121">Navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="15394-122">Eseguire ElasticDatabaseJobs directory di hello.\InstallElasticDatabaseJobsCmdlets.ps1 script toocopy hello in $home\Documents\WindowsPowerShell\Modules.</span><span class="sxs-lookup"><span data-stu-id="15394-122">Execute hello .\InstallElasticDatabaseJobsCmdlets.ps1 script toocopy hello ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="15394-123">Verranno inoltre automaticamente importate modulo hello da utilizzare, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="15394-123">This will also automatically import hello module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="15394-124">Installare i componenti di processi di Database elastico hello utilizzando PowerShell</span><span class="sxs-lookup"><span data-stu-id="15394-124">Install hello Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="15394-125">Avviare una finestra di comando di Microsoft Azure PowerShell e passare sottodirectory \tools toohello nella cartella Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x hello: digitare cd \tools</span><span class="sxs-lookup"><span data-stu-id="15394-125">Launch a Microsoft Azure PowerShell command window and navigate toohello \tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="15394-126">Eseguire lo script di PowerShell.\InstallElasticDatabaseJobs.ps1 hello e fornire valori per le variabili di richieste.</span><span class="sxs-lookup"><span data-stu-id="15394-126">Execute hello .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="15394-127">Questo script crea componenti hello descritti in [componenti e sui prezzi dei processi di Database elastico](sql-database-elastic-jobs-overview.md#components-and-pricing) configurazione servizio Cloud di Azure hello tooappropriately fanno uso dei componenti dipendenti hello.</span><span class="sxs-lookup"><span data-stu-id="15394-127">This script will create hello components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring hello Azure Cloud Service tooappropriately use hello dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="15394-128">Quando si esegue questo comando, viene visualizzata una finestra in cui vengono richiesti **Nome utente** e **Password**.</span><span class="sxs-lookup"><span data-stu-id="15394-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="15394-129">Non si tratta le credenziali di Azure, immettere nome utente hello e una password che saranno le credenziali di amministratore hello da toocreate per nuovo server hello.</span><span class="sxs-lookup"><span data-stu-id="15394-129">This is not your Azure credentials, enter hello user name and password that will be hello administrator credentials you want toocreate for hello new server.</span></span>

<span data-ttu-id="15394-130">parametri di Hello forniti nella chiamata di questo esempio possono essere modificati per le impostazioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="15394-130">hello parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="15394-131">esempio Hello vengono fornite ulteriori informazioni sul comportamento di hello di ogni parametro:</span><span class="sxs-lookup"><span data-stu-id="15394-131">hello following provides more information on hello behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="15394-132">.</span><span class="sxs-lookup"><span data-stu-id="15394-132">Parameter</span></span></th>
    <th><span data-ttu-id="15394-133">Description</span><span class="sxs-lookup"><span data-stu-id="15394-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="15394-134">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="15394-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="15394-135">Fornisce nome gruppo di risorse di Azure hello creato hello toocontain nuovo componenti di Azure.</span><span class="sxs-lookup"><span data-stu-id="15394-135">Provides hello Azure resource group name created toocontain hello newly created Azure components.</span></span> <span data-ttu-id="15394-136">Per impostazione predefinita questo parametro troppo "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="15394-136">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="15394-137">Non è consigliabile toochange questo valore.</span><span class="sxs-lookup"><span data-stu-id="15394-137">It is not recommended toochange this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="15394-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="15394-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="15394-139">Fornisce hello Azure percorso toobe utilizzato per hello nuovo componenti di Azure.</span><span class="sxs-lookup"><span data-stu-id="15394-139">Provides hello Azure location toobe used for hello newly created Azure components.</span></span> <span data-ttu-id="15394-140">Questo parametro toohello posizione centrale USA per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="15394-140">This parameter defaults toohello Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="15394-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="15394-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="15394-142">Fornisce il numero di hello del servizio worker tooinstall.</span><span class="sxs-lookup"><span data-stu-id="15394-142">Provides hello number of service workers tooinstall.</span></span> <span data-ttu-id="15394-143">Questo parametro per impostazione predefinita too1.</span><span class="sxs-lookup"><span data-stu-id="15394-143">This parameter defaults too1.</span></span> <span data-ttu-id="15394-144">Un numero elevato di thread di lavoro può essere utilizzato tooscale out hello servizio e tooprovide la disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="15394-144">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span> <span data-ttu-id="15394-145">È consigliabile toouse "2" per le distribuzioni che richiedono la disponibilità elevata del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="15394-145">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="15394-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="15394-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="15394-147">Fornisce dimensioni delle macchine Virtuali hello per l'utilizzo della hello servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="15394-147">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="15394-148">Questo parametro per impostazione predefinita tooA0.</span><span class="sxs-lookup"><span data-stu-id="15394-148">This parameter defaults tooA0.</span></span> <span data-ttu-id="15394-149">Vengono accettati i valori di parametri di A3/A0/A1/A2, causando il lavoro hello ruolo toouse una dimensione molto piccola/piccole, medie e grandi, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="15394-149">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="15394-150">Per altre informazioni sulle dimensioni dei ruoli di lavoro, vedere [Componenti e prezzi dei processi di database elastici](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="15394-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="15394-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="15394-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="15394-152">Fornisce l'obiettivo del livello di servizio hello per un'edizione Standard.</span><span class="sxs-lookup"><span data-stu-id="15394-152">Provides hello service level objective for a Standard edition.</span></span> <span data-ttu-id="15394-153">Questo parametro per impostazione predefinita tooS0.</span><span class="sxs-lookup"><span data-stu-id="15394-153">This parameter defaults tooS0.</span></span> <span data-ttu-id="15394-154">Vengono accettati i valori dei parametri di S0/S1, S2 o S3 determinando hello Database SQL di Azure toouse hello rispettivo SLO.</span><span class="sxs-lookup"><span data-stu-id="15394-154">Parameter values of S0/S1/S2/S3 are accepted which cause hello Azure SQL Database toouse hello respective SLO.</span></span> <span data-ttu-id="15394-155">Per ulteriori informazioni sugli SLO del database SQL, vedere [Componenti e prezzi dei processi di database elastici](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="15394-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="15394-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="15394-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="15394-157">Fornisce il nome utente amministratore di hello per hello appena creati server di Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="15394-157">Provides hello admin user name for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="15394-158">Quando non viene specificato, è possibile che il tooprompt credenziali hello verrà aperta una finestra di PowerShell le credenziali.</span><span class="sxs-lookup"><span data-stu-id="15394-158">When not specified, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="15394-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="15394-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="15394-160">Fornisce la password di amministratore di hello per hello appena creati server di Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="15394-160">Provides hello admin password for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="15394-161">Quando non viene specificato, è possibile che il tooprompt credenziali hello verrà aperta una finestra di PowerShell le credenziali.</span><span class="sxs-lookup"><span data-stu-id="15394-161">When not provided, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="15394-162">Per i sistemi che con un numero elevato di processi in esecuzione in parallelo rispetto a un numero elevato di database di destinazione, è consigliabile, ad esempio parametri toospecify: ServiceWorkerCount - 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.</span><span class="sxs-lookup"><span data-stu-id="15394-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended toospecify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="15394-163">Aggiornare un'installazione dei componenti dei processi di database elastici esistente tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="15394-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="15394-164">**Processi di database elastici** possono essere aggiornati all'interno di un'installazione esistente per la scalabilità e la disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="15394-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="15394-165">Questo processo consente gli aggiornamenti futuri del codice di servizio senza dovere toodrop e ricreare il database di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="15394-165">This process allows for future upgrades of service code without having toodrop and recreate hello control database.</span></span> <span data-ttu-id="15394-166">Questo processo può inoltre essere utilizzato all'interno di hello stesso conteggio della versione toomodify hello servizio VM dimensioni o hello server worker.</span><span class="sxs-lookup"><span data-stu-id="15394-166">This process can also be used within hello same version toomodify hello service VM size or hello server worker count.</span></span>

<span data-ttu-id="15394-167">tooupdate hello dimensione della macchina virtuale un'installazione, hello eseguire lo script con parametri seguente toohello valori aggiornati delle prescelto.</span><span class="sxs-lookup"><span data-stu-id="15394-167">tooupdate hello VM size of an installation, run hello following script with parameters updated toohello values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="15394-168">.</span><span class="sxs-lookup"><span data-stu-id="15394-168">Parameter</span></span></th>
  <th><span data-ttu-id="15394-169">Description</span><span class="sxs-lookup"><span data-stu-id="15394-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="15394-170">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="15394-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="15394-171">Identifica nome gruppo di risorse di Azure hello utilizzato quando i componenti dei processi di Database elastico hello sono stati inizialmente installati.</span><span class="sxs-lookup"><span data-stu-id="15394-171">Identifies hello Azure resource group name used when hello Elastic Database job components were initially installed.</span></span> <span data-ttu-id="15394-172">Per impostazione predefinita questo parametro troppo "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="15394-172">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="15394-173">Perché non è consigliabile toochange questo valore, non dovrebbe essere toospecify questo parametro.</span><span class="sxs-lookup"><span data-stu-id="15394-173">Since it is not recommended toochange this value, you shouldn't have toospecify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="15394-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="15394-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="15394-175">Fornisce il numero di hello del servizio worker tooinstall.</span><span class="sxs-lookup"><span data-stu-id="15394-175">Provides hello number of service workers tooinstall.</span></span>  <span data-ttu-id="15394-176">Questo parametro per impostazione predefinita too1.</span><span class="sxs-lookup"><span data-stu-id="15394-176">This parameter defaults too1.</span></span>  <span data-ttu-id="15394-177">Un numero elevato di thread di lavoro può essere utilizzato tooscale out hello servizio e tooprovide la disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="15394-177">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span>  <span data-ttu-id="15394-178">È consigliabile toouse "2" per le distribuzioni che richiedono la disponibilità elevata del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="15394-178">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="15394-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="15394-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="15394-180">Fornisce dimensioni delle macchine Virtuali hello per l'utilizzo della hello servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="15394-180">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="15394-181">Questo parametro per impostazione predefinita tooA0.</span><span class="sxs-lookup"><span data-stu-id="15394-181">This parameter defaults tooA0.</span></span> <span data-ttu-id="15394-182">Vengono accettati i valori di parametri di A3/A0/A1/A2, causando il lavoro hello ruolo toouse una dimensione molto piccola/piccole, medie e grandi, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="15394-182">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="15394-183">Per altre informazioni sulle dimensioni dei ruoli di lavoro, vedere [Componenti e prezzi dei processi di database elastici](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="15394-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a><span data-ttu-id="15394-184">Installare i componenti di processi di Database elastico hello utilizzando hello portale</span><span class="sxs-lookup"><span data-stu-id="15394-184">Install hello Elastic Database jobs components using hello Portal</span></span>
<span data-ttu-id="15394-185">Dopo aver [creato un pool elastico](sql-database-elastic-pool-manage-portal.md), è possibile installare **i processi di Database elastico** esecuzione tooenable componenti delle attività amministrative in tutti i database nel pool elastico hello.</span><span class="sxs-lookup"><span data-stu-id="15394-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components tooenable execution of administrative tasks against each database in hello elastic pool.</span></span> <span data-ttu-id="15394-186">A differenza di quando utilizzare hello **i processi di Database elastico** APIs di PowerShell, interfaccia portale hello è attualmente soggetta a restrizioni tooonly per eseguire un pool esistente.</span><span class="sxs-lookup"><span data-stu-id="15394-186">Unlike when using hello **Elastic Database jobs** PowerShell APIs, hello portal interface is currently restricted tooonly executing against an existing pool.</span></span>

<span data-ttu-id="15394-187">**Toocomplete tempo stimato:** 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="15394-187">**Estimated time toocomplete:** 10 minutes.</span></span>

1. <span data-ttu-id="15394-188">Dalla visualizzazione dashboard hello del pool elastico di hello tramite hello [portale Azure](https://portal.azure.com/#) , fare clic su **processo di creazione**.</span><span class="sxs-lookup"><span data-stu-id="15394-188">From hello dashboard view of hello elastic pool via hello [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="15394-189">Se si sta creando un processo per hello prima volta, è necessario installare **i processi di Database elastico** facendo **condizioni per l'anteprima**.</span><span class="sxs-lookup"><span data-stu-id="15394-189">If you are creating a job for hello first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="15394-190">Accettare le condizioni di hello facendo hello casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="15394-190">Accept hello terms by clicking hello checkbox.</span></span>
4. <span data-ttu-id="15394-191">Nella visualizzazione hello "Installazione servizi", fare clic su **processo CREDENZIALI**.</span><span class="sxs-lookup"><span data-stu-id="15394-191">In hello "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![Installazione di servizi di hello][1]
5. <span data-ttu-id="15394-193">Digitare un nome utente e una password per un amministratore del database. Come parte dell'installazione di hello, viene creato un nuovo server di Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="15394-193">Type a user name and password for a database admin. As part of hello installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="15394-194">All'interno di questo nuovo server, un nuovo database, noto come database del controllo hello, viene creato e utilizzato i metadati di hello toocontain per i processi di Database elastico.</span><span class="sxs-lookup"><span data-stu-id="15394-194">Within this new server, a new database, known as hello control database, is created and used toocontain hello meta data for Elastic Database jobs.</span></span> <span data-ttu-id="15394-195">nome utente Hello e la password creati in questo caso vengono utilizzati a scopo di hello di registrazione nel database del controllo toohello.</span><span class="sxs-lookup"><span data-stu-id="15394-195">hello user name and password created here are used for hello purpose of logging in toohello control database.</span></span> <span data-ttu-id="15394-196">Una credenziale separata viene usata per l'esecuzione di script sul database hello pool hello.</span><span class="sxs-lookup"><span data-stu-id="15394-196">A separate credential is used for script execution against hello databases within hello pool.</span></span>
   
    ![Creare nome utente e password][2]
6. <span data-ttu-id="15394-198">Fare clic su pulsante OK hello.</span><span class="sxs-lookup"><span data-stu-id="15394-198">Click hello OK button.</span></span> <span data-ttu-id="15394-199">i componenti di Hello vengono creati automaticamente in pochi minuti in un nuovo [gruppo di risorse](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="15394-199">hello components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="15394-200">è stato aggiunto il nuovo gruppo di risorse Hello toohello avviare discussioni, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="15394-200">hello new resource group is pinned toohello start board, as shown below.</span></span> <span data-ttu-id="15394-201">Tutti i processi di database elastico, una volta create (servizio Cloud, Database SQL, Bus di servizio e archiviazione) vengono creati nel gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="15394-201">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in hello group.</span></span>
   
    ![gruppo di risorse nella schermata iniziale][3]
7. <span data-ttu-id="15394-203">Se si tenta di toocreate o gestire un processo durante l'installazione, i processi di database elastico quando si specifica **credenziali** hello seguente messaggio verrà visualizzato.</span><span class="sxs-lookup"><span data-stu-id="15394-203">If you attempt toocreate or manage a job while elastic database jobs is installing, when providing **Credentials** you will see hello following message.</span></span>
   
    ![Distribuzione ancora in corso][4]

<span data-ttu-id="15394-205">Se la disinstallazione è necessario, eliminare il gruppo di risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="15394-205">If uninstallation is required, delete hello resource group.</span></span> <span data-ttu-id="15394-206">Vedere [come toouninstall hello Database elastico processo componenti](sql-database-elastic-jobs-uninstall.md).</span><span class="sxs-lookup"><span data-stu-id="15394-206">See [How toouninstall hello Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="15394-207">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="15394-207">Next steps</span></span>
<span data-ttu-id="15394-208">Verificare che una credenziale con diritti di hello appropriati per l'esecuzione dello script viene creato in ogni database nel gruppo di hello, per ulteriori informazioni, vedere [la protezione del Database SQL](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="15394-208">Ensure a credential with hello appropriate rights for script execution is created on each database in hello group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="15394-209">Vedere [creazione e gestione dei processi di un Database elastico](sql-database-elastic-jobs-create-and-manage.md) tooget avviato.</span><span class="sxs-lookup"><span data-stu-id="15394-209">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) tooget started.</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
