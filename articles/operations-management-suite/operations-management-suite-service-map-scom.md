---
title: Integrazione di Elenco dei servizi con System Center Operations Manager | Microsoft Docs
description: "Elenco dei servizi è una soluzione di Operations Management Suite che individua automaticamente i componenti delle applicazioni nei sistemi Windows e Linux e mappa la comunicazione fra i servizi. Questo articolo illustra l'uso di Elenco dei servizi per creare automaticamente diagrammi applicazioni distribuite in Operations Manager."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: a7dbe54ffb4daa941c19b51ba263dd3d23b7a98b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a><span data-ttu-id="cb5f7-104">Integrazione di Elenco dei servizi con System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="cb5f7-104">Service Map integration with System Center Operations Manager</span></span>
  > [!NOTE]
  > <span data-ttu-id="cb5f7-105">Questa funzionalità è disponibile in anteprima pubblica.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-105">This feature is in public preview.</span></span>
  > 
  
<span data-ttu-id="cb5f7-106">Elenco dei servizi di Operations Management Suite individua automaticamente i componenti delle applicazioni nei sistemi Windows e Linux ed esegue il mapping della comunicazione fra i servizi.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-106">Operations Management Suite Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="cb5f7-107">Elenco dei servizi consente di visualizzare i server nel modo in cui si pensa a essi, ovvero come sistemi interconnessi che forniscono servizi critici.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-107">Service Map allows you to view your servers the way you think of them, as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="cb5f7-108">Elenco dei servizi mostra le connessioni fra i server, i processi e le porte di tutte le architetture connesse via TCP senza bisogno di alcuna configurazione a parte l'installazione di un agente.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required besides the installation of an agent.</span></span> <span data-ttu-id="cb5f7-109">Per altre informazioni, vedere la [documentazione su Elenco dei servizi](operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="cb5f7-109">For more information, see the [Service Map documentation](operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="cb5f7-110">Con questa integrazione tra Elenco dei servizi e System Center Operations Manager è possibile creare automaticamente diagrammi applicazioni distribuite in Operations Manager basati sulle mappe delle dipendenze dinamiche in Elenco dei servizi.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-110">With this integration between Service Map and System Center Operations Manager, you can automatically create distributed application diagrams in Operations Manager that are based on the dynamic dependency maps in Service Map.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb5f7-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cb5f7-111">Prerequisites</span></span>
* <span data-ttu-id="cb5f7-112">Gruppo di gestione di Operations Manager che gestisce un set di server.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-112">An Operations Manager management group that is managing a set of servers.</span></span>
* <span data-ttu-id="cb5f7-113">Area di lavoro di Operations Manager con la soluzione Elenco dei servizi abilitata.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-113">An Operations Management Suite workspace with the Service Map solution enabled.</span></span>
* <span data-ttu-id="cb5f7-114">Set di server (almeno uno) che vengono gestiti da Operations Manager e inviano dati a Elenco dei servizi.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-114">A set of servers (at least one) that are being managed by Operations Manager and sending data to Service Map.</span></span> <span data-ttu-id="cb5f7-115">Sono supportati server Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-115">Windows and Linux servers are supported.</span></span>
* <span data-ttu-id="cb5f7-116">Un'entità servizio con accesso alla sottoscrizione di Azure associata all'area di lavoro di Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-116">A service principal with access to the Azure subscription that is associated with the Operations Management Suite workspace.</span></span> <span data-ttu-id="cb5f7-117">Per altre informazioni, vedere [Creare un'entità servizio](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="cb5f7-117">For more information, go to [Create a service principal](#creating-a-service-principal).</span></span>

## <a name="install-the-service-map-management-pack"></a><span data-ttu-id="cb5f7-118">Installare il management pack di Elenco dei servizi</span><span class="sxs-lookup"><span data-stu-id="cb5f7-118">Install the Service Map management pack</span></span>
<span data-ttu-id="cb5f7-119">L'integrazione tra Operations Manager ed Elenco dei servizi viene abilitata importando il bundle di management pack Microsoft.SystemCenter.ServiceMap (Microsoft.SystemCenter.ServiceMap.mpb).</span><span class="sxs-lookup"><span data-stu-id="cb5f7-119">You enable the integration between Operations Manager and Service Map by importing the Microsoft.SystemCenter.ServiceMap management pack bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span></span> <span data-ttu-id="cb5f7-120">Il bundle contiene i management pack seguenti:</span><span class="sxs-lookup"><span data-stu-id="cb5f7-120">The bundle contains the following management packs:</span></span>
* <span data-ttu-id="cb5f7-121">Microsoft Service Map Application Views</span><span class="sxs-lookup"><span data-stu-id="cb5f7-121">Microsoft Service Map Application Views</span></span>
* <span data-ttu-id="cb5f7-122">Microsoft System Center Service Map Internal</span><span class="sxs-lookup"><span data-stu-id="cb5f7-122">Microsoft System Center Service Map Internal</span></span>
* <span data-ttu-id="cb5f7-123">Microsoft System Center Service Map Overrides</span><span class="sxs-lookup"><span data-stu-id="cb5f7-123">Microsoft System Center Service Map Overrides</span></span>
* <span data-ttu-id="cb5f7-124">Microsoft System Center Service Map</span><span class="sxs-lookup"><span data-stu-id="cb5f7-124">Microsoft System Center Service Map</span></span>

## <a name="configure-the-service-map-integration"></a><span data-ttu-id="cb5f7-125">Configurare l'integrazione di Elenco dei servizi</span><span class="sxs-lookup"><span data-stu-id="cb5f7-125">Configure the Service Map integration</span></span>
<span data-ttu-id="cb5f7-126">Dopo avere installato il management pack di Elenco dei servizi, nel riquadro **Amministrazione** di **Operations Management Suite** sarà presente il nuovo nodo **Elenco dei servizi**.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-126">After you install the Service Map management pack, a new node, **Service Map**, is displayed under **Operations Management Suite** in the **Administration** pane.</span></span> 

<span data-ttu-id="cb5f7-127">Per configurare l'integrazione di Elenco dei servizi, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="cb5f7-127">To configure Service Map integration, do the following:</span></span>

1. <span data-ttu-id="cb5f7-128">Per aprire la configurazione guidata, fare clic su **Add workspace** (Aggiungi area di lavoro) nel riquadro **Service Map Overview** (Panoramica di Elenco dei servizi) .</span><span class="sxs-lookup"><span data-stu-id="cb5f7-128">To open the configuration wizard, in the **Service Map Overview** pane, click **Add workspace**.</span></span>  

    ![Riquadro Service Map Overview (Panoramica di Elenco dei servizi)](media/oms-service-map/scom-configuration.png)

2. <span data-ttu-id="cb5f7-130">Nella finestra **Configurazione di connessione** immettere l'ID o il nome del tenant, l'ID applicazione (noto anche come nome utente o ClientID) e la password dell'entità servizio, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-130">In the **Connection Configuration** window, enter the tenant name or ID, application ID (also known as the username or clientID), and password of the service principal, and then click **Next**.</span></span> <span data-ttu-id="cb5f7-131">Per altre informazioni, vedere [Creare un'entità servizio](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="cb5f7-131">For more information, go to [Create a service principal](#creating-a-service-principal).</span></span>

    ![Finestra di configurazione della connessione](media/oms-service-map/scom-config-spn.png)

3. <span data-ttu-id="cb5f7-133">Nella finestra **Subscription Selection** (Selezione della sottoscrizione), selezionare la sottoscrizione di Azure, il gruppo di risorse di Azure contenente l'area di lavoro di Operations Management Suite e infine l'area di lavoro stessa, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-133">In the **Subscription Selection** window, select the Azure subscription, Azure resource group (the one that contains the Operations Management Suite workspace), and Operations Management Suite workspace, and then click **Next**.</span></span>

    ![Area di lavoro di configurazione di Operations Manager](media/oms-service-map/scom-config-workspace.png)

4. <span data-ttu-id="cb5f7-135">Nella finestra **Machine Group Selection** (Selezione gruppi di computer) è possibile scegliere i gruppi di computer di Mapping dei servizi da sincronizzare con Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-135">In the **Machine Group Selection** window, you choose which Service Map Machine Groups you want to sync to Operations Manager.</span></span> <span data-ttu-id="cb5f7-136">Fare clic su **Add/Remove Machine Groups** (Aggiungi/Rimuovi gruppi di computer), scegliere i gruppi nell'elenco **Available Machine Groups** (Gruppi di computer disponibili) e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-136">Click **Add/Remove Machine Groups**, choose groups from the list of **Available Machine Groups**, and click **Add**.</span></span>  <span data-ttu-id="cb5f7-137">Dopo avere completato la selezione dei gruppi, fare clic su **OK** per terminare.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-137">When you are finished selecting groups, click **Ok** to finish.</span></span>
    
    ![Gruppi di computer di configurazione di Operations Manager](media/oms-service-map/scom-config-machine-groups.png)
    
5. <span data-ttu-id="cb5f7-139">Nella finestra **Selezione server** è possibile configurare il gruppo di server di Elenco dei servizi con i server che si desidera sincronizzare tra Operations Manager ed Elenco dei servizi.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-139">In the **Server Selection** window, you configure the Service Map Servers Group with the servers that you want to sync between Operations Manager and Service Map.</span></span> <span data-ttu-id="cb5f7-140">Fare clic su **Aggiungi/Rimuovi server**.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-140">Click **Add/Remove Servers**.</span></span>   
    
    <span data-ttu-id="cb5f7-141">Perché l'integrazione crei un diagramma applicazioni distribuite per un server, quest'ultimo deve essere:</span><span class="sxs-lookup"><span data-stu-id="cb5f7-141">For the integration to build a distributed application diagram for a server, the server must be:</span></span>

    * <span data-ttu-id="cb5f7-142">Gestito da Operations Manager</span><span class="sxs-lookup"><span data-stu-id="cb5f7-142">Managed by Operations Manager</span></span>
    * <span data-ttu-id="cb5f7-143">Gestito da Mapping dei servizi</span><span class="sxs-lookup"><span data-stu-id="cb5f7-143">Managed by Service Map</span></span>
    * <span data-ttu-id="cb5f7-144">Elencato nel gruppo di server di Mapping dei servizi</span><span class="sxs-lookup"><span data-stu-id="cb5f7-144">Listed in the Service Map Servers Group</span></span>

    ![Gruppo di configurazione di Operations Manager](media/oms-service-map/scom-config-group.png)

6. <span data-ttu-id="cb5f7-146">Facoltativo: selezionare il pool di risorse server di gestione per comunicare con Operations Management Suite, quindi fare clic su **Aggiungi area di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-146">Optional: Select the Management Server resource pool to communicate with Operations Management Suite, and then click **Add Workspace**.</span></span>

    ![Pool di risorse di configurazione di Operations Manager](media/oms-service-map/scom-config-pool.png)

    <span data-ttu-id="cb5f7-148">Per configurare e registrare l'area di lavoro di Operations Management Suite potrebbero essere necessari alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-148">It might take a minute to configure and register the Operations Management Suite workspace.</span></span> <span data-ttu-id="cb5f7-149">Dopo averlo configurato, Operations Manager avvia la prima sincronizzazione di Elenco dei servizi da Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-149">After it is configured, Operations Manager initiates the first Service Map sync from Operations Management Suite.</span></span>

    ![Pool di risorse di configurazione di Operations Manager](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a><span data-ttu-id="cb5f7-151">Monitorare le metriche del servizio</span><span class="sxs-lookup"><span data-stu-id="cb5f7-151">Monitor Service Map</span></span>
<span data-ttu-id="cb5f7-152">Dopo aver connesso l'area di lavoro di Operations Management Suite, nel riquadro **Monitoraggio** della console di Operations Manager comparirà una nuova cartella denominata Elenco dei servizi.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-152">After the Operations Management Suite workspace is connected, a new folder, Service Map, is displayed in the **Monitoring** pane of the Operations Manager console.</span></span>

![Riquadro Monitoraggio di Operations Manager](media/oms-service-map/scom-monitoring.png)

<span data-ttu-id="cb5f7-154">La cartella Mapping dei servizi ha quattro nodi:</span><span class="sxs-lookup"><span data-stu-id="cb5f7-154">The Service Map folder has four nodes:</span></span>
* <span data-ttu-id="cb5f7-155">**Avvisi attivi**: elenca tutti gli avvisi attivi per le comunicazioni tra Operations Manager e Mapping dei servizi.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-155">**Active Alerts**: Lists all the active alerts about the communication between Operations Manager and Service Map.</span></span>  <span data-ttu-id="cb5f7-156">Si noti che tali avvisi non corrispondono agli avvisi di Operations Management Suite sincronizzati con Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-156">Note that these alerts are not Operations Management Suite alerts being synced to Operations Manager.</span></span> 

* <span data-ttu-id="cb5f7-157">**Server**: contiene l'elenco dei server monitorati configurati per la sincronizzazione da Elenco dei servizi.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-157">**Servers**: Lists the monitored servers that are configured to sync from Service Map.</span></span>

    ![Riquadro Monitoraggio server di Operations Manager](media/oms-service-map/scom-monitoring-servers.png)

* <span data-ttu-id="cb5f7-159">**Machine Group Dependency Views** (Visualizzazioni dipendenze gruppi di computer): elenca tutti i gruppi di computer sincronizzati da Mapping dei servizi.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-159">**Machine Group Dependency Views**: Lists all machine groups that are synced from Service Map.</span></span> <span data-ttu-id="cb5f7-160">È possibile fare clic su un gruppo per visualizzarne il diagramma applicazioni distribuite.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-160">You can click any group to view its distributed application diagram.</span></span>

    ![Diagramma applicazioni distribuite di Operations Manager](media/oms-service-map/scom-group-dad.png)

* <span data-ttu-id="cb5f7-162">**Server Dependency Views** (Visualizzazioni dipendenze server): elenca tutti i server sincronizzati da Elenco dei servizi.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-162">**Server Dependency Views**: Lists all servers that are synced from Service Map.</span></span> <span data-ttu-id="cb5f7-163">È possibile fare clic su un server per visualizzarne il diagramma applicazioni distribuite.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-163">You can click any server to view its distributed application diagram.</span></span>

    ![Diagramma applicazioni distribuite di Operations Manager](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-the-workspace"></a><span data-ttu-id="cb5f7-165">Modificare o eliminare l'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="cb5f7-165">Edit or delete the workspace</span></span>
<span data-ttu-id="cb5f7-166">È possibile modificare o eliminare l'area di lavoro configurata tramite il riquadro **Service Map Overview** (Panoramica di Elenco dei servizi): riquadro **Amministrazione** --> **Operations Management Suite** > **Elenco dei servizi**.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-166">You can edit or delete the configured workspace through the **Service Map Overview** pane (**Administration** pane > **Operations Management Suite** > **Service Map**).</span></span> <span data-ttu-id="cb5f7-167">Attualmente è possibile configurare una sola area di lavoro di Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-167">You can configure only one Operations Management Suite workspace for now.</span></span>

![Riquadro Modifica area di lavoro di Operations Manager](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a><span data-ttu-id="cb5f7-169">Configurare regole e override</span><span class="sxs-lookup"><span data-stu-id="cb5f7-169">Configure rules and overrides</span></span>
<span data-ttu-id="cb5f7-170">Viene creata una regola _Microsoft.SystemCenter.ServiceMapImport.Rule_ per recuperare periodicamente le informazioni da Elenco dei servizi.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-170">A rule, _Microsoft.SystemCenter.ServiceMapImport.Rule_, is created to periodically fetch information from Service Map.</span></span> <span data-ttu-id="cb5f7-171">Per modificare gli intervalli di sincronizzazione è possibile configurare gli override della regola (riquadro **Tecnologie** > **Regole** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span><span class="sxs-lookup"><span data-stu-id="cb5f7-171">To change sync timings, you can configure overrides of the rule (**Authoring** pane > **Rules** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span></span>

![Finestra delle proprietà di override di Operations Manager](media/oms-service-map/scom-overrides.png)

* <span data-ttu-id="cb5f7-173">**Enabled**: abilita/disabilita gli aggiornamenti automatici.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-173">**Enabled**: Enable or disable automatic updates.</span></span> 
* <span data-ttu-id="cb5f7-174">**IntervalMinutes**: reimposta l'intervallo tra gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-174">**IntervalMinutes**: Reset the time between updates.</span></span> <span data-ttu-id="cb5f7-175">L'intervallo predefinito è un'ora.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-175">The default interval is one hour.</span></span> <span data-ttu-id="cb5f7-176">Se si desidera sincronizzare le mappe dei server più di frequente, è possibile modificare il valore.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-176">If you want to sync server maps more frequently, you can change the value.</span></span>
* <span data-ttu-id="cb5f7-177">**TimeoutSeconds**: reimposta l'intervallo di tempo prima che la richiesta raggiunga il timeout.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-177">**TimeoutSeconds**: Reset the length of time before the request times out.</span></span> 
* <span data-ttu-id="cb5f7-178">**TimeWindowMinutes**: reimposta l'intervallo di tempo per eseguire query sui dati.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-178">**TimeWindowMinutes**: Reset the time window for querying data.</span></span> <span data-ttu-id="cb5f7-179">Il valore predefinito è una finestra temporale di 60 minuti.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-179">Default is a 60-minute window.</span></span> <span data-ttu-id="cb5f7-180">Il valore massimo consentito da Elenco dei servizi è 60 minuti.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-180">The maximum value allowed by Service Map is 60 minutes.</span></span>

## <a name="known-issues-and-limitations"></a><span data-ttu-id="cb5f7-181">Problemi noti e limitazioni</span><span class="sxs-lookup"><span data-stu-id="cb5f7-181">Known issues and limitations</span></span>

<span data-ttu-id="cb5f7-182">La progettazione attuale presenta i problemi e le limitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="cb5f7-182">The current design presents the following issues and limitations:</span></span>
* <span data-ttu-id="cb5f7-183">È possibile connettersi a una sola area di lavoro di Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-183">You can only connect to a single Operations Management Suite workspace.</span></span>
* <span data-ttu-id="cb5f7-184">Anche se è possibile aggiungere manualmente server al gruppo di server di Mapping dei servizi tramite il riquadro **Creazione e modifica**, le mappe di tali server non vengono sincronizzate immediatamente.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-184">Although you can add servers to the Service Map Servers Group manually through the **Authoring** pane, the maps for those servers are not synced immediately.</span></span>  <span data-ttu-id="cb5f7-185">Verranno sincronizzate da Mapping dei servizi durante il ciclo di sincronizzazione successivo.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-185">They will be synced from Service Map during the next sync cycle.</span></span>
* <span data-ttu-id="cb5f7-186">Se si apportano modifiche ai diagrammi applicazioni distribuite creati dal Management Pack, tali modifiche verranno probabilmente sovrascritte durante la sincronizzazione successiva con Mapping dei servizi.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-186">If you make any changes to the Distributed Application Diagrams created by the management pack, those changes will likely be overwritten on the next sync with Service Map.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="cb5f7-187">Creare un’entità servizio</span><span class="sxs-lookup"><span data-stu-id="cb5f7-187">Create a service principal</span></span>
<span data-ttu-id="cb5f7-188">Per la documentazione ufficiale di Azure sulla creazione di un'entità servizio, vedere:</span><span class="sxs-lookup"><span data-stu-id="cb5f7-188">For official Azure documentation about creating a service principal, see:</span></span>
* <span data-ttu-id="cb5f7-189">[Create a service principal by using PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal) (Creare un'entità servizio usando PowerShell)</span><span class="sxs-lookup"><span data-stu-id="cb5f7-189">[Create a service principal by using PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)</span></span>
* <span data-ttu-id="cb5f7-190">[Create a service principal by using Azure CLI](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli) (Creare un'entità servizio usando Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="cb5f7-190">[Create a service principal by using Azure CLI](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)</span></span>
* <span data-ttu-id="cb5f7-191">[Create a service principal by using the Azure portal](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal) (Creare un'entità servizio usando il portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="cb5f7-191">[Create a service principal by using the Azure portal](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)</span></span>

### <a name="feedback"></a><span data-ttu-id="cb5f7-192">Commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="cb5f7-192">Feedback</span></span>
<span data-ttu-id="cb5f7-193">Per inviare commenti su Mapping dei servizi e sulla relativa documentazione,</span><span class="sxs-lookup"><span data-stu-id="cb5f7-193">Do you have any feedback for us about Service Map or this documentation?</span></span> <span data-ttu-id="cb5f7-194">Vedere la [pagina per i suggerimenti degli utenti](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), in cui è possibile suggerire funzionalità o votare i suggerimenti esistenti.</span><span class="sxs-lookup"><span data-stu-id="cb5f7-194">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote on existing suggestions.</span></span>
