---
title: aaaCreate dell'infrastruttura del servizio cluster nel portale di Azure hello | Documenti Microsoft
description: In questo articolo viene descritto come tooset di un cluster di Service Fabric protetto in Azure tramite hello portale di Azure e l'insieme di credenziali chiave di Azure.
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a>Creare un cluster di Service Fabric in Azure utilizzando hello portale di Azure
> [!div class="op_single_selector"]
> * [Gestione risorse di Azure](service-fabric-cluster-creation-via-arm.md)
> * [Portale di Azure](service-fabric-cluster-creation-via-portal.md)
> 
> 

Si tratta di una Guida dettagliata che illustra hello passaggi di configurazione di un cluster di Service Fabric sicuro in Azure utilizzando hello portale di Azure. Questa guida illustra hello alla procedura seguente:

* Impostare le chiavi di toomanage insieme di credenziali chiave per la sicurezza del cluster.
* Creare un cluster protetto in Azure tramite hello portale di Azure.
* Autenticare gli amministratori che usano i certificati.

> [!NOTE]
> Per le opzioni di sicurezza avanzata, ad esempio l'autenticazione dell'utente con Azure Active Directory e la configurazione dei certificati per la protezione delle applicazioni, [creare il cluster usando Azure Resource Manager][create-cluster-arm].
> 
> 

Un cluster protetto è un cluster che impedisce le operazioni di accesso non autorizzato toomanagement, che include la distribuzione, aggiornamento ed eliminazione di applicazioni, servizi e dati hello in che essi contenuti. Un cluster non sicuro da un cluster che chiunque può connettersi tooat qualsiasi momento ed eseguire operazioni di gestione. Sebbene sia possibile toocreate un cluster non sicuro, è **consiglia un cluster protetto toocreate**. Un cluster non protetto **non può essere protetto in un secondo momento**. Sarà necessario crearne uno nuovo.

concetti di Hello sono hello stesso per la creazione di cluster sicuri, se il cluster hello è cluster Linux o i cluster di Windows. Per altre informazioni e script helper per la creazione di cluster Linux protetti, vedere [Creare cluster protetti in Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters). Hello parametri ottenuti dallo script di supporto hello fornito possono essere immesso direttamente nel portale di hello come descritto nella sezione hello [creare un cluster nel portale di Azure hello](#create-cluster-portal).

## <a name="log-in-tooazure"></a>Accedi tooAzure
Questa guida usa [Azure PowerShell][azure-powershell]. Quando si avvia una nuova sessione PowerShell, accedi tooyour account Azure e selezionare la sottoscrizione prima di eseguire i comandi di Azure.

Log nell'account azure tooyour:

```powershell
Login-AzureRmAccount
```

Selezionare la propria sottoscrizione:

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a>Configurare l'insieme di credenziali delle chiavi
Questa parte della Guida hello viene illustrata la creazione di un insieme di credenziali chiave per un cluster di Service Fabric in Azure e per le applicazioni di Service Fabric. Per una guida completa in insieme di credenziali chiave, vedere hello [Guida introduttiva di insieme di credenziali chiave][key-vault-get-started].

Service Fabric utilizza toosecure certificati x. 509 un cluster. Insieme di credenziali chiave di Azure è toomanage utilizzati certificati per i cluster di Service Fabric in Azure. Quando viene distribuito un cluster in Azure, provider di risorse di Azure hello responsabile per la creazione di cluster di Service Fabric estrae i certificati dall'insieme di credenziali chiave e li installa nel cluster hello macchine virtuali.

Hello diagramma seguente illustra la relazione hello tra l'insieme di credenziali chiave, un cluster di Service Fabric e provider di risorse di Azure hello che utilizza i certificati archiviati nell'insieme di credenziali chiave durante la creazione di un cluster:

![Installazione del certificato][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>Creare un gruppo di risorse
primo passaggio Hello è toocreate un nuovo gruppo di risorse in modo specifico per l'insieme di credenziali chiave. Inserimento di insieme di credenziali chiave nel proprio gruppo di risorse, in modo che sia possibile rimuovere gruppi di risorse di calcolo e archiviazione, ad esempio gruppo di risorse hello con il cluster di Service Fabric - è consigliabile senza perdere le chiavi e segreti. gruppo di risorse Hello con l'insieme di credenziali chiave deve essere in hello stessa area geografica hello cluster che lo usa.

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a>Creare un insieme di credenziali delle chiavi
Creare un insieme di credenziali chiave nel nuovo gruppo di risorse hello. insieme di credenziali chiave Hello **deve essere abilitato per la distribuzione** tooallow hello certificati di infrastruttura servizio risorsa provider tooget da esso e installare nei nodi del cluster:

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
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

Se si dispone già di un insieme di credenziali delle chiavi, è possibile abilitarlo per la distribuzione tramite l'interfaccia della riga di comando di Azure:

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a>Aggiungere certificati tooKey insieme di credenziali
I certificati vengono usati in Service Fabric tooprovide autenticazione e crittografia toosecure vari aspetti di un cluster e le relative applicazioni. Per altre informazioni sull'uso dei certificati in Service Fabric, vedere [Scenari di sicurezza di un cluster di Service Fabric][service-fabric-cluster-security].

### <a name="cluster-and-server-certificate-required"></a>Cluster e certificato del server (obbligatorio)
Questo certificato è obbligatorio toosecure un cluster e impedire l'accesso non autorizzato tooit. Il certificato fornisce protezione del cluster in due modi:

* **Autenticazione del cluster:** autentica la comunicazione da nodo a nodo per la federazione di cluster. Solo i nodi che è possano provare la propria identità con il certificato è possono aggiungere il cluster hello.
* **L'autenticazione del server:** autentica hello cluster Gestione endpoint tooa client di gestione, in modo che hello gestione client riconosce stia comunicando toohello reale cluster. Questo certificato fornisce inoltre SSL per l'API di gestione HTTPS hello e per Service Fabric Explorer tramite HTTPS.

tooserve questi scopi, certificato hello deve soddisfare i seguenti requisiti hello:

* certificato di Hello deve contenere una chiave privata.
* Hello certificato deve essere creato per lo scambio di chiave, esportabile tooa file di scambio di informazioni personali (PFX).
* Hello nome soggetto del certificato deve corrispondere hello dominio utilizzato tooaccess hello dell'infrastruttura del servizio cluster. Questo è necessario tooprovide SSL per l'endpoint di gestione HTTPS del cluster hello e Service Fabric Explorer. È possibile ottenere un certificato SSL da un'autorità di certificazione (CA) per hello `.cloudapp.azure.com` dominio. Acquistare un nome di dominio personalizzato per il cluster. Quando si richiede un certificato dal nome del soggetto del certificato CA hello deve corrispondere il nome di dominio personalizzato hello utilizzato per il cluster.

### <a name="client-authentication-certificates"></a>Certificati di autenticazione client
I certificati client aggiuntivi autenticano gli amministratori per le attività di gestione del cluster. Service Fabric ha due livelli di accesso: **admin** e **utente di sola lettura**. Deve essere usato almeno un certificato per l'accesso amministrativo. Per l'accesso aggiuntivo a livello di utente, è necessario specificare un certificato separato. Per altre informazioni sui ruoli di accesso, vedere [Controllo degli accessi in base al ruolo per i client di Service Fabric][service-fabric-cluster-security-roles].

Non è necessario tooupload Client l'autenticazione dei certificati tooKey insieme di credenziali toowork con Service Fabric. Questi certificati sufficiente toobe fornita toousers autorizzati per la gestione di cluster. 

> [!NOTE]
> Azure Active Directory è hello consigliato client tooauthenticate modo per cluster di operazioni di gestione. toouse Azure Active Directory, è necessario [creare un cluster con Azure Resource Manager][create-cluster-arm].
> 
> 

### <a name="application-certificates-optional"></a>Certificati delle applicazioni (facoltativo)
Per motivi di sicurezza dell'applicazione, è possibile installare nel cluster numerosi certificati aggiuntivi. Prima di creare il cluster, considerare gli scenari di sicurezza dell'applicazione hello che richiedono un toobe certificato installato nei nodi di hello, ad esempio:

* Crittografia e decrittografia dei valori di configurazione dell'applicazione
* Crittografia dei dati tra i nodi durante la replica 

I certificati dell'applicazione non possono essere configurati durante la creazione di un cluster tramite il portale di Azure hello. tooconfigure i certificati dell'applicazione in fase di installazione del cluster, è necessario [creare un cluster con Azure Resource Manager][create-cluster-arm]. È anche possibile aggiungere cluster toohello certificati di applicazione dopo che è stato creato.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Formattazione dei certificati per l'uso di provider di risorse di Azure
I file di chiave privata (con estensione pfx) possono essere aggiunti e usati direttamente tramite l'insieme di credenziali delle chiavi. Tuttavia, il provider di risorse di Azure hello richiede toobe chiavi archiviate in un particolare formato JSON che include PFX hello come una base 64 codificata stringa hello e la password della chiave privata. tooaccommodate questi requisiti, le chiavi devono essere inseriti in una stringa JSON e quindi archiviati come *segreti* nell'insieme di credenziali chiave.

è un modulo di PowerShell toomake questo processo più semplice, [disponibile in GitHub][service-fabric-rp-helpers]. Seguire questi modulo hello toouse di passaggi:

1. Scaricare l'intero contenuto di hello del repository hello in una directory locale. 
2. Importare il modulo hello nella finestra di PowerShell:

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

Hello `Invoke-AddCertToKeyVault` comando in questo modulo di PowerShell Formatta automaticamente una chiave privata del certificato in una stringa JSON e ne carica tooKey insieme di credenziali. Usarlo certificato di cluster tooadd hello e qualsiasi tooKey certificati applicazione aggiuntiva dell'insieme di credenziali. Ripetere questo passaggio per tutti i certificati aggiuntivi desiderate tooinstall del cluster.

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

Questi sono tutti i prerequisiti di hello insieme di credenziali chiave per la configurazione di un modello di gestione risorse di cluster di Service Fabric che consente di installare i certificati per l'autenticazione di nodo, protezione di endpoint di gestione e l'autenticazione e qualsiasi maggiore sicurezza dell'applicazione funzionalità che utilizzano certificati x. 509. A questo punto, è ora necessario hello dopo l'installazione in Azure:

* Gruppo di risorse dell'insieme di credenziali delle chiavi
  * Insieme di credenziali di chiave
    * Certificato di autenticazione del server del cluster

</a "create-cluster-portal" ></a>

## <a name="create-cluster-in-hello-azure-portal"></a>Creare cluster in hello portale di Azure
### <a name="search-for-hello-service-fabric-cluster-resource"></a>Cercare hello risorsa cluster di Service Fabric
![ricerca per il modello di cluster di Service Fabric nel portale di Azure hello.][SearchforServiceFabricClusterTemplate]

1. Accedi toohello [portale di Azure][azure-portal].
2. Fare clic su **New** tooadd un nuovo modello di risorsa. Ricerca per il modello di Cluster di Service Fabric hello in hello **Marketplace** in **tutto**.
3. Selezionare **Cluster di Service Fabric** dall'elenco di hello.
4. Passare toohello **Cluster di Service Fabric** pannello, fare clic su **crea**,
5. Hello **cluster di Service Fabric crea** pannello è hello seguenti quattro passaggi.

#### <a name="1-basics"></a>1. Nozioni di base
![Schermata della creazione di un nuovo gruppo di risorse.][CreateRG]

Nel Pannello di nozioni di base hello tooprovide dettagli di base hello è necessario per il cluster.

1. Immettere il nome di hello del cluster.
2. Immettere un **nome utente** e **password** per Desktop remoto per hello macchine virtuali.
3. Verificare che hello tooselect **sottoscrizione** che si desidera toobe il cluster della distribuzione, soprattutto se si dispone di più sottoscrizioni.
4. Creare un **nuovo gruppo di risorse**. È migliore toogive hello stesso nome cluster hello, poiché è utile nella ricerca in un secondo momento, soprattutto quando si sta tentando di toomake modifiche tooyour distribuzione o Elimina il cluster.
   
   > [!NOTE]
   > Sebbene sia possibile decidere toouse un gruppo di risorse esistente, è toocreate una buona norma un nuovo gruppo di risorse. Questo rende facile toodelete cluster che non è necessario.
   > 
   > 
5. Seleziona hello **area** in cui si desidera che il cluster di hello toocreate. È necessario utilizzare hello stessa regione che la chiave dell'insieme di credenziali è in.

#### <a name="2-cluster-configuration"></a>2. Configurazione del cluster
![Creare un tipo di nodo][CreateNodeType]

Configurare i nodi del cluster. Tipi di nodo definiscono dimensioni di macchina virtuale hello, hello numero di macchine virtuali e le relative proprietà. Il cluster può avere più di un tipo di nodo, ma il tipo di nodo primario hello (primo definiti nel portale di hello hello) deve disporre di almeno cinque macchine virtuali, come questo è il tipo di nodo hello in cui vengono collocati i servizi di sistema di Service Fabric. Non è necessario configurare le **proprietà relative alla posizione**, perché una proprietà relativa alla posizione predefinita "NodeTypeName" viene aggiunta automaticamente.

> [!NOTE]
> Uno scenario comune per diversi tipi di nodi è costituito da un'applicazione contenente un servizio front-end e un servizio back-end. Si desidera tooput servizio front-end di hello in macchine virtuali più piccoli (dimensioni di macchina virtuale come D2) con le porte aperte toohello Internet, ma si vuole servizio back-end di hello tooput nelle macchine virtuali di dimensioni maggiori (con dimensioni di macchina virtuale come D4, D6, D15 e così via) e senza con connessione Internet di porte aperte.
> 
> 

1. Scegliere un nome per il tipo di nodo (1 too12 caratteri contenente solo lettere e numeri).
2. Hello minimo **dimensioni** dovuto di macchine virtuali per nodo primario hello hello tipo **durabilità** livello scelto per il cluster hello. valore predefinito di Hello per il livello di durabilità hello è Bronzo. Per ulteriori informazioni sulla durabilità, vedere [come toochoose hello Service Fabric cluster e affidabilità][service-fabric-cluster-capacity].
3. Selezionare dimensioni della macchina virtuale hello e il piano tariffario. Le macchine virtuali della serie D dispongono di unità SSD e sono consigliate per applicazioni con stato. Non usare SKU di VM con core parziali o meno di 7 GB di capacità disco disponibile. 
4. Hello minimo **numero** dovuto di macchine virtuali per nodo primario hello hello tipo **affidabilità** livello desiderato. valore predefinito di Hello per il livello di affidabilità hello è Silver. Per ulteriori informazioni sull'affidabilità, vedere [come toochoose hello Service Fabric cluster e affidabilità][service-fabric-cluster-capacity].
5. Scegliere hello numero di macchine virtuali per il tipo di nodo hello. È possibile ridimensionare verso l'alto o verso il basso numero hello di macchine virtuali in un tipo di nodo in un secondo momento, ma nel tipo di nodo primario hello, hello minima dipende dal livello di affidabilità hello che si è scelto. Gli altri tipi di nodo possono avere un minimo di 1 VM.
6. Configurare gli endpoint personalizzati. Questo campo consente un elenco delimitato da virgole di porte che si desidera tooexpose tramite hello bilanciamento del carico di Azure toohello tooenter rete Internet pubblica per le applicazioni. Ad esempio, se si prevede un cluster di tooyour applicazione web toodeploy, immettere "80" tooallow traffico sulla porta 80 in cluster. Per altre informazioni sugli endpoint, vedere [Comunicazioni con le applicazioni][service-fabric-connect-and-communicate-with-services]
7. Configurare la **diagnostica**del cluster. Per impostazione predefinita, in tooassist il cluster con la risoluzione dei problemi è abilitata la diagnostica. Se si desidera modifica di diagnostica toodisable hello **stato** attivare o disattivare troppo**Off**. **Non** è consigliabile disattivare la diagnostica.
8. Selezionare hello modalità si desidera impostare il cluster di aggiornamento dell'infrastruttura. Selezionare **automatico**, se si desidera hello sistema tooautomatically preleva hello versione più recente e provare tooupgrade tooit il cluster. Impostare la modalità di hello troppo**manuale**, se si desidera toochoose una versione supportata.

> [!NOTE]
> Microsoft supporta solo i cluster che eseguono versioni supportate di Service Fabric. Selezionando hello **manuale** modalità, si assume hello responsabilità tooupgrade versione tooa supportato cluster. Per ulteriori informazioni sulle modalità di aggiornamento dell'infrastruttura di hello vedere hello [documento di aggiornamento del cluster di infrastruttura del servizio.][service-fabric-cluster-upgrade]
> 
> 

#### <a name="3-security"></a>3. Sicurezza
![Schermata delle configurazioni di sicurezza nel portale di Azure.][SecurityConfigs]

passaggio finale Hello è cluster tooprovide certificato informazioni toosecure hello utilizzando hello insieme di credenziali chiave e un certificato creato in precedenza.

* Compilare i campi di un certificato primario hello con output di hello ottenuto dal caricamento hello **certificato cluster** tooKey insieme di credenziali usando hello `Invoke-AddCertToKeyVault` comando di PowerShell.

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* Controllare hello **configurare le impostazioni avanzate** casella certificati client tooenter per **amministratore client** e **client di sola lettura**. In questi campi, immettere identificazione personale hello del certificato client di amministrazione e l'identificazione personale hello del certificato client utente di sola lettura, se applicabile. Quando gli amministratori tentano tooconnect toohello cluster, essi vengono concesse immesso accesso solo se dispongono di un certificato con identificazione personale che corrispondono ai valori hello identificazione personale.  

#### <a name="4-summary"></a>4. Riepilogo
![Cattura di schermata della scheda avvio hello visualizzazione "Distribuzione Cluster di Service Fabric." ][Notifications]

creazione del cluster hello toocomplete, fare clic su **riepilogo** le configurazioni di hello toosee che hanno fornito o scaricare hello modello di gestione risorse di Azure che utilizzato toodeploy del cluster. Dopo aver fornito le impostazioni obbligatorie hello, hello **OK** pulsante diventa di colore verde, è possibile iniziare il processo hello facendovi clic sopra.

È possibile visualizzare lo stato di avanzamento di hello creazione nelle notifiche hello. (Fare clic sull'icona di campanello"hello" nella barra di stato hello in alto hello destra dello schermo). Se fa clic su **Pin tooStartboard** durante la creazione di cluster hello, si noterà **la distribuzione di Cluster di Service Fabric** bloccato toohello **avviare** Lavagna.

### <a name="view-your-cluster-status"></a>Visualizzare lo stato del cluster
![Cattura di schermata dei dettagli di cluster nel dashboard di hello.][ClusterDashboard]

Una volta creato il cluster, è possibile controllare il cluster nel portale di hello:

1. Andare troppo**Sfoglia** e fare clic su **servizio infrastruttura cluster**.
2. Trovare il cluster e selezionarlo.
3. È ora possibile visualizzare i dettagli di hello del cluster nel dashboard di hello, tra cui endpoint pubblico del cluster hello e tooService un collegamento Fabric Explorer.

Hello **nodo Monitoraggio** sezione nel Pannello di dashboard del cluster hello indica il numero di hello di macchine virtuali che sono integri e non integro. È possibile trovare altre informazioni sull'integrità del cluster hello in [introduzione di modello di integrità dell'infrastruttura a servizio][service-fabric-health-introduction].

> [!NOTE]
> I cluster di Service Fabric richiedono un certo numero di nodi toobe di disponibilità AlwaysOn toomaintain e mantengono lo stato, di cui viene fatto riferimento tooas "gestione quorum". Pertanto, non è in genere sicura tooshut verso il basso tutti i computer nel cluster hello a meno che non è stata innanzitutto eseguita una [backup completo dello stato del][service-fabric-reliable-services-backup-restore].
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a>Istanza di tooa Set di scalabilità della macchina virtuale o un nodo del cluster della connessione remota
Ognuno di hello NodeTypes specificate nei risultati del cluster in un riquadro attività di configurazione Set di scalabilità macchina virtuale. Vedere [tooa istanza del Set di scalabilità della macchina virtuale di connettersi in remoto] [ remote-connect-to-a-vm-scale-set] per informazioni dettagliate.

## <a name="next-steps"></a>Passaggi successivi
A questo punto, è stato creato un cluster protetto tramite i certificati per l'autenticazione di gestione. Successivamente, [connettersi cluster tooyour](service-fabric-connect-to-secure-cluster.md) e informazioni su come troppo[gestire segreti applicazione](service-fabric-application-secret-management.md).  Vedere anche [Service Fabric support options](service-fabric-support.md) (Opzioni di supporto di Service Fabric).

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
