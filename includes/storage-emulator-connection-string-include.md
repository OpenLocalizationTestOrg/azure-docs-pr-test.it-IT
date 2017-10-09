emulatore di archiviazione Hello supporta un singolo account fisso e una chiave di autenticazione noto per l'autenticazione chiave condivisa. Questo account e questa chiave sono hello le credenziali di autenticazione chiave condivisa sole consentite per l'utilizzo con l'emulatore di archiviazione hello. Sono:

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> chiave di autenticazione Hello supportate dall'emulatore di archiviazione hello è destinato solo a funzionalità di hello test del codice di autenticazione client. Non viene utilizzata per eventuali scopi di sicurezza. È possibile utilizzare l'account di archiviazione di produzione e la chiave con l'emulatore di archiviazione hello. Non utilizzare account di sviluppo hello con dati di produzione.
> 
> emulatore di archiviazione Hello supporta solo la connessione tramite HTTP. Tuttavia, HTTPS è hello consigliato di protocollo per accedere alle risorse in un account di archiviazione di Azure di produzione.
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a>Connettere l'account dell'emulatore toohello utilizzando un collegamento
Hello più semplice modo tooconnect toohello emulatore di archiviazione dall'applicazione è una stringa di connessione nel file di configurazione dell'applicazione che fa riferimento il collegamento hello tooconfigure `UseDevelopmentStorage=true`. Di seguito è riportato un esempio dell'emulatore di archiviazione toohello stringa connessione in un *app* file: 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a>La connessione utilizzando la chiave e il nome di un account noto hello toohello account dell'emulatore
toocreate una stringa di connessione che riferimenti hello Nome account dell'emulatore e chiave, è necessario specificare gli endpoint hello per ognuno di hello servizi si desidera toouse dall'emulatore hello nella stringa di connessione hello. Ciò è necessario in modo che la stringa di connessione hello farà riferimento a endpoint di emulatore hello, che sono diverse da quelle per un account di archiviazione di produzione. Ad esempio, il valore di hello la stringa di connessione sarà simile al seguente:

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

Questo valore è identico toohello collegamento illustrato sopra, `UseDevelopmentStorage=true`.

#### <a name="specify-an-http-proxy"></a>Specificare un proxy HTTP
È anche possibile specificare un toouse proxy HTTP quando si verifica il servizio nell'emulatore di archiviazione hello. Questo può essere utile per l'osservazione di richieste e risposte HTTP mentre si esegue il debug di operazioni nei servizi di archiviazione hello. toospecify un proxy, aggiungere hello `DevelopmentStorageProxyUri` opzione toohello stringa di connessione e impostare il proxy toohello valore URI. Di seguito è ad esempio, una stringa di connessione che punta toohello emulatore di archiviazione e di configura un proxy HTTP:

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

