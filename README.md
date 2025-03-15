# JEST tutorial for test-driven development
Learn how to write unit tests and other kinds of tests

# Setup

Install dependencies

`$ npm install`

Run tests

`$ NODE_ENV=test npx jest /path/to/test/file`

Run coverage

`$ NODE_ENV=test npx jest --coverage /path/to/test/file`

View coverage report in `coverage/lcov-report/index.html`

The followung database scripts are not necessary. If you still need
them for manual testing here they are:

`$ npx ts-node insert_sample_data.ts "mongodb://127.0.0.1:27017/my_library_db"`

Clean the database

`npx ts-node remove_db.ts "mongodb://127.0.0.1:27017/my_library_db"`

# Description

This repository illustrates how to use jest to write unit tests 
for a server in typescript. The examples are as follows:

- `tests/authorSchema.test.ts`: Unit tests to verify the schema of the authors colletion. 
- `tests/bookDetailsService.test.ts`: Unit tests to verify the behavior of the service that is used to retrieve the details of a particular book.
- `tests/createBookService.test.ts`: Unit tests to verify if a book is created successfully.

# For you to do

## Part 1

Write a unit test for the GET /authors service. 
The service should respond with a list of author names and lifetimes sorted by family name of the authors. It should respond
with a "No authors found" message when there are no authors in the database. If an error occurs when retrieving the authors then the
service responds with an error code of 500. The unit test
should be placed in `tests/authorService.test.ts`.

## Part 2

Briefly explain a limitation of the tests in `tests/authorSchema.test.ts` in the space below.

tests/authorSchema.test.ts primarily focus on validation constraints (e.g., required fields, maximum length) but do not test schema behaviors:

Here's an example:
* The tests use validateSync() instead of actually saving to MongoDB, so they do not check how the schema behaves when stored in a real database.
* If the schema includes default values or virtual fields, the tests do not validate their correctness.
* It does not test for duplicate authors.
* The tests do not cover scenarios like partial updates, invalid date ranges (e.g., date_of_death before date_of_birth), or optional fields being null.

## Part 3

Generate the coverage report for the tests you wrote. How can you improve
your tests using the coverage report? Briefly explain your 
process in the space below.

1. Add more tests related to branches[that check different paths in conditional logic] (5.71%) and functions[If schema methods exist (e.g., pre-save hooks or virtual properties), write tests that verify their behavior.] (5.88%).

2. Using the report to find untested parts of the `authorSchema` model, focusing on edge cases in validation, optional fields, and interactions with the database.

3. Instead of just `validateSync()`, attempt to save documents to MongoDB and verify the expected behavior.

4. After adding new test cases, generate a new coverage report to see improvements and ensure all critical logic is tested.