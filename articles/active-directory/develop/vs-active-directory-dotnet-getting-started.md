---
title: Introduzione ad Azure AD in progetti MVC di Visual Studio | Microsoft Docs
description: Come iniziare a utilizzare Azure Active Directory nei progetti MVC dopo la connessione o la creazione ad Azure AD utilizzando Visual Studio
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1c8b6a58-5144-4965-a905-625b9ee7b22b
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: c4d49cfc9887e422b3eaed2b96348c99eca48881
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-azure-active-directory-and-visual-studio-connected-services-mvc-projects"></a><span data-ttu-id="90672-103">Introduzione ad Azure Active Directory e ai servizi relativi a Visual Studio (progetti MVC)</span><span class="sxs-lookup"><span data-stu-id="90672-103">Getting Started with Azure Active Directory and Visual Studio connected services (MVC Projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="90672-104">Per iniziare</span><span class="sxs-lookup"><span data-stu-id="90672-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="90672-105">Risultati</span><span class="sxs-lookup"><span data-stu-id="90672-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="requiring-authentication-to-access-controllers"></a><span data-ttu-id="90672-106">Richiesta di autenticazione ai controller di accesso</span><span class="sxs-lookup"><span data-stu-id="90672-106">Requiring authentication to access controllers</span></span>
<span data-ttu-id="90672-107">Tutti i controller del progetto sono dotati dell'attributo **Authorize** .</span><span class="sxs-lookup"><span data-stu-id="90672-107">All controllers in your project were adorned with the **Authorize** attribute.</span></span> <span data-ttu-id="90672-108">Questo attributo richiede che l'utente venga autenticato prima di accedere ai controller.</span><span class="sxs-lookup"><span data-stu-id="90672-108">This attribute requires the user to be authenticated before accessing these controllers.</span></span> <span data-ttu-id="90672-109">Per permettere l'accesso anonimo al controller, rimuovere l'attributo dal controller.</span><span class="sxs-lookup"><span data-stu-id="90672-109">To allow the controller to be accessed anonymously, remove this attribute from the controller.</span></span> <span data-ttu-id="90672-110">Per configurare le autorizzazioni con un livello di granularità superiore, applicare l'attributo a ogni metodo che necessita di autorizzazione invece di applicarlo alla classe controller.</span><span class="sxs-lookup"><span data-stu-id="90672-110">If you want to set the permissions at a more granular level, apply the attribute to each method that requires authorization instead of applying it to the controller class.</span></span>

## <a name="adding-signin--signout-controls"></a><span data-ttu-id="90672-111">Aggiunta di controlli SignIn/SignOut</span><span class="sxs-lookup"><span data-stu-id="90672-111">Adding SignIn / SignOut Controls</span></span>
<span data-ttu-id="90672-112">Per aggiungere i controlli SignIn/SignOut alla visualizzazione, è possibile usare la visualizzazione parziale **_LoginPartial.cshtml** per aggiungere la funzionalità a una delle visualizzazioni.</span><span class="sxs-lookup"><span data-stu-id="90672-112">To add the SignIn/SignOut controls to your view, you can use the **_LoginPartial.cshtml** partial view to add the functionality to one of your views.</span></span> <span data-ttu-id="90672-113">L'esempio seguente illustra l'aggiunta di funzionalità alla visualizzazione **_Layout.cshtml** standard.</span><span class="sxs-lookup"><span data-stu-id="90672-113">Here is an example of the functionality added to the standard **_Layout.cshtml** view.</span></span> <span data-ttu-id="90672-114">(Notare l'ultimo elemento nella sezione div con class navbar-collapse):</span><span class="sxs-lookup"><span data-stu-id="90672-114">(Note the last element in the div with class navbar-collapse):</span></span>

<pre>
    &lt;!DOCTYPE html&gt; 
     &lt;html&gt; 
     &lt;head&gt; 
         &lt;meta charset="utf-8" /&gt; 
        &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt; 
        &lt;title&gt;@ViewBag.Title - My ASP.NET Application&lt;/title&gt; 
        @Styles.Render("~/Content/css") 
        @Scripts.Render("~/bundles/modernizr") 
    &lt;/head&gt; 
    &lt;body&gt; 
        &lt;div class="navbar navbar-inverse navbar-fixed-top"&gt; 
            &lt;div class="container"&gt; 
                &lt;div class="navbar-header"&gt; 
                    &lt;button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse"&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                    &lt;/button&gt; 
                    @Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" }) 
                &lt;/div&gt; 
                &lt;div class="navbar-collapse collapse"&gt; 
                    &lt;ul class="nav navbar-nav"&gt; 
                        &lt;li&gt;@Html.ActionLink("Home", "Index", "Home")&lt;/li&gt; 
                        &lt;li&gt;@Html.ActionLink("About", "About", "Home")&lt;/li&gt; 
                        &lt;li&gt;@Html.ActionLink("Contact", "Contact", "Home")&lt;/li&gt; 
                    &lt;/ul&gt; 
                    <span style="background-color:yellow">@Html.Partial("_LoginPartial")</span> 
                &lt;/div&gt; 
            &lt;/div&gt; 
        &lt;/div&gt; 
        &lt;div class="container body-content"&gt; 
            @RenderBody() 
            &lt;hr /&gt; 
            &lt;footer&gt; 
                &lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET Application&lt;/p&gt; 
            &lt;/footer&gt; 
        &lt;/div&gt; 
        @Scripts.Render("~/bundles/jquery") 
        @Scripts.Render("~/bundles/bootstrap") 
        @RenderSection("scripts", required: false) 
    &lt;/body&gt; 
    &lt;/html&gt;
</pre>

## <a name="next-steps"></a><span data-ttu-id="90672-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="90672-115">Next steps</span></span>
- [<span data-ttu-id="90672-116">Altre informazioni su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90672-116">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/) 

