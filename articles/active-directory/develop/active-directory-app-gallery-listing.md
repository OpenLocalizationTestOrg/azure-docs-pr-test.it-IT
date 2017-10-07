---
title: aaaListing l'applicazione nella raccolta di hello Azure Active Directory dell'applicazione
description: Come un'applicazione che supporta single sign-on in toolist hello raccolta di Azure Active Directory | Microsoft Azure
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a>Elenca l'applicazione nella raccolta di hello Azure Active Directory dell'applicazione
un'applicazione che supporta single sign-on con Azure Active Directory in hello toolist [raccolta di Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), un'applicazione hello deve prima esigenze tooimplement di hello seguenti modalità di integrazione:

* **OpenID Connect** : integrazione diretta con Azure AD Usa OpenID Connect per l'autenticazione e hello consenso di Azure AD API per la configurazione. Se si avvia solo un'integrazione e l'applicazione non supporta SAML, questo è la modalità consigliata hello.
* **SAML** : l'applicazione contiene già hello possibilità tooconfigure terze parti i provider di identità tramite protocollo SAML hello.

Di seguito è riportato un elenco dei requisiti di ogni modalità.

## <a name="openid-connect-integration"></a>Integrazione di OpenID Connect
toointegrate l'applicazione con Azure AD, hello seguente [le istruzioni per sviluppatori](active-directory-authentication-scenarios.md). Quindi completare alle seguenti domande hello e inviare toowaadpartners@microsoft.com.

* Fornire le credenziali per un tenant di prova o di un account con l'applicazione che può essere utilizzato da hello integrazione hello tootest team di Azure AD.  
* Vengono fornite istruzioni su come hello Azure AD può accedere e connettersi a un'istanza di applicazione di tooyour di Azure AD con hello [framework di consenso di Azure AD](active-directory-integrating-applications.md#overview-of-the-consent-framework). 
* Fornire eventuali altre istruzioni necessarie per hello Azure AD team tootest single sign-on con l'applicazione. 
* Fornire informazioni hello seguenti:

> Nome società:
> 
> Sito Web società:
> 
> Nome dell'applicazione:
> 
> Descrizione dell'applicazione (max 200 caratteri):
> 
> Sito Web dell'applicazione (informazioni):
> 
> Sito Web del supporto tecnico dell'applicazione o informazioni di contatto:
> 
> ID dell'applicazione hello, come illustrato nei dettagli dell'applicazione hello in https://portal.azure.com:
> 
> URL di iscrizione dell'applicazione esiti di toosign per i clienti e/o acquistare un'applicazione hello:
> 
> Scegliere le categorie di toothree per l'applicazione di toobe elencati sotto (per le categorie disponibili, vedere hello Azure Active Directory Marketplace):
> 
> Allegare l'icona piccola dell'applicazione (file PNG, 45x45 pixel, colore di sfondo a tinta unita):
> 
> Allegare l'icona grande dell'applicazione (file PNG, 215x215 pixel, colore di sfondo a tinta unita):
> 
> Allegare il logo dell'applicazione (file PNG, 150x122 pixel, colore di sfondo a tinta unita):
> 
> 

## <a name="saml-integration"></a>Integrazione di SAML
Qualsiasi app che supporta SAML 2.0 può integrarsi direttamente con un tenant di Azure AD usando [questi tooadd istruzioni un'applicazione personalizzata](../active-directory-saas-custom-apps.md). Dopo aver verificato che l'integrazione dell'applicazione funziona con Azure AD, inviare le seguenti informazioni troppo hello<mailto:waadpartners@microsoft.com>.

* Fornire le credenziali per un tenant di prova o di un account con l'applicazione che può essere utilizzato da hello integrazione hello tootest team di Azure AD.  
* Fornire hello SAML URL Sign-On, URL autorità di certificazione (ID entità), e l'URL di risposta (servizio consumer di asserzione) i valori per l'applicazione, come descritto [qui](../active-directory-saas-custom-apps.md). Se si forniscono in genere questi valori come parte di un file di metadati SAML, inviare anche quest'ultimo.
* Fornire una breve descrizione di come tooconfigure Azure AD come provider di identità dell'applicazione tramite SAML 2.0. Se l'applicazione supporta la configurazione di Azure AD come provider di identità tramite un portale amministrativo self-service, quindi verificare le credenziali di hello fornite in precedenza includono hello possibilità tooset questo backup.
* Fornire informazioni hello seguenti:

> Nome società:
> 
> Sito Web società:
> 
> Nome dell'applicazione:
> 
> Descrizione dell'applicazione (max 200 caratteri):
> 
> Sito Web dell'applicazione (informazioni):
> 
> Sito Web del supporto tecnico dell'applicazione o informazioni di contatto:
> 
> URL di iscrizione dell'applicazione esiti di toosign per i clienti e/o acquistare un'applicazione hello:
> 
> Scegliere le categorie di toothree per toobe l'applicazione elencati sotto (per le categorie disponibili, vedere hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):
> 
> Allegare l'icona piccola dell'applicazione (file PNG, 45x45 pixel, colore di sfondo a tinta unita):
> 
> Allegare l'icona grande dell'applicazione (file PNG, 215x215 pixel, colore di sfondo a tinta unita):
> 
> Allegare il logo dell'applicazione (file PNG, 150x122 pixel, colore di sfondo a tinta unita):
> 
> 

