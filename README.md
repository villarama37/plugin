# Using branch instead of tags

## TL;DR;

If we use branch, you need to use `npm upgrade <package>` to get the lastest from the branch because the `git SHA` is stored in the package-lock.json.

### Is this better than using tags?

If use tags, you would need to manually modify the package.json file of the plugins before running `npm install`.

Also, if multiple packages have change, you can probably run `npm upgrade <package1> <package2>`

# Test

- Create package library and push to github

  - `https://github.com/villarama37/package1`

- Create plugin

  - `https://github.com/villarama37/plugin`

- Add package
  `npm install git+ssh://git@github.com/villarama37/package1#master`

- Check package.lock file

```
~/work/science37/test-install/plugin (master ✘)✭ ᐅ cat package-lock.json
{
  "name": "plugin",
  "version": "1.0.0",
  "lockfileVersion": 1,
  "requires": true,
  "dependencies": {
    "package1": {
      "version": "git+ssh://git@github.com/villarama37/package1.git#346cc6c0a19ee89895f05384716620056ba080ba",
      "from": "git+ssh://git@github.com/villarama37/package1.git#master"
    }
  }
}
```

- Update package
- Run `npm install`
- package-lock.json is not modified
- Run `npm upgrade package1`
- package-lock.json is modified

```
cat package-lock.json
{
  "name": "plugin",
  "version": "1.0.0",
  "lockfileVersion": 1,
  "requires": true,
  "dependencies": {
    "package1": {
      "version": "git+ssh://git@github.com/villarama37/package1.git#c3330ede611520d46bcee85afe6c1ed398b3b607",
      "from": "git+ssh://git@github.com/villarama37/package1.git#master"
    }
  }
}
```
