# 💈 MC BARBER — Carta Fedeltà Digitale

Sito vetrina + carta fedeltà digitale per barbieri. Stack: HTML + CSS + JS + Firebase Firestore. Deploy su GitHub Pages. **Costo: 0€**

## 🔗 Link di accesso

- **Sito vetrina + carta fedeltà:** https://easyvetrina.github.io/mcbarber/
- **Pannello admin:** https://easyvetrina.github.io/mcbarber/admin.html
- **Password admin:** `mcbarber2026`

---

## 📁 Struttura file

```
barbiere/
├── index.html      → Sito vetrina + registrazione/login cliente
├── admin.html      → Pannello barbiere (password protetto)
└── README.md       → Queste istruzioni
```

---

## 🔥 STEP 1 — Configura Firebase

1. Vai su **https://console.firebase.google.com**
2. Clicca **"Aggiungi progetto"** → dai un nome (es. `barberclub-mario`)
3. Disabilita Google Analytics (non serve) → **Crea progetto**
4. Nel menu laterale clicca **"Firestore Database"** → **"Crea database"**
   - Scegli **"Modalità test"** (per ora va bene)
   - Scegli la regione **europe-west** → Avanti
5. Ora vai su **"Impostazioni progetto"** (icona ingranaggio in alto a sinistra)
6. Scorri fino a **"Le tue app"** → clicca l'icona **`</>`** (Web)
7. Registra l'app con un nome → copia il blocco `firebaseConfig`

### Incolla la config in entrambi i file

Nei file `index.html` e `admin.html` trova questo blocco e sostituisci con i tuoi dati reali:

```js
const firebaseConfig = {
  apiKey: "LA_TUA_API_KEY",           // ← sostituisci
  authDomain: "IL_TUO_PROGETTO.firebaseapp.com",
  projectId: "IL_TUO_PROGETTO",
  storageBucket: "IL_TUO_PROGETTO.appspot.com",
  messagingSenderId: "IL_TUO_SENDER_ID",
  appId: "IL_TUO_APP_ID"
};
```

---

## 🔐 STEP 2 — Cambia la password admin

In `admin.html` trova questa riga e cambia la password:

```js
const ADMIN_PASSWORD = "barbiere2024";  // ← cambia questa!
```

---

## 🌐 STEP 3 — Deploy su Netlify

1. Vai su **https://netlify.com** → registrati gratis con email
2. Clicca **"Add new site"** → **"Deploy manually"**
3. **Trascina la cartella `barbiere/`** nella zona di upload
4. Netlify ti dà un URL tipo `https://amazing-name-123.netlify.app`
5. (Opzionale) Clicca **"Domain settings"** per cambiare il nome in qualcosa di carino

---

## 🐙 STEP 4 — Carica su GitHub (backup)

```bash
git init
git add .
git commit -m "Prima versione MC BARBER"
git remote add origin https://github.com/TUO_USERNAME/barberclub.git
git push -u origin main
```

---

## ✂️ Come si usa

### Lato cliente (index.html)
1. Il cliente va sul sito
2. Si registra con nome + numero di telefono
3. Vede la sua carta con i timbri
4. Ad ogni visita mostra la schermata al barbiere

### Lato barbiere (admin.html)
1. Il barbiere va su `/admin.html`
2. Inserisce la password
3. Cerca il cliente e clicca **"Timbra"**
4. Quando il cliente raggiunge il numero di timbri, clicca **"Applica sconto"** (azzera il contatore)
5. Nelle **Impostazioni** può configurare: nome salone, tipo di sconto, numero di timbri

---

## ⚙️ Personalizzazione veloce

| Cosa cambiare | Dove |
|---|---|
| Nome salone | Admin → Impostazioni |
| Tipo di sconto | Admin → Impostazioni |
| N. timbri per premio | Admin → Impostazioni |
| Password admin | `admin.html` riga `ADMIN_PASSWORD` |
| Servizi e prezzi | `index.html` sezione `.services-grid` |
| Colori | `index.html` e `admin.html` sezione `:root` |

---

## 🔒 Sicurezza Firebase (importante dopo il lancio)

Quando vai live, aggiorna le **Firestore Rules** su Firebase Console:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /clienti/{doc} {
      allow read, write: if true; // OK per MVP
    }
    match /settings/{doc} {
      allow read: if true;
      allow write: if true; // proteggere in futuro con auth
    }
  }
}
```

---

## 💰 Costi

| Servizio | Piano | Costo |
|---|---|---|
| Firebase Firestore | Spark (gratuito) | 0€ |
| Netlify | Free | 0€ |
| Dominio Netlify | Incluso | 0€ |
| Dominio personalizzato (opz.) | — | ~10-15€/anno |

**Totale: 0€** (o 10-15€/anno se vuoi dominio personalizzato)
