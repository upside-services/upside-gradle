# upside-gradle
Collection of script plugins for gradle.

# Handy Aliases
## Common local workflow:
1. sets version to snapshot
2. runs tests
3. generates coverage report
4. publishes to maven local

`alias glocal='gradle snapshot build jacocoTestReport publishToMavenLocal'`

## Release new Version of project
1. Creates new minor version of artifacts example: 1.1.0-SNAPSHOT -> 1.1.0
2. Runs all tests
3. publishes to configured repos

`alias grelease='gradle clean final build publish'`
