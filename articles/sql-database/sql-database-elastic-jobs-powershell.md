---
title: Creare e gestire processi elastici con PowerShell | Documentazione Microsoft
description: PowerShell viene utilizzato per gestire i pool del database SQL di Azure
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
ms.openlocfilehash: b4c97e8f51581f9a3f7c5a8d8e82562255fe7b48
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="a211a-103">Creare e gestire processi elastici del database SQL con PowerShell (anteprima)</span><span class="sxs-lookup"><span data-stu-id="a211a-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="a211a-104">Le API di PowerShell per i **processi di database elastici** , in anteprima, consentono di definire il gruppo di database sul quale verranno eseguiti gli script.</span><span class="sxs-lookup"><span data-stu-id="a211a-104">The PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="a211a-105">Questo articolo illustra come creare e gestire **processi di database elastici** con i cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a211a-105">This article shows how to create and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="a211a-106">Vedere [Panoramica dei processi di database elastici](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a211a-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a211a-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a211a-107">Prerequisites</span></span>
* <span data-ttu-id="a211a-108">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a211a-108">An Azure subscription.</span></span> <span data-ttu-id="a211a-109">Per una versione di valutazione gratuita, vedere [Versione di valutazione gratuita di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a211a-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a211a-110">Un set di database creato con gli strumenti di database elastici.</span><span class="sxs-lookup"><span data-stu-id="a211a-110">A set of databases created with the Elastic Database tools.</span></span> <span data-ttu-id="a211a-111">Vedere [Iniziare a usare gli strumenti di database elastici](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a211a-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="a211a-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a211a-112">Azure PowerShell.</span></span> <span data-ttu-id="a211a-113">Per informazioni dettagliate, vedere [Come installare e configurare Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a211a-113">For detailed information, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="a211a-114">**processi di database elastici** di PowerShell, vedere [Installing processi di database elastici](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="a211a-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="a211a-115">Selezionare la sottoscrizione ad Azure</span><span class="sxs-lookup"><span data-stu-id="a211a-115">Select your Azure subscription</span></span>
<span data-ttu-id="a211a-116">Per selezionare la sottoscrizione, è necessario l'ID sottoscrizione (**-SubscriptionId**) o il nome della sottoscrizione (**-SubscriptionName**).</span><span class="sxs-lookup"><span data-stu-id="a211a-116">To select the subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="a211a-117">Se sono disponibili più sottoscrizioni, è possibile eseguire il cmdlet **Get-AzureRmSubscription** e copiare le informazioni sulla sottoscrizione desiderata dal set di risultati.</span><span class="sxs-lookup"><span data-stu-id="a211a-117">If you have multiple subscriptions you can run the **Get-AzureRmSubscription** cmdlet and copy the desired subscription information from the result set.</span></span> <span data-ttu-id="a211a-118">Dopo aver ottenuto le informazioni della sottoscrizione, eseguire il commandlet seguente per impostare tale sottoscrizione come predefinita, vale a dire la destinazione per la creazione e la gestione dei processi:</span><span class="sxs-lookup"><span data-stu-id="a211a-118">Once you have your subscription information, run the following commandlet to set this subscription as the default, namely the target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="a211a-119">L'utilizzo di [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) è consigliato per sviluppare ed eseguire gli script di PowerShell sui processi di database elastici.</span><span class="sxs-lookup"><span data-stu-id="a211a-119">The [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage to develop and execute PowerShell scripts against the Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="a211a-120">Oggetti dei processi di database elastici</span><span class="sxs-lookup"><span data-stu-id="a211a-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="a211a-121">La tabella seguente include l'elenco di tutti i tipi di oggetto dei **processi di database elastici** con la relativa descrizione e le API di PowerShell rilevanti.</span><span class="sxs-lookup"><span data-stu-id="a211a-121">The following table lists out all the object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="a211a-122">Tipo di oggetto</span><span class="sxs-lookup"><span data-stu-id="a211a-122">Object Type</span></span></th>
    <th><span data-ttu-id="a211a-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a211a-123">Description</span></span></th>
    <th><span data-ttu-id="a211a-124">API correlate di PowerShell</span><span class="sxs-lookup"><span data-stu-id="a211a-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="a211a-125">Credenziali</span><span class="sxs-lookup"><span data-stu-id="a211a-125">Credential</span></span></td>
    <td><span data-ttu-id="a211a-126">Nome utente e password da utilizzare per la connessione ai database per l'esecuzione di script o l'applicazione di DACPAC.</span><span class="sxs-lookup"><span data-stu-id="a211a-126">Username and password to use when connecting to databases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="a211a-127">La password viene crittografata prima dell’invio e archiviata nel database dei processi di database elastici.</span><span class="sxs-lookup"><span data-stu-id="a211a-127">The password is encrypted before sending to and storing in the Elastic Database Jobs database.</span></span>  <span data-ttu-id="a211a-128">La password viene decrittografata dal servizio dai processi di database elastici tramite la credenziale creata e caricata dallo script di installazione.</span><span class="sxs-lookup"><span data-stu-id="a211a-128">The password is decrypted by the Elastic Database Jobs service via the credential created and uploaded from the installation script.</span></span></td>
    <td><p><span data-ttu-id="a211a-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="a211a-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="a211a-130">New-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="a211a-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="a211a-131">Set-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="a211a-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="a211a-132">Script</span><span class="sxs-lookup"><span data-stu-id="a211a-132">Script</span></span></td>
    <td><span data-ttu-id="a211a-133">Script Transact-SQL da utilizzare per l'esecuzione nei database.</span><span class="sxs-lookup"><span data-stu-id="a211a-133">Transact-SQL script to be used for execution across databases.</span></span>  <span data-ttu-id="a211a-134">Lo script deve essere creato per essere idempotente, poiché il servizio ritenterà l'esecuzione dello script quando si verificheranno degli errori.</span><span class="sxs-lookup"><span data-stu-id="a211a-134">The script should be authored to be idempotent since the service will retry execution of the script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="a211a-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="a211a-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="a211a-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="a211a-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="a211a-137">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="a211a-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="a211a-138">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="a211a-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="a211a-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="a211a-139">DACPAC</span></span></td>
    <td><span data-ttu-id="a211a-140">Pacchetto dell'<a href="https://msdn.microsoft.com/library/ee210546.aspx">applicazione livello dati </a> da applicare tra i database.</span><span class="sxs-lookup"><span data-stu-id="a211a-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package to be applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="a211a-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="a211a-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="a211a-142">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="a211a-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="a211a-143">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="a211a-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="a211a-144">Destinazione del database</span><span class="sxs-lookup"><span data-stu-id="a211a-144">Database Target</span></span></td>
    <td><span data-ttu-id="a211a-145">Nome del database e del server che si riferisce a un Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="a211a-145">Database and server name pointing to an Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="a211a-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="a211a-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="a211a-147">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="a211a-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="a211a-148">Destinazione di partizionamento della mappa</span><span class="sxs-lookup"><span data-stu-id="a211a-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="a211a-149">Combinazione di una destinazione di database e una credenziale da utilizzare per determinare le informazioni archiviate all'interno di una mappa di partizionamento di un database elastico.</span><span class="sxs-lookup"><span data-stu-id="a211a-149">Combination of a database target and a credential to be used to determine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="a211a-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="a211a-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="a211a-151">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="a211a-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="a211a-152">Set-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="a211a-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="a211a-153">Destinazione di una raccolta personalizzata</span><span class="sxs-lookup"><span data-stu-id="a211a-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="a211a-154">Gruppo definito di database da utilizzare collettivamente per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a211a-154">Defined group of databases to collectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="a211a-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="a211a-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="a211a-156">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="a211a-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="a211a-157">Destinazione figlio di una raccolta personalizzata</span><span class="sxs-lookup"><span data-stu-id="a211a-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="a211a-158">Destinazione di database a cui fa riferimento una raccolta personalizzata.</span><span class="sxs-lookup"><span data-stu-id="a211a-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="a211a-159">Add-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="a211a-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="a211a-160">Remove-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="a211a-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="a211a-161">Job</span><span class="sxs-lookup"><span data-stu-id="a211a-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="a211a-162">Definizione dei parametri per un processo che possono essere utilizzati per attivare l'esecuzione o per soddisfare una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="a211a-162">Definition of parameters for a job that can be used to trigger execution or to fulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="a211a-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="a211a-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="a211a-164">New-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="a211a-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="a211a-165">Set-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="a211a-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="a211a-166">Esecuzione del processo</span><span class="sxs-lookup"><span data-stu-id="a211a-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="a211a-167">Contenitore di attività necessarie per soddisfare l'esecuzione di uno script o l’applicazione di un DACPAC a una destinazione utilizzando le credenziali per le connessioni di database con gestione degli errori gestiti in base ai criteri di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a211a-167">Container of tasks necessary to fulfill either executing a script or applying a DACPAC to a target using credentials for database connections with failures handled in accordance to an execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="a211a-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="a211a-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="a211a-169">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="a211a-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="a211a-170">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="a211a-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="a211a-171">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="a211a-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="a211a-172">Esecuzione dell'attività di processo</span><span class="sxs-lookup"><span data-stu-id="a211a-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="a211a-173">Singola unità di lavoro per soddisfare un processo.</span><span class="sxs-lookup"><span data-stu-id="a211a-173">Single unit of work to fulfill a job.</span></span></p>
    <p><span data-ttu-id="a211a-174">Se un'attività di processo non è in grado di essere eseguita con successo, verrà registrato il messaggio di eccezione risultante e una nuova attività di processo corrispondente verrà creata ed eseguita in base al criterio di esecuzione specificato.</span><span class="sxs-lookup"><span data-stu-id="a211a-174">If a job task is not able to successfully execute, the resulting exception message will be logged and a new matching job task will be created and executed in accordance to the specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="a211a-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="a211a-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="a211a-176">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="a211a-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="a211a-177">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="a211a-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="a211a-178">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="a211a-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="a211a-179">Criterio di esecuzione del processo</span><span class="sxs-lookup"><span data-stu-id="a211a-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="a211a-180">Controlla le sospensioni dell’esecuzione dei processi, gli intervalli tra i tentativi, e i limiti dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="a211a-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="a211a-181">I Processi di database elastici includono un criterio di esecuzione di processo predefinito che provoca essenzialmente infiniti tentativi quando si verificano errori di attività di processo con backoff esponenziale di intervalli tra ogni tentativo.</span><span class="sxs-lookup"><span data-stu-id="a211a-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="a211a-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="a211a-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="a211a-183">New-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="a211a-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="a211a-184">Set-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="a211a-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="a211a-185">Pianificazione</span><span class="sxs-lookup"><span data-stu-id="a211a-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="a211a-186">Specifiche relative al tempo utilizzate affinché l'esecuzione avvenga ad intervalli ricorrenti o una sola volta.</span><span class="sxs-lookup"><span data-stu-id="a211a-186">Time based specification for execution to take place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="a211a-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="a211a-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="a211a-188">New-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="a211a-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="a211a-189">Set-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="a211a-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="a211a-190">Trigger del processo</span><span class="sxs-lookup"><span data-stu-id="a211a-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="a211a-191">Un mapping tra un processo e una pianificazione per l'avvio dell’esecuzione del processo in base alla pianificazione.</span><span class="sxs-lookup"><span data-stu-id="a211a-191">A mapping between a job and a schedule to trigger job execution according to the schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="a211a-192">New-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="a211a-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="a211a-193">Remove-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="a211a-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="a211a-194">Tipi di gruppo di processi di database elastici supportati</span><span class="sxs-lookup"><span data-stu-id="a211a-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="a211a-195">Il processo esegue script Transact-SQL (T-SQL) o applica DACPAC in un gruppo di database.</span><span class="sxs-lookup"><span data-stu-id="a211a-195">The job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="a211a-196">Quando viene inviato un processo da eseguire in un gruppo di database, il processo si "espande" in processi figlio e ognuno completa l'esecuzione richiesta in un database singolo del gruppo.</span><span class="sxs-lookup"><span data-stu-id="a211a-196">When a job is submitted to be executed across a group of databases, the job “expands” the into child jobs where each performs the requested execution against a single database in the group.</span></span> 

<span data-ttu-id="a211a-197">Si possono creare due tipi di gruppi:</span><span class="sxs-lookup"><span data-stu-id="a211a-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="a211a-198">[Mappa partizioni](sql-database-elastic-scale-shard-map-management.md) : quando viene inviato un processo destinato a una mappa partizioni, il processo esegue query sulla mappa partizioni per determinare il set di partizioni corrente e quindi crea processi figlio per ogni partizione nella mappa partizioni.</span><span class="sxs-lookup"><span data-stu-id="a211a-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted to target a shard map, the job queries the shard map to determine its current set of shards, and then creates child jobs for each shard in the shard map.</span></span>
* <span data-ttu-id="a211a-199">Gruppo Raccolta personalizzata: set di database personalizzato.</span><span class="sxs-lookup"><span data-stu-id="a211a-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="a211a-200">Quando un processo è destinato a una raccolta personalizzata, crea processi figlio per ogni database attualmente nella raccolta personalizzata.</span><span class="sxs-lookup"><span data-stu-id="a211a-200">When a job targets a custom collection, it creates child jobs for each database currently in the custom collection.</span></span>

## <a name="to-set-the-elastic-database-jobs-connection"></a><span data-ttu-id="a211a-201">Per impostare la connessione dei processi di database elastici</span><span class="sxs-lookup"><span data-stu-id="a211a-201">To set the Elastic Database jobs connection</span></span>
<span data-ttu-id="a211a-202">È necessario impostare una connessione al *database di controllo* dei processi prima di usare le API dei processi.</span><span class="sxs-lookup"><span data-stu-id="a211a-202">A connection needs to be set to the jobs *control database* prior to using the jobs APIs.</span></span> <span data-ttu-id="a211a-203">L'esecuzione di questo cmdlet attiva la visualizzazione di una finestra delle credenziali che richiede il nome utente e la password creati durante l'installazione dei processi di database elastici.</span><span class="sxs-lookup"><span data-stu-id="a211a-203">Running this cmdlet triggers a credential window to pop up requesting the user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="a211a-204">Tutti gli esempi forniti in questo argomento presuppongono che il primo passaggio sia già stato eseguito.</span><span class="sxs-lookup"><span data-stu-id="a211a-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="a211a-205">Aprire una connessione ai processi di database elastici:</span><span class="sxs-lookup"><span data-stu-id="a211a-205">Open a connection to the Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-the-elastic-database-jobs"></a><span data-ttu-id="a211a-206">Credenziali crittografate all'interno dei processi di database elastici</span><span class="sxs-lookup"><span data-stu-id="a211a-206">Encrypted credentials within the Elastic Database jobs</span></span>
<span data-ttu-id="a211a-207">Le credenziali del database possono essere inserite nel *database di controllo* dei processi con la relativa password crittografata.</span><span class="sxs-lookup"><span data-stu-id="a211a-207">Database credentials can be inserted into the jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="a211a-208">È necessario archiviare le credenziali per abilitare l'esecuzione dei processi in un secondo momento tramite pianificazioni dei processi.</span><span class="sxs-lookup"><span data-stu-id="a211a-208">It is necessary to store credentials to enable jobs to be executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="a211a-209">La crittografia funziona tramite un certificato creato come parte dello script di installazione.</span><span class="sxs-lookup"><span data-stu-id="a211a-209">Encryption works through a certificate created as part of the installation script.</span></span> <span data-ttu-id="a211a-210">Lo script di installazione crea e carica il certificato nel servizio Cloud di Azure per la decrittografia delle password crittografate archiviate.</span><span class="sxs-lookup"><span data-stu-id="a211a-210">The installation script creates and uploads the certificate into the Azure Cloud Service for decryption of the stored encrypted passwords.</span></span> <span data-ttu-id="a211a-211">In seguito, il servizio cloud di Azure archivia la chiave pubblica nel *database di controllo* dei processi che consente all'API di PowerShell o all'interfaccia del portale di Azure classico di crittografare una password fornita, senza richiedere l'installazione locale del certificato.</span><span class="sxs-lookup"><span data-stu-id="a211a-211">The Azure Cloud Service later stores the public key within the jobs *control database* which enables the PowerShell API or Azure Classic Portal interface to encrypt a provided password without requiring the certificate to be locally installed.</span></span>

<span data-ttu-id="a211a-212">Le password delle credenziali vengono crittografate e protette dagli utenti con accesso in sola lettura agli oggetti dei processi di database elastici.</span><span class="sxs-lookup"><span data-stu-id="a211a-212">The credential passwords are encrypted and secure from users with read-only access to Elastic Database jobs objects.</span></span> <span data-ttu-id="a211a-213">È tuttavia possibile che un utente malintenzionato con accesso in lettura e scrittura agli oggetti dei processi di database elastici possa estrarre una password.</span><span class="sxs-lookup"><span data-stu-id="a211a-213">But it is possible for a malicious user with read-write access to Elastic Database Jobs objects to extract a password.</span></span> <span data-ttu-id="a211a-214">Le credenziali sono progettate per essere riutilizzate sulle esecuzioni del processo.</span><span class="sxs-lookup"><span data-stu-id="a211a-214">Credentials are designed to be reused across job executions.</span></span> <span data-ttu-id="a211a-215">Le credenziali vengono passate al database di destinazione quando si stabiliscono connessioni.</span><span class="sxs-lookup"><span data-stu-id="a211a-215">Credentials are passed to target databases when establishing connections.</span></span> <span data-ttu-id="a211a-216">Attualmente non sono previste restrizioni per i database di destinazione usati per le singole credenziali, quindi un utente malintenzionato potrebbe aggiungere una destinazione di database per un database sotto il suo controllo.</span><span class="sxs-lookup"><span data-stu-id="a211a-216">There are currently no restrictions on the target databases used for each credential, malicious user could add a database target for a database under the malicious user's control.</span></span> <span data-ttu-id="a211a-217">L'utente potrebbe quindi avviare un processo destinato a questo database per ottenere la password delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="a211a-217">The user could subsequently start a job targeting this database to gain the credential's password.</span></span>

<span data-ttu-id="a211a-218">Le procedure consigliate per i processi di database elastici includono:</span><span class="sxs-lookup"><span data-stu-id="a211a-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="a211a-219">Limitare l'utilizzo delle API a utenti attendibili.</span><span class="sxs-lookup"><span data-stu-id="a211a-219">Limit usage of the APIs to trusted individuals.</span></span>
* <span data-ttu-id="a211a-220">Le credenziali devono disporre dei privilegi minimi necessari per eseguire l'attività di processo.</span><span class="sxs-lookup"><span data-stu-id="a211a-220">Credentials should have the least privileges necessary to perform the job task.</span></span>  <span data-ttu-id="a211a-221">Per altre informazioni, vedere l'articolo [Autorizzazioni in SQL Server](https://msdn.microsoft.com/library/bb669084.aspx) di MSDN.</span><span class="sxs-lookup"><span data-stu-id="a211a-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="to-create-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="a211a-222">Per creare credenziali crittografate per l'esecuzione di processi nei database</span><span class="sxs-lookup"><span data-stu-id="a211a-222">To create an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="a211a-223">Per creare nuove credenziali crittografate, il [**cmdlet Get-Credential**](https://technet.microsoft.com/library/hh849815.aspx) richiede un nome utente e una password che possono essere passati al [**cmdlet New-AzureSqlJobCredential**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span><span class="sxs-lookup"><span data-stu-id="a211a-223">To create a new encrypted credential, the [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed to the [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="to-update-credentials"></a><span data-ttu-id="a211a-224">Per aggiornare le credenziali</span><span class="sxs-lookup"><span data-stu-id="a211a-224">To update credentials</span></span>
<span data-ttu-id="a211a-225">Quando la password cambia, usare il [**cmdlet Set-AzureSqlJobCredential**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) e impostare il parametro **CredentialName**.</span><span class="sxs-lookup"><span data-stu-id="a211a-225">When passwords change, use the [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set the **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="to-define-an-elastic-database-shard-map-target"></a><span data-ttu-id="a211a-226">Per definire la destinazione di una mappa partizioni del database elastico</span><span class="sxs-lookup"><span data-stu-id="a211a-226">To define an Elastic Database shard map target</span></span>
<span data-ttu-id="a211a-227">Per eseguire un processo su tutti i database in un set di partizioni, creato con la [libreria client dei database elastici](sql-database-elastic-database-client-library.md), usare una mappa partizioni come destinazione del database.</span><span class="sxs-lookup"><span data-stu-id="a211a-227">To execute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as the database target.</span></span> <span data-ttu-id="a211a-228">Questo esempio richiede un'applicazione partizionata creata con la libreria client dei database elastici.</span><span class="sxs-lookup"><span data-stu-id="a211a-228">This example requires a sharded application created using the Elastic Database client library.</span></span> <span data-ttu-id="a211a-229">Vedere l'esempio in [Iniziare a usare gli strumenti di database elastici](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a211a-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="a211a-230">Il database di gestione delle mappe partizioni deve essere impostato come destinazione di database e quindi si dovrà impostare la mappa partizioni specifica come destinazione.</span><span class="sxs-lookup"><span data-stu-id="a211a-230">The shard map manager database must be set as a database target and then the specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="a211a-231">Creare uno Script T-SQL per l'esecuzione tra database</span><span class="sxs-lookup"><span data-stu-id="a211a-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="a211a-232">Quando si creano script T-SQL per l'esecuzione, è consigliabile compilarli in modo che siano [idempotenti](https://en.wikipedia.org/wiki/Idempotence) e resilienti in caso di errori.</span><span class="sxs-lookup"><span data-stu-id="a211a-232">When creating T-SQL scripts for execution, it is highly recommended to build them to be [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="a211a-233">I processi di database elastici ritenterà l'esecuzione di uno script ogni volta che l'esecuzione rileva un errore, indipendentemente dalla classificazione dell'errore.</span><span class="sxs-lookup"><span data-stu-id="a211a-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of the classification of the failure.</span></span>

<span data-ttu-id="a211a-234">Usare il [**cmdlet New-AzureSqlJobContent**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) per creare e salvare uno script per l'esecuzione e impostare i parametri **-ContentName** e **-CommandText**.</span><span class="sxs-lookup"><span data-stu-id="a211a-234">Use the [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) to create and save a script for execution and set the **-ContentName** and **-CommandText** parameters.</span></span>

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

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="a211a-235">Creare un nuovo script da un file</span><span class="sxs-lookup"><span data-stu-id="a211a-235">Create a new script from a file</span></span>
<span data-ttu-id="a211a-236">Se lo script T-SQL è definito all'interno di un file, usare il codice seguente per importarlo:</span><span class="sxs-lookup"><span data-stu-id="a211a-236">If the T-SQL script is defined within a file, use this to import the script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path to SQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="to-update-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="a211a-237">Per aggiornare uno script T-SQL per l'esecuzione nei database</span><span class="sxs-lookup"><span data-stu-id="a211a-237">To update a T-SQL script for execution across databases</span></span>
<span data-ttu-id="a211a-238">Questo script di PowerShell aggiorna il testo del comando T-SQL per uno script esistente.</span><span class="sxs-lookup"><span data-stu-id="a211a-238">This PowerShell script updates the T-SQL command text for an existing script.</span></span>

<span data-ttu-id="a211a-239">Impostare le seguenti variabili in modo da riflettere la definizione dello script desiderata da impostare:</span><span class="sxs-lookup"><span data-stu-id="a211a-239">Set the following variables to reflect the desired script definition to be set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column to TestTable"
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

### <a name="to-update-the-definition-to-an-existing-script"></a><span data-ttu-id="a211a-240">Per aggiornare la definizione di uno script esistente</span><span class="sxs-lookup"><span data-stu-id="a211a-240">To update the definition to an existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="to-create-a-job-to-execute-a-script-across-a-shard-map"></a><span data-ttu-id="a211a-241">Creare un processo che esegua uno script in una mappa partizioni</span><span class="sxs-lookup"><span data-stu-id="a211a-241">To create a job to execute a script across a shard map</span></span>
<span data-ttu-id="a211a-242">Questo script di PowerShell avvia un processo per l'esecuzione di uno script in ogni partizione di una mappa partizioni di scalabilità elastica.</span><span class="sxs-lookup"><span data-stu-id="a211a-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="a211a-243">Impostare le seguenti variabili in modo da riflettere lo script e la destinazione desiderati:</span><span class="sxs-lookup"><span data-stu-id="a211a-243">Set the following variables to reflect the desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="to-execute-a-job"></a><span data-ttu-id="a211a-244">Per eseguire un processo</span><span class="sxs-lookup"><span data-stu-id="a211a-244">To execute a job</span></span>
<span data-ttu-id="a211a-245">Questo script di PowerShell esegue un processo esistente:</span><span class="sxs-lookup"><span data-stu-id="a211a-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="a211a-246">Aggiornare la variabile seguente per riflettere il nome del processo desiderato da eseguire:</span><span class="sxs-lookup"><span data-stu-id="a211a-246">Update the following variable to reflect the desired job name to have executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="to-retrieve-the-state-of-a-single-job-execution"></a><span data-ttu-id="a211a-247">Per recuperare lo stato di esecuzione di un singolo processo</span><span class="sxs-lookup"><span data-stu-id="a211a-247">To retrieve the state of a single job execution</span></span>
<span data-ttu-id="a211a-248">Usare il [**cmdlet Get-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) e impostare il parametro **JobExecutionId** per visualizzare lo stato di esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="a211a-248">Use the [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set the **JobExecutionId** parameter to view the state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="a211a-249">Usare lo stesso cmdlet **Get-AzureSqlJobExecution** con il parametro **IncludeChildren** per visualizzare lo stato delle esecuzioni del processo figlio, ovvero lo stato specifico per ogni esecuzione del processo in ogni database di destinazione del processo.</span><span class="sxs-lookup"><span data-stu-id="a211a-249">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="to-view-the-state-across-multiple-job-executions"></a><span data-ttu-id="a211a-250">Per visualizzare lo stato di più esecuzioni del processo</span><span class="sxs-lookup"><span data-stu-id="a211a-250">To view the state across multiple job executions</span></span>
<span data-ttu-id="a211a-251">Il [**cmdlet Get-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/new-azuresqljob) ha più parametri facoltativi che possono essere usati per visualizzare più esecuzioni di processo, filtrate tramite i parametri forniti.</span><span class="sxs-lookup"><span data-stu-id="a211a-251">The [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span></span> <span data-ttu-id="a211a-252">Di seguito vengono illustrati alcuni dei possibili modi per utilizzare Get-AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="a211a-252">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="a211a-253">Recuperare tutte le esecuzioni attive di processo di primo livello:</span><span class="sxs-lookup"><span data-stu-id="a211a-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="a211a-254">Recuperare tutte le esecuzioni di processo di primo livello, incluse le esecuzioni di processo inattive:</span><span class="sxs-lookup"><span data-stu-id="a211a-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="a211a-255">Recuperare tutte le esecuzioni di processo figlio di un ID di esecuzione processo fornito, incluse le esecuzioni di processo inattive:</span><span class="sxs-lookup"><span data-stu-id="a211a-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="a211a-256">Recuperare tutte le esecuzioni di processo create utilizzando una pianificazione / processo di combinazione, inclusi i processi inattivi:</span><span class="sxs-lookup"><span data-stu-id="a211a-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="a211a-257">Recuperare tutti i processi destinati a una mappa di partizione specificata, inclusi i processi inattivi:</span><span class="sxs-lookup"><span data-stu-id="a211a-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="a211a-258">Recuperare tutti i processi destinati a una raccolta personalizzata specificata, inclusi i processi inattivi:</span><span class="sxs-lookup"><span data-stu-id="a211a-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="a211a-259">Recuperare l'elenco delle esecuzioni delle attività di processo in una esecuzione di processo specifica:</span><span class="sxs-lookup"><span data-stu-id="a211a-259">Retrieve the list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="a211a-260">Recuperare i dettagli di esecuzione delle attività di processo:</span><span class="sxs-lookup"><span data-stu-id="a211a-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="a211a-261">Il seguente script PowerShell può essere utilizzato per visualizzare i dettagli di un'esecuzione delle attività di processo, che è particolarmente utile durante il debug degli errori di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a211a-261">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="to-retrieve-failures-within-job-task-executions"></a><span data-ttu-id="a211a-262">Per recuperare gli errori nelle esecuzioni delle attività di processo</span><span class="sxs-lookup"><span data-stu-id="a211a-262">To retrieve failures within job task executions</span></span>
<span data-ttu-id="a211a-263">L'oggetto **JobTaskExecution** include una proprietà per il ciclo di vita dell'attività insieme a una proprietà del messaggio.</span><span class="sxs-lookup"><span data-stu-id="a211a-263">The **JobTaskExecution object** includes a property for the lifecycle of the task along with a message property.</span></span> <span data-ttu-id="a211a-264">Se l'esecuzione di un'attività di processo non riesce, la proprietà del ciclo di vita verrà impostata su *Non riuscita* e la proprietà del messaggio verrà impostata sul messaggio di eccezione risultante e il relativo stack.</span><span class="sxs-lookup"><span data-stu-id="a211a-264">If a job task execution failed, the lifecycle property will be set to *Failed* and the message property will be set to the resulting exception message and its stack.</span></span> <span data-ttu-id="a211a-265">Se un processo ha esito negativo, è importante visualizzare i dettagli delle attività di processo che non sono riuscite per un determinato processo.</span><span class="sxs-lookup"><span data-stu-id="a211a-265">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="to-wait-for-a-job-execution-to-complete"></a><span data-ttu-id="a211a-266">Per attendere il completamento dell'esecuzione del processo</span><span class="sxs-lookup"><span data-stu-id="a211a-266">To wait for a job execution to complete</span></span>
<span data-ttu-id="a211a-267">Il seguente script PowerShell può essere utilizzato per attendere che un’attività di processo venga completata: </span><span class="sxs-lookup"><span data-stu-id="a211a-267">The following PowerShell script can be used to wait for a job task to complete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="a211a-268">Creare un criterio di esecuzione personalizzata</span><span class="sxs-lookup"><span data-stu-id="a211a-268">Create a custom execution policy</span></span>
<span data-ttu-id="a211a-269">I processi di database elastici supportano la creazione di criteri di esecuzione personalizzati che possono essere applicati all'avvio dei processi.</span><span class="sxs-lookup"><span data-stu-id="a211a-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="a211a-270">Criteri di esecuzione che attualmente consentono la definizione di:</span><span class="sxs-lookup"><span data-stu-id="a211a-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="a211a-271">Nome: Identificatore del criterio di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a211a-271">Name: Identifier for the execution policy.</span></span>
* <span data-ttu-id="a211a-272">Timeout del processo: tempo totale prima che un processo venga annullato dai processi di database elastici.</span><span class="sxs-lookup"><span data-stu-id="a211a-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="a211a-273">Intervallo tra tentativi iniziale: intervallo di attesa prima del primo tentativo.</span><span class="sxs-lookup"><span data-stu-id="a211a-273">Initial Retry Interval: Interval to wait before first retry.</span></span>
* <span data-ttu-id="a211a-274">Intervallo massimo di tentativi: estremità degli intervalli tra i tentativi da utilizzare.</span><span class="sxs-lookup"><span data-stu-id="a211a-274">Maximum Retry Interval: Cap of retry intervals to use.</span></span>
* <span data-ttu-id="a211a-275">Coefficiente di backoff dell’intervallo tra tentativi: coefficiente utilizzato per calcolare l’intervallo successivo tra i tentativi.</span><span class="sxs-lookup"><span data-stu-id="a211a-275">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span></span>  <span data-ttu-id="a211a-276">Viene utilizzata la seguente formula: (Intervallo tentativi iniziale) * Math.pow((Coefficiente di backoff dell’intervallo), (Numero di tentativi) - 2).</span><span class="sxs-lookup"><span data-stu-id="a211a-276">The following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="a211a-277">Numero massimo di tentativi: Il numero massimo di tentativi all'interno di un processo.</span><span class="sxs-lookup"><span data-stu-id="a211a-277">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span></span>

<span data-ttu-id="a211a-278">Il criterio di esecuzione predefinito utilizza i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="a211a-278">The default execution policy uses the following values:</span></span>

* <span data-ttu-id="a211a-279">Nome: Criterio di esecuzione predefinito</span><span class="sxs-lookup"><span data-stu-id="a211a-279">Name: Default execution policy</span></span>
* <span data-ttu-id="a211a-280">Timeout del processo: 1 settimana</span><span class="sxs-lookup"><span data-stu-id="a211a-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="a211a-281">Intervallo tra tentativi iniziale: 100 millisecondi</span><span class="sxs-lookup"><span data-stu-id="a211a-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="a211a-282">Intervallo massimo tra tentativi: 30 minuti</span><span class="sxs-lookup"><span data-stu-id="a211a-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="a211a-283">Coefficiente di intervallo tra tentativi: 2</span><span class="sxs-lookup"><span data-stu-id="a211a-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="a211a-284">Numero massimo di tentativi: 2,147,483,647</span><span class="sxs-lookup"><span data-stu-id="a211a-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="a211a-285">Creare il criterio di esecuzione desiderato:</span><span class="sxs-lookup"><span data-stu-id="a211a-285">Create the desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="a211a-286">Aggiornare il criterio di esecuzione personalizzato</span><span class="sxs-lookup"><span data-stu-id="a211a-286">Update a custom execution policy</span></span>
<span data-ttu-id="a211a-287">Aggiornare l'aggiornamento del criterio di esecuzione desiderato:</span><span class="sxs-lookup"><span data-stu-id="a211a-287">Update the desired execution policy to update:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="a211a-288">Annullare un processo</span><span class="sxs-lookup"><span data-stu-id="a211a-288">Cancel a job</span></span>
<span data-ttu-id="a211a-289">I processi di database elastici supportano le richieste di annullamento dei processi.</span><span class="sxs-lookup"><span data-stu-id="a211a-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="a211a-290">Se i processi di database elastici rilevano una richiesta di annullamento per un processo in fase di esecuzione, verrà effettuato un tentativo di arresto del processo.</span><span class="sxs-lookup"><span data-stu-id="a211a-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span></span>

<span data-ttu-id="a211a-291">E’ possibile cancellare un processo in due modi diversi tramite i processi di database elastici:</span><span class="sxs-lookup"><span data-stu-id="a211a-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="a211a-292">Annullare le attività attualmente in esecuzione: se viene rilevato un annullamento mentre un'attività è in esecuzione, l'annullamento verrà eseguito nell'aspetto dell'attività attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a211a-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span></span>  <span data-ttu-id="a211a-293">Ad esempio: se viene eseguita una query con esecuzione prolungata quando si tenta di eseguire un annullamento, si verificherà un tentativo di annullare la query.</span><span class="sxs-lookup"><span data-stu-id="a211a-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span></span>
2. <span data-ttu-id="a211a-294">Annullare i tentativi dell'attività: se viene rilevato un annullamento dal thread di controllo prima che venga avviata un'attività per l'esecuzione, il thread di controllo eviterà di avviare l'attività e dichiarerà annullata la richiesta.</span><span class="sxs-lookup"><span data-stu-id="a211a-294">Canceling task retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span></span>

<span data-ttu-id="a211a-295">Se viene richiesto un annullamento del processo per un processo padre, tale richiesta verrà rispettata per il processo padre e per tutti i relativi processi figlio.</span><span class="sxs-lookup"><span data-stu-id="a211a-295">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span></span>

<span data-ttu-id="a211a-296">Per inviare una richiesta di annullamento, usare il [**cmdlet Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) e impostare il parametro **JobExecutionId**.</span><span class="sxs-lookup"><span data-stu-id="a211a-296">To submit a cancellation request, use the [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set the **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="to-delete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="a211a-297">Per eliminare un processo e la relativa cronologia in modo asincrono</span><span class="sxs-lookup"><span data-stu-id="a211a-297">To delete a job and job history asynchronously</span></span>
<span data-ttu-id="a211a-298">I processi di database elastici supportano l'eliminazione asincrona dei processi.</span><span class="sxs-lookup"><span data-stu-id="a211a-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="a211a-299">Un processo può essere contrassegnato per l'eliminazione e il sistema lo eliminerà con tutta la relativa cronologia dopo il completamento di tutte le esecuzioni di processo per tale processo.</span><span class="sxs-lookup"><span data-stu-id="a211a-299">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span></span> <span data-ttu-id="a211a-300">Il sistema non annullerà automaticamente le esecuzioni di processo attive.</span><span class="sxs-lookup"><span data-stu-id="a211a-300">The system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="a211a-301">Richiamare [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) per annullare le esecuzioni di processo attive.</span><span class="sxs-lookup"><span data-stu-id="a211a-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) to cancel active job executions.</span></span>

<span data-ttu-id="a211a-302">Per attivare l'eliminazione di processi, usare il [**cmdlet Remove-AzureSqlJob**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) e impostare il parametro **JobName**.</span><span class="sxs-lookup"><span data-stu-id="a211a-302">To trigger job deletion, use the [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set the **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="to-create-a-custom-database-target"></a><span data-ttu-id="a211a-303">Per creare una destinazione di database personalizzata</span><span class="sxs-lookup"><span data-stu-id="a211a-303">To create a custom database target</span></span>
<span data-ttu-id="a211a-304">È possibile definire destinazioni di database personalizzate per l'esecuzione diretta o per l'inclusione in un gruppo di database personalizzato.</span><span class="sxs-lookup"><span data-stu-id="a211a-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="a211a-305">Ad esempio, poiché i **pool elastici** non sono ancora supportati direttamente se si usano le API di PowerShell, è possibile creare una destinazione di database personalizzata e una destinazione della raccolta di database personalizzata che comprenda tutti i database nel pool.</span><span class="sxs-lookup"><span data-stu-id="a211a-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all the databases in the pool.</span></span>

<span data-ttu-id="a211a-306">Impostare le seguenti variabili in modo da riflettere le informazioni desiderate sul database:</span><span class="sxs-lookup"><span data-stu-id="a211a-306">Set the following variables to reflect the desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="to-create-a-custom-database-collection-target"></a><span data-ttu-id="a211a-307">Per creare una destinazione per la raccolta di database personalizzata</span><span class="sxs-lookup"><span data-stu-id="a211a-307">To create a custom database collection target</span></span>
<span data-ttu-id="a211a-308">Usare il cmdlet [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) per definire una destinazione per la raccolta di database personalizzata per abilitare l'esecuzione in più destinazioni di database definite.</span><span class="sxs-lookup"><span data-stu-id="a211a-308">Use the [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet to define a custom database collection target to enable execution across multiple defined database targets.</span></span> <span data-ttu-id="a211a-309">Dopo aver creato un gruppo di database, è possibile associarli alla destinazione della raccolta personalizzata.</span><span class="sxs-lookup"><span data-stu-id="a211a-309">After creating a database group, databases can be associated with the custom collection target.</span></span>

<span data-ttu-id="a211a-310">Impostare le seguenti variabili in modo da riflettere la configurazione della destinazione della raccolta personalizzata desiderata:</span><span class="sxs-lookup"><span data-stu-id="a211a-310">Set the following variables to reflect the desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="to-add-databases-to-a-custom-database-collection-target"></a><span data-ttu-id="a211a-311">Per aggiungere database a una destinazione della raccolta di database personalizzata</span><span class="sxs-lookup"><span data-stu-id="a211a-311">To add databases to a custom database collection target</span></span>
<span data-ttu-id="a211a-312">Per aggiungere un database a una raccolta personalizzata specifica, usare il cmdlet [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget).</span><span class="sxs-lookup"><span data-stu-id="a211a-312">To add a database to a specific custom collection use the [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-the-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="a211a-313">Verificare i database in una destinazione per la raccolta dei database personalizzata</span><span class="sxs-lookup"><span data-stu-id="a211a-313">Review the databases within a custom database collection target</span></span>
<span data-ttu-id="a211a-314">Usare il cmdlet [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) per recuperare i database figlio all'interno di una destinazione di una raccolta database personalizzata.</span><span class="sxs-lookup"><span data-stu-id="a211a-314">Use the [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet to retrieve the child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-to-execute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="a211a-315">Creare un processo per eseguire uno script in una destinazione di una raccolta database personalizzata</span><span class="sxs-lookup"><span data-stu-id="a211a-315">Create a job to execute a script across a custom database collection target</span></span>
<span data-ttu-id="a211a-316">Usare il cmdlet [**New AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) per creare un processo rispetto a un gruppo di database definiti da una destinazione della raccolta di database personalizzata.</span><span class="sxs-lookup"><span data-stu-id="a211a-316">Use the [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet to create a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="a211a-317">I processi di database elastici espanderanno il processo in più processi figlio, ognuno corrispondente a un database associato alla destinazione di raccolta database personalizzata e eseguiranno lo script in tutti i database.</span><span class="sxs-lookup"><span data-stu-id="a211a-317">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span></span> <span data-ttu-id="a211a-318">Anche in questo caso, è importante che gli script siano idempotenti per essere flessibili ai tentativi.</span><span class="sxs-lookup"><span data-stu-id="a211a-318">Again, it is important that scripts are idempotent to be resilient to retries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="a211a-319">Raccolta dei dati tra database</span><span class="sxs-lookup"><span data-stu-id="a211a-319">Data collection across databases</span></span>
<span data-ttu-id="a211a-320">È possibile usare un processo per eseguire una query su un gruppo di database e inviare i risultati a una tabella specifica.</span><span class="sxs-lookup"><span data-stu-id="a211a-320">You can use a job to execute a query across a group of databases and send the results to a specific table.</span></span> <span data-ttu-id="a211a-321">E’ possibile eseguire una query sulla tabella dopo aver visualizzato i risultati della query da ciascun database.</span><span class="sxs-lookup"><span data-stu-id="a211a-321">The table can be queried after the fact to see the query’s results from each database.</span></span> <span data-ttu-id="a211a-322">In questo modo si avrà un metodo asincrono per eseguire una query su molti database.</span><span class="sxs-lookup"><span data-stu-id="a211a-322">This provides an asynchronous method to execute a query across many databases.</span></span> <span data-ttu-id="a211a-323">I tentativi non riusciti vengono gestiti automaticamente tramite la ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="a211a-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="a211a-324">La tabella di destinazione specificata verrà creata automaticamente, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="a211a-324">The specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="a211a-325">La nuova tabella corrisponde allo schema del set di risultati restituito.</span><span class="sxs-lookup"><span data-stu-id="a211a-325">The new table matches the schema of the returned result set.</span></span> <span data-ttu-id="a211a-326">Se uno script restituisce più set di risultati, i processi di database elastici invieranno solo il primo set alla tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a211a-326">If a script returns multiple result sets, Elastic Database jobs will only send the first to the destination table.</span></span>

<span data-ttu-id="a211a-327">Lo script di PowerShell seguente esegue uno script e raccoglie i risultati in una tabella specificata.</span><span class="sxs-lookup"><span data-stu-id="a211a-327">The following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="a211a-328">Questo script presuppone che sia stato creato uno script T-SQL che restituisce un singolo set di risultati e che sia stata creata una destinazione della raccolta di database personalizzata.</span><span class="sxs-lookup"><span data-stu-id="a211a-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="a211a-329">Questo script usa il cmdlet [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget).</span><span class="sxs-lookup"><span data-stu-id="a211a-329">This script uses the [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="a211a-330">Impostare i parametri per lo script, le credenziali e la destinazione di esecuzione:</span><span class="sxs-lookup"><span data-stu-id="a211a-330">Set the parameters for script, credentials, and execution target:</span></span>

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

### <a name="to-create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="a211a-331">Per creare e avviare un processo per gli scenari di raccolta dati</span><span class="sxs-lookup"><span data-stu-id="a211a-331">To create and start a job for data collection scenarios</span></span>
<span data-ttu-id="a211a-332">Questo script usa il cmdlet [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution).</span><span class="sxs-lookup"><span data-stu-id="a211a-332">This script uses the [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

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

## <a name="to-schedule-a-job-execution-trigger"></a><span data-ttu-id="a211a-333">Per pianificare un trigger di esecuzione del processo</span><span class="sxs-lookup"><span data-stu-id="a211a-333">To schedule a job execution trigger</span></span>
<span data-ttu-id="a211a-334">Lo script di PowerShell seguente può essere usato per creare una pianificazione ricorrente.</span><span class="sxs-lookup"><span data-stu-id="a211a-334">The following PowerShell script can be used to create a recurring schedule.</span></span> <span data-ttu-id="a211a-335">Questo script usa l'intervallo di minuti, ma [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) supporta anche i parametri -DayInterval, -HourInterval, -MonthInterval e -WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="a211a-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="a211a-336">Le pianificazioni che vengono eseguite una sola volta possono essere create specificando -OneTime.</span><span class="sxs-lookup"><span data-stu-id="a211a-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="a211a-337">Creare una nuova pianificazione:</span><span class="sxs-lookup"><span data-stu-id="a211a-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="to-trigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="a211a-338">Per attivare l'esecuzione di un processo in una pianificazione temporale</span><span class="sxs-lookup"><span data-stu-id="a211a-338">To trigger a job executed on a time schedule</span></span>
<span data-ttu-id="a211a-339">È possibile definire un trigger di processo per eseguire un processo in base a una pianificazione temporale.</span><span class="sxs-lookup"><span data-stu-id="a211a-339">A job trigger can be defined to have a job executed according to a time schedule.</span></span> <span data-ttu-id="a211a-340">Il seguente script di PowerShell può essere utilizzato per creare un trigger di processo.</span><span class="sxs-lookup"><span data-stu-id="a211a-340">The following PowerShell script can be used to create a job trigger.</span></span>

<span data-ttu-id="a211a-341">Usare [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) e impostare le variabili seguenti in modo che corrispondano al processo e alla pianificazione desiderati:</span><span class="sxs-lookup"><span data-stu-id="a211a-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set the following variables to correspond to the desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="to-remove-a-scheduled-association-to-stop-job-from-executing-on-schedule"></a><span data-ttu-id="a211a-342">Per rimuovere un'associazione pianificata per arrestare l'esecuzione di un processo in base a una pianificazione</span><span class="sxs-lookup"><span data-stu-id="a211a-342">To remove a scheduled association to stop job from executing on schedule</span></span>
<span data-ttu-id="a211a-343">Per sospendere l'esecuzione del processo ricorrente tramite un trigger di processo, è possibile rimuovere il trigger di processo.</span><span class="sxs-lookup"><span data-stu-id="a211a-343">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span></span> <span data-ttu-id="a211a-344">Rimuovere un trigger di processo per arrestare l'esecuzione di un processo in base a una pianificazione mediante il [**cmdlet Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span><span class="sxs-lookup"><span data-stu-id="a211a-344">Remove a job trigger to stop a job from being executed according to a schedule using the [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-to-a-time-schedule"></a><span data-ttu-id="a211a-345">Recuperare i trigger di processo associati a una pianificazione temporale</span><span class="sxs-lookup"><span data-stu-id="a211a-345">Retrieve job triggers bound to a time schedule</span></span>
<span data-ttu-id="a211a-346">Il seguente script PowerShell è utilizzabile per ottenere e visualizzare i trigger di processo registrati in una particolare pianificazione temporale.</span><span class="sxs-lookup"><span data-stu-id="a211a-346">The following PowerShell script can be used to obtain and display the job triggers registered to a particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="to-retrieve-job-triggers-bound-to-a-job"></a><span data-ttu-id="a211a-347">Per recuperare i trigger di processo associati a un processo</span><span class="sxs-lookup"><span data-stu-id="a211a-347">To retrieve job triggers bound to a job</span></span>
<span data-ttu-id="a211a-348">Usare [Get AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) per ottenere e visualizzare le pianificazioni che contengono un processo registrato.</span><span class="sxs-lookup"><span data-stu-id="a211a-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) to obtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="to-create-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="a211a-349">Per creare un'applicazione livello dati (DACPAC) per l'esecuzione sui database</span><span class="sxs-lookup"><span data-stu-id="a211a-349">To create a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="a211a-350">Per creare un'applicazione DACPAC, vedere [Applicazioni livello dati](https://msdn.microsoft.com/library/ee210546.aspx).</span><span class="sxs-lookup"><span data-stu-id="a211a-350">To create a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="a211a-351">Per distribuire un'applicazione DACPAC, usare il [cmdlet New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span><span class="sxs-lookup"><span data-stu-id="a211a-351">To deploy a DACPAC, use the [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="a211a-352">L'applicazione DACPAC deve essere accessibile al servizio.</span><span class="sxs-lookup"><span data-stu-id="a211a-352">The DACPAC must be accessible to the service.</span></span> <span data-ttu-id="a211a-353">È consigliabile caricare nell'archiviazione di Azure un'applicazione DACPAC creata e creare una [Firma di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) per DACPAC.</span><span class="sxs-lookup"><span data-stu-id="a211a-353">It is recommended to upload a created DACPAC to Azure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for the DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="to-update-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="a211a-354">Per aggiornare un'applicazione livello dati (DACPAC) per l'esecuzione nei database</span><span class="sxs-lookup"><span data-stu-id="a211a-354">To update a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="a211a-355">I DACPAC esistenti registrati all’interno dei processi di database elastici possono essere aggiornati in modo da fare riferimento ai nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="a211a-355">Existing DACPACs registered within Elastic Database Jobs can be updated to point to new URIs.</span></span> <span data-ttu-id="a211a-356">Usare il [**cmdlet Set-AzureSqlJobContentDefinition**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) per aggiornare l'URI DACPAC in una DACPAC registrata esistente:</span><span class="sxs-lookup"><span data-stu-id="a211a-356">Use the [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) to update the DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="to-create-a-job-to-apply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="a211a-357">Per creare un processo per applicare un'applicazione livello dati (DACPAC) nei database</span><span class="sxs-lookup"><span data-stu-id="a211a-357">To create a job to apply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="a211a-358">Dopo aver creato un DACPAC all'interno di processi di database elastici, è possibile creare un processo per applicare il DACPAC su un gruppo di database.</span><span class="sxs-lookup"><span data-stu-id="a211a-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created to apply the DACPAC across a group of databases.</span></span> <span data-ttu-id="a211a-359">Utilizzare il seguente script di PowerShell per creare un processo DACPAC su una raccolta personalizzata di database:</span><span class="sxs-lookup"><span data-stu-id="a211a-359">The following PowerShell script can be used to create a DACPAC job across a custom collection of databases:</span></span>

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
