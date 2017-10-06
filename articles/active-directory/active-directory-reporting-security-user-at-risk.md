---
title: aaaUsers contrassegnati per il report protezione rischi nel portale di Azure Active Directory hello | Documenti Microsoft
description: Informazioni sugli utenti hello contrassegnati per il report protezione rischi nel portale di Azure Active Directory hello
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a>Utenti contrassegnati per il report protezione rischi nel portale di Azure Active Directory hello

I report di sicurezza hello in hello Azure Active Directory (Azure AD), è possibile ottenere informazioni approfondite probabilità hello di account utente compromessi nell'ambiente in uso. 

Azure Active Directory rileva sospette azioni che sono account utente tooyour correlati. Per ogni azione rilevati viene creato un record denominato *evento di rischio*. Per altre informazioni, vedere [Eventi di rischio di Azure Active Directory](active-directory-identity-protection-risk-events.md). 

Hello rilevato gli eventi di rischio sono utilizzati toocalculate:

- **Accessi rischiosi** -un rischiosa l'accesso è un indicatore per un tentativo di accesso che siano stato eseguito da un utente che non è proprietario di legittimo hello di un account utente. Per altre informazioni, vedere [Accessi a rischio](active-directory-identityprotection.md#risky-sign-ins). 

- **Utenti contrassegnati per il rischio**. Un utente rischioso è indicativo di un account utente che potrebbe essere stato compromesso. Per altre informazioni, vedere [Utenti contrassegnati per il rischio](active-directory-identityprotection.md#users-flagged-for-risk).  

Nel portale di Azure hello, è possibile trovare sicurezza hello segnala hello **Azure Active Directory** pannello in hello **sicurezza** sezione.  

![Accessi a rischio](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>Licenza Azure AD è necessario tooaccess un report di sicurezza?  

Tutte le edizioni di Azure Active Directory offrono report sugli utenti contrassegnati per il rischio.  
Tuttavia, il livello di hello di granularità dei report varia tra le edizioni di hello: 

- In hello **le edizioni di Azure Active Directory Free e Basic**, già un elenco di utenti contrassegnati i rischi. 

- Hello **Azure Active Directory Premium 1** edition estende questo modello, consentendo anche tooexamine alcune hello sottostante gli eventi di rischio che sono stati rilevati per ogni report. 

- Hello **Azure Active Directory Premium 2** edition offre informazioni più dettagliate su tutti gli eventi di rischio sottostante hello e consente di criteri di sicurezza tooconfigure rispondono automaticamente tooconfigured rischio livelli.



## <a name="azure-active-directory-free-and-basic-edition"></a>Versione gratuita e di base di Azure Active Directory

gli utenti di Hello contrassegnati per il report di rischio nelle edizioni free e base di Azure Active Directory hello fornisce un elenco di account utente che sono stati compromessi. 


![Accessi a rischio](./media/active-directory-reporting-security-user-at-risk/03.png)

Se si seleziona un utente apre il pannello di dati utente correlato hello.
Per gli utenti che sono a rischio, è possibile esaminare una cronologia di accesso dell'utente di hello e reimpostare la password di hello se necessario.

![Accessi a rischio](./media/active-directory-reporting-security-user-at-risk/46.png)


Questa finestra di dialogo offre la possibilità di:

- Scaricare report hello

- Cercare gli utenti

![Accessi a rischio](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a>Versione Premium di Azure Active Directory

gli utenti di Hello contrassegnati per il report di rischio nelle edizioni premium di Azure Active Directory hello offre:

- Un [elenco di account di utenti](active-directory-identityprotection.md#users-flagged-for-risk) che potrebbero essere stati compromessi 

- Aggregare informazioni hello [tipi di eventi di rischio](active-directory-identity-protection-risk-events.md) che sono stati rilevati

- Un report di hello toodownload opzione

- Un'opzione tooconfigure un [criteri di monitoraggio e aggiornamento utente dei rischi](active-directory-identityprotection.md#user-risk-security-policy)  


![Accessi a rischio](./media/active-directory-reporting-security-user-at-risk/71.png)

Quando si seleziona un utente, si ottiene la visualizzazione di un report dettagliato per questo utente che consente di:

- Aprire hello che visualizzare tutti gli accessi

- Reimpostare la password dell'utente hello

- eliminare tutti gli eventi

- Ricercare gli eventi di rischio segnalati per utente hello. 


![Accessi a rischio](./media/active-directory-reporting-security-user-at-risk/324.png)


tooinvestigate un evento di rischio, selezionarne uno dall'hello di hello elenco tooopen **dettagli** pannello per questo evento di rischio. In hello **dettagli** pannello è hello opzione tooeither [chiudere manualmente un evento di rischio](active-directory-identityprotection.md#closing-risk-events-manually) o riattivare un evento di rischio chiuso manualmente. 


![Accessi a rischio](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a>Passaggi successivi

- Per altre informazioni in merito, vedere [Azure Active Directory Identity Protection](active-directory-identityprotection.md).

