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
# <a name="using-azure-container-registry-webhooks---azure-portal"></a><span data-ttu-id="b5e4e-104">Utilizzo dei webhook del registro contenitori di Azure - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b5e4e-104">Using Azure Container Registry webhooks - Azure portal</span></span>

<span data-ttu-id="b5e4e-105">Un registro di sistema del contenitore di Azure archivia e gestisce immagini contenitore Docker private, analogamente toohello Hub Docker archivia le immagini Docker pubbliche.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-105">An Azure container registry stores and manages private Docker container images, similar toohello way Docker Hub stores public Docker images.</span></span> <span data-ttu-id="b5e4e-106">Utilizzare gli eventi di tootrigger webhook quando determinate azioni si verificano in un repository del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-106">You use webhooks tootrigger events when certain actions take place in one of your registry repositories.</span></span> <span data-ttu-id="b5e4e-107">Webhook possono rispondere tooevents a livello del Registro di sistema hello o possono essere limitati tag repository specifico tooa verso il basso.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-107">Webhooks can respond tooevents at hello registry level or they can be scoped down tooa specific repository tag.</span></span> 

<span data-ttu-id="b5e4e-108">Per altre sfondo e i concetti, vedere hello [Panoramica](./container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="b5e4e-108">For more background and concepts, see hello [overview](./container-registry-intro.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5e4e-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b5e4e-109">Prerequisites</span></span> 

- <span data-ttu-id="b5e4e-110">Un registro contenitori gestito in Azure: creare un registro contenitori gestito nella sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="b5e4e-110">Azure container managed registry - Create a managed container registry in your Azure subscription.</span></span> <span data-ttu-id="b5e4e-111">Ad esempio, utilizzare hello portale di Azure o hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-111">For example, use hello Azure portal or hello Azure CLI 2.0.</span></span> 
- <span data-ttu-id="b5e4e-112">Docker CLI - tooset del computer locale come un host e accesso hello Docker CLI i comandi di Docker, installare il motore Docker.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-112">Docker CLI - tooset up your local computer as a Docker host and access hello Docker CLI commands, install Docker Engine.</span></span> 

## <a name="create-webhook-azure-portal"></a><span data-ttu-id="b5e4e-113">Creare un webhook tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b5e4e-113">Create webhook Azure portal</span></span>

1. <span data-ttu-id="b5e4e-114">Accedi al portale di Azure toohello e passare toohello del Registro di sistema in cui si desidera toocreate webhook.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-114">Log in toohello Azure portal and navigate toohello registry in which you want toocreate webhooks.</span></span> 

2. <span data-ttu-id="b5e4e-115">Nel Pannello di contenitore hello, selezionare scheda "Webhook" hello.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-115">In hello container blade, select hello "Webhooks" tab.</span></span> 

3. <span data-ttu-id="b5e4e-116">Selezionare "Aggiungi" dalla barra degli strumenti di hello webhook blade.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-116">Select "Add" from hello webhook blade toolbar.</span></span> 

4. <span data-ttu-id="b5e4e-117">Hello completo *Webhook creare* form con hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="b5e4e-117">Complete hello *Create Webhook* form with hello following information:</span></span>

| <span data-ttu-id="b5e4e-118">Valore</span><span class="sxs-lookup"><span data-stu-id="b5e4e-118">Value</span></span> | <span data-ttu-id="b5e4e-119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b5e4e-119">Description</span></span> |
|---|---|
| <span data-ttu-id="b5e4e-120">Nome</span><span class="sxs-lookup"><span data-stu-id="b5e4e-120">Name</span></span> | <span data-ttu-id="b5e4e-121">nome Hello da toogive toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-121">hello name you want toogive toohello webhook.</span></span> <span data-ttu-id="b5e4e-122">Può contenere solo lettere minuscole e numeri e avere una lunghezza compresa tra 5 e 50 caratteri.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-122">It can only contain lowercase letters and numbers and between 5-50 characters.</span></span> |
| <span data-ttu-id="b5e4e-123">URI del servizio</span><span class="sxs-lookup"><span data-stu-id="b5e4e-123">Service URI</span></span> | <span data-ttu-id="b5e4e-124">Hello URI in cui hello webhook per l'invio di notifiche POST.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-124">hello URI where hello webhook should send POST notifications.</span></span> |
| <span data-ttu-id="b5e4e-125">Intestazioni personalizzate</span><span class="sxs-lookup"><span data-stu-id="b5e4e-125">Custom headers</span></span> | <span data-ttu-id="b5e4e-126">Intestazioni desiderato toopass insieme richiesta POST hello.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-126">Headers you want toopass along with hello POST request.</span></span> <span data-ttu-id="b5e4e-127">Devono essere nel formato "chiave: valore".</span><span class="sxs-lookup"><span data-stu-id="b5e4e-127">They should be in "key: value" format.</span></span> |
| <span data-ttu-id="b5e4e-128">Azioni trigger</span><span class="sxs-lookup"><span data-stu-id="b5e4e-128">Trigger actions</span></span> | <span data-ttu-id="b5e4e-129">Azioni che attivano hello webhook.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-129">Actions that trigger hello webhook.</span></span> <span data-ttu-id="b5e4e-130">Attualmente webhook possono essere attivati da push e/o eliminare azioni tooan immagine.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-130">Currently webhooks can be triggered by push and/or delete actions tooan image.</span></span> |
| <span data-ttu-id="b5e4e-131">Stato</span><span class="sxs-lookup"><span data-stu-id="b5e4e-131">Status</span></span> | <span data-ttu-id="b5e4e-132">stato Hello hello webhook dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-132">hello status for hello webhook after it's created.</span></span> <span data-ttu-id="b5e4e-133">Questa opzione è abilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-133">It's enabled by default.</span></span> |
| <span data-ttu-id="b5e4e-134">Scope</span><span class="sxs-lookup"><span data-stu-id="b5e4e-134">Scope</span></span> | <span data-ttu-id="b5e4e-135">ambito Hello il cui funzionamento webhook hello.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-135">hello scope at which hello webhook works.</span></span> <span data-ttu-id="b5e4e-136">Per impostazione predefinita l'ambito di hello è per tutti gli eventi nel Registro di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-136">By default hello scope is for all events in hello registry.</span></span> <span data-ttu-id="b5e4e-137">Può essere specificato per un repository o da un tag con formato hello "repository: tag".</span><span class="sxs-lookup"><span data-stu-id="b5e4e-137">It can be specified for a repository or a tag by using hello format "repository: tag".</span></span> |

<span data-ttu-id="b5e4e-138">Modulo di webhook di esempio:</span><span class="sxs-lookup"><span data-stu-id="b5e4e-138">Example webhook form:</span></span>

![Interfaccia utente di DC/OS](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a><span data-ttu-id="b5e4e-140">Creare un webhook usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b5e4e-140">Create webhook Azure CLI</span></span>

<span data-ttu-id="b5e4e-141">un webhook utilizzando toocreate hello CLI di Azure, utilizzare hello [creare az acr webhook](/cli/azure/acr/webhook#create) comando.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-141">toocreate a webhook using hello Azure CLI, use hello [az acr webhook create](/cli/azure/acr/webhook#create) command.</span></span>

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a><span data-ttu-id="b5e4e-142">Testare un webhook</span><span class="sxs-lookup"><span data-stu-id="b5e4e-142">Test webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="b5e4e-143">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b5e4e-143">Azure portal</span></span>

<span data-ttu-id="b5e4e-144">Webhook hello toousing precedente nel contenitore immagine push e azioni di eliminazione, possono essere testata usando hello **Ping** pulsante.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-144">Prior toousing hello webhook on container image push and delete actions, it can be tested using hello **Ping** button.</span></span> <span data-ttu-id="b5e4e-145">Quando si, hello Ping Invia che un toohello richiesta post generico specificato endpoint e i registri hello risposta.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-145">When used, hello Ping sends a generic post request toohello specified endpoint and logs hello response.</span></span> <span data-ttu-id="b5e4e-146">Questa opzione è utile tooverify che hello webhook è stato configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-146">This is helpful tooverify that hello webhook has been set up correctly.</span></span>

1. <span data-ttu-id="b5e4e-147">Selezionare webhook hello desiderato tootest.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-147">Select hello webhook you want tootest.</span></span> 
2. <span data-ttu-id="b5e4e-148">Nella barra degli strumenti superiore hello, selezionare l'azione "Ping" hello.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-148">In hello top toolbar, select hello "Ping" action.</span></span> 
3. <span data-ttu-id="b5e4e-149">Controllare hello richiesta e risposta.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-149">Check hello request and response.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="b5e4e-150">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b5e4e-150">Azure CLI</span></span>

<span data-ttu-id="b5e4e-151">tootest un webhook di record con hello CLI di Azure, utilizzare hello [ping di az acr webhook](/cli/azure/acr/webhook#ping) comando.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-151">tootest an ACR webhook with hello Azure CLI, use hello [az acr webhook ping](/cli/azure/acr/webhook#ping) command.</span></span>

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

<span data-ttu-id="b5e4e-152">risultati di hello toosee, utilizzare hello [elenco eventi az acr webhook](/cli/azure/acr/webhook#list-events) comando.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-152">toosee hello results, use hello [az acr webhook list-events](/cli/azure/acr/webhook#list-events) command.</span></span> 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a><span data-ttu-id="b5e4e-153">Eliminare un webhook</span><span class="sxs-lookup"><span data-stu-id="b5e4e-153">Delete webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="b5e4e-154">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b5e4e-154">Azure portal</span></span>

<span data-ttu-id="b5e4e-155">È possibile eliminare ogni webhook selezionando webhook hello e quindi il pulsante Elimina hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b5e4e-155">Each webhook can be deleted by selecting hello webhook and then hello delete button on hello Azure portal.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="b5e4e-156">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b5e4e-156">Azure CLI</span></span>

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```