# Windsor Circle Front End Code Review Process

## Terminology

For clarity, the developer who wrote the code will be referred to as `the developer` and the developer reviewing the code will be referred to as `the reviewer`

## Process

- Code Review should happen for every major change before it is merged into the main dev branch
- Code Review should be cycled so that different developers are reviewing each developers code over time

## Accountability

- Code Review may reveal issues that are not a direct result of the current code changes.  Regardless of original authorship, the developer is responsible for making sure that all issues found in code review are either resolved or documented as separate bugs.  This includes functional, stylistic, documentation and testing concerns.
- Reviewers are encouraged to be curious and view their task as part of improving the application.  Developers are encouraged to avoid being defensive and instead focus on pragmatically doing their best to improve the codebase through the review process.

## Checklist

The following things should be checked for each code review.  Feel free to explicitly go through this list, or use it as a guideline, but a reviewer is responsible for each of these areas.

- Is the purpose of this change documented in Trello?
    - Is it clear what has changed
    - Does the scope of the code change match what is in Trello.  If its larger, is discussion required?
- Does the code work as expected?
    - Code review is not "testing" but should include a basic sanity check that the code does something like what is expected
- Does the code match Windsor Circle Style guidelines?
    - Code should pass jsHint and JSCS without any warnings
    - In addition to meeting the written style guidelines, is this code "in the spirit" of the rest of the codebase?
    - When in doubt the Style Guide should be considered authoratative.  If that raises disagreement, it should be a question of changing the style guide, not bypassing it.
- Is the code properly tested
    - Code written in ES6 style should have complete unit tests that cover all important behaviors (but not enforce code structure)
    - If this code is a bug fix it is especially important that it include a test to prevent regressions
    - All code changes should include instructions in the Trello card detailing the expected behavior that requires testing, as well as any special steps required to test it, or any known edge cases that occured during development
- Is the code clear to read?
    - If it is not easy to understand the code, it is appropriate to suggest comments or code changes as appropriate to make the meaning clear
    - If there are comments, check to make sure that they're still relevant and up to date with the current state of the code
- Does the code contain errors?
    - These can be explicit logic errors, or errors of omission (a variable was removed but the code still references it)
- Does this code make assumptions that are likely to change?
- What did the developer do well?  Tell them.
