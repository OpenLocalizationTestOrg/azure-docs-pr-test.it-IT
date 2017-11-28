## <a name="push-to-azure-from-git"></a><span data-ttu-id="6ec71-101">Effettuare il push in Azure da Git</span><span class="sxs-lookup"><span data-stu-id="6ec71-101">Push to Azure from Git</span></span>

<span data-ttu-id="6ec71-102">Aggiungere un'istanza remota di Azure al repository Git locale.</span><span class="sxs-lookup"><span data-stu-id="6ec71-102">Add an Azure remote to your local Git repository.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="6ec71-103">Effettuare il push all'istanza remota di Azure per distribuire l'app.</span><span class="sxs-lookup"><span data-stu-id="6ec71-103">Push to the Azure remote to deploy your app.</span></span> <span data-ttu-id="6ec71-104">Verrà richiesta la password creata in precedenza quando è stato creato l'utente della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="6ec71-104">You are prompted for the password you created earlier when you created the deployment user.</span></span> <span data-ttu-id="6ec71-105">Assicurarsi di immettere la password creata in [Configurare un utente della distribuzione](#configure-a-deployment-user), anziché quella usata per accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6ec71-105">Make sure that you enter the password you created in [Configure a deployment user](#configure-a-deployment-user), not the password you use to log in to the Azure portal.</span></span>

```bash
git push azure master
```

<span data-ttu-id="6ec71-106">Il comando precedente restituisce informazioni simili all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6ec71-106">The preceding command displays information similar to the following example:</span></span>
