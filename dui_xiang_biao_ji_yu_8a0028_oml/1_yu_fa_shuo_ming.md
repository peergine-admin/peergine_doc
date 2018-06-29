## 1\. 语法说明 {#1}

OML（对象标记语言，Object Markup Language）是Peergine中数据传递、数据存储和数据配置的通用数据表达格式。Peergine提供了OML解析器功能辅助生成和解析OML文本，请参考“[控件的OML解析器函数](..\pgatxkong_jian_de_bian_cheng_can_kao_ff1a\3_kong_jian_de_oml_jie_xi_qi_han_65703a.md)”章节。

OML的标记字符为：’(’、’)’、’[’、’]’、’{’、’}’、’&amp;’共7个ASCII字符。

OML描述的数据元素称为对象。由’(’和’)’之间的字符串称为对象的名称，由’[’和’]’之间的字符串称为对象的类型，由’{’和’}’之间的字符串为对象的内容或子对象。一个对象由名称、类型和内容(或子对象)构成。

OML的转义字符为’&amp;’。

‘(‘ 转义为 &amp;A，‘)‘ 转义为 &amp;B，‘[‘ 转义为 &amp;C，‘]‘ 转义为 &amp;D，‘{‘ 转义为 &amp;E，‘}‘ 转义为 &amp;F，‘&amp;‘ 转义为 &amp;G。