---
title: applicazione gestita di Azure aaaConsume | Documenti Microsoft
description: Descrive come un cliente crea un'applicazione gestita di Azure dai file pubblicati.
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a>Usare un'applicazione gestita interna

È possibile usare [applicazioni gestite](managed-application-overview.md) di Azure studiate per i membri della propria organizzazione. È, ad esempio, possibile selezionare applicazioni gestite disponibili dal reparto IT che garantiscano la conformità agli standard aziendali. Queste applicazioni gestite sono disponibili tramite hello catalogo di servizi, non hello Azure Marketplace.

Prima di procedere con questo articolo, è necessario disporre di un'applicazione gestita disponibile nel catalogo di servizi di hello per la sottoscrizione. Se qualcuno nell'organizzazione ha già creato un'applicazione gestita, vedere [Creare e pubblicare un'applicazione gestita di Azure](managed-application-publishing.md).

Attualmente, è possibile utilizzare Azure CLI o hello tooconsume portale Azure un'applicazione gestita.

## <a name="create-hello-managed-application-by-using-hello-portal"></a>Creare un'applicazione hello gestito tramite il portale di hello

toodeploy un'applicazione gestita tramite il portale di hello, seguire questi passaggi:

1. Passare toohello portale di Azure. Cercare **Service Catalog Managed Application** (Applicazione gestita del catalogo di servizi).

   ![Applicazione gestita del catalogo di servizi](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. Seleziona hello gestiti applicazione cui si desidera toocreate dall'elenco di hello delle soluzioni disponibili. Selezionare **Crea**.

   ![Selezione di applicazioni gestite](./media/managed-application-consumption/select-offer.png)

1. Fornire valori per parametri hello risorse hello tooprovision obbligatorio. Selezionare **West Central US** (Stati Uniti centro-occidentali) per il percorso. Selezionare **OK**.

   ![Parametri delle applicazioni gestite](./media/managed-application-consumption/input-parameters.png)

1. modello Hello convalida valori hello specificati. Se la convalida ha esito positivo, selezionare **OK** distribuzione hello toostart.

   ![Convalida dell'applicazione gestita](./media/managed-application-consumption/validation.png)

Al termine della distribuzione di hello, vengono effettuato il provisioning delle risorse appropriate hello definite nel modello hello nel gruppo di risorse gestite hello fornito.

## <a name="create-hello-managed-application-by-using-azure-cli"></a>Creare un'applicazione hello gestito tramite l'interfaccia CLI di Azure

Esistono due modi toocreate un'applicazione gestita tramite l'interfaccia CLI di Azure:

* Comando hello per la creazione di applicazioni gestite.
* Comando distribuzione hello modello regolare.

### <a name="use-hello-template-deployment-command"></a>Comando di distribuzione modello hello

Distribuire file applianceMainTemplate.json hello hello fornitore creato.

Creare quindi due gruppi di risorse. Hello primo gruppo di risorse è dove hello risorse applicazione gestita viene creata: Microsoft.Solutions/appliances. il secondo gruppo di risorse Hello contiene tutte le risorse di hello definite in mainTemplate.json. Questo gruppo di risorse è gestito da hello ISV.

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> Utilizzare `westcentralus` come percorso di hello hello del gruppo di risorse.
>

applianceMainTemplate.json toodeploy in mainResourceGroup, utilizzare hello comando seguente:

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

Dopo aver hello precedenti esecuzioni di modello, viene richiesto per i valori dei parametri definiti nel modello hello hello hello. Inoltre toohello parametri che sono necessarie risorse tooprovision in un modello, sono necessari due valori di parametro della chiave:

- **managedResourceGroupId**: ID di hello gruppo contenitore hello di risorse definiti in applianceMainTemplate.json hello. ID Hello è formato hello `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`. Nel precedente esempio di hello, dell'ID hello del `managedResourceGroup`.
- **applianceDefinitionId**: ID hello di hello gestiti risorsa di definizione dell'applicazione. Questo valore viene fornito da hello ISV.

> [!NOTE]
> publisher Hello deve concedere accesso toohello risorse al gruppo che contiene la definizione di applicazione hello gestito. risorse di definizione Hello viene creata nella sottoscrizione di hello server di pubblicazione. Pertanto, un utente, gruppo di utenti o l'applicazione nel tenant del cliente hello deve risorsa toothis accesso in lettura.

Dopo la distribuzione di hello viene completata correttamente, viene visualizzato hello gestito in mainResourceGroup viene creata l'applicazione. risorsa storageAccount Hello viene creato in managedResourceGroup.

### <a name="use-hello-create-command"></a>Hello utilizzare creare un comando

È possibile utilizzare hello `az managedapp create` comando toocreate un'applicazione gestita da hello gestiti definizione dell'applicazione.

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* **Id di definizione dello strumento**: ID di risorsa hello di hello gestiti creato nel passaggio precedente hello definizione dell'applicazione. tooobtain questo ID, eseguire hello comando seguente:

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  Questo comando restituisce la definizione di applicazione hello gestito. È necessario il valore di hello della proprietà ID hello.

* **rg-id gestito**: nome hello di hello gruppo contenitore hello di risorse definiti in applianceMainTemplate.json. Questo gruppo di risorse è il gruppo di risorse gestite hello. È gestito dal server di pubblicazione hello. Se non esiste, viene creato automaticamente.
* **gruppo di risorse**: viene creato il gruppo di risorse hello in hello gestiti risorsa dell'applicazione. Hello Microsoft.Solutions/appliance risorsa si trova in questo gruppo di risorse.
* **i parametri**: hello parametri che sono necessari per le risorse di hello definite in applianceMainTemplate.json.

## <a name="known-issues"></a>Problemi noti

Questa versione di anteprima include hello seguenti problemi:

* Durante la creazione di un'applicazione hello gestito hello viene visualizzato un errore di 500 interno del server. Se si esegue questo problema, è probabile che toobe intermittenti. Ripetere l'operazione di hello.
* Un nuovo gruppo di risorse è necessaria per il gruppo di risorse gestite hello. Se si utilizza un gruppo di risorse esistente, la distribuzione di hello ha esito negativo.
* Hello gruppo di risorse contenente hello Microsoft.Solutions/appliances risorsa deve essere creato in hello **westcentralus** percorso.

## <a name="next-steps"></a>Passaggi successivi

* Per le applicazioni toomanaged un'introduzione, vedere [panoramica delle applicazioni gestite](managed-application-overview.md).
* Per informazioni sulla pubblicazione di un'applicazione gestita del catalogo di servizi, vedere [Creare e pubblicare un'applicazione gestita del catalogo di servizi](managed-application-publishing.md).
* Per informazioni sulla pubblicazione applicazioni gestite toohello Azure Marketplace, vedere [gestito di Azure le applicazioni in hello Marketplace](managed-application-author-marketplace.md).
* Per informazioni sull'utilizzo di un'applicazione gestita da hello Marketplace, vedere [utilizzare Azure gestite le applicazioni in hello Marketplace](managed-application-consume-marketplace.md).
