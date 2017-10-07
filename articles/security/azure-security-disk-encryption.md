---
title: Crittografia del disco per Windows e le macchine virtuali IaaS Linux aaaAzure | Documenti Microsoft
description: Questo articolo offre una panoramica di Crittografia dischi di Microsoft Azure per le VM IaaS Windows e Linux.
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a>Azure Disk Encryption per le macchine virtuali IaaS Windows e Linux
Microsoft Azure è attivamente impegnata tooensuring la privacy dei dati, sovranità dati e consente di Azure ospitati toocontrol dati attraverso una serie di tecnologie avanzate tooencrypt, controllare e gestire chiavi di crittografia, access control e controllo dei dati. In questo modo i clienti di Azure la soluzione hello flessibilità toochoose hello che meglio soddisfa le proprie esigenze aziendali. In questo articolo, si introdurrà tooa nuova soluzione "Crittografia del disco di Azure per Windows e di Linux IaaS VM" toohelp proteggere e salvaguardare i propri impegni di sicurezza e conformità organizzativi toomeet i dati. carta Hello fornisce indicazioni dettagliate su come toouse hello disco di Azure le funzionalità di crittografia inclusi hello supportato scenari e l'esperienza utente hello.

> [!NOTE]
> Alcune indicazioni possono comportare un maggior utilizzo delle risorse di calcolo, rete o dati con un conseguente aumento dei costi di licenza o sottoscrizione.

## <a name="overview"></a>Panoramica
Crittografia dischi di Azure è una nuova funzionalità che consente di crittografare i dischi delle macchine virtuali IaaS Windows e Linux. Crittografia disco Azure sfrutta standard di settore hello [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) funzionalità di Windows e hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) funzionalità di crittografia del volume tooprovide Linux per hello del sistema operativo e i dischi dati hello. soluzione hello è integrato con [insieme credenziali chiavi Azure](https://azure.microsoft.com/documentation/services/key-vault/) toohelp è controllare e gestire i segreti e tutte le chiavi di crittografia del disco hello nella sottoscrizione dell'insieme di credenziali chiave. soluzione Hello assicura anche che tutti i dati nei dischi di macchina virtuale hello vengono crittografati a riposo nell'archiviazione Azure.

Crittografia dischi di Azure per macchine virtuali IaaS Windows e Linux ha ora **disponibilità generale** in tutte le aree pubbliche e AzureGov di Azure per macchine virtuali standard e macchine virtuali con archiviazione Premium.

### <a name="encryption-scenarios"></a>Scenari di crittografia
Hello soluzioni di crittografia del disco di Azure supporta hello seguenti scenari:

* Abilitare la crittografia nelle nuove VM IaaS create da chiavi di crittografia e VHD pre-crittografati
* Abilitare la crittografia in nuove macchine virtuali IaaS create da immagini della raccolta di Azure hello è supportato
* Abilitare la crittografia in VM IaaS esistenti in esecuzione in Azure
* Disabilitare la crittografia nelle VM IaaS Windows
* Disabilitare la crittografia nelle unità dati per le VM IaaS Linux
* Abilitare la crittografia delle macchine virtuali con disco gestito
* Aggiornare le impostazioni di crittografia di una macchina virtuale non dotata di archiviazione Premium crittografata esistente
* Backup e ripristino di macchine virtuali crittografate con chiave di crittografia della chiave

soluzione Hello supporta hello seguenti scenari per le macchine virtuali IaaS quando sono abilitati in Microsoft Azure:

* Integrazione dell'insieme di credenziali delle chiavi di Azure.
* Macchine virtuali di livello Standard: [serie A, D, DS, G, GS, F e così via per VM IaaS](https://azure.microsoft.com/pricing/details/virtual-machines/)
* Abilitare la crittografia in Windows e le macchine virtuali IaaS di Linux e le macchine virtuali di disco gestito da hello supportate immagini della raccolta di Azure
* Disabilitare la crittografia nel sistema operativo e nelle unità dati per le macchine virtuali IaaS Windows e per le macchine virtuali con disco gestito
* Disabilitare la crittografia nelle unità dati per le macchine virtuali IaaS Linux e per le macchine virtuali con disco gestito
* Abilitare la crittografia in VM IaaS eseguite nel sistema operativo client Windows
* Abilitare la crittografia su volumi con percorsi di montaggio
* Abilitare la crittografia nelle macchine virtuali Linux configurate con striping del disco (RAID) tramite mdadm
* Abilitare la crittografia nelle macchine virtuali Linux usando LVM per i dischi dati
* Abilitare la crittografia nelle VM Windows configurate con spazi di archiviazione
* Aggiornare le impostazioni di crittografia di una macchina virtuale non dotata di archiviazione Premium crittografata esistente
* Sono supportate tutte le aree di Azure pubbliche e AzureGov

soluzione Hello non supporta hello seguenti scenari, le funzionalità e tecnologie:

* VM IaaS del piano Basic
* Disabilitazione della crittografia in un'unità del sistema operativo per le VM IaaS Linux
* La disabilitazione della crittografia in un'unità di dati se è crittografato hello unità del sistema operativo per le macchine virtuali Iaas di Linux
* Macchine virtuali IaaS che vengono creati utilizzando il metodo di creazione hello classico di VM
* La crittografia per le immagini personalizzate nelle macchine virtuali Windows e Linux IaaS NON è supportata. La crittografia in disco del sistema operativo di Linux LVM non è attualmente supportata. Questa compatibilità è di prossima integrazione.
* Integrazione con il servizio di gestione delle chiavi locale.
* File di Azure (file system condiviso), file system di rete (NFS, Network File System), volumi dinamici e macchine virtuali Windows configurate con sistemi RAID basati su software
* Backup e ripristino di macchine virtuali crittografate senza chiave di crittografia della chiave.
* Aggiornare le impostazioni di crittografia di una macchina virtuale con archiviazione Premium crittografata esistente.

> [!NOTE]
> Backup e ripristino di macchine virtuali crittografate è supportata solo per le macchine virtuali che vengono crittografate con la configurazione KEK hello. Non sono supportati nelle macchine virtuali crittografate senza chiave di crittografia della chiave. La chiave di crittografia della chiave è un parametro facoltativo che abilita la crittografia delle VM. Questo supporto sarà presto disponibile.
> L'aggiornamento delle impostazioni di crittografia di una macchina virtuale con archiviazione Premium crittografata esistente non è supportato. Questo supporto sarà presto disponibile.

### <a name="encryption-features"></a>Funzionalità di crittografia
Quando si abilita e distribuire la crittografia del disco di Azure per le macchine virtuali IaaS di Azure, hello seguenti funzionalità sono abilitate, a seconda della configurazione di hello fornita:

* Crittografia del volume del sistema operativo hello volume tooprotect hello avvio inattivi nell'archiviazione
* Crittografia dei dati volumi tooprotect hello volumi di dati inattivi nell'archiviazione
* La disabilitazione della crittografia in hello del sistema operativo e dati unità per le macchine virtuali IaaS di Windows
* La disabilitazione della crittografia dati hello unità per le macchine virtuali IaaS Linux (solo se OS unità non crittografata)
* Protezione delle chiavi di crittografia hello e segreti nella sottoscrizione dell'insieme di credenziali chiave
* La segnalazione dello stato di crittografia hello di hello crittografati VM IaaS
* Rimozione delle impostazioni di configurazione di crittografia del disco dalla macchina virtuale IaaS di hello
* Backup e ripristino di macchine virtuali crittografati utilizzando il servizio di Backup di Azure hello

> [!NOTE]
> Backup e ripristino di macchine virtuali crittografate è supportata solo per le macchine virtuali che vengono crittografate con la configurazione KEK hello. Non sono supportati nelle macchine virtuali crittografate senza chiave di crittografia della chiave. La chiave di crittografia della chiave è un parametro facoltativo che abilita la crittografia delle VM.

Crittografia dischi di Azure per macchine virtuali IaaS per soluzioni Windows e Linux include:

* estensione di crittografia del disco Hello per Windows.
* estensione di crittografia del disco Hello per Linux.
* cmdlet di PowerShell Hello crittografia del disco.
* Hello la crittografia del cmdlet di Azure interfaccia della riga di comando (CLI).
* modelli di Azure Resource Manager Hello crittografia del disco.

Hello soluzioni di crittografia del disco di Azure è supportata nelle macchine virtuali IaaS che eseguono Windows o del sistema operativo Linux. Per ulteriori informazioni sui sistemi operativi hello supportato, vedere hello "Prerequisiti" sezione.

> [!NOTE]
> Non è previsto alcun addebito aggiuntivo per la crittografia dei dischi delle macchine virtuali con Crittografia dischi di Azure.

### <a name="value-proposition"></a>Proposta di valore
Quando si applica la soluzione hello crittografia-Gestione disco di Azure, è possibile soddisfare hello esigenze aziendali seguenti:

* Le macchine virtuali IaaS sono protette a rest, poiché è possibile utilizzare la crittografia standard del settore tecnologia tooaddress sicurezza e conformità i requisiti organizzativi.
* Le macchine virtuali IaaS vengono avviate con chiavi e criteri controllati dai clienti ed è possibile controllarne l'utilizzo nell'insieme di credenziali delle chiavi.

### <a name="encryption-workflow"></a>Flusso di lavoro della crittografia
crittografia disco tooenable per Windows e le macchine virtuali Linux, hello seguenti:

1. Scegliere uno scenario di crittografia tra hello precedente gli scenari di crittografia.
2. Crittografia disco tooenabling tramite il modello di gestione risorse di Azure disco crittografia hello, i cmdlet di PowerShell o il comando CLI di partecipare e specificare la configurazione di crittografia hello.

   * Per uno scenario VHD cliente crittografato hello, caricare l'account di archiviazione tooyour VHD crittografato hello e hello crittografia chiave tooyour materiale chiave dell'insieme di credenziali. Quindi, è possibile fornire hello crittografia configurazione tooenable crittografia in una nuova VM IaaS.
   * Per nuove macchine virtuali create da hello Marketplace e le macchine virtuali esistenti che sono già in esecuzione in Azure, fornire la crittografia tooenable configurazione di crittografia hello in hello VM IaaS.

3. Concedere accesso toohello piattaforma Azure tooread hello chiave di crittografia materiale (chiavi di crittografia di BitLocker per i sistemi Windows) e la Passphrase per Linux dalla crittografia di tooenable insieme di credenziali delle chiavi in hello VM IaaS.

4. Fornire hello Azure Active Directory (Azure AD) dell'applicazione identità toowrite hello crittografia chiave tooyour materiale chiave dell'insieme di credenziali. In questo modo viene abilitata la crittografia su hello VM IaaS per gli scenari di hello descritti nel passaggio 2.

5. Azure Aggiorna modello del servizio VM hello con la crittografia e la configurazione dell'insieme di credenziali chiave hello e imposta le VM crittografate.

 ![Microsoft Antimalware in Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a>Flusso di lavoro della decrittografia
crittografia del disco toodisable per le macchine virtuali IaaS, hello completo seguendo i passaggi generali:

1. Scegliere crittografia toodisable (decrittografia) in una VM IaaS in esecuzione in Azure tramite il modello di gestione risorse di Azure disco crittografia hello o i cmdlet di PowerShell e specificare la configurazione di decrittografia hello.

 Questo passaggio consente di disattivare la crittografia del volume di dati del sistema operativo o hello hello o entrambi in esecuzione la macchina virtuale IaaS Windows hello. Tuttavia, come indicato nella sezione precedente di hello, la disabilitazione della crittografia del disco del sistema operativo per Linux non è supportata. passaggio di decrittografia Hello è consentito solo per le unità dati le macchine virtuali Linux come disco del sistema operativo hello non è crittografato.
2. Gli aggiornamenti di Azure hello modello di macchina virtuale del servizio e VM IaaS hello è contrassegnato decrittografata. contenuto Hello di hello VM non venga crittografati a riposo.

> [!NOTE]
> operazione di disabilitazione crittografia Hello non elimina il materiale della chiave dell'insieme di credenziali e hello crittografia chiave (chiavi di crittografia di BitLocker per i sistemi Windows) o la Passphrase per Linux.
 > La disabilitazione della crittografica del disco del sistema operativo per Linux non è supportata. passaggio di decrittografia Hello è consentito solo per le unità dati le macchine virtuali Linux.
La disabilitazione della crittografia del disco dati per Linux non è supportata se è crittografato hello unità del sistema operativo.

## <a name="prerequisites"></a>Prerequisiti
Prima di abilitare la crittografia del disco di Azure nelle macchine virtuali IaaS di Azure per gli scenari supportato hello illustrati nella sezione "Overview" hello, vedere hello seguenti prerequisiti:

* È necessario disporre le risorse toocreate una sottoscrizione Azure attiva valida in Azure in aree hello è supportato.
* Crittografia disco Azure è supportata in hello seguenti versioni di Windows Server: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016.
* Crittografia di disco di Azure è supportata nelle seguenti versioni di client Windows hello: il client di Windows 10 e Windows 8.

> [!NOTE]
> Per Windows Server 2008 R2 è necessario che .NET Framework 4.5 sia installato prima dell'abilitazione della crittografia in Azure. È possibile installare da Windows Update per l'installazione dell'aggiornamento facoltativo hello Microsoft .NET Framework 4.5.2 per sistemi basati su x64 di Windows Server 2008 R2 ([KB2901983](https://support.microsoft.com/kb/2901983)).

* Crittografia disco Azure è supportata in hello seguente raccolta di Azure basato su distribuzioni di server Linux e le versioni:

| Distribuzione Linux | Versione | Tipo di volume supportato per la crittografia|
| --- | --- |--- |
| Ubuntu | 16.04-DAILY-LTS | Disco del sistema operativo e dati |
| Ubuntu | 14.04.5-DAILY-LTS | Disco del sistema operativo e dati |
| Ubuntu | 12.10 | Disco dati |
| Ubuntu | 12.04 | Disco dati |
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
| SLES | 12-SP1 (Premium) | Disco dati |
| SLES | HPC 12 | Disco dati |
| SLES | 11-SP4 (Premium) | Disco dati |
| SLES | 11 SP4 | Disco dati |

* Crittografia disco Azure richiede che l'insieme di credenziali chiave e le macchine virtuali si trovino in hello stessa regione di Azure e di sottoscrizione.

> [!NOTE]
> Configurazione delle risorse hello in aree separate provoca un errore nell'attivazione di funzionalità di crittografia del disco Azure hello.

* tooset configurato e configurare l'insieme di credenziali chiave di crittografia del disco di Azure, vedere sezione **impostare e configurare l'insieme di credenziali chiave di crittografia del disco Azure** in hello *prerequisiti* sezione di questo articolo.
* tooset configurato e configurare l'applicazione Azure AD in Azure Active directory per la crittografia del disco di Azure, vedere sezione **configurare un'applicazione hello Azure AD in Azure Active Directory** in hello *prerequisiti* sezione di questo articolo.
* tooset configurato e configurare criteri di accesso hello chiave dell'insieme di credenziali per un'applicazione hello Azure AD, nella sezione **impostare i criteri di accesso hello chiave dell'insieme di credenziali per un'applicazione hello Azure AD** in hello *prerequisiti* sezione In questo articolo.
* Nella sezione tooprepare un VHD di Windows pre-crittografato, **preparare un disco rigido virtuale di Windows pre-crittografato** in hello *appendice*.
* Nella sezione tooprepare un VHD Linux pre-crittografato, **preparare un VHD Linux pre-crittografato** in hello *appendice*.
* Hello piattaforma Azure necessita di chiavi di crittografia toohello di accesso o i segreti nel toomake insieme di credenziali chiave li macchina virtuale di toohello disponibili quando viene avviato e decrittografa il volume di macchina virtuale del sistema operativo hello. piattaforma tooAzure toogrant autorizzazioni set hello **EnabledForDiskEncryption** proprietà nell'insieme di credenziali chiave hello. Per ulteriori informazioni, vedere **impostare e configurare l'insieme di credenziali chiave di crittografia del disco Azure** in hello appendice.
* È necessario applicare il controllo delle versioni agli URL del segreto dell'insieme di credenziali delle chiavi e della chiave di crittografia della chiave. Azure applica questa restrizione relativa al controllo delle versioni. Per privata valida e KEK URL, vedere hello seguono esempi:

  * Esempio di URL segreto valido: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*
  * Esempio di URL della chiave di crittografia della chiave valido: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*

* Crittografia dischi di Azure non supporta la possibilità di specificare i numeri di porta come parte dei segreti dell'insieme di credenziali delle chiavi e degli URL della chiave di crittografia della chiave. Per esempi di URL di credenziali di chiave supportati e non supportati, vedere esempio hello:

  * URL dell'insieme di credenziali delle chiavi non accettabile: *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*
  * URL dell'insieme di credenziali delle chiavi accettabile: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*

* funzionalità di crittografia del disco Azure hello tooenable, hello le macchine virtuali IaaS deve soddisfare hello seguendo i requisiti di configurazione di endpoint di rete:
  * un token tooconnect tooyour chiave insieme di credenziali, hello VM IaaS tooget deve essere in grado di tooconnect endpoint di Azure Active Directory tooan, \[login.microsoftonline.com\].
  * toowrite hello crittografia chiavi tooyour chiave dell'insieme di credenziali, hello VM IaaS, deve essere in grado di tooconnect toohello chiave dell'insieme di credenziali endpoint.
  * Hello VM IaaS, deve essere in grado di tooconnect tooan archiviazione di Azure endpoint che ospita hello repository estensioni di Azure e un account di archiviazione di Azure che ospita hello file VHD.

  > [!NOTE]
  > Se i criteri di protezione limitano l'accesso da macchine virtuali di Azure toohello Internet, è possibile risolvere l'URI precedente hello e configurare un toohello di connettività in uscita tooallow regola specifica gli indirizzi IP.
  >
  >tooconfigure e accesso insieme credenziali chiavi Azure dietro un firewall (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)

* Utilizzare hello la versione più recente di Azure PowerShell SDK versione tooconfigure crittografia del disco di Azure. Scaricare una versione più recente di hello di [versione di Azure PowerShell](https://github.com/Azure/azure-powershell/releases)

 > [!NOTE]
  > Crittografia dischi di Azure non è supportata in [Azure PowerShell SDK versione 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016). Se si riceve un errore correlato toousing Azure PowerShell 1.1.0, vedere [tooAzure errore correlate di Azure disco crittografia PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).

* toorun qualsiasi comando CLI di Azure e associarlo a una sottoscrizione di Azure, è necessario installare prima CLI di Azure:
  * tooinstall CLI di Azure e associarlo a una sottoscrizione di Azure, vedere [come tooinstall e configurare Azure CLI](../cli-install-nodejs.md).
  * toouse CLI di Azure per Mac, Linux e Windows con Gestione risorse di Azure, vedere [i comandi CLI di Azure in modalità di gestione risorse](../virtual-machines/azure-cli-arm-commands.md).

* Quando la crittografia di un disco gestito, è obbligatorio tootake prerequisiti uno snapshot del disco hello gestito o un backup del disco hello di fuori di crittografia precedente tooenabling di crittografia del disco di Azure.  Senza un backup sul posto, qualsiasi errore imprevisto durante la crittografia potrebbe rendere impossibile disco hello e VM accessibili senza un'opzione di ripristino.  Set-AzureRmVMDiskEncryptionExtension attualmente non eseguire il backup di dischi gestiti e genereranno un errore in cui viene eseguito un disco gestito, a meno che non è stato specificato il parametro - skipVmBackup hello.  Questo parametro è unsafe toouse a meno che non è di fuori di crittografia del disco di Azure è già stata effettuata una copia di backup.   Quando viene specificato il parametro - skipVmBackup hello, hello cmdlet verrà non eseguire il backup di hello gestito disco precedente tooencryption.  Per questo motivo, viene considerato un toomake prerequisito obbligatorio che un backup del disco di hello gestito che macchina virtuale sia in posizione precedente tooenabling Azure crittografia del disco nel caso in cui è successivo ripristino necessari.  
> [!NOTE]
 > parametro - skipVmBackup Hello non deve mai essere utilizzata a meno che un backup o dello snapshot è già stato effettuato di fuori di crittografia del disco di Azure. 

* Hello soluzioni di crittografia del disco di Azure Usa protezione con chiave esterna di hello BitLocker per le macchine virtuali IaaS di Windows. Per le macchine virtuali sono aggiunte a un dominio, NON eseguire il push di criteri di gruppo che applichino protezioni TPM. Per informazioni sui criteri di gruppo hello "Consenti BitLocker senza un TPM compatibile", vedere [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).
* Criteri di BitLocker nelle macchine virtuali appartenenti a un dominio con criteri di gruppo personalizzato devono includere hello seguente impostazione: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` crittografia del disco di Azure avrà esito negativo quando le impostazioni di criteri di gruppo personalizzato per Bitlocker sono incompatibili. Nei computer che non disponevano di hello corretta impostazione di criteri di applicare i nuovi criteri hello, imponendo hello nuovi criteri tooupdate (gpupdate.exe /force) e il riavvio potrebbe essere necessario.  
* toocreate un'applicazione Azure AD, creare un insieme di credenziali chiave, o configurare un insieme di credenziali chiave esistente e attivare la crittografia, vedere hello [script di PowerShell dei prerequisiti di crittografia del disco di Azure](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
* prerequisiti di crittografia del disco tooconfigure utilizzando hello CLI di Azure, vedere [questo script Bash](https://github.com/ejarvi/ade-cli-getting-started).
* toouse hello Azure Backup service tooback backup e ripristino crittografato le macchine virtuali, quando è abilitata la crittografia con la crittografia del disco di Azure, crittografano le macchine virtuali tramite la configurazione della chiave di crittografia del disco Azure hello. Hello servizio di Backup supporta le macchine virtuali che vengono crittografate utilizzando solo la configurazione KEK. Vedere [la modalità di crittografia delle macchine virtuali con la crittografia di Backup di Azure tooback backup e ripristino](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).

* Per la crittografia di un volume del sistema operativo Linux, riavviare una macchina virtuale è attualmente necessaria alla fine di hello del processo di hello. Questa operazione può essere eseguita tramite il portale di hello, powershell o CLI.   stato di hello tootrack della crittografia, eseguire periodicamente il polling il messaggio di stato hello restituito da Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.  Una volta completata la crittografia, messaggio di stato hello hello restituito da questo comando indicherà questo.  Ad esempio, "ProgressMessage: disco del sistema operativo sono state crittografate, riavviare hello VM" in questo punto di hello VM può essere riavviato e utilizzato.  

* Crittografia disco Azure per Linux richiede dati dischi toohave un file system montato in Linux precedenti tooencryption

* In modo ricorsivo i dischi montati dati non supportati da hello crittografia del disco di Azure per Linux. Ad esempio, se hello sistema di destinazione è montato un disco in /foo/bar e quindi un'altra in /foo/bar/baz, crittografia hello di /foo/bar/baz avrà esito positivo, ma la crittografia di foo/barra avrà esito negativo. 

* Crittografia disco Azure è supportata solo su immagini della raccolta di Azure supportata che soddisfano i prerequisiti di hello menzionati in precedenza. Immagini personalizzate di clienti non sono supportate a causa di toocustom gli schemi di partizione e i comportamenti di processo che potrebbero esistere in queste immagini. Inoltre, potrebbero risultare incompatibili anche le macchine virtuali basate su immagini della raccolta che inizialmente soddisfacevano i prerequisiti ma che sono state modificate dopo la creazione.  Per che motivo, hello suggerito procedure per la crittografia di una VM Linux toostart da un'immagine della raccolta pulita, crittografare hello VM e aggiungere software personalizzato o dati toohello macchina virtuale in base alle esigenze.  

> [!NOTE]
> Backup e ripristino di macchine virtuali crittografate è supportata solo per le macchine virtuali che vengono crittografate con la configurazione KEK hello. Non sono supportati nelle macchine virtuali crittografate senza chiave di crittografia della chiave. La chiave di crittografia della chiave è un parametro facoltativo che abilita la macchina virtuale.

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a>Impostare hello applicazione Azure AD in Azure Active Directory
Quando è necessario toobe crittografia abilitata in una macchina virtuale in esecuzione in Azure, la crittografia del disco di Azure genera e scrive hello crittografia chiavi tooyour chiave dell'insieme di credenziali. La gestione delle chiavi di crittografia nell'insieme di credenziali delle chiavi richiede l'autenticazione di Azure AD.

Creare quindi un'applicazione Azure AD per questo scopo. È possibile trovare i passaggi dettagliati per la registrazione di un'applicazione nella sezione "Ottenere un'identità per hello applicazione" hello del post di blog hello [insieme credenziali chiavi Azure - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx). Questo post include anche alcuni esempi utili per l'installazione e la configurazione dell'insieme di credenziali delle chiavi. Ai fini dell'autenticazione, è possibile usare l'autenticazione basata sul segreto client o l'autenticazione di Azure AD basata sul certificato client.

#### <a name="client-secret-based-authentication-for-azure-ad"></a>Autenticazione basata su segreto client per Azure AD
Nelle sezioni Hello che seguono consentono di configurare un'autenticazione client basata su chiave privata per Azure AD.

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a>Creare un'applicazione Azure AD usando Azure PowerShell
Utilizzare hello seguente cmdlet di PowerShell toocreate un'applicazione Azure AD:

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> $azureAdApplication.ApplicationId è hello AD ClientID Azure e $aadClientSecret è privata hello del client che è necessario utilizzare tooenable successiva crittografia del disco di Azure. Proteggere la chiave privata client hello Azure AD in modo appropriato.

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a>Configurare Azure AD hello client ID e il segreto dal portale di Azure classico hello
È possibile anche impostare l'ID client di Azure AD e il segreto tramite hello [portale di Azure classico]( https://manage.windowsazure.com). tooperform questa attività, hello seguenti:

1. Fare clic su hello **Active Directory** scheda.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. Fare clic su **Aggiungi applicazione**e quindi nome dell'applicazione hello tipo.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. Fare clic sul pulsante freccia hello e quindi configurare le proprietà dell'applicazione hello.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. Fare clic su hello segno di spunta in hello inferiore sinistro toofinish. verrà visualizzata la pagina di configurazione dell'applicazione Hello e ID client di Azure AD hello viene visualizzato nella parte inferiore di hello della pagina hello.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. Salvare la chiave privata client hello Azure AD, scegliendo hello **salvare** pulsante. Si noti segreto client hello Azure AD nella casella di testo hello chiavi. Proteggerlo correttamente.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > Hello che precedono il flusso non è supportata nel portale di Azure classico hello.

##### <a name="use-an-existing-application"></a>Usare un'applicazione esistente
tooexecute hello i comandi seguenti, ottenere e usare hello [modulo Azure AD PowerShell](https://technet.microsoft.com/library/jj151815.aspx).

> [!NOTE]
> Hello comandi seguenti devono essere eseguiti da una nuova finestra di PowerShell. Non usare Azure PowerShell o comandi di hello Azure Resource Manager finestra tooexecute hello. Questo approccio è consigliato poiché questi cmdlet nel modulo di MSOnline hello o Azure AD PowerShell.

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a>Autenticazione basata su certificato per Azure AD
> [!NOTE]
> L'autenticazione basata su certificato per Azure AD non è attualmente supportata nelle VM Linux.

Hello nelle sezioni che seguono Mostra come tooconfigure un'autenticazione basata su certificati per Azure AD.

##### <a name="create-an-azure-ad-application"></a>Creare un'applicazione Azure AD
toocreate un'applicazione Azure AD, eseguire hello i cmdlet di PowerShell seguente:

> [!NOTE]
> Sostituire segue hello `yourpassword` stringa con la password sicura e la password di hello misura di sicurezza.

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

Dopo aver completato questo passaggio, caricare un file PFX file tooyour chiave dell'insieme di credenziali e abilitare hello accesso criteri necessari toodeploy che tooa certificato macchina virtuale.

##### <a name="use-an-existing-azure-ad-application"></a>Usare un'applicazione Azure AD esistente
Se si configura l'autenticazione basata su certificati per un'applicazione esistente, utilizzare i cmdlet di PowerShell hello illustrati di seguito. Essere tooexecute che di una nuova finestra di PowerShell.

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

Dopo aver completato questo passaggio, caricare un file PFX file tooyour chiave dell'insieme di credenziali e abilitare i criteri di accesso hello sono sufficiente toodeploy hello certificato tooa macchina virtuale.

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a>Caricare un file PFX file tooyour chiave dell'insieme di credenziali
Per una spiegazione dettagliata di questo processo, vedere [hello Blog del Team dell'insieme di credenziali chiave di Azure ufficiale](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx). Hello seguendo i cmdlet di PowerShell è, tuttavia, è sufficiente per l'attività hello. Essere tooexecute che essi dalla console di Azure PowerShell.

> [!NOTE]
> Sostituire segue hello `yourpassword` stringa con la password sicura e la password di hello misura di sicurezza.

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a>Distribuire un certificato di tooan l'insieme di credenziali chiave macchina virtuale esistente
Dopo aver completato il caricamento di hello PFX, è possibile distribuire un certificato in hello insieme di credenziali chiave tooan esistente VM con seguenti hello:
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a>Impostare i criteri di accesso hello chiave dell'insieme di credenziali per un'applicazione hello Azure AD
L'applicazione Azure AD richiede le chiavi di hello tooaccess diritti o i segreti nell'insieme di credenziali hello. Hello utilizzare [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant autorizzazioni toohello dell'applicazione, utilizzando l'ID client hello (che è stato generato quando è stata registrata un'applicazione hello) come hello _– ServicePrincipalName_ valore del parametro. toolearn informazioni, vedere hello post di blog [insieme credenziali chiavi Azure - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx). Di seguito è riportato un esempio di come tooperform questa attività tramite PowerShell:

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> Crittografia disco Azure richiede hello tooconfigure dopo l'applicazione client tooyour AD Azure i criteri di accesso: _WrapKey_ e _impostare_ autorizzazioni.

## <a name="terminology"></a>Terminologia
toounderstand alcuni dei termini comuni hello utilizzati da questa tecnologia, utilizzare hello terminologia nella tabella seguente:

| Terminologia | Definizione |
| --- | --- |
| Azure AD | Azure AD è l'abbreviazione di [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/). Un account Azure AD è un prerequisito per le operazioni di autenticazione, archiviazione e recupero dei segreti da un insieme di credenziali delle chiavi. |
| Azure Key Vault | Key Vault è un servizio di crittografia e gestione delle chiavi basato su moduli di sicurezza hardware convalidati dagli standard FIPS (Federal Information Processing Standards), che consentono di proteggere le chiavi crittografiche e i segreti sensibili. Per altre informazioni, vedere la documentazione di [Key Vault](https://azure.microsoft.com/services/key-vault/). |
| ARM | Gestione risorse di Azure |
| BitLocker |[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) è una riconosciuto dal settore Windows volume tecnologia di crittografia utilizzato tooenable crittografia del disco nelle macchine virtuali IaaS di Windows. |
| BEK | Le chiavi di crittografia di BitLocker sono volumi di dati e il volume di avvio utilizzati tooencrypt hello del sistema operativo. le chiavi BitLocker Hello siano protette in un insieme di credenziali chiave come segreti. |
| CLI | Vedere [Interfaccia della riga di comando di Azure](../cli-install-nodejs.md). |
| DM-Crypt |[DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) è il sottosistema di crittografia del disco basati su Linux, trasparente hello utilizzati di crittografia del disco tooenable nelle macchine virtuali IaaS di Linux. |
| KEK | Chiave di crittografia è hello chiave asimmetrica (RSA 2048) che è possibile utilizzare tooprotect o eseguire il wrapping segreto hello. È possibile fornire una chiave protetta tramite modulo di protezione hardware o una chiave protetta tramite software. Per altre informazioni, vedere la documentazione di [Azure Key Vault](https://azure.microsoft.com/services/key-vault/). |
| Cmdlet PS | Vedere [Azure PowerShell cmdlets](/powershell/azure/overview) (Cmdlet di Azure PowerShell). |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a>Installare e configurare l'insieme di credenziali delle chiavi per Crittografia dischi di Azure
Crittografia disco Azure consente di salvaguardare hello disco crittografia chiavi e segreti nell'insieme di credenziali chiave. tooset di credenziali delle chiavi di crittografia del disco di Azure, hello completato i passaggi in ognuna delle seguenti sezioni hello.

#### <a name="create-a-key-vault"></a>Creare un insieme di credenziali delle chiavi
toocreate un insieme di credenziali chiave, utilizzare uno dei hello le opzioni seguenti:

* [Modello di Resource Manager "101-Key-Vault-Create"](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [Azure PowerShell key vault cmdlets](/powershell/module/azurerm.keyvault/#key_vault) (Cmdlet dell'insieme di credenziali delle chiavi di Azure PowerShell)
* Gestione risorse di Azure
* Come troppo[proteggere credenziali delle chiavi](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)

> [!NOTE]
> Se un insieme di credenziali chiave è già configurato per la sottoscrizione, è possibile ignorare toohello nella sezione successiva.

![Insieme di credenziali chiave Azure](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a>Configurare una chiave di crittografia della chiave (facoltativo)
Se si desidera toouse una chiave di scambio delle CHIAVI per un ulteriore livello di protezione per le chiavi di crittografia BitLocker hello, aggiungere un insieme di credenziali chiave di KEK tooyour. Hello utilizzare [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) toocreate cmdlet una chiave di crittografia della chiave nell'insieme di credenziali chiave hello. È anche possibile importare una chiave di crittografia della chiave dal modulo di protezione hardware di gestione delle chiavi locale. Per altre informazioni, vedere la [Documentazione su Key Vault](https://azure.microsoft.com/documentation/services/key-vault/).

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

È possibile aggiungere hello KEK passando tooAzure Resource Manager o tramite l'interfaccia dell'insieme di credenziali chiave.

![Insieme di credenziali chiave Azure](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a>Configurare le autorizzazioni dell'insieme di credenziali delle chiavi
Hello piattaforma Azure necessita di chiavi di crittografia toohello di accesso o i segreti nel toomake insieme di credenziali chiave li toohello disponibile macchina virtuale per l'avvio e la decrittografia dei volumi hello. toogrant autorizzazioni toohello piattaforma Azure, hello set **EnabledForDiskEncryption** insieme di credenziali delle proprietà nella chiave hello tramite cmdlet di PowerShell hello insieme di credenziali delle chiavi:

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

È inoltre possibile impostare hello **EnabledForDiskEncryption** proprietà visitando hello [Esplora inventario risorse di Azure](https://resources.azure.com).

Come accennato in precedenza, è necessario impostare hello **EnabledForDiskEncryption** proprietà credenziali delle chiavi. In caso contrario, la distribuzione di hello non riuscirà.

È possibile impostare i criteri di accesso per l'applicazione Azure AD dall'interfaccia di insieme di credenziali chiave hello, come illustrato di seguito:

![Insieme di credenziali chiave Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Insieme di credenziali chiave Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

In hello **criteri di accesso avanzato** scheda, assicurarsi che l'insieme di credenziali chiave è abilitata per la crittografia del disco di Azure:

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a>Scenari di distribuzione della crittografia dei dischi ed esperienze utente
È possibile abilitare molti scenari di crittografia del disco e passaggi hello possono variare in base uno scenario toohello. Hello nelle sezioni seguenti riguardano scenari hello in maggiore dettaglio.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a>Abilitare la crittografia in nuove macchine virtuali IaaS creati da hello Marketplace
È possibile abilitare la crittografia del disco nella nuova macchina virtuale Windows IaaS da hello Marketplace in Azure utilizzando hello [modello di gestione risorse](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).

1. Nel modello hello avvio rapido di Azure, fare clic su **distribuire tooAzure**, immettere la configurazione di crittografia hello hello **parametri** blade e quindi fare clic su **OK**.

2. Selezionare una sottoscrizione hello, gruppo di risorse, percorso del gruppo di risorse, legali e contratto e quindi fare clic su **crea** tooenable crittografia in una nuova VM IaaS.

> [!NOTE]
> Questo modello consente di creare un nuovo crittografati macchina virtuale di Windows che usa l'immagine della raccolta hello Windows Server 2012.

È possibile abilitare la crittografia dei dischi in una nuova macchina virtuale IaaS RedHat Linux 7.2 con una matrice RAID-0 da 200 GB usando questo modello di [Resource Manager](https://aka.ms/fde-rhel). Dopo aver distribuito il modello di hello, verificare lo stato di crittografia di hello VM utilizzando hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet, come descritto in [unità la crittografia del sistema operativo in una VM Linux in esecuzione](#encrypting-os-drive-on-a-running-linux-vm). Quando viene restituito lo stato della macchina hello _VMRestartPending_, riavviare hello macchina virtuale.

Hello nella tabella seguente sono elencati i parametri del modello di gestione risorse hello per nuove macchine virtuali da uno scenario di Marketplace hello usando un ID client di Azure AD:

| . | Descrizione |
| --- | --- |
| adminUserName | Nome utente di amministratore per la macchina virtuale hello. |
| adminPassword | Password dell'utente amministratore per la macchina virtuale hello. |
| newStorageAccountName | Nome del toostore di account di archiviazione hello del sistema operativo e dischi rigidi virtuali dati. |
| vmSize | Dimensioni della VM hello. Attualmente sono supportate solo le serie A, D e G Standard. |
| virtualNetworkName | Nome della rete virtuale che hello NIC VM hello deve appartenere allo. |
| subnetName | Nome della subnet hello nella rete virtuale che hello NIC VM hello deve appartenere allo. |
| AADClientID | ID client dell'applicazione hello Azure AD che dispone di autorizzazioni toowrite segreti tooyour chiave dell'insieme di credenziali. |
| AADClientSecret | Segreto client dell'applicazione hello Azure AD che dispone di autorizzazioni toowrite segreti tooyour chiave dell'insieme di credenziali. |
| keyVaultURL | URL della chiave hello insieme di credenziali di tale chiave deve essere caricata a BitLocker hello. È possibile ottenerlo utilizzando cmdlet hello `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`. |
| keyEncryptionKeyURL | URL della chiave di crittografia della chiave hello che è usato tooencrypt hello generato chiave BitLocker (facoltativa). |
| keyVaultResourceGroup | Gruppo di risorse dell'insieme di credenziali chiave hello. |
| vmName | Nome della macchina virtuale che hello l'operazione di crittografia hello è toobe eseguiti. |

> [!NOTE]
> _KeyEncryptionKeyURL_ è un parametro facoltativo. È possibile portare la propria KEK toofurther salvaguardia hello dati chiave di crittografia (Passphrase segreto) nell'insieme di credenziali chiave.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a>Abilitare la crittografia delle nuove VM IaaS create da chiavi di crittografia e dischi rigidi virtuali crittografati dei clienti
In questo scenario, è possibile abilitare la crittografia utilizzando il modello di gestione risorse di hello, i cmdlet di PowerShell o i comandi CLI. Hello nelle sezioni seguenti illustrano nel modello di gestione risorse di maggiore dettaglio hello e i comandi CLI.

Seguire le istruzioni di hello da una di queste sezioni per preparare immagini pre-crittografate che possono essere usate in Azure. Dopo aver creato l'immagine di hello, è possibile utilizzare i passaggi di hello in hello successiva sezione toocreate una macchina virtuale Azure crittografati.

* [Preparare un disco rigido virtuale Windows pre-crittografato](#preparing-a-pre-encrypted-windows-vhd)
* [Preparare un disco rigido virtuale Linux pre-crittografato](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a>Utilizzando il modello di gestione risorse di hello
È possibile abilitare crittografia del disco in disco rigido virtuale crittografato utilizzando hello [modello di gestione risorse](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).

1. Nel modello hello avvio rapido di Azure, fare clic su **distribuire tooAzure**, immettere la configurazione di crittografia hello hello **parametri** blade e quindi fare clic su **OK**.

2. Selezionare una sottoscrizione hello, gruppo di risorse, percorso del gruppo di risorse, legali e contratto e quindi fare clic su **crea** crittografia tooenable in hello nuova VM IaaS.

Hello nella tabella seguente elenca i parametri del modello di gestione risorse hello per il disco rigido virtuale crittografato:

| . | Descrizione |
| --- | --- |
| newStorageAccountName | Nome di hello toostore di hello storage account crittografati disco rigido virtuale del sistema operativo. Questo account di archiviazione deve già stato creato in hello stesso gruppo di risorse e la stessa posizione come hello macchina virtuale. |
| osVhdUri | URI del disco rigido virtuale del sistema operativo di hello dall'account di archiviazione hello. |
| osType | Tipo di prodotto del sistema operativo (Windows/Linux). |
| virtualNetworkName | Nome della rete virtuale che hello NIC VM hello deve appartenere allo. Hello nome debba sono già stato creato in hello stesso gruppo di risorse e la stessa posizione come hello macchina virtuale. |
| subnetName | Nome della subnet hello nella rete virtuale che hello NIC VM hello deve appartenere allo. |
| vmSize | Dimensioni della VM hello. Attualmente sono supportate solo le serie A, D e G Standard. |
| keyVaultResourceID | Hello ResourceID che identifica una risorsa dell'insieme di credenziali chiave hello in Gestione risorse di Azure. È possibile ottenere tramite i cmdlet di PowerShell hello `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`. |
| keyVaultSecretUrl | URL della chiave di crittografia del disco hello impostato nell'insieme di credenziali chiave hello. |
| keyVaultKekUrl | URL della chiave di crittografia della chiave hello per crittografare una chiave di crittografia del disco hello generato. |
| vmName | Nome di hello VM IaaS. |

#### <a name="using-powershell-cmdlets"></a>Usare i cmdlet PowerShell
È possibile abilitare crittografia del disco in disco rigido virtuale crittografato tramite i cmdlet di PowerShell hello [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).  

#### <a name="using-cli-commands"></a>Uso dei comandi dell'interfaccia della riga di comando
crittografia disco tooenable per questo scenario utilizzando i comandi CLI, hello seguenti:

1. Impostare criteri di accesso per l'insieme di credenziali delle chiavi:

   * Set hello **EnabledForDiskEncryption** flag:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * Impostare le autorizzazioni tooAzure AD applicazione toowrite segreti tooyour chiave dell'insieme di credenziali:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. crittografia tooenable in una macchina virtuale esistente o in esecuzione, tipo:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. Ottenere lo stato della crittografia:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. crittografia tooenable in una nuova macchina virtuale dal disco rigido virtuale crittografato, utilizzare hello seguenti parametri con hello `azure vm create` comando:

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a>Abilitare la crittografia in una VM IaaS Windows esistente o in esecuzione in Azure
In questo scenario, è possibile abilitare la crittografia utilizzando il modello di gestione risorse di hello, i cmdlet di PowerShell o i comandi CLI. Hello nelle sezioni seguenti illustrano in dettaglio come tooenable usando hello modello di gestione risorse e i comandi CLI.

#### <a name="using-hello-resource-manager-template"></a>Utilizzando il modello di gestione risorse di hello
È possibile abilitare la crittografia del disco esistente o IaaS macchine virtuali di Windows in esecuzione in Azure utilizzando hello [modello di gestione risorse](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).

1. Nel modello hello avvio rapido di Azure, fare clic su **distribuire tooAzure**, immettere la configurazione di crittografia hello hello **parametri** blade e quindi fare clic su **OK**.

2. Selezionare una sottoscrizione hello, gruppo di risorse, percorso del gruppo di risorse, legali e contratto e quindi fare clic su **crea** crittografia tooenable in hello esistente o in esecuzione VM IaaS.

Hello nella tabella seguente vengono elencati parametri di modello di gestione risorse di hello per esistente o l'esecuzione di macchine virtuali che utilizzano un ID client di Azure AD:

| . | Descrizione |
| --- | --- |
| AADClientID | ID client dell'applicazione hello Azure AD che dispone di autorizzazioni toowrite segreti toohello chiave dell'insieme di credenziali. |
| AADClientSecret | Segreto client dell'applicazione hello Azure AD che dispone di autorizzazioni toowrite segreti toohello chiave dell'insieme di credenziali. |
| keyVaultName | Nome della chiave hello insieme di credenziali di tale chiave deve essere caricata a BitLocker hello. È possibile ottenerlo utilizzando cmdlet hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`. |
|  keyEncryptionKeyURL | URL della chiave di crittografia della chiave hello che è usato tooencrypt hello generato chiave BitLocker. Questo parametro è facoltativo se si seleziona **nokek** nell'elenco a discesa UseExistingKek hello. Se si seleziona **kek** nell'elenco a discesa UseExistingKek hello, è necessario immettere hello _keyEncryptionKeyURL_ valore. |
| volumeType | Tipo di volume viene eseguita l'operazione di crittografia hello. I valori validi sono _OS_, _Data_ e _All_. |
| sequenceVersion | Versione di sequenza di hello operazione BitLocker. Questo numero di versione incrementato ogni volta che viene eseguita un'operazione di crittografia del disco su hello stessa macchina virtuale. |
| vmName | Nome della macchina virtuale che hello l'operazione di crittografia hello è toobe eseguiti. |

> [!NOTE]
> _KeyEncryptionKeyURL_ è un parametro facoltativo. È possibile portare la propria KEK toofurther salvaguardia hello dati chiave di crittografia (segreti di crittografia di BitLocker) nell'insieme di credenziali chiave hello.

#### <a name="using-powershell-cmdlets"></a>Usare i cmdlet PowerShell
Per informazioni sull'abilitazione della crittografia con la crittografia del disco di Azure tramite i cmdlet di PowerShell, vedere il post di blog di hello [esplorare di crittografia del disco di Azure con Azure PowerShell - parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) e [esplorare crittografia del disco di Azure con Azure PowerShell - parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).

#### <a name="using-cli-commands"></a>Uso dei comandi dell'interfaccia della riga di comando
crittografia tooenable in esistente o in esecuzione Windows IaaS con macchina virtuale in Azure mediante i comandi CLI, hello seguenti:

1. criteri di accesso tooset nell'insieme di credenziali chiave hello:
   * Set hello **EnabledForDiskEncryption** flag:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * Impostare le autorizzazioni tooAzure AD applicazione toowrite segreti tooyour chiave dell'insieme di credenziali:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. crittografia tooenable in una macchina virtuale esistente o in esecuzione:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. stato di crittografia tooget:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. crittografia tooenable in una nuova macchina virtuale dal disco rigido virtuale crittografato, utilizzare hello seguenti parametri con hello `azure vm create` comando:

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a>Abilitare la crittografia in una VM IaaS Linux esistente o in esecuzione in Azure
È possibile abilitare la crittografia del disco in una VM Linux IaaS esistenti o è in esecuzione in Azure utilizzando hello [modello di gestione risorse](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).

1. Fare clic su **distribuire tooAzure** sul modello hello avvio rapido di Azure, immettere la configurazione di crittografia hello hello **parametri** blade e quindi fare clic su **OK**.

2. Selezionare una sottoscrizione hello, gruppo di risorse, percorso del gruppo di risorse, legali e contratto e quindi fare clic su **crea** crittografia tooenable in hello esistente o in esecuzione VM IaaS.

Hello nella tabella seguente elenca i parametri di modello di gestione risorse per esistente o in esecuzione macchine virtuali che utilizzano un ID client di Azure AD:

| . | Descrizione |
| --- | --- |
| AADClientID | ID client dell'applicazione hello Azure AD che dispone di autorizzazioni toowrite segreti toohello chiave dell'insieme di credenziali. |
| AADClientSecret | Segreto client dell'applicazione hello Azure AD che dispone di autorizzazioni toowrite segreti tooyour chiave dell'insieme di credenziali. |
| keyVaultName | Nome della chiave hello insieme di credenziali di tale chiave deve essere caricata a BitLocker hello. È possibile ottenerlo utilizzando cmdlet hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`. |
|  keyEncryptionKeyURL | URL della chiave di crittografia della chiave hello che è usato tooencrypt hello generato chiave BitLocker. Questo parametro è facoltativo se si seleziona **nokek** nell'elenco a discesa UseExistingKek hello. Se si seleziona **kek** nell'elenco a discesa UseExistingKek hello, è necessario immettere hello _keyEncryptionKeyURL_ valore. |
| volumeType | Tipo di volume viene eseguita l'operazione di crittografia hello. I valori supportati validi sono _OS_ o _All_ (per RHEL 7.2, CentOS 7.2 e Ubuntu 16.04) e _Data_ (per tutte le altre distribuzioni). |
| sequenceVersion | Versione di sequenza di hello operazione BitLocker. Questo numero di versione incrementato ogni volta che viene eseguita un'operazione di crittografia del disco su hello stessa macchina virtuale. |
| vmName | Nome della macchina virtuale che hello l'operazione di crittografia hello è toobe eseguiti. |
| passPhrase | Digitare una passphrase sicura come chiave di crittografia dati hello. |

> [!NOTE]
> _KeyEncryptionKeyURL_ è un parametro facoltativo. È possibile portare la propria KEK toofurther salvaguardia hello dati chiave di crittografia (passphrase segreto) nell'insieme di credenziali chiave.

#### <a name="cli-commands"></a>Comandi dell'interfaccia della riga di comando
È possibile abilitare crittografia del disco in disco rigido virtuale crittografato mediante installazione e utilizzo hello [comando CLI](../cli-install-nodejs.md). crittografia tooenable in esistente o macchine virtuali Linux IaaS in esecuzione in Azure utilizzando i comandi CLI, hello seguenti:

1. Impostare i criteri di accesso nell'insieme di credenziali chiave hello:

 * Set hello **EnabledForDiskEncryption** flag:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * Impostare le autorizzazioni tooAzure AD applicazione toowrite segreti tooyour chiave dell'insieme di credenziali:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. crittografia tooenable in una macchina virtuale esistente o in esecuzione:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. Ottenere lo stato della crittografia:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. crittografia tooenable in una nuova macchina virtuale dal disco rigido virtuale crittografato, utilizzare hello seguenti parametri con hello `azure vm create` comando:
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a>Ottenere lo stato di crittografia hello di una VM IaaS crittografati
È possibile ottenere lo stato di crittografia hello usando Gestione risorse di Azure, [i cmdlet di PowerShell](/powershell/azure/overview), o i comandi CLI. Hello le sezioni seguenti illustrano come toouse hello portale di Azure classico e tooget comandi CLI hello lo stato di crittografia.

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a>Ottenere lo stato di crittografia hello di una macchina virtuale di Windows crittografato tramite Gestione risorse di Azure
È possibile ottenere lo stato di crittografia hello di hello VM IaaS da Gestione risorse di Azure eseguendo hello seguenti:

1. Accedi toohello [portale di Azure classico](https://portal.azure.com/), quindi fare clic su **macchine virtuali** nel riquadro sinistro di hello toosee una visualizzazione di riepilogo delle macchine virtuali hello nella sottoscrizione. È possibile filtrare una visualizzazione di macchine virtuali hello selezionando il nome della sottoscrizione hello in hello **sottoscrizione** elenco a discesa.

2. Nella parte superiore di hello di hello **macchine virtuali** pagina, fare clic su **colonne**.

3. In hello **scegliere colonna** pannello seleziona **crittografia del disco**e quindi fare clic su **aggiornamento**. Verrà visualizzato lo stato di crittografia hello che mostra colonna crittografia disco hello _abilitato_ o _non abilitato_ per ogni macchina virtuale, come illustrato nella seguente illustrazione hello:

 ![Microsoft Antimalware in Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a>Ottenere lo stato di crittografia hello di una VM di IaaS (Windows/Linux) crittografata tramite cmdlet di PowerShell hello crittografia disco
È possibile ottenere lo stato di crittografia hello di hello VM IaaS dal cmdlet PowerShell di crittografia del disco hello `Get-AzureRmVMDiskEncryptionStatus`. le impostazioni di crittografia hello tooget per la macchina virtuale, immettere il seguente di hello:

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

È possibile esaminare l'output di hello di _Get AzureRmVMDiskEncryptionStatus_ per la crittografia della chiave URL.

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

Hello OSVolumeEncrypted e i valori delle impostazioni DataVolumesEncrypted vengono impostati too_Encrypted_, indicante che entrambi i volumi sono crittografati tramite crittografia di disco di Azure. Per informazioni sull'abilitazione della crittografia con la crittografia del disco di Azure tramite i cmdlet di PowerShell, vedere il post di blog di hello [esplorare di crittografia del disco di Azure con Azure PowerShell - parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) e [esplorare crittografia del disco di Azure con Azure PowerShell - parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).

> [!NOTE]
> Nelle macchine virtuali Linux, sono necessari tre minuti di toofour per hello `Get-AzureRmVMDiskEncryptionStatus` lo stato di crittografia di cmdlet tooreport hello.

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a>Ottenere lo stato di crittografia hello di hello VM IaaS dal comando CLI di hello crittografia disco
È possibile ottenere lo stato di crittografia hello di hello VM IaaS tramite comando CLI di crittografia del disco hello `azure vm show-disk-encryption-status`. le impostazioni di crittografia hello tooget per la macchina virtuale, immettere la sessione CLI di Azure:

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a>Disabilitare la crittografia nelle VM IaaS Windows in esecuzione
È possibile disabilitare la crittografia in un'esecuzione di Windows o Linux IaaS con macchina virtuale tramite il modello di gestione risorse di Azure disco crittografia hello o i cmdlet di PowerShell e specificare la configurazione di decrittografia hello.

##### <a name="windows-vm"></a>Macchina virtuale Windows
passaggio di disabilitare la crittografia Hello disabilita la crittografia di hello del sistema operativo, il volume di dati hello o entrambi in esecuzione la macchina virtuale IaaS Windows hello. Non è possibile disabilitare il volume del sistema operativo hello e lasciare il volume di dati hello crittografato. Quando viene eseguito il passaggio di disabilitare la crittografia hello, modello di distribuzione classica Azure hello Aggiorna modello del servizio VM hello e hello Windows IaaS con macchina virtuale è contrassegnato decrittografata. contenuto Hello di hello VM non venga crittografati a riposo. la decrittografia di Hello non elimina il materiale della chiave dell'insieme di credenziali e hello crittografia chiave (chiavi di crittografia di BitLocker per Windows e la Passphrase per Linux).

##### <a name="linux-vm"></a>VM Linux
passaggio di disabilitare la crittografia Hello disabilita la crittografia dei volumi di dati hello hello in esecuzione Linux IaaS con macchina virtuale. Questo passaggio funziona solo se il disco del sistema operativo hello non è crittografato.

> [!NOTE]
> La disabilitazione della crittografia nel disco del sistema operativo hello non è consentita nelle macchine virtuali Linux.

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>Disabilitare la crittografia in una macchina virtuale IaaS esistente o in esecuzione
È possibile disabilitare la crittografia del disco durante l'esecuzione di macchine virtuali IaaS di Windows tramite hello [modello di gestione risorse](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).

1. Nel modello hello avvio rapido di Azure, fare clic su **distribuire tooAzure**, immettere configurazione decrittografia hello hello **parametri** blade e quindi fare clic su **OK**.

2. Selezionare una sottoscrizione hello, gruppo di risorse, percorso del gruppo di risorse, legali e contratto e quindi fare clic su **crea** tooenable crittografia in una nuova VM IaaS.

Per le macchine virtuali Linux, è possibile disabilitare la crittografia tramite hello [disabilitare la crittografia in una VM Linux in esecuzione](https://aka.ms/decrypt-linuxvm) modello.

Hello nella tabella seguente sono elencati i parametri di modello di gestione delle risorse per la disabilitazione della crittografia in una VM IaaS in esecuzione:

| . | Descrizione |
| --- | --- |
| vmName | Nome della macchina virtuale che hello l'operazione di crittografia hello è toobe eseguiti.
| volumeType | Tipo del volume in cui viene eseguita l'operazione di decrittografia. I valori validi sono _OS_, _Data_ e _All_. Non è possibile disabilitare la crittografia durante l'esecuzione di volume di avvio o del sistema operativo Windows IaaS con macchina virtuale senza la disabilitazione della crittografia in hello _dati_ volume. Si noti inoltre che la disabilitazione della crittografia nel disco del sistema operativo hello non è consentita nelle macchine virtuali Linux. |
| sequenceVersion | Versione di sequenza di hello operazione BitLocker. Questo numero di versione incrementato ogni volta che viene eseguita un'operazione di decrittografia del disco su hello stessa macchina virtuale. |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>Disabilitare la crittografia in una macchina virtuale IaaS esistente o in esecuzione
crittografia toodisable in una VM IaaS esistenti o è in esecuzione tramite i cmdlet di PowerShell hello, vedere [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption). Questo cmdlet supporta sia le VM Windows che le VM Linux. crittografia toodisable, installa un'estensione nella macchina virtuale hello. Se hello _nome_ parametro non viene specificato, un'estensione con il nome predefinito hello _AzureDiskEncryption per le macchine virtuali Windows_ viene creato.

Nelle macchine virtuali Linux, hello AzureDiskEncryptionForLinux estensione viene utilizzato.

> [!NOTE]
> Questo cmdlet riavvia una macchina virtuale hello.

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a>Abilitare la crittografia su macchina virtuale IaaS pre-crittografata con disco gestito Azure
Utilizzare hello Azure gestito disco ARM modello toocreate una macchina virtuale crittografata da un disco rigido virtuale pre-crittografato utilizzando hello ARM modello si trova in   
[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a>Abilitare la crittografia su una nuova macchina virtuale IaaS Linux con disco gestito Azure
Utilizzare hello Azure gestito disco ARM modello toocreate in che un nuovo crittografato Linux IaaS con macchina virtuale utilizzando il modello ARM hello   
[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a>Abilitare la crittografia su una nuova macchina virtuale IaaS Windows con disco gestito Azure
 Utilizzare hello Azure gestito disco ARM modello toocreate in che un nuovo crittografato Linux IaaS con macchina virtuale utilizzando il modello ARM hello   
 [Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)

  > [!NOTE]
  >È obbligatorio toosnapshot e/o di backup un disco gestito basato all'esterno dell'istanza della macchina virtuale e precedenti tooenabling crittografia del disco di Azure.  Uno snapshot del disco gestito hello può essere prelevato portale hello o Backup di Azure può essere utilizzato.  Backup di verificare che un'opzione di ripristino è possibile nel caso di hello di qualsiasi errore imprevisto durante la crittografia.  Una volta che viene eseguito un backup, il cmdlet Set-AzureRmVMDiskEncryptionExtension hello può essere utilizzato tooencrypt gestiti dischi specificando il parametro - skipVmBackup hello.  Questo comando ha esito negativo su una macchina virtuale basata su un disco gestito finché non viene eseguito un backup e non viene specificato il parametro.    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a>Aggiornare le impostazioni di crittografia di una macchina virtuale non Premium crittografata esistente
  Utilizzare hello Azure disco crittografia supportata interfacce esistenti per l'esecuzione di macchine Virtuali [cmdlet di Powershell, i modelli di CLI o ARM] tooupdate le impostazioni di crittografia hello come client AAD ID/chiave privata, chiave di crittografia [KEK], chiave di crittografia di BitLocker per la macchina virtuale di Windows o la Passphrase per Impostazione di crittografia ECC VM Linux hello aggiornamento è supportato solo per le macchine virtuali supportate dall'archiviazione non premium. NON è supportata per le macchine virtuali dotate di archiviazione Premium.

## <a name="appendix"></a>Appendice
### <a name="connect-tooyour-subscription"></a>Connettere tooyour sottoscrizione
Prima di procedere, rivedere hello *prerequisiti* sezione in questo articolo. Dopo avere verificato che tutti i prerequisiti siano stati soddisfatti, connettere tooyour sottoscrizione effettuando hello seguenti:

1. Avviare una sessione di Azure PowerShell e accedere con il comando seguente hello tooyour account Azure:

    `Login-AzureRmAccount`

2. Se si dispone di più sottoscrizioni e si desidera uno toouse toospecify, digitare hello sottoscrizioni hello toosee per l'account di seguito:

    `Get-AzureRmSubscription`

3. sottoscrizione di hello toospecify da toouse, tipo:

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. tooverify che sottoscrizione hello configurata sia corretto, digitare:

    `Get-AzureRmSubscription`

5. tooconfirm hello Azure crittografia del disco sono installati i cmdlet, tipo:

    `Get-command *diskencryption*`

6. Dopo l'output di Hello conferma installazione crittografia disco di Azure PowerShell hello:

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a>Preparare un disco rigido virtuale Windows pre-crittografato
Nelle sezioni Hello che seguono sono tooprepare necessario un disco rigido virtuale di Windows pre-crittografato per la distribuzione come un disco rigido virtuale crittografata in IaaS di Azure. Utilizzare tooprepare informazioni hello e avviare un nuovo Windows macchina virtuale (VHD) in Azure Site Recovery o Azure.

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a>Aggiornamento gruppo criteri tooallow senza TPM per la protezione del sistema operativo
Configurare l'impostazione di criteri di gruppo per BitLocker hello **crittografia unità BitLocker**, che si trova in **criteri del Computer locale** > **configurazione Computer**  >  **Modelli amministrativi** > **componenti di Windows**. Modificare questa impostazione troppo**unità del sistema operativo** > **Richiedi autenticazione aggiuntiva all'avvio** > **Consenti BitLocker senza un TPM compatibile**, come illustrato nella seguente illustrazione hello:

![Microsoft Antimalware in Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a>Installare i componenti della funzionalità BitLocker
Per Windows Server 2012 e versioni successive, usare hello comando seguente:

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

Per Windows Server 2008 R2, utilizzare hello comando seguente:

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a>Preparare il volume del sistema operativo hello per BitLocker utilizzando`bdehdcfg`
toocompress hello partizione del sistema operativo e preparare hello macchina per BitLocker, eseguire hello comando seguente:

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a>Proteggere il volume di sistema operativo hello mediante BitLocker
Hello utilizzare [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) crittografia tooenable comando nel volume di avvio hello utilizzando una protezione con chiave esterna. Nel volume o unità esterne hello inoltre inserire la chiave esterna hello (.bek file). La crittografia è abilitata nel volume di sistema/avvio hello dopo il riavvio di hello.

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> Preparare hello macchina virtuale con una data/risorsa distinta disco rigido virtuale per ottenere la chiave esterna di hello mediante BitLocker.

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a>Crittografia di un'unità del sistema operativo in una VM Linux in esecuzione
Crittografia di un'unità del sistema operativo in una VM Linux in esecuzione è supportata in hello seguenti distribuzioni:

* RHEL 7.2
* CentOS 7.2
* Ubuntu 16.04

##### <a name="prerequisites-for-os-disk-encryption"></a>Prerequisiti per la crittografia del disco del sistema operativo

* dall'immagine del Marketplace hello in Gestione risorse di Azure, è necessario creare Hello macchina virtuale.
* VM di Azure con almeno 4 GB di RAM (7 GB consigliati).
* (Per RHEL e CentOS) Disabilitare SELinux. toodisable SELinux, vedere "4.4.2. La disabilitazione di SELinux"in hello [Guida dell'amministratore e dell'utente di SELinux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) su hello macchina virtuale.
* Dopo aver disabilitato SELinux, riavviare almeno una volta hello macchina virtuale.

##### <a name="steps"></a>Passi
1. Creare una macchina virtuale utilizzando una delle distribuzioni di hello specificate in precedenza.

 Per CentOS 7.2, la crittografia del disco del sistema operativo è supportata tramite un'immagine speciale. toouse questa immagine, specificare "7.2n" come hello SKU quando si crea hello VM:
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. Configurare secondo tooyour esigenze di hello macchina virtuale. Se si intende tooencrypt tutte le unità hello (sistema operativo + dati), unità dati hello necessario toobe montabile da /etc/fstab. e specificati.

 > [!NOTE]
 > Utilizzare UUID =... toospecify unità di dati in fstab/e così via, anziché specificare nome del dispositivo hello blocco (ad esempio, /dev/sdb1). Durante la crittografia, hello ordine delle modifiche di unità nel hello macchina virtuale. Se la macchina virtuale si basa su un ordine specifico di bloccare i dispositivi, ne verrà eseguito toomount dopo averle crittografia.

3. Disconnessione da sessioni SSH hello.

4. tooencrypt hello del sistema operativo, specificare volumeType come **tutti** o **OS** quando si [abilitare la crittografia](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).

 > [!NOTE]
 > Tutti i processi dello spazio dell'utente non in esecuzione come servizi `systemd` devono essere terminati con `SIGKILL`. Riavviare hello macchina virtuale. Quando si abilita la crittografia del disco del sistema operativo in una macchina virtuale in esecuzione, pianificare i tempi di inattività della VM.

5. Monitorare periodicamente lo stato di avanzamento hello di crittografia utilizzando istruzioni hello in hello [nella sezione successiva](#monitoring-os-encryption-progress).

6. Dopo Get AzureRmVmDiskEncryptionStatus mostrato "VMRestartPending", riavviare la macchina virtuale tramite l'accesso tooit o tramite il portale di hello, PowerShell o CLI.
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
Prima di riavviare, si consiglia di salvare [diagnostica di avvio](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) di hello macchina virtuale.

#### <a name="monitoring-os-encryption-progress"></a>Monitoraggio dello stato della crittografia del sistema operativo
Esistono tre modi per monitorare lo stato della crittografia del sistema operativo:

* Hello utilizzare `Get-AzureRmVmDiskEncryptionStatus` cmdlet ed esaminare il campo di ProgressMessage hello:
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 Raggiunge hello VM "Crittografia avviata del disco del sistema operativo", accetta di circa 40 minuti too50 su un'archiviazione Premium sottoposti a macchina virtuale.

 A causa dell'[errore #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` e `DataVolumesEncrypted`vengono visualizzati come `Unknown` in alcune distribuzioni. Con WALinuxAgent 2.1.5 e versioni successive questo errore viene risolto automaticamente. Se viene visualizzato `Unknown` nell'output di hello, è possibile verificare lo stato di crittografia del disco tramite hello Esplora inventario risorse di Azure.

 Andare troppo[Esplora inventario risorse di Azure](https://resources.azure.com/), quindi espandere questa gerarchia nel Pannello di selezione hello a sinistra:

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 In hello InstanceView, scorrere verso il basso lo stato di crittografia hello toosee delle unità.

 ![Visualizzazione dell'istanza della VM](./media/azure-security-disk-encryption/vm-instanceview.png)

* Esaminare la [diagnostica di avvio](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/). I messaggi da hello estensione ADE devono essere preceduti dalla `[AzureDiskEncryption]`.

* Accedi toohello VM tramite SSH e ottenere log di estensione hello da:

    /var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux

 Si consiglia di non accedere toohello VM mentre la crittografia del sistema operativo è in corso. Copiare i registri di hello solo quando hello altri due metodi hanno esito negativo.

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a>Preparare un disco rigido virtuale Linux pre-crittografato
##### <a name="ubuntu-16"></a>Ubuntu 16
Configurare la crittografia durante l'installazione di distribuzione hello eseguendo hello seguenti:

1. Selezionare **configurare volumi crittografati** quando si creano partizioni dischi hello.

 ![Configurazione di Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. Creare un'unità di avvio separata che non deve essere crittografata. Crittografare l'unità radice.

 ![Configurazione di Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. Specificare una passphrase. Si tratta di passphrase hello caricare toohello insieme di credenziali chiave.

 ![Configurazione di Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. Terminare il partizionamento.

 ![Configurazione di Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. Quando si avvia VM hello e una passphrase viene richiesto, utilizzare hello passphrase fornita nel passaggio 3.

 ![Configurazione di Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. Preparare hello VM per il caricamento in Azure utilizzando [queste istruzioni](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/). Non eseguire ancora ultimo passaggio di hello (Buongiorno deprovisioning VM).

Configurare crittografia toowork con Azure eseguendo hello seguenti:

1. Creare un file in /usr/local/sbin/azure_crypt_key.sh, con contenuto hello in hello lo script seguente. Prestare attenzione toohello KeyFileName, perché è un nome di file passphrase hello usato da Azure.

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. Modifica configurazione crypt hello in */e così via/crypttab*. L'aspetto dovrebbe risultare simile al seguente:
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. Se si sta modificando *azure_crypt_key.sh* in Windows ed è stato copiato tooLinux, eseguire `dos2unix /usr/local/sbin/azure_crypt_key.sh`.

4. Aggiungere script toohello delle autorizzazioni di esecuzione:
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. Modificare */etc/initramfs-tools/modules* accodando le righe:
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. Eseguire `update-initramfs -u -k all` tooupdate prova initramfs toomake prova `keyscript` effettive.

7. È ora possibile eseguire il deprovisioning hello macchina virtuale.

 ![Configurazione di Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. Passaggio successivo toohello continuare e [caricare il disco rigido virtuale](#upload-encrypted-vhd-to-an-azure-storage-account) in Azure.

##### <a name="opensuse-132"></a>openSUSE 13.2
crittografia tooconfigure durante l'installazione di distribuzione hello, hello seguenti:
1. Quando si partiziona dischi hello, selezionare **gruppo di volumi crittografare**e quindi immettere una password. Si tratta hello password che verrà caricato tooyour insieme di credenziali chiave.

 ![Configurazione di openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. Avvio hello VM utilizzando la password.

 ![Configurazione di openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. Preparazione hello VM per il caricamento tooAzure seguendo le istruzioni hello [preparare una macchina virtuale SLES o openSUSE per Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131). Non eseguire ancora ultimo passaggio di hello (Buongiorno deprovisioning VM).

tooconfigure crittografia toowork con Azure, hello seguenti:
1. Modificare /etc/dracut.conf hello e aggiungere hello seguente riga:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. Impostare come commento le righe dall'entità finale hello hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. Aggiungere hello seguente riga all'inizio di hello di /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh file hello:
 ```
    DRACUT_SYSTEMD=0
 ```
Modificare quindi tutte le occorrenze di:
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
in:
```
    if [ 1 ]; then
```
4. Modifica /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh e aggiungerlo troppo "dispositivo aprire LUKS #":

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. Eseguire `/usr/sbin/dracut -f -v` tooupdate hello initrd.

6. Ora è possibile eseguire il deprovisioning hello VM e [caricare il disco rigido virtuale](#upload-encrypted-vhd-to-an-azure-storage-account) in Azure.

##### <a name="centos-7"></a>CentOS 7
crittografia tooconfigure durante l'installazione di distribuzione hello, hello seguenti:
1. Selezionare **Encrypt my data** (Crittografa dati personali) durante il partizionamento dei dischi.

 ![Configurazione di CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. Assicurarsi **Encrypt** (Crittografa) sia selezionato per la partizione radice.

 ![Configurazione di CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. Specificare una passphrase. Si tratta di hello passphrase che verrà caricato tooyour insieme di credenziali chiave.

 ![Configurazione di CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. Quando si avvia VM hello e una passphrase viene richiesto, utilizzare hello passphrase fornita nel passaggio 3.

 ![Configurazione di CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. Hello preparare la macchina virtuale per il caricamento in Azure utilizzando istruzioni "CentOS 7.0 +" hello [preparare una macchina virtuale basata su CentOS per Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70). Non eseguire ancora ultimo passaggio di hello (Buongiorno deprovisioning VM).

6. Ora è possibile eseguire il deprovisioning hello VM e [caricare il disco rigido virtuale](#upload-encrypted-vhd-to-an-azure-storage-account) in Azure.

tooconfigure crittografia toowork con Azure, hello seguenti:

1. Modificare /etc/dracut.conf hello e aggiungere hello seguente riga:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. Impostare come commento le righe dall'entità finale hello hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. Aggiungere hello seguente riga all'inizio di hello di /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh file hello:
```
    DRACUT_SYSTEMD=0
```
Modificare quindi tutte le occorrenze di:
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
to
```
    if [ 1 ]; then
```
4. Modificare /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh e aggiungere questo dopo hello "dispositivo aprire LUKS #":
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. Eseguire hello "usr/servizio/dracut / -f - v" tooupdate hello initrd.

![Configurazione di CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a>Caricare crittografati VHD tooan account di archiviazione Azure
Dopo aver abilitato la crittografia BitLocker o DM Crypt, hello locale crittografato account di archiviazione tooyour toobe caricato esigenze disco rigido virtuale.

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a>Carica una chiave privata di crittografia del disco hello per hello pre-crittografato VM tooyour chiave dell'insieme di credenziali
chiave privata di crittografia del disco Hello ottenuto in precedenza deve essere caricato come un segreto nell'insieme di credenziali chiave. insieme di credenziali chiave Hello necessita di crittografia del disco toohave e autorizzazioni abilitate per il client di Azure AD.

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a>Segreto di crittografia del disco non crittografato con una chiave di crittografia della chiave
tooset backup segreto hello nell'insieme di credenziali chiave, utilizzare [Set AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret). Se si dispone di una macchina virtuale di Windows, file bek hello viene codificato come stringa base64 e quindi caricato tooyour insieme di credenziali chiave usando hello `Set-AzureKeyVaultSecret` cmdlet. Per Linux, hello passphrase viene codificata come stringa base64 e quindi caricato toohello insieme di credenziali chiave. Inoltre, assicurarsi che tale hello tag seguenti vengono impostate quando si crea il segreto hello nell'insieme di credenziali chiave hello.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

Hello utilizzare `$secretUrl` nel passaggio successivo di hello per [collegamento del disco del sistema operativo hello senza utilizzare KEK](#without-using-a-kek).

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a>Segreto di crittografia del disco crittografato con una chiave di crittografia della chiave
Prima di caricare l'insieme di credenziali chiave segreta toohello hello, è possibile crittografare facoltativamente, usando una chiave di crittografia della chiave. Incapsulamento hello utilizzare [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst crittografare segreto hello utilizzando hello chiave di crittografia della chiave. output di questa operazione wrap Hello è una stringa di URL con codificata base64, che è quindi possibile caricare come segreto tramite hello [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

Utilizzare `$KeyEncryptionKey` e `$secretUrl` nel passaggio successivo di hello per [collegamento del disco del sistema operativo hello utilizzando KEK](#using-a-kek).

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a>Specificare un URL del segreto quando si collega un disco del sistema operativo
#### <a name="without-using-a-kek"></a>Senza l'uso di una chiave di crittografia della chiave (KEK)
Mentre si collega disco hello del sistema operativo, è necessario toopass `$secretUrl`. URL di Hello è stato generato nella sezione "segreto di crittografia del disco non crittografata con una chiave di scambio delle CHIAVI" hello.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a>Uso di una chiave di crittografia della chiave (KEK)
Quando si collega il disco del sistema operativo hello, passare `$KeyEncryptionKey` e `$secretUrl`. URL di Hello è stato generato nella sezione "segreto di crittografia del disco non crittografata con una chiave di scambio delle CHIAVI" hello.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a>Scaricare questa guida
È possibile scaricare questa Guida da hello [Raccolta TechNet](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).

## <a name="for-more-information"></a>Per altre informazioni
[Esplorare Crittografia dischi di Azure con Azure PowerShell - Parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[Esplorare Crittografia dischi di Azure con Azure PowerShell - Parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
