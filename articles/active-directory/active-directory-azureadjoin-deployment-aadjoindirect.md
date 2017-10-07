---
title: aaaUsage scenari e considerazioni sulla distribuzione per l'aggiunta di Azure AD | Documenti Microsoft
description: "Questo argomento illustra come gli amministratori possono configurare la funzionalità Aggiunta ad Azure AD per gli utenti finali (dipendenti, studenti o altri utenti). Viene inoltre diversi scenari reali hello per l'uso di aggiunta ad Azure AD."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 81d4461e-21c8-4fdd-9076-0e4991979f62
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7e57971481aa312ebf8a69999d194f9dcc3d4708
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="usage-scenarios-and-deployment-considerations-for-azure-ad-join"></a>Scenari di utilizzo e considerazioni sulla distribuzione per Aggiunta di Azure AD
## <a name="usage-scenarios-for-azure-ad-join"></a>Scenari di utilizzo per Aggiunta ad Azure AD
### <a name="scenario-1-businesses-largely-in-hello-cloud"></a>Scenario 1: Imprese in gran parte nel cloud di hello
Azure Active Directory Join (aggiunta di Azure AD) possono trarre vantaggio è se attualmente operare e gestire le identità per l'azienda nel cloud hello o spostano appena toohello cloud. È possibile utilizzare un account che è stato creato in Azure AD toosign in tooWindows 10. Tramite [hello eseguire innanzitutto il processo di analisi (FRX)](active-directory-azureadjoin-user-frx.md), o creando un join di Azure AD da [menu Impostazioni hello](active-directory-azureadjoin-user-upgrade.md), gli utenti è possono aggiungere i tooAzure macchine AD.  Gli utenti potranno godere anche single sign-on (SSO) accesso cloud troppo risorse come Office 365, nel browser o nelle applicazioni di Office.

### <a name="scenario-2-educational-institutions"></a>Scenario 2: Istituti di istruzione
Gli istituti di istruzione hanno in genere due tipi di utenti: docenti e studenti. I membri di istituti di istruzione vengono considerati i membri dell'organizzazione hello a lungo termine. Per loro è consigliabile creare account locali. Ma gli studenti sono shorter-term membri dell'organizzazione hello e gli account possono essere gestiti in Azure AD. Ciò significa che può essere inserita scala directory cloud toohello anziché essere archiviata in locale. Significa anche che studenti verranno in grado di toosign in tooWindows con gli account di Azure AD e ottenere l'accesso alle risorse di 365 tooOffice nelle applicazioni di Office.

### <a name="scenario-3-retail-businesses"></a>Scenario 3: Negozi
I negozi impiegano lavoratori stagionali e dipendenti a lungo termine. In genere si creano account locali e si usano computer aggiunti a un dominio per i dipendenti a tempo pieno e a lungo termine. Ma stagionale sono shorter-term membri dell'organizzazione hello ed è auspicabile toomanage i propri account in cui le licenze utente possono essere più facilmente spostate. Quando si crea l'account utente nel cloud hello con licenze di Office 365, questi utenti vantaggi hello accesso tooWindows e applicazioni di Office con un account di Azure AD, mentre una volta terminata mantenere una maggiore flessibilità con le licenze.

### <a name="scenario-4-additional-scenarios"></a>Scenario 4: Scenari aggiuntivi
Insieme ai vantaggi hello descritti in precedenza, vantaggioso che gli utenti di aggiungere i relativi tooAzure dispositivi Active Directory a causa di un'esperienza semplificata di unione, la gestione dei dispositivi efficiente, registrazione per la gestione automatica dei dispositivi mobili e single sign-on tooAzure Active Directory e risorse locali.  

## <a name="deployment-considerations-for-azure-ad-join"></a>Considerazioni sulla distribuzione per Azure AD Join
### <a name="enable-your-users-toojoin-a-company-owned-device-directly-tooazure-ad"></a>Abilitare il toojoin agli utenti un dispositivo di proprietà dell'azienda direttamente tooAzure AD
Le aziende possono offrire le organizzazioni e società toopartner account solo cloud. Questi partner possono quindi accedere facilmente alle app e alle risorse aziendali tramite l'accesso Single Sign-On. Questo scenario è applicabile toousers che accedono alle risorse principalmente nel cloud di hello, ad esempio le applicazioni di Office 365 o SaaS che si basano su Azure AD per l'autenticazione.

### <a name="prerequisites"></a>Prerequisiti
**Il livello di organizzazione hello (amministratore)**

* Sottoscrizione di Azure con Azure Active Directory  

**A livello di utente hello**

* Windows 10 (Professional ed Enterprise)

### <a name="administrator-tasks"></a>Attività dell'amministratore
* [Configurare la registrazione dei dispositivi](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>Attività dell'utente
* [Configurare un nuovo dispositivo Windows 10 con Azure AD durante l'installazione](active-directory-azureadjoin-user-frx.md)
* [Configurare un dispositivo Windows 10 con Azure AD dal menu Impostazioni hello](active-directory-azureadjoin-user-upgrade.md)
* [Aggiungere un'organizzazione di tooyour dispositivo Windows 10 personale](active-directory-azureadjoin-personal-device.md)

## <a name="enable-byod-in-your-organization-for-windows-10"></a>Abilitare le funzionalità BYOD per Windows 10 nell'organizzazione
Le risorse e i App aziendali tooaccess dispositivi (BYOD) di Windows personale, è possibile impostare il toouse utenti e i dipendenti. Gli utenti possono aggiungere i relativi account (account aziendale o dell'istituto di istruzione) tooa personali Windows dispositivo tooaccess risorse di Azure AD in modo sicuro e conforme.

### <a name="prerequisites"></a>Prerequisiti
**Il livello di organizzazione hello (amministratore)**

* Sottoscrizione di Azure AD

**A livello di utente hello**

* Windows 10 (Professional ed Enterprise)

### <a name="administrator-tasks"></a>Attività dell'amministratore
* [Configurare la registrazione dei dispositivi](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>Attività dell'utente
* [Aggiungere un'organizzazione di tooyour dispositivo Windows 10 personale](active-directory-azureadjoin-personal-device.md)

## <a name="additional-information"></a>Informazioni aggiuntive
* [Windows 10 per enterprise hello: i dispositivi toouse modi per lavoro](active-directory-azureadjoin-windows10-devices-overview.md)
* [Estensione cloud dispositivi tooWindows 10 funzionalità tramite Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Autenticazione delle identità senza password con Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Scenari di utilizzo per Aggiunta ad Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Connettersi tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurare Aggiunta di Azure AD](active-directory-azureadjoin-setup.md)

