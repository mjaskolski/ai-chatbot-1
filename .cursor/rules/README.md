# Cursor Rules for AI Chatbot Project

This directory contains Cursor rules that help guide AI assistance for this project. These rules ensure consistent code quality, patterns, and best practices.

## Available Rules

### 🏗️ Always Applied Rules

1. **project-structure.mdc**
   - Always applied to provide context about the project
   - Contains project overview, tech stack, and key file references
   - Helps AI understand the application architecture

### 📝 Pattern-Based Rules (Applied by file type)

2. **coding-standards.mdc**
   - Applied to: `*.ts`, `*.tsx`, `*.js`, `*.jsx`
   - TypeScript and React coding conventions
   - Import organization, component structure, and best practices

3. **api-patterns.mdc**
   - Applied to: `app/**/route.ts`, `app/**/actions.ts`, `artifacts/actions.ts`
   - API route handlers and server action patterns
   - Error handling, validation, and streaming responses

4. **database-patterns.mdc**
   - Applied to: `lib/db/**/*.ts`, `app/**/queries.ts`
   - Drizzle ORM usage patterns
   - Query patterns, migrations, and transactions

5. **component-patterns.mdc**
   - Applied to: `components/**/*.tsx`, `app/**/*.tsx`
   - React component patterns and best practices
   - State management, performance optimization, and accessibility

6. **testing-standards.mdc**
   - Applied to: `tests/**/*.ts`, `**/*.test.ts`, `**/*.test.tsx`
   - Playwright E2E testing patterns
   - Page Object Model, test helpers, and best practices

### 🎯 Manual Rules (Applied on demand)

7. **ai-chat-implementation.mdc**
   - Comprehensive guide for implementing AI chat features
   - Model configuration, streaming, tools, and artifacts
   - Applied when working on AI-specific features

## How Rules Work

- **Always Applied**: Rules with `alwaysApply: true` are automatically included in every AI interaction
- **Pattern-Based**: Rules with `globs` patterns are applied when working with matching files
- **Manual**: Rules with `description` can be manually referenced when needed

## Usage Tips

1. Rules automatically provide context based on the files you're working with
2. Manual rules can be referenced by mentioning their topic (e.g., "help with AI chat implementation")
3. Rules contain code examples and file references using the `[filename](mdc:path)` format
4. All rules follow the project's established patterns and conventions

## Modifying Rules

To modify or add new rules:
1. Edit the `.mdc` files in this directory
2. Use proper frontmatter (alwaysApply, globs, or description)
3. Reference project files using `[display](mdc:path)` format
4. Keep rules focused and well-organized

## Rule Structure

```markdown
---
alwaysApply: true  # OR
globs: "*.ts,*.tsx"  # OR
description: "Description for manual application"
---
# Rule Title

Content with examples and references...
``` 