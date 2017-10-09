

## <a name="multi-and-single-instance-vms"></a>VM a istanza singola e a istanza multipla
Molti clienti che eseguono il numero di Azure critico che è possibile pianificare quando le proprie macchine virtuali è possibile eseguire la manutenzione pianificata a causa di tempi di inattività toohello - 15 minuti, che si verifica durante la manutenzione. Quando sottoposto a provisioning di macchine virtuali ricevono la manutenzione pianificata, è possibile utilizzare controllo toohelp set di disponibilità.

Per le VM in esecuzione in Azure sono possibili due configurazioni: a istanza singola o a istanza multipla. Le VM presenti in un set di disponibilità sono configurate a istanza multipla. Si noti che anche VM a istanza singola possono essere distribuite in un set di disponibilità, in modo che vengano considerate come macchine virtuali a istanza multipla. Le VM NON presenti in un set di disponibilità sono configurate come macchine virtuali a istanza singola.  Per informazioni dettagliate sul set di disponibilità, vedere [hello di gestire la disponibilità di macchine virtuali Windows](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [hello di gestire la disponibilità di macchine virtuali Linux](../articles/virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Toosingle istanza gli aggiornamenti di manutenzione pianificata e le macchine virtuali multi-istanza eseguita separatamente. Riconfigurare le macchine virtuali toobe a istanza singola (in tal caso multi-istanza) o toobe multi-istanza (se sono a istanza singola), è possibile controllare quando le proprie macchine virtuali visualizzato manutenzione hello pianificato. Per informazioni dettagliate sulla manutenzione pianificata delle macchine virtuali di Azure, vedere [Manutenzione pianificata per macchine virtuali Linux in Azure](../articles/virtual-machines/linux/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [Manutenzione pianificata per macchine virtuali Windows in Azure](../articles/virtual-machines/windows/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="for-multi-instance-configuration"></a>Configurazione a istanza multipla
È possibile selezionare l'ora di hello manutenzione pianificata influisce sulle macchine virtuali distribuite in una configurazione di Set di disponibilità tramite la rimozione di queste macchine virtuali dal set di disponibilità.

1. Un messaggio di posta elettronica viene inviato tooyou sette giorni prima hello pianificato manutenzione tooyour macchine virtuali in una configurazione di multi-istanza. Hello ID sottoscrizione e i nomi delle macchine virtuali multi-istanza hello interessato sono incluse nel corpo di hello del messaggio di posta elettronica hello.
2. Durante i sette giorni, è possibile scegliere ora hello le istanze vengono aggiornate rimuovendo le macchine virtuali multi-istanza in tale area dal set di disponibilità. Questa modifica in un riavvio, come macchina virtuale hello è lo spostamento da un host fisico, provoca di configurazione di destinazione per la manutenzione, l'host fisico tooanother che non è la destinazione per la manutenzione.
3. È possibile rimuovere hello VM dal relativo set di disponibilità in hello portale di Azure.

   1. Nel portale di hello selezionare hello VM tooremove hello Set di disponibilità.  

   2. In **impostazioni** fare clic su **Set di disponibilità**.

      ![Selezione del set di disponibilità](./media/virtual-machines-planned-maintenance-schedule/availabilitysetselection.png)

   3. La disponibilità di hello impostare dal menu a discesa, selezionare "Non fa parte di un set di disponibilità."

      ![Rimuovi dal set](./media/virtual-machines-planned-maintenance-schedule/availabilitysetwarning.png)

   4. Nella parte superiore di hello, fare clic su **salvare**. Fare clic su **Sì** tooacknowledge che questa azione riavvia hello macchina virtuale.

   >[!TIP]
   >È possibile riconfigurare hello toomulti-istanza di macchina virtuale in un secondo momento selezionando uno dei set di disponibilità hello elencato.

4. Macchine virtuali dal set di disponibilità sono spostati tooSingle-istanza host e non vengono aggiornate durante hello pianificato manutenzione tooAvailability impostare configurazioni.
5. Una volta completato hello aggiornamento tooAvailability impostare macchine virtuali (base descritti nel messaggio di posta elettronica originale hello tooschedule), è necessario aggiungere le macchine virtuali hello nei relativi set di disponibilità. Entrando a far parte di un set di disponibilità consente di riconfigurare le macchine virtuali hello come più istanze e comporta il riavvio. In genere, una volta completati in tutto l'ambiente Azure hello, tutti gli aggiornamenti di multi-istanza segue manutenzione a istanza singola.

È possibile rimuovere una macchina virtuale da un set di disponibilità anche usando Azure PowerShell:

```
Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Remove-AzureAvailabilitySet | Update-AzureVM
```

## <a name="for-single-instance-configuration"></a>Configurazione a istanza singola
È possibile selezionare l'ora di hello manutenzione pianificata influisce sulle è macchine virtuali in una configurazione a istanza singola mediante l'aggiunta di queste macchine virtuali nel set di disponibilità.

Procedura dettagliata

1. Un messaggio di posta elettronica viene inviato tooyou sette giorni prima hello pianificato tooVMs di manutenzione in una configurazione a istanza singola. Hello ID sottoscrizione e i nomi delle macchine virtuali a istanza singola di hello interessato sono incluse nel corpo di hello del messaggio di posta elettronica hello.
2. Durante i sette giorni, è possibile scegliere ora hello istanza riavvii aggiungendo la disponibilità di macchine virtuali a istanza singola tooan impostato in tale area stessa. Questa modifica in un riavvio, come macchina virtuale hello è lo spostamento da un host fisico, provoca di configurazione di destinazione per la manutenzione, l'host fisico tooanother che non è la destinazione per la manutenzione.
3. Seguire le istruzioni qui tooadd esistente macchine virtuali nel set di disponibilità utilizzando hello portale di Azure e Azure PowerShell. (Vedere esempio hello Azure PowerShell che segue questi passaggi.)
4. Una volta queste macchine virtuali vengono riconfigurate a istanza multipla, sono esclusi dal manutenzione pianificata hello macchine virtuali tooSingle-istanza.
5. Al termine dell'aggiornamento VM a istanza singola di hello (in base a tooschedule nel messaggio di posta elettronica originale hello), è possibile restituire le macchine virtuali di hello toosingle-istanza rimuovendo le macchine virtuali hello dei set di disponibilità.

Aggiunta di una macchina virtuale tooan anche set di disponibilità può essere ottenuta utilizzando Azure PowerShell:

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

<!--Anchors-->



<!--Link references-->
[Virtual Machines Manage Availability]: virtual-machines-windows-tutorial.md
[Understand planned versus unplanned maintenance]: virtual-machines-manage-availability.md#Understand-planned-versus-unplanned-maintenance/
