---
title: Configurare le impostazioni dell'app per le funzioni di Azure | Microsoft Docs
description: Informazioni su come configurare le impostazioni dell'app per le funzioni di Azure.
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
ms.openlocfilehash: 3b23011f66592151d517d61bf806da8743f38e03
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-manage-a-function-app-in-the-azure-portal"></a><span data-ttu-id="07792-103">Come gestire un'app per le funzioni nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="07792-103">How to manage a function app in the Azure portal</span></span> 

<span data-ttu-id="07792-104">In Funzioni di Azure un'app per le funzioni fornisce il contesto di esecuzione per le singole funzioni.</span><span class="sxs-lookup"><span data-stu-id="07792-104">In Azure Functions, a function app provides the execution context for your individual functions.</span></span> <span data-ttu-id="07792-105">I comportamenti dell'app per le funzioni si applicano a tutte le funzioni ospitate da un'app per le funzioni specifica.</span><span class="sxs-lookup"><span data-stu-id="07792-105">Function app behaviors apply to all functions hosted by a given function app.</span></span> <span data-ttu-id="07792-106">In questo argomento viene descritto come configurare e gestire le app per le funzioni nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="07792-106">This topic describes how to configure and manage your function apps in the Azure portal.</span></span>

<span data-ttu-id="07792-107">Innanzitutto passare al [portale di Azure](http://portal.azure.com) e accedere all'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="07792-107">To begin, go to the [Azure portal](http://portal.azure.com) and sign in to your Azure account.</span></span> <span data-ttu-id="07792-108">Nella barra di ricerca nella parte superiore del portale digitare il nome dell'app per le funzioni e selezionarla dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="07792-108">In the search bar at the top of the portal, type the name of your function app and select it from the list.</span></span> <span data-ttu-id="07792-109">Dopo aver selezionato l'app per le funzioni, viene visualizzata la pagina seguente:</span><span class="sxs-lookup"><span data-stu-id="07792-109">After selecting your function app, you see the following page:</span></span>

![Panoramica dell'app per le funzioni nel portale di Azure](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="07792-111"><a name="manage-app-service-settings"></a>Scheda delle impostazioni dell'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="07792-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![Panoramica dell'app per le funzioni nel portale di Azure.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="07792-113">Nella scheda **Impostazioni** è possibile aggiornare la versione di runtime di Funzioni usata dall'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="07792-113">The **Settings** tab is where you can update the Functions runtime version used by your function app.</span></span> <span data-ttu-id="07792-114">È anche possibile gestire le chiavi host usate per limitare l'accesso HTTP a tutte le funzioni ospitate dall'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="07792-114">It is also where you manage the host keys used to restrict HTTP access to all functions hosted by the function app.</span></span>

<span data-ttu-id="07792-115">Funzioni supporta sia i piani di hosting a consumo che i piani di hosting del servizio app.</span><span class="sxs-lookup"><span data-stu-id="07792-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="07792-116">Per altre informazioni vedere [Scegliere il piano di servizio corretto per Funzioni di Azure](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="07792-116">For more information, see [Choose the correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="07792-117">Per una migliore prevedibilità nel piano di consumo, Funzioni consente di limitare l'uso della piattaforma impostando una quota di uso giornaliera, in secondi di gigabyte.</span><span class="sxs-lookup"><span data-stu-id="07792-117">For better predictability in the Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="07792-118">Quando la quota di uso giornaliera viene raggiunta, l'app per le funzioni viene arrestata.</span><span class="sxs-lookup"><span data-stu-id="07792-118">Once the daily usage quota is reached, the function app is stopped.</span></span> <span data-ttu-id="07792-119">In questo caso può essere riattivata dallo stesso contesto dell'impostazione della quota di spesa giornaliera.</span><span class="sxs-lookup"><span data-stu-id="07792-119">A function app stopped as a result of reaching the spending quota can be re-enabled from the same context as establishing the daily spending quota.</span></span> <span data-ttu-id="07792-120">Vedere la [pagina prezzi di Funzioni di Azure](http://azure.microsoft.com/pricing/details/functions/) per altre informazioni sulla fatturazione.</span><span class="sxs-lookup"><span data-stu-id="07792-120">See the [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="07792-121">Scheda delle funzionalità della piattaforma</span><span class="sxs-lookup"><span data-stu-id="07792-121">Platform features tab</span></span>

![Scheda delle funzionalità della piattaforma per l'app per le funzioni.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="07792-123">Le app per le funzioni vengono eseguite e gestite dalla piattaforma Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="07792-123">Function apps run in, and are maintained, by the Azure App Service platform.</span></span> <span data-ttu-id="07792-124">Di conseguenza, le app per le funzioni hanno accesso alla maggior parte delle funzionalità di piattaforma di hosting Web di base di Azure.</span><span class="sxs-lookup"><span data-stu-id="07792-124">As such, your function apps have access to most of the features of Azure's core web hosting platform.</span></span> <span data-ttu-id="07792-125">Nella scheda **Funzionalità della piattaforma** è possibile accedere a molte funzionalità della piattaforma del servizio app che è possibile usare nelle app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="07792-125">The **Platform features** tab is where you access the many features of the App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="07792-126">Non tutte le funzionalità del servizio app sono disponibili quando un'app per le funzioni viene eseguita nel piano di hosting a consumo.</span><span class="sxs-lookup"><span data-stu-id="07792-126">Not all App Service features are available when a function app runs on the Consumption hosting plan.</span></span>

<span data-ttu-id="07792-127">La restante parte di questo argomento illustra le seguenti funzionalità di servizio app nel portale di Azure utili per Funzioni:</span><span class="sxs-lookup"><span data-stu-id="07792-127">The rest of this topic focuses on the following App Service features in the Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="07792-128">Editor del servizio app</span><span class="sxs-lookup"><span data-stu-id="07792-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="07792-129">Impostazioni dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="07792-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="07792-130">Console</span><span class="sxs-lookup"><span data-stu-id="07792-130">Console</span></span>](#console)
+ [<span data-ttu-id="07792-131">Strumenti avanzati (Kudu)</span><span class="sxs-lookup"><span data-stu-id="07792-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="07792-132">Opzioni di distribuzione</span><span class="sxs-lookup"><span data-stu-id="07792-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="07792-133">CORS</span><span class="sxs-lookup"><span data-stu-id="07792-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="07792-134">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="07792-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="07792-135">Definizione dell'API</span><span class="sxs-lookup"><span data-stu-id="07792-135">API definition</span></span>](#swagger)

<span data-ttu-id="07792-136">Per altre informazioni su come usare le impostazioni del servizio app, vedere [Configurare le impostazioni di del servizio app di Azure](../app-service-web/web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="07792-136">For more information about how to work with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="07792-137"><a name="editor"></a>Editor del servizio app</span><span class="sxs-lookup"><span data-stu-id="07792-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![Editor del servizio app per l'app per le funzioni.](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="07792-139">L'editor del servizio app è un editor avanzato, disponibile nel portale, che si può usare per modificare i file di configurazione JSON e i file del codice nello stesso modo.</span><span class="sxs-lookup"><span data-stu-id="07792-139">The App Service editor is an advanced in-portal editor that you can use to modify JSON configuration files and code files alike.</span></span> <span data-ttu-id="07792-140">Quando si sceglie questa opzione, viene aperta una scheda separata del browser con un editor di base.</span><span class="sxs-lookup"><span data-stu-id="07792-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="07792-141">Ciò consente di realizzare l'integrazione con l'archivio Git, eseguire il codice e il relativo debug e modificare le impostazioni dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="07792-141">This enables you to integrate with the Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="07792-142">Questo editor offre un ambiente di sviluppo migliorato per le funzioni confrontato con il pannello dell'app per le funzioni predefinito.</span><span class="sxs-lookup"><span data-stu-id="07792-142">This editor provides an enhanced development environment for your functions compared with the default function app blade.</span></span>    |

![Editor del servizio app](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="07792-144"><a name="settings"></a>Impostazioni dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="07792-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![Impostazioni delle applicazioni per l'app per le funzioni.](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="07792-146">Nel pannello **Impostazioni applicazione** del servizio app è possibile configurare e gestire le versioni di framework, il debug remoto, le impostazioni dell'app e le stringhe di connessione.</span><span class="sxs-lookup"><span data-stu-id="07792-146">The App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="07792-147">Quando l'app per le funzioni si integra con altri servizi di terze parti e di Azure, qui è possibile modificare tali impostazioni.</span><span class="sxs-lookup"><span data-stu-id="07792-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![Configurare le impostazioni dell'applicazione](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="07792-149"><a name="console"></a>Console</span><span class="sxs-lookup"><span data-stu-id="07792-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![Console dell'app per le funzioni nel portale di Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="07792-151">La console nel portale è uno strumento ideale per gli sviluppatori quando si desidera interagire con l'app per le funzioni dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="07792-151">The in-portal console is an ideal developer tool when you prefer to interact with your function app from the command line.</span></span> <span data-ttu-id="07792-152">I comandi comuni includono la creazione e lo spostamento di file e directory, nonché l'esecuzione di script e file batch.</span><span class="sxs-lookup"><span data-stu-id="07792-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![Console dell'app per le funzioni](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="07792-154"><a name="kudu"></a>Strumenti avanzati (Kudu)</span><span class="sxs-lookup"><span data-stu-id="07792-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![App per le funzioni Kudu nel portale di Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="07792-156">Gli strumenti avanzati per il servizio app, noto anche come Kudu, consentono l'accesso alle funzionalità amministrative avanzate dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="07792-156">The advanced tools for App Service (also known as Kudu) provide access to advanced administrative features of your function app.</span></span> <span data-ttu-id="07792-157">Dalla Kudu è possibile gestire informazioni di sistema, impostazioni dell'app, variabili di ambiente, estensioni del sito, intestazioni HTTP e variabili del server.</span><span class="sxs-lookup"><span data-stu-id="07792-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="07792-158">È anche possibile avviare **Kudu** selezionando l'endpoint SCM per l'app per le funzioni, ad esempio`https://<myfunctionapp>.scm.azurewebsites.net/`</span><span class="sxs-lookup"><span data-stu-id="07792-158">You can also launch **Kudu** by browsing to the SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![Configurare Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="07792-160"><a name="deployment">Opzioni di distribuzione</span><span class="sxs-lookup"><span data-stu-id="07792-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Opzioni di distribuzione dell'app per le funzioni nel portale di Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="07792-162">Funzioni consente di sviluppare il codice della funzione sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="07792-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="07792-163">È quindi possibile caricare il progetto dell'app per le funzioni locale in Azure.</span><span class="sxs-lookup"><span data-stu-id="07792-163">You can then upload your local function app project to Azure.</span></span> <span data-ttu-id="07792-164">Oltre al caricamento FTP tradizionale, Funzioni consente di distribuire l'app per le funzioni usando le soluzioni di integrazione continua più diffusi, come GitHub, VSTS, Dropbox, Bitbucket e altre.</span><span class="sxs-lookup"><span data-stu-id="07792-164">In addition to traditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="07792-165">Per altre informazioni, vedere [Distribuzione continua per Funzioni di Azure](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="07792-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="07792-166">Per caricare manualmente tramite FTP o Git locale, è necessario anche [configurare le credenziali di distribuzione](functions-continuous-deployment.md#credentials).</span><span class="sxs-lookup"><span data-stu-id="07792-166">To upload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="07792-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="07792-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![CORS di app per le funzioni nel portale di Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="07792-169">Per impedire l'esecuzione di codici dannosi nei servizi, il servizio app consente di bloccare le chiamate alle app per le funzioni da origini esterne.</span><span class="sxs-lookup"><span data-stu-id="07792-169">To prevent malicious code execution in your services, App Service blocks calls to your function apps from external sources.</span></span> <span data-ttu-id="07792-170">Funzioni supporta la condivisione di risorse tra le origini, CORS per consentire la definizione di un "elenco" di origini consentite da cui le funzioni possono accettare le richieste remote.</span><span class="sxs-lookup"><span data-stu-id="07792-170">Functions supports cross-origin resource sharing (CORS) to let you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![Configurare CORS per l'app per le funzioni](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="07792-172"><a name="auth"></a>Autenticazione</span><span class="sxs-lookup"><span data-stu-id="07792-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![Autenticazione dell'app per le funzioni nel portale di Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="07792-174">Quando le funzioni usano un trigger HTTP, è possibile richiedere innanzitutto l'autenticazione delle chiamate.</span><span class="sxs-lookup"><span data-stu-id="07792-174">When functions use an HTTP trigger, you can require calls to first be authenticated.</span></span> <span data-ttu-id="07792-175">Servizio app supporta l'autenticazione di Azure Active Directory e consente di accedere ai provider social, quali Facebook, Microsoft e Twitter.</span><span class="sxs-lookup"><span data-stu-id="07792-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="07792-176">Per informazioni dettagliate sulla configurazione di specifici provider di autenticazione, vedere [Autenticazione e autorizzazione nel servizio app di Azure](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="07792-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![Configurare l'autenticazione per un'app per le funzioni](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="07792-178"><a name="swagger"></a>Definizione dell'API</span><span class="sxs-lookup"><span data-stu-id="07792-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![Definizione dello swagger API dell'app per le funzioni nel portale di Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="07792-180">Funzioni supporta Swagger per consentire ai client di usare più facilmente le funzioni attivate da HTTP.</span><span class="sxs-lookup"><span data-stu-id="07792-180">Functions supports Swagger to allow clients to more easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="07792-181">Per altre informazioni sulla creazione di definizioni API con Swagger, visitare [Introduzione alle app per le API, ad ASP.NET e a Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="07792-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="07792-182">È anche possibile usare Proxy di Funzioni per definire una singola superficie API per le funzioni multiple.</span><span class="sxs-lookup"><span data-stu-id="07792-182">You can also use Functions Proxies to define a single API surface for multiple functions.</span></span> <span data-ttu-id="07792-183">Per altre informazioni, vedere [Uso di proxy in Funzioni di Azure](functions-proxies.md).</span><span class="sxs-lookup"><span data-stu-id="07792-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![Configurare l'API per l'app per le funzioni](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="07792-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="07792-185">Next steps</span></span>

+ [<span data-ttu-id="07792-186">Configurare le impostazioni del servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="07792-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="07792-187">Distribuzione continua per Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="07792-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



