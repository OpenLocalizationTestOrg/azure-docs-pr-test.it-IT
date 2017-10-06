---
title: aaaIntegrate automazione di Azure con controllo del codice sorgente di Visual Studio Team Services | Documenti Microsoft
description: Questo scenario illustra l'impostazione dell'integrazione con un account di Automazione di Azure e controllo del codice sorgente di Visual Studio Team Services.
services: automation
documentationcenter: 
author: eamono
manager: 
editor: 
keywords: Azure PowerShell, VSTS, controllo del codice sorgente, automazione
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.openlocfilehash: 8f6faa596a5ad1f8b72e820ca320b3e103d83579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a>Scenario di Automazione di Azure - Integrazione del controllo del codice sorgente con Visual Studio Team Services

In questo scenario, è necessario un progetto di Visual Studio Team Services che si utilizza toomanage runbook di automazione di Azure o le configurazioni DSC nel controllo del codice sorgente.
Questo articolo viene descritto come toointegrate VSTS con l'ambiente di automazione di Azure in modo che l'integrazione continua venga eseguita per ogni archiviazione.

## <a name="getting-hello-scenario"></a>Scenario di recupero hello

Questo scenario è costituito da due runbook PowerShell che è possibile importare direttamente da hello [raccolta Runbook](automation-runbook-gallery.md) hello portale di Azure o scaricare da hello [PowerShell Gallery](https://www.powershellgallery.com).

### <a name="runbooks"></a>Runbook

Runbook | Descrizione| 
--------|------------|
Sincronizzazione VSTS | Importare runbook o configurazioni dal controllo del codice sorgente VSTS al termine di un'archiviazione. Se eseguito manualmente, sarà importare e pubblicare tutti i runbook o configurazioni in hello account di automazione.| 
Sincronizzazione VSTSGit | Importare runbook o configurazioni da VSTS nel controllo del codice sorgente Git al termine di un'archiviazione. Se eseguito manualmente, sarà importare e pubblicare tutti i runbook o configurazioni in hello account di automazione.|

### <a name="variables"></a>variables

Variabile | Descrizione|
-----------|------------|
VSToken | Proteggere asset della variabile verrà creato che contiene i token di accesso personale VSTS hello. È possibile ottenere informazioni di modalità di accesso personale VSTS di toocreate token su hello [pagina autenticazione VSTS](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview). 
## <a name="installing-and-configuring-this-scenario"></a>Installazione e configurazione dello scenario

Creare un [token di accesso personale](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) in VSTS che si utilizzeranno i runbook hello toosync o configurazioni nell'account di automazione.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

Creare un [variabile secure](automation-variables.md) nel hello toohold account di automazione di accesso personale token in modo che i runbook hello può autenticarsi tooVSTS e sincronizzazione runbook hello o configurazioni in hello account di automazione. È possibile denominare questo token VSToken. 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

Importare runbook hello che verrà eseguita la sincronizzazione del runbook o configurazioni nell'account di automazione hello. È possibile utilizzare hello [runbook di esempio VSTS](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) o hello [Visual Studio Team Services con i runbook di esempio Git] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) da hello PowerShellGallery.com a seconda se si utilizza Visual Studio Team Services controllo o VSTS con Git di origine e distribuire tooyour account di automazione.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

È ora possibile [pubblicare](automation-creating-importing-runbook.md#publishing-a-runbook) questo runbook in modo da creare un webhook. 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

Creare un [webhook](automation-webhooks.md) per questo runbook VSTS di sincronizzazione e inserire parametri hello, come illustrato di seguito. Assicurarsi di copiare url del webhook hello perché sarà necessaria per una funzione hook del servizio in Visual Studio Team Services. Hello VSAccessTokenVariableName è il nome di hello (VSToken) della variabile di hello sicura creata dal token di accesso personale hello toohold precedenti. 

L'integrazione con Visual Studio Team Services (Sync-VSTS.ps1) richiederà hello seguenti parametri.
### <a name="sync-vsts-parameters"></a>Parametri di sincronizzazione VSTS

. | Descrizione| 
--------|------------|
WebhookData | Questa conterrà le informazioni sull'archiviazione hello inviati da hello VSTS servizio hook. È necessario lasciare vuoto questo parametro.| 
ResourceGroup | Questo è il nome di hello hello risorsa del gruppo di account di automazione hello in.|
AutomationAccountName | nome Hello dell'account di automazione hello che verrà eseguita la sincronizzazione con Visual Studio Team Services.|
VSFolder | Il nome della cartella hello in Visual Studio Team Services in cui sono presenti runbook hello e configurazioni.|
VSAccount | nome Hello di hello account Visual Studio Team Services.| 
VSAccessTokenVariableName | nome di Hello di hello sicura variabile (VSToken) che contiene i token di accesso personale VSTS hello.| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

Se si utilizza Visual Studio Team Services con GIT (Sync-VSTSGit.ps1) richiederà hello seguenti parametri.

. | Descrizione|
--------|------------|
WebhookData | Questa conterrà le informazioni sull'archiviazione hello inviati da hello VSTS servizio hook. È necessario lasciare vuoto questo parametro.| ResourceGroup | Questo nome hello hello risorsa del gruppo di account di automazione hello in.|
AutomationAccountName | nome Hello dell'account di automazione hello che verrà eseguita la sincronizzazione con Visual Studio Team Services.|
VSAccount | nome Hello di hello account Visual Studio Team Services.|
VSProject | nome di Hello del progetto hello in Visual Studio Team Services in cui sono presenti runbook hello e configurazioni.|
GitRepo | nome Hello del repository Git hello.|
GitBranch | nome di Hello di hello ramo nel repository Git di Visual Studio Team Services.|
Cartella | nome di Hello della cartella hello in ramo Git di Visual Studio Team Services.|
VSAccessTokenVariableName | nome di Hello di hello sicura variabile (VSToken) che contiene i token di accesso personale VSTS hello.|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

Creare un hook del servizio in Visual Studio Team Services per la cartella toohello archiviazioni che attiva il webhook check-in codice. Selezionare Web hook come hello servizio toointegrate con quando si crea una nuova sottoscrizione. È possibile acquisire familiarità con gli hook del servizio nella [documentazione relativa agli hook del servizio VSTS](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

Deve essere in grado di toodo tutte le archiviazioni dei runbook e le configurazioni in VSTS e sono automaticamente sincronizzati era nell'account di automazione.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

Se si esegue manualmente il runbook senza avviato da Visual Studio Team Services, è possibile lasciare vuoto il parametro webhookdata hello e eseguirà una sincronizzazione completa dalla cartella VSTS hello specificata.

Se si desidera scenario hello toouninstall, rimuovere hello servizio hook da Visual Studio Team Services, eliminare runbook hello e hello VSToken variabile.
