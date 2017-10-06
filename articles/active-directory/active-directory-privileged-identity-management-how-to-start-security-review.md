---
title: aaaHow toostart una revisione accesso | Documenti Microsoft
description: "Informazioni su come toocreate esaminare un accesso per l'identità con privilegi con hello applicazione Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a>Come toostart esaminare un accesso in Azure AD Privileged Identity Management
Le assegnazioni dei ruoli diventano "obsolete" quando gli utenti hanno accessi con privilegi di cui non necessitano più. Ordine tooreduce hello rischio associato a queste assegnazioni di ruolo non aggiornato, gli amministratori di ruolo con privilegi devono esaminare regolarmente ruoli hello che gli utenti sono stati assegnati. Questo documento descrive i passaggi di hello per l'avvio di una revisione dell'accesso in Azure AD Privileged Identity Management (PIM).

## <a name="start-an-access-review"></a>Avviare una verifica dell'accesso
> [!NOTE]
> Se non si aggiunti dashboard tooyour dell'applicazione di PIM hello in hello portale di Azure, vedere la procedura di hello in [Introduzione a Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)
> 
> 

Dalla pagina principale dell'applicazione PIM hello, sono disponibili tre modi toostart una revisione di accesso:

* **Verifiche di accesso** > **Aggiungi**
* **Ruoli** > **Verifica**
* Rivisto toobe ruolo specifico hello selezionare dall'elenco di ruoli hello > **revisione** pulsante

Quando fa clic su hello **esaminare** pulsante hello **avviare una verifica di accesso** pannello viene visualizzato. In questo pannello, in corso la revisione di hello tooconfigure con un nome e limite di tempo, scegliere un ruolo tooreview e decidere che eseguirà la revisione di hello.

![Schermata Inizia una verifica di accesso][1]

### <a name="configure-hello-review"></a>Configurare la revisione di hello
esaminare un accesso toocreate, è necessario tooname e impostare una data di inizio e fine.

![Schermata di configurazione della verifica][2]

Verificare che lunghezza hello di hello viene rivisto un tempo sufficiente per gli utenti toocomplete. Se termina prima della data di fine hello, è possibile arrestare sempre la revisione di hello in anticipo.

### <a name="choose-a-role-tooreview"></a>Scegliere un ruolo tooreview
Ogni verifica è incentrata su un solo ruolo. A meno che non è stato avviato hello accesso revisione dal pannello ruolo specifico, è necessario ora toochoose un ruolo.

1. Passare troppo**esaminare l'appartenenza al ruolo**
   
    ![Schermata Verifica l'appartenenza ai ruoli][3]
2. Scegliere un ruolo dall'elenco di hello.

### <a name="decide-who-will-perform-hello-review"></a>Decidere chi eseguirà la revisione di hello
Sono disponibili tre opzioni per l'esecuzione di una verifica. È possibile assegnare hello revisione toosomeone toocomplete altro, è possibile farlo manualmente oppure è possibile esaminare le proprie accesso avere ogni utente.

1. Passare troppo**selezionare revisori**
   
    ![Schermata Selezionare i revisori][4]
2. Scegliere una delle opzioni di hello:
   
   * **Seleziona il revisore**: usare questa opzione quando non è noto chi abbia bisogno dell'accesso. Con questa opzione, è possibile assegnare proprietario della risorsa hello revisione tooa o toocomplete gestione gruppo.
   * **Me**: utile se si desidera toopreview come accesso revisioni del lavoro o se si desidera tooreview per conto di utenti che non è possibile.
   * **I membri esaminare stessi**: usare questa revisione agli utenti di opzione toohave hello assegnazioni di ruolo.

### <a name="start-hello-review"></a>Avviare hello revisione
Infine, è necessario toorequire opzione hello agli utenti di fornire un motivo se approvare l'accesso. Se si desidera aggiungere una descrizione della revisione hello e selezionare **avviare**.

Assicurarsi che si consente agli utenti a indicare che una revisione accesso attenderne e visualizzarle [come tooperform un accesso esaminare](active-directory-privileged-identity-management-how-to-perform-security-review.md).

## <a name="manage-hello-access-review"></a>Gestire hello accesso revisione
È possibile monitorare lo stato di avanzamento hello come revisori hello completare le revisioni nel dashboard di Azure AD PIM hello, sezione esaminate in hello. Nessun diritto di accesso verrà modificato nella directory hello finché [revisione hello completa](active-directory-privileged-identity-management-how-to-complete-review.md).

Fino al periodo di revisione hello, è possibile tenere la revisione toocomplete gli utenti o arresto hello revisione tempestivamente dall'accesso di hello esamina sezione.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a>Sommario PIM
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
