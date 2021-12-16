#include <iostream>
using namespace std;

void countVaraibles(string prgm){
    int Integer, Char, Bool, Float, Double, String;
    Integer = Char = Bool = Float = Double = String = 0;
    int n = prgm.length();

    for (int i = 0; i < n; i++){
        if (i + 3 <= n && prgm.substr(i, 3) == "int"){
            Integer++;
            while (i < n && prgm[i] != '\n'){
                if (prgm[i] == ',') Integer++;
                i++;
            }
        }
        else if (i + 4 <= n && prgm.substr(i, 4) == "char"){
            Char++;
            while (i < n && prgm[i] != '\n'){
                if (prgm[i] == ',') Char++;
                i++;
            }
        }
        else if (i + 4 <= n && prgm.substr(i, 4) == "bool"){
            Bool++;
            while (i < n && prgm[i] != '\n'){
                if (prgm[i] == ',') Bool++;
                i++;
            }
        }
        else if (i + 5 <= n && prgm.substr(i, 5) == "float"){
            Float++;
            while (i < n && prgm[i] != '\n'){
                if (prgm[i] == ',') Float++;
                i++;
            }
        }
        else if (i + 6 <= n && prgm.substr(i, 6) == "double"){
            Double++;
            while (i < n && prgm[i] != '\n'){
                if (prgm[i] == ',') Double++;
                i++;
            }
        }
        else if (i + 6 <= n && prgm.substr(i, 6) == "string"){
            String++;
            while (i < n && prgm[i] != '\n'){
                if (prgm[i] == ',') String++;
                i++;
            }
        }
    }
    cout << "Counting Number of Variables:" << endl;
    cout << "Integers: " << Integer << endl;
    cout << "Characters: " << Char << endl;
    cout << "Booleans: " << Bool << endl;
    cout << "Floats: " << Float << endl;
    cout << "Doubles: " << Double << endl;
    cout << "Strings: " << String << endl;
}

string removeComments(string prgm)
{
    int n = prgm.length();
    string res;
    bool singleComment = false;
    bool multiComment = false;
    for (int i = 0; i < n; i++)
    {
        if (prgm[i] == '/' && prgm[i+1] == '/')
            singleComment = true, i++;
        else if (prgm[i] == '/' && prgm[i+1] == '*')
            multiComment = true,  i++;
        else if (singleComment == true && prgm[i] == '\n')
            singleComment = false;
        else if  (multiComment == true && prgm[i] == '*' && prgm[i+1] == '/')
            multiComment = false,  i++;
        else if (singleComment || multiComment)
            continue;
        else  res += prgm[i];
    }
    return res;
}


string removeSpaces(string prgm){
    int n = prgm.length();
    string res;
    bool spaceFound = true;
    for (int i = 0; i < n; i++){
        if (spaceFound && prgm[i] == ' ')
            continue;
        if (prgm[i] == ' ')
            spaceFound = true;
        else if (prgm[i] != ' ')
            spaceFound = false;
        res += prgm[i];
    }
    return res;
}

int main()
{
    string prgm;
    string new_prgm;
    getline(std::cin,prgm,'^');
    cout << " Modified Program \n";
    new_prgm = removeComments(prgm);
    new_prgm = removeSpaces(new_prgm);
    cout << new_prgm;
    cout << "\n-------------------\n";
    countVaraibles(new_prgm);
    return 0;
}

/*
//input example /n
 int n = prgm.length();
    int i = 0, j = -1, k = 40;
    bool spaceFound = false;
    while (++j < n && prgm[j] == ' ');
    while     (j < n)
    float a, b, c, d;
    string a;
    double x, y;
    char p, q, r, s, t, f, z;
        */
