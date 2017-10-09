---
title: 'Servizio di sincronizzazione Azure AD Connect: comprendere e personalizzare la sincronizzazione | Documentazione Microsoft'
description: Viene illustrato come funziona la sincronizzazione di Azure AD Connect e come toocustomize.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ee4bf802-045b-4da0-986e-90aba2de58d6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2016
ms.author: markvi
ms.openlocfilehash: 97e4bd9904b077f2628e5f8dcbaa6f1a76168a12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understand-and-customize-synchronization"></a>Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione
servizi di sincronizzazione di Azure Active Directory Connect Hello (sincronizzazione di Azure AD Connect) è un componente principale di Azure AD Connect. Si occupa di tutte le operazioni di hello che sono dati di identità toosynchronize correlati tra l'ambiente locale e Azure AD. Sincronizzazione di Azure AD Connect è successore hello di Forefront Identity Manager DirSync e Azure AD Sync con hello che Azure Active Directory Connector configurato.

In questo argomento è hello home per **sincronizzazione di Azure AD Connect** (chiamato anche **motore di sincronizzazione**) e gli elenchi di collegamenti tooall altri tooit di argomenti correlati. Per collegamenti tooAzure AD Connect, vedere [integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).

il servizio di sincronizzazione Hello è costituito da due componenti, hello locale **sincronizzazione di Azure AD Connect** componente e hello lato servizio in Azure AD chiamato **servizio di sincronizzazione di Azure AD Connect**. servizio Hello è comune per DirSync, Azure AD Sync e Azure AD Connect.

## <a name="azure-ad-connect-sync-topics"></a>Argomenti relativi al servizio di sincronizzazione Azure AD Connect
| Argomento | Vengono illustrate e quando tooread |
| --- | --- |
| **Concetti fondamentali sul servizio di sincronizzazione Azure AD Connect** | |
| [Informazioni sull'architettura di hello](active-directory-aadconnectsync-understanding-architecture.md) |Per coloro che sono nuovo motore di sincronizzazione toohello e desidera toolearn sull'architettura di hello e termini hello utilizzati. |
| [Concetti tecnici](active-directory-aadconnectsync-technical-concepts.md) |Una versione abbreviata di argomento architettura hello e brevemente illustra hello termini utilizzati. |
| [Topologie per Azure AD Connect](active-directory-aadconnect-topologies.md) |Viene descritto hello diversi scenari e le topologie hello sincronizzazione motore supporta. |
| **Configurazione personalizzata** | |
| [In esecuzione hello installazione guidata](active-directory-aadconnectsync-installation-wizard.md) |Illustra le opzioni sono disponibili quando si esegue nuovamente Installazione guidata di hello Azure AD Connect. |
| [Informazioni sul provisioning dichiarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md) |Viene descritto il modello di configurazione hello denominato provisioning dichiarativo. |
| [Informazioni sulle espressioni di provisioning dichiarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |Descrive la sintassi di hello per il linguaggio di espressioni hello utilizzato nel provisioning dichiarativo. |
| [Informazioni su configurazione predefinita di hello](active-directory-aadconnectsync-understanding-default-configuration.md) |Descrive le regole di out-of-box hello e la configurazione predefinita di hello. Descrive inoltre come hello regole interagiscono per toowork out-of-box scenari hello. |
| [Informazioni su utenti e contatti](active-directory-aadconnectsync-understanding-users-and-contacts.md) |Continua in argomento precedente hello e viene descritto l'utilizzo configurazione hello per utenti e contatti insieme, in particolare in un ambiente a più foreste. |
| [Come toomake toohello una modifica di configurazione predefinite](active-directory-aadconnectsync-change-the-configuration.md) |Viene illustrata la modalità di scorrimento toomake un tooattribute di modifica di configurazione comuni. |
| [Procedure consigliate per la modifica di configurazione predefinita di hello](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) |Limitazioni del supporto e per la configurazione di modifiche toohello out-of-box. |
| [Configurare il filtro](active-directory-aadconnectsync-configure-filtering.md) |Descrive hello diverse opzioni per la modalità di sincronizzazione toolimit che gli oggetti vengono tooAzure Active Directory e come dettagliate tooconfigure queste opzioni. |
| **Funzionalità e scenari** | |
| [Impedire eliminazioni accidentali](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) |Descrive hello *impedire eliminazioni accidentali* funzionalità e la modalità tooconfigure è. |
| [Utilità di pianificazione](active-directory-aadconnectsync-feature-scheduler.md) |Viene descritto hello predefinite dell'utilità di pianificazione, l'importazione, la sincronizzazione e l'esportazione di dati. |
| [Implementare la sincronizzazione password](active-directory-aadconnectsync-implement-password-synchronization.md) |Viene descritto il funzionamento della sincronizzazione delle password, come tooimplement e come toooperate e risoluzione dei problemi. |
| [Writeback dei dispositivi](active-directory-aadconnect-feature-device-writeback.md) |Illustra il funzionamento del writeback dei dispositivi in Azure AD Connect. |
| [Estensioni della directory](active-directory-aadconnectsync-feature-directory-extensions.md) |Viene descritto come tooextend hello dello schema di Azure AD con attributi personalizzati. |
| **Servizio di sincronizzazione** | |
| [Funzionalità del servizio di sincronizzazione di Azure AD Connect](active-directory-aadconnectsyncservice-features.md) |Descrive lato servizio di sincronizzazione hello e come toochange impostazioni di sincronizzazione in Azure AD. |
| [Resilienza degli attributi duplicati](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) |Viene descritto come tooenable e utilizzare **userPrincipalName** e **proxyAddresses** resilienza di valori di attributo duplicato. |
| **Operazioni e interfaccia utente** | |
| [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md) |Viene descritto hello UI Synchronization Service Manager, inclusi [operazioni](active-directory-aadconnectsync-service-manager-ui-operations.md), [connettori](active-directory-aadconnectsync-service-manager-ui-connectors.md), [progettazione di Metaverse](active-directory-aadconnectsync-service-manager-ui-mvdesigner.md), e [ricerca Metaverse](active-directory-aadconnectsync-service-manager-ui-mvsearch.md) schede. |
| [Attività operative e considerazioni](active-directory-aadconnectsync-operations.md) |Illustra aspetti operativi, ad esempio il ripristino di emergenza. |
| **Procedura:** | |
| [Reimposta account hello Azure AD](active-directory-aadconnectsync-howto-azureadaccount.md) |Modalità di utilizzo di tooconnect da Azure AD Connect sincronizzazione tooAzure AD credenziali hello tooreset hello dell'account di servizio. |
| **Altri riferimenti e informazioni** | |
| [Porte](active-directory-aadconnect-ports.md) |Gli elenchi di queste porte è necessario tooopen tra il motore di sincronizzazione hello e le directory locali e Azure AD. |
| [Attributi sincronizzati tooAzure Active Directory](active-directory-aadconnectsync-attributes-synchronized.md) |Elenca tutti gli attributi che vengono sincronizzati tra l'istanza locale di AD e Azure AD. |
| [Riferimento alle funzioni](active-directory-aadconnectsync-functions-reference.md) |Elenca tutte le funzioni disponibili nel provisioning dichiarativo. |

## <a name="additional-resources"></a>Risorse aggiuntive
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)

