---
title: ruoli di amministratore aaaAssigning in Azure Active Directory | Documenti Microsoft
description: Un ruolo di amministratore possa essere toocreate usato o modificare gli utenti, assegnare ruoli amministrativi, reimpostare le password utente, gestire le licenze utente o gestire i domini. Un utente viene assegnato un ruolo di amministratore ha hello delle stesse autorizzazioni su tutti i toowhich di servizi cloud sottoscritti dall'organizzazione.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7fc27e8e-b55f-4194-9b8f-2e95705fb731
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.reviewer: Vince.Smith
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: b96350c7264e6ad3620272e015ed9756b512dc4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assigning-administrator-roles-in-azure-active-directory"></a>Assegnazione dei ruoli di amministratore in Azure Active Directory
> [!div class="op_single_selector"]
> * [Portale di Azure]()
> * [portale di Azure classico](active-directory-assign-admin-roles.md)
>
>

Utilizzare amministratori di Azure Active Directory (Azure AD) toodesignate diversi per diverse funzioni. Tali amministratori possono accedere alle funzionalità selezionate nel portale di Azure classico o di hello portale di Azure e, a seconda del ruolo, verrà essere in grado di toocreate o modificare gli utenti, assegnare ruoli amministrativi tooothers, reimpostare le password utente, gestire le licenze utente e gestire domini, tra l'altro. Un utente è assegnato un ruolo di amministratore avrà hello delle stesse autorizzazioni in tutti toowhich di servizi cloud hello sottoscritti dall'organizzazione, indipendentemente dal fatto se si assegna ruolo hello nel portale di Office 365 hello o nel portale di Azure classico hello o usando modulo Hello Azure AD PowerShell Microsoft.

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo. Per modalità tooassign i ruoli di amministratore in Azure AD salve center, vedere [l'assegnazione di ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md).


sono disponibile i seguenti ruoli di amministratore Hello:

* **Amministratore fatturazione**: effettua acquisti, gestisce le sottoscrizioni, gestisce i ticket di supporto e monitora l'integrità del servizio.

* **Amministratore conformità**: gli utenti con questo ruolo dispongano delle autorizzazioni di gestione all'interno di Office 365 sicurezza hello & centro conformità e il centro di amministrazione di Exchange. Per altre informazioni vedere [Informazioni sui ruoli di amministratore di Office 365](https://support.office.com/en-us/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Amministratore di accesso condizionale**: gli utenti con questo ruolo hanno impostazioni di accesso condizionale di hello possibilità toomanage Azure Active Directory.

* **Amministratore del servizio CRM**: gli utenti con questo ruolo dispongono delle autorizzazioni globali all'interno di Microsoft CRM Online, quando il servizio di hello è presente, nonché hello possibilità toomanage i ticket di supporto e monitorare l'integrità del servizio. Per altre informazioni vedere [Informazioni sui ruoli di amministratore di Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Amministratori dispositivo**: gli utenti con questo ruolo diventano amministratori del computer locale in tutti i dispositivi Windows 10 vengono unite in join tooAzure Active Directory. Disporre gli oggetti di hello possibilità toomanage dispositivi in Azure Active Directory.

* **Lettori di directory**: si tratta di un ruolo legacy tooapplications toobe assegnato che non supportano hello [il Framework di consenso](active-directory-integrating-applications.md). Non deve essere assegnato agli utenti di tooany.

* **Account di sincronizzazione della directory**: non usare. Questo ruolo viene assegnato automaticamente servizio Connect di Azure AD toohello e non è intenzionale o per qualsiasi altro utilizzo è supportato.

* **I writer directory**: si tratta di un ruolo legacy tooapplications toobe assegnato che non supportano hello [il Framework di consenso](active-directory-integrating-applications.md). Non deve essere assegnato agli utenti di tooany.

* **Amministratore del servizio Exchange**: gli utenti con questo ruolo dispongono delle autorizzazioni globali all'interno di Microsoft Exchange Online, quando il servizio hello è presente. Per altre informazioni vedere [Informazioni sui ruoli di amministratore di Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Amministratore globale o amministratore della società**: gli utenti con questo ruolo hanno accesso alle funzionalità di amministrazione tooall in Azure Active Directory, nonché servizi che tooAzure federazione Active Directory come Online Exchange, SharePoint Online, e Skype for Business Online. persona Hello che effettua l'iscrizione per il tenant di Azure Active Directory hello diventa un amministratore globale. Solo gli amministratori globali possono assegnare altri ruoli di amministratore. In una società possono essere presenti più amministratori globali. Gli amministratori globali possono reimpostare password hello per tutti gli utenti e tutti gli altri amministratori.

  > [!NOTE]
  > In Microsoft API Graph, Azure AD API Graph e Azure AD PowerShell, questo ruolo è identificato come "Amministratore società". È "Amministratore globale" hello [portale di Azure](https://portal.azure.com).
  >
  >

* **Mittente dell'invito guest**: gli utenti in questo ruolo possono gestire gli inviti di utente guest B2B di Azure Active Directory quando hello "Membri è possono invitare" utente impostazione tooNo. Ulteriori informazioni su collaborazione B2B in [sull'anteprima di collaborazione Azure AD B2B hello](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b). Il ruolo non include altre autorizzazioni.

* **Amministratore del servizio Intune**: gli utenti con questo ruolo dispongono delle autorizzazioni globali all'interno di Microsoft Intune Online quando servizio hello è presente. Inoltre, questo ruolo contiene hello possibilità toomanage utenti e dispositivi in Criteri di tooassociate ordine, nonché creare e gestire gruppi.

* **Amministratore della cassetta postale**: questo ruolo viene usato solo nell'ambito del supporto per la posta elettronica di Exchange Online per dispositivi RIM Blackberry. Se l'organizzazione non usa la posta elettronica di Exchange Online in dispositivi RIM Blackberry, non usare questo ruolo.

* **Partner Tier 1 Support** (Supporto di livello 1 partner): non usare. Questo ruolo è stato deprecato e verrà rimossa da Azure AD in hello future. Il ruolo è riservato a pochi partner Microsoft per la rivendita e non è disponibile per un uso generale.

* **Partner Tier 2 Support** (Supporto di livello 2 partner): non usare. Questo ruolo è stato deprecato e verrà rimossa da Azure AD in hello future. Il ruolo è riservato a pochi partner Microsoft per la rivendita e non è disponibile per un uso generale.

* **Amministratore password/Amministratore supporto tecnico**: gli utenti con questo ruolo possono reimpostare le password, gestire le richieste di servizio e monitorare l'integrità del servizio. Gli amministratori password possono reimpostare le password solo per gli utenti e gli altri amministratori password.

  > [!NOTE]
  > In Microsoft Graph API, Azure AD Graph API e Azure AD PowerShell, questo ruolo è identificato come "Amministratore supporto tecnico". È "Password Administrator" hello [portale di Azure](https://portal.azure.com/).
  >
  >
  
* **Amministratore del servizio Power BI**: gli utenti con questo ruolo dispongono delle autorizzazioni globali all'interno di Microsoft Power BI, quando il servizio di hello è presente, nonché hello possibilità toomanage i ticket di supporto e monitorare l'integrità del servizio. Per altre informazioni vedere [Informazioni sui ruoli di amministratore di Office 365](https://support.office.com/en-us/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d?ui=en-US&rs=en-001&ad=US).

* **Amministratore del ruolo con privilegi**: gli utenti con questo ruolo possono gestire le assegnazioni dei ruoli in Azure Active Directory e in Azure AD Privileged Identity Management. Inoltre, questo ruolo consente la gestione di tutti gli aspetti di Privileged Identity Management.

* **Amministratore della sicurezza**: gli utenti con questo ruolo hanno le autorizzazioni di sola lettura hello del ruolo di lettore sicurezza hello e configurazione di toomanage hello possibilità per i servizi correlati alla sicurezza: la protezione dell'identità Azure Active Directory, Azure Protezione delle informazioni, gestione identità con privilegi e sulla protezione di Office 365 & centro conformità. Ulteriori informazioni sulle autorizzazioni di Office 365 sono disponibile all'indirizzo [le autorizzazioni di sicurezza di Office 365 hello & centro conformità](https://support.office.com/en-us/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1).

* **Lettore di sicurezza**: gli utenti con questo ruolo dispone globale accesso in sola lettura, incluse tutte le informazioni in Azure Active Directory, la protezione dell'identità, Privileged Identity Management, nonché hello possibilità tooread Azure Active Directory Accedi i report e i log di controllo. Hello concede inoltre dell'autorizzazione di sola lettura nel centro di conformità e sicurezza di Office 365. Ulteriori informazioni sulle autorizzazioni di Office 365 sono disponibile all'indirizzo [le autorizzazioni di sicurezza di Office 365 hello & centro conformità](https://support.office.com/en-us/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1).

* **Amministratore del servizio supporta**: gli utenti con questo ruolo possono aprire le richieste di assistenza con Microsoft per i servizi di Azure e Office 365 e visualizzazioni hello center dashboard e il messaggio di servizio nel portale di Azure hello e il portale di amministrazione di Office 365. Per altre informazioni vedere [Informazioni sui ruoli di amministratore di Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Amministratore del servizio SharePoint**: gli utenti con questo ruolo dispongono delle autorizzazioni globali all'interno di Microsoft SharePoint Online, quando il servizio di hello è presente, nonché hello possibilità toomanage i ticket di supporto e monitorare l'integrità del servizio. Per altre informazioni vedere [Informazioni sui ruoli di amministratore di Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Skype for Business o amministratore del servizio Lync**: gli utenti con questo ruolo dispone delle autorizzazioni globali all'interno di Microsoft Skype for Business, quando il servizio hello è presente, nonché gestire gli attributi di utente Skype specifici in Azure Active Directory. Inoltre, questo ruolo concede il ticket supporto di hello possibilità toomanage e monitoraggio del servizio integrità. Per altre informazioni vedere [Informazioni sui ruoli di amministratore di Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

  > [!NOTE]
  > In Microsoft Graph API, Azure AD Graph API e Azure AD PowerShell, questo ruolo è identificato come "Amministratore del sevizio Lync". È "Skype per Business amministratore del servizio" hello [portale di Azure](https://portal.azure.com/).
  >
  >

* **Amministratore account utente**: gli utenti con questo ruolo possono creare e gestire tutti gli aspetti degli utenti e dei gruppi. Inoltre, questo ruolo include il ticket di supporto toomanage possibilità hello e monitor del servizio integrità. Si applicano alcune restrizioni. Ad esempio, questo ruolo non consente l'eliminazione di un amministratore globale e mentre consente la modifica delle password per utenti non amministratori, non consente la modifica delle password per gli amministratori globali o altri amministratori con privilegi.

## <a name="administrator-permissions"></a>Autorizzazioni degli amministratori

### <a name="billing-administrator"></a>Amministratore fatturazione

| Operazione consentita | Operazione non consentita |
| --- | --- |
|<p>Visualizzare informazioni aziendali e sugli utenti</p><p>Gestire ticket di supporto di Office</p><p>Eseguire operazioni di fatturazione e acquisto per prodotti Office</p> |<p>Reimpostare le password utente</p><p>Creare e gestire visualizzazioni utente</p><p>Creare, modificare ed eliminare utenti e gruppi e gestire licenze utente</p><p>Gestire domini</p><p>Gestire informazioni aziendali</p><p>Delegare ruoli amministrativi tooothers</p><p>Usare la sincronizzazione delle directory</p><p>Visualizzare i log di controllo</p>|

### <a name="conditional-access-administrator"></a>Amministratore di accesso condizionale
| Operazione consentita | Operazione non consentita |
| --- | --- |
|<p>Visualizzare informazioni aziendali e sugli utenti</p><p>Gestire le impostazioni di accesso condizionale</p> |<p>Reimpostare le password utente</p><p>Creare e gestire visualizzazioni utente</p><p>Creare, modificare ed eliminare utenti e gruppi e gestire licenze utente</p><p>Gestire domini</p><p>Gestire informazioni aziendali</p><p>Delegare ruoli amministrativi tooothers</p><p>Usare la sincronizzazione delle directory</p><p>Visualizzare i log di controllo</p>|

### <a name="global-administrator"></a>Amministratore globale
| Operazione consentita | Operazione non consentita |
| --- | --- |
|<p>Visualizzare informazioni aziendali e sugli utenti</p><p>Gestire ticket di supporto di Office</p><p>Eseguire operazioni di fatturazione e acquisto per prodotti Office</p><p>Reimpostare le password utente</p><p>Reimpostare le password di altri amministratori</p><p>Creare e gestire visualizzazioni utente</p><p>Creare, modificare ed eliminare utenti e gruppi e gestire licenze utente</p><p>Gestire domini</p><p>Gestire informazioni aziendali</p><p>Delegare ruoli amministrativi tooothers</p><p>Usare la sincronizzazione delle directory</p><p>Abilitare o disabilitare l'autenticazione a più fattori</p><p>Visualizzare i log di controllo</p> |<p>N/D</p>|

### <a name="password-administrator"></a>Amministratore password
| Operazione consentita | Operazione non consentita |
| --- | --- |
| <p>Visualizzare informazioni aziendali e sugli utenti</p><p>Gestire ticket di supporto di Office</p><p>Reimpostare le password utente</p> <p>Reimpostare le password di altri amministratori</p>|<p>Eseguire operazioni di fatturazione e acquisto per prodotti Office</p><p>Creare e gestire visualizzazioni utente</p><p>Creare, modificare ed eliminare utenti e gruppi e gestire licenze utente</p><p>Gestire domini</p><p>Gestire informazioni aziendali</p><p>Delegare ruoli amministrativi tooothers</p><p>Usare la sincronizzazione delle directory</p><p>Visualizzazione dei report</p>|

### <a name="service-administrator"></a>Amministratore del servizio
| Operazione consentita | Operazione non consentita |
| --- | --- |
| <p>Visualizzare informazioni aziendali e sugli utenti</p><p>Gestire ticket di supporto di Office</p> |<p>Reimpostare le password utente</p><p>Eseguire operazioni di fatturazione e acquisto per prodotti Office</p><p>Creare e gestire visualizzazioni utente</p><p>Creare, modificare ed eliminare utenti e gruppi e gestire licenze utente</p><p>Gestire domini</p><p>Gestire informazioni aziendali</p><p>Delegare ruoli amministrativi tooothers</p><p>Usare la sincronizzazione delle directory</p><p>Visualizzare i log di controllo</p> |

### <a name="user-administrator"></a>Amministratore utenti
| Operazione consentita | Operazione non consentita |
| --- | --- |
| <p>Visualizzare informazioni aziendali e sugli utenti</p><p>Gestire ticket di supporto di Office</p><p>Reimpostare le password utente, con alcune limitazioni.</p><p>Reimpostare le password di altri amministratori</p><p>Reimpostare le password di altri utenti</p><p>Creare e gestire visualizzazioni utente</p><p>Creare, modificare ed eliminare utenti e gruppi, nonché gestire le licenze utente, con alcune limitazioni. Non può eliminare un amministratore globale o creare altri amministratori.</p> |<p>Eseguire operazioni di fatturazione e acquisto per prodotti Office</p><p>Gestire domini</p><p>Gestire informazioni aziendali</p><p>Delegare ruoli amministrativi tooothers</p><p>Usare la sincronizzazione delle directory</p><p>Abilitare o disabilitare l'autenticazione a più fattori</p><p>Visualizzare i log di controllo</p> |

### <a name="security-reader"></a>Ruolo con autorizzazioni di lettura per la sicurezza
| In | Operazione consentita |
| --- | --- |
| Centro di Identity Protection |Leggere tutte le informazioni sulle impostazioni e sui report di sicurezza per le funzionalità di sicurezza<ul><li>Filtro posta indesiderata<li>Crittografia<li>Prevenzione della perdita dei dati<li>Antimalware<li>Protezione avanzata dalle minacce<li>Anti-phishing<li>Regole del flusso di posta |
| Privileged Identity Management |<p>Contiene informazioni di accesso in sola lettura tooall esposte in Azure AD PIM: criteri e i report per le assegnazioni di ruolo di Azure AD, sicurezza esamina e in hello futuro leggere toopolicy accedere ai dati e report per gli scenari oltre all'assegnazione di ruolo di Azure AD.<p>**Non è possibile** iscriversi a Azure AD PIM o apportare eventuali modifiche di tooit. Nel portale di PIM o tramite PowerShell, un utente in questo ruolo possa attivare ruoli aggiuntivi (ad esempio, amministratore globale o amministratore con privilegi di ruolo), se l'utente di hello è un candidato per la loro. |
| <p>Monitorare l'integrità del servizio Office 365</p><p>Centro sicurezza e conformità di Office 365</p> |<ul><li>Leggere e gestire gli avvisi<li>Leggere i criteri di sicurezza<li>Leggere i dati di intelligence sulle minacce, usare Cloud App Discovery e mettere in quarantena in ricerca e analisi<li>Leggere tutti i report |

### <a name="security-administrator"></a>Amministratore della sicurezza
| In | Operazione consentita |
| --- | --- |
| Centro di Identity Protection |<ul><li>Tutte le autorizzazioni del ruolo di sicurezza Reader di hello.<li>Inoltre, hello possibilità tooperform tutte le operazioni IPC ad eccezione di reimpostazione delle password. |
| Privileged Identity Management |<ul><li>Tutte le autorizzazioni del ruolo di sicurezza Reader di hello.<li>**Non consente** di gestire le impostazioni o le appartenenze ai ruoli di Azure AD. |
| <p>Monitorare l'integrità del servizio Office 365</p><p>Centro sicurezza e conformità di Office 365 |<ul><li>Tutte le autorizzazioni del ruolo di sicurezza Reader di hello.<li>Configurare tutte le impostazioni nella funzionalità di Advanced Threat Protection hello (protezione da malware e virus, dannoso URL configurazione, la traccia di URL e così via). |

## <a name="details-about-hello-global-administrator-role"></a>Dettagli sul ruolo di amministratore globale di hello
amministratore globale di Hello ha le funzionalità amministrative tooall di accesso. Per impostazione predefinita, chi hello effettua l'iscrizione per una sottoscrizione di Azure viene assegnato il ruolo di amministratore globale hello per directory hello. Solo gli amministratori globali possono assegnare altri ruoli di amministratore.

### <a name="tooadd-a-colleague-as-a-global-administrator"></a>tooadd un collega come amministratore globale

1. Accedi toohello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com) con un account che sia un amministratore globale per la directory tenant hello.

   ![Apertura dell'interfaccia di amministrazione di Azure AD](./media/active-directory-assign-admin-roles/active-directory-admin-center.png)

2. Selezionare **Users and groups (Utenti e gruppi) &gt; All users** (Tutti gli utenti)

3. Trova utente hello desiderato toodesignate come amministratore globale e aprire il pannello hello per tale utente.

4. Nel Pannello di hello utente, selezionare **ruolo della Directory**.
 
5. Nel pannello dei ruoli directory hello, selezionare hello **amministratore globale** ruolo e salvare.

## <a name="assign-or-remove-administrator-roles"></a>Assegnare o rimuovere ruoli di amministratore
toolearn tooassign ruoli amministrativi tooa utente in Azure Active Directory, vedere [assegnare un utente tooadministrator ruoli in Azure Active Directory](active-directory-users-assign-role-azure-portal.md).

## <a name="deprecated-roles"></a>Ruoli deprecati

Hello seguenti ruoli non deve essere utilizzato. È stata deprecata e verrà rimossa da Azure AD in hello future.

* Amministratore di licenze ad hoc
* Autore di utenti verificati tramite posta elettronica
* Aggiunta di dispositivi
* Gestione dispositivi
* Utenti di dispositivi
* Aggiunta di dispositivi all'area di lavoro

## <a name="next-steps"></a>Passaggi successivi
* toolearn ulteriori informazioni sugli amministratori toochange per una sottoscrizione di Azure, vedere [come tooadd o modificare i ruoli di amministratore di Azure](../billing-add-change-azure-subscription-administrator.md)
* toolearn ulteriori informazioni sulla modalità di controllo di accesso alle risorse in Microsoft Azure, vedere [informazioni di accesso alle risorse di Azure](active-directory-understanding-resource-access.md)
* Per ulteriori informazioni sulla correlazione tooyour sottoscrizione di Azure da parte di Azure Active Directory, vedere [delle sottoscrizioni Azure sono associate con Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
* [Gestire gli utenti](active-directory-create-users.md)
* [Gestire le password](active-directory-manage-passwords.md)
* [Gestire i gruppi](active-directory-manage-groups.md)
