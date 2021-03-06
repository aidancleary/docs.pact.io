---
title: Question archive
---

Some less commonly, but no less importantly, asked questions.

## My team wants to run the application inside docker as they feel that running it inside a docker with http server is much more realistic scenario in line with production.

Contract testing is not about providing a realistic situation. It's about testing your requests and responses in focussed way, isolating the application under test from causes of failure that are unrelated to the contents of the requests and responses \(eg. networking issues, deployment problems, race conditions, downstream service unavailability\)

The types of tests that are about providing realistic situations are end-to-end tests, smoke tests, canary tests, performance tests etc. Incidentally, these types of tests are really bad at checking request/response correctness because their scope is so broad, it's hard to tell exactly what has gone wrong when something fails.

## Should pact files be used for Postman collections to execute integration tests?

You can do this, but would you be getting any extra benefit from it over your existing contract tests? Using contract tests should mean that the boring "when I send this request, I get this response" kind of tests are already done. Viewing the pacts and the verification results in a Pact Broker \(including interaction level results if using Pactflow\) will allow QAs to see what has already been covered, and allow them to identify any gaps, rather than just repeating existing automated tests. This should allow them to spend more time on high value exploratory manual testing.

## Does implementing contract tests means we have to get rid of existing integration tests with Postman?

The introduction of contract testing allows you to reduce your integrated and e2e tests - but how much they reduce them depends heavily on your situation. Some teams skip the integrated and e2e tests altogether, and some teams keep a smaller set that is focussed on the "business value" scenarios rather than the "is this request/response right" kind of scenarios.

## Should I commit the generated pacts into the consumer's repository?

You can if you want, but it's not necessary unless you have another use for them (like using them for stubs). Most people add them to the .gitignore file to avoid having to re-commit them every time they change.

## How can I tell if I have good contract test coverage of my API?

This is actually the wrong question to be asking. Contract tests aren't intended to provide any particular percentage coverage of the _provider_ (that's what the provider's own functional tests are for). Contract tests are meant to provide (as close to) 100% coverage of the _consumer_ code that makes the calls to the provider (you can think of this as the "provider client code"). If you execute your consumer Pact tests in a separate step in your test suite, you can use standard code coverage tools to determine whether or not your Pact tests have covered a sufficient percentage of your provider client code.

