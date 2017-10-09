---
title: "velocità effettiva della rete VM aaaOptimize | Documenti Microsoft"
description: "Informazioni su come macchina virtuale di Azure toooptimize rete velocità effettiva."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: a5cff2d0ab6e3553c3f90d99629521a431477de0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a>Ottimizzare la velocità effettiva di rete per le macchine virtuali di Azure

Le macchine virtuali di Azure hanno impostazioni di rete predefinite che possono essere ottimizzate ulteriormente per una migliore velocità effettiva di rete. In questo articolo viene descritto come toooptimize velocità effettiva di rete per Microsoft Windows Azure e le macchine virtuali Linux, incluse le distribuzioni principali quali Ubuntu, CentOS e Red Hat.

## <a name="windows-vm"></a>Macchina virtuale Windows

Se la macchina virtuale di Windows è supportata con [Accelerated rete](virtual-network-create-vm-accelerated-networking.md), abilitare tale funzionalità sarebbe una configurazione ottimale di hello per la velocità effettiva. Per tutte le altre macchine virtuali di Windows, tramite Receive-Side Scaling (RSS) esse possono raggiungere una velocità effettiva massima superiore rispetto a una VM senza RSS. È possibile disabilitare RSS per impostazione predefinita in una macchina virtuale Windows. Completare i seguenti passaggi toodetermine se è abilitato RSS hello e tooenable se è disabilitato.

1. Immettere hello `Get-NetAdapterRss` toosee comando di PowerShell se RSS è abilitato per una scheda di rete. In hello seguente esempio di output restituito da hello `Get-NetAdapterRss`, non è abilitato RSS.

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. Immettere hello tooenable comando RSS seguente:

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    comando precedente Hello non possiede un output. comando Hello modificato le impostazioni di interfaccia di rete, causando la perdita di connettività temporaneo per circa un minuto. Durante la perdita di connettività hello viene visualizzata una finestra di dialogo riconnessione in corso. Connettività in genere viene ripristinata dopo il tentativo di terzo hello.
3. Confermare che RSS è abilitato nella VM hello immettendo hello `Get-NetAdapterRss` nuovo il comando. Se ha esito positivo, viene restituito hello output di esempio riportato di seguito:

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a>VM Linux

RSS è sempre abilitato per impostazione predefinita nella macchina virtuale Linux di Azure. Il kernel Linux rilasciato a partire da gennaio January 2017 include nuove opzioni di ottimizzazione di rete che consentono una VM Linux tooachieve maggiore velocità effettiva della rete.

### <a name="ubuntu"></a>Ubuntu

Ottimizzazione di hello tooget ordine, prima di aggiornare toohello supportata più recente versione, a partire da giugno 2017, ovvero:
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
Al termine dell'aggiornamento di hello, immettere hello kernel più recente di comandi tooget hello seguenti:

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

Comando facoltativo:

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a>Kernel Ubuntu Azure (anteprima)
> [!WARNING]
> Questa versione di anteprima Linux Azure potrebbe non disporre kernel hello dello stesso livello di disponibilità e affidabilità come immagini Marketplace e directcompute che sono in genere il rilascio di disponibilità. funzionalità di Hello non è supportato, può avere vincolato funzionalità e potrebbe non essere affidabili kernel predefinito hello. Non usare questo kernel per carichi di lavoro di produzione.

Installando hello proposto kernel Linux di Azure, è possibile ottenere prestazioni di velocità effettiva significativo. tootry questo kernel, aggiungere questo too/etc/apt/sources.list riga

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

Eseguire quindi questi comandi come radice.
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a>CentOS

Ottimizzazione di hello tooget ordine, prima di aggiornare toohello supportata più recente versione, a partire da luglio 2017, ovvero:
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
Al termine dell'aggiornamento di hello, installare hello più recente Linux Integration Services (LIS).
ottimizzazione della velocità effettiva di Hello è LIS, a partire da 4.2.2-2. Immettere i seguenti comandi tooinstall LIS hello:

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a>Red Hat

Ottimizzazione di hello tooget ordine, prima di aggiornare toohello supportata più recente versione, a partire da luglio 2017, ovvero:
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
Al termine dell'aggiornamento di hello, installare hello più recente Linux Integration Services (LIS).
ottimizzazione della velocità effettiva di Hello è LIS, a partire da 4.2. Immettere hello toodownload i comandi seguenti e installarli:

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

Altre informazioni su Linux Integration Services versione 4.2 per Hyper-V visualizzando hello [pagina di download](https://www.microsoft.com/download/details.aspx?id=55106).

## <a name="next-steps"></a>Passaggi successivi
* Ora che hello VM è ottimizzato, vedere il risultato di hello con [della larghezza di banda/test della velocità effettiva macchina virtuale di Azure](virtual-network-bandwidth-testing.md) per lo scenario.
* Altre informazioni sono disponibili nell'articolo [Domande frequenti sulla rete virtuale di Azure](virtual-networks-faq.md).
