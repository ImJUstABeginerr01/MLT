# UKOM Exam Preparation App - Design Guidelines

## Design Approach
**System**: Material Design with productivity-focused adaptations, inspired by Linear's clarity and Notion's organization patterns for educational efficiency.

**Core Principle**: Clarity and efficiency for high-stakes exam preparation. Every element serves learning and assessment goals.

---

## Layout System

**Spacing Units**: Tailwind units of 2, 4, 6, 8, and 12 for consistent rhythm
- Component padding: p-4 to p-6
- Section spacing: py-8 to py-12
- Card gaps: gap-4 to gap-6

**Container Structure**:
- Landing page: max-w-6xl centered
- Exam interface: Full-width with side navigation (fixed sidebar 280px)
- Admin panel: max-w-7xl with dashboard grid

---

## Typography

**Font Family**: Inter (Google Fonts) for optimal screen readability
- Headers: font-semibold to font-bold
- Body: font-normal
- Stats/Numbers: font-medium, tabular-nums

**Hierarchy**:
- Page titles: text-3xl md:text-4xl font-bold
- Section headers: text-xl md:text-2xl font-semibold
- Question text: text-lg leading-relaxed
- Labels/metadata: text-sm font-medium
- Timer display: text-2xl md:text-3xl font-bold tabular-nums

---

## Component Library

### Landing Page
**Layout**: Clean, centered single-column with generous spacing (py-20 to py-32)

1. **Header** (sticky top-0)
   - Logo/App name (text-2xl font-bold)
   - Navigation links
   - "Login Admin" button (top-right)

2. **Hero Section** (py-24)
   - Main heading: "Platform Persiapan UKOM Profesional"
   - Subheading explaining purpose
   - Two prominent CTA cards side-by-side (grid-cols-1 md:grid-cols-2 gap-6):
     - "Tryout UKOM" card with icon and description
     - "Simulasi UKOM" card with icon and description
   - Each card: rounded-xl border-2 p-8 hover effect with arrow icon

3. **Features Section** (py-20)
   - Grid of 4 feature cards (grid-cols-1 md:grid-cols-2 lg:grid-cols-4)
   - Icons from Heroicons: Clock (Timer), BookmarkSquare (Save), ChartBar (Statistics), AcademicCap (6 Sections)

4. **Footer** (py-12 border-t)
   - Credits: "Dikembangkan oleh: [Developer Name]"
   - "Bank Soal oleh: [Creator Name]"
   - Copyright and version info

### Exam Interface

**Layout**: Fixed sidebar (280px) + Main content area

**Sidebar Components**:
1. **Header Block**
   - Mode badge (Tryout/Simulasi)
   - Subject name (text-lg font-semibold)
   - Section indicator (e.g., "Section 1 of 6")

2. **Timer Display** (prominent at top)
   - Large countdown (text-3xl font-bold tabular-nums)
   - Progress ring/bar showing time remaining
   - Warning state when < 10 minutes

3. **Question Navigator**
   - Grid of question numbers (grid-cols-5 gap-2)
   - Each number as button (w-10 h-10 rounded-lg)
   - Visual states:
     - Unanswered: border-2
     - Answered: filled
     - Bookmarked: star icon overlay (absolute top-0 right-0)
     - Current: ring-2 ring-offset-2
   - Legend below grid explaining states

4. **Action Buttons** (sticky bottom)
   - "Submit Ujian" (full-width, rounded-lg py-3)
   - "Keluar" (outline variant)

**Main Content Area**:
1. **Question Header**
   - Question number (text-2xl font-bold)
   - Bookmark toggle button (top-right, icon button with tooltip)

2. **Question Content**
   - Question text (text-lg leading-relaxed mb-8)
   - Image support (max-w-2xl rounded-lg mb-6) if applicable

3. **Answer Options**
   - Radio button list (space-y-4)
   - Each option: rounded-xl border-2 p-4 with hover state
   - Selected state: border-4 with checkmark icon

4. **Navigation Bar** (bottom, py-6 border-t)
   - Previous button (left)
   - Bookmark toggle (center)
   - Next button (right)
   - All buttons: rounded-lg px-6 py-3

### Results/Statistics Screen

**Layout**: Full-width with max-w-4xl centered

1. **Score Card** (top, rounded-2xl p-8 mb-8)
   - Large score display (text-6xl font-bold)
   - Pass/fail indicator
   - Completion time

2. **Statistics Grid** (grid-cols-1 md:grid-cols-3 gap-6)
   - Correct answers count with icon
   - Accuracy percentage with progress bar
   - Section breakdown with mini-charts

3. **Section Performance** (space-y-4)
   - Each section: rounded-xl p-6
   - Section name, score, progress bar
   - "Review Answers" button

4. **Readiness Assessment**
   - Text analysis with recommendations
   - "Coba Lagi" and "Lanjut Section Berikutnya" buttons

### Admin Panel

**Layout**: Dashboard with sidebar navigation (256px)

**Sidebar**:
- Dashboard link
- Manage Questions
- View Statistics
- User Management
- Logout button (bottom)

**Main Content**:
1. **Question Management Table**
   - Filters: Subject dropdown, Section dropdown, Search input
   - Table columns: ID, Question preview (truncated), Subject, Section, Actions
   - Actions: Edit (icon), Delete (icon)
   - "Add Question" button (top-right, rounded-lg px-6 py-3)

2. **Add/Edit Question Form** (max-w-3xl)
   - Form sections with clear labels
   - Subject selector (dropdown)
   - Section selector (dropdown)
   - Question textarea (min-h-32)
   - Image upload (drag-drop zone, rounded-xl border-2 border-dashed p-8)
   - Answer options (space-y-3, each with radio for correct answer)
   - Save/Cancel buttons (bottom)

---

## Interaction Patterns

**Animations**: Minimal, focus on functional feedback
- Button hover: subtle scale (scale-105)
- Card hover: gentle lift (shadow transition)
- Modal entrance: fade + slide from center
- Timer warning: gentle pulse when < 10 min

**Modals**:
- Submit confirmation: centered, rounded-2xl, p-8
- Warning dialogs: smaller, focused message
- Backdrop: backdrop-blur-sm

---

## Icons
Use **Heroicons** via CDN for consistent iconography throughout.

---

## Responsive Behavior

**Mobile** (< 768px):
- Sidebar becomes bottom sheet (pull-up drawer)
- Question navigator: grid-cols-5 (smaller buttons)
- Statistics: single column stack
- Admin table: card-based view instead of table

**Tablet/Desktop** (≥ 768px):
- Full sidebar layout
- Multi-column grids as specified
- Enhanced hover states