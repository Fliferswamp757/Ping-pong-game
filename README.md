# Ping-pong-game
The storage contains a prototype of my simple Ping-Pong game. The game was implemented in python code with the help of pygame library. 
There are 2 thin rectangles which can be moved by 2 players, the first one being movable by "w" and "s" keys and the second one with "arrow-up" and "arrow-down".
You can also play it as one player, but I guarantee, it will be harder.
NOTE - the game is early access, and development in progress.



Early code:



from pygame import *
from random import randint


back = (200, 255, 255)

win_width = 1400
win_height = 1000

window = display.set_mode((win_width, win_height))
display.set_caption("Ping-Pong")

window.fill(back)

class GameSprite(sprite.Sprite):   # základná trieda pre všetky objekty
    #class constructor
    def __init__(self, player_image, player_x, player_y, size_x, size_y, player_speed):
        sprite.Sprite.__init__(self)   # inicializácia rodičovskej triedy
 
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



class Player(GameSprite):   # trieda hráča
    def update_l(self):
        keys = key.get_pressed()   # zistí stlačené klávesy
        
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


while True:
    for e in event.get():
        if e.type == QUIT:
            quit()

    display.update()
