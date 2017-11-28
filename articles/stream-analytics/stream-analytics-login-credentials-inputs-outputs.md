---
title: 'Analisi di flusso: Ruotare le credenziali di accesso per input e output | Documentazione Microsoft'
description: Informazioni su come hello tooupdate le credenziali per l'output e input flusso Analitica.
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
ms.openlocfilehash: ac2374c539012b66ab390656c5750024e02f6bdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="4be78-104">Ruotare le credenziali di accesso per input e output nei processi di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="4be78-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="4be78-105">Sunto</span><span class="sxs-lookup"><span data-stu-id="4be78-105">Abstract</span></span>
<span data-ttu-id="4be78-106">Analitica di flusso di Azure attualmente non consente sostituendo le credenziali di hello su un input/output durante il processo di hello è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4be78-106">Azure Stream Analytics today doesn’t allow replacing hello credentials on an input/output while hello job is running.</span></span>

<span data-ttu-id="4be78-107">Mentre Analitica di flusso di Azure supporta la ripresa di un processo dall'ultimo output, Desideravamo intero processo di hello tooshare per ridurre al minimo ritardo hello tra hello l'arresto e avvio del processo di hello e la rotazione di credenziali di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="4be78-107">While Azure Stream Analytics does support resuming a job from last output, we wanted tooshare hello entire process for minimizing hello lag between hello stopping and starting of hello job and rotating hello login credentials.</span></span>

## <a name="part-1---prepare-hello-new-set-of-credentials"></a><span data-ttu-id="4be78-108">Parte 1: preparare nuovo set di credenziali di hello:</span><span class="sxs-lookup"><span data-stu-id="4be78-108">Part 1 - Prepare hello new set of credentials:</span></span>
<span data-ttu-id="4be78-109">Questa parte è applicabile toohello degli input/output seguente:</span><span class="sxs-lookup"><span data-stu-id="4be78-109">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="4be78-110">Archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="4be78-110">Blob Storage</span></span>
* <span data-ttu-id="4be78-111">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="4be78-111">Event Hubs</span></span>
* <span data-ttu-id="4be78-112">Database SQL</span><span class="sxs-lookup"><span data-stu-id="4be78-112">SQL Database</span></span>
* <span data-ttu-id="4be78-113">Archiviazione tabelle</span><span class="sxs-lookup"><span data-stu-id="4be78-113">Table Storage</span></span>

<span data-ttu-id="4be78-114">Per altri input/output, andare alla Parte 2.</span><span class="sxs-lookup"><span data-stu-id="4be78-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="4be78-115">Archiviazione BLOB/Archiviazione tabelle</span><span class="sxs-lookup"><span data-stu-id="4be78-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="4be78-116">Visitare toohello dell'estensione di archiviazione nel portale di gestione di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="4be78-116">Go toohello Storage extention on hello Azure Management portal:</span></span>  
   ![graphic1][graphic1]
2. <span data-ttu-id="4be78-118">Individuare utilizzato dal processo di archiviazione di hello e passare al suo interno:</span><span class="sxs-lookup"><span data-stu-id="4be78-118">Locate hello storage used by your job and go into it:</span></span>  
   ![graphic2][graphic2]
3. <span data-ttu-id="4be78-120">Fare clic sul comando Gestisci chiavi di accesso hello:</span><span class="sxs-lookup"><span data-stu-id="4be78-120">Click hello Manage Access Keys command:</span></span>  
   ![graphic3][graphic3]
4. <span data-ttu-id="4be78-122">Tra hello chiave di accesso primaria e chiave di accesso secondaria, hello **pick hello non utilizzato dal processo di**.</span><span class="sxs-lookup"><span data-stu-id="4be78-122">Between hello Primary Access Key and hello Secondary Access Key, **pick hello one not used by your job**.</span></span>
5. <span data-ttu-id="4be78-123">Premere l’opzione di rigenerazione: </span><span class="sxs-lookup"><span data-stu-id="4be78-123">Hit regenerate:</span></span>  
   ![graphic4][graphic4]
6. <span data-ttu-id="4be78-125">Copiare la chiave hello appena generato:</span><span class="sxs-lookup"><span data-stu-id="4be78-125">Copy hello newly generated key:</span></span>  
   ![graphic5][graphic5]
7. <span data-ttu-id="4be78-127">Continuare tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="4be78-127">Continue tooPart 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="4be78-128">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="4be78-128">Event hubs</span></span>
1. <span data-ttu-id="4be78-129">Passare l'estensione di Service Bus toohello nel portale di gestione di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="4be78-129">Go toohello Service Bus extension on hello Azure Management portal:</span></span>  
   ![graphic6][graphic6]
2. <span data-ttu-id="4be78-131">Individuare hello Namespace Bus di servizio utilizzato per il processo e passare al suo interno:</span><span class="sxs-lookup"><span data-stu-id="4be78-131">Locate hello Service Bus Namespace used by your job and go into it:</span></span>  
   ![graphic7][graphic7]
3. <span data-ttu-id="4be78-133">Se il processo utilizza un criterio di accesso condiviso su hello Service Bus Namespace, passare toostep 6</span><span class="sxs-lookup"><span data-stu-id="4be78-133">If your job uses a shared access policy on hello Service Bus Namespace, jump toostep 6</span></span>  
4. <span data-ttu-id="4be78-134">Consente di passare toohello scheda di hub eventi:</span><span class="sxs-lookup"><span data-stu-id="4be78-134">Go toohello Event Hubs tab:</span></span>  
   ![graphic8][graphic8]
5. <span data-ttu-id="4be78-136">Individuare hello utilizzato dal processo di Hub di eventi e passare al suo interno:</span><span class="sxs-lookup"><span data-stu-id="4be78-136">Locate hello Event Hub used by your job and go into it:</span></span>  
   ![graphic9][graphic9]
6. <span data-ttu-id="4be78-138">Consente di passare toohello scheda Configura:</span><span class="sxs-lookup"><span data-stu-id="4be78-138">Go toohello Configure Tab:</span></span>  
   ![graphic10][graphic10]
7. <span data-ttu-id="4be78-140">Nel menu a discesa Nome criterio hello, individuare i criteri di accesso condiviso hello utilizzato dal processo di:</span><span class="sxs-lookup"><span data-stu-id="4be78-140">On hello Policy Name drop-down, locate hello shared access policy used by your job:</span></span>  
   ![graphic11][graphic11]
8. <span data-ttu-id="4be78-142">Tra hello chiave primaria e chiave secondaria, hello **pick hello non utilizzato dal processo di**.</span><span class="sxs-lookup"><span data-stu-id="4be78-142">Between hello Primary Key and hello Secondary Key, **pick hello one not used by your job**.</span></span>  
9. <span data-ttu-id="4be78-143">Premere l’opzione di rigenerazione: </span><span class="sxs-lookup"><span data-stu-id="4be78-143">Hit regenerate:</span></span>  
   ![graphic12][graphic12]
10. <span data-ttu-id="4be78-145">Copiare la chiave hello appena generato:</span><span class="sxs-lookup"><span data-stu-id="4be78-145">Copy hello newly generated key:</span></span>  
   ![graphic13][graphic13]
11. <span data-ttu-id="4be78-147">Continuare tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="4be78-147">Continue tooPart 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="4be78-148">Database SQL</span><span class="sxs-lookup"><span data-stu-id="4be78-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="4be78-149">Nota: è necessario tooconnect toohello servizio Database SQL.</span><span class="sxs-lookup"><span data-stu-id="4be78-149">Note: you will need tooconnect toohello SQL Database Service.</span></span> <span data-ttu-id="4be78-150">Verrà tooshow come toodo questo utilizzando hello esperienza di gestione nel portale di gestione di Azure hello ma è possibile scegliere toouse nonché uno strumento sul lato client, ad esempio SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="4be78-150">We are going tooshow how toodo this using hello management experience on hello Azure Management portal but you may choose toouse some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="4be78-151">Passare l'estensione database SQL toohello nel portale di gestione di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="4be78-151">Go toohello SQL Databases extension on hello Azure Management portal:</span></span>  
   ![graphic14][graphic14]
2. <span data-ttu-id="4be78-153">Individuare i Database SQL utilizzato dal processo di hello e **fare clic su server hello** collegamento su hello stessa riga:</span><span class="sxs-lookup"><span data-stu-id="4be78-153">Locate hello SQL Database used by your job and **click on hello server** link on hello same line:</span></span>  
   <span data-ttu-id="4be78-154">![graphic15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="4be78-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="4be78-155">Fare clic sul comando Gestisci hello:</span><span class="sxs-lookup"><span data-stu-id="4be78-155">Click hello Manage command:</span></span>  
   ![graphic16][graphic16]
4. <span data-ttu-id="4be78-157">Digitare master del database: </span><span class="sxs-lookup"><span data-stu-id="4be78-157">Type Database Master:</span></span>  
   ![graphic17][graphic17]
5. <span data-ttu-id="4be78-159">Immettere il nome utente, la password e fare clic su Accedi: </span><span class="sxs-lookup"><span data-stu-id="4be78-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![graphic18][graphic18]
6. <span data-ttu-id="4be78-161">Fare clic su Nuova query: </span><span class="sxs-lookup"><span data-stu-id="4be78-161">Click New Query:</span></span>  
   ![graphic19][graphic19]
7. <span data-ttu-id="4be78-163">Tipo di hello seguente query sostituendo < login_name > con il nome utente e la sostituzione <enterStrongPasswordHere> con la nuova password:</span><span class="sxs-lookup"><span data-stu-id="4be78-163">Type in hello following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="4be78-164">Fare clic su Esegui: </span><span class="sxs-lookup"><span data-stu-id="4be78-164">Click Run:</span></span>  
   ![graphic20][graphic20]
9. <span data-ttu-id="4be78-166">Tornare indietro toostep 2 e questa volta scegliere database hello:</span><span class="sxs-lookup"><span data-stu-id="4be78-166">Go back toostep 2 and this time click hello database:</span></span>  
   ![graphic21][graphic21]
10. <span data-ttu-id="4be78-168">Fare clic sul comando Gestisci hello:</span><span class="sxs-lookup"><span data-stu-id="4be78-168">Click hello Manage command:</span></span>  
   ![graphic22][graphic22]
11. <span data-ttu-id="4be78-170">Digitare il nome utente, la password e fare clic su Accedi: </span><span class="sxs-lookup"><span data-stu-id="4be78-170">type in your User Name, Password, and click Logon:</span></span>  
   ![graphic23][graphic23]
12. <span data-ttu-id="4be78-172">Fare clic su Nuova query: </span><span class="sxs-lookup"><span data-stu-id="4be78-172">Click New Query:</span></span>  
   ![graphic24][graphic24]
13. <span data-ttu-id="4be78-174">Digitare nella seguente query sostituendo < nome_utente > con un nome con cui si desidera tooidentify hello questo account di accesso nel contesto di hello del database (è possibile fornire hello stesso valore scelto per < login_name >, ad esempio) e sostituendo < login_name > con il nuovo nome utente:</span><span class="sxs-lookup"><span data-stu-id="4be78-174">Type in hello following query replacing <user_name> with a name by which you want tooidentify this login in hello context of this database (you can provide hello same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="4be78-175">Fare clic su Esegui: </span><span class="sxs-lookup"><span data-stu-id="4be78-175">Click Run:</span></span>  
   ![graphic25][graphic25]
15. <span data-ttu-id="4be78-177">A questo punto è necessario fornire un nuovo utente hello stessi ruoli e i privilegi assegnati all'utente originale.</span><span class="sxs-lookup"><span data-stu-id="4be78-177">You should now provide your new user with hello same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="4be78-178">Continuare tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="4be78-178">Continue tooPart 2.</span></span>

## <a name="part-2-stopping-hello-stream-analytics-job"></a><span data-ttu-id="4be78-179">Parte 2: Arresto hello Analitica del processo di flusso</span><span class="sxs-lookup"><span data-stu-id="4be78-179">Part 2: Stopping hello Stream Analytics Job</span></span>
1. <span data-ttu-id="4be78-180">Visitare estensione Analitica flusso toohello nel portale di gestione di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="4be78-180">Go toohello Stream Analytics extension on hello Azure Management portal:</span></span>  
   ![graphic26][graphic26]
2. <span data-ttu-id="4be78-182">Individuare il processo e accedervi: </span><span class="sxs-lookup"><span data-stu-id="4be78-182">Locate your job and go into it:</span></span>  
   ![graphic27][graphic27]
3. <span data-ttu-id="4be78-184">Passare toohello input scheda o hello output in base a rotazione se credenziali hello su un Input o su un Output.</span><span class="sxs-lookup"><span data-stu-id="4be78-184">Go toohello Inputs tab or hello Outputs tab based on whether you are rotating hello credentials on an Input or on an Output.</span></span>  
   ![graphic28][graphic28]
4. <span data-ttu-id="4be78-186">Fare clic sul comando di arresto hello e confermare processo hello è stato arrestato.</span><span class="sxs-lookup"><span data-stu-id="4be78-186">Click hello Stop command and confirm hello job has stopped:</span></span>  
   <span data-ttu-id="4be78-187">![graphic29][graphic29] attendere toostop processo hello.</span><span class="sxs-lookup"><span data-stu-id="4be78-187">![graphic29][graphic29] Wait for hello job toostop.</span></span>
5. <span data-ttu-id="4be78-188">Individuare hello input/output desiderato credenziali toorotate on e passare al suo interno:</span><span class="sxs-lookup"><span data-stu-id="4be78-188">Locate hello input/output you want toorotate credentials on and go into it:</span></span>  
   ![graphic30][graphic30]
6. <span data-ttu-id="4be78-190">Procedere tooPart 3.</span><span class="sxs-lookup"><span data-stu-id="4be78-190">Proceed tooPart 3.</span></span>

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a><span data-ttu-id="4be78-191">Parte 3: Modifica delle credenziali di hello nel processo di flusso Analitica hello</span><span class="sxs-lookup"><span data-stu-id="4be78-191">Part 3: Editing hello credentials on hello Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="4be78-192">Archiviazione BLOB/Archiviazione tabelle</span><span class="sxs-lookup"><span data-stu-id="4be78-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="4be78-193">Trovare il campo chiave dell'Account di archiviazione hello e incollare la chiave appena generata:</span><span class="sxs-lookup"><span data-stu-id="4be78-193">Find hello Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![graphic31][graphic31]
2. <span data-ttu-id="4be78-195">Fare clic sul comando Salva hello e confermare il salvataggio delle modifiche:</span><span class="sxs-lookup"><span data-stu-id="4be78-195">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic32][graphic32]
3. <span data-ttu-id="4be78-197">Al salvataggio delle modifiche, verrà automaticamente avviato un test di connessione. Assicurarsi che abbia esito positivo.</span><span class="sxs-lookup"><span data-stu-id="4be78-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="4be78-198">Procedere tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="4be78-198">Proceed tooPart 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="4be78-199">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="4be78-199">Event hubs</span></span>
1. <span data-ttu-id="4be78-200">Trovare il campo chiave criterio Hub eventi hello e incollare la chiave appena generata:</span><span class="sxs-lookup"><span data-stu-id="4be78-200">Find hello Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![graphic33][graphic33]
2. <span data-ttu-id="4be78-202">Fare clic sul comando Salva hello e confermare il salvataggio delle modifiche:</span><span class="sxs-lookup"><span data-stu-id="4be78-202">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic34][graphic34]
3. <span data-ttu-id="4be78-204">Al salvataggio delle modifiche, verrà automaticamente avviato un test di connessione. Assicurarsi che abbia esito positivo.</span><span class="sxs-lookup"><span data-stu-id="4be78-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="4be78-205">Procedere tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="4be78-205">Proceed tooPart 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="4be78-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="4be78-206">Power BI</span></span>
1. <span data-ttu-id="4be78-207">Fare clic su autorizzazione rinnovo hello:</span><span class="sxs-lookup"><span data-stu-id="4be78-207">Click hello Renew authorization:</span></span>  

   ![graphic35][graphic35]
2. <span data-ttu-id="4be78-209">Verrà visualizzato hello seguito conferma:</span><span class="sxs-lookup"><span data-stu-id="4be78-209">You will get hello following confirmation:</span></span>  

   ![graphic36][graphic36]
3. <span data-ttu-id="4be78-211">Fare clic sul comando Salva hello e confermare il salvataggio delle modifiche:</span><span class="sxs-lookup"><span data-stu-id="4be78-211">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic37][graphic37]
4. <span data-ttu-id="4be78-213">Al salvataggio delle modifiche, verrà automaticamente avviato un test di connessione. Assicurarsi che abbia esito positivo.</span><span class="sxs-lookup"><span data-stu-id="4be78-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="4be78-214">Procedere tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="4be78-214">Proceed tooPart 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="4be78-215">Database SQL</span><span class="sxs-lookup"><span data-stu-id="4be78-215">SQL Database</span></span>
1. <span data-ttu-id="4be78-216">Trovare i campi nome utente e Password di hello e incollare l'insieme di credenziali appena creato:</span><span class="sxs-lookup"><span data-stu-id="4be78-216">Find hello User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![graphic38][graphic38]
2. <span data-ttu-id="4be78-218">Fare clic sul comando Salva hello e confermare il salvataggio delle modifiche:</span><span class="sxs-lookup"><span data-stu-id="4be78-218">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic39][graphic39]
3. <span data-ttu-id="4be78-220">Al salvataggio delle modifiche, verrà automaticamente avviato un test di connessione. Assicurarsi che abbia esito positivo.</span><span class="sxs-lookup"><span data-stu-id="4be78-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="4be78-221">Procedere tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="4be78-221">Proceed tooPart 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="4be78-222">Parte 4: avvio del processo dall’ora dell’ultimo arresto</span><span class="sxs-lookup"><span data-stu-id="4be78-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="4be78-223">Abbandona hello Input/Output:</span><span class="sxs-lookup"><span data-stu-id="4be78-223">Navigate away from hello Input/Output:</span></span>  
   ![graphic40][graphic40]
2. <span data-ttu-id="4be78-225">Fare clic sul comando di avvio hello:</span><span class="sxs-lookup"><span data-stu-id="4be78-225">Click hello Start command:</span></span>  
   ![graphic41][graphic41]
3. <span data-ttu-id="4be78-227">Selezionare ora ultimo arresto hello e fare clic su OK:</span><span class="sxs-lookup"><span data-stu-id="4be78-227">Pick hello Last Stopped Time and click OK:</span></span>  
   ![graphic42][graphic42]
4. <span data-ttu-id="4be78-229">Procedere tooPart 5.</span><span class="sxs-lookup"><span data-stu-id="4be78-229">Proceed tooPart 5.</span></span>  

## <a name="part-5-removing-hello-old-set-of-credentials"></a><span data-ttu-id="4be78-230">Parte 5: Rimozione di hello precedente set di credenziali</span><span class="sxs-lookup"><span data-stu-id="4be78-230">Part 5: Removing hello old set of credentials</span></span>
<span data-ttu-id="4be78-231">Questa parte è applicabile toohello degli input/output seguente:</span><span class="sxs-lookup"><span data-stu-id="4be78-231">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="4be78-232">Archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="4be78-232">Blob Storage</span></span>
* <span data-ttu-id="4be78-233">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="4be78-233">Event Hubs</span></span>
* <span data-ttu-id="4be78-234">Database SQL</span><span class="sxs-lookup"><span data-stu-id="4be78-234">SQL Database</span></span>
* <span data-ttu-id="4be78-235">Archiviazione tabelle</span><span class="sxs-lookup"><span data-stu-id="4be78-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="4be78-236">Archiviazione BLOB/Archiviazione tabelle</span><span class="sxs-lookup"><span data-stu-id="4be78-236">Blob storage/Table storage</span></span>
<span data-ttu-id="4be78-237">Ripetere parte 1 per la chiave di accesso utilizzato dal processo di hello toorenew hello ora inutilizzati chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="4be78-237">Repeat Part 1 for hello Access Key that was previously used by your job toorenew hello now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="4be78-238">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="4be78-238">Event hubs</span></span>
<span data-ttu-id="4be78-239">Ripetere parte 1 per la chiave utilizzata per il processo di hello toorenew hello chiave ora inutilizzati.</span><span class="sxs-lookup"><span data-stu-id="4be78-239">Repeat Part 1 for hello Key that was previously used by your job toorenew hello now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="4be78-240">Database SQL</span><span class="sxs-lookup"><span data-stu-id="4be78-240">SQL Database</span></span>
1. <span data-ttu-id="4be78-241">Tornare indietro toohello finestra di query da parte 1 passaggio 7 e tipo di query seguente, sostituendo < previous_login_name > con il nome utente utilizzato in precedenza per il processo di hello di hello:</span><span class="sxs-lookup"><span data-stu-id="4be78-241">Go back toohello query window from Part 1 Step 7 and type in hello following query, replacing <previous_login_name> with hello User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="4be78-242">Fare clic su Esegui: </span><span class="sxs-lookup"><span data-stu-id="4be78-242">Click Run:</span></span>  
   ![graphic43][graphic43]  

<span data-ttu-id="4be78-244">È necessario ottenere hello seguito conferma:</span><span class="sxs-lookup"><span data-stu-id="4be78-244">You should get hello following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="4be78-245">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="4be78-245">Get help</span></span>
<span data-ttu-id="4be78-246">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="4be78-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="4be78-247">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4be78-247">Next steps</span></span>
* [<span data-ttu-id="4be78-248">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="4be78-248">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="4be78-249">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="4be78-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="4be78-250">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="4be78-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="4be78-251">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="4be78-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="4be78-252">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="4be78-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

