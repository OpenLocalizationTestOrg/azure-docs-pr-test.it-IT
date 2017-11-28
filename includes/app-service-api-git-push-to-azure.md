<span data-ttu-id="194f9-101">Usare l'interfaccia della riga di comando di Azure per ottenere l'URL della distribuzione remota per l'app per le API.</span><span class="sxs-lookup"><span data-stu-id="194f9-101">Use the Azure CLI to get the remote deployment URL for your API App.</span></span> <span data-ttu-id="194f9-102">Nel comando seguente sostituire *\<nome_app>* con il nome dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="194f9-102">In the following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="194f9-103">Configurare la distribuzione Git locale per consentire il push nel computer remoto.</span><span class="sxs-lookup"><span data-stu-id="194f9-103">Configure your local Git deployment to be able to push to the remote.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="194f9-104">Effettuare il push all'istanza remota di Azure per distribuire l'app.</span><span class="sxs-lookup"><span data-stu-id="194f9-104">Push to the Azure remote to deploy your app.</span></span> <span data-ttu-id="194f9-105">Verrà richiesta la password creata in precedenza quando è stato creato l'utente della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="194f9-105">You are prompted for the password you created earlier when you created the deployment user.</span></span> <span data-ttu-id="194f9-106">Assicurarsi di immettere la password creata in un passaggio precedente della guida introduttiva, anziché quella usata per accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="194f9-106">Make sure that you enter the password you created in earlier in the quickstart, and not the password you use to log in to the Azure portal.</span></span>

```bash
git push azure master
```
