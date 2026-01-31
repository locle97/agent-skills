---
name: neo-brutalism-frontend
description: "Build production-ready Neo-brutalism UI components for React/Next.js applications following the Duckeebs design system. Use when building: (1) Hero sections, cards, buttons, badges, or other UI components with bold borders and offset shadows, (2) Gallery or grid layouts with hover effects, (3) Interactive elements requiring the neo-brutalism aesthetic (thick borders, hard shadows, vibrant colors, tactical hover interactions), (4) Any frontend work for the Duckeebs platform that needs to match the GMK Flare mockup design patterns."
---

# Neo-brutalism Frontend Builder

Build production-ready Neo-brutalism components for React/Next.js following the Duckeebs design system extracted from the GMK Flare mockup.

## Quick Start

1. **Review the request** - Identify component type (button, card, hero, gallery, etc.) and requirements
2. **Check component patterns** - See `references/component-patterns.md` for exact implementation examples
3. **Follow the workflow** - See `references/implementation-guide.md` for step-by-step process
4. **Apply the Trinity** - Every interactive element gets: border, shadow, and hover effect

## The Neo-brutalism Trinity

Always apply to interactive elements (buttons, cards, links):

```tsx
className="
  border-{2-5} border-black                              // Bold border
  shadow-[4px_4px_0px_0px_rgba(0,0,0,1)]                 // Offset shadow
  hover:translate-x-[-4px] hover:translate-y-[-4px]      // Hover lift
  transition-all duration-150                             // Smooth transition
"
```

## Core Design Tokens

**Shadows (offset, no blur):**
- Small: `shadow-[4px_4px_0px_0px_rgba(0,0,0,1)]`
- Medium: `shadow-[6px_6px_0px_0px_rgba(0,0,0,1)]`
- Large: `shadow-[10px_10px_0px_0px_rgba(0,0,0,1)]`
- Hover: `shadow-[12px_12px_0px_0px_rgba(0,0,0,1)]`

**Colors (semantic):**
- Primary CTA: `bg-[#FF6B35]` (keycap-orange)
- Secondary CTA: `bg-[#3A7CA5]` (keycap-blue)
- Success: `bg-[#2D936C]` or `bg-[#4BA67C]` (green)
- Warning: `bg-[#F9C74F]` (duck-yellow)
- Error: `bg-[#E63946]` (error-red)
- Background: `bg-[#F5C518]` (yellow) or `bg-[#FFFEF0]` (white)
- Text: `text-black` or `text-[#FFFEF0]`

**Typography:**
- Headings: `font-[Archivo_Black]` (bold, uppercase, tracking-tight)
- Body: `font-[Space_Mono]` (default, leading-relaxed)
- Labels: `font-bold text-xs uppercase tracking-wide`

## Implementation Process

### Step 1: Identify Component Type

Determine what you're building:
- **Buttons/CTAs** → See Button Patterns in `component-patterns.md`
- **Cards/Panels** → See Card Patterns in `component-patterns.md`
- **Hero Sections** → See Hero Section Pattern in `component-patterns.md`
- **Galleries/Grids** → See Gallery Grid Pattern in `component-patterns.md`
- **Status Indicators** → See Badge Patterns in `component-patterns.md`
- **Complex Sections** → Combine multiple patterns from `component-patterns.md`

### Step 2: Start with Structure

Build semantic HTML/JSX first without styling:

```tsx
function ProductCard({ title, image, status }) {
  return (
    <article>
      <div>
        <img src={image} alt={title} />
      </div>
      <header>
        <h3>{title}</h3>
        <span>{status}</span>
      </header>
    </article>
  );
}
```

### Step 3: Apply Neo-brutalism Styling

Add the core visual elements following patterns from `component-patterns.md`:

```tsx
function ProductCard({ title, image, status }) {
  return (
    <article className="
      bg-[#FFFEF0]
      border-5 border-black
      shadow-[10px_10px_0px_0px_rgba(0,0,0,1)]
      p-6
      cursor-pointer
      transition-all duration-200
      hover:translate-x-[-4px] hover:translate-y-[-4px]
    ">
      {/* Content */}
    </article>
  );
}
```

### Step 4: Add Interactions & Details

- Apply hover, active, and focus states
- Add floating badges or decorative elements if needed
- Include animations sparingly (see Animation patterns in `component-patterns.md`)
- Ensure responsive behavior (mobile-first approach)

### Step 5: Verify Quality

Check against the component checklist from `implementation-guide.md`:
- Applied Trinity to interactive elements
- Used semantic colors
- Proper typography hierarchy
- Accessibility (ARIA, focus states, keyboard nav)
- Responsive on mobile/tablet/desktop

## Reference Files

**For specific component implementations:**
→ Read `references/component-patterns.md`

Contains exact code for:
- Button variants (primary, outline, icon)
- Badge variants (standard, floating, status)
- Card layouts (basic, hoverable, with header)
- Hero sections with grid layouts
- Gallery grids with hover effects
- Sentiment/progress bars
- Info rows and stat displays
- Background decorations
- Responsive patterns

**For step-by-step workflow:**
→ Read `references/implementation-guide.md`

Contains:
- Detailed 10-step implementation process
- Common patterns (cards with badges, stats rows, section headers, image galleries)
- Component checklist
- Accessibility guidelines
- Performance considerations
- Common pitfalls to avoid

## Quick Examples

**Primary Button:**
```tsx
<button className="
  px-6 py-3 bg-[#FF6B35] text-[#FFFEF0]
  border-3 border-black
  shadow-[4px_4px_0px_0px_rgba(0,0,0,1)]
  hover:translate-x-[-2px] hover:translate-y-[-2px]
  hover:shadow-[6px_6px_0px_0px_rgba(0,0,0,1)]
  hover:bg-[#E63946]
  transition-all duration-150
  font-bold text-sm uppercase
">
  Click Me
</button>
```

**Feature Card:**
```tsx
<div className="
  bg-[#FFFEF0]
  border-5 border-black
  shadow-[10px_10px_0px_0px_rgba(0,0,0,1)]
  p-8
  hover:translate-x-[-4px] hover:translate-y-[-4px]
  transition-all duration-200
">
  <h3 className="font-[Archivo_Black] text-2xl mb-4">{title}</h3>
  <p className="text-base leading-relaxed">{description}</p>
</div>
```

**Status Badge:**
```tsx
<span className="
  px-4 py-2
  bg-[#2D936C] text-white
  border-3 border-black
  font-bold text-xs uppercase
">
  Live
</span>
```

## Integration with Existing Codebase

When working on the Duckeebs client project:

1. **Reference the style guide** - The project has `archieved/docs/style-guide.md` with additional context
2. **Use Shadcn components as base** - Extend components from `components/ui/` with Neo-brutalism classes
3. **Follow existing patterns** - Check `app/` directory for existing component usage
4. **Use path aliases** - Import with `@ui/`, `@/lib/`, `@layouts/` etc.

## Best Practices

✅ **Do:**
- Use hard-edged offset shadows (no blur)
- Apply thick borders (2-5px solid black)
- Implement hover translations (lift elements on hover)
- Use semantic colors from the design system
- Keep corners minimal (5px max radius)
- Test on mobile, tablet, desktop
- Ensure WCAG AA contrast

❌ **Don't:**
- Use blurred shadows or glows
- Skip borders on interactive elements
- Use arbitrary Tailwind colors (e.g., `bg-blue-500`)
- Round corners too much
- Animate everything without purpose
- Forget hover states
- Make touch targets smaller than 44px

## Workflow Summary

For every component:
1. Identify component type → Check `component-patterns.md` for reference
2. Build structure → Semantic HTML/JSX
3. Apply styling → Border + Shadow + Colors
4. Add interactions → Hover + Active + Focus states
5. Verify quality → Checklist from `implementation-guide.md`

**Most important:** Every interactive element MUST have the Trinity (border, shadow, hover).
