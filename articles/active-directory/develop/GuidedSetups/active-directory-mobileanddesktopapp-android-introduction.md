---
title: aaaAzure AD v2 Android Getting Started - introduzione | Documenti Microsoft
description: "Informazioni sul modo in cui un'app di Android può ottenere un token di accesso e chiamare l'API o le API Graph Microsoft che richiedono token di acceso dall'endpoint di Azure Active Directory v2"
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
ms.openlocfilehash: 7c76ab8bbf1a6c934ab672cccf85ae82f03f601a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a><span data-ttu-id="b4b21-103">Chiamare hello Microsoft Graph API da un'app per Android</span><span class="sxs-lookup"><span data-stu-id="b4b21-103">Call hello Microsoft Graph API from an Android app</span></span>

<span data-ttu-id="b4b21-104">Questa guida dimostra come un'applicazione Android nativa può ottenere un token di accesso e chiamare l'API Microsoft Graph o altre API che richiedono token di accesso dall'endpoint di Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="b4b21-104">This guide demonstrates how a native Android application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="b4b21-105">Alla fine di hello di questa Guida, l'applicazione verrà essere in grado di toocall un'API protetta utilizzando account personali (inclusi outlook.com, live.com e altri), nonché di lavoro e gli account dell'istituto di istruzione da qualsiasi società o organizzazione con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b4b21-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

### <a name="how-this-sample-works"></a><span data-ttu-id="b4b21-106">Come interpretare questo esempio</span><span class="sxs-lookup"><span data-stu-id="b4b21-106">How this sample works</span></span>
![Come interpretare questo esempio](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

<span data-ttu-id="b4b21-108">esempio Hello creato in questa guida si basa su uno scenario in cui un'applicazione Android è tooquery utilizzata un'API Web che accetta i token da Azure Active Directory v2 endpoint in questo caso, Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="b4b21-108">hello sample created by this guide is based on a scenario where an Android application is used tooquery a Web API that accepts tokens from Azure Active Directory v2 endpoint – in this case, Microsoft Graph API.</span></span> <span data-ttu-id="b4b21-109">Per questo scenario, un token viene aggiunto tooHTTP richieste tramite l'intestazione di autorizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="b4b21-109">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="b4b21-110">Acquisizione del token e il rinnovo viene gestita da hello libreria di autenticazione di Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="b4b21-110">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="b4b21-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b4b21-111">Pre-requisites</span></span>
* <span data-ttu-id="b4b21-112">Questa installazione guidata è basata su Android Studio, ma è accettabile anche qualsiasi altro ambiente di sviluppo di applicazioni Android.</span><span class="sxs-lookup"><span data-stu-id="b4b21-112">This guided setup is focused on Android Studio, but any other Android application development environment is also acceptable.</span></span> 
* <span data-ttu-id="b4b21-113">È necessario Android SDK 21 o versione successiva (è consigliato SDK 25).</span><span class="sxs-lookup"><span data-stu-id="b4b21-113">Android SDK 21 or newer is required (SDK 25 is recommended).</span></span>
* <span data-ttu-id="b4b21-114">Per questa versione di Microsoft Authentication Library (MSAL) per Android è necessario Google Chrome o un Web browser che usa schede personalizzate.</span><span class="sxs-lookup"><span data-stu-id="b4b21-114">Google Chrome or a web browser using Custom Tabs is required for this release of Microsoft Authentication Library (MSAL) for Android.</span></span>

> <span data-ttu-id="b4b21-115">Nota: Google Chrome non è incluso in Visual Studio Emulator for Android.</span><span class="sxs-lookup"><span data-stu-id="b4b21-115">Note: Google Chrome is not included on Visual Studio Emulator for Android.</span></span> <span data-ttu-id="b4b21-116">È consigliabile tootest questo codice in un emulatore con API 25 o un'immagine con API 21 o più recenti installati con Google Chrome.</span><span class="sxs-lookup"><span data-stu-id="b4b21-116">We recommend you tootest this code on an Emulator with API 25 or an image with API 21 or newer that has with Google Chrome installed.</span></span>


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a><span data-ttu-id="b4b21-117">Come toohandle token tooaccess acquisizione un'API Web protetta</span><span class="sxs-lookup"><span data-stu-id="b4b21-117">How toohandle token acquisition tooaccess a protected Web API</span></span>

<span data-ttu-id="b4b21-118">Dopo l'autenticazione utente hello, applicazione di esempio hello riceve un token che può essere utilizzato tooquery Microsoft Graph API o un'API Web protetta da Microsoft Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="b4b21-118">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="b4b21-119">API, ad esempio Microsoft Graph richiedono un tooallow token di accesso sull'accesso alle risorse specifiche – tooread, ad esempio, un profilo utente, del calendario dell'utente di accedere o inviare un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="b4b21-119">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="b4b21-120">L'applicazione può richiedere un token di accesso usando MSAL tooaccess queste risorse specificando gli ambiti di API.</span><span class="sxs-lookup"><span data-stu-id="b4b21-120">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="b4b21-121">Questo token di accesso viene quindi aggiunto toohello intestazione autorizzazione HTTP per ogni chiamata effettuata hello la risorsa protetta.</span><span class="sxs-lookup"><span data-stu-id="b4b21-121">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="b4b21-122">La memorizzazione nella cache e l'aggiornamento dei token di accesso vengono gestiti dalla libreria MSAL e non devono quindi essere effettuati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b4b21-122">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>

### <a name="libraries"></a><span data-ttu-id="b4b21-123">Librerie</span><span class="sxs-lookup"><span data-stu-id="b4b21-123">Libraries</span></span>

<span data-ttu-id="b4b21-124">Questa Guida Usa hello librerie seguenti:</span><span class="sxs-lookup"><span data-stu-id="b4b21-124">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="b4b21-125">Libreria</span><span class="sxs-lookup"><span data-stu-id="b4b21-125">Library</span></span>|<span data-ttu-id="b4b21-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b4b21-126">Description</span></span>|
|---|---|
|[<span data-ttu-id="b4b21-127">com.microsoft.identity.client</span><span class="sxs-lookup"><span data-stu-id="b4b21-127">com.microsoft.identity.client</span></span>](http://javadoc.io/doc/com.microsoft.identity.client/msal)|<span data-ttu-id="b4b21-128">Microsoft Authentication Library (MSAL)</span><span class="sxs-lookup"><span data-stu-id="b4b21-128">Microsoft Authentication Library (MSAL)</span></span>|
