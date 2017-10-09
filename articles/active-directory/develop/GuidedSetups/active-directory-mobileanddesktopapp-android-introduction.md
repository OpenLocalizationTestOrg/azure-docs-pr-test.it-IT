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
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a>Chiamare hello Microsoft Graph API da un'app per Android

Questa guida dimostra come un'applicazione Android nativa può ottenere un token di accesso e chiamare l'API Microsoft Graph o altre API che richiedono token di accesso dall'endpoint di Azure Active Directory v2.

Alla fine di hello di questa Guida, l'applicazione verrà essere in grado di toocall un'API protetta utilizzando account personali (inclusi outlook.com, live.com e altri), nonché di lavoro e gli account dell'istituto di istruzione da qualsiasi società o organizzazione con Azure Active Directory.  

### <a name="how-this-sample-works"></a>Come interpretare questo esempio
![Come interpretare questo esempio](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

esempio Hello creato in questa guida si basa su uno scenario in cui un'applicazione Android è tooquery utilizzata un'API Web che accetta i token da Azure Active Directory v2 endpoint in questo caso, Microsoft Graph API. Per questo scenario, un token viene aggiunto tooHTTP richieste tramite l'intestazione di autorizzazione hello. Acquisizione del token e il rinnovo viene gestita da hello libreria di autenticazione di Microsoft (MSAL).

### <a name="pre-requisites"></a>Prerequisiti
* Questa installazione guidata è basata su Android Studio, ma è accettabile anche qualsiasi altro ambiente di sviluppo di applicazioni Android. 
* È necessario Android SDK 21 o versione successiva (è consigliato SDK 25).
* Per questa versione di Microsoft Authentication Library (MSAL) per Android è necessario Google Chrome o un Web browser che usa schede personalizzate.

> Nota: Google Chrome non è incluso in Visual Studio Emulator for Android. È consigliabile tootest questo codice in un emulatore con API 25 o un'immagine con API 21 o più recenti installati con Google Chrome.


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a>Come toohandle token tooaccess acquisizione un'API Web protetta

Dopo l'autenticazione utente hello, applicazione di esempio hello riceve un token che può essere utilizzato tooquery Microsoft Graph API o un'API Web protetta da Microsoft Azure Active Directory v2.

API, ad esempio Microsoft Graph richiedono un tooallow token di accesso sull'accesso alle risorse specifiche – tooread, ad esempio, un profilo utente, del calendario dell'utente di accedere o inviare un messaggio di posta elettronica. L'applicazione può richiedere un token di accesso usando MSAL tooaccess queste risorse specificando gli ambiti di API. Questo token di accesso viene quindi aggiunto toohello intestazione autorizzazione HTTP per ogni chiamata effettuata hello la risorsa protetta. 

La memorizzazione nella cache e l'aggiornamento dei token di accesso vengono gestiti dalla libreria MSAL e non devono quindi essere effettuati dall'applicazione.

### <a name="libraries"></a>Librerie

Questa Guida Usa hello librerie seguenti:

|Libreria|Descrizione|
|---|---|
|[com.microsoft.identity.client](http://javadoc.io/doc/com.microsoft.identity.client/msal)|Microsoft Authentication Library (MSAL)|
