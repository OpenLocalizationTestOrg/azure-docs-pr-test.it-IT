---
title: "Protezione di identità di Active Directory - aaaAzure come utenti toounblock | Documenti Microsoft"
description: Informazioni su come sbloccare gli utenti bloccati da un criterio di Azure Active Directory Identity Protection.
services: active-directory
keywords: Azure Active Directory Identity Protection, sbloccare gli utenti
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a953d425-a3ef-41f8-a55d-0202c3f250a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: cdda2808822888f76aa75cf46478738c94df51a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection---how-toounblock-users"></a>Azure Active Directory la protezione dell'identità, come gli utenti toounblock
Con protezione dell'identità di Azure Active Directory, è possibile configurare i criteri utenti tooblock se hello configurato condizioni sono soddisfatte. In genere, un utente bloccato contatti help desk toobecome sbloccato. Questo argomento illustra i passaggi di hello è possibile eseguire toounblock un utente bloccato.

## <a name="determine-hello-reason-for-blocking"></a>Determinare il motivo di hello per il blocco
È necessario un toounblock passaggio prima un utente, tipo di hello toodetermine di criteri che ha bloccato l'utente hello poiché i passaggi successivi sono dipendono da essa.
Azure Active Directory Identity Protection consente di bloccare un utente mediante un criterio di rischio di accesso o un criterio di rischio.

È possibile ottenere il tipo di hello di criteri che ha bloccato un utente dall'intestazione hello nella finestra di dialogo hello presentato utente toohello durante un tentativo di accesso:

| Criteri | Finestra di dialogo utente |
| --- | --- |
| Rischio di accesso |![Accesso bloccato](./media/active-directory-identityprotection-unblock-howto/02.png) |
| Rischio utente |![Account bloccato](./media/active-directory-identityprotection-unblock-howto/104.png) |

Un utente bloccato da:

* Un criterio di rischio di accesso è noto anche come accesso sospetto
* Un criterio di rischio utente è noto anche come account a rischio

## <a name="unblocking-suspicious-sign-ins"></a>Sblocco di accessi sospetti
toounblock un accesso aggiuntivo sospetta, è necessario hello le opzioni seguenti:

1. **Accesso da una località o un dispositivo familiare** : un motivo comune per gli accessi sospetti bloccati è costituito da tentativi di accesso da località o dispositivi non familiari. Gli utenti possono determinare rapidamente se si tratta di hello motivo di blocco cercando toosign aggiuntivo da una posizione familiare o dispositivo.
2. **Escludere dai criteri** : se si ritiene che la configurazione corrente di hello dei criteri di accesso causa problemi per utenti specifici, è possibile escludere gli utenti di hello da esso. Per altre informazioni, vedere [Azure Active Directory Identity Protection](active-directory-identityprotection.md).
3. **Disabilita criterio** : se si ritiene che la configurazione dei criteri causa problemi per tutti gli utenti, è possibile disabilitare i criteri di hello. Per altre informazioni, vedere [Azure Active Directory Identity Protection](active-directory-identityprotection.md).

## <a name="unblocking-accounts-at-risk"></a>Sblocco di account a rischio
toounblock un account a rischio, è necessario hello le opzioni seguenti:

1. **Reimpostazione della password** -è possibile reimpostare la password dell'utente hello. Per informazioni dettagliate, vedere [Reimpostazione manuale della password di protezione](active-directory-identityprotection.md#manual-secure-password-reset) .
2. **Chiudere tutti gli eventi di rischio** -criteri di rischio hello utente impedisce a un utente se è stato raggiunto un livello di rischio utente hello configurato per bloccare l'accesso. È possibile ridurre il livello di rischio di un utente chiudendo manualmente gli eventi di rischio segnalati. Per informazioni dettagliate, vedere [Chiusura manuale degli eventi di rischio](active-directory-identityprotection.md#closing-risk-events-manually).
3. **Escludere dai criteri** : se si ritiene che la configurazione corrente di hello dei criteri di accesso causa problemi per utenti specifici, è possibile escludere gli utenti di hello da esso. Per altre informazioni, vedere [Azure Active Directory Identity Protection](active-directory-identityprotection.md).
4. **Disabilita criterio** : se si ritiene che la configurazione dei criteri causa problemi per tutti gli utenti, è possibile disabilitare i criteri di hello. Per altre informazioni, vedere [Azure Active Directory Identity Protection](active-directory-identityprotection.md).

## <a name="next-steps"></a>Passaggi successivi
 Si desidera tooknow informazioni su Azure AD Identity Protection? vedere [Azure Active Directory Identity Protection](active-directory-identityprotection.md).
