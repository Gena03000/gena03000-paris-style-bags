https://gena03000-webhook-rss.vercel.app/update-order
export default async function handler(req, res) {
  if (req.method === "POST") {
    const product = req.body;

    // Génération d'une entrée RSS
    const item = `
    <item>
      <title>${product.title}</title>
      <link>https://www.genacampbell.shop/products/${product.handle}</link>
      <description>${product.body_html}</description>
      <pubDate>${new Date().toUTCString()}</pubDate>
      <guid>https://www.genacampbell.shop/products/${product.handle}</guid>
    </item>`;

    // À cette étape, on pourrait stocker ou renvoyer l'entrée
    // Pour l'exemple, on renvoie simplement l'item généré
    res.status(200).send(item);
  } else {
    res.status(405).send("Méthode non autorisée");
  }
}
// webhook.js
const express = require("express");
const fs = require("fs");
const app = express();
app.use(express.json());

app.post("/update-rss", (req, res) => {
  const product = req.body;
  const newItem = `
    <item>
      <title>${product.title}</title>
      <link>https://www.genacampbell.shop/products/${product.handle}</link>
      <description>${product.body_html}</description>
      <pubDate>${new Date().toUTCString()}</pubDate>
      <guid>https://www.genacampbell.shop/products/${product.handle}</guid>
    </item>
  `;

  fs.readFile("rss.xml", "utf8", (err, data) => {
    const updated = data.replace("</channel></rss>", newItem + "\n</channel></rss>");
    fs.writeFile("rss.xml", updated, () => res.sendStatus(200));
  });
});

app.listen(3000);
# Paris Style Bags – Boutique Gena Campbell

Scripts visuels pour le carrousel Ligne25 et affichage dynamique des collections féminines.  
Intégration d’un flux RSS pour suivre les nouveautés produits en continu.  
Design responsive compatible mobile et desktop, optimisé pour Shopify.

## Badges GitHub

![GitHub repo size](https://img.shields.io/github/repo-size/Gena03000/gena03000-paris-style-bags)
![GitHub last commit](https://img.shields.io/github/last-commit/Gena03000/gena03000-paris-style-bags)
![GitHub top language](https://img.shields.io/github/languages/top/Gena03000/gena03000-paris-style-bags)
![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)

## Contenu

Ce dépôt contient les composants suivants :

- `Ligne25` : Carrousel d’images des collections Belleville à Terminus.
- `style.css` : Styles CSS responsives adaptés à Shopify.
- `rss.xml` : Flux RSS des nouveaux produits ajoutés à la boutique.
- `rss-script.js` : Script JavaScript pour injecter dynamiquement les produits dans le DOM.

## Installation

1. Copier les fichiers dans les sections personnalisées du thème Shopify.
2. Insérer le carrousel Ligne25 dans une page HTML ou une section dédiée.
3. Intégrer le script `rss-script.js` dans l’en-tête ou le pied de page.
4. Générer automatiquement le flux `rss.xml` via un webhook Shopify.

## Utilisation

Le carrousel permet une navigation visuelle entre les collections de la boutique.  
Le flux RSS est conçu pour lister les nouveautés produits sans rechargement de page.  
La mise à jour automatique est recommandée via webhook produit (`products/create`).

## Roadmap

- [x] Composant Ligne25 (carrousel images)
- [x] Intégration du flux RSS des nouveautés
- [ ] Mise en place du webhook serveur pour générer `rss.xml`
- [ ] Ajout du fichier de démonstration `index.html`
- [ ] Documentation visuelle dans le Wiki du dépôt

## Crédits

Développé par [Gena Campbell](https://www.genacampbell.shop)  
Design graphique et univers produit : ligne féminine, parisienne, élégante.

## Licence

Ce projet est publié sous licence MIT. Vous êtes libre de le modifier et de le redistribuer sous les conditions de cette licence.
