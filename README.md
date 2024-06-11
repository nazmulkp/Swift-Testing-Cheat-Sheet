# Swift Testing Cheat Sheet

A comprehensive guide to help you get started with Swift Testing. This cheat sheet covers basic syntax, assertions, setup and teardown, parameterized tests, asynchronous testing, performance testing, grouping tests, avoiding redundancies, and a comparison with XCTest.

## Table of Contents

1. [Basic Syntax](#1-basic-syntax)
2. [Assertions](#2-assertions)
3. [Setup and Teardown](#3-setup-and-teardown)
4. [Parameterized Tests](#4-parameterized-tests)
5. [Asynchronous Testing](#5-asynchronous-testing)
6. [Performance Testing](#6-performance-testing)
7. [Grouping Tests](#7-grouping-tests)
8. [Avoiding Redundancies](#8-avoiding-redundancies)
9. [Comparison with XCTest](#9-comparison-with-xctest)
10. [Migrating from XCTest to Swift Testing](#10-Migrating-from-XCTest-to-Swift-Testing)


## 1. Basic Syntax

**Define a Test Suite:**
``` swift
@Suite
struct MyTestSuite {
    // Test cases go here
}
```
**Define a Test Case:**

``` swift
@Test
func myTestCase() throws {
    // Test logic goes here
    expect(1 + 1 == 2)
}
```

## 2. Assertions
**Basic Assertions:**
``` swift
expect(x == y)  // Check for equality
expect(x != y)  // Check for inequality
expect(x > y)   // Check greater than
expect(x >= y)  // Check greater than or equal
expect(x < y)   // Check less than
expect(x <= y)  // Check less than or equal
```

**Nil Checks:**
``` swift
expect(x == nil)    // Check if nil
expect(x != nil)    // Check if not nil

```

**Boolean Checks:**
``` swift
expect(condition)  // Check if true
```

## 3. Setup and Teardown
**Setup before each test:**
``` swift
@Suite
struct MyTestSuite {
    init() async throws {
        // Setup code
    }

    @Test
    func myTestCase() throws {
        // Test logic
    }
}

```

**Teardown after each test::**
``` swift
@Suite
struct MyTestSuite {
    deinit {
        // Teardown code
    }

    @Test
    func myTestCase() throws {
        // Test logic
    }
}
```

## 4. Parameterized Tests
**Define Parameterized Test:**
``` swift
@ParameterizedTest
@Test
func addition(_ a: Int, _ b: Int, _ expected: Int) {
    expect(a + b == expected)
}

// Calling the parameterized test
addition(1, 1, 2)
addition(2, 2, 4)
```

## 5. Asynchronous Testing
**:**
``` swift
@Test
func testAsyncFunction() async throws {
    let result = try await asyncFunction()
    expect(result == expectedValue)
}
```

**Using ```#require``` for Immediate Assertion Failure:**
``` swift
@Test
func myTestCase() throws {
    try #require(x == y)
    #expect(z.isEnabled)
}
```

## 6. Performance Testing
**Measure Performance:**
``` swift
@PerformanceTest
func testPerformance() throws {
    measure {
        // Code to measure
    }
}
```

## 7. Grouping Tests
**Nested Test Suites:**
``` swift
@Suite
struct ParentSuite {
    @Suite
    struct ChildSuite {
        @Test
        func childTest() throws {
            expect(true)
        }
    }

    @Test
    func parentTest() throws {
        expect(true)
    }
}
```

## 8. Avoiding Redundancies
**Remove Redundant `test` Prefix:**
``` swift
@Test
func example() throws {
    expect(true)
}
```

## 9. Comparison with XCTest
![Screenshot 2024-06-11 at 6 51 18 PM](https://github.com/nazmulkp/Swift-Testing-Cheat-Sheet/assets/8841075/431c90b0-1922-4af9-8ca1-a3d7d2cb973b)

## 9. Migrating from XCTest to Swift Testing
**Supported Functionality:**

Use UI automation APIs (e.g., XCUIApplication).
Use performance testing APIs (e.g., XCTMetric).
Continue using Objective-C only tests with XCTest.
Avoid using XCTAssert(...) from Swift Testing tests, use #expect(...) instead.

**Recommended Practices:**
Share a single unit test target.
Swift Testing tests can coexist with XCTest.
Consolidate similar XCTest cases into parameterized tests.
Migrate XCTest classes with a single test method to a global @Test function.
Remove redundant test prefixes from method names.

