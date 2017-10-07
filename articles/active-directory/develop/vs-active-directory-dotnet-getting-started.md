---
title: aaaGet avviato con Azure AD nei progetti di Visual Studio MVC | Documenti Microsoft
description: "La modalità di avvio tramite Azure Active Directory nei progetti MVC dopo la creazione di un annuncio di Azure con Visual Studio tooor connessione tooget servizi connessi"
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
ms.openlocfilehash: 807824dd6e4e57e443f8a7322cf2e5326384316d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-and-visual-studio-connected-services-mvc-projects"></a>Introduzione ad Azure Active Directory e ai servizi relativi a Visual Studio (progetti MVC)
> [!div class="op_single_selector"]
> * [Per iniziare](vs-active-directory-dotnet-getting-started.md)
> * [Risultati](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="requiring-authentication-tooaccess-controllers"></a>Controller di tooaccess che richiede l'autenticazione
Tutti i controller nel progetto sono state decorare con hello **Authorize** attributo. Questo attributo richiede hello utente toobe autenticato prima di accedere a questi controller. tooallow hello controller toobe accedere in modo anonimo, rimuovere questo attributo dal controller hello. Se si desidera che le autorizzazioni hello tooset a un livello più granulare, applicare hello attributo tooeach (metodo) che richiede l'autorizzazione anziché applicarla classe controller toohello.

## <a name="adding-signin--signout-controls"></a>Aggiunta di controlli SignIn/SignOut
hello tooadd accesso/disconnessione controlla tooyour vista, è possibile usare hello **loginpartial. cshtml** visualizzazione parziale tooadd hello funzionalità tooone le viste. Di seguito è riportato un esempio dello standard toohello aggiunta di funzionalità hello **layout. cshtml** visualizzazione. (Nota hello ultimo elemento div hello con classe barra di spostamento e compressione):

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

## <a name="next-steps"></a>Passaggi successivi
- [Altre informazioni su Azure Active Directory](https://azure.microsoft.com/services/active-directory/) 

