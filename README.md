# Ping-pong-game
The storage contains a prototype of my simple Ping-Pong game. The game was implemented in python code with the help of pygame library. 
There are 2 thin rectangles which can be moved by 2 players, the first one being movable by "w" and "s" keys and the second one with "arrow-up" and "arrow-down".
You can also play it as one player, but I guarantee, it will be harder.
NOTE - the game is early access, and development in progress.

what this update includes:
- changes to window layout, color
- added necessary variables
- implemented and added player objects and the ball (.png files)
- large expansion of the main "while" game cycle




Early code:



from pygame import *

from random import randint


back = (255, 50, 50)

win_width = 1400

win_height = 1000

window = display.set_mode((win_width, win_height))

display.set_caption("Ping-Pong")

window.fill(back)

game = True

finish = False

clock = time.Clock()

FPS = 30



class GameSprite(sprite.Sprite):

    def __init__(self, player_image, player_x, player_y, size_x, size_y, player_speed):
        sprite.Sprite.__init__(self)
 
        #every sprite must store the image property
        self.image = transform.scale(image.load(player_image), (size_x, size_y))
        # načíta obrázok a zmenší ho na 55x55
        
        self.speed = player_speed   # rýchlosť objektu
 
        #every sprite must have the rect property – the rectangle it is fitted in
        self.rect = self.image.get_rect()   # vytvorí rectangle objekt
        self.rect.x = player_x   # nastaví x pozíciu
        self.rect.y = player_y   # nastaví y pozíciu

    def reset(self):
        window.blit(self.image, (self.rect.x, self.rect.y))
        # vykreslí objekt do okna



class Player(GameSprite):

    def update_l(self):
        keys = key.get_pressed()
        
        if keys[K_w] and self.rect.y > 5:
            self.rect.y -= self.speed   # pohyb doľava
            
        if keys[K_s] and self.rect.y < win_width - 80:
            self.rect.y += self.speed   # pohyb doprava


    def update_r(self):
        keys = key.get_pressed()   # zistí stlačené klávesy
        
        if keys[K_UP] and self.rect.y > 5:
            self.rect.y -= self.speed   # pohyb doľava
            
        if keys[K_DOWN] and self.rect.y < win_width - 80:
            self.rect.y += self.speed   # pohyb doprava



racket1 = Player("racket.png", 20, 400, 80, 240, 4)

racket2 = Player("racket.png", 1300, 400, 80, 240, 4)

ball = GameSprite("tenis_ball.png", 400, 400, 80, 80, 4)


speed_x = 3

speed_y = 3


font.init()

font = font.Font(None, 35)


lose1 = font.render("Player one.. eliminated.", True, (180, 0, 0))

lose2 = font.render("Player two.. eliminated.", True, (180, 0, 0))


while game:

    for e in event.get():

        if e.type == QUIT:
            game = False

    if finish != True:

        window.fill(back)

        racket1.update_l()
        
        racket2.update_r()

        ball.rect.x += speed_x

        ball.rect.y += speed_y

        if sprite.collide_rect(racket1, ball) or sprite.collide_rect(racket2, ball):
            speed_x *= -1
            speed_y *= 1

        if ball.rect.y > win_height-50 or ball.rect.y < 0:
            speed_y *= -1

        racket1.reset()

        racket2.reset()

        ball.reset()


    display.update()
