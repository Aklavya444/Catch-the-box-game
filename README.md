# Catch-the-box-game
import pygame
import random

#init
print(pygame.init())
print(pygame.mixer.init())

#DEF functions

#text on screen
def screentext(texts,color,x,y):
    text=font.render(texts,True,(color))
    wn.blit(text,(x,y))
    
#def ball making
def ball():
    if balltouch == 0:
        wn.blit(box,(cx,cy))





#Game variables
balltouch=0
width=1100
height=2300
white=255,255,255
red=255,0,0
lsx=100
lsy=20
lx=500
ly=1720
cx=random.randint(50,950)
cy=400
cs=30
score=0
life=3
fps=50
gameoverer=True
welcome=True
running=True


#inintialising variables
wn=pygame.display.set_mode((width,height))
clock=pygame.time.Clock()
font=pygame.font.Font(None,100)



        
#loading area


#gameoverimgae

go=pygame.image.load("gameimages/catchthebox/gameover.png")
gameovers=pygame.transform.scale(go,(width,height))

#welcome imgae

w1=pygame.image.load("gameimages/catchthebox/welcome.png")
welcomee=pygame.transform.scale(w1,(width,height))

#backgrkund loading
back=pygame.image.load("gameimages/catchthebox/background.png")
b1=pygame.transform.scale(back,(width,height))

# carry loading
c1=pygame.image.load("gameimages/catchthebox/carry.png")
carry=pygame.transform.scale(c1,(300,300))

#box loading
bx=pygame.image.load("gameimages/;catchthebox/box.png")
box=pygame.transform.scale(bx,(150,150))





#welcome loop
def welcomes():
    global welcome
    while welcome:
        for event in pygame.event.get():
            if event.type==pygame.KEYDOWN:
                
                #space
                if event.key==pygame.K_SPACE:
                    welcome=False
                #enter
                if event.key==pygame.K_RETURN:
                    gameloop()
                    welcome=False
        
        wn.blit(welcomee,(0,0))
        pygame.display.update()
    

#gameloop
def gameloop():
    
    #global area
    global cx
    global cy
    global life
    global running
    global lx
    global score
    
    while running:
        for event in pygame.event.get():
            if event.type==pygame.KEYDOWN:
                #key areaaa
                #Left key
                if event.key==pygame.K_LEFT:
                    
                    lx-=70
                    
                #Right key
                if event.key==pygame.K_RIGHT:
                    lx+=70
           
           
       #gameloop working area
       
        
        #screenmaking
        wn.blit(b1,(0,0))
               
       #fall the ball       
        cy+=15
        if cy>1950:
            cy=400
            wn.fill(red)           
            life-=1
            if life==0:
                life=3 
                score=0
                gameover()
                running=False
            pygame.display.update()
       
       
        
        #line making
        wn.blit(carry,(lx,ly))
        
        #circle making
        ball()
        
        
        #checking the ball touch
     
        if cy>1700 and cy<1800:
            if abs((lx+100)-cx)<70:
                balltouch=2 

                cx=random.randint(50,950)
                cy=400
                score+=1
                ball()
                balltouch=0
                
        
        
        screentext(("SCORE:- "+str(score)),red,100,100)
        
        screentext(("LIFE:-"+str(life)),red,750,100)
        
        clock.tick(fps)
        pygame.display.update()





#gameover loop
def gameover():
    global gameoverer
    while gameoverer:
        for event in pygame.event.get():
            if event.type==pygame.KEYDOWN:
                
                #space
                if event.key==pygame.K_SPACE:
                    running=False
                    gameoverer=False
                    
                #enter
                if event.key==pygame.K_RETURN:
                    gameloop()
        
        wn.blit(gameovers,(0,0))
        pygame.display.update()
    






welcomes()





