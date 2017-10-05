---
title: Come configurare il computer per lo sviluppo di applicazioni di Servizi multimediali con .NET
description: Informazioni sui prerequisiti generali per l'uso di Servizi multimediali con Media Services SDK per .NET e su come creare un'app di Visual Studio.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: 15828bc74937a036871b26493498232ec7cf6f06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="851ce-104">Sviluppo di applicazioni di Servizi multimediali con .NET</span><span class="sxs-lookup"><span data-stu-id="851ce-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="851ce-105">Questo argomento illustra come iniziare a sviluppare applicazioni di Servizi multimediali con .NET.</span><span class="sxs-lookup"><span data-stu-id="851ce-105">This topic discusses how to start developing Media Services applications using .NET.</span></span>

<span data-ttu-id="851ce-106">La libreria di **Azure Media Services .NET SDK** consente di programmare per Servizi multimediali usando .NET.</span><span class="sxs-lookup"><span data-stu-id="851ce-106">The **Azure Media Services .NET SDK** library enables you to program against Media Services using .NET.</span></span> <span data-ttu-id="851ce-107">Per facilitare ancora di più lo sviluppo con .NET, è disponibile la libreria di **Media Services .NET SDK Extensions**,</span><span class="sxs-lookup"><span data-stu-id="851ce-107">To make it even easier to develop with .NET, the **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="851ce-108">contenente un set di funzioni di supporto e metodi di estensione che semplificano il codice .NET.</span><span class="sxs-lookup"><span data-stu-id="851ce-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="851ce-109">Entrambe le librerie sono disponibili tramite **NuGet** e **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="851ce-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="851ce-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="851ce-110">Prerequisites</span></span>
* <span data-ttu-id="851ce-111">Un account di Servizi multimediali ottenuto con una sottoscrizione di Azure nuova o esistente.</span><span class="sxs-lookup"><span data-stu-id="851ce-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="851ce-112">Vedere l'argomento [Come creare un account di Servizi multimediali](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="851ce-112">See the topic [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="851ce-113">Sistemi operativi: Windows 10, Windows 7, Windows 2008 R2 o Windows 8.</span><span class="sxs-lookup"><span data-stu-id="851ce-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="851ce-114">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="851ce-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="851ce-115">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="851ce-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="851ce-116">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="851ce-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="851ce-117">In questa sezione viene illustrato come creare un progetto in Visual Studio e configurarlo per lo sviluppo in Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="851ce-117">This section shows you how to create a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="851ce-118">In questo caso, il progetto è un'applicazione console Windows C#, ma la stessa procedura di configurazione si applica ad altri tipi di progetti che è possibile creare per le applicazioni Servizi multimediali, ad esempio un'applicazione Windows Forms o un'applicazione Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="851ce-118">In this case, the project is a C# Windows console application, but the same setup steps shown here apply to other types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="851ce-119">Questa sezione illustra come usare **NuGet** per aggiungere Media Services .NET SDK Extensions e altre librerie dipendenti.</span><span class="sxs-lookup"><span data-stu-id="851ce-119">This section shows how to use **NuGet** to add Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="851ce-120">In alternativa, è possibile ottenere i bit più recenti di Media Services .NET SDK da GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) o [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), compilare la soluzione e quindi aggiungere i riferimenti al progetto client.</span><span class="sxs-lookup"><span data-stu-id="851ce-120">Alternatively, you can get the latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build the solution, and add the references to the client project.</span></span> <span data-ttu-id="851ce-121">Tutte le dipendenze necessarie vengono scaricate ed estratte automaticamente.</span><span class="sxs-lookup"><span data-stu-id="851ce-121">All the necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="851ce-122">Creare una nuova applicazione console C# in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="851ce-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="851ce-123">Immettere un valore nei campi **Nome**, **Percorso** e **Nome soluzione**, quindi fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="851ce-123">Enter the **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="851ce-124">Compilare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="851ce-124">Build the solution.</span></span>
3. <span data-ttu-id="851ce-125">Usare il pacchetto **NuGet** per installare e aggiungere **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span><span class="sxs-lookup"><span data-stu-id="851ce-125">Use **NuGet** to install and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="851ce-126">Insieme al pacchetto viene installato anche **Media Services .NET SDK** e vengono aggiunte tutte le altre dipendenze necessarie.</span><span class="sxs-lookup"><span data-stu-id="851ce-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="851ce-127">Verificare di aver installato la versione più aggiornata di NuGet.</span><span class="sxs-lookup"><span data-stu-id="851ce-127">Ensure that you have the newest version of NuGet installed.</span></span> <span data-ttu-id="851ce-128">Per altre informazioni e per istruzioni di installazione, vedere [NuGet](http://nuget.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="851ce-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="851ce-129">In Esplora soluzioni fare clic con il pulsante destro del mouse sul nome del progetto e scegliere Gestisci pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="851ce-129">In Solution Explorer, right-click the name of the project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="851ce-130">Viene visualizzata la finestra di dialogo Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="851ce-130">The Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="851ce-131">Nella raccolta Online eseguire la ricerca di Azure MediaServices Extensions, scegliere Azure Media Services .NET SDK Extensions e fare clic sul pulsante Installa.</span><span class="sxs-lookup"><span data-stu-id="851ce-131">In the Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click the Install button.</span></span>
   
    <span data-ttu-id="851ce-132">Il progetto viene modificato e vengono aggiunti riferimenti a Media Services .NET SDK, alle relative estensioni e ad altri assembly dipendenti.</span><span class="sxs-lookup"><span data-stu-id="851ce-132">The project is modified and references to the Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="851ce-133">Per ottenere un ambiente di sviluppo più lineare, prendere in considerazione l'abilitazione di NuGet Package Restore.</span><span class="sxs-lookup"><span data-stu-id="851ce-133">To promote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="851ce-134">Per altre informazioni vedere l'articolo relativo al [ripristino del pacchetto NuGet](http://docs.nuget.org/consume/package-restore).</span><span class="sxs-lookup"><span data-stu-id="851ce-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="851ce-135">Aggiungere un riferimento all'assembly **System.Configuration** .</span><span class="sxs-lookup"><span data-stu-id="851ce-135">Add a reference to **System.Configuration** assembly.</span></span> <span data-ttu-id="851ce-136">che contiene la classe**System.Configuration.ConfigurationManager** usata per accedere ai file di configurazione, ad esempio App.config.</span><span class="sxs-lookup"><span data-stu-id="851ce-136">This assembly contains the System.Configuration.**ConfigurationManager** class that is used to access configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="851ce-137">Per aggiungere riferimenti usando la finestra di dialogo Gestione riferimenti, fare clic sul nome del progetto in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="851ce-137">To add references using the Manage References dialog, right-click the project name in the Solution Explorer.</span></span> <span data-ttu-id="851ce-138">Selezionare quindi Aggiungi e Riferimenti.</span><span class="sxs-lookup"><span data-stu-id="851ce-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="851ce-139">Viene visualizzata la finestra di dialogo Gestione riferimenti.</span><span class="sxs-lookup"><span data-stu-id="851ce-139">The Manage References dialog appears.</span></span>
8. <span data-ttu-id="851ce-140">Negli assembly .NET Framework trovare e selezionare l'assembly System.Configuration e premere OK.</span><span class="sxs-lookup"><span data-stu-id="851ce-140">Under .NET framework assemblies, find and select the System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="851ce-141">Aprire il file App.config e aggiungere una sezione *appSettings* al file.</span><span class="sxs-lookup"><span data-stu-id="851ce-141">Open the App.config file and add an *appSettings* section to the file.</span></span>     
   
    <span data-ttu-id="851ce-142">Impostare i valori necessari per connettersi all'API di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="851ce-142">Set the values that are needed to connect to the Media Services API.</span></span> <span data-ttu-id="851ce-143">Per altre informazioni, vedere [Accesso all'API di Servizi multimediali di Azure con l'autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="851ce-143">For more information, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="851ce-144">Se si usa l'[autenticazione utente](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication), il file di configurazione avrà probabilmente i valori per il dominio tenant di Azure AD e l'endpoint dell'API di REST AMS.</span><span class="sxs-lookup"><span data-stu-id="851ce-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and the AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="851ce-145">La maggior parte dei codici di esempio di Servizi multimediali di Azure usa un tipo di utente (interattivo) di autenticazione per la connessione all'API di AMS.</span><span class="sxs-lookup"><span data-stu-id="851ce-145">Most code samples in the Azure Media Services documentation set, use a user (interactive) type of authentication to connect to the AMS API.</span></span> <span data-ttu-id="851ce-146">Questo metodo di autenticazione funzionerà in modo efficace per le app native di gestione o monitoraggio: app per dispositivi mobili, app di Windows e app console.</span><span class="sxs-lookup"><span data-stu-id="851ce-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="851ce-147">Questo metodo di autenticazione non è adatto per il tipo applicazioni come API delle applicazioni, servizi Web e server.</span><span class="sxs-lookup"><span data-stu-id="851ce-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="851ce-148">Per altre informazioni, vedere [Accesso all'API di Servizi multimediali di Azure con l'autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="851ce-148">For more information, see [Access the AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="851ce-149">Sovrascrivere le istruzioni **using** esistenti all'inizio del file Program.cs con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="851ce-149">Overwrite the existing **using** statements at the beginning of the Program.cs file with the following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="851ce-150">A questo punto, si è pronti per iniziare a sviluppare un'applicazione di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="851ce-150">At this point, you are ready to start developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="851ce-151">Esempio</span><span class="sxs-lookup"><span data-stu-id="851ce-151">Example</span></span>

<span data-ttu-id="851ce-152">Di seguito è riportato un semplice esempio che consente di eseguire la connessione all'API AMS ed elencare tutti i processori di contenuti multimediali disponibili.</span><span class="sxs-lookup"><span data-stu-id="851ce-152">Here is a small example that connects to the AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a><span data-ttu-id="851ce-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="851ce-153">Next steps</span></span>

<span data-ttu-id="851ce-154">Ora [è possibile connettersi all'API AMS](media-services-use-aad-auth-to-access-ams-api.md) e iniziare lo [sviluppo](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="851ce-154">Now [you can connect to the AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="851ce-155">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="851ce-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="851ce-156">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="851ce-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

