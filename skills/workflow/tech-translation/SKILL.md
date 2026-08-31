---
name: tech-translation
description: Translate technical documentation, code comments, and strings while preserving markup, code blocks, and terminology. Use when translating or localizing technical content.
category: workflow
tags: [translation, documentation, localization]
---

# tech-translation

Translate technical text accurately into natural, idiomatic target language without breaking markup, code blocks, or standard technical terminology.

## When to use

- Translating technical documents (Markdown, README, docs, guides, RFCs)
- Localizing code comments, docstrings, or commit messages
- Translating UI strings, error messages, and release notes
- Reviewing or standardizing bilingual documentation

## When not to

- Generating original documentation from scratch
- Translating non-technical prose where developer terminology conventions do not apply
- Machine-translating files without human/agent technical terminology verification

## Standards

1. **Markup & Code Integrity:**
   - Keep markdown structure, header levels, tables, lists, and indentation intact.
   - Do NOT translate code blocks, inline code (`` `variable` ``, `` `function()` ``), URLs, image links, file paths, CLI commands, or environment variables.
   - Preserve frontmatter keys (`name`, `description`, `tags`, etc.) and placeholder tokens (e.g. `{count}`, `%s`, `${id}`).

2. **Spacing & Punctuation (CJK / Western):**
   - Insert one half-width space between Chinese characters and English words or numbers (e.g., `使用 Docker 部署应用`, `支持 HTTP/2 协议`).
   - Do NOT add spaces between full-width punctuation and neighboring text.
   - Use standard full-width punctuation in Chinese prose (，。！？：“”《》), but keep ASCII punctuation inside code, URLs, and file paths.

3. **Terminology & Consistency:**
   - Maintain a consistent translation glossary across the entire document.
   - Use established industry translations (e.g., *repository* → 仓库, *branch* → 分支, *commit* → 提交, *concurrency* → 并发, *asynchronous* → 异步, *dependency* → 依赖).
   - Keep well-known proper nouns, protocol names, and product names untranslated (e.g., Git, Linux, Docker, RESTful, GraphQL, Kubernetes, Rust).
   - If a term has multiple interpretations or lacks standard consensus, keep the English term in parentheses on first mention (e.g., `可观测性 (Observability)`).

4. **Tone & Style:**
   - Accurate, concise, professional, and natural (信达雅).
   - Avoid "translationese" (translation-induced stiffness like overusing "被", "进行", "作为一个").
   - Prefer active voice and clear imperative statements for instructions.

## Steps

1. **Analyze source:** Identify target audience, source language, markdown structure, and code fences.
2. **Extract protected tokens:** Mark inline code, code blocks, URLs, and frontmatter keys as untranslatable.
3. **Translate content:** Translate prose section by section, maintaining idiomatic technical style and spacing rules.
4. **Align terminology:** Check key technical nouns against the standard glossary for consistency.
5. **Verify formatting:** Check that all links, tables, code fences, and tags remain syntactically valid.

## Example

Source:
```markdown
Run `npm install` to install dependencies. If Redis is not running, the cache service will fail.
```

Target (Chinese):
```markdown
运行 `npm install` 安装依赖。如果 Redis 服务未运行，缓存服务将会失败。
```

## Done when

The translated document preserves all original markdown structures, code, and links, follows punctuation/spacing rules, and uses consistent technical terminology throughout.
