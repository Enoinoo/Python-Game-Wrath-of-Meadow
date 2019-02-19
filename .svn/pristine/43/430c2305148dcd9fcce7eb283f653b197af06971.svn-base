#set position of window
import os
os.environ['SDL_VIDEO_WINDOW_POS'] = "%d,%d" % (400,100)

#set up pygame
import pygame, sys
from pygame.locals import *

pygame.init()
FPS = 30
fpsClock = pygame.time.Clock()

#set up window
DISPLAYSURF = pygame.display.set_mode((800,600))
pygame.display.set_caption('Project 2')

#variables
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
RED = (255, 0, 0)
GREEN = (0, 255, 0)
BLUE = (0,0,255)

#player class
class Player:

    def __init__(self):
        self.maxHealth = 5
        self.Health = 5
        self.maxSpeed = 8
        self.Speed = 5
        self.X = 275
        self.Y = 275
        self.playerBox = ()
        self.AnimationCounter = 0
        self.AnimationStage = 0

        #weapon
        self.Damage = 1
        self.FireRate = 5
        self.ShotSpeed = 20
        
    def __del__(self):
        return

    #call player.display() to put the player sprite on screen
    def display(self,direction):
        #increases animation stage every 8 frames
        if self.AnimationCounter%8 == 0:
                self.AnimationStage +=1
        if self.AnimationStage>3:
                self.AnimationStage = 0
        
        if direction == 'left':
            if self.AnimationStage == 0 or self.AnimationStage == 2:
                return DISPLAYSURF.blit(pygame.image.load('soldierleft.png'),(self.X,self.Y))
            elif self.AnimationStage == 1:
                return DISPLAYSURF.blit(pygame.image.load('soldierleft-leftfoot.png'),(self.X,self.Y))
            elif self.AnimationStage == 3:
                return DISPLAYSURF.blit(pygame.image.load('soldierleft-rightfoot.png'),(self.X,self.Y))

        elif direction == 'right':
            if self.AnimationStage == 0 or self.AnimationStage == 2:
                return DISPLAYSURF.blit(pygame.image.load('soldierright.png'),(self.X,self.Y))
            elif self.AnimationStage == 1:
                return DISPLAYSURF.blit(pygame.image.load('soldierright-leftfoot.png'),(self.X,self.Y))
            elif self.AnimationStage == 3:
                return DISPLAYSURF.blit(pygame.image.load('soldierright-rightfoot.png'),(self.X,self.Y))

        elif direction == 'up':
            if self.AnimationStage == 0 or self.AnimationStage == 2:
                return DISPLAYSURF.blit(pygame.image.load('soldierback.png'),(self.X,self.Y))
            elif self.AnimationStage == 1:
                return DISPLAYSURF.blit(pygame.image.load('soldierback-leftfoot.png'),(self.X,self.Y))
            elif self.AnimationStage == 3:
                return DISPLAYSURF.blit(pygame.image.load('soldierback-rightfoot.png'),(self.X,self.Y))

        elif direction == 'down':
            if self.AnimationStage == 0 or self.AnimationStage == 2:
                return DISPLAYSURF.blit(pygame.image.load('soldierfront.png'),(self.X,self.Y))
            elif self.AnimationStage == 1:
                return DISPLAYSURF.blit(pygame.image.load('soldierfront-leftfoot.png'),(self.X,self.Y))
            elif self.AnimationStage == 3:
                return DISPLAYSURF.blit(pygame.image.load('soldierfront-rightfoot.png'),(self.X,self.Y))


    #updates coordinates of player sprite ( player.move('left', 'down') )
    def move(self, x, y):
        if x == 'left':
            self.X -= self.Speed
            if self.X < 55:
                self.X = 55
        if x == 'right':
            self.X += self.Speed
            if self.X > 725-22:
                self.X = 725-22
        if y == 'up':
            self.Y -= self.Speed
            if self.Y < 35:
                self.Y = 35
        if y == 'down':
            self.Y += self.Speed
            if self.Y > 525-43:
                self.Y = 525-43

    #adds 1 to player health
    def addHealth(self):
        if self.Health < self.maxHealth:
            self.Health += 1

    #creats a Rect of the player in ((left, top), (right, bottom)) form
    def Box(self):
        self.playerBox = ((self.X, self.Y),(self.X+22, self.Y+43))
        return self.playerBox
            
class Enemy:

    def __init__(self,x,y,entrance):
        self.X = x
        self.Y = y
        self.EnemyBox = ()
        self.entrance = entrance
        self.AnimationCounter = 0
        self.AnimationStage = 0

    def __del__(self):
        return

    def subHealth(self, damage):
        if self.Health - damage > 0:
            self.Health -= damage
        else:
            self.Health = 0


class NormalEnemy(Enemy):

    def __init__(self,x,y,entrance, color):
        Enemy.__init__(self,x,y,entrance)
        self.Health = 3
        self.Damage = 1
        self.Speed = 2
        self.color = color
        self.facing = 'left'

    def __del__(self):
        return

    def display(self):
        if self.AnimationCounter%8 == 0:
                self.AnimationStage +=1
        if self.AnimationStage>3:
                self.AnimationStage = 0
        
        if self.facing == 'left':
            if self.AnimationStage == 0 or self.AnimationStage == 2:
                return DISPLAYSURF.blit(pygame.image.load('skeleton-left1.png'),(self.X,self.Y))
            elif self.AnimationStage == 1:
                return DISPLAYSURF.blit(pygame.image.load('skeleton-left2.png'),(self.X,self.Y))
            elif self.AnimationStage == 3:
                return DISPLAYSURF.blit(pygame.image.load('skeleton-left3.png'),(self.X,self.Y))

        elif self.facing == 'right':
            if self.AnimationStage == 0 or self.AnimationStage == 2:
                return DISPLAYSURF.blit(pygame.image.load('skeleton-right1.png'),(self.X,self.Y))
            elif self.AnimationStage == 1:
                return DISPLAYSURF.blit(pygame.image.load('skeleton-right2.png'),(self.X,self.Y))
            elif self.AnimationStage == 3:
                return DISPLAYSURF.blit(pygame.image.load('skeleton-right3.png'),(self.X,self.Y))

        elif self.facing == 'up':
            if self.AnimationStage == 0 or self.AnimationStage == 2:
                return DISPLAYSURF.blit(pygame.image.load('skeleton-back1.png'),(self.X,self.Y))
            elif self.AnimationStage == 1:
                return DISPLAYSURF.blit(pygame.image.load('skeleton-back2.png'),(self.X,self.Y))
            elif self.AnimationStage == 3:
                return DISPLAYSURF.blit(pygame.image.load('skeleton-back3.png'),(self.X,self.Y))

        elif self.facing == 'down':
            if self.AnimationStage == 0 or self.AnimationStage == 2:
                return DISPLAYSURF.blit(pygame.image.load('skeleton-front1.png'),(self.X,self.Y))
            elif self.AnimationStage == 1:
                return DISPLAYSURF.blit(pygame.image.load('skeleton-front2.png'),(self.X,self.Y))
            elif self.AnimationStage == 3:
                return DISPLAYSURF.blit(pygame.image.load('skeleton-front3.png'),(self.X,self.Y))

    def Box(self):
        self.EnemyBox = ((self.X, self.Y),(self.X+24,self.Y+47))
        return self.EnemyBox

    def Follow(self,x,y):
        #always trying to get its coordinates equal to the players
        if y+2<self.Y:
            self.Y-=self.Speed

        elif y-2>self.Y:
            self.Y+=self.Speed

        if x+2<self.X:
            self.X-=self.Speed

        elif x-2>self.X:
            self.X+=self.Speed

        if (x-5<self.X and x+5>self.X) and self.Y>y:
            self.facing = 'up'
        elif (x-5<self.X and x+5>self.X) and self.Y<y:
            self.facing = 'down'
        elif x>self.X:
            self.facing = 'right'
        elif x<self.X:
            self.facing = 'left'

        #stops enemies from moving through walls when entering room
        if self.entrance == 1:
            if self.X<100:
                if self.Y<240:
                    self.Y = 240
                if self.Y>270:
                    self.Y = 270
        if self.entrance == 2:
            if self.Y>475:
                if self.X<285:
                    self.X = 285
                if self.X>370:
                    self.X = 370
        if self.entrance == 3:
            if self.X>675:
                if self.Y<200:
                    self.Y = 200
                if self.Y>230:
                    self.Y = 230
        if self.entrance == 4:
            if self.Y<35:
                if self.X<475:
                    self.X = 475
                if self.X>500:
                    self.X = 500

class BouncingEnemy(Enemy):

    def __init__(self,x,y,entrance, color):
        Enemy.__init__(self,x,y,entrance)
        self.Health = 2
        self.Damage = 1
        self.Speed = 3
        self.Entering = True
        self.color = color
        #initial MoveDirection
        if entrance == 1:
            self.MoveDirection = 'DOWNRIGHT'
        elif entrance == 2:
            self.MoveDirection = 'UPRIGHT'
        elif entrance == 3:
            self.MoveDirection = 'UPLEFT'
        elif entrance == 4:
            self.MoveDirection = 'DOWNLEFT'

    def __del__(self):
        return

    def display(self):
        if self.AnimationCounter%8 == 0:
                self.AnimationStage +=1
        if self.AnimationStage>3:
                self.AnimationStage = 0
        
        if self.MoveDirection == 'UPLEFT' and self.Y<300:
            if self.AnimationStage == 0 or self.AnimationStage == 2:
                return DISPLAYSURF.blit(pygame.image.load('ghost-left1.png'),(self.X,self.Y))
            elif self.AnimationStage == 1:
                return DISPLAYSURF.blit(pygame.image.load('ghost-left2.png'),(self.X,self.Y))
            elif self.AnimationStage == 3:
                return DISPLAYSURF.blit(pygame.image.load('ghost-left3.png'),(self.X,self.Y))

        if self.MoveDirection == 'DOWNLEFT' and self.Y>300:
            if self.AnimationStage == 0 or self.AnimationStage == 2:
                return DISPLAYSURF.blit(pygame.image.load('ghost-left1.png'),(self.X,self.Y))
            elif self.AnimationStage == 1:
                return DISPLAYSURF.blit(pygame.image.load('ghost-left2.png'),(self.X,self.Y))
            elif self.AnimationStage == 3:
                return DISPLAYSURF.blit(pygame.image.load('ghost-left3.png'),(self.X,self.Y))

        elif self.MoveDirection == 'DOWNRIGHT' and self.Y>300:
            if self.AnimationStage == 0 or self.AnimationStage == 2:
                return DISPLAYSURF.blit(pygame.image.load('ghost-right1.png'),(self.X,self.Y))
            elif self.AnimationStage == 1:
                return DISPLAYSURF.blit(pygame.image.load('ghost-right2.png'),(self.X,self.Y))
            elif self.AnimationStage == 3:
                return DISPLAYSURF.blit(pygame.image.load('ghost-right3.png'),(self.X,self.Y))

        elif self.MoveDirection == 'UPRIGHT' and self.Y<300:
            if self.AnimationStage == 0 or self.AnimationStage == 2:
                return DISPLAYSURF.blit(pygame.image.load('ghost-right1.png'),(self.X,self.Y))
            elif self.AnimationStage == 1:
                return DISPLAYSURF.blit(pygame.image.load('ghost-right2.png'),(self.X,self.Y))
            elif self.AnimationStage == 3:
                return DISPLAYSURF.blit(pygame.image.load('ghost-right3.png'),(self.X,self.Y))

        elif (self.MoveDirection == 'UPLEFT' or self.MoveDirection == 'UPRIGHT') and self.Y>300:
            if self.AnimationStage == 0 or self.AnimationStage == 2:
                return DISPLAYSURF.blit(pygame.image.load('ghost-back1.png'),(self.X,self.Y))
            elif self.AnimationStage == 1:
                return DISPLAYSURF.blit(pygame.image.load('ghost-back2.png'),(self.X,self.Y))
            elif self.AnimationStage == 3:
                return DISPLAYSURF.blit(pygame.image.load('ghost-back3.png'),(self.X,self.Y))

        elif (self.MoveDirection == 'DOWNLEFT' or self.MoveDirection == 'DOWNRIGHT') and self.Y<300:
            if self.AnimationStage == 0 or self.AnimationStage == 2:
                return DISPLAYSURF.blit(pygame.image.load('ghost-front1.png'),(self.X,self.Y))
            elif self.AnimationStage == 1:
                return DISPLAYSURF.blit(pygame.image.load('ghost-front2.png'),(self.X,self.Y))
            elif self.AnimationStage == 3:
                return DISPLAYSURF.blit(pygame.image.load('ghost-front3.png'),(self.X,self.Y))

    def Box(self):
        self.EnemyBox = ((self.X, self.Y),(self.X+30,self.Y+43))
        return self.EnemyBox

    def Move(self):
        #entering is true if the enemy is still in an entrance
        if self.Entering:
            if self.entrance == 1:
                if self.X<50:
                    if self.Y<250:
                        self.MoveDirection = 'DOWNRIGHT'
                    elif self.Y>275:
                        self.MoveDirection = 'UPRIGHT'
                else:
                    self.Entering = False
            elif self.entrance == 2:
                if self.Y>500:
                    if self.X<275:
                        self.MoveDirection = 'UPRIGHT'
                    elif self.X>375:
                        self.MoveDirection = 'UPLEFT'
                else:
                    self.Entering = False
            elif self.entrance == 3:
                if self.X>700:
                    if self.Y<220:
                        self.MoveDirection = 'DOWNLEFT'
                    elif self.Y>245:
                        self.MoveDirection = 'UPLEFT'
                else:
                    self.Entering = False
            elif self.entrance == 4:
                if self.Y<25:
                    if self.X<475:
                        self.MoveDirection = 'DOWNRIGHT'
                    elif self.X>500:
                        self.MoveDirection = 'DOWNLEFT'
                else:
                    self.Entering = False
        #once the enemy has got through an entrance it will bounce off walls
        else:
            if self.X < 75:
                if self.MoveDirection == 'DOWNLEFT':
                    self.MoveDirection = 'DOWNRIGHT'
                else:
                    self.MoveDirection = 'UPRIGHT'

            elif self.X > 720-30:
                if self.MoveDirection == 'DOWNRIGHT':
                    self.MoveDirection = 'DOWNLEFT'
                else:
                    self.MoveDirection = 'UPLEFT'

            if self.Y < 30:
                if self.MoveDirection == 'UPLEFT':
                    self.MoveDirection = 'DOWNLEFT'
                else:
                    self.MoveDirection = 'DOWNRIGHT'

            elif self.Y > 525-43:
                if self.MoveDirection == 'DOWNLEFT':
                    self.MoveDirection = 'UPLEFT'
                else:
                    self.MoveDirection = 'UPRIGHT'

        #takes MoveDirection and adjusts coordinates
        if self.MoveDirection == 'DOWNLEFT':
            self.X -= self.Speed+1
            self.Y += self.Speed

        elif self.MoveDirection == 'DOWNRIGHT':
            self.X += self.Speed+1
            self.Y += self.Speed

        elif self.MoveDirection == 'UPLEFT':
            self.X -= self.Speed+1
            self.Y -= self.Speed

        elif self.MoveDirection == 'UPRIGHT':
            self.X += self.Speed+1
            self.Y -= self.Speed


class bullet:

    def __init__(self,x,y,speed,direction):
        self.X = x
        self.Y = y
        self.ShotSpeed = speed
        self.direction = direction
        self.BulletBox = ()

    def __del__(self):
        return

    def move(self):
        if self.direction == 'left':
            self.X-=self.ShotSpeed        
        if self.direction == 'right':
            self.X+=self.ShotSpeed
        if self.direction =='up':
            self.Y-=self.ShotSpeed
        if self.direction == 'down':
            self.Y+=self.ShotSpeed

    #displays bullet, changing shape depending on the direction it is shot in
    def display(self):
        if self.direction == 'left':
            return DISPLAYSURF.blit(pygame.image.load('bullet-left.png'),(self.X, self.Y+22))
        elif self.direction == 'right':
            return DISPLAYSURF.blit(pygame.image.load('bullet-right.png'),(self.X+22, self.Y+22))
        elif self.direction == 'up':
            return DISPLAYSURF.blit(pygame.image.load('bullet-up.png'),(self.X+5, self.Y))
        elif self.direction == 'down':
            return DISPLAYSURF.blit(pygame.image.load('bullet-down.png'),(self.X+5, self.Y))

    #hitbox for collision detection
    def Box(self):
        if self.direction == 'left':
            self.BulletBox = ((self.X, self.Y+22),(self.X+10,self.Y+27))
        elif self.direction == 'right':
            self.BulletBox = ((self.X+20, self.Y+22),(self.X+30,self.Y+27))
        elif self.direction == 'up' or self.direction == 'down':
            self.BulletBox = ((self.X+5, self.Y),(self.X+10,self.Y+10))
        return self.BulletBox
            
class Heart:
    def __init__(self,x,y):
        self.X = x
        self.Y = y
        self.type = "Heart"
    def __del__(self):
        return
    def display(self):
        return DISPLAYSURF.blit(pygame.image.load('heart.png'),(self.X,self.Y))
    def Box(self):
        return ((self.X,self.Y),(self.X+10,self.Y+10))

class Powerup:
    def __init__(self,x,y,kind):
        self.X = x
        self.Y = y
        self.type = kind
    def __del__(self):
        return
    def display(self):
        if self.type == 'HealthUp':
            pygame.draw.rect(DISPLAYSURF, RED, (self.X,self.Y,10,10))
        if self.type == 'FireRateUp':
            return DISPLAYSURF.blit(pygame.image.load('FireRate.png'),(self.X,self.Y))
    def Box(self):
        return ((self.X,self.Y),(self.X+10,self.Y+10))


        
#returns true if there is an intersection between R1 and R2
#R1 and R2 are of the form ((left,top),(right,bottom))
def intersect(R1,R2):
    left = max(R1[0][0],R2[0][0])
    right = min(R1[1][0],R2[1][0])
    top = max(R1[0][1],R2[0][1])
    bot = min(R1[1][1],R2[1][1])
    if (left > right) or (top > bot):
        return False
    else:
        return True

#music
pygame.mixer.music.load('song.wav')
GunShot = pygame.mixer.Sound('GUN shot.wav')
Death = pygame.mixer.Sound('deathsound.wav')
GameWin = pygame.mixer.Sound('gamewin.wav')
EnemyKilled = pygame.mixer.Sound('enemiekillsound.wav')


#variables
directionX = ''
directionY = ''
ShotDirection = ''
Bullets = []
Enemies = []
Items = []
ShotTimer = 0
ShotFired = False
Vulnerable = True
VulnerableTimer = 0
EnemiesKilled = 0
FrameCount = 0
Pause = False
player = Player()
facing = 'down'
level = 3
GameState = 0


#choose set of numbers from 1 to 4 randomly without choosing the same number
import random
def random_combination(r):
    pool = (1,2,3,4)
    n = len(pool)
    indices = sorted(random.sample(xrange(n), r))
    return tuple(pool[i] for i in indices)


#Game Loop
while True:
    #title screen
    if GameState == 0:
        DISPLAYSURF.blit(pygame.image.load('StartMenu.png'),(0,0))
    #game    
    if GameState == 1:
        if not Pause:
            if level == 1:
                #backround
                DISPLAYSURF.blit(pygame.image.load('Start.png'),(0, 0))
                                
            elif level == 2:
                DISPLAYSURF.blit(pygame.image.load('To Swamp.png'),(0, 0))
            elif level == 3:
                DISPLAYSURF.blit(pygame.image.load('swamp.png'),(0, 0))

                #Chooses the number of enemies that spawn at a time
                #for the first 540 frames only 1 enemy spawns at a time, after it is then randomly chosen between 1 and 4
                #EnemiesKilled determines when the player wins
                SpawnNumber = 0
                if EnemiesKilled < 10:
                    if (FrameCount%180 == 0) and FrameCount<540:
                        #1<=SpawnNumber<=4
                        SpawnNumber = 1
                        entrance = random_combination(SpawnNumber)
                    elif FrameCount>540 and (FrameCount%210 ==0 or FrameCount == 540):
                        SpawnNumber = random.randint(1,4)
                        entrance = random_combination(SpawnNumber)
                elif len(Enemies)==0:
                    GameState = 3
                    
                entrance = random_combination(SpawnNumber)
                #adds enemies to list placed at a random entrance
                for i in entrance:
                    if i == 1:
                        #25% chance to spawn a bouncing Enemy
                        if random.randint(1,4) == 1:
                            #10% chance to Spawn a blue bouncing enemy (drops item/powerup)
                            if random.randint(1,100)<=10:
                                Enemies.append(BouncingEnemy(-50,250, i, BLUE))
                            else:
                                Enemies.append(BouncingEnemy(-50,250, i, GREEN))
                        #75% chance to spawn a normal enemy
                        else:
                            #10% chance to spawn a blue normal enemy
                            if random.randint(1,100)<=10:
                                Enemies.append(NormalEnemy(-50,250, i, BLUE))
                            else:
                                Enemies.append(NormalEnemy(-50,250, i, RED))
                    if i == 2:
                        if random.randint(1,4) == 1:
                            if random.randint(1,100)<=10:
                                Enemies.append(BouncingEnemy(300,630, i, BLUE))
                            else:
                                Enemies.append(BouncingEnemy(300,630, i, GREEN))
                        else:
                            if random.randint(1,100)<=10:
                                Enemies.append(NormalEnemy(300,630, i, BLUE))
                            else:
                                Enemies.append(NormalEnemy(300,630, i, RED))
                    if i == 3:
                        if random.randint(1,4) == 1:
                            if random.randint(1,100)<=10:
                                Enemies.append(BouncingEnemy(800,225, i, BLUE))
                            else:
                                Enemies.append(BouncingEnemy(800,225, i, GREEN))
                        else:
                            if random.randint(1,100)<=10:
                                Enemies.append(NormalEnemy(800,225, i, BLUE))
                            else:
                                Enemies.append(NormalEnemy(800,225, i, RED))
                    if i == 4:
                        if random.randint(1,4) == 1:
                            if random.randint(1,100)<=10:
                                Enemies.append(BouncingEnemy(500,-50, i, BLUE))
                            else:
                                Enemies.append(BouncingEnemy(500,-50, i, GREEN))
                        else:
                            if random.randint(1,100)<=10:
                                Enemies.append(NormalEnemy(500,-50, i, BLUE))
                            else:
                                Enemies.append(NormalEnemy(500,-50, i, RED))
                
     
            directionX = ''
            directionY = ''
            ShotDirection = ''

            #player movement
            #pygame.key.get_pressed() returns a list of all keyspressed
            Keys = pygame.key.get_pressed() 
            #use if statements to search if a specific key is pressed
            if Keys[pygame.K_a]:
                directionX = 'left'
            if Keys[pygame.K_d]:
                directionX = 'right'
            if Keys[pygame.K_w]:
                directionY = 'up'
            if Keys[pygame.K_s]:
                directionY = 'down'
            #increments animation counter if buttons are held
            if Keys[pygame.K_a] or Keys[pygame.K_d] or Keys[pygame.K_w] or Keys[pygame.K_s]:
                player.AnimationCounter+=1
            #resets animation counter and animation stage to 0 when nothing is pressed
            else:
                player.AnimationCounter = 1
                player.AnimationStage = 0

            #shooting
            if Keys[pygame.K_LEFT]:
                 ShotDirection = 'left'
            if Keys[pygame.K_RIGHT]:
                ShotDirection = 'right'
            if Keys[pygame.K_UP]:
                ShotDirection = 'up'
            if Keys[pygame.K_DOWN]:
                ShotDirection = 'down'

            #allows for a delay between shots (FireRate)
            if ShotDirection != '' and ShotTimer == 0:
                GunShot.play()
                Bullets.append(bullet(player.X, player.Y, player.ShotSpeed, ShotDirection))
                ShotFired = True
                ShotTimer = 30-2*player.FireRate    #sets a delay for when the next bullet can be created (aka Fire Rate)

            if ShotTimer>0:
                ShotTimer-=1


            #Shooting
            for i in range(len(Bullets)):
                if i <= len(Bullets)-1:
                    if Bullets[i] == None:
                        Bullets.remove(None)
                    else:
                        Bullets[i].move()
                        Bullets[i].display()
                        #checks if bullet has hit a wall
                        if 0>Bullets[i].X>800 or 0>Bullets[i].Y>800:
                            Bullets[i] = None
                        #checks if bullet has hit an enemy
                        for k in range (len(Enemies)):
                            if k <= len(Enemies)-1:
                                if Enemies[k] != None and Bullets[i] != None:
                                    if intersect(Bullets[i].Box(),Enemies[k].Box()):    #checks if a bullet hit an enemy
                                        Bullets[i] = None
                                        Enemies[k].subHealth(player.Damage) #subtract enemy health by amount of damage a bullet does
                                    if Enemies[k].Health<=0:
                                        #if enemy is blue add either a heart or a powerup top the item list
                                        if Enemies[k].color == BLUE:
                                            #75% chance to add a heart to item list
                                            if random.randint(1,4)<3:
                                                Items.append(Heart(Enemies[k].X,Enemies[k].Y))
                                            #25 chance to add a powerup
                                            else:
                                                #50/50 chance for HealthUp or FireRate
                                                if random.randint(1,2)==1:
                                                    Items.append(Powerup(Enemies[k].X,Enemies[k].Y,'HealthUp'))
                                                else:
                                                    Items.append(Powerup(Enemies[k].X,Enemies[k].Y,'FireRateUp'))            
                                        EnemyKilled.play()
                                        Enemies[k] = None
                                        EnemiesKilled+=1

            for i in range (len(Enemies)):
                if i <= len(Enemies)-1:
                    if Enemies[i] == None:
                        Enemies.remove(None)
                    else:
                        #if Enemies[i] is a BouncingEnemy try: will fail because that method isnt in that class so it will do what is in except:
                        try:
                            Enemies[i].Follow(player.X,player.Y)
                        except:
                            Enemies[i].Move()
                        Enemies[i].display()
                        Enemies[i].AnimationCounter+=1
                        if intersect(Enemies[i].Box(), player.Box()) and Vulnerable:    #checks if an enemy touched the player and if the player hasnt just been hit
                            player.Health-=Enemies[i].Damage #decrease player health if hit by enemy
                            print player.Health
                            if player.Health == 0:
                                GameState = 2
                            Vulnerable = False
                            VulnerableTimer = 120  #creates a timer for how long the player is invincible
            
            for i in range (len(Items)):
                if i <= len(Items)-1:
                    Items[i].display()
                    #if player touches item, delete that item from screen
                    if intersect(Items[i].Box(),player.Box()):
                        if Items[i].type == 'Heart':
                            if player.Health<player.maxHealth:
                                player.Health+=1
                                print player.Health
                                Items[i] = None
                        elif Items[i].type == 'HealthUp':
                            player.maxHealth+=1
                            player.Health+=1
                            Items[i] = None
                        elif Items[i].type == 'FireRateUp':
                            player.FireRate+=2
                            Items[i] = None
                        if Items[i] == None:
                            Items.remove(None)
            
            #decriments the Vulnerable timer           
            if VulnerableTimer > 0:
                VulnerableTimer-=1
            if VulnerableTimer == 0:
                Vulnerable = True

            #if player is hit, the player will blink indicating he can not be hurt 
            if not Vulnerable and VulnerableTimer%10==0:
                pass
            else:
                if ShotDirection != '':
                    facing = ShotDirection
                elif directionY != '':
                    facing = directionY
                elif directionX != '':
                    facing = directionX
                player.display(facing)
            player.move(directionX,directionY)

            FrameCount+=1

        else:
            DISPLAYSURF.blit(pygame.image.load('Pause2.png'),(0,0))

        #death screen
        if GameState == 2:
            pygame.mixer.music.stop()
            DISPLAYSURF.blit(pygame.image.load('gameover.png'),(0,0))
            Death.play()
        #win screen
        if GameState == 3:
            pygame.mixer.music.stop()
            DISPLAYSURF.blit(pygame.image.load('Win.png'),(0,0))
            GameWin.play()
   
    for event in pygame.event.get():
        
        if event.type == QUIT:
            pygame.quit()
            sys.exit()

        if event.type == pygame.KEYDOWN:
            if GameState == 0:
                if event.key == K_SPACE:
                    GameState = 1
                    pygame.mixer.music.play(-1,0.0)
                if event.key == K_ESCAPE:
                    pygame.quit()
                    sys.exit()
            #game
            if GameState == 1:
                if Pause and event.key == K_ESCAPE:
                    Pause = False
                elif event.key == K_ESCAPE:
                    Pause = True
            #lose screen
            if GameState == 2:
                if event.key == K_ESCAPE:
                    #variables
                    directionX = ''
                    directionY = ''
                    ShotDirection = ''
                    Bullets = []
                    Enemies = []
                    ShotTimer = 0
                    ShotFired = False
                    Vulnerable = True
                    VulnerableTimer = 0
                    EnemiesKilled = 0
                    FrameCount = 0
                    Pause = False
                    player = Player()

                    GameState = 0
                if event.key == K_SPACE:
                    #variables
                    directionX = ''
                    directionY = ''
                    ShotDirection = ''
                    Bullets = []
                    Enemies = []
                    Items = []
                    ShotTimer = 0
                    ShotFired = False
                    Vulnerable = True
                    VulnerableTimer = 0
                    EnemiesKilled = 0
                    FrameCount = 0
                    Pause = False
                    player = Player()
                    facing = 'down'

                    GameState = 1
            #win screen
            if GameState == 3:
                if event.key == K_ESCAPE:
                    #variables
                    directionX = ''
                    directionY = ''
                    ShotDirection = ''
                    Bullets = []
                    Enemies = []
                    Items = []
                    ShotTimer = 0
                    ShotFired = False
                    Vulnerable = True
                    VulnerableTimer = 0
                    EnemiesKilled = 0
                    FrameCount = 0
                    Pause = False
                    player = Player()
                    facing = 'down'

                    GameState = 0
                if event.key == K_SPACE:
                    #variables
                    directionX = ''
                    directionY = ''
                    ShotDirection = ''
                    Bullets = []
                    Enemies = []
                    Items = []
                    ShotTimer = 0
                    ShotFired = False
                    Vulnerable = True
                    VulnerableTimer = 0
                    EnemiesKilled = 0
                    FrameCount = 0
                    Pause = False
                    player = Player()
                    facing = 'down'

                    GameState = 1
                
    pygame.display.update()
    pygame.display.flip()
    fpsClock.tick(FPS)
