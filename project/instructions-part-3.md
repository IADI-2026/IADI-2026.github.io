# Airport Management System — Part 3: React Client

---

## Introduction

In Part 3, your team must develop a **React client application** that integrates with the backend implemented in Part 2.

Before starting, you must:

1. Create a `part-2` branch in your repository to preserve the Part 2 codebase.
2. Continue development on the `main` branch for Part 3.

## General Requirements

### Technology Stack

You must use:

- React
- TypeScript
- Vite

### Project Structure

The React application must be placed in a **subfolder** named `react-client` at the root of the repository. This is *
*not** a Maven submodule.

## API Gateway Changes

The API Gateway implemented in Part 2 requires an `X-Api-Key` header on all requests. Since we don't want to expose this
key in the React client, the API Gateway must be updated as follows:

- The login endpoint must be **publicly accessible** — no `X-Api-Key` or `Authorization` header required.
- All other endpoints must **accept requests that include a valid `Authorization: Bearer <token>` header**, without
  requiring an `X-Api-Key` header.

## Pages

The application must include the following pages:

### `/login`

A login page that supports authentication for both **staff** and **passengers**.

- If your team implemented OAuth2 for passenger authentication in Part 2, that behaviour must be preserved in this part.
- After a successful login, the user must always be redirected to `/dashboard`.
- A logout option must be available.
- Closing the browser must clear the session (i.e., no persistent sessions).

### `/dashboard`

A dashboard page whose content must be rendered differently depending on the authenticated user's role:

#### Passenger

- One card displaying the passenger's personal information.
- One card per journey, each including a **Refresh** button that reloads only that card.

#### Airport Administrator

- One card per flight, displaying relevant flight information.
- Each card must allow changing the flight's operational status.
- Each card must include a **Refresh** button that reloads only that card.
- Refreshing the browser must reload all cards.

#### Creativity Component

Teams are invited to extend the dashboard with **one additional card** of their choosing, targeted at either the
passenger or the airport administrator role.

The card must use only endpoints already implemented in Part 2 — no new backend endpoints may be added. Cards with
higher complexity and practical usefulness will be valued more highly.

## Development and Production Modes

The application must support two running modes:

### Development Mode

Run the application using the Vite development server:

```
pnpm dev
```

### Production Mode

The React application must be bundled and served as **static content** from the web application module developed in Part
2.

- When running in production, the React client must be accessible at: `http://localhost:8090/app`
- The SSR web application from Part 2 must remain accessible at: `http://localhost:8090/web`
- The production build and installation into the web application's static content must be **automated via Maven**.

## Deliverables

### 1. Updated Repository

- A `part-2` branch preserving the Part 2 codebase.
- The `react-client` subfolder containing the React application.
- An updated Maven build that automates the production bundle installation.

### 2. `REACT_CLIENT.md`

Must include:

- React component diagram of the application
- Key architectural decisions and their justification (e.g., state management strategy, authentication, communication
  with the API Gateway, ...)
- Description of the additional card implemented as part of the creativity component

### 3. Updated `README.md`

Must include:

- Updated run and test instructions covering both development and production modes.
- A link to a video demonstrating the React client (see Video Rules below).
- A self-assessment table for Part 3 (see below).

#### Self-assessment for Part 3

Present a table with the self-assessment using percentages of fulfillment in the following topics (100% is perfect, >
50% needs improvement, <50% has flaws or is incomplete):

* Component Design & Reusability
* State Management (appropriate use of local state, context)
* API Integration & Error Handling
* React/TypeScript Best Practices (type safety, efficient component rendering, reusability, etc...)
* Passenger Authentication & Session Management
* Staff Authentication & Session Management
* Passenger User Experience
* Airport Administrator User Experience
* Creativity Component (complexity and usefulness of additional card)
* Documentation (`REACT_CLIENT.md` completeness and accuracy)
* Production Build & Maven Integration
* Demonstration Video

#### Video Rules

- The demonstration must preferably be recorded using the **production mode** (without the Vite dev server).
- If production mode is not achievable, the **development mode** is also accepted.
- If the production mode is used, the video must also demonstrate that the SSR web application from Part 2 continues to
  work correctly.
- Must be published on YouTube as an **unlisted video**.
- Must include narration (Portuguese or English).
- Maximum duration: **3 minutes**.

---

## Submission

The project must be submitted using the same GitHub repository as Parts 1 and 2.

## Use of AI Tools

Same rules as Part 2.

## Deadline

**31 May 2026 — 23:59**