# 混沌回忆艾丝妲行动顺序计算器

欢迎使用混沌回忆艾丝妲相关行动顺序计算器，通过这个工具，您可以优化您的战斗策略，提高战斗效率和胜率。本文将为您提供详细的使用说明，让您轻松上手。

## 使用前须知

在开始使用计算器之前，请注意以下几点：

- 此计算器模拟的是混沌回忆第二波的角色行动。
- 艾丝妲的大招需要在每一次“饮月”，也就是您的慢速主C，奇数次行动时开启。
- 艾丝妲的大招等级为10级，提供额外50速度，并穿戴4信使套。
- 除了艾丝妲之外，不考虑其他任何加速减速推条的因素。

## 如何运行计算器

### 1. 打开在线代码编译网站

首先，打开一个在线代码编译网站，我们建议使用 [Replit](https://replit.com/)。

### 2. 注册并登录

如果您还没有账号，注册并登录您的账号。

### 3. 创建项目

点击蓝色按钮，选择“Create a REPL”。在弹出的界面中，左侧选择Python，右上角为您的项目命名，例如“艾丝妲行动模拟”，然后点击右下角的蓝色按钮创建。

### 4. 粘贴代码

将以下代码粘贴到 `main.py` 文件中：

```python
class Car:
    def __init__(self, name, base_speed, panel_speed):
        self.name = name
        self.base_speed = base_speed
        self.panel_speed = panel_speed
        self.current_speed = panel_speed
        self.current_position = 0
        self.return_count = 0

    def update_position(self, delta_t):
        self.current_position += self.current_speed * delta_t

    def check_return(self, track_length):
        if self.current_position >= track_length:
            self.current_position -= track_length
            self.return_count += 1
            if self.name == "饮月" and self.return_count % 2 == 1:
                for car in cars.values():
                    car.current_speed = car.base_speed * 0.12 + 50 + car.panel_speed
            else:
                self.current_speed = (
                    self.panel_speed
                    if self.current_speed == self.panel_speed
                    else (
                        self.panel_speed
                        if self.current_speed == self.panel_speed + 50
                        else self.panel_speed + 50
                    )
                )
            return True
        else:
            return False

TRACK_LENGTH = 10000
DELTA_T = 0.001

cars = {
    "御空": Car("御空", 107, 170),
    "爱丝妲": Car("爱丝妲", 106, 163),
    "罗刹": Car("罗刹", 101, 162),
    "饮月": Car("饮月", 102, 104.2)
}

def adjust_speed(car, speed_delta):
    car.current_speed += speed_delta

adjust_speed(cars["御空"], 0)
adjust_speed(cars["爱丝妲"], 50)
adjust_speed(cars["罗刹"], 50)
adjust_speed(cars["饮月"], 50)

def race():
    result = []
    current_time = 0
    while current_time <= 250:
        for name, car in cars.items():
            car.update_position(DELTA_T)
            if car.check_return(TRACK_LENGTH):
                lap_time = current_time
                lap_count = car.return_count
                result.append((lap_time, name, lap_count))
        current_time += DELTA_T
    result.sort()
    return "\n".join([f"({item[1]}, {item[0]:.2f}, {item[2]})" for item in result])

print(race())
```

### 5. 配置角色属性

在代码中，您可以根据您的队伍角色属性进行修改。例如，如果您的御空的基础速度是108，面板速度是172，您可以将以下行中的数字改为相应的值：

```python
cars = {
    "御空": Car("御空", 108, 172),
    ...
}
```

### 6. 调整速度

如果您的队伍在第二波开始时有上一波艾丝妲的加速效果，请将以下行中的速度值从0改为50：

```python
adjust_speed(cars["御空"], 50)
```

### 7. 运行模拟

在代码编辑器的右上角，点击绿色按钮，选择“Run”。代码将开始运行，并在下方显示输出结果。

## 输出结果解释

运行完毕后，您会看到类似以下输出结果：

```
(爱丝妲, 46.95, 1)
(罗刹, 47.17, 1)
(御空, 58.82, 1)
(饮月, 64.85, 1)
(爱丝妲, 96.23, 2)
(罗刹, 96.69, 2)
(御空, 103.40, 2)
(饮月, 124.93, 2)
(爱丝妲, 143.17, 3)
(罗刹, 143.86, 3)
(御空, 148.85, 3)
(饮月, 189.78, 3)
(爱丝妲, 200.43, 4)
(罗刹, 201.21, 4)
(御空, 202.85, 4)
(爱丝妲, 247.38, 5)
(御空, 248.30, 5)
(罗刹, 248.38, 5)
(饮月, 249.87, 4)
```

输出结果的含义是：

- 每一行代表一个角色完成一圈的时间、名称和行动次数。
- 每一行的格式为：(角色名称, 完成时间, 行动次数数)。
- 输出结果按照完成时间从小到大排序。

例如，第一行的结果是：

```
(爱丝妲, 46.95, 1)
```

这意味着爱丝妲在46.95秒时完成了第一次的行动。

您可以根据这些结果来调整您的战斗策略，以便更好地安排角色的行动顺序，从而提高您的战斗效率和胜率。

祝您在混沌回忆中取得胜利！如果您有任何问题或需要进一步的帮助，请随时提问。
