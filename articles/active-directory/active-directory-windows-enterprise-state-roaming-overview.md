---
title: Panoramica di Roaming stato aaaEnterprise | Documenti Microsoft
description: Fornisce informazioni sulle impostazioni del servizio Enterprise State Roaming nei dispositivi Windows. Enterprise State Roaming offre agli utenti un'esperienza unificata tra i propri dispositivi Windows e riducendo i tempi di hello necessari per la configurazione di un nuovo dispositivo.
services: active-directory
keywords: informazioni su Enterprise State Roaming, sincronizzazione aziendale, cloud windows
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 83b3b58f-94c1-4ab0-be05-20e01f5ae3f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 436076383b70b7cd65a612e3928f62f26ac5fa84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-state-roaming-overview"></a>Panoramica di Enterprise State Roaming
Con Windows 10, [Azure Active Directory (Azure AD)](active-directory-whatis.md) utenti guadagno hello possibilità toosecurely sincronizzare le impostazioni utente e l'applicazione impostazioni dati toohello nel cloud. Enterprise State Roaming offre agli utenti un'esperienza unificata tra i propri dispositivi Windows e riducendo i tempi di hello necessari per la configurazione di un nuovo dispositivo. Enterprise State Roaming opera simile standard toohello [sincronizzazione impostazioni consumer](http://windows.microsoft.com/en-US/windows-8/sync-settings-pcs) che è stata introdotta in Windows 8. Il servizio Enterprise State Roaming offre anche i vantaggi seguenti:

* **Separazione di dati aziendali e dell'utente** : le organizzazioni mantengono i controlli dei propri dati e non esiste alcuna combinazione di dati aziendali in un account cloud di utenti o di dati utente in un account cloud aziendale.
* **La sicurezza avanzata** : dati vengono crittografati automaticamente prima di uscire dal dispositivo Windows 10 hello utente mediante Azure Rights Management (Azure RMS) e dati rimangono crittografati a riposo nel cloud hello. Tutto il contenuto rimane crittografato inattivi nel cloud hello, ad eccezione di hello gli spazi dei nomi, come nomi di impostazioni e i nomi delle app di Windows.  
* **Migliore gestione e monitoraggio** – fornisce visibilità e controllo su chi esegue la sincronizzazione delle impostazioni dell'organizzazione e i relativi dispositivi mediante l'integrazione del portale hello Azure AD. 

Enterprise State Roaming è disponibile in più aree di Azure. È possibile trovare hello aggiornato elenco delle aree disponibili su hello [servizi di Azure dalle aree](https://azure.microsoft.com/regions/#services) pagina in Azure Active Directory.

| Articolo | Descrizione |
| --- | --- |
| [Abilitare Enterprise State Roaming in Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md) |Enterprise State Roaming è organizzazione tooany disponibile con una sottoscrizione di Azure Active Directory (Azure AD) Premium. Per ulteriori informazioni su come tooget una sottoscrizione di Azure AD, vedere hello [prodotto Azure AD](https://azure.microsoft.com/services/active-directory) pagina. |
| [Domande frequenti su impostazioni e dati in roaming](active-directory-windows-enterprise-state-roaming-faqs.md) |Questo argomento fornisce le risposte ad alcune possibili domande degli amministratori IT in merito alle impostazioni e alla sincronizzazione dei dati delle app. |
| [Criteri di gruppo e impostazioni del software MDM per la sincronizzazione delle impostazioni](active-directory-windows-enterprise-state-roaming-group-policy-settings.md) |Windows 10 fornisce criteri di gruppo e sincronizzazione di dispositivi mobili (MDM) di gestione criteri impostazioni toolimit impostazioni. |
| [Riferimento alle impostazioni di roaming di Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md) |di seguito Hello è un elenco completo di tutte le impostazioni di hello che verranno spostate e/o essere sottoposti a backup in Windows 10. |
| [Risoluzione dei problemi](active-directory-windows-enterprise-state-roaming-troubleshooting.md) |Questo argomento illustra alcuni passaggi di base per la risoluzione dei problemi e contiene un elenco di problemi noti. |

