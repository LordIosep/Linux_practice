# Bandit
## Nivel 0-1
Contraseña encontrada en readme, abri el archivo con vi

```
$ ls -la
$ vi readme
```
Para ver el contenido de estos archivos se puede usar cat, vi, nano y vim
### Contraseña encontrada
* boJ9jbbUNNfktd78OOpsqOltutMc3MY1

## Nivel 1-2
Contraseña encontrada en -, de igual manera use vi

```
$ ls -la
$ vi ./-
```
### Contraseña encontrada
* CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9

## Nivel 2-3
Contraseña encontrada en spaces in this filename, de igual manera use vi

```
$ ls -la
$ vi spaces\ in\ this\ filename
```
### Contraseña encontrada
* UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK

## Nivel 3-4
Contraseña encontrada en *./inhere/.hidden*, esta es una carpeta oculta, luego se uso cat en **hibben**

```
$ ls -la
$ cd inhere/
$ ls -la
$ cat .hidden
```
### Contraseña encontrada
* pIwrPrtPN36QITSp3EQaw936yaFoFgAB

## Nivel 4-5
Contraseña encontrada en *./inhere*, al entrar se ve muchos archivos que no muetran que son, para eso se usa **file**

```
$ ls -la
$ file ./inhere/* //mostrara los archivos
$ cat ./inhere/-file07
```
![](https://github.com/LordIosep/Linux_practice/blob/main/Imagenes/File.PNG)

### Contraseña encontrada
* koReBOKuIDDepwhWk7jZC0RTdopnAYKh

## Nivel 5-6
Contraseña encontrada en *./inhere/maybehere07/.file2*, para este reto se uso el comando **find**.

```
$ ls -la
$ find . -type f -readable ! -executable -size 1033c
$ cat ./inhere/-file07
```
* Flags Find

Opciones        | Descripción                                                                                  
--------------- | ----------------------------------------------------------------------------------------
`. O ./ `       | Consulte el directorio de trabajo actual                                                     
`-type f`       | Coincidan con archivos que son **legibles**.                                                 
`-executable`   | Coincidan con los archivos que son **directorios ejecutables  &  que se pueden buscar**      
`! -executable` | Coincidan con archivos que **NO** son ejecutables & directorios que **NO** se pueden buscar  
`-size 1033c`   | El archivo usa **1033** unidades de espacio. `c` se refiere a **bytes** .                    

### Contraseña encontrada
* DXjZPULLxYr17uwoI01bNLQbtFemEgo7

## Nivel 6-7
En este nivel se encotro la contraseña en */var/lib/dpkg/info/bandit7.password*, se logro gracias al comando **find**, que sirve para buscar archivos.
```
$ find / -user bandit7 -group bandit6 -size 33c  //buscara con el usuario bandit7 con el grupo bandit6 con un tamaño 33 bytes
```
![](https://github.com/LordIosep/Linux_practice/blob/main/Imagenes/Bandit6.PNG)

Para remover los permisos denegados

```
$ find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
 /var/lib/dpkg/info/bandit7.password
$ cat /var/lib/dpkg/info/bandit7.password
```

### Contraseña encontrada
* HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
