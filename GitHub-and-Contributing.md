Articles in this category are designed to familiarize the reader with git, GitHub, and contributing back to LandSandBoat!

* [Using Github](https://github.com/LandSandBoat/server/wiki/Using-Github)
* [Style Guide](https://github.com/LandSandBoat/server/blob/release/CONTRIBUTING.md#style-guide)

Useful git commands:

```sh
# Number of commits per author since date
git shortlog -s --since="01 Jan 2021"

# Contribution statistics since "1 year ago"
git log --shortstat --since "1 year ago" | grep "files changed" | awk '{files+=$1; inserted+=$4; deleted+=$6} END {print "files changed", files, "lines inserted:", inserted, "lines deleted:", deleted}'

# Count commits since date
git rev-list --count --after="Jan 1 2021" --all --no-merges
```
