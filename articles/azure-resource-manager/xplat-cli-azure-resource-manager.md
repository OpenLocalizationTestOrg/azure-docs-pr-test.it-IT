---
title: risorse aaaManage con hello CLI di Azure | Documenti Microsoft
description: Utilizzare hello Azure interfaccia della riga di comando (CLI) toomanage Azure risorse e dei gruppi
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a>Utilizzare toomanage CLI di Azure hello Azure le risorse e gruppi di risorse
> [!div class="op_single_selector"]
> * [Portale](resource-group-portal.md) 
> * [Interfaccia della riga di comando di Azure](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [API REST](resource-manager-rest-api.md)
> 
> 

Hello interfaccia della riga di comando di Azure (Azure CLI) è uno dei vari strumenti è possibile utilizzare toodeploy e gestire le risorse con Gestione risorse. Questo articolo descrive toomanage modi comuni Azure le risorse e gruppi di risorse utilizzando hello CLI di Azure in modalità di gestione risorse. Per informazioni sull'utilizzo delle risorse di toodeploy hello CLI, vedere [distribuire le risorse con i modelli di gestione risorse e CLI di Azure](resource-group-template-deploy-cli.md). Per informazioni generali sulle risorse di Azure e Gestione risorse, visitare hello [Panoramica di gestione risorse di Azure](resource-group-overview.md).

> [!NOTE]
> toomanage Azure le risorse con hello CLI di Azure, è necessario troppo[installare hello Azure CLI](../cli-install-nodejs.md), e [Accedi tooAzure](../xplat-cli-connect.md) utilizzando hello `azure login` comando. Assicurarsi hello che CLI è in modalità di gestione risorse (eseguire `azure config mode arm`). Se aver eseguito queste operazioni, è possibile toogo pronto.
> 
> 

## <a name="get-resource-groups-and-resources"></a>Ottenere le risorse e i gruppi di risorse
### <a name="resource-groups"></a>Gruppi di risorse
tooget un elenco di tutti i gruppi di risorse nella sottoscrizione e i relativi percorsi, eseguire questo comando.

    azure group list


### <a name="resources"></a>Risorse
 nome di tutte le risorse in un gruppo, ad esempio un oggetto con toolist *testRG*, utilizzare hello comando seguente:

    azure resource list testRG

una singola risorsa all'interno di un gruppo di hello, ad esempio una macchina virtuale denominata tooview *MyUbuntuVM*, utilizzare un comando simile hello seguente:

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

Hello preavviso **Microsoft.Compute/virtualMachines** parametro. Questo parametro indica il tipo di hello della risorsa hello su che si siano richiedendo informazioni.

> [!NOTE]
> Quando si utilizza hello **risorse di azure** comandi diversi dai hello **elenco** comando, è necessario specificare una versione di hello API di risorsa hello con hello **-o** parametro. In caso di dubbi sulla versione di hello API, consultare il file di modello hello e trovare il campo apiVersion hello per risorse hello. Per altre informazioni sulle versioni dell'API in Resource Manager, vedere [Provider e tipi di risorse](resource-manager-supported-services.md).
> 
> 

Quando si visualizzano i dettagli su una risorsa, è spesso utile toouse hello `--json` parametro. Questo parametro consente di hello output più leggibile, perché alcuni valori sono strutture annidate o raccolte. esempio Hello illustra la restituzione di risultati hello di hello **Mostra** comando come un documento JSON.

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> Se si desidera, salvare hello JSON dati toofile tramite hello &gt; tooa di output di caratteri toodirect hello. ad esempio:
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a>Tag
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a>Gestire risorse
tooadd una risorsa, ad esempio un gruppo di risorse tooa account di archiviazione, eseguire un comando simile a:

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

Inoltre toospecifying hello versione dell'API di risorsa hello con hello **-o** parametro, utilizzare hello **-p** toopass JSON in formato stringa del parametro con le necessarie o proprietà aggiuntive.

toodelete una risorsa esistente, ad esempio una risorsa di macchina virtuale, utilizzare un comando simile hello seguente:

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

esistente toomove gruppo di risorse tooanother risorse o una sottoscrizione, utilizzare hello **dello spostamento delle risorse azure** comando. Hello seguente esempio viene illustrato come toomove Cache Redis tooa nuovo gruppo di risorse. In hello **-i** parametro, fornire un elenco delimitato da virgole di toomove dell'id di risorsa hello.

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a>Controllo accesso tooresources
È possibile utilizzare hello Azure CLI toocreate e gestire criteri toocontrol accedere tooAzure alle risorse. Per informazioni generali sulle definizioni dei criteri e tooresources l'assegnazione di criteri, vedere [utilizzare criteri toomanage risorse e controllare l'accesso](resource-manager-policy.md).

Ad esempio, definire hello seguente criteri toodeny tutte le richieste in cui si non trova Stati Uniti occidentali o North Central US e salvarlo toohello criteri definizione file policy.json:

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

Eseguire quindi hello **creare una definizione di criteri** comando:

    azure policy definition create MyPolicy -p c:\temp\policy.json

Questo comando Mostra il seguente toohello simili di output:

    + Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy

    data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny

 un criterio nell'ambito di hello desiderato, utilizzare hello tooassign **PolicyDefinitionId** restituito dal comando precedente hello. Nell'esempio seguente di hello, questo ambito è sottoscrizione hello, ma è possibile definire l'ambito tooresource gruppi o singole risorse:

    azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/

È possibile ottenere, modificare o rimuovere le definizioni dei criteri utilizzando hello **Mostra definizione criteri**, **set di definizione dei criteri**, e **definizione dei criteri di eliminazione** comandi.

Allo stesso modo, è possibile ottenere, modificare o rimuovere le assegnazioni di criteri con hello **Mostra assegnazione criteri**, **set assegnazione criteri**, e **eliminare l'assegnazione dei criteri** comandi .

## <a name="export-a-resource-group-as-a-template"></a>Esportare un gruppo di risorse come modello
Per un gruppo di risorse esistente, è possibile visualizzare il modello di gestione risorse hello per il gruppo di risorse hello. Esportazione modello hello offre due vantaggi:

1. È possibile automatizzare facilmente le distribuzioni future di soluzione hello perché tutta l'infrastruttura hello è definito nel modello di hello.
2. È possibile acquisire familiarità con la sintassi dei modelli esaminando hello JSON che rappresenta la soluzione.

Utilizza hello CLI di Azure, è possibile esportare un modello che rappresenta lo stato corrente di hello del gruppo di risorse, o scaricare il modello di hello che è stato utilizzato per una particolare distribuzione.

* **Esportare il modello di hello per un gruppo di risorse** -ciò risulta utile quando il gruppo di risorse tooa le modifiche apportate e necessario tooretrieve hello rappresentazione JSON del relativo stato corrente. Modello generato hello contiene tuttavia solo un numero minimo di parametri e non variabili. La maggior parte dei valori hello hello modello sono hardcoded. Prima di distribuire il modello di hello generato, è preferibile tooconvert più valori hello nei parametri in modo da personalizzare la distribuzione di hello per ambienti diversi.
  
    modello di hello tooexport per una risorsa gruppo tooa directory locale, eseguire hello `azure group export` comando come illustrato nell'esempio seguente hello. Usare una directory locale appropriata per l'ambiente del sistema operativo in uso.
  
        azure group export testRG ~/azure/templates/
* **Scaricare il modello di hello per una particolare distribuzione** -questo è utile quando è necessario tooview hello modello effettivo che è stato utilizzato toodeploy risorse. modello di Hello include tutti i parametri e variabili definite per la distribuzione originale hello. Tuttavia, se un utente nell'organizzazione apportate gruppo di risorse toohello le modifiche apportate all'esterno di definizione hello nel modello di hello, questo modello non rappresenta lo stato corrente di hello hello del gruppo di risorse.
  
    modello di hello toodownload utilizzato per una particolare tooa locale directory di distribuzione, eseguire hello `azure group deployment template download` comando. ad esempio:
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> La funzionalità di esportazione del modello è disponibile in anteprima e non tutti i tipi di risorse supportano attualmente l'esportazione di un modello. Durante il tentativo di tooexport un modello, si verifichi un errore che indica che alcune risorse non sono state esportate. Se necessario, definire manualmente queste risorse nel modello dopo averlo scaricato.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* Dettagli tooget delle operazioni di distribuzione e risolvere gli errori di distribuzione con hello CLI di Azure, vedere [per visualizzare le operazioni di distribuzione](resource-manager-deployment-operations.md).
* Se si desidera toouse hello CLI tooset risorse tooaccess script o da un'applicazione, vedere [toocreate CLI di Azure di utilizzare un'entità servizio tooaccess risorse](resource-group-authenticate-service-principal-cli.md).
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).

