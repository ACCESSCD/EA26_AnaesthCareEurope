# How to Build a GitHub Pages Reference Site with Claude Code
### Step-by-step guide for creating a downloadable PDF library webpage

> **Note:** This manual covers every step used to build the EA26 Anaesthesia Care Europe reference page.  
> Screenshots can be added by pasting images into this document.  
> The exact prompts typed into Claude are shown in blue boxes throughout.

---

## Before You Start — Common Mistakes to Avoid

- ❌ Do **not** open a pre-existing, unrelated PyCharm project and work in it by mistake  
- ❌ Do **not** try to create the webpage manually without Claude — use Claude Code in the terminal  
- ❌ Do **not** skip setting up the virtual environment  
- ✅ Always open the **correct** folder in PyCharm before starting  
- ✅ Always run Claude Code from inside the PyCharm terminal

---

## STEP 1 — Create a New Project in PyCharm

1. Open **PyCharm**
2. On the welcome screen click **New Project**  
   *(or go to File → New Project if PyCharm is already open)*
3. In the **Location** field, type the full path to your new project folder, e.g.:

   ```
   C:\Users\carol\PycharmProjects\EA26_AnaesthCareEurope
   ```

   > ⚠️ **Check the folder name carefully before clicking Create.**  
   > Previously the wrong folder (`Anaesthesia_for_CD_EA2026`) was opened by mistake.

4. Under **Python Interpreter**, select **New environment using Virtualenv**  
   *(PyCharm can set this up for you, or you can do it in Step 3 below)*
5. Click **Create**

---

## STEP 2 — Open the Terminal Inside PyCharm

1. At the bottom of the PyCharm window, click the **Terminal** tab  
   *(keyboard shortcut: `Alt + F12`)*
2. The terminal opens at the bottom of the screen, already pointing to your project folder  
3. Confirm you are in the right place — the prompt should show your project path:

   ```
   PS C:\Users\carol\PycharmProjects\EA26_AnaesthCareEurope>
   ```

---

## STEP 3 — Set Up a Virtual Environment

Type the following prompt into Claude Code (see Step 4 to start Claude first), **or** run it yourself in the terminal:

```
python -m venv venv
```

What Claude did:
```powershell
python -m venv venv
.\venv\Scripts\python.exe --version
# Output: Python 3.14.4
```

The virtual environment is created in a folder called `venv/` inside your project.  
To activate it manually at any time:
```powershell
.\venv\Scripts\Activate.ps1
```

---

## STEP 4 — Start Claude Code in the Terminal

In the PyCharm terminal, type:

```
claude
```

Press **Enter**. Claude Code will start and you will see a prompt where you can type instructions in plain English.

---

## STEP 5 — Set Up the Virtual Environment via Claude

Once Claude is running, type exactly:

> **Prompt used:**
> ```
> set up a virtual environment
> ```

Claude automatically ran:
```powershell
python -m venv venv
.\venv\Scripts\python.exe --version
```
Result: Virtual environment created with Python 3.14.4.

---

## STEP 6 — Connect the Project to Your GitHub Repository

> **Prompt used:**
> ```
> this is the github address https://github.com/ACCESSCD/EA26_AnaesthCareEurope connect to this
> ```

Claude checked the existing remotes with:
```bash
git remote -v
```

The repository was already connected. If it had not been, Claude would have run:
```bash
git remote add origin https://github.com/ACCESSCD/EA26_AnaesthCareEurope
```

---

## STEP 7 — Push the Initial Project to GitHub

> **Prompt used:**
> ```
> do it for me
> ```

Claude ran:
```bash
git add main.py
git commit -m "Initial commit"
git push -u origin main
```

Result: `main.py` was committed and pushed to the `main` branch on GitHub.  
*(The `.idea/` PyCharm folder was intentionally excluded as it contains IDE-specific settings.)*

---

## STEP 8 — Copy Your Source Files into the Project

> **Prompt used:**
> ```
> "C:\Users\carol\PycharmProjects\Anaesthesia_for_CD_EA2026" copy contents to here
> ```

Claude first listed what was in the source folder, then ran:
```powershell
Copy-Item "C:\Users\carol\PycharmProjects\Anaesthesia_for_CD_EA2026\*" `
  -Destination "C:\Users\carol\PycharmProjects\EA26_AnaesthCareEurope\" `
  -Recurse -Exclude ".idea"
```

Files copied (11 total):
| File | Description |
|------|-------------|
| `40 year workforce survey update.pdf` | Workforce survey |
| `Anaesthesia - 2008 - Kinsella...pdf` | Kinsella prospective audit |
| `Anaesthesia - 2022 - Patel...pdf` | Patel neuraxial study |
| `Are we finally tackling...pdf` | Pain review |
| `Charles intraoperative pain...pdf` | Charles 2024 Anesthesiology |
| `editorial IJOA sultan Landau 2025.pdf` | Sultan & Landau editorial |
| `Guglielminotti avoidable GA.pdf` | Avoidable GA study |
| `Juang 2017 national GA rates USA.pdf` | US national GA rates |
| `o carroll incidence of pain...pdf` | O'Carroll 2025 Anesthesiology |
| `RCOG pdf.pdf` | RCOG guideline |
| `Shibli RCOA source...pdf` | RCOA anaesthetic survey |
| `Skyline.svg` | Design graphic |

---

## STEP 9 — Create the Webpage

> **Prompt used:**
> ```
> i would like a web page. the design should be according to the svg. this should be a github page 
> where each file should be downloadable by clicking a link on the page, there should also be a 
> short summary of each source. The title of the page should be: Anaesthesia practice for 
> caesarean delivery in Europe. Presented Prof Carolyn Weiniger
> ```

Claude:
1. Read the `Skyline.svg` file to extract the colour palette:
   - **Navy blue** `#233187` — used for the header, card numbers, and buttons
   - **Peach** `#FFD1B0` — used for accents, presenter name, and the skyline graphic
2. Created `index.html` — a fully styled page with:
   - A navy header with the title and skyline banner
   - 11 numbered cards, one per PDF, each with a summary and Download button
3. Created `.nojekyll` — a blank file that tells GitHub Pages not to process files with special characters in their names (important for PDFs with spaces)
4. Committed and pushed both files plus all PDFs and the SVG:

```bash
git add index.html .nojekyll *.pdf Skyline.svg
git commit -m "Add GitHub Pages site with PDF reference library"
git push origin main
```

---

## STEP 10 — Enable GitHub Pages

1. Go to your GitHub repository in a browser:  
   **https://github.com/ACCESSCD/EA26_AnaesthCareEurope**

2. Click the **Settings** tab (top menu of the repository)

3. In the left sidebar, click **Pages**

4. Under **Source**, select:
   - Branch: **main**
   - Folder: **/ (root)**

5. Click **Save**

6. GitHub will display a banner:  
   *"Your site is ready to be published at https://accesscd.github.io/EA26_AnaesthCareEurope/"*

7. Wait 1–2 minutes, then visit:  
   **https://accesscd.github.io/EA26_AnaesthCareEurope/**

---

## Summary of All Prompts Used (in order)

Copy and paste these into Claude Code next time:

```
1. set up a virtual environment

2. this is the github address https://github.com/ACCESSCD/EA26_AnaesthCareEurope connect to this

3. do it for me

4. "C:\Users\carol\PycharmProjects\Anaesthesia_for_CD_EA2026" copy contents to here

5. i would like a web page. the design should be according to the svg. this should be a github 
   page where each file should be downloadable by clicking a link on the page, there should also 
   be a short summary of each source. The title of the page should be: Anaesthesia practice for 
   caesarean delivery in Europe. Presented Prof Carolyn Weiniger
```

Then complete Step 10 (GitHub Pages settings) manually in the browser.

---

## Quick-Reference Checklist for Next Time

- [ ] Open PyCharm → New Project → correct folder name
- [ ] Open Terminal (`Alt + F12`)
- [ ] Type `claude` to start Claude Code
- [ ] Prompt: *set up a virtual environment*
- [ ] Prompt: *connect to GitHub repo URL*
- [ ] Prompt: *push to GitHub*
- [ ] Prompt: *copy files from source folder*
- [ ] Prompt: *create the webpage* (with title, design, download links, summaries)
- [ ] GitHub → Settings → Pages → Deploy from main / root → Save
- [ ] Visit `https://accesscd.github.io/[repo-name]/`

---

*Manual written May 2026 — EA26 Anaesthesia Care Europe project*
