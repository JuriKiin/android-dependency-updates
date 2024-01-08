# android-dependency-updates
This Github Action is designed to automatically check for updates in your `libs.versions.toml `file.

If a newer version is found for any library, the action will print this, and optionally open an issue in your repository with the report.

## Inputs

### file-name `String` -`required`

This is the path to the `libs.versions.toml` file that you are running the check against.

### open-issue `Boolean` - `optional`

Whether or not you want an issue to be created if a newer version is found.

### github-token `Secret` - `required`

The github token for your repository.

**Note: This is automatically created by Github and accessed by:**

`${{ secrets.GITHUB_TOKEN }}`

## Outputs

### dependencies `List<String>`

A list of JSON strings representing the dependencies with outdated versions.
Each item in the list is in the following format:
```
{
    name: String,      // The name of the dependency
    version: String,   // The Current Version
    newVersion: String // The new found version
}

```

### Example usage
```
  check-dependencies:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout Repository
      uses: actions/checkout@v4

    - name: Set up Node.js
      uses: actions/setup-node@v4
      with:
        node-version: '16'

    - name: Install Node.js dependencies
      run: npm install

    - name: Check For Dependency Updates
      uses: ./
      with:
        file-name: 'libs.versions.toml'
        open-issue: true
        github-token: ${{ secrets.GITHUB_TOKEN }}
```

Support this project with a ⭐

[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/jurikiin)
