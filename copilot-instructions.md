---
description: Workspace customization and design guidance for Soc Ops Social Bingo project.
---

# Soc Ops — Copilot Instructions

This document captures the design system, codebase conventions, and development practices for the Soc Ops project.

---

## 🎨 Design System & Pink Theme

### Color Palette

The current design uses a vibrant **Pink Theme** with the following CSS variables:

```css
--primary-pink: #ff1493       /* Deep, bold pink */
--hot-pink: #ff69b4           /* Bright, playful pink */
--coral: #ff6b9d              /* Warm coral accent */
--blush: #ffc0d9              /* Soft, welcoming blush */
--cream: #fff5f7              /* Off-white background */
--white: #ffffff              /* Pure white */
--text-dark: #2d1b3d          /* Deep purple-dark text */
--text-light: #7a5a7a         /* Muted purple text */
--accent-green: #52c77d       /* Success/completion green */
--accent-gold: #ffd700        /* Victory/celebration gold */
```

#### When to Use Each Color

- **Primary Pink** (`#ff1493`): Main CTA buttons, headings, primary accents
- **Hot Pink** (`#ff69b4`): Secondary interactive elements, hover states, decorative borders
- **Blush** (`#ffc0d9`): Soft backgrounds, card overlays, subtle accents
- **Cream** (`#fff5f7`): Page background, light container backgrounds
- **Accent Green** (`#52c77d`): Selected tiles, completion feedback
- **Accent Gold** (`#ffd700`): Victory banner, winning lines, celebration moments

### Typography

**Font Stack:**
- **Headlines & UI**: Fredoka (400, 500, 600, 700 weights) — friendly, rounded, modern
- **Body & UI Copy**: Outfit (300, 400, 600, 700 weights) — clean, geometric, readable

**Usage:**
- Page titles and major headings: Fredoka 700 with gradient text (Pink → Hot Pink)
- Subheadings and labels: Fredoka 600, regular weight for body copy
- Small text and hints: Outfit 400, lighter weight for secondary info

### Component Styling

#### Buttons

Primary buttons use gradient backgrounds with hover lift animation:

```css
background: linear-gradient(135deg, var(--primary-pink), var(--hot-pink));
transition: all 0.3s ease;
box-shadow: 0 8px 20px rgba(255, 20, 147, 0.3);

/* Hover: translate up, increase shadow */
transform: translateY(-2px);
box-shadow: 0 12px 28px rgba(255, 20, 147, 0.4);
```

#### Cards

Semi-transparent white cards with backdrop blur for depth:

```css
background: rgba(255, 255, 255, 0.7);
backdrop-filter: blur(10px);
border: 2px solid rgba(255, 20, 147, 0.1);
border-radius: 1.5rem;
box-shadow: 0 8px 32px rgba(255, 20, 147, 0.1);
```

#### Tiles (Bingo Grid)

- **Default**: White background, pink border, dark text
- **Hovered**: Scale up 1.05, darker pink border, light pink background
- **Selected**: Green background with white text, green border, success checkmark
- **Winning**: Gold background with gold border, celebration styling
- **Free Cell**: Pink gradient background, larger font weight, disabled cursor

#### Animations

All major animations are **staggered** using `animation-delay` for polished reveal sequences:

```css
/* Stagger tiles on load */
animation: tileSlideIn 0.4s ease-out backwards;
animation-delay: calc(var(--index) * 30ms);

/* Stagger modal elements */
animation: slideUpCard 0.6s ease-out var(--index) * 0.1s both;
```

**Key animations:**
- `lobbyFadeIn`: Page load fade-in (0.8s)
- `lobbyBounceIn`: Content scale bounce (0.6s)
- `tileSlideIn`: Tile grid stagger (0.4s per tile)
- `victoryBounce`: Modal celebration bounce (0.6s)
- `emojiFloat`: Victory emoji floating motion (0.8s infinite)

### Responsive Behavior

- **Desktop**: Full 5×5 grid at `max-width: 24rem`
- **Tablet**: Grid scales with viewport, maintains 1:1 aspect ratio
- **Mobile** (< 480px): Font sizes reduce, grid uses 100% width
- All elements use touch-friendly sizes (min 44px tap targets)

---

## 🏗️ File Structure & Conventions

### Frontend Files

```
socops/src/main/resources/
├── templates/
│   └── game.html              # Thymeleaf template (HTML + inline JS)
└── static/
    └── css/
        └── app.css            # Pink theme stylesheet
```

### Backend Files

```
socops/src/main/java/com/socops/
├── SocOpsApplication.java     # Spring Boot entry point
├── web/
│   └── BingoRestController.java   # REST API endpoints
├── service/
│   └── BoardAssembler.java        # Game logic & board generation
├── model/
│   ├── BingoCell.java             # Cell data model
│   ├── PlayPhase.java             # Game phase enum
│   └── WinningStreak.java         # Victory detection result
└── data/
    └── IcebreakerPrompts.java     # Question bank
```

### Key Endpoints

- **GET** `/` → Renders `game.html` lobby
- **GET** `/api/bingo/fresh-board` → Returns 25 `BingoCell` objects (JSON)

---

## 🧪 Development Practices

### Linting & Code Quality

- **Maven Checkstyle**: Enforces unused imports, star import avoidance, code style
  - Run: `./mvnw -DskipTests checkstyle:check`
  - Config: `socops/config/checkstyle/checkstyle.xml`

### Testing

- **Unit Tests**: `src/test/java/com/socops/service/BoardAssemblerTests.java`
- **Run**: `./mvnw test`
- **TDD Workflow**: Use Explore agent for codebase discovery; TDD agents for test-driven features

### Build & Run

```bash
cd socops

# Build
./mvnw clean package

# Run
./mvnw spring-boot:run

# Test
./mvnw test

# Checkstyle
./mvnw -DskipTests checkstyle:check
```

---

## 🎯 Design Guidelines for Future Work

### When Adding UI Features

1. **Typography First**: Choose fonts that feel alive and distinctive
2. **Color Cohesion**: Extend the pink/coral/green palette; avoid introducing conflicting colors
3. **Motion Matters**: Add purposeful animations; avoid motion sickness (test with reduced-motion)
4. **Accessibility**: Ensure 4.5:1 contrast ratio, keyboard navigation, ARIA labels
5. **Performance**: Use CSS-only animations; minimize JavaScript animations

### When Modifying game.html

- Keep the modal, grid, and phase logic intact
- Extend component styling by adding new `.{feature}-*` classes in `app.css`
- Test on mobile (< 480px) and desktop (> 1024px)
- Preserve localStorage persistence for game state

### When Extending app.css

- Define new variables at the `:root` level (don't hard-code colors)
- Use CSS Grid and Flexbox for layout (no floats)
- Include `@media (prefers-reduced-motion: reduce)` in animated sections
- Group related styles with section comments: `/* ════ SECTION NAME ════ */`

### Custom Agents

- **Cloud Agent** (`.github/agents/cloud.agent.md`): Deployment and infrastructure guidance
- **UI Review** (`.github/agents/ui-review.agent.md`): Deep UX audit and screenshot testing
- **TDD Agents** (`.github/agents/tdd*.agent.md`): Test-driven feature development
- **Quiz Master** (`.github/agents/quiz-master.agent.md`): Themed icebreaker prompt curation

---

## 📚 Learning Resources

- **Frontend Design Guide**: `.github/instructions/frontend-design.instructions.md`
- **Setup Instructions**: `.github/instructions/setup.instructions.md`
- **Workshop Guides**: `workshop/` folder (01-setup through 04-multi-agent)

---

## ✨ Design Philosophy

Soc Ops is a **social-first, delightful-first** application. Every design decision should:

1. **Encourage Connection**: Use warm, inviting colors and friendly typography
2. **Celebrate Moments**: Animate victories, embrace joy in interactions
3. **Prioritize Clarity**: Clear hierarchy, readable text, intuitive interactions
4. **Respect Speed**: Smooth animations at 60fps, instant feedback on taps
5. **Include Everyone**: High contrast, keyboard support, accessible color choices

The pink theme communicates playfulness and energy while maintaining professionalism and clarity. All interactive elements should feel responsive, tactile, and alive.
