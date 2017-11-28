---
title: Raccogliere avvisi Nagios e Zabbix in Log Analytics di OMS | Microsoft Docs
description: "Nagios e Zabbix sono strumenti di monitoraggio open source. È possibile raccogliere avvisi da questi strumenti in Log Analytics per analizzarli insieme ad avvisi provenienti da altre origini.  Questo articolo descrive come configurare l'agente OMS per Linux per raccogliere avvisi da questi sistemi."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 0b64c32e1031e704d50aab0b38eaea41e27d134b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="e858a-105">Raccogliere avvisi da Nagios e Zabbix in Log Analytics tramite l'agente OMS per Linux</span><span class="sxs-lookup"><span data-stu-id="e858a-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="e858a-106">[Nagios](https://www.nagios.org/) e [Zabbix](http://www.zabbix.com/) sono strumenti di monitoraggio open source.</span><span class="sxs-lookup"><span data-stu-id="e858a-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="e858a-107">È possibile raccogliere avvisi da questi strumenti in Log Analytics per analizzarli insieme ad [avvisi provenienti da altre origini](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="e858a-107">You can collect alerts from these tools into Log Analytics in order to analyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="e858a-108">Questo articolo descrive come configurare l'agente OMS per Linux per raccogliere avvisi da questi sistemi.</span><span class="sxs-lookup"><span data-stu-id="e858a-108">This article describes how to configure the OMS Agent for Linux to collect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="e858a-109">Configurare la raccolta di avvisi</span><span class="sxs-lookup"><span data-stu-id="e858a-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="e858a-110">Configurazione della raccolta di avvisi Nagios</span><span class="sxs-lookup"><span data-stu-id="e858a-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="e858a-111">Per raccogliere avvisi, seguire questa procedura nel server Nagios.</span><span class="sxs-lookup"><span data-stu-id="e858a-111">Perform the following steps on the Nagios server to collect alerts.</span></span>

1. <span data-ttu-id="e858a-112">Concedere all'utente **omsagent** l'accesso in lettura al file di log Nagios, ad esempio `/var/log/nagios/nagios.log`.</span><span class="sxs-lookup"><span data-stu-id="e858a-112">Grant the user **omsagent** read access to the Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="e858a-113">Supponendo che il file nagios.log sia di proprietà del gruppo `nagios`, è possibile aggiungere l'utente **omsagent** al gruppo **nagios**.</span><span class="sxs-lookup"><span data-stu-id="e858a-113">Assuming the nagios.log file is owned by the group `nagios`, you can add the user **omsagent** to the **nagios** group.</span></span> 

    <span data-ttu-id="e858a-114">sudo usermod -a -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="e858a-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="e858a-115">Modificare il file di configurazione (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="e858a-115">Modify the configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="e858a-116">Assicurarsi che le voci seguenti siano presenti e non impostate come commento:</span><span class="sxs-lookup"><span data-stu-id="e858a-116">Ensure the following entries are present and not commented out:</span></span>  

        <source>  
          type tail  
          #Update path to point to your nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. <span data-ttu-id="e858a-117">Riavviare il daemon omsagent</span><span class="sxs-lookup"><span data-stu-id="e858a-117">Restart the omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="e858a-118">Configurazione della raccolta di avvisi Zabbix</span><span class="sxs-lookup"><span data-stu-id="e858a-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="e858a-119">Per raccogliere avvisi da un server Zabbix, è necessario specificare un utente e una password come *testo non crittografato*.</span><span class="sxs-lookup"><span data-stu-id="e858a-119">To collect alerts from a Zabbix server, you need to specify a user and password in *clear text*.</span></span> <span data-ttu-id="e858a-120">Sebbene non sia la condizione ideale, è consigliabile creare l'utente e assegnargli solo le autorizzazioni per il monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="e858a-120">This is not ideal, but we recommend that you create the user and grant permissions to monitor onlu.</span></span>

<span data-ttu-id="e858a-121">Per raccogliere avvisi, seguire questa procedura nel server Nagios.</span><span class="sxs-lookup"><span data-stu-id="e858a-121">Perform the following steps on the Nagios server to collect alerts.</span></span>

1. <span data-ttu-id="e858a-122">Modificare il file di configurazione (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="e858a-122">Modify the configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="e858a-123">Assicurarsi che le voci seguenti siano presenti e non impostate come commento.</span><span class="sxs-lookup"><span data-stu-id="e858a-123">Ensure the following entries are present and not commented out.</span></span>  <span data-ttu-id="e858a-124">Modificare il nome utente e la password con valori appropriati per l'ambiente Zabbix.</span><span class="sxs-lookup"><span data-stu-id="e858a-124">Change the user name and password to values for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="e858a-125">Riavviare il daemon omsagent</span><span class="sxs-lookup"><span data-stu-id="e858a-125">Restart the omsagent daemon</span></span>

    <span data-ttu-id="e858a-126">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="e858a-126">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="e858a-127">Record di avvisi</span><span class="sxs-lookup"><span data-stu-id="e858a-127">Alert records</span></span>
<span data-ttu-id="e858a-128">È possibile recuperare record di avvisi da Nagios e Zabbix usando le [ricerche log](log-analytics-log-searches.md) in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="e858a-128">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="e858a-129">Record di avvisi Nagios</span><span class="sxs-lookup"><span data-stu-id="e858a-129">Nagios Alert records</span></span>

<span data-ttu-id="e858a-130">Nei record di avvisi raccolti da Nagios, la proprietà **Tipo** è impostata su **Avviso** e **SourceSystem** su **Nagios**.</span><span class="sxs-lookup"><span data-stu-id="e858a-130">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="e858a-131">Includono le proprietà elencate nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="e858a-131">They have the properties in the following table.</span></span>

| <span data-ttu-id="e858a-132">Proprietà</span><span class="sxs-lookup"><span data-stu-id="e858a-132">Property</span></span> | <span data-ttu-id="e858a-133">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e858a-133">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e858a-134">Tipo</span><span class="sxs-lookup"><span data-stu-id="e858a-134">Type</span></span> |<span data-ttu-id="e858a-135">*Avviso*</span><span class="sxs-lookup"><span data-stu-id="e858a-135">*Alert*</span></span> |
| <span data-ttu-id="e858a-136">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="e858a-136">SourceSystem</span></span> |<span data-ttu-id="e858a-137">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="e858a-137">*Nagios*</span></span> |
| <span data-ttu-id="e858a-138">AlertName</span><span class="sxs-lookup"><span data-stu-id="e858a-138">AlertName</span></span> |<span data-ttu-id="e858a-139">Nome dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="e858a-139">Name of the alert.</span></span> |
| <span data-ttu-id="e858a-140">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="e858a-140">AlertDescription</span></span> | <span data-ttu-id="e858a-141">Descrizione dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="e858a-141">Description of the alert.</span></span> |
| <span data-ttu-id="e858a-142">AlertState</span><span class="sxs-lookup"><span data-stu-id="e858a-142">AlertState</span></span> | <span data-ttu-id="e858a-143">Stato del servizio o dell'host.</span><span class="sxs-lookup"><span data-stu-id="e858a-143">Status of the service or host.</span></span><br><br><span data-ttu-id="e858a-144">OK</span><span class="sxs-lookup"><span data-stu-id="e858a-144">OK</span></span><br><span data-ttu-id="e858a-145">WARNING</span><span class="sxs-lookup"><span data-stu-id="e858a-145">WARNING</span></span><br><span data-ttu-id="e858a-146">UP</span><span class="sxs-lookup"><span data-stu-id="e858a-146">UP</span></span><br><span data-ttu-id="e858a-147">DOWN</span><span class="sxs-lookup"><span data-stu-id="e858a-147">DOWN</span></span> |
| <span data-ttu-id="e858a-148">HostName</span><span class="sxs-lookup"><span data-stu-id="e858a-148">HostName</span></span> | <span data-ttu-id="e858a-149">Nome dell'host che ha creato l'avviso.</span><span class="sxs-lookup"><span data-stu-id="e858a-149">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="e858a-150">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="e858a-150">PriorityNumber</span></span> | <span data-ttu-id="e858a-151">Livello di priorità dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="e858a-151">Priority level of the alert.</span></span> |
| <span data-ttu-id="e858a-152">StateType</span><span class="sxs-lookup"><span data-stu-id="e858a-152">StateType</span></span> | <span data-ttu-id="e858a-153">Tipo di stato dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="e858a-153">The type of state of the alert.</span></span><br><br><span data-ttu-id="e858a-154">SOFT: problema che non è stato ricontrollato.</span><span class="sxs-lookup"><span data-stu-id="e858a-154">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="e858a-155">HARD: problema che è stata ricontrollato un determinato numero di volte.</span><span class="sxs-lookup"><span data-stu-id="e858a-155">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="e858a-156">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="e858a-156">TimeGenerated</span></span> |<span data-ttu-id="e858a-157">Data e ora in cui è stato creato l'avviso.</span><span class="sxs-lookup"><span data-stu-id="e858a-157">Date and time the alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="e858a-158">Record di avvisi Zabbix</span><span class="sxs-lookup"><span data-stu-id="e858a-158">Zabbix alert records</span></span>
<span data-ttu-id="e858a-159">Nei record di avvisi raccolti da Zabbix, la proprietà **Tipo** è impostata su **Avviso** e **SourceSystem** su **Zabbix**.</span><span class="sxs-lookup"><span data-stu-id="e858a-159">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="e858a-160">Includono le proprietà elencate nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="e858a-160">They have the properties in the following table.</span></span>

| <span data-ttu-id="e858a-161">Proprietà</span><span class="sxs-lookup"><span data-stu-id="e858a-161">Property</span></span> | <span data-ttu-id="e858a-162">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e858a-162">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e858a-163">Tipo</span><span class="sxs-lookup"><span data-stu-id="e858a-163">Type</span></span> |<span data-ttu-id="e858a-164">*Avviso*</span><span class="sxs-lookup"><span data-stu-id="e858a-164">*Alert*</span></span> |
| <span data-ttu-id="e858a-165">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="e858a-165">SourceSystem</span></span> |<span data-ttu-id="e858a-166">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="e858a-166">*Zabbix*</span></span> |
| <span data-ttu-id="e858a-167">AlertName</span><span class="sxs-lookup"><span data-stu-id="e858a-167">AlertName</span></span> | <span data-ttu-id="e858a-168">Nome dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="e858a-168">Name of the alert.</span></span> |
| <span data-ttu-id="e858a-169">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="e858a-169">AlertPriority</span></span> | <span data-ttu-id="e858a-170">Gravità dell'avviso</span><span class="sxs-lookup"><span data-stu-id="e858a-170">Severity of the alert.</span></span><br><br><span data-ttu-id="e858a-171">non classificata</span><span class="sxs-lookup"><span data-stu-id="e858a-171">not classified</span></span><br><span data-ttu-id="e858a-172">Informazioni</span><span class="sxs-lookup"><span data-stu-id="e858a-172">information</span></span><br><span data-ttu-id="e858a-173">Avviso</span><span class="sxs-lookup"><span data-stu-id="e858a-173">warning</span></span><br><span data-ttu-id="e858a-174">average</span><span class="sxs-lookup"><span data-stu-id="e858a-174">average</span></span><br><span data-ttu-id="e858a-175">elevata</span><span class="sxs-lookup"><span data-stu-id="e858a-175">high</span></span><br><span data-ttu-id="e858a-176">emergenza</span><span class="sxs-lookup"><span data-stu-id="e858a-176">disaster</span></span>  |
| <span data-ttu-id="e858a-177">AlertState</span><span class="sxs-lookup"><span data-stu-id="e858a-177">AlertState</span></span> | <span data-ttu-id="e858a-178">Stato dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="e858a-178">State of the alert.</span></span><br><br><span data-ttu-id="e858a-179">0: stato aggiornato.</span><span class="sxs-lookup"><span data-stu-id="e858a-179">0 - State is up to date.</span></span><br><span data-ttu-id="e858a-180">1: stato sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="e858a-180">1 - State is unknown.</span></span>  |
| <span data-ttu-id="e858a-181">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="e858a-181">AlertTypeNumber</span></span> | <span data-ttu-id="e858a-182">Specifica se l'avviso può generare più eventi relativi a problemi.</span><span class="sxs-lookup"><span data-stu-id="e858a-182">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="e858a-183">0: stato aggiornato.</span><span class="sxs-lookup"><span data-stu-id="e858a-183">0 - State is up to date.</span></span><br><span data-ttu-id="e858a-184">1: stato sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="e858a-184">1 - State is unknown.</span></span>    |
| <span data-ttu-id="e858a-185">Commenti</span><span class="sxs-lookup"><span data-stu-id="e858a-185">Comments</span></span> | <span data-ttu-id="e858a-186">Commenti aggiuntivi per l'avviso.</span><span class="sxs-lookup"><span data-stu-id="e858a-186">Additional comments for alert.</span></span> |
| <span data-ttu-id="e858a-187">HostName</span><span class="sxs-lookup"><span data-stu-id="e858a-187">HostName</span></span> | <span data-ttu-id="e858a-188">Nome dell'host che ha creato l'avviso.</span><span class="sxs-lookup"><span data-stu-id="e858a-188">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="e858a-189">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="e858a-189">PriorityNumber</span></span> | <span data-ttu-id="e858a-190">Valore che indica il livello di gravità dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="e858a-190">Value indicating severity of the alert.</span></span><br><br><span data-ttu-id="e858a-191">0: non classificata</span><span class="sxs-lookup"><span data-stu-id="e858a-191">0 - not classified</span></span><br><span data-ttu-id="e858a-192">1: informazioni</span><span class="sxs-lookup"><span data-stu-id="e858a-192">1 - information</span></span><br><span data-ttu-id="e858a-193">2: avviso</span><span class="sxs-lookup"><span data-stu-id="e858a-193">2 - warning</span></span><br><span data-ttu-id="e858a-194">3: media</span><span class="sxs-lookup"><span data-stu-id="e858a-194">3 - average</span></span><br><span data-ttu-id="e858a-195">4: elevata</span><span class="sxs-lookup"><span data-stu-id="e858a-195">4 - high</span></span><br><span data-ttu-id="e858a-196">5: emergenza</span><span class="sxs-lookup"><span data-stu-id="e858a-196">5 - disaster</span></span> |
| <span data-ttu-id="e858a-197">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="e858a-197">TimeGenerated</span></span> |<span data-ttu-id="e858a-198">Data e ora in cui è stato creato l'avviso.</span><span class="sxs-lookup"><span data-stu-id="e858a-198">Date and time the alert was created.</span></span> |
| <span data-ttu-id="e858a-199">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="e858a-199">TimeLastModified</span></span> |<span data-ttu-id="e858a-200">Data e ora in cui è stato modificato lo stato dell'avviso per l'ultima volta.</span><span class="sxs-lookup"><span data-stu-id="e858a-200">Date and time the state of the alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="e858a-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e858a-201">Next steps</span></span>
* <span data-ttu-id="e858a-202">Informazioni sugli [avvisi](log-analytics-alerts.md) in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="e858a-202">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="e858a-203">Informazioni sulle [ricerche nei log](log-analytics-log-searches.md) per analizzare i dati raccolti dalle origini dati e dalle soluzioni.</span><span class="sxs-lookup"><span data-stu-id="e858a-203">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
