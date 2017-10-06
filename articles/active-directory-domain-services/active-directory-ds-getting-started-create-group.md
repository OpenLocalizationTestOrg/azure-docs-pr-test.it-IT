---
title: 'Azure Active Directory Domain Services: Crea gruppo di amministratori di controller di dominio hello Azure AD | Documenti Microsoft'
description: Abilitare Azure Active Directory Domain Services utilizzando hello portale di Azure classico
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Abilitare Azure Active Directory Domain Services utilizzando hello portale di Azure classico
Questo articolo descrive e illustra le attività di configurazione hello necessarie tooenable Azure Active Directory servizi di dominio (Azure AD DS) per il tenant di Azure Active Directory (Azure AD).

> [!NOTE]
> [**Provare esperienza del portale Azure (anteprima) nuovo hello**](active-directory-ds-getting-started.md). 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a>Attività 1: creare gruppo di amministratori di controller di dominio hello Azure AD
Hello prima attività è toocreate un gruppo amministrativo nel tenant di Azure AD. Questo gruppo amministrativo speciale è chiamato *AAD DC Administrators*. Membri di questo gruppo vengono concesse le autorizzazioni amministrative nei computer che sono toohello appartenenti a un dominio gestito di Azure Active Directory Domain Services dominio. In computer appartenenti a un dominio, questo gruppo viene aggiunto il gruppo di amministratori toohello. Inoltre, i membri di questo gruppo è possono utilizzare Desktop remoto tooconnect in modalità remota toodomain computer appartenenti a un.  

> [!NOTE]
> Non si dispone delle autorizzazioni di amministratore dell'organizzazione o di amministratore di dominio nel dominio gestito hello creato tramite Azure Active Directory Domain Services. Nei domini gestiti, queste autorizzazioni sono riservate dal servizio hello e non vengono resi disponibili toousers nel tenant di hello. Tuttavia, è possibile utilizzare gruppo amministrativo di hello speciale creato in questa tooperform di attività di configurazione alcune operazioni privilegiate. Tali operazioni includono l'aggiunta a dominio toohello computer appartenenti toohello gruppo di amministrazione nei computer appartenenti a un dominio e la configurazione dei criteri di gruppo.
>

In questa attività di configurazione, si crea il gruppo amministrativo di hello e aggiungere uno o più utenti del gruppo toohello directory. gruppo amministrativo di hello toocreate per Azure Active Directory Domain Services hello seguenti:

1. Passare toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Nel riquadro sinistro hello selezionare hello **Active Directory** pulsante.
3. Selezionare tenant di Azure AD hello (directory) per il quale si desidera tooenable Azure servizi di dominio Active Directory. È possibile creare solo un dominio per ogni directory di Azure AD.

    ![Selezionare la directory di Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. In hello **directory anteprima** pagina, fare clic su hello **gruppi** scheda.
5. Fare clic su un tenant di Azure AD tooyour gruppo, nel riquadro attività hello nella parte inferiore di hello della finestra hello, tooadd **Aggiungi gruppo**.

    ![pulsante Aggiungi gruppo Hello](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. In hello **Aggiungi gruppo** finestra di dialogo casella, creare un gruppo denominato **gli amministratori di controller di dominio di AAD**, quindi impostare **tipo di gruppo** troppo**sicurezza**.

   > [!WARNING]
   > accesso tooenable all'interno del dominio gestito di Azure Active Directory Domain Services, creare un gruppo con lo stesso nome.
   >
   >

    ![finestra di dialogo Aggiungi gruppo Hello](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. In hello **descrizione** , immettere una descrizione che consente ad altri utenti toounderstand che questo gruppo concede le autorizzazioni amministrative all'interno di servizi di dominio di Azure Active Directory.
8. Dopo aver creato il gruppo di hello, fare clic su tooview nome gruppo di hello le relative proprietà.
9. tooadd utenti come membri del gruppo di hello, nella parte inferiore di hello della finestra hello, fare clic su hello **Aggiungi membri** pulsante.

    ![Pulsate Aggiungi membri gruppo](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. In hello **aggiungere membri** nella finestra di dialogo hello selezionare gli utenti devono essere membri del gruppo e quindi fare clic sull'icona di segno di spunta hello in hello in basso a destra.

    ![Aggiungere il gruppo di utenti tooadministrators](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a>Passaggio successivo
[Attività 2: creare o selezionare una rete virtuale di Azure](active-directory-ds-getting-started-vnet.md)
