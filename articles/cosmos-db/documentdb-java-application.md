---
title: Esercitazione sullo sviluppo di un'applicazione Java tramite Azure Cosmos DB | Microsoft Docs
description: Questa esercitazione sull'applicazione Web Java spiega come usare Azure Cosmos DB e l'API di DocumentDB per archiviare e accedere ai dati da un'applicazione Java ospitata nei siti Web di Azure.
keywords: Sviluppo di applicazioni, esercitazione sul database, applicazione Java, esercitazione sull'applicazione Web Java, DocumentDB, Azure, Microsoft Azure
services: cosmos-db
documentationcenter: java
author: dennyglee
manager: jhubbard
editor: mimig
ms.assetid: 0867a4a2-4bf5-4898-a1f4-44e3868f8725
ms.service: cosmos-db
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 08/22/2017
ms.author: denlee
ms.openlocfilehash: 292115b5603c6f05a5eab3492d4b3e2096b58ed2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-the-documentdb-api"></a><span data-ttu-id="d84b6-104">Creare un'applicazione Web Java con Azure Cosmos DB e l'API di DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d84b6-104">Build a Java web application using Azure Cosmos DB and the DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d84b6-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d84b6-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="d84b6-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="d84b6-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="d84b6-107">Java</span><span class="sxs-lookup"><span data-stu-id="d84b6-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="d84b6-108">Python</span><span class="sxs-lookup"><span data-stu-id="d84b6-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="d84b6-109">Questa esercitazione sull'applicazione Web Java illustra come usare il servizio [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) per archiviare i dati e accedervi da un'applicazione Java ospitata in app Web del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="d84b6-109">This Java web application tutorial shows you how to use the [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service to store and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="d84b6-110">In questo argomento, si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="d84b6-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="d84b6-111">Come creare un'applicazione JavaServer Pages (JSP) di base in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d84b6-111">How to build a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="d84b6-112">Come usare il servizio Azure Cosmos DB tramite [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="d84b6-112">How to work with the Azure Cosmos DB service using the [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="d84b6-113">Questa esercitazione illustra come creare un'applicazione di gestione delle attività basata su Web che consente di creare, recuperare e contrassegnare le attività come completate, come illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="d84b6-113">This Java application tutorial shows you how to create a web-based task-management application that enables you to create, retrieve, and mark tasks as complete, as shown in the following image.</span></span> <span data-ttu-id="d84b6-114">Tutte le attività nell'elenco attività vengono memorizzate come documenti JSON in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d84b6-114">Each of the tasks in the ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![Applicazione Java My ToDo List](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="d84b6-116">Questa esercitazione sullo sviluppo dell’applicazione presuppone che l'utente abbia già acquisito familiarità con l'uso di Java.</span><span class="sxs-lookup"><span data-stu-id="d84b6-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="d84b6-117">Se non si ha alcuna esperienza riguardo a Java o agli [strumenti richiesti come prerequisiti](#Prerequisites), è consigliabile scaricare il progetto [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) completo da GitHub e creare l'applicazione usando le [istruzioni alla fine di questo articolo](#GetProject).</span><span class="sxs-lookup"><span data-stu-id="d84b6-117">If you are new to Java or the [prerequisite tools](#Prerequisites), we recommend downloading the complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [the instructions at the end of this article](#GetProject).</span></span> <span data-ttu-id="d84b6-118">Una volta creata la soluzione, è possibile leggere l'articolo per approfondire il codice nel contesto del progetto.</span><span class="sxs-lookup"><span data-stu-id="d84b6-118">Once you have it built, you can review the article to gain insight on the code in the context of the project.</span></span>  
> 
> 

## <span data-ttu-id="d84b6-119"><a id="Prerequisites"></a>Prerequisiti per questa esercitazione sull'applicazione Web Java</span><span class="sxs-lookup"><span data-stu-id="d84b6-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="d84b6-120">Prima di iniziare questa esercitazione sullo sviluppo dell’applicazione, è necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="d84b6-120">Before you begin this application development tutorial, you must have the following:</span></span>

* <span data-ttu-id="d84b6-121">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="d84b6-121">An active Azure account.</span></span> <span data-ttu-id="d84b6-122">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="d84b6-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d84b6-123">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d84b6-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="d84b6-124">OPPURE</span><span class="sxs-lookup"><span data-stu-id="d84b6-124">OR</span></span>

    <span data-ttu-id="d84b6-125">Un'installazione locale dell'[emulatore Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="d84b6-125">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="d84b6-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="d84b6-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="d84b6-127">Eclipse IDE per sviluppatori Java EE.</span><span class="sxs-lookup"><span data-stu-id="d84b6-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="d84b6-128">Un sito Web di Azure con Java Runtime Environment (ad esempio Tomcat o Jetty) abilitato.</span><span class="sxs-lookup"><span data-stu-id="d84b6-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="d84b6-129">Se questi strumenti vengono installati per la prima volta, coreservlets.com fornisce una procedura dettagliata del processo di installazione nella sezione introduttiva dell'articolo relativo all' [esercitazione sull'installazione di TomCat7 e il relativo uso con Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) .</span><span class="sxs-lookup"><span data-stu-id="d84b6-129">If you're installing these tools for the first time, coreservlets.com provides a walk-through of the installation process in the Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="d84b6-130"><a id="CreateDB"></a>Passaggio 1: Creare un account di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d84b6-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="d84b6-131">Creare prima di tutto un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d84b6-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="d84b6-132">Se si ha già un account o si usa l'emulatore Azure Cosmos DB per questa esercitazione, è possibile proseguire con il [Passaggio 2: Creare l'applicazione Java JSP](#CreateJSP).</span><span class="sxs-lookup"><span data-stu-id="d84b6-132">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create the Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="d84b6-133"><a id="CreateJSP"></a>Passaggio 2: Creare l'applicazione Java JSP</span><span class="sxs-lookup"><span data-stu-id="d84b6-133"><a id="CreateJSP"></a>Step 2: Create the Java JSP application</span></span>
<span data-ttu-id="d84b6-134">Per creare l'applicazione JSP:</span><span class="sxs-lookup"><span data-stu-id="d84b6-134">To create the JSP application:</span></span>

1. <span data-ttu-id="d84b6-135">Iniziare innanzitutto con la creazione di un progetto Java.</span><span class="sxs-lookup"><span data-stu-id="d84b6-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="d84b6-136">Avviare Eclipse, quindi fare clic su **File**, **New** (Nuovo) e quindi su **Dynamic Web Project** (Progetto Web dinamico).</span><span class="sxs-lookup"><span data-stu-id="d84b6-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="d84b6-137">Se **Dynamic Web Project** (Progetto Web dinamico) non è presente nell'elenco dei progetti disponibili, seguire questa procedura: fare clic su **File**, su **New** (Nuovo) e su **Project** (Progetto), espandere **Web**, fare clic su **Dynamic Web Project** (Progetto Web dinamico), quindi selezionare **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="d84b6-137">If you don’t see **Dynamic Web Project** listed as an available project, do the following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![Sviluppo di applicazioni Java JSP](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="d84b6-139">Immettere un nome di progetto nella casella **Project name** (Nome progetto) e dal menu a discesa **Target Runtime** (Runtime di destinazione) selezionare facoltativamente un valore, ad esempio Apache Tomcat v7.0, e quindi fare clic su **Finish** (Fine).</span><span class="sxs-lookup"><span data-stu-id="d84b6-139">Enter a project name in the **Project name** box, and in the **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="d84b6-140">Se si seleziona un runtime di destinazione, sarà possibile eseguire il progetto in locale tramite Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d84b6-140">Selecting a target runtime enables you to run your project locally through Eclipse.</span></span>
3. <span data-ttu-id="d84b6-141">Nella vista Project Explorer di Eclipse espandere il progetto.</span><span class="sxs-lookup"><span data-stu-id="d84b6-141">In Eclipse, in the Project Explorer view, expand your project.</span></span> <span data-ttu-id="d84b6-142">Fare clic con il pulsante destro del mouse su **WebContent**, scegliere **New** e quindi fare clic su **JSP File**.</span><span class="sxs-lookup"><span data-stu-id="d84b6-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="d84b6-143">Nella finestra di dialogo **New JSP File** (Nuovo file JSP) assegnare al file il nome **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="d84b6-143">In the **New JSP File** dialog box, name the file **index.jsp**.</span></span> <span data-ttu-id="d84b6-144">Mantenere il nome **WebContent** per la cartella padre, come illustrato di seguito, e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="d84b6-144">Keep the parent folder as **WebContent**, as shown in the following illustration, and then click **Next**.</span></span>
   
    ![Esercitazione sull’applicazione web Java - Creare un nuovo File JSP](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="d84b6-146">Per le finalità di questa esercitazione, nella finestra di dialogo **Select JSP Template** (Seleziona modello JSP) selezionare **New JSP File (html)** (Nuovo file JSP - html), quindi fare clic su **Finish** (Fine).</span><span class="sxs-lookup"><span data-stu-id="d84b6-146">In the **Select JSP Template** dialog box, for the purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="d84b6-147">Quando in Eclipse viene aperto il file index.jsp, aggiungere il testo in modo da visualizzare **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="d84b6-147">When the index.jsp file opens in Eclipse, add text to display **Hello World!**</span></span> <span data-ttu-id="d84b6-148">all'interno dell'elemento <body> esistente.</span><span class="sxs-lookup"><span data-stu-id="d84b6-148">within the existing <body> element.</span></span> <span data-ttu-id="d84b6-149">Il contenuto <body> aggiornato dovrebbe avere un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="d84b6-149">Your updated <body> content should look like the following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="d84b6-150">Salvare il file index.jsp.</span><span class="sxs-lookup"><span data-stu-id="d84b6-150">Save the index.jsp file.</span></span>
8. <span data-ttu-id="d84b6-151">Se nel passaggio 2 è stato impostato un runtime di destinazione, è possibile fare clic su **Project** (Progetto), quindi su **Run** (Esegui) per eseguire l'applicazione JSP in locale:</span><span class="sxs-lookup"><span data-stu-id="d84b6-151">If you set a target runtime in step 2, you can click **Project** and then **Run** to run your JSP application locally:</span></span>
   
    ![Esercitazione sull’applicazione Java - Hello World](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="d84b6-153"><a id="InstallSDK"></a>Passaggio 3: Installazione di DocumentDB Java SDK</span><span class="sxs-lookup"><span data-stu-id="d84b6-153"><a id="InstallSDK"></a>Step 3: Install the DocumentDB Java SDK</span></span>
<span data-ttu-id="d84b6-154">Il modo più semplice per inserire DocumentDB Java SDK e le relative dipendenze è tramite [Apache Maven](http://maven.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="d84b6-154">The easiest way to pull in the DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="d84b6-155">A tale scopo, sarà necessario convertire il progetto in un progetto Maven completando i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d84b6-155">To do this, you will need to convert your project to a maven project by completing the following steps:</span></span>

1. <span data-ttu-id="d84b6-156">Fare clic con il pulsante destro del mouse sul progetto in Project Explorer (Esplora progetti), scegliere **Configure** (Configura) e quindi fare clic su **Convert to Maven Project** (Converti in progetto Maven).</span><span class="sxs-lookup"><span data-stu-id="d84b6-156">Right-click your project in the Project Explorer, click **Configure**, click **Convert to Maven Project**.</span></span>
2. <span data-ttu-id="d84b6-157">Nella finestra **Create new POM** (Crea nuovo POM) accettare le impostazioni predefinite e fare clic su **Finish** (Fine).</span><span class="sxs-lookup"><span data-stu-id="d84b6-157">In the **Create new POM** window, accept the defaults and click **Finish**.</span></span>
3. <span data-ttu-id="d84b6-158">In **Project Explorer**, aprire il file pom.xml.</span><span class="sxs-lookup"><span data-stu-id="d84b6-158">In **Project Explorer**, open the pom.xml file.</span></span>
4. <span data-ttu-id="d84b6-159">Nel riquadro **Dependencies** (Dipendenze) della scheda **Dependencies** (Dipendenze), fare clic su **Add** (Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="d84b6-159">On the **Dependencies** tab, in the **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="d84b6-160">Nella finestra **Select Dependency** (Seleziona dipendenza) eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d84b6-160">In the **Select Dependency** window, do the following:</span></span>
   
   * <span data-ttu-id="d84b6-161">Nella casella **Group Id** immettere com.microsoft.azure.</span><span class="sxs-lookup"><span data-stu-id="d84b6-161">In the **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="d84b6-162">Nella casella **Artifact Id** immettere azure-documentdb.</span><span class="sxs-lookup"><span data-stu-id="d84b6-162">In the **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="d84b6-163">Nella casella **Version** immettere 1.5.1.</span><span class="sxs-lookup"><span data-stu-id="d84b6-163">In the **Version** box, enter 1.5.1.</span></span>
     
   ![Installare l'SDK dell’applicazione Java di DocumentDB](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="d84b6-165">Oppure aggiungere l'XML della dipendenza per Group Id e Artifact Id direttamente nel file pom.xml mediante un editor di testo:</span><span class="sxs-lookup"><span data-stu-id="d84b6-165">Or add the dependency XML for Group Id and Artifact Id directly to the pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="d84b6-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span><span class="sxs-lookup"><span data-stu-id="d84b6-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="d84b6-167">Fare clic su **OK** e Maven installerà DocumentDB Java SDK.</span><span class="sxs-lookup"><span data-stu-id="d84b6-167">Click **OK** and Maven will install the DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="d84b6-168">Salvare il file pom.xml.</span><span class="sxs-lookup"><span data-stu-id="d84b6-168">Save the pom.xml file.</span></span>

## <span data-ttu-id="d84b6-169"><a id="UseService"></a>Passaggio 4: Uso del servizio Azure Cosmos DB in un'applicazione Java</span><span class="sxs-lookup"><span data-stu-id="d84b6-169"><a id="UseService"></a>Step 4: Using the Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="d84b6-170">Definire innanzitutto l'oggetto TodoItem in TodoItem.java:</span><span class="sxs-lookup"><span data-stu-id="d84b6-170">First, let's define the TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="d84b6-171">In questo progetto viene usato [Project Lombok](http://projectlombok.org/) per generare il costruttore, getter, setter e un generatore.</span><span class="sxs-lookup"><span data-stu-id="d84b6-171">In this project, we are using [Project Lombok](http://projectlombok.org/) to generate the constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="d84b6-172">In alternativa, è possibile scrivere il codice manualmente o farlo generare da IDE.</span><span class="sxs-lookup"><span data-stu-id="d84b6-172">Alternatively, you can write this code manually or have the IDE generate it.</span></span>
2. <span data-ttu-id="d84b6-173">Per richiamare il servizio Azure Cosmos DB, è necessario creare un'istanza di un nuovo client **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="d84b6-173">To invoke the Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="d84b6-174">È in genere preferibile riutilizzare il client **DocumentClient** anziché creare un nuovo client per ogni richiesta successiva.</span><span class="sxs-lookup"><span data-stu-id="d84b6-174">In general, it is best to reuse the **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="d84b6-175">È possibile riutilizzare il client eseguendo il wrapping del client in una factory **DocumentClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="d84b6-175">We can reuse the client by wrapping the client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="d84b6-176">In DocumentClientFactory.java è necessario incollare i valori URI e CHIAVE PRIMARIA salvati negli Appunti al [passaggio 1](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="d84b6-176">In DocumentClientFactory.java, you need to paste the URI and PRIMARY KEY value you saved to your clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="d84b6-177">Sostituire [YOUR\_ENDPOINT\_HERE] con l'URI e sostituire [YOUR\_KEY\_HERE] con la CHIAVE PRIMARIA.</span><span class="sxs-lookup"><span data-stu-id="d84b6-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="d84b6-178">Creare a questo punto un oggetto DAO (Data Access Object) per astrarre in modo permanente gli elementi ToDo in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d84b6-178">Now let's create a Data Access Object (DAO) to abstract persisting our ToDo items to Azure Cosmos DB.</span></span>
   
    <span data-ttu-id="d84b6-179">Per salvare gli elementi ToDo in una raccolta, il client deve conoscere i database e le raccolte da rendere permanenti (in base al riferimento dei collegamenti automatici).</span><span class="sxs-lookup"><span data-stu-id="d84b6-179">In order to save ToDo items to a collection, the client needs to know which database and collection to persist to (as referenced by self-links).</span></span> <span data-ttu-id="d84b6-180">È in genere preferibile memorizzare nella cache database e raccolte appena possibile, in modo da evitare episodi di round trip del database.</span><span class="sxs-lookup"><span data-stu-id="d84b6-180">In general, it is best to cache the database and collection when possible to avoid additional round-trips to the database.</span></span>
   
    <span data-ttu-id="d84b6-181">Il codice seguente illustra come recuperare il database e la raccolta, se esistenti, o crearne di nuovi se non esistenti:</span><span class="sxs-lookup"><span data-stu-id="d84b6-181">The following code illustrates how to retrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // The name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // The name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // The Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for the database object, so we don't have to query for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for the collection object, so we don't have to query for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get the database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache the database object so we won't have to query for it
                        // later to retrieve the selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create the database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get the collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache the collection object so we won't have to query for it
                        // later to retrieve the selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create the collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="d84b6-182">Il passaggio successivo consiste nella scrittura di codice per rendere permanenti gli elementi TodoItems nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="d84b6-182">The next step is to write some code to persist the TodoItems in to the collection.</span></span> <span data-ttu-id="d84b6-183">In questo esempio verrà usato [Gson](https://code.google.com/p/google-gson/) per serializzare e deserializzare gli oggetti POJO (Plain Old Java Object) dell'elemento TodoItem nei documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="d84b6-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) to serialize and de-serialize TodoItem Plain Old Java Objects (POJOs) to JSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize the TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate the document as a TodoItem for retrieval (so that we can
            // store multiple entity types in the collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist the document using the DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="d84b6-184">Come nel caso dei database e delle raccolte di Azure Cosmos DB, anche per fare riferimento ai documenti vengono usati collegamenti automatici.</span><span class="sxs-lookup"><span data-stu-id="d84b6-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="d84b6-185">La funzione di supporto seguente consente di recuperare documenti da un altro attributo, ad esempio "ID", piuttosto che da un collegamento automatico:</span><span class="sxs-lookup"><span data-stu-id="d84b6-185">The following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve the document using the DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. <span data-ttu-id="d84b6-186">Il metodo di supporto al passaggio 5 consente di recuperare un documento JSON dell'elemento TodoItem in base all'ID e di deserializzarlo in un oggetto POJO:</span><span class="sxs-lookup"><span data-stu-id="d84b6-186">We can use the helper method in step 5 to retrieve a TodoItem JSON document by id and then deserialize it to a POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve the document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize the document in to a TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="d84b6-187">È inoltre possibile usare il client DocumentClient per ottenere una raccolta o un elenco di elementi TodoItems mediante DocumentDB SQL:</span><span class="sxs-lookup"><span data-stu-id="d84b6-187">We can also use the DocumentClient to get a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve the TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize the documents in to TodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="d84b6-188">Sono disponibili diversi metodi per aggiornare un documento con il client DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="d84b6-188">There are many ways to update a document with the DocumentClient.</span></span> <span data-ttu-id="d84b6-189">Nell'applicazione dell'elenco Todo, può essere utile disporre di un'opzione da attivare o disattivare in caso di completamento di un elemento TodoItem.</span><span class="sxs-lookup"><span data-stu-id="d84b6-189">In our Todo list application, we want to be able to toggle whether a TodoItem is complete.</span></span> <span data-ttu-id="d84b6-190">A tale scopo, è necessario aggiornare l'attributo "complete" nel documento:</span><span class="sxs-lookup"><span data-stu-id="d84b6-190">This can be achieved by updating the "complete" attribute within the document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve the document from the database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update the document as a JSON document directly.
            // For more complex operations - you could de-serialize the document in
            // to a POJO, update the POJO, and then re-serialize the POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace the updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="d84b6-191">Infine, può essere utile disporre di un'opzione che consenta di eliminare un elemento TodoItem dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="d84b6-191">Finally, we want the ability to delete a TodoItem from our list.</span></span> <span data-ttu-id="d84b6-192">A tale scopo, è possibile usare il metodo di supporto scritto in precedenza per recuperare il collegamento automatico e quindi indicare al client di eliminarlo:</span><span class="sxs-lookup"><span data-stu-id="d84b6-192">To do this, we can use the helper method we wrote earlier to retrieve the self-link and then tell the client to delete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers to documents by self link rather than id.
   
            // Query for the document to retrieve the self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete the document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <span data-ttu-id="d84b6-193"><a id="Wire"></a>Passaggio 5: Collegare il resto del progetto di sviluppo dell'applicazione Java</span><span class="sxs-lookup"><span data-stu-id="d84b6-193"><a id="Wire"></a>Step 5: Wiring the rest of the of Java application development project together</span></span>
<span data-ttu-id="d84b6-194">Dopo aver completato questi passaggi, è necessario creare un'interfaccia utente intuitiva e collegarla all'oggetto DAO.</span><span class="sxs-lookup"><span data-stu-id="d84b6-194">Now that we've finished the fun bits - all that's left is to build a quick user interface and wire it up to our DAO.</span></span>

1. <span data-ttu-id="d84b6-195">Creare innanzitutto un controller per la chiamata dell'oggetto DAO:</span><span class="sxs-lookup"><span data-stu-id="d84b6-195">First, let's start with building a controller to call our DAO:</span></span>
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    <span data-ttu-id="d84b6-196">In un'applicazione più complessa il controller può ospitare una logica di business articolata nell'oggetto DAO.</span><span class="sxs-lookup"><span data-stu-id="d84b6-196">In a more complex application, the controller may house complicated business logic on top of the DAO.</span></span>
2. <span data-ttu-id="d84b6-197">Creare in seguito un oggetto servlet per l'indirizzamento delle richieste HTTP al controller:</span><span class="sxs-lookup"><span data-stu-id="d84b6-197">Next, we'll create a servlet to route HTTP requests to the controller:</span></span>
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. <span data-ttu-id="d84b6-198">Sarà necessaria un'interfaccia utente Web per la visualizzazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d84b6-198">We'll need a web user interface to display to the user.</span></span> <span data-ttu-id="d84b6-199">A tale scopo, riscrivere il file index.jsp creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="d84b6-199">Let's re-write the index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding to body for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- The ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at the end of the document so the pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="d84b6-200">Scrivere infine codice JavaScript sul lato client per il collegamento dell'interfaccia utente Web e dell'oggetto servlet:</span><span class="sxs-lookup"><span data-stu-id="d84b6-200">And finally, write some client-side JavaScript to tie the web user interface and the servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods to call Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api to update todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install the TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. <span data-ttu-id="d84b6-201">A questo punto,</span><span class="sxs-lookup"><span data-stu-id="d84b6-201">Awesome!</span></span> <span data-ttu-id="d84b6-202">è necessario testare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d84b6-202">Now all that's left is to test the application.</span></span> <span data-ttu-id="d84b6-203">Eseguire l'applicazione in locale e aggiungere alcuni elementi Todo specificando i valori relativi al nome e alla categoria dell'elemento e selezionando **Add Task** (Aggiungi attività).</span><span class="sxs-lookup"><span data-stu-id="d84b6-203">Run the application locally, and add some Todo items by filling in the item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="d84b6-204">Quando l'elemento viene visualizzato, è possibile aggiornarne lo stato attivando o disattivando la relativa casella di controllo e facendo clic su **Update Tasks**.</span><span class="sxs-lookup"><span data-stu-id="d84b6-204">Once the item appears, you can update whether it's complete by toggling the checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="d84b6-205"><a id="Deploy"></a>Passaggio 6: Distribuire l'applicazione Java in Siti Web di Azure</span><span class="sxs-lookup"><span data-stu-id="d84b6-205"><a id="Deploy"></a>Step 6: Deploy your Java application to Azure Web Sites</span></span>
<span data-ttu-id="d84b6-206">Con Siti Web di Azure la procedura di distribuzione di applicazioni Java è molto semplice e consiste nell'esportazione di un'applicazione come file con WAR e nel relativo caricamento tramite controllo del codice sorgente (ad esempio Git) o FTP.</span><span class="sxs-lookup"><span data-stu-id="d84b6-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="d84b6-207">Per esportare l'applicazione come file WAR, fare clic con il pulsante destro del mouse sul progetto in **Project Explorer** (Esplora progetti), fare clic su **Export** (Esporta) e quindi su **WAR File** (File WAR).</span><span class="sxs-lookup"><span data-stu-id="d84b6-207">To export your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="d84b6-208">Nella finestra **WAR Export** eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d84b6-208">In the **WAR Export** window, do the following:</span></span>
   
   * <span data-ttu-id="d84b6-209">Nella casella Web project immettere azure-documentdb-java-sample.</span><span class="sxs-lookup"><span data-stu-id="d84b6-209">In the Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="d84b6-210">Nella casella Destination scegliere una destinazione in cui salvare il file WAR.</span><span class="sxs-lookup"><span data-stu-id="d84b6-210">In the Destination box, choose a destination to save the WAR file.</span></span>
   * <span data-ttu-id="d84b6-211">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="d84b6-211">Click **Finish**.</span></span>
3. <span data-ttu-id="d84b6-212">A questo punto è sufficiente caricare il file nella directory **webapps** di Siti Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="d84b6-212">Now that you have a WAR file in hand, you can simply upload it to your Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="d84b6-213">Per istruzioni sul caricamento del file, vedere [Distribuire l'applicazione di esempio nelle app Web di Servizio app di Azure](../app-service-web/web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="d84b6-213">For instructions on uploading the file, see [Add a Java application to Azure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="d84b6-214">Dopo aver caricato il file con estensione war nella directory webapps, l'ambiente di runtime identificherà il file aggiunto e lo caricherà automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d84b6-214">Once the WAR file is uploaded to the webapps directory, the runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="d84b6-215">Per visualizzare il prodotto finito, passare a http://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ e iniziare ad aggiungere le attività.</span><span class="sxs-lookup"><span data-stu-id="d84b6-215">To view your finished product, navigate to http://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="d84b6-216"><a id="GetProject"></a>Ottenere il progetto da GitHub</span><span class="sxs-lookup"><span data-stu-id="d84b6-216"><a id="GetProject"></a>Get the project from GitHub</span></span>
<span data-ttu-id="d84b6-217">Tutti gli esempi in questa esercitazione sono inclusi nel progetto [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="d84b6-217">All the samples in this tutorial are included in the [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="d84b6-218">Per importare il progetto todo in Eclipse, assicurarsi di avere il software e le risorse elencate nella sezione [Prerequisiti](#Prerequisites) , quindi eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d84b6-218">To import the todo project into Eclipse, ensure you have the software and resources listed in the [Prerequisites](#Prerequisites) section, then do the following:</span></span>

1. <span data-ttu-id="d84b6-219">Installare [Project Lombok](http://projectlombok.org/).</span><span class="sxs-lookup"><span data-stu-id="d84b6-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="d84b6-220">Lombok viene usato per generare costruttori, getter e setter nel progetto.</span><span class="sxs-lookup"><span data-stu-id="d84b6-220">Lombok is used to generate constructors, getters, setters in the project.</span></span> <span data-ttu-id="d84b6-221">Dopo aver scaricato il file lombok.jar, fare doppio clic per installarlo o eseguire l'installazione dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="d84b6-221">Once you have downloaded the lombok.jar file, double-click it to install it or install it from the command line.</span></span>
2. <span data-ttu-id="d84b6-222">Se Eclipse è aperto, chiuderlo e riavviarlo per caricare Lombok.</span><span class="sxs-lookup"><span data-stu-id="d84b6-222">If Eclipse is open, close it and restart it to load Lombok.</span></span>
3. <span data-ttu-id="d84b6-223">In Eclipse scegliere **Import** (Importa) dal menu **File**.</span><span class="sxs-lookup"><span data-stu-id="d84b6-223">In Eclipse, on the **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="d84b6-224">Nella finestra **Import** (Importa) fare clic su **Git**, su **Projects from Git** (Progetti da Git) e quindi su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="d84b6-224">In the **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="d84b6-225">Nella schermata **Select Repository Source** (Seleziona origine repository) fare clic su **Clone URI** (Clona URI).</span><span class="sxs-lookup"><span data-stu-id="d84b6-225">On the **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="d84b6-226">Nella schermata **Source Git Repository** (Repository Git di origine), nella casella **URI**, immettere https://github.com/Azure-Samples/java-todo-app.git e quindi scegliere **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="d84b6-226">On the **Source Git Repository** screen, in the **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="d84b6-227">Nella schermata **Branch Selection** (Selezione ramo) assicurarsi che sia selezionata l'opzione **master** e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="d84b6-227">On the **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="d84b6-228">Nella schermata **Local Destination** (Destinazione locale) fare clic su **Browse** (Sfoglia) per selezionare una cartella in cui sia possibile copiare il repository e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="d84b6-228">On the **Local Destination** screen, click **Browse** to select a folder where the repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="d84b6-229">Nella schermata **Select a wizard to use for importing projects** (Selezionare una procedura guidata per l'importazione di progetti) assicurarsi che l'opzione **Import existing projects** (Importa progetti esistenti) sia selezionata e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="d84b6-229">On the **Select a wizard to use for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="d84b6-230">Nella schermata **Import Projects** (Importa progetti) deselezionare il progetto **DocumentDB** e quindi fare clic su **Finish** (Fine).</span><span class="sxs-lookup"><span data-stu-id="d84b6-230">On the **Import Projects** screen, unselect the **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="d84b6-231">Il progetto DocumentDB contiene Azure Cosmos DB Java SDK, che verrà aggiunto invece come dipendenza.</span><span class="sxs-lookup"><span data-stu-id="d84b6-231">The DocumentDB project contains the Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="d84b6-232">In **Esplora progetti** passare ad azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java e sostituire i valori HOST e MASTER_KEY con i valori URI e PRIMARY KEY dell'account Azure Cosmos DB, quindi salvare il file.</span><span class="sxs-lookup"><span data-stu-id="d84b6-232">In **Project Explorer**, navigate to azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace the HOST and MASTER_KEY values with the URI and PRIMARY KEY for your Azure Cosmos DB account, and then save the file.</span></span> <span data-ttu-id="d84b6-233">Per altre informazioni, vedere [Passaggio 1. Creare un account di database Azure Cosmos DB](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="d84b6-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="d84b6-234">In **Project Explorer** (Esplora progetti) fare clic con il pulsante destro del mouse su **azure-documentdb-java-sample**, fare clic su **Build Path** (Percorso compilazione) e quindi su **Configure Build Path** (Configura percorso compilazione).</span><span class="sxs-lookup"><span data-stu-id="d84b6-234">In **Project Explorer**, right click the **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="d84b6-235">Nella schermata **Java Build Path** (Percorso compilazione Java), nel riquadro a destra selezionare la scheda **Libraries** (Librerie) e quindi fare clic su **Add External JARs** (Aggiungi JAR esterni).</span><span class="sxs-lookup"><span data-stu-id="d84b6-235">On the **Java Build Path** screen, in the right pane, select the **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="d84b6-236">Passare al percorso del file lombok.jar e fare clic su **Open** (Apri) e quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d84b6-236">Navigate to the location of the lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="d84b6-237">Vedere il passaggio 12 per aprire nuovamente la finestra **Properties** (Proprietà) e quindi nel riquadro a sinistra fare clic su **Targeted Runtimes** (Runtime di destinazione).</span><span class="sxs-lookup"><span data-stu-id="d84b6-237">Use step 12 to open the **Properties** window again, and then in the left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="d84b6-238">Nella schermata **Targeted Runtimes** (Runtime di destinazione) fare clic su **New** (Nuovo), selezionare **Apache Tomcat v7.0** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d84b6-238">On the **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="d84b6-239">Vedere il passaggio 12 per aprire nuovamente la finestra **Properties** (Proprietà) e quindi nel riquadro a sinistra fare clic su **Project Facets** (Facet di progetto).</span><span class="sxs-lookup"><span data-stu-id="d84b6-239">Use step 12 to open the **Properties** window again, and then in the left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="d84b6-240">Nella schermata **Project Facets** (Facet di progetto) selezionare **Dynamic Web Module** (Modulo Web dinamico) e **Java** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d84b6-240">On the **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="d84b6-241">Nella scheda **Servers** (Server) nella parte inferiore della schermata fare clic con il pulsante destro del mouse su **Tomcat v7.0 Server at localhost** (Server Tomcat v7.0 in localhost) e quindi fare clic su **Add and Remove** (Aggiungi e rimuovi).</span><span class="sxs-lookup"><span data-stu-id="d84b6-241">On the **Servers** tab at the bottom of the screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="d84b6-242">Nella finestra **Add and Remove** (Aggiungi e rimuovi) spostare **azure-documentdb-java-sample** nella casella **Configured** (Configurato) e quindi fare clic su **Finish** (Fine).</span><span class="sxs-lookup"><span data-stu-id="d84b6-242">On the **Add and Remove** window, move **azure-documentdb-java-sample** to the **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="d84b6-243">Nella scheda **Server** fare clic con il pulsante destro del mouse su **Tomcat v7.0 Server at localhost** (Server Tomcat v7.0 in localhost) e quindi fare clic su **Restart** (Riavvia).</span><span class="sxs-lookup"><span data-stu-id="d84b6-243">In the **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="d84b6-244">In un browser, passare a http://localhost:8080/azure-documentdb-java-sample/ e iniziare ad aggiungere all'elenco attività.</span><span class="sxs-lookup"><span data-stu-id="d84b6-244">In a browser, navigate to http://localhost:8080/azure-documentdb-java-sample/ and start adding to your task list.</span></span> <span data-ttu-id="d84b6-245">Si noti che se sono stati modificati i valori di porta predefiniti, è necessario modificare la porta 8080 con il valore selezionato.</span><span class="sxs-lookup"><span data-stu-id="d84b6-245">Note that if you changed your default port values, change 8080 to the value you selected.</span></span>
22. <span data-ttu-id="d84b6-246">Per distribuire il progetto in un sito web di Azure, vedere il [passaggio 6. Distribuire l'applicazione in Siti Web di Azure](#Deploy).</span><span class="sxs-lookup"><span data-stu-id="d84b6-246">To deploy your project to an Azure web site, see [Step 6. Deploy your application to Azure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
