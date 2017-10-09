### <a name="tooview-local-network-gateways"></a>gateway di rete locale tooview

un elenco hello gateway di rete locale, utilizzare hello tooview [elenco locale gateway di rete az](https://docs.microsoft.com/cli/azure/network/local-gateway#list) comando.

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a>valori di chiave condivisa hello tooverify

Verificare che il valore di chiave condivisa hello è hello stesso valore utilizzato per la configurazione del dispositivo VPN. In caso contrario, eseguire connessione hello utilizzando il valore di hello dal dispositivo hello o aggiornare il dispositivo di hello con valore hello hello restituito. i valori Hello devono corrispondere. chiave, utilizzare hello condivisa di hello tooview [elenco di connessioni vpn di rete az](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a>gateway VPN di hello tooview indirizzo IP pubblico

toofind hello indirizzo IP pubblico del gateway di rete virtuale, utilizzare hello [elenco public-ip di rete az](https://docs.microsoft.com/cli/azure/network/public-ip#list) comando. Per facilitare la lettura, output di hello per questo esempio è elenco hello toodisplay formattato di indirizzi IP pubblici in formato tabella.

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
