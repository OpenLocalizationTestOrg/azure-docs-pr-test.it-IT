---
title: esempi di avvio rapido aaaAzure monitoraggio CLI 1.0. | Microsoft Docs
description: "Comandi dell'interfaccia della riga di comando 1.0 di esempio per le funzionalità di Monitoraggio di Azure. Monitoraggio di Azure è un servizio di Microsoft Azure che consente le notifiche di avviso toosend, gli URL web di chiamata in base ai valori di dati di telemetria configurati e servizi Cloud di scalabilità automatica, macchine virtuali e le applicazioni Web."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1653aa81-0ee6-4622-9c65-d4801ed9006f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6cd9cd62b3a1977276563f5e43f5384ccca66247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a>Esempi di avvio rapido dell'interfaccia della riga di comando multipiattaforma 1.0 per Monitoraggio di Azure
In questo articolo viene indicato il campionamento toohelp comandi dell'interfaccia della riga di comando (CLI) accedere alle funzionalità di monitoraggio di Azure. Monitoraggio di Azure consente tooAutoScale servizi Cloud, macchine virtuali e le applicazioni Web e toosend notifiche di avviso o URL web chiamata in base ai valori dei dati di telemetria configurato.

> [!NOTE]
> Monitoraggio di Azure è hello nuovo nome per ciò che è stato chiamato "Azure Insights" fino a 25 settembre 2016. Tuttavia, gli spazi dei nomi hello e pertanto comandi hello seguenti comunque contengono approfondite"hello".
> 
> 

## <a name="prerequisites"></a>Prerequisiti
Se non è ancora installato hello CLI di Azure, vedere [installazione hello Azure CLI](../cli-install-nodejs.md). Se non si ha familiarità con l'interfaccia CLI di Azure, è possibile leggere altre informazioni, vedere [hello utilizzare CLI di Azure per Mac, Linux e Windows con Gestione risorse di Azure](../xplat-cli-azure-resource-manager.md).

In Windows, installare npm da hello [sito Web Node.js](https://nodejs.org/). Dopo aver completato l'installazione di hello, di CMD.exe con privilegi di Esegui come amministratore, eseguire l'esempio hello dalla cartella hello in cui è installato npm:

```console
npm install azure-cli --global
```

Passare tooany/percorso della cartella desiderata e hello della riga di comando digitare:

```console
azure help
```

## <a name="log-in-tooazure"></a>Accedi tooAzure
primo passaggio Hello è toologin tooyour account Azure.

```console
azure login
```

Dopo aver eseguito questo comando, si disporrà toosign tramite istruzioni hello nella schermata di hello. Vengono quindi visualizzati l'account, l'ID tenant e l'ID sottoscrizione predefinito. Tutti i comandi di lavoro nel contesto di hello della sottoscrizione predefinita.

dettagli di hello toolist della sottoscrizione corrente, utilizzare hello comando seguente.

```console
azure account show
```

toochange lavoro contesto tooa sottoscrizione diversa, utilizzare hello comando seguente.

```console
azure account set "subscription ID or subscription name"
```

i comandi toouse Azure Resource Manager e il monitoraggio di Azure, è necessario toobe in modalità Azure Resource Manager.

```console
azure config mode arm
```

tooview un elenco di tutti i comandi di monitoraggio di Azure supportati, eseguire l'esempio hello.

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a>Visualizzare il registro attività di una sottoscrizione
tooview un elenco di attività del log eventi, eseguire l'esempio hello.

```console
azure insights logs list [options]
```

Provare hello seguente tooview tutte le opzioni disponibili.

```console
azure insights logs list -help
```

Di seguito è riportato un esempio registri toolist da un gruppo di risorse

```console
azure insights logs list --resourceGroup "myrg1"
```

Log di esempio toolist dal chiamante

```console
azure insights logs list --caller "myname@company.com"
```

Log di esempio toolist chiamante in un tipo di risorsa, all'interno di una data di inizio e fine

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a>Usare gli avvisi
È possibile utilizzare le informazioni di hello in hello sezione toowork con avvisi.

### <a name="get-alert-rules-in-a-resource-group"></a>Ottenere regole di avviso in un gruppo di risorse
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a>Creare una regola di avviso metrica
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a>Creare una regola di avviso test Web
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a>Eliminare una regola di avviso
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a>Profili dei log
Utilizzare informazioni hello toowork questa sezione con i profili di log.

### <a name="get-a-log-profile"></a>Acquisizione di un profilo di log
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a>Aggiungere un profilo di log senza conservazione
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>Rimozione di un profilo di log
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a>Aggiungere un profilo di log con conservazione
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a>Aggiungere un profilo di log con conservazione e hub eventi
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a>Diagnostica
Utilizzare informazioni hello toowork questa sezione con le impostazioni di diagnostica.

### <a name="get-a-diagnostic-setting"></a>Ottenere un'impostazione di diagnostica
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a>Disabilitare un'impostazione di diagnostica
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a>Abilitare un'impostazione di diagnostica senza conservazione
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a>Autoscale
Utilizzare informazioni hello toowork questa sezione con le impostazioni di scalabilità automatica. È necessario toomodify questi esempi.

### <a name="get-autoscale-settings-for-a-resource-group"></a>Ottenere le impostazioni di scalabilità automatica per un gruppo di risorse
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a>Ottenere le impostazioni di scalabilità automatica per nome in un gruppo di risorse
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a>Configurare le impostazioni di scalabilità automatica
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
