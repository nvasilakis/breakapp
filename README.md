# BreakApp

Developers today make pervasive use of third-party modules to reduce costs and accelerate release cycles, at a risk to safety and security.
BreakApp exploits module boundaries to automate security-oriented compartmentalization of legacy applications and enforce security policies, enhancing reliability and security.
It transparently spawns modules in protected compartments while preserving their original behavior.
Optional high-level policies decouple security assumptions made during development from requirements imposed for module composition and use.
These policies allow fine-tuning trade-offs such as security and performance based on changing threat models or load patterns.
Experimental results demonstrate feasibility by enabling simplified security hardening of existing systems with low performance overhead.

Read more about the problem and approach in our [PLOS17](http://nikos.vasilak.is/pubs/breakapp:plos:2017/) or [NDSS18](http://nikos.vasilak.is/pubs/breakapp:ndss:2018/) papers;
  if you have developed useful BreakApp policies, feel free to submit a [pull request](https://github.com/andromeda/breakapp).

## Installation

To install BreakApp:

```
npm install breakapp
```

You can install it globally using `-g`; this is also possible [without using sudo](https://github.com/sindresorhus/guides/blob/master/npm-global-without-sudo.md).

## Usage

Simply include and configure `breakapp` at the top level.

```JavaScript
var breakApp = require("breakapp");
// require other modules
```

Note that for security reasons it must be the first module loaded in your application. It will throw a warning if other third-party modules are found loaded.

## Application-wide Configuration

Users that know more about the application's security and performance characteristics (_e.g._, throughput-oriented, few dangerous modules _etc._) can further tune `breakapp`'s configuration.
The `configure` method allows users to pass in parameters that will guide decomposition beyond the defaults.

```JavaScript
var breakApp = require("breakapp");
breakApp.configure({box: breakApp.boxes.SBX, doubt: [/.*http.*/]});
```

The call above instructs the system to load all HTTP-related modules in their own dedicated sandboxes.

## Package-specific Policies

By default, BreakApp is fully backwards compatible:
  the only change really required is to import the `breakapp` module.
However, users concerned with can choose to confine individual packages.
For example, after loading `breakapp`, they can safely load `malicious` -- a package demonstrating several types of attacks.

```JavaScript
// an example profile
var breakApp = require("breakapp");
var malicious = require("malicious", {type: breakApp.type.PROCESS});
```

In the code above, `malicious` is imported with an isolation policy that protects against reading the state of any other imported modules (including, say, the database credentials).
As these application changes execute during runtime, developers policies give developers considerable flexibility in how to structure the application.

## Compatibility

Policy expressions are compatible with existing codebases.
Expressing policies are _backward_-compatible with systems that do _not_ provide a BreakApp-enabled module system;
  due to variadic arguments, the policy argument is ignored by the built-in `require` function.
Not specifying policies (_i.e._, all of the code out there today) are _forward_-compatible with systems that _do_ provide BreakApp-enabled module system:
  BreakApp will use the application-wide default configuration.

## Contributing

Send your pull requests back to the [@andromeda/breakapp](https://github.com/andromeda/breakapp) repository -- see [guidelines](https://github.com/andromeda/breakapp/CONTRIBUTING.md) there.
Thank you so much!
