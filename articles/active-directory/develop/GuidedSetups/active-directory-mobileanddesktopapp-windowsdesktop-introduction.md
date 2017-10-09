---
title: aaaAzure AD v2 Windows Desktop Getting Started - introduzione | Documenti Microsoft
description: Come applicazioni .NET per Windows Desktop (XAML) possono chiamare un'API che richiede token di accesso dall'endpoint di Azure Active Directory v2
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
ms.openlocfilehash: 89d98fc46190ba9e47b7c3095f91e32eca455fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a><span data-ttu-id="2425d-103">Chiamare hello Microsoft Graph API da un'app di Windows Desktop</span><span class="sxs-lookup"><span data-stu-id="2425d-103">Call hello Microsoft Graph API from a Windows Desktop app</span></span>

<span data-ttu-id="2425d-104">Questa guida dimostra come un'applicazione .NET per Windows Desktop (XAML) nativa può ottenere un token di accesso e chiamare l'API Microsoft Graph o altre API che richiedono token di accesso dall'endpoint di Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="2425d-104">This guide demonstrates how a native Windows Desktop .NET (XAML) application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="2425d-105">Alla fine di hello di questa Guida, l'applicazione verrà essere in grado di toocall un'API protetta utilizzando account personali (inclusi outlook.com, live.com e altri), nonché di lavoro e gli account dell'istituto di istruzione da qualsiasi società o organizzazione con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2425d-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

> <span data-ttu-id="2425d-106">Questa guida richiede Visual Studio 2015 Update 3 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2425d-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="2425d-107">Se non lo si ha, è possibile</span><span class="sxs-lookup"><span data-stu-id="2425d-107">Don’t have it?</span></span> [<span data-ttu-id="2425d-108">scaricare Visual Studio 2017 gratuitamente</span><span class="sxs-lookup"><span data-stu-id="2425d-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a><span data-ttu-id="2425d-109">Come interpretare questa guida</span><span class="sxs-lookup"><span data-stu-id="2425d-109">How this guide works</span></span>

![Come interpretare questa guida](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

<span data-ttu-id="2425d-111">applicazione di esempio Hello creata da questa Guida consente tooquery un'applicazione Desktop di Windows Microsoft Graph API o un'API Web che accetta i token dall'endpoint di Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="2425d-111">hello sample application created by this guide enables a Windows Desktop Application tooquery Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="2425d-112">Per questo scenario, un token viene aggiunto tooHTTP richieste tramite l'intestazione di autorizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="2425d-112">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="2425d-113">Acquisizione del token e il rinnovo viene gestita da hello libreria di autenticazione di Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="2425d-113">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="2425d-114">Gestione dell'acquisizione di token per l'accesso ad API Web protette</span><span class="sxs-lookup"><span data-stu-id="2425d-114">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="2425d-115">Dopo l'autenticazione utente hello, applicazione di esempio hello riceve un token che può essere utilizzato tooquery Microsoft Graph API o un'API Web protetta da Microsoft Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="2425d-115">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="2425d-116">API, ad esempio Microsoft Graph richiedono un tooallow token di accesso sull'accesso alle risorse specifiche – tooread, ad esempio, un profilo utente, del calendario dell'utente di accedere o inviare un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="2425d-116">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="2425d-117">L'applicazione può richiedere un token di accesso usando MSAL tooaccess queste risorse specificando gli ambiti di API.</span><span class="sxs-lookup"><span data-stu-id="2425d-117">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="2425d-118">Questo token di accesso viene quindi aggiunto toohello intestazione autorizzazione HTTP per ogni chiamata effettuata hello la risorsa protetta.</span><span class="sxs-lookup"><span data-stu-id="2425d-118">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="2425d-119">La memorizzazione nella cache e l'aggiornamento dei token di accesso vengono gestiti dalla libreria MSAL e non devono quindi essere effettuati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2425d-119">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="2425d-120">Pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="2425d-120">NuGet Packages</span></span>

<span data-ttu-id="2425d-121">Questa Guida Usa hello pacchetti NuGet seguenti:</span><span class="sxs-lookup"><span data-stu-id="2425d-121">This guide uses hello following NuGet packages:</span></span>

|<span data-ttu-id="2425d-122">Libreria</span><span class="sxs-lookup"><span data-stu-id="2425d-122">Library</span></span>|<span data-ttu-id="2425d-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2425d-123">Description</span></span>|
|---|---|
|[<span data-ttu-id="2425d-124">Microsoft.Identity.Client</span><span class="sxs-lookup"><span data-stu-id="2425d-124">Microsoft.Identity.Client</span></span>](https://www.nuget.org/packages/Microsoft.Identity.Client)|<span data-ttu-id="2425d-125">Microsoft Authentication Library (MSAL)</span><span class="sxs-lookup"><span data-stu-id="2425d-125">Microsoft Authentication Library (MSAL)</span></span>|

