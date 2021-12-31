// Conways game of life

#include <vector>
#include <stdexcept>
#include <cmath>

#include <iostream>
#include <fstream>
#include <string>

#include <sstream>

using namespace std;

// board (1s=alive, 0s=dead)
vector<vector<int>> board;
// temp board for updating
vector<vector<int>> temp_board;
// rows and columns of board
int rows;
int columns;

void initialize_board() {
    // Initializes the board based on a text file filed with 1s and 0s found in directory

    // txt -> string
    ifstream file("inital_state.txt");
    auto s = ostringstream{};
    s << file.rdbuf();
    string b = s.str();

    // string -> vector<vector<int>>
    stringstream bb(b);
    string val;
    while(getline(bb, val, '\n')) {
        
        vector<int> temp_row;
        for (int i = 0; i < val.length(); i++)
        {
            if (val[i] == '0'){temp_row.push_back(0);}
            else if (val[i] == '1'){temp_row.push_back(1);}
        }
        board.push_back(temp_row);
        temp_board.push_back(temp_row); // initializing temporary board here as well used for updating
    }

    // passing to global variables
    rows = board.size();
    columns = board[0].size();
}

void show_board() {
    // print board to terminal
    
    for (int i = 0; i < rows; i++)
    {
        for (int j = 0; j < columns; j++)
        {
            cout << board[i][j] << "";
        }       
        cout << endl;
    }
    for (int i = 0; i < columns; i++)
    {
        cout << "-";
    }
    cout << endl;
}

void update_board() {
    // looping through board and checking neighbors to apply rules to dead and alive cells

    for (int i = 0; i < rows; i++)
    {
        for (int j = 0; j < columns; j++)
        {
            int sum = 0; // number of alive nieghbors
            for (int x = -1; x <= 1; x++)
            {
                for (int y = -1; y <= 1; y++)
                {
                    try
                    {
                        if(x == 0 && y == 0) {continue;} // current cell
                        if(board.at(i+x).at(j+y) == 1) {++sum;}
                    }
                    catch(out_of_range)
                    {
                        continue;
                    }
                }
            }
            int current = board.at(i).at(j);

            if (sum == 3){
                temp_board.at(i).at(j) = 1;
            }
            else{
                if (current == 1 && sum == 2) {
                    temp_board.at(i).at(j) = 1;
                }
                else{temp_board.at(i).at(j) = 0;}
            }
        }
    }
    // temp_board updated, assigned to board
    board = temp_board;
}

int main() 
{
    cout << "Inital board from directory:" << endl;
    initialize_board();
    show_board();

    cout << endl << "Press enter to update board:";    
    string update_var;
    getline(cin, update_var);

    int i = 0;
    while(update_var.empty()) { // update loop
        cout << "Iteration: " << i << endl;
        i++;
        update_board();
        show_board();
        getline(cin, update_var);
    }

    return 0;
}
