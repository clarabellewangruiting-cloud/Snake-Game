import pygame
import sys
import random

pygame.init() # initialize all imported pygame modules

SW, SH = 650,650 # records screen size into variables
screen = pygame.display.set_mode((650,650)) # creates screen & sets screen size
BLOCK_SIZE = 50 # set variable "BLOCK_SIZE"
clock = pygame.time.Clock() #creates object, clock

class Snake: #defines class object "Snake"
    def __init__(self): #initial state of the class
        self.x, self.y = BLOCK_SIZE, BLOCK_SIZE #defines initial coords
        self.xdir = 1 # default moves in x direction
        self.ydir = 0 # default moves in y direction
        self.head = pygame.Rect(self.x, self.y, BLOCK_SIZE, BLOCK_SIZE) #store rectangular coords
        self.body = [pygame.Rect(self.x-BLOCK_SIZE,self.y,BLOCK_SIZE,BLOCK_SIZE)] #initial state only moving up so only x different between body & head
        self.dead = False
    def update(self): #movement of snake
        global apple
        for square in self.body: #if head hits body, dies
            if self.head.x == square.x and self.head.y == square.y:
                self.dead = True
            if self.head.x not in range (0,SW) or self.head.y not in range (0,SH): # if not in screen, dies
                self.dead = True

        if self.dead: # if dead, restart to default & create new apple
            self.x, self.y = BLOCK_SIZE, BLOCK_SIZE  # defines initial coords
            self.xdir = 1  # default moves in x direction
            self.ydir = 0  # default moves in y direction
            self.head = pygame.Rect(self.x, self.y, BLOCK_SIZE, BLOCK_SIZE)  # store rectangular coords
            self.body = [pygame.Rect(self.x - BLOCK_SIZE, self.y, BLOCK_SIZE,BLOCK_SIZE)]  # initial state only moving up so only x different between body & head
            self.dead = False
            apple = Apple () #create new apple

        self.body.append(self.head) #old head added as new body
        for i in range(len(self.body)-1): # for blocks in body, -1 cuz list starts at 0
            self.body[i].x, self.body[i].y = self.body[i+1].x, self.body[i+1].y # updates body coords, sets variables as current
        self.head.x += self.xdir * BLOCK_SIZE # moves head in x-direction
        self.head.y += self.ydir * BLOCK_SIZE # moves head in y-direction
        self.body.remove(self.head) # not too sure why this fixes the invisible wall after eating apple

class Apple:
    def __init__(self):
        self.x = int(random.randint(0,SW)/BLOCK_SIZE) * BLOCK_SIZE # turns random int into float, rounds it, then turn it back -> makes sure the apple are in the grids
        self.y = int(random.randint(0,SH)/BLOCK_SIZE) * BLOCK_SIZE
        self.rect = pygame.Rect(self.x, self.y, BLOCK_SIZE, BLOCK_SIZE)
    def update (self):
        pygame.draw.rect(screen, "red", self.rect)

def drawGrid():
    for x in range (0, SW, BLOCK_SIZE):
        for y in range (0, SH, BLOCK_SIZE):
            rect = pygame.Rect(x,y, BLOCK_SIZE, BLOCK_SIZE) #creates rectangles with block_size as x & y scales
            pygame.draw.rect(screen, "#3c3c3b", rect, 1)

drawGrid()
snake = Snake ()
apple = Apple ()

while True:
    for event in pygame.event.get(): # intakes input
        if event.type == pygame.QUIT: # stops loop when x is pressed
            pygame.quit()  # uninitialize all pygame modules
            sys.exit()
        if event.type == pygame.KEYDOWN: # keyboard pressed
            if event.key == pygame.K_DOWN: # down arrow key
                snake.ydir = 1
                snake.xdir = 0
            elif event.key == pygame.K_LEFT: # left arrow key
                snake.ydir = 0
                snake.xdir = -1
            elif event.key == pygame.K_RIGHT: # right arrow key
                snake.ydir = 0
                snake.xdir = 1
            elif event.key == pygame.K_UP: # up arrow key
                snake.ydir = -1
                snake.xdir = 0

    # Snake update
    snake.update()
    screen.fill("black")
    drawGrid() #clears field so there is no remanates, the loop can continuously update the position of the snake

    # Apple update
    apple.update()

    pygame.draw.rect(screen, "green", snake.head) # draws the rectangle rect = "snake.head" on the surface = "screen" in color = "green"

    for square in snake.body:
        pygame.draw.rect(screen, "green", square) # draws & color each body rect

    # eating apple
    if snake.head.x == apple.x and snake.head.y == apple.y:
        snake.body.append(pygame.Rect(square.x, square.y, BLOCK_SIZE, BLOCK_SIZE)) # adds body length
        apple = Apple() # sets new position for apple

    pygame.display.update()
    clock.tick(5) #updates the clock to run ___ frames per second
