---
title: aaaConfigure un nome di dominio personalizzato per l'endpoint di archiviazione Blob di Azure | Documenti Microsoft
description: Utilizzare il proprio endpoint di archiviazione Blob toohello nome canonico (CNAME) a hello toomap portale di Azure in un account di archiviazione di Azure.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: aaafd8c5-eacb-49dc-8c8b-3f7011ad5e92
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: marsma
ms.openlocfilehash: 6cca6a6e1dbb69e7078df7ed11b04e8b921ec2f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-for-your-blob-storage-endpoint"></a>Configurare un nome di dominio personalizzato per l'endpoint di archiviazione BLOB

È possibile configurare un nome di dominio personalizzato per l'accesso ai dati BLOB nell'account di archiviazione di Azure. Hello endpoint predefinito per l'archiviazione Blob è `<storage-account-name>.blob.core.windows.net`. Se si esegue il mapping di un dominio personalizzato e un sottodominio come **www.contoso.com** toohello endpoint di blob dell'account di archiviazione, gli utenti possono quindi accedere blob di dati nell'account di archiviazione con tale dominio.

> [!IMPORTANT]
> Archiviazione di Azure non supporta ancora in modo nativo HTTPS con domini personalizzati. È possibile attualmente [utilizzare BLOB tooaccess di hello rete CDN di Azure con i domini personalizzati tramite HTTPS](./storage-https-custom-domain-cdn.md).
>

Hello tabella seguente vengono illustrati alcuni URL di esempio per dati blob presenti in un account di archiviazione denominato **mystorageaccount**. dominio personalizzato Hello registrato per l'account di archiviazione hello è **www.contoso.com**:

| Tipo di risorsa | URL predefinito | URL di dominio personalizzato |
| --- | --- | --- |
| Account di archiviazione | http://mystorageaccount.blob.core.windows.net | http://www.contoso.com |
| BLOB |http://mystorageaccount.blob.core.windows.net/mycontainer/myblob | http://www.contoso.com/mycontainer/myblob |
| Contenitore radice | http://mystorageaccount.blob.core.windows.net/myblob or http://mystorageaccount.blob.core.windows.net/$root/myblob| http://www.contoso.com/myblob or http://www.contoso.com/$root/myblob |

## <a name="direct-vs-intermediary-domain-mapping"></a>Mapping di dominio diretto e con sottodominio intermedio

Esistono due modi toopoint l'endpoint blob toohello di dominio personalizzato per l'account di archiviazione: indirizzare CNAME mapping e l'utilizzo di hello *asverify* sottodominio intermedio.

### <a name="direct-cname-mapping"></a>Mapping diretto del record CNAME

Hello primo e più semplice, il metodo è un record di nome canonico (CNAME) che esegue il mapping del dominio personalizzato e il sottodominio direttamente toohello blob endpoint toocreate. Un record CNAME è una funzionalità di system (DNS) nome di dominio che esegue il mapping di un dominio di destinazione tooa di dominio di origine. In questo caso, il dominio di origine hello è proprio dominio personalizzato e un sottodominio, ad esempio *www.contoso.com*. dominio di destinazione di hello è l'endpoint del servizio Blob, ad esempio  *mystorageaccount.BLOB.Core.Windows.NET*.

metodo diretto Hello viene descritta in [registrare un dominio personalizzato](#register-a-custom-domain).

### <a name="intermediary-mapping-with-asverify"></a>Mapping intermedio con *asverify*

secondo metodo Hello Usa anche i record CNAME, ma prima utilizza un sottodominio speciale riconosciuto dai tempi di inattività Azure tooavoid: **asverify**.

il processo di Hello di mapping l'endpoint blob tooa di dominio personalizzato può comportare un breve periodo di inattività hello dominio mentre si registra in hello [portale di Azure](https://portal.azure.com). Se il dominio personalizzato supporta attualmente un'applicazione con un contratto di servizio (SLA) che richiede tempi di inattività, è quindi possibile utilizzare hello Azure *asverify* sottodominio come un passaggio di registrazione intermedio. Questo passaggio intermedio assicura gli utenti sono in grado di tooaccess dominio mentre viene eseguito il mapping DNS hello.

metodo intermediario Hello viene descritta in [registrare un dominio personalizzato utilizzando hello *asverify* sottodominio](#register-a-custom-domain-using-the-asverify-subdomain).

## <a name="register-a-custom-domain"></a>Registrare un dominio personalizzato
Utilizzare questo tooregister procedure il dominio personalizzato se si non teme sul dominio hello essere utenti tooyour temporaneamente non disponibile o se il dominio personalizzato non sta attualmente ospitando un'applicazione.

Se il dominio personalizzato supporta attualmente un'applicazione che non può avere alcun tempo di inattività, attenersi alla procedura hello [registrare un dominio personalizzato utilizzando hello *asverify* sottodominio](#register-a-custom-domain-using-the-asverify-subdomain).

tooconfigure un nome di dominio personalizzato, è necessario creare un nuovo record CNAME in DNS. record CNAME Hello specifica un alias per un nome di dominio. In questo caso, viene eseguito il mapping di indirizzi hello dell'endpoint di archiviazione Blob toohello dominio personalizzato per l'account di archiviazione.

In genere è possibile gestire le impostazioni DNS del dominio sul sito Web del registrar del dominio. Ogni autorità di registrazione è un metodo simile, ma leggermente diverso per specificare un record CNAME, ma il concetto di hello è hello stesso. Alcuni pacchetti di registrazione del dominio di base non offre la configurazione DNS, pertanto potrebbe essere necessario tooupgrade il pacchetto di registrazione del dominio prima di creare record CNAME hello.

1. Passare l'account di archiviazione tooyour in hello [portale di Azure](https://portal.azure.com).
1. In **servizio BLOB** nel Pannello di hello menu, selezionare **dominio personalizzato** tooopen hello *dominio personalizzato* blade.
1. Accedere al sito Web del registrar di dominio tooyour e toohello pagina per la gestione DNS passare. Queste informazioni possono essere disponibili in una sezione come **Domain Name**, **DNS** o **Name Server Management**.
1. Trovare la sezione hello per la gestione dei record CNAME. È possibile avere una pagina di impostazioni avanzate tooan toogo e cercare parole hello **CNAME**, **Alias**, o **sottodomini**.
1. Creare un nuovo record CNAME e specificare un alias di sottodominio, ad esempio **www** o **photos**. Quindi specificare un nome host, ovvero l'endpoint del servizio Blob, nel formato hello **mystorageaccount.blob.core.windows.net** (dove *mystorageaccount* hello nome dell'account di archiviazione). toouse di nome host Hello viene visualizzata nell'elemento #1 di hello *dominio personalizzato* pannello in hello [portale di Azure](https://portal.azure.com).
1. Nella casella di testo hello nella hello *dominio personalizzato* pannello in hello [portale di Azure](https://portal.azure.com), immettere il nome di hello del dominio personalizzato, inclusi il sottodominio hello. Ad esempio, se il dominio è **contoso.com** e l'alias di sottodominio è **www**, immettere **www.contoso.com**. Se il sottodominio è **foto**, immettere **photos.contoso.com**. hello sottodominio è *richiesto*.
1. Selezionare **salvare** su hello *dominio personalizzato* pannello tooregister il dominio personalizzato. Se la registrazione di hello ha esito positivo, si verrà visualizzata una notifica del portale che l'account di archiviazione è stato aggiornato.

Dopo il nuovo record CNAME è propagata tramite DNS, gli utenti è possono visualizzare dati blob utilizzando il dominio personalizzato, purché dispongano delle autorizzazioni appropriate di hello.

## <a name="register-a-custom-domain-using-hello-asverify-subdomain"></a>Registrare un dominio personalizzato utilizzando hello *asverify* sottodominio
Utilizzare questa stored procedure tooregister il dominio personalizzato se il dominio personalizzato supporta attualmente un'applicazione con un contratto di servizio che richiede che vi siano periodi di inattività. Creando un record CNAME che punti da `asverify.<subdomain>.<customdomain>` troppo`asverify.<storageaccount>.blob.core.windows.net`, è possibile pre-registrare il dominio con Azure. È quindi possibile creare un secondo record CNAME che punti da `<subdomain>.<customdomain>` troppo`<storageaccount>.blob.core.windows.net`, a quel punto dominio personalizzato di traffico tooyour sarà l'endpoint blob tooyour diretto.

Hello **asverify** sottodominio è un sottodominio speciale riconosciuto da Azure. Anteponendo `asverify` tooyour un sottodominio è consentire toorecognize Azure il dominio personalizzato senza modificare il record DNS hello per dominio hello. Quando si modificano i record DNS hello per dominio hello, verrà mappato toohello blob endpoint senza tempi di inattività.

1. Passare l'account di archiviazione tooyour in hello [portale di Azure](https://portal.azure.com).
1. In **servizio BLOB** nel Pannello di hello menu, selezionare **dominio personalizzato** tooopen hello *dominio personalizzato* blade.
1. Accedere al sito Web del provider DNS tooyour e toohello pagina per la gestione DNS passare. Queste informazioni possono essere disponibili in una sezione come **Domain Name**, **DNS** o **Name Server Management**.
1. Trovare la sezione hello per la gestione dei record CNAME. È possibile avere una pagina di impostazioni avanzate tooan toogo e cercare parole hello **CNAME**, **Alias**, o **sottodomini**.
1. Creare un nuovo record CNAME e fornire un alias di sottodominio che include hello *asverify* sottodominio. Ad esempio **asverify.www** o **asverify.photos**. Quindi specificare un nome host, ovvero l'endpoint del servizio Blob, nel formato hello **asverify.mystorageaccount.blob.core.windows.net** (dove **mystorageaccount** hello nome dell'account di archiviazione). toouse di nome host Hello viene visualizzata nell'elemento #2 di hello *dominio personalizzato* pannello in hello [portale di Azure](https://portal.azure.com).
1. Nella casella di testo hello nella hello *dominio personalizzato* pannello in hello [portale di Azure](https://portal.azure.com), immettere il nome di hello del dominio personalizzato, inclusi il sottodominio hello. Non includere *asverify*. Ad esempio, se il dominio è **contoso.com** e l'alias di sottodominio è **www**, immettere **www.contoso.com**. Se il sottodominio è **foto**, immettere **photos.contoso.com**. sottodominio hello è obbligatorio.
1. Seleziona hello **Usa convalida CNAME indiretta** casella di controllo.
1. Selezionare **salvare** su hello *dominio personalizzato* pannello tooregister il dominio personalizzato. Se la registrazione di hello ha esito positivo, si verrà visualizzata una notifica del portale che informa che l'account di archiviazione è stato aggiornato. A questo punto, il dominio personalizzato è stato verificato da Azure, ma dominio tooyour traffico non è ancora stato instradato tooyour account di archiviazione.
1. Sito Web del provider DNS tooyour restituire e creare un altro record CNAME che associa l'endpoint del servizio Blob tooyour sottodominio. Ad esempio, specificare il sottodominio hello come **www** o **foto** (senza hello *asverify*), e nome host come hello  **mystorageaccount.BLOB.Core.Windows.NET** (dove **mystorageaccount** hello nome dell'account di archiviazione). Con questo passaggio è stata completata la registrazione di hello del dominio personalizzato.
1. Infine, è possibile eliminare i record CNAME hello creato contiene hello **asverify** sottodominio, perché è stato necessario solo come passaggio intermedio.

Dopo il nuovo record CNAME è propagata tramite DNS, gli utenti è possono visualizzare dati blob utilizzando il dominio personalizzato, purché dispongano delle autorizzazioni appropriate di hello.

## <a name="test-your-custom-domain"></a>Testare un dominio personalizzato

il dominio personalizzato è tooconfirm mappato effettivamente tooyour endpoint del servizio Blob, creare un blob in un contenitore pubblico all'interno dell'account di archiviazione. Quindi, in un web browser, utilizzare un URI in hello blob hello tooaccess di formato seguente:

`http://<subdomain.customdomain>/<mycontainer>/<myblob>`

Ad esempio, è possibile utilizzare hello seguente URI tooaccess un web form in hello **myforms** contenitore hello **photos.contoso.com** sottodominio personalizzato:

`http://photos.contoso.com/myforms/applicationform.htm`

## <a name="deregister-a-custom-domain"></a>Annullare la registrazione di un dominio personalizzato

tooderegister un dominio personalizzato per l'endpoint di archiviazione Blob, utilizzare uno dei hello seguire le procedure seguenti.

### <a name="azure-portal"></a>Portale di Azure

Eseguire l'esempio hello nell'impostazione di dominio personalizzato hello tooremove portale Azure hello:

1. Passare l'account di archiviazione tooyour in hello [portale di Azure](https://portal.azure.com).
1. In **servizio BLOB** nel Pannello di hello menu, selezionare **dominio personalizzato** tooopen hello *dominio personalizzato* blade.
1. Contenuto crittografato hello hello della casella di testo contenente il nome di dominio personalizzato.
1. Seleziona hello **salvare** pulsante.

Quando il dominio personalizzato hello è stato rimosso correttamente, verrà visualizzata una notifica portale che informa che l'account di archiviazione è stato aggiornato.

### <a name="azure-cli-20"></a>Interfaccia della riga di comando di Azure 2.0

Hello utilizzare [aggiornamento dell'account di archiviazione az](https://docs.microsoft.com/cli/azure/storage/account#update) CLI di comandi e specificare una stringa vuota (`""`) per hello `--custom-domain` tooremove valore argomento una registrazione di un dominio personalizzato.

* Formato del comando:

  ```azurecli
  az storage account update \
      --name <storage-account-name> \
      --resource-group <resource-group-name> \
      --custom-domain ""
  ```

* Esempio del comando:

  ```azurecli
  az storage account update \
      --name mystorageaccount \
      --resource-group myresourcegroup \
      --custom-domain ""
  ```

### <a name="powershell"></a>PowerShell

Hello utilizzare [Set AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) cmdlet di PowerShell e specificare una stringa vuota (`""`) per hello `-CustomDomainName` tooremove valore argomento una registrazione di un dominio personalizzato.

* Formato del comando:

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "<resource-group-name>" `
      -AccountName "<storage-account-name>" `
      -CustomDomainName ""
  ```

* Esempio del comando:

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "myresourcegroup" `
      -AccountName "mystorageaccount" `
      -CustomDomainName ""
  ```

## <a name="next-steps"></a>Passaggi successivi
* [Eseguire il mapping di un endpoint di Azure rete CDN (Content Delivery) tooan dominio personalizzato](../cdn/cdn-map-content-to-custom-domain.md)
* [Tramite i BLOB in tooaccess hello rete CDN di Azure con i domini personalizzati tramite HTTPS](./storage-https-custom-domain-cdn.md)
