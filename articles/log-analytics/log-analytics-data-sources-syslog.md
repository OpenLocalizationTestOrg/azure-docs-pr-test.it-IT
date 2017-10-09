---
title: aaaCollect e analizzare i messaggi Syslog in OMS Log Analitica | Documenti Microsoft
description: "Syslog è un protocollo di registrazione di eventi che è tooLinux comuni. In questo articolo viene descritto come raccolta tooconfigure dei messaggi Syslog in Analitica di Log e i dettagli dei record di hello che ha creato nel repository OMS hello."
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
ms.openlocfilehash: 8bfa0bca3f2f18287d1352c98bbaa2a70e41e276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="5e473-104">Origini dati Syslog in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="5e473-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="5e473-105">Syslog è un protocollo di registrazione di eventi che è tooLinux comuni.</span><span class="sxs-lookup"><span data-stu-id="5e473-105">Syslog is an event logging protocol that is common tooLinux.</span></span>  <span data-ttu-id="5e473-106">Applicazioni invierà i messaggi che possono essere archiviati nel computer locale hello o recapitati tooa Syslog agente di raccolta.</span><span class="sxs-lookup"><span data-stu-id="5e473-106">Applications will send messages that may be stored on hello local machine or delivered tooa Syslog collector.</span></span>  <span data-ttu-id="5e473-107">Quando viene installato l'agente OMS per Linux hello, configura hello locale Syslog daemon tooforward messaggi toohello dell'agente.</span><span class="sxs-lookup"><span data-stu-id="5e473-107">When hello OMS Agent for Linux is installed, it configures hello local Syslog daemon tooforward messages toohello agent.</span></span>  <span data-ttu-id="5e473-108">agente Hello invia quindi tooLog messaggio hello Analitica in cui viene creato un record corrispondente nel repository OMS hello.</span><span class="sxs-lookup"><span data-stu-id="5e473-108">hello agent then sends hello message tooLog Analytics where a corresponding record is created in hello OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="5e473-109">Log Analitica supporta la raccolta di messaggi inviati dal rsyslog o syslog-ng, dove rsyslog è daemon predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="5e473-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is hello default daemon.</span></span> <span data-ttu-id="5e473-110">il daemon Hello predefinito syslog nella versione 5 di Red Hat Enterprise Linux CentOS e Oracle Linux (sysklog) non è supportato per la raccolta di eventi syslog.</span><span class="sxs-lookup"><span data-stu-id="5e473-110">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="5e473-111">dati di syslog toocollect da questa versione di queste distribuzioni, hello [daemon rsyslog](http://rsyslog.com) deve essere installato e configurato tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="5e473-111">toocollect syslog data from this version of these distributions, hello [rsyslog daemon](http://rsyslog.com) should be installed and configured tooreplace sysklog.</span></span>
>
>

![Raccolta Syslog](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="5e473-113">Configurazione di Syslog</span><span class="sxs-lookup"><span data-stu-id="5e473-113">Configuring Syslog</span></span>
<span data-ttu-id="5e473-114">Hello agente OMS per Linux verrà raccolti solo gli eventi con strutture di hello e livelli di gravità che vengono specificati nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="5e473-114">hello OMS Agent for Linux will only collect events with hello facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="5e473-115">Tramite il portale di OMS hello o mediante la gestione di file di configurazione di agenti di Linux, è possibile configurare Syslog.</span><span class="sxs-lookup"><span data-stu-id="5e473-115">You can configure Syslog through hello OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-hello-oms-portal"></a><span data-ttu-id="5e473-116">Configurare Syslog nel portale OMS hello</span><span class="sxs-lookup"><span data-stu-id="5e473-116">Configure Syslog in hello OMS portal</span></span>
<span data-ttu-id="5e473-117">Configurare Syslog da hello [menu dati nelle impostazioni di registro Analitica](log-analytics-data-sources.md#configuring-data-sources).</span><span class="sxs-lookup"><span data-stu-id="5e473-117">Configure Syslog from hello [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="5e473-118">Questa configurazione viene recapitata toohello i file di configurazione in ogni agente Linux.</span><span class="sxs-lookup"><span data-stu-id="5e473-118">This configuration is delivered toohello configuration file on each Linux agent.</span></span>

<span data-ttu-id="5e473-119">È possibile aggiungere una nuova funzionalità digitando il nome corrispondente e facendo clic su **+**.</span><span class="sxs-lookup"><span data-stu-id="5e473-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="5e473-120">Per ogni struttura, verranno raccolti solo i messaggi con livelli di gravità hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="5e473-120">For each facility, only messages with hello selected severities will be collected.</span></span>  <span data-ttu-id="5e473-121">Controllare i livelli di gravità di hello per funzionalità di hello specifico che si desidera toocollect.</span><span class="sxs-lookup"><span data-stu-id="5e473-121">Check hello severities for hello particular facility that you want toocollect.</span></span>  <span data-ttu-id="5e473-122">È possibile fornire eventuali criteri aggiuntivi toofilter messaggi.</span><span class="sxs-lookup"><span data-stu-id="5e473-122">You cannot provide any additional criteria toofilter messages.</span></span>

![Configurare Syslog](media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="5e473-124">Per impostazione predefinita, tutte le modifiche di configurazione vengono automaticamente spostate tooall agenti.</span><span class="sxs-lookup"><span data-stu-id="5e473-124">By default, all configuration changes are automatically pushed tooall agents.</span></span>  <span data-ttu-id="5e473-125">Se si desidera tooconfigure Syslog manualmente in ogni agente Linux, quindi deselezionare la casella di hello *Apply below macchine Linux di configurazione toomy*.</span><span class="sxs-lookup"><span data-stu-id="5e473-125">If you want tooconfigure Syslog manually on each Linux agent, then uncheck hello box *Apply below configuration toomy Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="5e473-126">Configurare Syslog sull'agente Linux</span><span class="sxs-lookup"><span data-stu-id="5e473-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="5e473-127">Quando hello [agente OMS è installato in un client Linux](log-analytics-linux-agents.md), l'installazione di un file di configurazione di syslog predefinito che definisce la funzione hello e gravità hello messaggi che vengono raccolti.</span><span class="sxs-lookup"><span data-stu-id="5e473-127">When hello [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines hello facility and severity of hello messages that are collected.</span></span>  <span data-ttu-id="5e473-128">È possibile modificare questa configurazione hello toochange di file.</span><span class="sxs-lookup"><span data-stu-id="5e473-128">You can modify this file toochange hello configuration.</span></span>  <span data-ttu-id="5e473-129">file di configurazione Hello è diversa a seconda di hello Syslog daemon che hello client è installato.</span><span class="sxs-lookup"><span data-stu-id="5e473-129">hello configuration file is different depending on hello Syslog daemon that hello client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="5e473-130">Se si modifica la configurazione di syslog hello, è necessario riavviare i daemon syslog hello hello modifiche tootake effetto.</span><span class="sxs-lookup"><span data-stu-id="5e473-130">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

#### <a name="rsyslog"></a><span data-ttu-id="5e473-131">rsyslog</span><span class="sxs-lookup"><span data-stu-id="5e473-131">rsyslog</span></span>
<span data-ttu-id="5e473-132">Hello file di configurazione per rsyslog si trova in **/etc/rsyslog.d/95-omsagent.conf**.</span><span class="sxs-lookup"><span data-stu-id="5e473-132">hello configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="5e473-133">I contenuti predefiniti sono visualizzati di seguito.</span><span class="sxs-lookup"><span data-stu-id="5e473-133">Its default contents are shown below.</span></span>  <span data-ttu-id="5e473-134">Consente di raccogliere i messaggi syslog inviati dall'agente locale hello per tutte le funzioni con un livello di avviso o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="5e473-134">This collects syslog messages sent from hello local agent for all facilities with a level of warning or higher.</span></span>

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

<span data-ttu-id="5e473-135">È possibile rimuovere una funzionalità di gestione tramite la rimozione della sezione del file di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="5e473-135">You can remove a facility by removing its section of hello configuration file.</span></span>  <span data-ttu-id="5e473-136">È possibile limitare i livelli di gravità di hello vengono raccolti per una particolare funzionalità modificando la voce di tale funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5e473-136">You can limit hello severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="5e473-137">Ad esempio, toolimit hello utente struttura toomessages con gravità maggiore o di errore è modificherebbe dalla riga di hello toohello di file di configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="5e473-137">For example, toolimit hello user facility toomessages with a severity of error or higher you would modify that line of hello configuration file toohello following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="5e473-138">syslog-ng</span><span class="sxs-lookup"><span data-stu-id="5e473-138">syslog-ng</span></span>
<span data-ttu-id="5e473-139">file di configurazione Hello per syslog-ng è percorso **/etc/syslog-ng/syslog-ng.conf**.</span><span class="sxs-lookup"><span data-stu-id="5e473-139">hello configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="5e473-140">I contenuti predefiniti sono visualizzati di seguito.</span><span class="sxs-lookup"><span data-stu-id="5e473-140">Its default contents are shown below.</span></span>  <span data-ttu-id="5e473-141">Consente di raccogliere i messaggi syslog inviati dall'agente locale hello per tutte le funzioni e tutti i livelli di gravità.</span><span class="sxs-lookup"><span data-stu-id="5e473-141">This collects syslog messages sent from hello local agent for all facilities and all severities.</span></span>   

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

<span data-ttu-id="5e473-142">È possibile rimuovere una funzionalità di gestione tramite la rimozione della sezione del file di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="5e473-142">You can remove a facility by removing its section of hello configuration file.</span></span>  <span data-ttu-id="5e473-143">È possibile limitare i livelli di gravità di hello vengono raccolti per una particolare funzionalità rimuovendole dal relativo elenco.</span><span class="sxs-lookup"><span data-stu-id="5e473-143">You can limit hello severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="5e473-144">Ad esempio, toolimit hello utente struttura toojust i messaggi di avviso e critici, è necessario modificare la sezione di hello toohello di file di configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="5e473-144">For example, toolimit hello user facility toojust alert and critical messages, you would modify that section of hello configuration file toohello following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a><span data-ttu-id="5e473-145">Raccolta dei dati da altre porte Syslog</span><span class="sxs-lookup"><span data-stu-id="5e473-145">Collecting data from additional Syslog ports</span></span>
<span data-ttu-id="5e473-146">agente OMS Hello è in attesa per i messaggi Syslog nel client locale di hello sulla porta 25224.</span><span class="sxs-lookup"><span data-stu-id="5e473-146">hello OMS agent listens for Syslog messages on hello local client on port 25224.</span></span>  <span data-ttu-id="5e473-147">Quando viene installato l'agente di hello, una configurazione predefinita di syslog è applicata e hello seguente posizione:</span><span class="sxs-lookup"><span data-stu-id="5e473-147">When hello agent is installed, a default syslog configuration is applied and found in hello following location:</span></span>

* <span data-ttu-id="5e473-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="5e473-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span></span>
* <span data-ttu-id="5e473-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span><span class="sxs-lookup"><span data-stu-id="5e473-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span></span>

<span data-ttu-id="5e473-150">È possibile modificare il numero di porta hello creando due file di configurazione: un file di configurazione FluentD e un file ng di rsyslog o syslog a seconda di daemon Syslog hello è stato installato.</span><span class="sxs-lookup"><span data-stu-id="5e473-150">You can change hello port number by creating two configuration files: a FluentD config file and a rsyslog-or-syslog-ng file depending on hello Syslog daemon you have installed.</span></span>  

* <span data-ttu-id="5e473-151">file di configurazione FluentD Hello deve essere un nuovo file si trova: `/etc/opt/microsoft/omsagent/conf/omsagent.d` e sostituire il valore di hello in hello **porta** voce con il numero di porta personalizzato.</span><span class="sxs-lookup"><span data-stu-id="5e473-151">hello FluentD config file should be a new file located in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` and replace hello value in hello **port** entry with your custom port number.</span></span>

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

* <span data-ttu-id="5e473-152">Per rsyslog, è necessario creare un nuovo file di configurazione si trova: `/etc/rsyslog.d/` e sostituire hello valore % SYSLOG_PORT % con il numero di porta personalizzato.</span><span class="sxs-lookup"><span data-stu-id="5e473-152">For rsyslog, you should create a new configuration file located in: `/etc/rsyslog.d/` and replace hello value %SYSLOG_PORT% with your custom port number.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="5e473-153">Se si modifica questo valore nel file di configurazione hello `95-omsagent.conf`, verrà sovrascritto quando l'agente di hello applica una configurazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5e473-153">If you modify this value in hello configuration file `95-omsagent.conf`, it will be overwritten when hello agent applies a default configuration.</span></span>
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* <span data-ttu-id="5e473-154">Hello syslog-ng configurazione deve essere modificato tramite la copia di configurazione di esempio hello illustrato di seguito e aggiunta hello personalizzate impostazioni modificate toohello fine del file di configurazione di syslog ng.conf hello nella `/etc/syslog-ng/`.</span><span class="sxs-lookup"><span data-stu-id="5e473-154">hello syslog-ng config should be modified by copying hello example configuration shown below and adding hello custom modified settings toohello end of hello syslog-ng.conf configuration file located in `/etc/syslog-ng/`.</span></span>  <span data-ttu-id="5e473-155">Eseguire **non** utilizzare etichetta predefinita hello **% WORKSPACE_ID % _oms** o **% WORKSPACE_ID_OMS**, definire un oggetto personalizzato toohelp etichetta distinguere le modifiche.</span><span class="sxs-lookup"><span data-stu-id="5e473-155">Do **not** use hello default label **%WORKSPACE_ID%_oms** or **%WORKSPACE_ID_OMS**, define a custom label toohelp distinguish your changes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="5e473-156">Se si modificano i valori predefiniti di hello nel file di configurazione di hello, verranno sovrascritti quando l'agente di hello applica una configurazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5e473-156">If you modify hello default values in hello configuration file, they will be overwritten when hello agent applies a default configuration.</span></span>
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

<span data-ttu-id="5e473-157">Dopo aver completato le modifiche di hello, hello Syslog e hello servizio dell'agente OMS è necessario riavviare toobe tooensure hello configurazione modifiche diventano effettive.</span><span class="sxs-lookup"><span data-stu-id="5e473-157">After completing hello changes, hello Syslog and hello OMS agent service needs toobe restarted tooensure hello configuration changes take effect.</span></span>   

## <a name="syslog-record-properties"></a><span data-ttu-id="5e473-158">Proprietà dei record Syslog</span><span class="sxs-lookup"><span data-stu-id="5e473-158">Syslog record properties</span></span>
<span data-ttu-id="5e473-159">Dispongono del tipo di record Syslog **Syslog** e dispone di proprietà hello in hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="5e473-159">Syslog records have a type of **Syslog** and have hello properties in hello following table.</span></span>

| <span data-ttu-id="5e473-160">Proprietà</span><span class="sxs-lookup"><span data-stu-id="5e473-160">Property</span></span> | <span data-ttu-id="5e473-161">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5e473-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5e473-162">Computer</span><span class="sxs-lookup"><span data-stu-id="5e473-162">Computer</span></span> |<span data-ttu-id="5e473-163">Computer in cui hello eventi raccolti da.</span><span class="sxs-lookup"><span data-stu-id="5e473-163">Computer that hello event was collected from.</span></span> |
| <span data-ttu-id="5e473-164">Facility</span><span class="sxs-lookup"><span data-stu-id="5e473-164">Facility</span></span> |<span data-ttu-id="5e473-165">Definisce la parte hello del sistema hello che ha generato il messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="5e473-165">Defines hello part of hello system that generated hello message.</span></span> |
| <span data-ttu-id="5e473-166">HostIP</span><span class="sxs-lookup"><span data-stu-id="5e473-166">HostIP</span></span> |<span data-ttu-id="5e473-167">Indirizzo IP del sistema hello invio messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="5e473-167">IP address of hello system sending hello message.</span></span> |
| <span data-ttu-id="5e473-168">HostName</span><span class="sxs-lookup"><span data-stu-id="5e473-168">HostName</span></span> |<span data-ttu-id="5e473-169">Nome del sistema hello invio messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="5e473-169">Name of hello system sending hello message.</span></span> |
| <span data-ttu-id="5e473-170">SeverityLevel</span><span class="sxs-lookup"><span data-stu-id="5e473-170">SeverityLevel</span></span> |<span data-ttu-id="5e473-171">Livello di gravità dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="5e473-171">Severity level of hello event.</span></span> |
| <span data-ttu-id="5e473-172">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="5e473-172">SyslogMessage</span></span> |<span data-ttu-id="5e473-173">Testo del messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="5e473-173">Text of hello message.</span></span> |
| <span data-ttu-id="5e473-174">ProcessID</span><span class="sxs-lookup"><span data-stu-id="5e473-174">ProcessID</span></span> |<span data-ttu-id="5e473-175">ID del processo di hello che ha generato il messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="5e473-175">ID of hello process that generated hello message.</span></span> |
| <span data-ttu-id="5e473-176">EventTime</span><span class="sxs-lookup"><span data-stu-id="5e473-176">EventTime</span></span> |<span data-ttu-id="5e473-177">Data e ora di hello evento è stato generato.</span><span class="sxs-lookup"><span data-stu-id="5e473-177">Date and time that hello event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="5e473-178">Query di log con record Syslog</span><span class="sxs-lookup"><span data-stu-id="5e473-178">Log queries with Syslog records</span></span>
<span data-ttu-id="5e473-179">Hello nella tabella seguente vengono forniti esempi di query di log che recuperano record Syslog.</span><span class="sxs-lookup"><span data-stu-id="5e473-179">hello following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="5e473-180">Query</span><span class="sxs-lookup"><span data-stu-id="5e473-180">Query</span></span> | <span data-ttu-id="5e473-181">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5e473-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5e473-182">Type=Syslog</span><span class="sxs-lookup"><span data-stu-id="5e473-182">Type=Syslog</span></span> |<span data-ttu-id="5e473-183">Tutti i record Syslog.</span><span class="sxs-lookup"><span data-stu-id="5e473-183">All Syslogs.</span></span> |
| <span data-ttu-id="5e473-184">Type=Syslog SeverityLevel=error</span><span class="sxs-lookup"><span data-stu-id="5e473-184">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="5e473-185">Tutti i record Syslog con livello di gravità errore.</span><span class="sxs-lookup"><span data-stu-id="5e473-185">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="5e473-186">Type=Syslog &#124; measure count() by Computer</span><span class="sxs-lookup"><span data-stu-id="5e473-186">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="5e473-187">Numero di record Syslog per computer.</span><span class="sxs-lookup"><span data-stu-id="5e473-187">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="5e473-188">Type=Syslog &#124; measure count() by Facility</span><span class="sxs-lookup"><span data-stu-id="5e473-188">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="5e473-189">Numero di record Syslog per funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5e473-189">Count of Syslog records by facility.</span></span> |

>[!NOTE]
> <span data-ttu-id="5e473-190">Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi hello sopra query modificherebbe toohello seguente.</span><span class="sxs-lookup"><span data-stu-id="5e473-190">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above queries would change toohello following.</span></span>

> | <span data-ttu-id="5e473-191">Query</span><span class="sxs-lookup"><span data-stu-id="5e473-191">Query</span></span> | <span data-ttu-id="5e473-192">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5e473-192">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5e473-193">syslog</span><span class="sxs-lookup"><span data-stu-id="5e473-193">Syslog</span></span> |<span data-ttu-id="5e473-194">Tutti i record Syslog.</span><span class="sxs-lookup"><span data-stu-id="5e473-194">All Syslogs.</span></span> |
| <span data-ttu-id="5e473-195">Syslog &#124; where SeverityLevel == "error"</span><span class="sxs-lookup"><span data-stu-id="5e473-195">Syslog &#124; where SeverityLevel == "error"</span></span> |<span data-ttu-id="5e473-196">Tutti i record Syslog con livello di gravità errore.</span><span class="sxs-lookup"><span data-stu-id="5e473-196">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="5e473-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span><span class="sxs-lookup"><span data-stu-id="5e473-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span></span> |<span data-ttu-id="5e473-198">Numero di record Syslog per computer.</span><span class="sxs-lookup"><span data-stu-id="5e473-198">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="5e473-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span><span class="sxs-lookup"><span data-stu-id="5e473-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span></span> |<span data-ttu-id="5e473-200">Numero di record Syslog per funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5e473-200">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5e473-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5e473-201">Next steps</span></span>
* <span data-ttu-id="5e473-202">Informazioni su [log ricerche](log-analytics-log-searches.md) tooanalyze hello dati raccolti da origini dati e le soluzioni.</span><span class="sxs-lookup"><span data-stu-id="5e473-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span>
* <span data-ttu-id="5e473-203">Utilizzare [campi personalizzati](log-analytics-custom-fields.md) tooparse dati da record syslog in singoli campi.</span><span class="sxs-lookup"><span data-stu-id="5e473-203">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="5e473-204">[Configurare gli agenti Linux](log-analytics-linux-agents.md) toocollect altri tipi di dati.</span><span class="sxs-lookup"><span data-stu-id="5e473-204">[Configure Linux agents](log-analytics-linux-agents.md) toocollect other types of data.</span></span>
