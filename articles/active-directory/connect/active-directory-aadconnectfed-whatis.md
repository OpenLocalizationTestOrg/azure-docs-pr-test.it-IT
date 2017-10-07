---
title: aaaAzure AD Connect e la federazione | Documenti Microsoft
description: "Questa pagina è una posizione centrale di hello per tutta la documentazione riguarda le operazioni di ADFS che usano Azure AD Connect."
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: f9107cf5-0131-499a-9edf-616bf3afef4d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: anandy
ms.openlocfilehash: dc70206eee2296c2320712ef2ade48ccebcc912d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-and-federation"></a>Azure AD Connect e federazione
Azure Active Directory (Azure AD) consente di configurare la federazione con Active Directory Federation Services (ADFS) locale e Azure AD. Con federazione accesso, è possibile abilitare toosign utenti nei servizi tooAzure basato su Active Directory e le relative password locale e, mentre nella rete aziendale hello, senza dovere tooenter nuovamente le proprie password. Utilizzando l'opzione di federazione hello con AD FS, è possibile distribuire una nuova installazione di ADFS oppure è possibile specificare un'installazione esistente in una farm di Windows Server 2012 R2.

In questo argomento è hello home per informazioni sulle funzionalità correlate alla federazione per Azure AD Connect. Un elenco di collegamenti tooall argomenti correlati. Per collegamenti tooAzure AD Connect, vedere [integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).

## <a name="azure-ad-connect-federation-topics"></a>Azure AD Connect - Argomenti sulla federazione
| Argomento | Vengono illustrate e quando tooread è |
|:--- |:--- |
| **Opzioni di accesso utente di Azure AD Connect** | |
| [Informazioni sulle opzioni di accesso utente](active-directory-aadconnect-user-signin.md) |Informazioni sulle varie opzioni di utente e gli effetti di esperienza utente hello sign in Azure. |
| **Installare ADFS con Azure AD Connect** | |
| [Prerequisiti](active-directory-aadconnect-get-started-custom.md#ad-fs-configuration-pre-requisites) |Vedere la sezione Prerequisiti di hello per una corretta installazione di ADFS tramite Azure AD Connect. |
| [Configurare una farm ADFS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs) |Installare una nuova farm ADFS tramite Azure AD Connect. |
| [Eseguire la federazione con Azure AD usando un ID di accesso alternativo](active-directory-aadconnect-federation-management.md#alternateid) | Configurazione della federazione usando l'ID di accesso alternativo  |
| **Modificare la configurazione di ADFS hello Active Directory** | |
| [Ripristino hello trust](active-directory-aadconnect-federation-management.md#repairthetrust) |Ripristino hello corrente trust tra locale ADFS e Office 365 o Azure. |
| [Aggiungere un nuovo server ADFS](active-directory-aadconnect-federation-management.md#addadfsserver) |Espandere la farm ADFS con un server ADFS aggiuntivo dopo l'installazione iniziale. |
| [Aggiungere un nuovo server WAP ADFS](active-directory-aadconnect-federation-management.md#addwapserver) |Espandere la farm ADFS con un server Web Application Proxy (WAP) aggiuntivo dopo l'installazione iniziale. |
| [Aggiungere un nuovo dominio federato](active-directory-aadconnect-federation-management.md#addfeddomain) |Aggiungere un altro toobe dominio federato con Azure AD. |
| [Aggiorna il certificato SSL hello](active-directory-aadconnectfed-ssl-update.md)| Aggiorna il certificato SSL di hello per una farm ADFS. |
| **Configurazione aggiuntiva della federazione** | |
| [Eseguire la federazione di più istanze di Azure AD con una singola istanza di AD FS](active-directory-aadconnectfed-single-adfs-multitenant-federation.md) | Eseguire la federazione di più istanze di Azure AD con una singola farm AD FS.| 
| [Aggiungere l'illustrazione o il logo personalizzato della società](active-directory-aadconnect-federation-management.md#customlogo) |Modificare l'esperienza di accesso hello specificando logo personalizzato hello che viene visualizzato nella pagina di accesso ADFS hello AD. |
| [Aggiungere una descrizione di accesso](active-directory-aadconnect-federation-management.md#addsignindescription) |Modificare hello Accedi descrizione nella pagina di accesso hello AD FS. |
| [Modificare le regole attestazioni per AD FS](active-directory-aadconnect-federation-management.md#modclaims) |Modificare o aggiungere regole attestazioni in ADFS corrispondenti alla configurazione della sincronizzazione tooAzure AD Connect. |


## <a name="additional-resources"></a>Risorse aggiuntive
* [Eseguire la federazione di due istanze di Azure AD con una singola istanza di AD FS](active-directory-aadconnectfed-single-adfs-multitenant-federation.md)
* [Distribuzione di AD FS in Azure](active-directory-aadconnect-azure-adfs.md)
* [Distribuzione di ADFS a disponibilità elevata tra aree geografiche in Azure con Gestione traffico di Azure](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)
