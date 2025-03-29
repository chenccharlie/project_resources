# PhotoStyleMatch Executive Request

## Project Overview
PhotoStyleMatch is a web application that allows users to upload photos and have them automatically stylized to match reference photos using Adobe Lightroom APIs and LLM analysis. The application targets both casual users who want to match the style of photos they've seen, and professional photographers who want to consistently apply their signature styles to batches of photos.

## Core Requirements

### Functionality
- Upload reference photos (style examples) and target photos (to be edited)
- Utilize LLM to analyze photos and understand desired style/vibe
- Allow users to confirm style understanding through optional chat
- Automatically determine precise Lightroom edit parameters
- Integrate with Adobe Lightroom APIs for photo editing
- Present edited results to users

### User Experience
- Showcase product features on the website
- Require user authentication (prominent social login, less prominent email/password)
- Implement freemium model with 3 free edits and paid credits thereafter

### Integration
- Adobe Lightroom API for photo edits and storage
- LLM integration with ability to upgrade/change LLM providers
- Stripe for payment processing
- Google Cloud Storage as backup storage if Lightroom storage is insufficient

## User Authentication
- Primary: Social login with Google and Apple
- Secondary: Email/password (less prominent)

## Photo Storage
- Primary: Adobe Lightroom account
- Backup: Google Cloud Storage

## Confirmed Adjustments
Lightroom adjustments to include (based on API capabilities):
- Exposure
- Contrast
- Highlights
- Shadows
- Whites
- Blacks
- Clarity
- Vibrance
- Saturation
- Temperature
- Tint
- And other parameters available via the Lightroom API

## Approved By
[Pending confirmation]