```markdown
# nodejs-docs-samples Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill provides guidance on contributing to the `nodejs-docs-samples` repository, a collection of TypeScript code samples demonstrating Node.js usage. It covers coding conventions, repository workflows (such as dependency upgrades), testing patterns, and common contributor commands.

## Coding Conventions

### File Naming
- Use **camelCase** for file names.
  - Example: `sampleFunction.ts`, `userRoutes.ts`

### Import Style
- Use **relative imports** for modules within the repository.
  ```typescript
  import { helperFunction } from './utils/helperFunction';
  ```

### Export Style
- Prefer **named exports**.
  ```typescript
  // In helperFunction.ts
  export function helperFunction() { /* ... */ }

  // In another file
  import { helperFunction } from './helperFunction';
  ```

### Commit Messages
- Follow the **conventional commit** format.
  - Prefixes: `chore`
  - Example: `chore: update uuid to v14.0.0 in all packages`

## Workflows

### Bulk Dependency Upgrade Across Packages
**Trigger:** When you need to upgrade one or more npm dependencies across all packages in the monorepo (e.g., for security, bugfixes, or feature updates).

**Command:** `/upgrade-dependency-all <dependency>@<version>`

#### Step-by-Step Instructions
1. **Identify outdated dependencies**  
   Locate all `package.json` files in the repository and check for outdated versions of the target dependency.
2. **Update dependency versions**  
   For each affected `package.json`, update the dependency version to the specified target.
3. **Update lock files (optional)**  
   If `package-lock.json` or `yarn.lock` files are present, update them to reflect the new dependency versions.
4. **Commit changes**  
   Commit all modified `package.json` and lock files in a single commit, following the conventional commit message style.

#### Example
Suppose you want to upgrade `uuid` to version `14.0.0` across all packages:
```sh
/upgrade-dependency-all uuid@14.0.0
```

This will:
- Find every `package.json` containing `uuid`
- Update the version to `14.0.0`
- Update lock files if present
- Commit all changes together

## Testing Patterns

- **Test File Naming:**  
  Test files use the pattern `*.test.*` (e.g., `sampleFunction.test.ts`).
- **Testing Framework:**  
  Not explicitly detected; check individual test files for framework usage.
- **Test Example:**
  ```typescript
  // sampleFunction.test.ts
  import { sampleFunction } from './sampleFunction';

  describe('sampleFunction', () => {
    it('should return expected result', () => {
      expect(sampleFunction()).toBe('expected');
    });
  });
  ```

## Commands

| Command                           | Purpose                                                    |
|------------------------------------|------------------------------------------------------------|
| /upgrade-dependency-all <dep>@<v>  | Upgrade a dependency across all packages in the repository. |

```