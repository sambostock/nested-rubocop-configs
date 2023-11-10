# Nested RuboCop Config Disables Test

All test files contain offending code:

```ruby
assert [].empty? # Should be assert_empty? []
```

In the following examples, we use
- `--disable-pending-cops` to hide the warning about pending cops
- `-ffi` to only output the paths of files which have offenses, and
- `sed` to make the absolute paths relative.

Therefore, for any command, if a file path is output, it means that the `Minitest` department was enabled for that file.

## Running `rubocop` with implicit config and no path

```console
% bundle exec rubocop --disable-pending-cops -ffi | sed "s|$(pwd)/||"
test/empty/example_test.rb
test/enabled/example_test.rb
test/inherit-empty/example_test.rb
test/inherit-enabled/example_test.rb
test/inherit-required_enabled/example_test.rb
test/inherit-required_only/example_test.rb
test/required_enabled/example_test.rb
test/required_only/example_test.rb
```

## Running `rubocop` with implicit config and explicit path

```console
% for dir in test/*; do cmd="bundle exec rubocop --disable-pending-cops -ffi $dir/example_test.rb"; echo "+$cmd"; eval $cmd | sed "s|$(pwd)/||"; echo; done
+bundle exec rubocop --disable-pending-cops -ffi test/disabled/example_test.rb
Error: unrecognized cop or department Minitest found in test/disabled/.rubocop.yml

+bundle exec rubocop --disable-pending-cops -ffi test/empty/example_test.rb
test/empty/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi test/enabled/example_test.rb
Error: unrecognized cop or department Minitest found in test/enabled/.rubocop.yml

+bundle exec rubocop --disable-pending-cops -ffi test/inherit-disabled/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi test/inherit-empty/example_test.rb
test/inherit-empty/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi test/inherit-enabled/example_test.rb
test/inherit-enabled/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi test/inherit-required_disabled/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi test/inherit-required_enabled/example_test.rb
test/inherit-required_enabled/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi test/inherit-required_only/example_test.rb
test/inherit-required_only/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi test/required_disabled/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi test/required_enabled/example_test.rb
test/required_enabled/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi test/required_only/example_test.rb
test/required_only/example_test.rb

```

## Running `rubocop` with explicit config and no path

```console
% for dir in test/*; do cmd="bundle exec rubocop --disable-pending-cops -ffi -c $dir/.rubocop.yml"; echo "+$cmd"; eval $cmd | sed "s|$(pwd)/||"; echo; done
+bundle exec rubocop --disable-pending-cops -ffi -c test/disabled/.rubocop.yml
Error: unrecognized cop or department Minitest found in test/disabled/.rubocop.yml

+bundle exec rubocop --disable-pending-cops -ffi -c test/empty/.rubocop.yml

+bundle exec rubocop --disable-pending-cops -ffi -c test/enabled/.rubocop.yml
Error: unrecognized cop or department Minitest found in test/enabled/.rubocop.yml

+bundle exec rubocop --disable-pending-cops -ffi -c test/inherit-disabled/.rubocop.yml

+bundle exec rubocop --disable-pending-cops -ffi -c test/inherit-empty/.rubocop.yml
test/disabled/example_test.rb
test/empty/example_test.rb
test/enabled/example_test.rb
test/inherit-disabled/example_test.rb
test/inherit-empty/example_test.rb
test/inherit-enabled/example_test.rb
test/inherit-required_disabled/example_test.rb
test/inherit-required_enabled/example_test.rb
test/inherit-required_only/example_test.rb
test/required_disabled/example_test.rb
test/required_enabled/example_test.rb
test/required_only/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi -c test/inherit-enabled/.rubocop.yml
test/disabled/example_test.rb
test/empty/example_test.rb
test/enabled/example_test.rb
test/inherit-disabled/example_test.rb
test/inherit-empty/example_test.rb
test/inherit-enabled/example_test.rb
test/inherit-required_disabled/example_test.rb
test/inherit-required_enabled/example_test.rb
test/inherit-required_only/example_test.rb
test/required_disabled/example_test.rb
test/required_enabled/example_test.rb
test/required_only/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi -c test/inherit-required_disabled/.rubocop.yml

+bundle exec rubocop --disable-pending-cops -ffi -c test/inherit-required_enabled/.rubocop.yml
test/disabled/example_test.rb
test/empty/example_test.rb
test/enabled/example_test.rb
test/inherit-disabled/example_test.rb
test/inherit-empty/example_test.rb
test/inherit-enabled/example_test.rb
test/inherit-required_disabled/example_test.rb
test/inherit-required_enabled/example_test.rb
test/inherit-required_only/example_test.rb
test/required_disabled/example_test.rb
test/required_enabled/example_test.rb
test/required_only/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi -c test/inherit-required_only/.rubocop.yml
test/disabled/example_test.rb
test/empty/example_test.rb
test/enabled/example_test.rb
test/inherit-disabled/example_test.rb
test/inherit-empty/example_test.rb
test/inherit-enabled/example_test.rb
test/inherit-required_disabled/example_test.rb
test/inherit-required_enabled/example_test.rb
test/inherit-required_only/example_test.rb
test/required_disabled/example_test.rb
test/required_enabled/example_test.rb
test/required_only/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi -c test/required_disabled/.rubocop.yml

+bundle exec rubocop --disable-pending-cops -ffi -c test/required_enabled/.rubocop.yml
test/disabled/example_test.rb
test/empty/example_test.rb
test/enabled/example_test.rb
test/inherit-disabled/example_test.rb
test/inherit-empty/example_test.rb
test/inherit-enabled/example_test.rb
test/inherit-required_disabled/example_test.rb
test/inherit-required_enabled/example_test.rb
test/inherit-required_only/example_test.rb
test/required_disabled/example_test.rb
test/required_enabled/example_test.rb
test/required_only/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi -c test/required_only/.rubocop.yml
test/disabled/example_test.rb
test/empty/example_test.rb
test/enabled/example_test.rb
test/inherit-disabled/example_test.rb
test/inherit-empty/example_test.rb
test/inherit-enabled/example_test.rb
test/inherit-required_disabled/example_test.rb
test/inherit-required_enabled/example_test.rb
test/inherit-required_only/example_test.rb
test/required_disabled/example_test.rb
test/required_enabled/example_test.rb
test/required_only/example_test.rb

```

## Running `rubocop` with explicit config and explicit path

```console
% for dir in test/*; do cmd="bundle exec rubocop --disable-pending-cops -ffi -c $dir/.rubocop.yml $dir/example_test.rb"; echo "+$cmd"; eval $cmd | sed "s|$(pwd)/||"; echo; done
+bundle exec rubocop --disable-pending-cops -ffi -c test/disabled/.rubocop.yml test/disabled/example_test.rb
Error: unrecognized cop or department Minitest found in test/disabled/.rubocop.yml

+bundle exec rubocop --disable-pending-cops -ffi -c test/empty/.rubocop.yml test/empty/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi -c test/enabled/.rubocop.yml test/enabled/example_test.rb
Error: unrecognized cop or department Minitest found in test/enabled/.rubocop.yml

+bundle exec rubocop --disable-pending-cops -ffi -c test/inherit-disabled/.rubocop.yml test/inherit-disabled/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi -c test/inherit-empty/.rubocop.yml test/inherit-empty/example_test.rb
test/inherit-empty/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi -c test/inherit-enabled/.rubocop.yml test/inherit-enabled/example_test.rb
test/inherit-enabled/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi -c test/inherit-required_disabled/.rubocop.yml test/inherit-required_disabled/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi -c test/inherit-required_enabled/.rubocop.yml test/inherit-required_enabled/example_test.rb
test/inherit-required_enabled/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi -c test/inherit-required_only/.rubocop.yml test/inherit-required_only/example_test.rb
test/inherit-required_only/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi -c test/required_disabled/.rubocop.yml test/required_disabled/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi -c test/required_enabled/.rubocop.yml test/required_enabled/example_test.rb
test/required_enabled/example_test.rb

+bundle exec rubocop --disable-pending-cops -ffi -c test/required_only/.rubocop.yml test/required_only/example_test.rb
test/required_only/example_test.rb

```

## Running `rubocop` with implicit config and no path, from sub-directories

```console
% for dir in test/*; do cmd="cd $dir && bundle exec rubocop --disable-pending-cops -ffi"; echo "+$cmd"; (eval $cmd && cd ..) | sed "s|$(pwd)/||"; echo; done
+cd test/disabled && bundle exec rubocop --disable-pending-cops -ffi
Error: unrecognized cop or department Minitest found in .rubocop.yml

+cd test/empty && bundle exec rubocop --disable-pending-cops -ffi
test/empty/example_test.rb

+cd test/enabled && bundle exec rubocop --disable-pending-cops -ffi
Error: unrecognized cop or department Minitest found in .rubocop.yml

+cd test/inherit-disabled && bundle exec rubocop --disable-pending-cops -ffi
test/inherit-disabled/example_test.rb

+cd test/inherit-empty && bundle exec rubocop --disable-pending-cops -ffi
test/inherit-empty/example_test.rb

+cd test/inherit-enabled && bundle exec rubocop --disable-pending-cops -ffi
test/inherit-enabled/example_test.rb

+cd test/inherit-required_disabled && bundle exec rubocop --disable-pending-cops -ffi
test/inherit-required_disabled/example_test.rb

+cd test/inherit-required_enabled && bundle exec rubocop --disable-pending-cops -ffi
test/inherit-required_enabled/example_test.rb

+cd test/inherit-required_only && bundle exec rubocop --disable-pending-cops -ffi
test/inherit-required_only/example_test.rb

+cd test/required_disabled && bundle exec rubocop --disable-pending-cops -ffi
test/required_disabled/example_test.rb

+cd test/required_enabled && bundle exec rubocop --disable-pending-cops -ffi
test/required_enabled/example_test.rb

+cd test/required_only && bundle exec rubocop --disable-pending-cops -ffi
test/required_only/example_test.rb

```

## Running `rubocop` with implicit config and explicit path, from sub-directories

```console
% for dir in test/*; do cmd="cd $dir && bundle exec rubocop --disable-pending-cops -ffi example_test.rb"; echo "+$cmd"; (eval $cmd && cd ..) | sed "s|$(pwd)/||"; echo; done
+cd test/disabled && bundle exec rubocop --disable-pending-cops -ffi example_test.rb
Error: unrecognized cop or department Minitest found in .rubocop.yml

+cd test/empty && bundle exec rubocop --disable-pending-cops -ffi example_test.rb
test/empty/example_test.rb

+cd test/enabled && bundle exec rubocop --disable-pending-cops -ffi example_test.rb
Error: unrecognized cop or department Minitest found in .rubocop.yml

+cd test/inherit-disabled && bundle exec rubocop --disable-pending-cops -ffi example_test.rb
test/inherit-disabled/example_test.rb

+cd test/inherit-empty && bundle exec rubocop --disable-pending-cops -ffi example_test.rb
test/inherit-empty/example_test.rb

+cd test/inherit-enabled && bundle exec rubocop --disable-pending-cops -ffi example_test.rb
test/inherit-enabled/example_test.rb

+cd test/inherit-required_disabled && bundle exec rubocop --disable-pending-cops -ffi example_test.rb
test/inherit-required_disabled/example_test.rb

+cd test/inherit-required_enabled && bundle exec rubocop --disable-pending-cops -ffi example_test.rb
test/inherit-required_enabled/example_test.rb

+cd test/inherit-required_only && bundle exec rubocop --disable-pending-cops -ffi example_test.rb
test/inherit-required_only/example_test.rb

+cd test/required_disabled && bundle exec rubocop --disable-pending-cops -ffi example_test.rb
test/required_disabled/example_test.rb

+cd test/required_enabled && bundle exec rubocop --disable-pending-cops -ffi example_test.rb
test/required_enabled/example_test.rb

+cd test/required_only && bundle exec rubocop --disable-pending-cops -ffi example_test.rb
test/required_only/example_test.rb

```

## Running `rubocop` with explicit config and no path, from sub-directories

```console
% for dir in test/*; do cmd="cd $dir && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml"; echo "+$cmd"; (eval $cmd && cd ..) | sed "s|$(pwd)/||"; echo; done
+cd test/disabled && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml
Error: unrecognized cop or department Minitest found in .rubocop.yml

+cd test/empty && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml
test/empty/example_test.rb

+cd test/enabled && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml
Error: unrecognized cop or department Minitest found in .rubocop.yml

+cd test/inherit-disabled && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml
test/inherit-disabled/example_test.rb

+cd test/inherit-empty && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml
test/inherit-empty/example_test.rb

+cd test/inherit-enabled && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml
test/inherit-enabled/example_test.rb

+cd test/inherit-required_disabled && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml
test/inherit-required_disabled/example_test.rb

+cd test/inherit-required_enabled && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml
test/inherit-required_enabled/example_test.rb

+cd test/inherit-required_only && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml
test/inherit-required_only/example_test.rb

+cd test/required_disabled && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml
test/required_disabled/example_test.rb

+cd test/required_enabled && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml
test/required_enabled/example_test.rb

+cd test/required_only && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml
test/required_only/example_test.rb

```

## Running `rubocop` with explicit config and explicit path, from sub-directories

```console
% for dir in test/*; do cmd="cd $dir && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml example_test.rb"; echo "+$cmd"; (eval $cmd && cd ..) | sed "s|$(pwd)/||"; echo; done
+cd test/disabled && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml example_test.rb
Error: unrecognized cop or department Minitest found in .rubocop.yml

+cd test/empty && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml example_test.rb
test/empty/example_test.rb

+cd test/enabled && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml example_test.rb
Error: unrecognized cop or department Minitest found in .rubocop.yml

+cd test/inherit-disabled && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml example_test.rb
test/inherit-disabled/example_test.rb

+cd test/inherit-empty && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml example_test.rb
test/inherit-empty/example_test.rb

+cd test/inherit-enabled && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml example_test.rb
test/inherit-enabled/example_test.rb

+cd test/inherit-required_disabled && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml example_test.rb
test/inherit-required_disabled/example_test.rb

+cd test/inherit-required_enabled && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml example_test.rb
test/inherit-required_enabled/example_test.rb

+cd test/inherit-required_only && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml example_test.rb
test/inherit-required_only/example_test.rb

+cd test/required_disabled && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml example_test.rb
test/required_disabled/example_test.rb

+cd test/required_enabled && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml example_test.rb
test/required_enabled/example_test.rb

+cd test/required_only && bundle exec rubocop --disable-pending-cops -ffi -c .rubocop.yml example_test.rb
test/required_only/example_test.rb

```
