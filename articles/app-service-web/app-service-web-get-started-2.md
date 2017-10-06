---
title: "app web prima di aaaAdd funzionalità tooyour | Documenti Microsoft"
description: "Aggiungere funzionalità interessanti tooyour prima web app in pochi minuti."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 542671c2-22f0-4f20-8b4b-fa477264c492
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2016
ms.author: cephalin
ms.openlocfilehash: 46c9b118c2c188508cb0a369c691a79073b7d7b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-functionality-tooyour-first-web-app"></a>Aggiungere funzionalità tooyour prima web app
In [distribuire il primo tooAzure app web in cinque minuti](app-service-web-get-started-dotnet.md), è stato distribuito un'app web di esempio per [Azure App Service](../app-service/app-service-value-prop-what-is.md). In questo articolo, aggiungerai rapidamente alcune app web di funzionalità eccellenti tooyour distribuito. In pochi minuti sarà possibile eseguire queste operazioni:

* Applicare l'autenticazione per gli utenti
* Ridimensionare automaticamente l'app
* ricevere avvisi sulle prestazioni di hello dell'app

Indipendentemente dal fatto che è stato distribuito nell'articolo precedente hello app di esempio, è possibile seguire la procedura in esercitazione hello.

Hello tre attività in questa esercitazione sono solo alcuni esempi di hello numerose funzionalità che si ottiene quando si inserisce l'app web nel servizio App. Molte delle funzionalità di hello sono disponibili in hello **libero** livello (ovvero quali la prima app web è in esecuzione nel), ed è possibile utilizzare il tootry crediti prova le funzionalità che richiedono livelli di prezzo alto. Garanzia di app web rimane in **libero** livello a meno che non si modifica in modo esplicito, tooa diverso livello di prezzo.

> [!NOTE]
> Hello web app è stato creato con l'interfaccia CLI di Azure viene eseguita nel **libero** livello, che consente solo di un'istanza di macchina virtuale condivisa con le quote di risorse. Per altre informazioni sulle risorse disponibili nel livello **Gratuito** , vedere [Limiti relativi al servizio app](../azure-subscription-service-limits.md#app-service-limits).
> 
> 

## <a name="authenticate-your-users"></a>Autenticare gli utenti
A questo punto, vediamo come è facile tooadd autenticazione tooyour app (approfondimento in [autenticazione/autorizzazione del servizio App](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)).

1. In hello portale pannello per l'app appena aperta, fare clic su **impostazioni** > **autenticazione / autorizzazione**.  
    ![Autenticazione: pannello Impostazioni](./media/app-service-web-get-started/aad-login-settings.png)
2. Fare clic su **su** tooturn sull'autenticazione.  
3. In **Provider di autenticazione** fare clic su **Azure Active Directory**.  
    ![Autenticazione: selezionare Azure AD](./media/app-service-web-get-started/aad-login-config.png)
4. In hello **impostazioni di Azure Active Directory** pannello, fare clic su **Express**, quindi fare clic su **OK**. salve le impostazioni predefinite creano una nuova applicazione Azure AD nella directory predefinita.  
    ![Autenticazione: configurazione rapida](./media/app-service-web-get-started/aad-login-express.png)
5. Fare clic su **Salva**.  
    ![Autenticazione: salvare la configurazione](./media/app-service-web-get-started/aad-login-save.png)
   
    Una volta modifica hello ha esito positivo, si noterà campanello notifica hello verde, con un messaggio descrittivo.
6. Nel pannello portale di hello dell'app, fare clic su hello **URL** collegamento (o **Sfoglia** nella barra dei menu hello). collegamento Hello è un indirizzo HTTP.  
    ![Autenticazione - Sfoglia tooURL](./media/app-service-web-get-started/aad-login-browse-click.png)  
    Ma una volta che viene aperto l'applicazione hello in una nuova scheda, hello URL di reindirizzamento casella più volte e finisce nella tua app con un indirizzo HTTPS. Si tratta è che si è già connessi tooyour sottoscrizione di Azure e è autenticato automaticamente nell'applicazione hello.  
    ![Autenticazione: accesso effettuato](./media/app-service-web-get-started/aad-login-browse-http-postclick.png)  
    Pertanto se è ora possibile aprire una sessione non autenticata in un altro browser, vedrai una schermata di accesso quando si visitano toohello stesso URL.  
    <!-- ![Authenticate - login page](./media/app-service-web-get-started/aad-login-browse.png)  -->
    Se non si è mai usato Azure Active Directory, è possibile che la directory predefinita non includa utenti di Azure AD. In tal caso, probabilmente solo account di hello in questa posizione è hello account Microsoft con la sottoscrizione di Azure. Che è il motivo per cui è stato effettuato automaticamente nell'app toohello in hello stesso browser in precedenza.
    È possibile utilizzare tale stesso toolog di account Microsoft in questa pagina account di accesso anche.

Complimenti, tutto il traffico tooyour web app per l'autenticazione.

Si può notare in hello **autenticazione / autorizzazione** pannello che è possibile eseguire molte altre, ad esempio:

* Abilitare l'accesso dai social network
* Abilitare più opzioni di accesso
* Modificare il comportamento predefinito di hello quando gli utenti passare tooyour app

Servizio App offre che una soluzione chiavi in mano per alcuni di autenticazione comuni hello deve pertanto non è necessario la logica di autenticazione hello tooprovide manualmente.
Per altre informazioni, vedere la pagina relativa all' [autenticazione/autorizzazione del servizio app](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/).

## <a name="scale-your-app-automatically-based-on-demand"></a>Ridimensionare automaticamente l'app in base alla richiesta
Successivamente, si scalabilità automatica dell'app in modo che non verrà regolato automaticamente, capacità toorespond toouser richiesta (approfondimento in [scalare in verticale l'app in Azure](web-sites-scale.md) e [scala conteggio delle istanze manualmente o automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md)).

In breve, è possibile ridimensionare l'app Web in due modi:

* [Aumentare le prestazioni](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): è possibile ottenere più CPU, memoria, spazio su disco e altre funzionalità, ad esempio macchine virtuali dedicate, domini e certificati personalizzati, slot di staging, ridimensionamento automatico e altro ancora. È la scalabilità verticale modificando hello del piano di servizio App che App appartiene al piano tariffario.
* [Scalabilità orizzontale](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): aumentare il numero di hello istanze di macchine Virtuali che eseguono l'app.
  È possibile scalare orizzontalmente tooas molte istanze di 50, a seconda del livello di prezzo.

Verrà ora configurato il ridimensionamento automatico.

1. In primo luogo, consente la scalabilità verticale per la scalabilità automatica tooenable. Nel Pannello di portale hello dell'app, fare clic su **impostazioni** > **scalabilità verticale (piano di servizio App)**.  
    ![Aumento delle prestazioni: pannello Impostazioni](./media/app-service-web-get-started/scale-up-settings.png)
2. Scorrere e seleziona hello **S1 Standard** livello, hello livello più basso che supporta la scalabilità automatica (cerchiata nella schermata), quindi fare clic su **selezionare**.  
    ![Passaggio a un piano superiore: scegliere il piano](./media/app-service-web-get-started/scale-up-select.png)
   
    Il passaggio a un piano superiore è stato completato.
   
   > [!IMPORTANT]
   > Questo piano esaurisce i crediti associati alla versione di valutazione gratuita. Se si dispone di un account a pagamento in base all'utilizzo, comporta account tooyour addebiti.
   > 
   > 
3. Ora verrà configurato il ridimensionamento automatico. Nel Pannello di portale hello dell'app, fare clic su **impostazioni** > **Scale Out (piano di servizio App)**.  
    ![Aumento del numero di istanze: pannello Impostazioni](./media/app-service-web-get-started/scale-out-settings.png)
4. Modifica **scalare** troppo**percentuale di CPU**. dispositivi di scorrimento Hello sotto l'elenco a discesa hello aggiornare di conseguenza. Definire quindi un intervallo di **Istanze** compreso tra **1** e **2** e un **Intervallo di destinazione** compreso tra **40** e **80**. Eseguire l'operazione, digitare nelle caselle hello o spostando i dispositivi di scorrimento hello.  
    ![Aumento del numero di istanze: configurare il ridimensionamento automatico.](./media/app-service-web-get-started/scale-out-configure.png)
   
    In base a questa configurazione, l'app aumenta automaticamente il numero di istanze quando l'utilizzo della CPU supera l'80% e lo riduce quando l'utilizzo della CPU scende sotto il 40%.
5. Fare clic su **salvare** nella barra dei menu hello.

Il ridimensionamento automatico dell'app è stato completato.

Si può notare in hello **delle impostazioni di scalabilità** pannello che è possibile eseguire molte altre, ad esempio:

* Ridimensionare manualmente tooa numero specifico di istanze
* Ridimensionare in base ad altre metriche delle prestazioni, ad esempio la percentuale di memoria o la coda del disco
* Personalizzare il comportamento del ridimensionamento quando viene attivata una regola per le prestazioni
* Ridimensionare automaticamente in base a una pianificazione
* Impostare il comportamento del ridimensionamento automatico per un evento futuro

Per altre informazioni sul passaggio dell'app a un piano superiore, vedere [Aumentare le prestazioni di un'app in Azure](web-sites-scale.md). Per altre informazioni sull'aumento del numero di istanze, vedere [Ridimensionare il conteggio delle istanze manualmente o automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md).

## <a name="receive-alerts-for-your-app"></a>Ricevere avvisi per l'app
Ora che l'app è il ridimensionamento automatico, cosa accade quando viene raggiunto il numero massimo di istanze hello (2) e della CPU è di sopra di utilizzo desiderato (80)?
È possibile impostare un avviso (approfondimento in [ricevere notifiche di avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)) tooinform questa situazione, in modo sarà possibile eseguire scalabilità verso l'alto o istanze dell'app, ad esempio. Ora verrà rapidamente configurato un avviso per questo scenario.

1. Nel Pannello di portale hello dell'app, fare clic su **strumenti** > **avvisi**.  
    ![Avvisi: pannello Impostazioni](./media/app-service-web-get-started/alert-settings.png)
2. Fare clic su **Aggiungi avviso**. Quindi, nel hello **risorse** casella risorsa selezionare hello che termina con **(serverfarm)**. Questo è il piano di servizio app.  
    ![Avvisi: aggiungere l'avviso per il piano di servizio app](./media/app-service-web-get-started/alert-add.png)
3. In **Nome** specificare `CPU Maxed`, in **Metrica** specificare **Percentuale CPU** e in **Soglia** specificare `90`, quindi selezionare **Invia messaggio di posta elettronica a proprietari, collaboratori e lettori** e infine fare clic su **OK**.   
    ![Avvisi: configurare l'avviso](./media/app-service-web-get-started/alert-configure.png)
   
    Al termine Azure creazione avviso hello, verrà visualizzato in hello **avvisi** blade.  
    ![Avvisi: configurazione terminata](./media/app-service-web-get-started/alert-done.png)

Ora è possibile ricevere gli avvisi.

Questa impostazione degli avvisi controlla l'utilizzo della CPU ogni cinque minuti. Se tale valore supera il 90%, si riceverà un avviso di posta elettronica, come chiunque altro sia autorizzato. toosee gli utenti autorizzati tooreceive hello avvisi, passare il pannello di portale toohello dell'app e fare clic su hello **accesso** pulsante.  
![Visualizzare chi riceve gli avvisi](./media/app-service-web-get-started/alert-rbac.png)

Si noterà che **gli amministratori delle sottoscrizioni** sono già hello **proprietario** dell'applicazione hello. Questo gruppo include è se si è amministratore dell'account hello di sottoscrizione di Azure (ad esempio, la sottoscrizione di valutazione). Per altre informazioni sul controllo degli accessi in base al ruolo di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-configure.md).

> [!NOTE]
> Regole di avviso è una funzionalità di Azure. Per altre informazioni, vedere [Ricevere notifiche di avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Nel hello tooconfigure modo avviso, si può notare un ampio set di strumenti in hello **strumenti** blade. In questo caso, è possibile risolvere i problemi, monitoraggio delle prestazioni, verificare la presenza di vulnerabilità, gestire le risorse, interagire con console macchina virtuale hello e aggiungere estensioni utili. Ti invitiamo tooclick su ognuno di questi strumenti toodiscover hello semplici ma potenti strumenti la portata di mano.

Scoprire come toodo ulteriori con l'app distribuita. Ecco un elenco parziale:

* [Acquistare e configurare un nome di dominio personalizzato](custom-dns-web-site-buydomains-web-app.md) : è possibile acquistare un dominio accattivante per l'app Web invece del dominio *.azurewebsites.net. In alternativa, è possibile usare un dominio già disponibile.
* [Configurare ambienti di gestione temporanea](web-sites-staged-publishing.md) -distribuire il tooa app URL di gestione temporanea prima di inserirli in produzione. aggiornare l'app Web live in modo affidabile e configurare una soluzione DevOps complessa con più slot di distribuzione.
* [Configurare la distribuzione continua](app-service-continuous-deployment.md): è possibile integrare lo sviluppo di app nel sistema di controllo del codice sorgente ed eseguire la distribuzione in Azure con ogni commit.
* [Accedere alle risorse locali](web-sites-hybrid-connection-get-started.md) : è possibile accedere a un database locale esistente o a un sistema CRM.
* [Eseguire il backup dell'app](web-sites-backup.md): è possibile configurare il backup e il ripristino per l'app Web e prepararsi a errori imprevisti ed eseguire il ripristino da tali errori.
* [Abilitare i log di diagnostica](web-sites-enable-diagnostic-log.md) -hello lettura IIS registra le tracce di Azure o un'applicazione. È possibile leggerli in un flusso, scaricarli o trasferirli in [Application Insights](../application-insights/app-insights-overview.md) per un'analisi pronta all'uso.
* [Analizzare l'app per cercare vulnerabilità](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) -
  È possibile analizzare l'app Web per cercare minacce attuali mediante il servizio fornito da [Tinfoil Security](https://www.tinfoilsecurity.com/).
* [Eseguire processi in background](../azure-functions/functions-overview.md) : è possibile eseguire processi per l'elaborazione di dati, la creazione di report e così via.
* [Conoscere il funzionamento del servizio app](../app-service/app-service-how-works-readme.md)

