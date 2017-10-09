### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a><span data-ttu-id="68c07-101">gateway di rete locale hello toomodify 'gatewayIpAddress'</span><span class="sxs-lookup"><span data-stu-id="68c07-101">toomodify hello local network gateway 'gatewayIpAddress'</span></span>

<span data-ttu-id="68c07-102">Se il dispositivo VPN hello che si desidera tooconnect toohas modificato l'indirizzo IP pubblico, è necessario toomodify hello rete locale gateway tooreflect modificare.</span><span class="sxs-lookup"><span data-stu-id="68c07-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="68c07-103">indirizzo IP del gateway Hello può essere modificato senza rimuovere una connessione gateway VPN esistente (se presente).</span><span class="sxs-lookup"><span data-stu-id="68c07-103">hello gateway IP address can be changed without removing an existing VPN gateway connection (if you have one).</span></span> <span data-ttu-id="68c07-104">indirizzo IP del gateway hello toomodify, sostituire hello i valori 'Sito2' e 'TestRG1' con la propria utilizzando hello [aggiornamento locale a gateway di rete az](https://docs.microsoft.com/cli/azure/network/local-gateway#update) comando.</span><span class="sxs-lookup"><span data-stu-id="68c07-104">toomodify hello gateway IP address, replace hello values 'Site2' and 'TestRG1' with your own using hello [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) command.</span></span>

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

<span data-ttu-id="68c07-105">Verificare che l'indirizzo IP hello sia corretto nella finestra di output di hello:</span><span class="sxs-lookup"><span data-stu-id="68c07-105">Verify that hello IP address is correct in hello output:</span></span>

```
"gatewayIpAddress": "23.99.222.170",
```