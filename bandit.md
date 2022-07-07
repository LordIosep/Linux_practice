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
```
bandit12@bandit:/tmp/random_dir$ tar -xf data5.bin
bandit12@bandit:/tmp/random_dir$ ls
binario.tar  binary  data  data5.bin  data6.bin  datos
```

Volvemos a verificar que tipo de arhivo es, con el comando `file`. 

```
bandit12@bandit:/tmp/random_dir$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
```
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

