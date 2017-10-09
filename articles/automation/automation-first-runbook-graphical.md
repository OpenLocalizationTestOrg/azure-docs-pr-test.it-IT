---
title: aaaMy primo grafica runbook di automazione di Azure | Documenti Microsoft
description: Esercitazione viene illustrata la creazione di hello, test e la pubblicazione di un runbook grafico semplice.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: runbook, modello di runbook, automazione runbook, runbook di Azure
ms.assetid: dcb88f19-ed2b-4372-9724-6625cd287c8a
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/17/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 964cf8bae75ca597959bfc39b2b07c22bbc9acb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-graphical-runbook"></a>Il primo runbook grafico

> [!div class="op_single_selector"]
> * [Grafico](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [Flusso di lavoro PowerShell](automation-first-runbook-textual.md)
> 
> 

In questa esercitazione viene illustrata la creazione hello di un [runbook grafico](automation-runbook-types.md#graphical-runbooks) in automazione di Azure.  Si inizia con un runbook semplice che verifica e pubblica mentre spiegheremo come tootrack hello lo stato di processo del runbook hello.  È modificare runbook hello tooactually Gestione risorse di Azure, in questo caso, avviare una macchina virtuale di Azure.  Verrà quindi completato esercitazione hello rendendo più affidabile hello runbook tramite l'aggiunta di parametri del runbook e collegamenti condizionali.

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa esercitazione, è necessario hello seguente.

* Sottoscrizione di Azure.  Se non si ha ancora una sottoscrizione, è possibile [attivare i vantaggi della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure <a href="/pricing/free-account/" target="_blank">[iscriversi per ottenere un account gratuito](https://azure.microsoft.com/free/).
* [Account di automazione di Azure](automation-sec-configure-azure-runas-account.md) toohold hello runbook ed eseguire l'autenticazione tooAzure risorse.  Questo account deve disporre dell'autorizzazione toostart e arrestare la macchina virtuale hello.
* Macchina virtuale di Azure.  Si arresterà e si avvierà la macchina virtuale in modo che non sia di produzione.

## <a name="step-1---create-runbook"></a>Passaggio 1: Creare un runbook
Viene innanzitutto creato un runbook semplice che restituisce testo hello *Hello World*.

1. Nel portale di Azure hello, aprire l'account di automazione.  
   pagina account di automazione Hello offre una rapida panoramica delle risorse hello in questo account.  Dovrebbero essere già disponibili alcuni asset.  La maggior parte di questi sono i moduli di hello che vengono inclusi automaticamente in un nuovo account di automazione.  È inoltre necessario avere asset delle credenziali hello menzionato in hello [prerequisiti](#prerequisites).
2. Fare clic su hello **runbook** riquadro tooopen hello elenco di runbook.<br> ![Controllo Runbook](media/automation-first-runbook-graphical/runbooks-resources-tile.png)
3. Creare un nuovo runbook facendo clic su hello **aggiungere un runbook** pulsante e quindi **creare un nuovo runbook**.
4. Nome di hello runbook hello *MyFirstRunbook grafica*.
5. In questo caso, verrà toocreate un [runbook grafico](automation-graphical-authoring-intro.md) pertanto selezionare **Graphical** per **tipo Runbook**.<br> ![Nuovo runbook](media/automation-first-runbook-graphical/create-new-runbook.png)<br>
6. Fare clic su **crea** toocreate hello runbook e l'editor grafico hello aperto.

## <a name="step-2---add-activities-toohello-runbook"></a>Passaggio 2: aggiungere attività toohello runbook
controllo della raccolta sul lato sinistro di hello dell'editor di hello Hello consente tooselect attività tooadd tooyour runbook.  Stiamo tooadd un **Write-Output** cmdlet toooutput testo hello runbook.

1. In hello controllo della raccolta, fare clic nella casella di testo hello ricerca e digitare **Write-Output**.  i risultati della ricerca Hello verranno visualizzati di seguito. <br> ![Microsoft.PowerShell.Utility](media/automation-first-runbook-graphical/search-powershell-cmdlet-writeoutput.png)
2. Scorrere verso il basso toohello inferiore dell'elenco di hello.  È possibile una rapida **Write-Output** e selezionare **aggiungere toocanvas** o fare clic su Avanti toohello cmdlet di hello puntini di sospensione e quindi selezionare **aggiungere toocanvas**.
3. Fare clic su hello **Write-Output** attività nell'area di disegno hello.  Consente di aprire Pannello di controllo configurazione hello, che consente attività hello tooconfigure.
4. Hello **etichetta** predefinito toohello nome del cmdlet hello, ma è possibile modificare toosomething più descrittivo. Modificarlo troppo*toooutput scrivere Hello World*.
5. Fare clic su **parametri** tooprovide valori per parametri del cmdlet hello.  
   Alcuni cmdlet avere più set di parametri ed è necessario tooselect quali uno toouse è. In questo caso, **Write-Output** ha un solo set di parametri, pertanto non è necessario tooselect uno. <br> ![Proprietà Write-Output](media/automation-first-runbook-graphical/write-output-properties-b.png)
6. Seleziona hello **InputObject** parametro.  Questo è il parametro hello in cui si specifica flusso di output di hello testo toosend toohello.
7. In hello **origine dati** elenco a discesa Seleziona **espressione PowerShell**.  Hello **origine dati** elenco a discesa sono disponibili varie origini utilizzare toopopulate un valore di parametro.  
   È possibile usare l'output da tali origini, ad esempio un'altra attività, un asset di automazione o un'espressione di PowerShell.  In questo caso, è sufficiente a testo hello toooutput *Hello World*. È possibile usare un'espressione di PowerShell e specificare una stringa.
8. In hello **espressione** digitare *"Hello World"* e quindi fare clic su **OK** due volte tooreturn toohello canvas.<br> ![PowerShell Expression](media/automation-first-runbook-graphical/expression-hello-world.png)
9. Salvare il runbook hello facendo **salvare**.<br> ![Salvataggio del runbook](media/automation-first-runbook-graphical/runbook-toolbar-save-revised20165.png)

## <a name="step-3---test-hello-runbook"></a>Passaggio 3: Test hello runbook
Prima Pubblichiamo toomake runbook hello è disponibile nell'ambiente di produzione, è necessario tootest è toomake assicurarsi che funzioni correttamente.  Quando si testa un runbook, è necessario eseguire la versione **Bozza** e visualizzarne l'output in modo interattivo.

1. Fare clic su **riquadro Test** blade di Test tooopen hello.<br> ![Riquadro Test](media/automation-first-runbook-graphical/runbook-toolbar-test-revised20165.png)
2. Fare clic su **avviare** test hello toostart.  Deve trattarsi di opzione hello solo abilitato.
3. Oggetto [processo del runbook](automation-runbook-execution.md) viene creato e il relativo stato visualizzati nel riquadro di hello.  
   lo stato del processo Hello viene avviato come *in coda* che indica che è in attesa per un runbook worker in hello cloud toobecome disponibili.  Viene quindi spostata troppo*iniziale* quando un thread di lavoro attestazioni processo hello e quindi *esecuzione* quando runbook hello effettivamente avviata l'esecuzione.  
4. Al termine del processo del runbook hello, viene visualizzato l'output. In questo caso, dovrebbe essere visualizzato *Hello World*.<br> ![Hello World](media/automation-first-runbook-graphical/runbook-test-results.png)
5. Chiudere l'area di disegno hello Test pannello tooreturn toohello.

## <a name="step-4---publish-and-start-hello-runbook"></a>Passaggio 4: pubblicare e avviare runbook hello
runbook Hello creata è ancora in modalità bozza. È necessario toopublish prima di poterlo eseguire nell'ambiente di produzione.  Quando si pubblica un runbook, con la versione bozza hello sovrascrivere versione hello già pubblicata.  In questo caso, non abbiamo una versione pubblicata ancora poiché runbook hello appena creato.

1. Fare clic su **pubblica** toopublish hello runbook e quindi **Sì** quando richiesto.<br> ![Pubblica](media/automation-first-runbook-graphical/runbook-toolbar-publish-revised20166.png)
2. Se si scorre tooview sinistro hello runbook hello **runbook** pannello mostra un **stato di creazione** di **pubblicato**.
3. Scorrimento toohello indietro tooview destra hello pannello **MyFirstRunbook**.  
   Hello opzioni in alto hello consentono toostart hello runbook, pianificarlo toostart in un momento nel futuro hello o creare un [webhook](automation-webhooks.md) in modo da poter essere avviato tramite una chiamata HTTP.
4. È sufficiente toostart hello runbook, fare clic sul **avviare** e quindi **Sì** quando richiesto.<br> ![Avvia runbook](media/automation-first-runbook-graphical/runbook-controls-start-revised20165.png)
5. Un pannello del processo è stato aperto per processo del runbook hello creati.  È possibile chiudere questo pannello, ma in questo caso viene lasciato aperto in modo è possibile controllare lo stato di avanzamento del processo di hello.
6. viene visualizzato lo stato del processo Hello in **riepilogo** e corrispondenze hello gli Stati che abbiamo visto quando è stato testato hello runbook.<br> ![Riepilogo dei processi](media/automation-first-runbook-graphical/runbook-job-summary.png)
7. Una volta hello Mostra lo stato runbook *completato*, fare clic su **Output**. Hello **Output** pannello è aperto ed è possibile osservare il nostro *Hello World* nel riquadro di hello.<br> ![Riepilogo dei processi](media/automation-first-runbook-graphical/runbook-job-output.png)  
8. Pannello di Output di hello Chiudi.
9. Fare clic su **tutti i log** tooopen hello flussi pannello processo del runbook hello.  Solo dovremmo vedere *Hello World* nell'output di hello flusso, tuttavia questa operazione consente di visualizzare i flussi per un processo del runbook, ad esempio dettagliati e di errore se runbook hello scrive toothem.<br> ![Riepilogo dei processi](media/automation-first-runbook-graphical/runbook-job-AllLogs.png)
10. Chiudere il pannello di tutti i log hello e blade di hello processo pannello tooreturn toohello MyFirstRunbook.
11. Fare clic su **processi** pannello processi di hello tooopen per questo runbook.  Elenca tutti i processi di hello creati da questo runbook. Dovremmo vedere solo un processo elencato in quanto è solo esecuzione hello processo una volta.<br> ![Processi](media/automation-first-runbook-graphical/runbook-control-jobs.png)
12. È possibile fare clic su questo processo tooopen hello stesso riquadro processo che abbiamo visto quando è stato avviato il runbook hello.  In questo modo si toogo indietro nel tempo e visualizzarne i dettagli di hello di qualsiasi processo che è stato creato per un runbook specifico.

## <a name="step-5---create-variable-assets"></a>Passaggio 5: Creare asset di variabile
Il runbook è stato testato e pubblicato, ma finora non esegue alcuna attività utile. Vogliamo toohave Gestione risorse di Azure.  Prima è stato possibile configurare tooauthenticate runbook hello, si crea un ID di sottoscrizione hello toohold variabile e farvi riferimento dopo che sono stati impostati hello attività tooauthenticate nel passaggio 6 seguente.  Incluso un contesto di riferimento toohello sottoscrizione consente tooeasily lavoro tra più sottoscrizioni.  Prima di procedere, copiare l'ID sottoscrizione dal riquadro di spostamento hello opzione sottoscrizioni hello.  

1. Nel Pannello di account di automazione hello, fare clic su hello **asset** riquadro e hello **asset** pannello viene aperto.
2. Nel pannello asset hello, fare clic su hello **variabili** riquadro.
3. Nel pannello variabili hello, fare clic su **aggiungere una variabile**.<br>![Variabile di Automazione](media/automation-first-runbook-graphical/create-new-subscriptionid-variable.png)
4. In hello nuova variabile pannello in hello **nome** immettere **AzureSubscriptionId** e hello **valore** casella immettere l'ID sottoscrizione.  Mantenere *stringa* per hello **tipo** e il valore predefinito hello per **crittografia**.  
5. Fare clic su **crea** variabile hello toocreate.  

## <a name="step-6---add-authentication-toomanage-azure-resources"></a>Passaggio 6: aggiungere l'autenticazione toomanage risorse di Azure
Ora che è disponibile una variabile toohold l'ID sottoscrizione, è possibile configurare tooauthenticate i runbook con hello Esegui come credenziali di cui viene fatto riferimento tooin hello [prerequisiti](#prerequisites).  Facciamo aggiungendo hello Azure runas connessione **Asset** e **Aggiungi AzureRMAccount** cmdlet toohello canvas.  

1. Editor grafico di hello aperto facendo **modifica** nel pannello MyFirstRunbook hello.<br> ![Modificare il runbook](media/automation-first-runbook-graphical/runbook-controls-edit-revised20165.png)
2. Non è necessario hello **scrivere Hello World toooutput** più, pertanto pulsante destro del mouse e selezionare **eliminare**.
3. Nel controllo della raccolta hello, espandere **connessioni** e aggiungere **AzureRunAsConnection** toohello area di disegno selezionando **aggiungere toocanvas**.
4. Nell'area di disegno hello, selezionare **AzureRunAsConnection** e nel riquadro di controllo configurazione di hello, digitare **ottenere eseguire come connessione** in hello **etichetta** casella di testo.  Si tratta di hello connessione
5. Nel controllo della raccolta hello, digitare **Aggiungi AzureRmAccount** nella casella di ricerca testo hello.
6. Aggiungi **Aggiungi AzureRmAccount** toohello area di disegno.<br> ![Add-AzureRMAccount](media/automation-first-runbook-graphical/search-powershell-cmdlet-addazurermaccount.png)
7. Passare il mouse su **ottenere eseguire come connessione** fino a quando non viene visualizzato un cerchio nella parte inferiore di hello della forma hello. Fare clic su cerchio hello e trascinare la freccia hello troppo**Aggiungi AzureRmAccount**.  freccia Hello creato è un *collegamento*.  Hello runbook viene avviato con **ottenere eseguire come connessione** e quindi eseguire **Aggiungi AzureRmAccount**.<br> ![Creare un collegamento tra le attività](media/automation-first-runbook-graphical/runbook-link-auth-activities.png)
8. Nell'area di disegno hello, selezionare **Aggiungi AzureRmAccount** e in configurazione hello controllo tipo di riquadro **accesso tooAzure** in hello **etichetta** casella di testo.
9. Fare clic su **parametri** e viene visualizzato il pannello di configurazione dei parametri attività hello.
10. **AzureRmAccount aggiungere** dispone di più set di parametri, pertanto è necessario tooselect uno prima che possiamo fornire i valori dei parametri.  Fare clic su **parametro impostato** e quindi selezionare hello **ServicePrincipalCertificatewithSubscriptionId** set di parametri.
11. Dopo aver selezionato il set di parametri di hello, parametri di hello vengono visualizzati nel Pannello di configurazione dei parametri attività hello.  Fare clic su **APPLICATIONID**.<br> ![Aggiungere parametri all'account Azure RM](media/automation-first-runbook-graphical/add-azurermaccount-params.png)
12. Nel Pannello di valore del parametro hello, selezionare **output attività** per hello **origine dati** e selezionare **ottenere eseguire come connessione** elenco hello in hello **campo percorso** tipo textbox **ApplicationId**, quindi fare clic su **OK**.  Si sta specificando nome di hello della proprietà hello per percorso campo hello perché l'attività hello restituisce un oggetto con proprietà più.
13. Fare clic su **CERTIFICATETHUMBPRINT**e nel Pannello di valore del parametro hello, selezionare **output attività** per hello **origine dati**.  Selezionare **ottenere eseguire come connessione** dall'elenco hello, hello **percorso campo** tipo textbox **CertificateThumbprint**, quindi fare clic su **OK**.
14. Fare clic su **SERVICEPRINCIPAL**e nel Pannello di valore del parametro hello, selezionare **ConstantValue** per hello **origine dati**, fare clic su opzione hello **True**, quindi fare clic su **OK**.
15. Fare clic su **TENANTID**e nel Pannello di valore del parametro hello, selezionare **output attività** per hello **origine dati**.  Selezionare **ottenere eseguire come connessione** dall'elenco hello, hello **percorso campo** tipo textbox **TenantId**, quindi fare clic su **OK** due volte.  
16. Nel controllo della raccolta hello, digitare **Set AzureRmContext** nella casella di ricerca testo hello.
17. Aggiungere **Set AzureRmContext** toohello area di disegno.
18. Nell'area di disegno hello, selezionare **Set AzureRmContext** e in configurazione hello controllo tipo di riquadro **specificare Id sottoscrizione** in hello **etichetta** casella di testo.
19. Fare clic su **parametri** e viene visualizzato il pannello di configurazione dei parametri attività hello.
20. **Set-AzureRmContext** dispone di più set di parametri, pertanto è necessario tooselect uno prima che possiamo fornire i valori dei parametri.  Fare clic su **parametro impostato** e quindi selezionare hello **SubscriptionId** set di parametri.  
21. Dopo aver selezionato il set di parametri di hello, parametri di hello vengono visualizzati nel Pannello di configurazione dei parametri attività hello.  Fare clic su **SubscriptionID**
22. Nel Pannello di valore del parametro hello, selezionare **Asset della variabile** per hello **origine dati** e selezionare **AzureSubscriptionId** dall'elenco di hello e quindi fare clic su **OK**  due volte.   
23. Passare il mouse su **tooAzure accesso** fino a quando non viene visualizzato un cerchio nella parte inferiore di hello della forma hello. Fare clic su cerchio hello e trascinare la freccia hello troppo**specificare Id sottoscrizione**.

Il runbook dovrebbe essere simile hello seguente a questo punto: <br>![Configurazione dell'autenticazione runbook](media/automation-first-runbook-graphical/runbook-auth-config.png)

## <a name="step-7---add-activity-toostart-a-virtual-machine"></a>Passaggio 7: aggiungere attività toostart una macchina virtuale
Di seguito viene aggiunta una **inizio AzureRmVM** attività toostart una macchina virtuale.  È possibile selezionare qualsiasi macchina virtuale nella sottoscrizione di Azure e per ora è hardcoded di nome nel cmdlet hello.

1. Nel controllo della raccolta hello, digitare **inizio AzureRm** nella casella di ricerca testo hello.
2. Aggiungere **inizio AzureRmVM** toohello area di disegno e quindi fare clic e trascinarlo sotto **specificare Id sottoscrizione**.
3. Passare il mouse su **specificare Id sottoscrizione** fino a quando non viene visualizzato un cerchio nella parte inferiore di hello della forma hello.  Fare clic su cerchio hello e trascinare la freccia hello troppo**inizio AzureRmVM**.
4. Selezionare **Start-AzureRmVM**.  Fare clic su **parametri** e quindi **parametro impostato** tooview hello imposta per **inizio AzureRmVM**.  Seleziona hello **ResourceGroupNameParameterSetName** set di parametri. Si noti che accanto a **ResourceGroupName** e **Name** sono presenti punti esclamativi.  Indicano che si tratta di parametri obbligatori.  Si noti anche che i valori previsti per entrambi sono stringhe.
5. Selezionare **Name**.  Selezionare **espressione PowerShell** per hello **origine dati** e digitare il nome di hello della macchina virtuale hello racchiuso tra virgolette doppie che si iniziano con il runbook.  Fare clic su **OK**.<br>![Valore del parametro Name di Start-AzureRmVM](media/automation-first-runbook-graphical/runbook-startvm-nameparameter.png)
6. Selezionare **ResourceGroupName**. Utilizzare **espressione PowerShell** per hello **origine dati** e digitare il nome di hello hello del gruppo di risorse racchiuso tra virgolette doppie.  Fare clic su **OK**.<br> ![Parametri di Start-AzureRmVM](media/automation-first-runbook-graphical/startazurermvm-params.png)
7. Fare clic su riquadro Test in modo che sia possibile testare il runbook hello.
8. Fare clic su **avviare** test hello toostart.  Una volta che è stata completata, verificare che la macchina virtuale hello è stata avviata.

Il runbook dovrebbe essere simile hello seguente a questo punto: <br>![Configurazione dell'autenticazione runbook](media/automation-first-runbook-graphical/runbook-startvm.png)

## <a name="step-8---add-additional-input-parameters-toohello-runbook"></a>Passaggio 8: aggiungere altri parametri di input toohello runbook
I runbook attualmente avvia macchina virtuale hello nel gruppo di risorse hello che sono state specificate nella hello **inizio AzureRmVM** cmdlet.  I runbook sarebbe più utile se è stato possibile specificarli entrambi durante hello runbook viene avviato.  È ora aggiungere parametri di input toohello runbook tooprovide tale funzionalità.

1. Editor grafico di hello aperto facendo **modifica** su hello **MyFirstRunbook** riquadro.
2. Fare clic su **Input e output** e quindi **aggiungere input** riquadro dei parametri di Input Runbook hello tooopen.<br> ![Input e output del runbook](media/automation-first-runbook-graphical/runbook-toolbar-InputandOutput-revised20165.png)
3. Specificare *VMName* per hello **nome**.  Mantenere *stringa* per hello **tipo**, ma modificare **obbligatorio** troppo*Sì*.  Fare clic su **OK**.
4. Creare un parametro di input obbligatorio secondo chiamato *ResourceGroupName* e quindi fare clic su **OK** tooclose hello **di Input e Output** riquadro.<br> ![Parametri di input del runbook](media/automation-first-runbook-graphical/start-azurermvm-params-outputs.png)
5. Seleziona hello **inizio AzureRmVM** attività e quindi fare clic su **parametri**.
6. Hello modifica **origine dati** per **nome** troppo**input Runbook** e quindi selezionare **VMName**.<br>
7. Hello modifica **origine dati** per **ResourceGroupName** troppo**input Runbook** e quindi selezionare **ResourceGroupName**.<br> ![Parametri Start-AzureVM](media/automation-first-runbook-graphical/start-azurermvm-params-runbookinput.png)
8. Salvare il runbook hello e aprire il riquadro di Test hello.  Si noti che è possibile ora specificare valori per hello due variabili di input utilizzati nel test hello.
9. Riquadro Test hello Chiudi.
10. Fare clic su **pubblica** la nuova versione hello toopublish di hello runbook.
11. Arrestare la macchina virtuale hello che è stato avviato nel passaggio precedente hello.
12. Fare clic su **avviare** toostart hello runbook.  Tipo di hello **VMName** e **ResourceGroupName** per la macchina virtuale hello che sarà toostart.<br> ![Start Runbook](media/automation-first-runbook-graphical/runbook-start-inputparams.png)
13. Al termine del processo di runbook hello, verificare che la macchina virtuale hello è stata avviata.

## <a name="step-9---create-a-conditional-link"></a>Passaggio 9: Creare un collegamento condizionale
È ora possibile modificare runbook hello in modo che cerca solo macchina virtuale di hello toostart se non è già stato avviato.  Questo scopo, aggiungere un **Get AzureRmVM** runbook toohello cmdlet che ottiene hello istanza lo stato del livello di macchina virtuale hello. Quindi aggiungere un modulo di codice del flusso di lavoro di PowerShell denominato **Ottieni stato** con un frammento di PowerShell codice toodetermine se hello macchina virtuale sia in esecuzione o arrestato.  Un collegamento condizionale da hello **Ottieni stato** modulo viene eseguito solo **inizio AzureRmVM** se lo stato di esecuzione corrente di hello viene arrestato.  Infine, abbiamo output tooinform un messaggio se hello VM è stato avviato correttamente o non deterministica tramite i cmdlet di PowerShell. Write-Output di hello.

1. Aprire **MyFirstRunbook** nell'editor grafico hello.
2. Rimuovi collegamento hello tra **specificare Id sottoscrizione** e **inizio AzureRmVM** facendo clic su di esso e quindi premendo hello *eliminare* chiave.
3. Nel controllo della raccolta hello, digitare **Get AzureRm** nella casella di ricerca testo hello.
4. Aggiungere **Get AzureRmVM** toohello area di disegno.
5. Selezionare **Get AzureRmVM** e quindi **parametro impostato** tooview hello imposta per **Get AzureRmVM**.  Seleziona hello **GetVirtualMachineInResourceGroupNameParamSet** set di parametri.  Si noti che accanto a **ResourceGroupName** e **Name** sono presenti punti esclamativi.  Indicano che si tratta di parametri obbligatori.  Si noti anche che i valori previsti per entrambi sono stringhe.
6. In **Origine dati** per **Nome** selezionare **Input runbook** e quindi selezionare **VMName**.  Fare clic su **OK**.
7. In **Origine dati** per **ResourceGroupName** selezionare **Input runbook** e quindi selezionare **ResourceGroupName**.  Fare clic su **OK**.
8. In **Origine dati** per **Stato** selezionare **Valore costante** e quindi fare clic su **True**.  Fare clic su **OK**.  
9. Creare un collegamento da **specificare Id sottoscrizione** troppo**Get AzureRmVM**.
10. Nel controllo libreria hello espandere **controllo Runbook** e aggiungere **codice** toohello area di disegno.  
11. Creare un collegamento da **Get AzureRmVM** troppo**codice**.  
12. Fare clic su **codice** e nel riquadro di configurazione hello, modificare l'etichetta troppo**Ottieni stato**.
13. Selezionare **codice** parametro e hello **Editor di codice** pannello viene visualizzato.  
14. Nell'editor di codice hello, incollare il seguente frammento di codice hello:
    
     ```
     $StatusesJson = $ActivityOutput['Get-AzureRmVM'].StatusesText
     $Statuses = ConvertFrom-Json $StatusesJson
     $StatusOut =""
     foreach ($Status in $Statuses){
     if($Status.Code -eq "Powerstate/running"){$StatusOut = "running"}
     elseif ($Status.Code -eq "Powerstate/deallocated") {$StatusOut = "stopped"}
     }
     $StatusOut
     ```
15. Creare un collegamento da **Ottieni stato** troppo**inizio AzureRmVM**.<br> ![Runbook con il modulo Code](media/automation-first-runbook-graphical/runbook-startvm-get-status.png)  
16. Selezionare il collegamento di hello e nel riquadro Configurazione hello modificare **applicare una condizione di** troppo**Sì**.   Collegamento hello nota attiva riga tooa tratteggiato che indica l'attività di destinazione hello viene eseguito solo se la condizione hello risolve tootrue.  
17. Per hello **espressione di condizione**, tipo *$ActivityOutput ['Ottieni stato'] - eq "Stopped"*.  **Inizio AzureRmVM** viene eseguita solo se macchina virtuale hello è stato arrestato.
18. Nel controllo della raccolta hello, espandere **cmdlet** e quindi **utility**.
19. Aggiungere **Write-Output** canvas toohello due volte.<br> ![Runbook con Write-Output](media/automation-first-runbook-graphical/runbook-startazurermvm-complete.png)
20. In hello prima **Write-Output** controllo, fare clic su **parametri** e modificare hello **etichetta** valore troppo*notificare macchina virtuale avviata*.
21. Per **InputObject**, modificare **origine dati** troppo**espressione PowerShell** e tipo di espressione hello *"$VMName avviato correttamente."* .
22. In hello secondo **Write-Output** controllo, fare clic su **parametri** e modificare hello **etichetta** valore troppo*notificare VM Start non è riuscita*
23. Per **InputObject**, modificare **origine dati** troppo**espressione PowerShell** e tipo di espressione hello *"$VMName non è stato possibile avviare."* .
24. Creare un collegamento da **inizio AzureRmVM** troppo**notificare macchina virtuale avviata** e **notifica non riuscita di VM avviare**.
25. Selezionare il collegamento hello troppo**notificare macchina virtuale avviata** e modificare **applicare una condizione di** troppo**True**.
26. Per hello **espressione di condizione**, tipo *$ActivityOutput ['Start-AzureRmVM']. IsSuccessStatusCode - eq $true*.  Questo Write-Output il controllo viene eseguito solo se macchina virtuale hello sia stato avviato correttamente.
27. Selezionare il collegamento hello troppo**notifica non riuscita di VM avviare** e modificare **applicare una condizione di** troppo**True**.
28. Per hello **espressione di condizione**, tipo *$ActivityOutput ['Start-AzureRmVM']. IsSuccessStatusCode - ne $true*.  Questo Write-Output controllo ora solo viene eseguito se macchina virtuale hello non sia stato avviato correttamente.
29. Salvare il runbook hello e aprire il riquadro di Test hello.
30. Avviare runbook hello con macchina virtuale hello arrestato e deve iniziare.

## <a name="next-steps"></a>Passaggi successivi
* toolearn ulteriori informazioni sui grafici per la modifica, vedere [grafici per la modifica in automazione di Azure](automation-graphical-authoring-intro.md)
* tooget avviato con runbook PowerShell, vedere [il runbook prima di PowerShell](automation-first-runbook-textual-powershell.md)
* tooget avviato con runbook del flusso di lavoro di PowerShell, vedere [il primo runbook del flusso di lavoro di PowerShell](automation-first-runbook-textual.md)

