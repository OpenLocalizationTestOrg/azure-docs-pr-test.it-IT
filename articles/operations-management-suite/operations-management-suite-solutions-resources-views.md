---
title: aaaViews nelle soluzioni di gestione di Operations Management Suite (OMS) | Documenti Microsoft
description: "Soluzioni di gestione in Operations Management Suite (OMS) in genere contiene uno o più dati toovisualize viste.  In questo articolo viene descritto come tooexport creata una vista da hello Visualizza finestra di progettazione e includerlo in una soluzione di gestione. "
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 570b278c-2d47-4e5a-9828-7f01f31ddf8c
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 303861465014a27289f831332b3d95925c0ae66d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a>Viste nelle soluzioni di gestione di Operations Management Suite (OMS) (anteprima)
> [!NOTE]
> Questa è una documentazione preliminare per la creazione di soluzioni di gestione in OMS attualmente disponibili in versione di anteprima. Qualsiasi schema descritto di seguito è soggetto toochange.    
>
>

[Soluzioni di gestione in Operations Management Suite (OMS)](operations-management-suite-solutions.md) in genere contiene uno o più dati toovisualize viste.  In questo articolo viene descritto come tooexport una vista creata dal hello [Visualizza finestra di progettazione](../log-analytics/log-analytics-view-designer.md) e includerlo in una soluzione di gestione.  

> [!NOTE]
> Hello esempi in questo articolo utilizzano parametri e variabili che sono entrambe soluzioni toomanagement necessarie o comuni e descritte in [la creazione di soluzioni di gestione in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)
>
>

## <a name="prerequisites"></a>Prerequisiti
Questo articolo si presuppone che si ha già familiarità con come troppo[creare una soluzione di gestione](operations-management-suite-solutions-creating.md) e la struttura di hello di un file di soluzione.

## <a name="overview"></a>Panoramica
tooinclude una vista in una soluzione di gestione, si crea un **risorse** nella hello [file di soluzione](operations-management-suite-solutions-creating.md).  Hello JSON che descrive la configurazione dettagliata della vista hello però in genere complessa e non un valore che è possibile che l'autore di una tipica soluzione deve essere in grado di toocreate manualmente.  metodo più comune Hello è toocreate hello vista utilizzando hello [Visualizza finestra di progettazione](../log-analytics/log-analytics-view-designer.md), esportarlo e quindi aggiungere la soluzione toohello dettagliato della configurazione.

di seguito sono riportati i passaggi di base di Hello tooadd una soluzione di tooa di visualizzazione.  Ogni passaggio è descritto in dettaglio nelle sezioni hello.

1. Esportare hello vista tooa file.
2. Creare la risorsa di una visualizzazione hello nella soluzione di hello.
3. Aggiungere hello vista Dettagli.

## <a name="export-hello-view-tooa-file"></a>Esportare hello vista tooa file
Seguire le istruzioni di hello in [Log Analitica Visualizza finestra di progettazione](../log-analytics/log-analytics-view-designer.md) tooexport un file tooa di visualizzazione.  Hello file esportato verrà essere nel formato JSON con hello stesso [elementi come file di soluzione hello](operations-management-suite-solutions-solution-file.md).  

Hello **risorse** elemento del file di visualizzazione hello avrà una risorsa con un tipo di **Microsoft.OperationalInsights/workspaces** che rappresenta hello area di lavoro OMS.  Questo elemento avrà un sottoelemento con un tipo di **viste** che rappresenta la visualizzazione hello e contiene la configurazione dettagliata.  Copia dettagli hello di questo elemento verrà quindi copiarlo in una soluzione.

## <a name="create-hello-view-resource-in-hello-solution"></a>Creare la risorsa di visualizzazione hello nella soluzione hello
Aggiungere hello seguente Visualizza risorse toohello **risorse** elemento del file di soluzione.  Vengono usate le variabili descritte di seguito, che è necessario aggiungere.  Si noti che hello **Dashboard** e **OverviewTile** proprietà sono segnaposto che vengono sovrascritte con le proprietà corrispondenti di hello dal file di visualizzazione esportata hello.

    {
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
        "type": "Microsoft.OperationalInsights/workspaces/views",
        "location": "[parameters('workspaceregionId')]",
        "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
        "dependson": [
            ],
        "properties": {
            "Id": "[variables('ViewName')]",
            "Name": "[variables('ViewName')]",
            "DisplayName": "[variables('ViewName')]",
            "Description": "",
            "Author": "[variables('ViewAuthor')]",
            "Source": "Local",
            "Dashboard": ,
            "OverviewTile":
        }
    }

Aggiungere hello successivo elemento di variabili toohello variabili hello del file di soluzione e sostituire hello toothose di valori per la soluzione.

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


Si noti che è possibile copiare risorse intera vista hello dal file di visualizzazione esportata, ma è necessario hello toomake dopo le modifiche per tale toowork nella soluzione.  

* Hello **tipo** per Vista hello necessario toobe modificato dalla risorsa **viste** troppo**Microsoft.OperationalInsights/workspaces**.
* Hello **nome** proprietà per la risorsa di visualizzazione hello deve nome area di lavoro di hello tooinclude toobe modificato.
* dipendenza Hello nell'area di lavoro hello deve toobe rimossi dal risorse dell'area di lavoro hello non sono definita nella soluzione hello.
* **DisplayName** proprietà esigenze toobe aggiunto toohello visualizzazione.  Hello **Id**, **nome**, e **DisplayName** deve corrispondere tutti.
* I nomi dei parametri devono essere modificate toomatch hello necessari set di parametri.
* Le variabili devono essere definite nella soluzione hello e utilizzate nelle proprietà di hello appropriato.

## <a name="add-hello-view-details"></a>Aggiungere hello visualizzazione dettagli
risorsa visualizzazione Hello in hello esportata visualizzazione file conterrà due elementi hello **proprietà** elemento denominato **Dashboard** e **OverviewTile** contenenti hello configurazione dettagliata di visualizzazione hello.  Copiare questi due elementi e il relativo contenuto in hello **proprietà** elemento di risorsa vista hello nel file di soluzione.

## <a name="example"></a>Esempio
Ad esempio, hello seguente esempio viene illustrato un file di soluzione semplice con una visualizzazione.  Puntini di sospensione (...) vengono visualizzati per hello **Dashboard** e **OverviewTile** contenuto per motivi di spazio.

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspaceName": {
                "type": "string"
            },
            "accountName": {
                "type": "string"
            },
            "workspaceRegionId": {
                "type": "string"
            },
            "regionId": {
                "type": "string"
            },
            "pricingTier": {
                "type": "string"
            }
        },
        "variables": {
            "SolutionVersion": "1.1",
            "SolutionPublisher": "Contoso",
            "SolutionName": "Contoso Solution",
            "LogAnalyticsApiVersion": "2015-11-01-preview",
            "ViewAuthor":  "user@contoso.com",
            "ViewDescription":  "This is a sample view.",
            "ViewName":  "Contoso View"
        },
        "resources": [
            {
                "name": "[concat(variables('SolutionName'), '(' ,parameters('workspacename'), ')')]",
                "location": "[parameters('workspaceRegionId')]",
                "tags": { },
                "type": "Microsoft.OperationsManagement/solutions",
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "dependsOn": [
                    "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspacename'), '/views/', variables('ViewName'))]"
                ],
                "properties": {
                    "workspaceResourceId": "[concat(resourceGroup().id, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspacename'))]",
                    "referencedResources": [
                    ],
                    "containedResources": [
                        "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/views/', variables('ViewName'))]"
                    ]
                },
                "plan": {
                    "name": "[concat(variables('SolutionName'), '(' ,parameters('workspaceName'), ')')]",
                    "Version": "[variables('SolutionVersion')]",
                    "product": "ContosoSolution",
                    "publisher": "[variables('SolutionPublisher')]",
                    "promotionCode": ""
                }
            },
            {
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
                "type": "Microsoft.OperationalInsights/workspaces/views",
                "location": "[parameters('workspaceregionId')]",
                "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
                "dependson": [
                ],
                "properties": {
                    "Id": "[variables('ViewName')]",
                    "Name": "[variables('ViewName')]",
                    "DisplayName": "[variables('ViewName')]",
                    "Description": "[variables('ViewDescription')]",
                    "Author": "[variables('ViewAuthor')]",
                    "Source": "Local",
                    "Dashboard": ...,
                    "OverviewTile": ...
                }
            }
          ]
    }




## <a name="next-steps"></a>Passaggi successivi
* Leggere le informazioni complete sulla creazione di [soluzioni di gestione](operations-management-suite-solutions-creating.md).
* Includere [runbook di Automazione nella soluzione di gestione](operations-management-suite-solutions-resources-automation.md).
