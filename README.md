# ClaudeTools (`claude-tools`) — Accounting Toolkit

A Claude Code plugin providing practical workflows for accountants, bookkeepers, and financial analysts.

## Included Accounting Tools

### Slash Commands
| Command | Usage | What It Does |
| :--- | :--- | :--- |
| `/claude-tools:reconcile` | `/claude-tools:reconcile bank.csv gl.csv` | Matches bank/credit card statements against the general ledger, isolates deposits in transit, outstanding checks, and unrecorded fees, and builds a reconciliation schedule. |
| `/claude-tools:journal-entry` | `/claude-tools:journal-entry [description or file]` | Drafts a balanced double-entry journal entry table (`Debits = Credits`) with account types, memos, and GAAP/accrual notes. |
| `/claude-tools:variance-analysis` | `/claude-tools:variance-analysis p_and_l.csv` | Runs Budget vs. Actual or period-over-period flux analysis with `$` and `%` variances, Favorable/Unfavorable (`F`/`U`) tags, and materiality flags. |

### Skills (Auto-Invoked or Slash-Invoked)
- **`bank-reconciliation`** (`skills/bank-reconciliation/SKILL.md`): Step-by-step bank & credit card reconciliation procedure with adjusting journal entry proposals.
- **`expense-categorizer`** (`skills/expense-categorizer/SKILL.md`): Maps raw transaction lists to a standard Chart of Accounts, flags expenses >= $75 missing receipts, highlights 50% meals rules, and isolates potential CapEx items.

### Subagents
- **`audit-reviewer`** (`agents/audit-reviewer.md`): Specialized audit subagent that scans trial balances, general ledgers, and expense exports for out-of-balance entries, duplicate invoices/payments, round-dollar manual adjustments, and period cut-off issues.

### MCP Servers (`.mcp.json`)
- **`spreadsheet`** (`uvx excel-mcp-server stdio`): Headless spreadsheet server powered by Python `openpyxl` (**no Microsoft Excel installation required**). Gives Claude direct tools to create, read, edit, format, and apply formulas across multi-tab `.xlsx` workbooks.

---

## First-Time Setup (No Python or Excel Experience Needed)

This plugin includes a built-in spreadsheet helper (`excel-mcp-server`) so Claude can read, create, and edit `.xlsx` spreadsheet files directly—**without needing Microsoft Excel installed**.

Even though the spreadsheet server runs on Python behind the scenes, **you do not need to install Python yourself**. Instead, you only need to install a single lightweight launcher tool called **`uv`**, which automatically downloads and manages Python and the spreadsheet server for you in the background.

### Step 1: Install `uv` (One-Time Setup)

**On Windows:**
1. Click the Windows **Start** button, type **PowerShell**, and click **Windows PowerShell** to open a terminal window.
2. Copy and paste the following command into the window and press **Enter**:
   ```powershell
   powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
   ```
3. **Important:** Close the PowerShell window and open a **new** one so Windows recognizes the new command.

**On Mac / Linux:**
1. Open the **Terminal** app (on Mac, press `Cmd + Space`, type `Terminal`, and press **Enter**).
2. Copy and paste the following command and press **Enter**:
   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```
3. Close the Terminal window and open a **new** one.

---

### Step 2: Verify the Spreadsheet Server Works (Optional)

In your newly opened PowerShell or Terminal window, copy and paste this command and press **Enter**:

```powershell
uvx excel-mcp-server --version
```

- The very first time you run this, `uv` will automatically download Python and the spreadsheet tool in a few seconds and print a version number.
- After this first run, it is saved on your computer and will start instantly whenever you open Claude Code.

---

### Step 3: Install the Plugin in Claude Code

**Option 1: Inside Claude Code (Slash Commands)**
1. Start **Claude Code** (`claude`).
2. Add this GitHub repository to your plugin marketplace:
   ```text
   /plugin marketplace add sneakydave123/ClaudeTools
   ```
3. Install the plugin:
   ```text
   /plugin install claude-tools@claude-tools
   ```

**Option 2: From the Terminal (Bash / PowerShell)**
Run this single command in your terminal to add the marketplace and install the plugin in one step:
```bash
claude plugin install claude-tools --marketplace sneakydave123/ClaudeTools
```

Once installed, the plugin and its `spreadsheet` MCP server load automatically every time you open Claude Code. *(You can type `/mcp` at any time to confirm that the `spreadsheet` server shows **connected**.)*

---

## Example Prompts

- *"Categorize the transactions in `october_amex.csv` and flag anything that needs a receipt."* (Triggers `expense-categorizer`)
- `/claude-tools:journal-entry Accrued $12,500 in bi-weekly wages across 5 days at month-end`
- `/claude-tools:reconcile chase_oct.xlsx quickbooks_gl_oct.xlsx`
- `/claude-tools:variance-analysis q3_budget_vs_actual.xlsx`
- *"Have the audit-reviewer agent check `general_ledger_2026.xlsx` for duplicate invoices or out-of-balance batches."*
