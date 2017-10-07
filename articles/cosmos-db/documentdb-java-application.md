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
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a>Compilare un'applicazione web Java utilizzando Azure Cosmos DB e hello API DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.JS](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

In questa esercitazione di applicazione web Java illustra come hello toouse [DB di Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) servizio toostore e accedere ai dati da un'applicazione Java ospitato in App Web di servizio App di Azure. In questo argomento, si apprenderà:

* Come toobuild un'applicazione Java Server Pages (JSP) di base in Eclipse.
* La modalità del servizio utilizzando hello toowork con hello Azure Cosmos DB [Azure SDK per Java DB Cosmos](https://github.com/Azure/azure-documentdb-java).

In questa esercitazione applicazione Java Mostra come applicazione di gestione delle attività toocreate basata sul web che consente di contrassegno, recuperare e si toocreate attività come completata, come illustrato nella seguente immagine hello. Ognuna delle attività hello nell'elenco attività hello vengono archiviate come documenti JSON in Azure Cosmos DB.

![Applicazione Java My ToDo List](./media/documentdb-java-application/image1.png)

> [!TIP]
> Questa esercitazione sullo sviluppo dell’applicazione presuppone che l'utente abbia già acquisito familiarità con l'uso di Java. Se si tooJava nuova o hello [strumenti prerequisiti](#Prerequisites), si consiglia di scaricare hello completo [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) progetto da GitHub e compilazione mediante [hello istruzioni alla fine di hello di questo articolo](#GetProject). Quando l'applicazione viene compilata, è possibile esaminare informazioni dettagliate di hello articolo toogain codice hello nel contesto di hello del progetto hello.  
> 
> 

## <a id="Prerequisites"></a>Prerequisiti per questa esercitazione sull'applicazione Web Java
Prima di iniziare questa esercitazione sullo sviluppo di applicazioni, è necessario disporre delle seguenti hello:

* Un account Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).

    OPPURE

    Un'installazione locale di hello [emulatore di Azure Cosmos DB](local-emulator.md).
* [Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
* [Eclipse IDE per sviluppatori Java EE.](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [Un sito Web di Azure con Java Runtime Environment (ad esempio Tomcat o Jetty) abilitato.](../app-service-web/web-sites-java-get-started.md)

Se si desidera installare questi strumenti per hello prima volta, coreservlets.com fornisce una panoramica del processo di installazione hello nella sezione introduttiva di hello del loro [esercitazione: installazione TomCat7 e utilizzarlo con Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) articolo.

## <a id="CreateDB"></a>Passaggio 1: Creare un account di Azure Cosmos DB
Creare prima di tutto un account Azure Cosmos DB. Se è già un account o se si utilizza hello Azure Cosmos DB emulatore per questa esercitazione, è possibile ignorare troppo[passaggio 2: creare un'applicazione JSP Java hello](#CreateJSP).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <a id="CreateJSP"></a>Passaggio 2: Creare un'applicazione JSP Java hello
hello toocreate applicazione JSP di:

1. Iniziare innanzitutto con la creazione di un progetto Java. Avviare Eclipse, quindi fare clic su **File**, **New** (Nuovo) e quindi su **Dynamic Web Project** (Progetto Web dinamico). Se non viene visualizzato **progetto Web dinamico** elencato come un progetto disponibile, hello seguente: fare clic su **File**, fare clic su **New**, fare clic su **progetto**..., espandere **Web**, fare clic su **progetto Web dinamico**, fare clic su **Avanti**.
   
    ![Sviluppo di applicazioni Java JSP](./media/documentdb-java-application/image10.png)
2. Immettere un nome di progetto in hello **nome progetto** casella e in hello **destinazione Runtime** menu a discesa, selezionare facoltativamente un valore (ad esempio Apache Tomcat versione 7.0) e quindi fare clic su **fine**. Consente la selezione di un runtime di destinazione è toorun progetto localmente mediante Eclipse.
3. Nella visualizzazione Project Explorer di hello in Eclipse, espandere il progetto. Fare clic con il pulsante destro del mouse su **WebContent**, scegliere **New** e quindi fare clic su **JSP File**.
4. In hello **New JSP File** della finestra di dialogo file hello nome **index.jsp**. Mantenere come cartella padre di hello **WebContent**, come illustrato nell'hello nella figura riportata di seguito e quindi fare clic su **Avanti**.
   
    ![Esercitazione sull’applicazione web Java - Creare un nuovo File JSP](./media/documentdb-java-application/image11.png)
5. In hello **Select JSP Template** la finestra di dialogo, a scopo di hello di questa esercitazione, selezionare **New JSP File (html)**, quindi fare clic su **fine**.
6. All'apertura di file di hello index.jsp in Eclipse, aggiungere testo toodisplay **Hello World!** all'interno di hello esistente <body> elemento. L'aggiornamento <body> contenuto dovrebbe essere simile hello seguente codice:
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. Salvare file index.jsp hello.
8. Se si imposta un runtime di destinazione nel passaggio 2, è possibile fare clic su **progetto** e quindi **eseguire** toorun dell'applicazione JSP in locale:
   
    ![Esercitazione sull’applicazione Java - Hello World](./media/documentdb-java-application/image12.png)

## <a id="InstallSDK"></a>Passaggio 3: Installare hello DocumentDB SDK per Java
Hello toopull modo più semplice in hello DocumentDB SDK per Java e le relative dipendenze è tramite [Apache Maven](http://maven.apache.org/).

toodo, è necessario tooconvert il progetto di maven tooa completando hello alla procedura seguente:

1. Pulsante destro del mouse sul progetto in Project Explorer di hello, fare clic su **configura**, fare clic su **convertire tooMaven progetto**.
2. In hello **creare nuovo POM** , accettare le impostazioni predefinite hello e fare clic su **fine**.
3. In **Esplora progetti**, aprire il file di pom.xml hello.
4. In hello **dipendenze** scheda hello **dipendenze** riquadro, fare clic su **Aggiungi**.
5. In hello **selezionare dipendenza** finestra hello seguenti:
   
   * In hello **Id gruppo** immettere com.microsoft.azure.
   * In hello **Id artefatto** immettere azure documentdb.
   * In hello **versione** immettere 1.5.1.
     
   ![Installare l'SDK dell’applicazione Java di DocumentDB](./media/documentdb-java-application/image13.png)
     
   * O aggiungere dipendenza hello XML per l'ID del gruppo e Id artefatto direttamente toohello pom.xml tramite un editor di testo:
     
        <dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency>
6. Fare clic su **OK** Maven installerà hello SDK per Java DocumentDB.
7. Salvare il file di pom.xml hello.

## <a id="UseService"></a>Passaggio 4: Utilizzo del servizio di Azure Cosmos DB hello in un'applicazione Java
1. In primo luogo, è pertanto possibile definire l'oggetto TodoItem hello in TodoItem.java:
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    In questo progetto, usiamo [progetto Lombok](http://projectlombok.org/) toogenerate hello costruttore, Get, set e un generatore di. In alternativa, è possibile scrivere questo codice manualmente o avere hello IDE generarlo.
2. servizio di Azure Cosmos DB tooinvoke hello, deve creare un'istanza di un nuovo **DocumentClient**. In generale, è migliore hello tooreuse **DocumentClient** : invece di creare un nuovo client per ogni richiesta successiva. È possibile riutilizzare il client hello eseguendo il wrapping di client hello in un **DocumentClientFactory**. In DocumentClientFactory.java, è necessario toopaste hello URI e chiave primaria il valore è stato salvato negli Appunti tooyour [passaggio 1](#CreateDB). Sostituire [YOUR\_ENDPOINT\_HERE] con l'URI e sostituire [YOUR\_KEY\_HERE] con la CHIAVE PRIMARIA.
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. Ora creiamo tooabstract un oggetto DAO (Data Access) persistenza nostri tooAzure elementi ToDo DB Cosmos.
   
    Ordinare elementi ToDo toosave tooa insieme, hello client deve tooknow toopersist quali database e la raccolta troppo (come riferimento self Link). In generale, è raccolta quando possibile e database di hello toocache migliore database toohello di tooavoid round trip aggiuntivi.
   
    Hello codice seguente viene illustrato come tooretrieve del database e una raccolta, se esistente o crearne uno nuovo se non esiste:
   
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
4. passaggio successivo Hello è toowrite alcuni hello di codice toopersist TodoItems toohello insieme. In questo esempio, si utilizzerà [Gson](https://code.google.com/p/google-gson/) tooserialize e deserializzare documenti tooJSON TodoItem normale precedente oggetti Java (POJOs).
   
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
5. Come nel caso dei database e delle raccolte di Azure Cosmos DB, anche per fare riferimento ai documenti vengono usati collegamenti automatici. Hello seguente consente di funzione di supporto IT recuperare documenti da un altro attributo (ad esempio, "id") anziché di collegamento self link:
   
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
6. È possibile utilizzare il metodo di supporto di hello nel passaggio 5 tooretrieve un documento JSON TodoItem dall'id e quindi deserializzarlo tooa POJO:
   
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
7. È anche possibile usare hello DocumentClient tooget una raccolta o un elenco di TodoItems utilizzando SQL di DocumentDB:
   
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
8. Esistono molti modi tooupdate un documento con hello DocumentClient. Nell'applicazione elenco attività, è necessario tootoggle in grado di toobe se un oggetto TodoItem è stato completato. Ciò può essere ottenuto l'aggiornamento dell'attributo "completa" di hello documento hello:
   
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
9. Infine, è necessario hello possibilità toodelete a TodoItem dall'elenco. toodo, è possibile utilizzare il metodo di supporto hello è scritto in precedenza tooretrieve hello collegamento self link e quindi indicare hello client toodelete è:
   
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

## <a id="Wire"></a>Passaggio 5: Cablaggio rest hello di hello del progetto di sviluppo di applicazioni Java insieme
Ora che è stato terminato fun hello bits - resta è toobuild un'interfaccia utente rapida e collegarla tooour DAO.

1. Innanzitutto, iniziamo con la creazione di un toocall controller il DAO:
   
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
   
    In un'applicazione più complessa, controller hello possono contenere la logica di business complessa sopra hello DAO.
2. Successivamente, si creerà un controller di toohello servlet tooroute HTTP richieste:
   
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
3. È necessario toohello utente toodisplay interfaccia web utente. Di seguito riscrivere hello index.jsp creato in precedenza:
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
4. Infine, scrivere alcuni interfaccia utente lato client JavaScript tootie hello web e hello servlet insieme:
   
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
5. A questo punto, Ora tutto ciò che resta è un'applicazione hello tootest. Eseguire un'applicazione hello in locale e aggiungere alcuni elementi Todo inserendo il nome di elemento hello e categoria e facendo clic su **Aggiungi attività**.
6. Quando viene visualizzato l'elemento hello, è possibile aggiornare se è stata completata l'attivazione e disattivazione di casella di controllo hello e facendo clic su **Aggiorna attività**.

## <a id="Deploy"></a>Passaggio 6: Distribuire il tooAzure applicazione Java siti Web
Con Siti Web di Azure la procedura di distribuzione di applicazioni Java è molto semplice e consiste nell'esportazione di un'applicazione come file con WAR e nel relativo caricamento tramite controllo del codice sorgente (ad esempio Git) o FTP.

1. tooexport l'applicazione come file WAR, fare clic sul progetto in **Esplora progetti**, fare clic su **esportare**, quindi fare clic su **File WAR**.
2. In hello **WAR esportare** finestra hello seguenti:
   
   * Nella casella progetto Web hello immettere esempio java di documentdb azure.
   * Nella casella destinazione hello, scegliere un file di destinazione toosave hello WAR.
   * Fare clic su **Finish**.
3. Ora che è un file WAR in parte, è possibile semplicemente caricare il tooyour sito Web di Azure **webapps** directory. Per istruzioni sul caricamento di file hello, vedere [aggiungere un tooAzure applicazione Java App del servizio Web App](../app-service-web/web-sites-java-add-app.md).
   
    Una volta caricato toohello WebApp directory file WAR hello, ambiente di runtime hello rileverà che è stato aggiunto e verrà caricato automaticamente.
4. tooview il prodotto finito, passare toohttp://YOUR\_sito\_NAME.azurewebsites.net/azure-java-sample/ e iniziare ad aggiungere le attività.

## <a id="GetProject"></a>Ottenere il progetto hello da GitHub
Tutti gli esempi di hello in questa esercitazione sono inclusi in hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) progetto su GitHub. progetto di attività tooimport hello in Eclipse, assicurarsi di aver software hello e le risorse elencati in hello [prerequisiti](#Prerequisites) sezione, quindi hello seguenti:

1. Installare [Project Lombok](http://projectlombok.org/). Lombok è usato toogenerate costruttori, metodi get, Setter nel progetto hello. Dopo aver scaricato il file di lombok.jar hello, fare doppio clic tooinstall, o installarlo dalla riga di comando hello.
2. Se Eclipse è aperto, chiuderlo e riavviarlo tooload Lombok.
3. In Eclipse, su hello **File** menu, fare clic su **importazione**.
4. In hello **importazione** finestra, fare clic su **Git**, fare clic su **progetti da Git**, quindi fare clic su **Avanti**.
5. In hello **selezionare l'origine del Repository** schermata, fare clic su **Clone URI**.
6. In hello **Git Repository di origine** schermo, in hello **URI** casella, immettere https://github.com/Azure-Samples/java-todo-app.git e quindi fare clic su **Avanti**.
7. In hello **selezione ramo** schermata, assicurarsi che **master** sia selezionata e quindi fare clic su **Avanti**.
8. In hello **destinazione locale** schermata, fare clic su **Sfoglia** tooselect una cartella in cui possono essere copiati e quindi fare clic su repository hello **Avanti**.
9. In hello **toouse una procedura guidata per l'importazione di progetti selezionare** schermata, assicurarsi che **importare progetti esistenti** sia selezionata e quindi fare clic su **Avanti**.
10. In hello **importazione progetti** dello schermo, deseleziona hello **DocumentDB** del progetto e quindi fare clic su **fine**. progetto DocumentDB Hello contiene hello Azure Cosmos DB SDK per Java, in cui si aggiungeranno come dipendenza invece.
11. In **Esplora progetti**passare tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java e sostituire i valori HOST e MASTER_KEY hello con hello URI e chiave primaria per l'account di Azure Cosmos DB, quindi Salva il file hello. Per altre informazioni, vedere [Passaggio 1. Creare un account di database Azure Cosmos DB](#CreateDB).
12. In **Esplora progetti**, fare clic con il pulsante destro hello **esempio java di documentdb azure**, fare clic su **Build Path**, quindi fare clic su **configurare Build Path**.
13. In hello **Java Build Path** schermata nel riquadro di destra hello, seleziona hello **librerie** scheda e quindi fare clic su **aggiungere file JAR esterna**. Passare toohello percorso del file lombok.jar hello e fare clic su **aprire**, quindi fare clic su **OK**.
14. Hello tooopen passaggio 12 di utilizzare **proprietà** nuovamente, finestra e quindi nel riquadro di sinistra hello fare clic su **destinazione runtime**.
15. In hello **destinazione runtime** schermata, fare clic su **New**selezionare **versione 7.0 Apache Tomcat**e quindi fare clic su **OK**.
16. Hello di usare il passaggio 12 tooopen **proprietà** nuovamente, finestra e quindi nel riquadro di sinistra hello fare clic su **facet progetto**.
17. In hello **progetto facet** selezionare **modulo Web dinamico** e **Java**, quindi fare clic su **OK**.
18. In hello **server** scheda in basso hello hello destro del mouse su **Tomcat versione 7.0 Server in localhost** e quindi fare clic su **aggiungere e rimuovere**.
19. In hello **aggiungere e rimuovere** finestra spostare **esempio java di documentdb azure** toohello **configurata** casella e quindi fare clic su **fine**.
20. In hello **server** scheda, fare doppio clic su **Tomcat versione 7.0 Server in localhost**, quindi fare clic su **riavviare**.
21. In un browser, passare toohttp://localhost:8080 esempio java di documentdb azure / / e iniziare ad aggiungere l'elenco di attività tooyour. Si noti che se è stato modificato i valori di porta predefinito, modificare il valore di toohello 8080 selezionato.
22. vedere il sito web di Azure, di tooan progetto toodeploy [passaggio 6. Distribuire i siti Web di tooAzure applicazione](#Deploy).

[1]: media/documentdb-java-application/keys.png
