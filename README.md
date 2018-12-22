# Python_learning
##Difficulties about this codes of greed_snake game.Help ! 
##All of them are based on python，
##problems:1.when it runs, it shows "Game over"  2.the 'DOWN' key can't work
import pygame
import sys
import time
import random
from pygame.locals import *

pygame .init()
fpsClock=pygame.time.Clock
###( 第一行告诉pygame初始化，
##用来控制游戏的速度。然后， 用如下两行代码斯建第二行创建个叫fpsClock的变量，该变量Pygame显示层(游戏元
##素画布)。

playSurface = pygame .display.set_mode((640, 480))
pygame.display.set_caption('Raspbeerry  Snake')
##接下来，你应该定义一些颜色。
##虽然这一步并不是必需的，它会减少你的代时量:如果你想把个对象设置为红色， 你只需要使用esco.变献不化调用pygame.Color指令，也不需要记住红绿蓝3种颜色值。下面的代码定义了程序中的颜色:

redColour = pygame.Color(255, 0, 0)
blackColour = pygame.Color(0,0, 0)
whiteColour = pygame .Color(255,255,255)
greyColour = pygame .Color(150,150, 150)

##如下几行代码初始化了些程序中用到的变量。 这是很重要的一步，因为如果游戏开始时这些变量为空，Python 将无法正常运行。别担心看不懂这些变量，先键入如下代码(只是不要漏掉了右边的逗号和方括号):

snakePosition = [100, 100]
snakeSegments =  [[100, 100], [80,100],[60,100]]
raspberryPosition = [300,300]
raspberrySpawned = 1
direction = 'right '
changeDirection = direction

def gameOver():
        gameOverFont = pygame.font.Font('freesansbold.ttf',72)
        gameOverSurf= gameOverFont.render('Game Over',True,greyColour)

        gameOverRect=gameOverSurf.get_rect()
         
        gameOverRect.midtop= (320,10)
        playSurface.blit (gameOverSurf,gameOverRect)
        pygame.display.flip()
        time. sleep(5)
        pygame.quit()
        sys.exit()
##类似循环，承数中的代码应该缩进。def后边每行代码开头都应该有四个空格的缩进，如果你使用IDLE.这些空格会被自动添加，但是如果你用文本编辑器，你需要手动添加空格。在丽数最后一行 (s.exi() 之后就不需要缩进了。
##gameOver的数用了一些了pygame 命令来完成个简 单的任务:用大号字体将Game Over打印在屏幕上，停留5秒，然后退出pygame和Python程序。在游戏开始之前就定义了结束函数，这看起来有点奇怪，但是所有的函数都应该在被调用前定义。Python 是不会自己执行gameover丽数的，直到我们调用该函数，
##
##程序的开头部分已经完成，接下来进入主要部分。该程序运行在一个无限循环(一个永不退出的while 循环)中，直到蛇撞到了墙或者自己的尾巴才会导致游戏结束。用如下代码开始主循环。

while True:
##没有其他的比较条件，Python会检测True是否为真。因为True一定为真循环会直进行， 直到你调用gmOom函数告诉Pyhton进出该循环。
##键入如下代四，注意代码缩进等级:
        for event in pygame.event.get():
            if event.type ==QUIT:
                pygame.quit ()
                sys.exit()
            elif event.type ==KEYDOWN:
                if event.key == K_RIGHT or event.key == ord('d'):
                    changeDirection = 'right'
                if event.key ==K_LEFT or event.key == ord('a'):
                    changeDirection = 'left'
                if event.key ==K_UP or event.key == ord('w'):
                    changeDirection = 'up'  
                if event.key ==K_DOWN or event.key==ord('s'):
                    changeDirection= 'down '
                if event.key == K_ESCAPE:
                    pygame.event .post (pygame.event.Event (QUIT))
        if changeDirection == 'right' and not direction == 'left':
                direction = changeDirection
        if changeDirection == 'left' and not direction == 'right':
                direction = changeDirection
        if changeDirection == 'up' and not direction == 'down':
                direction = changeDirection
        if changeDirection == 'down' and not direction == 'up':
                direction = changeDirection
        if direction == 'right':
                snakePosition[0]+= 20
        if direction == 'left':
                snakePosition[0]-=20
        if direction =='up':
                snakePosition[1]-= 20
        if direction =='down':
                snakePosition[1]+= 20
        snakeSegments.insert(0,list(snakePosition))
                 
##                                         这里用insert指令来向snakeSegments列表
##                                         (存有蛇”加新项目。每当Python运行到这行，
##                                          它会将蛇的身体增加一节，它的头部。
##                                          在玩家看来蛇在增长。
##                                          当然，你只希望当蛇吃到树有蛇会一 直变长。
##                                          键入如下几行代码:

        if snakePosition[0] ==raspberryPosition[0] and snakePosition[1] == raspberryPosition[1] :
                raspberrySpawned = 0
        else :
                snakeSegments. pop()
        if raspberrySpawned== 0: 
                x=random.randrange(1,32)
                y=random.randrange(1,24)
                raspberryPosition=  [int(x*20),int(y*20)]
        raspberrySpawned=1
##这部分代码通过判断安量asberyspawned是否为0来判断树梅是否物以T如果被吃掉，使用程序开始引入的andom模块获取个随机的位置。 然后梯个位置和蛇的每个小古的长度(20像素宽，20像素高)相乘来确定它在游戏界看的位置。随机地放置树毒是很重要的:防止用户预先知道F一个树莓出现的位置后rapberyspawmned变量置1,以此保证每个时刻界面上只有一个树维。
##现在你有了让蛇移动和生长的所需的代码了，包括树莓的被吃和新建操作(行中称为树莓重生)。但是我们还没有在界面上画东西。键入如下代码:

        playSurface. fill (blackColour)
        for snakePosition in snakeSegments:
                pygame.draw. rect (playSurface, whiteColour,Rect
                                   (snakePosition[0],snakePosition[1],20,20))
        pygame.draw.rect(playSurface, redColour, Rect
                         (raspberryPosition[0], raspberryPosition[1], 20,20))
        pygame.display.flip()

##这些代码让pygame填充背景色为黑色，蛇的头部和身体为白色，树莓为色。最后一行的pygame.display. flip()，让pygame更新界面(如果没8条指令，用户将看不到任何东西。每次当你在界面上画完对象时，记得使wgamne display.fip()来让用户看到更新。
##会感觉无聊的，现在，还没有沙及蛇死亡的代码。如果游戏中的角色永远死不了，玩家排
##所以用如下代码来设置些让蛇死亡的场景:
        if snakePosition[0]>620 or snakePosition[0]<0:
            gameOver()
        if snakePosition[1]>460 or snakePosition[1]<0:
            gameOver()
        for snakeBody in snakeSegments[1:]:
            if  snakePosition[0]==snakeBody[0] and snakePosition[1] ==  snakeBody[1]:
                    gameOver ()
##这里的for语句遍历蛇的每一小
## (从列表的第二项同时和当前蛇头的位置比较。
##  这里我们用snakeSegments[1:项开始遍历。
##列表第一 项为头部的位置，如果从第-项开始千始，蛇就死亡了。
##最后，只需要设置fpsClock变量的值即可控制游戏速度量(在程序开始处创建)，游戏会变得太快而无法正常玩。键入如
fpsClock. tick(20)
