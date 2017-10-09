### <a name="tooview-local-network-gateways"></a><span data-ttu-id="9342c-101">gateway di rete locale tooview</span><span class="sxs-lookup"><span data-stu-id="9342c-101">tooview local network gateways</span></span>

<span data-ttu-id="9342c-102">un elenco hello gateway di rete locale, utilizzare hello tooview [elenco locale gateway di rete az](https://docs.microsoft.com/cli/azure/network/local-gateway#list) comando.</span><span class="sxs-lookup"><span data-stu-id="9342c-102">tooview a list of hello local network gateways, use hello [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list) command.</span></span>

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a><span data-ttu-id="9342c-103">valori di chiave condivisa hello tooverify</span><span class="sxs-lookup"><span data-stu-id="9342c-103">tooverify hello shared key values</span></span>

<span data-ttu-id="9342c-104">Verificare che il valore di chiave condivisa hello è hello stesso valore utilizzato per la configurazione del dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="9342c-104">Verify that hello shared key value is hello same value that you used for your VPN device configuration.</span></span> <span data-ttu-id="9342c-105">In caso contrario, eseguire connessione hello utilizzando il valore di hello dal dispositivo hello o aggiornare il dispositivo di hello con valore hello hello restituito.</span><span class="sxs-lookup"><span data-stu-id="9342c-105">If it is not, either run hello connection again using hello value from hello device, or update hello device with hello value from hello return.</span></span> <span data-ttu-id="9342c-106">i valori Hello devono corrispondere.</span><span class="sxs-lookup"><span data-stu-id="9342c-106">hello values must match.</span></span> <span data-ttu-id="9342c-107">chiave, utilizzare hello condivisa di hello tooview [elenco di connessioni vpn di rete az](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span><span class="sxs-lookup"><span data-stu-id="9342c-107">tooview hello shared key, use hello [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span></span>

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a><span data-ttu-id="9342c-108">gateway VPN di hello tooview indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="9342c-108">tooview hello VPN gateway Public IP address</span></span>

<span data-ttu-id="9342c-109">toofind hello indirizzo IP pubblico del gateway di rete virtuale, utilizzare hello [elenco public-ip di rete az](https://docs.microsoft.com/cli/azure/network/public-ip#list) comando.</span><span class="sxs-lookup"><span data-stu-id="9342c-109">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="9342c-110">Per facilitare la lettura, output di hello per questo esempio è elenco hello toodisplay formattato di indirizzi IP pubblici in formato tabella.</span><span class="sxs-lookup"><span data-stu-id="9342c-110">For easy reading, hello output for this example is formatted toodisplay hello list of public IPs in table format.</span></span>

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
