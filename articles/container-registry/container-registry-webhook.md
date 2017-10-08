---
title: aaaAzure contenitore del Registro di sistema webhook | Documenti Microsoft
description: Webhook del registro contenitori di Azure
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: Docker, contenitori, registro contenitori di Azure
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a>Utilizzo dei webhook del registro contenitori di Azure - Portale di Azure

Un registro di sistema del contenitore di Azure archivia e gestisce immagini contenitore Docker private, analogamente toohello Hub Docker archivia le immagini Docker pubbliche. Utilizzare gli eventi di tootrigger webhook quando determinate azioni si verificano in un repository del Registro di sistema. Webhook possono rispondere tooevents a livello del Registro di sistema hello o possono essere limitati tag repository specifico tooa verso il basso. 

Per altre sfondo e i concetti, vedere hello [Panoramica](./container-registry-intro.md).

## <a name="prerequisites"></a>Prerequisiti 

- Un registro contenitori gestito in Azure: creare un registro contenitori gestito nella sottoscrizione di Azure Ad esempio, utilizzare hello portale di Azure o hello CLI di Azure 2.0. 
- Docker CLI - tooset del computer locale come un host e accesso hello Docker CLI i comandi di Docker, installare il motore Docker. 

## <a name="create-webhook-azure-portal"></a>Creare un webhook tramite il portale di Azure

1. Accedi al portale di Azure toohello e passare toohello del Registro di sistema in cui si desidera toocreate webhook. 

2. Nel Pannello di contenitore hello, selezionare scheda "Webhook" hello. 

3. Selezionare "Aggiungi" dalla barra degli strumenti di hello webhook blade. 

4. Hello completo *Webhook creare* form con hello le seguenti informazioni:

| Valore | Descrizione |
|---|---|
| Nome | nome Hello da toogive toohello webhook. Può contenere solo lettere minuscole e numeri e avere una lunghezza compresa tra 5 e 50 caratteri. |
| URI del servizio | Hello URI in cui hello webhook per l'invio di notifiche POST. |
| Intestazioni personalizzate | Intestazioni desiderato toopass insieme richiesta POST hello. Devono essere nel formato "chiave: valore". |
| Azioni trigger | Azioni che attivano hello webhook. Attualmente webhook possono essere attivati da push e/o eliminare azioni tooan immagine. |
| Stato | stato Hello hello webhook dopo averlo creato. Questa opzione è abilitata per impostazione predefinita. |
| Scope | ambito Hello il cui funzionamento webhook hello. Per impostazione predefinita l'ambito di hello è per tutti gli eventi nel Registro di sistema hello. Può essere specificato per un repository o da un tag con formato hello "repository: tag". |

Modulo di webhook di esempio:

![Interfaccia utente di DC/OS](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a>Creare un webhook usando l'interfaccia della riga di comando di Azure

un webhook utilizzando toocreate hello CLI di Azure, utilizzare hello [creare az acr webhook](/cli/azure/acr/webhook#create) comando.

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a>Testare un webhook

### <a name="azure-portal"></a>Portale di Azure

Webhook hello toousing precedente nel contenitore immagine push e azioni di eliminazione, possono essere testata usando hello **Ping** pulsante. Quando si, hello Ping Invia che un toohello richiesta post generico specificato endpoint e i registri hello risposta. Questa opzione è utile tooverify che hello webhook è stato configurato correttamente.

1. Selezionare webhook hello desiderato tootest. 
2. Nella barra degli strumenti superiore hello, selezionare l'azione "Ping" hello. 
3. Controllare hello richiesta e risposta.

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

tootest un webhook di record con hello CLI di Azure, utilizzare hello [ping di az acr webhook](/cli/azure/acr/webhook#ping) comando.

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

risultati di hello toosee, utilizzare hello [elenco eventi az acr webhook](/cli/azure/acr/webhook#list-events) comando. 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a>Eliminare un webhook

### <a name="azure-portal"></a>Portale di Azure

È possibile eliminare ogni webhook selezionando webhook hello e quindi il pulsante Elimina hello in hello portale di Azure.

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```