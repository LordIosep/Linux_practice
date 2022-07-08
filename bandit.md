# Bandit
## Nivel 0-1
### Tarea
La contraseña para el siguiente nivel se almacena en un archivo llamado `Readme` ubicado en el directorio de inicio.
### Solución 
En el mismo directorio donde nos encontramos podemos realizar un `ls` para ver que el archivo se encuentre ahi.
```
$ bandit0@bandit:~$ ls -l
$ readme
```
Como se puede observar esta el archivo `readme`,  entonces para ver el contenido de este archivo podemos usar estos comandos: cat, nano y vi 
```
bandit0@bandit:~$ cat readme
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```
### Contraseña encontrada
* boJ9jbbUNNfktd78OOpsqOltutMc3MY1

## Nivel 1-2
### Tarea
Obtenga la contraseña del archivo llamado '-'.
### Solución
`-` es un simbolo especial para linux en entonces que para ver este archivo se tiene que usar `cat`, pero agregando tambien la ruta. 

```
bandit1@bandit:~$ ls -l
-
bandit1@bandit:~$ cat ./-
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```
### Contraseña encontrada
* CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9

## Nivel 2-3
### Tarea 
La contraseña para el siguiente nivel se almacena en un archivo llamado *spaces in this filename* ubicado en el directorio de inicio.
### Solución
Al igual que el anterior al poner cat para ver el archivo sale error.
```
bandit2@bandit:~$ cat spaces in this filename
cat: spaces: No such file or directory
cat: in: No such file or directory
cat: this: No such file or directory
cat: filename: No such file or directory
```
Es entonces que se puede ver el archivo de dos maneras:
**Solucion 1:**
```
bandit2@bandit:~$ ls
spaces in this filename
bandit2@bandit:~$ spaces\ in\ this\ filename
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```
**Solucion 2:**
```
bandit2@bandit:~$ cat "spaces in this filename"
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```
### Contraseña encontrada
* UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK

## Nivel 3-4
### Tarea
La contraseña para el siguiente nivel se almacena en un archivo oculto en el directorio `inhere`.
### Solución
Para esta tarea tenemos dos soluciones una es moviendonos por los directorios hasta encontrar `inhere` y la otra es desde el mismo directorio donde nos encontramos, realizar la ejecucion de `ls` y `cat` dentro de los directorios existentes.
**Solucion 1:**
```
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$ ls -a
.  ..  .hidden
bandit3@bandit:~/inhere$ cat .hidden
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```
**Solucion 2:**
```
bandit3@bandit:~$ ls -a \inhere
.  ..  .hidden
bandit3@bandit:~$ cat inhere/.hidden
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```
### Contraseña encontrada
* pIwrPrtPN36QITSp3EQaw936yaFoFgAB

## Nivel 4-5
### Tarea 
La contraseña para el siguiente nivel se almacena en el único archivo legible por humanos en el directorio `inhere`.
### Solución
Para esta tarea se desea ver el archivo legible por humanos es entonces que usamos este comando `file`, para encontrar de todos los archivos de la carpeta cual se puede leer.

```
bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$ ls -la
total 48
drwxr-xr-x 2 root    root    4096 May  7  2020 .
drwxr-xr-x 3 root    root    4096 May  7  2020 ..
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file00
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file01
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file02
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file03
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file04
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file05
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file06
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file07
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file08
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file09
```
Como se puede observar hay muchos archivos y no sabemos cual se puede leer por humanos.
```
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```
El `-file07` es del tipo `ASCII text`, que es una de las codificaciones que los humanos pueden leer.
```
bandit4@bandit:~/inhere$ cat ./-file07
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```
### Contraseña encontrada
* koReBOKuIDDepwhWk7jZC0RTdopnAYKh

## Nivel 5-6
### Tarea
La contraseña para el siguiente nivel se almacena en un archivo en algún lugar del directorio inhere y tiene todas las siguientes propiedades:
* legible por humanos
* 1033 bytes de tamaño
* no ejecutable
### Solución
Para esta tarea se desea buscar un archivo con las caracteristicas anteriormente mencionadas, es por eso que se usara en comando `find`.

Opciones        | Descripción                                                                                  
--------------- | ----------------------------------------------------------------------------------------
`. O ./ `       | Consulte el directorio de trabajo actual                                                     
`-type f`       | Coincidan con archivos que son **legibles**.                                                 
`-executable`   | Coincidan con los archivos que son **directorios ejecutables  &  que se pueden buscar**      
`! -executable` | Coincidan con archivos que **NO** son ejecutables & directorios que **NO** se pueden buscar  
`-size 1033c`   | El archivo usa **1033** unidades de espacio. `c` se refiere a **bytes** .  


```
bandit5@bandit:~$ ls
inhere
bandit5@bandit:~$ cd inhere/
bandit5@bandit:~/inhere$ ls
maybehere00  maybehere03  maybehere06  maybehere09  maybehere12  maybehere15  maybehere18
maybehere01  maybehere04  maybehere07  maybehere10  maybehere13  maybehere16  maybehere19
maybehere02  maybehere05  maybehere08  maybehere11  maybehere14  maybehere17
bandit5@bandit:~$ find . -type f -readable ! -executable -size 1033c
./inhere/maybehere07/.file2
bandit5@bandit:~$ cat ./inhere/maybehere07/.file2
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```
Tambien se puede buscar de esta manera:
```
bandit5@bandit:~/inhere$ find . -type f -size 1033c ! -executable -exec file '{}' \; | grep ASCII
./maybehere07/.file2: ASCII text, with very long lines
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```
### Contraseña encontrada
* DXjZPULLxYr17uwoI01bNLQbtFemEgo7

## Nivel 6-7
### Tarea
Encuentre un archivo en algún lugar del servidor. Propiedades:
* owned by user bandit7
* owned by group bandit6
* 33 bytes in size
### Solución
Al igual que el anterior nivel se necesita buscar un archivo que tenga las caracteristicas ya mencionadas 
```
bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c  //buscara con el usuario bandit7 con el grupo bandit6 con un tamaño 33 bytes
```
![](https://github.com/LordIosep/Linux_practice/blob/main/Imagenes/Bandit6.PNG)

Para remover los permisos denegados

```
bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
```
### Contraseña encontrada
* HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs

## Nivel 7-8
### Tarea 
La contraseña para el siguiente nivel se almacena en el archivo `data.txt` junto a la palabra `millionth`.
### Solución
Después de iniciar sesión, estaremos en el directorio de inicio . Al ejecutar `ls`, verá que `data.txt` está justo en el directorio de inicio. Por lo tanto, no tenemos que realizar `cd`.

Si se hace `cat` al archivo `data.txt` solo se observara un monton de lineas con texto y se tardara mucho en encontrar la contraseña.

Se usara el comando grep, para buscar lineas que tengan un patron especifico; para este nivel se tienen dos soluciones, uno usando solo el comando `grep` y otro usando (`|`) con el comando `cat`.

Verificando el tamaño del archivo de data.txt, podemos ver que es enorme:
```
bandit7@bandit:~$ du -b data.txt 
4184396 data.txt
```
Por lo tanto, simplemente revisar el archivo llevaría demasiado tiempo y sería demasiado esfuerzo.

En su lugar, podemos intentar usar `grep`, ya que la contraseña está en la misma línea que la palabra `millionth`.
**Solución 1:**
```
bandit7@bandit:~$ grep "millionth" data.txt OR grep -w "millionth"
millionth cvX2JJa4CFALtqS87jk27qwqGhBM9plV              
```
**Solución 2:**
```
bandit7@bandit:~$ cat data.txt | grep "millionth”
millionth cvX2JJa4CFALtqS87jk27qwqGhBM9plV
```
## **Solución Extra**

Tambien se puede utilizar el comando `vi` que es un editor de texto de linux.
```
bandit7@bandit:~$ vi data.txt
```

En este editor buscamos la palabra `millionth` con `/`

![](https://github.com/LordIosep/Linux_practice/blob/main/Imagenes/vi.PNG)

### Contraseña encontrada
* cvX2JJa4CFALtqS87jk27qwqGhBM9plV

## Nivel 8-9
### Tarea
La contraseña para el siguiente nivel se almacena en el archivo `data.txt` y es la única línea de texto que aparece una sola vez.
### Solución
Para encontrar la línea que aparece solo una vez en el archivo, primero ordenamos las líneas y luego filtramos por la única, para eso usamos el comando `sort` luego (`|`) con `uniq`.

`uniq` es un comando que filtra la entrada y escribe en la salida. En concreto, filtra en función de líneas idénticas. Tiene una bandera -u, que filtra por líneas únicas (líneas que aparecen solo unas).

`sort` ordena las líneas de un archivo de texto. Además, tiene banderas para ordenar en reversa (`-r`) y ordenar numéricamente (`-n`).
```
bandit8@bandit:~$ ls 
data.txt
bandit8@bandit:~$  cat data.txt | sort | uniq -u
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```
Tambien se puede usar
```
bandit8@bandit:~$ sort data.txt | uniq -u
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```

### Contraseña encontrada
* UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR

## Nivel 9-10
### Tarea
La contraseña para el siguiente nivel se almacena en el archivo `data.txt` en una de las pocas cadenas legibles por humanos, precedida por varios caracteres `=`.
### Solución

Primero, debemos distinguir las cadenas legibles por humanos en 'data.txt'. Usamos el comando `strings`.
Segundo, Dado que la contraseña está precedida por varios caracteres '=', podemos usar la expresión regular, pasando `grep -E` PATTERN opciones. 

```
bandit9@bandit:~$  ls 
data.txt
bandit9@bandit:~$ file data.txt
data.txt: data
bandit9@bandit:~$ strings data.txt | grep ===
========== the*2i"4
========== password
Z)========== is
&========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
```

Tambien se puede hacer de esta manera

```
bandit9@bandit:~$ strings data.txt | grep -E "=+"
========== the*2i"4
=:G e
========== password
<I=zsGi
Z)========== is
A=|t&E
Zdb=
c^ LAh=3G
*SF=s
&========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
S=A.H&^
```
### Contraseña encontrada
* truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk

## Nivel 10-11
### Tarea
La contraseña para el siguiente nivel se almacena en el archivo `data.txt`, que contiene datos codificados en base64.
### Solución
Para esta tarea se desea encontrar la contraseña que esta en el archivo `data.txt` que este se encuentra en un formato base64 es por eso que se usara el comando `base64` que permite codificar y decodificar. Para decodificar, necesitamos usar la bandera  o flasg `-d`. 
```
bandit10@bandit:~$ ls 
data.txt
bandit10@bandit:~$cat data.txt
VGhlIHBhc3N3b3JkIGlzIElGdWt3S0dzRlc4TU9xM0lSRnFyeEUxaHhUTkViVVBSCg==
bandit10@bandit:~$ base64 -d data.txt // -d tag para  decodificar
The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
Tambien se puede usar:
bandit10@bandit:~$ cat data.txt | base64 — decode
The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
```
### Contraseña encontrada
* IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR

## Nivel 11-12
### Tarea
La contraseña para el siguiente nivel se almacena en el archivo data.txt , donde todas las letras minúsculas (az) y mayúsculas (AZ) se han rotado 13 posiciones.
### Solución
Sabemos que los caracteres en los datos están rotados por 13 caracteres. Podemos hacer que los caracteres vuelvan a su orden original usando el comando `tr`. El comando `tr`se utiliza para traducir/transformar datos de un formulario a otro.
```
bandit11@bandit:~$  ls 
data.txt
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh
```
En nuestro caso, para decodificar los contenidos en data.txt, el comando a utilizar es ``. Esto significa que para:
Mayúsculas : Mapa de `A-Z` a `N-ZA-M` 
Minúsculas : Mapa de `a-z` a `n-za-m`

Como tal, cualquiera de los siguientes comandos generará el `data.txt` contenido decodificado:

* cat data.txt | tr “A-Za-z” “N-ZA-Mn-za-m”
* cat data.txt | tr “a-zA-Z” “n-za-mN-ZA-M” or
* cat data.txt | tr “[a-zA-Z]” “[n-za-mN-ZA-M]”
* cat data.txt | tr “n-za-mN-ZA-M” “a-zA-Z”

```
bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
```
### Contraseña encontrada
* 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu

## Nivel 12-13
### Tarea
La contraseña para el siguiente nivel se almacena en el archivo data.txt , que es un volcado hexadecimal de un archivo que ha sido comprimido repetidamente. Para este nivel, puede ser útil crear un directorio bajo /tmp en el que pueda trabajar usando mkdir. Por ejemplo: mkdir /tmp/myname123. Luego copie el archivo de datos usando cp, y cámbiele el nombre usando mv
### Solución 
Esta tarea es una de las mas largas de bandit, es por eso que tendra partes donde se explicara lo que se hizo.
### Parte 1 **Crear directorio y mover archivo**
Ver el contenido del directorio de trabajo actual
```
bandido12@bandido:~$ ls 
datos.txt
```
Ver los datos que están presentes en el archivo
```
bandit12@bandit:~$ head data.txt 
00000000: 1f8b 0808 0650 b45e 0203 6461 7461 322e .....P.^..data2. 
00000010: 6269 6e00 013d 02c2 fd42 5a68 3931 4159 bin..=...BZh91AY 
00000020: 2653 598e 4f1c c800 001e 7fff fbf9 7fda &SY.O........... 
0000000f6 fff6 f7 f730: 4f7cf730: 4f7cf7 abde 5e9f ..Ov...}?..}..^. 
00000040: f3fe 9fbf f6f1 feee bfdf a3ff b001 3b1b ..............;. 
00000050: 5481 a1a0 1ea0 1a34 d0d0 001a 68d3 4683 T......4....hF 
00000060: 4680 0680 0034 1918 4c4d 190c 4000 0001 F....4..LM..@... 
00000070: a000 c87a 81a3 464d a8d3 43c5 1068 0346 ...z..FM..C..hF 
00000080: 8343 40d0 3400 0340 66a6 8068 0cd4 f500 .C@.4.. @f ..h....
00000090: 69ea 6800 0f50 68f2 4d00 680d 06ca 0190 ih.Ph.Mh....
```

Mirando los datos, vemos que el archivo consta de datos hexadecimales. Tenemos que convertir estos datos hexadecimales a binarios para recuperar el archivo real. Podemos hacer uso del comando `xxd` que nos permite manipular datos hexadecimales. La `-r` bandera se usa para decirle a `xxd` que invierta la operación (hexadecimal a binario)

Pero antes de hacer nada de esto, primero debemos crear un directorio de trabajo temporal en el directorio `/tmp`, ya que no tenemos permiso para crear nuevos archivos en la ubicación actual. Podemos hacer esto usando el comando `mkdir`. Para movernos al nuevo directorio podemos usar el comando `cd`.

Otra solucion seria:

Al leer las reglas dadas cuando ingresamos al servidor de bandit, también podemos usar `mktemp -d` para crear una carpeta con un nombre aleatorio, en lugar de usar `mkdir` y elegir un nombre. 
```
bandido12@bandido:~$ mkdir /tmp/random_dir
bandido12@bandido:~$ cd /tmp/random_dir
bandido12@bandido:/tmp/random_dir$
```
Ahora tenemos que mudarnos data.txta esta nueva ubicación. Podemos hacer esto usando el cpcomando. Y luego cambiamos el nombre del archivo para eliminar la .txtextensión, ya que sabemos que el archivo no es un archivo de texto.
```
bandit12@bandit:/tmp/random_dir$ cp ~/data.txt .
bandit12@bandit:/tmp/random_dir$ ls 
datos.txt
bandit12@bandit:/tmp/random_dir$ mv data.txt datos
bandit12@bandit:/tmp/random_dir$ ls 
datos
```
### Parte 2 **Revertir el volcado hexadecimal del archivo**
Ahora que los datos son un nuevo directorio, ahora podemos usar xxd para convertir los datos en su equivalente binario

Mirando el archivo, vemos el formato de los datos. Como se dijo, es un volcado hexadecimal. Se parece a esto:
```
$ cat hexdump_data | head
00000000: 1f8b 0808 0650 b45e 0203 6461 7461 322e  .....P.^..data2.
00000010: 6269 6e00 013d 02c2 fd42 5a68 3931 4159  bin..=...BZh91AY
00000020: 2653 598e 4f1c c800 001e 7fff fbf9 7fda  &SY.O...........
00000030: 9e7f 4f76 9fcf fe7d 3fff f67d abde 5e9f  ..Ov...}?..}..^.
00000040: f3fe 9fbf f6f1 feee bfdf a3ff b001 3b1b  ..............;.
00000050: 5481 a1a0 1ea0 1a34 d0d0 001a 68d3 4683  T......4....h.F.
00000060: 4680 0680 0034 1918 4c4d 190c 4000 0001  F....4..LM..@...
00000070: a000 c87a 81a3 464d a8d3 43c5 1068 0346  ...z..FM..C..h.F
00000080: 8343 40d0 3400 0340 66a6 8068 0cd4 f500  .C@.4..@f..h....
00000090: 69ea 6800 0f50 68f2 4d00 680d 06ca 0190  i.h..Ph.M.h.....
```

Sin embargo, queremos operar con los datos reales. Por lo tanto, revertimos el hexdump y obtenemos los datos reales.

```
bandit12@bandit:/tmp/random_dir$ xxd -r datos > binario
bandit12@bandit:/tmp/random_dir$ ls 
datos binario
bandit12@bandit:/tmp/random_dir$ file binario
binario: gzip compressed data, was "data2.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix

bandit12@bandit:/tmp/random_dir$ cat binario
P▒^data2.bin=▒▒BZh91AY&SY▒O▒▒▒▒ڞOv▒▒▒}?▒▒}▒▒^▒▒▒▒▒▒▒▒▒ߣ▒▒;▒▒▒▒4▒▒h▒F▒F▒▒4LM
                                                                           @▒▒z▒▒FM▒▒C▒hF▒C@▒4@f▒▒h
4hh▒=C%▒>X,▒k▒▒▒1▒▒GY▒▒hPh▒Mh
▒J▒쌑Oϊ▒▒{RBp▒Qix▒Y▒Z!d▒▒j▒(▒搿ݳ▒▒/▒▒A▒#▒A▒▒0P▒▒v▒▒`▒"3▒

                                          ▒▒d▒bX?▒▒z▒▒2▒▒<▒▒A ▒n}
5(3A▒▒
      wO▒R▒▒▒▒6▒XS{▒
▒▒9?L▒P▒yB▒▒=z▒m?▒L▒Nt*▒7{qP▒▒̜▒%"▒w9▒qm4▒▒ N3▒6▒▒▒K▒▒H䋑[▒▒}!
                                                             d▒▒3A4$▒M~▒\ɠJ▒C▒kUƦ\▒▒▒\▒FSN▒▒&=▒[▒▒q     \)▒$:▒▒H▒t&/▒(▒▒▒▒]▒▒BB9<s ▒▒h=
```
### Parte 2 **Descomprimir repetidamente**
Podemos ver que el archivo se comprimió con qzip, por lo que podemos descomprimir los datos con el comando `gunzip`. Al intentar descomprimir un archivo gzip, es importante que el archivo tenga la extensión correcta. Gunzip es una abreviatura de comando `gzip -d`
```
bandit12@bandit:/tmp/random_dir$ mv binario binario.gz
bandit12@bandit:/tmp/random_dir$ ls
binario.gz datos
bandit12@bandit:/tmp/random_dir$ gunzip binario.gz
bandit12@bandit:/tmp/random_dir$ ls 
datos binario
```
### Parte 2.1 
Sin embargo, los datos aún no están completamente descomprimidos, por lo que volvemos a mirar el comando `file`
```
bandit12@bandit:/tmp/random_dir$ file binario
binario: bzip2 compressed data, block size = 900k
```
Se puede observar que el archivo ahora se encuentra en formato `bzip2`, entonces usamos el comando ``bzip2 -d` para descomprimir
```
bandit12@bandit:/tmp/random_dir$ mv binario binario.bz2
bandit12@bandit:/tmp/random_dir$ ls
binario.bz2  datos
bandit12@bandit:/tmp/random_dir$ bzip2 -d binario.bz2
bandit12@bandit:/tmp/random_dir$ ls
binario  binary  data  datos
```
### Parte 2.2
Usando el comando `file` podemos ver que clase de archivo es

```
bandit12@bandit:/tmp/random_dir$ file binario
binario: gzip compressed data, was "data4.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix
```
Parece que ahora tenemos un archivo. Entonces usamos `tar` para extraer el archivo:
```
bandit12@bandit:/tmp/random_dir$ mv binario binario.tar
bandit12@bandit:/tmp/random_dir$ ls
binario.tar datos
bandit12@bandit:/tmp/random_dir$ tar -xf binario.tar ; ls
binario.tar  data5.bin  datos
```
### Parte 2.3
Volvemos a analizar el archivo con el comando `file` y usando `cat binario.tar o binario.tar | head` ('head' para obtener solo las primeras 10 líneas), podemos ver la cadena 'data5.bin', que es un nombre de archivo.
```
bandit12@bandit:/tmp/random_dir$ file data5.bin
data5.bin: POSIX tar archive (GNU)
bandit12@bandit:/tmp/random_dir$ cat data5.bin | head
data6.bin0000644000000000000000000000033613655050006011247 0ustar  rootrootBZh91AY&SY
                                                                                    +
                                                                                     ▒▒▒Y▒A▒▒z▒<jA▒▒j▒u▒  ▒
            ▒@ѣ ▒▒!▒hiM▒
 ▒▒▒BȨ$fz&1*▒Ԇf▒▒zG▒g}▒+▒Q▒P(f}▒▒@Թ▒▒▒▒▒Tj▒1▒P▒EƮ▒▒ߨ▒▒▒@Ț▒▒=▒s▒▒*▒▒▒As*Y▒▒!$r▒▒5▒▒▒Es▒]▒▒B@ 0▒,
```
Y se puede observar que hay otro archivo llamado `data6.bin`. Así que extraemos el archivo de nuevo.
### Parte 2.4
```
bandit12@bandit:/tmp/random_dir$ tar -xf data5.bin
bandit12@bandit:/tmp/random_dir$ ls
binario.tar  binary  data  data5.bin  data6.bin  datos
```

Volvemos a verificar que tipo de arhivo es, con el comando `file`. 
### Parte 2.5
```
bandit12@bandit:/tmp/random_dir$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
```
### Parte 2.6
Es un archivo bzip2 entonces usamos nuevamente el comando `bzip2 -d`
```
bandit12@bandit:/tmp/random_dir$ bzip2 -d data6.bin ; ls
bzip2: Can't guess original name for data6.bin -- using data6.bin.out
binario.tar  binary  data  data5.bin  data6.bin.out  datos
```
Volvemos a ver que archivo es con el comando `cat | head ` 
```
bandit12@bandit:/tmp/random_dir$ cat data6.bin.out | head
data8.bin0000644000000000000000000000011713655050006011246 0ustar  rootrooP▒^data9.bin
                                                                                      ▒HU(H,..▒/JQ▒,V▒▒ʪt▒t
w▒▒▒KM▒▒(▒p.3.O2J4▒*▒▒▒▒▒▒1
```
### Parte 2.6
Se puede observar que hay un archivo llamado `data8.bin`.

Finalmente, tenemos que hacer una descompresión más gzip y obtenemos un archivo legible con la contraseña.
```
bandit12@bandit:/tmp/random_di  $ xxd data8.bin
00000000: 1f8b 0808 0650 b45e 0203 6461 7461 392e  .....P.^..data9.
bandit12@bandit:/tmp/random_di$ mv data8.bin data8.gz
bandit12@bandit:/tmp/random_di$ gzip -d data8.gz
bandit12@bandit:/tmp/random_di9$ ls
binario.tar  binary  data  data5.bin  data6.bin.out  datos  data8  
bandit12@bandit:/tmp/random_di$ cat data8
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
```
## Solución cuando ya sabes los pasos a seguir

```
bandido12@bandido:~$ mkdir /tmp/pass123
bandido12@bandido:~$ cp data.txt  /tmp/pass123
bandido12@bandido:$cd /tmp/pass123
bandido12@bandido:/tmp/pass123$ xxd -r data.txt > data
bandido12@bandido:/tmp/pass123$ zcat data | bzcat | zcat | tar -xO | tar -xO | bzcat | tar -xO | zcat | cat
8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
```

### Contraseña encontrada
* 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL

## Nivel 13-14
### Tarea
La contraseña para el siguiente nivel se almacena en /etc/bandit_pass/bandit14 y solo puede leerla el usuario bandit14 . Para este nivel, no obtiene la siguiente contraseña, pero obtiene una clave SSH privada que puede usarse para iniciar sesión en el siguiente nivel.
### Solución
Inicié sesión en el servidor como bandit13 y encontré el archivo 'sshkey.private' en el directorio de inicio. 
```
bandit13@bandit:~$ ls 
sshkey.privado
```
Tenemos una clave privada SSH. Podemos usar el comando SSH con la bandera `-i` para usar la clave privada.

```
bandit13@bandit:~$ ssh -i sshkey.private bandit14@localhost
```
Le saldra el siguiente mensaje : Are you sure you want to continue connecting (yes/no)? al cuel tiene que respoder con ´yes´, etnonces podra entrar desde ssh al bandit14 desde el bandit 13.

Ahora a obtener la contraseña del usuario actual

```
bandido14@bandido:~$ gato /etc/bandit_pass/bandit14 
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
```
### Contraseña encontrada
* 4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e

## Nivel 14-15
### Tarea
La contraseña para el siguiente nivel se puede recuperar enviando la contraseña del nivel actual al puerto 30000 en localhost.
### Solución
De la pregunta sabemos que hay un servicio que se ejecuta en el puerto 30,000. Podemos intentar conectarnos al servicio usando el comando `netcat`.

Ayuda:`nc` es un alias para el comando`netcat` y se puede usar indistintamente.

Primero, necesitamos encontrar la contraseña para bandit14. Los niveles anteriores indicaban que la contraseña está en /etc/bandit_pass/bandit14 
```
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
```
A continuación, debemos enviar la contraseña al puerto 30000 en localhost. Solía nc​​​​conectarme al puerto localhost 3000 y escribir la contraseña.
```
bandit14@bandit:~$ nc localhost 30000
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
```

### Contraseña encontrada
* BfMYroe26WYalil77FoDi9qh59eK5xNr

## Nivel 15-16
### Tarea
La contraseña para el siguiente nivel se puede recuperar enviando la contraseña del nivel actual al puerto 30001 en localhost usando encriptación SSL.
### Solución
Dado que la tarea indica que la contraseña se puede recuperar mediante el cifrado SSL, me conecto al servidor localhost con el cliente OpenSSL y envío la contraseña desde este nivel. Luego, el servidor devuelve la contraseña para el siguiente nivel.

La forma más sencilla de lograr esto es usando el comando `openssl` junto con `s_client` el cual permite conectarse a los servicios en nuestra máquina usando SSL.
```
bandit15@bandit:~$ openssl s_client -connect localhost:30001
CONNECTED(00000003)
depth=0 CN = localhost
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = localhost
verify return:1
---
Certificate chain
 0 s:/CN=localhost
   i:/CN=localhost
---
.
.
.
Start Time: 1615101060
    Timeout   : 7200 (sec)
    Verify return code: 18 (self signed certificate)
    Extended master secret: yes
---
Password
Wrong! Please enter the correct current password
closed
```
Cuando proporcionamos la contraseña como "Password", aparece un error que dice una contraseña incorrecta

Proporcionemos la contraseña correcta para ver si obtenemos la contraseña para el siguiente nivel. La contraseña para el nivel actual se puede encontrar en `/etc/bandit_pass/bandit15`

```
bandit15@bandit:~$ cat /etc/bandit_pass/bandit15
BfMYroe26WYalil77FoDi9qh59eK5xNr
bandit15@bandit:~$ openssl s_client -connect localhost:30001
BfMYroe26WYalil77FoDi9qh59eK5xNr
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd
```

### Contraseña encontrada
* cluFn7wTiGryunymYOu4RcffSxQluehd

## Nivel 16-15
### Tarea
Las credenciales para el siguiente nivel se pueden recuperar enviando la contraseña del nivel actual a un puerto en localhost en el rango 31000 a 32000 . Primero averigüe cuáles de estos puertos tienen un servidor escuchando en ellos. Luego, averigüe cuáles de ellos hablan SSL y cuáles no. Solo hay 1 servidor que proporcionará las siguientes credenciales, los demás simplemente le enviarán lo que le envíe.
### Solución
Primero, necesitamos encontrar puertos abiertos entre 31000 y 32000 en localhost y verificar qué servicios se ejecutan en ellos. Utilicé el descubrimiento de servicios de nmap. (Esta tarea podría dividirse encontrando primero los puertos abiertos y luego haciendo el descubrimiento del servicio solo en estos puertos. Esto podría ser más rápido).

```
bandit16@bandit:~$ nmap -sV localhost -p 31000-32000

Starting Nmap 7.40 ( https://nmap.org ) at 2021-06-12 16:17 CEST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00026s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
```
La bandera `-p` es importante. Esta bandera nos permite elegir qué puertos escanear. De forma predeterminada, Nmap escanea los 1000 puertos principales (no los primeros 1000 puertos). Use -p para escanear todos los puertos 65535. La bandera `-sV` nos permite hacer un análisis de detección de servicio/versión.

Entonces, `nmap` nos dice que cinco puertos están abiertos. Solo dos puertos (31518 y 31790) usan SSL. Nmap también nos dice que el puerto 31518 solo ejecuta el servicio de echo. El puerto prometedor parece ser el puerto 31790, que ejecuta un servicio desconocido.

Otra solucion tambien seria usar el indicador o bandera  `-T4`, se usa para aumentar la velocidad de la exploración.

```
bandit16@bandit:~$ nmap -sV -T4 -p 31000-32000 localhost
Starting Nmap 7.40 ( https://nmap.org ) at 2021-03-07 09:04 CET
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00030s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port31790-TCP:V=7.40%T=SSL%I=7%D=3/7%Time=60448917%P=x86_64-pc-linux-gn
SF:u%r(GenericLines,31,"Wrong!\x20Please\x20enter\x20the\x20correct\x20cur
SF:rent\x20password\n")%r(GetRequest,31,"Wrong!\x20Please\x20enter\x20the\
SF:x20correct\x20current\x20password\n")%r(HTTPOptions,31,"Wrong!\x20Pleas
SF:e\x20enter\x20the\x20correct\x20current\x20password\n")%r(RTSPRequest,3
SF:1,"Wrong!\x20Please\x20enter\x20the\x20correct\x20current\x20password\n
SF:")%r(Help,31,"Wrong!\x20Please\x20enter\x20the\x20correct\x20current\x2
SF:0password\n")%r(SSLSessionReq,31,"Wrong!\x20Please\x20enter\x20the\x20c
SF:orrect\x20current\x20password\n")%r(TLSSessionReq,31,"Wrong!\x20Please\
SF:x20enter\x20the\x20correct\x20current\x20password\n")%r(Kerberos,31,"Wr
SF:ong!\x20Please\x20enter\x20the\x20correct\x20current\x20password\n")%r(
SF:FourOhFourRequest,31,"Wrong!\x20Please\x20enter\x20the\x20correct\x20cu
SF:rrent\x20password\n")%r(LPDString,31,"Wrong!\x20Please\x20enter\x20the\
SF:x20correct\x20current\x20password\n")%r(LDAPSearchReq,31,"Wrong!\x20Ple
SF:ase\x20enter\x20the\x20correct\x20current\x20password\n")%r(SIPOptions,
SF:31,"Wrong!\x20Please\x20enter\x20the\x20correct\x20current\x20password\
SF:n");
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 89.88 seconds
```

A partir de los resultados de nuestro escaneo, podemos ver que hay varios servicios que se ejecutan en ese rango, pero si observamos los resultados más de cerca, vemos que en el puerto 31790 hay un servicio que devuelve el mensaje "Ingrese la contraseña correcta". Como necesitamos encontrar un servicio para enviar contraseña, podemos concluir que este es el servicio que necesitamos.

Sabemos que el servicio utiliza encriptación SSL. Entonces necesitamos usar el comando openssly s_clientpara conectarnos al puerto y pasar la contraseña del usuario actual

```
bandit16@bandit:~$ cat /etc/bandit_pass/bandit16
cluFn7wTiGryunymYOu4RcffSxQluehd
bandit16@bandit:~$ openssl s_client --connect localhost:31790
CONNECTED(00000003)
.
.
.
---
cluFn7wTiGryunymYOu4RcffSxQluehd
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----
closed
```

No obtuvimos ninguna contraseña, pero obtuvimos una clave RSA que se puede usar con SSH para acceder al siguiente nivel. Necesitamos guardar la clave en un archivo para usarla con SSH. Como no tenemos permiso en el directorio de trabajo actual para crear un archivo. Creamos una carpeta en el `/tmp` directorio y trabajamos desde allí.

```
bandit16@bandit:~$ mkdir /tmp/random_sshkey
bandit16@bandit:~$ cd /tmp/random_sshkey
bandit16@bandit:/tmp/random_sshkey$ touch private.key
bandit16@bandit:/tmp/random_sshkey$ vim private.key
```

Se uso el editor de texto vim para para guardar la clave en el archivo

* Una vez que vim se abre, presione "i" para ingresar al modo de inserción
* Luego use Ctrl + Shift + V para pegar la clave copiada

![](https://github.com/LordIosep/Linux_practice/blob/main/Imagenes/nivel15_16.png)

* Pulse la tecla “Esc” para volver al modo normal
* Luego escriba :wqpara guardar y salir del archivo.

Cambie los permisos del archivo para que otros usuarios no puedan acceder al archivo

```
bandit16@bandit:/tmp/random_sshkey$ chmod 400 private.key
bandit16@bandit:/tmp/random_sshkey$ ls -l
total 4
-r-------- 1 bandit16 root 1676 Mar  7 09:23 private.key
```
Ahora podemos usar el archivo clave con el sshcomando para acceder al siguiente nivel.

```
bandit16@bandit:/tmp/random_sshkey$ ssh -i private.key bandit17@localhost

Linux bandit.otw.local 5.4.8 x86_64 GNU/Linux
      ,----..            ,----,          .---.
     /   /   \         ,/   .`|         /. ./|
    /   .     :      ,`   .'  :     .--'.  ' ;
   .   /   ;.  \   ;    ;     /    /__./ \ : |
  .   ;   /  ` ; .'___,/    ,' .--'.  '   \' .
  ;   |  ; \ ; | |    :     | /___/ \ |    ' '
  |   :  | ; | ' ;    |.';  ; ;   \  \;      :
  .   |  ' ' ' : `----'  |  |  \   ;  `      |
  '   ;  \; /  |     '   :  ;   .   \    .\  ;
   \   \  ',  /      |   |  '    \   \   ' \ |
    ;   :    /       '   :  |     :   '  |--"
     \   \ .'        ;   |.'       \   \ ;
  www. `---` ver     '---' he       '---" ire.org
Welcome to OverTheWire!
.
.
.
bandit17@bandit:~$
bandit17@bandit:~$ cat /etc/bandit_pass/bandit17
xLYVMN9WE5zQ5vHacb0sZEVqbrp7nBTn
```

### Contraseña encontrada
* xLYVMN9WE5zQ5vHacb0sZEVqbrp7nBTn

## Nivel 17-18
### Tarea
Hay 2 archivos en el directorio de inicio: `passwords.old` y `passwords.new`. La contraseña para el siguiente nivel está en `passwords.new` y es la única línea que se ha cambiado entre `passwords.old` y `passwords.new`.
### Solución
Ver los archivos que están presentes en el directorio de inicio.
```
bandit17@bandit:~$ ls
passwords.new  passwords.old
```

Sabemos que ambos archivos difieren en una sola línea y esa línea consiste en la contraseña que requerimos. Podemos ver los cambios que se han hecho en los archivos usando el Sabemos que ambos archivos difieren en una sola línea y esa línea consiste en la contraseña que requerimos. Podemos ver los cambios que se han hecho en los archivos usando el comando `diff`.
```
bandit17@bandit:~$ diff passwords.old passwords.new
42c42
< w0Yfolrc5bwjS4qw5mq1nnQi6mF03bii
---
> kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
```

El signo `<` representa las líneas que se han eliminado y el signo `>` representa las líneas que se han agregado en su lugar

La línea después del signo `>` es la contraseña para el siguiente nivel.

### Solucion 2

Esta solución alternativa se penso bansadose en el nivel 9,  sin embargo, no parece que `sort` mantenga el orden general de los archivos. Pero `grep` se puede utilizar para confirmar la contraseña correcta.

```
bandit17@bandit:~$ sort passwords.old passwords.new | uniq -u
kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
w0Yfolrc5bwjS4qw5mq1nnQi6mF03bii
bandit17@bandit:~$ cat passwords.new | grep w0Yfolrc5bwjS4qw5mq1nnQi6mF03bii
bandit17@bandit:~$ cat passwords.new | grep kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
```

### Contraseña encontrada
* kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd

## Nivel 18-19
### Tarea
La contraseña para el siguiente nivel se almacena en un archivo `readme` en el directorio de inicio. Desafortunadamente, alguien ha modificado `.bashrc` para cerrar la sesión cuando inicia sesión con SSH.
### Solución
Al leer la pregunta, entendemos que no podemos iniciar sesión directamente ya que el shell predeterminado "Bash" se ha modificado para no permitir ningún inicio de sesión mediante SSH. 

En lugar de iniciar sesión en la máquina con SSH, ejecutamos un comando a través de SSH. Primero, usamos `ls` para asegurarnos de que el archivo Léame esté en la carpeta y luego podemos usarlo `cat` para leerlo.

```
$ ssh bandit18@bandit.labs.overthewire.org -p 2220 ls         
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password: 
readme

$ ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme 
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password: 
IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x
```

### Solución 2
Como ya se menciono la shell predeterminada "Bash" se ha modificado para no permitir ningún inicio de sesión mediante SSH, es entoncees que necesitamos usar un shell que no sea bash para acceder al sistema.

Los detalles de todos los shells que están disponibles en un sistema se almacenan en `/etc/shells`. Veamos el archivo en nuestro sistema para tener una idea de cuáles son los diferentes shells que podrían estar presentes en el objetivo (solo en Linux)
```
> cat /etc/shells
# /etc/shells: valid login shells
/bin/sh
/bin/bash
/usr/bin/bash
/bin/rbash
/usr/bin/rbash
/bin/dash
/usr/bin/dash
/usr/bin/tmux
/usr/bin/screen
```

Cada línea en el archivo representa un shell que está presente en el sistema

Se puede usar el mismo método para ejecutar un comando con SSH pero usarlo `/bin/bash` como un comando para generar un shell bash o usar el `-t` indicador, lo que permite que se ejecute un 'pseudo-terminal' en la máquina de destino, de esta manera podemos ejecutar `\bin\sh`. Esto es especialmente útil si tenemos que ejecutar múltiples comandos porque no necesitamos repetir la declaración SSH y la contraseña.

```
$ ssh bandit18@bandit.labs.overthewire.org -p 2220 -t "/bin/sh"
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
bandit18@bandit.labs.overthewire.org's password: kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd //Password encontrado en el anterior nivel
$
```

Hemos logrado iniciar sesión con éxito usando el shell "sh"

Encuentre la contraseña que está presente en el archivo readme

```
$ ls
readme
$ cat readme
IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x
```

### Contraseña encontrada
* IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x

## Nivel 19-20
### Tarea
Para obtener acceso al siguiente nivel, debe usar el binario setuid en el directorio de inicio. Ejecutarlo sin argumentos para saber cómo usarlo. La contraseña para este nivel se puede encontrar en el lugar habitual (/etc/bandit_pass), después de haber utilizado el binario setuid.
### Solución
Nos han dicho que hay un archivo binario que está presente en el directorio de inicio que de alguna manera puede ayudarnos a acceder a la contraseña de bandit20. Echemos un vistazo al binario y verificamos quién es el propietario del binario setuid:

```
bandit19@bandit:~$ ls -la
total 28
drwxr-xr-x  2 root     root     4096 May  7  2020 .
drwxr-xr-x 41 root     root     4096 May  7  2020 ..
-rwsr-x---  1 bandit20 bandit19 7296 May  7  2020 bandit20-do
-rw-r--r--  1 root     root      220 May 15  2017 .bash_logout
-rw-r--r--  1 root     root     3526 May 15  2017 .bashrc
-rw-r--r--  1 root     root      675 May 15  2017 .profile
```

En este caso, el propietario es badit20 y el grupo es bandit19, esto con '-rwsr-x—' significa que el usuario bandit19 puede ejecutar el binario, pero el binario se ejecuta como usuario bandit20.

Ejecutar el binario dice que simplemente ejecuta otro comando como otro usuario (como ya se explicó, este usuario es bandit20). Esto significa que podemos acceder al archivo de contraseñas de los usuarios de bandit20, que solo puede leer el usuario bandit20.

El archivo nos dice que nos permite ejecutar un comando como otro usuario. Veamos un ejemplo de ejecución de un comando como otro usuario usando el comando id
```
bandit19@bandit:~$ id
uid=11019(bandit19) gid=11019(bandit19) groups=11019(bandit19)
bandit19@bandit:~$ ./bandit20-do id
uid=11019(bandit19) gid=11019(bandit19) euid=11020(bandit20) groups=11019(bandit19)
```

Observamos que cuando usamos el archivo binario, también se nos asigna el uid para bandit20, lo que significa que podemos ejecutar comandos como si fuéramos bandit20

Ahora que sabemos que podemos ejecutar comandos como bandit20, usemos el binario para acceder a la contraseña del usuario bandit20

```
bandit19@bandit:~$ ./bandit20-do 
Run a command as another user.
  Example: ./bandit20-do id
bandit19@bandit:~$ ./bandit20-do ls /etc/bandit_pass
bandit0   bandit12  bandit16  bandit2   bandit23  bandit27  bandit30  bandit4  bandit8
bandit1   bandit13  bandit17  bandit20  bandit24  bandit28  bandit31  bandit5  bandit9
bandit10  bandit14  bandit18  bandit21  bandit25  bandit29  bandit32  bandit6
bandit11  bandit15  bandit19  bandit22  bandit26  bandit3   bandit33  bandit7
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```

### Contraseña encontrada
* GbKksEFF4yrVs6il55v6gwY5aVje5f0j