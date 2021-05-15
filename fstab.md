### Автоматическое монтирование разделов при загрузке Linux
---

1. Создать папку, куда будет монтироваться раздел:

    ```sh
    sudo mkdir /home/media 
    sudo chmod 777 /home/media
    ```

1. Узнать UUID раздела, который будем монтировать:

    `lsblk -o +FSTYPE,UUID -e 7`

    ```txt
    NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT   FSTYPE UUID
    sda      8:0    0   1.8T  0 disk                     
    |-sda1   8:1    0    64G  0 part /            ext4   83aab899-55e5-4236-8927-671ea741d8ab
    `-sda2   8:2    0   1.8T  0 part              ntfs   CC4A787B4A7863DC
    sdb      8:16   0   1.8T  0 disk                     
    `-sdb1   8:17   0   1.8T  0 part              ext4   65a36a47-c024-447b-a519-5d255719ec69
    ```

1. Открыть в текстовом редакторе файл */etc/fstab* и добавить в конец файла строку:

    * для ext4:

        `UUID=%ваш_uuid% /home/media ext4 defaults,noatime 0 2`

    * для ntfs:

        `UUID=%ваш_uuid% /home/media ntfs rw,auto,user,fmask=133,dmask=022,uid=1000,gid=1000 0 0`

1. Сохранить изменения в файле */etc/fstab*

1. Смонтировать раздел:

    `sudo mount -a`

1. Убедиться, что раздел смонтировался, выполнив команду из п.2 (см. колонку *MOUNTPOINT*).
