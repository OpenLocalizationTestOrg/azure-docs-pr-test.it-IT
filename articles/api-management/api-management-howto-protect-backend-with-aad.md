---
title: aaaProtect un back-end Web API con Azure Active Directory e gestione API | Documenti Microsoft
description: Informazioni su come tooprotect un back-end Web API con Azure Active Directory e gestione API.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a><span data-ttu-id="f5524-103">Come tooprotect un back-end Web API con Azure Active Directory e gestione API</span><span class="sxs-lookup"><span data-stu-id="f5524-103">How tooprotect a Web API backend with Azure Active Directory and API Management</span></span>
<span data-ttu-id="f5524-104">Hello seguente video viene illustrato come toobuild un back-end Web API e proteggerla mediante il protocollo OAuth 2.0 con Azure Active Directory e gestione API.</span><span class="sxs-lookup"><span data-stu-id="f5524-104">hello following video shows how toobuild a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span></span>  <span data-ttu-id="f5524-105">In questo articolo viene fornita una panoramica e informazioni aggiuntive per hello i passaggi nel video hello.</span><span class="sxs-lookup"><span data-stu-id="f5524-105">This article provides an overview and additional information for hello steps in hello video.</span></span> <span data-ttu-id="f5524-106">Il video della durata di 24 minuti mostra come fare per:</span><span class="sxs-lookup"><span data-stu-id="f5524-106">This 24 minute video shows you how to:</span></span>

* <span data-ttu-id="f5524-107">Compilare il back-end di un'API Web e proteggerlo con AAD - iniziando all’1:30</span><span class="sxs-lookup"><span data-stu-id="f5524-107">Build a Web API backend and secure it with AAD - starting at 1:30</span></span>
* <span data-ttu-id="f5524-108">Importare l'API hello in Gestione API, a partire da 7:10</span><span class="sxs-lookup"><span data-stu-id="f5524-108">Import hello API into API Management - starting at 7:10</span></span>
* <span data-ttu-id="f5524-109">Configurare hello Developer toocall portale hello API, a partire da 9:09</span><span class="sxs-lookup"><span data-stu-id="f5524-109">Configure hello Developer portal toocall hello API - starting at 9:09</span></span>
* <span data-ttu-id="f5524-110">Configurare un hello toocall applicazione desktop API, a partire da 18:08</span><span class="sxs-lookup"><span data-stu-id="f5524-110">Configure a desktop application toocall hello API - starting at 18:08</span></span>
* <span data-ttu-id="f5524-111">Configurare un toopre di criteri di convalida JWT-autorizzare richieste - a partire da 20:47</span><span class="sxs-lookup"><span data-stu-id="f5524-111">Configure a JWT validation policy toopre-authorize requests - starting at 20:47</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a><span data-ttu-id="f5524-112">Creare una directory di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5524-112">Create an Azure AD directory</span></span>
<span data-ttu-id="f5524-113">toosecure l'API Web eseguito tramite Azure Active Directory è necessario disporre di un un tenant di AAD.</span><span class="sxs-lookup"><span data-stu-id="f5524-113">toosecure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span></span> <span data-ttu-id="f5524-114">Questo video usa un tenant denominato **APIMDemo** .</span><span class="sxs-lookup"><span data-stu-id="f5524-114">In this video a tenant named **APIMDemo** is used.</span></span> <span data-ttu-id="f5524-115">toocreate un tenant di AAD, accedi toohello [portale di Azure classico](https://manage.windowsazure.com) e fare clic su **New**->**servizi App**->**Active Directory**->**Directory**->**creazione personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="f5524-115">toocreate an AAD tenant, sign-in toohello [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span></span> 

![Azure Active Directory][api-management-create-aad-menu]

<span data-ttu-id="f5524-117">In questo esempio viene creata una directory denominata **APIMDemo** con un dominio predefinito denominato **DemoAPIM.onmicrosoft.com**. Questa directory viene utilizzata in tutto il video hello.</span><span class="sxs-lookup"><span data-stu-id="f5524-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**. This directory is used throughout hello video.</span></span>

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a><span data-ttu-id="f5524-119">Creare un servizio API Web protetto da Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5524-119">Create a Web API service secured by Azure Active Directory</span></span>
<span data-ttu-id="f5524-120">In questo passaggio viene creato il back-end di un'API Web con Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="f5524-120">In this step, a Web API backend is created using Visual Studio 2013.</span></span> <span data-ttu-id="f5524-121">Questo passaggio di hello video inizia da 1:30.</span><span class="sxs-lookup"><span data-stu-id="f5524-121">This step of hello video starts at 1:30.</span></span> <span data-ttu-id="f5524-122">progetto di back-end Web API toocreate in fare clic su Visual Studio **File**->**New**->**progetto**e scegliere **Web ASP.NET Applicazione** da hello **Web** elenco di modelli.</span><span class="sxs-lookup"><span data-stu-id="f5524-122">toocreate Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from hello **Web** templates list.</span></span> <span data-ttu-id="f5524-123">In questo video hello progetto viene denominato **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="f5524-123">In this video hello project is named **APIMAADDemo**.</span></span> <span data-ttu-id="f5524-124">Fare clic su **OK** progetto hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="f5524-124">Click **OK** toocreate hello project.</span></span> 

![Visual Studio][api-management-new-web-app]

<span data-ttu-id="f5524-126">Fare clic su **API Web** da hello **selezionare un modello di elenco** toocreate un progetto di API Web.</span><span class="sxs-lookup"><span data-stu-id="f5524-126">Click **Web API** from hello **Select a template list** toocreate a Web API project.</span></span> <span data-ttu-id="f5524-127">Fare clic su autenticazione di Azure Directory tooconfigure **Modifica autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="f5524-127">tooconfigure Azure Directory Authentication click **Change Authentication**.</span></span>

![Nuovo progetto][api-management-new-project]

<span data-ttu-id="f5524-129">Fare clic su **account aziendali**e specificare hello **dominio** del tenant di AAD.</span><span class="sxs-lookup"><span data-stu-id="f5524-129">Click **Organizational Accounts**, and specify hello **Domain** of your AAD tenant.</span></span> <span data-ttu-id="f5524-130">In hello in questo esempio è dominio **DemoAPIM.onmicrosoft.com**. dominio hello di directory può essere ottenuto dalla hello **domini** della directory.</span><span class="sxs-lookup"><span data-stu-id="f5524-130">In this example hello domain is **DemoAPIM.onmicrosoft.com**. hello domain of your directory can be obtained from hello **Domains** tab of your directory.</span></span>

![Domini][api-management-aad-domains]

<span data-ttu-id="f5524-132">Configurare le impostazioni di hello desiderato in hello **Modifica autenticazione** la finestra di dialogo e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="f5524-132">Configure hello desired settings in hello **Change Authentication** dialog box and click **OK**.</span></span>

![Modifica autenticazione][api-management-change-authentication]

<span data-ttu-id="f5524-134">Quando fa clic su **OK** Visual Studio tenterà tooregister l'applicazione con la directory di Azure AD e potrebbe essere richiesta toosign in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f5524-134">When you click **OK** Visual Studio will attempt tooregister your application with your Azure AD directory and you may be prompted toosign in by Visual Studio.</span></span> <span data-ttu-id="f5524-135">Accedere con un account amministrativo per la directory.</span><span class="sxs-lookup"><span data-stu-id="f5524-135">Sign in using an administrative account for your directory.</span></span>

![Accedi tooVisual Studio][api-management-sign-in-vidual-studio]

<span data-ttu-id="f5524-137">Questo progetto come un hello controllo API Web di Azure di tooconfigure casella per **Host nel cloud hello** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="f5524-137">tooconfigure this project as an Azure Web API check hello box for **Host in hello cloud** and then click **OK**.</span></span>

![Nuovo progetto][api-management-new-project-cloud]

<span data-ttu-id="f5524-139">Potrebbe essere richiesta toosign in tooAzure e quindi è possibile configurare hello App Web.</span><span class="sxs-lookup"><span data-stu-id="f5524-139">You may be prompted toosign in tooAzure, and then you can configure hello Web App.</span></span>

![Configurare][api-management-configure-web-app]

<span data-ttu-id="f5524-141">In questo esempio viene specificato un nuovo **Piano di servizio app** denominato **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="f5524-141">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span></span>

<span data-ttu-id="f5524-142">Fare clic su **OK** tooconfigure hello Web App e creare il progetto di hello.</span><span class="sxs-lookup"><span data-stu-id="f5524-142">Click **OK** tooconfigure hello Web App and create hello project.</span></span>

## <a name="add-hello-code-toohello-web-api-project"></a><span data-ttu-id="f5524-143">Aggiungere il progetto API Web di hello codice toohello</span><span class="sxs-lookup"><span data-stu-id="f5524-143">Add hello code toohello Web API project</span></span>
<span data-ttu-id="f5524-144">passaggio successivo Hello video hello aggiunge il progetto hello codice toohello API Web.</span><span class="sxs-lookup"><span data-stu-id="f5524-144">hello next step in hello video adds hello code toohello Web API project.</span></span> <span data-ttu-id="f5524-145">Questo passaggio inizia da 4:35 minuti.</span><span class="sxs-lookup"><span data-stu-id="f5524-145">This step starts at 4:35.</span></span>

<span data-ttu-id="f5524-146">Hello API Web in questo esempio implementa un servizio di calcolatrice di base usando un modello e un controller.</span><span class="sxs-lookup"><span data-stu-id="f5524-146">hello Web API in this example implements a basic calculator service using a model and a controller.</span></span> <span data-ttu-id="f5524-147">modello di hello tooadd per il servizio di hello, fare doppio clic su **modelli** in **Esplora** e scegliere **Aggiungi**, **classe**.</span><span class="sxs-lookup"><span data-stu-id="f5524-147">tooadd hello model for hello service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span></span> <span data-ttu-id="f5524-148">Nome classe hello `CalcInput` e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f5524-148">Name hello class `CalcInput` and click **Add**.</span></span>

<span data-ttu-id="f5524-149">Aggiungere il seguente hello `using` hello cima toohello istruzione `CalcInput.cs` file.</span><span class="sxs-lookup"><span data-stu-id="f5524-149">Add hello following `using` statement toohello top of hello `CalcInput.cs` file.</span></span>

```c#
using Newtonsoft.Json;
```

<span data-ttu-id="f5524-150">Sostituire la classe hello generato con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="f5524-150">Replace hello generated class with hello following code.</span></span>

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

<span data-ttu-id="f5524-151">Fare clic con il pulsante destro del mouse su **Controller** in **Esplora soluzioni** e scegliere **Aggiungi**->**Controller**.</span><span class="sxs-lookup"><span data-stu-id="f5524-151">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span></span> <span data-ttu-id="f5524-152">Scegliere **Web API 2 Controller - Empty** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f5524-152">Choose **Web API 2 Controller - Empty** and click **Add**.</span></span> <span data-ttu-id="f5524-153">Tipo **CalcController** per hello Controller e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f5524-153">Type **CalcController** for hello Controller name and click **Add**.</span></span>

![Aggiungi controller][api-management-add-controller]

<span data-ttu-id="f5524-155">Aggiungere il seguente hello `using` hello cima toohello istruzione `CalcController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="f5524-155">Add hello following `using` statement toohello top of hello `CalcController.cs` file.</span></span>

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

<span data-ttu-id="f5524-156">Sostituire classe controller hello generato con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="f5524-156">Replace hello generated controller class with hello following code.</span></span> <span data-ttu-id="f5524-157">Questo codice implementa hello `Add`, `Subtract`, `Multiply`, e `Divide` operazioni di base API Calculator hello.</span><span class="sxs-lookup"><span data-stu-id="f5524-157">This code implements hello `Add`, `Subtract`, `Multiply`, and `Divide` operations of hello Basic Calculator API.</span></span>

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

<span data-ttu-id="f5524-158">Premere **F6** toobuild e verificare la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="f5524-158">Press **F6** toobuild and verify hello solution.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="f5524-159">Pubblicare hello progetto tooAzure</span><span class="sxs-lookup"><span data-stu-id="f5524-159">Publish hello project tooAzure</span></span>
<span data-ttu-id="f5524-160">In questo hello passaggio Visual Studio progetto è tooAzure pubblicato.</span><span class="sxs-lookup"><span data-stu-id="f5524-160">In this step hello Visual Studio project is published tooAzure.</span></span> <span data-ttu-id="f5524-161">Questo passaggio di hello video inizia in corrispondenza di 5:45.</span><span class="sxs-lookup"><span data-stu-id="f5524-161">This step of hello video starts at 5:45.</span></span>

<span data-ttu-id="f5524-162">toopublish hello progetto tooAzure destro del mouse su hello **APIMAADDemo** sul progetto in Visual Studio e scegliere **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="f5524-162">toopublish hello project tooAzure, right-click hello **APIMAADDemo** project in Visual Studio and choose **Publish**.</span></span> <span data-ttu-id="f5524-163">Mantenere le impostazioni predefinite di hello in hello **pubblica sul Web** la finestra di dialogo e fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="f5524-163">Keep hello default settings in hello **Publish Web** dialog box and click **Publish**.</span></span>

![Pubblicazione sul Web][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a><span data-ttu-id="f5524-165">Concedere le autorizzazioni applicazione del servizio back-end toohello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5524-165">Grant permissions toohello Azure AD backend service application</span></span>
<span data-ttu-id="f5524-166">Viene creata una nuova applicazione per il servizio back-end hello nella directory di Azure AD come parte della configurazione hello e processo di pubblicazione del progetto API Web.</span><span class="sxs-lookup"><span data-stu-id="f5524-166">A new application for hello backend service is created in your Azure AD directory as part of hello configuring and publishing process of your Web API project.</span></span> <span data-ttu-id="f5524-167">In questo passaggio di hello video a partire da 6:13, le autorizzazioni vengono concesse back-end Web API toohello.</span><span class="sxs-lookup"><span data-stu-id="f5524-167">In this step of hello video, starting at 6:13, permissions are granted toohello Web API backend.</span></span>

![Applicazione][api-management-aad-backend-app]

<span data-ttu-id="f5524-169">Fare clic su nome hello di autorizzazioni di hello applicazione tooconfigure hello necessario.</span><span class="sxs-lookup"><span data-stu-id="f5524-169">Click hello name of hello application tooconfigure hello required permissions.</span></span> <span data-ttu-id="f5524-170">Passare toohello **configura** scheda e scorrere verso il basso toohello **autorizzazioni tooother applicazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="f5524-170">Navigate toohello **Configure** tab and scroll down toohello **permissions tooother applications** section.</span></span> <span data-ttu-id="f5524-171">Fare clic su hello **autorizzazioni applicazione** elenco a discesa accanto a **Windows** **Azure Active Directory**, casella hello per **lettura dati directory**, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="f5524-171">Click hello **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check hello box for **Read directory data**, and click **Save**.</span></span>

![Aggiungere autorizzazioni][api-management-aad-add-permissions]

> [!NOTE]
> <span data-ttu-id="f5524-173">Se **Windows** **Azure Active Directory** non è elencato nel autorizzazioni tooother applicazioni, fare clic su **aggiungere applicazione** e aggiungere l'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="f5524-173">If **Windows** **Azure Active Directory** is not listed under permissions tooother applications, click **Add application** and add it from hello list.</span></span>
> 
> 

<span data-ttu-id="f5524-174">Prendere nota di hello **URI Id App** per l'utilizzo in un passaggio successivo, quando un'applicazione Azure AD è configurata per portale per sviluppatori di hello gestione API.</span><span class="sxs-lookup"><span data-stu-id="f5524-174">Make a note of hello **App Id URI** for use in a subsequent step when an Azure AD application is configured for hello API Management developer portal.</span></span>

![URI ID app][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a><span data-ttu-id="f5524-176">Importare hello API Web in Gestione API</span><span class="sxs-lookup"><span data-stu-id="f5524-176">Import hello Web API into API Management</span></span>
<span data-ttu-id="f5524-177">Le API vengono configurate dal portale di pubblicazione di hello API, è possibile accedervi tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5524-177">APIs are configured from hello API publisher portal, which is accessed through hello Azure Portal.</span></span> <span data-ttu-id="f5524-178">tooreach, fare clic su **portale di pubblicazione** dalla barra degli strumenti hello del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="f5524-178">tooreach it, click **Publisher portal** from hello toolbar of your API Management service.</span></span> <span data-ttu-id="f5524-179">Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [gestione API prima] [ Manage your first API] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f5524-179">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API][Manage your first API] tutorial.</span></span>

![Portale di pubblicazione][api-management-management-console]

<span data-ttu-id="f5524-181">Le operazioni possono essere [aggiunti manualmente tooAPIs](api-management-howto-add-operations.md), o possono essere importati.</span><span class="sxs-lookup"><span data-stu-id="f5524-181">Operations can be [added tooAPIs manually](api-management-howto-add-operations.md), or they can be imported.</span></span> <span data-ttu-id="f5524-182">In questo video le operazioni vengono importante in formato Swagger a partire da 6:40 minuti.</span><span class="sxs-lookup"><span data-stu-id="f5524-182">In this video, operations are imported in Swagger format starting at 6:40.</span></span>

<span data-ttu-id="f5524-183">Creare un file denominato `calcapi.json` con contenuto seguente e salvarlo tooyour computer.</span><span class="sxs-lookup"><span data-stu-id="f5524-183">Create a file named `calcapi.json` with following contents and save it tooyour computer.</span></span> <span data-ttu-id="f5524-184">Verificare che hello `host` attributo punta back-end Web API tooyour.</span><span class="sxs-lookup"><span data-stu-id="f5524-184">Ensure that hello `host` attribute points tooyour Web API backend.</span></span> <span data-ttu-id="f5524-185">In questo esempio viene usato `"host": "apimaaddemo.azurewebsites.net"` .</span><span class="sxs-lookup"><span data-stu-id="f5524-185">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span></span>

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

<span data-ttu-id="f5524-186">Calcolatrice hello tooimport API, fare clic su **API** da hello **gestione API** menu hello a sinistra e quindi fare clic su **importazione API**.</span><span class="sxs-lookup"><span data-stu-id="f5524-186">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![Pulsante Importa API][api-management-import-api]

<span data-ttu-id="f5524-188">Eseguire hello seguendo i passaggi tooconfigure hello calcolatrice API.</span><span class="sxs-lookup"><span data-stu-id="f5524-188">Perform hello following steps tooconfigure hello calculator API.</span></span>

1. <span data-ttu-id="f5524-189">Fare clic su **dal file**, Sfoglia toohello `calculator.json` file salvato e fare clic su hello **Swagger** pulsante di opzione.</span><span class="sxs-lookup"><span data-stu-id="f5524-189">Click **From file**, browse toohello `calculator.json` file you saved, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="f5524-190">Tipo **calc** in hello **suffisso URL di Web API** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="f5524-190">Type **calc** into hello **Web API URL suffix** textbox.</span></span>
3. <span data-ttu-id="f5524-191">Fare clic nella hello **prodotti (facoltativi)** e scegliere **Starter**.</span><span class="sxs-lookup"><span data-stu-id="f5524-191">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="f5524-192">Fare clic su **salvare** tooimport hello API.</span><span class="sxs-lookup"><span data-stu-id="f5524-192">Click **Save** tooimport hello API.</span></span>

![Add new API][api-management-import-new-api]

<span data-ttu-id="f5524-194">Una volta importato, hello API hello pagina Riepilogo per l'API di hello viene visualizzato nel portale di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f5524-194">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a><span data-ttu-id="f5524-195">Chiamare API hello correttamente dal portale per sviluppatori hello</span><span class="sxs-lookup"><span data-stu-id="f5524-195">Call hello API unsuccessfully from hello developer portal</span></span>
<span data-ttu-id="f5524-196">A questo punto, hello API è stata importata in Gestione API, ma può ancora essere chiamato correttamente dal portale per sviluppatori hello perché il servizio back-end hello è protetto con autenticazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5524-196">At this point, hello API has been imported into API Management, but cannot yet be called successfully from hello developer portal because hello backend service is protected with Azure AD authentication.</span></span> <span data-ttu-id="f5524-197">Come illustrato nel video hello a partire da 7:40 utilizzando hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="f5524-197">This is demonstrated in hello video starting at 7:40 using hello following steps.</span></span>

<span data-ttu-id="f5524-198">Fare clic su **portale per sviluppatori** dalla parte superiore destra hello del portale di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f5524-198">Click **Developer portal** from hello top-right side of hello publisher portal.</span></span>

![Portale per sviluppatori][api-management-developer-portal-menu]

<span data-ttu-id="f5524-200">Fare clic su **API** e fare clic su hello **Calcolatrice** API.</span><span class="sxs-lookup"><span data-stu-id="f5524-200">Click **APIs** and click hello **Calculator** API.</span></span>

![Portale per sviluppatori][api-management-dev-portal-apis]

<span data-ttu-id="f5524-202">Fare clic su **Prova**.</span><span class="sxs-lookup"><span data-stu-id="f5524-202">Click **Try it**.</span></span>

![Prova][api-management-dev-portal-try-it]

<span data-ttu-id="f5524-204">Fare clic su **inviare** e prendere nota di stato della risposta hello **401 non autorizzato**.</span><span class="sxs-lookup"><span data-stu-id="f5524-204">Click **Send** and note hello response status of **401 Unauthorized**.</span></span>

![Invio][api-management-dev-portal-send-401]

<span data-ttu-id="f5524-206">non è autorizzato richiesta Hello poiché API back-end hello è protetto da Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f5524-206">hello request is unauthorized because hello backend API is protected by Azure Active Directory.</span></span> <span data-ttu-id="f5524-207">Prima di esito positivo della chiamata API hello portale per sviluppatori hello deve essere configurato tooauthorize sviluppatori mediante OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="f5524-207">Before successfully calling hello API hello developer portal must be configured tooauthorize developers using OAuth 2.0.</span></span> <span data-ttu-id="f5524-208">Questo processo è descritto nelle seguenti sezioni hello.</span><span class="sxs-lookup"><span data-stu-id="f5524-208">This process is described in hello following sections.</span></span>

## <a name="register-hello-developer-portal-as-an-aad-application"></a><span data-ttu-id="f5524-209">Registrare il portale per sviluppatori di hello come un'applicazione AAD</span><span class="sxs-lookup"><span data-stu-id="f5524-209">Register hello developer portal as an AAD application</span></span>
<span data-ttu-id="f5524-210">primo passaggio di Hello nella configurazione gli sviluppatori di tooauthorize portale per sviluppatori hello mediante OAuth 2.0 è portale per sviluppatori di hello tooregister come un'applicazione AAD.</span><span class="sxs-lookup"><span data-stu-id="f5524-210">hello first step in configuring hello developer portal tooauthorize developers using OAuth 2.0 is tooregister hello developer portal as an AAD application.</span></span> <span data-ttu-id="f5524-211">A partire da 8:27 video hello illustrato.</span><span class="sxs-lookup"><span data-stu-id="f5524-211">This is demonstrated starting at 8:27 in hello video.</span></span>

<span data-ttu-id="f5524-212">Passare a tenant di Azure AD toohello innanzitutto hello del video, in questo esempio **APIMDemo** e passare toohello **applicazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="f5524-212">Navigate toohello Azure AD tenant from hello first step of this video, in this example **APIMDemo** and navigate toohello **Applications** tab.</span></span>

![Nuova applicazione][api-management-aad-new-application-devportal]

<span data-ttu-id="f5524-214">Fare clic su hello **Aggiungi** toocreate una nuova applicazione Azure Active Directory e scegliere **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.</span><span class="sxs-lookup"><span data-stu-id="f5524-214">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Nuova applicazione][api-management-new-aad-application-menu]

<span data-ttu-id="f5524-216">Scegliere **Web dell'applicazione e/o API Web**, immettere un nome e fare clic sulla freccia avanti hello.</span><span class="sxs-lookup"><span data-stu-id="f5524-216">Choose **Web application and/or Web API**, enter a name, and click hello next arrow.</span></span> <span data-ttu-id="f5524-217">In questo esempio viene usato **APIMDeveloperPortal** .</span><span class="sxs-lookup"><span data-stu-id="f5524-217">In this example **APIMDeveloperPortal** is used.</span></span>

![Nuova applicazione][api-management-aad-new-application-devportal-1]

<span data-ttu-id="f5524-219">Per **Sign-on URL** immettere hello URL del servizio Gestione API e aggiungere `/signin`.</span><span class="sxs-lookup"><span data-stu-id="f5524-219">For **Sign-on URL** enter hello URL of your API Management service and append `/signin`.</span></span> <span data-ttu-id="f5524-220">In questo esempio viene usato `https://contoso5.portal.azure-api.net/signin` .</span><span class="sxs-lookup"><span data-stu-id="f5524-220">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span></span>

<span data-ttu-id="f5524-221">Per **URL Id App** immettere hello URL del servizio Gestione API e aggiungere alcuni caratteri univoci.</span><span class="sxs-lookup"><span data-stu-id="f5524-221">For **App Id URL** enter hello URL of your API Management service and append some unique characters.</span></span> <span data-ttu-id="f5524-222">Si può usare qualsiasi carattere. In questo esempio vengono usati `https://contoso5.portal.azure-api.net/dp`.</span><span class="sxs-lookup"><span data-stu-id="f5524-222">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span></span> <span data-ttu-id="f5524-223">Quando lo si desidera hello **proprietà App** sono configurate, fare clic su un'applicazione hello toocreate hello segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="f5524-223">When hello  desired **App properties** are configured, click hello check mark toocreate hello application.</span></span>

![Nuova applicazione][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a><span data-ttu-id="f5524-225">Configurare un server autorizzazione OAuth 2.0 in Gestione API</span><span class="sxs-lookup"><span data-stu-id="f5524-225">Configure an API Management OAuth 2.0 authorization server</span></span>
<span data-ttu-id="f5524-226">passaggio successivo Hello è tooconfigure un server di autorizzazione OAuth 2.0 in Gestione API.</span><span class="sxs-lookup"><span data-stu-id="f5524-226">hello next step is tooconfigure an OAuth 2.0 authorization server in API Management.</span></span> <span data-ttu-id="f5524-227">Questo passaggio è illustrato in hello video a partire da 9:43.</span><span class="sxs-lookup"><span data-stu-id="f5524-227">This step is demonstrated in hello video starting at 9:43.</span></span>

<span data-ttu-id="f5524-228">Fare clic su **sicurezza** hello gestione API scegliere dal menu a sinistra di hello **OAuth 2.0**, quindi fare clic su **aggiungere autorizzazione** server.</span><span class="sxs-lookup"><span data-stu-id="f5524-228">Click **Security** from hello API Management menu on hello left, click **OAuth 2.0**, and then click **Add authorization** server.</span></span>

![Add authorization server][api-management-add-authorization-server]

<span data-ttu-id="f5524-230">Immettere un nome e una descrizione facoltativa in hello **nome** e **descrizione** campi.</span><span class="sxs-lookup"><span data-stu-id="f5524-230">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> <span data-ttu-id="f5524-231">Questi campi sono server di autorizzazione OAuth 2.0 hello tooidentify utilizzati nell'istanza del servizio Gestione API di hello.</span><span class="sxs-lookup"><span data-stu-id="f5524-231">These fields are used tooidentify hello OAuth 2.0 authorization server within hello API Management service instance.</span></span> <span data-ttu-id="f5524-232">In questo esempio viene usato **Authorization server demo** .</span><span class="sxs-lookup"><span data-stu-id="f5524-232">In this example **Authorization server demo** is used.</span></span> <span data-ttu-id="f5524-233">In un secondo momento quando si specifica un toobe server OAuth 2.0 utilizzata per l'autenticazione per un'API, si selezionerà il nome specificato.</span><span class="sxs-lookup"><span data-stu-id="f5524-233">Later when you specify an OAuth 2.0 server toobe used for authentication for an API, you will select this name.</span></span>

<span data-ttu-id="f5524-234">Per hello **URL pagina di registrazione Client** immettere un valore segnaposto, ad esempio `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="f5524-234">For hello **Client registration page URL** enter a placeholder value such as `http://localhost`.</span></span>  <span data-ttu-id="f5524-235">Hello **URL pagina di registrazione Client** punti toohello pagina che gli utenti possono utilizzare toocreate e configurare i propri account per i provider di OAuth 2.0 che supportano la gestione degli account utente.</span><span class="sxs-lookup"><span data-stu-id="f5524-235">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="f5524-236">In questo esempio gli utenti non creano e configurano i propri account, quindi si usa un segnaposto.</span><span class="sxs-lookup"><span data-stu-id="f5524-236">In this example users do not create and configure their own accounts so a placeholder is used.</span></span>

![Add authorization server][api-management-add-authorization-server-1]

<span data-ttu-id="f5524-238">Successivamente, specificare un valore per **Authorization endpoint URL** e **Token endpoint URL**.</span><span class="sxs-lookup"><span data-stu-id="f5524-238">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span></span>

![Serve autorizzazione][api-management-add-authorization-server-1a]

<span data-ttu-id="f5524-240">Questi valori possono essere recuperati da hello **endpoint dell'App** pagina dell'applicazione AAD creato per il portale per sviluppatori di hello hello.</span><span class="sxs-lookup"><span data-stu-id="f5524-240">These values can be retrieved from hello **App Endpoints** page of hello AAD application you created for hello developer portal.</span></span> <span data-ttu-id="f5524-241">gli endpoint hello tooaccess passare toohello **configura** per un'applicazione hello AAD scheda e fare clic su **visualizzare endpoint**.</span><span class="sxs-lookup"><span data-stu-id="f5524-241">tooaccess hello endpoints navigate toohello **Configure** tab for hello AAD application and click **View endpoints**.</span></span>

![Applicazione][api-management-aad-devportal-application]

![Visualizza endpoint][api-management-aad-view-endpoints]

<span data-ttu-id="f5524-244">Hello copia **endpoint di autorizzazione OAuth 2.0** e incollarlo in hello **autorizzazione URL dell'endpoint** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="f5524-244">Copy hello **OAuth 2.0 authorization endpoint** and paste it into hello **Authorization endpoint URL** textbox.</span></span>

![Add authorization server][api-management-add-authorization-server-2]

<span data-ttu-id="f5524-246">Hello copia **endpoint token OAuth 2.0** e incollarlo in hello **URL dell'endpoint del Token** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="f5524-246">Copy hello **OAuth 2.0 token endpoint** and paste it into hello **Token endpoint URL** textbox.</span></span>

![Add authorization server][api-management-add-authorization-server-2a]

<span data-ttu-id="f5524-248">Inoltre toopasting nell'endpoint token hello, aggiungere un parametro aggiuntivo corpo denominato **risorse** e per valore hello utilizzare hello **URI Id App** da hello applicazione AAD per il servizio back-end hello che è stato Quando è stato pubblicato il progetto di Visual Studio hello creata.</span><span class="sxs-lookup"><span data-stu-id="f5524-248">In addition toopasting in hello token endpoint, add an additional body parameter named **resource** and for hello value use hello **App Id URI** from hello AAD application for hello backend service that was created when hello Visual Studio project was published.</span></span>

![URI ID app][api-management-aad-sso-uri]

<span data-ttu-id="f5524-250">Successivamente, specificare le credenziali di hello del client.</span><span class="sxs-lookup"><span data-stu-id="f5524-250">Next, specify hello client credentials.</span></span> <span data-ttu-id="f5524-251">Queste sono le credenziali di hello per risorsa hello da tooaccess, in questo caso hello portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="f5524-251">These are hello credentials for hello resource you want tooaccess, in this case hello developer portal.</span></span>

![Credenziali del client][api-management-client-credentials]

<span data-ttu-id="f5524-253">hello tooget **Id Client**, passare toohello **configura** scheda di hello applicazione AAD per hello di portale e copia developer hello **Id Client**.</span><span class="sxs-lookup"><span data-stu-id="f5524-253">tooget hello **Client Id**, navigate toohello **Configure** tab of hello AAD application for hello developer portal and copy hello **Client Id**.</span></span>

<span data-ttu-id="f5524-254">hello tooget **segreto Client** fare clic su hello **Seleziona durata** menu a discesa hello **chiavi** sezione e specificare un intervallo.</span><span class="sxs-lookup"><span data-stu-id="f5524-254">tooget hello **Client Secret** click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="f5524-255">In questo esempio viene usato 1 anno.</span><span class="sxs-lookup"><span data-stu-id="f5524-255">In this example 1 year is used.</span></span>

![ID client][api-management-aad-client-id]

<span data-ttu-id="f5524-257">Fare clic su **salvare** chiave hello configurazione e la visualizzazione toosave hello.</span><span class="sxs-lookup"><span data-stu-id="f5524-257">Click **Save** toosave hello configuration and display hello key.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f5524-258">Annotare il valore relativo alla chiave.</span><span class="sxs-lookup"><span data-stu-id="f5524-258">Make a note of this key.</span></span> <span data-ttu-id="f5524-259">Quando si chiude una finestra di configurazione di hello Azure Active Directory, non è più visualizzata chiave hello.</span><span class="sxs-lookup"><span data-stu-id="f5524-259">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

<span data-ttu-id="f5524-260">Chiave hello toohello chiave negli Appunti Copia hello portale di pubblicazione toohello indietro di commutatore, incollare hello **segreto Client** casella di testo, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="f5524-260">Copy hello key toohello clipboard, switch back toohello publisher portal, paste hello key into hello **Client Secret** textbox, and click **Save**.</span></span>

![Add authorization server][api-management-add-authorization-server-3]

<span data-ttu-id="f5524-262">Subito dopo le credenziali del client hello è una concessione del codice di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="f5524-262">Immediately following hello client credentials is an authorization code grant.</span></span> <span data-ttu-id="f5524-263">Copiare questo codice di autorizzazione e switch back tooyour dell'applicazione del portale di Azure AD per sviluppatori pagina di configurazione e incollare la concessione di autorizzazione hello hello **URL di risposta** campo e fare clic su **salvare** nuovamente.</span><span class="sxs-lookup"><span data-stu-id="f5524-263">Copy this authorization code and switch back tooyour Azure AD developer portal application configure page, and paste hello authorization grant into hello **Reply URL** field, and click **Save** again.</span></span>

![URL di risposta][api-management-aad-reply-url]

<span data-ttu-id="f5524-265">passaggio successivo Hello è autorizzazioni hello tooconfigure per il portale per sviluppatori hello applicazione AAD.</span><span class="sxs-lookup"><span data-stu-id="f5524-265">hello next step is tooconfigure hello permissions for hello developer portal AAD application.</span></span> <span data-ttu-id="f5524-266">Fare clic su **autorizzazioni applicazione** e casella hello per **lettura dati directory**.</span><span class="sxs-lookup"><span data-stu-id="f5524-266">Click **Application Permissions** and check hello box for **Read directory data**.</span></span> <span data-ttu-id="f5524-267">Fare clic su **salvare** toosave questa modifica e quindi fare clic su **aggiungere applicazione**.</span><span class="sxs-lookup"><span data-stu-id="f5524-267">Click **Save** toosave this change, and then click **Add application**.</span></span>

![Aggiungere autorizzazioni][api-management-add-devportal-permissions]

<span data-ttu-id="f5524-269">Fare clic sull'icona di ricerca di hello, tipo **ruoli** in hello a partire dalla casella, selezionare **APIMAADDemo**, fare clic su hello toosave di segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="f5524-269">Click hello search icon, type **APIM** into hello Starting with box, select **APIMAADDemo**, and click hello check mark toosave.</span></span>

![Aggiungere autorizzazioni][api-management-aad-add-app-permissions]

<span data-ttu-id="f5524-271">Fare clic su **autorizzazioni delegate** per **APIMAADDemo** e casella hello per **accesso APIMAADDemo**, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="f5524-271">Click **Delegated Permissions** for **APIMAADDemo** and check hello box for **Access APIMAADDemo**, and click **Save**.</span></span> <span data-ttu-id="f5524-272">In questo modo developer hello servizio back-end di hello tooaccess dell'applicazione del portale.</span><span class="sxs-lookup"><span data-stu-id="f5524-272">This allows hello developer portal application tooaccess hello backend service.</span></span>

![Aggiungere autorizzazioni][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a><span data-ttu-id="f5524-274">Attivare l'autorizzazione utente OAuth 2.0 per hello API calcolatrice</span><span class="sxs-lookup"><span data-stu-id="f5524-274">Enable OAuth 2.0 user authorization for hello Calculator API</span></span>
<span data-ttu-id="f5524-275">Ora che hello OAuth 2.0 server è configurato, è possibile specificarla nelle impostazioni di sicurezza hello per le API.</span><span class="sxs-lookup"><span data-stu-id="f5524-275">Now that hello OAuth 2.0 server is configured, you can specify it in hello security settings for your API.</span></span> <span data-ttu-id="f5524-276">Questo passaggio è illustrato in hello video a partire da 14:30.</span><span class="sxs-lookup"><span data-stu-id="f5524-276">This step is demonstrated in hello video starting at 14:30.</span></span>

<span data-ttu-id="f5524-277">Fare clic su **API** in hello menu a sinistra, quindi fare clic su **Calcolatrice** tooview e configurare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="f5524-277">Click **APIs** in hello left menu, and click  **Calculator** tooview and configure its settings.</span></span>

![API Calculator][api-management-calc-api]

<span data-ttu-id="f5524-279">Passare toohello **sicurezza** scheda, controllare hello **OAuth 2.0** casella di controllo, il server di autorizzazione desiderato selezionare hello da hello **server autorizzazione** elenco a discesa e fare clic su **Salvare**.</span><span class="sxs-lookup"><span data-stu-id="f5524-279">Navigate toohello **Security** tab, check hello **OAuth 2.0** checkbox, select hello desired authorization server from hello **Authorization server** drop-down, and click **Save**.</span></span>

![API Calculator][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a><span data-ttu-id="f5524-281">Chiamare correttamente hello calcolatrice API dal portale per sviluppatori hello</span><span class="sxs-lookup"><span data-stu-id="f5524-281">Successfully call hello Calculator API from hello developer portal</span></span>
<span data-ttu-id="f5524-282">Ora che l'autorizzazione di OAuth 2.0 hello è configurata su hello API, le operazioni possono essere chiamate correttamente dal centro per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="f5524-282">Now that hello OAuth 2.0 authorization is configured on hello API, its operations can be successfully called from hello developer center.</span></span> <span data-ttu-id="f5524-283">Questo passaggio è illustrato in hello video a partire da 15:00.</span><span class="sxs-lookup"><span data-stu-id="f5524-283">THis step is demonstrated in hello video starting at 15:00.</span></span>

<span data-ttu-id="f5524-284">Spostarsi indietro toohello **aggiungere due numeri interi** operazione del servizio di calcolatrice hello nel portale per sviluppatori hello e fare clic su **provarla**.</span><span class="sxs-lookup"><span data-stu-id="f5524-284">Navigate back toohello **Add two integers** operation of hello calculator service in hello developer portal and click **Try it**.</span></span> <span data-ttu-id="f5524-285">Nuovo elemento hello nota in hello **autorizzazione** sezione appena aggiunto un server di autorizzazione toohello corrispondente.</span><span class="sxs-lookup"><span data-stu-id="f5524-285">Note hello new item in hello **Authorization** section corresponding toohello authorization server you just added.</span></span>

![API Calculator][api-management-calc-authorization-server]

<span data-ttu-id="f5524-287">Selezionare **codice di autorizzazione** dall'autorizzazione hello elenco a discesa elenco e immettere le credenziali di hello di hello account toouse.</span><span class="sxs-lookup"><span data-stu-id="f5524-287">Select **Authorization code** from hello authorization drop-down list and enter hello credentials of hello account toouse.</span></span> <span data-ttu-id="f5524-288">Se già eseguito l'accesso con account hello potrebbero non essere richieste.</span><span class="sxs-lookup"><span data-stu-id="f5524-288">If you are already signed in with hello account you may not be prompted.</span></span>

![API Calculator][api-management-devportal-authorization-code]

<span data-ttu-id="f5524-290">Fare clic su **inviare** e hello nota **stato della risposta** di **200 OK** e hello risultati dell'operazione di hello nel contenuto della risposta hello.</span><span class="sxs-lookup"><span data-stu-id="f5524-290">Click **Send** and note hello **Response status** of **200 OK** and hello results of hello operation in hello response content.</span></span>

![API Calculator][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a><span data-ttu-id="f5524-292">Configurare un hello toocall applicazione desktop API</span><span class="sxs-lookup"><span data-stu-id="f5524-292">Configure a desktop application toocall hello API</span></span>
<span data-ttu-id="f5524-293">procedura Hello in hello video inizia in corrispondenza di 16:30 e configura hello di toocall API una semplice applicazione desktop.</span><span class="sxs-lookup"><span data-stu-id="f5524-293">hello next procedure in hello video starts at 16:30 and configures a simple desktop application toocall hello API.</span></span> <span data-ttu-id="f5524-294">primo passaggio Hello è tooregister applicazione desktop di hello in Azure AD e assegnargli accesso toohello directory e toohello back-end del servizio.</span><span class="sxs-lookup"><span data-stu-id="f5524-294">hello first step is tooregister hello desktop application in Azure AD and give it access toohello directory and toohello backend service.</span></span> <span data-ttu-id="f5524-295">18:25 è una dimostrazione di un'applicazione desktop hello richiamare un'operazione su Calcolatrice hello API.</span><span class="sxs-lookup"><span data-stu-id="f5524-295">At 18:25 there is a demonstration of hello desktop application calling an operation on hello calculator API.</span></span>

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a><span data-ttu-id="f5524-296">Configurare un toopre di criteri di convalida JWT-autorizzare richieste</span><span class="sxs-lookup"><span data-stu-id="f5524-296">Configure a JWT validation policy toopre-authorize requests</span></span>
<span data-ttu-id="f5524-297">inizia da 20:48 Hello procedura finale nel video hello e illustra come hello toouse [convalidare JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) toopre criteri-autorizzare richieste convalidando i token di accesso hello di ogni richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="f5524-297">hello final procedure in hello video starts at 20:48 and shows you how toouse hello [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy toopre-authorize requests by validating hello access tokens of each incoming request.</span></span> <span data-ttu-id="f5524-298">Se è richiesta hello non vengono convalidato dai criteri di convalida JWT hello, richiesta hello è bloccato da Gestione API e viene passato non toohello di back-end.</span><span class="sxs-lookup"><span data-stu-id="f5524-298">If hello request is not validated by hello Validate JWT policy, hello request is blocked by API Management and is not passed along toohello backend.</span></span>

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

<span data-ttu-id="f5524-299">Per un altro dimostrazione della configurazione e l'utilizzo di questo criterio, vedere [Cloud coprire episodio 177: più le funzionalità di gestione API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e far avanzare rapidamente too13:50.</span><span class="sxs-lookup"><span data-stu-id="f5524-299">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="f5524-300">Avanzamento rapido too15:00 criteri hello toosee configurati nell'editor Criteri di hello e quindi too18:50 per una dimostrazione di chiamata di un'operazione dal portale per sviluppatori di hello con e senza hello necessari token di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="f5524-300">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5524-301">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f5524-301">Next steps</span></span>
* <span data-ttu-id="f5524-302">Altre informazioni sui [video](https://azure.microsoft.com/documentation/videos/index/?services=api-management) relativi a Gestione API.</span><span class="sxs-lookup"><span data-stu-id="f5524-302">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="f5524-303">Per altri modi toosecure servizio back-end, vedere [autenticazione reciproca del certificato](api-management-howto-mutual-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="f5524-303">For other ways toosecure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
