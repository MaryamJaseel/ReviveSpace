## 1. Application Overview

**Application Name**: ReviveSpace

**Description**: A civic-tech web platform that enables citizens to report abandoned or underutilized properties and helps local governments identify, verify, and repurpose unused properties for public benefit. The platform bridges the gap between community awareness and government action through collaborative reporting, AI-assisted verification, and community-driven decision-making.

**Tagline**: Every abandoned building is a missed opportunity. ReviveSpace helps communities identify, verify, and repurpose unused properties for public benefit.

## 2. Users and Usage Scenarios

**Target Users**:
- **Citizens**: Community members who identify and report abandoned properties
- **Admins**: District administration officials responsible for verification and property management

**Core Usage Scenarios**:
- Citizens discover abandoned buildings in their neighborhood and submit reports with photos and details
- Admins review submitted reports, verify property status, and manage the workflow from initial report to action recommendation
- Community members vote on potential uses for verified vacant properties
- Government officials use data insights to prioritize urban revitalization efforts

## 3. Page Structure and Functionality

### 3.1 Page Hierarchy

```
ReviveSpace Platform
├── Public Pages
│   ├── Home Page
│   ├── Interactive Map View
│   ├── Property Detail Page
│   ├── Login Page
│   └── Registration Page
├── Citizen Pages (Authenticated)
│   ├── Report Property Page
│   └── My Reports Page
└── Admin Pages (Authenticated)
    └── Admin Dashboard
```

### 3.2 Public Pages

#### 3.2.1 Home Page
- Display platform tagline and mission statement
- Show key statistics: total reports submitted, properties verified, actions taken
- Provide quick access to Interactive Map View
- Include call-to-action buttons for Report Property and Login

#### 3.2.2 Interactive Map View
- Display map showing all reported properties with color-coded pins based on status and severity
- Support filtering by: status, property type, date reported, condition
- Cluster markers for dense areas to improve map readability
- Allow users to click on pins to view basic property information
- Provide link to full Property Detail Page

#### 3.2.3 Property Detail Page
- Display comprehensive property information:
  - Photo gallery of uploaded images
  - Location on mini-map
  - Property type and condition
  - Years unused estimate
  - Safety concerns
  - Current status with timeline showing workflow progression
  - Impact Score (0-100)
- Show community voting results with vote counts per option
- Display comments section for community discussion
- Provide voting interface for logged-in citizens

#### 3.2.4 Login Page
- Email and password input fields
- Login button
- Link to Registration Page

#### 3.2.5 Registration Page
- Email and password input fields
- Role selection: Citizen or Admin
- Register button
- Link to Login Page

### 3.3 Citizen Pages

#### 3.3.1 Report Property Page
- Photo upload interface supporting multiple images
- Location selection using map with GPS or manual pin placement
- Property details form:
  - Property type: Residential or Commercial building (radio buttons)
  - Approximate years unused (number input)
  - Current condition: Poor, Fair, Good (dropdown)
  - Safety concerns: checkboxes for broken windows, structural damage, overgrown vegetation, etc.
  - Potential uses: text input for suggestions
- Anonymous mode toggle option
- Submit report button

#### 3.3.2 My Reports Page
- List all reports submitted by the logged-in citizen
- Display report summary: property address, submission date, current status
- Provide link to view full Property Detail Page for each report

### 3.4 Admin Pages

#### 3.4.1 Admin Dashboard
- **Statistics Overview Section**:
  - Total reports count
  - Verified properties count
  - Actions taken count
- **Heatmap Visualization**:
  - Display vacant properties distribution by district
- **Priority Rankings Section**:
  - List properties sorted by Impact Score
  - Show top priority properties requiring attention
- **Reports Management Section**:
  - Display all reports in table format with columns: property address, reporter, submission date, status, Impact Score
  - Provide status change functionality for each report
  - Support filtering and sorting
- **Verification Management Section**:
  - List reports pending verification
  - Allow admins to mark properties as verified or rejected
- **Alerts Section**:
  - Display notifications for dangerous buildings
  - Flag properties with illegal dumping or encroachment
  - Show alert badges

## 4. Business Rules and Logic

### 4.1 AI-Based Image Analysis
- When citizen uploads photos during property reporting, system analyzes images using AI/LLM
- AI estimates structural condition from photos
- AI detects signs of abandonment: broken windows, overgrown vegetation, damaged roofs, lack of occupancy indicators
- System generates abandonment confidence score based on AI analysis
- Confidence score influences initial property status and priority

### 4.2 Property Status Workflow
Properties progress through the following states:
1. **Reported**: Initial submission by citizen
2. **Under Verification**: Admin reviewing the report
3. **Verified Vacant**: Admin confirms property is abandoned
4. **Notice Sent to Owner**: Government sends notification to property owner
5. **Owner Response**: Owner provides feedback or action plan
6. **Action Recommended**: Final recommendation for property repurposing

Only Admins can change property status. Status changes are recorded with timestamp.

### 4.3 Impact Score Calculation
Each property receives an Impact Score (0-100) calculated based on:
- **Location importance**: Urban density of the area (higher density = higher score)
- **Building condition severity**: Poor condition = higher score
- **Community demand**: Number of votes received
- **Potential beneficiaries**: Estimated number of people who would benefit from repurposing

Impact Score updates automatically when relevant factors change.

### 4.4 Community Voting Rules
- Only logged-in citizens can vote
- Each citizen can vote once per property
- Voting options: Affordable housing, Public library, Community center, Co-working space, Playground, Health clinic, Startup incubator, Women's self-help center
- Vote counts are displayed publicly
- Voting is only available for properties with status Verified Vacant or later

### 4.5 Anonymous Reporting
- When citizen enables anonymous mode during reporting, their identity is hidden from public view
- Admins can still access reporter information for verification purposes
- Anonymous reports display as \"Anonymous Citizen\" on Property Detail Page

### 4.6 Alerts and Notifications
- System generates alerts when:
  - Building condition deteriorates to dangerous level
  - Illegal dumping is reported at a property
  - Encroachment is detected
- Alerts appear in Admin Dashboard with priority badges
- Alert severity levels: High (red), Medium (orange), Low (yellow)

## 5. Exception and Boundary Cases

| Scenario | Handling |
|----------|----------|
| User uploads non-image files | System rejects upload and displays error message |
| GPS location unavailable | User can manually place pin on map |
| Duplicate property report | System detects existing report at same location and prompts user to view existing report instead |
| Admin attempts to change status backward in workflow | System prevents backward status changes except from Owner Response to Verified Vacant |
| Citizen attempts to vote multiple times | System prevents duplicate votes and displays message |
| Property owner not found for notice | Admin can mark as \"Owner Unknown\" and proceed to Action Recommended |
| AI analysis fails | System allows manual submission without AI score, admin reviews manually |
| User submits report without required fields | System displays validation errors and prevents submission |

## 6. Acceptance Criteria

1. Citizen registers an account and logs in successfully
2. Citizen navigates to Report Property Page and uploads photos of an abandoned building
3. Citizen marks the property location on the map and fills in all required property details
4. Citizen submits the report and sees confirmation message
5. Admin logs into Admin Dashboard and views the new report in Reports Management Section
6. Admin changes property status to Verified Vacant
7. Citizen views the property on Interactive Map View with updated status
8. Citizen opens Property Detail Page and casts a vote for preferred use

## 7. Features Not Included in This Release

- Mobile native applications for iOS and Android
- Email notifications to citizens when their report status changes
- Integration with government property databases for automatic owner lookup
- Historical data visualization showing property status changes over time
- Export functionality for reports and statistics
- Multi-language support
- Advanced search functionality with keyword search
- Property comparison feature
- Public API for third-party integrations
- Citizen reputation system or gamification
- Direct messaging between citizens and admins
- Document upload for property ownership verification
- Integration with social media for sharing reports
- Automated report generation for government officials
- Payment processing for property acquisition or development fees
