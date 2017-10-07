---
title: aaaConnecting la sicurezza prodotti toohello sicurezza Operations Management Suite (OMS) e la soluzione di controllo | Documenti Microsoft
description: Questo documento consente si tooconnect i prodotti di sicurezza tooOperations protezione del gruppo di gestione e di soluzione di controllo utilizzando il formato di eventi comuni.
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a><span data-ttu-id="6c77d-103">La connessione la sicurezza prodotti toohello sicurezza Operations Management Suite (OMS) e la soluzione di controllo</span><span class="sxs-lookup"><span data-stu-id="6c77d-103">Connecting your security products toohello Operations Management Suite (OMS) Security and Audit Solution</span></span> 
<span data-ttu-id="6c77d-104">Questo documento consente di connettersi ai prodotti di sicurezza in hello sicurezza OMS e la soluzione di controllo.</span><span class="sxs-lookup"><span data-stu-id="6c77d-104">This document helps you connect your security products into hello OMS Security and Audit Solution.</span></span> <span data-ttu-id="6c77d-105">è supportata le seguenti origini Hello:</span><span class="sxs-lookup"><span data-stu-id="6c77d-105">hello following sources are supported:</span></span>

- <span data-ttu-id="6c77d-106">Eventi Common Event Format (CEF)</span><span class="sxs-lookup"><span data-stu-id="6c77d-106">Common Event Format (CEF) events</span></span>
- <span data-ttu-id="6c77d-107">Eventi ASA Cisco</span><span class="sxs-lookup"><span data-stu-id="6c77d-107">Cisco ASA events</span></span>


## <a name="what-is-cef"></a><span data-ttu-id="6c77d-108">Informazioni su CEF</span><span class="sxs-lookup"><span data-stu-id="6c77d-108">What is CEF?</span></span>
<span data-ttu-id="6c77d-109">Il formato di evento comuni (CEF) è un formato standard di settore sopra i messaggi Syslog, utilizzati da molti sicurezza fornitori tooallow evento interoperabilità tra piattaforme diverse.</span><span class="sxs-lookup"><span data-stu-id="6c77d-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors tooallow event interoperability among different platforms.</span></span> <span data-ttu-id="6c77d-110">Soluzione di controllo e sicurezza OMS supporta inserimenti di dati utilizzo CEF, che consentono di tooconnect i prodotti di sicurezza con la sicurezza di OMS.</span><span class="sxs-lookup"><span data-stu-id="6c77d-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you tooconnect your security products with OMS Security.</span></span> 

<span data-ttu-id="6c77d-111">Connettendo il tooOMS di origine dati, verranno tootake in grado di sfruttare hello funzionalità che fanno parte della piattaforma seguenti:</span><span class="sxs-lookup"><span data-stu-id="6c77d-111">By connecting your data source tooOMS, you are able tootake advantage of hello following capabilities that are part of this platform:</span></span>

- <span data-ttu-id="6c77d-112">Ricerca e controllo</span><span class="sxs-lookup"><span data-stu-id="6c77d-112">Search & Correlation</span></span>
- <span data-ttu-id="6c77d-113">Controllo</span><span class="sxs-lookup"><span data-stu-id="6c77d-113">Auditing</span></span>
- <span data-ttu-id="6c77d-114">Avviso</span><span class="sxs-lookup"><span data-stu-id="6c77d-114">Alert</span></span>
- <span data-ttu-id="6c77d-115">Intelligence per le minacce</span><span class="sxs-lookup"><span data-stu-id="6c77d-115">Threat Intelligence</span></span>
- <span data-ttu-id="6c77d-116">Errori rilevanti</span><span class="sxs-lookup"><span data-stu-id="6c77d-116">Notable Issues</span></span>

## <a name="collection-of-security-solution-logs"></a><span data-ttu-id="6c77d-117">Raccolta di log di soluzioni per la sicurezza</span><span class="sxs-lookup"><span data-stu-id="6c77d-117">Collection of security solution logs</span></span>

<span data-ttu-id="6c77d-118">La soluzione per la sicurezza per OMS supporta la raccolta di log tramite CEF sui log Syslog e [ASA Cisco](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/).</span><span class="sxs-lookup"><span data-stu-id="6c77d-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span></span> <span data-ttu-id="6c77d-119">In questo esempio, l'origine hello (computer che genera log hello) è un computer Linux in esecuzione il daemon syslog-ng e destinazione hello è sicurezza OMS.</span><span class="sxs-lookup"><span data-stu-id="6c77d-119">In this example, hello source (computer that generates hello logs) is a Linux computer running syslog-ng daemon and hello target is OMS Security.</span></span> <span data-ttu-id="6c77d-120">il computer Linux tooprepare hello che occorre hello tooperform seguente attività:</span><span class="sxs-lookup"><span data-stu-id="6c77d-120">tooprepare hello Linux computer you will need tooperform hello following tasks:</span></span>

- <span data-ttu-id="6c77d-121">Scaricare hello agente OMS per Linux e versione 1.2.0-25 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="6c77d-121">Download hello OMS Agent for Linux, version 1.2.0-25 or above.</span></span>
- <span data-ttu-id="6c77d-122">Consultare la sezione hello **Guida all'installazione rapida** da [questo articolo](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall e area di lavoro tooyour hello onboard agente.</span><span class="sxs-lookup"><span data-stu-id="6c77d-122">Follow hello section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall and onboard hello agent tooyour workspace.</span></span>

<span data-ttu-id="6c77d-123">In genere, l'agente di hello è installato in un computer diverso da hello uno per i log di hello vengono generati.</span><span class="sxs-lookup"><span data-stu-id="6c77d-123">Typically, hello agent is installed on a different computer from hello one on which hello logs are generated.</span></span> <span data-ttu-id="6c77d-124">Computer agente di inoltro hello registri toohello richiederà in genere hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6c77d-124">Forwarding hello logs toohello agent machine will usually require hello following steps:</span></span>

- <span data-ttu-id="6c77d-125">Configurare la registrazione del prodotto/macchina tooforward hello gli eventi necessari toohello daemon syslog (rsyslog o syslog-ng) hello sul computer agente hello.</span><span class="sxs-lookup"><span data-stu-id="6c77d-125">Configure hello logging product/machine tooforward hello required events toohello syslog daemon (rsyslog or syslog-ng) on hello agent machine.</span></span>
- <span data-ttu-id="6c77d-126">Abilitare il daemon syslog hello nei hello agente macchina tooreceive messaggi provenienti da un sistema remoto.</span><span class="sxs-lookup"><span data-stu-id="6c77d-126">Enable hello syslog daemon on hello agent machine tooreceive messages from a remote system.</span></span>

<span data-ttu-id="6c77d-127">Nel computer agente hello, gli eventi di hello devono toobe inviato dalla porta UDP di toolocal daemon syslog hello 25226.</span><span class="sxs-lookup"><span data-stu-id="6c77d-127">On hello agent machine, hello events need toobe sent from hello syslog daemon toolocal UDP port 25226.</span></span> <span data-ttu-id="6c77d-128">agente Hello è in attesa di eventi in ingresso su questa porta.</span><span class="sxs-lookup"><span data-stu-id="6c77d-128">hello agent is listening for incoming events on this port.</span></span> <span data-ttu-id="6c77d-129">di seguito Hello è una configurazione di esempio per l'invio di tutti gli eventi dall'agente di toohello hello sistema locale (è possibile modificare hello configurazione toofit le impostazioni locali):</span><span class="sxs-lookup"><span data-stu-id="6c77d-129">hello following is an example configuration for sending all events from hello local system toohello agent (you can modify hello configuration toofit your local settings):</span></span>

1. <span data-ttu-id="6c77d-130">Finestra terminal aprire hello e passare toohello directory */etc/syslog-ng /*</span><span class="sxs-lookup"><span data-stu-id="6c77d-130">Open hello terminal window, and go toohello directory */etc/syslog-ng/*</span></span> 
2. <span data-ttu-id="6c77d-131">Creare un nuovo file *sicurezza-config-omsagent. conf* e aggiungere hello seguente contenuto: OMS_facility = local4</span><span class="sxs-lookup"><span data-stu-id="6c77d-131">Create a new file *security-config-omsagent.conf* and add hello following content:  OMS_facility = local4</span></span>
    
    <span data-ttu-id="6c77d-132">filter f_local4_oms { facility(local4); };</span><span class="sxs-lookup"><span data-stu-id="6c77d-132">filter f_local4_oms { facility(local4); };</span></span>

    <span data-ttu-id="6c77d-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span><span class="sxs-lookup"><span data-stu-id="6c77d-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span></span>

    <span data-ttu-id="6c77d-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span><span class="sxs-lookup"><span data-stu-id="6c77d-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span></span>
    
3. <span data-ttu-id="6c77d-135">Scaricare il file hello *security_events.conf* e posizionare */etc/opt/microsoft/omsagent/conf/omsagent.d/* nel computer dell'agente OMS hello.</span><span class="sxs-lookup"><span data-stu-id="6c77d-135">Download hello file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in hello OMS Agent computer.</span></span>
4. <span data-ttu-id="6c77d-136">Digitare il comando hello seguito daemon syslog di hello toorestart: *per syslog-ng eseguire:*</span><span class="sxs-lookup"><span data-stu-id="6c77d-136">Type hello command below toorestart hello syslog daemon:  *For syslog-ng run:*</span></span>
    
    ```
    sudo service rsyslog restart
    ```

    <span data-ttu-id="6c77d-137">*Per eseguire rsyslog:*</span><span class="sxs-lookup"><span data-stu-id="6c77d-137">*For rsyslog run:*</span></span>
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. <span data-ttu-id="6c77d-138">Digitare il comando hello sotto toorestart hello agente OMS:</span><span class="sxs-lookup"><span data-stu-id="6c77d-138">Type hello command below toorestart hello OMS Agent:</span></span>

    <span data-ttu-id="6c77d-139">*Per eseguire syslog-ng:*</span><span class="sxs-lookup"><span data-stu-id="6c77d-139">*For syslog-ng run:*</span></span>
    
    ```
    sudo service omsagent restart
    ```

    <span data-ttu-id="6c77d-140">*Per eseguire rsyslog:*</span><span class="sxs-lookup"><span data-stu-id="6c77d-140">*For rsyslog run:*</span></span>
    
    ```
    systemctl restart omsagent
    ```
6. <span data-ttu-id="6c77d-141">Digitare comando hello seguente ed esaminare tooconfirm risultato hello che non siano presenti errori nel log dell'agente OMS hello:</span><span class="sxs-lookup"><span data-stu-id="6c77d-141">Type hello command below and review hello result tooconfirm that there are no errors in hello OMS Agent log:</span></span>

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a><span data-ttu-id="6c77d-142">Esaminare gli eventi di sicurezza raccolti</span><span class="sxs-lookup"><span data-stu-id="6c77d-142">Reviewing collected security events</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

<span data-ttu-id="6c77d-143">Al termine del hello configurazione, eventi di protezione hello inizierà toobe caricamento dalla sicurezza di OMS.</span><span class="sxs-lookup"><span data-stu-id="6c77d-143">After hello configuration is over, hello security event will start toobe ingested by OMS Security.</span></span> <span data-ttu-id="6c77d-144">toovisualize tali eventi, aprire hello ricerca Log, digitare il comando di hello *tipo = CommonSecurityLog* in hello campo ricerca e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="6c77d-144">toovisualize those events, open hello Log Search, type hello command *Type=CommonSecurityLog* in hello search field and press ENTER.</span></span> <span data-ttu-id="6c77d-145">Hello esempio seguente viene illustrato il risultato di hello di questo comando, si noti che la sicurezza OMS in questo caso i registri di protezione da più fornitori già caricamento:</span><span class="sxs-lookup"><span data-stu-id="6c77d-145">hello following example shows hello result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span></span>
   
![Valutazione baseline di Sicurezza e controllo di OMS](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

<span data-ttu-id="6c77d-147">È possibile limitare la ricerca per un unico fornitore, ad esempio, Cisco online registra toovisualize, tipo: *tipo = CommonSecurityLog DeviceVendor = Cisco*.</span><span class="sxs-lookup"><span data-stu-id="6c77d-147">You can refine this search for one single vendor, for example, toovisualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span></span> <span data-ttu-id="6c77d-148">Hello "CommonSecurityLog" è predefinite campi per qualsiasi intestazione CEF inclusi extensios base hello, mentre un'altra estensione, se si tratta di "Custom Extension" o, non verrà inserito nel campo "AdditionalExtensions".</span><span class="sxs-lookup"><span data-stu-id="6c77d-148">hello “CommonSecurityLog” has predefined fields for any CEF header including hello basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span></span> <span data-ttu-id="6c77d-149">È possibile utilizzare i campi tooget dedicato di funzionalità di hello campi personalizzati da esso.</span><span class="sxs-lookup"><span data-stu-id="6c77d-149">You can use hello Custom Fields feature tooget dedicated fields from it.</span></span> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="6c77d-150">Accesso ai computer senza valutazione baseline</span><span class="sxs-lookup"><span data-stu-id="6c77d-150">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="6c77d-151">OMS supporta profilo di base membro di dominio hello in Windows Server 2008 R2 fino tooWindows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="6c77d-151">OMS supports hello domain member baseline profile on Windows Server 2008 R2 up tooWindows Server 2012 R2.</span></span> <span data-ttu-id="6c77d-152">La baseline di Windows Server 2016 non è ancora definitiva e verrà aggiunta non appena pubblicata.</span><span class="sxs-lookup"><span data-stu-id="6c77d-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="6c77d-153">Tutti gli altri sistemi operativi analizzati tramite OMS Security and Audit valutazione della linea di base vengono visualizzate in hello **computer privi di valutazione della linea di base** sezione.</span><span class="sxs-lookup"><span data-stu-id="6c77d-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under hello **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="6c77d-154">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="6c77d-154">See also</span></span>
<span data-ttu-id="6c77d-155">In questo documento, si è appreso come tooconnect il tooOMS soluzione CEF.</span><span class="sxs-lookup"><span data-stu-id="6c77d-155">In this document, you learned how tooconnect your CEF solution tooOMS.</span></span> <span data-ttu-id="6c77d-156">toolearn più sulla sicurezza di OMS, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="6c77d-156">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="6c77d-157">Panoramica di Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="6c77d-157">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="6c77d-158">Monitoraggio e risposta tooSecurity avvisi nella soluzione di controllo e protezione di Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="6c77d-158">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="6c77d-159">Monitoraggio delle risorse nella soluzione Operations Management Suite per la sicurezza e il controllo</span><span class="sxs-lookup"><span data-stu-id="6c77d-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

