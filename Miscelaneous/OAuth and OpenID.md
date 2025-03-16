**OAuth 2.0** and **OpenID Connect (OIDC)** are related but serve different purposes in the world of authentication and authorization. Let me explain each and how they work together:

---

### **OAuth 2.0**
- **Purpose**: OAuth 2.0 is an **authorization framework** that allows third-party applications to obtain limited access to a user's resources without exposing their credentials (e.g., username and password).
- **Key Concept**: Instead of the user sharing their password with an application, they authorize the application to act on their behalf by issuing access tokens.

#### **How OAuth 2.0 Works**:
1. **Resource Owner**: The user who owns the data or resource (e.g., your Google account).
2. **Client**: The third-party application requesting access (e.g., a fitness app that wants to read your Google calendar).
3. **Authorization Server**: The server that authenticates the user and issues tokens (e.g., Google’s OAuth 2.0 system).
4. **Resource Server**: The API that hosts the user's resources (e.g., Google Calendar API).

Workflow example:
1. The user logs into the third-party app via the **Authorization Server** (e.g., "Login with Google").
2. The Authorization Server issues an **Access Token** to the app.
3. The app uses the Access Token to access the user's resources on the **Resource Server**.

Tokens in OAuth:
- **Access Token**: Grants access to the user's resources.
- **Refresh Token**: Allows the app to request a new Access Token when the old one expires.

---

### **OpenID Connect (OIDC)**
- **Purpose**: OpenID Connect is a simple **authentication layer** built on top of OAuth 2.0. It verifies the identity of the user and provides basic profile information.
- **Key Difference**: While OAuth 2.0 is about authorization (granting access to resources), OIDC is about authentication (proving the user's identity).

#### **How OIDC Works**:
1. During the OAuth 2.0 process, OIDC adds an **ID Token** (in JSON Web Token format) alongside the Access Token.
2. The **ID Token** contains information about the authenticated user, such as their name, email, and unique identifier (`sub`).

OIDC also provides a standardized way for clients to get user profile data via the **UserInfo endpoint**.

---

### **Key Differences**:
| **Feature**          | **OAuth 2.0**                   | **OpenID Connect**            |
|-----------------------|----------------------------------|--------------------------------|
| Purpose               | Authorization (access to resources) | Authentication (verify identity) |
| Tokens Used           | Access Token, Refresh Token     | Access Token, ID Token         |
| User Info             | Not provided                   | Includes identity information |
| Use Case              | API access (e.g., read/write resources) | User login (e.g., "Login with Google") |

---

### **Common Use Cases**:
- **OAuth 2.0**:
  - Grant limited access to APIs (e.g., accessing Gmail or Google Drive on behalf of a user).
  - Delegating permissions to third-party apps.

- **OIDC**:
  - Single Sign-On (SSO) solutions (e.g., "Sign in with Google").
  - Centralized identity management for web or mobile apps.

---

Together, OAuth 2.0 and OIDC provide a comprehensive framework for secure and user-friendly authentication and authorization.