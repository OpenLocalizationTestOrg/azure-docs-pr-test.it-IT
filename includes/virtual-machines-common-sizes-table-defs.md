
## <a name="size-table-definitions"></a>Definizioni delle tabelle delle dimensioni

- La capacità di archiviazione viene visualizzata in unità di GiB o 1.024^3 byte. Quando il confronto dei dischi espresso in GB (1000 ^ 3 byte) toodisks misurata in GiB (1024 ^ 3) tenere presente che i numeri di capacità specificati in GiB potrebbero apparire più piccoli. Ad esempio, 1.023 GiB = 1.098,4 GB
- La velocità effettiva del disco viene misurata in operazioni di input/output al secondo (IOPS) e MBps, dove il valore di MBps corrisponde a 10^6 byte al secondo.
- I dischi dati possono operare in modalità memorizzata nella cache o non memorizzata nella cache. Per l'operazione del disco dati memorizzati nella cache, la modalità cache di hello host è troppo**ReadOnly** o **ReadWrite**.  Per l'operazione del disco dati non memorizzato nella cache, la modalità cache di hello host è impostata troppo**Nessuno**.
- **Prestazioni di rete previsto** è hello aggregati larghezza di banda massima allocata per ogni tipo di macchina virtuale in tutte le schede di rete, per tutte le destinazioni. I limiti superiori non sono garantiti, ma sono indicazioni tooprovide previsto per la selezione di hello VM adatto per un'applicazione hello previsto. Le prestazioni di rete effettive dipenderanno da svariati fattori, tra cui congestione della rete, carichi dell'applicazione e impostazioni di rete. Per informazioni sull'ottimizzazione della velocità effettiva della rete, vedere [Ottimizzazione della velocità effettiva di rete per Windows e Linux](../articles/virtual-network/virtual-network-optimize-network-bandwidth.md). hello tooachieve previsto delle prestazioni di rete in Linux o Windows, potrebbe essere necessario tooselect una specifica versione o ottimizzare la macchina virtuale. Per ulteriori informazioni, vedere [come i test per la velocità effettiva di macchina virtuale tooreliably](../articles/virtual-network/virtual-network-bandwidth-testing.md).

- &#8224; 16 CPU virtuali prestazioni in modo coerente raggiungerà limite hello in una versione futura.


