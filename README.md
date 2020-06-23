# final-flappy-birds
import pygame,sys,random
pygame.init()
DISPLAY = pygame.display.set_mode((640, 480))
pygame.display.set_caption('flappy bird')
BASICFONT = pygame.font.SysFont("SIMYOU.TTF", 80)

# 定義顏色變數
BLACK = pygame.Color(0, 0, 0)
WHITE = pygame.Color(255, 255, 255)
RED = pygame.Color(255, 0, 0)
GREY = pygame.Color(150, 150, 150)

class Bird(object):
  def __init__(self):
    self.birdRect = pygame.Rect(65, 50, 50, 50)
    self.birdStatus =[BLACK,RED,GREY]
    self.status = 0      # 預設飛行狀態
    self.birdX = 120     # 鳥所在X軸座標,即是向右飛行的速度
    self.birdY = 350     # 鳥所在Y軸座標,即上下飛行高度
    self.jump = False    # 預設情況小鳥自動降落
    self.jumpSpeed = 10  # 跳躍高度
    self.gravity = 5     # 重力
    self.dead = False    # 預設小鳥生命狀態為活著

  def birdUpdate(self):
    if self.jump:
      # 小鳥跳躍
      self.jumpSpeed -= 1           # 速度遞減，上升越來越慢
      self.birdY -= self.jumpSpeed  # 鳥Y軸座標減小，小鳥上升
    else:
      # 小鳥墜落
      self.gravity += 0.2           # 重力遞增，下降越來越快
      self.birdY += self.gravity    # 鳥Y軸座標增加，小鳥下降
  self.birdRect[1] = self.birdY     # 更改Y軸位置

class Pipeline(object):
    """定義一個管道類"""

    def __init__(self):
        """定義初始化方法"""
        self.wallx = 400  # 管道所在X軸座標
        self.pineUp = pygame.image.load("assets/top.png")
        self.pineDown = pygame.image.load("assets/bottom.png")

    def updatePipeline(self):
        """"管道移動方法"""
        self.wallx -= 5  # 管道X軸座標遞減，即管道向左移動
        # 當管道執行到一定位置，即小鳥飛越管道，分數加1，並且重置管道
        if self.wallx < -80:
            global score
            score += 1
            self.wallx = 400
