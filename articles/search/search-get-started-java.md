---
title: aaaGet avviato con ricerca di Azure in Java | Documenti Microsoft
description: Un cloud ospitato toobuild ricerca come applicazione in Azure con Java come linguaggio di programmazione.
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a><span data-ttu-id="17a87-103">Introduzione a Ricerca di Azure in Java</span><span class="sxs-lookup"><span data-stu-id="17a87-103">Get started with Azure Search in Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="17a87-104">Portale</span><span class="sxs-lookup"><span data-stu-id="17a87-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="17a87-105">.NET</span><span class="sxs-lookup"><span data-stu-id="17a87-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="17a87-106">Informazioni su come un linguaggio personalizzato toobuild ricerca applicazione che utilizza la ricerca di Azure per la sua esperienza di ricerca.</span><span class="sxs-lookup"><span data-stu-id="17a87-106">Learn how toobuild a custom Java search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="17a87-107">Questa esercitazione viene utilizzato hello [API REST di Azure ricerca](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello oggetti e operazioni in questo esercizio.</span><span class="sxs-lookup"><span data-stu-id="17a87-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="17a87-108">toorun in questo esempio, è necessario un servizio di ricerca di Azure, che è possibile iscriversi a in hello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="17a87-108">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="17a87-109">Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per istruzioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="17a87-109">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

<span data-ttu-id="17a87-110">È utilizzato hello seguente toobuild software e di test in questo esempio:</span><span class="sxs-lookup"><span data-stu-id="17a87-110">We used hello following software toobuild and test this sample:</span></span>

* <span data-ttu-id="17a87-111">[Eclipse IDE per sviluppatori Java EE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span><span class="sxs-lookup"><span data-stu-id="17a87-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span></span> <span data-ttu-id="17a87-112">Essere certi toodownload hello EE versione.</span><span class="sxs-lookup"><span data-stu-id="17a87-112">Be sure toodownload hello EE version.</span></span> <span data-ttu-id="17a87-113">Uno dei passaggi di verifica hello richiede una funzionalità che è disponibile solo in questa edizione.</span><span class="sxs-lookup"><span data-stu-id="17a87-113">One of hello verification steps requires a feature that is found only in this edition.</span></span>
* [<span data-ttu-id="17a87-114">JDK 8u40</span><span class="sxs-lookup"><span data-stu-id="17a87-114">JDK 8u40</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [<span data-ttu-id="17a87-115">Apache Tomcat 8.0</span><span class="sxs-lookup"><span data-stu-id="17a87-115">Apache Tomcat 8.0</span></span>](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a><span data-ttu-id="17a87-116">Informazioni sui dati hello</span><span class="sxs-lookup"><span data-stu-id="17a87-116">About hello data</span></span>
<span data-ttu-id="17a87-117">Questa applicazione di esempio utilizza i dati di hello [Italia geologiche servizi (USG)](http://geonames.usgs.gov/domestic/download_data.htm)filtro sulle dimensioni di hello lo stato di Rhode Island tooreduce hello set di dati.</span><span class="sxs-lookup"><span data-stu-id="17a87-117">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="17a87-118">Verrà utilizzata questa toobuild dati un'applicazione di ricerca che restituisce gli edifici punti di riferimento, ad esempio ospedale un numero e scuole, nonché funzionalità geologiche come flussi e laghi Summit.</span><span class="sxs-lookup"><span data-stu-id="17a87-118">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="17a87-119">In questa applicazione hello **SearchServlet.java** programma compila e carica hello indice utilizzando un [indicizzatore](https://msdn.microsoft.com/library/azure/dn798918.aspx) costrutto, recupero hello filtrati soltanto set di dati da un Database SQL di Azure pubblico.</span><span class="sxs-lookup"><span data-stu-id="17a87-119">In this application, hello **SearchServlet.java** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="17a87-120">Le credenziali predefinite e l'origine dati online toohello informazioni di connessione sono incluse nel codice programma hello.</span><span class="sxs-lookup"><span data-stu-id="17a87-120">Predefined credentials and connection  information toohello online data source are provided in hello program code.</span></span> <span data-ttu-id="17a87-121">In termini di accesso ai dati, non è necessaria alcuna ulteriore configurazione.</span><span class="sxs-lookup"><span data-stu-id="17a87-121">In terms of data access, no further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="17a87-122">In questo set di dati toostay in limite dei documenti di hello disponibile a livello di prezzo 10.000 hello è stato applicato un filtro.</span><span class="sxs-lookup"><span data-stu-id="17a87-122">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="17a87-123">Se si utilizza il livello standard di hello, questo limite non si applica ed è possibile modificare questo toouse di codice un set di dati più grande.</span><span class="sxs-lookup"><span data-stu-id="17a87-123">If you use hello standard tier, this limit does not apply, and you can modify this code toouse a bigger dataset.</span></span> <span data-ttu-id="17a87-124">Per ulteriori informazioni sulla capacità per ogni livello di prezzo, vedere [Limiti e vincoli](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="17a87-124">For details about capacity for each pricing tier, see [Limits and constraints](search-limits-quotas-capacity.md).</span></span>
> 
> 

## <a name="about-hello-program-files"></a><span data-ttu-id="17a87-125">Informazioni sui file di programma hello</span><span class="sxs-lookup"><span data-stu-id="17a87-125">About hello program files</span></span>
<span data-ttu-id="17a87-126">Hello elenco seguente vengono descritti i file hello esempio toothis pertinente.</span><span class="sxs-lookup"><span data-stu-id="17a87-126">hello following list describes hello files that are relevant toothis sample.</span></span>

* <span data-ttu-id="17a87-127">Search.jsp: Fornisce l'interfaccia utente di hello</span><span class="sxs-lookup"><span data-stu-id="17a87-127">Search.jsp: Provides hello user interface</span></span>
* <span data-ttu-id="17a87-128">SearchServlet.java: Fornisce i metodi (simile tooa controller MVC)</span><span class="sxs-lookup"><span data-stu-id="17a87-128">SearchServlet.java: Provides methods (similar tooa controller in MVC)</span></span>
* <span data-ttu-id="17a87-129">SearchServiceClient.java: gestisce le richieste HTTP </span><span class="sxs-lookup"><span data-stu-id="17a87-129">SearchServiceClient.java: Handles HTTP requests</span></span>
* <span data-ttu-id="17a87-130">SearchServiceHelper.java: una classe di supporto che fornisce metodi statici</span><span class="sxs-lookup"><span data-stu-id="17a87-130">SearchServiceHelper.java: A helper class that provides static methods</span></span>
* <span data-ttu-id="17a87-131">Document.Java: Fornisce il modello di dati di hello</span><span class="sxs-lookup"><span data-stu-id="17a87-131">Document.java: Provides hello data model</span></span>
* <span data-ttu-id="17a87-132">config.Properties: imposta l'URL del servizio di ricerca hello e la chiave api</span><span class="sxs-lookup"><span data-stu-id="17a87-132">config.properties: Sets hello Search service URL and api-key</span></span>
* <span data-ttu-id="17a87-133">Pom.xml: una dipendenza Maven</span><span class="sxs-lookup"><span data-stu-id="17a87-133">Pom.xml: A Maven dependency</span></span>

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="17a87-134">Trovare il nome del servizio hello e la chiave api del servizio di ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="17a87-134">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="17a87-135">Tutte le chiamate API REST in ricerca di Azure è necessario disporre URL del servizio hello e una chiave api.</span><span class="sxs-lookup"><span data-stu-id="17a87-135">All REST API calls into Azure Search require that you provide hello service URL and an api-key.</span></span> 

1. <span data-ttu-id="17a87-136">Accedi toohello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="17a87-136">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="17a87-137">Nella barra di spostamento hello, fare clic su **servizio di ricerca** toolist tutti i servizi di ricerca di Azure hello effettuato il provisioning per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="17a87-137">In hello jump bar, click **Search service** toolist all of hello Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="17a87-138">Selezionare servizio hello da toouse.</span><span class="sxs-lookup"><span data-stu-id="17a87-138">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="17a87-139">Nel dashboard del servizio hello, si noterà riquadri per informazioni essenziali e icona per l'accesso alle chiavi amministratore hello hello.</span><span class="sxs-lookup"><span data-stu-id="17a87-139">On hello service dashboard, you'll see tiles for essential information as well as hello key icon for accessing hello admin keys.</span></span>
   
      ![][3]
5. <span data-ttu-id="17a87-140">Copiare l'URL del servizio hello e una chiave amministratore.</span><span class="sxs-lookup"><span data-stu-id="17a87-140">Copy hello service URL and an admin key.</span></span> <span data-ttu-id="17a87-141">Saranno necessari in un secondo momento, quando vengono aggiunte toohello **config.properties** file.</span><span class="sxs-lookup"><span data-stu-id="17a87-141">You will need them later, when you add them toohello **config.properties** file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="17a87-142">Scaricare i file di esempio hello</span><span class="sxs-lookup"><span data-stu-id="17a87-142">Download hello sample files</span></span>
1. <span data-ttu-id="17a87-143">Andare troppo[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="17a87-143">Go too[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) on GitHub.</span></span>
2. <span data-ttu-id="17a87-144">Fare clic su **ZIP di Download**, salvare toodisk di file con estensione zip hello e quindi estrarre tutti i file hello in esso contenuti.</span><span class="sxs-lookup"><span data-stu-id="17a87-144">Click **Download ZIP**, save hello .zip file toodisk, and then extract all hello files it contains.</span></span> <span data-ttu-id="17a87-145">Prendere in considerazione l'estrazione hello di file in toomake di area di lavoro del linguaggio è più semplice progetto di hello toofind in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="17a87-145">Consider extracting hello files into your Java workspace toomake it easier toofind hello project later.</span></span>
3. <span data-ttu-id="17a87-146">file di esempio Hello sono di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="17a87-146">hello sample files are read-only.</span></span> <span data-ttu-id="17a87-147">Fare clic sulla proprietà della cartella e attributo di sola lettura non crittografato hello.</span><span class="sxs-lookup"><span data-stu-id="17a87-147">Right-click folder properties and clear hello read-only attribute.</span></span>

<span data-ttu-id="17a87-148">Tutte le successive modifiche e le istruzioni di esecuzione verranno effettuate sui file in questa cartella.</span><span class="sxs-lookup"><span data-stu-id="17a87-148">All subsequent file modifications and run statements will be made against files in this folder.</span></span>  

## <a name="import-project"></a><span data-ttu-id="17a87-149">Importare il progetto</span><span class="sxs-lookup"><span data-stu-id="17a87-149">Import project</span></span>
1. <span data-ttu-id="17a87-150">In Eclipse scegliere **File** > **Importa** > **Generale** >  **Progetti esistenti nell'area di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="17a87-150">In Eclipse, choose **File** > **Import** > **General** > **Existing Projects into Workspace**.</span></span>
   
    ![][4]
2. <span data-ttu-id="17a87-151">In **directory principale selezionare**, toohello cartella contenente file di esempio.</span><span class="sxs-lookup"><span data-stu-id="17a87-151">In **Select root directory**, browse toohello folder containing sample files.</span></span> <span data-ttu-id="17a87-152">Selezionare la cartella hello che contiene una cartella di hello. Project.</span><span class="sxs-lookup"><span data-stu-id="17a87-152">Select hello folder that contains hello .project folder.</span></span> <span data-ttu-id="17a87-153">progetto Hello dovrebbe essere visualizzati in hello **progetti** elenco come un elemento selezionato.</span><span class="sxs-lookup"><span data-stu-id="17a87-153">hello project should appear in hello **Projects** list as a selected item.</span></span>
   
    ![][12]
3. <span data-ttu-id="17a87-154">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="17a87-154">Click **Finish**.</span></span>
4. <span data-ttu-id="17a87-155">Utilizzare **Esplora progetti** tooview e modificare file hello.</span><span class="sxs-lookup"><span data-stu-id="17a87-155">Use **Project Explorer** tooview and edit hello files.</span></span> <span data-ttu-id="17a87-156">Se non è già aperto, fare clic su **finestra** > **Mostra visualizzazione** > **Esplora progetti** o utilizzare tooopen di scelta rapida hello è.</span><span class="sxs-lookup"><span data-stu-id="17a87-156">If it's not already open, click **Window** > **Show View** > **Project Explorer** or use hello shortcut tooopen it.</span></span>

## <a name="configure-hello-service-url-and-api-key"></a><span data-ttu-id="17a87-157">Configurare l'URL del servizio hello e la chiave api</span><span class="sxs-lookup"><span data-stu-id="17a87-157">Configure hello service URL and api-key</span></span>
1. <span data-ttu-id="17a87-158">In **Esplora progetti**, fare doppio clic su **config.properties** tooedit le impostazioni di configurazione hello contenente il nome di server hello e la chiave api.</span><span class="sxs-lookup"><span data-stu-id="17a87-158">In **Project Explorer**, double-click **config.properties** tooedit hello configuration settings containing hello server name and api-key.</span></span>
2. <span data-ttu-id="17a87-159">Fare riferimento toohello passaggi più indietro in questo articolo, in cui è possibile trovare hello URL del servizio e la chiave api in hello [portale Azure](https://portal.azure.com), i valori hello tooget ora immetterà **config.properties**.</span><span class="sxs-lookup"><span data-stu-id="17a87-159">Refer toohello steps earlier in this article, where you found hello service URL and api-key in hello [Azure Portal](https://portal.azure.com), tooget hello values you will now enter into **config.properties**.</span></span>
3. <span data-ttu-id="17a87-160">In **config.properties**, sostituire "Chiave Api" con hello chiave api per il servizio.</span><span class="sxs-lookup"><span data-stu-id="17a87-160">In **config.properties**, replace "Api Key" with hello api-key for your service.</span></span> <span data-ttu-id="17a87-161">Successivamente, il nome del servizio (hello primo componente del hello URL http://servicename.search.windows.net) sostituisce la "nome del servizio" hello stesso file.</span><span class="sxs-lookup"><span data-stu-id="17a87-161">Next, service name (hello first component of hello URL http://servicename.search.windows.net) replaces "service name" in hello same file.</span></span>
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a><span data-ttu-id="17a87-162">Configurare gli ambienti di progetto, compilazione e runtime hello</span><span class="sxs-lookup"><span data-stu-id="17a87-162">Configure hello project, build and runtime environments</span></span>
1. <span data-ttu-id="17a87-163">In Project Explorer di Eclipse fare clic sul progetto hello > **proprietà** > **facet progetto**.</span><span class="sxs-lookup"><span data-stu-id="17a87-163">In Eclipse, in Project Explorer, right-click hello project > **Properties** > **Project Facets**.</span></span>
2. <span data-ttu-id="17a87-164">Selezionare **Dynamic Web Module**, **Java** e **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="17a87-164">Select **Dynamic Web Module**, **Java**, and **JavaScript**.</span></span>
   
    ![][6]
3. <span data-ttu-id="17a87-165">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="17a87-165">Click **Apply**.</span></span>
4. <span data-ttu-id="17a87-166">Selezionare **Finestra** > **Preferenze** > **Server** > **Runtime Environments (Ambienti di runtime)** > **Aggiungi..**.</span><span class="sxs-lookup"><span data-stu-id="17a87-166">Select **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span></span>
5. <span data-ttu-id="17a87-167">Espandere Apache e selezionare la versione di hello del server Apache Tomcat hello che è installato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="17a87-167">Expand Apache and select hello version of hello Apache Tomcat server you previously installed.</span></span> <span data-ttu-id="17a87-168">In questo sistema è installata la versione 8.</span><span class="sxs-lookup"><span data-stu-id="17a87-168">On our system, we installed version 8.</span></span>
   
    ![][7]
6. <span data-ttu-id="17a87-169">Nella pagina successiva di hello, specificare directory di installazione di Tomcat hello.</span><span class="sxs-lookup"><span data-stu-id="17a87-169">On hello next page, specify hello Tomcat installation directory.</span></span> <span data-ttu-id="17a87-170">In un computer Windows, sarà probabilmente C:\Programmi\Microsoft Files\Apache Software Foundation\Tomcat *versione*.</span><span class="sxs-lookup"><span data-stu-id="17a87-170">On a Windows computer, this will most likely be C:\Program Files\Apache Software Foundation\Tomcat *version*.</span></span>
7. <span data-ttu-id="17a87-171">Fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="17a87-171">Click **Finish**.</span></span>
8. <span data-ttu-id="17a87-172">Selezionare **Finestra** > **Preferenze** > **Java** > **Installed JREs (JRE installati)** > **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="17a87-172">Select **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span></span>
9. <span data-ttu-id="17a87-173">In **Add JRE** (Aggiungi JRE) selezionare **Standard VM (VM standard)**.</span><span class="sxs-lookup"><span data-stu-id="17a87-173">In **Add JRE**, select **Standard VM**.</span></span>
10. <span data-ttu-id="17a87-174">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="17a87-174">Click **Next**.</span></span>
11. <span data-ttu-id="17a87-175">Nella definizione dell'ambiente JRE, nella home di JRE, fare clic su **Directory**.</span><span class="sxs-lookup"><span data-stu-id="17a87-175">In JRE Definition, in JRE home, click **Directory**.</span></span>
12. <span data-ttu-id="17a87-176">Passare troppo**programmi** > **Java** e selezionare hello JDK è installato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="17a87-176">Navigate too**Program Files** > **Java** and select hello JDK you previously installed.</span></span> <span data-ttu-id="17a87-177">È importante tooselect hello JDK come hello JRE.</span><span class="sxs-lookup"><span data-stu-id="17a87-177">It's important tooselect hello JDK as hello JRE.</span></span>
13. <span data-ttu-id="17a87-178">In JREs installato, scegliere hello **JDK**.</span><span class="sxs-lookup"><span data-stu-id="17a87-178">In Installed JREs, choose hello **JDK**.</span></span> <span data-ttu-id="17a87-179">Le impostazioni dovrebbero essere simile toohello seguente schermata.</span><span class="sxs-lookup"><span data-stu-id="17a87-179">Your settings should look similar toohello following screenshot.</span></span>
    
    ![][9]
14. <span data-ttu-id="17a87-180">Facoltativamente, selezionare **finestra** > **Browser Web** > **Internet Explorer** tooopen un'applicazione hello in una finestra del browser esterno.</span><span class="sxs-lookup"><span data-stu-id="17a87-180">Optionally, select **Window** > **Web Browser** > **Internet Explorer** tooopen hello application in an external browser window.</span></span> <span data-ttu-id="17a87-181">L’utilizzo di un browser esterno offre una migliore esperienza di applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="17a87-181">Using an external browser gives you a better Web application experience.</span></span>
    
    ![][8]

<span data-ttu-id="17a87-182">Attività di configurazione hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="17a87-182">You have now completed hello configuration tasks.</span></span> <span data-ttu-id="17a87-183">Successivamente, è possibile compilare ed eseguire il progetto di hello.</span><span class="sxs-lookup"><span data-stu-id="17a87-183">Next, you'll build and run hello project.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="17a87-184">Compilare il progetto hello</span><span class="sxs-lookup"><span data-stu-id="17a87-184">Build hello project</span></span>
1. <span data-ttu-id="17a87-185">In Esplora progetti, fare doppio clic su nome progetto hello e scegliere **runas** > **compilazione Maven...**  progetto hello tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="17a87-185">In Project Explorer, right-click hello project name and choose **Run As** > **Maven build...** tooconfigure hello project.</span></span>
   
    ![][10]
2. <span data-ttu-id="17a87-186">In Edit Configuration, in Goals, digitare "clean install", quindi fare clic su **Run**.</span><span class="sxs-lookup"><span data-stu-id="17a87-186">In Edit Configuration, in Goals, type "clean install", and then click **Run**.</span></span>

<span data-ttu-id="17a87-187">I messaggi di stato sono finestra della console toohello output.</span><span class="sxs-lookup"><span data-stu-id="17a87-187">Status messages are output toohello console window.</span></span> <span data-ttu-id="17a87-188">Dovrebbe essere progetto hello che indica di COMPILAZIONI COMPLETATE compilato senza errori.</span><span class="sxs-lookup"><span data-stu-id="17a87-188">You should see BUILD SUCCESS indicating hello project built without errors.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="17a87-189">Eseguire app hello</span><span class="sxs-lookup"><span data-stu-id="17a87-189">Run hello app</span></span>
<span data-ttu-id="17a87-190">In questo ultimo passaggio, si eseguirà un'applicazione hello in un ambiente di runtime del server locale.</span><span class="sxs-lookup"><span data-stu-id="17a87-190">In this last step, you will run hello application in a local server runtime environment.</span></span>

<span data-ttu-id="17a87-191">Se ancora non è stato specificato un ambiente di runtime del server in Eclipse, è necessario prima di tutto toodo.</span><span class="sxs-lookup"><span data-stu-id="17a87-191">If you haven't yet specified a server runtime environment in Eclipse, you'll need toodo that first.</span></span>

1. <span data-ttu-id="17a87-192">In Project Explorer espandere **WebContent**.</span><span class="sxs-lookup"><span data-stu-id="17a87-192">In Project Explorer, expand **WebContent**.</span></span>
2. <span data-ttu-id="17a87-193">Fare clic con il pulsante destro del mouse su **Search.jsp** > **Esegui come** > **Esegui come controllo server**.</span><span class="sxs-lookup"><span data-stu-id="17a87-193">Right-click **Search.jsp** > **Run As** > **Run on Server**.</span></span> <span data-ttu-id="17a87-194">Selezionare server Apache Tomcat hello e quindi fare clic su **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="17a87-194">Select hello Apache Tomcat server, and then click **Run**.</span></span>

> [!TIP]
> <span data-ttu-id="17a87-195">Se si utilizza un toostore non predefinito dell'area di lavoro del progetto, è necessario toomodify **Run Configuration** toopoint toohello progetto percorso tooavoid un errore di avvio del server.</span><span class="sxs-lookup"><span data-stu-id="17a87-195">If you used a non-default workspace toostore your project, you'll need toomodify **Run Configuration** toopoint toohello project location tooavoid a server start-up error.</span></span> <span data-ttu-id="17a87-196">In Esplora progetti fare clic con il pulsante destro del mouse su **Search.jsp** > **Esegui come** > **Configurazione di esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="17a87-196">In Project Explorer, right-click **Search.jsp** > **Run As** > **Run Configurations**.</span></span> <span data-ttu-id="17a87-197">Selezionare server Apache Tomcat hello.</span><span class="sxs-lookup"><span data-stu-id="17a87-197">Select hello Apache Tomcat server.</span></span> <span data-ttu-id="17a87-198">Fare clic su **Arguments**.</span><span class="sxs-lookup"><span data-stu-id="17a87-198">Click **Arguments**.</span></span> <span data-ttu-id="17a87-199">Fare clic su **dell'area di lavoro** o **File System** tooset hello contenente il progetto hello.</span><span class="sxs-lookup"><span data-stu-id="17a87-199">Click **Workspace** or **File System** tooset hello folder containing hello project.</span></span>
> 
> 

<span data-ttu-id="17a87-200">Quando si esegue un'applicazione hello, verrà visualizzato una finestra del browser, che fornisce una casella di ricerca per l'immissione di condizioni.</span><span class="sxs-lookup"><span data-stu-id="17a87-200">When you run hello application, you should see a browser window, providing a search box for entering terms.</span></span>

<span data-ttu-id="17a87-201">Attendere circa un minuto prima di scegliere **ricerca** toogive hello servizio ora toocreate e carico hello l'indice.</span><span class="sxs-lookup"><span data-stu-id="17a87-201">Wait about one minute before clicking **Search** toogive hello service time toocreate and load hello index.</span></span> <span data-ttu-id="17a87-202">Se si verifica un errore HTTP 404, è sufficiente toowait un po' più lungo prima di riprovare.</span><span class="sxs-lookup"><span data-stu-id="17a87-202">If you get an HTTP 404 error, you just need toowait a little bit longer before trying again.</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="17a87-203">Eseguire ricerche sui dati dei servizi geologici degli Stati Uniti</span><span class="sxs-lookup"><span data-stu-id="17a87-203">Search on USGS data</span></span>
<span data-ttu-id="17a87-204">Hello soltanto set di dati include i record che sono rilevante toohello lo stato di Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="17a87-204">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="17a87-205">Se si fa clic **ricerca** su una casella di ricerca vuoto, si otterrà voci primi 50 hello, hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="17a87-205">If you click **Search** on an empty search box, you will get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="17a87-206">Immettendo un termine di ricerca fornisce il motore di ricerca hello qualcosa toogo su.</span><span class="sxs-lookup"><span data-stu-id="17a87-206">Entering a search term will give hello search engine something toogo on.</span></span> <span data-ttu-id="17a87-207">Provare a immettere un nome locale.</span><span class="sxs-lookup"><span data-stu-id="17a87-207">Try entering a regional name.</span></span> <span data-ttu-id="17a87-208">"Roger Williams" è stato governor prima di hello del Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="17a87-208">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="17a87-209">Numerosi parchi, edifici e scuole prendono il suo nome.</span><span class="sxs-lookup"><span data-stu-id="17a87-209">Numerous parks, buildings, and schools are named after him.</span></span>

![][11]

<span data-ttu-id="17a87-210">È inoltre possibile tentare con uno dei termini seguenti:</span><span class="sxs-lookup"><span data-stu-id="17a87-210">You could also try any of these terms:</span></span>

* <span data-ttu-id="17a87-211">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="17a87-211">Pawtucket</span></span>
* <span data-ttu-id="17a87-212">Pembroke</span><span class="sxs-lookup"><span data-stu-id="17a87-212">Pembroke</span></span>
* <span data-ttu-id="17a87-213">goose +cape</span><span class="sxs-lookup"><span data-stu-id="17a87-213">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="17a87-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="17a87-214">Next steps</span></span>
<span data-ttu-id="17a87-215">Si tratta di hello prima esercitazione ricerca di Azure basato su Java e hello soltanto set di dati.</span><span class="sxs-lookup"><span data-stu-id="17a87-215">This is hello first Azure Search tutorial based on Java and hello USGS dataset.</span></span> <span data-ttu-id="17a87-216">Nel corso del tempo, toodemonstrate questa esercitazione verrà esteso le funzionalità di ricerca aggiuntive è toouse in soluzioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="17a87-216">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="17a87-217">Se si dispone già di alcuni concetti di base in ricerca di Azure, è possibile utilizzare questo esempio come un springboard per ulteriore sperimentazione, forse aumento hello [pagina ricerca](search-pagination-page-layout.md), o l'implementazione di [navigazione con facet](search-faceted-navigation.md).</span><span class="sxs-lookup"><span data-stu-id="17a87-217">If you already have some background in Azure Search, you can use this sample as a springboard for further experimentation, perhaps augmenting hello [search page](search-pagination-page-layout.md), or implementing [faceted navigation](search-faceted-navigation.md).</span></span> <span data-ttu-id="17a87-218">È inoltre possibile migliorare alla pagina dei risultati di ricerca hello aggiungendo i conteggi e l'invio in batch di documenti in modo che gli utenti possono spostarsi tra i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="17a87-218">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="17a87-219">TooAzure nuova ricerca?</span><span class="sxs-lookup"><span data-stu-id="17a87-219">New tooAzure Search?</span></span> <span data-ttu-id="17a87-220">È consigliabile tentare altri toodevelop esercitazioni la comprensione di ciò che è possibile creare.</span><span class="sxs-lookup"><span data-stu-id="17a87-220">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="17a87-221">Visitare il nostro [pagina della documentazione](https://azure.microsoft.com/documentation/services/search/) toofind più risorse.</span><span class="sxs-lookup"><span data-stu-id="17a87-221">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="17a87-222">È inoltre possibile visualizzare i collegamenti di hello nel nostro [elenco Video e un'esercitazione](search-video-demo-tutorial-list.md) tooaccess ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="17a87-222">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
