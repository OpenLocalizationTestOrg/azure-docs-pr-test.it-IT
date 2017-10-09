---
title: iOS v2 aaaAzure AD Getting Started - introduzione | Documenti Microsoft
description: "Informazioni sulle modalità per le applicazioni iOS (Swift) per chiamare un'API che richiede token di accesso dall'endpoint di Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: f40aebbb75490912e533aecc7eedfb2b2dcd8c6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-ios-app"></a><span data-ttu-id="0bc86-103">Chiamare hello Microsoft Graph API da un'app iOS</span><span class="sxs-lookup"><span data-stu-id="0bc86-103">Call hello Microsoft Graph API from an iOS app</span></span>

<span data-ttu-id="0bc86-104">Questa guida illustra come un'applicazione iOS nativa (Swift) è possibile ottenere un accesso token e chiamare hello Microsoft Graph API o altre API che richiedono i token di accesso dall'endpoint di Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="0bc86-104">This guide demonstrates how a native iOS application (Swift) can get an access token and call hello Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="0bc86-105">Alla fine di hello di questa Guida, l'applicazione verrà essere in grado di toocall un'API protetta utilizzando account personali (inclusi outlook.com, live.com e altri), nonché di lavoro e gli account dell'istituto di istruzione da qualsiasi società o organizzazione con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0bc86-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>

> ### <a name="pre-requisites"></a><span data-ttu-id="0bc86-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0bc86-106">Pre-requisites</span></span>
> - <span data-ttu-id="0bc86-107">XCode 8.x è obbligatorio per questa guida.</span><span class="sxs-lookup"><span data-stu-id="0bc86-107">XCode 8.x is required for this guide.</span></span> <span data-ttu-id="0bc86-108">È possibile scaricare XCode [da qui](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "URL di Download di XCode").</span><span class="sxs-lookup"><span data-stu-id="0bc86-108">You can download XCode [from here](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode Download URL").</span></span>
> - <span data-ttu-id="0bc86-109">[Carthage](https://github.com/Carthage/Carthage) per la gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="0bc86-109">[Carthage](https://github.com/Carthage/Carthage) for package management</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="0bc86-110">Come interpretare questa guida</span><span class="sxs-lookup"><span data-stu-id="0bc86-110">How this guide works</span></span>

![Come interpretare questa guida](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

<span data-ttu-id="0bc86-112">applicazione di esempio Hello creata da questa Guida consente un hello tooquery di iOS dell'applicazione Microsoft Graph API o un'API Web che accetta i token dall'endpoint di Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="0bc86-112">hello sample application created by this guide enables an iOS application tooquery hello Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="0bc86-113">Per questo scenario, un token viene aggiunto tooHTTP richieste tramite l'intestazione di autorizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="0bc86-113">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="0bc86-114">Acquisizione del token e il rinnovo viene gestita da hello libreria di autenticazione di Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="0bc86-114">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="0bc86-115">Gestione dell'acquisizione di token per l'accesso ad API Web protette</span><span class="sxs-lookup"><span data-stu-id="0bc86-115">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="0bc86-116">Dopo l'autenticazione utente hello, applicazione di esempio hello riceve un token che può essere utilizzato tooquery hello Microsoft Graph API o un'API Web protetta da Microsoft Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="0bc86-116">After hello user authenticates, hello sample application receives a token that can be used tooquery hello Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="0bc86-117">API, ad esempio Microsoft Graph richiedono un tooallow token di accesso sull'accesso alle risorse specifiche – tooread, ad esempio, un profilo utente, del calendario dell'utente di accedere o inviare un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="0bc86-117">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="0bc86-118">L'applicazione può richiedere un token di accesso tramite la libreria MSAL specificando gli ambiti API.</span><span class="sxs-lookup"><span data-stu-id="0bc86-118">Your application can request an access token using MSAL by specifying API scopes.</span></span> <span data-ttu-id="0bc86-119">Questo token di accesso viene quindi aggiunto toohello intestazione autorizzazione HTTP per ogni chiamata effettuata hello la risorsa protetta.</span><span class="sxs-lookup"><span data-stu-id="0bc86-119">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span>

<span data-ttu-id="0bc86-120">La memorizzazione nella cache e l'aggiornamento dei token di accesso vengono gestiti dalla libreria MSAL e non devono quindi essere effettuati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0bc86-120">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="0bc86-121">Pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="0bc86-121">NuGet packages</span></span>

<span data-ttu-id="0bc86-122">Questa Guida Usa hello pacchetti NuGet seguenti:</span><span class="sxs-lookup"><span data-stu-id="0bc86-122">This guide uses hello following NuGet packages:</span></span>

|<span data-ttu-id="0bc86-123">Libreria</span><span class="sxs-lookup"><span data-stu-id="0bc86-123">Library</span></span>|<span data-ttu-id="0bc86-124">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0bc86-124">Description</span></span>|
|---|---|
|[<span data-ttu-id="0bc86-125">MSAL.framework</span><span class="sxs-lookup"><span data-stu-id="0bc86-125">MSAL.framework</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|<span data-ttu-id="0bc86-126">Anteprima di Microsoft Authentication Library per iOS</span><span class="sxs-lookup"><span data-stu-id="0bc86-126">Microsoft Authentication Library Preview for iOS</span></span>|

