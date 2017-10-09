È possibile verificare che la connessione ha avuto esito positivo tramite hello [az rete-connessione vpn visualizzare](/cli/azure/network/vpn-connection#show) comando. Nell'esempio hello, '-name' fa riferimento il nome di toohello della connessione di hello che si desidera tootest. Quando la connessione hello è in corso di hello di viene stabilita, il relativo stato di connessione viene 'Connessione'. Una volta stabilita la connessione hello, lo stato di hello modifica too'Connected'.

```azurecli
az network vpn-connection show --name VNet1toSite2 --resource-group TestRG1
```

