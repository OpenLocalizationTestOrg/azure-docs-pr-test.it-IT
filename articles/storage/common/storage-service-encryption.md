---
title: la crittografia del servizio di archiviazione per i dati inattivi aaaAzure | Documenti Microsoft
description: "Utilizzare hello la crittografia del servizio di archiviazione di Azure funzionalità tooencrypt l'archiviazione Blob di Azure sul lato servizio hello quando si archiviano dati hello decrittografarlo quando si recuperano dati hello."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: edabe3ee-688b-41e0-b34f-613ac9c3fdfd
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: robinsh
ms.openlocfilehash: 4e03c5704071281a798936d41d86456afcfdec77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-service-encryption-for-data-at-rest"></a>Crittografia del servizio di archiviazione di Azure per dati inattivi
Azure Storage Service crittografia (SSE) per i dati inattivi consente di proteggere e tutelare toomeet i dati, la sicurezza dell'organizzazione e impegni di conformità. Con questa funzionalità, di archiviazione di Azure automaticamente crittografa il toostorage toopersisting precedente dei dati e decrittografa tooretrieval precedente. Hello crittografia, decrittografia e la gestione delle chiavi sono toousers completamente trasparente.

Hello nelle sezioni seguenti vengono forniscono istruzioni particolareggiate su come le funzionalità di crittografia di servizio di archiviazione di hello toouse nonché hello supportati gli scenari e l'esperienza utente.

## <a name="overview"></a>Panoramica
Archiviazione di Azure fornisce un set completo di funzionalità di sicurezza che insieme consentono agli sviluppatori di applicazioni sicure toobuild. È possibile proteggere i dati in transito tra un'applicazione e Azure usando la [crittografia lato client](../storage-client-side-encryption.md), HTTPS o SMB 3.0. La crittografia del servizio di archiviazione permette di eseguire la crittografia a riposo, gestendo le operazioni di crittografia, decrittografia e gestione delle chiavi in modo completamente trasparente. Tutti i dati vengono crittografati usando 256 bit [crittografia AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), uno di blocco più forte hello gli algoritmi di crittografia disponibili.

SSE funziona mediante la crittografia dei dati di hello quando viene scritto tooAzure archiviazione e può essere utilizzato per l'archiviazione di File e archiviazione Blob di Azure. Funziona per i seguenti hello:

* Archiviazione standard: account di archiviazione di uso generico per i BLOB, account di archiviazione file e account di archiviazione BLOB
* Archiviazione Premium 
* Tutti i livelli di ridondanza (LRS, ZRS, GRS e RA-GRS)
* Account di archiviazione di Azure Resource Manager (non classici) 
* Tutte le aree.

toolearn, vedere Domande frequenti su toohello.

tooenable o disabilitare la crittografia del servizio di archiviazione per un account di archiviazione, accedere a hello [portale di Azure](https://portal.azure.com) e selezionare un account di archiviazione. Nel pannello impostazioni hello, cercare hello sezione servizio Blob, come illustrato in questa schermata e fare clic su crittografia.

![Screenshot del portale che illustra l'opzione Crittografia](./media/storage-service-encryption/image1.png)
<br/>*Figura 1: abilitare la crittografia del servizio di archiviazione per il servizio BLOB (passaggio 1)*

![Screenshot del portale che illustra l'opzione Crittografia](./media/storage-service-encryption/image3.png)
<br/>*Figura 2: abilitare la crittografia del servizio di archiviazione per il servizio file (passaggio 1)*

Dopo aver selezionato l'impostazione di crittografia hello, è possibile abilitare o disabilitare la crittografia del servizio di archiviazione.

![Screenshot del portale che illustra le proprietà della crittografia](./media/storage-service-encryption/image2.png)
<br/>*Figura 3: abilitare la crittografia del servizio di archiviazione per il servizio BLOB e file (passaggio 2)*

## <a name="encryption-scenarios"></a>Scenari di crittografia
La funzionalità Crittografia del servizio di archiviazione può essere abilitata a livello di account di archiviazione. Una volta abilitato, i clienti sceglierà tooencrypt quali servizi. Supporta hello seguenti scenari:

* Crittografia di archiviazione BLOB e archiviazione file negli account di Resource Manager.
* La crittografia dei Blob e il servizio File negli account di archiviazione classico una volta eseguita la migrazione tooResource Gestione account di archiviazione.

SSE è hello limitazioni seguenti:

* La crittografia degli account di archiviazione classici non è supportata.
* SSE - i dati esistenti consente di crittografare dati appena creato solo dopo aver abilitata la crittografia hello. Se ad esempio si crea un nuovo account di archiviazione di gestione risorse ma non attivare la crittografia e quindi caricare BLOB o account di archiviazione toothat dischi rigidi virtuali archiviati e quindi attivare SSE, tali BLOB non verranno crittografati, a meno che vengono riscritti o copiati.
* Supporto di Marketplace - abilita la crittografia delle macchine virtuali creata da hello Marketplace tramite hello [portale di Azure](https://portal.azure.com), PowerShell e CLI di Azure. immagine di base del disco rigido virtuale Hello rimarrà non crittografata; Tuttavia, eventuali scritture eseguite dopo che è stata riattivata hello macchina virtuale verranno crittografate.
* I dati di tabelle e code non verranno crittografati.

## <a name="getting-started"></a>Introduzione
### <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>Passaggio 1: [Creare un nuovo account di archiviazione](../storage-create-storage-account.md).
### <a name="step-2-enable-encryption"></a>Passaggio 2: Abilitare la crittografia.
È possibile abilitare la crittografia mediante hello [portale di Azure](https://portal.azure.com).

> [!NOTE]
> Se si desidera tooprogrammatically Abilita o disabilita hello la crittografia del servizio di archiviazione in un account di archiviazione, è possibile utilizzare hello [API REST del Provider di risorse archiviazione Azure](https://msdn.microsoft.com/library/azure/mt163683.aspx), hello [libreria Client di Provider di risorse di archiviazione per .NET](https://msdn.microsoft.com/library/azure/mt131037.aspx), [Azure PowerShell](/powershell/azureps-cmdlets-docs), o hello [CLI di Azure](../storage-azure-cli.md).
> 
> 

### <a name="step-3-copy-data-toostorage-account"></a>Passaggio 3: Copiare account toostorage dati
Se si abilita SSE per hello servizio Blob, tutti i BLOB scritti toothat account di archiviazione verranno crittografati. Eventuali BLOB già presenti nell'account di archiviazione non verranno crittografati finché non saranno riscritti. È possibile copiare i dati di hello da tooone account di archiviazione con SSE crittografata, o anche abilitare SSE e copiare hello BLOB da un contenitore tooanother toosure che i dati precedenti sono crittografati. È possibile utilizzare uno qualsiasi dei seguenti strumenti tooaccomplish hello questo. Questo è hello stesso comportamento anche per l'archiviazione di File.

#### <a name="using-azcopy"></a>Con AzCopy
AzCopy è un'utilità della riga di comando di Windows progettata per la copia di dati tooand dall'archiviazione Blob di Microsoft Azure, File e tabella utilizzando i comandi semplici con prestazioni ottimali. È possibile utilizzare questo toocopy BLOB o dei file da un tooanother di account di archiviazione quello che ha attivato SSE. 

toolearn, visitare [trasferire i dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md).

#### <a name="using-smb"></a>Con SMB
Archiviazione di File di Azure offre le condivisioni di file in un cloud di hello tramite il protocollo SMB standard di hello. È possibile montare una condivisione di file da un client in locale o in Azure. Una volta montato, strumenti come Robocopy possono essere utilizzati toocopy file over tooAzure che condivisioni File. Per ulteriori informazioni, vedere [come toomount condividono i File di Azure in Windows](../files/storage-how-to-use-files-windows.md) e [come File di Azure toomount condividere in Linux](../storage-how-to-use-files-linux.md).


#### <a name="using-hello-storage-client-libraries"></a>Utilizzando le librerie Client di archiviazione hello
È possibile copiare tooand dati blob o di file dall'archiviazione blob o tra gli account di archiviazione tramite il set completo delle librerie Client di archiviazione inclusi .NET, C++, Java, Android, Node.js, PHP, Python e Ruby.

toolearn, visitare il nostro [Introduzione all'archiviazione Blob di Azure usando .NET](../blobs/storage-dotnet-how-to-use-blobs.md).

#### <a name="using-a-storage-explorer"></a>Con Storage Explorer
È possibile usare un account di archiviazione toocreate soluzioni di archiviazione, caricare e scaricare i dati, visualizzare il contenuto di BLOB e spostarsi tra le directory. È possibile utilizzare uno di questi account di archiviazione tooupload tooyour BLOB con la crittografia attivata. Con alcuni strumenti di esplorazione di archiviazione, è inoltre possibile copiare dati da blob tooa diverso contenitore di archiviazione esistente nell'account di archiviazione hello o un nuovo account di archiviazione con SSE abilitato.

toolearn, visitare [Esplora archivi Azure](../storage-explorers.md).

### <a name="step-4-query-hello-status-of-hello-encrypted-data"></a>Passaggio 4: Eseguire una Query sullo stato di hello di dati crittografato hello
È stata distribuita una versione aggiornata delle librerie Client di archiviazione hello che consente lo stato di hello tooquery di toodetermine un oggetto se si è crittografato o meno. È attualmente disponibile solo per Archiviazione BLOB. Supporto per l'archiviazione di File è roadmap hello. 

In hello frattempo, è possibile chiamare [ottenere proprietà Account](https://msdn.microsoft.com/library/azure/mt163553.aspx) tooverify che hello account di archiviazione è abilitata la crittografia o la vista hello proprietà account di archiviazione nel portale di Azure hello.

## <a name="encryption-and-decryption-workflow"></a>Flusso di lavoro di crittografia e decrittografia
Di seguito è riportata una breve descrizione del flusso di lavoro crittografia/decrittografia hello:

* cliente Hello abilita la crittografia sull'account di archiviazione hello.
* Quando il cliente hello scrive tooBlob dati (PUT Blob, inserire blocco, PUT Page, inserire File ecc) nuova o archiviazione di File; ogni operazione di scrittura viene crittografato con 256 bit [crittografia AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), uno di blocco più forte hello gli algoritmi di crittografia disponibili.
* Quando hello cliente necessita di dati tooaccess (GET Blob e così via), i dati vengono decrittografati automaticamente prima della restituzione toohello utente.
* Se la crittografia è disabilitata, nuove scritture non vengono più crittografate e i dati crittografati esistenti rimangano crittografati fino a quando non riscritto da utente hello. Mentre la crittografia è abilitata, consente di scrivere tooBlob o archiviazione di File verrà crittografata. stato Hello dei dati non cambia con utente hello passando tra l'abilitazione/disabilitazione della crittografia per l'account di archiviazione hello.
* Tutte le chiavi di crittografia vengono archiviate, crittografate e gestite da Microsoft.

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>Domande frequenti su Crittografia del servizio di archiviazione per i dati inattivi
**D: È disponibile un account di archiviazione classico. Si può abilitare Crittografia del servizio di archiviazione per questo account?**

R: No, la funzionalità di crittografia del servizio di archiviazione è supportata solo negli account di archiviazione di Resource Manager.

**D: Come si crittografano i dati nell'account di archiviazione classico?**

R: è possibile creare un nuovo account di archiviazione di gestione delle risorse e copiare i dati con [AzCopy](storage-use-azcopy.md) dall'account di archiviazione classico esistente tooyour appena creati account di archiviazione di gestione risorse. 

Se si esegue la migrazione il tooa di account account di archiviazione di gestione risorse di archiviazione classico, questa operazione è istantanea, modifica il tipo di hello del tuo account, ma non influenzano i dati esistenti. Eventuali nuovi dati verranno crittografati solo dopo l'attivazione della crittografia. Per ulteriori informazioni, vedere [supportata la migrazione di IaaS risorse della piattaforma da classica tooResource Manager](https://azure.microsoft.com/blog/iaas-migration-classic-resource-manager/). Si noti che questa operazione è supportata solo per i servizi BLOB e file.

**D: È disponibile un account di archiviazione di Resource Manager. Si può abilitare Crittografia del servizio di archiviazione per questo account?**

R: Sì, ma verranno crittografati solo i dati appena scritti. La funzionalità non è retroattiva e i dati già presenti non verranno crittografati. Non si è ancora supportata per l'anteprima di archiviazione di File hello.

**D: Vorrei tooencrypt hello dati correnti di un account di archiviazione di gestione risorse esistente?**

R: La crittografia del servizio di archiviazione può essere abilitata in qualsiasi momento in un account di archiviazione di Resource Manager. Tuttavia, i dati che erano già presenti non verranno crittografati. tooencrypt dati esistenti, è possibile copiare i file tooanother nome o un altro contenitore e quindi rimuovere le versioni non crittografato hello.

**D: È possibile usare Crittografia del servizio di archiviazione se si usa l'Archiviazione Premium?**

R: Sì, la funzionalità Crittografia del servizio di archiviazione è supportata nell'Archiviazione Standard e nell'Archiviazione Premium.  Archiviazione Premium non è supportata per il servizio File hello.

**D: Se si crea un nuovo account di archiviazione e si abilita Crittografia del servizio di archiviazione, quindi si crea una nuova VM usando tale account di archiviazione, la VM sarà crittografata?**

A: Sì. I dischi che utilizzano il nuovo account di archiviazione hello creati verranno crittografati, come vengono creati dopo l'abilitazione di SSE. Se hello che VM è stato creato utilizzando Azure Market Place, immagine di base del disco rigido virtuale hello rimarrà non crittografata; Tuttavia, eventuali scritture eseguite dopo che è stata riattivata hello macchina virtuale verranno crittografate.

**D: È possibile creare nuovi account di archiviazione con la funzionalità Crittografia del servizio di archiviazione abilitata usando Azure PowerShell e l'interfaccia della riga di comando di Azure?**

A: Sì.

**D: A quanto ammonta il costo aggiuntivo dell'Archiviazione di Azure se si abilita Crittografia del servizio di archiviazione?**

R: Non sono previsti costi aggiuntivi.

**D: chi gestisce le chiavi di crittografia hello?**

R: le chiavi di hello vengono gestite da Microsoft.

**D: È possibile usare le proprie chiavi di crittografia?**

R: stiamo lavorando per fornire funzionalità per i clienti toobring le rispettive chiavi di crittografia.

**D: posso revoca dell'accesso toohello chiavi di crittografia?**

R: non in questa fase. le chiavi di Hello sono completamente gestite da Microsoft.

**D: La funzionalità Crittografia del servizio di archiviazione è abilitata per impostazione predefinita quando si crea un nuovo account di archiviazione?**

R: SSE non è abilitato per impostazione predefinita. è possibile utilizzare hello tooenable portale Azure è. Anche a livello di codice, è possibile abilitare questa funzionalità utilizzando hello API REST di Provider di risorse di archiviazione.

**D: Quali sono le differenze rispetto alla Crittografia dischi di Azure?**

R: questa funzionalità è tooencrypt utilizzati dati nell'archiviazione Blob di Azure. Hello Azure crittografia del disco è utilizzato tooencrypt del sistema operativo e i dischi dati in macchine virtuali IaaS. Per altre informazioni, vedere la [Guida alla sicurezza delle risorse di archiviazione](../storage-security-guide.md).

**D: cosa accade se Abilita SSE, andare e abilitare la crittografia del disco di Azure su dischi hello?**

R: Non si verifica alcun problema. I dati verranno crittografati da entrambi i metodi.

**Q: l'account di archiviazione è configurato toobe replicata geo-ridondante. Se si abilita la crittografia del sistema di archiviazione, verrà crittografata anche la copia ridondante?**

R: Sì, tutte le copie dell'account di archiviazione hello vengono crittografate e tutte le opzioni di ridondanza, archiviazione con ridondanza locale (LRS), archiviazione ridondante di zona (ZRS), archiviazione ridondanza geografica (GRS) e archiviazione ridondanza geografica e accesso in lettura (RA-GRS), sono supportate.

**D: Non è possibile abilitare la crittografia sull'account di archiviazione.**

R: Se si tratta di un account di archiviazione di Resource Manager, gli account di archiviazione di tipo classico non sono supportati. 

**D: La crittografia del servizio di archiviazione è disponibile solo in aree specifiche?**

R: hello SSE è disponibile in tutte le aree per l'archiviazione Blob. Verificare hello sezione di disponibilità per l'archiviazione di File. 

**D: come si può contattare un utente se verificano problemi o si desidera tooprovide feedback?**

R: contattare [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) per eventuali problemi correlati tooStorage la crittografia del servizio.

## <a name="next-steps"></a>Passaggi successivi
Archiviazione di Azure fornisce un set completo di funzionalità di sicurezza che insieme consentono agli sviluppatori di applicazioni sicure toobuild. Per ulteriori dettagli, visitare hello [Guida alla protezione di archiviazione](../storage-security-guide.md).

