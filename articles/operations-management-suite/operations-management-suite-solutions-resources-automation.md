---
title: risorse di automazione aaaAzure nelle soluzioni OMS | Documenti Microsoft
description: "Soluzioni in OMS includerà in genere i runbook in automazione di Azure tooautomate processi, ad esempio la raccolta e l'elaborazione dati di monitoraggio.  Questo articolo viene descritto come tooinclude runbook e le relative risorse in una soluzione."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a>Aggiunta di soluzione di gestione OMS tooan risorse automazione di Azure (anteprima)
> [!NOTE]
> Questa è una documentazione preliminare per la creazione di soluzioni di gestione in OMS attualmente disponibili in versione di anteprima. Qualsiasi schema descritto di seguito è soggetto toochange.   


[Soluzioni di gestione in OMS](operations-management-suite-solutions.md) includerà in genere i runbook in automazione di Azure tooautomate processi, ad esempio la raccolta e l'elaborazione dati di monitoraggio.  Toorunbooks, gli account di automazione include inoltre risorse, ad esempio variabili e le pianificazioni che supportano i runbook di hello utilizzati nella soluzione hello.  Questo articolo viene descritto come tooinclude runbook e le relative risorse in una soluzione.

> [!NOTE]
> Hello esempi in questo articolo utilizzano parametri e variabili che sono entrambe soluzioni toomanagement necessarie o comuni e descritte in [la creazione di soluzioni di gestione in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md) 


## <a name="prerequisites"></a>Prerequisiti
Questo articolo si presuppone che si ha già familiarità con le seguenti informazioni hello.

- Come troppo[creare una soluzione di gestione](operations-management-suite-solutions-creating.md).
- struttura di Hello un [file di soluzione](operations-management-suite-solutions-solution-file.md).
- Come troppo[creare modelli di gestione risorse](../azure-resource-manager/resource-group-authoring-templates.md)

## <a name="automation-account"></a>Account di Automazione
Tutte le risorse di Automazione di Azure sono contenute in un [account di Automazione](../automation/automation-security-overview.md#automation-account-overview).  Come descritto in [OMS dell'area di lavoro e account di automazione](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello account di automazione non è incluso nella soluzione di gestione di hello ma deve essere presente prima di installata la soluzione hello.  Se non è disponibile, l'installazione di soluzioni hello avrà esito negativo.

nome di Hello di ogni risorsa automazione include nome hello del relativo account di automazione.  Questa operazione viene eseguita nella soluzione hello con hello **accountName** parametro come hello seguente esempio di una risorsa di runbook.

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a>Runbook
È consigliabile includere tutti i runbook utilizzati dalla soluzione hello nel file di soluzione hello in modo che vengono creati quando si installa la soluzione hello.  È non possono contenere corpo hello del runbook hello nel modello di hello, pertanto è consigliabile pubblicare hello runbook tooa percorso pubblico in modo da essere accessibile da qualsiasi utente che installa la soluzione.

[Runbook di automazione di Azure](../automation/automation-runbook-types.md) risorse hanno un tipo di **Microsoft.Automation/automationAccounts/runbooks** e hello seguente struttura. Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello. 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


in hello nella tabella seguente vengono descritte le proprietà di Hello per runbook.

| Proprietà | Descrizione |
|:--- |:--- |
| runbookType |Specifica i tipi di hello di hello runbook. <br><br> Script - Script di PowerShell <br>PowerShell - Flusso di lavoro di PowerShell <br> GraphPowerShell - Runbook di script di PowerShell grafico <br> GraphPowerShellWorkflow - Runbook di flusso di lavoro di PowerShell grafico |
| logProgress |Specifica se [stato record](../automation/automation-runbook-output-and-messages.md) devono essere generati per hello runbook. |
| logVerbose |Specifica se [record dettagliati](../automation/automation-runbook-output-and-messages.md) devono essere generati per hello runbook. |
| description |Descrizione facoltativa per il runbook hello. |
| publishContentLink |Specifica il contenuto di hello di hello runbook. <br><br>URI - Uri toohello contenuto del runbook hello.  Si tratterà di un file con estensione ps1 per i runbook di PowerShell e di script e di un file di runbook grafico esportato per un runbook di Graph.  <br> versione - versione di hello runbook per il proprio rilevamento. |


## <a name="automation-jobs"></a>Processi di Automazione
Quando si avvia un runbook in Automazione di Azure, viene creato un processo di automazione.  È possibile aggiungere un'automazione processo risorse tooyour soluzione tooautomatically-inizio un runbook quando la soluzione di gestione hello è installata.  Questo metodo è runbook toostart utilizzati in genere utilizzati per la configurazione iniziale della soluzione hello.  creare un runbook a intervalli regolari, toostart un [pianificazione](#schedules) e [pianificazione del processo](#job-schedules)

Risorse di processo hanno un tipo di **Microsoft.Automation/automationAccounts/jobs** e hello seguente struttura.  Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello. 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

in hello nella tabella seguente vengono descritte le proprietà di Hello per processi di automazione.

| Proprietà | Descrizione |
|:--- |:--- |
| runbook |Entità di un nome singolo con nome hello di hello runbook toostart. |
| parameters |Entità per ogni valore di parametro richiesto da runbook hello. |

il processo di Hello include il nome del runbook hello e qualsiasi toobe di valori di parametro inviati toohello runbook.  processo Hello deve [dipendono](operations-management-suite-solutions-solution-file.md#resources) hello runbook che viene avviato dall'hello runbook, è necessario creare prima il processo di hello.  Se sono presenti più runbook da avviare, è possibile definire l'ordine di avvio impostando un processo in modo che dipenda da un altro processo che deve essere eseguito prima.

nome Hello di una risorsa di processo deve contenere un GUID che viene in genere assegnato da un parametro.  Altre informazioni sui parametri GUID sono disponibili in [Creazione di soluzioni di gestione in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).  


## <a name="certificates"></a>Certificati
[Certificati di automazione di Azure](../automation/automation-certificates.md) dispone di un tipo di **Microsoft.Automation/automationAccounts/certificates** e hello seguente struttura. Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



Nella hello nella tabella seguente sono descritte le proprietà di Hello per le risorse di certificati.

| Proprietà | Descrizione |
|:--- |:--- |
| base64Value |Valore base 64 hello certificato. |
| thumbprint |Identificazione personale certificato hello. |



## <a name="credentials"></a>Credenziali
[Le credenziali di automazione Azure](../automation/automation-credentials.md) dispone di un tipo di **Microsoft.Automation/automationAccounts/credentials** e hello seguente struttura.  Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello. 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

Nella hello nella tabella seguente sono descritte le proprietà di Hello per le risorse di credenziali.

| Proprietà | Descrizione |
|:--- |:--- |
| userName |Nome utente per le credenziali di hello. |
| password |Password per le credenziali di hello. |


## <a name="schedules"></a>Pianificazioni
[Le pianificazioni di automazione Azure](../automation/automation-schedules.md) dispone di un tipo di **Microsoft.Automation/automationAccounts/schedules** e hello hello seguente struttura. Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

Nella hello nella tabella seguente sono descritte le proprietà di Hello per le risorse di pianificazione.

| Proprietà | Descrizione |
|:--- |:--- |
| description |Descrizione facoltativa per la pianificazione di hello. |
| startTime |Specifica l'ora di inizio hello di una pianificazione come oggetto DateTime. È possibile fornire una stringa se può essere convertito tooa DateTime valido. |
| isEnabled |Specifica se la pianificazione hello è abilitata. |
| interval |tipo di Hello di intervallo per la pianificazione di hello.<br><br>day<br>hour |
| frequency |Frequenza di pianificazione di hello deve generare in numero di ore o giorni. |

Pianifica deve disporre di un'ora di inizio con un valore maggiore di hello ora corrente.  Poiché non è in alcun modo di sapere quando è toobe corso installato, è possibile fornire questo valore con una variabile.

Utilizzare uno dei seguenti due strategie di utilizzo delle risorse di pianificazione in una soluzione hello.

- Usare un parametro per l'ora di inizio hello della pianificazione hello.  Questo richiederà hello utente tooprovide un valore quando installano la soluzione hello.  In caso di più pianificazioni, è possibile usare un unico valore di parametro anche per più di esse.
- Creare pianificazioni hello usando un runbook che inizia quando si installa la soluzione hello.  Ciò consente di rimuovere il requisito di hello di hello utente toospecify non può contenere un'ora, ma si pianificazione hello nella soluzione in modo verrà rimosso quando viene rimossa la soluzione hello.


### <a name="job-schedules"></a>Pianificazioni dei processi
Le risorse "pianificazione dei processi" collegano un runbook a una pianificazione.  Hanno un tipo di **Microsoft.Automation/automationAccounts/jobSchedules** e hello hello seguente struttura.  Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


in hello nella tabella seguente vengono descritte le proprietà di Hello per le pianificazioni dei processi.

| Proprietà | Descrizione |
|:--- |:--- |
| schedule name |Singolo **nome** entità con nome hello della pianificazione di hello. |
| runbook name  |Singolo **nome** entità con nome hello di hello runbook.  |



## <a name="variables"></a>variables
[Le variabili di automazione Azure](../automation/automation-variables.md) dispone di un tipo di **Microsoft.Automation/automationAccounts/variables** e hello seguente struttura.  Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello.

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

Nella hello nella tabella seguente sono descritte le proprietà di Hello per le risorse di variabile.

| Proprietà | Descrizione |
|:--- |:--- |
| description | Descrizione facoltativa per la variabile hello. |
| isEncrypted | Specifica se la variabile hello deve essere crittografata. |
| type | Questa proprietà attualmente non ha alcun effetto.  tipo di dati Hello della variabile hello verrà determinato dal valore iniziale di hello. |
| value | Valore variabile hello. |

> [!NOTE]
> Hello **tipo** proprietà attualmente non ha effetto sulla variabile hello viene creato.  il tipo di dati Hello per variabile hello verrà determinato dal valore hello.  

Se si imposta hello valore iniziale per la variabile di hello, deve essere configurato come tipo di dati corretto hello.  Hello nella tabella seguente fornisce hello diversi tipi di dati consentiti e la relativa sintassi.  Si noti che i valori in JSON sono previsti tooalways essere racchiusi tra virgolette con i caratteri speciali all'interno di virgolette hello.  Ad esempio, sarebbe specificato un valore stringa per le virgolette per racchiudere la stringa hello (utilizzando il carattere di escape hello (\\)) mentre un valore numerico verrà specificato con un set di virgolette.

| Tipo di dati | Descrizione | Esempio | Risolve troppo|
|:--|:--|:--|:--|
| string   | Racchiude il valore tra virgolette doppie.  | "\"Hello world\"" | "Hello world" |
| numeric  | Valore numerico con virgolette singole.| "64" | 64 |
| boolean  | **true** o **false** tra virgolette.  Si noti che questo valore deve essere minuscolo. | "true" | true |
| datetime | Valore di data serializzato.<br>È possibile utilizzare il cmdlet ConvertTo-Json hello in PowerShell toogenerate questo valore per una determinata data.<br>Esempio: get-date "5/24/2017 13:14:57" \| ConvertTo-Json | "\\/Date(1495656897378)\\/" | 2017-05-24 13:14:57 |

## <a name="modules"></a>Moduli
La soluzione di gestione non è necessario toodefine [moduli globali](../automation/automation-integration-modules.md) utilizzato dal runbook, poiché sarà sempre disponibile nell'account di automazione.  È necessario tooinclude una risorsa per qualsiasi altro modulo utilizzato dal runbook.

[I moduli di integrazione](../automation/automation-integration-modules.md) dispone di un tipo di **Microsoft.Automation/automationAccounts/modules** e hello seguente struttura.  Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello.

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


Nella hello nella tabella seguente sono descritte le proprietà di Hello per le risorse di modulo.

| Proprietà | Descrizione |
|:--- |:--- |
| contentLink |Specifica il contenuto di hello del modulo hello. <br><br>URI - Uri toohello contenuto del modulo hello.  Si tratterà di un file con estensione ps1 per i runbook di PowerShell e di script e di un file di runbook grafico esportato per un runbook di Graph.  <br> versione: versione del modulo di hello per il propria rilevamento. |

runbook Hello dovrebbero dipendere hello modulo risorsa tooensure che ha creato prima di hello runbook.

### <a name="updating-modules"></a>Aggiornamento dei moduli
Se si aggiorna una soluzione di gestione che include un runbook che utilizza una pianificazione e hello nuova versione della soluzione ha un nuovo modulo utilizzato dal runbook, runbook hello può utilizzare versione precedente di hello del modulo hello.  Si dovrebbero includere hello seguendo i runbook nella soluzione e toorun un processo prima di eventuali altri runbook.  Ciò garantisce che tutti i moduli vengono aggiornati come hello necessario per i runbook vengono caricati.

* [Aggiornamento ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) verrà verificato che tutti i moduli di hello usati dai runbook nella soluzione siano la versione più recente di hello.  
* [ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) verrà registrare di nuovo tutti hello pianificazione risorse tooensure che hello runbook collegati toothem con moduli di utilizzare hello più recenti.




## <a name="sample"></a>Esempio
Ecco un esempio di una soluzione che includono che include hello seguenti risorse:

- Runbook.  Si tratta di un runbook di esempio archiviato in un repository GitHub pubblico.
- Processo di automazione che avvia runbook hello quando si installa la soluzione hello.
- Pianificazione e processo pianificato toostart hello runbook a intervalli regolari.
- Certificato.
- Credenziali.
- Variabile.
- Modulo.  Si tratta di hello [OMSIngestionAPI modulo](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) per la scrittura di dati tooLog Analitica. 

esempio utilizza Hello [parametri soluzione standard](operations-management-suite-solutions-solution-file.md#parameters) variabili comunemente utilizzati in una soluzione come anziché valori toohardcoding nelle definizioni di risorse hello.


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a>Passaggi successivi
* [Aggiunta di una soluzione di visualizzazione tooyour](operations-management-suite-solutions-resources-views.md) toovisualize raccolti dati.
