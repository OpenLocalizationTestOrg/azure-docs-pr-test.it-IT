---
title: aaaSecure di accedere alle app di logica tooAzure | Documenti Microsoft
description: Aggiunta di sicurezza per la protezione di accesso tootriggers, input e output, i parametri di azione e servizi utilizzati con i flussi di lavoro in Azure App per la logica.
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a>Proteggere l'accesso alle App per la logica tooyour

Esistono toohelp disponibili molti strumenti di proteggere le app per la logica.

* Protezione accesso tootrigger un'app di logica (Trigger di richiesta HTTP)
* Protezione accesso toomanage, modificare o leggere un'app di logica
* Protezione accesso toocontents di input e output per un'esecuzione
* Protezione di parametri o input all'interno di azioni in un flusso di lavoro
* Protezione accesso tooservices che ricevono richieste da un flusso di lavoro

## <a name="secure-access-tootrigger"></a>Accesso sicuro tootrigger

Quando si lavora con un'app di logica che viene attivato su una richiesta HTTP ([richiesta](../connectors/connectors-native-reqres.md) o [Webhook](../connectors/connectors-native-webhook.md)), è possibile limitare l'accesso in modo che solo i client autorizzati possono essere attivati hello logica app. Tutte le richieste in un'app per la logica vengono crittografate e protette tramite SSL.

### <a name="shared-access-signature"></a>Firma di accesso condiviso

Ogni endpoint di richiesta per un'app logica include un [firma di accesso condiviso (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) come parte dell'URL hello. Ogni URL contiene parametri di query `sp`, `sv` e `sig`. Le autorizzazioni sono specificate dai `sp`, e i corrispondenti metodi tooHTTP consentiti, `sv` è toogenerate versione utilizzata hello, e `sig` è tootrigger accesso tooauthenticate utilizzato. firma Hello viene generato utilizzando l'algoritmo SHA256 hello con una chiave segreta in tutti i percorsi URL hello e proprietà. chiave segreta Hello viene mai esposta e pubblicata e vengono mantenute crittografate e archiviate come parte di app per la logica hello. App logica autorizza solo i trigger che include una firma valida creata con la chiave privata di hello.

#### <a name="regenerate-access-keys"></a>Per rigenerare le chiavi di accesso

È possibile rigenerare una chiave protetta nuovo a in qualsiasi momento tramite il portale di Azure o di API REST hello. Tutti gli URL correnti che sono stati generati in precedenza utilizzando la chiave precedente hello sono toofire invalidato e non è più autorizzato hello logica app.

1. Nel portale di Azure hello, aprire hello logica app da tooregenerate una chiave
1. Fare clic su hello **chiavi di accesso** voce di menu in **impostazioni**
1. Scegliere tooregenerate chiave hello e processo hello completo

URL recuperate dopo la rigenerazione sono firmati con una nuova chiave di accesso hello.

#### <a name="creating-callback-urls-with-an-expiration-date"></a>Creazione di URL di callback con una data di scadenza

Se si condivide hello URL con altre parti, è possibile generare gli URL con chiavi specifiche e le date di scadenza in base alle esigenze. È possibile quindi facilmente distribuire le chiavi o garantire accesso toofire un'app è limitato tooa determinati timespan. È possibile specificare una data di scadenza per un URL tramite hello [App API REST per la logica](https://docs.microsoft.com/rest/api/logic/workflowtriggers):

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

Nel corpo di hello, includere proprietà hello `NotAfter` come stringa di data JSON, che restituisce un URL di callback che è valido solo fino a quando hello `NotAfter` data e ora.

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a>Creazione di URL con una chiave privata primaria o secondaria

Quando si genera o elenco di URL callback per i trigger basata su richiesta, è possibile specificare anche l'URL hello toosign toouse chiave.  È possibile generare un URL firmato da una chiave specifica tramite hello [App API REST per la logica](https://docs.microsoft.com/rest/api/logic/workflowtriggers) come indicato di seguito:

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

Nel corpo di hello, includere proprietà hello `KeyType` come `Primary` o `Secondary`.  Restituisce un URL firmato dalla chiave di hello sicuro specificata.

### <a name="restrict-incoming-ip-addresses"></a>Limitare gli indirizzi IP in ingresso

Inoltre toohello firma di accesso condiviso, è preferibile toorestrict la chiamata di un'app logica solo da un client specifico.  Ad esempio, se si gestisce l'endpoint tramite Gestione API di Azure, è possibile limitare la logica di hello tooonly app accettare la richiesta di hello quando hello richiesta proviene da hello indirizzo IP dell'istanza gestione API.

Questa impostazione può essere configurata all'interno delle impostazioni di hello logica app:

1. Nel portale di Azure hello, aprire hello logica app da tooadd restrizioni degli indirizzi IP
1. Fare clic su hello **configurazione di controllo di accesso** voce di menu in **impostazioni**
1. Specificare elenco hello di toobe gli intervalli di indirizzi IP accettati dal trigger hello

Un intervallo IP valido ha il formato di hello `192.168.1.1/255`. Se si desidera hello logica app tooonly incendio come app nidificata logica, selezionare hello **solo ad altre App logica** opzione. Questa opzione consente di scrivere una risorsa toohello matrice vuota, ovvero solo le chiamate da hello servizio stesso (padre logica App) attivati correttamente.

> [!NOTE]
> È comunque possibile eseguire un'app logica con un trigger di richiesta tramite l'API REST hello / gestione `/triggers/{triggerName}/run` indipendentemente dall'IP. Questo scenario richiede l'autenticazione di base hello API REST di Azure e tutti gli eventi verrebbero visualizzati nella hello Log di controllo di Azure. Impostare i criteri di controllo di accesso di conseguenza.

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>L'impostazione di intervalli IP nella definizione di risorsa hello

Se si utilizza un [modello di distribuzione](logic-apps-create-deploy-template.md) tooautomate le distribuzioni, le impostazioni dell'intervallo IP hello possono essere configurate nel modello di risorsa hello.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a>Aggiunta di Azure Active Directory, OAuth o altri standard di sicurezza

autorizzazione più protocolli nella parte superiore di un'app di logica, tooadd [gestione API di Azure](https://azure.microsoft.com/services/api-management/) offre una app come un'API per la logica di monitoraggio, protezione, criteri e la documentazione per un endpoint con tooexpose funzionalità hello. Gestione API di Azure possono esporre un endpoint pubblico o privato per hello logica app, che può usare Azure Active Directory, certificato, OAuth o altri standard di sicurezza. Quando viene ricevuta una richiesta, gestione API di Azure inoltra hello richiesta toohello logica app (esecuzione di eventuali trasformazioni necessarie o restrizioni in transito). È possibile utilizzare l'intervallo IP in ingresso hello impostazioni hello logica app tooonly consentiranno hello logica app toobe attivato da Gestione API.

## <a name="secure-access-toomanage-or-edit-logic-apps"></a>Proteggere l'accesso alle App per la logica toomanage o di modifica

È possibile limitare l'accesso toomanagement operazioni su un'app logica in modo che solo utenti o gruppi specifici siano in grado di tooperform operazioni sulla risorsa hello. App per la logica di utilizzare hello Azure [controllo di accesso basato sui ruoli (RBAC)](../active-directory/role-based-access-control-configure.md) funzionalità e può essere personalizzata con hello stessi strumenti.  Esistono alcuni ruoli predefiniti, che è possibile assegnare anche i membri di tooas la sottoscrizione:

* **Logica App collaboratore** -fornisce accesso tooview, modificare e aggiornare un'app di logica.  Impossibile rimuovere la risorsa hello o eseguire operazioni di amministrazione.
* **Logica App operatore** : può visualizzare hello logica app e la cronologia di esecuzione e abilitare o disabilitare.  Non è possibile modificare o aggiornare la definizione di hello.

È inoltre possibile utilizzare [il blocco di risorsa di Azure](../azure-resource-manager/resource-group-lock-resources.md) tooprevent modifica o eliminazione di App per la logica. Questa funzionalità è utile tooprevent risorse di produzione da modifiche o eliminazioni.

## <a name="secure-access-toocontents-of-hello-run-history"></a>Accesso sicuro toocontents di hello cronologia di esecuzione

È possibile limitare l'accesso toocontents di input o output da precedenti esecuzioni toospecific intervalli di indirizzi IP.  

Tutti i dati all'interno di un'esecuzione del flusso di lavoro è crittografata in transito e a riposo. Quando viene effettuata una cronologia toorun chiamata, il servizio di hello autentica hello richiesta e fornisce collegamenti toohello richiesta e di input di risposta e di output. Questo collegamento può essere protette richieste pertanto sola tooview contenuto da un intervallo di indirizzi IP designato restituiscono contenuto hello. È possibile usare questa funzionalità per il controllo di accesso. È anche possibile specificare un indirizzo IP come `0.0.0.0` in modo che nessuno possa accedere a input e output. È necessario disporre delle autorizzazioni di amministratore è stato possibile rimuovere questa restrizione, fornendo il possibilità hello per contenuto tooworkflow 'just-in-time' accesso.

Questa impostazione può essere configurata all'interno delle impostazioni risorsa hello hello portale di Azure:

1. Nel portale di Azure hello, aprire hello logica app da tooadd restrizioni degli indirizzi IP
1. Fare clic su hello **configurazione di controllo di accesso** voce di menu in **impostazioni**
1. Specificare elenco hello di intervalli di indirizzi IP per l'accesso toocontent

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>L'impostazione di intervalli IP nella definizione di risorsa hello

Se si utilizza un [modello di distribuzione](logic-apps-create-deploy-template.md) tooautomate le distribuzioni, le impostazioni dell'intervallo IP hello possono essere configurate nel modello di risorsa hello.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a>Proteggere i parametri e gli input all'interno di un flusso di lavoro

È possibile tooparameterize alcuni aspetti di una definizione del flusso di lavoro per la distribuzione tra ambienti. Inoltre, alcuni parametri potrebbero essere parametri protetti non si desidera tooappear durante la modifica di un flusso di lavoro, ad esempio un ID client e segreto client per [l'autenticazione di Azure Active Directory](../connectors/connectors-native-http.md#authentication) di un'azione HTTP.

### <a name="using-parameters-and-secure-parameters"></a>Uso di parametri e parametri protetti

tooaccess hello valore di un parametro di risorsa in fase di esecuzione, hello [il linguaggio di definizione del flusso di lavoro](http://aka.ms/logicappsdocs) fornisce un `@parameters()` operazione. Inoltre, è possibile [specificare i parametri nel modello di distribuzione di risorse hello](../azure-resource-manager/resource-group-authoring-templates.md#parameters). Ma se si specifica il tipo di parametro hello come `securestring`, non viene restituito con il resto di hello hello della definizione di risorsa, il parametro hello e non saranno accessibile da Visualizzazione risorse hello dopo la distribuzione.

> [!NOTE]
> Se il parametro viene utilizzato in intestazioni hello o il corpo di una richiesta, il parametro hello potrebbe essere visibile mediante l'accesso alla cronologia di esecuzione hello e richiesta HTTP in uscita. Verificare che tooset i criteri di accesso al contenuto di conseguenza.
> Le intestazioni di autorizzazione non sono mai visibili tramite input o output. Se viene utilizzato il segreto hello sono, segreto hello non è recuperabile.

#### <a name="resource-deployment-template-with-secrets"></a>Modello di distribuzione risorse con segreti

Hello esempio seguente viene illustrata una distribuzione che fa riferimento a un parametro di secure `secret` in fase di esecuzione. In un file di parametri separati, è possibile specificare il valore di ambiente hello per hello `secret`, oppure utilizzare [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve segreti al momento della distribuzione.

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is hello request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a>Proteggere l'accesso alle richieste di ricezione tooservices da un flusso di lavoro

Esistono molti modi toohelp qualsiasi app per la logica hello endpoint deve tooaccess sicura.

### <a name="using-authentication-on-outbound-requests"></a>Uso dell'autenticazione nelle richieste in uscita

Quando si lavora con un HTTP, HTTP + Swagger (API aperta) o azione Webhook, è possibile aggiungere una richiesta di autenticazione toohello inviato. Potrebbe trattarsi di autenticazione di base, autenticazione del certificato o l'autenticazione di Azure Active Directory. Informazioni dettagliate su come tooconfigure questa autenticazione è reperibile [in questo articolo](../connectors/connectors-native-http.md#authentication).

### <a name="restricting-access-toologic-app-ip-addresses"></a>Limitazione degli indirizzi IP di accesso toologic app

Tutte le chiamate dalle app per la logica provengono da un set specifico di indirizzi IP in base all'area. È possibile aggiungere ulteriori filtri tooonly accetta richieste da quelli indicati gli indirizzi IP. Per un elenco di indirizzi IP, vedere [Limiti e configurazione delle app per la logica](logic-apps-limits-and-config.md#configuration).

### <a name="on-premises-connectivity"></a>Connettività locale

App per la logica forniscono l'integrazione con diversi servizi tooprovide, sicuro e affidabile la comunicazione in locale.

#### <a name="on-premises-data-gateway"></a>Gateway dati locale

Molti connettori gestiti per App per la logica forniscono una connettività sicura sistemi tooon locali, inclusi File System, SQL, SharePoint, DB2 e altro ancora. gateway Hello inoltra i dati da origini locali sui canali crittografati tramite hello Azure Service Bus. Tutto il traffico viene generato come proteggere il traffico in uscita dall'agente gateway hello. Altre informazioni, vedere [funzionamento gateway dati hello](logic-apps-gateway-install.md#gateway-cloud-service).

#### <a name="azure-api-management"></a>Gestione API di Azure

[Gestione API di Azure](https://azure.microsoft.com/services/api-management/) sono disponibili opzioni di connettività locale, inclusa l'integrazione di ExpressRoute e VPN da sito a sito per i sistemi locali tooon proxy e comunicazione protetti. Nella finestra di progettazione logica App hello, è possibile selezionare rapidamente un'API esposta da Gestione API di Azure all'interno di un flusso di lavoro forniscono un rapido accesso sistemi tooon locali.

#### <a name="hybrid-connections-from-azure-app-service"></a>Connessioni ibride dai servizi app di Azure

È possibile utilizzare funzionalità di una connessione ibrida locale hello per le API di Azure e Web App toocommunicate locale.  Informazioni dettagliate sulle connessioni ibride e come è possibile trovare tooconfigure [in questo articolo](../app-service-web/web-sites-hybrid-connection-get-started.md).

## <a name="next-steps"></a>Passaggi successivi
[Creare un modello di distribuzione](logic-apps-create-deploy-template.md)  
[Gestione delle eccezioni](logic-apps-exception-handling.md)  
[Monitorare le app per la logica](logic-apps-monitor-your-logic-apps.md)  
[Diagnosi degli errori delle app per la logica](logic-apps-diagnosing-failures.md)  
