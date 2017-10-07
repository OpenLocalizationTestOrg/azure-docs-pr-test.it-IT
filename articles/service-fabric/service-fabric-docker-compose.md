---
title: aaaAzure Service Fabric Docker comporre Preview
description: "Azure Service Fabric accetta Docker Compose toomake formato è più facile tooorchestrate i contenitori esistenti usando Service Fabric. Questo supporto è attualmente disponibile in versione di anteprima."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a>Supporto dell'applicazione Docker Compose in Azure Service Fabric (anteprima)

Docker utilizza hello [docker compose.yml](https://docs.docker.com/compose) file per la definizione di un contenitore a più applicazioni. toomake è facile per i clienti familiari con Docker tooorchestrate applicazioni contenitore esistenti in Azure Service Fabric è stato incluso il supporto di anteprima per Docker Compose in modo nativo nella piattaforma hello. Service Fabric può accettare la versione 3 (o successiva) dei file `docker-compose.yml`. 

Poiché questo supporto è disponibile in anteprima, è supportato solo un subset delle direttive Compose. Non sono supportati, ad esempio, gli aggiornamenti dell'applicazione. Tuttavia, è sempre possibile rimuovere e distribuire le applicazioni invece di aggiornarle.

toouse questa anteprima, creare il cluster con la versione 5.7 o versione successiva del runtime di Service Fabric hello tramite hello Azure portal insieme hello corrispondente SDK. 

> [!NOTE]
> Questa funzionalità è in versione di anteprima e non è supportata in produzione.

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a>Distribuire un file Docker Compose in Service Fabric

i comandi seguenti Hello creano un'applicazione di Service Fabric (denominato `fabric:/TestContainerApp` nel precedente esempio hello), che è possibile monitorare e gestire come qualsiasi altra applicazione di Service Fabric. È possibile utilizzare il nome di applicazione specificato hello per le query di integrità.

### <a name="use-powershell"></a>Usare PowerShell

Creare un'applicazione di servizio Fabric comporre da un file docker compose.yml eseguendo hello comando PowerShell seguente:

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

`RegistryUserName`e `RegistryPassword` riferimento toohello contenitore del Registro di sistema username e password. Dopo aver completato un'applicazione hello, è possibile controllare lo stato tramite hello comando seguente:

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

toodelete hello applicazione comporre tramite PowerShell, usare hello comando seguente:

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a>Usare l'interfaccia della riga di comando di Azure Service Fabric (sfctl)

In alternativa, è possibile utilizzare hello comando CLI di infrastruttura del servizio seguente:

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

Dopo aver creato un'applicazione hello, è possibile controllare lo stato tramite hello comando seguente:

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

hello toodelete comporre applicazione, utilizzare hello comando seguente:

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a>Direttive Compose supportate

Questa versione di anteprima supporta un subset di opzioni di configurazione hello dal formato di versione 3 comporre hello, inclusi hello primitive seguenti:

* Services > Deploy > Replicas
* Services > Deploy > Placement > Constraints
* Services > Deploy > Resources > Limits
    * -cpu-shares
    * -memory
    * -memory-swap
* Services > Commands
* Services > Environment
* Services > Ports
* Services > Image
* Services > Isolation (solo per Windows)
* Services > Logging > Driver
* Services > Logging > Driver > Options
* Volume & Deploy > Volume

Configurazione di cluster di hello per applicare i limiti delle risorse, come descritto in [governance delle risorse di Service Fabric](service-fabric-resource-governance.md). Tutte le altre direttive Docker Compose non sono supportate per questa versione di anteprima.

## <a name="servicednsname-computation"></a>Calcolo di ServiceDnsName

Se il nome del servizio hello specificato in un file di contenuto è un nome di dominio completo (ovvero, contiene un punto [.]), il nome DNS hello registrato da Service Fabric è `<ServiceName>` (incluso il punto di hello). In caso contrario, ogni segmento di percorso nel nome dell'applicazione hello diventa un'etichetta di dominio nel nome DNS del servizio hello, con hello primo segmento del percorso diventando etichetta di dominio di primo livello hello.

Ad esempio, se hello specificato nome di applicazione è `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` sarebbe hello nome DNS registrato.

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a>Differenze tra Compose (definizione di istanza) e il modello di applicazione di Service Fabric (definizione di tipo)

Un file docker-compose.yml descrive un set distribuibile di contenitori, incluse le relative proprietà e configurazioni.
Ad esempio, file hello può contenere variabili di ambiente e porte. È anche possibile specificare parametri di distribuzione, ad esempio i vincoli di posizione, i limiti delle risorse e i nomi DNS nel file docker compose.yml hello.

Hello [il modello di applicazione di Service Fabric](service-fabric-application-model.md) Usa i tipi di servizio e tipi di applicazione, in cui si possono avere molte istanze di applicazione di hello stesso tipo. È possibile, ad esempio, che sia presente un'istanza dell'applicazione per ogni cliente. Questo modello basato sul tipo supporta più versioni di hello stesso tipo di applicazione è registrata con il runtime di hello.

Ad esempio, il cliente può disporre di un'applicazione creata un'istanza con tipo, 1.0 di AppTypeA e cliente B può disporre di un'altra applicazione creata con hello lo stesso tipo e versione. Definire i tipi di applicazione hello nei manifesti di applicazione hello e specificare i parametri di nome e la distribuzione di applicazione hello quando si crea un'applicazione hello.

Anche se questo modello offre flessibilità, è inoltre pianificare toosupport un modello di distribuzione più semplice, basato su istanza in cui tipi sono impliciti dal file manifesto hello. In questo modello, ogni applicazione ottiene il proprio manifesto indipendente. Questa funzionalità viene offerta in anteprima aggiungendo il supporto per docker-compose.yml, che è un formato di distribuzione basato su istanze.

## <a name="next-steps"></a>Passaggi successivi

* Informazioni sull'hello [il modello di applicazione di Service Fabric](service-fabric-application-model.md)
* [Introduzione all'interfaccia della riga di comando di Service Fabric](service-fabric-cli.md)
