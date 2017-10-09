## <a name="what-is-blob-storage"></a>Informazioni sull'archiviazione BLOB
Archiviazione Blob di Azure è un servizio per l'archiviazione di grandi quantità di dati dell'oggetto non strutturati, ad esempio dati di testo o binario, che è possibile accedere da qualsiasi in HelloWorld tramite HTTP o HTTPS. È possibile utilizzare dati tooexpose di archiviazione Blob pubblicamente toohello world o dati dell'applicazione toostore privatamente.

Quelli di seguito sono gli impieghi più comuni dell'archiviazione BLOB:

* Servizio immagini o documenti direttamente browser tooa
* Archiviazione di file per l'accesso distribuito
* Flussi audio e video
* Archiviazione di dati per backup e ripristino, ripristino di emergenza e archiviazione
* Archiviazione di dati a scopo di analisi da parte di un servizio locale o ospitato in Azure

## <a name="blob-service-concepts"></a>Concetti del servizio BLOB
servizio Blob Hello contiene hello seguenti componenti:

![Architettura BLOB](./media/storage-blob-concepts-include/blob1.png)

* **Account di archiviazione:** tutti gli accessi tooAzure archiviazione viene eseguita tramite un account di archiviazione. Questo può essere un **account di archiviazione di uso generico** o un **account di archiviazione BLOB**, specializzato per l'archiviazione di oggetti/BLOB. Per altre informazioni, vedere [Informazioni sugli account di archiviazione di Azure](../articles/storage/common/storage-create-storage-account.md).
* **Contenitore:** un contenitore è un raggruppamento di un set di BLOB. Tutti i BLOB devono trovarsi in un contenitore. In un account può esistere un numero illimitato di contenitori. In un contenitore può essere archiviato un numero illimitato di BLOB. Si noti che il nome del contenitore hello deve essere minuscole.
* **BLOB:** file di qualsiasi tipo e dimensione. Archiviazione di Azure offre tre tipi di BLOB: i BLOB in blocchi, i BLOB di pagine e i BLOB di accodamento.
  
    *BLOB in blocchi* sono ideali per l'archiviazione di file di testo o file binari, ad esempio i documenti e i file multimediali. *BLOB di aggiunta* sono BLOB tooblock simili in quanto essi sono costituiti da blocchi, ma vengono ottimizzati per le operazioni di accodamento, in modo che siano utili per gli scenari di registrazione. Un blob in blocchi singolo può contenere un massimo di too50, i blocchi 000 di too100 MB, per una dimensione totale di leggermente superiore a 4,75 TB (100 MB X 50.000). Un blob di aggiunta singolo può contenere un massimo di too50, i blocchi 000 di too4 MB, per una dimensione totale leggermente superiore 195 GB (4 MB X 50.000).
  
    *BLOB di pagine* può essere backup too1 TB in dimensioni e sono più efficienti per le operazioni frequenti in lettura/scrittura. Le Macchine virtuali di Azure utilizzano i BLOB di pagine come dischi del sistema operativo e dati.
  
    Per informazioni sulla denominazione di contenitori e BLOB, vedere l'articolo relativo alla [denominazione e riferimento a contenitori, BLOB e metadati](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).

