# TeleDrive Ultra — Next-Gen Encrypted Telegram Cloud Drive & Vault

TeleDrive Ultra transforms a user's private Telegram supergroup and forum topics into an unlimited, zero-knowledge personal cloud storage drive and encrypted vault. This plan upgrades and ports the application into a native, ultra-responsive Android experience with multi-theme visual polish, a 7-step Telegram onboarding and dual-PIN security flow, real Telegram Bot API synchronization, built-in media streaming players, and batch file management.

### User Review & Critical Decisions

> [!IMPORTANT]
> The following product and design choices have been confirmed from your preferences and will guide the implementation:

- **Confirmed Decision 1 — Multi-Theme Luxury Design System**: Support 5 instant-switchable themes (**Nordic Frost Light**, **M3 Adaptive Dark**, **OLED Obsidian**, **Cyberpunk Neon**, and **Emerald Champagne**) with smooth animated color transitions, glassmorphic cards, and custom typography (`Plus Jakarta Sans` + `JetBrains Mono`).
- **Confirmed Decision 2 — 7-Step Telegram Onboarding & Dual Vault PIN Lock**: Include the signature 7-step interactive onboarding flow (Welcome, Telegram API Setup, Country & Phone Number, OTP Verification Code, 2FA Cloud Password, Auto-Backup Folder Selector, and Master Vault PIN setup) paired with a **Dual PIN Lock Screen** (`1234` for the Real Personal Vault, `9999` for the Panic/Decoy Vault mode).
- **Confirmed Decision 3 — Complete Power Feature Suite**:
  - **Real Telegram Bot API & Forum Topic Sync**: Live HTTP dispatch to `api.telegram.org` (`sendMessage`, `createForumTopic`, `sendDocument`) with an authentic Telegram Supergroup message bubble live preview modal.
  - **Built-in Streaming Media Players**: Persistent floating mini-player bar, full-screen interactive audio player with synthesized ambient playback & waveform progress scrubbers, video player modal, and code/PDF document reader.
  - **Encrypted Safi Vault Records**: Dedicated structured editors and unmasked Telegram message card previews for **Photos**, **SMS & OTP Codes**, **Bank/Travel Cards**, **Job Files**, **Tutorials**, **Software**, and **PDF Documents**.
  - **Advanced File & Folder Manager**: Physical folder-tab cutout cards, storage analytics rings/bars, search & multi-criteria sorting, batch selection mode, and instant share links.

---

### 1. Overview & Core Concept

- **What It Does**: TeleDrive Ultra provides an all-in-one personal cloud drive and encrypted credential vault backed by Telegram's cloud infrastructure. Users can organize files into color-coded Vault Folders (mirrored to Telegram Forum Topics), store sensitive records (OTP codes, payment cards, documents, photo albums), stream audio/video transfers with a persistent mini-player, and preview/dispatch formatted messages directly to their Telegram channel.
- **Target Audience / Persona**: Privacy-conscious power users, developers, and digital professionals who want unlimited cloud storage, instant Telegram topic organization, and military-grade local + cloud vault access with panic-PIN protection.
- **Key Value**: Combines the visual refinement of a flagship cloud drive (Dropbox / Google Drive inspired) with Telegram's unlimited storage, zero-knowledge AES-256 metadata tagging, and decoy vault security.

---

### 2. User Experience & Visual Design

- **Key User Flows**:
  1. **7-Step Onboarding & Dual-PIN Unlock**: First-time users (or users logging out) experience a sticky-header 7-step wizard with an animated sine-wave progress bar, country code picker, 2FA password toggle, device auto-backup folder toggles, and PIN configuration. Returning users can unlock with either the **Real PIN (`1234`)** or **Decoy PIN (`9999`)** or switch between vaults from Security Settings.
  2. **Home / Drive Dashboard**: Displays the top status bar with live connection state (`Telegram Synced` vs `Local Vault`), search & filter bar, quick action pills (`Upload`, `New Folder`, `Ghost Camera Scan`, `Batch Select`), interactive storage analytics breakdown card, 4 quick-access glass category cards, recent cloud files list, and the 2-column **Vault Folders Grid** with folder-tab cutouts.
  3. **Photos & Gallery Tab**: Features `Album` and `Timeline` view toggles, instant device photo picker integration (`PickVisualMedia`), photo count badges, and full-screen album inspection with Telegram sync preview.
  4. **Transfers & Streams Tab**: Displays active upload/download streams with animated progress bars, transfer speed indicators, play/pause/delete controls, 2-column recently uploaded cards, and a direct device file uploader.
  5. **Profile & Luxury Settings Tab**: Features a curved dark hero header with user identity (`Md Safi Islam • Team Leader`), `PRO` badge, live `DC5 22ms` Telegram session indicator, theme switcher sheet (5 themes), Telegram Bot & Supergroup configurator with live `Test Connection`, Dual PIN Vault lock screen trigger, push notification toggle, and session logout.
- **Visual Identity & Theme**:
  - *Aesthetic Direction*: Ultra-clean fintech/cloud-drive luxury with tactile squircle iconography, layered glassmorphism, and crisp micro-badges.
  - *Color Palette & Mood*:
    - **Nordic Frost (Light)**: `--background: #F5F7FC`, `--surface: #FFFFFF`, `--primary: #246BFD`, `--accent: #FDCB38`
    - **M3 Adaptive Dark**: `--background: #0C0E17`, `--surface: #151926`, `--primary: #3B82F6`, `--accent: #FDCB38`
    - **OLED Obsidian**: `--background: #000000`, `--surface: #0A0D14`, `--primary: #00F2FE`, `--accent: #10B981`
    - **Cyberpunk Neon**: `--background: #090615`, `--surface: #130D2A`, `--primary: #FF007F`, `--accent: #00F2FE`
    - **Emerald Champagne**: `--background: #071712`, `--surface: #0E261E`, `--primary: #10B981`, `--accent: #F59E0B`
  - *Typography & Hierarchy*: Bundled `Plus Jakarta Sans` for bold geometric headers and UI labels paired with `JetBrains Mono` for OTP codes, 16-digit card numbers, cryptographic hashes, and file sizes.
  - *Component Styling & Layout*: Edge-to-edge layout respecting system status and navigation bar insets, floating pill bottom dock with an elevated center `+` action button, and floating persistent audio mini-player bar positioned cleanly above the dock.
- **Interactive Feedback & Motion**:
  - Spring-physics tab transitions, animated sine-wave onboarding progress, rotating vinyl disc indicator in the mini-player, smooth progress bar fills, and sleek floating toast notifications at the top of the viewport.

---

### 3. Key Product Decisions & Trade-Offs

- **Decision 1: Native Jetpack Compose Architecture with Full Feature Parity**
  - *Chosen Approach*: Build the entire application natively in Kotlin and Jetpack Compose with Material 3 adaptive components, custom Canvas drawings (wavy progress bar, storage rings, Telegram doodle pattern), and Android system integrations (Photo Picker, Document Picker, Clipboard, Audio Synthesizer).
  - *Why*: Required by the AI Studio Android runtime (`gradle assembleDebug`) while delivering 60fps native animations, edge-to-edge system inset handling, and zero WebView lag.
  - *Alternatives Considered*: Wrapping the static HTML in a WebView — passed over because native Compose provides superior touch responsiveness, native file/photo pickers, and authentic Material 3 motion.
- **Decision 2: Real Telegram Bot HTTP API + Offline-First Local Persistence**
  - *Chosen Approach*: Persist all folders, vault records, theme preferences, onboarding state, and Telegram Bot credentials locally on device while executing real HTTPS calls to `https://api.telegram.org/bot<TOKEN>/...` for testing connections, creating Forum Topics, and dispatching records.
  - *Why*: Ensures the app works out-of-the-box with zero configuration in local vault mode and immediately dispatches real Telegram messages as soon as the user saves their Bot Token and Chat ID.

---

### 4. Technical Architecture & Data Strategy *(Technical Reference)*

- **Architecture & Component Diagram**:

```
┌───────────────────────────────────────────────────────────────────────────┐
│                        MainActivity (Edge-to-Edge)                        │
│               ThemeEngine (5 Switchable Color/Token Palettes)             │
└─────────────────────────────────────┬─────────────────────────────────────┘
                                      │ observes StateFlow
┌─────────────────────────────────────▼─────────────────────────────────────┐
│                             TeleDriveViewModel                            │
│  ┌──────────────────────┐ ┌──────────────────────┐ ┌───────────────────┐  │
│  │ Vault & Folder State │ │  Media & Stream Eng  │ │ Onboarding & PIN  │  │
│  │ (Real vs Decoy Mode) │ │ (Synth Audio/Video)  │ │   7-Step State    │  │
│  └──────────┬───────────┘ └──────────┬───────────┘ └─────────┬─────────┘  │
└─────────────┼────────────────────────┼───────────────────────┼────────────┘
              │                        │                       │
     ┌────────▼────────┐      ┌────────▼────────┐     ┌────────▼────────┐
     │ VaultRepository │      │ TelegramApiSvc  │     │  AudioSynthEng  │
     │ (SharedPrefs /  │      │ (HTTPS Bot API  │     │ (AudioTrack PCM │
     │  JSON Storage)  │      │  sendMessage &  │     │  Lo-Fi Chimes)  │
     └─────────────────┘      │  Forum Topics)  │     └─────────────────┘
                              └─────────────────┘
```

- **Data Model & State**:
  - `VaultCategory`: `id`, `name`, `icon`, `colorHex`, `sizeLabel`, `topicThreadId`, `isDecoy`
  - `VaultRecord`: `id`, `catId`, `title`, `notes`, `created`, `photoCount`, `imgUrl`, `phone`, `sender`, `otpCode`, `cardNumber`, `expiry`, `cvv`, `cardHolder`, `fileName`, `fileSize`, `sha256Hash`
  - `StreamItem`: `id`, `title`, `subtitle`, `progress`, `type` (`AUDIO`, `VIDEO`, `DOCUMENT`), `accentColorHex`, `speedLabel`, `isPaused`
  - `TelegramConfig`: `botToken`, `chatId`, `topicId`, `customDomain`, `apiId`, `apiHash`, `userPhone`, `autoBackupFolders`
  - `VaultSecurityState`: `isAuthenticated`, `isLocked`, `isDecoyMode`, `realPin` (`1234`), `decoyPin` (`9999`)

- **Interactive Component & State Mapping**:
  - **7-Step Onboarding & PIN Lock Screen**: Validates step inputs, updates the animated sine-wave progress header, toggles 2FA visibility, persists selected auto-backup folders, and switches active dataset between Real Vault and Decoy Vault based on the entered PIN (`1234` vs `9999`).
  - **Drive Dashboard & Batch Manager**: Filters folders and files in real time via search query, sorts by Name/Size/Date, supports multi-item selection for batch delete or batch Telegram dispatch, and opens folder detail sheets.
  - **Multi-Type Add/Save Modal**: Dynamically switches input fields based on selected category (`Photos` with Android Photo Picker, `SMS & OTP`, `Card Details`, or `Files & Documents` with Android Document Picker), computes SHA-256 verification preview, saves record, and launches the **Telegram Bot Live Message View**.
  - **Telegram Bot Live Message View & Configurator**: Renders an authentic Telegram message bubble with inline action buttons (`Copy OTP/Card`, `Send to Telegram Now`) and executes real HTTPS POST requests to the Telegram Bot API with toast feedback.
  - **Persistent Audio Mini-Player & Full-Screen Media Modals**: Generates real ambient harmonic audio via Android `AudioTrack` PCM synthesis, updates elapsed/total time every second, supports play/pause/skip/seek scrubbing, and provides interactive Document and Video preview modals.
