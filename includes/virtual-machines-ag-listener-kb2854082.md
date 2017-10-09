Successivamente, se tutti i server in cluster hello sono in esecuzione Windows Server 2008 R2 o Windows Server 2012, è necessario verificare tale hotfix hello [KB2854082](http://support.microsoft.com/kb/2854082) è installato in ogni server locali hello o macchine virtuali di Azure che fanno parte del cluster di hello. Qualsiasi server o una macchina virtuale che si trovano in cluster hello, ma non nel gruppo di disponibilità hello, deve essere installata la correzione.

In hello sessione desktop remoto per ognuno dei nodi del cluster hello, scaricare [KB2854082](http://support.microsoft.com/kb/2854082) tooa directory locale. Quindi, installare hotfix hello in ogni nodo del cluster in modo sequenziale. Se il servizio cluster hello è in esecuzione sul nodo del cluster hello, server hello viene riavviata alla fine di hello dell'installazione di hotfix hello.

> [!WARNING]
> L'arresto del servizio cluster hello o il riavvio hello server influisce sull'integrità del quorum hello del gruppo di disponibilità del cluster e hello e potrebbe causare il toogo cluster offline. toomaintain hello la disponibilità elevata del cluster durante l'installazione, verificare quanto segue:
> 
> * cluster Hello è l'integrità del quorum ottimale. 
> * Prima di installare l'hotfix hello su qualsiasi nodo, tutti i nodi del cluster sono online.
> * Prima di installare l'hotfix hello su qualsiasi altro nodo nel cluster hello, consentire hello hotfix installazione toorun toocompletion in un nodo, incluso il riavvio completo hello server.
> 
> 

