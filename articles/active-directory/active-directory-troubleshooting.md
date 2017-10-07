---
title: "Risoluzione dei problemi: Elemento \"Active Directory\" è mancante o non disponibile | Documenti Microsoft"
description: Quali toodo quando la voce di menu Active Directory non viene visualizzato nel portale di gestione Azure hello.
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a>Risoluzione dei problemi: Voce "Active Directory" mancante o non disponibile
Molte delle istruzioni di hello per l'utilizzo di servizi e funzionalità di Azure Active Directory iniziano con "toohello portale di gestione di Azure, fare clic su **Active Directory**." Ma cosa fare se non viene visualizzata la voce di menu o estensione di Active Directory hello o se è contrassegnato come **non disponibile**? In questo argomento è progettato toohelp. Viene descritto hello condizioni **Active Directory** non viene visualizzata o non è disponibile e viene spiegato come tooproceed.

## <a name="active-directory-is-missing"></a>Active Directory non disponibile
In genere, un **Active Directory** elemento viene visualizzato nel menu di navigazione sinistro hello. istruzioni di Hello nelle procedure di Azure Active Directory si supponga che nella visualizzazione di questo elemento.

![Schermata: Active Directory in Azure](./media/active-directory-troubleshooting/typical-view.png)

voce di Active Directory Hello viene visualizzata nel menu di navigazione sinistro hello quando una delle seguenti condizioni hello è true. In caso contrario, non viene visualizzato elemento hello.

* utente corrente Hello l'accesso con un account Microsoft (precedentemente noto come Windows Live ID).
  
    OPPURE
* Hello tenant di Azure dispone di una directory e account di hello corrente sia un amministratore di directory.
  
    OPPURE
* Hello tenant di Azure ha almeno uno spazio dei nomi di Azure AD Access Control (ACS). Per altre informazioni, vedere [Spazio dei nomi di Access Control](https://msdn.microsoft.com/library/azure/gg185908.aspx)
  
    OPPURE
* Hello tenant di Azure ha almeno un provider di Azure multi-Factor Authentication. Per altre informazioni, vedere [Amministrazione dei provider di Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

toocreate uno spazio dei nomi di controllo di accesso o un provider di multi-Factor Authentication, fare clic su **+ nuovo** > **servizi App** > **Active Directory**.

directory di tooa tooget diritti amministrativi, hanno un amministratore di assegnare a un amministratore tooyour account membro del ruolo. Per informazioni dettagliate, vedere [Assegnazione dei ruoli di amministratore in Azure AD](active-directory-assign-admin-roles.md).

## <a name="active-directory-is-not-available"></a>Active Directory non è disponibile
Quando si fa clic su **+Nuovo** > **Servizi app**, viene visualizzata la voce **Active Directory**. In particolare, voce di Active Directory hello viene visualizzata quando si verifica una delle funzionalità di Active Directory hello, ad esempio Directory, il controllo di accesso o Provider di multi-Factor Authentication, utente corrente toohello disponibili.

Tuttavia, durante il caricamento pagina hello, elemento hello è visualizzata in grigio e viene contrassegnato **non disponibile**. Questo stato è temporaneo. Attendere alcuni secondi, l'elemento hello diventa disponibile. Se hello ritardo è prolungato, l'aggiornamento della pagina web di hello consente spesso di risolvere il problema di hello.

![Schermata: Active Directory non disponibile](./media/active-directory-troubleshooting/not-available.png)

