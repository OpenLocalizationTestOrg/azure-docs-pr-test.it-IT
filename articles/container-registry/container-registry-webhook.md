---
title: Webhook del registro contenitori di Azure | Microsoft Docs
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
ms.openlocfilehash: d0190f5725671c320d92b897f0dcef7a526a86e3
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a><span data-ttu-id="6bb57-104">Utilizzo dei webhook del registro contenitori di Azure - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6bb57-104">Using Azure Container Registry webhooks - Azure portal</span></span>

<span data-ttu-id="6bb57-105">Un registro contenitori di Azure archivia e gestisce le immagini dei contenitori Docker private, in modo analogo a come Docker Hub archivia le immagini Docker pubbliche.</span><span class="sxs-lookup"><span data-stu-id="6bb57-105">An Azure container registry stores and manages private Docker container images, similar to the way Docker Hub stores public Docker images.</span></span> <span data-ttu-id="6bb57-106">Usando i webhook, è possibile attivare eventi specifici quando in uno dei repository del registro si verificano determinate azioni.</span><span class="sxs-lookup"><span data-stu-id="6bb57-106">You use webhooks to trigger events when certain actions take place in one of your registry repositories.</span></span> <span data-ttu-id="6bb57-107">I webhook possono rispondere agli eventi a livello di registro oppure possono essere limitati a un tag di repository specifico.</span><span class="sxs-lookup"><span data-stu-id="6bb57-107">Webhooks can respond to events at the registry level or they can be scoped down to a specific repository tag.</span></span> 

<span data-ttu-id="6bb57-108">Per altre informazioni di base e concetti, vedere la [panoramica](./container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="6bb57-108">For more background and concepts, see the [overview](./container-registry-intro.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bb57-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6bb57-109">Prerequisites</span></span> 

- <span data-ttu-id="6bb57-110">Un registro contenitori gestito in Azure: creare un registro contenitori gestito nella sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="6bb57-110">Azure container managed registry - Create a managed container registry in your Azure subscription.</span></span> <span data-ttu-id="6bb57-111">usando, ad esempio, il portale di Azure o l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="6bb57-111">For example, use the Azure portal or the Azure CLI 2.0.</span></span> 
- <span data-ttu-id="6bb57-112">Interfaccia della riga di comando di Docker: per configurare il computer locale come host Docker e accedere ai comandi della riga di comando di Docker, installare Docker Engine.</span><span class="sxs-lookup"><span data-stu-id="6bb57-112">Docker CLI - To set up your local computer as a Docker host and access the Docker CLI commands, install Docker Engine.</span></span> 

## <a name="create-webhook-azure-portal"></a><span data-ttu-id="6bb57-113">Creare un webhook tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6bb57-113">Create webhook Azure portal</span></span>

1. <span data-ttu-id="6bb57-114">Accedere al portale di Azure e passare al registro in cui si vuole creare i webhook.</span><span class="sxs-lookup"><span data-stu-id="6bb57-114">Log in to the Azure portal and navigate to the registry in which you want to create webhooks.</span></span> 

2. <span data-ttu-id="6bb57-115">Nel pannello del contenitore selezionare la scheda "Webhook".</span><span class="sxs-lookup"><span data-stu-id="6bb57-115">In the container blade, select the "Webhooks" tab.</span></span> 

3. <span data-ttu-id="6bb57-116">Selezionare "Aggiungi" nella barra degli strumenti del pannello relativo al webhook.</span><span class="sxs-lookup"><span data-stu-id="6bb57-116">Select "Add" from the webhook blade toolbar.</span></span> 

4. <span data-ttu-id="6bb57-117">Completare il modulo *Create Webhook* (Crea webhook) con le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6bb57-117">Complete the *Create Webhook* form with the following information:</span></span>

| <span data-ttu-id="6bb57-118">Valore</span><span class="sxs-lookup"><span data-stu-id="6bb57-118">Value</span></span> | <span data-ttu-id="6bb57-119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6bb57-119">Description</span></span> |
|---|---|
| <span data-ttu-id="6bb57-120">Nome</span><span class="sxs-lookup"><span data-stu-id="6bb57-120">Name</span></span> | <span data-ttu-id="6bb57-121">Il nome da assegnare al webhook.</span><span class="sxs-lookup"><span data-stu-id="6bb57-121">The name you want to give to the webhook.</span></span> <span data-ttu-id="6bb57-122">Può contenere solo lettere minuscole e numeri e avere una lunghezza compresa tra 5 e 50 caratteri.</span><span class="sxs-lookup"><span data-stu-id="6bb57-122">It can only contain lowercase letters and numbers and between 5-50 characters.</span></span> |
| <span data-ttu-id="6bb57-123">URI del servizio</span><span class="sxs-lookup"><span data-stu-id="6bb57-123">Service URI</span></span> | <span data-ttu-id="6bb57-124">L'URI in cui il webhook deve inviare le notifiche POST.</span><span class="sxs-lookup"><span data-stu-id="6bb57-124">The URI where the webhook should send POST notifications.</span></span> |
| <span data-ttu-id="6bb57-125">Intestazioni personalizzate</span><span class="sxs-lookup"><span data-stu-id="6bb57-125">Custom headers</span></span> | <span data-ttu-id="6bb57-126">Le intestazioni che si vuole passare insieme alla richiesta POST.</span><span class="sxs-lookup"><span data-stu-id="6bb57-126">Headers you want to pass along with the POST request.</span></span> <span data-ttu-id="6bb57-127">Devono essere nel formato "chiave: valore".</span><span class="sxs-lookup"><span data-stu-id="6bb57-127">They should be in "key: value" format.</span></span> |
| <span data-ttu-id="6bb57-128">Azioni trigger</span><span class="sxs-lookup"><span data-stu-id="6bb57-128">Trigger actions</span></span> | <span data-ttu-id="6bb57-129">Le azioni che attivano il webhook.</span><span class="sxs-lookup"><span data-stu-id="6bb57-129">Actions that trigger the webhook.</span></span> <span data-ttu-id="6bb57-130">Attualmente i webhook possono essere attivati tramite azioni di push e/o eliminazione in un'immagine.</span><span class="sxs-lookup"><span data-stu-id="6bb57-130">Currently webhooks can be triggered by push and/or delete actions to an image.</span></span> |
| <span data-ttu-id="6bb57-131">Stato</span><span class="sxs-lookup"><span data-stu-id="6bb57-131">Status</span></span> | <span data-ttu-id="6bb57-132">Lo stato del webhook dopo che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="6bb57-132">The status for the webhook after it's created.</span></span> <span data-ttu-id="6bb57-133">Questa opzione è abilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="6bb57-133">It's enabled by default.</span></span> |
| <span data-ttu-id="6bb57-134">Scope</span><span class="sxs-lookup"><span data-stu-id="6bb57-134">Scope</span></span> | <span data-ttu-id="6bb57-135">L'ambito in cui viene applicato il webhook.</span><span class="sxs-lookup"><span data-stu-id="6bb57-135">The scope at which the webhook works.</span></span> <span data-ttu-id="6bb57-136">Per impostazione predefinita, l'ambito comprende tutti gli eventi del registro.</span><span class="sxs-lookup"><span data-stu-id="6bb57-136">By default the scope is for all events in the registry.</span></span> <span data-ttu-id="6bb57-137">Può essere limitato a un repository o un tag usando il formato "repository: tag".</span><span class="sxs-lookup"><span data-stu-id="6bb57-137">It can be specified for a repository or a tag by using the format "repository: tag".</span></span> |

<span data-ttu-id="6bb57-138">Modulo di webhook di esempio:</span><span class="sxs-lookup"><span data-stu-id="6bb57-138">Example webhook form:</span></span>

![Interfaccia utente di DC/OS](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a><span data-ttu-id="6bb57-140">Creare un webhook usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="6bb57-140">Create webhook Azure CLI</span></span>

<span data-ttu-id="6bb57-141">Per creare un webhook usando l'interfaccia della riga di comando di Azure, usare il comando [az acr webhook create](/cli/azure/acr/webhook#create).</span><span class="sxs-lookup"><span data-stu-id="6bb57-141">To create a webhook using the Azure CLI, use the [az acr webhook create](/cli/azure/acr/webhook#create) command.</span></span>

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a><span data-ttu-id="6bb57-142">Testare un webhook</span><span class="sxs-lookup"><span data-stu-id="6bb57-142">Test webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="6bb57-143">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6bb57-143">Azure portal</span></span>

<span data-ttu-id="6bb57-144">Prima di usare il webhook in azioni di push o eliminazione di un'immagine del contenitore, è possibile testarlo tramite il pulsante **Ping**.</span><span class="sxs-lookup"><span data-stu-id="6bb57-144">Prior to using the webhook on container image push and delete actions, it can be tested using the **Ping** button.</span></span> <span data-ttu-id="6bb57-145">Quando viene usato, il comando Ping invia una richiesta POST generica all'endpoint specificato e registra la risposta.</span><span class="sxs-lookup"><span data-stu-id="6bb57-145">When used, the Ping sends a generic post request to the specified endpoint and logs the response.</span></span> <span data-ttu-id="6bb57-146">In questo modo è possibile verificare che il webhook sia stato configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="6bb57-146">This is helpful to verify that the webhook has been set up correctly.</span></span>

1. <span data-ttu-id="6bb57-147">Selezionare il webhook da testare.</span><span class="sxs-lookup"><span data-stu-id="6bb57-147">Select the webhook you want to test.</span></span> 
2. <span data-ttu-id="6bb57-148">Nella barra degli strumenti superiore selezionare l'azione "Ping".</span><span class="sxs-lookup"><span data-stu-id="6bb57-148">In the top toolbar, select the "Ping" action.</span></span> 
3. <span data-ttu-id="6bb57-149">Verificare la richiesta e la risposta.</span><span class="sxs-lookup"><span data-stu-id="6bb57-149">Check the request and response.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="6bb57-150">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="6bb57-150">Azure CLI</span></span>

<span data-ttu-id="6bb57-151">Per testare un webhook del registro contenitori di Azure con l'interfaccia della riga di comando di Azure, usare il comando [az acr webhook ping](/cli/azure/acr/webhook#ping).</span><span class="sxs-lookup"><span data-stu-id="6bb57-151">To test an ACR webhook with the Azure CLI, use the [az acr webhook ping](/cli/azure/acr/webhook#ping) command.</span></span>

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

<span data-ttu-id="6bb57-152">Per visualizzare i risultati, usare il comando [az acr webhook list-events](/cli/azure/acr/webhook#list-events).</span><span class="sxs-lookup"><span data-stu-id="6bb57-152">To see the results, use the [az acr webhook list-events](/cli/azure/acr/webhook#list-events) command.</span></span> 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a><span data-ttu-id="6bb57-153">Eliminare un webhook</span><span class="sxs-lookup"><span data-stu-id="6bb57-153">Delete webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="6bb57-154">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6bb57-154">Azure portal</span></span>

<span data-ttu-id="6bb57-155">Per eliminare un webhook, è possibile selezionarlo e usare il pulsante di eliminazione disponibile nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6bb57-155">Each webhook can be deleted by selecting the webhook and then the delete button on the Azure portal.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="6bb57-156">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="6bb57-156">Azure CLI</span></span>

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```