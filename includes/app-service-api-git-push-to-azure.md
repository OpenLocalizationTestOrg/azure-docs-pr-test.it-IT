Utilizzare l'URL di distribuzione remota hello di tooget di hello CLI di Azure per App per le API. In hello seguente comando, sostituire  *\<nome_app >* con il nome dell'applicazione web.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

Configurare il locale Git distribuzione toobe toopush in grado di toohello remoto.

```bash
git remote add azure <URI from previous step>
```

Effettuare il push dell'app toohello toodeploy remoto di Azure. Viene chiesto di immettere la password di hello creato in precedenza al momento della creazione utente distribuzione hello. Verificare che l'immissione di password hello creata precedenza in avvio rapido di hello e non la password di hello utilizzati toolog in toohello portale di Azure.

```bash
git push azure master
```
