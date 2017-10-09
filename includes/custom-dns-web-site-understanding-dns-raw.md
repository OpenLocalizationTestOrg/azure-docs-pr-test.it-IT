Hello sistema DNS (Domain Name) viene utilizzato toolocate risorse hello internet. Ad esempio, quando si immettere un indirizzo di app web nel browser o fare clic su un collegamento in una pagina web, utilizza dominio hello tootranslate DNS in un indirizzo IP. indirizzo IP Hello è sorta di come un indirizzo stradale, ma non è adatto molto risorse umana. Ad esempio, è molto più semplice tooremember un nome DNS come **contoso.com** rispetto al è tooremember un indirizzo IP, ad esempio 192.168.1.88 o 2001:0:4137:1f67:24a2:3888:9cce:fea3.

Hello sistema DNS si basa sul *record*. I record associano uno specifico *nome*, come **contoso.com**, a un indirizzo IP o a un altro nome DNS. Quando un'applicazione, ad esempio un web browser, ha un aspetto di un nome nel DNS, individua il record di hello e utilizza qualsiasi punta tooas hello indirizzo. Se hello valore toois punti di un indirizzo IP, tale valore verrà utilizzato il browser hello. Se invece punta tooanother il nome DNS, quindi un'applicazione hello ha risoluzione toodo nuovamente. In ultima analisi, la risoluzione del nome terminerà sempre in un indirizzo IP.

Quando si crea un'app web nel servizio App, un nome DNS viene assegnato automaticamente toohello web app. Questo nome assume forma hello  **&lt;yourwebappname&gt;. azurewebsites.net**. È inoltre un indirizzo IP virtuale disponibile per l'utilizzo per la creazione di DNS di record, pertanto è possibile creare record di tale punto di toohello **. azurewebsites.net**, oppure è possibile puntare l'indirizzo IP toohello.

> [!NOTE]
> indirizzo IP Hello dell'app web verrà modificato se si elimina e ricrea l'app web o modifica anche le modalità del piano di servizio App hello**libero** dopo che è stato impostato troppo**base**, **Shared**, o **Standard**.
> 
> 

Sono inoltre disponibili più tipi di record, ognuno con funzioni e limitazioni specifiche, ma per le app Web sono importanti solo due tipi, *A* e *CNAME*.

### <a name="address-record-a-record"></a>Record di indirizzo (record A)
Esegue il mapping, ad esempio un record A un dominio, **contoso.com** o **www.contoso.com**, *o in un dominio con caratteri jolly* , ad esempio  **\*. contoso.com**, indirizzo IP tooan. Nel caso di hello di un'app web nel servizio App, uno hello IP virtuale del servizio di hello o un indirizzo IP specifico che è stato acquistato per l'app web.

Hello principali vantaggi di un record in un record CNAME sono:

* È possibile associare un dominio radice, ad esempio **contoso.com** indirizzo IP tooan; molti Registrar che consentono solo questo utilizzo di un record
* È possibile usare un'unica voce con un carattere jolly, ad esempio **\*.contoso.com**, che gestirà le richieste per più sottodomini, ad esempio **mail.contoso.com**, **blogs.contoso.com** o **www.contso.com**.

> [!NOTE]
> Poiché viene eseguito il mapping di un record di indirizzo IP statico tooa, in grado di risolvere automaticamente le modifiche toohello indirizzo dell'app web. Viene fornito un indirizzo IP per l'utilizzo con un record quando si configurano le impostazioni di nome di dominio personalizzato per l'app web; Tuttavia, questo valore può variare se si elimina e ricrea l'app web o modifica troppo hello tooback modalità piano di servizio App**libero**.
> 
> 

### <a name="alias-record-cname-record"></a>Record alias (record CNAME)
Esegue il mapping di un record CNAME un *specifico* nome DNS, ad esempio **mail.contoso.com** o **www.contoso.com**, il nome di dominio (canonico) tooanother. Nel caso di hello di App del servizio Web App, il nome di dominio canonico hello è hello  **&lt;yourwebappname >. azurewebsites.net** nome di dominio dell'app web. Una volta creato, hello CNAME crea un alias per hello  **&lt;yourwebappname >. azurewebsites.net** nome di dominio. Hello voce CNAME risolverà l'indirizzo IP del toohello il  **&lt;yourwebappname >. azurewebsites.net** dominio nome automaticamente, se l'indirizzo IP hello dell'app web hello viene modificato, non è tootake alcuna azione.

> [!NOTE]
> Alcuni Registrar consentono solo i sottodomini toomap quando si utilizza un record CNAME, ad esempio **www.contoso.com**e non radice, nomi, ad esempio **contoso.com**. Per ulteriori informazioni sui record CNAME, vedere la documentazione di hello fornita dal registrar, <a href="http://en.wikipedia.org/wiki/CNAME_record">hello di Wikipedia sul record CNAME</a>, o hello <a href="http://tools.ietf.org/html/rfc1035">i nomi di dominio IETF - implementazione e specifiche</a> documento.
> 
> 

### <a name="web-app-dns-specifics"></a>Specifiche DNS di app Web
Uso di un record con le app Web è necessario per creare uno dei seguenti record TXT hello toofirst:

* **Per il dominio radice hello** -record TXT DNS A di  **@**  troppo  **&lt;yourwebappname&gt;. azurewebsites.net**.
* **Per un sottodominio specifico** -nome DNS A  **&lt;sottodominio >** troppo**&lt;yourwebappname&gt;. azurewebsites.net**. Ad esempio, **blog** se hello un record per **blogs.contoso.com**.
* **Per hello jolly sub-dodmains** -record TXT DNS A di * * * troppo  **&lt;yourwebappname&gt;. azurewebsites.net**.

Il record TXT è usato tooverify proprietario hello dominio che si sta tentando di toouse. Si tratta inoltre toocreating un record verso l'indirizzo IP virtuale toohello dell'app web.

È possibile trovare l'indirizzo IP hello e **. azurewebsites.net** hello nomi per l'app web eseguendo i passaggi seguenti:

1. Nel browser aprire hello [portale Azure](https://portal.azure.com).
2. In hello **App Web** pannello, fare clic sul nome dell'app web hello e quindi selezionare **i domini personalizzati** dal basso hello della pagina hello.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. In hello **i domini personalizzati** pannello, verrà visualizzato hello indirizzo IP virtuale. Salvare queste informazioni perché verranno usate durante la creazione dei record DNS
   
    ![](./media/custom-dns-web-site/virtual-ip-address.png)
   
   > [!NOTE]
   > È possibile utilizzare nomi di dominio personalizzato con un **libero** app web e aggiornare il piano di servizio App hello troppo**Shared**, **base**, **Standard**, o **Premium** livello. Per ulteriori informazioni sul servizio App hello piano di livelli di prezzo, incluso come toochange hello tariffario dell'app web, vedere [come App web tooscale](../articles/app-service-web/web-sites-scale.md).
   > 
   > 

