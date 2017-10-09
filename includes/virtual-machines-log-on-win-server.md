1. Facendo clic su **Connetti** si crea e si scarica un file Remote Desktop Protocol (file con estensione rdp). Fare clic su **aprire** toouse questo file.
2. Verrà visualizzato un avviso che RDP hello è da un editore sconosciuto. Si tratta di una situazione normale. Nella finestra di hello Desktop remoto, fare clic su **Connetti** toocontinue.
   
    ![Screenshot di un avviso relativo a un autore sconosciuto.](./media/virtual-machines-log-on-win-server/rdp-warn.png)
3. In hello **la sicurezza di Windows** , digitare le credenziali di hello per un account nella macchina virtuale hello e quindi fare clic su **OK**.
   
     **Account locale** -si tratta in genere LocalAccount hello nome utente e la password specificata al momento della creazione hello macchina virtuale. In questo caso, il dominio hello è il nome di hello della macchina virtuale hello e viene inserito come *vmname*&#92; *nome utente*.  
   
    **Aggiunto a un dominio VM** - se hello VM appartiene tooa dominio, immettere nome utente hello in formato hello *dominio*&#92; *Nome utente*. è inoltre necessario account Hello tooeither essere amministratori hello gruppo o sono state concesse toohello privilegi di accesso remoto macchina virtuale.
   
    **Controller di dominio** - se hello VM è un controller di dominio, digitare il nome utente hello e una password di un account di amministratore di dominio per quel dominio.
4. Fare clic su **Sì** tooverify hello identità della macchina virtuale hello e completare la registrazione.
   
   ![Screenshot che illustra un messaggio sul verifica identità hello di hello macchina virtuale.](./media/virtual-machines-log-on-win-server/cert-warning.png)

