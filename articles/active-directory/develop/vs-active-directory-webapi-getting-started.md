---
title: aaaGet avviato con Azure AD nei progetti di Visual Studio WebApi | Documenti Microsoft
description: "La modalità di avvio tramite Azure Active Directory nei progetti WebApi dopo la creazione di un annuncio di Azure con Visual Studio tooor connessione tooget servizi connessi"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: bf1eb32d-25cd-4abf-8679-2ead299fedaa
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/19/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 21413a71a2fd61f31268bf6d5e4d86b8be5bd16a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a>Introduzione ad Azure Active Directory e ai servizi relativi a Visual Studio (progetti WebApi)
> [!div class="op_single_selector"]
> * [Per iniziare](vs-active-directory-webapi-getting-started.md)
> * [Risultati](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-tooaccess-controllers"></a>Controller di tooaccess che richiede l'autenticazione
Tutti i controller nel progetto sono state decorare con hello **Authorize** attributo. Questo attributo richiede toobe utente hello autenticati prima che l'accesso a hello API definito da questi controller. tooallow hello controller toobe accedere in modo anonimo, rimuovere questo attributo dal controller hello. Se si desidera che le autorizzazioni hello tooset a un livello più granulare, applicare hello attributo tooeach (metodo) che richiede l'autorizzazione anziché applicarla classe controller toohello.

## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni su Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

