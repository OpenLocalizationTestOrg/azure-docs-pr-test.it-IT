---
title: Introduzione ad Android per Azure AD v2 - Intro | Microsoft Docs
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
ms.openlocfilehash: d933781713456f73aa76db557fdf35672dfb2a29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="call-the-microsoft-graph-api-from-an-android-app"></a><span data-ttu-id="8c994-103">Chiamare l'API Microsoft Graph da un'app Android</span><span class="sxs-lookup"><span data-stu-id="8c994-103">Call the Microsoft Graph API from an Android app</span></span>

<span data-ttu-id="8c994-104">Questa guida dimostra come un'applicazione Android nativa può ottenere un token di accesso e chiamare l'API Microsoft Graph o altre API che richiedono token di accesso dall'endpoint di Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="8c994-104">This guide demonstrates how a native Android application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="8c994-105">Al termine di questa guida, l'applicazione sarà in grado di chiamare un'API protetta usando sia account personali (ad esempio, outlook.com, live.com e altri) sia account aziendali o di istituti di istruzione di proprietà di aziende o organizzazioni con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8c994-105">At the end of this guide, your application will be able to call a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

### <a name="how-this-sample-works"></a><span data-ttu-id="8c994-106">Come interpretare questo esempio</span><span class="sxs-lookup"><span data-stu-id="8c994-106">How this sample works</span></span>
![Come interpretare questo esempio](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

<span data-ttu-id="8c994-108">L'esempio creato in questa guida si basa su uno scenario in cui viene usata un'applicazione Android per eseguire query su un'API Web che accetta token dall'endpoint di Azure Active Directory v2, in questo caso l'API Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="8c994-108">The sample created by this guide is based on a scenario where an Android application is used to query a Web API that accepts tokens from Azure Active Directory v2 endpoint – in this case, Microsoft Graph API.</span></span> <span data-ttu-id="8c994-109">Per questo scenario, viene aggiunto un token a richieste HTTP tramite l'intestazione di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="8c994-109">For this scenario, a token is added to HTTP requests via the Authorization header.</span></span> <span data-ttu-id="8c994-110">L'acquisizione e il rinnovo del token vengono gestiti da Microsoft Authentication Library (MSAL).</span><span class="sxs-lookup"><span data-stu-id="8c994-110">Token acquisition and renewal is handled by the Microsoft Authentication Library (MSAL).</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="8c994-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8c994-111">Pre-requisites</span></span>
* <span data-ttu-id="8c994-112">Questa installazione guidata è basata su Android Studio, ma è accettabile anche qualsiasi altro ambiente di sviluppo di applicazioni Android.</span><span class="sxs-lookup"><span data-stu-id="8c994-112">This guided setup is focused on Android Studio, but any other Android application development environment is also acceptable.</span></span> 
* <span data-ttu-id="8c994-113">È necessario Android SDK 21 o versione successiva (è consigliato SDK 25).</span><span class="sxs-lookup"><span data-stu-id="8c994-113">Android SDK 21 or newer is required (SDK 25 is recommended).</span></span>
* <span data-ttu-id="8c994-114">Per questa versione di Microsoft Authentication Library (MSAL) per Android è necessario Google Chrome o un Web browser che usa schede personalizzate.</span><span class="sxs-lookup"><span data-stu-id="8c994-114">Google Chrome or a web browser using Custom Tabs is required for this release of Microsoft Authentication Library (MSAL) for Android.</span></span>

> <span data-ttu-id="8c994-115">Nota: Google Chrome non è incluso in Visual Studio Emulator for Android.</span><span class="sxs-lookup"><span data-stu-id="8c994-115">Note: Google Chrome is not included on Visual Studio Emulator for Android.</span></span> <span data-ttu-id="8c994-116">È consigliabile testare questo codice in un emulatore con API 25 o in un'immagine con API 21 o versione successiva in cui è installato Google Chrome.</span><span class="sxs-lookup"><span data-stu-id="8c994-116">We recommend you to test this code on an Emulator with API 25 or an image with API 21 or newer that has with Google Chrome installed.</span></span>


### <a name="how-to-handle-token-acquisition-to-access-a-protected-web-api"></a><span data-ttu-id="8c994-117">Come gestire l'acquisizione dei token per accedere a un'API Web protetta</span><span class="sxs-lookup"><span data-stu-id="8c994-117">How to handle token acquisition to access a protected Web API</span></span>

<span data-ttu-id="8c994-118">Dopo che l'utente ha eseguito l'autenticazione, l'applicazione di esempio riceve un token che può essere usato per eseguire query nell'API Microsoft Graph o in un'API Web protetta da Microsoft Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="8c994-118">After the user authenticates, the sample application receives a token that can be used to query Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="8c994-119">API come Microsoft Graph richiedono un token di accesso per consentire l'accesso a risorse specifiche, ad esempio per leggere un profilo utente, accedere al calendario dell'utente o inviare un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="8c994-119">APIs such as Microsoft Graph require an access token to allow accessing specific resources – for example, to read a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="8c994-120">L'applicazione può richiedere un token di accesso usando la libreria MSAL per accedere alle risorse tramite la definizione di ambiti API.</span><span class="sxs-lookup"><span data-stu-id="8c994-120">Your application can request an access token using MSAL to access these resources by specifying API scopes.</span></span> <span data-ttu-id="8c994-121">Il token di accesso ottenuto viene quindi aggiunto all'intestazione di autorizzazione HTTP per ogni chiamata effettuata alla risorsa protetta.</span><span class="sxs-lookup"><span data-stu-id="8c994-121">This access token is then added to the HTTP Authorization header for every call made against the protected resource.</span></span> 

<span data-ttu-id="8c994-122">La memorizzazione nella cache e l'aggiornamento dei token di accesso vengono gestiti dalla libreria MSAL e non devono quindi essere effettuati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8c994-122">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>

### <a name="libraries"></a><span data-ttu-id="8c994-123">Librerie</span><span class="sxs-lookup"><span data-stu-id="8c994-123">Libraries</span></span>

<span data-ttu-id="8c994-124">Questa guida usa le librerie seguenti:</span><span class="sxs-lookup"><span data-stu-id="8c994-124">This guide uses the following libraries:</span></span>

|<span data-ttu-id="8c994-125">Libreria</span><span class="sxs-lookup"><span data-stu-id="8c994-125">Library</span></span>|<span data-ttu-id="8c994-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8c994-126">Description</span></span>|
|---|---|
|[<span data-ttu-id="8c994-127">com.microsoft.identity.client</span><span class="sxs-lookup"><span data-stu-id="8c994-127">com.microsoft.identity.client</span></span>](http://javadoc.io/doc/com.microsoft.identity.client/msal)|<span data-ttu-id="8c994-128">Microsoft Authentication Library (MSAL)</span><span class="sxs-lookup"><span data-stu-id="8c994-128">Microsoft Authentication Library (MSAL)</span></span>|
