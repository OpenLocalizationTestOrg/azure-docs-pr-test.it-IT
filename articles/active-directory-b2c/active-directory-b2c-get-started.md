---
title: 'Azure Active Directory B2C: creare un tenant di Azure Active Directory B2C | Microsoft Docs'
description: Un argomento su come toocreate un B2C di Azure Active Directory del tenant
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a>Creare un tenant di Azure Active Directory B2C in hello portale di Azure

Modificato da Sipi.

Questa guida introduttiva permette di creare un tenant di Microsoft Azure Active Directory (Azure AD) B2C in pochi minuti. Al termine, si dispone di un toouse tenant B2C per la registrazione delle applicazioni B2C.

## <a name="prerequisites"></a>Prerequisiti

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a>Accedi tooAzure

Accedi toohello [portale di Azure](https://portal.azure.com/).

## <a name="create-an-azure-ad-b2c-tenant"></a>Creare un tenant di Azure AD B2C

Le funzionalità B2C non possono essere abilitate nei tenant esistenti. È necessario toocreate un tenant di Azure Active Directory B2C.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

Congratulazioni, è stato creato un tenant di Azure Active Directory B2C. Si è un amministratore globale del tenant hello. può aggiungere altri amministratori globali in base alle esigenze. tooyour tooswitch nuovo tenant, fare clic su hello *gestire il nuovo collegamento di tenant*.

![Collegamento per gestire il nuovo tenant](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> Se si intende toouse un tenant B2C per un'app di produzione, leggere l'articolo hello su [scala di produzione e i tenant anteprima B2C](active-directory-b2c-reference-tenant-type.md). Vi sono problemi noti quando si elimina un B2C esistenti del tenant e ricrearlo con hello stesso nome di dominio. È necessario toocreate un tenant B2C con un nome di dominio diverso.
>
>

## <a name="link-your-tenant-tooyour-subscription"></a>Collegare la sottoscrizione tooyour tenant

È necessario toolink il AD B2C Azure tenant tooyour sottoscrizione di Azure tooenable B2C tutte le funzionalità e pagare gli addebiti di utilizzo. leggere più, toolearn [questo articolo](active-directory-b2c-how-to-enable-billing.md). Se si non collega il tooyour tenant di Azure Active Directory B2C sottoscrizione di Azure, alcune funzionalità è bloccata e viene visualizzato un messaggio di avviso ("alcuna sottoscrizione collegata toothis B2C tenant o hello sottoscrizione non richiede attenzione.") nelle impostazioni di hello B2C. È importante eseguire questo passaggio prima dell'invio delle applicazioni alla produzione.

## <a name="easy-access-toosettings"></a>Un accesso semplice toosettings

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

È inoltre possibile accedere pannello hello immettendo `Azure AD B2C` in **individuare risorse** nella parte superiore di hello del portale hello. Selezionare dall'elenco risultati hello **Azure Active Directory B2C** tooaccess hello pannello impostazioni B2C.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Registrare l'applicazione B2C in un tenant B2C](active-directory-b2c-app-registration.md)
