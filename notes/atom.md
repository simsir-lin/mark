#### 快捷键
 * ctrl + shift + p  ——  工具命令搜索
 * ctrl + p  ——  项目文件搜索
 * ctrl + shift + m  ——  mark预览
 * ctrl + w  ——  关闭当前tab
 * ctrl + alt + [  ——  闭合代码
 * ctrl + alt + ]  ——  展开代码
 * alt + \  ——  切换tree和编写区的焦点

#### 插件
 * emmet —— 支持[zen coding](http://www.w3cplus.com/tools/emmet-cheat-sheet.html) -- 快键键 ctrl + option + enter
 * [atom-beautify](https://atom.io/packages/atom-beautify) —— 格式化代码，快键键 ctrl + alt + b
 * minimap —— 右侧代码预览
 * minimap-git-diff —— 右侧代码预览中显示修改的内容
 * minimap-autohider —— 右侧代码预览中显示修改的内容
 * best-js-snippets —— js基本语法
 * atom-bootstrap3 —— bootstrap3 语法块
 * highlight-selected —— 高亮所有和当前选中单词一样的单词
 * minimap-highlight-selected —— 高亮所有和当前选中单词一样的单词在minmap中显示
 * autocomplete-paths —— 自动补全路径
 * autocomplete-en-cn —— 自动翻译
 * vuejs2-snippets —— vue提示语块
 * language-vue —— vue语法高亮显示
 * JSHint  —— js代码检查
 * language-javascript-jsx —— 高亮jsx文件语法
 * atom-ternjs —— js静态编译
 * javascript-snippets -- js提示块

#### 主题
 * [atom-material-ui](https://atom.io/themes/atom-material-ui)
 * [atom-material-syntax](https://atom.io/themes/atom-material-syntax)

#### 紧凑tree view
.tree-view {
  // background-color: whitesmoke;
  li:not(.list-nested-item), li.list-nested-item > .list-item {
    line-height: 1.85rem; // Edit me for height
  }
  .list-group .selected::before, .list-tree .selected::before {
    height: 1.85rem; // Edit me for height
  }
  .name.icon::before {
    margin: 0 0.5rem 0 0;    
  }
  .list-tree.has-collapsable-children .list-nested-item > .list-tree > li,
  .list-tree.has-collapsable-children .list-nested-item > .list-group > li {
    padding-left: 1rem;
  }
  .list-tree.has-collapsable-children li.list-item {
    margin-left: 1.1rem;
  }
  .list-tree.has-collapsable-children .list-nested-item > .list-item::before {
    margin-right: 0.3rem;
  }
}
