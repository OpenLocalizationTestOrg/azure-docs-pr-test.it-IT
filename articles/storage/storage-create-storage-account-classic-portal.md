---
title: toocreate aaaHow, gestire o eliminare un account di archiviazione nel portale di Azure classico hello | Documenti Microsoft
description: Creare un nuovo account di archiviazione, gestire le chiavi di accesso di account o eliminare un account di archiviazione nel portale di Azure hello. Informazioni sugli account di archiviazione Standard e Premium.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 5e4f4360-3f81-4d63-a0b1-e7771b67af11
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 6ee2359e02c7c9e9c111e1fc87a6160bb8b785b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>Informazioni sugli account di archiviazione di Azure
[!INCLUDE [storage-selector-portal-create-storage-account](../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-try-azure-tools](../../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Panoramica
Consente un account di archiviazione di Azure accedere toohello servizi Azure Blob, coda, tabella e File in archiviazione di Azure. L'account di archiviazione fornisce spazio dei nomi univoco hello per gli oggetti di data di archiviazione di Azure. Per impostazione predefinita, i dati di hello nell'account di sono disponibili solo tooyou, proprietario dell'account hello.

Sono disponibili due tipi di account di archiviazione:

* Un account di archiviazione standard include l'archiviazione BLOB, tabelle, di accodamento e file.
* Un account di archiviazione Premium attualmente supporta solo dischi di macchine virtuali di Azure. Per una panoramica approfondita del servizio di archiviazione Premium, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](storage-premium-storage.md) .

## <a name="storage-account-billing"></a>Fatturazione dell'account di archiviazione
L'importo fatturato per l'uso di Archiviazione di Azure dipende dall'account di archiviazione. I costi di archiviazione sono determinati da quattro fattori: capacità di archiviazione, schema di replica, transazioni di archiviazione e uscita dei dati.

* Capacità di archiviazione si riferisce toohow notevolmente il numero di account di archiviazione si utilizza toostore dati. il costo di Hello semplicemente archiviazione dei dati è determinato dalla quantità di dati vengono archiviati e modalità di replica.
* La replica determina quante copie dei dati vengono gestite in una sola volta e in quali posizioni.
* Le transazioni si riferiscono tooall lettura e scrittura operazioni tooAzure archiviazione.
* Dati in uscita fa riferimento toodata trasferita all'esterno di un'area di Azure. Quando si accedono a dati hello nell'account di archiviazione da un'applicazione che non è in esecuzione in hello stessa area, fatto che l'applicazione è un servizio cloud o un altro tipo di applicazione, quindi vengono addebitati i dati in uscita. (Per servizi di Azure, è possibile eseguire passaggi toogroup i dati e servizi in hello centri tooreduce stessi dati o eliminare i costi di uscita di dati.)  

Hello [prezzi di archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage) pagina vengono fornite informazioni dettagliate sui prezzi per la capacità di archiviazione, replica e le transazioni. Hello [dettagli prezzi dei trasferimenti di dati](https://azure.microsoft.com/pricing/details/data-transfers/) pagina vengono fornite informazioni dettagliate sui prezzi per i dati in uscita.

Per informazioni sugli obiettivi di capacità e prestazioni dell'account di archiviazione, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](storage-scalability-targets.md).

> [!NOTE]
> Quando si crea una macchina virtuale di Azure, un account di archiviazione viene creato automaticamente automaticamente nel percorso di distribuzione hello se non hai già un account di archiviazione in tale percorso. È pertanto necessario toofollow procedure hello toocreate un account di archiviazione per i dischi di macchina virtuale. nome account di archiviazione Hello si baserà sul nome della macchina virtuale hello. Vedere hello [documentazione di macchine virtuali di Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) per altri dettagli.
> 
> 

## <a name="create-a-storage-account"></a>Creare un account di archiviazione
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Fare clic su **New** hello sulla barra delle applicazioni nella parte inferiore di hello della pagina hello. Scegliere **Servizi dati** | **Archiviazione** e quindi fare clic su **Creazione rapida**.
   
    ![NewStorageAccount](./media/storage-create-storage-account-classic-portal/storage_NewStorageAccount.png)
3. In **URL**immettere un nome per l'account di archiviazione.
   
   > [!NOTE]
   > I nomi degli account di archiviazione devono avere una lunghezza compresa tra 3 e 24 caratteri e possono contenere solo numeri e lettere minuscole.
   > 
   > Nome dell'account di archiviazione deve essere univoco all'interno di Azure. Portale di Azure classico Hello indicherà se si seleziona nome account di archiviazione hello è già in uso.
   > 
   > 
   
    Vedere [gli endpoint di account di archiviazione](#storage-account-endpoints) sotto per informazioni dettagliate su come nome di account di archiviazione hello saranno tooaddress utilizzati oggetti di archiviazione di Azure.
4. In **posizione/gruppo di affinità**, selezionare un percorso per l'account di archiviazione è Chiudi tooyou tooyour clienti. Se i dati nell'account di archiviazione verranno eseguiti da un altro servizio di Azure, ad esempio una macchina virtuale di Azure o di un servizio cloud, è un gruppo di affinità da hello elenco toogroup tooselect account di archiviazione in hello nello stesso data center con altri servizi di Azure che si sta utilizzando tooimprove prestazioni e ridurre i costi.
   
    Si noti che è necessario selezionare un gruppo di affinità al momento della creazione dell'account di archiviazione. È possibile spostare un gruppo di affinità tooan account esistente. Per informazioni dettagliate sui gruppi di affinità, vedere [Condivisione del percorso del servizio con un gruppo di affinità](#service-co-location-with-an-affinity-group) più avanti.
   
   > [!IMPORTANT]
   > toodetermine i percorsi sono disponibili per la sottoscrizione, è possibile chiamare hello [l'elenco di tutti i provider di risorse](https://msdn.microsoft.com/library/azure/dn790524.aspx) operazione. provider toolist da PowerShell, chiamare [Get AzureLocation](https://msdn.microsoft.com/library/azure/dn757693.aspx). Da .NET, usare hello [elenco](https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.provideroperationsextensions.list.aspx) metodo della classe ProviderOperationsExtensions hello.
   > 
   > Per altre informazioni sui servizi disponibili in aree specifiche, vedere anche [Aree di Azure](https://azure.microsoft.com/regions/#services) .
   > 
   > 
5. Se si dispone di più di una sottoscrizione di Azure, hello **sottoscrizione** campo viene visualizzato. In **sottoscrizione**, immettere hello sottoscrizione di Azure che si desidera toouse hello account di archiviazione.
6. In **replica**, selezionare hello livello desiderato di replica per l'account di archiviazione. Hello consigliata l'opzione di replica è la replica con ridondanza geografica, che fornisce la durata massima per i dati. Per altre informazioni sulle opzioni di replica di Archiviazione di Azure, vedere [Replica di Archiviazione di Azure](storage-redundancy.md).
7. Fare clic su **Create Storage Account**.
   
    Potrebbe richiedere alcuni minuti toocreate account di archiviazione. stato hello toocheck, è possibile monitorare le notifiche di hello nella parte inferiore di hello di hello portale classico di Azure. Dopo aver creato l'account di archiviazione hello, il nuovo account di archiviazione è **Online** stato ed è pronto per l'utilizzo.

![StoragePage](./media/storage-create-storage-account-classic-portal/Storage_StoragePage.png)

### <a name="storage-account-endpoints"></a>Endpoint dell'account di archiviazione
Ogni oggetto archiviato in Archiviazione di Azure ha un indirizzo URL univoco. formati di nome account di archiviazione Hello hello sottodominio di tale indirizzo. Form Hello combinazione di nome di sottodominio e il dominio, ovvero servizio tooeach specifico, un *endpoint* dell'account di archiviazione.

Ad esempio, se l'account di archiviazione denominato *mystorageaccount*, gli endpoint predefiniti hello dell'account di archiviazione sono:

* Servizio BLOB: http://*mystorageaccount*.blob.core.windows.net
* Servizio tabelle: http://*mystorageaccount*.table.core.windows.net
* Servizio coda: http://*mystorageaccount*.queue.core.windows.net
* Servizio file: http://*mystorageaccount*.file.core.windows.net

È possibile visualizzare gli endpoint hello dell'account di archiviazione nel dashboard di archiviazione hello in hello [portale di Azure classico](https://manage.windowsazure.com) dopo aver creato l'account di hello.

Hello URL per l'accesso a un oggetto in un account di archiviazione viene creato aggiungendo il percorso dell'oggetto hello in endpoint toohello dell'account di archiviazione hello. Ad esempio, il formato di un indirizzo è simile al seguente: http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*.

È anche possibile configurare un toouse nome di dominio personalizzato con l'account di archiviazione. Per altri dettagli, vedere [Configurare un nome di dominio personalizzato per l'endpoint di archiviazione BLOB](storage-custom-domain-name.md) .

### <a name="service-co-location-with-an-affinity-group"></a>Condivisione del percorso del servizio con un gruppo di affinità
Un *gruppo di affinità* è un raggruppamento geografico dei servizi e delle VM di Azure con l'account di archiviazione di Azure. Un gruppo di affinità è possibile migliorare le prestazioni del servizio individuando i carichi di lavoro di computer in hello stesso data center o quasi destinatari hello. Inoltre, senza fatturazione spese in uscita quando si accede a dati in un account di archiviazione da un altro servizio che fa parte di hello stesso gruppo di affinità.

> [!NOTE]
> toocreate un gruppo di affinità, aprire hello <b>impostazioni</b> area di hello [portale classico di Azure](https://manage.windowsazure.com), fare clic su <b>gruppi di affinità</b>, quindi fare clic su <b>Aggiungi un gruppo di affinità</b> o hello <b>Aggiungi</b> pulsante. È anche possibile creare e gestire gruppi di affinità con hello API di gestione del servizio di Azure. Per altre informazioni, vedere <a href="http://msdn.microsoft.com/library/azure/ee460798.aspx">Operazioni sui gruppi di affinità</a>.
> 
> 

## <a name="view-copy-and-regenerate-storage-access-keys"></a>Visualizzare, copiare e rigenerare le chiavi di accesso alle risorse di archiviazione
Quando si crea un account di archiviazione, Azure genera due chiavi di accesso archiviazione a 512 bit, che vengono usate per l'autenticazione quando si accede all'account di archiviazione hello. Fornendo due chiavi di accesso di archiviazione, Azure consente chiavi hello tooregenerate senza servizio di archiviazione tooyour interruzione o del servizio di accesso toothat.

> [!NOTE]
> È consigliabile non condividere le chiavi di accesso alle risorse di archiviazione con altri utenti. risorse di toostorage toopermit accesso senza dover assegnare le chiavi di accesso, è possibile utilizzare un *firma di accesso condiviso*. Una firma di accesso condiviso fornisce risorse tooa di accesso dell'account per un intervallo che definisce e con autorizzazioni di hello specificato. Vedere [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) (Uso di firme di accesso condiviso) per altre informazioni.
> 
> 

In hello [portale di Azure classico](https://manage.windowsazure.com), utilizzare **Gestisci chiavi** nel dashboard di hello o hello **archiviazione** pagina tooview, copia e chiavi di accesso di archiviazione hello rigenerare utilizzati tooaccess hello servizi Blob, tabella e coda.

### <a name="copy-a-storage-access-key"></a>Copia di una chiave di accesso alle risorse di archiviazione
È possibile utilizzare **Gestisci chiavi** toocopy un toouse chiave di accesso di archiviazione in una stringa di connessione. stringa di connessione Hello richiede nome account di archiviazione hello e una chiave toouse dell'autenticazione. Per informazioni sulla configurazione connessione stringhe tooaccess servizi di archiviazione di Azure, vedere [configurare le stringhe di connessione di Azure Storage](storage-configure-connection-string.md).

1. In hello [portale di Azure classico](https://manage.windowsazure.com), fare clic su **archiviazione**, quindi fare clic su nome hello del dashboard di hello storage account tooopen hello.
2. Fare clic su **Manage Keys**.
   
     **Verrà aperto** Manage Access Keys.
   
    ![ManageKeys](./media/storage-create-storage-account-classic-portal/Storage_ManageKeys.png)
3. toocopy una chiave di accesso di archiviazione, testo chiave hello selezionare. Fare quindi clic con il pulsante destro del mouse e scegliere **Copy**.

### <a name="regenerate-storage-access-keys"></a>Rigenerazione delle chiavi di accesso alle risorse di archiviazione
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
2. Rigenerare la chiave di accesso primaria hello per l'account di archiviazione. In hello [portale di Azure classico](https://manage.windowsazure.com), dal dashboard di hello o hello **configura** pagina, fare clic su **Gestisci chiavi**. Fare clic su **rigenerare** in hello chiave di accesso primaria e quindi fare clic su **Sì** tooconfirm che si desidera toogenerate una nuova chiave.
3. Aggiornare le stringhe di connessione hello nella chiave di accesso primaria nuovo codice tooreference hello.
4. Rigenerare la chiave di accesso secondaria hello.

## <a name="delete-a-storage-account"></a>Eliminare un account di archiviazione
un account di archiviazione non è più in uso, utilizzare tooremove **eliminare** nel dashboard di hello o hello **configura** pagina. **Eliminare** eliminazioni hello account di archiviazione intero, inclusi tutti i BLOB di hello, tabelle e code nell'account hello.

> [!WARNING]
> È Impossibile toorestore un account di archiviazione eliminato o recuperare contenuto hello in essa contenute prima dell'eliminazione. Essere tooback che backup di tutti i desideri toosave prima di eliminare account hello. Ciò vale anche per tutte le risorse nell'account hello, quando si elimina un blob, tabella, una coda o un file, questo viene eliminato definitivamente.
> 
> Se l'account di archiviazione contiene i file di disco rigido virtuale per una macchina virtuale di Azure, è necessario eliminare eventuali immagini e dischi che utilizzano tali file di disco rigido virtuale prima di poter eliminare l'account di archiviazione hello. Se è in esecuzione e poi la elimini, arrestare innanzitutto macchina virtuale hello. toodelete dischi, passare toohello **dischi** scheda ed eliminare i dischi non esiste. immagini toodelete, passare toohello **immagini** scheda ed eliminare tutte le immagini archiviate nell'account hello.
> 
> 

1. In hello [portale di Azure classico](https://manage.windowsazure.com), fare clic su **archiviazione**.
2. Fare clic nella voce di account di archiviazione di hello, tranne che il nome di hello e quindi fare clic su **eliminare**.
   
     -Oppure-
   
    Fare clic sul nome del dashboard di hello storage account tooopen hello hello e quindi fare clic su **eliminare**.
3. Fare clic su **Sì** tooconfirm cui account di archiviazione toodelete hello.

## <a name="next-steps"></a>Passaggi successivi
* toolearn più sull'archiviazione di Azure, vedere hello [documentazione di archiviazione di Azure](https://azure.microsoft.com/documentation/services/storage/).
* Visitare hello [Blog del Team di archiviazione Azure](http://blogs.msdn.com/b/windowsazurestorage/).
* [Trasferimento dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md)

