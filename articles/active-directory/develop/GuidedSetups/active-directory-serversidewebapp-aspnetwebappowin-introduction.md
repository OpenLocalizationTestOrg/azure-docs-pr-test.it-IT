---
title: Introduzione al server Web ASP.NET per Azure AD v2 - Intro | Microsoft Docs
description: Implementazione di accessi Microsoft in una soluzione ASP.NET con un'applicazione tradizionale basata su Web browser tramite lo standard OpenID Connect
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 8062923b6270ec6253dc231a3db4333cf4666b42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-with-microsoft-to-an-aspnet-web-app"></a><span data-ttu-id="abf09-103">Aggiungere l'accesso con Microsoft a un'app Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="abf09-103">Add sign-in with Microsoft to an ASP.NET web app</span></span>

<span data-ttu-id="abf09-104">Questa guida illustra come implementare l'accesso con Microsoft usando una soluzione ASP.NET MVC con un'applicazione tradizionale basata su Web browser tramite OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="abf09-104">This guide demonstrates how to implement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="abf09-105">Al termine di questa guida, l'applicazione sarà in grado di accettare accessi sia di account personali (ad esempio, outlook.com, live.com e altri) sia di account aziendali o di istituti di istruzione di proprietà di aziende od organizzazioni con Azure Active Directory integrato.</span><span class="sxs-lookup"><span data-stu-id="abf09-105">At the end of this guide, your application will be able to accept sign ins of personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> 

> <span data-ttu-id="abf09-106">Questa guida richiede Visual Studio 2015 Update 3 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="abf09-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="abf09-107">Se non lo si ha, è possibile</span><span class="sxs-lookup"><span data-stu-id="abf09-107">Don’t have it?</span></span>  [<span data-ttu-id="abf09-108">scaricare Visual Studio 2017 gratuitamente</span><span class="sxs-lookup"><span data-stu-id="abf09-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="abf09-109">Come interpretare questa guida</span><span class="sxs-lookup"><span data-stu-id="abf09-109">How this guide works</span></span>

![Come interpretare questa guida](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

<span data-ttu-id="abf09-111">Questa guida si basa su uno scenario in cui un browser accede a un sito Web ASP.NET e chiede agli utenti di eseguire l'autenticazione tramite un pulsante di accesso.</span><span class="sxs-lookup"><span data-stu-id="abf09-111">This guide is based on the scenario where a browser accesses an ASP.NET web site, requesting a user to authenticate via a sign-in button.</span></span> <span data-ttu-id="abf09-112">In questo scenario, la maggior parte delle operazioni necessarie per il rendering della pagina Web viene eseguita sul lato server.</span><span class="sxs-lookup"><span data-stu-id="abf09-112">In this scenario, most of the work to render the web page occurs on the server side.</span></span>

## <a name="libraries"></a><span data-ttu-id="abf09-113">Librerie</span><span class="sxs-lookup"><span data-stu-id="abf09-113">Libraries</span></span>

<span data-ttu-id="abf09-114">Questa guida usa le librerie seguenti:</span><span class="sxs-lookup"><span data-stu-id="abf09-114">This guide uses the following libraries:</span></span>

|<span data-ttu-id="abf09-115">Libreria</span><span class="sxs-lookup"><span data-stu-id="abf09-115">Library</span></span>|<span data-ttu-id="abf09-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="abf09-116">Description</span></span>|
|---|---|
|[<span data-ttu-id="abf09-117">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="abf09-117">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="abf09-118">Middleware che consente a un'applicazione di usare OpenID Connect per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="abf09-118">Middleware that enables an application to use OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="abf09-119">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="abf09-119">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="abf09-120">Middleware che consente a un'applicazione di mantenere la sessione utente usando i cookie</span><span class="sxs-lookup"><span data-stu-id="abf09-120">Middleware that enables an application to maintain user session using cookies</span></span>|
|[<span data-ttu-id="abf09-121">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="abf09-121">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="abf09-122">Consente l'esecuzione in IIS di applicazioni basate su OWIN tramite la pipeline di richieste ASP.NET</span><span class="sxs-lookup"><span data-stu-id="abf09-122">Enables OWIN-based applications to run on IIS using the ASP.NET request pipeline</span></span>|

