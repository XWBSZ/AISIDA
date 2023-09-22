混沌回忆艾丝妲相关行动顺序计算器。

在开始使用之前，请注意以下几点：

0. 此代码模拟的是混沌回忆第二波的角色行动。

1. 艾丝妲的大招需要在每一次“饮月”，也就是你的慢速主C，奇数次行动时开启。

2. 艾丝妲的大招等级为10级，提供额外50速度，并穿戴4信使套。

3. 除了艾丝妲之外，不考虑其他任何加速减速推条的因素。

如何在手机上运行这个代码：
1. 打开一个在线代码编译网站：
https://replit.com

2. 注册并登录您的账号。

3. 点击蓝色按钮，选择“Create a REPL”。在弹出的界面中，左侧选择Python，右上角为您的项目命名，例如“艾丝妲二动模拟”，然后点击右下角的蓝色按钮创建。

4. 将以下代码粘贴到main.py文件中：

python
Copy code


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
                self.current_speed = self.panel_speed if self.current_speed == self.panel_speed else (
                        self.panel_speed if self.current_speed == self.panel_speed + 50 else self.panel_speed + 50)

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


配置角色属性：
python
Copy code
# 示例角色配置，请根据您的队伍角色属性进行修改
cars = {
    "御空": Car("御空", 107, 170),
    "爱丝妲": Car("爱丝妲", 106, 163),
    "罗刹": Car("罗刹", 101, 162),
    "饮月": Car("饮月", 102, 104.2)
}
调整速度：
如果您的队伍在第二波模拟时有艾丝妲的加速效果，请将以下行中的速度值从0改为50：

python
Copy code
adjust_speed(cars["御空"], 0)
运行模拟：
python
Copy code
print(race())
注意事项：
混沌回忆的第一轮时间为150，第二轮及之后的所有轮次都是100。如果您想模拟三轮以内的角色行动顺序，请将以下行中的时间从250改为350：
python
Copy code
while current_time <= 250:
现在您已经准备好模拟混沌回忆第二波的角色行动了！祝您好运！




User
给我的标题取个名字吧

ChatGPT
当然，请为您的GitHub攻略取一个有趣而专业的标题：

"混沌回忆第二波：角色行动模拟与优化"




User
我觉得前半部分还不够有吸引力

ChatGPT
明白了，为了增加吸引力，您可以考虑以下标题：

"解锁胜利之路：混沌回忆第二波角色行动高级模拟"





Send a message


Free Research Preview. ChatGPT may produce inaccurate information about people, places, or facts. ChatGPT August 3 Version
ChatGPT
