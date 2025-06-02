# 📈 Product Requirement Document (PRD)

## Project: Fixed Event Ticketing DApp

---

## 1. Objective

Develop a Web3-based Ticketing DApp for a **single, predefined event** that allows users to book and verify event tickets on-chain via NFT, while allowing an admin to manage the event lifecycle, seat status, and attendance verification.

---

## 2. Scope

### ✅ Included in Scope:

* NFT-based ticket minting for 1 fixed event
* Seat selection interface
* Wallet connection (MetaMask only)
* Attendance check-in via 6-digit OTP (non-QR)
* Admin panel for event control and verification

### ❌ Not in Scope:

* Multi-event or event creation by public users
* Multi-chain deployment
* Ticket resale / secondary market

---

## 3. Roles & Responsibilities

### 👤 User Role

* View event details
* Connect MetaMask wallet
* Select seat from visual seat picker
* Pay and mint NFT as ticket
* Generate 6-digit OTP code for check-in (valid 1 minute)
* Show code to admin for on-site validation

### 🛠️ Admin Role

* View and edit event metadata (title, location, date)
* Start/stop the event lifecycle
* View seat map with owner info and status
* Input and verify user-provided OTP
* Update seat status to "Checked"
* Withdraw ETH funds from the contract

---

## 4. Functional Requirements

### 🎫 Ticketing Logic

* Each ticket is a unique ERC721 NFT
* Minting requires exact ETH payment
* Minted ticket is linked to a selected seat
* Seat becomes locked ("Booked") upon minting

### 💼 Seat System

* All seats start as `Available`
* Once minted, seat becomes `Booked`
* After admin verifies, seat becomes `Checked`
* Only 1 seat per wallet is allowed

### 🔐 OTP Check-In

* System generates 6-digit code upon user check-in
* Code is valid for 1 minute
* One-time-use, tied to specific wallet + seat
* Stored securely off-chain (e.g. Redis or Firestore)

---

## 5. Technical Architecture

| Layer          | Technology                        |
| -------------- | --------------------------------- |
| Frontend       | Next.js, Tailwind CSS             |
| Wallet         | MetaMask (EVM-compatible)         |
| Web3 Provider  | viem or ethers.js                 |
| Smart Contract | Solidity (ERC721Enumerable)       |
| Backend        | Node.js / Firebase Functions      |
| Database       | Firestore / Redis                 |
| Storage        | IPFS / NFT.Storage (for metadata) |

---

## 6. User Flow

```plaintext
[Landing Page]
→ Connect Wallet
→ View Event Details
→ Click "Book Ticket"

[Booking Page]
→ Select Seat
→ Click "Pay & Mint"
→ NFT Ticket Minted
→ Confirmation shown

[Event Day]
→ Click "Check-in"
→ Sign message → OTP generated
→ Show OTP to Admin
```

---

## 7. Admin Flow

```plaintext
[Admin Dashboard]
→ Edit Event Info
→ Start Event

[Verification Phase]
→ View seat map
→ Input OTP from user
→ If valid → Mark seat as Checked

→ Stop Event
→ Withdraw ETH funds
```

---

## 8. Milestone To-Do List

| Milestone                                                                | Feature |
| ------------------------------------------------------------------------ | ------- |
| \[ ] **Smart Contract** – ERC721 ticketing + withdraw logic              |         |
| \[ ] **Event Metadata UI** – Admin edit for event title, date, and price |         |
| \[ ] **Seat Picker UI** – User-friendly layout with 3 status logic       |         |
| \[ ] **Minting Flow** – Payment via MetaMask + seat assignment           |         |
| \[ ] **OTP System** – User-side generation, admin-side validation        |         |
| \[ ] **Seat State Tracker** – Database record of seat status & ownership |         |
| \[ ] **Admin Verification Tool** – Input OTP, validate, update seat      |         |
| \[ ] **ETH Withdraw Panel** – Allow admin to collect event funds         |         |
| \[ ] **NFT Metadata Hosting** – IPFS integration with seat info          |         |
| \[ ] **Frontend UI** – Build full user & admin interface                 |         |

---

## 9. Success Metrics

* ✅ 100% seat tracking accuracy between frontend/backend/on-chain
* ✅ Successful NFT minting and delivery for every booked seat
* ✅ OTP codes are secure, unique, and auto-expire
* ✅ Admin flow allows real-time check-in processing without delay

---

## 10. Timeline Estimate

| Week   | Task                                     |
| ------ | ---------------------------------------- |
| Week 1 | Smart Contract + Metadata + Event Config |
| Week 2 | Booking & Seat Picker UI                 |
| Week 3 | OTP Check-in Flow + Admin Panel          |
| Week 4 | Integration Testing + Final Polish       |

---

## 11. Future Considerations

* Extend to Multi-Event via Factory Contracts
* NFT-based reward for attendees (POAP integration)
* Analytics dashboard for ticket sales
* Role-based access control for multi-admin use
