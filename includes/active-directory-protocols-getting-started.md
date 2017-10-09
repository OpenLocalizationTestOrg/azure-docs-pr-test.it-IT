---
title: aaaAzure AD Panoramica del protocollo .NET | Documenti Microsoft
description: "Modalità di accesso toouse HTTP messaggi tooauthorize tooweb applicazioni e API web nel tenant mediante Azure AD."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/21/2016
ms.author: priyamo
ms.openlocfilehash: 5bd54af028c445afd3f35d67d47d7c84b476c757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## Registrare l'applicazione nel tenant di Active Directory
In primo luogo, sarà necessario tooregister l'applicazione con il tenant di Azure Active Directory (Azure AD). Questo verrà offrono un ID applicazione per l'applicazione, nonché abilitare tooreceive token.

* Accedi toohello [portale Azure](https://portal.azure.com).
* Scegliere il tenant di Azure Active Directory facendo clic sul proprio account nel hello angolo superiore destro della pagina hello.
* Nel riquadro di spostamento a sinistra di hello, fare clic su **Azure Active Directory**.
* Fare clic su **Registrazioni per l'app** e quindi su **Aggiungi**.
* Seguire le istruzioni di hello e creare una nuova applicazione. Per questa esercitazione non è rilevante che si tratti di un'applicazione Web o un'applicazione nativa, ma per esempi specifici per le applicazioni Web o native, consultare le [guide introduttive](../articles/active-directory/develop/active-directory-developers-guide.md).
  * Per le applicazioni Web, fornire hello **Sign-On URL** ovvero hello URL di base dell'app, in cui gli utenti possono accedere ad esempio `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Per le applicazioni Native, fornire un **URI di reindirizzamento**, quali Azure AD utilizzerà le risposte token tooreturn. Immettere un'applicazione, tooyour specifico valore. ad esempio`http://MyFirstAADApp`
* Dopo aver completato la registrazione, Azure AD verrà assegnare l'applicazione di un identificatore univoco di client, hello l'ID dell'applicazione. Questo valore sarà necessario in hello nelle sezioni seguenti, quindi copiarlo dalla pagina dell'applicazione hello.
