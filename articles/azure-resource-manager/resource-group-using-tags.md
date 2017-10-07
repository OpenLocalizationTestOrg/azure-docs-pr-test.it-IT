---
title: aaaTag Azure le risorse per l'organizzazione logica | Documenti Microsoft
description: Viene illustrato come tooapply tag tooorganize Azure risorse per la fatturazione e la gestione.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 003a78e5-2ff8-4685-93b4-e94d6fb8ed5b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: AzurePortal
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tomfitz
ms.openlocfilehash: e07470463d160f8cefe5c80bc91e66a96af6ca45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-tags-tooorganize-your-azure-resources"></a>Utilizzare tag tooorganize le risorse di Azure
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> È possibile applicare tooresources solo tag che supportano le operazioni di gestione risorse di Azure. Se è stato creato una macchina virtuale, una rete virtuale o un account di archiviazione tramite il modello di distribuzione classica hello (ad esempio mediante hello portale di Azure classico), è possibile applicare una risorsa toothat tag. assegnazione di tag, toosupport ridistribuire tali risorse tramite Gestione risorse. Tutte le altre risorse supportano l'assegnazione di tag.
> 
> 

## <a name="policies-for-tag-consistency"></a>Criteri per la coerenza dei tag

È possibile utilizzare regole standard toocreate dei criteri di risorse dell'organizzazione. È possibile creare criteri che garantiscono le risorse sono contrassegnate con i valori appropriati di hello. Per altre informazioni, vedere [Applicare criteri delle risorse per i tag](resource-manager-policy-tags.md).

## <a name="powershell"></a>PowerShell
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

toosee hello tag esistenti per un *gruppo di risorse*, utilizzare:

```azurecli
az group show -n examplegroup --query tags
```

Lo script restituisce hello seguente formato:

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

toosee hello tag esistenti per un *risorsa con un ID di risorsa specificato*, utilizzare:

```azurecli
az resource show --id {resource-id} --query tags
```

In alternativa, toosee hello tag esistenti per un *risorse che dispone di un gruppo di nome e tipo di risorsa specificato*, utilizzare:

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

gruppi di risorse tooget che dispongono di un tag specifico, utilizzare `az group list`:

```azurecli
az group list --tag Dept=IT
```

utilizzare tutte le risorse di hello con un tag specifico e un valore, tooget `az resource list`:

```azurecli
az resource list --tag Dept=Finance
```

Ogni volta che si applica tag tooa risorsa o un gruppo di risorse, sovrascrivere i tag esistenti hello su tale risorsa o un gruppo di risorse. Pertanto, è necessario utilizzare un approccio diverso in base a se hello risorsa o il gruppo dispone di tag esistenti. 

tooadd tag tooa *gruppo di risorse senza i tag esistenti*, utilizzare:

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

tooadd tag tooa *risorsa senza i tag esistenti*, utilizzare:

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

tooadd tag tooa risorse che dispone già di tag, recuperare i tag esistenti hello, tale valore consente di riformattare e riapplicare tag nuove ed esistenti di hello: 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

tooapply tutti i tag da un gruppo tooits di risorse, e *non mantenere i tag esistenti risorse hello*, utilizzare hello lo script seguente:

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    az resource tag --tags $t --id $resid
  done 
done
```

tooapply tutti i tag da un gruppo tooits di risorse, e *preservare i tag esistenti risorse*, utilizzare hello lo script seguente:

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    jsonrtag=$(az resource show --id $resid --query tags)
    rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
    az resource tag --tags $t$rt --id $resid
  done 
done
```


## <a name="templates"></a>Modelli

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a>di Microsoft Azure
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a>API REST
Hello portale di Azure e PowerShell utilizzare hello [REST API di gestione risorse](https://docs.microsoft.com/rest/api/resources/) background hello. Se è necessario toointegrate tag in un altro ambiente, è possibile ottenere i tag con **ottenere** hello risorse ID e aggiornamento hello set di tag usando un **PATCH** chiamare.

## <a name="tags-and-billing"></a>Tag e fatturazione
È possibile utilizzare tag toogroup i dati di fatturazione. Ad esempio, se si eseguono più macchine virtuali per le organizzazioni diverse, è possibile utilizzare hello tag toogroup utilizzo dal centro di costo. È anche possibile utilizzare tag toocategorize costi dall'ambiente di runtime, quali l'utilizzo della fatturazione hello per le macchine virtuali in esecuzione nell'ambiente di produzione hello.


È possibile recuperare informazioni sui tag tramite hello [utilizzo delle risorse di Azure e RateCard APIs](../billing/billing-usage-rate-card-overview.md) o hello utilizzo con valori delimitati da virgole (CSV) file. Si scarica il file di utilizzo hello da hello [portale per gli account Azure](https://account.windowsazure.com/) o [portale EA](https://ea.azure.com). Per ulteriori informazioni sulla toobilling accesso a livello di codice, vedere [ottenere informazioni approfondite del consumo di risorse di Microsoft Azure](../billing/billing-usage-rate-card-overview.md). Per le operazioni API REST, vedere [Riferimento API REST alla fatturazione di Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).


Quando si scarica utilizzo hello CSV per i servizi che supportano i tag con fatturazione, tag di hello vengono visualizzati in hello **tag** colonna. Per altre informazioni, vedere [Comprendere la fattura per Microsoft Azure](../billing/billing-understand-your-bill.md).

![Vedere i tag della fatturazione](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a>Passaggi successivi
* È possibile applicare restrizioni e convenzioni all'interno della sottoscrizione tramite criteri personalizzati. Un criterio che è stato definito potrebbe richiedere che per tutte le risorse sia impostato un determinato tag. Per ulteriori informazioni, vedere [utilizzare criteri toomanage risorse e controllare l'accesso](resource-manager-policy.md).
* Per un toousing introduzione di Azure PowerShell quando si distribuisce le risorse, vedere [tramite Azure PowerShell con Azure Resource Manager](powershell-azure-resource-manager.md).
* Per un hello toousing introduzione CLI di Azure quando si distribuisce le risorse, vedere [Using hello CLI di Azure per Mac, Linux e Windows con Gestione risorse di Azure](xplat-cli-azure-resource-manager.md).
* Per un portale di hello toousing introduzione, vedere [Using hello toomanage portale Azure le risorse di Azure](resource-group-portal.md).  
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).

