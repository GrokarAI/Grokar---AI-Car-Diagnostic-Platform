# Privacy Policy

**Effective Date:** January 2025  
**Last Updated:** December 2025

---

## 1. Introduction

Grokar ("we," "our," or "the Platform") is committed to protecting user privacy. This Privacy Policy outlines our data practices, technical architecture decisions, and the measures we implement to ensure your automotive data remains private and secure.

This document is intended for both end-users and technical stakeholders who wish to understand our privacy-first approach.

---

## 2. Executive Summary

| Category | Our Approach |
|----------|--------------|
| Personal Data Collection | None |
| Data Storage | Client-side only |
| Server Persistence | Stateless |
| Third-Party Sharing | None |
| Tracking & Analytics | None |
| User Accounts | Not required |

---

## 3. Data Collection Practices

### 3.1 Data We Do NOT Collect

- **Personal Identifiable Information (PII):** No names, emails, phone numbers, or addresses
- **Authentication Credentials:** No user accounts, passwords, or OAuth tokens stored
- **Vehicle Identification Numbers (VINs):** Processed transiently, never persisted
- **Conversation Logs:** Chat sessions exist in-memory only during active use
- **IP Addresses:** Not logged or stored for any purpose
- **Device Fingerprints:** No browser or device fingerprinting implemented
- **Behavioral Analytics:** No tracking pixels, heatmaps, or session recordings

### 3.2 Transient Data Processing

During active sessions, the following data is processed **in-memory only**:

| Data Type | Purpose | Retention |
|-----------|---------|-----------|
| VIN Numbers | Vehicle identification via NHTSA API | Duration of request only |
| Chat Messages | AI response generation | Session duration only |
| Uploaded Images | OCR/Vision processing | Immediate processing, then discarded |
| Location Data | Mechanic finder feature | Never transmitted to servers |

---

## 4. Technical Architecture

### 4.1 Stateless Backend Design

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   Client App    │────▶│  Stateless API  │────▶│  External APIs  │
│  (Browser/PWA)  │◀────│   (No Storage)  │◀────│  (NHTSA, Grok)  │
└─────────────────┘     └─────────────────┘     └─────────────────┘
        │
        ▼
┌─────────────────┐
│  Local Storage  │
│  (User Device)  │
└─────────────────┘
```

**Key Architectural Decisions:**

1. **No Database Persistence for User Data:** Backend operates statelessly with no user data written to disk
2. **Client-Side Storage:** All persistent data (saved vehicles, service history) stored in browser localStorage
3. **Pass-Through API Design:** Server acts as a secure proxy to external services without logging requests
4. **Session Isolation:** Each browser session is independent with no cross-session data sharing

### 4.2 Data Flow Architecture

```
User Input ──▶ Client Validation ──▶ Encrypted Transit (HTTPS) ──▶ API Processing ──▶ Response
                                                                          │
                                                                          ▼
                                                              No Logging / No Storage
```

### 4.3 Local Storage Schema

Data persisted on the user's device only:

```typescript
interface LocalStorageSchema {
  savedVehicles: Vehicle[];      // User's garage
  serviceHistory: ServiceRecord[]; // Maintenance logs
  themePreference: 'light' | 'dark';
  sessionId: string;             // Temporary session identifier
}
```

**Important:** This data is stored exclusively in the user's browser and is never transmitted to our servers.

---

## 5. Third-Party Services

### 5.1 NHTSA (National Highway Traffic Safety Administration)

| Aspect | Details |
|--------|---------|
| Service | VIN Decoding & Recall Lookup |
| Data Sent | VIN number only |
| Data Received | Vehicle specifications, recall information |
| Privacy Policy | [NHTSA Privacy Policy](https://www.nhtsa.gov/privacy-policy) |
| Our Logging | None |

### 5.2 AI Services (Grok via OpenRouter)

| Aspect | Details |
|--------|---------|
| Service | Conversational AI & Image Analysis |
| Data Sent | User queries, uploaded images (base64) |
| Data Received | AI-generated responses |
| Our Logging | None |
| Retention | Governed by OpenRouter's policies |

**Note:** We recommend reviewing [OpenRouter's Privacy Policy](https://openrouter.ai/privacy) for details on their data handling practices.

---

## 6. Security Measures

### 6.1 Transport Security

- **TLS 1.3:** All communications encrypted in transit
- **HTTPS Only:** HTTP requests automatically redirected
- **HSTS:** HTTP Strict Transport Security headers implemented

### 6.2 Application Security

- **No Server-Side User Data:** Attack surface minimized by design
- **Input Validation:** All user inputs validated and sanitized
- **API Key Protection:** Third-party credentials stored server-side only, never exposed to clients
- **Content Security Policy:** CSP headers prevent XSS attacks

### 6.3 Client-Side Security

- **LocalStorage Isolation:** Browser same-origin policy protects stored data
- **No Sensitive Data in URLs:** Query parameters do not contain PII
- **Secure Context Required:** Features require HTTPS context

---

## 7. User Rights & Controls

### 7.1 Your Rights

| Right | Implementation |
|-------|----------------|
| Right to Access | All your data is in your browser's localStorage |
| Right to Deletion | Clear browser data or use in-app delete functions |
| Right to Portability | Export feature available for saved vehicles |
| Right to Restriction | No server-side data to restrict |
| Right to Object | No processing to object to |

### 7.2 Data Deletion

To remove all locally stored data:

**Option 1:** Use browser settings
- Chrome: Settings > Privacy > Clear browsing data > Cookies and site data

**Option 2:** In-app controls
- Garage: Delete individual vehicles
- Service History: Remove individual records

**Option 3:** Complete reset
- Browser Developer Tools > Application > Local Storage > Clear

---

## 8. Cookies & Tracking

### 8.1 Cookie Usage

| Cookie Type | Used? | Purpose |
|-------------|-------|---------|
| Essential/Session | Minimal | Session management only |
| Analytics | No | - |
| Advertising | No | - |
| Third-Party | No | - |

### 8.2 Tracking Technologies

We do **NOT** implement:
- Google Analytics or similar services
- Facebook Pixel or social tracking
- Advertising networks
- User behavior analytics
- A/B testing frameworks that track users
- Crash reporting with user identification

---

## 9. Children's Privacy

Grokar does not knowingly collect any information from children under 13 years of age. The service is intended for vehicle owners and automotive enthusiasts.

---

## 10. International Users

This service operates globally. Data processing occurs transiently through our servers but no personal data is stored, eliminating typical cross-border data transfer concerns.

---

## 11. Changes to This Policy

We reserve the right to update this Privacy Policy. Changes will be reflected in the "Last Updated" date. Significant changes will be communicated through:
- GitHub repository changelog
- In-app notification (if applicable)

---

## 12. Contact Information

For privacy-related inquiries:
- **GitHub Issues:** Open an issue in our repository
- **Security Concerns:** Report via GitHub Security Advisory

---

## 13. Compliance Statement

Our privacy practices align with the principles of:
- **GDPR** (General Data Protection Regulation)
- **CCPA** (California Consumer Privacy Act)
- **Privacy by Design** framework

While minimal data processing means many regulations have limited applicability, we maintain high standards as a matter of principle.

---

<div align="center">

**Our Philosophy**

*We built Grokar to help car owners, not to harvest their data.  
The best way to protect user data is to never collect it in the first place.*

</div>
