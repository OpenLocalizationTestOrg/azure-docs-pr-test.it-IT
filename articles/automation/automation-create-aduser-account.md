---
title: Account utente di Active Directory di Azure aaaCreate | Documenti Microsoft
description: In questo articolo viene descritto come credenziali di toocreate un account utente di Azure Active Directory per i runbook in automazione di Azure tooauthenticate in Azure e Azure classico.
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: utente di Azure Active Directory, Azure Service Management, account utente Azure AD
ms.assetid: fcfe266d-b22e-4dfb-8272-adcab09fc0cf
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 7c6ed4182dbab074d0bc5da7057f74ad321d8884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-azure-classic-deployment-and-resource-manager"></a>Autenticare i runbook con la distribuzione classica di Azure e Resource Manager
Questo articolo descrive i passaggi di hello che è necessario eseguire tooconfigure un account utente di Azure Active Directory per i runbook di automazione di Azure in esecuzione in base al modello di distribuzione classico di Azure o le risorse di gestione risorse di Azure.  Durante il processo continua toobe un'identità di autenticazione supportati per la gestione risorse di Azure basato su runbook, hello consigliabile metodo viene utilizzato un account RunAs di Azure.       

## <a name="create-a-new-azure-active-directory-user"></a>Creare un nuovo utente di Azure Active Directory
1. Accedere come amministratore del servizio per la sottoscrizione di Azure da toomanage hello toohello portale di Azure classico.
2. Selezionare **Active Directory**, quindi selezionare il nome di hello della directory dell'organizzazione.
3. Seleziona hello **utenti** scheda e quindi, nell'area di comando hello, selezionare **Aggiungi utente**.
4. In hello **informazioni sull'utente** pagina **tipo di utente**selezionare **nuovo utente nell'organizzazione**.
5. Immettere un nome utente.  
6. Selezionare nome di directory hello è associato alla sottoscrizione Azure nella pagina di hello Active Directory.
7. In hello **profilo utente** pagina, fornire un primo e ultimo nome, un nome descrittivo e utente da hello **ruoli** elenco.  Non selezionare **Abilita Multi-Factor Authentication**.
8. Si noti il nome completo dell'utente hello e la password temporanea.
9. Selezionare **Impostazioni -> Amministratori > Aggiungi**.
10. Digitare il nome utente completo hello dell'utente hello creato.
11. Selezionare hello sottoscrizione che si desidera hello toomanage utente.
12. Disconnettersi da Azure e ripetere l'accesso con account hello che appena creato. Sarà richiesto toochange hello password utente.

## <a name="create-an-automation-account-in-azure-classic-portal"></a>Creare un account di Automazione nel portale di Azure classico
In questa sezione per eseguire hello seguenti passaggi toocreate un account di automazione di Azure nel portale di Azure per l'utilizzo di hello. i runbook di gestione delle risorse Azure distribuzione classica.  

> [!NOTE]
> Account di automazione creati con il portale di Azure classico hello possono essere gestiti sia hello Azure classico e portale di Azure e una serie di cmdlet. Una volta creato l'account di hello, influisce in alcun modo come creare e gestire le risorse nell'account hello. Se si intende toocontinue toouse hello Azure portale classico, si consiglia di utilizzare in sostituzione di hello toocreate portale Azure qualsiasi account di automazione.
> 
> 

1. Accedere come amministratore del servizio per la sottoscrizione di Azure da toomanage hello toohello portale di Azure classico.
2. Selezionare **Automazione**.
3. In hello **automazione** selezionare **creare un Account di automazione**.
4. In hello **creare un Account di automazione** digitare un nome per il nuovo account di automazione, selezionare un **area** dall'elenco a discesa hello.  
5. Fare clic su **OK** tooaccept le impostazioni e creare account hello.
6. Dopo averlo creato verrà elencato in hello **automazione** pagina.
7. Fare clic su account hello e apporterà si toohello pagina Dashboard.  
8. Nella pagina Dashboard di automazione hello selezionare **asset**.
9. In hello **asset** selezionare **Aggiungi impostazioni** si trova nella parte inferiore di hello della pagina hello.
10. In hello **Aggiungi impostazioni** selezionare **Add Credential**.
11. In hello **definire credenziali** selezionare **credenziali di Windows PowerShell** da hello **tipo di credenziale** elenco a discesa elenco e specificare un nome per la credenziale hello.
12. In seguito hello **definire credenziali** pagina digitare nome utente hello dell'account utente di hello Active Directory creato in precedenza in hello **nome utente** password campo e hello in hello **Password**e **Conferma Password** campi. Fare clic su **OK** toosave le modifiche.

## <a name="create-an-automation-account-in-hello-azure-portal"></a>Creare un account di automazione in hello portale di Azure
In questa sezione, eseguire hello seguenti passaggi toocreate un account di automazione di Azure nel portale di Azure per l'utilizzo di hello. i runbook la gestione delle risorse in modalità Azure Resource Manager.  

1. Accedi toohello portale di Azure come amministratore del servizio per la sottoscrizione di Azure da toomanage hello.
2. Selezionare **Account di automazione**.
3. Nel Pannello di account di automazione hello, fare clic su **Aggiungi**.<br><br>![Aggiungi account di Automazione](media/automation-create-aduser-account/add-automation-acct-properties.png)
4. In hello **aggiungere Account di automazione** pannello in hello **nome** casella digitare un nome per il nuovo account di automazione.
5. Se si dispone di più di una sottoscrizione, specificare hello per il nuovo account di hello, nonché un nuovo o esistente **gruppo di risorse** e un Data Center Azure **percorso**.
6. Selezionare il valore di hello **Sì** per hello **creare account RunAs** opzione e fare clic su hello **crea** pulsante.  
   
    > [!NOTE]
    > Se si sceglie toonot creare account RunAs hello selezionando l'opzione hello **n**, verrà visualizzato un messaggio di avviso in hello **aggiungere Account di automazione** blade.  Mentre l'account di hello viene creato e assegnato toohello **collaboratore** ruolo nella sottoscrizione di hello, non disporrà di un'identità di autenticazione corrispondente all'interno del servizio directory di sottoscrizioni e di conseguenza, nessun accesso risorse nella sottoscrizione.  Questo impedirà tutti i runbook che fanno riferimento a questo account saranno in grado di tooauthenticate e operazioni sulle risorse di gestione risorse di Azure.
    > 
    >

    <br>![Aggiungi account di Automazione, avviso](media/automation-create-aduser-account/add-automation-acct-properties-error.png)<br>  
7. Mentre Azure crea account di automazione hello, è possibile monitorare lo stato di avanzamento hello in **notifiche** dal menu di hello.

Quando viene completata la creazione di hello delle credenziali hello, è necessario toocreate hello di tooassociate un Asset delle credenziali Account di automazione con hello account utente di Active Directory creato in precedenza.  Tenere presente, viene creato solo account di automazione hello e non è associata a un'identità di autenticazione.  Effettuare i passaggi di hello descritti in hello [credenziali asset nell'articolo di automazione di Azure](automation-credentials.md#creating-a-new-credential-asset) e immettere il valore hello **username** in formato hello **dominio\utente**.

## <a name="use-hello-credential-in-a-runbook"></a>Utilizzare credenziali hello in un runbook
È possibile recuperare hello credenziali in un runbook con hello [Get-AutomationPSCredential](http://msdn.microsoft.com/library/dn940015.aspx) attività e quindi utilizzarlo con [Add-AzureAccount](http://msdn.microsoft.com/library/azure/dn722528.aspx) tooconnect tooyour sottoscrizione di Azure. Se credenziali hello sono un amministratore di più sottoscrizioni di Azure, quindi è consigliabile usare anche [Select-AzureSubscription](http://msdn.microsoft.com/library/dn495203.aspx) toospecify hello corretto. Come illustrato nell'esempio hello Windows PowerShell riportato di seguito in genere visualizzato nella parte superiore di hello della maggior parte dei runbook di automazione di Azure.

    $cred = Get-AutomationPSCredential –Name "myuseraccount.onmicrosoft.com"
    Add-AzureAccount –Credential $cred
    Select-AzureSubscription –SubscriptionName "My Subscription"

È necessario ripetere queste righe dopo ogni [checkpoints](http://technet.microsoft.com/library/dn469257.aspx#bk_Checkpoints) del Runbook. Se hello runbook viene sospeso e quindi ripreso da un altro lavoro, sarà necessario tooperform nuovamente l'autenticazione hello.

## <a name="next-steps"></a>Passaggi successivi
* Revisione hello runbook diversi tipi e i passaggi per la creazione di runbook da hello articolo seguente [tipi di runbook di automazione di Azure](automation-runbook-types.md)

