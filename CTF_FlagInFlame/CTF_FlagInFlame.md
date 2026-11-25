# CTF : Flag In Flame

### Avant-propos
Conformément aux bonnes pratiques des CTF, le flag final est masqué.

### Description

**Objectif :** Retrouver le flag caché dans une image.
**Fichier fourni :** logs.txt

**Auteur :** Prince Niyonshuti N.
**Plateforme :** PicoCTF 

**Type :** Forensic

## Résolution

1. Analyse initiale avec strings
strings logs.txt | grep -E "[A-Z0-9]{10,}"

-> Aucun résultat exploitable.

Recherche plus spécifique :

strings res_decode | grep -E "^7.*D$"

-> Résultats non pertinents.

-> Le flag ne semble pas présent en clair dans le fichier.

Tentative de stéganographie avec steghide
steghide extract -sf res_decode

-> Erreur :

steghide: le format du fichier n'est pas supporté

-> Le fichier n’est pas compatible avec steghide.

Hypothèse : texte visible dans l’image (OCR)

Installation de Tesseract :

sudo apt install tesseract-ocr

Extraction du texte :

tesseract res_decode output
Analyse du résultat OCR
cat output.txt

-> On obtient du bruit, mais une chaîne attire l’attention :

7069636F4354467B666F72656E736963735F616E616C797369735F69735F616D617A696E675F35646161346132667D
Nettoyage du résultat
cat output.txt | tr -cd 'A-Z0-9\n'

-> Permet d’isoler la chaîne utile.

Identification de l’encodage

-> La chaîne contient uniquement des caractères [0-9A-F]
-> Il s’agit très probablement d’un encodage hexadécimal.

Décodage
echo "7069636F4354467B666F72656E736963735F616E616C797369735F69735F616D617A696E675F35646161346132667D" | xxd -r -p
Résultat

Le flag obtenu est :

picoCTF{forensics_analysis_is_amazing_5daa4a2f}