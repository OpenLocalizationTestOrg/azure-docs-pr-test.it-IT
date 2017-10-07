---
title: errori di toodiagnose aaaHow con hello connessione guidata di Azure Active Directory
description: Connessione guidata di active directory Hello ha rilevato un tipo di autenticazione incompatibile
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
ms.openlocfilehash: f71c5b41457c0c8db05042e8d5f723e58ad11844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a><span data-ttu-id="5bf60-103">Diagnostica degli errori con hello connessione guidata di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bf60-103">Diagnosing errors with hello Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="5bf60-104">Durante il rilevamento precedente codice di autenticazione, hello rilevato un tipo di autenticazione incompatibile.</span><span class="sxs-lookup"><span data-stu-id="5bf60-104">While detecting previous authentication code, hello wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="5bf60-105">Elementi verificati</span><span class="sxs-lookup"><span data-stu-id="5bf60-105">What is being checked?</span></span>
<span data-ttu-id="5bf60-106">**Nota:** toocorrectly rilevare precedente codice di autenticazione in un progetto, è necessario compilare il progetto hello.</span><span class="sxs-lookup"><span data-stu-id="5bf60-106">**Note:** toocorrectly detect previous authentication code in a project, hello project must be built.</span></span>  <span data-ttu-id="5bf60-107">Se si è verificato questo errore e non si ha il precedente codice di autenticazione del progetto, ricompilare e riprovare.</span><span class="sxs-lookup"><span data-stu-id="5bf60-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="5bf60-108">Tipi di progetto</span><span class="sxs-lookup"><span data-stu-id="5bf60-108">Project Types</span></span>
<span data-ttu-id="5bf60-109">procedura guidata di Hello controlla il tipo di hello di progetto che si sviluppa in modo è possibile inserire la logica di autenticazione appropriato hello nel progetto di hello.</span><span class="sxs-lookup"><span data-stu-id="5bf60-109">hello wizard checks hello type of project you’re developing so it can inject hello right authentication logic into hello project.</span></span>  <span data-ttu-id="5bf60-110">Se è presente alcun controller che deriva da `ApiController` nel progetto hello progetto hello viene considerato un progetto WebAPI.</span><span class="sxs-lookup"><span data-stu-id="5bf60-110">If there is any controller that derives from `ApiController` in hello project, hello project is considered a WebAPI project.</span></span>  <span data-ttu-id="5bf60-111">Se sono presenti solo i controller che derivano da `MVC.Controller` nel progetto hello progetto hello viene considerato un progetto MVC.</span><span class="sxs-lookup"><span data-stu-id="5bf60-111">If there are only controllers that derive from `MVC.Controller` in hello project, hello project is considered an MVC project.</span></span>  <span data-ttu-id="5bf60-112">Qualsiasi altro elemento non è supportato dalla procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="5bf60-112">Anything else is not supported by hello wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="5bf60-113">Codice di autenticazione compatibile</span><span class="sxs-lookup"><span data-stu-id="5bf60-113">Compatible Authentication Code</span></span>
<span data-ttu-id="5bf60-114">la procedura guidata Hello verifica inoltre le impostazioni di autenticazione che sono state configurate in precedenza con la procedura guidata hello o compatibili con la procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="5bf60-114">hello wizard also checks for authentication settings that have been previously configured with hello wizard or are compatible with hello wizard.</span></span>  <span data-ttu-id="5bf60-115">Se tutte le impostazioni sono presenti, viene considerato un caso rientrante, verrà visualizzata la procedura guidata hello impostazioni visualizzazione e hello.</span><span class="sxs-lookup"><span data-stu-id="5bf60-115">If all settings are present, it is considered a re-entrant case, and hello wizard opens display hello settings.</span></span>  <span data-ttu-id="5bf60-116">Se solo alcune delle impostazioni di hello sono presenti, viene considerato un caso di errore.</span><span class="sxs-lookup"><span data-stu-id="5bf60-116">If only some of hello settings are present, it is considered an error case.</span></span>

<span data-ttu-id="5bf60-117">In un progetto MVC, la procedura guidata hello verifica una delle seguenti impostazioni, derivanti dall'utilizzo precedente della procedura guidata hello hello:</span><span class="sxs-lookup"><span data-stu-id="5bf60-117">In an MVC project, hello wizard checks for any of hello following settings, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="5bf60-118">Inoltre, la procedura guidata hello controlla per una delle seguenti impostazioni in un progetto di Web API, derivanti dall'utilizzo precedente della procedura guidata hello hello:</span><span class="sxs-lookup"><span data-stu-id="5bf60-118">In addition, hello wizard checks for any of hello following settings in a Web API project, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="5bf60-119">Codice di autenticazione incompatibile</span><span class="sxs-lookup"><span data-stu-id="5bf60-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="5bf60-120">Infine, la procedura guidata hello tenta versioni toodetect di codice di autenticazione che sono state configurate con le versioni precedenti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5bf60-120">Finally, hello wizard attempts toodetect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="5bf60-121">Se si riceve questo errore, significa che il progetto contiene un tipo di autenticazione non compatibile.</span><span class="sxs-lookup"><span data-stu-id="5bf60-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="5bf60-122">la procedura guidata Hello rileva hello seguenti tipi di autenticazione da versioni precedenti di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="5bf60-122">hello wizard detects hello following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="5bf60-123">Autenticazione di Windows</span><span class="sxs-lookup"><span data-stu-id="5bf60-123">Windows Authentication</span></span> 
* <span data-ttu-id="5bf60-124">Account utente singoli</span><span class="sxs-lookup"><span data-stu-id="5bf60-124">Individual User Accounts</span></span> 
* <span data-ttu-id="5bf60-125">Account dell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="5bf60-125">Organizational Accounts</span></span> 

<span data-ttu-id="5bf60-126">toodetect l'autenticazione di Windows in un progetto MVC, hello guidata viene cercato hello `authentication` elemento il **Web. config** file.</span><span class="sxs-lookup"><span data-stu-id="5bf60-126">toodetect Windows Authentication in an MVC project, hello wizard looks for hello `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="5bf60-127">toodetect l'autenticazione di Windows in un progetto di Web API, hello guidata viene cercato hello `IISExpressWindowsAuthentication` elemento nel progetto **csproj** file:</span><span class="sxs-lookup"><span data-stu-id="5bf60-127">toodetect Windows Authentication in a Web API project, hello wizard looks for hello `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="5bf60-128">l'autenticazione di account utente toodetect, hello guidata viene cercato elemento pacchetto hello il **Packages** file.</span><span class="sxs-lookup"><span data-stu-id="5bf60-128">toodetect Individual User Accounts authentication, hello wizard looks for hello package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="5bf60-129">toodetect un vecchio modulo di autenticazione Account aziendale, hello guidata viene cercato hello che seguono l'elemento da **Web. config**:</span><span class="sxs-lookup"><span data-stu-id="5bf60-129">toodetect an old form of Organizational Account authentication, hello wizard looks for hello following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="5bf60-130">tipo di autenticazione hello toochange, rimuovere il tipo di autenticazione incompatibile hello e rieseguire la procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="5bf60-130">toochange hello authentication type, remove hello incompatible authentication type and run hello wizard again.</span></span>

<span data-ttu-id="5bf60-131">Per altre informazioni, vedere [Scenari di autenticazione per Azure AD](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="5bf60-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="5bf60-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5bf60-132">Next steps</span></span>
- [<span data-ttu-id="5bf60-133">Scenari di autenticazione per Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bf60-133">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)