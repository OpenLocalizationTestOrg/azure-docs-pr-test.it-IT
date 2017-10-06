---
title: aaaHow tooconfigure single sign-on tooan applicazione Proxy dell'applicazione | Documenti Microsoft
description: "Come è possibile configurare applicazione proxy di applicazione single sign-on tooyour rapidamente"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: e1289203177c77b3a8bcc9058c5c0b8ae50f243e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-single-sign-on-tooan-application-proxy-application"></a>Come tooconfigure single sign-on tooan applicazione Proxy di applicazione

Single sign-on (SSO) consente il tooaccess agli utenti un'applicazione senza effettuare l'autenticazione a più volte. Consente di hello autenticazione single toooccur nel cloud hello, in Azure Active Directory e consente servizio hello o connettore tooimpersonate hello utente toocomplete eventuali richieste di autenticazione aggiuntivi da un'applicazione hello.

## <a name="how-tooconfigure-single-sign-on"></a>Come tooconfigure single-sign-on
tooconfigure SSO, verificare innanzitutto che l'applicazione è configurata per la pre-autenticazione tramite Azure Active Directory. toodo, andare troppo**Azure Active Directory**  - &gt; **applicazioni aziendali**  - &gt; **tutte le applicazioni**  - &gt; Applicazione  **- &gt; Proxy dell'applicazione**. In questa pagina viene visualizzato "Pre-autenticazione" hello, campo e assicurarsi che sia troppo "Azure Active Directory. 

Per ulteriori informazioni sui metodi di preautenticazione hello, vedere il passaggio 4 di hello [documento pubblicazione app](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

   ![Metodo di preautenticazione nel portale di Azure](./media/application-proxy-config-sso-how-to/app-proxy.png)

## <a name="configuring-single-sign-on-modes-for-application-proxy-applications"></a>Configurazione delle modalità Single Sign-On per le applicazioni Proxy di applicazione
Successivamente è stato possibile configurare un tipo specifico di hello di single sign-on. Hello sign-on metodi sono classificati in base a cui il tipo di applicazione di back-end hello di autenticazione utilizzato. Le applicazioni Proxy di applicazione supportano tre tipi di accesso:

-   **Password-Sign-On basato su**: Password-sign-on basato su può essere utilizzato per qualsiasi applicazione che utilizza i campi nome utente e password toosign-on. I passaggi per la configurazione sono reperibili nella [documentazione relativa alla configurazione SSO tramite password](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#bring-your-own-password-sso-applications).

-   **Autenticazione integrata di Windows**: per le applicazioni che usano l'autenticazione integrata di Windows (IWA), l'accesso Single Sign-On è abilitato tramite delega vincolata Kerberos (KCD). Ciò consente agli utenti di Active Directory tooimpersonate e toosend connettori Proxy di applicazione e ricevere i token per loro conto. Dettagli su come configurare la delega vincolata Kerberos sono reperibile in hello [Single Sign-On con la documentazione di delega vincolata Kerberos](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd).

-   **Accesso basato su intestazione**: l'accesso basato su intestazione viene abilitato mediante una relazione e non richiede un'ulteriore configurazione. Per informazioni dettagliate sulla relazione hello e istruzioni dettagliate per la configurazione di single sign-on tooan applicazione che utilizza le intestazioni per l'autenticazione, vedere hello [PingAccess per la documentazione di Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).

Ognuna di queste opzioni sono disponibili dall'applicazione tooyour "Applicazioni aziendali" e apertura hello **Single Sign-On** pagina dal menu a sinistra di hello. Si noti che se l'applicazione è stato creato nel portale precedente hello, potrebbe non essere visualizzata tutte queste opzioni.

In questa pagina viene visualizzata inoltre un opzione di accesso aggiuntiva: Linked sign-on (Accesso collegato). Questa opzione è supportata anche da Proxy di applicazione. Si noti tuttavia che questa opzione non aggiunge applicazioni single sign-on toohello. Ciò premesso applicazione hello disponga già di accesso single sign-on implementata utilizzando un altro servizio, ad esempio Active Directory Federation Services. 

Questa opzione consente a un amministratore toocreate un'applicazione tooan collegamento che gli utenti prima visualizzata quando si accede a un'applicazione hello. Ad esempio, se è presente un'applicazione che viene configurato tooauthenticate utenti usando Active Directory Federation Services 2.0, un amministratore può utilizzare hello "collegate" Sign-On opzione toocreate tooit un collegamento nel Pannello di accesso hello.

## <a name="next-steps"></a>Passaggi successivi
[Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione](active-directory-application-proxy-sso-using-kcd.md)
