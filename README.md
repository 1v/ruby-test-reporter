# codeclimate-test-reporter

[![Code Climate](https://codeclimate.com/github/codeclimate/ruby-test-reporter/badges/gpa.svg)](https://codeclimate.com/github/codeclimate/ruby-test-reporter)
[![Build Status](https://travis-ci.org/1v/ruby-test-reporter.svg?branch=master)](https://travis-ci.org/1v/ruby-test-reporter)

Posts SimpleCov test coverage data from your Ruby test suite to Code Climate's
hosted, automated code review service.

Code Climate - [https://codeclimate.com](https://codeclimate.com)

## Installation

This gem requires a user, but not necessarily a paid account, on Code Climate,
so if you don't have one the first step is to signup at:
[https://codeclimate.com](https://codeclimate.com). Then:

* Add this to your Gemfile:

  ```ruby
  group :test do
    gem "simplecov"
    gem "codeclimate-test-reporter", "1.0.0.pre.rc2"
  end
  ```

* Start SimpleCov as you normally would (more information here:
  https://github.com/colszowka/simplecov)
* Set the `CODECLIMATE_REPO_TOKEN` environment variable (provided after you add
  your repo to your Code Climate account by clicking on "Setup Test Coverage" on
  the right hand side of your feed)
* Run the `codeclimate-test-reporter` executable after your test suite

  ```
  bundle exec rake
  bundle exec codeclimate-test-reporter
  ```

Please contact hello@codeclimate.com if you need any assistance setting this up.

## Troubleshooting / FYIs

Across the many different testing frameworks, setups, and environments, there
are lots of variables at play. If you're having any trouble with your test
coverage reporting or the results are confusing, please see our full
documentation here: https://docs.codeclimate.com/docs/setting-up-test-coverage

## Upgrading from pre-1.0 Versions

Version `1.0` of the this gem introduces new, breaking changes to the way the
test reporter is meant to be executed. The following list summarizes the major
differences:

* Previously, this gem extended `Simplecov` with a custom formatter which posted
  results to Code Climate. Now, you are responsible for executing `Simplecov`
  yourself, and then running `codeclimate-test-reporter` as a separate step in
  your build.
* Previously, this gem added some exclusion rules tuned according to feedback
  from its users, and now these no longer happen automatically. *If you are
  experiencing a discrepancy in test coverage % after switching to the new gem
  version, it may be due to missing exclusions. Filtering `vendor`, `spec`, or
  `test` directories may fix this issue.*
* Previously, during the execution of multiple test suites, this gem would send
  results from the first suite completed. You are now expected to run an
  executable packaged with this gem as a separate build step, which means that
  whatever results are there (likely the results from the last suite) will be
  posted to Code Climate.

## Contributions

Patches, bug fixes, feature requests, and pull requests are welcome on the
GitHub page for this project:
[https://github.com/codeclimate/ruby-test-reporter](https://github.com/codeclimate/ruby-test-reporter)

This gem is maintained by Bryan Helmkamp (bryan@codeclimate.com).

## Copyright

See LICENSE.txt

Portions of the implementation were inspired by the coveralls-ruby gem.
