---
title: aaaCreate e gestire processi elastici mediante PowerShell | Documenti Microsoft
description: Utilizzare PowerShell per il pool di Database SQL di Azure toomanage
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="f366e-103">Creare e gestire processi elastici del database SQL con PowerShell (anteprima)</span><span class="sxs-lookup"><span data-stu-id="f366e-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="f366e-104">Hello APIs di PowerShell per **i processi di Database elastico** (in anteprima), consentono di definire un gruppo di database sul quale script verranno eseguiti.</span><span class="sxs-lookup"><span data-stu-id="f366e-104">hello PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="f366e-105">Questo articolo viene illustrato come toocreate e gestire **i processi di Database elastico** utilizzando i cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f366e-105">This article shows how toocreate and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="f366e-106">Vedere [Panoramica dei processi di database elastici](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f366e-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f366e-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f366e-107">Prerequisites</span></span>
* <span data-ttu-id="f366e-108">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f366e-108">An Azure subscription.</span></span> <span data-ttu-id="f366e-109">Per una versione di valutazione gratuita, vedere [Versione di valutazione gratuita di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f366e-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f366e-110">Un set di database creati con gli strumenti di Database elastico hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-110">A set of databases created with hello Elastic Database tools.</span></span> <span data-ttu-id="f366e-111">Vedere [Iniziare a usare gli strumenti di database elastici](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f366e-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="f366e-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f366e-112">Azure PowerShell.</span></span> <span data-ttu-id="f366e-113">Per informazioni dettagliate, vedere [come tooinstall e configurare Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f366e-113">For detailed information, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="f366e-114">**processi di database elastici** di PowerShell, vedere [Installing processi di database elastici](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="f366e-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="f366e-115">Selezionare la sottoscrizione ad Azure</span><span class="sxs-lookup"><span data-stu-id="f366e-115">Select your Azure subscription</span></span>
<span data-ttu-id="f366e-116">sottoscrizione di hello tooselect è necessario l'Id sottoscrizione (**- SubscriptionId**) o nome della sottoscrizione (**- SubscriptionName**).</span><span class="sxs-lookup"><span data-stu-id="f366e-116">tooselect hello subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="f366e-117">Se si dispone di più sottoscrizioni, è possibile eseguire hello **Get AzureRmSubscription** hello cmdlet e copia desiderato informazioni sulla sottoscrizione dal set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-117">If you have multiple subscriptions you can run hello **Get-AzureRmSubscription** cmdlet and copy hello desired subscription information from hello result set.</span></span> <span data-ttu-id="f366e-118">Dopo aver creato le informazioni di sottoscrizione, eseguire hello seguente cmdlet tooset questa sottoscrizione come valore predefinito di hello, vale a dire hello destinazione per la creazione e la gestione dei processi:</span><span class="sxs-lookup"><span data-stu-id="f366e-118">Once you have your subscription information, run hello following commandlet tooset this subscription as hello default, namely hello target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="f366e-119">Hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) è consigliato per l'utilizzo toodevelop ed eseguire gli script di PowerShell in processi di Database elastico hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-119">hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage toodevelop and execute PowerShell scripts against hello Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="f366e-120">Oggetti dei processi di database elastici</span><span class="sxs-lookup"><span data-stu-id="f366e-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="f366e-121">Hello seguente tabella vengono elencati tutti i tipi di oggetto hello di **i processi di Database elastico** con la descrizione e APIs PowerShell rilevanti.</span><span class="sxs-lookup"><span data-stu-id="f366e-121">hello following table lists out all hello object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="f366e-122">Tipo di oggetto</span><span class="sxs-lookup"><span data-stu-id="f366e-122">Object Type</span></span></th>
    <th><span data-ttu-id="f366e-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f366e-123">Description</span></span></th>
    <th><span data-ttu-id="f366e-124">API correlate di PowerShell</span><span class="sxs-lookup"><span data-stu-id="f366e-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="f366e-125">Credenziali</span><span class="sxs-lookup"><span data-stu-id="f366e-125">Credential</span></span></td>
    <td><span data-ttu-id="f366e-126">Nome utente e password toouse quando ci si connette toodatabases per l'esecuzione di script o applicazione del file dacpac.</span><span class="sxs-lookup"><span data-stu-id="f366e-126">Username and password toouse when connecting toodatabases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="f366e-127">password Hello viene crittografata prima dell'invio tooand archiviato nel database di processi di Database elastico hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-127">hello password is encrypted before sending tooand storing in hello Elastic Database Jobs database.</span></span>  <span data-ttu-id="f366e-128">password Hello viene decrittografata dal servizio processi di Database elastico tramite credenziali hello creato e caricato da uno script di installazione di hello hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-128">hello password is decrypted by hello Elastic Database Jobs service via hello credential created and uploaded from hello installation script.</span></span></td>
    <td><p><span data-ttu-id="f366e-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="f366e-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="f366e-130">New-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="f366e-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="f366e-131">Set-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="f366e-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="f366e-132">Script</span><span class="sxs-lookup"><span data-stu-id="f366e-132">Script</span></span></td>
    <td><span data-ttu-id="f366e-133">Toobe di script Transact-SQL utilizzato per l'esecuzione tra i database.</span><span class="sxs-lookup"><span data-stu-id="f366e-133">Transact-SQL script toobe used for execution across databases.</span></span>  <span data-ttu-id="f366e-134">script Hello dovrebbe essere idempotente toobe creati in quanto hello verrà ritentata l'esecuzione dello script hello al momento di errori.</span><span class="sxs-lookup"><span data-stu-id="f366e-134">hello script should be authored toobe idempotent since hello service will retry execution of hello script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="f366e-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="f366e-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="f366e-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="f366e-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="f366e-137">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="f366e-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="f366e-138">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="f366e-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="f366e-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="f366e-139">DACPAC</span></span></td>
    <td><span data-ttu-id="f366e-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Applicazione livello dati </a> toobe applicate ai database del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f366e-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package toobe applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="f366e-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="f366e-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="f366e-142">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="f366e-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="f366e-143">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="f366e-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="f366e-144">Destinazione del database</span><span class="sxs-lookup"><span data-stu-id="f366e-144">Database Target</span></span></td>
    <td><span data-ttu-id="f366e-145">Server e database nome puntamento tooan Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="f366e-145">Database and server name pointing tooan Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="f366e-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="f366e-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="f366e-147">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="f366e-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="f366e-148">Destinazione di partizionamento della mappa</span><span class="sxs-lookup"><span data-stu-id="f366e-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="f366e-149">Combinazione di un database di destinazione e una credenziale toobe ha usato informazioni toodetermine archiviate all'interno di una mappa partizioni di Database elastico.</span><span class="sxs-lookup"><span data-stu-id="f366e-149">Combination of a database target and a credential toobe used toodetermine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="f366e-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="f366e-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="f366e-151">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="f366e-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="f366e-152">Set-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="f366e-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="f366e-153">Destinazione di una raccolta personalizzata</span><span class="sxs-lookup"><span data-stu-id="f366e-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="f366e-154">Gruppo definito di toocollectively database utilizzare per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f366e-154">Defined group of databases toocollectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="f366e-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="f366e-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="f366e-156">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="f366e-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="f366e-157">Destinazione figlio di una raccolta personalizzata</span><span class="sxs-lookup"><span data-stu-id="f366e-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="f366e-158">Destinazione di database a cui fa riferimento una raccolta personalizzata.</span><span class="sxs-lookup"><span data-stu-id="f366e-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="f366e-159">Add-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="f366e-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="f366e-160">Remove-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="f366e-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="f366e-161">Job</span><span class="sxs-lookup"><span data-stu-id="f366e-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="f366e-162">Definizione dei parametri per un processo che può essere utilizzato tootrigger esecuzione o toofulfill una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="f366e-162">Definition of parameters for a job that can be used tootrigger execution or toofulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="f366e-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="f366e-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="f366e-164">New-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="f366e-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="f366e-165">Set-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="f366e-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="f366e-166">Esecuzione del processo</span><span class="sxs-lookup"><span data-stu-id="f366e-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="f366e-167">Contenitore di attività toofulfill necessario eseguire uno script o l'applicazione di una destinazione tooa DACPAC utilizzando le credenziali per le connessioni di database a causa di errori gestiti in Criteri di conformità tooan esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f366e-167">Container of tasks necessary toofulfill either executing a script or applying a DACPAC tooa target using credentials for database connections with failures handled in accordance tooan execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="f366e-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="f366e-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="f366e-169">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="f366e-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="f366e-170">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="f366e-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="f366e-171">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="f366e-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="f366e-172">Esecuzione dell'attività di processo</span><span class="sxs-lookup"><span data-stu-id="f366e-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="f366e-173">Singola unità di lavoro toofulfill un processo.</span><span class="sxs-lookup"><span data-stu-id="f366e-173">Single unit of work toofulfill a job.</span></span></p>
    <p><span data-ttu-id="f366e-174">Se un'attività di processo non è in grado di toosuccessfully execute, verrà registrato il messaggio di eccezione risultante hello e una nuova attività di processo corrispondente verrà creata ed eseguite in base toohello specificato criteri di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f366e-174">If a job task is not able toosuccessfully execute, hello resulting exception message will be logged and a new matching job task will be created and executed in accordance toohello specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="f366e-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="f366e-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="f366e-176">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="f366e-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="f366e-177">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="f366e-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="f366e-178">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="f366e-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="f366e-179">Criterio di esecuzione del processo</span><span class="sxs-lookup"><span data-stu-id="f366e-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="f366e-180">Controlla le sospensioni dell’esecuzione dei processi, gli intervalli tra i tentativi, e i limiti dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="f366e-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="f366e-181">I Processi di database elastici includono un criterio di esecuzione di processo predefinito che provoca essenzialmente infiniti tentativi quando si verificano errori di attività di processo con backoff esponenziale di intervalli tra ogni tentativo.</span><span class="sxs-lookup"><span data-stu-id="f366e-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="f366e-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="f366e-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="f366e-183">New-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="f366e-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="f366e-184">Set-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="f366e-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="f366e-185">Pianificazione</span><span class="sxs-lookup"><span data-stu-id="f366e-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="f366e-186">Tempo base specifica per l'esecuzione tootake luogo un intervallo ricorrente o su una sola volta.</span><span class="sxs-lookup"><span data-stu-id="f366e-186">Time based specification for execution tootake place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="f366e-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="f366e-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="f366e-188">New-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="f366e-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="f366e-189">Set-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="f366e-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="f366e-190">Trigger del processo</span><span class="sxs-lookup"><span data-stu-id="f366e-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="f366e-191">Un mapping tra un processo e l'esecuzione del processo tootrigger una pianificazione in base toohello pianificazione.</span><span class="sxs-lookup"><span data-stu-id="f366e-191">A mapping between a job and a schedule tootrigger job execution according toohello schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="f366e-192">New-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="f366e-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="f366e-193">Remove-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="f366e-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="f366e-194">Tipi di gruppo di processi di database elastici supportati</span><span class="sxs-lookup"><span data-stu-id="f366e-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="f366e-195">processo Hello esegue script Transact-SQL (T-SQL) o un'applicazione di dacpac tra un gruppo di database.</span><span class="sxs-lookup"><span data-stu-id="f366e-195">hello job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="f366e-196">Quando un processo viene inviato toobe eseguita in un gruppo di database, il processo di hello "espande" hello in processi figlio in cui ogni esegue hello richiesto l'esecuzione su un singolo database nel gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-196">When a job is submitted toobe executed across a group of databases, hello job “expands” hello into child jobs where each performs hello requested execution against a single database in hello group.</span></span> 

<span data-ttu-id="f366e-197">Si possono creare due tipi di gruppi:</span><span class="sxs-lookup"><span data-stu-id="f366e-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="f366e-198">[Mappa partizioni](sql-database-elastic-scale-shard-map-management.md) gruppo: quando tootarget inviato una mappa partizioni è un processo, processo hello query hello partizioni mappa toodetermine il set di partizioni corrente e quindi crea i processi per ogni partizione figlio nella mappa partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted tootarget a shard map, hello job queries hello shard map toodetermine its current set of shards, and then creates child jobs for each shard in hello shard map.</span></span>
* <span data-ttu-id="f366e-199">Gruppo Raccolta personalizzata: set di database personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f366e-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="f366e-200">Quando un processo è destinato a una raccolta personalizzata, li crea i processi per ogni database attualmente in una raccolta personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-200">When a job targets a custom collection, it creates child jobs for each database currently in hello custom collection.</span></span>

## <a name="tooset-hello-elastic-database-jobs-connection"></a><span data-ttu-id="f366e-201">hello tooset connessione di processi di Database elastico</span><span class="sxs-lookup"><span data-stu-id="f366e-201">tooset hello Elastic Database jobs connection</span></span>
<span data-ttu-id="f366e-202">Una connessione è necessario impostare toohello processi di toobe *database del controllo* toousing precedente hello processi API.</span><span class="sxs-lookup"><span data-stu-id="f366e-202">A connection needs toobe set toohello jobs *control database* prior toousing hello jobs APIs.</span></span> <span data-ttu-id="f366e-203">Esecuzione di questo cmdlet attiva un toopop finestra credential per richiedere nome utente hello e la password creata durante l'installazione di processi di Database elastico.</span><span class="sxs-lookup"><span data-stu-id="f366e-203">Running this cmdlet triggers a credential window toopop up requesting hello user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="f366e-204">Tutti gli esempi forniti in questo argomento presuppongono che il primo passaggio sia già stato eseguito.</span><span class="sxs-lookup"><span data-stu-id="f366e-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="f366e-205">Aprire i processi di Database elastico toohello una connessione:</span><span class="sxs-lookup"><span data-stu-id="f366e-205">Open a connection toohello Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a><span data-ttu-id="f366e-206">Credenziali crittografate all'interno di processi di Database elastico hello</span><span class="sxs-lookup"><span data-stu-id="f366e-206">Encrypted credentials within hello Elastic Database jobs</span></span>
<span data-ttu-id="f366e-207">Le credenziali del database possono essere inserite nei processi hello *database del controllo* con la password crittografata.</span><span class="sxs-lookup"><span data-stu-id="f366e-207">Database credentials can be inserted into hello jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="f366e-208">È necessario toostore credenziali tooenable processi toobe eseguita in un secondo momento (utilizzando le pianificazioni dei processi).</span><span class="sxs-lookup"><span data-stu-id="f366e-208">It is necessary toostore credentials tooenable jobs toobe executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="f366e-209">Crittografia tramite un certificato creato come parte dello script di installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-209">Encryption works through a certificate created as part of hello installation script.</span></span> <span data-ttu-id="f366e-210">Crea script di installazione di Hello e caricamenti hello certificato hello servizio Cloud di Azure per la decrittografia di hello archiviate password crittografate.</span><span class="sxs-lookup"><span data-stu-id="f366e-210">hello installation script creates and uploads hello certificate into hello Azure Cloud Service for decryption of hello stored encrypted passwords.</span></span> <span data-ttu-id="f366e-211">in un secondo momento Hello servizio Cloud di Azure archivia la chiave pubblica hello all'interno di processi hello *database del controllo* che consente di hello API di PowerShell o portale di Azure classico interfaccia tooencrypt una password fornita senza richiedere il certificato di hello toobe installato nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="f366e-211">hello Azure Cloud Service later stores hello public key within hello jobs *control database* which enables hello PowerShell API or Azure Classic Portal interface tooencrypt a provided password without requiring hello certificate toobe locally installed.</span></span>

<span data-ttu-id="f366e-212">le password delle credenziali di Hello sono crittografati e protetti da utenti accesso in sola lettura tooElastic processi degli oggetti di Database.</span><span class="sxs-lookup"><span data-stu-id="f366e-212">hello credential passwords are encrypted and secure from users with read-only access tooElastic Database jobs objects.</span></span> <span data-ttu-id="f366e-213">Ma è possibile che un utente malintenzionato con accesso in lettura-scrittura tooElastic processi Database oggetti tooextract una password.</span><span class="sxs-lookup"><span data-stu-id="f366e-213">But it is possible for a malicious user with read-write access tooElastic Database Jobs objects tooextract a password.</span></span> <span data-ttu-id="f366e-214">Le credenziali sono progettate toobe riutilizzati tra esecuzioni del processo.</span><span class="sxs-lookup"><span data-stu-id="f366e-214">Credentials are designed toobe reused across job executions.</span></span> <span data-ttu-id="f366e-215">Le credenziali vengono passate tootarget database quando si stabiliscono connessioni.</span><span class="sxs-lookup"><span data-stu-id="f366e-215">Credentials are passed tootarget databases when establishing connections.</span></span> <span data-ttu-id="f366e-216">Non sono attualmente presenti restrizioni per i database di destinazione hello utilizzati per le credenziali, l'utente malintenzionato aggiunga un database di destinazione per un database nel controllo del codice dell'utente malintenzionato hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-216">There are currently no restrictions on hello target databases used for each credential, malicious user could add a database target for a database under hello malicious user's control.</span></span> <span data-ttu-id="f366e-217">utente Hello successivamente è stato possibile avviare un processo di destinazione password della credenziale in questo database toogain hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-217">hello user could subsequently start a job targeting this database toogain hello credential's password.</span></span>

<span data-ttu-id="f366e-218">Le procedure consigliate per i processi di database elastici includono:</span><span class="sxs-lookup"><span data-stu-id="f366e-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="f366e-219">Limitare l'utilizzo dei singoli utenti di tootrusted API hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-219">Limit usage of hello APIs tootrusted individuals.</span></span>
* <span data-ttu-id="f366e-220">Le credenziali devono avere hello almeno dei privilegi necessari tooperform hello mansione.</span><span class="sxs-lookup"><span data-stu-id="f366e-220">Credentials should have hello least privileges necessary tooperform hello job task.</span></span>  <span data-ttu-id="f366e-221">Per altre informazioni, vedere l'articolo [Autorizzazioni in SQL Server](https://msdn.microsoft.com/library/bb669084.aspx) di MSDN.</span><span class="sxs-lookup"><span data-stu-id="f366e-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="f366e-222">toocreate una credenziale per l'esecuzione del processo tra i database crittografata</span><span class="sxs-lookup"><span data-stu-id="f366e-222">toocreate an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="f366e-223">toocreate crittografata con una nuova credenziale, hello [ **cmdlet Get-Credential** ](https://technet.microsoft.com/library/hh849815.aspx) richiede un nome utente e una password che può essere passata toohello [ **New AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span><span class="sxs-lookup"><span data-stu-id="f366e-223">toocreate a new encrypted credential, hello [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed toohello [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a><span data-ttu-id="f366e-224">credenziali tooupdate</span><span class="sxs-lookup"><span data-stu-id="f366e-224">tooupdate credentials</span></span>
<span data-ttu-id="f366e-225">Quando si modificano le password, utilizzare hello [ **cmdlet Set-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) e set hello **CredentialName** parametro.</span><span class="sxs-lookup"><span data-stu-id="f366e-225">When passwords change, use hello [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set hello **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a><span data-ttu-id="f366e-226">toodefine una destinazione di mappa partizioni di Database elastico</span><span class="sxs-lookup"><span data-stu-id="f366e-226">toodefine an Elastic Database shard map target</span></span>
<span data-ttu-id="f366e-227">un processo in tutti i database in un set di partizioni tooexecute (creato utilizzando [libreria client di Database elastico](sql-database-elastic-database-client-library.md)), utilizzare una mappa partizioni come destinazione database hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-227">tooexecute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as hello database target.</span></span> <span data-ttu-id="f366e-228">In questo esempio richiede un'applicazione partizionata utilizzando la libreria client di Database elastico hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-228">This example requires a sharded application created using hello Elastic Database client library.</span></span> <span data-ttu-id="f366e-229">Vedere l'esempio in [Iniziare a usare gli strumenti di database elastici](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f366e-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="f366e-230">database di gestione della mappa partizioni Hello deve essere impostato come database di destinazione e quindi mappa partizioni specifici hello deve essere specificata come destinazione.</span><span class="sxs-lookup"><span data-stu-id="f366e-230">hello shard map manager database must be set as a database target and then hello specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="f366e-231">Creare uno Script T-SQL per l'esecuzione tra database</span><span class="sxs-lookup"><span data-stu-id="f366e-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="f366e-232">Durante la creazione di script T-SQL per l'esecuzione, è consigliabile toobuild li toobe [idempotente](https://en.wikipedia.org/wiki/Idempotence) e resilienti in caso di errori.</span><span class="sxs-lookup"><span data-stu-id="f366e-232">When creating T-SQL scripts for execution, it is highly recommended toobuild them toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="f366e-233">I processi di Database elastici ritenterà l'esecuzione di uno script ogni volta che l'esecuzione si verifica un errore, indipendentemente dalla classificazione hello dell'errore hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of hello classification of hello failure.</span></span>

<span data-ttu-id="f366e-234">Hello utilizzare [ **cmdlet New-AzureSqlJobContent** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate e salvare uno script per l'esecuzione e impostare hello **- documento ContentName** e **- CommandText**parametri.</span><span class="sxs-lookup"><span data-stu-id="f366e-234">Use hello [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate and save a script for execution and set hello **-ContentName** and **-CommandText** parameters.</span></span>

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="f366e-235">Creare un nuovo script da un file</span><span class="sxs-lookup"><span data-stu-id="f366e-235">Create a new script from a file</span></span>
<span data-ttu-id="f366e-236">Se lo script T-SQL hello è definito all'interno di un file, utilizzare questo script hello tooimport:</span><span class="sxs-lookup"><span data-stu-id="f366e-236">If hello T-SQL script is defined within a file, use this tooimport hello script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="f366e-237">script tooupdate T-SQL per l'esecuzione tra database</span><span class="sxs-lookup"><span data-stu-id="f366e-237">tooupdate a T-SQL script for execution across databases</span></span>
<span data-ttu-id="f366e-238">L'aggiornamento di script di PowerShell hello testo del comando T-SQL per uno script esistente.</span><span class="sxs-lookup"><span data-stu-id="f366e-238">This PowerShell script updates hello T-SQL command text for an existing script.</span></span>

<span data-ttu-id="f366e-239">Set hello seguente variabili tooreflect hello desiderato script definizione toobe insieme:</span><span class="sxs-lookup"><span data-stu-id="f366e-239">Set hello following variables tooreflect hello desired script definition toobe set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a><span data-ttu-id="f366e-240">script esistente tooan tooupdate hello definizione</span><span class="sxs-lookup"><span data-stu-id="f366e-240">tooupdate hello definition tooan existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a><span data-ttu-id="f366e-241">toocreate tooexecute un processo uno script in una mappa partizioni</span><span class="sxs-lookup"><span data-stu-id="f366e-241">toocreate a job tooexecute a script across a shard map</span></span>
<span data-ttu-id="f366e-242">Questo script di PowerShell avvia un processo per l'esecuzione di uno script in ogni partizione di una mappa partizioni di scalabilità elastica.</span><span class="sxs-lookup"><span data-stu-id="f366e-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="f366e-243">Hello set seguenti hello tooreflect variabili desiderato script e destinazione:</span><span class="sxs-lookup"><span data-stu-id="f366e-243">Set hello following variables tooreflect hello desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a><span data-ttu-id="f366e-244">tooexecute un processo</span><span class="sxs-lookup"><span data-stu-id="f366e-244">tooexecute a job</span></span>
<span data-ttu-id="f366e-245">Questo script di PowerShell esegue un processo esistente:</span><span class="sxs-lookup"><span data-stu-id="f366e-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="f366e-246">Aggiornare hello toohave nome di variabile tooreflect hello desiderato processo eseguito seguenti:</span><span class="sxs-lookup"><span data-stu-id="f366e-246">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="f366e-247">stato hello tooretrieve una singola esecuzione dei processi</span><span class="sxs-lookup"><span data-stu-id="f366e-247">tooretrieve hello state of a single job execution</span></span>
<span data-ttu-id="f366e-248">Hello utilizzare [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) e set hello **JobExecutionId** stato hello tooview di parametro di esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="f366e-248">Use hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set hello **JobExecutionId** parameter tooview hello state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="f366e-249">Utilizzare hello stesso **Get AzureSqlJobExecution** cmdlet con hello **IncludeChildren** parametro tooview hello stato esecuzioni del processo figlio, vale a dire hello stato specifico per ogni esecuzione del processo su ogni database di destinazione dal processo hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-249">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a><span data-ttu-id="f366e-250">stato hello tooview tra più esecuzioni di processo</span><span class="sxs-lookup"><span data-stu-id="f366e-250">tooview hello state across multiple job executions</span></span>
<span data-ttu-id="f366e-251">Hello [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) ha più parametri facoltativi che possono essere utilizzati toodisplay più esecuzioni di processo, filtrate tramite parametri hello fornito.</span><span class="sxs-lookup"><span data-stu-id="f366e-251">hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="f366e-252">esempio Hello vengono illustrate alcune delle possibili modi di hello toouse Get AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="f366e-252">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="f366e-253">Recuperare tutte le esecuzioni attive di processo di primo livello:</span><span class="sxs-lookup"><span data-stu-id="f366e-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="f366e-254">Recuperare tutte le esecuzioni di processo di primo livello, incluse le esecuzioni di processo inattive:</span><span class="sxs-lookup"><span data-stu-id="f366e-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="f366e-255">Recuperare tutte le esecuzioni di processo figlio di un ID di esecuzione processo fornito, incluse le esecuzioni di processo inattive:</span><span class="sxs-lookup"><span data-stu-id="f366e-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="f366e-256">Recuperare tutte le esecuzioni di processo create utilizzando una pianificazione / processo di combinazione, inclusi i processi inattivi:</span><span class="sxs-lookup"><span data-stu-id="f366e-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="f366e-257">Recuperare tutti i processi destinati a una mappa di partizione specificata, inclusi i processi inattivi:</span><span class="sxs-lookup"><span data-stu-id="f366e-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="f366e-258">Recuperare tutti i processi destinati a una raccolta personalizzata specificata, inclusi i processi inattivi:</span><span class="sxs-lookup"><span data-stu-id="f366e-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="f366e-259">Recuperare l'elenco di hello di esecuzioni di attività del processo in esecuzione un processo specifico:</span><span class="sxs-lookup"><span data-stu-id="f366e-259">Retrieve hello list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="f366e-260">Recuperare i dettagli di esecuzione delle attività di processo:</span><span class="sxs-lookup"><span data-stu-id="f366e-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="f366e-261">Hello lo script di PowerShell seguente può essere utilizzato tooview hello dettagli di un'esecuzione di attività di processo, è particolarmente utile quando il debug degli errori di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f366e-261">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a><span data-ttu-id="f366e-262">errori di tooretrieve all'interno di esecuzioni di attività di processo</span><span class="sxs-lookup"><span data-stu-id="f366e-262">tooretrieve failures within job task executions</span></span>
<span data-ttu-id="f366e-263">Hello **JobTaskExecution oggetto** include una proprietà per hello del ciclo di vita dell'attività hello insieme a una proprietà del messaggio.</span><span class="sxs-lookup"><span data-stu-id="f366e-263">hello **JobTaskExecution object** includes a property for hello lifecycle of hello task along with a message property.</span></span> <span data-ttu-id="f366e-264">Se un'esecuzione di attività del processo non è riuscita, hello del ciclo di vita e verrà impostata troppo*Failed* e verrà impostata la proprietà del messaggio hello toohello messaggio di eccezione risultante e il relativo stack.</span><span class="sxs-lookup"><span data-stu-id="f366e-264">If a job task execution failed, hello lifecycle property will be set too*Failed* and hello message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="f366e-265">Se un processo non riuscito, è importante tooview i dettagli di hello delle attività di processo che non è riuscita per un determinato processo.</span><span class="sxs-lookup"><span data-stu-id="f366e-265">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a><span data-ttu-id="f366e-266">toowait per toocomplete di esecuzione un processo</span><span class="sxs-lookup"><span data-stu-id="f366e-266">toowait for a job execution toocomplete</span></span>
<span data-ttu-id="f366e-267">Hello lo script di PowerShell seguente può essere utilizzato toowait per un toocomplete attività processo:</span><span class="sxs-lookup"><span data-stu-id="f366e-267">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="f366e-268">Creare un criterio di esecuzione personalizzata</span><span class="sxs-lookup"><span data-stu-id="f366e-268">Create a custom execution policy</span></span>
<span data-ttu-id="f366e-269">I processi di database elastici supportano la creazione di criteri di esecuzione personalizzati che possono essere applicati all'avvio dei processi.</span><span class="sxs-lookup"><span data-stu-id="f366e-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="f366e-270">Criteri di esecuzione che attualmente consentono la definizione di:</span><span class="sxs-lookup"><span data-stu-id="f366e-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="f366e-271">Nome: Identificatore per i criteri di esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-271">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="f366e-272">Timeout del processo: tempo totale prima che un processo venga annullato dai processi di database elastici.</span><span class="sxs-lookup"><span data-stu-id="f366e-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="f366e-273">Intervallo tra tentativi iniziale: Intervallo toowait prima del primo nuovo tentativo.</span><span class="sxs-lookup"><span data-stu-id="f366e-273">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="f366e-274">Intervallo tra tentativi massimo: Limite massimo di tentativi intervalli toouse.</span><span class="sxs-lookup"><span data-stu-id="f366e-274">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="f366e-275">Coefficiente di Backoff intervallo tentativi: Coefficiente utilizzato successivo intervallo hello toocalculate tra i tentativi.</span><span class="sxs-lookup"><span data-stu-id="f366e-275">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="f366e-276">Hello formula seguente viene utilizzata: (intervallo di tentativi iniziale) * Math.pow (intervallo Backoff coefficiente (), (numero di tentativi) - 2).</span><span class="sxs-lookup"><span data-stu-id="f366e-276">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="f366e-277">Numero massimo di tentativi: hello massimo di ripetizione tentativi tooperform all'interno di un processo.</span><span class="sxs-lookup"><span data-stu-id="f366e-277">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="f366e-278">criteri di esecuzione predefiniti Hello utilizzano hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="f366e-278">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="f366e-279">Nome: Criterio di esecuzione predefinito</span><span class="sxs-lookup"><span data-stu-id="f366e-279">Name: Default execution policy</span></span>
* <span data-ttu-id="f366e-280">Timeout del processo: 1 settimana</span><span class="sxs-lookup"><span data-stu-id="f366e-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="f366e-281">Intervallo tra tentativi iniziale: 100 millisecondi</span><span class="sxs-lookup"><span data-stu-id="f366e-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="f366e-282">Intervallo massimo tra tentativi: 30 minuti</span><span class="sxs-lookup"><span data-stu-id="f366e-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="f366e-283">Coefficiente di intervallo tra tentativi: 2</span><span class="sxs-lookup"><span data-stu-id="f366e-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="f366e-284">Numero massimo di tentativi: 2,147,483,647</span><span class="sxs-lookup"><span data-stu-id="f366e-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="f366e-285">Creare criteri di esecuzione hello desiderato:</span><span class="sxs-lookup"><span data-stu-id="f366e-285">Create hello desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="f366e-286">Aggiornare il criterio di esecuzione personalizzato</span><span class="sxs-lookup"><span data-stu-id="f366e-286">Update a custom execution policy</span></span>
<span data-ttu-id="f366e-287">Aggiornare tooupdate criteri di esecuzione hello desiderato:</span><span class="sxs-lookup"><span data-stu-id="f366e-287">Update hello desired execution policy tooupdate:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="f366e-288">Annullare un processo</span><span class="sxs-lookup"><span data-stu-id="f366e-288">Cancel a job</span></span>
<span data-ttu-id="f366e-289">I processi di database elastici supportano le richieste di annullamento dei processi.</span><span class="sxs-lookup"><span data-stu-id="f366e-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="f366e-290">Se i processi di Database elastico rileva una richiesta di annullamento per un processo in fase di esecuzione, verrà eseguito un tentativo con il processo di hello toostop.</span><span class="sxs-lookup"><span data-stu-id="f366e-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="f366e-291">E’ possibile cancellare un processo in due modi diversi tramite i processi di database elastici:</span><span class="sxs-lookup"><span data-stu-id="f366e-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="f366e-292">Annullamento di attività attualmente in esecuzione: se un annullamento viene rilevato durante un'attività è attualmente in esecuzione, verrà tentato un annullamento all'interno di hello aspetto dell'attività hello attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f366e-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="f366e-293">Ad esempio: se è presente una query a lunga esecuzione viene eseguita quando viene eseguito un tentativo di annullamento, sarà presente una query di hello toocancel tentativo.</span><span class="sxs-lookup"><span data-stu-id="f366e-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="f366e-294">Annullamento di tentativi dell'attività: se un annullamento viene rilevato dal thread di controllo hello prima di un'attività viene avviata per l'esecuzione, il thread di controllo hello evitare avvio attività hello e dichiarare richiesta hello come annullata.</span><span class="sxs-lookup"><span data-stu-id="f366e-294">Canceling task retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="f366e-295">Se è richiesto un annullamento di processo per un processo padre, la richiesta di annullamento hello sarà rispettata per il processo padre hello e per tutti i relativi processi figlio.</span><span class="sxs-lookup"><span data-stu-id="f366e-295">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="f366e-296">toosubmit una richiesta di annullamento, utilizzare hello [ **cmdlet Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) e set hello **JobExecutionId** parametro.</span><span class="sxs-lookup"><span data-stu-id="f366e-296">toosubmit a cancellation request, use hello [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set hello **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="f366e-297">toodelete un processo e la cronologia dei processi in modo asincrono</span><span class="sxs-lookup"><span data-stu-id="f366e-297">toodelete a job and job history asynchronously</span></span>
<span data-ttu-id="f366e-298">I processi di database elastici supportano l'eliminazione asincrona dei processi.</span><span class="sxs-lookup"><span data-stu-id="f366e-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="f366e-299">Un processo può essere contrassegnato per l'eliminazione e sistema hello eliminerà processo hello e tutta la relativa cronologia processo dopo aver completato tutte le esecuzioni di processo per il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-299">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="f366e-300">sistema Hello non annullerà automaticamente le esecuzioni di processo attivo.</span><span class="sxs-lookup"><span data-stu-id="f366e-300">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="f366e-301">Richiamare [ **Stop AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel esecuzioni di processo attivo.</span><span class="sxs-lookup"><span data-stu-id="f366e-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel active job executions.</span></span>

<span data-ttu-id="f366e-302">l'eliminazione di processo tootrigger, utilizzare hello [ **cmdlet Remove-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) e set hello **JobName** parametro.</span><span class="sxs-lookup"><span data-stu-id="f366e-302">tootrigger job deletion, use hello [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set hello **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a><span data-ttu-id="f366e-303">toocreate una destinazione di database personalizzati</span><span class="sxs-lookup"><span data-stu-id="f366e-303">toocreate a custom database target</span></span>
<span data-ttu-id="f366e-304">È possibile definire destinazioni di database personalizzate per l'esecuzione diretta o per l'inclusione in un gruppo di database personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f366e-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="f366e-305">Ad esempio, in quanto **pool elastici** sono non ancora supportato direttamente tramite APIs di PowerShell, è possibile creare un database personalizzato di destinazione e destinazione della raccolta di database personalizzata che comprende tutti i database nel pool di hello hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="f366e-306">Impostare le seguenti variabili tooreflect hello desiderato database informazioni hello:</span><span class="sxs-lookup"><span data-stu-id="f366e-306">Set hello following variables tooreflect hello desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a><span data-ttu-id="f366e-307">toocreate una destinazione di raccolta di database personalizzati</span><span class="sxs-lookup"><span data-stu-id="f366e-307">toocreate a custom database collection target</span></span>
<span data-ttu-id="f366e-308">Hello utilizzare [ **New AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) toodefine cmdlet un'esecuzione di database personalizzato insieme destinazione tooenable tra più destinazioni definita per il database.</span><span class="sxs-lookup"><span data-stu-id="f366e-308">Use hello [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine a custom database collection target tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="f366e-309">Dopo aver creato un gruppo di database, database possono essere associati a una destinazione di una raccolta personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-309">After creating a database group, databases can be associated with hello custom collection target.</span></span>

<span data-ttu-id="f366e-310">Impostare hello seguente configurazione di destinazione di variabili tooreflect hello raccolta personalizzata desiderata:</span><span class="sxs-lookup"><span data-stu-id="f366e-310">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="f366e-311">destinazione della raccolta tooadd database tooa database personalizzato</span><span class="sxs-lookup"><span data-stu-id="f366e-311">tooadd databases tooa custom database collection target</span></span>
<span data-ttu-id="f366e-312">una raccolta personalizzata specifica database tooa tooadd utilizzare hello [ **Aggiungi AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f366e-312">tooadd a database tooa specific custom collection use hello [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="f366e-313">Esaminare i database hello all'interno di una destinazione di raccolta di database personalizzati</span><span class="sxs-lookup"><span data-stu-id="f366e-313">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="f366e-314">Hello utilizzare [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) database di cmdlet tooretrieve hello figlio all'interno di una destinazione di raccolta database personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f366e-314">Use hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve hello child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="f366e-315">Creare un processo tooexecute uno script per una destinazione di raccolta database personalizzato</span><span class="sxs-lookup"><span data-stu-id="f366e-315">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="f366e-316">Hello utilizzare [ **New AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) toocreate cmdlet un processo rispetto a un gruppo di database definiti da una destinazione di raccolta database personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f366e-316">Use hello [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="f366e-317">I processi di Database elastici espanderà processo hello in più processi figlio, ogni database tooa corrispondente associata alla destinazione di raccolta di database personalizzata hello e assicurarsi che viene eseguito lo script di hello in tutti i database.</span><span class="sxs-lookup"><span data-stu-id="f366e-317">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="f366e-318">Nuovamente, è importante che gli script siano idempotenti toobe resilienti tooretries.</span><span class="sxs-lookup"><span data-stu-id="f366e-318">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="f366e-319">Raccolta dei dati tra database</span><span class="sxs-lookup"><span data-stu-id="f366e-319">Data collection across databases</span></span>
<span data-ttu-id="f366e-320">È possibile utilizzare tooexecute un processo una query in un gruppo di database e tabella specifica di hello risultati tooa di trasmissione.</span><span class="sxs-lookup"><span data-stu-id="f366e-320">You can use a job tooexecute a query across a group of databases and send hello results tooa specific table.</span></span> <span data-ttu-id="f366e-321">è possibile eseguire query di tabella Hello dopo i risultati della query di hello fatti toosee hello da ogni database.</span><span class="sxs-lookup"><span data-stu-id="f366e-321">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="f366e-322">In questo modo una query tooexecute un metodo asincrono in numerosi database.</span><span class="sxs-lookup"><span data-stu-id="f366e-322">This provides an asynchronous method tooexecute a query across many databases.</span></span> <span data-ttu-id="f366e-323">I tentativi non riusciti vengono gestiti automaticamente tramite la ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="f366e-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="f366e-324">tabella di destinazione specificato Hello verrà creata automaticamente se non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="f366e-324">hello specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="f366e-325">nuova tabella Hello corrisponde allo schema di hello di hello restituito set di risultati.</span><span class="sxs-lookup"><span data-stu-id="f366e-325">hello new table matches hello schema of hello returned result set.</span></span> <span data-ttu-id="f366e-326">Se uno script restituisce più set di risultati, i processi di Database elastico invierà prima tabella di destinazione toohello hello.</span><span class="sxs-lookup"><span data-stu-id="f366e-326">If a script returns multiple result sets, Elastic Database jobs will only send hello first toohello destination table.</span></span>

<span data-ttu-id="f366e-327">Hello seguente script di PowerShell esegue uno script e raccoglie i risultati in una tabella specificata.</span><span class="sxs-lookup"><span data-stu-id="f366e-327">hello following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="f366e-328">Questo script presuppone che sia stato creato uno script T-SQL che restituisce un singolo set di risultati e che sia stata creata una destinazione della raccolta di database personalizzata.</span><span class="sxs-lookup"><span data-stu-id="f366e-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="f366e-329">Questo script utilizza hello [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f366e-329">This script uses hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="f366e-330">Impostare i parametri di hello per script, le credenziali e la destinazione di esecuzione:</span><span class="sxs-lookup"><span data-stu-id="f366e-330">Set hello parameters for script, credentials, and execution target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="f366e-331">toocreate e avviare un processo per gli scenari di raccolta dati</span><span class="sxs-lookup"><span data-stu-id="f366e-331">toocreate and start a job for data collection scenarios</span></span>
<span data-ttu-id="f366e-332">Questo script utilizza hello [ **inizio AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f366e-332">This script uses hello [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a><span data-ttu-id="f366e-333">un trigger di processo esecuzione tooschedule</span><span class="sxs-lookup"><span data-stu-id="f366e-333">tooschedule a job execution trigger</span></span>
<span data-ttu-id="f366e-334">Hello lo script di PowerShell seguente può essere utilizzato toocreate a una pianificazione ricorrente.</span><span class="sxs-lookup"><span data-stu-id="f366e-334">hello following PowerShell script can be used toocreate a recurring schedule.</span></span> <span data-ttu-id="f366e-335">Questo script usa l'intervallo di minuti, ma [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) supporta anche i parametri -DayInterval, -HourInterval, -MonthInterval e -WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="f366e-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="f366e-336">Le pianificazioni che vengono eseguite una sola volta possono essere create specificando -OneTime.</span><span class="sxs-lookup"><span data-stu-id="f366e-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="f366e-337">Creare una nuova pianificazione:</span><span class="sxs-lookup"><span data-stu-id="f366e-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="f366e-338">un processo eseguito su una pianificazione temporale tootrigger</span><span class="sxs-lookup"><span data-stu-id="f366e-338">tootrigger a job executed on a time schedule</span></span>
<span data-ttu-id="f366e-339">Un trigger di processo può essere definito toohave un processo eseguito in base tooa tempo di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="f366e-339">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="f366e-340">Hello lo script di PowerShell seguente può essere utilizzato toocreate un trigger di processo.</span><span class="sxs-lookup"><span data-stu-id="f366e-340">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="f366e-341">Utilizzare [New AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) e set hello seguendo le variabili toocorrespond toohello desiderato processo e pianificazione:</span><span class="sxs-lookup"><span data-stu-id="f366e-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set hello following variables toocorrespond toohello desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="f366e-342">tooremove un processo toostop associazione pianificata l'esecuzione su pianificazione</span><span class="sxs-lookup"><span data-stu-id="f366e-342">tooremove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="f366e-343">esecuzione del processo tramite un trigger di processo, il trigger di processo hello ripresenta toodiscontinue può essere rimosso.</span><span class="sxs-lookup"><span data-stu-id="f366e-343">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span> <span data-ttu-id="f366e-344">Rimuovere un toostop trigger di processo un processo venga eseguito secondo pianificazione tooa utilizzando hello [ **cmdlet Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span><span class="sxs-lookup"><span data-stu-id="f366e-344">Remove a job trigger toostop a job from being executed according tooa schedule using hello [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a><span data-ttu-id="f366e-345">Recuperare la pianificazione di processo trigger associati tooa ora</span><span class="sxs-lookup"><span data-stu-id="f366e-345">Retrieve job triggers bound tooa time schedule</span></span>
<span data-ttu-id="f366e-346">Hello lo script di PowerShell seguente può essere utilizzato tooobtain e visualizzare hello processo trigger tooa registrati ora determinata pianificazione.</span><span class="sxs-lookup"><span data-stu-id="f366e-346">hello following PowerShell script can be used tooobtain and display hello job triggers registered tooa particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a><span data-ttu-id="f366e-347">i trigger di processo tooretrieve associato tooa processo</span><span class="sxs-lookup"><span data-stu-id="f366e-347">tooretrieve job triggers bound tooa job</span></span>
<span data-ttu-id="f366e-348">Utilizzare [Get AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain e la visualizzazione di pianificazioni contenente un processo registrato.</span><span class="sxs-lookup"><span data-stu-id="f366e-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="f366e-349">toocreate un'applicazione livello dati (con estensione DACPAC) per l'esecuzione tra database</span><span class="sxs-lookup"><span data-stu-id="f366e-349">toocreate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="f366e-350">toocreate un file DACPAC, vedere [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span><span class="sxs-lookup"><span data-stu-id="f366e-350">toocreate a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="f366e-351">un file DACPAC, toodeploy utilizzare hello [cmdlet New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span><span class="sxs-lookup"><span data-stu-id="f366e-351">toodeploy a DACPAC, use hello [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="f366e-352">Hello DACPAC deve essere accessibile toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="f366e-352">hello DACPAC must be accessible toohello service.</span></span> <span data-ttu-id="f366e-353">È consigliabile tooupload un tooAzure DACPAC creato, archiviazione e creare un [firma di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) per hello DACPAC.</span><span class="sxs-lookup"><span data-stu-id="f366e-353">It is recommended tooupload a created DACPAC tooAzure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for hello DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="f366e-354">tooupdate un'applicazione livello dati (con estensione DACPAC) per l'esecuzione tra database</span><span class="sxs-lookup"><span data-stu-id="f366e-354">tooupdate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="f366e-355">Dacpac esistente registrati all'interno di processi di Database elastico può essere aggiornato toopoint toonew URI.</span><span class="sxs-lookup"><span data-stu-id="f366e-355">Existing DACPACs registered within Elastic Database Jobs can be updated toopoint toonew URIs.</span></span> <span data-ttu-id="f366e-356">Hello utilizzare [ **cmdlet Set-AzureSqlJobContentDefinition** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello URI DACPAC su un oggetto esistente registrato DACPAC:</span><span class="sxs-lookup"><span data-stu-id="f366e-356">Use hello [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="f366e-357">toocreate tooapply un processo un'applicazione livello dati (con estensione DACPAC) tra database</span><span class="sxs-lookup"><span data-stu-id="f366e-357">toocreate a job tooapply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="f366e-358">Dopo aver creato un file DACPAC all'interno di processi di Database elastico, è possibile creare un processo tooapply hello DACPAC in un gruppo di database.</span><span class="sxs-lookup"><span data-stu-id="f366e-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created tooapply hello DACPAC across a group of databases.</span></span> <span data-ttu-id="f366e-359">Hello lo script di PowerShell seguente può essere utilizzato toocreate un processo con estensione DACPAC in una raccolta personalizzata di database:</span><span class="sxs-lookup"><span data-stu-id="f366e-359">hello following PowerShell script can be used toocreate a DACPAC job across a custom collection of databases:</span></span>

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
