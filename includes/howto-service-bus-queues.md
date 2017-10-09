## <a name="what-are-service-bus-queues"></a>Informazioni sulle code del bus di servizio
Le code del bus di servizio supportano un modello di comunicazione con **messaggistica negoziata** . Quando si usano le code, i componenti di un'applicazione distribuita non comunicano direttamente l'uno con l'altro, ma scambiano messaggi tramite una coda, che agisce da intermediario (broker). Un produttore di messaggio (mittente) passa una coda di messaggi toohello e continua l'elaborazione. In modo asincrono, un consumer di messaggi (destinatario) preleva il messaggio hello dalla coda hello e lo elabora. producer Hello non ha toowait per una risposta dal consumer hello in ordine toocontinue tooprocess e inviare altri messaggi. Le code consentono **First In, FIFO (First Out)** tooone di recapito di messaggi più consumer concorrenti. Ovvero, i messaggi vengono in genere ricevuti ed elaborati da ricevitori hello in hello ordine in cui sono stati aggiunti toohello coda e ogni messaggio viene ricevuto ed elaborato da un solo consumer di messaggi.

![Concetti relativi alle code](./media/howto-service-bus-queues/sb-queues-08.png)

Le code del bus di servizio sono una tecnologia di carattere generale che può essere usata in numerosi scenari:

* Comunicazione tra ruoli Web e di lavoro in un'applicazione Azure multilivello.
* Comunicazione tra app locali e app ospitate in Azure in una soluzione ibrida.
* Comunicazione tra componenti di un'applicazione distribuita in esecuzione in locale in organizzazioni diverse o in reparti diversi della stessa organizzazione.

Utilizzo di code consente più facilmente le applicazioni si tooscale e abilitare altre architettura tooyour di resilienza.


