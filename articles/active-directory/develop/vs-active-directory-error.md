---
title: Come diagnosticare gli errori con Connessione guidata di Azure Active Directory
description: La procedura guidata di connessione di Active Directory ha rilevato un tipo di autenticazione incompatibile.
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/05/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 4f29f62b2996cae98b02c1ed5fcb59eca09301ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="diagnosing-errors-with-the-azure-active-directory-connection-wizard"></a><span data-ttu-id="9eb70-103">Diagnosi degli errori con Connessione guidata di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9eb70-103">Diagnosing errors with the Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="9eb70-104">Durante il rilevamento di codice di autenticazione precedente, la procedura guidata ha rilevato un tipo di autenticazione non compatibile.</span><span class="sxs-lookup"><span data-stu-id="9eb70-104">While detecting previous authentication code, the wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="9eb70-105">Elementi verificati</span><span class="sxs-lookup"><span data-stu-id="9eb70-105">What is being checked?</span></span>
<span data-ttu-id="9eb70-106">**Nota:** per rilevare correttamente il precedente codice di autenticazione in un progetto, è necessario che il progetto sia compilato.</span><span class="sxs-lookup"><span data-stu-id="9eb70-106">**Note:** To correctly detect previous authentication code in a project, the project must be built.</span></span>  <span data-ttu-id="9eb70-107">Se si è verificato questo errore e non si ha il precedente codice di autenticazione del progetto, ricompilare e riprovare.</span><span class="sxs-lookup"><span data-stu-id="9eb70-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="9eb70-108">Tipi di progetto</span><span class="sxs-lookup"><span data-stu-id="9eb70-108">Project Types</span></span>
<span data-ttu-id="9eb70-109">La procedura guidata verifica il tipo di progetto in corso di sviluppo, in modo da potervi inserire la logica di autenticazione corretta.</span><span class="sxs-lookup"><span data-stu-id="9eb70-109">The wizard checks the type of project you’re developing so it can inject the right authentication logic into the project.</span></span>  <span data-ttu-id="9eb70-110">Se nel progetto è presente un controller che deriva da `ApiController`, il progetto verrà considerato come un progetto WebAPI.</span><span class="sxs-lookup"><span data-stu-id="9eb70-110">If there is any controller that derives from `ApiController` in the project, the project is considered a WebAPI project.</span></span>  <span data-ttu-id="9eb70-111">Se nel progetto sono presenti solo controller che derivano da `MVC.Controller`, il progetto verrà considerato come un progetto MVC.</span><span class="sxs-lookup"><span data-stu-id="9eb70-111">If there are only controllers that derive from `MVC.Controller` in the project, the project is considered an MVC project.</span></span>  <span data-ttu-id="9eb70-112">Qualsiasi altro elemento non è supportato dalla procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="9eb70-112">Anything else is not supported by the wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="9eb70-113">Codice di autenticazione compatibile</span><span class="sxs-lookup"><span data-stu-id="9eb70-113">Compatible Authentication Code</span></span>
<span data-ttu-id="9eb70-114">La procedura guidata cerca inoltre le impostazioni di autenticazione configurate in precedenza o che sono compatibili.</span><span class="sxs-lookup"><span data-stu-id="9eb70-114">The wizard also checks for authentication settings that have been previously configured with the wizard or are compatible with the wizard.</span></span>  <span data-ttu-id="9eb70-115">Se sono presenti tutte le impostazioni, viene considerato come caso rientrante. La procedura guidata verrà aperta e visualizzerà le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="9eb70-115">If all settings are present, it is considered a re-entrant case, and the wizard opens display the settings.</span></span>  <span data-ttu-id="9eb70-116">Se sono presenti solo alcune impostazioni, verrà considerato come caso di errore.</span><span class="sxs-lookup"><span data-stu-id="9eb70-116">If only some of the settings are present, it is considered an error case.</span></span>

<span data-ttu-id="9eb70-117">In un progetto MVC la procedura guidata cerca le impostazioni seguenti che derivano da usi precedenti della procedura guidata:</span><span class="sxs-lookup"><span data-stu-id="9eb70-117">In an MVC project, the wizard checks for any of the following settings, which result from previous use of the wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="9eb70-118">La procedura guidata cerca inoltre le impostazioni seguenti di un progetto API Web che derivano da usi precedenti della procedura guidata:</span><span class="sxs-lookup"><span data-stu-id="9eb70-118">In addition, the wizard checks for any of the following settings in a Web API project, which result from previous use of the wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="9eb70-119">Codice di autenticazione incompatibile</span><span class="sxs-lookup"><span data-stu-id="9eb70-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="9eb70-120">La procedura guidata prova infine a rilevare le versioni del codice di autenticazione configurate con le versioni precedenti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9eb70-120">Finally, the wizard attempts to detect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="9eb70-121">Se si riceve questo errore, significa che il progetto contiene un tipo di autenticazione non compatibile.</span><span class="sxs-lookup"><span data-stu-id="9eb70-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="9eb70-122">La procedura guidata rileva i tipi seguenti di autenticazione dalle versioni precedenti di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="9eb70-122">The wizard detects the following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="9eb70-123">Autenticazione di Windows</span><span class="sxs-lookup"><span data-stu-id="9eb70-123">Windows Authentication</span></span> 
* <span data-ttu-id="9eb70-124">Account utente singoli</span><span class="sxs-lookup"><span data-stu-id="9eb70-124">Individual User Accounts</span></span> 
* <span data-ttu-id="9eb70-125">Account dell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="9eb70-125">Organizational Accounts</span></span> 

<span data-ttu-id="9eb70-126">Per individuare Autenticazione di Windows in un progetto MVC, la procedura guidata cerca l'elemento `authentication` nel file **web.config** .</span><span class="sxs-lookup"><span data-stu-id="9eb70-126">To detect Windows Authentication in an MVC project, the wizard looks for the `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="9eb70-127">Per individuare Autenticazione di Windows in un progetto API Web, la procedura guidata cerca l'elemento `IISExpressWindowsAuthentication` nel file con estensione **csproj** del progetto:</span><span class="sxs-lookup"><span data-stu-id="9eb70-127">To detect Windows Authentication in a Web API project, the wizard looks for the `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="9eb70-128">Per individuare l'autenticazione per singoli account utente, la procedura guidata cerca l'elemento package dal file **Packages.config** .</span><span class="sxs-lookup"><span data-stu-id="9eb70-128">To detect Individual User Accounts authentication, the wizard looks for the package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="9eb70-129">Per individuare una precedente forma di autenticazione di tipo account aziendale, la procedura guidata cerca il seguente elemento dal file **web.config**:</span><span class="sxs-lookup"><span data-stu-id="9eb70-129">To detect an old form of Organizational Account authentication, the wizard looks for the following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="9eb70-130">Per cambiare il tipo di autenticazione, rimuovere il tipo non compatibile ed eseguire di nuovo la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="9eb70-130">To change the authentication type, remove the incompatible authentication type and run the wizard again.</span></span>

<span data-ttu-id="9eb70-131">Per altre informazioni, vedere [Scenari di autenticazione per Azure AD](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="9eb70-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="9eb70-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9eb70-132">Next steps</span></span>
- [<span data-ttu-id="9eb70-133">Scenari di autenticazione per Azure AD</span><span class="sxs-lookup"><span data-stu-id="9eb70-133">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)