---
title: "scalabilità della macchina virtuale aaaAzure imposta domande frequenti | Documenti Microsoft"
description: "Ottenere risposte toofrequently domande frequenti su set di scalabilità di macchine virtuali."
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: 0deb9e2bb79f87f17bbf748397b94dc53070cfbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a>Domande frequenti sui set di scalabilità di macchine virtuali di Azure

Ottenere risposte imposta toofrequently domande frequenti sulla scalabilità della macchina virtuale in Azure.

## <a name="autoscale"></a>Autoscale

### <a name="what-are-best-practices-for-azure-autoscale"></a>Quali sono le procedure consigliate per la scalabilità automatica di Azure?

Per informazioni sulle procedure consigliate per la scalabilità automatica, vedere [Procedure consigliate per la scalabilità automatica delle macchine virtuali](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a>Dove è possibile trovare i nomi delle metriche per la scalabilità automatica che usa metriche basate su host?

Per informazioni sui nomi delle metriche per la scalabilità automatica che usa metriche basate su host, vedere [Metriche supportate con Monitoraggio di Azure](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a>Sono disponibili eventuali esempi di scalabilità automatica basata sull'argomento o sulla lunghezza della coda del bus di servizio di Azure?

Sì. Per esempi di scalabilità automatica basata sull'argomento o sulla lunghezza della coda del bus di servizio di Azure, vedere [Metriche comuni per la scalabilità automatica di Monitoraggio di Azure](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).

Per una coda del Bus di servizio, utilizzare hello JSON seguente:

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

Per una coda di archiviazione, usare hello JSON seguente:

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

Sostituire i valori dell'esempio con gli URI (Uniform Resource Identifier) della risorsa specifica.


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a>È consigliabile applicare la scalabilità automatica usando metriche basate su host oppure un'estensione di diagnostica?

È possibile creare un'impostazione di scalabilità automatica su una delle metriche a livello di host di macchina virtuale toouse metriche di base del sistema operativo guest.

Per un elenco delle metriche supportate, vedere [Metriche comuni per la scalabilità automatica di Monitoraggio di Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics). 

Per un esempio completo per i set di scalabilità di macchine virtuali, vedere [Configurazione di scalabilità automatica avanzata con modelli di Resource Manager per set di scalabilità di macchine virtuali](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets). 

esempio Hello utilizza metrica di CPU a livello di host hello e una metrica conteggio dei messaggi.



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a>Come si impostano le regole di avviso in un set di scalabilità di macchine virtuali?

È possibile creare avvisi sulle metriche per i set di scalabilità di macchine virtuali tramite PowerShell o l'interfaccia della riga di comando di Azure. Per altre informazioni, vedere [Esempi di avvio rapido con PowerShell per Monitoraggio di Azure](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) ed [Esempi di avvio rapido dell'interfaccia della riga di comando multipiattaforma di Monitoraggio di Azure](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).

ID risorsa di destinazione del set di scalabilità della macchina virtuale hello Hello è simile al seguente: 

/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname

È possibile scegliere qualsiasi contatore di prestazioni della macchina virtuale come tooset metrica hello un avviso per. Per ulteriori informazioni, vedere [le metriche del sistema operativo Guest per macchine virtuali basate su Gestione risorse di Windows](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) e [le metriche del sistema operativo Guest per le macchine virtuali Linux](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in hello [Monitor di Azure per la scalabilità automatica metriche di uso comune](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)articolo.

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a>Come si configura la scalabilità automatica in un set di scalabilità di macchine virtuali tramite PowerShell?

tooset di scalabilità automatica su una scala di macchina virtuale impostata per l'utilizzo di PowerShell, vedere post di blog hello [come tooan di scalabilità automatica tooadd scalabilità della macchina virtuale Azure impostare](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).




## <a name="certificates"></a>Certificati

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a>Come è forniti in modo sicuro un toohello certificato VM? Come è possibile implementare un toorun di set di scalabilità macchina virtuale un sito Web in cui hello SSL per il sito Web di hello viene fornito in modo sicuro da una configurazione del certificato? (operazione di rotazione hello comune certificato potrebbe essere quasi hello uguale a un'operazione di aggiornamento della configurazione.) Si dispone di un esempio di come toodo questo? 

toosecurely spedire toohello un certificato VM, è possibile installare un certificato cliente direttamente in un archivio certificati di Windows dall'insieme di credenziali chiave hello cliente.

Utilizzare hello JSON seguente:

```json
"secrets": [
    {
        "sourceVault": {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
        },
        "vaultCertificates": [
            {
                "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                "certificateStore": "certificateStoreName"
            }
        ]
    }
]
```

codice Hello supporta Windows e Linux.

Per altre informazioni, vedere [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx) (Creare o aggiornare un set di scalabilità di macchine virtuali).


### <a name="example-of-self-signed-certificate"></a>Esempio di certificato autofirmato

1.  Creare un certificato autofirmato in un insieme di credenziali delle chiavi.

    Utilizzare hello i comandi di PowerShell seguente:

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    In questo modo di comando hello input per il modello di Azure Resource Manager hello.

    Per un esempio di come toocreate un certificato autofirmato in un insieme di credenziali chiave, vedere [scenari di sicurezza di Service Fabric cluster](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).

2.  Modificare il modello di gestione risorse di hello.

    Aggiungere la proprietà troppo**virtualMachineProfile**, come parte di hello risorsa del set di scalabilità di macchine virtuali:

    ```json 
    "osProfile": {
        "computerNamePrefix": "[variables('namingInfix')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "secrets": [
            {
                "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                },
                "vaultCertificates": [
                    {
                        "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                        "certificateStore": "My"
                    }
                ]
            }
        ]
    }
    ```
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a>È possibile specificare un toouse coppia di chiavi SSH per l'autenticazione SSH con un set da un modello di gestione risorse di scalabilità macchina virtuale Linux?  

Sì. Hello API REST per **osProfile** è l'API REST di VM standard toohello simile. 

Includere **osProfile** nel modello:

```json 
"osProfile": {
    "computerName": "[variables('vmName')]",
    "adminUsername": "[parameters('adminUserName')]",
    "linuxConfiguration": {
        "disablePasswordAuthentication": "true",
        "ssh": {
            "publicKeys": [
                {
                    "path": "[variables('sshKeyPath')]",
                    "keyData": "[parameters('sshKeyData')]"
                }
            ]
        }
    }
}
```
 
Questo blocco JSON viene utilizzato [modello di avvio rapido di hello 101-vm-sshkey GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).
 
Hello profilo del sistema operativo viene usato anche in [grelayhost.json hello GitHub quick start modello](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).

Per altre informazioni, vedere [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration) (Creare o aggiornare un set di scalabilità di macchine virtuali).
  

### <a name="how-do-i-remove-deprecated-certificates"></a>Come si rimuovono i certificati deprecati? 

tooremove deprecata certificati, hello Rimuovi vecchio certificato dall'elenco di certificati dell'insieme di credenziali hello. Lasciare tutti i certificati di hello che si desidera tooremain nel computer in uso nell'elenco di hello. Ciò non rimuove il certificato di hello da tutte le macchine virtuali. Non viene inoltre aggiunta hello certificato toonew le macchine virtuali che vengono creati nel set di scalabilità della macchina virtuale hello. 

certificato di hello tooremove da macchine virtuali esistenti, scrivere uno script personalizzato estensione toomanually rimuovere hello certificati dall'archivio certificati.
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a>Come inserisce una chiave pubblica SSH esistente nel livello SSH set di scalabilità di hello macchina virtuale durante il provisioning Desiderano toostore hello SSH pubblici valori di chiave nell'insieme di credenziali chiave di Azure e quindi utilizzarle del modello di gestione risorse.

Se si desidera fornire hello macchine virtuali solo con una chiave SSH pubblica, non è necessario tooput hello le chiavi pubbliche nell'insieme di credenziali chiave. Le chiavi pubbliche non sono segrete.
 
Quando si crea una VM Linux è possibile fornire le chiavi pubbliche SSH in testo normale:

```json
"linuxConfiguration": {
    "ssh": {
        "publicKeys": [
            {
                "path": "path",
                "keyData": "publickey"
            }
        ]
    }
```
 
Nome dell'elemento linuxConfiguration | Obbligatorio | Tipo | Descrizione
--- | --- | --- | --- |  ---
ssh | No | Raccolta | Specifica di configurazione della chiave SSH hello per un sistema operativo Linux
path | Sì | String | Specifica percorso di file Linux hello in cui le chiavi SSH hello o un certificato deve essere collocato
keyData | Sì | String | Specifica una chiave pubblica SSH con codifica Base64

Per un esempio, vedere [modello di avvio rapido di hello 101-vm-sshkey GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a>Durante l'esecuzione di `Update-AzureRmVmss` dopo l'aggiunta di più di un certificato da hello stessa chiave dell'insieme di credenziali, viene visualizzato hello il seguente messaggio:
 
>Update-AzureRmVmss: L'elenco secrets contiene istanze ripetute di /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev. Questo scenario non è consentito.
 
Questa situazione può verificarsi se si tenta di toore-aggiungere hello stesso insieme di credenziali invece di usare un nuovo certificato dell'insieme di credenziali per l'insieme di credenziali origine esistente hello. Hello `Add-AzureRmVmssSecret` comando non funziona correttamente se si aggiungono i segreti aggiuntivi.
 
tooadd più segreti da hello stesso insieme di credenziali chiave, elenco $vmss.properties.osProfile.secrets[0].vaultCertificates hello di aggiornamento.
 
Per hello previsto struttura di input, vedere [crea o aggiorna una macchina virtuale impostata](https://msdn.microsoft.com/library/azure/mt589035.aspx).
 
Trovare segreto hello in hello macchina virtuale scala set oggetto nell'insieme di credenziali chiave hello. Aggiungere quindi l'elenco di toohello di riferimento (hello URL e il nome di archivio segreto hello) certificato associato all'insieme di credenziali hello.

> [!NOTE] 
> Attualmente, è possibile rimuovere i certificati da macchine virtuali tramite API di set di scalabilità di hello macchina virtuale.
>

Nuove macchine virtuali non avranno vecchio certificato hello. Tuttavia, le macchine virtuali che hanno certificato hello e che sono già state distribuite avranno vecchio certificato hello.
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a>È possibile il push scalabilità della macchina virtuale toohello certificati impostare senza specificare la password di hello, quando hello certificato si trova nell'archivio segreto hello?

Le password hardcoded toohard negli script non è necessario. È possibile recuperare in modo dinamico le password con autorizzazioni di hello è utilizzare script di distribuzione toorun hello. Se si dispone di uno script che consente di spostare un certificato dall'insieme di credenziali chiave archivio segreto hello, hello archivio segreto `get certificate` comando genera anche la password di hello del file con estensione pfx hello.
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a>Impostazione di lavoro proprietà segreti hello di virtualMachineProfile.osProfile per la scala di una macchina virtuale Perché necessario valore sourceVault hello quando si dispone di toospecify hello URI assoluto di un certificato utilizzando proprietà certificateUrl hello? 

Un riferimento al certificato di gestione remota Windows (WinRM) deve essere presente in hello proprietà segreti di hello profilo del sistema operativo. 

Hello indicante l'insieme di credenziali origine hello mira tooenforce controllo elenco (ACL) criteri di accesso esistono nel modello di servizio Cloud di Azure dell'utente. Se non è specificato l'insieme di credenziali origine hello, gli utenti che non dispone delle autorizzazioni toodeploy o accesso segreti tooa insieme di credenziali chiave sarebbe in grado di toothrough un Provider di risorse di calcolo (CRP). Gli elenchi di controllo di accesso sono presenti anche per risorse inesistenti.

Se si specifica un ID insieme di credenziali di origine non corretti ma un URL valido dell'insieme di credenziali chiave, viene restituito un errore quando si esegue il polling operazione hello.
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a>Se è possibile aggiungere i segreti tooan set di scalabilità della macchina virtuale esistente, i segreti hello vengono inseriti in macchine virtuali esistenti o solo in nuovi? 

I certificati vengono aggiunti tooall le macchine virtuali, preesistenti anche quelle. Se la scalabilità della macchina virtuale imposta proprietà upgradePolicy impostato è troppo**manuale**, certificato hello viene aggiunto toohello VM quando si esegue un aggiornamento manuale in hello macchina virtuale.
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a>Dove vengono inseriti i certificati per le macchine virtuali Linux?

toolearn toodeploy certificati per le macchine virtuali Linux, vedere [distribuire certificati tooVMs da un insieme di credenziali chiave gestita dal cliente](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a>Come è possibile aggiungere un nuovo insieme di credenziali tooa nuovo certificato oggetto certificato?

tooadd un insieme di credenziali tooan esistente chiave privata certificati, vedere hello esempio PowerShell seguente. Usare solo un oggetto segreto.
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a>Toocertificates cosa accade se si ricreare l'immagine di una macchina virtuale?

Se si ricrea l'immagine di una macchina virtuale, i certificati vengono eliminati. Ricreazione dell'immagine eliminazioni hello intero disco del sistema operativo. 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a>Cosa accade se si elimina un certificato dall'insieme di credenziali chiave hello?

Se il segreto hello viene eliminato dall'insieme di credenziali chiave hello e si eseguirà `stop deallocate` per tutte le macchine virtuali e riavviarle, si verificherà un errore. Errore Hello si verifica perché hello CRP deve segreti hello tooretrieve dall'insieme di credenziali chiave di hello, ma non è possibile. In questo scenario, è possibile eliminare i certificati di hello dal modello di set di scalabilità di hello macchina virtuale. 

componente CRP Hello non rende persistenti i segreti di cliente. Se si esegue `stop deallocate` per tutte le macchine virtuali nel set di scalabilità della macchina virtuale hello cache di hello viene eliminata. In questo scenario, vengono recuperati i segreti dall'insieme di credenziali chiave hello.

Quando la scalabilità perché è una copia memorizzata nella cache del segreto hello in Azure Service Fabric (nel modello di infrastruttura di singolo tenant hello), si non verifica questo problema.
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a>Perché hanno posizione esatta di hello toospecify per URL certificato hello (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), come indicato [scenari di sicurezza di Service Fabric cluster](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?
 
Hello documentazione insieme credenziali chiavi Azure si afferma che hello che ottenere API REST del segreto deve restituire più recente del segreto hello hello se hello versione non è specificata.
 
Metodo | URL
--- | ---
GET | https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}

Sostituire {*secret-name*} con nome hello e sostituire {*secret-version*} con la versione di hello del segreto hello desiderato tooretrieve. versione del segreto Hello potrebbe essere escluse. In tal caso, la versione corrente di hello viene recuperata.
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a>Motivo per cui dispone la versione dei certificati hello toospecify quando si usa l'insieme di credenziali chiave?

scopo di Hello della versione di hello insieme di credenziali chiave requisito toospecify hello certificato è toomake sia cancellare utente toohello il certificato viene distribuito in macchine virtuali di loro.

Se si crea una macchina virtuale e quindi aggiorna il segreto nell'insieme di credenziali chiave di hello, hello nuovo certificato non è macchine virtuali tooyour scaricato. Ma le macchine virtuali e nuove macchine virtuali ottengono nuovo segreto hello tooreference. tooavoid, si è tooreference richiesto una versione del segreto.

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a>Il team collabora con diversi certificati che vengono distribuiti toous come chiavi pubbliche con estensione cer. Che cos'è l'approccio per la distribuzione di questi set di scalabilità della macchina virtuale tooa certificati consigliato hello?

toodeploy con estensione cer chiavi pubbliche tooa scala set di macchine virtuali, è possibile generare un file con estensione pfx che contiene solo i file con estensione cer. toodo questa operazione, utilizzare `X509ContentType = Pfx`. Ad esempio, caricare il file con estensione cer hello come oggetto x509Certificate2 in c# o PowerShell e quindi chiamare il metodo hello. 

Per altre informazioni, vedere [Metodo X509Certificate.Export (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a>Un'opzione per gli utenti toopass nei certificati non vengono visualizzati come stringhe base64. disponibile nella maggior parte degli altri provider di risorse.

tooemulate passando un certificato come una stringa base64, è possibile estrarre hello più recente con controllo delle versioni URL in un modello di gestione risorse. Includere hello proprietà JSON nel modello di gestione delle risorse seguenti:

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a>È necessario che i certificati toowrap negli oggetti JSON in insiemi di credenziali chiave?

Nei set di scalabilità di macchine virtuali e nelle macchine virtuali è necessario eseguire il wrapping dei certificati in oggetti JSON. 

È anche supportata hello tipo di contenuto application/x-pkcs12. Per istruzioni sull'uso di application/x-pkcs12, vedere [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/) (Certificati PFX in Azure Key Vault).
 
Non sono attualmente supportati i file con estensione cer. file con estensione cer toouse, esportarli in contenitori con estensione pfx.



## <a name="compliance"></a>Conformità

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a>I set di scalabilità di macchine virtuali sono compatibili con PCI?

Set di scalabilità di macchine virtuali sono un livello API ridotto hello CRP. Entrambi i componenti fanno parte della piattaforma di calcolo hello in hello albero del servizio di Azure.

Da una prospettiva di conformità, il set di scalabilità di macchine virtuali è una parte fondamentale della piattaforma di calcolo di Azure hello. Un team, strumenti, processi, metodologia di distribuzione, i controlli di sicurezza, just-in-time (JIT) compilazione, il monitoraggio, avvisi e così via, condividono con CRP hello stesso. Set di scalabilità di macchine virtuali sono settore PCI (Payment Card)-conforme poiché hello CRP fa parte di attestazione di hello corrente PCI Data Security Standard (DSS).

Per ulteriori informazioni, vedere [hello Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).






## <a name="extensions"></a>Estensioni

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a>Come si elimina un'estensione del set di scalabilità di macchine virtuali?

toodelete un scalabilità della macchina virtuale imposta l'estensione, usare hello esempio PowerShell seguente:

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
È possibile trovare il valore extensionName hello in `$vmss`.
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a>È disponibile un esempio di modello di set di scalabilità di macchine virtuali che si integra con Operations Management Suite?

Per un scalabilità della macchina virtuale del set di esempio di modello che si integra con Operations Management Suite, vedere hello secondo esempio [distribuire un cluster di Azure Service Fabric e abilitare il monitoraggio tramite Log Analitica](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a>Estensioni sembrano toorun in parallelo in set di scalabilità di macchine virtuali. In questo modo il toofail estensione script personalizzato. È possibile procedere toofix questo?

toolearn sulla sequenziazione di estensione nel set di scalabilità di macchine virtuali, vedere [la sequenza di estensione nel set di scalabilità di macchine virtuali di Azure](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a>Come reimpostare la password di hello per le macchine virtuali nel set di scalabilità della macchina virtuale?

la password tooreset hello per le macchine virtuali nella scalabilità della macchina virtuale impostata, utilizzare le estensioni di accesso VM. 

Utilizzare hello esempio PowerShell seguente:

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a>Come è possibile aggiungere un tooall estensione macchine virtuali nel set di scalabilità della macchina virtuale?

Se i criteri di aggiornamento sono stato impostato troppo**automatico**, modello di ridistribuzione hello con nuove proprietà di estensione hello Aggiorna tutte le macchine virtuali.

Se i criteri di aggiornamento sono stato impostato troppo**manuale**, prima di aggiornare estensione hello e quindi aggiornare manualmente tutte le istanze di macchine virtuali.

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a>Se vengono aggiornate le estensioni di hello associate a un set di scalabilità macchina virtuale esistente, sono già macchine virtuali interessate? (Vale a dire verrà hello macchine virtuali *non* modello set di scalabilità macchina virtuale deve corrispondere hello?) O verranno ignorate? Quando un computer esistente viene riparato servizio o ricreata l'immagine, sono gli script hello attualmente configurate nel set di scalabilità della macchina virtuale hello eseguita o script hello che sono state configurate utilizzato hello che creazione macchina virtuale?

Se la definizione di estensione hello nella scalabilità della macchina virtuale hello Imposta modello viene aggiornato e hello upgradePolicy impostata troppo**automatico**, aggiorna le macchine virtuali hello. Se hello upgradePolicy impostata troppo**manuale**, le estensioni vengono contrassegnate come non corrisponde al modello hello. 

Se una macchina virtuale esistente viene riparato servizio, viene visualizzato come un riavvio ed estensioni hello non vengono eseguiti nuovamente. Se ricreata l'immagine, è come sostituzione di unità del sistema operativo hello con immagine di origine hello. Qualsiasi specializzazione dal modello più recente di hello, ad esempio le estensioni, vengono eseguiti.
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a>Come posso iscrivermi a un dominio di Azure AD tooan set scala macchina virtuale?

un dominio di Azure Active Directory (Azure AD) la macchina virtuale scala set tooan toojoin, è possibile definire un'estensione. 

toodefine un'estensione, usare proprietà JsonADDomainExtension hello:

```json
"extensionProfile": {
    "extensions": [
        {
            "name": "joindomain",
            "properties": {
                "publisher": "Microsoft.Compute",
                "type": "JsonADDomainExtension",
                "typeHandlerVersion": "1.3",
                "settings": {
                    "Name": "[parameters('domainName')]",
                    "OUPath": "[variables('ouPath')]",
                    "User": "[variables('domainAndUsername')]",
                    "Restart": "true",
                    "Options": "[variables('domainJoinOptions')]"
                },
                "protectedsettings": {
                    "Password": "[parameters('domainJoinPassword')]"
                }
            }
        }
    ]
}
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a>L'estensione della macchina virtuale scala set sta tentando di tooinstall qualcosa che richiede un riavvio. Ad esempio, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"

Se l'estensione di set di scalabilità macchina virtuale tenta tooinstall qualcosa che richiede un riavvio, è possibile utilizzare l'estensione di hello Azure Automation Desired State Configuration (DSC di automazione). Se hello del sistema operativo è Windows Server 2012 R2, Azure effettua il pull di installazione di Windows Management Framework (WMF) 5.0 hello, riavvii e continua quindi con configurazione hello. 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a>Come si attiva l'antimalware nel set di scalabilità di macchine virtuali?

tooturn su antimalware nella scalabilità della macchina virtuale impostata, utilizzare hello esempio PowerShell seguente:

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve hello most recent version number of hello extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a>È necessario tooexecute uno script personalizzato che è ospitato in un account di archiviazione privata. Hello script viene eseguito correttamente quando archiviazione hello è pubblico, ma quando si tenta di toouse una firma di accesso condiviso (SAS), si verifica un errore. Viene visualizzato questo messaggio: "Parametri obbligatori mancanti per la firma di accesso condiviso valida". Il collegamento e la firma di accesso condiviso funzionano correttamente.

tooexecute uno script personalizzato che è ospitato in un account di archiviazione privato, configurare impostazioni protette con nome e chiave dell'account di archiviazione hello. Per altre informazioni, vedere [Estensione Script personalizzato per Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).







## <a name="networking"></a>Rete
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a>È possibile tooassign imposta una scala tooa di sicurezza gruppo (rete), in modo che verrà applicato tooall hello, schede di rete VM nel set di hello?

Sì. Un gruppo di sicurezza di rete possono essere applicato direttamente il set di scalabilità di tooa per farvi riferimento nella sezione configurazioni hello hello di profilo di rete. Esempio:

```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                 }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a>Come procedere uno scambio VIP per set di scalabilità della macchina virtuale in hello stessa sottoscrizione e la stessa regione?

Se si dispone di due virtuale set di scalabilità della macchina con front-end di bilanciamento del carico di Azure e si trovano in hello stessa sottoscrizione e area, è Impossibile deallocare hello gli indirizzi IP pubblici da ognuno di essi e assegnare toohello altri. Per un esempio, vedere [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) (Scambio di indirizzi VIP: distribuzione di tipo "blu-verde" in Azure Resource Manager). Se come hello risorse vengono deallocati allocata a livello di rete hello, ciò implica un ritardo. Un'opzione più rapida è toouse Gateway applicazione Azure con due pool back-end e una regola di routing. In alternativa, è possibile ospitare l'applicazione con [Servizio app di Azure](https://azure.microsoft.com/en-us/services/app-service/) che offre il supporto per commutare rapidamente gli slot di gestione temporanea in slot di produzione.
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a>Come è possibile specificare un intervallo di toouse di indirizzi IP privati per l'assegnazione di indirizzo IP privato statico?

Gli indirizzi IP vengono selezionati da una subnet specificata. 

metodo di allocazione Hello di indirizzi IP di set di scalabilità macchina virtuale è sempre "dinamico", ma ciò non significa che è possono modificare questi indirizzi IP. In questo caso, "dinamico" solo significa che non si specifica l'indirizzo IP hello in una richiesta PUT. Specificare hello statico impostata per l'utilizzo di subnet hello. 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a>Come distribuire una macchina virtuale scala set tooan esistente rete virtuale di Azure? 

toodeploy un scalabilità della macchina virtuale impostata tooan esistente rete virtuale di Azure, vedere [distribuire una macchina virtuale scala set tooan rete virtuale esistente](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet). 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a>Come aggiungere l'indirizzo IP hello di hello set toohello output di un modello della macchina virtuale prima nella scala di una macchina virtuale?

indirizzo IP di hello tooadd di hello prima macchina virtuale in un output di toohello set di scalabilità macchina virtuale di un modello, vedere [ARM: indirizzi IP privati del VMSS ottenere](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a>È possibile usare i set di scalabilità con la rete accelerata?

Sì. toouse accelerated rete, impostazioni enableAcceleratedNetworking tootrue la scala del set di configurazioni. Ad esempio,
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
        "name": "niconfig1",
        "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
                ]
            }
            }
        ]
        }
    }
    ]
}
```

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a>Come è possibile configurare i server DNS hello utilizzati da un set di scalabilità

toocreate una scalabilità della macchina virtuale è impostato con una configurazione personalizzata di DNS, aggiungere che configurazioni sezione del set di una scala di toohello dnsSettings pacchetto JSON. Esempio:
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a>Come è possibile configurare un tooassign set scala un tooeach di indirizzo IP pubblico VM?

toocreate set di scalabilità di macchine Virtuali che assegna un tooeach di indirizzo IP pubblico macchina virtuale, assicurarsi hello API versione di hello Microsoft.Compute/virtualMAchineScaleSets risorse 2017-03-30 e aggiungere un _publicipaddressconfiguration_ pacchetto JSON set di scalabilità toohello di sezione di configurazione IP. Esempio:

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a>È possibile configurare un toowork di set di scalabilità con più applicazioni gateway?

Sì. È possibile aggiungere hello id risorse per più Gateway applicazione back-end indirizzo pool toohello _applicationGatewayBackendAddressPools_ elenco hello _configurazioni IP_ sezione del set di scalabilità profilo di rete.

## <a name="scale"></a>Scalabilità

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a>In quale caso è consigliabile creare un set di scalabilità di macchine virtuali con meno di due macchine virtuali?

Uno dei motivi toocreate impostare un scalabilità della macchina virtuale con meno di due macchine virtuali verrebbero impostate le proprietà elastico toouse hello di scalabilità di macchine virtuali. Ad esempio, è possibile distribuire un set di scalabilità della macchina virtuale con zero toodefine macchine virtuali dell'infrastruttura senza sostenere i costi di esecuzione delle macchine Virtuali. Quindi, quando si è pronti toodeploy VM, aumentare hello "capacità" di hello set di scalabilità di macchina virtuale toohello numero di istanze di produzione.

È possibile creare un set di scalabilità di macchine virtuali con meno di due VM anche se si è interessati principalmente all'uso di un set di disponibilità con VM discrete, invece che alla disponibilità. Set di scalabilità di macchine virtuali offrono un toowork modo con le unità di calcolo indifferenziato che fungibili. Questa uniformità è un elemento di differenziazione chiave tra set di scalabilità di macchine virtuali e set di disponibilità. Molti carichi di lavoro senza stato non tengono traccia delle singole unità. Se si riduce il carico di lavoro di hello, è possibile scalare verso il basso tooone unità di calcolo e quindi applicare la scalabilità verticale toomany quando aumenta il carico di lavoro di hello.

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a>Come è possibile modificare il numero di hello di macchine virtuali in un set di scalabilità della macchina virtuale?

numero di hello toochange di macchine virtuali in un set di scalabilità della macchina virtuale, vedere [modificare il numero di istanze hello di un set di scalabilità della macchina virtuale](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a>Come è possibile definire avvisi personalizzati per il raggiungimento di determinate soglie?

La gestione degli avvisi per le soglie specificate offre una certa flessibilità. È ad esempio possibile definire webhook personalizzati. Hello webhook esempio seguente è da un modello di gestione risorse:

```json
{
    "type": "Microsoft.Insights/autoscaleSettings",
    "apiVersion": "[variables('insightsApi')]",
    "name": "autoscale",
    "location": "[parameters('resourceLocation')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
    ],
    "properties": {
        "name": "autoscale",
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
        "enabled": true,
        "notifications": [
            {
                "operation": "Scale",
                "email": {
                    "sendToSubscriptionAdministrator": true,
                    "sendToSubscriptionCoAdministrators": true,
                    "customEmails": [
                        "youremail@address.com"
                    ]
                },
                "webhooks": [
                    {
                        "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                        "properties": {
                            "key1": "custommetric",
                            "key2": "scalevmss"
                        }
                    }
                ]
            }
        ],
```

In questo esempio, un avviso diventa tooPagerduty.com quando viene raggiunta una soglia.



## <a name="patching-and-operations"></a>Applicazione di patch e operazioni

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a>Come si crea un set di scalabilità in un gruppo di risorse esistente?

Creazione di set di scalabilità in una risorsa esistente gruppo non è ancora possibile da hello portale di Azure, ma è possibile specificare un gruppo di risorse esistente quando la distribuzione di una scala impostata da un modello di gestione risorse di Azure. È anche possibile specificare un gruppo di risorse esistente durante la creazione di un set di scalabilità usando Azure PowerShell o l'interfaccia della riga di comando.

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a>È possibile spostare che una scala di imposta il gruppo di risorse tooanother?

Sì, è possibile spostare la scala set di risorse tooa nuova sottoscrizione o gruppo di risorse.

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a>Come aggiornare tooI la scalabilità della macchina virtuale impostata tooa nuova immagine? Come si gestisce l'applicazione di patch?

vedere la scalabilità della macchina virtuale impostata tooa nuova immagine e l'applicazione di patch toomanage, tooupdate [l'aggiornamento di un set di scalabilità della macchina virtuale](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a>È possibile utilizzare tooreset operazione di ricreazione immagine hello una macchina virtuale senza modificare l'immagine di hello? (Vale a dire, desidera reimpostare un VM toofactory impostazioni anziché tooa nuova immagine.)

Sì, è possibile utilizzare tooreset operazione di ricreazione immagine hello una macchina virtuale senza modificare l'immagine di hello. Tuttavia, se è impostata la scalabilità della macchina virtuale fa riferimento a un'immagine della piattaforma con `version = latest`, la macchina virtuale è possibile aggiornare tooa successive del sistema operativo dell'immagine quando si chiama `reimage`.

Per altre informazioni, vedere [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set) (Gestire tutte le VM in un set di scalabilità di macchine virtuali).



## <a name="troubleshooting"></a>Risoluzione dei problemi

### <a name="how-do-i-turn-on-boot-diagnostics"></a>Come si attiva la diagnostica di avvio?

tooturn sulla diagnostica di avvio, creare innanzitutto un account di archiviazione. Quindi, inserire questo blocco JSON nel set di scalabilità di macchine virtuali **virtualMachineProfile**e aggiornare i set di scalabilità della macchina virtuale hello:

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

Quando viene creata una nuova macchina virtuale, hello proprietà InstanceView di hello VM Mostra i dettagli di hello schermata hello e così via. Ad esempio:
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a>Proprietà della macchina virtuale

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a>Come si possono ottenere informazioni sulle proprietà di ogni macchina virtuale senza dover eseguire più chiamate? Ad esempio, come sarebbe? il dominio di errore hello per ognuna delle hello 100 macchine virtuali nel set di scalabilità della macchina virtuale

informazioni proprietà di tooget per ogni macchina virtuale senza effettuare più chiamate, è possibile chiamare `ListVMInstanceViews` effettuando un'API REST `GET` su hello seguente URI di risorsa:

/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a>È possibile passo degli argomenti dell'estensione diverse macchine virtuali toodifferent in un set di scalabilità della macchina virtuale?

No, è possibile passare argomenti estensione diverse macchine virtuali toodifferent in un set di scalabilità della macchina virtuale. Tuttavia, le estensioni possono agire in base alle proprietà di univoco hello di hello VM vengono eseguiti in, ad esempio sul nome del computer hello. Estensioni anche possono eseguire una query i metadati dell'istanza in http://169.254.169.254 tooget ulteriori informazioni su hello macchina virtuale.

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a>Perché sono presenti gap tra i nomi delle macchine virtuali del set di scalabilità di macchine virtuali e gli ID, ad esempio 0, 1, 3?

Sono presenti interruzioni tra i nomi di computer VM set di scalabilità macchina virtuale e gli ID di macchina virtuale perché la scalabilità della macchina virtuale impostata **overprovision** proprietà è impostata un valore predefinito toohello di **true**. Se overprovisioning è troppo**true**, più macchine virtuali a quella richiesta vengono creati. Le VM aggiuntive vengono quindi eliminate. In questo caso, ottenere la distribuzione di una maggiore affidabilità ma spese hello di denominazione contigue e contigue Network Address Translation (NAT) delle regole. 

È possibile impostare questa proprietà troppo**false**. Per i set di scalabilità di macchine virtuali di piccole dimensioni ciò non influisce significativamente sull'affidabilità della distribuzione.

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a>Qual è la differenza hello tra l'eliminazione di una macchina virtuale in un set di scalabilità della macchina virtuale e la deallocazione hello VM? Quando è consigliabile scegliere uno hello altri?

Hello differenza principale tra l'eliminazione di una macchina virtuale in un set di scalabilità della macchina virtuale e la deallocazione hello VM è che `deallocate` non comporta l'eliminazione hello dischi rigidi virtuali (VHD). L'esecuzione di `stop deallocate` comporta costi di archiviazione. È possibile utilizzare uno o altro per uno dei seguenti motivi hello hello:

- Si desidera toostop sostenere i costi di calcolo, ma si desidera tookeep hello disco stato di hello macchine virtuali.
- Si desidera un set di macchine virtuali toostart più rapidamente è possibile scalare in orizzontale un set di scalabilità della macchina virtuale.
  - Scenario toothis correlati, si potrebbe essere creato il proprio motore di scalabilità automatica e si desidera una scala end-to-end più veloce.
- È presente un set di scalabilità di macchine virtuali distribuito in modo non uniforme nei domini di errore o nei domini di aggiornamento. Questo problema può essere stato causato dall'eliminazione selettiva di VM o dall'eliminazione di VM dopo l'overprovisioning. Esecuzione `stop deallocate` seguito da `start` nella macchina virtuale hello scala impostata in modo uniforme distribuisce le macchine virtuali hello tra domini di errore o di domini di aggiornamento.

