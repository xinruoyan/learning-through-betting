# Python 外星人小项目

陈小熊

群里共读《蟒蛇书》，因为自己懒，没有跟着参与，其实跟着大家一起折腾会更有意思，如果不跟着，周四开会也没有交流，只是进去逛逛，觉得之前自己过了一遍，当时还在哔哩哔哩找了视频跟着学，加上《自学是一门手艺》重复多遍，基础这块基本没有问题。但其实知识不用就很快忘记。

除了正则表达式我用的较多，其他知识我很少有用的场景，完成付费英语小助手，当时计划付费学习如何用Python + deepl 自动翻译，并形成中英文对照，方便自己阅读和学习英语，后来因为各种事情耽误了。这个需求要计划这两个月完成，记得王雄搞定了，要记得链接请教他。

最近小孩喜欢玩游戏，想引导他们学习英语和编程，于是把书里的外星人小项目整起来，从出现飞机，到飞机可以移动，到可以打子弹，慢慢让他们见到，英语+编程是可以做出一些具体的东西出来，能实现自己想要的各种有趣的想法。

有了这个需求，找到书本，跟着逐字逐句边读，边敲，跟小学生学写字，描红一样，照着写，耗时间，因为经常出错，遇到有疑问的就停下来思考、请教和查阅，不断重复和前进。

如当时开始封装函数的时候，就遇到了问题，怎么都运行不出来，后来问阿坦要了代码，用 VScode 的代码比对功能，比较自己的代码和别人的代码，一比较才发，有一个字弄错了：“main” 写出 “mian”，哈，自己检查了很多遍都检查不出来。所以这个功能很实用。

![301a04734c30e2c7531d9794f64dc5f](https://raw.githubusercontent.com/cxiaoxiong/images/master/202308301555737.png)

在依葫芦画瓢地敲代码时候，感慨笑来老师那句话：一切学习都是说明书。找到正确的说明书，跟着耐心做，就一定能呈现出说明说的效果。但前提说花时间和精力进去。

附上相应的代码。明天开始继续描红，让外星人出场！！

```python
import sys
import pygame

from settings import Settings
from ship import Ship
from bullet import Bullet


class AlienInvasion:
    """初始化游戏资源和行为的类"""

    def __init__(self):
        """初始化游戏并创建游戏资源"""
        pygame.init()  # 初始化背景设置，
        self.settings = Settings()  # 创建Settings实例

       
        self.screen = pygame.display.set_mode((0, 0), pygame.FULLSCREEN)  # 全屏
        self.settings.screen_width = self.screen.get_rect().width  # 更新settings中的配置
        self.settings.screen_height = self.screen.get_rect().height
        self.screen = pygame.display.set_mode((self.settings.screen_width, self.settings.screen_height))
        self.ship = Ship(self)
        self.bullets = pygame.sprite.Group()  # 创建用于存储子弹的编组
        pygame.display.set_caption("Alien Invasion")

    def run_game(self):
        """开始游戏的主循环"""
        while True:  
            self._check_events()
            self.ship.update()
            self._update_bullets()

            # 每次循环重绘屏幕
            self._update_screen()

    def _check_events(self):
        """响应按键和鼠标事件"""
        for event in pygame.event.get():  
            if event.type == pygame.QUIT:  
                sys.exit()  # 退出游戏
            elif event.type == pygame.KEYDOWN:  
                self._check_keydown_events(event)
            elif event.type == pygame.KEYUP:
                self._check_keyup_events(event)

    def _check_keydown_events(self, event):
        """响应按键"""
        
        if event.key == pygame.K_RIGHT:
            self.ship.moving_right = True
        elif event.key == pygame.K_LEFT:
            self.ship.moving_left = True
        elif event.key == pygame.K_SPACE: # 按空格键发射子弹
            self._fire_bullet()
        elif event.key == pygame.K_q: #英文状态下，按 q 退出游戏
            sys.exit()

    def _fire_bullet(self):
        """创建一颗子弹，并将其加入编组bullets中"""
        if len(self.bullets) < self.settings.bullet_allowed:
            new_bullet = Bullet(self)  
            self.bullets.add(new_bullet)

    def _update_bullets(self):
        """更新子弹的位置并删除消失的子弹"""
        self.bullets.update()  

        # 删除消失的子弹
        for bullet in self.bullets.copy():
            if bullet.rect.bottom <= 0:
                self.bullets.remove(bullet)
       

    def _check_keyup_events(self, event):
        """响应松开"""
        if event.key == pygame.K_RIGHT:
            self.ship.moving_right = False
        elif event.key == pygame.K_LEFT:
            self.ship.moving_left = False

    def _update_screen(self):
        """更新屏幕上的图像，并切换到新屏幕"""
        self.screen.fill(self.settings.bg_color)  
        self.ship.blitme()  
        for bullet in self.bullets.sprites():
            bullet.draw_bullet()
        pygame.display.flip()  # 让最近绘制的屏幕可见

if __name__ == '__main__':
    # 创建游戏实例并运行游戏
    ai = AlienInvasion()
    ai.run_game()

```



