---
title: Panoramica di crittografia aaaAzure | Documenti Microsoft
description: Informazioni sulle varie opzioni di crittografia in Azure
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/18/2017
ms.author: barclayn
ms.openlocfilehash: ef9ab46de32b857e99e8fe628a61386b95cf197f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-overview"></a>Panoramica della crittografia di Azure

Questo articolo fornisce una panoramica dell'utilizzo della crittografia in Microsoft Azure. Vengono illustrate le aree principali hello di crittografia, tra cui crittografia, la crittografia volo e gestione delle chiavi con l'insieme di credenziali chiave. Ogni sezione include i collegamenti per informazioni più dettagliate.

## <a name="encryption-of-data-at-rest"></a>Crittografia dei dati inattivi

I dati inattivi includono informazioni presenti nell'archivio permanente su un supporto fisico, in qualsiasi formato digitale. Sono inclusi i file su supporto ottico o magnetico, i dati archiviati e i backup di dati. Microsoft Azure offre un'ampia gamma di toomeet soluzioni di archiviazione dati esigenze diverse, tra cui file, disco, blob e archiviazione tabella. Microsoft fornisce anche la crittografia tooprotect [Database SQL di Azure](../sql-database/sql-database-technical-overview.md), [CosmosDB](../cosmos-db/introduction.md)e Azure Data Lake.

La crittografia dei dati inattivi è disponibile per i servizi in hello Azure Software-as-a-Service (SaaS), Platform-as-a-Service (PaaS) e i modelli cloud Infrastructure-as-a-Service (IaaS). Questo documento sono riepilogate e fornisce le risorse toohelp si utilizzano opzioni di crittografia di Azure.

Per ulteriori informazioni sulle modalità dati inattivi vengono crittografati in Azure, vedere il documento hello intitolato [dati di Azure--crittografia](azure-security-encryption-atrest.md)

## <a name="azure-encryption-models"></a>Modelli di crittografia di Azure

Azure supporta vari modelli di crittografia, tra cui la crittografia lato server usando chiavi gestite dal servizio, usando chiavi gestite dal cliente in Azure Key Vault o usando chiavi gestite dal cliente sull'hardware controllato dal cliente. Crittografia client-side consente toomanage e l'archivio chiavi locale o in un altro percorso di protezione.

### <a name="client-side-encryption"></a>Crittografia lato client

La crittografia lato client viene eseguita all'esterno di Azure. La crittografia lato client include:

- Dati crittografati da un'applicazione in esecuzione nel centro dati del cliente hello o da un'applicazione di servizio
- I dati sono già crittografati quando vengono ricevuti da Azure.

Con la crittografia lato client il provider di servizi cloud hello non dispone di chiavi di crittografia toohello di accesso e non può decrittografare questi dati. È necessario mantenere il controllo completo dei tasti hello.

### <a name="server-side-encryption"></a>Modello di crittografia lato server

tre modelli di crittografia lato server Hello offrono caratteristiche di gestione delle chiavi diverse, che possono essere scelti per i requisiti.

- Le **chiavi gestite dal servizio** combinano controllo e comodità con un sovraccarico ridotto

- **Chiavi gestite dal cliente** consentono di controllare le chiavi di hello, inclusi hello possibilità toobring toogenerate nuovi o personali chiavi (BYOK).

- **Chiavi gestite dal servizio in ccustomer controlledhardware** consente chiavi toomanage nel repository proprietarie di fuori del controllo di Microsoft. Questo approccio viene definito HYOK (Host Your Own Key). Tuttavia, la configurazione è complessa e la maggior parte dei servizi di Azure non supporta questo modello.

### <a name="azure-disk-encryption"></a>Azure Disk Encryption

Macchine virtuali Linux e Windows possono essere protetti utilizzando [crittografia del disco Azure](azure-security-disk-encryption.md), che utilizza hello [Windows BitLocker](https://technet.microsoft.com/library/cc766295(v=ws.10).aspx) tecnologia e Linux [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) tooprotect i dischi del sistema operativo e dischi di dati con crittografia dell'intero volume.

Le chiavi e i segreti di crittografia vengono protetti nella sottoscrizione di [Azure Key Vault](../key-vault/key-vault-whatis.md). È possibile eseguire il backup e ripristinare crittografate macchine virtuali che vengono crittografate con la configurazione di KEK hello tramite il servizio di Azure Backup hello.

### <a name="azure-storage-service-encryption"></a>Crittografia del servizio di Archiviazione di Azure

I dati inattivi in archiviazione di Azure (BLOB e file) possono essere crittografati in scenari sia sul lato server sia sul lato client.

[La crittografia del servizio di archiviazione Azure](../storage/storage-service-encryption.md) (SSE) può crittografare automaticamente i dati prima che viene archiviato e lo decrittografa automaticamente quando si recuperano, rendendo hello elaborare completamente trasparente agli utenti. La crittografia del servizio di archiviazione utilizza 256 bit [crittografia AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), che fa parte di hello più forti crittografie a blocchi disponibili e gestisce la crittografia, decrittografia e la gestione delle chiavi in modo trasparente.

### <a name="client-side-encryption-of-azure-blobs"></a>Crittografia lato client di BLOB di Azure

La crittografia sul lato client di BLOB di Azure può essere eseguita in modi diversi.

È possibile utilizzare hello Azure Storage Client Library per dati tooencrypt del pacchetto NuGet .NET all'interno del toouploading precedente di applicazioni client tooAzure archiviazione.

toolearn ulteriori informazioni e download hello Azure Storage Client Library per il pacchetto NuGet di .NET, vedere il documento hello intitolato [8.3.0 di archiviazione Windows Azure](https://www.nuget.org/packages/WindowsAzure.Storage)

Quando si utilizza la crittografia lato client insieme di credenziali chiave di Azure, i dati vengono crittografati usando una singola simmetrica contenuto crittografia chiave (CEK) generato da hello Azure Storage client SDK. viene crittografato Hello CEK utilizzando una chiave di crittografia delle chiavi, che può essere una chiave simmetrica o una coppia di chiavi asimmetriche. È possibile gestirla in locale o archiviarla in Azure Key Vault. Hello dati crittografati viene quindi caricato tooAzure il servizio di archiviazione.

ulteriori informazioni sulla crittografia client-side insieme di credenziali chiave di Azure toolearn e Introduzione a come tooinstructions, vedere il documento hello intitolato [esercitazione: crittografare e decrittografare i BLOB in archiviazione di Microsoft Azure con l'insieme di credenziali chiave di Azure](../storage/storage-encrypt-decrypt-blobs-key-vault.md)

Infine, è possibile utilizzare anche hello Azure Storage Client Library per la crittografia di Java tooperform sul lato client prima di caricare dati tooAzure archiviazione e toodecrypt hello i dati durante il download di toohello client. Questa libreria supporta anche l'integrazione con [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) per la gestione delle chiavi dell'account di archiviazione.

### <a name="encryption-of-data-at-rest-with-azure-sql-database"></a>Crittografia dei dati inattivi con il database SQL di Azure

Il [database SQL di Azure](../sql-database/sql-database-technical-overview.md) è un servizio di database relazionale generico in Microsoft Azure che supporta strutture come dati relazionali, JSON, dati spaziali e XML. SQL Azure supporta la crittografia lato server tramite funzionalità Transparent Data Encryption (TDE) hello e crittografia lato client tramite funzionalità sempre crittografato hello.

#### <a name="transparent-data-encryption"></a>Transparent Data Encryption

[Crittografia dati trasparente TDE](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde) è usato tooencrypt [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016), [Database SQL di Azure](../sql-database/sql-database-technical-overview.md), e [Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) i file di dati in tempo reale, utilizzo di una chiave di crittografia del database (DEK), che viene archiviata nel record di avvio hello database per la disponibilità durante il ripristino.

La tecnologia TDE consente di proteggere i file di dati e di log usando gli algoritmi di crittografia AES e 3DES. La crittografia del file di database hello viene eseguita a livello di pagina hello; le pagine in un database crittografato Hello vengono crittografate prima di essere scritte toodisk e vengono decrittografate quando vengono letti in memoria. La tecnologia Transparent Data Encryption è ora abilitata per impostazione predefinita nei nuovi database SQL di Azure.

#### <a name="always-encrypted"></a>Always Encrypted

Hello [Always Encrypted](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine) funzionalità in SQL Azure consente tooencrypt dati all'interno di toostoring precedente di applicazioni client nel Database di SQL Azure e consente la delega tooenable di toothird di amministrazione di database locale parti e mantenere la separazione tra chi possiede e visualizzare dati hello e chi gestisce, ma non devono avere accesso tooit.

#### <a name="cellcolumn-level-encryption"></a>Crittografia a livello di colonna/cella (CLE)

Database SQL di Azure consente colonna tooa di crittografia simmetrica tooapply dei dati tramite Transact-SQL. Si tratta di [crittografia a livello di colonna o di crittografia a livello di cella](https://docs.microsoft.com/sql/relational-databases/security/encryption/encrypt-a-column-of-data) (CLE), poiché è possibile utilizzare il tooencrypt determinate colonne o celle anche specifiche dei dati con le chiavi di crittografia diversi. Ciò consente una funzionalità di crittografia più granulare rispetto alla crittografia Transparent Data Encryption che crittografa i dati in pagine.

CLE è disponibili funzioni predefinite che è possibile utilizzare tooencrypt dati utilizzando chiavi simmetriche o asimmetriche, con chiave pubblica di hello di un certificato o con una passphrase, usando 3DES.

### <a name="cosmos-db-database-encryption"></a>Crittografia del database Cosmos DB

[Azure Cosmos DB](../cosmos-db/database-encryption-at-rest.md) è il database multimodello distribuito a livello globale di Microsoft. Dati utente archiviati nel database Cosmos in memoria non volatile (unità SSD) vengono crittografati per impostazione predefinita. non esistono alcun tooturn controlli si attiva o disattiva. La crittografia dei dati inattivi viene implementata attraverso una serie di tecnologie di protezione, inclusi i sistemi di archiviazione protetta delle chiavi, le reti crittografate e le API di crittografia. Le chiavi di crittografia vengono gestite da Microsoft e ruotate in base alle linee guida interne di Microsoft.

### <a name="at-rest-encryption-in-azure-data-lake"></a>Crittografia di dati inattivi in Azure Data Lake

[Azure Data Lake](../data-lake-store/data-lake-store-encryption.md) è un repository di livello aziendale di ogni tipo di dati raccolti in una definizione formale di tooany precedente unica posizione di schema o i requisiti. Supporta l'archivio Azure Data Lake "in per impostazione predefinita," crittografia trasparente dei dati inattivi, impostato durante la creazione di hello del tuo account. Per impostazione predefinita, l'archivio Data Lake gestisce le chiavi di hello automaticamente, ma è necessario toomanage opzione hello li manualmente.

Vengono utilizzati tre tipi di chiavi di crittografia e decrittografia dei dati: hello chiave di crittografia Master (MEK), chiave DEK (Data Encryption) e chiave di crittografia di blocco (BEK). Hello MEK è usato tooencrypt hello chiave di Decrittografia, viene archiviato in un supporto permanente, e hello BEK è derivato da hello chiave di Decrittografia e il blocco di dati di hello. Se si siano gestendo le proprie chiavi, è possibile ruotare hello MEK.

## <a name="encryption-of-data-in-transit"></a>Crittografia dei dati in transito

Azure offre numerosi meccanismi per conservare i dati privati, durante il passaggio da una posizione tooanother.

### <a name="tlsssl-encryption-in-azure"></a>Crittografia TLS/SSL in Azure

Microsoft utilizza hello [Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) del protocollo dati tooprotect quando il trasferimento tra servizi cloud hello e clienti. Data center Microsoft negoziare una connessione TLS con i sistemi client che si connettono tooAzure servizi. Il protocollo TLS fornisce l'autenticazione avanzata, la riservatezza dei messaggi e l'integrità (abilitando il rilevamento di manomissioni, intercettazioni e falsificazioni di messaggi), l'interoperabilità, la flessibilità degli algoritmi, la facilità di distribuzione e di utilizzo.

[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) protegge le connessioni tra i sistemi client dei clienti e i servizi cloud di Microsoft con chiavi univoche. Le connessioni usano anche lunghezze di chiavi di crittografia basate a 2.048 bit basate su RSA. Questa combinazione rende difficile a qualcuno toointercept e accedere ai dati che sono in transito.

### <a name="azure-storage-transactions"></a>Transazioni di archiviazione di Azure

Quando si interagisce con l'archiviazione di Azure tramite il portale di Azure hello, tutte le transazioni si verificano tramite HTTPS. È anche possibile utilizzare hello API REST di archiviazione tramite HTTPS toointeract con archiviazione di Azure. È possibile applicare uso hello di HTTPS durante la chiamata di oggetti tooaccess API REST di hello negli account di archiviazione, consentendo il trasferimento protetto necessario per l'account di archiviazione hello.

Firme di accesso condiviso ([SAS](../storage/storage-dotnet-shared-access-signature-part-1.md)), che può essere utilizzato toodelegate accedere agli oggetti di archiviazione tooAzure, includono un'opzione toospecify tale hello solo quando si usano firme di accesso condiviso è possibile utilizzare il protocollo HTTPS. Ciò garantisce che qualsiasi utente sarà l'invio di collegamenti con i token di firma di accesso condiviso Usa protocollo corretto di hello.

[SMB 3.0](https://technet.microsoft.com/library/dn551363(v=ws.11).aspx#BKMK_SMBEncryption) utilizzati tooaccess condivisioni di File di Azure supporta la crittografia e disponibile in Windows Server 2012 R2, Windows 8, Windows 8.1 e Windows 10, che consente l'accesso tra più aree e anche accedere sul desktop hello.

Crittografia lato client Crittografa dati hello prima ha inviato tooAzure archiviazione, in modo che viene crittografato durante il trasferimento in rete hello.

### <a name="smb-encryption-over-azure-virtual-networks"></a>Crittografia SMB su reti virtuali di Azure 

[SMB 3.0](https://support.microsoft.com/help/2709568/new-smb-3-0-features-in-the-windows-server-2012-file-server) nelle macchine virtuali di Azure che esegue Windows Server 2012 e in precedenza si hello dati toomake possibilità i trasferimenti di proteggere la crittografia dei dati in transito su reti virtuali di Azure offre, attacchi di tooprotect manomissioni e l'intercettazione. Gli amministratori possono abilitare la crittografia SMB per hello intero server o condivisioni specifiche.

Per impostazione predefinita, dopo aver attivata la crittografia SMB per una condivisione o un server, solo i client SMB 3 consentiti tooaccess crittografato hello condivisioni.

## <a name="in-transit-encryption-in-azure-virtual-machines"></a>Crittografia di dati in transito in Macchine virtuali di Azure

Dati in transito to, from e tra le macchine virtuali di Azure che eseguono Windows vengono crittografati in diversi modi, a seconda della natura hello della connessione di hello.

### <a name="rdp-sessions"></a>Sessioni RDP

È possibile connettersi e accedere tooan macchina virtuale di Azure utilizzando hello [Remote Desktop Protocol](https://msdn.microsoft.com/library/aa383015(v=vs.85).aspx) (RDP) da un computer client Windows o da un Mac con un client RDP installati. I dati in transito sulla rete hello in sessioni RDP possono essere protetto da TLS.

È anche possibile utilizzare Desktop remoto tooconnect tooa VM Linux in Azure.

### <a name="secure-access-toolinux-vms-with-ssh"></a>Proteggere l'accesso alle macchine virtuali tooLinux con SSH

È possibile utilizzare [Secure Shell](../virtual-machines/linux/ssh-from-windows.md) tooLinux tooconnect (SSH) le macchine virtuali in esecuzione in Azure per la gestione remota. SSH è un protocollo per connessioni crittografate che consente accessi protetti su connessioni non sicure. È un protocollo di connessione predefinito hello per le macchine virtuali Linux ospitate in Azure. Utilizzando le chiavi SSH per l'autenticazione, distribuite hello per le password toolog in. SSH usa una coppia di chiavi pubblica/privata (asimmetrica) per l'autenticazione.

## <a name="azure-vpn-encryption"></a>Crittografia VPN di Azure

È possibile connettere tooAzure tramite una rete privata virtuale che crea l'informativa sulla privacy hello tooprotect tunnel sicuro dei dati di hello inviati attraverso la rete hello.

### <a name="azure-vpn-gateway"></a>Gateway VPN di Azure

[Gateway VPN di Azure](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md) possono essere utilizzati toosend crittografato il traffico tra la rete virtuale e il percorso locale attraverso una connessione pubblica o toosend il traffico tra reti virtuali.

La VPN da sito a sito usa [IPsec](https://en.wikipedia.org/wiki/IPsec) per la crittografia del trasporto. I gateway VPN di Azure usano un insieme di proposte predefinite. È possibile configurare i criteri IPsec/IKE personalizzati toouse gateway VPN di Azure con gli algoritmi di crittografia specifici e forza chiave, piuttosto che hello set di criteri predefinito di Azure.

### <a name="point-to-site-vpn"></a>VPN da punto a sito

Point-to-Site VPN consentono ai computer client singoli accedere tooan rete virtuale di Azure. [Hello Secure Socket Tunneling Protocol](https://technet.microsoft.com/library/2007.06.cableguy.aspx) (SSTP) è tunnel VPN di hello toocreate utilizzato e possono attraversare i firewall (tunnel hello viene visualizzato come una connessione HTTPS). È possibile usare la CA radice della PKI interna per la connettività Point-to-Site.

È possibile configurare una point-to-site VPN connessione tooa rete virtuale usando hello portale di Azure con l'autenticazione del certificato o PowerShell.

toolearn ulteriori informazioni su tooAzure di connessioni VPN point-to-site reti virtuali, vedere: [configurare un tooa connessione Point-to-Site rete virtuale utilizzando l'autenticazione di certificazione: portale di Azure](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md) e

[Configurare un tooa connessione Point-to-Site rete virtuale utilizzando l'autenticazione del certificato: PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="site-to-site-vpn"></a>Da sito a VPN 

Una connessione gateway VPN da sito a sito viene usato tooconnect tooan rete virtuale di Azure di rete locale tramite un tunnel VPN IPsec/IKE (IKEv1 o IKEv2). Questo tipo di connessione richiede un VPN dispositivo si trova in locale che dispone di un tooit di indirizzo IP pubblico accessibile pubblicamente.

È possibile configurare una sito a sito VPN connessione tooa rete virtuale utilizzando hello portale di Azure, PowerShell o hello Azure interfaccia della riga di comando (CLI).

Leggere qui per altre informazioni:

[Creare una connessione Site-to-Site nel portale di Azure hello](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

[Creare una connessione da sito a sito](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

[Creare una rete virtuale con una connessione VPN da sito a sito usando l'interfaccia della riga di comando](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="in-transit-encryption-in-azure-data-lake"></a>Crittografia di dati in transito in Azure Data Lake

Anche i dati in transito (noti anche come dati in movimento) vengono sempre crittografati in Data Lake Store. Inoltre supporto toopersistent toostoring precedenti dati tooencrypting hello dati vengono sempre anche protetti in transito tramite HTTPS. HTTPS è l'unico protocollo hello è supportato per hello che interfacce REST di archivio Data Lake.

toolearn più sulla crittografia dei dati in transito in Azure Data Lake, vedere il documento hello intitolato [crittografia dei dati in archivio Azure Data Lake.](../data-lake-store/data-lake-store-encryption.md)

## <a name="key-management-with-azure-key-vault"></a>Gestione delle chiavi con Azure Key Vault

Senza una corretta protezione dati e la gestione delle chiavi di hello, la crittografia è inutilizzabile. Insieme di credenziali chiave di Azure è la soluzione consigliata di Microsoft per gestire e controllare i tasti di scelta tooencryption utilizzati dai servizi cloud. Le chiavi tooaccess autorizzazioni possono essere assegnate tooservices o toousers tramite gli account di Azure Active Directory.

Insieme di credenziali chiave di Azure Elimina le organizzazioni di hello necessità tooconfigure, applicare la patch e gestire i moduli di protezione Hardware (HSM) e il software di gestione delle chiavi. Insieme di credenziali chiave di Azure, Microsoft non vede mai le chiavi e le applicazioni non dispone di accesso diretto toothem; si mantiene il controllo. È possibile anche importare o generare chiavi nei moduli di protezione hardware.

## <a name="next-steps"></a>Passaggi successivi

- [Panoramica della sicurezza in Azure](security-get-started-overview.md)
- [Panoramica della sicurezza di rete di Azure](security-network-overview.md)
- [Panoramica della sicurezza del database di Azure](azure-database-security-overview.md)
- [Informazioni generali sulla sicurezza di Macchine virtuali di Azure](security-virtual-machines-overview.md)
- [Crittografia dei dati inattivi](azure-security-encryption-atrest.md)
- [Procedure consigliate per la sicurezza e la crittografia dei dati](azure-security-data-encryption-best-practices.md)
