---
title: Applicazione .NET multilivello con il bus di servizio di Azure | Documentazione Microsoft
description: Un'esercitazione .NET che consente di sviluppare un'applicazione multilivello in Azure che usa le code di Bus di servizio per la comunicazione tra livelli.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 8b502f5ac5d89801d390a872e7a8b06e094ecbba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a><span data-ttu-id="2d655-103">Applicazione .NET multilivello che usa code del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="2d655-103">.NET multi-tier application using Azure Service Bus queues</span></span>
## <a name="introduction"></a><span data-ttu-id="2d655-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="2d655-104">Introduction</span></span>
<span data-ttu-id="2d655-105">Microsoft Azure consente di sviluppare applicazioni con la stessa semplicità offerta da Visual Studio e Azure SDK gratuito per .NET.</span><span class="sxs-lookup"><span data-stu-id="2d655-105">Developing for Microsoft Azure is easy using Visual Studio and the free Azure SDK for .NET.</span></span> <span data-ttu-id="2d655-106">Questa esercitazione illustra i passaggi per creare un'applicazione che usa più risorse di Azure in esecuzione nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="2d655-106">This tutorial walks you through the steps to create an application that uses multiple Azure resources running in your local environment.</span></span>

<span data-ttu-id="2d655-107">Verranno illustrate le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2d655-107">You will learn the following:</span></span>

* <span data-ttu-id="2d655-108">Abilitare il computer in uso per lo sviluppo per Azure tramite un singolo download e una singola installazione.</span><span class="sxs-lookup"><span data-stu-id="2d655-108">How to enable your computer for Azure development with a single download and install.</span></span>
* <span data-ttu-id="2d655-109">Utilizzare Visual Studio per lo sviluppo per Azure.</span><span class="sxs-lookup"><span data-stu-id="2d655-109">How to use Visual Studio to develop for Azure.</span></span>
* <span data-ttu-id="2d655-110">Creare un'applicazione multilivello in Azure utilizzando ruoli Web e ruoli di lavoro.</span><span class="sxs-lookup"><span data-stu-id="2d655-110">How to create a multi-tier application in Azure using web and worker roles.</span></span>
* <span data-ttu-id="2d655-111">Consentire le comunicazioni tra i livelli usando le code del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="2d655-111">How to communicate between tiers using Service Bus queues.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

<span data-ttu-id="2d655-112">In questa esercitazione verrà creata ed eseguita un'applicazione multilivello in un servizio cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d655-112">In this tutorial you'll build and run the multi-tier application in an Azure cloud service.</span></span> <span data-ttu-id="2d655-113">Il front-end è un ruolo Web ASP.NET MVC e il back-end è un ruolo di lavoro che usa una coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="2d655-113">The front end is an ASP.NET MVC web role and the back end is a worker-role that uses a Service Bus queue.</span></span> <span data-ttu-id="2d655-114">È possibile creare la stessa applicazione multilivello con il front-end come progetto Web distribuito in un sito Web di Azure invece che in un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="2d655-114">You can create the same multi-tier application with the front end as a web project, that is deployed to an Azure website instead of a cloud service.</span></span> <span data-ttu-id="2d655-115">È anche possibile vedere l'esercitazione sull'[applicazione .NET ibrida locale/sul cloud](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md).</span><span class="sxs-lookup"><span data-stu-id="2d655-115">You can also try out the [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span></span>

<span data-ttu-id="2d655-116">Nella schermata seguente è illustrata l'applicazione completata.</span><span class="sxs-lookup"><span data-stu-id="2d655-116">The following screen shot shows the completed application.</span></span>

![][0]

## <a name="scenario-overview-inter-role-communication"></a><span data-ttu-id="2d655-117">Informazioni generali sullo scenario: comunicazione tra ruoli</span><span class="sxs-lookup"><span data-stu-id="2d655-117">Scenario overview: inter-role communication</span></span>
<span data-ttu-id="2d655-118">Per inviare un ordine per l'elaborazione, è necessario che il componente dell'interfaccia utente front-end, in esecuzione nel ruolo Web, interagisca con la logica di livello intermedio in esecuzione nel ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="2d655-118">To submit an order for processing, the front-end UI component, running in the web role, must interact with the middle tier logic running in the worker role.</span></span> <span data-ttu-id="2d655-119">Questo esempio usa la messaggistica del bus di servizio per la comunicazione tra i livelli.</span><span class="sxs-lookup"><span data-stu-id="2d655-119">This example uses Service Bus messaging for the communication between the tiers.</span></span>

<span data-ttu-id="2d655-120">L'uso della messaggistica del bus di servizio tra il livello Web e il livello intermedio consente di disaccoppiare i due componenti.</span><span class="sxs-lookup"><span data-stu-id="2d655-120">Using Service Bus messaging between the web and middle tiers decouples the two components.</span></span> <span data-ttu-id="2d655-121">Invece di usare la messaggistica diretta, ovvero TCP o HTTP, il livello Web non si connette direttamente al livello intermedio, ma inserisce unità di lavoro, ad esempio messaggi, nel bus di servizio, che li conserva in modo affidabile fino a quando il livello intermedio non sarà pronto per usarli ed elaborarli.</span><span class="sxs-lookup"><span data-stu-id="2d655-121">In contrast to direct messaging (that is, TCP or HTTP), the web tier does not connect to the middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until the middle tier is ready to consume and process them.</span></span>

<span data-ttu-id="2d655-122">Il bus di servizio offre due entità per il supporto della messaggistica negoziata, ovvero le code e gli argomenti.</span><span class="sxs-lookup"><span data-stu-id="2d655-122">Service Bus provides two entities to support brokered messaging: queues and topics.</span></span> <span data-ttu-id="2d655-123">Se si usano le code, ogni messaggio inviato alla coda viene usato da un ricevitore singolo.</span><span class="sxs-lookup"><span data-stu-id="2d655-123">With queues, each message sent to the queue is consumed by a single receiver.</span></span> <span data-ttu-id="2d655-124">Gli argomenti supportano il modello pubblicazione/sottoscrizione, in cui ogni messaggio pubblicato viene reso disponibile a una sottoscrizione registrata per l'argomento.</span><span class="sxs-lookup"><span data-stu-id="2d655-124">Topics support the publish/subscribe pattern in which each published message is made available to a subscription registered with the topic.</span></span> <span data-ttu-id="2d655-125">Ogni sottoscrizione mantiene in modo logico la propria coda di messaggi.</span><span class="sxs-lookup"><span data-stu-id="2d655-125">Each subscription logically maintains its own queue of messages.</span></span> <span data-ttu-id="2d655-126">È anche possibile configurare le sottoscrizioni specificando regole di filtro per limitare i set di messaggi passati alla coda della sottoscrizione ai soli messaggi corrispondenti al filtro.</span><span class="sxs-lookup"><span data-stu-id="2d655-126">Subscriptions can also be configured with filter rules that restrict the set of messages passed to the subscription queue to those that match the filter.</span></span> <span data-ttu-id="2d655-127">Nel seguente esempio vengono usate le code del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="2d655-127">The following example uses Service Bus queues.</span></span>

![][1]

<span data-ttu-id="2d655-128">Questo meccanismo di comunicazione presenta alcuni vantaggi rispetto alla messaggistica diretta:</span><span class="sxs-lookup"><span data-stu-id="2d655-128">This communication mechanism has several advantages over direct messaging:</span></span>

* <span data-ttu-id="2d655-129">**Disaccoppiamento temporaneo.**</span><span class="sxs-lookup"><span data-stu-id="2d655-129">**Temporal decoupling.**</span></span> <span data-ttu-id="2d655-130">Grazie al modello di messaggistica asincrono, non è necessario che produttori e consumer siano online nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="2d655-130">With the asynchronous messaging pattern, producers and consumers need not be online at the same time.</span></span> <span data-ttu-id="2d655-131">I messaggi vengono archiviati in modo affidabile nel bus di servizio fino a quando il consumer non sarà pronto per riceverli.</span><span class="sxs-lookup"><span data-stu-id="2d655-131">Service Bus reliably stores messages until the consuming party is ready to receive them.</span></span> <span data-ttu-id="2d655-132">Questo consente la disconnessione volontaria (ad esempio, per attività di manutenzione) o involontaria (a seguito di un guasto) dei componenti dell'applicazione distribuita senza ripercussioni sull'intero sistema.</span><span class="sxs-lookup"><span data-stu-id="2d655-132">This enables the components of the distributed application to be disconnected, either voluntarily, for example, for maintenance, or due to a component crash, without impacting the system as a whole.</span></span> <span data-ttu-id="2d655-133">È inoltre possibile che l'applicazione consumer debba essere online solo in determinati orari.</span><span class="sxs-lookup"><span data-stu-id="2d655-133">Furthermore, the consuming application might only need to come online during certain times of the day.</span></span>
* <span data-ttu-id="2d655-134">**Livellamento del carico.**</span><span class="sxs-lookup"><span data-stu-id="2d655-134">**Load leveling.**</span></span> <span data-ttu-id="2d655-135">In molte applicazioni il carico del sistema varia in base al momento, mentre il tempo di elaborazione richiesto per ogni unità di lavoro è in genere costante.</span><span class="sxs-lookup"><span data-stu-id="2d655-135">In many applications, system load varies over time, while the processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="2d655-136">L'interposizione di una coda tra producer e consumer di messaggi implica che è necessario solo eseguire il provisioning dell'applicazione consumer (il ruolo di lavoro) per consentire a quest'ultima di gestire un carico medio anziché il carico massimo.</span><span class="sxs-lookup"><span data-stu-id="2d655-136">Intermediating message producers and consumers with a queue means that the consuming application (the worker) only needs to be provisioned to accommodate average load rather than peak load.</span></span> <span data-ttu-id="2d655-137">In base alla variazione del carico in ingresso, si verificherà un incremento o una riduzione della profondità della coda,</span><span class="sxs-lookup"><span data-stu-id="2d655-137">The depth of the queue grows and contracts as the incoming load varies.</span></span> <span data-ttu-id="2d655-138">con un risparmio diretto in termini economici rispetto alle risorse infrastrutturali richieste per gestire il carico dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2d655-138">This directly saves money in terms of the amount of infrastructure required to service the application load.</span></span>
* <span data-ttu-id="2d655-139">**Bilanciamento del carico.**</span><span class="sxs-lookup"><span data-stu-id="2d655-139">**Load balancing.**</span></span> <span data-ttu-id="2d655-140">Con l'aumento del carico, è possibile aggiungere altri processi di lavoro per la lettura della coda.</span><span class="sxs-lookup"><span data-stu-id="2d655-140">As load increases, more worker processes can be added to read from the queue.</span></span> <span data-ttu-id="2d655-141">Ciascun messaggio viene elaborato da un solo processo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="2d655-141">Each message is processed by only one of the worker processes.</span></span> <span data-ttu-id="2d655-142">Inoltre, il bilanciamento del carico di tipo pull consente un uso ottimale delle macchine di lavoro anche quando queste presentano una potenza di elaborazione diversa. Ogni macchina effettuerà infatti il pull dei messaggi alla propria velocità massima.</span><span class="sxs-lookup"><span data-stu-id="2d655-142">Furthermore, this pull-based load balancing enables optimal use of the worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="2d655-143">Questo modello viene spesso definito modello del *consumer concorrente*.</span><span class="sxs-lookup"><span data-stu-id="2d655-143">This pattern is often termed the *competing consumer* pattern.</span></span>
  
  ![][2]

<span data-ttu-id="2d655-144">Il codice che consente di implementare questa architettura viene illustrato nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="2d655-144">The following sections discuss the code that implements this architecture.</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="2d655-145">Configurare l'ambiente di sviluppo</span><span class="sxs-lookup"><span data-stu-id="2d655-145">Set up the development environment</span></span>
<span data-ttu-id="2d655-146">Prima di iniziare a sviluppare applicazioni Azure, è necessario ottenere gli strumenti e configurare l'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="2d655-146">Before you can begin developing Azure applications, get the tools and set up your development environment.</span></span>

1. <span data-ttu-id="2d655-147">Installare Azure SDK per .NET dalla [pagina di download](https://azure.microsoft.com/downloads/) di SDK.</span><span class="sxs-lookup"><span data-stu-id="2d655-147">Install the Azure SDK for .NET from the SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="2d655-148">Nella colonna **.NET** fare clic sulla versione di [Visual Studio](http://www.visualstudio.com) in uso.</span><span class="sxs-lookup"><span data-stu-id="2d655-148">In the **.NET** column, click the version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="2d655-149">I passaggi di questa esercitazione usano Visual Studio 2015, ma funzionano anche con Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2d655-149">The steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="2d655-150">Quando viene richiesto se eseguire o salvare il file di installazione, fare clic su **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="2d655-150">When prompted to run or save the installer, click **Run**.</span></span>
4. <span data-ttu-id="2d655-151">Nell'**Installazione guidata piattaforma Web** fare clic su **Installa** e procedere con l'installazione.</span><span class="sxs-lookup"><span data-stu-id="2d655-151">In the **Web Platform Installer**, click **Install** and proceed with the installation.</span></span>
5. <span data-ttu-id="2d655-152">Al termine dell'installazione, saranno disponibili tutti gli strumenti necessari per avviare lo sviluppo dell’app.</span><span class="sxs-lookup"><span data-stu-id="2d655-152">Once the installation is complete, you will have everything necessary to start to develop the app.</span></span> <span data-ttu-id="2d655-153">Nell'SDK sono disponibili gli strumenti che consentono di sviluppare con facilità applicazioni per Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d655-153">The SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="2d655-154">Creare uno spazio dei nomi</span><span class="sxs-lookup"><span data-stu-id="2d655-154">Create a namespace</span></span>
<span data-ttu-id="2d655-155">Il passaggio successivo consiste nel creare uno spazio dei nomi del servizio e nell'ottenere una chiave di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="2d655-155">The next step is to create a service namespace, and obtain a Shared Access Signature (SAS) key.</span></span> <span data-ttu-id="2d655-156">Uno spazio dei nomi fornisce un limite per ogni applicazione esposta tramite il bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="2d655-156">A namespace provides an application boundary for each application exposed through Service Bus.</span></span> <span data-ttu-id="2d655-157">Una chiave di firma di accesso condiviso viene generata dal sistema quando viene creato uno spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="2d655-157">A SAS key is generated by the system when a namespace is created.</span></span> <span data-ttu-id="2d655-158">La combinazione di spazio dei nomi e chiave di firma di accesso condiviso fornisce le credenziali che consentono al bus di servizio di autenticare l'accesso a un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2d655-158">The combination of namespace and SAS key provides the credentials for Service Bus to authenticate access to an application.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a><span data-ttu-id="2d655-159">Creare un ruolo web</span><span class="sxs-lookup"><span data-stu-id="2d655-159">Create a web role</span></span>
<span data-ttu-id="2d655-160">Creare in questa sezione il front-end dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2d655-160">In this section, you build the front end of your application.</span></span> <span data-ttu-id="2d655-161">Creare prima di tutto le pagine visualizzate dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2d655-161">First, you create the pages that your application displays.</span></span>
<span data-ttu-id="2d655-162">Aggiungere quindi il codice per inviare elementi a una coda del bus di servizio e visualizzare informazioni relative allo stato della coda.</span><span class="sxs-lookup"><span data-stu-id="2d655-162">After that, add code that submits items to a Service Bus queue and displays status information about the queue.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="2d655-163">Creare il progetto</span><span class="sxs-lookup"><span data-stu-id="2d655-163">Create the project</span></span>
1. <span data-ttu-id="2d655-164">Avviare Visual Studio con privilegi di amministratore: fare clic con il pulsante destro del mouse sull'icona del programma **Visual Studio** e quindi scegliere **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="2d655-164">Using administrator privileges, start Visual Studio: right-click the **Visual Studio** program icon, and then click **Run as administrator**.</span></span> <span data-ttu-id="2d655-165">Per l'emulatore di calcolo di Azure, illustrato più avanti in questo articolo, è necessario che Visual Studio sia avviato con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="2d655-165">The Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span></span>
   
   <span data-ttu-id="2d655-166">In Visual Studio scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="2d655-166">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="2d655-167">Da **Modelli installati** in **Visual C#** fare clic su **Cloud** e quindi su **Servizio cloud di Azure**.</span><span class="sxs-lookup"><span data-stu-id="2d655-167">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span></span> <span data-ttu-id="2d655-168">Assegnare al progetto il nome **MultiTierApp**.</span><span class="sxs-lookup"><span data-stu-id="2d655-168">Name the project **MultiTierApp**.</span></span> <span data-ttu-id="2d655-169">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2d655-169">Then click **OK**.</span></span>
   
   ![][9]
3. <span data-ttu-id="2d655-170">Dai ruoli **.NET Framework 4.5** fare doppio clic su **Ruolo Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="2d655-170">From **.NET Framework 4.5** roles, double-click **ASP.NET Web Role**.</span></span>
   
   ![][10]
4. <span data-ttu-id="2d655-171">Passare il puntatore su **WebRole1** in **Soluzione servizio cloud di Microsoft Azure**, quindi fare clic sull'icona a forma di matita e rinominare il ruolo Web in **FrontendWebRole**.</span><span class="sxs-lookup"><span data-stu-id="2d655-171">Hover over **WebRole1** under **Azure Cloud Service solution**, click the pencil icon, and rename the web role to **FrontendWebRole**.</span></span> <span data-ttu-id="2d655-172">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2d655-172">Then click **OK**.</span></span> <span data-ttu-id="2d655-173">Assicurarsi di immettere "Frontend" con una 'e' minuscola, non "FrontEnd".</span><span class="sxs-lookup"><span data-stu-id="2d655-173">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span></span>
   
   ![][11]
5. <span data-ttu-id="2d655-174">Nella finestra di dialogo **Nuovo progetto ASP.NET** fare clic su **MVC** in **Seleziona modello**.</span><span class="sxs-lookup"><span data-stu-id="2d655-174">From the **New ASP.NET Project** dialog box, in the **Select a template** list, click **MVC**.</span></span>
   
   ![][12]
6. <span data-ttu-id="2d655-175">Sempre nella finestra di dialogo **Nuovo progetto ASP.NET** fare clic sul pulsante **Modifica autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="2d655-175">Still in the **New ASP.NET Project** dialog box, click the **Change Authentication** button.</span></span> <span data-ttu-id="2d655-176">Nella finestra di dialogo **Modifica autenticazione** fare clic su **Nessuna autenticazione**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2d655-176">In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span> <span data-ttu-id="2d655-177">Per questa esercitazione si distribuisce un'applicazione che non richiede l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="2d655-177">For this tutorial, you're deploying an app that doesn't need a user login.</span></span>
   
    ![][16]
7. <span data-ttu-id="2d655-178">Nella finestra di dialogo **Nuovo progetto ASP.NET** fare clic su **OK** per creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="2d655-178">Back in the **New ASP.NET Project** dialog box, click **OK** to create the project.</span></span>
8. <span data-ttu-id="2d655-179">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Riferimenti** nel progetto **FrontendWebRole** e quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2d655-179">In **Solution Explorer**, in the **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span></span>
9. <span data-ttu-id="2d655-180">Fare clic sulla scheda **Sfoglia** e quindi cercare `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="2d655-180">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="2d655-181">Selezionare il pacchetto **WindowsAzure.ServiceBus**, fare clic su **Installa** e quindi accettare le condizioni per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="2d655-181">Select the **WindowsAzure.ServiceBus** package, click **Install**, and accept the terms of use.</span></span>
   
   ![][13]
   
   <span data-ttu-id="2d655-182">Sono ora disponibili riferimenti agli assembly client necessari e sono stati aggiunti nuovi file di codice.</span><span class="sxs-lookup"><span data-stu-id="2d655-182">Note that the required client assemblies are now referenced and some new code files have been added.</span></span>
10. <span data-ttu-id="2d655-183">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Modelli**, quindi scegliere **Aggiungi** e infine **Classe**.</span><span class="sxs-lookup"><span data-stu-id="2d655-183">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span></span> <span data-ttu-id="2d655-184">Nella casella **Nome** digitare il nome **OnlineOrder.cs**.</span><span class="sxs-lookup"><span data-stu-id="2d655-184">In the **Name** box, type the name **OnlineOrder.cs**.</span></span> <span data-ttu-id="2d655-185">Fare quindi clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2d655-185">Then click **Add**.</span></span>

### <a name="write-the-code-for-your-web-role"></a><span data-ttu-id="2d655-186">Scrivere il codice per il ruolo Web</span><span class="sxs-lookup"><span data-stu-id="2d655-186">Write the code for your web role</span></span>
<span data-ttu-id="2d655-187">Creare prima di tutto in questa sezione le diverse pagine visualizzate dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2d655-187">In this section, you create the various pages that your application displays.</span></span>

1. <span data-ttu-id="2d655-188">In Visual Studio, nel file OnlineOrder.cs sostituire la definizione dello spazio dei nomi esistente con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="2d655-188">In the OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with the following code:</span></span>
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. <span data-ttu-id="2d655-189">In **Esplora soluzioni** fare doppio clic su **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="2d655-189">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span> <span data-ttu-id="2d655-190">Aggiungere le istruzioni **using** seguenti nella parte iniziale del file per includere gli spazi dei nomi per il modello appena creato, oltre al bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="2d655-190">Add the following **using** statements at the top of the file to include the namespaces for the model you just created, as well as Service Bus.</span></span>
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. <span data-ttu-id="2d655-191">Anche nel file HomeController.cs sostituire la definizione dello spazio dei nomi esistente con il seguente codice.</span><span class="sxs-lookup"><span data-stu-id="2d655-191">Also in the HomeController.cs file in Visual Studio, replace the existing namespace definition with the following code.</span></span> <span data-ttu-id="2d655-192">Tale codice include metodi per la gestione dell'invio di elementi alla coda.</span><span class="sxs-lookup"><span data-stu-id="2d655-192">This code contains methods for handling the submission of items to the queue.</span></span>
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect to Submit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for the submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from the submission
           // form.
           [HttpPost]
           // Attribute to help prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting to queue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. <span data-ttu-id="2d655-193">Scegliere **Compila soluzione** dal menu **Compila** per verificare la correttezza del lavoro svolto finora.</span><span class="sxs-lookup"><span data-stu-id="2d655-193">From the **Build** menu, click **Build Solution** to test the accuracy of your work so far.</span></span>
5. <span data-ttu-id="2d655-194">Creare quindi la visualizzazione per il metodo `Submit()` creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2d655-194">Now, create the view for the `Submit()` method you created earlier.</span></span> <span data-ttu-id="2d655-195">Fare clic con il pulsante destro del mouse all'interno del metodo `Submit()`, ovvero l'overload del metodo `Submit()` che non accetta parametri, e quindi scegliere **Aggiungi visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="2d655-195">Right-click within the `Submit()` method (the overload of `Submit()` that takes no parameters), and then choose **Add View**.</span></span>
   
   ![][14]
6. <span data-ttu-id="2d655-196">Viene visualizzata una finestra di dialogo per la creazione della visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="2d655-196">A dialog box appears for creating the view.</span></span> <span data-ttu-id="2d655-197">Nell'elenco **Modello** scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2d655-197">In the **Template** list, choose **Create**.</span></span> <span data-ttu-id="2d655-198">Nell'elenco **Classe modello** scegliere la classe **OnlineOrder**.</span><span class="sxs-lookup"><span data-stu-id="2d655-198">In the **Model class** list, click the **OnlineOrder** class.</span></span>
   
   ![][15]
7. <span data-ttu-id="2d655-199">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2d655-199">Click **Add**.</span></span>
8. <span data-ttu-id="2d655-200">Modificare ora il nome visualizzato dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2d655-200">Now, change the displayed name of your application.</span></span> <span data-ttu-id="2d655-201">In **Esplora soluzioni** fare doppio clic sul file **Views\Shared\\_Layout.cshtml** per aprirlo nell'editor di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d655-201">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file to open it in the Visual Studio editor.</span></span>
9. <span data-ttu-id="2d655-202">Sostituire tutte le occorrenze di **My ASP.NET Application** con **LITWARE'S Products**.</span><span class="sxs-lookup"><span data-stu-id="2d655-202">Replace all occurrences of **My ASP.NET Application** with **LITWARE'S Products**.</span></span>
10. <span data-ttu-id="2d655-203">Rimuovere i collegamenti **Home**, **About** e **Contact**.</span><span class="sxs-lookup"><span data-stu-id="2d655-203">Remove the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="2d655-204">Eliminare il codice evidenziato:</span><span class="sxs-lookup"><span data-stu-id="2d655-204">Delete the highlighted code:</span></span>
    
    ![][28]
11. <span data-ttu-id="2d655-205">Modificare infine la pagina di invio in modo da includere informazioni sulla coda.</span><span class="sxs-lookup"><span data-stu-id="2d655-205">Finally, modify the submission page to include some information about the queue.</span></span> <span data-ttu-id="2d655-206">In **Esplora soluzioni** fare doppio clic sul file **Views\Home\Submit.cshtml** per aprirlo nell'editor di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d655-206">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file to open it in the Visual Studio editor.</span></span> <span data-ttu-id="2d655-207">Aggiungere la riga seguente dopo `<h2>Submit</h2>`.</span><span class="sxs-lookup"><span data-stu-id="2d655-207">Add the following line after `<h2>Submit</h2>`.</span></span> <span data-ttu-id="2d655-208">Per ora `ViewBag.MessageCount` non contiene valori.</span><span class="sxs-lookup"><span data-stu-id="2d655-208">For now, the `ViewBag.MessageCount` is empty.</span></span> <span data-ttu-id="2d655-209">Il valore verrà inserito successivamente.</span><span class="sxs-lookup"><span data-stu-id="2d655-209">You will populate it later.</span></span>
    
    ```html
    <p>Current number of orders in queue waiting to be processed: @ViewBag.MessageCount</p>
    ```
12. <span data-ttu-id="2d655-210">L'interfaccia utente è stata implementata.</span><span class="sxs-lookup"><span data-stu-id="2d655-210">You now have implemented your UI.</span></span> <span data-ttu-id="2d655-211">È possibile premere **F5** per eseguire l'applicazione e confermare che abbia l'aspetto previsto.</span><span class="sxs-lookup"><span data-stu-id="2d655-211">You can press **F5** to run your application and confirm that it looks as expected.</span></span>
    
    ![][17]

### <a name="write-the-code-for-submitting-items-to-a-service-bus-queue"></a><span data-ttu-id="2d655-212">Scrivere codice per l'invio di elementi a una coda del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="2d655-212">Write the code for submitting items to a Service Bus queue</span></span>
<span data-ttu-id="2d655-213">Aggiungere quindi il codice per l'invio di elementi a una coda.</span><span class="sxs-lookup"><span data-stu-id="2d655-213">Now, add code for submitting items to a queue.</span></span> <span data-ttu-id="2d655-214">Creare prima di tutto una classe contenente le informazioni di connessione della coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="2d655-214">First, you create a class that contains your Service Bus queue connection information.</span></span> <span data-ttu-id="2d655-215">Inizializzare quindi la connessione da Global.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="2d655-215">Then, initialize your connection from Global.aspx.cs.</span></span> <span data-ttu-id="2d655-216">Aggiornare infine il codice di invio creato in precedenza in HomeController.cs in modo da inviare effettivamente elementi alla coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="2d655-216">Finally, update the submission code you created earlier in HomeController.cs to actually submit items to a Service Bus queue.</span></span>

1. <span data-ttu-id="2d655-217">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **FrontendWebRole**. È necessario fare clic con il pulsante destro del mouse sul progetto, non sul ruolo.</span><span class="sxs-lookup"><span data-stu-id="2d655-217">In **Solution Explorer**, right-click **FrontendWebRole** (right-click the project, not the role).</span></span> <span data-ttu-id="2d655-218">Fare clic su **Aggiungi**, quindi su **Classe**.</span><span class="sxs-lookup"><span data-stu-id="2d655-218">Click **Add**, and then click **Class**.</span></span>
2. <span data-ttu-id="2d655-219">Assegnare alla classe il nome **QueueConnector.cs**.</span><span class="sxs-lookup"><span data-stu-id="2d655-219">Name the class **QueueConnector.cs**.</span></span> <span data-ttu-id="2d655-220">Fare clic su **Aggiungi** per creare la classe.</span><span class="sxs-lookup"><span data-stu-id="2d655-220">Click **Add** to create the class.</span></span>
3. <span data-ttu-id="2d655-221">Aggiungere ora codice che incapsula le informazioni di connessione e inizializza la connessione a una coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="2d655-221">Now, add code that encapsulates the connection information and initializes the connection to a Service Bus queue.</span></span> <span data-ttu-id="2d655-222">Sostituire l'intero contenuto di QueueConnector.cs con il codice seguente e immettere i valori per `your Service Bus namespace`, ovvero il nome dello spazio dei nomi, e `yourKey`, ovvero la **chiave primaria** ottenuta in precedenza dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d655-222">Replace the entire contents of QueueConnector.cs with the following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is the **primary key** you previously obtained from the Azure portal.</span></span>
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from the portal.
           public const string Namespace = "your Service Bus namespace";
   
           // The name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create the namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http to be friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create the namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create the queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client to the queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. <span data-ttu-id="2d655-223">Assicurarsi che venga chiamato il metodo **Initialize**.</span><span class="sxs-lookup"><span data-stu-id="2d655-223">Now, ensure that your **Initialize** method gets called.</span></span> <span data-ttu-id="2d655-224">In **Esplora soluzioni** fare doppio clic su **Global.asax\Global.asax.cs**.</span><span class="sxs-lookup"><span data-stu-id="2d655-224">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span></span>
5. <span data-ttu-id="2d655-225">Aggiungere la riga di codice seguente alla fine del metodo **Application_Start**.</span><span class="sxs-lookup"><span data-stu-id="2d655-225">Add the following line of code at the end of the **Application_Start** method.</span></span>
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. <span data-ttu-id="2d655-226">Verrà infine aggiornato il codice Web creato in precedenza, in modo da inviare elementi alla coda.</span><span class="sxs-lookup"><span data-stu-id="2d655-226">Finally, update the web code you created earlier, to submit items to the queue.</span></span> <span data-ttu-id="2d655-227">In **Esplora soluzioni** fare doppio clic su **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="2d655-227">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span>
7. <span data-ttu-id="2d655-228">Aggiornare il metodo `Submit()`, ovvero l'overload che non accetta parametri, come indicato di seguito per ottenere il numero di messaggi per la coda.</span><span class="sxs-lookup"><span data-stu-id="2d655-228">Update the `Submit()` method (the overload that takes no parameters) as follows to get the message count for the queue.</span></span>
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you to perform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get the queue, and obtain the message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. <span data-ttu-id="2d655-229">Aggiornare il metodo `Submit(OnlineOrder order)`, ovvero l'overload che accetta un parametro, come indicato di seguito per inviare alla coda le informazioni relative all'ordine.</span><span class="sxs-lookup"><span data-stu-id="2d655-229">Update the `Submit(OnlineOrder order)` method (the overload that takes one parameter) as follows to submit order information to the queue.</span></span>
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from the order.
           var message = new BrokeredMessage(order);
   
           // Submit the order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. <span data-ttu-id="2d655-230">È ora possibile eseguire di nuovo l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2d655-230">You can now run the application again.</span></span> <span data-ttu-id="2d655-231">Ogni volta che si invia un ordine, il conteggio dei messaggi aumenta.</span><span class="sxs-lookup"><span data-stu-id="2d655-231">Each time you submit an order, the message count increases.</span></span>
   
   ![][18]

## <a name="create-the-worker-role"></a><span data-ttu-id="2d655-232">Creare il ruolo di lavoro</span><span class="sxs-lookup"><span data-stu-id="2d655-232">Create the worker role</span></span>
<span data-ttu-id="2d655-233">Verrà ora creato il ruolo di lavoro che elabora l'invio dell'ordine.</span><span class="sxs-lookup"><span data-stu-id="2d655-233">You will now create the worker role that processes the order submissions.</span></span> <span data-ttu-id="2d655-234">In questo esempio viene usato il modello di progetto **Worker Role with Service Bus Queue** di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d655-234">This example uses the **Worker Role with Service Bus Queue** Visual Studio project template.</span></span> <span data-ttu-id="2d655-235">Le credenziali necessarie sono già state ottenute dal portale.</span><span class="sxs-lookup"><span data-stu-id="2d655-235">You already obtained the required credentials from the portal.</span></span>

1. <span data-ttu-id="2d655-236">Assicurarsi che Visual Studio sia connesso all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="2d655-236">Make sure you have connected Visual Studio to your Azure account.</span></span>
2. <span data-ttu-id="2d655-237">In **Esplora soluzioni** in Visual Studio fare clic con il pulsante destro del mouse sulla cartella **Roles** nel progetto **MultiTierApp**.</span><span class="sxs-lookup"><span data-stu-id="2d655-237">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under the **MultiTierApp** project.</span></span>
3. <span data-ttu-id="2d655-238">Fare clic su **Aggiungi**, quindi su **Nuovo progetto di ruolo di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="2d655-238">Click **Add**, and then click **New Worker Role Project**.</span></span> <span data-ttu-id="2d655-239">Viene visualizzata la finestra di dialogo **Aggiungi nuovo progetto di ruolo**.</span><span class="sxs-lookup"><span data-stu-id="2d655-239">The **Add New Role Project** dialog box appears.</span></span>
   
   ![][26]
4. <span data-ttu-id="2d655-240">Nella finestra di dialogo **Aggiungi nuovo progetto di ruolo** fare clic su **Worker Role with Service Bus Queue**.</span><span class="sxs-lookup"><span data-stu-id="2d655-240">In the **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span></span>
   
   ![][23]
5. <span data-ttu-id="2d655-241">Nella casella **Nome** assegnare il nome **OrderProcessingRole**.</span><span class="sxs-lookup"><span data-stu-id="2d655-241">In the **Name** box, name the project **OrderProcessingRole**.</span></span> <span data-ttu-id="2d655-242">Fare quindi clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2d655-242">Then click **Add**.</span></span>
6. <span data-ttu-id="2d655-243">Copiare negli Appunti la stringa di connessione ottenuta nel passaggio 9 della sezione "Creare uno spazio dei nomi del bus di servizio".</span><span class="sxs-lookup"><span data-stu-id="2d655-243">Copy the connection string that you obtained in step 9 of the "Create a Service Bus namespace" section to the clipboard.</span></span>
7. <span data-ttu-id="2d655-244">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul ruolo **OrderProcessingRole** creato nel passaggio 5. Assicurarsi di fare clic con il pulsante destro del mouse su **OrderProcessingRole** in **Ruoli** e non sulla classe.</span><span class="sxs-lookup"><span data-stu-id="2d655-244">In **Solution Explorer**, right-click the **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not the class).</span></span> <span data-ttu-id="2d655-245">Fare quindi clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="2d655-245">Then click **Properties**.</span></span>
8. <span data-ttu-id="2d655-246">Nella scheda **Impostazioni** della finestra di dialogo **Proprietà** posizionare il cursore all'interno della casella **Valore** per **Microsoft.ServiceBus.ConnectionString**, quindi incollare il valore dell'endpoint copiato al passaggio 6.</span><span class="sxs-lookup"><span data-stu-id="2d655-246">On the **Settings** tab of the **Properties** dialog box, click inside the **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste the endpoint value you copied in step 6.</span></span>
   
   ![][25]
9. <span data-ttu-id="2d655-247">Creare una classe **OnlineOrder** che rappresenti gli ordini elaborati dalla coda.</span><span class="sxs-lookup"><span data-stu-id="2d655-247">Create an **OnlineOrder** class to represent the orders as you process them from the queue.</span></span> <span data-ttu-id="2d655-248">È possibile riutilizzare una classe creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2d655-248">You can reuse a class you have already created.</span></span> <span data-ttu-id="2d655-249">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla classe **OrderProcessingRole**. È necessario fare clic con il pulsante destro del mouse sull'icona della classe, non sul ruolo.</span><span class="sxs-lookup"><span data-stu-id="2d655-249">In **Solution Explorer**, right-click the **OrderProcessingRole** class (right-click the class icon, not the role).</span></span> <span data-ttu-id="2d655-250">Fare clic su **Aggiungi**, quindi su **Elemento esistente**.</span><span class="sxs-lookup"><span data-stu-id="2d655-250">Click **Add**, then click **Existing Item**.</span></span>
10. <span data-ttu-id="2d655-251">Selezionare la sottocartella per **FrontendWebRole\Models**e fare doppio clic su **OnlineOrder.cs** per aggiungerlo al progetto corrente.</span><span class="sxs-lookup"><span data-stu-id="2d655-251">Browse to the subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** to add it to this project.</span></span>
11. <span data-ttu-id="2d655-252">In **WorkerRole.cs** modificare il valore della variabile **QueueName** da `"ProcessingQueue"` in `"OrdersQueue"` come illustrato nel codice seguente.</span><span class="sxs-lookup"><span data-stu-id="2d655-252">In **WorkerRole.cs**, change the value of the **QueueName** variable from `"ProcessingQueue"` to `"OrdersQueue"` as shown in the following code.</span></span>
    
    ```csharp
    // The name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. <span data-ttu-id="2d655-253">Aggiungere l'istruzione using seguente all'inizio del file WorkerRole.cs.</span><span class="sxs-lookup"><span data-stu-id="2d655-253">Add the following using statement at the top of the WorkerRole.cs file.</span></span>
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. <span data-ttu-id="2d655-254">Nella funzione `Run()`, all'interno della chiamata `OnMessage()`, sostituire il contenuto della clausola `try` con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="2d655-254">In the `Run()` function, inside the `OnMessage()` call, replace the contents of the `try` clause with the following code.</span></span>
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View the message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. <span data-ttu-id="2d655-255">L'applicazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="2d655-255">You have completed the application.</span></span> <span data-ttu-id="2d655-256">È possibile testare l'applicazione completa facendo clic con il pulsante destro del mouse sul progetto MultiTierApp in Esplora soluzioni. Selezionare quindi **Imposta come progetto di avvio** e premere F5.</span><span class="sxs-lookup"><span data-stu-id="2d655-256">You can test the full application by right-clicking the MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span></span> <span data-ttu-id="2d655-257">Il numero totale dei messaggi non aumenta perché il ruolo di lavoro elabora gli elementi dalla coda e li contrassegna come completati.</span><span class="sxs-lookup"><span data-stu-id="2d655-257">Note that the message count does not increment, because the worker role processes items from the queue and marks them as complete.</span></span> <span data-ttu-id="2d655-258">È possibile verificare l'output di traccia del ruolo di lavoro visualizzando l'interfaccia utente dell'emulatore di calcolo di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d655-258">You can see the trace output of your worker role by viewing the Azure Compute Emulator UI.</span></span> <span data-ttu-id="2d655-259">Per eseguire questa operazione, fare clic con il pulsante destro del mouse sull'icona dell'emulatore nell'area di notifica della barra delle applicazioni, quindi scegliere **Show Compute Emulator UI** (Mostra interfaccia utente dell'emulatore di calcolo).</span><span class="sxs-lookup"><span data-stu-id="2d655-259">You can do this by right-clicking the emulator icon in the notification area of your taskbar and selecting **Show Compute Emulator UI**.</span></span>
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a><span data-ttu-id="2d655-260">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2d655-260">Next steps</span></span>
<span data-ttu-id="2d655-261">Per ulteriori informazioni sul bus di servizio, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="2d655-261">To learn more about Service Bus, see the following resources:</span></span>  

* <span data-ttu-id="2d655-262">[Documentazione sul bus di servizio di Azure][sbdocs]</span><span class="sxs-lookup"><span data-stu-id="2d655-262">[Azure Service Bus documentation][sbdocs]</span></span>  
* <span data-ttu-id="2d655-263">[Pagina del servizio Bus di servizio][sbacom]</span><span class="sxs-lookup"><span data-stu-id="2d655-263">[Service Bus service page][sbacom]</span></span>  
* <span data-ttu-id="2d655-264">[Come usare le code del bus di servizio][sbacomqhowto]</span><span class="sxs-lookup"><span data-stu-id="2d655-264">[How to Use Service Bus Queues][sbacomqhowto]</span></span>  

<span data-ttu-id="2d655-265">Per altre informazioni sugli scenari multilivello, vedere:</span><span class="sxs-lookup"><span data-stu-id="2d655-265">To learn more about multi-tier scenarios, see:</span></span>  

* <span data-ttu-id="2d655-266">[Applicazione .NET multilivello con tabelle, code e BLOB di archiviazione di Azure][mutitierstorage]</span><span class="sxs-lookup"><span data-stu-id="2d655-266">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span></span>  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36
