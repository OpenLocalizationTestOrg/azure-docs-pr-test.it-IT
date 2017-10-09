---
title: aaaAzure AD v2 ASP.NET Web Server Getting Started - introduzione | Documenti Microsoft
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
ms.openlocfilehash: d6449926af2bdad24cbc8e91f74885a08f909103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a><span data-ttu-id="9a028-103">Aggiungere Accedi con l'app web ASP.NET di Microsoft tooan</span><span class="sxs-lookup"><span data-stu-id="9a028-103">Add sign-in with Microsoft tooan ASP.NET web app</span></span>

<span data-ttu-id="9a028-104">Questa guida illustra come tooimplement Accedi con Microsoft tramite una soluzione di MVC ASP.NET con un'applicazione web tradizionale basato su browser con OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="9a028-104">This guide demonstrates how tooimplement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="9a028-105">Alla fine di hello di questa Guida, l'applicazione verrà tooaccept in grado di accesso aggiuntivi del personale account (inclusi outlook.com, live.com e altri), nonché di lavoro e gli account da qualsiasi società o organizzazione che è integrato con Azure Active Directory dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="9a028-105">At hello end of this guide, your application will be able tooaccept sign ins of personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> 

> <span data-ttu-id="9a028-106">Questa guida richiede Visual Studio 2015 Update 3 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9a028-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="9a028-107">Se non lo si ha, è possibile</span><span class="sxs-lookup"><span data-stu-id="9a028-107">Don’t have it?</span></span>  [<span data-ttu-id="9a028-108">scaricare Visual Studio 2017 gratuitamente</span><span class="sxs-lookup"><span data-stu-id="9a028-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="9a028-109">Come interpretare questa guida</span><span class="sxs-lookup"><span data-stu-id="9a028-109">How this guide works</span></span>

![Come interpretare questa guida](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

<span data-ttu-id="9a028-111">Questa guida si basa sullo scenario hello in un browser accede a un sito web ASP.NET, che richiede un tooauthenticate utente tramite un pulsante Accedi.</span><span class="sxs-lookup"><span data-stu-id="9a028-111">This guide is based on hello scenario where a browser accesses an ASP.NET web site, requesting a user tooauthenticate via a sign-in button.</span></span> <span data-ttu-id="9a028-112">In questo scenario, la maggior parte della pagina web di hello lavoro toorender hello si verifica sul lato server hello.</span><span class="sxs-lookup"><span data-stu-id="9a028-112">In this scenario, most of hello work toorender hello web page occurs on hello server side.</span></span>

## <a name="libraries"></a><span data-ttu-id="9a028-113">Librerie</span><span class="sxs-lookup"><span data-stu-id="9a028-113">Libraries</span></span>

<span data-ttu-id="9a028-114">Questa Guida Usa hello librerie seguenti:</span><span class="sxs-lookup"><span data-stu-id="9a028-114">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="9a028-115">Libreria</span><span class="sxs-lookup"><span data-stu-id="9a028-115">Library</span></span>|<span data-ttu-id="9a028-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9a028-116">Description</span></span>|
|---|---|
|[<span data-ttu-id="9a028-117">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="9a028-117">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="9a028-118">Middleware che consente a un toouse applicazione OpenIdConnect per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="9a028-118">Middleware that enables an application toouse OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="9a028-119">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="9a028-119">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="9a028-120">Middleware che consente a una sessione di utente toomaintain dell'applicazione utilizzando i cookie</span><span class="sxs-lookup"><span data-stu-id="9a028-120">Middleware that enables an application toomaintain user session using cookies</span></span>|
|[<span data-ttu-id="9a028-121">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="9a028-121">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="9a028-122">Consente di applicazioni basate su OWIN toorun in IIS utilizzando la pipeline delle richieste ASP.NET hello</span><span class="sxs-lookup"><span data-stu-id="9a028-122">Enables OWIN-based applications toorun on IIS using hello ASP.NET request pipeline</span></span>|

