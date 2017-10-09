Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando e seguire hello le direzioni. Per altre informazioni sulla registrazione, vedere [Introduzione all'interfaccia della riga di comando di Azure 2.0](/cli/azure/get-started-with-azure-cli).

```azurecli
az login
```

Se si dispone di più di una sottoscrizione di Azure, è possibile elencare le sottoscrizioni di hello per conto di hello.

```azurecli
az account list --all
```

Specificare una sottoscrizione di hello che si desidera toouse.

```azurecli
az account set --subscription <replace_with_your_subscription_id>
```