# ASAK Bruno API collection

This folder is a Bruno collection that is versioned with the backend source.

## Open and run locally

1. Open Bruno and select **Open Collection**.
2. Select this `api` folder.
3. Choose the `local` environment.
4. Run **Health Check**.

The shared `local` environment uses `http://127.0.0.1:8080` as `baseUrl`.
Start the backend first with `..\\gradlew.bat bootRun` from `ASAK-back`.

## Collaboration rules

- Commit request files, shared environments, and non-sensitive test assertions.
- Put tokens, passwords, and other secrets in `api/.env`; it is ignored by Git.
- For developer-only overrides, create a `*.local.bru` file; it is also ignored.
- Add each implemented backend endpoint as a `.bru` request under a feature folder.
