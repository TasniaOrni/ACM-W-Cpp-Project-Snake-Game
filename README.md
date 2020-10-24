#include <iostream>
#include <conio.h>
#include<stdlib.h>
#include<stdin.h>
using namespace std;
const int width=20,hight=20;;
int x,y,fruitx,fruity,score;
bool gameover;
int tailX[100],tailY[100],ntail;
enum eDirection{
    STOP=0,
    LEFT,
    RIGHT,
    UP,
    DOWN
};
eDirection dir;

void setup(){
    gameover=false;
    dir=STOP;
    x=width/2;
    y=hight/2;
    fruitx=rand()%width;
    fruity=rand()%hight;
    score=0;
}
void draw(){
    system("clear");//system("cls");
    for (int i=0; i<width+4; i++)
        cout<<"=";
    
    cout<<endl;
    
    for (int i=0; i<hight; i++) {
        for (int j=0; j<width; j++) {
            if (j==0)
                cout<<"||";
            if (i== y && j==x)
                cout<<"O";
            else if(i==fruity && j==fruitx)
                cout<<"F";
            else{
                
                bool print=false;
                
                for (int k=0; k<ntail; k++) {
                    
                    if (tailX[k]==j && tailY[k]==i) {
                        cout<<"o";
                        print=true;
                    }
                   
                }
                if (!print) {
                    cout<<" ";
                    
                }
                cout<<endl;
            }
            if (j==width-1)
                cout<<"||";
        }
                cout<<endl;
    }
    for (int i=0; i<width+4; i++)
        cout<<"=";
    
    cout<<endl;
    cout<<"SCORE : "<<score<<endl;
}

void input(){
    
    if (_kbhit()){
        
        //ei function 2 ta amar lappy te run kore na
        switch (_getch()) {
            case 'a':
            dir=LEFT;
            break;
            case 'd':
            dir=RIGHT;
            break;
            case 'w':
            dir=UP;
            break;
            case 's':
            dir=DOWN;
            break;
            case 'x':
                gameover=true;
            break;
                }
            }
    }
void logic(){
    int prevX=tailX[0];
    int prevY=tailY[0];
    int prev2X,prev2Y;
    tailX[0]=x;
    tailY[0]=y;
    
    for (int i=0; i<ntail; i++) {
        prev2X=tailX[i];
        prev2Y=tailY[i];
        prevX=prev2X;
        prevY=prev2Y;
    }
    
    switch (dir) {
        case RIGHT:
            x++;
            break;
        case LEFT:
            x--;
            break;
        case UP:
            y++;
            break;
        case DOWN:
            y--;
            break;
        default:
            break;
            
    }
    if (x>width || x <0 || y>hight || y<0) {
        gameover=true;
    }
    for (int i=0; i<ntail; i++) {
        if (tailX[i]==x && tailY[i]==y) {
            gameover=true;
        }
    }
    
    if (x==fruitx && y==fruity) {
        
        score+=10;
        fruitx=rand()%width;
        fruity=rand()%hight;
        ntail++;
    }
}
    
int main(){
    
    setup();
    while (!gameover) {
        draw();
        input();
        logic();
    }
    return 0;
}


 
 
 
