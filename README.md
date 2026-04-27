
<html lang="fr">
<head>
<meta charset="UTF-8">
<title>Havana Parfums</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@500;700&display=swap" rel="stylesheet">

<style>
:root {
  /* ألوان الخلفية الأساسية */
  --bg-homme-base: #6f8ea6; /* الأزرق الغامق الذي اخترته */
  --bg-femme-base: #fce4ec; /* الوردي الفاتح */
  
  --card: #fff;
  --text: #111;
  --gold: #d4af37;
  
  /* لون البرق الذهبي مع شفافية خفيفة */
  --lightning-gold: rgba(212, 175, 55, 0.2); 
}

body {
  margin: 0;
  font-family: 'Playfair Display', serif;
  color: var(--text);
  transition: background-color 0.5s ease; /* تأثير انتقال لون الخلفية */
  
  /* --- بداية تعديل الخلفية المصممة (تصميم البرق) --- */
  
  /* اللون الافتراضي (الرجال) */
  background-color: var(--bg-homme-base);
  
  /* إنشاء تصميم البرق الذهبي باستخدام التدرجات الهندسية */
  background-image: 
    linear-gradient(115deg, transparent 20%, var(--lightning-gold) 20%, var(--lightning-gold) 22%, transparent 22%, transparent 40%, var(--lightning-gold) 40%, var(--lightning-gold) 42%, transparent 42%),
    linear-gradient(115deg, transparent 70%, var(--lightning-gold) 70%, var(--lightning-gold) 72%, transparent 72%, transparent 90%, var(--lightning-gold) 90%, var(--lightning-gold) 92%, transparent 92%);
  
  /* حجم التصميم المتكرر */
  background-size: 200px 350px;
  
  /* تحريك البرق ببطء ليعطي إحساساً بالفخامة */
  animation: moveLightnings 20s linear infinite;
}

/* حركة الخلفية */
@keyframes moveLightnings {
  from { background-position: 0 0, 0 0; }
  to { background-position: 200px 350px, -200px -350px; }
}

/* ضمان أن الحاوية الرئيسية شفافة لتظهر الخلفية */
.container {
  display: flex;
  gap: 10px;
  background: transparent;
}
/* --- نهاية تعديل الخلفية المصممة --- */

/* HEADER */
.header {
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  align-items: center;
  padding: 15px 25px;
  background: rgba(0,0,0,0.95);
  backdrop-filter: blur(10px);
  position: sticky;
  top: 0;
  z-index: 1000;
}

.logo {
  text-align: center;
}

.logo img {
  height: 60px;
}

/* ACTIONS */
.actions {
  display: flex;
  gap: 12px;
  justify-content: flex-end;
}

.icon-btn {
  background: transparent;
  border: 1px solid var(--gold);
  color: var(--gold);
  padding: 9px;
  border-radius: 50%;
  cursor: pointer;
  transition: 0.3s;
}

.icon-btn:hover {
  background: var(--gold);
  color: black;
  transform: scale(1.1);
}

/* TABS */
.tabs {
  display: flex;
  justify-content: center;
  gap: 20px;
  padding: 25px;
}

.tab {
  padding: 10px 28px;
  border: 1px solid var(--gold);
  border-radius: 30px;
  cursor: pointer;
  transition: 0.3s;
  background: white;
}

.tab.active,
.tab:hover {
  background: var(--gold);
  color: black;
}

/* PANIER */
#panier {
  width: 320px;
  background: #fff;
  padding: 20px;
  display: none;
  border-left: 2px solid var(--gold);
  box-shadow: -5px 0 15px rgba(0,0,0,0.05);
}

#liste-panier div {
  display: flex;
  justify-content: space-between;
  margin-bottom: 8px;
}

/* PRODUITS */
#produits {
  flex: 1;
  padding: 25px;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 25px;
}

.produit {
  background: var(--card);
  padding: 18px;
  border-radius: 15px;
  text-align: center;
  transition: 0.3s;
  border: 1px solid #eee;
  box-shadow: 0 5px 15px rgba(0,0,0,0.05);
}

.produit:hover {
  border: 1px solid var(--gold);
  transform: translateY(-8px);
  box-shadow: 0 10px 25px rgba(0,0,0,0.08);
}

.produit img {
  width: 100%;
  height: 170px;
  object-fit: contain;
  margin-bottom: 10px;
}

button {
  margin-top: 10px;
  background: transparent;
  border: 1px solid var(--gold);
  color: var(--gold);
  padding: 7px 15px;
  cursor: pointer;
  transition: 0.3s;
  border-radius: 20px;
}

button:hover {
  background: var(--gold);
  color: black;
}

/* RESPONSIVE */
@media(max-width:768px){
  .container { flex-direction: column; }
  #panier { width: 100%; }
}
</style>
</head>

<body>

<div class="header">
  <div></div>

  <div class="logo">
    <img src="hvn2.png" alt="Havana Parfums">
  </div>

  <div class="actions">
    <button class="icon-btn" onclick="togglePanier()">🛒</button>
    <button class="icon-btn" onclick="contact()">📞</button>
  </div>
</div>

<div class="tabs">
  <div class="tab active" onclick="changerCategorie(event,'homme')">Homme</div>
  <div class="tab" onclick="changerCategorie(event,'femme')">Femme</div>
</div>

<div class="container">
  <div id="panier">
    <h3>🛒 Panier</h3>
    <div id="liste-panier"></div>
    <h4>Total: <span id="total">0</span> DH</h4>
  </div>

  <div id="produits"></div>
</div>

<script>
const data = {
  homme: [
    { id: 1, nom: "Dior Sauvage", desc: "EDP 100ml", prix: 1200, stock: 5, img: "https://fimgs.net/mdimg/perfume/375x500.31861.jpg" },
    { id: 2, nom: "Bleu de Chanel", desc: "EDP 100ml", prix: 1350, stock: 15, img: "https://fimgs.net/mdimg/perfume/375x500.9099.jpg" }
  ],
  femme: [
    { id: 3, nom: "La Vie Est Belle", desc: "EDP 100ml", prix: 1300, stock: 12, img: "https://fimgs.net/mdimg/perfume/375x500.14982.jpg" },
    { id: 4, nom: "Black Opium", desc: "EDP 90ml", prix: 1250, stock: 6, img: "https://fimgs.net/mdimg/perfume/375x500.25324.jpg" }
  ]
};

let categorie = "homme";
let panier = {};

function changerCategorie(e, cat) {
  categorie = cat;
  
  // تبديل الكلاس Active بين الأزرار
  document.querySelectorAll(".tab").forEach(t => t.classList.remove("active"));
  e.target.classList.add("active");

  // تغيير لون الخلفية الأساسي حسب الفئة (مع الحفاظ على تصميم البرق)
  if (cat === 'homme') {
    document.body.style.backgroundColor = "#6f8ea6"; // الأزرق الغامق
  } else {
    document.body.style.backgroundColor = "#fce4ec"; // الوردي الفاتح
  }

  afficherProduits();
}

function afficherProduits() {
  const div = document.getElementById("produits");
  div.innerHTML = "";

  data[categorie].forEach(p => {
    div.innerHTML += `
      <div class="produit">
        <img src="${p.img}">
        <h4>${p.nom}</h4>
        <p>${p.desc}</p>
        <p>${p.prix} DH</p>
        <button onclick="ajouter(${p.id})">Ajouter</button>
      </div>
    `;
  });
}

function ajouter(id) {
  let produit = [...data.homme, ...data.femme].find(p => p.id === id);
  if (!panier[id]) panier[id] = { ...produit, qte: 0 };
  panier[id].qte++;
  afficherPanier();
}

function diminuer(id) {
  panier[id].qte--;
  if (panier[id].qte <= 0) delete panier[id];
  afficherPanier();
}

function afficherPanier() {
  const div = document.getElementById("panier");
  const liste = document.getElementById("liste-panier");

  let items = Object.values(panier);

  if (items.length === 0) {
    div.style.display = "none";
    return;
  }

  div.style.display = "block";
  liste.innerHTML = "";
  let total = 0;

  items.forEach(p => {
    total += p.prix * p.qte;

    liste.innerHTML += `
      <div>
        ${p.nom} (${p.qte})
        <div>
           <button onclick="ajouter(${p.id})">+</button>
           <button onclick="diminuer(${p.id})">-</button>
        </div>
      </div>
    `;
  });

  document.getElementById("total").innerText = total;
}

function togglePanier() {
  const p = document.getElementById("panier");
  p.style.display = (p.style.display === "block") ? "none" : "block";
}

function contact() {
  alert("Contact us: 0614740712");
}

// تشغيل العرض الأولي
afficherProduits();
</script>
</body>
</html>
</body>
</html>
