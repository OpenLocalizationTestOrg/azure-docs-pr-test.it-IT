## <a name="set-up-azure-cli-for-azure-dns"></a>Configurare l'interfaccia della riga di comando di Azure per DNS di Azure

### <a name="before-you-begin"></a>Prima di iniziare

Verificare di aver hello seguenti prima di iniziare la configurazione.

* Una sottoscrizione di Azure. Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).
* Installare hello l'ultima versione di hello CLI di Azure, disponibile per Windows, Linux o Mac. Altre informazioni sono disponibile all'indirizzo [installazione hello Azure CLI](../articles/cli-install-nodejs.md).

### <a name="sign-in-tooyour-azure-account"></a>Accedi tooyour account Azure

Aprire una finestra della console ed eseguire l'autenticazione con le credenziali. Per ulteriori informazioni, vedere [Accedi tooAzure da hello CLI di Azure](../articles/xplat-cli-connect.md)

```azurecli
azure login
```

### <a name="switch-cli-mode"></a>Passare alla modalità interfaccia della riga di comando

DNS di Azure usa Gestione risorse di Azure. Accertarsi di passare i comandi CLI modalità toouse Gestione risorse di Azure.

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a>Selezionare la sottoscrizione hello

Controllare le sottoscrizioni di hello per account hello.

```azurecli
azure account list
```

Scegliere quali di toouse le sottoscrizioni di Azure.

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso Viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse. Tuttavia, poiché tutte le risorse DNS sono globali, non è regionale, scelta hello del percorso del gruppo di risorse ha alcun impatto su DNS di Azure.

Se si usa un gruppo di risorse esistente, è possibile ignorare questo passaggio.

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a>Registrare il provider di risorse

Hello servizio DNS di Azure viene gestita dal provider di risorse Microsoft. Network hello. La sottoscrizione di Azure deve essere registrato toouse questo provider di risorse prima di poter usare DNS di Azure. Questa operazione viene eseguita una sola volta per ogni sottoscrizione.

```azurecli
azure provider register --namespace Microsoft.Network
```

