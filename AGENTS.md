# Agent Guidelines for retinal-oct

This repository is a Next.js 16 project using TypeScript, Tailwind CSS v4, and the App Router.

## Build, Lint, and Test Commands

### Development
```bash
npm run dev          # Start development server on localhost:3000
npm run build        # Create production build
npm run start        # Start production server (after build)
npm run lint         # Run ESLint
```

### Testing
This project currently has no test framework configured. Add tests using a framework like Jest, Vitest, or Playwright. Once configured, document test commands here.

### Running Single Tests
Once test framework is added, use pattern like:
```bash
npm test -- path/to/test.spec.ts    # Run specific test file
npm test -t "test name"             # Run tests matching pattern
```

## Code Style Guidelines

### Imports
- Use double quotes for all import statements
- Import types with `import type { ... }` to avoid runtime imports
- Order: React/Next.js imports → third-party libraries → local modules → type imports
- Example:
  ```typescript
  import Image from "next/image";
  import { useState } from "react";
  import type { Metadata } from "next";
  import "./globals.css";
  ```

### TypeScript
- Strict mode is enabled - always provide explicit types
- Use `Readonly<{...}>` for component props interfaces
- Use `interface` for object shapes that may be extended
- Use `type` for unions, intersections, and utility types
- Avoid `any` - use `unknown` with type guards when necessary
- Example props interface:
  ```typescript
  interface Props {
    title: string;
    count?: number;
  }
  ```

### Component Style
- Use function components with default exports
- Name components with PascalCase
- Keep components small and focused (< 200 lines preferred)
- Use React hooks at the top level of components
- Example:
  ```typescript
  export default function MyComponent({ title }: Props) {
    return <div>{title}</div>;
  }
  ```

### Styling with Tailwind CSS v4
- Use Tailwind utility classes exclusively
- Apply `dark:` prefix for dark mode styles
- Use responsive prefixes (`sm:`, `md:`, `lg:`) for breakpoints
- Keep class names organized in logical order (layout → spacing → visual)
- Prefer utility classes over inline styles or custom CSS
- Example:
  ```tsx
  <div className="flex flex-col items-center gap-4 p-4 dark:bg-black">
  ```

### Naming Conventions
- Components: PascalCase (`UserProfile.tsx`, `Header.tsx`)
- Files: kebab-case (`user-profile.tsx`, `api-handler.ts`)
- Variables/functions: camelCase (`getUserData`, `isLoading`)
- Constants: UPPER_SNAKE_CASE (`API_BASE_URL`, `MAX_RETRIES`)
- Types/interfaces: PascalCase (`UserData`, `ApiResponse`)

### File Structure (App Router)
- Use the `app/` directory for routes and pages
- Each route folder contains `page.tsx` for page content
- Use `layout.tsx` for shared layout components
- Server components by default, add `"use client"` for client components
- Keep route handlers in `app/api/` directory

### Error Handling
- Use try-catch blocks for async operations
- Return error objects or throw for unexpected errors
- Display user-friendly error messages
- Log errors appropriately (avoid logging sensitive data)
- Example:
  ```typescript
  try {
    const data = await fetchData();
    return { success: true, data };
  } catch (error) {
    console.error("Failed to fetch:", error);
    return { success: false, error: "Failed to load data" };
  }
  ```

### Accessibility
- Use semantic HTML elements (`nav`, `main`, `section`, etc.)
- Add `alt` text to images (empty `alt=""` for decorative images)
- Use proper ARIA labels when needed
- Ensure keyboard navigation support
- Maintain proper heading hierarchy

### Performance
- Use Next.js Image component for optimization (`next/image`)
- Lazy load heavy components with dynamic imports
- Use `loading="lazy"` for below-the-fold images
- Avoid unnecessary re-renders with proper dependency arrays
- Use React.memo for expensive pure components

### Code Quality
- Run `npm run lint` before committing changes
- Fix all ESLint warnings and errors
- Keep code DRY (Don't Repeat Yourself)
- Write self-documenting code with clear variable names
- Break complex functions into smaller, named functions

### Formatting
- This project uses a consistent formatting style (Prettier recommended)
- Maintain 2-space indentation
- Use semicolons at end of statements
- Keep lines under 100 characters when practical
- Add blank lines between logical sections

## Project-Specific Notes

- Path alias `@/*` maps to project root
- Supports both light and dark modes with `dark:` classes
- Uses Geist font family (Sans and Mono variants)
- Built with modern Next.js 16 and React 19 features
