# PhotoStyleMatch - UI Design Document

## 1. Design Principles

The PhotoStyleMatch UI is designed around the following core principles:

1. **Simplicity** - Clear, intuitive interfaces that guide users through the styling process
2. **Visual Focus** - Emphasis on the photos themselves with minimal UI distraction
3. **Progressive Disclosure** - Reveal complexity only when needed
4. **Responsive Design** - Full functionality across desktop and mobile devices
5. **Professional Aesthetic** - Clean, modern look that appeals to photographers
6. **Clear Feedback** - Transparent process status and results

## 2. Brand Identity

### 2.1 Color Palette

- **Primary**: #3B82F6 (Vibrant Blue) - Represents creativity and technology
- **Secondary**: #10B981 (Emerald Green) - Represents success and completion
- **Accent**: #F59E0B (Amber) - Used for call-to-action elements
- **Neutrals**:
  - #1F2937 (Dark Gray) - Text and headers
  - #F3F4F6 (Light Gray) - Backgrounds
  - #FFFFFF (White) - Cards and content areas
- **Feedback Colors**:
  - #EF4444 (Red) - Errors and warnings
  - #10B981 (Green) - Success messages

### 2.2 Typography

- **Headings**: Inter (Sans-serif), Bold/Semi-bold
- **Body**: Inter (Sans-serif), Regular/Light
- **Accent**: Inter (Sans-serif), Medium Italic
- **Font Sizes**:
  - Mobile: 14px base with 1.5 line height
  - Desktop: 16px base with 1.5 line height

### 2.3 Logo and Iconography

- **Logo**: Modern, minimalist design incorporating a camera aperture and color palette
- **Icons**: Outline style, consistent weight, rounded corners for cohesive look
- **Usage**: Icon + text for primary navigation, icons only for secondary actions

## 3. Responsive Layout Strategy

### 3.1 Breakpoints

- **Mobile**: < 640px
- **Tablet**: 640px - 1024px
- **Desktop**: > 1024px
- **Large Desktop**: > 1440px

### 3.2 Grid System

- 12-column grid for desktop layouts
- Stack components vertically on mobile
- Consistent spacing system (4px base unit)

### 3.3 Navigation

- **Desktop**: Horizontal navigation bar with dropdown menus
- **Mobile**: Hamburger menu expanding to full-screen navigation
- **Persistent**: User credits/account access always visible

## 4. Component Library

### 4.1 Core Components

#### 4.1.1 Buttons

- **Primary**: Filled, rounded, blue background
- **Secondary**: Outlined, rounded, transparent background
- **Tertiary**: Text-only, underline on hover
- **States**: Default, Hover, Active, Disabled

#### 4.1.2 Form Elements

- **Text Inputs**: Outlined with clear focus states
- **Dropdowns**: Custom styled selects with search functionality when appropriate
- **Checkboxes & Radio Buttons**: Custom styled for brand consistency
- **File Upload**: Drag-and-drop area with progress indicator

#### 4.1.3 Cards

- **Project Card**: Displays project thumbnail, name, status
- **Photo Card**: Shows photo with metadata and action buttons
- **Result Card**: Before/after comparison with download options

#### 4.1.4 Modals & Dialogs

- **Standard Modal**: White background, rounded corners, clear X to close
- **Alert Dialog**: Used for confirmations and warnings
- **Toast Notifications**: Non-intrusive status updates

#### 4.1.5 Navigation Elements

- **Primary Nav**: Main site sections
- **Secondary Nav**: Context-specific options
- **Breadcrumbs**: For deep navigation paths
- **Pagination**: For long lists of content

### 4.2 Custom Components

#### 4.2.1 Photo Upload Area

- Drag-and-drop zone with clear visual cues
- Multi-file selection support
- Upload progress visualization
- File validation feedback

#### 4.2.2 Style Analysis Display

- Visual representation of detected style
- Color palette extraction
- Histogram comparisons
- Parameter visualization

#### 4.2.3 Before/After Comparison

- Slider interface for comparing original and edited photos
- Split screen with adjustable divider
- Zooming capabilities
- Side-by-side grid view for multiple photos

#### 4.2.4 Chat Interface

- Clean, modern chat UI
- Support for image thumbnails in conversation
- Typing indicators
- Suggestion chips for common questions/actions

## 5. Screen Designs

### 5.1 Landing Page

#### 5.1.1 Layout

```
┌─────────────────────────────────────────────────┐
│                    HEADER                        │
├─────────────────────────────────────────────────┤
│                                                 │
│            HERO SECTION WITH CTA                │
│                                                 │
├─────────────────────────────────────────────────┤
│                                                 │
│            FEATURE SHOWCASE                     │
│                                                 │
├─────────────────────────────────────────────────┤
│                                                 │
│            EXAMPLE TRANSFORMATIONS              │
│                                                 │
├─────────────────────────────────────────────────┤
│                                                 │
│            USE CASES                            │
│                                                 │
├─────────────────────────────────────────────────┤
│                                                 │
│            PRICING                              │
│                                                 │
├─────────────────────────────────────────────────┤
│                                                 │
│            TESTIMONIALS                         │
│                                                 │
├─────────────────────────────────────────────────┤
│                                                 │
│            FINAL CTA                            │
│                                                 │
├─────────────────────────────────────────────────┤
│                    FOOTER                        │
└─────────────────────────────────────────────────┘
```

#### 5.1.2 Key Elements

- **Hero Section**: Bold headline, subheading, and primary CTA button
- **Feature Showcase**: Icon + text descriptions of key features
- **Example Transformations**: Before/after sliders showing impressive results
- **Use Cases**: Cards describing different user scenarios (casual vs professional)
- **Pricing**: Simple, transparent pricing tiers
- **Testimonials**: User quotes with profile photos
- **Final CTA**: Simplified signup form or button

### 5.2 Authentication Pages

#### 5.2.1 Login Layout

```
┌─────────────────────────────────────────────────┐
│                    HEADER                        │
├─────────────────────────────────────────────────┤
│                                                 │
│                    LOGO                         │
│                                                 │
│       ┌─────────────────────────────────┐       │
│       │                                 │       │
│       │        SOCIAL LOGIN BUTTONS     │       │
│       │                                 │       │
│       ├─────────────────────────────────┤       │
│       │              OR                 │       │
│       ├─────────────────────────────────┤       │
│       │                                 │       │
│       │        EMAIL/PASSWORD FORM      │       │
│       │                                 │       │
│       └─────────────────────────────────┘       │
│                                                 │
│             FORGOT PASSWORD LINK                │
│                                                 │
│             SIGN UP LINK                        │
│                                                 │
├─────────────────────────────────────────────────┤
│                    FOOTER                        │
└─────────────────────────────────────────────────┘
```

#### 5.2.2 Key Elements

- Prominent social login buttons (Google, Apple)
- Clear visual separation for email/password option
- Error handling with specific feedback
- Remember me option
- Password recovery flow
- Link to signup for new users

### 5.3 User Dashboard

#### 5.3.1 Dashboard Layout

```
┌─────────────────────────────────────────────────┐
│      HEADER WITH ACCOUNT INFO & CREDITS         │
├─────────────────────────────────────────────────┤
│                                                 │
│ ┌───────────┐                                   │
│ │           │                                   │
│ │ SIDEBAR   │   ┌─────────────────────────────┐ │
│ │ NAVIGATION│   │                             │ │
│ │           │   │    PROJECTS OVERVIEW        │ │
│ │           │   │                             │ │
│ │           │   └─────────────────────────────┘ │
│ │           │                                   │
│ │           │   ┌─────────────────────────────┐ │
│ │           │   │                             │ │
│ │           │   │    RECENT ACTIVITY          │ │
│ │           │   │                             │ │
│ │           │   └─────────────────────────────┘ │
│ │           │                                   │
│ │           │   ┌─────────────────────────────┐ │
│ │           │   │                             │ │
│ │           │   │    QUICK ACTIONS            │ │
│ │           │   │                             │ │
│ └───────────┘   └─────────────────────────────┘ │
│                                                 │
├─────────────────────────────────────────────────┤
│                    FOOTER                        │
└─────────────────────────────────────────────────┘
```

#### 5.3.2 Key Elements

- Credit balance with purchase option
- Project cards with thumbnails and status
- New project button
- Activity feed showing recent actions
- Quick action shortcuts (new upload, continue project)

### 5.4 Upload Interface

#### 5.4.1 Upload Layout

```
┌─────────────────────────────────────────────────┐
│      HEADER WITH ACCOUNT INFO & CREDITS         │
├─────────────────────────────────────────────────┤
│                                                 │
│ ┌───────────┐   ┌─────────────────────────────┐ │
│ │           │   │                             │ │
│ │ PROJECT   │   │        STEP INDICATOR       │ │
│ │ SIDEBAR   │   │                             │ │
│ │           │   ├─────────────────────────────┤ │
│ │           │   │                             │ │
│ │           │   │                             │ │
│ │           │   │                             │ │
│ │           │   │    UPLOAD AREA              │ │
│ │           │   │    (REFERENCE PHOTOS)       │ │
│ │           │   │                             │ │
│ │           │   │                             │ │
│ │           │   │                             │ │
│ │           │   ├─────────────────────────────┤ │
│ │           │   │                             │ │
│ │           │   │    UPLOAD AREA              │ │
│ │           │   │    (TARGET PHOTOS)          │ │
│ │           │   │                             │ │
│ │           │   │                             │ │
│ │           │   │                             │ │
│ └───────────┘   └─────────────────────────────┘ │
│                                                 │
│          BACK BUTTON     NEXT BUTTON            │
│                                                 │
├─────────────────────────────────────────────────┤
│                    FOOTER                        │
└─────────────────────────────────────────────────┘
```

#### 5.4.2 Key Elements

- Clearly separated upload areas for reference and target photos
- Drag-and-drop functionality with fallback button
- File type restrictions and size limits clearly indicated
- Upload progress indicators
- Thumbnail previews of uploaded files
- Basic organization options (reordering, removing)

### 5.5 Style Analysis & Confirmation

#### 5.5.1 Analysis Layout

```
┌─────────────────────────────────────────────────┐
│      HEADER WITH ACCOUNT INFO & CREDITS         │
├─────────────────────────────────────────────────┤
│                                                 │
│ ┌───────────┐   ┌─────────────────────────────┐ │
│ │           │   │                             │ │
│ │ PROJECT   │   │        STEP INDICATOR       │ │
│ │ SIDEBAR   │   │                             │ │
│ │           │   ├─────────────────────────────┤ │
│ │           │   │                             │ │
│ │           │   │    REFERENCE PHOTOS         │ │
│ │           │   │    THUMBNAILS               │ │
│ │           │   │                             │ │
│ │           │   ├─────────────────────────────┤ │
│ │           │   │                             │ │
│ │           │   │    STYLE ANALYSIS DISPLAY   │ │
│ │           │   │    (Visual + Text)          │ │
│ │           │   │                             │ │
│ │           │   ├─────────────────────────────┤ │
│ │           │   │                             │ │
│ │           │   │    CHAT INTERFACE           │ │
│ │           │   │    (Optional Refinement)    │ │
│ │           │   │                             │ │
│ └───────────┘   └─────────────────────────────┘ │
│                                                 │
│      BACK BUTTON     CONFIRM STYLE BUTTON       │
│                                                 │
├─────────────────────────────────────────────────┤
│                    FOOTER                        │
└─────────────────────────────────────────────────┘
```

#### 5.5.2 Key Elements

- Reference photo thumbnails with ability to view larger
- Visual style analysis (color palette, tone curves, etc.)
- Text description of identified style
- Chat interface for refinement questions
- Suggestion chips for common refinements
- Clear confirmation button

### 5.6 Processing & Results

#### 5.6.1 Results Layout

```
┌─────────────────────────────────────────────────┐
│      HEADER WITH ACCOUNT INFO & CREDITS         │
├─────────────────────────────────────────────────┤
│                                                 │
│ ┌───────────┐   ┌─────────────────────────────┐ │
│ │           │   │                             │ │
│ │ PROJECT   │   │      PROJECT TITLE          │ │
│ │ SIDEBAR   │   │                             │ │
│ │           │   ├─────────────────────────────┤ │
│ │           │   │                             │ │
│ │           │   │   RESULTS GALLERY           │ │
│ │           │   │   (Before/After Comparison) │ │
│ │           │   │                             │ │
│ │           │   │                             │ │
│ │           │   │                             │ │
│ │           │   │                             │ │
│ │           │   │                             │ │
│ │           │   ├─────────────────────────────┤ │
│ │           │   │                             │ │
│ │           │   │   DOWNLOAD & SHARE OPTIONS  │ │
│ │           │   │                             │ │
│ │           │   │                             │ │
│ └───────────┘   └─────────────────────────────┘ │
│                                                 │
│    NEW PROJECT       EDIT AGAIN     SHARE       │
│                                                 │
├─────────────────────────────────────────────────┤
│                    FOOTER                        │
└─────────────────────────────────────────────────┘
```

#### 5.6.2 Key Elements

- Before/after comparison for each photo
- Slider or toggle to compare results
- Applied parameters summary
- Download options (individual or batch)
- Sharing options
- Credit usage summary
- Option to start new project or edit again

### 5.7 Credit Purchase

#### 5.7.1 Purchase Layout

```
┌─────────────────────────────────────────────────┐
│      HEADER WITH ACCOUNT INFO & CREDITS         │
├─────────────────────────────────────────────────┤
│                                                 │
│               CURRENT CREDIT BALANCE            │
│                                                 │
│ ┌─────────────┐  ┌─────────────┐ ┌───────────┐  │
│ │             │  │             │ │           │  │
│ │  BASIC      │  │  STANDARD   │ │  PRO      │  │
│ │  PACKAGE    │  │  PACKAGE    │ │  PACKAGE  │  │
│ │             │  │             │ │           │  │
│ │  • X Credits│  │  • X Credits│ │• X Credits│  │
│ │  • $XX.XX   │  │  • $XX.XX   │ │• $XX.XX   │  │
│ │             │  │             │ │           │  │
│ │  BUY BUTTON │  │  BUY BUTTON │ │ BUY BUTTON│  │
│ │             │  │             │ │           │  │
│ └─────────────┘  └─────────────┘ └───────────┘  │
│                                                 │
│ ┌─────────────────────────────────────────────┐ │
│ │                                             │ │
│ │           SUBSCRIPTION OPTIONS              │ │
│ │           (For Professional Users)          │ │
│ │                                             │ │
│ └─────────────────────────────────────────────┘ │
│                                                 │
│                    FAQ                          │
│                                                 │
├─────────────────────────────────────────────────┤
│                    FOOTER                        │
└─────────────────────────────────────────────────┘
```

#### 5.7.2 Key Elements

- Clear pricing tiers with comparison
- Credit packages with quantity and pricing
- Subscription options for regular users
- Secure checkout process indicator
- Payment method selection
- Order summary
- FAQ section addressing common questions

## 6. Interaction Patterns

### 6.1 Upload Flow

1. User clicks "New Project" or "Upload Photos"
2. User names project (optional)
3. User uploads reference photos (drag-drop or file picker)
4. User uploads target photos (drag-drop or file picker)
5. System validates uploads
6. User proceeds to style analysis

### 6.2 Style Analysis Flow

1. System analyzes reference photos
2. System presents style analysis visually and textually
3. User reviews analysis
4. User can refine understanding via chat interface (optional)
5. User confirms style or makes adjustments
6. System proceeds to processing

### 6.3 Processing & Review Flow

1. System shows processing status with progress indicators
2. Upon completion, system presents results
3. User can compare before/after with slider
4. User can download or share results
5. User can start new project or edit again

### 6.4 Credit Purchase Flow

1. User clicks "Buy Credits" or is prompted when out of credits
2. User selects credit package or subscription
3. User completes checkout via Stripe
4. System confirms purchase and updates credit balance
5. User returns to previous activity

## 7. Accessibility Considerations

### 7.1 WCAG Compliance

- Target WCAG 2.1 AA compliance
- Proper semantic HTML structure
- Keyboard navigation support
- Focus management for modals and dialogs

### 7.2 Color & Contrast

- Minimum 4.5:1 contrast ratio for text
- Non-color dependent indicators
- Sufficient contrast for UI elements
- Tested with color blindness simulators

### 7.3 Screen Readers

- Proper ARIA attributes
- Alternative text for images
- Meaningful link and button text
- Proper heading structure

### 7.4 Responsive Considerations

- Touch targets minimum 44x44px
- Zoom support without breaking layout
- Responsive text scaling

## 8. Animation & Microinteractions

### 8.1 Purpose-Driven Animation

- Upload progress indicators
- Processing state transitions
- Before/after comparison transitions
- Feedback animations for actions

### 8.2 Performance Considerations

- GPU-accelerated animations
- Respecting reduced motion preferences
- Optimized for lower-powered devices

## 9. Implementation Notes

### 9.1 Component Library

- Build on React component library (e.g., MUI, Chakra UI)
- Custom styled components for branded elements
- Storybook for component documentation

### 9.2 Responsive Implementation

- Mobile-first approach
- Flexbox and CSS Grid for layouts
- Image optimization for different viewport sizes

### 9.3 Performance Optimization

- Lazy loading of images
- Code splitting
- Prefetching of likely next pages
- Image optimization

## 10. Future UI Enhancements

### 10.1 Advanced Editing Interface

- Manual adjustment capabilities after automatic processing
- Fine-tuning of specific parameters
- History/undo functionality

### 10.2 Professional Tools

- Batch renaming
- Metadata editing
- Custom presets management
- Client delivery interface

### 10.3 Community Features

- Style sharing marketplace
- User galleries (with permission)
- Inspiration feed

## 11. Appendix

### 11.1 User Testing Plan

- Initial prototype testing with 5-8 users from each target segment
- A/B testing for critical conversion points
- Ongoing feedback collection via in-app mechanisms

### 11.2 UI Component Reference

Detailed specifications for each UI component will be provided separately through a design system documentation.

---

*Document Version: 1.0*  
*Last Updated: March 29, 2025*  
*Author: Claude*
