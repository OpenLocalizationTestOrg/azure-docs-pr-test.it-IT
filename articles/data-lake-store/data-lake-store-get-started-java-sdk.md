---
title: applicazioni di toodevelop aaaUse hello SDK per Java in archivio Azure Data Lake | Documenti Microsoft
description: Utilizzare il SDK per Java archivio Azure Data Lake toocreate un account archivio Data Lake ed eseguire operazioni di base in hello archivio Data Lake
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d10e09db-5232-4e84-bb50-52efc2c21887
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/28/2017
ms.author: nitinme
ms.openlocfilehash: d3bcee449c2a2a4bd2f7b241af46ecc010b6b62e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a>Introduzione ad Archivio Azure Data Lake con Java
> [!div class="op_single_selector"]
> * [Portale](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [SDK per Java](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [Interfaccia della riga di comando di Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

Informazioni su come le operazioni di base toouse hello SDK per Java archivio Azure Data Lake tooperform creare, ad esempio cartelle, caricare e scaricare i file di dati e così via. Per altre informazioni su Data Lake, vedere [Azure Data Lake Store](data-lake-store-overview.md).

È possibile accedere a documenti di Java SDK API hello per archivio Azure Data Lake in [documenti API Java di Azure Data Lake archivio](https://azure.github.io/azure-data-lake-store-java/javadoc/).

## <a name="prerequisites"></a>Prerequisiti
* Kit di sviluppo Java (JDK 7 o versione successiva, usando Java versione 1.7 o successive)
* Account di Azure Data Lake Store. Seguire le istruzioni di hello in [introduzione archivio Azure Data Lake tramite il portale di Azure hello](data-lake-store-get-started-portal.md).
* [Maven](https://maven.apache.org/install.html). Questa esercitazione usa Maven per compilare e progettare le dipendenze. Sebbene sia possibile toobuild senza utilizzare un sistema di compilazione Maven o Gradle, verificare questi sistemi è molto più semplice dipendenze toomanage.
* (Facoltativo) E IDE come [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) oppure [Eclipse](https://www.eclipse.org/downloads/) o simili.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>Come si esegue l'autenticazione tramite Azure Active Directory?
In questa esercitazione viene utilizzato un tooretrieve di segreto di Azure AD applicazione client un token di Azure Active Directory (autenticazione di service to service). Vengono utilizzati da questo token toocreate un file di archivio Data Lake client oggetto tooperform operazioni e le operazioni di directory. Per istruzioni su come tooauthenticate con archivio Azure Data Lake hello segreto client, è eseguire hello seguendo i passaggi generali:

1. Creare un'applicazione Web di Azure AD
2. Recuperare l'endpoint del token per l'applicazione web di Azure AD hello hello client ID e segreto client.
3. Configurare l'accesso per l'applicazione web di Azure AD hello in hello archivio Data Lake file/cartella da tooaccess da hello applicazione Java che si sta creando.

Per istruzioni su come tooperform questi passaggi, vedere [creare un'applicazione Active Directory](data-lake-store-authenticate-using-active-directory.md).

Azure Active Directory fornisce che le altre opzioni nonché tooretrieve un token. È possibile scegliere tra un numero di autenticazione diversi meccanismi toosuit dello scenario, ad esempio, un'applicazione in esecuzione in un browser, un'applicazione distribuita come un'applicazione desktop o un'applicazione server in esecuzione in locale o in virtuale di Azure macchina. È anche possibile scegliere tra diversi tipi di credenziali quali password, certificati, autenticazione a 2 fattori e così via. Inoltre, Azure Active Directory consente toosynchronize gli utenti di Active Directory locale con il cloud hello. Per i dettagli, vedere [Scenari di autenticazione per Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md). 

## <a name="create-a-java-application"></a>Creare un'applicazione Java
Nell'esempio di codice Hello disponibile [su GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) illustra hello processo di creazione di file nell'archivio di hello, concatenazione di file, download di un file e l'eliminazione di alcuni file nell'archivio di hello. In questa sezione dell'articolo hello illustrati parti principali di hello di codice hello.

1. Creare un progetto di Maven utilizzando [sistema per mvn](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) da hello della riga di comando o con l'IDE. Per istruzioni su come un linguaggio toocreate progetto che utilizza IntelliJ, vedere [qui](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html). Per istruzioni su come toocreate un progetto usando Eclipse, vedere [qui](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm). 
2. Aggiungere hello seguente dipendenze tooyour Maven **pom.xml** file. Aggiungere hello seguente frammento di testo tra hello  **\</version >** tag e hello  **\</progetto >** tag:
   
        <dependencies>
          <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-data-lake-store-sdk</artifactId>
            <version>2.1.5</version>
          </dependency>
          <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-nop</artifactId>
            <version>1.7.21</version>
          </dependency>
        </dependencies>
   
    Hello prima dipendenza è toouse hello SDK di archivio Data Lake (`azure-data-lake-store-sdk`) dal repository di maven hello. Hello secondo dipendenza (`slf4j-nop`) è toospecify quali toouse framework di registrazione per questa applicazione. Usa Hello SDK di archivio Data Lake [slf4j](http://www.slf4j.org/) facciata di registrazione, che consente di scegliere da un numero di Framework di registrazione comuni, ad esempio log4j, registrazione, logback, ecc., Java o alcuna registrazione. Per questo esempio, si disabiliterà la registrazione, pertanto è utilizzare hello **slf4j-nop** associazione. toouse altre opzioni di registrazione nell'app, vedere [qui](http://www.slf4j.org/manual.html#projectDep).

### <a name="add-hello-application-code"></a>Aggiungere il codice dell'applicazione hello
Esistono tre parti principali toohello codice.

1. Ottenere il token di Azure Active Directory hello
2. Utilizzare hello token toocreate un client di archivio Data Lake.
3. Utilizzare le operazioni tooperform client hello archivio Data Lake.

#### <a name="step-1-obtain-an-azure-active-directory-token"></a>Passaggio 1: Ottenere un token di Azure Active Directory.
SDK di archivio Data Lake Hello fornisce pratici metodi che consentono di gestire i token di sicurezza hello necessari tootalk toohello account archivio Data Lake. Hello SDK non implica tuttavia utilizzato solo a questi metodi. È possibile usare qualsiasi altro modo per ottenere i token, come l'uso di hello [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), o il codice personalizzato.

hello toouse token tooobtain SDK di archivio Data Lake per un'applicazione Web di Active Directory hello creato in precedenza, utilizzare una delle sottoclassi di hello di `AccessTokenProvider` (hello l'esempio seguente viene utilizzato `ClientCredsTokenProvider`). le credenziali di hello memorizza nella cache di Hello provider di token rinnova automaticamente il token hello se si tratta tooexpire utilizzata token hello tooobtain in memoria. È possibile toocreate propria sottoclassi di `AccessTokenProvider` in modo token vengono ottenuti dal codice del cliente, ma per ora si hello di utilizzare solo uno forniti in hello SDK.

Sostituire **completare IN-qui** con i valori effettivi hello per hello applicazione Web di Azure Active Directory.

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a>Passaggio 2: Creare un oggetto client di Azure Data Lake Store (ADLStoreClient)
Creazione di un [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) oggetto richiede toospecify hello archivio Data Lake account hello nome e il provider di token generato nel passaggio precedente hello. Si noti che hello account archivio Data Lake nome deve toobe un nome di dominio completo. Ad esempio, sostituire **COMPLETARE QUI** con qualcosa simile a **mydatalakestore.azuredatalakestore.net**.

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a>Passaggio 3: Utilizzare hello ADLStoreClient tooperform file e directory
codice Hello riportato di seguito contiene frammenti di codice di esempio di alcune operazioni comuni. È possibile esaminare hello completo [documenti Data Lake archivio Java SDK API](https://azure.github.io/azure-data-lake-store-java/javadoc/) di hello **ADLStoreClient** oggetto toosee altre operazioni.

Si noti che i file vengono letti e scritti attraverso i flussi Java standard. Ciò significa che è possibile creare livelli di uno qualsiasi dei flussi di su hello hello Java in che archivio Data Lake flussi toobenefit dalla funzionalità di linguaggio standard (ad esempio, stampa flussi per l'output formattato o uno qualsiasi dei flussi di compressione o crittografia hello per le funzionalità aggiuntive Top, ecc.).

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is hello same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append toofile
    stream = client.getAppendStream(filename);
    stream.write(getSampleContent());
    stream.close();

    // Read File
    InputStream in = client.getReadStream(filename);
    byte[] b = new byte[64000];
    while (in.read(b) != -1) {
        System.out.write(b);
    }
    in.close();

    // concatenate hello two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename hello file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all hello subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-hello-application"></a>Passaggio 4: Compilare ed eseguire un'applicazione hello
1. toorun dall'IDE, individuare e premere hello **eseguire** pulsante. toorun Maven, utilizzare [exec: exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).
2. un file jar autonomo che è possibile eseguire dalla riga di comando di compilazione hello jar con tutte le dipendenze, incluse utilizzando hello tooproduce [plug-in assembly di Maven](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html). Hello pom.xml in hello [esempio di codice sorgente su github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) è un esempio di come toodo questo.

## <a name="next-steps"></a>Passaggi successivi
* [Esplorare JavaDoc per hello SDK per Java](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [Proteggere i dati in Data Lake Store](data-lake-store-secure-data.md)
* [Usare Azure Data Lake Analytics con Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usare Azure HDInsight con Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

