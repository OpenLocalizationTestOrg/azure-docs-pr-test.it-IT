---
title: Connessione dei prodotti per la sicurezza alla soluzione Sicurezza e controllo per Operations Management Suite (OMS) | Documentazione Microsoft
description: Questo documento consente di connettere i prodotti per la sicurezza alla soluzione Sicurezza e controllo per Operations Management Suite usando Common Event Format.
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
ms.openlocfilehash: 710a1fe0ce2b7a1841187cf75f4ffb090cc161e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connecting-your-security-products-to-the-operations-management-suite-oms-security-and-audit-solution"></a><span data-ttu-id="1a363-103">Connessione dei prodotti per la sicurezza alla soluzione Sicurezza e controllo per Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="1a363-103">Connecting your security products to the Operations Management Suite (OMS) Security and Audit Solution</span></span> 
<span data-ttu-id="1a363-104">Questo documento consente di connettere i prodotti per la sicurezza alla soluzione Sicurezza e controllo per OMS.</span><span class="sxs-lookup"><span data-stu-id="1a363-104">This document helps you connect your security products into the OMS Security and Audit Solution.</span></span> <span data-ttu-id="1a363-105">Sono supportate le origini seguenti:</span><span class="sxs-lookup"><span data-stu-id="1a363-105">The following sources are supported:</span></span>

- <span data-ttu-id="1a363-106">Eventi Common Event Format (CEF)</span><span class="sxs-lookup"><span data-stu-id="1a363-106">Common Event Format (CEF) events</span></span>
- <span data-ttu-id="1a363-107">Eventi ASA Cisco</span><span class="sxs-lookup"><span data-stu-id="1a363-107">Cisco ASA events</span></span>


## <a name="what-is-cef"></a><span data-ttu-id="1a363-108">Informazioni su CEF</span><span class="sxs-lookup"><span data-stu-id="1a363-108">What is CEF?</span></span>
<span data-ttu-id="1a363-109">Common Event Format (CEF) è un formato standard di settore su messaggi Syslog, usato da molti fornitori di soluzioni per la sicurezza per consentire l'interoperabilità degli eventi tra piattaforme diverse.</span><span class="sxs-lookup"><span data-stu-id="1a363-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors to allow event interoperability among different platforms.</span></span> <span data-ttu-id="1a363-110">La soluzione Sicurezza e controllo per OMS supporta l'inserimento dei dati tramite CEF, che consente di connettere i prodotti per la sicurezza a OMS.</span><span class="sxs-lookup"><span data-stu-id="1a363-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you to connect your security products with OMS Security.</span></span> 

<span data-ttu-id="1a363-111">Tramite la connessione dell'origine dati a OMS, è possibile sfruttare le funzionalità seguenti che fanno parte della piattaforma:</span><span class="sxs-lookup"><span data-stu-id="1a363-111">By connecting your data source to OMS, you are able to take advantage of the following capabilities that are part of this platform:</span></span>

- <span data-ttu-id="1a363-112">Ricerca e controllo</span><span class="sxs-lookup"><span data-stu-id="1a363-112">Search & Correlation</span></span>
- <span data-ttu-id="1a363-113">Controllo</span><span class="sxs-lookup"><span data-stu-id="1a363-113">Auditing</span></span>
- <span data-ttu-id="1a363-114">Avviso</span><span class="sxs-lookup"><span data-stu-id="1a363-114">Alert</span></span>
- <span data-ttu-id="1a363-115">Intelligence per le minacce</span><span class="sxs-lookup"><span data-stu-id="1a363-115">Threat Intelligence</span></span>
- <span data-ttu-id="1a363-116">Errori rilevanti</span><span class="sxs-lookup"><span data-stu-id="1a363-116">Notable Issues</span></span>

## <a name="collection-of-security-solution-logs"></a><span data-ttu-id="1a363-117">Raccolta di log di soluzioni per la sicurezza</span><span class="sxs-lookup"><span data-stu-id="1a363-117">Collection of security solution logs</span></span>

<span data-ttu-id="1a363-118">La soluzione per la sicurezza per OMS supporta la raccolta di log tramite CEF sui log Syslog e [ASA Cisco](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/).</span><span class="sxs-lookup"><span data-stu-id="1a363-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span></span> <span data-ttu-id="1a363-119">In questo esempio, l'origine (ossia il computer che genera i log) è un computer Linux che esegue il daemon syslog-ng e la destinazione è la soluzione per la sicurezza per OMS.</span><span class="sxs-lookup"><span data-stu-id="1a363-119">In this example, the source (computer that generates the logs) is a Linux computer running syslog-ng daemon and the target is OMS Security.</span></span> <span data-ttu-id="1a363-120">Per preparare il computer Linux, è necessario eseguire le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="1a363-120">To prepare the Linux computer you will need to perform the following tasks:</span></span>

- <span data-ttu-id="1a363-121">Scaricare l'agente OMS per Linux, versione 1.2.0-25 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="1a363-121">Download the OMS Agent for Linux, version 1.2.0-25 or above.</span></span>
- <span data-ttu-id="1a363-122">Per installare e caricare l'agente nell'area di lavoro, consultare la sezione **Quick Install Guide** (Guida all'installazione rapida) di [questo articolo](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span><span class="sxs-lookup"><span data-stu-id="1a363-122">Follow the section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) to install and onboard the agent to your workspace.</span></span>

<span data-ttu-id="1a363-123">In genere, l'agente è installato in un computer diverso da quello in cui vengono generati i log.</span><span class="sxs-lookup"><span data-stu-id="1a363-123">Typically, the agent is installed on a different computer from the one on which the logs are generated.</span></span> <span data-ttu-id="1a363-124">Per inoltrare i log al computer agente, vengono in genere richiesti i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1a363-124">Forwarding the logs to the agent machine will usually require the following steps:</span></span>

- <span data-ttu-id="1a363-125">Configurare il prodotto/computer di registrazione per inoltrare gli eventi necessari al daemon syslog (rsyslog o syslog-ng) nel computer agente.</span><span class="sxs-lookup"><span data-stu-id="1a363-125">Configure the logging product/machine to forward the required events to the syslog daemon (rsyslog or syslog-ng) on the agent machine.</span></span>
- <span data-ttu-id="1a363-126">Abilitare il daemon syslog nel computer agente per ricevere messaggi da un sistema remoto.</span><span class="sxs-lookup"><span data-stu-id="1a363-126">Enable the syslog daemon on the agent machine to receive messages from a remote system.</span></span>

<span data-ttu-id="1a363-127">Nel computer agente gli eventi devono essere inviati dal daemon syslog alla porta UDP 25226 locale.</span><span class="sxs-lookup"><span data-stu-id="1a363-127">On the agent machine, the events need to be sent from the syslog daemon to local UDP port 25226.</span></span> <span data-ttu-id="1a363-128">L'agente è in attesa di eventi in ingresso su questa porta.</span><span class="sxs-lookup"><span data-stu-id="1a363-128">The agent is listening for incoming events on this port.</span></span> <span data-ttu-id="1a363-129">Di seguito è riportata una configurazione di esempio per l'invio di tutti gli eventi dal sistema locale all'agente (è possibile modificare la configurazione per adattarla alle proprie impostazioni locali):</span><span class="sxs-lookup"><span data-stu-id="1a363-129">The following is an example configuration for sending all events from the local system to the agent (you can modify the configuration to fit your local settings):</span></span>

1. <span data-ttu-id="1a363-130">Aprire la finestra del terminale e passare alla directory */etc/syslog-ng/*</span><span class="sxs-lookup"><span data-stu-id="1a363-130">Open the terminal window, and go to the directory */etc/syslog-ng/*</span></span> 
2. <span data-ttu-id="1a363-131">Creare un nuovo file *security-config-omsagent.conf* e aggiungere il contenuto seguente: OMS_facility = local4</span><span class="sxs-lookup"><span data-stu-id="1a363-131">Create a new file *security-config-omsagent.conf* and add the following content:  OMS_facility = local4</span></span>
    
    <span data-ttu-id="1a363-132">filter f_local4_oms { facility(local4); };</span><span class="sxs-lookup"><span data-stu-id="1a363-132">filter f_local4_oms { facility(local4); };</span></span>

    <span data-ttu-id="1a363-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span><span class="sxs-lookup"><span data-stu-id="1a363-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span></span>

    <span data-ttu-id="1a363-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span><span class="sxs-lookup"><span data-stu-id="1a363-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span></span>
    
3. <span data-ttu-id="1a363-135">Scaricare il file *security_events.conf* e posizionarlo in */etc/opt/microsoft/omsagent/conf/omsagent.d/* nel computer agente OMS.</span><span class="sxs-lookup"><span data-stu-id="1a363-135">Download the file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in the OMS Agent computer.</span></span>
4. <span data-ttu-id="1a363-136">Digitare il comando seguente per riavviare il daemon syslog: *per syslog-ng eseguire:*</span><span class="sxs-lookup"><span data-stu-id="1a363-136">Type the command below to restart the syslog daemon:  *For syslog-ng run:*</span></span>
    
    ```
    sudo service rsyslog restart
    ```

    <span data-ttu-id="1a363-137">*Per eseguire rsyslog:*</span><span class="sxs-lookup"><span data-stu-id="1a363-137">*For rsyslog run:*</span></span>
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. <span data-ttu-id="1a363-138">Digitare il comando seguente per riavviare l'agente OMS:</span><span class="sxs-lookup"><span data-stu-id="1a363-138">Type the command below to restart the OMS Agent:</span></span>

    <span data-ttu-id="1a363-139">*Per eseguire syslog-ng:*</span><span class="sxs-lookup"><span data-stu-id="1a363-139">*For syslog-ng run:*</span></span>
    
    ```
    sudo service omsagent restart
    ```

    <span data-ttu-id="1a363-140">*Per eseguire rsyslog:*</span><span class="sxs-lookup"><span data-stu-id="1a363-140">*For rsyslog run:*</span></span>
    
    ```
    systemctl restart omsagent
    ```
6. <span data-ttu-id="1a363-141">Digitare il comando seguente ed esaminare il risultato per verificare che non siano presenti errori nel log dell'agente OMS:</span><span class="sxs-lookup"><span data-stu-id="1a363-141">Type the command below and review the result to confirm that there are no errors in the OMS Agent log:</span></span>

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a><span data-ttu-id="1a363-142">Esaminare gli eventi di sicurezza raccolti</span><span class="sxs-lookup"><span data-stu-id="1a363-142">Reviewing collected security events</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

<span data-ttu-id="1a363-143">Al termine della configurazione, gli eventi di sicurezza inizieranno a essere acquisiti dalla soluzione per la sicurezza per OMS.</span><span class="sxs-lookup"><span data-stu-id="1a363-143">After the configuration is over, the security event will start to be ingested by OMS Security.</span></span> <span data-ttu-id="1a363-144">Per visualizzare tali eventi, aprire Ricerca log, digitare il comando *Type=CommonSecurityLog* nel campo di ricerca e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="1a363-144">To visualize those events, open the Log Search, type the command *Type=CommonSecurityLog* in the search field and press ENTER.</span></span> <span data-ttu-id="1a363-145">Nell'esempio seguente viene illustrato il risultato di questo comando. Si noti che la soluzione per la sicurezza per OMS in questo caso ha già acquisito i log per la sicurezza da più fornitori:</span><span class="sxs-lookup"><span data-stu-id="1a363-145">The following example shows the result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span></span>
   
![Valutazione baseline di Sicurezza e controllo di OMS](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

<span data-ttu-id="1a363-147">È possibile perfezionare la ricerca per un unico fornitore. Ad esempio, per visualizzare i log online di Cisco, digitare: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span><span class="sxs-lookup"><span data-stu-id="1a363-147">You can refine this search for one single vendor, for example, to visualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span></span> <span data-ttu-id="1a363-148">"CommonSecurityLog" ha campi predefiniti per qualsiasi intestazione CEF che include le estensioni di base, mentre un'altra estensione "Estensione personalizzata" o meno, verrà inserita nel campo "AdditionalExtensions".</span><span class="sxs-lookup"><span data-stu-id="1a363-148">The “CommonSecurityLog” has predefined fields for any CEF header including the basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span></span> <span data-ttu-id="1a363-149">È possibile usare la funzionalità Campi personalizzati per recuperare i campi dedicati.</span><span class="sxs-lookup"><span data-stu-id="1a363-149">You can use the Custom Fields feature to get dedicated fields from it.</span></span> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="1a363-150">Accesso ai computer senza valutazione baseline</span><span class="sxs-lookup"><span data-stu-id="1a363-150">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="1a363-151">OMS supporta il profilo baseline dei membri di dominio in Windows Server 2008 R2 fino a Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="1a363-151">OMS supports the domain member baseline profile on Windows Server 2008 R2 up to Windows Server 2012 R2.</span></span> <span data-ttu-id="1a363-152">La baseline di Windows Server 2016 non è ancora definitiva e verrà aggiunta non appena pubblicata.</span><span class="sxs-lookup"><span data-stu-id="1a363-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="1a363-153">Tutti i sistemi operativi analizzati tramite la valutazione baseline della soluzione Sicurezza e controllo per OMS vengono visualizzati nella sezione **Computer senza valutazione baseline**.</span><span class="sxs-lookup"><span data-stu-id="1a363-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under the **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="1a363-154">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a363-154">See also</span></span>
<span data-ttu-id="1a363-155">In questo documento è stato descritto come connettere la soluzione CEF a OMS.</span><span class="sxs-lookup"><span data-stu-id="1a363-155">In this document, you learned how to connect your CEF solution to OMS.</span></span> <span data-ttu-id="1a363-156">Per altre informazioni sulle funzionalità di OMS per la sicurezza, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="1a363-156">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="1a363-157">Panoramica di Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="1a363-157">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="1a363-158">Monitoraggio e gestione degli avvisi di sicurezza nella soluzione Operations Management Suite per la sicurezza e il controllo</span><span class="sxs-lookup"><span data-stu-id="1a363-158">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="1a363-159">Monitoraggio delle risorse nella soluzione Operations Management Suite per la sicurezza e il controllo</span><span class="sxs-lookup"><span data-stu-id="1a363-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

