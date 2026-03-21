# CTF Write-up : Riddle Registry

## Avant-propos  
Conformément aux bonnes pratiques des CTF, le flag final est partiellement masqué dans ce document.

## Description  

**Objectif :**  
Retrouver un flag caché dans un fichier PDF qui semble contenir uniquement des données inutilisables.

- **Nom du challenge :** Riddle Registry  
- **Plateforme :** PicoCTF  
- **Catégorie :** Forensic 
- **Difficulté :** Facile  
- **Fichiers fournis :** confidential.pdf

1. Inspection des métadonnées du fichier 

```bash 
exiftool confidential.pdf
```
-> Pour "Author" nous obtenons "Author : cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9jOTk5ZTJhNH0=" ce qui apparaît comme une chaîne encodée suspecte.

2. Identification et décodage

La chaine est encodé en base64 : reconnaissable par son utilisation des caractères alphanumériques ainsi que du `=` de fin. 

**Décodage :**
```bash 
echo "cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9jOTk5ZTJhNH0=" | base64 -d
```

**Resultat :** La commande nous renvoie le flag qui commence par "picoCTF{".



