---
title: Panoramica di aaaAzure Active Directory device registration | Documenti Microsoft
description: "Registrazione dispositivo di Azure Active Directory è foundation hello per gli scenari di accesso condizionale basato su dispositivo. Quando un dispositivo viene registrato, disposizioni di registrazione dispositivo di Azure Active Directory hello dispositivo con un'identità che è dispositivo hello tooauthenticate usato quando hello utente accede."
services: active-directory
keywords: registrazione dispositivo, abilitare registrazione dispositivo, registrazione dispositivo e software MDM
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 1e92c1a2-01b8-4225-950b-373cd601b035
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: b9846e34fe873d271ebe71cbf8e70c6b4768885b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>Introduzione a Registrazione dispositivo Azure Active Directory
Registrazione dispositivo di Azure Active Directory è foundation hello per gli scenari di accesso condizionale basato su dispositivo. Quando un dispositivo viene registrato, registrazione dispositivo Azure Active Directory fornisce dispositivo hello con un'identità che è dispositivo hello tooauthenticate usato quando hello utente accede. dispositivo Hello autenticato e gli attributi di hello del dispositivo hello, possono quindi essere tooenforce utilizzato Criteri di accesso condizionale per le applicazioni ospitate nel cloud hello e locale.

Se combinato con una soluzione di management(MDM) di dispositivi mobili, ad esempio Microsoft Intune, sugli attributi del dispositivo hello in Azure Active Directory vengono aggiornati con informazioni aggiuntive sul dispositivo di hello. Ciò consente di regole di accesso condizionale toocreate che impongono l'accesso da dispositivi toomeet agli standard di sicurezza e conformità. Per altre informazioni sulla registrazione dei dispositivi in Microsoft Intune, vedere [Registrare i dispositivi per la gestione in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).

## <a name="scenarios-enabled-by-azure-active-directory-device-registration"></a>Scenari consentiti da Registrazione dispositivo Azure Active Directory
Registrazione dispositivo Azure Active Directory include il supporto per dispositivi iOS, Android e Windows. Hello singoli scenari in cui viene utilizzata la registrazione del dispositivo Azure Active Directory potrebbero essere più specifici requisiti e piattaforme supportano. Questi scenari sono i seguenti:

* **Tooapplications di accesso condizionale che sono ospitati in locale**: È possibile utilizzare i dispositivi registrati con criteri di accesso per le applicazioni che vengono configurate toouse AD FS con Windows Server 2012 R2. Per altre informazioni su come configurare l'accesso condizionale in locale, vedere [Configurazione dell'accesso condizionale locale usando il servizio Registrazione dispositivo di Azure Active Directory](active-directory-device-registration-on-premises-setup.md).
* **Accesso condizionale per applicazioni di Office 365 con Microsoft Intune** : gli amministratori IT possono effettuare il provisioning di accesso condizionale dispositivo criteri toosecure alle risorse aziendali, mentre in hello la stessa ora che consente agli information worker su dispositivi conformi servizi di hello tooaccess. Per altre informazioni, vedere [Criteri di accesso condizionale dei dispositivi per i servizi di Office 365](active-directory-conditional-access-device-policies.md).

## <a name="setting-up-azure-active-directory-device-registration"></a>Configurazione di Registrazione dispositivo Azure Active Directory
È necessario registrazione dispositivo di Azure AD tooenable nel portale di Azure hello in modo che i dispositivi mobili possono individuare il servizio hello cercando record DNS noti. È necessario configurare il DNS della società in modo che i dispositivi Windows 10, Windows 8.1, Windows 7, Android e iOS è possano individuare e usare servizio hello.
Puoi visualizzare e abilitare o disabilitare i dispositivi registrati mediante hello portale dell'amministratore in Azure Active Directory.

> [!NOTE]
> Per istruzioni più recenti su come visualizzare tooset di registrazione automatica dei dispositivi, [toosetup la registrazione automatica del dominio di Windows modalità unite in join i dispositivi con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).
> 
> 

### <a name="enable-azure-active-directory-device-registration-service"></a>Abilitare il servizio Registrazione dispositivo Azure Active Directory
1. Accedi toohello portale Microsoft Azure come amministratore.
2. Nel riquadro sinistro di hello selezionare **Active Directory**.
3. In hello **Directory** scheda, selezionare la directory.
4. Seleziona hello **configura** scheda.
5. Scorrere toohello sezione denominata **dispositivi**.
6. Selezionare **Tutti** per **Gli utenti possono aggiungere dispositivi all'area di lavoro**.
7. Selezionare il numero massimo di hello di dispositivi desiderato tooauthorize per ogni utente.

> [!NOTE]
> La registrazione con Microsoft Intune o con Gestione dispositivi mobili per Office 365 richiede l'aggiunta all'area di lavoro. Se è stato configurato uno di questi servizi, viene selezionata e hello NONE pulsante è disabilitato.
> 
> 

Per impostazione predefinita, l'autenticazione a due fattori non è abilitato per servizio hello. L'autenticazione a due fattori è tuttavia consigliabile quando si registra un dispositivo.

* Prima di richiedere l'autenticazione a due fattori per questo servizio, è necessario configurare un provider di autenticazione a due fattori in Azure Active Directory e configurare gli account utente per multi-Factor Authentication, vedere [aggiunta a più fattori Autenticazione tooAzure Active Directory](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* Se si usa AD FS con Windows Server 2012 R2, è necessario configurare un modulo di autenticazione a due fattori in AD FS. Vedere l'articolo relativo all'[uso di Multi-Factor Authentication con Active Directory Federation Services](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="configure-azure-active-directory-device-registration-discovery"></a>Configurare l'individuazione di Registrazione dispositivo Azure Active Directory
I dispositivi Windows 7 e Windows 8.1 individueranno il servizio Registrazione dispositivi di hello grazie alla combinazione di nome dell'account utente hello con un nome di server di registrazione dispositivo noto.

È necessario creare un record DNS CNAME che punta A toohello record associato al servizio registrazione dispositivo di Azure Active Directory. Hello record CNAME deve utilizzare enterpriseregistration prefisso noto hello seguito dal suffisso UPN hello utilizzato da account utente di hello nell'organizzazione. Se l'organizzazione usa più suffissi UPN, è necessario creare più record CNAME nel DNS.

Ad esempio, se si usano due suffissi UPN dell'organizzazione denominato @contoso.com e @region.contoso.com, si creerà hello seguenti record DNS.

| Voce | Tipo | Indirizzo |
| --- | --- | --- |
| enterpriseregistration.contoso.com |CNAME |enterpriseregistration.windows.net |
| enterpriseregistration.region.contoso.com |CNAME |enterpriseregistration.windows.net |

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>Visualizzare e gestire gli oggetti dispositivo di Azure Active Directory
1. Portale dell'amministratore di Azure hello possono visualizzare, bloccare e sbloccare i dispositivi. Un dispositivo bloccato non sarà più possibile tooapplications di accesso che sono configurati tooallow solo i dispositivi registrati.
2. Accedere come amministratore toohello portale di Microsoft Azure.
3. Nel riquadro sinistro di hello selezionare **Active Directory**.
4. Selezionare la propria directory.
5. Seleziona hello **utenti** scheda. Selezionare quindi un utente tooview i propri dispositivi
6. Seleziona hello **dispositivi** scheda.
7. Selezionare **dispositivi registrati** da hello menu a discesa.
8. Qui è possibile visualizzare, bloccare o sbloccare i dispositivi registrati dell'utente hello.

## <a name="additional-topics"></a>Argomenti aggiuntivi
È possibile registrare i dispositivi Windows 7 e Windows 8.1 aggiunti a un dominio con Registrazione dispositivo Azure AD. Hello seguenti argomenti vengono fornite ulteriori informazioni sui prerequisiti di hello e registrazione del dispositivo richiesto tooconfigure passaggi hello nei dispositivi Windows 7 e Windows 8.1.

* [Registrazione automatica dei dispositivi con Azure Active Directory per i dispositivi Windows aggiunti a un dominio](active-directory-conditional-access-automatic-device-registration.md)
* [Registrazione automatica dei dispositivi con Azure Active Directory per i dispositivi Windows 10 aggiunti a un dominio](active-directory-azureadjoin-devices-group-policy.md)

