---
title: aaaAzure strumenti da riga di comando multipiattaforma basate su Gestione risorse per l'App Web di Azure | Documenti Microsoft
description: Informazioni su come toouse hello toomanage strumenti da riga di comando multipiattaforma basate su Gestione risorse di Azure nuova App Web di Azure.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a>Utilizzo dell'interfaccia della riga di comando multipiattaforma basata su Azure Resource Manager per servizio app di Azure
> [!div class="op_single_selector"]
> * [Interfaccia della riga di comando di Azure](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)

Con la versione di hello della versione di strumenti della riga di comando multipiattaforma di Microsoft Azure 0.10.5, sono stati aggiunti nuovi comandi. Questi comandi assegnare hello utente hello possibilità toouse basate su Gestione risorse di Azure PowerShell comandi toomanage servizio App.

toolearn sulla gestione dei gruppi di risorse, vedere [toomanage CLI di Azure hello Azure usare risorse e gruppi di risorse](../azure-resource-manager/xplat-cli-azure-resource-manager.md). 

> [!NOTE] 
> Inoltre, provare [CLI di Azure 2.0](https://github.com/Azure/azure-cli), scritto in Python per modello di distribuzione di gestione risorse hello CLI prossima generazione.
>
>

## <a name="managing-app-service-plans"></a>Gestione di piani di servizio app
### <a name="create-an-app-service-plan"></a>Creare un piano di servizio app
toocreate un piano di servizio app, usare hello **appserviceplan azure creare** comando.

Di seguito sono le descrizioni dei parametri diversi hello:

* **-gruppo di risorse**: gruppo di risorse che include il piano di servizio app hello appena creato.
* **-nome**: nome del piano di servizio app hello.
* **--location**: località del piano di servizio app.
* **-sku**: hello desiderato sku di determinazione dei prezzi (hello opzioni sono: F1 (Free). D1 (Condiviso), B1 (Basic Small), B2 (Basic Medium), B3 (Basic Large), S1 (Standard Small), S2 (Standard Medium), S3 (Standard Large), P1 (Premium Small), P2 (Premium Medium) e P3 (Premium Large).
* **-istanze**: hello numero di thread di lavoro nel piano di servizio app hello (valore predefinito è 1).

Esempio toouse questo cmdlet:

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a>Creare un nuovo piano di servizio app

Utilizzando hello stesso **appserviceplan azure creare** comando, con hello parametro aggiuntivo **true - islinux**. Tenere presenti le restrizioni di hello e aree descritte nella [tooApp introduzione del servizio su Linux](app-service-linux-intro.md)

### <a name="list-existing-app-service-plans"></a>Visualizzare un elenco dei piani di servizio app esistenti
Utilizzare toolist hello esistente piani di servizio app, **appserviceplan azure elenco** comando.

toolist tutti i piani di servizio app in un gruppo di risorse specifico, utilizzare:

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

Utilizzare un piano di servizio app specifica, tooget **appserviceplan azure Mostra** comando:

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a>Configurare un piano di servizio app esistente
toochange hello impostazioni per un piano di servizio app esistente, utilizzare hello **configurazione azure appserviceplan** comando. È possibile modificare lo sku hello e il numero di lavori hello 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a>Ridimensionamento di un piano di servizio app
tooscale un esistente piano di servizio App, usare:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a>Modifica hello SKU di un piano di servizio App
toochange hello sku di un'esistente piano di servizio App, utilizzare:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a>Eliminare un piano di servizio app esistente
toodelete un piano di servizio app esistente, tutti assegnati App necessità toobe spostati o eliminati per primi. Utilizzando quindi hello **webapp azure eliminare** comando è possibile eliminare il piano di servizio app hello.

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a>Gestione delle app di servizio app
### <a name="create-a-web-app"></a>Creare un'app Web
toocreate un'app web, utilizzare hello **webapp azure creare** comando.

Di seguito sono le descrizioni dei parametri diversi hello:

* **-nome**: nome per l'app web hello.
* **-piano**: assegnare un nome per il piano di servizio hello utilizzato toohost hello web app.
* **-gruppo di risorse**: gruppo di risorse che ospita il piano di servizio App hello.
* **-percorso**: hello percorso app web.

Esempio toouse questo cmdlet:

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a>Eliminare un'app esistente
toodelete un'app esistente, è possibile utilizzare hello **webapp azure eliminare** comando. È necessario toospecify hello nome dell'applicazione hello e il nome del gruppo di risorse hello.

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a>Visualizzare un elenco delle app esistenti
app di esistenti hello toolist, utilizzare hello **elenco webapp azure** comando.

toolist tutte le App in un gruppo di risorse specifico, utilizzare:

    azure webapp list --resource-group ContosoAzureResourceGroup

tooget un'app specifica, utilizzare hello **webapp azure Mostra** comando.

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a>Configurare un'app esistente
toochange hello impostazioni e configurazioni per un'app esistente, utilizzare hello **set di configurazione di azure webapp** comando.

Esempio (1): modificare la versione di php hello di un'app 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

Esempio (2): aggiungere o modificare le impostazioni dell'app

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

tooknow altri della configurazione può essere modificata, utilizzare hello **set di configurazione azure webapp -h** comando.

### <a name="change-hello-state-of-an-existing-app"></a>Modifica dello stato di hello di un'app esistente
#### <a name="restart-an-app"></a>Riavviare un'app
toorestart un'app, è necessario specificare gruppo hello di nome e la risorsa dell'applicazione hello.

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a>Arrestare un'app
toostop un'app, è necessario specificare gruppo hello di nome e la risorsa dell'applicazione hello.

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a>Avviare un'app
toostart un'app, è necessario specificare gruppo hello di nome e la risorsa dell'applicazione hello.

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a>Gestire i profili di pubblicazione di un'app
Ogni app ha un profilo di pubblicazione che può essere utilizzati toopublish il codice.

#### <a name="get-publishing-profile"></a>Recuperare il profilo di pubblicazione
hello tooget profilo per un'app, l'utilizzo di pubblicazione:

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

Questo comando restituisce hello profilo nome utente e password toohello riga di comando di pubblicazione.

### <a name="manage-app-hostnames"></a>Gestire i nomi host dell'app
le associazioni nome host toomanage per l'app, usare hello **nomi host di configurazione di azure webapp** comando  

#### <a name="list-hostname-bindings"></a>Elencare le associazioni nome host
tooget hello corrente le associazioni nome host per un'app, usare:

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a>Aggiungere associazioni nome host
tooadd hostname associazioni tooan app, utilizzare:

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a>Eliminare associazioni nome host
le associazioni nome host toodelete, utilizzare:

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a>Passaggi successivi
* toolearn sul supporto di Azure Resource Manager CLI, vedere [toomanage CLI di Azure hello Azure usare risorse e gruppi di risorse.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)
* toolearn sulla gestione del servizio App tramite PowerShell, vedere [tooManage Using Azure Resource Manager-Based PowerShell App Web di Azure.](app-service-web-app-azure-resource-manager-powershell.md)
* toolearn sul servizio App di Azure su Linux, vedere [tooApp introduzione del servizio su Linux](app-service-linux-intro.md)
