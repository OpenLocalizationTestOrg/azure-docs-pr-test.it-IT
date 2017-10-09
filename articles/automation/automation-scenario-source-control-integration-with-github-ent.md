---
title: Integrazione del controllo codice sorgente automazione con GitHub Enterprise aaaAzure | Documenti Microsoft
description: Vengono illustrati i dettagli di hello come integrazione tooconfigure con GitHub Enterprise per controllo del codice sorgente dei runbook di automazione.
services: automation
documentationCenter: 
authors: mgoedtel
manager: jwhit
editor: 
ms.assetid: e01d817c-7d38-421c-adf5-647a4b526eb4
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: magoedte
ms.openlocfilehash: 915d36ccabb72fdee1dba663049a0b331249cd73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-github-enterprise"></a>Scenario di Automazione di Azure - Integrazione del controllo del codice sorgente di Automazione con GitHub Enterprise

Automazione supporta attualmente l'integrazione del controllo codice sorgente, che consente i runbook tooassociate nel repository del controllo codice sorgente GitHub di automazione account tooa.  Tuttavia, i clienti che hanno distribuito [GitHub Enterprise](https://enterprise.github.com/home) toosupport loro DevOps consigliate, anche il toouse è toomanage hello del ciclo di vita di runbook che sono sviluppate tooautomate processi di business e gestione dei servizi operazioni.  

In questo scenario, è necessario un computer Windows nel proprio data center configurato come un Runbook Worker ibrido con moduli di gestione risorse di Azure hello e installati gli strumenti Git.  computer di lavoro ibridi Hello dispone di un clone del repository Git locale hello.  Quando runbook hello viene eseguito nel ruolo di lavoro ibrido hello, sincronizzazione directory Git hello e contenuto del file hello runbook viene importati in hello account di automazione.

Questo articolo viene descritto come tooset la configurazione dell'ambiente di automazione di Azure. Iniziando dalla configurazione dell'automazione con le credenziali di sicurezza hello runbook necessari toosupport questo scenario e la distribuzione di un Runbook Worker ibrido nei dati runbook hello toorun al centro e accedere la toosynchronize repository GitHub Enterprise runbook con l'account di automazione.  


## <a name="getting-hello-scenario"></a>Scenario di recupero hello

Questo scenario è costituito da due runbook PowerShell che è possibile importare direttamente da hello [raccolta Runbook](automation-runbook-gallery.md) hello portale di Azure o scaricare da hello [PowerShell Gallery](https://www.powershellgallery.com).

### <a name="runbooks"></a>Runbook

Runbook | Descrizione| 
--------|------------|
Export-RunAsCertificateToHybridWorker | Runbook consente di esportare un certificato RunAs da un ruolo di lavoro ibrido di tooa account di automazione in modo che i runbook nel ruolo di lavoro hello possono autenticarsi con Azure nei runbook tooimport ordine in hello account di automazione.| 
Sync-LocalGitFolderToAutomationAccount | Le sincronizzazioni runbook hello cartella Git locale nel computer ibrida hello e quindi importare il file di runbook hello (*.ps1) nell'account di automazione hello.|

### <a name="credentials"></a>Credenziali

Credenziali | Descrizione|
-----------|------------|
GitHRWCredential | Asset delle credenziali create toocontain hello username e password per un utente con ruolo di lavoro ibrido toohello autorizzazioni.|

## <a name="installing-and-configuring-this-scenario"></a>Installazione e configurazione dello scenario

### <a name="prerequisites"></a>Prerequisiti

1. Hello sincronizzazione LocalGitFolderToAutomationAccount runbook viene autenticato mediante hello [account RunAs di Azure](automation-sec-configure-azure-runas-account.md). 

2. È necessario anche un'area di lavoro di Microsoft Operations Management Suite (OMS) con hello soluzione di automazione di Azure abilitata e configurata.  Se non si dispone di associato hello automazione account utilizzato tooinstall e configurare questo scenario, viene creato e configurato automaticamente quando si esegue hello **New OnPremiseHybridWorker.ps1** script da ibrida hello runbook worker.        

    > [!NOTE]
    > Attualmente hello regioni seguenti supportano solo integrazione di automazione con OMS - **Australia sudorientale**, **Stati Uniti orientali 2**, **Asia sudorientale**, e **occidentale Europa**. 

3. Un computer che può essere utilizzato come un Runbook Worker ibrido dedicato che ospiterà anche software GitHub hello e gestire i file di runbook hello (*runbook*con estensione ps1) in una directory di origine nel hello file system toosynchronize tra GitHub e Account di automazione.

### <a name="import-and-publish-hello-runbooks"></a>Importare e pubblicare i runbook hello

hello tooimport *esportazione RunAsCertificateToHybridWorker* e *sincronizzazione LocalGitFolderToAutomationAccount* runbook da hello raccolta di Runbook dell'account di automazione in hello portale di Azure Seguire le procedure di hello in [Importa Runbook dalla raccolta di Runbook hello](automation-runbook-gallery.md#to-import-a-runbook-from-the-runbook-gallery-with-the-azure-portal). Pubblicazione di un runbook hello dopo che sono stati importati correttamente nell'account di automazione.

### <a name="deploy-and-configure-hybrid-runbook-worker"></a>Distribuire e configurare un ruolo di lavoro ibrido per runbook

Se non si dispone di un Runbook Worker ibrido già distribuiti nel data center, è necessario rivedere i requisiti di hello e seguire i passaggi di installazione hello automatizzata utilizzando la procedura hello in [Azure Automation Runbook worker ibridi - automatizzare installare Configurazione e](automation-hybrid-runbook-worker.md#automated-deployment).  Dopo aver installato il ruolo di lavoro di hello ibrido correttamente in un computer, eseguire hello seguendo i passaggi toocomplete toosupport relativa configurazione in questo scenario.

1. Accedere toohello hosting hello Runbook Worker ibrido ruolo computer con un account che dispone di diritti amministrativi locali e creare un file di runbook directory toohold hello Git.  Clone hello Git repository toohello directory interna.
2. Se non si dispone già di un account RunAs creato o si desidera toocreate uno nuovo dedicato a tale scopo, dal portale di Azure hello passare tooAutomation account, selezionare l'account di automazione e creare un [asset delle credenziali](automation-credentials.md) che contiene hello username e password per un utente con ruolo di lavoro ibrido toohello autorizzazioni.  
3. Dall'account di automazione, [modificare runbook hello](automation-edit-textual-runbook.md)**esportazione RunAsCertificateToHybridWorker** e modificare il valore di hello per hello variabile *$Password* con un nome sicuro password.    Dopo aver modificato il valore di hello, fare clic su **pubblica** toohave hello versione bozza hello runbook pubblicati. 
5. Avviare runbook hello **esportazione RunAsCertificateToHybridWorker**e in hello **avvia Runbook** pannello opzione hello **impostazioni esecuzione test** selezionare opzione hello **Worker ibrido** in hello elenco a discesa selezionare hello ibrida gruppo di lavoro creato in precedenza per questo scenario.  

    Consente di esportare un ruolo di lavoro ibrido toohello certificato in modo che i runbook nel ruolo di lavoro hello possono autenticarsi con Azure utilizzando hello Esegui come connessione in ordine toomanage risorse di Azure (in particolare per questo scenario - Importa runbook toohello account di automazione).

4. Dall'account di automazione, selezionare hello gruppo di lavoro ibridi creato in precedenza e [specificare un account RunAs](automation-hrw-run-runbooks.md#runas-account) per gruppo di lavoro ibridi hello e asset delle credenziali di hello scelto è sufficiente o è già stato creato.  In questo modo che Hello sincronizzazione runbook può eseguire i comandi Git. 
5. Avviare runbook hello **sincronizzazione LocalGitFolderToAutomationAccount**, fornire i seguenti hello richiesti i valori dei parametri di input e in hello **avvia Runbook** pannello opzione hello **eseguire impostazioni** selezionare opzione hello **Worker ibrido** in hello elenco a discesa selezionare hello ibrida gruppo di lavoro creato in precedenza per questo scenario:
    * *Gruppo di risorse* : hello nome del gruppo di risorse associato all'account di automazione
    * *AutomationAccountName* : hello nome dell'account di automazione
    * *GitPath* : hello cartella locale o di file in hello Runbook Worker ibrido in cui è impostato Git toopull modifiche più recenti in

    Verrà sincronizzazione cartella Git locale hello nel computer di lavoro ibridi hello e quindi di importare file con estensione ps1 hello hello origine directory toohello account di automazione.

    ![Avviare Sync-LocalGitFolderToAutomationAccount Runbook](media/automation-scenario-source-control-integration-with-github-ent/start-runbook-synclocalgitfoldertoautoacct.png)<br>

7. Visualizzare i dettagli di riepilogo di processo per il runbook hello selezionandolo hello **runbook** pannello nell'account di automazione e quindi seleziona hello **processi** riquadro.  Verificare che siano stati completati selezionando hello **tutti i log** riquadro e flusso di log dettagliato hello esaminare i risultati.  

## <a name="next-steps"></a>Passaggi successivi

-  tooknow ulteriori informazioni sui tipi di runbook, i relativi vantaggi e limitazioni, vedere [tipi di runbook di automazione di Azure](automation-runbook-types.md)
-  Per altre informazioni sulla funzionalità di supporto degli script PowerShell, vedere il blog relativo al [supporto di script PowerShell nativi in Automazione di Azure](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)
