# PKL Language Debug Cases

Each example includes a `make run` target that demonstrates the issue. Currently, it only executes `pkl eval local.pkl`.

#### Modifications to the Original Code:
- The directory structure has been flattened.
- Properties and classes have been renamed to more generic terms.

#### Structure:
- `base.pkl` - Contains the base configuration.
- `generic_env.pkl` - Contains the configuration common to all environments.
- `local.pkl` - Contains the configuration specific to the local environment.


# ⚠️ Warning

This repository is intended solely for the discussion and demonstration of a specific issue encountered during development. The code contained herein is not designed for use as a starting point for other projects, and doing so may lead to unexpected results or errors. Please use caution and discretion when referencing this repository.

# Examples

## 1. `./example-1`

This example demonstrates that late bindings, similar to those in `pkl-go-examples`, result in an error in more complex scenarios.

## 2. `./example-2`

This example demonstrates an intuitive alternative to late bindings, which involves using a function and executing it in the environment-specific file (`local.pkl`). This approach results in a similar error to the previous example.

### 2.1. `./example-2.1-self-import`

Previous cases resulted in a similar error, which suggested two possible fixes:

```
To fix, do either of:
1. Add modifier `const` to property `env`
2. Self-import this module, and reference this property from the import.
```

Since this property is not a constant, the first option is not applicable. The second option is demonstrated in this example.

## 3. `./example-3`

This example demonstrates a workaround for the previous issues. It involves passing the `env` property as a parameter to the function when it is called in the `local.pkl` file.

# Expected Configuration

The expected configuration for all examples is the same as the output when running `example-3`:

```
$ make run
pkl eval local.pkl
env = "local"
resources {
  resourceA {
    region = "eu-north-1"
    endpoint = "http://localhost:42069"
    resourceName = "resourceA"
    fullResourceName = "example-local-resourceA"
  }
  resourceB {
    region = "eu-north-1"
    endpoint = "http://localhost:42024"
    resourceName = "resourceB"
    fullResourceName = "example-local-resourceB"
  }
}
```
