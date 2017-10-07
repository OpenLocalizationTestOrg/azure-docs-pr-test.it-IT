---
title: aaaUse bozza con il servizio contenitore di Azure e del Registro di sistema di Azure contenitore | Documenti Microsoft
description: Creare un cluster ACS Kubernetes e un toocreate del Registro di sistema di Azure contenitore della prima applicazione in Azure con bozza.
services: container-service
documentationcenter: 
author: squillace
manager: gamonroy
editor: 
tags: draft, helm, acs, azure-container-service
keywords: Docker, contenitori, microservizi, Kubernetes, Draft, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: f5e21cda01e5e8452bf86a5c8fa458904d89f451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a>Utilizzare bozza con il servizio contenitore di Azure e del Registro di sistema di Azure contenitore toobuild e distribuire un'applicazione tooKubernetes

[Bozza](https://aka.ms/draft) è un nuovo strumento open source che rende le applicazioni basate sul contenitore toodevelop semplice e distribuirli tooKubernetes cluster senza conoscere molto di Docker e Kubernetes - o anche l'installazione. Usando strumenti come bozza consentono lo stato attivo del team compilazione di un'applicazione hello con Kubernetes, non sostenere il maggior numero tooinfrastructure attenzione.

È possibile usare Draft con qualsiasi registro di immagini Docker e cluster Kubernetes, anche in locale. Questa esercitazione viene illustrato come toouse ACS con toocreate Kubernetes e record DNS di Azure uno sviluppatore CI/CD-ROM in tempo reale di pipeline utilizzando bozza.


## <a name="create-an-azure-container-registry"></a>Creare un Registro contenitori di Azure
È possibile [creare un nuovo registro contenitore Azure](../../container-registry/container-registry-get-started-azure-cli.md), ma hello passaggi sono i seguenti:

1. Creare un toomanage gruppo di risorse di Azure del cluster Kubernetes record del Registro di sistema e hello in ACS.
      ```azurecli
      az group create --name draft --location eastus
      ```

2. Creare un registro di immagini del Registro contenitori di Azure usando [az acr create](/cli/azure/acr#create)
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a>Creare un servizio contenitore di Azure con Kubernetes

A questo punto è pronti toouse [az acs creare](/cli/azure/acs#create) cluster toocreate un ACS utilizzando Kubernetes come hello `--orchestrator-type` valore.
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> Poiché Kubernetes non è di tipo di orchestrator hello predefinito, assicurarsi di utilizzare hello `--orchestrator-type kubernetes` passare.

output di Hello quando ha esito positivo sarà simile toohello seguente.

```json
waiting for AAD role toopropagate.done
{
  "id": "/subscriptions/<guid>/resourceGroups/draft/providers/Microsoft.Resources/deployments/azurecli14904.93snip09",
  "name": "azurecli1496227204.9323909",
  "properties": {
    "correlationId": "<guid>",
    "debugSetting": null,
    "dependencies": [],
    "mode": "Incremental",
    "outputs": null,
    "parameters": {
      "clientSecret": {
        "type": "SecureString"
      }
    },
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.ContainerService",
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "locations": [
              "westus"
            ],
            "properties": null,
            "resourceType": "containerServices"
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "template": null,
    "templateLink": null,
    "timestamp": "2017-05-31T10:46:29.434095+00:00"
  },
  "resourceGroup": "draft"
}
```

Dopo aver creato un cluster, è possibile importare le credenziali di hello utilizzando hello [az acs kubernetes get-credenziali](/cli/azure/acs/kubernetes#get-credentials) comando. Ora è un file di configurazione locale per il cluster, ovvero quali Helm e bozza necessario tooget proprio lavoro.

## <a name="install-and-configure-draft"></a>Installare e configurare Draft
istruzioni di installazione di Hello per bozza presenti hello [repository bozza](https://github.com/Azure/draft/blob/master/docs/install.md). Sono relativamente semplici, ma richiedono operazioni di configurazione, come dipende [Helm](https://aka.ms/helm) toocreate e distribuire un grafico Helm in cluster Kubernetes hello.

1. [Scaricare e installare Helm](https://aka.ms/helm#install).
2. Utilizzare toosearch Helm per e installa `stable/traefik`e in ingresso controller tooenable le richieste per le compilazioni in ingresso.
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    Ora impostare un'espressione di controllo su hello `ingress` controller toocapture hello IP valore esterno quando viene distribuito. Questo indirizzo IP sarà hello uno [mappata dominio distribuzione tooyour](#wire-up-deployment-domain) nella sezione successiva hello.

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    In questo caso, hello indirizzo IP esterno per il dominio di distribuzione hello è `13.64.108.240`. Ora è possibile mappare i IP toothat di dominio.

## <a name="wire-up-deployment-domain"></a>Collegare il dominio di distribuzione

Draft crea una versione per ogni grafico Helm creato, ovvero ogni applicazione a cui si sta lavorando. Ognuno di essi Ottiene un nome generato utilizzato dal progetto come un _sottodominio_ sopra radice hello _dominio distribuzione_ controllate dall'utente. (In questo esempio, si usa `squillace.io` come dominio distribuzione hello.) tooenable questo comportamento di sottodominio, è necessario creare un record A per `'*'` le voci DNS per il dominio di distribuzione, in modo che ogni generato sottodominio è indirizzato toohello Kubernetes controller di ingresso del cluster.

Un provider di dominio ha i propri server DNS di vie tooassign; troppo[delegare il tooAzure nameservers di dominio DNS](../../dns/dns-delegate-domain-azure-dns.md), si accettano hello alla procedura seguente:

1. Creare un gruppo di risorse per la propria zona.
    ```azurecli
    az group create --name squillace.io --location eastus
    {
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io",
      "location": "eastus",
      "managedBy": null,
      "name": "zones",
      "properties": {
        "provisioningState": "Succeeded"
      },
      "tags": null
    }
    ```

2. Creare una zona DNS per il proprio dominio.
Hello utilizzare [zona dns di rete az creare](/cli/azure/network/dns/zone#create) comando tooobtain hello nameservers toodelegate DNS controllare tooAzure DNS per il dominio.
    ```azurecli
    az network dns zone create --resource-group squillace.io --name squillace.io
    {
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/zones/providers/Microsoft.Network/dnszones/squillace.io",
      "location": "global",
      "maxNumberOfRecordSets": 5000,
      "name": "squillace.io",
      "nameServers": [
        "ns1-09.azure-dns.com.",
        "ns2-09.azure-dns.net.",
        "ns3-09.azure-dns.org.",
        "ns4-09.azure-dns.info."
      ],
      "numberOfRecordSets": 2,
      "resourceGroup": "squillace.io",
      "tags": {},
      "type": "Microsoft.Network/dnszones"
    }
    ```
3. Aggiungere i server DNS di hello che è toohello provider del dominio per il dominio di distribuzione, che consente il dominio è toouse DNS di Azure toorepoint desiderato.
4. Creare una voce di set di record A per il toohello di mapping dominio distribuzione `ingress` IP dal passaggio 2 della sezione precedente hello.
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
output di Hello simile al seguente:
    ```json
    {
      "arecords": [
        {
          "ipv4Address": "13.64.108.240"
        }
      ],
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io/providers/Microsoft.Network/dnszones/squillace.io/A/*",
      "metadata": null,
      "name": "*",
      "resourceGroup": "squillace.io",
      "ttl": 3600,
      "type": "Microsoft.Network/dnszones/A"
    }
    ```

5. Configurare toouse bozza del Registro di sistema e creare i sottodomini per ogni grafico Helm che viene creato. tooconfigure bozza, è necessario:
  - Il nome del Registro contenitori di Azure (in questo esempio, `draft`)
  - La chiave, o password, del registro da `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.
  - dominio di distribuzione principale di Hello di aver configurato toomap toohello Kubernetes in ingresso l'indirizzo IP esterno (in questo caso, `squillace.io`)

  Chiamare `draft init` e il processo di configurazione di hello viene chiesto di immettere i valori hello precedenti. processo Hello sembra qualcosa seguente hello hello prima di eseguirla.
 ```bash
    $ draft init
    Creating pack ruby...
    Creating pack node...
    Creating pack gradle...
    Creating pack maven...
    Creating pack php...
    Creating pack python...
    Creating pack dotnetcore...
    Creating pack golang...
    $DRAFT_HOME has been configured at /Users/ralphsquillace/.draft.

    In order tooinstall Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

Ora si è pronti toodeploy un'applicazione.


## <a name="build-and-deploy-an-application"></a>Compilare e distribuire un'applicazione

Nel repository di bozza hello sono [sei applicazioni di esempio semplice](https://github.com/Azure/draft/tree/master/examples). Clonare il repository hello e utilizziamo hello [esempio Python](https://github.com/Azure/draft/tree/master/examples/python). Modificare in directory esempi/Python hello e digitare `draft create` toobuild un'applicazione hello. Dovrebbe essere simile hello di esempio seguente.
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

output di Hello include un Dockerfile e un grafico Helm. toobuild e la distribuzione, è sufficiente digitare `draft up`. output di Hello è vasto, ma inizia come hello di esempio seguente.
```bash
$ draft up
--> Building Dockerfile
Step 1 : FROM python:onbuild
onbuild: Pulling from library/python
10a267c67f42: Pulling fs layer
fb5937da9414: Pulling fs layer
9021b2326a1e: Pulling fs layer
dbed9b09434e: Pulling fs layer
ea8a37f15161: Pulling fs layer
<snip>
```

e quando ha esito positivo termina con un codice simile toohello esempio seguente.
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

L'elemento è il nome del grafico, è ora possibile `curl http://gangly-bronco.squillace.io` risposta hello tooreceive, `Hello World!`.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver creato un cluster ACS Kubernetes, è possibile provare a utilizzare [Registro di sistema di Azure contenitore](../../container-registry/container-registry-intro.md) toocreate altre e diverse distribuzioni di questo scenario. È ad esempio possibile creare un recordset DNS di dominio draft._basedomain.toplevel_ che controlla le attività all'esterno di un sottodominio più profondo per distribuzioni specifiche del servizio contenitore di Azure.






