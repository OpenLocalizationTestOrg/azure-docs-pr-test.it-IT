---
title: ripristino di emergenza aaaImplement tramite backup e ripristino in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come toouse di backup e ripristino di emergenza tooperform in Gestione API di Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 058bfb579e3a3f51fb1dac8ea37eb4fdbc83a4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a>Come tooimplement il ripristino di emergenza tramite servizio di backup e ripristino in Gestione API di Azure
Per la scelta toopublish e gestire le API tramite Gestione API di Azure consente di usufruire di molte errore tolleranza di errore e l'infrastruttura di funzionalità che altrimenti sarebbe toodesign, implementare e gestire. Hello piattaforma Azure riduce gran parte di potenziali errori a una frazione del costo di hello.

toorecover da problemi di disponibilità hello regione in cui il servizio Gestione API di hosting si deve essere pronta tooreconstitute il servizio in un'area diversa in qualsiasi momento. A seconda di obiettivi di disponibilità e obiettivo tempo di ripristino si tooreserve un servizio di backup in una o più aree e provare toomaintain loro configurazione e la sincronizzazione con servizi attivi hello contenuto. backup del servizio Hello e funzionalità di ripristino fornisce hello, i blocchi necessari per implementare la strategia di ripristino di emergenza.

Questa guida viene illustrato come le richieste tooauthenticate Gestione risorse di Azure e come toobackup e ripristinare le istanze del servizio Gestione API.

> [!NOTE]
> Hello processo di backup e ripristino di un'istanza del servizio Gestione API per il ripristino di emergenza può essere utilizzato anche per la replica delle istanze del servizio Gestione API per scenari come la gestione temporanea.
>
> Si noti che ogni backup scade dopo 30 giorni. Se si tenta di toorestore una copia di backup dopo il periodo di scadenza 30 giorni hello è scaduto, ripristino hello avrà esito negativo con un `Cannot restore: backup expired` messaggio.
>
>

## <a name="authenticating-azure-resource-manager-requests"></a>Autenticazione delle richieste di Gestione risorse di Azure
> [!IMPORTANT]
> Hello API REST per il backup e ripristino Usa Gestione risorse di Azure e presenta un meccanismo di autenticazione diverso rispetto ai hello API REST per gestire le entità di gestione API. Hello in questa sezione viene descritta la modalità Azure Resource Manager tooauthenticate richieste. Per altre informazioni, vedere [Autenticazione delle richieste di Gestione risorse di Azure](http://msdn.microsoft.com/library/azure/dn790557.aspx).
>
>

Tutte le attività hello che vengono eseguite sulle risorse usando hello Azure Resource Manager deve essere autenticate con Azure Active Directory tramite hello alla procedura seguente.

* Aggiungere un tenant di Azure Active Directory toohello dell'applicazione.
* Impostare le autorizzazioni per un'applicazione hello che è stato aggiunto.
* Ottenere il token di hello per autenticare le richieste tooAzure Gestione risorse.

primo passaggio Hello è toocreate un'applicazione Azure Active Directory. Accedere hello [portale di Azure classico](http://manage.windowsazure.com/) mediante sottoscrizione hello che contiene il servizio Gestione API dell'istanza e passare toohello **applicazioni** scheda per il valore predefinito di Azure Active Directory.

> [!NOTE]
> Se directory predefinita di hello Azure Active Directory non è visibile tooyour account, l'amministratore di hello contatto di hello toogrant di sottoscrizione di Azure hello richiesto tooyour autorizzazioni account.

![Creare un'applicazione Azure Active Directory][api-management-add-aad-application]

Fare clic su **Aggiungi**, **Aggiungi un'applicazione che l'organizzazione sta sviluppando**, quindi scegliere **Applicazione client nativa**. Immettere un nome descrittivo e fare clic sulla freccia avanti hello. Immettere un URL di segnaposto, ad esempio `http://resources` per hello **URI di reindirizzamento**, come è un campo obbligatorio, ma il valore di hello non viene usato in un secondo momento. Fare clic su un'applicazione hello toosave hello casella di controllo.

Dopo aver salvata un'applicazione hello, fare clic su **configura**, scorrere verso il basso toohello **autorizzazioni tooother applicazioni** sezione e fare clic su **aggiungere applicazione**.

![Aggiungere autorizzazioni][api-management-aad-permissions-add]

Selezionare **Windows** **API di gestione del servizio di Azure** e fare clic su un'applicazione hello tooadd hello casella di controllo.

![Aggiungere autorizzazioni][api-management-aad-permissions]

Fare clic su **autorizzazioni delegate** accanto a hello appena aggiunto **Windows** **API di gestione del servizio di Azure** applicazione hello casella per **accesso Azure Gestione dei servizi (anteprima)**, fare clic su **salvare**.

![Aggiungere autorizzazioni][api-management-aad-delegated-permissions]

Tooinvoking precedente hello API che generano hello backup e ripristino, è necessario tooget un token. esempio Hello utilizza hello [ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) token di hello tooretrieve pacchetto nuget.

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed tooobtain hello JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

Sostituire `{tentand id}`, `{application id}`, e `{redirect uri}` utilizzando hello attenendosi alle istruzioni.

Sostituire `{tenant id}` con l'id tenant hello di hello applicazione Azure Active Directory appena creata. È possibile accedere id hello facendo **visualizzare endpoint**.

![Endpoint][api-management-aad-default-directory]

![Endpoint][api-management-endpoint]

Sostituire `{application id}` e `{redirect uri}` utilizzando hello **Id Client** e hello URL da hello **Redirect Uris** sezione dall'applicazione Azure Active Directory **Configura**  scheda.

![Risorse][api-management-aad-resources]

Una volta specificati i valori hello, esempio di codice hello deve restituire un token toohello simile esempio seguente.

![token][api-management-arm-token]

Prima di chiamare il metodo hello backup e ripristinare le operazioni descritte nelle sezioni che seguono hello, impostare l'intestazione della richiesta hello autorizzazione per la chiamata REST.

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <a name="step1"> </a>Backup di un servizio di Gestione API
tooback backup un hello problema del servizio Gestione API richiesta HTTP seguente:

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

dove:

* `subscriptionId`-id della sottoscrizione hello contenente il servizio di gestione API hello che si sta tentando di toobackup
* `resourceGroupName`-stringa nel formato hello "Api - predefinito-{servizio region}" dove `service-region` identifica hello regione di Azure in cui è ospitato il servizio Gestione API che si sta tentando di toobackup hello, ad esempio,`North-Central-US`
* `serviceName`-nome hello del servizio Gestione API effettuare un backup di specificata in fase di creazione di hello hello
* `api-version` - sostituire con `2014-02-14`

Nel corpo della richiesta di hello hello specificare nome account di archiviazione di Azure di destinazione hello, chiave di accesso, nome del contenitore blob e nome backup:

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

Impostare il valore di hello di hello `Content-Type` intestazione della richiesta troppo`application/json`.

Copia di backup è un'operazione a esecuzione prolungata che potrebbero essere necessari più toocomplete minuti.  Se hello richiesta ha esito positivo e processo di backup hello è stata avviata, riceverai un `202 Accepted` codice di stato di risposta con un `Location` intestazione.  Verificare 'GET' richiede URL di toohello in hello `Location` toofind intestazione stato hello dell'operazione di hello. Mentre è in corso il backup di hello continuerà tooreceive un codice di stato "202 accettato". Un codice di risposta `200 OK` indicherà il completamento dell'operazione di backup hello.

Nota: hello seguenti vincoli quando si effettua una richiesta di backup.

* **Contenitore** specificato nel corpo della richiesta hello **deve esistere**.
* Mentre il backup è in corso, **non tentare di eseguire alcuna operazione di gestione dei servizi** , ad esempio l'aggiornamento o il downgrade di SKU, la modifica di nomi di dominio e così via.
* Ripristino di un **backup è garantito solo per 30 giorni** dall'istante hello della creazione.
* **Dati di utilizzo** utilizzata per creare report analitica **non è incluso** nel backup hello. Utilizzare [API REST gestione API di Azure] [ Azure API Management REST API] tooperiodically recuperare i report di analitica per motivi di sicurezza.
* frequenza di Hello con cui si esegue il backup del servizio avrà effetto sull'obiettivo del punto di ripristino. è consigliabile implementare backup regolari, nonché l'esecuzione di backup su richiesta dopo aver apportato importante toominimize modifica tooyour servizio di gestione API.
* **Le modifiche** toohello effettuata configurazione del servizio (ad esempio, API, criteri, aspetto del portale per sviluppatori) durante l'operazione di backup è in corso **potrebbero non essere inclusi nel backup hello e pertanto andranno persi**.

## <a name="step2"></a>Ripristino di un servizio di Gestione API
un servizio di gestione API da un backup creato in precedenza toorestore apportare hello seguente richiesta HTTP:

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

dove:

* `subscriptionId`-id della sottoscrizione hello contenente si ripristina un backup nel servizio di gestione API hello
* `resourceGroupName`-stringa nel formato hello "Api - predefinito-{servizio region}" dove `service-region` identifica hello regione di Azure in cui è ospitato hello si ripristina un backup nel servizio di gestione API, ad esempio,`North-Central-US`
* `serviceName`-nome hello di hello gestione API del servizio in fase di ripristino specificato in fase di hello della creazione
* `api-version` - sostituire con `2014-02-14`

Nel corpo della richiesta di hello hello specificare percorso file di backup hello, ad esempio nome account di archiviazione di Azure, chiave di accesso, nome del contenitore blob e nome backup:

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

Impostare il valore di hello di hello `Content-Type` intestazione della richiesta troppo`application/json`.

Il ripristino è un'operazione a esecuzione prolungata che potrebbe essere too30 o altre toocomplete minuti.  Se hello richiesta è stata completata ed è stato avviato il processo di ripristino hello si riceverà un `202 Accepted` codice di stato di risposta con un `Location` intestazione.  Verificare 'GET' richiede URL di toohello in hello `Location` toofind intestazione stato hello dell'operazione di hello. Durante l'esecuzione di restore hello continuerà tooreceive '202 accettato' codice di stato. Un codice di risposta `200 OK` indicherà il completamento dell'operazione di ripristino hello.

> [!IMPORTANT]
> **Hello SKU** del servizio hello in fase di ripristino **deve corrispondere** hello SKU di hello backup del servizio in corso il ripristino.
>
> **Le modifiche** toohello effettuata configurazione del servizio (ad esempio, API, criteri, aspetto del portale per sviluppatori) durante l'operazione di ripristino è in corso **potrebbero essere sovrascritti**.
>
>

## <a name="next-steps"></a>Passaggi successivi
Estrarre hello seguente blog di Microsoft per le due procedure dettagliate diverse del processo di backup/ripristino hello.

* [Replicare account di Gestione API di Azure](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * Grazie a tooGisela per articolo toothis contributo.
* [Gestione API di Azure: Backup e ripristino della configurazione](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * approccio Hello dettagliata Stuart non corrisponde a informazioni aggiuntive ufficiale hello ma è molto interessante.

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png
