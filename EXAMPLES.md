# Usage Examples

This document provides detailed examples of using the Cognitive UX Audit skills in real-world scenarios.

## Quick Start Examples

### Example 1: Post-Development Review

**Scenario**: You just finished building a new login form and want to check for UX issues.

```bash
# In your Claude Code session
/ux-review
```

**What happens**:
- Agent scans your recent frontend changes
- Identifies common cognitive friction patterns
- Reports issues with severity levels
- Suggests specific fixes

**Sample Output**:
```
## UX Review Report

### Issue 1: Password Visibility Toggle Position
**Severity:** Level 3 — Medium
**Location:** LoginForm.tsx:45

**Problem:** Password visibility toggle (eye icon) is on the left side of input
**Expected:** Most users expect this control on the right (iOS/Android pattern)
**Fix:** Move toggle to right side of input field
```

---

### Example 2: E-commerce Checkout Audit

**Scenario**: Auditing a checkout flow for a mobile-first e-commerce app.

```bash
/ux-audit
```

**Interactive Session**:

```
Agent: What is the primary user's role?
You: Mobile-first online shopper, primarily uses Instagram and Amazon apps

Agent: What platforms has your target user spent the most time on?
You: iOS, Instagram, Amazon, Shopify stores

Agent: Are there any industry-specific meanings for colors or icons?
You: Standard e-commerce - green for success, red for errors/stock issues

Agent: Any specific screens to prioritize?
You: Checkout flow - cart, shipping, payment, confirmation

Agent: I found these screens:
1. Cart.tsx - Shopping cart with item list
2. ShippingForm.tsx - Address entry
3. PaymentForm.tsx - Payment method selection
4. OrderConfirmation.tsx - Success screen
5. ProductList.tsx - Main catalog

Should I proceed with the prioritized screens (1-4)?
You: Yes

[Agent begins analysis...]
```

**Sample Report**:

```markdown
# Cognitive UX Audit Report

## Screen 1: Shopping Cart (Cart.tsx)

### User's Primary Goal
Review items and proceed to checkout

### Visual Hierarchy Analysis

| Element | Goal Relevance | Current Visual Weight | Match? |
|---------|----------------|----------------------|---------|
| Item list | Critical | High | ✓ |
| Total price | Critical | Medium | ✗ |
| "Checkout" button | Critical (Primary CTA) | High | ✓ |
| "Continue Shopping" | Secondary | High | ✗ |
| Promo code field | Supporting | High | ✗ |
| Item thumbnails | Important | Medium | ✓ |

---

### Issue 1: Competing Primary CTAs

**Severity:** Level 2 — High
**Location:** Cart.tsx:120-125

**Friction Point:** CTA Hierarchy Violation

**Problem:**
- "Checkout" and "Continue Shopping" buttons have identical styling
- Both use solid blue background, same size
- User must read text to differentiate

**Cognitive Conflict:**
- Automatic brain: Sees two equal-importance actions, pauses to decide
- Reflective brain: Must engage to read and choose

**Context Mismatch:**
User's goal is to checkout. "Continue Shopping" is a secondary, exit action.
Amazon (user's reference platform) makes checkout dominant, shopping a text link.

**Recommended Fix:**
```tsx
// Current (WRONG)
<Button variant="primary">Continue Shopping</Button>
<Button variant="primary">Checkout</Button>

// Recommended
<Button variant="text">Continue Shopping</Button>
<Button variant="primary">Checkout</Button>
```

---

### Issue 2: Buried Critical Information

**Severity:** Level 2 — High
**Location:** Cart.tsx:89

**Friction Point:** Information Hierarchy Violation

**Problem:**
Total price displayed in small gray text, below promo code field

**Cognitive Conflict:**
- User needs to verify total before committing to checkout
- Total should be visually dominant (Critical information)
- Current: Total has lower weight than promo code field (Supporting information)

**Context Mismatch:**
On Amazon/Shopify, total is bold, large, and prominently placed above checkout button.

**Recommended Fix:**
```tsx
// Move total above checkout button
// Increase font size to 24px (from 16px)
// Change color from gray (#666) to black (#000)
// Add bold weight
```

---

## Screen 2: Payment Form (PaymentForm.tsx)

### Issue 3: Stroop Conflict - Destructive Action Color

**Severity:** Level 1 — Critical
**Location:** PaymentForm.tsx:156

**Friction Point:** Color-Action Semantic Mismatch (Stroop Effect)

**Cognitive Conflict:**
- Automatic brain sees: Green button = Safe, Positive, Proceed
- Button action: "Remove Payment Method" (destructive)
- Reflective brain must override automatic impulse

**Context Mismatch:**
User's digital habitat (iOS, Instagram, Amazon) consistently uses:
- Green for positive, safe actions (Add, Save, Confirm)
- Red or gray for destructive/removal actions

**Risk:** User may accidentally delete payment method thinking they're saving it

**Recommended Fix:**
```tsx
// Current (DANGEROUS)
<Button color="success" onClick={removePaymentMethod}>
  Remove Payment Method
</Button>

// Recommended
<Button variant="text" color="destructive" onClick={removePaymentMethod}>
  Remove Payment Method
</Button>
// Also add confirmation dialog
```
```

---

### Example 3: Enterprise Dashboard Audit

**Scenario**: SaaS analytics dashboard for data analysts.

```bash
/ux-audit
```

**Session**:
```
Agent: What is the primary user's role?
You: Data analyst at enterprise companies

Agent: What platforms has your target user spent the most time on?
You: Excel, Tableau, Google Analytics, Jira

Agent: Industry-specific color meanings?
You: Red often means below-target/negative, green means above-target/positive
In our domain, these are performance indicators, not errors

Agent: Focus areas?
You: Main analytics dashboard

[Analysis begins...]
```

**Sample Finding**:
```markdown
### Issue: Domain Semantic Violation

**Severity:** Level 2 — High
**Location:** MetricsCard.tsx:67

**Friction Point:** Prior Knowledge Mismatch

**Problem:**
Revenue decrease shown with green color and downward arrow

**Cognitive Conflict:**
- User's domain model: Green = good performance, red = poor performance
- System shows: Revenue down 12% in green with ✓ icon
- User must override automatic interpretation (green = good) to understand this is actually bad

**Context Mismatch:**
In Tableau/Excel (user's habitat), downward trends in revenue are ALWAYS red.
Your users spent years building this mental model.

**Recommended Fix:**
```tsx
// Use semantic coloring based on metric context
const trendColor = metric.isPositive
  ? 'success'  // Green for improvements
  : 'error'    // Red for declines

// For revenue: decrease = negative = red
// For costs: decrease = positive = green
```
```

---

## Advanced Usage Patterns

### Pattern 1: Focused Component Audit

Audit a specific component in isolation:

```bash
/ux-audit

# When asked about focus areas:
> Only audit the NavigationBar.tsx component
```

### Pattern 2: Multi-Persona Audit

Audit the same interface for different user types:

```bash
# First audit
/ux-audit
> Primary user: Beginner user, first-time app users

# Second audit
/ux-audit
> Primary user: Power user, IT professionals
```

This helps identify if your interface tries to serve conflicting mental models.

### Pattern 3: Platform-Specific Review

```bash
/ux-audit

> Digital habitat: Exclusively Windows desktop, Microsoft Office suite
> Focus: Keyboard navigation and shortcuts
```

Ensures your web app respects Windows conventions vs. Mac conventions.

---

## Common Issues Found

### Visual Hierarchy Issues

1. **CTA Overload**
   - Problem: 3+ primary-styled buttons on one screen
   - Common in: Settings pages, forms with multiple submit options
   - Fix: Keep 1-2 primary CTAs max

2. **Buried Primary Action**
   - Problem: Main action styled as secondary or text link
   - Common in: Confirmation modals, multi-step forms
   - Fix: Make the goal-completing action visually dominant

3. **Information-Weight Mismatch**
   - Problem: Critical data smaller/lighter than peripheral info
   - Common in: Dashboards, data tables
   - Fix: Size/contrast proportional to user's goal relevance

### Stroop Conflicts

1. **Destructive Green Buttons**
   - Action: Delete, Remove, Unsubscribe
   - Color: Green, blue (positive associations)
   - Fix: Use red outline or text-only destructive styling

2. **Positive Red Indicators**
   - Info: Success message, completion status
   - Color: Red (automatic error association)
   - Fix: Use green, blue, or neutral colors for positive states

3. **Icon Semantic Misuse**
   - Problem: Heart icon for "Save" instead of "Like"
   - Problem: Plus icon for "Expand" instead of "Add"
   - Fix: Use globally-recognized icon meanings

### Platform Convention Breaks

1. **Button Order Reversal**
   - Windows: [Cancel] [OK]
   - Mac: [OK] [Cancel]
   - Mobile: Primary at bottom
   - Fix: Match user's declared platform

2. **Navigation Placement**
   - Problem: Hamburger menu on right (contradicts 95% of mobile apps)
   - Fix: Left-side navigation on mobile

---

## Tips for Better Audits

### 1. Be Specific About User Background
```
❌ Bad: "General consumers"
✓ Good: "Mobile-first shoppers, primarily use Instagram/TikTok, age 18-35"
```

### 2. Mention Competing Apps
```
❌ Bad: "Uses social media"
✓ Good: "Daily Instagram/TikTok user, expects swipe gestures and bottom navigation"
```

### 3. Clarify Domain-Specific Meanings
```
❌ Bad: "Finance app"
✓ Good: "Stock trading app - in this domain, red numbers mean positive (gains),
green means negative (losses) - opposite of typical UX conventions"
```

### 4. Prioritize High-Traffic Flows
```
✓ Good: "Focus on: Login → Dashboard → Create Report (our main user journey)"
```

---

## Interpreting Severity Levels

### Level 1 (Critical) - Fix Immediately
- **Characteristics**: Stroop conflicts, potential data loss
- **Timeline**: Before next deployment
- **Example**: Green "Delete All Data" button

### Level 2 (High) - Fix Soon
- **Characteristics**: Domain mismatches, confused primary CTAs
- **Timeline**: Within current sprint
- **Example**: 3 primary-styled buttons on checkout page

### Level 3 (Medium) - Plan to Fix
- **Characteristics**: Platform convention breaks
- **Timeline**: Next major update
- **Example**: Windows app with Mac-style button order

### Level 4 (Low) - Nice to Have
- **Characteristics**: Minor optimizations
- **Timeline**: When capacity allows
- **Example**: Inconsistent button corner radius

---

## Integration with Development Workflow

### During Feature Planning
```bash
# Before coding
/ux-audit
> Focus: Wireframes and mockups for new checkout flow
```

### During Development
```bash
# Quick checks while coding
/ux-review
```

### Before PR/Deployment
```bash
# Full audit before merging
/ux-audit
> Focus: All changed screens
```

### Post-Launch Validation
```bash
/ux-audit
> Persona: Real user feedback (based on support tickets)
```
