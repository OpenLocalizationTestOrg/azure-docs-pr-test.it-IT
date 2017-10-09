## <a name="push-tooazure-from-git"></a>Eseguire il push tooAzure da Git

Aggiungere un repository Git locale tooyour remoto di Azure.

```bash
git remote add azure <URI from previous step>
```

Effettuare il push dell'app toohello toodeploy remoto di Azure. Viene chiesto di immettere la password di hello creato in precedenza al momento della creazione utente distribuzione hello. Assicurarsi di immettere la password di hello è stato creato in [configurare un utente di distribuzione](#configure-a-deployment-user), non la password di hello utilizzati toolog in toohello portale di Azure.

```bash
git push azure master
```

Hello comando precedente consente di visualizzare informazioni toohello simile esempio seguente:
