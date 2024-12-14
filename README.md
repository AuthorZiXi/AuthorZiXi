## 作者紫汐（旧名"茶红 落叶"）

业余爱好编程，平常喜欢玩一些VN。

现居浙江金华，学生。

近期消息：

ScnScript已被临时搁置，重制之后事情太多了。

TinySystem的Config模块原型的test做好了，支持创建编辑结构体和查看设置（不是指有了具体设置界面，这里是指winform的效果，大概几百行）

还写了个`CreateDerivedObjectForm`，C#的`Extensions`方法挺好用的

下面是一个扩展方法的示例，遍历对象树很好用

```cs
public static void Foreach<T>(this ConfigurableItem item, Func<ConfigurableItem, T> createNodeFunc, Action<T, T> addChildAction, T parentNode)
{
    T currentNode = createNodeFunc(item);
    addChildAction(currentNode, parentNode);

    if (item is ConfigGroup group)
    {
        foreach (var child in group.Items)
        {
            Foreach(child, createNodeFunc, addChildAction, currentNode);
        }
    }
}
```

下面是我在`TinySystem.Tests.TsConfig`里面`ViewConfigs`窗体的使用方法

```cs
treeView1.Nodes.Clear();
TreeNode rootTreeNode = new TreeNode("临时");
Group.Foreach(
    item =>
    {
         var node = new TreeNode(item.DisplayName);
         node.Tag = item;
         node.ToolTipText = item.GetDetail(true);
         return node;
    }, // 创建TreeNode的函数
    (childNode, parentNode) => parentNode.Nodes.Add(childNode), // 添加子节点的操作
    rootTreeNode // 根节点
);

foreach (var node in rootTreeNode.Nodes)
{
      if (node is TreeNode treeNode)
      {
         treeView1.Nodes.Add(treeNode);

      }
}

treeView1.ExpandAll();
```

[落叶文档](teared-leaffall.github.io) 目前老早被国内屏蔽了，只不过有时还是能上，应该近期不会更新

近期要最后一次月考了，前面请了几天假，学习跟不上了😱😵

-- 2024.12.14
 
## ☕额外信息
> 
> ⏱️ 我想下一个项目到来还需要很长一段时间。
>
> 💬 您也可以在其他社交平台与我通信或提交反馈哦!😉
>
> 📫 联系我: ✉ 1423360499@qq.com
>
> 🎇 每天都要开心哦！ 🎉
> 
> 🌈 让我们展望未来！  (≧∇≦)/ 😚
