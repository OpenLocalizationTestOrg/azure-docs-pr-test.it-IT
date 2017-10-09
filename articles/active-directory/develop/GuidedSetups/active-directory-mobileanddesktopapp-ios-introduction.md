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
# <a name="call-hello-microsoft-graph-api-from-an-ios-app"></a>Chiamare hello Microsoft Graph API da un'app iOS

Questa guida illustra come un'applicazione iOS nativa (Swift) è possibile ottenere un accesso token e chiamare hello Microsoft Graph API o altre API che richiedono i token di accesso dall'endpoint di Azure Active Directory v2.

Alla fine di hello di questa Guida, l'applicazione verrà essere in grado di toocall un'API protetta utilizzando account personali (inclusi outlook.com, live.com e altri), nonché di lavoro e gli account dell'istituto di istruzione da qualsiasi società o organizzazione con Azure Active Directory.

> ### <a name="pre-requisites"></a>Prerequisiti
> - XCode 8.x è obbligatorio per questa guida. È possibile scaricare XCode [da qui](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "URL di Download di XCode").
> - [Carthage](https://github.com/Carthage/Carthage) per la gestione pacchetti

### <a name="how-this-guide-works"></a>Come interpretare questa guida

![Come interpretare questa guida](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

applicazione di esempio Hello creata da questa Guida consente un hello tooquery di iOS dell'applicazione Microsoft Graph API o un'API Web che accetta i token dall'endpoint di Azure Active Directory v2. Per questo scenario, un token viene aggiunto tooHTTP richieste tramite l'intestazione di autorizzazione hello. Acquisizione del token e il rinnovo viene gestita da hello libreria di autenticazione di Microsoft (MSAL).


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>Gestione dell'acquisizione di token per l'accesso ad API Web protette

Dopo l'autenticazione utente hello, applicazione di esempio hello riceve un token che può essere utilizzato tooquery hello Microsoft Graph API o un'API Web protetta da Microsoft Azure Active Directory v2.

API, ad esempio Microsoft Graph richiedono un tooallow token di accesso sull'accesso alle risorse specifiche – tooread, ad esempio, un profilo utente, del calendario dell'utente di accedere o inviare un messaggio di posta elettronica. L'applicazione può richiedere un token di accesso tramite la libreria MSAL specificando gli ambiti API. Questo token di accesso viene quindi aggiunto toohello intestazione autorizzazione HTTP per ogni chiamata effettuata hello la risorsa protetta.

La memorizzazione nella cache e l'aggiornamento dei token di accesso vengono gestiti dalla libreria MSAL e non devono quindi essere effettuati dall'applicazione.


### <a name="nuget-packages"></a>Pacchetti NuGet

Questa Guida Usa hello pacchetti NuGet seguenti:

|Libreria|Descrizione|
|---|---|
|[MSAL.framework](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|Anteprima di Microsoft Authentication Library per iOS|

