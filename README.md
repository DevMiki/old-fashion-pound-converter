# Old Fashion Pound

Small Java library for doing arithmetic on the pre-decimal British currency system:

- `1 pound = 20 shillings`
- `1 shilling = 12 pennies`
- `1 pound = 240 pennies` (the internal base unit)

The project is primarily a library (`it.core.Amount` and `it.core.currencies.*`), plus a tiny demo entrypoint (`it.core.Main`).

## What it does

`Amount` stores a value as a total number of pennies and provides the four basic operations:

- `sum(Amount)` / `sumByString("Xp Ys Zd")`
- `subtract(Amount)` (throws `NegativeAmountException` if the result is negative)
- `multiply(int)`
- `divide(int)` (returns quotient and remainder)

Operations return a `Result`:

- `WholeResult`: a single formatted amount (`Xp Ys Zd`)
- `FractionalResult`: a whole amount plus the remainder (`Xp Ys Zd (Xp Ys Zd)`)

## Input / output format

Formatting uses:

- `p` = pounds
- `s` = shillings
- `d` = pennies

Example: `12p 6s 10d` means 12 pounds, 6 shillings and 10 pennies.

`Amount.sumByString(...)` parses exactly the format `Xp Ys Zd` (with spaces), e.g. `3p 4s 10d`.

## Quickstart

### Build and run tests

Requires Java 13+ and Maven.

```bash
mvn test
```

### Run the demo

```bash
mvn -q package
java -cp target/classes it.core.Main
```

## Usage example

```java
final Amount a = new Amount(new Penny(9), new Shilling(8), new Pound(10));
System.out.println(a.divide(7));            // 1p 9s 9d (0p 0s 6d)
System.out.println(a.sumByString("3p 4s 10d")); // 13p 13s 7d
```

## Code map

- `src/main/java/it/core/Amount.java`: core arithmetic and formatting (pennies as base units)
- `src/main/java/it/core/currencies/*`: `Penny`, `Shilling`, `Pound` conversions to base units
- `src/main/java/it/core/result/*`: result types (`WholeResult`, `FractionalResult`)



