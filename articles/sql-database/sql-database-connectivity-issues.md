---
title: Correggere un errore di connessione SQL temporaneo | Documentazione Microsoft
description: 'Informazioni su come risolvere, diagnosticare ed evitare un errore di connessione SQL o errore temporaneo nel database SQL di Azure. '
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
ms.openlocfilehash: ae081fc0432e36bf9f4d4f06f289386ddce37990
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="aa4b0-104">Risolvere, diagnosticare ed evitare gli errori di connessione SQL e gli errori temporanei per il database SQL</span><span class="sxs-lookup"><span data-stu-id="aa4b0-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="aa4b0-105">Questo articolo illustra come evitare, risolvere, diagnosticare e ridurre gli errori di connessione e gli errori temporanei che si verificano nell'applicazione client durante l'interazione con il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-105">This article describes how to prevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="aa4b0-106">Informazioni su come configurare la logica di ripetizione dei tentativi, compilare la stringa di connessione e modificare altre impostazioni di connessione.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-106">Learn how to configure retry logic, build the connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="aa4b0-107">Errori temporanei</span><span class="sxs-lookup"><span data-stu-id="aa4b0-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="aa4b0-108">Un errore temporaneo è un errore la cui causa sottostante si risolverà automaticamente in modo rapido.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span></span> <span data-ttu-id="aa4b0-109">Una causa occasionale di errori temporanei è costituita dal cambio rapido di risorse hardware da parte del sistema Azure per ottenere un bilanciamento migliore dei diversi carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-109">An occasional cause of transient errors is when the Azure system quickly shifts hardware resources to better load-balance various workloads.</span></span> <span data-ttu-id="aa4b0-110">La maggior parte di questi eventi di riconfigurazione spesso viene completata in meno di 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-110">Most of these reconfiguration events often complete in less than 60 seconds.</span></span> <span data-ttu-id="aa4b0-111">Durante questo intervallo di riconfigurazione possono verificarsi problemi di connessione al database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-111">During this reconfiguration time span, you may have connectivity issues to Azure SQL Database.</span></span> <span data-ttu-id="aa4b0-112">Le applicazioni che si connettono al database SQL di Azure devono essere create in modo da prevedere questi errori temporanei, gestirli implementando la logica di ripetizione dei tentativi nel codice anziché visualizzandoli agli utenti come errori dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-112">Applications connecting to Azure SQL Database should be built to expect these transient errors, handle them by implementing retry logic in their code instead of surfacing them to users as application errors.</span></span>

<span data-ttu-id="aa4b0-113">Se il programma client usa ADO.NET, l'errore temporaneo verrà segnalato al programma tramite la generazione di un'eccezione **SqlException**.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-113">If your client program is using ADO.NET, your program is told about the transient error by the throw of an **SqlException**.</span></span> <span data-ttu-id="aa4b0-114">È possibile confrontare la proprietà **Number** con l'elenco di errori temporanei disponibili nella parte iniziale dell'argomento [Codici di errore SQL per applicazioni client del database SQL](sql-database-develop-error-messages.md).</span><span class="sxs-lookup"><span data-stu-id="aa4b0-114">The **Number** property can be compared against the list of transient errors near the top of the topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="aa4b0-115">Confronto tra connessione e comando</span><span class="sxs-lookup"><span data-stu-id="aa4b0-115">Connection versus command</span></span>
<span data-ttu-id="aa4b0-116">È possibile riprovare a stabilire la connessione SQL o stabilirne una nuova, in base a quanto indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-116">You'll retry the SQL connection or establish it again, depending on the following:</span></span>

* <span data-ttu-id="aa4b0-117">**Si verifica un errore temporaneo durante un tentativo di connessione**: riprovare a stabilire la connessione dopo un intervallo di alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-117">**A transient error occurs during a connection try**: The connection should be retried after delaying for several seconds.</span></span>
* <span data-ttu-id="aa4b0-118">**Si verifica un errore temporaneo durante un comando di query SQL**: non riprovare immediatamente a eseguire il comando.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-118">**A transient error occurs during a SQL query command**: The command should not be immediately retried.</span></span> <span data-ttu-id="aa4b0-119">È invece consigliabile stabilire una nuova connessione dopo un breve intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-119">Instead, after a delay, the connection should be freshly established.</span></span> <span data-ttu-id="aa4b0-120">Sarà quindi possibile provare a rieseguire il comando.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-120">Then the command can be retried.</span></span>

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="aa4b0-121">Logica di ripetizione dei tentativi per errori temporanei</span><span class="sxs-lookup"><span data-stu-id="aa4b0-121">Retry logic for transient errors</span></span>
<span data-ttu-id="aa4b0-122">I programmi client in cui occasionalmente si verifica un errore temporaneo sono più affidabili se contengono una logica di ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="aa4b0-123">Se il programma comunica con il database SQL di Azure tramite middleware di terze parti, chiedere al fornitore se il middleware include la logica di ripetizione dei tentativi per errori temporanei.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with the vendor whether the middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a><span data-ttu-id="aa4b0-124">Principi per la ripetizione dei tentativi</span><span class="sxs-lookup"><span data-stu-id="aa4b0-124">Principles for retry</span></span>
* <span data-ttu-id="aa4b0-125">È consigliabile ripetere un tentativo di stabilire una connessione se l'errore è temporaneo.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-125">An attempt to open a connection should be retried if the error is transient.</span></span>
* <span data-ttu-id="aa4b0-126">Non è consigliabile riprovare direttamente a eseguire un'istruzione SQL SELECT non riuscita con un errore temporaneo.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-126">A SQL SELECT statement that fails with a transient error should not be retried directly.</span></span>
  
  * <span data-ttu-id="aa4b0-127">Stabilire invece una nuova connessione e quindi provare a eseguire di nuovo l'istruzione SELECT.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-127">Instead, establish a fresh connection, and then retry the SELECT.</span></span>
* <span data-ttu-id="aa4b0-128">Quando un'istruzione SQL UPDATE non riesce con un errore temporaneo, è consigliabile stabilire una nuova connessione prima di provare a eseguire di nuovo l'istruzione UPDATE.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-128">When a SQL UPDATE statement fails with a transient error, a fresh connection should be established before the UPDATE is retried.</span></span>
  
  * <span data-ttu-id="aa4b0-129">La logica di ripetizione dei tentativi deve assicurare il completamento dell'intera transazione di database o il rollback dell'intera transazione.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-129">The retry logic must ensure that either the entire database transaction completed, or that the entire transaction is rolled back.</span></span>

#### <a name="other-considerations-for-retry"></a><span data-ttu-id="aa4b0-130">Altre considerazioni per la ripetizione dei tentativi</span><span class="sxs-lookup"><span data-stu-id="aa4b0-130">Other considerations for retry</span></span>
* <span data-ttu-id="aa4b0-131">Un programma batch avviato automaticamente dopo l'orario di lavoro e con completamento previsto prima del mattino può permettersi di attendere a lungo tra i diversi tentativi.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford to very patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="aa4b0-132">Un programma di interfaccia utente deve tenere conto della tendenza degli utenti a desistere dopo un'attesa troppo lunga.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-132">A user interface program should account for the human tendency to give up after too long a wait.</span></span>
  
  * <span data-ttu-id="aa4b0-133">La soluzione, tuttavia, non deve prevedere nuovi tentativi con intervalli di pochi secondi, perché un criterio simile può inondare il sistema con un numero eccessivo di richieste.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-133">However, the solution must not be to retry every few seconds, because that policy can flood the system with requests.</span></span>

#### <a name="interval-increase-between-retries"></a><span data-ttu-id="aa4b0-134">Incremento dell'intervallo tra i tentativi</span><span class="sxs-lookup"><span data-stu-id="aa4b0-134">Interval increase between retries</span></span>
<span data-ttu-id="aa4b0-135">È consigliabile attendere 5 secondi prima di riprovare.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-135">We recommend that you delay for 5 seconds before your first retry.</span></span> <span data-ttu-id="aa4b0-136">Al primo tentativo con un ritardo inferiore a 5 secondi, si rischia di sovraccaricare il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-136">Retrying after a delay shorter than 5 seconds risks overwhelming the cloud service.</span></span> <span data-ttu-id="aa4b0-137">Per ogni tentativo successivo, aumentare in modo esponenziale il ritardo, fino a un massimo di 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-137">For each subsequent retry the delay should grow exponentially, up to a maximum of 60 seconds.</span></span>

<span data-ttu-id="aa4b0-138">Per i client che usano ADO.NET, è disponibile una discussione sul *periodo di blocco* in [Pool di connessioni di SQL Server (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa4b0-138">A discussion of the *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="aa4b0-139">È anche possibile che si voglia impostare un numero massimo di nuovi tentativi prima dell'autoterminazione del programma.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-139">You might also want to set a maximum number of retries before the program self-terminates.</span></span>

#### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="aa4b0-140">Esempi di codice con logica di ripetizione dei tentativi</span><span class="sxs-lookup"><span data-stu-id="aa4b0-140">Code samples with retry logic</span></span>
<span data-ttu-id="aa4b0-141">Esempi di codice con logica di ripetizione dei tentativi in diversi linguaggi di programmazione sono disponibili in:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-141">Code samples with retry logic, in a variety of programming languages, are available at:</span></span>

* [<span data-ttu-id="aa4b0-142">Raccolte di connessioni per database SQL e Server SQL</span><span class="sxs-lookup"><span data-stu-id="aa4b0-142">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a><span data-ttu-id="aa4b0-143">Eseguire test sulla logica di ripetizione tentativi</span><span class="sxs-lookup"><span data-stu-id="aa4b0-143">Test your retry logic</span></span>
<span data-ttu-id="aa4b0-144">Per testare la logica di ripetizione dei tentativi, è necessario simulare o provocare un errore che può essere corretto mentre il programma è ancora in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-144">To test your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span></span>

##### <a name="test-by-disconnecting-from-the-network"></a><span data-ttu-id="aa4b0-145">Eseguire il test mediante la disconnessione dalla rete</span><span class="sxs-lookup"><span data-stu-id="aa4b0-145">Test by disconnecting from the network</span></span>
<span data-ttu-id="aa4b0-146">Uno dei modi per testare la logica di ripetizione dei tentativi consiste nel disconnettere il computer client dalla rete mentre il programma è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-146">One way you can test your retry logic is to disconnect your client computer from the network while the program is running.</span></span> <span data-ttu-id="aa4b0-147">Verrà visualizzato un errore analogo a:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-147">The error will be:</span></span>

* <span data-ttu-id="aa4b0-148">**SqlException.Number** = 11001</span><span class="sxs-lookup"><span data-stu-id="aa4b0-148">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="aa4b0-149">Messaggio: "Host sconosciuto"</span><span class="sxs-lookup"><span data-stu-id="aa4b0-149">Message: "No such host is known"</span></span>

<span data-ttu-id="aa4b0-150">Come parte del primo tentativo, il programma può correggere l'errore di digitazione e quindi provare a connettersi.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-150">As part of the first retry attempt, your program can correct the misspelling, and then attempt to connect.</span></span>

<span data-ttu-id="aa4b0-151">Per semplificare le operazioni, disconnettere il computer dalla rete prima di avviare il programma.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-151">To make this practical, you unplug your computer from the network before you start your program.</span></span> <span data-ttu-id="aa4b0-152">Il programma riconoscerà quindi un parametro di runtime che ha le conseguenze seguenti sul programma:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-152">Then your program recognizes a run time parameter that causes the program to:</span></span>

1. <span data-ttu-id="aa4b0-153">Aggiunta temporanea di 11001 al rispettivo elenco di errori da considerare temporanei.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-153">Temporarily add 11001 to its list of errors to consider as transient.</span></span>
2. <span data-ttu-id="aa4b0-154">Tentativo della prima connessione come di consueto.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-154">Attempt its first connection as usual.</span></span>
3. <span data-ttu-id="aa4b0-155">Dopo il rilevamento dell'errore, rimozione di 11001 dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-155">After the error is caught, remove 11001 from the list.</span></span>
4. <span data-ttu-id="aa4b0-156">Visualizzazione di un messaggio che richiede all'utente di connettere il computer alla rete.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-156">Display a message telling the user to plug the computer into the network.</span></span>
   * <span data-ttu-id="aa4b0-157">Sospensione delle ulteriori esecuzioni con il metodo **Console.ReadLine** o una finestra di dialogo con un pulsante OK.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-157">Pause further execution by using either the **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="aa4b0-158">L'utente preme il tasto INVIO dopo la connessione del computer alla rete.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-158">The user presses the Enter key after the computer plugged into the network.</span></span>
5. <span data-ttu-id="aa4b0-159">Nuovo tentativo di connessione, con esito positivo previsto.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-159">Attempt again to connect, expecting success.</span></span>

##### <a name="test-by-misspelling-the-database-name-when-connecting"></a><span data-ttu-id="aa4b0-160">Eseguire il test mediante la digitazione non corretta del nome del database durante la connessione</span><span class="sxs-lookup"><span data-stu-id="aa4b0-160">Test by misspelling the database name when connecting</span></span>
<span data-ttu-id="aa4b0-161">Il programma può intenzionalmente digitare in modo errato il nome utente prima del primo tentativo di connessione.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-161">Your program can purposely misspell the user name before the first connection attempt.</span></span> <span data-ttu-id="aa4b0-162">Verrà visualizzato un errore analogo a:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-162">The error will be:</span></span>

* <span data-ttu-id="aa4b0-163">**SqlException.Number** = 18456</span><span class="sxs-lookup"><span data-stu-id="aa4b0-163">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="aa4b0-164">Messaggio: "Accesso non riuscito per l'utente 'WRONG_MyUserName'."</span><span class="sxs-lookup"><span data-stu-id="aa4b0-164">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="aa4b0-165">Come parte del primo tentativo, il programma può correggere l'errore di digitazione e quindi provare a connettersi.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-165">As part of the first retry attempt, your program can correct the misspelling, and then attempt to connect.</span></span>

<span data-ttu-id="aa4b0-166">Per semplificare le operazioni, il programma potrebbe riconoscere un parametro di runtime che ha le conseguenze seguenti sul programma:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-166">To make this practical, your program could recognize a run time parameter that causes the program to:</span></span>

1. <span data-ttu-id="aa4b0-167">Aggiunta temporanea di 18456 al rispettivo elenco di errori da considerare temporanei.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-167">Temporarily add 18456 to its list of errors to consider as transient.</span></span>
2. <span data-ttu-id="aa4b0-168">Aggiunta intenzionale di 'WRONG_' al nome utente.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-168">Purposely add 'WRONG_' to the user name.</span></span>
3. <span data-ttu-id="aa4b0-169">Dopo il rilevamento dell'errore, rimozione di 18456 dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-169">After the error is caught, remove 18456 from the list.</span></span>
4. <span data-ttu-id="aa4b0-170">Rimozione di 'WRONG_' dal nome utente.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-170">Remove 'WRONG_' from the user name.</span></span>
5. <span data-ttu-id="aa4b0-171">Nuovo tentativo di connessione, con esito positivo previsto.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-171">Attempt again to connect, expecting success.</span></span>

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="aa4b0-172">Parametri di SqlConnection di .NET per nuovi tentativi di connessione</span><span class="sxs-lookup"><span data-stu-id="aa4b0-172">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="aa4b0-173">Se il programma client si connette al database SQL di Azure usando la classe **System.Data.SqlClient.SqlConnection**, è necessario usare .NET 4.6.1 o versioni successive (o .NET Core) per poterne sfruttare la funzionalità di ripetizione dei tentativi di connessione.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-173">If your client program connects to to Azure SQL Database by using the .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span></span> <span data-ttu-id="aa4b0-174">Per conoscere i dettagli della funzionalità, vedere [qui](http://go.microsoft.com/fwlink/?linkid=393996).</span><span class="sxs-lookup"><span data-stu-id="aa4b0-174">Details of the feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points to dn632678.aspx, which links to a downloadable .docx related to SqlClient and SQL Server 2014.
-->


<span data-ttu-id="aa4b0-175">Quando si crea la [stringa di connessione](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) per l'oggetto **SqlConnection** , è necessario coordinare i valori tra i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-175">When you build the [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate the values among the following parameters:</span></span>

* <span data-ttu-id="aa4b0-176">ConnectRetryCount &nbsp;&nbsp;*(Il valore predefinito è 1. L'intervallo consentito è tra 0 e 255.)*</span><span class="sxs-lookup"><span data-stu-id="aa4b0-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span></span>
* <span data-ttu-id="aa4b0-177">ConnectRetryInterval &nbsp;&nbsp;*(Il valore predefinito è 1 secondo. L'intervallo consentito è tra 1 e 60.)*</span><span class="sxs-lookup"><span data-stu-id="aa4b0-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span></span>
* <span data-ttu-id="aa4b0-178">Timeout di connessione &nbsp;&nbsp;*(Il valore predefinito è 15 secondi. L'intervallo consentito è tra 0 e 2147483647)*</span><span class="sxs-lookup"><span data-stu-id="aa4b0-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span></span>

<span data-ttu-id="aa4b0-179">In particolare, i valori scelti devono rendere vera l'eguaglianza seguente:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-179">Specifically, your chosen values should make the following equality true:</span></span>

* <span data-ttu-id="aa4b0-180">Timeout di connessione = ConnectRetryCount * ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="aa4b0-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span></span>

<span data-ttu-id="aa4b0-181">Ad esempio, se il numero = 3 e l'intervallo = 10 secondi, un timeout di soli 29 secondi non garantirebbe al sistema il tempo sufficiente per il terzo tentativo e il tentativo di connessione finale: 29 < 3 * 10.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-181">For example, if the count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give the system enough time for its 3rd and final retry at connecting: 29 < 3 * 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="aa4b0-182">Confronto tra connessione e comando</span><span class="sxs-lookup"><span data-stu-id="aa4b0-182">Connection versus command</span></span>
<span data-ttu-id="aa4b0-183">I parametri **ConnectRetryCount** e **ConnectRetryInterval** consentono all'oggetto **SqlConnection** di ripetere l'operazione di connessione senza interferire con il programma, ad esempio per restituire il controllo al programma.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-183">The **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry the connect operation without telling or bothering your program, such as returning control to your program.</span></span> <span data-ttu-id="aa4b0-184">I tentativi possono verificarsi nelle situazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-184">The retries can occur in the following situations:</span></span>

* <span data-ttu-id="aa4b0-185">Chiamata al metodo mySqlConnection.Open</span><span class="sxs-lookup"><span data-stu-id="aa4b0-185">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="aa4b0-186">Chiamata al metodo mySqlConnection.Execute</span><span class="sxs-lookup"><span data-stu-id="aa4b0-186">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="aa4b0-187">È importante sottolineare che,</span><span class="sxs-lookup"><span data-stu-id="aa4b0-187">There is a subtlety.</span></span> <span data-ttu-id="aa4b0-188">se si verifica un errore temporaneo durante l'esecuzione della *query*, l'oggetto **SqlConnection** non ripete l'operazione di connessione e certamente non ritenta l'esecuzione della query.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry the connect operation, and it certainly does not retry your query.</span></span> <span data-ttu-id="aa4b0-189">Prima di inviare la query per l'esecuzione, tuttavia, **SqlConnection** controlla rapidamente la connessione e,</span><span class="sxs-lookup"><span data-stu-id="aa4b0-189">However, **SqlConnection** very quickly checks the connection before sending your query for execution.</span></span> <span data-ttu-id="aa4b0-190">se viene rilevato un problema, **SqlConnection** ritenta l'operazione di connessione.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-190">If the quick check detects a connection problem, **SqlConnection** retries the connect operation.</span></span> <span data-ttu-id="aa4b0-191">Se il tentativo ha esito positivo, la query viene inviata per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-191">If the retry succeeds, you query is sent for execution.</span></span>

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="aa4b0-192">Opportunità di combinare ConnectRetryCount con la logica di ripetizione dei tentativi nell'applicazione</span><span class="sxs-lookup"><span data-stu-id="aa4b0-192">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="aa4b0-193">Si supponga che l'applicazione disponga di una logica di ripetizione dei tentativi particolarmente avanzata,</span><span class="sxs-lookup"><span data-stu-id="aa4b0-193">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="aa4b0-194">in cui l'operazione di connessione può essere ritentata fino a 4 volte.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-194">It might retry the connect operation 4 times.</span></span> <span data-ttu-id="aa4b0-195">Se si aggiunge **ConnectRetryInterval** e **ConnectRetryCount** = 3 alla stringa di connessione, il numero dei tentativi aumenterà a 4 * 3 = 12 tentativi.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 to your connection string, you will increase the retry count to 4 * 3 = 12 retries.</span></span> <span data-ttu-id="aa4b0-196">Un numero così elevato di tentativi potrebbe non essere consigliabile.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-196">You might not intend such a high number of retries.</span></span>

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-to-azure-sql-database"></a><span data-ttu-id="aa4b0-197">Connessioni al database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="aa4b0-197">Connections to Azure SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="aa4b0-198">Connessione: stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="aa4b0-198">Connection: Connection string</span></span>
<span data-ttu-id="aa4b0-199">La stringa di connessione necessaria per la connessione al database SQL di Azure è leggermente diversa dalla stringa usata per la connessione a Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-199">The connection string necessary for connecting to Azure SQL Database is slightly different from the string for connecting to Microsoft SQL Server.</span></span> <span data-ttu-id="aa4b0-200">È possibile copiare la stringa di connessione per il database dal [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="aa4b0-200">You can copy the connection string for your database from the [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="aa4b0-201">Connessione: indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="aa4b0-201">Connection: IP address</span></span>
<span data-ttu-id="aa4b0-202">È necessario configurare il server di database SQL in modo che accetti le comunicazioni dall'indirizzo IP del computer che ospita il programma client.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-202">You must configure the SQL Database server to accept communication from the IP address of the computer that hosts your client program.</span></span> <span data-ttu-id="aa4b0-203">Per eseguire questa operazione, modificare le impostazioni del firewall tramite il [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="aa4b0-203">You do this by editing the firewall settings through the [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="aa4b0-204">Se si dimentica di configurare l'indirizzo IP, il programma restituirà un messaggio di errore che indica l'indirizzo IP necessario.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-204">If you forget to configure the IP address, your program will fail with a handy error message that states the necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="aa4b0-205">Per altre informazioni, vedere [Procedura: Configurare le impostazioni del firewall nel database SQL](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="aa4b0-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span></span>

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="aa4b0-206">Connessione: porte</span><span class="sxs-lookup"><span data-stu-id="aa4b0-206">Connection: Ports</span></span>
<span data-ttu-id="aa4b0-207">È in genere sufficiente assicurarsi che la porta 1433 sia aperta per le comunicazioni in uscita nel computer che ospita il programma client.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-207">Typically you only need to ensure that port 1433 is open for outbound communication, on the computer that hosts you client program.</span></span>

<span data-ttu-id="aa4b0-208">Ad esempio, se il programma client è ospitato in un computer Windows, Windows Firewall nell'host consente di aprire la porta 1433:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-208">For example, when your client program is hosted on a Windows computer, the Windows Firewall on the host enables you to open port 1433:</span></span>

1. <span data-ttu-id="aa4b0-209">Aprire il Pannello di controllo</span><span class="sxs-lookup"><span data-stu-id="aa4b0-209">Open the Control Panel</span></span>
2. <span data-ttu-id="aa4b0-210">&gt; Tutti gli elementi del Pannello di controllo</span><span class="sxs-lookup"><span data-stu-id="aa4b0-210">&gt; All Control Panel Items</span></span>
3. <span data-ttu-id="aa4b0-211">&gt; Windows Firewall</span><span class="sxs-lookup"><span data-stu-id="aa4b0-211">&gt; Windows Firewall</span></span>
4. <span data-ttu-id="aa4b0-212">&gt; Impostazioni avanzate</span><span class="sxs-lookup"><span data-stu-id="aa4b0-212">&gt; Advanced Settings</span></span>
5. <span data-ttu-id="aa4b0-213">&gt; Regole in uscita</span><span class="sxs-lookup"><span data-stu-id="aa4b0-213">&gt; Outbound Rules</span></span>
6. <span data-ttu-id="aa4b0-214">&gt; Azioni</span><span class="sxs-lookup"><span data-stu-id="aa4b0-214">&gt; Actions</span></span>
7. <span data-ttu-id="aa4b0-215">&gt; Nuova regola</span><span class="sxs-lookup"><span data-stu-id="aa4b0-215">&gt; New Rule</span></span>

<span data-ttu-id="aa4b0-216">Se il programma client è ospitato in una macchina virtuale (VM) di Azure, vedere </span><span class="sxs-lookup"><span data-stu-id="aa4b0-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span></span><br/><span data-ttu-id="aa4b0-217">[Porte superiori a 1433 per ADO.NET 4.5 e il database SQL](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="aa4b0-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="aa4b0-218">Per informazioni generali sulla configurazione di porte e indirizzi IP, vedere [Firewall del database SQL di Azure](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="aa4b0-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a><span data-ttu-id="aa4b0-219">Connessione: ADO.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="aa4b0-219">Connection: ADO.NET 4.6.1</span></span>
<span data-ttu-id="aa4b0-220">Se il programma utilizza classi ADO.NET come **System.Data.SqlClient.SqlConnection** per la connessione al database SQL di Azure, è consigliabile utilizzare .NET Framework 4.6.1 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** to connect to Azure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span></span>

<span data-ttu-id="aa4b0-221">ADO.NET 4.6.1:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-221">ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="aa4b0-222">Per il database SQL di Azure, è possibile migliorare l'affidabilità aprendo una connessione con il metodo **SqlConnection.Open** .</span><span class="sxs-lookup"><span data-stu-id="aa4b0-222">For Azure SQL Database, there is improved reliability when you open a connection by using the **SqlConnection.Open** method.</span></span> <span data-ttu-id="aa4b0-223">Il metodo **Open** incorpora ora meccanismi di ripetizione dei tentativi di tipo "massimo sforzo" in risposta agli errori temporanei, per alcuni errori entro l'intervallo del timeout di connessione.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-223">The **Open** method now incorporates best effort retry mechanisms in response to transient faults, for certain errors within the Connection Timeout period.</span></span>
* <span data-ttu-id="aa4b0-224">Supporta il pool di connessioni,</span><span class="sxs-lookup"><span data-stu-id="aa4b0-224">Supports connection pooling.</span></span> <span data-ttu-id="aa4b0-225">inclusa una verifica efficiente del funzionamento dell'oggetto connessione fornito al programma.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-225">This includes an efficient verification that the connection object it gives your program is functioning.</span></span>

<span data-ttu-id="aa4b0-226">Quando si usa un oggetto connessione da un pool di connessioni, è consigliabile che il programma chiuda temporaneamente la connessione se non deve essere usata immediatamente.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-226">When you use a connection object from a connection pool, we recommend that your program temporarily close the connection when not immediately using it.</span></span> <span data-ttu-id="aa4b0-227">La riapertura di una connessione è meno dispendiosa della creazione di una nuova connessione.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-227">Re-opening a connection is not expensive the way creating a new connection is.</span></span>

<span data-ttu-id="aa4b0-228">Se si usa ADO.NET 4.0 o versioni precedenti, è consigliabile eseguire l'aggiornamento alla versione più recente di ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade to the latest ADO.NET.</span></span>

* <span data-ttu-id="aa4b0-229">A partire da novembre 2015, è possibile [scaricare ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa4b0-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="aa4b0-230">Diagnostica</span><span class="sxs-lookup"><span data-stu-id="aa4b0-230">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="aa4b0-231">Diagnostica: verificare se le utilità si possono connettere</span><span class="sxs-lookup"><span data-stu-id="aa4b0-231">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="aa4b0-232">Se il programma non riesce a connettersi al database SQL di Azure, un'opzione di diagnostica consente di provare a connettersi mediante un programma di utilità.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-232">If your program is failing to connect to Azure SQL Database, one diagnostic option is to try to connect with a utility program.</span></span> <span data-ttu-id="aa4b0-233">Idealmente l'utilità si connette mediante la stessa libreria usata dal programma.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-233">Ideally the utility would connect by using the same library that your program uses.</span></span>

<span data-ttu-id="aa4b0-234">In qualsiasi computer Windows è possibile provare queste utilità:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-234">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="aa4b0-235">SQL Server Management Studio (ssms.exe), che si connette tramite ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span></span>
* <span data-ttu-id="aa4b0-236">sqlcmd.exe, che si connette tramite [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa4b0-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span></span>

<span data-ttu-id="aa4b0-237">Dopo la connessione, verificare il funzionamento di una breve query SQL SELECT.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-237">Once connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-the-open-ports"></a><span data-ttu-id="aa4b0-238">Diagnostica: verificare le porte aperte</span><span class="sxs-lookup"><span data-stu-id="aa4b0-238">Diagnostics: Check the open ports</span></span>
<span data-ttu-id="aa4b0-239">Si supponga che si sospetti che gli errori di connessione siano dovuti a problemi relativi alle porte.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-239">Suppose you suspect that connection attempts are failing due to port issues.</span></span> <span data-ttu-id="aa4b0-240">Nel computer è possibile eseguire un'utilità che fornisce informazioni sulle configurazioni delle porte.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-240">On your computer you can run a utility that reports on the port configurations.</span></span>

<span data-ttu-id="aa4b0-241">In Linux possono risultare utili le utilità seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-241">On Linux the following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="aa4b0-242">Modificare il valore di esempio con il proprio indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-242">(Change the example value to be your IP address.)</span></span>

<span data-ttu-id="aa4b0-243">In Windows è possibile usare l'utilità [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) .</span><span class="sxs-lookup"><span data-stu-id="aa4b0-243">On Windows the [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="aa4b0-244">Ecco un'esecuzione di esempio che ha eseguito una query relativa alla situazione delle porte in un server di database SQL di Azure e che è stata eseguita in un computer portatile:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-244">Here is an example execution that queried the port situation on an Azure SQL Database server, and which was run on a laptop computer:</span></span>

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting to resolve name to IP address...
Name resolved to 23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="aa4b0-245">Diagnostica: registrare gli errori</span><span class="sxs-lookup"><span data-stu-id="aa4b0-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="aa4b0-246">La diagnosi di un problema intermittente è spesso agevolata dal rilevamento di uno schema generale nel corso di giorni o settimane.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="aa4b0-247">Il client può supportare l'analisi tramite la registrazione di tutti gli errori rilevati.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="aa4b0-248">È possibile che si riesca a correlare le voci del log con i dati di errore registrati internamente dal database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-248">You might be able to correlate the log entries with error data that Azure SQL Database logs itself internally.</span></span>

<span data-ttu-id="aa4b0-249">Enterprise Library 6 (EntLib60) offre classi .NET gestite per semplificare la registrazione:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-249">Enterprise Library 6 (EntLib60) offers .NET managed classes to assist with logging:</span></span>

* [<span data-ttu-id="aa4b0-250">5 - Più facile che mai: Uso del blocco applicazione di registrazione</span><span class="sxs-lookup"><span data-stu-id="aa4b0-250">5 - As Easy As Falling Off a Log: Using the Logging Application Block</span></span>](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="aa4b0-251">Diagnostica: cercare errori nei log di sistema</span><span class="sxs-lookup"><span data-stu-id="aa4b0-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="aa4b0-252">Ecco alcune istruzioni Transact-SQL SELECT che eseguono query nei log alla ricerca di errori e di altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span></span>

| <span data-ttu-id="aa4b0-253">Query di un log</span><span class="sxs-lookup"><span data-stu-id="aa4b0-253">Query of log</span></span> | <span data-ttu-id="aa4b0-254">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aa4b0-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="aa4b0-255">La visualizzazione [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) offre informazioni sui singoli eventi, inclusi quelli che possono causare errori temporanei o di connettività.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-255">The [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="aa4b0-256">In teoria, è possibile correlare i valori **start_time** o **end_time** con le informazioni relative al momento in cui si sono verificati problemi nel programma client.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-256">Ideally you can correlate the **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="aa4b0-257">**SUGGERIMENTO**: è necessario connettersi al database **master** per eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-257">**TIP:** You must connect to the **master** database to run this.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="aa4b0-258">La vista [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) offre un conteggio aggregato dei tipi di evento, per consentire operazioni di diagnostica aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-258">The [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span></span><br/><br/><span data-ttu-id="aa4b0-259">**SUGGERIMENTO**: è necessario connettersi al database **master** per eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-259">**TIP:** You must connect to the **master** database to run this.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-the-sql-database-log"></a><span data-ttu-id="aa4b0-260">Diagnostica: cercare eventi relativi a problemi nel log del database SQL</span><span class="sxs-lookup"><span data-stu-id="aa4b0-260">Diagnostics: Search for problem events in the SQL Database log</span></span>
<span data-ttu-id="aa4b0-261">È possibile cercare voci relative agli eventi problematici nel log del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-261">You can search for entries about problem events in the log of Azure SQL Database.</span></span> <span data-ttu-id="aa4b0-262">Provare a eseguire l'istruzione Transact-SQL SELECT seguente nel database **master** :</span><span class="sxs-lookup"><span data-stu-id="aa4b0-262">Try the following Transact-SQL SELECT statement in the **master** database:</span></span>

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


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="aa4b0-263">Alcune righe restituite da sys.fn_xe_telemetry_blob_target_read_file</span><span class="sxs-lookup"><span data-stu-id="aa4b0-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="aa4b0-264">Una riga restituita avrà un aspetto analogo al seguente.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-264">Next is what a returned row might look like.</span></span> <span data-ttu-id="aa4b0-265">I valori Null mostrati sono spesso non Null in altre righe.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-265">The null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="aa4b0-266">Enterprise Library 6</span><span class="sxs-lookup"><span data-stu-id="aa4b0-266">Enterprise Library 6</span></span>
<span data-ttu-id="aa4b0-267">Enterprise Library 6 (EntLib60) è un framework di classi .NET che semplifica l'implementazione di client affidabili dei servizi cloud, ad esempio il servizio database SQL di Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is the Azure SQL Database service.</span></span> <span data-ttu-id="aa4b0-268">Gli argomenti dedicati a ogni area per cui EntLib60 può risultare utile sono disponibili in:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-268">You can locate topics dedicated to each area in which EntLib60 can assist by first visiting:</span></span>

* [<span data-ttu-id="aa4b0-269">Enterprise Library 6 - Aprile 2013</span><span class="sxs-lookup"><span data-stu-id="aa4b0-269">Enterprise Library 6 - April 2013</span></span>](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

<span data-ttu-id="aa4b0-270">Logica di ripetizione dei tentativi per la gestione degli errori temporanei è un'area in cui EntLib60 può essere utile:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span></span>

* [<span data-ttu-id="aa4b0-271">4 - Perseveranza, il segreto di ogni successo: Uso del blocco applicazione di gestione degli errori temporanei</span><span class="sxs-lookup"><span data-stu-id="aa4b0-271">4 - Perseverance, Secret of All Triumphs: Using the Transient Fault Handling Application Block</span></span>](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> <span data-ttu-id="aa4b0-272">Il codice sorgente per EntLib60 è disponibile per il [download](http://go.microsoft.com/fwlink/p/?LinkID=290898)pubblico.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-272">The source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="aa4b0-273">Microsoft non prevede di fornire altre funzionalità o aggiornamenti di manutenzione per EntLib.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-273">Microsoft has no plans to make further feature updates or maintenance updates to EntLib.</span></span>
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="aa4b0-274">Classi di EntLib60 per errori temporanei e ripetizione dei tentativi</span><span class="sxs-lookup"><span data-stu-id="aa4b0-274">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="aa4b0-275">Le classi seguenti di EntLib60 sono particolarmente utili per la logica di ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-275">The following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="aa4b0-276">Tutte queste classi sono disponibili nello spazio dei nomi **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling** o nei livelli sottostanti:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-276">All these  are in, or are further under, the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

<span data-ttu-id="aa4b0-277">*Nello spazio dei nomi **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span><span class="sxs-lookup"><span data-stu-id="aa4b0-277">*In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span></span>

* <span data-ttu-id="aa4b0-278">**RetryPolicy** </span><span class="sxs-lookup"><span data-stu-id="aa4b0-278">**RetryPolicy** class</span></span>
  
  * <span data-ttu-id="aa4b0-279">**ExecuteAction** </span><span class="sxs-lookup"><span data-stu-id="aa4b0-279">**ExecuteAction** method</span></span>
* <span data-ttu-id="aa4b0-280">**ExponentialBackoff** </span><span class="sxs-lookup"><span data-stu-id="aa4b0-280">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="aa4b0-281">**SqlDatabaseTransientErrorDetectionStrategy** </span><span class="sxs-lookup"><span data-stu-id="aa4b0-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="aa4b0-282">**ReliableSqlConnection** </span><span class="sxs-lookup"><span data-stu-id="aa4b0-282">**ReliableSqlConnection** class</span></span>
  
  * <span data-ttu-id="aa4b0-283">**ExecuteCommand** </span><span class="sxs-lookup"><span data-stu-id="aa4b0-283">**ExecuteCommand** method</span></span>

<span data-ttu-id="aa4b0-284">Nello spazio dei nomi **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-284">In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="aa4b0-285">**AlwaysTransientErrorDetectionStrategy** </span><span class="sxs-lookup"><span data-stu-id="aa4b0-285">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="aa4b0-286">**NeverTransientErrorDetectionStrategy** </span><span class="sxs-lookup"><span data-stu-id="aa4b0-286">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="aa4b0-287">Ecco i collegamenti alle informazioni relative a EntLib60:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-287">Here are links to information about EntLib60:</span></span>

* <span data-ttu-id="aa4b0-288">[Download gratuito dell'eBook relativo alla Guida per gli sviluppatori di Microsoft Enterprise Library, seconda edizione](http://www.microsoft.com/download/details.aspx?id=41145)</span><span class="sxs-lookup"><span data-stu-id="aa4b0-288">Free [Book Download: Developer's Guide to Microsoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span></span>
* <span data-ttu-id="aa4b0-289">Procedure consigliate: [Indicazioni generali per la ripetizione di tentativi](../best-practices-retry-general.md) offre un'eccellente discussione approfondita della logica di ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="aa4b0-290">Download NuGet di [Enterprise Library - Blocco applicazione per la gestione di errori temporanei 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span><span class="sxs-lookup"><span data-stu-id="aa4b0-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-the-logging-block"></a><span data-ttu-id="aa4b0-291">EntLib60: il blocco di registrazione</span><span class="sxs-lookup"><span data-stu-id="aa4b0-291">EntLib60: The logging block</span></span>
* <span data-ttu-id="aa4b0-292">Il blocco di registrazione è una soluzione a flessibilità e configurabilità elevata che consente di:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-292">The Logging block is a highly flexible and configurable solution that allows you to:</span></span>
  
  * <span data-ttu-id="aa4b0-293">Creare e archiviare messaggi di log in diverse posizioni.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-293">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="aa4b0-294">Classificare e filtrare i messaggi.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-294">Categorize and filter messages.</span></span>
  * <span data-ttu-id="aa4b0-295">Raccogliere informazioni contestuali utili per il debug e la traccia, oltre che per i requisiti di controllo e di registrazione generale.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="aa4b0-296">Il blocco di registrazione astrae la funzionalità di registrazione dalla destinazione di registrazione, in modo che il codice applicazione sia coerente, indipendentemente dalla posizione e dal tipo di archivio di registrazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-296">The Logging block abstracts the logging functionality from the log destination so that the application code is consistent, irrespective of the location and type of the target logging store.</span></span>

<span data-ttu-id="aa4b0-297">Per informazioni dettagliate vedere [5 - Più facile che mai: uso del blocco applicazione di registrazione](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="aa4b0-297">For details see: [5 - As Easy As Falling Off a Log: Using the Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="aa4b0-298">Codice sorgente del metodo IsTransient di EntLib60</span><span class="sxs-lookup"><span data-stu-id="aa4b0-298">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="aa4b0-299">La classe **SqlDatabaseTransientErrorDetectionStrategy** include anche il codice sorgente C# per il metodo **IsTransient**.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-299">Next, from the **SqlDatabaseTransientErrorDetectionStrategy** class, is the C# source code for the **IsTransient** method.</span></span> <span data-ttu-id="aa4b0-300">Il codice sorgente chiarisce gli errori considerati temporanei e idonei alla ripetizione dei tentativi, a partire da aprile 2013.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-300">The source code clarifies which errors were considered to be transient and worthy of retry, as of April 2013.</span></span>

<span data-ttu-id="aa4b0-301">Molte righe **//comment** sono state rimosse da questa copia per migliorarne la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-301">Numerous **//comment** lines have been removed from this copy to emphasize readability.</span></span>

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in the exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // The service is currently busy. Retry the request after 10 seconds.
            // Code: (reason code to be decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode the reason code from the error message to
            // determine the grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach the decoded values as additional attributes to
            // the original SQL exception.
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
            // The instance of SQL Server you attempted to connect to
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


## <a name="next-steps"></a><span data-ttu-id="aa4b0-302">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aa4b0-302">Next steps</span></span>
* <span data-ttu-id="aa4b0-303">Per risolvere altri problemi di connessione del database SQL di Azure, visitare [Risoluzione dei problemi di connessione al database SQL di Azure](sql-database-troubleshoot-common-connection-issues.md).</span><span class="sxs-lookup"><span data-stu-id="aa4b0-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues to Azure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="aa4b0-304">Pool di connessioni di SQL Server (ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="aa4b0-304">SQL Server Connection Pooling (ADO.NET)</span></span>](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [<span data-ttu-id="aa4b0-305">*Retrying* è una libreria generica Apache 2.0 di ripetizione dei tentativi scritta in **Python** per semplificare l'attività di aggiunta del comportamento di ripetizione dei tentativi a qualsiasi codice.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, to simplify the task of adding retry behavior to just about anything.</span></span>](https://pypi.python.org/pypi/retrying)

