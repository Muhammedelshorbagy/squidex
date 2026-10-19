# Squidex 7.21.0 alias-limit build kit

1. Create a new PRIVATE repository on github.com and upload everything in this folder
   (including the hidden .github folder) to its main branch.
2. Open the repo's Actions tab -> "build-squidex-alias-limit" -> Run workflow.
3. When it finishes, download the "squidex-dlls" artifact (2 DLLs).

Deploy (on the server):
- Stop the app pool, back up Squidex.dll and Squidex.Domain.Apps.Entities.dll in the site folder.
- Copy the two new DLLs over them.
- In appsettings.json, in the "graphQL" section, set:  "maxAliases": 20,  "enableTracing": false
  (remove maxDepth / maxComplexity, they do nothing on 7.21.0)
- Start the app pool, then rerun the 100-alias test: it must return a GraphQL error, not 200.
