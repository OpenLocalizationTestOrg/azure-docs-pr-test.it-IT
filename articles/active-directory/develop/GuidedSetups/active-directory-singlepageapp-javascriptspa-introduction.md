---
title: aaaAzure AD v2 JS SPA interattiva installazione - Introduzione | Documenti Microsoft
description: Come le applicazioni SPA di Javascript possono chiamare un'API che richiede token di accesso dall'endpoint di Azure Active Directory v2
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
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a>Hello chiamata API di Microsoft Graph dall'applicazione di pagina singola (SPA) un JavaScript

Questa guida illustra come lavoro personale, può accedere un JavaScript singola pagina applicazione (SPA) e account scuola, ottenere un token di accesso e chiamare l'API di Microsoft Graph hello o altre API che richiedono token di accesso di hello endpoint v2 Azure Active Directory.

### <a name="how-this-guide-works"></a>Come interpretare questa guida

![Funzionamento delle app di esempio hello generati da questa Guida](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a>Altre informazioni

applicazione di esempio Hello creata da questa Guida consente un hello tooquery SPA JavaScript Microsoft Graph API o un'API Web che accetta i token dall'endpoint di Azure Active Directory v2. Per questo scenario, dopo che un utente firma in un token di accesso è richieste tooHTTP richiesto e aggiunti tramite l'intestazione di autorizzazione hello. Acquisizione del token e il rinnovo vengono gestiti da hello libreria di autenticazione di Microsoft (MSAL).

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a>Librerie

Questa Guida Usa hello seguente libreria:

|Libreria|Descrizione|
|---|---|
|[msal.js](https://github.com/AzureAD/microsoft-authentication-library-for-js)|Authentication Library di Microsoft per l'anteprima di JavaScript|

> [!NOTE]
> *msal.js* hello destinazioni *endpoint di Azure Active Directory v2* -che abilita toosign account personali, dell'istituto di istruzione e aziendali in e acquisire i token. Hello *endpoint di Azure Active Directory v2* è [alcune limitazioni](..\active-directory-v2-limitations.md). Se si è interessati solo gli account di lavoro e dell'istituto di istruzione, utilizzare *adal.js* hello e *V1 endpoint*. toounderstand differenze tra gli endpoint v1 e v2 hello leggere hello [v1, v2 confronto](..\active-directory-v2-compare.md).

<!--end-collapse-->
