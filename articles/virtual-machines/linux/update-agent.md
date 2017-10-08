---
title: hello aaaUpdate agente Linux di Azure da GitHub | Documenti Microsoft
description: "Informazioni su come tooupdate agente Linux di Azure per le VM Linux nella versione più recente di Azure toohello da GitHub"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: f1f19300-987d-4f29-9393-9aba866f049c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: mingzhan
ms.openlocfilehash: 4ce7c56efc1e6563e6415f7687573f9fb9e7b4c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a>Come tooupdate hello agente Linux di Azure in una macchina virtuale

tooupdate il [agente Linux di Azure](https://github.com/Azure/WALinuxAgent) in una VM Linux in Azure, è necessario disporre di:

- Una VM Linux in esecuzione in Azure.
- Una VM Linux di toothat connessione con SSH.

È sempre consigliabile ricercare innanzitutto un pacchetto nel repository di distribuzione di Linux hello. È possibile pacchetto hello disponibile potrebbero non essere la versione più recente di hello, tuttavia, l'abilitazione degli aggiornamenti automatici garantisce hello agente Linux otterranno sempre l'aggiornamento più recente di hello. Si devono avere problemi di installazione da gestori di pacchetti hello, è consigliabile rivolgersi supporto dal fornitore distro hello.

## <a name="updating-hello-azure-linux-agent"></a>Aggiornamento hello agente Linux di Azure

## <a name="ubuntu"></a>Ubuntu

#### <a name="check-your-current-package-version"></a>Verificare la versione corrente del pacchetto

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>Aggiornare la cache del pacchetto

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Installare una versione più recente del pacchetto hello

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a>Verificare che la funzione di aggiornamento automatico sia abilitata

Se è abilitato, verificare innanzitutto toosee:

```bash
cat /etc/waagent.conf
```

Trovare "AutoUpdate.Enabled". Se viene visualizzato questo output, la funzione è abilitata:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable eseguire:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Riavviare il servizio di waagent hello

#### <a name="restart-agent-for-1404"></a>Riavviare l'agente per 14.04

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a>Riavviare l'agente per 16.04 / 17.04

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a>Debian

### <a name="debian-7-wheezy"></a>Debian 7 "Wheezy"

#### <a name="check-your-current-package-version"></a>Verificare la versione corrente del pacchetto

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a>Aggiornare la cache del pacchetto

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Installare una versione più recente del pacchetto hello

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a>Abilitare l'aggiornamento automatico dell'agente
Per questa versione di Debian, che non ha una versione > = 2.0.16, la funzione di aggiornamento automatico non è disponibile. output di Hello dalla hello sopra comando illustra se il pacchetto di hello è aggiornato.

### <a name="debian-8-jessie--debian-9-stretch"></a>Debian 8 "Jessie" / Debian 9 "Stretch"

#### <a name="check-your-current-package-version"></a>Verificare la versione corrente del pacchetto

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>Aggiornare la cache del pacchetto

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Installare una versione più recente del pacchetto hello

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a>Verificare che la funzione di aggiornamento automatico sia abilitata 

Se è abilitato, verificare innanzitutto toosee:

```bash
cat /etc/waagent.conf
```

Trovare "AutoUpdate.Enabled". Se viene visualizzato questo output, la funzione è abilitata:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable eseguire:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Riavviare il servizio di waagent hello

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a>Redhat / CentOS

### <a name="rhelcentos-6"></a>RHEL/CentOS 6

#### <a name="check-your-current-package-version"></a>Verificare la versione corrente del pacchetto

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>Verificare gli aggiornamenti disponibili

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>Installare una versione più recente del pacchetto hello

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a>Verificare che la funzione di aggiornamento automatico sia abilitata 

Se è abilitato, verificare innanzitutto toosee:

```bash
cat /etc/waagent.conf
```

Trovare "AutoUpdate.Enabled". Se viene visualizzato questo output, la funzione è abilitata:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable eseguire:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Riavviare il servizio di waagent hello

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a>RHEL/CentOS 7

#### <a name="check-your-current-package-version"></a>Verificare la versione corrente del pacchetto

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>Verificare gli aggiornamenti disponibili

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>Installare una versione più recente del pacchetto hello

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a>Verificare che la funzione di aggiornamento automatico sia abilitata 

Se è abilitato, verificare innanzitutto toosee:

```bash
cat /etc/waagent.conf
```

Trovare "AutoUpdate.Enabled". Se viene visualizzato questo output, la funzione è abilitata:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable eseguire:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Riavviare il servizio di waagent hello

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a>SUSE SLES

### <a name="suse-sles-11-sp4"></a>SUSE SLES 11 SP4

#### <a name="check-your-current-package-version"></a>Verificare la versione corrente del pacchetto

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>Verificare gli aggiornamenti disponibili

Hello sopra l'output viene visualizzato è se il pacchetto di hello backup toodate.

#### <a name="install-hello-latest-package-version"></a>Installare una versione più recente del pacchetto hello

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>Verificare che la funzione di aggiornamento automatico sia abilitata 

Se è abilitato, verificare innanzitutto toosee:

```bash
cat /etc/waagent.conf
```

Trovare "AutoUpdate.Enabled". Se viene visualizzato questo output, la funzione è abilitata:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable eseguire:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Riavviare il servizio di waagent hello

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a>SUSE SLES 12 SP2

#### <a name="check-your-current-package-version"></a>Verificare la versione corrente del pacchetto

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>Verificare gli aggiornamenti disponibili

Nell'output di hello da hello precedente, verranno visualizzati è se il pacchetto di hello è aggiornata.

#### <a name="install-hello-latest-package-version"></a>Installare una versione più recente del pacchetto hello

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>Verificare che la funzione di aggiornamento automatico sia abilitata 

Se è abilitato, verificare innanzitutto toosee:

```bash
cat /etc/waagent.conf
```

Trovare "AutoUpdate.Enabled". Se viene visualizzato questo output, la funzione è abilitata:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable eseguire:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Riavviare il servizio di waagent hello

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a>Oracle 6 e 7

Per Oracle Linux, assicurarsi che tale hello `Addons` repository è abilitato. Scegliere file hello tooedit `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) o `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux) e modificare la riga hello `enabled=0` troppo`enabled=1` in **[ol6_addons]** o **[ol7_addons]** In questo file.

Quindi, tooinstall hello versione più recente di hello agente Linux di Azure, tipo:

```bash
sudo yum install WALinuxAgent
```

Se non si trova il repository di componente aggiuntivo hello è semplicemente possibile aggiungere queste righe alla fine del file .repo in base a versione Oracle Linux tooyour hello:

Per macchine virtuali Oracle Linux 6:

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

Per macchine virtuali Oracle Linux 7:

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

Quindi digitare:

```bash
sudo yum update WALinuxAgent
```

In genere è sufficiente, ma se per qualche motivo, che è necessario tooinstall da https://github.com direttamente, utilizzare hello seguendo i passaggi.


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a>Aggiornare l'agente Linux di hello quando è presente alcun pacchetto dell'agente per la distribuzione

Installare wget (sono disponibili alcune distribuzioni che non installano per impostazione predefinita, ad esempio Oracle Linux, in CentOS e Red Hat versioni 6.4 e 6.5) digitando `sudo yum install wget` nella riga di comando hello.

### <a name="1-download-hello-latest-version"></a>1. Scaricare la versione più recente di hello
Aprire [hello versione dell'agente Linux di Azure in GitHub](https://github.com/Azure/WALinuxAgent/releases) in una pagina web e individuare il numero di versione più recente hello. (È possibile individuare la versione corrente digitando `waagent --version`.)

#### <a name="for-version-22x-or-later-type"></a>Per la versione 2.2.x o successiva, digitare:
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

Hello riga seguente usa versione 2.2.0 ad esempio:

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a>2. Installare hello agente Linux di Azure

#### <a name="for-version-22x-use"></a>Per la versione 2.2.x, usare:
Potrebbe essere necessario pacchetto hello tooinstall `setuptools` prima - [qui](https://pypi.python.org/pypi/setuptools). Quindi eseguire:

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a>Verificare che la funzione di aggiornamento automatico sia abilitata

Se è abilitato, verificare innanzitutto toosee:

```bash
cat /etc/waagent.conf
```

Trovare "AutoUpdate.Enabled". Se viene visualizzato questo output, la funzione è abilitata:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable eseguire:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a>3. Riavviare il servizio di waagent hello
Per la maggior parte delle distribuzioni Linux:

```bash
sudo service waagent restart
```

Per Ubuntu, utilizzare:

```bash
sudo service walinuxagent restart
```

Per CoreOS, usare:

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a>4. Verificare hello agente Linux di Azure versione
    
```bash
waagent -version
```

Per CoreOS, hello sopra comando potrebbe non funzionare.

Si noterà che hello agente Linux di Azure versione è stata aggiornata toohello nuova versione.

Per ulteriori informazioni sulla hello agente Linux di Azure, vedere [Leggimi agente Linux di Azure](https://github.com/Azure/WALinuxAgent).
