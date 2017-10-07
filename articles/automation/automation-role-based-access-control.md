---
title: controllo di accesso basato su aaaRole in automazione di Azure | Documenti Microsoft
description: Il controllo degli accessi in base al ruolo consente di gestire gli accessi per le risorse di Azure. Questo articolo viene descritto come tooset backup RBAC in automazione di Azure.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: controllo degli accessi in base al ruolo di Automazione, controllo degli accessi in base al ruolo, controllo degli accessi in base al ruolo di Azure
ms.assetid: 04b5625e-0ee8-4b5b-85cd-7734c1b3d4a3
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 051438e44d0c5c514d6dbaac5a312344ee311cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-in-azure-automation"></a>Controllo degli accessi in base al ruolo in Automazione di Azure
## <a name="role-based-access-control"></a>Controllo degli accessi in base al ruolo
Il controllo degli accessi in base al ruolo consente di gestire gli accessi per le risorse di Azure. Utilizzando [RBAC](../active-directory/role-based-access-control-configure.md), è possibile isolare il compiti all'interno del team e concedere solo hello quantità di accesso toousers, gruppi e le applicazioni che devono tooperform i processi. È possibile concedere accesso basato sui ruoli toousers utilizzando hello portale di Azure, gli strumenti da riga di comando di Azure o le API di gestione di Azure.

## <a name="rbac-in-automation-accounts"></a>Controllo degli accessi in base al ruolo negli account di automazione
In automazione di Azure, l'accesso viene concesso tramite l'assegnazione di hello appropriato RBAC ruolo toousers, gruppi e le applicazioni di hello ambito di account di automazione. Seguenti sono hello ruoli predefiniti supportati da un account di automazione:  

| **Ruolo** | **Descrizione** |
|:--- |:--- |
| Proprietario |ruolo proprietario Hello consente di accedere alle risorse di tooall e le azioni all'interno di un account di automazione, fornendo accesso tooother utenti, gruppi e applicazioni toomanage hello account di automazione. |
| Collaboratore |ruolo di collaboratore Hello consente toomanage tutto tranne la modifica di altro utente account di automazione tooan le autorizzazioni di accesso. |
| Reader |ruolo di lettore Hello consente tooview tutte le risorse di hello in automazione di un account ma non possono apportare alcuna modifica. |
| Operatore di automazione |ruolo di operatore di automazione Hello consente attività operative tooperform ad esempio avvio, arrestare, sospendere, riprendere e pianificare i processi. Questo ruolo è utile se si desidera tooprotect le risorse di Account di automazione come asset di credenziali e i runbook vengano visualizzati o modificati, ma consente ancora i membri di tooexecute l'organizzazione questi runbook. |
| Amministratore accessi utente |ruolo di amministratore di accesso utente Hello consente toomanage account accesso tooAzure automazione. |

> [!NOTE]
> È possibile concedere accesso diritti tooa specifico del runbook o runbook, solo le risorse di toohello e le azioni all'interno di hello account di automazione.  
> 
> 

In questo articolo si assiste come tooset backup RBAC in automazione di Azure. Innanzitutto, si accettano ingrandire esaminare hello singole autorizzazioni concesse toohello collaboratore, lettore, l'operatore di automazione e amministratore di accesso utente in modo che si ottengono una buona conoscenza prima di concedere a tutti gli utenti i diritti toohello account di automazione.  In caso contrario potrebbero verificarsi conseguenze impreviste o indesiderate.     

## <a name="contributor-role-permissions"></a>Autorizzazioni del ruolo Collaboratore
Hello nella tabella seguente presenta azioni specifiche hello che possono essere eseguite dal ruolo di collaboratore hello in automazione.

| **Tipo di risorsa** | **Lettura** | **Scrittura** | **Eliminazione** | **Altre azioni** |
|:--- |:--- |:--- |:--- |:--- |
| Account di automazione di Azure |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Asset di certificato di Automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Asset di connessione di Automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Asset del tipo di connessione di Automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Asset credenziali di Automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Asset di pianificazione di Automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Asset di tipo variabile di Automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Configurazione dello stato desiderato di Automazione | | | |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |
| Tipo di risorsa del ruolo di lavoro ibrido per runbook |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Processo di automazione di Azure |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |
| Flusso del processo di automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Pianificazione del processo di automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Modulo di automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Runbook di Automazione di Azure |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |
| Bozza di runbook di Automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |
| Processo di test della bozza di runbook di Automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |
| Webhook di automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |

## <a name="reader-role-permissions"></a>Autorizzazioni del ruolo Lettore
Hello nella tabella seguente presenta azioni specifiche hello che possono essere eseguite dal ruolo di lettore hello in automazione.

| **Tipo di risorsa** | **Lettura** | **Scrittura** | **Eliminazione** | **Altre azioni** |
|:--- |:--- |:--- |:--- |:--- |
| Amministratore sottoscrizione classico |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Blocco di gestione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Autorizzazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Operazioni del provider |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Assegnazione di ruolo |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Definizione di ruolo |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="automation-operator-role-permissions"></a>Autorizzazioni del ruolo Automation Operator
Hello nella tabella seguente presenta hello le azioni che possono essere eseguite dal ruolo operatore automazione hello in automazione.

| **Tipo di risorsa** | **Lettura** | **Scrittura** | **Eliminazione** | **Altre azioni** |
|:--- |:--- |:--- |:--- |:--- |
| Account di automazione di Azure |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Asset di certificato di Automazione | | | | |
| Asset di connessione di Automazione | | | | |
| Asset del tipo di connessione di Automazione | | | | |
| Asset credenziali di Automazione | | | | |
| Asset di pianificazione di Automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | |
| Asset di tipo variabile di Automazione | | | | |
| Configurazione dello stato desiderato di Automazione | | | | |
| Tipo di risorsa del ruolo di lavoro ibrido per runbook | | | | |
| Processo di automazione di Azure |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |
| Flusso del processo di automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Pianificazione del processo di automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | |
| Modulo di automazione | | | | |
| Runbook di Automazione di Azure |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Bozza di runbook di Automazione | | | | |
| Processo di test della bozza di runbook di Automazione | | | | |
| Webhook di automazione | | | | |

Per ulteriori dettagli, hello [azioni operatore automazione](../active-directory/role-based-access-built-in-roles.md#automation-operator) elenchi hello azioni supportate dal ruolo di operatore di automazione di hello in account di automazione hello e le relative risorse.

## <a name="user-access-administrator-role-permissions"></a>Autorizzazioni del ruolo Amministratore Accesso utenti
Hello nella tabella seguente presenta hello le azioni che possono essere eseguite dal ruolo di amministratore di accesso utente hello in automazione.

| **Tipo di risorsa** | **Lettura** | **Scrittura** | **Eliminazione** | **Altre azioni** |
|:--- |:--- |:--- |:--- |:--- |
| Account di automazione di Azure |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Asset di certificato di Automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Asset di connessione di Automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Asset del tipo di connessione di Automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Asset credenziali di Automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Asset di pianificazione di Automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Asset di tipo variabile di Automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Configurazione dello stato desiderato di Automazione | | | | |
| Tipo di risorsa del ruolo di lavoro ibrido per runbook |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Processo di automazione di Azure |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Flusso del processo di automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Pianificazione del processo di automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Modulo di automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Runbook di Automazione di Azure |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Bozza di runbook di Automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Processo di test della bozza di runbook di Automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Webhook di automazione |![Stato verde](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="configure-rbac-for-your-automation-account-using-azure-portal"></a>Configurare il controllo degli accessi in base al ruolo per l'account di automazione tramite il portale di Azure
1. Accedi toohello [portale Azure](https://portal.azure.com/) e aprire l'account di automazione dal Pannello di hello gli account di automazione.  
2. Fare clic su hello **accesso** controllo hello angolo superiore destro. Verrà visualizzata hello **utenti** pannello in cui è possibile aggiungere nuovi utenti, gruppi e applicazioni di toomanage l'account di automazione e visualizza i ruoli esistenti che possono essere configurati per hello Account di automazione.  
   
   ![Pulsante Accesso](media/automation-role-based-access-control/automation-01-access-button.png)  

> [!NOTE]
> **Gli amministratori delle sottoscrizioni** esiste già come utente predefinito hello. gruppo di active directory Hello sottoscrizione admins include amministratori di servizio hello e co-administrator(s) per la sottoscrizione di Azure. Servizio salve è proprietario di hello della sottoscrizione di Azure e le relative risorse e verrà hanno il ruolo di proprietario hello ereditato per gli account di automazione hello troppo. Ciò significa che l'accesso hello è **Inherited** per **gli amministratori e ai coamministratori del servizio** di una sottoscrizione e le relative **assegnato** per tutti gli altri utenti di hello. Fare clic su **gli amministratori delle sottoscrizioni** tooview ulteriori dettagli sulle relative autorizzazioni.  
> 
> 

### <a name="add-a-new-user-and-assign-a-role"></a>Aggiungere un nuovo utente e assegnare un ruolo
1. Dal pannello utenti hello, fare clic su **Aggiungi** tooopen hello **Pannello di accesso Add** in cui è possibile aggiungere un utente, gruppo o l'applicazione e assegnare un ruolo toothem.  
   
   ![Add user](media/automation-role-based-access-control/automation-02-add-user.png)  
2. Selezionare un ruolo dall'elenco di hello dei ruoli disponibili. Si sceglierà hello **lettore** ruolo, ma è possibile scegliere qualsiasi hello disponibili ruoli predefiniti che supporta un Account di automazione o qualsiasi ruolo personalizzata definita.  
   
   ![Selezionare il ruolo](media/automation-role-based-access-control/automation-03-select-role.png)  
3. Fare clic su **aggiungere utenti** tooopen hello **aggiungere utenti** blade. Se è stato aggiunto alcun toomanage utenti, gruppi o le applicazioni sono elencati la sottoscrizione, quindi gli utenti ed è possibile selezionarle tooadd accesso. Se non vi sono elencati tutti gli utenti o se non è elencato utente hello desiderato per l'aggiunta di fare clic su **invitare** tooopen hello **guest di invitare** pannello, in cui è possibile invitare un utente con un account Microsoft valido indirizzo di posta elettronica, ad esempio Outlook.com, OneDrive o Xbox Live ID. Dopo aver immesso l'indirizzo di posta elettronica hello dell'utente hello, fare clic su **selezionare** tooadd hello utente e quindi fare clic su **OK**. 
   
   ![Aggiungi utenti](media/automation-role-based-access-control/automation-04-add-users.png)  
   
   Ora dovrebbe essere utente hello aggiunto toohello **utenti** pannello con hello **lettore** ruolo assegnato.  
   
   ![Elencare gli utenti](media/automation-role-based-access-control/automation-05-list-users.png)  
   
   È inoltre possibile assegnare un utente toohello ruolo hello **ruoli** blade. 
4. Fare clic su **ruoli** da hello tooopen pannello agli utenti di hello **pannello ruoli**. Questo pannello, è possibile visualizzare il nome di hello del ruolo di hello, hello numerosi utenti e gruppi assegnati toothat ruolo.
   
    ![Assegnare un ruolo dal pannello Utenti](media/automation-role-based-access-control/automation-06-assign-role-from-users-blade.png)  
   
   > [!NOTE]
   > Controllo di accesso basato sui ruoli può essere impostato solo a livello di Account di automazione hello e non a qualsiasi risorsa seguente hello Account di automazione.
   > 
   > 
   
    È possibile assegnare più di un utente tooa ruolo, gruppo o applicazione. Ad esempio, se si aggiunta hello **automazione operatore** ruolo insieme hello **ruolo lettura** toohello utente, quindi è possibile visualizzare tutte le risorse di automazione di hello, nonché eseguire i processi del runbook hello. È possibile espandere l'elenco a discesa di hello tooview un elenco di ruoli assegnati toohello utente.  
   
    ![Visualizzare più ruoli](media/automation-role-based-access-control/automation-07-view-multiple-roles.png)  

### <a name="remove-a-user"></a>Rimuovere un utente
È possibile rimuovere l'autorizzazione di accesso per un utente che non gestisce hello Account di automazione o che non lavorano per organizzazione hello hello. Seguenti sono hello tooremove passaggi di un utente: 

1. Da hello **utenti** blade, assegnazione di ruolo selezionare hello che si desidera tooremove.
2. Fare clic su hello **rimuovere** pulsante nel Pannello di Dettagli assegnazione hello.
3. Fare clic su **Sì** tooconfirm rimozione. 
   
   ![Rimuovere utenti](media/automation-role-based-access-control/automation-08-remove-users.png)  

## <a name="role-assigned-user"></a>Utente assegnato a un ruolo
Quando si connette un ruolo di utente assegnato tooa tootheir account di automazione, verranno visualizzate nell'elenco di hello dell'account del proprietario di hello **directory predefinito**. Directory predefinita del proprietario di hello predefinito directory toohello devono passare in hello tooview ordine account di automazione che sono stati aggiunti.  

![Directory predefinita](media/automation-role-based-access-control/automation-09-default-directory-in-role-assigned-user.png)  

### <a name="user-experience-for-automation-operator-role"></a>Esperienza utente per il ruolo Automation Operator
Quando un utente, che è assegnato a viste ruolo di operatore automazione toohello siano assegnati all'account di automazione di hello, possono solo visualizzare l'elenco hello dei runbook, pianificazioni e i processi del runbook creata in hello account di automazione, ma non è possibile visualizzare le relative definizioni. È possibile avviare, arrestare, sospendere, riprendere o pianificare il processo di runbook hello. utente Hello non sarà necessario accedere alle risorse di automazione tooother, ad esempio le configurazioni, i gruppi di lavoro ibrido o i nodi DSC.  

![Nessun tooresourcres di accesso](media/automation-role-based-access-control/automation-10-no-access-to-resources.png)  

Quando l'utente di hello fa clic su runbook hello, hello comandi tooview hello origine o di modificare runbook hello non vengono forniti come ruolo di operatore automazione hello non consente l'accesso toothem.  

![Nessun runbook tooedit accesso](media/automation-role-based-access-control/automation-11-no-access-to-edit-runbook.png)  

utente Hello avrà accesso tooview e toocreate pianificazioni ma non avrà accesso tooany altri tipo di risorsa.  

![Nessun tooassets di accesso](media/automation-role-based-access-control/automation-12-no-access-to-assets.png)  

Questo utente non ha anche accesso tooview hello webhook associato a un runbook

![Nessun toowebhooks di accesso](media/automation-role-based-access-control/automation-13-no-access-to-webhooks.png)  

## <a name="configure-rbac-for-your-automation-account-using-azure-powershell"></a>Configurare il controllo degli accessi in base al ruolo per l'account di automazione tramite Azure PowerShell
Accesso basato sui ruoli può anche essere configurato tooan Account di automazione con hello seguenti [cmdlet di Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md).

• [Get-AzureRmRoleDefinition](https://msdn.microsoft.com/library/mt603792.aspx) elenca tutti i ruoli del controllo degli accessi in base al ruolo disponibili in Azure Active Directory. È possibile utilizzare questo comando insieme hello **nome** toolist proprietà tutti hello azioni che possono essere eseguite da un ruolo specifico.  
    **Esempio:**  
    ![Ottenere la definizione del ruolo](media/automation-role-based-access-control/automation-14-get-azurerm-role-definition.png)  

• [Get AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt619413.aspx) specificare un elenco di assegnazioni di ruolo di Azure AD RBAC in hello ambito. Senza parametri, questo comando restituisce tutte le assegnazioni di ruolo hello apportate nella sottoscrizione hello. Hello utilizzare **ExpandPrincipalGroups** assegnazioni di parametro toolist access per hello specificato utente così come gruppi hello hello utente è membro.  
    **Esempio:** toolist comando che segue di hello di utilizzare tutti gli utenti di hello e i relativi ruoli all'interno di un account di automazione.

    Get-AzureRMRoleAssignment -scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>” 

![Ottenere l'assegnazione del ruolo](media/automation-role-based-access-control/automation-15-get-azurerm-role-assignment.png)

• [New AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603580.aspx) tooassign toousers, gruppi e applicazioni tooa particolare ambito di accesso.  
    **Esempio:** ruolo di "Operatore automazione" hello tooassign per un utente nell'ambito dell'Account di automazione hello comando che segue di hello utilizzare.

    New-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish toogrant access> -RoleDefinitionName "Automation operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”  

![Nuova assegnazione del ruolo](media/automation-role-based-access-control/automation-16-new-azurerm-role-assignment.png)

• Utilizzare [Remove AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603781.aspx) tooremove accesso di un'applicazione da un ambito specifico, gruppo o utente specificato.  
    **Esempio:** comando che segue di hello utilizzare utente hello tooremove dal ruolo "Operatore automazione" hello in hello ambito dell'Account di automazione.

    Remove-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish tooremove> -RoleDefinitionName "Automation Operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”

In hello esempi sopra riportati, sostituire **Accedi Id**, **Id sottoscrizione**, **nome gruppo di risorse** e **nome account di automazione** con il dettagli dell'account. Scegliere **Sì** quando viene richiesto di tooconfirm prima di continuare tooremove assegnazione di ruolo utente.   

## <a name="next-steps"></a>Passaggi successivi
* Per informazioni sui diversi modi tooconfigure RBAC per l'automazione di Azure, vedere troppo[gestione accessi con Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md).
* Per informazioni su modi toostart un runbook, vedere [avvio di un runbook](automation-starting-a-runbook.md)
* Per informazioni sui tipi di runbook diverso, fare riferimento troppo[tipi di runbook di automazione di Azure](automation-runbook-types.md)

