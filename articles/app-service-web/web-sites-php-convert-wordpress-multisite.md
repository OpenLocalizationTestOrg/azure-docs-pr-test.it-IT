---
title: aaaConvert tooMultisite di WordPress in Azure App Service
description: Informazioni su come tootake un'app web WordPress esistente viene creata attraverso la raccolta di hello in Azure e convertirlo tooWordPress multisito
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 1153f0a8043de875f081704cd0a124776758878c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="convert-wordpress-toomultisite-in-azure-app-service"></a>Convertire tooMultisite WordPress in Azure App Service
## <a name="overview"></a>Panoramica
*Autore: [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*

In questa esercitazione si apprenderà come tootake un'app web WordPress esistente creato tramite la raccolta hello in Azure e convertire in una distribuzione multisito WordPress installare. Inoltre, si apprenderà come tooassign tooeach un dominio personalizzato di hello i siti secondari all'interno dell'installazione.

Si presuppone che sia già disponibile un'installazione esistente di WordPress. In caso contrario, attenersi alla hello orientamenti di [creare un sito web WordPress dalla raccolta di hello in Azure][website-from-gallery].

La conversione di un WordPress esistente tooMultisite installazione singolo sito è in genere abbastanza semplice e molti dei passaggi iniziali di hello qui derivano direttamente da hello [creare una rete] [ wordpress-codex-create-a-network] pagina hello [WordPress Codex](http://codex.wordpress.org).

Di seguito sono riportati i requisiti iniziali.

## <a name="allow-multisite"></a>Abilitare il multisito
È necessario innanzitutto tooenable multisito tramite hello `wp-config.php` file con hello **WP\_Consenti\_MULTISITO** costante. Esistono due metodi tooedit i file di applicazione web: hello per primo è tramite FTP e hello secondo tramite Git. Se non si ha familiarità con le modalità di toosetup uno di questi metodi, consultare toohello seguenti esercitazioni:

* [PHP web site with MySQL and FTP][website-w-mysql-and-ftp-ftp-setup] (Sito Web PHP con MySQL e FTP)
* [Sito Web PHP con MySQL e Git][website-w-mysql-and-git-git-setup]

Aprire hello `wp-config.php` file con l'editor di propria scelta hello e aggiungere il seguente hello sopra hello `/* That's all, stop editing! Happy blogging. */` riga.

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

Essere che il file hello toosave e caricarlo server back-toohello!

## <a name="network-setup"></a>Configurazione della rete
Accedi toohello *-opzione amministrazione-wp* area dell'app web e si verrà visualizzato un nuovo elemento in hello **strumenti** denominata **il programma di installazione di rete**. Fare clic su **il programma di installazione di rete** e inserire hello dettagli della rete.

![Schermata di configurazione della rete][wordpress-network-setup]

Questa esercitazione viene utilizzato hello *sottodirectory* sito schema perché si prevede di configurare i domini personalizzati per ogni sito secondario in un secondo momento nell'esercitazione di hello e dovrebbe funzionare sempre. Tuttavia, dovrebbe essere possibile toosetup un sottodominio installazione se si esegue il mapping di un dominio tramite hello [portale Azure](https://portal.azure.com) e del programma di installazione con caratteri jolly DNS in modo corretto.

Per ulteriori informazioni su Visual Studio sottodominio installazioni sottodirectory vedere hello [tipi di rete multisito] [ wordpress-codex-types-of-networks] articolo su hello WordPress Codex.

## <a name="enable-hello-network"></a>Abilitare hello rete
rete Hello è ora configurato nel database di hello, ma non vi è una rete funzionalità rimanenti per passaggio tooenable hello. Finalizzare hello `wp-config.php` impostazioni e verificare `web.config` correttamente indirizza ogni sito.

Dopo aver fatto clic hello **installare** pulsante hello *il programma di installazione di rete* pagina WordPress tenterà hello tooupdate `wp-config.php` e `web.config` file. Tuttavia, è sempre necessario controllare hello file tooensure hello aggiornamenti siano stato completati. In caso contrario, questa schermata verrà visualizzata con gli aggiornamenti necessari hello. Modificare e salvare il file hello.

Dopo avere completato questi aggiornamenti sono necessari toolog out e log nuovamente nel dashboard di hello wp admin.

A questo punto occorre un altro menu sulla barra di amministrazione di hello etichettata **siti personali**. Questo menu consente toocontrol della rete tramite hello **amministratore di rete** dashboard.

## <a name="adding-custom-domains"></a>Aggiunta di domini personalizzati
Hello [WordPress MU dominio Mapping] [ wordpress-plugin-wordpress-mu-domain-mapping] plug-in rende un sito di tooany semplicissimo tooadd domini personalizzati nella rete. Affinché toooperate plug-in di hello correttamente, è necessario toodo alcune impostazioni aggiuntive in hello portale, nonché del Registrar.

## <a name="enable-domain-mapping-toohello-web-app"></a>Abilitare l'app web toohello mapping di dominio
Hello **libero** [servizio App](http://go.microsoft.com/fwlink/?LinkId=529714) piano modalità non supporta l'aggiunta di domini personalizzati tooWeb app. È necessario troppo tooswitch**Shared** o **Standard** modalità. toodo questo:

* Accedi al portale di Azure toohello e individuare l'app web. 
* Fare clic su hello **scalabilità verticale** scheda **impostazioni**.
* In **Generale** selezionare *CONDIVISO* o *STANDARD*
* Fare clic su **Save**

È possibile ricevere un messaggio che chiede modifica hello tooverify e confermare l'app web può ora addebitato un costo, in base all'utilizzo e hello altra configurazione che è impostata.

Richiede pochi secondi, le nuove impostazioni tooprocess hello, ora è un'impostazione di toostart tempestivamente il dominio.

## <a name="verify-your-domain"></a>Verifica del dominio
Prima di App Web di Azure consentirà toomap un sito di toohello di dominio, è necessario innanzitutto creare hello autorizzazione toomap hello dominio tooverify. toodo in tal caso, è necessario aggiungere una nuova voce DNS di tooyour record CNAME.

* Nella console di gestione DNS del dominio tooyour di log
* Creare un nuovo CNAME *awverify*
* Punto *awverify* troppo*awverify. YOUR_DOMAIN.azurewebsites.NET*

Potrebbe richiedere del tempo hello DNS modifiche toogo effettive completo, pertanto se hello seguendo i passaggi non funziona immediatamente, passare una tazza di caffè, quindi tornare e riprovare.

## <a name="add-hello-domain-toohello-web-app"></a>Aggiungere l'applicazione web di hello dominio toohello
Fare clic su app web tooyour restituito tramite il portale di Azure, hello **impostazioni**, quindi fare clic su **SSL e i domini personalizzati**.

Quando hello *impostazioni SSL* sono visualizzate, verranno visualizzati campi hello in cui è necessario immettere tutti i domini di hello che si desidera tooassign tooyour web app. Se un dominio non è visualizzato nell'elenco, non sarà disponibile per il mapping all'interno di WordPress, indipendentemente dalla modalità DNS del dominio hello è il programma di installazione.

![Finestra di dialogo Manage custom domains][wordpress-manage-domains]

Dopo aver digitato il dominio nella casella di testo hello, Azure verrà verificato hello record CNAME creato in precedenza. Se hello DNS non sono state propagate completamente, verrà visualizzato un indicatore rosso. Se invece l'operazione è riuscita, verrà visualizzato un segno di spunta verde. 

Prendere nota dell'indirizzo IP indicato nella parte inferiore di hello della finestra di dialogo hello hello. È necessario questo hello toosetup un record per il dominio.

## <a name="setup-hello-domain-a-record"></a>Record di un dominio hello del programma di installazione
Se hello altri passaggi sono stati completati, è possibile assegnare a questo punto hello dominio tooyour Azure web app tramite un record A DNS. 

È importante toonote qui che App web di Azure accetta sia CNAME che un record, tuttavia si *deve* utilizzare un mapping di un record tooenable dominio corretto. Un record CNAME non può essere inoltrato tooanother CNAME, che è ciò che Azure creata con YOUR_DOMAIN.azurewebsites.net.

Usa indirizzo IP hello dal passaggio precedente hello, restituire gestore DNS tooyour e hello installazione un indirizzo IP toothat toopoint record.

## <a name="install-and-setup-hello-plugin"></a>Installare e configurare il plug-in hello
La funzionalità multisito WordPress non dispone di domini personalizzati di toomap un metodo incorporato. Tuttavia, è un plug-in denominato [WordPress MU dominio Mapping] [ wordpress-plugin-wordpress-mu-domain-mapping] che aggiunge funzionalità hello automaticamente. Accedi toohello parte di amministratore di rete del sito e installare hello **WordPress MU dominio Mapping** plug-in.

Dopo l'installazione e l'attivazione di plug-in di hello, visitare **impostazioni** > **dominio Mapping** plug-in di tooconfigure hello. Nella casella di testo prima hello, *indirizzo IP del Server*, hello input indirizzo IP utilizzato toosetup hello un record per il dominio hello. Impostare qualsiasi *opzioni dominio* desiderato (impostazioni predefinite di hello spesso sono supportate) e fare clic su **salvare**.

## <a name="map-hello-domain"></a>Eseguire il mapping hello dominio
Visitare hello **Dashboard** per il sito hello desiderato toomap dominio hello. Fare clic su **strumenti** > **dominio Mapping** e tipo hello nuovo dominio nella casella di testo hello e fare clic su **Aggiungi**.

Per impostazione predefinita, il nuovo dominio di hello sarà dominio del sito di toohello riscritto generato automaticamente. Se si desidera toohave tutto il traffico inviato toohello nuovo dominio, controllare hello *dominio primario per questo blog* casella prima del salvataggio. È possibile aggiungere un numero illimitato di sito tooa domini, ma solo uno può essere principale.

## <a name="do-it-again"></a>Ripetere l'operazione
Le app Web di Azure consentono di tooadd un numero illimitato di domini tooa web app. tooadd un altro dominio sarà necessario hello tooexecute **verificare il dominio** e **del programma di installazione del record di dominio A hello** sezioni per ciascun dominio.    

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png


