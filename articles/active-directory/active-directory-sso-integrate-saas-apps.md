---
title: aaaIntegrate Azure Active Directory single sign-on con le app SaaS | Documenti Microsoft
description: "Abilitare l'autenticazione Single Sign-On e la gestione dell’accesso centralizzata per il provisioning degli utenti delle app SaaS in Azure Active Directory. Cenni preliminari sull'app di tooSaaS toointegrate Azure Active Directory."
services: active-directory
keywords: Integrare Azure AD con app SaaS
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 53b9d341-d1fc-4bbb-ac7c-3f4c68fcf00a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: aaronsm
ms.openlocfilehash: fe621a30429c81c32470635d105ae3e95184efa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-single-sign-on-with-saas-apps"></a>Integrare i servizi Single Sign-On di Azure Active Directory nelle app SaaS
> [!div class="op_single_selector"]
> * [Portale di Azure](active-directory-enterprise-apps-manage-sso.md)
> * [portale di Azure classico](active-directory-sso-integrate-saas-apps.md)
>
>

[!INCLUDE [active-directory-sso-use-case-intro](../../includes/active-directory-sso-use-case-intro.md)]

tooget avviato l'impostazione di single sign-on per un'applicazione che sta rendere l'organizzazione, si utilizzerà una directory esistente in Azure Active Directory (Azure AD). È possibile usare una directory di Azure AD ottenuta tramite Microsoft Azure, Office 365 o Windows Intune. Se si dispone di due o più di questi, vedere [amministrare la directory di Azure AD](active-directory-administer.md) toodetermine quali uno toouse.

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo. Per modalità tooassign i ruoli di amministratore in Azure AD salve center, vedere [l'assegnazione di ruoli di amministratore in Azure Active Directory](active-directory-enterprise-apps-manage-sso.md).

## <a name="authentication"></a>Autenticazione
Per le applicazioni che supportano hello SAML 2.0, WS-Federation, o i protocolli di OpenID Connect, Azure Active Directory utilizza le relazioni di trust tooestablish certificati di firma. Per altre informazioni su questo aspetto, vedere [Gestione dei certificati per Single Sign-On federato](active-directory-sso-certs.md).

Per le applicazioni che supportano solo HTML basata su form Accedi, tooestablish 'archiviazione password' di Azure Active Directory utilizza le relazioni di trust. Questo consente agli utenti di hello in toobe l'organizzazione automaticamente connesso tooa applicazione SaaS da Azure AD con informazioni sull'account utente di hello da hello applicazione SaaS. Azure AD raccoglie e archivia in modo sicuro informazioni sull'account utente di hello e la password correlata hello. Per altre informazioni, vedere [Single Sign-On basato su password](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).

## <a name="authorization"></a>Authorization
Un account di provisioning consente un toouse toobe autorizzato utente un'applicazione dopo che sono autenticati tramite l'accesso single sign-on. Il provisioning dell'utente può essere eseguito manualmente o in alcuni casi è possibile aggiungere e rimuovere le informazioni utente da app SaaS hello in base alle modifiche apportate in Azure Active Directory. Per altre informazioni sull'uso dei connettori di Azure AD esistenti per il provisioning automatico, vedere [Automatizzare il provisioning e il deprovisioning utenti in applicazioni SaaS con Azure Active Directory](active-directory-saas-app-provisioning.md).

In caso contrario, è possibile manualmente aggiungere app tooan di informazioni utente, o usare altre soluzioni di provisioning che sono disponibili in marketplace hello.

## <a name="access"></a>Accesso
Azure AD fornisce diversi modi personalizzabili toodeploy applicazioni tooend utenti dell'organizzazione. Non è obbligatorio usare soluzioni specifiche per la distribuzione o l'accesso. È possibile utilizzare [hello soluzione più adatta alle proprie esigenze](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).

## <a name="additional-considerations-for-applications-already-in-use"></a>Considerazioni aggiuntive per le applicazioni già in uso.
Configurando l'accesso single sign in un'applicazione che usa già l'organizzazione è un processo diverso dal processo di hello di creazione di nuovi account per una nuova applicazione. Esistono un paio di passaggi preliminari tra cui: mapping delle identità utente nell'identità di tooAzure AD applicazione hello e di comprendere come gli utenti otterranno la registrazione nell'applicazione tooan dopo l'integrazione.

> [!NOTE]
> tooset di SSO per un'applicazione esistente, è necessario disporre di diritti di amministratore globale toohave in entrambi Azure AD e hello applicazione SaaS.
>
>

### <a name="mapping-user-accounts"></a>Mapping degli account utente
Un'identità utente ha in genere un identificatore univoco che può essere un indirizzo di posta elettronica o un nome dell'entità utente (UPN). Sarà necessario toolink (map) ogni applicazione identità tootheir AD Azure rispettive identità utente. Esistono un paio di modi tooaccomplish questo a seconda di come requisito hello dell'autenticazione dell'applicazione.

Per ulteriori informazioni sull'esecuzione del mapping identità di applicazione con le identità di Azure AD, vedere [personalizzazione di attestazioni rilasciate nel token SAML hello](http://social.technet.microsoft.com/wiki/contents/articles/31257.azure-active-directory-customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps.aspx) e [personalizzazione dei mapping degli attributi per il provisioning](active-directory-saas-customizing-attribute-mappings.md).

### <a name="understanding-hello-users-log-in-experience"></a>Informazioni di accesso dell'utente hello esperienza
Quando si integra SSO per un'applicazione che è già in uso, è importante toorealize che hello esperienza utente sarà interessate. Per tutte le applicazioni, gli utenti inizieranno con loro toosign le credenziali di Azure AD in. È possibile che usano un'applicazione hello tooaccess portale diverso.

SSO per alcune applicazioni può essere eseguita nell'interfaccia di accesso dell'applicazione hello, ma per altre applicazioni, hello utente disporrà toogo tramite un portale centrale, ad esempio ([My Apps](http://myapps.microsoft.com) o [Office365](http://portal.office.com/myapps)) toosign in. Ulteriori informazioni sui tipi diversi di hello di SSO e l'esperienza utente in [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

È un'altra risorsa preziosa *eliminazione consenso dell'utente* in hello [orientamenti sviluppatori](active-directory-applications-guiding-developers-for-lob-applications.md) articolo.

## <a name="next-steps"></a>Passaggi successivi
Per le app SaaS che trova nella raccolta di App hello, Azure AD fornisce una serie di [esercitazioni sull'App SaaS toointegrate](active-directory-saas-tutorial-list.md).

Se l'applicazione non è presente nella raccolta di App, è possibile [aggiungerlo toohello raccolta di App di Azure AD come applicazione personalizzata](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).

È molto più dettagli su tutti questi problemi nella libreria Azure.com hello, a partire da [novità di accesso alle applicazioni e single sign-on con Azure Active Directory?](active-directory-appssoaccess-whatis.md).

Inoltre, non perdete hello [articolo indice per la gestione delle applicazioni in Azure Active Directory](active-directory-apps-index.md).
