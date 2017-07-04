## 3\. 控件的OML解析器函数: {#3-oml}

### 1) String omlEncode(sEle) {#1-string-omlencode-sele}

**描述：**

对指定字符串进行OML编码。如果该字符串中包含OML的标记字符，则这些标记字符将转换成转义后的标记，请参考“[对象标记语言(OML)](..\dui_xiang_biao_ji_yu_8a0028_oml\README.md)”章节。

**参数：**

sEle：[字符串] 需要编码的字符串

**返回值：**

[字符串] 编码后的字符串。

**示例(JavaScript)：**

var sEncEle = pgAtx.omlEncode(“abc(efg[hij{klm”);

### 2) String omlDecode(sEle) {#2-string-omldecode-sele}

**描述：**

对指定字符串进行OML解码。

**参数：**

sEle：[字符串] 需要解码的字符串

**返回值：**

[字符串] 解码后的字符串。

**示例(JavaScript)：**

var sDecEle = pgAtx.omlDecode(“abc&amp;Aefg&amp;Chij&amp;Eklm”);

### 3) String omlSetName(sEle, sPath, sName) {#3-string-omlsetname-sele-spath-sname}

**描述：**

设置一个OML元素的名称。

**参数：**

sEle：OML字符串

sPath：需要设置名称的OML元素在整个OML字符串中的路径

sName：设置的新名字。不需要对此参数进行OML编码。

**返回值：**

[字符串] 设置元素名称后的整个OML字符串。

**示例(JavaScript)：**

var sEle = “(Name0)[Class0]{aaaaa}(Name1)[Class0]{bbbb}”;

var sNewEle = pgAtx.omlSetName(sEle, “Name0”, “NameX”);

### 4) String omlSetClass(sEle, sPath, sClass) {#4-string-omlsetclass-sele-spath-sclass}

**描述：**

设置一个OML元素的类型

**参数：**

sEle：OML字符串

sPath：需要设置名称的OML元素在整个OML字符串中的路径

sClass：设置的新类型。不需要对此参数进行OML编码。

**返回值：**

[字符串] 设置元素类型后的整个OML字符串。

**示例(JavaScript)：**

var sEle = “(Name0)[Class0]{aaaaa}(Name1)[Class0]{bbbb}”;

var sNewEle = pgAtx.omlSetClass(sEle, “Name0”, “ClassX”);

### 5) String omlSetContent(sEle, sPath, sContent) {#5-string-omlsetcontent-sele-spath-scontent}

**描述：**

设置一个OML元素的内容

**参数：**

sEle：OML字符串

sPath：需要设置名称的OML元素在整个OML字符串中的路径

sContent：设置的新内容。不需要对此参数进行OML编码。

**返回值：**

[字符串] 设置元素内容后的整个OML字符串。

**示例(JavaScript)：**

var sEle = “(Name0)[Class0]{aaaaa}(Name1)[Class0]{bbbb}”;

var sNewEle = pgAtx.omlSetContent(sEle, “Name0”, “XXXXX”);

### 6) String omlNewEle(sName, sClass, sContent) {#6-string-omlnewele-sname-sclass-scontent}

**描述：**

生成一个OML元素字符串

**参数：**

sName：元素的名称。不需要对此参数进行OML编码。

sClass：元素的类型。不需要对此参数进行OML编码。

sContent：元素的内容。不需要对此参数进行OML编码。

**返回值：**

[字符串] 生成的OML元素字符串。

**示例(JavaScript)：**

var sNewEle = pgAtx.omlNewEle(“Name0”, “Class0”, “aaaaaaaaaa”);

### 7) String omlGetEle(sEle, sPath, uSize, uPos) {#7-string-omlgetele-sele-spath-usize-upos}

**描述：**

从一个OML字符串中获取指定的OML元素

**参数：**

sEle：OML字符串

sPath：要获取的元素在整个OML字符串的路径

uSize：获取OML元素的个数

uPos：获取OML元素的起始位置

**返回值：**

[字符串] 获取到的OML元素。

**示例(JavaScript)：**

var sEle = “(PeerList){(Peer0){}(Peer1){}(Peer2){}(Peer4){}}”;

var sSubEle = pgAtx.omlGetEle(sEle, “PeerList.”, 2, 0);

### 8) String omlDeleteEle(sEle, sPath, uSize, uPos) {#8-string-omldeleteele-sele-spath-usize-upos}

**描述：**

从一个OML字符串中删除指定的OML元素

**参数：**

sEle：OML字符串

sPath：要删除的元素在整个OML字符串的路径

uSize：删除OML元素的个数

uPos：删除OML元素的起始位置

**返回值：**

[字符串] 删除指定元素后的OML字符串。

**示例(JavaScript)：**

var sEle = “(PeerList){(Peer0){}(Peer1){}(Peer2){}(Peer4){}}”;

var sSubEle = pgAtx.omlDeleteEle(sEle, “PeerList.”, 3, 1);

### 9) String omlGetName(sEle, sPath) {#9-string-omlgetname-sele-spath}

**描述：**

获取指定OML元素的名称

**参数：**

sEle：OML字符串

sPath：要获取名称的元素在整个OML字符串的路径

**返回值：**

[字符串] 获取到的元素名称。

**示例(JavaScript)：**

var sEle = “(Name0)[Class0]{aaaaa}(Name1)[Class0]{bbbb}”;

var sName = pgAtx.omlGetName(sEle, “”);

### 10) String omlGetClass(sEle, sPath) {#10-string-omlgetclass-sele-spath}

**描述：**

获取指定OML元素的类型

**参数：**

sEle：OML字符串

sPath：要获取类型的元素在整个OML字符串的路径

**返回值：**

[字符串] 获取到的元素类型。

**示例(JavaScript)：**

var sEle = “(Name0)[Class0]{aaaaa}(Name1)[Class0]{bbbb}”;

var sClass = pgAtx.omlGetClass(sEle, “Name1”);

### 11) String omlGetContent(sEle, sPath) {#11-string-omlgetcontent-sele-spath}

**描述：**

获取指定OML元素的内容

**参数：**

sEle：OML字符串

sPath：要获取内容的元素在整个OML字符串的路径

**返回值：**

[字符串] 获取到的元素内容。

**示例(JavaScript)：**

var sEle = “(Name0)[Class0]{aaaaa}(Name1)[Class0]{bbbb}”;

var sContent = pgAtx.omlGetContent(sEle, “Name1”);