I'll explore the codebase to understand the session-replay service flows. Let me start by examining the directory structure and key files related to session replay.

Ran tool
Now let me examine the main session replay controllers to understand the flows:

Read file: app/controllers/api/web/sessions_replay_controller.rb
Read file: app/controllers/api/internal/sessions_replay_controller.rb
Now let me examine the session replay fetch service and permissions:

Read file: lib/session_replay/fetch.rb
Read file: lib/session_replay/session_replay_permissions.rb
Now let me examine the ClickHouse handlers for session replay:

Ran tool
Read file: app/models/concerns/search/click_house_handler/session_replay/base.rb
Read file: app/models/concerns/search/click_house_handler/session_replay/session_details.rb
Read file: app/models/concerns/search/click_house_handler/session_replay/pagination.rb
Now let me examine the decorators and formatters:

Read file: app/controllers/decorators/sessions_replay_controller_decorator.rb
Now let me examine the rate limiting and background jobs:

Ran tool
Ran tool
Ran tool
Let me check the models related to session replay:

Ran tool
Read file: app/models/session.rb
Now let me examine the AI issues models:

Ran tool
Read file: app/models/ui_bug.rb
Read file: app/models/broken_functionality.rb
Now let me check the routes to understand the API endpoints:

Ran tool
Read file: config/routes.rb
Now let me examine the session filters and permissions:

Read file: app/controllers/concerns/api/web/session_replay/session_filters.rb
Based on my exploration of the codebase, I can now provide a comprehensive analysis of the session-replay service flows. Let me create the documentation with Mermaid flowcharts.

## Session Replay Service Flows

Based on my analysis of the Ruby on Rails application codebase, here are the main flows for the session-replay service:

### 1. Session Replay List Flow (Index/Pagination)

**Summary**: This flow handles retrieving and paginating through session replay data. It's triggered when users request a list of sessions with optional filtering and pagination.

**Flow**:
```mermaid
flowchart TD
    A[Client Request] --> B[Web SessionsReplayController#index]
    B --> C[Rate Limit Check]
    C --> D[Authentication & Permissions]
    D --> E[Validate Parameters]
    E --> F[Build Session Filters]
    F --> G[ClickHouse Pagination Handler]
    G --> H[Fetch Sessions Count]
    H --> I[Fetch Sessions Data]
    I --> J[Mark AI Issues Sessions]
    J --> K[Decorate Response]
    K --> L[Return JSON Response]
    
    subgraph "External Services"
        M[ClickHouse Database]
        N[Redis Rate Limiting]
    end
    
    G --> M
    C --> N
```

### 2. Session Replay Details Flow (Show)

**Summary**: This flow retrieves detailed information about a specific session, including crashes, bugs, APM metrics, and AI-generated issues. It's triggered when users request details for a specific session ID.

**Flow**:
```mermaid
flowchart TD
    A[Client Request] --> B[Web SessionsReplayController#show]
    B --> C[Rate Limit Check]
    C --> D[Authentication & Permissions]
    D --> E[Validate Session ID]
    E --> F[Fetch Session Details from ClickHouse]
    F --> G{Session Exists?}
    G -->|No| H[Return 404]
    G -->|Yes| I[Fetch Session Bugs]
    I --> J[Fetch Session Crashes]
    J --> K[Fetch APM Metrics]
    K --> L[Fetch AI Issues]
    L --> M[Decorate Session Details]
    M --> N[Return JSON Response]
    
    subgraph "External Services"
        O[ClickHouse Database]
        P[Bugs Service]
        Q[Crashes Service]
        R[APM Service]
        S[AI Issues Database]
    end
    
    F --> O
    I --> P
    J --> Q
    K --> R
    L --> S
```

### 3. Session Replay Filters Flow

**Summary**: This flow provides available filter options for session replay data, including devices, app versions, platforms, and other metadata. It's triggered when the UI needs to populate filter dropdowns.

**Flow**:
```mermaid
flowchart TD
    A[Client Request] --> B[Web SessionsReplayController#filters]
    B --> C[Rate Limit Check]
    C --> D[Authentication & Permissions]
    D --> E[Fetch Filter Data from ClickHouse]
    E --> F[Process Device Names]
    F --> G[Map OS Names]
    G --> H[Decorate Filter Response]
    H --> I[Return JSON Response]
    
    subgraph "External Services"
        J[ClickHouse Database]
        K[Device Name Mapper]
        L[OS Name Mapper]
    end
    
    E --> J
    F --> K
    G --> L
```

### 4. AI Issues Rating Flow

**Summary**: This flow handles user feedback on AI-generated issues (UI bugs and broken functionality). It's triggered when users rate the accuracy of AI-detected issues.

**Flow**:
```mermaid
flowchart TD
    A[Client Request] --> B[Web SessionsReplayController#rate_ui_bug]
    A --> C[Web SessionsReplayController#rate_broken_functionality]
    B --> D[Rate Limit Check]
    C --> D
    D --> E[Authentication & Permissions]
    E --> F[Validate Rating Parameters]
    F --> G[Find AI Issue Record]
    G --> H[Update Rating]
    H --> I[Return Success Response]
    
    subgraph "Database"
        J[UiBug Model]
        K[BrokenFunctionality Model]
    end
    
    B --> J
    C --> K
```

### 5. Internal Session Replay Flow (Review Suspected Sessions)

**Summary**: This flow is used internally to identify sessions that might need review based on prompt end times and other criteria. It's triggered by internal services or background processes.

**Flow**:
```mermaid
flowchart TD
    A[Internal Request] --> B[Internal SessionsReplayController#review_suspected_sessions]
    B --> C[Prepare Application Details]
    C --> D[Build Prompt End Time Filters]
    D --> E[Apply App Version Filters]
    E --> F[Apply Platform Filters]
    F --> G[Query ClickHouse Materialized View]
    G --> H[Count Suspected Sessions]
    H --> I[Return Session Counts]
    
    subgraph "External Services"
        J[Core Service]
        K[ClickHouse Materialized View]
    end
    
    C --> J
    G --> K
```

### 6. Session Replay Data Fetching Flow

**Summary**: This flow handles fetching session replay data from external services (bugs, crashes, APM metrics). It's used as a supporting flow for the main session details flow.

**Flow**:
```mermaid
flowchart TD
    A[SessionReplay::Fetch] --> B[session_occurrences]
    A --> C[session_bugs]
    A --> D[session_apm_metrics]
    
    B --> E[Parse Session ID]
    C --> E
    D --> E
    E --> F[Build Request Parameters]
    F --> G[Make HTTP Request to External Service]
    G --> H[Parse Response]
    H --> I[Return Data]
    
    subgraph "External Services"
        J[Crashes Service]
        K[Bugs Service]
        L[APM Service]
    end
    
    B --> J
    C --> K
    D --> L
```

### Key Components and Technologies:

1. **Controllers**: Handle HTTP requests, authentication, rate limiting, and parameter validation
2. **ClickHouse**: Primary database for session data storage and querying
3. **Redis**: Used for rate limiting and caching
4. **External Services**: Bugs, Crashes, and APM services for additional data
5. **AI Models**: UiBug and BrokenFunctionality models for AI-generated issues
6. **Decorators**: Transform raw data into formatted responses
7. **Rate Limiters**: Prevent abuse with configurable thresholds
8. **S3**: Storage for session logs and attachments

The session replay service is designed with a microservices architecture, using ClickHouse for high-performance analytics queries and external services for specialized data. It includes comprehensive rate limiting, authentication, and permission checks to ensure secure access to session data.
