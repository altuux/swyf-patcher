# Release v2.0.4

## What's Changed in v2.0.4 (Hotfix)

### Fixes

- **PC Clock Error Bypass (`KolkataApi.SystemClockIncorrect`)**:
  - Resolves Issues #2 and #4 where the game blocked startup/play with *"Game says my PC clock is incorrect"* due to `edgeServerTime` drifting more than 300 seconds behind real UTC time.
  - `KolkataPatcher` now patches `KolkataApi.SystemClockIncorrect` to always return `false`.
- **`PatchCoreModule` `NullReferenceException` Fix (`RedirectMethod`)**:
  - Resolves Issues #1, #5, and #6 where patching failed in `KolkataPatcher.Program.<PatchCoreModule>g__RedirectMethod` on builds where `UnityEngine.PlayerPrefs` methods existed as `extern` (`InternalCall`) methods with a null IL `MethodBody`.
  - Properly clears `InternalCall` / `PInvokeImpl` flags and initializes a fresh `MethodBody` before emitting IL redirects.
- **AI Gateway Stability & Reasoning Normalization (`tools/proxy.py`)**:
  - Prevents `ConnectionAbortedError` (`WinError 10053`) / `BrokenPipeError` thread crashes when the game closes a socket mid-request (e.g. when a call ends or cancels).
  - Automatically cascades across independent Groq free-tier model quotas (`qwen/qwen3.8-27b` -> `openai/gpt-oss-120b` -> `openai/gpt-oss-20b`) on `HTTP 429` using the same API key.
  - Normalizes `reasoning_content` as well as `reasoning` when `content` is empty or whitespace-only.

---

## Assets

- `SWYF-Complete-Package-v2.0.4.zip`: All-in-one package for Windows (`KolkataPatcher.exe` + `SWYF-Gateway.exe` + `README.md`).
- `SWYF-Complete-Package-Linux-v2.0.4.tar.gz` / `.zip`: All-in-one package for Linux / Steam Deck (`KolkataPatcher-linux` + `SWYF-Gateway-linux` + `README.md`).
- Standalone binaries: `KolkataPatcher.exe`, `KolkataPatcher-linux`, `SWYF-Gateway.exe`, `SWYF-Gateway-linux`.
