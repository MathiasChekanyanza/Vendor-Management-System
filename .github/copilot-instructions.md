# Copilot / AI Agent Instructions — Vendor Management System

These concise instructions help AI coding agents be productive in this repository. Only project-discoverable facts are included.

1. Project snapshot
   - Single-page React app implemented as a functional component in `vendor-management-app.tsx`.
   - UI uses Tailwind CSS utility classes (look for className string patterns) and `lucide-react` icons.
   - No `package.json` or build scripts found in the workspace root — ask the human or check repo root before changing build-related files.

2. Persisted storage contract (critical)
   - The app accesses a host-provided storage API on `window.storage` with methods used in the code: `list(prefix)`, `get(key)`, `set(key, value)`, `delete(key)`.
   - Keys for vendor records are prefixed with `vendor:` (example: `vendor:vendor_166...`). Do not replace this contract; adapt by adding an adapter module if migration is needed.

3. Data shape and invariants (use these exact fields when creating/updating vendors)
   - Vendor object (JSON-stringified in storage):
     - id (string), name (string), address (string), phone (string)
     - image (string | empty) — stored as a data URL (base64) when present
     - createdAt (number), updatedAt (number) — Unix ms timestamps
   - Listing/sorting: UI sorts vendors by `createdAt` descending.

4. UI & UX patterns to follow
   - Modal form is controlled by `showForm` boolean; editing uses `editingVendor` to prefill `formData`.
   - Image uploads are validated client-side (size limit 2,000,000 bytes). Keep this validation when touching the upload flow.
   - Error handling pattern: log with `console.error(...)` and surface to the user with `alert(...)`.

5. Example code snippets (copy/paste-safe)
   - Save vendor: `await window.storage.set(`vendor:${vendor.id}`, JSON.stringify(vendor))`
   - Read vendors: call `await window.storage.list('vendor:')` then `await window.storage.get(key)` for each key

6. Editing rules for AI agents (actionable and repo-specific)
   - Preserve the `window.storage` usage. If you need to change the storage layer, implement a new adapter (e.g. `src/lib/storageAdapter.ts`) and migrate call sites in a separate PR that includes tests or a manual migration step.
   - Keep UI state patterns (useState/useEffect) and naming (formData, showForm, editingVendor) to reduce cognitive load for maintainers.
   - When adding new fields to vendor objects, maintain backward compatibility: default missing fields when reading from storage and bump `updatedAt` when writing.

7. Missing / unknown bits that require human input
   - No build/test commands discovered: ask which package manager and start/build scripts to use. Common expectations: React + Tailwind + lucide-react.
   - No test harness detected. If asked to add tests, confirm preferred framework (Jest/React Testing Library or Vitest) before creating files.

8. Where to look next (key file to inspect)
   - `vendor-management-app.tsx` — primary UI and business logic (single file currently). Use it as the canonical example for storage access and data shape.

If anything in the above is unclear or you want more/less detail (for example, a full storage adapter example or suggested test scaffolding), tell me what to add and I will update this file.
