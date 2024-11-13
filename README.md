# snake--AP-project
#include <iostream>
#include <vector>
#include <ctime>
#include <cstdlib>
#include <conio.h>
#include <windows.h>

using namespace std;

void menu(){
    cout<<"\t--------------------------welcom back-----------------------------------\n";
    
    cout<<"\t|\t1.START      2.ABOUT US       3.HELP       4.SETING            |\n";
    
    cout<<"\t------------------------------------------------------------------------\n";   
    
    
    
}
void ABOUTUS(){
	
	cout<<"\t------------------------------------------------------------------------\n";
	cout<<"\t                          about us\n";
	cout<<"        Team Members : Fereshteh Tabeei, Mina Sajadi, Atefe Kalamati\n" 
	    <<"        Email : fe.tabeei@gmail.com, minasajadi1383@gmail.com,  \n"
	    <<"        Atefekalamati@gmail.com\n"
	    <<"        Teacher : Dr. Amintoosi\n"
	    <<"        Advanced programming class\n";
	
}
void HELP(){
	cout<<"\t------------------------------------------------------------------------\n";
	cout<<"\t                          HELP\n";
	cout<<"        Three components in the game:\n"
	    <<"        O: snake\n"
	    <<"        E: snake's enemy. You can't let the enemy hits the snake.\n"
	    <<"        F: Food. snake eats food and adds to the length of its tail. \n"
	    <<"        ------------------------------------------------------------------------ \n"
	    <<"        In the game when you type \n"
	    <<"        a: the snake changes its way to the left. \n"
	    <<"        d: the snake changes its way to the right. \n"
	    <<"        w: the snake changes its way to the up.\n"
	    <<"        s: the snake changes its way to the down. \n"
	    <<"        x: you quit the game. \n";
}
void SETING(){
	
    cout<<"\t------------------------------------------------------------------------\n";
    cout<<"\t                          SETING\n";
    
    cout<<"\t   color   |   code   \n";
    cout<<"\t----------------------\n";
    cout<<"\t   black   |   0      \n";
    cout<<"\t   blue    |   1      \n";
    cout<<"\t   green   |   2      \n";
    cout<<"\t   cyan    |   3      \n";
    cout<<"\t   red     |   4      \n";
    cout<<"\t   purple  |   5      \n";
    
	int x,y;
	cout<<"enter your background color:\n";
	cin>>x;
	
	cout<<"enter your text color:\n";
	cin>>y;
	
	if(x==0){
		switch(y){
			case 0 : system("color 00");break;
			case 1 : system("color 01");break;
			case 2 : system("color 02");break;
			case 3 : system("color 03");break;
			case 4 : system("color 04");break;
			case 5 : system("color 05");break;
		}
	}else if(x==1){
		switch(y) {
		
			case 0 : system("color 10");break;
			case 1 : system("color 11");break;
			case 2 : system("color 12");break;
			case 3 : system("color 13");break;
			case 4 : system("color 14");break;
			case 5 : system("color 15");break;
	    }
	}else if(x==2){
		switch(y){
			case 0 : system("color 20");break;
			case 1 : system("color 21");break;
			case 2 : system("color 22");break;
			case 3 : system("color 23");break;
			case 4 : system("color 24");break;
			case 5 : system("color 25");break;
		}
	}else if (x==3){
		switch(y){
			case 0 : system("color 30");break;
			case 1 : system("color 31");break;
			case 2 : system("color 32");break;
			case 3 : system("color 33");break;
			case 4 : system("color 34");break;
			case 5 : system("color 35");break;
		}
	}else if (x==4){
		switch(y){
			case 0 : system("color 40");break;
			case 1 : system("color 41");break;
			case 2 : system("color 42");break;
			case 3 : system("color 43");break;
			case 4 : system("color 44");break;
			case 5 : system("color 45");break;
		}
	}else if(x==5){
		switch(y){
			case 0 : system("color 50");break;
			case 1 : system("color 51");break;
			case 2 : system("color 52");break;
			case 3 : system("color 53");break;
			case 4 : system("color 54");break;
			case 5 : system("color 55");break;
		}
		
	}else
	    cout<<"invalid data.";


}

enum eDirection { STOP = 0, LEFT, RIGHT, UP, DOWN };

class Entity {
public:
    int x, y;

    Entity(int x = 0, int y = 0) : x(x), y(y) {}

    void setPosition(int newX, int newY) {
        x = newX;
        y = newY;
    }

    void randomPosition(int width, int height) {
        x = rand() % width;
        y = rand() % height;
    }
};

class Snake : public Entity {
public:
    int tailX[100], tailY[100];
    int nTail;

    Snake() : nTail(0) {
        setPosition(0, 0);
    }

    void move(eDirection dir, int width, int height) {
        int prevX = tailX[0];
        int prevY = tailY[0];
        int prev2X, prev2Y;
        tailX[0] = x;
        tailY[0] = y;
        for (int i = 1; i < nTail; i++) {
            prev2X = tailX[i];
            prev2Y = tailY[i];
            tailX[i] = prevX;
            tailY[i] = prevY;
            prevX = prev2X;
            prevY = prev2Y;
        }

        switch (dir) {
        case LEFT:
            x--;
            break;
        case RIGHT:
            x++;
            break;
        case UP:
            y--;
            break;
        case DOWN:
            y++;
            break;
        default:
            break;
        }

        if (x >= width) x = 0;
        else if (x < 0) x = width - 1;

        if (y >= height) y = 0;
        else if (y < 0) y = height - 1;
    }

    bool hasCollided() {
        for (int i = 0; i < nTail; i++) {
            if (tailX[i] == x && tailY[i] == y)
                return true;
        }
        return false;
    }

    void grow() {
        nTail++;
        cout<<'\a';
    }
};

class Enemy : public Entity {
public:
    int tailX[100], tailY[100];
    int nTail;

    Enemy() : nTail(0) {
        setPosition(0, 0);
    }

    void moveTowards(int targetX, int targetY) {
        int prevX = tailX[0];
        int prevY = tailY[0];
        int prev2X, prev2Y;
        tailX[0] = x;
        tailY[0] = y;
        for (int i = 1; i < nTail; i++) {
            prev2X = tailX[i];
            prev2Y = tailY[i];
            tailX[i] = prevX;
            tailY[i] = prevY;
            prevX = prev2X;
            prevY = prev2Y;
        }

        if (x < targetX) x++;
        else if (x > targetX) x--;

        if (y < targetY) y++;
        else if (y > targetY) y--;
    }

    void grow() {
        nTail++;
    }
};

class Game {
private:
    bool gameOver;
    int width, height;
    int score;
    bool enemyMove;
    eDirection dir;
    Snake snake;
    Entity fruit;
    vector<Enemy> enemies;
    HANDLE hConsole;

public:
    Game() : hConsole(GetStdHandle(STD_OUTPUT_HANDLE)) {
        setup();
    }

    void setup() {
    	Sleep(300);
    	system("cls");
        gameOver = false;
        dir = STOP;
        score = 0;
        cout << "Enter the width of the game board: ";
        cin >> width;
        cout << "Enter the height of the game board: ";
        cin >> height;

        snake.setPosition(width / 2, height / 2);
        fruit.randomPosition(width, height);

        int numEnemies;
        cout << "Enter the number of enemies: ";
        cin >> numEnemies;
        enemies.resize(numEnemies);
        for (auto &enemy : enemies) {
            enemy.randomPosition(width, height);
        }
    }

    void draw() {
    	Sleep(800);
    	system("cls");
        COORD coord = { 0, 0 };
        SetConsoleCursorPosition(hConsole, coord);

        for (int i = 0; i < width + 2; i++)
            cout << "#";
        cout << endl;

        for (int i = 0; i < height; i++) {
            for (int j = 0; j < width; j++) {
                if (j == 0) cout << "#";
                if (i == snake.y && j == snake.x) cout << "O";
                else if (i == fruit.y && j == fruit.x) cout << "F";
                else {
                    bool isEmpty = true;
                    for (auto &enemy : enemies) {
                        if (i == enemy.y && j == enemy.x) {
                            cout << "E";
                            isEmpty = false;
                            break;
                        }
                        for (int k = 0; k < enemy.nTail; k++) {
                            if (enemy.tailX[k] == j && enemy.tailY[k] == i) {
                                cout << "e";
                                isEmpty = false;
                                break;
                            }
                        }
                        if (!isEmpty) break;
                    }

                    if (isEmpty) {
                        bool printTail = false;
                        for (int k = 0; k < snake.nTail; k++) {
                            if (snake.tailX[k] == j && snake.tailY[k] == i) {
                                cout << "o";
                                printTail = true;
                            }
                        }
                        if (!printTail) cout << " ";
                    }
                }

                if (j == width - 1) cout << "#";
            }
            cout << endl;
        }

        for (int i = 0; i < width + 2; i++)
            cout << "#";
        cout << endl;
        cout << "Score:" << score << endl;
    }

    void input() {
        if (_kbhit()) {
            switch (_getch()) {
            case 'a':
                dir = LEFT;
                break;
            case 'd':
                dir = RIGHT;
                break;
            case 'w':
                dir = UP;
                break;
            case 's':
                dir = DOWN;
                break;
            case 'x':
                gameOver = true;
                break;
            }
        }
    }

    void logic() {
        snake.move(dir, width, height);

        if (snake.hasCollided()) {
            gameOver = true;
            cout<<'\a';
        }

        for (auto &enemy : enemies) {
            if (snake.x == enemy.x && snake.y == enemy.y) {
                gameOver = true;
                cout<<'\a';
                return;
            }
        }

        if (snake.x == fruit.x && snake.y == fruit.y) {
            score += 10;
            fruit.randomPosition(width, height);
            snake.grow();
        }

        for (auto &enemy : enemies) {
            if (enemy.x == fruit.x && enemy.y == fruit.y) {
                fruit.randomPosition(width, height);
                enemy.grow();
            }
        }

        if (enemyMove) {
            for (auto &enemy : enemies) {
                enemy.moveTowards(snake.x, snake.y);
            }
        }

        enemyMove = !enemyMove;
    }

    void run() {
        while (!gameOver) {
            draw();
            input();
            logic();
            Sleep(50);
        }
    }
};
int main()
{
  	int n;

    
	 	while(n!='x'){
	 	
		system("cls");
		menu();
    	cout<<"what is your choise";
        cin>>n;
	 cout<<endl;
        	
		 if(n==1){
		 	
	    Game game;
        game.run();	
			
		}else if(n==2){
			ABOUTUS();
			
		}else if(n==3){
			HELP();
			
		}else if(n==4){
			SETING();	 
	        }
    		
	 	}	
}
