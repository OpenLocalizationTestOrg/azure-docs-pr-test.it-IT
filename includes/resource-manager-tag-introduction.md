Per applicare i tag tooyour risorse di Azure toologically organizzarli in categorie. Ogni tag è costituito da un nome e un valore. Ad esempio, è possibile applicare nome hello "Ambiente" e le risorse hello valore "Produzione" tooall hello nell'ambiente di produzione. Senza questo tag, potrebbe essere difficile stabilire se una risorsa è destinata allo sviluppo, al testing o alla produzione. "Environment" e "Production" sono solo esempi. Per definire nomi hello e valori che hello più appropriate per l'organizzazione di sottoscrizione.

Dopo aver applicato i tag, è possibile recuperare tutte le risorse di hello nella sottoscrizione con tale nome di tag e il valore. Abilita tag si tooretrieve correlati alle risorse che si trovano in gruppi di risorse diversi. Questo approccio è utile quando è necessario tooorganize risorse per la fatturazione o gestione.

Hello limitazioni seguenti si applica tootags:

* Ogni risorsa o gruppo di risorse può avere un massimo di 15 coppie nome-valore di tag. Questa limitazione si applica solo gruppo di risorse toohello tootags applicati direttamente o una risorsa. Un gruppo di risorse può contenere più risorse ognuna con 15 coppie nome-valore di tag. 
* nome del tag Hello è limitato too512 caratteri e il valore di tag hello è limitato too256 caratteri. Per gli account di archiviazione, il nome di tag hello è limitato too128 caratteri e il valore di tag hello è limitato too256 caratteri.
* Gruppo di risorse toohello tag applicati non vengono ereditati dalle risorse hello in tale gruppo di risorse. 

Se si dispone di più di 15 valori che è necessario tooassociate con una risorsa, utilizzare una stringa JSON per il valore di tag hello. stringa JSON Hello può contenere molti valori che sono applicati tooa singolo tag nome. In questo articolo viene illustrato un esempio di assegnazione di tag di toohello stringa JSON.
