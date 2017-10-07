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
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a>Esportare i certificati di Azure Cosmos DB emulatore hello per l'utilizzo con Java, Python e Node.js

[**Scaricare hello emulatore**](https://aka.ms/cosmosdb-emulator)

Hello Azure Cosmos DB emulatore offre un ambiente locale che emula hello Azure Cosmos DB servizio a scopo di sviluppo incluso l'utilizzo di connessioni SSL. Questo post di seguito viene illustrato l'utilizzo tooexport hello SSL dei certificati per l'utilizzo in linguaggi e Runtime che non si integrano con hello archivio certificati di Windows, ad esempio Java che utilizza un proprio [archivio certificati](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) e Python che utilizza [socket wrapper](https://docs.python.org/2/library/ssl.html) e Node.js che usa [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback). È possibile leggere altre informazioni sull'emulatore hello in [hello utilizzare Azure Cosmos DB emulatore per lo sviluppo e test](./local-emulator.md).

Questa esercitazione sono trattati hello seguenti attività:

> [!div class="checklist"]
> * Rotazione dei certificati
> * Esportazione di un certificato SSL
> * Apprendere come toouse hello certificato in Java, Python e Node.js

## <a name="certification-rotation"></a>Rotazione della certificazione

I certificati nel hello che emulatore locale di Azure Cosmos DB vengono generati hello prima esecuzione dell'emulatore hello. Esistono due certificati, Quello utilizzato per la connessione emulatore locale toohello e uno per la gestione dei segreti nell'emulatore hello. certificato di Hello da tooexport è certificato di connessione hello con il nome descrittivo di hello "DocumentDBEmulatorCertificate".

Entrambi i certificati possono essere rigenerati facendo **Reimposta dati** come illustrato di seguito da Azure Cosmos DB emulatore in esecuzione nella barra delle applicazioni di Windows hello. Se è rigenerare i certificati di hello e installati nell'archivio certificati di Java hello o li utilizzati altrove, è necessario tooupdate correlate, in caso contrario l'applicazione non è più connetterà emulatore locale toohello.

![Reimpostazione dei dati nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a>Come tooexport hello certificato SSL di Azure Cosmos DB

1. Avviare il gestore di certificati di Windows hello eseguendo certlm.msc e passare toohello personale -> cartella certificati e certificati hello aperto con il nome descrittivo hello **DocumentDbEmulatorCertificate**.

    ![Passaggio 1 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. Fare clic su **Details** (Dettagli) quindi su **OK**.

    ![Passaggio 2 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. Fare clic su **copiare tooFile...** .

    ![Passaggio 3 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. Fare clic su **Avanti**.

    ![Passaggio 4 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. Fare clic su **No, do not export private key** (No, non esportare la chiave privata) e quindi su **Next** (Avanti).

    ![Passaggio 5 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. Fare clic su **Base-64 encoded X.509 (.CER)** (Codificato in base 64 X.509 (.CER)) e quindi su **Next** (Avanti).

    ![Passaggio 6 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. Assegnare un nome di certificato hello. In questo caso, **documentdbemulatorcert**, quindi fare clic su **Next** (Avanti).

    ![Passaggio 7 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. Fare clic su **Finish** (Fine).

    ![Passaggio 8 dell'esportazione nell'emulatore locale di Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a>Come toouse hello certificato in Java

Durante l'esecuzione di applicazioni Java o MongoDB che utilizzano client Java hello è più facile certificato di hello tooinstall nell'archivio certificati predefinito di hello Java di passaggio hello "-Djavax.net.ssl.trustStore=<keystore> - Djavax.net.ssl.trustStorePassword= "<password>" flag. Ad esempio hello incluso [applicazione Java Demo](https://localhost:8081/_explorer/index.html) dipende dall'archivio certificati predefinito di hello.

Seguire le istruzioni hello hello [aggiunta di un certificato toohello archivio certificati Autorità di certificazione Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello x. 509 del certificato nell'archivio certificati di hello predefinito Java. Tenere in considerazione che è possibile lavorare in directory hello % JAVA_HOME % quando si esegue keytool.

Una volta hello "CosmosDBEmulatorCertificate" SSL certificato sia installato l'applicazione deve essere in grado di tooconnect e utilizzare hello locale Azure Cosmos DB emulatore. Se si continuano toohave problemi è hello toofollow [debug connessioni SSL/TLS](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) articolo. È molto probabile hello certificato non è installato nell'archivio %JAVA_HOME%/jre/lib/security/cacerts hello. Per esempio, se si dispone di più versioni installate di Java l'applicazione stia utilizzando un archivio diverso cacerts di hello uno che è stato aggiornato.

## <a name="how-toouse-hello-certificate-in-python"></a>Come toouse hello certificato di Python

Da hello predefinito [SDK(version 2.0.0 or higher) Python](documentdb-sdk-python.md) per hello API DocumentDB non tenta di utilizzare certificato SSL di hello quando ci si connette emulatore locale toohello. Se tuttavia si vuole toouse SSL convalida è possibile seguire negli esempi di hello hello [Python socket wrapper](https://docs.python.org/2/library/ssl.html) documentazione.

## <a name="how-toouse-hello-certificate-in-nodejs"></a>Come toouse hello certificato in Node.js

Da hello predefinito [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) per hello API DocumentDB non tenta di utilizzare certificato SSL di hello quando ci si connette emulatore locale toohello. Se tuttavia si vuole toouse SSL convalida è possibile seguire negli esempi di hello hello [documentazione su Node.js](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, effettuata seguente hello:

> [!div class="checklist"]
> * Rotazione dei certificati
> * Certificato SSL hello esportata
> * Appreso come toouse hello certificato in Java, Python e Node.js

È ora possibile procedere toohello concetti per ulteriori informazioni su DB Cosmos.

> [!div class="nextstepaction"]
> [Distribuzione globale](distribute-data-globally.md) 
