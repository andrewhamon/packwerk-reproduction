Packwerk seems to confuse files that have a prefix that matches an adjacent
folder.

In this repo, the file `app/helpers/foobar_fizz.rb` belongs to the package
`app/helpers`, however packwerk thinks that it belongs to `app/helpers/foobar` instead. This file has a dependency on `app/helpers/meow/package.yml`, and that dependency is correctly declared in the `app/helpers` package.

Packwerk fails, though complaining that there is a violation in the `app/helpers/foobar` package (the wrong package). This is the error message:

```
app/helpers/foobar_fizz.rb:4:17
Dependency violation: ::Meow::Woof belongs to 'app/helpers/meow', but 'app/helpers/foobar' does not specify a dependency on 'app/helpers/meow'.
Are we missing an abstraction?
Is the code making the reference, and the referenced constant, in the right packages?

Inference details: this is a reference to ::Meow::Woof which seems to be defined in app/helpers/meow/woof.rb.
To receive help interpreting or resolving this error message, see: https://github.com/Shopify/packwerk/blob/main/TROUBLESHOOT.md#Troubleshooting-violations


1 offense detected

No stale violations detected
```

This seems to happen any time a file has a common prefix with an adjacent folder.
