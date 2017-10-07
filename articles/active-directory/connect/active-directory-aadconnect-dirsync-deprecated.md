---
title: aaaUpgrade da DirSync e Azure AD Sync | Documenti Microsoft
description: Viene descritto come tooupgrade da tooAzure DirSync e Azure AD Sync AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: bd68fb88-110b-4d76-978a-233e15590803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d465b137fb54f0c6e28ccf73429c4bd3aafd8698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-windows-azure-active-directory-sync-and-azure-active-directory-sync"></a>Aggiornare il servizio di sincronizzazione di Microsoft Azure Active Directory e Azure Active Directory Sync
Azure AD Connect è hello tooconnect modo migliore le directory locali con Azure AD e Office 365. Si tratta di un tooAzure tooupgrade molto tempo AD Connect dalla sincronizzazione Windows Azure Active Directory (DirSync) o Azure AD Sync come questi strumenti sono ora deprecata e verrà raggiunta fine del supporto di 13 aprile 2017.

Hello due identità gli strumenti di sincronizzazione che sono deprecati sono disponibili per i clienti singola foresta (DirSync) e per i clienti avanzati a più foreste e (Azure AD Sync). Gli strumenti obsoleti sono stati sostituiti da un'unica soluzione disponibile per tutti gli scenari: Azure AD Connect. Questa soluzione offre nuove funzionalità, miglioramenti e supporto per nuovi scenari. toobe toocontinue in grado di toosynchronize il tooAzure dati di identità locale AD e Office 365, è consigliabile effettuare l'aggiornamento tooAzure AD Connect.

ultima versione di Hello di DirSync è stato rilasciato nel luglio 2014 e l'ultima versione di hello di Azure AD Sync è stato rilasciato nel maggio 2015.

## <a name="what-is-azure-ad-connect"></a>Cos'è Azure AD Connect
Azure AD Connect è tooDirSync successore hello e Azure AD Sync. La soluzione combina tutti gli scenari dei due strumenti supportati. Per altre informazioni sull'argomento, vedere [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).

## <a name="deprecation-schedule"></a>Pianificazione della deprecazione
| Date | Commento |
| --- | --- |
| 13 aprile 2016 |Annuncio della deprecazione dei servizi di sincronizzazione di Azure Active Directory ("DirSync") e Microsoft Azure Active Directory Sync ("Azure AD Sync"). |
| 13 aprile 2017 |Termine del supporto. I clienti non saranno in grado di tooopen un case di supporto senza effettuare l'aggiornamento tooAzure AD eseguire per primo. |
|31 dicembre 2017|Azure AD non accetterà più comunicazioni provenienti da Azure Active Directory Sync ("DirSync") e Microsoft Azure Active Directory Sync ("Azure AD Sync").

## <a name="how-tootransition-tooazure-ad-connect"></a>Come tootransition tooAzure Active Directory Connect
Se si usa DirSync, è possibile eseguire l'aggiornamento in due modi: aggiornamento sul posto e distribuzione in parallelo. L'aggiornamento sul posto è consigliato per la maggior parte dei clienti e se si dispone di un sistema operativo recente con meno di 50.000 oggetti. In altri casi, è consigliabile toodo una distribuzione in parallelo in cui la configurazione di DirSync è spostato tooa nuovo server che esegue Azure AD Connect.

Se si usa Azure AD Sync, è consigliabile un aggiornamento sul posto. Se si desidera, è possibile tooinstall un nuovo server di Azure AD Connect in parallelo ed eseguire una migrazione di attività dal tooAzure server di sincronizzazione di Active Directory di Azure AD Connect.

| Soluzione | Scenario |
| --- | --- |
| [Aggiornamento da DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>Se è presente un server DirSync esistente già in esecuzione.</li> |
| [Aggiornamento da Azure AD Sync](active-directory-aadconnect-upgrade-previous-version.md) |<li>Se si esegue l'aggiornamento da Azure AD Sync.</li> |

Se si desidera toosee come toodo sul posto l'aggiornamento da DirSync tooAzure AD Connect, quindi vedere il video su Channel 9:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-in-place-upgrade-from-legacy-tools/player]
>
>

## <a name="faq"></a>domande frequenti
**D: ho ricevuto una notifica di posta elettronica dal Team di Azure hello e/o di un messaggio da centro messaggi di Office 365 hello, ma l'utilizzo di Connect.**  
notifica di Hello anche inviata toocustomers con Azure AD Connect con un numero di build 1.0. \*,0 (utilizzando una versione di pre-1.1). Si consiglia ai clienti rilascia toostay corrente con Azure AD Connect. Hello [l'aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md) funzionalità introdotta in 1.1 rende facile tooalways dispone di una versione recente di Azure AD Connect installato.

**D: DirSync/Azure AD Sync smetteranno di funzionare il 13 aprile 2017?**  
DirSync/Azure AD Sync continuerà toowork in aprile 2017 13.  Il 31 dicembre 2017, tuttavia, Azure AD non accetterà più comunicazioni provenienti da DirSync/Azure AD Sync.

**D: Da quali versioni di DirSync è possibile eseguire l'aggiornamento?**  
È supportato tooupgrade da qualsiasi versione di DirSync attualmente in uso.

**Q: cosa succede hello connettore Azure AD per FIM o MIM?**  
il connettore Azure AD per FIM o MIM Hello è **non** stati annunciati come deprecati. Si tratta di un **blocco delle funzionalità**: non vengono aggiunte nuove funzionalità e non si ricevono correzioni dei bug. Si consiglia ai clienti che utilizzano il toomove tooplan da esso tooAzure AD Connect. È fortemente consigliabile toonot inizio eventuali nuove distribuzioni di utilizzarlo. Questo connettore verrà annunciato deprecata in hello future.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
