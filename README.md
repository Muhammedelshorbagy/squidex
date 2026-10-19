# Squidex alias-limit build kit (base commit 476bb8f395bc38525ab02d65cffbdb111df7131a, 2026-01-16)

Your install was fingerprinted: all Squidex*.dll are a main-branch snapshot (labelled 7.21.0)
from between 2025-12-08 and 2026-01-16 (Squidex.Hosting 7.37.0, no UserInfo/SSRF code).
The backend source is identical across that whole window, so this build matches it.

1. Upload everything in this folder (including the hidden .github folder) to a private GitHub repo.
2. Actions -> build-squidex-alias-limit -> Run workflow.
3. Download the artifact "squidex-backend" and unzip it.

Deploy on the server (PowerShell as Administrator):

  Stop-WebAppPool Squidex-test
  Copy-Item C:\Host\Squidex-Test C:\Host\Squidex-Test-backup -Recurse     # full backup first
  # copy ONLY these two files from the artifact over the site folder:
  #   Squidex.dll
  #   Squidex.Domain.Apps.Entities.dll
  # then edit appsettings.json, section "graphQL": add  "maxAliases": 20,  "enableTracing": false
  Start-WebAppPool Squidex-test

Rollback: stop the pool, copy the two backed-up DLLs back, start the pool.
