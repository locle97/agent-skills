# Neo-brutalism Implementation Guide

Step-by-step workflow for building production-ready Neo-brutalism components in React/Next.js following the Duckeebs design system.

## Implementation Workflow

### 1. Review Design Requirements

Before building, identify:
- **Component type**: Button, card, hero section, gallery, etc.
- **Interaction needs**: Hover effects, animations, clickability
- **Content structure**: Text, images, badges, stats
- **Responsive behavior**: Mobile vs desktop layout

### 2. Start with Semantic HTML/JSX Structure

Build the component structure first without styling:

```tsx
// Example: Product card
function ProductCard({ title, image, status, stats }) {
  return (
    <article>
      <div>
        <img src={image} alt={title} />
      </div>
      <header>
        <h3>{title}</h3>
        <span>{status}</span>
      </header>
      <div>
        {stats.map(stat => (
          <div key={stat.label}>
            <span>{stat.label}</span>
            <span>{stat.value}</span>
          </div>
        ))}
      </div>
    </article>
  );
}
```

### 3. Apply Neo-brutalism Base Styling

Add the core Neo-brutalism visual elements:

**The Trinity (always apply to interactive elements):**
1. **Border**: `border-{2-5} border-black`
2. **Shadow**: `shadow-[4px_4px_0px_0px_rgba(0,0,0,1)]`
3. **Hover**: `hover:translate-x-[-4px] hover:translate-y-[-4px] hover:shadow-[10px_10px_0px_0px_rgba(0,0,0,1)]`

```tsx
function ProductCard({ title, image, status, stats }) {
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

### 4. Apply Color Semantics

Use the correct color for the component's purpose:

**Color Usage Guide:**
- **Primary CTA**: `bg-[#FF6B35]` (keycap-orange)
- **Secondary CTA**: `bg-[#3A7CA5]` (keycap-blue)
- **Success/Positive**: `bg-[#4BA67C]` (keycap-green) or `bg-[#2D936C]`
- **Warning/Medium**: `bg-[#F9C74F]` (duck-yellow)
- **Error/Negative**: `bg-[#E63946]` (error-red)
- **Neutral/Info**: `bg-[#6B7280]` (gray)
- **Background**: `bg-[#F5C518]` (yellow) or `bg-[#FFFEF0]` (white)
- **Text**: `text-black` or `text-[#FFFEF0]`

```tsx
{/* Status badge with semantic color */}
<span className={`
  px-4 py-2
  border-3 border-black
  font-bold text-xs uppercase
  ${status === 'live' ? 'bg-[#2D936C] text-white' :
    status === 'upcoming' ? 'bg-[#F9C74F] text-black' :
    'bg-[#6B7280] text-white'}
`}>
  {status}
</span>
```

### 5. Add Typography Styling

Follow the typography hierarchy:

```tsx
{/* Heading sizes */}
<h1 className="font-[Archivo_Black] text-5xl md:text-6xl leading-tight uppercase tracking-tight">
  Main Title
</h1>

<h2 className="font-[Archivo_Black] text-3xl md:text-5xl leading-tight uppercase tracking-tight">
  Section Title
</h2>

<h3 className="font-[Archivo_Black] text-2xl md:text-4xl leading-tight uppercase">
  Subsection
</h3>

<h4 className="font-[Archivo_Black] text-xl md:text-2xl uppercase">
  Card Title
</h4>

{/* Body text */}
<p className="font-[Space_Mono] text-base leading-relaxed">
  Regular body text with good readability
</p>

{/* Labels */}
<span className="font-bold text-xs uppercase tracking-wide">
  Label Text
</span>
```

### 6. Implement Interactions

Add hover, active, and focus states:

```tsx
<button className="
  px-6 py-3
  bg-[#FF6B35] text-[#FFFEF0]
  border-3 border-black
  shadow-[4px_4px_0px_0px_rgba(0,0,0,1)]
  font-bold text-sm uppercase
  cursor-pointer
  transition-all duration-150

  /* Hover: lift and extend shadow */
  hover:translate-x-[-2px]
  hover:translate-y-[-2px]
  hover:shadow-[6px_6px_0px_0px_rgba(0,0,0,1)]
  hover:bg-[#E63946]

  /* Active: push down */
  active:translate-x-[1px]
  active:translate-y-[1px]
  active:shadow-[2px_2px_0px_0px_rgba(0,0,0,1)]

  /* Focus: visible ring */
  focus-visible:ring-4
  focus-visible:ring-black
  focus-visible:ring-offset-2
">
  Click Me
</button>
```

### 7. Add Animations (When Appropriate)

Use subtle, purposeful animations from the design system:

```tsx
{/* Floating badge */}
<div className="
  absolute -top-4 -left-4
  bg-black text-[#F5C518]
  px-6 py-3
  font-[Archivo_Black] text-sm uppercase
  rotate-[-8deg]
  animate-[bounce_2s_ease-in-out_infinite]
">
  NEW
</div>

{/* Pulsing indicator */}
<span className="
  w-3 h-3
  bg-[#E63946]
  rounded-full
  animate-[blink_1s_ease-in-out_infinite]
" />

{/* Glowing CTA */}
<button className="
  ...
  animate-[glow_1.5s_ease-in-out_infinite_alternate]
">
  High Priority
</button>
```

**Animation Guidelines:**
- Use sparingly—only for important elements or status indicators
- Prefer subtle movements (floating, pulsing) over flashy effects
- Match animation duration to component importance (1-2s for badges, 20s for background decorations)

### 8. Handle Responsive Design

Build mobile-first, enhance for desktop:

```tsx
<section className="
  py-10          {/* Mobile padding */}
  md:py-15       {/* Desktop padding */}
  lg:py-20
">
  <div className="
    container
    max-w-[1400px]
    mx-auto
    px-4          {/* Mobile padding */}
    md:px-6       {/* Desktop padding */}
  ">
    <div className="
      grid
      grid-cols-1           {/* Mobile: stack */}
      md:grid-cols-2        {/* Tablet: 2 columns */}
      lg:grid-cols-3        {/* Desktop: 3 columns */}
      gap-6
    ">
      {/* Cards */}
    </div>
  </div>
</section>
```

**Responsive Patterns:**
- Stack grids vertically on mobile
- Remove rotation/skew on mobile for better readability
- Increase touch target sizes (min 44px height)
- Hide decorative background elements on small screens

### 9. Optimize Accessibility

Ensure WCAG compliance:

```tsx
<button
  className="..."
  aria-label="Add to wishlist"
  tabIndex={0}
>
  {/* Icon or text */}
</button>

{/* Images with alt text */}
<img
  src={image}
  alt={`${title} product render`}
  loading="lazy"
/>

{/* Semantic landmarks */}
<section aria-label="Product gallery">
  <h2 className="sr-only">Featured Products</h2>
  <div className="grid...">
    {/* Products */}
  </div>
</section>

{/* Focus indicators (never remove) */}
<a className="
  ...
  focus-visible:ring-4
  focus-visible:ring-black
  focus-visible:outline-none
">
  Link
</a>
```

### 10. Extract to Reusable Components

After implementing once, extract common patterns:

```tsx
// components/ui/neo-button.tsx
interface NeoButtonProps {
  variant?: 'primary' | 'secondary' | 'ghost';
  size?: 'sm' | 'md' | 'lg';
  children: React.ReactNode;
  onClick?: () => void;
}

export function NeoButton({
  variant = 'primary',
  size = 'md',
  children,
  ...props
}: NeoButtonProps) {
  const baseClasses = "font-bold uppercase border-3 border-black transition-all duration-150";

  const variantClasses = {
    primary: "bg-[#FF6B35] text-[#FFFEF0] hover:bg-[#E63946]",
    secondary: "bg-[#FFFEF0] text-black hover:bg-[#F5C518]",
    ghost: "bg-transparent border-black text-black hover:bg-black hover:text-[#F5C518]"
  };

  const sizeClasses = {
    sm: "px-4 py-2 text-xs",
    md: "px-6 py-3 text-sm",
    lg: "px-8 py-4 text-base"
  };

  const shadowClasses = "shadow-[4px_4px_0px_0px_rgba(0,0,0,1)] hover:translate-x-[-2px] hover:translate-y-[-2px] hover:shadow-[6px_6px_0px_0px_rgba(0,0,0,1)]";

  return (
    <button
      className={`${baseClasses} ${variantClasses[variant]} ${sizeClasses[size]} ${shadowClasses}`}
      {...props}
    >
      {children}
    </button>
  );
}
```

## Common Implementation Patterns

### Pattern 1: Card with Floating Badge

```tsx
function FeatureCard({ title, description, badge }) {
  return (
    <div className="relative">
      {/* Floating badge */}
      {badge && (
        <div className="
          absolute -top-4 -right-4
          bg-[#E63946] text-[#FFFEF0]
          px-4 py-2
          border-3 border-black
          font-bold text-xs uppercase
          rotate-6 z-10
        ">
          {badge}
        </div>
      )}

      {/* Card */}
      <div className="
        bg-[#FFFEF0]
        border-5 border-black
        shadow-[10px_10px_0px_0px_rgba(0,0,0,1)]
        p-8
        hover:translate-x-[-4px]
        hover:translate-y-[-4px]
        transition-all duration-200
      ">
        <h3 className="font-[Archivo_Black] text-2xl mb-4">{title}</h3>
        <p className="text-base leading-relaxed">{description}</p>
      </div>
    </div>
  );
}
```

### Pattern 2: Stats Row with Icons

```tsx
function StatsRow({ stats }) {
  return (
    <div className="flex gap-4 flex-wrap">
      {stats.map((stat, i) => (
        <div key={i} className="
          flex items-center gap-3
          bg-black text-[#F5C518]
          px-5 py-3
          border-3 border-black
          font-bold text-sm
          transition-all duration-150
          hover:bg-[#FF6B35]
          hover:text-[#FFFEF0]
          hover:translate-y-[-3px]
        ">
          {stat.icon}
          <span>{stat.label}</span>
        </div>
      ))}
    </div>
  );
}
```

### Pattern 3: Section with Decorative Header

```tsx
function Section({ icon, title, badge, children }) {
  return (
    <section className="py-12 md:py-16">
      <div className="container">
        {/* Section header */}
        <div className="flex items-center gap-5 mb-10">
          <div className="
            w-15 h-15
            bg-black text-[#F5C518]
            flex items-center justify-center
            text-3xl
            border-4 border-black
            flex-shrink-0
          ">
            {icon}
          </div>
          <h2 className="
            font-[Archivo_Black]
            text-4xl
            uppercase
            tracking-tight
            relative
            after:content-['']
            after:absolute
            after:-bottom-2
            after:left-0
            after:w-15
            after:h-1.5
            after:bg-[#FF6B35]
          ">
            {title}
          </h2>
        </div>

        {children}
      </div>
    </section>
  );
}
```

### Pattern 4: Image Gallery with Hover Effects

```tsx
function GalleryGrid({ items }) {
  return (
    <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
      {items.map((item, i) => (
        <div key={i} className="
          relative
          cursor-pointer
          transition-all duration-200
          hover:translate-x-[-4px]
          hover:translate-y-[-4px]
          group
        ">
          <div className="
            border-4 border-black
            shadow-[6px_6px_0px_0px_rgba(0,0,0,1)]
            group-hover:shadow-[10px_10px_0px_0px_rgba(0,0,0,1)]
            overflow-hidden
            bg-[#FFF9E0]
            transition-shadow duration-200
          ">
            <img
              src={item.image}
              alt={item.label}
              className="
                w-full h-50 object-cover
                transition-transform duration-300
                group-hover:scale-105
              "
            />
          </div>

          <div className="
            absolute -bottom-2.5 left-4
            bg-black text-[#F5C518]
            px-4 py-2
            text-xs font-bold uppercase
          ">
            {item.label}
          </div>
        </div>
      ))}
    </div>
  );
}
```

## Checklist for Every Component

Before considering a component complete:

- [ ] Applied the Trinity (border, shadow, hover) to interactive elements
- [ ] Used semantic colors matching component purpose
- [ ] Implemented proper typography hierarchy
- [ ] Added hover, active, and focus states
- [ ] Tested on mobile, tablet, and desktop
- [ ] Ensured WCAG AA contrast ratios
- [ ] Added proper ARIA labels and semantic HTML
- [ ] Verified keyboard navigation works
- [ ] Tested with screen reader (if time permits)
- [ ] Extracted reusable parts to shared components

## Performance Considerations

- Use `loading="lazy"` on images below the fold
- Prefer CSS animations over JavaScript for smooth performance
- Avoid deeply nested grids and flexbox (flatten when possible)
- Use `transition-all` sparingly—prefer specific properties like `transition-transform`
- Optimize shadow rendering by using transform instead of changing shadow values

## Common Pitfalls to Avoid

❌ **Don't**: Use blurred shadows or glows
✅ **Do**: Use hard-edged offset shadows only

❌ **Don't**: Round corners too much (avoid `rounded-full` on cards)
✅ **Do**: Use minimal radius (5px max) or sharp corners

❌ **Don't**: Use subtle grays for borders
✅ **Do**: Use solid black (`border-black`) for all borders

❌ **Don't**: Animate everything
✅ **Do**: Animate purposefully (status indicators, important CTAs)

❌ **Don't**: Use generic Tailwind colors (`bg-blue-500`)
✅ **Do**: Use design system tokens (`bg-[#3A7CA5]`)

❌ **Don't**: Skip hover states on interactive elements
✅ **Do**: Always implement the hover translation + shadow pattern

❌ **Don't**: Make elements too small (< 44px height for touch targets)
✅ **Do**: Ensure generous padding and minimum sizes
