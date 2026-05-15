# Run MCP

Start the local dev server, capture a fresh screenshot of the site, save it as `screenshot.png` in the repo root, and push to GitHub.

## Steps

1. Start http-server on port 8080 if not already running:
   ```powershell
   $env:PATH = [System.Environment]::GetEnvironmentVariable("PATH","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("PATH","User")
   Start-Process powershell -ArgumentList "-NoProfile -Command `"cd 'c:\Users\PearsonVue_User\Desktop\VSC'; npx http-server -p 8080`"" -WindowStyle Minimized
   Start-Sleep -Seconds 4
   ```

2. Use the Playwright MCP browser to:
   - Navigate to `http://localhost:8080`
   - Take a screenshot saved as `screenshot.png` in the repo root

3. Commit and push using the `/gitpush` command.
