---
title: soluzioni di gestione aaaCreating Operations Management Suite (OMS) | Documenti Microsoft
description: "Soluzioni di gestione estendono le funzionalità di hello di Operations Management Suite (OMS), fornendo gli scenari di gestione di pacchetti che è possibile aggiungere l'area di lavoro OMS tootheir.  Questo articolo fornisce informazioni dettagliate su come creare toobe di soluzioni di gestione utilizzato nel proprio ambiente o resi disponibili tooyour clienti."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f408df1b21f519fd1eb2cbeb19cca18f6c4161f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a>Creazione di una soluzione di gestione in Operations Management Suite (OMS) (anteprima)
> [!NOTE]
> Questa è una documentazione preliminare per la creazione di soluzioni di gestione in OMS attualmente disponibili in versione di anteprima. Qualsiasi schema descritto di seguito è soggetto toochange.  

Le soluzioni di gestione in Operations Management Suite (OMS) vengono implementate come [modelli di Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).  attività principali Hello per apprendere come tooauthor soluzioni di gestione, è fondamentale comprendere come troppo[creare un modello](../azure-resource-manager/resource-group-authoring-templates.md).  Questo articolo fornisce informazioni dettagliate univoci dei modelli utilizzati per le soluzioni e come risorse tipica soluzione tooconfigure.


## <a name="tools"></a>Strumenti

È possibile utilizzare qualsiasi toowork editor di testo con i file di soluzione, ma è consigliabile l'utilizzo delle funzionalità di hello fornite in Visual Studio o codice di Visual Studio, come descritto in hello seguenti articoli.

- [Creazione e distribuzione di gruppi di risorse di Azure tramite Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [Utilizzo dei modelli di Azure Resource Manager nel codice di Visual Studio](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a>Structure
struttura di base di un file di soluzione di gestione Hello è hello stesso come un [modello di gestione risorse](../azure-resource-manager/resource-group-authoring-templates.md#template-format) cui è indicato di seguito.  Hello sezioni seguenti vengono descritti gli elementi di livello superiore di hello ed e il relativo contenuto in una soluzione.  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a>parameters
[I parametri](../azure-resource-manager/resource-group-authoring-templates.md#parameters) sono valori richiesti dall'utente hello quando installano la soluzione di gestione hello.  Ci sono parametri standard comuni a tutte le soluzioni ed è possibile aggiungere altri parametri in base a quanto necessario per la soluzione specifica.  Modo gli utenti forniscono i valori dei parametri quando si installa la soluzione dipenderà determinato parametro hello e la modalità di installazione soluzione hello.

Quando un utente installa la soluzione di gestione tramite hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) o [modelli di avvio rapido di Azure](operations-management-suite-solutions.md#finding-and-installing-management-solutions) sono tooselect richiesta un [OMS dell'area di lavoro e account di automazione ](operations-management-suite-solutions.md#oms-workspace-and-automation-account).  Questi sono valori hello toopopulate utilizzato di ciascun parametro hello standard.  Hello utente non vengono richieste toodirectly fornire valori per parametri standard hello, ma sono valori tooprovide richiesta per i parametri aggiuntivi.

Quando utente hello installa la soluzione [un altro metodo](operations-management-suite-solutions.md#finding-and-installing-management-solutions), devono specificare un valore per tutti i parametri standard e tutti i parametri aggiuntivi.

Di seguito è illustrato un parametro di esempio.  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

Hello nella tabella seguente vengono descritti gli attributi di hello di un parametro.

| Attributo | Descrizione |
|:--- |:--- |
| type |Tipo di dati per il parametro hello. controllo di input Hello visualizzato per l'utente hello dipende dal tipo di dati hello.<br><br>bool - Casella di riepilogo a discesa<br>string - Casella di testo<br>int - Casella di testo<br>securestring - Campo della password<br> |
| category |Categoria facoltativo per il parametro hello.  Parametri in hello stessa categoria vengono raggruppati insieme. |
| control |Funzionalità aggiuntiva per i parametri di stringa.<br><br>datetime - Viene visualizzato un controllo Datetime.<br>GUID - valore Guid viene generato automaticamente e non viene visualizzato il parametro hello. |
| description |Descrizione facoltativa per il parametro hello.  Visualizzato in un parametro di toohello informazioni successivo fumetto. |

### <a name="standard-parameters"></a>Parametri standard
Hello nella tabella seguente elenca hello parametri standard per tutte le soluzioni di gestione.  Questi valori vengono popolati per utente hello anziché richiedere il loro quando la soluzione viene installata dal hello Azure Marketplace o Guida rapida di modelli.  utente Hello deve fornire valori per tali se soluzione hello viene installato con un altro metodo.

> [!NOTE]
> interfaccia utente di Hello nei modelli di Azure Marketplace e Guida introduttiva hello prevede che i nomi di parametro hello nella tabella hello.  Se si utilizzano nomi di parametro diversi quindi verrà richiesto all'utente hello e non viene automaticamente popolate.
>
>

| . | Tipo | Descrizione |
|:--- |:--- |:--- |
| accountName |string |Nome dell'account di Automazione di Azure. |
| pricingTier |string |Piano tariffario dell'area di lavoro di Log Analytics e dell'account di Automazione di Azure. |
| regionId |string |Area di hello account di automazione di Azure. |
| solutionName |string |Nome della soluzione hello.  Se si distribuisce la soluzione tramite i modelli di avvio rapido, è necessario definire solutionName come un parametro che consente di definire una stringa invece richiedere hello utente toospecify uno. |
| workspaceName |string |Nome dell'area di lavoro di Log Analytics. |
| workspaceRegionId |string |Area dell'area di lavoro Log Analitica hello. |


Di seguito è la struttura hello parametri hello standard che è possibile copiare e incollare il file di soluzione.  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of hello Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of hello Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


Si fa riferimento a valori tooparameter in altri elementi di soluzione hello con sintassi hello **parametri ('parameter name')**.  Ad esempio, tooaccess hello Nome area di lavoro, si utilizzerebbe **parameters('workspaceName')**

## <a name="variables"></a>variables
[Le variabili](../azure-resource-manager/resource-group-authoring-templates.md#variables) sono valori che verrà utilizzato nel resto di hello della soluzione di gestione di hello.  Questi valori non sono esposti toohello utente installa la soluzione hello.  Si tratta di autore hello tooprovide prevista con un'unica posizione in cui è possibile gestire i valori che possono essere utilizzati più volte nella soluzione hello. È necessario inserire qualsiasi soluzione tooyour specifico di valori nelle variabili come toohard anziché la codifica hello **risorse** elemento.  Questo rende più leggibile il codice hello e consente tooeasily modificare questi valori nelle versioni successive.

Di seguito è riportato un esempio di elemento **variables** con i parametri tipici usati nelle soluzioni.

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

Si fa riferimento a valori toovariable tramite la soluzione hello con sintassi hello **variabili ('variable name')**.  Ad esempio, tooaccess hello variabile SolutionName, si utilizzerebbe **variables('SolutionName')**.

È possibile anche definire variabili complesse che moltiplicano set di valori;  risultano particolarmente utili nelle soluzioni di gestione in cui si definiscono più proprietà per diversi tipi di risorse.  Ad esempio, è Impossibile ristrutturare le variabili della soluzione hello illustrate in precedenza toohello seguente.

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

In questo caso, si fa riferimento toovariable valori tramite la soluzione hello con sintassi hello **variables('variable name').property**.  Ad esempio, tooaccess hello variabile nome di soluzione, si utilizzerebbe **variables('Solution'). Nome**.

## <a name="resources"></a>Risorse
[Risorse](../azure-resource-manager/resource-group-authoring-templates.md#resources) definire hello diverse risorse che installerà e configurerà la soluzione di gestione.  Questo sarà hello più grande e la parte più complesse del modello di hello.  È possibile ottenere struttura hello e una descrizione completa degli elementi di risorsa in [modelli Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#resources).  In altri articoli di questa documentazione sono descritti i tipi di risorse definiti più comunemente. 


### <a name="dependencies"></a>Dipendenze
Hello **dependsOn** elementi specifica un [dipendenza](../azure-resource-manager/resource-group-define-dependencies.md) in un'altra risorsa.  Quando si installa la soluzione hello, non viene creata una risorsa fino a quando tutte le relative dipendenze sono state create.  La soluzione potrebbe ad esempio [avviare un runbook](operations-management-suite-solutions-resources-automation.md#runbooks) quando viene installata usando una [risorsa processo](operations-management-suite-solutions-resources-automation.md#automation-jobs).  risorsa di processo Hello sarebbe dipende hello runbook risorsa toomake runbook hello sia stata creata prima che venga creato il processo di hello.

### <a name="oms-workspace-and-automation-account"></a>Area di lavoro OMS e account di Automazione
Soluzioni di gestione richiedono un [area di lavoro OMS](../log-analytics/log-analytics-manage-access.md) toocontain visualizzazioni e un [account di automazione](../automation/automation-security-overview.md#automation-account-overview) toocontain runbook e le relative risorse.  Questi devono essere disponibili prima hello risorse nella soluzione hello vengono create e non devono essere definite nella soluzione hello stessa.  utente Hello verrà [specificare un account e l'area di lavoro](operations-management-suite-solutions.md#oms-workspace-and-automation-account) quando si distribuisce la soluzione, ma come autore hello è necessario considerare hello seguenti punti.

## <a name="solution-resource"></a>Risorse della soluzione
Ogni soluzione richiede una voce di risorsa in hello **risorse** elemento che definisce una soluzione di hello stessa.  Ciò avrà un tipo di **Microsoft.OperationsManagement/solutions** e hello seguente struttura. Ciò include [parametri standard](#parameters) e [variabili](#variables) che sono di proprietà in genere utilizzate toodefine della soluzione hello.


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a>Dipendenze
Hello soluzione risorsa deve avere un [dipendenza](../azure-resource-manager/resource-group-define-dependencies.md) in tutte le altre risorse nella soluzione hello poiché devono tooexist prima di creare soluzioni hello.  Questo scopo, aggiungere una voce per ogni risorsa in hello **dependsOn** elemento.

### <a name="properties"></a>Proprietà
Hello soluzione hello alcune proprietà della risorsa in hello nella tabella seguente.  Sono incluse risorse hello a cui fa riferimento e contenuti da soluzione hello che definisce la modalità di gestione risorse di hello dopo l'installazione della soluzione hello.  Ogni risorsa nella soluzione hello dovrebbe essere elencato in entrambi hello **referencedResources** o hello **containedResources** proprietà.

| Proprietà | Description |
|:--- |:--- |
| workspaceResourceId |ID dell'area di lavoro di Log Analitica hello in forma di hello  *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<nome area di lavoro\>*. |
| referencedResources |Elenco delle risorse nella soluzione hello che non devono essere rimossi quando la soluzione hello viene rimossa. |
| containedResources |Elenco delle risorse nella soluzione hello che devono essere rimossi quando la soluzione hello viene rimossa. |

esempio Hello precedente è una soluzione con un runbook, a una pianificazione e visualizzazione.  pianificazione di Hello e runbook sono *riferimento* in hello **proprietà** elemento in modo non vengono rimossi quando la soluzione hello viene rimosso.  visualizzazione di Hello è *contenuti* viene rimosso quando viene rimossa la soluzione hello.

### <a name="plan"></a>Pianificazione
Hello **piano** entità della risorsa di soluzione hello dispone di proprietà hello in hello nella tabella seguente.

| Proprietà | Descrizione |
|:--- |:--- |
| name |Nome della soluzione hello. |
| version |Versione della soluzione hello, come determinato dall'autore hello. |
| product |Soluzione di hello tooidentify stringa univoca. |
| publisher |Server di pubblicazione della soluzione hello. |



## <a name="sample"></a>Esempio
È possibile visualizzare esempi di file della soluzione con una risorsa di soluzione in hello posizioni seguenti.

- [Risorse di Automazione](operations-management-suite-solutions-resources-automation.md#sample)
- [Risorse di ricerca e di avviso](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a>Passaggi successivi
* [Aggiungere avvisi e le ricerche salvate](operations-management-suite-solutions-resources-searches-alerts.md) tooyour soluzione di gestione.
* [Aggiungere visualizzazioni](operations-management-suite-solutions-resources-views.md) tooyour soluzione di gestione.
* [Aggiungere i runbook e altre risorse di automazione](operations-management-suite-solutions-resources-automation.md) tooyour soluzione di gestione.
* Informazioni sul supporto di hello [modelli Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).
* Cercare i [modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates) per esempi di modelli di Resource Manager.
