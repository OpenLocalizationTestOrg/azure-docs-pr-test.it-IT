---
title: Account di automazione di Azure (autonomo) aaaCreate | Documenti Microsoft
description: "Esercitazione che illustra utilizzare hello di esempio, test e la creazione di autenticazione dell'entità di sicurezza in automazione di Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 1500d25d9565d4082768933834303a17c5e84234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-azure-automation-account"></a>Creare un account di Automazione di Azure autonomo
Questo argomento viene illustrato come toocreate un account di automazione dal portale di Azure, se si desidera tooevaluate e informazioni su automazione di Azure senza includere soluzioni di gestione aggiuntivo hello o l'integrazione con OMS Log Analitica tooprovide hello monitoraggio avanzate di processi del runbook.  È possibile aggiungere tali soluzioni di gestione o integrare con Analitica di Log in qualsiasi punto hello future.  Con account di automazione hello, si runbook tooauthenticate in grado di gestire le risorse in Gestione risorse di Azure o Azure distribuzione classica.

Quando si crea un account di automazione in hello portale di Azure, viene creato automaticamente:

* Account RunAs, che consente di creare una nuova entità servizio in Azure Active Directory, un certificato, e assegna hello controllo degli accessi in base al ruolo Collaboratore (RBAC), che è utilizzato le risorse di gestione risorse toomanage utilizzo dei runbook.   
* Account RunAs classico caricando un certificato di gestione, viene utilizzato toomanage risorse classiche utilizzo dei runbook.  

Questo semplifica il processo di hello automaticamente e consente di avviare rapidamente la compilazione e distribuzione di runbook toosupport deve l'automazione.  

## <a name="permissions-required-toocreate-automation-account"></a>Account di automazione toocreate necessario disporre di autorizzazioni
toocreate o aggiornamento di un account di automazione, è necessario disporre hello seguenti privilegi specifici e le autorizzazioni necessarie toocomplete in questo argomento.   
 
* In ordine toocreate un account di automazione, l'account utente di Active Directory deve toobe tooa aggiunto ruolo con ruolo di proprietario toohello equivalenti autorizzazioni per le risorse di Microsoft come descritto nell'articolo [controllo di accesso basato sui ruoli in automazione di Azure ](automation-role-based-access-control.md).  
* Se le registrazioni di App hello impostazione è troppo**Sì**, gli utenti senza privilegi di amministratore nel tenant di Azure AD possono [registrare AD applicazioni](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions).  Se le registrazioni di app hello impostazione è troppo**n**, utente hello eseguendo questa azione deve essere un amministratore globale di Azure AD. 

Se non si un membro di istanza di Active Directory della sottoscrizione hello prima dell'aggiunta di toohello amministratore/coamministratore ruolo globale della sottoscrizione di hello, tooActive Directory aggiunti come guest. In questo caso, viene visualizzato un "non si dispone delle autorizzazioni toocreate..." visualizzazione dell'avviso hello **aggiungere Account di automazione** blade. Gli utenti che sono stati aggiunti toohello amministratore/coamministratore ruolo globale prima può essere rimosso dall'istanza di Active Directory della sottoscrizione hello e riaggiunto toomake loro un utente in Active Directory completa. tooverify tale situazione, hello **Azure Active Directory** riquadro nel portale di Azure selezionare hello **utenti e gruppi**selezionare **tutti gli utenti** e, dopo aver selezionato hello un utente specifico, seleziona **profilo**. valore di hello Hello **tipo utente** attributo del profilo utenti hello non deve essere uguale **Guest**.

## <a name="create-a-new-automation-account-from-hello-azure-portal"></a>Creare un nuovo Account di automazione da hello portale di Azure
In questa sezione, eseguire hello seguendo i passaggi toocreate un account di automazione di Azure nel portale di Azure hello.    

1. Accedi toohello portale di Azure con un account che sia un membro del ruolo di amministratori della sottoscrizione hello e al coamministratore della sottoscrizione hello.
2. Fare clic su **New**.<br><br> ![Selezionare l'opzione Nuovo nel portale di Azure](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  
3. Cercare **automazione** e quindi in hello risultati della ricerca selezionare **di automazione e controllo***.<br><br> ![Cercare e selezionare Automazione nel Marketplace](media/automation-create-standalone-account/automation-marketplace-select-create-automationacct.png)<br> 
3. Nel Pannello di account di automazione hello, fare clic su **Aggiungi**.<br><br>![Aggiungi account di Automazione](media/automation-create-standalone-account/automation-create-automationacct-properties.png)
   
   > [!NOTE]
   > Se viene visualizzato hello seguente avviso nella hello **aggiungere Account di automazione** pannello, è perché l'account non è un membro del ruolo di amministratori della sottoscrizione hello e co-amministratore della sottoscrizione hello.<br><br>![Aggiungi account di Automazione, avviso](media/automation-create-standalone-account/create-account-without-perms.png)
   > 
   > 
4. In hello **aggiungere Account di automazione** pannello in hello **nome** casella digitare un nome per il nuovo account di automazione.
5. Se si dispone di più di una sottoscrizione, specificarne uno per account hello nuovo o esistente **gruppo di risorse** e un Data Center Azure **percorso**.
6. Verificare il valore di hello **Sì** è selezionato per hello **creare account RunAs** opzione e fare clic su hello **crea** pulsante.  
   
   > [!NOTE]
   > Se si sceglie toonot creare account RunAs hello selezionando l'opzione hello **n**, viene visualizzata con un messaggio di avviso in hello **aggiungere Account di automazione** blade.  Mentre hello account viene creato nel portale di Azure hello, non ha un'identità di autenticazione corrispondente all'interno del classica o servizio directory di gestione risorse di sottoscrizione e di conseguenza, non tooresources di accesso nella sottoscrizione.  Ciò impedisce qualsiasi runbook che fanno riferimento a questo account saranno in grado di tooauthenticate e operazioni sulle risorse di tali modelli di distribuzione.
   > 
   > ![Aggiungi account di Automazione, avviso](media/automation-create-standalone-account/create-account-decline-create-runas-msg.png)<br>
   > Quando un'entità servizio hello non viene creata un ruolo Collaboratore hello non è assegnato.
   > 

7. Mentre Azure crea account di automazione hello, è possibile monitorare lo stato di avanzamento hello in **notifiche** dal menu di hello.

### <a name="resources-included"></a>Risorse incluse
Quando viene creato correttamente hello account di automazione, varie risorse vengono create automaticamente per l'utente.  Hello nella tabella seguente sono riepilogate le risorse per hello account RunAs.<br>

| Risorsa | Descrizione |
| --- | --- |
| Runbook AzureAutomationTutorial |Un runbook grafico di esempio che illustra come tooauthenticate utilizzando hello account RunAs e recupera tutte le risorse di gestione risorse di hello. |
| Runbook AzureAutomationTutorialScript |Un runbook di PowerShell di esempio che illustra come tooauthenticate utilizzando hello account RunAs e recupera tutte le risorse di gestione risorse di hello. |
| AzureRunAsCertificate |Asset del certificato creato durante la creazione di account di automazione automaticamente o tramite script di PowerShell hello di sotto di un account esistente.  Consente di tooauthenticate con Azure in modo che è possibile gestire le risorse di Azure Resource Manager dai runbook.  La durata di questo certificato è di un anno. |
| AzureRunAsConnection |Asset della connessione creato durante la creazione di account di automazione automaticamente o tramite script di PowerShell hello di sotto di un account esistente. |

Hello nella tabella seguente sono riepilogate le risorse per hello Classic account RunAs.<br>

| Risorsa | Descrizione |
| --- | --- |
| Runbook AzureClassicAutomationTutorial |Grafica runbook di esempio, che ottiene tutte le macchine virtuali classiche hello in una sottoscrizione utilizzando hello Classic Account runas (certificato) e quindi restituisce lo stato e nome della macchina virtuale hello. |
| Runbook di script AzureClassicAutomationTutorial |Un runbook di PowerShell riportato, che ottiene tutte le macchine virtuali classiche hello in una sottoscrizione utilizzando hello Classic Account runas (certificato) e quindi restituisce lo stato e nome della macchina virtuale hello. |
| AzureClassicRunAsCertificate |Asset del certificato creato automaticamente che è utilizzato tooauthenticate con Azure in modo che è possibile gestire le risorse di Azure classiche dai runbook.  La durata di questo certificato è di un anno. |
| AzureClassicRunAsConnection |Asset della connessione automaticamente creata utilizzato tooauthenticate con Azure in modo che è possibile gestire le risorse di Azure classiche dai runbook. |


## <a name="next-steps"></a>Passaggi successivi
* toolearn ulteriori informazioni sui grafici per la modifica, vedere [grafici per la modifica in automazione di Azure](automation-graphical-authoring-intro.md).
* tooget avviato con runbook PowerShell, vedere [il primo runbook PowerShell](automation-first-runbook-textual-powershell.md).
* tooget avviato con runbook del flusso di lavoro di PowerShell, vedere [il primo runbook del flusso di lavoro PowerShell](automation-first-runbook-textual.md).
