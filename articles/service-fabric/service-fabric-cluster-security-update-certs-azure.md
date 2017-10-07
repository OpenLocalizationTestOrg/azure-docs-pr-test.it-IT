---
title: i certificati aaaManage in un cluster di Azure Service Fabric | Documenti Microsoft
description: Viene descritto come tooadd nuovi certificati, il certificato di rollover e Rimuovi certificato tooor da un cluster di Service Fabric.
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a>Aggiungere o rimuovere certificati per un cluster Service Fabric in Azure
Si consiglia di acquisire familiarità con l'utilizzo di certificati x. 509 Service Fabric e acquisire familiarità con hello [degli scenari di sicurezza Cluster](service-fabric-cluster-security.md). È necessario comprendere cos'è un certificato del cluster e a cosa serve prima di procedere.

Consente di infrastruttura servizio che specificare che due cluster i certificati, uno primario e secondario, quando si configura certificato di sicurezza durante la creazione del cluster nei certificati tooclient aggiunta. Fare riferimento troppo[creazione di un cluster di azure mediante portale](service-fabric-cluster-creation-via-portal.md) o [creazione di un cluster di azure con Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) per informazioni dettagliate sulla configurazione al momento della creazione. Se si specifica un solo certificato cluster al momento della creazione, che viene quindi utilizzato come certificato primario hello. Dopo la creazione del cluster è possibile aggiungere un nuovo certificato come secondario.

> [!NOTE]
> Per un cluster protetto, è sempre necessario certificato almeno un cluster valido (non revocati e non scaduti) (primario o secondario) distribuito (in caso contrario hello cluster si arresterà). 90 giorni prima della scadenza, di raggiungere tutti i certificati validi sistema hello genera una traccia di avviso e anche un evento di avviso di integrità nel nodo hello. Attualmente non sono disponibili messaggi di posta elettronica o altre notifiche inviati da Service Fabric su questo argomento. 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a>Aggiungere un certificato secondario del cluster tramite il portale di hello

Impossibile aggiungere il certificato secondario del cluster tramite hello portale di Azure. Hai toouse Azure powershell per tale. processo Hello descritta più avanti in questo documento.

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a>Scambiare certificati cluster hello tramite il portale di hello

Dopo avere distribuito correttamente un certificato secondario del cluster, se si desidera tooswap hello primario e secondario, quindi passare pannello sicurezza toohello e selezionare hello 'Swap primario' opzione hello contesto menu tooswap hello secondario cert con certificato primario Hello.

![Scambiare i certificati][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a>Rimuovere un certificato di cluster tramite il portale di hello

Per un cluster sicura, occorre sempre almeno un valido (non revocato e non scaduto) certificato (primario o secondario) distribuito in caso contrario, hello cluster si arresterà.

un certificato secondario venga utilizzato per la protezione del cluster, pannello di navigazione toohello sicurezza e selezionare hello 'Delete' opzione dal menu di scelta rapida hello sul certificato secondario hello tooremove.

Se si intende certificato hello tooremove che è contrassegnato come primario, sarà necessario tooswap con hello secondario prima e quindi eliminare hello secondario dopo il completamento dell'aggiornamento hello.

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a>Aggiungere un certificato secondario tramite PowerShell per Resource Manager

Questi passaggi presuppongono che si ha familiarità con il funzionamento di gestione risorse e avere distribuito almeno un cluster Service Fabric utilizzando un modello di gestione delle risorse e modello hello utilizzato tooset di cluster hello utili. Si presuppone anche che si abbia dimestichezza con l'uso di JSON.

> [!NOTE]
> Se si sta cercando un modello di esempio e i parametri che è possibile utilizzare toofollow lungo o come un punto di partenza, quindi scaricarlo da questo [repository git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample). 
> 
> 

### <a name="edit-your-resource-manager-template"></a>Modificare il modello di Azure Resource Manager

Per facilitare la seguente lungo, esempio 5-VM-1-NodeTypes-Secure_Step2.JSON contiene tutte le modifiche di hello che verrà rilasciato. esempio Hello è disponibile in [repository git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).

**Verificare che toofollow tutti i passaggi di hello**

**Passaggio 1:** apre un modello di gestione risorse di hello utilizzato toodeploy del Cluster. Se è stato scaricato l'esempio hello da hello sopra repository, quindi utilizzare 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy un cluster protetto e quindi aprire il modello.

**Passaggio 2:** Aggiungi **due nuovi parametri** "secCertificateThumbprint" e "secCertificateUrlValue" di tipo "stringa" toohello sezione relativa ai parametri del modello. È possibile copiare hello seguente frammento di codice e aggiungerlo toohello modello. A seconda del modello di origine hello si potrebbe già dispone di tali, in tal caso, spostare toohello successivo. 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

**Passaggio 3:** apportare modifiche toohello **Microsoft.ServiceFabric/clusters** risorse - individuare una definizione di risorsa "Microsoft.ServiceFabric/clusters" hello nel modello. In proprietà di tale definizione, si noterà "Certificato" JSON tag, che dovrebbe essere simile hello frammento di codice JSON seguente:

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

Aggiungere un nuovo tag "thumbprintSecondary" e assegnare un valore "[parameters('secCertificateThumbprint')]".  

In tal caso, dopo la definizione di risorsa hello dovrebbe essere simile hello seguente (a seconda dell'origine del modello di hello, potrebbe non essere esattamente come hello frammento di codice riportato di seguito). 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

Se si desidera troppo**cert hello rollover**, quindi specificare nuovo certificato hello come database primario corrente hello primario e in movimento come database secondario. Di conseguenza il rollover di hello del corrente certificato primario toohello nuovo certificato in un unico passaggio di distribuzione.

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


**Passaggio 4:** apportare modifiche troppo**tutti** hello **Microsoft.Compute/virtualMachineScaleSets** le definizioni delle risorse - individuare hello Microsoft.Compute/virtualMachineScaleSets risorsa definizione. Scorrere toohello "publisher": "Microsoft.Azure.ServiceFabric" in "virtualMachineProfile".

Nelle impostazioni del server di pubblicazione dell'infrastruttura servizio hello, dovrebbe essere simile al seguente.

![Json_Pub_Setting1][Json_Pub_Setting1]

Aggiungere hello nuovo cert voci tooit

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

proprietà Hello dovrebbe essere simile al seguente

![Json_Pub_Setting2][Json_Pub_Setting2]

Se si desidera troppo**cert hello rollover**, quindi specificare nuovo certificato hello come database primario corrente hello primario e in movimento come database secondario. Di conseguenza il rollover di hello del corrente certificato toohello nuovo certificato in un unico passaggio di distribuzione. 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
proprietà Hello dovrebbe essere simile al seguente

![Json_Pub_Setting3][Json_Pub_Setting3]


**Passaggio 5:** apportare modifiche troppo**tutti** hello **Microsoft.Compute/virtualMachineScaleSets** le definizioni delle risorse - individuare hello Microsoft.Compute/virtualMachineScaleSets risorsa definizione. Scorrere toohello "vaultCertificates":, in "OSProfile". Dovrebbe avere un aspetto simile al seguente:


![Json_Pub_Setting4][Json_Pub_Setting4]

Aggiungere tooit secCertificateUrlValue hello. Utilizzare hello frammento di codice seguente:

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
Ora hello Json risultante dovrebbe essere simile al seguente.
![Json_Pub_Setting5][Json_Pub_Setting5]


> [!NOTE]
> Assicurarsi che nel modello sono ripetuti i passaggi 4 e 5 per tutte le definizioni di risorse Nodetypes/Microsoft.Compute/virtualMachineScaleSets hello. Se non è disponibile uno di essi, non verrà installato il certificato di hello in tale VMSS e sarà necessario ottenere risultati imprevisti del cluster, inclusi i cluster hello procedendo verso il basso (se si finisce con nessun certificato valido di che tale cluster hello è possibile utilizzare per la sicurezza. È quindi importante verificare, prima di procedere.
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a>Modificare i file tooreflect hello nuovi parametri di modello che è stato aggiunto in precedenza
Se si utilizza l'esempio hello hello [repository git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow insieme, è possibile avviare le modifiche toomake hello esempio 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON 

Modifica il parametro di modello di gestione risorse File, aggiungere hello due nuovi parametri per secCertificateThumbprint e secCertificateUrlValue. 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a>Distribuire hello modello tooAzure

- Si sono ora pronti toodeploy tooAzure il modello. Aprire il prompt dei comandi di Azure PowerShell versione 1+.
- Accedi tooyour Account Azure e selezionare la sottoscrizione di azure specifico di hello. Questo è un passaggio importante per gli amministratori che dispongono di accesso toomore rispetto a una sottoscrizione di azure.

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

Test hello modello precedente toodeploying è. Utilizzare hello stesso gruppo di risorse del cluster attualmente distribuito.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

Distribuire un gruppo di risorse tooyour modello hello. Utilizzare hello stesso gruppo di risorse del cluster attualmente distribuito. Eseguire il comando di New-AzureRmResourceGroupDeployment hello. Non è necessaria la modalità di hello toospecify, poiché il valore predefinito di hello è **incrementale**.

> [!NOTE]
> Se si imposta la modalità tooComplete, è possibile eliminare inavvertitamente le risorse che non sono presenti nel modello. Non usarla in questo scenario.
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

Ecco un riempimento all'esempio di hello powershell stessa.

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

Una volta completata la distribuzione di hello, connettersi utilizzando cluster tooyour hello nuovo certificato ed eseguire alcune query. Se si è in grado di toodo. È quindi possibile eliminare il vecchio certificato di hello. 

Se si utilizza un certificato autofirmato, non dimenticare tooimport loro nell'archivio certificati locale TrustedPeople.

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
Di seguito è cluster sicuro tooa tooconnect comando hello di riferimento rapido 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
Di seguito è l'integrità del cluster hello comando tooget di riferimento rapido

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a>Distribuzione di cluster toohello certificati di applicazione.

È possibile utilizzare hello stessi passaggi come descritto in 5 passaggi sopra toohave hello certificati distribuiti da un toohello keyvault nodi. È sufficiente definire e usare parametri diversi.


## <a name="adding-or-removing-client-certificates"></a>Aggiunta o rimozione di certificati client

I certificati di addizione toohello cluster, è possibile aggiungere operazioni di gestione tooperform i certificati client in un cluster di service fabric.

È possibile aggiungere due tipi di certificati client, Amministratore o Sola lettura, Quindi possono essere utilizzati toocontrol accesso toohello admin operazioni e le operazioni di Query nel cluster hello. Per impostazione predefinita, i certificati di hello cluster vengono aggiunti toohello Admin certificati elenco consentito.

È possibile specificare un numero qualsiasi di certificati client. Ogni aggiunta o l'eliminazione di risultati in un cluster di configurazione aggiornamento toohello service fabric


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a>Aggiunta di certificati client Amministratore o Sola lettura tramite il portale

1. Passare a pannello sicurezza toohello e selezionare hello '+ autenticazione' pulsante sopra pannello sicurezza hello.
2. Nel Pannello di "Aggiungere Authentication" hello, scegliere 'Tipo di autenticazione' - 'Client di sola lettura' o ' Admin' hello
3. Scegliere il metodo di autorizzazione hello. Se è necessario cercare questo certificato utilizzando il nome di soggetto hello o un'identificazione personale hello indica tooService dell'infrastruttura. In generale, non è un metodo di autorizzazione buona pratica toouse hello del nome soggetto. 

![Aggiungere il certificato client][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a>Eliminazione di certificati Client - Admin o sola lettura tramite hello portale

un certificato secondario venga utilizzato per la protezione del cluster, pannello di navigazione toohello sicurezza e selezionare hello 'Delete' opzione dal menu di scelta rapida hello certificato specifico hello tooremove.



## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sulla gestione del cluster, leggere questi articoli:

* [Processo di aggiornamento del cluster di infrastruttura di servizi e operazioni eseguibile dall'utente](service-fabric-cluster-upgrade.md)
* [Configurare l’accesso in base al ruolo per i client](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


