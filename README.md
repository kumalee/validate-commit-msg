# validate-commit-msg-smart

[![travis build](https://img.shields.io/travis/kumalee/validate-commit-msg.svg?style=flat-square)](https://travis-ci.org/kumalee/validate-commit-msg)
[![codecov coverage](https://img.shields.io/codecov/c/github/kumalee/validate-commit-msg.svg?style=flat-square)](https://codecov.io/github/kumalee/validate-commit-msg)
[![version](https://img.shields.io/npm/v/validate-commit-msg-smart.svg?style=flat-square)](http://npm.im/validate-commit-msg-smart)
[![downloads](https://img.shields.io/npm/dm/validate-commit-msg-smart.svg?style=flat-square)](http://npm-stat.com/charts.html?package=validate-commit-msg-smart&from=2016-07-11)
[![MIT License](https://img.shields.io/npm/l/validate-commit-msg-smart.svg?style=flat-square)](http://opensource.org/licenses/MIT)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg?style=flat-square)](https://github.com/semantic-release/semantic-release)
[![Donate][donate-badge]][donate]

This provides you a binary that you can use as a githook to validate the commit message. I recommend
[ghooks](http://npm.im/ghooks). You'll want to make this part of the `commit-msg` githook.

Validates that your commit message follows this format:

```
<type>(<scope>): <subject>
```

## Usage

### options

You can specify options in `package.json`

```javascript
{
  "config": {
    "validate-commit-msg": {
      "types": ["feat", "fix", "docs", "style", "refactor", "perf", "test", "chore", "revert"], // default
      "warnOnFail": false, // default
      "maxSubjectLength": 100, // default
      "subjectPattern": ".+", // default
      "subjectPatternErrorMsg": 'subject does not match subject pattern!', // default
      "helpMessage": "" //default
    }
  }
}
```

#### types

These are the types that are allowed for your commit message. If omitted, the value is what is shown above.

You can also specify: `"types": "*"` to indicate that you don't wish to validate types

You can use RegExp in "types" to validate some special types, like a commit message for jira. For example:

```
// in package.json
"types": [
  "RegExp jira\\-\\d+\\s?feat"
]

// in commit message
jira-0730 feat: support RegExp in types now.
```

** Must start with `RegExp ` and Can't use `():` in types' RegExp. **

#### warnOnFail

If this is set to `true` errors will be logged to the console, however the commit will still pass.

#### maxSubjectLength

This will control the maximum length of the subject.

#### subjectPattern

Optional, accepts a RegExp to match the commit message subject against.

#### subjectPatternErrorMsg

If `subjectPattern` is provided, this message will be displayed if the commit message subject does not match the pattern.

#### helpMessage

If provided, the helpMessage string is displayed when a commit message is not valid. This allows projects to provide a better developer experience for new contributors.

The `helpMessage` also supports interpoling a single `%s` with the original commit message.

### Other notes

If the commit message begins with `WIP` then none of the validation will happen.


## Credits

This was originally developed by contributors to [the angular.js project](https://github.com/angular/angular.js). I
pulled it out so I could re-use this same kind of thing in other projects.

[donate-badge]: https://img.shields.io/badge/$-support-green.svg?style=flat-square
[donate]: http://kcd.im/donate
