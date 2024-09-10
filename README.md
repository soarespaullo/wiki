# MONTAR AUTOMATICAMENTE NO BOOT LUKS S/ LVM

### Abrir a partição.
```
# cryptsetup luksOpen /dev/sdX kRypt0
```

### Criando os diretórios para montagem das partições.

```
 # mkdir -p /media/{Backup,kRypt0}
```

### Montando a Partição.

```
# mount /dev/mapper/Backup /media/kRypt0
```

### Criando Chave.
```
dd if=/dev/urandom of=/root/chave bs=4096 count=1
```
```
# cryptsetup luksAddKey /dev/sdX /root/chave
passphrase
```

### Só o ROOT ter acesso.
```
# sudo su -
# chmod 0400 chave
# exit
```
### Montar Automático no BOOT do Sistema.

```
# vim /etc/crypttab
Backup	/dev/sdX	/root/chave	luks
```

```
# vim /etc/fstab
/dev/mapper/Backup		/media/Backup	ntfs	defaults	0	0
```

### reboot

### Conferindo se está tudo certo.
```
# mount | greep  media
```
