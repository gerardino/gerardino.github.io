# Pull Requests To Release

**Get PR identifier (`/#\d*/`) from commit messages across commits between last tag and current commit**

    for m in $(git rev-list HEAD ^$(git describe --abbrev=0) --grep="\#[0-9+]"); do echo $(git show --oneline $m | grep -o "#[0-9]*"); done

---

Get last release

    git describe | xargs git rev-list -n 1

Get the list of commits from `HEAD` to commit B

    git rev-list HEAD ^2018-11-21_09-59
    git rev-list HEAD ^2018-11-21_09-59

List commits since last tag

    git rev-list HEAD ^$(git describe --abbrev=0)

get list of revisions since last tag with a `#+`

    git rev-list HEAD ^$(git describe --abbrev=0) --grep="\#[0-9+]" | xargs git show --oneline

Get short commit description for the latest tag

    git describe | xargs git show --oneline

Create TAG with information:

    git tag -a "$(date '+%Y-%m-%d')" -m "PR(s):$(for m in $(git rev-list HEAD ^$(git describe --abbrev=0) --grep='#[0-9]*'); do printf ' '$(git show --oneline $m | grep -o '#[0-9]*'); done)"
    
    git tag -a "$(date '+%Y-%m-%d')" -m "PR(s):$(for m in $(git rev-list HEAD ^$(git describe --abbrev=0) --grep='Merge pull request #[0-9]*'); do printf ' '$(git show --oneline $m | grep -o '#[0-9]*'); done)"

Check if current head already has a tag:

    [ -z $(git tag -l --points-at HEAD) ] && echo "No tag" || echo "Has tag"

Create tag with information only if there’s a tag already

    [ -z $(git tag -l --points-at HEAD) ] && $(git tag -a "$(date '+%Y-%m-%d')" -m "PR(s):$(for m in $(git rev-list HEAD ^$(git describe --abbrev=0) --grep='Merge pull request #[0-9]*'); do printf ' '$(git show --oneline $m | grep -o '#[0-9]*'); done)") || echo "No tag created"
