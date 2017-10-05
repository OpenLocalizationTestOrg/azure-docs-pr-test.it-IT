---
title: Esportare i certificati dell'emulatore di Azure Cosmos DB | Microsoft Docs
description: "Quando si effettua lo sviluppo in linguaggi e runtime che non usano l'archivio certificati Windows, sarà necessario esportare e gestire i certificati SSL. Questo post contiene istruzioni dettagliate."
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
ms.openlocfilehash: 4add5028d50972316902cecd8c399781c012cb77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="export-the-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a><span data-ttu-id="fe837-105">Esportare i certificati dell'emulatore di Azure Cosmos DB per l'uso con Java, Python e Node.js</span><span class="sxs-lookup"><span data-stu-id="fe837-105">Export the Azure Cosmos DB Emulator certificates for use with Java, Python, and Node.js</span></span>

[<span data-ttu-id="fe837-106">**Scaricare l'emulatore**</span><span class="sxs-lookup"><span data-stu-id="fe837-106">**Download the Emulator**</span></span>](https://aka.ms/cosmosdb-emulator)

<span data-ttu-id="fe837-107">L'emulatore di Azure Cosmos DB fornisce un ambiente locale che emula il servizio Azure Cosmos DB per obiettivi di sviluppo, incluso l'uso di connessioni SSL.</span><span class="sxs-lookup"><span data-stu-id="fe837-107">The Azure Cosmos DB Emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes including its use of SSL connections.</span></span> <span data-ttu-id="fe837-108">Questo post illustra come esportare i certificati SSL da usare in linguaggi e runtime non integrati con l'archivio certificati Windows, ad esempio Java che usa il proprio [archivio certificati](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html), Python che usa [wrapper per socket](https://docs.python.org/2/library/ssl.html) e Node.js che usa [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="fe837-108">This post demonstrates how to export the SSL certificates for use in languages and runtimes that do not integrate with the Windows Certificate Store such as Java which uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) and Python which uses [socket wrappers](https://docs.python.org/2/library/ssl.html) and Node.js which uses [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span> <span data-ttu-id="fe837-109">Per altre informazioni sull'emulatore, vedere [Usare l'emulatore di Azure Cosmos DB per sviluppo e test](./local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="fe837-109">You can read more about the emulator in [Use the Azure Cosmos DB Emulator for development and testing](./local-emulator.md).</span></span>

<span data-ttu-id="fe837-110">Questa esercitazione illustra le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="fe837-110">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fe837-111">Rotazione dei certificati</span><span class="sxs-lookup"><span data-stu-id="fe837-111">Rotating certificates</span></span>
> * <span data-ttu-id="fe837-112">Esportazione di un certificato SSL</span><span class="sxs-lookup"><span data-stu-id="fe837-112">Exporting SSL certificate</span></span>
> * <span data-ttu-id="fe837-113">Come usare il certificato in Java, Python e Node.js</span><span class="sxs-lookup"><span data-stu-id="fe837-113">Learning how to use the certificate in Java, Python, and Node.js</span></span>

## <a name="certification-rotation"></a><span data-ttu-id="fe837-114">Rotazione della certificazione</span><span class="sxs-lookup"><span data-stu-id="fe837-114">Certification rotation</span></span>

<span data-ttu-id="fe837-115">I certificati nell'emulatore locale di Azure Cosmos DB vengono generati la prima volta che l'emulatore viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="fe837-115">Certificates in the Azure Cosmos DB Local Emulator are generated the first time the emulator is run.</span></span> <span data-ttu-id="fe837-116">Esistono due certificati,</span><span class="sxs-lookup"><span data-stu-id="fe837-116">There are two certificates.</span></span> <span data-ttu-id="fe837-117">uno usato per la connessione all'emulatore locale e l'altro per la gestione dei segreti nell'emulatore.</span><span class="sxs-lookup"><span data-stu-id="fe837-117">One used for connecting to the local emulator and one for managing secrets within the emulator.</span></span> <span data-ttu-id="fe837-118">Il certificato che si vuole esportare è il certificato per la connessione con il nome descrittivo "DocumentDBEmulatorCertificate".</span><span class="sxs-lookup"><span data-stu-id="fe837-118">The certificate you want to export is the connection certificate with the friendly name "DocumentDBEmulatorCertificate".</span></span>

<span data-ttu-id="fe837-119">Entrambi i certificati possono essere rigenerati facendo clic su **Reset Data** (Reimposta dati), come illustrato di seguito, dall'emulatore di Azure Cosmos DB in esecuzione nell'area di notifica di Windows.</span><span class="sxs-lookup"><span data-stu-id="fe837-119">Both certificates can be regenerated by clicking **Reset Data** as shown below from Azure Cosmos DB Emulator running in the Windows Tray.</span></span> <span data-ttu-id="fe837-120">Se si rigenerano i certificati e questi sono stati installati nell'archivio certificati di Java o usati altrove, sarà necessario aggiornarli. In caso contrario l'applicazione non si connetterà più all'emulatore locale.</span><span class="sxs-lookup"><span data-stu-id="fe837-120">If you regenerate the certificates and have installed them into the Java certificate store or used them elsewhere you will need to update them, otherwise your application will no longer connect to the local emulator.</span></span>

![Reimpostazione dei dati nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-to-export-the-azure-cosmos-db-ssl-certificate"></a><span data-ttu-id="fe837-122">Come esportare il certificato SSL dell'emulatore di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fe837-122">How to export the Azure Cosmos DB SSL certificate</span></span>

1. <span data-ttu-id="fe837-123">Avviare Gestione certificati di Windows eseguendo certlm.msc, passare alla cartella Personale->Certificati e aprire il certificato con il nome descrittivo **DocumentDbEmulatorCertificate**.</span><span class="sxs-lookup"><span data-stu-id="fe837-123">Start the Windows Certificate manager by running certlm.msc and navigate to the Personal->Certificates folder and open the certificate with the friendly name **DocumentDbEmulatorCertificate**.</span></span>

    ![Passaggio 1 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. <span data-ttu-id="fe837-125">Fare clic su **Details** (Dettagli) quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="fe837-125">Click on **Details** then **OK**.</span></span>

    ![Passaggio 2 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. <span data-ttu-id="fe837-127">Fare clic su **Copy to File...** (Copia in file).</span><span class="sxs-lookup"><span data-stu-id="fe837-127">Click **Copy to File...**.</span></span>

    ![Passaggio 3 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. <span data-ttu-id="fe837-129">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="fe837-129">Click **Next**.</span></span>

    ![Passaggio 4 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. <span data-ttu-id="fe837-131">Fare clic su **No, do not export private key** (No, non esportare la chiave privata) e quindi su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="fe837-131">Click **No, do not export private key**, then click **Next**.</span></span>

    ![Passaggio 5 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. <span data-ttu-id="fe837-133">Fare clic su **Base-64 encoded X.509 (.CER)** (Codificato in base 64 X.509 (.CER)) e quindi su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="fe837-133">Click on **Base-64 encoded X.509 (.CER)** and then **Next**.</span></span>

    ![Passaggio 6 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. <span data-ttu-id="fe837-135">Assegnare un nome al certificato.</span><span class="sxs-lookup"><span data-stu-id="fe837-135">Give the certificate a name.</span></span> <span data-ttu-id="fe837-136">In questo caso, **documentdbemulatorcert**, quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="fe837-136">In this case **documentdbemulatorcert** and then click **Next**.</span></span>

    ![Passaggio 7 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. <span data-ttu-id="fe837-138">Fare clic su **Finish** (Fine).</span><span class="sxs-lookup"><span data-stu-id="fe837-138">Click **Finish**.</span></span>

    ![Passaggio 8 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-to-use-the-certificate-in-java"></a><span data-ttu-id="fe837-140">Come usare il certificato in Java</span><span class="sxs-lookup"><span data-stu-id="fe837-140">How to use the certificate in Java</span></span>

<span data-ttu-id="fe837-141">Quando si eseguono applicazioni Java o applicazioni MongoDB che usano il client Java, è più facile installare il certificato nell'archivio certificati predefinito di Java che passare i flag "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>".</span><span class="sxs-lookup"><span data-stu-id="fe837-141">When running Java applications or MongoDB applications that use the Java client it is easier to install the certificate into the Java default certificate store than passing the "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>" flags.</span></span> <span data-ttu-id="fe837-142">Ad esempio, l'[applicazione demo Java](https://localhost:8081/_explorer/index.html) inclusa dipende dall'archivio certificati predefinito.</span><span class="sxs-lookup"><span data-stu-id="fe837-142">For example the included [Java Demo application](https://localhost:8081/_explorer/index.html) depends on the default certificate store.</span></span>

<span data-ttu-id="fe837-143">Seguire le istruzioni indicate in [Aggiunta di un certificato all'archivio certificati CA Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store) per importare il certificato X.509 nell'archivio certificati Java predefinito.</span><span class="sxs-lookup"><span data-stu-id="fe837-143">Follow the instructions in the [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store) to import the X.509 certificate into the default Java certificate store.</span></span> <span data-ttu-id="fe837-144">Tenere presente che si usa la directory %JAVA_HOME% quando si esegue keytool.</span><span class="sxs-lookup"><span data-stu-id="fe837-144">Keep in mind you will be working in the %JAVA_HOME% directory when running keytool.</span></span>

<span data-ttu-id="fe837-145">Dopo l'installazione del certificato SSL "CosmosDBEmulatorCertificate", l'applicazione potrà connettersi e usare l'emulatore di Azure Cosmos DB locale.</span><span class="sxs-lookup"><span data-stu-id="fe837-145">Once the "CosmosDBEmulatorCertificate" SSL certificate is installed your application should be able to connect and use the local Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="fe837-146">Se i problemi persistono, vedere l'articolo [Debug delle connessioni SSL/TLS](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html).</span><span class="sxs-lookup"><span data-stu-id="fe837-146">If you continue to have trouble you may want to follow the [Debugging SSL/TLS Connections](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) article.</span></span> <span data-ttu-id="fe837-147">Molto probabilmente il certificato non è installato nell'archivio %JAVA_HOME%/jre/lib/security/cacerts.</span><span class="sxs-lookup"><span data-stu-id="fe837-147">It is very likely the certificate is not installed into the %JAVA_HOME%/jre/lib/security/cacerts store.</span></span> <span data-ttu-id="fe837-148">Se, ad esempio, sono installate più versioni di Java, è possibile che l'applicazione stia usando un archivio cacerts diverso da quello aggiornato.</span><span class="sxs-lookup"><span data-stu-id="fe837-148">For example if you have multiple installed versions of Java your application may be using a different cacerts store than the one you updated.</span></span>

## <a name="how-to-use-the-certificate-in-python"></a><span data-ttu-id="fe837-149">Come usare il certificato in Python</span><span class="sxs-lookup"><span data-stu-id="fe837-149">How to use the certificate in Python</span></span>

<span data-ttu-id="fe837-150">Per impostazione predefinita, [Python SDK (2.0.0 o versione successiva)](documentdb-sdk-python.md) per l'API di DocumentDB non prova a usare il certificato SSL quando si connette all'emulatore locale.</span><span class="sxs-lookup"><span data-stu-id="fe837-150">By default the [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) for the DocumentDB API will not try and use the SSL certificate when connecting to the local emulator.</span></span> <span data-ttu-id="fe837-151">Se tuttavia si vuole usare la convalida SSL, è possibile seguire gli esempi della documentazione sui [wrapper per socket di Python](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="fe837-151">If however you want to use SSL validation you can follow the examples in the [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentation.</span></span>

## <a name="how-to-use-the-certificate-in-nodejs"></a><span data-ttu-id="fe837-152">Come usare il certificato in Node.js</span><span class="sxs-lookup"><span data-stu-id="fe837-152">How to use the certificate in Node.js</span></span>

<span data-ttu-id="fe837-153">Per impostazione predefinita, [Node.js SDK (1.10.1 o versione successiva)](documentdb-sdk-node.md) per l'API di DocumentDB non prova a usare il certificato SSL quando si connette all'emulatore locale.</span><span class="sxs-lookup"><span data-stu-id="fe837-153">By default the [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) for the DocumentDB API will not try and use the SSL certificate when connecting to the local emulator.</span></span> <span data-ttu-id="fe837-154">Se tuttavia si vuole usare la convalida SSL, è possibile seguire gli esempi nella [documentazione di Node.js](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="fe837-154">If however you want to use SSL validation you can follow the examples in the [Node.js documentation](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe837-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fe837-155">Next steps</span></span>

<span data-ttu-id="fe837-156">In questa esercitazione sono state eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fe837-156">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fe837-157">Rotazione dei certificati</span><span class="sxs-lookup"><span data-stu-id="fe837-157">Rotated certificates</span></span>
> * <span data-ttu-id="fe837-158">Esportazione del certificato SSL</span><span class="sxs-lookup"><span data-stu-id="fe837-158">Exported the SSL certificate</span></span>
> * <span data-ttu-id="fe837-159">Uso del certificato in Java, Python e Node.js</span><span class="sxs-lookup"><span data-stu-id="fe837-159">Learned how to use the certificate in Java, Python and Node.js</span></span>

<span data-ttu-id="fe837-160">È ora possibile passare alla sezione Concetti per altre informazioni su Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fe837-160">You can now proceed to the Concepts section for more information about Cosmos DB.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fe837-161">Distribuzione globale</span><span class="sxs-lookup"><span data-stu-id="fe837-161">Global distribution</span></span>](distribute-data-globally.md) 
