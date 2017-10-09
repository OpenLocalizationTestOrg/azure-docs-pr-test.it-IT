Quando non è più necessario un disco dati è una macchina virtuale tooa collegato, è possibile scollegarlo facilmente. Scollegare un disco rimuove il disco hello dalla macchina virtuale hello, ma non Elimina disco hello dall'account di archiviazione Azure hello.

Se si desiderano nuovamente toouse hello esistente dati hello disco, è possibile ricollegarlo toohello stessa macchina virtuale o un altro.  

> [!NOTE]
> toodetach un disco del sistema operativo, è necessario prima macchina virtuale di toodelete hello.
>

## <a name="find-hello-disk"></a>Trovare il disco hello
Se non si conosce il nome di hello di hello disco oppure da tooverify, prima rimuoverlo, seguire questi passaggi.

1. Accedi toohello [portale di Azure](https://portal.azure.com).

2. Fare clic su **macchine virtuali**, e quindi selezionare hello VM appropriato.

3. Fare clic su **dischi** lungo hello bordo sinistro del dashboard di hello macchina virtuale, in **impostazioni**.

 dashboard macchina virtuale Hello Elenca hello nome e tipo di tutti i dischi collegati. Ad esempio, in questa schermata è visualizzata una macchina virtuale con un solo disco del sistema operativo e un unico disco dati:

    ![Ricerca di un disco dati](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a>Scollegare il disco hello
1. Dal portale di Azure hello, fare clic su **macchine virtuali**, quindi fare clic su nome hello della macchina virtuale hello che ha un disco dati hello desiderato toodetach.

2. Fare clic su **dischi** lungo hello bordo sinistro del dashboard di hello macchina virtuale, in **impostazioni**.

3. Fare clic hello disco toodetach.

  ![Identificare hello disco toodetach](./media/howto-detach-disk-windows-linux/disklist.png)

4. Dalla barra dei comandi di hello, fare clic su **scollegamento**.

  ![Individuare hello detach-comando](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. Nella finestra di conferma hello, fare clic su **Sì** disco hello toodetach.

  ![Confermare di scollegamento del disco hello](./media/howto-detach-disk-windows-linux/confirmdetach.png)

Hello disco rimane nel servizio di archiviazione, ma non è più macchine virtuali tooa associata.
