---
title: esercitazione REST Bus aaaService con l'inoltro di Azure | Documenti Microsoft
description: Compilare una semplice applicazione host di inoltro del bus di servizio di Azure che espone un'interfaccia basata su REST.
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: b68650993a0390e7cef891ccb4236095cd86d4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="5beab-103">Esercitazione su REST per l'inoltro WCF di Azure</span><span class="sxs-lookup"><span data-stu-id="5beab-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="5beab-104">In questa esercitazione viene descritto come un semplice inoltro Azure toobuild host applicazione che espone un'interfaccia basata su REST.</span><span class="sxs-lookup"><span data-stu-id="5beab-104">This tutorial describes how toobuild a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="5beab-105">REST consente a un client web, ad esempio un web browser, hello tooaccess le richieste API del Bus di servizio tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="5beab-105">REST enables a web client, such as a web browser, tooaccess hello Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="5beab-106">esercitazione Hello utilizza tooconstruct programmazione modello hello REST di Windows Communication Foundation (WCF) un servizio REST sul Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="5beab-106">hello tutorial uses hello Windows Communication Foundation (WCF) REST programming model tooconstruct a REST service on Service Bus.</span></span> <span data-ttu-id="5beab-107">Per ulteriori informazioni, vedere [il modello di programmazione REST WCF](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) e [progettazione e implementazione di servizi](/dotnet/framework/wcf/designing-and-implementing-services) in hello documentazione WCF.</span><span class="sxs-lookup"><span data-stu-id="5beab-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in hello WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="5beab-108">Passaggio 1: Creare uno spazio dei nomi</span><span class="sxs-lookup"><span data-stu-id="5beab-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="5beab-109">utilizzando toobegin hello le funzionalità di inoltro in Azure, è innanzitutto necessario creare uno spazio dei nomi del servizio.</span><span class="sxs-lookup"><span data-stu-id="5beab-109">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="5beab-110">Uno spazio dei nomi funge da contenitore di ambito in cui indirizzare le risorse di Azure nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5beab-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="5beab-111">Seguire hello [le istruzioni qui](relay-create-namespace-portal.md) toocreate uno spazio dei nomi di inoltro.</span><span class="sxs-lookup"><span data-stu-id="5beab-111">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a><span data-ttu-id="5beab-112">Passaggio 2: Definire un toouse contratto di servizio WCF basato su REST con l'inoltro di Azure</span><span class="sxs-lookup"><span data-stu-id="5beab-112">Step 2: Define a REST-based WCF service contract toouse with Azure Relay</span></span>

<span data-ttu-id="5beab-113">Quando si crea un servizio in stile REST WCF, è necessario definire il contratto di hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-113">When you create a WCF REST-style service, you must define hello contract.</span></span> <span data-ttu-id="5beab-114">contratto Hello specifica quali operazioni hello host supporta.</span><span class="sxs-lookup"><span data-stu-id="5beab-114">hello contract specifies what operations hello host supports.</span></span> <span data-ttu-id="5beab-115">Un'operazione di servizio può essere considerata come un metodo del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="5beab-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="5beab-116">I contratti vengono creati definendo un'interfaccia C++, C# o Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="5beab-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="5beab-117">Ogni metodo nell'interfaccia hello corrisponde tooa operazione del servizio specifica.</span><span class="sxs-lookup"><span data-stu-id="5beab-117">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="5beab-118">Hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attributo deve essere applicato tooeach interfaccia e hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attributo deve essere applicato tooeach operazione.</span><span class="sxs-lookup"><span data-stu-id="5beab-118">hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied tooeach interface, and hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied tooeach operation.</span></span> <span data-ttu-id="5beab-119">Se un metodo in un'interfaccia con hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) privo di hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), questo metodo non è esposto.</span><span class="sxs-lookup"><span data-stu-id="5beab-119">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="5beab-120">codice Hello usato per queste attività è illustrata nell'esempio hello procedura hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-120">hello code used for these tasks is shown in hello example following hello procedure.</span></span>

<span data-ttu-id="5beab-121">la differenza principale tra un contratto WCF e un contratto in stile REST Hello è hello aggiunta di una proprietà di toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="5beab-121">hello primary difference between a WCF contract and a REST-style contract is hello addition of a property toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="5beab-122">Questa proprietà consente di toomap un metodo al metodo di interfaccia tooa su hello altro lato dell'interfaccia hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-122">This property enables you toomap a method in your interface tooa method on hello other side of hello interface.</span></span> <span data-ttu-id="5beab-123">In questo caso, si utilizzerà [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink tooHTTP un metodo GET.</span><span class="sxs-lookup"><span data-stu-id="5beab-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink a method tooHTTP GET.</span></span> <span data-ttu-id="5beab-124">In questo modo il Bus di servizio tooaccurately recuperare e interpretare i comandi inviati toohello interfaccia.</span><span class="sxs-lookup"><span data-stu-id="5beab-124">This allows Service Bus tooaccurately retrieve and interpret commands sent toohello interface.</span></span>

### <a name="toocreate-a-contract-with-an-interface"></a><span data-ttu-id="5beab-125">un contratto con un'interfaccia toocreate</span><span class="sxs-lookup"><span data-stu-id="5beab-125">toocreate a contract with an interface</span></span>

1. <span data-ttu-id="5beab-126">Aprire Visual Studio come amministratore: il programma hello pulsante destro del mouse in hello **avviare** menu e quindi fare clic su **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="5beab-126">Open Visual Studio as an administrator: right-click hello program in hello **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="5beab-127">Creare un nuovo progetto di applicazione console.</span><span class="sxs-lookup"><span data-stu-id="5beab-127">Create a new console application project.</span></span> <span data-ttu-id="5beab-128">Fare clic su hello **File** dal menu **New**, quindi selezionare **progetto**.</span><span class="sxs-lookup"><span data-stu-id="5beab-128">Click hello **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="5beab-129">In hello **nuovo progetto** nella finestra di dialogo fare clic su **Visual c#**selezionare hello **applicazione Console** , modello e specificare il nome **ImageListener**.</span><span class="sxs-lookup"><span data-stu-id="5beab-129">In hello **New Project** dialog box, click **Visual C#**, select hello **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="5beab-130">Utilizzare hello predefinito **percorso**.</span><span class="sxs-lookup"><span data-stu-id="5beab-130">Use hello default **Location**.</span></span> <span data-ttu-id="5beab-131">Fare clic su **OK** progetto hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="5beab-131">Click **OK** toocreate hello project.</span></span>
3. <span data-ttu-id="5beab-132">Per un progetto C#, Visual Studio crea un file `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="5beab-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="5beab-133">Questa classe contiene un oggetto vuoto `Main()` (metodo), necessari per un toobuild di progetto applicazione console in modo corretto.</span><span class="sxs-lookup"><span data-stu-id="5beab-133">This class contains an empty `Main()` method, required for a console application project toobuild correctly.</span></span>
4. <span data-ttu-id="5beab-134">Aggiungere riferimenti tooService Bus e **System.ServiceModel.dll** toohello progetto per l'installazione del pacchetto NuGet di Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-134">Add references tooService Bus and **System.ServiceModel.dll** toohello project by installing hello Service Bus NuGet package.</span></span> <span data-ttu-id="5beab-135">Questo pacchetto aggiunge automaticamente le librerie del Bus di servizio toohello riferimenti, nonché hello WCF **System. ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="5beab-135">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="5beab-136">In Esplora soluzioni fare doppio clic su hello **ImageListener** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5beab-136">In Solution Explorer, right-click hello **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="5beab-137">Fare clic su hello **Sfoglia** tab, quindi cercare `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="5beab-137">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="5beab-138">Fare clic su **installare**e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="5beab-138">Click **Install**, and accept hello terms of use.</span></span>
5. <span data-ttu-id="5beab-139">È necessario aggiungere in modo esplicito un riferimento troppo**System.ServiceModel.Web.dll** toohello progetto:</span><span class="sxs-lookup"><span data-stu-id="5beab-139">You must explicitly add a reference too**System.ServiceModel.Web.dll** toohello project:</span></span>
   
    <span data-ttu-id="5beab-140">a.</span><span class="sxs-lookup"><span data-stu-id="5beab-140">a.</span></span> <span data-ttu-id="5beab-141">In Esplora soluzioni fare doppio clic su hello **riferimenti** nella cartella di progetto hello, quindi fare clic su **Aggiungi riferimento**.</span><span class="sxs-lookup"><span data-stu-id="5beab-141">In Solution Explorer, right-click hello **References** folder under hello project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="5beab-142">b.</span><span class="sxs-lookup"><span data-stu-id="5beab-142">b.</span></span> <span data-ttu-id="5beab-143">In hello **Aggiungi riferimento** finestra di dialogo fare clic su hello **Framework** scheda sul lato sinistro hello e hello **ricerca** digitare **System.ServiceModel.Web** .</span><span class="sxs-lookup"><span data-stu-id="5beab-143">In hello **Add Reference** dialog box, click hello **Framework** tab on hello left-hand side and in hello **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="5beab-144">Seleziona hello **System.ServiceModel.Web** casella di controllo, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5beab-144">Select hello **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="5beab-145">Aggiungere il seguente hello `using` istruzioni nella parte superiore di hello del file Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-145">Add hello following `using` statements at hello top of hello Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="5beab-146">[System. ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) uno spazio dei nomi hello che abilita l'accesso programmatico toobasic funzionalità di WCF.</span><span class="sxs-lookup"><span data-stu-id="5beab-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables programmatic access toobasic features of WCF.</span></span> <span data-ttu-id="5beab-147">Inoltro WCF Usa molti degli oggetti hello e degli attributi WCF toodefine di contratti di servizio.</span><span class="sxs-lookup"><span data-stu-id="5beab-147">WCF Relay uses many of hello objects and attributes of WCF toodefine service contracts.</span></span> <span data-ttu-id="5beab-148">Questo spazio dei nomi viene usato nella maggior parte delle applicazioni di inoltro.</span><span class="sxs-lookup"><span data-stu-id="5beab-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="5beab-149">Analogamente, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) consentono di definire il canale hello, ovvero hello oggetto usato per comunicare con l'inoltro di Azure e hello web browser client.</span><span class="sxs-lookup"><span data-stu-id="5beab-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define hello channel, which is hello object through which you communicate with Azure Relay and hello client web browser.</span></span> <span data-ttu-id="5beab-150">Infine, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contiene i tipi di hello che consentono di applicazioni basate sul web toocreate.</span><span class="sxs-lookup"><span data-stu-id="5beab-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains hello types that enable you toocreate web-based applications.</span></span>
7. <span data-ttu-id="5beab-151">Rinominare hello `ImageListener` dello spazio dei nomi troppo**ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="5beab-151">Rename hello `ImageListener` namespace too**Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="5beab-152">Dopo la parentesi graffa di dichiarazione dello spazio dei nomi hello di hello, è possibile definire direttamente una nuova interfaccia denominata **IImageContract** e applicare hello **ServiceContractAttribute** interfaccia toohello attributo con un valore di `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="5beab-152">Directly after hello opening curly brace of hello namespace declaration, define a new interface named **IImageContract** and apply hello **ServiceContractAttribute** attribute toohello interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="5beab-153">il valore di spazio dei nomi Hello è diverso dallo spazio dei nomi hello usato nell'ambito di hello del codice.</span><span class="sxs-lookup"><span data-stu-id="5beab-153">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="5beab-154">valore dello spazio dei nomi Hello viene usato come identificatore univoco per questo contratto e deve disporre di informazioni sulla versione.</span><span class="sxs-lookup"><span data-stu-id="5beab-154">hello namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="5beab-155">Per altre informazioni, vedere [Controllo delle versioni del servizio](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="5beab-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="5beab-156">Specificare in modo esplicito lo spazio dei nomi hello impedisce l'aggiunta il nome del contratto toohello valore dello spazio dei nomi predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-156">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="5beab-157">All'interno di hello `IImageContract` l'interfaccia, dichiarare un metodo per hello singola operazione hello `IImageContract` espone contratto in hello interfaccia e applicare hello `OperationContractAttribute` attributo toohello metodo che si vuole tooexpose come parte del servizio pubblico hello Bus contratto.</span><span class="sxs-lookup"><span data-stu-id="5beab-157">Within hello `IImageContract` interface, declare a method for hello single operation hello `IImageContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="5beab-158">In hello **OperationContract** attributo, aggiungere hello **WebGet** valore.</span><span class="sxs-lookup"><span data-stu-id="5beab-158">In hello **OperationContract** attribute, add hello **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="5beab-159">In questo modo consente hello tooroute servizio di inoltro richieste HTTP GET troppo`GetImage`, hello tootranslate restituiscono i valori e `GetImage` in una risposta HTTP GETRESPONSE.</span><span class="sxs-lookup"><span data-stu-id="5beab-159">Doing so enables hello relay service tooroute HTTP GET requests too`GetImage`, and tootranslate hello return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="5beab-160">Più avanti nell'esercitazione di hello, si utilizzerà un tooaccess browser web, questo metodo e immagine hello toodisplay nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-160">Later in hello tutorial, you will use a web browser tooaccess this method, and toodisplay hello image in hello browser.</span></span>
11. <span data-ttu-id="5beab-161">Direttamente dopo hello `IImageContract` definizione, dichiarare un canale che eredita da entrambi hello `IImageContract` e `IClientChannel` interfacce.</span><span class="sxs-lookup"><span data-stu-id="5beab-161">Directly after hello `IImageContract` definition, declare a channel that inherits from both hello `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="5beab-162">Un canale è l'oggetto WCF hello attraverso cui client e servizio hello passare informazioni tooeach altri.</span><span class="sxs-lookup"><span data-stu-id="5beab-162">A channel is hello WCF object through which hello service and client pass information tooeach other.</span></span> <span data-ttu-id="5beab-163">In un secondo momento, si creerà il canale hello nell'applicazione host.</span><span class="sxs-lookup"><span data-stu-id="5beab-163">Later, you will create hello channel in your host application.</span></span> <span data-ttu-id="5beab-164">Inoltro Azure utilizza quindi questo canale toopass hello richieste GET HTTP dal hello browser tooyour **GetImage** implementazione.</span><span class="sxs-lookup"><span data-stu-id="5beab-164">Azure Relay then uses this channel toopass hello HTTP GET requests from hello browser tooyour **GetImage** implementation.</span></span> <span data-ttu-id="5beab-165">inoltro Hello utilizza inoltre hello di hello canale tootake **GetImage** valore restituito e viene convertito in una risposta HTTP GETRESPONSE per browser client hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-165">hello relay also uses hello channel tootake hello **GetImage** return value and translate it into an HTTP GETRESPONSE for hello client browser.</span></span>
12. <span data-ttu-id="5beab-166">Da hello **compilare** menu, fare clic su **Compila soluzione** accuratezza hello tooconfirm del lavoro svolto finora.</span><span class="sxs-lookup"><span data-stu-id="5beab-166">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="5beab-167">Esempio</span><span class="sxs-lookup"><span data-stu-id="5beab-167">Example</span></span>
<span data-ttu-id="5beab-168">Hello di codice seguente mostra un'interfaccia di base che definisce un contratto di inoltro WCF.</span><span class="sxs-lookup"><span data-stu-id="5beab-168">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a><span data-ttu-id="5beab-169">Passaggio 3: Implementare un toouse di contratto del servizio Bus di servizio WCF basato su REST</span><span class="sxs-lookup"><span data-stu-id="5beab-169">Step 3: Implement a REST-based WCF service contract toouse Service Bus</span></span>
<span data-ttu-id="5beab-170">Creazione di un servizio di inoltro WCF di tipo REST è necessario innanzitutto creare contratto hello, che viene definito tramite un'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="5beab-170">Creating a REST-style WCF Relay service requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="5beab-171">passaggio successivo Hello è interfaccia hello tooimplement.</span><span class="sxs-lookup"><span data-stu-id="5beab-171">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="5beab-172">Ciò comporta la creazione di una classe denominata **ImageService** che implementa hello definito dall'utente **IImageContract** interfaccia.</span><span class="sxs-lookup"><span data-stu-id="5beab-172">This involves creating a class named **ImageService** that implements hello user-defined **IImageContract** interface.</span></span> <span data-ttu-id="5beab-173">Dopo aver implementato il contratto di hello, configurare l'interfaccia hello utilizzando un file app. config.</span><span class="sxs-lookup"><span data-stu-id="5beab-173">After you implement hello contract, you then configure hello interface using an App.config file.</span></span> <span data-ttu-id="5beab-174">file di configurazione Hello contiene le informazioni necessarie per un'applicazione hello, ad esempio nome hello del servizio di hello, il nome di hello del contratto hello e tipo hello di protocollo è toocommunicate utilizzato con il servizio di inoltro hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-174">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="5beab-175">Nell'esempio hello hello procedura viene fornito codice di Hello utilizzato per queste attività.</span><span class="sxs-lookup"><span data-stu-id="5beab-175">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

<span data-ttu-id="5beab-176">Come con i passaggi precedenti hello, c'è differenza minima tra l'implementazione di un contratto in stile REST e un contratto di inoltro WCF.</span><span class="sxs-lookup"><span data-stu-id="5beab-176">As with hello previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="tooimplement-a-rest-style-service-bus-contract"></a><span data-ttu-id="5beab-177">contratto del Bus di servizio tooimplement un stile REST</span><span class="sxs-lookup"><span data-stu-id="5beab-177">tooimplement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="5beab-178">Creare una nuova classe denominata **ImageService** direttamente dopo la definizione di hello di hello **IImageContract** interfaccia.</span><span class="sxs-lookup"><span data-stu-id="5beab-178">Create a new class named **ImageService** directly after hello definition of hello **IImageContract** interface.</span></span> <span data-ttu-id="5beab-179">Hello **ImageService** implementa hello **IImageContract** interfaccia.</span><span class="sxs-lookup"><span data-stu-id="5beab-179">hello **ImageService** class implements hello **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="5beab-180">Le implementazioni di interfaccia tooother simili, è possibile implementare definizione hello in un file diverso.</span><span class="sxs-lookup"><span data-stu-id="5beab-180">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="5beab-181">Tuttavia, per questa esercitazione, implementazione hello viene visualizzato in hello lo stesso file di definizione di interfaccia hello e `Main()` metodo.</span><span class="sxs-lookup"><span data-stu-id="5beab-181">However, for this tutorial, hello implementation appears in hello same file as hello interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="5beab-182">Applicare hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attributo toohello **IImageService** tooindicate di classe che hello classe è un'implementazione di un contratto WCF.</span><span class="sxs-lookup"><span data-stu-id="5beab-182">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello **IImageService** class tooindicate that hello class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="5beab-183">Come accennato in precedenza, questo spazio dei nomi non è uno spazio dei nomi tradizionale.</span><span class="sxs-lookup"><span data-stu-id="5beab-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="5beab-184">In alternativa, è parte dell'architettura WCF che identifica il contratto di hello hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-184">Instead, it is part of hello WCF architecture that identifies hello contract.</span></span> <span data-ttu-id="5beab-185">Per ulteriori informazioni, vedere hello [nomi di contratto dati](https://msdn.microsoft.com/library/ms731045.aspx) argomento nella documentazione di WCF hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-185">For more information, see hello [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in hello WCF documentation.</span></span>
3. <span data-ttu-id="5beab-186">Aggiungere un progetto di tooyour immagine jpg.</span><span class="sxs-lookup"><span data-stu-id="5beab-186">Add a .jpg image tooyour project.</span></span>  
   
    <span data-ttu-id="5beab-187">Si tratta di un'immagine contenente il servizio hello in hello browser di ricezione.</span><span class="sxs-lookup"><span data-stu-id="5beab-187">This is a picture that hello service displays in hello receiving browser.</span></span> <span data-ttu-id="5beab-188">Fare clic con il pulsante destro del mouse sul progetto e quindi scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5beab-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="5beab-189">Fare clic su **Elemento esistente**.</span><span class="sxs-lookup"><span data-stu-id="5beab-189">Then click **Existing Item**.</span></span> <span data-ttu-id="5beab-190">Hello utilizzare **Aggiungi elemento esistente** della finestra di dialogo toobrowse tooan appropriato. jpg e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5beab-190">Use hello **Add Existing Item** dialog box toobrowse tooan appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="5beab-191">Quando si aggiungono file hello, assicurarsi che **tutti i file** è selezionata in hello riepilogo Avanti toohello **nome File:** campo.</span><span class="sxs-lookup"><span data-stu-id="5beab-191">When adding hello file, make sure that **All Files** is selected in hello drop-down list next toohello **File name:** field.</span></span> <span data-ttu-id="5beab-192">rest Hello di questa esercitazione si presuppone che hello nome dell'immagine di hello sia "image.jpg".</span><span class="sxs-lookup"><span data-stu-id="5beab-192">hello rest of this tutorial assumes that hello name of hello image is "image.jpg".</span></span> <span data-ttu-id="5beab-193">Se si dispone di un file diverso, si verrà toorename hello immagine o modificare il codice toocompensate.</span><span class="sxs-lookup"><span data-stu-id="5beab-193">If you have a different file, you will have toorename hello image, or change your code toocompensate.</span></span>
4. <span data-ttu-id="5beab-194">Assicurarsi che hello in esecuzione del servizio è possibile trovare il file di immagine hello, in toomake **Esplora soluzioni** fare clic sul file di immagine hello, quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="5beab-194">toomake sure that hello running service can find hello image file, in **Solution Explorer** right-click hello image file, then click **Properties**.</span></span> <span data-ttu-id="5beab-195">In hello **proprietà** riquadro, impostare **copiare tooOutput Directory** troppo**copia se più recente**.</span><span class="sxs-lookup"><span data-stu-id="5beab-195">In hello **Properties** pane, set **Copy tooOutput Directory** too**Copy if newer**.</span></span>
5. <span data-ttu-id="5beab-196">Aggiungere un riferimento toohello **System.Drawing.dll** toohello di assembly del progetto e aggiungere associate riportate di seguito hello `using` istruzioni.</span><span class="sxs-lookup"><span data-stu-id="5beab-196">Add a reference toohello **System.Drawing.dll** assembly toohello project, and also add hello following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="5beab-197">In hello **ImageService** classe, aggiungere hello seguenti costruttore che carica hello bitmap e prepara toosend il browser client toohello.</span><span class="sxs-lookup"><span data-stu-id="5beab-197">In hello **ImageService** class, add hello following constructor that loads hello bitmap and prepares toosend it toohello client browser.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. <span data-ttu-id="5beab-198">Direttamente dopo il codice precedente hello, aggiungere il seguente hello **GetImage** metodo hello **ImageService** messaggio tooreturn HTTP di classe che contiene l'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-198">Directly after hello previous code, add hello following **GetImage** method in hello **ImageService** class tooreturn an HTTP message that contains hello image.</span></span>
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    <span data-ttu-id="5beab-199">Questa implementazione utilizza **MemoryStream** tooretrieve hello immagine e prepararla per lo streaming toohello browser.</span><span class="sxs-lookup"><span data-stu-id="5beab-199">This implementation uses **MemoryStream** tooretrieve hello image and prepare it for streaming toohello browser.</span></span> <span data-ttu-id="5beab-200">Avvia la posizione del flusso hello da zero, dichiara il contenuto di flusso hello in formato jpeg e flussi di informazioni hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-200">It starts hello stream position at zero, declares hello stream content as a jpeg, and streams hello information.</span></span>
8. <span data-ttu-id="5beab-201">Da hello **compilare** menu, fare clic su **Compila soluzione**.</span><span class="sxs-lookup"><span data-stu-id="5beab-201">From hello **Build** menu, click **Build Solution**.</span></span>

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a><span data-ttu-id="5beab-202">configurazione di hello toodefine per l'esecuzione del servizio web hello sul Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="5beab-202">toodefine hello configuration for running hello web service on Service Bus</span></span>
1. <span data-ttu-id="5beab-203">In **Esplora**, fare doppio clic su **app** tooopen nell'editor di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-203">In **Solution Explorer**, double-click **App.config** tooopen it in hello Visual Studio editor.</span></span>
   
    <span data-ttu-id="5beab-204">Hello **app** file include il nome di servizio hello endpoint (vale a dire hello location inoltro Azure espone per i client e host toocommunicate reciprocamente) e associazione (tipo hello di protocollo utilizzato toocommunicate).</span><span class="sxs-lookup"><span data-stu-id="5beab-204">hello **App.config** file includes hello service name, endpoint (that is, hello location Azure Relay exposes for clients and hosts toocommunicate with each other), and binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="5beab-205">Hello differenza principale è tale endpoint di servizio hello configurato si riferisce tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) associazione.</span><span class="sxs-lookup"><span data-stu-id="5beab-205">hello main difference here is that hello configured service endpoint refers tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="5beab-206">Hello `<system.serviceModel>` elemento XML è un elemento WCF che definisce uno o più servizi.</span><span class="sxs-lookup"><span data-stu-id="5beab-206">hello `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="5beab-207">In questo caso, è endpoint e nome del servizio utilizzato toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-207">Here, it is used toodefine hello service name and endpoint.</span></span> <span data-ttu-id="5beab-208">Nella parte inferiore di hello di hello `<system.serviceModel>` elemento (ma si trovano all'interno `<system.serviceModel>`), aggiungere un `<bindings>` elemento che dispone di hello dopo contenuto.</span><span class="sxs-lookup"><span data-stu-id="5beab-208">At hello bottom of hello `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has hello following content.</span></span> <span data-ttu-id="5beab-209">Definisce le associazioni hello usate in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-209">This defines hello bindings used in hello application.</span></span> <span data-ttu-id="5beab-210">È possibile definire più associazioni, ma per questa esercitazione se ne definisce una sola.</span><span class="sxs-lookup"><span data-stu-id="5beab-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    <span data-ttu-id="5beab-211">codice precedente Hello definisce un inoltro WCF [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding con **relayClientAuthenticationType** impostare troppo**Nessuno**.</span><span class="sxs-lookup"><span data-stu-id="5beab-211">hello previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set too**None**.</span></span> <span data-ttu-id="5beab-212">Questa impostazione indica che un endpoint che utilizza questa associazione non richiede le credenziali client.</span><span class="sxs-lookup"><span data-stu-id="5beab-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="5beab-213">Dopo aver hello `<bindings>` elemento, aggiungere un `<services>` elemento.</span><span class="sxs-lookup"><span data-stu-id="5beab-213">After hello `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="5beab-214">Associazioni toohello simili, è possibile definire più servizi in un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="5beab-214">Similar toohello bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="5beab-215">Tuttavia, per questa esercitazione, se ne definisce solo uno.</span><span class="sxs-lookup"><span data-stu-id="5beab-215">However, for this tutorial, you define only one.</span></span>
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    <span data-ttu-id="5beab-216">Questo passaggio Configura un servizio che utilizza valori predefiniti definito in precedenza hello **webHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="5beab-216">This step configures a service that uses hello previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="5beab-217">Utilizza inoltre il valore predefinito di hello **sbTokenProvider**, che è definito nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-217">It also uses hello default **sbTokenProvider**, which is defined in hello next step.</span></span>
4. <span data-ttu-id="5beab-218">Dopo aver hello `<services>` elemento, creare un `<behaviors>` elemento con hello contenuto seguente, sostituendo "SAS_KEY" con hello *firma di accesso condiviso* chiave (SAS) è stato ottenuto in precedenza da hello [portale di Azure ][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="5beab-218">After hello `<services>` element, create a `<behaviors>` element with hello following content, replacing "SAS_KEY" with hello *Shared Access Signature* (SAS) key you previously obtained from hello [Azure portal][Azure portal].</span></span>
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. <span data-ttu-id="5beab-219">Ancora in App. config, hello `<appSettings>` elemento, valore di stringa di sostituzione hello intera connessione con stringa di connessione hello ottenuto dal portale hello in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5beab-219">Still in App.config, in hello `<appSettings>` element, replace hello entire connection string value with hello connection string you previously obtained from hello portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="5beab-220">Da hello **compilare** menu, fare clic su **Compila soluzione** dell'intera soluzione hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="5beab-220">From hello **Build** menu, click **Build Solution** toobuild hello entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="5beab-221">Esempio</span><span class="sxs-lookup"><span data-stu-id="5beab-221">Example</span></span>
<span data-ttu-id="5beab-222">Hello codice seguente viene illustrato implementazione hello di contratto e del servizio per un servizio basato su REST che è in esecuzione sul Bus di servizio utilizzando hello **WebHttpRelayBinding** associazione.</span><span class="sxs-lookup"><span data-stu-id="5beab-222">hello following code shows hello contract and service implementation for a REST-based service that is running on  Service Bus using hello **WebHttpRelayBinding** binding.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="5beab-223">Hello riportato di seguito hello file app. config associato al servizio hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-223">hello following example shows hello App.config file associated with hello service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove hello ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a><span data-ttu-id="5beab-224">Passaggio 4: Host toouse di servizio WCF basato su REST hello Azure inoltro</span><span class="sxs-lookup"><span data-stu-id="5beab-224">Step 4: Host hello REST-based WCF service toouse Azure Relay</span></span>
<span data-ttu-id="5beab-225">Questo passaggio viene descritto come toorun un sito web del servizio con un'applicazione console relè WCF.</span><span class="sxs-lookup"><span data-stu-id="5beab-225">This step describes how toorun a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="5beab-226">Nell'esempio hello hello procedura, viene fornito un elenco completo del codice hello scritto in questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="5beab-226">A complete listing of hello code written in this step is provided in hello example following hello procedure.</span></span>

### <a name="toocreate-a-base-address-for-hello-service"></a><span data-ttu-id="5beab-227">un indirizzo di base per il servizio hello toocreate</span><span class="sxs-lookup"><span data-stu-id="5beab-227">toocreate a base address for hello service</span></span>
1. <span data-ttu-id="5beab-228">In hello `Main()` dichiarazione di funzione, creare uno spazio dei nomi di variabile toostore hello del progetto.</span><span class="sxs-lookup"><span data-stu-id="5beab-228">In hello `Main()` function declaration, create a variable toostore hello namespace of your project.</span></span> <span data-ttu-id="5beab-229">Verificare che tooreplace `yourNamespace` con nome hello dello spazio dei nomi di inoltro hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5beab-229">Make sure tooreplace `yourNamespace` with hello name of hello Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="5beab-230">Bus di servizio utilizza il nome di hello del toocreate dello spazio dei nomi, un URI univoco.</span><span class="sxs-lookup"><span data-stu-id="5beab-230">Service Bus uses hello name of your namespace toocreate a unique URI.</span></span>
2. <span data-ttu-id="5beab-231">Creare un `Uri` istanza per l'indirizzo di base hello servizio hello basato sullo spazio dei nomi hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-231">Create a `Uri` instance for hello base address of hello service that is based on hello namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a><span data-ttu-id="5beab-232">toocreate e configurare l'host del servizio web hello</span><span class="sxs-lookup"><span data-stu-id="5beab-232">toocreate and configure hello web service host</span></span>
* <span data-ttu-id="5beab-233">Creare l'host del servizio web hello, utilizzando l'indirizzo URI hello creato in precedenza in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="5beab-233">Create hello web service host, using hello URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="5beab-234">host del servizio Hello è oggetto WCF hello che crea un'istanza di un'applicazione hello host.</span><span class="sxs-lookup"><span data-stu-id="5beab-234">hello service host is hello WCF object that instantiates hello host application.</span></span> <span data-ttu-id="5beab-235">Questo esempio passa il tipo di hello dell'host si desidera toocreate (un **ImageService**), e anche hello indirizzo in cui si desidera un'applicazione host tooexpose hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-235">This example passes it hello type of host you want toocreate (an **ImageService**), and also hello address at which you want tooexpose hello host application.</span></span>

### <a name="toorun-hello-web-service-host"></a><span data-ttu-id="5beab-236">host del servizio web hello toorun</span><span class="sxs-lookup"><span data-stu-id="5beab-236">toorun hello web service host</span></span>
1. <span data-ttu-id="5beab-237">Aprire il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-237">Open hello service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="5beab-238">servizio Hello è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5beab-238">hello service is now running.</span></span>
2. <span data-ttu-id="5beab-239">Visualizzare un messaggio che indica che è in esecuzione il servizio hello e come toostop hello del servizio.</span><span class="sxs-lookup"><span data-stu-id="5beab-239">Display a message indicating that hello service is running, and how toostop hello service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="5beab-240">Al termine, chiudere l'host del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-240">When finished, close hello service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="5beab-241">Esempio</span><span class="sxs-lookup"><span data-stu-id="5beab-241">Example</span></span>
<span data-ttu-id="5beab-242">Hello di esempio seguente include il contratto di servizio hello e l'implementazione dai passaggi precedenti nel servizio di hello di esercitazione e ospita hello in un'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="5beab-242">hello following example includes hello service contract and implementation from previous steps in hello tutorial and hosts hello service in a console application.</span></span> <span data-ttu-id="5beab-243">Compilare hello seguente di codice in un file eseguibile chiamato ImageListener.exe.</span><span class="sxs-lookup"><span data-stu-id="5beab-243">Compile hello following code into an executable named ImageListener.exe.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-hello-code"></a><span data-ttu-id="5beab-244">La compilazione di codice hello</span><span class="sxs-lookup"><span data-stu-id="5beab-244">Compiling hello code</span></span>
<span data-ttu-id="5beab-245">Dopo aver compilato la soluzione hello, hello in seguito un'applicazione hello toorun:</span><span class="sxs-lookup"><span data-stu-id="5beab-245">After building hello solution, do hello following toorun hello application:</span></span>

1. <span data-ttu-id="5beab-246">Premere **F5**, o percorso del file eseguibile toohello (ImageListener\bin\Debug\ImageListener.exe), il servizio di hello toorun Sfoglia.</span><span class="sxs-lookup"><span data-stu-id="5beab-246">Press **F5**, or browse toohello executable file location (ImageListener\bin\Debug\ImageListener.exe), toorun hello service.</span></span> <span data-ttu-id="5beab-247">Mantenere hello app in esecuzione, come passaggio successivo di tooperform hello è obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="5beab-247">Keep hello app running, as it's required tooperform hello next step.</span></span>
2. <span data-ttu-id="5beab-248">Copiare e incollare l'indirizzo di hello dal prompt dei comandi di hello in un'immagine di hello toosee browser.</span><span class="sxs-lookup"><span data-stu-id="5beab-248">Copy and paste hello address from hello command prompt into a browser toosee hello image.</span></span>
3. <span data-ttu-id="5beab-249">Al termine, premere **invio** in app di hello tooclose finestra prompt dei comandi hello.</span><span class="sxs-lookup"><span data-stu-id="5beab-249">When you are finished, press **Enter** in hello command prompt window tooclose hello app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5beab-250">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5beab-250">Next steps</span></span>
<span data-ttu-id="5beab-251">Dopo aver creato un'applicazione che utilizza il servizio di inoltro di hello Bus di servizio, vedere hello seguente toolearn articoli più sull'inoltro di Azure:</span><span class="sxs-lookup"><span data-stu-id="5beab-251">Now that you've built an application that uses hello Service Bus relay service, see hello following articles toolearn more about Azure Relay:</span></span>

* [<span data-ttu-id="5beab-252">Panoramica dell'architettura del bus di servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="5beab-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="5beab-253">Panoramica del servizio di inoltro di Azure</span><span class="sxs-lookup"><span data-stu-id="5beab-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="5beab-254">Come servizio con .NET di inoltro toouse hello WCF</span><span class="sxs-lookup"><span data-stu-id="5beab-254">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
