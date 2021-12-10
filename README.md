# forked from [Lencerf/vscode-beancount](https://github.com/Lencerf/vscode-beancount)

# VSCode-Beancount

VSCode extension for the text-based double-entry accounting tool [Beancount](http://furius.ca/beancount/)

[![version](https://vsmarketplacebadge.apphb.com/version-short/Lencerf.beancount.svg)](https://marketplace.visualstudio.com/items?itemName=Lencerf.beancount)
[![ratings](https://vsmarketplacebadge.apphb.com/rating-star/Lencerf.beancount.svg)](https://marketplace.visualstudio.com/items?itemName=Lencerf.beancount#review-details)
[![installs](https://vsmarketplacebadge.apphb.com/installs-short/Lencerf.beancount.svg)](https://marketplace.visualstudio.com/items?itemName=Lencerf.beancount)
[![license](https://img.shields.io/badge/license-MIT-brightgreen.svg)](https://raw.githubusercontent.com/Lencerf/vscode-beancount/master/LICENSE.txt)
[![Build Status](https://travis-ci.org/Lencerf/vscode-beancount.svg?branch=master)](https://travis-ci.org/Lencerf/vscode-beancount)
[![Code Style: Google](https://img.shields.io/badge/code%20style-google-blueviolet.svg)](https://github.com/google/gts)

## Features

1. Syntax highlight (syntax file from [draug3n/sublime-beancount](https://github.com/draug3n/sublime-beancount/blob/master/beancount.tmLanguage))
2. Decimal point alignment
3. Auto-completion of account names, payees, and narrations
4. Auto balance checking after saving files
5. Hovers with account balances.
6. Code snippets ([@vlamacko](https://github.com/Lencerf/vscode-beancount/pull/7))
7. Region folding - use indentation ([#5](https://github.com/Lencerf/vscode-beancount/issues/5)), or special comments ([#11](https://github.com/Lencerf/vscode-beancount/pull/11))
8. (Experimental) Use Pinyin initial letters to input existing Chinese narrations and payees quickly. 使用拼音首字母快速输入现有的中文受款人和描述。[See details](https://github.com/Lencerf/vscode-beancount/blob/master/InputMethods.md).

## Extension Settings

This extension contributes the following settings:

* `beancount.indentationSize`:Specify the default indentation size of bean file.
* `beancount.separatorColumn`: specify the column of the decimal separator.
* `beancount.instantAlignment`: Set it to `true` to align the amount (like 1.00 BTC) once a decimal point is inserted.
* `beancount.completePayeeNarration`: Controls whether the auto completion list should include payee and narration fields.
* `beancount.completeMetadata`: Controls whether the auto completion list should include metadatas.
* `beancount.completeTransaction`: Controls whether the auto completion list should include whole transactions.
* `beancount.mainBeanFile`: If you are splitting beancount files into multiple files, set this value to either the full path or the relative path to your main bean file so that
this extension can get all account information. If it is left blank, the extension will consider the file in the current
window as the main file.
* `beancount.runFavaOnActivate`: If it is set to `true`, [fava](https://github.com/beancount/fava) will run once this extension is activated.
* `beancount.favaPath`: Specify the path of Fava if Fava is not installed in the main Python installation.
* `beancount.python3Path`: Specify the path of Python if beancount is not installed in the main Python installation.
* `beancount.inputMethods`: List the input methods for auto-completion of payees and narrations with CJK characters. Currently only `pinyin` is supported. [See details](https://github.com/Lencerf/vscode-beancount/blob/master/InputMethods.md).

## Recommended practices

0. **Make sure you installed Python3 and [beancount](https://pypi.org/project/beancount/). Set `beancount.python3Path` to the correct path.**
1. Split your ledger into several `.bean` files according to time and
put all your `open`/`close` in a main file.
2. Include all other files in the
main file by the `include` command in the main bean file.
3. Open `BeanFolder` with VSCode and set `beancount.mainBeanFile` to the full path of `main.bean` in the current [Workspace Settings](https://code.visualstudio.com/docs/getstarted/settings).

For example, the file structure of your directory looks like this
```
BeanFolder
├── .vscode
│   └── settings.json
├── main.bean
├── before2017.bean
├── 2017-01.bean
└── 2017-02.bean
```
If you open `.vscode/settings.json`, you should see something like this:
```json
{
    "beancount.mainBeanFile": "main.bean"
}
```

Now once `BeanFolder` is opened as a workspace in VSCode, this extension will be able to invoke beancount to check errors and calculate balances.

## Known Issues

see GitHub [issue page](https://github.com/Lencerf/vscode-beancount/issues)

## Release Notes

### 0.6.1 (2021-04-17)
* 小幅优化
* 修复小错误

### 0.5.9 (2020-11-15)
* 小幅优化
* 增加触发字符 “:”，以激活 MetaData 的补全提示
* 增加设置项：indentationSize，以区分 Posting 和 MetaData
* 重写自动补全智能提示的逻辑，Accounts 和 MetaData 的提示不会再混在一起

### 0.5.8 (2020-10-17)
* 小幅优化 InputMethod 特性，存在中英文混合情况时英文单词也是有效的了
* 扩展自动补全，MetaData 也可以了（排除time、memo这些不规律的）

### 0.5.7
* 小幅优化
* 对于.bean和python.exe路径允许Win式 % 环境变量
* 扩展自动补全，可以通过 Payee+Narration 完整补全 Txn
