# Use `inout` at Function Call Sites

* Proposal: TBD
* Author(s): [Trent Nadeau](http://github.com/tanadeau)
* Status: TBD
* Review manager: TBD

## Introduction

Currently when a function has `inout` parameters, the arguments are passed with the `&` prefix operator. For example:

```swift
func add1(inout num: Int) {
    num += 1
}

var n = 5
add1(&n) // n is now 6
```

This operator does not fit with the rest of the language nor how the parameter is written at the function declaration. It should be replaced so that `inout` is used in both locations so that the call site above would instead be written as:

```swift
add1(inout n) // symmetric and now obvious that n can change
```

*Discussion thread TBD*

## Motivation

The `&` prefix operator is a holdover from C where it is usually read as "address of" and creates a pointer. While very useful in C due to its pervasive use of pointers, its meaning is not the same and introduces an unnecessary syntactic stumbling block from users coming from C. Removing this operator and using `inout` removes this stumbling block due to the semantic change.

This operator is also disconnected from how the function declaration is written and does not imply that the argument may (and likely will) change. Using `inout` stands out, making it clear on first read that the variable may change.

It is also possible that Swift may add Rust-like borrowing in the future. In that case, the `&` symbol would be better used for a borrowed reference. Note that Rust uses the same symbol for declaring a borrowed reference and creating one, creating a nice symmetry in that respect of the language. I think Swift would want to have such symmetry as well.

## Detailed design

```
in-out-expression → inout identifier
```

## Alternatives Considered

Keeping the syntax as it currently is.
