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
# <a name="get-started-with-azure-data-lake-store-using-java"></a><span data-ttu-id="fab5c-103">Introduzione ad Archivio Azure Data Lake con Java</span><span class="sxs-lookup"><span data-stu-id="fab5c-103">Get started with Azure Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fab5c-104">Portale</span><span class="sxs-lookup"><span data-stu-id="fab5c-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="fab5c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fab5c-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="fab5c-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="fab5c-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="fab5c-107">SDK per Java</span><span class="sxs-lookup"><span data-stu-id="fab5c-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="fab5c-108">API REST</span><span class="sxs-lookup"><span data-stu-id="fab5c-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="fab5c-109">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="fab5c-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="fab5c-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="fab5c-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="fab5c-111">Python</span><span class="sxs-lookup"><span data-stu-id="fab5c-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="fab5c-112">Informazioni su come le operazioni di base toouse hello SDK per Java archivio Azure Data Lake tooperform creare, ad esempio cartelle, caricare e scaricare i file di dati e così via. Per altre informazioni su Data Lake, vedere [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fab5c-112">Learn how toouse hello Azure Data Lake Store Java SDK tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="fab5c-113">È possibile accedere a documenti di Java SDK API hello per archivio Azure Data Lake in [documenti API Java di Azure Data Lake archivio](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span><span class="sxs-lookup"><span data-stu-id="fab5c-113">You can access hello Java SDK API docs for Azure Data Lake Store at [Azure Data Lake Store Java API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fab5c-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fab5c-114">Prerequisites</span></span>
* <span data-ttu-id="fab5c-115">Kit di sviluppo Java (JDK 7 o versione successiva, usando Java versione 1.7 o successive)</span><span class="sxs-lookup"><span data-stu-id="fab5c-115">Java Development Kit (JDK 7 or higher, using Java version 1.7 or higher)</span></span>
* <span data-ttu-id="fab5c-116">Account di Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="fab5c-116">Azure Data Lake Store account.</span></span> <span data-ttu-id="fab5c-117">Seguire le istruzioni di hello in [introduzione archivio Azure Data Lake tramite il portale di Azure hello](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fab5c-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="fab5c-118">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="fab5c-118">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="fab5c-119">Questa esercitazione usa Maven per compilare e progettare le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="fab5c-119">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="fab5c-120">Sebbene sia possibile toobuild senza utilizzare un sistema di compilazione Maven o Gradle, verificare questi sistemi è molto più semplice dipendenze toomanage.</span><span class="sxs-lookup"><span data-stu-id="fab5c-120">Although it is possible toobuild without using a build system like Maven or Gradle, these systems make is much easier toomanage dependencies.</span></span>
* <span data-ttu-id="fab5c-121">(Facoltativo) E IDE come [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) oppure [Eclipse](https://www.eclipse.org/downloads/) o simili.</span><span class="sxs-lookup"><span data-stu-id="fab5c-121">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="fab5c-122">Come si esegue l'autenticazione tramite Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fab5c-122">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="fab5c-123">In questa esercitazione viene utilizzato un tooretrieve di segreto di Azure AD applicazione client un token di Azure Active Directory (autenticazione di service to service).</span><span class="sxs-lookup"><span data-stu-id="fab5c-123">In this tutorial we use a Azure AD application client secret tooretrieve an Azure Active Directory token (service-to-service authentication).</span></span> <span data-ttu-id="fab5c-124">Vengono utilizzati da questo token toocreate un file di archivio Data Lake client oggetto tooperform operazioni e le operazioni di directory.</span><span class="sxs-lookup"><span data-stu-id="fab5c-124">We use this token toocreate an Data Lake Store client object tooperform operations file and directory operations.</span></span> <span data-ttu-id="fab5c-125">Per istruzioni su come tooauthenticate con archivio Azure Data Lake hello segreto client, è eseguire hello seguendo i passaggi generali:</span><span class="sxs-lookup"><span data-stu-id="fab5c-125">For instructions on how tooauthenticate with Azure Data Lake Store using hello client secret, we perform hello following high-level steps:</span></span>

1. <span data-ttu-id="fab5c-126">Creare un'applicazione Web di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fab5c-126">Create an Azure AD web application</span></span>
2. <span data-ttu-id="fab5c-127">Recuperare l'endpoint del token per l'applicazione web di Azure AD hello hello client ID e segreto client.</span><span class="sxs-lookup"><span data-stu-id="fab5c-127">Retrieve hello client ID, client secret, and token endpoint for hello Azure AD web application.</span></span>
3. <span data-ttu-id="fab5c-128">Configurare l'accesso per l'applicazione web di Azure AD hello in hello archivio Data Lake file/cartella da tooaccess da hello applicazione Java che si sta creando.</span><span class="sxs-lookup"><span data-stu-id="fab5c-128">Configure access for hello Azure AD web application on hello Data Lake Store file/folder that you want tooaccess from hello Java application you are creating.</span></span>

<span data-ttu-id="fab5c-129">Per istruzioni su come tooperform questi passaggi, vedere [creare un'applicazione Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="fab5c-129">For instructions on how tooperform these steps, see [Create an Active Directory application](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="fab5c-130">Azure Active Directory fornisce che le altre opzioni nonché tooretrieve un token.</span><span class="sxs-lookup"><span data-stu-id="fab5c-130">Azure Active Directory provides other options as well tooretrieve a token.</span></span> <span data-ttu-id="fab5c-131">È possibile scegliere tra un numero di autenticazione diversi meccanismi toosuit dello scenario, ad esempio, un'applicazione in esecuzione in un browser, un'applicazione distribuita come un'applicazione desktop o un'applicazione server in esecuzione in locale o in virtuale di Azure macchina.</span><span class="sxs-lookup"><span data-stu-id="fab5c-131">You can pick from a number of different authentication mechanisms toosuit your scenario, for example, an application running in a browser, an application distributed as a desktop application, or a server application running on-premises or in an Azure virtual machine.</span></span> <span data-ttu-id="fab5c-132">È anche possibile scegliere tra diversi tipi di credenziali quali password, certificati, autenticazione a 2 fattori e così via. Inoltre, Azure Active Directory consente toosynchronize gli utenti di Active Directory locale con il cloud hello.</span><span class="sxs-lookup"><span data-stu-id="fab5c-132">You can also pick from different types of credentials like passwords, certificates, 2-factor authentication, etc. In addition, Azure Active Directory allows you toosynchronize your on-premises Active Directory users with hello cloud.</span></span> <span data-ttu-id="fab5c-133">Per i dettagli, vedere [Scenari di autenticazione per Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="fab5c-133">For details, see [Authentication Scenarios for Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span></span> 

## <a name="create-a-java-application"></a><span data-ttu-id="fab5c-134">Creare un'applicazione Java</span><span class="sxs-lookup"><span data-stu-id="fab5c-134">Create a Java application</span></span>
<span data-ttu-id="fab5c-135">Nell'esempio di codice Hello disponibile [su GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) illustra hello processo di creazione di file nell'archivio di hello, concatenazione di file, download di un file e l'eliminazione di alcuni file nell'archivio di hello.</span><span class="sxs-lookup"><span data-stu-id="fab5c-135">hello code sample available [on GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) walks you through hello process of creating files in hello store, concatenating files, downloading a file, and deleting some files in hello store.</span></span> <span data-ttu-id="fab5c-136">In questa sezione dell'articolo hello illustrati parti principali di hello di codice hello.</span><span class="sxs-lookup"><span data-stu-id="fab5c-136">This section of hello article walk you through hello main parts of hello code.</span></span>

1. <span data-ttu-id="fab5c-137">Creare un progetto di Maven utilizzando [sistema per mvn](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) da hello della riga di comando o con l'IDE.</span><span class="sxs-lookup"><span data-stu-id="fab5c-137">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from hello command-line or using an IDE.</span></span> <span data-ttu-id="fab5c-138">Per istruzioni su come un linguaggio toocreate progetto che utilizza IntelliJ, vedere [qui](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span><span class="sxs-lookup"><span data-stu-id="fab5c-138">For instructions on how toocreate a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="fab5c-139">Per istruzioni su come toocreate un progetto usando Eclipse, vedere [qui](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span><span class="sxs-lookup"><span data-stu-id="fab5c-139">For instructions on how toocreate a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span> 
2. <span data-ttu-id="fab5c-140">Aggiungere hello seguente dipendenze tooyour Maven **pom.xml** file.</span><span class="sxs-lookup"><span data-stu-id="fab5c-140">Add hello following dependencies tooyour Maven **pom.xml** file.</span></span> <span data-ttu-id="fab5c-141">Aggiungere hello seguente frammento di testo tra hello  **\</version >** tag e hello  **\</progetto >** tag:</span><span class="sxs-lookup"><span data-stu-id="fab5c-141">Add hello following snippet of text between hello **\</version>** tag and hello **\</project>** tag:</span></span>
   
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
   
    <span data-ttu-id="fab5c-142">Hello prima dipendenza è toouse hello SDK di archivio Data Lake (`azure-data-lake-store-sdk`) dal repository di maven hello.</span><span class="sxs-lookup"><span data-stu-id="fab5c-142">hello first dependency is toouse hello Data Lake Store SDK (`azure-data-lake-store-sdk`) from hello maven repository.</span></span> <span data-ttu-id="fab5c-143">Hello secondo dipendenza (`slf4j-nop`) è toospecify quali toouse framework di registrazione per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="fab5c-143">hello second dependency (`slf4j-nop`) is toospecify which logging framework toouse for this application.</span></span> <span data-ttu-id="fab5c-144">Usa Hello SDK di archivio Data Lake [slf4j](http://www.slf4j.org/) facciata di registrazione, che consente di scegliere da un numero di Framework di registrazione comuni, ad esempio log4j, registrazione, logback, ecc., Java o alcuna registrazione.</span><span class="sxs-lookup"><span data-stu-id="fab5c-144">hello Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="fab5c-145">Per questo esempio, si disabiliterà la registrazione, pertanto è utilizzare hello **slf4j-nop** associazione.</span><span class="sxs-lookup"><span data-stu-id="fab5c-145">For this example, we will disable logging, hence we use hello **slf4j-nop** binding.</span></span> <span data-ttu-id="fab5c-146">toouse altre opzioni di registrazione nell'app, vedere [qui](http://www.slf4j.org/manual.html#projectDep).</span><span class="sxs-lookup"><span data-stu-id="fab5c-146">toouse other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

### <a name="add-hello-application-code"></a><span data-ttu-id="fab5c-147">Aggiungere il codice dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="fab5c-147">Add hello application code</span></span>
<span data-ttu-id="fab5c-148">Esistono tre parti principali toohello codice.</span><span class="sxs-lookup"><span data-stu-id="fab5c-148">There are three main parts toohello code.</span></span>

1. <span data-ttu-id="fab5c-149">Ottenere il token di Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="fab5c-149">Obtain hello Azure Active Directory token</span></span>
2. <span data-ttu-id="fab5c-150">Utilizzare hello token toocreate un client di archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fab5c-150">Use hello token toocreate a Data Lake Store client.</span></span>
3. <span data-ttu-id="fab5c-151">Utilizzare le operazioni tooperform client hello archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fab5c-151">Use hello Data Lake Store client tooperform operations.</span></span>

#### <a name="step-1-obtain-an-azure-active-directory-token"></a><span data-ttu-id="fab5c-152">Passaggio 1: Ottenere un token di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fab5c-152">Step 1: Obtain an Azure Active Directory token.</span></span>
<span data-ttu-id="fab5c-153">SDK di archivio Data Lake Hello fornisce pratici metodi che consentono di gestire i token di sicurezza hello necessari tootalk toohello account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fab5c-153">hello Data Lake Store SDK provides convenient methods that let you manage hello security tokens needed tootalk toohello Data Lake Store account.</span></span> <span data-ttu-id="fab5c-154">Hello SDK non implica tuttavia utilizzato solo a questi metodi.</span><span class="sxs-lookup"><span data-stu-id="fab5c-154">However, hello SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="fab5c-155">È possibile usare qualsiasi altro modo per ottenere i token, come l'uso di hello [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), o il codice personalizzato.</span><span class="sxs-lookup"><span data-stu-id="fab5c-155">You can use any other means of obtaining token as well, like using hello [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

<span data-ttu-id="fab5c-156">hello toouse token tooobtain SDK di archivio Data Lake per un'applicazione Web di Active Directory hello creato in precedenza, utilizzare una delle sottoclassi di hello di `AccessTokenProvider` (hello l'esempio seguente viene utilizzato `ClientCredsTokenProvider`).</span><span class="sxs-lookup"><span data-stu-id="fab5c-156">toouse hello Data Lake Store SDK tooobtain token for hello Active Directory Web application you created earlier, use one of hello subclasses of `AccessTokenProvider` (hello example below uses `ClientCredsTokenProvider`).</span></span> <span data-ttu-id="fab5c-157">le credenziali di hello memorizza nella cache di Hello provider di token rinnova automaticamente il token hello se si tratta tooexpire utilizzata token hello tooobtain in memoria.</span><span class="sxs-lookup"><span data-stu-id="fab5c-157">hello token provider caches hello creds used tooobtain hello token in memory, and automatically renews hello token if it is about tooexpire.</span></span> <span data-ttu-id="fab5c-158">È possibile toocreate propria sottoclassi di `AccessTokenProvider` in modo token vengono ottenuti dal codice del cliente, ma per ora si hello di utilizzare solo uno forniti in hello SDK.</span><span class="sxs-lookup"><span data-stu-id="fab5c-158">It is possible toocreate your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code, but for now let's just use hello one provided in hello SDK.</span></span>

<span data-ttu-id="fab5c-159">Sostituire **completare IN-qui** con i valori effettivi hello per hello applicazione Web di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fab5c-159">Replace **FILL-IN-HERE** with hello actual values for hello Azure Active Directory Web application.</span></span>

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a><span data-ttu-id="fab5c-160">Passaggio 2: Creare un oggetto client di Azure Data Lake Store (ADLStoreClient)</span><span class="sxs-lookup"><span data-stu-id="fab5c-160">Step 2: Create an Azure Data Lake Store client (ADLStoreClient) object</span></span>
<span data-ttu-id="fab5c-161">Creazione di un [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) oggetto richiede toospecify hello archivio Data Lake account hello nome e il provider di token generato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="fab5c-161">Creating an [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object requires you toospecify hello Data Lake Store account name and hello token provider you generated in hello last step.</span></span> <span data-ttu-id="fab5c-162">Si noti che hello account archivio Data Lake nome deve toobe un nome di dominio completo.</span><span class="sxs-lookup"><span data-stu-id="fab5c-162">Note that hello Data Lake Store account name needs toobe a fully qualified domain name.</span></span> <span data-ttu-id="fab5c-163">Ad esempio, sostituire **COMPLETARE QUI** con qualcosa simile a **mydatalakestore.azuredatalakestore.net**.</span><span class="sxs-lookup"><span data-stu-id="fab5c-163">For example, replace **FILL-IN-HERE** with something like **mydatalakestore.azuredatalakestore.net**.</span></span>

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a><span data-ttu-id="fab5c-164">Passaggio 3: Utilizzare hello ADLStoreClient tooperform file e directory</span><span class="sxs-lookup"><span data-stu-id="fab5c-164">Step 3: Use hello ADLStoreClient tooperform file and directory operations</span></span>
<span data-ttu-id="fab5c-165">codice Hello riportato di seguito contiene frammenti di codice di esempio di alcune operazioni comuni.</span><span class="sxs-lookup"><span data-stu-id="fab5c-165">hello code below contains example snippets of some common operations.</span></span> <span data-ttu-id="fab5c-166">È possibile esaminare hello completo [documenti Data Lake archivio Java SDK API](https://azure.github.io/azure-data-lake-store-java/javadoc/) di hello **ADLStoreClient** oggetto toosee altre operazioni.</span><span class="sxs-lookup"><span data-stu-id="fab5c-166">You can look at hello full [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) of hello **ADLStoreClient** object toosee other operations.</span></span>

<span data-ttu-id="fab5c-167">Si noti che i file vengono letti e scritti attraverso i flussi Java standard.</span><span class="sxs-lookup"><span data-stu-id="fab5c-167">Note that files are read from and written into using standard Java streams.</span></span> <span data-ttu-id="fab5c-168">Ciò significa che è possibile creare livelli di uno qualsiasi dei flussi di su hello hello Java in che archivio Data Lake flussi toobenefit dalla funzionalità di linguaggio standard (ad esempio, stampa flussi per l'output formattato o uno qualsiasi dei flussi di compressione o crittografia hello per le funzionalità aggiuntive Top, ecc.).</span><span class="sxs-lookup"><span data-stu-id="fab5c-168">This means that you can layer any of hello Java streams on top of hello Data Lake Store streams toobenefit from standard Java functionality (e.g., Print streams for formatted output, or any of hello compression or encryption streams for additional functionality on top, etc.).</span></span>

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

#### <a name="step-4-build-and-run-hello-application"></a><span data-ttu-id="fab5c-169">Passaggio 4: Compilare ed eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="fab5c-169">Step 4: Build and run hello application</span></span>
1. <span data-ttu-id="fab5c-170">toorun dall'IDE, individuare e premere hello **eseguire** pulsante.</span><span class="sxs-lookup"><span data-stu-id="fab5c-170">toorun from within an IDE, locate and press hello **Run** button.</span></span> <span data-ttu-id="fab5c-171">toorun Maven, utilizzare [exec: exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span><span class="sxs-lookup"><span data-stu-id="fab5c-171">toorun from Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span></span>
2. <span data-ttu-id="fab5c-172">un file jar autonomo che è possibile eseguire dalla riga di comando di compilazione hello jar con tutte le dipendenze, incluse utilizzando hello tooproduce [plug-in assembly di Maven](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span><span class="sxs-lookup"><span data-stu-id="fab5c-172">tooproduce a standalone jar that you can run from command-line build hello jar with all dependencies included, using hello [Maven assembly plugin](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span></span> <span data-ttu-id="fab5c-173">Hello pom.xml in hello [esempio di codice sorgente su github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) è un esempio di come toodo questo.</span><span class="sxs-lookup"><span data-stu-id="fab5c-173">hello pom.xml in hello [example source code on github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) has an example of how toodo this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fab5c-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fab5c-174">Next steps</span></span>
* [<span data-ttu-id="fab5c-175">Esplorare JavaDoc per hello SDK per Java</span><span class="sxs-lookup"><span data-stu-id="fab5c-175">Explore JavaDoc for hello Java SDK</span></span>](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [<span data-ttu-id="fab5c-176">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="fab5c-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="fab5c-177">Usare Azure Data Lake Analytics con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="fab5c-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="fab5c-178">Usare Azure HDInsight con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="fab5c-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

