---
title: aaaHost una trascrizione nel sito Web di guide in una VM Linux | Documenti Microsoft
description: Impostare e ospitare un sito Web basato su Ruby on Rails in Azure usando una macchina virtuale Linux.
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a>Applicazione Web Ruby on Rails in una macchina virtuale di Azure
Questa esercitazione viene illustrato come toohost una trascrizione nel sito Web di guide in Azure utilizzando una macchina virtuale di Linux.  

Questa esercitazione è stata convalidata usando Ubuntu Server 14.04 LTS. Se si utilizza una distribuzione Linux diversa, potrebbe essere necessario toomodify hello passaggi tooinstall Guide.

> [!IMPORTANT]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md).  In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.
>
>

## <a name="create-an-azure-vm"></a>Creare una macchina virtuale di Azure
Iniziare creando una macchina virtuale di Azure con un'immagine Linux.

toocreate hello VM, è possibile utilizzare il portale di Azure hello o hello Azure interfaccia della riga di comando (CLI).

### <a name="azure-portal"></a>Portale di Azure
1. Sign in hello [portale di Azure](https://portal.azure.com)
2. Fare clic su **New**, quindi digitare "Ubuntu Server 14.04" nella casella di ricerca hello. Fare clic sulla voce hello restituito dalla ricerca hello. Per il modello di distribuzione di hello, selezionare **classico**, quindi fare clic su "Crea".
3. Nel Pannello di nozioni di base hello, specificare i valori per i campi necessario hello: nome (per hello VM), nome utente, tipo di autenticazione e le credenziali corrispondenti hello, sottoscrizione di Azure, gruppo di risorse e percorso.

   ![Creare una nuova immagine Ubuntu](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. Dopo il provisioning di hello VM, fare clic sul nome della macchina virtuale hello e fare clic su **endpoint** in hello **impostazioni** categoria. Trovare l'endpoint SSH hello, elencati in **autonomo**.

   ![Endpoint predefinito](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure
Seguire i passaggi di hello in [creare una macchina virtuale che esegue Linux][vm-instructions].

Dopo il provisioning di hello VM, è possibile ottenere l'endpoint SSH hello eseguendo hello comando seguente:

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a>Installare Ruby on Rails
1. Usare SSH tooconnect toohello macchina virtuale.
2. Dalla sessione SSH hello, utilizzare hello seguendo i comandi tooinstall Ruby hello VM:

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    installazione di Hello potrebbe richiedere alcuni minuti. Quando viene completato, usare hello successivo comando tooverify Ruby è installato:

        ruby -v

3. Comando che segue di hello utilizzare tooinstall Guide:

        sudo gem install rails --no-rdoc --no-ri -V

    Utilizzare hello - no-rdoc e --no-ri flag tooskip installazione della documentazione di hello, che è più veloce.
    Questo comando richiederà probabilmente tooexecute, pertanto l'aggiunta di hello -V verrà visualizzate le informazioni sullo stato dell'installazione hello molto tempo.

## <a name="create-and-run-an-app"></a>Creare ed eseguire un'applicazione
Mentre si è ancora connessi tramite SSH, eseguire hello seguenti comandi:

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

Hello [nuova](http://guides.rubyonrails.org/command_line.html#rails-new) comando crea una nuova app Guide. Hello [server](http://guides.rubyonrails.org/command_line.html#rails-server) comando Avvia hello server web WEBrick fornita con guide. (Per la produzione, è preferibile toouse un server diverso, ad esempio esclusive o passeggero.)

Verrà visualizzato il seguente toohello simili di output.

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a>Aggiungere un endpoint
1. Passare toohello [portale] [https://portal.azure.com] e selezionare la macchina virtuale.

2. Selezionare **endpoint** in hello **impostazioni** lungo pagina hello di hello bordo sinistro.

3. Fare clic su **aggiungere** nella parte superiore di hello della pagina hello.

4. In hello **aggiungere endpoint** finestra di dialogo immettere hello le seguenti informazioni:

   * **Nome**: HTTP
   * **Protocollo**: TCP
   * **Porta pubblica**: 80
   * **Porta privata**: 3000
   * **Indirizzo IP mobile**: Disabilitato
   * **Elenco di controllo di accesso - ordine**: 1001, o in un altro valore che imposta la priorità hello della regola di accesso.
   * **Elenco di controllo di accesso - Nome**: allowHTTP
   * **Elenco di controllo di accesso - Azione**: consenti
   * **Elenco di controllo di accesso - Subnet remota**: 1.0.0.0/16

     Questo endpoint dispone di una porta pubblica 80 che indirizza il traffico toohello porta privata di 3000, in cui è in ascolto server Guide hello. regola di elenco di controllo di accesso Hello consente il traffico pubblico sulla porta 80.

     ![new-endpoint](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. Fare clic su OK toosave hello endpoint.

6. Verrà visualizzato il messaggio **Salvataggio dell'endpoint della macchina virtuale**. Una volta che il messaggio scomparirà, endpoint hello è attiva. È ora possibile testare l'applicazione passando il nome DNS toohello della macchina virtuale. sito Web di Hello dovrebbe apparire simile toohello seguenti:

    ![Pagina predefinita Rails][default-rails-cloud]

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, si ha la maggior parte dei passaggi di hello manualmente. In un ambiente di produzione, è necessario scrivere la propria app in un computer di sviluppo e distribuirlo toohello macchina virtuale di Azure. Inoltre, la maggior parte degli ambienti di produzione ospitano un'applicazione hello Guide in combinazione con un altro processo server come Apache o NginX, che gestisce richieste routing toomultiple istanze di un'applicazione hello guide e serve risorse statiche. Per altre informazioni, vedere http://rubyonrails.org/deploy/.

toolearn ulteriori informazioni su Ruby su Guide, visitare hello [Ruby le guide di Guide][rails-guides].

servizi di Azure toouse dall'applicazione Ruby, vedere:

* [Archiviare dati non strutturati mediante BLOB][blobs]
* [Archiviare coppie chiave-valore mediante tabelle][tables]
* [Fornire il contenuto di larghezza di banda elevata con hello Content Delivery Network][cdn-howto]

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png
