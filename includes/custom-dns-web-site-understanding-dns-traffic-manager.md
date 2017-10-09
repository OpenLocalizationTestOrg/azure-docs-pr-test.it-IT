Hello sistema DNS (Domain Name) è costituito da parti toolocate utilizzati in hello internet. Ad esempio, quando si immettere un indirizzo nel browser o fare clic su un collegamento in una pagina web, utilizza dominio hello tootranslate DNS in un indirizzo IP. indirizzo IP Hello è sorta di come un indirizzo stradale, ma non è adatto molto risorse umana. Ad esempio, è molto più semplice tooremember un nome DNS come **contoso.com** rispetto al è tooremember un indirizzo IP, ad esempio 192.168.1.88 o 2001:0:4137:1f67:24a2:3888:9cce:fea3.

Hello sistema DNS si basa sul *record*. I record associano uno specifico *nome*, come **contoso.com**, a un indirizzo IP o a un altro nome DNS. Quando un'applicazione, ad esempio un web browser, ha un aspetto di un nome nel DNS, individua il record di hello e utilizza qualsiasi punta tooas hello indirizzo. Se hello valore toois punti di un indirizzo IP, tale valore verrà utilizzato il browser hello. Se invece punta tooanother il nome DNS, quindi un'applicazione hello ha risoluzione toodo nuovamente. In ultima analisi, la risoluzione del nome terminerà sempre in un indirizzo IP.

Quando si crea un sito Web di Azure, viene assegnato automaticamente un nome DNS del sito toohello. Questo nome assume forma hello  **&lt;yoursitename&gt;. azurewebsites.net**. Quando si aggiunge il sito Web come un endpoint di gestione traffico di Azure, il sito Web è quindi possibile accedere tramite hello  **&lt;yourtrafficmanagerprofile&gt;. trafficmanager.net** dominio.

> [!NOTE]
> Quando il sito Web è configurato come un endpoint di Traffic Manager, utilizzare hello **. trafficmanager.net** indirizzo durante la creazione di record DNS.
> 
> Con Gestione traffico è possibile usare unicamente record CNAME.
> 
> 

Sono inoltre più tipi di record, ciascuno con le proprie funzioni e le limitazioni, ma per siti Web configurati tooas endpoint di gestione traffico, è solo importante circa una volta; *CNAME* record.

### <a name="cname-or-alias-record"></a>Record CNAME o Alias
Esegue il mapping di un record CNAME un *specifico* nome DNS, ad esempio **mail.contoso.com** o **www.contoso.com**, il nome di dominio (canonico) tooanother. Nel caso di hello di siti Web di Azure tramite Gestione traffico, il nome di dominio canonico hello è hello  **&lt;myapp >. trafficmanager.net** nome di dominio del profilo di Traffic Manager. Una volta creato, hello CNAME crea un alias per hello  **&lt;myapp >. trafficmanager.net** nome di dominio. Hello voce CNAME risolverà l'indirizzo IP del toohello il  **&lt;myapp >. trafficmanager.net** dominio nome automaticamente, pertanto se cambia indirizzo IP di hello del sito Web di hello, non è tootake alcuna azione.

Una volta traffico arriva in Traffic Manager, quindi instrada hello tooyour siti Web, utilizzando sia configurato per metodo di bilanciamento del carico di hello. Si tratta di sito Web tooyour toovisitors completamente trasparente. Visualizzerà solo il nome di dominio personalizzato hello nel browser.

> [!NOTE]
> Alcuni Registrar consentono solo i sottodomini toomap quando si utilizza un record CNAME, ad esempio **www.contoso.com**e non radice, nomi, ad esempio **contoso.com**. Per ulteriori informazioni sui record CNAME, vedere la documentazione di hello fornita dal registrar, <a href="http://en.wikipedia.org/wiki/CNAME_record">hello di Wikipedia sul record CNAME</a>, o hello <a href="http://tools.ietf.org/html/rfc1035">i nomi di dominio IETF - implementazione e specifiche</a> documento.
> 
> 

