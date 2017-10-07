---
title: i certificati di Azure Cosmos DB emulatore hello aaaExport | Documenti Microsoft
description: "Quando si sviluppa in linguaggi e Runtime che non utilizzano l'archivio certificati di Windows hello sarà anche necessario tooexport e gestire i certificati SSL hello. Questo post contiene istruzioni dettagliate."
services: cosmos-db
documentationcenter: 
keywords: Emulatore di Azure Cosmos DB
author: voellm
manager: jhubbard
editor: 
ms.assetid: ef43deda-c2e9-4193-99e2-7f6a88a0319f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: tvoellm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: db56cda856fccf93d71ae5b21c4090ccb9aa40a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a><span data-ttu-id="3a41a-105">Esportare i certificati di Azure Cosmos DB emulatore hello per l'utilizzo con Java, Python e Node.js</span><span class="sxs-lookup"><span data-stu-id="3a41a-105">Export hello Azure Cosmos DB Emulator certificates for use with Java, Python, and Node.js</span></span>

[<span data-ttu-id="3a41a-106">**Scaricare hello emulatore**</span><span class="sxs-lookup"><span data-stu-id="3a41a-106">**Download hello Emulator**</span></span>](https://aka.ms/cosmosdb-emulator)

<span data-ttu-id="3a41a-107">Hello Azure Cosmos DB emulatore offre un ambiente locale che emula hello Azure Cosmos DB servizio a scopo di sviluppo incluso l'utilizzo di connessioni SSL.</span><span class="sxs-lookup"><span data-stu-id="3a41a-107">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes including its use of SSL connections.</span></span> <span data-ttu-id="3a41a-108">Questo post di seguito viene illustrato l'utilizzo tooexport hello SSL dei certificati per l'utilizzo in linguaggi e Runtime che non si integrano con hello archivio certificati di Windows, ad esempio Java che utilizza un proprio [archivio certificati](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) e Python che utilizza [socket wrapper](https://docs.python.org/2/library/ssl.html) e Node.js che usa [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="3a41a-108">This post demonstrates how tooexport hello SSL certificates for use in languages and runtimes that do not integrate with hello Windows Certificate Store such as Java which uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) and Python which uses [socket wrappers](https://docs.python.org/2/library/ssl.html) and Node.js which uses [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span> <span data-ttu-id="3a41a-109">È possibile leggere altre informazioni sull'emulatore hello in [hello utilizzare Azure Cosmos DB emulatore per lo sviluppo e test](./local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="3a41a-109">You can read more about hello emulator in [Use hello Azure Cosmos DB Emulator for development and testing](./local-emulator.md).</span></span>

<span data-ttu-id="3a41a-110">Questa esercitazione sono trattati hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="3a41a-110">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3a41a-111">Rotazione dei certificati</span><span class="sxs-lookup"><span data-stu-id="3a41a-111">Rotating certificates</span></span>
> * <span data-ttu-id="3a41a-112">Esportazione di un certificato SSL</span><span class="sxs-lookup"><span data-stu-id="3a41a-112">Exporting SSL certificate</span></span>
> * <span data-ttu-id="3a41a-113">Apprendere come toouse hello certificato in Java, Python e Node.js</span><span class="sxs-lookup"><span data-stu-id="3a41a-113">Learning how toouse hello certificate in Java, Python, and Node.js</span></span>

## <a name="certification-rotation"></a><span data-ttu-id="3a41a-114">Rotazione della certificazione</span><span class="sxs-lookup"><span data-stu-id="3a41a-114">Certification rotation</span></span>

<span data-ttu-id="3a41a-115">I certificati nel hello che emulatore locale di Azure Cosmos DB vengono generati hello prima esecuzione dell'emulatore hello.</span><span class="sxs-lookup"><span data-stu-id="3a41a-115">Certificates in hello Azure Cosmos DB Local Emulator are generated hello first time hello emulator is run.</span></span> <span data-ttu-id="3a41a-116">Esistono due certificati,</span><span class="sxs-lookup"><span data-stu-id="3a41a-116">There are two certificates.</span></span> <span data-ttu-id="3a41a-117">Quello utilizzato per la connessione emulatore locale toohello e uno per la gestione dei segreti nell'emulatore hello.</span><span class="sxs-lookup"><span data-stu-id="3a41a-117">One used for connecting toohello local emulator and one for managing secrets within hello emulator.</span></span> <span data-ttu-id="3a41a-118">certificato di Hello da tooexport è certificato di connessione hello con il nome descrittivo di hello "DocumentDBEmulatorCertificate".</span><span class="sxs-lookup"><span data-stu-id="3a41a-118">hello certificate you want tooexport is hello connection certificate with hello friendly name "DocumentDBEmulatorCertificate".</span></span>

<span data-ttu-id="3a41a-119">Entrambi i certificati possono essere rigenerati facendo **Reimposta dati** come illustrato di seguito da Azure Cosmos DB emulatore in esecuzione nella barra delle applicazioni di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="3a41a-119">Both certificates can be regenerated by clicking **Reset Data** as shown below from Azure Cosmos DB Emulator running in hello Windows Tray.</span></span> <span data-ttu-id="3a41a-120">Se è rigenerare i certificati di hello e installati nell'archivio certificati di Java hello o li utilizzati altrove, è necessario tooupdate correlate, in caso contrario l'applicazione non è più connetterà emulatore locale toohello.</span><span class="sxs-lookup"><span data-stu-id="3a41a-120">If you regenerate hello certificates and have installed them into hello Java certificate store or used them elsewhere you will need tooupdate them, otherwise your application will no longer connect toohello local emulator.</span></span>

![Reimpostazione dei dati nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a><span data-ttu-id="3a41a-122">Come tooexport hello certificato SSL di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3a41a-122">How tooexport hello Azure Cosmos DB SSL certificate</span></span>

1. <span data-ttu-id="3a41a-123">Avviare il gestore di certificati di Windows hello eseguendo certlm.msc e passare toohello personale -> cartella certificati e certificati hello aperto con il nome descrittivo hello **DocumentDbEmulatorCertificate**.</span><span class="sxs-lookup"><span data-stu-id="3a41a-123">Start hello Windows Certificate manager by running certlm.msc and navigate toohello Personal->Certificates folder and open hello certificate with hello friendly name **DocumentDbEmulatorCertificate**.</span></span>

    ![Passaggio 1 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. <span data-ttu-id="3a41a-125">Fare clic su **Details** (Dettagli) quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3a41a-125">Click on **Details** then **OK**.</span></span>

    ![Passaggio 2 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. <span data-ttu-id="3a41a-127">Fare clic su **copiare tooFile...** .</span><span class="sxs-lookup"><span data-stu-id="3a41a-127">Click **Copy tooFile...**.</span></span>

    ![Passaggio 3 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. <span data-ttu-id="3a41a-129">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3a41a-129">Click **Next**.</span></span>

    ![Passaggio 4 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. <span data-ttu-id="3a41a-131">Fare clic su **No, do not export private key** (No, non esportare la chiave privata) e quindi su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="3a41a-131">Click **No, do not export private key**, then click **Next**.</span></span>

    ![Passaggio 5 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. <span data-ttu-id="3a41a-133">Fare clic su **Base-64 encoded X.509 (.CER)** (Codificato in base 64 X.509 (.CER)) e quindi su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="3a41a-133">Click on **Base-64 encoded X.509 (.CER)** and then **Next**.</span></span>

    ![Passaggio 6 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. <span data-ttu-id="3a41a-135">Assegnare un nome di certificato hello.</span><span class="sxs-lookup"><span data-stu-id="3a41a-135">Give hello certificate a name.</span></span> <span data-ttu-id="3a41a-136">In questo caso, **documentdbemulatorcert**, quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="3a41a-136">In this case **documentdbemulatorcert** and then click **Next**.</span></span>

    ![Passaggio 7 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. <span data-ttu-id="3a41a-138">Fare clic su **Finish** (Fine).</span><span class="sxs-lookup"><span data-stu-id="3a41a-138">Click **Finish**.</span></span>

    ![Passaggio 8 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a><span data-ttu-id="3a41a-140">Come toouse hello certificato in Java</span><span class="sxs-lookup"><span data-stu-id="3a41a-140">How toouse hello certificate in Java</span></span>

<span data-ttu-id="3a41a-141">Durante l'esecuzione di applicazioni Java o MongoDB che utilizzano client Java hello è più facile certificato di hello tooinstall nell'archivio certificati predefinito di hello Java di passaggio hello "-Djavax.net.ssl.trustStore=<keystore> - Djavax.net.ssl.trustStorePassword= "<password>" flag.</span><span class="sxs-lookup"><span data-stu-id="3a41a-141">When running Java applications or MongoDB applications that use hello Java client it is easier tooinstall hello certificate into hello Java default certificate store than passing hello "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>" flags.</span></span> <span data-ttu-id="3a41a-142">Ad esempio hello incluso [applicazione Java Demo](https://localhost:8081/_explorer/index.html) dipende dall'archivio certificati predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="3a41a-142">For example hello included [Java Demo application](https://localhost:8081/_explorer/index.html) depends on hello default certificate store.</span></span>

<span data-ttu-id="3a41a-143">Seguire le istruzioni hello hello [aggiunta di un certificato toohello archivio certificati Autorità di certificazione Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello x. 509 del certificato nell'archivio certificati di hello predefinito Java.</span><span class="sxs-lookup"><span data-stu-id="3a41a-143">Follow hello instructions in hello [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello X.509 certificate into hello default Java certificate store.</span></span> <span data-ttu-id="3a41a-144">Tenere in considerazione che è possibile lavorare in directory hello % JAVA_HOME % quando si esegue keytool.</span><span class="sxs-lookup"><span data-stu-id="3a41a-144">Keep in mind you will be working in hello %JAVA_HOME% directory when running keytool.</span></span>

<span data-ttu-id="3a41a-145">Una volta hello "CosmosDBEmulatorCertificate" SSL certificato sia installato l'applicazione deve essere in grado di tooconnect e utilizzare hello locale Azure Cosmos DB emulatore.</span><span class="sxs-lookup"><span data-stu-id="3a41a-145">Once hello "CosmosDBEmulatorCertificate" SSL certificate is installed your application should be able tooconnect and use hello local Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="3a41a-146">Se si continuano toohave problemi è hello toofollow [debug connessioni SSL/TLS](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) articolo.</span><span class="sxs-lookup"><span data-stu-id="3a41a-146">If you continue toohave trouble you may want toofollow hello [Debugging SSL/TLS Connections](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) article.</span></span> <span data-ttu-id="3a41a-147">È molto probabile hello certificato non è installato nell'archivio %JAVA_HOME%/jre/lib/security/cacerts hello.</span><span class="sxs-lookup"><span data-stu-id="3a41a-147">It is very likely hello certificate is not installed into hello %JAVA_HOME%/jre/lib/security/cacerts store.</span></span> <span data-ttu-id="3a41a-148">Per esempio, se si dispone di più versioni installate di Java l'applicazione stia utilizzando un archivio diverso cacerts di hello uno che è stato aggiornato.</span><span class="sxs-lookup"><span data-stu-id="3a41a-148">For example if you have multiple installed versions of Java your application may be using a different cacerts store than hello one you updated.</span></span>

## <a name="how-toouse-hello-certificate-in-python"></a><span data-ttu-id="3a41a-149">Come toouse hello certificato di Python</span><span class="sxs-lookup"><span data-stu-id="3a41a-149">How toouse hello certificate in Python</span></span>

<span data-ttu-id="3a41a-150">Da hello predefinito [SDK(version 2.0.0 or higher) Python](documentdb-sdk-python.md) per hello API DocumentDB non tenta di utilizzare certificato SSL di hello quando ci si connette emulatore locale toohello.</span><span class="sxs-lookup"><span data-stu-id="3a41a-150">By default hello [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) for hello DocumentDB API will not try and use hello SSL certificate when connecting toohello local emulator.</span></span> <span data-ttu-id="3a41a-151">Se tuttavia si vuole toouse SSL convalida è possibile seguire negli esempi di hello hello [Python socket wrapper](https://docs.python.org/2/library/ssl.html) documentazione.</span><span class="sxs-lookup"><span data-stu-id="3a41a-151">If however you want toouse SSL validation you can follow hello examples in hello [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentation.</span></span>

## <a name="how-toouse-hello-certificate-in-nodejs"></a><span data-ttu-id="3a41a-152">Come toouse hello certificato in Node.js</span><span class="sxs-lookup"><span data-stu-id="3a41a-152">How toouse hello certificate in Node.js</span></span>

<span data-ttu-id="3a41a-153">Da hello predefinito [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) per hello API DocumentDB non tenta di utilizzare certificato SSL di hello quando ci si connette emulatore locale toohello.</span><span class="sxs-lookup"><span data-stu-id="3a41a-153">By default hello [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) for hello DocumentDB API will not try and use hello SSL certificate when connecting toohello local emulator.</span></span> <span data-ttu-id="3a41a-154">Se tuttavia si vuole toouse SSL convalida è possibile seguire negli esempi di hello hello [documentazione su Node.js](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="3a41a-154">If however you want toouse SSL validation you can follow hello examples in hello [Node.js documentation](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a41a-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3a41a-155">Next steps</span></span>

<span data-ttu-id="3a41a-156">In questa esercitazione, effettuata seguente hello:</span><span class="sxs-lookup"><span data-stu-id="3a41a-156">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3a41a-157">Rotazione dei certificati</span><span class="sxs-lookup"><span data-stu-id="3a41a-157">Rotated certificates</span></span>
> * <span data-ttu-id="3a41a-158">Certificato SSL hello esportata</span><span class="sxs-lookup"><span data-stu-id="3a41a-158">Exported hello SSL certificate</span></span>
> * <span data-ttu-id="3a41a-159">Appreso come toouse hello certificato in Java, Python e Node.js</span><span class="sxs-lookup"><span data-stu-id="3a41a-159">Learned how toouse hello certificate in Java, Python and Node.js</span></span>

<span data-ttu-id="3a41a-160">È ora possibile procedere toohello concetti per ulteriori informazioni su DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="3a41a-160">You can now proceed toohello Concepts section for more information about Cosmos DB.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3a41a-161">Distribuzione globale</span><span class="sxs-lookup"><span data-stu-id="3a41a-161">Global distribution</span></span>](distribute-data-globally.md) 
