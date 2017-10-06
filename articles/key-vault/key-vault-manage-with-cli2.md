---
title: insieme di credenziali chiave di Azure usa CLI aaaManage | Documenti Microsoft
description: "Utilizzare questa attività comuni di esercitazione tooautomate nell'insieme di credenziali chiave usando hello CLI 2.0"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ambapat
ms.openlocfilehash: 76855c0ea09b6b307159468382a6a63627205556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli-20"></a>Gestire Key Vault tramite l'interfaccia della riga di comando 2.0
L'insieme di credenziali delle chiavi di Azure è disponibile nella maggior parte delle aree. Per ulteriori informazioni, vedere hello [insieme di credenziali chiave pagina dei prezzi](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introduzione
Utilizzare questa esercitazione toohelp si ottiene avviato con insieme credenziali chiavi Azure toocreate un contenitore di protezione avanzato (un insieme di credenziali) in Azure, toostore e gestire chiavi di crittografia e i segreti in Azure. Illustra hello processo di toocreate interfaccia della riga di comando multipiattaforma di Azure utilizzando un insieme di credenziali che contiene una chiave o una password che è quindi possibile utilizzare con un'applicazione Azure. L'esercitazione spiega poi come un'applicazione può usare questa chiave o password.

**Toocomplete tempo stimato:** 20 minuti

> [!NOTE]
> In questa esercitazione non include istruzioni su come toowrite hello applicazione Azure che uno dei passaggi di hello include, che mostra come tooauthorize un toouse applicazione una chiave o la chiave privata della chiave hello insieme di credenziali.
>
> Questa esercitazione viene utilizzato hello 2.0 CLI di Azure più recenti.
>
>

Per informazioni generali sull'insieme di credenziali di Azure, vedere [Cos'è l'insieme di credenziali chiave di Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa esercitazione, è necessario disporre di hello seguenti:

* TooMicrosoft una sottoscrizione Azure. Se non si dispone di una sottoscrizione, è possibile iscriversi per una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial).
* Interfaccia della riga di comando versione 2.0 o successiva. tooinstall hello versione più recente e connettersi tooyour sottoscrizione di Azure, vedere [installare e configurare l'interfaccia della riga di comando multipiattaforma di Azure 2.0 hello](/cli/azure/install-azure-cli).
* Un'applicazione che verrà configurato toouse hello chiave o password creati in questa esercitazione. Un'applicazione di esempio è disponibile da hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343). Per istruzioni, vedere il file Leggimi di accompagnamento hello.

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a>Risorse della Guida per l'interfaccia della riga di comando multipiattaforma di Microsoft Azure
In questa esercitazione si presuppone che si ha familiarità con l'interfaccia della riga di comando hello (Bash, Terminal, prompt dei comandi)

Hello - Guida o -h parametro può essere utilizzato tooview della Guida in linea per i comandi specifici. In alternativa, help hello azure [comando] [opzioni] formato può essere anche usato tooreturn hello stesse informazioni. Ad esempio, i comandi tutte restituito seguente hello hello stesse informazioni:

```
az account set --help
az account set -h
```

In caso di dubbi sui parametri hello necessari da un comando, fare riferimento tramite toohelp - help, -h o az help [comando].

È inoltre possibile leggere hello seguenti esercitazioni tooget familiarità con Gestione risorse di Azure nell'interfaccia della riga di comando multipiattaforma di Azure:

* [Installare l'interfaccia da riga di comando di Azure](/cli/azure/install-azure-cli)
* [Introduzione all'interfaccia della riga di comando di Azure 2.0](/cli/azure/get-started-with-azure-cli)

## <a name="connect-tooyour-subscriptions"></a>Connettersi tooyour sottoscrizioni
toolog con un account aziendale, utilizzare hello comando seguente:

```
az login -u username@domain.com -p password
```

o se si desidera toolog digitando in modo interattivo

```
az login
```

Se si dispone di più sottoscrizioni e si desidera toospecify un uno toouse specifico per l'insieme di credenziali chiave di Azure, digitare hello sottoscrizioni hello toosee per l'account di seguito:

```
az account list
```

Quindi, toospecify hello sottoscrizione toouse, tipo:

```
az account set --subscription <subscription name or ID>
```

Per ulteriori informazioni sulla configurazione dell'interfaccia della riga di comando multipiattaforma di Azure, vedere [Installare l'interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli).

## <a name="create-a-new-resource-group"></a>Creare un nuovo gruppo di risorse
Quando si usa Gestione risorse di Azure, tutte le risorse correlate vengono create in un gruppo di risorse. Per questa esercitazione si creerà un nuovo gruppo di risorse denominato 'ContosoResourceGroup'.

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

primo parametro Hello è il nome di gruppo di risorse e hello secondo parametro è il percorso di hello. Per il percorso, utilizzare il comando di hello `az account list-locations` tooidentify come toospecify toohello un percorso alternativo uno in questo esempio. Se servono altre informazioni, digitare: `az account list-locations -h`.

## <a name="register-hello-key-vault-resource-provider"></a>Registrazione provider di risorse hello insieme di credenziali chiave
Verificare che il provider di risorse dell'insieme di credenziali delle chiavi sia registrato nella sottoscrizione:

```
az provider register -n Microsoft.KeyVault
```

Questa operazione deve solo toobe eseguito una volta per ogni sottoscrizione.

## <a name="create-a-key-vault"></a>Creare un insieme di credenziali delle chiavi
Hello utilizzare `az keyvault create` comando toocreate un insieme di credenziali chiave. Questo script ha tre parametri obbligatori: il nome di un gruppo di risorse, un insieme di credenziali delle chiavi e la posizione geografica di hello.

Ad esempio, se si utilizza il nome dell'insieme di credenziali hello di ContosoKeyVault, nome gruppo di risorse hello di ContosoResourceGroup e il percorso di hello dell'Asia orientale, digitare:
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

output di Hello di questo comando Mostra le proprietà dell'insieme di credenziali chiave hello appena creato. proprietà di Hello due più importanti sono:

* **nome**: nell'esempio hello tratta ContosoKeyVault. Questo nome verrà usato per altri comandi di Key Vault.
* **vaultUri**: nell'esempio hello tratta https://contosokeyvault.vault.azure.net. Le applicazioni che usano l'insieme di credenziali tramite l'API REST devono usare questo URI.

L'account di Azure è ora autorizzato tooperform insieme di credenziali di qualsiasi operazione su questa chiave. Nessun altro lo è ancora.

## <a name="add-a-key-or-secret-toohello-key-vault"></a>Aggiungere una chiave o un insieme di credenziali chiave segreta toohello
Se si desidera toocreate insieme credenziali chiavi Azure una chiave protetta tramite software per l'utente, utilizzare hello `az key create` comandi e digitare il seguente hello:
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
Tuttavia, se si dispone di una chiave esistente in un file con estensione PEM salvato come file locale in un file denominato softkey.pem che si desidera tooupload tooAzure insieme di credenziali chiave, digitare hello seguenti chiave hello tooimport dagli hello. File con estensione PEM, che protegge hello chiave tramite software nel servizio insieme di credenziali chiave hello:
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
È ora possibile fare riferimento chiave hello creati o caricati tooAzure insieme di credenziali chiave utilizzando il relativo URI. Utilizzare **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways ottenere la versione corrente di hello e usare **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget tale versione.

tooadd un insieme di credenziali toohello segreto, che è una password denominata SQLPassword e con valore hello Pa$ $w0rd tooAzure insieme di credenziali chiave hello tipo seguente:
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
È ora possibile fare riferimento a questa password che sono state aggiunte tooAzure insieme di credenziali chiave, tramite il relativo URI. Utilizzare **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways ottenere la versione corrente di hello e usare **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget tale versione.

Si considerino hello chiave o il segreto appena creato:

* tooview il tipo di chiave,:`az keyvault key list --vault-name 'ContosoKeyVault'`
* tooview segreto, tipo:`az keyvault secret list --vault-name 'ContosoKeyVault'`

## <a name="register-an-application-with-azure-active-directory"></a>Registrare un'applicazione con Azure Active Directory
Questo passaggio di solito viene eseguito da uno sviluppatore, su un computer separato. Non è tooAzure specifico insieme di credenziali chiave ma è incluso in questo caso, per motivi di completezza.

> [!IMPORTANT]
> esercitazione hello toocomplete, l'account, insieme di credenziali hello e un'applicazione hello che verrà registrato in questo passaggio deve essere in hello stessa directory di Azure.
>
>

Le applicazioni che usano un insieme di credenziali delle chiavi devono eseguire l'autenticazione con un token di Azure Active Directory. toodo, hello proprietario di un'applicazione hello deve innanzitutto registrare l'applicazione hello in Azure Active Directory. Alla fine di hello della registrazione, proprietario dell'applicazione hello Ottiene hello seguenti valori:

* Un **ID applicazione** (noto anche come un ID Client) e **chiave di autenticazione** (noto anche come hello segreto condiviso). un'applicazione Hello deve presentare entrambi questi tooAzure valori tooget un token di Active Directory. Come un'applicazione hello viene configurato toodo che ciò dipende dall'applicazione hello. Per l'applicazione di esempio insieme di credenziali chiave hello, proprietario dell'applicazione hello imposta questi valori nel file app. config hello.

applicazione hello tooregister in Azure Active Directory:

1. Accedi toohello portale di Azure.
2. A sinistra di hello, fare clic su **Azure Active Directory**, quindi selezionare hello directory in cui è necessario registrare l'applicazione. <br> <br> 

> [!Note] 
> È necessario selezionare hello stessa directory che contiene hello sottoscrizione di Azure con cui è stato creato l'insieme di credenziali chiave. Non si conosce la directory in questo caso, fare clic su **impostazioni**, identificare hello sottoscrizione con cui è stato creato l'insieme di credenziali chiave e il nome di hello nota della directory hello visualizzato nell'ultima colonna hello.

3. Fare clic su **APPLICAZIONI**. Se nessuna App è stati aggiunti tooyour directory, questa pagina mostrerà solo hello **aggiungere un'App** collegamento. Fare clic sul collegamento hello o in alternativa, è possibile fare clic su hello **aggiungere** hello barra dei comandi.
4. In hello **Aggiungi applicazione** procedura guidata hello **cosa si desidera toodo?** pagina, fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.
5. In hello **informazioni sull'applicazione** pagina, specificare un nome per l'applicazione e selezionare **applicazione WEB, e/o API WEB** (hello predefinito). Fare clic sull'icona Avanti hello.
6. In hello **proprietà App** specificare hello **URL accesso** e **URI ID APP** per l'applicazione web. Se l'applicazione non ha questi valori, è possibile crearli per questo passaggio (ad esempio, è possibile specificare http://test1.contoso.com per entrambe le caselle). Non è importante se esistono di questi siti. aspetto importante è che URI ID app hello per ogni applicazione è diverso per ogni applicazione nella directory. directory Hello usato tooidentify questa stringa l'app.
7. Fare clic su hello icona completata toosave le modifiche apportate nella procedura guidata hello.
8. Nella pagina introduttiva hello, fare clic su **configura**.
9. Scorrere toohello **chiavi** sezione, selezionare la durata hello e quindi fare clic su **salvare**. pagina Hello viene aggiornato e verrà visualizzato un valore di chiave. È necessario configurare l'applicazione con questo valore di chiave e hello **ID CLIENT** valore. Le istruzioni per questa configurazione saranno specifiche dell'applicazione.
10. Copiare valore dell'ID di hello client dalla pagina, che verrà utilizzato in hello successivo passaggio tooset le autorizzazioni per l'insieme di credenziali.

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a>Autorizzare hello applicazione toouse hello chiave o il segreto
tooauthorize hello applicazione tooaccess hello chiave o al segreto nell'insieme di credenziali hello, utilizzare hello `az keyvault set-policy` comando.

Ad esempio, se il nome dell'insieme di credenziali è ContosoKeyVault e hello applicazione cui si desidera tooauthorize ha un ID client 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed e si desidera tooauthorize hello applicazione toodecrypt e accedere con le chiavi nell'insieme di credenziali, quindi eseguire hello seguenti:
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

Se si desiderano che stessi segreti tooread applicazione tooauthorize nell'insieme di credenziali, eseguire hello:
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a>Se si desidera toouse un modulo di protezione hardware (HSM)
Per maggiore sicurezza, è possibile importare o generare chiavi in moduli di protezione hardware (HSM) che non lasciano mai il limite HSM hello. Hello i moduli HSM sono FIPS 140-2 livello 2 convalidato. Se questo requisito non si applica a tooyou, ignorare questa sezione e passare troppo[Elimina insieme di credenziali chiave hello e le chiavi associate e i segreti](#delete-the-key-vault-and-associated-keys-and-secrets).

toocreate queste chiavi HSM protette, è necessario avere una sottoscrizione di insieme di credenziali che supporta chiavi HSM protette.

Quando si crea keyvault hello, aggiungere il parametro 'sku' hello:

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
È possibile aggiungere le chiavi protette tramite software (come illustrato in precedenza) e l'insieme di credenziali delle chiavi HSM protette toothis. toocreate una chiave HSM protetta, set hello destinazione parametro too'HSM':

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

È possibile utilizzare hello successivo comando tooimport una chiave da un file con estensione PEM nel computer in uso. Questo comando consente di importare chiave hello in hello servizio insieme di credenziali chiave HSM:

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
comando successivo Hello Importa un "bring your own key" pacchetto (BYOK). Ciò consente di generare la chiave nel modulo di protezione hardware locale e trasferirlo nel servizio insieme di credenziali chiave, hello tooHSMs senza chiave hello lasciando limite HSM hello:

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
Per ulteriori istruzioni su come toogenerate il pacchetto BYOK, vedere [come toouse HSM-Protected chiavi insieme di credenziali chiave di Azure](key-vault-hsm-protected-keys.md).

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a>Eliminare l'insieme di credenziali chiave hello e le chiavi associate e i segreti
Se non è più necessario insieme di credenziali chiave hello e hello chiave o il segreto in esso contenuti, è possibile eliminare l'insieme di credenziali chiave hello utilizzando hello `az keyvault delete` comando:

```
az keyvault delete --name 'ContosoKeyVault'
```

In alternativa, è possibile eliminare un gruppo di risorse di Azure intero, che include l'insieme di credenziali chiave di hello e altre risorse che incluso in tale gruppo:

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a>Altri comandi dell'interfaccia della riga di comando multipiattaforma di Azure
Altri comandi che potrebbero essere utili per la gestione dell'insieme di credenziali delle chiavi di Azure.

Questo comando ottiene una visualizzazione tabulare di tutte le chiavi e le proprietà selezionate:

az keyvault key list --vault-name 'ContosoKeyVault'

Questo comando Visualizza un elenco completo delle proprietà per la chiave specificata hello:

az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'

Questo comando ottiene una visualizzazione tabulare di tutti nomi dei segreti e tutte le proprietà selezionate:

az keyvault secret list --vault-name 'ContosoKeyVault'

Di seguito è riportato un esempio di come tooremove una chiave specifica:

az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'

Di seguito è riportato un esempio di come tooremove un segreto specifico:

az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'


## <a name="next-steps"></a>Passaggi successivi
Per riferimenti sull'interfaccia della riga di comando di Azure per i comandi delle credenziali delle chiavi, vedere [Key Vault CLI reference](/cli/azure/keyvault) (Riferimento dell'interfaccia della riga di comando di Key Vault)

Per i riferimenti di programmazione, vedere [hello Guida per gli sviluppatori insieme credenziali chiavi Azure](key-vault-developers-guide.md).
