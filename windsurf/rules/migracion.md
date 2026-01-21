---
trigger: always_on
---

# Migration Rules: lifeid-mobile (Legacy to Expo 53)

## 1. Fundamental Principles

These are the main rules that must be followed to migrate any functionality from the legacy project (`lifeid-mobile-base`) to the new project (`lifeid-mobile-53`).

- **Rule 1.1 (Preliminary Analysis):** Before implementing, the corresponding component or screen in the legacy project must be analyzed to understand its business logic, state management, and user flow.
- **Rule 1.2 (UI with React Native Paper):** The entire user interface must be rebuilt using components from the `react-native-paper` package. Direct migration of `@mui/material` components or associated styles should be avoided.
- **Rule 1.3 (Typed Services):** All communication with the backend must be done exclusively through the services already defined and typed in the `src/services` directory. The use of `axios` or `fetch` directly in the interface components is prohibited.
- **Rule 1.4 (Centralized State Management):** The state of the application, especially user information and authentication status, must be managed through existing `Contexts` (e.g., `AuthContext`, `UserContext`).
- **Rule 1.5 (Navigation with Expo Router):** The navigation structure must follow the Expo Router “file-system routing” paradigm. New screens must be created as files within the `app/` directory.
- **Rule 1.6 (Flow Replication, Not Code Migration):** The legacy project serves exclusively as a reference to understand the application's flow and business logic. Direct code porting is prohibited. All functionality must be re-implemented from scratch using the tools and patterns of the Expo 53 ecosystem (React Native Paper, Expo Router, Typed Services, etc.).

## 2. Screen Migration Process

For each screen or component to be migrated, the following process must be followed:

1. **Identify the Legacy Screen:** Locate the screen file in `lifeid-mobile-base/screens/`.
2. **Create the Route File:** Create the corresponding file in the `lifeid-mobile-53/app/` structure. For example, `screens/Login/Login.tsx` becomes `app/login.tsx`.
3. **Implement the Logic:** Reimplement the component logic using React hooks (`useState`, `useEffect`) and context hooks (`useAuth`).
4. **Connect Services:** Import and use service functions (`*.services.ts`) to get or send data.
5. **Build the UI:** Lay out the screen using `react-native-paper` components and the global styles/themes of the new project.

## 3. Dependency Management

- **Rule 3.1 (Do Not Add Obsolete Dependencies):** Do not add dependencies from the legacy `package.json` without first checking if there is a modern alternative or if its functionality is already covered by Expo SDK 53 (e.g., `uuid` -> `expo-crypto`).
- **Rule 3.2 (Updating Native Components):** Components that depend on obsolete native APIs, such as `BarCodeScanner`, must be replaced with their modern equivalents (`expo-camera/next`), as indicated in the project memory.

## 4. References

- **Legacy Project:** `C:\Users\Denis\Documents\Flock\lifeid-mobile-base`

- **New Project (Destino):** `C:\Users\Denis\Documents\lifeid-mobile-53`