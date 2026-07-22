# Codex Build Prompt

Build a lightweight deployable web MVP for the project: Omni-channel KOL Collaboration Tool.

## Main Goal

Create a flexible web tool that helps KOL Promotion Specialists upload creator collaboration data, manage cross-platform outreach (YouTube/TikTok/IG), and generate daily follow-up task lists. 

The MVP should accommodate multiple brands/projects and focus on this core user question:
**Who should I follow up with today, what is their status, and what is the exact action to take?**

## Tech Requirement

Please build this as a lightweight web app that can be deployed later to Vercel or Netlify.

Recommended stack:
* React or Next.js
* TypeScript if possible
* Clean and simple UI
* No login required
* No database required (Local storage is acceptable for saving Settings)
* No external API integration required
* Data should be processed temporarily in the browser

## 1. Global Settings (Configuration Hub)

Before processing data, the app must include a **Settings** section where users can customize their workflow. These settings must dictate how other components behave:
*   **Brand Management:** Add/edit/delete brand names.
*   **Database Column Configurator:** Allow users to add, edit, or remove custom table headers for the uploaded spreadsheet. 
*   **Fulfillment Methods:** Define how samples/payments are delivered (e.g., Physical Shipping, Bank Transfer, Order Placement).
*   **Content Review Criteria:** Define customizable checklists for content approval (e.g., Logo visibility, BGM rules).

## 2. Dashboard (Today's Workspace)

*   **View Toggle:** Default to an "All Work/Brands" overview. Allow users to filter the dashboard by specific custom brands defined in Settings.
*   **Project Overview:** Display aggregate stats categorized by two dimensions: 
    1. By Brand
    2. By Specific Product

## 3. Data Input & KOL Database

Users will upload a CSV or Excel file. The app must parse this based on the headers defined in Settings. 

The baseline columns must include:
*   Creator username & Profile link
*   **Channel type** (e.g., YouTube, TikTok, Instagram)
*   **Creator tier / level** (e.g., Micro, Mid, Macro)
*   Contact method
*   Product & Brand
*   Current status
*   Fulfillment method & status (Shipping/Bank Transfer, mapped to Settings)
*   **Transfer / Payment account details** (e.g., PayPal/Bank Info)
*   **Paid amount / Collaboration fee**
*   Sample delivered date / Payment cleared date
*   Video progress
*   Video posted date (Updated from first video posted date)
*   Video upload time
*   Collaboration count (How many times we worked with them)
*   **Collaborated models / Past products**
*   Last contact date & follow-up count
*   Notes

## 4. Daily Task Summary & Priority Logic

Generate a summary showing total creators and tasks broken down by priority. Priority logic based on `docs/mvp-rules.md`:
1.  **Highest:** Fulfillment completed (delivered/transferred) but video progress is still 0.
2.  **High:** Creator posted 1 video but has not posted the required subsequent content.
3.  **Medium:** Followed up but no reply after 1 day.
4.  **Low:** Contacted but no reply after 2 days.

*   **Highest Priority Explanation:** Provide a text breakdown for "Highest" priority creators explaining *why* they are urgent (e.g., delivery timing vs. missing video) and the suggested next action.
*   **Failed Candidate Warning:** Flag creators based on failure rules, but require the user to manually confirm/mark them as failed.

## 5. Message Generator

Allow the user to select one creator from the task table and choose a platform channel: **YouTube, TikTok, or Instagram**. 

Generate an English message, followed by a Chinese translation/explanation. 

**STRICT TEMPLATE RULE FOR OUTREACH:** 
When generating outreach messages or emails, the prompt MUST strictly follow this fixed structure:
1.  **Compliment:** Acknowledge their recent specific content.
2.  **Purpose:** State the reason for reaching out clearly.
3.  **Company Introduction:** Briefly introduce the brand.
4.  **Product Introduction:** Highlight key selling points relevant to their audience.

**STRICT SUBJECT LINE RULE:**
All generated email subject lines MUST use this exact format: `[FIFINE Collaboration Invitation: Product Name]`

## 6. Content Review Module

Allow users to select a creator whose video is ready for review and display the dynamic checklist defined in the Settings module. Allow the user to check off items before generating a final approval/revision message.

## UI Requirements

Keep the interface clean, practical, and modular. Suggested layout:
1.  **Top Navigation:** Dashboard | KOL Database | Settings
2.  **Dashboard View:** "All Brands" selector, summary cards, and Project categorizations.
3.  **Upload Area & Data Preview** (Reflecting custom headers).
4.  **Daily Task Table** (Sorted by priority).
5.  **Highest Priority Action Panel**.
6.  **Omni-channel Message Generator & Content Reviewer** (Appears when clicking a task).

## Important Notes

*   Do NOT build a login system, backend database, or payment system.
*   Do NOT hardcode the table headers or fulfillment methods (they must pull from Settings).
*   Focus purely on a functional frontend MVP that processes CSV/Excel files locally and guides the specialist's daily workflow.
