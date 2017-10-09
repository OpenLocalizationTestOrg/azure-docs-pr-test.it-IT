---
title: insieme di credenziali chiave di Azure usa CLI aaaManage | Documenti Microsoft
description: "Utilizzare questa attività comuni di esercitazione tooautomate nell'insieme di credenziali chiave usando hello CLI"
services: key-vault
documentationcenter: 
author: BrucePerlerMS
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 66be6e44-684a-411b-802e-884628458ae7
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: bruceper
ms.openlocfilehash: 9ef506faa67e1f0db5b9e303300d63b135ddd7b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli"></a>Gestire l'insieme di credenziali delle chiavi tramite l'interfaccia della riga di comando

L'insieme di credenziali delle chiavi di Azure è disponibile nella maggior parte delle aree. Per ulteriori informazioni, vedere hello [insieme di credenziali chiave pagina dei prezzi](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introduzione

Utilizzare questa esercitazione toohelp si ottiene avviato con insieme credenziali chiavi Azure toocreate un contenitore di protezione avanzato (un insieme di credenziali) in Azure, toostore e gestire chiavi di crittografia e i segreti in Azure. Illustra hello processo di toocreate interfaccia della riga di comando multipiattaforma di Azure utilizzando un insieme di credenziali che contiene una chiave o una password che è quindi possibile utilizzare con un'applicazione Azure. L'esercitazione spiega poi come un'applicazione può usare questa chiave o password.

**Toocomplete tempo stimato:** 20 minuti

> [!NOTE]
> In questa esercitazione non include istruzioni su come toowrite hello applicazione Azure che uno dei passaggi di hello include, che mostra come tooauthorize un toouse applicazione una chiave o la chiave privata della chiave hello insieme di credenziali.
> 
> Attualmente, non è possibile configurare l'insieme di credenziali chiave di Azure nel portale di Azure hello. Seguire invece le istruzioni relative all'interfaccia della riga di comando multipiattaforma. In alternativa, per le istruzioni relative ad Azure PowerShell, vedere [questa esercitazione equivalente](key-vault-get-started.md).
> 
> 

Per informazioni generali sull'insieme di credenziali di Azure, vedere [Cos'è l'insieme di credenziali delle chiavi di Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione, è necessario disporre di hello seguenti:

* TooMicrosoft una sottoscrizione Azure. Se non si dispone di una sottoscrizione, è possibile iscriversi per una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial).
* Interfaccia della riga di comando multipiattaforma versione 0.9.1 o successiva. tooinstall hello versione più recente e connettersi tooyour sottoscrizione di Azure, vedere [installare e configurare l'interfaccia della riga di comando multipiattaforma di Azure hello](../cli-install-nodejs.md).
* Un'applicazione che verrà configurato toouse hello chiave o password creati in questa esercitazione. Un'applicazione di esempio è disponibile da hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343). Per istruzioni, vedere il file Leggimi di accompagnamento hello.

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a>Risorse della Guida per l'interfaccia della riga di comando multipiattaforma di Microsoft Azure

In questa esercitazione si presuppone che si ha familiarità con l'interfaccia della riga di comando hello (Bash, Terminal, prompt dei comandi)

Hello - Guida o -h parametro può essere utilizzato tooview della Guida in linea per i comandi specifici. In alternativa, help hello azure [comando] [opzioni] formato può essere anche usato tooreturn hello stesse informazioni. Ad esempio, i comandi tutte restituito seguente hello hello stesse informazioni:

    azure account set --help

    azure account set -h

    azure help account set

In caso di dubbi sui parametri hello necessari da un comando, fare riferimento tramite toohelp - help, -h o azure help [comando].

È inoltre possibile leggere hello seguenti esercitazioni tooget familiarità con Gestione risorse di Azure nell'interfaccia della riga di comando multipiattaforma di Azure:

* [Come tooinstall e configurare l'interfaccia riga di comando multipiattaforma di Azure](../cli-install-nodejs.md)
* [Uso dell'interfaccia della riga di comando multipiattaforma di Azure con Gestione risorse di Azure](../xplat-cli-azure-resource-manager.md)

## <a name="connect-tooyour-subscriptions"></a>Connettersi tooyour sottoscrizioni

toolog con un account aziendale, utilizzare hello comando seguente:

    azure login -u username -p password

o se si desidera toolog digitando in modo interattivo

    azure login

> [!NOTE]
> metodo di accesso Hello funziona solo con account aziendale. L'account aziendale corrisponde a un utente gestito dall'organizzazione e definito nel tenant Azure Active Directory dell'organizzazione.
> 
> 

Se si dispone attualmente di un account aziendale e si utilizza un toolog account Microsoft in tooyour sottoscrizione di Azure, è possibile creare facilmente tramite hello i passaggi seguenti.

1. Account di accesso toohello accesso toohello [il portale di gestione di Azure](https://manage.windowsazure.com/)e fare clic su Active Directory.
2. Se è presente alcuna directory, selezionare la directory di creare e fornire hello informazioni richieste.
3. Selezionare la directory e aggiungere un nuovo utente. Questo nuovo utente corrisponde a un account aziendale. Durante la creazione dell'utente hello hello verrà fornito con un indirizzo di posta elettronica per l'utente hello e una password temporanea. Salvare queste informazioni perché verranno utilizzate in un altro passaggio.
4. Dal portale di hello, selezionare le impostazioni e quindi selezionare gli amministratori. Selezionare Aggiungi e aggiungere hello nuovo utente come coamministratore. In questo modo hello account aziendale toomanage la sottoscrizione di Azure.
5. Infine, disconnettersi hello portale di Azure e quindi accedere di nuovo utilizzando hello nuovo account aziendale. Se si tratta di hello prima registrazione in tempo con questo account, sarà password hello toochange richiesta.

Per altre informazioni sull'uso dell'account aziendale con Microsoft Azure, vedere [Iscrizione ad Azure come organizzazione](../active-directory/sign-up-organization.md).

Se si dispone di più sottoscrizioni e si desidera toospecify un uno toouse specifico per l'insieme di credenziali chiave di Azure, digitare hello sottoscrizioni hello toosee per l'account di seguito:

    azure account list

Quindi, toospecify hello sottoscrizione toouse, tipo:

    azure account set <subscription name>

Per ulteriori informazioni sulla configurazione dell'interfaccia della riga di comando multipiattaforma di Azure, vedere [come tooInstall e l'interfaccia della riga di comando multipiattaforma di Azure configurare](../cli-install-nodejs.md).

## <a name="switch-toousing-azure-resource-manager"></a>Opzione toousing Gestione risorse di Azure
insieme di credenziali chiave Hello richiede Gestione risorse di Azure, quindi digitare hello seguenti modalità di gestione risorse tooAzure tooswitch:

    azure config mode arm

## <a name="create-a-new-resource-group"></a>Creare un nuovo gruppo di risorse
Quando si usa Gestione risorse di Azure, tutte le risorse correlate vengono create in un gruppo di risorse. Per questa esercitazione si creerà un nuovo gruppo di risorse denominato 'ContosoResourceGroup'.

    azure group create 'ContosoResourceGroup' 'East Asia'

primo parametro Hello è il nome di gruppo di risorse e hello secondo parametro è il percorso di hello. Per il percorso, utilizzare il comando di hello `azure location list` tooidentify come toospecify toohello un percorso alternativo uno in questo esempio. Se servono altre informazioni, digitare: `azure help location`

## <a name="register-hello-key-vault-resource-provider"></a>Registrazione provider di risorse hello insieme di credenziali chiave
Verificare che il provider di risorse dell'insieme di credenziali delle chiavi sia registrato nella sottoscrizione:

`azure provider register Microsoft.KeyVault`

Questa operazione deve solo toobe eseguito una volta per ogni sottoscrizione.

## <a name="create-a-key-vault"></a>Creare un insieme di credenziali delle chiavi

Hello utilizzare `azure keyvault create` comando toocreate un insieme di credenziali chiave. Questo script ha tre parametri obbligatori: il nome di un gruppo di risorse, un insieme di credenziali delle chiavi e la posizione geografica di hello.

Ad esempio, se si utilizza il nome dell'insieme di credenziali hello di ContosoKeyVault, nome gruppo di risorse hello di ContosoResourceGroup e il percorso di hello dell'Asia orientale, digitare:

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

output di Hello di questo comando Mostra le proprietà dell'insieme di credenziali chiave hello appena creato. proprietà di Hello due più importanti sono:

* **Nome**: nell'esempio hello tratta ContosoKeyVault. Questo nome verrà usato per altri cmdlet di insieme di credenziali delle chiavi.
* **vaultUri**: nell'esempio hello tratta https://contosokeyvault.vault.azure.net. Le applicazioni che usano l'insieme di credenziali tramite l'API REST devono usare questo URI.

L'account di Azure è ora autorizzato tooperform insieme di credenziali di qualsiasi operazione su questa chiave. Nessun altro lo è ancora.

## <a name="add-a-key-or-secret-toohello-key-vault"></a>Aggiungere una chiave o un insieme di credenziali chiave segreta toohello

Se si desidera toocreate insieme credenziali chiavi Azure una chiave protetta tramite software per l'utente, utilizzare hello `azure key create` comandi e digitare il seguente hello:

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

Tuttavia, se si dispone di una chiave esistente in un file con estensione PEM salvato come file locale in un file denominato softkey.pem che si desidera tooupload tooAzure insieme di credenziali chiave, digitare hello seguenti chiave hello tooimport dagli hello. File con estensione PEM, che protegge hello chiave tramite software nel servizio insieme di credenziali chiave hello:

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

È ora possibile fare riferimento chiave hello creati o caricati tooAzure insieme di credenziali chiave utilizzando il relativo URI. Utilizzare **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways ottenere la versione corrente di hello e usare **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget tale versione.

tooadd un insieme di credenziali toohello segreto, che è una password denominata SQLPassword e con valore hello Pa$ $w0rd tooAzure insieme di credenziali chiave hello tipo seguente:

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

È ora possibile fare riferimento a questa password che sono state aggiunte tooAzure insieme di credenziali chiave, tramite il relativo URI. Utilizzare **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways ottenere la versione corrente di hello e usare **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget tale versione.

Si considerino hello chiave o il segreto appena creato:

* tooview il tipo di chiave,:`azure keyvault key list --vault-name 'ContosoKeyVault'`
* tooview segreto, tipo:`azure keyvault secret list --vault-name 'ContosoKeyVault'`

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
2. A sinistra di hello, fare clic su **Active Directory**, quindi selezionare hello directory in cui è necessario registrare l'applicazione. <br> <br> 

>[!NOTE] 
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
tooauthorize hello applicazione tooaccess hello chiave o al segreto nell'insieme di credenziali hello, utilizzare hello `azure keyvault set-policy` comando.

Ad esempio, se il nome dell'insieme di credenziali è ContosoKeyVault e hello applicazione cui si desidera tooauthorize ha un ID client 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed e si desidera tooauthorize hello applicazione toodecrypt e accedere con le chiavi nell'insieme di credenziali, quindi eseguire hello seguenti:

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> Se si esegue nel prompt dei comandi di Windows, si devono sostituire le virgolette singole con le virgolette doppie e anche di escape doppie interno hello. Ad esempio: "[\"decrypt\",\"sign\"]".
> 
> 

Se si desiderano che stessi segreti tooread applicazione tooauthorize nell'insieme di credenziali, eseguire hello:

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a>Se si desidera toouse un modulo di protezione hardware (HSM)
Per maggiore sicurezza, è possibile importare o generare chiavi in moduli di protezione hardware (HSM) che non lasciano mai il limite HSM hello. Hello i moduli HSM sono FIPS 140-2 livello 2 convalidato. Se questo requisito non si applica a tooyou, ignorare questa sezione e passare troppo[Elimina insieme di credenziali chiave hello e le chiavi associate e i segreti](#delete-the-key-vault-and-associated-keys-and-secrets).

toocreate queste chiavi HSM protette, è necessario avere una sottoscrizione di insieme di credenziali che supporta chiavi HSM protette.

Quando si crea keyvault hello, aggiungere il parametro 'sku' hello:

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

È possibile aggiungere le chiavi protette tramite software (come illustrato in precedenza) e l'insieme di credenziali delle chiavi HSM protette toothis. toocreate una chiave HSM protetta, set hello destinazione parametro too'HSM':

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

È possibile utilizzare hello successivo comando tooimport una chiave da un file con estensione PEM nel computer in uso. Questo comando consente di importare chiave hello in hello servizio insieme di credenziali chiave HSM:

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

comando successivo Hello Importa un "bring your own key" pacchetto (BYOK). Ciò consente di generare la chiave nel modulo di protezione hardware locale e trasferirlo nel servizio insieme di credenziali chiave, hello tooHSMs senza chiave hello lasciando limite HSM hello:

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

Per ulteriori istruzioni su come toogenerate il pacchetto BYOK, vedere [come toouse HSM-Protected chiavi insieme di credenziali chiave di Azure](key-vault-hsm-protected-keys.md).

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a>Eliminare l'insieme di credenziali chiave hello e le chiavi associate e i segreti
Se non è più necessario insieme di credenziali chiave hello e hello chiave o il segreto in esso contenuti, è possibile eliminare l'insieme di credenziali chiave hello tramite comando di eliminazione keyvault hello azure:

    azure keyvault delete --vault-name 'ContosoKeyVault'

In alternativa, è possibile eliminare un gruppo di risorse di Azure intero, che include l'insieme di credenziali chiave di hello e altre risorse che incluso in tale gruppo:

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a>Altri comandi dell'interfaccia della riga di comando multipiattaforma di Azure
Altri comandi che potrebbero essere utili per la gestione dell'insieme di credenziali delle chiavi di Azure.

Questo comando ottiene una visualizzazione tabulare di tutte le chiavi e le proprietà selezionate:

    azure keyvault key list --vault-name 'ContosoKeyVault'

Questo comando Visualizza un elenco completo delle proprietà per la chiave specificata hello:

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

Questo comando ottiene una visualizzazione tabulare di tutti nomi dei segreti e tutte le proprietà selezionate:

    azure keyvault secret list --vault-name 'ContosoKeyVault'

Di seguito è riportato un esempio di come tooremove una chiave specifica:

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

Di seguito è riportato un esempio di come tooremove un segreto specifico:

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a>Passaggi successivi
Per i riferimenti di programmazione, vedere [hello Guida per gli sviluppatori insieme credenziali chiavi Azure](key-vault-developers-guide.md).

