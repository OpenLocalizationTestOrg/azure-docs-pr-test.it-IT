---
title: aaaCreate un Azure Service Fabric del cluster da un modello | Documenti Microsoft
description: In questo articolo viene descritto come tooset di un'infrastruttura protetta di servizio cluster in Azure tramite Gestione risorse di Azure, insieme di credenziali chiave di Azure e Azure Active Directory (Azure AD) per l'autenticazione client.
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a>Creare un cluster di Service Fabric usando Azure Resource Manager
> [!div class="op_single_selector"]
> * [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
> * [Portale di Azure](service-fabric-cluster-creation-via-portal.md)
>
>

Questo articolo contiene una guida dettagliata che illustra la configurazione di un cluster di Azure Service Fabric sicuro in Azure tramite Azure Resource Manager. È consapevole di che tale articolo hello è lungo. Tuttavia, a meno che non si conoscono già accuratamente il contenuto di hello, essere toofollow verificare ogni passaggio con attenzione.

Hello vengono trattate hello seguire le procedure seguenti:

* Configurazione dei certificati di tooupload insieme di credenziali chiave Azure per la sicurezza del cluster e dell'applicazione
* Creazione di un cluster sicuro in Azure con Azure Resource Manager
* Autenticazione degli utenti con Azure Active Directory (Azure AD) per la gestione dei cluster

Un cluster sicura è un cluster che impedisce le operazioni toomanagement accesso non autorizzato. Ciò include la distribuzione, l'aggiornamento e l'eliminazione di applicazioni, servizi e dati hello in che essi contenuti. Un cluster non sicuro da un cluster che chiunque può connettersi tooat qualsiasi momento ed eseguire operazioni di gestione. Sebbene sia possibile toocreate un cluster non sicuro, si consiglia di creare un cluster protetto sin hello. Poiché un cluster non sicuro non può essere protetto in un secondo momento, è necessario crearne uno nuovo.

il concetto di Hello di creazione di cluster sicuri è hello stesso, che si tratti di cluster Linux o Windows. Per altre informazioni e script helper per la creazione di cluster Linux sicuri, vedere [Creare cluster protetti in Linux](#secure-linux-clusters).

## <a name="sign-in-tooyour-azure-account"></a>Accedi tooyour account Azure
Questa guida usa [Azure PowerShell][azure-powershell]. Quando si avvia una nuova sessione PowerShell, accedi tooyour account Azure e selezionare la sottoscrizione prima di eseguire i comandi di Azure.

Accedi tooyour account di Azure:

```powershell
Login-AzureRmAccount
```

Selezionare la propria sottoscrizione:

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a>Configurare un insieme di credenziali delle chiavi
Questa sezione illustra la creazione di un insieme di credenziali delle chiavi per un cluster di Service Fabric in Azure e per le applicazioni di Service Fabric. Per una guida completa tooAzure insieme di credenziali chiave, vedere toohello [Guida introduttiva di insieme di credenziali chiave][key-vault-get-started].

Service Fabric utilizza toosecure certificati x. 509 un cluster e fornisce le funzionalità di sicurezza dell'applicazione. Utilizzare i certificati toomanage insieme di credenziali chiave per i cluster di Service Fabric in Azure. Quando viene distribuito un cluster in Azure, i provider di risorse di Azure hello che è responsabili della creazione di cluster di Service Fabric estrae i certificati dall'insieme di credenziali chiave e li installa nel cluster hello macchine virtuali.

Hello diagramma seguente viene illustrata hello relazione tra l'insieme di credenziali chiave di Azure, un cluster di Service Fabric e provider di risorse di Azure hello che utilizza i certificati archiviati in un insieme di credenziali chiave durante la creazione di un cluster:

![Diagramma dell'installazione del certificato][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>Creare un gruppo di risorse
primo passaggio Hello è toocreate un gruppo di risorse in modo specifico per l'insieme di credenziali chiave. Si consiglia di inserire l'insieme di credenziali chiave hello nel proprio gruppo di risorse. Questa azione consente di rimuovere hello calcolo e archiviazione gruppi di risorse, tra cui gruppo di risorse hello che contiene il cluster di Service Fabric, senza perdere le chiavi e segreti. gruppo di risorse Hello che contiene l'insieme di credenziali chiave _deve essere in hello stessa regione_ come cluster hello che lo usa.

Se si prevede di cluster toodeploy in più aree, si consiglia di assegnare un nome gruppo di risorse hello e hello chiave dell'insieme di credenziali in modo che indica quale regione a cui appartiene.  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
output di Hello dovrebbe essere simile al seguente:

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a>Creare un insieme di credenziali chiave nel nuovo gruppo di risorse hello
insieme di credenziali chiave Hello _deve essere abilitato per la distribuzione_ tooallow hello calcolo certificati tooget provider di risorse da esso e installarla su istanze di macchine virtuali:

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

output di Hello dovrebbe essere simile al seguente:

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a>Usare un insieme di credenziali delle chiavi esistente

toouse un insieme di credenziali esistente, si _deve essere abilitata per la distribuzione_ tooallow hello calcolo certificati tooget provider di risorse da esso e installarlo nei nodi del cluster:

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a>Aggiungere certificati tooyour insieme di credenziali

I certificati vengono usati in Service Fabric tooprovide autenticazione e crittografia toosecure vari aspetti di un cluster e le relative applicazioni. Per altre informazioni sull'uso dei certificati in Service Fabric, vedere [Scenari di sicurezza di un cluster di Service Fabric][service-fabric-cluster-security].

### <a name="cluster-and-server-certificate-required"></a>Cluster e certificato del server (obbligatorio)
Questo certificato è obbligatorio toosecure un cluster e impedire l'accesso non autorizzato tooit. Il certificato fornisce protezione del cluster in due modi:

* Autenticazione del cluster: autentica la comunicazione da nodo a nodo per la federazione di cluster. Solo i nodi che è possano provare la propria identità con il certificato è possono aggiungere il cluster hello.
* L'autenticazione del server: hello cluster Gestione endpoint tooa gestione client viene autenticato in modo che hello client management sa stia comunicando toohello reale cluster. Questo certificato fornisce inoltre SSL per l'API di gestione HTTPS hello e per Service Fabric Explorer tramite HTTPS.

tooserve questi scopi, certificato hello deve soddisfare i seguenti requisiti hello:

* certificato di Hello deve contenere una chiave privata.
* Hello certificato deve essere creato per lo scambio di chiave, ovvero esportabile tooa file di scambio di informazioni personali (PFX).
* nome del soggetto del certificato Hello deve corrispondere dominio hello utilizzare cluster di Service Fabric tooaccess hello. Questo tipo di associazione è obbligatorio tooprovide SSL per l'endpoint di gestione del cluster hello HTTPS e Service Fabric Explorer. È possibile ottenere un certificato SSL da un'autorità di certificazione (CA) per hello. cloudapp.azure.com dominio. È necessario ottenere un nome di dominio personalizzato per il cluster. Quando si richiede un certificato da un'autorità di certificazione, hello Nome soggetto del certificato deve corrispondere nome di dominio personalizzato hello utilizzati per il cluster.

### <a name="application-certificates-optional"></a>Certificati delle applicazioni (facoltativo)
Per motivi di sicurezza dell'applicazione, è possibile installare nel cluster numerosi certificati aggiuntivi. Prima di creare il cluster, considerare gli scenari di sicurezza dell'applicazione hello che richiedono un toobe certificato installato nei nodi di hello, ad esempio:

* Crittografia e decrittografia dei valori di configurazione dell'applicazione.
* Crittografia dei dati tra i nodi durante la replica.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Formattazione dei certificati per l'uso di provider di risorse di Azure
È possibile aggiungere e usare file di chiave privata (PFX) direttamente tramite l'insieme di credenziali delle chiavi. Tuttavia, i provider di risorse di calcolo di Azure hello richiede toobe chiavi archiviate in un particolare formato JavaScript Object Notation (JSON). formato di Hello include file con estensione pfx hello come una stringa base 64 codificata in formato e la password della chiave privata hello. tooaccommodate questi requisiti, hello chiavi devono essere inserite in una stringa JSON e quindi archiviate come "segreti" nella chiave hello insieme di credenziali.

Questo processo più semplice, toomake un [modulo PowerShell è disponibile in GitHub][service-fabric-rp-helpers]. modulo hello toouse, hello seguenti:

1. Scaricare l'intero contenuto di hello del repository hello in una directory locale.
2. Passare toohello directory locale.
2. Importare il modulo ServiceFabricRPHelpers hello nella finestra di PowerShell:

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

Hello `Invoke-AddCertToKeyVault` comando in questo modulo di PowerShell Formatta automaticamente una chiave privata del certificato in una stringa JSON e ne carica toohello insieme di credenziali chiave. Utilizzare il certificato del cluster hello di hello comando tooadd e qualsiasi applicazione aggiuntiva certificati toohello chiave dell'insieme di credenziali. Ripetere questo passaggio per tutti i certificati aggiuntivi desiderate tooinstall del cluster.

#### <a name="uploading-an-existing-certificate"></a>Caricamento di un certificato esistente

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

Se si verifica un errore, ad esempio hello uno riportati di seguito, significa in genere la presenza di un conflitto di risorse URL. conflitto di hello tooresolve, nome dell'insieme di credenziali chiave hello di modifica.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Dopo la risoluzione dei conflitti di hello, l'output di hello dovrebbe essere simile al seguente:

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
>È necessario hello tre precedente stringhe, CertificateThumbprint SourceVault e CertificateURL, tooset di un cluster di Service Fabric sicuro e tooobtain tutti i certificati dell'applicazione che è possibile utilizzare per la sicurezza dell'applicazione. Se non si salva le stringhe di hello, può essere difficile tooretrieve li eseguendo una ricerca chiave hello insieme di credenziali in un secondo momento.

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a>Creazione di un certificato autofirmato e caricarlo insieme di credenziali chiave toohello

Se è già stato caricato nell'insieme di credenziali chiave di certificati toohello, ignorare questo passaggio. Questo passaggio è per la generazione di un nuovo certificato autofirmato e caricarlo insieme di credenziali chiave tooyour. Dopo avere modificato i parametri di hello in hello lo script seguente e quindi eseguirlo, verrà richiesto di immettere una password del certificato.  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

Se si verifica un errore, ad esempio hello uno riportati di seguito, significa in genere la presenza di un conflitto di risorse URL. conflitto hello tooresolve, insieme di credenziali chiave di hello Modifica nome, nome RG e così via.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Dopo la risoluzione dei conflitti di hello, l'output di hello dovrebbe essere simile al seguente:

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
>È necessario hello tre precedente stringhe, CertificateThumbprint SourceVault e CertificateURL, tooset di un cluster di Service Fabric sicuro e tooobtain tutti i certificati dell'applicazione che è possibile utilizzare per la sicurezza dell'applicazione. Se non si salva le stringhe di hello, può essere difficile tooretrieve li eseguendo una ricerca chiave hello insieme di credenziali in un secondo momento.

 A questo punto, è necessario disporre di hello degli elementi sul posto di seguito:

* gruppo di risorse dell'insieme di credenziali chiave Hello.
* Hello insieme di credenziali chiave e il relativo URL (denominato SourceVault nelle hello precede l'output di PowerShell).
* certificato di autenticazione server cluster Hello e il relativo URL nell'insieme di credenziali chiave hello.
* i certificati dell'applicazione Hello e gli URL nell'insieme di credenziali chiave hello.


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a>Configurare Azure Active Directory per l'autenticazione client

Azure AD consente alle organizzazioni (noto come tenant) toomanage utente accesso tooapplications. Alcune applicazioni sono caratterizzate da un'interfaccia utente di accesso basata sul Web, altre invece da un'esperienza client nativa. In questo articolo si presuppone che sia già stato creato un tenant. In caso contrario, iniziare leggendo [come tenant di Azure Active Directory tooget][active-directory-howto-tenant].

Un cluster di Service Fabric offre tooits punti di ingresso diverse funzionalità di gestione, tra cui hello basata sul web [Service Fabric Explorer] [ service-fabric-visualizing-your-cluster] e [Visual Studio] [service-fabric-manage-application-in-visual-studio]. Di conseguenza, creare due cluster di toohello accesso Azure AD applicazioni toocontrol, un'applicazione web e un'applicazione nativa.

toosimplify alcuni dei passaggi di hello coinvolti nella configurazione di Azure AD con un cluster di Service Fabric, è stato creato un set di script di Windows PowerShell.

> [!NOTE]
> È necessario completare i seguenti passaggi prima di creare cluster hello hello. Poiché gli script hello prevedono che gli endpoint e i nomi dei cluster, i valori di hello devono essere pianificati e non i valori che è già stato creato.

1. [Scaricare gli script hello] [ sf-aad-ps-script-download] tooyour computer.
2. Pulsante destro del mouse hello file zip, selezionare **proprietà**selezionare hello **Unblock** casella di controllo e quindi fare clic su **applica**.
3. Estrarre il file zip hello.
4. Eseguire `SetupApplications.ps1`e fornire hello TenantId, ClusterName e WebApplicationReplyUrl come parametri. ad esempio:

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    È possibile trovare l'ID tenant eseguendo il comando di PowerShell hello `Get-AzureSubscription`. L'esecuzione di questo comando Visualizza hello TenantId per ogni sottoscrizione.

    ClusterName è applicazioni hello Azure AD usato tooprefix creati dallo script hello. Non è necessario toomatch hello nome effettivo del cluster esattamente. È previsto toomake solo è più facile toomap Azure AD artefatti toohello cluster di Service Fabric è utilizzato con.

    WebApplicationReplyUrl è l'endpoint predefinito hello restituiti da Azure AD utenti tooyour dopo aver effettuato l'accesso. Impostare questo endpoint come endpoint di Service Fabric Explorer hello per il cluster, che per impostazione predefinita è:

    https://&lt;cluster_domain&gt;:19080/Explorer

    Si è toosign richiesta nell'account tooan che dispone di privilegi amministrativi per il tenant hello Azure AD. Dopo l'accesso, hello script crea web hello e applicazioni native toorepresent il cluster di Service Fabric. Se si osservano le applicazioni del tenant hello hello su [portale di Azure classico][azure-classic-portal], verranno visualizzate due voci di nuovo:

   * *ClusterName*\_Cluster
   * *ClusterName*\_Client

   script Hello stampa hello JSON richiesto dal modello di Azure Resource Manager hello quando si crea il cluster hello nella sezione successiva hello, pertanto è una finestra di PowerShell buona tookeep hello aprire.

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a>Creare un modello di Cluster Resource Manager di Service Fabric
In questa sezione, hello output di hello precedente vengono utilizzati i comandi di PowerShell in un modello di gestione risorse di cluster di Service Fabric.

Modelli di gestione risorse di esempio sono disponibili in hello [raccolta di modelli di avvio rapido di Azure su GitHub][azure-quickstart-templates]. Questi modelli possono essere usati come punto di partenza per il modello del cluster.

### <a name="create-hello-resource-manager-template"></a>Creare il modello di gestione risorse di hello
Questa Guida Usa hello [5 nodi cluster sicuro] [ service-fabric-secure-cluster-5-node-1-nodetype] modello di esempio e i parametri di modello. Scaricare `azuredeploy.json` e `azuredeploy.parameters.json` tooyour computer e aprire entrambi i file in un editor di testo.

### <a name="add-certificates"></a>Aggiungere certificati
Aggiungere modello di gestione risorse di cluster tooa certificati facendo riferimento hello chiave dell'insieme di credenziali contenente le chiavi di hello certificato. Si consiglia di posizionare i valori di insieme di credenziali chiave hello in un file di parametri di modello di gestione risorse. In questo modo consente di mantenere hello Gestione risorse file modello riutilizzabile e privo di distribuzione tooa specifico di valori.

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a>Aggiungere che set di scalabilità di macchine virtuali di tutti i certificati toohello osProfile
Ogni certificato installato nel cluster hello deve essere configurato nella sezione osProfile hello della risorsa di set di scalabilità hello (Microsoft.Compute/virtualMachineScaleSets). Questa azione indica certificato hello risorsa provider tooinstall hello in hello macchine virtuali. Questa installazione include sia il certificato di cluster hello e i certificati di sicurezza dell'applicazione che si prevede di toouse per le applicazioni:

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-hello-service-fabric-cluster-certificate"></a>Configurare il certificato del cluster di Service Fabric hello
certificato di autenticazione Hello cluster deve essere configurato in entrambe le risorse di cluster Service Fabric hello (Microsoft.ServiceFabric/clusters) e imposta hello estensione Service Fabric per la scalabilità della macchina virtuale nella risorsa set di scalabilità della macchina virtuale hello. In questo modo hello Service Fabric resource provider tooconfigure per utilizzare per l'autenticazione del cluster e l'autenticazione server per l'endpoint di gestione.

##### <a name="virtual-machine-scale-set-resource"></a>Risorsa del set di scalabilità di macchine virtuali:
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a>Risorsa di Service Fabric:
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a>Inserire la configurazione di Azure AD
configurazione di Hello Azure Active Directory creato in precedenza può essere inseriti direttamente nel modello di gestione delle risorse. Tuttavia, è consigliabile prima di estrarre i valori hello in riutilizzabile modello parametri file tookeep hello Gestione risorse e privi di distribuzione tooa specifico di valori.

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### <a "configure-arm" ></a>Configurare i parametri del modello di Resource Manager
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
Infine, usare valori di output di hello dall'insieme di credenziali chiave di hello e file dei parametri di Azure AD PowerShell comandi toopopulate hello:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
A questo punto, è necessario disporre di hello degli elementi sul posto di seguito:

* Gruppo di risorse dell'insieme di credenziali delle chiavi
  * Insieme di credenziali delle chiavi
  * Certificato di autenticazione del server del cluster
  * Certificato di crittografia dei dati
* Tenant di Azure Active Directory
  * Applicazione Azure AD per la gestione basata su Web e Service Fabric Explorer
  * Applicazione Azure AD per la gestione dei client nativi
  * Utenti e ruoli assegnati
* Modello di Cluster Resource Manager di Service Fabric
  * Certificati configurati tramite l'insieme di credenziali delle chiavi
  * Azure Active Directory configurato

Hello seguente diagramma viene illustrato dove la chiave dell'insieme di credenziali e la configurazione di Azure AD rientrano nel modello di gestione delle risorse.

![Mappa di dipendenza di Resource Manager][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a>Creare il cluster hello
Si è ora cluster hello toocreate pronto utilizzando [la distribuzione dei modelli di risorse di Azure][resource-group-template-deploy].

#### <a name="test-it"></a>Eseguirne il test
Utilizzare il modello di gestione risorse di hello tootest comando PowerShell seguente con un file dei parametri:

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a>Distribuirlo
Se hello Gestione risorse modello test viene superato, utilizzare hello toodeploy comando PowerShell seguente un modello di gestione delle risorse con un file dei parametri:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a>Assegnare gli utenti tooroles
Dopo aver creato hello toorepresent di applicazioni del cluster, assegnare gli utenti ruoli toohello supportati dall'infrastruttura di servizio: sola lettura e l'amministratore. È possibile assegnare ruoli hello utilizzando hello [portale di Azure classico][azure-classic-portal].

1. Nel portale di Azure hello, andare tooyour tenant e quindi selezionare **applicazioni**.
2. Selezionare l'applicazione web hello, che ha un nome come `myTestCluster_Cluster`.
3. Fare clic su hello **utenti** scheda.
4. Selezionare un tooassign utente e quindi fare clic su hello **assegnare** pulsante in basso hello hello.

    ![Gli utenti tooroles pulsante Assegna][assign-users-to-roles-button]
5. Selezionare hello ruolo tooassign toohello utente.

    ![Finestra di dialogo "Assegna utenti"][assign-users-to-roles-dialog]

> [!NOTE]
> Per altre informazioni sui ruoli in Service Fabric, vedere [Controllo degli accessi in base al ruolo per i client di Service Fabric](service-fabric-cluster-security-roles.md).
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a>Creare cluster protetti in Linux
processo di hello toomake più semplice, sono disponibili un [script helper](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux). Prima di usare questo script helper, assicurarsi che sia già installata un'interfaccia della riga di comando di Azure e che sia nel percorso in uso. Assicurarsi che script hello disponga delle autorizzazioni tooexecute eseguendo `chmod +x cert_helper.py` dopo averlo scaricato. Hello primo passaggio consiste nell'account Azure tooyour toosign con CLI hello `azure login` comando. Dopo aver effettuato l'accesso tooyour account Azure, utilizzare hello helper script con l'autorità di certificazione firmato certificato, come hello seguente comando Mostra:

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

il parametro - ifile Hello può accettare un file con estensione pfx o un file con estensione PEM come input, con un tipo di hello certificato (pfx o pem oppure ss se si tratta di un certificato autofirmato).
parametro -h Hello stampato il testo della Guida hello.


Questo comando restituisce i seguenti tre stringhe come output di hello hello:

* SourceVaultID, ovvero ID hello per hello nuovo KeyVault ResourceGroup è creato per l'utente
* CertificateUrl per l'accesso a hello certificato
* CertificateThumbprint, usata per l'autenticazione.

Hello di esempio seguente viene illustrato come toouse hello comando:

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
L'esecuzione di hello precedente consente di comando hello tre stringhe, come indicato di seguito:

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

nome del soggetto del certificato Hello deve corrispondere dominio hello utilizzare cluster di Service Fabric tooaccess hello. Questa corrispondenza è obbligatorio tooprovide SSL per l'endpoint di gestione del cluster hello HTTPS e Service Fabric Explorer. È possibile ottenere un certificato SSL da un'autorità di certificazione per hello `.cloudapp.azure.com` dominio. È necessario ottenere un nome di dominio personalizzato per il cluster. Quando si richiede un certificato da un'autorità di certificazione, hello Nome soggetto del certificato deve corrispondere nome di dominio personalizzato hello utilizzati per il cluster.

Questi nomi di oggetto sono voci hello è necessario toocreate un cluster di Service Fabric sicuro (senza Azure AD), come descritto in [parametri di modello Configure Resource Manager](#configure-arm). È possibile connettersi toohello sicura cluster seguendo le istruzioni di hello per [cluster tooa di accesso client di autenticazione](service-fabric-connect-to-secure-cluster.md). I cluster di anteprima Linux non supportano l'autenticazione di Azure AD. È possibile assegnare ruoli amministratore e client, come descritto in hello [assegnare ruoli toousers](#assign-roles) sezione. Quando si specificano i ruoli di amministratore e il client per un cluster di anteprima di Linux, è necessario tooprovide identificazioni personali del certificato per l'autenticazione. (Non si specifica il nome di soggetto hello, perché non viene eseguita alcuna convalida della catena o revoche di certificati in questa versione di anteprima.)

Se si desidera toouse un certificato autofirmato per il test, è possibile utilizzare hello toogenerate script stesso uno. È quindi possibile caricare l'insieme di credenziali chiave hello certificato tooyour fornendo flag hello `ss` anziché specificare il nome del certificato hello percorso e il certificato. Ad esempio, vedere hello comando per la creazione e caricamento di un certificato autofirmato seguente:

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
Questo comando restituisce hello stesso tre stringhe: SourceVault CertificateUrl e CertificateThumbprint. È quindi possibile utilizzare hello stringhe toocreate sia un cluster protetto di Linux e un percorso in cui viene inserito certificato autofirmato hello. È necessario hello certificato autofirmato tooconnect toohello cluster. È possibile connettersi toohello sicura cluster seguendo le istruzioni di hello per [cluster tooa di accesso client di autenticazione](service-fabric-connect-to-secure-cluster.md).

nome del soggetto del certificato Hello deve corrispondere dominio hello utilizzare cluster di Service Fabric tooaccess hello. Questa corrispondenza è obbligatorio tooprovide SSL per l'endpoint di gestione del cluster hello HTTPS e Service Fabric Explorer. È possibile ottenere un certificato SSL da un'autorità di certificazione per hello `.cloudapp.azure.com` dominio. È necessario ottenere un nome di dominio personalizzato per il cluster. Quando si richiede un certificato da un'autorità di certificazione, hello Nome soggetto del certificato deve corrispondere nome di dominio personalizzato hello utilizzati per il cluster.

È possibile compilare i parametri di hello dallo script di supporto hello in hello portale di Azure, come descritto in hello [creare un cluster nel portale di Azure hello](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) sezione.

## <a name="next-steps"></a>Passaggi successivi
A questo punto, è stato creato un cluster con Azure Active Directory che fornisce l'autenticazione per la gestione. Successivamente, [connettersi cluster tooyour](service-fabric-connect-to-secure-cluster.md) e informazioni su come troppo[gestire segreti applicazione](service-fabric-application-secret-management.md).

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a>Risoluzione dei problemi di configurazione di Azure Active Directory per l'autenticazione client
Se verifica un problema mentre si sta configurando Azure AD per l'autenticazione client, esaminare le potenziali soluzioni hello in questa sezione.

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a>Si tooselect un certificato viene richiesto di Service Fabric Explorer
#### <a name="problem"></a>Problema
Dopo l'accesso correttamente in Service Fabric Explorer tooAzure Active Directory, il browser hello restituisce toohello home page di ma si tooselect un certificato verrà visualizzato un messaggio.

![Finestra di dialogo di selezione certificato in SFX][sfx-select-certificate-dialog]

#### <a name="reason"></a>Motivo
utente Hello non è assegnato un ruolo in hello applicazione cluster di Azure AD. Di conseguenza, l'autenticazione di Azure AD non riesce nel cluster di Service Fabric. Service Fabric Explorer fallback toocertificate autenticazione.

#### <a name="solution"></a>Soluzione
Seguire le istruzioni di hello per la configurazione di Azure AD e Assegna ruoli utente. Inoltre, è consigliabile attivare "Utente assegnazione tooaccess obbligatorio app", come `SetupApplications.ps1` does.

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a>Connessione con PowerShell non riesce con errore: "hello specificato credenziali non sono valide"
#### <a name="problem"></a>Problema
Quando si usa PowerShell tooconnect toohello cluster utilizzando la modalità di sicurezza "AzureActiveDirectory", dopo l'accesso correttamente tooAzure Active Directory, connessione hello ha esito negativo con errore: "hello specificato credenziali non sono valide."

#### <a name="solution"></a>Soluzione
Questa soluzione è hello che identico hello uno precedente.

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a>Service Fabric Explorer restituisce un errore durante l'accesso: "AADSTS50011"
#### <a name="problem"></a>Problema
Quando si tenta di toosign in tooAzure AD in Service Fabric Explorer, pagina hello restituisce un errore: "AADSTS50011: hello indirizzo di risposta &lt;url&gt; non corrispondono agli indirizzi di risposta hello configurati per l'applicazione hello: &lt;guid&gt;."

![Indirizzo di risposta di SFX non corrispondente][sfx-reply-address-not-match]

#### <a name="reason"></a>Motivo
un'applicazione Hello cluster (web) che rappresenta Service Fabric Explorer tenta tooauthenticate con Azure AD e come parte della richiesta di hello fornisce hello URL restituito di reindirizzamento. Ma hello URL non è elencato in un'applicazione hello Azure AD **URL di risposta** elenco.

#### <a name="solution"></a>Soluzione
In hello **configura** scheda di hello cluster applicazione (web), aggiungere hello URL di Service Fabric Explorer toohello **URL di risposta** elenco o sostituire uno degli elementi di hello nell'elenco di hello. Al termine, salvare la modifica.

![URL di risposta dell'applicazione Web][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a>Connettere il cluster di hello utilizzando l'autenticazione di Azure AD tramite PowerShell
cluster di Service Fabric hello tooconnect, utilizzare hello esempio di comando PowerShell seguente:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

toolearn sul cmdlet Connect-ServiceFabricCluster hello, vedere [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a>È possibile riutilizzare il tenant di hello stesso Azure Active Directory in più cluster?
Sì. Ma tenere presente che un'applicazione tooadd hello URL di Service Fabric Explorer tooyour cluster (web). In caso contrario, Service Fabric Explorer non funzionerà.

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a>Perché è ancora necessario un certificato del server se Azure AD è abilitato?
FabricClient e FabricGateway eseguono un'autenticazione reciproca. Durante l'autenticazione di Azure AD, integrazione di Azure AD fornisce un client server toohello delle identità e certificato del server hello è l'identità del server hello tooverify utilizzato. Per altre informazioni sui certificati di Service Fabric, vedere [Certificati X.509 e Service Fabric][x509-certificates-and-service-fabric].

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

