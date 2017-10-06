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
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a><span data-ttu-id="dc9c4-103">Compilare e distribuire un'app per le API Java nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="dc9c4-103">Build and deploy a Java API app in Azure App Service</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="dc9c4-104">Questa esercitazione viene illustrato come un'applicazione Java toocreate e distribuire le applicazioni API del servizio App tooAzure utilizzando [Git].</span><span class="sxs-lookup"><span data-stu-id="dc9c4-104">This tutorial shows how toocreate a Java application and deploy it tooAzure App Service API Apps using [Git].</span></span> <span data-ttu-id="dc9c4-105">istruzioni di Hello in questa esercitazione possono essere seguite su qualsiasi sistema operativo che è in grado di eseguire Java.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="dc9c4-106">codice Hello in questa esercitazione viene compilato utilizzando [Maven].</span><span class="sxs-lookup"><span data-stu-id="dc9c4-106">hello code in this tutorial is built using [Maven].</span></span> <span data-ttu-id="dc9c4-107">[JAX RS] è usato toocreate hello servizio RESTful e viene generato in base hello [Swagger] specifiche dei metadati utilizzando hello [Swagger Editor].</span><span class="sxs-lookup"><span data-stu-id="dc9c4-107">[Jax-RS] is used toocreate hello RESTful Service, and is generated based on hello [Swagger] metadata specification using hello [Swagger Editor].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc9c4-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dc9c4-108">Prerequisites</span></span>
1. <span data-ttu-id="dc9c4-109">[Java Development Kit 8] \((o versione successiva)</span><span class="sxs-lookup"><span data-stu-id="dc9c4-109">[Java Developer's Kit 8] \(or later)</span></span>
2. <span data-ttu-id="dc9c4-110">[Maven] installato nel computer di sviluppo</span><span class="sxs-lookup"><span data-stu-id="dc9c4-110">[Maven] installed on your development machine</span></span>
3. <span data-ttu-id="dc9c4-111">[Git] installato nel computer di sviluppo</span><span class="sxs-lookup"><span data-stu-id="dc9c4-111">[Git] installed on your development machine</span></span>
4. <span data-ttu-id="dc9c4-112">Un pagamento o [versione di valutazione gratuita] sottoscrizione troppo[Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="dc9c4-112">A paid or [free trial] subscription too[Microsoft Azure]</span></span>
5. <span data-ttu-id="dc9c4-113">Un'applicazione di test HTTP come [Postman]</span><span class="sxs-lookup"><span data-stu-id="dc9c4-113">An HTTP test application like [Postman]</span></span>

## <a name="scaffold-hello-api-using-swaggerio"></a><span data-ttu-id="dc9c4-114">API di hello Scaffold utilizzando Swagger.IO</span><span class="sxs-lookup"><span data-stu-id="dc9c4-114">Scaffold hello API using Swagger.IO</span></span>
<span data-ttu-id="dc9c4-115">Editor di hello swagger.io online, è possibile immettere codice JSON Swagger o YAML che rappresenta la struttura hello dell'API.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-115">Using hello swagger.io online editor, you can enter Swagger JSON or YAML code representing hello structure of your API.</span></span> <span data-ttu-id="dc9c4-116">Dopo aver creato il della superficie di attacco di hello API progettato, è possibile esportare il codice per un'ampia gamma di piattaforme e Framework.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-116">Once you have hello API surface area designed, you can export code for a variety of platforms and frameworks.</span></span> <span data-ttu-id="dc9c4-117">Nella sezione successiva hello, codice hello scaffolding sarà funzionalità fittizio tooinclude modificato.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-117">In hello next section, hello scaffolded code will be modified tooinclude mock functionality.</span></span> 

<span data-ttu-id="dc9c4-118">In questa dimostrazione inizierà con un corpo JSON Swagger verranno incollati in editor swagger.io hello, che verrà quindi essere utilizzato toogenerate codice che utilizza tooaccess JAX RS un endpoint dell'API REST.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-118">This demonstration will begin with a Swagger JSON body that you will paste into hello swagger.io editor, which will then be used toogenerate code making use of JAX-RS tooaccess a REST API endpoint.</span></span> <span data-ttu-id="dc9c4-119">Quindi, viene modificato dati fittizi tooreturn codice hello scaffolding, simulando un'API REST compilato nella parte superiore di un meccanismo di persistenza dei dati.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-119">Then, you'll edit hello scaffolded code tooreturn mock data, simulating a REST API built atop a data persistence mechanism.</span></span>  

1. <span data-ttu-id="dc9c4-120">Hello copia negli Appunti tooyour di codice JSON Swagger seguente:</span><span class="sxs-lookup"><span data-stu-id="dc9c4-120">Copy hello following Swagger JSON code tooyour clipboard:</span></span>
   
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
2. <span data-ttu-id="dc9c4-121">Passare toohello [Online Editor Swagger].</span><span class="sxs-lookup"><span data-stu-id="dc9c4-121">Navigate toohello [Online Swagger Editor].</span></span> <span data-ttu-id="dc9c4-122">Una volta, fare clic su hello **File -> Incolla JSON** voce di menu.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-122">Once there, click hello **File -> Paste JSON** menu item.</span></span>
   
    ![Voce di menu Paste JSON (Incolla JSON)][paste-json]
3. <span data-ttu-id="dc9c4-124">Incollare in hello contatti elenco API Swagger JSON copiato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-124">Paste in hello Contacts List API Swagger JSON you copied earlier.</span></span> 
   
    ![Incollare codice JSON in Swagger][pasted-swagger]
4. <span data-ttu-id="dc9c4-126">Consente di visualizzare pagine della documentazione di hello e visualizzato nell'editor di hello riepilogo delle API.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-126">View hello documentation pages and API summary rendered in hello editor.</span></span> 
   
    ![Visualizzare documenti generati da Swagger][view-swagger-generated-docs]
5. <span data-ttu-id="dc9c4-128">Seleziona hello **generare Server -> JAX RS** codice lato server menu opzione tooscaffold hello modificherai implementazione fittizia di tooadd successive.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-128">Select hello **Generate Server -> JAX-RS** menu option tooscaffold hello server-side code you'll edit later tooadd mock implementation.</span></span> 
   
    ![Generare una voce di menu del codice][generate-code-menu-item]
   
    <span data-ttu-id="dc9c4-130">Dopo la generazione del codice hello, all'utente verrà fornito un toodownload file ZIP.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-130">Once hello code is generated, you'll be provided a ZIP file toodownload.</span></span> <span data-ttu-id="dc9c4-131">Questo file contiene codice hello scaffolding dal generatore di codice hello Swagger e tutti associati gli script di compilazione.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-131">This file contains hello code scaffolded by hello Swagger code generator and all associated build scripts.</span></span> <span data-ttu-id="dc9c4-132">Decomprimere directory tooa intera libreria di hello nella workstation di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-132">Unzip hello entire library tooa directory on your development workstation.</span></span> 

## <a name="edit-hello-code-tooadd-api-implementation"></a><span data-ttu-id="dc9c4-133">Modifica tooadd codice hello implementazione delle API</span><span class="sxs-lookup"><span data-stu-id="dc9c4-133">Edit hello Code tooadd API Implementation</span></span>
<span data-ttu-id="dc9c4-134">In questa sezione sostituirai implementazione sul lato server hello generato Swagger del codice con il codice personalizzato.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-134">In this section, you'll replace hello Swagger-generated code's server-side implementation with your custom code.</span></span> <span data-ttu-id="dc9c4-135">nuovo codice Hello restituirà un ArrayList di contatto entità toohello del client chiamante.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-135">hello new code will return an ArrayList of Contact entities toohello calling client.</span></span> 

1. <span data-ttu-id="dc9c4-136">Aprire hello *Contact.java* file di modello, che si trova in hello *src/gen/java/io/swagger/modello* cartella utilizzando [codice di Visual Studio] o un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-136">Open hello *Contact.java* model file, which is located in hello *src/gen/java/io/swagger/model* folder, using [Visual Studio Code] or your favorite text editor.</span></span> 
   
    ![Aprire un file di modello dei contatti][open-contact-model-file]
2. <span data-ttu-id="dc9c4-138">Aggiungere hello seguente costruttore all'interno di hello **contatto** classe.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-138">Add hello following constructor within hello **Contact** class.</span></span> 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. <span data-ttu-id="dc9c4-139">Aprire hello *ContactsApiServiceImpl.java* file di implementazione del servizio, che si trova in hello *src/main/java/io/swagger/api/impl* cartella utilizzando [codice di Visual Studio]o un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-139">Open hello *ContactsApiServiceImpl.java* service implementation file, which is located in hello *src/main/java/io/swagger/api/impl* folder, using [Visual Studio Code] or your favorite text editor.</span></span>
   
    ![Aprire il file del codice di servizio dei contatti][open-contact-service-code-file]
4. <span data-ttu-id="dc9c4-141">Sovrascrivere il codice di hello nel file hello con questo nuovo tooadd di codice un codice di implementazione fittizia toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-141">Overwrite hello code in hello file with this new code tooadd a mock implementation toohello service code.</span></span> 
   
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
5. <span data-ttu-id="dc9c4-142">Aprire un prompt dei comandi e modificare una cartella radice toohello di directory dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-142">Open a command prompt and change directory toohello root folder of your application.</span></span>
6. <span data-ttu-id="dc9c4-143">Eseguire hello seguendo Maven comando toobuild hello codice ed eseguirlo utilizzando hello server app Jetty locale.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-143">Execute hello following Maven command toobuild hello code and run it using hello Jetty app server locally.</span></span> 
   
        mvn package jetty:run
7. <span data-ttu-id="dc9c4-144">Verrà visualizzata la finestra di comando hello riflettere che Jetty ha avviato il codice sulla porta 8080.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-144">You should see hello command window reflect that Jetty has started your code on port 8080.</span></span> 
   
    ![Aprire il file del codice di servizio dei contatti][run-jetty-war]
8. <span data-ttu-id="dc9c4-146">Utilizzare [Postman] toomake un'API di richiesta toohello "ottenere tutti i contatti" metodo http://localhost:8080/api/contatti.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-146">Use [Postman] toomake a request toohello "get all contacts" API method at http://localhost:8080/api/contacts.</span></span>
   
    ![Hello chiamata dell'API contatti][calling-contacts-api]
9. <span data-ttu-id="dc9c4-148">Utilizzare [Postman] metodo toomake un'API di richiesta toohello "ottenere un contatto specifico" disponibile all'indirizzo http://localhost:8080/api/contatti/2.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-148">Use [Postman] toomake a request toohello "get specific contact" API method located at http://localhost:8080/api/contacts/2.</span></span>
   
    ![Hello chiamata dell'API contatti][calling-specific-contact-api]
10. <span data-ttu-id="dc9c4-150">Infine, compilare file WAR Java (archivio Web) hello eseguendo hello comando Maven nella console seguente.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-150">Finally, build hello Java WAR (Web ARchive) file by executing hello following Maven command in your console.</span></span> 
    
         mvn package war:war
11. <span data-ttu-id="dc9c4-151">Una volta creato file WAR hello, sarà inserito hello **destinazione** cartella.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-151">Once hello WAR file is built, it will be placed into hello **target** folder.</span></span> <span data-ttu-id="dc9c4-152">Passare alla hello **destinazione** cartella e rinominare hello file WAR troppo**ROOT.war**.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-152">Navigate into hello **target** folder and rename hello WAR file too**ROOT.war**.</span></span> <span data-ttu-id="dc9c4-153">(Assicurarsi che l'uso delle maiuscole hello corrisponde a questo formato).</span><span class="sxs-lookup"><span data-stu-id="dc9c4-153">(Make sure hello capitalization matches this format).</span></span>
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. <span data-ttu-id="dc9c4-154">Infine, eseguire i seguenti comandi dalla cartella radice hello toocreate l'applicazione hello un **distribuire** hello di toodeploy toouse cartella WAR file tooAzure.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-154">Finally, execute hello following commands from hello root folder of your application toocreate a **deploy** folder toouse toodeploy hello WAR file tooAzure.</span></span> 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a><span data-ttu-id="dc9c4-155">Pubblicare l'output di hello tooAzure servizio App</span><span class="sxs-lookup"><span data-stu-id="dc9c4-155">Publish hello output tooAzure App Service</span></span>
<span data-ttu-id="dc9c4-156">In questa sezione che si apprenderà come toocreate una nuova App API hello tramite il portale di Azure, preparare tale App per le API per l'hosting di applicazioni Java e distribuire hello appena creato WAR file tooAzure toorun di servizio App di App per le nuove API.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-156">In this section you'll learn how toocreate a new API App using hello Azure Portal, prepare that API App for hosting Java applications, and deploy hello newly-created WAR file tooAzure App Service toorun your new API App.</span></span> 

1. <span data-ttu-id="dc9c4-157">Creare una nuova app per le API in hello [portale di Azure], facendo clic su hello **nuovo -> Web + Mobile -> app per le API** voce di menu, immettere i dettagli dell'app e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-157">Create a new API app in hello [Azure portal], by clicking hello **New -> Web + Mobile -> API app** menu item, entering your app details, and then clicking **Create**.</span></span>
   
    ![Creare una nuova app per le API][create-api-app]
2. <span data-ttu-id="dc9c4-159">Dopo aver creato l'app dell'API, aprire l'app **impostazioni** pannello, quindi fare clic su hello **le impostazioni dell'applicazione** voce di menu.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-159">Once your API app has been created, open your app's **Settings** blade, and then click hello **Application settings** menu item.</span></span> <span data-ttu-id="dc9c4-160">Selezionare hello versioni più recenti di Java delle opzioni disponibili hello, quindi selezionare hello Tomcat più recenti da hello **contenitore Web** menu e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-160">Select hello latest Java versions from hello available options, then select hello latest Tomcat from hello **Web container** menu, and then click **Save**.</span></span>
   
    ![Nel linguaggio hello pannello App per le API][set-up-java]
3. <span data-ttu-id="dc9c4-162">Fare clic su hello **le credenziali di distribuzione** menu impostazioni di elemento e fornire un nome utente e la password da toouse per la pubblicazione di file tooyour App per le API.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-162">Click hello **Deployment credentials** settings menu item, and provide a username and password you wish toouse for publishing files tooyour API App.</span></span> 
   
    ![Reimpostare le credenziali di distribuzione][deployment-credentials]
4. <span data-ttu-id="dc9c4-164">Fare clic su hello **origine distribuzione** voce di menu impostazioni.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-164">Click hello **Deployment source** settings menu item.</span></span> <span data-ttu-id="dc9c4-165">Una volta, fare clic su hello **origine scegliere** pulsante, hello seleziona **Git Repository locale** opzione e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-165">Once there, click hello **Choose source** button, select hello **Local Git Repository** option, and then click **OK**.</span></span> <span data-ttu-id="dc9c4-166">Verrà creato un repository Git in esecuzione in Azure, contenente un'associazione con l'app per le API.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-166">This will create a Git repository running in Azure, that has an association with your API App.</span></span> <span data-ttu-id="dc9c4-167">Ogni volta che si esegue il commit codice toohello *master* ramo del repository Git, il codice verrà pubblicato nell'istanza API App in esecuzione in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-167">Each time you commit code toohello *master* branch of your Git repository, your code will be published into your live running API App instance.</span></span> 
   
    ![Configurare un nuovo repository Git locale][select-git-repo]
5. <span data-ttu-id="dc9c4-169">Copiare negli Appunti tooyour dell'hello nuovo repository Git URL.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-169">Copy hello new Git repository's URL tooyour clipboard.</span></span> <span data-ttu-id="dc9c4-170">Salvare il file, poiché risulterà di grande importanza più avanti.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-170">Save this as it will be important in a moment.</span></span> 
   
    ![Configurare un nuovo repository Git per l'app][copy-git-repo-url]
6. <span data-ttu-id="dc9c4-172">Push hello WAR file toohello online repository GIT.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-172">Git push hello WAR file toohello online repository.</span></span> <span data-ttu-id="dc9c4-173">toodo, passare alla hello **distribuire** cartella creata in precedenza in modo che è possibile applicare facilmente codice hello backup toohello repository in esecuzione nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-173">toodo this, navigate into hello **deploy** folder you created earlier so that you can easily commit hello code up toohello repository running in your App Service.</span></span> <span data-ttu-id="dc9c4-174">Una volta è nella finestra di console hello e spostato nella cartella hello cartella webapps hello in cui si trova, emettere hello Git comandi toolaunch hello processo e attivano una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-174">Once you're in hello console window and navigated into hello folder where hello webapps folder is located, issue hello following Git commands toolaunch hello process and fire off a deployment.</span></span> 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    <span data-ttu-id="dc9c4-175">Quando si esegue hello **push** richiesta, verrà chiesto di password hello creato in precedenza per le credenziali di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-175">Once you issue hello **push** request, you'll be asked for hello password you created for hello deployment credential earlier.</span></span> <span data-ttu-id="dc9c4-176">Dopo aver immesso le credenziali, verrà visualizzata la visualizzazione del portale che hello aggiornamento è stata distribuita.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-176">After you enter your credentials, you should see your portal display that hello update was deployed.</span></span>
7. <span data-ttu-id="dc9c4-177">Se si utilizza ancora una volta Postman toohit hello appena distribuito API App in esecuzione in Azure App Service, si noterà che il comportamento di hello è coerente e che ora ha restituito dati di contatto come previsto, e con le modifiche di codice semplice toohello Swagger.io scaffolding codice Java.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-177">If you once again use Postman toohit hello newly-deployed API App running in Azure App Service, you'll see that hello behavior is consistent and that now it is returning contact data as expected, and using simple code changes toohello Swagger.io scaffolded Java code.</span></span> 
   
    ![Usare l'API REST dei contatti Java in Azure][postman-calling-azure-contacts]

## <a name="next-steps"></a><span data-ttu-id="dc9c4-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dc9c4-179">Next steps</span></span>
<span data-ttu-id="dc9c4-180">In questo articolo è stato in grado di toostart con un file Swagger JSON e codice Java scaffolding ottenuto dall'editor Swagger.io hello.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-180">In this article, you were able toostart with a Swagger JSON file and some scaffolded Java code obtained from hello Swagger.io editor.</span></span> <span data-ttu-id="dc9c4-181">Con alcune modifiche e un processo di distribuzione di un repository Git è stata creata un'app per le API funzionale, scritta in Java.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-181">From there, your simple changes and a Git deploy process resulted in having a functional API app written in Java.</span></span> <span data-ttu-id="dc9c4-182">esercitazione successiva Hello viene illustrato come troppo[utilizzare App per le API da client JavaScript, tramite condivisione CORS][App Service API CORS].</span><span class="sxs-lookup"><span data-stu-id="dc9c4-182">hello next tutorial shows how too[consume API apps from JavaScript clients, using CORS][App Service API CORS].</span></span> <span data-ttu-id="dc9c4-183">Le esercitazioni successive in hello serie Mostra come tooimplement autenticazione e autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-183">Later tutorials in hello series show how tooimplement authentication and authorization.</span></span>

<span data-ttu-id="dc9c4-184">toobuild in questo esempio, per ulteriori informazioni su hello [Storage SDK per Java] BLOB di toopersist hello JSON.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-184">toobuild on this sample, you can learn more about hello [Storage SDK for Java] toopersist hello JSON blobs.</span></span> <span data-ttu-id="dc9c4-185">In alternativa, è Impossibile usare hello [SDK per Java DB documento] toosave tooAzure di dati del contatto DB documento.</span><span class="sxs-lookup"><span data-stu-id="dc9c4-185">Or, you could use hello [Document DB Java SDK] toosave your Contact data tooAzure Document DB.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="dc9c4-186">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="dc9c4-186">See Also</span></span>
<span data-ttu-id="dc9c4-187">Per altre informazioni sull'uso di Azure con Java, vedere [Azure for Java developers](/java/azure) (Azure per sviluppatori Java).</span><span class="sxs-lookup"><span data-stu-id="dc9c4-187">For more information about using Azure with Java, visit [Azure for Java developers](/java/azure).</span></span>

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
