---
title: aaaOffice 365 condivisione esterna e la collaborazione B2B di Azure Active Directory | Documenti Microsoft
description: Informazioni sul mapping delle attestazioni per Collaborazione B2B in Azure Active Directory
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a>Condivisione esterna di Office 365 e Collaborazione B2B di Azure Active Directory

Condivisione in Office 365 (OneDrive, SharePoint Online, gruppi unificati, e così via) e B2B di Azure Active Directory (Azure AD) sono tecnicamente di collaborazione esterna hello stessa cosa. Condivisione tutti esterna (ad eccezione di OneDrive/SharePoint Online), inclusi gli utenti guest in gruppi di Office 365, Usa già l'invito di collaborazione Azure AD B2B hello API per la condivisione.

La gestione degli inviti di OneDrive/SharePoint Online è separata. Il supporto per la condivisione esterna in OneDrive/SharePoint Online è iniziato prima dello sviluppo del supporto di Azure AD. Nel tempo, la condivisione esterna OneDrive/SharePoint Online sono accumulati diverse funzionalità e diversi milioni di utenti che utilizzano prodotto hello del incorporati modello di condivisione. Rimangono tuttavia alcune sottili differenze di funzionamento tra la condivisione esterna di OneDrive/SharePoint Online e quella di Collaborazione B2B di Azure AD:

- OneDrive o SharePoint Online l'aggiunta di utenti toohello directory dopo che gli utenti hanno riscattati gli inviti. Prima di rimborso, pertanto, non viene visualizzato utente hello nel portale di Azure AD. Se un utente in hello frattempo invita a un altro sito, viene generato un nuovo invito. Quando invece si usa Collaborazione B2B di Azure AD, gli utenti vengono aggiunti immediatamente all'invito e sono quindi visibili ovunque.

- esperienza di riscatto Hello in OneDrive o SharePoint Online è diverso dall'esperienza hello in collaborazione B2B di Azure Active Directory. Dopo che un utente Riscatta un invito, hello esperienze simili.

- Gli utenti invitati di Collaborazione B2B di Azure AD possono essere selezionati nelle finestre di dialogo di condivisione di OneDrive/SharePoint Online. Dopo avere riscattato gli inviti, gli utenti invitati di OneDrive/SharePoint Online vengono visualizzati anche in Azure AD.

- toomanage esterno condivisione in OneDrive o SharePoint Online con la collaborazione B2B di Azure Active Directory, imposta hello OneDrive/SharePoint Online esterne condivisione impostazione troppo**solo consentire la condivisione con utenti esterni già nella directory hello**. Gli utenti possono accedere a siti tooexternally condivisi e prelievo da collaboratori esterni che hello amministratore è stato aggiunto. salve aggiungere collaboratori esterni di hello tramite hello invito di collaborazione B2B API.

![Hello OneDrive/SharePoint Online esterni di impostazione di condivisione](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a>Passaggi successivi

Vedere gli altri articoli su Azure AD B2B Collaboration.

* [Che cos'è Azure AD B2B Collaboration?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Proprietà dell'utente di Collaborazione B2B](active-directory-b2b-user-properties.md)
* [Aggiunta di un ruolo di tooa utente collaborazione B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegare gli inviti a Collaborazione B2B](active-directory-b2b-delegate-invitations.md)
* [Gruppi dinamici e Collaborazione B2B](active-directory-b2b-dynamic-groups.md)
* [Codici ed esempi di PowerShell per Collaborazione B2B](active-directory-b2b-code-samples.md)
* [Configurare app SaaS per Collaborazione B2B](active-directory-b2b-configure-saas-apps.md)
* [Token utente in Collaborazione B2B](active-directory-b2b-user-token.md)
* [Mapping delle attestazioni utente per Collaborazione B2B](active-directory-b2b-claims-mapping.md)
* [Limitazioni correnti di Collaborazione B2B](active-directory-b2b-current-limitations.md)
