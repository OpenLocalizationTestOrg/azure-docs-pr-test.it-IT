---
title: aaaConnect Windows computer tooAzure Log Analitica | Documenti Microsoft
description: Questo articolo illustra i computer Windows hello passaggi tooconnect hello nel toohello infrastruttura on-premise servizio Analitica Log utilizzando una versione personalizzata di hello Microsoft Monitoring Agent (MMA).
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a><span data-ttu-id="046cc-103">Connettere i computer toohello Log Analitica servizio Windows Azure</span><span class="sxs-lookup"><span data-stu-id="046cc-103">Connect Windows computers toohello Log Analytics service in Azure</span></span>

<span data-ttu-id="046cc-104">Questo articolo illustra i passaggi di hello i computer Windows tooconnect nelle aree di lavoro tooOMS infrastruttura locale utilizzando una versione personalizzata di hello Microsoft Monitoring Agent (MMA).</span><span class="sxs-lookup"><span data-stu-id="046cc-104">This article shows hello steps tooconnect Windows computers in your on-premises infrastructure tooOMS workspaces by using a customized version of hello Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="046cc-105">È necessario tooinstall e collegare gli agenti per tutti i computer hello che si desidera tooonboard affinché possano toosend data toohello Log Analitica e tooview e agire su tali dati.</span><span class="sxs-lookup"><span data-stu-id="046cc-105">You need tooinstall and connect agents for all of hello computers that you want tooonboard in order for them toosend data toohello Log Analytics service and tooview and act on that data.</span></span> <span data-ttu-id="046cc-106">Ogni agente può segnalare toomultiple aree di lavoro.</span><span class="sxs-lookup"><span data-stu-id="046cc-106">Each agent can report toomultiple workspaces.</span></span>

<span data-ttu-id="046cc-107">È possibile installare gli agenti tramite il programma di installazione, la riga di comando o con Configurazione dello stato desiderato in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="046cc-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="046cc-108">Per le macchine virtuali in esecuzione in Azure, è possibile semplificare l'installazione utilizzando hello [estensione della macchina virtuale](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="046cc-108">For virtual machines running in Azure, you can simplify installation by using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="046cc-109">Nei computer con connettività Internet, l'agente hello utilizza hello connessione toohello Internet toosend dati tooOMS.</span><span class="sxs-lookup"><span data-stu-id="046cc-109">On computers with Internet connectivity, hello agent uses hello connection toohello Internet toosend data tooOMS.</span></span> <span data-ttu-id="046cc-110">Per i computer che non dispongono di connettività Internet, è possibile utilizzare un proxy o hello [OMS Gateway](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="046cc-110">For computers that do not have Internet connectivity, you can use a proxy or hello [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="046cc-111">Connette il tooOMS computer Windows è semplice con tre semplici passaggi:</span><span class="sxs-lookup"><span data-stu-id="046cc-111">Connecting your Windows computers tooOMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="046cc-112">Scaricare i file di programma di installazione dell'agente di hello dal portale OMS hello</span><span class="sxs-lookup"><span data-stu-id="046cc-112">Download hello agent setup file from hello OMS portal</span></span>
2. <span data-ttu-id="046cc-113">Installazione dell'agente di hello tramite il metodo hello che scelto</span><span class="sxs-lookup"><span data-stu-id="046cc-113">Install hello agent using hello method you choose</span></span>
3. <span data-ttu-id="046cc-114">Configurare l'agente di hello o aggiungere altre aree di lavoro, se necessario</span><span class="sxs-lookup"><span data-stu-id="046cc-114">Configure hello agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="046cc-115">Hello diagramma seguente mostra la relazione hello tra OMS e computer Windows dopo aver installato e configurato gli agenti.</span><span class="sxs-lookup"><span data-stu-id="046cc-115">hello following diagram shows hello relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="046cc-117">Se i criteri di sicurezza IT non consentono i computer su toohello di tooconnect la rete Internet, è possibile configurare il toohello tooconnect computer Gateway OMS.</span><span class="sxs-lookup"><span data-stu-id="046cc-117">If your IT security policies do not allow computers on your network tooconnect toohello Internet, you can configure your computers tooconnect toohello OMS Gateway.</span></span> <span data-ttu-id="046cc-118">Per ulteriori informazioni e procedure su come tooconfigure toocommunicate del server tramite un servizio OMS toohello Gateway OMS, vedere [connettersi tooOMS computer tramite Gateway OMS hello](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="046cc-118">For more information and steps on how tooconfigure your servers toocommunicate through an OMS Gateway toohello OMS service, see [Connect computers tooOMS using hello OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="046cc-119">Requisiti di sistema e configurazione richiesta</span><span class="sxs-lookup"><span data-stu-id="046cc-119">System requirements and required configuration</span></span>
<span data-ttu-id="046cc-120">Prima di installare o distribuire gli agenti, esaminare hello seguenti siano soddisfatti i requisiti di hello tooensure di dettagli.</span><span class="sxs-lookup"><span data-stu-id="046cc-120">Before you install or deploy agents, review hello following details tooensure you meet hello requirements.</span></span>

- <span data-ttu-id="046cc-121">È possibile installare solo hello OMS MMA su computer che eseguono Windows Server 2008 SP 1 o versioni successive o Windows 7 SP1 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="046cc-121">You can only install hello OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="046cc-122">È necessaria una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="046cc-122">You need an Azure subscription.</span></span>  <span data-ttu-id="046cc-123">Per altre informazioni, vedere [Introduzione a Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="046cc-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="046cc-124">Ogni computer Windows deve essere in grado di tooconnect toohello Internet utilizzando HTTPS o toohello OMS Gateway.</span><span class="sxs-lookup"><span data-stu-id="046cc-124">Each Windows computer must be able tooconnect toohello Internet using HTTPS or toohello OMS Gateway.</span></span> <span data-ttu-id="046cc-125">La connessione può essere direttamente tramite un proxy, o hello OMS Gateway.</span><span class="sxs-lookup"><span data-stu-id="046cc-125">This connection can be direct, via a proxy, or through hello OMS Gateway.</span></span>
- <span data-ttu-id="046cc-126">È possibile installare hello MMA OMS in computer autonomi, server e macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="046cc-126">You can install hello OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="046cc-127">Se si desidera tooconnect tooOMS di macchine virtuali ospitate di Azure, vedere [tooLog di macchine virtuali di Azure connettersi Analitica](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="046cc-127">If you want tooconnect Azure-hosted virtual machines tooOMS, see [Connect Azure virtual machines tooLog Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="046cc-128">agente di Hello deve toouse la porta TCP 443 per varie risorse.</span><span class="sxs-lookup"><span data-stu-id="046cc-128">hello agent needs toouse TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="046cc-129">Rete</span><span class="sxs-lookup"><span data-stu-id="046cc-129">Network</span></span>

<span data-ttu-id="046cc-130">È necessario che Windows agenti tooconnect tooand registro servizio OMS hello, accedere alle risorse di toonetwork, inclusi i numeri di porta hello e gli URL di dominio.</span><span class="sxs-lookup"><span data-stu-id="046cc-130">For Windows agents tooconnect tooand register with hello OMS service, they must have access toonetwork resources, including hello port numbers and domain URLs.</span></span>

- <span data-ttu-id="046cc-131">Per i server proxy, è necessario tooensure che hello server proxy corretto le risorse vengono configurate nelle impostazioni dell'agente.</span><span class="sxs-lookup"><span data-stu-id="046cc-131">For proxy servers, you need tooensure that hello appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="046cc-132">Per i firewall che limitano l'accesso toohello Internet, si o ai tecnici di rete necessario tooconfigure tooOMS di accesso toopermit il firewall.</span><span class="sxs-lookup"><span data-stu-id="046cc-132">For firewalls that restrict access toohello Internet, you or your networking engineers need tooconfigure your firewall toopermit access tooOMS.</span></span> <span data-ttu-id="046cc-133">Non è necessaria alcuna azione sulle impostazioni dell'agente.</span><span class="sxs-lookup"><span data-stu-id="046cc-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="046cc-134">Hello nella tabella seguente mostra le risorse necessarie per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="046cc-134">hello following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="046cc-135">Alcune delle seguenti risorse hello citati di Operational Insights, che è stato un nome precedente di Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="046cc-135">Some of hello following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="046cc-136">Risorsa agente</span><span class="sxs-lookup"><span data-stu-id="046cc-136">Agent Resource</span></span> | <span data-ttu-id="046cc-137">Porte</span><span class="sxs-lookup"><span data-stu-id="046cc-137">Ports</span></span> | <span data-ttu-id="046cc-138">Ignorare l'analisi HTTPS</span><span class="sxs-lookup"><span data-stu-id="046cc-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="046cc-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="046cc-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="046cc-140">443</span><span class="sxs-lookup"><span data-stu-id="046cc-140">443</span></span> | <span data-ttu-id="046cc-141">Sì</span><span class="sxs-lookup"><span data-stu-id="046cc-141">Yes</span></span> |
| <span data-ttu-id="046cc-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="046cc-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="046cc-143">443</span><span class="sxs-lookup"><span data-stu-id="046cc-143">443</span></span> | <span data-ttu-id="046cc-144">Sì</span><span class="sxs-lookup"><span data-stu-id="046cc-144">Yes</span></span> |
| <span data-ttu-id="046cc-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="046cc-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="046cc-146">443</span><span class="sxs-lookup"><span data-stu-id="046cc-146">443</span></span> | <span data-ttu-id="046cc-147">Sì</span><span class="sxs-lookup"><span data-stu-id="046cc-147">Yes</span></span> |
| <span data-ttu-id="046cc-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="046cc-148">*.azure-automation.net</span></span> | <span data-ttu-id="046cc-149">443</span><span class="sxs-lookup"><span data-stu-id="046cc-149">443</span></span> | <span data-ttu-id="046cc-150">Sì</span><span class="sxs-lookup"><span data-stu-id="046cc-150">Yes</span></span> |



## <a name="download-hello-agent-setup-file-from-oms"></a><span data-ttu-id="046cc-151">Scaricare i file di programma di installazione dell'agente di hello da OMS</span><span class="sxs-lookup"><span data-stu-id="046cc-151">Download hello agent setup file from OMS</span></span>
1. <span data-ttu-id="046cc-152">Nel portale di OMS hello in hello **Panoramica** pagina, fare clic su hello **impostazioni** riquadro.</span><span class="sxs-lookup"><span data-stu-id="046cc-152">In hello OMS portal, on hello **Overview** page, click hello **Settings** tile.</span></span>  <span data-ttu-id="046cc-153">Fare clic su hello **Connected Sources** scheda nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="046cc-153">Click hello **Connected Sources** tab at hello top.</span></span>  
    <span data-ttu-id="046cc-154">![Scheda Origini connesse](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="046cc-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="046cc-155">Fare clic su **server Windows** e quindi fare clic su **Download Windows Agent** file di installazione di tooyour applicabile computer processore tipo toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="046cc-155">Click **Windows Servers** and then click **Download Windows Agent** applicable tooyour computer processor type toodownload hello setup file.</span></span>
3. <span data-ttu-id="046cc-156">In hello destra **ID area di lavoro**, fare clic sull'icona di hello copia e Incolla hello ID nel blocco note.</span><span class="sxs-lookup"><span data-stu-id="046cc-156">On hello right of **Workspace ID**, click hello copy icon and paste hello ID into Notepad.</span></span>
4. <span data-ttu-id="046cc-157">In hello destra **chiave primaria**, fare clic sull'icona di copia hello e incollare la chiave hello nel blocco note.</span><span class="sxs-lookup"><span data-stu-id="046cc-157">On hello right of **Primary Key**, click hello copy icon and paste hello key into Notepad.</span></span>     

## <a name="install-hello-agent-using-setup"></a><span data-ttu-id="046cc-158">Installazione dell'agente di hello tramite il programma di installazione</span><span class="sxs-lookup"><span data-stu-id="046cc-158">Install hello agent using setup</span></span>
1. <span data-ttu-id="046cc-159">Esecuzione agente hello tooinstall di programma di installazione in un computer che si desidera toomanage.</span><span class="sxs-lookup"><span data-stu-id="046cc-159">Run Setup tooinstall hello agent on a computer that you want toomanage.</span></span>
2. <span data-ttu-id="046cc-160">Nella pagina di benvenuto hello, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="046cc-160">On hello Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="046cc-161">Nella pagina condizioni di licenza hello leggere hello di licenza e quindi fare clic su **accetto**.</span><span class="sxs-lookup"><span data-stu-id="046cc-161">On hello License Terms page, read hello license and then click **I Agree**.</span></span>
4. <span data-ttu-id="046cc-162">Nella pagina di destinazione cartella hello, modificare o mantenere una cartella di installazione predefinita di hello e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="046cc-162">On hello Destination Folder page, change or keep hello default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="046cc-163">Nella pagina di opzioni di installazione agente hello, è possibile scegliere tooAzure tooconnect agente hello Analitica Log (OMS), Operations Manager, oppure è possibile omettere le scelte di hello se si desidera agente hello tooconfigure in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="046cc-163">On hello Agent Setup Options page, you can choose tooconnect hello agent tooAzure Log Analytics (OMS), Operations Manager, or you can leave hello choices blank if you want tooconfigure hello agent later.</span></span> <span data-ttu-id="046cc-164">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="046cc-164">Click **Next**.</span></span>   
    - <span data-ttu-id="046cc-165">Se si sceglie tooconnect tooAzure Analitica Log (OMS), incollare hello **ID area di lavoro** e **chiave dell'area di lavoro (chiave primaria)** copiati nel blocco note nella procedura precedente hello e quindi fare clic su  **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="046cc-165">If you chose tooconnect tooAzure Log Analytics (OMS), paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in hello previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="046cc-166">![incollare ID area di lavoro e chiave primaria](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="046cc-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="046cc-167">Se si sceglie tooconnect tooOperations Manager, digitare hello **nome gruppo di gestione**, **Server di gestione** nome, e **porta Server di gestione**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="046cc-167">If you chose tooconnect tooOperations Manager, type hello **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="046cc-168">Nella pagina Account azione agente hello, scegliere l'account di sistema locale hello o un account di dominio locale e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="046cc-168">On hello Agent Action Account page, choose either hello Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="046cc-169">![Configurazione del gruppo di gestione](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="046cc-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="046cc-170">Nella pagina Pronto tooInstall hello, rivedere le scelte effettuate e quindi fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="046cc-170">On hello Ready tooInstall page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="046cc-171">Pagina Configurazione completata hello, fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="046cc-171">On hello Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="046cc-172">Al termine, hello **Microsoft Monitoring Agent** viene visualizzato **Pannello di controllo**.</span><span class="sxs-lookup"><span data-stu-id="046cc-172">When complete, hello **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="046cc-173">È possibile verificare la configurazione non esiste e verificare che l'agente di hello è connesso tooOperational Insights (OMS).</span><span class="sxs-lookup"><span data-stu-id="046cc-173">You can review your configuration there and verify that hello agent is connected tooOperational Insights (OMS).</span></span> <span data-ttu-id="046cc-174">Quando connesso tooOMS, hello agente viene visualizzato un messaggio che informa: **hello Microsoft Monitoring Agent è connesso correttamente il servizio di Microsoft Operations Management Suite toohello.**</span><span class="sxs-lookup"><span data-stu-id="046cc-174">When connected tooOMS, hello agent displays a message stating: **hello Microsoft Monitoring Agent has successfully connected toohello Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="046cc-175">Configurare le impostazioni proxy</span><span class="sxs-lookup"><span data-stu-id="046cc-175">Configure proxy settings</span></span>

<span data-ttu-id="046cc-176">È possibile utilizzare hello seguendo le impostazioni di proxy tooconfigure di procedure per hello Microsoft Monitoring Agent tramite il pannello di controllo.</span><span class="sxs-lookup"><span data-stu-id="046cc-176">You can use hello following procedure tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="046cc-177">È necessario toouse questa procedura per ogni server.</span><span class="sxs-lookup"><span data-stu-id="046cc-177">You need toouse this procedure for each server.</span></span> <span data-ttu-id="046cc-178">Se si dispone di molti server, che è necessario tooconfigure, può risultare più semplice toouse un tooautomate script questo processo.</span><span class="sxs-lookup"><span data-stu-id="046cc-178">If you have many servers that you need tooconfigure, you might find it easier toouse a script tooautomate this process.</span></span> <span data-ttu-id="046cc-179">In questo caso, vedere la procedura successiva hello [tooconfigure impostazioni del proxy per Microsoft Monitoring Agent tramite uno script hello](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span><span class="sxs-lookup"><span data-stu-id="046cc-179">If so, see hello next procedure [tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="046cc-180">impostazioni di proxy tooconfigure per hello Microsoft Monitoring Agent tramite il pannello di controllo</span><span class="sxs-lookup"><span data-stu-id="046cc-180">tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="046cc-181">Aprire il **Pannello di controllo**.</span><span class="sxs-lookup"><span data-stu-id="046cc-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="046cc-182">Aprire **Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="046cc-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="046cc-183">Fare clic su hello **le impostazioni del Proxy** scheda.</span><span class="sxs-lookup"><span data-stu-id="046cc-183">Click hello **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="046cc-184">![Scheda Impostazioni proxy](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="046cc-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="046cc-185">Selezionare **utilizza un server proxy** e digitare l'URL di hello e numero di porta, se necessario, in modo analogo toohello esempio illustrato.</span><span class="sxs-lookup"><span data-stu-id="046cc-185">Select **Use a proxy server** and type hello URL and port number, if one is needed, similar toohello example shown.</span></span> <span data-ttu-id="046cc-186">Se il server proxy richiede l'autenticazione, digitare hello nome utente e password tooaccess hello server proxy.</span><span class="sxs-lookup"><span data-stu-id="046cc-186">If your proxy server requires authentication, type hello username and password tooaccess hello proxy server.</span></span>


### <a name="verify-agent-connectivity-toooms"></a><span data-ttu-id="046cc-187">Verificare tooOMS di connettività agente</span><span class="sxs-lookup"><span data-stu-id="046cc-187">Verify agent connectivity tooOMS</span></span>

<span data-ttu-id="046cc-188">È possibile verificare facilmente se gli agenti comunicano con OMS con hello seguente procedura:</span><span class="sxs-lookup"><span data-stu-id="046cc-188">You can easily verify whether your agents are communicating with OMS using hello following procedure:</span></span>

1.  <span data-ttu-id="046cc-189">Nel computer di hello con agente di Windows hello, aprire Pannello di controllo.</span><span class="sxs-lookup"><span data-stu-id="046cc-189">On hello computer with hello Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="046cc-190">Aprire Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="046cc-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="046cc-191">Fare clic sulla scheda di hello Analitica Log di Azure (OMS).</span><span class="sxs-lookup"><span data-stu-id="046cc-191">Click hello Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="046cc-192">Nella colonna Stato hello, dovrebbe essere che l'agente di hello stabilita la connessione del servizio Operations Management Suite toohello.</span><span class="sxs-lookup"><span data-stu-id="046cc-192">In hello Status column, you should see that hello agent connected successfully toohello Operations Management Suite service.</span></span>

![agente connesso](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="046cc-194">impostazioni di proxy tooconfigure per hello Microsoft Monitoring Agent tramite uno script</span><span class="sxs-lookup"><span data-stu-id="046cc-194">tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="046cc-195">Copiare hello seguente esempio, aggiornarlo con l'ambiente specifico tooyour informazioni, salvarlo con un'estensione di file PS1 e quindi eseguire script hello in ogni computer che si connette direttamente servizio OMS toohello.</span><span class="sxs-lookup"><span data-stu-id="046cc-195">Copy hello following sample, update it with information specific tooyour environment, save it with a PS1 file name extension, and then run hello script on each computer that connects directly toohello OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a><span data-ttu-id="046cc-196">Installazione dell'agente di hello tramite riga di comando hello</span><span class="sxs-lookup"><span data-stu-id="046cc-196">Install hello agent using hello command line</span></span>
- <span data-ttu-id="046cc-197">Modificare e quindi utilizzare hello seguente agente hello tooinstall di esempio tramite la riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="046cc-197">Modify and then use hello following example tooinstall hello agent using hello command line.</span></span> <span data-ttu-id="046cc-198">esempio Hello esegue un'installazione completamente invisibile all'utente.</span><span class="sxs-lookup"><span data-stu-id="046cc-198">hello example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="046cc-199">Se si desidera tooupgrade un agente, è necessario toouse hello Log Analitica API di scripting.</span><span class="sxs-lookup"><span data-stu-id="046cc-199">If you want tooupgrade an agent, you need toouse hello Log Analytics scripting API.</span></span> <span data-ttu-id="046cc-200">Vedere hello successiva sezione tooupgrade un agente.</span><span class="sxs-lookup"><span data-stu-id="046cc-200">See hello next section tooupgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="046cc-201">agente Hello utilizza IExpress come il programma di autoestrazione utilizzando hello `/c` comando.</span><span class="sxs-lookup"><span data-stu-id="046cc-201">hello agent uses IExpress as its self-extractor using hello `/c` command.</span></span> <span data-ttu-id="046cc-202">È possibile visualizzare i parametri della riga di comando di hello in [della riga di comando per IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) e quindi aggiornamento hello esempio toosuit le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="046cc-202">You can see hello command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update hello example toosuit your needs.</span></span>

|<span data-ttu-id="046cc-203">Opzioni specifiche di MMA</span><span class="sxs-lookup"><span data-stu-id="046cc-203">MMA-specific options</span></span>                   |<span data-ttu-id="046cc-204">Note</span><span class="sxs-lookup"><span data-stu-id="046cc-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="046cc-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="046cc-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="046cc-206">1 = l'area di lavoro Configura hello agente tooreport tooa</span><span class="sxs-lookup"><span data-stu-id="046cc-206">1 = Configure hello agent tooreport tooa workspace</span></span>                |
|<span data-ttu-id="046cc-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="046cc-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="046cc-208">Id area di lavoro (guid) per hello dell'area di lavoro tooadd</span><span class="sxs-lookup"><span data-stu-id="046cc-208">Workspace Id (guid) for hello workspace tooadd</span></span>                    |
|<span data-ttu-id="046cc-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="046cc-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="046cc-210">Eseguire l'autenticazione tooinitially utilizzato chiave dell'area di lavoro con area di lavoro hello</span><span class="sxs-lookup"><span data-stu-id="046cc-210">Workspace key used tooinitially authenticate with hello workspace</span></span> |
|<span data-ttu-id="046cc-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="046cc-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="046cc-212">Specificare l'ambiente cloud hello in cui si trova l'area di lavoro hello</span><span class="sxs-lookup"><span data-stu-id="046cc-212">Specify hello cloud environment where hello workspace is located</span></span> <br> <span data-ttu-id="046cc-213">0 = Cloud commerciale di Azure (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="046cc-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="046cc-214">1 = Azure per enti pubblici</span><span class="sxs-lookup"><span data-stu-id="046cc-214">1 = Azure Government</span></span> |
|<span data-ttu-id="046cc-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="046cc-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="046cc-216">URI per hello proxy toouse</span><span class="sxs-lookup"><span data-stu-id="046cc-216">URI for hello proxy toouse</span></span> |
|<span data-ttu-id="046cc-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="046cc-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="046cc-218">Nome utente tooaccess un proxy autenticato</span><span class="sxs-lookup"><span data-stu-id="046cc-218">Username tooaccess an authenticated proxy</span></span> |
|<span data-ttu-id="046cc-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="046cc-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="046cc-220">Password tooaccess un proxy autenticato</span><span class="sxs-lookup"><span data-stu-id="046cc-220">Password tooaccess an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="046cc-221">tooavoid che colpisce hello della riga di comando lunghezza massima di IExpress, installare agente hello con nessuna area di lavoro configurato e quindi usare una configurazione tooset script per area di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="046cc-221">tooavoid hitting hello command-line length limit of IExpress, install hello agent with no workspace configured and then use a script tooset configuration for hello workspace.</span></span>

>[!NOTE]
<span data-ttu-id="046cc-222">Se viene visualizzato un `Command line option syntax error.` quando si utilizza hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parametro, è possibile utilizzare hello seguente soluzione alternativa:</span><span class="sxs-lookup"><span data-stu-id="046cc-222">If you get a `Command line option syntax error.` when using hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use hello following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="046cc-223">Aggiungere un'area di lavoro usando uno script</span><span class="sxs-lookup"><span data-stu-id="046cc-223">Add a workspace using a script</span></span>
<span data-ttu-id="046cc-224">Aggiungere un'area di lavoro con API di scripting di hello Analitica Log agente hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="046cc-224">Add a workspace using hello Log Analytics agent scripting API with hello following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="046cc-225">tooadd un'area di lavoro in Azure per governo, hello utilizzare script di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="046cc-225">tooadd a workspace in Azure for US Government, use hello following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="046cc-226">Se si utilizza la riga di comando hello o script precedentemente tooinstall o configurare l'agente di hello, `EnableAzureOperationalInsights` è stato sostituito da `AddCloudWorkspace`.</span><span class="sxs-lookup"><span data-stu-id="046cc-226">If you've used hello command line or script previously tooinstall or configure hello agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="046cc-227">Installazione dell'agente di hello tramite DSC in automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="046cc-227">Install hello agent using DSC in Azure Automation</span></span>

<span data-ttu-id="046cc-228">È possibile utilizzare hello seguente agente hello tooinstall esempio di script con DSC in automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="046cc-228">You can use hello following script example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="046cc-229">esempio Hello installa hello agente a 64 bit, identificato da hello `URI` valore.</span><span class="sxs-lookup"><span data-stu-id="046cc-229">hello example installs hello 64-bit agent, identified by hello `URI` value.</span></span> <span data-ttu-id="046cc-230">È inoltre possibile utilizzare versione a 32 bit hello sostituendo il valore URI hello.</span><span class="sxs-lookup"><span data-stu-id="046cc-230">You can also use hello 32-bit version by replacing hello URI value.</span></span> <span data-ttu-id="046cc-231">Hello URI per entrambe le versioni sono:</span><span class="sxs-lookup"><span data-stu-id="046cc-231">hello URIs for both versions are:</span></span>

- <span data-ttu-id="046cc-232">Agente di Windows a 64 bit - https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="046cc-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="046cc-233">Agente di Windows a 32 bit - https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="046cc-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="046cc-234">La procedura e lo script di esempio riportati di seguito non determinano l'aggiornamento di un agente esistente.</span><span class="sxs-lookup"><span data-stu-id="046cc-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="046cc-235">Importare hello xPSDesiredStateConfiguration modulo DSC da [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) in automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="046cc-235">Import hello xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="046cc-236">Creare gli asset variabili di Automazione di Azure per *OPSINSIGHTS_WS_ID* e *OPSINSIGHTS_WS_KEY*.</span><span class="sxs-lookup"><span data-stu-id="046cc-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="046cc-237">Impostare *OPSINSIGHTS_WS_ID* ID area di lavoro di OMS Log Analitica tooyour e impostare *OPSINSIGHTS_WS_KEY* toohello chiave primaria dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="046cc-237">Set *OPSINSIGHTS_WS_ID* tooyour OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* toohello primary key of your workspace.</span></span>
3.  <span data-ttu-id="046cc-238">Utilizzare hello seguente script e salvarlo come MMAgent.ps1</span><span class="sxs-lookup"><span data-stu-id="046cc-238">Use hello following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="046cc-239">Modificare e quindi utilizzare hello seguente agente hello tooinstall di esempio con DSC in automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="046cc-239">Modify and then use hello following example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="046cc-240">Importare MMAgent.ps1 in automazione di Azure tramite l'interfaccia di automazione di Azure hello o un cmdlet.</span><span class="sxs-lookup"><span data-stu-id="046cc-240">Import MMAgent.ps1 into Azure Automation by using hello Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="046cc-241">Assegnare una configurazione di toohello del nodo.</span><span class="sxs-lookup"><span data-stu-id="046cc-241">Assign a node toohello configuration.</span></span> <span data-ttu-id="046cc-242">Entro 15 minuti, il nodo hello controlla la configurazione e hello MMA viene inserito il nodo toohello.</span><span class="sxs-lookup"><span data-stu-id="046cc-242">Within 15 minutes, hello node checks its configuration and hello MMA is pushed toohello node.</span></span>

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a><span data-ttu-id="046cc-243">Ottenere il valore ProductId più recente di hello</span><span class="sxs-lookup"><span data-stu-id="046cc-243">Get hello latest ProductId value</span></span>

<span data-ttu-id="046cc-244">Hello `ProductId value` in hello MMAgent.ps1 script è univoco tooeach versione dell'agente.</span><span class="sxs-lookup"><span data-stu-id="046cc-244">hello `ProductId value` in hello MMAgent.ps1 script is unique tooeach agent version.</span></span> <span data-ttu-id="046cc-245">Quando viene pubblicata una versione aggiornata di ogni agente, il valore di ProductId hello cambia.</span><span class="sxs-lookup"><span data-stu-id="046cc-245">When an updated version of each agent is published, hello ProductId value changes.</span></span> <span data-ttu-id="046cc-246">In tal caso, quando hello ProductId viene modificato in futuro hello, è possibile trovare la versione di agente hello utilizzando un semplice script.</span><span class="sxs-lookup"><span data-stu-id="046cc-246">So, when hello ProductId changes in hello future, you can find hello agent version using a simple script.</span></span> <span data-ttu-id="046cc-247">Dopo aver hello ultima versione dell'agente installato in un server di prova, è possibile utilizzare il valore di ProductId hello installato tooget script seguente hello.</span><span class="sxs-lookup"><span data-stu-id="046cc-247">After you have hello latest agent version installed on a test server, you can use hello following script tooget hello installed ProductId value.</span></span> <span data-ttu-id="046cc-248">Utilizza il valore ProductId più recente di hello, è possibile aggiornare il valore di hello in hello MMAgent.ps1 script.</span><span class="sxs-lookup"><span data-stu-id="046cc-248">Using hello latest ProductId value, you can update hello value in hello MMAgent.ps1 script.</span></span>

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="046cc-249">Configurare manualmente un agente o aggiungere nuove aree di lavoro</span><span class="sxs-lookup"><span data-stu-id="046cc-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="046cc-250">Se sono stati installati gli agenti, ma non sono stati configurati o se si desidera che le aree di lavoro di hello agente tooreport toomultiple, è possibile utilizzare hello seguente informazioni tooenable un agente o riconfigurarlo.</span><span class="sxs-lookup"><span data-stu-id="046cc-250">If you've installed agents but did not configure them or if you want hello agent tooreport toomultiple workspaces, you can use hello following information tooenable an agent or reconfigure it.</span></span> <span data-ttu-id="046cc-251">Dopo aver configurato l'agente hello, verrà registrato con il servizio agente hello e otterrà le informazioni di configurazione necessarie nonché i management pack che contengono informazioni sulla soluzione.</span><span class="sxs-lookup"><span data-stu-id="046cc-251">After you've configured hello agent, it will register with hello agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="046cc-252">Dopo aver installato Microsoft Monitoring Agent hello, aprire **Pannello di controllo**.</span><span class="sxs-lookup"><span data-stu-id="046cc-252">After you've installed hello Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="046cc-253">Aprire **Microsoft Monitoring Agent** e quindi fare clic su hello **Analitica Log di Azure (OMS)** scheda.</span><span class="sxs-lookup"><span data-stu-id="046cc-253">Open **Microsoft Monitoring Agent** and then click hello **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="046cc-254">Fare clic su **Aggiungi** tooopen hello **aggiungere un'area di lavoro Analitica Log** casella.</span><span class="sxs-lookup"><span data-stu-id="046cc-254">Click **Add** tooopen hello **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="046cc-255">Hello Incolla **ID area di lavoro** e **chiave dell'area di lavoro (chiave primaria)** copiati nel blocco note nella procedura precedente per hello area di lavoro che desidera tooadd e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="046cc-255">Paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for hello workspace that you want tooadd and then click **OK**.</span></span>  
    <span data-ttu-id="046cc-256">![Configurare Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="046cc-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="046cc-257">Dopo la raccolta dei dati dai computer monitorati dall'agente di hello, numero di hello di computer monitorati da OMS verrà visualizzato nel portale OMS hello in hello **Connected Sources** scheda **impostazioni** come  **Server collegati**.</span><span class="sxs-lookup"><span data-stu-id="046cc-257">After data is collected from computers monitored by hello agent, hello number of computers monitored by OMS will appear in hello OMS portal on hello **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="toodisable-an-agent"></a><span data-ttu-id="046cc-258">toodisable un agente</span><span class="sxs-lookup"><span data-stu-id="046cc-258">toodisable an agent</span></span>
1. <span data-ttu-id="046cc-259">Dopo aver installato l'agente di hello, aprire **Pannello di controllo**.</span><span class="sxs-lookup"><span data-stu-id="046cc-259">After installing hello agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="046cc-260">Aprire Microsoft Monitoring Agent e quindi fare clic su hello **Analitica Log di Azure (OMS)** scheda.</span><span class="sxs-lookup"><span data-stu-id="046cc-260">Open Microsoft Monitoring Agent and then click hello **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="046cc-261">Selezionare un'area di lavoro e quindi fare clic su **Rimuovi**.</span><span class="sxs-lookup"><span data-stu-id="046cc-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="046cc-262">Ripetere questo passaggio per tutte le altre aree di lavoro.</span><span class="sxs-lookup"><span data-stu-id="046cc-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="046cc-263">Facoltativamente, configurare il gruppo gestione Operations Manager di agenti tooreport tooan</span><span class="sxs-lookup"><span data-stu-id="046cc-263">Optionally, configure agents tooreport tooan Operations Manager management group</span></span>

<span data-ttu-id="046cc-264">Se si utilizza Operations Manager dell'infrastruttura IT, è possibile utilizzare anche l'agente MMA hello come un agente Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="046cc-264">If you use Operations Manager in your IT infrastructure, you can also use hello MMA agent as an Operations Manager agent.</span></span>

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="046cc-265">gruppo di gestione di tooconfigure MMA agenti tooreport tooan Operations Manager</span><span class="sxs-lookup"><span data-stu-id="046cc-265">tooconfigure MMA agents tooreport tooan Operations Manager management group</span></span>
1.  <span data-ttu-id="046cc-266">Nel computer in cui è installato l'agente di hello hello aprire **Pannello di controllo**.</span><span class="sxs-lookup"><span data-stu-id="046cc-266">On hello computer where hello agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="046cc-267">Aprire **Microsoft Monitoring Agent** e quindi fare clic su hello **Operations Manager** scheda.</span><span class="sxs-lookup"><span data-stu-id="046cc-267">Open **Microsoft Monitoring Agent** and then click hello **Operations Manager** tab.</span></span>  
    <span data-ttu-id="046cc-268">![Microsoft Monitoring Agent scheda Operations Manager](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="046cc-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="046cc-269">Se i server di Operations Manager sono configurati per l'integrazione con Active Directory, fare clic su **Aggiorna automaticamente assegnazioni gruppi di gestione da Servizi di dominio Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="046cc-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="046cc-270">Fare clic su **Aggiungi** tooopen hello **aggiungere un gruppo di gestione** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="046cc-270">Click **Add** tooopen hello **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="046cc-271">![Microsoft Monitoring Agent Aggiungi gruppo di gestione](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="046cc-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="046cc-272">In **nome gruppo di gestione** casella, il nome del tipo hello del gruppo di gestione.</span><span class="sxs-lookup"><span data-stu-id="046cc-272">In **Management group name** box, type hello name of your management group.</span></span>
6.  <span data-ttu-id="046cc-273">In hello **server di gestione primario** casella, il nome di computer tipo hello del server di gestione primario hello.</span><span class="sxs-lookup"><span data-stu-id="046cc-273">In hello **Primary management server** box, type hello computer name of hello primary management server.</span></span>
7.  <span data-ttu-id="046cc-274">In hello **porta server di gestione** casella, numero di porta TCP di tipo hello.</span><span class="sxs-lookup"><span data-stu-id="046cc-274">In hello **Management server port** box, type hello TCP port number.</span></span>
8.  <span data-ttu-id="046cc-275">In **Account azione agente**, scegliere l'account di sistema locale hello o un account di dominio locale.</span><span class="sxs-lookup"><span data-stu-id="046cc-275">Under **Agent Action Account**, choose either hello Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="046cc-276">Fare clic su **OK** tooclose hello **aggiungere un gruppo di gestione** la finestra di dialogo e quindi fare clic su **OK** tooclose hello **Microsoft Monitoring Agent proprietà**la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="046cc-276">Click **OK** tooclose hello **Add a Management Group** dialog box and then click **OK** tooclose hello **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="046cc-277">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="046cc-277">Next steps</span></span>

- <span data-ttu-id="046cc-278">[Aggiungere soluzioni Analitica Log da hello Solutions Gallery](log-analytics-add-solutions.md) tooadd funzionalità e raccolta dati.</span><span class="sxs-lookup"><span data-stu-id="046cc-278">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
