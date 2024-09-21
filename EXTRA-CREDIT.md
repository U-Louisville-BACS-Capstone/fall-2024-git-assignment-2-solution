# Extra credit for Git/GitHub Assignment 2

## Question 1

**When correcting conflicts on Kaitlyn’s and Drew’s branches, why
didn’t Git detect the change from `print()` to `logging.debug()` in
some statements? Explain in detail.**

The change from `print()` to `logging.debug()` were not textual
conflicts -- they were semantic conflicts.  Git can only detect
textual conflicts.

Specifically, the `main` branch had moved on to convert all `print()`
statements to `logging.SOMETHING()`.  However, lines of code that
Kaitlyn and Drew added were entirely new -- there were no
corresponding lines of code on `main` that had been changed to
`logging.debug()`.  Hence, there was no textual conflict, and
therefore Git did not detect it.

## Question 2

**In the rebases of Drew’s branch, why did Git detect a conflict in
the CI test result files, but ultimately the rebased commit only
contained a change in the calculator.py file?  Explain in detail.**

Git detected a textual conflict of Drew's expected result files when
it was rebased against the `main` branch before Kaitlyn's
`add-basic-operations` branch was merged in.  Specifically: Drew's
code changed the functionality of the calculator compared to what was
on `main`, and therefore it created conflicts with the expected
results files.

However, when Kaitlyn's branch was merged in to `main` and Drew
rebased against that (i.e., when Drew rebased against 9ff5e91),
Kaitlyn's expected results files were the same as Drew's expected
results files because the default seed (0) resulted in a pseudo-random
operator of 3, meaning that both Kaitlyn's results and Drew's results
chose the "Multiplying!" operation -- and therefore their expected
results files were identical.

## Question 3

**Why was it useful to add the 3rd CI test that tested a variety of
seed values? Explain in detail.**

The original 2 tests do not test all the possible paths through the
code.  Specifically, they only test the code that is run for a single
`op` value.  Adding the `--seed` CLI functionality and looping through
calling the calculator 100 times exercised all possible `op` values,
and therefore all the code paths that can be taken through the
program.
