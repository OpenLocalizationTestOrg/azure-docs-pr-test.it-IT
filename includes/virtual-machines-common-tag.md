


## <a name="tagging-a-virtual-machine-through-templates"></a>Assegnazione di tag a una macchina virtuale tramite modelli
In primo luogo, diamo un'occhiata ai tag tramite modelli. [Questo modello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) racchiude il tag su hello seguenti risorse: calcolo (macchina virtuale), di archiviazione (Account di archiviazione) e di rete (indirizzo IP pubblico, rete virtuale e l'interfaccia di rete). Questo modello riguarda una VM Windows ma può essere adattato per le VM Linux.

Fare clic su hello **distribuire tooAzure** pulsante hello [collegamento modello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags). Questo si sposterà toohello [portale di Azure](https://portal.azure.com/) in cui è possibile distribuire questo modello.

![Distribuzione semplice di tag](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

Questo modello include hello tag seguenti: *reparto*, *applicazione*, e *creato da*. È possibile aggiungere o modificare i tag direttamente nel modello di hello se si desidera che i nomi di tag diverso.

![Tag di Azure in un modello](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

Come si può notare, vengono definiti i tag di hello come coppie chiave/valore, separate da due punti (:). tag Hello devono essere definiti in questo formato:

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

Salvare il file di modello hello dopo aver completato la modifica con tag hello di propria scelta.

Successivamente, nel hello **modifica parametri** sezione, è possibile compilare i valori hello per i tag.

![Modificare i tag nel portale di Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

Fare clic su **crea** toodeploy questo modello con i valori di tag.

## <a name="tagging-through-hello-portal"></a>Assegnazione di tag tramite hello portale
Dopo aver creato le risorse con i tag, è possibile visualizzare, aggiungere ed eliminare i tag nel portale di hello.

Seleziona hello tag tooview sull'icona del tag:

![Icona di tag nel portale di Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

Aggiungere un nuovo tag tramite il portale di hello definendo la propria coppia chiave/valore e salvarlo.

![Aggiungi nuovo Tag nel portale di Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

Il nuovo tag verrà ora visualizzato nell'elenco di hello di tag per la risorsa.

![Nuovo Tag salvato nel portale di Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

