---
title: aaaGet un ID di macchina virtuale Linux di Azure | Documenti Microsoft
description: Viene descritto come tooget e utilizzare un Azure Linux VM ID univoco.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a>Accesso e uso dell'ID univoco di una VM di Azure
L'ID univoco di una VM di Azure è un identificatore a 128 bit codificato e archiviato nel sistema SMBIOS di tutte le VM IaaS di Azure e attualmente può essere letto usando i comandi BIOS della piattaforma.

L'ID univoco di una VM di Azure è una proprietà di sola lettura. L'ID univoco di una VM di Azure non verrà modificato in caso di riavvio, arresto (pianificato o non pianificato), avvio/arresto della deallocazione, riparazione di servizi o ripristino sul posto. Tuttavia, se hello VM è un toocreate snapshot e copia di una nuova istanza, nuovo ID di macchina virtuale di Azure è configurato.

> [!NOTE]
> Se si dispone di macchine virtuali meno recenti create e in esecuzione poiché questa nuova funzionalità ottenuto implementata (18 settembre 2014), riavviare la macchina virtuale tooautomatically ottenere un ID univoco Azure.
> 
> 

tooaccess univoco ID macchina virtuale Azure all'interno di hello VM:

## <a name="create-a-vm"></a>Creare una macchina virtuale
Per altre informazioni, vedere [Creare una macchina virtuale](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="connect-toohello-vm"></a>Connettersi toohello VM
Per altre informazioni, vedere [SSH da Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="query-vm-unique-id"></a>Effettuare una query dell'ID univoco di una VM
Comando (l'esempio usa **Ubuntu**):

```bash
sudo dmidecode | grep UUID
```

Risultati previsti per l'esempio:

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

A causa di tooBig bit ordine Little-Endian, hello effettivo ID univoco di VM in questo caso sarà:

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

ID univoco di VM Azure può essere usata in diversi scenari se hello macchina virtuale è in esecuzione in Azure o in locale e può aiutare i requisiti di gestione licenze, report o generale che è possibile in distribuzioni IaaS di Azure. Molti fornitori di software indipendenti, applicazioni e la certificazione li in Azure possono richiedere una macchina virtuale di Azure in tutto il ciclo di vita e tootell tooidentify se hello macchina virtuale è in esecuzione in Azure, locale o in altri provider di cloud. Questo identificatore di piattaforma, ad esempio consente di rilevare se il software di hello correttamente è concesso in licenza o della Guida di qualsiasi origine tooits dati di macchina virtuale, ad esempio tooassist sull'impostazione hello destra la metrica per piattaforma destra hello e tootrack toocorrelate e correlare queste metriche, tra cui altri utilizzi.

