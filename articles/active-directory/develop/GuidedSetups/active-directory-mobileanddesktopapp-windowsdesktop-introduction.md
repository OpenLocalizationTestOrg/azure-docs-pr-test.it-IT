---
title: Introduzione a Windows Desktop per Azure AD v2 - Intro | Microsoft Docs
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
ms.openlocfilehash: 4a695c00fce4deb02261ba58ec95469746bb1486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="call-the-microsoft-graph-api-from-a-windows-desktop-app"></a><span data-ttu-id="e35ff-103">Chiamare l'API Microsoft Graph da un'app Windows Desktop</span><span class="sxs-lookup"><span data-stu-id="e35ff-103">Call the Microsoft Graph API from a Windows Desktop app</span></span>

<span data-ttu-id="e35ff-104">Questa guida dimostra come un'applicazione .NET per Windows Desktop (XAML) nativa può ottenere un token di accesso e chiamare l'API Microsoft Graph o altre API che richiedono token di accesso dall'endpoint di Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="e35ff-104">This guide demonstrates how a native Windows Desktop .NET (XAML) application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="e35ff-105">Al termine di questa guida, l'applicazione sarà in grado di chiamare un'API protetta usando sia account personali (ad esempio, outlook.com, live.com e altri) sia account aziendali o di istituti di istruzione di proprietà di aziende o organizzazioni con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e35ff-105">At the end of this guide, your application will be able to call a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

> <span data-ttu-id="e35ff-106">Questa guida richiede Visual Studio 2015 Update 3 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e35ff-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="e35ff-107">Se non lo si ha, è possibile</span><span class="sxs-lookup"><span data-stu-id="e35ff-107">Don’t have it?</span></span> [<span data-ttu-id="e35ff-108">scaricare Visual Studio 2017 gratuitamente</span><span class="sxs-lookup"><span data-stu-id="e35ff-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a><span data-ttu-id="e35ff-109">Come interpretare questa guida</span><span class="sxs-lookup"><span data-stu-id="e35ff-109">How this guide works</span></span>

![Come interpretare questa guida](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

<span data-ttu-id="e35ff-111">L'applicazione di esempio creata in questa guida consente a un'applicazione per Windows Desktop di eseguire query nell'API Microsoft Graph o in un'API Web che accetta token dall'endpoint di Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="e35ff-111">The sample application created by this guide enables a Windows Desktop Application to query Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="e35ff-112">Per questo scenario, viene aggiunto un token a richieste HTTP tramite l'intestazione di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="e35ff-112">For this scenario, a token is added to HTTP requests via the Authorization header.</span></span> <span data-ttu-id="e35ff-113">L'acquisizione e il rinnovo del token vengono gestiti da Microsoft Authentication Library (MSAL).</span><span class="sxs-lookup"><span data-stu-id="e35ff-113">Token acquisition and renewal is handled by the Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="e35ff-114">Gestione dell'acquisizione di token per l'accesso ad API Web protette</span><span class="sxs-lookup"><span data-stu-id="e35ff-114">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="e35ff-115">Dopo che l'utente ha eseguito l'autenticazione, l'applicazione di esempio riceve un token che può essere usato per eseguire query nell'API Microsoft Graph o in un'API Web protetta da Microsoft Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="e35ff-115">After the user authenticates, the sample application receives a token that can be used to query Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="e35ff-116">API come Microsoft Graph richiedono un token di accesso per consentire l'accesso a risorse specifiche, ad esempio per leggere un profilo utente, accedere al calendario dell'utente o inviare un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="e35ff-116">APIs such as Microsoft Graph require an access token to allow accessing specific resources – for example, to read a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="e35ff-117">L'applicazione può richiedere un token di accesso usando la libreria MSAL per accedere alle risorse tramite la definizione di ambiti API.</span><span class="sxs-lookup"><span data-stu-id="e35ff-117">Your application can request an access token using MSAL to access these resources by specifying API scopes.</span></span> <span data-ttu-id="e35ff-118">Il token di accesso ottenuto viene quindi aggiunto all'intestazione di autorizzazione HTTP per ogni chiamata effettuata alla risorsa protetta.</span><span class="sxs-lookup"><span data-stu-id="e35ff-118">This access token is then added to the HTTP Authorization header for every call made against the protected resource.</span></span> 

<span data-ttu-id="e35ff-119">La memorizzazione nella cache e l'aggiornamento dei token di accesso vengono gestiti dalla libreria MSAL e non devono quindi essere effettuati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e35ff-119">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="e35ff-120">Pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="e35ff-120">NuGet Packages</span></span>

<span data-ttu-id="e35ff-121">Questa guida usa i pacchetti NuGet seguenti:</span><span class="sxs-lookup"><span data-stu-id="e35ff-121">This guide uses the following NuGet packages:</span></span>

|<span data-ttu-id="e35ff-122">Libreria</span><span class="sxs-lookup"><span data-stu-id="e35ff-122">Library</span></span>|<span data-ttu-id="e35ff-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e35ff-123">Description</span></span>|
|---|---|
|[<span data-ttu-id="e35ff-124">Microsoft.Identity.Client</span><span class="sxs-lookup"><span data-stu-id="e35ff-124">Microsoft.Identity.Client</span></span>](https://www.nuget.org/packages/Microsoft.Identity.Client)|<span data-ttu-id="e35ff-125">Microsoft Authentication Library (MSAL)</span><span class="sxs-lookup"><span data-stu-id="e35ff-125">Microsoft Authentication Library (MSAL)</span></span>|

