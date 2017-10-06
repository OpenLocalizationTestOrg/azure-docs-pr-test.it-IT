---
title: aaaWork con esistente locale server proxy e Azure AD | Documenti Microsoft
description: Descrive come toowork con esistente proxy server locali.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="f00b2-103">Usare server proxy locali esistenti</span><span class="sxs-lookup"><span data-stu-id="f00b2-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="f00b2-104">Questo articolo viene illustrato come toowork di connettori Proxy di applicazione di Azure Active Directory (Azure AD) tooconfigure con i server proxy in uscita.</span><span class="sxs-lookup"><span data-stu-id="f00b2-104">This article explains how tooconfigure Azure Active Directory (Azure AD) Application Proxy connectors toowork with outbound proxy servers.</span></span> <span data-ttu-id="f00b2-105">È rivolto ai clienti con ambienti di rete che dispongono di proxy esistenti.</span><span class="sxs-lookup"><span data-stu-id="f00b2-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="f00b2-106">Iniziamo esaminando questi scenari di distribuzione principali:</span><span class="sxs-lookup"><span data-stu-id="f00b2-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="f00b2-107">Configurare i connettori toobypass i proxy in uscita in locale.</span><span class="sxs-lookup"><span data-stu-id="f00b2-107">Configure connectors toobypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="f00b2-108">Configurare i connettori toouse un Proxy di applicazione AD Azure di tooaccess proxy in uscita.</span><span class="sxs-lookup"><span data-stu-id="f00b2-108">Configure connectors toouse an outbound proxy tooaccess Azure AD Application Proxy.</span></span>

<span data-ttu-id="f00b2-109">Per ulteriori informazioni sui connettori, vedere [Informazioni sui connettori proxy di applicazione di Azure AD](application-proxy-understand-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="f00b2-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-hello-outbound-proxy"></a><span data-ttu-id="f00b2-110">Configurare il proxy in uscita hello</span><span class="sxs-lookup"><span data-stu-id="f00b2-110">Configure hello outbound proxy</span></span>

<span data-ttu-id="f00b2-111">Se si dispone di un proxy in uscita nell'ambiente in uso, è possibile utilizzare un account proxy in uscita hello tooconfigure di autorizzazioni appropriate.</span><span class="sxs-lookup"><span data-stu-id="f00b2-111">If you have an outbound proxy in your environment, use an account with appropriate permissions tooconfigure hello outbound proxy.</span></span> <span data-ttu-id="f00b2-112">Poiché il programma di installazione hello viene eseguito nel contesto di hello dell'utente hello che sta eseguendo l'installazione di hello, è possibile controllare configurazione hello utilizzando Microsoft Edge o un altro browser Internet.</span><span class="sxs-lookup"><span data-stu-id="f00b2-112">Because hello installer runs in hello context of hello user who's doing hello installation, you can check hello configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="f00b2-113">impostazioni del proxy tooconfigure hello in Microsoft Edge:</span><span class="sxs-lookup"><span data-stu-id="f00b2-113">tooconfigure hello proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="f00b2-114">Andare troppo**impostazioni** > **impostazioni avanzate di visualizzazione** > **aprire le impostazioni del Proxy** > **l'installazione manuale del Proxy** .</span><span class="sxs-lookup"><span data-stu-id="f00b2-114">Go too**Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="f00b2-115">Impostare **utilizza un server proxy** troppo**su**selezionare hello **non utilizzare un server proxy hello per indirizzi locali (intranet)** casella di controllo, quindi scegliere Modifica hello indirizzo e porta tooreflect il server proxy locale.</span><span class="sxs-lookup"><span data-stu-id="f00b2-115">Set **Use a proxy server** too**On**, select hello **Don’t use hello proxy server for local (intranet) addresses** check box, and then change hello address and port tooreflect your local proxy server.</span></span>
3. <span data-ttu-id="f00b2-116">Specificare le impostazioni del proxy necessarie hello.</span><span class="sxs-lookup"><span data-stu-id="f00b2-116">Fill in hello necessary proxy settings.</span></span>

   ![Finestra di dialogo per le impostazioni proxy](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="f00b2-118">Ignorare i proxy in uscita</span><span class="sxs-lookup"><span data-stu-id="f00b2-118">Bypass outbound proxies</span></span>

<span data-ttu-id="f00b2-119">I connettori sono componenti del sistema operativo sottostanti che creano le richieste in uscita.</span><span class="sxs-lookup"><span data-stu-id="f00b2-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="f00b2-120">Questi componenti tentano automaticamente di un server proxy nella rete hello toolocate.</span><span class="sxs-lookup"><span data-stu-id="f00b2-120">These components automatically attempt toolocate a proxy server on hello network.</span></span> <span data-ttu-id="f00b2-121">Utilizzano il rilevamento automatico WPAD (Web Proxy), se è abilitata nell'ambiente di hello.</span><span class="sxs-lookup"><span data-stu-id="f00b2-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in hello environment.</span></span>

<span data-ttu-id="f00b2-122">componenti del sistema operativo Hello tentano toolocate un server proxy eseguendo una ricerca DNS per wpad.domainsuffix.</span><span class="sxs-lookup"><span data-stu-id="f00b2-122">hello OS components attempt toolocate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="f00b2-123">Se viene risolto in DNS, IP toohello viene quindi eseguita una richiesta HTTP indirizzo per WPAD.</span><span class="sxs-lookup"><span data-stu-id="f00b2-123">If this resolves in DNS, an HTTP request is then made toohello IP address for wpad.dat.</span></span> <span data-ttu-id="f00b2-124">La richiesta diventa script di configurazione proxy hello nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="f00b2-124">This request becomes hello proxy configuration script in your environment.</span></span> <span data-ttu-id="f00b2-125">connettore di Hello Usa questo tooselect di script, un server proxy in uscita.</span><span class="sxs-lookup"><span data-stu-id="f00b2-125">hello connector uses this script tooselect an outbound proxy server.</span></span> <span data-ttu-id="f00b2-126">Tuttavia, connettore traffico potrà comunque non passa attraverso, a causa delle impostazioni di configurazione aggiuntive necessarie sul proxy hello.</span><span class="sxs-lookup"><span data-stu-id="f00b2-126">However, connector traffic might still not go through, because of additional configuration settings needed on hello proxy.</span></span>

<span data-ttu-id="f00b2-127">È possibile configurare hello connettore toobypass toohello connettività Azure di indirizzare il tooensure proxy locale che utilizza i servizi.</span><span class="sxs-lookup"><span data-stu-id="f00b2-127">You can configure hello connector toobypass your on-premises proxy tooensure that it uses direct connectivity toohello Azure services.</span></span> <span data-ttu-id="f00b2-128">Questo approccio è consigliato (se i criteri di rete consentono), in quanto significa che si dispone di una minore toomaintain di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f00b2-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration toomaintain.</span></span>

<span data-ttu-id="f00b2-129">utilizzo di proxy in uscita toodisable per connettore hello, modificare il file di C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config hello e hello *system.net* sezione illustrata in questo esempio di codice :</span><span class="sxs-lookup"><span data-stu-id="f00b2-129">toodisable outbound proxy usage for hello connector, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
<span data-ttu-id="f00b2-130">tooensure che il servizio di aggiornamento del connettore hello ignora inoltre proxy hello, creare un file di ApplicationProxyConnectorUpdaterService.exe.config toohello modifica simile all'aggiornamento del connettore Proxy C:\Program Files\Microsoft AAD App.</span><span class="sxs-lookup"><span data-stu-id="f00b2-130">tooensure that hello Connector Updater service also bypasses hello proxy, make a similar change toohello ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="f00b2-131">Essere certi toomake copie dei file originali hello, nel caso in cui è necessario toorevert toohello file con estensione config predefinito.</span><span class="sxs-lookup"><span data-stu-id="f00b2-131">Be sure toomake copies of hello original files, in case you need toorevert toohello default .config files.</span></span>

## <a name="use-hello-outbound-proxy-server"></a><span data-ttu-id="f00b2-132">Utilizza un server proxy in uscita hello</span><span class="sxs-lookup"><span data-stu-id="f00b2-132">Use hello outbound proxy server</span></span>

<span data-ttu-id="f00b2-133">In alcuni ambienti richiedono tutti toogo il traffico in uscita tramite un proxy in uscita, senza eccezione.</span><span class="sxs-lookup"><span data-stu-id="f00b2-133">Some environments require all outbound traffic toogo through an outbound proxy, without exception.</span></span> <span data-ttu-id="f00b2-134">Di conseguenza, ignorando il proxy di hello non è un'opzione.</span><span class="sxs-lookup"><span data-stu-id="f00b2-134">As a result, bypassing hello proxy is not an option.</span></span>

<span data-ttu-id="f00b2-135">È possibile configurare hello connettore traffico toogo tramite proxy in uscita hello, come illustrato nel seguente diagramma hello:</span><span class="sxs-lookup"><span data-stu-id="f00b2-135">You can configure hello connector traffic toogo through hello outbound proxy, as shown in hello following diagram:</span></span>

 ![Configurazione connettore traffico toogo tramite un tooAzure proxy in uscita AD Proxy dell'applicazione](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="f00b2-137">Di conseguenza di ottenere solo il traffico in uscita, non è tooconfigure è necessario l'accesso attraverso i firewall in ingresso.</span><span class="sxs-lookup"><span data-stu-id="f00b2-137">As a result of having only outbound traffic, there's no need tooconfigure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a><span data-ttu-id="f00b2-138">Passaggio 1: Configurare il connettore di hello e relativi servizi toogo tramite proxy in uscita hello</span><span class="sxs-lookup"><span data-stu-id="f00b2-138">Step 1: Configure hello connector and related services toogo through hello outbound proxy</span></span>

<span data-ttu-id="f00b2-139">Come illustrato in precedenza, se WPAD è abilitata nell'ambiente di hello e configurata in modo appropriato, connettore hello rileverà automaticamente i server e tentativo toouse di proxy in uscita di hello è.</span><span class="sxs-lookup"><span data-stu-id="f00b2-139">As covered earlier, if WPAD is enabled in hello environment and configured appropriately, hello connector will automatically discover hello outbound proxy server and attempt toouse it.</span></span> <span data-ttu-id="f00b2-140">Tuttavia, è possibile configurare in modo esplicito hello connettore toogo tramite un proxy in uscita.</span><span class="sxs-lookup"><span data-stu-id="f00b2-140">However, you can explicitly configure hello connector toogo through an outbound proxy.</span></span>

<span data-ttu-id="f00b2-141">toodo in tal caso, modificare il file di C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config hello e aggiungere hello *system.net* sezione illustrata in questo esempio di codice.</span><span class="sxs-lookup"><span data-stu-id="f00b2-141">toodo so, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample.</span></span> <span data-ttu-id="f00b2-142">Modifica *proxyserver:8080* tooreflect il nome del server proxy locale o un indirizzo IP e hello porta che è in ascolto.</span><span class="sxs-lookup"><span data-stu-id="f00b2-142">Change *proxyserver:8080* tooreflect your local proxy server name or IP address, and hello port that it's listening on.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

<span data-ttu-id="f00b2-143">Successivamente, configurare proxy hello toouse del servizio di aggiornamento del connettore hello apportando una modifica toohello di file analoghi si trova in C:\Program Files\Microsoft AAD App Proxy connettore Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span><span class="sxs-lookup"><span data-stu-id="f00b2-143">Next, configure hello Connector Updater service toouse hello proxy by making a similar change toohello file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a><span data-ttu-id="f00b2-144">Passaggio 2: Configurare il traffico di hello proxy tooallow dal connettore hello e i servizi correlati tooflow tramite</span><span class="sxs-lookup"><span data-stu-id="f00b2-144">Step 2: Configure hello proxy tooallow traffic from hello connector and related services tooflow through</span></span>

<span data-ttu-id="f00b2-145">Esistono quattro aspetti tooconsider proxy in uscita hello:</span><span class="sxs-lookup"><span data-stu-id="f00b2-145">There are four aspects tooconsider at hello outbound proxy:</span></span>
* <span data-ttu-id="f00b2-146">Regole in uscita del proxy</span><span class="sxs-lookup"><span data-stu-id="f00b2-146">Proxy outbound rules</span></span>
* <span data-ttu-id="f00b2-147">Autenticazione proxy</span><span class="sxs-lookup"><span data-stu-id="f00b2-147">Proxy authentication</span></span>
* <span data-ttu-id="f00b2-148">Porte proxy</span><span class="sxs-lookup"><span data-stu-id="f00b2-148">Proxy ports</span></span>
* <span data-ttu-id="f00b2-149">Ispezione SSL</span><span class="sxs-lookup"><span data-stu-id="f00b2-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="f00b2-150">Regole in uscita del proxy</span><span class="sxs-lookup"><span data-stu-id="f00b2-150">Proxy outbound rules</span></span>
<span data-ttu-id="f00b2-151">Consenti accesso toohello seguendo gli endpoint per l'accesso al servizio connettore:</span><span class="sxs-lookup"><span data-stu-id="f00b2-151">Allow access toohello following endpoints for connector service access:</span></span>

* <span data-ttu-id="f00b2-152">*.msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="f00b2-152">*.msappproxy.net</span></span>
* <span data-ttu-id="f00b2-153">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="f00b2-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="f00b2-154">Per la registrazione iniziale, Consenti accesso toohello seguenti endpoint:</span><span class="sxs-lookup"><span data-stu-id="f00b2-154">For initial registration, allow access toohello following endpoints:</span></span>

* <span data-ttu-id="f00b2-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="f00b2-155">login.windows.net</span></span>
* <span data-ttu-id="f00b2-156">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="f00b2-156">login.microsoftonline.com</span></span>

<span data-ttu-id="f00b2-157">Se non è possibile consentire la connettività di dominio completo e intervalli IP toospecify invece è necessario, è possibile utilizzare queste opzioni:</span><span class="sxs-lookup"><span data-stu-id="f00b2-157">If you can't allow connectivity by FQDN and need toospecify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="f00b2-158">Consentire l'accesso in uscita di hello connettore tooall destinazioni.</span><span class="sxs-lookup"><span data-stu-id="f00b2-158">Allow hello connector outbound access tooall destinations.</span></span>
* <span data-ttu-id="f00b2-159">Consentire l'accesso in uscita al connettore hello troppo[intervalli IP Data Center di Azure](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="f00b2-159">Allow hello connector outbound access too[Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="f00b2-160">sfida di Hello con elenco hello intervalli IP di Data Center di Azure consiste nel fatto che viene aggiornato ogni settimana.</span><span class="sxs-lookup"><span data-stu-id="f00b2-160">hello challenge with using hello list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="f00b2-161">È necessario tooput un processo in tooensure sul posto che le regole di accesso vengono aggiornate di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="f00b2-161">You need tooput a process in place tooensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="f00b2-162">Autenticazione proxy</span><span class="sxs-lookup"><span data-stu-id="f00b2-162">Proxy authentication</span></span>

<span data-ttu-id="f00b2-163">L'autenticazione proxy non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="f00b2-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="f00b2-164">Il Consiglio corrente è destinazioni di Internet toohello tooallow hello connettore l'accesso anonimo.</span><span class="sxs-lookup"><span data-stu-id="f00b2-164">Our current recommendation is tooallow hello connector anonymous access toohello Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="f00b2-165">Porte proxy</span><span class="sxs-lookup"><span data-stu-id="f00b2-165">Proxy ports</span></span>

<span data-ttu-id="f00b2-166">connettore Hello consente le connessioni in uscita basata su SSL utilizzando il metodo CONNECT hello.</span><span class="sxs-lookup"><span data-stu-id="f00b2-166">hello connector makes outbound SSL-based connections by using hello CONNECT method.</span></span> <span data-ttu-id="f00b2-167">Questo metodo imposta essenzialmente un tunnel tramite proxy in uscita hello.</span><span class="sxs-lookup"><span data-stu-id="f00b2-167">This method essentially sets up a tunnel through hello outbound proxy.</span></span> <span data-ttu-id="f00b2-168">Configurare hello proxy server tooallow tunneling tooports 443 e 80.</span><span class="sxs-lookup"><span data-stu-id="f00b2-168">Configure hello proxy server tooallow tunneling tooports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="f00b2-169">Quando il bus di servizio viene eseguito su HTTPS, usa la porta 443.</span><span class="sxs-lookup"><span data-stu-id="f00b2-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="f00b2-170">Tuttavia, per impostazione predefinita, Bus di servizio vengono tentate connessioni TCP dirette e ritorna tooHTTPS solo se si verifica un errore di connettività diretta.</span><span class="sxs-lookup"><span data-stu-id="f00b2-170">However, by default, Service Bus attempts direct TCP connections and falls back tooHTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="f00b2-171">tooensure hello Bus di servizio, il traffico viene inviato tramite server proxy in uscita hello, verificare che tale connettore hello non può connettersi direttamente toohello servizi di Azure per le porte 9350, 9352 e 5671.</span><span class="sxs-lookup"><span data-stu-id="f00b2-171">tooensure that hello Service Bus traffic is also sent through hello outbound proxy server, ensure that hello connector cannot directly connect toohello Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="f00b2-172">Ispezione SSL</span><span class="sxs-lookup"><span data-stu-id="f00b2-172">SSL inspection</span></span>
<span data-ttu-id="f00b2-173">Non utilizzare ispezione SSL per il traffico di connettore hello, perché causa problemi per il traffico connettore hello.</span><span class="sxs-lookup"><span data-stu-id="f00b2-173">Do not use SSL inspection for hello connector traffic, because it causes problems for hello connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="f00b2-174">Risolvere i problemi relativi al connettore proxy e alla connettività del servizio</span><span class="sxs-lookup"><span data-stu-id="f00b2-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="f00b2-175">A questo punto dovrebbe essere tutto il traffico che passano attraverso il proxy di hello.</span><span class="sxs-lookup"><span data-stu-id="f00b2-175">Now you should see all traffic flowing through hello proxy.</span></span> <span data-ttu-id="f00b2-176">Se si verificano problemi, dovrebbe consentire di hello le seguenti informazioni sulla risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="f00b2-176">If you have problems, hello following troubleshooting information should help.</span></span>

<span data-ttu-id="f00b2-177">Hello tooidentify modo migliore e risolvere i problemi di connettività del connettore problemi è una rete di acquisizione nel servizio del connettore hello durante l'avvio del servizio del connettore hello tootake.</span><span class="sxs-lookup"><span data-stu-id="f00b2-177">hello best way tooidentify and troubleshoot connector connectivity issues is tootake a network capture on hello connector service while starting hello connector service.</span></span> <span data-ttu-id="f00b2-178">Questa può essere un'attività molto complessa, quindi vediamo alcuni semplici suggerimenti sull'acquisizione e il filtraggio delle tracce di rete.</span><span class="sxs-lookup"><span data-stu-id="f00b2-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="f00b2-179">È possibile utilizzare hello monitoraggio dello strumento di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="f00b2-179">You can use hello monitoring tool of your choice.</span></span> <span data-ttu-id="f00b2-180">Ai fini di hello di questo articolo, abbiamo utilizzato Microsoft Network Monitor 3.4.</span><span class="sxs-lookup"><span data-stu-id="f00b2-180">For hello purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="f00b2-181">È possibile [scaricarlo da Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span><span class="sxs-lookup"><span data-stu-id="f00b2-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="f00b2-182">esempi di Hello e i filtri utilizzati in hello le sezioni seguenti sono specifici tooNetwork monitoraggio, ma i principi di hello possono essere applicato tooany lo strumento di analisi.</span><span class="sxs-lookup"><span data-stu-id="f00b2-182">hello examples and filters that we use in hello following sections are specific tooNetwork Monitor, but hello principles can be applied tooany analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="f00b2-183">Eseguire un'acquisizione con Network Monitor</span><span class="sxs-lookup"><span data-stu-id="f00b2-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="f00b2-184">toostart un'acquisizione:</span><span class="sxs-lookup"><span data-stu-id="f00b2-184">toostart a capture:</span></span>

1. <span data-ttu-id="f00b2-185">Aprire Network Monitor e fare clic su **New Capture** (Nuova acquisizione).</span><span class="sxs-lookup"><span data-stu-id="f00b2-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="f00b2-186">Fare clic su hello **avviare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="f00b2-186">Click hello **Start** button.</span></span>

   ![Finestra di Network Monitor](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="f00b2-188">Dopo aver completato un'acquisizione, fare clic su hello **arrestare** tooend pulsante è.</span><span class="sxs-lookup"><span data-stu-id="f00b2-188">After you complete a capture, click hello **Stop** button tooend it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="f00b2-189">Eseguire un'acquisizione del traffico del connettore</span><span class="sxs-lookup"><span data-stu-id="f00b2-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="f00b2-190">Per risolvere il problema iniziale, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f00b2-190">For initial troubleshooting, perform hello following steps:</span></span>

1. <span data-ttu-id="f00b2-191">Da services.msc, arrestare il servizio di Azure Active Directory Application Proxy Connector hello.</span><span class="sxs-lookup"><span data-stu-id="f00b2-191">From services.msc, stop hello Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="f00b2-192">Avviare l'acquisizione di rete hello.</span><span class="sxs-lookup"><span data-stu-id="f00b2-192">Start hello network capture.</span></span>
3. <span data-ttu-id="f00b2-193">Avviare il servizio di Azure Active Directory Application Proxy Connector hello.</span><span class="sxs-lookup"><span data-stu-id="f00b2-193">Start hello Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="f00b2-194">Arrestare l'acquisizione di rete hello.</span><span class="sxs-lookup"><span data-stu-id="f00b2-194">Stop hello network capture.</span></span>

   ![Servizio connettore proxy applicazione di Azure AD in services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a><span data-ttu-id="f00b2-196">Esaminare le richieste di hello dal server proxy di hello connettore toohello</span><span class="sxs-lookup"><span data-stu-id="f00b2-196">Look at hello requests from hello connector toohello proxy server</span></span>

<span data-ttu-id="f00b2-197">Ora che hai un'acquisizione di rete, si è pronti toofilter è.</span><span class="sxs-lookup"><span data-stu-id="f00b2-197">Now that you’ve got a network capture, you're ready toofilter it.</span></span> <span data-ttu-id="f00b2-198">Hello toolooking chiave traccia hello è comprendere in che modo toofilter hello acquisire.</span><span class="sxs-lookup"><span data-stu-id="f00b2-198">hello key toolooking at hello trace is understanding how toofilter hello capture.</span></span>

<span data-ttu-id="f00b2-199">Un filtro è il seguente (dove 8080 è porta del servizio proxy hello):</span><span class="sxs-lookup"><span data-stu-id="f00b2-199">One filter is as follows (where 8080 is hello proxy service port):</span></span>

<span data-ttu-id="f00b2-200">**(http.Request or http.Response) and tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="f00b2-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="f00b2-201">Se si immette questo filtro in hello **filtro di visualizzazione** window e selezionare **applica**, vengono applicati i filtri traffico hello acquisito in base al filtro hello.</span><span class="sxs-lookup"><span data-stu-id="f00b2-201">If you enter this filter in hello **Display Filter** window and select **Apply**, it filters hello captured traffic based on hello filter.</span></span>

<span data-ttu-id="f00b2-202">Hello filtro precedente viene semplicemente hello richieste e risposte HTTP da e verso la porta proxy hello.</span><span class="sxs-lookup"><span data-stu-id="f00b2-202">hello preceding filter shows just hello HTTP requests and responses to/from hello proxy port.</span></span> <span data-ttu-id="f00b2-203">Per l'avvio di un connettore in connettore di hello è toouse configurato un server proxy, il filtro hello mostrerebbe simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f00b2-203">For a connector startup where hello connector is configured toouse a proxy server, hello filter would show something like this:</span></span>

 ![Elenco di esempio di richieste e risposte HTTP filtrate](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="f00b2-205">Ora in modo specifico cercano le richieste di connessione che mostrano la comunicazione con i server proxy hello hello.</span><span class="sxs-lookup"><span data-stu-id="f00b2-205">You're now specifically looking for hello CONNECT requests that show communication with hello proxy server.</span></span> <span data-ttu-id="f00b2-206">Al completamento dell'operazione si ottiene una risposta HTTP affermativa (200).</span><span class="sxs-lookup"><span data-stu-id="f00b2-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="f00b2-207">Se viene visualizzato altri codici di risposta, ad esempio 407 o 502 proxy hello è che richiede l'autenticazione o non consenta il traffico di hello per altri motivi.</span><span class="sxs-lookup"><span data-stu-id="f00b2-207">If you see other response codes, such as 407 or 502, hello proxy is requiring authentication or not allowing hello traffic for some other reason.</span></span> <span data-ttu-id="f00b2-208">A questo punto ci si rivolge al team di supporto del server proxy.</span><span class="sxs-lookup"><span data-stu-id="f00b2-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="f00b2-209">Identificare tentativi di connessione TCP non riusciti</span><span class="sxs-lookup"><span data-stu-id="f00b2-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="f00b2-210">Hello altro scenario comune che potrebbe essere interessati è quando hello connettore tenta tooconnect direttamente, ma non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="f00b2-210">hello other common scenario that you may be interested in is when hello connector is trying tooconnect directly, but it's failing.</span></span>

<span data-ttu-id="f00b2-211">Un altro filtro di monitoraggio della rete che consente di identificare il problema si tooeasily è:</span><span class="sxs-lookup"><span data-stu-id="f00b2-211">Another Network Monitor filter that helps you tooeasily identify this problem is:</span></span>

<span data-ttu-id="f00b2-212">**property.TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="f00b2-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="f00b2-213">Un pacchetto SYN è primo pacchetto hello inviati tooestablish una connessione TCP.</span><span class="sxs-lookup"><span data-stu-id="f00b2-213">A SYN packet is hello first packet sent tooestablish a TCP connection.</span></span> <span data-ttu-id="f00b2-214">Se il pacchetto non restituisce una risposta, è contrassegnandola hello SYN.</span><span class="sxs-lookup"><span data-stu-id="f00b2-214">If this packet doesn’t return a response, hello SYN is reattempted.</span></span> <span data-ttu-id="f00b2-215">Utilizzare qualsiasi SYNs ritrasmessi hello toosee filtro precedente.</span><span class="sxs-lookup"><span data-stu-id="f00b2-215">You can use hello preceding filter toosee any retransmitted SYNs.</span></span> <span data-ttu-id="f00b2-216">Controllare quindi se questi SYNs corrispondono tooany relativi al connettore traffico.</span><span class="sxs-lookup"><span data-stu-id="f00b2-216">Then, you can check whether these SYNs correspond tooany connector-related traffic.</span></span>

<span data-ttu-id="f00b2-217">Hello esempio seguente viene illustrato un tentativo di connessione non riuscita porta Bus tooService 9352:</span><span class="sxs-lookup"><span data-stu-id="f00b2-217">hello following example shows a failed connection attempt tooService Bus port 9352:</span></span>

 ![Risposta di esempio per un tentativo di connessione non riuscito](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="f00b2-219">Se visualizzato qualcosa di simile hello prima risposta, connettore hello sta tentando di toocommunicate direttamente con hello Azure Service Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="f00b2-219">If you see something like hello preceding response, hello connector is trying toocommunicate directly with hello Azure Service Bus service.</span></span> <span data-ttu-id="f00b2-220">Se si prevede di hello connettore toomake connessioni dirette toohello Azure services, questa risposta è una chiara indicazione che si verifica un problema di rete o un firewall.</span><span class="sxs-lookup"><span data-stu-id="f00b2-220">If you expect hello connector toomake direct connections toohello Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="f00b2-221">Se si toouse configurato un server proxy, la risposta potrebbe indicare che il Bus di servizio tenta una connessione diretta TCP prima del passaggio tooattempting una connessione tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f00b2-221">If you are configured toouse a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching tooattempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="f00b2-222">L'analisi delle tracce di rete non è per tutti.</span><span class="sxs-lookup"><span data-stu-id="f00b2-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="f00b2-223">Ma può essere un strumento prezioso tooget rapidamente le informazioni su cosa accade in rete.</span><span class="sxs-lookup"><span data-stu-id="f00b2-223">But it can be a valuable tool tooget quick information about what's going on with your network.</span></span>

<span data-ttu-id="f00b2-224">Se si continua toostruggle con problemi di connettività di connettore, è possibile creare un ticket con il team di supporto.</span><span class="sxs-lookup"><span data-stu-id="f00b2-224">If you continue toostruggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="f00b2-225">il team di Hello consente di semplificare la risoluzione del problema.</span><span class="sxs-lookup"><span data-stu-id="f00b2-225">hello team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="f00b2-226">Per informazioni sulla risoluzione degli errori con il connettore del proxy applicazione, vedere [Risolvere i problemi del proxy applicazione](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="f00b2-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f00b2-227">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f00b2-227">Next steps</span></span>

[<span data-ttu-id="f00b2-228">Comprendere i connettori del proxy applicazione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f00b2-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="f00b2-229">
[Come toosilently installa hello connettore del Proxy dell'applicazione AD Azure](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="f00b2-229">
[How toosilently install hello Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
