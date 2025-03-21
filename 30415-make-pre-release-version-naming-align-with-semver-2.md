# Make pre-release version naming align with semver 2

> Issue #30415 - Created on 7/21/2024

> Original URL: https://github.com/facebook/react/issues/30415

## Description

## Summary

The two latest pre-releases are:

`19.0.0-rc-163365a0-20240717`
`19.0.0-rc-01172397-20240716`

According to semver 2 pre-release versions are supposed to be ordered by dot-separated string ordering:

https://semver.org/
> Precedence for two pre-release versions with the same major, minor, and patch version MUST be determined by comparing each dot separated identifier from left to right until a difference is found


The easiest fix would be to reverse the hash- and date-string in the pre-release versions to this:

`19.0.0-rc-20240717-163365a0`
`19.0.0-rc-20240716-01172397`

This would help us since some of our toolings rely on this ordering to determine the latest version.
