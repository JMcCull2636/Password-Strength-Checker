#include <iostream>
#include <string>
#include <cctype>

using namespace std;

class Password {
private:
    string text;

public:
    Password(string t) {
        text = t;
    }

    string getText() const { 
        return text;
    }
};

class Validator {
public:
    bool hasNumber(const string &s) const { 
        for (char c : s) {
            if (isdigit(c)) return true;
        }
        return false;
    }
    bool hasUpper(const string &s) const { 
        for (char c : s) {
            if (isupper(c)) return true;
        }
        return false;
    }

    bool hasLower(const string &s) const { 
        for (char c : s) {
            if (islower(c)) return true;
        }
        return false;
    }

    bool hasSymbol(const string &s) const { 
        string symbols = "!@#$%^&*()-_=+[]{};:'\",.<>?/\\|`~";
        for (char c : s) {
            if (symbols.find(c) != string::npos) return true;
        }
        return false;
    }

    string checkStrength(const string &s) const { 
        int score = 0;

        if (s.length() >= 8) score++;
        if (hasNumber(s)) score++;
        if (hasUpper(s)) score++;
        if (hasLower(s)) score++;
        if (hasSymbol(s)) score++;

        if (score <= 2)
            return "Weak";
        else if (score == 3 || score == 4)
            return "Medium";
        else
            return "Strong";
    }
};

int main() {
    string input;
    cout << "Enter a password: ";
    getline(cin, input);

    Password p(input);
    Validator v;

    string strength = v.checkStrength(p.getText());

    cout << "Password Strength: " << strength << endl; 

    return 0;
}


    
