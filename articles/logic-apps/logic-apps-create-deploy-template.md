---
title: modelli di distribuzione aaaCreate per le applicazioni di logica di Azure | Documenti Microsoft
description: Creare modelli di Azure Resource Manager per la distribuzione delle app per la logica e la gestione dei rilasci
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 85928ec6-d7cb-488e-926e-2e5db89508ee
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 2f09445f10a376a745d6acbba94ca29d5f79fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-templates-for-logic-apps-deployment-and-release-management"></a>Creare modelli per la distribuzione delle app per la logica e la gestione dei rilasci

Dopo aver creata un'app di logica, è possibile toocreate come un modello di gestione risorse di Azure.
In questo modo, è possibile distribuire facilmente hello logica app tooany ambiente o il gruppo di risorse in cui potrebbe essere necessario.
Per altre informazioni sui modelli di Resource Manager, vedere gli articoli su [creazione di modelli di Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) e [distribuzione delle risorse con i modelli di Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="logic-app-deployment-template"></a>Modello di distribuzione di app per la logica

Un'app per la logica dispone di tre componenti di base:

* **Risorse app logica**: contiene informazioni sugli elementi quali prezzi piano, il percorso e definizione di flusso di lavoro hello.
* **Definizione del flusso di lavoro**: descrive i passaggi del flusso di lavoro e come motore di App per la logica di hello deve essere eseguita del flusso di lavoro hello logica dell'applicazione.
È possibile visualizzare questa definizione nella finestra **Visualizzazione Codice** dell'app per la logica.
Nella risorsa di applicazione hello logica, è possibile trovare questa definizione in hello `definition` proprietà.
* **Connessioni**: fa riferimento a risorse tooseparate archiviano in modo sicuro i metadati relativi a tutte le connessioni connettore, ad esempio una stringa di connessione e un token di accesso.
Nella risorsa di applicazione hello logica, la logica app fa riferimento a queste risorse in hello `parameters` sezione.

È possibile visualizzare tutti questi elementi delle app per la logica esistenti usando uno strumento come [Esplora inventario risorse di Azure](http://resources.azure.com).

toomake un modello per un'app di logica toouse con distribuzioni del gruppo di risorse, è necessario definire le risorse di hello e parametri in base alle esigenze.
Ad esempio, se si distribuisce tooa sviluppo, test e ambiente di produzione, può essere opportuno i database SQL tooa toouse connessione diverse stringhe in ogni ambiente.
In alternativa, è possibile toodeploy in diverse sottoscrizioni o gruppi di risorse.  

## <a name="create-a-logic-app-deployment-template"></a>Creare un modello di distribuzione di app per la logica

toohave modo più semplice di Hello un modello di distribuzione app logica valida è toouse il [Visual Studio Tools per App per la logica](logic-apps-deploy-from-vs.md).
strumenti di Visual Studio Hello generano un modello di distribuzione valido che può essere utilizzato in qualsiasi percorso o la sottoscrizione.

Esistono altri strumenti utili per la creazione di un modello di distribuzione di app per la logica.
È possibile creare manualmente, vale a dire usando hello risorse già descritto qui toocreate parametri in base alle esigenze.
Un'altra opzione è toouse un [autore del modello app logica](https://github.com/jeffhollan/LogicAppTemplateCreator) modulo di PowerShell. Questo modulo open source valuta innanzitutto hello logica app e le connessioni che utilizza e quindi genera risorse modello con i parametri necessari hello per la distribuzione.
Ad esempio, se si dispone di un'app di logica che riceve un messaggio da una coda di Service Bus di Azure e aggiunge dati tooan Azure SQL database, strumento hello mantiene tutta la logica dell'orchestrazione hello e Parametrizza hello SQL e le stringhe di connessione di Service Bus in modo che possano essere impostati in fase di distribuzione.

> [!NOTE]
> Le connessioni devono essere all'interno di hello hello logica app stesso gruppo di risorse.
>
>

### <a name="install-hello-logic-app-template-powershell-module"></a>Installare il modulo PowerShell di modello di hello logica app
modulo di Hello più semplice modo tooinstall hello è tramite hello [PowerShell Gallery](https://www.powershellgallery.com/packages/LogicAppTemplate/0.1), utilizzando il comando hello `Install-Module -Name LogicAppTemplate`.  

È anche possibile installare il modulo di PowerShell hello manualmente:

1. Scaricare la versione più recente di hello di hello [autore del modello app logica](https://github.com/jeffhollan/LogicAppTemplateCreator/releases).  
2. Estrarre la cartella hello nella cartella del modulo di PowerShell (in genere `%UserProfile%\Documents\WindowsPowerShell\Modules`).

Per hello modulo toowork con qualsiasi tenant e sottoscrizione accesso token, è consigliabile utilizzarlo con hello [ARMClient](https://github.com/projectkudu/ARMClient) strumento da riga di comando.  Questo [post di blog ](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html) illustra ARMClient in modo più dettagliato.

### <a name="generate-a-logic-app-template-by-using-powershell"></a>Generare un modello di app per la logica tramite PowerShell
Dopo l'installazione di PowerShell, è possibile generare un modello utilizzando hello comando seguente:

`armclient token $SubscriptionId | Get-LogicAppTemplate -LogicApp MyApp -ResourceGroup MyRG -SubscriptionId $SubscriptionId -Verbose | Out-File C:\template.json`

`$SubscriptionId`ID di sottoscrizione di Azure hello. Questa riga ottiene innanzitutto un accesso token tramite ARMClient, quindi invia tramite pipe tramite toohello script di PowerShell e quindi crea il modello di hello in un file JSON.

## <a name="add-parameters-tooa-logic-app-template"></a>Aggiungere modello di applicazione di parametri tooa logica
Dopo aver creato il modello di applicazione logica, è possibile continuare tooadd o modificare i parametri che potrebbero essere necessari. Ad esempio, se la definizione include un ID di risorsa tooan funzione Azure o di un flusso di lavoro annidato che si prevede di toodeploy in un'unica distribuzione, è possibile aggiungere ulteriori modelli tooyour di risorse e parametrizzare ID in base alle esigenze. Hello vale tooany riferimenti toocustom API o Swagger endpoint desiderato toodeploy con ogni gruppo di risorse.

## <a name="deploy-a-logic-app-template"></a>Distribuire un modello di app per la logica

È possibile distribuire il modello utilizzando qualsiasi strumento come PowerShell, l'API REST [gestione del rilascio di Visual Studio Team Services](#team-services)e la distribuzione dei modelli tramite hello portale di Azure.
I valori hello toostore per i parametri, è inoltre consigliabile creare un [file parametro](../azure-resource-manager/resource-group-template-deploy.md#parameter-files).
Informazioni su come troppo[distribuire le risorse con i modelli di gestione risorse di Azure e PowerShell](../azure-resource-manager/resource-group-template-deploy.md) o [distribuire le risorse con i modelli di gestione risorse di Azure e Azure portal hello](../azure-resource-manager/resource-group-template-deploy-portal.md).

### <a name="authorize-oauth-connections"></a>Autorizzare le connessioni OAuth

Dopo la distribuzione, hello logica app funziona end-to-end con parametri validi.
Tuttavia, è comunque necessario autorizzare OAuth connessioni toogenerate un token di accesso valido.
tooauthorize OAuth connessioni, aprire hello logica app nella logica di progettazione di App hello e autorizzare le connessioni. O per la distribuzione automatica, è possibile utilizzare un tooeach tooconsent script connessione OAuth.
Nel progetto [LogicAppConnectionAuth](https://github.com/logicappsio/LogicAppConnectionAuth) è presente uno script di esempio su GitHub.

<a name="team-services"></a>
## <a name="visual-studio-team-services-release-management"></a>Visual Studio Team Services Release Management

Uno scenario comune per la distribuzione e gestione di un ambiente è uno strumento come gestione del rilascio in Visual Studio Team Services con un modello di distribuzione app logica toouse. Visual Studio Team Services include un [distribuzione gruppo di risorse di Azure](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/DeployAzureResourceGroup) attività che è possibile aggiungere build tooany o della pipeline di rilascio. È necessario toohave un [dell'entità servizio](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/) per l'autorizzazione toodeploy, quindi è possibile generare la definizione di versione hello.

1. In Release Management selezionare **Vuoto** per creare una definizione vuota.

    ![Creare una definizione vuota][1]

2. Scegliere tutte le risorse che necessarie per questa operazione, probabilmente inclusi hello logica app modello generato manualmente o come parte di hello processo di compilazione.
3. Aggiungere un'attività **Distribuzione gruppo di risorse di Azure** .
4. Configurare con un [dell'entità servizio](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/)e fare riferimento ai file di modello e i parametri di modello hello.
5. Continuare toobuild passaggi nel processo di rilascio hello per qualsiasi altro ambiente, dei test automatizzati o responsabili approvazione in base alle esigenze.

<!-- Image References -->
[1]: ./media/logic-apps-create-deploy-template/emptyreleasedefinition.png
