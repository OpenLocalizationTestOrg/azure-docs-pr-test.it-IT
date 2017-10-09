
* la conversione di Hello richiede un riavvio della macchina virtuale hello, pertanto, pianificare la migrazione di hello delle macchine virtuali in una finestra di manutenzione preesistente. 

* conversione di Hello non è reversibile. 

* Conversione di hello tootest assicurarsi di essere. Eseguire la migrazione di una macchina virtuale di test prima di eseguire la migrazione di hello nell'ambiente di produzione.

* Durante la conversione di hello, si dealloca hello macchina virtuale. Quando viene avviato dopo la conversione di hello, Hello VM riceve un nuovo indirizzo IP. Se necessario, è possibile [assegnare un indirizzo IP statico](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) toohello macchina virtuale.

* Hello dischi rigidi virtuali originali e account di archiviazione hello utilizzata da hello VM prima che la conversione non vengono eliminati. Gli addebiti tooincur continuano. tooavoid fatturati per questi elementi, eliminare i BLOB VHD originale hello dopo aver verificato che la conversione di hello è stata completata.
