# PhotoStyleMatch - Product Requirements Document

## 1. Introduction

### 1.1 Purpose
PhotoStyleMatch is a web application that allows users to automatically apply photo styling from reference images to their own photos using Adobe Lightroom APIs and LLM analysis. This document outlines the detailed requirements and specifications for the development and implementation of the application.

### 1.2 Target Audience
The application targets two primary user groups:
1. **Casual Users**: Individuals who want to match the style of photos they've seen online to their own similar photos.
2. **Professional Photographers**: Independent photographers who want to consistently apply their signature styles to batches of photos efficiently.

### 1.3 Product Vision
To provide an intuitive, efficient tool that democratizes professional-quality photo styling through AI-assisted parameter determination and automated Lightroom adjustments.

## 2. User Journeys

### 2.1 Casual User Journey
1. Discovers the product through marketing or search
2. Signs up using Google or Apple account
3. Uploads a reference photo with desired style
4. Uploads their own photo(s) to be edited
5. Reviews LLM's style analysis and confirms or adjusts
6. Receives edited photos with style applied
7. Downloads or shares results
8. Potentially purchases credits for more edits

### 2.2 Professional Photographer Journey
1. Signs up for the service using preferred method
2. Uploads a batch of reference photos showcasing their signature style
3. Uploads client photos to be edited
4. Reviews and confirms style analysis
5. Receives batch-processed photos with consistent styling
6. Downloads photos or shares directly with clients
7. Purchases additional credits as needed

## 3. Functional Requirements

### 3.1 Authentication & User Management
- **FR1.1:** Implement social login with Google and Apple (primary methods)
- **FR1.2:** Provide email/password authentication (secondary method)
- **FR1.3:** Implement user profile management
- **FR1.4:** Track usage and credits per user
- **FR1.5:** Support password reset and account recovery

### 3.2 Photo Upload & Management
- **FR2.1:** Allow uploading multiple reference photos (up to 5)
- **FR2.2:** Allow uploading multiple target photos (up to 20 per batch)
- **FR2.3:** Support common image formats (JPEG, PNG, HEIC, RAW)
- **FR2.4:** Validate photos for size, format, and content
- **FR2.5:** Store photos in Lightroom catalog or Google Cloud Storage
- **FR2.6:** Implement photo organization by project/session

### 3.3 Style Analysis & LLM Integration
- **FR3.1:** Analyze reference photos to extract style characteristics
- **FR3.2:** Generate human-readable style description
- **FR3.3:** Present style analysis to user for confirmation
- **FR3.4:** Allow chat-based refinement of style understanding
- **FR3.5:** Support multiple LLM providers via abstracted interface
- **FR3.6:** Implement LLM provider selection and configuration in admin panel

### 3.4 Lightroom Integration
- **FR4.1:** Authenticate with Adobe Lightroom API
- **FR4.2:** Upload photos to Lightroom catalog
- **FR4.3:** Apply determined edit parameters to photos
- **FR4.4:** Support for all available Lightroom adjustment parameters
- **FR4.5:** Retrieve edited photos
- **FR4.6:** Handle API rate limits and quotas

### 3.5 Edit Parameter Determination
- **FR5.1:** Analyze target photos to determine base characteristics
- **FR5.2:** Calculate specific Lightroom parameter adjustments needed
- **FR5.3:** Apply consistent style across diverse photos
- **FR5.4:** Save and reuse style presets for efficiency

### 3.6 Results & Delivery
- **FR6.1:** Present before/after comparison of photos
- **FR6.2:** Allow downloading of edited photos individually or as zip
- **FR6.3:** Provide sharing options (link, email, social)
- **FR6.4:** Store edit history for user reference

### 3.7 Payment & Credits
- **FR7.1:** Provide 3 free edits for new users
- **FR7.2:** Implement credit-based system for additional edits
- **FR7.3:** Integrate Stripe for payment processing
- **FR7.4:** Offer various credit packages at different price points
- **FR7.5:** Implement subscription option for professional users

## 4. Non-Functional Requirements

### 4.1 Performance
- **NFR1.1:** Process individual photo style analysis in under 30 seconds
- **NFR1.2:** Complete batch processing (up to 20 photos) in under 10 minutes
- **NFR1.3:** Handle up to 1000 concurrent users
- **NFR1.4:** Support file uploads up to 50MB per photo

### 4.2 Security
- **NFR2.1:** Implement OAuth 2.0 for social authentication
- **NFR2.2:** Secure password storage with bcrypt or equivalent
- **NFR2.3:** Encrypt all data in transit with TLS
- **NFR2.4:** Implement proper access controls to user data
- **NFR2.5:** Comply with GDPR and CCPA data protection requirements

### 4.3 Reliability
- **NFR3.1:** Achieve 99.5% uptime for core services
- **NFR3.2:** Implement retry mechanisms for API failures
- **NFR3.3:** Provide graceful degradation when services are unavailable
- **NFR3.4:** Backup user data daily

### 4.4 Scalability
- **NFR4.1:** Design for horizontal scaling of web and processing services
- **NFR4.2:** Implement queue-based processing for photo edits
- **NFR4.3:** Use cloud storage solutions for elastic storage capacity

### 4.5 Usability
- **NFR5.1:** Design responsive interface for desktop and mobile
- **NFR5.2:** Create intuitive upload and edit workflow
- **NFR5.3:** Implement progress indicators for processing steps
- **NFR5.4:** Design consistent UI with clear visual hierarchy
- **NFR5.5:** Support all major browsers (Chrome, Safari, Firefox, Edge)

## 5. Technical Stack

### 5.1 Frontend
- React.js for UI components
- Redux for state management
- Tailwind CSS for styling
- Next.js for server-side rendering and routing

### 5.2 Backend
- Node.js with Express for API
- Python for LLM integration and image analysis
- WebSockets for real-time processing updates

### 5.3 Database
- PostgreSQL for user data and metadata
- Redis for caching and session management

### 5.4 Infrastructure
- Docker for containerization
- Kubernetes for orchestration
- Google Cloud Platform for hosting
- Google Cloud Storage for backup storage
- Adobe Lightroom API for photo processing

### 5.5 Third-Party Services
- Adobe Lightroom API
- LLM providers (with abstraction layer for flexibility)
- Stripe for payment processing
- Google/Apple authentication providers

## 6. User Interface

### 6.1 Landing Page
- Product showcase with examples
- Benefits and use cases
- Call-to-action for signup/login

### 6.2 Authentication Pages
- Streamlined login/signup with social options prominent
- Email/password option available but secondary

### 6.3 Dashboard
- Overview of projects/sessions
- Credit balance and usage statistics
- Quick-start actions

### 6.4 Upload Interface
- Clear distinction between reference and target photos
- Drag-and-drop functionality
- Progress indicators

### 6.5 Style Analysis & Confirmation
- Visual representation of detected style
- Text description of style characteristics
- Chat interface for refinement

### 6.6 Results Gallery
- Before/after comparison view
- Download and sharing options
- Edit history and metadata

### 6.7 Credit Purchase
- Clear pricing tiers
- Secure checkout process
- Subscription options for professionals

## 7. Data Models

### 7.1 User
- ID, name, email, auth_provider, created_at, updated_at
- credit_balance, free_edits_used
- subscription_status, subscription_expiry

### 7.2 Project
- ID, user_id, name, description, created_at, updated_at
- status (in_progress, completed, failed)

### 7.3 Photo
- ID, project_id, original_filename, storage_path, type (reference, target)
- format, size, dimensions, upload_date
- lightroom_catalog_id, lightroom_asset_id

### 7.4 Style
- ID, project_id, name, description
- LLM_analysis_text, confirmed_by_user
- parameter_adjustments (JSON of Lightroom parameters)

### 7.5 Edit
- ID, photo_id, style_id, status
- created_at, completed_at
- original_photo_url, edited_photo_url
- parameters_applied (JSON)

### 7.6 Credit Transaction
- ID, user_id, amount, transaction_type
- payment_id, created_at
- description

## 8. API Endpoints

### 8.1 Authentication
- POST /api/auth/login
- POST /api/auth/register
- POST /api/auth/social-login
- POST /api/auth/logout
- POST /api/auth/reset-password

### 8.2 Users
- GET /api/users/me
- PUT /api/users/me
- GET /api/users/credits
- POST /api/users/purchase-credits

### 8.3 Projects
- GET /api/projects
- POST /api/projects
- GET /api/projects/:id
- PUT /api/projects/:id
- DELETE /api/projects/:id

### 8.4 Photos
- POST /api/projects/:id/photos
- GET /api/projects/:id/photos
- DELETE /api/photos/:id

### 8.5 Styles
- POST /api/projects/:id/styles
- GET /api/projects/:id/styles
- PUT /api/styles/:id
- DELETE /api/styles/:id

### 8.6 Edits
- POST /api/projects/:id/edits
- GET /api/projects/:id/edits
- GET /api/edits/:id
- GET /api/edits/:id/download

### 8.7 LLM Chat
- POST /api/projects/:id/chat
- GET /api/projects/:id/chat-history

## 9. Milestones & Delivery Plan

### 9.1 Phase 1: MVP (2 Months)
- Basic authentication (social and email)
- Photo upload (single reference, single target)
- Simple style analysis with fixed LLM
- Core Lightroom integration
- Basic results delivery
- Credit system foundation

### 9.2 Phase 2: Enhanced Features (2 Months)
- Multi-photo uploads
- Advanced style analysis
- Chat interface for style refinement
- Improved parameter determination
- Before/after comparison
- Complete payment integration

### 9.3 Phase 3: Professional Tools (2 Months)
- Batch processing
- Style presets and reuse
- Enhanced user management
- Performance optimizations
- API for integration

### 9.4 Phase 4: Scale & Polish (1 Month)
- UI/UX refinements
- Performance optimizations
- Analytics integration
- Advanced sharing options
- Marketing site enhancements

## 10. Success Metrics

### 10.1 User Engagement
- Sign-up conversion rate: 10%+
- Free trial to paid conversion: 5%+
- Return rate: 30%+ within 30 days

### 10.2 Technical Performance
- Style analysis accuracy (subjective user rating): 4.5/5
- Processing time within targets
- System uptime: 99.5%+

### 10.3 Business Metrics
- Customer acquisition cost < Lifetime value/3
- Monthly recurring revenue growth: 15%+
- Churn rate < 5% monthly

## 11. Risks & Mitigations

### 11.1 Technical Risks
- **Risk**: Adobe API limitations or changes
  - **Mitigation**: Implement abstraction layer and monitor API changes

- **Risk**: LLM accuracy for style determination
  - **Mitigation**: Continuous training, human verification option

- **Risk**: Performance bottlenecks with high volume
  - **Mitigation**: Queue-based architecture, horizontal scaling

### 11.2 Business Risks
- **Risk**: Low conversion to paid
  - **Mitigation**: A/B test pricing models, enhance value proposition

- **Risk**: Competitor entry
  - **Mitigation**: Focus on unique styling capabilities and professional tools

- **Risk**: High cost of processing
  - **Mitigation**: Optimize processing, batch operations, evaluate pricing

## 12. Open Questions & Decisions

1. Should we implement image recognition to categorize photos for better style matching?
2. What is the optimal pricing structure for different user segments?
3. Should we consider offering a white-label solution for photography businesses?
4. What level of customization should be provided post-automated editing?
5. Should we implement a public gallery of before/after examples (with permission)?

## 13. Approval
This PRD is pending approval.

---

*Document Version: 1.0*  
*Last Updated: March 29, 2025*  
*Author: Claude*
