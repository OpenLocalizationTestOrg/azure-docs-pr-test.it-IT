---
title: Proteggere i dati personali inattivi con crittografia aaaAzure | Documenti Microsoft
description: Questo articolo fa parte di una serie consentono di utilizzare i dati personali tooprotect Azure
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a>Tecnologie di crittografia di Azure: proteggere i dati personali inattivi con la crittografia

In questo articolo consente di comprendere e utilizzare dati toosecure tecnologie di crittografia Azure inattivi.

Crittografia dei dati inattivi è essenziale come best practice tooprotect riservate o personali dati e conformità toomeet e requisiti sulla privacy dei dati.
Crittografia inattivi è l'autore dell'attacco hello tooprevent progettato l'accesso ai dati di non crittografato hello garantendo hello dati vengono crittografati quando nel disco.

## <a name="scenario"></a>Scenario 

Una società crociera di grandi dimensioni, sede hello negli Stati Uniti, all'espansione relativo itinerari toooffer operazioni Mediterraneo, hello e mare Baltico, nonché hello isole britannico. toosupport tali attività, che è stato acquisito più righe crociera inferiori basate in Italia, Germania, Danimarca e hello Regno Unito

la società Hello utilizza i dati aziendali di Microsoft Azure toostore nel cloud hello. Può trattarsi di dipendente e/o informazioni sul cliente, ad esempio:

- Indirizzi
- Numeri di telefono
- Codici fiscali
- informazioni mediche
- Dati delle carte di credito

società Hello necessario proteggere la privacy hello di dati dipendenti e clienti durante la creazione di servizi accessibili toothose dati che ne hanno necessità. ad esempio quelli che si occupano di retribuzioni e prenotazioni.

riga crociera Hello gestisce anche un database di grandi dimensioni di benefici e la fedeltà dei membri del programma che include informazioni personali tootrack relazioni con i clienti correnti e precedenti.

### <a name="problem-statement"></a>Presentazione del problema

società Hello necessario proteggere la privacy hello dei dati personali dei dipendenti e clienti durante la creazione di reparti toothose accessibile dati che ne hanno necessità (ad esempio, retribuzioni e le prenotazioni reparti). Questi dati personali viene archiviati all'esterno di centro dati aziendale controllati hello e non sono incluso nel controllo fisico dell'azienda hello.

### <a name="company-goal"></a>Obiettivo dell'azienda

Come parte di una strategia di sicurezza a più livelli di difesa in profondità, è un tooensure obiettivo aziendale che tutte le origini dati che contengono dati personali vengono crittografate, inclusi quelli che risiedono nell'archiviazione cloud. Se non è autorizzato toohello persone guadagno accedere ai dati personali, deve essere in un formato che verrà eseguito il rendering illeggibile. L'applicazione della crittografia deve essere facile, o trasparente, per utenti e amministratori.

## <a name="solutions"></a>Soluzioni

Servizi di Azure forniscono più toohelp strumenti e tecnologie proteggere i dati personali rest crittografandola.

### <a name="azure-key-vault"></a>Insieme di credenziali chiave Azure

[Insieme di credenziali chiave di Azure](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) fornisce l'archiviazione sicura per le chiavi di hello utilizzate tooencrypt dati inattivi nei servizi di Azure e hello consigliata principali soluzioni di archiviazione e la gestione. Gestire la chiave di crittografia è essenziale toosecuring archiviati dati.

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a>Utilizzo di chiavi di tooprotect Azure insieme di credenziali chiave di crittografia dati personali

toouse insieme di credenziali chiave di Azure, è necessario un account di Azure di tooan sottoscrizione. Deve essere installato anche Azure PowerShell. Con PowerShell cmdlet toodo hello seguenti passaggi:

1. Connettersi tooyour sottoscrizioni

2. Creare un insieme di credenziali delle chiavi

3. Aggiungere una chiave o un insieme di credenziali chiave segreta toohello

4. Registrare le applicazioni che verranno utilizzato l'insieme di credenziali chiave hello con Azure Active Directory

5. Autorizzare hello applicazioni toouse hello chiave o il segreto

toocreate un insieme di credenziali chiave, utilizzare i cmdlet di PowerShell New-AzureRmKeyVault hello. È necessario assegnare un nome dell'insieme di credenziali, un nome del gruppo di risorse e una posizione geografica. Si utilizzerà il nome di archivio hello quando la gestione delle chiavi tramite altri cmdlet. Le applicazioni che utilizzano l'insieme di credenziali di hello tramite API REST hello utilizzerà l'URI dell'insieme di credenziali hello.

Azure Key Vault può fornire una chiave protetta tramite software oppure è possibile importare una chiave esistente in un file PFX. È anche possibile archiviare i segreti (password) nell'insieme di credenziali hello.

È anche possibile generare una chiave nel modulo di protezione hardware locale e trasferirlo nel servizio insieme di credenziali chiave, hello tooHSMs senza chiave hello lasciando limite HSM hello.

Per istruzioni dettagliate sull'utilizzo di credenziali chiave di Azure, seguire i passaggi hello [introduzione insieme credenziali chiavi Azure.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)

Per un elenco dei cmdlet di PowerShell usati con Azure Key Vault, vedere [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).

### <a name="azure-disk-encryption-for-windows"></a>Crittografia dischi di Azure per Windows

[Crittografia dischi di Azure per macchine virtuali IaaS Windows e Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protegge i dati personali inattivi nelle macchine virtuali di Azure e si integra con Azure Key Vault. La crittografia del disco di Azure Usa [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows e [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux tooencrypt entrambi hello del sistema operativo e hello dischi dati. Crittografia dischi di Azure è supportata in Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 e nei client Windows 8 e Windows 10.

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a>Utilizzo di dati personali tooprotect di crittografia del disco di Azure

toouse crittografia del disco di Azure, è necessario un account di Azure di tooan sottoscrizione. tooenable Azure disco crittografia per Windows e le macchine virtuali Linux, hello seguenti:

1. Utilizzare il modello di gestione risorse di Azure disco crittografia hello, PowerShell o crittografia del disco tooenable hello interfaccia della riga di comando (CLI) e specificare la configurazione di crittografia. 

2. Concedere accesso toohello materiale della piattaforma Azure tooread hello crittografia di credenziali delle chiavi.

3. Fornire un Azure Active Directory (AAD) applicazione identità toowrite hello crittografia chiave tooyour materiale chiave insieme di credenziali.

Azure Aggiorna hello macchina virtuale e la configurazione dell'insieme di credenziali chiave hello e impostare la macchina virtuale crittografata.

Quando si configura il toosupport insieme di credenziali chiave crittografia del disco di Azure, è possibile aggiungere una chiave di crittografia della chiave (KEK) per maggiore sicurezza e toosupport backup di macchine virtuali crittografati.

![](media/protect-personal-data-at-rest/create-key.png)

Le istruzioni dettagliate per esperienze utente e scenari di distribuzione specifici sono disponibili in [Crittografia dischi di Azure per le macchine virtuali IaaS Windows e Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption).

### <a name="azure-storage-service-encryption"></a>Crittografia del servizio di archiviazione di Azure

[Azure Storage Service crittografia (SSE) per i dati inattivi](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) consente di proteggere e salvaguardare i propri impegni di sicurezza e conformità organizzativi toomeet i dati. Archiviazione di Azure crittografa i dati utilizzando toostorage di toopersisting precedente la crittografia AES a 256 bit automaticamente e lo decrittografa tooretrieval precedente. Questo servizio è disponibile per BLOB di Azure e File di Azure.

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a>Utilizzo di dati personali di tooprotect la crittografia del servizio di archiviazione

la crittografia del servizio di archiviazione, tooenable hello seguenti:

1. Accedere hello portale di Azure.

2. Selezionare un account di archiviazione.

3. In impostazioni, nella sezione del servizio Blob hello, selezionare la crittografia.

4. In hello sezione servizio File, selezionare la crittografia.

Dopo aver selezionato l'impostazione di crittografia hello, è possibile abilitare o disabilitare la crittografia del servizio di archiviazione.

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

I nuovi dati verranno crittografati. I dati presenti nei file esistenti in questo account di archiviazione resteranno non crittografati.

Dopo l'abilitazione della crittografia, copiare account di archiviazione dati toohello utilizzando uno dei seguenti metodi hello:

1. Copiare BLOB o i file con hello [utilità della riga di comando AzCopy](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).

2. [Montare una condivisione file SMB tramite](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) pertanto è possibile utilizzare un'utilità, ad esempio file toocopy Robocopy.

3. Copiare blob o file di dati tooand dall'archiviazione blob o tra gli account di archiviazione tramite [le librerie Client di archiviazione, ad esempio .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).

4.  Utilizzare un [Esplora archivi](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload tooyour account di archiviazione di BLOB con la crittografia attivata.

### <a name="transparent-data-encryption"></a>Transparent Data Encryption

Transparent Data Encryption (TDE) è una funzionalità di SQL Azure mediante il quale è possibile crittografare i dati in entrambi i livelli di hello database e server. La tecnologia TDE è ora abilitata per impostazione predefinita in tutti i nuovi database creati. TDE consente di eseguire la crittografia dei / o e la decrittografia dei file di dati e log hello in tempo reale.

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a>Utilizzo di dati personali tooprotect di Transparent Data Encryption

È possibile configurare Transparent Data Encryption tramite il portale di Azure, hello utilizzando hello API REST o PowerShell. tooenable TDE in un database esistente tramite il portale di Azure, hello hello seguenti:

1. Visitare hello Azure portale in <https://portal.azure.com> e Accedi con l'account amministratore di Azure o collaboratore.

2. Nel banner sinistro hello, fare clic su tooBROWSE e quindi fare clic su database SQL.

3. Con il database SQL selezionati nel riquadro di sinistra hello, fare clic sul proprio database utente.

4. Nel pannello database hello, fare clic su tutte le impostazioni.

5. Nel pannello impostazioni hello, fare clic su Pannello di Transparent data encryption parte tooopen hello Transparent data encryption.

6. Nel Pannello di crittografia dati hello, spostare hello dati crittografia pulsante tooOn e quindi fare clic su Salva (in alto hello pagina hello) impostazione hello tooapply. lo stato di crittografia Hello indicherà approssimativamente lo stato di avanzamento hello di hello transparent data encryption.

![Abilitazione della crittografia dei dati](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

Istruzioni su come tooenable Transparent Data Encryption e informazioni su come decrittografare i database protetti da Transparent Data Encryption e altro ancora sono disponibili nell'articolo hello [Transparent Data Encryption con il Database SQL di Azure.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)

## <a name="summary"></a>Riepilogo

Per eseguire l'obiettivo di crittografare i dati personali archiviati nel cloud di Azure hello società Hello. È possibile farlo mediante la crittografia del disco di Azure troppo proteggere volumi completi. Questo può includere i file del sistema operativo hello e file di dati che contengono informazioni personali e altri dati sensibili. È possibile tooprotect utilizzati i dati personali che viene archiviati in file di BLOB e crittografia del servizio di archiviazione di Azure. Per i dati archiviati in database SQL di Azure, Transparent Data Encryption offre protezione dall'esposizione non autorizzata delle informazioni personali.

tooprotect hello chiavi di dati tooencrypt usato in Azure, è possibile utilizzare insieme credenziali chiavi Azure aziendale hello. Questo semplifica il processo di gestione delle chiavi hello e Abilita hello controllo toomaintain aziendale delle chiavi per l'accesso e crittografare i dati personali.

## <a name="next-steps"></a>Passaggi successivi

- [Guida alla risoluzione dei problemi di Crittografia dischi di Azure](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [Crittografare una macchina virtuale di Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [Crittografia dei dati in Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [Crittografia di dati inattivi del database in Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
