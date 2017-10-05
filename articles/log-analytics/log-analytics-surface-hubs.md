---
title: Monitorare dispositivi Surface Hub con Log Analytics di Azure | Documentazione Microsoft
description: "Usare la soluzione Surface Hub per monitorarne l'integrità e comprenderne la modalità d'uso."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6ecd0d09589fec85c1633f528afc1165c346b7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-to-track-their-health"></a><span data-ttu-id="d97a4-103">Monitorare dispositivi Surface Hub con Log Analytics per tracciare la loro integrità</span><span class="sxs-lookup"><span data-stu-id="d97a4-103">Monitor Surface Hubs with Log Analytics to track their health</span></span>

![Simbolo di Surface Hub](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

<span data-ttu-id="d97a4-105">In questo articolo viene descritto come usare la soluzione Surface Hub in Log Analytics per monitorare i dispositivi di Microsoft Surface Hub con Microsoft Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="d97a4-105">This article describes how you can use the Surface Hub solution in Log Analytics to monitor Microsoft Surface Hub devices with the Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="d97a4-106">Log Analytics aiuta a monitorare l'integrità di Surface Hub e comprenderne la modalità d'uso.</span><span class="sxs-lookup"><span data-stu-id="d97a4-106">Log Analytics helps you track the health of your Surface Hubs as well as understand how they are being used.</span></span>

<span data-ttu-id="d97a4-107">Per ogni soluzione Surface Hub viene installato il Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="d97a4-107">Each Surface Hub has the Microsoft Monitoring Agent installed.</span></span> <span data-ttu-id="d97a4-108">L'agente permette di trasferire i dati da Surface Hub a OMS.</span><span class="sxs-lookup"><span data-stu-id="d97a4-108">Its through the agent that you can send data from your Surface Hub to OMS.</span></span> <span data-ttu-id="d97a4-109">I file di log vengono letti da Surface Hub, per poi essere inviati al servizio OMS.</span><span class="sxs-lookup"><span data-stu-id="d97a4-109">Log files are read from your Surface Hubs and are then are sent to the OMS service.</span></span> <span data-ttu-id="d97a4-110">Nel dashboard di Surface Hub in OMS vengono mostrati i vari problemi, come lo stato offline dei server, il calendario non sincronizzato, o se l'account del dispositivo non riesce ad accedere a Skype.</span><span class="sxs-lookup"><span data-stu-id="d97a4-110">Issues like servers being offline, the calendar not syncing, or if the device account is unable to log into Skype are shown in OMS in the Surface Hub dashboard.</span></span> <span data-ttu-id="d97a4-111">Usando i dati presenti nel dashboard, è possibile identificare i dispositivi che non sono in esecuzione o che hanno altri problemi e, potenzialmente, è possibile apportare le opportune correzioni ai problemi rilevati.</span><span class="sxs-lookup"><span data-stu-id="d97a4-111">By using the data in the dashboard, you can identify devices that are not running, or that are having other problems, and potentially apply fixes for the detected issues.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="d97a4-112">Installazione e configurazione della soluzione</span><span class="sxs-lookup"><span data-stu-id="d97a4-112">Installing and configuring the solution</span></span>
<span data-ttu-id="d97a4-113">Usare le informazioni seguenti per installare e configurare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="d97a4-113">Use the following information to install and configure the solution.</span></span> <span data-ttu-id="d97a4-114">Per gestire Surface Hub da Microsoft Operations Management Suite (OMS), sono richiesti:</span><span class="sxs-lookup"><span data-stu-id="d97a4-114">In order to manage your Surface Hubs from the Microsoft Operations Management Suite (OMS), you'll need the following:</span></span>

* <span data-ttu-id="d97a4-115">Una sottoscrizione valida a [OMS](http://www.microsoft.com/oms).</span><span class="sxs-lookup"><span data-stu-id="d97a4-115">A valid subscription to [OMS](http://www.microsoft.com/oms).</span></span>
* <span data-ttu-id="d97a4-116">Un livello di [sottoscrizione OMS](https://azure.microsoft.com/pricing/details/log-analytics/) che supporta il numero di dispositivi che si desidera monitorare.</span><span class="sxs-lookup"><span data-stu-id="d97a4-116">An [OMS subscription](https://azure.microsoft.com/pricing/details/log-analytics/) level that will support the number of devices you want to monitor.</span></span> <span data-ttu-id="d97a4-117">I prezzi di OMS variano a seconda del numero dei dispositivi registrati e del volume di dati in elaborazione.</span><span class="sxs-lookup"><span data-stu-id="d97a4-117">OMS pricing varies depending on how many devices are enrolled, and how much data it processes.</span></span> <span data-ttu-id="d97a4-118">Tali aspetti devono essere presi in considerazione quando si pianifica la distribuzione di Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="d97a4-118">You'll want to take this into consideration when planning your Surface Hub rollout.</span></span>

<span data-ttu-id="d97a4-119">Successivamente, è possibile aggiungere una sottoscrizione OMS alla sottoscrizione Microsoft Azure esistente, oppure si può scegliere di creare una nuova area di lavoro direttamente tramite il portale di OMS.</span><span class="sxs-lookup"><span data-stu-id="d97a4-119">Next, you will either add an OMS subscription to your existing Microsoft Azure subscription or create a new workspace directly through the OMS portal.</span></span> <span data-ttu-id="d97a4-120">le istruzioni dettagliate per usare uno di questi metodi sono fornite nella sezione [Introduzione a Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d97a4-120">Detailed instructions for using either method is at [Get started with Log Analytics](log-analytics-get-started.md).</span></span> <span data-ttu-id="d97a4-121">Una volta impostata la sottoscrizione OMS, ci sono due modi per registrare i dispositivi di Surface Hub:</span><span class="sxs-lookup"><span data-stu-id="d97a4-121">Once the OMS subscription is set up, there are two ways to enroll your Surface Hub devices:</span></span>

* <span data-ttu-id="d97a4-122">Automaticamente tramite Intune</span><span class="sxs-lookup"><span data-stu-id="d97a4-122">Automatically through Intune</span></span>
* <span data-ttu-id="d97a4-123">Manualmente tramite **Impostazioni** sul dispositivo di Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="d97a4-123">Manually through **Settings** on your Surface Hub device.</span></span>

## <a name="set-up-monitoring"></a><span data-ttu-id="d97a4-124">Configurare il monitoraggio</span><span class="sxs-lookup"><span data-stu-id="d97a4-124">Set up monitoring</span></span>
<span data-ttu-id="d97a4-125">È possibile monitorare l'integrità e l'attività di Surface Hub con Log Analytics in OMS.</span><span class="sxs-lookup"><span data-stu-id="d97a4-125">You can monitor the health and activity of your Surface Hub using Log Analytics in OMS.</span></span> <span data-ttu-id="d97a4-126">È possibile registrare Surface Hub in OMS tramite Intune, oppure localmente usando **Impostazioni** in Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="d97a4-126">You can enroll the Surface Hub in OMS by using Intune, or locally by using **Settings** on the Surface Hub.</span></span>

## <a name="connect-surface-hubs-to-oms-through-intune"></a><span data-ttu-id="d97a4-127">Connettere i dispositivi Surface Hub a OMS tramite Intune</span><span class="sxs-lookup"><span data-stu-id="d97a4-127">Connect Surface Hubs to OMS through Intune</span></span>
<span data-ttu-id="d97a4-128">L'ID e la chiave dell'area di lavoro necessari per l'area di lavoro OMS incaricata di gestire Surface Hub</span><span class="sxs-lookup"><span data-stu-id="d97a4-128">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="d97a4-129">sono disponibili nel portale di OMS.</span><span class="sxs-lookup"><span data-stu-id="d97a4-129">You can get those from the OMS portal.</span></span>

<span data-ttu-id="d97a4-130">InTune è un prodotto Microsoft che consente di gestire centralmente le impostazioni di configurazione di OMS che si applicano a uno o più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="d97a4-130">Intune is a Microsoft product that allows you to centrally manage the OMS configuration settings that are applied to one or more of your devices.</span></span> <span data-ttu-id="d97a4-131">Seguire questa procedura per configurare i dispositivi tramite Intune:</span><span class="sxs-lookup"><span data-stu-id="d97a4-131">Follow these steps to configure your devices through Intune:</span></span>

1. <span data-ttu-id="d97a4-132">Accedere a Intune.</span><span class="sxs-lookup"><span data-stu-id="d97a4-132">Sign in to Intune.</span></span>
2. <span data-ttu-id="d97a4-133">Andare a **Impostazioni** > **Origini connesse**.</span><span class="sxs-lookup"><span data-stu-id="d97a4-133">Navigate to **Settings** > **Connected Sources**.</span></span>
3. <span data-ttu-id="d97a4-134">Creare o modificare un criterio basato sul modello di Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="d97a4-134">Create or edit a policy based on the Surface Hub template.</span></span>
4. <span data-ttu-id="d97a4-135">Andare alla sezione OMS (Azure Operational Insights) del criterio e aggiungere l'*ID area di lavoro* e la *Chiave area di lavoro* al criterio.</span><span class="sxs-lookup"><span data-stu-id="d97a4-135">Navigate to the OMS (Azure Operational Insights) section of the policy, and add the *Workspace ID* and *Workspace Key* to the policy.</span></span>
5. <span data-ttu-id="d97a4-136">Salvare il criterio.</span><span class="sxs-lookup"><span data-stu-id="d97a4-136">Save the policy.</span></span>
6. <span data-ttu-id="d97a4-137">Associare il criterio al gruppo di dispositivi appropriato.</span><span class="sxs-lookup"><span data-stu-id="d97a4-137">Associate the policy with the appropriate group of devices.</span></span>

   ![Criterio di Intune](./media/log-analytics-surface-hubs/intune.png)

<span data-ttu-id="d97a4-139">A questo punto, Intune sincronizza le impostazioni di OMS con i dispositivi nel gruppo di destinazione, registrandoli nell'area di lavoro di OMS.</span><span class="sxs-lookup"><span data-stu-id="d97a4-139">Intune then syncs the OMS settings with the devices in the target group, enrolling them in your OMS workspace.</span></span>

## <a name="connect-surface-hubs-to-oms-using-the-settings-app"></a><span data-ttu-id="d97a4-140">Connettere Surface Hub a OMS usando l'app Impostazioni</span><span class="sxs-lookup"><span data-stu-id="d97a4-140">Connect Surface Hubs to OMS using the Settings app</span></span>
<span data-ttu-id="d97a4-141">L'ID e la chiave dell'area di lavoro necessari per l'area di lavoro OMS incaricata di gestire Surface Hub</span><span class="sxs-lookup"><span data-stu-id="d97a4-141">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="d97a4-142">sono disponibili nel portale di OMS.</span><span class="sxs-lookup"><span data-stu-id="d97a4-142">You can get those from the OMS portal.</span></span>

<span data-ttu-id="d97a4-143">Se non si usa Intune per gestire l'ambiente, è possibile registrare i dispositivi manualmente tramite **Impostazioni** in ogni Surface Hub:</span><span class="sxs-lookup"><span data-stu-id="d97a4-143">If you don't use Intune to manage your environment, you can enroll devices manually through **Settings** on each Surface Hub:</span></span>

1. <span data-ttu-id="d97a4-144">Da Surface Hub aprire **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="d97a4-144">From your Surface Hub, open **Settings**.</span></span>
2. <span data-ttu-id="d97a4-145">Immettere le credenziali di amministratore del dispositivo quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="d97a4-145">Enter the device admin credentials when prompted.</span></span>
3. <span data-ttu-id="d97a4-146">Fare clic su **Questo dispositivo** e in **Monitoraggio** fare clic su **Configura impostazioni OMS**.</span><span class="sxs-lookup"><span data-stu-id="d97a4-146">Click **This device**, and the under **Monitoring**, click **Configure OMS Settings**.</span></span>
4. <span data-ttu-id="d97a4-147">Selezionare **Abilita monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="d97a4-147">Select **Enable monitoring**.</span></span>
5. <span data-ttu-id="d97a4-148">Nella finestra di dialogo Impostazioni di OMS, immetter l'**ID area di lavoro** e la **Chiave area di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="d97a4-148">In the OMS settings dialog, type the **Workspace ID** and type the **Workspace Key**.</span></span>  
   <span data-ttu-id="d97a4-149">![impostazioni](./media/log-analytics-surface-hubs/settings.png)</span><span class="sxs-lookup"><span data-stu-id="d97a4-149">![settings](./media/log-analytics-surface-hubs/settings.png)</span></span>
6. <span data-ttu-id="d97a4-150">Fare clic su **OK** per portare a termine la configurazione.</span><span class="sxs-lookup"><span data-stu-id="d97a4-150">Click **OK** to complete the configuration.</span></span>

<span data-ttu-id="d97a4-151">Un messaggio di conferma viene visualizzato per indicare il buon esito dell'operazione o l'eventuale presenza di errori.</span><span class="sxs-lookup"><span data-stu-id="d97a4-151">A confirmation appears telling you whether or not the OMS configuration was successfully applied to the device.</span></span> <span data-ttu-id="d97a4-152">Se la configurazione di OMS viene correttamente applicata al dispositivo, appare un messaggio per indicare che l'agente è connesso al servizio OMS.</span><span class="sxs-lookup"><span data-stu-id="d97a4-152">If it was, a message appears stating that the agent successfully connected to the OMS service.</span></span> <span data-ttu-id="d97a4-153">Il dispositivo inizia quindi a inviare dati a OMS dove possono essere visualizzati e gestiti secondo le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="d97a4-153">The device then starts sending data to OMS where you can view and act on it.</span></span>

## <a name="monitor-surface-hubs"></a><span data-ttu-id="d97a4-154">Monitorare Surface Hub</span><span class="sxs-lookup"><span data-stu-id="d97a4-154">Monitor Surface Hubs</span></span>
<span data-ttu-id="d97a4-155">Monitorare Surface Hub con OMS è molto simile all'attività di monitoraggio di qualsiasi altro dispositivo registrato.</span><span class="sxs-lookup"><span data-stu-id="d97a4-155">Monitoring your Surface Hubs using OMS is much like monitoring any other enrolled devices.</span></span>

1. <span data-ttu-id="d97a4-156">Accedere al portale di OMS.</span><span class="sxs-lookup"><span data-stu-id="d97a4-156">Sign in to the OMS portal.</span></span>
2. <span data-ttu-id="d97a4-157">Andare al dashboard del pacchetto della soluzione Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="d97a4-157">Navigate to the Surface Hub solution pack dashboard.</span></span>
3. <span data-ttu-id="d97a4-158">Viene visualizzata l'integrità del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d97a4-158">Your device's health is displayed.</span></span>

   ![Dashboard di Surface Hub](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

<span data-ttu-id="d97a4-160">È possibile creare [avvisi](log-analytics-alerts.md) in base alle ricerche log esistenti o personalizzate.</span><span class="sxs-lookup"><span data-stu-id="d97a4-160">You can create [alerts](log-analytics-alerts.md) based on existing or custom log searches.</span></span> <span data-ttu-id="d97a4-161">Con i dati che OMS ha raccolto da Surface Hub, è possibile cercare problemi e avvisi in base alle condizioni definite per i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="d97a4-161">Using the data the OMS collects from your Surface Hubs, you can search for issues and alert on the conditions that you define for your devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d97a4-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d97a4-162">Next steps</span></span>
* <span data-ttu-id="d97a4-163">Usare le [ricerche log in Log Analytics](log-analytics-log-searches.md) per visualizzare i dati dettagliati di Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="d97a4-163">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Surface Hub data.</span></span>
* <span data-ttu-id="d97a4-164">Creare [avvisi](log-analytics-alerts.md) che informano della presenza di problemi relativi a Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="d97a4-164">Create [alerts](log-analytics-alerts.md) to notify you when issues occur with your Surface Hubs.</span></span>
