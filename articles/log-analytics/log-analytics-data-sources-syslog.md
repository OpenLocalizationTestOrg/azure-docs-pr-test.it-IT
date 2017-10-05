---
title: Raccogliere e analizzare messaggi Syslog in Log Analytics di OMS | Documentazione Microsoft
description: "Syslog è un protocollo di registrazione di eventi comunemente usato in Linux. Questo articolo descrive come configurare una raccolta di messaggi Syslog in Log Analytics e illustra i dettagli dei record creati nel repository OMS."
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
ms.date: 07/12/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 7513f405d5c7c05a8e6e2b7b0e6313f23a319c84
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="a4507-104">Origini dati Syslog in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="a4507-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="a4507-105">Syslog è un protocollo di registrazione di eventi comunemente usato in Linux.</span><span class="sxs-lookup"><span data-stu-id="a4507-105">Syslog is an event logging protocol that is common to Linux.</span></span>  <span data-ttu-id="a4507-106">Le applicazioni inviano messaggi che possono essere archiviati nel computer locale o recapitati a un agente di raccolta di Syslog.</span><span class="sxs-lookup"><span data-stu-id="a4507-106">Applications will send messages that may be stored on the local machine or delivered to a Syslog collector.</span></span>  <span data-ttu-id="a4507-107">Quando viene installato, l'agente OMS per Linux configura il daemon Syslog locale in modo da inoltrare i messaggi all'agente.</span><span class="sxs-lookup"><span data-stu-id="a4507-107">When the OMS Agent for Linux is installed, it configures the local Syslog daemon to forward messages to the agent.</span></span>  <span data-ttu-id="a4507-108">Quest'ultimo invia quindi il messaggio a Log Analytics, dove viene creato un record corrispondente nel repository OMS.</span><span class="sxs-lookup"><span data-stu-id="a4507-108">The agent then sends the message to Log Analytics where a corresponding record is created in the OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="a4507-109">Log Analytics supporta la raccolta di messaggi inviati da rsyslog o syslog-ng, dove rsyslog rappresenta il daemon predefinito.</span><span class="sxs-lookup"><span data-stu-id="a4507-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is the default daemon.</span></span> <span data-ttu-id="a4507-110">Il daemon SysLog predefinito nella versione 5 di Red Hat Enterprise Linux, CentOS e nella versione Oracle Linux (sysklog) non è supportato per la raccolta di eventi SysLog.</span><span class="sxs-lookup"><span data-stu-id="a4507-110">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="a4507-111">Per raccogliere i dati di SysLog da questa versione delle distribuzioni, è necessario installare e configurare il [daemon rsyslog](http://rsyslog.com) in modo da sostituire sysklog.</span><span class="sxs-lookup"><span data-stu-id="a4507-111">To collect syslog data from this version of these distributions, the [rsyslog daemon](http://rsyslog.com) should be installed and configured to replace sysklog.</span></span>
>
>

![Raccolta Syslog](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="a4507-113">Configurazione di Syslog</span><span class="sxs-lookup"><span data-stu-id="a4507-113">Configuring Syslog</span></span>
<span data-ttu-id="a4507-114">L'agente OMS per Linux raccoglie solo gli eventi con le funzionalità e i livelli di gravità specificati nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="a4507-114">The OMS Agent for Linux will only collect events with the facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="a4507-115">È possibile configurare Syslog tramite il portale di OMS o mediante la gestione dei file di configurazione sugli agenti Linux.</span><span class="sxs-lookup"><span data-stu-id="a4507-115">You can configure Syslog through the OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-the-oms-portal"></a><span data-ttu-id="a4507-116">Configurare Syslog nel portale di OMS</span><span class="sxs-lookup"><span data-stu-id="a4507-116">Configure Syslog in the OMS portal</span></span>
<span data-ttu-id="a4507-117">Configurare Syslog usando il [menu Dati in Impostazioni di Log Analytics](log-analytics-data-sources.md#configuring-data-sources).</span><span class="sxs-lookup"><span data-stu-id="a4507-117">Configure Syslog from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="a4507-118">Questa configurazione viene distribuita al file di configurazione su ogni agente Linux.</span><span class="sxs-lookup"><span data-stu-id="a4507-118">This configuration is delivered to the configuration file on each Linux agent.</span></span>

<span data-ttu-id="a4507-119">È possibile aggiungere una nuova funzionalità digitando il nome corrispondente e facendo clic su **+**.</span><span class="sxs-lookup"><span data-stu-id="a4507-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="a4507-120">Per ogni funzionalità vengono raccolti solo i messaggi con i livelli di gravità selezionati.</span><span class="sxs-lookup"><span data-stu-id="a4507-120">For each facility, only messages with the selected severities will be collected.</span></span>  <span data-ttu-id="a4507-121">Controllare i livelli di gravità relativi alla funzionalità per la quale si vuole raccogliere i dati.</span><span class="sxs-lookup"><span data-stu-id="a4507-121">Check the severities for the particular facility that you want to collect.</span></span>  <span data-ttu-id="a4507-122">Non è possibile specificare altri criteri per filtrare i messaggi.</span><span class="sxs-lookup"><span data-stu-id="a4507-122">You cannot provide any additional criteria to filter messages.</span></span>

![Configurare Syslog](media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="a4507-124">Per impostazione predefinita, viene eseguito automaticamente il push di tutte le modifiche di configurazione in tutti gli agenti.</span><span class="sxs-lookup"><span data-stu-id="a4507-124">By default, all configuration changes are automatically pushed to all agents.</span></span>  <span data-ttu-id="a4507-125">Per configurare Syslog manualmente su ogni agente Linux, deselezionare la casella *Apply below configuration to my Linux machines*(Applica la configurazione seguente ai computer Linux in uso).</span><span class="sxs-lookup"><span data-stu-id="a4507-125">If you want to configure Syslog manually on each Linux agent, then uncheck the box *Apply below configuration to my Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="a4507-126">Configurare Syslog sull'agente Linux</span><span class="sxs-lookup"><span data-stu-id="a4507-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="a4507-127">Durante l' [installazione dell'agente OMS in un client Linux](log-analytics-linux-agents.md), viene installato un file di configurazione syslog predefinito che definisce la funzionalità e il livello di gravità dei messaggi raccolti.</span><span class="sxs-lookup"><span data-stu-id="a4507-127">When the [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines the facility and severity of the messages that are collected.</span></span>  <span data-ttu-id="a4507-128">È possibile modificare questo file per cambiare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="a4507-128">You can modify this file to change the configuration.</span></span>  <span data-ttu-id="a4507-129">Il file di configurazione è diverso a seconda del daemon Syslog installato nel client.</span><span class="sxs-lookup"><span data-stu-id="a4507-129">The configuration file is different depending on the Syslog daemon that the client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="a4507-130">Se si modifica la configurazione di SysLog, è necessario riavviare il daemon SysLog per rendere effettive le modifiche.</span><span class="sxs-lookup"><span data-stu-id="a4507-130">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span></span>
>
>

#### <a name="rsyslog"></a><span data-ttu-id="a4507-131">rsyslog</span><span class="sxs-lookup"><span data-stu-id="a4507-131">rsyslog</span></span>
<span data-ttu-id="a4507-132">Il file di configurazione per rsyslog si trova in **/etc/rsyslog.d/95-omsagent.conf**.</span><span class="sxs-lookup"><span data-stu-id="a4507-132">The configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="a4507-133">I contenuti predefiniti sono visualizzati di seguito.</span><span class="sxs-lookup"><span data-stu-id="a4507-133">Its default contents are shown below.</span></span>  <span data-ttu-id="a4507-134">Questo daemon raccoglie i messaggi syslog inviati dall'agente locale per tutte le funzionalità con livello di gravità avviso o superiore.</span><span class="sxs-lookup"><span data-stu-id="a4507-134">This collects syslog messages sent from the local agent for all facilities with a level of warning or higher.</span></span>

    kern.warning       @127.0.0.1:25224
    user.warning       @127.0.0.1:25224
    daemon.warning     @127.0.0.1:25224
    auth.warning       @127.0.0.1:25224
    syslog.warning     @127.0.0.1:25224
    uucp.warning       @127.0.0.1:25224
    authpriv.warning   @127.0.0.1:25224
    ftp.warning        @127.0.0.1:25224
    cron.warning       @127.0.0.1:25224
    local0.warning     @127.0.0.1:25224
    local1.warning     @127.0.0.1:25224
    local2.warning     @127.0.0.1:25224
    local3.warning     @127.0.0.1:25224
    local4.warning     @127.0.0.1:25224
    local5.warning     @127.0.0.1:25224
    local6.warning     @127.0.0.1:25224
    local7.warning     @127.0.0.1:25224

<span data-ttu-id="a4507-135">È possibile rimuovere una funzionalità eliminando la sezione corrispondente del file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="a4507-135">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="a4507-136">È possibile limitare i livelli di gravità che vengono raccolti per una particolare funzionalità modificando la voce relativa a tale funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a4507-136">You can limit the severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="a4507-137">Ad esempio, per limitare la funzionalità utente ai messaggi con livello di gravità errore o superiore, modificare la riga del file di configurazione nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="a4507-137">For example, to limit the user facility to messages with a severity of error or higher you would modify that line of the configuration file to the following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="a4507-138">syslog-ng</span><span class="sxs-lookup"><span data-stu-id="a4507-138">syslog-ng</span></span>
<span data-ttu-id="a4507-139">Il file di configurazione per syslog-ng si trova in **/etc/syslog-ng/syslog-ng.conf**.</span><span class="sxs-lookup"><span data-stu-id="a4507-139">The configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="a4507-140">I contenuti predefiniti sono visualizzati di seguito.</span><span class="sxs-lookup"><span data-stu-id="a4507-140">Its default contents are shown below.</span></span>  <span data-ttu-id="a4507-141">Questo daemon raccoglie i messaggi syslog inviati dall'agente locale per tutte le funzionalità e tutti i livelli di gravità.</span><span class="sxs-lookup"><span data-stu-id="a4507-141">This collects syslog messages sent from the local agent for all facilities and all severities.</span></span>   

    #
    # Warnings (except iptables) in one file:
    #
    destination warn { file("/var/log/warn" fsync(yes)); };
    log { source(src); filter(f_warn); destination(warn); };

    #OMS_Destination
    destination d_oms { udp("127.0.0.1" port(25224)); };

    #OMS_facility = auth
    filter f_auth_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(auth); };
    log { source(src); filter(f_auth_oms); destination(d_oms); };

    #OMS_facility = authpriv
    filter f_authpriv_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(authpriv); };
    log { source(src); filter(f_authpriv_oms); destination(d_oms); };

    #OMS_facility = cron
    filter f_cron_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(cron); };
    log { source(src); filter(f_cron_oms); destination(d_oms); };

    #OMS_facility = daemon
    filter f_daemon_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(daemon); };
    log { source(src); filter(f_daemon_oms); destination(d_oms); };

    #OMS_facility = kern
    filter f_kern_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(kern); };
    log { source(src); filter(f_kern_oms); destination(d_oms); };

    #OMS_facility = local0
    filter f_local0_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local0); };
    log { source(src); filter(f_local0_oms); destination(d_oms); };

    #OMS_facility = local1
    filter f_local1_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local1); };
    log { source(src); filter(f_local1_oms); destination(d_oms); };

    #OMS_facility = mail
    filter f_mail_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(mail); };
    log { source(src); filter(f_mail_oms); destination(d_oms); };

    #OMS_facility = syslog
    filter f_syslog_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(syslog); };
    log { source(src); filter(f_syslog_oms); destination(d_oms); };

    #OMS_facility = user
    filter f_user_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };

<span data-ttu-id="a4507-142">È possibile rimuovere una funzionalità eliminando la sezione corrispondente del file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="a4507-142">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="a4507-143">È possibile limitare i livelli di gravità che vengono raccolti per una particolare funzionalità rimuovendoli dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="a4507-143">You can limit the severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="a4507-144">Per limitare la funzionalità utente ai messaggi di avviso e critici, modificare la sezione del file di configurazione nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="a4507-144">For example, to limit the user facility to just alert and critical messages, you would modify that section of the configuration file to the following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a><span data-ttu-id="a4507-145">Raccolta dei dati da altre porte Syslog</span><span class="sxs-lookup"><span data-stu-id="a4507-145">Collecting data from additional Syslog ports</span></span>
<span data-ttu-id="a4507-146">L'agente OMS rimane in ascolto dei messaggi Syslog nel client locale sulla porta 25224.</span><span class="sxs-lookup"><span data-stu-id="a4507-146">The OMS agent listens for Syslog messages on the local client on port 25224.</span></span>  <span data-ttu-id="a4507-147">Quando l'agente viene installato, viene applicata una configurazione di SysLog predefinita, disponibile nella posizione seguente:</span><span class="sxs-lookup"><span data-stu-id="a4507-147">When the agent is installed, a default syslog configuration is applied and found in the following location:</span></span>

* <span data-ttu-id="a4507-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="a4507-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span></span>
* <span data-ttu-id="a4507-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span><span class="sxs-lookup"><span data-stu-id="a4507-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span></span>

<span data-ttu-id="a4507-150">È possibile modificare il numero di porta creando due file di configurazione: un file config FluentD e un file rsyslog-or-syslog-ng a seconda del daemon Syslog che è stato installato.</span><span class="sxs-lookup"><span data-stu-id="a4507-150">You can change the port number by creating two configuration files: a FluentD config file and a rsyslog-or-syslog-ng file depending on the Syslog daemon you have installed.</span></span>  

* <span data-ttu-id="a4507-151">Il file config FluentD deve essere un nuovo file in: `/etc/opt/microsoft/omsagent/conf/omsagent.d`. Sostituire il valore della **porta** con il numero di porta personalizzato.</span><span class="sxs-lookup"><span data-stu-id="a4507-151">The FluentD config file should be a new file located in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` and replace the value in the **port** entry with your custom port number.</span></span>

        <source>
          type syslog
          port %SYSLOG_PORT%
          bind 127.0.0.1
          protocol_type udp
          tag oms.syslog
        </source>
        <filter oms.syslog.**>
          type filter_syslog
        </filter>

* <span data-ttu-id="a4507-152">Per rsyslog, creare un nuovo file di configurazione in: `/etc/rsyslog.d/`. Sostituire il valore %SYSLOG_PORT% con il numero di porta personalizzato.</span><span class="sxs-lookup"><span data-stu-id="a4507-152">For rsyslog, you should create a new configuration file located in: `/etc/rsyslog.d/` and replace the value %SYSLOG_PORT% with your custom port number.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="a4507-153">Se questo valore viene modificato nel file di configurazione `95-omsagent.conf`, verrà sovrascritto quando l'agente applicherà una configurazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="a4507-153">If you modify this value in the configuration file `95-omsagent.conf`, it will be overwritten when the agent applies a default configuration.</span></span>
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* <span data-ttu-id="a4507-154">Modificare la configurazione syslog-ng copiando la configurazione di esempio illustrata di seguito e aggiungendo le impostazioni modificate personalizzate alla fine del file di configurazione syslog-ng.conf in `/etc/syslog-ng/`.</span><span class="sxs-lookup"><span data-stu-id="a4507-154">The syslog-ng config should be modified by copying the example configuration shown below and adding the custom modified settings to the end of the syslog-ng.conf configuration file located in `/etc/syslog-ng/`.</span></span>  <span data-ttu-id="a4507-155">**Non** usare l'etichetta predefinita **%WORKSPACE_ID%_oms** o **%WORKSPACE_ID_OMS**. Definire un'etichetta personalizzata per distinguere le modifiche.</span><span class="sxs-lookup"><span data-stu-id="a4507-155">Do **not** use the default label **%WORKSPACE_ID%_oms** or **%WORKSPACE_ID_OMS**, define a custom label to help distinguish your changes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="a4507-156">Se questi valori vengono modificati nel file di configurazione, verranno sovrascritti quando l'agente applicherà una configurazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="a4507-156">If you modify the default values in the configuration file, they will be overwritten when the agent applies a default configuration.</span></span>
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

<span data-ttu-id="a4507-157">Dopo aver completato le modifiche, riavviare Syslog e il servizio agente OMS per assicurarsi che le modifiche apportate alla configurazione abbiano effetto.</span><span class="sxs-lookup"><span data-stu-id="a4507-157">After completing the changes, the Syslog and the OMS agent service needs to be restarted to ensure the configuration changes take effect.</span></span>   

## <a name="syslog-record-properties"></a><span data-ttu-id="a4507-158">Proprietà dei record Syslog</span><span class="sxs-lookup"><span data-stu-id="a4507-158">Syslog record properties</span></span>
<span data-ttu-id="a4507-159">I record Syslog sono di tipo **Syslog** e hanno le proprietà descritte nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="a4507-159">Syslog records have a type of **Syslog** and have the properties in the following table.</span></span>

| <span data-ttu-id="a4507-160">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a4507-160">Property</span></span> | <span data-ttu-id="a4507-161">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4507-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a4507-162">Computer</span><span class="sxs-lookup"><span data-stu-id="a4507-162">Computer</span></span> |<span data-ttu-id="a4507-163">Computer da cui è stato raccolto l'evento.</span><span class="sxs-lookup"><span data-stu-id="a4507-163">Computer that the event was collected from.</span></span> |
| <span data-ttu-id="a4507-164">Facility</span><span class="sxs-lookup"><span data-stu-id="a4507-164">Facility</span></span> |<span data-ttu-id="a4507-165">Parte del sistema che ha generato il messaggio.</span><span class="sxs-lookup"><span data-stu-id="a4507-165">Defines the part of the system that generated the message.</span></span> |
| <span data-ttu-id="a4507-166">HostIP</span><span class="sxs-lookup"><span data-stu-id="a4507-166">HostIP</span></span> |<span data-ttu-id="a4507-167">Indirizzo IP del sistema che ha inviato il messaggio.</span><span class="sxs-lookup"><span data-stu-id="a4507-167">IP address of the system sending the message.</span></span> |
| <span data-ttu-id="a4507-168">HostName</span><span class="sxs-lookup"><span data-stu-id="a4507-168">HostName</span></span> |<span data-ttu-id="a4507-169">Nome del sistema che ha inviato il messaggio.</span><span class="sxs-lookup"><span data-stu-id="a4507-169">Name of the system sending the message.</span></span> |
| <span data-ttu-id="a4507-170">SeverityLevel</span><span class="sxs-lookup"><span data-stu-id="a4507-170">SeverityLevel</span></span> |<span data-ttu-id="a4507-171">Livello di gravità dell'evento.</span><span class="sxs-lookup"><span data-stu-id="a4507-171">Severity level of the event.</span></span> |
| <span data-ttu-id="a4507-172">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="a4507-172">SyslogMessage</span></span> |<span data-ttu-id="a4507-173">Testo del messaggio.</span><span class="sxs-lookup"><span data-stu-id="a4507-173">Text of the message.</span></span> |
| <span data-ttu-id="a4507-174">ProcessID</span><span class="sxs-lookup"><span data-stu-id="a4507-174">ProcessID</span></span> |<span data-ttu-id="a4507-175">ID del processo che ha generato il messaggio.</span><span class="sxs-lookup"><span data-stu-id="a4507-175">ID of the process that generated the message.</span></span> |
| <span data-ttu-id="a4507-176">EventTime</span><span class="sxs-lookup"><span data-stu-id="a4507-176">EventTime</span></span> |<span data-ttu-id="a4507-177">Data e ora in cui è stato generato l'evento.</span><span class="sxs-lookup"><span data-stu-id="a4507-177">Date and time that the event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="a4507-178">Query di log con record Syslog</span><span class="sxs-lookup"><span data-stu-id="a4507-178">Log queries with Syslog records</span></span>
<span data-ttu-id="a4507-179">La tabella seguente mostra alcuni esempi di query di log che recuperano i record Syslog.</span><span class="sxs-lookup"><span data-stu-id="a4507-179">The following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="a4507-180">Query</span><span class="sxs-lookup"><span data-stu-id="a4507-180">Query</span></span> | <span data-ttu-id="a4507-181">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4507-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a4507-182">Type=Syslog</span><span class="sxs-lookup"><span data-stu-id="a4507-182">Type=Syslog</span></span> |<span data-ttu-id="a4507-183">Tutti i record Syslog.</span><span class="sxs-lookup"><span data-stu-id="a4507-183">All Syslogs.</span></span> |
| <span data-ttu-id="a4507-184">Type=Syslog SeverityLevel=error</span><span class="sxs-lookup"><span data-stu-id="a4507-184">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="a4507-185">Tutti i record Syslog con livello di gravità errore.</span><span class="sxs-lookup"><span data-stu-id="a4507-185">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="a4507-186">Type=Syslog &#124; measure count() by Computer</span><span class="sxs-lookup"><span data-stu-id="a4507-186">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="a4507-187">Numero di record Syslog per computer.</span><span class="sxs-lookup"><span data-stu-id="a4507-187">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="a4507-188">Type=Syslog &#124; measure count() by Facility</span><span class="sxs-lookup"><span data-stu-id="a4507-188">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="a4507-189">Numero di record Syslog per funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a4507-189">Count of Syslog records by facility.</span></span> |

>[!NOTE]
> <span data-ttu-id="a4507-190">Se l'area di lavoro è stata aggiornata al [nuovo linguaggio di query di Log Analytics](log-analytics-log-search-upgrade.md), le query precedenti verranno sostituite da quelle seguenti.</span><span class="sxs-lookup"><span data-stu-id="a4507-190">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above queries would change to the following.</span></span>

> | <span data-ttu-id="a4507-191">Query</span><span class="sxs-lookup"><span data-stu-id="a4507-191">Query</span></span> | <span data-ttu-id="a4507-192">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4507-192">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a4507-193">syslog</span><span class="sxs-lookup"><span data-stu-id="a4507-193">Syslog</span></span> |<span data-ttu-id="a4507-194">Tutti i record Syslog.</span><span class="sxs-lookup"><span data-stu-id="a4507-194">All Syslogs.</span></span> |
| <span data-ttu-id="a4507-195">Syslog &#124; where SeverityLevel == "error"</span><span class="sxs-lookup"><span data-stu-id="a4507-195">Syslog &#124; where SeverityLevel == "error"</span></span> |<span data-ttu-id="a4507-196">Tutti i record Syslog con livello di gravità errore.</span><span class="sxs-lookup"><span data-stu-id="a4507-196">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="a4507-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span><span class="sxs-lookup"><span data-stu-id="a4507-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span></span> |<span data-ttu-id="a4507-198">Numero di record Syslog per computer.</span><span class="sxs-lookup"><span data-stu-id="a4507-198">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="a4507-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span><span class="sxs-lookup"><span data-stu-id="a4507-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span></span> |<span data-ttu-id="a4507-200">Numero di record Syslog per funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a4507-200">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a4507-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4507-201">Next steps</span></span>
* <span data-ttu-id="a4507-202">Informazioni sulle [ricerche nei log](log-analytics-log-searches.md) per analizzare i dati raccolti dalle origini dati e dalle soluzioni.</span><span class="sxs-lookup"><span data-stu-id="a4507-202">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span>
* <span data-ttu-id="a4507-203">Usare [campi personalizzati](log-analytics-custom-fields.md) per analizzare i dati dei record Syslog nei singoli campi.</span><span class="sxs-lookup"><span data-stu-id="a4507-203">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="a4507-204">[Configurare agenti Linux](log-analytics-linux-agents.md) per raccogliere altri tipi di dati.</span><span class="sxs-lookup"><span data-stu-id="a4507-204">[Configure Linux agents](log-analytics-linux-agents.md) to collect other types of data.</span></span>
