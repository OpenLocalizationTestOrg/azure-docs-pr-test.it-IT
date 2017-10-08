---
title: una pipeline CI/CD-ROM in Azure con Team Services aaaCreate | Documenti Microsoft
description: Informazioni su come pipeline di toocreate un Visual Studio Team Services per l'integrazione continua e recapito che distribuisce un tooIIS app web in una macchina virtuale Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a>Creare una pipeline di integrazione continua con Visual Studio Team Services e IIS
tooautomate hello compilazione, test e le fasi di distribuzione dello sviluppo di applicazioni, è possibile utilizzare un'integrazione continua e la pipeline di distribuzione (CI/CD). In questa esercitazione viene creata una pipeline CI/CD tramite Visual Studio Team Services e una macchina virtuale Windows in Azure che esegue IIS. Si apprenderà come:

> [!div class="checklist"]
> * Pubblicare un progetto di Team Services tooa applicazione web ASP.NET
> * creare una definizione di compilazione che viene attivata dal commit del codice
> * installare e configurare IIS su una macchina virtuale in Azure
> * Aggiungi gruppo di distribuzione tooa istanze IIS hello in Team Services
> * Creare un nuovo web toopublish definizione versione distribuire pacchetti tooIIS
> * Testare hello CI/CD pipeline

Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo. Eseguire `Get-Module -ListAvailable AzureRM` versione hello toofind. Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).


## <a name="create-project-in-team-services"></a>Creare un progetto in Team Services
Visual Studio Team Services consente per uno sviluppo e una collaborazione facilitata senza mantenere una soluzione di gestione del codice in locale. Team Services offre i test sul codice cloud, compilazione e informazioni approfondite sull'applicazione. È possibile scegliere l'archivio di controllo della versione e l'IDE che meglio si adatta allo sviluppo del codice. Per questa esercitazione, è possibile utilizzare un account gratuito toocreate un'app web ASP.NET base e pipeline CI/CD-ROM. Se non si dispone già di un account Team Services, [crearne uno](http://go.microsoft.com/fwlink/?LinkId=307137).

processo di commit codice hello toomanage, definizioni di compilazione e rilasciare le definizioni, creare un progetto Team Services, come indicato di seguito:

1. Aprire il dashboard di Team Services in un browser Web e scegliere **Nuovo progetto**.
2. Immettere *myWebApp* per hello **nome progetto**. Lasciare tutti gli altri toouse di valori predefinito *Git* controllo della versione e *Agile* processo elemento di lavoro.
3. Opzione di hello troppo**condividere con** *i membri del Team*, quindi selezionare **crea**.
5. Dopo aver creato il progetto, scegliere opzione hello troppo**inizializzare con un file Leggimi o gitignore**, quindi **inizializzare**.
6. All'interno del nuovo progetto, scegliere **dashboard** in alto di hello, quindi selezionare **aperta in Visual Studio**.


## <a name="create-aspnet-web-application"></a>Creare un'applicazione Web ASP.NET
Nel passaggio precedente hello, è stato creato un progetto Team Services. passaggio finale Hello apre il nuovo progetto in Visual Studio. Per gestire il commit di codice hello **Team Explorer** finestra. Creare una copia locale del nuovo progetto, quindi creare un'applicazione Web ASP.NET da un modello, come indicato di seguito:

1. Selezionare **Clone** toocreate un repository git locale del progetto Team Services.
    
    ![Clonare l'archivio dal progetto Team Services](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. In **Soluzioni** selezionare **Nuovo**.

    ![Creare una soluzione per l'applicazione Web](media/tutorial-vsts-iis-cicd/new_solution.png)

3. Selezionare **Web** modelli, quindi scegliere hello **applicazione Web ASP.NET** modello.
    1. Immettere un nome per l'applicazione, ad esempio *myWebApp*e deselezionare la casella di hello per **Crea directory per soluzione**.
    2. Se l'opzione hello è disponibile, deselezionare la casella di hello troppo**Aggiungi Application Insights tooproject**. Application Insights, è necessario per l'applicazione web con Azure Application Insights è tooauthorize. tookeep è semplice in questa esercitazione, ignorare questo processo.
    3. Selezionare **OK**.
4. Scegliere **MVC** dall'elenco di modelli di hello.
    1. Selezionare **Modifica autenticazione**, scegliere **No Authentication** (Nessuna autenticazione), quindi selezionare **OK**.
    2. Selezionare **OK** toocreate la soluzione.
5. In hello **Team Explorer** finestra, scegliere **modifiche**.

    ![Eseguire il commit di repository git di servizi tooTeam modifiche locali](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. Nella casella di testo hello commit, immettere un messaggio, ad esempio *commit iniziale*. Scegliere **tutti il Commit e sincronizzazione** dal menu a discesa hello.


## <a name="create-build-definition"></a>Creare una definizione di compilazione
In Team Services, si utilizza un toooutline di definizione di compilazione come l'applicazione deve essere compilato. In questa esercitazione viene creata una definizione di base che accetta il codice sorgente, compilare la soluzione hello, quindi crea web distribuisce pacchetto è possibile utilizzare toorun hello web app in un server IIS.

1. Nel progetto Team Services, scegliere **compilazione & versione** in alto di hello, quindi selezionare **compilazioni**.
3. Selezionare **+ Nuova definizione**.
4. Scegliere hello **ASP.NET (anteprima)** modello e selezionare **applica**.
5. Lasciare l'impostazione predefinita, tutti hello i valori delle attività. In **Ottieni origini**, verificare che hello *myWebApp* repository e *master* branch è selezionato.

    ![Creare la definizione di compilazione nel progetto Team Services](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. In hello **trigger** spostare hello dispositivo di scorrimento per **attiva trigger** troppo*abilitato*.
7. Salvare la definizione di compilazione hello e coda di una nuova compilazione selezionando **Salva e coda** , quindi **Salva e coda** nuovamente. Lasciare le impostazioni predefinite hello e selezionare **coda**.

Espressioni di controllo come compilazione hello viene pianificata su un agente ospitato, quindi avvia toobuild. Hello l'output è simile toohello seguente esempio:

![Completamento della compilazione del progetto Team Services](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a>Crea macchina virtuale
tooprovide toorun una piattaforma app web ASP.NET, è necessario che una macchina virtuale di Windows che esegue IIS. Team Services utilizza toointeract un agente con l'istanza IIS hello come si esegue il commit di codice e vengono attivate le compilazioni.

Creare rapidamente una macchina virtuale Windows Server 2016 tramite [questo esempio di script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json). Accetta alcuni minuti per toorun script hello e creare hello macchina virtuale. Dopo aver creato hello macchina virtuale, aprire la porta 80 per il traffico web con [Aggiungi AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) come indicato di seguito:

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

tooconnect tooyour macchina virtuale, ottenere l'indirizzo IP pubblico hello con [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) come indicato di seguito:

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

Creare una macchina virtuale di tooyour sessione desktop remoto:

```cmd
mstsc /v:<publicIpAddress>
```

In hello macchina virtuale, aprire un **amministratore PowerShell** prompt dei comandi. Installare IIS e le funzionalità .NET necessarie come segue:

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a>Creare un gruppo di distribuzione
toopush out web hello server IIS toohello del pacchetto di distribuzione, si definisce un gruppo di distribuzione in Team Services. Questo gruppo consente toospecify quali server sono hello di nuove compilazioni come si esegue il commit di codice tooTeam servizi e le compilazioni vengono completate.

1. In Team Services scegliere **Build & Release** (Compilazione e versione) e quindi selezionare **Gruppi di distribuzione**.
2. Scegliere **Aggiungi gruppo di distribuzione**.
3. Immettere un nome per il gruppo di hello, ad esempio *myIIS*, quindi selezionare **crea**.
4. In hello **registrare macchine** sezione, verificare *Windows* è selezionata, quindi la casella hello troppo**utilizzare un token di accesso personali nello script hello per l'autenticazione**.
5. Selezionare **copiare script tooclipboard**.


### <a name="add-iis-vm-toohello-deployment-group"></a>Aggiungere il gruppo di distribuzione di VM IIS toohello
Con il gruppo di distribuzione hello creato, aggiungere ogni gruppo toohello istanza IIS. Team Services genera uno script che scarica e configura un agente su hello macchina virtuale che riceve di nuovo web di distribuire pacchetti che viene quindi applicato tooIIS.

1. In hello **amministratore PowerShell** sessione nella VM, incollare ed eseguire script hello copiato dal Team Services.
2. Quando il tag tooconfigure richiesta per l'agente di hello, scegliere *Y* e immettere *web*.
3. Quando richiesto per l'account utente di hello, premere *restituire* tooaccept hello predefinite.
4. Attendere hello toofinish di script con un messaggio *vstsagent.account.computername servizio è stato avviato correttamente*.
5. In hello **gruppi di distribuzione** pagina di hello **compilazione & versione** del menu aprirlo hello *myIIS* gruppo di distribuzione. In hello **macchine** scheda, verificare che la macchina virtuale sia elencata.

    ![Macchina virtuale è stato aggiunto gruppo di distribuzione di servizi tooTeam](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a>Creare una definizione della versione
toopublish le compilazioni, si crea una definizione di versione in Team Services. Questa definizione viene attivata automaticamente dalla corretta compilazione dell'applicazione. Scegliendo hello distribuzione gruppo toopush pacchetto di distribuzione web e definire le impostazioni di IIS appropriate hello.

1. Scegliere **Build & Release** (Compilazione e versione), quindi selezionare **Compilazioni**. Scegliere una definizione di compilazione hello creato in un passaggio precedente.
2. In **completati di recente**, scegliere la compilazione più recente di hello, quindi selezionare **versione**.
3. Scegliere **Sì** toocreate una definizione di versione.
4. Scegliere hello **vuoto** modello, quindi selezionare **Avanti**.
5. Verificare la definizione di compilazione progetto e di origine hello vengono popolati con il progetto.
6. Seleziona hello **distribuzione continua** casella di controllo, quindi selezionare **crea**.
7. Selezionare la casella di riepilogo hello troppo Avanti**+ Aggiungi attività** e scegliere *aggiungere una fase di distribuzione gruppo*.
    
    ![Definizione di attività toorelease componente aggiuntivo di Team Services](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. Scegliere **Aggiungi** Avanti troppo**Deploy(Preview) App Web di IIS**, quindi selezionare **Chiudi**.
9. Seleziona hello **esecuzione nel gruppo di distribuzione** attività padre.
    1. Per **gruppo distribuzione**, selezionare la distribuzione di hello gruppo creato in precedenza, ad esempio *myIIS*.
    2. In hello **computer tag** , quindi selezionare **Aggiungi** scegliere hello *web* tag.
    
    ![Attività del gruppo di distribuzione della definizione di versione per IIS](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. Seleziona hello **distribuzione: distribuzione di App Web IIS** tooconfigure attività di IIS istanza impostazioni come segue:
    1. Per **Nome del sito Web**, immettere *Sito Web predefinito*.
    2. Lasciare hello tutte le altre impostazioni predefinite.
12. Scegliere **Slava**, quindi selezionare **OK** due volte.


## <a name="create-a-release-and-publish"></a>Creare e pubblicare una versione
È ora possibile effettuare il push del pacchetto di distribuzione Web come una nuova versione. Questo passaggio comunica con l'agente di hello in ogni istanza che fa parte del gruppo di distribuzione hello, inserisce web hello distribuire il pacchetto, quindi Configura applicazione web IIS toorun hello aggiornato.

1. Nella definizione di versione selezionare **+ Release** (+ Versione), quindi scegliere **Crea versione**.
2. Verificare che la build più recente di hello sia selezionata nell'elenco a discesa hello, insieme a **distribuzione automatizzata: dopo la creazione della versione**. Selezionare **Crea**.
3. Un banner di piccole dimensioni viene visualizzata nella parte superiore di hello della definizione di versione, ad esempio *versione 'Versione 1' è stato creato*. Collegamento di versione di hello selezionare.
4. Aprire hello **registri** scheda stato versione di hello toowatch.
    
    ![Push del pacchetto di distribuzione Web e versione di Team Services corretti](media/tutorial-vsts-iis-cicd/successful_release.png)

5. Una volta completata la versione hello, aprire un web browser e immettere l'indirizzo PIP pubblico hello della macchina virtuale. L'applicazione Web ASP.NET è in esecuzione.

    ![App web ASP.NET in esecuzione sulla macchina virtuale IIS](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a>Testare hello intero CI/CD pipeline
L'applicazione web in esecuzione in IIS, provare pipeline CI/CD intera hello. Dopo aver apportato una modifica in Visual Studio e commit viene attivato il codice, una compilazione che quindi attiva una versione del web aggiornata distribuire tooIIS pacchetto:

1. In Visual Studio, aprire hello **Esplora** finestra.
2. Passare tooand open *myWebApp | Viste | Home | Cshtml*
3. Modifica riga 6 tooread:

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. Salvare il file hello.
5. Aprire hello **Team Explorer** finestra, seleziona hello *myWebApp* del progetto, quindi scegliere **modifiche**.
6. Immettere un messaggio di commit, ad esempio *test CI/CD pipeline*, quindi scegliere **tutti i Commit e sincronizzazione** dal menu a discesa hello.
7. Nell'area di lavoro di Team Services, viene attivata una nuova compilazione dal commit di codice hello. 
    - Scegliere **Build & Release** (Compilazione e versione), quindi selezionare **Compilazioni**. 
    - Scegliere la definizione di compilazione, quindi selezionare hello **in coda & esecuzione** toowatch compilazione come hello compilare l'avanzamento.
9. Una volta compilazione hello ha esito positivo, viene attivata una nuova versione.
    - Scegliere **compilazione & versione**, quindi **versioni** pacchetto inserito tooyour VM IIS di distribuzione web di hello toosee. 
    - Seleziona hello **aggiornamento** stato hello tooupdate di icona. Quando hello *ambienti* colonna viene visualizzato un segno di spunta verde, versione di hello è distribuita correttamente tooIIS.
11. applicare le modifiche toosee, aggiornare il sito Web IIS in un browser.

    ![App web ASP.NET in esecuzione sulla macchina virtuale IIS dalla pipeline CI/CD](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è creata un'applicazione web ASP.NET in Team Services e compilazione configurata e versione definizioni toodeploy nuova distribuzione web tooIIS di pacchetti in ogni caso di commit di codice. Si è appreso come:

> [!div class="checklist"]
> * Pubblicare un progetto di Team Services tooa applicazione web ASP.NET
> * creare una definizione di compilazione che viene attivata dal commit del codice
> * installare e configurare IIS su una macchina virtuale in Azure
> * Aggiungi gruppo di distribuzione tooa istanze IIS hello in Team Services
> * Creare un nuovo web toopublish definizione versione distribuire pacchetti tooIIS
> * Testare hello CI/CD pipeline

Spostare toolearn esercitazione successiva toohello come toosecure un server web con i certificati SSL.

> [!div class="nextstepaction"]
> [Secure web server with SSL (Proteggere il server Web con SSL)](tutorial-secure-web-server.md)