---
title: aaaSecure la chiave dell'insieme di credenziali | Documenti Microsoft
description: Gestire le autorizzazioni di accesso per un insieme di credenziali delle chiavi per controllare insiemi di credenziali, chiavi e segreti. Modello di autenticazione e autorizzazione per l'insieme di credenziali delle chiavi e come toosecure la chiave dell'insieme di credenziali
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e5b4e083-4a39-4410-8e3a-2832ad6db405
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 84f5fc18142a1ad89babbd11f4f65eca105afc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-key-vault"></a>Proteggere l'insieme di credenziali delle chiavi
Insieme di credenziali delle chiavi di Azure è un servizio cloud che consente di proteggere le chiavi di crittografia e i segreti (ad esempio, certificati, stringhe di connessione e password) per le applicazioni cloud. Poiché i dati sensibili e critici per il business, si desidera toosecure accesso tooyour chiave gli insiemi di credenziali in modo che solo dalle applicazioni autorizzate e gli utenti possono accedere a insieme di credenziali chiave. In questo articolo viene fornita una panoramica del modello di insieme di credenziali chiave di accesso, illustra l'autenticazione e autorizzazione e viene descritto come toosecure accesso tookey insieme di credenziali per le applicazioni cloud con un esempio.

## <a name="overview"></a>Panoramica
Insieme di credenziali chiave di accesso tooa viene controllato tramite due interfacce separate: piano di gestione e di dati. Per entrambi i piani autenticazione appropriato e l'autorizzazione è necessaria prima di un chiamante (un utente o un'applicazione) può ottenere l'insieme di credenziali di accesso tookey. L'autenticazione stabilisce l'identità di hello del chiamante hello, mentre l'autorizzazione determina quali chiamante hello operazioni tooperform.

Per l'autenticazione, sia il piano di gestione sia il piano dati usano Azure Active Directory. Per l'autorizzazione, il piano di gestione usa il controllo degli accessi in base al ruolo, mentre il piano dati usa i criteri di accesso dell'insieme di credenziali delle chiavi.

Di seguito è riportata una breve panoramica di hello argomenti trattati:

[Autenticazione tramite Azure Active Directory](#authentication-using-azure-active-directory) -questa sezione viene illustrato come un chiamante effettua l'autenticazione con Azure Active Directory tooaccess un insieme di credenziali chiave tramite Gestione piano e di dati. 

[Piano di gestione e piano dati](#management-plane-and-data-plane): questi sono i due piani usati per accedere all'insieme di credenziali delle chiavi. Ogni piano di accesso supporta operazioni specifiche. In questa sezione descrive gli endpoint di accesso di hello, le operazioni supportate e accedere al metodo di controllo utilizzato da ogni piano. 

[Controllo di accesso di gestione piano](#management-plane-access-control) : In questa sezione esamineremo accedendo operazioni piano toomanagement utilizzando il controllo di accesso basato sui ruoli.

[Controllo di accesso ai dati piano](#data-plane-access-control) -questa sezione viene descritto come il piano di accesso dati di toocontrol dei criteri di accesso di toouse insieme di credenziali chiave.

[Esempio](#example) -in questo esempio viene descritto come toosetup controllo dell'accesso per l'insieme di credenziali chiave tooallow tre diversi team (team addetto alla sicurezza, gli sviluppatori/operatori e i revisori) tooperform toodevelop di attività specifiche, gestire e monitorare un'applicazione in Azure .

## <a name="authentication-using-azure-active-directory"></a>Autenticazione tramite Azure Active Directory
Quando si crea un insieme di credenziali chiave in una sottoscrizione di Azure, è associato automaticamente al tenant di Azure Active Directory della sottoscrizione hello. Tutti i chiamanti (utenti e applicazioni) devono essere registrati in questa tooaccess tenant questo insieme di credenziali chiave. Insieme di credenziali chiave di Azure Active Directory tooaccess deve autenticare un utente o un'applicazione. Si applica tooboth gestione piano e dati access. In entrambi i casi, un'applicazione può accedere a un insieme di credenziali delle chiavi in due modi:

* **accesso utente+app**: in genere questo meccanismo viene usato per le applicazioni che accedono all'insieme di credenziali delle chiavi per conto di un utente connesso. Azure PowerShell e il portale di Azure offrono un esempio di questo tipo di accesso. Esistono due modi toogrant accesso toousers: unidirezionale è toogrant accesso toousers consentire l'accesso da qualsiasi applicazione dell'insieme di credenziali chiave e hello altro modo è un insieme di credenziali utente tookey accesso toogrant solo quando un'applicazione specifica (identità composta di cui viene fatto riferimento tooas). 
* **solo app accesso** : per le applicazioni che esegue servizi daemon, processi in background viene concessa l'identità dell'applicazione hello e così via. accedere toohello chiave dell'insieme di credenziali.

In entrambi i tipi di applicazioni, applicazione hello esegue l'autenticazione con Azure Active Directory utilizzando uno dei hello [metodi di autenticazione supportati](../active-directory/active-directory-authentication-scenarios.md) e acquisisce un token. Metodo di autenticazione utilizzato dipende dal tipo di applicazione hello. L'applicazione hello viene utilizzato questo token e invia l'insieme di credenziali tookey richiesta API REST. In caso di hello accesso piano di gestione delle richieste vengono indirizzate attraverso endpoint di gestione risorse di Azure. Quando si accede a piano dati, applicazioni hello comunica direttamente tooa endpoint di insieme di credenziali chiave. Visualizzare ulteriori dettagli su hello [flusso di autenticazione intero](../active-directory/active-directory-protocols-oauth-code.md). 

nome della risorsa Hello per cui un'applicazione hello richiede un token è diversa a seconda se accede a un'applicazione hello piano di gestione o un piano di dati. Nome risorsa hello è pertanto gestione piano o dati piano estremità descritte nella tabella hello in una sezione successiva, a seconda di hello ambiente Azure.

Con un singolo meccanismo per l'autenticazione tooboth piano dati e la gestione presenta un proprio vantaggi:

* Le organizzazioni possono controllare in modo centralizzato accesso tooall chiave gli insiemi di credenziali nella propria organizzazione
* Se un utente lascia, immediatamente perdono l'accesso tooall insiemi di credenziali chiave organizzazione hello
* È possibile personalizzare l'autenticazione tramite le opzioni di hello in Azure Active Directory (ad esempio, l'abilitazione autenticazione a più fattori per una maggiore sicurezza)

## <a name="management-plane-and-data-plane"></a>Piano di gestione e piano dati
Insieme di credenziali delle chiavi è un servizio di Azure disponibile tramite il modello di distribuzione Azure Resource Manager. Quando si crea un insieme di credenziali delle chiavi, si ottiene un contenitore virtuale nel quale è possibile creare altri oggetti come chiavi, segreti e certificati. Quindi possibile accedere credenziali delle chiavi utilizzando Gestione piano e piano tooperform specifiche operazioni sui dati. Interfaccia di gestione del piano è toomanage utilizzati insieme di credenziali della chiave stessa, ad esempio di creazione, eliminazione, aggiornamento degli attributi di chiave dell'insieme di credenziali e l'impostazione di criteri di accesso per il piano di dati. Interfaccia piano dati è utilizzato tooadd, eliminare, modificare e utilizzare chiavi hello, i segreti e dei certificati archiviati nell'insieme di credenziali chiave.

Hello piano e dati piano le interfacce di gestione sono accessibili tramite diversi endpoint (vedere la tabella). Hello seconda colonna hello tabella descrive i nomi DNS hello per questi endpoint in diversi ambienti di Azure. terza colonna Hello descrive le operazioni di hello che è possibile eseguire dal piano ogni accesso. Ognuno dei piani ha anche uno specifico meccanismo di controllo di accesso: per il piano di gestione viene usato il controllo degli accessi in base al ruolo di Azure Resource Manager, mentre per il piano dati vengono usati i criteri di accesso dell'insieme di credenziali delle chiavi.

| Piano di accesso | Endpoint di accesso | Operazioni | Meccanismo di controllo di accesso |
| --- | --- | --- | --- |
| Piano di gestione |**Globale:**<br> management.azure.com:443<br><br> **Azure per la Cina:**<br> management.chinacloudapi.cn:443<br><br> **Azure per enti pubblici statunitensi:**<br> management.usgovcloudapi.net:443<br><br> **Azure per la Germania:**<br> management.microsoftazure.de:443 |Creare/Leggere/Aggiornare/Eliminare l'insieme di credenziali delle chiavi <br> Impostare criteri di accesso per l'insieme di credenziali delle chiavi<br>Impostare tag per l'insieme di credenziali delle chiavi |Controllo degli accessi in base al ruolo di Azure Resource Manager |
| Piano dati |**Globale:**<br> &lt;nome-insiemecredenziali&gt;.vault.azure.net:443<br><br> **Azure per la Cina:**<br> &lt;nome-insiemecredenziali&gt;.vault.azure.cn:443<br><br> **Azure per enti pubblici statunitensi:**<br> &lt;nome-insiemecredenziali&gt;.vault.usgovcloudapi.net:443<br><br> **Azure per la Germania:**<br> &lt;nome-insiemecredenziali&gt;.vault.microsoftazure.de:443 |Per le chiavi: Decrypt, Encrypt, UnwrapKey, WrapKey, Verify, Sign, Get, List, Update, Create, Import, Delete, Backup, Restore<br><br> Per i segreti: Get, List, Set, Delete |Criteri di accesso dell'insieme di credenziali delle chiavi |

Hello gestione piano e dati piano i controlli di accesso funzionano in modo indipendente. Ad esempio, se si desidera toogrant un'applicazione toouse tasti di scelta in un insieme di credenziali chiave, è necessario solo toogrant piano le autorizzazioni di accesso tramite criteri di accesso dell'insieme di credenziali chiave e nessun accesso al piano di gestione necessarie per questa applicazione. E, viceversa, se si desidera toobe un utente in grado di tooread insieme di credenziali delle proprietà e i tag, ma non sono presenti tookeys di accesso, i segreti o i certificati, è possibile concedere a questo utente, è necessario l'accesso a 'read' utilizzando RBAC e alcun piano toodata di accesso.

## <a name="management-plane-access-control"></a>Controllo di accesso al piano di gestione
il piano di gestione di Hello è costituito da operazioni che influiscono sulle hello insieme di credenziali chiave stessa. È ad esempio possibile creare o eliminare un insieme di credenziali, ottenere l'elenco degli insiemi di credenziali di una sottoscrizione, È possibile recuperare le proprietà di chiave dell'insieme di credenziali (ad esempio SKU, tag) e impostare i criteri di accesso che consentono di controllare gli utenti di hello e le applicazioni che possono accedere alle chiavi e segreti nell'insieme di credenziali chiave di hello insieme di credenziali chiave. Il controllo di accesso al piano di gestione è basato sul controllo degli accessi in base al ruolo. Vedere l'elenco completo di hello delle operazioni di insieme di credenziali chiave che possono essere eseguite tramite il piano di gestione nella tabella hello nella precedente sezione. 

### <a name="role-based-access-control-rbac"></a>Controllo degli accessi in base al ruolo
Ogni sottoscrizione di Azure è associata a un'istanza di Azure Active Directory. Gli utenti, gruppi e applicazioni da questa directory possono essere concesse le risorse di toomanage accesso hello sottoscrizione di Azure che utilizzano modelli di distribuzione Azure Resource Manager hello. Questo tipo di controllo di accesso è tooas denominata controllo di accesso basato sui ruoli (RBAC). toomanage accedere a questo, è possibile utilizzare hello [portale di Azure](https://portal.azure.com/), hello [strumenti di Azure CLI](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), o hello [API REST di gestione risorse di Azure](https://msdn.microsoft.com/library/azure/dn906885.aspx).

Con il modello di gestione risorse di Azure hello, creare credenziali delle chiavi in una risorsa gruppo e controllo accesso toohello piano di gestione di questo insieme di credenziali chiave usando Azure Active Directory. Ad esempio, è possibile concedere agli utenti o un gruppo possibilità toomanage chiave insiemi di credenziali in un gruppo di risorse specifico.

È possibile concedere accesso toousers, gruppi e applicazioni in un ambito specifico mediante l'assegnazione di ruoli RBAC appropriati. Ad esempio, toogrant accedere tooa utente toomanage chiave gli insiemi di credenziali, è necessario assegnare un ruolo predefinito 'insieme di credenziali chiave collaboratore' toothis utente a un ambito specifico. ambito Hello in questo caso sarebbe una sottoscrizione, un gruppo di risorse o solo una specifica chiave dell'insieme di credenziali. Un ruolo a livello di sottoscrizione si applica a gruppi di risorse tooall e risorse all'interno di tale sottoscrizione. Un ruolo a livello di gruppo di risorse applicata tooall risorse in tale gruppo di risorse. Un ruolo assegnato per una risorsa specifica solo toothat risorse. Sono disponibili diversi ruoli predefiniti (vedere [RBAC: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md)), e se hello i ruoli predefiniti non si adattano alle esigenze, è inoltre possibile definire i propri ruoli.

> [!IMPORTANT]
> Si noti che se un utente dispone di piano di gestione dell'insieme di credenziali chiave tooa collaboratore autorizzazioni (RBAC), può concedere stesso piano toodata di accesso, mediante l'impostazione di criteri di accesso dell'insieme di credenziali chiave, che controlla il piano di toodata accesso. Pertanto, è consigliabile controllare tootightly chi ha 'Collaboratore' accesso tooyour gli insiemi di credenziali chiave tooensure solo gli utenti autorizzati possono accedere e gestire gli insiemi di credenziali chiave, le chiavi, i segreti e certificati.
> 
> 

## <a name="data-plane-access-control"></a>Controllo di accesso al piano dati
piano dati insieme di credenziali chiave di Hello è costituita da operazioni che influiscono sugli oggetti hello in un insieme di credenziali, ad esempio le chiavi, i segreti e certificati.  Sono incluse le operazioni relative alle chiavi, come la creazione, l'importazione, l'aggiornamento, la generazione di un elenco, il backup e il ripristino, le operazioni di crittografia, come la firma, la verifica, la crittografia, la decrittografia, l'esecuzione e la rimozione del wrapping, nonché l'impostazione di tag e altri attributi per le chiavi. Analogamente, per i segreti sono incluse le operazioni per ottenere, impostare, elencare ed eliminare i segreti.

L'accesso al piano dati viene concesso impostando criteri di accesso per un insieme di credenziali delle chiavi. Un utente, gruppo o un'applicazione deve disporre delle autorizzazioni di collaboratore (RBAC) per il piano di gestione per un insieme di credenziali chiave toobe in grado di tooset i criteri di accesso per tale chiave dell'insieme di credenziali. Un utente, gruppo o l'applicazione è possibile concedere accesso tooperform specifico di operazioni per le chiavi o i segreti in un insieme di credenziali chiave. Supporto di insieme di credenziali delle chiavi le voci di criteri di accesso too16 per un insieme di credenziali chiave. Creare un gruppo di sicurezza di Azure Active Directory e aggiungere gli utenti toothat gruppo toogrant dati piano accesso tooseveral utenti tooa chiave dell'insieme di credenziali.

### <a name="key-vault-access-policies"></a>Criteri di accesso di Key Vault
I criteri di accesso dell'insieme di credenziali chiave concedono certificati, i segreti e le autorizzazioni tookeys separatamente. Ad esempio, è possibile assegnare tasti tooonly accesso utente, ma non le autorizzazioni per i segreti. Tuttavia, le chiavi tooaccess autorizzazioni o segreti o i certificati sono a livello di insieme di credenziali hello. In altre parole, i criteri di accesso dell'insieme di credenziali delle chiavi non supportano le autorizzazioni a livello di oggetto. È possibile utilizzare [portale di Azure](https://portal.azure.com/), hello [strumenti di Azure CLI](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), o hello [API REST di gestione dell'insieme di credenziali chiave](https://msdn.microsoft.com/library/azure/mt620024.aspx) tooset i criteri di accesso per un insieme di credenziali chiave.

> [!IMPORTANT]
> Si noti che i criteri di accesso dell'insieme di credenziali chiave si applicano a livello di insieme di credenziali hello. Ad esempio, quando un utente viene concesso chiavi toocreate e delete di autorizzazione, lei può eseguire le operazioni in tutte le chiavi in tale insieme di credenziali chiave.
> 
> 

## <a name="example"></a>Esempio
Si supponga di voler sviluppare un'applicazione che usa un certificato per SSL, il servizio Archiviazione di Azure per archiviare i dati e una chiave RSA a 2048 bit per le operazioni di firma. Si supponga inoltre che tale applicazione venga eseguita in una macchina virtuale (o in un set di scalabilità di macchine virtuali). È possibile utilizzare un insieme di credenziali chiave di toostore che tutti hello segreti dell'applicazione e usare insieme di credenziali chiave toostore hello bootstrap certificato utilizzato da tooauthenticate applicazione hello con Azure Active Directory.

In tal caso, ecco un riepilogo di tutti i hello chiavi e segreti toobe archiviati in un insieme di credenziali chiave.

* **Certificato SSL**: usato per SSL.
* **Chiave di archiviazione** -utilizzato tooget accesso tooStorage account
* **Chiave RSA a 2048 bit**: usata per le operazioni di firma.
* **Certificato bootstrap** -usare tooauthenticate tooAzure Active Directory, tooget tookey insieme di credenziali toofetch hello archiviazione tasto di scelta e la chiave RSA hello di utilizzo per la firma.

Ora si soddisfano persone hello che la gestione, distribuzione e il controllo di questa applicazione. In questo esempio verranno usati tre ruoli.

* **Il team di sicurezza** : si tratta in genere il personale IT da hello 'ufficio di hello compagnia (amministratore responsabile della sicurezza)' o equivalente, responsabile hello custodia corretta dei segreti, ad esempio i certificati SSL, utilizzate per la firma, stringhe di connessione per le chiavi RSA database, chiavi dell'account di archiviazione.
* **Gli sviluppatori/operatori** -si tratta di persone hello sviluppano l'applicazione e quindi distribuirla in Azure. In genere, non fanno parte del team di sicurezza, hello e pertanto non dovrebbe avere accesso tooany a dati riservati, ad esempio i certificati SSL, le chiavi RSA, ma la distribuzione di un'applicazione hello deve avere accesso toothose.
* **I revisori** -si tratta in genere un set diverso di persone, isolate da sviluppatori hello e generale del personale IT. Le relative responsabilità legate è tooreview corretto utilizzo e la manutenzione di certificati, chiavi, e così via e garantire la conformità agli standard di protezione dati. 

Un ruolo più ambito hello all'esterno di questa applicazione, ma pertinente toobe qui indicato e che sarebbe sottoscrizione hello (o gruppo di risorse) amministratore. Imposta le autorizzazioni di accesso iniziale per il team di sicurezza hello amministratore della sottoscrizione. Di seguito si presuppone che amministratore della sottoscrizione hello ha concesso l'accesso toohello team tooa risorsa gruppo di sicurezza in cui tutti hello risorse necessarie per risiedono questa applicazione.

Ora esaminare le azioni di ogni ruolo vengono eseguite nel contesto di hello di questa applicazione.

* **Team responsabile della sicurezza**
  * Creare insiemi di credenziali delle chiavi
  * Attivare la registrazione degli insiemi di credenziali delle chiavi
  * Aggiungere chiavi o segreti
  * Creare una copia di backup delle chiavi per il ripristino di emergenza
  * Impostare l'accesso di insieme di credenziali chiave toogrant autorizzazioni toousers e applicazioni tooperform specifiche operazioni di criteri
  * Distribuire periodicamente chiavi o segreti
* **Sviluppatori/operatori**
  * Ottenere i riferimenti toobootstrap e certificati SSL (le identificazioni personali), la chiave di archiviazione (segreto URI) e chiave (chiave URI) dal team di sicurezza per la firma
  * Sviluppare e distribuire l'applicazione che accede a chiavi e segreti a livello di codice
* **Revisori**
  * Esaminare i log dell'utilizzo tooconfirm corretto utilizzo/chiave privata e conformità agli standard di protezione dati

Ora esaminare quali credenziali tookey le autorizzazioni di accesso necessarie per ogni ruolo (e l'applicazione hello) tooperform alle attività assegnate. 

| Ruolo utente | Autorizzazioni del piano di gestione | Autorizzazioni del piano dati |
| --- | --- | --- |
| Team responsabile della sicurezza |key vault Contributor |Chiavi: backup, create, delete, get, import, list, restore <br> Segreti: all |
| Sviluppatori/operatori |insieme di credenziali chiave distribuire autorizzazione in modo che la distribuzione di macchine virtuali di hello possono recuperare i segreti dall'insieme di credenziali chiave hello |Nessuno |
| Revisori |Nessuna |Chiavi: list<br>Segreti: list |
| Applicazione |Nessuna |Chiavi: sign<br>Segreti: get |

> [!NOTE]
> I revisori necessitano dell'autorizzazione di elenco per le chiavi e segreti in modo è possibile controllare gli attributi per le chiavi e segreti non vengono generati nei registri di hello, ad esempio di tag, attivazione e di scadenza.
> 
> 

Oltre all'insieme di credenziali di autorizzazione tookey, tutti i tre ruoli anche necessitano accedere tooother alle risorse. Ad esempio, toobe in grado di toodeploy macchine virtuali (o Web App ecc.) Gli sviluppatori/operatori è necessario anche tipi di risorse toothose 'Collaboratore' accesso. I revisori necessario account di accesso in lettura toohello archiviazione in cui sono archiviati i log dell'insieme di credenziali chiave hello.

Poiché lo stato attivo hello di questo articolo riguarda la protezione dei insieme di credenziali chiave di accesso tooyour, è solo illustrare parti pertinenti di hello relativo argomento toothis e ignorare i dettagli relativi alla distribuzione di certificati, l'accesso alle chiavi e segreti a livello di codice e così via. che sono trattati in altri documenti. Distribuzione dei certificati archiviati nell'insieme di credenziali chiave tooVMs viene descritta in un [post di blog](https://blogs.technet.microsoft.com/kv/2016/09/14/updated-deploy-certificates-to-vms-from-customer-managed-key-vault/)ed è [codice di esempio](https://www.microsoft.com/download/details.aspx?id=45343) disponibile che illustra come toouse bootstrap certificato tooauthenticate tooAzure AD tooget insieme di credenziali di accesso tookey.

La maggior parte delle autorizzazioni di accesso hello possono essere concesse tramite il portale di Azure, ma toogrant autorizzazioni granulari hello di tooachieve toouse Azure PowerShell (o CLI di Azure) è il risultato desiderato. 

Si supponga di Hello seguenti frammenti di codice PowerShell:

* amministratore di Azure Active Directory di Hello ha creato i gruppi di sicurezza che rappresentano hello tre ruoli, vale a dire Team di protezione di Contoso, Contoso App Devops, Contoso App Auditors. i gruppi di utenti toohello che appartengono anche aggiunte Hello amministratore.
* **ContosoAppRG** gruppo di risorse hello in cui si trova tutte le risorse di hello. **contosologstorage** vengono memorizzati i registri di hello. 
* Insieme di credenziali chiave **ContosoKeyVault** e account di archiviazione usato per i log dell'insieme di credenziali chiave **contosologstorage** hello deve essere nello stesso percorso di Azure

Amministratore della sottoscrizione prima hello assegna 'della chiave dell'insieme di credenziali collaboratore' e ' utente amministratore di accesso ' ruoli toohello sicurezza team. In questo modo le risorse del tooother accesso toomanage team sicurezza hello e gestire insiemi di credenziali chiave nel gruppo di risorse hello ContosoAppRG.

```
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "key vault Contributor" -ResourceGroupName ContosoAppRG
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "User Access Administrator" -ResourceGroupName ContosoAppRG
```

Hello script riportato di seguito viene illustrato come team addetto alla sicurezza hello può creare un insieme di credenziali chiave, la registrazione del programma di installazione e impostare le autorizzazioni di accesso per altri ruoli e l'applicazione hello. 

```
# Create key vault and enable logging
$sa = Get-AzureRmStorageAccount -ResourceGroup ContosoAppRG -Name contosologstorage
$kv = New-AzureRmKeyVault -VaultName ContosoKeyVault -ResourceGroup ContosoAppRG -SKU premium -Location 'westus' -EnabledForDeployment
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

# Data plane permissions for Security team
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -PermissionsToKeys backup,create,delete,get,import,list,restore -PermissionsToSecrets all

# Management plane permissions for Dev/ops
# Create a new role from an existing role
$devopsrole = Get-AzureRmRoleDefinition -Name "Virtual Machine Contributor"
$devopsrole.Id = $null
$devopsrole.Name = "Contoso App Devops"
$devopsrole.Description = "Can deploy VMs that need secrets from key vault"
$devopsrole.AssignableScopes = @("/subscriptions/<SUBSCRIPTION-GUID>")

# Add permission for dev/ops so they can deploy VMs that have secrets deployed from key vaults
$devopsrole.Actions.Add("Microsoft.KeyVault/vaults/deploy/action")
New-AzureRmRoleDefinition -Role $devopsrole

# Assign this newly defined role tooDev ops security group
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Devops')[0].Id -RoleDefinitionName "Contoso App Devops" -ResourceGroupName ContosoAppRG

# Data plane permissions for Auditors
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Auditors')[0].Id -PermissionsToKeys list -PermissionsToSecrets list
```

ruolo personalizzata Hello è definito, è solo toohello assegnabile sottoscrizione in cui viene creato gruppo di risorse ContosoAppRG hello. Se hello stessi ruoli personalizzati verranno utilizzati per altri progetti in altre sottoscrizioni, di ambito potrebbe avere altre sottoscrizioni aggiunte.

assegnazione di ruolo personalizzata Hello per gli sviluppatori hello gli operatori per l'autorizzazione "distribuire/azione" hello è il gruppo di risorse toohello con ambito. In questo modo solo le macchine virtuali hello creato nel gruppo di risorse hello 'ContosoAppRG' otterrà i segreti hello (certificato SSL e cert bootstrap). Tutte le macchine virtuali che consente di creare un membro del team di sviluppatori/operatori in un altro gruppo di risorse non saranno in grado di tooget questi segreti anche se erano segreto hello URI.

Questo esempio illustra uno scenario semplice. Scenari realistici potrebbero essere più complessi e potrebbe essere necessario tooadjust autorizzazioni tooyour chiave dell'insieme di credenziali in base alle proprie esigenze. Ad esempio, in questo esempio, si presuppone di che quel team sicurezza fornirà hello chiave e il segreto riferimenti (URI e le identificazioni personali) che tooreference necessità del team di sviluppatori/operatori nelle proprie applicazioni. Di conseguenza, non è necessario toogrant sviluppatori/operatori accesso piano dati. Si noti inoltre che questo esempio riguarda principalmente la sicurezza dell'insieme di credenziali delle chiavi. Simile considerazione toosecure [le macchine virtuali](https://azure.microsoft.com/services/virtual-machines/security/), [gli account di archiviazione](../storage/common/storage-security-guide.md) e altre risorse di Azure troppo.

> [!NOTE]
> Nota: questo esempio mostra come l'accesso all'insieme di credenziali delle chiavi verrà bloccato nell'ambiente di produzione. gli sviluppatori di Hello dovrebbero avere il proprio gruppo di risorse o la sottoscrizione in cui hanno le autorizzazioni complete toomanage loro insiemi di credenziali, le macchine virtuali e account di archiviazione in cui lo sviluppo di un'applicazione hello.
> 
> 

## <a name="resources"></a>Risorse
* [Controllo degli accessi in base al ruolo di Azure Active Directory](../active-directory/role-based-access-control-configure.md)
  
  Questo articolo spiega hello controllo di accesso basato sui ruoli di Azure Active Directory e il relativo funzionamento.
* [Controllo degli accessi in base al ruolo: Ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md)
  
  I dettagli di questo articolo tutti hello ruoli predefiniti disponibili in RBAC.
* [Comprendere la distribuzione di Gestione delle risorse e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md)
  
  In questo articolo illustra la distribuzione di gestione risorse di hello e modelli di distribuzione classica e spiega hello vantaggi dell'utilizzo di gruppi di gestione risorse e risorse hello
* [Gestire il controllo degli accessi in base al ruolo con Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  
  Questo articolo viene illustrato come toomanage basata su ruoli controllo di accesso con Azure PowerShell
* [Controllo degli accessi basato sui ruoli con hello API REST di gestione](../active-directory/role-based-access-control-manage-access-rest.md)
  
  Questo articolo illustra come toouse hello toomanage API REST sui ruoli.
* [Controllo degli accessi in base al ruolo per Microsoft Azure da Ignite](https://channel9.msdn.com/events/Ignite/2015/BRK2707)
  
  Si tratta di un video su Channel 9 conferenza Ignite 2015 MS hello tooa di collegamento. In questa sessione, si parla di accedere alle funzionalità di reporting in Azure e gestione e l'esplorazione di procedure consigliate per la protezione dell'accesso tooAzure sottoscrizioni tramite Azure Active Directory.
* [Autorizzare l'accesso tooweb applicazioni tramite OAuth 2.0 e Azure Active Directory](../active-directory/active-directory-protocols-oauth-code.md)
  
  Questo articolo descrive l'intero flusso di OAuth 2.0 per l'autenticazione con Azure Active Directory.
* [key vault Management REST APIs](https://msdn.microsoft.com/library/azure/mt620024.aspx) (API REST di gestione dell'insieme di credenziali delle chiavi)
  
  Questo documento è riferimento hello per hello API REST toomanage la chiave dell'insieme di credenziali a livello di codice, inclusa l'impostazione di criteri di accesso dell'insieme di credenziali chiave.
* [key vault REST APIs](https://msdn.microsoft.com/library/azure/dn903609.aspx) (API REST dell'insieme di credenziali delle chiavi)
  
  Insieme di credenziali tookey collegamento documentazione di riferimento API REST.
* [Key access control](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_KeyAccessControl) (Controllo di accesso per le chiavi)
  
  Documentazione di riferimento controllo accesso tooSecret collegamento.
* [Secret access control](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_SecretAccessControl) (Controllo di accesso per i segreti)
  
  Documentazione di riferimento controllo accesso tooKey collegamento.
* [Impostare](https://msdn.microsoft.com/library/mt603625.aspx) e [rimuovere](https://msdn.microsoft.com/library/mt619427.aspx) i criteri di accesso dell'insieme di credenziali delle chiavi usando PowerShell
  
  Documentazione di tooreference collegamenti per criteri di accesso dell'insieme di credenziali chiave toomanage cmdlet PowerShell.

## <a name="next-steps"></a>Passaggi successivi
Per un'esercitazione introduttiva per gli amministratori, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](key-vault-get-started.md).

Per altre informazioni sulla registrazione dell'utilizzo per l'insieme di credenziali delle chiavi, vedere [Registrazione dell'insieme di credenziali delle chiavi di Azure](key-vault-logging.md).

Per altre informazioni sull'uso di chiavi e segreti con l'insieme di credenziali delle chiavi di Azure, vedere [About Keys and Secrets](https://msdn.microsoft.com/library/azure/dn903623.aspx) (Informazioni su chiavi e segreti).

In caso di domande sull'insieme di credenziali chiave, visitare hello [insieme di credenziali chiave Azure forum](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault)

