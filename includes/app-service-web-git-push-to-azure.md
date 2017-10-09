## <a name="push-tooazure-from-git"></a><span data-ttu-id="a2ab6-101">Eseguire il push tooAzure da Git</span><span class="sxs-lookup"><span data-stu-id="a2ab6-101">Push tooAzure from Git</span></span>

<span data-ttu-id="a2ab6-102">Aggiungere un repository Git locale tooyour remoto di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-102">Add an Azure remote tooyour local Git repository.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="a2ab6-103">Effettuare il push dell'app toohello toodeploy remoto di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-103">Push toohello Azure remote toodeploy your app.</span></span> <span data-ttu-id="a2ab6-104">Viene chiesto di immettere la password di hello creato in precedenza al momento della creazione utente distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-104">You are prompted for hello password you created earlier when you created hello deployment user.</span></span> <span data-ttu-id="a2ab6-105">Assicurarsi di immettere la password di hello è stato creato in [configurare un utente di distribuzione](#configure-a-deployment-user), non la password di hello utilizzati toolog in toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-105">Make sure that you enter hello password you created in [Configure a deployment user](#configure-a-deployment-user), not hello password you use toolog in toohello Azure portal.</span></span>

```bash
git push azure master
```

<span data-ttu-id="a2ab6-106">Hello comando precedente consente di visualizzare informazioni toohello simile esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="a2ab6-106">hello preceding command displays information similar toohello following example:</span></span>
