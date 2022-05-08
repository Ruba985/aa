
# a snake game using C++

This program represent the most old and popular game, the snake game which is a simple application of C++ basics.
## table of content 
1. API reference 
2. a summery for the code 
3. used by 
4. the code 
5. programmers 

## API reference 
This program has six functions 'main()' , 'setup()', 'my_pause()', 'Draw()', 'input()', and 'logic()'. 

## a summery for the code
in the main function all other functions have been combined and called. first, it start with setup function
that  set up the score caculater and the size of the game frame. Then, a boolean decision loop decide if the 
turn of the rest functions start or not. In the beggining, the draw function start drawing the boundries and
the front of the game by displaying the score calculatur and the quit game instructor. After that, the input 
function will read the user input from keyboard and pass it to logic function to determine the snake movment
by chang its place coordinatie within the frame and redraw the game front with the new place. All of that happend
during time that less than one second,so we added another function inside logic function to slowdowm the process 
of chnging the snake place. 

## used by 
the game can used by anyone want to have a fun time. just click run and then start taking the fruits by move the
snake using a specific keys from the keyboard in order to increase the score. But without touching the frame to 
not and quit the game. Once the user need to quit the game, there is an option to do that. 

## the code 
// institute : Effat university
// programmers : Albatol, Nada, Amal
// ECE103L - spring 22 , course project
// SNAKE GAME using c++ language
#include <conio.h> // to be able to use kbhit() function
#include <stdio.h>
#include <stdlib.h> // to be able to use rand() function
#include <ctime>
int i, j, height = 20, width = 20;
int gameover, score;
int x, y, fruitx, fruity, flag;

// control the time to slowdown the game
void My_Pause(unsigned secs = 1U)
{
    const int milsecs = 1000;
    clock_t wait = secs * milsecs + clock();
    while ( wait > clock() ) continue;
}

//set the position of the fruit within the boundary
void setup()
{
    // it is not game over
	gameover = 0;

	// centralise the snake body
	x = height / 2;
	y = width / 2;
	// star generating fruits in range of boundary height and width to keep it inside
label1:
	fruitx = rand() % 20;
	if (fruitx == 0)
		goto label1; // generate another number again
label2:
	fruity = rand() % 20;
	if (fruity == 0)
		goto label2; // generate another number again
	score = 0; // initialize score with zero
}

//create the boundary in which the game will be played.
void draw()
{
    // a function from c library that keep basic symbols on its place each time the game is refreshing
    system("cls");
    // draw the boundary and display it
	for (i = 0; i < height; i++) {
		for (j = 0; j < width; j++) {
			if (i == 0 || i == width - 1
				|| j == 0
				|| j == height - 1) {
				printf("#");
			}
			else {
				if (i == x && j == y)
					printf("0"); // display the snake body
				else if (i == fruitx
						&& j == fruity)
					printf("*"); // the fruit symbol
				else
					printf(" ");
			}
		}
		printf("\n");
	}

	// Print the score after the
	// game ends
	printf("score = %d", score);
	printf("\n");
	printf("press X to quit the game");
}

//take the input from the keyboard
void input()
{
	if (kbhit()) // a function that read the input from the keyboard
        {
		switch (getch()) // test the input and set the flag value to control the movement
		 {
		case 'a':
			flag = 1; // go left
			break;
		case 's':
			flag = 2; // go down
			break;
		case 'd':
			flag = 3; // go right
			break;
		case 'w':
			flag = 4; // go up
			break;
		case 'x':
			gameover = 1; // to exist the game
			break;
		}
	}
}

//set the movement of the snake
void logic()
{
    // slowdown the game for 2 seconds
    My_Pause(1);
    // test the number of the flag which was determined by input function
	switch (flag) {

	case 1:
		y--; // go left by
		break;
	case 2:
		x++;
		break;
	case 3:
		y++;
		break;
	case 4:
		x--;
		break;
	default:
		break;
	}

	// If the game is over
	if (x < 0 || x > height
		|| y < 0 || y > width)
		gameover = 1;

	// If snake reaches the fruit
	// then update the score
	if (x == fruitx && y == fruity) {
	label3:
		fruitx = rand() % 20;
		if (fruitx == 0)
			goto label3;

	// After eating the above fruit
	// generate new fruit
	label4:
		fruity = rand() % 20;
		if (fruity == 0)
			goto label4;
		score += 10;
	}
}

// Driver Code
int main()
{
	// Generate boundary
	setup();

	// Until the game is overX
	while (!gameover) {

		// Function Call
		draw();
		input();
		logic();
	}
}

## programmers
* Albato Basalib
* Nada Bajunayd 
* Amal Matar 
