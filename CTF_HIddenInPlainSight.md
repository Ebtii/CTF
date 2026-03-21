# CTF Write-up : Hidden in Plainsight

## Avant-propos  
Conformément aux bonnes pratiques des CTF, le flag final est partiellement masqué dans ce document.

## Description  

**Objectif :**  
Trouver un fichier caché dans une image JPG via stéganographie.

- **Nom du challenge :** Hidden in Plainsight  
- **Plateforme :** PicoCTF  
- **Catégorie :** Forensic 
- **Difficulté :** Facile  
- **Fichier fourni :** img.jpg  

---

## Résolution  

### 1. Inspection des métadonnées

```bash 
exiftool img.jpg
```

-> Nous remarquons le champ :  
`Comment : c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9`.
La chaîne semble encodée en base64.

### 3. Décodage Base64

```bash 
echo "c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9" | base64 -d
steghide:cEF6endvcmQ=
```

Nous décodons ensuite la deuxième partie :

```bash
echo "cEF6endvcmQ=" | base64 -d
pAzzword
```
-> Il s'agit possiblement d'un mot de passe pour pouvoir utiliser steghide.

### 4. Analyse avec steghide

**Vérification de la présence de données cachées**

```bash
steghide info img.jpg
```

-> Après avoir entré le mot de passe pAzzword, on obtient :
`embedded file "flag.txt` 
Ce qui signifie qu'un fichier est bien caché dans l’image.

### 5. Extraction du fichier

```bash
steghide extract -sf img.jpg
```
-> Un mot de passe est demandé pour pouvoir extraire le fichier `flag.txt`, celui-ci correspond à "pAzzword"

### 6. Lecture du flag

**Affichage du contenu**
```bash
strings flag.txt
```

### Résultat :

**Résultat :** le flag est affiché "picoCTF{******_**_*****_********}"
