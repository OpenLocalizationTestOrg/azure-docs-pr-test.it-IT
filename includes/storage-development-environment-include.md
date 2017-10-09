## <a name="set-up-your-development-environment"></a>Configurazione dell'ambiente di sviluppo
Successivamente, configurare l'ambiente di sviluppo in Visual Studio in modo da essere pronti tootry esempi di codice hello in questa Guida.

### <a name="create-a-windows-console-application-project"></a>Creare un progetto di applicazione console di Windows
In Visual Studio creare una nuova applicazione console di Windows. Hello alla procedura seguente viene illustrato come toocreate un'applicazione console in Visual Studio 2017, tuttavia, i passaggi di hello sono simili in altre versioni di Visual Studio.

1. Selezionare **File** > **Nuovo** > **Progetto**
2. Selezionare **Installati** > **Modelli** > **Visual C#** > **Desktop classico di Windows**
3. Selezionare **App console (.NET Framework)**
4. Immettere un nome per l'applicazione in hello **nome:** campo
5. Selezionare **OK**.

![Finestra di dialogo di creazione del progetto in Visual Studio](./media/storage-development-environment-include/storage-development-environment-include-1.png)

Tutti gli esempi di codice in questa esercitazione è possibile aggiungere toohello `Main()` metodo dell'applicazione console `Program.cs` file.

È possibile usare Azure Storage Client Library hello in qualsiasi tipo di applicazione .NET, tra cui un'app web o servizio di cloud di Azure e le applicazioni desktop e mobile. Per semplicità, in questa guida si usa un'applicazione console.

### <a name="use-nuget-tooinstall-hello-required-packages"></a>Utilizzare i pacchetti hello necessario tooinstall NuGet
Sono disponibili due pacchetti, è necessario tooreference in toocomplete il progetto in questa esercitazione:

* [Microsoft Azure Storage Client Library per .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): questo pacchetto fornisce l'accesso programmatico toodata risorse nell'account di archiviazione.
* [Libreria Gestione configurazione di Microsoft Azure per .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): questo pacchetto fornisce una classe per l'analisi di una stringa di connessione in un file di configurazione, indipendentemente dalla posizione in cui viene eseguita l'applicazione.

È possibile utilizzare NuGet tooobtain entrambi i pacchetti. A tale scopo, seguire questa procedura:

1. Fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** e scegliere **Gestisci pacchetti NuGet**.
2. Cercare online "Windowsazure" e fare clic su **installare** tooinstall hello libreria Client di archiviazione e le relative dipendenze.
3. Cercare online "WindowsAzure.ConfigurationManager" e fare clic su **installare** tooinstall hello Azure Configuration Manager.

> [!NOTE]
> pacchetto libreria Client di archiviazione Hello è incluso anche in hello [Azure SDK per .NET](https://azure.microsoft.com/downloads/). Tuttavia, è consigliabile installare anche hello libreria Client di archiviazione da NuGet tooensure che siano sempre più recente della libreria client hello hello.
> 
> le dipendenze ODataLib Hello hello libreria Client di archiviazione per .NET vengono risolti da pacchetti ODataLib hello disponibili su NuGet, non da WCF Data Services. le librerie ODataLib Hello possono essere scaricate direttamente o a cui fa riferimento al progetto di codice attraverso NuGet. pacchetti ODataLib specifici Hello utilizzati da hello libreria Client di archiviazione sono [OData](http://nuget.org/packages/Microsoft.Data.OData/), [Edm](http://nuget.org/packages/Microsoft.Data.Edm/), e [spaziale](http://nuget.org/packages/System.Spatial/). Queste librerie vengono usati dalle classi di archiviazione Azure Table hello, sono le dipendenze necessarie per la programmazione con hello libreria Client di archiviazione.
> 
> 

### <a name="determine-your-target-environment"></a>Determinare l'ambiente di destinazione
Sono disponibili due opzioni di ambiente per l'esecuzione di esempi di hello in questa guida:

* È possibile eseguire il codice con un account di archiviazione di Azure nel cloud hello. 
* È possibile eseguire il codice nell'emulatore di archiviazione Azure hello. emulatore di archiviazione Hello è un ambiente locale che emula un account di archiviazione di Azure nel cloud hello. emulatore Hello è un'opzione disponibile per il test e debug del codice, mentre l'applicazione è in fase di sviluppo. emulatore di Hello utilizza un account noto e una chiave. Per ulteriori informazioni, vedere [hello Usa emulatore di archiviazione di Azure per sviluppo e test](../articles/storage/common/storage-use-emulator.md)

Se la destinazione è un account di archiviazione nel cloud hello, copiare la chiave di accesso primaria hello dell'account di archiviazione da hello portale di Azure. Per altre informazioni, vedere [Gestire le chiavi di accesso alle risorse di archiviazione](../articles/storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).

> [!NOTE]
> È possibile destinare tooavoid emulatore di archiviazione hello sostenere i costi di archiviazione di Azure. Tuttavia, se si sceglie tootarget un account di archiviazione di Azure nel cloud hello, i costi per l'esecuzione di questa esercitazione sarà trascurabili.
> 
> 

### <a name="configure-your-storage-connection-string"></a>Configurare la stringa di connessione di archiviazione
Hello Azure Storage Client Library per .NET supporta l'utilizzo di un endpoint di tooconfigure stringa di connessione archiviazione e le credenziali per l'accesso ai servizi di archiviazione. Hello migliore modo toomaintain la stringa di connessione di archiviazione è in un file di configurazione. 

Per ulteriori informazioni sulle stringhe di connessione, vedere [configurare tooAzure una stringa di connessione archiviazione](../articles/storage/common/storage-configure-connection-string.md).

> [!NOTE]
> La chiave di account di archiviazione è simile toohello radice la password dell'account di archiviazione. Essere sempre attenzione tooprotect la chiave di account di archiviazione. Evitare di distribuirlo agli utenti di tooother a livello di codice, e salvarlo in un file di testo che è accessibile tooothers. Rigenerare la chiave usando hello portale di Azure, se si ritiene che potrebbero essere state compromesse.
> 
> 

tooconfigure la stringa di connessione, aprire hello `app.config` file da Esplora soluzioni in Visual Studio. Aggiungere contenuto hello di hello `<appSettings>` elemento riportato di seguito. Sostituire `account-name` con nome hello dell'account di archiviazione, e `account-key` con la chiave di accesso account:

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key" />
    </appSettings>
</configuration>
```

Ad esempio, l'impostazione di configurazione si presenta simile a:

```xml
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=GMuzNHjlB3S9itqZJHHCnRkrokLkcSyW7yK9BRbGp0ENePunLPwBgpxV1Z/pVo9zpem/2xSHXkMqTHHLcx8XRA==" />
```

emulatore di archiviazione hello tootarget, è possibile utilizzare un collegamento che esegue il mapping delle chiavi e il nome di un account noto toohello. In questo caso, l'impostazione della stringa di connessione è:

```xml
<add key="StorageConnectionString" value="UseDevelopmentStorage=true;" />
```

