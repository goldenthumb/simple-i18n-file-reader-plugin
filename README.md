# simple-i18n-csv-to-json
[![npm](https://img.shields.io/npm/v/@goldenthumb/simple-i18n-csv-to-json.svg)](https://www.npmjs.com/package/@goldenthumb/simple-i18n-csv-to-json)

## Install
```sh
npm install @goldenthumb/simple-i18n-csv-to-json
```
```js
const toJson = require('@goldenthumb/simple-i18n-csv-to-json');
```

## Usage
### sample csv
|     | ko | en | ja   | zh_CN | zh_TW |
|-----|----|----|------|-------|-------|
| yes | 예 | Yes | はい  | 是的   | 是的   |
| No  |    | No | いいえ | 没有   | 沒有   |
<br />
,ko,en,ja,zh_CN,zh_TW <br>
yes,예,Yes,はい,是的,是的 <br>
no,,No,いいえ,没有,沒有 <br>

### CLI

```
Usage: i18n-csv2json <input file> [<output file>] [--allowEmpty]
$ i18n-csv2json ./sample.csv ./output.json
```

### Basic
```
$ i18n-csv2json ./sample.csv ./output.json
```

```js
const toJson = require('@goldenthumb/simple-i18n-csv-to-json');

(async () => {
  try {
    const result = await toJson('./sample.csv');
    console.log(result);
    
    > result
      {
        ko: {
          yes: '예'
        },
        en: {
          yes: 'Yes',
          no: 'No'
        },
        ja: {
          yes: 'はい',
          no: 'いいえ'
        },
        zh_CN: {
          yes: '是的',
          no: '没有'
        },
        zh_TW: {
          yes: '是的',
          no: '沒有'
        }
      };
  } catch(e) {
    console.log(e);
  }
})();
```
### Allow Empty String
```
$ i18n-csv2json ./sample.csv ./output.json --allowEmpty
```

```js
const toJson = require('@goldenthumb/simple-i18n-csv-to-json');

(async () => {
  try {
    const result = await toJson('./sample.csv', { allowEmpty: true });
    console.log(result);
    
    > result
      {
        ko: {
          yes: '예',
          no: ''
        },
        en: {
          yes: 'Yes',
          no: 'No'
        },
        ja: {
          yes: 'はい',
          no: 'いいえ'
        },
        zh_CN: {
          yes: '是的',
          no: '没有'
        },
        zh_TW: {
          yes: '是的',
          no: '沒有'
        }
      };
  } catch(e) {
    console.log(e);
  }
})();

```

### Using by with @goldenthumb/simple
[@goldenthumb/simple](https://github.com/goldenthumb/simple-i18n)
```sh
npm install @goldenthumb/simple-i18n @goldenthumb/simple-i18n-csv-to-json
```

```js
const SimpleI18n = require('@goldenthumb/simple-i18n');
const toJson = require('@goldenthumb/simple-i18n-csv-to-json');

(async () => {
  try {
    const messages = await toJson('./sample.csv');
    const i18n = new SimpleI18n({
      defaultLocale: ['en'],
      locale: 'en',
      messages
    });
    
    i18n.message('yes')
    > Yes.

    i18n.switchLang('ja');
    i18n.message('no');
    > いいえ
  } catch(e) {
    console.log(e);
  }
})();

```

## License
MIT
