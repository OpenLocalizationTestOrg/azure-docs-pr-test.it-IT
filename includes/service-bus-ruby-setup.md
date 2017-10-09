## <a name="create-a-ruby-application"></a>Creare un'applicazione Ruby
Per istruzioni, vedere [Creare un'applicazione Ruby in Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-toouse-service-bus"></a>Configurare il tooUse applicazione Bus di servizio
toouse Service Bus, scaricare e usare il pacchetto Azure Ruby hello, che include un set di librerie di praticità che comunicano con servizi REST di archiviazione hello.

### <a name="use-rubygems-tooobtain-hello-package"></a>Utilizzare un pacchetto di hello tooobtain RubyGems
1. Usare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).
2. Digitare "indicatore installa azure" dipendenze e l'indicatore di hello comando finestra tooinstall hello.

### <a name="import-hello-package"></a>Importa pacchetto di hello
Utilizzando un editor di testo, aggiungere hello seguente toohello cima hello Ruby file in cui si intende toouse archiviazione:

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a>Configurare una stringa di connessione per il bus di servizio
Esempio di codice seguente hello di utilizzare i valori hello tooset dello spazio dei nomi, nome di hello key, key, firmatario e host:

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

Impostare il valore toohello valore dello spazio dei nomi di hello che anziché l'intero URL hello è stato creato. Ad esempio, usare **"yourexamplenamespace"** e non "yourexamplenamespace.servicebus.windows.net".
