# Vitest Lab

## Setup

### Installatoin

```bash
cd vitest-lab
npm install
```

### Tests

```bash
npm test

#run once
npm run test:run

#run with coverage repor
npm run test:coverage
```

## Reflection Answers

### Part 2: AAA

**Reflection Question:** Why might the Arrange-Act-Assert pattern be useful, especially for complex tests?Look at the `add` tests. The first test uses explicit Arrange-Act-Assert comments. Why might this pattern be useful, especially for complex tests?

Arrange Act Assert pattern provides clear structure that makes tests easier to read and maintain. "Arrange" part, you set up the test data and preconditions. For "Act", you execute the function being tested. For "Assert", we verify the results. For more complex tests you can use it because it clearly separates setup stuff from the actual test logic, which makes it obvious what is being tested and what the expected outcome should be. Also helps identify issues faster.

### Part 2: Seeing a Test Fail

**Questions:**
1. Which tests fail?
2. What information does Vitest provide about the failure?
3. How does this relate to "code that throws an error when actual doesn't match expected"?

When the `add` function is switched to recieve `a - b`:
1. All three `add` tests fail (adds two positive, adds negative, and adds zero)
2. the expected value, the received value, the exact line where the assertion failed, and a visual diff showing the difference
3. the `expect().toBe()` assertion internally throws an error when the actual result doesn't match the expected value, which Vitest catches and reports as a test failure

### Part 4: Unit/Integration Tests

**Reflection Questions:**
1.  The `strings.test.ts` file contains **unit tests** — they test individual functions in isolation. The `content.test.ts` file contains **integration tests** — they test how multiple units work together.
2.  If the `slugify` function had a bug, which tests would fail? (Answer: Both the unit tests in `strings.test.ts` AND the integration tests in `content.test.ts`)
3.  What additional confidence do the integration tests give you that unit tests alone wouldn't provide?

1. `strings.test.ts` contains unit tests that test individual functions (`slugify`, `truncate`, `capitalize`, `countWords`) separately. `content.test.ts` contains integration tests that test how `processArticle` and other functions work together with the string utilities.

2. If `slugify` had a bug, the unit tests in `strings.test.ts` + the integration tests in `content.test.ts` would fail.

3. Integration tests gives confidence that the units work correctly together. Unit tests verify each function works in isolation, integration tests verify that the data flows correctly between functions, the interfaces match up correctly, and combined behavior produces the results you expect.

## Additional Test Cases

1. **slugify to handle numbers in the string**
   ```typescript
   it('handles numbers in the string', () => {
     expect(slugify('Article 123 Test')).toBe('article-123-test');
   });
   ```

2. **truncate to handle empty string**
   ```typescript
   it('handles empty string', () => {
     expect(truncate('', 10)).toBe('');
   });
   ```

3. **capitalize to handle single character**
   ```typescript
   it('handles single character', () => {
     expect(capitalize('a')).toBe('A');
   });
   ```

4. **countWords: counts a single word correctly**
   ```typescript
   it('counts a single word correctly', () => {
     expect(countWords('Hello')).toBe(1);
   });
   ```

## Testing Trophy Connection

At the base, there's **static analysis** with type checking of TypeScript. It catches type errors before tests run. Above that, **unit tests** for separate utility functions. They verify each function works correctly in isolation. At the integration level, we tested the `content.ts` service which combines multiple utilities together, giving higher confidence that the pieces work together as a real application would use them. While unit tests are fast and precise, the integration tests give us the most confidence that our system actually works E2E.