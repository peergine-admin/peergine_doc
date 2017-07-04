## 8\. PG_CLASS_Board类: {#8-pg-class-board}

### 1) 描述： {#1}

白板共享类。

### 2) 选项： {#2}

无

### 3) 方法： {#3}

#### PG_METH_BOARD_Open {#pg-meth-board-open}

ID：32

说明：打开一个白板共享对象。

交互方式：

方式7

发送请求参数：样例：(Wnd){3664687}

Wnd：白板窗口的句柄

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_BOARD_Close {#pg-meth-board-close}

ID：33

说明：关闭一个白板共享对象。

交互方式：

方式7

发送请求参数：空

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_BOARD_Shape {#pg-meth-board-shape}

ID：34

说明：设置绘图的参数。

交互方式：

方式7

发送请求参数：样例：(Shape){1}(Color){223344}(Width){3}(Type){0}

Shape：图形的类型。参考“

常量：图形的类型

”章节

Color：线条的颜色，RGB格式。

Width：线条的宽度（像素）

Type：线条的风格（未实现）

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_BOARD_Cursor {#pg-meth-board-cursor}

ID：35

说明：设置不同图形的鼠标光标。

交互方式：

方式7

发送请求参数：样例：(Shape){1}(Path){c:\temp\pen.cur}

Shape：图形的类型。参考“

常量：图形的类型

”章节

Path：光标文件的路径，文件名的后缀必须为“.cur”。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：无此操作

#### PG_METH_BOARD_Save {#pg-meth-board-save}

ID：36

说明：保存白板上所写画的内容到图片里。

交互方式：

方式5

发送请求参数：样例：(Path){c:\temp\xxxx.png}

Path：保存白板的图片文件路径，后缀必须为“png”。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：样例：(Path){c:\temp\xxxx.png}

Path：保存白板的图片文件路径，后缀必须为“png”。

#### PG_METH_BOARD_Load {#pg-meth-board-load}

ID：37

说明：从文件打开一个图片显示在白板上。

交互方式：

方式5

发送请求参数：样例：(Path){c:\temp\xxxx.png}

Path：打开的图片文件路径，后缀必须为“png”。

接收请求参数：无此操作

发送应答参数：无此操作

接收应答参数：样例：(Path){c:\temp\xxxx.png}

Path：打开的图片文件路径，后缀必须为“png”。

### 4) 常量：图形的类型 {#4}

#### PG_BOARD_SHAPE_Null {#pg-board-shape-null}

ID：0

说明：取消绘图状态

#### PG_BOARD_SHAPE_Pen {#pg-board-shape-pen}

ID：1

说明：绘制任意线条

#### PG_BOARD_SHAPE_Line {#pg-board-shape-line}

ID：2

说明：绘制直线

#### PG_BOARD_SHAPE_Rectangle {#pg-board-shape-rectangle}

ID：3

说明：绘制矩形

#### PG_BOARD_SHAPE_Ellipse {#pg-board-shape-ellipse}

ID：4

说明：绘制椭圆

#### PG_BOARD_SHAPE_Pointer {#pg-board-shape-pointer}

ID：5

说明：绘制指针。当一个节点上的鼠标移动时，在其他节点上绘制同步移动的指针。