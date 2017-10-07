---
title: le impostazioni dell'App di Azure funzione aaaConfigure | Documenti Microsoft
description: Informazioni su come tooconfigure Azure funzionare le impostazioni dell'app.
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a><span data-ttu-id="856f3-103">Come un'app di funzione nel portale di Azure hello toomanage</span><span class="sxs-lookup"><span data-stu-id="856f3-103">How toomanage a function app in hello Azure portal</span></span> 

<span data-ttu-id="856f3-104">Nelle funzioni di Azure, un'app di funzione fornisce il contesto di esecuzione hello per le singole funzioni.</span><span class="sxs-lookup"><span data-stu-id="856f3-104">In Azure Functions, a function app provides hello execution context for your individual functions.</span></span> <span data-ttu-id="856f3-105">I comportamenti di app di funzione applicano funzioni di tooall ospitate da un'app di funzione specificata.</span><span class="sxs-lookup"><span data-stu-id="856f3-105">Function app behaviors apply tooall functions hosted by a given function app.</span></span> <span data-ttu-id="856f3-106">Questo argomento viene descritto come tooconfigure e gestire le app di funzione in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="856f3-106">This topic describes how tooconfigure and manage your function apps in hello Azure portal.</span></span>

<span data-ttu-id="856f3-107">toobegin, andare toohello [portale di Azure](http://portal.azure.com) ed eseguire l'accesso tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="856f3-107">toobegin, go toohello [Azure portal](http://portal.azure.com) and sign in tooyour Azure account.</span></span> <span data-ttu-id="856f3-108">Nella barra di ricerca hello nella parte superiore di hello del portale hello, digitare il nome di hello dell'app in funzione e selezionarlo dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="856f3-108">In hello search bar at hello top of hello portal, type hello name of your function app and select it from hello list.</span></span> <span data-ttu-id="856f3-109">Dopo aver selezionato l'app di funzione, viene visualizzato hello pagina seguente:</span><span class="sxs-lookup"><span data-stu-id="856f3-109">After selecting your function app, you see hello following page:</span></span>

![Panoramica della funzione app nel portale di Azure hello](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="856f3-111"><a name="manage-app-service-settings"></a>Scheda delle impostazioni dell'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="856f3-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![Panoramica della funzione app nel portale di Azure hello.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="856f3-113">Hello **impostazioni** scheda è dove è possibile aggiornare versione del runtime funzioni hello usato dall'app (funzione).</span><span class="sxs-lookup"><span data-stu-id="856f3-113">hello **Settings** tab is where you can update hello Functions runtime version used by your function app.</span></span> <span data-ttu-id="856f3-114">È inoltre possibile gestire hello host chiavi utilizzate toorestrict HTTP tooall funzioni di accesso ospitate da app di funzione hello.</span><span class="sxs-lookup"><span data-stu-id="856f3-114">It is also where you manage hello host keys used toorestrict HTTP access tooall functions hosted by hello function app.</span></span>

<span data-ttu-id="856f3-115">Funzioni supporta sia i piani di hosting a consumo che i piani di hosting del servizio app.</span><span class="sxs-lookup"><span data-stu-id="856f3-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="856f3-116">Per ulteriori informazioni, vedere [piano di servizio corretto scegliere hello per le funzioni di Azure](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="856f3-116">For more information, see [Choose hello correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="856f3-117">Per una migliore prevedibilità nel piano di consumo hello, funzioni consente di limitare l'utilizzo di piattaforma impostando una quota di utilizzo giornaliero, in secondi di gigabyte.</span><span class="sxs-lookup"><span data-stu-id="856f3-117">For better predictability in hello Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="856f3-118">Una volta raggiunto quota di utilizzo giornaliero hello, app di funzione hello è stato arrestato.</span><span class="sxs-lookup"><span data-stu-id="856f3-118">Once hello daily usage quota is reached, hello function app is stopped.</span></span> <span data-ttu-id="856f3-119">Un'app di funzione arrestata in seguito a raggiungere hello spesa quota può essere riattivata da hello stabilire hello quotidianamente spesa quota stesso contesto.</span><span class="sxs-lookup"><span data-stu-id="856f3-119">A function app stopped as a result of reaching hello spending quota can be re-enabled from hello same context as establishing hello daily spending quota.</span></span> <span data-ttu-id="856f3-120">Vedere hello [funzioni Azure pagina dei prezzi](http://azure.microsoft.com/pricing/details/functions/) per i dettagli sulla fatturazione.</span><span class="sxs-lookup"><span data-stu-id="856f3-120">See hello [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="856f3-121">Scheda delle funzionalità della piattaforma</span><span class="sxs-lookup"><span data-stu-id="856f3-121">Platform features tab</span></span>

![Scheda delle funzionalità della piattaforma per l'app per le funzioni.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="856f3-123">Funzione App eseguite in e vengono mantenute, dalla piattaforma Azure App Service hello.</span><span class="sxs-lookup"><span data-stu-id="856f3-123">Function apps run in, and are maintained, by hello Azure App Service platform.</span></span> <span data-ttu-id="856f3-124">Di conseguenza, le app di funzione hanno accesso toomost funzionalità hello di piattaforma di hosting web di base di Azure.</span><span class="sxs-lookup"><span data-stu-id="856f3-124">As such, your function apps have access toomost of hello features of Azure's core web hosting platform.</span></span> <span data-ttu-id="856f3-125">Hello **funzionalità della piattaforma** scheda è dove è possibile accedere hello molte funzionalità della piattaforma di servizio App che è possibile utilizzare nelle app di funzione hello.</span><span class="sxs-lookup"><span data-stu-id="856f3-125">hello **Platform features** tab is where you access hello many features of hello App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="856f3-126">Non tutte le funzionalità di servizio App sono disponibili quando si esegue un'app di funzione nel piano di hosting consumo hello.</span><span class="sxs-lookup"><span data-stu-id="856f3-126">Not all App Service features are available when a function app runs on hello Consumption hosting plan.</span></span>

<span data-ttu-id="856f3-127">rest Hello di questo argomento è incentrato su hello seguenti caratteristiche di servizio App in hello portale di Azure che sono utili per le funzioni:</span><span class="sxs-lookup"><span data-stu-id="856f3-127">hello rest of this topic focuses on hello following App Service features in hello Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="856f3-128">Editor del servizio app</span><span class="sxs-lookup"><span data-stu-id="856f3-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="856f3-129">Impostazioni dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="856f3-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="856f3-130">Console</span><span class="sxs-lookup"><span data-stu-id="856f3-130">Console</span></span>](#console)
+ [<span data-ttu-id="856f3-131">Strumenti avanzati (Kudu)</span><span class="sxs-lookup"><span data-stu-id="856f3-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="856f3-132">Opzioni di distribuzione</span><span class="sxs-lookup"><span data-stu-id="856f3-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="856f3-133">CORS</span><span class="sxs-lookup"><span data-stu-id="856f3-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="856f3-134">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="856f3-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="856f3-135">Definizione dell'API</span><span class="sxs-lookup"><span data-stu-id="856f3-135">API definition</span></span>](#swagger)

<span data-ttu-id="856f3-136">Per ulteriori informazioni su come toowork con le impostazioni di servizio App, vedere [configurare le impostazioni di Azure App Service](../app-service-web/web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="856f3-136">For more information about how toowork with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="856f3-137"><a name="editor"></a>Editor del servizio app</span><span class="sxs-lookup"><span data-stu-id="856f3-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![Editor del servizio app per l'app per le funzioni.](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="856f3-139">Hello editor di servizio App è un editor avanzato nel portale, che è possibile utilizzare i file di configurazione JSON toomodify e file di codice simili.</span><span class="sxs-lookup"><span data-stu-id="856f3-139">hello App Service editor is an advanced in-portal editor that you can use toomodify JSON configuration files and code files alike.</span></span> <span data-ttu-id="856f3-140">Quando si sceglie questa opzione, viene aperta una scheda separata del browser con un editor di base.</span><span class="sxs-lookup"><span data-stu-id="856f3-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="856f3-141">Questo consente toointegrate con codice di debug, esecuzione e repository Git hello e modificare le impostazioni dell'app di funzione.</span><span class="sxs-lookup"><span data-stu-id="856f3-141">This enables you toointegrate with hello Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="856f3-142">Questo editor fornisce un ambiente di sviluppo avanzato per le funzioni confrontato con pannello app di funzione predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="856f3-142">This editor provides an enhanced development environment for your functions compared with hello default function app blade.</span></span>    |

![Hello editor di servizio App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="856f3-144"><a name="settings"></a>Impostazioni dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="856f3-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![Impostazioni delle applicazioni per l'app per le funzioni.](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="856f3-146">Servizio App Hello **le impostazioni dell'applicazione** pannello è possibile configurare e gestire le versioni di framework, il debug remoto, le impostazioni dell'app e le stringhe di connessione.</span><span class="sxs-lookup"><span data-stu-id="856f3-146">hello App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="856f3-147">Quando l'app per le funzioni si integra con altri servizi di terze parti e di Azure, qui è possibile modificare tali impostazioni.</span><span class="sxs-lookup"><span data-stu-id="856f3-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![Configurare le impostazioni dell'applicazione](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="856f3-149"><a name="console"></a>Console</span><span class="sxs-lookup"><span data-stu-id="856f3-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![Console di app di funzione in hello portale di Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="856f3-151">console di Hello nel portale è uno strumento ideale per sviluppatori quando si preferisce toointeract con l'app di funzione dalla riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="856f3-151">hello in-portal console is an ideal developer tool when you prefer toointeract with your function app from hello command line.</span></span> <span data-ttu-id="856f3-152">I comandi comuni includono la creazione e lo spostamento di file e directory, nonché l'esecuzione di script e file batch.</span><span class="sxs-lookup"><span data-stu-id="856f3-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![Console dell'app per le funzioni](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="856f3-154"><a name="kudu"></a>Strumenti avanzati (Kudu)</span><span class="sxs-lookup"><span data-stu-id="856f3-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![Funzione app Kudu in hello portale di Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="856f3-156">Hello strumenti avanzati per il servizio App (noto anche come Kudu) forniscono accesso tooadvanced le funzionalità amministrative dell'app in funzione.</span><span class="sxs-lookup"><span data-stu-id="856f3-156">hello advanced tools for App Service (also known as Kudu) provide access tooadvanced administrative features of your function app.</span></span> <span data-ttu-id="856f3-157">Dalla Kudu è possibile gestire informazioni di sistema, impostazioni dell'app, variabili di ambiente, estensioni del sito, intestazioni HTTP e variabili del server.</span><span class="sxs-lookup"><span data-stu-id="856f3-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="856f3-158">È anche possibile avviare **Kudu** esplorando toohello endpoint di Gestione controllo servizi per l'app di funzione, ad esempio`https://<myfunctionapp>.scm.azurewebsites.net/`</span><span class="sxs-lookup"><span data-stu-id="856f3-158">You can also launch **Kudu** by browsing toohello SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![Configurare Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="856f3-160"><a name="deployment">Opzioni di distribuzione</span><span class="sxs-lookup"><span data-stu-id="856f3-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Opzioni di distribuzione di app di funzione in hello portale di Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="856f3-162">Funzioni consente di sviluppare il codice della funzione sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="856f3-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="856f3-163">È quindi possibile caricare il tooAzure di progetto app di funzione locale.</span><span class="sxs-lookup"><span data-stu-id="856f3-163">You can then upload your local function app project tooAzure.</span></span> <span data-ttu-id="856f3-164">Inoltre tootraditional di caricamento tramite FTP, le funzioni consentono di distribuire un'applicazione di funzione con soluzioni di integrazione continua comuni, come GitHub, Visual Studio Team Services, Dropbox, Bitbucket e altri.</span><span class="sxs-lookup"><span data-stu-id="856f3-164">In addition tootraditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="856f3-165">Per altre informazioni, vedere [Distribuzione continua per Funzioni di Azure](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="856f3-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="856f3-166">tooupload manualmente tramite FTP o Git locale, è anche necessario [configurare le credenziali di distribuzione](functions-continuous-deployment.md#credentials).</span><span class="sxs-lookup"><span data-stu-id="856f3-166">tooupload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="856f3-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="856f3-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![Funzione app CORS in hello portale di Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="856f3-169">esecuzione di codice dannoso tooprevent nei servizi, i blocchi di servizio App chiama tooyour funzione app da origini esterne.</span><span class="sxs-lookup"><span data-stu-id="856f3-169">tooprevent malicious code execution in your services, App Service blocks calls tooyour function apps from external sources.</span></span> <span data-ttu-id="856f3-170">Funzioni supporta risorse multiorigine (CORS) toolet si definisce un "elenco" di consentite le origini da cui le funzioni possono accettare richieste remote di condivisione.</span><span class="sxs-lookup"><span data-stu-id="856f3-170">Functions supports cross-origin resource sharing (CORS) toolet you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![Configurare CORS per l'app per le funzioni](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="856f3-172"><a name="auth"></a>Autenticazione</span><span class="sxs-lookup"><span data-stu-id="856f3-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![Autenticazione dell'app nel portale di Azure hello (funzione)](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="856f3-174">Quando le funzioni utilizzano un trigger HTTP, è possibile richiedere chiamate toofirst essere autenticato.</span><span class="sxs-lookup"><span data-stu-id="856f3-174">When functions use an HTTP trigger, you can require calls toofirst be authenticated.</span></span> <span data-ttu-id="856f3-175">Servizio app supporta l'autenticazione di Azure Active Directory e consente di accedere ai provider social, quali Facebook, Microsoft e Twitter.</span><span class="sxs-lookup"><span data-stu-id="856f3-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="856f3-176">Per informazioni dettagliate sulla configurazione di specifici provider di autenticazione, vedere [Autenticazione e autorizzazione nel servizio app di Azure](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="856f3-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![Configurare l'autenticazione per un'app per le funzioni](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="856f3-178"><a name="swagger"></a>Definizione dell'API</span><span class="sxs-lookup"><span data-stu-id="856f3-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![Funzione app API swagger di definizione di hello portale di Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="856f3-180">Funzioni supporta Swagger tooallow client toomore utilizzare facilmente le funzioni di attivazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="856f3-180">Functions supports Swagger tooallow clients toomore easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="856f3-181">Per altre informazioni sulla creazione di definizioni API con Swagger, visitare [Introduzione alle app per le API, ad ASP.NET e a Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="856f3-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="856f3-182">Inoltre, è possibile utilizzare funzioni proxy toodefine una superficie API singola per più funzioni.</span><span class="sxs-lookup"><span data-stu-id="856f3-182">You can also use Functions Proxies toodefine a single API surface for multiple functions.</span></span> <span data-ttu-id="856f3-183">Per altre informazioni, vedere [Uso di proxy in Funzioni di Azure](functions-proxies.md).</span><span class="sxs-lookup"><span data-stu-id="856f3-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![Configurare l'API per l'app per le funzioni](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="856f3-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="856f3-185">Next steps</span></span>

+ [<span data-ttu-id="856f3-186">Configurare le impostazioni del servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="856f3-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="856f3-187">Distribuzione continua per Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="856f3-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



