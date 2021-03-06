# System Call

[![Build Status](https://travis-ci.org/tlux/systemcall.svg?branch=master)](https://travis-ci.org/tlux/systemcall)
[![Coverage Status](https://coveralls.io/repos/github/tlux/systemcall/badge.svg?branch=master)](https://coveralls.io/github/tlux/systemcall?branch=master)
[![Gem Version](https://badge.fury.io/rb/systemcall.svg)](https://badge.fury.io/rb/systemcall)

A simple wrapper around Ruby's Open3 to call CLI programs and process their
output.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'systemcall'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install systemcall

## Usage

### Functional

To run a CLI program use the following method:

```ruby
SystemCall.call('which', 'bash')
SystemCall.call(['which', 'bash'])
# => #<SystemCall::Result ...>
```

A command that has been executed returns a result object. When the command has
run successfully, the result may look like so:

```ruby
result = SystemCall.call('which', 'bash')
result.exit_code # => 0
result.success? # => true
result.error? # => false
result.success_result # => "/bin/bash"
result.error_result # => ""
result.result # => "/bin/bash"
```

When the command failed, it may look like this:

```ruby
result = SystemCall.call('which', 'unknown')
result.exit_code # => 1
result.success? # => false
result.error? # => true
```

In critical cases, the method may also raise:

```ruby
SystemCall.call('unknown')
# ** (Errno::ENOENT) No such file or directory - unknown
```

### Mixin

Alternatively, you can include the `SystemCall` module directly in your classes
or modules. The included method name is `system_call` but the API is the same as
for `SystemCall.call`.

```ruby
include SystemCall

system_call('which', 'bash')
system_call(['which', 'bash'])
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run
`rake spec` to run the tests. You can also run `bin/console` for an interactive
prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To
release a new version, update the version number in `version.rb`, and then run
`bundle exec rake release`, which will create a git tag for the version, push
git commits and tags, and push the `.gem` file to
[rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at
https://github.com/tlux/systemcall.

## License

The gem is available as open source under the terms of the

[MIT License](https://opensource.org/licenses/MIT).
