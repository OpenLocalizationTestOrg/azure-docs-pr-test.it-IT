---
title: aaaManage SSO per il Proxy di applicazione Azure AD | Documenti Microsoft
description: Informazioni sui concetti di base di hello di single sign-on con Proxy dell'applicazione
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: a278751a5cb1bf98c970a4e5d2eb3edc3b784096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a>Come viene offerto l'accesso Single Sign-On dal proxy di applicazione di Azure AD?

Single Sign-On è un elemento chiave del proxy di applicazione di Azure AD.  Fornisce un'esperienza utente ottimale hello perché gli utenti dispongono solo di toosign in Active Directory nel cloud hello tooAzure. Dopo l'autenticazione tooAzure Active Directory, connettore Proxy dell'applicazione hello gestisce un'applicazione hello autenticazione toohello locale. un'applicazione Hello back-end non è possibile distinguere hello da un utente remoto di accedere tramite il Proxy di applicazione e un utilizzo normale in un dispositivo aggiunto al dominio. 

toouse Azure Active Directory per applicazioni single sign-on tooyour, è necessario tooselect **Azure Active Directory** come metodo di preautenticazione hello. Se si seleziona **pass-through** quindi gli utenti non eseguono l'autenticazione Active Directory tooAzure affatto, ma sono diretti toohello retta applicazione. È possibile configurare questa impostazione quando si pubblica un'applicazione, o passa tooyour applicazione nel portale di Azure hello e modificare le impostazioni del Proxy di applicazione hello. 

toosee il single sign-on le opzioni, seguire questi passaggi:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Passare troppo**Azure Active Directory** > **applicazioni aziendali** > **tutte le applicazioni**.
3. Selezionare hello app il cui accesso single sign-on opzioni desidera toomanage.
4. Selezionare **Single Sign-On**.

   ![Menu a discesa Single Sign-On](./media/application-proxy-sso-overview/single-sign-on-mode.png)

menu a discesa Hello Mostra cinque opzioni per l'applicazione di single sign-on tooyour:

* Single Sign-On di Azure AD disabilitato
* Accesso basato su password
* Linked sign-on (Accesso collegato)
* Autenticazione integrata di Windows
* Accesso basato su intestazione

## <a name="azure-ad-single-sign-on-disabled"></a>Single Sign-On di Azure AD disabilitato

Se non si desidera l'integrazione di Azure Active Directory toouse per single sign-on tooyour applicazione, scegliere **Azure single sign-on AD disabilitato**. Con questa opzione selezionata, gli utenti possono eseguire l'autenticazione due volte. In primo luogo, essi autenticare tooAzure Active Directory e quindi accedere toohello applicazione stessa. 

Questa opzione è una scelta ottimale se l'applicazione locale non richiede tooauthenticate gli utenti, ma si desidera tooadd Azure Active Directory come un livello di sicurezza per l'accesso remoto. 

## <a name="password-based-sign-on"></a>Accesso basato su password

Se si desidera toouse Azure Active Directory come un insieme di credenziali di password per le applicazioni locali, scegliere **Password-sign-on basato su**. Questa opzione è la scelta migliore se l'autenticazione all'applicazione è bastata su nome utente e password e non su intestazioni o token di accesso. Con basato su password sign-on, gli utenti devono toosign in hello applicazione toohello prima volta che accedono ad esso. Successivamente, Azure Active Directory fornisce hello username e password per conto di utente hello. 

Per informazioni sulla configurazione dell'accesso basato su password, vedere [Insieme di credenziali delle password per l'accesso Single Sign-On con il proxy di applicazione](application-proxy-sso-azure-portal.md).

## <a name="linked-sign-on"></a>Linked sign-on (Accesso collegato)

Se è già stata configurata una soluzione di accesso Single Sign-On per le identità locali, scegliere **Accesso collegato**. Questa opzione consente alle soluzioni SSO esistenti di Azure Active Directory tooleverage, ma ancora consente agli utenti di applicazione toohello di accesso remoto. 

Per altre informazioni sul linked sign-on (accesso collegato), noto formalmente come Single Sign-On esistente, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

## <a name="integrated-windows-authentication"></a>Autenticazione integrata di Windows

Se le applicazioni locali utilizzano Authentication(IWA) integrata di Windows o se si desidera toouse delega vincolata Kerberos (KCD) per single sign-on, scegliere **autenticazione integrata di Windows**. Con questa opzione, gli utenti devono solo tooauthenticate tooAzure Active Directory e quindi connettore Proxy dell'applicazione hello rappresenta hello utente tooget un token Kerberos e Accedi toohello applicazione. 

Per informazioni sulla configurazione dell'autenticazione di Windows integrata, vedere [Delega vincolata Kerberos per l'accesso Single Sign-On con il proxy di applicazione](active-directory-application-proxy-sso-using-kcd.md).

## <a name="header-based-sign-on"></a>Accesso basato su intestazione 

Se le applicazioni usano le intestazioni per l'autenticazione, scegliere **Accesso basato su intestazione**. Con questa opzione, gli utenti devono solo tooauthentication hello Azure Active Directory. I partner Microsoft con un servizio di autenticazione di terze parti chiamato PingAccess, in cui convertire i token di accesso di Azure Active Directory hello in un formato di intestazione per un'applicazione hello. 

Per informazioni sulla configurazione dell'autenticazione basata su intestazione, vedere [Autenticazione basata su intestazione per l'accesso Single Sign-On con il proxy di applicazione](application-proxy-ping-access.md).

## <a name="next-steps"></a>Passaggi successivi

- [Insieme di credenziali delle password per l'accesso Single Sign-On con il proxy di applicazione](application-proxy-sso-azure-portal.md)
- [Delega vincolata Kerberos per l'accesso Single Sign-On con il proxy di applicazione](active-directory-application-proxy-sso-using-kcd.md)
- [Autenticazione basata su intestazione per l'accesso Single Sign-On con il proxy di applicazione](application-proxy-ping-access.md) 
