# StayEase: Airbnb Clone Project

## Overview
StayEase is a full-stack clone of the Airbnb platform, focused on enabling users to browse property listings, view details, and make bookings. This project includes both frontend and backend development, emphasizing responsive UI, secure checkout, and a seamless booking experience.

## Project Goals
- Build a responsive and functional web application
- Implement component-based frontend using React
- Integrate backend APIs and database for real-time interaction
- Ensure accessibility and mobile responsiveness

## Tech Stack
- **Frontend:** HTML, CSS, JavaScript (React)
- **Version Control:** Git & GitHub
- **Design:** Figma (UI/UX)
- **Deployment:** To be decided (e.g., Netlify for frontend, Render or Heroku for backend)

## UI/UX Design Planning

### Design Goals
- Create an intuitive booking flow
- Ensure visual consistency across pages
- Prioritize mobile responsiveness and speed
- Deliver a pleasant and accessible user experience

### Key Features
- Property search with filters
- Detailed view for each property
- Secure checkout process
- User registration and authentication

### Primary Pages

| Page                  | Description                                                  |
|-----------------------|--------------------------------------------------------------|
| Property Listing View | Grid view showing available properties with filters          |
| Listing Detailed View | Full property info, images, pricing, and booking form        |
| Simple Checkout View  | Final confirmation and secure payment                        |

### Importance of User-Friendly Design
User-friendly design is critical for reducing friction and increasing bookings. It ensures clarity, builds trust, and accommodates all users (including mobile and disabled users), leading to higher satisfaction and conversions.

### Figma Design Specifications

**Color Styles:**
- Primary: `#FF5A5F`
- Secondary: `#008489`
- Background: `#FFFFFF`
- Text: `#222222`
- Secondary Text: `#717171`

**Typography:**
- Primary Font: Circular
- Headings: Bold (700), 24px–32px
- Body: Medium (500), 16px
- Secondary Text: Book (400), 14px

### Why Design Properties Matter
Identifying color schemes, font styles, and sizes in mockups ensures brand consistency, readability, and a polished user experience. These elements guide developers in implementing exact UI elements, helping translate design to code accurately.

## Project Roles and Responsibilities

| Role             | Responsibilities                                                                 |
|------------------|-----------------------------------------------------------------------------------|
| Project Manager  | Coordinates the team, manages deadlines, tracks progress                         |
| Frontend Devs    | Implement UI components, connect frontend to backend, ensure responsiveness      |
| Backend Devs     | Build APIs, manage DB interactions, implement logic (e.g., bookings, login)      |
| Designers        | Create mockups, maintain Figma design system, focus on user experience            |
| QA/Testers       | Write test cases, perform manual and automated testing, report bugs               |
| DevOps Engineers | Set up hosting, CI/CD pipelines, monitor server infrastructure                   |
| Product Owner    | Defines requirements, prioritizes features, ensures project meets user needs      |
| Scrum Master     | Facilitates sprints, removes blockers, leads retrospectives and standups          |

## UI Component Patterns

We plan to build reusable components for efficiency and design consistency.

### Planned Components:

**1. Navbar**
- Logo
- Search bar
- User dropdown/login link
- Hamburger menu for mobile

**2. Property Card**
- Thumbnail image
- Price, rating, and location
- Favorite (heart) button
- Click to view more

**3. Footer**
- Company info (About, Careers, Help)
- Social media links
- Copyright

Each component will be modular, mobile-friendly, and accessible. Shared styles and props will ensure consistency across pages.

