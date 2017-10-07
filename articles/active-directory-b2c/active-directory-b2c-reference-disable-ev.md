---
title: 'Azure Active Directory B2C: disabilitare la verifica tramite posta elettronica durante l''iscrizione dell''utente | Documentazione Microsoft'
description: Un argomento che illustra come toodisable posta elettronica di verifica durante l'iscrizione in Azure Active Directory B2C consumer
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: a8a42eddcb577725f04d70e1b1ebbebf10b5937c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a>Azure Active Directory B2C: disabilitare la verifica tramite posta elettronica durante l'iscrizione dell'utente
Quando abilitata, B2C Azure Active Directory (Azure AD) offre un consumer hello toosign possibilità per applicazioni fornendo un indirizzo di posta elettronica e la creazione di un account locale. Azure Active Directory B2C assicura gli indirizzi di posta elettronica valido richiedendo consumer tooverify loro durante il processo di iscrizione hello. Impedisce inoltre un processo automatizzato dannoso la generazione di un account fittizio per le applicazioni di hello.

Alcuni sviluppatori di applicazioni preferiscono tooskip verifica della posta elettronica durante il processo di iscrizione hello e invece che disponga di consumer verifica indirizzo di posta elettronica hello in un secondo momento. toosupport, Azure AD B2C può essere configurato toodisable verifica della posta elettronica. In questo modo viene creato un processo di iscrizione più uniforme e offre agli sviluppatori hello flessibilità toodifferentiate hello i consumer accertato l'indirizzo di posta elettronica da tali utenti che non siano.

Per impostazione predefinita, nei criteri di iscrizione la verifica tramite posta elettronica è abilitata. Utilizzare hello seguendo i passaggi tooturn disattivata:

1. [Seguire questi blade di passaggi toonavigate toohello B2C funzionalità nel portale di Azure hello](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Fare clic su **Criteri di iscrizione** o su **Criteri di iscrizione o di accesso**, a seconda della configurazione usata per l'iscrizione.
3. Fare clic su tooopen i criteri (ad esempio, "B2C_1_SiUp") è. Fare clic su **modifica** nella parte superiore di hello del pannello hello.
4. Fare clic su **Personalizzazione dell'interfaccia utente della pagina**.
5. Fare clic su **Pagina di iscrizione dell'account locale**.
6. Fare clic su **indirizzo di posta elettronica** in hello **nome** colonna sotto hello **attributi iscrizione** sezione.
7. Hello attiva/disattiva **Richiedi verifica** opzione troppo**n**.
8. Fare clic su **OK** nella parte inferiore di hello fino a raggiungere hello **Modifica criterio** blade.
9. Fare clic su **salvare** nella parte superiore di hello del pannello hello. L'operazione è completata.

> [!NOTE]
> Disabilitare la verifica tramite posta elettronica nel processo di iscrizione hello può causare toospam. Se si disabilita predefinito hello, è consigliabile aggiungere il sistema di verifica.
> 
> 

Ci sono sempre toofeedback aperti e i suggerimenti! Se si hanno difficoltà a questo argomento o avere indicazioni per migliorare il contenuto, Gradiremmo commenti e suggerimenti nella parte inferiore di hello della pagina hello. Per le richieste di funzionalità, aggiungerli troppo[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).
