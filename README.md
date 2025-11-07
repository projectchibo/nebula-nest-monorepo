# Nebula Nest Monorepo
 
 Single repo hosting multiple projects for the same Firebase project.
 
 ## Structure
 - **apps/landing**: React + Vite SPA (TypeScript)
 - **functions/**: Firebase Cloud Functions (TypeScript)
 - **tsconfig.base.json**: Shared TS config
 
 ## Requirements
 - Node 18+
 - npm 9+
 - Firebase CLI (`npm i -g firebase-tools`)
 
 ## Install
 ```bash
 npm install
 ```
 This installs dependencies for all workspaces.
 
 ## Develop
 - **Landing app**
 ```bash
 npm run dev
 ```
 Serves on http://localhost:5173
 
 ## Build all
 ```bash
 npm run build
 ```
 Runs `build` in each workspace (`apps/*`, `functions`).
 
 ## Firebase setup (one-time)
 Run in repo root:
 ```bash
 firebase login
 firebase init
 ```
 Recommended choices during `firebase init`:
 - **Use an existing project**: select your Firebase project
 - **Features**: Functions (you can add Hosting later if desired)
 - **Functions language**: TypeScript
 - **Functions directory**: `functions`
 - **ESLint**: your choice
 - **Install deps**: choose "No" (npm workspaces will handle it)
 
 This will create `firebase.json` and `.firebaserc`.
 
 ## Deploy (after init)
 - Functions:
 ```bash
 npm --workspace functions run build
 firebase deploy --only functions
 ```
 - Hosting (if later added for landing app):
   - Build the SPA: `npm --workspace apps/landing run build`
   - Configure `firebase.json` hosting public to `apps/landing/dist`
   - Deploy: `firebase deploy --only hosting`
 
 ## Add more apps later
 - Create a new folder under `apps/` with its own `package.json` and build scripts
 - It will be picked up by the workspace automatically
 
 ## Scripts reference
 - **root**
   - `build`: build all workspaces
   - `dev`: run landing app dev server
   - `lint`, `typecheck`, `clean`: forwards to each workspace if present
 - **apps/landing**
   - `dev`, `build`, `preview`, `typecheck`
 - **functions**
   - `build`, `typecheck`, `clean`