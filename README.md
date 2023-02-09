## 代码预处理
### 生成抽象语法树
本仓库基于[treesitter](https://github.com/tree-sitter/tree-sitter),能够将python,java,javascript,cpp,c#,typescript,php,go(按照codegeex代码翻译对应的八种语言)源文件解析生成python嵌套列表格式的ast。

例如：
```
def factorial(n):
    factorial = 1
    for i in range(1, n + 1):
        factorial *= i
    return factorial
```
解析后生成ast列表：
```
[['module ', ['function_definition name: ', ['identifier'], ' parameters: ', ['parameters ', ['identifier']], ' body: ', ['block ', ['expression_statement ', ['assignment left: ', ['identifier'], ' right: ', ['integer']]], ' ', ['for_statement left: ', ['identifier'], ' right: ', ['call function: ', ['identifier'], ' arguments: ', ['argument_list ', ['integer'], ' ', ['binary_operator left: ', ['identifier'], ' right: ', ['integer']]]], ' body: ', ['block ', ['expression_statement ', ['augmented_assignment left: ', ['identifier'], ' right: ', ['identifier']]]]], ' ', ['return_statement ', ['identifier']]]]]]
```
#### 使用方式
[setting.ipynb](/setting.ipynb)文件内code2ast函数，参数为language和filepath。<br>language标签如下："Python","Cpp","java","javascript","C-sharp","Go","PHP"。

### 解析语法文件
[grammar.ipynb](/grammar.ipynb)文件内存有将各个语言grammar.json文件解析后得到的字典。<br>
如cpp语法文件解析后字典：
```
{'translation_unit': '_top_level_item',
 '_top_level_item': [['function_definition',
   'linkage_specification',
   'declaration',
   '_statement',
   'attributed_statement',
   'type_definition',
   '_empty_declaration',
   'preproc_if',
   'preproc_ifdef',
   'preproc_include',
   'preproc_def',
   'preproc_function_def',
   'preproc_call'],
  'namespace_definition',
  'concept_definition',
  'namespace_alias_definition',
  'using_declaration',
  'alias_declaration',
  'static_assert_declaration',
  'template_declaration',
  'template_instantiation',
  'constructor_or_destructor_definition',
  'operator_cast_definition',
  'operator_cast_declaration'],
 'preproc_include': [None,
  {
      ....
```

