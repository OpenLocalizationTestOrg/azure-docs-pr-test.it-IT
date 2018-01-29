
I limiti seguenti si applicano ai Backup di Azure.

| Identificatore limite | Limite predefinito |
| --- | --- |
| Numero di server/macchine che possono essere registrati con ogni insieme di credenziali |50 per Windows Server/Client/SCDPM  <br/> 200 per le macchine virtuali IaaS |
| Dimensioni di un'origine dati per i dati archiviati nel servizio di archiviazione Azure insieme di credenziali |54400 GB max<sup>1</sup> |
| Numero di insiemi di credenziali di backup creati in ogni sottoscrizione di Azure |25 insiemi di credenziali dei servizi di ripristino per ogni area |
| Numero di volte in cui è possibile pianificare backup al giorno |3 al giorno per Windows Server/Client <br/> 2 al giorno per SCDPM <br/> Una volta al giorno per le macchine virtuali IaaS |
| Dischi dati collegati a una macchina virtuale di Azure per il backup |16 |
| Dimensione di un singolo disco dati collegato a una macchina virtuale di Azure per il backup| 1023 GB <sup>2</sup>|

* <sup>1</sup>Il limite di 54400 GB non si applica ai backup delle macchine virtuali IaaS.
* <sup>2</sup> È disponibile un'[anteprima privata](https://gallery.technet.microsoft.com/Instant-recovery-point-and-25fe398a?redir=0) per il supporto di dischi non gestiti con dimensioni fino a 4 TB. 

