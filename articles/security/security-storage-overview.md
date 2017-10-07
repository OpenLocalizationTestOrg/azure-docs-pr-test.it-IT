---
title: "funzionalità aaaSecurity che può essere utilizzata con l'archiviazione di Azure | Documenti Microsoft"
description: " In questo articolo viene fornita una panoramica delle funzionalità di sicurezza di Azure hello principali che può essere utilizzato con l'archiviazione di Azure. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 521180dc-2cc9-43f1-ae87-2701de7ca6b8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 663cd2705527957d21ff9475a6322b42a16c95e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-overview"></a>Panoramica sulla sicurezza di Archiviazione di Azure
Archiviazione di Azure è una soluzione di archiviazione cloud hello per le moderne applicazioni che si basano su esigenze di hello toomeet scalabilità dei clienti, disponibilità e durata. Archiviazione di Azure offre un set completo di funzionalità di sicurezza:

* account di archiviazione Hello possono essere protetti utilizzando Role-Based Access Control e Azure Active Directory.
* È possibile proteggere i dati in transito tra un'applicazione e Azure usando la crittografia lato client, HTTPS o SMB 3.0.
* Dati possono essere impostati toobe crittografato automaticamente quando scritti tooAzure archiviazione mediante la crittografia del servizio di archiviazione.
* I dischi del sistema operativo e i dati utilizzati dalle macchine virtuali possono essere impostati toobe crittografata con la crittografia del disco di Azure.
* È possibile concedere l'accesso delegato toohello dati oggetti nell'archiviazione di Azure tramite firme di accesso condiviso.
* metodo di autenticazione Hello utilizzato da un utente durante l'accesso di archiviazione può essere rilevato tramite analitica di archiviazione.

Per informazioni più dettagliate di sicurezza in archiviazione di Azure, vedere hello [Guida alla protezione di archiviazione di Azure](../storage/common/storage-security-guide.md). Questa guida fornisce un approfondimento di funzionalità di sicurezza hello dell'archiviazione di Azure, ad esempio chiavi account di archiviazione, la crittografia dei dati in transito e rest e analitica di archiviazione.

Questo articolo offre informazioni generali sulle funzionalità di sicurezza di Azure che possono essere usate con Archiviazione di Azure. Vengono forniti tooarticles che forniscono i dettagli di ogni funzionalità in modo da acquisire più collegamenti.

Di seguito sono hello core funzionalità toobe illustrate in questo articolo:

* Controllo degli accessi in base al ruolo
* L'accesso delegato toostorage oggetti
* Crittografia in transito
* Crittografia di dati inattivi/Crittografia del servizio di archiviazione
* Azure Disk Encryption
* Insieme di credenziali chiave Azure

## <a name="role-based-access-control-rbac"></a>Controllo degli accessi in base al ruolo
È possibile proteggere l'account di archiviazione con il controllo degli accessi in base al ruolo. Limitazione dell'accesso basato su hello [necessario tooknow](https://en.wikipedia.org/wiki/Need_to_know) e [privilegio](https://en.wikipedia.org/wiki/Principle_of_least_privilege) principi di sicurezza è fondamentale per le organizzazioni che vogliono tooenforce criteri di sicurezza per l'accesso ai dati. Questi diritti di accesso vengono concesse tramite l'assegnazione di hello appropriato RBAC ruolo toogroups e alle applicazioni da un determinato ambito. È possibile utilizzare [ruoli RBAC incorporati](../active-directory/role-based-access-built-in-roles.md), ad esempio di collaboratore di Account di archiviazione, tooassign privilegi toousers.

Altre informazioni:

* [Controllo degli accessi in base al ruolo di Azure Active Directory](../active-directory/role-based-access-control-configure.md)

## <a name="delegated-access-toostorage-objects"></a>L'accesso delegato toostorage oggetti
Una firma di accesso condiviso (SAS) fornisce l'accesso delegato tooresources nell'account di archiviazione. Hello SAS significa che è possibile concedere a che un client limitate tooobjects autorizzazioni nell'account di archiviazione per un determinato periodo di tempo e con un set specificato di autorizzazioni. È possibile concedere queste autorizzazioni limitate senza tooshare le chiavi di accesso di account. Hello firma di accesso condiviso è un URI che include i parametri di query di tutte le informazioni di hello necessarie per la risorsa di archiviazione tooa l'accesso autenticato. risorse di archiviazione tooaccess con hello SAS, hello client deve solo tooprovide hello SAS toohello appropriato al costruttore o metodo.

Altre informazioni:

* [Modello di firma di accesso condiviso di conoscenza hello](../storage/common/storage-dotnet-shared-access-signature-part-1.md)
* [Creare e usare una firma di accesso condiviso con l'archiviazione BLOB](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)

## <a name="encryption-in-transit"></a>Crittografia in transito
La crittografia in transito è un meccanismo di protezione dei dati durante la trasmissione tra le reti. Con Archiviazione di Azure è possibile proteggere i dati con:

* [Crittografia a livello di trasporto](../storage/common/storage-security-guide.md#encryption-in-transit), ad esempio HTTPS quando si trasferiscono dati all'interno o all'esterno di Archiviazione di Azure.
* [Crittografia di rete](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), ad esempio la crittografia SMB 3.0 per le condivisioni file di Azure.
* [Crittografia client-side](../storage/common/storage-security-guide.md#using-client-side-encryption-to-secure-data-that-you-send-to-storage), dati di hello tooencrypt prima di essere trasferiti in toodecrypt e archiviazione dati hello dopo che viene trasferita all'esterno di archiviazione.

Altre informazioni sulla crittografia lato client:

* [Crittografia lato client per Archiviazione di Microsoft Azure](https://blogs.msdn.microsoft.com/windowsazurestorage/2015/04/28/client-side-encryption-for-microsoft-azure-storage-preview/)
* [Serie di controlli della sicurezza del cloud: crittografia dei dati in transito](http://blogs.microsoft.com/cybertrust/2015/08/10/cloud-security-controls-series-encrypting-data-in-transit/)

## <a name="encryption-at-rest"></a>Crittografia di dati inattivi
Per molte organizzazioni, [la crittografia dei dati inattivi](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) è un passaggio obbligatorio per assicurare la privacy dei dati, la conformità e la sovranità dei dati. Esistono tre funzionalità di Azure che consentono di crittografare dati inattivi:

* [La crittografia del servizio di archiviazione](../storage/common/storage-security-guide.md#encryption-at-rest) consente che il servizio di archiviazione hello crittografa automaticamente i dati durante la scrittura di archiviazione tooAzure toorequest.
* [Crittografia client-side](../storage/common/storage-security-guide.md#client-side-encryption) offre inoltre funzionalità hello di crittografia.
* [Crittografia disco Azure](../storage/common/storage-security-guide.md#using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) consente tooencrypt hello del sistema operativo dischi e i dischi di dati utilizzati da una macchina virtuale IaaS.

Altre informazioni su Crittografia del servizio di archiviazione:

* La [crittografia del servizio di archiviazione di Azure](https://azure.microsoft.com/services/storage/) è disponibile per [Archiviazione BLOB di Azure](https://azure.microsoft.com/services/storage/blobs/). Per informazioni su altri tipi di archiviazione di Azure, vedere [File](https://azure.microsoft.com/services/storage/files/), [Disco (Archiviazione Premium)](https://azure.microsoft.com/services/storage/premium-storage/), [Tabella](https://azure.microsoft.com/services/storage/tables/) e [Coda](https://azure.microsoft.com/services/storage/queues/).
* [Crittografia del servizio di archiviazione di Azure per dati inattivi](../storage/common/storage-service-encryption.md)

## <a name="azure-disk-encryption"></a>Azure Disk Encryption
Crittografia dischi di Azure per le macchine virtuali consente di soddisfare i requisiti di conformità e sicurezza dell'organizzazione, grazie alla possibilità di crittografare i dischi delle macchine virtuali, inclusi i dischi di avvio e di dati, con chiavi e criteri gestiti in [Insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/services/key-vault/).

Crittografia dischi per le macchine virtuali funziona con sistemi operativi sia Linux, sia Windows. Utilizza inoltre un insieme di credenziali chiave toohelp proteggere, gestire e controllare l'uso delle chiavi di crittografia del disco. Tutti i dati di hello i dischi di macchina virtuale vengono crittografati a riposo usando la tecnologia di crittografia standard del settore negli account di archiviazione di Azure. soluzioni di crittografia del disco per Windows Hello è basato su [crittografia unità BitLocker di Microsoft](https://technet.microsoft.com/library/cc732774.aspx), e hello Linux soluzione si basa su [dm crypt](https://en.wikipedia.org/wiki/Dm-crypt).

Altre informazioni:

* [Crittografia dischi di Azure per le macchine virtuali IaaS Windows e Linux](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)

## <a name="azure-key-vault"></a>Insieme di credenziali chiave Azure
La crittografia del disco di Azure Usa [insieme credenziali chiavi Azure](https://azure.microsoft.com/services/key-vault/) toohelp controllare e gestire chiavi di crittografia del disco e i segreti nella sottoscrizione di insieme di credenziali delle chiavi, assicurando che tutti i dati nei dischi di macchina virtuale hello vengono crittografati a riposo in di Azure Spazio di archiviazione. È consigliabile utilizzare chiavi tooaudit insieme di credenziali chiave e utilizzo dei criteri.

Altre informazioni:

* [Cos'è l'insieme di credenziali chiave di Azure?](../key-vault/key-vault-whatis.md)
* [Introduzione all'insieme di credenziali delle chiavi di Azure](../key-vault/key-vault-get-started.md)
