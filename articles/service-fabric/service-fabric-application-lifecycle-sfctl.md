---
title: applicazioni Azure Service Fabric aaaManage utilizzando Azure Service Fabric CLI
description: Informazioni su come toodeploy e rimuovere le applicazioni da un'infrastruttura di Azure del servizio cluster tramite CLI di Azure Service Fabric
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: d9f98cee1d70f71a2aab68ff556956619910e4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a>Gestire un'applicazione di Azure Service Fabric usando l'interfaccia della riga di comando di Azure Service Fabric

Informazioni su come toocreate ed eliminare le applicazioni in esecuzione in un cluster di Azure Service Fabric.

## <a name="prerequisites"></a>Prerequisiti

* Installare l'interfaccia della riga di comando di Service Fabric. Selezionare il cluster Service Fabric. Per altre informazioni, vedere [Introduzione all'interfaccia della riga di comando di Service Fabric](service-fabric-cli.md).

* Disporre di un Service Fabric applicazione pacchetto pronto toobe distribuito. Per ulteriori informazioni su come tooauthor e un'applicazione, pacchetto conoscenza hello [il modello di applicazione di Service Fabric](service-fabric-application-model.md).

## <a name="overview"></a>Panoramica

toodeploy una nuova applicazione, completare questi passaggi:

1. Caricare un archivio immagini di Service Fabric toohello di pacchetto di applicazione.
2. Eseguire il provisioning di un tipo di applicazione.
3. Specificare e creare un'applicazione.
4. Specificare e creare i servizi.

tooremove un'applicazione esistente, completare questi passaggi:

1. Eliminare un'applicazione hello.
2. Hello annullamento del provisioning è associato il tipo di applicazione.
3. Eliminare il contenuto di hello image store.

## <a name="deploy-a-new-application"></a>Distribuire un'applicazione nuova

toodeploy una nuova applicazione hello completo seguenti attività:

### <a name="upload-a-new-application-package-toohello-image-store"></a>Caricare un nuovo archivio di immagini toohello pacchetto applicazione

Prima di creare un'applicazione, caricare l'archivio immagini di hello applicazione pacchetto toohello Service Fabric.

Ad esempio, se il pacchetto dell'applicazione è in hello `app_package_dir` directory, utilizzare hello seguenti directory hello tooupload di comandi:

```azurecli
sfctl application upload --path ~/app_package_dir
```

Per i pacchetti di applicazione di grandi dimensioni, è possibile specificare hello `--show-progress` opzione toodisplay lo stato di avanzamento hello del caricamento hello.

### <a name="provision-hello-application-type"></a>Tipo di provisioning dell'applicazione hello

Al termine di caricamento di hello, eseguire il provisioning di un'applicazione hello. applicazione hello tooprovision, utilizzare hello comando seguente:

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

valore per Hello `application-type-build-path` hello nome della directory hello in cui è caricato il pacchetto dell'applicazione.

### <a name="create-an-application-from-an-application-type"></a>Creare un'applicazione da un tipo di applicazione

Dopo effettuare il provisioning di un'applicazione hello, utilizzare hello successivo comando tooname e creare l'applicazione:

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

`app-name`è il nome di hello che si desidera toouse per l'istanza dell'applicazione hello. È possibile ottenere parametri aggiuntivi dal manifesto dell'applicazione di cui è stato eseguito il provisioning.

nome dell'applicazione Hello deve iniziare con il prefisso hello `fabric:/`.

### <a name="create-services-for-hello-new-application"></a>Creazione di servizi per la nuova applicazione hello

Dopo aver creato un'applicazione, è possibile creare servizi da un'applicazione hello. Nell'esempio seguente di hello, è creare un nuovo servizio senza stato dall'applicazione. servizi di Hello che è possibile creare da un'applicazione vengono definiti in un manifesto del servizio nel pacchetto di applicazione definito in precedenza hello.

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a>Verificare l'integrità e la distribuzione dell'applicazione

tooverify tutto è integro, utilizzare hello seguenti comandi di integrità:

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

tooverify che servizio hello è integro, utilizzare l'integrità di hello tooretrieve comandi simili del servizio hello e l'applicazione:

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

I servizi e le applicazioni integri devono avere il valore `HealthState` impostato su `Ok`.

## <a name="remove-an-existing-application"></a>Rimuovere un'applicazione esistente

tooremove, un'applicazione hello completo seguenti attività:

### <a name="delete-hello-application"></a>Eliminare un'applicazione hello

applicazione hello toodelete, utilizzare hello comando seguente:

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a>Annullare il provisioning di tipo di applicazione hello

Dopo l'eliminazione di un'applicazione hello, è possibile annullare il provisioning di tipo di applicazione hello se non è più necessario. tipo di applicazione hello toounprovision, utilizzare hello comando seguente:

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

Hello tipo nome e tipo di versione deve corrispondere al nome hello e la versione nel manifesto di applicazione definito in precedenza hello.

### <a name="delete-hello-application-package"></a>Eliminare il pacchetto di applicazione hello

Dopo che si dispone di annullamento del provisioning di tipo di applicazione hello, è possibile eliminare il pacchetto di applicazione hello dall'archivio immagini hello se non è più necessario. L'eliminazione di pacchetti di applicazioni consente di recuperare spazio su disco. 

pacchetto di applicazione hello toodelete dall'archivio immagini hello, utilizzare hello comando seguente:

```azurecli
sfctl store delete --content-path app_package_dir
```

`content-path`deve essere hello nome della directory hello caricato durante la creazione di un'applicazione hello.

## <a name="upgrade-application"></a>Aggiornare l'applicazione

Dopo aver creato l'applicazione, è possibile ripetere hello stesso set di passaggi tooprovision una seconda versione dell'applicazione. Quindi, con un aggiornamento dell'applicazione di Service Fabric è possibile passare la seconda versione hello toorunning di un'applicazione hello. Per ulteriori informazioni, vedere la documentazione di hello in [gli aggiornamenti dell'applicazione Service Fabric](service-fabric-application-upgrade.md).

tooperform un aggiornamento, prima effettuare il provisioning hello prossima versione di hello applicazione utilizzando hello comandi stesso come in precedenza:

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

È consigliabile quindi tooperform un aggiornamento automatico monitorato, avviare l'aggiornamento di hello eseguendo hello comando seguente:

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

Gli aggiornamenti eseguono l'override dei parametri esistenti con il set specificato. Parametri dell'applicazione devono essere passati come argomenti toohello del comando di aggiornamento, se necessario. I parametri dell'applicazione devono essere codificati come oggetto JSON.

tooretrieve tutti i parametri specificati in precedenza, è possibile usare hello `sfctl application info` comando.

Quando un aggiornamento dell'applicazione è in corso, lo stato di hello può essere recuperato tramite il `sfctl application upgrade-status` comando.

Infine, se un aggiornamento è in corso e deve toobe annullata, è possibile utilizzare hello `sfctl application upgrade-rollback` tooroll nuovamente hello l'aggiornamento.

## <a name="next-steps"></a>Passaggi successivi

* [Azure Service Fabric command line](service-fabric-cli.md) (Riga di comando di Service Fabric)
* [Introduzione a Service Fabric in Linux](service-fabric-get-started-linux.md)
* [Service Fabric application upgrade](service-fabric-application-upgrade.md) (Aggiornamento di un'applicazione Service Fabric)
