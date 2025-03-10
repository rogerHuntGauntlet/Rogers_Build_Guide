# React TypeScript Development Guidelines

## Core Principles

1. **Component-Based Architecture**
   - Build small, focused components (< 300 lines)
   - Use composition over inheritance
   - One main component per file

2. **Type Safety**
   - Define explicit interfaces for all props
   - Use TypeScript features to ensure type safety
   - Avoid using `any` type

3. **Performance First**
   - Memoize expensive calculations and callbacks
   - Implement virtualization for long lists
   - Use React.memo for pure components

4. **Maintainable Code**
   - Follow consistent naming conventions
   - Document complex logic and component APIs
   - Write tests for critical functionality

## File Structure

```
src/
├── components/  # UI components organized by domain
├── hooks/       # Custom React hooks
├── pages/       # Route components
├── types/       # TypeScript definitions
├── utils/       # Helper functions
└── lib/         # Third-party integrations
```

## Naming Conventions

| Item | Convention | Example |
|------|------------|---------|
| Component files | PascalCase | `Button.tsx` |
| Utility files | camelCase | `formatDate.ts` |
| CSS modules | kebab-case | `button-styles.module.css` |
| Component names | PascalCase | `UserProfile` |
| Functions | camelCase | `calculateTotal` |
| Constants | UPPER_SNAKE_CASE | `MAX_ITEMS` |

## Component Template

```tsx
// Imports
import React from 'react';
import type { ButtonProps } from './types';

// Component interface
interface Props {
  label: string;
  onClick: () => void;
  variant?: 'primary' | 'secondary';
}

// Component definition
export const Button: React.FC<Props> = ({ 
  label, 
  onClick, 
  variant = 'primary' 
}) => {
  // 1. Hooks
  const [isHovered, setIsHovered] = useState(false);
  
  // 2. Event handlers
  const handleMouseEnter = () => setIsHovered(true);
  const handleMouseLeave = () => setIsHovered(false);
  
  // 3. Return JSX
  return (
    <button
      className={`btn btn-${variant}`}
      onClick={onClick}
      onMouseEnter={handleMouseEnter}
      onMouseLeave={handleMouseLeave}
    >
      {label}
    </button>
  );
};
```

## Best Practices

### State Management
- Keep state as local as possible
- Use React Query for server state
- Use Context API sparingly

### Performance
- Use `useMemo` for expensive calculations
- Use `useCallback` for event handlers passed as props
- Implement virtualization for long lists

### Accessibility
- Use semantic HTML elements
- Add proper ARIA attributes
- Ensure keyboard navigation works
- Maintain sufficient color contrast

### Testing
- Write tests for critical user interactions
- Test component props and state changes
- Place tests next to components (`Component.test.tsx`)

## Code Review Checklist

- [ ] Component follows size guidelines
- [ ] Props are properly typed with interfaces
- [ ] Performance optimizations are in place
- [ ] Code is properly documented
- [ ] Tests cover critical functionality
- [ ] Accessibility requirements are met
- [ ] No console logs or debugging code 