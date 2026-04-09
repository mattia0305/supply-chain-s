# Supply Chain Simulator

Simulatore web interattivo di Supply Chain per studenti universitari. Multi-utente, real-time, con dashboard professore.

## Stack tecnologico

| Layer | Tecnologia | Hosting (gratuito) |
|-------|-----------|---------------------|
| Frontend + API | Next.js 16 + TypeScript | Vercel (free) |
| Database | PostgreSQL via Supabase | Supabase (free tier) |
| Auth | Supabase Auth | Supabase |
| Real-time | Supabase Realtime | Supabase |
| UI | Tailwind CSS + Recharts | — |

## Setup (10 minuti)

### 1. Crea progetto Supabase

1. Vai su [supabase.com](https://supabase.com) → crea account gratuito
2. Crea un nuovo progetto
3. Vai su **SQL Editor** → incolla il contenuto di `supabase/schema.sql` → esegui
4. Vai su **Settings → API** e copia:
   - `Project URL` → `NEXT_PUBLIC_SUPABASE_URL`
   - `anon public key` → `NEXT_PUBLIC_SUPABASE_ANON_KEY`

### 2. Configura variabili d'ambiente

Modifica `.env.local` nella root del progetto:

```env
NEXT_PUBLIC_SUPABASE_URL=https://xxxxxxxxxxxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbGci...
```

### 3. Deploy su Vercel

```bash
npm install -g vercel
vercel --prod
```

Oppure importa direttamente da GitHub su vercel.com e aggiungi le env vars nelle settings.

### 4. Sviluppo locale

```bash
npm install
npm run dev
# Apri http://localhost:3000
```

---

## Flusso di una sessione

### Professore
1. Registrati come **Professore** su `/auth/register?role=professor`
2. Crea sessione: nome, difficoltà, n. team, periodi di simulazione
3. Condividi il **codice** (6 caratteri) agli studenti
4. Apri la fase di **configurazione** quando tutti sono in lobby
5. Monitora team in real-time (tab Team / Catena)
6. Inietta eventi dalla tab **Eventi**
7. Avvia simulazione → analizza KPI

### Studente
1. Registrati come **Studente** su `/auth/register?role=student`
2. Inserisci il codice → scegli team e ruolo
3. Imposta i parametri della tua azienda → "Sono pronto"
4. Attendi simulazione → analizza risultati

---

## Ruoli

| Ruolo | Emoji | Decisioni chiave |
|-------|-------|-----------------|
| Fornitore | 🏭 | Capacità produttiva, costo, lead time |
| Produttore | ⚙️ | Batch size, efficienza, costi fissi |
| Magazzino | 🏪 | Posizione, capacità, costo stoccaggio |
| Distributore | 🚛 | Modalità trasporto, tempi, flotta |
| Rivenditore | 🛒 | Domanda media, scorte, prezzo vendita |

## Difficoltà

| Livello | Parametri | Scenario |
|---------|-----------|----------|
| 🟢 Facile | 3-4/ruolo | Stabile, poche variabili |
| 🟡 Media | 6-8/ruolo | Variabilità, qualità, affidabilità |
| 🔴 Difficile | 10+/ruolo | Alta incertezza, multi-modale, backup |

## KPI calcolati

Service Level · Fill Rate · Ricavi · Costi · Profitto · Margine Lordo ·
On-Time Delivery · Ciclo Ordine · Rotazione Scorte · Stockout · Bullwhip Index · CO₂

## Struttura

```
app/
├── auth/                   # Login / Registrazione
├── professor/              # Dashboard professore + gestione sessioni
└── session/[id]/           # Lobby → Configurazione → Simulazione → Risultati

lib/simulation/engine.ts    # Motore di simulazione (puro TS, no server)
types/index.ts              # Tutti i tipi e costanti
supabase/schema.sql         # Schema DB (esegui su Supabase)
```
"# supply-chain-sim" 
