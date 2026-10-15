# Part 3: Code Coverage

-------

When we cover unit testing, we will learn about _code coverage_, the percentage of your app's code that is exercised by tests.  As we will learn, there are many ways to measure code coverage, but this assignment has preinstalled a library called SimpleCov that measures "statement coverage"--essentially, which lines of your app were at least touched by your tests.

You can see that the first two lines of `features/support/env.rb` (which Cucumber loads automatically on each run) start the SimpleCov test coverage measurement.

Each time you run your tests (whether Cucumber acceptance tests or RSpec unit/module tests), SimpleCov  generates a report in a directory named `coverage/`. To see the results, open `coverage/index.html` after a test run, and click on the name of any files in your app to see which lines were covered by your tests.  Alternatively, on Codio, right click `coverage/index.html` and click `Preview Static`

<details>
  <summary> 
  What Cucumber scenarios would you have to add in order to cover the non-covered lines?
  </summary>
  <p><blockquote> 
  You can add a simple scenario for creating a movie and a simple
  scenario for destroying a movie.  However, the current controller
  doesn't do any error checking if creation or deletion fails.  If
  that code were added to the controller, you would either need
  multiple scenarios (to cover both happy and sad paths) or you would
  need to write more detailed RSpec tests to cover the corner cases.
  The RSpec assignments will show you how to do that.
  </blockquote></p>
</details>

If your test coverage isn't already at 90%, add scenarios and steps to
cover the gaps as indicated by SimpleCov.
**You will get 100% credit by getting at least 90% code coverage.**

---

[← Part 2: use Acceptance Tests to get new scenarios passing](03-Part-2--use-Acceptance-Tests-to-get-new-scenarios-passing.md) | [Contents](README.md) | [Submission →](05-Submission.md)
