---
name: explain-method
description: Explains a method or function in detail — high-level overview paragraph followed by a line-by-line breakdown with inline comments and a summary table. Works with any language (C++, Kotlin, Rust, Python, Go, Java, etc.) auto-detected from the file. Use when user says "explain this method", "what does this function do", "walk me through this code", "break down this function", or pastes a function and asks what it does. Supports depth control: "overview only" for just the summary paragraph, "deep dive" or default for full line-by-line + table.
---

# explain-method

## Quick start

User points at a method (selects it, pastes it, or names it) and says "explain this".
Read the method, detect the language, then produce:

1. **Overview** — 2-4 sentence paragraph: what the function does, its role in the system, inputs/outputs, and any non-obvious invariants.
2. **Annotated code** — reprint the method with inline comments on every non-trivial line.
3. **Line table** — markdown table summarising the key lines.

## Depth modes

| User says | What to produce |
|-----------|----------------|
| "overview only" | Overview paragraph only, no code reprint |
| default / "explain" / "deep dive" | Overview + annotated code + table |
| "just the table" | Table only |

## Workflow

1. **Read the method** — if the user named it without pasting, use grep/Read to locate it first.
2. **Detect language** from file extension or syntax.
3. **Overview paragraph** — cover: purpose, caller context (if visible), inputs, outputs, side effects, error handling strategy.
4. **Annotated code block** — reprint the full method in a fenced code block, language-tagged. Add `//` or `#` inline comments on lines that are non-obvious. Do NOT comment self-explanatory lines (variable declarations with clear names, closing braces, etc.).
5. **Key lines table** — columns: `Line` | `What it does` | `Why it matters`. Include only lines worth calling out (5–15 rows). Use the original line numbers from the file.

## Language comment styles

| Language | Inline comment |
|----------|---------------|
| C, C++, Kotlin, Java, Go, Rust, Swift | `// comment` |
| Python, Shell, Ruby | `# comment` |
| SQL | `-- comment` |

## Example output shape

```
### Overview
[2-4 sentence paragraph]

### Annotated code
```cpp
int foo(int x) {
    if (x < 0) return -1;  // guard: reject negative input early
    ...
}
```

### Key lines
| Line | What it does | Why it matters |
|------|-------------|----------------|
| 42   | `llama_decode(g_ctx, batch)` | Runs one forward pass through the LLM; non-zero return = KV cache full |
```

## Rules

- Never summarise what is already obvious from the identifier name.
- If a line involves a library call (llama.cpp, JNI, Android API, etc.), name the library and briefly explain what that call does at the system level.
- If the method has a known failure mode visible in the code, call it out in the overview.
- Keep the table to the most impactful lines — not every line.