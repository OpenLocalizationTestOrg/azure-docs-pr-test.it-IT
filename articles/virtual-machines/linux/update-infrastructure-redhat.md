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
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a>Red Hat Update Infrastructure (RHUI) per macchine virtuali Red Hat Enterprise Linux su richiesta in Azure
Macchine virtuali create da hello su richiesta Red Hat Enterprise Linux (RHEL) le immagini disponibili in Azure Marketplace sono registrati tooaccess hello Red Hat aggiornamento dell'infrastruttura (RHUI) distribuito in Azure.  le istanze RHEL su richiesta di Hello hanno repository di accesso tooa internazionali yum e gli aggiornamenti incrementali in grado di tooreceive.

elenco di repository yum Hello, che viene gestito da RHUI, è configurato nell'istanza di RHEL durante il provisioning. Non è necessario di altre operazioni di configurazione - eseguire toodo `yum update` dopo che l'istanza RHEL è pronto tooget aggiornamenti più recenti di hello.

> [!NOTE]
> Settembre 2016 sono stati distribuiti un RHUI Azure aggiornato e in gennaio January 2017 iniziata arresto graduale di hello RHUI meno recente di Azure. Se è stato utilizzato immagini RHEL hello (o i relativi snapshot) da settembre 2016 o versione successiva - probabilmente è richiesta alcuna azione. Se, tuttavia, si dispone di istantanee precedente le macchine virtuali, la configurazione deve toobe aggiornati per accesso ininterrotto toohello RHUI di Azure.
> 

## <a name="rhui-azure-infrastructure-update"></a>Aggiornamento dell'infrastruttura RHUI di Azure
A partire da settembre 2016, Azure offre un nuovo set di server RHUI (Red Hat Update Infrastructure). Questi server vengono distribuiti con [Gestione traffico di Azure](https://azure.microsoft.com/services/traffic-manager/) in modo che un singolo endpoint (rhui-1.micrsoft.com) possa essere usato da qualsiasi VM indipendentemente dall'area. Hello nuove immagini RHEL pagamento a consumo (PAYG) in hello Azure Marketplace (versioni con data di validità settembre 2016 o versione successive) punto toohello nuovi Azure RHUI server e non richiedono alcuna azione aggiuntiva.

### <a name="determine-if-action-is-required"></a>Determinare se è richiesta qualche azione
Se si verificano problemi di connessione tooAzure RHUI dalla VM Azure RHEL PAYG, seguire questi passaggi
1. Individuare nella configurazione della VM un endpoint Azure RHUI

    Controllare se `/etc/yum.repos.d/rh-cloud.repo` file contiene i riferimento troppo`rhui-[1-3].microsoft.com` in baseurl di `[rhui-microsoft-azure-rhel*]` sezione del file hello. Se è - si usa hello nuovo RHUI di Azure.

    Se è rivolta tooa percorso con modello di hello `mirrorlist.*cds[1-4].cloudapp.net` -aggiornamento della configurazione hello è obbligatorio.

    Se si sta utilizzando hello nuova configurazione e non può effettuare la connessione tooAzure RHUI - file di supporto tecnico di Microsoft o Red Hat.

    > [!NOTE]
    > Accesso ospitato tooAzure RHUI è limitato toohello macchine virtuali all'interno di [intervalli IP dei data center Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).
    > 

2. Se hello RHUI Azure precedente è ancora disponibile quando si questo controllo e si desidera una configurazione di hello tooautomatically aggiornamento, eseguire hello comando seguente:

    `sudo yum update RHEL6`o `sudo yum update RHEL7` a seconda della versione di hello RHEL famiglia.

3. Se non è possibile connettersi toohello precedente RHUI di Azure, seguire hello manuale i passaggi descritti nella sezione successiva hello.

4. Assicurarsi che configurazione hello tooupdate hello origine immagine/snapshot interessate VM è stato eseguito il provisioning da.

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a>Arresto graduale di hello precedente RHUI di Azure
Durante l'arresto di hello di hello precedente RHUI di Azure è limitare l'accesso tooit come indicato di seguito:

1. Consente di limitare ulteriormente l'accesso (ACL) tooset di indirizzi IP che sono già connessi tooit. Possibili effetti collaterali: se si utilizza ancora hello RHUI Azure precedente, le nuove macchine virtuali potrebbero non essere in grado di tooconnect tooit. RHEL macchine virtuali con gli indirizzi IP dinamici che attraversano la sequenza di arresto/deallocazione/avvio che venga visualizzato di nuovo indirizzo IP e di conseguenza anche Impossibile avviano tooconnect toohello RHUI precedente di Azure

2. Arresto del server di distribuzione di contenuti di mirror. Possibili effetti collaterali: quando è stato chiuso CDSes altre vengono visualizzate più `yum update` ora la manutenzione, un timeout più fino hello punto quando non è possibile connettersi toohello RHUI Azure precedente.

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a>Hello gli indirizzi IP per i nuovi server di distribuzione di contenuti RHUI hello sono
Se si utilizza toofurther di configurazione di rete da macchine virtuali PAYG RHEL limitare l'accesso, assicurarsi che hello seguenti indirizzi IP consentito per `yum update` toowork a seconda di ambiente hello in. 

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

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a>Aggiornamento manuale procedure toouse hello nuovi Azure RHUI server
Firma della chiave pubblica hello download (tramite curl)

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

Verificare la chiave hello scaricato

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

Controllare l'output di hello, verificare `keyid` e `user ID packet`:

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

Installare la chiave pubblica di hello

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

Scaricare, verificare e installare l'RPM del client

Scaricare: per RHEL 6

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

Per RHEL 7

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

Verificare:

```bash
rpm -Kv azureclient.rpm
```

Verificare nell'output di tale firma di hello pacchetto è OK

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

Installare hello RPM

```bash
sudo rpm -U azureclient.rpm
```

Al termine, verificare che sia possibile accedere hello modulo RHUI Azure VM

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a>-Uno script per l'automazione hello precedente attività
Utilizzare lo script seguente come attività hello tooautomate necessari dell'aggiornamento di macchine virtuali toohello nuova RHUI Azure i server interessati hello.

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

## <a name="rhui-overview"></a>Panoramica di RHUI
[Infrastruttura di aggiornamento di Red Hat](https://access.redhat.com/products/red-hat-update-infrastructure) offre un contenuto del repository yum toomanage altamente scalabile per le istanze di cloud Red Hat Enterprise Linux che sono ospitati da provider di cloud Certificate Red Hat. Basato sul progetto di pasta upstream hello, RHUI consente ai provider di cloud toolocally mirror ospitato Red Hat repository contenuto, creare repository personalizzati con i propri contenuti e apportare tali archivi tooa disponibile ampio gruppo di utenti finali tramite un bilanciamento del carico sistema di recapito del contenuto.

## <a name="regions-where-rhui-is-available"></a>Aree in cui viene è disponibile l'infrastruttura RHUI
Il servizio RHUI è disponibile in tutte le aree in cui sono disponibili le immagini di RHEL su richiesta. Pubbliche tutte le regioni elencate in hello attualmente include [dashboard di stato Azure](https://azure.microsoft.com/status/) aree della pagina, Azure del governo e Azure in Germania. L'accesso al servizio RHUI per macchine virtuali sottoposte a provisioning da immagini di RHEL su richiesta è incluso nel rispettivo prezzo. Disponibilità cloud internazionali/nazionali aggiuntivi verranno aggiornate di disponibilità su richiesta RHEL in hello future.

> [!NOTE]
> Accesso ospitato tooAzure RHUI è limitato toohello macchine virtuali all'interno di [intervalli IP dei data center Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).
> 
> 

## <a name="get-updates-from-another-update-repository"></a>Ottenere aggiornamenti da un altro repository di aggiornamenti
Se è necessario tooget aggiornamenti da un repository di aggiornamento diversi (anziché RHUI ospitato di Azure), è necessario innanzitutto toounregister le istanze da RHUI. È necessario toore la registrazione con l'infrastruttura di aggiornamento desiderato hello (ad esempio Red Hat Satellite o Red Hat Customer Portal CDN). Saranno necessarie sottoscrizioni di Red Hat appropriate per questi servizi e una registrazione per il programma [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).

toounregister RHUI e registrare di nuovo tooyour infrastruttura di aggiornamento seguire questi passaggi:

1. Modifica /etc/yum.repos.d/rh-cloud.repo e modificare tutti `enabled=1` troppo`enabled=0`. ad esempio:
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. Modificare /etc/yum/pluginconf.d/rhnplugin.conf e `enabled=0` troppo`enabled=1`.
3. Quindi registrare con l'infrastruttura di hello desiderato, ad esempio Red Hat Customer Portal. Seguire Red Hat Guida alla soluzione in [come tooregister e sottoscrivere un toohello sistema Red Hat Customer Portal](https://access.redhat.com/solutions/253273).

> [!NOTE]
> Accesso toohello RHUI ospitato di Azure è inclusa nel prezzo di immagine di hello RHEL pagamento a consumo (PAYG). L'annullamento della registrazione di una macchina virtuale RHEL PAYG da hello RHUI ospitato di Azure non converte macchina virtuale hello in tipo Bring-Your-proprietari-licenza (BYOL) macchina virtuale. Se si registra hello stessa macchina virtuale con un'altra origine degli aggiornamenti è possibile gli addebiti di doppi: innanzitutto ora per la tariffa di software RHEL Azure e hello seconda volta per sottoscrizioni di Red Hat. 
> 
> Se è necessario in modo coerente toouse un'infrastruttura di aggiornamento diversi da RHUI ospitato da Azure considerare la creazione e la distribuzione di immagini (tipo-BYOL) come descritto in [creare e caricare Red Hat basato su macchina virtuale per Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articolo.
> 

## <a name="next-steps"></a>Passaggi successivi
toocreate una VM di Red Hat Enterprise Linux dall'immagine di Azure Marketplace consumo e sfruttare RHUI ospitato di Azure andare troppo[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/). Si sarà in grado di toouse `yum update` nell'istanza di RHEL senza eventuali impostazioni aggiuntive.

