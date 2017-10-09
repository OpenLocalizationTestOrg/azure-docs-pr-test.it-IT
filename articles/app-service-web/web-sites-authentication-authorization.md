---
title: aaaAuthenticate con locale di Active Directory in Azure app | Documenti Microsoft
description: Informazioni sulle diverse opzioni di hello per le app line-of-business in Azure App Service tooauthenticate con Active Directory locale
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: dde6b7e6-bf6a-4fa5-8390-3a18155d21bd
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: 65bf25aaa0447fbbea7c754db55842d57e70757e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-on-premises-active-directory-in-your-azure-app"></a>Eseguire l'autenticazione con l'istanza locale di Active Directory nell'app Azure
Questo articolo illustra come tooauthenticate con locale Active Directory (AD) in [Azure App Service](../app-service/app-service-value-prop-what-is.md). Un'applicazione Azure è ospitata nel cloud hello, ma esistono modi tooauthenticate locale agli utenti di Active Directory in modo sicuro. 

## <a name="authenticate-through-azure-active-directory"></a>Eseguire l'autenticazione tramite Azure Active Directory
Un tenant di Azure Active Directory può essere sincronizzato a livello di directory con un'istanza di Active Directory locale. Questo approccio consente agli utenti di Active Directory di accedere all'App da hello internet ed eseguire l'autenticazione utilizzando le credenziali locali. Inoltre, il servizio app di Azure offre una [soluzione chiavi in mano per questo metodo](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). Con pochi clic su un pulsante è possibile abilitare l'autenticazione con un tenant sincronizzato a livello di directory per l'app Azure. Questo approccio presenta hello seguenti vantaggi:

* Non richiede alcun codice di autenticazione nell'app. Consente di eseguire servizio App hello autenticazione e il tempo richiesto per funzionalità nell'app.
* [API Azure AD Graph](http://msdn.microsoft.com/library/azure/hh974476.aspx) consente di accedere ai dati di toodirectory dall'app di Azure.
* Fornisce l'accesso SSO troppo[tutte le applicazioni supportate da Azure Active Directory](/marketplace/active-directory/), inclusi Office 365, Dynamics CRM Online, Microsoft Intune e migliaia di applicazioni cloud non Microsoft. 
* Azure Active Directory supporta il controllo degli accessi in base al ruolo. È possibile utilizzare il modello di hello [Authorize(Roles="X")] con codice tooyour modifiche minime.

toosee toowrite un'app di Azure line-of-business che esegue l'autenticazione con Azure Active Directory, vedere [creare un'app di Azure line-of-business con l'autenticazione di Azure Active Directory](web-sites-dotnet-lob-application-azure-ad.md).

## <a name="authenticate-through-an-on-premises-sts"></a>Eseguire l'autenticazione tramite un servizio token di sicurezza locale
Se si dispone di un locale servizio token di sicurezza (STS) come Active Directory Federation Services (ADFS), è possibile utilizzare l'autenticazione toofederate per l'app Azure. Questo approccio è migliore quando i criteri aziendali impediscono che i dati di Active Directory vengano archiviati in Azure. Si noti tuttavia seguente hello:

* La topologia del servizio token di sicurezza deve essere distribuita in locale, con sovraccarico in termini di costi e gestione.
* Solo gli amministratori di AD FS possono configurare [relying party trust e le regole attestazioni](http://technet.microsoft.com/library/dd807108.aspx), che potrebbe limitare le opzioni per gli sviluppatori di hello. In hello invece, è possibile toomanage e personalizzare [attestazioni](http://technet.microsoft.com/library/ee913571.aspx) in ogni applicazione.
* Tooon locale di accedere ai dati di Active Directory richiedono una soluzione distinta tramite firewall aziendale hello.

toosee toowrite un'app di Azure line-of-business che esegue l'autenticazione con un servizio token di sicurezza locale, vedere [creare un'app di Azure line-of-business con l'autenticazione di ADFS](web-sites-dotnet-lob-application-adfs.md).

