Con Gestione risorse di Azure, si definiscono i parametri per i valori si desidera toospecify quando viene distribuito il modello di hello. modello Hello include una sezione denominata parametri che contiene tutti i valori di parametro hello.
È necessario definire un parametro per i valori che variano in base progetto hello che si distribuisce o Hello che si distribuisce ambiente di hello. Non definire parametri per i valori che saranno sempre hello stesso. Ogni valore del parametro viene utilizzato in hello toodefine di modello hello distribuire le risorse. 

Quando si definiscono i parametri, utilizzare hello **allowedValues** toospecify campo che i valori di un utente può fornire durante la distribuzione. Hello utilizzare **defaultValue** campo tooassign un parametro di valore toohello, se viene fornito alcun valore durante la distribuzione.

Si descrive ogni parametro di modello hello.

### <a name="logicappname"></a>logicAppName
nome Hello di hello logica app toocreate.

    "logicAppName": {
        "type": "string"
    }