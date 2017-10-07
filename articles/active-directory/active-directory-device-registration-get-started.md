---
title: aaaHow tooconfigure la registrazione automatica dei dispositivi appartenenti a un dominio di Windows con Azure Active Directory | Documenti Microsoft
description: Configurare i server appartenenti a un dominio Windows dispositivi tooregister automatico e invisibile con Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>Introduzione a Registrazione dispositivo Azure Active Directory

Registrazione dispositivo di Azure Active Directory è foundation hello per gli scenari di accesso condizionale basato su dispositivo. Quando un dispositivo viene registrato, registrazione dispositivo Azure Active Directory fornisce dispositivo hello con un'identità che è dispositivo hello tooauthenticate usato quando hello utente accede. dispositivo Hello autenticato e gli attributi di hello del dispositivo hello, possono quindi essere tooenforce utilizzato Criteri di accesso condizionale per le applicazioni ospitate nel cloud hello e locale.

Se combinato con una soluzione di management(MDM) di dispositivi mobili, ad esempio Microsoft Intune, sugli attributi del dispositivo hello in Azure Active Directory vengono aggiornati con informazioni aggiuntive sul dispositivo di hello. Ciò consente di regole di accesso condizionale toocreate che impongono l'accesso da dispositivi toomeet agli standard di sicurezza e conformità. Per altre informazioni sulla registrazione dei dispositivi in Microsoft Intune, vedere l'articolo "Registrare i dispositivi per la gestione in Intune".
Gli scenari consentiti da Registrazione dispositivo Azure Active Directory includono il supporto per dispositivi iOS, Android e Windows. Hello singoli scenari in cui viene utilizzata la registrazione del dispositivo di Azure Active Directory potrebbero essere più specifici requisiti e piattaforme supportano. 

Questi scenari sono i seguenti:

- **Accesso condizionale per applicazioni di Office 365 con Microsoft Intune:** gli amministratori IT possono effettuare il provisioning di accesso condizionale dispositivo criteri toosecure alle risorse aziendali, mentre in hello la stessa ora che consente agli information worker su dispositivi conformi servizi di hello tooaccess. Per altre informazioni, vedere Criteri di accesso condizionale dei dispositivi per i servizi di Office 365.

- **Tooapplications di accesso condizionale che sono ospitati in locale:** è possibile utilizzare i dispositivi registrati con criteri di accesso per le applicazioni che vengono configurate toouse AD FS con Windows Server 2012 R2. Per altre informazioni su come configurare l'accesso condizionale in locale, vedere [Configurazione dell'accesso condizionale locale usando il servizio Registrazione dispositivo di Azure Active Directory](active-directory-device-registration-on-premises-setup.md).

## <a name="setting-up-azure-active-directory-device-registration"></a>Configurazione della Registrazione dispositivo di Azure Active Directory

registrazione dei dispositivi toosetup, sono disponibili diverse opzioni:

- Possono registrare dispositivi quando dominio unita in join tooAzure Active Directory. Per ulteriori informazioni su questo argomento, è possibile ulteriori informazioni sulle impostazioni di aggiunta ad Azure AD e hello necessari per il dominio di Azure AD toojoin gli utenti.

- È possibile registrare dispositivi quando gli utenti di aggiungere lavoro o scuola account tooWindows in un dispositivo personale o quando i dispositivi mobili si connettono alle risorse di lavoro tooa richiedere la registrazione. tooensure, è necessario abilitare registrazione dispositivo di Azure Active Directory nel portale di Azure hello. 

- Registrazione automatica dei dispositivi per i computer aggiunti a un dominio tradizionale. tooensure, prima di continuare con la registrazione automatica dei dispositivi, è necessario prima il programma di installazione Azure AD Connect.

Per istruzioni più recenti, vedere [come tooconfigure la registrazione automatica di Windows appartenenti a un dominio dispositivi con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).  
È anche possibile esaminare e abilitare o disabilitare i dispositivi registrati mediante hello portale dell'amministratore in Azure Active Directory.

## <a name="enable-hello-azure-active-directory-device-registration-service"></a>Abilitare il servizio registrazione dispositivo di Azure Active Directory hello

**hello tooenable servizio Registrazione dispositivi di Azure Active Directory:**

1.  Accedi toohello portale Microsoft Azure come amministratore.

2.  Nel riquadro sinistro di hello selezionare **Active Directory**.

3.  Nella scheda Directory hello, selezionare la directory.

4.  Fare clic su **Configure**.

5.  Scorrere troppo**dispositivi**.

6.  Selezionare Tutti per Gli utenti possono registrare i propri dispositivi in Azure AD.

7.  Selezionare il numero massimo di hello di dispositivi desiderato tooauthorize per ogni utente.

registrazione di Hello con Microsoft Intune o gestione dei dispositivi mobili per Office 365 richiede la registrazione del dispositivo. Se è stato configurato uno di questi servizi, sarà selezionata l'opzione **Tutti** e disabilitata l'opzione **Nessuno**. Verificare che siano configurati correttamente e che dispone della licenza hello appropriata.

Per impostazione predefinita, l'autenticazione a due fattori non è abilitato per servizio hello. L'autenticazione a due fattori è tuttavia consigliabile quando si registra un dispositivo.

- Prima di richiedere l'autenticazione a due fattori per questo servizio, è necessario configurare un provider di autenticazione a due fattori in Azure Active Directory e configurare gli account utente per multi-Factor Authentication, vedere Aggiunta di multi-Factor Authentication tooAzure Active Directory

- Se si usa AD FS con Windows Server 2012 R2, è necessario configurare un modulo di autenticazione a due fattori in AD FS. Vedere l'articolo relativo all'uso di Multi-Factor Authentication con Active Directory Federation Services.

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>Visualizzare e gestire gli oggetti dispositivo di Azure Active Directory

Portale dell'amministratore di Azure hello possono visualizzare, bloccare e sbloccare i dispositivi. Un dispositivo bloccato non sarà più possibile tooapplications di accesso che sono configurati tooallow solo i dispositivi registrati.

**tooview e gestire gli oggetti dispositivo in Azure Active Directory:**
 
1.  Accedere toohello portale Microsoft Azure come amministratore.

2.  Nel riquadro sinistro di hello selezionare **Active Directory**.

3.  Selezionare la propria directory.

4.  Selezionare **Utenti**. 

5.  Fare clic su utente hello per cui si desidera dispositivi hello toosee.

6.  Selezionare **Dispositivi**.

7.  Selezionare **Dispositivi registrati**.

A questo punto, è possibile esaminare, bloccare o sbloccare i dispositivi registrati dell'utente hello.
I dispositivi Windows 10 che sono locali appartenenti a un dominio e registrati automaticamente non vengono visualizzati nella scheda utenti hello. Utilizzare toofind di comando PowerShell Get-MsolDevice hello tutti i dispositivi dell'organizzazione. 


## <a name="next-steps"></a>Passaggi successivi

toosetup automatizzata registrazione dei dispositivi, vedere [come tooconfigure la registrazione automatica di Windows appartenenti a un dominio dispositivi con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).


