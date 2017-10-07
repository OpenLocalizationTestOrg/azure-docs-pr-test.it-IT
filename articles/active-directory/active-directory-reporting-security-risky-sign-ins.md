---
title: report accessi aaaRisky nel portale di Azure Active Directory hello | Documenti Microsoft
description: Informazioni su report accessi rischiosa hello nel portale di Azure Active Directory hello
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a>Report accessi rischiosa nel portale di Azure Active Directory hello

I report di sicurezza hello in Azure Active Directory (Azure AD) è possibile ottenere informazioni approfondite probabilità hello di account utente compromessi nell'ambiente in uso. 

Azure Active Directory rileva sospette azioni che sono account utente tooyour correlati. Per ogni azione rilevati viene creato un record denominato *evento di rischio*. Per altre informazioni, vedere [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md) (Eventi di rischio di Azure Active Directory). 

Hello rilevato gli eventi di rischio sono utilizzati toocalculate:

- **Accessi rischiosi** -un rischiosa l'accesso è un indicatore per un tentativo di accesso che siano stato eseguito da un utente che non è proprietario di legittimo hello di un account utente. Per informazioni dettagliate, vedere [Accessi a rischio](active-directory-identityprotection.md#risky-sign-ins). 

- **Utenti contrassegnati per il rischio**. Un utente rischioso è indicativo di un account utente che potrebbe essere stato compromesso. Per informazioni dettagliate, vedere [Utenti contrassegnati per il rischio](active-directory-identityprotection.md#users-flagged-for-risk).  

In [hello Azure portal](https://portal.azure.com), è possibile trovare sicurezza hello segnala hello **Azure Active Directory** pannello in hello **sicurezza** sezione. 

![Accessi a rischio](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>Licenza Azure AD è necessario tooaccess un report di sicurezza?  

Tutte le edizioni di Azure Active Directory offrono report relativi agli accessi a rischio.  
Tuttavia, il livello di hello di granularità dei report varia tra le edizioni di hello: 

- In hello **le edizioni di Azure Active Directory Free e Basic**, già un elenco degli accessi rischiosi. 

- Hello **Azure Active Directory Premium 1** edition estende questo modello, consentendo anche tooexamine alcune hello sottostante gli eventi di rischio che sono stati rilevati per ogni report. 

- Hello **Azure Active Directory Premium 2** edition fornisce all'hello più informazioni dettagliate su tutti gli eventi di rischio sottostante e consente inoltre di criteri di sicurezza tooconfigure rispondono automaticamente tooconfigured livelli di rischio.



## <a name="azure-active-directory-free-and-basic-edition"></a>Versione gratuita e di base di Azure Active Directory

Hello Azure Active Directory gratuita e base edizioni offrono un elenco di rischiosi accessi che sono state rilevate per gli utenti. Questo report elenca quanto riportato di seguito.

- **Utente** : hello nome dell'utente hello utilizzato durante l'operazione di accesso hello
- **IP** -hello indirizzo IP del dispositivo hello che tooAzure tooconnect utilizzato Active Directory
- **Percorso** -percorso hello utilizzato tooconnect tooAzure Active Directory
- **Ora di accesso** -hello ora quando accedi hello è stata eseguita
- **Stato** -hello stato Accedi hello


![Accessi a rischio](./media/active-directory-reporting-security-risky-sign-ins/01.png)

In base l'analisi dell'hello rischiosa sign-in, è possibile fornire commenti e suggerimenti tooAzure Active Directory sotto forma di hello seguenti azioni:

- Risolvi
- Contrassegna come falso positivo
- Ignora
- Riattiva

![Accessi a rischio](./media/active-directory-reporting-security-risky-sign-ins/21.png)

Per informazioni dettagliate, vedere [Chiusura manuale degli eventi di rischio](active-directory-identityprotection.md#closing-risk-events-manually).

Questo report offre la possibilità di:

- Eseguire ricerche sulle risorse
- Scaricare i dati del report hello


![Accessi a rischio](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a>Versione Premium di Azure Active Directory

report accessi rischiosa Hello nelle edizioni premium di Azure Active Directory hello offre:

- Aggregare informazioni hello [tipi di eventi di rischio](active-directory-identity-protection-risk-events.md) che sono stati rilevati

- Un report di hello toodownload opzione


![Accessi a rischio](./media/active-directory-reporting-security-risky-sign-ins/456.png)


Quando si seleziona un evento di rischio, si ottiene la visualizzazione di un report dettagliato per questo evento di rischio che consente di:

- Un'opzione tooconfigure un [criteri di monitoraggio e aggiornamento utente dei rischi](active-directory-identityprotection.md#user-risk-security-policy)  

- Sequenza temporale di rilevamento hello di revisione per l'evento di rischio hello  

- esaminare l'elenco di utenti per cui è stato rilevato l'evento di rischio

- [chiudere manualmente gli eventi di rischio](active-directory-identityprotection.md#closing-risk-events-manually) o riattivare un evento di rischio chiuso manualmente. 


![Accessi a rischio](./media/active-directory-reporting-security-risky-sign-ins/457.png)

Quando si seleziona un utente, si ottiene la visualizzazione di un report dettagliato per questo utente che consente di:

- Aprire hello che visualizzare tutti gli accessi

- Reimpostare la password dell'utente hello

- eliminare tutti gli eventi

- Ricercare gli eventi di rischio segnalati per utente hello. 


![Accessi a rischio](./media/active-directory-reporting-security-risky-sign-ins/324.png)


tooinvestigate un evento di rischio, selezionarne uno dall'elenco di hello.  
Verrà visualizzata hello **dettagli** pannello per questo evento di rischio. In hello **dettagli** pannello è hello opzione tooeither [chiudere manualmente un evento di rischio](active-directory-identityprotection.md#closing-risk-events-manually) o riattivare un evento di rischio chiuso manualmente. 


![Accessi a rischio](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a>Passaggi successivi

- Per altre informazioni in merito, vedere [Azure Active Directory Identity Protection](active-directory-identityprotection.md).

