# SigmaHQ Rule Conventions <!-- omit in toc -->

This document describes an additional set of rule conventions enforced by the SigmaHQ rule repository in order to ensure an easy to maintain rule base. For the general Sigma specification please read the [Sigma_specification.md](../Sigma_specification.md).

## Summary

- [Summary](#summary)
- [Structure](#structure)
- [Filenames](#filenames)
- [Titles](#titles)
- [Status](#status)
- [References](#references)
- [Detection](#detection)
  - [Item Lists](#item-lists)
- [False Postivess](#false-postivess)

## Structure

The rules consist of a few required sections and several optional ones.

```yaml
title [required]
id [required]
related [optional]
   - id {rule-id}
      type {type-identifier}
status [required]
description [required]
references [required]
author [required]
date [required]
modified [optional]
tags [required]
logsource [required]
   category [optional]
   product [optional]
   service [optional]
   definition [optional]
   ...
detection
   {search-identifier} [optional]
      {string-list} [optional]
      {map-list} [optional]
      {field: value} [optional]
   ...
   condition
fields [optional]
falsepositives [required]
level [required]
```

## Filenames

All rule filename must follow the convention described in [Sigmahq_filename_rule.md](./Sigmahq_filename_rule.md)

## Titles

All SigmaHQ rule titles must use title casing

Example:

```yml
title: Suspicious Office Child Process
```

## Status

All newly created rules must start with a status of `experimental`

## References

- All rules must provide a public reference when possible
- References to git based platforms such as Github or Gitlab must provide a permalink instead of the main branch link. This is to avoid any future confusion in the intended reference in case the maintainer make changes

## Detection

### Item Lists

Single item list must be expressed in the same line instead of multi-line.

Example of single list items:

```yml
detection:
    selection:
        Image|endswith: '\example.exe'
```

Example of multi item list:

```yml
detection:
    selection:
        Image|endswith:
            - '\example_1.exe'
            - '\example_2.exe'
            - '\example_3.exe'
```

## False Postivess

- If the rule author expects false positives, then its must be expressed. For example:

```yml
falsepositives:
    - During software installation
    - Legitimate usage of the tool
```

- In cases where the author doesn't know of any false positives then value the should be `Unknown`.
- If the rule author doesn't expect false positives the value should be `Unlikely`.

Also please note the following

- Keywords such as `None`, `Pentest`, `Penetration Test`, `Red Team` are not accepted as valid values.
