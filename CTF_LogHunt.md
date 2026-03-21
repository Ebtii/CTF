# CTF Write-up : Log Hunt

## Avant-propos  
Conformément aux bonnes pratiques des CTF, le flag final est partiellement masqué dans ce document.

## Description  

**Objectif :**  
Reconstituer un flag à partir de fragments dispersés dans des logs serveur.

- **Nom du challenge :** Log Hunt  
- **Plateforme :** PicoCTF  
- **Catégorie :** Forensic  
- **Difficulté :** Facile  
- **Fichiers fournis :** server.log  

---

## Résolution  

### 1. Identification du fichier  

On commence par vérifier le type du fichier :

```bash
file server.log
server.log: ASCII text
```
### 2. Recherche de fragments du flag

```bash
strings server.log | grep -i "picoCTF"
```
-> Le flag est partagé sur plusieurs lignes du log dont chacune ont pour point commun l'expressions "FLAGPART:".

**Recherche plus affinée**

```bash
strings server.log | grep -i "FLAGPART:" | uniq | sort -n
```

-> Filtrage par expression et tri afin de retrouver chaque partie du flag dans le bon ordre

### 3. Resultat 

**Resultat :** Le flag complet est divisé en 4 parties dont la première commence par la signature "picoCTF{". 
