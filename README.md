[Монтирование файловой системы](https://docs.selectel.ru/servers-and-infrastructure/dedicated/troubleshooting/mount-file-system/?_gl=1*p0c72m*_gcl_au*OTYxMjUyMDg0LjE3MTM5ODI0MTU.*_ga*MTY2NzgwNTE5Ni4xNzEzOTgyNTY3*_ga_H3R3VJH01B*MTcyMDM0ODg0OS4yNi4xLjE3MjAzNTAzNDkuNTguMC4w#mount-manually)

![disks!](/20240707155843.png)

LVM (менеджер логических томов) не используется
___
## infiltrate-root /dev/sda1
![infiltrate-root-sda1!](/20240707160201.png)
<details>
	<summary><code>infiltrate-root /dev/sda1</code> log</summary>
	<pre>
	egrep: warning: egrep is obsolescent; using grep -E
	Mounting /dev/sda1 to /newroot...
	WARNING: Shell /bin/bash not found on new root.
	chroot: failed to run command ‘/bin/bash’: No such file or directory
	Unmounting /dev/sda1
	</pre>
</details>

## infiltrate-root /dev/sda2
![infiltrate-root-sda2!](/20240707173855.png)
<details>
	<summary><code>infiltrate-root /dev/sda2</code> log</summary>
	<pre>
	egrep: warning: egrep is obsolescent; using grep -E
	Mounting /dev/sda2 to /newroot...
	mount: /newroot: operation failed: Invalid argument.
	Failed to mount /dev/sda2
	</pre>
</details>

## infiltrate-root /dev/sda3
![infiltrate-root-sda3!](/20240707171059.png)

Завершилось без ошибок, но подключение к серверу установить так и не получилось.
![server-ping!](/20240707171811.png)

## infiltrate-root /dev/sda4
![infiltrate-root-sda4!](/20240707174038.png)
<details>
	<summary><code>infiltrate-root /dev/sda4</code> log</summary>
	<pre>
	egrep: warning: egrep is obsolescent; using grep -E
	Mounting /dev/sda4 to /newroot...
	WARNING: Shell /bin/bash not found on new root.
	chroot: failed to run command ‘/bin/bash’: No such file or directory
	Unmounting /dev/sda4
	</pre>
</details>


## infiltrate-root /dev/sda5
![infiltrate-root-sda5!](/20240707174053.png)
<details>
	<summary><code>infiltrate-root /dev/sda5</code> log</summary>
	<pre>
	egrep: warning: egrep is obsolescent; using grep -E
	Mounting /dev/sda5 to /newroot...
	WARNING: Shell /bin/bash not found on new root.
	chroot: failed to run command ‘/bin/bash’: No such file or directory
	Unmounting /dev/sda5
	</pre>
</details>

___
## sda1 вручную

Команда `infiltrate-root /dev/sda1` отработала с ошибками -> выполняю шаг 5 [монтирования файловой системы вручную](https://docs.selectel.ru/servers-and-infrastructure/dedicated/troubleshooting/mount-file-system/#mount-manually):

![sda1-manual!](/20240707160749.png)
<details>
	<summary><code>chroot /mnt /bin/bash</code> log</summary>
	<pre>
	chroot: failed to run command ‘/bin/bash’: No such file or directory
	</pre>
</details>

## sda2 вручную

![sda2-manual!](/20240707170105.png)
<details>
	<summary><code>mount /dev/sda2</code> log</summary>
	<pre>
	mount: /mnt: unknown filesystem type 'swap'.
    dmesg(1) may have more information after failed mount system call.
	</pre>
</details>

## sda3 вручную
![sda3-manual!](/20240707163945.png)

Сменил пароль на `hgjfkd657483` и синхронизировал данные:

![password-change!](/20240707164339.png)

Попытался размонтировать файловую систему, но выдало ошибку:

![unmount!](/20240707164526.png)

## sda4 и sda5 вручную
После монтирования sda4, кроме файла EFI в нем ничего не было.
После монтирования раздела sda5 в папке mnt также нет необходимых папок (`/bin/bash`) для подключения к окружению.
![sda5-manual!](/20240707170714.png)
