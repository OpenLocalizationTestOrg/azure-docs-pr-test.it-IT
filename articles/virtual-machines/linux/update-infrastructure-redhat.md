---
title: Red Hat Update Infrastructure (RHUI) | Microsoft Docs
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
ms.openlocfilehash: 07815d691ffe57f0349f7a90ced4a2fcc1ab834f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a><span data-ttu-id="cb64f-103">Red Hat Update Infrastructure (RHUI) per macchine virtuali Red Hat Enterprise Linux su richiesta in Azure</span><span class="sxs-lookup"><span data-stu-id="cb64f-103">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>
<span data-ttu-id="cb64f-104">Le macchine virtuali create dalle immagini di Red Hat Enterprise Linux (RHEL) su richiesta disponibili in Azure Marketplace vengono registrate per accedere al servizio Red Hat Update Infrastructure (RHUI) distribuito in Azure.</span><span class="sxs-lookup"><span data-stu-id="cb64f-104">Virtual machines created from the on-demand Red Hat Enterprise Linux (RHEL) images available in Azure Marketplace are registered to access the Red Hat Update Infrastructure (RHUI) deployed in Azure.</span></span>  <span data-ttu-id="cb64f-105">Le istanze di RHEL su richiesta potranno accedere a repository yum a livello di area e potranno ricevere aggiornamenti incrementali.</span><span class="sxs-lookup"><span data-stu-id="cb64f-105">The on-demand RHEL instances have access to a regional yum repository and able to receive incremental updates.</span></span>

<span data-ttu-id="cb64f-106">L'elenco di repository yum, gestito da RHUI, viene configurato nell'istanza di RHEL durante il provisioning.</span><span class="sxs-lookup"><span data-stu-id="cb64f-106">The yum repository list, which is managed by RHUI, is configured in your RHEL instance during provisioning.</span></span> <span data-ttu-id="cb64f-107">Non è necessario eseguire altre attività di configurazione. Eseguire `yum update` non appena l'istanza di RHEL è pronta per l'installazione degli aggiornamenti più recenti.</span><span class="sxs-lookup"><span data-stu-id="cb64f-107">You don't need to do any additional configuration - run `yum update` after your RHEL instance is ready to get the latest updates.</span></span>

> [!NOTE]
> <span data-ttu-id="cb64f-108">In settembre 2016 è stata distribuita l'infrastruttura RHUI di Azure aggiornata e in gennaio 2017 è stato avviato l'arresto graduale della precedente.</span><span class="sxs-lookup"><span data-stu-id="cb64f-108">In September 2016 we deployed an updated Azure RHUI and in January 2017 we started phased shutdown of the older Azure RHUI.</span></span> <span data-ttu-id="cb64f-109">Se si usano immagini RHEL (o i relativi snapshot) da settembre 2016 o da un momento successivo probabilmente non è richiesta alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="cb64f-109">If you have been using the RHEL images (or their snapshots) from September 2016 or later - likely no action is required.</span></span> <span data-ttu-id="cb64f-110">Se invece si dispone di snapshot/VM precedenti, la loro configurazione deve essere aggiornata per l'accesso ininterrotto all'infrastruttura RHUI di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb64f-110">If, however, you have older snapshots/VMs, their configuration needs to be updated for uninterrupted access to the Azure RHUI.</span></span>
> 

## <a name="rhui-azure-infrastructure-update"></a><span data-ttu-id="cb64f-111">Aggiornamento dell'infrastruttura RHUI di Azure</span><span class="sxs-lookup"><span data-stu-id="cb64f-111">RHUI Azure Infrastructure Update</span></span>
<span data-ttu-id="cb64f-112">A partire da settembre 2016, Azure offre un nuovo set di server RHUI (Red Hat Update Infrastructure).</span><span class="sxs-lookup"><span data-stu-id="cb64f-112">As of September 2016, Azure has a new set of Red Hat Update Infrastructure (RHUI) servers.</span></span> <span data-ttu-id="cb64f-113">Questi server vengono distribuiti con [Gestione traffico di Azure](https://azure.microsoft.com/services/traffic-manager/) in modo che un singolo endpoint (rhui-1.micrsoft.com) possa essere usato da qualsiasi VM indipendentemente dall'area.</span><span class="sxs-lookup"><span data-stu-id="cb64f-113">These servers are deployed with [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) so that a single endpoint (rhui-1.microsoft.com) can be used by any VM regardless of region.</span></span> <span data-ttu-id="cb64f-114">Le nuove immagini RHEL Pay-As-You-Go (PAYG) con pagamento in base al consumo in Azure Marketplace (versioni di settembre 2016 o successive) puntano ai nuovi server RHUI di Azure senza richiedere altre operazioni.</span><span class="sxs-lookup"><span data-stu-id="cb64f-114">The new RHEL Pay-As-You-Go (PAYG) images in the Azure Marketplace (versions dated September 2016 or later) point to the new Azure RHUI servers and do not require any additional action.</span></span>

### <a name="determine-if-action-is-required"></a><span data-ttu-id="cb64f-115">Determinare se è richiesta qualche azione</span><span class="sxs-lookup"><span data-stu-id="cb64f-115">Determine if action is required</span></span>
<span data-ttu-id="cb64f-116">Se si verificano problemi di connessione all'infrastruttura RHUI di Azure da una VM con pagamento in base al consumo di Azure RHEL, seguire questi passaggi</span><span class="sxs-lookup"><span data-stu-id="cb64f-116">If you are experiencing problems connecting to Azure RHUI from your Azure RHEL PAYG VM, follow these steps</span></span>
1. <span data-ttu-id="cb64f-117">Individuare nella configurazione della VM un endpoint Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="cb64f-117">Inspect VM configuration for Azure RHUI endpoint</span></span>

    <span data-ttu-id="cb64f-118">Controllare se il file `/etc/yum.repos.d/rh-cloud.repo` contiene riferimenti a `rhui-[1-3].microsoft.com` nel baseurl della sezione `[rhui-microsoft-azure-rhel*]` del file.</span><span class="sxs-lookup"><span data-stu-id="cb64f-118">Check if `/etc/yum.repos.d/rh-cloud.repo` file contains reference to `rhui-[1-3].microsoft.com` in baseurl of `[rhui-microsoft-azure-rhel*]` section of the file.</span></span> <span data-ttu-id="cb64f-119">In questo caso è in uso la nuova infrastruttura RHUI di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb64f-119">If it is - you are using the new Azure RHUI.</span></span>

    <span data-ttu-id="cb64f-120">Se punta un percorso con il modello `mirrorlist.*cds[1-4].cloudapp.net`, è necessario l'aggiornamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="cb64f-120">If it pointing to a location with the following pattern `mirrorlist.*cds[1-4].cloudapp.net` - the configuration update is required.</span></span>

    <span data-ttu-id="cb64f-121">Se è in uso la nuova configurazione ma non è possibile connettersi all'infrastruttura RHUI di Azure, rivolgersi al servizio di supporto di Microsoft o di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="cb64f-121">If you are using the new configuration and still cannot connect to Azure RHUI - file a support case with Microsoft or Red Hat.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cb64f-122">L'accesso all'istanza di RHUI ospitata in Azure è limitato alle macchine virtuali comprese negli [intervalli di indirizzi IP dei data center di Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="cb64f-122">Access to Azure-hosted RHUI is limited to the VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
    > 

2. <span data-ttu-id="cb64f-123">Se la vecchia infrastruttura RHUI di Azure è ancora disponibile quando si eseguire questo controllo e si desidera aggiornare automaticamente la configurazione, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cb64f-123">If the old Azure RHUI is still available when you do this check and you would like to automatically update the configuration, execute the following command:</span></span>

    <span data-ttu-id="cb64f-124">`sudo yum update RHEL6`o `sudo yum update RHEL7` a seconda della versione della famiglia RHEL.</span><span class="sxs-lookup"><span data-stu-id="cb64f-124">`sudo yum update RHEL6` or `sudo yum update RHEL7` depending on the RHEL family version.</span></span>

3. <span data-ttu-id="cb64f-125">Se non è più possibile connettersi alla vecchia infrastruttura RHUI di Azure, seguire i passaggi manuali descritti nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="cb64f-125">If you can no longer connect to the old Azure RHUI, follow the manual steps described in the next section.</span></span>

4. <span data-ttu-id="cb64f-126">Assicurarsi di aggiornare la configurazione sull'immagine/snapshot sorgente da cui è stato eseguito il provisioning della VM interessata.</span><span class="sxs-lookup"><span data-stu-id="cb64f-126">Make sure to update the configuration on the source image/snapshot affected VM was provisioned from.</span></span>

### <a name="phased-shutdown-of-the-old-azure-rhui"></a><span data-ttu-id="cb64f-127">Arresto graduale della precedente infrastruttura RHUI di Azure</span><span class="sxs-lookup"><span data-stu-id="cb64f-127">Phased shutdown of the old Azure RHUI</span></span>
<span data-ttu-id="cb64f-128">Durante l'arresto della precedente infrastruttura RHUI di Azure, l'accesso all'infrastruttura stessa è limitato come segue:</span><span class="sxs-lookup"><span data-stu-id="cb64f-128">During the shutdown of the old Azure RHUI we restrict access to it as follows:</span></span>

1. <span data-ttu-id="cb64f-129">Accesso ulteriormente limitato (elenco di controllo di accesso) al gruppo di indirizzi IP già connessi.</span><span class="sxs-lookup"><span data-stu-id="cb64f-129">Further restrict access (ACL) to set of IP addresses that are already connecting to it.</span></span> <span data-ttu-id="cb64f-130">Possibili effetti collaterali: se si continua a usare la precedente infrastruttura RHUI di Azure, le nuove VM potrebbero non riuscire a connettersi a essa.</span><span class="sxs-lookup"><span data-stu-id="cb64f-130">Possible side-effects: if you continue using the old Azure RHUI - your new VMs may not be able to connect to it.</span></span> <span data-ttu-id="cb64f-131">Le VM RHEL con indirizzi IP dinamici che passano attraverso la sequenza di arresto/deallocazione/avvio possono ricevere un nuovo IP e pertanto potrebbero iniziare a non riuscire a connettersi alla precedente infrastruttura RHUI di Azure</span><span class="sxs-lookup"><span data-stu-id="cb64f-131">RHEL VMs with dynamic IPs that go through shutdown/deallocate/start sequence may receive new IP and hence also could start failing to connect to the old Azure RHUI</span></span>

2. <span data-ttu-id="cb64f-132">Arresto del server di distribuzione di contenuti di mirror.</span><span class="sxs-lookup"><span data-stu-id="cb64f-132">Shutdown of mirror content delivery servers.</span></span> <span data-ttu-id="cb64f-133">Possibili effetti collaterali: poiché sono stati arrestati altri CDSes, potrebbe essere necessario più tempo per la manutenzione di `yum update` e potrebbero verificarsi più timeout fino a quando non sarà più possibile connettersi alla vecchia infrastruttura RHUI di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb64f-133">Possible side-effects: as we shut down more CDSes you may see longer `yum update` servicing time, more timeouts up until the point when you can no longer connect to the old Azure RHUI.</span></span>

### <a name="the-ips-for-the-new-rhui-content-delivery-servers-are"></a><span data-ttu-id="cb64f-134">Gli indirizzi IP per i nuovi server di distribuzione di contenuti RHUI sono</span><span class="sxs-lookup"><span data-stu-id="cb64f-134">The IPs for the new RHUI content delivery servers are</span></span>
<span data-ttu-id="cb64f-135">Se si usa la configurazione di rete per limitare ulteriormente l'accesso dalle VM RHEL con pagamento in base al consumo, assicurarsi che siano consentiti i seguenti IP per il funzionamento di `yum update` a seconda dell'ambiente in cui ci si trova.</span><span class="sxs-lookup"><span data-stu-id="cb64f-135">If you are using network configuration to further restrict access from RHEL PAYG VMs, make sure the following IPs are allowed for `yum update` to work depending on the environment you are in.</span></span> 

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

### <a name="manual-update-procedure-to-use-the-new-azure-rhui-servers"></a><span data-ttu-id="cb64f-136">Procedura di aggiornamento manuale per l'uso dei nuovi server RHUI di Azure</span><span class="sxs-lookup"><span data-stu-id="cb64f-136">Manual update procedure to use the new Azure RHUI servers</span></span>
<span data-ttu-id="cb64f-137">Scaricare (tramite curl) la firma con chiave pubblica</span><span class="sxs-lookup"><span data-stu-id="cb64f-137">Download (via curl) the public key signature</span></span>

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

<span data-ttu-id="cb64f-138">Verificare la chiave scaricata</span><span class="sxs-lookup"><span data-stu-id="cb64f-138">Verify the downloaded key</span></span>

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="cb64f-139">Controllare l'output, verificare `keyid` e `user ID packet`:</span><span class="sxs-lookup"><span data-stu-id="cb64f-139">Check the output, verify `keyid` and `user ID packet`:</span></span>

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

<span data-ttu-id="cb64f-140">Installare la chiave pubblica</span><span class="sxs-lookup"><span data-stu-id="cb64f-140">Install the public key</span></span>

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="cb64f-141">Scaricare, verificare e installare l'RPM del client</span><span class="sxs-lookup"><span data-stu-id="cb64f-141">Download, Verify, and Install Client RPM</span></span>

<span data-ttu-id="cb64f-142">Scaricare: per RHEL 6</span><span class="sxs-lookup"><span data-stu-id="cb64f-142">Download: For RHEL 6</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

<span data-ttu-id="cb64f-143">Per RHEL 7</span><span class="sxs-lookup"><span data-stu-id="cb64f-143">For RHEL 7</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

<span data-ttu-id="cb64f-144">Verificare:</span><span class="sxs-lookup"><span data-stu-id="cb64f-144">Verify:</span></span>

```bash
rpm -Kv azureclient.rpm
```

<span data-ttu-id="cb64f-145">Controllare nell'output che la firma del pacchetto sia corretta</span><span class="sxs-lookup"><span data-stu-id="cb64f-145">Check in output that signature of the package is OK</span></span>

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

<span data-ttu-id="cb64f-146">Installare l'RPM</span><span class="sxs-lookup"><span data-stu-id="cb64f-146">Install the RPM</span></span>

```bash
sudo rpm -U azureclient.rpm
```

<span data-ttu-id="cb64f-147">Al termine, verificare che sia possibile accedere all'infrastruttura RHUI di Azure dalla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="cb64f-147">Upon completion, verify that you can access Azure RHUI form the VM</span></span>

### <a name="all-in-one-script-for-automating-the-preceding-task"></a><span data-ttu-id="cb64f-148">Script all-in-one per automatizzare l'attività precedente</span><span class="sxs-lookup"><span data-stu-id="cb64f-148">All-in-one script for automating the preceding task</span></span>
<span data-ttu-id="cb64f-149">Usare lo script seguente, in base alle proprie esigenze, per automatizzare l'attività di aggiornamento delle macchine virtuali interessate ai nuovi server RHUI di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb64f-149">Use the following script as needed to automate the task of updating affected VMs to the new Azure RHUI servers.</span></span>

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

## <a name="rhui-overview"></a><span data-ttu-id="cb64f-150">Panoramica di RHUI</span><span class="sxs-lookup"><span data-stu-id="cb64f-150">RHUI overview</span></span>
<span data-ttu-id="cb64f-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offre una soluzione altamente scalabile per gestire il contenuto del repository yum per le istanze cloud di Red Hat Enterprise Linux ospitate dai provider cloud certificati da Red Hat.</span><span class="sxs-lookup"><span data-stu-id="cb64f-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offers a highly scalable solution to manage yum repository content for Red Hat Enterprise Linux cloud instances that are hosted by Red Hat-certified cloud providers.</span></span> <span data-ttu-id="cb64f-152">In base al progetto Pulp upstream, RHUI consente ai provider cloud di eseguire il mirroring locale del contenuto del repository ospitato da Red Hat e creare repository personalizzati con il proprio contenuto e rendere disponibili tali repository per un ampio gruppo di utenti finali tramite un sistema di distribuzione del contenuto con bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="cb64f-152">Based on the upstream Pulp project, RHUI allows cloud providers to locally mirror Red Hat-hosted repository content, create custom repositories with their own content, and make those repositories available to a large group of end users through a load-balanced content delivery system.</span></span>

## <a name="regions-where-rhui-is-available"></a><span data-ttu-id="cb64f-153">Aree in cui viene è disponibile l'infrastruttura RHUI</span><span class="sxs-lookup"><span data-stu-id="cb64f-153">Regions where RHUI is available</span></span>
<span data-ttu-id="cb64f-154">Il servizio RHUI è disponibile in tutte le aree in cui sono disponibili le immagini di RHEL su richiesta.</span><span class="sxs-lookup"><span data-stu-id="cb64f-154">RHUI is available in all regions where RHEL on-demand images are available.</span></span> <span data-ttu-id="cb64f-155">Include attualmente tutte le aree pubbliche elencate nella pagina del [dashboard di stato di Azure](https://azure.microsoft.com/status/), le aree di Azure per il governo degli Stati Uniti e le aree di Azure per la Germania.</span><span class="sxs-lookup"><span data-stu-id="cb64f-155">It currently includes all public regions listed on the [Azure status dashboard](https://azure.microsoft.com/status/) page, Azure US Government and Azure Germany regions.</span></span> <span data-ttu-id="cb64f-156">L'accesso al servizio RHUI per macchine virtuali sottoposte a provisioning da immagini di RHEL su richiesta è incluso nel rispettivo prezzo.</span><span class="sxs-lookup"><span data-stu-id="cb64f-156">RHUI access for VMs provisioned from RHEL on-demand images is included in their price.</span></span> <span data-ttu-id="cb64f-157">La disponibilità di cloud locale/nazionale verrà aggiornata in base all'espansione della disponibilità di RHEL su richiesta in futuro.</span><span class="sxs-lookup"><span data-stu-id="cb64f-157">Additional regional/national cloud availability will be updated as we expand RHEL on-demand availability in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="cb64f-158">L'accesso all'istanza di RHUI ospitata in Azure è limitato alle macchine virtuali comprese negli [intervalli di indirizzi IP dei data center di Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="cb64f-158">Access to Azure-hosted RHUI is limited to the VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
> 
> 

## <a name="get-updates-from-another-update-repository"></a><span data-ttu-id="cb64f-159">Ottenere aggiornamenti da un altro repository di aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="cb64f-159">Get updates from another update repository</span></span>
<span data-ttu-id="cb64f-160">Se è necessario ottenere gli aggiornamenti da un repository di aggiornamento diverso (anziché da un'infrastruttura RHUI ospitata in Azure), prima è necessario annullare la registrazione delle istanze dall'infrastruttura RHUI.</span><span class="sxs-lookup"><span data-stu-id="cb64f-160">If you need to get updates from a different update repository (instead of Azure-hosted RHUI), first you need to unregister your instances from RHUI.</span></span> <span data-ttu-id="cb64f-161">Quindi è necessario registrarle nuovamente con l'infrastruttura di aggiornamento desiderata (ad esempio Red Hat Satellite o la rete CDN Red Hat Customer Portal).</span><span class="sxs-lookup"><span data-stu-id="cb64f-161">Then you need to re-register them with the desired update infrastructure (such as Red Hat Satellite or Red Hat Customer Portal CDN).</span></span> <span data-ttu-id="cb64f-162">Saranno necessarie sottoscrizioni di Red Hat appropriate per questi servizi e una registrazione per il programma [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="cb64f-162">You will need appropriate Red Hat subscriptions for these services and registration for [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span></span>

<span data-ttu-id="cb64f-163">Per annullare la registrazione all'infrastruttura RHUI e registrarsi all'infrastruttura di aggiornamento desiderata, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="cb64f-163">To unregister RHUI and reregister to your update infrastructure follow these steps:</span></span>

1. <span data-ttu-id="cb64f-164">Modificare /etc/yum.repos.d/rh-cloud.repo e sostituire tutte le occorrenze di `enabled=1` con `enabled=0`.</span><span class="sxs-lookup"><span data-stu-id="cb64f-164">Edit /etc/yum.repos.d/rh-cloud.repo and change all `enabled=1` to `enabled=0`.</span></span> <span data-ttu-id="cb64f-165">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="cb64f-165">For example:</span></span>
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. <span data-ttu-id="cb64f-166">Modificare /etc/yum/pluginconf.d/rhnplugin.conf e sostituire tutte le occorrenze di `enabled=0` con `enabled=1`.</span><span class="sxs-lookup"><span data-stu-id="cb64f-166">Edit /etc/yum/pluginconf.d/rhnplugin.conf and change `enabled=0` to `enabled=1`.</span></span>
3. <span data-ttu-id="cb64f-167">Eseguire quindi la registrazione all'infrastruttura desiderata, ad esempio il portale dei clienti di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="cb64f-167">Then register with the desired infrastructure, such as Red Hat Customer Portal.</span></span> <span data-ttu-id="cb64f-168">Per informazioni su come [eseguire la registrazione e la sottoscrizione di un sistema nel portale dei clienti di Red Hat](https://access.redhat.com/solutions/253273), vedere la guida della soluzione Red Hat.</span><span class="sxs-lookup"><span data-stu-id="cb64f-168">Follow Red Hat solution guide on [how to register and subscribe a system to the Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span></span>

> [!NOTE]
> <span data-ttu-id="cb64f-169">L'accesso al servizio RHUI ospitato in Azure è incluso nel prezzo dell'immagine di RHEL con pagamento in base al consumo.</span><span class="sxs-lookup"><span data-stu-id="cb64f-169">Access to the Azure-hosted RHUI is included in the RHEL Pay-As-You-Go (PAYG) image price.</span></span> <span data-ttu-id="cb64f-170">Annullando la registrazione di una VM RHEL con pagamento in base al consumo dall'infrastruttura RHUI ospitata in Azure non si converte la VM nel tipo BYOL (Bring-Your-Own-License).</span><span class="sxs-lookup"><span data-stu-id="cb64f-170">Unregistering a PAYG RHEL VM from the Azure-hosted RHUI does not convert the virtual machine into Bring-Your-Own-License (BYOL) type VM.</span></span> <span data-ttu-id="cb64f-171">Se si registra la stessa VM con un'altra origine di aggiornamenti si potrebbe incorrere in addebiti doppi: la prima volta per la tariffa del software Azure RHEL e la seconda volta per le sottoscrizioni di Red Hat.</span><span class="sxs-lookup"><span data-stu-id="cb64f-171">If you register the same VM with another source of updates you may be incurring double charges: first time for Azure RHEL software fee, and the second time for Red Hat subscription(s).</span></span> 
> 
> <span data-ttu-id="cb64f-172">Se è necessario usare in modo continuativo un'infrastruttura di aggiornamento diversa dall'infrastruttura RHUI ospitata in Azure, prendere in considerazione la creazione e la distribuzione di immagini personalizzate di tipo BYOL, come descritto nell'articolo [Preparare una macchina virtuale basata su RedHat per Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="cb64f-172">If you consistently need to use an update infrastructure other than Azure-hosted RHUI consider creating and deploying your own (BYOL-type) images as described in [Create and Upload Red Hat-based virtual machine for Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article.</span></span>
> 

## <a name="next-steps"></a><span data-ttu-id="cb64f-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cb64f-173">Next steps</span></span>
<span data-ttu-id="cb64f-174">Per creare una macchina virtuale Red Hat Enterprise Linux dall'immagine con pagamento in base al consumo di Azure Marketplace e sfruttare i vantaggi dell'infrastruttura RHUI ospitata in Azure, passare ad [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span><span class="sxs-lookup"><span data-stu-id="cb64f-174">To create a Red Hat Enterprise Linux VM from Azure Marketplace Pay-As-You-Go image and leverage Azure-hosted RHUI go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span></span> <span data-ttu-id="cb64f-175">Sarà possibile usare `yum update` nell'istanza di RHEL senza impostazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="cb64f-175">You will be able to use `yum update` in your RHEL instance without any additional setup.</span></span>

