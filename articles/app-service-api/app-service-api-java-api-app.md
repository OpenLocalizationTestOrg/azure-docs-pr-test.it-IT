---
title: aaaBuild e distribuire un'applicazione API Java in Azure App Service
description: Informazioni su come un'applicazione API Java toocreate pacchetto e distribuirlo tooAzure servizio App.
services: app-service\api
documentationcenter: java
author: rmcmurray
manager: erikre
editor: tdykstra
ms.assetid: 8d21ba5f-fc57-4269-bc8f-2fcab936ec22
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: get-started-article
ms.date: 04/25/2017
ms.author: rachelap;robmcm
ms.openlocfilehash: a4056fec870b1c4bed8ee14bb0e748b3ee89b9e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a>Compilare e distribuire un'app per le API Java nel servizio app di Azure
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

Questa esercitazione viene illustrato come un'applicazione Java toocreate e distribuire le applicazioni API del servizio App tooAzure utilizzando [Git]. istruzioni di Hello in questa esercitazione possono essere seguite su qualsiasi sistema operativo che è in grado di eseguire Java. codice Hello in questa esercitazione viene compilato utilizzando [Maven]. [JAX RS] è usato toocreate hello servizio RESTful e viene generato in base hello [Swagger] specifiche dei metadati utilizzando hello [Swagger Editor].

## <a name="prerequisites"></a>Prerequisiti
1. [Java Development Kit 8] \((o versione successiva)
2. [Maven] installato nel computer di sviluppo
3. [Git] installato nel computer di sviluppo
4. Un pagamento o [versione di valutazione gratuita] sottoscrizione troppo[Microsoft Azure]
5. Un'applicazione di test HTTP come [Postman]

## <a name="scaffold-hello-api-using-swaggerio"></a>API di hello Scaffold utilizzando Swagger.IO
Editor di hello swagger.io online, è possibile immettere codice JSON Swagger o YAML che rappresenta la struttura hello dell'API. Dopo aver creato il della superficie di attacco di hello API progettato, è possibile esportare il codice per un'ampia gamma di piattaforme e Framework. Nella sezione successiva hello, codice hello scaffolding sarà funzionalità fittizio tooinclude modificato. 

In questa dimostrazione inizierà con un corpo JSON Swagger verranno incollati in editor swagger.io hello, che verrà quindi essere utilizzato toogenerate codice che utilizza tooaccess JAX RS un endpoint dell'API REST. Quindi, viene modificato dati fittizi tooreturn codice hello scaffolding, simulando un'API REST compilato nella parte superiore di un meccanismo di persistenza dei dati.  

1. Hello copia negli Appunti tooyour di codice JSON Swagger seguente:
   
        {
            "swagger": "2.0",
            "info": {
                "version": "v1",
                "title": "Contact List",
                "description": "A Contact list API based on Swagger and built using Java"
            },
            "host": "localhost",
            "schemes": [
                "http",
                "https"
            ],
            "basePath": "/api",
            "paths": {
                "/contacts": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_get",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                },
                "/contacts/{id}": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_getById",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "parameters": [
                            {
                                "name": "id",
                                "in": "path",
                                "required": true,
                                "type": "integer",
                                "format": "int32"
                            }
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                }
            },
            "definitions": {
                "Contact": {
                    "type": "object",
                    "properties": {
                        "Id": {
                            "format": "int32",
                            "type": "integer"
                        },
                        "Name": {
                            "type": "string"
                        },
                        "EmailAddress": {
                            "type": "string"
                        }
                    }
                }
            }
        }
2. Passare toohello [Online Editor Swagger]. Una volta, fare clic su hello **File -> Incolla JSON** voce di menu.
   
    ![Voce di menu Paste JSON (Incolla JSON)][paste-json]
3. Incollare in hello contatti elenco API Swagger JSON copiato in precedenza. 
   
    ![Incollare codice JSON in Swagger][pasted-swagger]
4. Consente di visualizzare pagine della documentazione di hello e visualizzato nell'editor di hello riepilogo delle API. 
   
    ![Visualizzare documenti generati da Swagger][view-swagger-generated-docs]
5. Seleziona hello **generare Server -> JAX RS** codice lato server menu opzione tooscaffold hello modificherai implementazione fittizia di tooadd successive. 
   
    ![Generare una voce di menu del codice][generate-code-menu-item]
   
    Dopo la generazione del codice hello, all'utente verrà fornito un toodownload file ZIP. Questo file contiene codice hello scaffolding dal generatore di codice hello Swagger e tutti associati gli script di compilazione. Decomprimere directory tooa intera libreria di hello nella workstation di sviluppo. 

## <a name="edit-hello-code-tooadd-api-implementation"></a>Modifica tooadd codice hello implementazione delle API
In questa sezione sostituirai implementazione sul lato server hello generato Swagger del codice con il codice personalizzato. nuovo codice Hello restituirà un ArrayList di contatto entità toohello del client chiamante. 

1. Aprire hello *Contact.java* file di modello, che si trova in hello *src/gen/java/io/swagger/modello* cartella utilizzando [codice di Visual Studio] o un editor di testo. 
   
    ![Aprire un file di modello dei contatti][open-contact-model-file]
2. Aggiungere hello seguente costruttore all'interno di hello **contatto** classe. 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. Aprire hello *ContactsApiServiceImpl.java* file di implementazione del servizio, che si trova in hello *src/main/java/io/swagger/api/impl* cartella utilizzando [codice di Visual Studio]o un editor di testo.
   
    ![Aprire il file del codice di servizio dei contatti][open-contact-service-code-file]
4. Sovrascrivere il codice di hello nel file hello con questo nuovo tooadd di codice un codice di implementazione fittizia toohello servizio. 
   
        package io.swagger.api.impl;
   
        import io.swagger.api.*;
        
        import io.swagger.model.Contact;
        import java.util.*;
        import io.swagger.api.NotFoundException;
               
        import javax.ws.rs.core.Response;
        import javax.ws.rs.core.SecurityContext;
   
        @javax.annotation.Generated(value = "class io.swagger.codegen.languages.JaxRSServerCodegen", date = "2015-11-24T21:54:11.648Z")
        public class ContactsApiServiceImpl extends ContactsApiService {
   
            private ArrayList<Contact> loadContacts()
            {
                ArrayList<Contact> list = new ArrayList<Contact>();
                list.add(new Contact(1, "Barney Poland", "barney@contoso.com"));
                list.add(new Contact(2, "Lacy Barrera", "lacy@contoso.com"));
                list.add(new Contact(3, "Lora Riggs", "lora@contoso.com"));
                return list;
            }
   
            @Override
            public Response contactsGet(SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                return Response.ok().entity(list).build();
                }
   
            @Override
            public Response contactsGetById(Integer id, SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                Contact ret = null;
   
                for(int i=0; i<list.size(); i++)
                {
                    if(list.get(i).getId() == id)
                        {
                            ret = list.get(i);
                        }
                }
                return Response.ok().entity(ret).build();
            }
        }
5. Aprire un prompt dei comandi e modificare una cartella radice toohello di directory dell'applicazione.
6. Eseguire hello seguendo Maven comando toobuild hello codice ed eseguirlo utilizzando hello server app Jetty locale. 
   
        mvn package jetty:run
7. Verrà visualizzata la finestra di comando hello riflettere che Jetty ha avviato il codice sulla porta 8080. 
   
    ![Aprire il file del codice di servizio dei contatti][run-jetty-war]
8. Utilizzare [Postman] toomake un'API di richiesta toohello "ottenere tutti i contatti" metodo http://localhost:8080/api/contatti.
   
    ![Hello chiamata dell'API contatti][calling-contacts-api]
9. Utilizzare [Postman] metodo toomake un'API di richiesta toohello "ottenere un contatto specifico" disponibile all'indirizzo http://localhost:8080/api/contatti/2.
   
    ![Hello chiamata dell'API contatti][calling-specific-contact-api]
10. Infine, compilare file WAR Java (archivio Web) hello eseguendo hello comando Maven nella console seguente. 
    
         mvn package war:war
11. Una volta creato file WAR hello, sarà inserito hello **destinazione** cartella. Passare alla hello **destinazione** cartella e rinominare hello file WAR troppo**ROOT.war**. (Assicurarsi che l'uso delle maiuscole hello corrisponde a questo formato).
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. Infine, eseguire i seguenti comandi dalla cartella radice hello toocreate l'applicazione hello un **distribuire** hello di toodeploy toouse cartella WAR file tooAzure. 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a>Pubblicare l'output di hello tooAzure servizio App
In questa sezione che si apprenderà come toocreate una nuova App API hello tramite il portale di Azure, preparare tale App per le API per l'hosting di applicazioni Java e distribuire hello appena creato WAR file tooAzure toorun di servizio App di App per le nuove API. 

1. Creare una nuova app per le API in hello [portale di Azure], facendo clic su hello **nuovo -> Web + Mobile -> app per le API** voce di menu, immettere i dettagli dell'app e quindi fare clic su **crea**.
   
    ![Creare una nuova app per le API][create-api-app]
2. Dopo aver creato l'app dell'API, aprire l'app **impostazioni** pannello, quindi fare clic su hello **le impostazioni dell'applicazione** voce di menu. Selezionare hello versioni più recenti di Java delle opzioni disponibili hello, quindi selezionare hello Tomcat più recenti da hello **contenitore Web** menu e quindi fare clic su **salvare**.
   
    ![Nel linguaggio hello pannello App per le API][set-up-java]
3. Fare clic su hello **le credenziali di distribuzione** menu impostazioni di elemento e fornire un nome utente e la password da toouse per la pubblicazione di file tooyour App per le API. 
   
    ![Reimpostare le credenziali di distribuzione][deployment-credentials]
4. Fare clic su hello **origine distribuzione** voce di menu impostazioni. Una volta, fare clic su hello **origine scegliere** pulsante, hello seleziona **Git Repository locale** opzione e quindi fare clic su **OK**. Verrà creato un repository Git in esecuzione in Azure, contenente un'associazione con l'app per le API. Ogni volta che si esegue il commit codice toohello *master* ramo del repository Git, il codice verrà pubblicato nell'istanza API App in esecuzione in tempo reale. 
   
    ![Configurare un nuovo repository Git locale][select-git-repo]
5. Copiare negli Appunti tooyour dell'hello nuovo repository Git URL. Salvare il file, poiché risulterà di grande importanza più avanti. 
   
    ![Configurare un nuovo repository Git per l'app][copy-git-repo-url]
6. Push hello WAR file toohello online repository GIT. toodo, passare alla hello **distribuire** cartella creata in precedenza in modo che è possibile applicare facilmente codice hello backup toohello repository in esecuzione nel servizio App. Una volta è nella finestra di console hello e spostato nella cartella hello cartella webapps hello in cui si trova, emettere hello Git comandi toolaunch hello processo e attivano una distribuzione. 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    Quando si esegue hello **push** richiesta, verrà chiesto di password hello creato in precedenza per le credenziali di distribuzione hello. Dopo aver immesso le credenziali, verrà visualizzata la visualizzazione del portale che hello aggiornamento è stata distribuita.
7. Se si utilizza ancora una volta Postman toohit hello appena distribuito API App in esecuzione in Azure App Service, si noterà che il comportamento di hello è coerente e che ora ha restituito dati di contatto come previsto, e con le modifiche di codice semplice toohello Swagger.io scaffolding codice Java. 
   
    ![Usare l'API REST dei contatti Java in Azure][postman-calling-azure-contacts]

## <a name="next-steps"></a>Passaggi successivi
In questo articolo è stato in grado di toostart con un file Swagger JSON e codice Java scaffolding ottenuto dall'editor Swagger.io hello. Con alcune modifiche e un processo di distribuzione di un repository Git è stata creata un'app per le API funzionale, scritta in Java. esercitazione successiva Hello viene illustrato come troppo[utilizzare App per le API da client JavaScript, tramite condivisione CORS][App Service API CORS]. Le esercitazioni successive in hello serie Mostra come tooimplement autenticazione e autorizzazione.

toobuild in questo esempio, per ulteriori informazioni su hello [Storage SDK per Java] BLOB di toopersist hello JSON. In alternativa, è Impossibile usare hello [SDK per Java DB documento] toosave tooAzure di dati del contatto DB documento. 

<a name="see-also"></a>

## <a name="see-also"></a>Vedere anche
Per altre informazioni sull'uso di Azure con Java, vedere [Azure for Java developers](/java/azure) (Azure per sviluppatori Java).

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[portale di Azure]: https://portal.azure.com/
[SDK per Java DB documento]: ../documentdb/documentdb-java-application.md
[versione di valutazione gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Java Development Kit 8]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[JAX RS]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[Online Editor Swagger]: http://editor2.swagger.io/
[Postman]: https://www.getpostman.com/
[Storage SDK per Java]:../storage/blobs/storage-java-how-to-use-blob-storage.md
[Swagger]: http://swagger.io/
[Swagger Editor]: http://editor.swagger.io/
[codice di Visual Studio]: https://code.visualstudio.com

<!-- IMG List -->

[paste-json]: ./media/app-service-api-java-api-app/paste-json.png
[pasted-swagger]: ./media/app-service-api-java-api-app/pasted-swagger.png
[view-swagger-generated-docs]: ./media/app-service-api-java-api-app/view-swagger-generated-docs.png
[generate-code-menu-item]: ./media/app-service-api-java-api-app/generate-code-menu-item.png
[open-contact-model-file]: ./media/app-service-api-java-api-app/open-contact-model-file.png
[open-contact-service-code-file]: ./media/app-service-api-java-api-app/open-contact-service-code-file.png
[run-jetty-war]: ./media/app-service-api-java-api-app/run-jetty-war.png
[calling-contacts-api]: ./media/app-service-api-java-api-app/calling-contacts-api.png
[calling-specific-contact-api]: ./media/app-service-api-java-api-app/calling-specific-contact-api.png
[create-api-app]: ./media/app-service-api-java-api-app/create-api-app.png
[set-up-java]: ./media/app-service-api-java-api-app/set-up-java.png
[deployment-credentials]: ./media/app-service-api-java-api-app/deployment-credentials.png
[select-git-repo]: ./media/app-service-api-java-api-app/select-git-repo.png
[copy-git-repo-url]: ./media/app-service-api-java-api-app/copy-git-repo-url.png
[postman-calling-azure-contacts]: ./media/app-service-api-java-api-app/postman-calling-azure-contacts.png
