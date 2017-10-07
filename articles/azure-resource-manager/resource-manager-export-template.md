---
title: modello di Azure Resource Manager aaaExport | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure tooexport un modello da un gruppo di risorse esistente.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a>Esportare un modello di Azure Resource Manager da risorse esistenti
In questo articolo viene illustrato come tooexport un modello di gestione risorse da risorse esistenti nella sottoscrizione. È possibile utilizzare tale toogain modello generato una migliore comprensione della sintassi dei modelli.

Esistono due modi tooexport un modello:

* È possibile esportare hello **modello effettivo utilizzato per la distribuzione**. modello esportato Hello include tutti i parametri di hello e variabili, esattamente come appaiono nel modello originale hello. Questo approccio è utile per la distribuzione di risorse tramite il portale di hello e desidera toosee hello modello toocreate tali risorse. Il modello è immediatamente utilizzabile. 
* È possibile esportare un **generato modello che rappresenta lo stato corrente di hello hello del gruppo di risorse**. modello esportato Hello non è basato su qualsiasi modello utilizzato per la distribuzione. Al contrario, viene creato un modello che è uno snapshot hello del gruppo di risorse. modello esportato Hello molti valori hardcoded e probabilmente non tutti i parametri in genere è possibile definire. Questo approccio è utile quando è stato modificato il gruppo di risorse hello dopo la distribuzione. Il modello richiede in genere modifiche prima di poter essere usato.

Questo argomento vengono illustrati entrambi gli approcci tramite il portale di hello.

## <a name="deploy-resources"></a>Distribuire le risorse
Iniziamo distribuendo tooAzure risorse che è possibile utilizzare per l'esportazione come modello. Se si dispone già di un gruppo di risorse nella sottoscrizione che si desidera tooexport tooa modello, è possibile ignorare questa sezione. resto Hello di questo articolo si presuppone che è stato distribuito hello web app e soluzioni di database SQL illustrate in questa sezione. Se si utilizza una soluzione diversa, l'esperienza potrebbe essere leggermente diversa, ma i passaggi di hello tooexport un modello sono hello stesso. 

1. In hello [portale di Azure](https://portal.azure.com)selezionare **New**.
   
      ![Selezionare Nuovo](./media/resource-manager-export-template/new.png)
2. Cercare **web app + SQL** e selezionare le opzioni disponibili hello.
   
      ![Cercare App Web e SQL](./media/resource-manager-export-template/webapp-sql.png)

3. Selezionare **Crea**.

      ![Selezionare Crea](./media/resource-manager-export-template/create.png)

4. Fornire valori hello necessario per hello web app e il database SQL. Selezionare **Crea**.

      ![Specificare i valori per Web e SQL](./media/resource-manager-export-template/provide-web-values.png)

distribuzione di Hello potrebbe richiedere un minuto. Al termine della distribuzione di hello, la sottoscrizione contiene la soluzione hello.

## <a name="view-template-from-deployment-history"></a>Visualizzare il modello dalla cronologia delle distribuzioni
1. Andare a pannello di gruppo di risorse toohello per il nuovo gruppo di risorse. Si noti che pannello hello illustra il risultato di hello dell'ultima distribuzione hello. Selezionare questo collegamento.
   
      ![pannello Gruppo di risorse](./media/resource-manager-export-template/select-deployment.png)
2. Visualizzare una cronologia delle distribuzioni per il gruppo di hello. Il caso, il pannello hello Elenca probabilmente solo una distribuzione. Selezionare questa distribuzione.
   
     ![ultima distribuzione](./media/resource-manager-export-template/select-history.png)
3. Pannello Hello Visualizza un riepilogo della distribuzione hello. Hello riepilogo include stato hello della distribuzione di hello e relativi valori di hello forniti per i parametri e operazioni. modello di hello toosee utilizzato per la distribuzione di hello, seleziona **modello di visualizzazione**.
   
     ![visualizzare il riepilogo della distribuzione](./media/resource-manager-export-template/view-template.png)
4. Gestione risorse recupera hello i seguenti sette file automaticamente:
   
   1. **Modello** -modello hello che definisce l'infrastruttura di hello per la soluzione. Durante la creazione di account di archiviazione hello tramite il portale di hello, Gestione risorse utilizzato toodeploy un modello e salvato il modello per riferimento futuro.
   2. **I parametri** -un file di parametri che è possibile usare nei valori toopass durante la distribuzione. Contiene valori hello forniti durante la distribuzione prima di hello. È possibile modificare questi valori quando si ridistribuisce il modello di hello.
   3. **CLI** -file script di Azure un'interfaccia di riga comando (CLI) che è possibile utilizzare il modello di hello toodeploy.
   3. **2.0 CLI** -file script di Azure un'interfaccia di riga comando (CLI) che è possibile utilizzare il modello di hello toodeploy.
   4. **PowerShell** -file di script di PowerShell di Azure che è possibile utilizzare il modello di hello toodeploy.
   5. **.NET** -classe di oggetto .NET che è possibile utilizzare il modello di hello toodeploy.
   6. **Ruby** -classe A Ruby che è possibile utilizzare il modello di hello toodeploy.
      
      file Hello sono disponibili tramite i collegamenti tra blade hello. Per impostazione predefinita, il pannello hello Visualizza modello hello.
      
       ![Visualizza modello](./media/resource-manager-export-template/see-template.png)
      
Questo modello è modello effettivo hello utilizzato toocreate l'app web e database SQL. Si noti che contiene i parametri che consentono di valori diversi tooprovide durante la distribuzione. toolearn ulteriori informazioni su struttura hello di un modello, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).

## <a name="export-hello-template-from-resource-group"></a>Esportare il modello di hello dal gruppo di risorse
Se si manualmente hanno modificato le risorse o aggiunta di risorse in più distribuzioni, il recupero di un modello dalla cronologia della distribuzione di hello non riflette lo stato corrente di hello hello del gruppo di risorse. In questa sezione viene illustrato come un modello che rispecchia tooexport hello stato corrente del gruppo di risorse hello. 

> [!NOTE]
> Non è possibile esportare un modello per un gruppo di risorse con più di 200 risorse.
> 
> 

1. modello di hello tooview per un gruppo di risorse, seleziona **script di automazione**.
   
      ![esportare un gruppo di risorse](./media/resource-manager-export-template/select-automation.png)
   
     Gestione risorse analizza hello le risorse nel gruppo di risorse hello e genera un modello per tali risorse. Non tutti i tipi di risorse supportano la funzione di modello di esportazione hello. Potrebbe essere visualizzato un errore che informa che si è verificato un problema con l'esportazione di hello. Si apprenderà come toohandle tali problemi nel hello [esportazione problemi](#fix-export-issues) sezione.
2. Vedrai nuovamente sei file hello che è possibile utilizzare soluzioni hello tooredeploy. Tuttavia, questo modello in fase di hello è leggermente diverso. Si noti che il modello hello generato contiene meno parametri di modello hello nella sezione precedente. Inoltre, molti dei valori di hello (ad esempio, percorso e i valori di SKU) sono hardcoded in questo modello, piuttosto che accetta un valore di parametro. Prima di riutilizzare questo modello, è opportuno tooedit hello modello toomake migliorare l'utilizzo di parametri. 
   
3. Sono disponibili due opzioni per la continuazione toowork con questo modello. È possibile scaricare il modello di hello e lavorare localmente su di esso con un editor di JSON. In alternativa, è possibile salvare hello modello tooyour raccolta e il lavoro tramite il portale di hello.
   
     Se si ha familiarità con un editor di JSON come [Visual Studio Code](https://code.visualstudio.com/) o [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), è preferibile scaricare modello hello in locale e utilizzare tale editor. toowork in locale, selezionare **scaricare**.
   
      ![scaricare il modello](./media/resource-manager-export-template/download-template.png)
   
     Se non è configurato con un editor di JSON, è preferibile modificare hello modello tramite il portale di hello. resto Hello di questo argomento si presuppone che è stato salvato libreria tooyour di hello modelli nel portale di hello. Tuttavia, si apportano hello stesso modello toohello modifiche di sintassi se si lavora in locale con un editor di JSON o tramite il portale di hello. Selezionare toowork tramite il portale di hello **aggiungere toolibrary**.
   
      ![aggiungere toolibrary](./media/resource-manager-export-template/add-to-library.png)
   
     Quando si aggiunge una raccolta di modelli di toohello, assegnare il modello di hello un nome e una descrizione. Selezionare quindi **Salva**.
   
     ![impostare i valori di modello](./media/resource-manager-export-template/save-library-template.png)
4. tooview un modello salvato nella libreria, selezionare **più servizi**, tipo **modelli** toofilter risultati, selezionare **modelli**.
   
      ![trovare i modelli](./media/resource-manager-export-template/find-templates.png)
5. Selezionare il modello di hello con nome hello che è stato salvato.
   
      ![selezionare modello](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a>Personalizzare il modello di hello
funzionamento del modello Hello esportata correttamente che se si desidera toocreate hello stesso web app e il database SQL per ogni distribuzione. Le opzioni disponibili in Resource Manager consentono, tuttavia, di distribuire modelli con maggiore flessibilità. Questo articolo illustra come parametri tooadd per hello database password e nome di amministratore. È possibile utilizzare questo stesso tooadd approccio una maggiore flessibilità per gli altri valori nel modello di hello.

1. modello di hello toocustomize, selezionare **modifica**.
   
     ![visualizzare il modello](./media/resource-manager-export-template/select-edit.png)
2. Selezionare il modello di hello.
   
     ![modificare un modello](./media/resource-manager-export-template/select-added-template.png)
3. i valori hello in grado di toopass toobe che è possibile toospecify durante la distribuzione, aggiungere hello seguenti due parametri toohello **parametri** sezione nel modello hello:

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. nuovi parametri hello toouse, sostituire la definizione di hello SQL server in hello **risorse** sezione. Si noti che in **administratorLogin** e **administratorLoginPassword** vengono ora usati valori di parametro.

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. Selezionare **OK** al termine modifica modello hello.
7. Selezionare **salvare** modello toohello di toosave hello le modifiche.
   
     ![salvare il modello](./media/resource-manager-export-template/save-template.png)
8. modello di hello aggiornato tooredeploy, selezionare **Distribuisci**.
   
     ![distribuire un modello](./media/resource-manager-export-template/redeploy-template.png)
9. Fornire i valori dei parametri e selezionare un gruppo toodeploy hello di risorse per.


## <a name="fix-export-issues"></a>Risolvere i problemi di esportazione
Non tutti i tipi di risorse supportano la funzione di modello di esportazione hello. Questo problema, manualmente tooresolve aggiungere risorse mancanti hello nuovamente nel modello. messaggio di errore Hello include i tipi di risorsa hello che non possono essere esportati. Trovare il tipo di risorsa nelle [informazioni di riferimento sui modelli](/azure/templates/). Ad esempio, di aggiungere un gateway di rete virtuale, vedere toomanually [riferimento a un modello Microsoft.Network/virtualNetworkGateways](/azure/templates/microsoft.network/virtualnetworkgateways).

> [!NOTE]
> Si verificano problemi di esportazione solo quando si esporta da un gruppo di risorse invece che dalla cronologia della distribuzione. Se l'ultima distribuzione in modo accurato rappresenta lo stato corrente di hello hello del gruppo di risorse, è necessario esportare il modello di hello dalla cronologia della distribuzione hello anziché dal gruppo di risorse hello. Esportare solo da un gruppo di risorse quando sono state apportate gruppo di risorse toohello modifiche che non sono definiti in un unico modello.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Si è appreso come tooexport un modello dalle risorse di cui è stato creato nel portale di hello.

* È possibile distribuire un modello tramite [PowerShell](resource-group-template-deploy.md), l'[interfaccia della riga di comando di Azure](resource-group-template-deploy-cli.md) o l'[API REST](resource-group-template-deploy-rest.md).
* toosee tooexport un modello tramite PowerShell, vedere [tramite Azure PowerShell con Azure Resource Manager](powershell-azure-resource-manager.md).
* toosee tooexport un modello tramite l'interfaccia CLI di Azure, vedere [hello utilizzare CLI di Azure per Mac, Linux e Windows con Gestione risorse di Azure](xplat-cli-azure-resource-manager.md).

