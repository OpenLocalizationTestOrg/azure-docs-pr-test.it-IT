---
title: Compilare e distribuire un'app per le API Java nel servizio app di Azure
description: Informazioni su come creare un pacchetto dell'app per le API Java e distribuirlo nel servizio app di Azure.
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
ms.openlocfilehash: e38c540071cb49b0177e79178566d72ecb5f8886
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a><span data-ttu-id="0a8f1-103">Compilare e distribuire un'app per le API Java nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="0a8f1-103">Build and deploy a Java API app in Azure App Service</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="0a8f1-104">Questa esercitazione illustra come creare un'applicazione Java e come distribuirla nelle app per le API del servizio app di Azure tramite [Git].</span><span class="sxs-lookup"><span data-stu-id="0a8f1-104">This tutorial shows how to create a Java application and deploy it to Azure App Service API Apps using [Git].</span></span> <span data-ttu-id="0a8f1-105">Le istruzioni di questa esercitazione possono essere eseguite in qualsiasi sistema operativo in grado di eseguire Java.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-105">The instructions in this tutorial can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="0a8f1-106">Il codice in questa esercitazione viene compilato con [Maven].</span><span class="sxs-lookup"><span data-stu-id="0a8f1-106">The code in this tutorial is built using [Maven].</span></span> <span data-ttu-id="0a8f1-107">[Jax-RS] consente invece di creare il servizio RESTful e viene generato in base alle specifiche dei metadati [Swagger] usando l'[editor Swagger].</span><span class="sxs-lookup"><span data-stu-id="0a8f1-107">[Jax-RS] is used to create the RESTful Service, and is generated based on the [Swagger] metadata specification using the [Swagger Editor].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a8f1-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0a8f1-108">Prerequisites</span></span>
1. <span data-ttu-id="0a8f1-109">[Java Development Kit 8] \((o versione successiva)</span><span class="sxs-lookup"><span data-stu-id="0a8f1-109">[Java Developer's Kit 8] \(or later)</span></span>
2. <span data-ttu-id="0a8f1-110">[Maven] installato nel computer di sviluppo</span><span class="sxs-lookup"><span data-stu-id="0a8f1-110">[Maven] installed on your development machine</span></span>
3. <span data-ttu-id="0a8f1-111">[Git] installato nel computer di sviluppo</span><span class="sxs-lookup"><span data-stu-id="0a8f1-111">[Git] installed on your development machine</span></span>
4. <span data-ttu-id="0a8f1-112">Una sottoscrizione di [valutazione gratuita] o a pagamento a [Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="0a8f1-112">A paid or [free trial] subscription to [Microsoft Azure]</span></span>
5. <span data-ttu-id="0a8f1-113">Un'applicazione di test HTTP come [Postman]</span><span class="sxs-lookup"><span data-stu-id="0a8f1-113">An HTTP test application like [Postman]</span></span>

## <a name="scaffold-the-api-using-swaggerio"></a><span data-ttu-id="0a8f1-114">Eseguire lo scaffolding dell'API con Swagger.IO</span><span class="sxs-lookup"><span data-stu-id="0a8f1-114">Scaffold the API using Swagger.IO</span></span>
<span data-ttu-id="0a8f1-115">Nell'editor online Swagger.io è possibile immettere il codice YAML o JSON Swagger che rappresenta la struttura dell'API.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-115">Using the swagger.io online editor, you can enter Swagger JSON or YAML code representing the structure of your API.</span></span> <span data-ttu-id="0a8f1-116">Dopo aver progettato la superficie di attacco dell'API, è possibile esportare il codice per vari tipi di piattaforme e framework.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-116">Once you have the API surface area designed, you can export code for a variety of platforms and frameworks.</span></span> <span data-ttu-id="0a8f1-117">Nella sezione successiva, il codice sottoposto a scaffolding verrà modificato in modo da includere la funzionalità di implementazione fittizia.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-117">In the next section, the scaffolded code will be modified to include mock functionality.</span></span> 

<span data-ttu-id="0a8f1-118">In questa dimostrazione, un corpo JSON Swagger iniziale verrà incollato nell'editor Swagger.io, che verrà quindi usato per generare codice che sfrutta JAX-RS per accedere a un endpoint API REST.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-118">This demonstration will begin with a Swagger JSON body that you will paste into the swagger.io editor, which will then be used to generate code making use of JAX-RS to access a REST API endpoint.</span></span> <span data-ttu-id="0a8f1-119">Si modificherà quindi il codice con scaffolding in modo che restituisca dati fittizi, simulando un'API REST creata in base a un meccanismo di persistenza dei dati.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-119">Then, you'll edit the scaffolded code to return mock data, simulating a REST API built atop a data persistence mechanism.</span></span>  

1. <span data-ttu-id="0a8f1-120">Copiare negli appunti il codice JSON Swagger seguente:</span><span class="sxs-lookup"><span data-stu-id="0a8f1-120">Copy the following Swagger JSON code to your clipboard:</span></span>
   
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
2. <span data-ttu-id="0a8f1-121">Passare all' [editor Swagger online].</span><span class="sxs-lookup"><span data-stu-id="0a8f1-121">Navigate to the [Online Swagger Editor].</span></span> <span data-ttu-id="0a8f1-122">Fare clic sulla voce di menu **File -> Paste JSON** (Incolla JSON).</span><span class="sxs-lookup"><span data-stu-id="0a8f1-122">Once there, click the **File -> Paste JSON** menu item.</span></span>
   
    ![Voce di menu Paste JSON (Incolla JSON)][paste-json]
3. <span data-ttu-id="0a8f1-124">Incollare il codice JSON Swagger relativo all'API dell'elenco dei contatti copiato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-124">Paste in the Contacts List API Swagger JSON you copied earlier.</span></span> 
   
    ![Incollare codice JSON in Swagger][pasted-swagger]
4. <span data-ttu-id="0a8f1-126">Visualizzare le pagine di documentazione e il riepilogo dell'API restituito nell'editor.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-126">View the documentation pages and API summary rendered in the editor.</span></span> 
   
    ![Visualizzare documenti generati da Swagger][view-swagger-generated-docs]
5. <span data-ttu-id="0a8f1-128">Selezionare l'opzione di menu **Generate Server -> JAX-RS** (Genera server -> JAX-RS) per eseguire lo scaffolding del codice lato server che dovrà essere modificato per aggiungere l'implementazione fittizia.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-128">Select the **Generate Server -> JAX-RS** menu option to scaffold the server-side code you'll edit later to add mock implementation.</span></span> 
   
    ![Generare una voce di menu del codice][generate-code-menu-item]
   
    <span data-ttu-id="0a8f1-130">Al termine della generazione del codice, verrà visualizzato un file ZIP per il download.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-130">Once the code is generated, you'll be provided a ZIP file to download.</span></span> <span data-ttu-id="0a8f1-131">Il file contiene il codice sottoposto a scaffolding dal generatore di codice Swagger e tutti gli script di compilazione associati.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-131">This file contains the code scaffolded by the Swagger code generator and all associated build scripts.</span></span> <span data-ttu-id="0a8f1-132">Decomprimere l'intera libreria in una directory della workstation di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-132">Unzip the entire library to a directory on your development workstation.</span></span> 

## <a name="edit-the-code-to-add-api-implementation"></a><span data-ttu-id="0a8f1-133">Modificare il codice per aggiungere l'implementazione dell'API</span><span class="sxs-lookup"><span data-stu-id="0a8f1-133">Edit the Code to add API Implementation</span></span>
<span data-ttu-id="0a8f1-134">In questa sezione si sostituirà l'implementazione sul lato server del codice generato da Swagger con il codice personalizzato.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-134">In this section, you'll replace the Swagger-generated code's server-side implementation with your custom code.</span></span> <span data-ttu-id="0a8f1-135">Il nuovo codice restituirà al client chiamante un'entità ArrayList of Contact.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-135">The new code will return an ArrayList of Contact entities to the calling client.</span></span> 

1. <span data-ttu-id="0a8f1-136">Aprire il file di modello *Contact.java* incluso nella cartella *src/gen/java/io/swagger/model* usando [Visual Studio Code] o l'editor di testo preferito.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-136">Open the *Contact.java* model file, which is located in the *src/gen/java/io/swagger/model* folder, using [Visual Studio Code] or your favorite text editor.</span></span> 
   
    ![Aprire un file di modello dei contatti][open-contact-model-file]
2. <span data-ttu-id="0a8f1-138">Aggiungere il costruttore seguente alla classe **Contact**.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-138">Add the following constructor within the **Contact** class.</span></span> 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. <span data-ttu-id="0a8f1-139">Aprire il file di implementazione del servizio *ContactsApiServiceImpl.java* incluso nella cartella *src/main/java/io/swagger/api/impl* usando [Visual Studio Code] o l'editor di testo preferito.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-139">Open the *ContactsApiServiceImpl.java* service implementation file, which is located in the *src/main/java/io/swagger/api/impl* folder, using [Visual Studio Code] or your favorite text editor.</span></span>
   
    ![Aprire il file del codice di servizio dei contatti][open-contact-service-code-file]
4. <span data-ttu-id="0a8f1-141">Sovrascrivere il codice del file con questo nuovo codice per aggiungere un'implementazione fittizia al codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-141">Overwrite the code in the file with this new code to add a mock implementation to the service code.</span></span> 
   
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
5. <span data-ttu-id="0a8f1-142">Aprire il prompt dei comandi e passare alla cartella radice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-142">Open a command prompt and change directory to the root folder of your application.</span></span>
6. <span data-ttu-id="0a8f1-143">Eseguire il comando Maven seguente per compilare il codice ed eseguirlo in locale tramite il server di app Jetty.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-143">Execute the following Maven command to build the code and run it using the Jetty app server locally.</span></span> 
   
        mvn package jetty:run
7. <span data-ttu-id="0a8f1-144">Dovrebbe essere visualizzata la finestra di comando in cui si specifica che Jetty ha avviato il codice sulla porta 8080.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-144">You should see the command window reflect that Jetty has started your code on port 8080.</span></span> 
   
    ![Aprire il file del codice di servizio dei contatti][run-jetty-war]
8. <span data-ttu-id="0a8f1-146">Usare [Postman] per effettuare una richiesta al metodo API "ottieni tutti i contatti" in http://localhost:8080/api/contacts.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-146">Use [Postman] to make a request to the "get all contacts" API method at http://localhost:8080/api/contacts.</span></span>
   
    ![Chiamare l'API dei contatti][calling-contacts-api]
9. <span data-ttu-id="0a8f1-148">Usare [Postman] per effettuare una richiesta al metodo API "ottieni tutti i contatti" in http://localhost:8080/api/contacts/2.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-148">Use [Postman] to make a request to the "get specific contact" API method located at http://localhost:8080/api/contacts/2.</span></span>
   
    ![Chiamare l'API dei contatti][calling-specific-contact-api]
10. <span data-ttu-id="0a8f1-150">Compilare infine il file Java WAR (Web ARchive) eseguendo il seguente comando Maven nella console.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-150">Finally, build the Java WAR (Web ARchive) file by executing the following Maven command in your console.</span></span> 
    
         mvn package war:war
11. <span data-ttu-id="0a8f1-151">Una volta creato, il file WAR verrà inserito nella cartella di **destinazione**.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-151">Once the WAR file is built, it will be placed into the **target** folder.</span></span> <span data-ttu-id="0a8f1-152">Passare alla cartella di **destinazione** e rinominare il file WAR **ROOT.war**,</span><span class="sxs-lookup"><span data-stu-id="0a8f1-152">Navigate into the **target** folder and rename the WAR file to **ROOT.war**.</span></span> <span data-ttu-id="0a8f1-153">accertandosi di rispettare le lettere maiuscole.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-153">(Make sure the capitalization matches this format).</span></span>
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. <span data-ttu-id="0a8f1-154">Eseguire infine i comandi seguenti dalla cartella radice dell'applicazione per creare una cartella di **distribuzione** da usare per distribuire il file WAR in Azure.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-154">Finally, execute the following commands from the root folder of your application to create a **deploy** folder to use to deploy the WAR file to Azure.</span></span> 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-the-output-to-azure-app-service"></a><span data-ttu-id="0a8f1-155">Pubblicare l'output nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="0a8f1-155">Publish the output to Azure App Service</span></span>
<span data-ttu-id="0a8f1-156">Questa sezione descrive come creare una nuova app per le API tramite il portale di Azure, preparare l'app per le API per l'hosting di applicazioni Java e distribuire il file WAR appena creato nel servizio app di Azure per eseguire la nuova app per le API.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-156">In this section you'll learn how to create a new API App using the Azure Portal, prepare that API App for hosting Java applications, and deploy the newly-created WAR file to Azure App Service to run your new API App.</span></span> 

1. <span data-ttu-id="0a8f1-157">Creare una nuova app per le API nel [Portale di Azure]. A tale scopo, fare clic sulla voce di menu **Nuovo -> Web e dispositivi mobili -> API App**, immettere i dettagli dell'app e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-157">Create a new API app in the [Azure portal], by clicking the **New -> Web + Mobile -> API app** menu item, entering your app details, and then clicking **Create**.</span></span>
   
    ![Creare una nuova app per le API][create-api-app]
2. <span data-ttu-id="0a8f1-159">Dopo aver creato l'app per le API, aprire il pannello **Impostazioni** dell'app e quindi fare clic sulla voce di menu **Impostazioni dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-159">Once your API app has been created, open your app's **Settings** blade, and then click the **Application settings** menu item.</span></span> <span data-ttu-id="0a8f1-160">Selezionare le versioni più recenti di Java nelle opzioni disponibili e quindi la versione più recente di Tomcat nel menu **Contenitore Web** e infine fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-160">Select the latest Java versions from the available options, then select the latest Tomcat from the **Web container** menu, and then click **Save**.</span></span>
   
    ![Configurare Java nel pannello dell'app per le API][set-up-java]
3. <span data-ttu-id="0a8f1-162">Fare clic sulla voce di menu delle impostazioni **Credenziali per la distribuzione** e specificare il nome utente e la password da usare per la pubblicazione dei file nell'app per le API.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-162">Click the **Deployment credentials** settings menu item, and provide a username and password you wish to use for publishing files to your API App.</span></span> 
   
    ![Reimpostare le credenziali di distribuzione][deployment-credentials]
4. <span data-ttu-id="0a8f1-164">Fare clic sulla voce di menu delle impostazioni **Origine distribuzione** .</span><span class="sxs-lookup"><span data-stu-id="0a8f1-164">Click the **Deployment source** settings menu item.</span></span> <span data-ttu-id="0a8f1-165">Fare quindi clic sul pulsante **Scegliere l'origine**, selezionare l'opzione **Local Git Repository** e infine fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-165">Once there, click the **Choose source** button, select the **Local Git Repository** option, and then click **OK**.</span></span> <span data-ttu-id="0a8f1-166">Verrà creato un repository Git in esecuzione in Azure, contenente un'associazione con l'app per le API.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-166">This will create a Git repository running in Azure, that has an association with your API App.</span></span> <span data-ttu-id="0a8f1-167">Ogni volta che si esegue il commit di un codice nel ramo *master* del repository Git, il codice verrà pubblicato nell'istanza dell'app per le API in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-167">Each time you commit code to the *master* branch of your Git repository, your code will be published into your live running API App instance.</span></span> 
   
    ![Configurare un nuovo repository Git locale][select-git-repo]
5. <span data-ttu-id="0a8f1-169">Copiare negli appunti l'URL del nuovo repository Git.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-169">Copy the new Git repository's URL to your clipboard.</span></span> <span data-ttu-id="0a8f1-170">Salvare il file, poiché risulterà di grande importanza più avanti.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-170">Save this as it will be important in a moment.</span></span> 
   
    ![Configurare un nuovo repository Git per l'app][copy-git-repo-url]
6. <span data-ttu-id="0a8f1-172">Eseguire il push GIT del file WAR nel repository online.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-172">Git push the WAR file to the online repository.</span></span> <span data-ttu-id="0a8f1-173">A tale scopo, passare alla cartella di **distribuzione** creata in precedenza, in modo da poter facilmente eseguire il commit del codice nel repository in cui è in esecuzione il servizio app.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-173">To do this, navigate into the **deploy** folder you created earlier so that you can easily commit the code up to the repository running in your App Service.</span></span> <span data-ttu-id="0a8f1-174">Dopo aver attivato la finestra della console ed essersi spostati nella directory in cui si trova la cartella webapps, inviare i comandi Git seguenti per avviare il processo e attivare una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-174">Once you're in the console window and navigated into the folder where the webapps folder is located, issue the following Git commands to launch the process and fire off a deployment.</span></span> 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    <span data-ttu-id="0a8f1-175">Dopo aver emesso la richiesta di **push** , viene richiesta la password creata in precedenza per le credenziali di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-175">Once you issue the **push** request, you'll be asked for the password you created for the deployment credential earlier.</span></span> <span data-ttu-id="0a8f1-176">Dopo l'immissione delle credenziali, nel portale dovrebbe essere visualizzata la distribuzione dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-176">After you enter your credentials, you should see your portal display that the update was deployed.</span></span>
7. <span data-ttu-id="0a8f1-177">Se si accede alla nuova app per le API in esecuzione nel servizio app di Azure con Postman, si noterà che il comportamento è coerente, che ora restituisce i dati dei contatti previsti e, tramite un semplice codice, si trasforma in codice Java sottoposto a scaffolding da Swagger.io.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-177">If you once again use Postman to hit the newly-deployed API App running in Azure App Service, you'll see that the behavior is consistent and that now it is returning contact data as expected, and using simple code changes to the Swagger.io scaffolded Java code.</span></span> 
   
    ![Usare l'API REST dei contatti Java in Azure][postman-calling-azure-contacts]

## <a name="next-steps"></a><span data-ttu-id="0a8f1-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0a8f1-179">Next steps</span></span>
<span data-ttu-id="0a8f1-180">Questo articolo è iniziato con un file JSON Swagger e il codice Java sottoposto a scaffolding ottenuto dall'editor Swagger.io.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-180">In this article, you were able to start with a Swagger JSON file and some scaffolded Java code obtained from the Swagger.io editor.</span></span> <span data-ttu-id="0a8f1-181">Con alcune modifiche e un processo di distribuzione di un repository Git è stata creata un'app per le API funzionale, scritta in Java.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-181">From there, your simple changes and a Git deploy process resulted in having a functional API app written in Java.</span></span> <span data-ttu-id="0a8f1-182">L'esercitazione successiva mostra come [utilizzare app per le API da client JavaScript tramite CORS][App Service API CORS].</span><span class="sxs-lookup"><span data-stu-id="0a8f1-182">The next tutorial shows how to [consume API apps from JavaScript clients, using CORS][App Service API CORS].</span></span> <span data-ttu-id="0a8f1-183">Le esercitazioni successive della serie illustrano come implementare l'autenticazione e l'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-183">Later tutorials in the series show how to implement authentication and authorization.</span></span>

<span data-ttu-id="0a8f1-184">Per approfondire questo esempio, è possibile acquisire informazioni su [Storage SDK per Java] per rendere permanenti i BLOB JSON.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-184">To build on this sample, you can learn more about the [Storage SDK for Java] to persist the JSON blobs.</span></span> <span data-ttu-id="0a8f1-185">In alternativa, è possibile usare [DocumentDB Java SDK] per salvare i dati dei contatti in Azure DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="0a8f1-185">Or, you could use the [Document DB Java SDK] to save your Contact data to Azure Document DB.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="0a8f1-186">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0a8f1-186">See Also</span></span>
<span data-ttu-id="0a8f1-187">Per altre informazioni sull'uso di Azure con Java, vedere [Azure for Java developers](/java/azure) (Azure per sviluppatori Java).</span><span class="sxs-lookup"><span data-stu-id="0a8f1-187">For more information about using Azure with Java, visit [Azure for Java developers](/java/azure).</span></span>

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[Portale di Azure]: https://portal.azure.com/
[DocumentDB Java SDK]: ../documentdb/documentdb-java-application.md
[valutazione gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Java Development Kit 8]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[Jax-RS]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[editor Swagger online]: http://editor2.swagger.io/
[Postman]: https://www.getpostman.com/
[Storage SDK per Java]:../storage/blobs/storage-java-how-to-use-blob-storage.md
[Swagger]: http://swagger.io/
[editor Swagger]: http://editor.swagger.io/
[Visual Studio Code]: https://code.visualstudio.com

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
