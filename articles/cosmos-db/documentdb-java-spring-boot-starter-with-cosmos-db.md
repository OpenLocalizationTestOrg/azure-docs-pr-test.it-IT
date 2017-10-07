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
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a>Come toouse hello Spring avvio iniziale con l'API di Azure Cosmos DB DocumentDB

## <a name="overview"></a>Panoramica

Hello  **[Spring Framework]**  è una soluzione open source che consente agli sviluppatori Java di creare applicazioni di livello aziendale. Uno dei progetti comuni a più di hello che viene compilato in cui piattaforma è [avvio Spring], che fornisce un approccio semplificato per la creazione di applicazioni Java autonome. gli sviluppatori toohelp iniziare con l'avvio della primavera, sono disponibili in diversi pacchetti di esempio Spring avvio <https://github.com/spring-guides/>. Inoltre toochoosing dall'elenco di hello di avvio di base Spring progetti, hello  **[Spring Initializr]**  consente agli sviluppatori di iniziare a utilizzare la creazione di applicazioni Spring avvio personalizzate.

DB Cosmos Azure è un servizio di database distribuiti a livello globale che consente agli sviluppatori toowork con i dati tramite una vasta gamma di API standard, ad esempio DocumentDB, MongoDB, grafico e tabella API. Microsoft Spring avvio Starter consente sviluppatori toouse Spring avvio le applicazioni che si integrano facilmente con Azure Cosmos DB utilizzando APIs DocumentDB.

In questo articolo viene illustrata la creazione di un database di Azure Cosmos utilizzando hello portale di Azure, quindi l'uso di hello **Spring Initializr** toocreate un'applicazione java personalizzate, quindi aggiungere hello Spring avvio Starter funzionalità tooyour personalizzato applicazione toostore dati e recuperare i dati del database Cosmos Azure utilizzando l'API DocumentDB hello.

## <a name="prerequisites"></a>Prerequisiti

Hello seguenti prerequisiti è necessari nei passaggi di hello ordine toofollow in questo articolo:

* Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].

* [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versione 1.7 o successiva.

* [Apache Maven](http://maven.apache.org/), versione 3.0 o versione successiva.

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a>Creare un database di Azure Cosmos utilizzando hello portale di Azure

1. Sfoglia toohello Azure portale in <https://portal.azure.com/> e fare clic su **+ nuovo**.

   ![Portale di Azure][AZ01]

1. Fare clic su **Database** e quindi su **Azure Cosmos DB**.

   ![Portale di Azure][AZ02]

1. In hello **Azure Cosmos DB** pagina, immettere hello le seguenti informazioni:

   * Immettere un univoco **ID**, che verrà utilizzato come hello URI per il database. ad esempio *wingtiptoysdata.documents.azure.com*.
   * Scegliere **SQL (DB documento)** per hello API.
   * Scegliere hello **sottoscrizione** toouse si desidera per il database.
   * Specificare se toocreate un nuovo **gruppo di risorse** per il database, oppure scegliere un gruppo di risorse esistente.
   * Specificare hello **percorso** per il database.
   
   Dopo aver specificato queste opzioni, fare clic su **crea** toocreate del database.

   ![Portale di Azure][AZ03]

1. Quando il database è stato creato, viene elencato nella finestra di Azure **Dashboard**, nonché nel hello **tutte le risorse** e **Azure Cosmos DB** pagine. È possibile fare clic sul database in qualsiasi tali percorsi tooopen hello pagina delle proprietà per la cache.

   ![Portale di Azure][AZ04]

1. Quando viene visualizzata la pagina proprietà hello per il database, fare clic su **le chiavi di accesso** e copiare le chiavi di accesso e l'URI per il database, si userà questi valori all'interno dell'applicazione di avvio molla.

   ![Portale di Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a>Creare una semplice applicazione di avvio Spring con hello Spring Initializr

1. Sfoglia troppo<https://start.spring.io/>.

1. Specifica che si desidera toogenerate un **Maven** il progetto con **Java**, immettere hello **gruppo** e **artefatto** nomi per l'applicazione, e quindi fare clic su pulsante hello troppo**generare progetto**.

   ![Opzioni di base di Spring Initializr][SI01]

   > [!NOTE]
   >
   > Hello Spring Initializr utilizza hello **gruppo** e **artefatto** nome del pacchetto hello toocreate nomi, ad esempio: *com.example.wintiptoys*.
   >

1. Quando richiesto, scaricare percorso tooa del progetto hello nel computer locale.

   ![Scaricare il progetto Spring Boot personalizzato][SI02]

1. Dopo che sono stati estratti i file hello nel sistema locale, è possibile che l'applicazione di avvio Spring semplice sarà pronta per la modifica.

   ![File del progetto Spring Boot personalizzato][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a>Configurare il hello toouse di avvio Spring app Azure Spring avvio Starter

1. Individuare hello *pom.xml* file nella directory hello dell'app; ad esempio:

   `C:\SpringBoot\wingtiptoys\pom.xml`

   -oppure-

   `/users/example/home/wingtiptoys/pom.xml`

   ![Individuare il file pom.xml hello][PM01]

1. Aprire hello *pom.xml* file in un editor di testo e aggiungere hello seguente toolist righe di `<dependencies>`:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Modifica file pom.xml hello][PM02]

1. Salvare e chiudere hello *pom.xml* file.

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a>Configurare il toouse app Spring avvio del database di Azure Cosmos

1. Individuare hello *application.properties* file hello *risorse* directory dell'app, ad esempio:

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   -oppure-

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Individuare il file application.properties hello][RE01]

1. Aprire hello *application.properties* file in un editor di testo e aggiungere i seguenti file toohello righe hello e sostituire i valori di esempio hello con le proprietà appropriate hello per il database:

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Modifica file application.properties hello][RE02]

1. Salvare e chiudere hello *application.properties* file.

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a>Aggiungere la funzionalità database basic tooimplement codice di esempio

In questa sezione creare due classi Java per l'archiviazione dei dati utente e quindi modificare la toocreate classe principale dell'applicazione un'istanza della classe utente hello e salvarlo tooyour database.

### <a name="define-a-basic-class-for-storing-user-data"></a>Definire una classe di base per l'archiviazione dei dati utente

1. Creare un nuovo file denominato *User.java* in hello stessa directory del file principale dell'applicazione Java.

1. Aprire hello *User.java* file in un editor di testo e aggiungere i seguenti hello righe toohello file toodefine una classe generica che consente di archiviare e recuperare i valori del database:

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

1. Salvare e chiudere hello *User.java* file.

### <a name="define-a-data-repository-interface"></a>Definire un'interfaccia del repository di dati

1. Creare un nuovo file denominato *UserRepository.java* in hello stessa directory del file principale dell'applicazione Java.

1. Aprire hello *UserRepository.java* file in un editor di testo e aggiungere i seguenti hello righe toohello file toodefine un'interfaccia del repository di utente che estende l'interfaccia del repository di hello predefinita DocumentDB:

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. Salvare e chiudere hello *UserRepository.java* file.

### <a name="modify-hello-main-application-class"></a>Modificare classe principale dell'applicazione hello

1. Individuare i file Java di hello principale dell'applicazione nella directory del pacchetto dell'app; hello Per esempio:

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   -oppure-

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Individuare il file di hello applicazione Java][JV01]

1. Aprire i file Java di hello principale dell'applicazione in un editor di testo e aggiungere i seguenti file toohello righe hello:

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

1. Salvare e chiudere i file Java di hello principale dell'applicazione.

## <a name="build-and-test-your-app"></a>Compilare e testare l'app

1. Aprire un prompt dei comandi e cambiare directory toohello cartella in cui il *pom.xml* file si trova, ad esempio:

   `cd C:\SpringBoot\wingtiptoys`

   -oppure-

   `cd /users/example/home/wingtiptoys`

1. Compilare l'applicazione Spring Boot con Maven ed eseguirla, ad esempio:

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. L'applicazione verrà visualizzati diversi messaggi di runtime e verrà visualizzato il messaggio hello `User: testFirstName testLastName` visualizzato tooindicate che valori correttamente archiviati e recuperati dal database.

   ![Output ha esito positivo di un'applicazione hello][JV02]

1. Facoltativo: È possibile utilizzare l'hello tooview portale Azure hello contenuto del database Cosmos Azure dalla pagina delle proprietà hello di per il database, fare clic su **Document Explorer**e quindi selezionando e hello tooview di elenco hello visualizzato elemento contenuto.

   ![Usando i dati di hello Document Explorer tooview][JV03]

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sull'utilizzo di Azure Cosmos DB e Java, vedere hello seguenti articoli:

* [Documentazione di Azure Cosmos DB].

* [DB Cosmos Azure: Creare un'applicazione API DocumentDB con Java e hello portale di Azure][Build a DocumentDB API app with Java]

Per ulteriori informazioni sull'utilizzo di applicazioni di avvio Spring in Azure, vedere hello seguenti articoli:

* [Spring Boot DocumenDB Starter for Azure](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [Distribuire un servizio App di Azure di toohello Spring avvio applicazione](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Esegue un'applicazione di avvio molla su un Kubernetes Cluster in hello servizio contenitore di Azure](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure] hello e [Java Tools per Visual Studio Team Services].

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
