### <a name="noconnection"></a>toomodify rete locale gateway prefissi degli indirizzi IP - Nessuna connessione gateway

Se si dispone di una connessione gateway e desiderate tooadd o rimuovere i prefissi di indirizzi IP, utilizzare hello stesso comando usare gateway di rete locale hello toocreate [locale-gateway di rete az creare](https://docs.microsoft.com/cli/azure/network/local-gateway#create). È anche possibile utilizzare questo indirizzo IP del gateway comando tooupdate hello per dispositivo VPN hello. impostazioni correnti di hello toooverwrite, utilizzare nome esistente di hello del gateway di rete locale. Se si utilizza un nome diverso, si crea un nuovo gateway di rete locale, anziché sovrascrivere hello uno esistente.

È necessario specificare ogni volta che si apporta una modifica, l'elenco completo di hello di prefissi, hello non solo i prefissi che si desidera toochange. Specificare solo i prefissi di hello che si desidera tookeep. In questo caso, 10.0.0.0/24 e 20.0.0.0/24.

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --connection-name TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

### <a name="withconnection"></a>toomodify rete locale gateway prefissi di indirizzi IP - connessione gateway esistente

Se si dispone di una connessione gateway e tooadd o rimuovere i prefissi di indirizzi IP, è possibile aggiornare i prefissi di hello utilizzando [aggiornamento locale a gateway di rete az](https://docs.microsoft.com/cli/azure/network/local-gateway#update). Questo comporterà periodi di inattività per la connessione VPN. Quando si modifica l'indirizzo IP hello prefissi, non è necessario gateway VPN di hello toodelete.

È necessario specificare ogni volta che si apporta una modifica, l'elenco completo di hello di prefissi, hello non solo i prefissi che si desidera toochange. In questo esempio 10.0.0.0/24 e 20.0.0.0/24 sono già presenti. Aggiungiamo hello prefissi 30.0.0.0/24 e 40.0.0.0/24 e specificare tutti i 4 di prefissi hello durante l'aggiornamento.

```azurecli
az network local-gateway update --local-address-prefixes 10.0.0.0/24 20.0.0.0/24 30.0.0.0/24 40.0.0.0/24 --name VNet1toSite2 --connection-name TestRG1
```