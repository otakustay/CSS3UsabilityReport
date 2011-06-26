### 项目目标

对CSS Level3中定义的所有新增属性做一次可用性的评估，得出使用指导方针。

### 项目结构

抽取CSS Level3的新增的158个属性，按所属模块分类。每个模块独立一个文件夹，每个属性独立一个文件。

每个文件由以下几部分组成：

1. 基本信息：属性的基本信息，如属性的名称、所属的模块，以及最终可用性评级的结果。
2. 功能介绍：对属性一个简单的介绍，多数将取自CSS3标准，并进行翻译。
3. 可用性评定：从浏览器兼容性和可降级性等多方面进行评估。
4. 综合评价：对属性的效果和可用性进行综合的评价，并给出合理的使用指导。

### 评价标准

评价从多个方面进行，首先满分为10分，并按以下规则进行相应的计算：

    // 截止2011年6月
    var browsers = ['IE6', 'IE7', 'IE8', 'Firefox 3.6', 'Firefox 4.0', 'Firefox 5.0', 'Chrome'];
    var total = browsers.length * 3;
    var sum = 0;
    for (var i = 0; i < browsers.length; i++) {
        var browser = browsers[i];
        var mark = 3;
        if (!isSupportedBy(browser)) {
            mark = 0;
            // 可以通过其他CSS样式模拟
            if (canSimulateByCSS()) {
                // 模拟后不影响DOM结构
                if (isDOMIdentical()) {
                    mark += 1;
                }
                // 模拟后不影响视觉效果
                if (isVisuallyIdentical()) {
                    mark += 1;
                    // 模拟后不影响交互效果
                    if (isInteractivelyIdentical()) {
                        mark += 1;
                    }
                }
            }
            // 可以通过javascript计算模拟
            else if (canSimulateByJavascript()) {
                // 模拟不影响DOM结构
                if (isDOMIdentical()) {
                    mark += 1;
                }
                // 如果javascript一次执行可适应未来DOM变动
                if (isPermanentlyEffective()) {
                    mark += 1;
                }
            }
        }
        sum += mark;
    }

    // 按满分10分，等比计算，保留1位小数
    var result = ((sum / total) * 10).toFixed(1);
    // 星级按满分10分计算，0.5分为一级，不满0.5按0.5计算
    var star = (result - Math.floor(result)) > 0.5 ? Math.ceil(result) : Math.floor(result) + 0.5;

### 参与方式

所有人均可参与，以开源项目的形式进行，只要你熟悉[Markdown](http://daringfireball.net/projects/markdown/syntax "Daring Fireball: Markdown Syntax Documentation")语法即可。

对任何属性进行评估、修正、补充，均可以直接在对应的文件上进行编辑，并在适当的时候进行Pull Request即可。