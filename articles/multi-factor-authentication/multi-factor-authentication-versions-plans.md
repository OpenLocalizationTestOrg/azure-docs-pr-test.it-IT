---
title: versioni di MFA aaaAzure e utilizzo dei piani | Documenti Microsoft
description: Informazioni sui client di multi-factor Authentication hello e diversi metodi di hello e le versioni disponibili. Informazioni dettagliate su ogni piano a consumo
keywords: 
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: kgremban
ms.openlocfilehash: 4914747e435531b9f950356d23aa386f3d9585d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-azure-multi-factor-authentication"></a>Come tooget Azure multi-Factor Authentication

Per quanto riguarda tooprotecting gli account, la verifica deve essere standard all'interno dell'organizzazione. Questa funzionalità è particolarmente importante per gli account amministrativi che dispone di accesso tooresources con privilegi. Per questo motivo, Microsoft offre due passaggi di base verifica funzionalità tooOffice 365 e gli amministratori di Azure. Se si desidera utilizzare funzionalità hello tooupgrade per gli amministratori o estendere rest toohello di verifica in due passaggi degli utenti, è possibile acquistare Azure multi-Factor Authentication. 

Vengono illustrate in questo articolo viene illustrata la differenza hello tra le versioni di hello offerti tooadministrators e hello versione completa di Azure MFA e specifica quali funzionalità sono disponibili in ciascuno. Se si è pronti hello toodeploy completa offerta di Azure MFA, hello opzioni di implementazione vengono illustrate nelle sezioni successive e la modalità di calcolo di utilizzo di Microsoft.

>[!IMPORTANT]
>Questo articolo mira toobe toohelp una Guida per comprendere hello modi toobuy Azure multi-Factor Authentication. Per informazioni specifiche sui prezzi e fatturazione, è sempre necessario fare riferimento toohello [multi-Factor Authentication pagina dei prezzi](https://azure.microsoft.com/pricing/details/multi-factor-authentication/).

## <a name="available-versions-of-azure-multi-factor-authentication"></a>Versioni disponibili di Azure Multi-Factor Authentication

Hello nella tabella seguente vengono descritte hello le differenze tra le tre versioni di multi-factor authentication:

| Versione | Descrizione |
| --- | --- |
| Multi-Factor Authentication per Office 365 |Questa versione funziona solo con applicazioni di Office 365 e viene gestita dal portale di Office 365 hello. Gli amministratori possono [proteggere le risorse di Office 365 con la verifica in due passaggi](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6). Questa versione è inclusa in una sottoscrizione di Office 365. |
| Multi-Factor Authentication per amministratori di Azure | Gli amministratori globali di tenant di Azure possono abilitare la verifica in due passaggi per gli account di amministratore senza costi aggiuntivi.|
| Azure Multi-Factor Authentication | "Completa" versione hello tooas spesso con cui viene fatto riferimento, Azure multi-Factor Authentication offre il set più completo di hello delle funzionalità. Fornisce opzioni di configurazione aggiuntive tramite hello [portale di Azure classico](https://manage.windowsazure.com)segnalazione avanzate e supporto per un intervallo di on-premise e applicazioni cloud. Azure multi-Factor Authentication è incluso in Azure Active Directory Premium (piani P1 e P2) ed Enterprise Mobility + Security (piani E3 ed E5) e può essere distribuito uno [nel cloud hello o in locale](multi-factor-authentication-get-started.md). |

## <a name="feature-comparison-of-versions"></a>Confronto tra le funzionalità delle versioni
Hello nella tabella seguente fornisce un elenco delle funzionalità di hello disponibili in hello varie versioni di Azure multi-Factor Authentication.

> [!NOTE]
> Questa tabella di confronto vengono descritte le funzionalità di hello che fanno parte di ogni versione di multi-Factor Authentication. Se si dispone di servizi di Azure multi-Factor Authentication completi hello, alcune funzionalità potrebbero non essere disponibili a seconda se si utilizza [MFA nel cloud hello autenticazione a più fattori in locale o](multi-factor-authentication-get-started.md).


| Funzionalità | Multi-Factor Authentication per Office 365 | Multi-Factor Authentication per amministratori di Azure | Azure Multi-Factor Authentication |
| --- |:---:|:---:|:---:|
| Protezione degli account amministratore con MFA |● |● (solo per l'account amministratore globale) |● |
| App per dispositivi mobili come secondo fattore |● |● |● |
| Chiamata telefonica come secondo fattore |● |● |● |
| SMS come secondo fattore |● |● |● |
| Password di app per i client che non supportano MFA |● |● |● |
| Controllo amministrativo sui metodi di verifica |● |● |● |
| Modalità PIN | | |● |
| Avviso di illecito | | |● |
| Report MFA | | |● |
| Bypass monouso | | |● |
| Messaggi di saluto personalizzati per le telefonate | | |● |
| ID chiamante personalizzato per le telefonate | | |● |
| IP attendibili | | |● |
| Memorizzazione di MFA per dispositivi attendibili |● |● |● |
| SDK MFA | | |● (richiede un provider Multi-Factor Authentication e una sottoscrizione completa di Azure) |
| MFA per applicazioni locali | | |● |

## <a name="how-tooget-azure-multi-factor-authentication"></a>Come tooget Azure multi-Factor Authentication
Se si desidera che la funzionalità completa hello offerta da Azure multi-Factor Authentication, sono disponibili diverse opzioni:

### <a name="option-1---mfa-licenses"></a>Opzione 1: licenze MFA

Acquistare licenze di Azure multi-Factor Authentication e assegnarli agli utenti di tooyour in Azure Active Directory. 

Se si utilizza questa opzione, è necessario creare un Provider di Azure multi-Factor Authentication solo se è necessario inoltre verifica in due passaggi tooprovide per alcuni utenti che non dispone di licenze. In caso contrario, il servizio potrebbe essere fatturato due volte.

### <a name="option-2---bundled-licenses-that-include-mfa"></a>Opzione 2: licenze in bundle che includono MFA

Acquistare licenze che includono Azure multi-Factor Authentication, ad esempio Azure Active Directory Premium (P1 or P2) o Enterprise Mobility + Security (E3 o E5) e assegnare loro tooyour utenti in Azure Active Directory. 

Se si utilizza questa opzione, è necessario creare un Provider di Azure multi-Factor Authentication solo se è necessario inoltre verifica in due passaggi tooprovide per alcuni utenti che non dispone di licenze. In caso contrario, il servizio potrebbe essere fatturato due volte. 

### <a name="option-3---mfa-consumption-based-model"></a>Opzione 3: modello in base al consumo di MFA

Creare un provider Azure Multi-Factor Authentication all'interno di una sottoscrizione di Azure. I provider Azure MFA sono risorse di Azure fatturate sulla base del contratto Enterprise, usando i fondi degli impegni monetari di Azure o sulla carta di credito come tutte le altre risorse di Azure. Questi provider possono essere creati solo nelle sottoscrizioni complete di Azure, non nelle sottoscrizione limitate di Azure con un limite di spesa di $ 0. Le sottoscrizioni limitate vengono create quando si attivano le licenze, come nelle opzioni 1 e 2. 

Quando si usa un provider di Azure Multi-Factor Authentication, sono disponibili due modelli di uso fatturati tramite la sottoscrizione di Azure:  

1. **Per ogni utente** - alle aziende che desiderano tooenable di verifica in due passaggi per un numero fisso di dipendenti che richiedono regolarmente l'autenticazione. Per ogni utente fatturazione si basa sul numero di hello di utenti abilitati per l'autenticazione a più fattori nel tenant di Azure AD e/o il Server di autenticazione a più fattori di Azure. Se gli utenti vengono abilitati per l'autenticazione a più fattori in entrambi AD Azure e Azure MFA Server, la sincronizzazione di dominio (Azure AD Connect) è abilitata, quindi è più ampio di utenti hello di conteggio. Se non è abilitata la sincronizzazione di dominio, quindi si conteggio somma hello di tutti gli utenti abilitati per l'autenticazione a più fattori in Azure AD e Azure MFA Server. Fatturazione è giornaliera sistema Commerce toohello ripartito e verrà segnalata. 

  > [!NOTE]
  > Esempio di fatturazione 1: oggi si hanno 5.000 utenti abilitati per l'autenticazione a più fattori. sistema di autenticazione a più fattori Hello divide tale numero per 31 e gli 161.29 utenti report per tale giorno. Domani abiliti 15 più utenti, in modo hello sistema di autenticazione a più fattori i report 161.77 utenti per tale giorno. Fine hello del ciclo di fatturazione hello, hello totale degli utenti calcolate rispetto alla sottoscrizione Azure aggiunge tooaround 5.000. 
  >
  > Fatturazione esempio 2: è una combinazione di utenti con licenza e gli utenti senza, in modo che sia un toomake di Provider di autenticazione a più fattori di Azure per utente di differenza hello. Nel tenant esistono 4.500 licenze Enterprise Mobility + Security, ma 5.000 utenti abilitati per MFA. Alla sottoscrizione di Azure vengono fatturati 500 utenti, ripartiti e segnalati ogni giorno come 16,13 utenti. 

2. **Per autenticazione** - alle aziende che desiderano tooenable la verifica per un ampio gruppo di utenti che richiedono raramente l'autenticazione. Fatturazione si basa sul numero di hello di richieste di verifica in due passaggi ricevute dal servizio cloud Azure MFA, indipendentemente dall'esito positivo o vengono negate le verifiche di hello. La fatturazione viene visualizzato nella dichiarazione di Azure-utilizzo in pacchetti da 10 autenticazioni e segnalati toohello Commerce sistema ogni giorno. 

  > [!NOTE]
  > Fatturazione esempio 3: oggi, hello servizio Azure MFA ricevuto 3,105 le richieste di verifica in due passaggi. Alla sottoscrizione di Azure vengono fatturati 310,5 pacchetti di autenticazione. 

È importante toonote può avere le licenze di Azure MFA, ma comunque ottenere fatturato per la configurazione in base al consumo. Se si configura un provider Azure MFA per autenticazione, viene fatturata ogni richiesta di verifica in due passaggi, anche quelle eseguite dagli utenti con licenza. Se si configura un Provider di autenticazione a più fattori di Azure per utente in un dominio che non è collegato tooyour tenant di Azure AD, verrà addebitato ogni utente abilitato anche se gli utenti dispongono di licenze in Azure AD. 

## <a name="next-steps"></a>Passaggi successivi

- Per altre informazioni sui prezzi, vedere [Multi-Factor Authentication Prezzi](https://azure.microsoft.com/pricing/details/multi-factor-authentication/).

- Scegliere se toodeploy Azure MFA [in locale o cloud hello](multi-factor-authentication-get-started.md)
