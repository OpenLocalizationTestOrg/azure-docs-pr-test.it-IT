---
title: aaaUpgrade tooAzure AD applicazione Proxy | Documenti Microsoft
description: Scegliere la soluzione del proxy migliore se si esegue l'aggiornamento da Microsoft Forefront o Unified Access Gateway.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7dc2633140b384e25792470dadbb7f3fa7992a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="compare-remote-access-solutions"></a>Confrontare le soluzioni di accesso remoto

Il proxy dell'applicazione di Azure Active Directory è una delle due soluzioni di accesso remoto offerte da Microsoft. altri Hello è Proxy applicazione Web, la versione locale di hello. Queste due soluzioni sostituiscono i prodotti precedenti offerti da Microsoft: Microsoft Forefront Threat Management Gateway (TMG) e Unified Access Gateway (UAG). Utilizzare questo toounderstand articolo come vengono confrontate con queste soluzioni con quattro tooeach altri. Se si utilizza ancora hello deprecato soluzioni Forefront Threat Management gateway o UAG, usare questo piano toohelp articolo tooone la migrazione del Proxy dell'applicazione hello. 


## <a name="feature-comparison"></a>Confronto tra le funzionalità

Utilizzare questo toounderstand tabella confrontare tooeach altri Threat Management Gateway (TMG), Unified Access Gateway (UAG), Proxy applicazione Web (WAP) e del Proxy di applicazione AD Azure (AP).

| Funzionalità | TMG | UAG | WAP | AP |
| ------- | --- | --- | --- | --- |
| Autenticazione del certificato | Sì | Sì | - | - |
| Pubblicare in modo selettivo le app del browser | Sì | Sì | Sì | Sì |
| Preautenticazione e Single Sign-On | Sì | Sì | Sì | Sì | 
| Firewall di livello 2/3 | Sì | Sì | - | - |
| Funzionalità proxy di inoltro | Sì | - | - | - |
| Funzionalità VPN | Sì | Sì | - | - |
| Supporto dei protocolli rich | - | Sì | Sì, se in esecuzione su HTTP | Sì, se in esecuzione su HTTP o tramite Gateway Desktop remoto |
| Funge da server proxy ADFS | - | Sì | Sì | - |
| Un portale per l'accesso all'applicazione | - | Sì | - | Sì |
| Conversione dei collegamenti al corpo della risposta | Sì | Sì | - | Sì | 
| Autenticazione con intestazioni | - | Sì | - | Sì, con PingAccess | 
| Sicurezza a livello di cloud | - | - | - | Sì | 
| Accesso condizionale | - | Sì | - | Sì |
| Nessun componente in hello rete perimetrale (DMZ) | - | - | - | Sì |
| Nessuna connessione in ingresso | - | - | - | Sì |

Per la maggior parte degli scenari, è consigliabile applicazione AD Azure come soluzione moderna hello. Il Proxy applicazione Web è preferito esclusivamente in scenari che richiedono un server proxy per il servizio federativo AD e non è possibile usare domini personalizzati in Azure Active Directory. 

Proxy dell'applicazione Azure Active Directory offre i vantaggi univoco quando confrontati toosimilar prodotti, tra cui:

- Estensione delle risorse di Azure AD tooon locale
   - Sicurezza e protezione a livello di scalabilità
   - Funzionalità quali l'accesso condizionale e multi-Factor Authentication sono tooenable semplice
- Nessun componente nella rete perimetrale hello
- Nessuna connessione in ingresso necessaria
- Un pannello che gli utenti possono passare toofor tutte le applicazioni, incluso Office 365, Azure AD integrato App SaaS e App web locale. 


## <a name="next-steps"></a>Passaggi successivi

- [Utilizzare applicazioni di Azure AD tooprovide applicazioni locali tooon di accesso remoto sicuro](active-directory-application-proxy-get-started.md)
- [Eseguire la transizione da Forefront TMG e UAG tooApplication Proxy](https://blogs.technet.microsoft.com/isablog/2015/06/30/modernizing-microsoft-application-access-with-web-application-proxy-and-azure-active-directory-application-proxy/).
