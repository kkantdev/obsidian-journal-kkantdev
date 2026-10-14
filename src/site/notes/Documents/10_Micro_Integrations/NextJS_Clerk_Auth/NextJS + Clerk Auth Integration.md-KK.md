---
{"dg-publish":true,"permalink":"/documents/10-micro-integrations/next-js-clerk-auth/next-js-clerk-auth-integration-md-kk/","tags":["project"],"dg-note-properties":{"tags":["project"]}}
---

# Documentation: Next.js + Clerk Cloud Auth Setup Guide

This document covers the step-by-step implementation for integrating **Clerk Authentication** into a standard **Next.js (App Router)** application.

---
So that you have to install Node.js  

```
winget install OpenJS.NodeJS.LTS
```

```
node -v
```


🛠️ Step 1: Initialize Next.js Project

Run the official initializer in your terminal to scaffold a clean Next.js application frame.

Bash

```
npx create-next-app@latest my-app --yes
```

> _Note: The `--yes` flag applies standard defaults (TypeScript, Tailwind CSS, ESLint, and App Router structure) automatically._

Once complete, navigate into the project directory:

Bash

```
cd my-app
```

---

## 📦 Step 2: Install the Clerk SDK

Install the official Clerk Next.js package, which provides the global state providers, pre-built hooks, and frontend components.

Bash

```
npm install @clerk/nextjs
```

---

## 🔑 Step 3: Configure Cloud Keys (`.env.local`)

Create an environment file named `.env.local` directly in the **root directory** of your project to safely map your application to the Clerk Cloud instance:

Code snippet

```
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_your_publishable_key_here
CLERK_SECRET_KEY=sk_test_your_secret_key_here
```

> _⚠️ Safety Note: Never commit this file to GitHub or public source control._

---

## 🌍 Step 4: Inject the Global Cloud Provider

To allow Clerk to monitor user state across your entire web application, wrap your root node layout framework.

Update **`src/app/layout.tsx`**:

TypeScript

```
import { ClerkProvider } from '@clerk/nextjs'
import './globals.css'

export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <ClerkProvider>
      <html lang="en">
        <body>{children}</body>
      </html>
    </ClerkProvider>
  )
}
```

---

## 🛡️ Step 5: Mount Request Interception (Middleware)

Clerk checks requests to evaluate authentication contexts on incoming page loads. Create a new file named **`src/middleware.ts`**:

TypeScript

```
import { clerkMiddleware } from '@clerk/nextjs/server'

export default clerkMiddleware()

export const config = {
  matcher: [
    // Exclude static asset paths and Next.js internal core routes
    '/((?! _next|[^?] *\\.(?:html?|css|js(?!on)|jpe? g|webp|png|gif|svg|ttf|woff2?|ico|csv|docx?|xlsx?|zip|webmanifest)).*)',
    // Always intercept API and tRPC routes
    '/(api|trpc)(.*)',
    // Always intercept internal Clerk dashboard routing endpoints
    '/__clerk/(.*)',
  ],
}
```

---

## 🎨 Step 6: Implement Cloud Connection Test Elements

Wipe out the template placeholder view inside your entry layout file to add reactive components that show different contents based on connection status.

Update **`src/app/page.tsx`**:

TypeScript

```
import { SignedIn, SignedOut, SignInButton, UserButton } from "@clerk/nextjs";

export default function Home() {
  return (
    <main className="flex min-h-screen flex-col items-center justify-center bg-slate-50 p-6">
      <div className="bg-white p-8 rounded-2xl shadow-xl max-w-sm w-full text-center">
        <h1 className="text-xl font-bold mb-4 text-slate-800">Telecom System Check</h1>
        
        {/* Rendered if the client is logged out */}
        <SignedOut>
          <p className="text-slate-500 mb-6">Cloud Authentication Connection: Offline</p>
          <SignInButton mode="modal">
            <button className="w-full bg-blue-600 hover:bg-blue-700 text-white font-medium py-2.5 px-4 rounded-xl transition">
              Connect to Auth Server
            </button>
          </SignInButton>
        </SignedOut>

        {/* Rendered if the client session is verified */}
        <SignedIn>
          <p className="text-emerald-600 font-semibold mb-2">✓ Connection Securely Active</p>
          <p className="text-slate-500 mb-6">User Token verified by Cloud Layer.</p>
          <div className="flex justify-center">
            <UserButton />
          </div>
        </SignedIn>
      </div>
    </main>
  );
}
```

---

## 🚀 Step 7: Launch Local Development Engine

Spin up your local client proxy server to evaluate the setup live:

Bash

```
npm run dev
```

Navigate your browser window to `http://localhost:3000` to verify structural functionality.