---
title: 'Azure Active Directory Domain Services: Guida all''amministrazione | Documentazione Microsoft'
description: "Creare un'unità organizzativa (OU) nei domini gestiti di Servizi di dominio Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 52602ad8-2b93-4082-8487-427bdcfa8126
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: ce7539e5d5c7c1bf9505ef229f2d31d84c00da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-organizational-unit-ou-on-an-azure-ad-domain-services-managed-domain"></a>Creare un'unità organizzativa (OU) in un dominio gestito di Servizi di dominio Azure AD
I domini gestiti di Servizi di dominio Azure AD includono due contenitori predefiniti denominati rispettivamente "AADDC Computers" e "AADDC Users". Hello 'AADDC computer' contenitore dispone di oggetti computer per tutti i computer aggiunti toohello di dominio gestiti. contenitore 'AADDC Users' Hello include utenti e gruppi nel tenant di Azure AD hello. In alcuni casi, potrebbe essere account di servizio toocreate necessarie sui carichi di lavoro toodeploy dominio hello gestito. A tale scopo, è possibile creare un'unità organizzativa personalizzato (OU) nel dominio gestito hello e creare gli account del servizio all'interno di tale unità Organizzativa. In questo articolo illustra come toocreate un'unità Organizzativa nel dominio gestito.

## <a name="before-you-begin"></a>Prima di iniziare
attività di hello tooperform elencate in questo articolo, è necessario:

1. Una **sottoscrizione di Azure**valida.
2. Una **directory di Azure AD** sincronizzata con una directory locale o con una directory solo cloud.
3. **Servizi di dominio AD Azure** deve essere abilitato per la directory hello Azure AD. Se non è ancora fatto, seguire tutte le attività descritte nella hello hello [Guida introduttiva](active-directory-ds-getting-started.md).
4. Una macchina virtuale con dominio da cui si amministra i servizi di dominio hello Azure AD gestite dominio. Se non si dispone di questo tipo di una macchina virtuale, seguire tutte le attività hello descritte nell'articolo hello intitolata [aggiunta a un dominio gestito di macchina virtuale tooa Windows](active-directory-ds-admin-guide-join-windows-vm.md).
5. Sono necessarie le credenziali di hello di un **gruppo 'Administrators di controller di dominio di AAD' dell'utente account appartenenti toohello** nella directory, toocreate un'unità Organizzativa nel dominio gestito.

## <a name="install-ad-administration-tools-on-a-domain-joined-virtual-machine-for-remote-administration"></a>Installare gli strumenti di amministrazione di AD in una macchina virtuale aggiunta al dominio per l'amministrazione remota
Domini gestiti di servizi di dominio AD Azure possono essere gestiti in remoto mediante familiari strumenti di amministrazione di Active Directory, ad esempio hello Active Directory amministrativi centro o PowerShell di Active Directory. Gli amministratori tenant non sono controller di privilegi tooconnect toodomain hello dominio gestito tramite Desktop remoto. tooadminister hello dominio gestiti, installare funzionalità di strumenti di amministrazione di hello Active Directory in un dominio gestito toohello unita in join di macchina virtuale. Vedere l'articolo toohello [amministrare un dominio di servizi di dominio Active Directory di Azure gestito](active-directory-ds-admin-guide-administer-domain.md) per le istruzioni.

## <a name="create-an-organizational-unit-on-hello-managed-domain"></a>Creare un'unità organizzativa nel dominio gestito hello
Ora che sono installati strumenti di amministrazione di Active Directory hello hello dominio unito macchina virtuale, sarà possibile utilizzare toocreate questi strumenti un'unità organizzativa nel dominio hello gestito. Eseguire hello alla procedura seguente:

> [!NOTE]
> Solo i membri del gruppo 'Administrators di controller di dominio di AAD' hello hanno hello dei privilegi necessari toocreate un'unità Organizzativa. Assicurarsi di eseguire operazioni come utente appartenente al gruppo toothis hello.
>
>

1. Dalla schermata Start hello, fare clic su **strumenti di amministrazione**. Dovrebbe essere hello AD installati strumenti di amministrazione sulla macchina virtuale hello.

    ![Strumenti di amministrazione installati nel server](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. Fare clic su **Centro di amministrazione di Active Directory**.

    ![Centro di amministrazione di Active Directory](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. dominio hello tooview, fare clic sul nome di dominio hello nel riquadro di sinistra hello (ad esempio, ' contoso100.com').

    ![Centro di amministrazione di Active Directory - Visualizza dominio](./media/active-directory-domain-services-admin-guide/create-ou-adac-overview.png)
4. Sul lato destro hello **attività** riquadro, fare clic su **New** nel nodo di nome di dominio hello. In questo esempio, si fa clic **New** nel nodo 'contoso100(local)' hello sul lato destro hello **attività** riquadro.

    ![Centro di amministrazione di Active Directory - Nuova OU](./media/active-directory-domain-services-admin-guide/create-ou-adac-new-ou.png)
5. Dovrebbe essere hello opzione toocreate un'unità organizzativa. Fare clic su **unità organizzativa** toolaunch hello **Crea unità organizzativa** finestra di dialogo.
6. In hello **Crea unità organizzativa** finestra di dialogo, specificare un **nome** per hello nuova unità Organizzativa. Fornire una breve descrizione di hello unità Organizzativa. È inoltre possibile impostare hello **gestito da** field per hello unità Organizzativa. toocreate hello OU personalizzato, fare clic su **OK**.

    ![Centro di amministrazione di Active Directory - finestra di dialogo Crea OU](./media/active-directory-domain-services-admin-guide/create-ou-dialog.png)
7. Hello appena creati OU dovrebbe ora apparire in hello AD amministrazione centro.

    ![Centro di amministrazione di Active Directory - OU creata](./media/active-directory-domain-services-admin-guide/create-ou-done.png)

## <a name="permissionssecurity-for-newly-created-ous"></a>Autorizzazioni/sicurezza per le OU appena create
Per impostazione predefinita, l'utente hello (membro del gruppo di hello 'AAD DC Administrators') che ha creato l'unità Organizzativa è dispongono di privilegi amministrativi (controllo completo) su hello hello unità Organizzativa. Hello è possibile quindi proseguo e concedere agli utenti di privilegi tooother o toohello ' AAD controller di dominio ' Administrators in base alle esigenze. Come mostrato nella seguente schermata hello, hello utente 'bob@domainservicespreview.onmicrosoft.com' che ha creato hello 'MyCustomOU' unità organizzativa viene concesso il controllo completo su di esso.

 ![Centro di amministrazione di Active Directory - Sicurezza della nuova OU](./media/active-directory-domain-services-admin-guide/create-ou-permissions.png)

## <a name="notes-on-administering-custom-ous"></a>Note sull'amministrazione delle OU personalizzate
Dopo avere creato un'unità organizzativa personalizzata, è possibile procedere alla creazione di utenti, gruppi, computer e account del servizio in questa unità organizzativa. È possibile spostare gli utenti o gruppi da hello unità organizzative di toocustom OU 'AADDC Users'.

> [!WARNING]
> Account utente, gruppi, account del servizio e oggetti computer creati in unità organizzative personalizzate non sono disponibili nel tenant di Azure AD. In altre parole, questi oggetti non vengono visualizzati utilizzando l'API di Azure AD Graph hello o nell'interfaccia utente AD Azure hello. Questi oggetti saranno disponibili solo nel dominio gestito di Servizi di dominio Azure AD.
>
>

## <a name="related-content"></a>Contenuti correlati
* [Amministrare un dominio gestito di Servizi di dominio Azure AD](active-directory-ds-admin-guide-administer-domain.md)
* [Configurare criteri di gruppo in un dominio gestito](active-directory-ds-admin-guide-administer-group-policy.md)
* [Centro di amministrazione di Active Directory: Introduzione](https://technet.microsoft.com/library/dd560651.aspx)
* [Guida dettagliata agli account del servizio gestiti](https://technet.microsoft.com/library/dd548356.aspx)
