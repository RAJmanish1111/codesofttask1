# codesofttask1
This project is about game.
#include <iostream>
#include <vector>
#include <string>

using namespace std;

void initializeBoard(vector<vector<char>> &board);
void displayBoard(const vector<vector<char>> &board);
bool checkWin(const vector<vector<char>> &board, char player);
bool checkDraw(const vector<vector<char>> &board);
void switchPlayer(char &currentPlayer);

int main()
{
    vector<vector<char>> board(3, vector<char>(3, ' '));
    char currentPlayer = 'X';
    bool gameOver = false;

    cout << "Welcome to Tic-Tac-Toe!\n\n";

    do
    {
        initializeBoard(board);

        while (!gameOver)
        {
            displayBoard(board);
            cout << "Player " << currentPlayer << ", enter your move (row column): ";
            int row, col;
            cin >> row >> col;

            if (row < 0 || row >= 3 || col < 0 || col >= 3 || board[row][col] != ' ')
            {
                cout << "Invalid move. Try again.\n";
                continue;
            }

            board[row][col] = currentPlayer;

            if (checkWin(board, currentPlayer))
            {
                displayBoard(board);
                cout << "Player " << currentPlayer << " wins!\n";
                gameOver = true;
            }
            else if (checkDraw(board))
            {
                displayBoard(board);
                cout << "It's a draw!\n";
                gameOver = true;
            }

            switchPlayer(currentPlayer);
        }

        cout << "Do you want to play again? (y/n): ";
        char playAgain;
        cin >> playAgain;

        if (playAgain != 'y' && playAgain != 'Y')
        {
            break;
        }

        gameOver = false;
    } while (true);

    cout << "Thanks for playing!\n";

    return 0;
}

void initializeBoard(vector<vector<char>> &board)
{
    for (int i = 0; i < 3; ++i)
    {
        for (int j = 0; j < 3; ++j)
        {
            board[i][j] = ' ';
        }
    }
}

void displayBoard(const vector<vector<char>> &board)
{
    cout << "\n  0 1 2\n";
    for (int i = 0; i < 3; ++i)
    {
        cout << i << " ";
        for (int j = 0; j < 3; ++j)
        {
            cout << board[i][j];
            if (j < 2)
            {
                cout << "|";
            }
        }
        cout << "\n";
        if (i < 2)
        {
            cout << "  -----\n";
        }
    }
    cout << "\n";
}

bool checkWin(const vector<vector<char>> &board, char player)
{
    for (int i = 0; i < 3; ++i)
    {
        if (board[i][0] == player && board[i][1] == player && board[i][2] == player)
        {
            return true;
        }
        if (board[0][i] == player && board[1][i] == player && board[2][i] == player)
        {
            return true;
        }
    }
    if (board[0][0] == player && board[1][1] == player && board[2][2] == player)
    {
        return true;
    }
    if (board[0][2] == player && board[1][1] == player && board[2][0] == player)
    {
        return true;
    }
    return false;
}

bool checkDraw(const vector<vector<char>> &board)
{
    for (int i = 0; i < 3; ++i)
    {
        for (int j = 0; j < 3; ++j)
        {
            if (board[i][j] == ' ')
            {
                return false;
            }
        }
    }
    return true;
}

void switchPlayer(char &currentPlayer)
{
    if (currentPlayer == 'X')
    {
        currentPlayer = 'O';
    }
    else
    {
        currentPlayer = 'X';
    }
}
