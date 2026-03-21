# CTF : Command & Control Niveau 2

### Avant-propos 
Conformément aux bonnes pratiques des CTF, le flag final est masqué. 

### Description 

**Objectif :** Retrouver le nom de la machine à partir d’un dump mémoire.  
**Fichier fourni :** ch2.tbz2 

**Auteur :** Thanat0s
**Plateforme :** Root-Me  

**Type :** Forensic

---

## Résolution 

1. Identification du type du fichier fourni.

```bash
file ch2.tbz2
```
-> Le fichier est un bzip2.

2. Décompression via `bunzip2` et inspection de l'image disque :

```bash 
bunzip2 ch2.tbz2
```
-> Cette commande extrait le fichier `ch2.dmp` contenu dans l'archive.

3. Verification de l'intégrité du dump mémoire 

```bash 
md5sum ch2.dmp  
e3a902d4d44e0f7bd9cb29865e0a15de  ch2.dmp  
```
-> Le fichier est donc valide

4. Identification du dump

```bash 
file ch2.dmp  
ch2.dmp: data  
```
-> Le fichier n'est pas un dump mémoire standard.

5. Analyse à l'aide de Volatility 3

```bash
vol3 -f ch2.dmp windows.info
Unsatisfied requirement plugins.Info.kernel.layer_name
Unsatisfied requirement plugins.Info.kernel.symbol_table_name
```

-> Volatility ne parvient pas à exploiter le dump.

6. Recherche avec `strings` et `grep`

```bash 
strings ch2.dmp | grep -i "^COMPUTERNAME"
```
->  Nous obtenons plusieurs occurrences de : 
```bash 
COMPUTERNAME=WIN-XXXXXXXXXXX   
COMPUTERNAME=WIN-XXXXXXXXXXX   
COMPUTERNAME=WIN-XXXXXXXXXXX 
```

**Resultat : **
Le flag est le nom de la machine. 



