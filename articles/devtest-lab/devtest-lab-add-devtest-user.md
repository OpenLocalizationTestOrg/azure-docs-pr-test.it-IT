---
title: aaaAdd proprietari e utenti in Azure DevTest Labs | Documenti Microsoft
description: Aggiungere proprietari e utenti in Azure DevTest Labs con hello portale di Azure o PowerShell
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a>Aggiungere proprietari e utenti in Azure DevTest Labs
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

L'accesso in Azure DevTest Labs è controllato dal [Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-what-is.md). Usa tale controllo, è possibile isolare il compiti all'interno del team in *ruoli* in cui si quantità di concessioni solo hello di accesso necessarie toousers tooperform il proprio lavoro. Tre di questi ruoli Controllo degli accessi in base al ruolo sono *Proprietario*, *Utente DevTest Labs* e *Collaboratore*. In questo articolo viene illustrato quali azioni possono essere eseguite in ciascuno dei tre ruoli RBAC principali hello. Da qui, si apprenderà come entrambi tramite lab tooa agli utenti di tooadd - hello portale e tramite uno script di PowerShell, e come gli utenti tooadd hello livello di sottoscrizione.

## <a name="actions-that-can-be-performed-in-each-role"></a>Azioni che possono essere eseguite in ogni ruolo
Esistono tre ruoli principali che è possibile assegnare a un utente:

* Proprietario
* Utente DevTest Labs
* Collaboratore

Hello nella tabella seguente vengono illustrate le azioni che possono essere eseguite dagli utenti in ciascuno di questi ruoli hello:

| **Azioni che gli utenti in questo ruolo possono eseguire** | **Utente DevTest Labs** | **Proprietario** | **Collaboratore** |
| --- | --- | --- | --- |
| **Attività lab** | | | |
| Aggiungere lab tooa utenti |No |Sì |No |
| Aggiornare le impostazioni dei costi |No |Sì |Sì |
| **Attività di base delle VM** | | | |
| Aggiungere e rimuovere immagini personalizzate |No |Sì |Sì |
| Aggiungere, aggiornare ed eliminare formule |Sì |Sì |Sì |
| Aggiungere all'elenco elementi consentiti le immagini di Azure Marketplace |No |Sì |Sì |
| **Attività della macchina virtuale** | | | |
| Creare VM |Sì |Sì |Sì |
| Avviare, arrestare ed eliminare VM |Solo macchine virtuali create dall'utente hello |Sì |Sì |
| Aggiornare i criteri delle VM |No |Sì |Sì |
| Aggiungere/Rimuovere dischi dati nelle VM |Solo macchine virtuali create dall'utente hello |Sì |Sì |
| **Attività degli elementi** | | | |
| Aggiungere e rimuovere repository di elementi |No |Sì |Sì |
| Applicare elementi |Sì |Sì |Sì |

> [!NOTE]
> Quando un utente crea una macchina virtuale, tale utente viene assegnato automaticamente toohello **proprietario** ruolo di macchina virtuale creata hello.
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a>Aggiungere un proprietario o un utente a livello di hello lab
I proprietari e gli utenti possono essere aggiunti al livello di lab hello tramite hello portale di Azure. Sono inclusi gli utenti esterni con un [account Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account)valido.
Hello alla procedura seguente consentono di eseguire il processo di hello di aggiunta di un ambiente lab tooa proprietario o l'utente in Azure DevTest Labs:

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.
3. Elenco dei laboratori hello selezionare lab desiderato hello.
4. Nel pannello del lab hello, selezionare **configurazione**. 
5. In hello **configurazione** pannello seleziona **utenti**.
6. In hello **utenti** pannello seleziona **+ Aggiungi**.
   
    ![Add user](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. In hello **selezionare un ruolo** blade, ruolo desiderato selezionare hello. Hello sezione [azioni che possono essere eseguite in ogni ruolo](#actions-that-can-be-performed-in-each-role) elenchi hello diverse azioni che possono essere eseguite dagli utenti nei ruoli di proprietario, di utente DevTest e collaboratore hello.
8. In hello **aggiungere utenti** pannello, immettere l'indirizzo di posta elettronica hello o il nome dell'utente di hello si vuole tooadd nel ruolo hello è specificato. Se non è possibile trovare l'utente hello, un messaggio di errore viene illustrato il problema di hello. Se l'utente hello viene trovato, tale utente sia elencato e selezionato. 
9. Scegliere **Seleziona**.
10. Selezionare **OK** tooclose hello **aggiungere accesso** blade.
11. Quando si torna toohello **utenti** pannello hello utente è stato aggiunto.  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a>Aggiungere un ambiente lab tooa utente esterno tramite PowerShell
Inoltre gli utenti tooadding hello portale di Azure, è possibile aggiungere un ambiente lab tooyour utente esterno utilizzando uno script di PowerShell. In hello seguente esempio, è sufficiente modificare i valori dei parametri hello in hello **toochange valori** commento.
È possibile recuperare hello `subscriptionId`, `labResourceGroup`, e `labName` valori dal pannello lab hello in hello portale di Azure.

> [!NOTE]
> script di esempio Hello si presuppone che hello specificato l'utente è stato aggiunto come un toohello guest Active Directory e avrà esito negativo se non è questo caso di hello. tooadd un utente non hello lab tooa Active Directory, utilizzare ruolo tooa di hello tooassign portale Azure hello utente come illustrato nella sezione hello, [aggiungere un proprietario o un utente a livello di lab hello](#add-an-owner-or-user-at-the-lab-level).   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a>Aggiungere un proprietario o un utente a livello di sottoscrizione hello
Autorizzazioni di Azure vengono propagate dall'ambito di toochild ambito padre in Azure. Quindi i proprietari di una sottoscrizione di Azure contenente lab sono automaticamente proprietari di tali lab. Possiedono anche le macchine virtuali hello e altre risorse create da utenti dell'ambiente di test di hello e servizio Azure DevTest Labs hello. 

È possibile aggiungere lab tooa proprietari aggiuntivi tramite il pannello del lab hello in hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). Tuttavia, hello aggiunta ambiti del proprietario di amministrazione non sono più ampia di ambito del proprietario della sottoscrizione hello. Ad esempio hello aggiunta di proprietari non dispone di accesso completo toosome delle risorse di hello che vengono creati nella sottoscrizione hello hello servizio DevTest Labs. 

tooadd un tooan proprietario sottoscrizione di Azure, seguire questi passaggi:

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selezionare **più servizi**, quindi selezionare **sottoscrizioni** dall'elenco di hello.
3. Selezionare la sottoscrizione hello desiderato.
4. Selezionare l'icona **Accesso** . 
   
    ![Utenti di accesso](./media/devtest-lab-add-devtest-user/access-users.png)
5. In hello **utenti** pannello seleziona **Aggiungi**.
   
    ![Add user](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. In hello **selezionare un ruolo** pannello selezionare **proprietario**.
7. In hello **aggiungere utenti** pannello, immettere l'indirizzo di posta elettronica hello o il nome dell'utente hello desiderato tooadd come proprietario. Se l'utente hello non viene trovato, viene visualizzato un messaggio di errore che spiega il problema di hello. Se l'utente hello viene trovato, tale utente è elencato in hello **utente** casella di testo.
8. Selezionare il nome di un utente si trova hello.
9. Scegliere **Seleziona**.
10. Selezionare **OK** tooclose hello **aggiungere accesso** blade.
11. Quando si torna toohello **utenti** pannello hello utente è stato aggiunto come proprietario. L'utente è ora un proprietario di un lab creato in questa sottoscrizione e pertanto essere tooperform in grado di attività di proprietario. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

