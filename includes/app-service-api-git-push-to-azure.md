<span data-ttu-id="557d3-101">Utilizzare l'URL di distribuzione remota hello di tooget di hello CLI di Azure per App per le API.</span><span class="sxs-lookup"><span data-stu-id="557d3-101">Use hello Azure CLI tooget hello remote deployment URL for your API App.</span></span> <span data-ttu-id="557d3-102">In hello seguente comando, sostituire  *\<nome_app >* con il nome dell'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="557d3-102">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="557d3-103">Configurare il locale Git distribuzione toobe toopush in grado di toohello remoto.</span><span class="sxs-lookup"><span data-stu-id="557d3-103">Configure your local Git deployment toobe able toopush toohello remote.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="557d3-104">Effettuare il push dell'app toohello toodeploy remoto di Azure.</span><span class="sxs-lookup"><span data-stu-id="557d3-104">Push toohello Azure remote toodeploy your app.</span></span> <span data-ttu-id="557d3-105">Viene chiesto di immettere la password di hello creato in precedenza al momento della creazione utente distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="557d3-105">You are prompted for hello password you created earlier when you created hello deployment user.</span></span> <span data-ttu-id="557d3-106">Verificare che l'immissione di password hello creata precedenza in avvio rapido di hello e non la password di hello utilizzati toolog in toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="557d3-106">Make sure that you enter hello password you created in earlier in hello quickstart, and not hello password you use toolog in toohello Azure portal.</span></span>

```bash
git push azure master
```
