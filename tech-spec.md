# SmartLegal Africa - Technical Specification

## 1. Tech Stack Overview

| Category | Technology |
|----------|------------|
| Framework | React 18 + TypeScript |
| Build Tool | Vite |
| Styling | Tailwind CSS 3.4 |
| UI Components | shadcn/ui |
| Animation | Framer Motion |
| Icons | Lucide React |
| Fonts | Inter (system fallback) |

## 2. Tailwind Configuration Guide

### Color Extensions

```javascript
// tailwind.config.js
colors: {
  primary: {
    DEFAULT: '#9C1C6B',
    dark: '#7A1654',
    light: '#D4A5C3',
  },
  secondary: {
    DEFAULT: '#00A0B0',
    dark: '#008A98',
  },
}
```

### Font Extensions

```javascript
fontFamily: {
  sans: ['Inter', 'system-ui', 'sans-serif'],
}
```

## 3. Component Inventory

### Shadcn/UI Components (Pre-installed)

| Component | Usage | Style Overrides |
|-----------|-------|-----------------|
| Button | CTAs, navigation | Custom colors, rounded-full |
| Card | Feature cards | Custom border radius |
| Sheet | Mobile navigation | - |
| Separator | Visual dividers | - |

### Custom Components

| Component | Props Interface | Description |
|-----------|-----------------|-------------|
| `Header` | `{}` | Fixed navigation with scroll effect |
| `HeroSection` | `{}` | Gradient hero with curved SVG |
| `FeatureCard` | `{ icon: LucideIcon, title: string, description: string }` | Feature display card |
| `FeaturesGrid` | `{}` | How it Works section |
| `AdditionalFeatures` | `{}` | Virtual Call Center, Accounting, Leave Management |
| `DataMigration` | `{}` | Simple info section |
| `CTASection` | `{ title: string, description: string, buttonText: string }` | Reusable CTA |
| `MatterManagement` | `{}` | Legal matter management section |
| `WorkflowAutomation` | `{}` | Workflow CTA section |
| `Footer` | `{}` | Site footer with links |

## 4. Animation Implementation Plan

| Interaction Name | Tech Choice | Implementation Logic |
|------------------|-------------|---------------------|
| Hero Text Reveal | Framer Motion | `staggerChildren: 0.1`, `y: 20 -> 0`, `opacity: 0 -> 1` |
| Hero Image Scale | Framer Motion | `scale: 0.9 -> 1`, `opacity: 0 -> 1`, delay 0.3s |
| Section Fade In | Framer Motion + whileInView | `y: 40 -> 0`, `opacity: 0 -> 1`, viewport once |
| Feature Cards Stagger | Framer Motion | `staggerChildren: 0.1`, slide up + fade |
| Card Hover Lift | Tailwind + Framer | `whileHover: { y: -4 }`, shadow transition |
| Button Hover | Tailwind | `hover:scale-[1.02]`, `transition-all duration-200` |
| Nav Scroll Effect | React State | Add shadow class when `scrollY > 10` |
| Mobile Menu | Framer Motion | Slide in from right, backdrop fade |

### Animation Timing Constants

```typescript
const ANIMATION = {
  duration: {
    fast: 0.2,
    normal: 0.3,
    slow: 0.5,
    slower: 0.8,
  },
  ease: {
    default: [0.4, 0, 0.2, 1],
    bounce: [0.68, -0.55, 0.265, 1.55],
  },
  stagger: {
    fast: 0.05,
    normal: 0.1,
    slow: 0.15,
  },
};
```

## 5. Project File Structure

```
app/
├── src/
│   ├── components/
│   │   ├── ui/              # shadcn components
│   │   ├── Header.tsx
│   │   ├── Footer.tsx
│   │   ├── FeatureCard.tsx
│   │   └── MobileNav.tsx
│   ├── sections/
│   │   ├── HeroSection.tsx
│   │   ├── FeaturesGrid.tsx
│   │   ├── AdditionalFeatures.tsx
│   │   ├── DataMigration.tsx
│   │   ├── CTASection.tsx
│   │   ├── MatterManagement.tsx
│   │   └── WorkflowAutomation.tsx
│   ├── hooks/
│   │   └── useScrollPosition.ts
│   ├── lib/
│   │   ├── utils.ts
│   │   └── animations.ts
│   ├── App.tsx
│   ├── main.tsx
│   └── index.css
├── public/
│   └── images/
│       └── hero-image.jpg
├── index.html
├── tailwind.config.js
├── vite.config.ts
└── package.json
```

## 6. Package Installation List

```bash
# Animation library
npm install framer-motion

# Icons (already included with shadcn)
# lucide-react is pre-installed

# No additional packages needed
```

## 7. Responsive Breakpoints

| Breakpoint | Width | Layout Changes |
|------------|-------|----------------|
| Mobile | < 640px | Single column, hamburger menu |
| Tablet | 640-1024px | 2-column grids |
| Desktop | > 1024px | Full layout, 3-column grids |

## 8. Key Implementation Notes

### Hero Curved Background
- Use SVG path for the curved wave shape
- Gradient: linear-gradient from primary to primary-light
- Position absolutely behind content

### Feature Cards
- Use CSS Grid for responsive layout
- Icons from Lucide React
- Consistent padding and hover effects

### Footer
- 4-column grid on desktop
- Stack to single column on mobile
- Social icons with hover color change

### Performance
- Use `will-change` on animated elements
- Lazy load below-fold sections
- Optimize images for web
