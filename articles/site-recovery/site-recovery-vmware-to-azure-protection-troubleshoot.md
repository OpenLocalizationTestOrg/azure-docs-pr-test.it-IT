---
title: aaaTroubleshoot protezione errori VMware/fisici tooAzure | Documenti Microsoft
description: Questo articolo vengono descritti gli errori di replica della macchina VMware di comuni hello e come tootroubleshoot li
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
ms.openlocfilehash: b821e9aa2610482ba1900645fb75e75744dc442f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a><span data-ttu-id="962a8-103">Risolvere i problemi di replica per macchine virtuali VMware/server fisici locali</span><span class="sxs-lookup"><span data-stu-id="962a8-103">Troubleshoot on-premises VMware/Physical server replication issues</span></span>
<span data-ttu-id="962a8-104">Potrebbe essere visualizzato un messaggio di errore specifico durante la protezione delle macchine virtuali VMware o dei server fisici con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="962a8-104">You may receive a specific error message when protecting your VMware virtual machines or physical servers using Azure Site Recovery.</span></span> <span data-ttu-id="962a8-105">Questo articolo presenta alcuni dei messaggi di errore più comuni rilevati, insieme a tooresolve passaggi di risoluzione dei problemi di hello li.</span><span class="sxs-lookup"><span data-stu-id="962a8-105">This article details some of hello more common error messages encountered, along with troubleshooting steps tooresolve them.</span></span>


## <a name="initial-replication-is-stuck-at-0"></a><span data-ttu-id="962a8-106">Replica iniziale bloccata allo 0%</span><span class="sxs-lookup"><span data-stu-id="962a8-106">Initial replication is stuck at 0%</span></span>
<span data-ttu-id="962a8-107">La maggior parte degli errori di replica iniziale hello che si verificano al supporto tecnico è a causa di problemi di tooconnectivity tra server al processo server di origine o di processo server in Azure.</span><span class="sxs-lookup"><span data-stu-id="962a8-107">Most of hello initial replication failures that we encounter at support are due tooconnectivity issues between source server-to-process server or process server-to-Azure.</span></span>
<span data-ttu-id="962a8-108">Per la maggior parte dei casi, è possibile self risolvere questi problemi seguendo i passaggi di hello elencati di seguito.</span><span class="sxs-lookup"><span data-stu-id="962a8-108">For most cases, you can self troubleshoot these issues by following hello steps listed below.</span></span>

###<a name="check-hello-following-on-source-machine"></a><span data-ttu-id="962a8-109">Verificare hello seguenti nel computer di origine</span><span class="sxs-lookup"><span data-stu-id="962a8-109">Check hello following on SOURCE MACHINE</span></span>
* <span data-ttu-id="962a8-110">Dalla riga di comando di computer Server di origine, è possibile usare Telnet tooping hello Server di elaborazione con la porta https (impostazione predefinita 9443) come illustrato di seguito toosee se sono presenti problemi di connettività di rete o porta del firewall problemi gravi.</span><span class="sxs-lookup"><span data-stu-id="962a8-110">From Source Server machine command line, use Telnet tooping hello Process Server with https port (default 9443) as shown below toosee if there are any network connectivity issues or firewall port blocking issues.</span></span>
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > <span data-ttu-id="962a8-111">Utilizzo di Telnet, non usare la connettività tootest PING.</span><span class="sxs-lookup"><span data-stu-id="962a8-111">Use Telnet, don’t use PING tootest connectivity.</span></span>  <span data-ttu-id="962a8-112">Se Telnet non è installato, seguire l'elenco di passaggi hello [qui](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="962a8-112">If Telnet is not installed, follow hello steps list [here](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span></span>

<span data-ttu-id="962a8-113">Se non è possibile tooconnect, consente la porta in ingresso 9443 sul Server di elaborazione hello e controllare se hello problema ancora viene chiuso.</span><span class="sxs-lookup"><span data-stu-id="962a8-113">If unable tooconnect, allow inbound port 9443 on hello Process Server and check if hello problem still exits.</span></span> <span data-ttu-id="962a8-114">Si sono verificati alcuni casi in cui il problema era dovuto al posizionamento del server di elaborazione dietro una rete perimetrale.</span><span class="sxs-lookup"><span data-stu-id="962a8-114">There has been some cases where process server was behind DMZ, which was causing this problem.</span></span>

* <span data-ttu-id="962a8-115">Controllare lo stato di hello del servizio `InMage Scout VX Agent – Sentinel/OutpostStart` se non è in esecuzione e controllare se il problema di hello esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="962a8-115">Check hello status of service `InMage Scout VX Agent – Sentinel/OutpostStart` if it is not running and check if hello problem still exists.</span></span>   
 
###<a name="check-hello-following-on-process-server"></a><span data-ttu-id="962a8-116">Verificare hello seguenti nel SERVER di elaborazione</span><span class="sxs-lookup"><span data-stu-id="962a8-116">Check hello following on PROCESS SERVER</span></span>

* <span data-ttu-id="962a8-117">**Controllare se i server di elaborazione è attivamente push tooAzure dati**</span><span class="sxs-lookup"><span data-stu-id="962a8-117">**Check if process server is actively pushing data tooAzure**</span></span> 

<span data-ttu-id="962a8-118">Computer Server di elaborazione, aprire hello Task Manager (premere Ctrl + Maiusc-Esc).</span><span class="sxs-lookup"><span data-stu-id="962a8-118">From Process Server machine, open hello Task Manager (press Ctrl-Shift-Esc ).</span></span> <span data-ttu-id="962a8-119">Andare nella scheda prestazioni toohello e fare clic sul collegamento 'Monitoraggio risorse Open'.</span><span class="sxs-lookup"><span data-stu-id="962a8-119">Go toohello Performance tab and click ‘Open Resource Monitor’ link.</span></span> <span data-ttu-id="962a8-120">Da Gestione risorse, passare tooNetwork scheda. Controllare se cbengine.exe 'Processi con attività rete' sta inviando attivamente volumi elevati di dati (in Mbps).</span><span class="sxs-lookup"><span data-stu-id="962a8-120">From Resource Manager, go tooNetwork tab. Check if cbengine.exe in ‘Processes with Network Activity’ is actively sending large volume (in Mbs) of data.</span></span>

![Abilitare la replica](./media/site-recovery-protection-common-errors/cbengine.png)

<span data-ttu-id="962a8-122">Se non seguire i passaggi di hello elencati di seguito:</span><span class="sxs-lookup"><span data-stu-id="962a8-122">If not follow hello steps listed below:</span></span>

* <span data-ttu-id="962a8-123">**Verificare se i server di elaborazione è in grado di tooconnect Blob di Azure**: selezionare e controllare cbengine.exe tooview hello 'Connessioni TCP' toosee se si verifica la connettività dal processo server tooAzure archiviazione blob URL.</span><span class="sxs-lookup"><span data-stu-id="962a8-123">**Check if Process server is able tooconnect Azure Blob**: Select and check cbengine.exe tooview hello ‘TCP Connections’ toosee if there is connectivity from Process server tooAzure Storage blob URL.</span></span>

![Abilitare la replica](./media/site-recovery-protection-common-errors/rmonitor.png)

<span data-ttu-id="962a8-125">In caso contrario, andare tooControl pannello > servizi, controllare se hello seguenti servizi siano in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="962a8-125">If not then go tooControl Panel > Services, check if hello following services are up and running:</span></span>

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
<span data-ttu-id="962a8-126">(Ri) Avviare il servizio che non è in esecuzione e verificare se il problema di hello esista ancora.</span><span class="sxs-lookup"><span data-stu-id="962a8-126">(Re)Start any service which is not running and check if hello problem still exists.</span></span>

* <span data-ttu-id="962a8-127">**Verificare se i server di elaborazione è in grado di tooconnect indirizzo IP pubblico di tooAzure tramite la porta 443**</span><span class="sxs-lookup"><span data-stu-id="962a8-127">**Check if Process server is able tooconnect tooAzure Public IP address using port 443**</span></span>

<span data-ttu-id="962a8-128">Aprire hello CBEngineCurr.errlog più recenti da `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` e cercare: 443 e connessione tentativo non riuscito.</span><span class="sxs-lookup"><span data-stu-id="962a8-128">Open hello latest CBEngineCurr.errlog from `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` and search for :443  and connection attempt failed.</span></span>

![Abilitare la replica](./media/site-recovery-protection-common-errors/logdetails1.png)

<span data-ttu-id="962a8-130">Se si verificano problemi, dalla riga di comando di Server di elaborazione, usare telnet tooping l'indirizzo IP pubblico di Azure (mascherato sopra immagine) trovato in hello CBEngineCurr.currLog tramite la porta 443.</span><span class="sxs-lookup"><span data-stu-id="962a8-130">If there are issues, then from Process Server command line, use telnet tooping your Azure Public IP address (masked in above image) found in hello CBEngineCurr.currLog using port 443.</span></span>

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
<span data-ttu-id="962a8-131">Se si tooconnect non è possibile, controllare se il problema di accesso di hello è scadenza toofirewall o Proxy, come descritto nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="962a8-131">If you are unable tooconnect, then check if hello access issue is due toofirewall or Proxy as described in next step.</span></span>


* <span data-ttu-id="962a8-132">**Controllare se firewall basato su indirizzi IP nel server di elaborazione non bloccano l'accesso**: se si utilizza un regole del firewall basato su indirizzi IP nel server di hello, quindi scaricare elenco completo di hello dei Data Center intervalli IP Microsoft Azure da [qui ](https://www.microsoft.com/download/details.aspx?id=41653) e li aggiunge tooyour firewall configurazione tooensure consentono la comunicazione tooAzure (e hello porta HTTPS (443)).</span><span class="sxs-lookup"><span data-stu-id="962a8-132">**Check if IP address-based firewall on Process server are not blocking access**: If you are using an IP address-based firewall rules on hello server, then download hello complete list of Microsoft Azure Datacenter IP Ranges from [here](https://www.microsoft.com/download/details.aspx?id=41653) and add them tooyour firewall configuration tooensure they allow communication tooAzure (and hello HTTPS (443) port).</span></span>  <span data-ttu-id="962a8-133">Consenti gli intervalli di indirizzi IP per hello area della sottoscrizione di Azure e per Stati Uniti occidentali (utilizzato per il controllo di accesso e gestione delle identità).</span><span class="sxs-lookup"><span data-stu-id="962a8-133">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

* <span data-ttu-id="962a8-134">**Controllare se il firewall basato su URL sul server di elaborazione non blocchi l'accesso**: se si utilizza una regola firewall URL basato su server hello, assicurarsi di hello URL seguenti viene aggiunti toofirewall configurazione.</span><span class="sxs-lookup"><span data-stu-id="962a8-134">**Check if URL-based firewall on Process server is not blocking access**:  If you are using a URL based firewall rules on hello server, ensure hello following URLs are added toofirewall configuration.</span></span> 
     
  <span data-ttu-id="962a8-135">`*.accesscontrol.windows.net:`, usato per il controllo di accesso e la gestione delle identità.</span><span class="sxs-lookup"><span data-stu-id="962a8-135">`*.accesscontrol.windows.net:` Used for access control and identity management</span></span>

  <span data-ttu-id="962a8-136">`*.backup.windowsazure.com:`, usato per l'orchestrazione e il trasferimento dei dati di replica.</span><span class="sxs-lookup"><span data-stu-id="962a8-136">`*.backup.windowsazure.com:` Used for replication data transfer and orchestration</span></span>

  <span data-ttu-id="962a8-137">`*.blob.core.windows.net:`Utilizzato per l'accesso toohello account di archiviazione che archivia i dati replicati</span><span class="sxs-lookup"><span data-stu-id="962a8-137">`*.blob.core.windows.net:` Used for access toohello storage account that stores replicated data</span></span>

  <span data-ttu-id="962a8-138">`*.hypervrecoverymanager.windowsazure.com:`, usato per l'orchestrazione e le operazioni di gestione della replica.</span><span class="sxs-lookup"><span data-stu-id="962a8-138">`*.hypervrecoverymanager.windowsazure.com:` Used for replication management operations and orchestration</span></span>

  <span data-ttu-id="962a8-139">`time.nist.gov`e `time.windows.com`: utilizzato toocheck sincronizzazione dell'ora tra sistema e l'ora globale.</span><span class="sxs-lookup"><span data-stu-id="962a8-139">`time.nist.gov` and `time.windows.com`: Used toocheck time synchronization between system and global time.</span></span>

<span data-ttu-id="962a8-140">URL per il **cloud di Azure per enti pubblici**:</span><span class="sxs-lookup"><span data-stu-id="962a8-140">URLs for **Azure Government Cloud**:</span></span>

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* <span data-ttu-id="962a8-141">**Controllare che le impostazioni del proxy nel server di elaborazione non blocchino l'accesso**.</span><span class="sxs-lookup"><span data-stu-id="962a8-141">**Check if Proxy Settings on Process server are not blocking access**.</span></span>  <span data-ttu-id="962a8-142">Se si utilizza un Server Proxy, verificare il nome di server proxy hello venga risolto dal server DNS hello.</span><span class="sxs-lookup"><span data-stu-id="962a8-142">If you are using a Proxy Server, ensure hello proxy server name is resolving by hello DNS server.</span></span>
<span data-ttu-id="962a8-143">toocheck di quanto specificato in fase di hello del programma di installazione di Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="962a8-143">toocheck what you have provided at hello time of Configuration Server setup.</span></span> <span data-ttu-id="962a8-144">Passare tooregistry chiave</span><span class="sxs-lookup"><span data-stu-id="962a8-144">Go tooregistry key</span></span>

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

<span data-ttu-id="962a8-145">Verificare che hello stesse impostazioni sono utilizzate da dati toosend agente di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="962a8-145">Now ensure that hello same settings are being used by Azure Site Recovery agent toosend data.</span></span>
<span data-ttu-id="962a8-146">Cercare Backup di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="962a8-146">Search Microsoft Azure  Backup</span></span> 

![Abilitare la replica](./media/site-recovery-protection-common-errors/mab.png)

<span data-ttu-id="962a8-148">Aprire il servizio e fare clic su Azione > Modifica proprietà.</span><span class="sxs-lookup"><span data-stu-id="962a8-148">Open it and click on Action > Change Properties.</span></span> <span data-ttu-id="962a8-149">Nella scheda Configurazione del Proxy, verrà visualizzato l'indirizzo proxy hello, che deve essere lo stesso come indicato dalle impostazioni del Registro di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="962a8-149">Under Proxy Configuration tab, you should see hello proxy address, which should be same as shown by hello registry settings.</span></span> <span data-ttu-id="962a8-150">In caso contrario,. modificarlo toohello stesso indirizzo.</span><span class="sxs-lookup"><span data-stu-id="962a8-150">If not, please change it toohello same address.</span></span>

![Abilitare la replica](./media/site-recovery-protection-common-errors/mabproxy.png)

* <span data-ttu-id="962a8-152">**Controllare se nel server di elaborazione non è vincolato limitazione della larghezza di banda**: aumentare la larghezza di banda hello e verificare se il problema di hello esista ancora.</span><span class="sxs-lookup"><span data-stu-id="962a8-152">**Check if Throttle bandwidth is not constrained on Process server**:  Increase hello bandwidth  and check if hello problem still exists.</span></span>

##<a name="next-steps"></a><span data-ttu-id="962a8-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="962a8-153">Next steps</span></span>
<span data-ttu-id="962a8-154">Se è necessario ulteriore assistenza, quindi registrare la query troppo[forum ASR](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="962a8-154">If you need more help, then post your query too[ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span></span> <span data-ttu-id="962a8-155">È disponibile una community attiva e uno dei nostri tecnici saranno in grado di tooassist è.</span><span class="sxs-lookup"><span data-stu-id="962a8-155">We have an active community and one of our engineers will be able tooassist you.</span></span>
