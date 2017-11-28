---
title: applicazione in locale/cloud ibrida di inoltro WCF (.NET) aaaAzure | Documenti Microsoft
description: Informazioni su come applicazione ibrida toocreate un .NET in locale/cloud tramite Azure un inoltro WCF.
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9ed02f7c-ebfb-4f39-9c97-b7dc15bcb4c1
ms.service: service-bus-relay
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: sethm
ms.openlocfilehash: aab8b1dbdc85c4edf7b0ccef0921b69524b2d306
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a><span data-ttu-id="bb953-103">Applicazione ibrida cloud/locale (.NET) usando il servizio d'inoltro WCF di Azure</span><span class="sxs-lookup"><span data-stu-id="bb953-103">.NET on-premises/cloud hybrid application using Azure WCF Relay</span></span>
## <a name="introduction"></a><span data-ttu-id="bb953-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="bb953-104">Introduction</span></span>

<span data-ttu-id="bb953-105">Questo articolo illustra come toobuild ibrido cloud applicazione con Microsoft Azure e Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb953-105">This article shows how toobuild a hybrid cloud application with Microsoft Azure and Visual Studio.</span></span> <span data-ttu-id="bb953-106">esercitazione Hello presuppone che si ha alcuna esperienza precedente con Azure.</span><span class="sxs-lookup"><span data-stu-id="bb953-106">hello tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="bb953-107">In meno di 30 minuti, si disporrà di un'applicazione che utilizza più risorse di Azure backup e in esecuzione nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-107">In less than 30 minutes, you will have an application that uses multiple Azure resources up and running in hello cloud.</span></span>

<span data-ttu-id="bb953-108">Si acquisiranno le nozioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb953-108">You will learn:</span></span>

* <span data-ttu-id="bb953-109">Come toocreate o adattare un servizio web esistente per l'utilizzo da una soluzione web.</span><span class="sxs-lookup"><span data-stu-id="bb953-109">How toocreate or adapt an existing web service for consumption by a web solution.</span></span>
* <span data-ttu-id="bb953-110">Come dati toouse hello Azure WCF Relay service tooshare tra un'applicazione Azure e un servizio web ospitato in un' posizione.</span><span class="sxs-lookup"><span data-stu-id="bb953-110">How toouse hello Azure WCF Relay service tooshare data between an Azure application and a web service hosted elsewhere.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a><span data-ttu-id="bb953-111">Vantaggi del servizio d'inoltro di Azure con soluzioni ibride</span><span class="sxs-lookup"><span data-stu-id="bb953-111">How Azure Relay helps with hybrid solutions</span></span>

<span data-ttu-id="bb953-112">Soluzioni di business sono in genere costituite da una combinazione di codice personalizzato scritto tootackle nuovo e requisiti aziendali e le funzionalità esistenti fornito da soluzioni e i sistemi che sono già presenti.</span><span class="sxs-lookup"><span data-stu-id="bb953-112">Business solutions are typically composed of a combination of custom code written tootackle new and unique business requirements and existing functionality provided by solutions and systems that are already in place.</span></span>

<span data-ttu-id="bb953-113">Architetti di soluzioni cloud hello toouse per una gestione più semplice di requisiti di scalabilità e ridurre i costi operativi sono in avvio.</span><span class="sxs-lookup"><span data-stu-id="bb953-113">Solution architects are starting toouse hello cloud for easier handling of scale requirements and lower operational costs.</span></span> <span data-ttu-id="bb953-114">In questo modo, individuano che le risorse di servizio che preferiscono tooleverage come blocchi predefiniti per le relative soluzioni sono all'interno di firewall aziendale hello e all'esterno di facile raggiungono per l'accesso dalla soluzione di cloud hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-114">In doing so, they find that existing service assets they'd like tooleverage as building blocks for their solutions are inside hello corporate firewall and out of easy reach for access by hello cloud solution.</span></span> <span data-ttu-id="bb953-115">Molti servizi interni non vengono compilati o ospitati in modo che essi possono essere facilmente esposti perimetrale alla rete aziendale hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-115">Many internal services are not built or hosted in a way that they can be easily exposed at hello corporate network edge.</span></span>

<span data-ttu-id="bb953-116">[Inoltro Azure](https://azure.microsoft.com/services/service-bus/) è progettato per hello caso d'uso di servizi web di Windows Communication Foundation (WCF) esistente e rendere tali servizi in modo sicuro accessibile toosolutions che risiedono all'esterno di perimetrale aziendale hello senza infrastruttura della rete aziendale toohello modifiche intrusiva.</span><span class="sxs-lookup"><span data-stu-id="bb953-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is designed for hello use-case of taking existing Windows Communication Foundation (WCF) web services and making those services securely accessible toosolutions that reside outside hello corporate perimeter without requiring intrusive changes toohello corporate network infrastructure.</span></span> <span data-ttu-id="bb953-117">Tali servizi di inoltro sono ospitate all'interno all'ambiente esistente, ma viene delegato in attesa di servizio in arrivo sessioni e richieste toohello inoltro ospitato su cloud.</span><span class="sxs-lookup"><span data-stu-id="bb953-117">Such relay services are still hosted inside their existing environment, but they delegate listening for incoming sessions and requests toohello cloud-hosted relay service.</span></span> <span data-ttu-id="bb953-118">Il servizio d'inoltro di Azure protegge anche quei servizi dall'accesso non autorizzato tramite l'autenticazione con [firma di accesso condiviso](../service-bus-messaging/service-bus-sas.md).</span><span class="sxs-lookup"><span data-stu-id="bb953-118">Azure Relay also protects those services from unauthorized access by using [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) authentication.</span></span>

## <a name="solution-scenario"></a><span data-ttu-id="bb953-119">Scenario della soluzione</span><span class="sxs-lookup"><span data-stu-id="bb953-119">Solution scenario</span></span>
<span data-ttu-id="bb953-120">In questa esercitazione si creerà un sito Web ASP.NET che consente di toosee un elenco di prodotti nella pagina di inventario del prodotto hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-120">In this tutorial, you will create an ASP.NET website that enables you toosee a list of products on hello product inventory page.</span></span>

![][0]

<span data-ttu-id="bb953-121">esercitazione Hello presuppone che si dispone di informazioni sui prodotti in un sistema locale esistente e che utilizza Azure inoltro tooreach in tale sistema.</span><span class="sxs-lookup"><span data-stu-id="bb953-121">hello tutorial assumes that you have product information in an existing on-premises system, and uses Azure Relay tooreach into that system.</span></span> <span data-ttu-id="bb953-122">Tale operazione viene simulata da un servizio Web eseguito in una semplice applicazione console ed è supportata da un insieme di prodotti in memoria.</span><span class="sxs-lookup"><span data-stu-id="bb953-122">This is simulated by a web service that runs in a simple console application and is backed by an in-memory set of products.</span></span> <span data-ttu-id="bb953-123">Si verrà toorun in grado di questa applicazione console nel proprio computer e la distribuzione di ruolo web hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="bb953-123">You will be able toorun this console application on your own computer and deploy hello web role into Azure.</span></span> <span data-ttu-id="bb953-124">In questo modo, si noterà come ruolo web hello in esecuzione in Data Center di Azure hello verrà effettivamente chiamato nel computer, anche se il computer verrà quasi certamente sono protetti da almeno un firewall e un livello di translation (NAT) indirizzo di rete.</span><span class="sxs-lookup"><span data-stu-id="bb953-124">By doing so, you will see how hello web role running in hello Azure datacenter will indeed call into your computer, even though your computer will almost certainly reside behind at least one firewall and a network address translation (NAT) layer.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="bb953-125">Configurare un ambiente di sviluppo hello</span><span class="sxs-lookup"><span data-stu-id="bb953-125">Set up hello development environment</span></span>

<span data-ttu-id="bb953-126">Prima di iniziare lo sviluppo di applicazioni Azure, scaricare gli strumenti di hello e configurare l'ambiente di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="bb953-126">Before you can begin developing Azure applications, download hello tools and set up your development environment:</span></span>

1. <span data-ttu-id="bb953-127">Installare hello Azure SDK per .NET da hello SDK [pagina di download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bb953-127">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="bb953-128">In hello **.NET** colonna, fare clic sulla versione di hello di [Visual Studio](http://www.visualstudio.com) in uso.</span><span class="sxs-lookup"><span data-stu-id="bb953-128">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="bb953-129">Hello i passaggi in questa esercitazione usare Visual Studio 2015, ma funzionano anche con Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="bb953-129">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="bb953-130">Quando viene chiesto di toorun o salvare installer hello, fare clic su **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="bb953-130">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="bb953-131">In hello **installazione guidata piattaforma Web**, fare clic su **installare** e continuare l'installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-131">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="bb953-132">Al termine dell'installazione di hello, sarà necessario tutto il necessario toostart toodevelop hello app.</span><span class="sxs-lookup"><span data-stu-id="bb953-132">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="bb953-133">Hello SDK include strumenti che consentono di sviluppare facilmente applicazioni Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb953-133">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="bb953-134">Creare uno spazio dei nomi</span><span class="sxs-lookup"><span data-stu-id="bb953-134">Create a namespace</span></span>

<span data-ttu-id="bb953-135">utilizzando toobegin hello le funzionalità di inoltro in Azure, è innanzitutto necessario creare uno spazio dei nomi del servizio.</span><span class="sxs-lookup"><span data-stu-id="bb953-135">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="bb953-136">Uno spazio dei nomi funge da contenitore di ambito in cui indirizzare le risorse di Azure nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bb953-136">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="bb953-137">Seguire hello [le istruzioni qui](relay-create-namespace-portal.md) toocreate uno spazio dei nomi di inoltro.</span><span class="sxs-lookup"><span data-stu-id="bb953-137">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="create-an-on-premises-server"></a><span data-ttu-id="bb953-138">Creare un server locale</span><span class="sxs-lookup"><span data-stu-id="bb953-138">Create an on-premises server</span></span>

<span data-ttu-id="bb953-139">In primo luogo, si creerà un sistema di catalogo prodotti locale fittizio.</span><span class="sxs-lookup"><span data-stu-id="bb953-139">First, you will build a (mock) on-premises product catalog system.</span></span> <span data-ttu-id="bb953-140">Sarà piuttosto semplice. si noterà come rappresenta un sistema di catalogo locale effettivo del prodotto con una superficie completa del servizio che si sta tentando di toointegrate.</span><span class="sxs-lookup"><span data-stu-id="bb953-140">It will be fairly simple; you can see this as representing an actual on-premises product catalog system with a complete service surface that we're trying toointegrate.</span></span>

<span data-ttu-id="bb953-141">Questo progetto è un'applicazione console Visual Studio e utilizza hello [pacchetto NuGet di Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello le librerie del Bus di servizio e le impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="bb953-141">This project is a Visual Studio console application, and uses hello [Azure Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello Service Bus libraries and configuration settings.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="bb953-142">Creare il progetto hello</span><span class="sxs-lookup"><span data-stu-id="bb953-142">Create hello project</span></span>

1. <span data-ttu-id="bb953-143">Usando privilegi di amministratore, avviare Microsoft Visual.</span><span class="sxs-lookup"><span data-stu-id="bb953-143">Using administrator privileges, start Microsoft Visual Studio.</span></span> <span data-ttu-id="bb953-144">In tal caso, fare doppio clic sull'icona di programma Visual Studio hello toodo e quindi fare clic su **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="bb953-144">toodo so, right-click hello Visual Studio program icon, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="bb953-145">In Visual Studio, su hello **File** menu, fare clic su **New**, quindi fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="bb953-145">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="bb953-146">Da **Modelli installati** in **Visual C#** fare clic su **App console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="bb953-146">From **Installed Templates**, under **Visual C#**, click **Console App (.NET Framework)**.</span></span> <span data-ttu-id="bb953-147">In hello **nome** casella, il nome del tipo hello **ProductsServer**:</span><span class="sxs-lookup"><span data-stu-id="bb953-147">In hello **Name** box, type hello name **ProductsServer**:</span></span>

   ![][11]
4. <span data-ttu-id="bb953-148">Fare clic su **OK** toocreate hello **ProductsServer** progetto.</span><span class="sxs-lookup"><span data-stu-id="bb953-148">Click **OK** toocreate hello **ProductsServer** project.</span></span>
5. <span data-ttu-id="bb953-149">Se Gestione di pacchetti hello NuGet per Visual Studio è già stato installato, ignorare toohello successivo.</span><span class="sxs-lookup"><span data-stu-id="bb953-149">If you have already installed hello NuGet package manager for Visual Studio, skip toohello next step.</span></span> <span data-ttu-id="bb953-150">In caso contrario, visitare il sito [NuGet][NuGet] e fare clic su [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) (Installa NuGet).</span><span class="sxs-lookup"><span data-stu-id="bb953-150">Otherwise, visit [NuGet][NuGet] and click [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span></span> <span data-ttu-id="bb953-151">Seguire hello richieste tooinstall hello di gestione pacchetti NuGet, quindi riavviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb953-151">Follow hello prompts tooinstall hello NuGet package manager, then re-start Visual Studio.</span></span>
6. <span data-ttu-id="bb953-152">In Esplora soluzioni fare doppio clic su hello **ProductsServer** del progetto, quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="bb953-152">In Solution Explorer, right-click hello **ProductsServer** project, then click **Manage NuGet Packages**.</span></span>
7. <span data-ttu-id="bb953-153">Fare clic su hello **Sfoglia** tab, quindi cercare `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="bb953-153">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="bb953-154">Seleziona hello **Windowsazure** pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bb953-154">Select hello **WindowsAzure.ServiceBus** package.</span></span>
8. <span data-ttu-id="bb953-155">Fare clic su **installare**e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="bb953-155">Click **Install**, and accept hello terms of use.</span></span>

   ![][13]

   <span data-ttu-id="bb953-156">Si noti che hello necessari assembly client fa riferimento a questo punto.</span><span class="sxs-lookup"><span data-stu-id="bb953-156">Note that hello required client assemblies are now referenced.</span></span>
8. <span data-ttu-id="bb953-157">Aggiungere una nuova classe per il contratto dei prodotti.</span><span class="sxs-lookup"><span data-stu-id="bb953-157">Add a new class for your product contract.</span></span> <span data-ttu-id="bb953-158">In Esplora soluzioni fare doppio clic su hello **ProductsServer** sul progetto e scegliere **Aggiungi**, quindi fare clic su **classe**.</span><span class="sxs-lookup"><span data-stu-id="bb953-158">In Solution Explorer, right-click hello **ProductsServer** project and click **Add**, and then click **Class**.</span></span>
9. <span data-ttu-id="bb953-159">In hello **nome** casella, il nome del tipo hello **ProductsContract.cs**.</span><span class="sxs-lookup"><span data-stu-id="bb953-159">In hello **Name** box, type hello name **ProductsContract.cs**.</span></span> <span data-ttu-id="bb953-160">Fare quindi clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="bb953-160">Then click **Add**.</span></span>
10. <span data-ttu-id="bb953-161">In **ProductsContract.cs**, sostituire definizione dello spazio dei nomi di hello con hello seguente di codice, che definisce il contratto di hello del servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-161">In **ProductsContract.cs**, replace hello namespace definition with hello following code, which defines hello contract for hello service.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define hello data contract for hello service
        [DataContract]
        // Declare hello serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define hello service contract.
        [ServiceContract]
        interface IProducts
        {
            [OperationContract]
            IList<ProductData> GetProducts();

        }

        interface IProductsChannel : IProducts, IClientChannel
        {
        }
    }
    ```
11. <span data-ttu-id="bb953-162">In Program.cs, sostituire hello seguente di codice che aggiunge il servizio di profilo hello e l'host di hello per tale definizione dello spazio dei nomi hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-162">In Program.cs, replace hello namespace definition with hello following code, which adds hello profile service and hello host for it.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement hello IProducts interface.
        class ProductsService : IProducts
        {

            // Populate array of products for display on website
            ProductData[] products =
                new []
                    {
                        new ProductData{ Id = "1", Name = "Rock",
                                         Quantity = "1"},
                        new ProductData{ Id = "2", Name = "Paper",
                                         Quantity = "3"},
                        new ProductData{ Id = "3", Name = "Scissors",
                                         Quantity = "5"},
                        new ProductData{ Id = "4", Name = "Well",
                                         Quantity = "2500"},
                    };

            // Display a message in hello service console application
            // when hello list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define hello Main() function in hello service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER tooclose");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. <span data-ttu-id="bb953-163">In Esplora soluzioni fare doppio clic su hello **app** tooopen del file nell'editor di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-163">In Solution Explorer, double-click hello **App.config** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="bb953-164">Nella parte inferiore di hello di hello `<system.ServiceModel>` elemento (ma si trovano all'interno `<system.ServiceModel>`), aggiungere hello seguente codice XML.</span><span class="sxs-lookup"><span data-stu-id="bb953-164">At hello bottom of hello `<system.ServiceModel>` element (but still within `<system.ServiceModel>`), add hello following XML code.</span></span> <span data-ttu-id="bb953-165">Tooreplace assicurarsi di essere *yourServiceNamespace* con nome hello dello spazio dei nomi, e *yourKey* con la chiave di firma di accesso condiviso hello recuperati in precedenza dal portale hello:</span><span class="sxs-lookup"><span data-stu-id="bb953-165">Be sure tooreplace *yourServiceNamespace* with hello name of your namespace, and *yourKey* with hello SAS key you retrieved earlier from hello portal:</span></span>

    ```xml
    <system.serviceModel>
    ...
      <services>
         <service name="ProductsServer.ProductsService">
           <endpoint address="sb://yourServiceNamespace.servicebus.windows.net/products" binding="netTcpRelayBinding" contract="ProductsServer.IProducts" behaviorConfiguration="products"/>
         </service>
      </services>
      <behaviors>
         <endpointBehaviors>
           <behavior name="products">
             <transportClientEndpointBehavior>
                <tokenProvider>
                   <sharedAccessSignature keyName="RootManageSharedAccessKey" key="yourKey" />
                </tokenProvider>
             </transportClientEndpointBehavior>
           </behavior>
         </endpointBehaviors>
      </behaviors>
    </system.serviceModel>
    ```
13. <span data-ttu-id="bb953-166">Ancora in App. config, hello `<appSettings>` elemento, valore di stringa di connessione hello sostituire la stringa di connessione hello ottenuto dal portale hello in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bb953-166">Still in App.config, in hello `<appSettings>` element, replace hello connection string value with hello connection string you previously obtained from hello portal.</span></span>

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. <span data-ttu-id="bb953-167">Premere **Ctrl + MAIUSC + B** o da hello **compilare** menu, fare clic su **Compila soluzione** toobuild hello applicazione e verificare la correttezza hello del lavoro finora.</span><span class="sxs-lookup"><span data-stu-id="bb953-167">Press **Ctrl+Shift+B** or from hello **Build** menu, click **Build Solution** toobuild hello application and verify hello accuracy of your work so far.</span></span>

## <a name="create-an-aspnet-application"></a><span data-ttu-id="bb953-168">Creare un'applicazione ASP.NET</span><span class="sxs-lookup"><span data-stu-id="bb953-168">Create an ASP.NET application</span></span>

<span data-ttu-id="bb953-169">In questa sezione si creerà una semplice applicazione ASP.NET per visualizzare i dati recuperati dal servizio dei prodotti.</span><span class="sxs-lookup"><span data-stu-id="bb953-169">In this section you will build a simple ASP.NET application that displays data retrieved from your product service.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="bb953-170">Creare il progetto hello</span><span class="sxs-lookup"><span data-stu-id="bb953-170">Create hello project</span></span>

1. <span data-ttu-id="bb953-171">Assicurarsi che Visual Studio sia in esecuzione con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="bb953-171">Ensure that Visual Studio is running with administrator privileges.</span></span>
2. <span data-ttu-id="bb953-172">In Visual Studio, su hello **File** menu, fare clic su **New**, quindi fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="bb953-172">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="bb953-173">Da **Modelli installati** in **Visual C#** fare clic su **Applicazione Web ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="bb953-173">From **Installed Templates**, under **Visual C#**, click **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="bb953-174">Progetto hello nome **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="bb953-174">Name hello project **ProductsPortal**.</span></span> <span data-ttu-id="bb953-175">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="bb953-175">Then click **OK**.</span></span>

   ![][15]

4. <span data-ttu-id="bb953-176">Da hello **modelli ASP.NET** elenco hello **nuova applicazione Web ASP.NET** finestra di dialogo, fare clic su **MVC**.</span><span class="sxs-lookup"><span data-stu-id="bb953-176">From hello **ASP.NET Templates** list in hello **New ASP.NET Web Application** dialog, click **MVC**.</span></span>

   ![][16]

6. <span data-ttu-id="bb953-177">Fare clic su hello **Modifica autenticazione** pulsante.</span><span class="sxs-lookup"><span data-stu-id="bb953-177">Click hello **Change Authentication** button.</span></span> <span data-ttu-id="bb953-178">In hello **Modifica autenticazione** finestra di dialogo, verificare che **Nessuna autenticazione** sia selezionata e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="bb953-178">In hello **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="bb953-179">Per questa esercitazione si distribuisce un'app che non richiede l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="bb953-179">For this tutorial, you're deploying an app that does not need a user login.</span></span>

    ![][18]

7. <span data-ttu-id="bb953-180">In hello **nuova applicazione Web ASP.NET** finestra di dialogo, fare clic su **OK** toocreate hello MVC app.</span><span class="sxs-lookup"><span data-stu-id="bb953-180">Back in hello **New ASP.NET Web Application** dialog, click **OK** toocreate hello MVC app.</span></span>
8. <span data-ttu-id="bb953-181">A questo punto è necessario configurare le risorse di Azure per una nuova app Web.</span><span class="sxs-lookup"><span data-stu-id="bb953-181">Now you must configure Azure resources for a new web app.</span></span> <span data-ttu-id="bb953-182">Seguire i passaggi hello hello [pubblicare tooAzure sezione di questo articolo](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="bb953-182">Follow hello steps in hello [Publish tooAzure section of this article](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="bb953-183">Restituire toothis esercitazione, quindi procedere toohello successivo.</span><span class="sxs-lookup"><span data-stu-id="bb953-183">Then, return toothis tutorial and proceed toohello next step.</span></span>
10. <span data-ttu-id="bb953-184">In Esplora soluzioni fare clic con il pulsante destro del mouse su **Modelli**, scegliere **Aggiungi** e infine fare clic su **Classe**.</span><span class="sxs-lookup"><span data-stu-id="bb953-184">In Solution Explorer, right-click **Models** and then click **Add**, then click **Class**.</span></span> <span data-ttu-id="bb953-185">In hello **nome** casella, il nome del tipo hello **Product.cs**.</span><span class="sxs-lookup"><span data-stu-id="bb953-185">In hello **Name** box, type hello name **Product.cs**.</span></span> <span data-ttu-id="bb953-186">Fare quindi clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="bb953-186">Then click **Add**.</span></span>

    ![][17]

### <a name="modify-hello-web-application"></a><span data-ttu-id="bb953-187">Modificare un'applicazione web hello</span><span class="sxs-lookup"><span data-stu-id="bb953-187">Modify hello web application</span></span>

1. <span data-ttu-id="bb953-188">Nel file di Product.cs hello in Visual Studio, sostituire la definizione dello spazio dei nomi esistente hello con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="bb953-188">In hello Product.cs file in Visual Studio, replace hello existing namespace definition with hello following code.</span></span>

   ```csharp
    // Declare properties for hello products inventory.
    namespace ProductsWeb.Models
    {
       public class Product
       {
           public string Id { get; set; }
           public string Name { get; set; }
           public string Quantity { get; set; }
       }
    }
    ```
2. <span data-ttu-id="bb953-189">In Esplora soluzioni espandere hello **controller** cartella, quindi fare doppio clic su hello **HomeController.cs** file tooopen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb953-189">In Solution Explorer, expand hello **Controllers** folder, then double-click hello **HomeController.cs** file tooopen it in Visual Studio.</span></span>
3. <span data-ttu-id="bb953-190">In **HomeController.cs**, sostituire la definizione dello spazio dei nomi esistente hello con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="bb953-190">In **HomeController.cs**, replace hello existing namespace definition with hello following code.</span></span>

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of hello products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. <span data-ttu-id="bb953-191">In Esplora soluzioni, espandere cartella Views\Shared hello, quindi fare doppio clic su **layout. cshtml** tooopen nell'editor di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-191">In Solution Explorer, expand hello Views\Shared folder, then double-click **_Layout.cshtml** tooopen it in hello Visual Studio editor.</span></span>
5. <span data-ttu-id="bb953-192">Modificare tutte le occorrenze di **applicazione ASP.NET** troppo**prodotti di LITWARE**.</span><span class="sxs-lookup"><span data-stu-id="bb953-192">Change all occurrences of **My ASP.NET Application** too**LITWARE's Products**.</span></span>
6. <span data-ttu-id="bb953-193">Rimuovere hello **Home**, **su**, e **contatto** collegamenti.</span><span class="sxs-lookup"><span data-stu-id="bb953-193">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="bb953-194">Nell'esempio seguente di hello, eliminare il codice di hello evidenziato.</span><span class="sxs-lookup"><span data-stu-id="bb953-194">In hello following example, delete hello highlighted code.</span></span>

    ![][41]

7. <span data-ttu-id="bb953-195">In Esplora soluzioni, espandere cartella Views\Home hello, quindi fare doppio clic su **cshtml** tooopen nell'editor di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-195">In Solution Explorer, expand hello Views\Home folder, then double-click **Index.cshtml** tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="bb953-196">Sostituire hello l'intero contenuto del file hello con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="bb953-196">Replace hello entire contents of hello file with hello following code.</span></span>

   ```html
   @model IEnumerable<ProductsWeb.Models.Product>

   @{
            ViewBag.Title = "Index";
   }

   <h2>Prod Inventory</h2>

   <table>
             <tr>
                 <th>
                     @Html.DisplayNameFor(model => model.Name)
                 </th>
                 <th></th>
                 <th>
                     @Html.DisplayNameFor(model => model.Quantity)
                 </th>
             </tr>

   @foreach (var item in Model) {
             <tr>
                 <td>
                     @Html.DisplayFor(modelItem => item.Name)
                 </td>
                 <td>
                     @Html.DisplayFor(modelItem => item.Quantity)
                 </td>
             </tr>
   }

   </table>
   ```
8. <span data-ttu-id="bb953-197">accuratezza hello tooverify del lavoro svolto finora, è possibile premere **Ctrl + MAIUSC + B** progetto hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="bb953-197">tooverify hello accuracy of your work so far, you can press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="run-hello-app-locally"></a><span data-ttu-id="bb953-198">Eseguire app hello in locale</span><span class="sxs-lookup"><span data-stu-id="bb953-198">Run hello app locally</span></span>

<span data-ttu-id="bb953-199">Eseguire tooverify applicazione hello del corretto funzionamento.</span><span class="sxs-lookup"><span data-stu-id="bb953-199">Run hello application tooverify that it works.</span></span>

1. <span data-ttu-id="bb953-200">Verificare che **ProductsPortal** progetto attivo hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-200">Ensure that **ProductsPortal** is hello active project.</span></span> <span data-ttu-id="bb953-201">Nome del progetto hello in Esplora soluzioni e scegliere **imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="bb953-201">Right-click hello project name in Solution Explorer and select **Set As Startup Project**.</span></span>
2. <span data-ttu-id="bb953-202">In Visual Studio premere **F5**.</span><span class="sxs-lookup"><span data-stu-id="bb953-202">In Visual Studio, press **F5**.</span></span>
3. <span data-ttu-id="bb953-203">L'applicazione dovrebbe risultare in esecuzione in un browser.</span><span class="sxs-lookup"><span data-stu-id="bb953-203">Your application should appear, running in a browser.</span></span>

   ![][21]

## <a name="put-hello-pieces-together"></a><span data-ttu-id="bb953-204">Unire parti hello</span><span class="sxs-lookup"><span data-stu-id="bb953-204">Put hello pieces together</span></span>

<span data-ttu-id="bb953-205">passaggio successivo Hello è toohook backup hello ai prodotti server locali con hello applicazione ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="bb953-205">hello next step is toohook up hello on-premises products server with hello ASP.NET application.</span></span>

1. <span data-ttu-id="bb953-206">Se non è già aperto, in Visual Studio aprire nuovamente hello **ProductsPortal** progetto creato in hello [creare un'applicazione ASP.NET](#create-an-aspnet-application) sezione.</span><span class="sxs-lookup"><span data-stu-id="bb953-206">If it is not already open, in Visual Studio re-open hello **ProductsPortal** project you created in hello [Create an ASP.NET application](#create-an-aspnet-application) section.</span></span>
2. <span data-ttu-id="bb953-207">Passaggio toohello simile nella sezione "Creare un Server locale" hello, aggiungere riferimenti al progetto toohello pacchetto NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-207">Similar toohello step in hello "Create an On-Premises Server" section, add hello NuGet package toohello project references.</span></span> <span data-ttu-id="bb953-208">In Esplora soluzioni fare doppio clic su hello **ProductsPortal** del progetto, quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="bb953-208">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="bb953-209">Ricerca di "Bus di servizio" e seleziona hello **Windowsazure** elemento.</span><span class="sxs-lookup"><span data-stu-id="bb953-209">Search for "Service Bus" and select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="bb953-210">Quindi completare l'installazione di hello e chiudere questa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="bb953-210">Then complete hello installation and close this dialog box.</span></span>
4. <span data-ttu-id="bb953-211">In Esplora soluzioni fare doppio clic su hello **ProductsPortal** del progetto, quindi fare clic su **Aggiungi**, quindi **elemento esistente**.</span><span class="sxs-lookup"><span data-stu-id="bb953-211">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Add**, then **Existing Item**.</span></span>
5. <span data-ttu-id="bb953-212">Passare toohello **ProductsContract.cs** file hello **ProductsServer** progetto console.</span><span class="sxs-lookup"><span data-stu-id="bb953-212">Navigate toohello **ProductsContract.cs** file from hello **ProductsServer** console project.</span></span> <span data-ttu-id="bb953-213">Fare clic su toohighlight ProductsContract.cs.</span><span class="sxs-lookup"><span data-stu-id="bb953-213">Click toohighlight ProductsContract.cs.</span></span> <span data-ttu-id="bb953-214">Fare clic su hello freccia giù accanto troppo**Aggiungi**, quindi fare clic su **Aggiungi come collegamento**.</span><span class="sxs-lookup"><span data-stu-id="bb953-214">Click hello down arrow next too**Add**, then click **Add as Link**.</span></span>

   ![][24]

6. <span data-ttu-id="bb953-215">Aprire quindi hello **HomeController.cs** file nell'editor di Visual Studio hello e sostituire definizione dello spazio dei nomi hello con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="bb953-215">Now open hello **HomeController.cs** file in hello Visual Studio editor and replace hello namespace definition with hello following code.</span></span> <span data-ttu-id="bb953-216">Tooreplace assicurarsi di essere *yourServiceNamespace* con nome hello dello spazio dei nomi del servizio, e *yourKey* con la chiave di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="bb953-216">Be sure tooreplace *yourServiceNamespace* with hello name of your service namespace, and *yourKey* with your SAS key.</span></span> <span data-ttu-id="bb953-217">In questo modo hello client toocall hello servizio locale, restituendo hello risultato della chiamata di hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-217">This will enable hello client toocall hello on-premises service, returning hello result of hello call.</span></span>

   ```csharp
   namespace ProductsWeb.Controllers
   {
       using System.Linq;
       using System.ServiceModel;
       using System.Web.Mvc;
       using Microsoft.ServiceBus;
       using Models;
       using ProductsServer;

       public class HomeController : Controller
       {
           // Declare hello channel factory.
           static ChannelFactory<IProductsChannel> channelFactory;

           static HomeController()
           {
               // Create shared access signature token credentials for authentication.
               channelFactory = new ChannelFactory<IProductsChannel>(new NetTcpRelayBinding(),
                   "sb://yourServiceNamespace.servicebus.windows.net/products");
               channelFactory.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior {
                   TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                       "RootManageSharedAccessKey", "yourKey") });
           }

           public ActionResult Index()
           {
               using (IProductsChannel channel = channelFactory.CreateChannel())
               {
                   // Return a view of hello products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. <span data-ttu-id="bb953-218">In Esplora soluzioni fare doppio clic su hello **ProductsPortal** soluzione (assicurarsi che tooright clic hello, non il progetto hello).</span><span class="sxs-lookup"><span data-stu-id="bb953-218">In Solution Explorer, right-click hello **ProductsPortal** solution (make sure tooright-click hello solution, not hello project).</span></span> <span data-ttu-id="bb953-219">Scegliere **Aggiungi**, quindi fare clic su **Progetto esistente**.</span><span class="sxs-lookup"><span data-stu-id="bb953-219">Click **Add**, then click **Existing Project**.</span></span>
8. <span data-ttu-id="bb953-220">Passare toohello **ProductsServer** del progetto, quindi fare doppio clic su hello **ProductsServer.csproj** tooadd file di soluzione è.</span><span class="sxs-lookup"><span data-stu-id="bb953-220">Navigate toohello **ProductsServer** project, then double-click hello **ProductsServer.csproj** solution file tooadd it.</span></span>
9. <span data-ttu-id="bb953-221">**ProductsServer** devono essere eseguite nei dati di hello toodisplay ordine nella **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="bb953-221">**ProductsServer** must be running in order toodisplay hello data on **ProductsPortal**.</span></span> <span data-ttu-id="bb953-222">In Esplora soluzioni fare doppio clic su hello **ProductsPortal** soluzione e fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="bb953-222">In Solution Explorer, right-click hello **ProductsPortal** solution and click **Properties**.</span></span> <span data-ttu-id="bb953-223">Hello **pagine delle proprietà** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="bb953-223">hello **Property Pages** dialog box is displayed.</span></span>
10. <span data-ttu-id="bb953-224">Sul lato sinistro di hello, fare clic su **progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="bb953-224">On hello left side, click **Startup Project**.</span></span> <span data-ttu-id="bb953-225">Sul lato destro di hello, fare clic su **più progetti di avvio**.</span><span class="sxs-lookup"><span data-stu-id="bb953-225">On hello right side, click **Multiple startup projects**.</span></span> <span data-ttu-id="bb953-226">Verificare che **ProductsServer** e **ProductsPortal** viene visualizzato, nell'ordine specificato, con **avviare** impostata come azione hello per entrambi.</span><span class="sxs-lookup"><span data-stu-id="bb953-226">Ensure that **ProductsServer** and **ProductsPortal** appear, in that order, with **Start** set as hello action for both.</span></span>

      ![][25]

11. <span data-ttu-id="bb953-227">Ancora in hello **proprietà** la finestra di dialogo, fare clic su **dipendenze progetto** sul lato sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-227">Still in hello **Properties** dialog box, click **Project Dependencies** on hello left side.</span></span>
12. <span data-ttu-id="bb953-228">In hello **progetti** elenco, fare clic su **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="bb953-228">In hello **Projects** list, click **ProductsServer**.</span></span> <span data-ttu-id="bb953-229">Verificare che **ProductsPortal** non sia selezionato.</span><span class="sxs-lookup"><span data-stu-id="bb953-229">Ensure that **ProductsPortal** is not selected.</span></span>
13. <span data-ttu-id="bb953-230">In hello **progetti** elenco, fare clic su **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="bb953-230">In hello **Projects** list, click **ProductsPortal**.</span></span> <span data-ttu-id="bb953-231">Assicurarsi che **ProductsServer** sia selezionato.</span><span class="sxs-lookup"><span data-stu-id="bb953-231">Ensure that **ProductsServer** is selected.</span></span>

    ![][26]

14. <span data-ttu-id="bb953-232">Fare clic su **OK** in hello **pagine delle proprietà** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="bb953-232">Click **OK** in hello **Property Pages** dialog box.</span></span>

## <a name="run-hello-project-locally"></a><span data-ttu-id="bb953-233">Eseguire il progetto hello in locale</span><span class="sxs-lookup"><span data-stu-id="bb953-233">Run hello project locally</span></span>

<span data-ttu-id="bb953-234">l'applicazione hello tootest localmente, in Visual Studio premere **F5**.</span><span class="sxs-lookup"><span data-stu-id="bb953-234">tootest hello application locally, in Visual Studio press **F5**.</span></span> <span data-ttu-id="bb953-235">server locale Hello (**ProductsServer**) deve iniziare prima, quindi hello **ProductsPortal** deve avviare l'applicazione in una finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="bb953-235">hello on-premises server (**ProductsServer**) should start first, then hello **ProductsPortal** application should start in a browser window.</span></span> <span data-ttu-id="bb953-236">Questa volta, si noterà che l'inventario del prodotto hello Elenca i dati recuperati da hello prodotto del servizio nel sistema locale.</span><span class="sxs-lookup"><span data-stu-id="bb953-236">This time, you will see that hello product inventory lists data retrieved from hello product service on-premises system.</span></span>

![][10]

<span data-ttu-id="bb953-237">Premere **aggiornamento** su hello **ProductsPortal** pagina.</span><span class="sxs-lookup"><span data-stu-id="bb953-237">Press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="bb953-238">Ogni volta che si aggiorna la pagina hello, si noterà hello server app viene visualizzato un messaggio quando `GetProducts()` da **ProductsServer** viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="bb953-238">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

<span data-ttu-id="bb953-239">Chiudere entrambe le applicazioni prima del passaggio successivo toohello di procedere.</span><span class="sxs-lookup"><span data-stu-id="bb953-239">Close both applications before proceeding toohello next step.</span></span>

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a><span data-ttu-id="bb953-240">Distribuire l'applicazione web di Azure di hello ProductsPortal progetto tooan</span><span class="sxs-lookup"><span data-stu-id="bb953-240">Deploy hello ProductsPortal project tooan Azure web app</span></span>

<span data-ttu-id="bb953-241">passaggio successivo Hello è toorepublish hello Azure Web app **ProductsPortal** front-end.</span><span class="sxs-lookup"><span data-stu-id="bb953-241">hello next step is toorepublish hello Azure Web app **ProductsPortal** frontend.</span></span> <span data-ttu-id="bb953-242">Hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb953-242">Do hello following:</span></span>

1. <span data-ttu-id="bb953-243">In Esplora soluzioni fare doppio clic su hello **ProductsPortal** del progetto e fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="bb953-243">In Solution Explorer, right-click hello **ProductsPortal** project, and click **Publish**.</span></span> <span data-ttu-id="bb953-244">Quindi, fare clic su **pubblica** su hello **pubblica** pagina.</span><span class="sxs-lookup"><span data-stu-id="bb953-244">Then, click **Publish** on hello **Publish** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="bb953-245">Si potrebbe visualizzare un messaggio di errore nella finestra del browser hello quando hello **ProductsPortal** progetto web viene avviato automaticamente dopo la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-245">You may see an error message in hello browser window when hello **ProductsPortal** web project is automatically launched after hello deployment.</span></span> <span data-ttu-id="bb953-246">È previsto e si verifica perché hello **ProductsServer** applicazione non è ancora in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="bb953-246">This is expected, and occurs because hello **ProductsServer** application isn't running yet.</span></span>
>
>

2. <span data-ttu-id="bb953-247">Copia URL hello di hello distribuite app web, è necessario hello URL nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-247">Copy hello URL of hello deployed web app, as you will need hello URL in hello next step.</span></span> <span data-ttu-id="bb953-248">È anche possibile ottenere l'URL dalla finestra attività di servizio App di Azure hello in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="bb953-248">You can also obtain this URL from hello Azure App Service Activity window in Visual Studio:</span></span>

  ![][9]

3. <span data-ttu-id="bb953-249">Chiudere hello toostop finestra del browser di hello in esecuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bb953-249">Close hello browser window toostop hello running application.</span></span>

### <a name="set-productsportal-as-web-app"></a><span data-ttu-id="bb953-250">Impostare ProductsPortal come app Web</span><span class="sxs-lookup"><span data-stu-id="bb953-250">Set ProductsPortal as web app</span></span>

<span data-ttu-id="bb953-251">Prima di un'applicazione hello in esecuzione nel cloud hello, è necessario assicurarsi che **ProductsPortal** viene avviato dall'interno di Visual Studio come un'app web.</span><span class="sxs-lookup"><span data-stu-id="bb953-251">Before running hello application in hello cloud, you must ensure that **ProductsPortal** is launched from within Visual Studio as a web app.</span></span>

1. <span data-ttu-id="bb953-252">In Visual Studio, fare doppio clic su hello **ProductsPortal** del progetto e quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="bb953-252">In Visual Studio, right-click hello **ProductsPortal** project and then click **Properties**.</span></span>
2. <span data-ttu-id="bb953-253">Nella colonna sinistra hello, fare clic su **Web**.</span><span class="sxs-lookup"><span data-stu-id="bb953-253">In hello left-hand column, click **Web**.</span></span>
3. <span data-ttu-id="bb953-254">In hello **azione di avvio** fare clic su hello **Avvia URL** pulsante e immettere nella casella di testo hello hello URL per l'app web distribuiti in precedenza; ad esempio, `http://productsportal1234567890.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="bb953-254">In hello **Start Action** section, click hello **Start URL** button, and in hello text box enter hello URL for your previously deployed web app; for example, `http://productsportal1234567890.azurewebsites.net/`.</span></span>

    ![][27]

4. <span data-ttu-id="bb953-255">Da hello **File** menu in Visual Studio, fare clic su **Salva tutto**.</span><span class="sxs-lookup"><span data-stu-id="bb953-255">From hello **File** menu in Visual Studio, click **Save All**.</span></span>
5. <span data-ttu-id="bb953-256">Dal menu Compila di hello in Visual Studio, fare clic su **Ricompila soluzione**.</span><span class="sxs-lookup"><span data-stu-id="bb953-256">From hello Build menu in Visual Studio, click **Rebuild Solution**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="bb953-257">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="bb953-257">Run hello application</span></span>

1. <span data-ttu-id="bb953-258">Premere F5 toobuild ed eseguire un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-258">Press F5 toobuild and run hello application.</span></span> <span data-ttu-id="bb953-259">server locale Hello (hello **ProductsServer** applicazione console) deve iniziare prima, quindi hello **ProductsPortal** deve avviare l'applicazione in una finestra del browser, come illustrato nella seguente schermata hello ripresa.</span><span class="sxs-lookup"><span data-stu-id="bb953-259">hello on-premises server (hello **ProductsServer** console application) should start first, then hello **ProductsPortal** application should start in a browser window, as shown in hello following screen shot.</span></span> <span data-ttu-id="bb953-260">Si noti nuovamente che l'inventario del prodotto hello Elenca i dati recuperati da hello prodotto del servizio nel sistema locale e li visualizza nell'app web hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-260">Notice again that hello product inventory lists data retrieved from hello product service on-premises system, and displays that data in hello web app.</span></span> <span data-ttu-id="bb953-261">Controllare toomake URL hello assicurarsi che **ProductsPortal** è in esecuzione nel cloud di hello, come un'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="bb953-261">Check hello URL toomake sure that **ProductsPortal** is running in hello cloud, as an Azure web app.</span></span>

   ![][1]

   > [!IMPORTANT]
   > <span data-ttu-id="bb953-262">Hello **ProductsServer** applicazione console deve essere in esecuzione e in grado di tooserve hello dati toohello **ProductsPortal** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bb953-262">hello **ProductsServer** console application must be running and able tooserve hello data toohello **ProductsPortal** application.</span></span> <span data-ttu-id="bb953-263">Se il browser hello viene visualizzato un errore, attendere alcuni secondi altre per **ProductsServer** tooload e hello di visualizzazione seguenti del messaggio.</span><span class="sxs-lookup"><span data-stu-id="bb953-263">If hello browser displays an error, wait a few more seconds for **ProductsServer** tooload and display hello following message.</span></span> <span data-ttu-id="bb953-264">Premere quindi **aggiornamento** nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="bb953-264">Then press **Refresh** in hello browser.</span></span>
   >
   >

   ![][37]
2. <span data-ttu-id="bb953-265">Nel browser hello, premere **aggiornamento** su hello **ProductsPortal** pagina.</span><span class="sxs-lookup"><span data-stu-id="bb953-265">Back in hello browser, press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="bb953-266">Ogni volta che si aggiorna la pagina hello, si noterà hello server app viene visualizzato un messaggio quando `GetProducts()` da **ProductsServer** viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="bb953-266">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

    ![][38]

## <a name="next-steps"></a><span data-ttu-id="bb953-267">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bb953-267">Next steps</span></span>

<span data-ttu-id="bb953-268">toolearn ulteriori informazioni sull'inoltro di Azure, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="bb953-268">toolearn more about Azure Relay, see hello following resources:</span></span>  

* [<span data-ttu-id="bb953-269">Che cos'è il servizio di inoltro di Azure?</span><span class="sxs-lookup"><span data-stu-id="bb953-269">What is Azure Relay?</span></span>](relay-what-is-it.md)  
* [<span data-ttu-id="bb953-270">La modalità di inoltro toouse</span><span class="sxs-lookup"><span data-stu-id="bb953-270">How toouse Relay</span></span>](service-bus-dotnet-how-to-use-relay.md)  

[0]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hybrid.png
[1]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[NuGet]: http://nuget.org

[11]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-con-1.png
[13]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-13.png
[15]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-2.png
[16]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-4.png
[17]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-7.png
[18]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-5.png
[9]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-9.png
[10]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App3.png

[21]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App1.png
[24]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-12.png
[25]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-13.png
[26]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-14.png
[27]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-8.png

[36]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[37]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service1.png
[38]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service2.png
[41]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-40.png
[43]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-hybrid-43.png
