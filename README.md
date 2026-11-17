# Contrôle d’accès ESP32 — tableau de supervision

Interface web de supervision d’un prototype ESP32-CAM. Elle affiche une image de caméra et le dernier résultat d’analyse fourni dans un fichier JSON : détection d’humain et de visage, identité, similarité, confiance et statut d’accès.

## Contenu du dépôt

- `index.html` : tableau de bord HTML/CSS/JavaScript, adapté aux petits écrans.
- `resultat.json` : exemple de résultat d’analyse consommé par l’interface.

L’interface interroge le JSON et renouvelle l’image toutes les deux secondes. Elle ne réalise pas elle-même l’inférence ni l’authentification.

## Essai local

Avec Python 3 installé, depuis le dossier du dépôt :

```sh
python -m http.server 8000 --bind 127.0.0.1
```

Ouvrir `http://127.0.0.1:8000`. Le JSON fourni permet d’examiner l’affichage. L’image est chargée depuis l’URL Cloudinary configurée dans `index.html` ; sa disponibilité dépend du service externe. Pour une démonstration publique, utiliser une image synthétique ou autorisée et des résultats anonymisés.

## Architecture du prototype

```text
ESP32-CAM → image hébergée → interface web
Analyse externe → resultat.json → interface web
```

Le firmware, le moteur d’analyse et la commande d’ouverture ne sont pas fournis dans ce dépôt. L’indicateur « système actif » est un libellé statique, pas une vérification de disponibilité. L’interface peut conserver des résultats anciens en cas d’erreur réseau.

## Périmètre

Prototype de visualisation, sans contrôle d’accès sécurisé ni validation de performance biométrique. Les scores affichés ne sont pas une garantie d’identité. Le projet doit être présenté comme une interface de supervision IoT ; une chaîne complète de reconnaissance et d’ouverture n’est pas reproductible à partir de ce seul dépôt.
