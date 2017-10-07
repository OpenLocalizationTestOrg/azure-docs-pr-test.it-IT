---
title: aaaHow toouse hello Spring avvio iniziale con un'API di Azure Cosmos DB DocumentDB
description: Informazioni su come tooconfigure creare un'applicazione con hello Spring avvio inizializzatore con hello Azure Cosmos DB DocumentDB API.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: Spring, Spring Boot Starter, Cosmos DB
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/08/2017
ms.author: robmcm;yungez;kevinzha
ms.openlocfilehash: a2c6de678f850676cb2887e224e5c12950db0e53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="35ef4-104">Come toouse hello Spring avvio iniziale con l'API di Azure Cosmos DB DocumentDB</span><span class="sxs-lookup"><span data-stu-id="35ef4-104">How toouse hello Spring Boot Starter with Azure Cosmos DB DocumentDB API</span></span>

## <a name="overview"></a><span data-ttu-id="35ef4-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="35ef4-105">Overview</span></span>

<span data-ttu-id="35ef4-106">Hello  **[Spring Framework]**  è una soluzione open source che consente agli sviluppatori Java di creare applicazioni di livello aziendale.</span><span class="sxs-lookup"><span data-stu-id="35ef4-106">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="35ef4-107">Uno dei progetti comuni a più di hello che viene compilato in cui piattaforma è [avvio Spring], che fornisce un approccio semplificato per la creazione di applicazioni Java autonome.</span><span class="sxs-lookup"><span data-stu-id="35ef4-107">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="35ef4-108">gli sviluppatori toohelp iniziare con l'avvio della primavera, sono disponibili in diversi pacchetti di esempio Spring avvio <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="35ef4-108">toohelp developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="35ef4-109">Inoltre toochoosing dall'elenco di hello di avvio di base Spring progetti, hello  **[Spring Initializr]**  consente agli sviluppatori di iniziare a utilizzare la creazione di applicazioni Spring avvio personalizzate.</span><span class="sxs-lookup"><span data-stu-id="35ef4-109">In addition toochoosing from hello list of basic Spring Boot projects, hello **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="35ef4-110">DB Cosmos Azure è un servizio di database distribuiti a livello globale che consente agli sviluppatori toowork con i dati tramite una vasta gamma di API standard, ad esempio DocumentDB, MongoDB, grafico e tabella API.</span><span class="sxs-lookup"><span data-stu-id="35ef4-110">Azure Cosmos DB is a globally-distributed database service that allows developers toowork with data using a variety of standard APIs, such as DocumentDB, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="35ef4-111">Microsoft Spring avvio Starter consente sviluppatori toouse Spring avvio le applicazioni che si integrano facilmente con Azure Cosmos DB utilizzando APIs DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="35ef4-111">Microsoft's Spring Boot Starter enables developers toouse Spring Boot applications that easily integrate with Azure Cosmos DB by using DocumentDB APIs.</span></span>

<span data-ttu-id="35ef4-112">In questo articolo viene illustrata la creazione di un database di Azure Cosmos utilizzando hello portale di Azure, quindi l'uso di hello **Spring Initializr** toocreate un'applicazione java personalizzate, quindi aggiungere hello Spring avvio Starter funzionalità tooyour personalizzato applicazione toostore dati e recuperare i dati del database Cosmos Azure utilizzando l'API DocumentDB hello.</span><span class="sxs-lookup"><span data-stu-id="35ef4-112">This article demonstrates creating an Azure Cosmos DB using hello Azure portal, then using hello **Spring Initializr** toocreate a custom java application, and then add hello Spring Boot Starter functionality tooyour custom application toostore data in and retrieve data from your Azure Cosmos DB by using hello DocumentDB API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35ef4-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="35ef4-113">Prerequisites</span></span>

<span data-ttu-id="35ef4-114">Hello seguenti prerequisiti è necessari nei passaggi di hello ordine toofollow in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="35ef4-114">hello following prerequisites are required in order toofollow hello steps in this article:</span></span>

* <span data-ttu-id="35ef4-115">Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].</span><span class="sxs-lookup"><span data-stu-id="35ef4-115">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="35ef4-116">[Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versione 1.7 o successiva.</span><span class="sxs-lookup"><span data-stu-id="35ef4-116">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="35ef4-117">[Apache Maven](http://maven.apache.org/), versione 3.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="35ef4-117">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a><span data-ttu-id="35ef4-118">Creare un database di Azure Cosmos utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="35ef4-118">Create an Azure Cosmos DB by using hello Azure portal</span></span>

1. <span data-ttu-id="35ef4-119">Sfoglia toohello Azure portale in <https://portal.azure.com/> e fare clic su **+ nuovo**.</span><span class="sxs-lookup"><span data-stu-id="35ef4-119">Browse toohello Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Portale di Azure][AZ01]

1. <span data-ttu-id="35ef4-121">Fare clic su **Database** e quindi su **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="35ef4-121">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Portale di Azure][AZ02]

1. <span data-ttu-id="35ef4-123">In hello **Azure Cosmos DB** pagina, immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="35ef4-123">On hello **Azure Cosmos DB** page, enter hello following information:</span></span>

   * <span data-ttu-id="35ef4-124">Immettere un univoco **ID**, che verrà utilizzato come hello URI per il database.</span><span class="sxs-lookup"><span data-stu-id="35ef4-124">Enter a unique **ID**, which you will use as hello URI for your database.</span></span> <span data-ttu-id="35ef4-125">ad esempio *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="35ef4-125">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="35ef4-126">Scegliere **SQL (DB documento)** per hello API.</span><span class="sxs-lookup"><span data-stu-id="35ef4-126">Choose **SQL (Document DB)** for hello API.</span></span>
   * <span data-ttu-id="35ef4-127">Scegliere hello **sottoscrizione** toouse si desidera per il database.</span><span class="sxs-lookup"><span data-stu-id="35ef4-127">Choose hello **Subscription** you want toouse for your database.</span></span>
   * <span data-ttu-id="35ef4-128">Specificare se toocreate un nuovo **gruppo di risorse** per il database, oppure scegliere un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="35ef4-128">Specify whether toocreate a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="35ef4-129">Specificare hello **percorso** per il database.</span><span class="sxs-lookup"><span data-stu-id="35ef4-129">Specify hello **Location** for your database.</span></span>
   
   <span data-ttu-id="35ef4-130">Dopo aver specificato queste opzioni, fare clic su **crea** toocreate del database.</span><span class="sxs-lookup"><span data-stu-id="35ef4-130">When you have specified these options, click **Create** toocreate your database.</span></span>

   ![Portale di Azure][AZ03]

1. <span data-ttu-id="35ef4-132">Quando il database è stato creato, viene elencato nella finestra di Azure **Dashboard**, nonché nel hello **tutte le risorse** e **Azure Cosmos DB** pagine.</span><span class="sxs-lookup"><span data-stu-id="35ef4-132">When your database has been created, it is listed on your Azure **Dashboard**, as well as under hello **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="35ef4-133">È possibile fare clic sul database in qualsiasi tali percorsi tooopen hello pagina delle proprietà per la cache.</span><span class="sxs-lookup"><span data-stu-id="35ef4-133">You can click on your database on any of those locations tooopen hello properties page for your cache.</span></span>

   ![Portale di Azure][AZ04]

1. <span data-ttu-id="35ef4-135">Quando viene visualizzata la pagina proprietà hello per il database, fare clic su **le chiavi di accesso** e copiare le chiavi di accesso e l'URI per il database, si userà questi valori all'interno dell'applicazione di avvio molla.</span><span class="sxs-lookup"><span data-stu-id="35ef4-135">When hello properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Portale di Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a><span data-ttu-id="35ef4-137">Creare una semplice applicazione di avvio Spring con hello Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="35ef4-137">Create a simple Spring Boot application with hello Spring Initializr</span></span>

1. <span data-ttu-id="35ef4-138">Sfoglia troppo<https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="35ef4-138">Browse too<https://start.spring.io/>.</span></span>

1. <span data-ttu-id="35ef4-139">Specifica che si desidera toogenerate un **Maven** il progetto con **Java**, immettere hello **gruppo** e **artefatto** nomi per l'applicazione, e quindi fare clic su pulsante hello troppo**generare progetto**.</span><span class="sxs-lookup"><span data-stu-id="35ef4-139">Specify that you want toogenerate a **Maven** project with **Java**, enter hello **Group** and **Artifact** names for your application, and then click hello button too**Generate Project**.</span></span>

   ![Opzioni di base di Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="35ef4-141">Hello Spring Initializr utilizza hello **gruppo** e **artefatto** nome del pacchetto hello toocreate nomi, ad esempio: *com.example.wintiptoys*.</span><span class="sxs-lookup"><span data-stu-id="35ef4-141">hello Spring Initializr uses hello **Group** and **Artifact** names toocreate hello package name; for example: *com.example.wintiptoys*.</span></span>
   >

1. <span data-ttu-id="35ef4-142">Quando richiesto, scaricare percorso tooa del progetto hello nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="35ef4-142">When prompted, download hello project tooa path on your local computer.</span></span>

   ![Scaricare il progetto Spring Boot personalizzato][SI02]

1. <span data-ttu-id="35ef4-144">Dopo che sono stati estratti i file hello nel sistema locale, è possibile che l'applicazione di avvio Spring semplice sarà pronta per la modifica.</span><span class="sxs-lookup"><span data-stu-id="35ef4-144">After you have extracted hello files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![File del progetto Spring Boot personalizzato][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a><span data-ttu-id="35ef4-146">Configurare il hello toouse di avvio Spring app Azure Spring avvio Starter</span><span class="sxs-lookup"><span data-stu-id="35ef4-146">Configure your Spring Boot app toouse hello Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="35ef4-147">Individuare hello *pom.xml* file nella directory hello dell'app; ad esempio:</span><span class="sxs-lookup"><span data-stu-id="35ef4-147">Locate hello *pom.xml* file in hello directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\pom.xml`

   <span data-ttu-id="35ef4-148">-oppure-</span><span class="sxs-lookup"><span data-stu-id="35ef4-148">-or-</span></span>

   `/users/example/home/wingtiptoys/pom.xml`

   ![Individuare il file pom.xml hello][PM01]

1. <span data-ttu-id="35ef4-150">Aprire hello *pom.xml* file in un editor di testo e aggiungere hello seguente toolist righe di `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="35ef4-150">Open hello *pom.xml* file in a text editor, and add hello following lines toolist of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Modifica file pom.xml hello][PM02]

1. <span data-ttu-id="35ef4-152">Salvare e chiudere hello *pom.xml* file.</span><span class="sxs-lookup"><span data-stu-id="35ef4-152">Save and close hello *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a><span data-ttu-id="35ef4-153">Configurare il toouse app Spring avvio del database di Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="35ef4-153">Configure your Spring Boot app toouse your Azure Cosmos DB</span></span>

1. <span data-ttu-id="35ef4-154">Individuare hello *application.properties* file hello *risorse* directory dell'app, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="35ef4-154">Locate hello *application.properties* file in hello *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   <span data-ttu-id="35ef4-155">-oppure-</span><span class="sxs-lookup"><span data-stu-id="35ef4-155">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Individuare il file application.properties hello][RE01]

1. <span data-ttu-id="35ef4-157">Aprire hello *application.properties* file in un editor di testo e aggiungere i seguenti file toohello righe hello e sostituire i valori di esempio hello con le proprietà appropriate hello per il database:</span><span class="sxs-lookup"><span data-stu-id="35ef4-157">Open hello *application.properties* file in a text editor, and add hello following lines toohello file, and replace hello sample values with hello appropriate properties for your database:</span></span>

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Modifica file application.properties hello][RE02]

1. <span data-ttu-id="35ef4-159">Salvare e chiudere hello *application.properties* file.</span><span class="sxs-lookup"><span data-stu-id="35ef4-159">Save and close hello *application.properties* file.</span></span>

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a><span data-ttu-id="35ef4-160">Aggiungere la funzionalità database basic tooimplement codice di esempio</span><span class="sxs-lookup"><span data-stu-id="35ef4-160">Add sample code tooimplement basic database functionality</span></span>

<span data-ttu-id="35ef4-161">In questa sezione creare due classi Java per l'archiviazione dei dati utente e quindi modificare la toocreate classe principale dell'applicazione un'istanza della classe utente hello e salvarlo tooyour database.</span><span class="sxs-lookup"><span data-stu-id="35ef4-161">In this section you create two Java classes for storing user data, and then you modify your main application class toocreate an instance of hello user class and save it tooyour database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="35ef4-162">Definire una classe di base per l'archiviazione dei dati utente</span><span class="sxs-lookup"><span data-stu-id="35ef4-162">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="35ef4-163">Creare un nuovo file denominato *User.java* in hello stessa directory del file principale dell'applicazione Java.</span><span class="sxs-lookup"><span data-stu-id="35ef4-163">Create a new file named *User.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="35ef4-164">Aprire hello *User.java* file in un editor di testo e aggiungere i seguenti hello righe toohello file toodefine una classe generica che consente di archiviare e recuperare i valori del database:</span><span class="sxs-lookup"><span data-stu-id="35ef4-164">Open hello *User.java* file in a text editor, and add hello following lines toohello file toodefine a generic user class that stores and retrieve values in your database:</span></span>

   ```java
   package com.example.wingtiptoys;

   public class User {
      private String id;
      private String firstName;
      private String lastName;
 
      public User(String id, String firstName, String lastName) {
         this.id = id;
         this.firstName = firstName;
         this.lastName = lastName;
      }
   
      public String getId() {
         return this.id;
      }

      public void setId(String id) {
         this.id = id;
      }

      public String getFirstName() {
         return firstName;
      }

      public void setFirstName(String firstName) {
         this.firstName = firstName;
      }

      public String getLastName() {
         return lastName;
      }

      public void setLastName(String lastName) {
         this.lastName = lastName;
      }

      @Override
      public String toString() {
         return String.format("User: %s %s", firstName, lastName);
      }
   }
   ```

1. <span data-ttu-id="35ef4-165">Salvare e chiudere hello *User.java* file.</span><span class="sxs-lookup"><span data-stu-id="35ef4-165">Save and close hello *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="35ef4-166">Definire un'interfaccia del repository di dati</span><span class="sxs-lookup"><span data-stu-id="35ef4-166">Define a data repository interface</span></span>

1. <span data-ttu-id="35ef4-167">Creare un nuovo file denominato *UserRepository.java* in hello stessa directory del file principale dell'applicazione Java.</span><span class="sxs-lookup"><span data-stu-id="35ef4-167">Create a new file named *UserRepository.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="35ef4-168">Aprire hello *UserRepository.java* file in un editor di testo e aggiungere i seguenti hello righe toohello file toodefine un'interfaccia del repository di utente che estende l'interfaccia del repository di hello predefinita DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="35ef4-168">Open hello *UserRepository.java* file in a text editor, and add hello following lines toohello file toodefine a user repository interface that extends hello default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. <span data-ttu-id="35ef4-169">Salvare e chiudere hello *UserRepository.java* file.</span><span class="sxs-lookup"><span data-stu-id="35ef4-169">Save and close hello *UserRepository.java* file.</span></span>

### <a name="modify-hello-main-application-class"></a><span data-ttu-id="35ef4-170">Modificare classe principale dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="35ef4-170">Modify hello main application class</span></span>

1. <span data-ttu-id="35ef4-171">Individuare i file Java di hello principale dell'applicazione nella directory del pacchetto dell'app; hello Per esempio:</span><span class="sxs-lookup"><span data-stu-id="35ef4-171">Locate hello main application Java file in hello package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   <span data-ttu-id="35ef4-172">-oppure-</span><span class="sxs-lookup"><span data-stu-id="35ef4-172">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Individuare il file di hello applicazione Java][JV01]

1. <span data-ttu-id="35ef4-174">Aprire i file Java di hello principale dell'applicazione in un editor di testo e aggiungere i seguenti file toohello righe hello:</span><span class="sxs-lookup"><span data-stu-id="35ef4-174">Open hello main application Java file in a text editor, and add hello following lines toohello file:</span></span>

   ```java
   package com.example.wingtiptoys;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class WingtiptoysApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;
    
      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysApplication.class, args);
      }

      public void run(String... var1) throws Exception {
         final User testUser = new User("testId", "testFirstName", "testLastName");

         repository.deleteAll();
         repository.save(testUser);

         final User result = repository.findOne(testUser.getId());

         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

1. <span data-ttu-id="35ef4-175">Salvare e chiudere i file Java di hello principale dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="35ef4-175">Save and close hello main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="35ef4-176">Compilare e testare l'app</span><span class="sxs-lookup"><span data-stu-id="35ef4-176">Build and test your app</span></span>

1. <span data-ttu-id="35ef4-177">Aprire un prompt dei comandi e cambiare directory toohello cartella in cui il *pom.xml* file si trova, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="35ef4-177">Open a command prompt and change directory toohello folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoys`

   <span data-ttu-id="35ef4-178">-oppure-</span><span class="sxs-lookup"><span data-stu-id="35ef4-178">-or-</span></span>

   `cd /users/example/home/wingtiptoys`

1. <span data-ttu-id="35ef4-179">Compilare l'applicazione Spring Boot con Maven ed eseguirla, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="35ef4-179">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. <span data-ttu-id="35ef4-180">L'applicazione verrà visualizzati diversi messaggi di runtime e verrà visualizzato il messaggio hello `User: testFirstName testLastName` visualizzato tooindicate che valori correttamente archiviati e recuperati dal database.</span><span class="sxs-lookup"><span data-stu-id="35ef4-180">Your application will display several runtime messages, and you should see hello message `User: testFirstName testLastName` displayed tooindicate that values have been successfully stored and retrieved from your database.</span></span>

   ![Output ha esito positivo di un'applicazione hello][JV02]

1. <span data-ttu-id="35ef4-182">Facoltativo: È possibile utilizzare l'hello tooview portale Azure hello contenuto del database Cosmos Azure dalla pagina delle proprietà hello di per il database, fare clic su **Document Explorer**e quindi selezionando e hello tooview di elenco hello visualizzato elemento contenuto.</span><span class="sxs-lookup"><span data-stu-id="35ef4-182">OPTIONAL: You can use hello Azure portal tooview hello contents of your Azure Cosmos DB from hello properties page for your database by clicking  **Document Explorer**, and then selecting and item from hello displayed list tooview hello contents.</span></span>

   ![Usando i dati di hello Document Explorer tooview][JV03]

## <a name="next-steps"></a><span data-ttu-id="35ef4-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="35ef4-184">Next steps</span></span>

<span data-ttu-id="35ef4-185">Per ulteriori informazioni sull'utilizzo di Azure Cosmos DB e Java, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="35ef4-185">For more information about using Azure Cosmos DB and Java, see hello following articles:</span></span>

* <span data-ttu-id="35ef4-186">[Documentazione di Azure Cosmos DB].</span><span class="sxs-lookup"><span data-stu-id="35ef4-186">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="35ef4-187">[DB Cosmos Azure: Creare un'applicazione API DocumentDB con Java e hello portale di Azure][Build a DocumentDB API app with Java]</span><span class="sxs-lookup"><span data-stu-id="35ef4-187">[Azure Cosmos DB: Build a DocumentDB API app with Java and hello Azure portal][Build a DocumentDB API app with Java]</span></span>

<span data-ttu-id="35ef4-188">Per ulteriori informazioni sull'utilizzo di applicazioni di avvio Spring in Azure, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="35ef4-188">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="35ef4-189">Spring Boot DocumenDB Starter for Azure</span><span class="sxs-lookup"><span data-stu-id="35ef4-189">Spring Boot DocumenDB Starter for Azure</span></span>](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [<span data-ttu-id="35ef4-190">Distribuire un servizio App di Azure di toohello Spring avvio applicazione</span><span class="sxs-lookup"><span data-stu-id="35ef4-190">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="35ef4-191">Esegue un'applicazione di avvio molla su un Kubernetes Cluster in hello servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="35ef4-191">Running a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="35ef4-192">Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure] hello e [Java Tools per Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="35ef4-192">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Documentazione di Azure Cosmos DB]: /azure/cosmos-db/
[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[Build a DocumentDB API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-documentdb-java
[account Azure gratuito]: https://azure.microsoft.com/pricing/free-trial/
[Java Tools per Visual Studio Team Services]: https://java.visualstudio.com/
[vantaggi per i sottoscrittori di MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[avvio Spring]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ01.png
[AZ02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ02.png
[AZ03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ03.png
[AZ04]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ04.png
[AZ05]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ05.png

[SI01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI01.png
[SI02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI02.png
[SI03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI03.png

[RE01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE01.png
[RE02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE02.png

[PM01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM01.png
[PM02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM02.png

[JV01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV01.png
[JV02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV02.png
[JV03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV03.png
