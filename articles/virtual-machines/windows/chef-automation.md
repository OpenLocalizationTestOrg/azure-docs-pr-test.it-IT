---
title: distribuzione della macchina virtuale con Chef aaaAzure | Documenti Microsoft
description: Informazioni su come toouse Chef toodo automatizzata la distribuzione delle macchine virtuali e la configurazione in Microsoft Azure
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a>Automazione della distribuzione delle macchine virtuali di Azure con Chef
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Chef rappresenta uno strumento molto utile che fornisce soluzioni automatizzate e configurazioni di stato personalizzate.

Con la versione più recente di cloud api, Chef offre perfetta integrazione con Azure, offrendo hello tooprovision possibilità e distribuire gli stati di configurazione con un unico comando.

In questo articolo verrà illustrato come tooset backup il tooprovision ambiente Chef virtuali di Azure dei computer e vengono illustrati la creazione di un criterio o "Guida di riferimento" e quindi distribuire questo tooan cookbook macchina virtuale di Azure.

Verranno ora illustrate alcune nozioni di base su Chef.

## <a name="chef-basics"></a>Nozioni di base su Chef
Prima di iniziare, è consigliabile che esaminare i concetti di base hello di Chef. <a href="http://www.chef.io/chef" target="_blank">qui</a> è disponibile del materiale che sarebbe opportuno leggere rapidamente prima di tentare di eseguire la procedura. Prima di iniziare, verrà tuttavia riepilogo della nozioni di base hello.

Hello seguente diagramma viene illustrata l'architettura di Chef di alto livello hello.

![][2]

Chef ha tre componenti principali dell'architettura: Chef Workstation, Chef Server e Chef Client (nodo).

Hello Chef Server è il punto di gestione e sono disponibili due opzioni per il Chef Server hello: una soluzione ospitata o una soluzione locale. Si utilizzerà una soluzione in hosting.

Client Hello Chef (nodo) è agente hello che si trova nei server hello che si sta gestendo.

Hello Chef Workstation è la workstation di amministrazione in cui è creare i criteri e si eseguono i comandi di gestione. Esegui hello **knife** comando dalla Chef Workstation toomanage hello l'infrastruttura.

È inoltre disponibile il concetto di hello di "Cookbook" e "Soluzioni". Questi sono effettivamente criteri hello è definire e applicare tooour server.

## <a name="preparing-hello-workstation"></a>Preparare la workstation hello
In primo luogo, consente di workstation Prepara hello. Nel seguente esempio viene utilizzata una workstation Windows standard. È necessario toocreate toostore una directory del file di configurazione e guide.

Creare innanzitutto una directory denominata C:\chef.

Creare quindi una seconda directory denominata c:\chef\cookbooks.

È ora necessario toodownload il file di impostazioni di Azure affinché Chef possa comunicare con la sottoscrizione di Azure.

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
Scaricare il hello PowerShell Azure utilizzando impostazioni di pubblicazione [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) comando. 

Salvare hello di file di impostazioni di pubblicazione in C:\chef.

## <a name="creating-a-managed-chef-account"></a>Creazione di un account Chef gestito
Iscriversi per ottenere un account Chef ospitato [qui](https://manage.chef.io/signup)

Durante il processo di iscrizione hello, sarà richiesto toocreate una nuova organizzazione.

![][3]

Una volta creata l'organizzazione, è possibile scaricare hello starter kit.

![][4]

> [!NOTE]
> Se viene visualizzato un messaggio che informa che le chiavi verranno reimpostate, si tratta tooproceed ok è non disponibile alcuna infrastruttura esistente come ancora configurato.
> 
> 

Il file ZIP dello Starter Kit contiene i file di configurazione e le chiavi dell'organizzazione.

## <a name="configuring-hello-chef-workstation"></a>Configurazione della workstation Chef hello
Estrarre il contenuto di hello di hello chef starter.zip tooC:\chef.

Copiare tutti i file in starter\chef-chef-repo\.chef tooyour c:\chef directory.

La directory dovrebbe essere simile al seguente hello di esempio seguente.

![][5]

È ora incluso un file di pubblicazione Azure hello radice hello c:\chef quattro file di.

file PEM Hello contengono l'organizzazione e le chiavi private di amministratore per la comunicazione, mentre file knife hello contiene la configurazione efficace. È necessario tooedit hello knife file.

Aprire il file hello nell'editor preferito e modificare cookbook_path"hello" rimuovendo hello /... / dal percorso di hello viene visualizzato come indicato di seguito.

    cookbook_path  ["#{current_dir}/cookbooks"]

Aggiungere inoltre riflettente hello nome di Azure nelle righe seguenti hello file di impostazioni di pubblicazione.

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

Il file knife dovrebbe apparire simile toohello esempio seguente.

![][6]

Queste righe garantisce che fa riferimento a directory Cookbook hello in c:\chef\cookbooks Knife e Usa anche il file di impostazioni di pubblicazione Azure durante le operazioni di Azure.

## <a name="installing-hello-chef-development-kit"></a>L'installazione di hello Chef Development Kit
Avanti [scaricare e installare](http://downloads.getchef.com/chef-dk/windows) hello tooset ChefDK (Chef Development Kit) di Chef Workstation.

![][7]

Installare nel percorso predefinito di hello di c:\opscode. L'installazione richiederà all'incirca 10 minuti.

Verificare che la variabile PATH contenga voci relative ai percorsi C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin

Se questi percorsi non sono presenti, assicurarsi di aggiungerli.

*Nota hello ordine di hello percorso è importante!* Se i percorsi opscode non sono nell'ordine corretto hello è problemi.

Prima di continuare, riavviare la workstation.

Successivamente, verrà installato estensione Knife Azure hello. In questo modo Knife hello "Plug-in Azure".

Eseguire hello comando seguente.

    chef gem install knife-azure ––pre

> [!NOTE]
> argomento di pre-Hello garantisce che si ricevono più recente versione RC di hello di hello Knife Azure plug-in che offre accesso toohello più recente di API.
> 
> 

È probabile che un numero di dipendenze verrà installato anche in hello contemporaneamente.

![][8]

tooensure che tutto è configurato correttamente, hello esecuzione comando seguente.

    knife azure image list

Se tutto è stato configurato correttamente, verrà visualizzato un elenco delle immagini di Azure disponibili.

A questo punto impostazione di workstation Hello!

## <a name="creating-a-cookbook"></a>Creazione di un cookbook
Viene utilizzato un Cookbook da Chef toodefine un set di comandi che si desidera tooexecute nel client gestito. Creare un Cookbook è semplice e utilizziamo hello **chef generare cookbook** comando toogenerate il nostro modello Cookbook. In questo esempio il cookbook verrà denominato webserver, in quanto si desidera creare un criterio che distribuisca automaticamente IIS.

Nella directory di C:\Chef eseguire hello comando seguente.

    chef generate cookbook webserver

Verrà generato un set di file nella directory hello C:\Chef\cookbooks\webserver. È ora necessario set hello toodefine di comandi che desideriamo nostri tooexecute client Chef nella macchina virtuale gestita.

i comandi di Hello vengono archiviati in RB file hello. In questo file, sarà verranno definiti un set di comandi che viene installato IIS, IIS avvia e copia di una cartella wwwroot del modello file toohello.

Modificare il file di C:\chef\cookbooks\webserver\recipes\default.rb hello e aggiungere hello seguenti righe.

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

Dopo aver terminato, salvare file hello.

## <a name="creating-a-template"></a>Creazione di un modello
Come accennato in precedenza, è necessario un file di modello che verrà utilizzato come la pagina default.html toogenerate.

Eseguire hello seguente modello di comando toogenerate hello.

    chef generate template webserver Default.htm

Passare ora toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file. Modificare il file hello aggiungendo codice semplice "Hello World" HTML e quindi salvare il file hello.

## <a name="upload-hello-cookbook-toohello-chef-server"></a>Caricare hello Cookbook toohello Chef Server
In questo passaggio, stiamo richiede una copia di hello Cookbook che abbiamo creato il computer locale e caricarlo toohello Chef Server ospitato. Una volta caricato, hello Cookbook verrà visualizzato in hello **criteri** scheda.

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a>Distribuzione di una macchina virtuale con il comando Knife Azure
Verrà ora distribuire una macchina virtuale di Azure e applicare hello Cookbook "Server Web" che consente di installare IIS web predefinito e servizio web page.

In ordine toodo questo, utilizzare hello **server knife azure creare** comando.

Sto comando hello visualizzata del successivo.

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

i parametri di Hello sono di chiara interpretazione. Sostituire le variabili desiderate ed eseguire il comando.

> [!NOTE]
> Tramite riga di comando hello hello, sono automazione anche le regole di filtro dell'endpoint rete utilizzando il parametro – tcp endpoint hello. Dopo avere aperto le porte 80 e 3389 tooprovide toomy web pagina di accesso sessione RDP.
> 
> 

Dopo aver eseguito il comando hello, passare toohello Azure portal per visualizzare il computer iniziare tooprovision.

![][13]

prompt dei comandi di Hello viene visualizzato accanto.

![][10]

Una volta completata la distribuzione di hello, si dovrebbe essere servizio web di toohello tooconnect in grado di sulla porta 80 è fosse stata aperta la porta hello quando è stato eseguito il provisioning hello di macchina virtuale con il comando Knife Azure hello. Questa macchina virtuale è hello macchina virtuale solo il servizio cloud, sarà la connessione con l'url del servizio cloud hello.

![][11]

In questo esempio è stata impiegata una certa dose di creatività nell'uso del codice HTML.

Non dimenticare che è anche possibile connettersi tramite una sessione RDP dal portale di Azure tramite la porta 3389 hello.

Si spera che questa guida sia stata utile. Ora è possibile avviare l'infrastruttura come percorso di codice con Azure.

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->
