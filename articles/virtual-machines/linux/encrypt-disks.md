---
title: aaaEncrypt dischi in una VM Linux di Azure | Documenti Microsoft
description: Come tooencrypt dischi virtuali in una VM Linux per l'utilizzo di protezione avanzata hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a>Come tooencrypt dischi virtuali in una VM Linux
Per migliorare gli aspetti di sicurezza e conformità delle macchine virtuali (VM), i dischi virtuali in Azure possono essere crittografati. I dischi vengono crittografati usando chiavi di crittografia protette in un insieme di credenziali delle chiavi di Azure. È possibile controllare queste chiavi di crittografia e il loro uso. In questo articolo illustra in dettaglio come tooencrypt dischi virtuali in una VM Linux utilizzando hello CLI di Azure 2.0. È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Comandi rapidi
Se è necessario tooquickly attività hello, hello seguente hello dettagli sezione base comandi tooencrypt dischi virtuali nella macchina virtuale. Ulteriori informazioni e il contesto per ogni passaggio è reperibile rest hello del documento hello, [avvio qui](#overview-of-disk-encryption).

È necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login). In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono *myResourceGroup*, *myKey* e *myVM*.

Innanzitutto, abilitare il provider insieme credenziali chiavi Azure hello nella sottoscrizione di Azure con [registro provider az](/cli/azure/provider#register) e creare un gruppo di risorse con [gruppo az creare](/cli/azure/group#create). esempio Hello crea il nome di un gruppo di risorse *myResourceGroup* in hello *eastus* percorso:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Creare un insieme di credenziali chiave di Azure con [keyvault az creare](/cli/azure/keyvault#create) e abilitare hello insieme di credenziali chiave per l'utilizzo con crittografia del disco. Specificare un nome univoco di Key Vault per *keyvault_name* come indicato di seguito:

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

Creare una chiave di crittografia nell'insieme di credenziali delle chiavi con [az keyvault key create](/cli/azure/keyvault/key#create). esempio Hello crea una chiave denominata *myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

Creare un'entità servizio usando Azure Active Directory con [az ad sp creare-per-rbac](/cli/azure/ad/sp#create-for-rbac). handle dell'entità servizio di Hello hello autenticazione e lo scambio delle chiavi di crittografia dall'insieme di credenziali chiave. Hello di esempio seguente legge i valori hello per un'entità servizio hello Id e la password per l'uso nei comandi di versioni successive:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

password Hello viene restituita solo quando si crea hello dell'entità servizio. Se si desidera, visualizzare e registrare hello password (`echo $sp_password`). È possibile elencare le entità servizio con [az ad sp list](/cli/azure/ad/sp#list) e visualizzare informazioni aggiuntive su un'entità servizio specifica con [az ad sp show](/cli/azure/ad/sp#show).

Impostare le autorizzazioni per l'insieme di credenziali delle chiavi con [az keyvault set-policy](/cli/azure/keyvault#set-policy). Nell'esempio seguente di hello, hello ID entità servizio viene fornito da hello precedente comando:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

Creare una macchina virtuale con [az vm create](/cli/azure/vm#create) e collegare un disco dati di 5 Gb. Solo determinate immagini di marketplace supportano la crittografia del disco. esempio Hello crea una macchina virtuale denominata `myVM` utilizzando un **CentOS 7.2n** immagine:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH tramite VM tooyour hello `publicIpAddress` illustrato nell'output di hello di hello precedente comando. Creare una partizione e un file System, quindi montare il disco di dati hello. Per ulteriori informazioni, vedere [connettersi tooa nuovo disco VM Linux toomount hello](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Chiudere la sessione SSH.

Crittografare la macchina virtuale con [az vm encryption enable](/cli/azure/vm/encryption#enable). esempio Hello utilizza hello `$sp_id` e `$sp_password` variabili da hello precedente `ad sp create-for-rbac` comando:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

Comporta un tempo per hello disco crittografia processo toocomplete. Monitorare lo stato di hello del processo di hello con [Mostra la crittografia di vm az](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Mostra lo stato di Hello **EncryptionInProgress**. Attendere fino a quando lo stato di hello report del disco del sistema operativo hello **VMRestartPending**, quindi riavviare la macchina virtuale con [riavvio vm az](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

Hello il processo di crittografia del disco è finalizzato durante il processo di avvio di hello, quindi attendere qualche minuto prima di archiviare lo stato di hello di crittografia con **Mostra la crittografia di vm az**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

stato Hello deve segnalare ora sia disco hello del sistema operativo e dati come **Encrypted**.

## <a name="overview-of-disk-encryption"></a>Panoramica della crittografia dei dischi
I dischi virtuali delle VM Linux vengono crittografati a riposo mediante [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). Non è previsto alcun addebito per la crittografia dei dischi virtuali in Azure. Chiavi di crittografia vengono archiviate nell'insieme di credenziali di Azure chiave tramite software di protezione oppure è possibile importare o generare le chiavi in moduli di protezione Hardware (HSM) Certificate tooFIPS standard di livello 2 di 140-2. È possibile esercitare il controllo su queste chiavi di crittografia e sul loro uso. Queste chiavi di crittografia sono utilizzati tooencrypt e decrittografare i dischi virtuali collegati tooyour macchina virtuale. Un'entità servizio di Azure Active Directory offre un meccanismo protetto per il rilascio delle chiavi di crittografia all'accensione e allo spegnimento delle VM.

il processo di Hello per la crittografia di una macchina virtuale è il seguente:

1. Creare una chiave di crittografia in un insieme di credenziali delle chiavi di Azure.
2. Configurare hello crittografia chiave toobe utilizzabile per la crittografia dei dischi.
3. chiave di crittografia hello tooread dall'hello insieme di credenziali chiave di Azure, creare un servizio di Azure Active Directory principale con le autorizzazioni appropriate di hello.
4. Eseguire hello comando tooencrypt i dischi virtuali, specifica dell'entità servizio di Azure Active Directory hello e appropriato toobe chiave crittografica utilizzata.
5. le entità richieste di servizio Azure Active Directory Hello hello chiave di crittografia richiesto dall'insieme di credenziali chiave di Azure.
6. i dischi virtuali Hello vengono crittografati tramite la chiave crittografica hello fornito.

## <a name="encryption-process"></a>Processo di crittografia
Crittografia del disco si basa su hello i componenti aggiuntivi seguenti:

* **Insieme di credenziali chiave di Azure** -utilizzate le chiavi di crittografia toosafeguard e segreti utilizzati per il processo di crittografia/decrittografia hello disco.
  * Se disponibile, è possibile usare un insieme di credenziali delle chiavi di Azure esistente. Non si dispone toodedicate i dischi tooencrypting un insieme di credenziali chiave.
  * limiti amministrativi tooseparate e visibilità chiave, è possibile creare un insieme di credenziali chiave dedicato.
* **Azure Active Directory** : handle hello lo scambio sicuro di chiavi di crittografia necessarie e richiesta l'autenticazione per le azioni.
  * In genere, è possibile inserire l'applicazione in un'istanza esistente di Azure Active Directory.
  * entità servizio Hello fornisce un meccanismo protetto di toorequest e generato le chiavi di crittografia appropriato hello. Non si sta procedendo a sviluppare un'applicazione reale integrata con Azure Active Directory.

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

## <a name="create-azure-key-vault-and-keys"></a>Creare le chiavi e l'insieme di credenziali delle chiavi di Azure
È necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login). In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono *myResourceGroup*, *myKey* e *myVM*.

primo passaggio Hello è toocreate toostore un insieme di credenziali chiave Azure le chiavi di crittografia. Insieme di credenziali chiave di Azure è possibile archiviare le chiavi, i segreti, o le password che consentono di toosecurely implementano nelle applicazioni e servizi. Per la crittografia del disco virtuale, si usa l'insieme di credenziali chiave toostore una chiave di crittografia che viene utilizzato tooencrypt o decrittografare i dischi virtuali.

Abilitare il provider di credenziali chiave hello nella sottoscrizione di Azure con [registro provider az](/cli/azure/provider#register) e creare un gruppo di risorse con [gruppo az creare](/cli/azure/group#create). esempio Hello crea il nome di un gruppo di risorse *myResourceGroup* in hello `eastus` percorso:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Hello insieme credenziali chiavi Azure contenente hello le chiavi di crittografia e calcolo associato risorse, ad esempio hello macchina virtuale stessa e di archiviazione devono trovarsi nella hello stessa area. Creare un insieme di credenziali chiave di Azure con [keyvault az creare](/cli/azure/keyvault#create) e abilitare hello insieme di credenziali chiave per l'utilizzo con crittografia del disco. Specificare un nome univoco di Key Vault per *keyvault_name* come indicato di seguito:

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

È possibile archiviare le chiavi di crittografia usando il software o il modulo di protezione hardware. L'uso di un modulo di protezione hardware richiede un insieme di credenziali delle chiavi premium. È un toocreating costi aggiuntivi premium insieme di credenziali chiave anziché standard insieme di credenziali chiave che archivia le chiavi protette tramite software. aggiungere un insieme di credenziali chiave premium nel precedente passaggio hello toocreate `--sku Premium` toohello comando. Hello esempio seguente usa le chiavi protette tramite software poiché è stato creato un insieme di credenziali chiave standard.

Per entrambi i modelli di protezione, hello piattaforma Azure deve toobe concesso accesso toorequest hello chiavi di crittografia quando si avvia i dischi virtuali hello toodecrypt hello macchina virtuale. Creare una chiave di crittografia nell'insieme di credenziali delle chiavi con [az keyvault key create](/cli/azure/keyvault/key#create). esempio Hello crea una chiave denominata *myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Creare hello dell'entità servizio di Azure Active Directory
Quando i dischi virtuali vengono crittografati o decrittografati, specificare l'autenticazione di account toohandle hello e lo scambio delle chiavi di crittografia dall'insieme di credenziali chiave. Questo account, un'entità di servizio di Azure Active Directory consente hello piattaforma Azure toorequest hello appropriato le chiavi di crittografia per conto di hello macchina virtuale. Un'istanza di Azure Active Directory predefinita è già disponibile nella sottoscrizione, anche se molte organizzazioni hanno directory di Azure Active Directory dedicate.

Creare un'entità servizio usando Azure Active Directory con [az ad sp creare-per-rbac](/cli/azure/ad/sp#create-for-rbac). Hello di esempio seguente legge i valori hello per un'entità servizio hello Id e la password per l'uso nei comandi di versioni successive:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

password di Hello viene visualizzata solo quando si crea il servizio di hello principale. Se si desidera, visualizzare e registrare hello password (`echo $sp_password`). È possibile elencare le entità servizio con [az ad sp list](/cli/azure/ad/sp#list) e visualizzare informazioni aggiuntive su un'entità servizio specifica con [az ad sp show](/cli/azure/ad/sp#show).

toosuccessfully crittografare o decrittografare i dischi virtuali, le autorizzazioni sulla chiave di crittografia hello archiviati nell'insieme di credenziali chiave devono essere principale tooread hello chiavi del set toopermit hello Azure Active Directory del servizio. Impostare le autorizzazioni per l'insieme di credenziali delle chiavi con [az keyvault set-policy](/cli/azure/keyvault#set-policy). Nell'esempio seguente di hello, hello ID entità servizio viene fornito da hello precedente comando:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a>Crea macchina virtuale
tooactually crittografare alcuni dischi virtuali, consente di creare una macchina virtuale e aggiungere un disco dati. Creare una macchina virtuale tooencrypt con [creare vm az](/cli/azure/vm#create) e collegare un disco dati di 5 Gb. Solo determinate immagini di marketplace supportano la crittografia del disco. esempio Hello crea una macchina virtuale denominata *myVM* utilizzando un **CentOS 7.2n** immagine:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH tramite VM tooyour hello `publicIpAddress` illustrato nell'output di hello di hello precedente comando. Creare una partizione e un file System, quindi montare il disco di dati hello. Per ulteriori informazioni, vedere [connettersi tooa nuovo disco VM Linux toomount hello](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Chiudere la sessione SSH.


## <a name="encrypt-virtual-machine"></a>Crittografare una macchina virtuale
tooencrypt hello i dischi virtuali, riunire tutti i componenti precedenti hello:

1. Specificare hello entità servizio di Azure Active Directory e una password.
2. Specificare hello insieme di credenziali chiave toostore hello metadati per i dischi crittografati.
3. Specificare hello toouse di chiavi di crittografia per hello effettivo crittografia e decrittografia.
4. Specificare se si desidera tooencrypt hello del sistema operativo disco, i dischi dati hello o tutti.

Crittografare la macchina virtuale con [az vm encryption enable](/cli/azure/vm/encryption#enable). esempio Hello utilizza hello `$sp_id` e `$sp_password` variabili da hello precedente `ad sp create-for-rbac` comando:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

Comporta un tempo per hello disco crittografia processo toocomplete. Monitorare lo stato di hello del processo di hello con [Mostra la crittografia di vm az](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

l'output è simile toohello seguente esempio troncato Hello:

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

Attendere fino a quando lo stato di hello report del disco del sistema operativo hello **VMRestartPending**, quindi riavviare la macchina virtuale con [riavvio vm az](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

Hello il processo di crittografia del disco è finalizzato durante il processo di avvio di hello, quindi attendere qualche minuto prima di archiviare lo stato di hello di crittografia con **Mostra la crittografia di vm az**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

stato Hello deve segnalare ora sia disco hello del sistema operativo e dati come **Encrypted**.


## <a name="add-additional-data-disks"></a>Aggiungere ulteriori dischi dati
Dopo che sono stati crittografati i dischi dati, è possibile in seguito si aggiungono altri dischi virtuali tooyour VM e anche crittografarle. Ad esempio, consente di aggiungere un secondo tooyour disco virtuale VM come segue:

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

Eseguire di nuovo hello comando tooencrypt hello i dischi virtuali come indicato di seguito:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a>Passaggi successivi
* Per altre informazioni sulla gestione dell'insieme di credenziali delle chiavi di Azure, tra cui come eliminare chiavi crittografiche e insiemi di credenziali, vedere [Gestire l'insieme di credenziali delle chiavi tramite l'interfaccia della riga di comando](../../key-vault/key-vault-manage-with-cli2.md).
* Per ulteriori informazioni sulla crittografia del disco, ad esempio la preparazione di un tooAzure di tooupload macchina virtuale personalizzata crittografato, vedere [crittografia del disco Azure](../../security/azure-security-disk-encryption.md).
