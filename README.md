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
