---
title: aaaLog in tooAzure da hello CLI | Documenti Microsoft
description: Connettersi tooyour sottoscrizione di Azure da hello interfaccia della riga di comando di Azure (Azure CLI) per Windows, Mac e Linux
editor: tysonn
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: ed856527-d75e-4e16-93fb-253dafad209d
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: rasquill
"\"/": 
ms.openlocfilehash: 42682c00c8dea78b2c624e640379716d1d4d7a2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="log-in-tooazure-from-hello-azure-cli"></a>Accedi tooAzure da hello CLI di Azure
Hello CLI di Azure è un set di comandi open source, multipiattaforma per l'utilizzo di risorse di Azure. Questo articolo descrive hello modi tooprovide account Azure credenziali tooconnect hello Azure CLI tooyour sottoscrizione di Azure:

* Eseguire hello `azure login` tooauthenticate comando CLI tramite Azure Active Directory. Questo consente di metodo accedere tooCLI comandi sia in [comando modalità](#cli-command-modes). Quando si esegue il comando hello senza opzioni aggiuntive, `azure login` chiede toocontinue accedono in modo interattivo tramite un portale web. Per ulteriori `azure login` le opzioni del comando, vedere scenari di hello in questo articolo, o tipo `azure login --help`.
* Se è necessario solo i comandi CLI modalità gestione dei servizi Azure toouse (non consigliati per le distribuzioni più nuove), è possibile scaricare e installare un file di impostazioni di pubblicazione nel computer in uso.

Se non è ancora installato hello CLI, vedere [installazione hello Azure CLI](cli-install-nodejs.md). Se non si dispone di una sottoscrizione di Azure, è possibile creare un [account gratuito](http://azure.microsoft.com/free/) in pochi minuti.

Per informazioni sulle diverse identità dell'account e sulle sottoscrizioni di Azure, vedere [Associare le sottoscrizioni di Azure ad Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="scenario-1-azure-login-with-interactive-login"></a>Scenario 1: accesso di Azure con accesso interattivo
Con alcuni account, hello CLI richiede toorun `azure login` e continuare il processo di accesso hello con un browser web tramite un portale web, un processo denominato *accesso interattivo*. Una causa comune è quando si dispone di un account aziendale o dell'istituto di istruzione (detto anche un *account aziendale*) configurata l'autenticazione a più fattori toorequire. Utilizzare inoltre accesso interattivo con l'account Microsoft, quando si desidera toouse comandi della modalità di gestione delle risorse.

Accesso interattivo è semplice: tipo `azure login` - senza opzioni, come illustrato nell'esempio seguente hello:

```
azure login
```                                                                                             

output di Hello visualizzato è simile alla seguente hello:

```         
info:    Executing command login
info:    toosign in, use a web browser tooopen hello page http://aka.ms/devicelogin. Enter hello code XXXXXXXXX tooauthenticate.
```
Copiare il codice hello offerto tooyou nell'output del comando hello e aprire toohttp://aka.ms/devicelogin un browser o un'altra pagina, se specificato. (È possibile aprire un browser di hello stesso computer, oppure in un altro computer o dispositivo.) Immettere il codice hello e non è richiesta tooenter hello username e password per l'identità di hello desiderato toouse. Al termine delle operazioni, shell dei comandi hello completa accesso hello. Potrebbe essere simile a:

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> Con l'accesso interattivo l'autenticazione e l'autorizzazione vengono eseguite usando Azure Active Directory. Se si utilizza un'identità dell'account Microsoft, il processo di accesso di hello accede nel dominio predefinito, Azure Active Directory. Se è stata effettuata l'iscrizione per un account Azure gratuito, Azure Active Directory ha creato automaticamente un dominio predefinito per l'account.
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a>Scenario 2: accesso di Azure con un nome utente e una password
Hello utilizzare `azure login` comando con il nome utente hello (`-u`) tooauthenticate parametro quando si desidera un lavoro toouse account aziendale o dell'istituto di istruzione che non richiede l'autenticazione a più fattori. Viene richiesto dalla riga di comando hello password hello (o è possibile passare come parametro aggiuntivo di hello password hello `azure login` comando). Hello seguente esempio passa hello nome utente di un account aziendale:

    azure login -u myUserName@contoso.onmicrosoft.com

Si è quindi richiesto tooenter la password:

    info:    Executing command login
    Password: *********

quindi, viene completato il processo di accesso di Hello.

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

Se si tratta del primo registrazione in tempo con queste credenziali, viene chiesto tooverify che si desidera toocache un token di autenticazione. Questo messaggio si verifica anche se è stata utilizzata in precedenza hello `azure logout` comando (descritta più avanti in articolo hello). eseguire il prompt dei comandi per gli scenari di automazione, toobypass `azure login` con hello `-q` parametro.

## <a name="scenario-3-azure-login-with-a-service-principal"></a>Scenario 3: accesso di Azure con un'entità servizio
Se si crea un'entità servizio per un'applicazione Active Directory e dell'entità servizio hello dispone delle autorizzazioni per la sottoscrizione, è possibile utilizzare hello `azure login` entità servizio hello tooauthenticate di comando. A seconda dello scenario, è possibile fornire credenziali hello dell'entità servizio hello come parametri espliciti di hello `azure login` comando. Ad esempio, hello seguente comando passa nome dell'entità servizio hello e l'ID tenant di Active Directory:

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

Verrà quindi richiesto tooprovide hello password. È anche possibile fornire le credenziali di hello tramite un codice di script o applicazione CLI o utilizzare un'entità di servizio certificato tooauthenticate hello in modo non interattivo per scenari di automazione. Per dettagli ed esempi, vedere [Autenticazione di un'entità servizio con Gestione risorse di Azure](resource-group-authenticate-service-principal-cli.md).

## <a name="scenario-4-use-a-publish-settings-file"></a>Scenario 4: usare un file di impostazioni di pubblicazione
Se è necessario solo i comandi CLI toouse hello gestione del servizio Azure modalità (ad esempio, toodeploy macchine virtuali di Azure nel modello di distribuzione classica hello), è possibile connettersi utilizzando un file di impostazioni di pubblicazione. Questo metodo consente di installare un certificato nel computer locale che consente attività di gestione tooperform per come sottoscrizione hello e certificato hello sono validi.

* **file di impostazioni di pubblicazione hello toodownload** per l'account, assicurarsi che hello CLI è in modalità di gestione dei servizi digitando `azure config mode asm`. Eseguire quindi hello comando seguente:

        azure account download

Verrà aperto il browser predefinito e chiede toosign in toohello [portale di Azure classico](https://manage.windowsazure.com). Dopo l'accesso, viene scaricato un file `.publishsettings` . Prendere nota del percorso in cui il file viene salvato.

> [!NOTE]
> Se l'account è associato a più tenant di Azure Active Directory, potrebbe essere richiesta tooselect che si desiderano toodownload impostazioni di pubblicazione di Active Directory del file di.
>
>

Dopo aver selezionato utilizzando la pagina di download hello o visitando il portale di Azure classico hello, hello Active Directory selezionato diventa hello predefinito utilizzato dal portale classico hello e pagina di download. Dopo aver stabilito l'impostazione predefinita, viene visualizzato il testo hello '**fare clic qui pagina di selezione toohello tooreturn**' nella parte superiore di hello della pagina di download di hello. Utilizzare hello fornito collegamento tooreturn toohello la pagina di selezione.

* **file di impostazioni di pubblicazione tooimport hello**eseguire hello il seguente comando:

        azure account import <path tooyour .publishsettings file>

> [!IMPORTANT]
> Dopo avere importato le impostazioni di pubblicazione, è necessario eliminare hello `.publishsettings` file. Non è più necessario da hello CLI di Azure e presenta un rischio per la sicurezza, poiché potrebbe essere utilizzato toogain accesso tooyour sottoscrizione.
>
>

## <a name="cli-command-modes"></a>Modalità di comando dell'interfaccia della riga di comando
Hello CLI di Azure sono disponibili due modalità di comando per l'utilizzo di risorse di Azure, con diversi set di comandi:

* **Modalità di gestione risorse** - per l'utilizzo di risorse di Azure nel modello di distribuzione di gestione risorse di hello. tooset questa modalità, eseguire `azure config mode arm`.
* **Modalità di gestione dei servizi** - per l'utilizzo di risorse di Azure nel modello di distribuzione classica hello. tooset questa modalità, eseguire `azure config mode asm`.

Alla prima installazione, hello versione corrente di hello che CLI è in modalità di gestione risorse.

> [!NOTE]
> modalità di gestione risorse di Hello e gestione dei servizi si escludono a vicenda. Vale a dire le risorse create in una modalità non possono essere gestite da hello altra modalità.
>
>

## <a name="multiple-subscriptions"></a>Più sottoscrizioni
Se si dispone di più sottoscrizioni di Azure, la connessione tooAzure concede l'accesso tooall sottoscrizioni associate le credenziali. Una sottoscrizione è selezionata come predefinito hello e utilizzata da hello CLI di Azure quando si eseguono operazioni. È possibile visualizzare le sottoscrizioni di hello, inclusi la sottoscrizione predefinita hello corrente, usando hello `azure account list` comando. Questo comando restituisce informazioni che seguono di toohello simile:

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

Nel precedente elenco di hello, hello **corrente** colonna indica una sottoscrizione predefinita corrente hello come Azure-sub-1. sottoscrizione di toochange hello predefinito, utilizzare hello `azure account set` comandi e specificare hello sottoscrizione che si desidera predefinito hello toobe. ad esempio:

    azure account set Azure-sub-2

In questo caso hello predefinito tooAzure sottoscrizione-sub-2.

> [!NOTE]
> Modifica sottoscrizione predefinita hello diventa effettiva immediatamente, senza che sia una modifica globale; nuovi comandi CLI di Azure, se vengono eseguiti da hello stessa istanza della riga di comando o un'istanza diversa, utilizzare la nuova sottoscrizione predefinita di hello.
>
>

Se si desidera toouse una sottoscrizione non predefinito con hello CLI di Azure, senza impostazione predefinita corrente della toochange hello, è possibile utilizzare hello `--subscription` l'opzione per il comando hello e specificare il nome di hello di sottoscrizione hello desiderato toouse per l'operazione di hello.

Dopo avere connesso tooyour sottoscrizione di Azure, iniziare a utilizzare hello Azure CLI comandi toowork con risorse di Azure.

## <a name="storage-of-cli-settings"></a>Archiviazione delle impostazioni dell'interfaccia della riga di comando
Se si accede con hello `azure login` comando o l'importazione delle impostazioni di pubblicazione, il profilo CLI e il log vengono archiviati un `.azure` directory situata nel `user` directory. La directory `user` è protetta dal sistema operativo. Tuttavia, si consiglia di eseguire passaggi aggiuntivi tooencrypt il `user` directory. È possibile farlo in hello seguenti modi:

* In Windows, modificare le proprietà di directory hello o utilizzare BitLocker.
* In Mac, attivare FileVault per directory hello.
* In Ubuntu, funzione hello Encrypted Home directory. Altre distribuzioni di Linux offrono funzionalità analoghe.

## <a name="logging-out"></a>Disconnessione
toolog out, usare hello comando seguente:

    azure logout -u <username>

Se hello sottoscrizioni associate account hello solo vengono autenticati con Active Directory, la disconnessione le informazioni sulla sottoscrizione dal profilo locale hello eliminazioni hello. Tuttavia, se un file di impostazioni di pubblicazione è stato importato anche per le sottoscrizioni di hello, la disconnessione solo eliminazioni Active Directory le informazioni dal profilo locale hello correlate.

## <a name="next-steps"></a>Passaggi successivi
* i comandi CLI di Azure toouse, vedere [i comandi CLI di Azure in modalità di gestione risorse](virtual-machines/azure-cli-arm-commands.md) e [i comandi CLI di Azure in modalità di gestione dei servizi](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).
* toolearn ulteriori informazioni su hello CLI di Azure, scaricare il codice sorgente, segnalare i problemi, o collaborazione progetto toohello, visitare hello [repository GitHub per hello Azure CLI](https://github.com/azure/azure-xplat-cli).
* Se si verificano problemi nell'utilizzo hello CLI di Azure o Azure, visitare hello [forum di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).
