# Bokeh Rendering by Blender

A guide to render bokeh images by Blender 2.93

[1. Blender 入门](#Sec.1)
 
&emsp;&emsp; [1.1. 基础设置](#Sec.1.1)

&emsp;&emsp; [1.2. 基础操作及快捷键](#Sec.1.2)

&emsp;&emsp; [1.3. 高阶操作](#Sec.1.3)

&emsp;&emsp; [1.4. 界面常用按钮介绍](#Sec.1.4)

[2. Python 脚本](#Sec.2)

&emsp;&emsp; [2.1. 安装 cv2 包](#Sec.2.1)

&emsp;&emsp; [2.2. 脚本使用](#Sec.2.2)

&emsp;&emsp; [2.3. 脚本图文说明](#Sec.2.3)

---


<span id="Sec.1"></span>
# 1. Blender 入门

<span id="Sec.1.1"></span>
## 1.1. 基础设置

参见 [https://www.bilibili.com/video/BV1pV41127Dq?spm_id_from=333.999.0.0](https://www.bilibili.com/video/BV1pV41127Dq?spm_id_from=333.999.0.0)

(翻译软件和插件可以暂时不管)

<span id="Sec.1.2"></span>
## 1.2. 基础操作及快捷键

以下为常用的查看及渲染模型的操作，不包括自己建模的操作

| 操作 | 作用 |
| :-: | :-: |
| 空格 | 播放动画 |
| 鼠标中建 或 Alt+鼠标左键 | 旋转视角 |
| Shift+鼠标中键 或 Alt+Shift+鼠标左键 | 平移视角 |
| 滚轮 | 推拉视角 |
| 小键盘0 | 调整为摄像机拍摄视角 |
| T | 显示/隐藏左侧工具栏 |
| N | 显示/隐藏右侧工具栏 |
| F12 | 渲染图像 |
| Ctrl+F12 | 渲染动画 |
| 鼠标移动到视图面板的角落，出现十字符，此时按住鼠标左键向**内侧**拖拉 | 新建视图（见下图展示）|
| 鼠标移动到视图面板的角落，出现十字符，此时按住鼠标左键向**外侧**推拉 | 合并视图（见下图展示）|

 ![image](https://user-images.githubusercontent.com/38718148/159126423-13bda3bc-4c7e-4e1f-86b5-1f14590e7010.png)
 
 ![image](https://user-images.githubusercontent.com/38718148/159126141-fabd43c7-630f-493f-8b39-394a4e3a5f5f.png)

<span id="Sec.1.3"></span>
## 1.3. 高阶操作

下面介绍一个稍微复杂一点的操作：调整相机的拍摄视角

1. 按小键盘 0，进入相机当前拍摄视角
2. 按 N，打开右侧工具栏，点击 视图 -> 视图锁定 -> 打开**锁定相机到视图方位**
3. 此时，可以使用对拍摄视角进行旋转（鼠标中建 或 Alt+鼠标左键）和平移（Shift+鼠标中键 或 Alt+Shift+鼠标左键）
4. 调整好后，关闭右侧工具栏中的**锁定相机到视图方位**

![image](https://user-images.githubusercontent.com/38718148/159154284-8df92098-3e8d-453e-b836-d6429b82909e.png)

<span id="Sec.1.4"></span>
## 1.4. 界面常用按钮介绍（仅限脚本相关）

- **工作区 Compositing**：设置后处理的节点；**工作区 Scripting**：通常包含文本编辑器和 Python 控制台，可编写 Python 脚本；**最右侧加号**：添加新的工作区

![image](https://user-images.githubusercontent.com/38718148/159127003-3961889a-ae97-40d5-b1b5-4fb4617c4378.png)

- **编辑器类型**：一般和**新建视图**搭配使用，可在同一界面执行多项任务

![image](https://user-images.githubusercontent.com/38718148/159127451-b40c91c8-5e27-497a-9224-72ee539bf7c6.png)

- 当编辑器类型设置为**文本编辑器**时，可编写 Python 脚本；当设置为 **Python 控制台**时，可快速编写命令，用于验证；当设置为**信息**时，鼠标点击界面不同按钮都会弹出相应的 Python 代码，并且点击代码后按 Ctrl+C 可以直接复制，便于脚本编写

![image](https://user-images.githubusercontent.com/38718148/159148233-77d24ed7-4222-4bbd-952b-3260b47b9dd7.png)


- **视图着色方式**：一般选择中间两个，用最右边的渲染模式可能会很卡

![image](https://user-images.githubusercontent.com/38718148/159127304-feaf1d61-2dbb-4dc3-ac37-ea01964b2417.png)

- **渲染属性**：更改渲引擎及相关设置

![image](https://user-images.githubusercontent.com/38718148/159127952-424dcbc5-7232-47dd-8e5c-ccc2e4cad820.png)

- **输出属性**：调整分辨率，输出路径等相关设置

![image](https://user-images.githubusercontent.com/38718148/159127961-c397f77c-99cf-48f0-afd7-65363e7606af.png)

- **视图层属性**：调整输出通道，开启Z通道可输出深度图

![image](https://user-images.githubusercontent.com/38718148/159127971-d1b012d0-514c-4d10-ac4b-5eaebea35e65.png)

- **物体数据（相机）属性**：调整相机相关参数，可开启景深，并调整光圈大小和聚焦距离

![image](https://user-images.githubusercontent.com/38718148/159127977-c49c6159-9c6c-44ca-a1a7-d688af76f2a6.png)


<span id="Sec.2"></span>
# 2. Python 脚本

<span id="Sec.2.1"></span>
## 2.1. 安装 cv2 包
由于 Blender 的 Python 环境与我们一般使用的 Anaconda 环境不通用，为了后续 Python 脚本的正常运行，还需要安装 cv2 包。参见 [https://blender.stackexchange.com/questions/5287/using-3rd-party-python-modules#](https://blender.stackexchange.com/questions/5287/using-3rd-party-python-modules#)

> - 在 Blender 的 Scripting 工作区的控制台中（控制台如下图所示，注意在编写代码时，鼠标需要保持在当前面板之内），输入
> 
> ```python
> >>> import sys
> >>> sys.exec_prefix
> '/PATH_TO_BLENDER_PYTHON'
> ```
>
> - 在 Linux 或 Windows 命令行界面输入（注意第一行要加 bin）
> 
> ```
> > cd /PATH_TO_BLENDER_PYTHON/bin
> > ./python -m ensurepip
> > ./python -m pip install opencv-python==4.5.4.60（若后续运行脚本时无法打开 .exr 格式图片，可更换 cv2 版本）
> ```
>
> - 安装好后回到 Blender 控制台，输入 import cv2 看是否安装成功

![image](https://user-images.githubusercontent.com/38718148/159147078-1fc417d6-bef2-4fad-8f84-c3a471a1d605.png)

<span id="Sec.2.2"></span>
## 2.2. 脚本使用

- 为了确保脚本正确运行，需要提前用鼠标点击一下**相机**，将其设置为活跃对象（可能存在多个相机，选择渲染过程对应的相机，即按**小键盘 0** 场景对应的相机）

![image](https://user-images.githubusercontent.com/38718148/159153839-dbb36adf-6439-487b-b6b3-8cbd26ef71c3.png)

- 在 Scripting 工作区或其他含有文本编辑器的工作区中新建脚本，复制以下代码并运行。注意更改保存路径。为了加速渲染过程，可适当调整光线采样数量 bpy.context.scene.cycles.samples。程序运行过程中整个界面是卡死的，要想终止程序，只能强行关闭 Blender

```python
# This script works well for Blender 2.93

import bpy
import os
import json
import cv2
import numpy as np

# settings
focus_num = 10  # number of refocused disparity "df". "df" is evenly spaced from the smallest disparity to the largest one
max_blur_radii = np.linspace(10, 50, 5)  # maximum blur radius "K*(d_max-d_min)", or blur parameter "K" if normalizing dispairty range from 0 to 1 

save_root = 'YOUR_ABSOLUTE_PATH'  # change to your absolute path
os.makedirs(save_root, exist_ok=True)


# sensor information
resolution_x = bpy.context.scene.render.resolution_x
resolution_y = bpy.context.scene.render.resolution_y
focal_length = bpy.context.object.data.lens * 1e-3
sensor_width = bpy.context.object.data.sensor_width * 1e-3


# output properties
bpy.context.scene.render.resolution_percentage = 100
bpy.context.scene.render.pixel_aspect_x = 1
bpy.context.scene.render.pixel_aspect_x = 1
bpy.context.scene.render.image_settings.color_mode = 'RGB'
bpy.context.scene.render.image_settings.color_depth = '16'
bpy.context.scene.render.image_settings.file_format = 'OPEN_EXR'


# compositing (do not use compositor when making 3D models !!!)
bpy.context.view_layer.use_pass_combined = True
bpy.context.view_layer.use_pass_z = True
bpy.context.scene.use_nodes = True
tree = bpy.context.scene.node_tree
for node in tree.nodes:
    tree.nodes.remove(node)
render_node = tree.nodes.new(type='CompositorNodeRLayers')
composite_node = tree.nodes.new(type='CompositorNodeComposite')
links = tree.links

# render depth map
links.new(render_node.outputs['Depth'], composite_node.inputs['Image'])
bpy.context.scene.render.engine = 'BLENDER_EEVEE'
bpy.context.scene.eevee.taa_render_samples = 1
bpy.context.scene.render.filepath = os.path.join(save_root, 'depth')
bpy.ops.render.render(write_still=True)
depth = cv2.imread(os.path.join(save_root, 'depth.exr'), -1)[..., 0]
depth_max = depth.max()
depth_min = depth.min()
disp = 1 / depth
disp_range = disp.max() - disp.min()
cv2.imwrite(os.path.join(save_root, 'disparity.jpg'), (disp - disp.min()) / (disp.max() - disp.min()) * 255)


# render all-in-focus image
links.new(render_node.outputs['Image'], composite_node.inputs['Image'])
bpy.context.object.data.dof.use_dof = False
bpy.context.scene.render.engine = 'CYCLES'
bpy.context.scene.cycles.feature_set = 'SUPPORTED'
bpy.context.scene.cycles.device = 'GPU'
bpy.context.scene.cycles.samples = 4096  # decrease to improve efficiency
bpy.context.scene.cycles.use_adaptive_sampling = True
bpy.context.scene.cycles.use_denoising = True
bpy.context.scene.cycles.denoiser = 'OPENIMAGEDENOISE'  # or 'OPTIX'
bpy.context.scene.render.filepath = os.path.join(save_root, 'image')
bpy.ops.render.render(write_still=True)
image = cv2.imread(os.path.join(save_root, 'image.exr'), -1)[..., :3] ** (1/2.2)
cv2.imwrite(os.path.join(save_root, 'image.jpg'), image * 255)


# render bokeh images
bpy.context.object.data.dof.use_dof = True

blur_parameters = []
f_stops = []

focus_distances = list(1/np.linspace(1/depth.max(), 1/depth.min(), focus_num))
for max_blur_radius in max_blur_radii:
    blur_parameter = max_blur_radius / disp_range
    f_stop = 0.5 * focal_length**2 * (resolution_x/sensor_width) / blur_parameter
    blur_parameters.append(blur_parameter)
    f_stops.append(f_stop)

for i, f_stop in enumerate(f_stops):
    bpy.context.object.data.dof.aperture_fstop = f_stop
    for j, focus_distance in enumerate(focus_distances):
        bpy.context.object.data.dof.focus_distance = focus_distance
        bpy.context.scene.render.filepath = os.path.join(save_root, f'bokeh_{i:0>2d}_{j:0>2d}')
        bpy.ops.render.render(write_still=True)
        bokeh = cv2.imread(os.path.join(save_root, f'bokeh_{i:0>2d}_{j:0>2d}.exr'), -1)[..., :3] ** (1/2.2)
        cv2.imwrite(os.path.join(save_root, f'bokeh_{i:0>2d}_{j:0>2d}.jpg'), bokeh * 255)


# save information
info_dict = {
    'resolution_x': resolution_x,
    'resolution_y': resolution_y,
    'focal_length': focal_length,
    'sensor_width': sensor_width,
    'focus_distances': focus_distances,
    'f_stops': f_stops,
    'blur_parameters': blur_parameters
}

info_json = json.dumps(info_dict, sort_keys=False, indent=4, separators=(',', ': '))

f = open(os.path.join(save_root, 'info.json'), 'w')
f.write(info_json)
```

- 若程序报错可按下图操作查看报错信息

![image](https://user-images.githubusercontent.com/38718148/159153954-decf2359-441e-4896-ac56-5afd37528ca2.png)


<span id="Sec.2.3"></span>
## 2.3. 脚本图文说明

- 对于每个场景，设置聚焦点的数量及模糊程度参数，并设置保存数据的路径

```python
# settings
focus_num = 10  # number of refocused disparity "df". "df" is evenly spaced from the smallest disparity to the largest one
max_blur_radii = np.linspace(10, 50, 5)  # maximum blur radii "K*(d_max-d_min)", or blur parameter "K" if normalizing dispairty range from 0 to 1 

save_root = 'YOUR_ABSOLUTE_PATH'  # change to your absolute path
os.makedirs(save_root, exist_ok=True)
```

- 获取图像分辨率及相机参数

```python
# sensor information
resolution_x = bpy.context.scene.render.resolution_x
resolution_y = bpy.context.scene.render.resolution_y
focal_length = bpy.context.object.data.lens * 1e-3
sensor_width = bpy.context.object.data.sensor_width * 1e-3
```

- 调整输出图像的相关设置

```python
# output properties
bpy.context.scene.render.resolution_percentage = 100
bpy.context.scene.render.pixel_aspect_x = 1
bpy.context.scene.render.pixel_aspect_x = 1
bpy.context.scene.render.image_settings.color_mode = 'RGB'
bpy.context.scene.render.image_settings.color_depth = '16'
bpy.context.scene.render.image_settings.file_format = 'OPEN_EXR'
```

- 设置合成节点（代码会清空原有节点），用于导出图片。代码等价于下图所示操作（在 Compositing 工作区中使用 Shift+A 快捷键可添加新节点）

```python
# compositing (do not use compositor when making 3D models !!!)
bpy.context.view_layer.use_pass_combined = True
bpy.context.view_layer.use_pass_z = True
bpy.context.scene.use_nodes = True
tree = bpy.context.scene.node_tree
for node in tree.nodes:
    tree.nodes.remove(node)
render_node = tree.nodes.new(type='CompositorNodeRLayers')
composite_node = tree.nodes.new(type='CompositorNodeComposite')
links = tree.links
```
![image](https://user-images.githubusercontent.com/38718148/159131018-731b69bc-e905-4166-a38a-ef94d63925de.png)

- 渲染并保存深度图（视差图）。使用 Eevee 渲染引擎（Cycles 渲染引擎输出的深度图有孔洞）

```python
# render depth map
links.new(render_node.outputs['Depth'], composite_node.inputs['Image'])
bpy.context.scene.render.engine = 'BLENDER_EEVEE'
bpy.context.scene.eevee.taa_render_samples = 1
bpy.context.scene.render.filepath = os.path.join(save_root, 'depth')
bpy.ops.render.render(write_still=True)
depth = cv2.imread(os.path.join(save_root, 'depth.exr'), -1)[..., 0]
depth_max = depth.max()
depth_min = depth.min()
disp = 1 / depth
disp_range = disp.max() - disp.min()
cv2.imwrite(os.path.join(save_root, 'disparity.jpg'), (disp - disp.min()) / (disp.max() - disp.min()) * 255)
```
![image](https://user-images.githubusercontent.com/38718148/159131046-3ef5398c-3b79-445e-9eda-23880a6976ce.png)

![disparity](https://user-images.githubusercontent.com/38718148/159131783-303adf97-6a92-49a6-87cc-8d0b3fb32638.jpg)


- 渲染并保存全聚焦图。使用 Cycles 渲染引擎。注意，**光线采样数量 bpy.context.scene.cycles.samples 极大影响着渲染速度**，下方渲染的全聚焦图以及后面的散景图均设置光线采样数量为 60

```python
# render all-in-focus image
links.new(render_node.outputs['Image'], composite_node.inputs['Image'])
bpy.context.object.data.dof.use_dof = False
bpy.context.scene.render.engine = 'CYCLES'
bpy.context.scene.cycles.feature_set = 'SUPPORTED'
bpy.context.scene.cycles.device = 'GPU'
bpy.context.scene.cycles.samples = 4096  # decrease to improve efficiency
bpy.context.scene.cycles.use_adaptive_sampling = True
bpy.context.scene.cycles.use_denoising = True
bpy.context.scene.cycles.denoiser = 'OPENIMAGEDENOISE'  # or 'OPTIX'
bpy.context.scene.render.filepath = os.path.join(save_root, 'image')
bpy.ops.render.render(write_still=True)
image = cv2.imread(os.path.join(save_root, 'image.exr'), -1)[..., :3] ** (1/2.2)
cv2.imwrite(os.path.join(save_root, 'image.jpg'), image * 255)
```
![image](https://user-images.githubusercontent.com/38718148/159131144-d00b46db-4248-496c-8110-b02e75e3d246.png)

![image](https://user-images.githubusercontent.com/38718148/159131776-797dfd5c-c0ff-4fdb-b201-574c671769f7.jpg)

- 根据所需模糊程度，计算相应的 f_stops，然后渲染不同聚焦距离和不同模糊程度的散景图像。使用 Cycles 渲染引擎。

```python
# render bokeh images
bpy.context.object.data.dof.use_dof = True

blur_parameters = []
f_stops = []

focus_distances = list(1/np.linspace(1/depth.max(), 1/depth.min(), focus_num))
for max_blur_radius in max_blur_radii:
    blur_parameter = max_blur_radius / disp_range
    f_stop = 0.5 * focal_length**2 * (resolution_x/sensor_width) / blur_parameter
    blur_parameters.append(blur_parameter)
    f_stops.append(f_stop)

for i, f_stop in enumerate(f_stops):
    bpy.context.object.data.dof.aperture_fstop = f_stop
    for j, focus_distance in enumerate(focus_distances):
        bpy.context.object.data.dof.focus_distance = focus_distance
        bpy.context.scene.render.filepath = os.path.join(save_root, f'bokeh_{i:0>2d}_{j:0>2d}')
        bpy.ops.render.render(write_still=True)
        bokeh = cv2.imread(os.path.join(save_root, f'bokeh_{i:0>2d}_{j:0>2d}.exr'), -1)[..., :3] ** (1/2.2)
        cv2.imwrite(os.path.join(save_root, f'bokeh_{i:0>2d}_{j:0>2d}.jpg'), bokeh * 255)
```
![bokeh_04_00](https://user-images.githubusercontent.com/38718148/159132224-908f8278-15ae-4e65-9deb-903746228f8e.jpg)

- 将部分信息保存至 .json 文件中，便于后续方法测试

```python
# save information
info_dict = {
    'resolution_x': resolution_x,
    'resolution_y': resolution_y,
    'focal_length': focal_length,
    'sensor_width': sensor_width,
    'focus_distances': focus_distances,
    'f_stops': f_stops,
    'blur_parameters': blur_parameters
}

info_json = json.dumps(info_dict, sort_keys=False, indent=4, separators=(',', ': '))

f = open(os.path.join(save_root, 'info.json'), 'w')
f.write(info_json)
```
![image](https://user-images.githubusercontent.com/38718148/159134154-c3065615-f70a-472e-801a-775f615ada94.png)

