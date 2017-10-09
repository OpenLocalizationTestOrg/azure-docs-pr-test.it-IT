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
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a>Aggiungere Accedi con l'app web ASP.NET di Microsoft tooan

Questa guida illustra come tooimplement Accedi con Microsoft tramite una soluzione di MVC ASP.NET con un'applicazione web tradizionale basato su browser con OpenID Connect. 

Alla fine di hello di questa Guida, l'applicazione verrà tooaccept in grado di accesso aggiuntivi del personale account (inclusi outlook.com, live.com e altri), nonché di lavoro e gli account da qualsiasi società o organizzazione che è integrato con Azure Active Directory dell'istituto di istruzione. 

> Questa guida richiede Visual Studio 2015 Update 3 o Visual Studio 2017.  Se non lo si ha, è possibile  [scaricare Visual Studio 2017 gratuitamente](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a>Come interpretare questa guida

![Come interpretare questa guida](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

Questa guida si basa sullo scenario hello in un browser accede a un sito web ASP.NET, che richiede un tooauthenticate utente tramite un pulsante Accedi. In questo scenario, la maggior parte della pagina web di hello lavoro toorender hello si verifica sul lato server hello.

## <a name="libraries"></a>Librerie

Questa Guida Usa hello librerie seguenti:

|Libreria|Descrizione|
|---|---|
|[Microsoft.Owin.Security.OpenIdConnect](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|Middleware che consente a un toouse applicazione OpenIdConnect per l'autenticazione|
|[Microsoft.Owin.Security.Cookies](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|Middleware che consente a una sessione di utente toomaintain dell'applicazione utilizzando i cookie|
|[Microsoft.Owin.Host.SystemWeb](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|Consente di applicazioni basate su OWIN toorun in IIS utilizzando la pipeline delle richieste ASP.NET hello|

