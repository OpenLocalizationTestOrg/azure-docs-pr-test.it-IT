---
title: le applicazioni aaaHow vengono visualizzate nel Pannello di accesso hello | Documenti Microsoft
description: "Risoluzione dei problemi perché un'applicazione viene visualizzato nel Pannello di accesso hello"
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
ms.reviewr: japere
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a>Modalità di visualizzazione di applicazioni nel Pannello di accesso hello

Hello Pannello di accesso è un portale basato sul web che consente a un utente con un lavoro o account Azure Active Directory (Azure AD) tooview avvio basato su cloud le applicazioni e dell'istituto di istruzione che hello amministratore di Azure AD ha concesso l'accesso a. Queste applicazioni sono configurate per conto di utente hello nel portale di Azure AD hello. può eseguire il provisioning salve hello applicazione toohello utente direttamente o tooa gruppo che un utente fa parte di risultante in un'applicazione hello visualizzati nel Pannello di accesso dell'utente hello.

## <a name="general-issues-toocheck-first"></a>Generale problemi toocheck prima

-   Se un'applicazione è stata rimossa solo da un utente o gruppo hello utente è membro di, riprovare toosign avanti e indietro nel Pannello di accesso dell'utente hello dopo pochi minuti toosee se un'applicazione hello viene rimosso.

-   Se una licenza è stata rimossa solo da un utente o gruppo utente hello è che un membro di questo potrebbe richiedere molto tempo, a seconda delle dimensioni di hello e la complessità del gruppo di hello per toobe le modifiche apportate. Consentire del tempo aggiuntivo prima della firma in hello Pannello di accesso.

## <a name="problems-related-tooassigning-applications-toousers"></a>Problemi correlati tooassigning applicazioni toousers

Un utente può essere visualizzata un'applicazione nel proprio pannello di accesso perché che è stata precedentemente assegnate tooit. Di seguito sono toocheck alcuni modi:

-   [Verificare se un utente è assegnato toohello applicazione](#check-if-a-user-is-assigned-to-the-application)

-   [Controllare se un utente è in una licenza correlati toohello applicazione](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a>Verificare se un utente è assegnato toohello applicazione

toocheck se un utente è assegnato toohello applicazione, attenersi alla procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

6.  **Ricerca** per nome hello dell'applicazione hello in questione.

7.  Fare clic su **Utenti e gruppi**.

8.  Controllare toosee se l'utente è assegnato toohello applicazione.

  * Se si desidera tooremove hello utente da un'applicazione hello, **fare clic sulla riga hello** dell'utente hello e selezionare **eliminare**.

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a>Controllare se un utente è in una licenza correlati toohello applicazione

toocheck un utente assegnate le licenze, seguire hello passaggi riportati di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti gli utenti**.

6.  **Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su **licenze** toosee utente hello licenze è attualmente assegnato.

   * Se utente hello viene assegnata una licenza di Office tooan tooappear applicazioni di Office di terze parti prima in questo modo su hello nel Pannello di accesso dell'utente.

## <a name="problems-related-tooassigning-applications-toogroups"></a>Problemi correlati tooassigning applicazioni toogroups

Un utente potrebbe contenere un'applicazione nel proprio pannello di accesso perché fanno parte di un gruppo che dispone di un'applicazione hello. Di seguito sono toocheck alcuni modi:

-   [Controllare le appartenenze ai gruppi di un utente ](#check-a-users-group-memberships)

-   [Controllare se un utente è un membro di un gruppo dispone di licenza tooa](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a>Controllare le appartenenze a gruppi dell'utente

toocheck appartenenza a un gruppo, seguire hello passaggi riportati di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti gli utenti**.

6.  **Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su **gruppi.**

8.  Controllare toosee se l'utente fa parte di un'applicazione toohello gruppo assegnato.

   * Se si desidera tooremove hello utente dal gruppo di hello, **fare clic sulla riga hello** del gruppo di hello e seleziona Elimina.

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a>Controllare se un utente è un membro di un gruppo dispone di licenza tooa

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Tutti gli utenti**.

6.  **Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.

7.  Fare clic su **gruppi.**

8.  Fare clic sulla riga hello di un gruppo specifico.

9.  Fare clic su **licenze** toosee quale gruppo di licenze hello è assegnato tooit.

  * Se gruppo hello viene assegnata una licenza di Office tooan in che questo potrebbe rendere determinati tooappear applicazioni di Office di terze parti prima hello nel Pannello di accesso dell'utente.


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Se questi passaggi di risoluzione dei problemi non hello di risolvere il problema di hello

Aprire un ticket di supporto con hello se disponibili le seguenti informazioni:

-   ID errore di correlazione

-   UPN (indirizzo di posta elettronica dell'utente)

-   ID tenant

-   Tipo di browser

-   Fuso orario e ora o intervallo di tempo durante il quale si verifica l'errore

-   Tracce Fiddler

## <a name="next-steps"></a>Passaggi successivi
[Gestione di applicazioni con Azure Active Directory](active-directory-enable-sso-scenario.md)
