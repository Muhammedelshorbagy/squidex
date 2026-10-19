# Squidex alias-limit build kit (base: commit 223687424, 2026-01-20)

Your install is NOT the official 7.21.0 tag: it is a newer snapshot of the main branch
(still .NET 8) that is labelled 7.21.0. This kit builds from that snapshot's source.

1. Upload everything in this folder (including the hidden .github folder) to a private GitHub repo.
2. Actions -> build-squidex-alias-limit -> Run workflow.
3. Download the artifact "squidex-backend" and unzip it to C:\temp\out on the server.

Deploy on the server (PowerShell as Administrator):

  Stop-WebAppPool Squidex-test
  Copy-Item C:\Host\Squidex-Test C:\Host\Squidex-Test-backup -Recurse     # FULL backup first
  robocopy C:\temp\out C:\Host\Squidex-Test /E /XF appsettings*.json web.config /XD wwwroot Assets logs
  # edit C:\Host\Squidex-Test\appsettings.json, section "graphQL": add  "maxAliases": 20,  "enableTracing": false
  Start-WebAppPool Squidex-test

Do not use /MIR (it would delete your Assets folder).
Rollback: stop the pool, delete the site folder contents, copy the backup folder back, start the pool.
