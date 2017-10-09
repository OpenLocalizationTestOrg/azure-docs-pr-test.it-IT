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
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a>Chiamare hello Microsoft Graph API da un'app di Windows Desktop

Questa guida dimostra come un'applicazione .NET per Windows Desktop (XAML) nativa può ottenere un token di accesso e chiamare l'API Microsoft Graph o altre API che richiedono token di accesso dall'endpoint di Azure Active Directory v2.

Alla fine di hello di questa Guida, l'applicazione verrà essere in grado di toocall un'API protetta utilizzando account personali (inclusi outlook.com, live.com e altri), nonché di lavoro e gli account dell'istituto di istruzione da qualsiasi società o organizzazione con Azure Active Directory.  

> Questa guida richiede Visual Studio 2015 Update 3 o Visual Studio 2017.  Se non lo si ha, è possibile [scaricare Visual Studio 2017 gratuitamente](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a>Come interpretare questa guida

![Come interpretare questa guida](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

applicazione di esempio Hello creata da questa Guida consente tooquery un'applicazione Desktop di Windows Microsoft Graph API o un'API Web che accetta i token dall'endpoint di Azure Active Directory v2. Per questo scenario, un token viene aggiunto tooHTTP richieste tramite l'intestazione di autorizzazione hello. Acquisizione del token e il rinnovo viene gestita da hello libreria di autenticazione di Microsoft (MSAL).


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>Gestione dell'acquisizione di token per l'accesso ad API Web protette

Dopo l'autenticazione utente hello, applicazione di esempio hello riceve un token che può essere utilizzato tooquery Microsoft Graph API o un'API Web protetta da Microsoft Azure Active Directory v2.

API, ad esempio Microsoft Graph richiedono un tooallow token di accesso sull'accesso alle risorse specifiche – tooread, ad esempio, un profilo utente, del calendario dell'utente di accedere o inviare un messaggio di posta elettronica. L'applicazione può richiedere un token di accesso usando MSAL tooaccess queste risorse specificando gli ambiti di API. Questo token di accesso viene quindi aggiunto toohello intestazione autorizzazione HTTP per ogni chiamata effettuata hello la risorsa protetta. 

La memorizzazione nella cache e l'aggiornamento dei token di accesso vengono gestiti dalla libreria MSAL e non devono quindi essere effettuati dall'applicazione.


### <a name="nuget-packages"></a>Pacchetti NuGet

Questa Guida Usa hello pacchetti NuGet seguenti:

|Libreria|Descrizione|
|---|---|
|[Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client)|Microsoft Authentication Library (MSAL)|

