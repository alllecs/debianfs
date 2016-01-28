
Author:
https://github.com/ZubairLK/mkdebianrfs.git

script that uses qemu and debbootstrap to make a core debian rootfs

Go to http://www.elinux.org/How_to_make_a_debian_rootfs_for_MIPS_CI20 for instructions

Instruction:

1. Обновление пакетов
````
	sudo apt-get update
````
2. Установка пакетов
````
	sudo apt-get install binfmt-support qemu qemu-user-static debootstrap
````
3. Клонирование репозитория
````
	git clone https://github.com/alllecs/debianfs.git
````
4. Вход в папку
````
	cd debianfs
````
5. Создание образа
````
	sudo if=/dev/zero of=jessiesmall.img bs=2M count=2048
````
6. Форматирование
````
	sudo mkfs.ext4 jessiesmall.img
````
7. Создание папки
````
	sudo mkdir jessiesmall
````
8. Монитрование образа
````
	sudo mount -o loop jessiesmall.img jessiesmall
````
9. Разархивация
````
	sudo tar vxjf jessiesmall.tar.bz2
````
10. Размонтирование
````
	sudo umount jessiesmall
````
11. Изменение прав
````
	sudo chown pcuser:pcuser jessiesmall.img
````
12. Запуск qemu
````
	qemu-system-mips -M malta -m 256 -kernel vmlinux -append "console=ttyS0 root=/dev/sda" -serial stdio -nographic -monitor none -hda jessiesmall.img
````
