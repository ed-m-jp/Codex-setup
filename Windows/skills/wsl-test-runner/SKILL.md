---
name: wsl-test-runner
description: run php artisan test commands through wsl for php and laravel projects from the current codex working directory. use this skill whenever the user asks to run tests, rerun tests, run php artisan test, execute tests, verify tests, check a new test, check an updated test, or when any plan or todo includes running tests. always use wsl.exe bash -lc, always cd into the current codex working directory, and always run the exact test files provided by the user or, if none are provided, the test files codex created or updated during the current task.
---

# PHP Artisan Test Runner

Run Laravel and PHP test commands through WSL from the current Codex working directory.

## Core rules

1. Always run tests through WSL.
2. Always use `wsl.exe bash -lc`.
3. Always `cd` into the same folder Codex is currently running in before executing `php artisan test`.
4. Never run `php artisan test` directly outside WSL for this skill.
5. Assume network access is granted for these test runs.
6. Return the executed command and the test results.
7. Do not claim tests passed if they were not actually executed.
8. If the user does not provide specific test paths, run the test files Codex created or updated during the current task.
9. Do not silently switch to unrelated tests, the full suite, or guessed files outside the current task.

## Command pattern

Use this exact command shape:

```bash
wsl.exe bash -lc "cd <current-working-directory> && php artisan test <test-paths>"
