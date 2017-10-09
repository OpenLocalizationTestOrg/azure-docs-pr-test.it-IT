| Risorsa | Limite predefinito | Limite massimo |
| --- | --- | --- |
| VM per [sottoscrizione](../articles/billing-buy-sign-up-azure-subscription.md) |10.000<sup>1</sup> per area |10.000 per area |
| Numero totale di core della VM per ogni [sottoscrizione](../articles/billing-buy-sign-up-azure-subscription.md) |20<sup>1</sup> per area | Contattare il supporto tecnico |
| Core di VM per ogni serie (Dv2, F e così via) per ogni [sottoscrizione](../articles/billing-buy-sign-up-azure-subscription.md) |20<sup>1</sup> per area | Contattare il supporto tecnico |
| [Coamministratori](../articles/billing-add-change-azure-subscription-administrator.md) per sottoscrizione |Senza limiti |Senza limiti |
| [Account di archiviazione](../articles/storage/common/storage-create-storage-account.md) per sottoscrizione |200 |200<sup>2</sup> |
| [Gruppi di risorse](../articles/azure-resource-manager/resource-group-overview.md) per sottoscrizione |800 |800 |
| [Set di disponibilità](../articles/virtual-machines/windows/manage-availability.md#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy) per sottoscrizione |2.000 per area |2.000 per area |
| Letture API Gestione risorse |15.000 all'ora |15.000 all'ora |
| Scritture API Gestione risorse |1.200 all'ora |1.200 all'ora |
| Dimensioni delle richieste API di gestione delle risorse |4.194.304 byte |4.194.304 byte |
| Tag per sottoscrizione<sup>3</sup> |senza limiti |senza limiti |
| Calcoli di tag univoco per sottoscrizione<sup>3</sup> | 10.000 | 10.000 |
| [Servizi cloud](../articles/cloud-services/cloud-services-choose-me.md) per sottoscrizione |Non applicabile<sup>4</sup> |Non applicabile<sup>4</sup> |
| [Gruppi di affinità](../articles/virtual-network/virtual-networks-migrate-to-regional-vnet.md) per sottoscrizione |Non applicabile<sup>4</sup> |Non applicabile<sup>4</sup> |

<sup>1</sup>I limiti predefiniti variano in base al tipo di categoria di offerta, ad esempio Versione di valutazione gratuita, Pagamento in base al consumo, e al tipo di serie, ad esempio Dv2, F, G e così via.

<sup>2</sup>Sono inclusi gli account di archiviazione Standard e Premium. Se sono necessari più di 200 account di archiviazione, inviare una richiesta tramite il [supporto tecnico di Azure](https://azure.microsoft.com/support/faq/). il team di archiviazione di Azure Hello esamina il caso aziendale e può approvare too250 gli account di archiviazione.

<sup>3</sup>È possibile applicare un numero illimitato di tag per sottoscrizione. numero di Hello di tag per ogni risorsa o gruppo di risorse è limitato too15. Gestione risorse restituisce solo un [elenco di nomi di tag univoco e valori](/rest/api/resources/tags#Tags_List) nella sottoscrizione di hello quando un numero di tag hello è minore o uguale a 10.000. È comunque possibile trovare una risorsa dal tag quando il numero di hello supera i 10.000.  

<sup>4</sup>queste funzionalità sono più necessari con gruppi di risorse di Azure e hello Azure Resource Manager.

> [!NOTE]
> È importante tooemphasize core macchina virtuale con un limite totale internazionale, nonché un internazionali limite di dimensioni serie (Dv2, F, e così via) che vengono applicate separatamente.  Si consideri ad esempio una sottoscrizione con limite di core di VM totale per gli Stati Uniti orientali pari a 30, un limite di core di serie A pari a 30 e un limite di core di serie D pari a 30.  Questa sottoscrizione sia possibile usare le macchine virtuali A1 toodeploy 30 o 30 macchine virtuali D1 o una combinazione di hello due non tooexceed un totale di 30 core (ad esempio, macchine virtuali A1 10 e 20 macchine virtuali D1).  
> <!-- -->
> 
> 

