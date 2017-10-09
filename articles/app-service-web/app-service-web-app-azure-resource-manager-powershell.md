---
title: i comandi aaaAzure basate su Gestione risorse di PowerShell per App Web di Azure | Documenti Microsoft
description: Informazioni su come toouse hello toomanage di comandi basati su Gestione risorse di Azure PowerShell nuova App Web di Azure.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a>Uso di PowerShell Azure Resource Manager-Based tooManage Azure Web App
> [!div class="op_single_selector"]
> * [Interfaccia della riga di comando di Azure](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

Con Microsoft Azure PowerShell versione 1.0.0 sono stati aggiunti nuovi comandi, in modo da fornire hello utente hello possibilità toouse basate su Gestione risorse di Azure PowerShell comandi toomanage App Web.

toolearn sulla gestione dei gruppi di risorse, vedere [tramite Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md). 

toolearn sull'elenco completo di hello dei parametri e le opzioni di hello i cmdlet di PowerShell, vedere hello [completo riferimento ai Cmdlet basato su Web App Azure Resource Manager Cmdlets di PowerShell](https://msdn.microsoft.com/library/mt619237.aspx)

## <a name="managing-app-service-plans"></a>Gestione di piani di servizio app
### <a name="create-an-app-service-plan"></a>Creare un piano di servizio app
toocreate un piano di servizio app, usare hello **New AzureRmAppServicePlan** cmdlet.

Di seguito sono le descrizioni dei parametri diversi hello:

* **Nome**: nome del piano di servizio app hello.
* **Location**: località del piano di servizio.
* **ResourceGroupName**: gruppo di risorse che include il piano di servizio app hello appena creato.
* **Livello**: hello desiderato piano tariffario (valore predefinito è gratuito, altre opzioni sono condiviso, Basic, Standard e Premium).
* **WorkerSize**: hello dimensioni di processi di lavoro (impostazione predefinita è piccola se è stato specificato il parametro di livello hello come Basic, Standard o Premium. Le altre opzioni sono Medium e Large.
* **Il numero di lavori**: hello numero di thread di lavoro nel piano di servizio app hello (valore predefinito è 1). 

Esempio toouse questo cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a>Creare un piano di servizio app in un ambiente del servizio app
toocreate piano di servizio app in un ambiente del servizio app, utilizzare hello stesso comando **New AzureRmAppServicePlan** con hello toospecify parametri aggiuntivi del ASE nome e il nome del gruppo di risorse di base.

Esempio toouse questo cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

altre informazioni sull'ambiente del servizio app, controllo toolearn [tooApp introduzione dell'ambiente del servizio](app-service-app-service-environment-intro.md)

### <a name="list-existing-app-service-plans"></a>Visualizzare un elenco dei piani di servizio app esistenti
Utilizzare toolist hello esistente piani di servizio app, **Get AzureRmAppServicePlan** cmdlet.

toolist tutti i piani di servizio app nella sottoscrizione, utilizzare: 

    Get-AzureRmAppServicePlan

toolist tutti i piani di servizio app in un gruppo di risorse specifico, utilizzare:

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

tooget un piano di servizio app specifica, utilizzare:

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a>Configurare un piano di servizio app esistente
toochange hello impostazioni per un piano di servizio app esistente, utilizzare hello **Set AzureRmAppServicePlan** cmdlet. È possibile modificare il livello di hello, dimensione di lavoro e il numero di lavori hello 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a>Ridimensionamento di un piano di servizio app
tooscale un esistente piano di servizio App, usare:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a>Modifica delle dimensioni di lavoro hello di un piano di servizio App
dimensioni di hello toochange di processi di lavoro in un App servizio piano esistente, utilizzare:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a>Modifica hello a livello di un piano di servizio App
livello di hello toochange di un App servizio piano esistente, utilizzare:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a>Eliminare un piano di servizio app esistente
toodelete un piano di servizio app esistente, tutti assegnati web App necessità toobe spostati o eliminati per primi. Utilizzando quindi hello **Remove AzureRmAppServicePlan** cmdlet è possibile eliminare il piano di servizio app hello.

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a>Gestione di app Web del servizio app
### <a name="create-a-web-app"></a>Creare un'app Web
toocreate un'app web, utilizzare hello **New AzureRmWebApp** cmdlet.

Di seguito sono le descrizioni dei parametri diversi hello:

* **Nome**: nome per l'app web hello.
* **AppServicePlan**: assegnare un nome per il piano di servizio hello utilizzato toohost hello web app.
* **ResourceGroupName**: gruppo di risorse che ospita il piano di servizio App hello.
* **Percorso**: hello percorso app web.

Esempio toouse questo cmdlet:

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a>Creare un'app Web in un ambiente del servizio app
toocreate un'app web in un ambiente di servizio App (ASE). Utilizzare hello stesso **New AzureRmWebApp** comando con parametri aggiuntivi toospecify hello ASE nome e il nome di gruppo di risorse hello hello ASE a cui appartiene.

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

altre informazioni sull'ambiente del servizio app, controllo toolearn [tooApp introduzione dell'ambiente del servizio](app-service-app-service-environment-intro.md)

### <a name="delete-an-existing-web-app"></a>Eliminare un'app Web esistente
un'app web esistente, è possibile utilizzare hello toodelete **Remove AzureRmWebApp** cmdlet, è necessario toospecify hello nome dell'app web hello e il nome del gruppo di risorse hello.

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a>Visualizzare un elenco delle app Web esistenti
toolist hello esistente nelle App web, utilizzare hello **Get AzureRmWebApp** cmdlet.

toolist tutte le app web nella sottoscrizione, utilizzare:

    Get-AzureRmWebApp

toolist tutte le app web in un gruppo di risorse specifico, utilizzare:

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

tooget un'applicazione web specifica, utilizzare:

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a>Configurare un'app Web esistente
toochange hello impostazioni e configurazioni per un'app web esistente, utilizzare hello **Set AzureRmWebApp** cmdlet. Per un elenco completo dei parametri, controllare hello [collegamento di riferimento di Cmdlet](https://msdn.microsoft.com/library/mt652487.aspx)

Esempio (1): utilizzare questo cmdlet toochange le stringhe di connessione

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

Esempio (2): aggiungere o modificare le impostazioni dell'app

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


Esempio (3): impostare hello web app toorun in modalità a 64 bit

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a>Modifica dello stato di hello di un'App Web esistente
#### <a name="restart-a-web-app"></a>Riavviare un'app Web
toorestart un'app web, è necessario specificare hello nome e risorsa gruppo di hello web app.

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a>Arrestare un'app Web
toostop un'app web, è necessario specificare hello nome e risorsa gruppo di hello web app.

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a>Avviare un'app Web
toostart un'app web, è necessario specificare hello nome e risorsa gruppo di hello web app.

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a>Gestire i profili di pubblicazione delle app Web
Ciascuna applicazione web dispone di un profilo di pubblicazione che può essere utilizzati toopublish App, è possibile eseguire diverse operazioni in profili di pubblicazione.

#### <a name="get-publishing-profile"></a>Recuperare il profilo di pubblicazione
hello tooget pubblicazione profilo per un'app web, utilizzare:

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

Questo comando esegue l'eco dell'output di hello pubblicazione profilo toohello riga di comando e hello file di testo tooa profilo di pubblicazione.

#### <a name="reset-publishing-profile"></a>Reimpostare il profilo di pubblicazione
tooreset entrambi hello la password di pubblicazione per FTP e distribuzione web per un'app web, utilizzare:

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a>Gestire i certificati delle app Web
toolearn sulle procedure toomanage web i certificati di app, vedere [binding a certificati SSL con PowerShell](app-service-web-app-powershell-ssl-binding.md)

### <a name="next-steps"></a>Passaggi successivi
* toolearn sul supporto di gestione risorse di Azure PowerShell, vedere [tramite Azure PowerShell con Gestione risorse di Azure.](../powershell-azure-resource-manager.md)
* toolearn sugli ambienti di servizio App, vedere [tooApp introduzione dell'ambiente del servizio.](app-service-app-service-environment-intro.md)
* toolearn sulla gestione dei certificati SSL del servizio App tramite PowerShell, vedere [binding a certificati SSL tramite PowerShell.](app-service-web-app-powershell-ssl-binding.md)
* toolearn sull'elenco completo di hello basate su Gestione risorse di Azure di cmdlet di PowerShell per le app Web di Azure, vedere [riferimento ai Cmdlet di Azure Web App Azure Resource Manager Cmdlets di PowerShell.](https://msdn.microsoft.com/library/mt619237.aspx)
* * toolearn sulla gestione del servizio App usando l'interfaccia CLI, vedere [Using Azure Resource Manager-Based XPlat CLI per l'App Web di Azure.](app-service-web-app-azure-resource-manager-xplat-cli.md)

