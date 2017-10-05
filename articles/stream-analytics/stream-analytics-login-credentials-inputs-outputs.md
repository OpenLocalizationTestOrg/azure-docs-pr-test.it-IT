---
title: 'Analisi di flusso: Ruotare le credenziali di accesso per input e output | Documentazione Microsoft'
description: Informazioni su come aggiornare le credenziali di input e output di Analisi dei flussi.
keywords: credenziali di accesso
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 2cb995a3969a8cb025f371ed0ab160cd04b0454d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="20d16-104">Ruotare le credenziali di accesso per input e output nei processi di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="20d16-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="20d16-105">Sunto</span><span class="sxs-lookup"><span data-stu-id="20d16-105">Abstract</span></span>
<span data-ttu-id="20d16-106">Analisi dei flussi di Azure, al momento, non consente di sostituire le credenziali su input/output durante l’esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="20d16-106">Azure Stream Analytics today doesn’t allow replacing the credentials on an input/output while the job is running.</span></span>

<span data-ttu-id="20d16-107">Nonostante Analisi di flusso di Azure supporti la ripresa di un processo dall’ultimo output, abbiamo voluto condividere l’intero processo per ridurre l’intervallo fra l’arresto e l’avvio del processo e la rotazione delle credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="20d16-107">While Azure Stream Analytics does support resuming a job from last output, we wanted to share the entire process for minimizing the lag between the stopping and starting of the job and rotating the login credentials.</span></span>

## <a name="part-1---prepare-the-new-set-of-credentials"></a><span data-ttu-id="20d16-108">Parte 1 - Preparare il nuovo set di credenziali:</span><span class="sxs-lookup"><span data-stu-id="20d16-108">Part 1 - Prepare the new set of credentials:</span></span>
<span data-ttu-id="20d16-109">Questa parte è applicabile ai seguenti input/output:</span><span class="sxs-lookup"><span data-stu-id="20d16-109">This part is applicable to the following inputs/outputs:</span></span>

* <span data-ttu-id="20d16-110">Archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="20d16-110">Blob Storage</span></span>
* <span data-ttu-id="20d16-111">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="20d16-111">Event Hubs</span></span>
* <span data-ttu-id="20d16-112">Database SQL</span><span class="sxs-lookup"><span data-stu-id="20d16-112">SQL Database</span></span>
* <span data-ttu-id="20d16-113">Archiviazione tabelle</span><span class="sxs-lookup"><span data-stu-id="20d16-113">Table Storage</span></span>

<span data-ttu-id="20d16-114">Per altri input/output, andare alla Parte 2.</span><span class="sxs-lookup"><span data-stu-id="20d16-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="20d16-115">Archiviazione BLOB/Archiviazione tabelle</span><span class="sxs-lookup"><span data-stu-id="20d16-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="20d16-116">Andare all'estensione di Archiviazione nel portale di gestione di Azure: </span><span class="sxs-lookup"><span data-stu-id="20d16-116">Go to the Storage extention on the Azure Management portal:</span></span>  
   ![graphic1][graphic1]
2. <span data-ttu-id="20d16-118">Individuare l’archiviazione usata dal processo e accedervi: </span><span class="sxs-lookup"><span data-stu-id="20d16-118">Locate the storage used by your job and go into it:</span></span>  
   ![graphic2][graphic2]
3. <span data-ttu-id="20d16-120">Fare clic sul comando Gestisci chiavi di accesso: </span><span class="sxs-lookup"><span data-stu-id="20d16-120">Click the Manage Access Keys command:</span></span>  
   ![graphic3][graphic3]
4. <span data-ttu-id="20d16-122">Tra la chiave di accesso primaria e la chiave di accesso secondaria, **selezionare quella non usata dal processo**.</span><span class="sxs-lookup"><span data-stu-id="20d16-122">Between the Primary Access Key and the Secondary Access Key, **pick the one not used by your job**.</span></span>
5. <span data-ttu-id="20d16-123">Premere l’opzione di rigenerazione: </span><span class="sxs-lookup"><span data-stu-id="20d16-123">Hit regenerate:</span></span>  
   ![graphic4][graphic4]
6. <span data-ttu-id="20d16-125">Copiare la chiave appena generata: </span><span class="sxs-lookup"><span data-stu-id="20d16-125">Copy the newly generated key:</span></span>  
   ![graphic5][graphic5]
7. <span data-ttu-id="20d16-127">Continuare con la Parte 2.</span><span class="sxs-lookup"><span data-stu-id="20d16-127">Continue to Part 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="20d16-128">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="20d16-128">Event hubs</span></span>
1. <span data-ttu-id="20d16-129">Andare all'estensione del bus di servizio sul portale di gestione di Azure: </span><span class="sxs-lookup"><span data-stu-id="20d16-129">Go to the Service Bus extension on the Azure Management portal:</span></span>  
   ![graphic6][graphic6]
2. <span data-ttu-id="20d16-131">Individuare lo spazio dei nomi del bus di servizio usato dal processo e accedervi: </span><span class="sxs-lookup"><span data-stu-id="20d16-131">Locate the Service Bus Namespace used by your job and go into it:</span></span>  
   ![graphic7][graphic7]
3. <span data-ttu-id="20d16-133">Se il processo usa criteri di accesso condivisi sullo spazio dei nomi del bus di servizio, saltare al passaggio 6</span><span class="sxs-lookup"><span data-stu-id="20d16-133">If your job uses a shared access policy on the Service Bus Namespace, jump to step 6</span></span>  
4. <span data-ttu-id="20d16-134">Andare alla scheda Hub eventi: </span><span class="sxs-lookup"><span data-stu-id="20d16-134">Go to the Event Hubs tab:</span></span>  
   ![graphic8][graphic8]
5. <span data-ttu-id="20d16-136">Individuare l’hub eventi usato dal processo e accedervi: </span><span class="sxs-lookup"><span data-stu-id="20d16-136">Locate the Event Hub used by your job and go into it:</span></span>  
   ![graphic9][graphic9]
6. <span data-ttu-id="20d16-138">Andare alla scheda Configura: </span><span class="sxs-lookup"><span data-stu-id="20d16-138">Go to the Configure Tab:</span></span>  
   ![graphic10][graphic10]
7. <span data-ttu-id="20d16-140">Nell’elenco a discesa Nome criteri, individuare i criteri di accesso condivisi usati dal processo: </span><span class="sxs-lookup"><span data-stu-id="20d16-140">On the Policy Name drop-down, locate the shared access policy used by your job:</span></span>  
   ![graphic11][graphic11]
8. <span data-ttu-id="20d16-142">Tra la chiave primaria e la chiave secondaria, **selezionare quella non usata dal processo**.</span><span class="sxs-lookup"><span data-stu-id="20d16-142">Between the Primary Key and the Secondary Key, **pick the one not used by your job**.</span></span>  
9. <span data-ttu-id="20d16-143">Premere l’opzione di rigenerazione: </span><span class="sxs-lookup"><span data-stu-id="20d16-143">Hit regenerate:</span></span>  
   ![graphic12][graphic12]
10. <span data-ttu-id="20d16-145">Copiare la chiave appena generata: </span><span class="sxs-lookup"><span data-stu-id="20d16-145">Copy the newly generated key:</span></span>  
   ![graphic13][graphic13]
11. <span data-ttu-id="20d16-147">Continuare con la Parte 2.</span><span class="sxs-lookup"><span data-stu-id="20d16-147">Continue to Part 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="20d16-148">Database SQL</span><span class="sxs-lookup"><span data-stu-id="20d16-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="20d16-149">Nota: sarà necessario connettersi al servizio Database SQL.</span><span class="sxs-lookup"><span data-stu-id="20d16-149">Note: you will need to connect to the SQL Database Service.</span></span> <span data-ttu-id="20d16-150">Verrà mostrato come eseguire l'operazione usando lo strumento di gestione sul portale di gestione di Azure. Tuttavia, è anche possibile scegliere uno strumento sul lato client come SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="20d16-150">We are going to show how to do this using the management experience on the Azure Management portal but you may choose to use some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="20d16-151">Andare all'estensione del database SQL sul portale di gestione di Azure: </span><span class="sxs-lookup"><span data-stu-id="20d16-151">Go to the SQL Databases extension on the Azure Management portal:</span></span>  
   ![graphic14][graphic14]
2. <span data-ttu-id="20d16-153">Individuare il database SQL usato dal processo e **fare clic sul collegamento al server** sulla stessa riga:</span><span class="sxs-lookup"><span data-stu-id="20d16-153">Locate the SQL Database used by your job and **click on the server** link on the same line:</span></span>  
   <span data-ttu-id="20d16-154">![graphic15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="20d16-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="20d16-155">Fare clic sul comando Gestisci: </span><span class="sxs-lookup"><span data-stu-id="20d16-155">Click the Manage command:</span></span>  
   ![graphic16][graphic16]
4. <span data-ttu-id="20d16-157">Digitare master del database: </span><span class="sxs-lookup"><span data-stu-id="20d16-157">Type Database Master:</span></span>  
   ![graphic17][graphic17]
5. <span data-ttu-id="20d16-159">Immettere il nome utente, la password e fare clic su Accedi: </span><span class="sxs-lookup"><span data-stu-id="20d16-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![graphic18][graphic18]
6. <span data-ttu-id="20d16-161">Fare clic su Nuova query: </span><span class="sxs-lookup"><span data-stu-id="20d16-161">Click New Query:</span></span>  
   ![graphic19][graphic19]
7. <span data-ttu-id="20d16-163">Immettere la query seguente sostituendo <login_name> con il nome utente e sostituendo <enterStrongPasswordHere> con la nuova password:</span><span class="sxs-lookup"><span data-stu-id="20d16-163">Type in the following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="20d16-164">Fare clic su Esegui: </span><span class="sxs-lookup"><span data-stu-id="20d16-164">Click Run:</span></span>  
   ![graphic20][graphic20]
9. <span data-ttu-id="20d16-166">Tornare al passaggio 2 e, questa volta, fare clic sul database: </span><span class="sxs-lookup"><span data-stu-id="20d16-166">Go back to step 2 and this time click the database:</span></span>  
   ![graphic21][graphic21]
10. <span data-ttu-id="20d16-168">Fare clic sul comando Gestisci: </span><span class="sxs-lookup"><span data-stu-id="20d16-168">Click the Manage command:</span></span>  
   ![graphic22][graphic22]
11. <span data-ttu-id="20d16-170">Digitare il nome utente, la password e fare clic su Accedi: </span><span class="sxs-lookup"><span data-stu-id="20d16-170">type in your User Name, Password, and click Logon:</span></span>  
   ![graphic23][graphic23]
12. <span data-ttu-id="20d16-172">Fare clic su Nuova query: </span><span class="sxs-lookup"><span data-stu-id="20d16-172">Click New Query:</span></span>  
   ![graphic24][graphic24]
13. <span data-ttu-id="20d16-174">Immettere la query seguente sostituendo <user_name> con il nome con cui identificare l'accesso nel contesto di questo database (è possibile indicare lo stesso valore assegnato per <login_name>, ad esempio) e sostituendo <login_name> con il nuovo nome utente:</span><span class="sxs-lookup"><span data-stu-id="20d16-174">Type in the following query replacing <user_name> with a name by which you want to identify this login in the context of this database (you can provide the same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="20d16-175">Fare clic su Esegui: </span><span class="sxs-lookup"><span data-stu-id="20d16-175">Click Run:</span></span>  
   ![graphic25][graphic25]
15. <span data-ttu-id="20d16-177">A questo punto è necessario assegnare al nuovo utente gli stessi ruoli e privilegi che aveva l'utente originale.</span><span class="sxs-lookup"><span data-stu-id="20d16-177">You should now provide your new user with the same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="20d16-178">Continuare con la Parte 2.</span><span class="sxs-lookup"><span data-stu-id="20d16-178">Continue to Part 2.</span></span>

## <a name="part-2-stopping-the-stream-analytics-job"></a><span data-ttu-id="20d16-179">Parte 2: arresto del processo di Analisi dei flussi</span><span class="sxs-lookup"><span data-stu-id="20d16-179">Part 2: Stopping the Stream Analytics Job</span></span>
1. <span data-ttu-id="20d16-180">Andare all'estensione di Analisi di flusso sul portale di gestione di Azure: </span><span class="sxs-lookup"><span data-stu-id="20d16-180">Go to the Stream Analytics extension on the Azure Management portal:</span></span>  
   ![graphic26][graphic26]
2. <span data-ttu-id="20d16-182">Individuare il processo e accedervi: </span><span class="sxs-lookup"><span data-stu-id="20d16-182">Locate your job and go into it:</span></span>  
   ![graphic27][graphic27]
3. <span data-ttu-id="20d16-184">Andare nella scheda Input o nella scheda Output a seconda se si stanno ruotando le credenziali su un Input o su un Output.</span><span class="sxs-lookup"><span data-stu-id="20d16-184">Go to the Inputs tab or the Outputs tab based on whether you are rotating the credentials on an Input or on an Output.</span></span>  
   ![graphic28][graphic28]
4. <span data-ttu-id="20d16-186">Fare clic sul comando Arresta e confermare l’arresto del processo: </span><span class="sxs-lookup"><span data-stu-id="20d16-186">Click the Stop command and confirm the job has stopped:</span></span>  
   <span data-ttu-id="20d16-187">![graphic29][graphic29] Attendere l'arresto del processo.</span><span class="sxs-lookup"><span data-stu-id="20d16-187">![graphic29][graphic29] Wait for the job to stop.</span></span>
5. <span data-ttu-id="20d16-188">Individuare l’input/output su cui ruotare le credenziali e accedervi: </span><span class="sxs-lookup"><span data-stu-id="20d16-188">Locate the input/output you want to rotate credentials on and go into it:</span></span>  
   ![graphic30][graphic30]
6. <span data-ttu-id="20d16-190">Andare alla Parte 3.</span><span class="sxs-lookup"><span data-stu-id="20d16-190">Proceed to Part 3.</span></span>

## <a name="part-3-editing-the-credentials-on-the-stream-analytics-job"></a><span data-ttu-id="20d16-191">Parte 3: modifica delle credenziali sul processo di Analisi dei flussi</span><span class="sxs-lookup"><span data-stu-id="20d16-191">Part 3: Editing the credentials on the Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="20d16-192">Archiviazione BLOB/Archiviazione tabelle</span><span class="sxs-lookup"><span data-stu-id="20d16-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="20d16-193">Individuare il campo Chiave dell'account di archiviazione e incollarvi la chiave appena generata: </span><span class="sxs-lookup"><span data-stu-id="20d16-193">Find the Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![graphic31][graphic31]
2. <span data-ttu-id="20d16-195">Fare clic sul comando Salva e confermare il salvataggio delle modifiche: </span><span class="sxs-lookup"><span data-stu-id="20d16-195">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic32][graphic32]
3. <span data-ttu-id="20d16-197">Al salvataggio delle modifiche, verrà automaticamente avviato un test di connessione. Assicurarsi che abbia esito positivo.</span><span class="sxs-lookup"><span data-stu-id="20d16-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="20d16-198">Andare alla Parte 4.</span><span class="sxs-lookup"><span data-stu-id="20d16-198">Proceed to Part 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="20d16-199">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="20d16-199">Event hubs</span></span>
1. <span data-ttu-id="20d16-200">Individuare il campo Chiave di criterio dell’hub eventi e incollarvi la chiave appena generata: </span><span class="sxs-lookup"><span data-stu-id="20d16-200">Find the Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![graphic33][graphic33]
2. <span data-ttu-id="20d16-202">Fare clic sul comando Salva e confermare il salvataggio delle modifiche: </span><span class="sxs-lookup"><span data-stu-id="20d16-202">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic34][graphic34]
3. <span data-ttu-id="20d16-204">Al salvataggio delle modifiche, verrà automaticamente avviato un test di connessione. Assicurarsi che abbia esito positivo.</span><span class="sxs-lookup"><span data-stu-id="20d16-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="20d16-205">Andare alla Parte 4.</span><span class="sxs-lookup"><span data-stu-id="20d16-205">Proceed to Part 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="20d16-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="20d16-206">Power BI</span></span>
1. <span data-ttu-id="20d16-207">Fare clic su Rinnova autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="20d16-207">Click the Renew authorization:</span></span>  

   ![graphic35][graphic35]
2. <span data-ttu-id="20d16-209">Si otterrà la conferma seguente:</span><span class="sxs-lookup"><span data-stu-id="20d16-209">You will get the following confirmation:</span></span>  

   ![graphic36][graphic36]
3. <span data-ttu-id="20d16-211">Fare clic sul comando Salva e confermare il salvataggio delle modifiche: </span><span class="sxs-lookup"><span data-stu-id="20d16-211">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic37][graphic37]
4. <span data-ttu-id="20d16-213">Al salvataggio delle modifiche, verrà automaticamente avviato un test di connessione. Assicurarsi che abbia esito positivo.</span><span class="sxs-lookup"><span data-stu-id="20d16-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="20d16-214">Andare alla Parte 4.</span><span class="sxs-lookup"><span data-stu-id="20d16-214">Proceed to Part 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="20d16-215">Database SQL</span><span class="sxs-lookup"><span data-stu-id="20d16-215">SQL Database</span></span>
1. <span data-ttu-id="20d16-216">Individuare i campi Nome utente e Password e incollarvi il set di credenziali appena create: </span><span class="sxs-lookup"><span data-stu-id="20d16-216">Find the User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![graphic38][graphic38]
2. <span data-ttu-id="20d16-218">Fare clic sul comando Salva e confermare il salvataggio delle modifiche: </span><span class="sxs-lookup"><span data-stu-id="20d16-218">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic39][graphic39]
3. <span data-ttu-id="20d16-220">Al salvataggio delle modifiche, verrà automaticamente avviato un test di connessione. Assicurarsi che abbia esito positivo.</span><span class="sxs-lookup"><span data-stu-id="20d16-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="20d16-221">Andare alla Parte 4.</span><span class="sxs-lookup"><span data-stu-id="20d16-221">Proceed to Part 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="20d16-222">Parte 4: avvio del processo dall’ora dell’ultimo arresto</span><span class="sxs-lookup"><span data-stu-id="20d16-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="20d16-223">Uscire da Input/Output: </span><span class="sxs-lookup"><span data-stu-id="20d16-223">Navigate away from the Input/Output:</span></span>  
   ![graphic40][graphic40]
2. <span data-ttu-id="20d16-225">Fare clic sul comando di avvio: </span><span class="sxs-lookup"><span data-stu-id="20d16-225">Click the Start command:</span></span>  
   ![graphic41][graphic41]
3. <span data-ttu-id="20d16-227">Selezionare l’ora dell’ultimo arresto e fare clic su OK: </span><span class="sxs-lookup"><span data-stu-id="20d16-227">Pick the Last Stopped Time and click OK:</span></span>  
   ![graphic42][graphic42]
4. <span data-ttu-id="20d16-229">Andare alla Parte 5.</span><span class="sxs-lookup"><span data-stu-id="20d16-229">Proceed to Part 5.</span></span>  

## <a name="part-5-removing-the-old-set-of-credentials"></a><span data-ttu-id="20d16-230">Parte 5: rimozione del set di credenziali precedente</span><span class="sxs-lookup"><span data-stu-id="20d16-230">Part 5: Removing the old set of credentials</span></span>
<span data-ttu-id="20d16-231">Questa parte è applicabile ai seguenti input/output:</span><span class="sxs-lookup"><span data-stu-id="20d16-231">This part is applicable to the following inputs/outputs:</span></span>

* <span data-ttu-id="20d16-232">Archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="20d16-232">Blob Storage</span></span>
* <span data-ttu-id="20d16-233">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="20d16-233">Event Hubs</span></span>
* <span data-ttu-id="20d16-234">Database SQL</span><span class="sxs-lookup"><span data-stu-id="20d16-234">SQL Database</span></span>
* <span data-ttu-id="20d16-235">Archiviazione tabelle</span><span class="sxs-lookup"><span data-stu-id="20d16-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="20d16-236">Archiviazione BLOB/Archiviazione tabelle</span><span class="sxs-lookup"><span data-stu-id="20d16-236">Blob storage/Table storage</span></span>
<span data-ttu-id="20d16-237">Ripetere la Parte 1 per la chiave di accesso usata in precedenza dal processo per rinnovare la chiave di accesso ora inutilizzata.</span><span class="sxs-lookup"><span data-stu-id="20d16-237">Repeat Part 1 for the Access Key that was previously used by your job to renew the now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="20d16-238">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="20d16-238">Event hubs</span></span>
<span data-ttu-id="20d16-239">Ripetere la Parte 1 per la chiave usata in precedenza dal processo per rinnovare la chiave ora inutilizzata.</span><span class="sxs-lookup"><span data-stu-id="20d16-239">Repeat Part 1 for the Key that was previously used by your job to renew the now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="20d16-240">Database SQL</span><span class="sxs-lookup"><span data-stu-id="20d16-240">SQL Database</span></span>
1. <span data-ttu-id="20d16-241">Tornare alla finestra delle query dalla Parte 1 Passaggio 7 e immettere la query seguente, sostituendo <previous_login_name> con il nome utente usato in precedenza dal processo:</span><span class="sxs-lookup"><span data-stu-id="20d16-241">Go back to the query window from Part 1 Step 7 and type in the following query, replacing <previous_login_name> with the User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="20d16-242">Fare clic su Esegui: </span><span class="sxs-lookup"><span data-stu-id="20d16-242">Click Run:</span></span>  
   ![graphic43][graphic43]  

<span data-ttu-id="20d16-244">Si dovrebbe ottenere la conferma seguente:</span><span class="sxs-lookup"><span data-stu-id="20d16-244">You should get the following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="20d16-245">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="20d16-245">Get help</span></span>
<span data-ttu-id="20d16-246">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="20d16-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="20d16-247">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="20d16-247">Next steps</span></span>
* [<span data-ttu-id="20d16-248">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="20d16-248">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="20d16-249">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="20d16-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="20d16-250">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="20d16-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="20d16-251">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="20d16-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="20d16-252">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="20d16-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png

