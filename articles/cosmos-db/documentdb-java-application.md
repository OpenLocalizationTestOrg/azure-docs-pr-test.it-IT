---
title: esercitazione sullo sviluppo di applicazioni aaaJava tramite Azure Cosmos DB | Documenti Microsoft
description: In questa esercitazione di applicazione web Java Mostra come toouse hello Azure Cosmos DB e l'API DocumentDB toostore hello e accedere ai dati da un'applicazione Java ospitata in siti Web di Azure.
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
ms.openlocfilehash: e073de23beb0037ee1e37b48a69e8fe7cdc3fc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a><span data-ttu-id="2b580-104">Compilare un'applicazione web Java utilizzando Azure Cosmos DB e hello API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="2b580-104">Build a Java web application using Azure Cosmos DB and hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2b580-105">.NET</span><span class="sxs-lookup"><span data-stu-id="2b580-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="2b580-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="2b580-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="2b580-107">Java</span><span class="sxs-lookup"><span data-stu-id="2b580-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="2b580-108">Python</span><span class="sxs-lookup"><span data-stu-id="2b580-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="2b580-109">In questa esercitazione di applicazione web Java illustra come hello toouse [DB di Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) servizio toostore e accedere ai dati da un'applicazione Java ospitato in App Web di servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="2b580-109">This Java web application tutorial shows you how toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service toostore and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="2b580-110">In questo argomento, si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="2b580-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="2b580-111">Come toobuild un'applicazione Java Server Pages (JSP) di base in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="2b580-111">How toobuild a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="2b580-112">La modalità del servizio utilizzando hello toowork con hello Azure Cosmos DB [Azure SDK per Java DB Cosmos](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="2b580-112">How toowork with hello Azure Cosmos DB service using hello [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="2b580-113">In questa esercitazione applicazione Java Mostra come applicazione di gestione delle attività toocreate basata sul web che consente di contrassegno, recuperare e si toocreate attività come completata, come illustrato nella seguente immagine hello.</span><span class="sxs-lookup"><span data-stu-id="2b580-113">This Java application tutorial shows you how toocreate a web-based task-management application that enables you toocreate, retrieve, and mark tasks as complete, as shown in hello following image.</span></span> <span data-ttu-id="2b580-114">Ognuna delle attività hello nell'elenco attività hello vengono archiviate come documenti JSON in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2b580-114">Each of hello tasks in hello ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![Applicazione Java My ToDo List](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="2b580-116">Questa esercitazione sullo sviluppo dell’applicazione presuppone che l'utente abbia già acquisito familiarità con l'uso di Java.</span><span class="sxs-lookup"><span data-stu-id="2b580-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="2b580-117">Se si tooJava nuova o hello [strumenti prerequisiti](#Prerequisites), si consiglia di scaricare hello completo [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) progetto da GitHub e compilazione mediante [hello istruzioni alla fine di hello di questo articolo](#GetProject).</span><span class="sxs-lookup"><span data-stu-id="2b580-117">If you are new tooJava or hello [prerequisite tools](#Prerequisites), we recommend downloading hello complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [hello instructions at hello end of this article](#GetProject).</span></span> <span data-ttu-id="2b580-118">Quando l'applicazione viene compilata, è possibile esaminare informazioni dettagliate di hello articolo toogain codice hello nel contesto di hello del progetto hello.</span><span class="sxs-lookup"><span data-stu-id="2b580-118">Once you have it built, you can review hello article toogain insight on hello code in hello context of hello project.</span></span>  
> 
> 

## <span data-ttu-id="2b580-119"><a id="Prerequisites"></a>Prerequisiti per questa esercitazione sull'applicazione Web Java</span><span class="sxs-lookup"><span data-stu-id="2b580-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="2b580-120">Prima di iniziare questa esercitazione sullo sviluppo di applicazioni, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="2b580-120">Before you begin this application development tutorial, you must have hello following:</span></span>

* <span data-ttu-id="2b580-121">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="2b580-121">An active Azure account.</span></span> <span data-ttu-id="2b580-122">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="2b580-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2b580-123">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2b580-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="2b580-124">OPPURE</span><span class="sxs-lookup"><span data-stu-id="2b580-124">OR</span></span>

    <span data-ttu-id="2b580-125">Un'installazione locale di hello [emulatore di Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="2b580-125">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="2b580-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="2b580-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="2b580-127">Eclipse IDE per sviluppatori Java EE.</span><span class="sxs-lookup"><span data-stu-id="2b580-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="2b580-128">Un sito Web di Azure con Java Runtime Environment (ad esempio Tomcat o Jetty) abilitato.</span><span class="sxs-lookup"><span data-stu-id="2b580-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="2b580-129">Se si desidera installare questi strumenti per hello prima volta, coreservlets.com fornisce una panoramica del processo di installazione hello nella sezione introduttiva di hello del loro [esercitazione: installazione TomCat7 e utilizzarlo con Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) articolo.</span><span class="sxs-lookup"><span data-stu-id="2b580-129">If you're installing these tools for hello first time, coreservlets.com provides a walk-through of hello installation process in hello Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="2b580-130"><a id="CreateDB"></a>Passaggio 1: Creare un account di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2b580-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="2b580-131">Creare prima di tutto un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2b580-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="2b580-132">Se è già un account o se si utilizza hello Azure Cosmos DB emulatore per questa esercitazione, è possibile ignorare troppo[passaggio 2: creare un'applicazione JSP Java hello](#CreateJSP).</span><span class="sxs-lookup"><span data-stu-id="2b580-132">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create hello Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="2b580-133"><a id="CreateJSP"></a>Passaggio 2: Creare un'applicazione JSP Java hello</span><span class="sxs-lookup"><span data-stu-id="2b580-133"><a id="CreateJSP"></a>Step 2: Create hello Java JSP application</span></span>
<span data-ttu-id="2b580-134">hello toocreate applicazione JSP di:</span><span class="sxs-lookup"><span data-stu-id="2b580-134">toocreate hello JSP application:</span></span>

1. <span data-ttu-id="2b580-135">Iniziare innanzitutto con la creazione di un progetto Java.</span><span class="sxs-lookup"><span data-stu-id="2b580-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="2b580-136">Avviare Eclipse, quindi fare clic su **File**, **New** (Nuovo) e quindi su **Dynamic Web Project** (Progetto Web dinamico).</span><span class="sxs-lookup"><span data-stu-id="2b580-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="2b580-137">Se non viene visualizzato **progetto Web dinamico** elencato come un progetto disponibile, hello seguente: fare clic su **File**, fare clic su **New**, fare clic su **progetto**..., espandere **Web**, fare clic su **progetto Web dinamico**, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2b580-137">If you don’t see **Dynamic Web Project** listed as an available project, do hello following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![Sviluppo di applicazioni Java JSP](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="2b580-139">Immettere un nome di progetto in hello **nome progetto** casella e in hello **destinazione Runtime** menu a discesa, selezionare facoltativamente un valore (ad esempio Apache Tomcat versione 7.0) e quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="2b580-139">Enter a project name in hello **Project name** box, and in hello **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="2b580-140">Consente la selezione di un runtime di destinazione è toorun progetto localmente mediante Eclipse.</span><span class="sxs-lookup"><span data-stu-id="2b580-140">Selecting a target runtime enables you toorun your project locally through Eclipse.</span></span>
3. <span data-ttu-id="2b580-141">Nella visualizzazione Project Explorer di hello in Eclipse, espandere il progetto.</span><span class="sxs-lookup"><span data-stu-id="2b580-141">In Eclipse, in hello Project Explorer view, expand your project.</span></span> <span data-ttu-id="2b580-142">Fare clic con il pulsante destro del mouse su **WebContent**, scegliere **New** e quindi fare clic su **JSP File**.</span><span class="sxs-lookup"><span data-stu-id="2b580-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="2b580-143">In hello **New JSP File** della finestra di dialogo file hello nome **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="2b580-143">In hello **New JSP File** dialog box, name hello file **index.jsp**.</span></span> <span data-ttu-id="2b580-144">Mantenere come cartella padre di hello **WebContent**, come illustrato nell'hello nella figura riportata di seguito e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2b580-144">Keep hello parent folder as **WebContent**, as shown in hello following illustration, and then click **Next**.</span></span>
   
    ![Esercitazione sull’applicazione web Java - Creare un nuovo File JSP](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="2b580-146">In hello **Select JSP Template** la finestra di dialogo, a scopo di hello di questa esercitazione, selezionare **New JSP File (html)**, quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="2b580-146">In hello **Select JSP Template** dialog box, for hello purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="2b580-147">All'apertura di file di hello index.jsp in Eclipse, aggiungere testo toodisplay **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="2b580-147">When hello index.jsp file opens in Eclipse, add text toodisplay **Hello World!**</span></span> <span data-ttu-id="2b580-148">all'interno di hello esistente <body> elemento.</span><span class="sxs-lookup"><span data-stu-id="2b580-148">within hello existing <body> element.</span></span> <span data-ttu-id="2b580-149">L'aggiornamento <body> contenuto dovrebbe essere simile hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="2b580-149">Your updated <body> content should look like hello following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="2b580-150">Salvare file index.jsp hello.</span><span class="sxs-lookup"><span data-stu-id="2b580-150">Save hello index.jsp file.</span></span>
8. <span data-ttu-id="2b580-151">Se si imposta un runtime di destinazione nel passaggio 2, è possibile fare clic su **progetto** e quindi **eseguire** toorun dell'applicazione JSP in locale:</span><span class="sxs-lookup"><span data-stu-id="2b580-151">If you set a target runtime in step 2, you can click **Project** and then **Run** toorun your JSP application locally:</span></span>
   
    ![Esercitazione sull’applicazione Java - Hello World](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="2b580-153"><a id="InstallSDK"></a>Passaggio 3: Installare hello DocumentDB SDK per Java</span><span class="sxs-lookup"><span data-stu-id="2b580-153"><a id="InstallSDK"></a>Step 3: Install hello DocumentDB Java SDK</span></span>
<span data-ttu-id="2b580-154">Hello toopull modo più semplice in hello DocumentDB SDK per Java e le relative dipendenze è tramite [Apache Maven](http://maven.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="2b580-154">hello easiest way toopull in hello DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="2b580-155">toodo, è necessario tooconvert il progetto di maven tooa completando hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2b580-155">toodo this, you will need tooconvert your project tooa maven project by completing hello following steps:</span></span>

1. <span data-ttu-id="2b580-156">Pulsante destro del mouse sul progetto in Project Explorer di hello, fare clic su **configura**, fare clic su **convertire tooMaven progetto**.</span><span class="sxs-lookup"><span data-stu-id="2b580-156">Right-click your project in hello Project Explorer, click **Configure**, click **Convert tooMaven Project**.</span></span>
2. <span data-ttu-id="2b580-157">In hello **creare nuovo POM** , accettare le impostazioni predefinite hello e fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="2b580-157">In hello **Create new POM** window, accept hello defaults and click **Finish**.</span></span>
3. <span data-ttu-id="2b580-158">In **Esplora progetti**, aprire il file di pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="2b580-158">In **Project Explorer**, open hello pom.xml file.</span></span>
4. <span data-ttu-id="2b580-159">In hello **dipendenze** scheda hello **dipendenze** riquadro, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2b580-159">On hello **Dependencies** tab, in hello **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="2b580-160">In hello **selezionare dipendenza** finestra hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="2b580-160">In hello **Select Dependency** window, do hello following:</span></span>
   
   * <span data-ttu-id="2b580-161">In hello **Id gruppo** immettere com.microsoft.azure.</span><span class="sxs-lookup"><span data-stu-id="2b580-161">In hello **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="2b580-162">In hello **Id artefatto** immettere azure documentdb.</span><span class="sxs-lookup"><span data-stu-id="2b580-162">In hello **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="2b580-163">In hello **versione** immettere 1.5.1.</span><span class="sxs-lookup"><span data-stu-id="2b580-163">In hello **Version** box, enter 1.5.1.</span></span>
     
   ![Installare l'SDK dell’applicazione Java di DocumentDB](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="2b580-165">O aggiungere dipendenza hello XML per l'ID del gruppo e Id artefatto direttamente toohello pom.xml tramite un editor di testo:</span><span class="sxs-lookup"><span data-stu-id="2b580-165">Or add hello dependency XML for Group Id and Artifact Id directly toohello pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="2b580-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span><span class="sxs-lookup"><span data-stu-id="2b580-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="2b580-167">Fare clic su **OK** Maven installerà hello SDK per Java DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2b580-167">Click **OK** and Maven will install hello DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="2b580-168">Salvare il file di pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="2b580-168">Save hello pom.xml file.</span></span>

## <span data-ttu-id="2b580-169"><a id="UseService"></a>Passaggio 4: Utilizzo del servizio di Azure Cosmos DB hello in un'applicazione Java</span><span class="sxs-lookup"><span data-stu-id="2b580-169"><a id="UseService"></a>Step 4: Using hello Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="2b580-170">In primo luogo, è pertanto possibile definire l'oggetto TodoItem hello in TodoItem.java:</span><span class="sxs-lookup"><span data-stu-id="2b580-170">First, let's define hello TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="2b580-171">In questo progetto, usiamo [progetto Lombok](http://projectlombok.org/) toogenerate hello costruttore, Get, set e un generatore di.</span><span class="sxs-lookup"><span data-stu-id="2b580-171">In this project, we are using [Project Lombok](http://projectlombok.org/) toogenerate hello constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="2b580-172">In alternativa, è possibile scrivere questo codice manualmente o avere hello IDE generarlo.</span><span class="sxs-lookup"><span data-stu-id="2b580-172">Alternatively, you can write this code manually or have hello IDE generate it.</span></span>
2. <span data-ttu-id="2b580-173">servizio di Azure Cosmos DB tooinvoke hello, deve creare un'istanza di un nuovo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="2b580-173">tooinvoke hello Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="2b580-174">In generale, è migliore hello tooreuse **DocumentClient** : invece di creare un nuovo client per ogni richiesta successiva.</span><span class="sxs-lookup"><span data-stu-id="2b580-174">In general, it is best tooreuse hello **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="2b580-175">È possibile riutilizzare il client hello eseguendo il wrapping di client hello in un **DocumentClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="2b580-175">We can reuse hello client by wrapping hello client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="2b580-176">In DocumentClientFactory.java, è necessario toopaste hello URI e chiave primaria il valore è stato salvato negli Appunti tooyour [passaggio 1](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="2b580-176">In DocumentClientFactory.java, you need toopaste hello URI and PRIMARY KEY value you saved tooyour clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="2b580-177">Sostituire [YOUR\_ENDPOINT\_HERE] con l'URI e sostituire [YOUR\_KEY\_HERE] con la CHIAVE PRIMARIA.</span><span class="sxs-lookup"><span data-stu-id="2b580-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="2b580-178">Ora creiamo tooabstract un oggetto DAO (Data Access) persistenza nostri tooAzure elementi ToDo DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2b580-178">Now let's create a Data Access Object (DAO) tooabstract persisting our ToDo items tooAzure Cosmos DB.</span></span>
   
    <span data-ttu-id="2b580-179">Ordinare elementi ToDo toosave tooa insieme, hello client deve tooknow toopersist quali database e la raccolta troppo (come riferimento self Link).</span><span class="sxs-lookup"><span data-stu-id="2b580-179">In order toosave ToDo items tooa collection, hello client needs tooknow which database and collection toopersist too(as referenced by self-links).</span></span> <span data-ttu-id="2b580-180">In generale, è raccolta quando possibile e database di hello toocache migliore database toohello di tooavoid round trip aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="2b580-180">In general, it is best toocache hello database and collection when possible tooavoid additional round-trips toohello database.</span></span>
   
    <span data-ttu-id="2b580-181">Hello codice seguente viene illustrato come tooretrieve del database e una raccolta, se esistente o crearne uno nuovo se non esiste:</span><span class="sxs-lookup"><span data-stu-id="2b580-181">hello following code illustrates how tooretrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // hello name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // hello name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // hello Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for hello database object, so we don't have tooquery for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for hello collection object, so we don't have tooquery for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get hello database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache hello database object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create hello database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get hello collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache hello collection object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create hello collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="2b580-182">passaggio successivo Hello è toowrite alcuni hello di codice toopersist TodoItems toohello insieme.</span><span class="sxs-lookup"><span data-stu-id="2b580-182">hello next step is toowrite some code toopersist hello TodoItems in toohello collection.</span></span> <span data-ttu-id="2b580-183">In questo esempio, si utilizzerà [Gson](https://code.google.com/p/google-gson/) tooserialize e deserializzare documenti tooJSON TodoItem normale precedente oggetti Java (POJOs).</span><span class="sxs-lookup"><span data-stu-id="2b580-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) tooserialize and de-serialize TodoItem Plain Old Java Objects (POJOs) tooJSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize hello TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate hello document as a TodoItem for retrieval (so that we can
            // store multiple entity types in hello collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist hello document using hello DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="2b580-184">Come nel caso dei database e delle raccolte di Azure Cosmos DB, anche per fare riferimento ai documenti vengono usati collegamenti automatici.</span><span class="sxs-lookup"><span data-stu-id="2b580-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="2b580-185">Hello seguente consente di funzione di supporto IT recuperare documenti da un altro attributo (ad esempio, "id") anziché di collegamento self link:</span><span class="sxs-lookup"><span data-stu-id="2b580-185">hello following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve hello document using hello DocumentClient.
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
6. <span data-ttu-id="2b580-186">È possibile utilizzare il metodo di supporto di hello nel passaggio 5 tooretrieve un documento JSON TodoItem dall'id e quindi deserializzarlo tooa POJO:</span><span class="sxs-lookup"><span data-stu-id="2b580-186">We can use hello helper method in step 5 tooretrieve a TodoItem JSON document by id and then deserialize it tooa POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve hello document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize hello document in tooa TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="2b580-187">È anche possibile usare hello DocumentClient tooget una raccolta o un elenco di TodoItems utilizzando SQL di DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="2b580-187">We can also use hello DocumentClient tooget a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve hello TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize hello documents in tooTodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="2b580-188">Esistono molti modi tooupdate un documento con hello DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="2b580-188">There are many ways tooupdate a document with hello DocumentClient.</span></span> <span data-ttu-id="2b580-189">Nell'applicazione elenco attività, è necessario tootoggle in grado di toobe se un oggetto TodoItem è stato completato.</span><span class="sxs-lookup"><span data-stu-id="2b580-189">In our Todo list application, we want toobe able tootoggle whether a TodoItem is complete.</span></span> <span data-ttu-id="2b580-190">Ciò può essere ottenuto l'aggiornamento dell'attributo "completa" di hello documento hello:</span><span class="sxs-lookup"><span data-stu-id="2b580-190">This can be achieved by updating hello "complete" attribute within hello document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve hello document from hello database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update hello document as a JSON document directly.
            // For more complex operations - you could de-serialize hello document in
            // tooa POJO, update hello POJO, and then re-serialize hello POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace hello updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="2b580-191">Infine, è necessario hello possibilità toodelete a TodoItem dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="2b580-191">Finally, we want hello ability toodelete a TodoItem from our list.</span></span> <span data-ttu-id="2b580-192">toodo, è possibile utilizzare il metodo di supporto hello è scritto in precedenza tooretrieve hello collegamento self link e quindi indicare hello client toodelete è:</span><span class="sxs-lookup"><span data-stu-id="2b580-192">toodo this, we can use hello helper method we wrote earlier tooretrieve hello self-link and then tell hello client toodelete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers toodocuments by self link rather than id.
   
            // Query for hello document tooretrieve hello self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete hello document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <span data-ttu-id="2b580-193"><a id="Wire"></a>Passaggio 5: Cablaggio rest hello di hello del progetto di sviluppo di applicazioni Java insieme</span><span class="sxs-lookup"><span data-stu-id="2b580-193"><a id="Wire"></a>Step 5: Wiring hello rest of hello of Java application development project together</span></span>
<span data-ttu-id="2b580-194">Ora che è stato terminato fun hello bits - resta è toobuild un'interfaccia utente rapida e collegarla tooour DAO.</span><span class="sxs-lookup"><span data-stu-id="2b580-194">Now that we've finished hello fun bits - all that's left is toobuild a quick user interface and wire it up tooour DAO.</span></span>

1. <span data-ttu-id="2b580-195">Innanzitutto, iniziamo con la creazione di un toocall controller il DAO:</span><span class="sxs-lookup"><span data-stu-id="2b580-195">First, let's start with building a controller toocall our DAO:</span></span>
   
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
   
    <span data-ttu-id="2b580-196">In un'applicazione più complessa, controller hello possono contenere la logica di business complessa sopra hello DAO.</span><span class="sxs-lookup"><span data-stu-id="2b580-196">In a more complex application, hello controller may house complicated business logic on top of hello DAO.</span></span>
2. <span data-ttu-id="2b580-197">Successivamente, si creerà un controller di toohello servlet tooroute HTTP richieste:</span><span class="sxs-lookup"><span data-stu-id="2b580-197">Next, we'll create a servlet tooroute HTTP requests toohello controller:</span></span>
   
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
3. <span data-ttu-id="2b580-198">È necessario toohello utente toodisplay interfaccia web utente.</span><span class="sxs-lookup"><span data-stu-id="2b580-198">We'll need a web user interface toodisplay toohello user.</span></span> <span data-ttu-id="2b580-199">Di seguito riscrivere hello index.jsp creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="2b580-199">Let's re-write hello index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding toobody for fixed nav bar */
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
   
            <!-- hello ToDo List -->
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
   
          <!-- Placed at hello end of hello document so hello pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="2b580-200">Infine, scrivere alcuni interfaccia utente lato client JavaScript tootie hello web e hello servlet insieme:</span><span class="sxs-lookup"><span data-stu-id="2b580-200">And finally, write some client-side JavaScript tootie hello web user interface and hello servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods toocall Java backend.
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
   
              // Call api tooupdate todo items.
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
           * Install hello TodoApp
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
5. <span data-ttu-id="2b580-201">A questo punto,</span><span class="sxs-lookup"><span data-stu-id="2b580-201">Awesome!</span></span> <span data-ttu-id="2b580-202">Ora tutto ciò che resta è un'applicazione hello tootest.</span><span class="sxs-lookup"><span data-stu-id="2b580-202">Now all that's left is tootest hello application.</span></span> <span data-ttu-id="2b580-203">Eseguire un'applicazione hello in locale e aggiungere alcuni elementi Todo inserendo il nome di elemento hello e categoria e facendo clic su **Aggiungi attività**.</span><span class="sxs-lookup"><span data-stu-id="2b580-203">Run hello application locally, and add some Todo items by filling in hello item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="2b580-204">Quando viene visualizzato l'elemento hello, è possibile aggiornare se è stata completata l'attivazione e disattivazione di casella di controllo hello e facendo clic su **Aggiorna attività**.</span><span class="sxs-lookup"><span data-stu-id="2b580-204">Once hello item appears, you can update whether it's complete by toggling hello checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="2b580-205"><a id="Deploy"></a>Passaggio 6: Distribuire il tooAzure applicazione Java siti Web</span><span class="sxs-lookup"><span data-stu-id="2b580-205"><a id="Deploy"></a>Step 6: Deploy your Java application tooAzure Web Sites</span></span>
<span data-ttu-id="2b580-206">Con Siti Web di Azure la procedura di distribuzione di applicazioni Java è molto semplice e consiste nell'esportazione di un'applicazione come file con WAR e nel relativo caricamento tramite controllo del codice sorgente (ad esempio Git) o FTP.</span><span class="sxs-lookup"><span data-stu-id="2b580-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="2b580-207">tooexport l'applicazione come file WAR, fare clic sul progetto in **Esplora progetti**, fare clic su **esportare**, quindi fare clic su **File WAR**.</span><span class="sxs-lookup"><span data-stu-id="2b580-207">tooexport your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="2b580-208">In hello **WAR esportare** finestra hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="2b580-208">In hello **WAR Export** window, do hello following:</span></span>
   
   * <span data-ttu-id="2b580-209">Nella casella progetto Web hello immettere esempio java di documentdb azure.</span><span class="sxs-lookup"><span data-stu-id="2b580-209">In hello Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="2b580-210">Nella casella destinazione hello, scegliere un file di destinazione toosave hello WAR.</span><span class="sxs-lookup"><span data-stu-id="2b580-210">In hello Destination box, choose a destination toosave hello WAR file.</span></span>
   * <span data-ttu-id="2b580-211">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="2b580-211">Click **Finish**.</span></span>
3. <span data-ttu-id="2b580-212">Ora che è un file WAR in parte, è possibile semplicemente caricare il tooyour sito Web di Azure **webapps** directory.</span><span class="sxs-lookup"><span data-stu-id="2b580-212">Now that you have a WAR file in hand, you can simply upload it tooyour Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="2b580-213">Per istruzioni sul caricamento di file hello, vedere [aggiungere un tooAzure applicazione Java App del servizio Web App](../app-service-web/web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="2b580-213">For instructions on uploading hello file, see [Add a Java application tooAzure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="2b580-214">Una volta caricato toohello WebApp directory file WAR hello, ambiente di runtime hello rileverà che è stato aggiunto e verrà caricato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2b580-214">Once hello WAR file is uploaded toohello webapps directory, hello runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="2b580-215">tooview il prodotto finito, passare toohttp://YOUR\_sito\_NAME.azurewebsites.net/azure-java-sample/ e iniziare ad aggiungere le attività.</span><span class="sxs-lookup"><span data-stu-id="2b580-215">tooview your finished product, navigate toohttp://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="2b580-216"><a id="GetProject"></a>Ottenere il progetto hello da GitHub</span><span class="sxs-lookup"><span data-stu-id="2b580-216"><a id="GetProject"></a>Get hello project from GitHub</span></span>
<span data-ttu-id="2b580-217">Tutti gli esempi di hello in questa esercitazione sono inclusi in hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) progetto su GitHub.</span><span class="sxs-lookup"><span data-stu-id="2b580-217">All hello samples in this tutorial are included in hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="2b580-218">progetto di attività tooimport hello in Eclipse, assicurarsi di aver software hello e le risorse elencati in hello [prerequisiti](#Prerequisites) sezione, quindi hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="2b580-218">tooimport hello todo project into Eclipse, ensure you have hello software and resources listed in hello [Prerequisites](#Prerequisites) section, then do hello following:</span></span>

1. <span data-ttu-id="2b580-219">Installare [Project Lombok](http://projectlombok.org/).</span><span class="sxs-lookup"><span data-stu-id="2b580-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="2b580-220">Lombok è usato toogenerate costruttori, metodi get, Setter nel progetto hello.</span><span class="sxs-lookup"><span data-stu-id="2b580-220">Lombok is used toogenerate constructors, getters, setters in hello project.</span></span> <span data-ttu-id="2b580-221">Dopo aver scaricato il file di lombok.jar hello, fare doppio clic tooinstall, o installarlo dalla riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="2b580-221">Once you have downloaded hello lombok.jar file, double-click it tooinstall it or install it from hello command line.</span></span>
2. <span data-ttu-id="2b580-222">Se Eclipse è aperto, chiuderlo e riavviarlo tooload Lombok.</span><span class="sxs-lookup"><span data-stu-id="2b580-222">If Eclipse is open, close it and restart it tooload Lombok.</span></span>
3. <span data-ttu-id="2b580-223">In Eclipse, su hello **File** menu, fare clic su **importazione**.</span><span class="sxs-lookup"><span data-stu-id="2b580-223">In Eclipse, on hello **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="2b580-224">In hello **importazione** finestra, fare clic su **Git**, fare clic su **progetti da Git**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2b580-224">In hello **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="2b580-225">In hello **selezionare l'origine del Repository** schermata, fare clic su **Clone URI**.</span><span class="sxs-lookup"><span data-stu-id="2b580-225">On hello **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="2b580-226">In hello **Git Repository di origine** schermo, in hello **URI** casella, immettere https://github.com/Azure-Samples/java-todo-app.git e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2b580-226">On hello **Source Git Repository** screen, in hello **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="2b580-227">In hello **selezione ramo** schermata, assicurarsi che **master** sia selezionata e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2b580-227">On hello **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="2b580-228">In hello **destinazione locale** schermata, fare clic su **Sfoglia** tooselect una cartella in cui possono essere copiati e quindi fare clic su repository hello **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2b580-228">On hello **Local Destination** screen, click **Browse** tooselect a folder where hello repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="2b580-229">In hello **toouse una procedura guidata per l'importazione di progetti selezionare** schermata, assicurarsi che **importare progetti esistenti** sia selezionata e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2b580-229">On hello **Select a wizard toouse for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="2b580-230">In hello **importazione progetti** dello schermo, deseleziona hello **DocumentDB** del progetto e quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="2b580-230">On hello **Import Projects** screen, unselect hello **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="2b580-231">progetto DocumentDB Hello contiene hello Azure Cosmos DB SDK per Java, in cui si aggiungeranno come dipendenza invece.</span><span class="sxs-lookup"><span data-stu-id="2b580-231">hello DocumentDB project contains hello Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="2b580-232">In **Esplora progetti**passare tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java e sostituire i valori HOST e MASTER_KEY hello con hello URI e chiave primaria per l'account di Azure Cosmos DB, quindi Salva il file hello.</span><span class="sxs-lookup"><span data-stu-id="2b580-232">In **Project Explorer**, navigate tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace hello HOST and MASTER_KEY values with hello URI and PRIMARY KEY for your Azure Cosmos DB account, and then save hello file.</span></span> <span data-ttu-id="2b580-233">Per altre informazioni, vedere [Passaggio 1. Creare un account di database Azure Cosmos DB](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="2b580-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="2b580-234">In **Esplora progetti**, fare clic con il pulsante destro hello **esempio java di documentdb azure**, fare clic su **Build Path**, quindi fare clic su **configurare Build Path**.</span><span class="sxs-lookup"><span data-stu-id="2b580-234">In **Project Explorer**, right click hello **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="2b580-235">In hello **Java Build Path** schermata nel riquadro di destra hello, seleziona hello **librerie** scheda e quindi fare clic su **aggiungere file JAR esterna**.</span><span class="sxs-lookup"><span data-stu-id="2b580-235">On hello **Java Build Path** screen, in hello right pane, select hello **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="2b580-236">Passare toohello percorso del file lombok.jar hello e fare clic su **aprire**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b580-236">Navigate toohello location of hello lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="2b580-237">Hello tooopen passaggio 12 di utilizzare **proprietà** nuovamente, finestra e quindi nel riquadro di sinistra hello fare clic su **destinazione runtime**.</span><span class="sxs-lookup"><span data-stu-id="2b580-237">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="2b580-238">In hello **destinazione runtime** schermata, fare clic su **New**selezionare **versione 7.0 Apache Tomcat**e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b580-238">On hello **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="2b580-239">Hello di usare il passaggio 12 tooopen **proprietà** nuovamente, finestra e quindi nel riquadro di sinistra hello fare clic su **facet progetto**.</span><span class="sxs-lookup"><span data-stu-id="2b580-239">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="2b580-240">In hello **progetto facet** selezionare **modulo Web dinamico** e **Java**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b580-240">On hello **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="2b580-241">In hello **server** scheda in basso hello hello destro del mouse su **Tomcat versione 7.0 Server in localhost** e quindi fare clic su **aggiungere e rimuovere**.</span><span class="sxs-lookup"><span data-stu-id="2b580-241">On hello **Servers** tab at hello bottom of hello screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="2b580-242">In hello **aggiungere e rimuovere** finestra spostare **esempio java di documentdb azure** toohello **configurata** casella e quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="2b580-242">On hello **Add and Remove** window, move **azure-documentdb-java-sample** toohello **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="2b580-243">In hello **server** scheda, fare doppio clic su **Tomcat versione 7.0 Server in localhost**, quindi fare clic su **riavviare**.</span><span class="sxs-lookup"><span data-stu-id="2b580-243">In hello **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="2b580-244">In un browser, passare toohttp://localhost:8080 esempio java di documentdb azure / / e iniziare ad aggiungere l'elenco di attività tooyour.</span><span class="sxs-lookup"><span data-stu-id="2b580-244">In a browser, navigate toohttp://localhost:8080/azure-documentdb-java-sample/ and start adding tooyour task list.</span></span> <span data-ttu-id="2b580-245">Si noti che se è stato modificato i valori di porta predefinito, modificare il valore di toohello 8080 selezionato.</span><span class="sxs-lookup"><span data-stu-id="2b580-245">Note that if you changed your default port values, change 8080 toohello value you selected.</span></span>
22. <span data-ttu-id="2b580-246">vedere il sito web di Azure, di tooan progetto toodeploy [passaggio 6. Distribuire i siti Web di tooAzure applicazione](#Deploy).</span><span class="sxs-lookup"><span data-stu-id="2b580-246">toodeploy your project tooan Azure web site, see [Step 6. Deploy your application tooAzure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
