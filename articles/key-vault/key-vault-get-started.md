---
title: aaaGet avviato con l'insieme di credenziali chiave di Azure | Documenti Microsoft
description: Utilizzare questa esercitazione toohelp si ottiene avviato con insieme credenziali chiavi Azure toocreate un contenitore di protezione avanzato in Azure, toostore e gestire chiavi di crittografia e i segreti in Azure.
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 36721e1d-38b8-4a15-ba6f-14ed5be4de79
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 865853b778dec5fca5c7db0d060627554c0a9cb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-key-vault"></a>Introduzione all'insieme di credenziali delle chiavi di Azure
L'insieme di credenziali delle chiavi di Azure è disponibile nella maggior parte delle aree. Per ulteriori informazioni, vedere hello [insieme di credenziali chiave pagina dei prezzi](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introduzione
Utilizzare questa esercitazione toohelp si ottiene avviato con insieme credenziali chiavi Azure toocreate un contenitore di protezione avanzato (un insieme di credenziali) in Azure, toostore e gestire chiavi di crittografia e i segreti in Azure. Illustra hello processo dell'utilizzo di Azure PowerShell toocreate un insieme di credenziali che contiene una chiave o una password che è quindi possibile utilizzare con un'applicazione Azure. L'esercitazione spiega poi come un'applicazione può usare questa chiave o password.

**Toocomplete tempo stimato:** 20 minuti

> [!NOTE]
> In questa esercitazione sono incluse istruzioni per la modalità toowrite hello applicazione Azure che include uno dei passaggi di hello, vale a dire come tooauthorize un toouse applicazione una chiave o la chiave privata della chiave hello insieme di credenziali.
>
> Questa esercitazione usa Azure PowerShell. Per le istruzioni relative all'interfaccia della riga di comando multipiattaforma, vedere [questa esercitazione equivalente](key-vault-manage-with-cli2.md).
>
>

Per informazioni generali sull'insieme di credenziali di Azure, vedere [Cos'è l'insieme di credenziali chiave di Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa esercitazione, è necessario disporre di hello seguenti:

* TooMicrosoft una sottoscrizione Azure. Se non si ha una sottoscrizione, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).
* Azure PowerShell **versione minima 1.1.0**. tooinstall Azure PowerShell e associarlo a una sottoscrizione di Azure, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview). Se già stato installato Azure PowerShell e non conosce la versione di hello, dalla console di hello Azure PowerShell, digitare `(Get-Module azure -ListAvailable).Version`. Se sono installate le versioni di Azure PowerShell dalla 0.9.1 alla 0.9.8, è comunque possibile svolgere questa esercitazione, con alcune piccole modifiche. Ad esempio, è necessario utilizzare hello `Switch-AzureMode AzureResourceManager` comando e alcuni dei comandi di hello insieme credenziali chiavi Azure sono stati modificati. Per un elenco di cmdlet di insieme di credenziali chiave per le versioni 0.9.1 tramite 0.9.8 hello, vedere [cmdlet insieme di credenziali delle chiavi di Azure](/powershell/module/azurerm.keyvault/#key_vault).
* Un'applicazione che verrà configurato toouse hello chiave o password creati in questa esercitazione. Un'applicazione di esempio è disponibile da hello [Microsoft Download Center](http://www.microsoft.com/en-us/download/details.aspx?id=45343). Per istruzioni, vedere il file Leggimi di accompagnamento hello.

Questa esercitazione è progettata per i principianti di Azure PowerShell, ma presuppone la conoscenza dei concetti di base hello, ad esempio le sessioni, cmdlet e i moduli. Per altre informazioni, vedere [Introduzione a Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx).

tooget informazioni dettagliate della Guida per tutti i cmdlet che viene visualizzato in questa esercitazione, usare hello **Get-Help** cmdlet.

    Get-Help <cmdlet-name> -Detailed

Ad esempio, la Guida di tooget per hello **accesso AzureRmAccount** cmdlet, digitare:

    Get-Help Login-AzureRmAccount -Detailed

È inoltre possibile leggere hello seguenti esercitazioni tooget familiarità con Azure Resource Manager in Azure PowerShell:

* [Come tooinstall e configurare Azure PowerShell](/powershell/azure/overview)
* [Utilizzo di Azure PowerShell con Gestione risorse](../powershell-azure-resource-manager.md)

## <a id="connect"></a>Connettersi tooyour sottoscrizioni
Avviare una sessione di Azure PowerShell e accedere con il comando seguente hello tooyour account Azure:  

    Login-AzureRmAccount

Si noti che se si utilizza un'istanza specifica di Azure, ad esempio, Azure per enti pubblici, utilizzare hello - parametro ambiente con questo comando. Ad esempio: `Login-AzureRmAccount –Environment (Get-AzureRmEnvironment –Name AzureUSGovernment)`

Nella finestra popup del browser hello, immettere il nome utente dell'account Azure e la password. Azure PowerShell recupera tutte le sottoscrizioni di hello che sono associate a questo account e per impostazione predefinita, utilizza hello prima.

Se si dispone di più sottoscrizioni e si desidera toospecify un uno toouse specifico per l'insieme di credenziali chiave di Azure, digitare hello sottoscrizioni hello toosee per l'account di seguito:

    Get-AzureRmSubscription

Quindi, toospecify hello sottoscrizione toouse, tipo:

    Set-AzureRmContext -SubscriptionId <subscription ID>

Per ulteriori informazioni sulla configurazione di Azure PowerShell, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

## <a id="resource"></a>Creare un nuovo gruppo di risorse
Quando si usa Gestione risorse di Azure, tutte le risorse correlate vengono create in un gruppo di risorse. Per questa esercitazione verrà creato un nuovo gruppo di risorse denominato **ContosoResourceGroup** :

    New-AzureRmResourceGroup –Name 'ContosoResourceGroup' –Location 'East Asia'


## <a id="vault"></a>Creare un insieme di credenziali chiave
Hello utilizzare [New AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) toocreate cmdlet un insieme di credenziali chiave. Questo cmdlet ha tre parametri obbligatori: un **nome gruppo di risorse**, **nome insieme di credenziali chiave**, hello e **posizione geografica**.

Ad esempio, se si utilizza il nome dell'insieme di credenziali hello di **ContosoKeyVault**, nome del gruppo di risorse hello **ContosoResourceGroup**e il percorso di hello del **Asia orientale**, tipo:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

output di Hello di questo cmdlet Mostra le proprietà dell'insieme di credenziali chiave hello appena creato. proprietà di Hello due più importanti sono:

* **Nome dell'insieme di credenziali**: nell'esempio hello, si tratta di **ContosoKeyVault**. Questo nome verrà usato per altri cmdlet di insieme di credenziali delle chiavi.
* **URI dell'insieme di credenziali**: nell'esempio hello, si tratta di https://contosokeyvault.vault.azure.net/. Le applicazioni che usano l'insieme di credenziali tramite l'API REST devono usare questo URI.

L'account di Azure è ora autorizzato tooperform insieme di credenziali di qualsiasi operazione su questa chiave. Nessun altro lo è ancora.

> [!NOTE]
> Se viene visualizzato l'errore hello **sottoscrizione hello non è registrato toouse dello spazio dei nomi 'Microsoft.KeyVault'** quando si tenta toocreate il nuovo insieme di credenziali chiave, eseguire `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"` e quindi eseguire nuovamente il comando New-AzureRmKeyVault. Per altre informazioni, vedere [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider).
>
>

## <a id="add"></a>Aggiungere una chiave o un insieme di credenziali chiave segreta toohello
Se si desidera toocreate insieme credenziali chiavi Azure una chiave protetta tramite software per l'utente, utilizzare hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) cmdlet e digitare hello seguente:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -Destination 'Software'

Tuttavia, se si dispone di una chiave protetta tramite software esistente una. PFX salvato tooyour C:\ unità in un file denominato che si desidera tooupload tooAzure insieme di credenziali chiave hello tipo segue variabile hello tooset softkey.pfx **securepfxpwd** per una password di **123** per hello. File PFX:

    $securepfxpwd = ConvertTo-SecureString –String '123' –AsPlainText –Force

Digitare quindi hello seguenti chiave hello tooimport dagli hello. File PFX, che protegge hello chiave tramite software nel servizio insieme di credenziali chiave hello:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd


È ora possibile fare riferimento a questa chiave che è stato creato o caricato tooAzure insieme di credenziali chiave utilizzando il relativo URI. Utilizzare **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways ottenere la versione corrente di hello e usare **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget tale versione.  

toodisplay hello URI per questa chiave, tipo:

    $Key.key.kid

tooadd un insieme di credenziali toohello secret ha valore hello Pa$ $w0rd tooAzure insieme di credenziali chiave e una password denominata SQLPassword, convertire il valore di hello della stringa protetta di Pa$ $w0rd tooa innanzitutto digitando hello riportato di seguito:

    $secretvalue = ConvertTo-SecureString 'Pa$$w0rd' -AsPlainText -Force

Quindi, digitare quanto segue di hello:

    $secret = Set-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword' -SecretValue $secretvalue

È ora possibile fare riferimento a questa password che sono state aggiunte tooAzure insieme di credenziali chiave, tramite il relativo URI. Utilizzare **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways ottenere la versione corrente di hello e usare **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget tale versione.

toodisplay hello URI per il segreto, tipo:

    $secret.Id

Si considerino hello chiave o il segreto appena creato:

* tooview il tipo di chiave,:`Get-AzureKeyVaultKey –VaultName 'ContosoKeyVault'`
* tooview segreto, tipo:`Get-AzureKeyVaultSecret –VaultName 'ContosoKeyVault'`

A questo punto, l'insieme di credenziali chiave e chiave o il segreto è pronto per applicazioni toouse. È necessario autorizzare toouse applicazioni li.  

## <a id="register"></a>Registrare un'applicazione con Azure Active Directory
Questo passaggio di solito viene eseguito da uno sviluppatore, su un computer separato. Non è tooAzure specifico insieme di credenziali chiave, ma è incluso di seguito per motivi di completezza.

> [!IMPORTANT]
> esercitazione hello toocomplete, l'account, insieme di credenziali hello e un'applicazione hello che verrà registrato in questo passaggio deve essere in hello stessa directory di Azure.
>
>

Le applicazioni che usano un insieme di credenziali delle chiavi devono eseguire l'autenticazione con un token di Azure Active Directory. toodo, hello proprietario di un'applicazione hello deve innanzitutto registrare l'applicazione hello in Azure Active Directory. Alla fine di hello della registrazione, proprietario dell'applicazione hello Ottiene hello seguenti valori:

* Un **ID applicazione** (noto anche come un ID Client) e **chiave di autenticazione** (noto anche come hello segreto condiviso). un'applicazione Hello deve presentare un token di entrambi questi valori tooAzure Active Directory, tooget. Come un'applicazione hello viene configurato toodo che ciò dipende dall'applicazione hello. Per l'applicazione di esempio insieme di credenziali chiave hello, proprietario dell'applicazione hello imposta questi valori nel file app. config hello.

applicazione hello tooregister in Azure Active Directory:

1. Accedi toohello portale di Azure classico.
2. A sinistra di hello, fare clic su **Active Directory**, quindi selezionare hello directory in cui è necessario registrare l'applicazione. <br> <br> **Nota:** è necessario selezionare hello stessa directory che contiene hello sottoscrizione di Azure con cui è stato creato l'insieme di credenziali chiave. Non si conosce la directory in questo caso, fare clic su **impostazioni**, identificare hello sottoscrizione con cui è stato creato l'insieme di credenziali chiave e il nome di hello nota della directory hello visualizzato nell'ultima colonna hello.
3. Fare clic su **APPLICAZIONI**. Se nessuna App è stati aggiunti tooyour directory, questa pagina vengono visualizzati solo hello **aggiungere un'App** collegamento. In alternativa, è possibile fare clic o fare clic sul collegamento hello **aggiungere** hello barra dei comandi.
4. In hello **Aggiungi applicazione** procedura guidata hello **cosa si desidera toodo?** pagina, fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.
5. In hello **informazioni sull'applicazione** pagina, specificare un nome per l'applicazione e quindi selezionare **applicazione WEB, e/o API WEB** (hello predefinito). Fare clic su hello **Avanti** icona.
6. In hello **proprietà App** specificare hello **URL accesso** e **URI ID APP** per l'applicazione web. Se l'applicazione non ha questi valori, è possibile crearli per questo passaggio (ad esempio, è possibile specificare http://test1.contoso.com per entrambe le caselle). Non è importante se questi siti esistono. Aspetto importante è che URI ID app hello per ogni applicazione è diverso per ogni applicazione nella directory. directory Hello usato tooidentify questa stringa l'app.
7. Fare clic su hello **completa** icona toosave le modifiche apportate nella procedura guidata hello.
8. In hello **avvio rapido** pagina, fare clic su **configura**.
9. Scorrere toohello **chiavi** sezione, selezionare la durata hello e quindi fare clic su **salvare**. pagina Hello viene aggiornato e verrà visualizzato un valore di chiave. È necessario configurare l'applicazione con questo valore di chiave e hello **ID CLIENT** valore. Le istruzioni per questa configurazione sono specifiche dell'applicazione.
10. Copiare valore dell'ID di hello client dalla pagina, che verrà utilizzato in hello successivo passaggio tooset le autorizzazioni per l'insieme di credenziali.

## <a id="authorize"></a>Autorizzare hello applicazione toouse hello chiave o il segreto
tooauthorize hello applicazione tooaccess hello chiave o al segreto nell'insieme di credenziali hello, utilizzare il [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.

Ad esempio, se il nome dell'insieme di credenziali è **ContosoKeyVault** e si desidera tooauthorize ha un ID client 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed e si vuole tooauthorize hello applicazione toodecrypt e accedere con le chiavi in un'applicazione hello insieme di credenziali, eseguire hello seguente:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

Se si desiderano che stessi segreti tooread applicazione tooauthorize nell'insieme di credenziali, eseguire hello:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get

## <a id="HSM"></a>Se si desidera toouse un modulo di protezione hardware (HSM)
Per maggiore sicurezza, è possibile importare o generare chiavi in moduli di protezione hardware (HSM) che non lasciano mai il limite HSM hello. Hello i moduli HSM sono FIPS 140-2 livello 2 convalidato. Se questo requisito non si applica a tooyou, ignorare questa sezione e passare troppo[Elimina insieme di credenziali chiave hello e le chiavi associate e i segreti](#delete).

toocreate queste chiavi HSM protette, è necessario utilizzare hello [chiavi HSM protette toosupport di livello di servizio dell'insieme di credenziali chiave di Azure Premium](https://azure.microsoft.com/pricing/free-trial/). Si noti anche che questa funzionalità non è disponibile nella versione Azure per la Cina.

Quando si crea l'insieme di credenziali chiave di hello, aggiungere hello **- SKU** parametro:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVaultHSM' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -SKU 'Premium'



È possibile aggiungere le chiavi protette tramite software (come illustrato in precedenza) e l'insieme di credenziali chiave toothis chiavi HSM protette. toocreate una chiave HSM protetta, hello set **-destinazione** too'HSM parametro ':

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -Destination 'HSM'

È possibile utilizzare una chiave da hello successivo comando tooimport una. File PFX nel computer in uso. Questo comando consente di importare chiave hello in hello servizio insieme di credenziali chiave HSM:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd -Destination 'HSM'


comando successivo Hello Importa un "bring your own key" pacchetto (BYOK). Questo scenario consente di generare la chiave nel modulo di protezione hardware locale e trasferirlo nel servizio insieme di credenziali chiave, hello tooHSMs senza chiave hello lasciando limite HSM hello:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\ITByok.byok' -Destination 'HSM'

Per ulteriori istruzioni su come toogenerate il pacchetto BYOK, vedere [come toogenerate e trasferire chiavi HSM protette per insieme credenziali chiavi Azure](key-vault-hsm-protected-keys.md).

## <a id="delete"></a>Eliminare l'insieme di credenziali chiave hello e le chiavi associate e i segreti
Se non è più necessario insieme di credenziali chiave hello e hello chiave o il segreto in esso contenuti, è possibile eliminare l'insieme di credenziali chiave hello utilizzando hello [Remove AzureRmKeyVault](/powershell/module/azurerm.keyvault/remove-azurermkeyvault) cmdlet:

    Remove-AzureRmKeyVault -VaultName 'ContosoKeyVault'

In alternativa, è possibile eliminare un gruppo di risorse di Azure intero, che include l'insieme di credenziali chiave di hello e altre risorse che incluso in tale gruppo:

    Remove-AzureRmResourceGroup -ResourceGroupName 'ContosoResourceGroup'


## <a id="other"></a>Altri cmdlet di Azure PowerShell
Altri comandi che potrebbero essere utili per la gestione dell'insieme di credenziali delle chiavi di Azure:

* `$Keys = Get-AzureKeyVaultKey -VaultName 'ContosoKeyVault'`: questo comando ottiene una visualizzazione tabulare di tutte le chiavi e le proprietà selezionate.
* `$Keys[0]`: Questo comando Visualizza un elenco completo delle proprietà per la chiave specificata hello
* `Get-AzureKeyVaultSecret`: questo comando elenca in una visualizzazione tabulare tutti i nomi di segreto e le proprietà selezionate.
* `Remove-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey'`: Esempio come tooremove una chiave specifica.
* `Remove-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword'`: Esempio come tooremove un segreto specifico.

## <a id="next"></a>Passaggi successivi
Per un'esercitazione successiva sull'uso dell'insieme di credenziali delle chiavi di Azure in un'applicazione Web, vedere [Usare l'insieme di credenziali delle chiavi di Azure da un'applicazione Web](key-vault-use-from-web-application.md).

toosee come viene utilizzato l'insieme di credenziali chiave, vedere [la registrazione dell'insieme di credenziali chiave di Azure](key-vault-logging.md).

Per un elenco dei cmdlet PowerShell di Azure più recenti di hello per insieme credenziali chiavi Azure, vedere [cmdlet insieme di credenziali delle chiavi di Azure](/powershell/module/azurerm.keyvault/#key_vault).

Per i riferimenti di programmazione, vedere [hello Guida per gli sviluppatori insieme credenziali chiavi Azure](key-vault-developers-guide.md).
