# Test & Benchmark Requirements

## Current State
- Unit tests: 1 test file (a2_ml_test.exs) — count unknown (mix not runnable without correct Elixir version)
- Integration tests: NONE
- E2E tests: NONE
- Benchmarks: NONE
- panic-attack scan: NEVER RUN

## What's Missing
### Point-to-Point (P2P)
- a2_ml.ex (main module) — possibly tested via a2_ml_test.exs but coverage unknown
- a2ml/parser.ex — likely undertested (complex parsing logic)
- a2ml/renderer.ex — likely undertested (output formatting)
- a2ml/types.ex — type definitions may not need direct tests but validation does
- erl_crash.dump exists in repo root — indicates past crash, should not be committed

### End-to-End (E2E)
- Parse real-world A2ML documents end-to-end
- Render A2ML and verify output matches expected format
- Round-trip (parse -> render -> parse) fidelity check
- Error reporting for malformed input

### Aspect Tests
- [ ] Security (untrusted A2ML input, injection via trust levels)
- [ ] Performance (parsing large documents)
- [ ] Concurrency (GenServer usage if any)
- [ ] Error handling (malformed A2ML, missing fields, encoding issues)
- [ ] Accessibility (N/A)

### Build & Execution
- [ ] mix compile — clean? (erl_crash.dump suggests past issues)
- [ ] mix test — not verified (asdf version mismatch)
- [ ] Self-diagnostic — none

### Benchmarks Needed
- Parse throughput vs a2ml-rs and a2ml-deno implementations
- Memory usage for large documents on BEAM

### Self-Tests
- [ ] panic-attack assail on own repo
- [ ] Remove erl_crash.dump from repo (should be in .gitignore)
- [ ] Built-in doctor/check command (if applicable)

## Priority
- **MEDIUM** — Small library (3 source modules) with 1 test file. The single test file likely covers basics but with no way to run it currently (version mismatch), actual coverage is unknown. The erl_crash.dump in the repo is a red flag.

## FAKE-FUZZ ALERT

- `tests/fuzz/placeholder.txt` is a scorecard placeholder inherited from rsr-template-repo — it does NOT provide real fuzz testing
- Replace with an actual fuzz harness (see rsr-template-repo/tests/fuzz/README.adoc) or remove the file
- Priority: P2 — creates false impression of fuzz coverage
