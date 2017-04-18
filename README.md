# npl-string

一些常见的字符串处理函数，是对 [NPL](https://github.com/LiXizhi/NPLRuntime) 原生 `string` 的扩展。

*****

> ## 使用方法

在你自己的项目的启动文件中引入该模块即可：

    NPL.load('string');

*****

> ## 文档

> ### replace(oldValue, newValue)

    返回一个新字符串，其中当前实例中出现的所有指定字符串都替换为另一个指定的字符串。
    更好的：http://lua-users.org/wiki/StringReplace
    params:
      oldValue: （string）需要被替换的字符串，可以是一个正则表达式。
      newValue: （string or function）新的字符串或特定格式的字符串，也可以是一个function
    示例：
      local str = 'Hello ParaEngine';
      local str2 = str:replace('e', 'NPL'); => 'HNPLllo ParaEnginNPL'
      local str2 = string.replace(str, 'e', 'NPL'); => 'HNPLllo ParaEnginNPL'
    神奇用法：
      local str = 'Hello ParaEngine';
      local str2 = str:replace('(a)', '%1-'); => 'Hello Pa-ra-Engine'
      如果原字符串中本来就有“（）”呢，比如，需要将“Hello Par(a)Engine”中的“(a)”替换为“a-”。则需为“()”加上转义符：
      local str = 'Hello Par(a)Engine';
      local str2 = str:replace('%(a%)', 'a-'); => 'Hello Para-Engine'
      如果用来替换的字符串中含有“%”呢？因为“%”也是一个特殊字符，因此也需要转义：
      local str = 'Hello Par(a)Engine';
      local str2 = str:replace('%(a%)', '%%1'); => 'Hello Par%1Engine'
      如果用来替换的字符串中含有“()”，则不需要转义：
      local str = 'Hello ParaEngine';
      local str2 = str:replace('r(a)', 'r(%1)'); => 'Hello Par(a)Engine'
    还有更神奇的：
      local str = 'Hello ParaEngine';
      local str2 = str:replace('(P)(a)', '%2%1'); => 'Hello aPraEngine'
    第二个参数是function的示例：
      local str = 'Hello ParaEngine';
      local str2 = str:replace('(%w+)', function(w)
        return w:len();
      end); => '5 10'
      local str3 = str:replace('Hello', function(s)
        return s:upper();
      end); => 'HELLO ParaEngine'

> ### split(separator, outResults)

    拆分字符串
    示例：
      local str = 'aaa,bbb,ccc';
      local ary = str:split(','); => {'aaa', 'bbb', 'ccc'}
      local ary = string.split(str, ','); => {'aaa', 'bbb', 'ccc'}

> ### join(separator, list)

    将字符串数组合并为一个字符串，并以指定的字符间隔。
    示例：
      local list = {'aaa', 'bbb', 'ccc'};
      local str = string.join(',', list); => 'aaa,bbb,ccc'

> ### trim()

    去除字符串开始和结尾处的空格
    示例：
      local str = '  abcdefg   ';
      local str2 = str:trim(); => 'abcdefg';
      local str2 = string.trim(str); => 'abcdefg'

> ### trimStart()

    去除字符串开始处的空格
    示例：
      local str = '  abcdefg   ';
      local str2 = str:trimStart(); => 'abcdefg   ';
      local str2 = string.trimStart(str); => 'abcdefg   '

> ### trimEnd()

    去除字符串结尾处的空格
    示例：
      local str = '  abcdefg   ';
      local str2 = str:trimEnd(); => '  abcdefg';
      local str2 = string.trimEnd(str); => '  abcdefg'

> ### startsWith(str, ignoreCase)

    判断字符串的开头是否与指定字符串匹配
    params:
      str: （string）要比较的字符串
      [ ignoreCase ]: （boolean）是否忽略大小写。可选参数。默认为false。
    示例：
      local str = 'abcdefg';
      local str2 = 'aBc';
      local bl = str:startsWith(str2); => false
      local bl = string.startsWith(str, str2); => false
      local bl = str:startsWith(str2, true); => true
      local bl = string.startsWith(str, str2, true); => true

> ### endsWith(str, ignoreCase)

    判断字符串的结尾是否与指定字符串匹配
    params:
      str: （string）要比较的字符串
      [ ignoreCase ]: （boolean）是否忽略大小写。可选参数。默认为false。
    示例：
      local str = 'abcdefg';
      local str2 = 'eFg';
      local bl = str:endsWith(str2); => false
      local bl = string.endsWith(str, str2); => false
      local bl = str:endsWith(str2, true); => true
      local bl = string.endsWith(str, str2, true); => true

> ### encodeURI()

    把字符串作为 URI 进行编码。某些字符将被十六进制的转义序列进行替换。
    示例：
      local str = 'http://www.nooong.com';
      local str2 = str:encodeURI(); => http%3A%2F%2Fwww.nooong.com
      local str2 = string.encodeURI(str); => http%3A%2F%2Fwww.nooong.com

> ### decodeURI()

    可对 encodeURI() 函数编码过的 URI 进行解码。
    示例：
      local str = 'http://www.nooong.com';
      local str2 = str:encodeURI(); => http%3A%2F%2Fwww.nooong.com
      local str3 = str2:decodeURI(); => http://www.nooong.com
      local str4 = string.decodeURI(str2); => http://www.nooong.com


