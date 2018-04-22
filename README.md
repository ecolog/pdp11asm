# Ассемблер PDP11/БК0010

Транслятор ассемблерных программ для процессоров семейства DEC в машинный код PDP11/БК0010.


## Как собрать транслятор из исходников

```bash
make
```

Скомпилированые бинарники под некоторые платформы лежат в папке [release](https://github.com/imachug/pdp11asm/tree/master/release).


## Трансляция ассемблерного текста в машинные коды


1. Скопируйте бинарник под вашу платформу куда-нибудь (например, `/Users/Ivanq/Documents/BK0010/compiler` на MacOS или `/home/Documents/BK0010/compiler` на Linux).

2. Создайте файл [compile.sh](https://gist.github.com/imachug/3a27a7516fc50b5b8b2595b8af2d571e) в той же директории и добавьте ему права на выполнение (например, в терминале командой `chmod +x compile.sh`). По умолчанию компилятор создает файл без заголовка и без расширения (чистый бинарный код), но если Вам нужен BIN-файл (с заголовком, содержащим адрес и длину), добавьте строку `.LINK 1000` в самое начало своей программы и `make_bk0010_rom "file.bin", 1000` в конец своей ассемблерной программы. (1000 - адрес, с которого будет компилироваться программа)

3. Вам понадобится текстовый редактор Sublime Text и [плагин для подсветки синтаксиса DEC/PDP11](https://gist.github.com/imachug/3ab11df5e91c8d815a8c63a76bb08b14).

4. В настройках Sublime Text выберете *Browse packages...*. Откроется папка пакетов. Создайте в ней файл `User/BK0010.sublime-build`:

```json
{
    "shell_cmd": "\"<path_to_compiler>/compile.sh\" \"$file_path/$file_name\""
}
```

`<path_to_compiler>` - это полный путь к файлу [compile.sh](https://gist.github.com/imachug/3a27a7516fc50b5b8b2595b8af2d571e) на вашем компьютере (относительный путь типа `~/Documents` почему-то не работает). Чтобы узнать полный путь к файлу на MacOS, нажмите на него правой кнопкой мыши, затем удерживайте <kbd>alt</kbd> и выберете *Copy as Pathname*.

5. Теперь, чтобы транслировать ассемблерную программу, нажмите в Sublime Text <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>B</kbd>, выберите `BK0010`. В следующий раз будет работать просто <kbd>Ctrl</kbd>+<kbd>B</kbd>.

6. Результат работы транслятора - файл с машинным кодом - запишется в ту же директорию, где лежит исходный текст ассемблерной программы.

7. Для запуска вам понадобится эмулятор БК0010/11М.
