---
title: aaaEncrypt dischi in una VM Linux con hello Azure CLI 1.0 | Documenti Microsoft
description: Come tooencrypt dischi in una VM Linux utilizzando hello Azure CLI 1.0 e modello di distribuzione di gestione risorse di hello
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: 68a0394d366c3c6941e2c6db0d4263123f951946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a>Crittografare i dischi in una VM Linux utilizzando hello Azure CLI 1.0
Per migliorare gli aspetti di sicurezza e conformità delle macchine virtuali (VM), i dischi virtuali in Azure possono essere crittografati a riposo. I dischi vengono crittografati usando chiavi di crittografia protette in un insieme di credenziali delle chiavi di Azure. È possibile controllare queste chiavi di crittografia e il loro uso. In questo articolo illustra in dettaglio come tooencrypt dischi virtuali in una VM Linux utilizzando hello Azure CLI 1.0 e modello di distribuzione di gestione risorse di hello.

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- [Azure CLI 1.0](#quick-commands) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello

## <a name="quick-commands"></a>Comandi rapidi
Se è necessario tooquickly attività hello, hello seguente hello dettagli sezione base comandi tooencrypt dischi virtuali nella macchina virtuale. Ulteriori informazioni e il contesto per ogni passaggio è reperibile rest hello del documento hello, [avvio qui](#overview-of-disk-encryption).

È necessario hello [più recente di Azure CLI 1.0](../../xplat-cli-install.md) installato e registrato con modalità di gestione risorse di hello come indicato di seguito:

```azurecli
azure config mode arm
```

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono `myResourceGroup`, `myKeyVault` e `myVM`.

Innanzitutto, abilitare il provider di credenziali chiave hello nella sottoscrizione di Azure e creare un gruppo di risorse. esempio Hello crea il nome di un gruppo di risorse `myResourceGroup` in hello `WestUS` percorso:

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

Creare un insieme di credenziali delle chiavi di Azure. esempio Hello crea un insieme di credenziali di chiave denominato `myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

Creare una chiave di crittografia nell'insieme di credenziali delle chiavi e abilitarlo per la crittografia del disco. esempio Hello crea una chiave denominata `myKey`:

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

Creare un endpoint tramite Azure Active Directory per la gestione dell'autenticazione hello e lo scambio delle chiavi di crittografia dall'insieme di credenziali chiave. Hello `--home-page` e `--identifier-uris` non è necessario l'indirizzo instradabile effettivo toobe. Per hello massimo livello di sicurezza, i segreti del client devono essere utilizzati anziché le password. Hello CLI di Azure attualmente non è possibile generare i segreti dei client. I segreti dei client possono essere generati solo nel portale di Azure hello. esempio Hello crea un endpoint di Azure Active Directory denominato `myAADApp` e viene utilizzata una password di `myPassword`. Specificare una password personalizzata come di seguito:

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

Hello nota `applicationId` illustrato nell'output di hello da hello precedente comando. Questo ID applicazione viene utilizzato in hello alla procedura seguente:

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

Aggiungere un tooan disco dati macchina virtuale esistente. esempio Hello aggiunge un tooa disco dati macchina virtuale denominata `myVM`:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Esaminare i dettagli di hello per la chiave di insieme di credenziali chiave e hello che è stato creato. È necessario hello ID insieme di credenziali chiave, URI e chiave URL nel passaggio finale hello. Hello esempio esamina i dettagli di hello per un insieme di credenziali di chiave denominato `myKeyVault` e una chiave denominata `myKey`:

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

Crittografare i dischi come di seguito, immettendo i propri nomi di parametro:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

Hello CLI di Azure non fornisce gli errori dettagliati durante il processo di crittografia hello. Per ulteriori informazioni sulla risoluzione dei problemi, vedere `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`. Come hello precedente comando dispone di molte variabili e potrebbero non essere molto indicazione as avrà esito negativo processo di hello toowhy, un esempio di comandi completo potrebbe essere come segue:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

Infine, esaminare lo stato di crittografia hello nuovamente tooconfirm che i dischi virtuali sono ora stati crittografati. esempio Hello Controlla stato hello di una macchina virtuale denominata `myVM` in hello `myResourceGroup` gruppo di risorse:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a>Panoramica della crittografia dei dischi
I dischi virtuali delle VM Linux vengono crittografati a riposo mediante [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). Non è previsto alcun addebito per la crittografia dei dischi virtuali in Azure. Chiavi di crittografia vengono archiviate nell'insieme di credenziali di Azure chiave tramite software di protezione oppure è possibile importare o generare le chiavi in moduli di protezione Hardware (HSM) Certificate tooFIPS standard di livello 2 di 140-2. È possibile esercitare il controllo su queste chiavi di crittografia e sul loro uso. Queste chiavi di crittografia sono utilizzati tooencrypt e decrittografare i dischi virtuali collegati tooyour macchina virtuale. Un endpoint di Azure Active Directory fornisce un meccanismo protetto per il rilascio di queste chiavi di crittografia all'accensione e allo spegnimento delle VM.

il processo di Hello per la crittografia di una macchina virtuale è il seguente:

1. Creare una chiave di crittografia in un insieme di credenziali delle chiavi di Azure.
2. Configurare hello crittografia chiave toobe utilizzabile per la crittografia dei dischi.
3. chiave di crittografia hello tooread dall'hello insieme di credenziali chiave di Azure, creare un endpoint tramite Azure Active Directory con le autorizzazioni appropriate di hello.
4. Eseguire hello comando tooencrypt i dischi virtuali, specificando l'endpoint di Azure Active Directory hello e appropriato toobe chiave crittografica utilizzata.
5. endpoint di Azure Active Directory Hello richiede la chiave di crittografia richiesto di hello insieme credenziali chiavi Azure.
6. i dischi virtuali Hello vengono crittografati tramite la chiave crittografica hello fornito.

## <a name="supporting-services-and-encryption-process"></a>Servizi di supporto e processo di crittografia
Crittografia del disco si basa su hello i componenti aggiuntivi seguenti:

* **Insieme di credenziali chiave di Azure** -utilizzate le chiavi di crittografia toosafeguard e segreti utilizzati per il processo di crittografia/decrittografia hello disco.
  * Se disponibile, è possibile usare un insieme di credenziali delle chiavi di Azure esistente. Non si dispone toodedicate i dischi tooencrypting un insieme di credenziali chiave.
  * limiti amministrativi tooseparate e visibilità chiave, è possibile creare un insieme di credenziali chiave dedicato.
* **Azure Active Directory** : handle hello lo scambio sicuro di chiavi di crittografia necessarie e richiesta l'autenticazione per le azioni.
  * In genere, è possibile inserire l'applicazione in un'istanza esistente di Azure Active Directory.
  * un'applicazione Hello è più un endpoint per l'insieme di credenziali chiave hello e toorequest servizi macchina virtuale e ottenere generato le chiavi di crittografia appropriato hello. Non si sta procedendo a sviluppare un'applicazione reale integrata con Azure Active Directory.

## <a name="requirements-and-limitations"></a>Requisiti e limitazioni
Requisiti relativi alla crittografia dei dischi e scenari supportati:

* Hello seguente server Linux SKU - Ubuntu, CentOS, SUSE e SUSE Linux Enterprise Server (SLES) e Red Hat Enterprise Linux.
* Tutte le risorse (ad esempio l'insieme di credenziali chiave, l'account di archiviazione e macchina virtuale) devono essere in hello stessa regione di Azure e sottoscrizione.
* VM standard delle serie A, D, DS, G e GS.

Crittografia del disco non è attualmente supportata nei seguenti scenari hello:

* VM di base.
* Macchine virtuali create con modello di distribuzione classica hello.
* Disabilitare la crittografia del disco del sistema operativo nelle VM Linux.
* Aggiornamento delle chiavi di crittografia in una VM Linux già crittografato hello.

## <a name="create-hello-azure-key-vault-and-keys"></a>Creare hello insieme credenziali chiavi Azure e le chiavi
toocomplete hello restanti in questa Guida, è necessario hello [più recente di Azure CLI 1.0](../../xplat-cli-install.md) installato e registrato con modalità di gestione risorse di hello come indicato di seguito:

```azurecli
azure config mode arm
```

Nel corso di esempi di comandi hello, sostituire tutti i parametri di esempio con i nomi, percorso e i valori di chiave. Negli esempi seguenti Hello utilizzano una convenzione di `myResourceGroup`, `myKeyVault`, `myAADApp`e così via.

primo passaggio Hello è toocreate toostore un insieme di credenziali chiave Azure le chiavi di crittografia. Insieme di credenziali chiave di Azure è possibile archiviare le chiavi, i segreti, o le password che consentono di toosecurely implementano nelle applicazioni e servizi. Per la crittografia del disco virtuale, si usa l'insieme di credenziali chiave toostore una chiave di crittografia che viene utilizzato tooencrypt o decrittografare i dischi virtuali.

Abilitare il provider di credenziali chiave hello nella sottoscrizione di Azure, quindi creare un gruppo di risorse. esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `WestUS` percorso:

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

Hello insieme credenziali chiavi Azure contenente hello le chiavi di crittografia e calcolo associato risorse, ad esempio hello macchina virtuale stessa e di archiviazione devono trovarsi nella hello stessa area. esempio Hello crea un insieme di credenziali chiave di Azure denominato `myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

È possibile archiviare le chiavi di crittografia usando il software o il modulo di protezione hardware. L'uso di un modulo di protezione hardware richiede un insieme di credenziali delle chiavi premium. È un toocreating costi aggiuntivi premium insieme di credenziali chiave anziché standard insieme di credenziali chiave che archivia le chiavi protette tramite software. aggiungere un insieme di credenziali chiave premium nel precedente passaggio hello toocreate `--sku Premium` toohello comando. Hello esempio seguente usa le chiavi protette tramite software poiché è stato creato un insieme di credenziali chiave standard.

Per entrambi i modelli di protezione, hello piattaforma Azure deve toobe concesso accesso toorequest hello chiavi di crittografia quando si avvia i dischi virtuali hello toodecrypt hello macchina virtuale. Creare una chiave di crittografia all'interno dell'insieme di credenziali delle chiavi, quindi abilitarne l'uso con la crittografia del disco virtuale. esempio Hello crea una chiave denominata `myKey` e quindi lo abilita per la crittografia del disco:

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a>Creare un'applicazione hello Azure Active Directory
Quando i dischi virtuali vengono crittografati o decrittografati, si utilizza un'autenticazione hello toohandle di endpoint e lo scambio delle chiavi di crittografia dall'insieme di credenziali chiave. Questo endpoint, un'applicazione Azure Active Directory, consente di hello piattaforma Azure toorequest hello appropriato le chiavi di crittografia per conto di hello macchina virtuale. Un'istanza di Azure Active Directory predefinita è già disponibile nella sottoscrizione, anche se molte organizzazioni hanno directory di Azure Active Directory dedicate.

Come si sta creando un'applicazione Azure Active Directory completa, hello `--home-page` e `--identifier-uris` parametri nel seguente esempio hello non richiedono l'indirizzo instradabile effettivo toobe. Hello esempio specifica inoltre un segreto basato su password, anziché la generazione di chiavi all'interno di hello portale di Azure. In questo momento, è Impossibile eseguire la generazione di chiavi da hello CLI di Azure.

Creare l'applicazione di Azure Active Directory. esempio Hello crea un'applicazione denominata `myAADApp` e viene utilizzata una password di `myPassword`. Specificare una password personalizzata come di seguito:

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

Prendere nota di hello `applicationId` restituito nell'output di hello da hello precedente comando. Questo ID applicazione viene utilizzato in alcune hello rimanenti passaggi. Creare quindi un nome dell'entità servizio (SPN) in modo che un'applicazione hello è accessibile all'interno dell'ambiente. toosuccessfully crittografare o decrittografare i dischi virtuali, le autorizzazioni sulla chiave di crittografia hello archiviati nell'insieme di credenziali chiave devono essere tooread hello chiavi del set toopermit hello Azure Active Directory dell'applicazione.

Creare hello SPN e impostare le autorizzazioni appropriate di hello come segue:

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a>Aggiungere un disco virtuale ed esaminare lo stato di crittografia
tooactually crittografare alcuni dischi virtuali, consente di aggiungere un disco tooan macchina virtuale esistente. Aggiungere un tooan disco dati di 5Gb esistente VM come indicato di seguito:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

i dischi virtuali Hello attualmente non sono crittografati. Controllare hello stato corrente di crittografia di una macchina virtuale come segue:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a>Crittografare i dischi virtuali
toonow crittografare i dischi virtuali hello, riunire tutti i componenti precedenti hello:

1. Specificare un'applicazione hello Azure Active Directory e la password.
2. Specificare hello insieme di credenziali chiave toostore hello metadati per i dischi crittografati.
3. Specificare hello toouse di chiavi di crittografia per hello effettivo crittografia e decrittografia.
4. Specificare se si desidera tooencrypt hello del sistema operativo disco, i dischi dati hello o tutti.

Consente di esaminare i dettagli di hello per la chiave di insieme di credenziali chiave di Azure e hello che è stato creato, come necessario hello ID insieme di credenziali chiave, URI e quindi digitare un URL passaggio finale hello:

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

Crittografare i dischi virtuali tramite output di hello dalla hello `azure keyvault show` e `azure keyvault key show` comandi nel modo seguente:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

Come hello precedente comando dispone di numerose variabili, hello esempio seguente è di comandi completo per il riferimento hello:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

Hello CLI di Azure non fornisce gli errori dettagliati durante il processo di crittografia hello. Per ulteriori informazioni sulla risoluzione dei problemi, esaminare `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` su hello VM si esegue la crittografia.

Infine, consente di esaminare lo stato di crittografia hello nuovamente tooconfirm che i dischi virtuali ora sono stati crittografati:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a>Aggiungere ulteriori dischi dati
Dopo che sono stati crittografati i dischi dati, è possibile in seguito si aggiungono altri dischi virtuali tooyour VM e anche crittografarle. Quando si esegue hello `azure vm enable-disk-encryption` comando, incremento hello sequenza versione che utilizza hello `--sequence-version` parametro. Questo parametro di versione sequenza consente tooperform ripetute operazioni con hello stessa macchina virtuale.

Ad esempio, consente di aggiungere un secondo tooyour disco virtuale VM come segue:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Eseguire di nuovo hello comando tooencrypt hello dischi virtuali, questa volta aggiungendo hello `--sequence-version` parametro e incremento hello compreso il primo eseguire come segue:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a>Passaggi successivi
* Per altre informazioni sulla gestione dell'insieme di credenziali delle chiavi di Azure, tra cui come eliminare chiavi crittografiche e insiemi di credenziali, vedere [Gestire l'insieme di credenziali delle chiavi tramite l'interfaccia della riga di comando](../../key-vault/key-vault-manage-with-cli2.md).
* Per ulteriori informazioni sulla crittografia del disco, ad esempio la preparazione di un tooAzure di tooupload macchina virtuale personalizzata crittografato, vedere [crittografia del disco Azure](../../security/azure-security-disk-encryption.md).
