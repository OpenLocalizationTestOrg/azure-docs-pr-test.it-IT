---
title: gli avvisi Nagios e Zabbix aaaCollect in OMS Log Analitica | Documenti Microsoft
description: "Nagios e Zabbix sono strumenti di monitoraggio open source. È possibile raccogliere gli avvisi da questi strumenti in Analitica di Log in ordine tooanalyze li insieme gli avvisi generati da altre origini.  In questo articolo viene descritto come tooconfigure hello agente OMS per Linux toocollect avvisi da questi sistemi."
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
ms.openlocfilehash: 23e2252e4fed8bc87baec063694a8472ca84220d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="affa9-105">Raccogliere avvisi da Nagios e Zabbix in Log Analytics tramite l'agente OMS per Linux</span><span class="sxs-lookup"><span data-stu-id="affa9-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="affa9-106">[Nagios](https://www.nagios.org/) e [Zabbix](http://www.zabbix.com/) sono strumenti di monitoraggio open source.</span><span class="sxs-lookup"><span data-stu-id="affa9-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="affa9-107">È possibile raccogliere gli avvisi da questi strumenti in Analitica di Log in ordine tooanalyze lungo con [gli avvisi generati da altre origini](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="affa9-107">You can collect alerts from these tools into Log Analytics in order tooanalyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="affa9-108">In questo articolo viene descritto come tooconfigure hello agente OMS per Linux toocollect avvisi da questi sistemi.</span><span class="sxs-lookup"><span data-stu-id="affa9-108">This article describes how tooconfigure hello OMS Agent for Linux toocollect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="affa9-109">Configurare la raccolta di avvisi</span><span class="sxs-lookup"><span data-stu-id="affa9-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="affa9-110">Configurazione della raccolta di avvisi Nagios</span><span class="sxs-lookup"><span data-stu-id="affa9-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="affa9-111">Eseguire operazioni sugli avvisi di toocollect server Nagios hello hello.</span><span class="sxs-lookup"><span data-stu-id="affa9-111">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="affa9-112">Concedere all'utente di hello **omsagent** file di log Nagios toohello accesso in lettura (ad esempio `/var/log/nagios/nagios.log`).</span><span class="sxs-lookup"><span data-stu-id="affa9-112">Grant hello user **omsagent** read access toohello Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="affa9-113">Supponendo che i file nagios.log hello è di proprietà di gruppo hello `nagios`, è possibile aggiungere l'utente hello **omsagent** toohello **nagios** gruppo.</span><span class="sxs-lookup"><span data-stu-id="affa9-113">Assuming hello nagios.log file is owned by hello group `nagios`, you can add hello user **omsagent** toohello **nagios** group.</span></span> 

    <span data-ttu-id="affa9-114">sudo usermod -a -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="affa9-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="affa9-115">Modificare i file di configurazione hello (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="affa9-115">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="affa9-116">Verificare che siano presenti e non come commento hello seguenti voci:</span><span class="sxs-lookup"><span data-stu-id="affa9-116">Ensure hello following entries are present and not commented out:</span></span>  

        <source>  
          type tail  
          #Update path toopoint tooyour nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. <span data-ttu-id="affa9-117">Riavviare i daemon omsagent hello</span><span class="sxs-lookup"><span data-stu-id="affa9-117">Restart hello omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="affa9-118">Configurazione della raccolta di avvisi Zabbix</span><span class="sxs-lookup"><span data-stu-id="affa9-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="affa9-119">toocollect gli avvisi da un server Zabbix, è necessario toospecify un utente e password in *cancellare il testo*.</span><span class="sxs-lookup"><span data-stu-id="affa9-119">toocollect alerts from a Zabbix server, you need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="affa9-120">Non è ideale, ma è consigliabile creare hello utente e concedere le autorizzazioni toomonitor onlu.</span><span class="sxs-lookup"><span data-stu-id="affa9-120">This is not ideal, but we recommend that you create hello user and grant permissions toomonitor onlu.</span></span>

<span data-ttu-id="affa9-121">Eseguire operazioni sugli avvisi di toocollect server Nagios hello hello.</span><span class="sxs-lookup"><span data-stu-id="affa9-121">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="affa9-122">Modificare i file di configurazione hello (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="affa9-122">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="affa9-123">Verificare hello voci seguenti siano presenti e non impostate come commento.  Modificare toovalues hello utente nome e una password per l'ambiente Zabbix.</span><span class="sxs-lookup"><span data-stu-id="affa9-123">Ensure hello following entries are present and not commented out.  Change hello user name and password toovalues for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="affa9-124">Riavviare i daemon omsagent hello</span><span class="sxs-lookup"><span data-stu-id="affa9-124">Restart hello omsagent daemon</span></span>

    <span data-ttu-id="affa9-125">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="affa9-125">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="affa9-126">Record di avvisi</span><span class="sxs-lookup"><span data-stu-id="affa9-126">Alert records</span></span>
<span data-ttu-id="affa9-127">È possibile recuperare record di avvisi da Nagios e Zabbix usando le [ricerche log](log-analytics-log-searches.md) in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="affa9-127">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="affa9-128">Record di avvisi Nagios</span><span class="sxs-lookup"><span data-stu-id="affa9-128">Nagios Alert records</span></span>

<span data-ttu-id="affa9-129">Nei record di avvisi raccolti da Nagios, la proprietà **Tipo** è impostata su **Avviso** e **SourceSystem** su **Nagios**.</span><span class="sxs-lookup"><span data-stu-id="affa9-129">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="affa9-130">Presentano proprietà hello in hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="affa9-130">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="affa9-131">Proprietà</span><span class="sxs-lookup"><span data-stu-id="affa9-131">Property</span></span> | <span data-ttu-id="affa9-132">Descrizione</span><span class="sxs-lookup"><span data-stu-id="affa9-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="affa9-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="affa9-133">Type</span></span> |<span data-ttu-id="affa9-134">*Avviso*</span><span class="sxs-lookup"><span data-stu-id="affa9-134">*Alert*</span></span> |
| <span data-ttu-id="affa9-135">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="affa9-135">SourceSystem</span></span> |<span data-ttu-id="affa9-136">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="affa9-136">*Nagios*</span></span> |
| <span data-ttu-id="affa9-137">AlertName</span><span class="sxs-lookup"><span data-stu-id="affa9-137">AlertName</span></span> |<span data-ttu-id="affa9-138">Nome dell'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="affa9-138">Name of hello alert.</span></span> |
| <span data-ttu-id="affa9-139">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="affa9-139">AlertDescription</span></span> | <span data-ttu-id="affa9-140">Descrizione dell'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="affa9-140">Description of hello alert.</span></span> |
| <span data-ttu-id="affa9-141">AlertState</span><span class="sxs-lookup"><span data-stu-id="affa9-141">AlertState</span></span> | <span data-ttu-id="affa9-142">Stato del servizio hello o dell'host.</span><span class="sxs-lookup"><span data-stu-id="affa9-142">Status of hello service or host.</span></span><br><br><span data-ttu-id="affa9-143">OK</span><span class="sxs-lookup"><span data-stu-id="affa9-143">OK</span></span><br><span data-ttu-id="affa9-144">WARNING</span><span class="sxs-lookup"><span data-stu-id="affa9-144">WARNING</span></span><br><span data-ttu-id="affa9-145">UP</span><span class="sxs-lookup"><span data-stu-id="affa9-145">UP</span></span><br><span data-ttu-id="affa9-146">DOWN</span><span class="sxs-lookup"><span data-stu-id="affa9-146">DOWN</span></span> |
| <span data-ttu-id="affa9-147">HostName</span><span class="sxs-lookup"><span data-stu-id="affa9-147">HostName</span></span> | <span data-ttu-id="affa9-148">Nome dell'host hello creati avviso hello.</span><span class="sxs-lookup"><span data-stu-id="affa9-148">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="affa9-149">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="affa9-149">PriorityNumber</span></span> | <span data-ttu-id="affa9-150">Livello di priorità dell'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="affa9-150">Priority level of hello alert.</span></span> |
| <span data-ttu-id="affa9-151">StateType</span><span class="sxs-lookup"><span data-stu-id="affa9-151">StateType</span></span> | <span data-ttu-id="affa9-152">tipo di Hello dello stato di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="affa9-152">hello type of state of hello alert.</span></span><br><br><span data-ttu-id="affa9-153">SOFT: problema che non è stato ricontrollato.</span><span class="sxs-lookup"><span data-stu-id="affa9-153">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="affa9-154">HARD: problema che è stata ricontrollato un determinato numero di volte.</span><span class="sxs-lookup"><span data-stu-id="affa9-154">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="affa9-155">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="affa9-155">TimeGenerated</span></span> |<span data-ttu-id="affa9-156">Data e ora avviso hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="affa9-156">Date and time hello alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="affa9-157">Record di avvisi Zabbix</span><span class="sxs-lookup"><span data-stu-id="affa9-157">Zabbix alert records</span></span>
<span data-ttu-id="affa9-158">Nei record di avvisi raccolti da Zabbix, la proprietà **Tipo** è impostata su **Avviso** e **SourceSystem** su **Zabbix**.</span><span class="sxs-lookup"><span data-stu-id="affa9-158">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="affa9-159">Presentano proprietà hello in hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="affa9-159">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="affa9-160">Proprietà</span><span class="sxs-lookup"><span data-stu-id="affa9-160">Property</span></span> | <span data-ttu-id="affa9-161">Descrizione</span><span class="sxs-lookup"><span data-stu-id="affa9-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="affa9-162">Tipo</span><span class="sxs-lookup"><span data-stu-id="affa9-162">Type</span></span> |<span data-ttu-id="affa9-163">*Avviso*</span><span class="sxs-lookup"><span data-stu-id="affa9-163">*Alert*</span></span> |
| <span data-ttu-id="affa9-164">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="affa9-164">SourceSystem</span></span> |<span data-ttu-id="affa9-165">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="affa9-165">*Zabbix*</span></span> |
| <span data-ttu-id="affa9-166">AlertName</span><span class="sxs-lookup"><span data-stu-id="affa9-166">AlertName</span></span> | <span data-ttu-id="affa9-167">Nome dell'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="affa9-167">Name of hello alert.</span></span> |
| <span data-ttu-id="affa9-168">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="affa9-168">AlertPriority</span></span> | <span data-ttu-id="affa9-169">Gravità dell'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="affa9-169">Severity of hello alert.</span></span><br><br><span data-ttu-id="affa9-170">non classificata</span><span class="sxs-lookup"><span data-stu-id="affa9-170">not classified</span></span><br><span data-ttu-id="affa9-171">Informazioni</span><span class="sxs-lookup"><span data-stu-id="affa9-171">information</span></span><br><span data-ttu-id="affa9-172">Avviso</span><span class="sxs-lookup"><span data-stu-id="affa9-172">warning</span></span><br><span data-ttu-id="affa9-173">average</span><span class="sxs-lookup"><span data-stu-id="affa9-173">average</span></span><br><span data-ttu-id="affa9-174">elevata</span><span class="sxs-lookup"><span data-stu-id="affa9-174">high</span></span><br><span data-ttu-id="affa9-175">emergenza</span><span class="sxs-lookup"><span data-stu-id="affa9-175">disaster</span></span>  |
| <span data-ttu-id="affa9-176">AlertState</span><span class="sxs-lookup"><span data-stu-id="affa9-176">AlertState</span></span> | <span data-ttu-id="affa9-177">Stato di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="affa9-177">State of hello alert.</span></span><br><br><span data-ttu-id="affa9-178">0 - lo stato è backup toodate.</span><span class="sxs-lookup"><span data-stu-id="affa9-178">0 - State is up toodate.</span></span><br><span data-ttu-id="affa9-179">1: stato sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="affa9-179">1 - State is unknown.</span></span>  |
| <span data-ttu-id="affa9-180">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="affa9-180">AlertTypeNumber</span></span> | <span data-ttu-id="affa9-181">Specifica se l'avviso può generare più eventi relativi a problemi.</span><span class="sxs-lookup"><span data-stu-id="affa9-181">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="affa9-182">0 - lo stato è backup toodate.</span><span class="sxs-lookup"><span data-stu-id="affa9-182">0 - State is up toodate.</span></span><br><span data-ttu-id="affa9-183">1: stato sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="affa9-183">1 - State is unknown.</span></span>    |
| <span data-ttu-id="affa9-184">Commenti</span><span class="sxs-lookup"><span data-stu-id="affa9-184">Comments</span></span> | <span data-ttu-id="affa9-185">Commenti aggiuntivi per l'avviso.</span><span class="sxs-lookup"><span data-stu-id="affa9-185">Additional comments for alert.</span></span> |
| <span data-ttu-id="affa9-186">HostName</span><span class="sxs-lookup"><span data-stu-id="affa9-186">HostName</span></span> | <span data-ttu-id="affa9-187">Nome dell'host hello creati avviso hello.</span><span class="sxs-lookup"><span data-stu-id="affa9-187">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="affa9-188">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="affa9-188">PriorityNumber</span></span> | <span data-ttu-id="affa9-189">Valore che indica la gravità dell'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="affa9-189">Value indicating severity of hello alert.</span></span><br><br><span data-ttu-id="affa9-190">0: non classificata</span><span class="sxs-lookup"><span data-stu-id="affa9-190">0 - not classified</span></span><br><span data-ttu-id="affa9-191">1: informazioni</span><span class="sxs-lookup"><span data-stu-id="affa9-191">1 - information</span></span><br><span data-ttu-id="affa9-192">2: avviso</span><span class="sxs-lookup"><span data-stu-id="affa9-192">2 - warning</span></span><br><span data-ttu-id="affa9-193">3: media</span><span class="sxs-lookup"><span data-stu-id="affa9-193">3 - average</span></span><br><span data-ttu-id="affa9-194">4: elevata</span><span class="sxs-lookup"><span data-stu-id="affa9-194">4 - high</span></span><br><span data-ttu-id="affa9-195">5: emergenza</span><span class="sxs-lookup"><span data-stu-id="affa9-195">5 - disaster</span></span> |
| <span data-ttu-id="affa9-196">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="affa9-196">TimeGenerated</span></span> |<span data-ttu-id="affa9-197">Data e ora avviso hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="affa9-197">Date and time hello alert was created.</span></span> |
| <span data-ttu-id="affa9-198">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="affa9-198">TimeLastModified</span></span> |<span data-ttu-id="affa9-199">Ultima modifica dello stato di hello data e ora dell'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="affa9-199">Date and time hello state of hello alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="affa9-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="affa9-200">Next steps</span></span>
* <span data-ttu-id="affa9-201">Informazioni sugli [avvisi](log-analytics-alerts.md) in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="affa9-201">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="affa9-202">Informazioni su [log ricerche](log-analytics-log-searches.md) tooanalyze hello dati raccolti da origini dati e le soluzioni.</span><span class="sxs-lookup"><span data-stu-id="affa9-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
