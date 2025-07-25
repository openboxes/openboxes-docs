# Running Automation Tests

A primary goal of the OpenBoxes project is increasing our automation test coverage. Doing so not only gives us more confidence that the application is working correctly, but also makes it easier for us to trust that a new change won't break existing functionality.

If you're interesting in writing new automation tests but are unsure where to start, feel free to reach out to us on [Slack](http://slack-signup.openboxes.com), and we can help you pick a feature to test.



### Frontend Tests

To run frontend unit tests:

```
npm test
```



### Backend Tests

Our current backend test coverage is: [![codecov](https://codecov.io/gh/openboxes/openboxes/branch/develop/graph/badge.svg?token=Ki6DtbxXok)](https://codecov.io/gh/openboxes/openboxes)

To run backend unit tests:

```
grails test-app -unit
```

For instructions on how to run backend API tests, see [the integration test README file](https://github.com/openboxes/openboxes/blob/develop/src/integration-test/README.md) in the openboxes repository.



### End-To-End Tests

We have an end-to-end (E2E) test suite written in Playwright. These tests run against a live, deployed environment and are meant to simulate real user behaviour.

See the [e2e repository](https://github.com/openboxes/openboxes-e2e) for instructions on how to contribute.
