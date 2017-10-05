---
title: Esercitazione sull'inoltro WCF del bus di servizio di Azure | Microsoft Docs
description: Creare un'applicazione client e un servizio del bus di servizio usando Inoltro WCF.
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: sethm
ms.openlocfilehash: 5347bf85cad32b59677369d51a1f36529aef6662
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="85ad8-103">Esercitazione sull'inoltro WCF di Azure</span><span class="sxs-lookup"><span data-stu-id="85ad8-103">Azure WCF Relay tutorial</span></span>

<span data-ttu-id="85ad8-104">Questa esercitazione descrive come compilare una semplice applicazione e servizio client di inoltro WCF usando Inoltro di Azure.</span><span class="sxs-lookup"><span data-stu-id="85ad8-104">This tutorial describes how to build a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="85ad8-105">Per un'esercitazione simile che usa la [messaggistica](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging) del bus di servizio, vedere [Introduzione alle code del bus di servizio](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="85ad8-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="85ad8-106">L'esecuzione di questa esercitazione consente di acquisire una comprensione dei passaggi necessari per creare un'applicazione client e di servizio di inoltro WCF.</span><span class="sxs-lookup"><span data-stu-id="85ad8-106">Working through this tutorial gives you an understanding of the steps that are required to create a WCF Relay client and service application.</span></span> <span data-ttu-id="85ad8-107">Come per le rispettive controparti WCF originali, un servizio è un costrutto che espone uno o più endpoint, ognuno dei quali espone a sua volta una o più operazioni del servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="85ad8-108">L'endpoint di un servizio specifica un indirizzo in cui è disponibile il servizio, un binding che contiene le informazioni che un client deve comunicare al servizio e un contratto che definisce la funzionalità fornita dal servizio ai propri client.</span><span class="sxs-lookup"><span data-stu-id="85ad8-108">The endpoint of a service specifies an address where the service can be found, a binding that contains the information that a client must communicate with the service, and a contract that defines the functionality provided by the service to its clients.</span></span> <span data-ttu-id="85ad8-109">La differenza principale tra WCF e l'inoltro WCF riguarda l'esposizione dell'endpoint nel cloud invece che localmente nel computer.</span><span class="sxs-lookup"><span data-stu-id="85ad8-109">The main difference between WCF and WCF Relay is that the endpoint is exposed in the cloud instead of locally on your computer.</span></span>

<span data-ttu-id="85ad8-110">Dopo aver eseguito la sequenza di argomenti in questa esercitazione, saranno disponibili un servizio in esecuzione e un client che potrà richiamare le operazioni del servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-110">After you work through the sequence of topics in this tutorial, you will have a running service, and a client that can invoke the operations of the service.</span></span> <span data-ttu-id="85ad8-111">Il primo argomento descrive come configurare un account.</span><span class="sxs-lookup"><span data-stu-id="85ad8-111">The first topic describes how to set up an account.</span></span> <span data-ttu-id="85ad8-112">I passaggi successivi descrivono come definire un servizio che usa un contratto, come implementare il servizio e come configurarlo nel codice.</span><span class="sxs-lookup"><span data-stu-id="85ad8-112">The next steps describe how to define a service that uses a contract, how to implement the service, and how to configure the service in code.</span></span> <span data-ttu-id="85ad8-113">Descrivono anche come ospitare ed eseguire il servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-113">They also describe how to host and run the service.</span></span> <span data-ttu-id="85ad8-114">Il servizio creato è self-hosted e il client e il servizio vengono eseguiti nello stesso computer.</span><span class="sxs-lookup"><span data-stu-id="85ad8-114">The service that is created is self-hosted and the client and service run on the same computer.</span></span> <span data-ttu-id="85ad8-115">È possibile configurare il servizio usando il codice o un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="85ad8-115">You can configure the service by using either code or a configuration file.</span></span>

<span data-ttu-id="85ad8-116">I tre passaggi finali descrivono come creare un'applicazione client, configurare l'applicazione client e creare e usare un client in grado di accedere alla funzionalità dell'host.</span><span class="sxs-lookup"><span data-stu-id="85ad8-116">The final three steps describe how to create a client application, configure the client application, and create and use a client that can access the functionality of the host.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85ad8-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="85ad8-117">Prerequisites</span></span>

<span data-ttu-id="85ad8-118">Per completare l'esercitazione sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="85ad8-118">To complete this tutorial, you'll need the following:</span></span>

* <span data-ttu-id="85ad8-119">[Microsoft Visual Studio 2015 o versione successiva](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="85ad8-119">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="85ad8-120">Questa esercitazione usa Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="85ad8-120">This tutorial uses Visual Studio 2017.</span></span>
* <span data-ttu-id="85ad8-121">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="85ad8-121">An active Azure account.</span></span> <span data-ttu-id="85ad8-122">Se non si ha un account, è possibile crearne uno gratuito in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="85ad8-122">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="85ad8-123">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="85ad8-123">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="85ad8-124">Creare uno spazio dei nomi del servizio</span><span class="sxs-lookup"><span data-stu-id="85ad8-124">Create a service namespace</span></span>

<span data-ttu-id="85ad8-125">Il primo passaggio consiste nel creare uno spazio dei nomi e nell'ottenere una chiave di [firma di accesso condiviso](../service-bus-messaging/service-bus-sas.md).</span><span class="sxs-lookup"><span data-stu-id="85ad8-125">The first step is to create a namespace, and to obtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="85ad8-126">Uno spazio dei nomi fornisce un limite per ogni applicazione esposta tramite il servizio di inoltro.</span><span class="sxs-lookup"><span data-stu-id="85ad8-126">A namespace provides an application boundary for each application exposed through the relay service.</span></span> <span data-ttu-id="85ad8-127">Una chiave di firma di accesso condiviso viene generata dal sistema quando viene creato uno spazio dei nomi del servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-127">A SAS key is automatically generated by the system when a service namespace is created.</span></span> <span data-ttu-id="85ad8-128">La combinazione di spazio dei nomi servizio e chiave di firma di accesso condiviso fornisce le credenziali che consentono ad Azure di autenticare l'accesso a un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="85ad8-128">The combination of service namespace and SAS key provides the credentials for Azure to authenticate access to an application.</span></span> <span data-ttu-id="85ad8-129">Seguire [queste istruzioni](relay-create-namespace-portal.md) per creare uno spazio dei nomi di inoltro.</span><span class="sxs-lookup"><span data-stu-id="85ad8-129">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="85ad8-130">Definire un contratto del servizio WCF</span><span class="sxs-lookup"><span data-stu-id="85ad8-130">Define a WCF service contract</span></span>

<span data-ttu-id="85ad8-131">Il contratto di servizio specifica le operazioni (terminologia dei servizi Web per indicare metodi o funzioni) supportate dal servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-131">The service contract specifies what operations (the web service terminology for methods or functions) the service supports.</span></span> <span data-ttu-id="85ad8-132">I contratti vengono creati definendo un'interfaccia C++, C# o Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="85ad8-132">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="85ad8-133">Ogni metodo dell'interfaccia corrisponde a un'operazione di servizio specifico.</span><span class="sxs-lookup"><span data-stu-id="85ad8-133">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="85ad8-134">A ogni interfaccia deve essere applicato l'attributo [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) e a ogni operazione deve essere applicato l'attributo [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="85ad8-134">Each interface must have the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied to it, and each operation must have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied to it.</span></span> <span data-ttu-id="85ad8-135">Se un metodo di un'interfaccia con l'attributo [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) non ha l'attributo [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), il metodo non viene esposto.</span><span class="sxs-lookup"><span data-stu-id="85ad8-135">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="85ad8-136">Il codice per eseguire queste attività viene fornito nell'esempio che segue la procedura.</span><span class="sxs-lookup"><span data-stu-id="85ad8-136">The code for these tasks is provided in the example following the procedure.</span></span> <span data-ttu-id="85ad8-137">Per una descrizione più ampia dei contratti e dei servizi, vedere [Progettazione e implementazione di servizi](https://msdn.microsoft.com/library/ms729746.aspx) nella documentazione di WCF.</span><span class="sxs-lookup"><span data-stu-id="85ad8-137">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in the WCF documentation.</span></span>

### <a name="create-a-relay-contract-with-an-interface"></a><span data-ttu-id="85ad8-138">Creare un contratto di inoltro con un'interfaccia</span><span class="sxs-lookup"><span data-stu-id="85ad8-138">Create a relay contract with an interface</span></span>

1. <span data-ttu-id="85ad8-139">Aprire Visual Studio con ruolo di amministratore. Fare clic con il pulsante destro del mouse sul programma nel menu **Start** e scegliere **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-139">Open Visual Studio as an administrator by right-clicking the program in the **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="85ad8-140">Creare un nuovo progetto di applicazione console.</span><span class="sxs-lookup"><span data-stu-id="85ad8-140">Create a new console application project.</span></span> <span data-ttu-id="85ad8-141">Fare clic sul menu**File**, selezionare **Nuovo** e fare clic su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-141">Click the **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="85ad8-142">Nella finestra di dialogo **Nuovo progetto** fare clic su **Visual C#**. Se **Visual C#** non è visualizzato, vedere in **Altri linguaggi**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-142">In the **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="85ad8-143">Fare clic sul modello **App console (.NET Framework)** e denominarlo **EchoService**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-143">Click the **Console App (.NET Framework)** template, and name it **EchoService**.</span></span> <span data-ttu-id="85ad8-144">Fare clic su **OK** per creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="85ad8-144">Click **OK** to create the project.</span></span>

    ![][2]

3. <span data-ttu-id="85ad8-145">Installare il pacchetto NuGet del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-145">Install the Service Bus NuGet package.</span></span> <span data-ttu-id="85ad8-146">Questo pacchetto aggiunge automaticamente i riferimenti alle librerie del bus di servizio, oltre all'oggetto **System.ServiceModel** di WCF.</span><span class="sxs-lookup"><span data-stu-id="85ad8-146">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="85ad8-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) è lo spazio dei nomi che consente l'accesso a livello di codice alle funzionalità di base di WCF.</span><span class="sxs-lookup"><span data-stu-id="85ad8-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables you to programmatically access the basic features of WCF.</span></span> <span data-ttu-id="85ad8-148">Il bus di servizio utilizza molti degli oggetti e degli attributi di WCF per definire i contratti di servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-148">Service Bus uses many of the objects and attributes of WCF to define service contracts.</span></span>

    <span data-ttu-id="85ad8-149">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto e quindi scegliere **Gestisci pacchetti NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-149">In Solution Explorer, right-click the project, and then click **Manage NuGet Packages...**.</span></span> <span data-ttu-id="85ad8-150">Fare clic sulla scheda **Sfoglia** e quindi cercare `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="85ad8-150">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="85ad8-151">Assicurarsi che il nome del progetto sia selezionato nella casella **Versione**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-151">Ensure that the project name is selected in the **Version(s)** box.</span></span> <span data-ttu-id="85ad8-152">Fare clic su **Installa**e accettare le condizioni per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="85ad8-152">Click **Install**, and accept the terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="85ad8-153">In Esplora soluzioni fare doppio clic sul file Program.cs per aprirlo nell'editor, se non è già aperto.</span><span class="sxs-lookup"><span data-stu-id="85ad8-153">In Solution Explorer, double-click the Program.cs file to open it in the editor, if it is not already open.</span></span>
5. <span data-ttu-id="85ad8-154">Aggiungere le istruzioni using seguenti all'inizio del file:</span><span class="sxs-lookup"><span data-stu-id="85ad8-154">Add the following using statements at the top of the file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="85ad8-155">Modificare il nome predefinito dello spazio dei nomi da **EchoService** a **Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-155">Change the namespace name from its default name of **EchoService** to **Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="85ad8-156">Questa esercitazione usa lo spazio dei nomi C# **Microsoft.ServiceBus.Samples**, ovvero lo spazio dei nomi del tipo gestito in base al contratto usato nel file di configurazione nel passaggio [Configurare il client WCF](#configure-the-wcf-client).</span><span class="sxs-lookup"><span data-stu-id="85ad8-156">This tutorial uses the C# namespace **Microsoft.ServiceBus.Samples**, which is the namespace of the contract-based managed type that is used in the configuration file in the [Configure the WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="85ad8-157">È possibile specificare qualsiasi spazio dei nomi quando si crea questo esempio. L'esercitazione tuttavia non funzionerà a meno che gli spazi dei nomi del contratto e del servizio non vengano modificati di conseguenza nel file di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="85ad8-157">You can specify any namespace you want when you build this sample; however, the tutorial will not work unless you then modify the namespaces of the contract and service accordingly, in the application configuration file.</span></span> <span data-ttu-id="85ad8-158">Lo spazio dei nomi specificato nel file App.config deve essere lo stesso specificato nei file C#.</span><span class="sxs-lookup"><span data-stu-id="85ad8-158">The namespace specified in the App.config file must be the same as the namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="85ad8-159">Subito dopo la dichiarazione dello spazio dei nomi `Microsoft.ServiceBus.Samples`, ma sempre nello spazio dei nomi, definire una nuova interfaccia denominata `IEchoContract` e applicare l'attributo `ServiceContractAttribute` all'interfaccia con un valore dello spazio dei nomi `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="85ad8-159">Directly after the `Microsoft.ServiceBus.Samples` namespace declaration, but within the namespace, define a new interface named `IEchoContract` and apply the `ServiceContractAttribute` attribute to the interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="85ad8-160">Il valore dello spazio dei nomi è diverso dallo spazio dei nomi usato nell'ambito del codice.</span><span class="sxs-lookup"><span data-stu-id="85ad8-160">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="85ad8-161">Il valore dello spazio dei nomi viene invece usato come identificatore univoco per questo contratto.</span><span class="sxs-lookup"><span data-stu-id="85ad8-161">Instead, the namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="85ad8-162">Specificando lo spazio dei nomi in modo esplicito si impedisce che il valore predefinito dello spazio dei nomi venga aggiunto al nome del contratto.</span><span class="sxs-lookup"><span data-stu-id="85ad8-162">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span> <span data-ttu-id="85ad8-163">Incollare il codice seguente dopo la dichiarazione dello spazio dei nomi:</span><span class="sxs-lookup"><span data-stu-id="85ad8-163">Paste the following code after the namespace declaration:</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="85ad8-164">Lo spazio dei nomi del contratto del servizio include in genere uno schema di denominazione che contiene informazioni sulla versione.</span><span class="sxs-lookup"><span data-stu-id="85ad8-164">Typically, the service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="85ad8-165">Se si includono le informazioni sulla versione nello spazio dei nomi del contratto di servizio, si consente ai servizi di isolare le modifiche principali definendo un nuovo contratto di servizio con un nuovo spazio dei nomi ed esponendolo in un nuovo endpoint.</span><span class="sxs-lookup"><span data-stu-id="85ad8-165">Including version information in the service contract namespace enables services to isolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="85ad8-166">In questo modo i client possono continuare a usare il contratto del servizio precedente senza dover essere aggiornati.</span><span class="sxs-lookup"><span data-stu-id="85ad8-166">In this manner, clients can continue to use the old service contract without having to be updated.</span></span> <span data-ttu-id="85ad8-167">Le informazioni sulla versione possono essere costituite da una data o da un numero di build.</span><span class="sxs-lookup"><span data-stu-id="85ad8-167">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="85ad8-168">Per altre informazioni, vedere [Controllo delle versioni del servizio](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="85ad8-168">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="85ad8-169">Ai fini di questa esercitazione, lo schema di denominazione dello spazio dei nomi del contratto del servizio non include informazioni sulla versione.</span><span class="sxs-lookup"><span data-stu-id="85ad8-169">For the purposes of this tutorial, the naming scheme of the service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="85ad8-170">Nell'interfaccia `IEchoContract` dichiarare un metodo per la singola operazione esposta dal contratto `IEchoContract` nell'interfaccia e applicare l'attributo `OperationContractAttribute` al metodo da esporre come parte del contratto pubblico di inoltro WCF, come segue:</span><span class="sxs-lookup"><span data-stu-id="85ad8-170">Within the `IEchoContract` interface, declare a method for the single operation the `IEchoContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public WCF Relay contract, as follows:</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="85ad8-171">Direttamente dopo la definizione dell'interfaccia `IEchoContract` dichiarare un canale che eredita dalle interfacce `IEchoContract` e `IClientChannel`, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="85ad8-171">Directly after the `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also to the `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="85ad8-172">Un canale è l'oggetto WCF attraverso il quale l'host e il client si scambiano informazioni.</span><span class="sxs-lookup"><span data-stu-id="85ad8-172">A channel is the WCF object through which the host and client pass information to each other.</span></span> <span data-ttu-id="85ad8-173">Successivamente si scriverà il codice per il canale per ripetere le informazioni tra le due applicazioni.</span><span class="sxs-lookup"><span data-stu-id="85ad8-173">Later, you will write code against the channel to echo information between the two applications.</span></span>
10. <span data-ttu-id="85ad8-174">Scegliere **Compila soluzione** dal menu **Compila** o premere **CTRL+MAIUSC+B** per confermare la correttezza di quanto fatto finora.</span><span class="sxs-lookup"><span data-stu-id="85ad8-174">From the **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="85ad8-175">Esempio</span><span class="sxs-lookup"><span data-stu-id="85ad8-175">Example</span></span>

<span data-ttu-id="85ad8-176">L'esempio di codice seguente illustra un'interfaccia di base che definisce un contratto dell'inoltro WCF.</span><span class="sxs-lookup"><span data-stu-id="85ad8-176">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="85ad8-177">Dopo aver creato l'interfaccia, è possibile implementarla.</span><span class="sxs-lookup"><span data-stu-id="85ad8-177">Now that the interface is created, you can implement the interface.</span></span>

## <a name="implement-the-wcf-contract"></a><span data-ttu-id="85ad8-178">Implementare il contratto WCF</span><span class="sxs-lookup"><span data-stu-id="85ad8-178">Implement the WCF contract</span></span>

<span data-ttu-id="85ad8-179">La creazione di un inoltro di Azure deve essere preceduta dalla creazione del contratto, che viene definito usando un'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="85ad8-179">Creating an Azure relay requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="85ad8-180">Per altre informazioni sulla creazione dell'interfaccia, vedere il passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="85ad8-180">For more information about creating the interface, see the previous step.</span></span> <span data-ttu-id="85ad8-181">Il passaggio successivo consiste nell'implementazione dell'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="85ad8-181">The next step is to implement the interface.</span></span> <span data-ttu-id="85ad8-182">Questa operazione richiede la creazione di una classe denominata `EchoService` t che implementa l'interfaccia `IEchoContract` definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="85ad8-182">This involves creating a class named `EchoService` that implements the user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="85ad8-183">Dopo l'implementazione dell'interfaccia, si procede alla sua configurazione usando un file di configurazione App.config.</span><span class="sxs-lookup"><span data-stu-id="85ad8-183">After you implement the interface, you then configure the interface using an App.config configuration file.</span></span> <span data-ttu-id="85ad8-184">Il file di configurazione contiene le informazioni necessarie per l'applicazione, ad esempio il nome del servizio, il nome del contratto e il tipo di protocollo usato per comunicare con il servizio di inoltro.</span><span class="sxs-lookup"><span data-stu-id="85ad8-184">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="85ad8-185">Il codice usato per eseguire queste attività viene fornito nell'esempio che segue la procedura.</span><span class="sxs-lookup"><span data-stu-id="85ad8-185">The code used for these tasks is provided in the example following the procedure.</span></span> <span data-ttu-id="85ad8-186">Per una descrizione di carattere generale sull'implementazione di un contratto di servizio, vedere [Implementazione dei contratti di servizio](https://msdn.microsoft.com/library/ms733764.aspx) nella documentazione di WCF.</span><span class="sxs-lookup"><span data-stu-id="85ad8-186">For a more general discussion about how to implement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in the WCF documentation.</span></span>

1. <span data-ttu-id="85ad8-187">Creare una nuova classe denominata `EchoService` direttamente dopo la definizione dell’interfaccia `IEchoContract`.</span><span class="sxs-lookup"><span data-stu-id="85ad8-187">Create a new class named `EchoService` directly after the definition of the `IEchoContract` interface.</span></span> <span data-ttu-id="85ad8-188">La classe `EchoService` implementa l'interfaccia `IEchoContract`.</span><span class="sxs-lookup"><span data-stu-id="85ad8-188">The `EchoService` class implements the `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="85ad8-189">Analogamente ad altre implementazioni di interfaccia, è possibile implementare la definizione in un altro file.</span><span class="sxs-lookup"><span data-stu-id="85ad8-189">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="85ad8-190">Tuttavia, per questa esercitazione l'implementazione si trova nello stesso file che contiene la definizione di interfaccia e il metodo `Main`.</span><span class="sxs-lookup"><span data-stu-id="85ad8-190">However, for this tutorial, the implementation is located in the same file as the interface definition and the `Main` method.</span></span>
2. <span data-ttu-id="85ad8-191">Applicare l'attributo [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) all'interfaccia `IEchoContract`.</span><span class="sxs-lookup"><span data-stu-id="85ad8-191">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the `IEchoContract` interface.</span></span> <span data-ttu-id="85ad8-192">L'attributo specifica lo spazio dei nomi e il nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-192">The attribute specifies the service name and namespace.</span></span> <span data-ttu-id="85ad8-193">Al termine dell'operazione, la classe `EchoService` ha un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="85ad8-193">After doing so, the `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="85ad8-194">Implementare il metodo `Echo` definito nell'interfaccia `IEchoContract` nella classe `EchoService`.</span><span class="sxs-lookup"><span data-stu-id="85ad8-194">Implement the `Echo` method defined in the `IEchoContract` interface in the `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="85ad8-195">Scegliere **Compila soluzione** dal menu **Compila** per verificare la correttezza del lavoro.</span><span class="sxs-lookup"><span data-stu-id="85ad8-195">Click **Build**, then click **Build Solution** to confirm the accuracy of your work.</span></span>

### <a name="define-the-configuration-for-the-service-host"></a><span data-ttu-id="85ad8-196">Definire la configurazione dell'host del servizio</span><span class="sxs-lookup"><span data-stu-id="85ad8-196">Define the configuration for the service host</span></span>

1. <span data-ttu-id="85ad8-197">Il file di configurazione è molto simile a un file di configurazione WCF.</span><span class="sxs-lookup"><span data-stu-id="85ad8-197">The configuration file is very similar to a WCF configuration file.</span></span> <span data-ttu-id="85ad8-198">Include il nome del servizio, l'endpoint (ovvero il percorso esposto dall'inoltro di Azure per le comunicazioni tra client e host) e l'associazione (ossia il tipo di protocollo usato per la comunicazione).</span><span class="sxs-lookup"><span data-stu-id="85ad8-198">It includes the service name, endpoint (that is, the location that Azure Relay exposes for clients and hosts to communicate with each other), and the binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="85ad8-199">La differenza principale consiste nel fatto che l'endpoint di servizio configurato fa riferimento a un’associazione [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) che non fa parte di .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="85ad8-199">The main difference is that this configured service endpoint refers to a [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of the .NET Framework.</span></span> <span data-ttu-id="85ad8-200">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) è una delle associazioni definite dal servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-200">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of the bindings defined by the service.</span></span>
2. <span data-ttu-id="85ad8-201">In **Esplora soluzioni** fare doppio clic sul file App.config per aprirlo nell'editor di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-201">In **Solution Explorer**, double-click the App.config file to open it in the Visual Studio editor.</span></span>
3. <span data-ttu-id="85ad8-202">Nell'elemento `<appSettings>` sostituire i segnaposto con il nome dello spazio dei nomi del servizio e la chiave di firma di accesso condiviso copiata nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="85ad8-202">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="85ad8-203">All'interno dei tag `<system.serviceModel>` aggiungere un elemento `<services>`.</span><span class="sxs-lookup"><span data-stu-id="85ad8-203">Within the `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="85ad8-204">È possibile definire più applicazioni di inoltro in un singolo file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="85ad8-204">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="85ad8-205">In questa esercitazione ne viene tuttavia definita solo una.</span><span class="sxs-lookup"><span data-stu-id="85ad8-205">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="85ad8-206">Nell'elemento `<services>` aggiungere un elemento `<service>` per definire il nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-206">Within the `<services>` element, add a `<service>` element to define the name of the service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="85ad8-207">Nell'elemento `<service>` definire la posizione del contratto, nonché il tipo di binding per l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="85ad8-207">Within the `<service>` element, define the location of the endpoint contract, and also the type of binding for the endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="85ad8-208">L'endpoint definisce la posizione in cui il client cercherà l'applicazione host.</span><span class="sxs-lookup"><span data-stu-id="85ad8-208">The endpoint defines where the client will look for the host application.</span></span> <span data-ttu-id="85ad8-209">Successivamente nell'esercitazione si userà questo passaggio per creare un URI che espone completamente l'host tramite l'inoltro di Azure.</span><span class="sxs-lookup"><span data-stu-id="85ad8-209">Later, the tutorial uses this step to create a URI that fully exposes the host through Azure Relay.</span></span> <span data-ttu-id="85ad8-210">L'associazione dichiara che come protocollo per le comunicazioni con il servizio di inoltro viene usato TCP.</span><span class="sxs-lookup"><span data-stu-id="85ad8-210">The binding declares that we are using TCP as the protocol to communicate with the relay service.</span></span>
7. <span data-ttu-id="85ad8-211">Scegliere **Compila soluzione** dal menu **Compila** per verificare la correttezza del lavoro.</span><span class="sxs-lookup"><span data-stu-id="85ad8-211">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="85ad8-212">Esempio</span><span class="sxs-lookup"><span data-stu-id="85ad8-212">Example</span></span>

<span data-ttu-id="85ad8-213">Il codice seguente illustra l'implementazione del contratto di servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-213">The following code shows the implementation of the service contract.</span></span>

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

<span data-ttu-id="85ad8-214">Il codice seguente illustra il formato di base del file App.config associato all'host del servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-214">The following code shows the basic format of the App.config file associated with the service host.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-to-register-with-the-relay-service"></a><span data-ttu-id="85ad8-215">Ospitare ed eseguire un servizio Web di base per la registrazione con il servizio di inoltro</span><span class="sxs-lookup"><span data-stu-id="85ad8-215">Host and run a basic web service to register with the relay service</span></span>

<span data-ttu-id="85ad8-216">Questo passaggio descrive come eseguire un servizio di inoltro di Azure.</span><span class="sxs-lookup"><span data-stu-id="85ad8-216">This step describes how to run an Azure Relay service.</span></span>

### <a name="create-the-relay-credentials"></a><span data-ttu-id="85ad8-217">Creare le credenziali di inoltro</span><span class="sxs-lookup"><span data-stu-id="85ad8-217">Create the relay credentials</span></span>

1. <span data-ttu-id="85ad8-218">In `Main()` creare due variabili in cui archiviare lo spazio dei nomi e la chiave di firma di accesso condiviso  letti dalla finestra della console.</span><span class="sxs-lookup"><span data-stu-id="85ad8-218">In `Main()`, create two variables in which to store the namespace and the SAS key that are read from the console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="85ad8-219">La chiave di firma di accesso condiviso verrà usata in seguito per accedere al progetto.</span><span class="sxs-lookup"><span data-stu-id="85ad8-219">The SAS key will be used later to access your project.</span></span> <span data-ttu-id="85ad8-220">Lo spazio dei nomi viene passato come parametro a `CreateServiceUri` per creare un URI del servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-220">The namespace is passed as a parameter to `CreateServiceUri` to create a service URI.</span></span>
2. <span data-ttu-id="85ad8-221">Tramite un oggetto [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) dichiarare che come tipo di credenziali si userà una chiave di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="85ad8-221">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as the credential type.</span></span> <span data-ttu-id="85ad8-222">Aggiungere il codice seguente direttamente dopo il codice aggiunto nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="85ad8-222">Add the following code directly after the code added in the last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-the-service"></a><span data-ttu-id="85ad8-223">Creare un indirizzo di base per il servizio</span><span class="sxs-lookup"><span data-stu-id="85ad8-223">Create a base address for the service</span></span>

<span data-ttu-id="85ad8-224">Dopo il codice aggiunto nel passaggio precedente, creare un'istanza di `Uri` per l'indirizzo di base del servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-224">After the code you added in the last step, create a `Uri` instance for the base address of the service.</span></span> <span data-ttu-id="85ad8-225">L'URI specifica lo schema del bus di servizio, lo spazio dei nomi e il percorso dell'interfaccia del servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-225">This URI specifies the Service Bus scheme, the namespace, and the path of the service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="85ad8-226">"sb" è l'abbreviazione dello schema del bus di servizio e indica che si usa il protocollo TCP.</span><span class="sxs-lookup"><span data-stu-id="85ad8-226">"sb" is an abbreviation for the Service Bus scheme, and indicates that we are using TCP as the protocol.</span></span> <span data-ttu-id="85ad8-227">Il protocollo è stato indicato anche in precedenza nel file di configurazione, quando come associazione si è specificato [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx).</span><span class="sxs-lookup"><span data-stu-id="85ad8-227">This was also previously indicated in the configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as the binding.</span></span>

<span data-ttu-id="85ad8-228">Per questa esercitazione l'URI è `sb://putServiceNamespaceHere.windows.net/EchoService`.</span><span class="sxs-lookup"><span data-stu-id="85ad8-228">For this tutorial, the URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="create-and-configure-the-service-host"></a><span data-ttu-id="85ad8-229">Creare e configurare l'host del servizio</span><span class="sxs-lookup"><span data-stu-id="85ad8-229">Create and configure the service host</span></span>

1. <span data-ttu-id="85ad8-230">Impostare la modalità di connessione su `AutoDetect`.</span><span class="sxs-lookup"><span data-stu-id="85ad8-230">Set the connectivity mode to `AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="85ad8-231">La modalità di connessione descrive il protocollo usato dal servizio per comunicare con il servizio di inoltro, ovvero HTTP o TCP.</span><span class="sxs-lookup"><span data-stu-id="85ad8-231">The connectivity mode describes the protocol the service uses to communicate with the relay service; either HTTP or TCP.</span></span> <span data-ttu-id="85ad8-232">Quando si usa l'impostazione predefinita `AutoDetect`, il servizio prova a connettersi all'inoltro di Azure tramite TCP, se disponibile, e tramite HTTP se TCP non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="85ad8-232">Using the default setting `AutoDetect`, the service attempts to connect to Azure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="85ad8-233">Si noti che questo protocollo è diverso da quello specificato dal servizio per la comunicazione client.</span><span class="sxs-lookup"><span data-stu-id="85ad8-233">Note that this differs from the protocol the service specifies for client communication.</span></span> <span data-ttu-id="85ad8-234">Il protocollo dipende dal binding usato.</span><span class="sxs-lookup"><span data-stu-id="85ad8-234">That protocol is determined by the binding used.</span></span> <span data-ttu-id="85ad8-235">Ad esempio, un servizio può usare l'associazione [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) che specifica che l'endpoint comunica con i client tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="85ad8-235">For example, a service can use the [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="85ad8-236">Lo stesso servizio può specificare **ConnectivityMode.AutoDetect** per indicare che il servizio comunica con l'inoltro di Azure tramite TCP.</span><span class="sxs-lookup"><span data-stu-id="85ad8-236">That same service could specify **ConnectivityMode.AutoDetect** so that the service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="85ad8-237">Creare l'host del servizio usando l'URI creato precedentemente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="85ad8-237">Create the service host, using the URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="85ad8-238">L'host del servizio è l'oggetto WCF che crea un'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-238">The service host is the WCF object that instantiates the service.</span></span> <span data-ttu-id="85ad8-239">In questo caso, viene passato il tipo di servizio che si vuole creare (`EchoService`), insieme all'indirizzo in cui si vuole esporre il servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-239">Here, you pass it the type of service you want to create (an `EchoService` type), and also to the address at which you want to expose the service.</span></span>
3. <span data-ttu-id="85ad8-240">All'inizio del file Program.cs aggiungere riferimenti a [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) e [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span><span class="sxs-lookup"><span data-stu-id="85ad8-240">At the top of the Program.cs file, add references to [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="85ad8-241">Tornando a `Main()`, configurare l'endpoint per abilitare l'accesso pubblico.</span><span class="sxs-lookup"><span data-stu-id="85ad8-241">Back in `Main()`, configure the endpoint to enable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="85ad8-242">Questo passaggio segnala al servizio di inoltro che l'applicazione può essere trovata pubblicamente esaminando il feed ATOM per il progetto.</span><span class="sxs-lookup"><span data-stu-id="85ad8-242">This step informs the relay service that your application can be found publicly by examining the ATOM feed for your project.</span></span> <span data-ttu-id="85ad8-243">Se si imposta **DiscoveryType** su **private**, un client sarà comunque in grado di accedere al servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-243">If you set **DiscoveryType** to **private**, a client would still be able to access the service.</span></span> <span data-ttu-id="85ad8-244">Quest'ultimo non sarà tuttavia visibile durante la ricerca nello spazio dei nomi Relay.</span><span class="sxs-lookup"><span data-stu-id="85ad8-244">However, the service would not appear when it searches the Relay namespace.</span></span> <span data-ttu-id="85ad8-245">Il client dovrà invece conoscere in anticipo il percorso dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="85ad8-245">Instead, the client would have to know the endpoint path beforehand.</span></span>
5. <span data-ttu-id="85ad8-246">Applicare le credenziali del servizio agli endpoint di servizio definiti nel file App.config:</span><span class="sxs-lookup"><span data-stu-id="85ad8-246">Apply the service credentials to the service endpoints defined in the App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="85ad8-247">Come spiegato nel passaggio precedente, nel file di configurazione potrebbero essere stati dichiarati più servizi e più endpoint.</span><span class="sxs-lookup"><span data-stu-id="85ad8-247">As stated in the previous step, you could have declared multiple services and endpoints in the configuration file.</span></span> <span data-ttu-id="85ad8-248">In tal caso, questo codice scorrerebbe il file di configurazione per cercare tutti gli endpoint a cui applicare le credenziali.</span><span class="sxs-lookup"><span data-stu-id="85ad8-248">If you had, this code would traverse the configuration file and search for every endpoint to which it should apply your credentials.</span></span> <span data-ttu-id="85ad8-249">Per questa esercitazione, nel file di configurazione è tuttavia contenuto un solo endpoint.</span><span class="sxs-lookup"><span data-stu-id="85ad8-249">However, for this tutorial, the configuration file has only one endpoint.</span></span>

### <a name="open-the-service-host"></a><span data-ttu-id="85ad8-250">Aprire l'host del servizio</span><span class="sxs-lookup"><span data-stu-id="85ad8-250">Open the service host</span></span>

1. <span data-ttu-id="85ad8-251">Aprire il servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-251">Open the service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="85ad8-252">Informare l'utente che il servizio è in esecuzione e spiegargli come arrestarlo.</span><span class="sxs-lookup"><span data-stu-id="85ad8-252">Inform the user that the service is running, and explain how to shut down the service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="85ad8-253">Al termine, chiudere l'host del servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-253">When finished, close the service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="85ad8-254">Premere **CTRL+MAIUSC+B** per compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="85ad8-254">Press **Ctrl+Shift+B** to build the project.</span></span>

### <a name="example"></a><span data-ttu-id="85ad8-255">Esempio</span><span class="sxs-lookup"><span data-stu-id="85ad8-255">Example</span></span>

<span data-ttu-id="85ad8-256">Il codice del servizio completato comparirà come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="85ad8-256">Your completed service code should appear as follows.</span></span> <span data-ttu-id="85ad8-257">Il codice include il contratto di servizio e l'implementazione dei passaggi precedenti nell'esercitazione e ospita il servizio in un'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="85ad8-257">The code includes the service contract and implementation from previous steps in the tutorial, and hosts the service in a console application.</span></span>

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create the credentials object for the endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create the service URI based on the service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create the service host reading the configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create the ServiceRegistrySettings behavior for the endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add the Relay credentials to all endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open the service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            // Close the service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-the-service-contract"></a><span data-ttu-id="85ad8-258">Creare un client WCF per il contratto di servizio</span><span class="sxs-lookup"><span data-stu-id="85ad8-258">Create a WCF client for the service contract</span></span>

<span data-ttu-id="85ad8-259">Il passaggio successivo consiste nel creare un'applicazione client e nel definire il contratto di servizio che sarà implementato nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="85ad8-259">The next step is to create a client application and define the service contract you will implement in later steps.</span></span> <span data-ttu-id="85ad8-260">Si noti che molti di questi passaggi sono simili ai passaggi usati per la creazione di un servizio: ovvero definizione di un contratto, modifica di un file App.config, uso delle credenziali per la connessione al servizio di inoltro e così via.</span><span class="sxs-lookup"><span data-stu-id="85ad8-260">Note that many of these steps resemble the steps used to create a service: defining a contract, editing an App.config file, using credentials to connect to the relay service, and so on.</span></span> <span data-ttu-id="85ad8-261">Il codice usato per eseguire queste attività viene fornito nell'esempio che segue la procedura.</span><span class="sxs-lookup"><span data-stu-id="85ad8-261">The code used for these tasks is provided in the example following the procedure.</span></span>

1. <span data-ttu-id="85ad8-262">Creare un nuovo progetto nella soluzione Visual Studio attuale per il client eseguendo le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="85ad8-262">Create a new project in the current Visual Studio solution for the client by doing the following:</span></span>

   1. <span data-ttu-id="85ad8-263">Nella stessa soluzione che include il servizio in Esplora soluzioni fare clic con il pulsante destro del mouse sulla soluzione attuale, non sul progetto, e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-263">In Solution Explorer, in the same solution that contains the service, right-click the current solution (not the project), and click **Add**.</span></span> <span data-ttu-id="85ad8-264">Fare clic su **Nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-264">Then click **New Project**.</span></span>
   2. <span data-ttu-id="85ad8-265">Nella finestra di dialogo **Aggiungi nuovo progetto** fare clic su **Visual C#**. Se **Visual C#** non è visibile, cercare in **Other Languages** (Altri linguaggi), selezionare il modello **App console (.NET Framework)** e denominarlo **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-265">In the **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select the **Console App (.NET Framework)** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="85ad8-266">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-266">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="85ad8-267">In Esplora soluzioni fare doppio clic sul file Program.cs nel progetto **EchoClient** per aprirlo nell'editor, se non è già aperto.</span><span class="sxs-lookup"><span data-stu-id="85ad8-267">In Solution Explorer, double-click the Program.cs file in the **EchoClient** project to open it in the editor, if it is not already open.</span></span>
3. <span data-ttu-id="85ad8-268">Modificare il nome dello spazio dei nomi da nome predefinito di `EchoClient` a `Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="85ad8-268">Change the namespace name from its default name of `EchoClient` to `Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="85ad8-269">Installare il [pacchetto NuGet del bus di servizio](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **EchoClient** e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-269">Install the [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click the **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="85ad8-270">Fare clic sulla scheda **Sfoglia** e cercare `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="85ad8-270">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="85ad8-271">Fare clic su **Installa**e accettare le condizioni per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="85ad8-271">Click **Install**, and accept the terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="85ad8-272">Aggiungere un'istruzione `using` per lo spazio dei nomi [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) nel file Program.cs.</span><span class="sxs-lookup"><span data-stu-id="85ad8-272">Add a `using` statement for the [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in the Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="85ad8-273">Aggiungere la definizione del contratto di servizio allo spazio dei nomi, come mostrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="85ad8-273">Add the service contract definition to the namespace, as shown in the following example.</span></span> <span data-ttu-id="85ad8-274">Si noti che questa definizione è identica alla definizione usata nel progetto **Service**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-274">Note that this definition is identical to the definition used in the **Service** project.</span></span> <span data-ttu-id="85ad8-275">È necessario aggiungere il codice alla parte iniziale dello spazio dei nomi `Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="85ad8-275">You should add this code at the top of the `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="85ad8-276">Premere **CTRL+MAIUSC+B** per compilare il client.</span><span class="sxs-lookup"><span data-stu-id="85ad8-276">Press **Ctrl+Shift+B** to build the client.</span></span>

### <a name="example"></a><span data-ttu-id="85ad8-277">Esempio</span><span class="sxs-lookup"><span data-stu-id="85ad8-277">Example</span></span>

<span data-ttu-id="85ad8-278">Il codice seguente illustra lo stato corrente del file Program.cs nel progetto **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-278">The following code shows the current status of the Program.cs file in the **EchoClient** project.</span></span>

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-the-wcf-client"></a><span data-ttu-id="85ad8-279">Configurare il client WCF</span><span class="sxs-lookup"><span data-stu-id="85ad8-279">Configure the WCF client</span></span>

<span data-ttu-id="85ad8-280">In questo passaggio si crea un file App.config per un'applicazione client di base che accede al servizio creato in precedenza in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="85ad8-280">In this step, you create an App.config file for a basic client application that accesses the service created previously in this tutorial.</span></span> <span data-ttu-id="85ad8-281">Il file App.config definisce il contratto, il binding e il nome dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="85ad8-281">This App.config file defines the contract, binding, and name of the endpoint.</span></span> <span data-ttu-id="85ad8-282">Il codice usato per eseguire queste attività viene fornito nell'esempio che segue la procedura.</span><span class="sxs-lookup"><span data-stu-id="85ad8-282">The code used for these tasks is provided in the example following the procedure.</span></span>

1. <span data-ttu-id="85ad8-283">In Esplora soluzioni fare doppio clic su **App.config** nel progetto **EchoClient** per aprire il file nell'editor di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-283">In Solution Explorer, in the **EchoClient** project, double-click **App.config** to open the file in the Visual Studio editor.</span></span>
2. <span data-ttu-id="85ad8-284">Nell'elemento `<appSettings>` sostituire i segnaposto con il nome dello spazio dei nomi del servizio e la chiave di firma di accesso condiviso copiata nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="85ad8-284">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="85ad8-285">Nell'elemento system.serviceModel aggiungere un elemento `<client>`.</span><span class="sxs-lookup"><span data-stu-id="85ad8-285">Within the system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="85ad8-286">Questo passaggio dichiara che si sta definendo un'applicazione client di tipo WCF.</span><span class="sxs-lookup"><span data-stu-id="85ad8-286">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="85ad8-287">Nell'elemento `client` definire il nome, il contratto e il tipo di binding per l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="85ad8-287">Within the `client` element, define the name, contract, and binding type for the endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="85ad8-288">Questo passaggio specifica il nome dell'endpoint, il contratto definito nel servizio e l'uso del protocollo TCP da parte dell'applicazione per comunicare con l'inoltro di Azure.</span><span class="sxs-lookup"><span data-stu-id="85ad8-288">This step defines the name of the endpoint, the contract defined in the service, and the fact that the client application uses TCP to communicate with Azure Relay.</span></span> <span data-ttu-id="85ad8-289">Il nome dell'endpoint viene usato nel passaggio successivo per collegare questa configurazione dell'endpoint con l'URI del servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-289">The endpoint name is used in the next step to link this endpoint configuration with the service URI.</span></span>
5. <span data-ttu-id="85ad8-290">Fare clic su **File** quindi su **Salva tutto**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-290">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="85ad8-291">Esempio</span><span class="sxs-lookup"><span data-stu-id="85ad8-291">Example</span></span>

<span data-ttu-id="85ad8-292">Il codice seguente mostra il file App.config per il client Echo.</span><span class="sxs-lookup"><span data-stu-id="85ad8-292">The following code shows the App.config file for the Echo client.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-the-wcf-client"></a><span data-ttu-id="85ad8-293">Implementare il client WCF</span><span class="sxs-lookup"><span data-stu-id="85ad8-293">Implement the WCF client</span></span>
<span data-ttu-id="85ad8-294">In questo passaggio si implementa un'applicazione client di base che accede al servizio creato in precedenza in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="85ad8-294">In this step, you implement a basic client application that accesses the service you created previously in this tutorial.</span></span> <span data-ttu-id="85ad8-295">Analogamente al servizio, il client esegue molte delle stesse operazioni per accedere all'inoltro di Azure:</span><span class="sxs-lookup"><span data-stu-id="85ad8-295">Similar to the service, the client performs many of the same operations to access Azure Relay:</span></span>

1. <span data-ttu-id="85ad8-296">Imposta la modalità di connessione.</span><span class="sxs-lookup"><span data-stu-id="85ad8-296">Sets the connectivity mode.</span></span>
2. <span data-ttu-id="85ad8-297">Crea l'URI che individua il servizio host.</span><span class="sxs-lookup"><span data-stu-id="85ad8-297">Creates the URI that locates the host service.</span></span>
3. <span data-ttu-id="85ad8-298">Definisce le credenziali di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="85ad8-298">Defines the security credentials.</span></span>
4. <span data-ttu-id="85ad8-299">Applica le credenziali alla connessione.</span><span class="sxs-lookup"><span data-stu-id="85ad8-299">Applies the credentials to the connection.</span></span>
5. <span data-ttu-id="85ad8-300">Apre la connessione.</span><span class="sxs-lookup"><span data-stu-id="85ad8-300">Opens the connection.</span></span>
6. <span data-ttu-id="85ad8-301">Esegue attività specifiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="85ad8-301">Performs the application-specific tasks.</span></span>
7. <span data-ttu-id="85ad8-302">Chiude la connessione.</span><span class="sxs-lookup"><span data-stu-id="85ad8-302">Closes the connection.</span></span>

<span data-ttu-id="85ad8-303">Una delle differenze principali, tuttavia, consiste nel fatto che l'applicazione client usa un canale per connettersi al servizio di inoltro, mentre il servizio usa una chiamata a **ServiceHost**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-303">However, one of the main differences is that the client application uses a channel to connect to the relay service, whereas the service uses a call to **ServiceHost**.</span></span> <span data-ttu-id="85ad8-304">Il codice usato per eseguire queste attività viene fornito nell'esempio che segue la procedura.</span><span class="sxs-lookup"><span data-stu-id="85ad8-304">The code used for these tasks is provided in the example following the procedure.</span></span>

### <a name="implement-a-client-application"></a><span data-ttu-id="85ad8-305">Implementare un'applicazione client</span><span class="sxs-lookup"><span data-stu-id="85ad8-305">Implement a client application</span></span>
1. <span data-ttu-id="85ad8-306">Impostare la modalità di connessione su **AutoDetect**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-306">Set the connectivity mode to **AutoDetect**.</span></span> <span data-ttu-id="85ad8-307">Aggiungere il codice seguente nel metodo `Main()` dell'applicazione **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-307">Add the following code inside the `Main()` method of the **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="85ad8-308">Definire le variabile per includere i valori per lo spazio dei nomi del servizio e la chiave di firma di accesso condiviso letti dalla console.</span><span class="sxs-lookup"><span data-stu-id="85ad8-308">Define variables to hold the values for the service namespace, and SAS key that are read from the console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="85ad8-309">Creare l'URI che definisce il percorso dell'host nel progetto di inoltro.</span><span class="sxs-lookup"><span data-stu-id="85ad8-309">Create the URI that defines the location of the host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="85ad8-310">Creare l'oggetto credential per l'endpoint dello spazio dei nomi del servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-310">Create the credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="85ad8-311">Creare la channel factory che carica la configurazione descritta nel file App.config.</span><span class="sxs-lookup"><span data-stu-id="85ad8-311">Create the channel factory that loads the configuration described in the App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="85ad8-312">Una channel factory è un oggetto WCF che crea un canale attraverso il quale comunicano le applicazioni di servizio e client.</span><span class="sxs-lookup"><span data-stu-id="85ad8-312">A channel factory is a WCF object that creates a channel through which the service and client applications communicate.</span></span>
6. <span data-ttu-id="85ad8-313">Applicare le credenziali.</span><span class="sxs-lookup"><span data-stu-id="85ad8-313">Apply the credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="85ad8-314">Creare e aprire il canale per il servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-314">Create and open the channel to the service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="85ad8-315">Scrivere l'interfaccia utente di base e la funzionalità per echo.</span><span class="sxs-lookup"><span data-stu-id="85ad8-315">Write the basic user interface and functionality for the echo.</span></span>

    ```csharp
    Console.WriteLine("Enter text to echo (or [Enter] to exit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    <span data-ttu-id="85ad8-316">Si noti che il codice usa l'istanza dell'oggetto canale come proxy per il servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-316">Note that the code uses the instance of the channel object as a proxy for the service.</span></span>
9. <span data-ttu-id="85ad8-317">Chiudere il canale, quindi chiudere la factory.</span><span class="sxs-lookup"><span data-stu-id="85ad8-317">Close the channel, and close the factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a><span data-ttu-id="85ad8-318">Esempio</span><span class="sxs-lookup"><span data-stu-id="85ad8-318">Example</span></span>

<span data-ttu-id="85ad8-319">Il codice completo dovrebbe apparire come mostrato di seguito e illustra come creare un'applicazione client, come chiamare le operazioni del servizio e come chiudere il client al termine della chiamata dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="85ad8-319">Your completed code should appear as follows, showing how to create a client application, how to call the operations of the service, and how to close the client after the operation call is finished.</span></span>

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text to echo (or [Enter] to exit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="run-the-applications"></a><span data-ttu-id="85ad8-320">Eseguire le applicazioni</span><span class="sxs-lookup"><span data-stu-id="85ad8-320">Run the applications</span></span>

1. <span data-ttu-id="85ad8-321">Premere **CTRL+MAIUSC+B** per compilare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="85ad8-321">Press **Ctrl+Shift+B** to build the solution.</span></span> <span data-ttu-id="85ad8-322">Verranno compilati sia il progetto client che il progetto di servizio creati nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="85ad8-322">This builds both the client project and the service project that you created in the previous steps.</span></span>
2. <span data-ttu-id="85ad8-323">Prima di eseguire l'applicazione client, è necessario assicurarsi che l'applicazione di servizio sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="85ad8-323">Before running the client application, you must make sure that the service application is running.</span></span> <span data-ttu-id="85ad8-324">In Esplora soluzioni in Visual Studio fare clic con il pulsante destro del mouse sulla soluzione **EchoService** e scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-324">In Solution Explorer in Visual Studio, right-click the **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="85ad8-325">Nella finestra di dialogo delle proprietà della soluzione fare clic su **Progetto di avvio** e quindi sul pulsante **Progetti di avvio multipli**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-325">In the solution properties dialog box, click **Startup Project**, then click the **Multiple startup projects** button.</span></span> <span data-ttu-id="85ad8-326">Verificare che **EchoService** sia visualizzato per primo nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="85ad8-326">Make sure **EchoService** appears first in the list.</span></span>
4. <span data-ttu-id="85ad8-327">Impostare su **Avvio** la casella **Azione** per entrambi i progetti **EchoService** ed **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-327">Set the **Action** box for both the **EchoService** and **EchoClient** projects to **Start**.</span></span>

    ![][5]
5. <span data-ttu-id="85ad8-328">Fare clic su **Dipendenze progetto**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-328">Click **Project Dependencies**.</span></span> <span data-ttu-id="85ad8-329">Nella casella **Progetti** selezionare **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-329">In the **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="85ad8-330">Nella casella **Dipendente da** verificare che sia selezionato **EchoService**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-330">In the **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="85ad8-331">Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-331">Click **OK** to dismiss the **Properties** dialog.</span></span>
7. <span data-ttu-id="85ad8-332">Premere **F5** per eseguire entrambi i progetti.</span><span class="sxs-lookup"><span data-stu-id="85ad8-332">Press **F5** to run both projects.</span></span>
8. <span data-ttu-id="85ad8-333">Verranno visualizzate entrambe le finestre della console e verrà richiesto il nome dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="85ad8-333">Both console windows open and prompt you for the namespace name.</span></span> <span data-ttu-id="85ad8-334">Il servizio deve essere eseguito per primo. Nella finestra della console **EchoService** immettere lo spazio dei nomi e quindi premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="85ad8-334">The service must run first, so in the **EchoService** console window, enter the namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="85ad8-335">Verrà quindi chiesto di specificare la chiave di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="85ad8-335">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="85ad8-336">Immettere la chiave di firma di accesso condiviso e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="85ad8-336">Enter the SAS key and press ENTER.</span></span>

    <span data-ttu-id="85ad8-337">Ecco un esempio dell'output dalla finestra della console.</span><span class="sxs-lookup"><span data-stu-id="85ad8-337">Here is example output from the console window.</span></span> <span data-ttu-id="85ad8-338">Si noti che i valori specificati hanno semplicemente scopo esemplificativo.</span><span class="sxs-lookup"><span data-stu-id="85ad8-338">Note that the values provided here are for example purposes only.</span></span>

    <span data-ttu-id="85ad8-339">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="85ad8-339">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="85ad8-340">L'applicazione di servizio stampa l'indirizzo su cui è in ascolto nella finestra della console, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="85ad8-340">The service application prints to the console window the address on which it's listening, as seen in the following example.</span></span>

    <span data-ttu-id="85ad8-341">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`</span><span class="sxs-lookup"><span data-stu-id="85ad8-341">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`</span></span>
10. <span data-ttu-id="85ad8-342">Nella finestra della console **EchoClient** immettere le stesse informazioni immesse precedentemente per l'applicazione di servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-342">In the **EchoClient** console window, enter the same information that you entered previously for the service application.</span></span> <span data-ttu-id="85ad8-343">Eseguire la procedura precedente per immettere gli stessi valori di spazio dei nomi del servizio e chiave di firma di accesso condiviso per l'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="85ad8-343">Follow the previous steps to enter the same service namespace and SAS key values for the client application.</span></span>
11. <span data-ttu-id="85ad8-344">Dopo l'immissione di questi valori, il client aprirà un canale per il servizio e richiederà l'immissione dello stesso testo, come mostrato nell'esempio di output della console seguente.</span><span class="sxs-lookup"><span data-stu-id="85ad8-344">After entering these values, the client opens a channel to the service and prompts you to enter some text as seen in the following console output example.</span></span>

    `Enter text to echo (or [Enter] to exit):`

    <span data-ttu-id="85ad8-345">Immettere il testo da inviare all'applicazione del servizio, quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="85ad8-345">Enter some text to send to the service application and press Enter.</span></span> <span data-ttu-id="85ad8-346">Il testo viene inviato al servizio tramite l'operazione del servizio Echo e viene visualizzato nella finestra della console del servizio, come illustrato nell'output di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="85ad8-346">This text is sent to the service through the Echo service operation and appears in the service console window as in the following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="85ad8-347">L'applicazione client riceve il valore restituito dell'operazione `Echo`, ovvero il testo originale, quindi lo stampa nella finestra della console.</span><span class="sxs-lookup"><span data-stu-id="85ad8-347">The client application receives the return value of the `Echo` operation, which is the original text, and prints it to its console window.</span></span> <span data-ttu-id="85ad8-348">Di seguito è riportato un output di esempio dalla finestra della console client.</span><span class="sxs-lookup"><span data-stu-id="85ad8-348">The following is example output from the client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="85ad8-349">È possibile continuare a inviare messaggi di testo dal client al servizio in questo modo.</span><span class="sxs-lookup"><span data-stu-id="85ad8-349">You can continue sending text messages from the client to the service in this manner.</span></span> <span data-ttu-id="85ad8-350">Al termine, premere INVIO nelle finestre del client e della console per terminare entrambe le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="85ad8-350">When you are finished, press Enter in the client and service console windows to end both applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85ad8-351">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="85ad8-351">Next steps</span></span>

<span data-ttu-id="85ad8-352">Questa esercitazione ha illustrato come compilare un'applicazione client e di servizio di inoltro di Azure usando le funzionalità di inoltro WCF del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="85ad8-352">This tutorial showed how to build an Azure Relay client application and service using the WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="85ad8-353">Per un'esercitazione simile che usa la [messaggistica](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging) del bus di servizio, vedere [Introduzione alle code del bus di servizio](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="85ad8-353">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="85ad8-354">Per altre informazioni sul servizio d'inoltro di Azure, vedere gli argomenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="85ad8-354">To learn more about Azure Relay, see the following topics.</span></span>

* [<span data-ttu-id="85ad8-355">Panoramica dell'architettura del bus di servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="85ad8-355">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="85ad8-356">Panoramica del servizio di inoltro di Azure</span><span class="sxs-lookup"><span data-stu-id="85ad8-356">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="85ad8-357">Come usare il servizio di inoltro WCF con .NET</span><span class="sxs-lookup"><span data-stu-id="85ad8-357">How to use the WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
