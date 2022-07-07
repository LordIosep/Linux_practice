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
```
bandit11@bandit:~$  ls 
data.txt
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh
```
Sabemos que los caracteres en los datos están rotados por 13 caracteres. Podemos hacer que los caracteres vuelvan a su orden original usando el comando `tr`. El comando `tr`se utiliza para traducir/transformar datos de un formulario a otro.

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