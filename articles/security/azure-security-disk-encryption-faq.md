---
title: domande frequenti su crittografia disco aaaAzure | Documenti Microsoft
description: In questo articolo vengono fornite le risposte toofrequently domande frequenti su Microsoft Azure disco crittografia per Windows e le macchine virtuali IaaS di Linux.
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: 7188da52-5540-421d-bf45-d124dee74979
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: devtiw
ms.openlocfilehash: 17f084628ba4ef22e9d37dd3052ef10f8eb2cd7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-frequently-asked-questions-faq"></a>Domande frequenti su Crittografia dischi di Azure

Questo documento fornisce le risposte alle domande frequenti su Crittografia dischi di Azure per le macchine virtuali IaaS Windows e Linux. Per altre informazioni su questo servizio, vedere [Azure Disk Encryption per le macchine virtuali IaaS Windows e Linux](https://docs.microsoft.com/azure/security/azure-security-disk-encryption).

## <a name="general-questions"></a>Domande generali
**D.** In quale area è disponibile Crittografia dischi di Azure in versione GA?

**R:** Crittografia dischi di Azure per le macchine virtuali IaaS Windows e Linux è disponibile in versione GA (disponibilità generale) in tutte le aree pubbliche di Azure.

**D:** Quali esperienze utente sono disponibili con Crittografia dischi di Azure?

**R:** La versione GA di Crittografia dischi di Azure supporta i modelli di Azure Resource Manager, Azure PowerShell e l'interfaccia della riga di comando di Azure. Questo assicura una notevole flessibilità, in quanto sono disponibili tre diverse opzioni per l'abilitazione della crittografia del disco per le macchine virtuali IaaS. Ulteriori informazioni sull'esperienza utente hello e informazioni aggiuntive dettagliate è disponibile in scenari di distribuzione di crittografia del disco Azure hello ed esperienze.

**D:** Quanto costa Crittografia dischi di Azure?

**R:** Non è previsto alcun addebito per la crittografia dei dischi delle macchine virtuali con Crittografia dischi di Azure.

**D:** Con quali livelli di macchine virtuali è possibile usare Crittografia dischi di Azure?

**R:** Crittografia dischi di Azure è disponibile solo per le macchine virtuali del piano Standard, incluse le macchine virtuali IaaS serie [A, D, DS, G, GS, F](https://azure.microsoft.com/pricing/details/virtual-machines/) e così via, comprese le macchine virtuali con Archiviazione Premium. Non è disponibile per le macchine virtuali del piano Basic.

**D:** Quali distribuzioni di Linux sono supportate da Crittografia dischi di Azure?

**R:** crittografia del disco di Azure è supportata in hello seguendo le distribuzioni di server Linux e le versioni:

| Distribuzione Linux | Versione | Tipo di volume supportato per la crittografia|
| --- | --- |--- |
| Ubuntu | 16.04-DAILY-LTS | Disco del sistema operativo e dati |
| Ubuntu | 14.04.5-DAILY-LTS | Disco del sistema operativo e dati |
| RHEL | 7.3 | Disco del sistema operativo e dati |
| RHEL | 7,2 | Disco del sistema operativo e dati |
| RHEL | 6.8 | Disco del sistema operativo e dati |
| RHEL | 6.7 | Disco dati |
| CentOS | 7.3 | Disco del sistema operativo e dati |
| CentOS | 7.2n | Disco del sistema operativo e dati |
| CentOS | 6.8 | Disco del sistema operativo e dati |
| CentOS | 7.1 | Disco dati |
| CentOS | 7.0 | Disco dati |
| CentOS | 6.7 | Disco dati |
| CentOS | 6.6 | Disco dati |
| CentOS | 6,5 | Disco dati |
| openSUSE | 13.2 | Disco dati |
| SLES | 12 SP1 | Disco dati |
| SLES | Priority:12-SP1 | Disco dati |
| SLES | HPC 12 | Disco dati |
| SLES | Priority:11-SP4 | Disco dati |
| SLES | 11 SP4 | Disco dati |

**D:** Come si può iniziare a usare Crittografia dischi di Azure?

**R:** clienti utili come tooget iniziare dalla lettura hello white paper di crittografia del disco di Azure si trova [qui](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)

**D:** È possibile crittografare sia i volumi di avvio che i volumi di dati con Crittografia dischi di Azure?

**R:** Sì, è possibile crittografare volumi di avvio e volumi di dati per le macchine virtuali IaaS Windows e Linux. Per le macchine virtuali di Windows, è possibile crittografare i dati hello senza hello encrpting primo volume del sistema operativo. Per le macchine virtuali Linux, è possibile crittografare il volume di dati hello senza encryptinng hello volume del sistema operativo. Una volta per Liux sono stati crittografati volume hello del sistema operativo, la disabilitazione della crittografia in un volume del sistema operativo per le macchine virtuali IaaS di Linux non è supportata

**D:** Crittografia dischi di Azure rende disponibili funzionalità BYOK (Bring Your Own Key)?

**R:** Sì, è possibile fornire le proprie chiavi di crittografia della chiave. Tali chiavi siano protette nell'insieme di credenziali chiave di Azure, ovvero l'archivio delle chiavi di crittografia del disco Azure hello. Per ulteriori informazioni sulla chiave di crittografia della chiave hello supportare gli scenari, vedere esperienze e scenari di distribuzione di hello crittografia del disco di Azure

**D:** È possibile usare una chiave di crittografia della chiave creata in Azure?

**R:** Sì, è possibile utilizzare una chiave di crittografia della chiave toogenerate insieme di credenziali chiave di Azure per l'utilizzo di crittografia del disco di Azure. Tali chiavi siano protette nell'insieme di credenziali chiave di Azure, ovvero l'archivio delle chiavi di crittografia del disco Azure hello. Per ulteriori informazioni sulla chiave di crittografia della chiave hello supportare gli scenari, vedere esperienze e scenari di distribuzione di hello crittografia del disco di Azure

**Q:** è possibile utilizzare chiavi di crittografia hello servizio/HSM toosafeguard gestione delle chiavi locale?

**R:** non è possibile utilizzare le chiavi di crittografia hello servizio/HSM toosafeguard gestione delle chiavi locale hello con la crittografia del disco di Azure. È possibile utilizzare solo chiavi di crittografia hello servizio toosafeguard hello Azure dell'insieme di credenziali chiave. Per ulteriori informazioni sulla chiave di crittografia della chiave hello supportare gli scenari, vedere esperienze e scenari di distribuzione di hello crittografia del disco di Azure

**Q:** quali sono crittografia del disco Azure tooconfigure prerequisiti hello?

**R:** hello Azure disco crittografia prerequisiti PowerShell script toocreate AAD dell'applicazione, creare nuovo insieme di credenziali chiave o del programma di installazione esistente dell'insieme di credenziali chiave disco crittografia accesso tooenable crittografia e tutelare i segreti e la chiave.  Per ulteriori informazioni sulla chiave di crittografia della chiave hello supportare gli scenari, vedere i prerequisiti di crittografia del disco Azure hello e scenari di distribuzione e l'esperienza

**Q:** dove è possibile ottenere ulteriori informazioni su come toouse PowerShell per la configurazione di crittografia del disco di Azure?

**R:** Sono disponibili alcuni interessanti articoli su come eseguire le attività di base in Crittografia dischi di Azure, oltre a scenari più avanzati. Per le attività di base hello, fai clic su Esplora [crittografia del disco di Azure con Azure PowerShell - parte 1](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/explore-azure-disk-encryption-with-azure-powershell/). Per gli scenari più avanzati, vedere [Esplorare Crittografia dischi di Azure con Azure PowerShell - Parte 2](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2/).

**D:** Quale versione di Azure PowerShell è supportata da Crittografia dischi di Azure?

**R:** utilizzare hello più recente di Azure PowerShell SDK versione tooconfigure crittografia del disco di Azure. Scaricare una versione più recente di hello di [Azure PowerShell](https://github.com/Azure/azure-powershell/releases). Crittografia dischi di Azure NON è supportato da Azure SDK versione 1.1.0.

> [!NOTE]
> estensione dell'anteprima di Linux Azure disco crittografia Hello è deprecata. Per informazioni dettagliate, vedere toodocumentation [qui](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/12/deprecating-azure-disk-encryption-preview-extension-for-linux-iaas-vms/)

**D:** È possibile applicare Crittografia dischi di Azure a un'immagine Linux personalizzata?

**R:** Non è possibile applicare Crittografia dischi di Azure a un'immagine Linux personalizzata. È supportato solo le immagini Linux raccolta hello per le distribuzioni di hello supportata indicate sopra. Attualmente le immagini Linux personalizzate non sono supportate.

**Q:** è possibile applicare gli aggiornamenti tooa Linux Red Hat VM mediante l'aggiornamento Yum?

**R:** Sì, è possibile aggiornare e/o applicare patch a una macchina virtuale Linux Red Hat seguendo le istruzioni riportate [qui](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/13/applying-updates-to-a-encrypted-azure-iaas-red-hat-vm-using-yum-update/)

**Q:** in cui è possibile passare tooask domanda o fornire commenti e suggerimenti

**R:** è possibile fornire porre domande o commenti e suggerimenti sul forum di crittografia del disco di Azure hello [qui](https://social.msdn.microsoft.com/Forums/home?forum=AzureDiskEncryption)

## <a name="see-also"></a>Vedere anche
In questo documento, illustrando più hello più frequenti domande correlate tooAzure crittografia del disco, per ulteriori informazioni su questo servizio e la relativa funzionalità di lettura:

- [Applicare la crittografia dei dischi nel Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Crittografare una macchina virtuale di Azure](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Crittografia dei dati inattivi di Azure](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
