# Fresh Agent Prompt — WKU EOP MiroFish Simulation
**Paste this entire document as your opening message to a new Claude Code session.**

---

## Who I Am & What I'm Doing

I work in emergency management at Western Kentucky University. I am using **MiroFish** — an AI-powered crowd simulation engine — to test WKU's Emergency Operations Plan (EOP) by simulating how a crowd of ~30,000 people behaves during a **tornado warning on a maximum-capacity home football game day** at L.T. Smith Stadium.

This is not a coding project — it is an emergency preparedness tool. I need your help getting MiroFish running and executing simulations.

---

## What Has Already Been Done

This repo (`MiroFish-WKU-EOP`) is a clone of MiroFish with the following files already created:

| File | Purpose |
|---|---|
| `wku_eop_seed_template.md` | Background scenario data to upload into MiroFish as seed material |
| `wku_eop_query_template.md` | 14 pre-written prediction queries ready to paste into MiroFish |
| `WKU_EOP_SETUP_GUIDE.md` | Plain-English setup guide (non-developer audience) |
| `.env` | Environment config file — needs API keys filled in |

The Python package manager `uv` is already installed on this machine.

---

## What Still Needs To Be Done — In Order

### 1. Verify Node.js is installed
Run: `node -v`
- If it returns a version number (e.g. `v22.x.x`), proceed.
- If not, go to https://nodejs.org, download and install the LTS version, then restart.

### 2. Get API Keys (if not already in .env)
Open the `.env` file. If `LLM_API_KEY` and `ZEP_API_KEY` still say `your_api_key_here`, the user needs to provide them.

- **LLM API key** → https://bailian.console.aliyun.com/ (Alibaba Qwen, recommended) or https://platform.openai.com/
- **Zep Cloud key** → https://app.getzep.com/ (free tier is sufficient)

Ask the user: *"Do you have your LLM API key and Zep Cloud key ready to enter?"*

### 3. Fill in .env
Replace placeholder values in `.env` with real keys. Do not commit `.env` to git.

### 4. Install dependencies
```
npm run setup:all
```
Fix any errors. Fall back to Docker if source install fails:
```
cp .env.example .env
docker compose up -d
```

### 5. Start the application
```
npm run dev
```
Confirm:
- Frontend running at http://localhost:3000
- Backend running at http://localhost:5001

### 6. Incorporate EOP documents (IMPORTANT)
The user plans to bring in official WKU EOP documents via dispatch. When they provide them:
- Extract: shelter locations, population capacities, official protocol names, communication procedures, named scenarios
- Update `wku_eop_seed_template.md` with real data from those documents
- The more specific the seed, the more accurate the simulation

### 7. Run the first simulation
1. Open http://localhost:3000
2. Upload `wku_eop_seed_template.md` as seed material
3. Paste **Query 1** from `wku_eop_query_template.md`
4. Set rounds to **20**, agents to **15** for the first test run
5. Review the prediction report output

---

## The Core Scenario (Summary)

- **Event:** WKU home football game, L.T. Smith Stadium at full capacity (~22,000 in stadium, ~30,000+ on campus total)
- **Emergency:** Tornado WARNING issued mid-game (not a watch — a confirmed tornado tracking toward campus)
- **Protocol:** Shelter-in-place — crowd directed to stadium lower concourse, DSU basement, nearest concrete structures
- **Key unknowns to simulate:** compliance rates, tailgater vulnerability, alert delay impact, misinformation spread, visiting fan behavior

---

## Key Files & Paths

- **Project root:** `C:\Users\payet\OneDrive\Documents\Claudeworkspace\Mirofish\MiroFish\`
- **GitHub repo:** https://github.com/thm16812/MiroFish-WKU-EOP
- **Setup guide:** `WKU_EOP_SETUP_GUIDE.md` — read this if anything is unclear
- **Seed template:** `wku_eop_seed_template.md` — upload this to MiroFish
- **Query template:** `wku_eop_query_template.md` — paste queries from here

---

## Important Notes for the Agent

- The user is **not a developer** — explain technical steps in plain English
- Do not over-engineer. The goal is to get simulations running, not to rewrite the codebase
- `.env` must never be committed to git (it is gitignored)
- Start simulation runs at ≤40 rounds to manage LLM API costs
- When EOP documents arrive, incorporate real WKU data into the seed template before running
- The simulation output (prediction report + agent interaction view) should be saved/exported for use in EOP review meetings

---

*Created: March 2026 | WKU Emergency Management | MiroFish-WKU-EOP*
