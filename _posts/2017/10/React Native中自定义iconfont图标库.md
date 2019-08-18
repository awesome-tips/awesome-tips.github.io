---
title: React Native中自定义iconfont图标库
date: 2017-10-01 00:00:00
author: 知识小集成员
cover: true
---

React Native中自定义iconfont图标库
----------

接上一条。

使用`Unicode`码显得不直观，所以我们可以自定义图标库。`react-native-vector-icons`有一些内置的图标库，我们参考其创建方式，我们以Zocial为例，如下代码所示：

```javascript
import createIconSet from './lib/create-icon-set';
import glyphMap from './glyphmaps/Zocial.json';

const iconSet = createIconSet(glyphMap, 'zocial', 'Zocial.ttf');

export default iconSet;

export const Button = iconSet.Button;
export const TabBarItem = iconSet.TabBarItem;
export const TabBarItemIOS = iconSet.TabBarItemIOS;
export const ToolbarAndroid = iconSet.ToolbarAndroid;
export const getImageSource = iconSet.getImageSource;
```

最主要的就是createIconSet函数，它接受三个参数：字形映射表、字体名、字体文件名。

首先我们需要制作一个字形映射表，这是一个json文件，其内容如下代码所示：

```javascript
{
  "home": 58981,
  "setting": 58928,
  "stack-overflow": 59479
}
```

key是我们可以在代码中直接使用的字符串，value是Unicode码对应的10进制数字，其中Unicode码可以在iconfont.cn上查看(实际就是就`&#xe665;`串中有`e665`)。

然后我们创建一个js文件，参考Zocial.js，依葫芦画瓢，如下代码所示：

```javascript
import createIconSet from 'react-native-vector-icons/lib/create-icon-set';

import glyphMap from './iconfont.json';

const iconSet = createIconSet(glyphMap, 'iconfont', 'iconfont.ttf');

export default iconSet;

export const Button = iconSet.Button;
export const TabBarItem = iconSet.TabBarItem;
export const TabBarItemIOS = iconSet.TabBarItemIOS;
export const ToolbarAndroid = iconSet.ToolbarAndroid;
export const getImageSource = iconSet.getImageSource;
```

在工程中，我们就可以直接使用这个自定义图标库了，如下代码所示：

```javascript
import Icon from './assets/fonts/iconfont';

const setTabBarIcon = () => ({tintColor}) => {
  return <Icon name='home' size={30} color={tintColor}/>
};
```

比使用Unicode直观多了。

参考

1. [Github react-native-vector-icons](https://github.com/oblador/react-native-vector-icons)
2. [React Native与Iconfont](https://github.com/MrErHu/blog/issues/15)