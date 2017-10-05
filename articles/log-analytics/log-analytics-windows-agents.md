---
title: Connettere computer Windows a Log Analytics di Azure | Microsoft Docs
description: Questo articolo illustra i passaggi necessari per connettere i computer Windows dell'infrastruttura locale al servizio Log Analytics usando una versione personalizzata di Microsoft Monitoring Agent (MMA).
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
ms.openlocfilehash: 48a0eaeb10d406d551c9e5870edde06809bd7544
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-windows-computers-to-the-log-analytics-service-in-azure"></a><span data-ttu-id="296d5-103">Connettere computer Windows al servizio Log Analytics in Azure</span><span class="sxs-lookup"><span data-stu-id="296d5-103">Connect Windows computers to the Log Analytics service in Azure</span></span>

<span data-ttu-id="296d5-104">Questo articolo illustra i passaggi necessari per connettere i computer Windows dell'infrastruttura locale alle aree di lavoro di OMS usando una versione personalizzata di Microsoft Monitoring Agent (MMA).</span><span class="sxs-lookup"><span data-stu-id="296d5-104">This article shows the steps to connect Windows computers in your on-premises infrastructure to OMS workspaces by using a customized version of the Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="296d5-105">È necessario installare e connettere gli agenti per tutti i computer da caricare affinché possano inviare dati al servizio Log Analytics e visualizzare ed eseguire operazioni su tali dati.</span><span class="sxs-lookup"><span data-stu-id="296d5-105">You need to install and connect agents for all of the computers that you want to onboard in order for them to send data to the Log Analytics service and to view and act on that data.</span></span> <span data-ttu-id="296d5-106">Ogni agente può inviare report a più aree di lavoro.</span><span class="sxs-lookup"><span data-stu-id="296d5-106">Each agent can report to multiple workspaces.</span></span>

<span data-ttu-id="296d5-107">È possibile installare gli agenti tramite il programma di installazione, la riga di comando o con Configurazione dello stato desiderato in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="296d5-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="296d5-108">Per le macchine virtuali eseguite in Azure, è possibile semplificare l'installazione usando l'[estensione macchina virtuale](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="296d5-108">For virtual machines running in Azure, you can simplify installation by using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="296d5-109">Nei computer con connettività a Internet, l'agente usa la connessione a Internet per inviare dati a OMS.</span><span class="sxs-lookup"><span data-stu-id="296d5-109">On computers with Internet connectivity, the agent uses the connection to the Internet to send data to OMS.</span></span> <span data-ttu-id="296d5-110">Per i computer che non hanno connettività Internet, è possibile usare un proxy o il [gateway di OMS](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="296d5-110">For computers that do not have Internet connectivity, you can use a proxy or the [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="296d5-111">La connessione dei computer Windows a OMS è semplice e richiede solo tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="296d5-111">Connecting your Windows computers to OMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="296d5-112">Scaricare il file di installazione dell'agente dal portale di OMS</span><span class="sxs-lookup"><span data-stu-id="296d5-112">Download the agent setup file from the OMS portal</span></span>
2. <span data-ttu-id="296d5-113">Installare l'agente usando il metodo che scelto</span><span class="sxs-lookup"><span data-stu-id="296d5-113">Install the agent using the method you choose</span></span>
3. <span data-ttu-id="296d5-114">Configurare l'agente o aggiungere altre aree di lavoro, se necessario</span><span class="sxs-lookup"><span data-stu-id="296d5-114">Configure the agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="296d5-115">Il diagramma seguente illustra la relazione tra i computer Windows e OMS dopo l'installazione e la configurazione degli agenti.</span><span class="sxs-lookup"><span data-stu-id="296d5-115">The following diagram shows the relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="296d5-117">Se i criteri di protezione IT non consentono ai computer nella rete di connettersi a Internet, è possibile configurare i computer per connettersi al Gateway OMS.</span><span class="sxs-lookup"><span data-stu-id="296d5-117">If your IT security policies do not allow computers on your network to connect to the Internet, you can configure your computers to connect to the OMS Gateway.</span></span> <span data-ttu-id="296d5-118">Per altre informazioni e procedure per la configurazione dei server per la comunicazione tramite un gateway OMS con il servizio OMS, vedere [Connettere computer a OMS usando il gateway OMS](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="296d5-118">For more information and steps on how to configure your servers to communicate through an OMS Gateway to the OMS service, see [Connect computers to OMS using the OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="296d5-119">Requisiti di sistema e configurazione richiesta</span><span class="sxs-lookup"><span data-stu-id="296d5-119">System requirements and required configuration</span></span>
<span data-ttu-id="296d5-120">Prima di installare o distribuire gli agenti, esaminare i dettagli seguenti per assicurarsi che i requisiti siano soddisfatti.</span><span class="sxs-lookup"><span data-stu-id="296d5-120">Before you install or deploy agents, review the following details to ensure you meet the requirements.</span></span>

- <span data-ttu-id="296d5-121">È possibile installare MMA per OMS solo in computer che eseguono Windows Server 2008 Service Pack 1 o versione successiva oppure Windows 7 SP1 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="296d5-121">You can only install the OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="296d5-122">È necessaria una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="296d5-122">You need an Azure subscription.</span></span>  <span data-ttu-id="296d5-123">Per altre informazioni, vedere [Introduzione a Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="296d5-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="296d5-124">Ogni computer Windows deve potersi connettere a Internet tramite il protocollo HTTPS o il gateway di OMS.</span><span class="sxs-lookup"><span data-stu-id="296d5-124">Each Windows computer must be able to connect to the Internet using HTTPS or to the OMS Gateway.</span></span> <span data-ttu-id="296d5-125">Questa connessione può essere diretta, tramite un proxy o tramite il gateway di OMS.</span><span class="sxs-lookup"><span data-stu-id="296d5-125">This connection can be direct, via a proxy, or through the OMS Gateway.</span></span>
- <span data-ttu-id="296d5-126">È possibile installare MMA per OMS in computer autonomi, server e macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="296d5-126">You can install the OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="296d5-127">Per connettere a OMS le macchine virtuali ospitate da Azure, vedere l'articolo [Connettere macchine virtuali di Azure a Log Analytics](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="296d5-127">If you want to connect Azure-hosted virtual machines to OMS, see [Connect Azure virtual machines to Log Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="296d5-128">L'agente deve usare la porta TCP 443 per diverse risorse.</span><span class="sxs-lookup"><span data-stu-id="296d5-128">The agent needs to use TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="296d5-129">Rete</span><span class="sxs-lookup"><span data-stu-id="296d5-129">Network</span></span>

<span data-ttu-id="296d5-130">Per far sì che gli agenti di Windows si connettano e si registrino con il servizio OMS, devono avere accesso alle risorse di rete, compresi gli URL di dominio e i numeri di porta.</span><span class="sxs-lookup"><span data-stu-id="296d5-130">For Windows agents to connect to and register with the OMS service, they must have access to network resources, including the port numbers and domain URLs.</span></span>

- <span data-ttu-id="296d5-131">Per i server proxy, è necessario assicurarsi che le risorse del server proxy appropriate siano configurate nelle impostazioni dell'agente.</span><span class="sxs-lookup"><span data-stu-id="296d5-131">For proxy servers, you need to ensure that the appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="296d5-132">Per i firewall che limitano l'accesso a Internet, è necessario che l'utente o gli ingegneri di rete configurino il firewall per consentire l'accesso a OMS.</span><span class="sxs-lookup"><span data-stu-id="296d5-132">For firewalls that restrict access to the Internet, you or your networking engineers need to configure your firewall to permit access to OMS.</span></span> <span data-ttu-id="296d5-133">Non è necessaria alcuna azione sulle impostazioni dell'agente.</span><span class="sxs-lookup"><span data-stu-id="296d5-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="296d5-134">Nella tabella seguente vengono visualizzate le risorse necessarie per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="296d5-134">The following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="296d5-135">Alcune delle risorse seguenti fanno riferimento a Operational Insights, che era il nome precedente di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="296d5-135">Some of the following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="296d5-136">Risorsa agente</span><span class="sxs-lookup"><span data-stu-id="296d5-136">Agent Resource</span></span> | <span data-ttu-id="296d5-137">Porte</span><span class="sxs-lookup"><span data-stu-id="296d5-137">Ports</span></span> | <span data-ttu-id="296d5-138">Ignorare l'analisi HTTPS</span><span class="sxs-lookup"><span data-stu-id="296d5-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="296d5-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="296d5-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="296d5-140">443</span><span class="sxs-lookup"><span data-stu-id="296d5-140">443</span></span> | <span data-ttu-id="296d5-141">Sì</span><span class="sxs-lookup"><span data-stu-id="296d5-141">Yes</span></span> |
| <span data-ttu-id="296d5-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="296d5-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="296d5-143">443</span><span class="sxs-lookup"><span data-stu-id="296d5-143">443</span></span> | <span data-ttu-id="296d5-144">Sì</span><span class="sxs-lookup"><span data-stu-id="296d5-144">Yes</span></span> |
| <span data-ttu-id="296d5-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="296d5-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="296d5-146">443</span><span class="sxs-lookup"><span data-stu-id="296d5-146">443</span></span> | <span data-ttu-id="296d5-147">Sì</span><span class="sxs-lookup"><span data-stu-id="296d5-147">Yes</span></span> |
| <span data-ttu-id="296d5-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="296d5-148">*.azure-automation.net</span></span> | <span data-ttu-id="296d5-149">443</span><span class="sxs-lookup"><span data-stu-id="296d5-149">443</span></span> | <span data-ttu-id="296d5-150">Sì</span><span class="sxs-lookup"><span data-stu-id="296d5-150">Yes</span></span> |



## <a name="download-the-agent-setup-file-from-oms"></a><span data-ttu-id="296d5-151">Per scaricare il file di installazione dell'agente da OMS</span><span class="sxs-lookup"><span data-stu-id="296d5-151">Download the agent setup file from OMS</span></span>
1. <span data-ttu-id="296d5-152">Nella pagina **Panoramica** del portale di OMS fare clic sul riquadro **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="296d5-152">In the OMS portal, on the **Overview** page, click the **Settings** tile.</span></span>  <span data-ttu-id="296d5-153">Scegliere la scheda **Connected Sources** nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="296d5-153">Click the **Connected Sources** tab at the top.</span></span>  
    <span data-ttu-id="296d5-154">![Scheda Origini connesse](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="296d5-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="296d5-155">Fare clic su **Server Windows** e quindi fare clic su **Scarica agente Windows** applicabile al tipo di processore del computer per scaricare il file di installazione.</span><span class="sxs-lookup"><span data-stu-id="296d5-155">Click **Windows Servers** and then click **Download Windows Agent** applicable to your computer processor type to download the setup file.</span></span>
3. <span data-ttu-id="296d5-156">A destra di **ID area di lavoro**fare clic sull'icona di copia e incollare l'ID nel Blocco note.</span><span class="sxs-lookup"><span data-stu-id="296d5-156">On the right of **Workspace ID**, click the copy icon and paste the ID into Notepad.</span></span>
4. <span data-ttu-id="296d5-157">A destra di **Chiave primaria**fare clic sull'icona di copia e incollare la chiave nel Blocco note.</span><span class="sxs-lookup"><span data-stu-id="296d5-157">On the right of **Primary Key**, click the copy icon and paste the key into Notepad.</span></span>     

## <a name="install-the-agent-using-setup"></a><span data-ttu-id="296d5-158">Installare gli agenti con il programma di installazione</span><span class="sxs-lookup"><span data-stu-id="296d5-158">Install the agent using setup</span></span>
1. <span data-ttu-id="296d5-159">Eseguire il programma di installazione per installare l'agente in un computer da gestire.</span><span class="sxs-lookup"><span data-stu-id="296d5-159">Run Setup to install the agent on a computer that you want to manage.</span></span>
2. <span data-ttu-id="296d5-160">Nella pagina di benvenuto fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="296d5-160">On the Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="296d5-161">Nella pagina Condizioni di licenza leggere la licenza e quindi fare clic su **Accetto**.</span><span class="sxs-lookup"><span data-stu-id="296d5-161">On the License Terms page, read the license and then click **I Agree**.</span></span>
4. <span data-ttu-id="296d5-162">Nella pagina della cartella di destinazione modificare o mantenere la cartella di installazione predefinita e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="296d5-162">On the Destination Folder page, change or keep the default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="296d5-163">Nella pagina delle opzioni di installazione dell'agente è possibile scegliere di connettere l'agente ad Azure Log Analytics (OMS) o Operations Manager oppure di lasciare vuote le opzioni se si vuole configurare l'agente in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="296d5-163">On the Agent Setup Options page, you can choose to connect the agent to Azure Log Analytics (OMS), Operations Manager, or you can leave the choices blank if you want to configure the agent later.</span></span> <span data-ttu-id="296d5-164">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="296d5-164">Click **Next**.</span></span>   
    - <span data-ttu-id="296d5-165">Se si sceglie di connettersi ad Azure Log Analytics (OMS), incollare l'**ID area di lavoro** e la **chiave dell'area di lavoro (chiave primaria)** copiati nel Blocco note durante la procedura precedente e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="296d5-165">If you chose to connect to Azure Log Analytics (OMS), paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in the previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="296d5-166">![incollare ID area di lavoro e chiave primaria](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="296d5-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="296d5-167">Se si sceglie di connettersi a Operations Manager, digitare il **nome del gruppo di gestione**, il nome del **server di gestione** e la **porta del server di gestione** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="296d5-167">If you chose to connect to Operations Manager, type the **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="296d5-168">Nella pagina Account azione agente scegliere l'Account di sistema locale o un account di dominio locale e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="296d5-168">On the Agent Action Account page, choose either the Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="296d5-169">![configurazione del gruppo di gestione](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![account azione agente](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="296d5-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="296d5-170">Nella pagina Pronto per l'installazione rivedere le scelte effettuate e quindi fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="296d5-170">On the Ready to Install page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="296d5-171">Nella pagina Configurazione completata fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="296d5-171">On the Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="296d5-172">Al termine, verrà visualizzato **Microsoft Monitoring Agent** nel **Pannello di controllo**.</span><span class="sxs-lookup"><span data-stu-id="296d5-172">When complete, the **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="296d5-173">È possibile rivedere la configurazione e verificare che l'agente sia connesso a Operational Insights (OMS).</span><span class="sxs-lookup"><span data-stu-id="296d5-173">You can review your configuration there and verify that the agent is connected to Operational Insights (OMS).</span></span> <span data-ttu-id="296d5-174">Quando si è connessi a OMS, l'agente visualizza un messaggio nel quale è indicato che **Microsoft Monitoring Agent ha eseguito la connessione al servizio Microsoft Operations Management Suite.**</span><span class="sxs-lookup"><span data-stu-id="296d5-174">When connected to OMS, the agent displays a message stating: **The Microsoft Monitoring Agent has successfully connected to the Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="296d5-175">Configurare le impostazioni proxy</span><span class="sxs-lookup"><span data-stu-id="296d5-175">Configure proxy settings</span></span>

<span data-ttu-id="296d5-176">È possibile usare la procedura seguente per configurare le impostazioni proxy per Microsoft Monitoring Agent tramite il Pannello di controllo.</span><span class="sxs-lookup"><span data-stu-id="296d5-176">You can use the following procedure to configure proxy settings for the Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="296d5-177">È necessario ripetere la procedura per ogni server.</span><span class="sxs-lookup"><span data-stu-id="296d5-177">You need to use this procedure for each server.</span></span> <span data-ttu-id="296d5-178">Se è necessario configurare molti server, può risultare più semplice usare uno script per automatizzare il processo.</span><span class="sxs-lookup"><span data-stu-id="296d5-178">If you have many servers that you need to configure, you might find it easier to use a script to automate this process.</span></span> <span data-ttu-id="296d5-179">In questo caso, vedere la procedura seguente [Per configurare le impostazioni proxy per Microsoft Monitoring Agent tramite uno script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span><span class="sxs-lookup"><span data-stu-id="296d5-179">If so, see the next procedure [To configure proxy settings for the Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="296d5-180">Per configurare le impostazioni proxy per Microsoft Monitoring Agent tramite il Pannello di controllo</span><span class="sxs-lookup"><span data-stu-id="296d5-180">To configure proxy settings for the Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="296d5-181">Aprire il **Pannello di controllo**.</span><span class="sxs-lookup"><span data-stu-id="296d5-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="296d5-182">Aprire **Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="296d5-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="296d5-183">Fare clic sulla scheda **Impostazioni proxy**.</span><span class="sxs-lookup"><span data-stu-id="296d5-183">Click the **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="296d5-184">![Scheda Impostazioni proxy](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="296d5-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="296d5-185">Selezionare **Usa server proxy** e digitare l'URL e il numero di porta, se necessario, in modo analogo all'esempio illustrato.</span><span class="sxs-lookup"><span data-stu-id="296d5-185">Select **Use a proxy server** and type the URL and port number, if one is needed, similar to the example shown.</span></span> <span data-ttu-id="296d5-186">Se il server proxy richiede l'autenticazione, digitare il nome utente e la password per accedere al server proxy.</span><span class="sxs-lookup"><span data-stu-id="296d5-186">If your proxy server requires authentication, type the username and password to access the proxy server.</span></span>


### <a name="verify-agent-connectivity-to-oms"></a><span data-ttu-id="296d5-187">Verificare la connettività dell'agente a OMS</span><span class="sxs-lookup"><span data-stu-id="296d5-187">Verify agent connectivity to OMS</span></span>

<span data-ttu-id="296d5-188">È possibile verificare facilmente se gli agenti comunicano con OMS tramite la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="296d5-188">You can easily verify whether your agents are communicating with OMS using the following procedure:</span></span>

1.  <span data-ttu-id="296d5-189">Nel computer con l'agente di Windows, aprire il pannello di controllo.</span><span class="sxs-lookup"><span data-stu-id="296d5-189">On the computer with the Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="296d5-190">Aprire Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="296d5-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="296d5-191">Fare clic sulla scheda Azure Log Analytics (OMS).</span><span class="sxs-lookup"><span data-stu-id="296d5-191">Click the Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="296d5-192">Nella colonna dello stato, si dovrebbe vedere che l'agente si è connesso correttamente al servizio Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="296d5-192">In the Status column, you should see that the agent connected successfully to the Operations Management Suite service.</span></span>

![agente connesso](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="296d5-194">Per configurare le impostazioni proxy per Microsoft Monitoring Agent tramite uno script</span><span class="sxs-lookup"><span data-stu-id="296d5-194">To configure proxy settings for the Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="296d5-195">Copiare l'esempio seguente, aggiornarlo con le informazioni specifiche per l'ambiente, salvarlo con un'estensione di file PS1 ed eseguire lo script in ogni computer che si connette direttamente al servizio OMS.</span><span class="sxs-lookup"><span data-stu-id="296d5-195">Copy the following sample, update it with information specific to your environment, save it with a PS1 file name extension, and then run the script on each computer that connects directly to the OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get the Health Service configuration object.  We need to determine if we
    #have the right update rollup with the API we need.  If not, no need to run the rest of the script.
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

    Write-Output "Setting proxy to $ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-the-agent-using-the-command-line"></a><span data-ttu-id="296d5-196">Installare l'agente usando la riga di comando</span><span class="sxs-lookup"><span data-stu-id="296d5-196">Install the agent using the command line</span></span>
- <span data-ttu-id="296d5-197">Modificare e usare il seguente esempio per installare l'agente mediante la riga di comando.</span><span class="sxs-lookup"><span data-stu-id="296d5-197">Modify and then use the following example to install the agent using the command line.</span></span> <span data-ttu-id="296d5-198">L'esempio esegue un'installazione completamente automatica.</span><span class="sxs-lookup"><span data-stu-id="296d5-198">The example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="296d5-199">Per aggiornare un agente è necessario usare l'API di scripting di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="296d5-199">If you want to upgrade an agent, you need to use the Log Analytics scripting API.</span></span> <span data-ttu-id="296d5-200">La procedura per aggiornare un agente è descritta nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="296d5-200">See the next section to upgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="296d5-201">L'agente usa IExpress come programma di autoestrazione tramite il comando `/c`.</span><span class="sxs-lookup"><span data-stu-id="296d5-201">The agent uses IExpress as its self-extractor using the `/c` command.</span></span> <span data-ttu-id="296d5-202">È possibile vedere le opzioni della riga di comando in [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) (Opzioni della riga di comando di IExpress) e quindi aggiornare l'esempio in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="296d5-202">You can see the command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update the example to suit your needs.</span></span>

|<span data-ttu-id="296d5-203">Opzioni specifiche di MMA</span><span class="sxs-lookup"><span data-stu-id="296d5-203">MMA-specific options</span></span>                   |<span data-ttu-id="296d5-204">Note</span><span class="sxs-lookup"><span data-stu-id="296d5-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="296d5-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="296d5-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="296d5-206">1 = Configura l'agente per fare riferimento a un'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="296d5-206">1 = Configure the agent to report to a workspace</span></span>                |
|<span data-ttu-id="296d5-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="296d5-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="296d5-208">Id dell'area di lavoro (guid) per l'area di lavoro da aggiungere</span><span class="sxs-lookup"><span data-stu-id="296d5-208">Workspace Id (guid) for the workspace to add</span></span>                    |
|<span data-ttu-id="296d5-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="296d5-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="296d5-210">Chiave dell'area di lavoro usata per autenticarsi inizialmente nell'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="296d5-210">Workspace key used to initially authenticate with the workspace</span></span> |
|<span data-ttu-id="296d5-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="296d5-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="296d5-212">Specificare l'ambiente cloud in cui si trova l'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="296d5-212">Specify the cloud environment where the workspace is located</span></span> <br> <span data-ttu-id="296d5-213">0 = Cloud commerciale di Azure (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="296d5-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="296d5-214">1 = Azure per enti pubblici</span><span class="sxs-lookup"><span data-stu-id="296d5-214">1 = Azure Government</span></span> |
|<span data-ttu-id="296d5-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="296d5-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="296d5-216">URI per il proxy da usare</span><span class="sxs-lookup"><span data-stu-id="296d5-216">URI for the proxy to use</span></span> |
|<span data-ttu-id="296d5-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="296d5-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="296d5-218">Nome utente per accedere a un proxy autenticato</span><span class="sxs-lookup"><span data-stu-id="296d5-218">Username to access an authenticated proxy</span></span> |
|<span data-ttu-id="296d5-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="296d5-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="296d5-220">Password per accedere a un proxy autenticato</span><span class="sxs-lookup"><span data-stu-id="296d5-220">Password to access an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="296d5-221">Per evitare di raggiungere il limite di lunghezza della riga di comando di IExpress, installare l'agente con nessuna area di lavoro configurata e quindi usare uno script per impostare la configurazione per l'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="296d5-221">To avoid hitting the command-line length limit of IExpress, install the agent with no workspace configured and then use a script to set configuration for the workspace.</span></span>

>[!NOTE]
<span data-ttu-id="296d5-222">Se viene visualizzato un `Command line option syntax error.` quando si usa il parametro `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE`, è possibile usare la seguente soluzione alternativa:</span><span class="sxs-lookup"><span data-stu-id="296d5-222">If you get a `Command line option syntax error.` when using the `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use the following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="296d5-223">Aggiungere un'area di lavoro usando uno script</span><span class="sxs-lookup"><span data-stu-id="296d5-223">Add a workspace using a script</span></span>
<span data-ttu-id="296d5-224">Aggiornare un'area di lavoro usando l'API di scripting di Log Analytics con l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="296d5-224">Add a workspace using the Log Analytics agent scripting API with the following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="296d5-225">Per aggiungere un'area di lavoro in Azure per enti pubblici statunitensi, usare il seguente script di esempio:</span><span class="sxs-lookup"><span data-stu-id="296d5-225">To add a workspace in Azure for US Government, use the following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="296d5-226">Se in precedenza sono stati usati la riga di comando o uno script per installare o configurare l'agente, `EnableAzureOperationalInsights` è stato sostituito da `AddCloudWorkspace`.</span><span class="sxs-lookup"><span data-stu-id="296d5-226">If you've used the command line or script previously to install or configure the agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-the-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="296d5-227">Installare l'agente usando DSC in Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="296d5-227">Install the agent using DSC in Azure Automation</span></span>

<span data-ttu-id="296d5-228">È possibile utilizzare lo script di esempio riportato di seguito per installare l'agente utilizzando DSC in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="296d5-228">You can use the following script example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="296d5-229">Nell'esempio viene installato l'agente a 64 bit, identificato dal valore `URI`.</span><span class="sxs-lookup"><span data-stu-id="296d5-229">The example installs the 64-bit agent, identified by the `URI` value.</span></span> <span data-ttu-id="296d5-230">È possibile utilizzare anche la versione a 32 bit sostituendo il valore dell'URI.</span><span class="sxs-lookup"><span data-stu-id="296d5-230">You can also use the 32-bit version by replacing the URI value.</span></span> <span data-ttu-id="296d5-231">Gli URI per entrambe le versioni sono:</span><span class="sxs-lookup"><span data-stu-id="296d5-231">The URIs for both versions are:</span></span>

- <span data-ttu-id="296d5-232">Agente di Windows a 64 bit - https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="296d5-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="296d5-233">Agente di Windows a 32 bit - https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="296d5-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="296d5-234">La procedura e lo script di esempio riportati di seguito non determinano l'aggiornamento di un agente esistente.</span><span class="sxs-lookup"><span data-stu-id="296d5-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="296d5-235">Importare il modulo xPSDesiredStateConfiguration da [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="296d5-235">Import the xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="296d5-236">Creare gli asset variabili di Automazione di Azure per *OPSINSIGHTS_WS_ID* e *OPSINSIGHTS_WS_KEY*.</span><span class="sxs-lookup"><span data-stu-id="296d5-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="296d5-237">Impostare *OPSINSIGHTS_WS_ID* sull'ID dell'area di lavoro di Log Analytics di OMS e impostare *OPSINSIGHTS_WS_KEY* sulla chiave primaria dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="296d5-237">Set *OPSINSIGHTS_WS_ID* to your OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* to the primary key of your workspace.</span></span>
3.  <span data-ttu-id="296d5-238">Usare lo script seguente e salvarlo come MMAgent.ps1</span><span class="sxs-lookup"><span data-stu-id="296d5-238">Use the following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="296d5-239">Modificare e quindi usare l'esempio seguente per installare l'agente usando DSC in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="296d5-239">Modify and then use the following example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="296d5-240">Importare MMAgent.ps1 in Automazione di Azure tramite l'interfaccia di Automazione di Azure o il cmdlet.</span><span class="sxs-lookup"><span data-stu-id="296d5-240">Import MMAgent.ps1 into Azure Automation by using the Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="296d5-241">Assegnare un nodo alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="296d5-241">Assign a node to the configuration.</span></span> <span data-ttu-id="296d5-242">Entro 15 minuti il nodo controlla la configurazione e viene effettuato il push di MMA al nodo.</span><span class="sxs-lookup"><span data-stu-id="296d5-242">Within 15 minutes, the node checks its configuration and the MMA is pushed to the node.</span></span>

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

### <a name="get-the-latest-productid-value"></a><span data-ttu-id="296d5-243">Ottenere il valore di ProductId più recente</span><span class="sxs-lookup"><span data-stu-id="296d5-243">Get the latest ProductId value</span></span>

<span data-ttu-id="296d5-244">Il `ProductId value` nello script MMAgent.ps1 di è univoco per ogni versione dell'agente.</span><span class="sxs-lookup"><span data-stu-id="296d5-244">The `ProductId value` in the MMAgent.ps1 script is unique to each agent version.</span></span> <span data-ttu-id="296d5-245">Quando viene pubblicata una versione aggiornata di ogni agente, il valore di ProductId cambia.</span><span class="sxs-lookup"><span data-stu-id="296d5-245">When an updated version of each agent is published, the ProductId value changes.</span></span> <span data-ttu-id="296d5-246">Pertanto, quando il ProductId viene modificato in un secondo momento, è possibile individuare la versione dell'agente utilizzando un semplice script.</span><span class="sxs-lookup"><span data-stu-id="296d5-246">So, when the ProductId changes in the future, you can find the agent version using a simple script.</span></span> <span data-ttu-id="296d5-247">Dopo aver installato la versione più recente dell'agente in un server di prova, è possibile utilizzare lo script seguente per ottenere il valore di ProductId installato.</span><span class="sxs-lookup"><span data-stu-id="296d5-247">After you have the latest agent version installed on a test server, you can use the following script to get the installed ProductId value.</span></span> <span data-ttu-id="296d5-248">Utilizzando il valore di ProductId più recente, è possibile aggiornare il valore nello script MMAgent.ps1.</span><span class="sxs-lookup"><span data-stu-id="296d5-248">Using the latest ProductId value, you can update the value in the MMAgent.ps1 script.</span></span>

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

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="296d5-249">Configurare manualmente un agente o aggiungere nuove aree di lavoro</span><span class="sxs-lookup"><span data-stu-id="296d5-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="296d5-250">Se gli agenti sono stati installati ma non configurati o se si vuole che l'agente invii report a più aree di lavoro, è possibile usare le informazioni seguenti per abilitare un agente o riconfigurarlo.</span><span class="sxs-lookup"><span data-stu-id="296d5-250">If you've installed agents but did not configure them or if you want the agent to report to multiple workspaces, you can use the following information to enable an agent or reconfigure it.</span></span> <span data-ttu-id="296d5-251">Dopo aver configurato l'agente, questo verrà registrato con il servizio agente e otterrà le informazioni di configurazione necessarie nonché i Management Pack contenenti informazioni sulla soluzione.</span><span class="sxs-lookup"><span data-stu-id="296d5-251">After you've configured the agent, it will register with the agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="296d5-252">Dopo avere installato Microsoft Monitoring Agent, aprire il **Pannello di controllo**.</span><span class="sxs-lookup"><span data-stu-id="296d5-252">After you've installed the Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="296d5-253">Aprire **Microsoft Monitoring Agent** e fare clic sulla scheda **Azure Log Analytics (OMS)**.</span><span class="sxs-lookup"><span data-stu-id="296d5-253">Open **Microsoft Monitoring Agent** and then click the **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="296d5-254">Fare clic su **Aggiungi** per aprire la casella **Aggiungi un'area di lavoro di Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="296d5-254">Click **Add** to open the **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="296d5-255">Incollare l'**ID area di lavoro** e la **chiave dell'area di lavoro (chiave primaria)**, copiati nel Blocco note durante una procedura precedente relativa all'area di lavoro da aggiungere e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="296d5-255">Paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for the workspace that you want to add and then click **OK**.</span></span>  
    <span data-ttu-id="296d5-256">![configurazione di Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="296d5-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="296d5-257">Al termine della raccolta dei dati dai computer monitorati dall'agente, il numero di computer monitorati da OMS verrà visualizzato nel portale di OMS nella scheda **Origini connesse** della sezione **Impostazioni** come **server connessi**.</span><span class="sxs-lookup"><span data-stu-id="296d5-257">After data is collected from computers monitored by the agent, the number of computers monitored by OMS will appear in the OMS portal on the **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="to-disable-an-agent"></a><span data-ttu-id="296d5-258">Per disabilitare l'agente</span><span class="sxs-lookup"><span data-stu-id="296d5-258">To disable an agent</span></span>
1. <span data-ttu-id="296d5-259">Dopo aver installato l'agente, aprire il **Pannello di controllo**.</span><span class="sxs-lookup"><span data-stu-id="296d5-259">After installing the agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="296d5-260">Aprire Microsoft Monitoring Agent e fare clic sulla scheda **Azure Log Analytics (OMS)** .</span><span class="sxs-lookup"><span data-stu-id="296d5-260">Open Microsoft Monitoring Agent and then click the **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="296d5-261">Selezionare un'area di lavoro e quindi fare clic su **Rimuovi**.</span><span class="sxs-lookup"><span data-stu-id="296d5-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="296d5-262">Ripetere questo passaggio per tutte le altre aree di lavoro.</span><span class="sxs-lookup"><span data-stu-id="296d5-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="296d5-263">Configurare facoltativamente gli agenti per l'invio di report a un gruppo di gestione di Operations Manager</span><span class="sxs-lookup"><span data-stu-id="296d5-263">Optionally, configure agents to report to an Operations Manager management group</span></span>

<span data-ttu-id="296d5-264">Se si usa Operations Manager nell'infrastruttura IT, è anche possibile usare l'agente MMA come agente di Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="296d5-264">If you use Operations Manager in your IT infrastructure, you can also use the MMA agent as an Operations Manager agent.</span></span>

### <a name="to-configure-mma-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="296d5-265">Per configurare gli agenti MMA per l'invio di report a un gruppo di gestione di Operations Manager</span><span class="sxs-lookup"><span data-stu-id="296d5-265">To configure MMA agents to report to an Operations Manager management group</span></span>
1.  <span data-ttu-id="296d5-266">Nel computer in cui è installato l'agente aprire **Pannello di controllo**.</span><span class="sxs-lookup"><span data-stu-id="296d5-266">On the computer where the agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="296d5-267">Aprire **Microsoft Monitoring Agent** e fare clic sulla scheda **Operations Manager**.</span><span class="sxs-lookup"><span data-stu-id="296d5-267">Open **Microsoft Monitoring Agent** and then click the **Operations Manager** tab.</span></span>  
    <span data-ttu-id="296d5-268">![Microsoft Monitoring Agent scheda Operations Manager](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="296d5-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="296d5-269">Se i server di Operations Manager sono configurati per l'integrazione con Active Directory, fare clic su **Aggiorna automaticamente assegnazioni gruppi di gestione da Servizi di dominio Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="296d5-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="296d5-270">Fare clic su **Aggiungi** per aprire la finestra di dialogo **Aggiungi gruppo di gestione**.</span><span class="sxs-lookup"><span data-stu-id="296d5-270">Click **Add** to open the **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="296d5-271">![Microsoft Monitoring Agent Aggiungi gruppo di gestione](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="296d5-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="296d5-272">In **Nome gruppo di gestione** digitare il nome del gruppo di gestione.</span><span class="sxs-lookup"><span data-stu-id="296d5-272">In **Management group name** box, type the name of your management group.</span></span>
6.  <span data-ttu-id="296d5-273">Nella casella **Server di gestione primario** digitare il nome computer del server di gestione primario.</span><span class="sxs-lookup"><span data-stu-id="296d5-273">In the **Primary management server** box, type the computer name of the primary management server.</span></span>
7.  <span data-ttu-id="296d5-274">Nella casella **Porta server di gestione** digitare il numero di porta TCP.</span><span class="sxs-lookup"><span data-stu-id="296d5-274">In the **Management server port** box, type the TCP port number.</span></span>
8.  <span data-ttu-id="296d5-275">In **Account azione agente**scegliere l'account di sistema locale o un account di dominio locale.</span><span class="sxs-lookup"><span data-stu-id="296d5-275">Under **Agent Action Account**, choose either the Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="296d5-276">Fare clic su **OK** per chiudere la finestra di dialogo **Aggiungi gruppo di gestione** e quindi fare clic su **OK** per chiudere la finestra di dialogo **Proprietà di Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="296d5-276">Click **OK** to close the **Add a Management Group** dialog box and then click **OK** to close the **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="296d5-277">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="296d5-277">Next steps</span></span>

- <span data-ttu-id="296d5-278">[Aggiungere soluzioni di Log Analytics dalla raccolta soluzioni](log-analytics-add-solutions.md) per aggiungere funzionalità e raccogliere i dati.</span><span class="sxs-lookup"><span data-stu-id="296d5-278">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
