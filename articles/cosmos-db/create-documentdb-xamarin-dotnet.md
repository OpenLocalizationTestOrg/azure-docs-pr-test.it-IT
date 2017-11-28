---
title: 'Azure Cosmos DB: Creare un''app Web con Xamarin e l''autenticazione di Facebook | Microsoft Docs'
description: "Visualizza un esempio di codice .NET è possibile utilizzare tooconnect tooand query Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a><span data-ttu-id="7dd9b-103">Azure Cosmos DB: Creare un'app Web con .NET, Xamarin e l'autenticazione di Facebook</span><span class="sxs-lookup"><span data-stu-id="7dd9b-103">Azure Cosmos DB: Build a web app with .NET, Xamarin, and Facebook authentication</span></span>

<span data-ttu-id="7dd9b-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="7dd9b-105">Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="7dd9b-106">Questa Guida introduttiva viene illustrato come un account Azure Cosmos DB toocreate, database di documenti e l'utilizzo di raccolta hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="7dd9b-107">Verrà quindi compilare e distribuire un'app web di elenco todo basata su hello [API .NET di DocumentDB](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/)e il motore di autorizzazione hello Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), and hello Azure Cosmos DB authorization engine.</span></span> <span data-ttu-id="7dd9b-108">app web di elenco attività Hello implementa un modello di dati per ogni utente che consente agli utenti toologin utilizzando Facebook Auth e gestire i propri elementi toodo.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-108">hello todo list web app implements a per-user data pattern that enables users toologin using Facebook Auth and manage their own toodo items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7dd9b-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7dd9b-109">Prerequisites</span></span>

<span data-ttu-id="7dd9b-110">Se si dispone già di Visual Studio 2017, che installata, è possibile scaricare e utilizzare hello **libero** [2017 di Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7dd9b-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="7dd9b-111">Assicurarsi di abilitare **lo sviluppo di Azure** durante l'installazione di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="7dd9b-112">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="7dd9b-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="7dd9b-113">Aggiungere una raccolta</span><span class="sxs-lookup"><span data-stu-id="7dd9b-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="7dd9b-114">Applicazione di esempio hello clonare</span><span class="sxs-lookup"><span data-stu-id="7dd9b-114">Clone hello sample application</span></span>

<span data-ttu-id="7dd9b-115">Ora si app clone un'API DocumentDB da github, impostare la stringa di connessione hello ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="7dd9b-116">Si noterà quanto sia facile toowork con i dati a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-116">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="7dd9b-117">Aprire una finestra terminale git, ad esempio git bash, e `cd` tooa directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-117">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="7dd9b-118">Eseguire hello seguenti repository di esempio di comando tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. <span data-ttu-id="7dd9b-119">Aprire hello DocumentDBTodo.sln file dalla cartella samples/xamarin/UserItems/xamarin.forms hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-119">Then open hello DocumentDBTodo.sln file from hello samples/xamarin/UserItems/xamarin.forms folder in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="7dd9b-120">Esaminare il codice hello</span><span class="sxs-lookup"><span data-stu-id="7dd9b-120">Review hello code</span></span>

<span data-ttu-id="7dd9b-121">codice Hello nella cartella Xamarin hello contiene:</span><span class="sxs-lookup"><span data-stu-id="7dd9b-121">hello code in hello Xamarin folder contains:</span></span>

* <span data-ttu-id="7dd9b-122">App Xamarin.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-122">Xamarin app.</span></span> <span data-ttu-id="7dd9b-123">applicazione Hello Archivia elementi di attività dell'utente hello in una raccolta partizionata denominata UserItems.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-123">hello app stores hello user's todo items in a partitioned collection named UserItems.</span></span>
* <span data-ttu-id="7dd9b-124">API del gestore di token di risorsa.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-124">Resource token broker API.</span></span> <span data-ttu-id="7dd9b-125">Una risorsa di Azure Cosmos DB toobroker API Web ASP.NET semplice token toohello gli utenti dell'applicazione hello connesso.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-125">A simple ASP.NET Web API toobroker Azure Cosmos DB resource tokens toohello logged in users of hello app.</span></span> <span data-ttu-id="7dd9b-126">I token di risorsa sono token di accesso di breve durata che forniscono app hello hello accesso toohello registrato nei dati dell'utente.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-126">Resource tokens are short-lived access tokens that provide hello app with hello access toohello logged in user's data.</span></span>

<span data-ttu-id="7dd9b-127">flusso di dati e l'autenticazione Hello è illustrato nel diagramma hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-127">hello authentication and data flow is illustrated in hello diagram below.</span></span>

* <span data-ttu-id="7dd9b-128">Hello UserItems raccolta viene creato con la chiave di partizione hello ' / userid'.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-128">hello UserItems collection is created with hello partition key '/userid'.</span></span> <span data-ttu-id="7dd9b-129">Specifica che una chiave di partizione per una raccolta consente all'infinito tooscale Azure Cosmos DB come numero hello di utenti ed elementi aumenta.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-129">Specifying a partition key for a collection allows Azure Cosmos DB tooscale infinitely as hello number of users and items grows.</span></span>
* <span data-ttu-id="7dd9b-130">app Xamarin Hello consente toologin gli utenti con credenziali di Facebook.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-130">hello Xamarin app allows users toologin with Facebook credentials.</span></span>
* <span data-ttu-id="7dd9b-131">app Xamarin Hello utilizza l'API ResourceTokenBroker tooauthenticate token di accesso Facebook</span><span class="sxs-lookup"><span data-stu-id="7dd9b-131">hello Xamarin app uses Facebook access token tooauthenticate with ResourceTokenBroker API</span></span>
* <span data-ttu-id="7dd9b-132">gestore di token Hello risorsa API autentica hello richiesta utilizzando la funzionalità di autenticazione del servizio App e richiede un token di risorsa di Azure Cosmos DB con i documenti tooall di accesso in lettura/scrittura condivisione chiave di partizione dell'utente autenticato hello.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-132">hello resource token broker API authenticates hello request using App Service Auth feature, and requests an Azure Cosmos DB resource token with read/write access tooall documents sharing hello authenticated user's partition key.</span></span>
* <span data-ttu-id="7dd9b-133">Gestore di token di risorsa restituisce hello risorsa toohello token client app.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-133">Resource token broker returns hello resource token toohello client app.</span></span>
* <span data-ttu-id="7dd9b-134">app Hello accede agli elementi di attività dell'utente hello utilizzando il token di risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-134">hello app accesses hello user's todo items using hello resource token.</span></span>

![App elenco attività con dati di esempio](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a><span data-ttu-id="7dd9b-136">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="7dd9b-136">Update your connection string</span></span>

<span data-ttu-id="7dd9b-137">Tornare toohello tooget portale Azure le informazioni sulla stringa di connessione e copiarla in app hello.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-137">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="7dd9b-138">In hello [portale di Azure](http://portal.azure.com/)il Cosmos Azure DB account, nel riquadro di spostamento sinistro hello fare clic su **chiavi**, quindi fare clic su **le chiavi di lettura / scrittura**.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-138">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="7dd9b-139">Utilizzare i pulsanti di hello copia sul lato destro hello di hello toocopy di hello schermata URI e chiave primaria nel file Web. config hello nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-139">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello Web.config file in hello next step.</span></span>

    ![Visualizzare e copiare una chiave di accesso nel portale di Azure hello, pannello di chiavi](./media/create-documentdb-xamarin-dotnet/keys.png)

2. <span data-ttu-id="7dd9b-141">In Visual Studio 2017, aprire il file Web. config hello nella cartella di azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker hello.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-141">In Visual Studio 2017, open hello Web.config file in hello azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker folder.</span></span> 

3. <span data-ttu-id="7dd9b-142">Copiare il valore dell'URI dal portale di hello (con il pulsante di copia hello) e renderlo hello valore accountUrl hello in Web. config.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-142">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello accountUrl in Web.config.</span></span> 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. <span data-ttu-id="7dd9b-143">Quindi copiare il valore di chiave primaria dal portale di hello e renderlo hello valore accountKey hello in Web.congif.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-143">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello accountKey in Web.congif.</span></span> 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

<span data-ttu-id="7dd9b-144">È stato aggiornato a questo punto l'app con tutte le informazioni di hello deve toocommunicate con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-144">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="build-and-deploy-hello-web-app"></a><span data-ttu-id="7dd9b-145">Compilare e distribuire l'app web hello</span><span class="sxs-lookup"><span data-stu-id="7dd9b-145">Build and deploy hello web app</span></span>

1. <span data-ttu-id="7dd9b-146">Nel portale di Azure hello, creare una servizio App sito Web toohost hello risorse token broker API.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-146">In hello Azure portal, create an App Service website toohost hello Resource token broker API.</span></span>
2. <span data-ttu-id="7dd9b-147">Nel portale di Azure hello, aprire il pannello Impostazioni applicazione hello del gestore di token hello risorsa sito Web API.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-147">In hello Azure portal, open hello App Settings blade of hello Resource token broker API website.</span></span> <span data-ttu-id="7dd9b-148">Compilare hello seguendo le impostazioni dell'app:</span><span class="sxs-lookup"><span data-stu-id="7dd9b-148">Fill in hello following app settings:</span></span>

    * <span data-ttu-id="7dd9b-149">accountUrl - URL di account Azure Cosmos DB hello dalla scheda di hello chiavi dell'account di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-149">accountUrl - hello Azure Cosmos DB account URL from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="7dd9b-150">accountKey - chiave master dell'account Azure Cosmos DB hello dalla scheda chiavi hello dell'account di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-150">accountKey - hello Azure Cosmos DB account master key from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="7dd9b-151">Valori di databaseId e collectionId del database e della raccolta creati</span><span class="sxs-lookup"><span data-stu-id="7dd9b-151">databaseId and collectionId of your created database and collection</span></span>

3. <span data-ttu-id="7dd9b-152">Pubblicare hello ResourceTokenBroker soluzione tooyour creato sito Web.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-152">Publish hello ResourceTokenBroker solution tooyour created website.</span></span>

4. <span data-ttu-id="7dd9b-153">Aprire il progetto di Xamarin hello e passare tooTodoItemManager.cs.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-153">Open hello Xamarin project, and navigate tooTodoItemManager.cs.</span></span> <span data-ttu-id="7dd9b-154">Specificare i valori hello per accountURL, collectionId, databaseId, così come resourceTokenBrokerURL come hello url di base https per il sito Web di Service broker token risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-154">Fill in hello values for accountURL, collectionId, databaseId, as well as resourceTokenBrokerURL as hello base https url for hello resource token broker website.</span></span>

5. <span data-ttu-id="7dd9b-155">Hello completo [come tooconfigure l'account di accesso Facebook di toouse applicazione di servizio App](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) toosetup esercitazione l'autenticazione di Facebook e configurare sito Web ResourceTokenBroker hello.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-155">Complete hello [How tooconfigure your App Service application toouse Facebook login](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) tutorial toosetup Facebook authentication and configure hello ResourceTokenBroker website.</span></span>

    <span data-ttu-id="7dd9b-156">Eseguire app Xamarin hello.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-156">Run hello Xamarin app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="7dd9b-157">Esaminare i contratti di servizio nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="7dd9b-157">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="7dd9b-158">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="7dd9b-158">Clean up resources</span></span>

<span data-ttu-id="7dd9b-159">Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa Guida rapida hello portale di Azure con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7dd9b-159">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="7dd9b-160">Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-160">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you just created.</span></span> 
2. <span data-ttu-id="7dd9b-161">Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-161">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7dd9b-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7dd9b-162">Next steps</span></span>

<span data-ttu-id="7dd9b-163">In questa Guida rapida, si è appreso come toocreate un account Azure Cosmos DB, creare una raccolta utilizzando Esplora dati, hello e compilare e distribuire un'app Xamarin.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-163">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and build and deploy a Xamarin app.</span></span> <span data-ttu-id="7dd9b-164">È ora possibile importare account Cosmos DB tooyour di dati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="7dd9b-164">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="7dd9b-165">Importare dati in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7dd9b-165">Import data into Azure Cosmos DB</span></span>](import-data.md)
