---
title: Esercitazione su REST del bus di servizio usando il servizio di inoltro di Azure | Documentazione Microsoft
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
ms.openlocfilehash: 0db9dbd2d2743907e3f0b259228201d4f5d0c3c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="888c1-103">Esercitazione su REST per l'inoltro WCF di Azure</span><span class="sxs-lookup"><span data-stu-id="888c1-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="888c1-104">Questa esercitazione descrive come creare una semplice applicazione host di inoltro di Azure che espone un'interfaccia basata su REST.</span><span class="sxs-lookup"><span data-stu-id="888c1-104">This tutorial describes how to build a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="888c1-105">REST consente ai client Web, ad esempio un Web browser, di accedere all'API del bus di servizio tramite richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="888c1-105">REST enables a web client, such as a web browser, to access the Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="888c1-106">In questa esercitazione viene usato il modello di programmazione REST di Windows Communication Foundation (WCF) per creare un servizio REST nel bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="888c1-106">The tutorial uses the Windows Communication Foundation (WCF) REST programming model to construct a REST service on Service Bus.</span></span> <span data-ttu-id="888c1-107">Per altre informazioni, vedere [Modello di programmazione HTTP Web WCF](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) e [Progettazione e implementazione di servizi](/dotnet/framework/wcf/designing-and-implementing-services) nella documentazione di WCF.</span><span class="sxs-lookup"><span data-stu-id="888c1-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in the WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="888c1-108">Passaggio 1: Creare uno spazio dei nomi</span><span class="sxs-lookup"><span data-stu-id="888c1-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="888c1-109">Per usare le funzionalità del servizio d'inoltro di Azure, è prima necessario creare uno spazio dei nomi del servizio.</span><span class="sxs-lookup"><span data-stu-id="888c1-109">To begin using the relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="888c1-110">Uno spazio dei nomi funge da contenitore di ambito in cui indirizzare le risorse di Azure nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="888c1-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="888c1-111">Seguire le [istruzioni qui](relay-create-namespace-portal.md) per creare uno spazio dei nomi di inoltro.</span><span class="sxs-lookup"><span data-stu-id="888c1-111">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-to-use-with-azure-relay"></a><span data-ttu-id="888c1-112">Passaggio 2: definire un contratto di servizio WCF basato su REST da usare con il servizio di inoltro di Azure</span><span class="sxs-lookup"><span data-stu-id="888c1-112">Step 2: Define a REST-based WCF service contract to use with Azure Relay</span></span>

<span data-ttu-id="888c1-113">Quando si crea un servizio basato su REST WCF, è necessario definire il contratto.</span><span class="sxs-lookup"><span data-stu-id="888c1-113">When you create a WCF REST-style service, you must define the contract.</span></span> <span data-ttu-id="888c1-114">Il contratto specifica quali operazioni sono supportate dall'host.</span><span class="sxs-lookup"><span data-stu-id="888c1-114">The contract specifies what operations the host supports.</span></span> <span data-ttu-id="888c1-115">Un'operazione di servizio può essere considerata come un metodo del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="888c1-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="888c1-116">I contratti vengono creati definendo un'interfaccia C++, C# o Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="888c1-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="888c1-117">Ogni metodo dell'interfaccia corrisponde a un'operazione di servizio specifico.</span><span class="sxs-lookup"><span data-stu-id="888c1-117">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="888c1-118">L'attributo [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) deve essere applicato a ogni interfaccia e l'attributo [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) deve essere applicato a ogni operazione.</span><span class="sxs-lookup"><span data-stu-id="888c1-118">The [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied to each interface, and the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied to each operation.</span></span> <span data-ttu-id="888c1-119">Se un metodo di un'interfaccia che ha [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) non ha [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), non viene esposto.</span><span class="sxs-lookup"><span data-stu-id="888c1-119">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="888c1-120">Il codice usato per eseguire queste attività viene illustrato nell'esempio che segue la procedura.</span><span class="sxs-lookup"><span data-stu-id="888c1-120">The code used for these tasks is shown in the example following the procedure.</span></span>

<span data-ttu-id="888c1-121">La differenza principale tra un contratto di WCF e un contratto di tipo REST è costituita dall'aggiunta di una proprietà all'attributo [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="888c1-121">The primary difference between a WCF contract and a REST-style contract is the addition of a property to the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="888c1-122">Questa proprietà consente di eseguire il mapping di un metodo dell'interfaccia a un metodo su altro lato dell'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="888c1-122">This property enables you to map a method in your interface to a method on the other side of the interface.</span></span> <span data-ttu-id="888c1-123">In tal caso, si userà [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) per collegare un metodo a HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="888c1-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) to link a method to HTTP GET.</span></span> <span data-ttu-id="888c1-124">In questo modo il bus di servizio può recuperare e interpretare in modo accurato i comandi inviati all'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="888c1-124">This allows Service Bus to accurately retrieve and interpret commands sent to the interface.</span></span>

### <a name="to-create-a-contract-with-an-interface"></a><span data-ttu-id="888c1-125">Per creare un contratto con un'interfaccia</span><span class="sxs-lookup"><span data-stu-id="888c1-125">To create a contract with an interface</span></span>

1. <span data-ttu-id="888c1-126">Aprire Visual Studio come amministratore: fare clic con il pulsante destro del mouse sul programma nel menu **Start** e quindi fare clic su **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="888c1-126">Open Visual Studio as an administrator: right-click the program in the **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="888c1-127">Creare un nuovo progetto di applicazione console.</span><span class="sxs-lookup"><span data-stu-id="888c1-127">Create a new console application project.</span></span> <span data-ttu-id="888c1-128">Scegliere il menu **File**, selezionare **Nuovo** e quindi **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="888c1-128">Click the **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="888c1-129">Nella finestra di dialogo **Nuovo progetto** fare clic su **Visual C#**, selezionare il modello **Applicazione console** e denominarlo **ImageListener**.</span><span class="sxs-lookup"><span data-stu-id="888c1-129">In the **New Project** dialog box, click **Visual C#**, select the **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="888c1-130">Usare il valore predefinito **Percorso**.</span><span class="sxs-lookup"><span data-stu-id="888c1-130">Use the default **Location**.</span></span> <span data-ttu-id="888c1-131">Fare clic su **OK** per creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="888c1-131">Click **OK** to create the project.</span></span>
3. <span data-ttu-id="888c1-132">Per un progetto C#, Visual Studio crea un file `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="888c1-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="888c1-133">Questa classe contiene un metodo `Main()` vuoto, necessario per una corretta compilazione del progetto di applicazione console.</span><span class="sxs-lookup"><span data-stu-id="888c1-133">This class contains an empty `Main()` method, required for a console application project to build correctly.</span></span>
4. <span data-ttu-id="888c1-134">Aggiungere al progetto i riferimenti al bus di servizio e a **System.ServiceModel.dll** installando il pacchetto NuGet del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="888c1-134">Add references to Service Bus and **System.ServiceModel.dll** to the project by installing the Service Bus NuGet package.</span></span> <span data-ttu-id="888c1-135">Questo pacchetto aggiunge automaticamente i riferimenti alle librerie del bus di servizio, oltre all'oggetto **System.ServiceModel** di WCF.</span><span class="sxs-lookup"><span data-stu-id="888c1-135">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="888c1-136">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **ImageListener** e quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="888c1-136">In Solution Explorer, right-click the **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="888c1-137">Fare clic sulla scheda **Sfoglia** e cercare `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="888c1-137">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="888c1-138">Fare clic su **Installa**e accettare le condizioni per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="888c1-138">Click **Install**, and accept the terms of use.</span></span>
5. <span data-ttu-id="888c1-139">È necessario aggiungere in modo esplicito un riferimento a **System.ServiceModel.Web.dll** nel progetto:</span><span class="sxs-lookup"><span data-stu-id="888c1-139">You must explicitly add a reference to **System.ServiceModel.Web.dll** to the project:</span></span>
   
    <span data-ttu-id="888c1-140">a.</span><span class="sxs-lookup"><span data-stu-id="888c1-140">a.</span></span> <span data-ttu-id="888c1-141">In Esplora soluzioni fare clic con il pulsante destro del mouse sulla cartella **Riferimenti** nella cartella di progetto e quindi fare clic su **Aggiungi riferimento**.</span><span class="sxs-lookup"><span data-stu-id="888c1-141">In Solution Explorer, right-click the **References** folder under the project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="888c1-142">b.</span><span class="sxs-lookup"><span data-stu-id="888c1-142">b.</span></span> <span data-ttu-id="888c1-143">Nella finestra di dialogo **Aggiungi riferimento** fare clic sulla scheda **Framework** sul lato sinistro e nella casella **Cerca** digitare **System.ServiceModel.Web**.</span><span class="sxs-lookup"><span data-stu-id="888c1-143">In the **Add Reference** dialog box, click the **Framework** tab on the left-hand side and in the **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="888c1-144">Selezionare la casella di controllo **System.ServiceModel.Web** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="888c1-144">Select the **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="888c1-145">Aggiungere le istruzioni `using` seguenti all'inizio del file Program.cs.</span><span class="sxs-lookup"><span data-stu-id="888c1-145">Add the following `using` statements at the top of the Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="888c1-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) è lo spazio dei nomi che consente l'accesso a livello di codice alle funzionalità di base di WCF.</span><span class="sxs-lookup"><span data-stu-id="888c1-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables programmatic access to basic features of WCF.</span></span> <span data-ttu-id="888c1-147">Inoltro WCF usa molti oggetti e attributi di WCF per definire i contratti di servizio.</span><span class="sxs-lookup"><span data-stu-id="888c1-147">WCF Relay uses many of the objects and attributes of WCF to define service contracts.</span></span> <span data-ttu-id="888c1-148">Questo spazio dei nomi viene usato nella maggior parte delle applicazioni di inoltro.</span><span class="sxs-lookup"><span data-stu-id="888c1-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="888c1-149">Analogamente, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) consente di definire il canale, ossia l'oggetto usato per comunicare con il servizio di inoltro di Azure e il Web browser client.</span><span class="sxs-lookup"><span data-stu-id="888c1-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define the channel, which is the object through which you communicate with Azure Relay and the client web browser.</span></span> <span data-ttu-id="888c1-150">Infine, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contiene i tipi che consentono di creare applicazioni basate sul Web.</span><span class="sxs-lookup"><span data-stu-id="888c1-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains the types that enable you to create web-based applications.</span></span>
7. <span data-ttu-id="888c1-151">Rinominare lo spazio dei nomi `ImageListener` in **Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="888c1-151">Rename the `ImageListener` namespace to **Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="888c1-152">Subito dopo la parentesi graffa aperta nella dichiarazione dello spazio dei nomi, definire una nuova interfaccia denominata **IImageContract** e applicare l'attributo **ServiceContractAttribute** all'interfaccia con il valore `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="888c1-152">Directly after the opening curly brace of the namespace declaration, define a new interface named **IImageContract** and apply the **ServiceContractAttribute** attribute to the interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="888c1-153">Il valore dello spazio dei nomi è diverso dallo spazio dei nomi usato nell'ambito del codice.</span><span class="sxs-lookup"><span data-stu-id="888c1-153">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="888c1-154">Il valore dello spazio dei nomi viene utilizzato come identificatore univoco per questo contratto e deve disporre delle informazioni sulla versione.</span><span class="sxs-lookup"><span data-stu-id="888c1-154">The namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="888c1-155">Per altre informazioni, vedere [Controllo delle versioni del servizio](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="888c1-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="888c1-156">Specificando lo spazio dei nomi in modo esplicito si impedisce che il valore predefinito dello spazio dei nomi venga aggiunto al nome del contratto.</span><span class="sxs-lookup"><span data-stu-id="888c1-156">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="888c1-157">Nell'interfaccia `IImageContract` dichiarare un metodo per la singola operazione esposta dal contratto `IImageContract` nell'interfaccia e applicare l'attributo `OperationContractAttribute` al metodo da esporre come parte del contratto pubblico del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="888c1-157">Within the `IImageContract` interface, declare a method for the single operation the `IImageContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="888c1-158">Nell'attributo **OperationContract** aggiungere il valore **WebGet**.</span><span class="sxs-lookup"><span data-stu-id="888c1-158">In the **OperationContract** attribute, add the **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="888c1-159">Ciò consente al servizio di inoltro di instradare le richieste HTTP GET a `GetImage` e di convertire i valori restituiti di `GetImage` in una risposta HTTP GETRESPONSE.</span><span class="sxs-lookup"><span data-stu-id="888c1-159">Doing so enables the relay service to route HTTP GET requests to `GetImage`, and to translate the return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="888c1-160">Più avanti nell'esercitazione si utilizzerà un Web browser per accedere a questo metodo e per visualizzare l'immagine nel browser.</span><span class="sxs-lookup"><span data-stu-id="888c1-160">Later in the tutorial, you will use a web browser to access this method, and to display the image in the browser.</span></span>
11. <span data-ttu-id="888c1-161">Subito dopo la definizione di `IImageContract`, dichiarare un canale che eredita dalle interfacce `IImageContract` e `IClientChannel`.</span><span class="sxs-lookup"><span data-stu-id="888c1-161">Directly after the `IImageContract` definition, declare a channel that inherits from both the `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="888c1-162">Un canale è l'oggetto WCF tramite il quale il servizio e il client si scambiano le informazioni.</span><span class="sxs-lookup"><span data-stu-id="888c1-162">A channel is the WCF object through which the service and client pass information to each other.</span></span> <span data-ttu-id="888c1-163">In seguito verrà creato il canale nell'applicazione host.</span><span class="sxs-lookup"><span data-stu-id="888c1-163">Later, you will create the channel in your host application.</span></span> <span data-ttu-id="888c1-164">A questo punto, il servizio di inoltro di Azure usa questo canale per passare le richieste HTTP GET dal browser all'implementazione di **GetImage**.</span><span class="sxs-lookup"><span data-stu-id="888c1-164">Azure Relay then uses this channel to pass the HTTP GET requests from the browser to your **GetImage** implementation.</span></span> <span data-ttu-id="888c1-165">L'inoltro usa il canale anche per richiedere il valore restituito **GetImage** e convertirlo in una risposta HTTP GETRESPONSE per il browser client.</span><span class="sxs-lookup"><span data-stu-id="888c1-165">The relay also uses the channel to take the **GetImage** return value and translate it into an HTTP GETRESPONSE for the client browser.</span></span>
12. <span data-ttu-id="888c1-166">Dal menu **Compila**, fare clic su **Compila soluzione** per verificare la correttezza del lavoro svolto finora.</span><span class="sxs-lookup"><span data-stu-id="888c1-166">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="888c1-167">Esempio</span><span class="sxs-lookup"><span data-stu-id="888c1-167">Example</span></span>
<span data-ttu-id="888c1-168">L'esempio di codice seguente illustra un'interfaccia di base che definisce un contratto dell'inoltro WCF.</span><span class="sxs-lookup"><span data-stu-id="888c1-168">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

## <a name="step-3-implement-a-rest-based-wcf-service-contract-to-use-service-bus"></a><span data-ttu-id="888c1-169">Passaggio 3: implementare un contratto di servizio WCF basato su REST per utilizzare il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="888c1-169">Step 3: Implement a REST-based WCF service contract to use Service Bus</span></span>
<span data-ttu-id="888c1-170">La creazione di un servizio di inoltro WCF basato su REST richiede prima la creazione del contratto, che viene definito usando un'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="888c1-170">Creating a REST-style WCF Relay service requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="888c1-171">Il passaggio successivo consiste nell'implementazione dell'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="888c1-171">The next step is to implement the interface.</span></span> <span data-ttu-id="888c1-172">Ciò comporta la creazione di una classe denominata **ImageService** che implementa l’interfaccia **IImageContract** definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="888c1-172">This involves creating a class named **ImageService** that implements the user-defined **IImageContract** interface.</span></span> <span data-ttu-id="888c1-173">Dopo aver implementato il contratto, è quindi necessario configurare l'interfaccia utilizzando un file App.config.</span><span class="sxs-lookup"><span data-stu-id="888c1-173">After you implement the contract, you then configure the interface using an App.config file.</span></span> <span data-ttu-id="888c1-174">Il file di configurazione contiene le informazioni necessarie per l'applicazione, ad esempio il nome del servizio, il nome del contratto e il tipo di protocollo usato per comunicare con il servizio di inoltro.</span><span class="sxs-lookup"><span data-stu-id="888c1-174">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="888c1-175">Il codice usato per eseguire queste attività viene fornito nell'esempio che segue la procedura.</span><span class="sxs-lookup"><span data-stu-id="888c1-175">The code used for these tasks is provided in the example following the procedure.</span></span>

<span data-ttu-id="888c1-176">Come per i passaggi precedenti, è impercettibile la differenza tra l'implementazione di un contratto di tipo REST e di un contratto dell'inoltro WCF.</span><span class="sxs-lookup"><span data-stu-id="888c1-176">As with the previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="to-implement-a-rest-style-service-bus-contract"></a><span data-ttu-id="888c1-177">Per implementare un contratto del bus di servizio di tipo REST</span><span class="sxs-lookup"><span data-stu-id="888c1-177">To implement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="888c1-178">Creare una nuova classe denominata **ImageService** direttamente dopo la definizione dell'interfaccia **IImageContract**.</span><span class="sxs-lookup"><span data-stu-id="888c1-178">Create a new class named **ImageService** directly after the definition of the **IImageContract** interface.</span></span> <span data-ttu-id="888c1-179">La classe **ImageService** implementa l'interfaccia **IImageContract**.</span><span class="sxs-lookup"><span data-stu-id="888c1-179">The **ImageService** class implements the **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="888c1-180">Analogamente ad altre implementazioni di interfaccia, è possibile implementare la definizione in un altro file.</span><span class="sxs-lookup"><span data-stu-id="888c1-180">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="888c1-181">Tuttavia, per questa esercitazione, l'implementazione è presente nello stesso file di definizione dell'interfaccia e del metodo `Main()`.</span><span class="sxs-lookup"><span data-stu-id="888c1-181">However, for this tutorial, the implementation appears in the same file as the interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="888c1-182">Applicare l'attributo [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) alla classe **IImageService** per indicare che la classe è un'implementazione di un contratto WCF.</span><span class="sxs-lookup"><span data-stu-id="888c1-182">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the **IImageService** class to indicate that the class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="888c1-183">Come accennato in precedenza, questo spazio dei nomi non è uno spazio dei nomi tradizionale.</span><span class="sxs-lookup"><span data-stu-id="888c1-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="888c1-184">Infatti, fa parte dell'architettura WCF che identifica il contratto.</span><span class="sxs-lookup"><span data-stu-id="888c1-184">Instead, it is part of the WCF architecture that identifies the contract.</span></span> <span data-ttu-id="888c1-185">Per altre informazioni, vedere l'argomento [Nomi di contratto dati](https://msdn.microsoft.com/library/ms731045.aspx) nella documentazione di WCF.</span><span class="sxs-lookup"><span data-stu-id="888c1-185">For more information, see the [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in the WCF documentation.</span></span>
3. <span data-ttu-id="888c1-186">Aggiungere un'immagine con estensione jpg al progetto.</span><span class="sxs-lookup"><span data-stu-id="888c1-186">Add a .jpg image to your project.</span></span>  
   
    <span data-ttu-id="888c1-187">Si tratta di un'immagine che viene visualizzata nel browser di ricezione dal servizio.</span><span class="sxs-lookup"><span data-stu-id="888c1-187">This is a picture that the service displays in the receiving browser.</span></span> <span data-ttu-id="888c1-188">Fare clic con il pulsante destro del mouse sul progetto e quindi scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="888c1-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="888c1-189">Fare clic su **Elemento esistente**.</span><span class="sxs-lookup"><span data-stu-id="888c1-189">Then click **Existing Item**.</span></span> <span data-ttu-id="888c1-190">Usare la finestra di dialogo **Aggiungi elemento esistente** per trovare un'immagine con estensione jpg appropriata e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="888c1-190">Use the **Add Existing Item** dialog box to browse to an appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="888c1-191">Quando si aggiunge il file, assicurarsi che **Tutti i file** sia selezionato nell'elenco a discesa accanto al campo **Nome file:**.</span><span class="sxs-lookup"><span data-stu-id="888c1-191">When adding the file, make sure that **All Files** is selected in the drop-down list next to the **File name:** field.</span></span> <span data-ttu-id="888c1-192">Nella parte restante di questa esercitazione si presuppone che il nome dell'immagine sia "image.jpg".</span><span class="sxs-lookup"><span data-stu-id="888c1-192">The rest of this tutorial assumes that the name of the image is "image.jpg".</span></span> <span data-ttu-id="888c1-193">Se si dispone di un file diverso, è necessario rinominare l'immagine o modificare il codice per compensare.</span><span class="sxs-lookup"><span data-stu-id="888c1-193">If you have a different file, you will have to rename the image, or change your code to compensate.</span></span>
4. <span data-ttu-id="888c1-194">Per assicurarsi che il servizio in esecuzione riesca a trovare il file di immagine, in **Esplora soluzioni** fare clic con il pulsante destro del mouse sul file di immagine e scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="888c1-194">To make sure that the running service can find the image file, in **Solution Explorer** right-click the image file, then click **Properties**.</span></span> <span data-ttu-id="888c1-195">Nel riquadro **Proprietà** impostare il valore di **Copia in directory di output** su **Copia se più recente**.</span><span class="sxs-lookup"><span data-stu-id="888c1-195">In the **Properties** pane, set **Copy to Output Directory** to **Copy if newer**.</span></span>
5. <span data-ttu-id="888c1-196">Aggiungere al progetto un riferimento all'assembly **System.Drawing.dll** e anche le istruzioni `using` associate riportate qui sotto.</span><span class="sxs-lookup"><span data-stu-id="888c1-196">Add a reference to the **System.Drawing.dll** assembly to the project, and also add the following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="888c1-197">Nella classe **ImageService** aggiungere il costruttore seguente che consente di caricare la bitmap e prepararla per l'invio al browser client.</span><span class="sxs-lookup"><span data-stu-id="888c1-197">In the **ImageService** class, add the following constructor that loads the bitmap and prepares to send it to the client browser.</span></span>
   
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
7. <span data-ttu-id="888c1-198">Direttamente dopo il codice precedente, aggiungere il metodo **GetImage** seguente nella classe **ImageService** per restituire un messaggio HTTP che contiene l'immagine.</span><span class="sxs-lookup"><span data-stu-id="888c1-198">Directly after the previous code, add the following **GetImage** method in the **ImageService** class to return an HTTP message that contains the image.</span></span>
   
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
   
    <span data-ttu-id="888c1-199">Questa implementazione usa **MemoryStream** per recuperare l'immagine e prepararla per la trasmissione in streaming al browser.</span><span class="sxs-lookup"><span data-stu-id="888c1-199">This implementation uses **MemoryStream** to retrieve the image and prepare it for streaming to the browser.</span></span> <span data-ttu-id="888c1-200">Avvia la posizione del flusso da zero, dichiara il contenuto di flusso come jpeg e trasmette le informazioni.</span><span class="sxs-lookup"><span data-stu-id="888c1-200">It starts the stream position at zero, declares the stream content as a jpeg, and streams the information.</span></span>
8. <span data-ttu-id="888c1-201">Dal menu **Compila** scegliere **Compila soluzione**.</span><span class="sxs-lookup"><span data-stu-id="888c1-201">From the **Build** menu, click **Build Solution**.</span></span>

### <a name="to-define-the-configuration-for-running-the-web-service-on-service-bus"></a><span data-ttu-id="888c1-202">Per definire la configurazione per l'esecuzione del servizio Web sul bus di servizio</span><span class="sxs-lookup"><span data-stu-id="888c1-202">To define the configuration for running the web service on Service Bus</span></span>
1. <span data-ttu-id="888c1-203">In **Esplora soluzioni** fare doppio clic sul file **App.config** per aprirlo nell'editor di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="888c1-203">In **Solution Explorer**, double-click **App.config** to open it in the Visual Studio editor.</span></span>
   
    <span data-ttu-id="888c1-204">Il file **App.config** include il nome del servizio, l'endpoint (ovvero il percorso esposto dal servizio di inoltro di Azure per le comunicazioni tra client e host) e il binding (ossia il tipo di protocollo usato per la comunicazione).</span><span class="sxs-lookup"><span data-stu-id="888c1-204">The **App.config** file includes the service name, endpoint (that is, the location Azure Relay exposes for clients and hosts to communicate with each other), and binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="888c1-205">La differenza principale è che l'endpoint di servizio configurato fa riferimento a un'associazione [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding).</span><span class="sxs-lookup"><span data-stu-id="888c1-205">The main difference here is that the configured service endpoint refers to a [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="888c1-206">L'elemento XML `<system.serviceModel>` è un elemento WCF che definisce uno o più servizi.</span><span class="sxs-lookup"><span data-stu-id="888c1-206">The `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="888c1-207">In questo caso, viene utilizzato per definire il nome del servizio e l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="888c1-207">Here, it is used to define the service name and endpoint.</span></span> <span data-ttu-id="888c1-208">Nella parte inferiore dell'elemento `<system.serviceModel>`, ma sempre in `<system.serviceModel>`, aggiungere un elemento `<bindings>` che include il contenuto seguente.</span><span class="sxs-lookup"><span data-stu-id="888c1-208">At the bottom of the `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has the following content.</span></span> <span data-ttu-id="888c1-209">In tal modo, vengono definite le associazioni utilizzate nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="888c1-209">This defines the bindings used in the application.</span></span> <span data-ttu-id="888c1-210">È possibile definire più associazioni, ma per questa esercitazione se ne definisce una sola.</span><span class="sxs-lookup"><span data-stu-id="888c1-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
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
   
    <span data-ttu-id="888c1-211">Il codice precedente definisce un'associazione [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) dell'inoltro WCF con **relayClientAuthenticationType** impostato su **None**.</span><span class="sxs-lookup"><span data-stu-id="888c1-211">The previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set to **None**.</span></span> <span data-ttu-id="888c1-212">Questa impostazione indica che un endpoint che utilizza questa associazione non richiede le credenziali client.</span><span class="sxs-lookup"><span data-stu-id="888c1-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="888c1-213">Dopo l'elemento `<bindings>` aggiungere un elemento `<services>`.</span><span class="sxs-lookup"><span data-stu-id="888c1-213">After the `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="888c1-214">Come per le associazioni, è possibile definire più servizi in un solo file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="888c1-214">Similar to the bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="888c1-215">Tuttavia, per questa esercitazione, se ne definisce solo uno.</span><span class="sxs-lookup"><span data-stu-id="888c1-215">However, for this tutorial, you define only one.</span></span>
   
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
   
    <span data-ttu-id="888c1-216">Questo passaggio consente di configurare un servizio che usa il valore predefinito **webHttpRelayBinding** definito in precedenza.</span><span class="sxs-lookup"><span data-stu-id="888c1-216">This step configures a service that uses the previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="888c1-217">Usa anche il valore predefinito **sbTokenProvider**, definito nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="888c1-217">It also uses the default **sbTokenProvider**, which is defined in the next step.</span></span>
4. <span data-ttu-id="888c1-218">Dopo l'elemento `<services>` creare un elemento `<behaviors>` con il contenuto seguente, sostituendo "SAS_KEY" con la chiave di *firma di accesso condiviso* ottenuta in precedenza dal [portale di Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="888c1-218">After the `<services>` element, create a `<behaviors>` element with the following content, replacing "SAS_KEY" with the *Shared Access Signature* (SAS) key you previously obtained from the [Azure portal][Azure portal].</span></span>
   
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
5. <span data-ttu-id="888c1-219">Nell'elemento `<appSettings>`, sempre nel file App.config, sostituire il valore dell'intera stringa di connessione con la stringa di connessione ottenuta prima dal portale.</span><span class="sxs-lookup"><span data-stu-id="888c1-219">Still in App.config, in the `<appSettings>` element, replace the entire connection string value with the connection string you previously obtained from the portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="888c1-220">Scegliere **Compila soluzione** dal menu **Compila** per compilare l'intera soluzione.</span><span class="sxs-lookup"><span data-stu-id="888c1-220">From the **Build** menu, click **Build Solution** to build the entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="888c1-221">Esempio</span><span class="sxs-lookup"><span data-stu-id="888c1-221">Example</span></span>
<span data-ttu-id="888c1-222">Il codice seguente illustra l'implementazione del contratto e del servizio per un servizio basato su REST eseguito nel bus di servizio usando l'associazione **WebHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="888c1-222">The following code shows the contract and service implementation for a REST-based service that is running on  Service Bus using the **WebHttpRelayBinding** binding.</span></span>

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

<span data-ttu-id="888c1-223">Nell'esempio seguente viene illustrato il file App.config associato al servizio.</span><span class="sxs-lookup"><span data-stu-id="888c1-223">The following example shows the App.config file associated with the service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove the ones they don't need. -->
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

## <a name="step-4-host-the-rest-based-wcf-service-to-use-azure-relay"></a><span data-ttu-id="888c1-224">Passaggio 4: eseguire l'hosting del servizio WCF basato su REST per usare il servizio di inoltro di Azure</span><span class="sxs-lookup"><span data-stu-id="888c1-224">Step 4: Host the REST-based WCF service to use Azure Relay</span></span>
<span data-ttu-id="888c1-225">Questo passaggio descrive come eseguire un servizio Web usando un'applicazione console con l'inoltro WCF.</span><span class="sxs-lookup"><span data-stu-id="888c1-225">This step describes how to run a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="888c1-226">Un elenco completo del codice scritto in questo passaggio viene fornito nell’esempio che segue la procedura.</span><span class="sxs-lookup"><span data-stu-id="888c1-226">A complete listing of the code written in this step is provided in the example following the procedure.</span></span>

### <a name="to-create-a-base-address-for-the-service"></a><span data-ttu-id="888c1-227">Per creare un indirizzo di base per il servizio</span><span class="sxs-lookup"><span data-stu-id="888c1-227">To create a base address for the service</span></span>
1. <span data-ttu-id="888c1-228">Nella dichiarazione della funzione `Main()` creare una variabile per archiviare lo spazio dei nomi del progetto.</span><span class="sxs-lookup"><span data-stu-id="888c1-228">In the `Main()` function declaration, create a variable to store the namespace of your project.</span></span> <span data-ttu-id="888c1-229">Assicurarsi di sostituire `yourNamespace` con il nome dello spazio dei nomi di inoltro creato prima.</span><span class="sxs-lookup"><span data-stu-id="888c1-229">Make sure to replace `yourNamespace` with the name of the Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="888c1-230">Il bus di servizio utilizza il nome dello spazio dei nomi per creare un URI univoco.</span><span class="sxs-lookup"><span data-stu-id="888c1-230">Service Bus uses the name of your namespace to create a unique URI.</span></span>
2. <span data-ttu-id="888c1-231">Creare un'istanza di `Uri` per l'indirizzo di base del servizio basato sullo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="888c1-231">Create a `Uri` instance for the base address of the service that is based on the namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="to-create-and-configure-the-web-service-host"></a><span data-ttu-id="888c1-232">Per creare e configurare l'host del servizio Web</span><span class="sxs-lookup"><span data-stu-id="888c1-232">To create and configure the web service host</span></span>
* <span data-ttu-id="888c1-233">Creare l'host del servizio Web utilizzando l'indirizzo URI creato precedentemente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="888c1-233">Create the web service host, using the URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="888c1-234">L'host del servizio è l'oggetto WCF che crea un'istanza dell'applicazione host.</span><span class="sxs-lookup"><span data-stu-id="888c1-234">The service host is the WCF object that instantiates the host application.</span></span> <span data-ttu-id="888c1-235">In questo esempio viene passato il tipo di host da creare, ovvero **ImageService**, nonché l'indirizzo al quale si vuole esporre l'applicazione host.</span><span class="sxs-lookup"><span data-stu-id="888c1-235">This example passes it the type of host you want to create (an **ImageService**), and also the address at which you want to expose the host application.</span></span>

### <a name="to-run-the-web-service-host"></a><span data-ttu-id="888c1-236">Per eseguire l'host del servizio Web</span><span class="sxs-lookup"><span data-stu-id="888c1-236">To run the web service host</span></span>
1. <span data-ttu-id="888c1-237">Aprire il servizio.</span><span class="sxs-lookup"><span data-stu-id="888c1-237">Open the service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="888c1-238">Il servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="888c1-238">The service is now running.</span></span>
2. <span data-ttu-id="888c1-239">Visualizzare un messaggio che indica che il servizio è in esecuzione e come arrestare il servizio.</span><span class="sxs-lookup"><span data-stu-id="888c1-239">Display a message indicating that the service is running, and how to stop the service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy the following address into a browser to see the image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="888c1-240">Al termine, chiudere l'host del servizio.</span><span class="sxs-lookup"><span data-stu-id="888c1-240">When finished, close the service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="888c1-241">Esempio</span><span class="sxs-lookup"><span data-stu-id="888c1-241">Example</span></span>
<span data-ttu-id="888c1-242">Nell'esempio seguente vengono inclusi il contratto di servizio e l'implementazione dei passaggi precedenti dell'esercitazione e viene ospitato il servizio in un'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="888c1-242">The following example includes the service contract and implementation from previous steps in the tutorial and hosts the service in a console application.</span></span> <span data-ttu-id="888c1-243">Compilare il codice seguente in un eseguibile denominato ImageListener.exe.</span><span class="sxs-lookup"><span data-stu-id="888c1-243">Compile the following code into an executable named ImageListener.exe.</span></span>

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

            Console.WriteLine("Copy the following address into a browser to see the image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-the-code"></a><span data-ttu-id="888c1-244">Compilazione del codice</span><span class="sxs-lookup"><span data-stu-id="888c1-244">Compiling the code</span></span>
<span data-ttu-id="888c1-245">Dopo aver compilato la soluzione, effettuare le operazioni seguenti per eseguire l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="888c1-245">After building the solution, do the following to run the application:</span></span>

1. <span data-ttu-id="888c1-246">Premere **F5** o passare al percorso del file eseguibile ImageListener\bin\Debug\ImageListener.exe per eseguire il servizio.</span><span class="sxs-lookup"><span data-stu-id="888c1-246">Press **F5**, or browse to the executable file location (ImageListener\bin\Debug\ImageListener.exe), to run the service.</span></span> <span data-ttu-id="888c1-247">Mantenere l'app in esecuzione perché verrà usata per eseguire il passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="888c1-247">Keep the app running, as it's required to perform the next step.</span></span>
2. <span data-ttu-id="888c1-248">Copiare e incollare l'indirizzo dal prompt dei comandi in un browser per visualizzare l'immagine.</span><span class="sxs-lookup"><span data-stu-id="888c1-248">Copy and paste the address from the command prompt into a browser to see the image.</span></span>
3. <span data-ttu-id="888c1-249">Al termine, premere **INVIO** nella finestra del prompt dei comandi per chiudere l'app.</span><span class="sxs-lookup"><span data-stu-id="888c1-249">When you are finished, press **Enter** in the command prompt window to close the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="888c1-250">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="888c1-250">Next steps</span></span>
<span data-ttu-id="888c1-251">A questo punto, dopo avere creato un'applicazione che usa il servizio di inoltro del bus di servizio, vedere gli articoli seguenti per altre informazioni sul servizio di inoltro di Azure:</span><span class="sxs-lookup"><span data-stu-id="888c1-251">Now that you've built an application that uses the Service Bus relay service, see the following articles to learn more about Azure Relay:</span></span>

* [<span data-ttu-id="888c1-252">Panoramica dell'architettura del bus di servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="888c1-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="888c1-253">Panoramica del servizio di inoltro di Azure</span><span class="sxs-lookup"><span data-stu-id="888c1-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="888c1-254">Come usare il servizio di inoltro WCF con .NET</span><span class="sxs-lookup"><span data-stu-id="888c1-254">How to use the WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
