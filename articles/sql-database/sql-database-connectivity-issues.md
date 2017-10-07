---
title: aaaFix un errore di connessione SQL, errore temporaneo | Documenti Microsoft
description: 'Informazioni su come tootroubleshoot, diagnosticare ed evitare un errore di connessione SQL o temporanei nel Database di SQL Azure. '
keywords: "connessione sql,stringa di connessione,problemi di connettività,errore temporaneo,errore di connessione"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="8ad79-104">Risolvere, diagnosticare ed evitare gli errori di connessione SQL e gli errori temporanei per il database SQL</span><span class="sxs-lookup"><span data-stu-id="8ad79-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="8ad79-105">In questo articolo viene descritto come tooprevent, risolvere, diagnosticare e risolvere gli errori di connessione e gli errori temporanei che nell'applicazione client viene rilevato quando interagisce con il Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ad79-105">This article describes how tooprevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="8ad79-106">Informazioni su come tooconfigure la logica di riesecuzione, compilare la stringa di connessione hello e modificare altre impostazioni di connessione.</span><span class="sxs-lookup"><span data-stu-id="8ad79-106">Learn how tooconfigure retry logic, build hello connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="8ad79-107">Errori temporanei</span><span class="sxs-lookup"><span data-stu-id="8ad79-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="8ad79-108">Un errore temporaneo è un errore la cui causa sottostante si risolverà automaticamente in modo rapido.</span><span class="sxs-lookup"><span data-stu-id="8ad79-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span></span> <span data-ttu-id="8ad79-109">Una causa di errori temporanei occasionale è quando hello sistema Azure scorre rapidamente hardware risorse toobetter il bilanciamento del carico diversi carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8ad79-109">An occasional cause of transient errors is when hello Azure system quickly shifts hardware resources toobetter load-balance various workloads.</span></span> <span data-ttu-id="8ad79-110">La maggior parte di questi eventi di riconfigurazione spesso viene completata in meno di 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="8ad79-110">Most of these reconfiguration events often complete in less than 60 seconds.</span></span> <span data-ttu-id="8ad79-111">Durante questo intervallo di riconfigurazione, è possibile connettività problemi tooAzure Database SQL.</span><span class="sxs-lookup"><span data-stu-id="8ad79-111">During this reconfiguration time span, you may have connectivity issues tooAzure SQL Database.</span></span> <span data-ttu-id="8ad79-112">Applicazioni che si connettono tooAzure Database SQL deve essere compilato tooexpect questi errori temporanei, li implementando la logica nel codice anziché superfici li toousers come errori dell'applicazione di tentativi di handle.</span><span class="sxs-lookup"><span data-stu-id="8ad79-112">Applications connecting tooAzure SQL Database should be built tooexpect these transient errors, handle them by implementing retry logic in their code instead of surfacing them toousers as application errors.</span></span>

<span data-ttu-id="8ad79-113">Se il programma client utilizza ADO.NET, il programma verrà comunicato sull'errore temporaneo hello da throw hello di un **SqlException**.</span><span class="sxs-lookup"><span data-stu-id="8ad79-113">If your client program is using ADO.NET, your program is told about hello transient error by hello throw of an **SqlException**.</span></span> <span data-ttu-id="8ad79-114">Hello **numero** proprietà può essere confrontata con l'elenco di hello di errori temporanei parte superiore di hello di argomento hello: [codici di errore SQL per le applicazioni client di Database SQL](sql-database-develop-error-messages.md).</span><span class="sxs-lookup"><span data-stu-id="8ad79-114">hello **Number** property can be compared against hello list of transient errors near hello top of hello topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="8ad79-115">Confronto tra connessione e comando</span><span class="sxs-lookup"><span data-stu-id="8ad79-115">Connection versus command</span></span>
<span data-ttu-id="8ad79-116">Si tentare la connessione a SQL hello oppure stabilire nuovamente, a seconda delle operazioni seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="8ad79-116">You'll retry hello SQL connection or establish it again, depending on hello following:</span></span>

* <span data-ttu-id="8ad79-117">**Si verifica un errore temporaneo durante un tentativo di connessione**: connessione hello deve essere riprovata dopo il ritardo per alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="8ad79-117">**A transient error occurs during a connection try**: hello connection should be retried after delaying for several seconds.</span></span>
* <span data-ttu-id="8ad79-118">**Si verifica un errore temporaneo durante un comando di query SQL**: comando hello non deve essere riprovata immediatamente.</span><span class="sxs-lookup"><span data-stu-id="8ad79-118">**A transient error occurs during a SQL query command**: hello command should not be immediately retried.</span></span> <span data-ttu-id="8ad79-119">Al contrario, dopo un ritardo, hello deve appena stabilire la connessione.</span><span class="sxs-lookup"><span data-stu-id="8ad79-119">Instead, after a delay, hello connection should be freshly established.</span></span> <span data-ttu-id="8ad79-120">È possibile ritentare quindi il comando hello.</span><span class="sxs-lookup"><span data-stu-id="8ad79-120">Then hello command can be retried.</span></span>

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="8ad79-121">Logica di ripetizione dei tentativi per errori temporanei</span><span class="sxs-lookup"><span data-stu-id="8ad79-121">Retry logic for transient errors</span></span>
<span data-ttu-id="8ad79-122">I programmi client in cui occasionalmente si verifica un errore temporaneo sono più affidabili se contengono una logica di ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="8ad79-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="8ad79-123">Quando il programma comunica con il Database di SQL Azure tramite un middleware di parti 3rd, verificare con il fornitore hello se middleware hello contiene la logica di tentativi per errori temporanei.</span><span class="sxs-lookup"><span data-stu-id="8ad79-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with hello vendor whether hello middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a><span data-ttu-id="8ad79-124">Principi per la ripetizione dei tentativi</span><span class="sxs-lookup"><span data-stu-id="8ad79-124">Principles for retry</span></span>
* <span data-ttu-id="8ad79-125">Se l'errore hello è temporaneo, è necessario riprovare un tooopen tentativo di una connessione.</span><span class="sxs-lookup"><span data-stu-id="8ad79-125">An attempt tooopen a connection should be retried if hello error is transient.</span></span>
* <span data-ttu-id="8ad79-126">Non è consigliabile riprovare direttamente a eseguire un'istruzione SQL SELECT non riuscita con un errore temporaneo.</span><span class="sxs-lookup"><span data-stu-id="8ad79-126">A SQL SELECT statement that fails with a transient error should not be retried directly.</span></span>
  
  * <span data-ttu-id="8ad79-127">Al contrario, definire una nuova connessione e ripetere hello selezionare.</span><span class="sxs-lookup"><span data-stu-id="8ad79-127">Instead, establish a fresh connection, and then retry hello SELECT.</span></span>
* <span data-ttu-id="8ad79-128">Quando un'istruzione SQL UPDATE ha esito negativo con un errore temporaneo, una nuova connessione deve essere stabilita prima hello che nuovo tentativo di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="8ad79-128">When a SQL UPDATE statement fails with a transient error, a fresh connection should be established before hello UPDATE is retried.</span></span>
  
  * <span data-ttu-id="8ad79-129">logica di riesecuzione Hello è necessario assicurarsi che transazione intero database hello completata o dell'intera transazione che hello viene eseguito il rollback.</span><span class="sxs-lookup"><span data-stu-id="8ad79-129">hello retry logic must ensure that either hello entire database transaction completed, or that hello entire transaction is rolled back.</span></span>

#### <a name="other-considerations-for-retry"></a><span data-ttu-id="8ad79-130">Altre considerazioni per la ripetizione dei tentativi</span><span class="sxs-lookup"><span data-stu-id="8ad79-130">Other considerations for retry</span></span>
* <span data-ttu-id="8ad79-131">Un file batch che viene avviato automaticamente dopo l'orario di lavoro, e che verranno completati prima mattino, è possibile concedere toovery paziente con intervalli di tempo lunghi tra il numero di tentativi.</span><span class="sxs-lookup"><span data-stu-id="8ad79-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford toovery patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="8ad79-132">Un programma dell'interfaccia utente devono tener conto hello tendenza umano toogive backup dopo troppo tempo di attesa.</span><span class="sxs-lookup"><span data-stu-id="8ad79-132">A user interface program should account for hello human tendency toogive up after too long a wait.</span></span>
  
  * <span data-ttu-id="8ad79-133">Tuttavia, soluzione hello non deve essere tooretry ogni pochi secondi, perché tale criterio può riempire sistema hello con le richieste.</span><span class="sxs-lookup"><span data-stu-id="8ad79-133">However, hello solution must not be tooretry every few seconds, because that policy can flood hello system with requests.</span></span>

#### <a name="interval-increase-between-retries"></a><span data-ttu-id="8ad79-134">Incremento dell'intervallo tra i tentativi</span><span class="sxs-lookup"><span data-stu-id="8ad79-134">Interval increase between retries</span></span>
<span data-ttu-id="8ad79-135">È consigliabile attendere 5 secondi prima di riprovare.</span><span class="sxs-lookup"><span data-stu-id="8ad79-135">We recommend that you delay for 5 seconds before your first retry.</span></span> <span data-ttu-id="8ad79-136">Nuovo tentativo dopo un ritardo inferiore a 5 secondi rischi in termini di servizio cloud di hello impegnativo.</span><span class="sxs-lookup"><span data-stu-id="8ad79-136">Retrying after a delay shorter than 5 seconds risks overwhelming hello cloud service.</span></span> <span data-ttu-id="8ad79-137">Per ogni tentativo successivo ritardo hello aumentino in modo esponenziale, backup tooa massimo di 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="8ad79-137">For each subsequent retry hello delay should grow exponentially, up tooa maximum of 60 seconds.</span></span>

<span data-ttu-id="8ad79-138">Una discussione di hello *il periodo di blocco* per i client che usano ADO.NET è disponibile in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ad79-138">A discussion of hello *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="8ad79-139">È inoltre possibile tooset un numero massimo di tentativi prima della chiusura automatica dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8ad79-139">You might also want tooset a maximum number of retries before hello program self-terminates.</span></span>

#### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="8ad79-140">Esempi di codice con logica di ripetizione dei tentativi</span><span class="sxs-lookup"><span data-stu-id="8ad79-140">Code samples with retry logic</span></span>
<span data-ttu-id="8ad79-141">Esempi di codice con logica di ripetizione dei tentativi in diversi linguaggi di programmazione sono disponibili in:</span><span class="sxs-lookup"><span data-stu-id="8ad79-141">Code samples with retry logic, in a variety of programming languages, are available at:</span></span>

* [<span data-ttu-id="8ad79-142">Raccolte di connessioni per database SQL e Server SQL</span><span class="sxs-lookup"><span data-stu-id="8ad79-142">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a><span data-ttu-id="8ad79-143">Eseguire test sulla logica di ripetizione tentativi</span><span class="sxs-lookup"><span data-stu-id="8ad79-143">Test your retry logic</span></span>
<span data-ttu-id="8ad79-144">tootest la logica di tentativi, è necessario simulare o provocare un errore che possono essere corretti, mentre il programma è ancora in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8ad79-144">tootest your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span></span>

##### <a name="test-by-disconnecting-from-hello-network"></a><span data-ttu-id="8ad79-145">Per testare la disconnessione dalla rete hello</span><span class="sxs-lookup"><span data-stu-id="8ad79-145">Test by disconnecting from hello network</span></span>
<span data-ttu-id="8ad79-146">È possibile testare la logica di ripetizione è toodisconnect computer client da hello di rete durante l'esecuzione programma hello.</span><span class="sxs-lookup"><span data-stu-id="8ad79-146">One way you can test your retry logic is toodisconnect your client computer from hello network while hello program is running.</span></span> <span data-ttu-id="8ad79-147">Errore Hello sarà:</span><span class="sxs-lookup"><span data-stu-id="8ad79-147">hello error will be:</span></span>

* <span data-ttu-id="8ad79-148">**SqlException.Number** = 11001</span><span class="sxs-lookup"><span data-stu-id="8ad79-148">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="8ad79-149">Messaggio: "Host sconosciuto"</span><span class="sxs-lookup"><span data-stu-id="8ad79-149">Message: "No such host is known"</span></span>

<span data-ttu-id="8ad79-150">Come parte di hello innanzitutto nuovo tentativo, il programma può correggere l'errore di ortografia hello e quindi tentare tooconnect.</span><span class="sxs-lookup"><span data-stu-id="8ad79-150">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="8ad79-151">toomake questo pratici, si scollega il computer dalla rete hello prima di avviare il programma.</span><span class="sxs-lookup"><span data-stu-id="8ad79-151">toomake this practical, you unplug your computer from hello network before you start your program.</span></span> <span data-ttu-id="8ad79-152">Quindi il programma riconosce un parametro runtime che causa hello programma:</span><span class="sxs-lookup"><span data-stu-id="8ad79-152">Then your program recognizes a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="8ad79-153">Aggiungere temporaneamente 11001 tooits elenco di errori tooconsider come oggetto temporaneo.</span><span class="sxs-lookup"><span data-stu-id="8ad79-153">Temporarily add 11001 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="8ad79-154">Tentativo della prima connessione come di consueto.</span><span class="sxs-lookup"><span data-stu-id="8ad79-154">Attempt its first connection as usual.</span></span>
3. <span data-ttu-id="8ad79-155">Dopo aver hello viene rilevato l'errore, rimuovere 11001 dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="8ad79-155">After hello error is caught, remove 11001 from hello list.</span></span>
4. <span data-ttu-id="8ad79-156">Visualizzare un messaggio che indica i computer di hello hello utente tooplug rete hello.</span><span class="sxs-lookup"><span data-stu-id="8ad79-156">Display a message telling hello user tooplug hello computer into hello network.</span></span>
   * <span data-ttu-id="8ad79-157">Sospendere l'esecuzione ulteriormente utilizzando entrambi hello **ReadLine** metodo o una finestra di dialogo con un pulsante OK.</span><span class="sxs-lookup"><span data-stu-id="8ad79-157">Pause further execution by using either hello **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="8ad79-158">Hello utente preme hello INVIO dopo hello computer collegato in rete hello.</span><span class="sxs-lookup"><span data-stu-id="8ad79-158">hello user presses hello Enter key after hello computer plugged into hello network.</span></span>
5. <span data-ttu-id="8ad79-159">Tentare nuovamente tooconnect, prevede l'esito positivo.</span><span class="sxs-lookup"><span data-stu-id="8ad79-159">Attempt again tooconnect, expecting success.</span></span>

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a><span data-ttu-id="8ad79-160">Test in base al nome di database hello errore di ortografia durante la connessione</span><span class="sxs-lookup"><span data-stu-id="8ad79-160">Test by misspelling hello database name when connecting</span></span>
<span data-ttu-id="8ad79-161">Il programma può intenzionalmente in modo errato il nome utente hello prima il primo tentativo di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="8ad79-161">Your program can purposely misspell hello user name before hello first connection attempt.</span></span> <span data-ttu-id="8ad79-162">Errore Hello sarà:</span><span class="sxs-lookup"><span data-stu-id="8ad79-162">hello error will be:</span></span>

* <span data-ttu-id="8ad79-163">**SqlException.Number** = 18456</span><span class="sxs-lookup"><span data-stu-id="8ad79-163">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="8ad79-164">Messaggio: "Accesso non riuscito per l'utente 'WRONG_MyUserName'."</span><span class="sxs-lookup"><span data-stu-id="8ad79-164">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="8ad79-165">Come parte di hello innanzitutto nuovo tentativo, il programma può correggere l'errore di ortografia hello e quindi tentare tooconnect.</span><span class="sxs-lookup"><span data-stu-id="8ad79-165">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="8ad79-166">toomake questo pratica, il programma può riconoscere un parametro runtime che causa hello programma:</span><span class="sxs-lookup"><span data-stu-id="8ad79-166">toomake this practical, your program could recognize a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="8ad79-167">Aggiungere temporaneamente 18456 tooits elenco di errori tooconsider come oggetto temporaneo.</span><span class="sxs-lookup"><span data-stu-id="8ad79-167">Temporarily add 18456 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="8ad79-168">Aggiungere intenzionalmente nome utente di toohello 'WRONG_'.</span><span class="sxs-lookup"><span data-stu-id="8ad79-168">Purposely add 'WRONG_' toohello user name.</span></span>
3. <span data-ttu-id="8ad79-169">Dopo aver hello viene rilevato l'errore, rimuovere 18456 dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="8ad79-169">After hello error is caught, remove 18456 from hello list.</span></span>
4. <span data-ttu-id="8ad79-170">Rimuovere 'WRONG_' da nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="8ad79-170">Remove 'WRONG_' from hello user name.</span></span>
5. <span data-ttu-id="8ad79-171">Tentare nuovamente tooconnect, prevede l'esito positivo.</span><span class="sxs-lookup"><span data-stu-id="8ad79-171">Attempt again tooconnect, expecting success.</span></span>

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="8ad79-172">Parametri di SqlConnection di .NET per nuovi tentativi di connessione</span><span class="sxs-lookup"><span data-stu-id="8ad79-172">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="8ad79-173">Se il programma client si connette tootooAzure Database SQL tramite la classe di .NET Framework hello **SqlConnection**, è necessario utilizzare .NET 4.6.1 o versioni successive (o .NET Core) in modo è possibile sfruttare la funzionalità di tentativi di connessione.</span><span class="sxs-lookup"><span data-stu-id="8ad79-173">If your client program connects tootooAzure SQL Database by using hello .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span></span> <span data-ttu-id="8ad79-174">I dettagli della funzionalità hello sono [qui](http://go.microsoft.com/fwlink/?linkid=393996).</span><span class="sxs-lookup"><span data-stu-id="8ad79-174">Details of hello feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


<span data-ttu-id="8ad79-175">Quando si compila hello [stringa di connessione](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) per il **SqlConnection** dell'oggetto, è necessario coordinare valori hello tra hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="8ad79-175">When you build hello [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate hello values among hello following parameters:</span></span>

* <span data-ttu-id="8ad79-176">ConnectRetryCount &nbsp;&nbsp;*(Il valore predefinito è 1. L'intervallo consentito è tra 0 e 255.)*</span><span class="sxs-lookup"><span data-stu-id="8ad79-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span></span>
* <span data-ttu-id="8ad79-177">ConnectRetryInterval &nbsp;&nbsp;*(Il valore predefinito è 1 secondo. L'intervallo consentito è tra 1 e 60.)*</span><span class="sxs-lookup"><span data-stu-id="8ad79-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span></span>
* <span data-ttu-id="8ad79-178">Timeout di connessione &nbsp;&nbsp;*(Il valore predefinito è 15 secondi. L'intervallo consentito è tra 0 e 2147483647)*</span><span class="sxs-lookup"><span data-stu-id="8ad79-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span></span>

<span data-ttu-id="8ad79-179">In particolare, i valori scelti devono apportare hello seguente uguaglianza true:</span><span class="sxs-lookup"><span data-stu-id="8ad79-179">Specifically, your chosen values should make hello following equality true:</span></span>

* <span data-ttu-id="8ad79-180">Timeout di connessione = ConnectRetryCount * ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="8ad79-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span></span>

<span data-ttu-id="8ad79-181">Ad esempio, se hello count = 3 e l'intervallo = 10 secondi, un timeout di solo 29 secondi non abbastanza concederebbe sistema hello tempo sufficiente per il 3 e l'ultimo attendere e riprovare la connessione: 29 < 3 * 10.</span><span class="sxs-lookup"><span data-stu-id="8ad79-181">For example, if hello count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give hello system enough time for its 3rd and final retry at connecting: 29 < 3 * 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="8ad79-182">Confronto tra connessione e comando</span><span class="sxs-lookup"><span data-stu-id="8ad79-182">Connection versus command</span></span>
<span data-ttu-id="8ad79-183">Hello **ConnectRetryCount** e **ConnectRetryInterval** parametri consentono il **SqlConnection** hello tentativi oggetto operazione di connessione senza indicare o richiedere l'intervento del programma, ad esempio la restituzione tooyour programma del controllo.</span><span class="sxs-lookup"><span data-stu-id="8ad79-183">hello **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry hello connect operation without telling or bothering your program, such as returning control tooyour program.</span></span> <span data-ttu-id="8ad79-184">tentativi di Hello possono verificarsi nelle seguenti situazioni hello:</span><span class="sxs-lookup"><span data-stu-id="8ad79-184">hello retries can occur in hello following situations:</span></span>

* <span data-ttu-id="8ad79-185">Chiamata al metodo mySqlConnection.Open</span><span class="sxs-lookup"><span data-stu-id="8ad79-185">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="8ad79-186">Chiamata al metodo mySqlConnection.Execute</span><span class="sxs-lookup"><span data-stu-id="8ad79-186">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="8ad79-187">È importante sottolineare che,</span><span class="sxs-lookup"><span data-stu-id="8ad79-187">There is a subtlety.</span></span> <span data-ttu-id="8ad79-188">Se si verifica un errore temporaneo durante la *query* è in esecuzione, il **SqlConnection** operazione di connessione non tentativi hello e certamente non ripetere la query dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="8ad79-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry hello connect operation, and it certainly does not retry your query.</span></span> <span data-ttu-id="8ad79-189">Tuttavia, **SqlConnection** molto rapidamente controlli hello connessione prima di inviare la query per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8ad79-189">However, **SqlConnection** very quickly checks hello connection before sending your query for execution.</span></span> <span data-ttu-id="8ad79-190">Se il controllo rapido hello rileva un problema di connessione, **SqlConnection** hello tentativi operazione di connessione.</span><span class="sxs-lookup"><span data-stu-id="8ad79-190">If hello quick check detects a connection problem, **SqlConnection** retries hello connect operation.</span></span> <span data-ttu-id="8ad79-191">Se i tentativi di hello ha esito positivo, si eseguono query viene inviata per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8ad79-191">If hello retry succeeds, you query is sent for execution.</span></span>

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="8ad79-192">Opportunità di combinare ConnectRetryCount con la logica di ripetizione dei tentativi nell'applicazione</span><span class="sxs-lookup"><span data-stu-id="8ad79-192">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="8ad79-193">Si supponga che l'applicazione disponga di una logica di ripetizione dei tentativi particolarmente avanzata,</span><span class="sxs-lookup"><span data-stu-id="8ad79-193">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="8ad79-194">È possibile ripetere hello operazione di connessione 4 volte.</span><span class="sxs-lookup"><span data-stu-id="8ad79-194">It might retry hello connect operation 4 times.</span></span> <span data-ttu-id="8ad79-195">Se si aggiungono **ConnectRetryInterval** e **ConnectRetryCount** = stringa di connessione tooyour 3, si aumenterà hello tentativi conteggio too4 * 3 = 12 tentativi.</span><span class="sxs-lookup"><span data-stu-id="8ad79-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 tooyour connection string, you will increase hello retry count too4 * 3 = 12 retries.</span></span> <span data-ttu-id="8ad79-196">Un numero così elevato di tentativi potrebbe non essere consigliabile.</span><span class="sxs-lookup"><span data-stu-id="8ad79-196">You might not intend such a high number of retries.</span></span>

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a><span data-ttu-id="8ad79-197">Connessioni tooAzure Database SQL</span><span class="sxs-lookup"><span data-stu-id="8ad79-197">Connections tooAzure SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="8ad79-198">Connessione: stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="8ad79-198">Connection: Connection string</span></span>
<span data-ttu-id="8ad79-199">stringa di connessione Hello necessario per la connessione tooAzure Database SQL è leggermente diverso da stringa hello per la connessione tooMicrosoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8ad79-199">hello connection string necessary for connecting tooAzure SQL Database is slightly different from hello string for connecting tooMicrosoft SQL Server.</span></span> <span data-ttu-id="8ad79-200">È possibile copiare la stringa di connessione hello per il database da hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8ad79-200">You can copy hello connection string for your database from hello [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="8ad79-201">Connessione: indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="8ad79-201">Connection: IP address</span></span>
<span data-ttu-id="8ad79-202">È necessario configurare hello Database di SQL server tooaccept comunicazione dall'indirizzo IP hello del computer hello che ospita il programma client.</span><span class="sxs-lookup"><span data-stu-id="8ad79-202">You must configure hello SQL Database server tooaccept communication from hello IP address of hello computer that hosts your client program.</span></span> <span data-ttu-id="8ad79-203">A tale scopo, la modifica delle impostazioni del firewall hello tramite hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8ad79-203">You do this by editing hello firewall settings through hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="8ad79-204">Se si dimentica l'indirizzo IP tooconfigure hello, il programma avrà esito negativo con un messaggio di errore utile indicante l'indirizzo IP hello necessaria.</span><span class="sxs-lookup"><span data-stu-id="8ad79-204">If you forget tooconfigure hello IP address, your program will fail with a handy error message that states hello necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="8ad79-205">Per altre informazioni, vedere [Procedura: Configurare le impostazioni del firewall nel database SQL](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="8ad79-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span></span>

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="8ad79-206">Connessione: porte</span><span class="sxs-lookup"><span data-stu-id="8ad79-206">Connection: Ports</span></span>
<span data-ttu-id="8ad79-207">In genere è necessario solo che la porta 1433 è aperta per le comunicazioni in uscita, computer che ospita l'applicazione client si hello tooensure.</span><span class="sxs-lookup"><span data-stu-id="8ad79-207">Typically you only need tooensure that port 1433 is open for outbound communication, on hello computer that hosts you client program.</span></span>

<span data-ttu-id="8ad79-208">Ad esempio, quando il programma client è ospitato in un computer Windows, hello Windows Firewall nell'host di hello consente tooopen porta 1433:</span><span class="sxs-lookup"><span data-stu-id="8ad79-208">For example, when your client program is hosted on a Windows computer, hello Windows Firewall on hello host enables you tooopen port 1433:</span></span>

1. <span data-ttu-id="8ad79-209">Aprire Pannello di controllo hello</span><span class="sxs-lookup"><span data-stu-id="8ad79-209">Open hello Control Panel</span></span>
2. <span data-ttu-id="8ad79-210">&gt; Tutti gli elementi del Pannello di controllo</span><span class="sxs-lookup"><span data-stu-id="8ad79-210">&gt; All Control Panel Items</span></span>
3. <span data-ttu-id="8ad79-211">&gt; Windows Firewall</span><span class="sxs-lookup"><span data-stu-id="8ad79-211">&gt; Windows Firewall</span></span>
4. <span data-ttu-id="8ad79-212">&gt; Impostazioni avanzate</span><span class="sxs-lookup"><span data-stu-id="8ad79-212">&gt; Advanced Settings</span></span>
5. <span data-ttu-id="8ad79-213">&gt; Regole in uscita</span><span class="sxs-lookup"><span data-stu-id="8ad79-213">&gt; Outbound Rules</span></span>
6. <span data-ttu-id="8ad79-214">&gt; Azioni</span><span class="sxs-lookup"><span data-stu-id="8ad79-214">&gt; Actions</span></span>
7. <span data-ttu-id="8ad79-215">&gt; Nuova regola</span><span class="sxs-lookup"><span data-stu-id="8ad79-215">&gt; New Rule</span></span>

<span data-ttu-id="8ad79-216">Se il programma client è ospitato in una macchina virtuale (VM) di Azure, vedere </span><span class="sxs-lookup"><span data-stu-id="8ad79-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span></span><br/><span data-ttu-id="8ad79-217">[Porte superiori a 1433 per ADO.NET 4.5 e il database SQL](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="8ad79-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="8ad79-218">Per informazioni generali sulla configurazione di porte e indirizzi IP, vedere [Firewall del database SQL di Azure](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="8ad79-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a><span data-ttu-id="8ad79-219">Connessione: ADO.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="8ad79-219">Connection: ADO.NET 4.6.1</span></span>
<span data-ttu-id="8ad79-220">Se il programma utilizza le classi di ADO.NET come **SqlConnection** tooconnect tooAzure Database SQL, è consigliabile utilizzare .NET Framework versione 4.6.1 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="8ad79-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** tooconnect tooAzure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span></span>

<span data-ttu-id="8ad79-221">ADO.NET 4.6.1:</span><span class="sxs-lookup"><span data-stu-id="8ad79-221">ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="8ad79-222">Database SQL di Azure, è maggiore affidabilità quando si apre una connessione con hello **SqlConnection.Open** metodo.</span><span class="sxs-lookup"><span data-stu-id="8ad79-222">For Azure SQL Database, there is improved reliability when you open a connection by using hello **SqlConnection.Open** method.</span></span> <span data-ttu-id="8ad79-223">Hello **aprire** metodo incorpora una migliore meccanismi sforzo retry negli errori tootransient risposta, per alcuni errori entro il periodo di Timeout di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="8ad79-223">hello **Open** method now incorporates best effort retry mechanisms in response tootransient faults, for certain errors within hello Connection Timeout period.</span></span>
* <span data-ttu-id="8ad79-224">Supporta il pool di connessioni,</span><span class="sxs-lookup"><span data-stu-id="8ad79-224">Supports connection pooling.</span></span> <span data-ttu-id="8ad79-225">Sono inclusi una verifica efficiente che hello connessione oggetto offre il programma è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8ad79-225">This includes an efficient verification that hello connection object it gives your program is functioning.</span></span>

<span data-ttu-id="8ad79-226">Quando si utilizza un oggetto connessione da un pool di connessioni, è consigliabile che il programma chiudere temporaneamente connessione hello in uso non immediatamente.</span><span class="sxs-lookup"><span data-stu-id="8ad79-226">When you use a connection object from a connection pool, we recommend that your program temporarily close hello connection when not immediately using it.</span></span> <span data-ttu-id="8ad79-227">Aprire di nuovo una connessione non è dispendiosa è modo di hello creando una nuova connessione.</span><span class="sxs-lookup"><span data-stu-id="8ad79-227">Re-opening a connection is not expensive hello way creating a new connection is.</span></span>

<span data-ttu-id="8ad79-228">Se si sta utilizzando ADO.NET 4.0 o versioni precedenti, si consiglia di eseguire l'aggiornamento toohello ADO.NET più recente.</span><span class="sxs-lookup"><span data-stu-id="8ad79-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade toohello latest ADO.NET.</span></span>

* <span data-ttu-id="8ad79-229">A partire da novembre 2015, è possibile [scaricare ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ad79-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="8ad79-230">Diagnostica</span><span class="sxs-lookup"><span data-stu-id="8ad79-230">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="8ad79-231">Diagnostica: verificare se le utilità si possono connettere</span><span class="sxs-lookup"><span data-stu-id="8ad79-231">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="8ad79-232">Se il programma non riesce tooconnect tooAzure Database SQL, un'opzione di diagnostica è tooconnect tootry con un programma di utilità.</span><span class="sxs-lookup"><span data-stu-id="8ad79-232">If your program is failing tooconnect tooAzure SQL Database, one diagnostic option is tootry tooconnect with a utility program.</span></span> <span data-ttu-id="8ad79-233">In teoria utilità hello si connetterà utilizzando hello stessa libreria che utilizza il programma.</span><span class="sxs-lookup"><span data-stu-id="8ad79-233">Ideally hello utility would connect by using hello same library that your program uses.</span></span>

<span data-ttu-id="8ad79-234">In qualsiasi computer Windows è possibile provare queste utilità:</span><span class="sxs-lookup"><span data-stu-id="8ad79-234">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="8ad79-235">SQL Server Management Studio (ssms.exe), che si connette tramite ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="8ad79-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span></span>
* <span data-ttu-id="8ad79-236">sqlcmd.exe, che si connette tramite [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ad79-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span></span>

<span data-ttu-id="8ad79-237">Dopo la connessione, verificare il funzionamento di una breve query SQL SELECT.</span><span class="sxs-lookup"><span data-stu-id="8ad79-237">Once connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a><span data-ttu-id="8ad79-238">Diagnostica: Controllare le porte aperte hello</span><span class="sxs-lookup"><span data-stu-id="8ad79-238">Diagnostics: Check hello open ports</span></span>
<span data-ttu-id="8ad79-239">Si supponga che si ritiene che i tentativi di connessione hanno esito negativo a causa di problemi di tooport.</span><span class="sxs-lookup"><span data-stu-id="8ad79-239">Suppose you suspect that connection attempts are failing due tooport issues.</span></span> <span data-ttu-id="8ad79-240">Il computer è possibile eseguire un'utilità che consenta di segnalare le configurazioni delle porte hello.</span><span class="sxs-lookup"><span data-stu-id="8ad79-240">On your computer you can run a utility that reports on hello port configurations.</span></span>

<span data-ttu-id="8ad79-241">In Linux hello utilità seguenti potrebbero risultare utili:</span><span class="sxs-lookup"><span data-stu-id="8ad79-241">On Linux hello following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="8ad79-242">(Modifica hello esempio valore toobe l'indirizzo IP.)</span><span class="sxs-lookup"><span data-stu-id="8ad79-242">(Change hello example value toobe your IP address.)</span></span>

<span data-ttu-id="8ad79-243">In Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) può risultare utile.</span><span class="sxs-lookup"><span data-stu-id="8ad79-243">On Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="8ad79-244">Ecco un'esecuzione di esempio che query situazione porta hello in un server di Database SQL di Azure e che è stato eseguito in un computer portatile:</span><span class="sxs-lookup"><span data-stu-id="8ad79-244">Here is an example execution that queried hello port situation on an Azure SQL Database server, and which was run on a laptop computer:</span></span>

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="8ad79-245">Diagnostica: registrare gli errori</span><span class="sxs-lookup"><span data-stu-id="8ad79-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="8ad79-246">La diagnosi di un problema intermittente è spesso agevolata dal rilevamento di uno schema generale nel corso di giorni o settimane.</span><span class="sxs-lookup"><span data-stu-id="8ad79-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="8ad79-247">Il client può supportare l'analisi tramite la registrazione di tutti gli errori rilevati.</span><span class="sxs-lookup"><span data-stu-id="8ad79-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="8ad79-248">Potrebbe essere in grado di toocorrelate voci di log hello con i dati di errore di Database SQL di Azure stesso internamente.</span><span class="sxs-lookup"><span data-stu-id="8ad79-248">You might be able toocorrelate hello log entries with error data that Azure SQL Database logs itself internally.</span></span>

<span data-ttu-id="8ad79-249">Enterprise Library 6 (EntLib60) offre tooassist classi gestite .NET con la registrazione:</span><span class="sxs-lookup"><span data-stu-id="8ad79-249">Enterprise Library 6 (EntLib60) offers .NET managed classes tooassist with logging:</span></span>

* [<span data-ttu-id="8ad79-250">5 - come semplice come fallback disattivazione di un Log: utilizzando hello blocco applicazione per la registrazione</span><span class="sxs-lookup"><span data-stu-id="8ad79-250">5 - As Easy As Falling Off a Log: Using hello Logging Application Block</span></span>](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="8ad79-251">Diagnostica: cercare errori nei log di sistema</span><span class="sxs-lookup"><span data-stu-id="8ad79-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="8ad79-252">Ecco alcune istruzioni Transact-SQL SELECT che eseguono query nei log alla ricerca di errori e di altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="8ad79-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span></span>

| <span data-ttu-id="8ad79-253">Query di un log</span><span class="sxs-lookup"><span data-stu-id="8ad79-253">Query of log</span></span> | <span data-ttu-id="8ad79-254">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8ad79-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="8ad79-255">Hello [Sys. event_log](http://msdn.microsoft.com/library/dn270018.aspx) Vista offre informazioni sui singoli eventi, inclusi alcuni che possono causare errori temporanei o gli errori di connettività.</span><span class="sxs-lookup"><span data-stu-id="8ad79-255">hello [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="8ad79-256">In teoria è possibile correlare hello **start_time** o **end_time** valori con le informazioni quando il programma client si sono verificati problemi.</span><span class="sxs-lookup"><span data-stu-id="8ad79-256">Ideally you can correlate hello **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="8ad79-257">**Suggerimento:** è necessario connettersi toohello **master** database toorun questo.</span><span class="sxs-lookup"><span data-stu-id="8ad79-257">**TIP:** You must connect toohello **master** database toorun this.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="8ad79-258">Hello [Sys. database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) visualizzazione offre i conteggi aggregati di tipi di evento, per ulteriori operazioni di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="8ad79-258">hello [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span></span><br/><br/><span data-ttu-id="8ad79-259">**Suggerimento:** è necessario connettersi toohello **master** database toorun questo.</span><span class="sxs-lookup"><span data-stu-id="8ad79-259">**TIP:** You must connect toohello **master** database toorun this.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a><span data-ttu-id="8ad79-260">Diagnostica: Ricerca gli eventi di problemi nel Registro di Database SQL di hello</span><span class="sxs-lookup"><span data-stu-id="8ad79-260">Diagnostics: Search for problem events in hello SQL Database log</span></span>
<span data-ttu-id="8ad79-261">È possibile cercare le voci relative a eventi problema nel registro eventi di hello del Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ad79-261">You can search for entries about problem events in hello log of Azure SQL Database.</span></span> <span data-ttu-id="8ad79-262">Provare a hello seguente istruzione Transact-SQL SELECT in hello **master** database:</span><span class="sxs-lookup"><span data-stu-id="8ad79-262">Try hello following Transact-SQL SELECT statement in hello **master** database:</span></span>

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="8ad79-263">Alcune righe restituite da sys.fn_xe_telemetry_blob_target_read_file</span><span class="sxs-lookup"><span data-stu-id="8ad79-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="8ad79-264">Una riga restituita avrà un aspetto analogo al seguente.</span><span class="sxs-lookup"><span data-stu-id="8ad79-264">Next is what a returned row might look like.</span></span> <span data-ttu-id="8ad79-265">i valori null di Hello illustrati sono spesso non null in altre righe.</span><span class="sxs-lookup"><span data-stu-id="8ad79-265">hello null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="8ad79-266">Enterprise Library 6</span><span class="sxs-lookup"><span data-stu-id="8ad79-266">Enterprise Library 6</span></span>
<span data-ttu-id="8ad79-267">Enterprise Library 6 (EntLib60) è un framework di classi .NET che consente di implementare un client affidabile di servizi cloud, uno dei quali è il servizio di Database SQL di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8ad79-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is hello Azure SQL Database service.</span></span> <span data-ttu-id="8ad79-268">È possibile individuare l'area tooeach dedicato di argomenti in cui EntLib60 può fornire supporto visitando prima:</span><span class="sxs-lookup"><span data-stu-id="8ad79-268">You can locate topics dedicated tooeach area in which EntLib60 can assist by first visiting:</span></span>

* [<span data-ttu-id="8ad79-269">Enterprise Library 6 - Aprile 2013</span><span class="sxs-lookup"><span data-stu-id="8ad79-269">Enterprise Library 6 - April 2013</span></span>](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

<span data-ttu-id="8ad79-270">Logica di ripetizione dei tentativi per la gestione degli errori temporanei è un'area in cui EntLib60 può essere utile:</span><span class="sxs-lookup"><span data-stu-id="8ad79-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span></span>

* [<span data-ttu-id="8ad79-271">4 - perseverance, segreto del luogo tutti: utilizzando hello Transient Fault Handling Application Block</span><span class="sxs-lookup"><span data-stu-id="8ad79-271">4 - Perseverance, Secret of All Triumphs: Using hello Transient Fault Handling Application Block</span></span>](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> <span data-ttu-id="8ad79-272">Hello codice sorgente per EntLib60 è disponibile per public [scaricare](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span><span class="sxs-lookup"><span data-stu-id="8ad79-272">hello source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="8ad79-273">Microsoft non dispone di alcuna funzionalità di piani toomake ulteriori aggiornamenti o manutenzione aggiornamenti tooEntLib.</span><span class="sxs-lookup"><span data-stu-id="8ad79-273">Microsoft has no plans toomake further feature updates or maintenance updates tooEntLib.</span></span>
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="8ad79-274">Classi di EntLib60 per errori temporanei e ripetizione dei tentativi</span><span class="sxs-lookup"><span data-stu-id="8ad79-274">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="8ad79-275">le seguenti classi EntLib60 Hello sono particolarmente utile per la logica di ripetizione.</span><span class="sxs-lookup"><span data-stu-id="8ad79-275">hello following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="8ad79-276">Tutti questi sono in, o sotto, hello dello spazio dei nomi **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span><span class="sxs-lookup"><span data-stu-id="8ad79-276">All these  are in, or are further under, hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

<span data-ttu-id="8ad79-277">*Nello spazio dei nomi hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span><span class="sxs-lookup"><span data-stu-id="8ad79-277">*In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span></span>

* <span data-ttu-id="8ad79-278">**RetryPolicy**</span><span class="sxs-lookup"><span data-stu-id="8ad79-278">**RetryPolicy** class</span></span>
  
  * <span data-ttu-id="8ad79-279">**ExecuteAction**</span><span class="sxs-lookup"><span data-stu-id="8ad79-279">**ExecuteAction** method</span></span>
* <span data-ttu-id="8ad79-280">**ExponentialBackoff**</span><span class="sxs-lookup"><span data-stu-id="8ad79-280">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="8ad79-281">**SqlDatabaseTransientErrorDetectionStrategy**</span><span class="sxs-lookup"><span data-stu-id="8ad79-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="8ad79-282">**ReliableSqlConnection**</span><span class="sxs-lookup"><span data-stu-id="8ad79-282">**ReliableSqlConnection** class</span></span>
  
  * <span data-ttu-id="8ad79-283">**ExecuteCommand**</span><span class="sxs-lookup"><span data-stu-id="8ad79-283">**ExecuteCommand** method</span></span>

<span data-ttu-id="8ad79-284">Nello spazio dei nomi hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span><span class="sxs-lookup"><span data-stu-id="8ad79-284">In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="8ad79-285">**AlwaysTransientErrorDetectionStrategy**</span><span class="sxs-lookup"><span data-stu-id="8ad79-285">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="8ad79-286">**NeverTransientErrorDetectionStrategy**</span><span class="sxs-lookup"><span data-stu-id="8ad79-286">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="8ad79-287">Di seguito sono collegamenti tooinformation su EntLib60:</span><span class="sxs-lookup"><span data-stu-id="8ad79-287">Here are links tooinformation about EntLib60:</span></span>

* <span data-ttu-id="8ad79-288">Libera [Download della Rubrica: tooMicrosoft Guida per gli sviluppatori Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span><span class="sxs-lookup"><span data-stu-id="8ad79-288">Free [Book Download: Developer's Guide tooMicrosoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span></span>
* <span data-ttu-id="8ad79-289">Procedure consigliate: [Indicazioni generali per la ripetizione di tentativi](../best-practices-retry-general.md) offre un'eccellente discussione approfondita della logica di ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="8ad79-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="8ad79-290">Download NuGet di [Enterprise Library - Blocco applicazione per la gestione di errori temporanei 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span><span class="sxs-lookup"><span data-stu-id="8ad79-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a><span data-ttu-id="8ad79-291">EntLib60: blocco di registrazione hello</span><span class="sxs-lookup"><span data-stu-id="8ad79-291">EntLib60: hello logging block</span></span>
* <span data-ttu-id="8ad79-292">blocco di registrazione Hello è una soluzione estremamente flessibile e configurabile che consente di:</span><span class="sxs-lookup"><span data-stu-id="8ad79-292">hello Logging block is a highly flexible and configurable solution that allows you to:</span></span>
  
  * <span data-ttu-id="8ad79-293">Creare e archiviare messaggi di log in diverse posizioni.</span><span class="sxs-lookup"><span data-stu-id="8ad79-293">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="8ad79-294">Classificare e filtrare i messaggi.</span><span class="sxs-lookup"><span data-stu-id="8ad79-294">Categorize and filter messages.</span></span>
  * <span data-ttu-id="8ad79-295">Raccogliere informazioni contestuali utili per il debug e la traccia, oltre che per i requisiti di controllo e di registrazione generale.</span><span class="sxs-lookup"><span data-stu-id="8ad79-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="8ad79-296">blocco registrazione Hello astrae hello la funzionalità di registrazione dalla destinazione del log hello in modo che il codice dell'applicazione hello è coerenza, indipendentemente dalla posizione hello e il tipo di archivio di registrazione di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="8ad79-296">hello Logging block abstracts hello logging functionality from hello log destination so that hello application code is consistent, irrespective of hello location and type of hello target logging store.</span></span>

<span data-ttu-id="8ad79-297">Per informazioni dettagliate, vedere: [5 - come semplice come fallback disattivazione di un Log: utilizzando hello blocco applicazione per la registrazione](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="8ad79-297">For details see: [5 - As Easy As Falling Off a Log: Using hello Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="8ad79-298">Codice sorgente del metodo IsTransient di EntLib60</span><span class="sxs-lookup"><span data-stu-id="8ad79-298">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="8ad79-299">Successivamente, da hello **SqlDatabaseTransientErrorDetectionStrategy** classe, è il codice sorgente c# hello per hello **IsTransient** metodo.</span><span class="sxs-lookup"><span data-stu-id="8ad79-299">Next, from hello **SqlDatabaseTransientErrorDetectionStrategy** class, is hello C# source code for hello **IsTransient** method.</span></span> <span data-ttu-id="8ad79-300">codice sorgente Hello chiarisce gli errori sono stati considerati toobe temporaneo e richiedere un nuovo tentativo, a partire da aprile 2013.</span><span class="sxs-lookup"><span data-stu-id="8ad79-300">hello source code clarifies which errors were considered toobe transient and worthy of retry, as of April 2013.</span></span>

<span data-ttu-id="8ad79-301">Numerosi **//comment** righe sono state rimosse da questo leggibilità tooemphasize copia.</span><span class="sxs-lookup"><span data-stu-id="8ad79-301">Numerous **//comment** lines have been removed from this copy tooemphasize readability.</span></span>

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // hello instance of SQL Server you attempted tooconnect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a><span data-ttu-id="8ad79-302">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8ad79-302">Next steps</span></span>
* <span data-ttu-id="8ad79-303">Per risolvere altri problemi di connessione Database SQL di Azure, visitare [connessione di risolvere i problemi tooAzure Database SQL](sql-database-troubleshoot-common-connection-issues.md).</span><span class="sxs-lookup"><span data-stu-id="8ad79-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues tooAzure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="8ad79-304">Pool di connessioni di SQL Server (ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="8ad79-304">SQL Server Connection Pooling (ADO.NET)</span></span>](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [<span data-ttu-id="8ad79-305">*Nuovo tentativo* è generica nuovo tentativo di libreria, scritta in una licenza di Apache 2.0 **Python**, attività hello toosimplify aggiunta toojust comportamento di ripetizione su un valore.</span><span class="sxs-lookup"><span data-stu-id="8ad79-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, toosimplify hello task of adding retry behavior toojust about anything.</span></span>](https://pypi.python.org/pypi/retrying)

