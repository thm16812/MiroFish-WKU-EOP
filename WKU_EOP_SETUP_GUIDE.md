# WKU EOP MiroFish Setup Guide
**Plain-English Guide for Non-Developers**
**Scenario: Tornado Warning — Maximum-Capacity Game Day**

---

## Before You Start: What You Need

You need two API keys before MiroFish will run. Both have free tiers.

| Key | Where to Get It | Cost |
|---|---|---|
| LLM API key (the AI brain) | https://bailian.console.aliyun.com/ (Alibaba) or https://platform.openai.com/ (OpenAI) | Pay-per-use; see cost estimate below |
| Zep Cloud key (agent memory) | https://app.getzep.com/ | Free monthly quota is enough |

---

## Step 1: Install Node.js (One-Time, Required)

MiroFish's web interface runs on Node.js. You need to install it once.

1. Open your web browser and go to: **https://nodejs.org**
2. Click the big green **"LTS"** download button (Long Term Support — the stable version)
3. Run the downloaded installer
4. **Important:** When the installer asks about "Tools for Native Modules," check that box
5. Click through and finish the install
6. Restart your computer after it finishes

To confirm it worked: open Command Prompt and type `node -v` — you should see a version number like `v22.x.x`

> Note: Node.js requires administrator permission to install on Windows. If you see a UAC
> prompt asking "Do you want to allow this app to make changes?", click Yes.

---

## Step 2: Fill In Your API Keys

1. Open the file called **`.env`** in the MiroFish folder
   - Note: This file starts with a dot — Windows may hide it. In File Explorer,
     go to View → Show → Hidden Items to see it
   - Or open it directly: right-click → Open With → Notepad
2. Replace `your_api_key_here` with your LLM API key
3. Replace `your_zep_api_key_here` with your Zep Cloud key
4. Save the file (Ctrl+S)
5. Do not share this file — it contains your private keys

---

## Step 3: Install MiroFish Dependencies

Open **Command Prompt** (or PowerShell) and type these commands one at a time:

```
cd "C:\Users\payet\OneDrive\Documents\Claudeworkspace\Mirofish\MiroFish"
npm run setup:all
```

This downloads all the software pieces MiroFish needs. It may take 3–5 minutes.
You'll see a lot of text scrolling — that's normal. Wait for it to finish.

If you see errors, see the Troubleshooting section at the bottom.

---

## Step 4: Start MiroFish

In the same Command Prompt window, type:

```
npm run dev
```

You'll see text from two services starting up — "backend" (green) and "frontend" (cyan).
When you see something like `ready on http://localhost:3000`, it's ready.

Open your web browser and go to: **http://localhost:3000**

You should see the MiroFish interface.

> To stop MiroFish: go back to the Command Prompt window and press **Ctrl + C**

---

## Step 5: Upload Your Seed Material

Your seed material is the background information that MiroFish uses to build the simulation world.
For our tornado/game day scenario, the seed file is **`wku_eop_seed_template.md`** in the MiroFish folder.

**How to upload:**
1. In the MiroFish web interface, look for an **"Upload"** button or **"Seed Material"** section
2. Click it and select the file `wku_eop_seed_template.md`
3. Wait for MiroFish to process it — it will extract locations, population data, and scenario details
4. You'll see it confirm that it has built the simulation world

**Tip:** If you receive official EOP documents via dispatch, add the key details
(shelter locations, communication protocols, population figures) into the seed template
before uploading. The more real data you provide, the better the simulation.

---

## Step 6: Type Your Prediction Query

After uploading the seed, you'll see a text input area for your prediction question.

1. Open the file **`wku_eop_query_template.md`** in a text editor (Notepad is fine)
2. Choose a query from the list — start with **Query 1** or **Query 2**
3. Copy it (Ctrl+C)
4. Paste it into the MiroFish prediction input (Ctrl+V)
5. Edit any bracketed text [LIKE THIS] if needed
6. Press Submit (or Enter)

---

## Step 7: Set Your Simulation Rounds

After submitting your query, MiroFish will ask how many rounds to run.

**What is a "round"?**
Think of a round as one tick of the clock in your simulated scenario. In each round, every
agent (simulated person) reads what's happening, thinks about it, and reacts. More rounds
= more time simulated = more realistic long-term behavior, but also more cost.

**Recommended starting points:**

| Goal | Rounds | Agents | Notes |
|---|---|---|---|
| Quick test to see if it works | 5 | 10 | Very cheap, basic output |
| Decent WKU EOP scenario run | 20–30 | 15–20 | Good balance of quality and cost |
| Full detailed simulation | 35–40 | 20–25 | Max recommended before costs climb |

**Important:** Do not exceed 40 rounds until you understand the cost. See below.

---

## Step 8: Read the Output

When the simulation finishes, MiroFish generates two things:

**1. Prediction Report**
A written summary that answers your prediction question. It will describe:
- How the crowd behaved overall
- Which groups complied, froze, or acted dangerously
- Key turning points in crowd behavior
- Specific recommendations for WKU EOP (if your query asked for them)

**2. Agent Interaction View**
An interactive view of what each individual simulated person did and said during the scenario.
You can click on any agent and ask them questions — for example:
- "Why didn't you go to the shelter immediately?"
- "What did you hear from other people around you?"
- "What would have made you comply faster?"

This is especially useful for understanding behavior that surprised you in the report.

---

## Step 9: Save Your Results

**To save the prediction report:**
- Look for a **"Export"** or **"Download Report"** button in the interface
- Save it as a PDF or copy the text into a Word document
- Name your file with the scenario and date: e.g., `WKU_Tornado_GameDay_2026-03-24.pdf`

**For EOP review meetings:**
- The prediction report can be printed and distributed directly
- The agent interaction view is best demonstrated live on a laptop
- Key quotes from agents can be copied and included in after-action reports

---

## API Cost Awareness

LLM tokens are the "fuel" that powers every agent's thinking. You are charged per 1,000 tokens.

**Rough estimate for Alibaba Qwen-Plus:**

| Simulation Size | Tokens Used (approx) | Estimated Cost |
|---|---|---|
| 10 agents × 10 rounds | ~50,000 tokens | ~$0.05–$0.15 |
| 20 agents × 30 rounds | ~600,000 tokens | ~$0.60–$2.00 |
| 25 agents × 40 rounds | ~1,200,000 tokens | ~$1.50–$5.00 |

> Costs vary by provider and model. OpenAI GPT-4o is roughly 10–20x more expensive than Qwen-Plus
> for the same simulation. Start with Qwen-Plus or another cost-effective provider.

**Tips to control cost:**
- Always start with 5–10 rounds to verify everything is working before a full run
- Zep Cloud memory is separate from LLM cost and is free within monthly limits
- You can re-run only parts of a simulation by adjusting the query, not the full seed

---

## Troubleshooting

### "npm is not recognized"
Node.js is not installed. Go back to Step 1 and install it, then restart Command Prompt.

### "Port 3000 is already in use"
Something else is using that port. In Command Prompt: `npx kill-port 3000` then try again.
Or try opening http://localhost:3001 — MiroFish may have moved to the next available port.

### "Port 5001 is already in use"
Same issue for the backend. Run: `npx kill-port 5001`

### "uv: command not found" / backend won't start
`uv` (Python package manager) needs to be in your PATH. Restart Command Prompt after installation.
If still not found: `py -m pip install uv` as a fallback.

### "ZEP_API_KEY invalid" / memory errors
Your Zep key in the `.env` file may have extra spaces or be missing. Open `.env` in Notepad
and confirm the key is on one line with no spaces before or after the `=` sign.

### "LLM API error" / simulation won't start
Check that your LLM API key is valid and has available credits/quota. Log in to your provider's
dashboard and verify the key is active. Also confirm `LLM_BASE_URL` matches your provider.

### Simulation produces very generic output
Your seed material may be too sparse. Go back to `wku_eop_seed_template.md`, fill in more
specific WKU details (real building names, population counts, communication protocols),
and re-upload before running again.

### "Docker" errors when not using Docker
You do not need Docker for the source code installation. If you see Docker-related errors,
you may have accidentally run `docker compose up` instead of `npm run dev`.

---

## When You Get EOP Documents via Dispatch

When your official WKU EOP documents arrive:

1. Open `wku_eop_seed_template.md`
2. Update sections marked [CONFIRM] with real figures from the documents
3. Fill in any sections marked [FILL IN]
4. Add specific shelter location names, capacity numbers, and communication protocols
5. Save the file and re-upload it to MiroFish before your next simulation run
6. Your query template queries will automatically become more accurate

---

*Guide version: 1.0 | Written for WKU Emergency Management staff | March 2026*
*Contact WKU IT Help Desk or your simulation coordinator for technical support*
