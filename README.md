# Avtoikonom - Cypress E2E Testing Suite

Automated end-to-end testing suite for the Avtoikonom admin platform built with Cypress.

## Project Overview

This project contains automated tests for the Avtoikonom partner management system, including partner creation, login workflows, and file uploads.

**Base URL:** `https://dev.admin.avtoikonom.com`

## Tech Stack

- **Cypress** - E2E testing framework
- **JavaScript/ES6** - Test scripting
- **Faker.js** - Test data generation
- **Page Object Model** - Test structure pattern

## Project Structure

```
cypress/
├── e2e/                 # Test specifications
│   └── CreatePartner.cy.js
├── pages/               # Page Object Model classes
│   ├── BasePage.js
│   ├── LoginPage.js
│   └── PartnersPage.js
├── fixtures/            # Test data and images
│   ├── test-image.js
│   └── test-image.png
├── support/             # Helper files and commands
│   ├── e2e.js
│   └── commands.js
└── cypress.config.js    # Cypress configuration
```

## Setup

1. **Install dependencies:**
   ```bash
   npm install
   ```

2. **Configure credentials:**
   - Update `cypress.config.js` with test credentials in the `env` section
   - Current test user: `test_qa@example.com`

## Running Tests

```bash
# Open Cypress Test Runner
npx cypress open

# Run all tests headlessly
npx cypress run

# Run specific test
npx cypress run --spec "cypress/e2e/CreatePartner.cy.js"
```

## Test Cases

### Create Partner Test
- **File:** `cypress/e2e/CreatePartner.cy.js`
- **What it does:**
  1. Logs in with valid credentials
  2. Navigates to Partners section
  3. Creates a new partner with:
     - Auto-generated partner name
     - Partner type (Service)
     - Selected services
     - Subscription tier
     - Address (with Google Places autocomplete)
     - Phone number
     - Contact person
     - Description
     - Logo upload (test-image.png)
     - Clicks "Save" after the logo is uploaded
     - Clicks "Save" to save the newly created Partner
     

## Dependencies

- `@faker-js/faker` - Generates random test data
- `cypress-file-upload` - File upload handling
- `cypress-xpath` - XPath selector support
- `cypress-iframe` - iframe handling

## Known Issues & Debugging

### Image Upload
If image upload fails:
1. Ensure `cypress/fixtures/test-image.png` exists
2. If file input is in an iframe, use:
   ```javascript
   cy.frameLoaded()
   cy.iframe().find('input[type="file"]').selectFile('fixtures/test-image.png')
   ```
3. Check selector with `cy.get('input[type="file"]').debug()`

## Environment Variables

Located in `cypress.config.js`:
- `username` - Test login email
- `password` - Test login password

## CI/CD Integration

- **Cypress Cloud Project ID:** `ioif8v`
- MCP Server configured for Cypress Cloud integration (requires `CYPRESS_MCP_TOKEN`)
