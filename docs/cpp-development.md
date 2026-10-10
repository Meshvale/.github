# C++ development protocol

| Field | Value |
|---|---|
| ID | MESHVALE-CPP-001 |
| Version | 0.2.0 |
| Status | Living |
| Owner | Meshvale organization community repository |
| Applies to | Geometry, Interchange, Repair, Simplify, Validate |

This document owns shared C++ development practice. Product contracts own mesh
semantics, APIs and failure behavior; each repository's `ENVIRONMENT.md` owns its
build commands. Repository `.clang-format` files project the formatting policy.

## Language and style

**CPP-001.** Build portable C++20 with CMake target requirements
`cxx_std_20` and extensions disabled. Use supported standard-library facilities;
later-standard features require a reviewed baseline change. Select concepts,
ranges, views and other features when they improve the interface. Modules,
coroutines, concurrency and new dependencies need a product requirement.

**CPP-002.** Follow the [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html).
Use `snake_case.h` headers and `snake_case.cpp` implementation files; `.cpp` is
Meshvale's explicit exception to Google's `.cc`. Use self-contained headers,
path-derived include guards, direct includes and Google include ordering.
Types and ordinary functions use `UpperCamelCase`, variables use `snake_case`,
private class fields end in `_`, and constants use `kUpperCamelCase`.
Google's documented accessor and STL-like naming exceptions apply.

**CPP-003.** Format changed C++ code with the receiving repository's Google-based
`.clang-format`, using a formatter that supports its C++20 setting. Review names,
ownership and API documentation separately: formatting does not prove compliance.
Document public lifetimes, preconditions, failure and thread-safety guarantees.

**CPP-008.** Give semantic values a name and an owner. Use typed, named constants
for diagnostic codes, schema/property keys, format identifiers, sentinels, masks,
dimensions, tolerances, thresholds and default limits. Names state purpose and,
where applicable, units; document a non-obvious value's source or rationale. Prefer
`constexpr` values, `std::string_view` for immutable text, `enum class` for finite
states, and existing domain/SDK constants instead of duplicated literals.

Keep a constant in the smallest owning scope; share it only when callers share
the same contract. Put public compile-time values in their owning `.h` and private
implementation values in `.cpp`. Configuration owns genuinely configurable
values. Avoid unrelated global constant collections and names such as `kThree`
that conceal meaning. Convert enums to stable wire strings at the serialization
boundary; preserve published spellings, numeric values and failure behavior.

Ordinary zero/one arithmetic, empty values, self-explanatory test inputs and
human-facing prose at its diagnostic construction site may remain literal when
they do not encode a hidden rule or machine-readable identifier. Repetition is
not required for a value to need a name. Review each semantic literal in new or
modified code; qualify legacy cleanup separately instead of claiming whole-repo
compliance. Tests retain independent protocol expectations rather than deriving
every expected value from the same production constant.

## Safety and product boundaries

**CPP-004.** Use RAII and explicit ownership; borrowing through `std::span` or
`std::string_view` must remain within the owner's lifetime. Check external indices,
offsets, arithmetic overflow and allocation sizes before accessing storage.
Preserve each product's polygon, attribute and non-manifold contracts rather than
assuming triangular, single-UV or manifold input. Fast-math and unchecked undefined
behavior cannot replace those guarantees; optimize from measurements.

**CPP-005.** Meshvale retains exceptions as an explicit exception to Google's
exception policy. Preserve existing allocation, callback and language-binding
contracts; expected product failures use their documented result/diagnostic forms.
Use `noexcept` only where the implementation can uphold it. Mutation and publication
must preserve their owning contracts' rollback, cancellation and source-protection
guarantees.

## Change and verification

**CPP-006.** Before implementation, read the affected product contract and build
instructions. Keep behavior, formatting and compatibility migrations reviewable
as separate changes. Pin dependency revisions and record the tested combination;
keep local tool paths and build evidence in ignored configuration.

**CPP-007.** Run the repository's documentation and portability checks, affected
native tests and installed-package consumers. Binding changes also require clean
installed Python tests. Match dependency build mode and runtime configuration.
Apply warnings as errors to Meshvale targets, independently of dependency flags.
Evaluate static analysis and applicable ASan, UBSan or TSan checks for the changed
risk; record actual tools, coverage and unavailable checks rather than claiming
an unexecuted matrix. Reuse the product's existing test framework.

## Adoption and references

Existing `.hpp` headers and public snake-case APIs are migration work, not evidence
of full style compliance. Header/API migrations require dedicated changes covering
includes, installed consumers, packaging and compatibility decisions; published
names retain their contract until that migration is verified.

The [Mindrally C++ skill](https://github.com/Mindrally/skills/blob/7682ca77710e0971eab4e0ae5dddfa281aea0ba5/cpp/SKILL.md)
informed the modern-C++ checklist. This protocol selects C++20 and Google naming
when its recommendations differ; it does not install that skill or mandate its
optional frameworks or language features.
