# Codex-Desktop-App-Unable-to-Load-Organization-Settings-Error-on-Windows
Error When launching the Codex desktop app, it shows: Unable to load organization settings  The app is paused until organization settings can be loaded securely. Network connection, proxy, or firewall issues may prevent access.  Please check your network connection and try again, or sign out and use another account.

Symptoms:
- ChatGPT website works normally.
- Other applications work normally.
- Reinstalling Codex does not fix the issue.
- Clicking Retry or Sign out does not help.
- The issue may happen after a crash, update, or abnormal shutdown.


How to fix:
- Step 1 — Backup Codex data
Open PowerShell:
cd $HOME

Create a full backup:
Copy-Item `
"$HOME\.codex" `
"$HOME\.codex.full_backup" `
-Recurse `
-Force

Verify:
Test-Path "$HOME\.codex.full_backup"

Expected:
True

- Step 2 — Close Codex completely
Exit Codex.
Check running processes:
tasklist | findstr /i "codex openai chatgpt"

If needed:
taskkill /F /IM Codex.exe

- Step 3 — Rename the corrupted state folder
Do not delete it.
Rename:
Rename-Item `
"$HOME\.codex" `
".codex.backup"

Result:
C:\Users\<USERNAME>\.codex.backup

Your original data is preserved.
- Step 4 — Start Codex again
Launch Codex.
The app will:
- create a fresh .codex folder;
- initialize a clean state;
- load organization settings;
- allow login.
- The error should disappear.
