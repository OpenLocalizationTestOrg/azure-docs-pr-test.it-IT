---
title: toocreate aaaHow, gestire o eliminare un account di archiviazione nel portale di Azure hello | Documenti Microsoft
description: Creare un nuovo account di archiviazione, gestire le chiavi di accesso di account o eliminare un account di archiviazione nel portale di Azure hello. Informazioni sugli account di archiviazione Standard e Premium.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 87c37da0-6cc6-4d88-a330-ef2896a1531d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
f1_keywords: sql13.swb.windowsazurestorage.connect.f1
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: c11c6509e192170db4812f47c389fc1009b94daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>Informazioni sugli account di archiviazione di Azure
[!INCLUDE [storage-selector-portal-create-storage-account](../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

## <a name="overview"></a>Panoramica
Un account di archiviazione di Azure fornisce un toostore spazio dei nomi univoco e accedere agli oggetti di dati di archiviazione di Azure. Tutti gli oggetti in un account di archiviazione vengono fatturati insieme come gruppo. Per impostazione predefinita, i dati di hello nell'account di sono disponibili solo tooyou, proprietario dell'account hello.

[!INCLUDE [storage-account-types-include](../../includes/storage-account-types-include.md)]

## <a name="storage-account-billing"></a>Fatturazione dell'account di archiviazione
[!INCLUDE [storage-account-billing-include](../../includes/storage-account-billing-include.md)]

> [!NOTE]
> Quando si crea una macchina virtuale di Azure, un account di archiviazione viene creato automaticamente automaticamente nel percorso di distribuzione hello se non hai già un account di archiviazione in tale percorso. È pertanto necessario toofollow procedure hello toocreate un account di archiviazione per i dischi di macchina virtuale. nome account di archiviazione Hello si baserà sul nome della macchina virtuale hello. Vedere hello [documentazione di macchine virtuali di Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) per altri dettagli.
> 
> 

## <a name="storage-account-endpoints"></a>Endpoint dell'account di archiviazione
Ogni oggetto archiviato in Archiviazione di Azure ha un indirizzo URL univoco. formati di nome account di archiviazione Hello hello sottodominio di tale indirizzo. Form Hello combinazione di nome di sottodominio e il dominio, ovvero servizio tooeach specifico, un *endpoint* dell'account di archiviazione.

Ad esempio, se l'account di archiviazione denominato *mystorageaccount*, gli endpoint predefiniti hello dell'account di archiviazione sono:

* Servizio BLOB: http://*mystorageaccount*.blob.core.windows.net
* Servizio tabelle: http://*mystorageaccount*.table.core.windows.net
* Servizio coda: http://*mystorageaccount*.queue.core.windows.net
* Servizio file: http://*mystorageaccount*.file.core.windows.net

> [!NOTE]
> Un account di archiviazione Blob espone solo endpoint del servizio Blob hello.
> 
> 

Hello URL per l'accesso a un oggetto in un account di archiviazione viene creato aggiungendo il percorso dell'oggetto hello in endpoint toohello dell'account di archiviazione hello. Ad esempio, il formato di un indirizzo è simile al seguente: http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*.

È anche possibile configurare un toouse nome di dominio personalizzato con l'account di archiviazione. Per informazioni dettagliate sugli account di archiviazione classici, vedere [Configurare un nome di dominio personalizzato per l'endpoint di archiviazione BLOB](storage-custom-domain-name.md) . Per gli account di archiviazione di gestione delle risorse, questa funzionalità non è stato aggiunto toohello [portale di Azure](https://portal.azure.com) ancora, ma è possibile configurarlo con PowerShell. Per ulteriori informazioni, vedere hello [Set AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607146.aspx) cmdlet.  

## <a name="create-a-storage-account"></a>Creare un account di archiviazione
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nel menu Hub hello, selezionare **New** -> **archiviazione** -> **account di archiviazione**.
3. Immettere un nome per l'account di archiviazione. Vedere [gli endpoint di account di archiviazione](#storage-account-endpoints) per informazioni dettagliate su come nome di account di archiviazione hello saranno tooaddress utilizzati oggetti di archiviazione di Azure.
   
   > [!NOTE]
   > I nomi degli account di archiviazione devono avere una lunghezza compresa tra 3 e 24 caratteri e possono contenere solo numeri e lettere minuscole.
   > 
   > Nome dell'account di archiviazione deve essere univoco all'interno di Azure. portale di Azure Hello indicherà se si seleziona nome account di archiviazione hello è già in uso.
   > 
   > 
4. Specificare hello toobe di modello di distribuzione usato: **Gestione risorse** o **classico**. **Gestione risorse** hello consiglia di modello di distribuzione. Per altre informazioni, vedere [Comprendere la distribuzione di Gestione delle risorse e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).
   
   > [!NOTE]
   > Account di archiviazione BLOB può essere creato solo tramite modello di distribuzione di gestione risorse di hello.
   > 
   > 
5. Selezionare il tipo di hello di account di archiviazione: **generici** o **nell'archiviazione Blob**. **Interesse generale** hello predefinito.
   
    Se **generici** è stata selezionata, quindi specificare il livello di prestazioni hello: **Standard** o **Premium**. valore predefinito di Hello è **Standard**. Per ulteriori informazioni sugli account di archiviazione standard e premium, vedere [tooMicrosoft introduzione di archiviazione di Azure](storage-introduction.md) e [archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro di macchina virtuale Azure](storage-premium-storage.md).
   
    Se **nell'archiviazione Blob** è stata selezionata, quindi specificare il livello di accesso di hello: **Hot** o **sporadico**. valore predefinito di Hello è **Hot**. Per informazioni dettagliate, vedere l'articolo [Archivio BLOB di Azure: livelli di archiviazione ad accesso frequente e sporadico](storage-blob-storage-tiers.md) .
6. Selezionare l'opzione replication hello per account di archiviazione hello: **LRS**, **GRS**, **RA-GRS**, o **ZRS**. valore predefinito di Hello è **RA-GRS**. Per altre informazioni sulle opzioni di replica di Archiviazione di Azure, vedere [Replica di Archiviazione di Azure](storage-redundancy.md).
7. Selezionare la sottoscrizione di hello in cui si desidera toocreate hello nuovo account di archiviazione.
8. Specificare un nuovo gruppo di risorse o selezionarne uno esistente. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
9. Selezionare l'area geografica dell'account di archiviazione hello. Per altre informazioni sui servizi disponibili in aree specifiche, vedere [Aree di Azure](https://azure.microsoft.com/regions/#services) .
10. Fare clic su **crea** account di archiviazione toocreate hello.

## <a name="manage-your-storage-account"></a>Gestire l'account di archiviazione
### <a name="change-your-account-configuration"></a>Modificare la configurazione dell'account
Dopo aver creato l'account di archiviazione, è possibile modificare la configurazione, ad esempio per cambiare l'opzione di replica hello utilizzato per l'account di hello o modifica i livelli di accesso di hello per un account di archiviazione Blob. In hello [portale di Azure](https://portal.azure.com), passare l'account di archiviazione tooyour, trovare e fare clic su **configurazione** in **impostazioni** tooview e/o modifica configurazione dell'account hello.

> [!NOTE]
> In base al livello di prestazioni hello che scelto durante la creazione di account di archiviazione hello, alcune opzioni di replica potrebbero non essere disponibili.
> 
> 

Modifica l'opzione di replica hello verrà modificato il piano tariffario. Per informazioni più dettagliate, vedere la pagina [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/) .

Per i Blob possono essere soggette a modifica il livello di accesso di hello gli account di archiviazione gli addebiti per hello modificare inoltre toochanging i prezzi. Vedere hello [Blob gli account di archiviazione - prezzi e fatturazione](storage-blob-storage-tiers.md#pricing-and-billing) per altri dettagli.

### <a name="manage-your-storage-access-keys"></a>Gestire le chiavi di accesso alle risorse di archiviazione
Quando si crea un account di archiviazione, Azure genera due chiavi di accesso archiviazione a 512 bit, che vengono usate per l'autenticazione quando si accede all'account di archiviazione hello. Fornendo due chiavi di accesso di archiviazione, Azure consente chiavi hello tooregenerate senza servizio di archiviazione tooyour interruzione o del servizio di accesso toothat.

> [!NOTE]
> È consigliabile non condividere le chiavi di accesso alle risorse di archiviazione con altri utenti. risorse di toostorage toopermit accesso senza dover assegnare le chiavi di accesso, è possibile utilizzare un *firma di accesso condiviso*. Una firma di accesso condiviso fornisce risorse tooa di accesso dell'account per un intervallo che definisce e con autorizzazioni di hello specificato. Vedere [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) (Uso di firme di accesso condiviso) per altre informazioni.
> 
> 
<a id="view-and-copy-storage-access-keys"/></a>
#### <a name="view-and-copy-storage-access-keys"></a>Visualizzare e copiare le chiavi di accesso alle risorse di archiviazione
In hello [portale di Azure](https://portal.azure.com)passare tooyour account di archiviazione, fare clic su **tutte le impostazioni** e quindi fare clic su **le chiavi di accesso** tooview, copiare e rigenerare le chiavi di accesso di account. Hello **chiavi di accesso** pannello include anche le stringhe di connessione configurati in precedenza utilizzando le chiavi primarie e secondarie, che è possibile copiare toouse nelle applicazioni.

#### <a name="regenerate-storage-access-keys"></a>Rigenerazione delle chiavi di accesso alle risorse di archiviazione
Si consiglia di modificare le chiavi di accesso hello tooyour dell'account di archiviazione periodicamente toohelp tenere le connessioni di archiviazione sicura. Due chiavi di accesso vengono assegnate in modo che sia possibile gestire account di archiviazione toohello connessioni tramite una chiave di accesso, mentre si rigenera hello altre chiavi di accesso.

> [!WARNING]
> Rigenerare le chiavi di accesso possono influire sulla servizi in Azure, nonché di applicazioni che dipendono da account di archiviazione hello. Tutti i client che utilizzano account di archiviazione di hello accesso tooaccess chiave hello devono essere una nuova chiave di hello toouse aggiornato.
> 
> 

**Servizi multimediali** -se si dispone di servizi multimediali che dipendono da account di archiviazione, è necessario risincronizzare le chiavi di accesso hello con il servizio multimediale dopo aver rigenerato chiavi hello.

**Applicazioni** : se si dispone di applicazioni web o account di archiviazione hello utilizzo dei servizi cloud, si perderanno le connessioni hello se si rigenerano le chiavi, a meno che non si esegue il rollback delle chiavi.

**Esplora archivi** : se si utilizza uno [applicazioni Esplora archiviazione](storage-explorers.md), sarà probabilmente necessario chiave di archiviazione hello tooupdate usati da tali applicazioni.

Ecco il processo di hello rotazione delle chiavi di accesso di archiviazione:

1. Aggiornare le stringhe di connessione hello nella chiave di accesso secondaria applicazione codice tooreference hello hello dell'account di archiviazione.
2. Rigenerare la chiave di accesso primaria hello per l'account di archiviazione. In hello **chiavi di accesso** pannello, fare clic su **rigenerare Key1**e quindi fare clic su **Sì** tooconfirm che si desidera toogenerate una nuova chiave.
3. Aggiornare le stringhe di connessione hello nella chiave di accesso primaria nuovo codice tooreference hello.
4. Chiave di accesso secondaria rigenerare hello in hello stesso modo.

## <a name="delete-a-storage-account"></a>Eliminare un account di archiviazione
tooremove un account di archiviazione non è più in uso, passare l'account di archiviazione toohello in hello [portale di Azure](https://portal.azure.com), fare clic su **eliminare**. Se si elimina un account di archiviazione, hello conto, inclusi tutti i dati nell'account hello.

> [!WARNING]
> È Impossibile toorestore un account di archiviazione eliminato o recuperare contenuto hello in essa contenute prima dell'eliminazione. Essere tooback che backup di tutti i desideri toosave prima di eliminare account hello. Ciò vale anche per tutte le risorse nell'account hello, quando si elimina un blob, tabella, una coda o un file, questo viene eliminato definitivamente.
> 
> 

toodelete un account di archiviazione associato a una macchina virtuale di Azure, è innanzitutto necessario assicurarsi che i dischi di macchina virtuale sono stati eliminati. Se non si elimina innanzitutto i dischi di macchina virtuale, quando si tenta di toodelete account di archiviazione, verranno vedere un messaggio di errore simile a:

    Failed toodelete storage account <vm-storage-account-name>. Unable toodelete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.

Se l'account di archiviazione hello Usa modello di distribuzione classica hello, è possibile rimuovere il disco di macchina virtuale hello attenendosi alla procedura seguente in hello [portale di Azure](https://manage.windowsazure.com):

1. Passare toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Passare toohello scheda di macchine virtuali.
3. Fare clic sulla scheda dischi hello.
4. Selezionare il disco dati, quindi fare clic su Elimina disco.
5. immagini del disco toodelete, passare scheda immagini toohello ed eliminare tutte le immagini archiviate nell'account hello.

Per ulteriori informazioni, vedere hello [macchina virtuale di Azure documentazione](http://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="next-steps"></a>Passaggi successivi
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma, disponibile da Microsoft che consente di toowork visivamente i dati di archiviazione di Azure in Windows, macOS e Linux.
* [Livelli Frequente e Non frequente dell'archiviazione BLOB di Azure](storage-blob-storage-tiers.md)
* [Replica di Archiviazione di Azure](storage-redundancy.md)
* [Configurare le stringhe di connessione di archiviazione di Azure](storage-configure-connection-string.md)
* [Trasferimento dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md)
* Visitare hello [Blog del Team di archiviazione Azure](http://blogs.msdn.com/b/windowsazurestorage/).

