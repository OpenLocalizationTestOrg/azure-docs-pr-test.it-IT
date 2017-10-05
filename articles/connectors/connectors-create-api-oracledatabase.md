---
title: Aggiungere il connettore Oracle Database in App per la logica di Azure | Microsoft Docs
description: Usare il connettore Oracle Database in un'app per la logica
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: cc64441617eb5e7d5e70c1cf5c491a672428bc51
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-the-oracle-database-connector"></a><span data-ttu-id="e4e3a-103">Introduzione al connettore Oracle Database</span><span class="sxs-lookup"><span data-stu-id="e4e3a-103">Get started with the Oracle Database connector</span></span>

<span data-ttu-id="e4e3a-104">Usando il connettore Oracle Database, è possibile creare flussi di lavoro dell'organizzazione che usano i dati nel database esistente.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-104">Using the Oracle Database connector, you create organizational workflows that use data in your existing database.</span></span> <span data-ttu-id="e4e3a-105">Questo connettore può connettersi a un'istanza locale di Oracle Database o a una macchina virtuale di Azure con Oracle Database installato.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-105">This connector can connect to an on-premises Oracle Database, or an Azure virtual machine with Oracle Database installed.</span></span> <span data-ttu-id="e4e3a-106">Con questo connettore è possibile:</span><span class="sxs-lookup"><span data-stu-id="e4e3a-106">With this connector, you can:</span></span>

* <span data-ttu-id="e4e3a-107">Creare il flusso di lavoro aggiungendo un nuovo cliente in un database di clienti o aggiornando un ordine in un database di ordini.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-107">Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="e4e3a-108">Usare le azioni per ottenere una riga di dati, inserire una nuova riga e persino eliminare una riga.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-108">Use actions to get a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="e4e3a-109">Quando ad esempio viene creato un record in Dynamics CRM Online (trigger), è possibile inserire una riga in Oracle Database (azione).</span><span class="sxs-lookup"><span data-stu-id="e4e3a-109">For example, when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Oracle Database (an action).</span></span> 

<span data-ttu-id="e4e3a-110">Questo argomento illustra come usare il connettore Oracle Database in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-110">This topic shows you how to use the Oracle Database connector in a logic app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4e3a-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e4e3a-111">Prerequisites</span></span>

* <span data-ttu-id="e4e3a-112">Versioni di Oracle supportate:</span><span class="sxs-lookup"><span data-stu-id="e4e3a-112">Supported Oracle versions:</span></span> 
    * <span data-ttu-id="e4e3a-113">Oracle 9 e versioni successive</span><span class="sxs-lookup"><span data-stu-id="e4e3a-113">Oracle 9 and later</span></span>
    * <span data-ttu-id="e4e3a-114">Software client Oracle 8.1.7 e versioni successive</span><span class="sxs-lookup"><span data-stu-id="e4e3a-114">Oracle client software 8.1.7 and later</span></span>

* <span data-ttu-id="e4e3a-115">Installare il gateway dati locale.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-115">Install the on-premises data gateway.</span></span> <span data-ttu-id="e4e3a-116">Questi passaggi sono illustrati in [Connettersi ai dati locali dalle app per la logica](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="e4e3a-116">[Connect to on-premises data from logic apps](../logic-apps/logic-apps-gateway-connection.md) lists the steps.</span></span> <span data-ttu-id="e4e3a-117">Il gateway è necessario per connettersi a un'istanza locale di Oracle Database o a una VM di Azure con Oracle DB installato.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-117">The gateway is required to connect to an on-premises Oracle Database, or an Azure VM with Oracle DB installed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="e4e3a-118">Il gateway dati locale svolge la funzione di bridge e consente il trasferimento sicuro dei dati tra i dati locali (non nel cloud) e le app per la logica.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-118">The on-premises data gateway acts as a bridge, and provides a secure data transfer between on-premises data (data that is not in the cloud) and your logic apps.</span></span> <span data-ttu-id="e4e3a-119">Lo stesso gateway può essere anche usato con più servizi e più origini dati.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-119">The same gateway can be used with multiple services, and multiple data sources.</span></span> <span data-ttu-id="e4e3a-120">Potrebbe quindi essere necessario installare il gateway una sola volta.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-120">So, you may only need to install the gateway once.</span></span>

* <span data-ttu-id="e4e3a-121">Installare il client Oracle nella macchina in cui è stato installato il gateway dati locale.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-121">Install the Oracle Client on the machine where you installed the on-premises data gateway.</span></span> <span data-ttu-id="e4e3a-122">Assicurarsi di installare il provider di dati Oracle a 64 bit per .NET da Oracle:</span><span class="sxs-lookup"><span data-stu-id="e4e3a-122">Be sure to install the 64-bit Oracle Data Provider for .NET from Oracle:</span></span>  

  [<span data-ttu-id="e4e3a-123">ODAC 64 bit 12c versione 4 (12.1.0.2.4) per Windows x64</span><span class="sxs-lookup"><span data-stu-id="e4e3a-123">64-bit ODAC 12c Release 4 (12.1.0.2.4) for Windows x64</span></span>](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > <span data-ttu-id="e4e3a-124">Se il client Oracle non è installato, si verifica un errore quando si cerca di creare o usare la connessione.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-124">If the Oracle client is not installed, an error occurs when you try to create or use the connection.</span></span> <span data-ttu-id="e4e3a-125">Vedere gli errori comuni in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-125">See the common errors in this topic.</span></span>


## <a name="add-the-connector"></a><span data-ttu-id="e4e3a-126">Aggiungere il connettore</span><span class="sxs-lookup"><span data-stu-id="e4e3a-126">Add the connector</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4e3a-127">Questo connettore non include trigger.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-127">This connector does not have any triggers.</span></span> <span data-ttu-id="e4e3a-128">Ha solo azioni.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-128">It has only actions.</span></span> <span data-ttu-id="e4e3a-129">Quando si crea l'app per la logica, aggiungere quindi un altro trigger per avviare l'app per la logica, ad esempio **Pianificazione - Ricorrenza** o **Richiesta/Risposta - Risposta**.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-129">So when you create your logic app, add another trigger to start your logic app, such as **Schedule - Recurrence**, or **Request / Response - Response**.</span></span> 

1. <span data-ttu-id="e4e3a-130">Nel [portale di Azure](https://portal.azure.com) creare un'app per la logica vuota.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-130">In the [Azure portal](https://portal.azure.com), create a blank logic app.</span></span>

2. <span data-ttu-id="e4e3a-131">All'avvio dell'app per la logica, selezionare il trigger **Richiesta/Risposta - Risposta**:</span><span class="sxs-lookup"><span data-stu-id="e4e3a-131">At the start of your logic app, select the **Request / Response - Request** trigger:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. <span data-ttu-id="e4e3a-132">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-132">Select **Save**.</span></span> <span data-ttu-id="e4e3a-133">Quando si salva, viene generato automaticamente un URL di richiesta.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-133">When you save, a request URL is automatically generated.</span></span> 

4. <span data-ttu-id="e4e3a-134">Selezionare **Nuovo passaggio** e quindi **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-134">Select **New step**, and select **Add an action**.</span></span> <span data-ttu-id="e4e3a-135">Digitare `oracle` per visualizzare le azioni disponibili:</span><span class="sxs-lookup"><span data-stu-id="e4e3a-135">Type in `oracle` to see the available actions:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > <span data-ttu-id="e4e3a-136">Questo è anche il modo più rapido per visualizzare i trigger e le azioni disponibili per i connettori.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-136">This is also the quickest way to see the triggers and actions available for any connector.</span></span> <span data-ttu-id="e4e3a-137">Digitare parte del nome del connettore, ad esempio `oracle`.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-137">Type in part of the connector name, such as `oracle`.</span></span> <span data-ttu-id="e4e3a-138">La finestra di progettazione elenca i trigger e le azioni.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-138">The designer lists any triggers and any actions.</span></span> 

5. <span data-ttu-id="e4e3a-139">Selezionare una delle azioni, ad esempio **Oracle Database - Ottieni riga**.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-139">Select one of the actions, such as **Oracle Database - Get row**.</span></span> <span data-ttu-id="e4e3a-140">Selezionare **Connect via on-premises data gateway** (Connetti tramite gateway dati locale).</span><span class="sxs-lookup"><span data-stu-id="e4e3a-140">Select **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="e4e3a-141">Immettere il nome del server Oracle, il metodo di autenticazione, il nome utente e la password e selezionare il gateway:</span><span class="sxs-lookup"><span data-stu-id="e4e3a-141">Enter the Oracle server name, authentication method, username, password, and select the gateway:</span></span>

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. <span data-ttu-id="e4e3a-142">Una volta stabilita la connessione, selezionare una tabella nell'elenco e immettere l'ID di riga per la tabella.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-142">Once connected, select a table from the list, and enter the row ID to your table.</span></span> <span data-ttu-id="e4e3a-143">È necessario conoscere l'identificatore della tabella.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-143">You need to know the identifier to the table.</span></span> <span data-ttu-id="e4e3a-144">Se non lo si conosce, contattare l'amministratore di Oracle DB e ottenere l'output di `select * from yourTableName`.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-144">If you don't know, contact your Oracle DB administrator, and get the output from `select * from yourTableName`.</span></span> <span data-ttu-id="e4e3a-145">In questo modo si otterranno le informazioni di identificazione necessarie per procedere.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-145">This gives you the identifiable information you need to proceed.</span></span>

    <span data-ttu-id="e4e3a-146">Nell'esempio seguente i dati del processo vengono restituiti da un database delle risorse umane:</span><span class="sxs-lookup"><span data-stu-id="e4e3a-146">In the following example, job data is being returned from a Human Resources database:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. <span data-ttu-id="e4e3a-147">Nel passaggio successivo è possibile usare uno qualsiasi degli altri connettori per creare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-147">In this next step, you can use any of the other connectors to build your workflow.</span></span> <span data-ttu-id="e4e3a-148">Se si vuole provare a recuperare i dati da Oracle, inviare a se stessi un messaggio di posta elettronica con i dati di Oracle usando uno dei connettori di invio di posta elettronica, ad esempio Office 365 o Gmail.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-148">If you want to test getting data from Oracle, then send yourself an email with the Oracle data using one of the send email connectors, such Office 365 or Gmail.</span></span> <span data-ttu-id="e4e3a-149">Usare i token dinamici della tabella Oracle per creare `Subject` e `Body` del messaggio di posta elettronica:</span><span class="sxs-lookup"><span data-stu-id="e4e3a-149">Use the dynamic tokens from the Oracle table to build the `Subject` and `Body` of your email:</span></span>

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. <span data-ttu-id="e4e3a-150">**Salvare** l'app per la logica e quindi selezionare **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-150">**Save** your logic app, and then select **Run**.</span></span> <span data-ttu-id="e4e3a-151">Chiudere la finestra di progettazione ed esaminare lo stato nella cronologia delle esecuzioni.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-151">Close the designer, and look at the runs history for the status.</span></span> <span data-ttu-id="e4e3a-152">In caso di esito negativo, selezionare la riga relativa al messaggio non inviato.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-152">If it fails, select the failed message row.</span></span> <span data-ttu-id="e4e3a-153">La finestra di progettazione viene aperta e mostra il passaggio non riuscito, con le informazioni sull'errore.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-153">The designer opens, and shows you which step failed, and also shows the error information.</span></span> <span data-ttu-id="e4e3a-154">In caso di esito positivo, si dovrebbe ricevere un messaggio di posta elettronica con le informazioni aggiunte.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-154">If it succeeds, then you should receive an email with the information you added.</span></span>


### <a name="workflow-ideas"></a><span data-ttu-id="e4e3a-155">Idee per i flussi di lavoro</span><span class="sxs-lookup"><span data-stu-id="e4e3a-155">Workflow ideas</span></span>

* <span data-ttu-id="e4e3a-156">Si vuole monitorare l'hashtag #oracle e inserire i Tweet in un database in modo che sia possibile eseguire query su di essi e usarli in altre applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-156">You want to monitor the #oracle hashtag, and put the tweets in a database so they can be queried, and used within other applications.</span></span> <span data-ttu-id="e4e3a-157">In un'app per la logica aggiungere il trigger `Twitter - When a new tweet is posted` e immettere l'hashtag **#oracle**.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-157">In a logic app, add the `Twitter - When a new tweet is posted` trigger, and enter the **#oracle** hashtag.</span></span> <span data-ttu-id="e4e3a-158">Aggiungere quindi l'azione `Oracle Database - Insert row` e selezionare la tabella:</span><span class="sxs-lookup"><span data-stu-id="e4e3a-158">Then, add the `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* <span data-ttu-id="e4e3a-159">Messaggi inviati a una coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-159">Messages are sent to a Service Bus queue.</span></span> <span data-ttu-id="e4e3a-160">Si vuole ottenere questi messaggi e inserirli in un database.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-160">You want to get these messages, and put them in a database.</span></span> <span data-ttu-id="e4e3a-161">In un'app per la logica aggiungere il trigger `Service Bus - when a message is received in a queue` e selezionare la coda.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-161">In a logic app, add the `Service Bus - when a message is received in a queue` trigger, and select the queue.</span></span> <span data-ttu-id="e4e3a-162">Aggiungere quindi l'azione `Oracle Database - Insert row` e selezionare la tabella:</span><span class="sxs-lookup"><span data-stu-id="e4e3a-162">Then, add the `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a><span data-ttu-id="e4e3a-163">Errori comuni</span><span class="sxs-lookup"><span data-stu-id="e4e3a-163">Common errors</span></span>

#### <a name="error-cannot-reach-the-gateway"></a><span data-ttu-id="e4e3a-164">**Errore**: Non è possibile raggiungere il gateway</span><span class="sxs-lookup"><span data-stu-id="e4e3a-164">**Error**: Cannot reach the Gateway</span></span>

<span data-ttu-id="e4e3a-165">**Causa**: il gateway dati locale non è in grado di connettersi al cloud.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-165">**Cause**: The on-premises data gateway is not able to connect to the cloud.</span></span> 

<span data-ttu-id="e4e3a-166">**Mitigazione**: assicurarsi che il gateway sia in esecuzione nel computer locale in cui è stato installato e che sia in grado di connettersi a Internet.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-166">**Mitigation**: Make sure your gateway is running on the on-premises machine where you installed it, and that it can connect to the internet.</span></span>  <span data-ttu-id="e4e3a-167">È consigliabile non installare il gateway in un computer che potrebbe venire spento o andare in sospensione.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-167">We recommend not installing the gateway on a computer that may be turned off or sleep.</span></span> <span data-ttu-id="e4e3a-168">È anche possibile riavviare il servizio gateway dati locale (PBIEgwService).</span><span class="sxs-lookup"><span data-stu-id="e4e3a-168">You can also restart the on-premises data gateway service (PBIEgwService).</span></span>

#### <a name="error-the-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-to-install-the-official-provider"></a><span data-ttu-id="e4e3a-169">**Errore**: Il provider usato è deprecato: 'System.Data.OracleClient richiede il software client Oracle versione 8.1.7 o versione successiva.'</span><span class="sxs-lookup"><span data-stu-id="e4e3a-169">**Error**: The provider being used is deprecated: 'System.Data.OracleClient requires Oracle client software version 8.1.7 or greater.'.</span></span> <span data-ttu-id="e4e3a-170">Visitare il sito [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) per installare il provider ufficiale.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-170">Please visit [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) to install the official provider.</span></span>

<span data-ttu-id="e4e3a-171">**Causa**: Oracle client SDK non è installato nel computer in cui è in esecuzione il gateway dati locale.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-171">**Cause**: The Oracle client SDK is not installed on the machine where the on-premises data gateway is running.</span></span>  

<span data-ttu-id="e4e3a-172">**Risoluzione**: scaricare e installare Oracle client SDK nello stesso computer del gateway dati locale.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-172">**Resolution**: Download and install the Oracle client SDK on the same computer as the on-premises data gateway.</span></span>

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a><span data-ttu-id="e4e3a-173">**Errore**: La tabella '[NomeTabella]' non definisce alcuna colonna chiave</span><span class="sxs-lookup"><span data-stu-id="e4e3a-173">**Error**: Table '[Tablename]' does not define any key columns</span></span>

<span data-ttu-id="e4e3a-174">**Causa**: la tabella non ha alcuna chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-174">**Cause**: The table does not have any primary key.</span></span>  

<span data-ttu-id="e4e3a-175">**Risoluzione**: il connettore Oracle Database richiede l'uso di una tabella con una colonna chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-175">**Resolution**: The Oracle Database connector requires that a table with a primary key column be used.</span></span>

#### <a name="currently-not-supported"></a><span data-ttu-id="e4e3a-176">Attualmente non supportati</span><span class="sxs-lookup"><span data-stu-id="e4e3a-176">Currently not supported</span></span>

* <span data-ttu-id="e4e3a-177">Viste e stored procedure</span><span class="sxs-lookup"><span data-stu-id="e4e3a-177">Views and stored procedures</span></span> 
* <span data-ttu-id="e4e3a-178">Tabelle con chiavi composte</span><span class="sxs-lookup"><span data-stu-id="e4e3a-178">Any table with composite keys</span></span>
* <span data-ttu-id="e4e3a-179">Tipi di oggetti annidati nelle tabelle</span><span class="sxs-lookup"><span data-stu-id="e4e3a-179">Nested object types in tables</span></span>
 
## <a name="connector-specific-details"></a><span data-ttu-id="e4e3a-180">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="e4e3a-180">Connector-specific details</span></span>

<span data-ttu-id="e4e3a-181">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/oracle/).</span><span class="sxs-lookup"><span data-stu-id="e4e3a-181">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/oracle/).</span></span> 

## <a name="get-some-help"></a><span data-ttu-id="e4e3a-182">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="e4e3a-182">Get some help</span></span>

<span data-ttu-id="e4e3a-183">Il [forum di App per la logica di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) è il posto ideale per porre domande, fornire risposte e vedere cosa stanno facendo gli altri utenti di App per la logica.</span><span class="sxs-lookup"><span data-stu-id="e4e3a-183">The [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is a great place to ask questions, answer questions, and see what other Logic Apps users are doing.</span></span> 

<span data-ttu-id="e4e3a-184">È possibile migliorare App per la logica e i connettori votando e inviando le idee nella pagina [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="e4e3a-184">You can help improve Logic Apps and connectors by voting and submitting your ideas at [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span></span> 


## <a name="next-steps"></a><span data-ttu-id="e4e3a-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e4e3a-185">Next steps</span></span>
<span data-ttu-id="e4e3a-186">[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md) e scoprire i connettori disponibili in App per la logica nell'[elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e4e3a-186">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md), and explore the available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
