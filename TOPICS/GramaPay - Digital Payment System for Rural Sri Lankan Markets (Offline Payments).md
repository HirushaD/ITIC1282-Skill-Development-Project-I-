The key idea was:
- QR-code-based offline payment system
- Vendors and customers settle transactions without internet
- Uses batched, store-and-forward sync when connectivity returns

## The Core Problem It Solves  
In rural Sri Lankan markets (Peliyagoda fish market, Kandy wholesale market, Dambulla economic centre):  
- Vendors and customers **cannot rely on mobile data** - it's slow, drops during peak hours, and costs money  
- **Friction payment** (cash counting, fake note detection, change giving) causes hours of lost time daily  
- Digital payment apps (f-pay, mobile wallets) **require internet** - the vendor's phone needs data to receive, and so does the customer  
- The vendor has **no record** of transactions beyond cash in hand - no sales history, no daily totals, no accounting  
GramaPay solves all four problems by making transactions **internationally asynchronous**.

## How It Works - The Core Innovation  
The key insight: **internet is only needed to reconcile, not to transact.**

```
CUSTOMER SCANS VENDOR QR
         ↓
  [Customer App]
  
  Creates transaction record locally:
	  {
    vendor_id: "V_001",
    amount: 450,
    currency: "LKR",
    timestamp: 2025-07-03T14:32:00,
    tx_hash: SHA256(vendor_id + amount + timestamp + secret_key)
	  }
         ↓
  [Customer App] → stores in local queue (no internet needed)
  [Customer App] → displays "Payment Sent ✓" to vendor
         ↓
  [Vendor App] ← shows "Received ✓ — Rs. 450" (no internet needed)
         ↓
  LATER... when either phone has data:
         ↓
  [Sync Server] ← receives batched transactions from both sides
  [Sync Server] ← reconciles: did customer send, did vendor receive?
  [Sync Server] → confirms or disputes
```

 **both phones are independent ledgers**. As long as they eventually sync, the books balance. This is essentially how blockchain double-entry works - but simpler and without the blockchain.

## The Technical Architecture
```
┌──────────────────────────────────────────────────────┐
│                  GRAMAPAY SYSTEM                     │
│                                                      │
│  ┌──────────────┐       ┌──────────────────────────┐ │
│  │ Customer App │       │      Vendor App          │ │
│  │   (Android)  │       │       (Android)          │ │
│  │              │       │                          │ │
│  │ • QR Scanner │       │ • QR Generator           │ │
│  │ • Amount     │       │ • Amount Entry           │ │
│  │   Entry      │       │ • Daily Sales View       │ │
│  │ • TX Queue   │       │ • TX Queue               │ │
│  │ • Sync       │       │ • Settlement History     │ │
│  │   Manager    │       │ • Sync Manager           │ │
│  └──────┬───────┘       └────────────┬─────────────┘ │
│         │                            │               │
│         │     [Periodic Sync]        │               │
│         └──────────┐  ┌──────────────┘               │
│                     ▼                                │
│         ┌───────────────────────┐                    │
│         │    Sync Server        │                    │
│         │   (Flask/Node.js)     │                    │
│         │                       │                    │
│         │ • Conflict Resolution │                    │
│         │ • Double-entry Check  │                    │
│         │ • Settlement Engine   │                    │
│         │ • Vendor Commission   │                    │
│         │   Calculator          │                    │
│         └───────────┬───────────┘                    │
│                     │                                │
│         ┌───────────▼───────────┐                    │
│         │      SQLite DB        │                    │
│         │  (Transaction Ledger) │                    │
│         └───────────────────────┘                    │
└──────────────────────────────────────────────────────┘
```

# Full Assignment  
##  Student 1: QR System & Transaction Security  
**Owns:** The trust layer - how a QR code carries enough information to be trustworthy, and how transactions are secured.  
**What they build:**  
1.**QR Code Generation (Vendor Side)**  
- Vendor's phone generates a **dynamic QR code** containing:  
- Vendor ID (unique, assigned at registration)  
- Merchant name (display name)  
- Current timestamp (Unix epoch, prevents replay attacks)  
- A HMAC-SHA256 signature of the above using the vendor's secret key  
- Format: `gramapay://pay?vendor=V001&time=1719912345&sig=abc123...`  
- Encode this as a QR code using **ZXing** library  
- QR refreshes every 60 seconds (prevents screenshot fraud)  
2.**QR Code Scanner (Customer Side)**  
- Customer scans vendor's QR code  
- App parses the URL, extracts vendor ID, timestamp, signature  
- Validates HMAC signature using the **vendor's public key** (registered at server)  
- Checks timestamp is within ±5 minutes (prevents old QR reuse)  
3.**Transaction Signing**  
- Once amount is entered, customer signs the full transaction:  
- `tx_data = vendor_id + customer_id + amount + timestamp`  
- `customer_signature = HMAC-SHA256(tx_data, customer_secret_key)`  
- Transaction stored locally in SQLite queue  
4.**Fraud Prevention**  
- Duplicate transaction detection (same tx_hash cannot be used twice)  
- Amount tampering prevention (signature covers amount)  
- Vendor impersonation prevention (server validates vendor key)  

**Deliverable:** A working QR payment flow between two Android devices — customer scans vendor QR, enters amount, confirms, and both phones show the transaction locally without internet.