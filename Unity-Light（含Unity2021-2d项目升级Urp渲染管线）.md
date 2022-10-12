# Unity-Light（含Unity2021-2d项目升级Urp渲染管线）



## 普通渲染管线（比较老旧的光效升级方式，已舍弃）

要使场景和角色拥有光效，那就得让他们先暗下来，给他们添加相应的材质

### *场景材质的添加*

> 选中需要添加材质的场景，在右侧框内的“材质”菜单中，选中Default-Diffuse材质

### 人物材质的添加

> 在任意文件夹创建一个材质，在shader菜单中选中Sprites下拉菜单中的Diffuse



### 场景光效的添加

> 可以直接在右侧菜单创建各种光源，
>
> 光源既可以是固定的，
>
> 又可以作为其他 GameObject 的子对象，跟随父对象移动。



## 通用渲染管线（Universal RP）

### 前言

​	为了得到更好的光线效果，我们需要将Untiy的渲染管线升级到 Urp. Untiy2020 以前的的版本，网上的教程已经十分详尽，再次不过多赘述，有需要直接进行百度即可。这里重点讲的是 Unity2020 以上版本的升级步骤（在中文互联网上没有找到相关教程，于是在此记录我在其他渠道的学习经历）

### 组件的添加

​	在 **PackageManager** 中搜索 **Universal RP**，点击 **install** 进行下载



### 渲染管线的修改

​	选择在自己喜欢的**文件夹下**，**右键 -> Create -> Rendering -> URP Asset (with 2D Renderer)**，然后给其命名为自己喜欢的名字，操作正确的话，会生成以下两个文件

![image-20220930160755284](C:/Users/liaoz/AppData/Roaming/Typora/typora-user-images/image-20220930160755284.png)

​	上述步骤完成后，在Unity窗口的右上角选择 **Edit -> Project Settings -> Graphics**，随后将第一个选项修改为我们刚刚创建的文件。

​	接着继续在 **Project Settings** 窗口中，选择 Quality ，并将 **Rendering -> Render Pipline Asset** 修改为我们刚刚创建的文件即可。



### 材质的升级

​	上述步骤操作完成，渲染管线的修改就基本完成的，现在我们需要将当前的材质都升级到URP。

​	同样是在Unity窗口右上角，选择 **Window -> Rendering -> Render Pipline Converter** 打开 **Render Pipline Converter** 窗口，中间的选择框需要选择 **Convert Built-in to 2D(URP)** ， 紧接着将下面的所有选项勾选，然后点击 **左下角 Initialize Converters** 将场景中的材质都加载进来，最后点击 **右下角 Convert Asset** 将所有材质都升级到 URP。

​	完成上述步骤之后，就可以将所有材质都升级到 URP 了，随后你就可以看到场景里面的物品都会变为黑色（不出意外的话.....），这时候不需要慌张，你只需要在场景中添加 **光照（2D Light）**，就可以看到有色彩的场景了

**（意外情况：**

​	不出意外的话，一般都会出意外的，一般分为下列两种情况（我遇到的情况只有两种）：

>1. **场景中的物品没有变暗**
>
>   ​	这种情况其实是相对简单的，只需要更改场景中物品的材质，将其改为 **Sprite-Lit-Default** 即可
>
>2. **场景中的物品呈现紫色**
>
>   ​	当这种情况出现时，一般表示物品的材质丢失。在升级到URP后，之前的材质可能会因为不适配导致材质丢失，从而使物品呈现材质丢失的状态。此时的修改方法是，创建URP自己的 Shader Graphs **（右键 -> Create -> Shader Graphs -> URP -> Lit Shader Graphs）**，并将之前的 **Shader Graphs** 中的内容复制到刚刚创建的 **Lit Shader Graphs** 中，随后将对应的参数连接好（详细操作可以看 [这个视频](https://www.youtube.com/watch?v=BCR2xQ7jWMU) )



### 添加光照

​	如果你读到这，那么恭喜你，你成功将你当前的项目升级到URP了！！

​	现在你可以看到，当你添加对应的 **光照(2d)** 到自己的项目中，周围的场景都会被照亮。

​	可是现在的光照看起来还是不太理想，我们可以使用另一个美化灯光的插件，来使我们的场景效果变得更加的真实，这个强大的插件叫做 **Post Processing**



## 后处理（Post Processing）

​	同样的操作，到 Package Manger 中找到我们强大的 Post Processing 插件并下载，下载方法不多赘述。

​	下载完成后，在 **Hierarchy** 窗口里面右键创建 **Volume -> Global Volume**，选择创建好的 **Global Volume** ，在**Inspector** 窗口里点击 **Add Override** 添加 **Bloom** 组件，勾选自己想要的效果并调整参数即可得到自己想要的效果。（这里我只勾选了 Bloom 前面的两个选项，其他选项与其他组件的功能就需要你自己查阅资料了）

​	最后选择 Main Camera，在 Inspector 窗口中勾选 PostProcessing 就可以在 Scene 窗口中看到 **更好的光线渲染效果**





