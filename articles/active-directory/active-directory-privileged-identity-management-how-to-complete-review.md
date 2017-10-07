---
title: aaaHow toocomplete una revisione accesso | Documenti Microsoft
description: "Dopo che è stata avviata una verifica di accesso in Azure AD Privileged Identity Management, informazioni su come toocomplete e Visualizza risultati di hello"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a>Come toocomplete esaminare un accesso in Azure AD Privileged Identity Management
Gli amministratori dei ruoli con privilegi possono esaminare l'accesso con privilegi dopo che è stata [avviata una verifica della sicurezza](active-directory-privileged-identity-management-how-to-start-security-review.md). Azure AD Privileged Identity Management (PIM) invia automaticamente un messaggio di posta elettronica che richiede tooreview agli utenti l'accesso. Se un utente non ha ottenuto un messaggio di posta elettronica, è possibile inviarli istruzioni hello in [come tooperform una sicurezza esaminare](active-directory-privileged-identity-management-how-to-perform-security-review.md).

Dopo la fase di revisione di sicurezza hello o tutti gli utenti di hello hanno terminato loro self-esaminare, seguire i passaggi hello in hello toomanage questo articolo e visualizzare i risultati di hello.

## <a name="manage-security-reviews"></a>Gestire le verifiche della sicurezza
1. Passare toohello [portale di Azure](https://portal.azure.com/) e seleziona hello **Azure AD Privileged Identity Management** applicazione nel dashboard.
2. Seleziona hello **accedere revisioni** sezione dashboard hello.
3. Selezionare una revisione accesso hello che si desidera toomanage.

Nel Pannello di dettaglio della revisione accesso hello esistono un numero opzioni per la gestione di tale revisione.

![Schermata dei pulsanti di verifica dell'accesso PIM][1]

### <a name="remind"></a>Promemoria
Se una revisione di accesso è configurata in modo che gli utenti di hello esaminare autonomamente, hello **promemoria** pulsante Invia una notifica. 

### <a name="stop"></a>Arresto
Tutte le revisioni accesso hanno una data di fine, ma è possibile utilizzare hello **arrestare** toofinish pulsante è all'inizio. Se tutti gli utenti non sono stato implementati entro questo periodo, non sarà in grado di tooafter si arresta la revisione di hello. Non è possibile riavviare una verifica dopo che è stata interrotta.

### <a name="apply"></a>Applica
Al termine di una revisione di accesso, sia perché si raggiunge la data di fine hello o interrotto manualmente, hello **applica** pulsante implementa risultato hello della revisione hello. Se nella revisione di hello è stato negato l'accesso dell'utente, questo è passaggio hello rimuoverà l'assegnazione di ruolo.  

### <a name="export"></a>Esporta
Se si desidera risultati hello tooapply di revisione della sicurezza hello manualmente, è possibile esportare revisione hello. Hello **esportare** pulsante verrà avviato il download di un file CSV. È possibile gestire i risultati di hello in Excel o in altri programmi in cui aprire il file CSV.

### <a name="delete"></a>Elimina
Se non si è interessati in hello rivedere le ulteriori, eliminarlo. Hello **eliminare** pulsante rimuove l'applicazione PIM hello hello revisione.

> [!IMPORTANT]
> È non verrà visualizzato un avviso prima che l'eliminazione viene eseguita, pertanto è necessario assicurarsi che si desidera toodelete che esaminare. 

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
