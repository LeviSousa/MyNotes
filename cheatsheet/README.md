# Cheatsheet

## Git

### Check changes of last commit

This will get the changes introduced in the last commit. This [is actually short](https://stackoverflow.com/a/9903611) for `$ git diff HEAD^ HEAD`, as `HEAD` is the default comparison target.

```bash
$ git diff @^
$ git diff HEAD^
```

## Javascript

### Apply CSS to `console.log` message

Adding `%c`, a [formatting specifier](https://console.spec.whatwg.org/#formatting-specifiers), to `console.log`'s first argument, allows to set the wanted CSS to be applied (set as second argument).

```javascript
console.log('%cColored Text', 'background:yellow;color:black');
```
