# Neo-brutalism Component Patterns

Component patterns extracted from the GMK Flare mockup, demonstrating production-ready Neo-brutalism design implementation.

## Design System Tokens

```css
/* Core Colors */
--yellow: #F5C518;
--yellow-light: #FFF9E0;
--orange: #FF6B35;
--orange-dark: #E55A2B;
--black: #1a1a1a;
--white: #FFFEF0;
--red: #E63946;
--green: #2D936C;
--gray: #6B7280;

/* Shadows (offset, no blur) */
--shadow: 6px 6px 0px var(--black);
--shadow-sm: 4px 4px 0px var(--black);
--shadow-lg: 10px 10px 0px var(--black);
--shadow-hover: 12px 12px 0px var(--black);

/* Tailwind Equivalents */
neo-shadow: shadow-[4px_4px_0px_0px_rgba(0,0,0,1)]
neo-shadow-lg: shadow-[10px_10px_0px_0px_rgba(0,0,0,1)]
neo-border: border-2 border-black
neo-hover: hover:translate-x-[-4px] hover:translate-y-[-4px] hover:shadow-none transition-all duration-150
```

## Animations

```css
@keyframes float {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  50% { transform: translateY(-20px) rotate(3deg); }
}

@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.1); }
}

@keyframes bounce {
  0%, 100% { transform: rotate(-8deg) translateY(0); }
  50% { transform: rotate(-8deg) translateY(-5px); }
}

@keyframes glow {
  from { box-shadow: 4px 4px 0 var(--black); }
  to { box-shadow: 4px 4px 20px rgba(230, 57, 70, 0.5), 4px 4px 0 var(--black); }
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.3; }
}
```

## Button Patterns

### Primary Button
```tsx
<button className="
  px-6 py-3
  bg-[#FF6B35] text-[#FFFEF0]
  border-3 border-black
  shadow-[4px_4px_0px_0px_rgba(0,0,0,1)]
  hover:translate-x-[-2px] hover:translate-y-[-2px]
  hover:shadow-[6px_6px_0px_0px_rgba(0,0,0,1)]
  hover:bg-[#E63946]
  transition-all duration-150
  font-bold text-sm uppercase tracking-wide
">
  Primary Action
</button>
```

### Outline Button
```tsx
<button className="
  px-6 py-3
  bg-[#FFFEF0] text-black
  border-3 border-black
  shadow-[4px_4px_0px_0px_rgba(0,0,0,1)]
  hover:translate-x-[-2px] hover:translate-y-[-2px]
  hover:shadow-[6px_6px_0px_0px_rgba(0,0,0,1)]
  transition-all duration-150
  font-bold text-sm uppercase tracking-wide
">
  Secondary Action
</button>
```

### Icon Button
```tsx
<button className="
  flex items-center gap-3
  px-7 py-4
  bg-[#FF6B35] text-[#FFFEF0]
  border-4 border-black
  shadow-[6px_6px_0px_0px_rgba(0,0,0,1)]
  hover:translate-x-[-4px] hover:translate-y-[-4px]
  hover:shadow-[12px_12px_0px_0px_rgba(0,0,0,1)]
  hover:bg-[#E63946]
  transition-all duration-150
  font-[Archivo_Black] text-base uppercase tracking-wider
">
  <span>🔔</span>
  <span>Notify Me</span>
</button>
```

## Badge Patterns

### Standard Badge
```tsx
<span className="
  inline-block px-5 py-2.5
  bg-[#FFFEF0] text-black
  border-3 border-black
  shadow-[4px_4px_0px_0px_rgba(0,0,0,1)]
  font-bold text-xs uppercase tracking-wide
  cursor-pointer
  hover:translate-x-[-2px] hover:translate-y-[-2px]
  hover:shadow-[6px_6px_0px_0px_rgba(0,0,0,1)]
  hover:bg-[#FF6B35] hover:text-[#FFFEF0]
  transition-all duration-150
">
  Tag Name
</span>
```

### Floating Badge (Keycap)
```tsx
<div className="
  absolute -top-4 -left-4
  bg-black text-[#F5C518]
  px-6 py-3
  font-[Archivo_Black] text-sm uppercase tracking-wider
  rotate-[-8deg] z-10
  animate-bounce
">
  KEYCAP
</div>
```

### Status Badge
```tsx
<div className="
  inline-flex items-center gap-2.5
  bg-[#F5C518] text-black
  px-5 py-2.5
  font-bold text-xs
">
  <span className="
    w-2.5 h-2.5
    bg-[#E63946]
    rounded-full
    animate-blink
  "></span>
  Live Status
</div>
```

## Card Patterns

### Basic Card
```tsx
<div className="
  bg-[#FFFEF0]
  border-5 border-black
  shadow-[10px_10px_0px_0px_rgba(0,0,0,1)]
  p-9
  relative
  rotate-1
">
  {/* Content */}
</div>
```

### Hoverable Card
```tsx
<div className="
  bg-[#FFFEF0]
  border-5 border-black
  shadow-[10px_10px_0px_0px_rgba(0,0,0,1)]
  p-9
  cursor-pointer
  transition-all duration-200
  hover:translate-x-[-4px] hover:translate-y-[-4px]
">
  {/* Content */}
</div>
```

### Card with Header
```tsx
<div className="bg-[#FFFEF0] border-5 border-black shadow-[10px_10px_0px_0px_rgba(0,0,0,1)]">
  <div className="
    bg-black text-[#F5C518]
    px-6 py-5
    font-[Archivo_Black] text-lg uppercase tracking-wider
    flex items-center gap-4
  ">
    <span className="text-2xl">📊</span>
    <span>Card Title</span>
  </div>
  <div className="p-6">
    {/* Content */}
  </div>
</div>
```

## Hero Section Pattern

```tsx
<section className="py-10 md:py-15">
  <div className="container max-w-[1400px] mx-auto px-5">
    {/* Breadcrumb */}
    <nav className="flex items-center gap-2.5 mb-8 text-sm font-bold">
      <a className="
        text-black no-underline px-4 py-2
        bg-[#FFFEF0] border-3 border-black
        shadow-[3px_3px_0px_0px_rgba(0,0,0,1)]
        transition-all duration-150
        hover:translate-x-[-2px] hover:translate-y-[-2px]
        hover:shadow-[5px_5px_0px_0px_rgba(0,0,0,1)]
      ">
        🏠 Home
      </a>
      <span className="text-xl">→</span>
      <a>Interest Checks</a>
    </nav>

    {/* Hero Grid */}
    <div className="grid md:grid-cols-[1.2fr_1fr] gap-10 items-start">
      {/* Image Section */}
      <div className="relative rotate-[-2deg] transition-transform duration-300 hover:rotate-0 hover:scale-105">
        <div className="
          bg-[#FFFEF0] border-5 border-black
          shadow-[10px_10px_0px_0px_rgba(0,0,0,1)]
          p-5 relative overflow-hidden
        ">
          {/* Decorative stripe */}
          <div className="
            absolute top-0 left-0 right-0 h-10
            bg-[repeating-linear-gradient(90deg,#FF6B35_0px,#FF6B35_20px,#F5C518_20px,#F5C518_40px)]
            border-b-4 border-black
          "></div>

          <img src="..." className="w-full h-auto block mt-8" />
        </div>

        {/* Floating badges */}
        <div className="absolute -top-4 -left-4 bg-black text-[#F5C518] px-6 py-3 font-[Archivo_Black] text-sm uppercase tracking-wider rotate-[-8deg] z-10 animate-bounce">
          KEYCAP
        </div>
        <div className="absolute top-5 -right-6 bg-[#E63946] text-[#FFFEF0] px-8 py-4 font-[Archivo_Black] text-base uppercase tracking-[3px] border-4 border-black shadow-[6px_6px_0px_0px_rgba(0,0,0,1)] rotate-12 z-10">
          HIGH INTEREST
        </div>
      </div>

      {/* Info Card */}
      <div className="
        bg-[#FFFEF0] border-5 border-black
        shadow-[10px_10px_0px_0px_rgba(0,0,0,1)]
        p-9 relative rotate-1
      ">
        {/* Emoji decoration */}
        <div className="absolute -top-8 right-8 text-5xl animate-flame">🔥</div>

        {/* Content */}
        <div className="mb-6 relative">
          <h1 className="font-[Archivo_Black] text-5xl leading-tight text-black uppercase tracking-tight">
            GMK CYL <span className="text-[#FF6B35]">FLARE</span> (IC)
          </h1>
          <div className="absolute -bottom-2.5 left-0 w-20 h-2 bg-[#FF6B35]"></div>
        </div>

        <p className="text-base leading-relaxed text-black my-8 p-5 bg-[#F5C518] border-3 border-dashed border-black">
          Description text...
        </p>

        {/* Stats */}
        <div className="flex gap-4 my-6 flex-wrap">
          <div className="
            bg-black text-[#F5C518]
            px-5 py-3 flex items-center gap-2.5
            font-bold text-sm
            border-3 border-black
            transition-all duration-150
            hover:bg-[#FF6B35] hover:text-[#FFFEF0]
            hover:translate-y-[-3px]
          ">
            <svg className="w-4.5 h-4.5" viewBox="0 0 24 24" fill="currentColor">
              <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
            </svg>
            73 replies
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
```

## Gallery Grid Pattern

```tsx
<section className="py-12 md:py-16">
  <div className="container">
    <div className="bg-[#FFFEF0] border-5 border-black shadow-[10px_10px_0px_0px_rgba(0,0,0,1)] p-10 relative">
      {/* Badge decoration */}
      <div className="absolute -top-6 right-10 text-4xl bg-[#F5C518] px-4 py-1 border-4 border-black">📸</div>

      <div className="grid grid-cols-1 md:grid-cols-3 gap-6 mt-8">
        {items.map((item) => (
          <div className="
            relative cursor-pointer
            transition-all duration-200
            hover:translate-x-[-4px] hover:translate-y-[-4px]
            group
          ">
            <div className="
              border-4 border-black
              shadow-[6px_6px_0px_0px_rgba(0,0,0,1)]
              group-hover:shadow-[10px_10px_0px_0px_rgba(0,0,0,1)]
              overflow-hidden bg-[#FFF9E0]
              transition-shadow duration-200
            ">
              <img className="
                w-full h-50 object-cover block
                transition-transform duration-300
                group-hover:scale-105
              " />
            </div>

            <div className="absolute -bottom-2.5 left-4 bg-black text-[#F5C518] px-4 py-2 text-xs font-bold uppercase tracking-wide">
              Label
            </div>

            {item.featured && (
              <div className="absolute top-4 -right-2.5 bg-[#FF6B35] text-[#FFFEF0] px-3 py-1.5 text-xs font-bold uppercase border-3 border-black rotate-3">
                Featured
              </div>
            )}
          </div>
        ))}
      </div>

      {/* Navigation */}
      <div className="flex justify-center gap-4 mt-10">
        <button className="
          w-12 h-12 bg-[#F5C518]
          border-4 border-black
          shadow-[4px_4px_0px_0px_rgba(0,0,0,1)]
          cursor-pointer text-xl
          flex items-center justify-center
          transition-all duration-150
          hover:translate-x-[-2px] hover:translate-y-[-2px]
          hover:shadow-[6px_6px_0px_0px_rgba(0,0,0,1)]
          hover:bg-[#FF6B35]
        ">
          ←
        </button>
      </div>
    </div>
  </div>
</section>
```

## Sentiment Bar Pattern

```tsx
<div className="mt-8 p-6 bg-[#F5C518] border-4 border-black">
  <div className="flex justify-between items-center mb-5 flex-wrap gap-4">
    <div>
      <h3 className="font-[Archivo_Black] text-lg uppercase tracking-wider">
        Community Sentiment
      </h3>
      <span className="bg-black text-[#F5C518] px-4 py-2 font-bold">
        43 votes
      </span>
    </div>

    <div className="
      bg-[#E63946] text-[#FFFEF0]
      px-5 py-2.5
      font-[Archivo_Black] text-sm uppercase tracking-wider
      border-3 border-black
      shadow-[4px_4px_0px_0px_rgba(0,0,0,1)]
      animate-glow
    ">
      🔥 HIGH INTEREST
    </div>
  </div>

  <div className="flex flex-col gap-4">
    {[
      { label: 'Positive', value: 44, color: 'bg-[repeating-linear-gradient(45deg,#4CAF50,#4CAF50_10px,#45a049_10px,#45a049_20px)]' },
      { label: 'Neutral', value: 35, color: 'bg-[repeating-linear-gradient(45deg,#9E9E9E,#9E9E9E_10px,#888_10px,#888_20px)]' },
      { label: 'Negative', value: 21, color: 'bg-[repeating-linear-gradient(45deg,#E63946,#E63946_10px,#c0392b_10px,#c0392b_20px)]' }
    ].map(bar => (
      <div className="flex items-center gap-4">
        <span className="w-20 font-bold text-xs uppercase">{bar.label}</span>
        <div className="flex-1 h-8 bg-[#FFFEF0] border-3 border-black relative overflow-hidden">
          <div className={`h-full ${bar.color} transition-all duration-1000`} style={{ width: `${bar.value}%` }}></div>
        </div>
        <span className="w-12 font-bold text-base text-right">{bar.value}%</span>
      </div>
    ))}
  </div>
</div>
```

## Info Row Pattern

```tsx
<div className="flex justify-between items-center py-4 border-b-3 border-dashed border-black last:border-b-0">
  <span className="font-bold uppercase text-xs tracking-wide text-[#6B7280] flex items-center gap-2.5">
    <svg className="w-4.5 h-4.5" />
    Label
  </span>
  <span className="font-bold text-base text-black text-right">
    Value
  </span>
</div>

{/* Highlighted value */}
<div className="flex justify-between items-center py-4">
  <span className="font-bold uppercase text-xs tracking-wide text-[#6B7280]">
    Label
  </span>
  <span className="
    font-bold text-base text-black
    bg-[#FF6B35] text-[#FFFEF0]
    px-4 py-2 border-3 border-black
  ">
    73
  </span>
</div>
```

## Background Decorations

```tsx
{/* Fixed background shapes */}
<div className="fixed pointer-events-none z-0">
  {/* Zigzag */}
  <div className="
    absolute top-[15%] -left-12 w-50 h-10
    bg-[repeating-linear-gradient(90deg,var(--black)_0px,var(--black)_20px,transparent_20px,transparent_40px)]
    skew-y-[-5deg] animate-float opacity-30
  " />

  {/* Circle outline */}
  <div className="
    absolute top-[25%] right-[3%] w-30 h-30
    border-6 border-dashed border-black rounded-full
    animate-spin opacity-20
  " style={{ animationDuration: '20s' }} />

  {/* Dots grid */}
  <div className="
    absolute bottom-[20%] left-[2%] w-25 h-25
    bg-[radial-gradient(black_3px,transparent_3px)]
    bg-[size:15px_15px]
    animate-float-reverse opacity-20
  " />

  {/* Star */}
  <div className="
    absolute top-[60%] right-[5%]
    text-8xl text-black animate-pulse opacity-15
  ">
    ✦
  </div>
</div>
```

## Responsive Patterns

```tsx
{/* Mobile-first responsive grid */}
<div className="
  grid grid-cols-1
  md:grid-cols-2
  lg:grid-cols-3
  gap-6
">
  {/* Cards */}
</div>

{/* Conditional rotation on mobile */}
<div className="
  rotate-0
  md:rotate-[-2deg]
  transition-transform
">
  {/* Content */}
</div>

{/* Stack on mobile, side-by-side on desktop */}
<div className="
  flex flex-col
  md:flex-row
  gap-4
">
  {/* Items */}
</div>
```
