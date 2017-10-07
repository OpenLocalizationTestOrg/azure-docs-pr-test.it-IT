---
title: aaaSet di gestione temporanea di ambienti per le app web in Azure App Service | Documenti Microsoft
description: Informazioni su come toouse staging pubblicazione per le app web in Azure App Service.
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a>Configurare gli ambienti di gestione temporanea nel Servizio app di Azure
<a name="Overview"></a>

Quando si distribuisce l'app web, l'app web su Linux, back-end per dispositivi mobili e app per le API troppo[servizio App](http://go.microsoft.com/fwlink/?LinkId=529714), è possibile distribuire uno slot di distribuzione separata tooa anziché slot di produzione predefinito hello durante l'esecuzione in hello **Standard**o **Premium** modalità del piano di servizio App. Gli slot di distribuzione sono in realtà app dal vivo con nomi host specifici. Gli elementi di contenuto e le configurazioni di App possono essere scambiati tra i due slot di distribuzione, compreso hello slot di produzione. Distribuzione di slot di distribuzione di applicazione tooa ha hello seguenti vantaggi:

* È possibile convalidare modifiche all'applicazione in uno slot di distribuzione di gestione temporanea prima di scambiarlo con lo slot di produzione hello.
* Distribuzione di uno slot tooa app prima che lo scambio alla produzione assicura che tutte le istanze di slot hello sono riscaldate prima viene scambiato nell'ambiente di produzione. Ciò consente di evitare i tempi di inattività al momento della distribuzione dell'app. Hello reindirizzamento del traffico è seamless e nessuna richiesta viene eliminata in seguito a operazioni di scambio. L'intero flusso di lavoro può essere automatizzata tramite la configurazione di [scambio automatico](#Auto-Swap) quando non è necessario spazio di pre-swapping convalida.
* Dopo uno scambio, slot hello con app con installazione di appoggio in precedenza può hello precedente dell'applicazione di produzione. Se le modifiche di hello scambiate nello slot di produzione hello non corrisponda a quello desiderato, è possibile eseguire hello che stesso scambio immediatamente il backup tooget "ultimo noto buona sito".

Ciascuna modalità di piano App Service supporta un numero diverso di slot di distribuzione. supporta la modalità dell'app toofind numero hello di slot, vedere [prezzi del servizio App](https://azure.microsoft.com/pricing/details/app-service/).

* Quando l'applicazione ha più slot, è possibile modificare la modalità hello.
* Gli slot non di produzione non sono scalabili.
* La gestione delle risorse collegate non è supportata per gli slot non di produzione. In hello [portale Azure](http://go.microsoft.com/fwlink/?LinkId=529715) solo, è possibile evitare il potenziale impatto su uno slot di produzione spostando temporaneamente hello slot non di produzione tooa servizio App piano modalità diversa. Si noti che lo slot non di produzione hello deve condividere nuovamente hello stessa modalità con lo slot di produzione hello prima che è possibile scambiare gli slot di due hello.

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a>Aggiungere uno slot di distribuzione
app Hello deve essere eseguita in hello **Standard** o **Premium** modalità in ordine per si tooenable più slot di distribuzione.

1. In hello [portale Azure](https://portal.azure.com/), Apri l'app [pannello della risorsa](../azure-resource-manager/resource-group-portal.md#manage-resources).
2. Scegliere hello **gli slot di distribuzione** opzione, quindi fare clic su **Aggiungi Slot**.
   
    ![Aggiungi nuovo slot di distribuzione][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > Se l'applicazione hello non sia già in hello **Standard** o **Premium** modalità, si riceverà un messaggio che indica la modalità di hello è supportato per l'abilitazione della pubblicazione di gestione temporanea. A questo punto, si dispone di hello opzione tooselect **aggiornamento** e passare toohello **scala** scheda dell'app prima di continuare.
   > 
   > 
3. In hello **aggiungere uno slot** pannello, assegnare un nome di uno slot hello e selezionare se tooclone configurazione delle app da un altro slot di distribuzione esistente. Fare clic su hello toocontinue di segno di spunta.
   
    ![Origine della configurazione][ConfigurationSource1]
   
    Hello prima volta che si aggiunge uno slot, si avrà solo due opzioni: configurazione clone dallo slot di hello predefinito nell'ambiente di produzione o non è affatto.
    Dopo aver creato gli slot diverse, sarà in grado di tooclone configurazione da uno slot diverso da hello nell'ambiente di produzione:
   
    ![Origini della configurazione][MultipleConfigurationSources]
4. Nel pannello della risorsa dell'applicazione, fare clic su **gli slot di distribuzione**, quindi fare clic su un tooopen slot di distribuzione pannello della risorsa che dello slot, con un set di configurazione come qualsiasi altra app e sulle metriche. Hello nome dello slot hello viene visualizzato nella parte superiore di hello di hello pannello tooremind che si sta visualizzando hello slot di distribuzione.
   
    ![Titolo slot di distribuzione][StagingTitle]
5. Fare clic su URL app hello nel pannello hello dello slot. Si noti lo slot di distribuzione hello ha il proprio nome host ed è anche un'applicazione in tempo reale. lo slot di distribuzione toohello accesso pubblico toolimit, vedere [App del servizio Web App: slot di distribuzione di produzione toonon accesso web blocco](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).

Non è presente alcun contenuto dopo la creazione dello slot di distribuzione. È possibile distribuire slot toohello da un repository di completamente diverso, o un ramo del repository diversi. È inoltre possibile modificare hello configurazione dello slot. Hello utilizzare pubblicazione le credenziali di distribuzione o del profilo associate hello slot di distribuzione per gli aggiornamenti del contenuto.  Ad esempio, è possibile [pubblicare toothis slot con git](app-service-deploy-local-git.md).

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a>Configurazione per gli slot di distribuzione ##
Quando si clona una configurazione da un altro slot di distribuzione, configurazione clonato hello è modificabile. Inoltre, alcuni elementi di configurazione seguirà contenuto hello in uno scambio (non slot specifico) mentre altri elementi di configurazione verranno mantenuta nel hello stesso slot dopo uno scambio (slot specifico). Hello elenchi seguenti vengono illustrati configurazione hello che verrà modificata durante lo scambio di slot.

**Impostazioni che vengono scambiate**:

* Impostazioni generali, quali la versione del framework, 32/64 bit, i socket Web
* Impostazioni dell'App (può essere configurato toostick tooa slot)
* Stringhe di connessione (può essere configurato toostick tooa slot)
* Mapping dei gestori
* Impostazioni di monitoraggio e diagnostica
* Contenuto WebJobs

**Impostazioni che non vengono scambiate**:

* Endpoint di pubblicazione
* Nomi di dominio personalizzati
* Certificati e associazioni SSL
* Impostazioni di scalabilità
* Utilità di pianificazione WebJobs

app impostazione o connessione stringa toostick tooa slot (non invertito), hello accesso tooconfigure **le impostazioni dell'applicazione** pannello per una specificato slot, quindi seleziona hello **impostazione Slot** casella per hello elementi di configurazione che è necessario utilizzare slot hello. Si noti che il contrassegno di un elemento di configurazione come slot specifico ha l'effetto di hello definizione di tale elemento come non sostituibili tra tutti gli slot di distribuzione hello associati hello app.

![Impostazioni di slot][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a>Swap degli slot di distribuzione 
È possibile scambiare gli slot di distribuzione di hello **Panoramica** o **gli slot di distribuzione** visualizzazione del pannello della risorsa dell'applicazione.

> [!IMPORTANT]
> Prima che lo scambio di un'app da uno slot di distribuzione nell'ambiente di produzione, assicurarsi che tutte le impostazioni specifiche di slot non sono configurate esattamente come si desidera toohave nella destinazione dello scambio hello.
> 
> 

1. tooswap gli slot di distribuzione, fare clic su hello **scambiare** pulsante nella barra dei comandi di hello dell'applicazione hello o nella barra dei comandi hello di uno slot di distribuzione.
   
    ![Pulsante Swap][SwapButtonBar]

2. Verificare che tale destinazione hello scambio origine e lo scambio siano impostate correttamente. In genere, destinazione dello scambio hello è slot di produzione hello. Fare clic su **OK** operazione hello toocomplete. Al termine dell'operazione di hello, gli slot di distribuzione hello sono stati invertiti.

    ![Scambio completo](./media/web-sites-staged-publishing/SwapImmediately.png)

    Per hello **scambio con anteprima** Scambia tipo, vedere [scambio con anteprima (scambio multifase)](#Multi-Phase).  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a>Scambio con anteprima (swap multifase)

Lo scambio con anteprima o swap multifase semplifica la convalida degli elementi di configurazione di uno slot specifico, ad esempio le stringhe di connessione.
Per i carichi di lavoro mission-critical, si desidera toovalidate che hello app si comporta come previsto quando viene applicata la configurazione dello slot di produzione hello, ed è necessario eseguire tale convalida *prima* app hello viene scambiato nell'ambiente di produzione. Lo scambio con anteprima è ciò che serve.

> [!NOTE]
> Lo scambio con anteprima non è supportato nelle applicazioni Web in Linux.

Quando si utilizza hello **scambio con anteprima** opzione (vedere [scambiare gli slot di distribuzione](#Swap)), servizio App hello seguenti:

- Non è compromessa mantiene hello destinazione slot invariato così carico di lavoro esistente in tale slot (ad esempio produzione).
- Si applica agli elementi di configurazione di hello di hello slot toohello origine slot di destinazione, incluse le stringhe di connessione specifica slot hello e le impostazioni dell'app.
- Riavvia i processi di lavoro hello nello slot di origine hello utilizzando tali elementi di configurazione menzionati in precedenza.
- Quando si completa scambio hello: slot di origine remota warmed hello passa in uno slot di destinazione hello. slot di destinazione Hello viene spostato in uno slot di origine hello come uno scambio manuale.
- Quando si annulla swap hello: consente di riapplicare gli elementi di configurazione hello dello slot di origine di hello origine slot toohello.

È possibile visualizzare l'anteprima esattamente come applicazione hello comporterà con la configurazione dello slot di destinazione hello. Dopo aver completato la convalida, è completare lo scambio di hello in un passaggio separato. Questo passaggio è hello vantaggio che lo slot di origine hello già riscaldato con la configurazione desiderata hello e i client non subiscono alcun tempo di inattività.  

Esempi per cmdlet di Azure PowerShell disponibili per lo scambio multifase hello sono inclusi in hello cmdlet PowerShell di Azure per sezione slot di distribuzione.

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a>Configurare lo scambio automatico
Semplifica lo scambio automatico DevOps scenari in cui si desidera toocontinuously distribuisce l'app con zero a freddo e tempi di inattività per i clienti finali dell'app hello. Quando uno slot di distribuzione è configurato per lo scambio automatico nell'ambiente di produzione, ogni volta che si esegue il push slot toothat di aggiornamento di codice, il servizio App automaticamente scambiare app hello nell'ambiente di produzione dopo che è già stato riscaldato nello slot di hello.

> [!IMPORTANT]
> Quando si abilita scambio automatico per uno slot, verificare che la configurazione dello slot di hello è esattamente configurazione hello per lo slot di destinazione di hello (in genere slot di produzione di hello).
> 
> 

> [!NOTE]
> Lo scambio automatico non è supportato nelle applicazioni Web in Linux.

La configurazione dello scambio automatico per uno slot è semplice. Attenersi alla procedura hello riportata di seguito:

1. In **Slot di distribuzione** selezionare uno slot non di produzione e scegliere **Impostazioni applicazione** nel pannello delle risorse di questo slot.  
   
    ![][Autoswap1]
2. Selezionare **su** per **scambio automatico**, selezionare uno slot di destinazione desiderato hello **Slot di scambio automatico**, fare clic su **salvare** nella barra dei comandi di hello. Assicurarsi di configurazione per lo slot di hello è esattamente hello destinata agli slot di destinazione hello.
   
    Hello **notifiche** scheda lampeggia una verde **successo** al termine dell'operazione di hello.
   
    ![][Autoswap2]
   
   > [!NOTE]
   > tootest scambio automatico per l'app, è possibile selezionare prima uno slot di destinazione non di produzione in **Slot di scambio automatico** toobecome familiarità con la funzione hello.  
   > 
   > 
3. Eseguire uno slot di distribuzione toothat push di codice. Verrà eseguito lo scambio automatico dopo un breve periodo di tempo e aggiornamento hello verrà riflesse nell'URL di slot di destinazione.

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a>toorollback un'app di produzione dopo lo scambio
Se vengono rilevati errori nell'ambiente di produzione dopo uno scambio di slot, il rollup slot hello tootheir indietro pre-swap stati per lo scambio di slot hello due stesso immediatamente.

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a>Riscaldamento personalizzato prima dello scambio
Alcune app potrebbero richiedere azioni di riscaldamento personalizzate. Hello `applicationInitialization` consente di elemento di configurazione in Web. config è toospecify l'inizializzazione personalizzata azioni toobe eseguita prima che venga ricevuta una richiesta. operazione di scambio Hello attenderà questo toocomplete riscaldamento personalizzato. Di seguito è riportato un frammento web.config di esempio.

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a>toodelete uno slot di distribuzione
Nel Pannello di hello per uno slot di distribuzione, pannello dello slot di distribuzione hello aperto, fare clic su **Panoramica** (pagina predefinita di hello), fare clic su **eliminare** nella barra dei comandi di hello.  

![Per eliminare uno slot di distribuzione][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a>Cmdlet Azure PowerShell per gli slot di distribuzione
Azure PowerShell è un modulo che fornisce i cmdlet toomanage Azure tramite Windows PowerShell, incluso il supporto per la gestione di slot di distribuzione in Azure App Service.

* Per informazioni sull'installazione e configurazione di Azure PowerShell e sull'autenticazione di Azure PowerShell con la sottoscrizione di Azure, vedere [come tooinstall e configurare Microsoft Azure PowerShell](/powershell/azure/overview).  

- - -
### <a name="create-a-web-app"></a>Creare un'app Web
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a>Creare uno slot di distribuzione
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a>Avviare uno scambio con revisione (scambio multifase) e applicare slot toosource configurazione dello slot di destinazione
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a>Annullare uno scambio (scambio con anteprima) in sospeso e ripristinare la configurazione dello slot di origine
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a>Swap degli slot di distribuzione
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a>Eliminare slot di distribuzione
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a>Comandi dell'interfaccia della riga di comando di Azure per gli slot di distribuzione
Hello CLI di Azure fornisce comandi multipiattaforma per l'utilizzo di Azure, incluso il supporto per la gestione di slot di distribuzione di servizio App.

* Per istruzioni sull'installazione e configurazione hello CLI di Azure, incluse le informazioni su come tooconnect CLI di Azure tooyour sottoscrizione di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md).
* comandi di hello toolist disponibili per il servizio App di Azure in hello CLI di Azure, chiamare `azure site -h`.

> [!NOTE] 
> Per i comandi dell'[interfaccia della riga di comando di Azure 2.0](https://github.com/Azure/azure-cli) relativi agli slot di distribuzione, vedere [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).

- - -
### <a name="azure-site-list"></a>azure site list
Per informazioni sulle App hello nella sottoscrizione corrente hello, chiamare **elenco del sito azure**, come illustrato nell'esempio seguente hello.

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a>azure site create
toocreate uno slot di distribuzione, chiamare **sito azure creare** e specificare il nome di hello di un'app esistente e il nome di hello di hello slot toocreate, come in hello di esempio seguente.

`azure site create webappslotstest --slot staging`

controllo del codice sorgente per hello nuovo slot di, utilizzare hello tooenable **- git** opzione, come in hello di esempio seguente.

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a>azure site swap
toomake hello dell'applicazione di produzione hello slot di distribuzione aggiornato, utilizzare hello **scambio sito azure** comando tooperform un'operazione di scambio, come in hello di esempio seguente. applicazione di produzione Hello non verifichino tempi di inattività, né verrà sottoposta ad a un avvio a freddo.

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a>azure site delete
toodelete uno slot di distribuzione che non è più necessario, utilizzare hello **eliminazione sito azure** comando, come in hello di esempio seguente.

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> Verificare il funzionamento di un'app Web. [provare il servizio app](https://azure.microsoft.com/try/app-service/) immediatamente e creare un'app iniziale temporanea, senza necessità di fornire una carta di credito e senza impegni.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
[Azure App Service Web App: consente di bloccare gli slot di distribuzione di produzione toonon di accesso web](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[tooApp introduzione del servizio in Linux](./app-service-linux-intro.md)
[versione di valutazione gratuita di Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

