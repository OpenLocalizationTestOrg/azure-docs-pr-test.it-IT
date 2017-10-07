---
title: aaaEncryption in archivio Azure Data Lake | Documenti Microsoft
description: Informazioni sul funzionamento della crittografia e della rotazione delle chiavi in Azure Data Lake Store
services: data-lake-store
documentationcenter: 
author: yagupta
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 4/14/2017
ms.author: yagupta
ms.openlocfilehash: a9f3a2dce8232deba93005594d1e6a21e9c0cbee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encryption-of-data-in-azure-data-lake-store"></a>Crittografia dei dati in Azure Data Lake Store

La crittografia in Azure Data Lake Store consente di proteggere i dati, implementare criteri di sicurezza aziendali e soddisfare i requisiti di conformità normativi. In questo articolo viene fornita una panoramica di progettazione hello e vengono illustrati alcuni aspetti tecnici di hello dell'implementazione.

Data Lake Store supporta la crittografia dei dati sia inattivi che in transito. Per i dati inattivi, Data Lake Store supporta la crittografia trasparente "attivata per impostazione predefinita". Di seguito è riportata una spiegazione più dettagliata:

* **In per impostazione predefinita**: quando si crea un nuovo account archivio Data Lake, impostazione predefinita hello abilita la crittografia. Successivamente, i dati archiviati nell'archivio Data Lake sono sempre crittografato toostoring precedenti nel supporto permanente. Questo è il comportamento di hello per tutti i dati e non può essere modificato dopo la creazione di un account.
* **Transparent**: archivio Data Lake automaticamente crittografa i dati precedenti toopersisting e li decrittografa tooretrieval precedente dei dati. crittografia Hello configurata e gestita a livello di archivio Data Lake hello da un amministratore. Non vengono apportate modifiche toohello dati alle API di accesso. Non sono quindi necessarie modifiche nelle applicazioni e nei servizi che interagiscono con Data Lake Store a causa della crittografia.

Anche i dati in transito (noti anche come dati in movimento) vengono sempre crittografati in Data Lake Store. Inoltre supporto toopersistent toostoring precedenti dati tooencrypting hello dati vengono sempre anche protetti in transito tramite HTTPS. HTTPS è l'unico protocollo hello è supportato per hello che interfacce REST di archivio Data Lake. Hello diagramma seguente illustra come dati diventano crittografati nell'archivio Data Lake:

![Diagramma della crittografia dei dati in Data Lake Store](./media/data-lake-store-encryption/fig1.png)


## <a name="set-up-encryption-with-data-lake-store"></a>Configurare la crittografia con Data Lake Store

La crittografia per Data Lake Store viene configurata durante la creazione di un account ed è sempre abilitata per impostazione predefinita. È possibile gestire le chiavi di hello autonomamente o consentire toomanage archivio Data Lake per si (si tratta di hello predefinito).

Per altre informazioni, vedere la [Introduzione](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).

## <a name="how-encryption-works-in-data-lake-store"></a>Come funziona la crittografia in Data Lake Store

Hello informazioni seguenti sono descritte come chiavi di crittografia master toomanage e illustra hello tre diversi tipi di chiavi, è possibile usare nella crittografia dei dati per l'archivio Data Lake.

### <a name="master-encryption-keys"></a>Chiavi di crittografia master

Data Lake Store offre due modalità per la gestione delle chiavi di crittografia master. Per il momento, si supponga che la chiave di crittografia master hello è chiave di primo livello hello. Chiave di crittografia master toohello di accesso è necessario toodecrypt tutti i dati archiviati in archivio Data Lake.

come indicato di seguito sono riportati i Hello due modalità per gestire la chiave di crittografia master hello:

*   Chiavi gestite dal servizio
*   Chiavi gestite dal cliente

In entrambe le modalità, la chiave di crittografia master hello è protetto da archiviare nell'insieme di credenziali chiave di Azure. Insieme di credenziali chiave è un servizio completamente gestito, estremamente sicuro in Azure che può essere utilizzati toosafeguard le chiavi di crittografia. Per altre informazioni, vedere [Key Vault](https://azure.microsoft.com/services/key-vault).

Di seguito è riportato un confronto delle funzionalità fornite da due modalità di gestione MEKs hello di hello breve.

|  | Chiavi gestite dal servizio | Chiavi gestite dal cliente |
| --- | --- | --- |
|Come vengono archiviati i dati?|Crittografia sempre attiva toobeing precedenti archiviati.|Crittografia sempre attiva toobeing precedenti archiviati.|
|In cui è archiviato hello chiave di crittografia Master?|Insieme di credenziali delle chiavi|Insieme di credenziali delle chiavi|
|Sono qualsiasi tipo di crittografia chiavi archiviate in hello deselezionare all'esterno dell'insieme di credenziali chiave? |No|No|
|Hello MEK può essere recuperato dall'insieme di credenziali chiave?|No. Dopo aver hello che MEK viene archiviato nell'insieme di credenziali chiave, utilizzabile solo per la crittografia e decrittografia.|No. Dopo aver hello che MEK viene archiviato nell'insieme di credenziali chiave, utilizzabile solo per la crittografia e decrittografia.|
|Il proprietario dell'istanza di insieme di credenziali chiave hello e hello MEK?|Hello servizio archivio Data Lake|Si è proprietari di istanza di insieme di credenziali chiave hello, che appartiene alla sottoscrizione Azure. Hello MEK nell'insieme di credenziali chiave può essere gestito dal software o hardware.|
|È possibile revocare l'accesso toohello MEK per il servizio archivio Data Lake hello?|No|Sì. È possibile gestire gli elenchi di controllo di accesso nell'insieme di credenziali chiave e rimuovere l'accesso controllo voci toohello identità del servizio per il servizio archivio Data Lake hello.|
|È possibile in modo permanente eliminare hello MEK?|No|Sì. Se si elimina hello MEK dall'insieme di credenziali chiave, non è possibile decrittografare i dati di hello in hello account archivio Data Lake a chiunque, inclusi il servizio di archivio Data Lake hello. <br><br> Se è stato in modo esplicito backup hello MEK precedente toodeleting dall'insieme di credenziali chiave, può essere ripristinato hello MEK e dati hello possono quindi essere recuperati. Tuttavia, se non backup hello MEK precedente toodeleting dall'insieme di credenziali chiave, hello dati in hello account archivio Data Lake non possono mai essere decrittografati successivamente.|


A parte questa differenza di chi gestisce hello MEK e istanza insieme di credenziali chiave hello in cui si trova, rest hello della progettazione hello è hello uguale per entrambe le modalità.

Quando si sceglie la modalità di hello per hello chiavi di crittografia master è seguente hello tooremember importanti:

*   È possibile scegliere se il cliente toouse gestita chiavi o le chiavi del servizio gestito quando si esegue il provisioning di un account archivio Data Lake.
*   Dopo il provisioning di un account archivio Data Lake, non è possibile modificare la modalità di hello.

### <a name="encryption-and-decryption-of-data"></a>Crittografia e decrittografia dei dati

Esistono tre tipi di chiavi usate nella progettazione di hello crittografia dei dati. Hello nella tabella seguente fornisce un riepilogo:

| Chiave                   | Abbreviazione | Elemento associato | Posizione di archiviazione                             | Tipo       | Note                                                                                                   |
|-----------------------|--------------|-----------------|----------------------------------------------|------------|---------------------------------------------------------------------------------------------------------|
| Chiave di crittografia master | MEK          | Un account Data Lake Store | Insieme di credenziali di chiave                              | Asimmetrica | Può essere gestita da Data Lake Store o dall'utente.                                                              |
| Chiave di crittografia dei dati   | DEK          | Un account Data Lake Store | Risorsa di archiviazione persistente, gestita dal servizio Data Lake Store | Simmetrica  | chiave di Decrittografia Hello viene crittografato hello MEK. Hello che DEK crittografato è ciò che viene archiviato in un supporto permanente. |
| Chiave di crittografia a blocchi  | BEK          | Un blocco di dati | Nessuno                                         | Simmetrica  | Hello BEK è derivato da hello chiave di Decrittografia e il blocco di dati di hello.                                                      |

Hello seguente diagramma vengono illustrati questi concetti:

![Chiavi nella crittografia dei dati](./media/data-lake-store-encryption/fig2.png)

#### <a name="pseudo-algorithm-when-a-file-is-toobe-decrypted"></a>Algoritmo di pseudo quando un file è toobe decrittografata:
1.  Controllare se hello chiave di Decrittografia per account archivio Data Lake hello è memorizzato nella cache e pronta per l'utilizzo.
    - In caso contrario, leggere hello crittografato una chiave di Decrittografia dall'archivio permanente e inviarlo tooKey insieme di credenziali toobe decrittografato. Hello cache decrittografata una chiave di Decrittografia in memoria. È ora pronto toouse.
2.  Per ogni blocco di dati nel file hello:
    - Blocco crittografato hello di lettura dei dati dall'archivio permanente.
    - Generare hello BEK dalla chiave di Decrittografia hello e blocco di crittografato hello di dati.
    - Utilizzare i dati di toodecrypt BEK hello.


#### <a name="pseudo-algorithm-when-a-block-of-data-is-toobe-encrypted"></a>L'algoritmo pseudo quando un blocco di dati è toobe crittografato:
1.  Controllare se hello chiave di Decrittografia per account archivio Data Lake hello è memorizzato nella cache e pronta per l'utilizzo.
    - In caso contrario, leggere hello crittografato una chiave di Decrittografia dall'archivio permanente e inviarlo tooKey insieme di credenziali toobe decrittografato. Hello cache decrittografata una chiave di Decrittografia in memoria. È ora pronto toouse.
2.  Generare un BEK univoco per il blocco di hello di dati da hello chiave di Decrittografia.
3.  Crittografare il blocco di dati hello con hello BEK, utilizzando la crittografia AES-256.
4.  Blocco di dati crittografati hello archivio dei dati in un archivio permanente.

> [!NOTE] 
> Per motivi di prestazioni chiave DEK in hello deselezionare hello viene memorizzato nella cache in memoria per un breve periodo di tempo e immediatamente verrà cancellato in seguito. Nel supporto permanente, vengono sempre archiviato crittografati da hello MEK.

## <a name="key-rotation"></a>Rotazione delle chiavi

Quando si utilizzano chiavi gestita dal cliente, è possibile ruotare hello MEK. toolearn tooset di un account archivio Data Lake con chiavi gestita dal cliente, vedere [Introduzione](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).

### <a name="prerequisites"></a>Prerequisiti

Quando si configura hello account archivio Data Lake, si sono scelto toouse chiavi personalizzate. Questa opzione non può essere modificata dopo la creazione di account hello. Hello passaggi seguenti presuppongono che si siano utilizzando chiavi gestita dal cliente (ovvero, si sono scelto chiavi personalizzate dall'insieme di credenziali chiave).

Si noti che se si utilizzano le opzioni predefinite di hello per la crittografia, i dati sono sempre crittografati utilizzando le chiavi gestite dall'archivio Data Lake. In questo caso, non si dispongono delle chiavi toorotate possibilità hello, come vengono gestite da archivio Data Lake.

### <a name="how-toorotate-hello-mek-in-data-lake-store"></a>Come toorotate hello MEK in archivio Data Lake

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Selezionare l'istanza di insieme di credenziali chiave toohello che archivia le chiavi associate all'account archivio Data Lake. Selezionare **Chiavi**.

    ![Screenshot di Key Vault](./media/data-lake-store-encryption/keyvault.png)

3.  Selezionare hello chiave associate all'account archivio Data Lake e creare una nuova versione di questa chiave. Si noti che archivio Data Lake attualmente supporta solo la rotazione delle chiavi tooa nuova versione di una chiave. Non supporta la rotazione tooa altra chiave.

   ![Screenshot della finestra Chiavi con Nuova versione in evidenza](./media/data-lake-store-encryption/keynewversion.png)

4.  Selezionare l'account di archiviazione di archivio Data Lake toohello e scegliere **crittografia**.

    ![Screenshot della finestra dell'account di archiviazione di Data Lake Store con Crittografia in evidenza](./media/data-lake-store-encryption/select-encryption.png)

5.  Un messaggio informa che è disponibile una nuova versione di chiave della chiave di hello. Fare clic su **ruota chiave** nuova versione di tooupdate hello toohello chiave.

    ![Screenshot della finestra Data Lake Store con il messaggio e Ruota chiave in evidenza](./media/data-lake-store-encryption/rotatekey.png)

Questa operazione richiederà meno di due minuti, e nessun tempo di inattività previsto a causa di rotazione tookey. Una volta completata l'operazione di hello, nuova versione di hello della chiave di hello è in uso.
