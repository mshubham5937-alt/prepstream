# Design Guidelines: Competitive Exam Prep App (JEE/NEET)

## Brand Identity

**Purpose**: Empower Indian students preparing for JEE/NEET with AI-powered practice and instant tutoring.

**Aesthetic Direction**: **Editorial/Magazine** with a bold, confident personality. Think premium learning experience - clean typographic hierarchy, curated content presentation, and sophisticated use of space. The app should feel like a personal tutor, not a gamified toy.

**Memorable Element**: The AI Tutor is the hero feature - represented by a signature "Spark" icon that pulses subtly, suggesting intelligence and responsiveness. Dark mode as primary interface (better for long study sessions).

## Navigation Architecture

**Root Navigation**: Tab Bar (4 tabs)
1. **Practice** - Main question interface (home)
2. **Progress** - Stats, accuracy charts, streak tracking
3. **Library** - Saved questions, bookmarks, notes
4. **Profile** - Settings, language, logout (if auth)

**Floating Action Button**: "Ask AI Tutor" (appears when viewing solution)

**Authentication**: Optional SSO for progress sync across devices
- Apple Sign-In (iOS)
- Google Sign-In (Android/cross-platform)
- If no auth: local storage only, still include profile screen with avatar and preferences

## Screen-by-Screen Specifications

### 1. Practice Screen (Main)
**Purpose**: Display questions, accept answers, show results

**Layout**:
- **Header**: Transparent, custom
  - Left: Filter button (opens filters modal)
  - Center: Subject badge (e.g., "Physics • Level 3")
  - Right: Settings icon
- **Main Content**: Full-screen scrollable snap container (vertical snap-scroll between questions)
  - Each question is a full-viewport card
  - Top insets: headerHeight + 24px
  - Bottom insets: tabBarHeight + 24px
- **Floating Elements**: 
  - Submit button (bottom center, appears when option selected)
  - "Next Question" button (replaces submit after submission)
  - AI Tutor FAB (bottom right, appears after viewing solution)

**Components**:
- Question card (full screen)
- 4 option buttons (MCQ)
- Solution panel (slides up after submission)
- Difficulty indicator dots (1-5, top of card)
- AI-generated badge (if applicable)

**Empty State**: N/A (always generates questions)

### 2. Filters Modal (Native Modal)
**Purpose**: Set exam type, subject, difficulty, language

**Layout**:
- **Header**: Standard modal header
  - Left: Cancel text button
  - Center: "Filters"
  - Right: Apply button (primary action)
- **Main Content**: Scrollable form
  - Top insets: 16px
  - Bottom insets: insets.bottom + 24px

**Components**:
- Exam type selector (JEE/NEET) - segmented control
- Subject dropdown (includes "Mix" option)
- Difficulty slider (1-5 with descriptive labels)
- Language picker (13 Indian languages)
- Generate button (primary, full-width at bottom)

### 3. AI Tutor Chat (Slide-up Modal)
**Purpose**: Answer student doubts about current question

**Layout**:
- **Header**: Custom, attached to modal
  - Left: Sparkles icon (animated pulse)
  - Center: "AI Tutor"
  - Right: Close (X) button
- **Main Content**: Chat interface
  - Messages scrollable area
  - Top insets: 16px
  - Bottom insets: 0 (input bar is separate)
- **Fixed Input Bar**: Text input + send button
  - Bottom insets: insets.bottom + 16px

**Components**:
- Message bubbles (user: right-aligned, AI: left-aligned)
- Typing indicator (3 bouncing dots)
- Text input with send button
- Context banner (shows current question summary at top, dismissible)

**Empty State**: Shows welcome message from AI tutor

### 4. Progress Screen
**Purpose**: Visualize learning analytics and streaks

**Layout**:
- **Header**: Default navigation header, non-transparent
  - Title: "Your Progress"
  - Background: surface color
- **Main Content**: Scrollable
  - Top insets: 16px
  - Bottom insets: tabBarHeight + 24px

**Components**:
- Stats cards (questions attempted, accuracy %, current streak)
- Subject-wise breakdown (horizontal scrollable cards)
- Weekly activity heatmap
- Difficulty distribution chart
- Recent activity feed

**Empty State**: 
- Illustration: empty-progress.png
- Message: "Start practicing to see your stats here"
- CTA button: "Begin Practice"

### 5. Library Screen
**Purpose**: Access saved/bookmarked questions and notes

**Layout**:
- **Header**: Default with search bar
  - Title: "Library"
  - Search placeholder: "Search saved questions..."
- **Main Content**: List view (FlatList)
  - Top insets: 16px
  - Bottom insets: tabBarHeight + 24px

**Components**:
- Segmented control (Bookmarks / Notes / Mistakes)
- Question list items (shows subject, difficulty, preview)
- Swipe actions (remove bookmark, edit note)

**Empty State**:
- Illustration: empty-library.png
- Message: "Bookmark questions while practicing"
- Appears in each tab when empty

### 6. Profile Screen
**Purpose**: User settings, preferences, account management

**Layout**:
- **Header**: Custom, transparent
  - Large avatar at top
  - Display name below avatar
- **Main Content**: Scrollable form
  - Top insets: headerHeight + 120px (avatar height)
  - Bottom insets: tabBarHeight + 24px

**Components**:
- Avatar (circular, 80px, editable)
- Display name field
- Theme toggle (Dark/Light)
- Language preference
- Notifications toggle
- Account section (if auth enabled):
  - Sync status
  - Log out button (with confirmation)
  - Delete account (nested under Settings > Account, double confirmation)
- Privacy policy & terms links
- App version footer

## Color Palette

**Primary**: `#6366F1` (Indigo) - Confident, intelligent, not generic blue
**Primary Dark**: `#4F46E5`
**Accent**: `#F59E0B` (Amber) - Warmth for success states

**Background**: 
- Dark mode (default): `#0F1117` (deep navy-black)
- Light mode: `#FFFFFF`

**Surface**: 
- Dark: `#1A1D2E` (elevated cards)
- Light: `#F3F4F6`

**Borders**:
- Dark: `#2D3142`
- Light: `#E5E7EB`

**Text**:
- Primary (Dark): `#F9FAFB`
- Primary (Light): `#111827`
- Secondary (Dark): `#9CA3AF`
- Secondary (Light): `#6B7280`

**Semantic Colors**:
- Success: `#10B981` (Green)
- Error: `#EF4444` (Red)
- Warning: `#F59E0B` (Amber)
- Info: `#3B82F6` (Blue)

## Typography

**Font**: Nunito (Google Font) - Friendly, legible, approachable for long study sessions
**Fallback**: System sans-serif

**Type Scale**:
- Display (Question text): 24px, Bold, 1.4 line-height
- Heading 1: 20px, Bold
- Heading 2: 18px, SemiBold
- Body: 16px, Regular, 1.6 line-height
- Caption: 14px, Regular
- Small: 12px, Medium

**Hierarchy Principle**: Bold titles, Regular body. Use size + weight contrast, not color alone.

## Visual Design

**Icons**: Lucide icons (already in code) - consistent, modern
**Touchable Feedback**: 90% opacity on press for all buttons
**Shadows**: ONLY for floating action buttons:
  - shadowOffset: {width: 0, height: 2}
  - shadowOpacity: 0.10
  - shadowRadius: 2
**Borders**: 2px for option buttons, 1px for cards
**Spacing Scale**: 4px, 8px, 12px, 16px, 24px, 32px, 48px

## Assets to Generate

**Icon & Splash**:
1. `icon.png` - App icon: Bold "E" (for Exam) inside sparkle/brain fusion symbol, indigo gradient - WHERE: Device home screen
2. `splash-icon.png` - Same icon, larger - WHERE: Launch screen

**Empty States**:
3. `empty-library.png` - Open book with bookmark floating above, minimal line art - WHERE: Library screen when no saved items
4. `empty-progress.png` - Bar chart with single bar rising, aspirational feel - WHERE: Progress screen before practice begins

**Profile Avatars** (generate 6 preset options):
5. `avatar-1.png` through `avatar-6.png` - Geometric abstract avatars in brand colors - WHERE: Profile screen, user can select

**Onboarding**:
6. `onboard-welcome.png` - Student silhouette with sparkles representing AI assistance - WHERE: First launch welcome screen
7. `onboard-practice.png` - Stack of question cards with checkmark - WHERE: Onboarding step 2
8. `onboard-progress.png` - Rising graph with trophy - WHERE: Onboarding step 3

**Illustration Style**: Minimal line art with subtle gradients using primary colors. No clipart. Think Duolingo's sophistication, not its cartoonishness.