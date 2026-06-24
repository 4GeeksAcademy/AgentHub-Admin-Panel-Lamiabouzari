# AgentHub Admin Panel - Project Specification

## 1. Product Description
1. AgentHub Admin Panel is a single-page administrative interface to monitor users, manage AI agents, review skill inventories, oversee agent contracts, and triage runtime errors.
2. The product is read/write at UI level only, using in-memory or local mock data collections to simulate operational workflows without server integration.
3. The primary users are operations managers and support staff who need a fast control surface for daily moderation, configuration, and status tracking tasks.
4. The UI must prioritize quick scanning, actionability, and consistency by using reusable components for cards, tables, dropdowns, and modals.

## 2. Tech Stack and Constraints
1. The implementation must use only HTML, Tailwind CSS via CDN, and Vanilla JavaScript (ES6+), with no frameworks, build tools, or package manager dependencies.
2. Tailwind must be loaded through the official CDN script in the document head; custom styling should be done with utility classes and optional small inline style tokens where needed.
3. No backend is allowed. No API requests, no database access, and no server-side rendering are permitted. All data must be represented as static seed data in JavaScript.
4. The application must run by opening the HTML file directly in a browser or through a basic static file server, with zero compile steps.

## 3. Component Inventory
1. Layout components: persistent sidebar navigation, top header with page title and controls, and main content container with responsive spacing.
2. Data display components: metric cards, tabular list sections, collapsible content rows, badges for status/plan, and chart placeholder panel.
3. Interaction components: dropdown menus, modal windows, form fields (including textarea), confirmation affordances, and row-level action buttons.
4. Feedback components: empty-state labels, resolved status indicators, and contextual messaging for destructive actions.

## 4. Dashboard
1. The dashboard must present exactly 4 metric cards at the top for high-level KPIs (for example: total users, active agents, active contracts, unresolved errors).
2. A weekly activity chart placeholder must appear below or beside the cards and reserve visual space for future chart integration, including title and axis labels or legend placeholder text.
3. Metric cards must include label, value, and trend context (such as up/down text indicator) to support quick decision-making.
4. Dashboard sections must be responsive, stacking vertically on small screens and using multi-column layout on medium and larger screens.

## 5. User Management
1. The Users section must display at least 5 seeded user records, each containing Name, Email, Plan, and Status.
2. Each user row must provide a View Detail action that opens a modal with expanded user information and a close control.
3. Each user row must provide a Delete action that removes the user from the current UI dataset after confirmation.
4. Status and Plan fields must use clear visual tags/badges to distinguish tiers and active or inactive state.

## 6. Agent Management
1. The Agents section must display at least 4 seeded agents with identifying metadata (for example name and status) and associated skills.
2. Each agent item must include a collapsible skills list that can expand and collapse without leaving the page.
3. A Configure action must open a modal containing an editable textarea for agent configuration text and a Save interaction that updates local UI state.
4. Each agent item must include a Delete action with confirmation and immediate UI removal.

## 7. Skills
1. The Skills section must list at least 4 skills with Name, Description, and Usage Count displayed in a structured list or table.
2. Each skill must include a View Detail action that opens a modal with complete skill information and related metadata.
3. Each skill must include a Delete action with confirmation and immediate removal from the rendered list.
4. Usage count formatting must remain consistent (numeric, right-aligned or clearly grouped) to support quick comparison.

## 8. Agent Contracts
1. The Contracts section must include at least 4 contract entries with Client, Agent, Skills, Start Date, End Date, and Amount Paid.
2. Every contract row must include a detailed contract modal that displays full contract terms, parties, period, and payment summary.
3. Skills for each contract must support multi-skill display (comma-separated or chips) and remain readable on mobile layouts.
4. Amount Paid must be formatted as currency and dates must use a consistent, human-readable format.

## 9. Error Log
1. The Error Log section must display at least 6 seeded error entries including Timestamp, Agent Name, Error Type, and Description.
2. Each error entry must include a View Detail action that opens a modal with full error context and troubleshooting notes placeholder.
3. Each error entry must include a Mark as Resolved action that updates status in the UI and visually differentiates resolved versus unresolved entries.
4. Error records should default to newest-first ordering based on timestamp for triage efficiency.

## 10. Global Interactions
1. The interface must provide a dark mode toggle that switches global theme tokens/classes and preserves readability/contrast across all components.
2. Sidebar navigation must support section switching (Dashboard, Users, Agents, Skills, Contracts, Error Log) and visually highlight the active section.
3. Dropdown menus must open on trigger interaction and close when the user clicks outside the dropdown boundary.
4. Modal windows must open for detail/configuration flows and close on explicit close actions, and also close when backdrop is clicked.
5. Shared interaction behavior must be implemented once and reused across sections to ensure consistent keyboard and pointer behavior.

## 11. Data Model
1. Users hardcoded dataset: an array of at least 5 objects with fields `id`, `name`, `email`, `plan`, `status`, and optional `createdAt`; `id` must be unique and stable for UI actions like modal open and delete.
2. Agents hardcoded dataset: an array of at least 4 objects with fields `id`, `name`, `status`, `skills` (array of skill IDs or names), and `configuration` (string used in editable textarea); collapsible rendering must read from `skills`.
3. Skills hardcoded dataset: an array of at least 4 objects with fields `id`, `name`, `description`, and `usageCount` (number); usage values must support sorting or comparison in the UI.
4. Contracts hardcoded dataset: an array of at least 4 objects with fields `id`, `client`, `agentId` or `agentName`, `skills` (array), `startDate`, `endDate`, `amountPaid`, and optional `currency`; modal detail view must map directly from these fields.
5. Error Logs hardcoded dataset: an array of at least 6 objects with fields `id`, `timestamp`, `agentName`, `errorType`, `description`, `resolved` (boolean), and optional `details`; Mark as Resolved must flip `resolved` in local state.
6. Relationship constraints: contracts should reference existing agents and skills, and dashboard metrics must be derived from these hardcoded arrays rather than duplicated constants.

## 12. Acceptance Criteria
1. The specification defines all required sections: Product Description, Tech Stack and Constraints, Component Inventory, Dashboard, User Management, Agent Management, Skills, Agent Contracts, Error Log, Global Interactions, Data Model, and Acceptance Criteria.
2. Dashboard requirements are met in scope with 4 metric cards and one weekly activity chart placeholder.
3. User Management requirements are met in scope with at least 5 users containing Name, Email, Plan, Status, plus View Detail modal and Delete action.
4. Agent Management requirements are met in scope with at least 4 agents, collapsible skills list, Configure modal with editable textarea, and Delete action.
5. Skills requirements are met in scope with at least 4 skills containing name, description, usage count, and row actions for View Detail and Delete.
6. Agent Contracts requirements are met in scope with at least 4 contracts containing client, agent, skills, dates, amount paid, and detailed contract modal.
7. Error Log requirements are met in scope with at least 6 errors containing timestamp, agent name, error type, description, and actions for View Detail and Mark as Resolved.
8. Global interaction requirements are met in scope with dark mode toggle, sidebar navigation, dropdown menus, outside-click dropdown close, modal windows, and backdrop-click modal close.
9. Data model requirements are met in scope with explicit hardcoded arrays for Users, Agents, Skills, Contracts, and Error Logs, including required fields and UI action compatibility.
10. The implementation constraints are explicit: HTML + Tailwind CDN + Vanilla JavaScript only, and no backend integration.
