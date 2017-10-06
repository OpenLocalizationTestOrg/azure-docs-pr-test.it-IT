---
title: aaaHow tooSet dei Computer per lo sviluppo di servizi multimediali con .NET
description: Informazioni sui prerequisiti di hello per servizi multimediali usando hello Media Services SDK per .NET. Viene inoltre illustrato come toocreate un'app di Visual Studio.
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
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="b00b2-104">Sviluppo di applicazioni di Servizi multimediali con .NET</span><span class="sxs-lookup"><span data-stu-id="b00b2-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="b00b2-105">Questo argomento viene illustrata la modalità di servizi multimediali di sviluppo di toostart applicazioni con .NET.</span><span class="sxs-lookup"><span data-stu-id="b00b2-105">This topic discusses how toostart developing Media Services applications using .NET.</span></span>

<span data-ttu-id="b00b2-106">Hello **Azure Media Services .NET SDK** libreria consente tooprogram in servizi multimediali usando .NET.</span><span class="sxs-lookup"><span data-stu-id="b00b2-106">hello **Azure Media Services .NET SDK** library enables you tooprogram against Media Services using .NET.</span></span> <span data-ttu-id="b00b2-107">anche più facile toodevelop con .NET, hello toomake **Azure Media Services .NET SDK Extensions** viene fornita una libreria.</span><span class="sxs-lookup"><span data-stu-id="b00b2-107">toomake it even easier toodevelop with .NET, hello **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="b00b2-108">contenente un set di funzioni di supporto e metodi di estensione che semplificano il codice .NET.</span><span class="sxs-lookup"><span data-stu-id="b00b2-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="b00b2-109">Entrambe le librerie sono disponibili tramite **NuGet** e **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="b00b2-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b00b2-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b00b2-110">Prerequisites</span></span>
* <span data-ttu-id="b00b2-111">Un account di Servizi multimediali ottenuto con una sottoscrizione di Azure nuova o esistente.</span><span class="sxs-lookup"><span data-stu-id="b00b2-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="b00b2-112">Vedere l'argomento hello [come un Account di servizi multimediali tooCreate](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="b00b2-112">See hello topic [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="b00b2-113">Sistemi operativi: Windows 10, Windows 7, Windows 2008 R2 o Windows 8.</span><span class="sxs-lookup"><span data-stu-id="b00b2-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="b00b2-114">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="b00b2-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="b00b2-115">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b00b2-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="b00b2-116">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b00b2-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="b00b2-117">In questa sezione illustra come toocreate un progetto in Visual Studio e configurarlo per lo sviluppo di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="b00b2-117">This section shows you how toocreate a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="b00b2-118">In questo caso, il progetto di hello è un'applicazione console c# Windows, ma hello stessi passaggi di configurazione illustrati di seguito si applicano tooother tipi di progetti, che è possibile creare per le applicazioni di servizi multimediali (ad esempio, un'applicazione Windows Form o un'applicazione Web ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="b00b2-118">In this case, hello project is a C# Windows console application, but hello same setup steps shown here apply tooother types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="b00b2-119">Questa sezione viene illustrato come toouse **NuGet** tooadd Media Services .NET SDK extensions e altre librerie dipendenti.</span><span class="sxs-lookup"><span data-stu-id="b00b2-119">This section shows how toouse **NuGet** tooadd Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="b00b2-120">In alternativa, è possibile ottenere i bit di Media Services .NET SDK più recente di hello da GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) o [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), compilare la soluzione hello e aggiungere hello riferimenti toohello client progetto.</span><span class="sxs-lookup"><span data-stu-id="b00b2-120">Alternatively, you can get hello latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build hello solution, and add hello references toohello client project.</span></span> <span data-ttu-id="b00b2-121">Tutte le dipendenze necessarie di hello scaricate ed estratte automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b00b2-121">All hello necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="b00b2-122">Creare una nuova applicazione console C# in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b00b2-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="b00b2-123">Immettere hello **nome**, **percorso**, e **Nome soluzione**, quindi fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="b00b2-123">Enter hello **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="b00b2-124">Compilare la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="b00b2-124">Build hello solution.</span></span>
3. <span data-ttu-id="b00b2-125">Utilizzare **NuGet** tooinstall e aggiungere **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span><span class="sxs-lookup"><span data-stu-id="b00b2-125">Use **NuGet** tooinstall and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="b00b2-126">Insieme al pacchetto viene installato anche **Media Services .NET SDK** e vengono aggiunte tutte le altre dipendenze necessarie.</span><span class="sxs-lookup"><span data-stu-id="b00b2-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="b00b2-127">Assicurarsi di aver hello la versione più recente di NuGet.</span><span class="sxs-lookup"><span data-stu-id="b00b2-127">Ensure that you have hello newest version of NuGet installed.</span></span> <span data-ttu-id="b00b2-128">Per altre informazioni e per istruzioni di installazione, vedere [NuGet](http://nuget.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="b00b2-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="b00b2-129">In Esplora soluzioni fare doppio clic su nome hello del progetto di hello e scegliere Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="b00b2-129">In Solution Explorer, right-click hello name of hello project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="b00b2-130">verrà visualizzata la finestra di dialogo Gestisci pacchetti NuGet di Hello.</span><span class="sxs-lookup"><span data-stu-id="b00b2-130">hello Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="b00b2-131">Nella raccolta Online hello, cercare le estensioni di Microsoft Azure, scegliere Azure Media Services .NET SDK Extensions e quindi fare clic su pulsante Installa hello.</span><span class="sxs-lookup"><span data-stu-id="b00b2-131">In hello Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click hello Install button.</span></span>
   
    <span data-ttu-id="b00b2-132">progetto Hello viene modificato e fa riferimento a toohello Media Services .NET SDK Extensions Media Services .NET SDK e altri assembly dipendenti vengono aggiunti.</span><span class="sxs-lookup"><span data-stu-id="b00b2-132">hello project is modified and references toohello Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="b00b2-133">toopromote un ambiente di sviluppo di pulizia, è consigliabile abilitare il ripristino del pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="b00b2-133">toopromote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="b00b2-134">Per altre informazioni vedere l'articolo relativo al [ripristino del pacchetto NuGet](http://docs.nuget.org/consume/package-restore).</span><span class="sxs-lookup"><span data-stu-id="b00b2-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="b00b2-135">Aggiungere un riferimento troppo**Configuration** assembly.</span><span class="sxs-lookup"><span data-stu-id="b00b2-135">Add a reference too**System.Configuration** assembly.</span></span> <span data-ttu-id="b00b2-136">Questo assembly contiene hello System. Configuration. **ConfigurationManager** classe che rappresenta il file di configurazione tooaccess utilizzato (ad esempio, App. config).</span><span class="sxs-lookup"><span data-stu-id="b00b2-136">This assembly contains hello System.Configuration.**ConfigurationManager** class that is used tooaccess configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="b00b2-137">riferimenti tooadd mediante finestra di dialogo Gestione riferimenti hello, fare clic sul nome del progetto in Esplora soluzioni hello hello.</span><span class="sxs-lookup"><span data-stu-id="b00b2-137">tooadd references using hello Manage References dialog, right-click hello project name in hello Solution Explorer.</span></span> <span data-ttu-id="b00b2-138">Selezionare quindi Aggiungi e Riferimenti.</span><span class="sxs-lookup"><span data-stu-id="b00b2-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="b00b2-139">viene visualizzata la finestra Gestione riferimenti Hello.</span><span class="sxs-lookup"><span data-stu-id="b00b2-139">hello Manage References dialog appears.</span></span>
8. <span data-ttu-id="b00b2-140">Negli assembly di .NET framework, trovare e selezionare l'assembly System. Configuration hello e fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="b00b2-140">Under .NET framework assemblies, find and select hello System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="b00b2-141">Aprire il file app. config hello e aggiungere un *appSettings* file toohello di sezione.</span><span class="sxs-lookup"><span data-stu-id="b00b2-141">Open hello App.config file and add an *appSettings* section toohello file.</span></span>     
   
    <span data-ttu-id="b00b2-142">Impostare i valori hello che sono necessari tooconnect toohello API di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="b00b2-142">Set hello values that are needed tooconnect toohello Media Services API.</span></span> <span data-ttu-id="b00b2-143">Per ulteriori informazioni, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="b00b2-143">For more information, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="b00b2-144">Se si utilizza [l'autenticazione utente](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) il file di configurazione verrà probabilmente dispongono di valori per il dominio tenant di Azure AD e hello endpoint API REST AMS.</span><span class="sxs-lookup"><span data-stu-id="b00b2-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and hello AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="b00b2-145">La maggior parte degli esempi di codice nella documentazione di servizi multimediali di Azure hello impostato, utilizzare un tipo di utente (interattivo) di autenticazione tooconnect toohello AMS API.</span><span class="sxs-lookup"><span data-stu-id="b00b2-145">Most code samples in hello Azure Media Services documentation set, use a user (interactive) type of authentication tooconnect toohello AMS API.</span></span> <span data-ttu-id="b00b2-146">Questo metodo di autenticazione funzionerà in modo efficace per le app native di gestione o monitoraggio: app per dispositivi mobili, app di Windows e app console.</span><span class="sxs-lookup"><span data-stu-id="b00b2-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="b00b2-147">Questo metodo di autenticazione non è adatto per il tipo applicazioni come API delle applicazioni, servizi Web e server.</span><span class="sxs-lookup"><span data-stu-id="b00b2-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="b00b2-148">Per ulteriori informazioni, vedere [hello accesso API AMS con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="b00b2-148">For more information, see [Access hello AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="b00b2-149">Sovrascrivi hello esistente **utilizzando** istruzioni all'inizio di hello del file Program.cs hello con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="b00b2-149">Overwrite hello existing **using** statements at hello beginning of hello Program.cs file with hello following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="b00b2-150">A questo punto, si è pronti toostart lo sviluppo di un'applicazione di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="b00b2-150">At this point, you are ready toostart developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="b00b2-151">Esempio</span><span class="sxs-lookup"><span data-stu-id="b00b2-151">Example</span></span>

<span data-ttu-id="b00b2-152">Di seguito è riportato un esempio di piccole dimensioni che si connette toohello AMS API e vengono elencati tutti i processori di contenuti multimediali disponibili.</span><span class="sxs-lookup"><span data-stu-id="b00b2-152">Here is a small example that connects toohello AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from hello App.config file.
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

##<a name="next-steps"></a><span data-ttu-id="b00b2-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b00b2-153">Next steps</span></span>

<span data-ttu-id="b00b2-154">Ora [è possibile connettersi toohello API AMS](media-services-use-aad-auth-to-access-ams-api.md) e avviare [sviluppo](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b00b2-154">Now [you can connect toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="b00b2-155">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="b00b2-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b00b2-156">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="b00b2-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

