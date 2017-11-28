---
title: aaaRed Hat aggiornamento dell'infrastruttura (RHUI) | Documenti Microsoft
description: Informazioni sul servizio Red Hat Update Infrastructure (RHUI) per istanze di Red Hat Enterprise Linux in Microsoft Azure
services: virtual-machines-linux
documentationcenter: 
author: BorisB2015
manager: timlt
editor: 
ms.assetid: f495f1b4-ae24-46b9-8d26-c617ce3daf3a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: borisb
ms.openlocfilehash: cc244857104b25e4e61862c518db77e915e137ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a><span data-ttu-id="ef0e0-103">Red Hat Update Infrastructure (RHUI) per macchine virtuali Red Hat Enterprise Linux su richiesta in Azure</span><span class="sxs-lookup"><span data-stu-id="ef0e0-103">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>
<span data-ttu-id="ef0e0-104">Macchine virtuali create da hello su richiesta Red Hat Enterprise Linux (RHEL) le immagini disponibili in Azure Marketplace sono registrati tooaccess hello Red Hat aggiornamento dell'infrastruttura (RHUI) distribuito in Azure.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-104">Virtual machines created from hello on-demand Red Hat Enterprise Linux (RHEL) images available in Azure Marketplace are registered tooaccess hello Red Hat Update Infrastructure (RHUI) deployed in Azure.</span></span>  <span data-ttu-id="ef0e0-105">le istanze RHEL su richiesta di Hello hanno repository di accesso tooa internazionali yum e gli aggiornamenti incrementali in grado di tooreceive.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-105">hello on-demand RHEL instances have access tooa regional yum repository and able tooreceive incremental updates.</span></span>

<span data-ttu-id="ef0e0-106">elenco di repository yum Hello, che viene gestito da RHUI, è configurato nell'istanza di RHEL durante il provisioning.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-106">hello yum repository list, which is managed by RHUI, is configured in your RHEL instance during provisioning.</span></span> <span data-ttu-id="ef0e0-107">Non è necessario di altre operazioni di configurazione - eseguire toodo `yum update` dopo che l'istanza RHEL è pronto tooget aggiornamenti più recenti di hello.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-107">You don't need toodo any additional configuration - run `yum update` after your RHEL instance is ready tooget hello latest updates.</span></span>

> [!NOTE]
> <span data-ttu-id="ef0e0-108">Settembre 2016 sono stati distribuiti un RHUI Azure aggiornato e in gennaio January 2017 iniziata arresto graduale di hello RHUI meno recente di Azure.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-108">In September 2016 we deployed an updated Azure RHUI and in January 2017 we started phased shutdown of hello older Azure RHUI.</span></span> <span data-ttu-id="ef0e0-109">Se è stato utilizzato immagini RHEL hello (o i relativi snapshot) da settembre 2016 o versione successiva - probabilmente è richiesta alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-109">If you have been using hello RHEL images (or their snapshots) from September 2016 or later - likely no action is required.</span></span> <span data-ttu-id="ef0e0-110">Se, tuttavia, si dispone di istantanee precedente le macchine virtuali, la configurazione deve toobe aggiornati per accesso ininterrotto toohello RHUI di Azure.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-110">If, however, you have older snapshots/VMs, their configuration needs toobe updated for uninterrupted access toohello Azure RHUI.</span></span>
> 

## <a name="rhui-azure-infrastructure-update"></a><span data-ttu-id="ef0e0-111">Aggiornamento dell'infrastruttura RHUI di Azure</span><span class="sxs-lookup"><span data-stu-id="ef0e0-111">RHUI Azure Infrastructure Update</span></span>
<span data-ttu-id="ef0e0-112">A partire da settembre 2016, Azure offre un nuovo set di server RHUI (Red Hat Update Infrastructure).</span><span class="sxs-lookup"><span data-stu-id="ef0e0-112">As of September 2016, Azure has a new set of Red Hat Update Infrastructure (RHUI) servers.</span></span> <span data-ttu-id="ef0e0-113">Questi server vengono distribuiti con [Gestione traffico di Azure](https://azure.microsoft.com/services/traffic-manager/) in modo che un singolo endpoint (rhui-1.micrsoft.com) possa essere usato da qualsiasi VM indipendentemente dall'area.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-113">These servers are deployed with [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) so that a single endpoint (rhui-1.microsoft.com) can be used by any VM regardless of region.</span></span> <span data-ttu-id="ef0e0-114">Hello nuove immagini RHEL pagamento a consumo (PAYG) in hello Azure Marketplace (versioni con data di validità settembre 2016 o versione successive) punto toohello nuovi Azure RHUI server e non richiedono alcuna azione aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-114">hello new RHEL Pay-As-You-Go (PAYG) images in hello Azure Marketplace (versions dated September 2016 or later) point toohello new Azure RHUI servers and do not require any additional action.</span></span>

### <a name="determine-if-action-is-required"></a><span data-ttu-id="ef0e0-115">Determinare se è richiesta qualche azione</span><span class="sxs-lookup"><span data-stu-id="ef0e0-115">Determine if action is required</span></span>
<span data-ttu-id="ef0e0-116">Se si verificano problemi di connessione tooAzure RHUI dalla VM Azure RHEL PAYG, seguire questi passaggi</span><span class="sxs-lookup"><span data-stu-id="ef0e0-116">If you are experiencing problems connecting tooAzure RHUI from your Azure RHEL PAYG VM, follow these steps</span></span>
1. <span data-ttu-id="ef0e0-117">Individuare nella configurazione della VM un endpoint Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="ef0e0-117">Inspect VM configuration for Azure RHUI endpoint</span></span>

    <span data-ttu-id="ef0e0-118">Controllare se `/etc/yum.repos.d/rh-cloud.repo` file contiene i riferimento troppo`rhui-[1-3].microsoft.com` in baseurl di `[rhui-microsoft-azure-rhel*]` sezione del file hello.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-118">Check if `/etc/yum.repos.d/rh-cloud.repo` file contains reference too`rhui-[1-3].microsoft.com` in baseurl of `[rhui-microsoft-azure-rhel*]` section of hello file.</span></span> <span data-ttu-id="ef0e0-119">Se è - si usa hello nuovo RHUI di Azure.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-119">If it is - you are using hello new Azure RHUI.</span></span>

    <span data-ttu-id="ef0e0-120">Se è rivolta tooa percorso con modello di hello `mirrorlist.*cds[1-4].cloudapp.net` -aggiornamento della configurazione hello è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-120">If it pointing tooa location with hello following pattern `mirrorlist.*cds[1-4].cloudapp.net` - hello configuration update is required.</span></span>

    <span data-ttu-id="ef0e0-121">Se si sta utilizzando hello nuova configurazione e non può effettuare la connessione tooAzure RHUI - file di supporto tecnico di Microsoft o Red Hat.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-121">If you are using hello new configuration and still cannot connect tooAzure RHUI - file a support case with Microsoft or Red Hat.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ef0e0-122">Accesso ospitato tooAzure RHUI è limitato toohello macchine virtuali all'interno di [intervalli IP dei data center Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="ef0e0-122">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
    > 

2. <span data-ttu-id="ef0e0-123">Se hello RHUI Azure precedente è ancora disponibile quando si questo controllo e si desidera una configurazione di hello tooautomatically aggiornamento, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ef0e0-123">If hello old Azure RHUI is still available when you do this check and you would like tooautomatically update hello configuration, execute hello following command:</span></span>

    <span data-ttu-id="ef0e0-124">`sudo yum update RHEL6`o `sudo yum update RHEL7` a seconda della versione di hello RHEL famiglia.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-124">`sudo yum update RHEL6` or `sudo yum update RHEL7` depending on hello RHEL family version.</span></span>

3. <span data-ttu-id="ef0e0-125">Se non è possibile connettersi toohello precedente RHUI di Azure, seguire hello manuale i passaggi descritti nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-125">If you can no longer connect toohello old Azure RHUI, follow hello manual steps described in hello next section.</span></span>

4. <span data-ttu-id="ef0e0-126">Assicurarsi che configurazione hello tooupdate hello origine immagine/snapshot interessate VM è stato eseguito il provisioning da.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-126">Make sure tooupdate hello configuration on hello source image/snapshot affected VM was provisioned from.</span></span>

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a><span data-ttu-id="ef0e0-127">Arresto graduale di hello precedente RHUI di Azure</span><span class="sxs-lookup"><span data-stu-id="ef0e0-127">Phased shutdown of hello old Azure RHUI</span></span>
<span data-ttu-id="ef0e0-128">Durante l'arresto di hello di hello precedente RHUI di Azure è limitare l'accesso tooit come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ef0e0-128">During hello shutdown of hello old Azure RHUI we restrict access tooit as follows:</span></span>

1. <span data-ttu-id="ef0e0-129">Consente di limitare ulteriormente l'accesso (ACL) tooset di indirizzi IP che sono già connessi tooit.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-129">Further restrict access (ACL) tooset of IP addresses that are already connecting tooit.</span></span> <span data-ttu-id="ef0e0-130">Possibili effetti collaterali: se si utilizza ancora hello RHUI Azure precedente, le nuove macchine virtuali potrebbero non essere in grado di tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-130">Possible side-effects: if you continue using hello old Azure RHUI - your new VMs may not be able tooconnect tooit.</span></span> <span data-ttu-id="ef0e0-131">RHEL macchine virtuali con gli indirizzi IP dinamici che attraversano la sequenza di arresto/deallocazione/avvio che venga visualizzato di nuovo indirizzo IP e di conseguenza anche Impossibile avviano tooconnect toohello RHUI precedente di Azure</span><span class="sxs-lookup"><span data-stu-id="ef0e0-131">RHEL VMs with dynamic IPs that go through shutdown/deallocate/start sequence may receive new IP and hence also could start failing tooconnect toohello old Azure RHUI</span></span>

2. <span data-ttu-id="ef0e0-132">Arresto del server di distribuzione di contenuti di mirror.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-132">Shutdown of mirror content delivery servers.</span></span> <span data-ttu-id="ef0e0-133">Possibili effetti collaterali: quando è stato chiuso CDSes altre vengono visualizzate più `yum update` ora la manutenzione, un timeout più fino hello punto quando non è possibile connettersi toohello RHUI Azure precedente.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-133">Possible side-effects: as we shut down more CDSes you may see longer `yum update` servicing time, more timeouts up until hello point when you can no longer connect toohello old Azure RHUI.</span></span>

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a><span data-ttu-id="ef0e0-134">Hello gli indirizzi IP per i nuovi server di distribuzione di contenuti RHUI hello sono</span><span class="sxs-lookup"><span data-stu-id="ef0e0-134">hello IPs for hello new RHUI content delivery servers are</span></span>
<span data-ttu-id="ef0e0-135">Se si utilizza toofurther di configurazione di rete da macchine virtuali PAYG RHEL limitare l'accesso, assicurarsi che hello seguenti indirizzi IP consentito per `yum update` toowork a seconda di ambiente hello in.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-135">If you are using network configuration toofurther restrict access from RHEL PAYG VMs, make sure hello following IPs are allowed for `yum update` toowork depending on hello environment you are in.</span></span> 

```
# Azure Global
13.91.47.76
40.85.190.91
52.187.75.218
52.174.163.213

# Azure US Government
13.72.186.193

# Azure Germany
51.5.243.77
51.4.228.145
```

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a><span data-ttu-id="ef0e0-136">Aggiornamento manuale procedure toouse hello nuovi Azure RHUI server</span><span class="sxs-lookup"><span data-stu-id="ef0e0-136">Manual update procedure toouse hello new Azure RHUI servers</span></span>
<span data-ttu-id="ef0e0-137">Firma della chiave pubblica hello download (tramite curl)</span><span class="sxs-lookup"><span data-stu-id="ef0e0-137">Download (via curl) hello public key signature</span></span>

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

<span data-ttu-id="ef0e0-138">Verificare la chiave hello scaricato</span><span class="sxs-lookup"><span data-stu-id="ef0e0-138">Verify hello downloaded key</span></span>

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="ef0e0-139">Controllare l'output di hello, verificare `keyid` e `user ID packet`:</span><span class="sxs-lookup"><span data-stu-id="ef0e0-139">Check hello output, verify `keyid` and `user ID packet`:</span></span>

```bash
Version: GnuPG v1.4.7 (GNU/Linux)
:public key packet:
        version 4, algo 1, created 1446074508, expires 0
        pkey[0]: [2048 bits]
        pkey[1]: [17 bits]
        keyid: EB3E94ADBE1229CF
:user ID packet: "Microsoft (Release signing) <gpgsecurity@microsoft.com>"
:signature packet: algo 1, keyid EB3E94ADBE1229CF
        version 4, created 1446074508, md5len 0, sigclass 0x13
        digest algo 2, begin of digest 1a 9b
        hashed subpkt 2 len 4 (sig created 2015-10-28)
        hashed subpkt 27 len 1 (key flags: 03)
        hashed subpkt 11 len 5 (pref-sym-algos: 9 8 7 3 2)
        hashed subpkt 21 len 3 (pref-hash-algos: 2 8 3)
        hashed subpkt 22 len 2 (pref-zip-algos: 2 1)
        hashed subpkt 30 len 1 (features: 01)
        hashed subpkt 23 len 1 (key server preferences: 80)
        subpkt 16 len 8 (issuer key ID EB3E94ADBE1229CF)
        data: [2047 bits]
```

<span data-ttu-id="ef0e0-140">Installare la chiave pubblica di hello</span><span class="sxs-lookup"><span data-stu-id="ef0e0-140">Install hello public key</span></span>

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="ef0e0-141">Scaricare, verificare e installare l'RPM del client</span><span class="sxs-lookup"><span data-stu-id="ef0e0-141">Download, Verify, and Install Client RPM</span></span>

<span data-ttu-id="ef0e0-142">Scaricare: per RHEL 6</span><span class="sxs-lookup"><span data-stu-id="ef0e0-142">Download: For RHEL 6</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

<span data-ttu-id="ef0e0-143">Per RHEL 7</span><span class="sxs-lookup"><span data-stu-id="ef0e0-143">For RHEL 7</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

<span data-ttu-id="ef0e0-144">Verificare:</span><span class="sxs-lookup"><span data-stu-id="ef0e0-144">Verify:</span></span>

```bash
rpm -Kv azureclient.rpm
```

<span data-ttu-id="ef0e0-145">Verificare nell'output di tale firma di hello pacchetto è OK</span><span class="sxs-lookup"><span data-stu-id="ef0e0-145">Check in output that signature of hello package is OK</span></span>

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

<span data-ttu-id="ef0e0-146">Installare hello RPM</span><span class="sxs-lookup"><span data-stu-id="ef0e0-146">Install hello RPM</span></span>

```bash
sudo rpm -U azureclient.rpm
```

<span data-ttu-id="ef0e0-147">Al termine, verificare che sia possibile accedere hello modulo RHUI Azure VM</span><span class="sxs-lookup"><span data-stu-id="ef0e0-147">Upon completion, verify that you can access Azure RHUI form hello VM</span></span>

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a><span data-ttu-id="ef0e0-148">-Uno script per l'automazione hello precedente attività</span><span class="sxs-lookup"><span data-stu-id="ef0e0-148">All-in-one script for automating hello preceding task</span></span>
<span data-ttu-id="ef0e0-149">Utilizzare lo script seguente come attività hello tooautomate necessari dell'aggiornamento di macchine virtuali toohello nuova RHUI Azure i server interessati hello.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-149">Use hello following script as needed tooautomate hello task of updating affected VMs toohello new Azure RHUI servers.</span></span>

```sh
# Download key
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 

# Validate key
if ! gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release | grep -q "keyid: EB3E94ADBE1229CF"; then
    echo "Keyfile azure.asc NOT valid. Exiting."
    exit 1
fi

# Install Key
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release

# Download RPM package
if grep -q "release 7" /etc/redhat-release; then
    ver=7
elif  grep -q "release 6" /etc/redhat-release; then
    ver=6
else
    echo "Version not supported, exiting"
    exit 1
fi

url=https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel$ver/rhui-azure-rhel$ver-2.0-2.noarch.rpm
curl -o azureclient.rpm "$url"

# Verify package
if ! rpm -Kv azureclient.rpm | grep -q "key ID be1229cf: OK"; then
    echo "RPM failed validation ($url)"
    exit 1
fi

# Install package
sudo rpm -U azureclient.rpm
```

## <a name="rhui-overview"></a><span data-ttu-id="ef0e0-150">Panoramica di RHUI</span><span class="sxs-lookup"><span data-stu-id="ef0e0-150">RHUI overview</span></span>
<span data-ttu-id="ef0e0-151">[Infrastruttura di aggiornamento di Red Hat](https://access.redhat.com/products/red-hat-update-infrastructure) offre un contenuto del repository yum toomanage altamente scalabile per le istanze di cloud Red Hat Enterprise Linux che sono ospitati da provider di cloud Certificate Red Hat.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offers a highly scalable solution toomanage yum repository content for Red Hat Enterprise Linux cloud instances that are hosted by Red Hat-certified cloud providers.</span></span> <span data-ttu-id="ef0e0-152">Basato sul progetto di pasta upstream hello, RHUI consente ai provider di cloud toolocally mirror ospitato Red Hat repository contenuto, creare repository personalizzati con i propri contenuti e apportare tali archivi tooa disponibile ampio gruppo di utenti finali tramite un bilanciamento del carico sistema di recapito del contenuto.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-152">Based on hello upstream Pulp project, RHUI allows cloud providers toolocally mirror Red Hat-hosted repository content, create custom repositories with their own content, and make those repositories available tooa large group of end users through a load-balanced content delivery system.</span></span>

## <a name="regions-where-rhui-is-available"></a><span data-ttu-id="ef0e0-153">Aree in cui viene è disponibile l'infrastruttura RHUI</span><span class="sxs-lookup"><span data-stu-id="ef0e0-153">Regions where RHUI is available</span></span>
<span data-ttu-id="ef0e0-154">Il servizio RHUI è disponibile in tutte le aree in cui sono disponibili le immagini di RHEL su richiesta.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-154">RHUI is available in all regions where RHEL on-demand images are available.</span></span> <span data-ttu-id="ef0e0-155">Pubbliche tutte le regioni elencate in hello attualmente include [dashboard di stato Azure](https://azure.microsoft.com/status/) aree della pagina, Azure del governo e Azure in Germania.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-155">It currently includes all public regions listed on hello [Azure status dashboard](https://azure.microsoft.com/status/) page, Azure US Government and Azure Germany regions.</span></span> <span data-ttu-id="ef0e0-156">L'accesso al servizio RHUI per macchine virtuali sottoposte a provisioning da immagini di RHEL su richiesta è incluso nel rispettivo prezzo.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-156">RHUI access for VMs provisioned from RHEL on-demand images is included in their price.</span></span> <span data-ttu-id="ef0e0-157">Disponibilità cloud internazionali/nazionali aggiuntivi verranno aggiornate di disponibilità su richiesta RHEL in hello future.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-157">Additional regional/national cloud availability will be updated as we expand RHEL on-demand availability in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="ef0e0-158">Accesso ospitato tooAzure RHUI è limitato toohello macchine virtuali all'interno di [intervalli IP dei data center Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="ef0e0-158">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
> 
> 

## <a name="get-updates-from-another-update-repository"></a><span data-ttu-id="ef0e0-159">Ottenere aggiornamenti da un altro repository di aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="ef0e0-159">Get updates from another update repository</span></span>
<span data-ttu-id="ef0e0-160">Se è necessario tooget aggiornamenti da un repository di aggiornamento diversi (anziché RHUI ospitato di Azure), è necessario innanzitutto toounregister le istanze da RHUI.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-160">If you need tooget updates from a different update repository (instead of Azure-hosted RHUI), first you need toounregister your instances from RHUI.</span></span> <span data-ttu-id="ef0e0-161">È necessario toore la registrazione con l'infrastruttura di aggiornamento desiderato hello (ad esempio Red Hat Satellite o Red Hat Customer Portal CDN).</span><span class="sxs-lookup"><span data-stu-id="ef0e0-161">Then you need toore-register them with hello desired update infrastructure (such as Red Hat Satellite or Red Hat Customer Portal CDN).</span></span> <span data-ttu-id="ef0e0-162">Saranno necessarie sottoscrizioni di Red Hat appropriate per questi servizi e una registrazione per il programma [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="ef0e0-162">You will need appropriate Red Hat subscriptions for these services and registration for [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span></span>

<span data-ttu-id="ef0e0-163">toounregister RHUI e registrare di nuovo tooyour infrastruttura di aggiornamento seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="ef0e0-163">toounregister RHUI and reregister tooyour update infrastructure follow these steps:</span></span>

1. <span data-ttu-id="ef0e0-164">Modifica /etc/yum.repos.d/rh-cloud.repo e modificare tutti `enabled=1` troppo`enabled=0`.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-164">Edit /etc/yum.repos.d/rh-cloud.repo and change all `enabled=1` too`enabled=0`.</span></span> <span data-ttu-id="ef0e0-165">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ef0e0-165">For example:</span></span>
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. <span data-ttu-id="ef0e0-166">Modificare /etc/yum/pluginconf.d/rhnplugin.conf e `enabled=0` troppo`enabled=1`.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-166">Edit /etc/yum/pluginconf.d/rhnplugin.conf and change `enabled=0` too`enabled=1`.</span></span>
3. <span data-ttu-id="ef0e0-167">Quindi registrare con l'infrastruttura di hello desiderato, ad esempio Red Hat Customer Portal.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-167">Then register with hello desired infrastructure, such as Red Hat Customer Portal.</span></span> <span data-ttu-id="ef0e0-168">Seguire Red Hat Guida alla soluzione in [come tooregister e sottoscrivere un toohello sistema Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span><span class="sxs-lookup"><span data-stu-id="ef0e0-168">Follow Red Hat solution guide on [how tooregister and subscribe a system toohello Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span></span>

> [!NOTE]
> <span data-ttu-id="ef0e0-169">Accesso toohello RHUI ospitato di Azure è inclusa nel prezzo di immagine di hello RHEL pagamento a consumo (PAYG).</span><span class="sxs-lookup"><span data-stu-id="ef0e0-169">Access toohello Azure-hosted RHUI is included in hello RHEL Pay-As-You-Go (PAYG) image price.</span></span> <span data-ttu-id="ef0e0-170">L'annullamento della registrazione di una macchina virtuale RHEL PAYG da hello RHUI ospitato di Azure non converte macchina virtuale hello in tipo Bring-Your-proprietari-licenza (BYOL) macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-170">Unregistering a PAYG RHEL VM from hello Azure-hosted RHUI does not convert hello virtual machine into Bring-Your-Own-License (BYOL) type VM.</span></span> <span data-ttu-id="ef0e0-171">Se si registra hello stessa macchina virtuale con un'altra origine degli aggiornamenti è possibile gli addebiti di doppi: innanzitutto ora per la tariffa di software RHEL Azure e hello seconda volta per sottoscrizioni di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-171">If you register hello same VM with another source of updates you may be incurring double charges: first time for Azure RHEL software fee, and hello second time for Red Hat subscription(s).</span></span> 
> 
> <span data-ttu-id="ef0e0-172">Se è necessario in modo coerente toouse un'infrastruttura di aggiornamento diversi da RHUI ospitato da Azure considerare la creazione e la distribuzione di immagini (tipo-BYOL) come descritto in [creare e caricare Red Hat basato su macchina virtuale per Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articolo.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-172">If you consistently need toouse an update infrastructure other than Azure-hosted RHUI consider creating and deploying your own (BYOL-type) images as described in [Create and Upload Red Hat-based virtual machine for Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article.</span></span>
> 

## <a name="next-steps"></a><span data-ttu-id="ef0e0-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ef0e0-173">Next steps</span></span>
<span data-ttu-id="ef0e0-174">toocreate una VM di Red Hat Enterprise Linux dall'immagine di Azure Marketplace consumo e sfruttare RHUI ospitato di Azure andare troppo[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span><span class="sxs-lookup"><span data-stu-id="ef0e0-174">toocreate a Red Hat Enterprise Linux VM from Azure Marketplace Pay-As-You-Go image and leverage Azure-hosted RHUI go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span></span> <span data-ttu-id="ef0e0-175">Si sarà in grado di toouse `yum update` nell'istanza di RHEL senza eventuali impostazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="ef0e0-175">You will be able toouse `yum update` in your RHEL instance without any additional setup.</span></span>

