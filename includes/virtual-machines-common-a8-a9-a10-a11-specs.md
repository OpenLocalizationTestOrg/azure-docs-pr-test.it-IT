

## <a name="deployment-considerations"></a>Considerazioni sulla distribuzione
* **Sottoscrizione di Azure** – toodeploy più di qualche istanze con utilizzo intensivo di calcolo, prendere in considerazione una sottoscrizione prepagata o altre opzioni di acquisto. Con un [account gratuito di Azure](https://azure.microsoft.com/free/)è possibile usare solo un numero limitato di core di calcolo di Azure.

* **Determinazione dei prezzi e disponibilità** -dimensioni di queste macchine Virtuali sono disponibili solo nel piano tariffario Standard hello. Per la disponibilità nelle aree di Azure, vedere [Prodotti disponibili in base all'area] (https://azure.microsoft.com/regions/services/). 
* **Quota di core** : potrebbe essere necessario quota di core hello tooincrease nella sottoscrizione di Azure dal valore predefinito di hello. La sottoscrizione anche potrebbe limitare il numero di hello di core, che è possibile distribuire in determinati gruppi di dimensioni macchina virtuale incluso hello H serie. aumentare la quota toorequest, [aprire una richiesta di supporto clienti online](../articles/azure-supportability/how-to-create-azure-support-request.md) senza alcun costo. I limiti predefiniti possono variare in base alla categoria della sottoscrizione.
  
  > [!NOTE]
  > Se si hanno esigenze di capacità su larga scala, contattare il supporto di Azure. Le quote di Azure sono limiti di credito e non garanzie di capacità. A prescindere dalla quota, viene addebitato solo l'uso dei core effettivamente impiegati.
  > 
  > 
* **Rete virtuale** : Azure [rete virtuale](https://azure.microsoft.com/documentation/services/virtual-network/) è di istanze con utilizzo intensivo di calcolo hello toouse non necessari. Tuttavia, per molte distribuzioni, è necessario almeno una cloud basato su rete virtuale di Azure o una connessione site-to-site, se è necessario tooaccess risorse locali. Se necessario, creare una nuova rete virtuale istanze hello toodeploy. Aggiunta della rete virtuale tooa di macchine virtuali con utilizzo intensivo di calcolo in un gruppo di affinità non è supportata.
* **Ridimensionamento** : a causa delle loro hardware specializzato, è possibile ridimensionare solo istanze con utilizzo intensivo di calcolo all'interno di hello stesse dimensioni famiglia (H-series o complesse serie a). Ad esempio, è possibile ridimensionare solo una macchina virtuale serie H da una serie di H dimensioni tooanother. Inoltre, il ridimensionamento da una dimensione con utilizzo intensivo di calcolo di dimensioni non complesse tooa non è supportato.  
