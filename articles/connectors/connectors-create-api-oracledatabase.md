---
title: connettore di Database Oracle aaaAdd hello nelle app di logica di Azure | Documenti Microsoft
description: Utilizzare il connettore di Oracle Database hello in un'app di logica
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
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a><span data-ttu-id="a25ce-103">Iniziare con il connettore hello Database Oracle</span><span class="sxs-lookup"><span data-stu-id="a25ce-103">Get started with hello Oracle Database connector</span></span>

<span data-ttu-id="a25ce-104">Con connettore del Database Oracle hello è creare flussi di lavoro aziendali che utilizzano i dati nel database esistente.</span><span class="sxs-lookup"><span data-stu-id="a25ce-104">Using hello Oracle Database connector, you create organizational workflows that use data in your existing database.</span></span> <span data-ttu-id="a25ce-105">Questo connettore può connettersi tooan Database Oracle locale o una macchina virtuale Azure con Database Oracle installato.</span><span class="sxs-lookup"><span data-stu-id="a25ce-105">This connector can connect tooan on-premises Oracle Database, or an Azure virtual machine with Oracle Database installed.</span></span> <span data-ttu-id="a25ce-106">Con questo connettore è possibile:</span><span class="sxs-lookup"><span data-stu-id="a25ce-106">With this connector, you can:</span></span>

* <span data-ttu-id="a25ce-107">Compilare il flusso di lavoro aggiungendo un nuovo database di clienti tooa cliente o l'aggiornamento di un ordine in un database orders.</span><span class="sxs-lookup"><span data-stu-id="a25ce-107">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="a25ce-108">Utilizzare azioni tooget una riga di dati, inserire una nuova riga e di eliminare.</span><span class="sxs-lookup"><span data-stu-id="a25ce-108">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="a25ce-109">Quando ad esempio viene creato un record in Dynamics CRM Online (trigger), è possibile inserire una riga in Oracle Database (azione).</span><span class="sxs-lookup"><span data-stu-id="a25ce-109">For example, when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Oracle Database (an action).</span></span> 

<span data-ttu-id="a25ce-110">Questo argomento viene illustrato come toouse hello connettore del Database Oracle in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="a25ce-110">This topic shows you how toouse hello Oracle Database connector in a logic app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a25ce-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a25ce-111">Prerequisites</span></span>

* <span data-ttu-id="a25ce-112">Versioni di Oracle supportate:</span><span class="sxs-lookup"><span data-stu-id="a25ce-112">Supported Oracle versions:</span></span> 
    * <span data-ttu-id="a25ce-113">Oracle 9 e versioni successive</span><span class="sxs-lookup"><span data-stu-id="a25ce-113">Oracle 9 and later</span></span>
    * <span data-ttu-id="a25ce-114">Software client Oracle 8.1.7 e versioni successive</span><span class="sxs-lookup"><span data-stu-id="a25ce-114">Oracle client software 8.1.7 and later</span></span>

* <span data-ttu-id="a25ce-115">Installare il gateway dati locale di hello.</span><span class="sxs-lookup"><span data-stu-id="a25ce-115">Install hello on-premises data gateway.</span></span> <span data-ttu-id="a25ce-116">[Connessione dati tooon locale da App per la logica](../logic-apps/logic-apps-gateway-connection.md) elenchi hello passaggi.</span><span class="sxs-lookup"><span data-stu-id="a25ce-116">[Connect tooon-premises data from logic apps](../logic-apps/logic-apps-gateway-connection.md) lists hello steps.</span></span> <span data-ttu-id="a25ce-117">gateway Hello è obbligatorio tooconnect tooan Database Oracle locale o una macchina virtuale di Azure con i database Oracle installato.</span><span class="sxs-lookup"><span data-stu-id="a25ce-117">hello gateway is required tooconnect tooan on-premises Oracle Database, or an Azure VM with Oracle DB installed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="a25ce-118">gateway dati locale di Hello funge da ponte e fornisce un trasferimento tramite la protezione dei dati tra App per la logica e di dati in locale (dati che non sono nel cloud hello).</span><span class="sxs-lookup"><span data-stu-id="a25ce-118">hello on-premises data gateway acts as a bridge, and provides a secure data transfer between on-premises data (data that is not in hello cloud) and your logic apps.</span></span> <span data-ttu-id="a25ce-119">Hello stesso gateway può essere utilizzato con più servizi e più origini dati.</span><span class="sxs-lookup"><span data-stu-id="a25ce-119">hello same gateway can be used with multiple services, and multiple data sources.</span></span> <span data-ttu-id="a25ce-120">In tal caso, potrebbe essere gateway hello tooinstall una sola volta.</span><span class="sxs-lookup"><span data-stu-id="a25ce-120">So, you may only need tooinstall hello gateway once.</span></span>

* <span data-ttu-id="a25ce-121">Installare hello del Client Oracle nel computer di hello in cui è installato gateway dati locale di hello.</span><span class="sxs-lookup"><span data-stu-id="a25ce-121">Install hello Oracle Client on hello machine where you installed hello on-premises data gateway.</span></span> <span data-ttu-id="a25ce-122">Assicurarsi di tooinstall hello Provider di dati Oracle a 64 bit per .NET da Oracle:</span><span class="sxs-lookup"><span data-stu-id="a25ce-122">Be sure tooinstall hello 64-bit Oracle Data Provider for .NET from Oracle:</span></span>  

  [<span data-ttu-id="a25ce-123">ODAC 64 bit 12c versione 4 (12.1.0.2.4) per Windows x64</span><span class="sxs-lookup"><span data-stu-id="a25ce-123">64-bit ODAC 12c Release 4 (12.1.0.2.4) for Windows x64</span></span>](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > <span data-ttu-id="a25ce-124">Se non è installato il client di Oracle hello, si verifica un errore quando si tenta di toocreate o utilizzare connessione hello.</span><span class="sxs-lookup"><span data-stu-id="a25ce-124">If hello Oracle client is not installed, an error occurs when you try toocreate or use hello connection.</span></span> <span data-ttu-id="a25ce-125">Vedere gli errori comuni di hello in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="a25ce-125">See hello common errors in this topic.</span></span>


## <a name="add-hello-connector"></a><span data-ttu-id="a25ce-126">Aggiungere il connettore hello</span><span class="sxs-lookup"><span data-stu-id="a25ce-126">Add hello connector</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a25ce-127">Questo connettore non include trigger.</span><span class="sxs-lookup"><span data-stu-id="a25ce-127">This connector does not have any triggers.</span></span> <span data-ttu-id="a25ce-128">Ha solo azioni.</span><span class="sxs-lookup"><span data-stu-id="a25ce-128">It has only actions.</span></span> <span data-ttu-id="a25ce-129">Pertanto quando si crea la logica app, aggiungere un altro trigger toostart app logica, ad esempio **pianificazione - ricorrenza**, o **richiesta / risposta - risposta**.</span><span class="sxs-lookup"><span data-stu-id="a25ce-129">So when you create your logic app, add another trigger toostart your logic app, such as **Schedule - Recurrence**, or **Request / Response - Response**.</span></span> 

1. <span data-ttu-id="a25ce-130">In hello [portale di Azure](https://portal.azure.com), creare un'app logica vuoto.</span><span class="sxs-lookup"><span data-stu-id="a25ce-130">In hello [Azure portal](https://portal.azure.com), create a blank logic app.</span></span>

2. <span data-ttu-id="a25ce-131">All'avvio di hello dell'app logica, selezionare hello **richiesta / risposta - richiesta** trigger:</span><span class="sxs-lookup"><span data-stu-id="a25ce-131">At hello start of your logic app, select hello **Request / Response - Request** trigger:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. <span data-ttu-id="a25ce-132">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a25ce-132">Select **Save**.</span></span> <span data-ttu-id="a25ce-133">Quando si salva, viene generato automaticamente un URL di richiesta.</span><span class="sxs-lookup"><span data-stu-id="a25ce-133">When you save, a request URL is automatically generated.</span></span> 

4. <span data-ttu-id="a25ce-134">Selezionare **Nuovo passaggio** e quindi **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="a25ce-134">Select **New step**, and select **Add an action**.</span></span> <span data-ttu-id="a25ce-135">Digitare `oracle` toosee hello azioni disponibili:</span><span class="sxs-lookup"><span data-stu-id="a25ce-135">Type in `oracle` toosee hello available actions:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > <span data-ttu-id="a25ce-136">È anche toosee modo più rapido hello hello trigger e le azioni disponibili per i connettori.</span><span class="sxs-lookup"><span data-stu-id="a25ce-136">This is also hello quickest way toosee hello triggers and actions available for any connector.</span></span> <span data-ttu-id="a25ce-137">Digitare parte del nome del connettore hello, ad esempio `oracle`.</span><span class="sxs-lookup"><span data-stu-id="a25ce-137">Type in part of hello connector name, such as `oracle`.</span></span> <span data-ttu-id="a25ce-138">progettazione di Hello Elenca tutti i trigger e le azioni.</span><span class="sxs-lookup"><span data-stu-id="a25ce-138">hello designer lists any triggers and any actions.</span></span> 

5. <span data-ttu-id="a25ce-139">Selezionare una delle operazioni di hello, ad esempio **Database Oracle - Get riga**.</span><span class="sxs-lookup"><span data-stu-id="a25ce-139">Select one of hello actions, such as **Oracle Database - Get row**.</span></span> <span data-ttu-id="a25ce-140">Selezionare **Connect via on-premises data gateway** (Connetti tramite gateway dati locale).</span><span class="sxs-lookup"><span data-stu-id="a25ce-140">Select **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="a25ce-141">Immettere un nome del server Oracle hello, metodo di autenticazione, username, password e il gateway hello selezionare:</span><span class="sxs-lookup"><span data-stu-id="a25ce-141">Enter hello Oracle server name, authentication method, username, password, and select hello gateway:</span></span>

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. <span data-ttu-id="a25ce-142">Una volta connesso, selezionare una tabella dall'elenco hello e immettere hello riga ID tooyour tabella.</span><span class="sxs-lookup"><span data-stu-id="a25ce-142">Once connected, select a table from hello list, and enter hello row ID tooyour table.</span></span> <span data-ttu-id="a25ce-143">Tooknow hello identificatore toohello tabella è necessaria.</span><span class="sxs-lookup"><span data-stu-id="a25ce-143">You need tooknow hello identifier toohello table.</span></span> <span data-ttu-id="a25ce-144">Se non si conosce, contattare l'amministratore di database Oracle e ottenere l'output hello `select * from yourTableName`.</span><span class="sxs-lookup"><span data-stu-id="a25ce-144">If you don't know, contact your Oracle DB administrator, and get hello output from `select * from yourTableName`.</span></span> <span data-ttu-id="a25ce-145">In questo modo si hello informazioni personali necessarie tooproceed.</span><span class="sxs-lookup"><span data-stu-id="a25ce-145">This gives you hello identifiable information you need tooproceed.</span></span>

    <span data-ttu-id="a25ce-146">Nell'esempio seguente di hello, dati del processo viene restituiti da un database delle risorse umane:</span><span class="sxs-lookup"><span data-stu-id="a25ce-146">In hello following example, job data is being returned from a Human Resources database:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. <span data-ttu-id="a25ce-147">In questo passaggio successivo, è possibile utilizzare uno qualsiasi dei hello toobuild altri connettori il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a25ce-147">In this next step, you can use any of hello other connectors toobuild your workflow.</span></span> <span data-ttu-id="a25ce-148">Se si desidera tootest recupero dei dati da Oracle, invia un messaggio di posta elettronica con i dati di Oracle hello utilizzando uno dei hello inviare posta elettronica connettori, tali Office 365 o Gmail.</span><span class="sxs-lookup"><span data-stu-id="a25ce-148">If you want tootest getting data from Oracle, then send yourself an email with hello Oracle data using one of hello send email connectors, such Office 365 or Gmail.</span></span> <span data-ttu-id="a25ce-149">Usare i token dinamico hello da hello toobuild tabella Oracle di hello `Subject` e `Body` del messaggio di posta elettronica:</span><span class="sxs-lookup"><span data-stu-id="a25ce-149">Use hello dynamic tokens from hello Oracle table toobuild hello `Subject` and `Body` of your email:</span></span>

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. <span data-ttu-id="a25ce-150">**Salvare** l'app per la logica e quindi selezionare **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="a25ce-150">**Save** your logic app, and then select **Run**.</span></span> <span data-ttu-id="a25ce-151">Chiudere Progettazione hello ed esaminare hello cronologia di esecuzione per lo stato di hello.</span><span class="sxs-lookup"><span data-stu-id="a25ce-151">Close hello designer, and look at hello runs history for hello status.</span></span> <span data-ttu-id="a25ce-152">In caso contrario, selezionare una riga messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="a25ce-152">If it fails, select hello failed message row.</span></span> <span data-ttu-id="a25ce-153">verrà visualizzata la finestra di progettazione Hello e mostra che passaggio non è riuscita e mostra inoltre hello informazioni sull'errore.</span><span class="sxs-lookup"><span data-stu-id="a25ce-153">hello designer opens, and shows you which step failed, and also shows hello error information.</span></span> <span data-ttu-id="a25ce-154">Se ha esito positivo, verrà visualizzato un messaggio di posta elettronica con le informazioni di hello che è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="a25ce-154">If it succeeds, then you should receive an email with hello information you added.</span></span>


### <a name="workflow-ideas"></a><span data-ttu-id="a25ce-155">Idee per i flussi di lavoro</span><span class="sxs-lookup"><span data-stu-id="a25ce-155">Workflow ideas</span></span>

* <span data-ttu-id="a25ce-156">Si desidera toomonitor hello #oracle hashtag e inserire TWEET hello in un database in modo che possono essere eseguite query e utilizzate all'interno di altre applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a25ce-156">You want toomonitor hello #oracle hashtag, and put hello tweets in a database so they can be queried, and used within other applications.</span></span> <span data-ttu-id="a25ce-157">In un'app di logica, aggiungere hello `Twitter - When a new tweet is posted` attivare, quindi immettere hello **#oracle** hashtag.</span><span class="sxs-lookup"><span data-stu-id="a25ce-157">In a logic app, add hello `Twitter - When a new tweet is posted` trigger, and enter hello **#oracle** hashtag.</span></span> <span data-ttu-id="a25ce-158">Aggiungere quindi hello `Oracle Database - Insert row` azione, quindi selezionare la tabella:</span><span class="sxs-lookup"><span data-stu-id="a25ce-158">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* <span data-ttu-id="a25ce-159">I messaggi vengono inviati tooa della coda del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="a25ce-159">Messages are sent tooa Service Bus queue.</span></span> <span data-ttu-id="a25ce-160">Si desidera tooget questi messaggi e inserirli in un database.</span><span class="sxs-lookup"><span data-stu-id="a25ce-160">You want tooget these messages, and put them in a database.</span></span> <span data-ttu-id="a25ce-161">In un'app di logica, aggiungere hello `Service Bus - when a message is received in a queue` trigger e coda hello selezionare.</span><span class="sxs-lookup"><span data-stu-id="a25ce-161">In a logic app, add hello `Service Bus - when a message is received in a queue` trigger, and select hello queue.</span></span> <span data-ttu-id="a25ce-162">Aggiungere quindi hello `Oracle Database - Insert row` azione, quindi selezionare la tabella:</span><span class="sxs-lookup"><span data-stu-id="a25ce-162">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a><span data-ttu-id="a25ce-163">Errori comuni</span><span class="sxs-lookup"><span data-stu-id="a25ce-163">Common errors</span></span>

#### <a name="error-cannot-reach-hello-gateway"></a><span data-ttu-id="a25ce-164">**Errore**: Impossibile raggiungere hello Gateway</span><span class="sxs-lookup"><span data-stu-id="a25ce-164">**Error**: Cannot reach hello Gateway</span></span>

<span data-ttu-id="a25ce-165">**Causa**: gateway dati locale di hello non è in grado di tooconnect toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="a25ce-165">**Cause**: hello on-premises data gateway is not able tooconnect toohello cloud.</span></span> 

<span data-ttu-id="a25ce-166">**Attenuazione**: verificare che il gateway è in esecuzione nel computer locale di hello in cui è stato installato e che può connettersi toohello internet.</span><span class="sxs-lookup"><span data-stu-id="a25ce-166">**Mitigation**: Make sure your gateway is running on hello on-premises machine where you installed it, and that it can connect toohello internet.</span></span>  <span data-ttu-id="a25ce-167">Si consiglia di non installare il gateway hello in un computer che può essere disattivata o sospensione.</span><span class="sxs-lookup"><span data-stu-id="a25ce-167">We recommend not installing hello gateway on a computer that may be turned off or sleep.</span></span> <span data-ttu-id="a25ce-168">È anche possibile riavviare il servizio hello locale data gateway (PBIEgwService).</span><span class="sxs-lookup"><span data-stu-id="a25ce-168">You can also restart hello on-premises data gateway service (PBIEgwService).</span></span>

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a><span data-ttu-id="a25ce-169">**Errore**: hello provider in uso è deprecato: ' OracleClient richiede software client Oracle versione 8.1.7 o versione successiva.'.</span><span class="sxs-lookup"><span data-stu-id="a25ce-169">**Error**: hello provider being used is deprecated: 'System.Data.OracleClient requires Oracle client software version 8.1.7 or greater.'.</span></span> <span data-ttu-id="a25ce-170">Visitare [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall provider ufficiale di hello.</span><span class="sxs-lookup"><span data-stu-id="a25ce-170">Please visit [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello official provider.</span></span>

<span data-ttu-id="a25ce-171">**Causa**: hello Oracle client SDK non è installato nel computer di hello dove hello locali gateway dati è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a25ce-171">**Cause**: hello Oracle client SDK is not installed on hello machine where hello on-premises data gateway is running.</span></span>  

<span data-ttu-id="a25ce-172">**Risoluzione**: scaricare e installare il client Oracle hello SDK in hello stesso computer del gateway dati locale di hello.</span><span class="sxs-lookup"><span data-stu-id="a25ce-172">**Resolution**: Download and install hello Oracle client SDK on hello same computer as hello on-premises data gateway.</span></span>

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a><span data-ttu-id="a25ce-173">**Errore**: La tabella '[NomeTabella]' non definisce alcuna colonna chiave</span><span class="sxs-lookup"><span data-stu-id="a25ce-173">**Error**: Table '[Tablename]' does not define any key columns</span></span>

<span data-ttu-id="a25ce-174">**Causa**: tabella hello non dispone di qualsiasi chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="a25ce-174">**Cause**: hello table does not have any primary key.</span></span>  

<span data-ttu-id="a25ce-175">**Risoluzione**: connettore del Database Oracle hello è necessario utilizzare una tabella con una colonna chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="a25ce-175">**Resolution**: hello Oracle Database connector requires that a table with a primary key column be used.</span></span>

#### <a name="currently-not-supported"></a><span data-ttu-id="a25ce-176">Attualmente non supportati</span><span class="sxs-lookup"><span data-stu-id="a25ce-176">Currently not supported</span></span>

* <span data-ttu-id="a25ce-177">Viste e stored procedure</span><span class="sxs-lookup"><span data-stu-id="a25ce-177">Views and stored procedures</span></span> 
* <span data-ttu-id="a25ce-178">Tabelle con chiavi composte</span><span class="sxs-lookup"><span data-stu-id="a25ce-178">Any table with composite keys</span></span>
* <span data-ttu-id="a25ce-179">Tipi di oggetti annidati nelle tabelle</span><span class="sxs-lookup"><span data-stu-id="a25ce-179">Nested object types in tables</span></span>
 
## <a name="connector-specific-details"></a><span data-ttu-id="a25ce-180">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="a25ce-180">Connector-specific details</span></span>

<span data-ttu-id="a25ce-181">Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/oracle/).</span><span class="sxs-lookup"><span data-stu-id="a25ce-181">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/oracle/).</span></span> 

## <a name="get-some-help"></a><span data-ttu-id="a25ce-182">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="a25ce-182">Get some help</span></span>

<span data-ttu-id="a25ce-183">Hello [forum di Azure logica app](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) è inserire domande tooask, rispondere alle domande e osservare gli altri utenti di App per la logica sono un'eccellente.</span><span class="sxs-lookup"><span data-stu-id="a25ce-183">hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is a great place tooask questions, answer questions, and see what other Logic Apps users are doing.</span></span> 

<span data-ttu-id="a25ce-184">È possibile migliorare App per la logica e i connettori votando e inviando le idee nella pagina [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="a25ce-184">You can help improve Logic Apps and connectors by voting and submitting your ideas at [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span></span> 


## <a name="next-steps"></a><span data-ttu-id="a25ce-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a25ce-185">Next steps</span></span>
<span data-ttu-id="a25ce-186">[Creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md)ed esplorare i connettori disponibili hello in App per la logica nel nostro [elenco API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="a25ce-186">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md), and explore hello available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
