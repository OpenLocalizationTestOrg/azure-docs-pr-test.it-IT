---
title: rilevato da Azure Active Directory Identity Protection aaaVulnerabilities | Documenti Microsoft
description: "Panoramica di vulnerabilità hello rilevate da Azure Active Directory Identity Protection."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestione applicazioni, sicurezza, rischio, livello di rischio, vulnerabilità, criteri di sicurezza"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 5e1cb401f8b566a180eb46e3420a090bcfc66767
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a>Vulnerabilità rilevate da Azure Active Directory Identity Protection
Le vulnerabilità sono punti deboli in un ambiente che possono essere sfruttati da un utente malintenzionato. È consigliabile risolvere tali condizioni di sicurezza hello tooimprove vulnerabilità dell'organizzazione e di impedire ai pirati informatici sfrutti li.


![vulnerabilità](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilità")



Hello nelle sezioni seguenti forniscono una panoramica delle vulnerabilità hello segnalati da Identity Protection.

## <a name="multi-factor-authentication-registration-not-configured"></a>Registrazione per l'autenticazione a più fattori non configurata
Questa vulnerabilità contribuisce di controllare la distribuzione di hello Azure multi-Factor Authentication all'interno dell'organizzazione. 

Azure multi-factor authentication fornisce un secondo livello toouser di autenticazione di sicurezza. Consente di salvaguardare accesso toodata e applicazioni rispettando richiesta dell'utente per un semplice processo. Offre autenticazione avanzata tramite una gamma di semplici opzioni di verifica, ad esempio una telefonata, un SMS, una notifica dell'app mobile o un codice di verifica e token OATH di terze parti.

È consigliabile richiedere l'autenticazione a più fattori di Azure per l'accesso degli utenti. L'autenticazione a più fattori svolge un ruolo chiave nei criteri di accesso condizionale basati sul rischio disponibili tramite Identity Protection.

Per altre informazioni, vedere [Informazioni su Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)

## <a name="unmanaged-cloud-apps"></a>App per cloud non gestite
Questa vulnerabilità consente di identificare le app per cloud non gestite all'interno dell'organizzazione.

Nelle aziende moderne i reparti IT spesso sono consapevoli tutte le applicazioni cloud hello che gli utenti dell'organizzazione utilizzando toodo il proprio lavoro. È facile toosee perché gli amministratori avranno preoccupazioni dati toocorporate di accesso non autorizzato, perdita di dati e altri rischi di protezione. 

È consigliabile l'organizzazione di distribuire le applicazioni cloud di Cloud App Discovery toodiscover non gestita e toomanage queste applicazioni con Azure Active Directory.

Per altre informazioni, vedere [Ricerca di applicazioni cloud non gestite con Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).

## <a name="security-alerts-from-privileged-identity-management"></a>Avvisi di sicurezza di Privileged Identity Management
Questa vulnerabilità permette di identificare e risolvere gli avvisi sulle identità con privilegi all'interno dell'organizzazione.  

tooenable utenti toocarry operazioni privilegiate, le organizzazioni devono toogrant utenti di accesso con privilegi temporanei o permanente in Azure AD, le risorse di Azure o Office 365 o altre applicazioni SaaS. Ognuno di questi privilegi superficie di attacco hello aumenta gli utenti dell'organizzazione. Questa vulnerabilità consente di identificare gli utenti con accesso con privilegi non necessario e richiedere l'azione appropriata tooreduce o eliminare il rischio di hello che comportano. 

È consigliabile che l'organizzazione utilizza Azure AD Privileged Identity Management toomanage, controllo e le identità di monitoraggio privilegiato e tooresources loro accesso in Azure AD, nonché altri Microsoft online services quali Office 365 o Microsoft Intune.

Per altre informazioni, vedere [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md). 

## <a name="see-also"></a>Vedere anche
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

