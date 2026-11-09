# Apt404 Roommate Messenger (IRC Edition)

A minimalist, distraction-free instant messaging client designed for household communication, inspired by classic mIRC and modern terminal aesthetics.

---

## 1. Quick Start & Setup

1. **Launch**: Open `msn_roommates.html` in any modern web browser.
2. **Initial State (Clean Slate)**: The client connects into a quiet, completely **blank lobby**. No preset channels or message clutter are loaded.
3. **Create Channels**: Click the green **`+ Add`** button in the sidebar under **Channels** to create your custom channels (e.g., `#lounge`, `#kitchen`, `#chores`, `#study`, `#gaming`).
4. **Edit & Delete Channels**:
   - Hover over any channel in the sidebar: click **`✎`** to rename it or edit its topic, or click **`×`** to delete it.
   - You can also edit or delete the currently active channel directly from the top header bar.
5. **Multi-Tab / Multi-Device Sync**: The app uses the HTML5 `BroadcastChannel` API (`apt404-irc-channel`). Open the file across multiple browser tabs or windows to chat live with different roommate personas in real time.

---

## 2. Admin Security & Role-Based UI Visibility

### Are Admin Tools Private to You?
**Yes.** All admin tools and destructive controls are strictly restricted by user role and protected by a host PIN:

* **What Regular Roommates See**:
  - Regular roommates (`Alex`, `Sam`, `Jordan`, `Taylor`) see only the clean chat interface and public channel list.
  - The **`+ Add` Channel** button is completely hidden.
  - The hover **Edit (`✎`)** and **Delete (`×`)** buttons on channels are completely hidden.
  - The **`⚙` (Admin Gear)** icon next to users in the Online list is completely hidden (only the `PM` button is shown).
  - The channel header **Edit** and **Delete Channel** buttons are completely hidden.
  - Attempting to run admin slash commands (`/op`, `/kick`, `/ban`, `/addchan`, `/delchan`) returns an operator permission error (`* Error: You do not have operator privileges (+o)`).

* **Admin Authentication & PIN Protection**:
  - The client is protected with an **Admin PIN** (Default: **`4040`**).
  - If a roommate attempts to select the **Admin (House Lead / OP)** persona from the dropdown, an **Admin Authentication Modal** prompts for the PIN.
  - Without the correct PIN, access is denied and the persona reverts to a standard member.

---

## 3. Complete Command Reference

Type any command directly into the chat input bar starting with a forward slash (`/`).

### Standard User Commands

| Command | Arguments | Description | Example |
| :--- | :--- | :--- | :--- |
| `/me` | `<action>` | Broadcasts a 3rd-person action message. | `/me is cooking breakfast` |
| `/nick` | `<new_name>` | Updates your display handle across all channels. | `/nick Alex_Kitchen` |
| `/join` | `<#channel>` | Switches to the specified channel (or creates it if it does not exist). | `/join #lounge` |
| `/clear` | *None* | Clears the active channel or private message log. | `/clear` |
| `/topic` | *None* | Displays the current topic of the channel. | `/topic` |
| `/help` | *None* | Prints the list of available commands in your terminal log. | `/help` |

### Administrator / Operator Commands (`@OP` Required)

| Command | Arguments | Description | Example |
| :--- | :--- | :--- | :--- |
| `/addchan` | `<#channel> [topic]` | Creates a new channel dynamically. | `/addchan #bills Rent & utility split tracking` |
| `/delchan` | `<#channel>` | Deletes an existing channel and ejects occupants back to the Lobby. | `/delchan #bills` |
| `/topic` | `<new_topic>` | Changes and updates the active channel topic for all roommates. | `/topic Quiet hours are active until 8:00 AM` |
| `/op` | `<nick>` | Promotes a roommate to Channel Operator (`@OP`). | `/op Sam` |
| `/deop` | `<nick>` | Demotes an Operator back to standard roommate permissions. | `/deop Sam` |
| `/kick` | `<nick> [reason]` | Ejects a user from the active conversation with a reason logged to the room. | `/kick Jordan Left dirty dishes in sink` |
| `/ban` | `<nick>` | Applies a network ban, locking the target user's message input and tagging them `[BANNED]`. | `/ban Taylor` |
| `/unban` | `<nick>` | Lifts an active ban and restores full messaging capabilities. | `/unban Taylor` |

---

## 4. Visual Channel & User Management Tools

In addition to slash commands, full GUI management tools are built directly into the client for administrators:

### Channel Creation & Inline Editing
* **Add Channel**: Click **`+ Add`** in the Channels sidebar header to open the creation dialog.
* **Edit on Hover**: Hover over any channel in the sidebar and click **`✎`** to open the **Edit Channel Settings** modal (rename or update topic).
* **Delete Channel**: Click **`×`** in the sidebar or click **`Delete`** in the active channel header to remove the channel.

### User Management Modal
* In the **Online** dropdown menu, click the **`⚙`** (Gear) icon next to any roommate.
* From the **Admin Control Panel**, you can:
  * Click **Promote to @OP** / **Demote from @OP**.
  * Enter a custom kick reason and click **Kick User**.
  * Toggle **Ban User** / **Unban User**.

---

## 5. Private Messaging (Query)

* To start a 1-on-1 private chat with any roommate, click the **`PM`** button next to their name in the sidebar's **Online** dropdown.
* Private messages open in an isolated buffer labeled `Query: <Nick>`.
* Roommate simulated bot replies are room-aware and will respond naturally to private queries (e.g., asking to borrow a charger or checking if someone is awake).
