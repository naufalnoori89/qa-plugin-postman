# Postman Plugin for AI QA Agent

This plugin enables Postman/Newman test automation through the AI QA Agent.

## Overview

The Postman plugin provides:
- API test automation using Postman collections
- Newman command-line test execution
- Environment-based configuration (dev, qa)
- Test result analysis
- Integration with Postman Echo for testing

## Framework

- **Framework**: Newman (Postman CLI)
- **Runtime**: Node.js 22+
- **Execution**: Jenkins
- **Test Endpoint**: Postman Echo (https://postman-echo.com)

## Capabilities

1. **discover_suites** - List available Postman collections
2. **create_tests** - Create new API tests
3. **modify_tests** - Modify existing collections
4. **run_tests** - Execute tests via Newman
5. **analyze_results** - Analyze Newman test results

## Directory Structure

```
qa-plugin-postman/
├── plugin.yaml          # Plugin manifest
├── README.md            # This file
├── package.json         # Node dependencies
├── collections/         # Postman collections
├── environments/        # Environment configurations
│   ├── dev/            # Development environment
│   └── qa/             # QA environment
├── knowledge/          # Plugin documentation for RAG
├── schemas/            # JSON schemas
├── templates/          # Test templates
└── scripts/            # Helper scripts
```

## Available Collections

### 1. Industry Standard Tests

Industry-standard API test collection using **Postman Echo**:

#### What is Postman Echo?

Postman Echo is a service provided by Postman that echoes back any data you send to it. Perfect for testing API requests without needing a real backend.

- **Base URL**: https://postman-echo.com
- **Purpose**: Testing and validation
- **Response**: Echoes back request details

#### Included Tests:

**1. GET Request** - Retrieve Data
- Validates 200 OK status
- Checks response time < 2000ms
- Validates JSON response
- Verifies query parameters are echoed
- Confirms headers are returned

**2. POST Request** - Create Data
- Validates 200 OK status
- Confirms data is echoed back
- Validates request body
- Checks Content-Type header
- Verifies posted JSON structure

**3. DELETE Request** - Remove Data
- Validates 200 OK status
- Checks response time
- Validates JSON response
- Confirms request URL
- Verifies headers

**BONUS: PUT Request** - Update Data
- Validates 200 OK status
- Confirms updated data is echoed
- Validates request structure

## Usage

### List Collections

```
User: "What Postman test suites are available?"
```

### Run Tests

```
User: "Run the industry standard tests in QA environment"
```

### Create Tests

```
User: "Create a Postman test for the login API endpoint"
```

## Postman Echo Endpoints

The collection uses these Postman Echo endpoints:

| Method | Endpoint | Purpose |
|--------|----------|---------|
| GET | /get | Echo GET requests with query params |
| POST | /post | Echo POST requests with body |
| PUT | /put | Echo PUT requests with body |
| DELETE | /delete | Echo DELETE requests |

## Environments

### Development (dev)
- Base URL: https://postman-echo.com
- Timeout: 5000ms
- Use for local testing

### QA (qa)
- Base URL: https://postman-echo.com
- Timeout: 10000ms
- Use for QA validation

## Test Standards

All Postman collections follow industry best practices:
- Clear test descriptions
- Comprehensive assertions
- Response time validation
- JSON structure validation
- Proper error handling
- Environment variable usage

## Running Tests Locally

### Prerequisites
```bash
npm install
```

### Run with Newman
```bash
# Run the industry standard tests
newman run collections/industry-standard-tests.json

# Run with environment
newman run collections/industry-standard-tests.json \
  -e environments/dev/environment.json

# Run with detailed output
newman run collections/industry-standard-tests.json --reporters cli,json
```

## Example Test Results

When you run the industry standard tests, you should see:

```
Industry Standard API Tests

→ GET - Retrieve Data
  ✓ Status code is 200
  ✓ Response time is less than 2000ms
  ✓ Response has valid JSON
  ✓ Response contains args object
  ✓ Query parameters are echoed correctly
  ✓ Response contains headers object

→ POST - Create Data
  ✓ Status code is 200
  ✓ Response has valid JSON
  ✓ Posted data is echoed back
  ✓ Request body data is correct
  ✓ Content-Type header is present
  ✓ Response contains request URL

→ DELETE - Remove Data
  ✓ Status code is 200
  ✓ Response time is less than 2000ms
  ✓ Response has valid JSON
  ✓ Delete request URL is correct
  ✓ Request headers are echoed
  ✓ No error in response
```

## Why Postman Echo?

✅ **Always Available** - No setup required
✅ **No Authentication** - Perfect for testing
✅ **Predictable** - Always returns same structure
✅ **Fast** - Quick response times
✅ **Reliable** - Maintained by Postman
✅ **Safe** - No side effects, data is not stored

## Version

Current version: 1.0.0
Testing endpoint: Postman Echo (https://postman-echo.com)
