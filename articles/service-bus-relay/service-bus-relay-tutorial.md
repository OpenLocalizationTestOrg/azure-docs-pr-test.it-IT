---
title: esercitazione di inoltro di Service Bus WCF aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: 78cd52ef51e9fcfcda2f13ec54bde3af50d76476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="01007-103">Esercitazione sull'inoltro WCF di Azure</span><span class="sxs-lookup"><span data-stu-id="01007-103">Azure WCF Relay tutorial</span></span>

<span data-ttu-id="01007-104">Questa esercitazione viene descritto come toobuild WCF semplice inoltro applicazione client e un servizio usando l'inoltro di Azure.</span><span class="sxs-lookup"><span data-stu-id="01007-104">This tutorial describes how toobuild a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="01007-105">Per un'esercitazione simile che usa la [messaggistica](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging) del bus di servizio, vedere [Introduzione alle code del bus di servizio](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="01007-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="01007-106">Esecuzione di questa esercitazione consente di conoscere i passaggi di hello toocreate richiesto un'applicazione client e il servizio di inoltro WCF.</span><span class="sxs-lookup"><span data-stu-id="01007-106">Working through this tutorial gives you an understanding of hello steps that are required toocreate a WCF Relay client and service application.</span></span> <span data-ttu-id="01007-107">Come per le rispettive controparti WCF originali, un servizio è un costrutto che espone uno o più endpoint, ognuno dei quali espone a sua volta una o più operazioni del servizio.</span><span class="sxs-lookup"><span data-stu-id="01007-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="01007-108">endpoint Hello di un servizio specifica un indirizzo in cui è possibile trovare il servizio di hello, un'associazione che contiene informazioni hello che un client deve comunicare con il servizio di hello e un contratto che definisce funzionalità hello fornita dal client di tooits hello del servizio.</span><span class="sxs-lookup"><span data-stu-id="01007-108">hello endpoint of a service specifies an address where hello service can be found, a binding that contains hello information that a client must communicate with hello service, and a contract that defines hello functionality provided by hello service tooits clients.</span></span> <span data-ttu-id="01007-109">Hello differenza principale tra WCF e di inoltro WCF è che tale endpoint hello è esposto nel cloud hello anziché in locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="01007-109">hello main difference between WCF and WCF Relay is that hello endpoint is exposed in hello cloud instead of locally on your computer.</span></span>

<span data-ttu-id="01007-110">Dopo aver eseguito la sequenza di hello di argomenti in questa esercitazione, si disporrà di un servizio in esecuzione e un client che è possibile richiamare le operazioni del servizio hello hello.</span><span class="sxs-lookup"><span data-stu-id="01007-110">After you work through hello sequence of topics in this tutorial, you will have a running service, and a client that can invoke hello operations of hello service.</span></span> <span data-ttu-id="01007-111">Hello primo argomento viene descritto come tooset un account.</span><span class="sxs-lookup"><span data-stu-id="01007-111">hello first topic describes how tooset up an account.</span></span> <span data-ttu-id="01007-112">passaggi successivi Hello descrivono come toodefine un servizio che usa un contratto, come tooimplement hello servizio e come tooconfigure hello servizio nel codice.</span><span class="sxs-lookup"><span data-stu-id="01007-112">hello next steps describe how toodefine a service that uses a contract, how tooimplement hello service, and how tooconfigure hello service in code.</span></span> <span data-ttu-id="01007-113">Vengono inoltre descritte come servizio hello toohost ed eseguire.</span><span class="sxs-lookup"><span data-stu-id="01007-113">They also describe how toohost and run hello service.</span></span> <span data-ttu-id="01007-114">Hello servizio creato è Self-hosted e hello client e servizio eseguito hello stesso computer.</span><span class="sxs-lookup"><span data-stu-id="01007-114">hello service that is created is self-hosted and hello client and service run on hello same computer.</span></span> <span data-ttu-id="01007-115">È possibile configurare il servizio di hello tramite codice o un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="01007-115">You can configure hello service by using either code or a configuration file.</span></span>

<span data-ttu-id="01007-116">Hello finale tre descritta come toocreate un'applicazione client, configurare un'applicazione client, hello e creare e utilizzare un client che è possibile accedere alla funzionalità hello dell'host hello.</span><span class="sxs-lookup"><span data-stu-id="01007-116">hello final three steps describe how toocreate a client application, configure hello client application, and create and use a client that can access hello functionality of hello host.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01007-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="01007-117">Prerequisites</span></span>

<span data-ttu-id="01007-118">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="01007-118">toocomplete this tutorial, you'll need hello following:</span></span>

* <span data-ttu-id="01007-119">[Microsoft Visual Studio 2015 o versione successiva](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="01007-119">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="01007-120">Questa esercitazione usa Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="01007-120">This tutorial uses Visual Studio 2017.</span></span>
* <span data-ttu-id="01007-121">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="01007-121">An active Azure account.</span></span> <span data-ttu-id="01007-122">Se non si ha un account, è possibile crearne uno gratuito in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="01007-122">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="01007-123">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="01007-123">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="01007-124">Creare uno spazio dei nomi del servizio</span><span class="sxs-lookup"><span data-stu-id="01007-124">Create a service namespace</span></span>

<span data-ttu-id="01007-125">primo passaggio Hello è toocreate uno spazio dei nomi e tooobtain un [firma di accesso condiviso (SAS)](../service-bus-messaging/service-bus-sas.md) chiave.</span><span class="sxs-lookup"><span data-stu-id="01007-125">hello first step is toocreate a namespace, and tooobtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="01007-126">Uno spazio dei nomi fornisce un limite per ogni applicazione esposta attraverso il servizio di inoltro hello.</span><span class="sxs-lookup"><span data-stu-id="01007-126">A namespace provides an application boundary for each application exposed through hello relay service.</span></span> <span data-ttu-id="01007-127">Una chiave di firma di accesso condiviso viene generata automaticamente dal sistema hello quando viene creato uno spazio dei nomi del servizio.</span><span class="sxs-lookup"><span data-stu-id="01007-127">A SAS key is automatically generated by hello system when a service namespace is created.</span></span> <span data-ttu-id="01007-128">combinazione di Hello di spazio dei nomi servizio e la chiave di firma di accesso condiviso fornisce le credenziali di hello per applicazione tooan di accesso tooauthenticate Azure.</span><span class="sxs-lookup"><span data-stu-id="01007-128">hello combination of service namespace and SAS key provides hello credentials for Azure tooauthenticate access tooan application.</span></span> <span data-ttu-id="01007-129">Seguire hello [le istruzioni qui](relay-create-namespace-portal.md) toocreate uno spazio dei nomi di inoltro.</span><span class="sxs-lookup"><span data-stu-id="01007-129">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="01007-130">Definire un contratto del servizio WCF</span><span class="sxs-lookup"><span data-stu-id="01007-130">Define a WCF service contract</span></span>

<span data-ttu-id="01007-131">contratto di servizio Hello specifica il servizio supporta hello operations (hello web terminologia relativa ai servizi per i metodi o funzioni).</span><span class="sxs-lookup"><span data-stu-id="01007-131">hello service contract specifies what operations (hello web service terminology for methods or functions) hello service supports.</span></span> <span data-ttu-id="01007-132">I contratti vengono creati definendo un'interfaccia C++, C# o Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="01007-132">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="01007-133">Ogni metodo nell'interfaccia hello corrisponde tooa operazione del servizio specifica.</span><span class="sxs-lookup"><span data-stu-id="01007-133">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="01007-134">Ogni interfaccia deve essere hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) tooit applicare l'attributo e ogni operazione deve essere hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) tooit attributo applicato.</span><span class="sxs-lookup"><span data-stu-id="01007-134">Each interface must have hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied tooit, and each operation must have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied tooit.</span></span> <span data-ttu-id="01007-135">Se un metodo in un'interfaccia con hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attributo non dispone di hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attributo, questo metodo non è esposto.</span><span class="sxs-lookup"><span data-stu-id="01007-135">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="01007-136">Nell'esempio hello hello procedura viene fornito codice di Hello per le attività.</span><span class="sxs-lookup"><span data-stu-id="01007-136">hello code for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="01007-137">Per una descrizione più ampia dei contratti e servizi, vedere [progettazione e implementazione di servizi](https://msdn.microsoft.com/library/ms729746.aspx) in hello documentazione WCF.</span><span class="sxs-lookup"><span data-stu-id="01007-137">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in hello WCF documentation.</span></span>

### <a name="create-a-relay-contract-with-an-interface"></a><span data-ttu-id="01007-138">Creare un contratto di inoltro con un'interfaccia</span><span class="sxs-lookup"><span data-stu-id="01007-138">Create a relay contract with an interface</span></span>

1. <span data-ttu-id="01007-139">Aprire Visual Studio come amministratore facendo clic con il programma hello in hello **avviare** menu e selezionando **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="01007-139">Open Visual Studio as an administrator by right-clicking hello program in hello **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="01007-140">Creare un nuovo progetto di applicazione console.</span><span class="sxs-lookup"><span data-stu-id="01007-140">Create a new console application project.</span></span> <span data-ttu-id="01007-141">Fare clic su hello **File** dal menu **New**, quindi fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="01007-141">Click hello **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="01007-142">In hello **nuovo progetto** finestra di dialogo, fare clic su **Visual c#** (se **Visual c#** non è visualizzato, cercarlo in **altri linguaggi**).</span><span class="sxs-lookup"><span data-stu-id="01007-142">In hello **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="01007-143">Fare clic su hello **applicazione Console (.NET Framework)** , modello e denominarlo **EchoService**.</span><span class="sxs-lookup"><span data-stu-id="01007-143">Click hello **Console App (.NET Framework)** template, and name it **EchoService**.</span></span> <span data-ttu-id="01007-144">Fare clic su **OK** progetto hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="01007-144">Click **OK** toocreate hello project.</span></span>

    ![][2]

3. <span data-ttu-id="01007-145">Installare il pacchetto NuGet di Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="01007-145">Install hello Service Bus NuGet package.</span></span> <span data-ttu-id="01007-146">Questo pacchetto aggiunge automaticamente le librerie del Bus di servizio toohello riferimenti, nonché hello WCF **System. ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="01007-146">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="01007-147">[System. ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) spazio dei nomi hello consente tooprogrammatically accesso hello funzionalità di base di WCF.</span><span class="sxs-lookup"><span data-stu-id="01007-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables you tooprogrammatically access hello basic features of WCF.</span></span> <span data-ttu-id="01007-148">Bus di servizio Usa molti degli oggetti hello e degli attributi WCF toodefine di contratti di servizio.</span><span class="sxs-lookup"><span data-stu-id="01007-148">Service Bus uses many of hello objects and attributes of WCF toodefine service contracts.</span></span>

    <span data-ttu-id="01007-149">In Esplora soluzioni, fare clic sul progetto hello e quindi fare clic su **Gestisci pacchetti NuGet... **. Fare clic su hello **Sfoglia** tab, quindi cercare `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="01007-149">In Solution Explorer, right-click hello project, and then click **Manage NuGet Packages...**. Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="01007-150">Selezionare il nome del progetto hello hello **versioni** casella.</span><span class="sxs-lookup"><span data-stu-id="01007-150">Ensure that hello project name is selected in hello **Version(s)** box.</span></span> <span data-ttu-id="01007-151">Fare clic su **installare**e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="01007-151">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="01007-152">In Esplora soluzioni fare doppio clic su hello Program.cs file tooopen possa nell'editor di hello, se non è già aperta.</span><span class="sxs-lookup"><span data-stu-id="01007-152">In Solution Explorer, double-click hello Program.cs file tooopen it in hello editor, if it is not already open.</span></span>
5. <span data-ttu-id="01007-153">Aggiungere il seguente hello istruzioni using all'inizio di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="01007-153">Add hello following using statements at hello top of hello file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="01007-154">Spazio dei nomi hello Modifica nome predefinito di **EchoService** troppo**ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="01007-154">Change hello namespace name from its default name of **EchoService** too**Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="01007-155">Questa esercitazione viene utilizzato lo spazio dei nomi hello c# **ServiceBus**, ovvero hello dello spazio dei nomi di hello basati su contratto di tipo che viene utilizzato nel file di configurazione hello in hello gestito [configurare il client WCF hello](#configure-the-wcf-client) passaggio.</span><span class="sxs-lookup"><span data-stu-id="01007-155">This tutorial uses hello C# namespace **Microsoft.ServiceBus.Samples**, which is hello namespace of hello contract-based managed type that is used in hello configuration file in hello [Configure hello WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="01007-156">È possibile specificare qualsiasi spazio dei nomi desiderato quando si compila questo esempio. Tuttavia, esercitazione hello non funzionerà a meno che non è quindi modificare hello gli spazi dei nomi del contratto hello e del servizio di conseguenza, nel file di configurazione dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="01007-156">You can specify any namespace you want when you build this sample; however, hello tutorial will not work unless you then modify hello namespaces of hello contract and service accordingly, in hello application configuration file.</span></span> <span data-ttu-id="01007-157">spazio dei nomi Hello specificato nel file app. config file deve essere hello hello uguale allo spazio dei nomi hello specificato nel file c#.</span><span class="sxs-lookup"><span data-stu-id="01007-157">hello namespace specified in hello App.config file must be hello same as hello namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="01007-158">Direttamente dopo hello `Microsoft.ServiceBus.Samples` dichiarazione dello spazio dei nomi, ma nello spazio dei nomi hello, definire una nuova interfaccia denominata `IEchoContract` e applicare hello `ServiceContractAttribute` interfaccia toohello attributo con il valore dello spazio dei nomi `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="01007-158">Directly after hello `Microsoft.ServiceBus.Samples` namespace declaration, but within hello namespace, define a new interface named `IEchoContract` and apply hello `ServiceContractAttribute` attribute toohello interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="01007-159">il valore di spazio dei nomi Hello è diverso dallo spazio dei nomi hello usato nell'ambito di hello del codice.</span><span class="sxs-lookup"><span data-stu-id="01007-159">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="01007-160">Al contrario, il valore di spazio dei nomi hello viene utilizzato come identificatore univoco per questo contratto.</span><span class="sxs-lookup"><span data-stu-id="01007-160">Instead, hello namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="01007-161">Specificare in modo esplicito lo spazio dei nomi hello impedisce l'aggiunta il nome del contratto toohello valore dello spazio dei nomi predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="01007-161">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span> <span data-ttu-id="01007-162">Incollare hello seguente codice dopo la dichiarazione dello spazio dei nomi hello:</span><span class="sxs-lookup"><span data-stu-id="01007-162">Paste hello following code after hello namespace declaration:</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="01007-163">Spazio dei nomi del contratto di servizio hello contiene in genere, uno schema di denominazione che include informazioni sulla versione.</span><span class="sxs-lookup"><span data-stu-id="01007-163">Typically, hello service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="01007-164">Inclusione di informazioni sulla versione nello spazio dei nomi del contratto di servizio hello consente modifiche principali di servizio tooisolate definendo un nuovo contratto di servizio con un nuovo spazio dei nomi ed esponendolo in un nuovo endpoint.</span><span class="sxs-lookup"><span data-stu-id="01007-164">Including version information in hello service contract namespace enables services tooisolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="01007-165">In questo modo, i client possono continuare contratto del servizio precedente toouse hello senza toobe aggiornato.</span><span class="sxs-lookup"><span data-stu-id="01007-165">In this manner, clients can continue toouse hello old service contract without having toobe updated.</span></span> <span data-ttu-id="01007-166">Le informazioni sulla versione possono essere costituite da una data o da un numero di build.</span><span class="sxs-lookup"><span data-stu-id="01007-166">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="01007-167">Per altre informazioni, vedere [Controllo delle versioni del servizio](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="01007-167">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="01007-168">Ai fini di hello di questa esercitazione, hello denominazione dello spazio dei nomi di contratto di servizio hello non contiene informazioni sulla versione.</span><span class="sxs-lookup"><span data-stu-id="01007-168">For hello purposes of this tutorial, hello naming scheme of hello service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="01007-169">All'interno di hello `IEchoContract` l'interfaccia, dichiarare un metodo per hello singola operazione hello `IEchoContract` espone contratto in hello interfaccia e applicare hello `OperationContractAttribute` metodo toohello di attributo che si desidera tooexpose come parte di hello pubblica inoltro WCF contratto, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="01007-169">Within hello `IEchoContract` interface, declare a method for hello single operation hello `IEchoContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public WCF Relay contract, as follows:</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="01007-170">Direttamente dopo hello `IEchoContract` definizione dell'interfaccia, dichiarare un canale che eredita sia da `IEchoContract` e anche toohello `IClientChannel` interfaccia, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="01007-170">Directly after hello `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also toohello `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="01007-171">Un canale è l'oggetto WCF hello attraverso cui client e host hello passare informazioni tooeach altri.</span><span class="sxs-lookup"><span data-stu-id="01007-171">A channel is hello WCF object through which hello host and client pass information tooeach other.</span></span> <span data-ttu-id="01007-172">In un secondo momento, si scriverà codice in base a informazioni di tooecho hello del canale tra due applicazioni hello.</span><span class="sxs-lookup"><span data-stu-id="01007-172">Later, you will write code against hello channel tooecho information between hello two applications.</span></span>
10. <span data-ttu-id="01007-173">Da hello **compilare** menu, fare clic su **Compila soluzione** o premere **Ctrl + MAIUSC + B** accuratezza hello tooconfirm del lavoro svolto finora.</span><span class="sxs-lookup"><span data-stu-id="01007-173">From hello **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="01007-174">Esempio</span><span class="sxs-lookup"><span data-stu-id="01007-174">Example</span></span>

<span data-ttu-id="01007-175">Hello di codice seguente mostra un'interfaccia di base che definisce un contratto di inoltro WCF.</span><span class="sxs-lookup"><span data-stu-id="01007-175">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

<span data-ttu-id="01007-176">Dopo aver creato hello interfaccia, è possibile implementare l'interfaccia hello.</span><span class="sxs-lookup"><span data-stu-id="01007-176">Now that hello interface is created, you can implement hello interface.</span></span>

## <a name="implement-hello-wcf-contract"></a><span data-ttu-id="01007-177">Contratto di implementare hello WCF</span><span class="sxs-lookup"><span data-stu-id="01007-177">Implement hello WCF contract</span></span>

<span data-ttu-id="01007-178">Creazione di un server di inoltro di Azure è necessario innanzitutto creare contratto hello, che viene definito tramite un'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="01007-178">Creating an Azure relay requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="01007-179">Per ulteriori informazioni sulla creazione di hello interfaccia, vedere il passaggio precedente di hello.</span><span class="sxs-lookup"><span data-stu-id="01007-179">For more information about creating hello interface, see hello previous step.</span></span> <span data-ttu-id="01007-180">passaggio successivo Hello è interfaccia hello tooimplement.</span><span class="sxs-lookup"><span data-stu-id="01007-180">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="01007-181">Ciò comporta la creazione di una classe denominata `EchoService` che implementa hello definito dall'utente `IEchoContract` interfaccia.</span><span class="sxs-lookup"><span data-stu-id="01007-181">This involves creating a class named `EchoService` that implements hello user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="01007-182">Dopo avere implementato l'interfaccia di hello, configurare l'interfaccia hello utilizzando un file di configurazione App. config.</span><span class="sxs-lookup"><span data-stu-id="01007-182">After you implement hello interface, you then configure hello interface using an App.config configuration file.</span></span> <span data-ttu-id="01007-183">file di configurazione Hello contiene le informazioni necessarie per un'applicazione hello, ad esempio nome hello del servizio di hello, il nome di hello del contratto hello e tipo hello di protocollo è toocommunicate utilizzato con il servizio di inoltro hello.</span><span class="sxs-lookup"><span data-stu-id="01007-183">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="01007-184">Nell'esempio hello hello procedura viene fornito codice di Hello utilizzato per queste attività.</span><span class="sxs-lookup"><span data-stu-id="01007-184">hello code used for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="01007-185">Per una discussione più generale su come un servizio tooimplement contratto, vedere [contratti di servizio che implementa](https://msdn.microsoft.com/library/ms733764.aspx) in hello documentazione WCF.</span><span class="sxs-lookup"><span data-stu-id="01007-185">For a more general discussion about how tooimplement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in hello WCF documentation.</span></span>

1. <span data-ttu-id="01007-186">Creare una nuova classe denominata `EchoService` direttamente dopo la definizione di hello di hello `IEchoContract` interfaccia.</span><span class="sxs-lookup"><span data-stu-id="01007-186">Create a new class named `EchoService` directly after hello definition of hello `IEchoContract` interface.</span></span> <span data-ttu-id="01007-187">Hello `EchoService` implementa hello `IEchoContract` interfaccia.</span><span class="sxs-lookup"><span data-stu-id="01007-187">hello `EchoService` class implements hello `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="01007-188">Le implementazioni di interfaccia tooother simili, è possibile implementare definizione hello in un file diverso.</span><span class="sxs-lookup"><span data-stu-id="01007-188">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="01007-189">Tuttavia, per questa esercitazione, implementazione hello si trova in hello lo stesso file di definizione dell'interfaccia hello e hello `Main` metodo.</span><span class="sxs-lookup"><span data-stu-id="01007-189">However, for this tutorial, hello implementation is located in hello same file as hello interface definition and hello `Main` method.</span></span>
2. <span data-ttu-id="01007-190">Applicare hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attributo toohello `IEchoContract` interfaccia.</span><span class="sxs-lookup"><span data-stu-id="01007-190">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello `IEchoContract` interface.</span></span> <span data-ttu-id="01007-191">attributo di Hello Specifica spazio dei nomi e nome del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="01007-191">hello attribute specifies hello service name and namespace.</span></span> <span data-ttu-id="01007-192">Al termine dell'operazione, hello `EchoService` classe viene visualizzata come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="01007-192">After doing so, hello `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="01007-193">Hello implementare `Echo` metodo definito in hello `IEchoContract` interfaccia hello `EchoService` classe.</span><span class="sxs-lookup"><span data-stu-id="01007-193">Implement hello `Echo` method defined in hello `IEchoContract` interface in hello `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="01007-194">Fare clic su **compilare**, quindi fare clic su **Compila soluzione** accuratezza hello tooconfirm del lavoro.</span><span class="sxs-lookup"><span data-stu-id="01007-194">Click **Build**, then click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="define-hello-configuration-for-hello-service-host"></a><span data-ttu-id="01007-195">Definire la configurazione per l'host del servizio hello hello</span><span class="sxs-lookup"><span data-stu-id="01007-195">Define hello configuration for hello service host</span></span>

1. <span data-ttu-id="01007-196">file di configurazione Hello è molto simile file di configurazione WCF tooa.</span><span class="sxs-lookup"><span data-stu-id="01007-196">hello configuration file is very similar tooa WCF configuration file.</span></span> <span data-ttu-id="01007-197">Include il nome del servizio hello, endpoint (vale a dire hello percorso inoltro Azure espone per i client e host toocommunicate reciprocamente) e hello associazione (tipo hello di protocollo utilizzato toocommunicate).</span><span class="sxs-lookup"><span data-stu-id="01007-197">It includes hello service name, endpoint (that is, hello location that Azure Relay exposes for clients and hosts toocommunicate with each other), and hello binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="01007-198">Hello differenza principale è che l'endpoint del servizio si riferisce tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, che non fa parte di .NET Framework hello.</span><span class="sxs-lookup"><span data-stu-id="01007-198">hello main difference is that this configured service endpoint refers tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of hello .NET Framework.</span></span> <span data-ttu-id="01007-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) è una delle associazioni hello definite dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="01007-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of hello bindings defined by hello service.</span></span>
2. <span data-ttu-id="01007-200">In **Esplora**, fare doppio clic su hello app. config file tooopen nell'editor di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="01007-200">In **Solution Explorer**, double-click hello App.config file tooopen it in hello Visual Studio editor.</span></span>
3. <span data-ttu-id="01007-201">In hello `<appSettings>` elemento, sostituire i segnaposto hello con nome hello dello spazio dei nomi di servizio e hello chiave di firma di accesso condiviso che è stato copiato in un passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="01007-201">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="01007-202">All'interno di hello `<system.serviceModel>` tag, aggiungere un `<services>` elemento.</span><span class="sxs-lookup"><span data-stu-id="01007-202">Within hello `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="01007-203">È possibile definire più applicazioni di inoltro in un singolo file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="01007-203">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="01007-204">In questa esercitazione ne viene tuttavia definita solo una.</span><span class="sxs-lookup"><span data-stu-id="01007-204">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="01007-205">All'interno di hello `<services>` elemento, aggiungere un `<service>` nome del servizio hello hello toodefine dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="01007-205">Within hello `<services>` element, add a `<service>` element toodefine hello name of hello service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="01007-206">All'interno di hello `<service>` elemento, definire il percorso di hello del contratto dell'endpoint hello e hello anche tipo di associazione per l'endpoint di hello.</span><span class="sxs-lookup"><span data-stu-id="01007-206">Within hello `<service>` element, define hello location of hello endpoint contract, and also hello type of binding for hello endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="01007-207">endpoint Hello definisce dove client hello cercherà un'applicazione hello host.</span><span class="sxs-lookup"><span data-stu-id="01007-207">hello endpoint defines where hello client will look for hello host application.</span></span> <span data-ttu-id="01007-208">In un secondo momento, esercitazione hello utilizza questo toocreate passaggio un URI che espone completamente host hello tramite inoltro di Azure.</span><span class="sxs-lookup"><span data-stu-id="01007-208">Later, hello tutorial uses this step toocreate a URI that fully exposes hello host through Azure Relay.</span></span> <span data-ttu-id="01007-209">associazione di Hello dichiara che si sta usando TCP come hello toocommunicate protocollo con il servizio di inoltro hello.</span><span class="sxs-lookup"><span data-stu-id="01007-209">hello binding declares that we are using TCP as hello protocol toocommunicate with hello relay service.</span></span>
7. <span data-ttu-id="01007-210">Da hello **compilare** menu, fare clic su **Compila soluzione** accuratezza hello tooconfirm del lavoro.</span><span class="sxs-lookup"><span data-stu-id="01007-210">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="01007-211">Esempio</span><span class="sxs-lookup"><span data-stu-id="01007-211">Example</span></span>

<span data-ttu-id="01007-212">Hello codice riportato di seguito viene illustrata hello implementazione del contratto di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="01007-212">hello following code shows hello implementation of hello service contract.</span></span>

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

<span data-ttu-id="01007-213">Hello codice riportato di seguito viene illustrato hello base formato del file app. config hello associato all'host del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="01007-213">hello following code shows hello basic format of hello App.config file associated with hello service host.</span></span>

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

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a><span data-ttu-id="01007-214">Ospitare ed eseguire un tooregister di servizio web di base con il servizio di inoltro hello</span><span class="sxs-lookup"><span data-stu-id="01007-214">Host and run a basic web service tooregister with hello relay service</span></span>

<span data-ttu-id="01007-215">Questo passaggio viene descritto come toorun un Azure inoltro servizio.</span><span class="sxs-lookup"><span data-stu-id="01007-215">This step describes how toorun an Azure Relay service.</span></span>

### <a name="create-hello-relay-credentials"></a><span data-ttu-id="01007-216">Creare le credenziali di inoltro di hello</span><span class="sxs-lookup"><span data-stu-id="01007-216">Create hello relay credentials</span></span>

1. <span data-ttu-id="01007-217">In `Main()`, creare due variabili nello spazio dei nomi di hello quali toostore e chiave di firma di accesso condiviso che vengono letti dalla finestra della console hello hello.</span><span class="sxs-lookup"><span data-stu-id="01007-217">In `Main()`, create two variables in which toostore hello namespace and hello SAS key that are read from hello console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="01007-218">chiave di firma di accesso condiviso Hello sarà usato tooaccess successive al progetto.</span><span class="sxs-lookup"><span data-stu-id="01007-218">hello SAS key will be used later tooaccess your project.</span></span> <span data-ttu-id="01007-219">spazio dei nomi Hello viene passato come parametro troppo`CreateServiceUri` toocreate un URI del servizio.</span><span class="sxs-lookup"><span data-stu-id="01007-219">hello namespace is passed as a parameter too`CreateServiceUri` toocreate a service URI.</span></span>
2. <span data-ttu-id="01007-220">Utilizzando un [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) di oggetti, dichiarare che si utilizzerà una chiave di firma di accesso condiviso come tipo di credenziale hello.</span><span class="sxs-lookup"><span data-stu-id="01007-220">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as hello credential type.</span></span> <span data-ttu-id="01007-221">Aggiungere hello seguente codice immediatamente dopo il codice hello aggiunto nell'ultimo passaggio hello.</span><span class="sxs-lookup"><span data-stu-id="01007-221">Add hello following code directly after hello code added in hello last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a><span data-ttu-id="01007-222">Creare un indirizzo di base per il servizio hello</span><span class="sxs-lookup"><span data-stu-id="01007-222">Create a base address for hello service</span></span>

<span data-ttu-id="01007-223">Dopo il codice hello aggiunto nell'ultimo passaggio hello, creare un `Uri` istanza per l'indirizzo di base hello del servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="01007-223">After hello code you added in hello last step, create a `Uri` instance for hello base address of hello service.</span></span> <span data-ttu-id="01007-224">Questo URI specifica lo schema di Service Bus hello, hello dello spazio dei nomi e il percorso di hello dell'interfaccia di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="01007-224">This URI specifies hello Service Bus scheme, hello namespace, and hello path of hello service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="01007-225">"sb" è un'abbreviazione per lo schema di Service Bus hello e indica che si sta usando TCP come protocollo di hello.</span><span class="sxs-lookup"><span data-stu-id="01007-225">"sb" is an abbreviation for hello Service Bus scheme, and indicates that we are using TCP as hello protocol.</span></span> <span data-ttu-id="01007-226">Questo è stato indicato anche in precedenza nel file di configurazione hello quando [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) come associazione hello è stato specificato.</span><span class="sxs-lookup"><span data-stu-id="01007-226">This was also previously indicated in hello configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as hello binding.</span></span>

<span data-ttu-id="01007-227">Per questa esercitazione, hello URI è `sb://putServiceNamespaceHere.windows.net/EchoService`.</span><span class="sxs-lookup"><span data-stu-id="01007-227">For this tutorial, hello URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="create-and-configure-hello-service-host"></a><span data-ttu-id="01007-228">Creare e configurare l'host del servizio hello</span><span class="sxs-lookup"><span data-stu-id="01007-228">Create and configure hello service host</span></span>

1. <span data-ttu-id="01007-229">Impostare la modalità di connettività hello troppo`AutoDetect`.</span><span class="sxs-lookup"><span data-stu-id="01007-229">Set hello connectivity mode too`AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="01007-230">modalità di connettività Hello descrive toocommunicate hello protocollo hello servizio viene utilizzato con il servizio di inoltro hello. HTTP o TCP.</span><span class="sxs-lookup"><span data-stu-id="01007-230">hello connectivity mode describes hello protocol hello service uses toocommunicate with hello relay service; either HTTP or TCP.</span></span> <span data-ttu-id="01007-231">Usa impostazione predefinita hello `AutoDetect`, servizio hello tenta tooconnect tooAzure inoltro su TCP se disponibile e HTTP se TCP non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="01007-231">Using hello default setting `AutoDetect`, hello service attempts tooconnect tooAzure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="01007-232">Si noti che questo comportamento è diverso dal servizio di hello protocollo hello specifica per la comunicazione client.</span><span class="sxs-lookup"><span data-stu-id="01007-232">Note that this differs from hello protocol hello service specifies for client communication.</span></span> <span data-ttu-id="01007-233">Tale protocollo è determinato dall'associazione hello utilizzata.</span><span class="sxs-lookup"><span data-stu-id="01007-233">That protocol is determined by hello binding used.</span></span> <span data-ttu-id="01007-234">Ad esempio, un servizio può utilizzare hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, che specifica che l'endpoint comunica con i client su HTTP.</span><span class="sxs-lookup"><span data-stu-id="01007-234">For example, a service can use hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="01007-235">Che è possibile specificare il servizio stesso **Connectivitymode** in modo che il servizio di hello comunica con Azure inoltro tramite TCP.</span><span class="sxs-lookup"><span data-stu-id="01007-235">That same service could specify **ConnectivityMode.AutoDetect** so that hello service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="01007-236">Creare l'host del servizio hello, tramite hello che URI creato in precedenza in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="01007-236">Create hello service host, using hello URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="01007-237">host del servizio Hello è oggetto WCF hello che crea un'istanza del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="01007-237">hello service host is hello WCF object that instantiates hello service.</span></span> <span data-ttu-id="01007-238">In questo caso, si passa il tipo di hello del servizio si desidera toocreate (un `EchoService` tipo) e anche l'indirizzo toohello in corrispondenza del quale si desidera che il servizio di hello tooexpose.</span><span class="sxs-lookup"><span data-stu-id="01007-238">Here, you pass it hello type of service you want toocreate (an `EchoService` type), and also toohello address at which you want tooexpose hello service.</span></span>
3. <span data-ttu-id="01007-239">Nella parte superiore di hello del file Program.cs hello, aggiungere i riferimenti troppo[ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) e [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span><span class="sxs-lookup"><span data-stu-id="01007-239">At hello top of hello Program.cs file, add references too[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="01007-240">In `Main()`, configurare l'accesso pubblico tooenable endpoint hello.</span><span class="sxs-lookup"><span data-stu-id="01007-240">Back in `Main()`, configure hello endpoint tooenable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="01007-241">Questo passaggio segnala al servizio di inoltro hello di che l'applicazione può essere trovata pubblicamente esaminando il feed ATOM hello per il progetto.</span><span class="sxs-lookup"><span data-stu-id="01007-241">This step informs hello relay service that your application can be found publicly by examining hello ATOM feed for your project.</span></span> <span data-ttu-id="01007-242">Se si imposta **DiscoveryType** troppo**privata**, un client sarà comunque servizio hello in grado di tooaccess.</span><span class="sxs-lookup"><span data-stu-id="01007-242">If you set **DiscoveryType** too**private**, a client would still be able tooaccess hello service.</span></span> <span data-ttu-id="01007-243">Tuttavia, il servizio di hello non sarebbe stato visualizzato durante la ricerca dello spazio dei nomi di inoltro hello.</span><span class="sxs-lookup"><span data-stu-id="01007-243">However, hello service would not appear when it searches hello Relay namespace.</span></span> <span data-ttu-id="01007-244">Invece, client hello avrebbe percorso dell'endpoint tooknow hello in anticipo.</span><span class="sxs-lookup"><span data-stu-id="01007-244">Instead, hello client would have tooknow hello endpoint path beforehand.</span></span>
5. <span data-ttu-id="01007-245">Applicare le credenziali del servizio di hello toohello gli endpoint del servizio definiti nel file app. config hello:</span><span class="sxs-lookup"><span data-stu-id="01007-245">Apply hello service credentials toohello service endpoints defined in hello App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="01007-246">Come indicato nel passaggio precedente hello, si potrebbero avere dichiarati più servizi ed endpoint nel file di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="01007-246">As stated in hello previous step, you could have declared multiple services and endpoints in hello configuration file.</span></span> <span data-ttu-id="01007-247">Se si dispone, questo codice scorrerebbe il file di configurazione di hello e ricerca per toowhich ogni endpoint è necessario applicare le credenziali.</span><span class="sxs-lookup"><span data-stu-id="01007-247">If you had, this code would traverse hello configuration file and search for every endpoint toowhich it should apply your credentials.</span></span> <span data-ttu-id="01007-248">Per questa esercitazione, tuttavia, i file di configurazione hello ha solo un endpoint.</span><span class="sxs-lookup"><span data-stu-id="01007-248">However, for this tutorial, hello configuration file has only one endpoint.</span></span>

### <a name="open-hello-service-host"></a><span data-ttu-id="01007-249">Host del servizio aprire hello</span><span class="sxs-lookup"><span data-stu-id="01007-249">Open hello service host</span></span>

1. <span data-ttu-id="01007-250">Aprire il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="01007-250">Open hello service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="01007-251">Informare l'utente hello hello servizio è in esecuzione e spiegare come tooshut servizio hello.</span><span class="sxs-lookup"><span data-stu-id="01007-251">Inform hello user that hello service is running, and explain how tooshut down hello service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="01007-252">Al termine, chiudere l'host del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="01007-252">When finished, close hello service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="01007-253">Premere **Ctrl + MAIUSC + B** progetto hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="01007-253">Press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="example"></a><span data-ttu-id="01007-254">Esempio</span><span class="sxs-lookup"><span data-stu-id="01007-254">Example</span></span>

<span data-ttu-id="01007-255">Il codice del servizio completato comparirà come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="01007-255">Your completed service code should appear as follows.</span></span> <span data-ttu-id="01007-256">codice Hello include il contratto di servizio hello e l'implementazione dai passaggi precedenti nell'esercitazione hello e host hello servizio in un'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="01007-256">hello code includes hello service contract and implementation from previous steps in hello tutorial, and hosts hello service in a console application.</span></span>

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

           // Create hello credentials object for hello endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create hello service URI based on hello service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create hello service host reading hello configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create hello ServiceRegistrySettings behavior for hello endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add hello Relay credentials tooall endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open hello service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            // Close hello service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-hello-service-contract"></a><span data-ttu-id="01007-257">Creare un client WCF per il contratto di servizio hello</span><span class="sxs-lookup"><span data-stu-id="01007-257">Create a WCF client for hello service contract</span></span>

<span data-ttu-id="01007-258">passaggio successivo Hello è un'applicazione client toocreate e definire il contratto di servizio hello implementerà nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="01007-258">hello next step is toocreate a client application and define hello service contract you will implement in later steps.</span></span> <span data-ttu-id="01007-259">Si noti che molti di questi passaggi sono simili a passaggi hello usare toocreate un servizio: la definizione di un contratto, la modifica di un file app. config file, usare un servizio di inoltro di credenziali tooconnect toohello e così via.</span><span class="sxs-lookup"><span data-stu-id="01007-259">Note that many of these steps resemble hello steps used toocreate a service: defining a contract, editing an App.config file, using credentials tooconnect toohello relay service, and so on.</span></span> <span data-ttu-id="01007-260">Nell'esempio hello hello procedura viene fornito codice di Hello utilizzato per queste attività.</span><span class="sxs-lookup"><span data-stu-id="01007-260">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="01007-261">Creare un nuovo progetto nella soluzione Visual Studio corrente hello per client hello eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="01007-261">Create a new project in hello current Visual Studio solution for hello client by doing hello following:</span></span>

   1. <span data-ttu-id="01007-262">In Esplora soluzioni in hello stessa soluzione che contiene il servizio di hello, fare doppio clic hello corrente soluzione (non il progetto hello) e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="01007-262">In Solution Explorer, in hello same solution that contains hello service, right-click hello current solution (not hello project), and click **Add**.</span></span> <span data-ttu-id="01007-263">Fare clic su **Nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="01007-263">Then click **New Project**.</span></span>
   2. <span data-ttu-id="01007-264">In hello **Aggiungi nuovo progetto** la finestra di dialogo, fare clic su **Visual c#** (se **Visual c#** non è visualizzato, cercarlo in **altri linguaggi**), selezionare hello **Applicazione console (.NET Framework)** , modello e denominarlo **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="01007-264">In hello **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select hello **Console App (.NET Framework)** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="01007-265">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="01007-265">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="01007-266">In Esplora soluzioni fare doppio clic sul file Program.cs hello in hello **EchoClient** progetto tooopen possa nell'editor di hello, se non è già aperta.</span><span class="sxs-lookup"><span data-stu-id="01007-266">In Solution Explorer, double-click hello Program.cs file in hello **EchoClient** project tooopen it in hello editor, if it is not already open.</span></span>
3. <span data-ttu-id="01007-267">Spazio dei nomi hello Modifica nome predefinito di `EchoClient` troppo`Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="01007-267">Change hello namespace name from its default name of `EchoClient` too`Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="01007-268">Installare hello [pacchetto NuGet di Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Esplora soluzioni fare doppio clic su hello **EchoClient** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="01007-268">Install hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click hello **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="01007-269">Fare clic su hello **Sfoglia** tab, quindi cercare `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="01007-269">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="01007-270">Fare clic su **installare**e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="01007-270">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="01007-271">Aggiungere un `using` istruzione per hello [System. ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) dello spazio dei nomi nel file Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="01007-271">Add a `using` statement for hello [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in hello Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="01007-272">Aggiungere hello contratto definizione toohello spazio dei nomi servizio, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="01007-272">Add hello service contract definition toohello namespace, as shown in hello following example.</span></span> <span data-ttu-id="01007-273">Si noti che questa definizione è identica toohello definizione hello **servizio** progetto.</span><span class="sxs-lookup"><span data-stu-id="01007-273">Note that this definition is identical toohello definition used in hello **Service** project.</span></span> <span data-ttu-id="01007-274">È necessario aggiungere il codice nella parte superiore di hello di hello `Microsoft.ServiceBus.Samples` dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="01007-274">You should add this code at hello top of hello `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="01007-275">Premere **Ctrl + MAIUSC + B** client hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="01007-275">Press **Ctrl+Shift+B** toobuild hello client.</span></span>

### <a name="example"></a><span data-ttu-id="01007-276">Esempio</span><span class="sxs-lookup"><span data-stu-id="01007-276">Example</span></span>

<span data-ttu-id="01007-277">Hello codice seguente viene illustrato lo stato corrente di hello del file Program.cs hello in hello **EchoClient** progetto.</span><span class="sxs-lookup"><span data-stu-id="01007-277">hello following code shows hello current status of hello Program.cs file in hello **EchoClient** project.</span></span>

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

## <a name="configure-hello-wcf-client"></a><span data-ttu-id="01007-278">Configurare il client WCF hello</span><span class="sxs-lookup"><span data-stu-id="01007-278">Configure hello WCF client</span></span>

<span data-ttu-id="01007-279">In questo passaggio si crea un file app. config per un'applicazione client di base che accede al servizio hello creato in precedenza in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="01007-279">In this step, you create an App.config file for a basic client application that accesses hello service created previously in this tutorial.</span></span> <span data-ttu-id="01007-280">Questo file app. config definisce il contratto di hello, associazione e nome dell'endpoint hello.</span><span class="sxs-lookup"><span data-stu-id="01007-280">This App.config file defines hello contract, binding, and name of hello endpoint.</span></span> <span data-ttu-id="01007-281">Nell'esempio hello hello procedura viene fornito codice di Hello utilizzato per queste attività.</span><span class="sxs-lookup"><span data-stu-id="01007-281">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="01007-282">In Esplora soluzioni, in hello **EchoClient** progetto, fare doppio clic su **app** file hello tooopen nell'editor di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="01007-282">In Solution Explorer, in hello **EchoClient** project, double-click **App.config** tooopen hello file in hello Visual Studio editor.</span></span>
2. <span data-ttu-id="01007-283">In hello `<appSettings>` elemento, sostituire i segnaposto hello con nome hello dello spazio dei nomi di servizio e hello chiave di firma di accesso condiviso che è stato copiato in un passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="01007-283">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="01007-284">Nell'elemento System. ServiceModel hello, aggiungere un `<client>` elemento.</span><span class="sxs-lookup"><span data-stu-id="01007-284">Within hello system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="01007-285">Questo passaggio dichiara che si sta definendo un'applicazione client di tipo WCF.</span><span class="sxs-lookup"><span data-stu-id="01007-285">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="01007-286">All'interno di hello `client` elemento, definire il nome di hello, contratto e il tipo di associazione per l'endpoint di hello.</span><span class="sxs-lookup"><span data-stu-id="01007-286">Within hello `client` element, define hello name, contract, and binding type for hello endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="01007-287">Questo passaggio definisce il nome di hello dell'endpoint hello contratto hello definito nel servizio hello e dei fatti hello che un'applicazione hello client utilizza toocommunicate TCP con l'inoltro di Azure.</span><span class="sxs-lookup"><span data-stu-id="01007-287">This step defines hello name of hello endpoint, hello contract defined in hello service, and hello fact that hello client application uses TCP toocommunicate with Azure Relay.</span></span> <span data-ttu-id="01007-288">Hello nome dell'endpoint viene usato in hello passaggio successivo toolink questa configurazione endpoint con l'URI del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="01007-288">hello endpoint name is used in hello next step toolink this endpoint configuration with hello service URI.</span></span>
5. <span data-ttu-id="01007-289">Fare clic su **File** quindi su **Salva tutto**.</span><span class="sxs-lookup"><span data-stu-id="01007-289">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="01007-290">Esempio</span><span class="sxs-lookup"><span data-stu-id="01007-290">Example</span></span>

<span data-ttu-id="01007-291">Hello codice seguente viene illustrato il file app. config hello per client Echo hello.</span><span class="sxs-lookup"><span data-stu-id="01007-291">hello following code shows hello App.config file for hello Echo client.</span></span>

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

## <a name="implement-hello-wcf-client"></a><span data-ttu-id="01007-292">Client WCF di implementare hello</span><span class="sxs-lookup"><span data-stu-id="01007-292">Implement hello WCF client</span></span>
<span data-ttu-id="01007-293">In questo passaggio è implementare un'applicazione client di base che accede al servizio hello creato in precedenza in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="01007-293">In this step, you implement a basic client application that accesses hello service you created previously in this tutorial.</span></span> <span data-ttu-id="01007-294">Servizio toohello simile, hello client esegue molte delle hello stesso operazioni tooaccess inoltro di Azure:</span><span class="sxs-lookup"><span data-stu-id="01007-294">Similar toohello service, hello client performs many of hello same operations tooaccess Azure Relay:</span></span>

1. <span data-ttu-id="01007-295">Imposta la modalità di connettività hello.</span><span class="sxs-lookup"><span data-stu-id="01007-295">Sets hello connectivity mode.</span></span>
2. <span data-ttu-id="01007-296">Crea hello URI che individua il servizio host hello.</span><span class="sxs-lookup"><span data-stu-id="01007-296">Creates hello URI that locates hello host service.</span></span>
3. <span data-ttu-id="01007-297">Definisce le credenziali di sicurezza hello.</span><span class="sxs-lookup"><span data-stu-id="01007-297">Defines hello security credentials.</span></span>
4. <span data-ttu-id="01007-298">Si applica hello credenziali toohello connessione.</span><span class="sxs-lookup"><span data-stu-id="01007-298">Applies hello credentials toohello connection.</span></span>
5. <span data-ttu-id="01007-299">Apre connessione hello.</span><span class="sxs-lookup"><span data-stu-id="01007-299">Opens hello connection.</span></span>
6. <span data-ttu-id="01007-300">Esegue attività specifiche dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="01007-300">Performs hello application-specific tasks.</span></span>
7. <span data-ttu-id="01007-301">Chiude la connessione hello.</span><span class="sxs-lookup"><span data-stu-id="01007-301">Closes hello connection.</span></span>

<span data-ttu-id="01007-302">Tuttavia, una delle principali differenze hello è che un'applicazione hello client utilizza un servizio di inoltro toohello tooconnect di canale, mentre il servizio hello utilizza una chiamata troppo**ServiceHost**.</span><span class="sxs-lookup"><span data-stu-id="01007-302">However, one of hello main differences is that hello client application uses a channel tooconnect toohello relay service, whereas hello service uses a call too**ServiceHost**.</span></span> <span data-ttu-id="01007-303">Nell'esempio hello hello procedura viene fornito codice di Hello utilizzato per queste attività.</span><span class="sxs-lookup"><span data-stu-id="01007-303">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

### <a name="implement-a-client-application"></a><span data-ttu-id="01007-304">Implementare un'applicazione client</span><span class="sxs-lookup"><span data-stu-id="01007-304">Implement a client application</span></span>
1. <span data-ttu-id="01007-305">Impostare la modalità di connettività hello troppo**AutoDetect**.</span><span class="sxs-lookup"><span data-stu-id="01007-305">Set hello connectivity mode too**AutoDetect**.</span></span> <span data-ttu-id="01007-306">Aggiungere hello seguente codice all'interno di hello `Main()` metodo hello **EchoClient** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="01007-306">Add hello following code inside hello `Main()` method of hello **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="01007-307">Definire toohold hello i valori delle variabili per spazio dei nomi servizio hello e la chiave di firma di accesso condiviso che vengono letti dalla console hello.</span><span class="sxs-lookup"><span data-stu-id="01007-307">Define variables toohold hello values for hello service namespace, and SAS key that are read from hello console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="01007-308">Creare hello URI che definisce il percorso di hello dell'host hello nel progetto di inoltro.</span><span class="sxs-lookup"><span data-stu-id="01007-308">Create hello URI that defines hello location of hello host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="01007-309">Creare l'oggetto credenziale hello per l'endpoint dello spazio dei nomi del servizio.</span><span class="sxs-lookup"><span data-stu-id="01007-309">Create hello credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="01007-310">Creare hello channel factory che carica la configurazione di hello descritte nel file app. config hello.</span><span class="sxs-lookup"><span data-stu-id="01007-310">Create hello channel factory that loads hello configuration described in hello App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="01007-311">Una channel factory è un oggetto WCF che crea un canale attraverso il quale comunicano hello servizi e applicazioni client.</span><span class="sxs-lookup"><span data-stu-id="01007-311">A channel factory is a WCF object that creates a channel through which hello service and client applications communicate.</span></span>
6. <span data-ttu-id="01007-312">Applicare le credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="01007-312">Apply hello credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="01007-313">Creare e aprire il canale toohello servizio hello.</span><span class="sxs-lookup"><span data-stu-id="01007-313">Create and open hello channel toohello service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="01007-314">Scrivere l'interfaccia utente di base hello e funzionalità per echo hello.</span><span class="sxs-lookup"><span data-stu-id="01007-314">Write hello basic user interface and functionality for hello echo.</span></span>

    ```csharp
    Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
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

    <span data-ttu-id="01007-315">Si noti che il codice hello utilizza istanza hello oggetto channel hello come proxy per il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="01007-315">Note that hello code uses hello instance of hello channel object as a proxy for hello service.</span></span>
9. <span data-ttu-id="01007-316">Chiudere il canale hello e factory hello Chiudi.</span><span class="sxs-lookup"><span data-stu-id="01007-316">Close hello channel, and close hello factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a><span data-ttu-id="01007-317">Esempio</span><span class="sxs-lookup"><span data-stu-id="01007-317">Example</span></span>

<span data-ttu-id="01007-318">Il codice completato compariranno come indicato di seguito, che mostra come toocreate un'applicazione client, come toocall hello operazioni del servizio hello e come tooclose hello client dopo un'operazione di hello chiama viene completato.</span><span class="sxs-lookup"><span data-stu-id="01007-318">Your completed code should appear as follows, showing how toocreate a client application, how toocall hello operations of hello service, and how tooclose hello client after hello operation call is finished.</span></span>

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

            Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
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

## <a name="run-hello-applications"></a><span data-ttu-id="01007-319">Eseguire applicazioni hello</span><span class="sxs-lookup"><span data-stu-id="01007-319">Run hello applications</span></span>

1. <span data-ttu-id="01007-320">Premere **Ctrl + MAIUSC + B** soluzione hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="01007-320">Press **Ctrl+Shift+B** toobuild hello solution.</span></span> <span data-ttu-id="01007-321">Verranno compilati il progetto di client hello sia progetto servizio hello creato nei passaggi precedenti hello.</span><span class="sxs-lookup"><span data-stu-id="01007-321">This builds both hello client project and hello service project that you created in hello previous steps.</span></span>
2. <span data-ttu-id="01007-322">Prima dell'applicazione client hello in esecuzione, è necessario assicurarsi che un'applicazione hello servizio sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="01007-322">Before running hello client application, you must make sure that hello service application is running.</span></span> <span data-ttu-id="01007-323">In Esplora soluzioni in Visual Studio, fare doppio clic su hello **EchoService** soluzione, quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="01007-323">In Solution Explorer in Visual Studio, right-click hello **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="01007-324">Nella finestra proprietà di hello soluzione, fare clic su **progetto di avvio**, quindi fare clic su hello **più progetti di avvio** pulsante.</span><span class="sxs-lookup"><span data-stu-id="01007-324">In hello solution properties dialog box, click **Startup Project**, then click hello **Multiple startup projects** button.</span></span> <span data-ttu-id="01007-325">Assicurarsi che **EchoService** visualizzata per prima nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="01007-325">Make sure **EchoService** appears first in hello list.</span></span>
4. <span data-ttu-id="01007-326">Set hello **azione** casella per entrambi hello **EchoService** e **EchoClient** progetti troppo**avviare**.</span><span class="sxs-lookup"><span data-stu-id="01007-326">Set hello **Action** box for both hello **EchoService** and **EchoClient** projects too**Start**.</span></span>

    ![][5]
5. <span data-ttu-id="01007-327">Fare clic su **Dipendenze progetto**.</span><span class="sxs-lookup"><span data-stu-id="01007-327">Click **Project Dependencies**.</span></span> <span data-ttu-id="01007-328">In hello **progetti** , quindi selezionare **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="01007-328">In hello **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="01007-329">In hello **dipende** verificare **EchoService** è selezionata.</span><span class="sxs-lookup"><span data-stu-id="01007-329">In hello **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="01007-330">Fare clic su **OK** toodismiss hello **proprietà** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="01007-330">Click **OK** toodismiss hello **Properties** dialog.</span></span>
7. <span data-ttu-id="01007-331">Premere **F5** toorun entrambi i progetti.</span><span class="sxs-lookup"><span data-stu-id="01007-331">Press **F5** toorun both projects.</span></span>
8. <span data-ttu-id="01007-332">Richiesto per il nome dello spazio dei nomi hello in entrambe le finestre della console della finestra.</span><span class="sxs-lookup"><span data-stu-id="01007-332">Both console windows open and prompt you for hello namespace name.</span></span> <span data-ttu-id="01007-333">Hello servizio deve essere eseguito in primo luogo, in hello **EchoService** finestra della console, immettere lo spazio dei nomi hello e quindi premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="01007-333">hello service must run first, so in hello **EchoService** console window, enter hello namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="01007-334">Verrà quindi chiesto di specificare la chiave di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="01007-334">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="01007-335">Immettere una chiave SAS hello e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="01007-335">Enter hello SAS key and press ENTER.</span></span>

    <span data-ttu-id="01007-336">Di seguito è riportato l'output dalla finestra di console hello.</span><span class="sxs-lookup"><span data-stu-id="01007-336">Here is example output from hello console window.</span></span> <span data-ttu-id="01007-337">Si noti che i valori hello fornito di seguito sono ad esempio a solo scopo.</span><span class="sxs-lookup"><span data-stu-id="01007-337">Note that hello values provided here are for example purposes only.</span></span>

    <span data-ttu-id="01007-338">`Your Service Namespace: myNamespace``Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="01007-338">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="01007-339">applicazione di servizio Hello stampa indirizzo hello finestra console toohello su cui è in ascolto, come illustrato nel seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="01007-339">hello service application prints toohello console window hello address on which it's listening, as seen in hello following example.</span></span>

    <span data-ttu-id="01007-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/``Press [Enter] tooexit`</span><span class="sxs-lookup"><span data-stu-id="01007-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`</span></span>
10. <span data-ttu-id="01007-341">In hello **EchoClient** finestra della console, immettere hello corrispondono a quelle immesse in precedenza per l'applicazione di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="01007-341">In hello **EchoClient** console window, enter hello same information that you entered previously for hello service application.</span></span> <span data-ttu-id="01007-342">Seguire hello tooenter passaggi precedenti di hello stesso spazio dei nomi servizio e SAS valori per un'applicazione client hello di chiave.</span><span class="sxs-lookup"><span data-stu-id="01007-342">Follow hello previous steps tooenter hello same service namespace and SAS key values for hello client application.</span></span>
11. <span data-ttu-id="01007-343">Dopo aver immesso questi valori, client hello apre un servizio toohello di canale e richiede tooenter è testo, come illustrato nel seguente esempio di output di console hello.</span><span class="sxs-lookup"><span data-stu-id="01007-343">After entering these values, hello client opens a channel toohello service and prompts you tooenter some text as seen in hello following console output example.</span></span>

    `Enter text tooecho (or [Enter] tooexit):`

    <span data-ttu-id="01007-344">Immettere un'applicazione di servizio toohello toosend testo e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="01007-344">Enter some text toosend toohello service application and press Enter.</span></span> <span data-ttu-id="01007-345">Questo testo viene inviato toohello servizio tramite l'operazione del servizio Echo hello e viene visualizzato nella finestra della console hello servizio come illustrato di seguito l'output di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="01007-345">This text is sent toohello service through hello Echo service operation and appears in hello service console window as in hello following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="01007-346">un'applicazione Hello client riceve il valore restituito di hello di hello `Echo` operazione, che è il testo originale hello e stampato tooits finestra della console.</span><span class="sxs-lookup"><span data-stu-id="01007-346">hello client application receives hello return value of hello `Echo` operation, which is hello original text, and prints it tooits console window.</span></span> <span data-ttu-id="01007-347">esempio Hello è riportato l'output dalla finestra di console client hello.</span><span class="sxs-lookup"><span data-stu-id="01007-347">hello following is example output from hello client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="01007-348">È possibile continuare a inviare messaggi di testo dal servizio di toohello hello client in questo modo.</span><span class="sxs-lookup"><span data-stu-id="01007-348">You can continue sending text messages from hello client toohello service in this manner.</span></span> <span data-ttu-id="01007-349">Al termine, premere INVIO in hello tooend windows console client e servizio entrambe le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="01007-349">When you are finished, press Enter in hello client and service console windows tooend both applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01007-350">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="01007-350">Next steps</span></span>

<span data-ttu-id="01007-351">In questa esercitazione è stato illustrato come toobuild un'applicazione client di inoltro di Azure e un servizio usando hello funzionalità di inoltro WCF del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="01007-351">This tutorial showed how toobuild an Azure Relay client application and service using hello WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="01007-352">Per un'esercitazione simile che usa la [messaggistica](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging) del bus di servizio, vedere [Introduzione alle code del bus di servizio](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="01007-352">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="01007-353">toolearn ulteriori informazioni sull'inoltro di Azure, vedere i seguenti argomenti hello.</span><span class="sxs-lookup"><span data-stu-id="01007-353">toolearn more about Azure Relay, see hello following topics.</span></span>

* [<span data-ttu-id="01007-354">Panoramica dell'architettura del bus di servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="01007-354">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="01007-355">Panoramica del servizio di inoltro di Azure</span><span class="sxs-lookup"><span data-stu-id="01007-355">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="01007-356">Come servizio con .NET di inoltro toouse hello WCF</span><span class="sxs-lookup"><span data-stu-id="01007-356">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
