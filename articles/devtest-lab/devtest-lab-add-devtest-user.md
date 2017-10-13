---
title: Aggiungere proprietari e utenti in Azure DevTest Labs | Documentazione Microsoft
description: Aggiungere proprietari e utenti in Azure DevTest Labs usando il portale di Azure o PowerShell
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
ms.openlocfilehash: d67fa257574d6cb4ad4b18521900374fb51da290
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a>Aggiungere proprietari e utenti in Azure DevTest Labs
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

L'accesso in Azure DevTest Labs è controllato dal [Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-what-is.md). Usando il Controllo degli accessi in base al ruolo, è possibile separare i compiti del team in *ruoli* in cui si concede solo la quantità di accesso necessaria agli utenti per svolgere il proprio lavoro. Tre di questi ruoli Controllo degli accessi in base al ruolo sono *Proprietario*, *Utente DevTest Labs* e *Collaboratore*. In questo articolo vengono indicate le azioni che possono essere eseguite in ognuno dei tre ruoli Controllo degli accessi in base al ruolo principali. Viene poi illustrato come aggiungere utenti a un lab, sia tramite il portale che tramite uno script di PowerShell, e come aggiungere utenti a livello di sottoscrizione.

## <a name="actions-that-can-be-performed-in-each-role"></a>Azioni che possono essere eseguite in ogni ruolo
Esistono tre ruoli principali che è possibile assegnare a un utente:

* Proprietario
* Utente DevTest Labs
* Collaboratore

La tabella seguente illustra le azioni che possono essere eseguite dagli utenti in ognuno di questi ruoli:

| **Azioni che gli utenti in questo ruolo possono eseguire** | **Utente DevTest Labs** | **Proprietario** | **Collaboratore** |
| --- | --- | --- | --- |
| **Attività lab** | | | |
| Aggiungere utenti a un lab |No |Sì |No |
| Aggiornare le impostazioni dei costi |No |Sì |Sì |
| **Attività di base delle VM** | | | |
| Aggiungere e rimuovere immagini personalizzate |No |Sì |Sì |
| Aggiungere, aggiornare ed eliminare formule |Sì |Sì |Sì |
| Aggiungere all'elenco elementi consentiti le immagini di Azure Marketplace |No |Sì |Sì |
| **Attività della macchina virtuale** | | | |
| Creare VM |Sì |Sì |Sì |
| Avviare, arrestare ed eliminare VM |Solo VM create dall'utente |Sì |Sì |
| Aggiornare i criteri delle VM |No |Sì |Sì |
| Aggiungere/Rimuovere dischi dati nelle VM |Solo VM create dall'utente |Sì |Sì |
| **Attività degli elementi** | | | |
| Aggiungere e rimuovere repository di elementi |No |Sì |Sì |
| Applicare elementi |Sì |Sì |Sì |

> [!NOTE]
> Quando un utente crea una VM, tale utente viene automaticamente assegnato al ruolo **Proprietario** della VM creata.
> 
> 

## <a name="add-an-owner-or-user-at-the-lab-level"></a>Aggiungere un utente o un proprietario a livello di lab
Proprietari e utenti possono essere aggiunti a livello di lab tramite il portale di Azure. Sono inclusi gli utenti esterni con un [account Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account)valido.
Il processo di aggiunta di un proprietario o di un utente a un lab in Azure DevTest Labs prevede i passaggi seguenti:

1. Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selezionare **Altri servizi** e quindi **DevTest Labs** dall'elenco.
3. Nell'elenco dei lab selezionare il lab desiderato.
4. Nel pannello del lab selezionare **Configurazione**. 
5. Nel pannello **Configurazione** selezionare **Utenti**.
6. Nel pannello **Utenti** selezionare **+Aggiungi**.
   
    ![Add user](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. Nel pannello **Selezionare un ruolo** selezionare il ruolo desiderato. La sezione [Azioni che possono essere eseguite in ogni ruolo](#actions-that-can-be-performed-in-each-role) elenca le diverse azioni che possono essere eseguite dagli utenti nei ruoli Proprietario, Utente DevTest Labs e Collaboratore.
8. Nel pannello **Aggiungi utenti** immettere l'indirizzo di posta elettronica o il nome dell'utente che si vuole aggiungere nel ruolo specificato. Se l'utente non viene trovato, un messaggio di errore spiega il problema. Se l'utente viene trovato, tale utente è elencato e selezionato. 
9. Scegliere **Seleziona**.
10. Selezionare **OK** per chiudere il pannello **Aggiungi accesso**.
11. Quando si torna al pannello **Utenti** , l'utente risulta aggiunto.  

## <a name="add-an-external-user-to-a-lab-using-powershell"></a>Aggiungere un utente esterno a un lab usando PowerShell
Oltre ad aggiungere gli utenti nel portale di Azure, è possibile aggiungere un utente esterno al lab usando uno script di PowerShell. Nell'esempio seguente, è sufficiente modificare i valori dei parametri nel commento **Values to change** (Valori da modificare).
È possibile recuperare i valori `subscriptionId`, `labResourceGroup` e `labName` dal pannello Lab nel portale di Azure.

> [!NOTE]
> Lo script di esempio presume che l'utente specificato sia stato aggiunto come guest ad Active Directory. In caso contrario, avrà esito negativo. Per aggiungere a un lab un utente non presente in Active Directory, usare il portale di Azure per assegnare l'utente a un ruolo come illustrato nella sezione [Aggiungere un utente o un proprietario a livello di lab](#add-an-owner-or-user-at-the-lab-level).   
> 
> 

    # Add an external user in DevTest Labs user role to a lab
    # Ensure that guest users can be added to the Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values to change
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select the Azure subscription that contains the lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve the user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create the role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-the-subscription-level"></a>Aggiungere un utente o un proprietario a livello di sottoscrizione
Le autorizzazioni di Azure vengono propagate dall'ambito padre all'ambito figlio in Azure. Quindi i proprietari di una sottoscrizione di Azure contenente lab sono automaticamente proprietari di tali lab. Sono proprietari anche delle VM e delle altre risorse create dagli utenti del lab e dal servizio Azure DevTest Labs. 

È possibile aggiungere altri proprietari a un lab tramite il pannello del lab nel [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). L'ambito di amministrazione del proprietario aggiunto è tuttavia più limitato dell'ambito del proprietario della sottoscrizione. I proprietari aggiunti, ad esempio, non hanno accesso completo ad alcune delle risorse create nella sottoscrizione dal servizio DevTest Labs. 

Per aggiungere un proprietario a una sottoscrizione di Azure, seguire questi passaggi:

1. Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selezionare **Altri servizi** e quindi **Sottoscrizioni** dall'elenco.
3. Selezionare la sottoscrizione da usare.
4. Selezionare l'icona **Accesso** . 
   
    ![Utenti di accesso](./media/devtest-lab-add-devtest-user/access-users.png)
5. Nel pannello **Utenti** selezionare **Aggiungi**.
   
    ![Add user](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. Nel pannello **Selezionare un ruolo** selezionare **Proprietario**.
7. Nel pannello **Aggiungi utenti** immettere l'indirizzo di posta elettronica o il nome dell'utente che si vuole aggiungere come proprietario. Se l'utente non viene trovato, si riceve un messaggio di errore che spiega il problema. Se l'utente viene trovato, tale utente viene elencato sotto la casella di testo **Utente** .
8. Selezionare il nome utente individuato.
9. Scegliere **Seleziona**.
10. Selezionare **OK** per chiudere il pannello **Aggiungi accesso**.
11. Quando si torna al pannello **Utenti** , l'utente risulta aggiunto come proprietario. Questo utente è ora un proprietario di qualsiasi lab creato in questa sottoscrizione e quindi può eseguire le attività del proprietario. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

