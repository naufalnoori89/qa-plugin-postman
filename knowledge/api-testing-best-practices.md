# API Testing Best Practices

## Overview

This document outlines best practices for API testing using Postman/Newman.

## Test Structure

### 1. Request Organization
- Group related requests in folders
- Use descriptive names for requests
- Include request descriptions
- Order requests logically

### 2. Test Assertions

**Status Code Validation:**
```javascript
pm.test('Status code is 200', function () {
    pm.response.to.have.status(200);
});
```

**Response Time:**
```javascript
pm.test('Response time is less than 500ms', function () {
    pm.expect(pm.response.responseTime).to.be.below(500);
});
```

**JSON Schema Validation:**
```javascript
pm.test('Response has valid structure', function () {
    pm.expect(jsonData).to.have.property('id');
    pm.expect(jsonData).to.have.property('name');
});
```

### 3. Environment Variables

Use environment variables for:
- Base URLs
- API keys
- Test data
- Configuration values

### 4. Pre-request Scripts

Use for:
- Data setup
- Token generation
- Dynamic variables
- Request preparation

### 5. Test Scripts

Always validate:
- Status codes
- Response times
- Response structure
- Data correctness
- Error handling

## Industry Standards

### GET Requests
- Verify 200 OK status
- Check response structure
- Validate data types
- Ensure performance

### POST Requests
- Verify 201 Created status
- Check created resource
- Validate location header
- Confirm data persistence

### DELETE Requests
- Verify 204 No Content or 200 OK
- Confirm deletion
- Check error handling
- Validate cleanup

## Common Patterns

### Authentication
- Store tokens in environment
- Refresh tokens as needed
- Handle expired tokens

### Data Validation
- Check required fields
- Validate data types
- Verify constraints
- Test edge cases

### Error Handling
- Test invalid inputs
- Verify error messages
- Check status codes
- Validate error structure
