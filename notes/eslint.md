#### rule
 * 所有的规则默认都是禁用的。在配置文件中，使用 "extends": "eslint:recommended" 来启用推荐的规则，报告一些常见的问题，在下文中这些推荐的规则都带有一个✔️标记

#### 翻译
 * comma-dangle: 要求或禁止末尾逗号
 * no-cond-assign: 禁止条件表达式中出现赋值操作符
 * no-console: 禁用 console
 * no-constant-condition: 禁止在条件中使用常量表达式
 * no-control-regex: 禁止在正则表达式中使用控制字符
 * no-debugger: 禁用 debugger
 * no-dupe-args: 禁止 function 定义中出现重名参数
 * no-dupe-keys: 禁止对象字面量中出现重复的 key
 * no-duplicate-case: 禁止重复的 case 标签
 * no-empty: 禁止空语句块
 * no-empty-character-class: 禁止在正则表达式中使用空字符集
 * no-ex-assign: 禁止对 catch 子句的参数重新赋值
 * no-extra-boolean-cast: 禁止不必要的布尔转换
 * no-extra-parens: 禁止不必要的括号
 * no-extra-semi: 禁止不必要的分号
 * no-func-assign: 禁止对 function 声明重新赋值
 * no-inner-declarations: 禁止在嵌套的块中出现 function 或 var 声明
 * no-invalid-regexp: 禁止 RegExp 构造函数中无效的正则表达式字符串
 * no-irregular-whitespace: 禁止在字符串和注释之外不规则的空白
 * no-negated-in-lhs: 禁止在 in 表达式中出现否定的左操作数
 * no-obj-calls: 禁止把全局对象 (Math 和 JSON) 作为函数调用
 * no-prototype-builtins: 禁止直接使用 Object.prototypes 的内置属性
 * no-regex-spaces: 禁止正则表达式字面量中出现多个空格
 * no-sparse-arrays: 禁用稀疏数组
 * no-unexpected-multiline: 禁止出现令人困惑的多行表达式
 * no-unreachable: 禁止在return、throw、continue 和 break语句之后出现不可达代码
 * no-unsafe-finally: 禁止在 finally 语句块中出现控制流语句
 * use-isnan: 要求使用 isNaN() 检查 NaN
 * valid-jsdoc: 强制使用有效的 JSDoc 注释
 * valid-typeof: 强制 typeof 表达式与有效的字符串进行比较

 * accessor-pairs: 强制 getter 和 setter 在对象中成对出现
 * array-callback-return: 强制数组方法的回调函数中有 return 语句
 * block-scoped-var: 强制把变量的使用限制在其定义的作用域范围内
 * complexity: 指定程序中允许的最大环路复杂度
 * consistent-return: 要求 return 语句要么总是指定返回的值，要么不指定
 * curly: 强制所有控制语句使用一致的括号风格
 * default-case: 要求 switch 语句中有 default 分支
 * dot-location: 强制在点号之前和之后一致的换行
 * dot-notation: 强制在任何允许的时候使用点号
 * eqeqeq: 要求使用 === 和 !==
 * guard-for-in: 要求 for-in 循环中有一个 if 语句
 * no-alert: 禁用 alert、confirm 和 prompt
 * no-caller: 禁用 arguments.caller 或 arguments.callee
 * no-case-declarations: 不允许在 case 子句中使用词法声明
 * no-div-regex: 禁止除法操作符显式的出现在正则表达式开始的位置
 * no-else-return: 禁止 if 语句中有 return 之后有 else
 * no-empty-function: 禁止出现空函数
 * no-empty-pattern: 禁止使用空解构模式
 * no-eq-null: 禁止在没有类型检查操作符的情况下与 null 进行比较
 * no-eval: 禁用 eval()
 * no-extend-native: 禁止扩展原生类型
 * no-extra-bind: 禁止不必要的 .bind() 调用
 * no-extra-label: 禁用不必要的标签
 * no-fallthrough: 禁止 case 语句落空
 * no-floating-decimal: 禁止数字字面量中使用前导和末尾小数点
 * no-implicit-coercion: 禁止使用短符号进行类型转换
 * no-implicit-globals: 禁止在全局范围内使用 var 和命名的 function 声明
 * no-implied-eval: 禁止使用类似 eval() 的方法
 * no-invalid-this: 禁止 this 关键字出现在类和类对象之外
 * no-iterator: 禁用 iterator 属性
 * no-labels: 禁用标签语句
 * no-lone-blocks: 禁用不必要的嵌套块
 * no-loop-func: 禁止在循环中出现 function 声明和表达式
 * no-magic-numbers: 禁用魔术数字
 * no-multi-spaces: 禁止使用多个空格
 * no-multi-str: 禁止使用多行字符串
 * no-native-reassign: 禁止对原生对象赋值
 * no-new: 禁止在非赋值或条件语句中使用 new 操作符
 * no-new-func: 禁止对 Function 对象使用 new 操作符
 * no-new-wrappers: 禁止对 String，Number 和 Boolean 使用 new 操作符
 * no-octal: 禁用八进制字面量
 * no-octal-escape: 禁止在字符串中使用八进制转义序列
 * no-param-reassign: 不允许对 function 的参数进行重新赋值
 * no-proto: 禁用 proto 属性
 * no-redeclare: 禁止使用 var 多次声明同一变量
 * no-return-assign: 禁止在 return 语句中使用赋值语句
 * no-script-url: 禁止使用 javascript: url
 * no-self-assign: 禁止自我赋值
 * no-self-compare: 禁止自身比较
 * no-sequences: 禁用逗号操作符
 * no-throw-literal: 禁止抛出非异常字面量
 * no-unmodified-loop-condition: 禁用一成不变的循环条件
 * no-unused-expressions: 禁止出现未使用过的表达式
 * no-unused-labels: 禁用未使用过的标签
 * no-useless-call: 禁止不必要的 .call() 和 .apply()
 * no-useless-concat: 禁止不必要的字符串字面量或模板字面量的连接
 * no-useless-escape: 禁用不必要的转义字符
 * no-void: 禁用 void 操作符
 * no-warning-comments: 禁止在注释中使用特定的警告术语
 * no-with: 禁用 with 语句
 * radix: 强制在parseInt()使用基数参数
 * vars-on-top: 要求所有的 var 声明出现在它们所在的作用域顶部
 * wrap-iife: 要求 IIFE 使用括号括起来
 * yoda: 要求或禁止 “Yoda” 条件
 * Strict Mode

#### 该规则与使用严格模式和严格模式指令有关：
 * strict: 要求或禁止使用严格模式指令

#### 这些规则与变量声明有关：
 * init-declarations: 要求或禁止 var 声明中的初始化
 * no-catch-shadow: 不允许 catch 子句的参数与外层作用域中的变量同名
 * no-delete-var: 禁止删除变量
 * no-label-var: 不允许标签与变量同名
 * no-restricted-globals: 禁用特定的全局变量
 * no-shadow: 禁止 var 声明 与外层作用域的变量同名
 * no-shadow-restricted-names: 禁止覆盖受限制的标识符
 * no-undef: 禁用未声明的变量，除非它们在 /global / 注释中被提到
 * no-undef-init: 禁止将变量初始化为 undefined
 * no-undefined: 禁止将 undefined 作为标识符
 * no-unused-vars: 禁止出现未使用过的变量
 * no-use-before-define: 不允许在变量定义之前使用它们

#### Node.js and CommonJS 这些规则是关于Node.js 或 在浏览器中使用CommonJS 的：
 * callback-return: require return statements after callbacks
 * global-require: 要求 require() 出现在顶层模块作用域中
 * handle-callback-err: 要求回调函数中有容错处理
 * no-mixed-requires: 禁止混合常规 var 声明和 require 调用
 * no-new-require: 禁止调用 require 时使用 new 操作符
 * no-path-concat: 禁止对 `__dirname` 和 `__filename` 进行字符串连接
 * no-process-env: 禁用 process.env
 * no-process-exit: 禁用 process.exit()
 * no-restricted-modules: 禁用指定的通过 require 加载的模块
 * no-sync: 禁用同步方法

#### Stylistic Issues 这些规则是关于风格指南的，而且是非常主观的：
 * array-bracket-spacing: 强制数组方括号中使用一致的空格
 * block-spacing: 强制在单行代码块中使用一致的空格
 * brace-style: 强制在代码块中使用一致的大括号风格
 * camelcase: 强制使用骆驼拼写法命名约定
 * comma-spacing: 强制在逗号前后使用一致的空格
 * comma-style: 强制使用一致的逗号风格
 * computed-property-spacing: 强制在计算的属性的方括号中使用一致的空格
 * consistent-this: 当获取当前执行环境的上下文时，强制使用一致的命名
 * eol-last: 强制文件末尾至少保留一行空行
 * func-names: 强制使用命名的 function 表达式
 * func-style: 强制一致地使用函数声明或函数表达式
 * id-blacklist: 禁止使用指定的标识符
 * id-length: 强制标识符的最新和最大长度
 * id-match: 要求标识符匹配一个指定的正则表达式
 * indent: 强制使用一致的缩进
 * jsx-quotes: 强制在 JSX 属性中一致地使用双引号或单引号
 * key-spacing: 强制在对象字面量的属性中键和值之间使用一致的间距
 * keyword-spacing: 强制在关键字前后使用一致的空格
 * linebreak-style: 强制使用一致的换行风格
 * lines-around-comment: 要求在注释周围有空行
 * max-depth: 强制可嵌套的块的最大深度
 * max-len: 强制一行的最大长度
 * max-lines: 强制最大行数
 * max-nested-callbacks: 强制回调函数最大嵌套深度
 * max-params: 强制 function 定义中最多允许的参数数量
 * max-statements: 强制 function 块最多允许的的语句数量
 * max-statements-per-line: 强制每一行中所允许的最大语句数量
 * new-cap: 要求构造函数首字母大写
 * new-parens: 要求调用无参构造函数时有圆括号
 * newline-after-var: 要求或禁止 var 声明语句后有一行空行
 * newline-before-return: 要求 return 语句之前有一空行
 * newline-per-chained-call: 要求方法链中每个调用都有一个换行符
 * no-array-constructor: 禁止使用 Array 构造函数
 * no-bitwise: 禁用按位运算符
 * no-continue: 禁用 continue 语句
 * no-inline-comments: 禁止在代码行后使用内联注释
 * no-lonely-if: 禁止 if 作为唯一的语句出现在 else 语句中
 * no-mixed-operators: 禁止混合使用不同的操作符
 * no-mixed-spaces-and-tabs: 不允许空格和 tab 混合缩进
 * no-multiple-empty-lines: 不允许多个空行
 * no-negated-condition: 不允许否定的表达式
 * no-nested-ternary: 不允许使用嵌套的三元表达式
 * no-new-object: 禁止使用 Object 的构造函数
 * no-plusplus: 禁止使用一元操作符 ++ 和 –
 * no-restricted-syntax: 禁止使用特定的语法
 * no-spaced-func: 禁止 function 标识符和括号之间出现空格
 * no-ternary: 不允许使用三元操作符
 * no-trailing-spaces: 禁用行尾空格
 * no-underscore-dangle: 禁止标识符中有悬空下划线
 * no-unneeded-ternary: 禁止可以在有更简单的可替代的表达式时使用三元操作符
 * no-whitespace-before-property: 禁止属性前有空白
 * object-curly-newline: 强制花括号内换行符的一致性
 * object-curly-spacing: 强制在花括号中使用一致的空格
 * object-property-newline: 强制将对象的属性放在不同的行上
 * one-var: 强制函数中的变量要么一起声明要么分开声明
 * one-var-declaration-per-line: 要求或禁止在 var 声明周围换行
 * operator-assignment: 要求或禁止在可能的情况下要求使用简化的赋值操作符
 * operator-linebreak: 强制操作符使用一致的换行符
 * padded-blocks: 要求或禁止块内填充
 * quote-props: 要求对象字面量属性名称用引号括起来
 * quotes: 强制使用一致的反勾号、双引号或单引号
 * require-jsdoc: 要求使用 JSDoc 注释
 * semi: 要求或禁止使用分号而不是 ASI
 * semi-spacing: 强制分号之前和之后使用一致的空格
 * sort-vars: 要求同一个声明块中的变量按顺序排列
 * space-before-blocks: 强制在块之前使用一致的空格
 * space-before-function-paren: 强制在 function的左括号之前使用一致的空格
 * space-in-parens: 强制在圆括号内使用一致的空格
 * space-infix-ops: 要求操作符周围有空格
 * space-unary-ops: 强制在一元操作符前后使用一致的空格
 * spaced-comment: 强制在注释中 // 或 /* 使用一致的空格
 * unicode-bom: 要求或禁止 Unicode BOM
 * wrap-regex: 要求正则表达式被括号括起来

#### ECMAScript 6 这些规则只与 ES6 有关, 即通常所说的 ES2015：
 * arrow-body-style: 要求箭头函数体使用大括号
 * arrow-parens: 要求箭头函数的参数使用圆括号
 * arrow-spacing: 强制箭头函数的箭头前后使用一致的空格
 * constructor-super: 要求在构造函数中有 super() 的调用
 * generator-star-spacing: 强制 generator 函数中 * 号周围使用一致的空格
 * no-class-assign: 禁止修改类声明的变量
 * no-confusing-arrow: disallow arrow functions where they could be confused with comparisons
 * no-const-assign: 禁止修改 const 声明的变量
 * no-dupe-class-members: 禁止类成员中出现重复的名称
 * no-duplicate-imports: disallow duplicate module imports
 * no-new-symbol: disallow new operators with the Symbol object
 * no-restricted-imports: disallow specified modules when loaded by import
 * no-this-before-super: 禁止在构造函数中，在调用 super() 之前使用 this 或 super
 * no-useless-computed-key: disallow unnecessary computed property keys in object literals
 * no-useless-constructor: 禁用不必要的构造函数
 * no-useless-rename: disallow renaming import, export, and destructured assignments to the same name
 * no-var: 要求使用 let 或 const 而不是 var
 * object-shorthand: 要求或禁止对象字面量中方法和属性使用简写语法
 * prefer-arrow-callback: 要求使用箭头函数作为回调
 * prefer-const: 要求使用 const 声明那些声明后不再被修改的变量
 * prefer-reflect: 要求在合适的地方使用 Reflect 方法
 * prefer-rest-params: require rest parameters instead of arguments
 * prefer-spread: 要求使用扩展运算符而非 .apply()
 * prefer-template: 要求使用模板字面量而非字符串连接
 * require-yield: 要求generator 函数内有 yield
 * rest-spread-spacing: enforce spacing between rest and spread operators and their expressions
 * sort-imports: 强制模块内的 import 排序
 * template-curly-spacing: 要求或禁止模板字符串中的嵌入表达式周围空格的使用
 * yield-star-spacing: 强制在 yield* 表达式中 * 周围使用空格
