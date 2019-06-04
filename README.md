# 前端公共组件开发方案

| 版本 | 修改内容 | 修改时间 | 修改人 | 备注 |
| -- | -------- | --- | --- | ----- |
| 1.0 | 文档制定 | 2019-6-3 | 于水峰 |   |

原则

全事业部统一组件，统一风格，有完善的文档、样例

# 工程说明

整体组件工程分三部分：

1. [occ-web](https://github.com/omni-channel-cloud/occ-web)里面包含了命令行工具oc-cli、生成新模块时所使用的模板，后面说到的标准表单就放在该模板中.

&emsp;&emsp;&emsp;&emsp; 其中oc-cli工具已经提交到npm（安装方式: npm i oc-cli -g），修改后需要发布到npm，并通知大家更新

2. [occ-webapp](https://github.com/omni-channel-cloud/occ-webapp)命令行工具的模板，含工具类、业务组件。

&emsp;&emsp;&emsp;&emsp; oc init 时，会从GitHub下载该工程，生成默认的工程结构。更新后及时通知大家更新

1. [occ-tinper-bee](https://github.com/omni-channel-cloud/occ-tinper-bee) 基础组件

&emsp;&emsp;&emsp;&emsp; 该工程引用了标准[tinper-bee](https://github.com/tinper-bee)中的所有组件，并在此基础上增加了入口用来复写其组件（主要是样式复写）。更新后及时通知大家更新。

# 开发备忘

1. 工程：

各业务线独立工程

公共业务组件更新后需要有专人负责更新并提交到git上。后续会把公共业务组件抽象成为独立npm依赖，减少更新时对整个工程的操作。

2. 文档

每个组件要有独立MarkDown说明文档，并提供独立demo

3. UX

<font size=4 color=red>**所有组件要遵循UI/UE的统一规范**</font>

# 1、参照

参照作为公共业务组件，置于occ-webapp [**occ-common/src/components**](https://github.com/omni-channel-cloud/occ-webapp/tree/master/occ-common/src/components)中，命名 **Refer**

## 1.1 参照形式

### 1.1.1 表型参照

### 1.1.2 树型参照

### 1.1.3 左树右表参照

## 1.2 参照适用场景

### 1.2.1 searchbox中的参照

### 1.2.2 billcard中的参照

### 1.2.5 editGrid中的参照

### 1.2.6 dialog中的参照

## 1.3 其他

### 1.3.1 参照过滤条件

### 1.3.2 参照联动

# 2、 标准组件

标准组件作为公共业务组件，置于occ-webapp [**occ-common/src/components**](https://github.com/omni-channel-cloud/occ-webapp/tree/master/occ-common/src/components)中

## 2.0 基础组件样式适配（occ-tinper-bee）

几乎所有的组件都需要根据UI出具的规范调整。随着所有标准组件、标准表单实现的过程中同步对基础组件的样式进行调整。如有单独使用的组件，则需要在使用前单独适配该组件。

**注意：** 所有的调整需要标示出调整说明、调整人、调整时间，有典型使用场景时要提供说明。调整前如果其他人对该组件已经进行过调整，要求与之前的调整人进行沟通，并对其典型场景进行充分测试。

## 2.1 SearchForm（需适配模板）

 查询条件Form，根据UE要求

1. searchForm默认展示一行，且仅占据一行元素空间；
2. 超出后默认隐藏；
3. 展开时浮动于下方元素上面；
4. 点击搜索后展开内容自动收起；
5. 支持回车查询、清空条件功能

## 2.2 Grid（需适配模板）

 1.分页

 2.renderType：超连接、枚举翻译、按钮

 3.字段排序

 4.字段内容过滤

 5.子表的编辑，数据收集提交

 6.字段更新华隐藏、展示

 7.\*分组表头；列、行合并

## 2.3 FormList （需模板适配）

 包含展示和编辑两种状态。对应原系统的showcard/editcard，

1. 需要支持分组（setion）展示
2. 数据收集、提交
3. 字段关联

## 2.4 Dialog

1. 简单单表查看及维护

2. 拉单界面：单表拉单、主子表拉单，含搜索

## 2.5 ButtonGroup

 1. 列表功能按钮分组

 2. 支持单个按钮的情况

 3. 表单子表，编辑态的按钮

 4. 受 系统管理-按钮权限 控制

## 2.6 Tabs（表单中需适配模板）

 1. 子表多tabs

 2. FormList多tabs

 3. 参照中的多tabs（需要与参照协作）

## 2.7 Echarts

## 2.8 多级级联菜单

 如行政区划，支持四级级联选择

# 3、标准表单

提供两种默认的快速开发模板，放置与occ-web中的template中，在oc init 时可以选择这两个模板，结合单据模板，最大化减少代码编写。

目标：生成表单，根据注册的小应用编码获取单据模板，通过配置请求地址既可以完整简单单据的开发。

## 3.1 单表

## 3.2 主子表

# 4、其他

## 4.1 扩展开发

全局提供了统一的扩展接口：[OccExtendsHOC](https://github.com/omni-channel-cloud/occ-webapp/tree/master/occ-common/src/components/OccExtendsHOC)，所有微应用要被其高阶实现（oc-cli生成的模板已经默认高阶）。

目前提供了模板、扩展、按钮权限三种扩展方式，如有其他扩展也基于此来处理。

三种扩展分别在该组件下建立子目录：template、extends、buttonAuth三个目录。

### 4.1.1 字段扩展

在超出模板可配置范围时的扩展开发

1. 查询调价

2. 列表显示

3. Form表单

4. 子表

### 4.1.2 功能按钮扩展

通过扩展开发的方式新增按钮

### 4.1.3 事件扩展：事件增加、修改、增加前后规则

 1. 增加事件：如扩展的按钮

 2. 修改时间：复写标准事件

 3. 增加前后规则：对原来的事件之前或之后增加逻辑

### 4.1.4 标准业务扩展：扩充逻辑内容

 原有业务页面中增加一小块独立的交互及逻辑，需保证提交数据时可以获取这部分新增内容

## 4.2 按钮权限

 根据&quot;按钮权限&quot;中的配置，控制按钮的可用性（或是否可见）

## 4.3 单据模板

 结合原来的单据模板，对其进行解析。适配原来所有配置逻辑。

### 4.3.1 表单模板

 展示态、编辑态的单据模板。对单据模板进行解析并影响展现及控制

### 4.3.2 列表模板：展示列表、主子表

### 4.3.3 查询模板（暂无）

## 4.4 审批流

 适配iuap工作台的审批流交互

## 4.5 附件上传

 与dialog结合，适配原上传场景

## 4.6 导入/导出

 适配iuap工作台的导入导出