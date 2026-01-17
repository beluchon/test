

---

📌 **Prérequis**

✅ Un compte **Cloudflare** (gratuit)  
✅ Un compte **Porkbun**  
✅ Un serveur avec **Docker/Dockge** (ex: Ubuntu + Docker)  
✅ Une application à exposer (ex: **Nginx Proxy Manager**)

---

🛒 **Étape 1 : Acheter un domaine sur Porkbun 🛒**

1.1 🌐 **Créer un compte Porkbun**  
👉 Allez sur : [porkbun.com](https://www.porkbun.com)

1.2 🎯 **Rechercher et acheter un domaine**  
👉 Dans l’interface Porkbun, recherchez votre domaine (ex: `beluchon.top`)  

---

☁️ **Étape 2 : Transférer le domaine vers Cloudflare ☁️**

2.1 🌐 **Accéder à Cloudflare**  
👉 Allez sur : [dash.cloudflare.com](https://dash.cloudflare.com)

2.2 🔄 **Ajouter un site**  
👉 Cliquez sur **“Add a site”**  
👉 Entrez votre domaine (ex: `beluchon.top`)  
👉 Sélectionnez **Plan Free → Continue**

2.3 📊 **Vérification des enregistrements DNS**  
👉 Cloudflare scanne vos DNS existants  
👉 Supprimez les enregistrements existants → **“Continue to activation”** et allez en bas

2.4 🔄 **Cloudflare Nameservers**  
👉 Cloudflare vous donne 2 nameservers à utiliser :  
`yyyy.ns.cloudflare.com`  
`TTTT.ns.cloudflare.com`  


<img width="1894" height="896" alt="tet-" src="https://github.com/user-attachments/assets/889814f6-28e6-40a9-b1c6-47931f6686c1" />


📌 **Notez-les précieusement 📌**

---

⚙️ **Étape 3 : Configurer les nameservers sur Porkbun ⚙️**

<img width="1630" height="493" alt="2025-11-07 23_31_29-Greenshot" src="https://github.com/user-attachments/assets/e24cd2d5-4539-43e8-a12c-a0b3bf1e8ac2" />


3.1 🧭 **Dans l’interface Porkbun**  
👉 Allez dans **Domain Management**  
👉 Cliquez sur votre domaine (`beluchon.top`)  
👉 Cherchez **“Nameservers”**

3.2 🧩 **Supprimer les anciens nameservers**  
👉 Supprimez les anciens enregistrements  
👉 Ajoutez les 2 nameservers de Cloudflare :  
`yyyy.ns.cloudflare.com`  
`TTTT.ns.cloudflare.com`  
👉 Cliquez sur **“Submit”**

3.3 🔄 **Retour sur Cloudflare**  
👉 Cliquez sur **“Continue”**

⏳ **Attendez quelques minutes…**

✅ **Une fois activé →**

---

🚇 **Étape 4 : Configuration Cloudflare Tunnel 🚇**

4.1 🛡️ **Accéder à Cloudflare Zero Trust**  
👉 Allez sur : [https://one.dash.cloudflare.com](https://one.dash.cloudflare.com)  
👉 Connectez-vous avec votre compte Cloudflare 🎯

4.2 🛠️ **Créer un tunnel**  
👉 Dans le menu de gauche : **Networks > Tunnels**  
👉 Cliquez sur **“Create a tunnel”**

<img width="1860" height="793" alt="2025-11-07 23_32_56-Greenshot" src="https://github.com/user-attachments/assets/eda11bba-d45f-49c2-a072-ab52bca978b9" />


👉 Nommez votre tunnel (ex: `mon-tunnel`) 📝

4.3 🧩 **Copier la commande**  
👉 Copiez la commande générée (attention : ne gardez que la partie après `eyj`)  

💾 **Collez-la dans un bloc note pour l’utiliser plus tard**

👉 Dans l’interface Cloudflare Tunnel :  
- **Hostname** : `*`  
- **Domain** : `beluchon.top`  
- **Path** : (laissez vide)  
- **Type** : `HTTP`  
- **URL** : `http://nginx-proxy-manager:80`  
👉 Cliquez sur **“Save”**

---

📡 **Étape 5 : Configurer les DNS dans Cloudflare 📡**

5.1 📥 **Ajouter un enregistrement DNS**  

<img width="1894" height="896" alt="tet-" src="https://github.com/user-attachments/assets/5b25bb12-2fff-4a2d-b5b4-6969440e3a6c" />


👉 Allez dans **DNS Records → Add Record**

- **Type** : `CNAME`
- **Name** : `*`  
- **Target** : Copiez votre ID tunnel + `.cfargotunnel.com`  
  Ex: `e9c999bb-f3de-3294-881a-5444907c0972.cfargotunnel.com`  
- Cliquez sur **“Save”**

⚠️ **Important** : Avant de lancer la stack, vous devrez copier la clé qui commence par `eyj` a coter de tunnel_token

---
aller sur dockge ou avec l'invite de commande et coller le texte dans se fichier https://github.com/beluchon/test/blob/main/docker%20compose.yml

⚠️ **Important** : Avant de lancer la stack, vous devrez copier la clé qui commence par `eyj`qui vous avez mis dans un bloc note a coter de tunnel_token


6.1 🌐 **Accéder à Nginx Proxy Manager**

👉 Ouvrez : `http://VOTRE-IP-SERVEUR:81`

🔒 **Identifiants par défaut** :  
- Email : `admin@example.com`  
- Password : `changeme`

6.2 🏗️ **Créer un Proxy Host**

👉 Dans Nginx Proxy Manager :

- **Hosts → Proxy Hosts → Add Proxy Host**

🔍 **Configuration Details** :

- **Domain Names** : `mediafusion.beluchon.top`  
- **Scheme** : `http` des fois le http ne marchera pas et faudra mettre https
- **Forward Hostname/IP** : `mediafusion` (ou nom du conteneur) et si ne marche pas vous pouvez mettre votre ip de la machine
- **Forward Port** : `80` (port du conteneur)  

👉 Cliquez sur **“Save”**
