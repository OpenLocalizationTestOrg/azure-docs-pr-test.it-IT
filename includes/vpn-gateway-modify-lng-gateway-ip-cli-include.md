### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a>gateway di rete locale hello toomodify 'gatewayIpAddress'

Se il dispositivo VPN hello che si desidera tooconnect toohas modificato l'indirizzo IP pubblico, è necessario toomodify hello rete locale gateway tooreflect modificare. indirizzo IP del gateway Hello può essere modificato senza rimuovere una connessione gateway VPN esistente (se presente). indirizzo IP del gateway hello toomodify, sostituire hello i valori 'Sito2' e 'TestRG1' con la propria utilizzando hello [aggiornamento locale a gateway di rete az](https://docs.microsoft.com/cli/azure/network/local-gateway#update) comando.

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

Verificare che l'indirizzo IP hello sia corretto nella finestra di output di hello:

```
"gatewayIpAddress": "23.99.222.170",
```