---
title: "identità aaaCreate per app di Azure con Azure CLI | Documenti Microsoft"
description: "Viene descritto come controllare toouse CLI di Azure toocreate un'applicazione Azure Active Directory e dell'entità servizio e concedere tooresources accedere tramite l'accesso basato sui ruoli. Viene illustrato come applicazione tooauthenticate con un certificato o la password."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 0d693ec801d4f4d6c24ec420580776e73014b325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a>Utilizzare toocreate CLI di Azure un risorse tooaccess dell'entità servizio

Quando si dispone di un'app o script che richiede risorse tooaccess, è possibile impostare un'identità per l'applicazione hello e l'applicazione hello con le proprie credenziali di autenticazione. Questa identità è nota come entità servizio. Questo approccio consente di:

* Assegnare le autorizzazioni di identità app toohello che sono diverse dalle proprie autorizzazioni. In genere, queste autorizzazioni sono limitate tooexactly quali app hello deve toodo.
* Usare un certificato per l'autenticazione in caso di esecuzione di uno script automatico.

In questo articolo illustra come toouse [CLI di Azure 1.0](../cli-install-nodejs.md) tooset backup toorun un'applicazione con le proprie credenziali e identità. Installare una versione più recente di hello di [CLI di Azure 1.0](../cli-install-nodejs.md) toomake che l'ambiente corrisponda esempi hello in questo articolo.

## <a name="required-permissions"></a>Autorizzazioni necessarie
toocomplete in questo argomento, è necessario disporre delle autorizzazioni sufficienti in Azure Active Directory sia la sottoscrizione di Azure. In particolare, devono essere in grado di toocreate un'app in Azure Active Directory hello e assegnazione di ruolo tooa principale di servizio hello. 

Hello più semplice modo toocheck se l'account disponga delle autorizzazioni appropriate è tramite il portale di hello. Vedere l'articolo su come [controllare le autorizzazioni necessarie nel portale](resource-group-create-service-principal-portal.md#required-permissions).

A questo punto, procedere sezione tooa per uno [password](#create-service-principal-with-password) o [certificato](#create-service-principal-with-certificate) l'autenticazione.

## <a name="create-service-principal-with-password"></a>Creare un'entità servizio con password
In questa sezione, eseguire hello passaggi toocreate hello applicazione Active Directory con una password e assegnare l'entità di servizio toohello ruolo Lettore hello.

1. Eseguire l'accesso tooyour account.
   
   ```azurecli
   azure login
   ```
2. toocreate un'identità di applicazione, specificare nome hello dell'applicazione hello e una password, come illustrato nel comando seguente hello:
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   viene restituita l'entità servizio nuovo Hello. Id oggetto Hello è necessaria quando si concedono autorizzazioni. guid Hello elencato con hello nomi dell'entità servizio è necessaria durante l'accesso. Questo guid è hello stesso valore di id app hello. Nelle applicazioni di esempio hello, questo valore è hello tooas cui `Client ID`. 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. Concedere le autorizzazioni dell'entità hello servizio nella sottoscrizione. In questo esempio, aggiungere hello servizio principale toohello ruolo lettura, che concede l'autorizzazione tooread tutte le risorse nella sottoscrizione hello. Per gli altri ruoli, vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md). Per il parametro objectid hello, fornire l'Id di oggetto da usare durante la creazione di un'applicazione hello hello. Prima di eseguire questo comando, è necessario consentire un certo tempo hello toopropagate principale nuovo servizio di Azure Active Directory. Quando si eseguono questi comandi manualmente, in genere trascorre tempo sufficiente tra le attività. In uno script, è necessario aggiungere un passaggio toosleep tra i comandi di hello (ad esempio `sleep 15`). Se viene visualizzato che un messaggio hello a errore principale non esiste nella directory di hello, eseguire di nuovo il comando hello.
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
L'operazione è terminata. L'applicazione AD e l''entità servizio sono così configurate. Nella sezione successiva Hello viene illustrato come toolog con hello credenziali tramite l'interfaccia CLI di Azure. Se si desiderano credenziali hello toouse codice nell'applicazione in uso, non è necessario toocontinue con questo argomento. È possibile passare toohello [applicazioni di esempio](#sample-applications) per esempi di accesso con l'id dell'applicazione e la password. 

### <a name="provide-credentials-through-azure-cli"></a>Fornire le credenziali tramite l'interfaccia della riga di comando di Azure
A questo punto, è necessario toolog in come operazioni tooperform dell'applicazione hello.

1. Ogni volta che si accede come un'entità servizio, è necessario id tenant di hello tooprovide della directory hello per le app di Active Directory. Un tenant è un'istanza di Azure Active Directory. id tenant di hello tooretrieve per la sottoscrizione attualmente autenticata, utilizzare:
   
   ```azurecli
   azure account show
   ```
   
   Che restituisce:
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     Se è necessario l'id tenant di hello tooget di un'altra sottoscrizione, utilizzare hello comando seguente:
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. Se è necessario tooretrieve hello client id toouse per l'accesso, utilizzare:
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     Hello valore toouse per l'accesso è il guid di hello elencato in nomi dell'entità servizio hello.
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. Accedi come servizio hello principale.
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    Viene chiesto di immettere la password di hello. Specificare la password di hello specificata durante la creazione di un'applicazione hello Active Directory.
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

Ora vengono autenticate come entità servizio hello per entità di servizio hello creato.

In alternativa, è possibile richiamare le operazioni REST da toolog riga di comando hello in. Dalla risposta di autenticazione hello, è possibile recuperare il token di accesso hello per l'utilizzo con altre operazioni. Per un esempio di recupero dei token di accesso hello richiamando operazioni REST, vedere [la generazione di un Token di accesso](resource-manager-rest-api.md#generating-an-access-token).

## <a name="create-service-principal-with-certificate"></a>Creare un'entità servizio con certificato
In questa sezione, eseguire passaggi di hello per:

* Creare un certificato autofirmato
* creare applicazione AD hello con certificato hello e l'entità servizio hello
* assegnare l'entità di servizio toohello ruolo Lettore hello

toocomplete questi passaggi, è necessario disporre di [OpenSSL](http://www.openssl.org/) installato.

1. Creare un certificato autofirmato.
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. Hello precedente passaggio creato due file - privkey.pem e cert.pem. Combinare le chiavi pubbliche e private hello in un singolo file.

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. Aprire hello **examplecert.pem** file e cercare di sequenza di caratteri tra lunga hello **---BEGIN CERTIFICATE---** e **---END CERTIFICATE---**. Copiare i dati del certificato hello. Passare questi dati come parametro durante la creazione di un'entità servizio hello.

4. Eseguire l'accesso tooyour account.

   ```azurecli
   azure login
   ```
5. entità di servizio toocreate hello, specificare il nome di hello hello app e dei dati del certificato hello, come illustrato nel comando seguente hello:
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   viene restituita l'entità servizio nuovo Hello. Id oggetto Hello è necessaria quando si concedono autorizzazioni. guid Hello elencato con hello nomi dell'entità servizio è necessaria durante l'accesso. Questo guid è hello stesso valore di id app hello. Nelle applicazioni di esempio hello, questo valore è hello tooas cui ID Client. 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. Concedere le autorizzazioni dell'entità hello servizio nella sottoscrizione. In questo esempio, aggiungere hello servizio principale toohello ruolo lettura, che concede l'autorizzazione tooread tutte le risorse nella sottoscrizione hello. Per gli altri ruoli, vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md). Per il parametro objectid hello, fornire l'Id di oggetto da usare durante la creazione di un'applicazione hello hello. Prima di eseguire questo comando, è necessario consentire un certo tempo hello toopropagate principale nuovo servizio di Azure Active Directory. Quando si eseguono questi comandi manualmente, in genere trascorre tempo sufficiente tra le attività. In uno script, è necessario aggiungere un passaggio toosleep tra i comandi di hello (ad esempio `sleep 15`). Se viene visualizzato che un messaggio hello a errore principale non esiste nella directory di hello, eseguire di nuovo il comando hello.
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a>Fornire il certificato tramite uno script dell'interfaccia della riga di comando di Azure automatizzato
A questo punto, è necessario toolog in come operazioni tooperform dell'applicazione hello.

1. Ogni volta che si accede come un'entità servizio, è necessario id tenant di hello tooprovide della directory hello per le app di Active Directory. Un tenant è un'istanza di Azure Active Directory. id tenant di hello tooretrieve per la sottoscrizione attualmente autenticata, utilizzare:
   
   ```azurecli
   azure account show
   ```
   
   Che restituisce:
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   Se è necessario l'id tenant di hello tooget di un'altra sottoscrizione, utilizzare hello comando seguente:
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. tooretrieve hello identificazione personale del certificato e rimuovere i caratteri non necessari, usare:
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   Viene restituito un valore di identificazione personale simile a:
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. Se è necessario tooretrieve hello client id toouse per l'accesso, utilizzare:
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   Hello valore toouse per l'accesso è il guid di hello elencato in nomi dell'entità servizio hello.
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. Accedi come servizio hello principale.
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

Ora vengono autenticate come entità servizio hello per hello applicazione Azure Active Directory creato.

## <a name="change-credentials"></a>Modificare le credenziali

utilizzano le credenziali di hello toochange per un'app di Active Directory, a causa una compromissione della sicurezza o la scadenza di una credenziale, `azure ad app set`.

toochange una password, utilizzare:

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

toochange un valore del certificato, utilizzare:

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a>Debug

È possibile riscontrare hello gli errori seguenti durante la creazione di un'entità servizio:

* **"Authentication_Unauthorized"** o **"alcuna sottoscrizione non trovato nel contesto di hello".** -Viene visualizzato questo errore quando l'account non dispone di hello [delle autorizzazioni necessarie](#required-permissions) su hello Azure Active Directory tooregister un'app. In genere, l'errore si verifica quando solo gli utenti amministratori di Azure Active Directory possono registrare le app e l'account in uso non è un account di amministratore. Chiedere tooeither l'amministratore assegna si tooan ruolo di amministratore o tooenable utenti tooregister app.

* L'account **"ha azione tooperform autorizzazione 'Microsoft.Authorization/roleAssignments/write' su"sottoscrizioni / {guid}"ambito".**  -Questo errore viene visualizzato quando l'account non dispone di sufficienti autorizzazioni tooassign un'identità tooan ruolo. Chiedere il tooadd amministratore sottoscrizione si tooUser accesso ruolo di amministratore.

## <a name="sample-applications"></a>Applicazioni di esempio
Per informazioni su come un'applicazione hello tramite diverse piattaforme, vedere:

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>Passaggi successivi
* Per informazioni dettagliate sull'integrazione di un'applicazione in Azure per la gestione delle risorse, vedere [tooauthorization di Guida per gli sviluppatori con API di gestione risorse di Azure hello](resource-manager-api-authentication.md).
* tooget ulteriori informazioni sull'utilizzo di certificati e CLI di Azure, vedere [l'autenticazione basata su certificati con le entità servizio di Azure dalla riga di comando Linux](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx). 
* Per un elenco di azioni disponibili che possono essere concesse o negate toousers, vedere [operazioni di Provider di risorse di Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).
