---
title: aaaWrong set di utenti stanno applicazione raccolta tooan provisioning Azure AD | Documenti Microsoft
description: Informazioni su come toofind il motivo per cui un set diverso di utenti viene effettuato il provisioning tooan applicazione rispetto a quelli previsti
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: adb90b12a53fb3160ce2b73b2559df92b283438e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a>Il set corretto di utenti stanno applicazione raccolta tooan provisioning Azure AD

Gli utenti che sono toohello provisioning app è principalmente dovute quali utenti e gruppi sono stati **assegnato** toohello applicazione.

Utilizzare le risorse di hello sotto toolearn come toocheck quali utenti e gruppi assegnati tooan applicazione in Azure Active Directory.

## <a name="assign-a-user-directly-as-an-administrator"></a>Assegnare un utente direttamente come amministratore

tooassign uno o più applicazioni tooan utenti direttamente, procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

  * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.

7.  Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.

9.  Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.

10. Tipo di hello **nome completo** o **indirizzo di posta elettronica** dell'utente hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.

11. Passare il mouse su hello **utente** in hello elenco tooreveal un **casella di controllo**. Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello dell'utente il toohello utente **selezionati** elenco.

12. **Facoltativo:** se si desidera troppo**aggiungere più di un utente**, in un altro tipo di **nome completo** o **indirizzo di posta elettronica** in hello **Cerca per nome o l'indirizzo di posta elettronica** casella di ricerca e fare clic su questo toohello utente hello casella di controllo tooadd **selezionati** elenco.

13. Al termine della selezione utenti, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.

14. **Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un ruolo tooassign toohello utenti selezionati.

15. Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gli utenti selezionati.

Se il provisioning è configurato ed è già in esecuzione per un'app, i nuovi utenti dovranno essere applicazione tooan provisioning in circa 10 minuti. Controllare hello **i log di controllo** per informazioni dettagliate.

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a>Assegnare un gruppo direttamente tooan applicazione come amministratore

tooassign uno o più gruppi di applicazioni tooan direttamente, seguire hello passaggi riportati di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

  * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.

7.  Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.

9.  Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.

10. Tipo di hello **nome del gruppo completo** del gruppo di hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.

11. Passare il mouse su hello **gruppo** in hello elenco tooreveal un **casella di controllo**. Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello del gruppo toohello l'utente **selezionati** elenco.

12. **Facoltativo:** se si desidera troppo**aggiungere più di un gruppo**, in un altro tipo di **nome del gruppo completo** in hello **ricerca per nome o indirizzo di posta** casella di ricerca Fare clic su hello casella di controllo tooadd toohello questo gruppo **selezionati** elenco.

13. Al termine della selezione gruppi, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.

14. **Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un toohello tooassign ruolo gruppi di sicurezza selezionato.

15. Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gruppi selezionati.

Se il provisioning è configurato ed è già in esecuzione per un'app, nuovi utenti, incluso nel gruppo di hello devono essere sottoposto a provisioning tooan applicazione circa 10 minuti. Controllare hello **i log di controllo** per informazioni dettagliate.

>[!IMPORTANT]
>Provisioning di hello nome del gruppo e gruppo dettagli, nei membri toohello inoltre, se supportato per alcune applicazioni. È possibile abilitare o disabilitare questa funzionalità abilitando o disabilitando hello **Mapping** per oggetti di gruppo visualizzati nelle hello **Provisioning** scheda. 
>
>

Se è abilitato il provisioning di gruppi, prestare attenzione tooreview hello attributo mapping tooensure un campo appropriato viene utilizzato per hello "corrispondente di ID". Può trattarsi di nome visualizzato hello o posta elettronica, alias, come hello gruppo e i relativi membri non essere disponibile se la proprietà corrispondente hello è vuota o non popolata per un gruppo in Azure AD.

## <a name="next-steps"></a>Passaggi successivi
[Automatizzare Provisioning e Deprovisioning tooSaaS applicazioni con Azure Active Directory](active-directory-saas-app-provisioning.md)
