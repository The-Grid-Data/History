Skip to main content

[](/en/)

  * Learn
  * Use
  * Build
  * Participate
  * Research

Search```K`

Languages EN

# Testing ERC-20 tokens with Waffle

wafflesmart contractssoliditytestingerc-20

Intermediate

![✍️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/270d.svg)Vladislav
Starostenko

![📆](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4c6.svg)
October 16, 2020

![⏱️](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/23f1.svg)42
minute read minute read

On this page

  * A few words about Waffle
  * The quick tutorial
  * Step #1: Install waffle in your project Link to doc
  * Step #2: Write a smart contract Link to doc
  * Step #3: Compile your smart contract Link to doc
  * Step #4: Test your smart contract Link to doc
    * Step #4.1 Install necessary dependencies Link to doc
    * Step #4.2 Create test file Link to doc
    * Step #4.3 Emitting events Link to doc
    * Step #4.4 Revert with message Link to doc
    * Step #4.5 Change-token-balance Link to doc
  * Congratulations

In this tutorial you will learn how to:

  * Write tests for smart contracts with Waffle
  * Use some popular matchers to test smart contracts with Waffle

Assumptions:

  * you can get around in a terminal,
  * you can create a new `JavaScript` project,
  * you've written a few lines of `Solidity` code,
  * you've written a few tests in `JavaScript`,
  * you’ve used `yarn` or `npm`, JavaScripts’s package installer.

Again, if any of these are untrue, or you don’t plan to reproduce the code in
this article, you can likely still follow along just fine.

## A few words about Waffle

[Waffle(opens in a new tab)](https://getwaffle.io) is the most advanced
library for writing and testing smart contracts.

Works with the [JavaScript API](/en/developers/docs/apis/javascript/) ethers-
js.

You can read more details in the [Waffle documentation(opens in a new
tab)](https://ethereum-waffle.readthedocs.io/en/latest/#waffle-documentation)
!

## The quick tutorial

First things first, create new `JavaScript` or `TypeScript` project ( I'll use
`TS`, but if you use `JS` it's not a problem ) :

Somewhat like this :

package.json

    
    
    1{
    
    2  "name": "tutorial",
    
    3  "version": "1.0.0",
    
    4  "main": "index.js",
    
    5  "license": "MIT",
    
    6  "scripts": {
    
    7    "test": "export NODE_ENV=test && mocha",
    
    8    "lint": "eslint '{src,test}/**/*.ts'",
    
    9    "lint:fix": "eslint --fix '{src,test}/**/*.ts'",
    
    10    "build": "waffle"
    
    11  },
    
    12  "devDependencies": {
    
    13    "@types/mocha": "^5.2.7",
    
    14    "@typescript-eslint/eslint-plugin": "^2.30.0",
    
    15    "@typescript-eslint/parser": "^2.30.0",
    
    16    "eslint": "^6.8.0",
    
    17    "eslint-plugin-import": "^2.20.2",
    
    18    "ethers": "^5.0.17",
    
    19    "mocha": "^7.1.2",
    
    20    "ts-node": "^8.9.1",
    
    21    "typescript": "^3.8.3"
    
    22  }
    
    23}
    
    Show all

tsconfig.json

    
    
    1{
    
    2  "compilerOptions": {
    
    3    "declaration": true,
    
    4    "esModuleInterop": true,
    
    5    "lib": [
    
    6      "ES2018"
    
    7    ],
    
    8    "module": "CommonJS",
    
    9    "moduleResolution": "node",
    
    10    "outDir": "dist",
    
    11    "resolveJsonModule": true,
    
    12    "skipLibCheck": true,
    
    13    "strict": true,
    
    14    "target": "ES2018"
    
    15  }
    
    16}
    
    Show all

.gitignore

    
    
    1node_modules
    
    2build

.eslintrc.js

    
    
    1module.exports = {
    
    2  "env": {
    
    3  "es6": true
    
    4},
    
    5  "extends": [
    
    6  "plugin:@typescript-eslint/recommended",
    
    7  "plugin:import/errors",
    
    8  "plugin:import/warnings",
    
    9  "plugin:import/typescript"
    
    10],
    
    11  "parser": "@typescript-eslint/parser",
    
    12  "parserOptions": {
    
    13  "project": "./tsconfig.json",
    
    14    "sourceType": "module"
    
    15},
    
    16  "rules": {
    
    17  "@typescript-eslint/camelcase": "off",
    
    18    "@typescript-eslint/explicit-function-return-type": "off",
    
    19    "@typescript-eslint/explicit-member-accessibility": [
    
    20    "error",
    
    21    {
    
    22      "accessibility": "no-public",
    
    23      "overrides": {
    
    24        "parameterProperties": "off"
    
    25      }
    
    26    }
    
    27  ],
    
    28    "@typescript-eslint/indent": [
    
    29    "error",
    
    30    2,
    
    31    {
    
    32      "ArrayExpression": 1,
    
    33      "CallExpression": {
    
    34        "arguments": 1
    
    35      },
    
    36      "FunctionDeclaration": {
    
    37        "body": 1,
    
    38        "parameters": 1
    
    39      },
    
    40      "FunctionExpression": {
    
    41        "body": 1,
    
    42        "parameters": 1
    
    43      },
    
    44      "ImportDeclaration": 1,
    
    45      "MemberExpression": 1,
    
    46      "ObjectExpression": 1,
    
    47      "SwitchCase": 1,
    
    48      "VariableDeclarator": 1,
    
    49      "flatTernaryExpressions": false,
    
    50      "ignoreComments": false,
    
    51      "outerIIFEBody": 1
    
    52    }
    
    53  ],
    
    54    "@typescript-eslint/interface-name-prefix": "off",
    
    55    "@typescript-eslint/member-delimiter-style": [
    
    56    "error",
    
    57    {
    
    58      "multiline": {
    
    59        "delimiter": "semi",
    
    60        "requireLast": true
    
    61      },
    
    62      "singleline": {
    
    63        "delimiter": "semi",
    
    64        "requireLast": false
    
    65      }
    
    66    }
    
    67  ],
    
    68    "@typescript-eslint/no-explicit-any": "off",
    
    69    "@typescript-eslint/no-parameter-properties": "off",
    
    70    "@typescript-eslint/no-unused-vars": [
    
    71    "error",
    
    72    {
    
    73      "args": "none",
    
    74      "ignoreRestSiblings": true,
    
    75      "vars": "all"
    
    76    }
    
    77  ],
    
    78    "@typescript-eslint/no-use-before-define": "off",
    
    79    "@typescript-eslint/no-useless-constructor": "error",
    
    80    "@typescript-eslint/no-var-requires": "warn",
    
    81    "accessor-pairs": "error",
    
    82    "array-bracket-spacing": [
    
    83    "error",
    
    84    "never"
    
    85  ],
    
    86    "arrow-spacing": [
    
    87    "error",
    
    88    {
    
    89      "after": true,
    
    90      "before": true
    
    91    }
    
    92  ],
    
    93    "block-spacing": [
    
    94    "error",
    
    95    "always"
    
    96  ],
    
    97    "brace-style": [
    
    98    "error",
    
    99    "1tbs",
    
    100    {
    
    101      "allowSingleLine": true
    
    102    }
    
    103  ],
    
    104    "camelcase": "off",
    
    105    "comma-dangle": [
    
    106    "error",
    
    107    {
    
    108      "arrays": "never",
    
    109      "exports": "never",
    
    110      "functions": "never",
    
    111      "imports": "never",
    
    112      "objects": "never"
    
    113    }
    
    114  ],
    
    115    "comma-spacing": [
    
    116    "error",
    
    117    {
    
    118      "after": true,
    
    119      "before": false
    
    120    }
    
    121  ],
    
    122    "comma-style": [
    
    123    "error",
    
    124    "last"
    
    125  ],
    
    126    "computed-property-spacing": [
    
    127    "error",
    
    128    "never"
    
    129  ],
    
    130    "constructor-super": "error",
    
    131    "curly": [
    
    132    "error",
    
    133    "multi-line"
    
    134  ],
    
    135    "dot-location": [
    
    136    "error",
    
    137    "property"
    
    138  ],
    
    139    "eol-last": "error",
    
    140    "eqeqeq": [
    
    141    "error",
    
    142    "always",
    
    143    {
    
    144      "null": "ignore"
    
    145    }
    
    146  ],
    
    147    "func-call-spacing": [
    
    148    "error",
    
    149    "never"
    
    150  ],
    
    151    "generator-star-spacing": [
    
    152    "error",
    
    153    {
    
    154      "after": true,
    
    155      "before": true
    
    156    }
    
    157  ],
    
    158    "handle-callback-err": [
    
    159    "error",
    
    160    "^(err|error)$"
    
    161  ],
    
    162    "import/default": "off",
    
    163    "import/named": "off",
    
    164    "import/no-extraneous-dependencies": [
    
    165    "error",
    
    166    {
    
    167      "devDependencies": false
    
    168    }
    
    169  ],
    
    170    "import/no-unresolved": "off",
    
    171    "indent": "off",
    
    172    "key-spacing": [
    
    173    "error",
    
    174    {
    
    175      "afterColon": true,
    
    176      "beforeColon": false
    
    177    }
    
    178  ],
    
    179    "keyword-spacing": [
    
    180    "error",
    
    181    {
    
    182      "after": true,
    
    183      "before": true
    
    184    }
    
    185  ],
    
    186    "linebreak-style": [
    
    187    "error",
    
    188    "unix"
    
    189  ],
    
    190    "lines-between-class-members": [
    
    191    "error",
    
    192    "always",
    
    193    {
    
    194      "exceptAfterSingleLine": true
    
    195    }
    
    196  ],
    
    197    "max-len": [
    
    198    "error",
    
    199    {
    
    200      "code": 120
    
    201    }
    
    202  ],
    
    203    "new-cap": [
    
    204    "error",
    
    205    {
    
    206      "capIsNew": false,
    
    207      "newIsCap": true
    
    208    }
    
    209  ],
    
    210    "new-parens": "error",
    
    211    "no-array-constructor": "error",
    
    212    "no-async-promise-executor": "error",
    
    213    "no-caller": "error",
    
    214    "no-class-assign": "error",
    
    215    "no-compare-neg-zero": "error",
    
    216    "no-cond-assign": "error",
    
    217    "no-const-assign": "error",
    
    218    "no-constant-condition": [
    
    219    "error",
    
    220    {
    
    221      "checkLoops": false
    
    222    }
    
    223  ],
    
    224    "no-control-regex": "error",
    
    225    "no-debugger": "error",
    
    226    "no-delete-var": "error",
    
    227    "no-dupe-args": "error",
    
    228    "no-dupe-keys": "error",
    
    229    "no-duplicate-case": "error",
    
    230    "no-empty-character-class": "error",
    
    231    "no-empty-pattern": "error",
    
    232    "no-eval": "error",
    
    233    "no-ex-assign": "error",
    
    234    "no-extend-native": "error",
    
    235    "no-extra-bind": "error",
    
    236    "no-extra-boolean-cast": "error",
    
    237    "no-extra-parens": [
    
    238    "error",
    
    239    "functions"
    
    240  ],
    
    241    "no-fallthrough": "error",
    
    242    "no-floating-decimal": "error",
    
    243    "no-func-assign": "error",
    
    244    "no-global-assign": "error",
    
    245    "no-implied-eval": "error",
    
    246    "no-inner-declarations": [
    
    247    "error",
    
    248    "functions"
    
    249  ],
    
    250    "no-invalid-regexp": "error",
    
    251    "no-irregular-whitespace": "error",
    
    252    "no-iterator": "error",
    
    253    "no-label-var": "error",
    
    254    "no-labels": [
    
    255    "error",
    
    256    {
    
    257      "allowLoop": false,
    
    258      "allowSwitch": false
    
    259    }
    
    260  ],
    
    261    "no-lone-blocks": "error",
    
    262    "no-misleading-character-class": "error",
    
    263    "no-mixed-operators": [
    
    264    "error",
    
    265    {
    
    266      "allowSamePrecedence": true,
    
    267      "groups": [
    
    268        [
    
    269          "==",
    
    270          "!=",
    
    271          "===",
    
    272          "!==",
    
    273          ">",
    
    274          ">=",
    
    275          "<",
    
    276          "<="
    
    277        ],
    
    278        [
    
    279          "&&",
    
    280          "||"
    
    281        ],
    
    282        [
    
    283          "in",
    
    284          "instanceof"
    
    285        ]
    
    286      ]
    
    287    }
    
    288  ],
    
    289    "no-mixed-spaces-and-tabs": "error",
    
    290    "no-multi-spaces": "error",
    
    291    "no-multi-str": "error",
    
    292    "no-multiple-empty-lines": [
    
    293    "error",
    
    294    {
    
    295      "max": 1,
    
    296      "maxEOF": 0
    
    297    }
    
    298  ],
    
    299    "no-negated-in-lhs": "error",
    
    300    "no-new": "error",
    
    301    "no-new-func": "error",
    
    302    "no-new-object": "error",
    
    303    "no-new-require": "error",
    
    304    "no-new-symbol": "error",
    
    305    "no-new-wrappers": "error",
    
    306    "no-obj-calls": "error",
    
    307    "no-octal": "error",
    
    308    "no-octal-escape": "error",
    
    309    "no-path-concat": "error",
    
    310    "no-proto": "error",
    
    311    "no-prototype-builtins": "error",
    
    312    "no-redeclare": [
    
    313    "error",
    
    314    {
    
    315      "builtinGlobals": false
    
    316    }
    
    317  ],
    
    318    "no-regex-spaces": "error",
    
    319    "no-return-assign": [
    
    320    "error",
    
    321    "except-parens"
    
    322  ],
    
    323    "no-return-await": "error",
    
    324    "no-self-assign": "error",
    
    325    "no-self-compare": "error",
    
    326    "no-sequences": "error",
    
    327    "no-shadow-restricted-names": "error",
    
    328    "no-sparse-arrays": "error",
    
    329    "no-tabs": "error",
    
    330    "no-template-curly-in-string": "error",
    
    331    "no-this-before-super": "error",
    
    332    "no-throw-literal": "error",
    
    333    "no-trailing-spaces": "error",
    
    334    "no-unexpected-multiline": "error",
    
    335    "no-unmodified-loop-condition": "error",
    
    336    "no-unneeded-ternary": [
    
    337    "error",
    
    338    {
    
    339      "defaultAssignment": false
    
    340    }
    
    341  ],
    
    342    "no-unreachable": "error",
    
    343    "no-unsafe-finally": "error",
    
    344    "no-unsafe-negation": "error",
    
    345    "no-use-before-define": [
    
    346    "error",
    
    347    {
    
    348      "classes": false,
    
    349      "functions": false,
    
    350      "variables": false
    
    351    }
    
    352  ],
    
    353    "no-useless-call": "error",
    
    354    "no-useless-catch": "error",
    
    355    "no-useless-computed-key": "error",
    
    356    "no-useless-escape": "error",
    
    357    "no-useless-rename": "error",
    
    358    "no-useless-return": "error",
    
    359    "no-whitespace-before-property": "error",
    
    360    "no-with": "error",
    
    361    "object-curly-spacing": [
    
    362    "error",
    
    363    "never"
    
    364  ],
    
    365    "object-property-newline": [
    
    366    "error",
    
    367    {
    
    368      "allowMultiplePropertiesPerLine": true
    
    369    }
    
    370  ],
    
    371    "one-var": [
    
    372    "error",
    
    373    {
    
    374      "initialized": "never"
    
    375    }
    
    376  ],
    
    377    "operator-linebreak": [
    
    378    "error",
    
    379    "after",
    
    380    {
    
    381      "overrides": {
    
    382        ":": "before",
    
    383        "?": "before"
    
    384      }
    
    385    }
    
    386  ],
    
    387    "padded-blocks": [
    
    388    "error",
    
    389    {
    
    390      "blocks": "never",
    
    391      "classes": "never",
    
    392      "switches": "never"
    
    393    }
    
    394  ],
    
    395    "prefer-const": [
    
    396    "error",
    
    397    {
    
    398      "destructuring": "all"
    
    399    }
    
    400  ],
    
    401    "prefer-promise-reject-errors": "error",
    
    402    "quote-props": [
    
    403    "error",
    
    404    "as-needed"
    
    405  ],
    
    406    "quotes": [
    
    407    "error",
    
    408    "single"
    
    409  ],
    
    410    "rest-spread-spacing": [
    
    411    "error",
    
    412    "never"
    
    413  ],
    
    414    "semi": [
    
    415    "error",
    
    416    "always"
    
    417  ],
    
    418    "semi-spacing": [
    
    419    "error",
    
    420    {
    
    421      "after": true,
    
    422      "before": false
    
    423    }
    
    424  ],
    
    425    "space-before-blocks": [
    
    426    "error",
    
    427    "always"
    
    428  ],
    
    429    "space-before-function-paren": [
    
    430    "error",
    
    431    {
    
    432      "anonymous": "always",
    
    433      "named": "never",
    
    434      "asyncArrow": "always"
    
    435    }
    
    436  ],
    
    437    "space-in-parens": [
    
    438    "error",
    
    439    "never"
    
    440  ],
    
    441    "space-infix-ops": "error",
    
    442    "space-unary-ops": [
    
    443    "error",
    
    444    {
    
    445      "nonwords": false,
    
    446      "words": true
    
    447    }
    
    448  ],
    
    449    "spaced-comment": [
    
    450    "error",
    
    451    "always",
    
    452    {
    
    453      "block": {
    
    454        "balanced": true,
    
    455        "exceptions": [
    
    456          "*"
    
    457        ],
    
    458        "markers": [
    
    459          "*package",
    
    460          "!",
    
    461          ",",
    
    462          ":",
    
    463          "::",
    
    464          "flow-include"
    
    465        ]
    
    466      },
    
    467      "line": {
    
    468        "markers": [
    
    469          "*package",
    
    470          "!",
    
    471          "/",
    
    472          ",",
    
    473          "="
    
    474        ]
    
    475      }
    
    476    }
    
    477  ],
    
    478    "symbol-description": "error",
    
    479    "template-curly-spacing": [
    
    480    "error",
    
    481    "never"
    
    482  ],
    
    483    "template-tag-spacing": [
    
    484    "error",
    
    485    "never"
    
    486  ],
    
    487    "unicode-bom": [
    
    488    "error",
    
    489    "never"
    
    490  ],
    
    491    "use-isnan": "error",
    
    492    "valid-typeof": [
    
    493    "error",
    
    494    {
    
    495      "requireStringLiterals": true
    
    496    }
    
    497  ],
    
    498    "wrap-iife": [
    
    499    "error",
    
    500    "any",
    
    501    {
    
    502      "functionPrototypeMethods": true
    
    503    }
    
    504  ],
    
    505    "yield-star-spacing": [
    
    506    "error",
    
    507    "both"
    
    508  ],
    
    509    "yoda": [
    
    510    "error",
    
    511    "never"
    
    512  ]
    
    513},
    
    514  "overrides": [
    
    515  {
    
    516    "files": [
    
    517      "test/**/*.ts"
    
    518    ],
    
    519    "rules": {
    
    520      "@typescript-eslint/no-explicit-any": "off",
    
    521      "@typescript-eslint/no-non-null-assertion": "off",
    
    522      "@typescript-eslint/no-var-requires": "off",
    
    523      "no-unused-expressions": "off",
    
    524      "prefer-promise-reject-errors": "off",
    
    525      "import/no-extraneous-dependencies": [
    
    526        "error",
    
    527        {
    
    528          "devDependencies": true
    
    529        }
    
    530      ]
    
    531    }
    
    532  }
    
    533]
    
    534}
    
    Show all

## Step #1: Install waffle in your project [Link to doc(opens in a new
tab)](https://ethereum-waffle.readthedocs.io/en/latest/getting-
started.html#installation)

To get started, install `ethereum-waffle`. In this tutorial, I'll use `yarn`,
so to install `ethereum-waffle` run:

    
    
     yarn add --dev ethereum-waffle

## Step #2: Write a smart contract [Link to doc(opens in a new
tab)](https://ethereum-waffle.readthedocs.io/en/latest/getting-
started.html#writing-a-contract)

In this tutorial, I'll use [ERC20(opens in a new
tab)](https://github.com/OpenZeppelin/openzeppelin-
contracts/blob/ded2b0a55c9c13731963ab7b85a70c8e73504bab/contracts/token/ERC20/ERC20.sol)
token from [OpenZeppelin(opens in a new tab)](https://openzeppelin.com).

So, add `OpenZeppelin` by installing it with `yarn`:

    
    
     yarn add @openzeppelin/contracts -D

Then create `BasicToken.sol` contract in `src` directory:

    
    
    1pragma solidity ^0.6.0;
    
    2
    
    3import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
    
    4
    
    5// Example class - a mock class derived from ERC20
    
    6contract BasicToken is ERC20 {
    
    7    constructor(uint256 initialBalance) ERC20("Basic", "BSC") public {
    
    8        _mint(msg.sender, initialBalance);
    
    9    }
    
    10}
    
    11
    
    Show all
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

## Step #3: Compile your smart contract [Link to doc(opens in a new
tab)](https://ethereum-waffle.readthedocs.io/en/latest/getting-
started.html#compiling-the-contract)

To compile your smart contract add the following entry in the `package.json`
of your project :

    
    
    1{
    
    2  "scripts": {
    
    3    "build": "waffle"
    
    4  }
    
    5}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

Also, add `waffle.json` file in the main directory of your project.

An example of `waffle.json` configuration:

    
    
    1{
    
    2  "compilerType": "solcjs",
    
    3  "compilerVersion": "0.6.2",
    
    4  "sourceDirectory": "./src",
    
    5  "outputDirectory": "./build"
    
    6}
    
    ![📋](https://cdnjs.cloudflare.com/ajax/libs/twemoji/12.0.4/2/svg/1f4cb.svg) Copy

You can read more about the Waffle configuration [here(opens in a new
tab)](https://ethereum-
waffle.readthedocs.io/en/latest/configuration.html#configuration).

Then just run `yarn build` to compile your smart contract.

You should see that Waffle compiled your contract and placed the resulting
JSON output inside the `build` directory.

BasicToken.json

    
    
    1{
    
    2  "abi": [
    
    3    {
    
    4      "inputs": [
    
    5        {
    
    6          "internalType": "uint256",
    
    7          "name": "initialBalance",
    
    8          "type": "uint256"
    
    9        }
    
    10      ],
    
    11      "stateMutability": "nonpayable",
    
    12      "type": "constructor"
    
    13    },
    
    14    {
    
    15      "anonymous": false,
    
    16      "inputs": [
    
    17        {
    
    18          "indexed": true,
    
    19          "internalType": "address",
    
    20          "name": "owner",
    
    21          "type": "address"
    
    22        },
    
    23        {
    
    24          "indexed": true,
    
    25          "internalType": "address",
    
    26          "name": "spender",
    
    27          "type": "address"
    
    28        },
    
    29        {
    
    30          "indexed": false,
    
    31          "internalType": "uint256",
    
    32          "name": "value",
    
    33          "type": "uint256"
    
    34        }
    
    35      ],
    
    36      "name": "Approval",
    
    37      "type": "event"
    
    38    },
    
    39    {
    
    40      "anonymous": false,
    
    41      "inputs": [
    
    42        {
    
    43          "indexed": true,
    
    44          "internalType": "address",
    
    45          "name": "from",
    
    46          "type": "address"
    
    47        },
    
    48        {
    
    49          "indexed": true,
    
    50          "internalType": "address",
    
    51          "name": "to",
    
    52          "type": "address"
    
    53        },
    
    54        {
    
    55          "indexed": false,
    
    56          "internalType": "uint256",
    
    57          "name": "value",
    
    58          "type": "uint256"
    
    59        }
    
    60      ],
    
    61      "name": "Transfer",
    
    62      "type": "event"
    
    63    },
    
    64    {
    
    65      "inputs": [
    
    66        {
    
    67          "internalType": "address",
    
    68          "name": "owner",
    
    69          "type": "address"
    
    70        },
    
    71        {
    
    72          "internalType": "address",
    
    73          "name": "spender",
    
    74          "type": "address"
    
    75        }
    
    76      ],
    
    77      "name": "allowance",
    
    78      "outputs": [
    
    79        {
    
    80          "internalType": "uint256",
    
    81          "name": "",
    
    82          "type": "uint256"
    
    83        }
    
    84      ],
    
    85      "stateMutability": "view",
    
    86      "type": "function"
    
    87    },
    
    88    {
    
    89      "inputs": [
    
    90        {
    
    91          "internalType": "address",
    
    92          "name": "spender",
    
    93          "type": "address"
    
    94        },
    
    95        {
    
    96          "internalType": "uint256",
    
    97          "name": "amount",
    
    98          "type": "uint256"
    
    99        }
    
    100      ],
    
    101      "name": "approve",
    
    102      "outputs": [
    
    103        {
    
    104          "internalType": "bool",
    
    105          "name": "",
    
    106          "type": "bool"
    
    107        }
    
    108      ],
    
    109      "stateMutability": "nonpayable",
    
    110      "type": "function"
    
    111    },
    
    112    {
    
    113      "inputs": [
    
    114        {
    
    115          "internalType": "address",
    
    116          "name": "account",
    
    117          "type": "address"
    
    118        }
    
    119      ],
    
    120      "name": "balanceOf",
    
    121      "outputs": [
    
    122        {
    
    123          "internalType": "uint256",
    
    124          "name": "",
    
    125          "type": "uint256"
    
    126        }
    
    127      ],
    
    128      "stateMutability": "view",
    
    129      "type": "function"
    
    130    },
    
    131    {
    
    132      "inputs": [],
    
    133      "name": "decimals",
    
    134      "outputs": [
    
    135        {
    
    136          "internalType": "uint8",
    
    137          "name": "",
    
    138          "type": "uint8"
    
    139        }
    
    140      ],
    
    141      "stateMutability": "view",
    
    142      "type": "function"
    
    143    },
    
    144    {
    
    145      "inputs": [
    
    146        {
    
    147          "internalType": "address",
    
    148          "name": "spender",
    
    149          "type": "address"
    
    150        },
    
    151        {
    
    152          "internalType": "uint256",
    
    153          "name": "subtractedValue",
    
    154          "type": "uint256"
    
    155        }
    
    156      ],
    
    157      "name": "decreaseAllowance",
    
    158      "outputs": [
    
    159        {
    
    160          "internalType": "bool",
    
    161          "name": "",
    
    162          "type": "bool"
    
    163        }
    
    164      ],
    
    165      "stateMutability": "nonpayable",
    
    166      "type": "function"
    
    167    },
    
    168    {
    
    169      "inputs": [
    
    170        {
    
    171          "internalType": "address",
    
    172          "name": "spender",
    
    173          "type": "address"
    
    174        },
    
    175        {
    
    176          "internalType": "uint256",
    
    177          "name": "addedValue",
    
    178          "type": "uint256"
    
    179        }
    
    180      ],
    
    181      "name": "increaseAllowance",
    
    182      "outputs": [
    
    183        {
    
    184          "internalType": "bool",
    
    185          "name": "",
    
    186          "type": "bool"
    
    187        }
    
    188      ],
    
    189      "stateMutability": "nonpayable",
    
    190      "type": "function"
    
    191    },
    
    192    {
    
    193      "inputs": [],
    
    194      "name": "name",
    
    195      "outputs": [
    
    196        {
    
    197          "internalType": "string",
    
    198          "name": "",
    
    199          "type": "string"
    
    200        }
    
    201      ],
    
    202      "stateMutability": "view",
    
    203      "type": "function"
    
    204    },
    
    205    {
    
    206      "inputs": [],
    
    207      "name": "symbol",
    
    208      "outputs": [
    
    209        {
    
    210          "internalType": "string",
    
    211          "name": "",
    
    212          "type": "string"
    
    213        }
    
    214      ],
    
    215      "stateMutability": "view",
    
    216      "type": "function"
    
    217    },
    
    218    {
    
    219      "inputs": [],
    
    220      "name": "totalSupply",
    
    221      "outputs": [
    
    222        {
    
    223          "internalType": "uint256",
    
    224          "name": "",
    
    225          "type": "uint256"
    
    226        }
    
    227      ],
    
    228      "stateMutability": "view",
    
    229      "type": "function"
    
    230    },
    
    231    {
    
    232      "inputs": [
    
    233        {
    
    234          "internalType": "address",
    
    235          "name": "recipient",
    
    236          "type": "address"
    
    237        },
    
    238        {
    
    239          "internalType": "uint256",
    
    240          "name": "amount",
    
    241          "type": "uint256"
    
    242        }
    
    243      ],
    
    244      "name": "transfer",
    
    245      "outputs": [
    
    246        {
    
    247          "internalType": "bool",
    
    248          "name": "",
    
    249          "type": "bool"
    
    250        }
    
    251      ],
    
    252      "stateMutability": "nonpayable",
    
    253      "type": "function"
    
    254    },
    
    255    {
    
    256      "inputs": [
    
    257        {
    
    258          "internalType": "address",
    
    259          "name": "sender",
    
    260          "type": "address"
    
    261        },
    
    262        {
    
    263          "internalType": "address",
    
    264          "name": "recipient",
    
    265          "type": "address"
    
    266        },
    
    267        {
    
    268          "internalType": "uint256",
    
    269          "name": "amount",
    
    270          "type": "uint256"
    
    271        }
    
    272      ],
    
    273      "name": "transferFrom",
    
    274      "outputs": [
    
    275        {
    
    276          "internalType": "bool",
    
    277          "name": "",
    
    278          "type": "bool"
    
    279        }
    
    280      ],
    
    281      "stateMutability": "nonpayable",
    
    282      "type": "function"
    
    283    }
    
    284  ],
    
    285  "evm": {
    
    286    "bytecode": {
    
    287      "linkReferences": {},
    
    288      "object": "60806040523480156200001157600080fd5b506040516200153938038062001539833981810160405260208110156200003757600080fd5b81019080805190602001909291905050506040518060400160405280600581526020017f42617369630000000000000000000000000000000000000000000000000000008152506040518060400160405280600381526020017f42534300000000000000000000000000000000000000000000000000000000008152508160039080519060200190620000cc92919062000389565b508060049080519060200190620000e592919062000389565b506012600560006101000a81548160ff021916908360ff16021790555050506200011633826200011d60201b60201c565b5062000438565b600073ffffffffffffffffffffffffffffffffffffffff168273ffffffffffffffffffffffffffffffffffffffff161415620001c1576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252601f8152602001807f45524332303a206d696e7420746f20746865207a65726f20616464726573730081525060200191505060405180910390fd5b620001d560008383620002fb60201b60201c565b620001f1816002546200030060201b62000f2d1790919060201c565b6002819055506200024f816000808573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020546200030060201b62000f2d1790919060201c565b6000808473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055508173ffffffffffffffffffffffffffffffffffffffff16600073ffffffffffffffffffffffffffffffffffffffff167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef836040518082815260200191505060405180910390a35050565b505050565b6000808284019050838110156200037f576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252601b8152602001807f536166654d6174683a206164646974696f6e206f766572666c6f77000000000081525060200191505060405180910390fd5b8091505092915050565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f10620003cc57805160ff1916838001178555620003fd565b82800160010185558215620003fd579182015b82811115620003fc578251825591602001919060010190620003df565b5b5090506200040c919062000410565b5090565b6200043591905b808211156200043157600081600090555060010162000417565b5090565b90565b6110f180620004486000396000f3fe608060405234801561001057600080fd5b50600436106100a95760003560e01c80633950935111610071578063395093511461025f57806370a08231146102c557806395d89b411461031d578063a457c2d7146103a0578063a9059cbb14610406578063dd62ed3e1461046c576100a9565b806306fdde03146100ae578063095ea7b31461013157806318160ddd1461019757806323b872dd146101b5578063313ce5671461023b575b600080fd5b6100b66104e4565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156100f65780820151818401526020810190506100db565b50505050905090810190601f1680156101235780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b61017d6004803603604081101561014757600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610586565b604051808215151515815260200191505060405180910390f35b61019f6105a4565b6040518082815260200191505060405180910390f35b610221600480360360608110156101cb57600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291905050506105ae565b604051808215151515815260200191505060405180910390f35b610243610687565b604051808260ff1660ff16815260200191505060405180910390f35b6102ab6004803603604081101561027557600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291908035906020019092919050505061069e565b604051808215151515815260200191505060405180910390f35b610307600480360360208110156102db57600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190505050610751565b6040518082815260200191505060405180910390f35b610325610799565b6040518080602001828103825283818151815260200191508051906020019080838360005b8381101561036557808201518184015260208101905061034a565b50505050905090810190601f1680156103925780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b6103ec600480360360408110156103b657600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291908035906020019092919050505061083b565b604051808215151515815260200191505060405180910390f35b6104526004803603604081101561041c57600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610908565b604051808215151515815260200191505060405180910390f35b6104ce6004803603604081101561048257600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190505050610926565b6040518082815260200191505060405180910390f35b606060038054600181600116156101000203166002900480601f01602080910402602001604051908101604052809291908181526020018280546001816001161561010002031660029004801561057c5780601f106105515761010080835404028352916020019161057c565b820191906000526020600020905b81548152906001019060200180831161055f57829003601f168201915b5050505050905090565b600061059a6105936109ad565b84846109b5565b6001905092915050565b6000600254905090565b60006105bb848484610bac565b61067c846105c76109ad565b6106778560405180606001604052806028815260200161102660289139600160008b73ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020600061062d6109ad565b73ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054610e6d9092919063ffffffff16565b6109b5565b600190509392505050565b6000600560009054906101000a900460ff16905090565b60006107476106ab6109ad565b8461074285600160006106bc6109ad565b73ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008973ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054610f2d90919063ffffffff16565b6109b5565b6001905092915050565b60008060008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020549050919050565b606060048054600181600116156101000203166002900480601f0160208091040260200160405190810160405280929190818152602001828054600181600116156101000203166002900480156108315780601f1061080657610100808354040283529160200191610831565b820191906000526020600020905b81548152906001019060200180831161081457829003601f168201915b5050505050905090565b60006108fe6108486109ad565b846108f98560405180606001604052806025815260200161109760259139600160006108726109ad565b73ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008a73ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054610e6d9092919063ffffffff16565b6109b5565b6001905092915050565b600061091c6109156109ad565b8484610bac565b6001905092915050565b6000600160008473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054905092915050565b600033905090565b600073ffffffffffffffffffffffffffffffffffffffff168373ffffffffffffffffffffffffffffffffffffffff161415610a3b576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260248152602001806110736024913960400191505060405180910390fd5b600073ffffffffffffffffffffffffffffffffffffffff168273ffffffffffffffffffffffffffffffffffffffff161415610ac1576040517f08c379a0000000000000000000000000000000000000000000000000000000008152600401808060200182810382526022815260200180610fde6022913960400191505060405180910390fd5b80600160008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055508173ffffffffffffffffffffffffffffffffffffffff168373ffffffffffffffffffffffffffffffffffffffff167f8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925836040518082815260200191505060405180910390a3505050565b600073ffffffffffffffffffffffffffffffffffffffff168373ffffffffffffffffffffffffffffffffffffffff161415610c32576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252602581526020018061104e6025913960400191505060405180910390fd5b600073ffffffffffffffffffffffffffffffffffffffff168273ffffffffffffffffffffffffffffffffffffffff161415610cb8576040517f08c379a0000000000000000000000000000000000000000000000000000000008152600401808060200182810382526023815260200180610fbb6023913960400191505060405180910390fd5b610cc3838383610fb5565b610d2e81604051806060016040528060268152602001611000602691396000808773ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054610e6d9092919063ffffffff16565b6000808573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002081905550610dc1816000808573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054610f2d90919063ffffffff16565b6000808473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055508173ffffffffffffffffffffffffffffffffffffffff168373ffffffffffffffffffffffffffffffffffffffff167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef836040518082815260200191505060405180910390a3505050565b6000838311158290610f1a576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825283818151815260200191508051906020019080838360005b83811015610edf578082015181840152602081019050610ec4565b50505050905090810190601f168015610f0c5780820380516001836020036101000a031916815260200191505b509250505060405180910390fd5b5060008385039050809150509392505050565b600080828401905083811015610fab576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252601b8152602001807f536166654d6174683a206164646974696f6e206f766572666c6f77000000000081525060200191505060405180910390fd5b8091505092915050565b50505056fe45524332303a207472616e7366657220746f20746865207a65726f206164647265737345524332303a20617070726f766520746f20746865207a65726f206164647265737345524332303a207472616e7366657220616d6f756e7420657863656564732062616c616e636545524332303a207472616e7366657220616d6f756e74206578636565647320616c6c6f77616e636545524332303a207472616e736665722066726f6d20746865207a65726f206164647265737345524332303a20617070726f76652066726f6d20746865207a65726f206164647265737345524332303a2064656372656173656420616c6c6f77616e63652062656c6f77207a65726fa264697066735822122081c840f087cef92feccb03fadc678b2708c331896ec5432b5d4c675f27b6d3e664736f6c63430006020033",
    
    289      "opcodes": "PUSH1 0x80 PUSH1 0x40 MSTORE CALLVALUE DUP1 ISZERO PUSH3 0x11 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST POP PUSH1 0x40 MLOAD PUSH3 0x1539 CODESIZE SUB DUP1 PUSH3 0x1539 DUP4 CODECOPY DUP2 DUP2 ADD PUSH1 0x40 MSTORE PUSH1 0x20 DUP2 LT ISZERO PUSH3 0x37 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST DUP2 ADD SWAP1 DUP1 DUP1 MLOAD SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 POP POP POP PUSH1 0x40 MLOAD DUP1 PUSH1 0x40 ADD PUSH1 0x40 MSTORE DUP1 PUSH1 0x5 DUP2 MSTORE PUSH1 0x20 ADD PUSH32 0x4261736963000000000000000000000000000000000000000000000000000000 DUP2 MSTORE POP PUSH1 0x40 MLOAD DUP1 PUSH1 0x40 ADD PUSH1 0x40 MSTORE DUP1 PUSH1 0x3 DUP2 MSTORE PUSH1 0x20 ADD PUSH32 0x4253430000000000000000000000000000000000000000000000000000000000 DUP2 MSTORE POP DUP2 PUSH1 0x3 SWAP1 DUP1 MLOAD SWAP1 PUSH1 0x20 ADD SWAP1 PUSH3 0xCC SWAP3 SWAP2 SWAP1 PUSH3 0x389 JUMP JUMPDEST POP DUP1 PUSH1 0x4 SWAP1 DUP1 MLOAD SWAP1 PUSH1 0x20 ADD SWAP1 PUSH3 0xE5 SWAP3 SWAP2 SWAP1 PUSH3 0x389 JUMP JUMPDEST POP PUSH1 0x12 PUSH1 0x5 PUSH1 0x0 PUSH2 0x100 EXP DUP2 SLOAD DUP2 PUSH1 0xFF MUL NOT AND SWAP1 DUP4 PUSH1 0xFF AND MUL OR SWAP1 SSTORE POP POP POP PUSH3 0x116 CALLER DUP3 PUSH3 0x11D PUSH1 0x20 SHL PUSH1 0x20 SHR JUMP JUMPDEST POP PUSH3 0x438 JUMP JUMPDEST PUSH1 0x0 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP3 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND EQ ISZERO PUSH3 0x1C1 JUMPI PUSH1 0x40 MLOAD PUSH32 0x8C379A000000000000000000000000000000000000000000000000000000000 DUP2 MSTORE PUSH1 0x4 ADD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE PUSH1 0x1F DUP2 MSTORE PUSH1 0x20 ADD DUP1 PUSH32 0x45524332303A206D696E7420746F20746865207A65726F206164647265737300 DUP2 MSTORE POP PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 REVERT JUMPDEST PUSH3 0x1D5 PUSH1 0x0 DUP4 DUP4 PUSH3 0x2FB PUSH1 0x20 SHL PUSH1 0x20 SHR JUMP JUMPDEST PUSH3 0x1F1 DUP2 PUSH1 0x2 SLOAD PUSH3 0x300 PUSH1 0x20 SHL PUSH3 0xF2D OR SWAP1 SWAP2 SWAP1 PUSH1 0x20 SHR JUMP JUMPDEST PUSH1 0x2 DUP2 SWAP1 SSTORE POP PUSH3 0x24F DUP2 PUSH1 0x0 DUP1 DUP6 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 SLOAD PUSH3 0x300 PUSH1 0x20 SHL PUSH3 0xF2D OR SWAP1 SWAP2 SWAP1 PUSH1 0x20 SHR JUMP JUMPDEST PUSH1 0x0 DUP1 DUP5 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 DUP2 SWAP1 SSTORE POP DUP2 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH1 0x0 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH32 0xDDF252AD1BE2C89B69C2B068FC378DAA952BA7F163C4A11628F55A4DF523B3EF DUP4 PUSH1 0x40 MLOAD DUP1 DUP3 DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 LOG3 POP POP JUMP JUMPDEST POP POP POP JUMP JUMPDEST PUSH1 0x0 DUP1 DUP3 DUP5 ADD SWAP1 POP DUP4 DUP2 LT ISZERO PUSH3 0x37F JUMPI PUSH1 0x40 MLOAD PUSH32 0x8C379A000000000000000000000000000000000000000000000000000000000 DUP2 MSTORE PUSH1 0x4 ADD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE PUSH1 0x1B DUP2 MSTORE PUSH1 0x20 ADD DUP1 PUSH32 0x536166654D6174683A206164646974696F6E206F766572666C6F770000000000 DUP2 MSTORE POP PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 REVERT JUMPDEST DUP1 SWAP2 POP POP SWAP3 SWAP2 POP POP JUMP JUMPDEST DUP3 DUP1 SLOAD PUSH1 0x1 DUP2 PUSH1 0x1 AND ISZERO PUSH2 0x100 MUL SUB AND PUSH1 0x2 SWAP1 DIV SWAP1 PUSH1 0x0 MSTORE PUSH1 0x20 PUSH1 0x0 KECCAK256 SWAP1 PUSH1 0x1F ADD PUSH1 0x20 SWAP1 DIV DUP2 ADD SWAP3 DUP3 PUSH1 0x1F LT PUSH3 0x3CC JUMPI DUP1 MLOAD PUSH1 0xFF NOT AND DUP4 DUP1 ADD OR DUP6 SSTORE PUSH3 0x3FD JUMP JUMPDEST DUP3 DUP1 ADD PUSH1 0x1 ADD DUP6 SSTORE DUP3 ISZERO PUSH3 0x3FD JUMPI SWAP2 DUP3 ADD JUMPDEST DUP3 DUP2 GT ISZERO PUSH3 0x3FC JUMPI DUP3 MLOAD DUP3 SSTORE SWAP2 PUSH1 0x20 ADD SWAP2 SWAP1 PUSH1 0x1 ADD SWAP1 PUSH3 0x3DF JUMP JUMPDEST JUMPDEST POP SWAP1 POP PUSH3 0x40C SWAP2 SWAP1 PUSH3 0x410 JUMP JUMPDEST POP SWAP1 JUMP JUMPDEST PUSH3 0x435 SWAP2 SWAP1 JUMPDEST DUP1 DUP3 GT ISZERO PUSH3 0x431 JUMPI PUSH1 0x0 DUP2 PUSH1 0x0 SWAP1 SSTORE POP PUSH1 0x1 ADD PUSH3 0x417 JUMP JUMPDEST POP SWAP1 JUMP JUMPDEST SWAP1 JUMP JUMPDEST PUSH2 0x10F1 DUP1 PUSH3 0x448 PUSH1 0x0 CODECOPY PUSH1 0x0 RETURN INVALID PUSH1 0x80 PUSH1 0x40 MSTORE CALLVALUE DUP1 ISZERO PUSH2 0x10 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST POP PUSH1 0x4 CALLDATASIZE LT PUSH2 0xA9 JUMPI PUSH1 0x0 CALLDATALOAD PUSH1 0xE0 SHR DUP1 PUSH4 0x39509351 GT PUSH2 0x71 JUMPI DUP1 PUSH4 0x39509351 EQ PUSH2 0x25F JUMPI DUP1 PUSH4 0x70A08231 EQ PUSH2 0x2C5 JUMPI DUP1 PUSH4 0x95D89B41 EQ PUSH2 0x31D JUMPI DUP1 PUSH4 0xA457C2D7 EQ PUSH2 0x3A0 JUMPI DUP1 PUSH4 0xA9059CBB EQ PUSH2 0x406 JUMPI DUP1 PUSH4 0xDD62ED3E EQ PUSH2 0x46C JUMPI PUSH2 0xA9 JUMP JUMPDEST DUP1 PUSH4 0x6FDDE03 EQ PUSH2 0xAE JUMPI DUP1 PUSH4 0x95EA7B3 EQ PUSH2 0x131 JUMPI DUP1 PUSH4 0x18160DDD EQ PUSH2 0x197 JUMPI DUP1 PUSH4 0x23B872DD EQ PUSH2 0x1B5 JUMPI DUP1 PUSH4 0x313CE567 EQ PUSH2 0x23B JUMPI JUMPDEST PUSH1 0x0 DUP1 REVERT JUMPDEST PUSH2 0xB6 PUSH2 0x4E4 JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE DUP4 DUP2 DUP2 MLOAD DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP DUP1 MLOAD SWAP1 PUSH1 0x20 ADD SWAP1 DUP1 DUP4 DUP4 PUSH1 0x0 JUMPDEST DUP4 DUP2 LT ISZERO PUSH2 0xF6 JUMPI DUP1 DUP3 ADD MLOAD DUP2 DUP5 ADD MSTORE PUSH1 0x20 DUP2 ADD SWAP1 POP PUSH2 0xDB JUMP JUMPDEST POP POP POP POP SWAP1 POP SWAP1 DUP2 ADD SWAP1 PUSH1 0x1F AND DUP1 ISZERO PUSH2 0x123 JUMPI DUP1 DUP3 SUB DUP1 MLOAD PUSH1 0x1 DUP4 PUSH1 0x20 SUB PUSH2 0x100 EXP SUB NOT AND DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP JUMPDEST POP SWAP3 POP POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x17D PUSH1 0x4 DUP1 CALLDATASIZE SUB PUSH1 0x40 DUP2 LT ISZERO PUSH2 0x147 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST DUP2 ADD SWAP1 DUP1 DUP1 CALLDATALOAD PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 DUP1 CALLDATALOAD SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 POP POP POP PUSH2 0x586 JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP3 ISZERO ISZERO ISZERO ISZERO DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x19F PUSH2 0x5A4 JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP3 DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x221 PUSH1 0x4 DUP1 CALLDATASIZE SUB PUSH1 0x60 DUP2 LT ISZERO PUSH2 0x1CB JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST DUP2 ADD SWAP1 DUP1 DUP1 CALLDATALOAD PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 DUP1 CALLDATALOAD PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 DUP1 CALLDATALOAD SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 POP POP POP PUSH2 0x5AE JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP3 ISZERO ISZERO ISZERO ISZERO DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x243 PUSH2 0x687 JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP3 PUSH1 0xFF AND PUSH1 0xFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x2AB PUSH1 0x4 DUP1 CALLDATASIZE SUB PUSH1 0x40 DUP2 LT ISZERO PUSH2 0x275 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST DUP2 ADD SWAP1 DUP1 DUP1 CALLDATALOAD PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 DUP1 CALLDATALOAD SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 POP POP POP PUSH2 0x69E JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP3 ISZERO ISZERO ISZERO ISZERO DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x307 PUSH1 0x4 DUP1 CALLDATASIZE SUB PUSH1 0x20 DUP2 LT ISZERO PUSH2 0x2DB JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST DUP2 ADD SWAP1 DUP1 DUP1 CALLDATALOAD PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 POP POP POP PUSH2 0x751 JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP3 DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x325 PUSH2 0x799 JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE DUP4 DUP2 DUP2 MLOAD DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP DUP1 MLOAD SWAP1 PUSH1 0x20 ADD SWAP1 DUP1 DUP4 DUP4 PUSH1 0x0 JUMPDEST DUP4 DUP2 LT ISZERO PUSH2 0x365 JUMPI DUP1 DUP3 ADD MLOAD DUP2 DUP5 ADD MSTORE PUSH1 0x20 DUP2 ADD SWAP1 POP PUSH2 0x34A JUMP JUMPDEST POP POP POP POP SWAP1 POP SWAP1 DUP2 ADD SWAP1 PUSH1 0x1F AND DUP1 ISZERO PUSH2 0x392 JUMPI DUP1 DUP3 SUB DUP1 MLOAD PUSH1 0x1 DUP4 PUSH1 0x20 SUB PUSH2 0x100 EXP SUB NOT AND DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP JUMPDEST POP SWAP3 POP POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x3EC PUSH1 0x4 DUP1 CALLDATASIZE SUB PUSH1 0x40 DUP2 LT ISZERO PUSH2 0x3B6 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST DUP2 ADD SWAP1 DUP1 DUP1 CALLDATALOAD PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 DUP1 CALLDATALOAD SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 POP POP POP PUSH2 0x83B JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP3 ISZERO ISZERO ISZERO ISZERO DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x452 PUSH1 0x4 DUP1 CALLDATASIZE SUB PUSH1 0x40 DUP2 LT ISZERO PUSH2 0x41C JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST DUP2 ADD SWAP1 DUP1 DUP1 CALLDATALOAD PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 DUP1 CALLDATALOAD SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 POP POP POP PUSH2 0x908 JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP3 ISZERO ISZERO ISZERO ISZERO DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x4CE PUSH1 0x4 DUP1 CALLDATASIZE SUB PUSH1 0x40 DUP2 LT ISZERO PUSH2 0x482 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST DUP2 ADD SWAP1 DUP1 DUP1 CALLDATALOAD PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 DUP1 CALLDATALOAD PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 POP POP POP PUSH2 0x926 JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP3 DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH1 0x60 PUSH1 0x3 DUP1 SLOAD PUSH1 0x1 DUP2 PUSH1 0x1 AND ISZERO PUSH2 0x100 MUL SUB AND PUSH1 0x2 SWAP1 DIV DUP1 PUSH1 0x1F ADD PUSH1 0x20 DUP1 SWAP2 DIV MUL PUSH1 0x20 ADD PUSH1 0x40 MLOAD SWAP1 DUP2 ADD PUSH1 0x40 MSTORE DUP1 SWAP3 SWAP2 SWAP1 DUP2 DUP2 MSTORE PUSH1 0x20 ADD DUP3 DUP1 SLOAD PUSH1 0x1 DUP2 PUSH1 0x1 AND ISZERO PUSH2 0x100 MUL SUB AND PUSH1 0x2 SWAP1 DIV DUP1 ISZERO PUSH2 0x57C JUMPI DUP1 PUSH1 0x1F LT PUSH2 0x551 JUMPI PUSH2 0x100 DUP1 DUP4 SLOAD DIV MUL DUP4 MSTORE SWAP2 PUSH1 0x20 ADD SWAP2 PUSH2 0x57C JUMP JUMPDEST DUP3 ADD SWAP2 SWAP1 PUSH1 0x0 MSTORE PUSH1 0x20 PUSH1 0x0 KECCAK256 SWAP1 JUMPDEST DUP2 SLOAD DUP2 MSTORE SWAP1 PUSH1 0x1 ADD SWAP1 PUSH1 0x20 ADD DUP1 DUP4 GT PUSH2 0x55F JUMPI DUP3 SWAP1 SUB PUSH1 0x1F AND DUP3 ADD SWAP2 JUMPDEST POP POP POP POP POP SWAP1 POP SWAP1 JUMP JUMPDEST PUSH1 0x0 PUSH2 0x59A PUSH2 0x593 PUSH2 0x9AD JUMP JUMPDEST DUP5 DUP5 PUSH2 0x9B5 JUMP JUMPDEST PUSH1 0x1 SWAP1 POP SWAP3 SWAP2 POP POP JUMP JUMPDEST PUSH1 0x0 PUSH1 0x2 SLOAD SWAP1 POP SWAP1 JUMP JUMPDEST PUSH1 0x0 PUSH2 0x5BB DUP5 DUP5 DUP5 PUSH2 0xBAC JUMP JUMPDEST PUSH2 0x67C DUP5 PUSH2 0x5C7 PUSH2 0x9AD JUMP JUMPDEST PUSH2 0x677 DUP6 PUSH1 0x40 MLOAD DUP1 PUSH1 0x60 ADD PUSH1 0x40 MSTORE DUP1 PUSH1 0x28 DUP2 MSTORE PUSH1 0x20 ADD PUSH2 0x1026 PUSH1 0x28 SWAP2 CODECOPY PUSH1 0x1 PUSH1 0x0 DUP12 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 PUSH1 0x0 PUSH2 0x62D PUSH2 0x9AD JUMP JUMPDEST PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 SLOAD PUSH2 0xE6D SWAP1 SWAP3 SWAP2 SWAP1 PUSH4 0xFFFFFFFF AND JUMP JUMPDEST PUSH2 0x9B5 JUMP JUMPDEST PUSH1 0x1 SWAP1 POP SWAP4 SWAP3 POP POP POP JUMP JUMPDEST PUSH1 0x0 PUSH1 0x5 PUSH1 0x0 SWAP1 SLOAD SWAP1 PUSH2 0x100 EXP SWAP1 DIV PUSH1 0xFF AND SWAP1 POP SWAP1 JUMP JUMPDEST PUSH1 0x0 PUSH2 0x747 PUSH2 0x6AB PUSH2 0x9AD JUMP JUMPDEST DUP5 PUSH2 0x742 DUP6 PUSH1 0x1 PUSH1 0x0 PUSH2 0x6BC PUSH2 0x9AD JUMP JUMPDEST PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 PUSH1 0x0 DUP10 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 SLOAD PUSH2 0xF2D SWAP1 SWAP2 SWAP1 PUSH4 0xFFFFFFFF AND JUMP JUMPDEST PUSH2 0x9B5 JUMP JUMPDEST PUSH1 0x1 SWAP1 POP SWAP3 SWAP2 POP POP JUMP JUMPDEST PUSH1 0x0 DUP1 PUSH1 0x0 DUP4 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 SLOAD SWAP1 POP SWAP2 SWAP1 POP JUMP JUMPDEST PUSH1 0x60 PUSH1 0x4 DUP1 SLOAD PUSH1 0x1 DUP2 PUSH1 0x1 AND ISZERO PUSH2 0x100 MUL SUB AND PUSH1 0x2 SWAP1 DIV DUP1 PUSH1 0x1F ADD PUSH1 0x20 DUP1 SWAP2 DIV MUL PUSH1 0x20 ADD PUSH1 0x40 MLOAD SWAP1 DUP2 ADD PUSH1 0x40 MSTORE DUP1 SWAP3 SWAP2 SWAP1 DUP2 DUP2 MSTORE PUSH1 0x20 ADD DUP3 DUP1 SLOAD PUSH1 0x1 DUP2 PUSH1 0x1 AND ISZERO PUSH2 0x100 MUL SUB AND PUSH1 0x2 SWAP1 DIV DUP1 ISZERO PUSH2 0x831 JUMPI DUP1 PUSH1 0x1F LT PUSH2 0x806 JUMPI PUSH2 0x100 DUP1 DUP4 SLOAD DIV MUL DUP4 MSTORE SWAP2 PUSH1 0x20 ADD SWAP2 PUSH2 0x831 JUMP JUMPDEST DUP3 ADD SWAP2 SWAP1 PUSH1 0x0 MSTORE PUSH1 0x20 PUSH1 0x0 KECCAK256 SWAP1 JUMPDEST DUP2 SLOAD DUP2 MSTORE SWAP1 PUSH1 0x1 ADD SWAP1 PUSH1 0x20 ADD DUP1 DUP4 GT PUSH2 0x814 JUMPI DUP3 SWAP1 SUB PUSH1 0x1F AND DUP3 ADD SWAP2 JUMPDEST POP POP POP POP POP SWAP1 POP SWAP1 JUMP JUMPDEST PUSH1 0x0 PUSH2 0x8FE PUSH2 0x848 PUSH2 0x9AD JUMP JUMPDEST DUP5 PUSH2 0x8F9 DUP6 PUSH1 0x40 MLOAD DUP1 PUSH1 0x60 ADD PUSH1 0x40 MSTORE DUP1 PUSH1 0x25 DUP2 MSTORE PUSH1 0x20 ADD PUSH2 0x1097 PUSH1 0x25 SWAP2 CODECOPY PUSH1 0x1 PUSH1 0x0 PUSH2 0x872 PUSH2 0x9AD JUMP JUMPDEST PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 PUSH1 0x0 DUP11 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 SLOAD PUSH2 0xE6D SWAP1 SWAP3 SWAP2 SWAP1 PUSH4 0xFFFFFFFF AND JUMP JUMPDEST PUSH2 0x9B5 JUMP JUMPDEST PUSH1 0x1 SWAP1 POP SWAP3 SWAP2 POP POP JUMP JUMPDEST PUSH1 0x0 PUSH2 0x91C PUSH2 0x915 PUSH2 0x9AD JUMP JUMPDEST DUP5 DUP5 PUSH2 0xBAC JUMP JUMPDEST PUSH1 0x1 SWAP1 POP SWAP3 SWAP2 POP POP JUMP JUMPDEST PUSH1 0x0 PUSH1 0x1 PUSH1 0x0 DUP5 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 PUSH1 0x0 DUP4 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 SLOAD SWAP1 POP SWAP3 SWAP2 POP POP JUMP JUMPDEST PUSH1 0x0 CALLER SWAP1 POP SWAP1 JUMP JUMPDEST PUSH1 0x0 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP4 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND EQ ISZERO PUSH2 0xA3B JUMPI PUSH1 0x40 MLOAD PUSH32 0x8C379A000000000000000000000000000000000000000000000000000000000 DUP2 MSTORE PUSH1 0x4 ADD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE PUSH1 0x24 DUP2 MSTORE PUSH1 0x20 ADD DUP1 PUSH2 0x1073 PUSH1 0x24 SWAP2 CODECOPY PUSH1 0x40 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 REVERT JUMPDEST PUSH1 0x0 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP3 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND EQ ISZERO PUSH2 0xAC1 JUMPI PUSH1 0x40 MLOAD PUSH32 0x8C379A000000000000000000000000000000000000000000000000000000000 DUP2 MSTORE PUSH1 0x4 ADD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE PUSH1 0x22 DUP2 MSTORE PUSH1 0x20 ADD DUP1 PUSH2 0xFDE PUSH1 0x22 SWAP2 CODECOPY PUSH1 0x40 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 REVERT JUMPDEST DUP1 PUSH1 0x1 PUSH1 0x0 DUP6 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 PUSH1 0x0 DUP5 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 DUP2 SWAP1 SSTORE POP DUP2 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP4 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH32 0x8C5BE1E5EBEC7D5BD14F71427D1E84F3DD0314C0F7B2291E5B200AC8C7C3B925 DUP4 PUSH1 0x40 MLOAD DUP1 DUP3 DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 LOG3 POP POP POP JUMP JUMPDEST PUSH1 0x0 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP4 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND EQ ISZERO PUSH2 0xC32 JUMPI PUSH1 0x40 MLOAD PUSH32 0x8C379A000000000000000000000000000000000000000000000000000000000 DUP2 MSTORE PUSH1 0x4 ADD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE PUSH1 0x25 DUP2 MSTORE PUSH1 0x20 ADD DUP1 PUSH2 0x104E PUSH1 0x25 SWAP2 CODECOPY PUSH1 0x40 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 REVERT JUMPDEST PUSH1 0x0 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP3 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND EQ ISZERO PUSH2 0xCB8 JUMPI PUSH1 0x40 MLOAD PUSH32 0x8C379A000000000000000000000000000000000000000000000000000000000 DUP2 MSTORE PUSH1 0x4 ADD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE PUSH1 0x23 DUP2 MSTORE PUSH1 0x20 ADD DUP1 PUSH2 0xFBB PUSH1 0x23 SWAP2 CODECOPY PUSH1 0x40 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 REVERT JUMPDEST PUSH2 0xCC3 DUP4 DUP4 DUP4 PUSH2 0xFB5 JUMP JUMPDEST PUSH2 0xD2E DUP2 PUSH1 0x40 MLOAD DUP1 PUSH1 0x60 ADD PUSH1 0x40 MSTORE DUP1 PUSH1 0x26 DUP2 MSTORE PUSH1 0x20 ADD PUSH2 0x1000 PUSH1 0x26 SWAP2 CODECOPY PUSH1 0x0 DUP1 DUP8 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 SLOAD PUSH2 0xE6D SWAP1 SWAP3 SWAP2 SWAP1 PUSH4 0xFFFFFFFF AND JUMP JUMPDEST PUSH1 0x0 DUP1 DUP6 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 DUP2 SWAP1 SSTORE POP PUSH2 0xDC1 DUP2 PUSH1 0x0 DUP1 DUP6 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 SLOAD PUSH2 0xF2D SWAP1 SWAP2 SWAP1 PUSH4 0xFFFFFFFF AND JUMP JUMPDEST PUSH1 0x0 DUP1 DUP5 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 DUP2 SWAP1 SSTORE POP DUP2 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP4 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH32 0xDDF252AD1BE2C89B69C2B068FC378DAA952BA7F163C4A11628F55A4DF523B3EF DUP4 PUSH1 0x40 MLOAD DUP1 DUP3 DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 LOG3 POP POP POP JUMP JUMPDEST PUSH1 0x0 DUP4 DUP4 GT ISZERO DUP3 SWAP1 PUSH2 0xF1A JUMPI PUSH1 0x40 MLOAD PUSH32 0x8C379A000000000000000000000000000000000000000000000000000000000 DUP2 MSTORE PUSH1 0x4 ADD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE DUP4 DUP2 DUP2 MLOAD DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP DUP1 MLOAD SWAP1 PUSH1 0x20 ADD SWAP1 DUP1 DUP4 DUP4 PUSH1 0x0 JUMPDEST DUP4 DUP2 LT ISZERO PUSH2 0xEDF JUMPI DUP1 DUP3 ADD MLOAD DUP2 DUP5 ADD MSTORE PUSH1 0x20 DUP2 ADD SWAP1 POP PUSH2 0xEC4 JUMP JUMPDEST POP POP POP POP SWAP1 POP SWAP1 DUP2 ADD SWAP1 PUSH1 0x1F AND DUP1 ISZERO PUSH2 0xF0C JUMPI DUP1 DUP3 SUB DUP1 MLOAD PUSH1 0x1 DUP4 PUSH1 0x20 SUB PUSH2 0x100 EXP SUB NOT AND DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP JUMPDEST POP SWAP3 POP POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 REVERT JUMPDEST POP PUSH1 0x0 DUP4 DUP6 SUB SWAP1 POP DUP1 SWAP2 POP POP SWAP4 SWAP3 POP POP POP JUMP JUMPDEST PUSH1 0x0 DUP1 DUP3 DUP5 ADD SWAP1 POP DUP4 DUP2 LT ISZERO PUSH2 0xFAB JUMPI PUSH1 0x40 MLOAD PUSH32 0x8C379A000000000000000000000000000000000000000000000000000000000 DUP2 MSTORE PUSH1 0x4 ADD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE PUSH1 0x1B DUP2 MSTORE PUSH1 0x20 ADD DUP1 PUSH32 0x536166654D6174683A206164646974696F6E206F766572666C6F770000000000 DUP2 MSTORE POP PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 REVERT JUMPDEST DUP1 SWAP2 POP POP SWAP3 SWAP2 POP POP JUMP JUMPDEST POP POP POP JUMP INVALID GASLIMIT MSTORE NUMBER ORIGIN ADDRESS GASPRICE KECCAK256 PUSH21 0x72616E7366657220746F20746865207A65726F2061 PUSH5 0x6472657373 GASLIMIT MSTORE NUMBER ORIGIN ADDRESS GASPRICE KECCAK256 PUSH2 0x7070 PUSH19 0x6F766520746F20746865207A65726F20616464 PUSH19 0x65737345524332303A207472616E7366657220 PUSH2 0x6D6F PUSH22 0x6E7420657863656564732062616C616E636545524332 ADDRESS GASPRICE KECCAK256 PUSH21 0x72616E7366657220616D6F756E7420657863656564 PUSH20 0x20616C6C6F77616E636545524332303A20747261 PUSH15 0x736665722066726F6D20746865207A PUSH6 0x726F20616464 PUSH19 0x65737345524332303A20617070726F76652066 PUSH19 0x6F6D20746865207A65726F2061646472657373 GASLIMIT MSTORE NUMBER ORIGIN ADDRESS GASPRICE KECCAK256 PUSH5 0x6563726561 PUSH20 0x656420616C6C6F77616E63652062656C6F77207A PUSH6 0x726FA2646970 PUSH7 0x735822122081C8 BLOCKHASH CREATE DUP8 0xCE 0xF9 0x2F 0xEC 0xCB SUB STATICCALL 0xDC PUSH8 0x8B2708C331896EC5 NUMBER 0x2B 0x5D 0x4C PUSH8 0x5F27B6D3E664736F PUSH13 0x63430006020033000000000000 ",
    
    290      "sourceMap": "142:152:5:-:0;;;177:115;8:9:-1;5:2;;;30:1;27;20:12;5:2;177:115:5;;;;;;;;;;;;;;;13:2:-1;8:3;5:11;2:2;;;29:1;26;19:12;2:2;177:115:5;;;;;;;;;;;;;;;;2013:141:2;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;2093:4;2085:5;:12;;;;;;;;;;;;:::i;:::-;;2117:6;2107:7;:16;;;;;;;;;;;;:::i;:::-;;2145:2;2133:9;;:14;;;;;;;;;;;;;;;;;;2013:141;;252:33:5::1;258:10;270:14;252:5;;;:33;;:::i;:::-;177:115:::0;142:152;;7835:370:2;7937:1;7918:21;;:7;:21;;;;7910:65;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;7986:49;8015:1;8019:7;8028:6;7986:20;;;:49;;:::i;:::-;8061:24;8078:6;8061:12;;:16;;;;;;:24;;;;:::i;:::-;8046:12;:39;;;;8116:30;8139:6;8116:9;:18;8126:7;8116:18;;;;;;;;;;;;;;;;:22;;;;;;:30;;;;:::i;:::-;8095:9;:18;8105:7;8095:18;;;;;;;;;;;;;;;:51;;;;8182:7;8161:37;;8178:1;8161:37;;;8191:6;8161:37;;;;;;;;;;;;;;;;;;7835:370;;:::o;10695:92::-;;;;:::o;874:176:1:-;932:7;951:9;967:1;963;:5;951:17;;991:1;986;:6;;978:46;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;1042:1;1035:8;;;874:176;;;;:::o;142:152:5:-;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;:::i;:::-;;;:::o;:::-;;;;;;;;;;;;;;;;;;;;;;;;;;;:::o;:::-;;;;;;;"
    
    291    },
    
    292    "deployedBytecode": {
    
    293      "linkReferences": {},
    
    294      "object": "608060405234801561001057600080fd5b50600436106100a95760003560e01c80633950935111610071578063395093511461025f57806370a08231146102c557806395d89b411461031d578063a457c2d7146103a0578063a9059cbb14610406578063dd62ed3e1461046c576100a9565b806306fdde03146100ae578063095ea7b31461013157806318160ddd1461019757806323b872dd146101b5578063313ce5671461023b575b600080fd5b6100b66104e4565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156100f65780820151818401526020810190506100db565b50505050905090810190601f1680156101235780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b61017d6004803603604081101561014757600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610586565b604051808215151515815260200191505060405180910390f35b61019f6105a4565b6040518082815260200191505060405180910390f35b610221600480360360608110156101cb57600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291905050506105ae565b604051808215151515815260200191505060405180910390f35b610243610687565b604051808260ff1660ff16815260200191505060405180910390f35b6102ab6004803603604081101561027557600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291908035906020019092919050505061069e565b604051808215151515815260200191505060405180910390f35b610307600480360360208110156102db57600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190505050610751565b6040518082815260200191505060405180910390f35b610325610799565b6040518080602001828103825283818151815260200191508051906020019080838360005b8381101561036557808201518184015260208101905061034a565b50505050905090810190601f1680156103925780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b6103ec600480360360408110156103b657600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291908035906020019092919050505061083b565b604051808215151515815260200191505060405180910390f35b6104526004803603604081101561041c57600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610908565b604051808215151515815260200191505060405180910390f35b6104ce6004803603604081101561048257600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190505050610926565b6040518082815260200191505060405180910390f35b606060038054600181600116156101000203166002900480601f01602080910402602001604051908101604052809291908181526020018280546001816001161561010002031660029004801561057c5780601f106105515761010080835404028352916020019161057c565b820191906000526020600020905b81548152906001019060200180831161055f57829003601f168201915b5050505050905090565b600061059a6105936109ad565b84846109b5565b6001905092915050565b6000600254905090565b60006105bb848484610bac565b61067c846105c76109ad565b6106778560405180606001604052806028815260200161102660289139600160008b73ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020600061062d6109ad565b73ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054610e6d9092919063ffffffff16565b6109b5565b600190509392505050565b6000600560009054906101000a900460ff16905090565b60006107476106ab6109ad565b8461074285600160006106bc6109ad565b73ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008973ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054610f2d90919063ffffffff16565b6109b5565b6001905092915050565b60008060008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020549050919050565b606060048054600181600116156101000203166002900480601f0160208091040260200160405190810160405280929190818152602001828054600181600116156101000203166002900480156108315780601f1061080657610100808354040283529160200191610831565b820191906000526020600020905b81548152906001019060200180831161081457829003601f168201915b5050505050905090565b60006108fe6108486109ad565b846108f98560405180606001604052806025815260200161109760259139600160006108726109ad565b73ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008a73ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054610e6d9092919063ffffffff16565b6109b5565b6001905092915050565b600061091c6109156109ad565b8484610bac565b6001905092915050565b6000600160008473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054905092915050565b600033905090565b600073ffffffffffffffffffffffffffffffffffffffff168373ffffffffffffffffffffffffffffffffffffffff161415610a3b576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260248152602001806110736024913960400191505060405180910390fd5b600073ffffffffffffffffffffffffffffffffffffffff168273ffffffffffffffffffffffffffffffffffffffff161415610ac1576040517f08c379a0000000000000000000000000000000000000000000000000000000008152600401808060200182810382526022815260200180610fde6022913960400191505060405180910390fd5b80600160008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055508173ffffffffffffffffffffffffffffffffffffffff168373ffffffffffffffffffffffffffffffffffffffff167f8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925836040518082815260200191505060405180910390a3505050565b600073ffffffffffffffffffffffffffffffffffffffff168373ffffffffffffffffffffffffffffffffffffffff161415610c32576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252602581526020018061104e6025913960400191505060405180910390fd5b600073ffffffffffffffffffffffffffffffffffffffff168273ffffffffffffffffffffffffffffffffffffffff161415610cb8576040517f08c379a0000000000000000000000000000000000000000000000000000000008152600401808060200182810382526023815260200180610fbb6023913960400191505060405180910390fd5b610cc3838383610fb5565b610d2e81604051806060016040528060268152602001611000602691396000808773ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054610e6d9092919063ffffffff16565b6000808573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002081905550610dc1816000808573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054610f2d90919063ffffffff16565b6000808473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055508173ffffffffffffffffffffffffffffffffffffffff168373ffffffffffffffffffffffffffffffffffffffff167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef836040518082815260200191505060405180910390a3505050565b6000838311158290610f1a576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825283818151815260200191508051906020019080838360005b83811015610edf578082015181840152602081019050610ec4565b50505050905090810190601f168015610f0c5780820380516001836020036101000a031916815260200191505b509250505060405180910390fd5b5060008385039050809150509392505050565b600080828401905083811015610fab576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252601b8152602001807f536166654d6174683a206164646974696f6e206f766572666c6f77000000000081525060200191505060405180910390fd5b8091505092915050565b50505056fe45524332303a207472616e7366657220746f20746865207a65726f206164647265737345524332303a20617070726f766520746f20746865207a65726f206164647265737345524332303a207472616e7366657220616d6f756e7420657863656564732062616c616e636545524332303a207472616e7366657220616d6f756e74206578636565647320616c6c6f77616e636545524332303a207472616e736665722066726f6d20746865207a65726f206164647265737345524332303a20617070726f76652066726f6d20746865207a65726f206164647265737345524332303a2064656372656173656420616c6c6f77616e63652062656c6f77207a65726fa264697066735822122081c840f087cef92feccb03fadc678b2708c331896ec5432b5d4c675f27b6d3e664736f6c63430006020033",
    
    295      "opcodes": "PUSH1 0x80 PUSH1 0x40 MSTORE CALLVALUE DUP1 ISZERO PUSH2 0x10 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST POP PUSH1 0x4 CALLDATASIZE LT PUSH2 0xA9 JUMPI PUSH1 0x0 CALLDATALOAD PUSH1 0xE0 SHR DUP1 PUSH4 0x39509351 GT PUSH2 0x71 JUMPI DUP1 PUSH4 0x39509351 EQ PUSH2 0x25F JUMPI DUP1 PUSH4 0x70A08231 EQ PUSH2 0x2C5 JUMPI DUP1 PUSH4 0x95D89B41 EQ PUSH2 0x31D JUMPI DUP1 PUSH4 0xA457C2D7 EQ PUSH2 0x3A0 JUMPI DUP1 PUSH4 0xA9059CBB EQ PUSH2 0x406 JUMPI DUP1 PUSH4 0xDD62ED3E EQ PUSH2 0x46C JUMPI PUSH2 0xA9 JUMP JUMPDEST DUP1 PUSH4 0x6FDDE03 EQ PUSH2 0xAE JUMPI DUP1 PUSH4 0x95EA7B3 EQ PUSH2 0x131 JUMPI DUP1 PUSH4 0x18160DDD EQ PUSH2 0x197 JUMPI DUP1 PUSH4 0x23B872DD EQ PUSH2 0x1B5 JUMPI DUP1 PUSH4 0x313CE567 EQ PUSH2 0x23B JUMPI JUMPDEST PUSH1 0x0 DUP1 REVERT JUMPDEST PUSH2 0xB6 PUSH2 0x4E4 JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE DUP4 DUP2 DUP2 MLOAD DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP DUP1 MLOAD SWAP1 PUSH1 0x20 ADD SWAP1 DUP1 DUP4 DUP4 PUSH1 0x0 JUMPDEST DUP4 DUP2 LT ISZERO PUSH2 0xF6 JUMPI DUP1 DUP3 ADD MLOAD DUP2 DUP5 ADD MSTORE PUSH1 0x20 DUP2 ADD SWAP1 POP PUSH2 0xDB JUMP JUMPDEST POP POP POP POP SWAP1 POP SWAP1 DUP2 ADD SWAP1 PUSH1 0x1F AND DUP1 ISZERO PUSH2 0x123 JUMPI DUP1 DUP3 SUB DUP1 MLOAD PUSH1 0x1 DUP4 PUSH1 0x20 SUB PUSH2 0x100 EXP SUB NOT AND DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP JUMPDEST POP SWAP3 POP POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x17D PUSH1 0x4 DUP1 CALLDATASIZE SUB PUSH1 0x40 DUP2 LT ISZERO PUSH2 0x147 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST DUP2 ADD SWAP1 DUP1 DUP1 CALLDATALOAD PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 DUP1 CALLDATALOAD SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 POP POP POP PUSH2 0x586 JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP3 ISZERO ISZERO ISZERO ISZERO DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x19F PUSH2 0x5A4 JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP3 DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x221 PUSH1 0x4 DUP1 CALLDATASIZE SUB PUSH1 0x60 DUP2 LT ISZERO PUSH2 0x1CB JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST DUP2 ADD SWAP1 DUP1 DUP1 CALLDATALOAD PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 DUP1 CALLDATALOAD PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 DUP1 CALLDATALOAD SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 POP POP POP PUSH2 0x5AE JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP3 ISZERO ISZERO ISZERO ISZERO DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x243 PUSH2 0x687 JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP3 PUSH1 0xFF AND PUSH1 0xFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x2AB PUSH1 0x4 DUP1 CALLDATASIZE SUB PUSH1 0x40 DUP2 LT ISZERO PUSH2 0x275 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST DUP2 ADD SWAP1 DUP1 DUP1 CALLDATALOAD PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 DUP1 CALLDATALOAD SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 POP POP POP PUSH2 0x69E JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP3 ISZERO ISZERO ISZERO ISZERO DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x307 PUSH1 0x4 DUP1 CALLDATASIZE SUB PUSH1 0x20 DUP2 LT ISZERO PUSH2 0x2DB JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST DUP2 ADD SWAP1 DUP1 DUP1 CALLDATALOAD PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 POP POP POP PUSH2 0x751 JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP3 DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x325 PUSH2 0x799 JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE DUP4 DUP2 DUP2 MLOAD DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP DUP1 MLOAD SWAP1 PUSH1 0x20 ADD SWAP1 DUP1 DUP4 DUP4 PUSH1 0x0 JUMPDEST DUP4 DUP2 LT ISZERO PUSH2 0x365 JUMPI DUP1 DUP3 ADD MLOAD DUP2 DUP5 ADD MSTORE PUSH1 0x20 DUP2 ADD SWAP1 POP PUSH2 0x34A JUMP JUMPDEST POP POP POP POP SWAP1 POP SWAP1 DUP2 ADD SWAP1 PUSH1 0x1F AND DUP1 ISZERO PUSH2 0x392 JUMPI DUP1 DUP3 SUB DUP1 MLOAD PUSH1 0x1 DUP4 PUSH1 0x20 SUB PUSH2 0x100 EXP SUB NOT AND DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP JUMPDEST POP SWAP3 POP POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x3EC PUSH1 0x4 DUP1 CALLDATASIZE SUB PUSH1 0x40 DUP2 LT ISZERO PUSH2 0x3B6 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST DUP2 ADD SWAP1 DUP1 DUP1 CALLDATALOAD PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 DUP1 CALLDATALOAD SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 POP POP POP PUSH2 0x83B JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP3 ISZERO ISZERO ISZERO ISZERO DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x452 PUSH1 0x4 DUP1 CALLDATASIZE SUB PUSH1 0x40 DUP2 LT ISZERO PUSH2 0x41C JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST DUP2 ADD SWAP1 DUP1 DUP1 CALLDATALOAD PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 DUP1 CALLDATALOAD SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 POP POP POP PUSH2 0x908 JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP3 ISZERO ISZERO ISZERO ISZERO DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH2 0x4CE PUSH1 0x4 DUP1 CALLDATASIZE SUB PUSH1 0x40 DUP2 LT ISZERO PUSH2 0x482 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST DUP2 ADD SWAP1 DUP1 DUP1 CALLDATALOAD PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 DUP1 CALLDATALOAD PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 POP POP POP PUSH2 0x926 JUMP JUMPDEST PUSH1 0x40 MLOAD DUP1 DUP3 DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 RETURN JUMPDEST PUSH1 0x60 PUSH1 0x3 DUP1 SLOAD PUSH1 0x1 DUP2 PUSH1 0x1 AND ISZERO PUSH2 0x100 MUL SUB AND PUSH1 0x2 SWAP1 DIV DUP1 PUSH1 0x1F ADD PUSH1 0x20 DUP1 SWAP2 DIV MUL PUSH1 0x20 ADD PUSH1 0x40 MLOAD SWAP1 DUP2 ADD PUSH1 0x40 MSTORE DUP1 SWAP3 SWAP2 SWAP1 DUP2 DUP2 MSTORE PUSH1 0x20 ADD DUP3 DUP1 SLOAD PUSH1 0x1 DUP2 PUSH1 0x1 AND ISZERO PUSH2 0x100 MUL SUB AND PUSH1 0x2 SWAP1 DIV DUP1 ISZERO PUSH2 0x57C JUMPI DUP1 PUSH1 0x1F LT PUSH2 0x551 JUMPI PUSH2 0x100 DUP1 DUP4 SLOAD DIV MUL DUP4 MSTORE SWAP2 PUSH1 0x20 ADD SWAP2 PUSH2 0x57C JUMP JUMPDEST DUP3 ADD SWAP2 SWAP1 PUSH1 0x0 MSTORE PUSH1 0x20 PUSH1 0x0 KECCAK256 SWAP1 JUMPDEST DUP2 SLOAD DUP2 MSTORE SWAP1 PUSH1 0x1 ADD SWAP1 PUSH1 0x20 ADD DUP1 DUP4 GT PUSH2 0x55F JUMPI DUP3 SWAP1 SUB PUSH1 0x1F AND DUP3 ADD SWAP2 JUMPDEST POP POP POP POP POP SWAP1 POP SWAP1 JUMP JUMPDEST PUSH1 0x0 PUSH2 0x59A PUSH2 0x593 PUSH2 0x9AD JUMP JUMPDEST DUP5 DUP5 PUSH2 0x9B5 JUMP JUMPDEST PUSH1 0x1 SWAP1 POP SWAP3 SWAP2 POP POP JUMP JUMPDEST PUSH1 0x0 PUSH1 0x2 SLOAD SWAP1 POP SWAP1 JUMP JUMPDEST PUSH1 0x0 PUSH2 0x5BB DUP5 DUP5 DUP5 PUSH2 0xBAC JUMP JUMPDEST PUSH2 0x67C DUP5 PUSH2 0x5C7 PUSH2 0x9AD JUMP JUMPDEST PUSH2 0x677 DUP6 PUSH1 0x40 MLOAD DUP1 PUSH1 0x60 ADD PUSH1 0x40 MSTORE DUP1 PUSH1 0x28 DUP2 MSTORE PUSH1 0x20 ADD PUSH2 0x1026 PUSH1 0x28 SWAP2 CODECOPY PUSH1 0x1 PUSH1 0x0 DUP12 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 PUSH1 0x0 PUSH2 0x62D PUSH2 0x9AD JUMP JUMPDEST PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 SLOAD PUSH2 0xE6D SWAP1 SWAP3 SWAP2 SWAP1 PUSH4 0xFFFFFFFF AND JUMP JUMPDEST PUSH2 0x9B5 JUMP JUMPDEST PUSH1 0x1 SWAP1 POP SWAP4 SWAP3 POP POP POP JUMP JUMPDEST PUSH1 0x0 PUSH1 0x5 PUSH1 0x0 SWAP1 SLOAD SWAP1 PUSH2 0x100 EXP SWAP1 DIV PUSH1 0xFF AND SWAP1 POP SWAP1 JUMP JUMPDEST PUSH1 0x0 PUSH2 0x747 PUSH2 0x6AB PUSH2 0x9AD JUMP JUMPDEST DUP5 PUSH2 0x742 DUP6 PUSH1 0x1 PUSH1 0x0 PUSH2 0x6BC PUSH2 0x9AD JUMP JUMPDEST PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 PUSH1 0x0 DUP10 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 SLOAD PUSH2 0xF2D SWAP1 SWAP2 SWAP1 PUSH4 0xFFFFFFFF AND JUMP JUMPDEST PUSH2 0x9B5 JUMP JUMPDEST PUSH1 0x1 SWAP1 POP SWAP3 SWAP2 POP POP JUMP JUMPDEST PUSH1 0x0 DUP1 PUSH1 0x0 DUP4 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 SLOAD SWAP1 POP SWAP2 SWAP1 POP JUMP JUMPDEST PUSH1 0x60 PUSH1 0x4 DUP1 SLOAD PUSH1 0x1 DUP2 PUSH1 0x1 AND ISZERO PUSH2 0x100 MUL SUB AND PUSH1 0x2 SWAP1 DIV DUP1 PUSH1 0x1F ADD PUSH1 0x20 DUP1 SWAP2 DIV MUL PUSH1 0x20 ADD PUSH1 0x40 MLOAD SWAP1 DUP2 ADD PUSH1 0x40 MSTORE DUP1 SWAP3 SWAP2 SWAP1 DUP2 DUP2 MSTORE PUSH1 0x20 ADD DUP3 DUP1 SLOAD PUSH1 0x1 DUP2 PUSH1 0x1 AND ISZERO PUSH2 0x100 MUL SUB AND PUSH1 0x2 SWAP1 DIV DUP1 ISZERO PUSH2 0x831 JUMPI DUP1 PUSH1 0x1F LT PUSH2 0x806 JUMPI PUSH2 0x100 DUP1 DUP4 SLOAD DIV MUL DUP4 MSTORE SWAP2 PUSH1 0x20 ADD SWAP2 PUSH2 0x831 JUMP JUMPDEST DUP3 ADD SWAP2 SWAP1 PUSH1 0x0 MSTORE PUSH1 0x20 PUSH1 0x0 KECCAK256 SWAP1 JUMPDEST DUP2 SLOAD DUP2 MSTORE SWAP1 PUSH1 0x1 ADD SWAP1 PUSH1 0x20 ADD DUP1 DUP4 GT PUSH2 0x814 JUMPI DUP3 SWAP1 SUB PUSH1 0x1F AND DUP3 ADD SWAP2 JUMPDEST POP POP POP POP POP SWAP1 POP SWAP1 JUMP JUMPDEST PUSH1 0x0 PUSH2 0x8FE PUSH2 0x848 PUSH2 0x9AD JUMP JUMPDEST DUP5 PUSH2 0x8F9 DUP6 PUSH1 0x40 MLOAD DUP1 PUSH1 0x60 ADD PUSH1 0x40 MSTORE DUP1 PUSH1 0x25 DUP2 MSTORE PUSH1 0x20 ADD PUSH2 0x1097 PUSH1 0x25 SWAP2 CODECOPY PUSH1 0x1 PUSH1 0x0 PUSH2 0x872 PUSH2 0x9AD JUMP JUMPDEST PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 PUSH1 0x0 DUP11 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 SLOAD PUSH2 0xE6D SWAP1 SWAP3 SWAP2 SWAP1 PUSH4 0xFFFFFFFF AND JUMP JUMPDEST PUSH2 0x9B5 JUMP JUMPDEST PUSH1 0x1 SWAP1 POP SWAP3 SWAP2 POP POP JUMP JUMPDEST PUSH1 0x0 PUSH2 0x91C PUSH2 0x915 PUSH2 0x9AD JUMP JUMPDEST DUP5 DUP5 PUSH2 0xBAC JUMP JUMPDEST PUSH1 0x1 SWAP1 POP SWAP3 SWAP2 POP POP JUMP JUMPDEST PUSH1 0x0 PUSH1 0x1 PUSH1 0x0 DUP5 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 PUSH1 0x0 DUP4 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 SLOAD SWAP1 POP SWAP3 SWAP2 POP POP JUMP JUMPDEST PUSH1 0x0 CALLER SWAP1 POP SWAP1 JUMP JUMPDEST PUSH1 0x0 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP4 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND EQ ISZERO PUSH2 0xA3B JUMPI PUSH1 0x40 MLOAD PUSH32 0x8C379A000000000000000000000000000000000000000000000000000000000 DUP2 MSTORE PUSH1 0x4 ADD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE PUSH1 0x24 DUP2 MSTORE PUSH1 0x20 ADD DUP1 PUSH2 0x1073 PUSH1 0x24 SWAP2 CODECOPY PUSH1 0x40 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 REVERT JUMPDEST PUSH1 0x0 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP3 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND EQ ISZERO PUSH2 0xAC1 JUMPI PUSH1 0x40 MLOAD PUSH32 0x8C379A000000000000000000000000000000000000000000000000000000000 DUP2 MSTORE PUSH1 0x4 ADD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE PUSH1 0x22 DUP2 MSTORE PUSH1 0x20 ADD DUP1 PUSH2 0xFDE PUSH1 0x22 SWAP2 CODECOPY PUSH1 0x40 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 REVERT JUMPDEST DUP1 PUSH1 0x1 PUSH1 0x0 DUP6 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 PUSH1 0x0 DUP5 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 DUP2 SWAP1 SSTORE POP DUP2 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP4 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH32 0x8C5BE1E5EBEC7D5BD14F71427D1E84F3DD0314C0F7B2291E5B200AC8C7C3B925 DUP4 PUSH1 0x40 MLOAD DUP1 DUP3 DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 LOG3 POP POP POP JUMP JUMPDEST PUSH1 0x0 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP4 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND EQ ISZERO PUSH2 0xC32 JUMPI PUSH1 0x40 MLOAD PUSH32 0x8C379A000000000000000000000000000000000000000000000000000000000 DUP2 MSTORE PUSH1 0x4 ADD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE PUSH1 0x25 DUP2 MSTORE PUSH1 0x20 ADD DUP1 PUSH2 0x104E PUSH1 0x25 SWAP2 CODECOPY PUSH1 0x40 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 REVERT JUMPDEST PUSH1 0x0 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP3 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND EQ ISZERO PUSH2 0xCB8 JUMPI PUSH1 0x40 MLOAD PUSH32 0x8C379A000000000000000000000000000000000000000000000000000000000 DUP2 MSTORE PUSH1 0x4 ADD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE PUSH1 0x23 DUP2 MSTORE PUSH1 0x20 ADD DUP1 PUSH2 0xFBB PUSH1 0x23 SWAP2 CODECOPY PUSH1 0x40 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 REVERT JUMPDEST PUSH2 0xCC3 DUP4 DUP4 DUP4 PUSH2 0xFB5 JUMP JUMPDEST PUSH2 0xD2E DUP2 PUSH1 0x40 MLOAD DUP1 PUSH1 0x60 ADD PUSH1 0x40 MSTORE DUP1 PUSH1 0x26 DUP2 MSTORE PUSH1 0x20 ADD PUSH2 0x1000 PUSH1 0x26 SWAP2 CODECOPY PUSH1 0x0 DUP1 DUP8 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 SLOAD PUSH2 0xE6D SWAP1 SWAP3 SWAP2 SWAP1 PUSH4 0xFFFFFFFF AND JUMP JUMPDEST PUSH1 0x0 DUP1 DUP6 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 DUP2 SWAP1 SSTORE POP PUSH2 0xDC1 DUP2 PUSH1 0x0 DUP1 DUP6 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 SLOAD PUSH2 0xF2D SWAP1 SWAP2 SWAP1 PUSH4 0xFFFFFFFF AND JUMP JUMPDEST PUSH1 0x0 DUP1 DUP5 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP2 MSTORE PUSH1 0x20 ADD SWAP1 DUP2 MSTORE PUSH1 0x20 ADD PUSH1 0x0 KECCAK256 DUP2 SWAP1 SSTORE POP DUP2 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND DUP4 PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH32 0xDDF252AD1BE2C89B69C2B068FC378DAA952BA7F163C4A11628F55A4DF523B3EF DUP4 PUSH1 0x40 MLOAD DUP1 DUP3 DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 LOG3 POP POP POP JUMP JUMPDEST PUSH1 0x0 DUP4 DUP4 GT ISZERO DUP3 SWAP1 PUSH2 0xF1A JUMPI PUSH1 0x40 MLOAD PUSH32 0x8C379A000000000000000000000000000000000000000000000000000000000 DUP2 MSTORE PUSH1 0x4 ADD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE DUP4 DUP2 DUP2 MLOAD DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP DUP1 MLOAD SWAP1 PUSH1 0x20 ADD SWAP1 DUP1 DUP4 DUP4 PUSH1 0x0 JUMPDEST DUP4 DUP2 LT ISZERO PUSH2 0xEDF JUMPI DUP1 DUP3 ADD MLOAD DUP2 DUP5 ADD MSTORE PUSH1 0x20 DUP2 ADD SWAP1 POP PUSH2 0xEC4 JUMP JUMPDEST POP POP POP POP SWAP1 POP SWAP1 DUP2 ADD SWAP1 PUSH1 0x1F AND DUP1 ISZERO PUSH2 0xF0C JUMPI DUP1 DUP3 SUB DUP1 MLOAD PUSH1 0x1 DUP4 PUSH1 0x20 SUB PUSH2 0x100 EXP SUB NOT AND DUP2 MSTORE PUSH1 0x20 ADD SWAP2 POP JUMPDEST POP SWAP3 POP POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 REVERT JUMPDEST POP PUSH1 0x0 DUP4 DUP6 SUB SWAP1 POP DUP1 SWAP2 POP POP SWAP4 SWAP3 POP POP POP JUMP JUMPDEST PUSH1 0x0 DUP1 DUP3 DUP5 ADD SWAP1 POP DUP4 DUP2 LT ISZERO PUSH2 0xFAB JUMPI PUSH1 0x40 MLOAD PUSH32 0x8C379A000000000000000000000000000000000000000000000000000000000 DUP2 MSTORE PUSH1 0x4 ADD DUP1 DUP1 PUSH1 0x20 ADD DUP3 DUP2 SUB DUP3 MSTORE PUSH1 0x1B DUP2 MSTORE PUSH1 0x20 ADD DUP1 PUSH32 0x536166654D6174683A206164646974696F6E206F766572666C6F770000000000 DUP2 MSTORE POP PUSH1 0x20 ADD SWAP2 POP POP PUSH1 0x40 MLOAD DUP1 SWAP2 SUB SWAP1 REVERT JUMPDEST DUP1 SWAP2 POP POP SWAP3 SWAP2 POP POP JUMP JUMPDEST POP POP POP JUMP INVALID GASLIMIT MSTORE NUMBER ORIGIN ADDRESS GASPRICE KECCAK256 PUSH21 0x72616E7366657220746F20746865207A65726F2061 PUSH5 0x6472657373 GASLIMIT MSTORE NUMBER ORIGIN ADDRESS GASPRICE KECCAK256 PUSH2 0x7070 PUSH19 0x6F766520746F20746865207A65726F20616464 PUSH19 0x65737345524332303A207472616E7366657220 PUSH2 0x6D6F PUSH22 0x6E7420657863656564732062616C616E636545524332 ADDRESS GASPRICE KECCAK256 PUSH21 0x72616E7366657220616D6F756E7420657863656564 PUSH20 0x20616C6C6F77616E636545524332303A20747261 PUSH15 0x736665722066726F6D20746865207A PUSH6 0x726F20616464 PUSH19 0x65737345524332303A20617070726F76652066 PUSH19 0x6F6D20746865207A65726F2061646472657373 GASLIMIT MSTORE NUMBER ORIGIN ADDRESS GASPRICE KECCAK256 PUSH5 0x6563726561 PUSH20 0x656420616C6C6F77616E63652062656C6F77207A PUSH6 0x726FA2646970 PUSH7 0x735822122081C8 BLOCKHASH CREATE DUP8 0xCE 0xF9 0x2F 0xEC 0xCB SUB STATICCALL 0xDC PUSH8 0x8B2708C331896EC5 NUMBER 0x2B 0x5D 0x4C PUSH8 0x5F27B6D3E664736F PUSH13 0x63430006020033000000000000 ",
    
    296      "sourceMap": "142:152:5:-:0;;;;8:9:-1;5:2;;;30:1;27;20:12;5:2;142:152:5;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;2219:81:2;;;:::i;:::-;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;23:1:-1;8:100;33:3;30:1;27:10;8:100;;;99:1;94:3;90:11;84:18;80:1;75:3;71:11;64:39;52:2;49:1;45:10;40:15;;8:100;;;12:14;2219:81:2;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;4255:166;;;;;;13:2:-1;8:3;5:11;2:2;;;29:1;26;19:12;2:2;4255:166:2;;;;;;;;;;;;;;;;;;;;;;;;;;;;:::i;:::-;;;;;;;;;;;;;;;;;;;;;;;3262:98;;;:::i;:::-;;;;;;;;;;;;;;;;;;;4881:317;;;;;;13:2:-1;8:3;5:11;2:2;;;29:1;26;19:12;2:2;4881:317:2;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;:::i;:::-;;;;;;;;;;;;;;;;;;;;;;;3121:81;;;:::i;:::-;;;;;;;;;;;;;;;;;;;;;;;5593:215;;;;;;13:2:-1;8:3;5:11;2:2;;;29:1;26;19:12;2:2;5593:215:2;;;;;;;;;;;;;;;;;;;;;;;;;;;;:::i;:::-;;;;;;;;;;;;;;;;;;;;;;;3418:117;;;;;;13:2:-1;8:3;5:11;2:2;;;29:1;26;19:12;2:2;3418:117:2;;;;;;;;;;;;;;;;;;;:::i;:::-;;;;;;;;;;;;;;;;;;;2413:85;;;:::i;:::-;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;23:1:-1;8:100;33:3;30:1;27:10;8:100;;;99:1;94:3;90:11;84:18;80:1;75:3;71:11;64:39;52:2;49:1;45:10;40:15;;8:100;;;12:14;2413:85:2;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;6295:266;;;;;;13:2:-1;8:3;5:11;2:2;;;29:1;26;19:12;2:2;6295:266:2;;;;;;;;;;;;;;;;;;;;;;;;;;;;:::i;:::-;;;;;;;;;;;;;;;;;;;;;;;3738:172;;;;;;13:2:-1;8:3;5:11;2:2;;;29:1;26;19:12;2:2;3738:172:2;;;;;;;;;;;;;;;;;;;;;;;;;;;;:::i;:::-;;;;;;;;;;;;;;;;;;;;;;;3968:149;;;;;;13:2:-1;8:3;5:11;2:2;;;29:1;26;19:12;2:2;3968:149:2;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;:::i;:::-;;;;;;;;;;;;;;;;;;;2219:81;2256:13;2288:5;2281:12;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;2219:81;:::o;4255:166::-;4338:4;4354:39;4363:12;:10;:12::i;:::-;4377:7;4386:6;4354:8;:39::i;:::-;4410:4;4403:11;;4255:166;;;;:::o;3262:98::-;3315:7;3341:12;;3334:19;;3262:98;:::o;4881:317::-;4987:4;5003:36;5013:6;5021:9;5032:6;5003:9;:36::i;:::-;5049:121;5058:6;5066:12;:10;:12::i;:::-;5080:89;5118:6;5080:89;;;;;;;;;;;;;;;;;:11;:19;5092:6;5080:19;;;;;;;;;;;;;;;:33;5100:12;:10;:12::i;:::-;5080:33;;;;;;;;;;;;;;;;:37;;:89;;;;;:::i;:::-;5049:8;:121::i;:::-;5187:4;5180:11;;4881:317;;;;;:::o;3121:81::-;3162:5;3186:9;;;;;;;;;;;3179:16;;3121:81;:::o;5593:215::-;5681:4;5697:83;5706:12;:10;:12::i;:::-;5720:7;5729:50;5768:10;5729:11;:25;5741:12;:10;:12::i;:::-;5729:25;;;;;;;;;;;;;;;:34;5755:7;5729:34;;;;;;;;;;;;;;;;:38;;:50;;;;:::i;:::-;5697:8;:83::i;:::-;5797:4;5790:11;;5593:215;;;;:::o;3418:117::-;3484:7;3510:9;:18;3520:7;3510:18;;;;;;;;;;;;;;;;3503:25;;3418:117;;;:::o;2413:85::-;2452:13;2484:7;2477:14;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;2413:85;:::o;6295:266::-;6388:4;6404:129;6413:12;:10;:12::i;:::-;6427:7;6436:96;6475:15;6436:96;;;;;;;;;;;;;;;;;:11;:25;6448:12;:10;:12::i;:::-;6436:25;;;;;;;;;;;;;;;:34;6462:7;6436:34;;;;;;;;;;;;;;;;:38;;:96;;;;;:::i;:::-;6404:8;:129::i;:::-;6550:4;6543:11;;6295:266;;;;:::o;3738:172::-;3824:4;3840:42;3850:12;:10;:12::i;:::-;3864:9;3875:6;3840:9;:42::i;:::-;3899:4;3892:11;;3738:172;;;;:::o;3968:149::-;4057:7;4083:11;:18;4095:5;4083:18;;;;;;;;;;;;;;;:27;4102:7;4083:27;;;;;;;;;;;;;;;;4076:34;;3968:149;;;;:::o;590:104:0:-;643:15;677:10;670:17;;590:104;:::o;9357:340:2:-;9475:1;9458:19;;:5;:19;;;;9450:68;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;9555:1;9536:21;;:7;:21;;;;9528:68;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;9637:6;9607:11;:18;9619:5;9607:18;;;;;;;;;;;;;;;:27;9626:7;9607:27;;;;;;;;;;;;;;;:36;;;;9674:7;9658:32;;9667:5;9658:32;;;9683:6;9658:32;;;;;;;;;;;;;;;;;;9357:340;;;:::o;7035:530::-;7158:1;7140:20;;:6;:20;;;;7132:70;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;7241:1;7220:23;;:9;:23;;;;7212:71;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;7294:47;7315:6;7323:9;7334:6;7294:20;:47::i;:::-;7372:71;7394:6;7372:71;;;;;;;;;;;;;;;;;:9;:17;7382:6;7372:17;;;;;;;;;;;;;;;;:21;;:71;;;;;:::i;:::-;7352:9;:17;7362:6;7352:17;;;;;;;;;;;;;;;:91;;;;7476:32;7501:6;7476:9;:20;7486:9;7476:20;;;;;;;;;;;;;;;;:24;;:32;;;;:::i;:::-;7453:9;:20;7463:9;7453:20;;;;;;;;;;;;;;;:55;;;;7540:9;7523:35;;7532:6;7523:35;;;7551:6;7523:35;;;;;;;;;;;;;;;;;;7035:530;;;:::o;1746:187:1:-;1832:7;1864:1;1859;:6;;1867:12;1851:29;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;23:1:-1;8:100;33:3;30:1;27:10;8:100;;;99:1;94:3;90:11;84:18;80:1;75:3;71:11;64:39;52:2;49:1;45:10;40:15;;8:100;;;12:14;1851:29:1;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;1890:9;1906:1;1902;:5;1890:17;;1925:1;1918:8;;;1746:187;;;;;:::o;874:176::-;932:7;951:9;967:1;963;:5;951:17;;991:1;986;:6;;978:46;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;1042:1;1035:8;;;874:176;;;;:::o;10695:92:2:-;;;;:::o"
    
    297    }
    
    298  },
    
    299  "bytecode": "60806040523480156200001157600080fd5b506040516200153938038062001539833981810160405260208110156200003757600080fd5b81019080805190602001909291905050506040518060400160405280600581526020017f42617369630000000000000000000000000000000000000000000000000000008152506040518060400160405280600381526020017f42534300000000000000000000000000000000000000000000000000000000008152508160039080519060200190620000cc92919062000389565b508060049080519060200190620000e592919062000389565b506012600560006101000a81548160ff021916908360ff16021790555050506200011633826200011d60201b60201c565b5062000438565b600073ffffffffffffffffffffffffffffffffffffffff168273ffffffffffffffffffffffffffffffffffffffff161415620001c1576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252601f8152602001807f45524332303a206d696e7420746f20746865207a65726f20616464726573730081525060200191505060405180910390fd5b620001d560008383620002fb60201b60201c565b620001f1816002546200030060201b62000f2d1790919060201c565b6002819055506200024f816000808573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020546200030060201b62000f2d1790919060201c565b6000808473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055508173ffffffffffffffffffffffffffffffffffffffff16600073ffffffffffffffffffffffffffffffffffffffff167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef836040518082815260200191505060405180910390a35050565b505050565b6000808284019050838110156200037f576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252601b8152602001807f536166654d6174683a206164646974696f6e206f766572666c6f77000000000081525060200191505060405180910390fd5b8091505092915050565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f10620003cc57805160ff1916838001178555620003fd565b82800160010185558215620003fd579182015b82811115620003fc578251825591602001919060010190620003df565b5b5090506200040c919062000410565b5090565b6200043591905b808211156200043157600081600090555060010162000417565b5090565b90565b6110f180620004486000396000f3fe608060405234801561001057600080fd5b50600436106100a95760003560e01c80633950935111610071578063395093511461025f57806370a08231146102c557806395d89b411461031d578063a457c2d7146103a0578063a9059cbb14610406578063dd62ed3e1461046c576100a9565b806306fdde03146100ae578063095ea7b31461013157806318160ddd1461019757806323b872dd146101b5578063313ce5671461023b575b600080fd5b6100b66104e4565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156100f65780820151818401526020810190506100db565b50505050905090810190601f1680156101235780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b61017d6004803603604081101561014757600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610586565b604051808215151515815260200191505060405180910390f35b61019f6105a4565b6040518082815260200191505060405180910390f35b610221600480360360608110156101cb57600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291905050506105ae565b604051808215151515815260200191505060405180910390f35b610243610687565b604051808260ff1660ff16815260200191505060405180910390f35b6102ab6004803603604081101561027557600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291908035906020019092919050505061069e565b604051808215151515815260200191505060405180910390f35b610307600480360360208110156102db57600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190505050610751565b6040518082815260200191505060405180910390f35b610325610799565b6040518080602001828103825283818151815260200191508051906020019080838360005b8381101561036557808201518184015260208101905061034a565b50505050905090810190601f1680156103925780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b6103ec600480360360408110156103b657600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291908035906020019092919050505061083b565b604051808215151515815260200191505060405180910390f35b6104526004803603604081101561041c57600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610908565b604051808215151515815260200191505060405180910390f35b6104ce6004803603604081101561048257600080fd5b81019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190505050610926565b6040518082815260200191505060405180910390f35b606060038054600181600116156101000203166002900480601f01602080910402602001604051908101604052809291908181526020018280546001816001161561010002031660029004801561057c5780601f106105515761010080835404028352916020019161057c565b820191906000526020600020905b81548152906001019060200180831161055f57829003601f168201915b5050505050905090565b600061059a6105936109ad565b84846109b5565b6001905092915050565b6000600254905090565b60006105bb848484610bac565b61067c846105c76109ad565b6106778560405180606001604052806028815260200161102660289139600160008b73ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020600061062d6109ad565b73ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054610e6d9092919063ffffffff16565b6109b5565b600190509392505050565b6000600560009054906101000a900460ff16905090565b60006107476106ab6109ad565b8461074285600160006106bc6109ad565b73ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008973ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054610f2d90919063ffffffff16565b6109b5565b6001905092915050565b60008060008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020549050919050565b606060048054600181600116156101000203166002900480601f0160208091040260200160405190810160405280929190818152602001828054600181600116156101000203166002900480156108315780601f1061080657610100808354040283529160200191610831565b820191906000526020600020905b81548152906001019060200180831161081457829003601f168201915b5050505050905090565b60006108fe6108486109ad565b846108f98560405180606001604052806025815260200161109760259139600160006108726109ad565b73ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008a73ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054610e6d9092919063ffffffff16565b6109b5565b6001905092915050565b600061091c6109156109ad565b8484610bac565b6001905092915050565b6000600160008473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054905092915050565b600033905090565b600073ffffffffffffffffffffffffffffffffffffffff168373ffffffffffffffffffffffffffffffffffffffff161415610a3b576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260248152602001806110736024913960400191505060405180910390fd5b600073ffffffffffffffffffffffffffffffffffffffff168273ffffffffffffffffffffffffffffffffffffffff161415610ac1576040517f08c379a0000000000000000000000000000000000000000000000000000000008152600401808060200182810382526022815260200180610fde6022913960400191505060405180910390fd5b80600160008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055508173ffffffffffffffffffffffffffffffffffffffff168373ffffffffffffffffffffffffffffffffffffffff167f8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925836040518082815260200191505060405180910390a3505050565b600073ffffffffffffffffffffffffffffffffffffffff168373ffffffffffffffffffffffffffffffffffffffff161415610c32576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252602581526020018061104e6025913960400191505060405180910390fd5b600073ffffffffffffffffffffffffffffffffffffffff168273ffffffffffffffffffffffffffffffffffffffff161415610cb8576040517f08c379a0000000000000000000000000000000000000000000000000000000008152600401808060200182810382526023815260200180610fbb6023913960400191505060405180910390fd5b610cc3838383610fb5565b610d2e81604051806060016040528060268152602001611000602691396000808773ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054610e6d9092919063ffffffff16565b6000808573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002081905550610dc1816000808573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054610f2d90919063ffffffff16565b6000808473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055508173ffffffffffffffffffffffffffffffffffffffff168373ffffffffffffffffffffffffffffffffffffffff167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef836040518082815260200191505060405180910390a3505050565b6000838311158290610f1a576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825283818151815260200191508051906020019080838360005b83811015610edf578082015181840152602081019050610ec4565b50505050905090810190601f168015610f0c5780820380516001836020036101000a031916815260200191505b509250505060405180910390fd5b5060008385039050809150509392505050565b600080828401905083811015610fab576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252601b8152602001807f536166654d6174683a206164646974696f6e206f766572666c6f77000000000081525060200191505060405180910390fd5b8091505092915050565b50505056fe45524332303a207472616e7366657220746f20746865207a65726f206164647265737345524332303a20617070726f766520746f20746865207a65726f206164647265737345524332303a207472616e7366657220616d6f756e7420657863656564732062616c616e636545524332303a207472616e7366657220616d6f756e74206578636565647320616c6c6f77616e636545524332303a207472616e736665722066726f6d20746865207a65726f206164647265737345524332303a20617070726f76652066726f6d20746865207a65726f206164647265737345524332303a2064656372656173656420616c6c6f77616e63652062656c6f77207a65726fa264697066735822122081c840f087cef92feccb03fadc678b2708c331896ec5432b5d4c675f27b6d3e664736f6c63430006020033"
    
    300}
    
    Show all

## Step #4: Test your smart contract [Link to doc(opens in a new
tab)](https://ethereum-waffle.readthedocs.io/en/latest/getting-
started.html#writing-tests)

### Step #4.1 Install necessary dependencies [Link to doc(opens in a new
tab)](https://ethereum-waffle.readthedocs.io/en/latest/getting-
started.html#writing-tests)

After we have successfully authored a Smart Contract we can test it. We will
use `Waffle` to do it.

Tests in `Waffle` are written using `Mocha` alongside with `Chai`. We can use
a different test environment, but `Waffle` matchers only work with `Chai`.

So, we need to add `Chai` to our dependencies :

    
    
     yarn add --dev mocha chai

### Step #4.2 Create test file [Link to doc(opens in a new
tab)](https://ethereum-waffle.readthedocs.io/en/latest/getting-
started.html#writing-tests)

To write our test we need to create `BasicToken.test.ts` file in our test
directory.

    
    
    1import { expect, use } from "chai"
    
    2import { Contract } from "ethers"
    
    3import { deployContract, MockProvider, solidity } from "ethereum-waffle"
    
    4import BasicToken from "../build/BasicToken.json"
    
    5
    
    6use(solidity)
    
    7
    
    8describe("BasicToken", () => {
    
    9  const [wallet, walletTo] = new MockProvider().getWallets()
    
    10  let token: Contract
    
    11
    
    12  beforeEach(async () => {
    
    13    token = await deployContract(wallet, BasicToken, [1000])
    
    14  })
    
    15})
    
    Show all

So, we use `deployContract` method from `Waffle` to deploy our token. As
arguments, we should pass `wallet`, the compiled json file of our contract and
default balance.

`Waffle` also allows us to create a `wallet`, which makes it very easy to
deploy a contract.

You can read more about `wallet` [here(opens in a new tab)](https://ethereum-
waffle.readthedocs.io/en/latest/basic-testing.html?highlight=wallet#getting-
wallets) and you can read more about the deploying function [here(opens in a
new tab)](https://ethereum-waffle.readthedocs.io/en/latest/basic-
testing.html?highlight=wallet#deploying-contracts).

Let's write a simple test to check balance of our wallet. Since we submitted
the value 1000 during the deployment our contract, the balance of our wallet
must be 1000 tokens, which we can check in the first test.

    
    
    1it("Assigns initial balance", async () => {
    
    2  expect(await token.balanceOf(wallet.address)).to.equal(1000)
    
    3})

To run the test use `yarn test`

### Step #4.3 Emitting events [Link to doc(opens in a new
tab)](https://ethereum-
waffle.readthedocs.io/en/latest/matchers.html?highlight=changeBalance#emitting-
events)

In this tutorial, I want to show you the most useful matchers of `Waffle`, so
let's start with the first one.

`Waffle` allows us to test what events where emitted.

In this tutorial, I'll test the `transfer` method of our contract.

In this test, I'll make a transfer from one wallet to another and check
whether the `Transfer` event was called.

    
    
    1it("Transfer emits event", async () => {
    
    2  await expect(token.transfer(walletTo.address, 7))
    
    3    .to.emit(token, "Transfer")
    
    4    .withArgs(wallet.address, walletTo.address, 7)
    
    5})

Also, a big advantage of this matcher is that we can check which arguments
this event was called with by adding `withArgs` to our test.

This will allow us to be sure that our function is being called correctly!

### Step #4.4 Revert with message [Link to doc(opens in a new
tab)](https://ethereum-
waffle.readthedocs.io/en/latest/matchers.html?highlight=changeBalance#revert-
with-message)

`Waffle` allows us to test what message it was reverted with.

We will use `revertedWith` matcher in our test to check it.

We can write a test in which we will perform a transfer for an amount greater
than we have on our wallet. And then we'll check if the transaction reverted
with the exact message!

    
    
    1it("Can not transfer above the amount", async () => {
    
    2  await expect(token.transfer(walletTo.address, 1007)).to.be.revertedWith(
    
    3    "VM Exception while processing transaction: revert ERC20: transfer amount exceeds balance"
    
    4  )
    
    5})

### Step #4.5 Change-token-balance [Link to doc(opens in a new
tab)](https://ethereum-
waffle.readthedocs.io/en/latest/matchers.html?highlight=changeBalance#change-
balance)

`Waffle` allows us to check for changes in the balances of the wallets!

We can use the `changeTokenBalance` matcher to check the balance change or the
`changeTokenBalances` for a multiple account.

The matcher can accept `numbers`, `strings` and `BigNumbers` as a balance
change, while the address should be specified as a wallet or a contract.

Let's write the next test:

    
    
    1it("Send transaction changes receiver balance", async () => {
    
    2  await expect(() =>
    
    3    wallet.sendTransaction({ to: walletTo.address, gasPrice: 0, value: 200 })
    
    4  ).to.changeBalance(walletTo, 200)
    
    5})

The above is a test for a single wallet.

And the next one for multiple wallets:

    
    
    1it("Send transaction changes sender and receiver balances", async () => {
    
    2  await expect(() =>
    
    3    wallet.sendTransaction({ to: walletTo.address, gasPrice: 0, value: 200 })
    
    4  ).to.changeBalances([wallet, walletTo], [-200, 200])
    
    5})

The transaction is expected to be passed as a callback (we need to check the
balance before the call) or as a transaction response.

## Congratulations

**Congratulations! You've made it through my tutorial. You've taken your first
big step towards testing smart contracts with Waffle.**

**Code from this tutorial you can be find[here(opens in a new
tab)](https://github.com/VladStarostenko/tutorial-for-ethereum-org-website).**

**More documentation about`Waffle` available [here(opens in a new
tab)](https://getwaffle.io).**

p

Last edit: [@pettinarip(opens in a new tab)](https://github.com/pettinarip),
December 8, 2023

See contributors

### Was this tutorial helpful?

YesNo

  * [Edit page(opens in a new tab)](https://github.com/ethereum/ethereum-org-website/tree/dev/public/content/developers/tutorials/testing-erc-20-tokens-with-waffle/index.md)
  * On this page

    * A few words about Waffle
    * The quick tutorial
    * Step #1: Install waffle in your project Link to doc
    * Step #2: Write a smart contract Link to doc
    * Step #3: Compile your smart contract Link to doc
    * Step #4: Test your smart contract Link to doc
      * Step #4.1 Install necessary dependencies Link to doc
      * Step #4.2 Create test file Link to doc
      * Step #4.3 Emitting events Link to doc
      * Step #4.4 Revert with message Link to doc
      * Step #4.5 Change-token-balance Link to doc
    * Congratulations

Website last updated: May 22, 2024

[(opens in a new tab)](https://github.com/ethereum/ethereum-org-
website)[(opens in a new tab)](https://twitter.com/ethdotorg)[(opens in a new
tab)](https://discord.gg/ethereum-org)

### Learn

  * [Learn Hub](/en/learn/)
  * [What is Ethereum?](/en/what-is-ethereum/)
  * [What is ether (ETH)?](/en/eth/)
  * [Ethereum wallets](/en/wallets/)
  * [What is Web3?](/en/web3/)
  * [Smart contracts](/en/smart-contracts/)
  * [Gas fees](/en/gas/)
  * [Run a node](/en/run-a-node/)
  * [Ethereum security and scam prevention](/en/security/)
  * [Quiz Hub](/en/quizzes/)
  * [Ethereum glossary](/en/glossary/)

### Use

  * [Guides](/en/guides/)
  * [Choose your wallet](/en/wallets/find-wallet/)
  * [Get ETH](/en/get-eth/)
  * [Dapps - Decentralized applications](/en/dapps/)
  * [Stablecoins](/en/stablecoins/)
  * [NFTs - Non-fungible tokens](/en/nft/)
  * [DeFi - Decentralized finance](/en/defi/)
  * [DAOs - Decentralized autonomous organizations](/en/dao/)
  * [Decentralized identity](/en/decentralized-identity/)
  * [Stake ETH](/en/staking/)
  * [Layer 2](/en/layer-2/)

### Build

  * [Builder's home](/en/developers/)
  * [Tutorials](/en/developers/tutorials/)
  * [Documentation](/en/developers/docs/)
  * [Learn by coding](/en/developers/learning-tools/)
  * [Set up local environment](/en/developers/local-environment/)
  * [Grants](/en/community/grants/)
  * [Foundational topics](/en/developers/docs/intro-to-ethereum/)
  * [UX/UI design fundamentals](/en/developers/docs/design-and-ux/)
  * [Enterprise - Mainnet Ethereum](/en/enterprise/)
  * [Enterprise - Private Ethereum](/en/enterprise/private-ethereum/)

### Participate

  * [Community hub](/en/community/)
  * [Online communities](/en/community/online/)
  * [Ethereum events](/en/community/events/)
  * [Contributing to ethereum.org](/en/contributing/)
  * [Translation Program](/en/contributing/translation-program/)
  * [Ethereum bug bounty program](/en/bug-bounty/)
  * [Ethereum Foundation](/en/foundation/)
  * [Ethereum Foundation Blog(opens in a new tab)](https://blog.ethereum.org/)
  * [Ecosystem Support Program(opens in a new tab)](https://esp.ethereum.foundation)
  * [Devcon(opens in a new tab)](https://devcon.org/)

### Research

  * [Ethereum Whitepaper](/en/whitepaper/)
  * [Ethereum roadmap](/en/roadmap/)
  * [Improved security](/en/roadmap/security/)
  * [Technical history of Ethereum](/en/history/)
  * [Open research](/en/community/research/)
  * [Ethereum Improvement Proposals](/en/eips/)
  * [Ethereum governance](/en/governance/)

  * [About us](/en/about/)
  * [Ethereum brand assets](/en/assets/)
  * [Code of conduct](/en/community/code-of-conduct/)
  * [Jobs](/en/about/#open-jobs)
  * [Privacy policy](/en/privacy-policy/)
  * [Terms of use](/en/terms-of-use/)
  * [Cookie policy](/en/cookie-policy/)
  * [Press Contact(opens in a new tab)](mailto:press@ethereum.org)

Is this page helpful?

