---
title: di aaaHow tooremove un utente accedere alle applicazioni tooan | Documenti Microsoft
description: Comprendere come di tooremove un utente accedere a tooan applicazione
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
ms.openlocfilehash: 17017bddb73aad5a0ef3a411ac91bf0423f0b600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooremove-a-users-access-tooan-application"></a>Come di tooremove un utente accedere a tooan applicazione

Questo articolo è utile toounderstand come del tooremove un utente applicazione tooan di accesso.

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a>Voglio tooremove dell'applicazione tooan di assegnazione di un utente specifico o del gruppo

tooremove un'applicazione di tooan assegnazione utente o gruppo, seguire i passaggi di hello elencati in hello [rimuovere l'assegnazione di un utente o gruppo da un'applicazione aziendale in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) articolo.

. # # voglio toodisable tutte le applicazioni di tooan di accesso per ogni utente

toodisable tutti utente accessi tooan dell'applicazione, seguire la procedura seguente hello elencata in hello [disabilitare l'accesso degli utenti per un'applicazione aziendale in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) articolo.

## <a name="i-want-toodelete-an-application-entirely"></a>Voglio toodelete un'applicazione completamente

troppo**eliminare un'applicazione**, seguire le istruzioni di hello seguenti:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

   * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello da toodelete.

7.  Una volta che un'applicazione hello caricato, fare clic su **eliminare** icona dell'applicazione principale hello **Panoramica** blade.

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a>Voglio toodisable tutti i futuri consenso operazioni tooany dell'applicazione

La disabilitazione di consenso dell'utente per l'intera directory impedire agli utenti finali di consenso tooany applicazione. Gli amministratori possono sempre dare consenso per conto degli utenti. toolearn più sull'applicazione di consenso e motivi per cui è possibile o potrebbe non essere toodo, lettura [consenso dell'amministratore e utente di conoscenza](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).

troppo**disabilitare tutte le operazioni utente future consenso nella directory intera**, seguire le istruzioni di hello seguenti:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **utenti e gruppi** nel menu di navigazione hello.

5.  Fare clic su **Impostazioni utente**.

6.  Disabilitare tutte le operazioni di consenso utente future impostazione hello **gli utenti possono consentire App tooaccess i propri dati** attivare o disattivare troppo**n** e fare clic su hello **salvare** pulsante.


# <a name="next-steps"></a>Passaggi successivi
[La gestione di accesso tooapps](active-directory-managing-access-to-apps.md)
