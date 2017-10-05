---
title: Risoluzione dei problemi di protezione per VMware/server fisici in Azure | Microsoft Docs
description: Questo articolo descrive i problemi comuni di replica delle macchine virtuali VMware e come risolverli
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/26/2017
ms.author: asgang
ms.openlocfilehash: 6ebec2e06566b1e2d6834fdd81c0d8b2801b80b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a><span data-ttu-id="ff041-103">Risolvere i problemi di replica per macchine virtuali VMware/server fisici locali</span><span class="sxs-lookup"><span data-stu-id="ff041-103">Troubleshoot on-premises VMware/Physical server replication issues</span></span>
<span data-ttu-id="ff041-104">Potrebbe essere visualizzato un messaggio di errore specifico durante la protezione delle macchine virtuali VMware o dei server fisici con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="ff041-104">You may receive a specific error message when protecting your VMware virtual machines or physical servers using Azure Site Recovery.</span></span> <span data-ttu-id="ff041-105">Questo articolo illustra nei dettagli alcuni dei più comuni messaggi di errore visualizzati e spiega le procedure per la risoluzione dei problemi relativi a tali messaggi.</span><span class="sxs-lookup"><span data-stu-id="ff041-105">This article details some of the more common error messages encountered, along with troubleshooting steps to resolve them.</span></span>


## <a name="initial-replication-is-stuck-at-0"></a><span data-ttu-id="ff041-106">Replica iniziale bloccata allo 0%</span><span class="sxs-lookup"><span data-stu-id="ff041-106">Initial replication is stuck at 0%</span></span>
<span data-ttu-id="ff041-107">La maggior parte degli errori di replica iniziale segnalata al supporto tecnico è dovuta a problemi di connettività tra il server di origine e il server di elaborazione oppure tra il server di elaborazione e Azure.</span><span class="sxs-lookup"><span data-stu-id="ff041-107">Most of the initial replication failures that we encounter at support are due to connectivity issues between source server-to-process server or process server-to-Azure.</span></span>
<span data-ttu-id="ff041-108">Nella maggior parte dei casi, è possibile risolvere questi problemi autonomamente seguendo i passaggi elencati di seguito.</span><span class="sxs-lookup"><span data-stu-id="ff041-108">For most cases, you can self troubleshoot these issues by following the steps listed below.</span></span>

###<a name="check-the-following-on-source-machine"></a><span data-ttu-id="ff041-109">Controllare quanto segue nel COMPUTER DI ORIGINE</span><span class="sxs-lookup"><span data-stu-id="ff041-109">Check the following on SOURCE MACHINE</span></span>
* <span data-ttu-id="ff041-110">Dalla riga di comando del computer del server di origine, usare Telnet per effettuare il ping del server di elaborazione con la porta HTTPS (impostazione predefinita 9443) come illustrato di seguito, per stabilire se sono presenti problemi di connettività di rete o problemi di blocco delle porte del firewall.</span><span class="sxs-lookup"><span data-stu-id="ff041-110">From Source Server machine command line, use Telnet to ping the Process Server with https port (default 9443) as shown below to see if there are any network connectivity issues or firewall port blocking issues.</span></span>
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > <span data-ttu-id="ff041-111">Usare Telnet e non usare PING per testare la connettività.</span><span class="sxs-lookup"><span data-stu-id="ff041-111">Use Telnet, don’t use PING to test connectivity.</span></span>  <span data-ttu-id="ff041-112">Se Telnet non è installato, seguire la procedura [qui](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx) indicata.</span><span class="sxs-lookup"><span data-stu-id="ff041-112">If Telnet is not installed, follow the steps list [here](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span></span>

<span data-ttu-id="ff041-113">Se non è possibile connettersi, consentire la porta in ingresso 9443 nel server di elaborazione e controllare se il problema persiste.</span><span class="sxs-lookup"><span data-stu-id="ff041-113">If unable to connect, allow inbound port 9443 on the Process Server and check if the problem still exits.</span></span> <span data-ttu-id="ff041-114">Si sono verificati alcuni casi in cui il problema era dovuto al posizionamento del server di elaborazione dietro una rete perimetrale.</span><span class="sxs-lookup"><span data-stu-id="ff041-114">There has been some cases where process server was behind DMZ, which was causing this problem.</span></span>

* <span data-ttu-id="ff041-115">Controllare lo stato del servizio `InMage Scout VX Agent – Sentinel/OutpostStart` se non è in esecuzione e controllare se il problema persiste.</span><span class="sxs-lookup"><span data-stu-id="ff041-115">Check the status of service `InMage Scout VX Agent – Sentinel/OutpostStart` if it is not running and check if the problem still exists.</span></span>   
 
###<a name="check-the-following-on-process-server"></a><span data-ttu-id="ff041-116">Controllare quanto segue nel SERVER DI ELABORAZIONE</span><span class="sxs-lookup"><span data-stu-id="ff041-116">Check the following on PROCESS SERVER</span></span>

* <span data-ttu-id="ff041-117">**Controllare se il server di elaborazione effettua attivamente il push dei dati in Azure**</span><span class="sxs-lookup"><span data-stu-id="ff041-117">**Check if process server is actively pushing data to Azure**</span></span> 

<span data-ttu-id="ff041-118">Dal computer del server di elaborazione aprire Gestione attività (premere CTRL+MAIUSC-ESC).</span><span class="sxs-lookup"><span data-stu-id="ff041-118">From Process Server machine, open the Task Manager (press Ctrl-Shift-Esc ).</span></span> <span data-ttu-id="ff041-119">Passare alla scheda Prestazioni e fare clic sul collegamento 'Apri Monitoraggio risorse'.</span><span class="sxs-lookup"><span data-stu-id="ff041-119">Go to the Performance tab and click ‘Open Resource Monitor’ link.</span></span> <span data-ttu-id="ff041-120">Da Monitoraggio risorse passare alla scheda Rete.</span><span class="sxs-lookup"><span data-stu-id="ff041-120">From Resource Manager, go to Network tab.</span></span> <span data-ttu-id="ff041-121">Controllare se cbengine.exe 'Processi con attività rete' sta inviando attivamente volumi elevati di dati (in Mbps).</span><span class="sxs-lookup"><span data-stu-id="ff041-121">Check if cbengine.exe in ‘Processes with Network Activity’ is actively sending large volume (in Mbs) of data.</span></span>

![Abilitare la replica](./media/site-recovery-protection-common-errors/cbengine.png)

<span data-ttu-id="ff041-123">Se non è questo il caso, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ff041-123">If not follow the steps listed below:</span></span>

* <span data-ttu-id="ff041-124">**Controllare se il server di elaborazione è in grado di connettersi al servizio BLOB di Azure**: selezionare e controllare cbengine.exe per visualizzare le 'Connessioni TCP' e verificare se è disponibile la connettività dal server di elaborazione all'URL del BLOB del servizio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ff041-124">**Check if Process server is able to connect Azure Blob**: Select and check cbengine.exe to view the ‘TCP Connections’ to see if there is connectivity from Process server to Azure Storage blob URL.</span></span>

![Abilitare la replica](./media/site-recovery-protection-common-errors/rmonitor.png)

<span data-ttu-id="ff041-126">Se non è questo il caso, passare a Pannello di controllo > Servizi e controllare se i servizi seguenti sono in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="ff041-126">If not then go to Control Panel > Services, check if the following services are up and running:</span></span>

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
<span data-ttu-id="ff041-127">(Ri)avviare gli eventuali servizi non in esecuzione e verificare se il problema persiste.</span><span class="sxs-lookup"><span data-stu-id="ff041-127">(Re)Start any service which is not running and check if the problem still exists.</span></span>

* <span data-ttu-id="ff041-128">**Controllare se il server di elaborazione è in grado di connettersi all'indirizzo IP pubblico di Azure tramite la porta 443**</span><span class="sxs-lookup"><span data-stu-id="ff041-128">**Check if Process server is able to connect to Azure Public IP address using port 443**</span></span>

<span data-ttu-id="ff041-129">Aprire il più recente CBEngineCurr.errlog da `%programfiles%\Microsoft Azure Recovery Services Agent\Temp`, quindi cercare :443 e un messaggio di errore che indica un tentativo di connessione non riuscito.</span><span class="sxs-lookup"><span data-stu-id="ff041-129">Open the latest CBEngineCurr.errlog from `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` and search for :443  and connection attempt failed.</span></span>

![Abilitare la replica](./media/site-recovery-protection-common-errors/logdetails1.png)

<span data-ttu-id="ff041-131">Se sono presenti problemi, dalla riga di comando del server di elaborazione usare Telnet per effettuare il ping dell'indirizzo IP pubblico di Azure (mascherato nell'immagine precedente) indicato nel file CBEngineCurr.currLog per la porta 443.</span><span class="sxs-lookup"><span data-stu-id="ff041-131">If there are issues, then from Process Server command line, use telnet to ping your Azure Public IP address (masked in above image) found in the CBEngineCurr.currLog using port 443.</span></span>

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
<span data-ttu-id="ff041-132">Se non si riesce a connettersi, verificare se il problema di accesso è causato dal firewall o da un proxy, come descritto nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="ff041-132">If you are unable to connect, then check if the access issue is due to firewall or Proxy as described in next step.</span></span>


* <span data-ttu-id="ff041-133">**Controllare che l'accesso non sia bloccato da un firewall basato su indirizzi IP nel server di elaborazione**: se si usano regole del firewall basate su indirizzi IP nel server, scaricare l'elenco completo degli intervalli IP dei data center di Microsoft Azure da [qui](https://www.microsoft.com/download/details.aspx?id=41653) e aggiungerli alla configurazione del firewall per assicurarsi che consentano le comunicazioni con Azure e la porta HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="ff041-133">**Check if IP address-based firewall on Process server are not blocking access**: If you are using an IP address-based firewall rules on the server, then download the complete list of Microsoft Azure Datacenter IP Ranges from [here](https://www.microsoft.com/download/details.aspx?id=41653) and add them to your firewall configuration to ensure they allow communication to Azure (and the HTTPS (443) port).</span></span>  <span data-ttu-id="ff041-134">Consentire gli intervalli di indirizzi IP per l'area di Azure della sottoscrizione e per gli Stati Uniti occidentali (usati per il controllo di accesso e la gestione delle identità).</span><span class="sxs-lookup"><span data-stu-id="ff041-134">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

* <span data-ttu-id="ff041-135">**Controllare che l'accesso non sia bloccato da un firewall basato su URL nel server di elaborazione**: se si usano regole del firewall basate su URL nel server, assicurarsi di aggiungere gli URL seguenti alla configurazione del firewall.</span><span class="sxs-lookup"><span data-stu-id="ff041-135">**Check if URL-based firewall on Process server is not blocking access**:  If you are using a URL based firewall rules on the server, ensure the following URLs are added to firewall configuration.</span></span> 
     
  <span data-ttu-id="ff041-136">`*.accesscontrol.windows.net:`, usato per il controllo di accesso e la gestione delle identità.</span><span class="sxs-lookup"><span data-stu-id="ff041-136">`*.accesscontrol.windows.net:` Used for access control and identity management</span></span>

  <span data-ttu-id="ff041-137">`*.backup.windowsazure.com:`, usato per l'orchestrazione e il trasferimento dei dati di replica.</span><span class="sxs-lookup"><span data-stu-id="ff041-137">`*.backup.windowsazure.com:` Used for replication data transfer and orchestration</span></span>

  <span data-ttu-id="ff041-138">`*.blob.core.windows.net:`, usato per l'accesso all'account di archiviazione in cui sono archiviati i dati replicati.</span><span class="sxs-lookup"><span data-stu-id="ff041-138">`*.blob.core.windows.net:` Used for access to the storage account that stores replicated data</span></span>

  <span data-ttu-id="ff041-139">`*.hypervrecoverymanager.windowsazure.com:`, usato per l'orchestrazione e le operazioni di gestione della replica.</span><span class="sxs-lookup"><span data-stu-id="ff041-139">`*.hypervrecoverymanager.windowsazure.com:` Used for replication management operations and orchestration</span></span>

  <span data-ttu-id="ff041-140">`time.nist.gov` e `time.windows.com`, usati per controllare la sincronizzazione tra ora di sistema e ora globale.</span><span class="sxs-lookup"><span data-stu-id="ff041-140">`time.nist.gov` and `time.windows.com`: Used to check time synchronization between system and global time.</span></span>

<span data-ttu-id="ff041-141">URL per il **cloud di Azure per enti pubblici**:</span><span class="sxs-lookup"><span data-stu-id="ff041-141">URLs for **Azure Government Cloud**:</span></span>

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* <span data-ttu-id="ff041-142">**Controllare che le impostazioni del proxy nel server di elaborazione non blocchino l'accesso**.</span><span class="sxs-lookup"><span data-stu-id="ff041-142">**Check if Proxy Settings on Process server are not blocking access**.</span></span>  <span data-ttu-id="ff041-143">Se si usa un server proxy, assicurarsi che il nome del server proxy venga risolto dal server DNS.</span><span class="sxs-lookup"><span data-stu-id="ff041-143">If you are using a Proxy Server, ensure the proxy server name is resolving by the DNS server.</span></span>
<span data-ttu-id="ff041-144">Per controllare le impostazioni specificate al momento dell'installazione del server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="ff041-144">To check what you have provided at the time of Configuration Server setup.</span></span> <span data-ttu-id="ff041-145">Passare alla chiave del Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="ff041-145">Go to registry key</span></span>

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

<span data-ttu-id="ff041-146">Verificare ora che le stesse impostazioni vengano usate dall'agente di Azure Site Recovery per l'invio dei dati.</span><span class="sxs-lookup"><span data-stu-id="ff041-146">Now ensure that the same settings are being used by Azure Site Recovery agent to send data.</span></span>
<span data-ttu-id="ff041-147">Cercare Backup di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="ff041-147">Search Microsoft Azure  Backup</span></span> 

![Abilitare la replica](./media/site-recovery-protection-common-errors/mab.png)

<span data-ttu-id="ff041-149">Aprire il servizio e fare clic su Azione > Modifica proprietà.</span><span class="sxs-lookup"><span data-stu-id="ff041-149">Open it and click on Action > Change Properties.</span></span> <span data-ttu-id="ff041-150">Nella scheda Configurazione proxy dovrebbe essere visualizzato l'indirizzo del proxy, che dovrebbe essere lo stesso indicato nelle impostazioni del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="ff041-150">Under Proxy Configuration tab, you should see the proxy address, which should be same as shown by the registry settings.</span></span> <span data-ttu-id="ff041-151">In caso contrario, modificarlo per impostare lo stesso indirizzo.</span><span class="sxs-lookup"><span data-stu-id="ff041-151">If not, please change it to the same address.</span></span>

![Abilitare la replica](./media/site-recovery-protection-common-errors/mabproxy.png)

* <span data-ttu-id="ff041-153">**Controllare che la larghezza di banda non sia vincolata nel server di elaborazione**: aumentare la larghezza di banda e controllare se il problema persiste.</span><span class="sxs-lookup"><span data-stu-id="ff041-153">**Check if Throttle bandwidth is not constrained on Process server**:  Increase the bandwidth  and check if the problem still exists.</span></span>

##<a name="next-steps"></a><span data-ttu-id="ff041-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ff041-154">Next steps</span></span>
<span data-ttu-id="ff041-155">Se è necessaria ulteriore assistenza, pubblicare la domanda nel [forum per ASR](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ff041-155">If you need more help, then post your query to [ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span></span> <span data-ttu-id="ff041-156">La community è molto attiva e uno dei tecnici Microsoft sarà in grado di offrire il supporto richiesto.</span><span class="sxs-lookup"><span data-stu-id="ff041-156">We have an active community and one of our engineers will be able to assist you.</span></span>