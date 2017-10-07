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
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a>Diagnostica degli errori con hello connessione guidata di Azure Active Directory
Durante il rilevamento precedente codice di autenticazione, hello rilevato un tipo di autenticazione incompatibile.   

## <a name="what-is-being-checked"></a>Elementi verificati
**Nota:** toocorrectly rilevare precedente codice di autenticazione in un progetto, è necessario compilare il progetto hello.  Se si è verificato questo errore e non si ha il precedente codice di autenticazione del progetto, ricompilare e riprovare.

### <a name="project-types"></a>Tipi di progetto
procedura guidata di Hello controlla il tipo di hello di progetto che si sviluppa in modo è possibile inserire la logica di autenticazione appropriato hello nel progetto di hello.  Se è presente alcun controller che deriva da `ApiController` nel progetto hello progetto hello viene considerato un progetto WebAPI.  Se sono presenti solo i controller che derivano da `MVC.Controller` nel progetto hello progetto hello viene considerato un progetto MVC.  Qualsiasi altro elemento non è supportato dalla procedura guidata hello.

### <a name="compatible-authentication-code"></a>Codice di autenticazione compatibile
la procedura guidata Hello verifica inoltre le impostazioni di autenticazione che sono state configurate in precedenza con la procedura guidata hello o compatibili con la procedura guidata hello.  Se tutte le impostazioni sono presenti, viene considerato un caso rientrante, verrà visualizzata la procedura guidata hello impostazioni visualizzazione e hello.  Se solo alcune delle impostazioni di hello sono presenti, viene considerato un caso di errore.

In un progetto MVC, la procedura guidata hello verifica una delle seguenti impostazioni, derivanti dall'utilizzo precedente della procedura guidata hello hello:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

Inoltre, la procedura guidata hello controlla per una delle seguenti impostazioni in un progetto di Web API, derivanti dall'utilizzo precedente della procedura guidata hello hello:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a>Codice di autenticazione incompatibile
Infine, la procedura guidata hello tenta versioni toodetect di codice di autenticazione che sono state configurate con le versioni precedenti di Visual Studio. Se si riceve questo errore, significa che il progetto contiene un tipo di autenticazione non compatibile. la procedura guidata Hello rileva hello seguenti tipi di autenticazione da versioni precedenti di Visual Studio:

* Autenticazione di Windows 
* Account utente singoli 
* Account dell'organizzazione 

toodetect l'autenticazione di Windows in un progetto MVC, hello guidata viene cercato hello `authentication` elemento il **Web. config** file.

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

toodetect l'autenticazione di Windows in un progetto di Web API, hello guidata viene cercato hello `IISExpressWindowsAuthentication` elemento nel progetto **csproj** file:

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

l'autenticazione di account utente toodetect, hello guidata viene cercato elemento pacchetto hello il **Packages** file.

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

toodetect un vecchio modulo di autenticazione Account aziendale, hello guidata viene cercato hello che seguono l'elemento da **Web. config**:

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

tipo di autenticazione hello toochange, rimuovere il tipo di autenticazione incompatibile hello e rieseguire la procedura guidata hello.

Per altre informazioni, vedere [Scenari di autenticazione per Azure AD](active-directory-authentication-scenarios.md).

#<a name="next-steps"></a>Passaggi successivi
- [Scenari di autenticazione per Azure AD](active-directory-authentication-scenarios.md)