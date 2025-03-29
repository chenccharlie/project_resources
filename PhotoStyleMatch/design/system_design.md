# PhotoStyleMatch - System Design Document

## 1. Architecture Overview

PhotoStyleMatch follows a microservices architecture to allow for scalability, maintainability, and the ability to upgrade components independently. The system is divided into several key services, each responsible for a specific aspect of functionality.

### 1.1 High-Level Architecture Diagram

```
┌───────────────────┐     ┌───────────────────┐     ┌───────────────────┐
│                   │     │                   │     │                   │
│    Client         │────▶│    API Gateway    │────▶│  Auth Service     │
│    Applications   │     │                   │     │                   │
│                   │     └───────────────────┘     └───────────────────┘
└───────────────────┘                │
                                     │
                                     ▼
┌───────────────────┐     ┌───────────────────┐     ┌───────────────────┐
│                   │     │                   │     │                   │
│  Adobe Lightroom  │◀───▶│   Core Services   │◀───▶│   LLM Service     │
│      API          │     │                   │     │                   │
│                   │     └───────────────────┘     └───────────────────┘
└───────────────────┘                │
                                     │
                                     ▼
┌───────────────────┐     ┌───────────────────┐     ┌───────────────────┐
│                   │     │                   │     │                   │
│  Storage Service  │◀───▶│   Job Queue       │◀───▶│   Payment Service │
│                   │     │                   │     │                   │
└───────────────────┘     └───────────────────┘     └───────────────────┘
```

### 1.2 Key Components

1. **Client Applications**
   - Web application (React/Next.js)
   - Future mobile applications

2. **API Gateway**
   - Routes requests to appropriate services
   - Handles authentication validation
   - Rate limiting and request throttling

3. **Auth Service**
   - Manages user authentication
   - Handles social login (Google, Apple) 
   - Email/password authentication
   - Token issuance and validation

4. **Core Services**
   - Project management
   - Photo upload and validation
   - Style analysis orchestration
   - Edit processing coordination

5. **LLM Service**
   - Abstraction layer for different LLM providers
   - Style analysis logic
   - Parameter determination algorithms
   - Chat interface backend

6. **Adobe Lightroom Integration**
   - Authentication with Adobe APIs
   - Photo upload to Lightroom
   - Parameter application
   - Edited photo retrieval

7. **Storage Service**
   - Primary: Adobe Lightroom storage
   - Backup: Google Cloud Storage
   - Manages temporary storage during processing

8. **Job Queue**
   - Manages asynchronous processing tasks
   - Handles retries and failures
   - Distributes load across worker instances

9. **Payment Service**
   - Credit management
   - Stripe integration
   - Subscription handling

## 2. Detailed Component Design

### 2.1 Client Application Architecture

The client application follows a modern React architecture with Next.js for server-side rendering and routing:

```
┌─────────────────────────────────────────────┐
│                                             │
│                Next.js App                  │
│                                             │
├─────────────┬─────────────┬─────────────────┤
│             │             │                 │
│  Pages      │  Components │  State Mgmt     │
│             │             │  (Redux)        │
│             │             │                 │
└─────────────┴─────────────┴─────────────────┘
        │             │             │
        ▼             ▼             ▼
┌─────────────┬─────────────┬─────────────────┐
│             │             │                 │
│  API        │  Auth       │  Storage        │
│  Services   │  Services   │  Services       │
│             │             │                 │
└─────────────┴─────────────┴─────────────────┘
```

Key technologies:
- React for UI components
- Next.js for routing and SSR
- Redux for state management
- Tailwind CSS for styling
- Axios for API communication
- Socket.IO for real-time updates

### 2.2 Backend Service Architecture

Each backend service is containerized with Docker and deployed on Kubernetes:

```
┌────────────────────────────────────────────────────────┐
│                   Kubernetes Cluster                   │
│                                                        │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │             │  │             │  │             │     │
│  │ API Gateway │  │ Auth Service│  │ Core Service│     │
│  │  Pods       │  │  Pods       │  │  Pods       │     │
│  │             │  │             │  │             │     │
│  └─────────────┘  └─────────────┘  └─────────────┘     │
│                                                        │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │             │  │             │  │             │     │
│  │ LLM Service │  │ Job Workers │  │ Payment     │     │
│  │  Pods       │  │  Pods       │  │ Service Pods│     │
│  │             │  │             │  │             │     │
│  └─────────────┘  └─────────────┘  └─────────────┘     │
│                                                        │
└────────────────────────────────────────────────────────┘
```

Each service:
- Follows a REST API pattern
- Has its own database access layer
- Communicates with other services via API calls or message queue
- Is independently scalable
- Has health monitoring and logging

### 2.3 Data Flow

The following sequence illustrates the data flow for a typical photo editing process:

1. User uploads reference photo(s) and target photo(s)
2. Core service validates uploads and stores them temporarily
3. Core service creates processing job and adds to queue
4. LLM service analyzes reference photos for style characteristics
5. LLM service generates human-readable style description
6. User confirms or refines style using chat interface
7. LLM service analyzes target photos and determines edit parameters
8. Lightroom integration service uploads photos to Lightroom
9. Lightroom integration service applies determined parameters
10. Lightroom integration service retrieves edited photos
11. Storage service stores edited photos
12. Core service updates project status
13. User is notified of completion
14. User views, downloads, or shares results

## 3. Database Design

### 3.1 Database Architecture

PhotoStyleMatch uses a polyglot persistence approach:

1. **PostgreSQL** - Primary relational database for:
   - User accounts and profiles
   - Project metadata
   - Photo metadata
   - Credit transactions
   - Relationships between entities

2. **Redis** - In-memory data store for:
   - Session management
   - Caching
   - Real-time notifications
   - Job queue management

3. **Google Cloud Storage/Adobe Lightroom** - Binary storage for:
   - Original photos
   - Edited photos
   - Temporary processing files

### 3.2 Entity-Relationship Diagram

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   User      │     │   Project   │     │    Photo    │
├─────────────┤     ├─────────────┤     ├─────────────┤
│ id          │1   *│ id          │1   *│ id          │
│ name        ├────▶│ user_id     ├────▶│ project_id  │
│ email       │     │ name        │     │ filename    │
│ auth_provider│     │ description │     │ storage_path│
│ credits     │     │ created_at  │     │ type        │
│ ...         │     │ ...         │     │ ...         │
└─────────────┘     └─────────────┘     └─────────────┘
      │1                   │1                 │*
      │                    │                  │
      ▼*                   ▼*                 ▼1
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│ CreditTrans │     │   Style     │     │    Edit     │
├─────────────┤     ├─────────────┤     ├─────────────┤
│ id          │     │ id          │     │ id          │
│ user_id     │     │ project_id  │     │ photo_id    │
│ amount      │     │ description │     │ style_id    │
│ type        │     │ llm_analysis│     │ status      │
│ payment_id  │     │ parameters  │     │ params_used │
│ ...         │     │ ...         │     │ ...         │
└─────────────┘     └─────────────┘     └─────────────┘
```

## 4. Integration Points

### 4.1 Adobe Lightroom API Integration

#### 4.1.1 Authentication Flow
1. Application registers with Adobe Developer Console
2. OAuth 2.0 flow for authentication
3. Token storage and refresh mechanisms

#### 4.1.2 Key Endpoints Used
- `/catalog` - Manage photo catalogs
- `/assets` - Upload and manage photos
- `/edit` - Apply editing parameters
- `/rendition` - Retrieve edited photos

#### 4.1.3 Rate Limiting Considerations
- Implement exponential backoff strategy
- Queue jobs to manage API quota
- Monitor usage patterns

### 4.2 LLM Provider Integration

#### 4.2.1 Abstraction Layer
LLM Service uses a provider abstraction pattern:

```
┌─────────────────────────────────────────┐
│         LLM Provider Interface          │
└─────────────────────────────────────────┘
                    │
        ┌───────────┼───────────┐
        │           │           │
        ▼           ▼           ▼
┌─────────────┐┌─────────────┐┌─────────────┐
│ OpenAI      ││ Claude      ││ Other       │
│ Provider    ││ Provider    ││ Provider    │
└─────────────┘└─────────────┘└─────────────┘
```

This allows for:
- Easy switching between providers
- A/B testing of providers
- Fallback mechanisms
- Parallel processing for comparison

#### 4.2.2 Key LLM Functions
- Style analysis from reference images
- Parameter determination for target images
- Natural language chat interface
- Style description generation

### 4.3 Payment Integration (Stripe)

#### 4.3.1 Integration Points
- Checkout API for credit purchases
- Subscription API for professional plans
- Customer portal for subscription management
- Webhook handlers for event processing

#### 4.3.2 Security Considerations
- Server-side confirmation of transactions
- Webhook signature verification
- PCI compliance through Stripe Elements

### 4.4 Cloud Storage Integration

#### 4.4.1 Google Cloud Storage
- Temporary storage during processing
- Backup storage when needed
- Signed URLs for secure access

## 5. Security Design

### 5.1 Authentication & Authorization

- JSON Web Tokens (JWT) for authentication
- Role-based access control
- OAuth 2.0 for social authentication
- Secure password hashing (bcrypt)
- CSRF protection

### 5.2 Data Protection

- Encryption in transit (TLS)
- Secure storage of sensitive credentials
- Principle of least privilege
- Input validation and sanitization
- Output encoding

### 5.3 API Security

- Rate limiting
- API keys and secrets management
- Request validation
- Proper error handling without leaking details

### 5.4 Compliance Considerations

- GDPR compliance for European users
- CCPA compliance for California residents
- Data minimization principles
- User consent management
- Data export and deletion capabilities

## 6. Scalability & Performance

### 6.1 Horizontal Scaling

- Stateless services for easy replication
- Kubernetes for container orchestration
- Auto-scaling based on load metrics

### 6.2 Performance Optimizations

- Caching strategy (Redis)
- Background processing for intensive tasks
- Efficient database queries with proper indexing
- Image optimization before processing
- CDN for static assets

### 6.3 Load Handling

- Queue-based architecture for processing
- Rate limiting for external APIs
- Graceful degradation under high load
- Circuit breakers for failing services

## 7. Monitoring & Logging

### 7.1 Monitoring Infrastructure

- Prometheus for metrics collection
- Grafana for visualization
- Alerting based on thresholds
- Service health checks

### 7.2 Logging Strategy

- Structured logging (JSON format)
- Centralized log collection
- Log levels for different environments
- Correlation IDs for request tracing

### 7.3 Key Metrics

- API response times
- Processing queue length
- Error rates
- Authentication success/failure
- Credit usage
- Storage utilization
- Third-party API response times

## 8. Deployment & DevOps

### 8.1 CI/CD Pipeline

- GitHub Actions for CI/CD
- Automated testing
- Containerization with Docker
- Staging environment for pre-production validation

### 8.2 Environment Strategy

- Development
- Staging
- Production
- Feature flags for controlled rollout

### 8.3 Backup & Recovery

- Database backups
- Infrastructure as Code (Terraform)
- Disaster recovery plan
- Rollback procedures

## 9. Future Considerations

### 9.1 Mobile Application

- React Native for cross-platform support
- Shared authentication system
- Optimized for mobile uploads

### 9.2 Advanced Features

- Style marketplace
- AI-generated style recommendations
- Batch processing improvements
- Professional photographer dashboard

### 9.3 Integration Opportunities

- Social media platform integrations
- Photography workflow tools
- Print service providers

## 10. Appendix

### 10.1 Technology Stack Summary

- **Frontend:** React, Next.js, Redux, Tailwind CSS
- **Backend:** Node.js, Express, Python
- **Databases:** PostgreSQL, Redis
- **Infrastructure:** Docker, Kubernetes, Google Cloud Platform
- **Third-party Services:** Adobe Lightroom API, LLM Providers, Stripe
- **Storage:** Google Cloud Storage, Adobe Lightroom

### 10.2 API Documentation References

- Detailed API documentation will be available via Swagger/OpenAPI
- Authentication flow documentation
- WebSocket event documentation

### 10.3 Infrastructure Diagram

Detailed infrastructure diagram to be developed during implementation phase.

---

*Document Version: 1.0*  
*Last Updated: March 29, 2025*  
*Author: Claude*
