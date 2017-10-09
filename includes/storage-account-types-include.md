Sono disponibili due tipi di account di archiviazione:

### <a name="general-purpose-storage-accounts"></a>Account di archiviazione di uso generico
Un consente di account di archiviazione generico accedere tooAzure servizi di archiviazione, ad esempio tabelle, code, i file, BLOB e Azure i dischi di macchina virtuale con un singolo account. Questo tipo di account di archiviazione offre due livelli di prestazioni:

* Un livello di prestazioni di archiviazione standard che consente di toostore tabelle, code, i file, BLOB e Azure dischi della macchina virtuale.
* Un livello di prestazioni di archiviazione Premium che attualmente supporta solo dischi di macchina virtuale di Azure. Per una panoramica approfondita del servizio di archiviazione Premium, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../articles/storage/common/storage-premium-storage.md) .

### <a name="blob-storage-accounts"></a>Account di archiviazione BLOB
Gli account di archiviazione BLOB sono account di archiviazione specializzati per l'archiviazione dei dati non strutturati come BLOB (oggetti) in Archiviazione di Azure. Account di archiviazione BLOB sono account di archiviazione generico esistenti tooyour simile e condividono tutti hello prestazioni, disponibilità, scalabilità e durabilità funzionalità eccellenti utilizzare oggi inclusi coerenza API 100% per i BLOB in blocchi e BLOB di aggiunta. Per applicazioni che richiedono solo archivi BLOB in blocchi o BLOB di aggiunta, è consigliabile usare account di archiviazione BLOB.

> [!NOTE]
> Gli account di archiviazione BLOB supportano solo i BLOB in blocchi e i BLOB di aggiunta, non i BLOB di pagine.
> 
> 

Account di archiviazione BLOB esporre hello **livello di accesso** attributi che possono essere specificati durante la creazione di account e modificarlo in base alle esigenze. I livelli di accesso che possono essere specificati in base al modello di accesso ai dati sono di due tipi:

* Oggetto **Hot** livello di accesso che indica che gli oggetti hello nell'account di archiviazione hello si accederà più frequentemente. In questo modo è toostore dati a un costo inferiore di accesso.
* Oggetto **sporadico** livello di accesso che indica che gli oggetti hello nell'account di archiviazione hello si accederà meno frequentemente. In questo modo è toostore dati a un costo di archiviazione di dati inferiore.

Se viene apportata una modifica nel modello di utilizzo di hello dei dati, è anche possibile passare tra questi livelli di accesso in qualsiasi momento. Modifica livello di accesso hello può comportare costi aggiuntivi. Per informazioni dettagliate, vedere [Prezzi e fatturazione per gli account di archiviazione BLOB](../articles/storage/blobs/storage-blob-storage-tiers.md#pricing-and-billing) .

Per informazioni dettagliate sugli account di archiviazione BLOB, vedere [Archivio BLOB di Azure: livelli Frequente e Sporadico](../articles/storage/blobs/storage-blob-storage-tiers.md).

Prima di poter creare un account di archiviazione, è necessario disporre di una sottoscrizione di Azure, ovvero un piano che offre accesso tooa diversi servizi di Azure. Per iniziare a usare Azure, è possibile usare un [account gratuito](https://azure.microsoft.com/pricing/free-trial/). Dopo aver deciso toopurchase un piano di sottoscrizione, è possibile scegliere tra un'ampia gamma di [le opzioni di acquisto](https://azure.microsoft.com/pricing/purchase-options/). Gli utenti [iscritti a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)ricevono crediti mensili gratuiti che possono essere usati con i servizi di Azure, incluso il servizio Archiviazione di Azure. Per informazioni sui prezzi in base al volume, vedere la pagina relativa ai [prezzi di Archiviazione di Azure ](https://azure.microsoft.com/pricing/details/storage/) .

toolearn toocreate un account di archiviazione, vedere [creare un account di archiviazione](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account) per altri dettagli. È possibile creare backup too200 denominati in modo univoco l'account di archiviazione con una singola sottoscrizione. Per informazioni dettagliate sui limiti dell'account di archiviazione, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](../articles/storage/common/storage-scalability-targets.md) .

