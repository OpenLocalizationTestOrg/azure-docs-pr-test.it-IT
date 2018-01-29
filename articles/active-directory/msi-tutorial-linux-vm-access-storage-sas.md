---
title: "Usare un'identità del servizio gestito di una macchina virtuale Linux per accedere ad Archiviazione di Azure tramite credenziali della firma di accesso condiviso"
description: "Esercitazione che illustra come usare un'identità del servizio gestito di una macchina virtuale Linux per accedere ad Archiviazione di Azure tramite credenziali di firma di accesso condiviso anziché tramite una chiave di accesso dell'account di archiviazione."
services: active-directory
documentationcenter: 
author: bryanla
manager: mtillman
editor: bryanla
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/20/2017
ms.author: bryanla
ms.openlocfilehash: a4dda36ce1ae01c4fe66394a86dd9624b3c41d9f
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2017
---
# <a name="use-a-linux-vm-managed-service-identity-to-access-azure-storage-via-a-sas-credential"></a>Usare un'identità del servizio gestito di una macchina virtuale Linux per accedere ad Archiviazione di Azure tramite credenziali di firma di accesso condiviso

[!INCLUDE[preview-notice](../../includes/active-directory-msi-preview-notice.md)]

Questa esercitazione illustra come abilitare un'identità del servizio gestito per una macchina virtuale Linux e quindi usare l'identità per ottenere credenziali di firma di accesso condiviso (SAS, Shared Access Signature) di archiviazione. In particolare, [credenziali di firma di accesso condiviso del servizio](/azure/storage/common/storage-dotnet-shared-access-signature-part-1?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#types-of-shared-access-signatures). 

La firma di accesso condiviso del servizio offre la possibilità di concedere accesso limitato agli oggetti in un account di archiviazione per un periodo di tempo limitato e per un servizio specifico (in questo caso, il servizio BLOB) senza esporre la chiave di accesso di un account. È possibile usare credenziali di firma di accesso condiviso come di consueto durante le operazioni di archiviazione, ad esempio quando si usa Storage SDK. In questa esercitazione viene illustrato come caricare e scaricare un oggetto BLOB tramite l'interfaccia della riga di comando di Archiviazione di Azure. Si apprenderà come:


> [!div class="checklist"]
> * Abilitare Identità del servizio gestito in una macchina virtuale Linux 
> * Concedere alla macchina virtuale l'accesso alla firma di accesso condiviso dell'account di archiviazione in Resource Manager 
> * Ottenere un token di accesso tramite l'identità della macchina virtuale e usarlo per recuperare la firma di accesso condiviso da Resource Manager 

## <a name="prerequisites"></a>Prerequisiti

[!INCLUDE [msi-qs-configure-prereqs](../../includes/active-directory-msi-qs-configure-prereqs.md)]

[!INCLUDE [msi-tut-prereqs](../../includes/active-directory-msi-tut-prereqs.md)]

## <a name="sign-in-to-azure"></a>Accedere ad Azure
Accedere al portale di Azure all'indirizzo [https://portal.azure.com](https://portal.azure.com).


## <a name="create-a-linux-virtual-machine-in-a-new-resource-group"></a>Creare una macchina virtuale Linux in un nuovo gruppo di risorse

Per questa esercitazione si creerà una nuova macchina virtuale Linux, ma è anche possibile abilitare l'identità del servizio gestito in una macchina virtuale esistente.

1. Fare clic sul pulsante **+/Crea nuovo servizio** nell'angolo superiore sinistro del portale di Azure.
2. Selezionare **Calcolo** e quindi **Ubuntu Server 16.04 LTS**.
3. Immettere le informazioni relative alla macchina virtuale. In **Tipo di autenticazione** selezionare **Chiave pubblica SSH** o **Password**. Le credenziali create consentono di eseguire l'accesso alla macchina virtuale.

    ![Testo immagine alt](media/msi-tutorial-linux-vm-access-arm/msi-linux-vm.png)

4. Dall'elenco a discesa **Sottoscrizione** selezionare una sottoscrizione per la macchina virtuale.
5. Per selezionare un nuovo **Gruppo di risorse** in cui creare la macchina virtuale, scegliere **Crea nuovo**. Al termine fare clic su **OK**.
6. Selezionare la dimensione della macchina virtuale. Per visualizzare altre dimensioni, selezionare **View all** (Visualizza tutto) o modificare il filtro Tipo di disco supportato. Nel pannello delle impostazioni mantenere le impostazioni predefinite e fare clic su **OK**.

## <a name="enable-msi-on-your-vm"></a>Abilitare identità del servizio gestito nella macchina virtuale

Un'identità del servizio gestito per una macchina virtuale consente di ottenere i token di accesso da Azure AD senza dover inserire le credenziali nel codice. A livello sottostante, quando si abilita Identità del servizio gestito, si eseguono due operazioni, ovvero si installa l'estensione di Identità del servizio gestito nella macchina virtuale e si abilita la funzionalità per tale macchina.  

1. Passare al gruppo di risorse della nuova macchina virtuale e selezionare la macchina virtuale creata nel passaggio precedente.
2. Nella sezione "Impostazioni" della macchina virtuale a sinistra fare clic su **Configurazione**.
3. Per registrare e abilitare identità del servizio gestita, scegliere **Sì**. Se si vuole disabilitare questa funzionalità, scegliere No.
4. Assicurarsi di fare clic su **Salva** per salvare la configurazione.

    ![Testo immagine alt](media/msi-tutorial-linux-vm-access-arm/msi-linux-extension.png)

5. Per verificare le estensioni installate nella macchina virtuale, fare clic su **Estensioni**. Se Identità del servizio gestito è abilitata, nell'elenco è inclusa la voce **ManagedIdentityExtensionforLinux**.

    ![Testo immagine alt](media/msi-tutorial-linux-vm-access-arm/msi-extension-value.png)

## <a name="create-a-storage-account"></a>Creare un account di archiviazione 

Se non ne è già disponibile uno, creare un account di archiviazione.  È anche possibile ignorare questo passaggio e concedere alla macchina virtuale l'accesso Identità del servizio gestito alle chiavi di un account di archiviazione esistente. 

1. Fare clic sul pulsante **+/Crea nuovo servizio** nell'angolo superiore sinistro del portale di Azure.
2. Fare clic su **Archiviazione**, quindi **Account di archiviazione**. Viene visualizzato un nuovo pannello "Crea account di archiviazione".
3. Immettere un **nome** per l'account di archiviazione, che verrà usato in un secondo momento.  
4. **Modello di distribuzione** e **Tipologia account** devono essere impostati su "Gestione di risorse" e "Utilizzo generico". 
5. Verificare che le impostazioni in **Sottoscrizione** e **Gruppo di risorse** corrispondano a quelle specificate al momento della creazione della macchina virtuale nel passaggio precedente.
6. Fare clic su **Crea**.

    ![Creare un nuovo account di archiviazione](media/msi-tutorial-linux-vm-access-storage/msi-storage-create.png)

## <a name="create-a-blob-container-in-the-storage-account"></a>Creare un contenitore BLOB nell'account di archiviazione

Successivamente verrà caricato e scaricato un file per il nuovo account di archiviazione. Poiché i file richiedono l'archiviazione BLOB, è necessario creare un contenitore BLOB in cui archiviare il file.

1. Tornare all'account di archiviazione appena creato.
2. Fare clic sul collegamento **Contenitori** nel pannello a sinistra, in "Servizio BLOB".
3. Fare clic su **+ Contenitore** nella parte superiore della pagina e verrà visualizzato il pannello "Nuovo contenitore".
4. Assegnare un nome al contenitore, selezionare un livello di accesso, quindi fare clic su **OK**. Il nome specificato verrà usato più avanti nell'esercitazione. 

    ![Creare un contenitore di archiviazione](media/msi-tutorial-linux-vm-access-storage/create-blob-container.png)

## <a name="grant-your-vms-msi-access-to-use-a-storage-sas"></a>Concedere l'identità del servizio gestito della macchina virtuale per usare una firma di accesso condiviso di archiviazione 

Archiviazione di Azure non supporta l'autenticazione di Azure AD in modo nativo.  È tuttavia possibile usare un'identità del servizio gestito per recuperare una firma di accesso condiviso di archiviazione da Resource Manager e quindi usarla per accedere all'archivio.  In questo passaggio, alla macchina virtuale viene concesso l'accesso tramite identità del servizio gestito alla firma di accesso condiviso di archiviazione.   

1. Tornare all'account di archiviazione appena creato.   
2. Fare clic sul collegamento **Controllo di accesso (IAM)** nel pannello di sinistra.  
3. Fare clic su **+ Aggiungi** nella parte superiore della pagina per aggiungere una nuova assegnazione di ruolo alla macchina virtuale.
4. Impostare **Ruolo** su "Collaboratore Account di archiviazione" sul lato destro della pagina. 
5. Nell'elenco a discesa successivo impostare **Assegna accesso a** sulla risorsa "Macchina virtuale".  
6. Assicurarsi quindi che la sottoscrizione appropriata sia presente nell'elenco a discesa **Sottoscrizione** e quindi impostare **Gruppo di risorse** su "Tutti i gruppi di risorse".  
7. In **Seleziona** scegliere infine la macchina virtuale Linux nell'elenco a discesa e quindi fare clic su **Salva**.  

    ![Testo immagine alt](media/msi-tutorial-linux-vm-access-storage/msi-storage-role-sas.png)

## <a name="get-an-access-token-using-the-vms-identity-and-use-it-to-call-azure-resource-manager"></a>Ottenere un token di accesso usando l'identità della macchina virtuale e usarlo per chiamare Azure Resource Manager

Il resto dell'esercitazione prevede che le operazioni vengano svolte dalla macchina virtuale creata in precedenza.

Per completare questi passaggi, è necessario disporre di un client SSH. Se si usa Windows, è possibile usare il client SSH nel [sottosistema Windows per Linux](https://msdn.microsoft.com/commandline/wsl/install_guide). Per richiedere assistenza nella configurazione delle chiavi del client SSH, vedere [Come usare le chiavi SSH con Windows in Azure](../virtual-machines/linux/ssh-from-windows.md) o [Come creare e usare una coppia di chiavi SSH pubblica e privata per le macchine virtuali Linux in Azure](../virtual-machines/linux/mac-create-ssh-keys.md).

1. Nel portale di Azure passare a **Macchine virtuali**, selezionare la macchina virtuale Linux e quindi nella parte superiore della pagina **Panoramica** fare clic su **Connetti**. Copiare la stringa di connessione alla macchina virtuale. 
2. Connettersi alla macchina virtuale tramite il client SSH.  
3. Successivamente, verrà richiesto di immettere la **Password** aggiunta durante la creazione della **macchina virtuale Linux**. A questo punto l'accesso è stato eseguito correttamente.  
4. Usare CURL per ottenere il token di accesso per Azure Resource Manager.  

    Di seguito sono illustrate la richiesta e la risposta CURL per il token di accesso:
    
    ```bash
    curl http://localhost:50342/oauth2/token --data "resource=https://management.azure.com/" -H Metadata:true    
    ```
    
    > [!NOTE]
    > Nella richiesta precedente il valore del parametro "risorsa" deve corrispondere esattamente a quello previsto da Azure AD. Quando si usa l'ID risorsa di Azure Resource Manager, è necessario includere la barra finale nell'URI.
    > Nella risposta seguente l'elemento access_token è stato abbreviato per comodità.
    
    ```bash
    {"access_token":"eyJ0eXAiOiJ...",
    "refresh_token":"",
    "expires_in":"3599",
    "expires_on":"1504130527",
    "not_before":"1504126627",
    "resource":"https://management.azure.com",
    "token_type":"Bearer"} 
     ```

## <a name="get-a-sas-credential-from-azure-resource-manager-to-make-storage-calls"></a>Ottenere credenziali di firma di accesso condiviso da Azure Resource Manager per eseguire chiamate al servizio di archiviazione

Di seguito viene usato CURL per eseguire una chiamata a Resource Manager tramite il token di accesso recuperato nella sezione precedente e creare credenziali di firma di accesso condiviso di archiviazione. Dopo aver creato le credenziali di firma di accesso condiviso, è possibile chiamare operazioni di upload/download di archiviazione.

Per creare le credenziali di firma di accesso condiviso in questa richiesta verranno usati i parametri della richiesta HTTP seguente:

```JSON
{
    "canonicalizedResource":"/blob/<STORAGE ACCOUNT NAME>/<CONTAINER NAME>",
    "signedResource":"c",              // The kind of resource accessible with the SAS, in this case a container (c).
    "signedPermission":"rcw",          // Permissions for this SAS, in this case (r)ead, (c)reate, and (w)rite.  Order is important.
    "signedProtocol":"https",          // Require the SAS be used on https protocol.
    "signedExpiry":"<EXPIRATION TIME>" // UTC expiration time for SAS in ISO 8601 format, for example 2017-09-22T00:06:00Z.
}
```

Questi parametri sono inclusi nel corpo del comando POST della richiesta di credenziali di firma di accesso condiviso. Per altre informazioni sui parametri per la creazione di credenziali di firma di accesso condiviso, vedere le [informazioni di riferimento REST per la firma di accesso condiviso del servizio List](/rest/api/storagerp/storageaccounts/listservicesas).

Per ottenere le credenziali di firma di accesso condiviso, usare la richiesta CURL seguente. Sostituire i valori dei parametri `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, `<STORAGE ACCOUNT NAME>`, `<CONTAINER NAME>` e `<EXPIRATION TIME>` con valori personalizzati. Sostituire il valore di `<ACCESS TOKEN>` con il token di accesso recuperato in precedenza:

```bash 
curl https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Storage/storageAccounts/<STORAGE ACCOUNT NAME>/listServiceSas/?api-version=2017-06-01 -X POST -d "{\"canonicalizedResource\":\"/blob/<STORAGE ACCOUNT NAME>/<CONTAINER NAME>\",\"signedResource\":\"c\",\"signedPermission\":\"rcw\",\"signedProtocol\":\"https\",\"signedExpiry\":\"<EXPIRATION TIME>\"}" -H "Authorization: Bearer <ACCESS TOKEN>"
```

> [!NOTE]
> Il testo nell'URL precedente fa distinzione tra maiuscole e minuscole. Assicurarsi quindi di usare la stessa combinazione di maiuscole e minuscole usata per i gruppi di risorse. È anche importante tenere conto che questa è una richiesta POST, non una richiesta GET.

La risposta CURL restituisce le credenziali di firma di accesso condiviso:  

```bash 
{"serviceSasToken":"sv=2015-04-05&sr=c&spr=https&st=2017-09-22T00%3A10%3A00Z&se=2017-09-22T02%3A00%3A00Z&sp=rcw&sig=QcVwljccgWcNMbe9roAJbD8J5oEkYoq%2F0cUPlgriBn0%3D"} 
```

Creare un file di BLOB esempio da caricare nel contenitore di archiviazione BLOB. A tale scopo, in una macchina virtuale Linux eseguire il comando seguente. 

```bash
echo "This is a test file." > test.txt
```

Eseguire quindi l'autenticazione con il comando `az storage` dell'interfaccia della riga di comando usando le credenziali di firma di accesso condiviso e caricare il file nel contenitore BLOB. Per questo passaggio è necessario [installare la versione più recente dell'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/install-azure-cli) nella macchina virtuale, se non è già stato fatto.

```azurecli-interactive
 az storage blob upload --container-name 
                        --file 
                        --name
                        --account-name 
                        --sas-token
```

Risposta: 

```JSON
Finished[#############################################################]  100.0000%
{
  "etag": "\"0x8D4F9929765C139\"",
  "lastModified": "2017-09-21T03:58:56+00:00"
}
```

È anche possibile scaricare il file usando l'interfaccia della riga di comando di Azure ed eseguendo l'autenticazione con le credenziali di firma di accesso condiviso. 

Richiesta: 

```azurecli-interactive
az storage blob download --container-name
                         --file 
                         --name 
                         --account-name
                         --sas-token
```

Risposta: 

```JSON
{
  "content": null,
  "metadata": {},
  "name": "testblob",
  "properties": {
    "appendBlobCommittedBlockCount": null,
    "blobType": "BlockBlob",
    "contentLength": 16,
    "contentRange": "bytes 0-15/16",
    "contentSettings": {
      "cacheControl": null,
      "contentDisposition": null,
      "contentEncoding": null,
      "contentLanguage": null,
      "contentMd5": "Aryr///Rb+D8JQ8IytleDA==",
      "contentType": "text/plain"
    },
    "copy": {
      "completionTime": null,
      "id": null,
      "progress": null,
      "source": null,
      "status": null,
      "statusDescription": null
    },
    "etag": "\"0x8D4F9929765C139\"",
    "lastModified": "2017-09-21T03:58:56+00:00",
    "lease": {
      "duration": null,
      "state": "available",
      "status": "unlocked"
    },
    "pageBlobSequenceNumber": null,
    "serverEncrypted": false
  },
  "snapshot": null
}
```

## <a name="next-steps"></a>Passaggi successivi

- Per una panoramica dell'identità di servizio gestito, vedere [Panoramica dell'identità di servizio gestito](../active-directory/msi-overview.md).
- Per informazioni su come eseguire questa stessa procedura usando una chiave dell'account di archiviazione, vedere [Usare un'identità del servizio gestito per una macchina virtuale Linux per accedere ad Archiviazione di Azure](msi-tutorial-linux-vm-access-storage.md)
- Per altre informazioni sulla funzionalità della firma di accesso condiviso dell'account di Archiviazione di Azure, vedere:
  - [Uso delle firme di accesso condiviso](/azure/storage/common/storage-dotnet-shared-access-signature-part-1.md)
  - [Creazione di una firma di accesso condiviso del servizio](/rest/api/storageservices/Constructing-a-Service-SAS.md)

Usare la sezione dei commenti seguente per fornire commenti e suggerimenti utili per migliorare e organizzare i contenuti disponibili.
