---
title: applicazione multilivello aaa.NET utilizzando Azure Service Bus | Documenti Microsoft
description: "Un'esercitazione .NET che consente di sviluppare un'applicazione a più livelli in Azure che utilizza toocommunicate code Service Bus tra livelli."
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
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a><span data-ttu-id="06a7e-103">Applicazione .NET multilivello che usa code del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="06a7e-103">.NET multi-tier application using Azure Service Bus queues</span></span>
## <a name="introduction"></a><span data-ttu-id="06a7e-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="06a7e-104">Introduction</span></span>
<span data-ttu-id="06a7e-105">Sviluppo per Microsoft Azure è semplice con Visual Studio e hello gratuito di Azure SDK per .NET.</span><span class="sxs-lookup"><span data-stu-id="06a7e-105">Developing for Microsoft Azure is easy using Visual Studio and hello free Azure SDK for .NET.</span></span> <span data-ttu-id="06a7e-106">In questa esercitazione illustra hello passaggi toocreate un'applicazione che utilizza più risorse di Azure in esecuzione nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="06a7e-106">This tutorial walks you through hello steps toocreate an application that uses multiple Azure resources running in your local environment.</span></span>

<span data-ttu-id="06a7e-107">Si apprenderà seguente hello:</span><span class="sxs-lookup"><span data-stu-id="06a7e-107">You will learn hello following:</span></span>

* <span data-ttu-id="06a7e-108">Come tooenable del computer per lo sviluppo di Azure con un singolo scaricare e installare.</span><span class="sxs-lookup"><span data-stu-id="06a7e-108">How tooenable your computer for Azure development with a single download and install.</span></span>
* <span data-ttu-id="06a7e-109">Come toouse toodevelop di Visual Studio per Azure.</span><span class="sxs-lookup"><span data-stu-id="06a7e-109">How toouse Visual Studio toodevelop for Azure.</span></span>
* <span data-ttu-id="06a7e-110">Come toocreate un'applicazione a più livelli in Azure usando i ruoli web e di lavoro.</span><span class="sxs-lookup"><span data-stu-id="06a7e-110">How toocreate a multi-tier application in Azure using web and worker roles.</span></span>
* <span data-ttu-id="06a7e-111">Come toocommunicate tra livelli mediante le code del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="06a7e-111">How toocommunicate between tiers using Service Bus queues.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

<span data-ttu-id="06a7e-112">In questa esercitazione si sarà compilare ed eseguire un'applicazione multilivello hello in un servizio cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="06a7e-112">In this tutorial you'll build and run hello multi-tier application in an Azure cloud service.</span></span> <span data-ttu-id="06a7e-113">front-end Hello è un ruolo web ASP.NET MVC e back-end hello è un ruolo di lavoro che utilizza una coda del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="06a7e-113">hello front end is an ASP.NET MVC web role and hello back end is a worker-role that uses a Service Bus queue.</span></span> <span data-ttu-id="06a7e-114">È possibile creare hello stesso multilivello con front-end hello come progetto di applicazione web, che viene distribuito tooan sito Web di Azure invece di un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="06a7e-114">You can create hello same multi-tier application with hello front end as a web project, that is deployed tooan Azure website instead of a cloud service.</span></span> <span data-ttu-id="06a7e-115">È anche possibile provare hello [un'applicazione in locale/cloud ibrida .NET](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="06a7e-115">You can also try out hello [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span></span>

<span data-ttu-id="06a7e-116">Hello cattura di schermata seguente mostra un'applicazione hello completata.</span><span class="sxs-lookup"><span data-stu-id="06a7e-116">hello following screen shot shows hello completed application.</span></span>

![][0]

## <a name="scenario-overview-inter-role-communication"></a><span data-ttu-id="06a7e-117">Informazioni generali sullo scenario: comunicazione tra ruoli</span><span class="sxs-lookup"><span data-stu-id="06a7e-117">Scenario overview: inter-role communication</span></span>
<span data-ttu-id="06a7e-118">toosubmit un ordine per l'elaborazione, componente dell'interfaccia utente front-end hello, in esecuzione nel ruolo web hello devono interagire con la logica di livello intermedio hello in esecuzione nel ruolo di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-118">toosubmit an order for processing, hello front-end UI component, running in hello web role, must interact with hello middle tier logic running in hello worker role.</span></span> <span data-ttu-id="06a7e-119">In questo esempio utilizza la messaggistica di Service Bus per la comunicazione tra i livelli di hello hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-119">This example uses Service Bus messaging for hello communication between hello tiers.</span></span>

<span data-ttu-id="06a7e-120">Uso del Bus di servizio Messaggistica tra i livelli intermedi e web hello separa i due componenti.</span><span class="sxs-lookup"><span data-stu-id="06a7e-120">Using Service Bus messaging between hello web and middle tiers decouples the two components.</span></span> <span data-ttu-id="06a7e-121">Al contrario di hello toodirect messaggistica (ovvero, TCP o HTTP), livello web non si connette intermedio toohello direttamente. invece inserisce le unità di lavoro, come i messaggi nel Bus di servizio, che li mantiene fino al livello intermedio hello tooconsume pronto in modo affidabile ed elaborarle.</span><span class="sxs-lookup"><span data-stu-id="06a7e-121">In contrast toodirect messaging (that is, TCP or HTTP), hello web tier does not connect toohello middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until hello middle tier is ready tooconsume and process them.</span></span>

<span data-ttu-id="06a7e-122">Bus di servizio offre due entità toosupport negoziata messaggistica: code e argomenti.</span><span class="sxs-lookup"><span data-stu-id="06a7e-122">Service Bus provides two entities toosupport brokered messaging: queues and topics.</span></span> <span data-ttu-id="06a7e-123">Con le code, ogni messaggio inviato toohello coda viene utilizzata da un singolo ricevitore.</span><span class="sxs-lookup"><span data-stu-id="06a7e-123">With queues, each message sent toohello queue is consumed by a single receiver.</span></span> <span data-ttu-id="06a7e-124">Gli argomenti supportano modello hello pubblicazione/sottoscrizione in cui ogni messaggio pubblicato viene reso disponibile tooa sottoscrizione registrata con argomento hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-124">Topics support hello publish/subscribe pattern in which each published message is made available tooa subscription registered with hello topic.</span></span> <span data-ttu-id="06a7e-125">Ogni sottoscrizione mantiene in modo logico la propria coda di messaggi.</span><span class="sxs-lookup"><span data-stu-id="06a7e-125">Each subscription logically maintains its own queue of messages.</span></span> <span data-ttu-id="06a7e-126">Le sottoscrizioni possono essere configurate anche con regole dei filtri che limitano il set di hello di messaggi passati a hello sottoscrizione coda toothose che corrispondono al filtro hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-126">Subscriptions can also be configured with filter rules that restrict hello set of messages passed to hello subscription queue toothose that match hello filter.</span></span> <span data-ttu-id="06a7e-127">Hello esempio seguente usa le code del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="06a7e-127">hello following example uses Service Bus queues.</span></span>

![][1]

<span data-ttu-id="06a7e-128">Questo meccanismo di comunicazione presenta alcuni vantaggi rispetto alla messaggistica diretta:</span><span class="sxs-lookup"><span data-stu-id="06a7e-128">This communication mechanism has several advantages over direct messaging:</span></span>

* <span data-ttu-id="06a7e-129">**Disaccoppiamento temporaneo.**</span><span class="sxs-lookup"><span data-stu-id="06a7e-129">**Temporal decoupling.**</span></span> <span data-ttu-id="06a7e-130">Con modello di messaggistica asincrona di hello, producer e consumer non è necessario online all'indirizzo hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="06a7e-130">With hello asynchronous messaging pattern, producers and consumers need not be online at hello same time.</span></span> <span data-ttu-id="06a7e-131">Bus di servizio archivia in modo affidabile i messaggi hello finché consumer non è pronto a riceverli.</span><span class="sxs-lookup"><span data-stu-id="06a7e-131">Service Bus reliably stores messages until hello consuming party is ready to receive them.</span></span> <span data-ttu-id="06a7e-132">In questo modo i componenti di hello di toobe applicazione hello distribuita disconnesso, sia volontariamente, ad esempio, per la manutenzione o a causa di arresto anomalo del componente tooa, senza alcun impatto sul sistema nel suo complesso.</span><span class="sxs-lookup"><span data-stu-id="06a7e-132">This enables hello components of hello distributed application toobe disconnected, either voluntarily, for example, for maintenance, or due tooa component crash, without impacting the system as a whole.</span></span> <span data-ttu-id="06a7e-133">Inoltre, hello utilizzano l'applicazione potrebbe essere necessario solo toocome online durante determinate ore del giorno hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-133">Furthermore, hello consuming application might only need toocome online during certain times of hello day.</span></span>
* <span data-ttu-id="06a7e-134">**Livellamento del carico.**</span><span class="sxs-lookup"><span data-stu-id="06a7e-134">**Load leveling.**</span></span> <span data-ttu-id="06a7e-135">In molte applicazioni, il carico del sistema varia nel tempo, mentre il tempo di elaborazione di hello necessario per ogni unità di lavoro è in genere costante.</span><span class="sxs-lookup"><span data-stu-id="06a7e-135">In many applications, system load varies over time, while hello processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="06a7e-136">Interposizione messaggio producer e consumer una coda significa che hello utilizzo applicazione (worker hello) solo esigenze toobe provisioning tooaccommodate di carico medio invece di un carico di picco.</span><span class="sxs-lookup"><span data-stu-id="06a7e-136">Intermediating message producers and consumers with a queue means that hello consuming application (hello worker) only needs toobe provisioned tooaccommodate average load rather than peak load.</span></span> <span data-ttu-id="06a7e-137">profondità Hello della coda di hello aumentano e i contratti in base alla variazione carico in ingresso hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-137">hello depth of hello queue grows and contracts as hello incoming load varies.</span></span> <span data-ttu-id="06a7e-138">In questo modo direttamente money in termini di quantità hello infrastruttura richiesto tooservice hello carico dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="06a7e-138">This directly saves money in terms of hello amount of infrastructure required tooservice hello application load.</span></span>
* <span data-ttu-id="06a7e-139">**Bilanciamento del carico.**</span><span class="sxs-lookup"><span data-stu-id="06a7e-139">**Load balancing.**</span></span> <span data-ttu-id="06a7e-140">Come aumentare del carico, altri processi di lavoro è possibile aggiungere tooread dalla coda hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-140">As load increases, more worker processes can be added tooread from hello queue.</span></span> <span data-ttu-id="06a7e-141">Ogni messaggio viene elaborato da un solo hello di processi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="06a7e-141">Each message is processed by only one of hello worker processes.</span></span> <span data-ttu-id="06a7e-142">Inoltre, il bilanciamento del carico basato su pull consente l'utilizzo ottimale delle macchine lavoro hello anche se le macchine di lavoro si differenziano in termini di potenza di elaborazione, come verrà estraggono i messaggi alla propria velocità massima.</span><span class="sxs-lookup"><span data-stu-id="06a7e-142">Furthermore, this pull-based load balancing enables optimal use of hello worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="06a7e-143">Questo modello viene spesso definito hello *consumer concorrente* modello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-143">This pattern is often termed hello *competing consumer* pattern.</span></span>
  
  ![][2]

<span data-ttu-id="06a7e-144">Hello le sezioni seguenti viene illustrato il codice hello che implementa questa architettura.</span><span class="sxs-lookup"><span data-stu-id="06a7e-144">hello following sections discuss hello code that implements this architecture.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="06a7e-145">Configurare un ambiente di sviluppo hello</span><span class="sxs-lookup"><span data-stu-id="06a7e-145">Set up hello development environment</span></span>
<span data-ttu-id="06a7e-146">Prima di iniziare lo sviluppo di applicazioni Azure, Scarica gli strumenti di hello e configurare l'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="06a7e-146">Before you can begin developing Azure applications, get hello tools and set up your development environment.</span></span>

1. <span data-ttu-id="06a7e-147">Installare hello Azure SDK per .NET da hello SDK [pagina di download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="06a7e-147">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="06a7e-148">In hello **.NET** colonna, fare clic sulla versione di hello di [Visual Studio](http://www.visualstudio.com) in uso.</span><span class="sxs-lookup"><span data-stu-id="06a7e-148">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="06a7e-149">Hello i passaggi in questa esercitazione usare Visual Studio 2015, ma funzionano anche con Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="06a7e-149">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="06a7e-150">Quando viene chiesto di toorun o salvare installer hello, fare clic su **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-150">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="06a7e-151">In hello **installazione guidata piattaforma Web**, fare clic su **installare** e continuare l'installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-151">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="06a7e-152">Al termine dell'installazione di hello, sarà necessario tutto il necessario toostart toodevelop hello app.</span><span class="sxs-lookup"><span data-stu-id="06a7e-152">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="06a7e-153">Hello SDK include strumenti che consentono di sviluppare facilmente applicazioni Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="06a7e-153">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="06a7e-154">Creare uno spazio dei nomi</span><span class="sxs-lookup"><span data-stu-id="06a7e-154">Create a namespace</span></span>
<span data-ttu-id="06a7e-155">passaggio successivo Hello è toocreate uno spazio dei nomi di servizio e ottenere una chiave di firma di accesso condiviso (SAS).</span><span class="sxs-lookup"><span data-stu-id="06a7e-155">hello next step is toocreate a service namespace, and obtain a Shared Access Signature (SAS) key.</span></span> <span data-ttu-id="06a7e-156">Uno spazio dei nomi fornisce un limite per ogni applicazione esposta tramite il bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="06a7e-156">A namespace provides an application boundary for each application exposed through Service Bus.</span></span> <span data-ttu-id="06a7e-157">Una chiave di firma di accesso condiviso viene generata dal sistema hello quando viene creato uno spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="06a7e-157">A SAS key is generated by hello system when a namespace is created.</span></span> <span data-ttu-id="06a7e-158">combinazione di Hello di spazio dei nomi e la chiave di firma di accesso condiviso fornisce le credenziali di hello per applicazione tooan accesso tooauthenticate di Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="06a7e-158">hello combination of namespace and SAS key provides hello credentials for Service Bus tooauthenticate access tooan application.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a><span data-ttu-id="06a7e-159">Creare un ruolo web</span><span class="sxs-lookup"><span data-stu-id="06a7e-159">Create a web role</span></span>
<span data-ttu-id="06a7e-160">In questa sezione, si compila front-end di hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="06a7e-160">In this section, you build hello front end of your application.</span></span> <span data-ttu-id="06a7e-161">Creare innanzitutto le pagine di hello visualizzato dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="06a7e-161">First, you create hello pages that your application displays.</span></span>
<span data-ttu-id="06a7e-162">Successivamente, aggiungere il codice che invia gli elementi della coda del Bus di servizio tooa e visualizza le informazioni di stato coda hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-162">After that, add code that submits items tooa Service Bus queue and displays status information about hello queue.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="06a7e-163">Creare il progetto hello</span><span class="sxs-lookup"><span data-stu-id="06a7e-163">Create hello project</span></span>
1. <span data-ttu-id="06a7e-164">Con privilegi di amministratore, avviare Visual Studio: hello rapida **Visual Studio** sull'icona di programma e quindi fare clic su **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-164">Using administrator privileges, start Visual Studio: right-click hello **Visual Studio** program icon, and then click **Run as administrator**.</span></span> <span data-ttu-id="06a7e-165">emulatore di calcolo di Azure Hello, descritto più avanti in questo articolo, è necessario che è possibile avviare Visual Studio con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="06a7e-165">hello Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span></span>
   
   <span data-ttu-id="06a7e-166">In Visual Studio, su hello **File** menu, fare clic su **New**, quindi fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-166">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="06a7e-167">Da **Modelli installati** in **Visual C#** fare clic su **Cloud** e quindi su **Servizio cloud di Azure**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-167">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span></span> <span data-ttu-id="06a7e-168">Progetto hello nome **MultiTierApp**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-168">Name hello project **MultiTierApp**.</span></span> <span data-ttu-id="06a7e-169">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-169">Then click **OK**.</span></span>
   
   ![][9]
3. <span data-ttu-id="06a7e-170">Dai ruoli **.NET Framework 4.5** fare doppio clic su **Ruolo Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-170">From **.NET Framework 4.5** roles, double-click **ASP.NET Web Role**.</span></span>
   
   ![][10]
4. <span data-ttu-id="06a7e-171">Passare il mouse su **WebRole1** in **soluzione servizio Cloud di Azure**, fare clic sull'icona di matita hello e rinominare il ruolo di web hello troppo**FrontendWebRole**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-171">Hover over **WebRole1** under **Azure Cloud Service solution**, click hello pencil icon, and rename hello web role too**FrontendWebRole**.</span></span> <span data-ttu-id="06a7e-172">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-172">Then click **OK**.</span></span> <span data-ttu-id="06a7e-173">Assicurarsi di immettere "Frontend" con una 'e' minuscola, non "FrontEnd".</span><span class="sxs-lookup"><span data-stu-id="06a7e-173">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span></span>
   
   ![][11]
5. <span data-ttu-id="06a7e-174">Da hello **nuovo progetto ASP.NET** della finestra di dialogo hello **selezionare un modello** elenco, fare clic su **MVC**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-174">From hello **New ASP.NET Project** dialog box, in hello **Select a template** list, click **MVC**.</span></span>
   
   ![][12]
6. <span data-ttu-id="06a7e-175">Ancora in hello **nuovo progetto ASP.NET** finestra di dialogo fare clic su hello **Modifica autenticazione** pulsante.</span><span class="sxs-lookup"><span data-stu-id="06a7e-175">Still in hello **New ASP.NET Project** dialog box, click hello **Change Authentication** button.</span></span> <span data-ttu-id="06a7e-176">In hello **Modifica autenticazione** la finestra di dialogo, fare clic su **Nessuna autenticazione**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-176">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span> <span data-ttu-id="06a7e-177">Per questa esercitazione si distribuisce un'applicazione che non richiede l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="06a7e-177">For this tutorial, you're deploying an app that doesn't need a user login.</span></span>
   
    ![][16]
7. <span data-ttu-id="06a7e-178">In hello **nuovo progetto ASP.NET** la finestra di dialogo, fare clic su **OK** progetto hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="06a7e-178">Back in hello **New ASP.NET Project** dialog box, click **OK** toocreate hello project.</span></span>
8. <span data-ttu-id="06a7e-179">In **Esplora**, in hello **FrontendWebRole** del progetto, fare doppio clic su **riferimenti**, quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-179">In **Solution Explorer**, in hello **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span></span>
9. <span data-ttu-id="06a7e-180">Fare clic su hello **Sfoglia** tab, quindi cercare `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="06a7e-180">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="06a7e-181">Seleziona hello **Windowsazure** del pacchetto, fare clic su **installare**e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="06a7e-181">Select hello **WindowsAzure.ServiceBus** package, click **Install**, and accept hello terms of use.</span></span>
   
   ![][13]
   
   <span data-ttu-id="06a7e-182">Si noti che hello e obbligatori per l'assembly client fa riferimento a questo punto sono stati aggiunti alcuni nuovi file di codice.</span><span class="sxs-lookup"><span data-stu-id="06a7e-182">Note that hello required client assemblies are now referenced and some new code files have been added.</span></span>
10. <span data-ttu-id="06a7e-183">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Modelli**, quindi scegliere **Aggiungi** e infine **Classe**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-183">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span></span> <span data-ttu-id="06a7e-184">In hello **nome** casella, il nome del tipo hello **Onlineorder**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-184">In hello **Name** box, type hello name **OnlineOrder.cs**.</span></span> <span data-ttu-id="06a7e-185">Fare quindi clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-185">Then click **Add**.</span></span>

### <a name="write-hello-code-for-your-web-role"></a><span data-ttu-id="06a7e-186">Scrittura di codice hello per il ruolo web</span><span class="sxs-lookup"><span data-stu-id="06a7e-186">Write hello code for your web role</span></span>
<span data-ttu-id="06a7e-187">In questa sezione è creare hello varie pagine visualizzato dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="06a7e-187">In this section, you create hello various pages that your application displays.</span></span>

1. <span data-ttu-id="06a7e-188">Nel file di Onlineorder hello in Visual Studio, sostituire la definizione dello spazio dei nomi esistente con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="06a7e-188">In hello OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with hello following code:</span></span>
   
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
2. <span data-ttu-id="06a7e-189">In **Esplora soluzioni** fare doppio clic su **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-189">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span> <span data-ttu-id="06a7e-190">Aggiungere il seguente hello **utilizzando** istruzioni nella parte superiore di hello di hello file tooinclude hello gli spazi dei nomi per il modello appena creato, nonché il Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="06a7e-190">Add hello following **using** statements at hello top of hello file tooinclude hello namespaces for the model you just created, as well as Service Bus.</span></span>
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. <span data-ttu-id="06a7e-191">Anche nel file di hello HomeController. cs in Visual Studio, sostituire la definizione dello spazio dei nomi esistente con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="06a7e-191">Also in hello HomeController.cs file in Visual Studio, replace the existing namespace definition with hello following code.</span></span> <span data-ttu-id="06a7e-192">Questo codice contiene metodi per la gestione di presentazione hello della coda toohello degli elementi.</span><span class="sxs-lookup"><span data-stu-id="06a7e-192">This code contains methods for handling hello submission of items toohello queue.</span></span>
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
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
4. <span data-ttu-id="06a7e-193">Da hello **compilare** menu, fare clic su **Compila soluzione** accuratezza hello tootest del lavoro svolto finora.</span><span class="sxs-lookup"><span data-stu-id="06a7e-193">From hello **Build** menu, click **Build Solution** tootest hello accuracy of your work so far.</span></span>
5. <span data-ttu-id="06a7e-194">A questo punto, creare vista hello per hello `Submit()` metodo creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="06a7e-194">Now, create hello view for hello `Submit()` method you created earlier.</span></span> <span data-ttu-id="06a7e-195">Fare doppio clic all'interno di hello `Submit()` metodo (overload hello del `Submit()` che non accetta parametri), quindi scegliere **Aggiungi visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-195">Right-click within hello `Submit()` method (hello overload of `Submit()` that takes no parameters), and then choose **Add View**.</span></span>
   
   ![][14]
6. <span data-ttu-id="06a7e-196">Una finestra di dialogo viene visualizzata per la creazione di visualizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-196">A dialog box appears for creating hello view.</span></span> <span data-ttu-id="06a7e-197">In hello **modello** scegliere **crea**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-197">In hello **Template** list, choose **Create**.</span></span> <span data-ttu-id="06a7e-198">In hello **classe modello** elenco, fare clic su hello **OnlineOrder** classe.</span><span class="sxs-lookup"><span data-stu-id="06a7e-198">In hello **Model class** list, click hello **OnlineOrder** class.</span></span>
   
   ![][15]
7. <span data-ttu-id="06a7e-199">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-199">Click **Add**.</span></span>
8. <span data-ttu-id="06a7e-200">A questo punto, modificare il nome di hello visualizzato dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="06a7e-200">Now, change hello displayed name of your application.</span></span> <span data-ttu-id="06a7e-201">In **Esplora**, fare doppio clic su di **Views\Shared\\layout. cshtml** tooopen del file nell'editor di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-201">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="06a7e-202">Sostituire tutte le occorrenze di **My ASP.NET Application** con **LITWARE'S Products**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-202">Replace all occurrences of **My ASP.NET Application** with **LITWARE'S Products**.</span></span>
10. <span data-ttu-id="06a7e-203">Rimuovere hello **Home**, **su**, e **contatto** collegamenti.</span><span class="sxs-lookup"><span data-stu-id="06a7e-203">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="06a7e-204">Eliminare il codice evidenziato hello:</span><span class="sxs-lookup"><span data-stu-id="06a7e-204">Delete hello highlighted code:</span></span>
    
    ![][28]
11. <span data-ttu-id="06a7e-205">Infine, modificare hello invio pagina tooinclude alcune informazioni sulla coda hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-205">Finally, modify hello submission page tooinclude some information about hello queue.</span></span> <span data-ttu-id="06a7e-206">In **Esplora**, fare doppio clic su di **Views\Home\Submit.cshtml** tooopen del file nell'editor di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-206">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="06a7e-207">Aggiungere hello successiva riga dopo `<h2>Submit</h2>`.</span><span class="sxs-lookup"><span data-stu-id="06a7e-207">Add hello following line after `<h2>Submit</h2>`.</span></span> <span data-ttu-id="06a7e-208">Per il momento, hello `ViewBag.MessageCount` è vuoto.</span><span class="sxs-lookup"><span data-stu-id="06a7e-208">For now, hello `ViewBag.MessageCount` is empty.</span></span> <span data-ttu-id="06a7e-209">Il valore verrà inserito successivamente.</span><span class="sxs-lookup"><span data-stu-id="06a7e-209">You will populate it later.</span></span>
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. <span data-ttu-id="06a7e-210">L'interfaccia utente è stata implementata.</span><span class="sxs-lookup"><span data-stu-id="06a7e-210">You now have implemented your UI.</span></span> <span data-ttu-id="06a7e-211">È possibile premere **F5** toorun l'applicazione e verificare che l'aspetto di come previsto.</span><span class="sxs-lookup"><span data-stu-id="06a7e-211">You can press **F5** toorun your application and confirm that it looks as expected.</span></span>
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a><span data-ttu-id="06a7e-212">Scrittura di codice hello per l'invio di elementi della coda del Bus di servizio tooa</span><span class="sxs-lookup"><span data-stu-id="06a7e-212">Write hello code for submitting items tooa Service Bus queue</span></span>
<span data-ttu-id="06a7e-213">A questo punto, aggiungere codice per l'invio a coda tooa degli elementi.</span><span class="sxs-lookup"><span data-stu-id="06a7e-213">Now, add code for submitting items tooa queue.</span></span> <span data-ttu-id="06a7e-214">Creare prima di tutto una classe contenente le informazioni di connessione della coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="06a7e-214">First, you create a class that contains your Service Bus queue connection information.</span></span> <span data-ttu-id="06a7e-215">Inizializzare quindi la connessione da Global.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="06a7e-215">Then, initialize your connection from Global.aspx.cs.</span></span> <span data-ttu-id="06a7e-216">Infine, aggiornare il codice di invio hello creato in precedenza nella coda di Service Bus tooa HomeController.cs tooactually invia gli elementi.</span><span class="sxs-lookup"><span data-stu-id="06a7e-216">Finally, update hello submission code you created earlier in HomeController.cs tooactually submit items tooa Service Bus queue.</span></span>

1. <span data-ttu-id="06a7e-217">In **Esplora**, fare doppio clic su **FrontendWebRole** (progetto hello pulsante destro del mouse, non il ruolo hello).</span><span class="sxs-lookup"><span data-stu-id="06a7e-217">In **Solution Explorer**, right-click **FrontendWebRole** (right-click hello project, not hello role).</span></span> <span data-ttu-id="06a7e-218">Fare clic su **Aggiungi**, quindi su **Classe**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-218">Click **Add**, and then click **Class**.</span></span>
2. <span data-ttu-id="06a7e-219">Nome classe hello **QueueConnector.cs**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-219">Name hello class **QueueConnector.cs**.</span></span> <span data-ttu-id="06a7e-220">Fare clic su **Aggiungi** classe hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="06a7e-220">Click **Add** toocreate hello class.</span></span>
3. <span data-ttu-id="06a7e-221">A questo punto, aggiungere il codice che incapsula le informazioni di connessione hello e inizializza coda di Service Bus tooa connessione hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-221">Now, add code that encapsulates hello connection information and initializes hello connection tooa Service Bus queue.</span></span> <span data-ttu-id="06a7e-222">Sostituire hello l'intero contenuto di QueueConnector.cs con hello seguente di codice e immettere i valori per `your Service Bus namespace` (il nome dello spazio dei nomi) e `yourKey`, ovvero hello **chiave primaria** ottenuto in precedenza da hello Azure portale.</span><span class="sxs-lookup"><span data-stu-id="06a7e-222">Replace hello entire contents of QueueConnector.cs with hello following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is hello **primary key** you previously obtained from hello Azure portal.</span></span>
   
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
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. <span data-ttu-id="06a7e-223">Assicurarsi che venga chiamato il metodo **Initialize**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-223">Now, ensure that your **Initialize** method gets called.</span></span> <span data-ttu-id="06a7e-224">In **Esplora soluzioni** fare doppio clic su **Global.asax\Global.asax.cs**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-224">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span></span>
5. <span data-ttu-id="06a7e-225">Aggiungere hello successiva riga di codice alla fine hello hello **Application_Start** metodo.</span><span class="sxs-lookup"><span data-stu-id="06a7e-225">Add hello following line of code at hello end of hello **Application_Start** method.</span></span>
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. <span data-ttu-id="06a7e-226">Infine, aggiornare il codice di web hello creato in precedenza, per inviare gli elementi toohello coda.</span><span class="sxs-lookup"><span data-stu-id="06a7e-226">Finally, update hello web code you created earlier, to submit items toohello queue.</span></span> <span data-ttu-id="06a7e-227">In **Esplora soluzioni** fare doppio clic su **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-227">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span>
7. <span data-ttu-id="06a7e-228">Hello aggiornamento `Submit()` metodo (overload hello che non accetta parametri) come indicato di seguito tooget hello numero messaggi per coda hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-228">Update hello `Submit()` method (hello overload that takes no parameters) as follows tooget hello message count for hello queue.</span></span>
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. <span data-ttu-id="06a7e-229">Hello aggiornamento `Submit(OnlineOrder order)` metodo (hello dell'overload che accetta un parametro) come indicato di seguito toosubmit ordine coda toohello informazioni.</span><span class="sxs-lookup"><span data-stu-id="06a7e-229">Update hello `Submit(OnlineOrder order)` method (hello overload that takes one parameter) as follows toosubmit order information toohello queue.</span></span>
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. <span data-ttu-id="06a7e-230">È ora possibile eseguire nuovamente l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-230">You can now run hello application again.</span></span> <span data-ttu-id="06a7e-231">Ogni volta che si invia un ordine, aumenta il numero di messaggi hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-231">Each time you submit an order, hello message count increases.</span></span>
   
   ![][18]

## <a name="create-hello-worker-role"></a><span data-ttu-id="06a7e-232">Creare il ruolo di lavoro hello</span><span class="sxs-lookup"><span data-stu-id="06a7e-232">Create hello worker role</span></span>
<span data-ttu-id="06a7e-233">Si creerà ora ruolo di lavoro hello che elabora gli invii di ordine di hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-233">You will now create hello worker role that processes hello order submissions.</span></span> <span data-ttu-id="06a7e-234">Questo esempio viene utilizzato hello **ruolo di lavoro con coda di Service Bus** il modello di progetto di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="06a7e-234">This example uses hello **Worker Role with Service Bus Queue** Visual Studio project template.</span></span> <span data-ttu-id="06a7e-235">Le credenziali necessarie hello già ottenuto dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-235">You already obtained hello required credentials from hello portal.</span></span>

1. <span data-ttu-id="06a7e-236">Verificare che si è connessi a Visual Studio tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="06a7e-236">Make sure you have connected Visual Studio tooyour Azure account.</span></span>
2. <span data-ttu-id="06a7e-237">In Visual Studio, in **Esplora** destro la **ruoli** cartella hello **MultiTierApp** progetto.</span><span class="sxs-lookup"><span data-stu-id="06a7e-237">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under hello **MultiTierApp** project.</span></span>
3. <span data-ttu-id="06a7e-238">Fare clic su **Aggiungi**, quindi su **Nuovo progetto di ruolo di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-238">Click **Add**, and then click **New Worker Role Project**.</span></span> <span data-ttu-id="06a7e-239">Hello **Aggiungi nuovo progetto di ruolo** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="06a7e-239">hello **Add New Role Project** dialog box appears.</span></span>
   
   ![][26]
4. <span data-ttu-id="06a7e-240">In hello **Aggiungi nuovo progetto di ruolo** la finestra di dialogo, fare clic su **ruolo di lavoro con coda di Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-240">In hello **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span></span>
   
   ![][23]
5. <span data-ttu-id="06a7e-241">In hello **nome** casella, il progetto di hello nome **OrderProcessingRole**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-241">In hello **Name** box, name hello project **OrderProcessingRole**.</span></span> <span data-ttu-id="06a7e-242">Fare quindi clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-242">Then click **Add**.</span></span>
6. <span data-ttu-id="06a7e-243">Copiare una stringa di connessione hello ottenuto nel passaggio 9 di blocco per Appunti toohello sezione "Creare uno spazio dei nomi del Bus di servizio" hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-243">Copy hello connection string that you obtained in step 9 of hello "Create a Service Bus namespace" section toohello clipboard.</span></span>
7. <span data-ttu-id="06a7e-244">In **Esplora**, hello rapida **OrderProcessingRole** creato nel passaggio 5 (assicurarsi che si fa clic su **OrderProcessingRole** in **Ruoli**, e non hello classe).</span><span class="sxs-lookup"><span data-stu-id="06a7e-244">In **Solution Explorer**, right-click hello **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not hello class).</span></span> <span data-ttu-id="06a7e-245">Fare quindi clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-245">Then click **Properties**.</span></span>
8. <span data-ttu-id="06a7e-246">In hello **impostazioni** scheda di hello **proprietà** la finestra di dialogo, fare clic all'interno di hello **valore** casella **Microsoft.ServiceBus.ConnectionString**, quindi incollare il valore di endpoint hello copiato nel passaggio 6.</span><span class="sxs-lookup"><span data-stu-id="06a7e-246">On hello **Settings** tab of hello **Properties** dialog box, click inside hello **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste hello endpoint value you copied in step 6.</span></span>
   
   ![][25]
9. <span data-ttu-id="06a7e-247">Creare un **OnlineOrder** classe toorepresent hello ordini elaborati dalla coda hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-247">Create an **OnlineOrder** class toorepresent hello orders as you process them from hello queue.</span></span> <span data-ttu-id="06a7e-248">È possibile riutilizzare una classe creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="06a7e-248">You can reuse a class you have already created.</span></span> <span data-ttu-id="06a7e-249">In **Esplora**, hello rapida **OrderProcessingRole** classe (icona del pulsante destro del mouse hello classe, non il ruolo hello).</span><span class="sxs-lookup"><span data-stu-id="06a7e-249">In **Solution Explorer**, right-click hello **OrderProcessingRole** class (right-click hello class icon, not hello role).</span></span> <span data-ttu-id="06a7e-250">Fare clic su **Aggiungi**, quindi su **Elemento esistente**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-250">Click **Add**, then click **Existing Item**.</span></span>
10. <span data-ttu-id="06a7e-251">Individuare la sottocartella toohello per **FrontendWebRole\Models**e quindi fare doppio clic su **Onlineorder** tooadd è toothis progetto.</span><span class="sxs-lookup"><span data-stu-id="06a7e-251">Browse toohello subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** tooadd it toothis project.</span></span>
11. <span data-ttu-id="06a7e-252">In **WorkerRole.cs**, modificare il valore di hello di hello **QueueName** variabile `"ProcessingQueue"` troppo`"OrdersQueue"` come illustrato nel seguente codice hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-252">In **WorkerRole.cs**, change hello value of hello **QueueName** variable from `"ProcessingQueue"` too`"OrdersQueue"` as shown in hello following code.</span></span>
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. <span data-ttu-id="06a7e-253">Aggiungere hello seguente istruzione using nella parte superiore di hello del file WorkerRole.cs hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-253">Add hello following using statement at hello top of hello WorkerRole.cs file.</span></span>
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. <span data-ttu-id="06a7e-254">In hello `Run()` funzione, all'interno di hello `OnMessage()` chiamare, sostituire il contenuto di hello di hello `try` clausola con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="06a7e-254">In hello `Run()` function, inside hello `OnMessage()` call, replace hello contents of hello `try` clause with hello following code.</span></span>
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. <span data-ttu-id="06a7e-255">È stata completata l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="06a7e-255">You have completed hello application.</span></span> <span data-ttu-id="06a7e-256">È possibile testare un'applicazione hello completo facendo clic con il progetto MultiTierApp hello in Esplora soluzioni selezionare **imposta come progetto di avvio**e quindi premendo F5.</span><span class="sxs-lookup"><span data-stu-id="06a7e-256">You can test hello full application by right-clicking hello MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span></span> <span data-ttu-id="06a7e-257">Si noti che il numero di messaggi non aumenta perché il ruolo di lavoro hello elabora gli elementi dalla coda hello e li contrassegna come completata.</span><span class="sxs-lookup"><span data-stu-id="06a7e-257">Note that the message count does not increment, because hello worker role processes items from hello queue and marks them as complete.</span></span> <span data-ttu-id="06a7e-258">È possibile visualizzare l'output di traccia hello del ruolo di lavoro visualizzando hello interfaccia utente emulatore di calcolo di Azure.</span><span class="sxs-lookup"><span data-stu-id="06a7e-258">You can see hello trace output of your worker role by viewing hello Azure Compute Emulator UI.</span></span> <span data-ttu-id="06a7e-259">È possibile farlo facendo clic sull'icona di emulatore hello nell'area di notifica hello della barra delle applicazioni e selezionando **Mostra interfaccia utente di emulatore di calcolo**.</span><span class="sxs-lookup"><span data-stu-id="06a7e-259">You can do this by right-clicking hello emulator icon in hello notification area of your taskbar and selecting **Show Compute Emulator UI**.</span></span>
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a><span data-ttu-id="06a7e-260">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06a7e-260">Next steps</span></span>
<span data-ttu-id="06a7e-261">toolearn ulteriori informazioni su Service Bus, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="06a7e-261">toolearn more about Service Bus, see hello following resources:</span></span>  

* <span data-ttu-id="06a7e-262">[Documentazione sul bus di servizio di Azure][sbdocs]</span><span class="sxs-lookup"><span data-stu-id="06a7e-262">[Azure Service Bus documentation][sbdocs]</span></span>  
* <span data-ttu-id="06a7e-263">[Pagina del servizio Bus di servizio][sbacom]</span><span class="sxs-lookup"><span data-stu-id="06a7e-263">[Service Bus service page][sbacom]</span></span>  
* <span data-ttu-id="06a7e-264">[Come tooUse code di Service Bus][sbacomqhowto]</span><span class="sxs-lookup"><span data-stu-id="06a7e-264">[How tooUse Service Bus Queues][sbacomqhowto]</span></span>  

<span data-ttu-id="06a7e-265">toolearn ulteriori informazioni su scenari a più livelli, vedere:</span><span class="sxs-lookup"><span data-stu-id="06a7e-265">toolearn more about multi-tier scenarios, see:</span></span>  

* <span data-ttu-id="06a7e-266">[Applicazione .NET multilivello con tabelle, code e BLOB di archiviazione di Azure][mutitierstorage]</span><span class="sxs-lookup"><span data-stu-id="06a7e-266">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span></span>  

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
