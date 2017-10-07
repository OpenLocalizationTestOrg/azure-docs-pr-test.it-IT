---
title: ruoli di controllo di accesso basato sui ruoli personalizzati aaaCreate e assegnare toointernal e gli utenti esterni in Azure | Documenti Microsoft
description: Assegnare ruoli personalizzati di controllo degli accessi in base al ruolo creati con PowerShell e l'interfaccia della riga di comando per utenti interni ed esterni
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a>Introduzione al controllo degli accessi in base al ruolo

Controllo di accesso basato sui ruoli è una funzionalità di sola portale Azure consentendo ai proprietari di una sottoscrizione di hello tooassign ruoli granulari tooother gli utenti possono gestire gli ambiti di risorsa specifico nel proprio ambiente.

RBAC consente una migliore gestione della sicurezza per organizzazioni di grandi dimensioni e per piccole e medie imprese di utilizzo con collaboratori esterni, i fornitori o collaboratori esterni che devono accedere alle risorse di toospecific nell'ambiente di ma non necessariamente toohello intera infrastruttura o qualsiasi ambiti correlati alla fatturazione. RBAC hello flessibilità di proprietario di una sottoscrizione di Azure gestita da account di amministratore hello (ruolo di amministratore del servizio a livello di sottoscrizione) e sono più utenti invitati toowork in hello ma senza stessa sottoscrizione qualsiasi amministrativi diritti per tale. Da una gestione e la prospettiva di fatturazione, funzionalità RBAC hello dimostra toobe un'opzione efficiente time e della gestione per l'utilizzo di Azure in vari scenari.

## <a name="prerequisites"></a>Prerequisiti
L'utilizzo nell'ambiente Azure hello RBAC richiede:

* Un computer autonomo con sottoscrizione di Azure toohello utente assegnato come proprietario (ruolo di sottoscrizione)
* Ruolo di proprietario hello di hello sottoscrizione di Azure
* Avere accesso toohello [portale di Azure](https://portal.azure.com)
* Verificare che hello toohave seguendo i provider di risorse registrato per la sottoscrizione utente hello: **Microsoft**. Per ulteriori informazioni su come tooregister hello i provider di risorse, vedere [i provider di gestione delle risorse, aree, le versioni dell'API e schemi](/azure-resource-manager/resource-manager-supported-services.md).

> [!NOTE]
> Le sottoscrizioni di Office 365 o di licenze di Azure Active Directory (ad esempio: accesso tooAzure Active Directory) fornito da hello Office 365 portal non qualità usa tale controllo.

## <a name="how-can-rbac-be-used"></a>Modalità d'uso del controllo degli accessi in base al ruolo
Il controllo degli accessi in base al ruolo può essere applicato in tre ambiti diversi in Azure. Da hello massimo ambito toohello uno più basso, sono i seguenti:

* Sottoscrizione (più alto)
* Gruppo di risorse
* Ambito di risorsa (hello più basso livello di accesso offerta autorizzazioni destinazione tooan ambito di singole risorse di Azure)

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a>Assegnare i ruoli RBAC ambito della sottoscrizione hello
Ecco due esempi comuni di uso del controllo degli accessi in base al ruolo:

* Con utenti esterni di organizzazioni hello (non fa parte del tenant di Azure Active Directory dell'utente admin hello) invitato toomanage determinate risorse o la sottoscrizione intera hello
* Utilizzo con utenti all'interno dell'organizzazione hello (fanno parte del tenant di Azure Active Directory dell'utente hello) ma parte del team diversi o gruppi a cui è necessario un accesso granulare entrambi toohello intera sottoscrizione o gruppi di risorse toocertain o la risorsa gli ambiti in hello ambiente

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a>Concedere l'accesso a livello di sottoscrizione per un utente all'esterno di Azure Active Directory
Ruoli RBAC possono essere concessa solo da **proprietari** della sottoscrizione hello pertanto l'utente amministratore hello necessario accedere con un nome utente che dispone di questo ruolo pre-assegnato o ha creato hello sottoscrizione di Azure.

Dal portale di Azure hello, dopo aver Accedi come amministratore, selezionare "Sottoscrizioni" e scegliere hello desiderato uno.
![Pannello di sottoscrizione nel portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) per impostazione predefinita, se l'utente amministratore hello ha acquistato hello sottoscrizione di Azure, utente hello viene visualizzata come **amministratore dell'Account**, questo corso ruolo sottoscrizione hello. Per ulteriori informazioni sui ruoli di hello sottoscrizione di Azure, vedere [aggiungere o modificare ruoli di amministratore di Azure che gestiscono la sottoscrizione hello o servizi](/billing/billing-add-change-azure-subscription-administrator.md).

In questo esempio hello utente "alflanigan@outlook.com" è hello **proprietario** sottoscrizione in hello AAD di hello "Versione di valutazione gratuita" tenant "Default tenant di Azure". Poiché questo utente creatore hello di hello sottoscrizione di Azure con hello iniziale Account Microsoft "Outlook" (Account Microsoft = Outlook, in tempo reale e così via) nome di dominio hello predefinito per tutti gli altri utenti aggiunti in questo tenant sarà **"@alflaniganuoutlook.onmicrosoft.com"**. Per impostazione predefinita, sintassi hello del nuovo dominio hello è formata dalla combinazione di nome hello di nome utente e dominio dell'utente hello che ha creato il tenant hello e aggiunta estensione hello **". c o m"**.
Inoltre, gli utenti possono Accedi con un nome di dominio personalizzato nel tenant di hello dopo l'aggiunta e verifica per il nuovo tenant di hello. Per ulteriori informazioni su come tooverify un nome di dominio personalizzato in un tenant di Azure Active Directory, vedere [aggiungere una directory tooyour nome di dominio personalizzato](/active-directory/active-directory-add-domain).

In questo esempio, la directory hello "tenant predefinito Azure" contiene solo gli utenti con il nome di dominio hello "@alflanigan.onmicrosoft.com".

Dopo aver selezionato la sottoscrizione hello, è necessario fare clic su utente admin hello **il controllo di accesso (IAM)** e quindi **aggiungere un nuovo ruolo**.





![funzione IAM di controllo di accesso nel portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![aggiungere un nuovo utente nella funzione IAM di controllo di accesso nel portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

passaggio successivo Hello è tooselect hello ruolo toobe assegnato e utente hello che verrà assegnato al ruolo RBAC hello. In hello **ruolo** utente admin hello di menu a discesa Visualizza solo hello RBAC ruoli predefiniti che sono disponibili in Azure. Per altre descrizioni di ogni ruolo e dei relativi ambiti assegnabili, vedere [Ruoli predefiniti per il controllo degli accessi in base al ruolo di Azure](/active-directory/role-based-access-built-in-roles.md).

l'utente amministratore Hello deve quindi l'indirizzo di posta elettronica hello tooadd dell'utente esterno hello. Hello previsto è il comportamento per hello utente esterno toonot compaiano in hello tenant esistente. Dopo che è stato invitato l'utente esterno hello, saranno visibile in **sottoscrizioni > controllo di accesso (IAM)** con tutti gli utenti correnti hello che sono attualmente assegnati a un ruolo RBAC hello ambito della sottoscrizione.





![aggiungere le autorizzazioni toonew RBAC ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![elenco di ruoli di controllo degli accessi in base al ruolo a livello di sottoscrizione](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

utente Hello "chessercarlton@gmail.com" è stato invitato toobe un **proprietario** per hello sottoscrizione "Versione di valutazione gratuita". Dopo l'invio di invito hello utente esterno hello riceverà una conferma tramite posta elettronica con un collegamento di attivazione.
![Invito tramite posta elettronica per il ruolo di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)

Da organizzazione toohello esterno, hello nuovo utente non dispone gli attributi esistenti nella directory "Tenant di Azure predefinita" hello. Verranno creati previo consenso toobe registrate nella directory hello associata alla sottoscrizione hello che egli è stato assegnato un ruolo utente esterno hello.





![messaggio di invito tramite posta elettronica per il ruolo di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

utente esterno Hello Mostra in hello tenant di Azure Active Directory in come utente esterno e possono essere visualizzato nel portale di Azure hello e nel portale classico hello.





![pannello utenti azure active directory portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![pannello utenti azure active directory portale di Azure classico](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

In hello **utenti** vista in entrambi i portali hello perché gli utenti esterni può essere riconosciuto da:

* tipo di icona diversa Hello in hello portale di Azure
* Hello diverso punti nel portale classico hello di determinazione dell'origine

Tuttavia, la concessione **proprietario** o **collaboratore** accesso tooan esterno utente hello **sottoscrizione** ambito, non consentire hello accesso toohello amministrazione della directory dell'utente, a meno che non hello **amministratore globale** lo consente. In proprietà utente hello, hello **tipo utente** che presenta due parametri comuni, **membro** e **Guest** possono essere identificati. Un membro è un utente a cui viene registrato nella directory di hello mentre un utente guest è una directory toohello utente oltre agli inviti inviati da un'origine esterna. Per altre informazioni, vedere [Procedura per aggiungere utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori](/active-directory/active-directory-b2b-admin-add-users).

> [!NOTE]
> Assicurarsi che dopo aver immesso le credenziali di hello nel portale di hello, gli utenti esterni hello Seleziona directory corretta di hello toosign in. Hello stesso utente può dispone di accesso toomultiple directory e possono selezionare uno di essi facendo clic sul nome utente hello in hello lato superiore destro nel portale di Azure hello e quindi scegliere la directory appropriata hello dall'elenco a discesa hello.

Pur essendo guest nella directory di hello, utente esterno hello possibile gestire tutte le risorse per hello sottoscrizione di Azure, ma Impossibile accedere alla directory hello.





![portale di Azure active directory tooazure con restrizioni di accesso](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

Azure Active Directory e una sottoscrizione di Azure non hanno una relazione padre-figlio come quella che hanno altre risorse di Azure, ad esempio le macchine virtuali, le reti virtuali, le app Web, le risorse di archiviazione e così via, con una sottoscrizione di Azure. Hello tutti quest'ultimo viene creato, gestiti e fatturati in una sottoscrizione di Azure, mentre una sottoscrizione di Azure viene utilizzato toomanage hello accesso tooan directory Azure. Per ulteriori informazioni, vedere [sottoscrizione di Azure è tooAzure correlati AD](/active-directory/active-directory-how-subscriptions-associated-directory).

Da tutti hello RBAC ruoli predefiniti, **proprietario** e **collaboratore** offrono l'accesso di gestione complete risorse tooall in ambiente hello, hello differenza corso che non è possibile creare un collaboratore e delete nuovo Ruoli RBAC. come Hello altri ruoli predefiniti **collaboratore alla macchina virtuale** offrono l'accesso di gestione completa solo le risorse toohello indicate dal nome hello, indipendentemente dal hello **gruppo di risorse** la creazione in.

L'assegnazione hello ruolo incorporato e RBAC di **collaboratore alla macchina virtuale** a livello di sottoscrizione, significa che tale ruolo hello assegnati all'utente di hello:

* Può visualizzare tutte le macchine virtuali indipendentemente dal loro distribuzione data e hello gruppi di risorse di che fanno parte
* Dispone di macchine virtuali di gestione complete accesso toohello nella sottoscrizione hello
* Non è possibile visualizzare altri tipi di risorse nella sottoscrizione di hello
* Non può applicare modifiche dalla prospettiva della fatturazione

> [!NOTE]
> ACCESSI da un'unica funzionalità del portale Azure, non concede portale classico toohello di accesso.

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a>Assegnare un RBAC ruolo tooan esterno utente predefiniti
Per uno scenario diverso in questo test, hello utente esterno "alflanigan@gmail.com" viene aggiunto come un **collaboratore alla macchina virtuale**.




![ruolo predefinito collaboratore macchina virtuale](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

un comportamento normale per questo utente esterno con questo ruolo incorporato Hello è toosee e gestire solo le macchine virtuali e i relativi adiacenti Gestione risorse solo le risorse necessarie durante la distribuzione. Per impostazione predefinita, questi ruoli limitati consentono l'accesso solo le risorse corrispondenti tootheir create nel portale di Azure hello, indipendentemente dal fatto che alcune può ancora essere distribuito nel portale classico di hello (ad esempio: le macchine virtuali).





![Panoramica del ruolo Collaboratore macchina virtuale nel portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a>Concedere accesso a livello di sottoscrizione per un utente in hello stessa directory
flusso del processo Hello è identica tooadding un utente esterno, sia da hello prospettiva concessione hello RBAC ruolo di amministratore, nonché utente hello concessa ruolo toohello di accesso. differenza Hello è che utente hello invitato non riceverà gli inviti di qualsiasi messaggio di posta elettronica come tutti gli ambiti di risorsa hello in sottoscrizione hello saranno disponibili nel dashboard di hello dopo l'accesso.

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a>Assegnare ruoli RBAC nell'ambito del gruppo di risorse hello
L'assegnazione di un ruolo RBAC un **gruppo di risorse** ambito è un processo identico per l'assegnazione di ruolo hello a livello di sottoscrizione hello, per entrambi i tipi di utenti - esterni o interni (hello in parte stessa directory). Hello gli utenti a cui vengono assegnati il ruolo di RBAC hello è toosee nel proprio ambiente solo il gruppo di risorse hello che sia stato assegnato l'accesso da hello **gruppi di risorse** icona in hello portale di Azure.

## <a name="assign-rbac-roles-at-hello-resource-scope"></a>Assegnare i ruoli RBAC ambito risorsa hello
L'assegnazione di un ruolo RBAC a un ambito di risorse in Azure è un processo per l'assegnazione di ruolo hello a livello di sottoscrizione hello o a livello di gruppo di risorse hello identico, seguente hello stesso flusso di lavoro per entrambi gli scenari. Nuovamente, gli utenti di hello che vengono assegnati hello RBAC ruolo possono visualizzare solo gli elementi hello che sono stati assegnati l'accesso a, entrambi in hello **tutte le risorse** scheda o direttamente nei loro dashboard.

Un aspetto importante per RBAC sia nell'ambito di gruppo di risorse o risorse è per directory corretta di hello utenti toomake toohello verificare toosign-in.





![accesso alla directory nel portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a>Assegnare ruoli di controllo degli accessi in base al ruolo per un gruppo di Azure Active Directory
Tutti gli scenari di hello utilizzando RBAC hello tre diversi ambiti privilegi hello Azure offerta di gestione, distribuzione e amministrazione delle varie risorse come un utente assegnato senza hello necessario della gestione di una sottoscrizione personale. Tutte le risorse di hello create più avanti dagli utenti di hello assegnato vengono fatturate in hello una sottoscrizione di Azure in cui gli utenti di hello hanno accesso al ruolo RBAC hello indipendentemente dal fatto che viene assegnato per una sottoscrizione, un gruppo di risorse o un ambito di risorsa. In questo modo, hello gli utenti che dispongono delle autorizzazioni di amministratore per la sottoscrizione Azure intera di fatturazione è una panoramica completa sul consumo di hello, indipendentemente dal fatto che che gestisce le risorse di hello.

Per le organizzazioni più grandi, è possono applicare ruoli RBAC in hello allo stesso modo per gruppi di Azure Active Directory si considera di tale utente amministratore hello prospettiva hello vuole toogrant un accesso granulare hello per team o reparti interi, non singolarmente per ogni utente, pertanto possibilità di valutazione è molto tempo e la gestione efficiente. tooillustrate questo esempio, hello **collaboratore** ruolo è stato aggiunto tooone dei gruppi di hello nel tenant di hello a livello di sottoscrizione hello.





![aggiungere il ruolo di controllo degli accessi in base al ruolo per i gruppi AAD](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

Questi gruppi sono gruppi di sicurezza di cui viene eseguito il provisioning e la gestione solo all'interno di Azure Active Directory.

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a>Creare un supporto di tooopen ruolo RBAC personalizzato richieste tramite PowerShell
ruoli RBAC incorporati Hello che sono disponibili in Azure verificare alcuni livelli di autorizzazione basate sulle risorse disponibili di hello in ambiente hello. Tuttavia, se nessuno di questi ruoli sono adatti alle esigenze dell'utente dell'amministratore di hello, è accesso toolimit di hello opzione ulteriormente creando ruoli RBAC personalizzati.

Creazione di ruoli RBAC personalizzati richiede un ruolo incorporato e tootake, modificarlo e importarlo in ambiente hello. download di Hello e il caricamento del ruolo hello vengono gestiti tramite PowerShell o CLI.

È importante toounderstand prerequisiti a hello di creazione di un ruolo personalizzato che possono concedere un accesso granulare a livello di sottoscrizione hello e consentono inoltre di hello invitato hello flessibilità di apertura di richieste di supporto.

Per questo ruolo predefiniti di esempio hello **lettore** che consente agli utenti accesso tooview tutte le risorse hello ambiti ma non tooedit li o crearne di nuovi è stato personalizzato tooallow hello utente hello possibile aprire le richieste di assistenza.

Hello prima azione di esportazione hello **lettore** ruolo esigenze toobe completata in PowerShell è stato eseguito con autorizzazioni elevate come amministratore.

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Screenshot di PowerShell per il ruolo Lettore di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

È quindi necessario modello JSON di hello tooextract del ruolo hello.





![Modello JSON per il ruolo personalizzato Lettore di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

Un tipico ruolo di controllo degli accessi in base al ruolo è composto da tre sezioni principali, **Actions**, **NotActions** e **AssignableScopes**.

In hello **azione** sezione sono elencati tutti hello operazioni consentite per questo ruolo. È importante toounderstand che ogni azione viene assegnato da un provider di risorse. In questo caso, per la creazione di hello ticket di supporto **Microsoft. support** provider di risorse deve essere elencato.

toosee in grado di toobe tutti hello i provider di risorse disponibili e registrati nella sottoscrizione, è possibile utilizzare PowerShell.
```
Get-AzureRMResourceProvider

```
Inoltre, è possibile controllare per hello tutti hello disponibile PowerShell cmdlet toomanage hello provider di risorse.
    ![Screenshot di PowerShell per la gestione dei provider di risorse](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)

toorestrict tutti hello azioni per un particolare ruolo RBAC resource provider sono elencati nella sezione hello **NotActions**.
Infine, è obbligatoria che tale ruolo RBAC hello contiene sottoscrizione esplicita hello ID in cui viene utilizzato. Hello gli ID di sottoscrizione sono elencati sotto hello **AssignableScopes**, in caso contrario non sarà possibile ruolo hello tooimport nella sottoscrizione.

Dopo la creazione e personalizzazione hello RBAC ruolo, è necessario ambiente hello indietro importati toobe.

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

In questo esempio, nome personalizzato per questo ruolo RBAC il hello è "lettore supporto ticket livello di accesso" consentendo hello utente tooview tutti gli elementi nella sottoscrizione di hello e anche le richieste di assistenza tooopen.

> [!NOTE]
> sono Hello solo due ruoli RBAC incorporati che consentono l'azione hello di apertura di richieste di supporto **proprietario** e **collaboratore**. Per un utente toobe in grado di tooopen le richieste di assistenza, egli deve essere assegnato un RBAC ruolo solo nell'ambito di sottoscrizione hello, poiché tutte le richieste di supporto vengono create in base a una sottoscrizione di Azure.

Questo nuovo ruolo personalizzato è stato assegnato l'utente tooan hello stessa directory.





![schermata del ruolo RBAC personalizzata importata nel portale di Azure hello](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![schermata di assegnazione personalizzato toouser ruolo RBAC importati in hello stessa directory](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![screenshot delle autorizzazioni per il ruolo personalizzato importato di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

esempio Hello è stata ulteriormente i limiti di hello tooemphasize dettagliate di questo ruolo RBAC personalizzato come indicato di seguito:
* Può creare nuove richieste di supporto
* Non può creare nuovi ambiti di risorse, ad esempio la macchina virtuale
* Non può creare nuovi gruppi di risorse





![screenshot del ruolo personalizzato di controllo degli accessi in base al ruolo che crea richieste di supporto](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![schermata del ruolo RBAC personalizzato non è possibile toocreate macchine virtuali](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![schermata del ruolo RBAC personalizzato non è possibile toocreate RGs nuovo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a>Creare un supporto di tooopen ruolo RBAC personalizzato richieste tramite l'interfaccia CLI di Azure
In esecuzione su un Mac e senza accesso tooPowerShell, CLI di Azure è toogo modo hello.

Hello passaggi toocreate un ruolo personalizzato sono hello stesso, con l'unica eccezione hello che usa CLI ruolo hello non è possibile scaricare un modello JSON, ma possono essere visualizzati in hello CLI.

Per questo esempio ho scelto ruolo incorporato e hello di **lettore Backup**.

```

azure role show "backup reader" --json

```





![Screenshot dell'interfaccia della riga di comando del ruolo di lettore backup](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

Modifica ruolo hello in Visual Studio dopo la copia memorizzando hello in un modello JSON, hello **Microsoft. support** provider di risorse è stata aggiunta in hello **azioni** sezioni in modo che l'utente può aprire richieste di assistenza continuando toobe un lettore per gli insiemi di credenziali backup hello. Caso è necessario tooadd ID di sottoscrizione hello in cui verrà utilizzato questo ruolo in hello **AssignableScopes** sezione.

```

azure role create --inputfile <path>

```





![Screenshot dell'interfaccia della riga di comando di importazione del ruolo personalizzato di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

nuovo ruolo Hello è ora disponibile nel portale di Azure hello e processo di tutte le assegnazioni di hello è hello stesso, come negli esempi precedenti hello.





![Screenshot del portale di Azure del ruolo personalizzato di controllo degli accessi in base al ruolo creato usando l'interfaccia della riga di comando 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

A partire da hello 2017 di compilazione più recente, hello Shell di Cloud di Azure è disponibile. Shell Cloud Azure è un complemento tooIDE hello portale di Azure. Con questo servizio si ottiene una shell basata su browser autenticata e ospitata in Azure che è possibile usare al posto dell'interfaccia della riga di comando installata nel computer.





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
