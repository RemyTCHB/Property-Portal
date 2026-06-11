TCHB Property Portal (Investor Network)

Welcome to the Total Cash Home Buyers (TCHB) Property Portal. This project is a highly interactive, secure, and dynamic frontend web application designed to present real estate investment proposals to an exclusive network of buyers.

The application dynamically fetches property data from a Google Sheets backend (via Google Apps Script) and presents it using a premium, dark-themed UI featuring custom Canvas animations, secure two-step authentication, and dynamic financial charts.

🚀 Features

Secure Two-Step Authentication (2FA): * Users must enter an authorized Email and a specific Access Key to view a property.

A 6-digit OTP (One-Time Password) is sent via a webhook to verify the user's identity before unlocking the proposal.

Dynamic Data Rendering: Fetches real-time property statuses, pricing, and specific deal metrics from a centralized database.

Interactive Financial Proposals: Automatically adapts the UI to the type of deal being viewed (e.g., Creative/Subject-To, Wholesale, Fix & Flip, Novation, Seller Finance, Rental).

Data Visualization: Utilizes Chart.js to render beautiful, comparative charts for interest accumulation, monthly payment structuring, and capital slice breakdowns.

Premium UI/UX:

Custom Pointer: A custom-built cursor featuring a smooth, color-cycling, concentric radial gradient (Emerald, Indigo, Crimson) that tracks mouse movement.

Interactive Grid Background: A full-screen <canvas> that draws dynamic, interactive "sparks" that respond to user clicks and idle time.

Print-Ready: The proposal page includes dedicated print-media CSS to export beautifully formatted PDFs directly from the browser.

📁 Project Structure

The project relies on two primary HTML files, designed to run entirely in the browser without a heavy build step.

1. index.html (The Dashboard)

The main entry point. It fetches the active database of properties and displays them in an interactive grid.

Displays property status (Available, Pending, Sold).

Handles the initial Authentication Modal (Email & Access Key -> OTP).

Features the animated concentric ring loader and text gradients.

2. proposal.html (The Deal Room)

The detailed proposal view, accessed via a URL parameter (?id=PROPERTY_ID).

Includes a "Secure Gate" to ensure direct links cannot bypass authentication.

Dynamically populates specific tables (e.g., Subject-To Amortization vs. Standard Market) based on the Deal_Type data parameter.

Renders comparative bar and doughnut charts.

Optimized for PDF export (hides secure gates, animations, and cursors when printing).

🛠 Technology Stack

HTML5 / Vanilla JavaScript: Core structure and logic. No heavy JavaScript frameworks required.

Tailwind CSS (via CDN): Used for rapid, responsive styling and utility classes. Custom configurations are injected directly into the <head>.

Chart.js: Used in proposal.html for financial data visualization.

HTML5 Canvas: Used for the interactive, animated grid background.

Backend Backend/Database: Google Apps Script (exec URLs) acts as a REST API to fetch data and trigger email/logging webhooks.

⚙️ Configuration & Setup

Because this project uses vanilla web technologies and CDN links, no npm install or build processes are required. You can simply host these files on any static web server (like GitHub Pages, Netlify, or Vercel).

API Endpoints

The portal relies on two distinct Google Apps Scripts to function. If you ever need to migrate the backend or update the scripts, you must update these constants located at the top of the <script> tags in both index.html and proposal.html:

// 1. Fetches the active property database (Expected to return a JSON array of properties)
const API_URL = "[https://script.google.com/macros/s/.../exec](https://script.google.com/macros/s/.../exec)";

// 2. Handles triggering OTP emails and logging access attempts (Expected to accept POST requests)
const LOGGING_WEBHOOK_URL = "[https://script.google.com/macros/s/.../exec](https://script.google.com/macros/s/.../exec)";


Branding Colors

The project utilizes a custom Tailwind theme defined in the <head>. To alter the primary brand colors globally, update the Tailwind configuration block:

tailwind.config = {
    theme: {
        extend: {
            colors: {
                brand: {
                    dark: '#0b0f19', 
                    card: 'rgba(17, 24, 39, 0.75)',
                    purple: '#4f46e5', 
                    crimson: '#dc2626', 
                    emerald: '#10b981', 
                    gold: '#f59e0b'
                }
            }
        }
    }
}


🎨 Note on Custom Animations

This project relies heavily on custom CSS @keyframes and mix-blend-mode properties to achieve its unique look.

The Custom Pointer: Controlled via #mouseGlow, #cursor-dot, and #cursor-ring CSS ids. The gradient uses a radial-gradient setup combined with a hue-rotate animation to cycle colors smoothly without harsh edges.

The Canvas Grid: The background sparks are calculated mathematically in the JavaScript animateGrid function, relying on requestAnimationFrame for high-performance 60fps rendering.

Strictly Confidential. Distribution of portal access keys is prohibited.
