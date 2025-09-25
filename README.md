# 天津财经大学抢课脚本

这是一个用于天津财经大学选课系统的自动化抢课脚本，帮助学生在选课高峰期快速选择心仪的课程。

## 功能特点

- 🔄 **自动检测**：每0.3秒自动扫描页面中的选课按钮
- 🎯 **精准定位**：支持按特定条件高亮显示目标选课按钮
- ⚡ **快速响应**：实时监控按钮状态并及时点击
- 🚦 **安全检测**：自动跳过已禁用的按钮，避免无效操作
- 📍 **视觉辅助**：红色高亮显示目标按钮，方便确认

## 使用方法

### 基础抢课模式
```javascript
let timer = setInterval(() => {
    // 查找所有带有"选课"字样的按钮
    let btns = Array.from(document.querySelectorAll('button, a, input[type="button"], input[type="submit"]'))
        .filter(btn =>
            btn.innerText.includes('选课') ||
            (btn.value && btn.value.includes('选课'))
        );

    if (btns.length >= 4) {
        let btn = btns[3]; // 下标3是第4个
        // 给高亮显示，方便你确认
        btn.style.outline = '4px solid red';
        btn.scrollIntoView({behavior: 'smooth', block: 'center'});
        // 如果未禁用则点击
        if (!btn.disabled && !btn.classList.contains('disabled')) {
            console.log('尝试点击第4个选课按钮:', btn);
            btn.click();
        } else {
            console.log('第4个选课按钮已禁用，等待中...');
        }
    } else {
        console.log('未找到4个及以上"选课"按钮，当前数量:', btns.length);
    }
}, 300); // 每0.3秒尝试一次
```

精准定位模式

```javascript
// 精准高亮你要的"选课"按钮
let targetBtn = Array.from(document.querySelectorAll('button, a, input[type="button"], input[type="submit"]'))
  .find(btn => 
    btn.getAttribute('onclick') === "pushFjjxxkClass('963e9d7eaf364a409cd8035aefbe0a03','401b9c91d3c647dc96134860dd25e86e')"
  );

if (targetBtn) {
  targetBtn.style.outline = '5px solid red';
  targetBtn.style.boxShadow = '0 0 10px 2px #f00';
  targetBtn.scrollIntoView({behavior: 'smooth', block: 'center'});
  console.log('已高亮你要的"选课"按钮:', targetBtn);
} else {
  console.log('未找到目标"选课"按钮');
}
```

注意事项

⚠️ 重要提醒：

· 仅限个人学习使用，请遵守学校相关规定
· 使用前请确认目标课程代码是否正确
· 建议在选课系统非高峰期测试脚本功能
· 过度频繁请求可能触发系统防护机制

自定义配置

修改检测间隔

```javascript
// 将300改为其他数值（单位：毫秒）
}, 500); // 每0.5秒检测一次
```

修改目标按钮索引

```javascript
// 修改btns数组的索引来选择不同位置的按钮
let btn = btns[0]; // 第1个选课按钮
let btn = btns[1]; // 第2个选课按钮
// 以此类推...
```

自定义按钮识别条件

```javascript
// 修改filter条件来识别特定的选课按钮
.filter(btn =>
    btn.innerText.includes('特定课程名称') ||
    btn.id === 'specific-button-id'
)
```

故障排除

常见问题：

1. 脚本不执行：检查浏览器控制台是否有错误信息
2. 找不到按钮：确认页面加载完成，检查按钮选择器条件
3. 点击无效：检查按钮是否被禁用或有其他交互限制

调试命令：

```javascript
// 检查当前页面上的所有按钮
console.log('所有按钮:', document.querySelectorAll('button, a, input[type="button"], input[type="submit"]'));

// 手动停止脚本
clearInterval(timer);
```

免责声明

本脚本仅供技术学习和研究使用，使用者应承担因使用本脚本而产生的一切后果。请合理使用，遵守学校规章制度，不要干扰正常选课秩序。

