---
title: Usare Java SDK per sviluppare applicazioni in Azure Data Lake Store | Documentazione Microsoft
description: Usare Java SDK con Azure Data Lake Store per creare un account Data Lake Store ed eseguire le relative operazioni di base
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
ms.openlocfilehash: 91128b53a2f1cd3ddcbee5b07da0d67668944fb4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a><span data-ttu-id="902ba-103">Introduzione ad Archivio Azure Data Lake con Java</span><span class="sxs-lookup"><span data-stu-id="902ba-103">Get started with Azure Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="902ba-104">Portale</span><span class="sxs-lookup"><span data-stu-id="902ba-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="902ba-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="902ba-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="902ba-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="902ba-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="902ba-107">SDK per Java</span><span class="sxs-lookup"><span data-stu-id="902ba-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="902ba-108">API REST</span><span class="sxs-lookup"><span data-stu-id="902ba-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="902ba-109">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="902ba-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="902ba-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="902ba-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="902ba-111">Python</span><span class="sxs-lookup"><span data-stu-id="902ba-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="902ba-112">Informazioni su come usare l'SDK Java con Azure Data Lake Store per eseguire le operazioni di base, ad esempio creare cartelle, caricare e scaricare i file di dati e così via. Per altre informazioni su Data Lake, vedere [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="902ba-112">Learn how to use the Azure Data Lake Store Java SDK to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="902ba-113">Per la documentazione API dell'SDK Java per Azure Data Lake Store accedere a [Documentazione API Java di Azure Data Lake Store](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span><span class="sxs-lookup"><span data-stu-id="902ba-113">You can access the Java SDK API docs for Azure Data Lake Store at [Azure Data Lake Store Java API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="902ba-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="902ba-114">Prerequisites</span></span>
* <span data-ttu-id="902ba-115">Kit di sviluppo Java (JDK 7 o versione successiva, usando Java versione 1.7 o successive)</span><span class="sxs-lookup"><span data-stu-id="902ba-115">Java Development Kit (JDK 7 or higher, using Java version 1.7 or higher)</span></span>
* <span data-ttu-id="902ba-116">Account di Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="902ba-116">Azure Data Lake Store account.</span></span> <span data-ttu-id="902ba-117">Seguire le istruzioni fornite in [Introduzione ad Archivio Azure Data Lake tramite il portale di Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="902ba-117">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="902ba-118">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="902ba-118">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="902ba-119">Questa esercitazione usa Maven per compilare e progettare le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="902ba-119">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="902ba-120">Sebbene sia possibile compilare senza ricorrere a un sistema di compilazione come Maven o Gradle, questi sistemi semplificano la gestione delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="902ba-120">Although it is possible to build without using a build system like Maven or Gradle, these systems make is much easier to manage dependencies.</span></span>
* <span data-ttu-id="902ba-121">(Facoltativo) E IDE come [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) oppure [Eclipse](https://www.eclipse.org/downloads/) o simili.</span><span class="sxs-lookup"><span data-stu-id="902ba-121">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="902ba-122">Come si esegue l'autenticazione tramite Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="902ba-122">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="902ba-123">In questa esercitazione si usa un segreto client dell'applicazione di Azure AD per recuperare un token di Azure Active Directory (autenticazione da servizio a servizio).</span><span class="sxs-lookup"><span data-stu-id="902ba-123">In this tutorial we use a Azure AD application client secret to retrieve an Azure Active Directory token (service-to-service authentication).</span></span> <span data-ttu-id="902ba-124">Il token viene usato per creare un oggetto client di Data Lake Store per eseguire operazioni su file e directory.</span><span class="sxs-lookup"><span data-stu-id="902ba-124">We use this token to create an Data Lake Store client object to perform operations file and directory operations.</span></span> <span data-ttu-id="902ba-125">Per istruzioni su come eseguire l'autenticazione con Azure Data Lake Store con il segreto client, fare riferimento ai passaggi principali seguenti:</span><span class="sxs-lookup"><span data-stu-id="902ba-125">For instructions on how to authenticate with Azure Data Lake Store using the client secret, we perform the following high-level steps:</span></span>

1. <span data-ttu-id="902ba-126">Creare un'applicazione Web di Azure AD</span><span class="sxs-lookup"><span data-stu-id="902ba-126">Create an Azure AD web application</span></span>
2. <span data-ttu-id="902ba-127">Recuperare l'ID client, il segreto client e l'endpoint token per l'applicazione Web di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="902ba-127">Retrieve the client ID, client secret, and token endpoint for the Azure AD web application.</span></span>
3. <span data-ttu-id="902ba-128">Configurare l'accesso per l'applicazione Web di Azure AD per il file/cartella di Data Lake Store a cui si desidera accedere dall'applicazione Java che si sta creando.</span><span class="sxs-lookup"><span data-stu-id="902ba-128">Configure access for the Azure AD web application on the Data Lake Store file/folder that you want to access from the Java application you are creating.</span></span>

<span data-ttu-id="902ba-129">Per istruzioni su come eseguire questi passaggi, vedere [Creare un'applicazione di Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="902ba-129">For instructions on how to perform these steps, see [Create an Active Directory application](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="902ba-130">Azure Active Directory offre anche altre opzioni anche per recuperare un token.</span><span class="sxs-lookup"><span data-stu-id="902ba-130">Azure Active Directory provides other options as well to retrieve a token.</span></span> <span data-ttu-id="902ba-131">È possibile scegliere tra una serie di meccanismi di autenticazione differenti da adattare allo scenario, come ad esempio un'applicazione in esecuzione in un browser, un'applicazione distribuita come applicazione desktop o un'applicazione server in esecuzione in locale o su una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="902ba-131">You can pick from a number of different authentication mechanisms to suit your scenario, for example, an application running in a browser, an application distributed as a desktop application, or a server application running on-premises or in an Azure virtual machine.</span></span> <span data-ttu-id="902ba-132">È anche possibile scegliere tra diversi tipi di credenziali quali password, certificati, autenticazione a 2 fattori e così via. Inoltre, Azure Active Directory consente di sincronizzare gli utenti di Active Directory locali con il cloud.</span><span class="sxs-lookup"><span data-stu-id="902ba-132">You can also pick from different types of credentials like passwords, certificates, 2-factor authentication, etc. In addition, Azure Active Directory allows you to synchronize your on-premises Active Directory users with the cloud.</span></span> <span data-ttu-id="902ba-133">Per i dettagli, vedere [Scenari di autenticazione per Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="902ba-133">For details, see [Authentication Scenarios for Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span></span> 

## <a name="create-a-java-application"></a><span data-ttu-id="902ba-134">Creare un'applicazione Java</span><span class="sxs-lookup"><span data-stu-id="902ba-134">Create a Java application</span></span>
<span data-ttu-id="902ba-135">Il codice di esempio disponibile in [GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) offre una descrizione dei processi di creazione dei file nell'archivio, concatenazione dei file, download di un file ed eliminazione di alcuni file nell'archivio.</span><span class="sxs-lookup"><span data-stu-id="902ba-135">The code sample available [on GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) walks you through the process of creating files in the store, concatenating files, downloading a file, and deleting some files in the store.</span></span> <span data-ttu-id="902ba-136">In questa sezione dell'articolo vengono descritte le parti principali del codice.</span><span class="sxs-lookup"><span data-stu-id="902ba-136">This section of the article walk you through the main parts of the code.</span></span>

1. <span data-ttu-id="902ba-137">Creare un progetto Maven usando l'[archetipo mvn](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) dalla riga di comando o con un IDE.</span><span class="sxs-lookup"><span data-stu-id="902ba-137">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from the command-line or using an IDE.</span></span> <span data-ttu-id="902ba-138">Per istruzioni su come creare un progetto Java usando IntelliJ, vedere [qui](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span><span class="sxs-lookup"><span data-stu-id="902ba-138">For instructions on how to create a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="902ba-139">Per istruzioni su come creare un progetto Java usando Eclipse, vedere [qui](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span><span class="sxs-lookup"><span data-stu-id="902ba-139">For instructions on how to create a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span> 
2. <span data-ttu-id="902ba-140">Aggiungere le dipendenze seguenti al file **pom.xml** di Maven.</span><span class="sxs-lookup"><span data-stu-id="902ba-140">Add the following dependencies to your Maven **pom.xml** file.</span></span> <span data-ttu-id="902ba-141">Aggiungere il frammento di testo seguente tra il tag **\</version>** e il tag **\</project>**:</span><span class="sxs-lookup"><span data-stu-id="902ba-141">Add the following snippet of text between the **\</version>** tag and the **\</project>** tag:</span></span>
   
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
   
    <span data-ttu-id="902ba-142">La prima dipendenza serve a usare l'SDK di Data Lake Store (`azure-data-lake-store-sdk`) dal repository di Maven.</span><span class="sxs-lookup"><span data-stu-id="902ba-142">The first dependency is to use the Data Lake Store SDK (`azure-data-lake-store-sdk`) from the maven repository.</span></span> <span data-ttu-id="902ba-143">La seconda dipendenza (`slf4j-nop`) serve a specificare quali framework di registrazione usare per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="902ba-143">The second dependency (`slf4j-nop`) is to specify which logging framework to use for this application.</span></span> <span data-ttu-id="902ba-144">L'SDK di Data Lake Store usa la façade di registrazione [SLF4J](http://www.slf4j.org/), che consente di scegliere tra un numero di framework di registrazione comuni, come SLF4J, registrazione Java, logback e così via, o nessuna registrazione.</span><span class="sxs-lookup"><span data-stu-id="902ba-144">The Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="902ba-145">In questo esempio la registrazione verrà disabilitata, quindi si farà ricorso all'associazione **SLF4J-nop**.</span><span class="sxs-lookup"><span data-stu-id="902ba-145">For this example, we will disable logging, hence we use the **slf4j-nop** binding.</span></span> <span data-ttu-id="902ba-146">Per usare altre opzioni di registrazione nell'applicazione, vedere [qui](http://www.slf4j.org/manual.html#projectDep).</span><span class="sxs-lookup"><span data-stu-id="902ba-146">To use other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

### <a name="add-the-application-code"></a><span data-ttu-id="902ba-147">Aggiungere il codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="902ba-147">Add the application code</span></span>
<span data-ttu-id="902ba-148">Il codice si compone di tre parti principali.</span><span class="sxs-lookup"><span data-stu-id="902ba-148">There are three main parts to the code.</span></span>

1. <span data-ttu-id="902ba-149">Ottenere il token di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="902ba-149">Obtain the Azure Active Directory token</span></span>
2. <span data-ttu-id="902ba-150">Usare il token per creare un client di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="902ba-150">Use the token to create a Data Lake Store client.</span></span>
3. <span data-ttu-id="902ba-151">Usare il client di Data Lake Store per eseguire le operazioni.</span><span class="sxs-lookup"><span data-stu-id="902ba-151">Use the Data Lake Store client to perform operations.</span></span>

#### <a name="step-1-obtain-an-azure-active-directory-token"></a><span data-ttu-id="902ba-152">Passaggio 1: Ottenere un token di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="902ba-152">Step 1: Obtain an Azure Active Directory token.</span></span>
<span data-ttu-id="902ba-153">Data Lake Store SDK mette a disposizione metodi pratici che consentono di gestire i token di sicurezza necessari per comunicare con l'account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="902ba-153">The Data Lake Store SDK provides convenient methods that let you manage the security tokens needed to talk to the Data Lake Store account.</span></span> <span data-ttu-id="902ba-154">Tuttavia, l'SDK non implica l'uso esclusivo di questi metodi.</span><span class="sxs-lookup"><span data-stu-id="902ba-154">However, the SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="902ba-155">È possibile usare qualsiasi altro modo per ottenere i token, come l'[SDK di Azure Active Directory](https://github.com/AzureAD/azure-activedirectory-library-for-java) o il proprio codice personalizzato.</span><span class="sxs-lookup"><span data-stu-id="902ba-155">You can use any other means of obtaining token as well, like using the [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

<span data-ttu-id="902ba-156">Per usare Data Lake Store SDK per ottenere il token per l'applicazione Web Active Directory creato prima, usare una delle sottoclassi di `AccessTokenProvider`. L'esempio seguente usa `ClientCredsTokenProvider`.</span><span class="sxs-lookup"><span data-stu-id="902ba-156">To use the Data Lake Store SDK to obtain token for the Active Directory Web application you created earlier, use one of the subclasses of `AccessTokenProvider` (the example below uses `ClientCredsTokenProvider`).</span></span> <span data-ttu-id="902ba-157">Il provider di token memorizza nella cache le credenziali usate per ottenere il token in memoria e rinnova automaticamente il token se sta per scadere.</span><span class="sxs-lookup"><span data-stu-id="902ba-157">The token provider caches the creds used to obtain the token in memory, and automatically renews the token if it is about to expire.</span></span> <span data-ttu-id="902ba-158">È possibile creare altre sottoclassi di `AccessTokenProvider` in modo che i token vengano ottenuti con il codice cliente, ma per ora verrà usata solo quella fornita nell'SDK.</span><span class="sxs-lookup"><span data-stu-id="902ba-158">It is possible to create your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code, but for now let's just use the one provided in the SDK.</span></span>

<span data-ttu-id="902ba-159">Sostituire **FILL-IN-HERE** (COMPLETARE QUI) con i valori effettivi per l'applicazione Web di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="902ba-159">Replace **FILL-IN-HERE** with the actual values for the Azure Active Directory Web application.</span></span>

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a><span data-ttu-id="902ba-160">Passaggio 2: Creare un oggetto client di Azure Data Lake Store (ADLStoreClient)</span><span class="sxs-lookup"><span data-stu-id="902ba-160">Step 2: Create an Azure Data Lake Store client (ADLStoreClient) object</span></span>
<span data-ttu-id="902ba-161">Per la creazione di un oggetto [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) si deve specificare il nome dell'account di Data Lake Store e il provider di token generato nell'ultimo passaggio.</span><span class="sxs-lookup"><span data-stu-id="902ba-161">Creating an [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object requires you to specify the Data Lake Store account name and the token provider you generated in the last step.</span></span> <span data-ttu-id="902ba-162">Si noti che il nome dell'account di Data Lake Store deve essere un nome di dominio completo.</span><span class="sxs-lookup"><span data-stu-id="902ba-162">Note that the Data Lake Store account name needs to be a fully qualified domain name.</span></span> <span data-ttu-id="902ba-163">Ad esempio, sostituire **COMPLETARE QUI** con qualcosa simile a **mydatalakestore.azuredatalakestore.net**.</span><span class="sxs-lookup"><span data-stu-id="902ba-163">For example, replace **FILL-IN-HERE** with something like **mydatalakestore.azuredatalakestore.net**.</span></span>

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just the account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-the-adlstoreclient-to-perform-file-and-directory-operations"></a><span data-ttu-id="902ba-164">Passaggio 3: Usare l'oggetto ADLStoreClient per eseguire operazioni su file e directory</span><span class="sxs-lookup"><span data-stu-id="902ba-164">Step 3: Use the ADLStoreClient to perform file and directory operations</span></span>
<span data-ttu-id="902ba-165">Il codice riportato di seguito contiene frammenti di esempio di alcune operazioni comuni.</span><span class="sxs-lookup"><span data-stu-id="902ba-165">The code below contains example snippets of some common operations.</span></span> <span data-ttu-id="902ba-166">È possibile esaminare tutta la [documentazione API relativa all'SDK Java di Data Lake Store](https://azure.github.io/azure-data-lake-store-java/javadoc/) dell'oggetto **ADLStoreClient** per vedere altre operazioni.</span><span class="sxs-lookup"><span data-stu-id="902ba-166">You can look at the full [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) of the **ADLStoreClient** object to see other operations.</span></span>

<span data-ttu-id="902ba-167">Si noti che i file vengono letti e scritti attraverso i flussi Java standard.</span><span class="sxs-lookup"><span data-stu-id="902ba-167">Note that files are read from and written into using standard Java streams.</span></span> <span data-ttu-id="902ba-168">Ciò significa che è possibile livellare uno qualsiasi dei flussi Java al livello superiore dei flussi di Data Lake Store per sfruttare la funzionalità Java standard (ad esempio i flussi di stampa per l'output formattato o uno dei flussi di compressione o crittografia per funzionalità aggiuntive del livello superiore, e così via).</span><span class="sxs-lookup"><span data-stu-id="902ba-168">This means that you can layer any of the Java streams on top of the Data Lake Store streams to benefit from standard Java functionality (e.g., Print streams for formatted output, or any of the compression or encryption streams for additional functionality on top, etc.).</span></span>

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is the same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append to file
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

    // concatenate the two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename the file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all the subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-the-application"></a><span data-ttu-id="902ba-169">Passaggio 4: Compilare ed eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="902ba-169">Step 4: Build and run the application</span></span>
1. <span data-ttu-id="902ba-170">Per eseguirla da un IDE, individuare l'applicazione e premere il pulsante **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="902ba-170">To run from within an IDE, locate and press the **Run** button.</span></span> <span data-ttu-id="902ba-171">Per eseguirla da Maven, usare [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span><span class="sxs-lookup"><span data-stu-id="902ba-171">To run from Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span></span>
2. <span data-ttu-id="902ba-172">Per produrre un file jar autonomo eseguibile dalla riga di comando, compilare il file jar con tutte le dipendenze incluse usando il [plug-in dell'assembly Maven](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span><span class="sxs-lookup"><span data-stu-id="902ba-172">To produce a standalone jar that you can run from command-line build the jar with all dependencies included, using the [Maven assembly plugin](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span></span> <span data-ttu-id="902ba-173">Il file pom.xml nell'[esempio di codice sorgente su GitHub](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) offre un esempio che descrive come eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="902ba-173">The pom.xml in the [example source code on github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) has an example of how to do this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="902ba-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="902ba-174">Next steps</span></span>
* <span data-ttu-id="902ba-175">[Explore JavaDoc for the Java SDK](https://azure.github.io/azure-data-lake-store-java/javadoc/) (Cercare Java SDK in JavaDoc)</span><span class="sxs-lookup"><span data-stu-id="902ba-175">[Explore JavaDoc for the Java SDK](https://azure.github.io/azure-data-lake-store-java/javadoc/)</span></span>
* [<span data-ttu-id="902ba-176">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="902ba-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="902ba-177">Usare Azure Data Lake Analytics con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="902ba-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="902ba-178">Usare Azure HDInsight con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="902ba-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

