---
title: gli eventi aaaCustom per griglia di eventi di Azure | Documenti Microsoft
description: Utilizzare toopublish griglia di eventi di Azure un argomento e sottoscrizione evento toothat.
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 5055df1c970b043cadf06978a076f7f5c83501cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a>Creare e instradare eventi personalizzati con la griglia di eventi di Azure

Azure griglia di eventi è un servizio di gestione degli eventi per il cloud hello. In questo articolo, utilizzare hello Azure CLI toocreate un argomento personalizzato, sottoscrizione toohello argomento e attivare i risultati di hello evento tooview hello. In genere, si inviano endpoint tooan gli eventi che risponde a eventi toohello, ad esempio, un webhook o una funzione di Azure. Tuttavia, toosimplify in questo articolo, si invia hello eventi tooa URL che raccoglie solo i messaggi hello. L'URL viene creato con [RequestBin](https://requestb.in/), uno strumento open source di terze parti.

>[!NOTE]
>**RequestBin** è uno strumento open source non destinato all'utilizzo a velocità effettiva elevata. uso di Hello dello strumento di hello qui è puramente dimostrativo. Se si esegue il push più di un evento alla volta, potrebbe non visualizza tutti gli eventi dello strumento hello.

Al termine, vedrai che i dati dell'evento hello sono stati inviati tooan endpoint.

![Dati dell'evento](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo articolo richiede che si eseguono più recente di Azure CLI hello (2.0.14 o versione successiva). versione di hello toofind, eseguire `az --version`. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0](/cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Gli argomenti della griglia di eventi sono risorse di Azure e devono essere inseriti in un gruppo di risorse di Azure. gruppo di risorse Hello è una raccolta logica in cui Azure le risorse vengono distribuite e gestite.

Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando. 

esempio Hello crea un gruppo di risorse denominato *gridResourceGroup* in hello *westus2* percorso.

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a>Creare un argomento personalizzato

Un argomento fornisce un endpoint definito dall'utente in cui vengono pubblicati gli eventi. Hello esempio seguente crea argomento hello nel gruppo di risorse. Sostituire `<topic_name>` con un nome univoco per l'argomento. nome dell'argomento Hello deve essere univoco perché viene rappresentata da una voce DNS. Per la versione di anteprima hello griglia eventi supporta **westus2** e **westcentralus** percorsi.

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a>Creare un endpoint del messaggio

Prima di sottoscrizione toohello argomento, creare endpoint hello per il messaggio di evento hello. Anziché scrivere eventi toohello toorespond di codice, creare un endpoint che raccoglie i messaggi hello, pertanto è possibile visualizzarli. RequestBin è un'open source, strumento di terze parti che consente di toocreate un endpoint e visualizza le richieste inviate tooit. Andare troppo[RequestBin](https://requestb.in/), fare clic su **creare un RequestBin**.  Copiare l'URL bin hello, perché necessaria per la sottoscrizione toohello argomento.

## <a name="subscribe-tooa-topic"></a>La sottoscrizione di argomento tooa

L'iscrizione tooa argomento tootell griglia eventi gli eventi che si desidera tootrack. Hello esempio sottoscrive toohello argomento è stato creato e passa l'URL di hello da RequestBin come endpoint hello la notifica dell'evento. Sostituire `<event_subscription_name>` con un nome univoco per la sottoscrizione, e `<URL_from_RequestBin>` con valore hello hello precedente sezione. Se si specifica un endpoint per la sottoscrizione, griglia eventi gestisce hello routing dell'endpoint toothat eventi. Per `<topic_name>`, utilizzare il valore di hello creato in precedenza. 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a>Inviare un argomento dell'evento tooyour

A questo punto, si attivano toosee un evento come evento griglia distribuisce endpoint tooyour di messaggio hello. In primo luogo, è ora possibile ottenere l'URL di hello e la chiave per l'argomento hello. Usare ancora una volta il nome dell'argomento per `<topic_name>`.

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

toosimplify questo articolo è stata configurata toosend toohello argomento dell'esempio evento dati. In genere, un'applicazione o servizio di Azure invierebbe dati dell'evento hello. Hello di esempio seguente ottiene i dati dell'evento hello:

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

Se si `echo "$body"` è possibile visualizzare eventi completo hello. Hello `data` elemento di hello JSON è payload hello dell'evento. Questo campo accetta qualsiasi JSON ben formato. È inoltre possibile utilizzare il campo di soggetto hello per il routing e il filtro avanzato.

CURL è una utilità che esegue richieste HTTP. In questo articolo, utilizziamo argomento tooour dell'evento CURL toosend hello. 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

Si have attivato l'evento hello e griglia di eventi inviati endpoint di toohello messaggio hello che è configurato per la sottoscrizione. Sfoglia toohello RequestBin URL creato in precedenza. In alternativa, fare clic su Aggiorna nel browser di RequestBin aperto. Viene visualizzato l'evento di hello che appena stata inviata. 

```json
[{
  "id": "1807",
  "eventType": "recordInserted",
  "subject": "myapp/vehicles/motorcycles",
  "eventTime": "2017-08-10T21:03:07+00:00",
  "data": {
    "make": "Ducati",
    "model": "Monster"
  },
  "topic": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/topics/{topic}"
}]
```

## <a name="clean-up-resources"></a>Pulire le risorse
Se si prevede di utilizzo di questo evento toocontinue, non eseguire la pulizia delle risorse di hello create in questo articolo. Se non si prevede toocontinue, utilizzare hello seguendo le risorse di hello toodelete comando che è stato creato in questo articolo.

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a>Passaggi successivi

Ora che è stato appreso come toocreate argomenti e sottoscrizioni di eventi, ulteriori informazioni su quali griglia di eventi consente di eseguire:

- [Informazioni sulla griglia di eventi](overview.md)
- [Monitorare le modifiche alla macchina virtuale con la griglia di eventi di Azure e le app per la logica](monitor-virtual-machine-changes-event-grid-logic-app.md)
