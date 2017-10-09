| **Risorsa** | **Limite predefinito** | **Limite massimo** |
| --- | --- | --- |
| Account Batch per area per sottoscrizione | 3 |50 |
| Core dedicati per account Batch (modalità Servizio Batch)<sup>1</sup> | 20 | N/A<sup>2</sup> |
| Core a bassa priorità per account Batch (modalità Servizio Batch)<sup>3</sup> | 50 | N/A<sup>4</sup> |
| Processi attivi e pianificazioni dei processi<sup>5</sup> per ogni account Batch | 20 | 5000<sup>6</sup> |
| Pool per account Batch | 20 | 2500 |

<sup>1</sup> quote di core dedicato visualizzate sono solo per gli account in modalità di allocazione del pool di troppo**Batch servizio**. Per gli account con la modalità di hello impostata troppo**sottoscrizione utente**, le quote di core si basano su una quota di core VM hello livello regionale o per il gruppo di macchine Virtuali nella sottoscrizione.

<sup>2</sup> hello numero di core dedicati per ogni account di Batch può essere aumentato, ma non è specificato il numero massimo di hello. Contattare il supporto Azure toodiscuss aumentare le opzioni.

<sup>3</sup> quote di core con priorità bassa visualizzate sono solo per gli account in modalità di allocazione del pool di troppo**Batch servizio**. Core con priorità bassa non sono disponibili per gli account in modalità di allocazione del pool di troppo**sottoscrizione utente**.

<sup>4</sup> hello numero di core con priorità bassa per l'account Batch può essere aumentato, ma non è specificato il numero massimo di hello. Contattare il supporto Azure toodiscuss aumentare le opzioni.

<sup>5</sup> I processi completati e le pianificazioni dei processi non sono limitati.

<sup>6</sup> supporto contattare Azure se si desidera toorequest un aumento oltre questo limite.
