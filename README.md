# cpp-obscure-heroes
#include <iostream>
#include <string>
#include <algorithm>
#include <cctype>

using namespace std;

const int HERO_COUNT = 10;

// Parallel arrays
string names[HERO_COUNT] = {
    "Squirrel Girl", "Arm-Fall-Off-Boy", "The Tick", "Matter-Eater Lad",
    "Bouncing Boy", "Doorman", "Zeitgeist", "Madame Fatal",
    "Ragman", "Dogwelder"
};

string powers[HERO_COUNT] = {
    "Control Squirrels", "Detachable Limbs", "Super Strength", "Eat Anything",
    "Bounce", "Teleportation", "Acid Vomit", "Disguise",
    "Soul Absorption", "Weld Dogs to People"
};

string weaknesses[HERO_COUNT] = {
    "Time Limits", "Heavy Objects", "Poor Judgment", "Stomach Limits",
    "Sharp Objects", "Doors Only", "Short Duration", "Old Age",
    "Guilt", "Dog Supply"
};

// Multidimensional array: Year and Universe
string info[HERO_COUNT][2] = {
    {"1992", "Marvel"}, {"1989", "DC"}, {"1986", "Other"},
    {"1962", "DC"}, {"1961", "DC"}, {"1989", "Marvel"},
    {"2001", "Marvel"}, {"1940", "Other"}, {"1976", "DC"}, {"1996", "DC"}
};

// Function declarations
void showMenu();
void searchByName();
void findByPower();
void sortHeroes();
void displayCase(bool toUpper);
string toCase(string s, bool upper);
void displayAll();

int main() {
    int choice;
    do {
        showMenu();
        cin >> choice;
        cin.ignore(); // Clear newline buffer
        switch (choice) {
            case 1: searchByName(); break;
            case 2: findByPower(); break;
            case 3: sortHeroes(); break;
            case 4: displayCase(true); break;
            case 5: displayCase(false); break;
            case 6: cout << "Goodbye!\n"; break;
            default: cout << "Invalid choice.\n";
        }
    } while (choice != 6);

    return 0;
}

// Menu
void showMenu() {
    cout << "\nObscure Superhero Database\n";
    cout << "1. Search by Name\n";
    cout << "2. Find by Superpower\n";
    cout << "3. Sort Alphabetically\n";
    cout << "4. Display ALL (UPPERCASE)\n";
    cout << "5. Display ALL (lowercase)\n";
    cout << "6. Exit\n";
    cout << "Enter your choice: ";
}

// Case-insensitive string comparison
bool caseInsensitiveMatch(string a, string b) {
    transform(a.begin(), a.end(), a.begin(), ::tolower);
    transform(b.begin(), b.end(), b.begin(), ::tolower);
    return a.find(b) != string::npos;
}

// Search by Name
void searchByName() {
    string query;
    cout << "Enter name to search: ";
    getline(cin, query);

    for (int i = 0; i < HERO_COUNT; ++i) {
        if (caseInsensitiveMatch(names[i], query)) {
            cout << "\n" << names[i] << " | " << powers[i] << " | " << weaknesses[i]
                 << " | " << info[i][0] << " | " << info[i][1] << endl;
        }
    }
}

// Find by Superpower
void findByPower() {
    string query;
    cout << "Enter power to search: ";
    getline(cin, query);

    for (int i = 0; i < HERO_COUNT; ++i) {
        if (caseInsensitiveMatch(powers[i], query)) {
            cout << "\n" << names[i] << " | " << powers[i] << " | " << weaknesses[i]
                 << " | " << info[i][0] << " | " << info[i][1] << endl;
        }
    }
}

// Alphabetical sort
void sortHeroes() {
    for (int i = 0; i < HERO_COUNT - 1; ++i) {
        for (int j = i + 1; j < HERO_COUNT; ++j) {
            if (names[i] > names[j]) {
                swap(names[i], names[j]);
                swap(powers[i], powers[j]);
                swap(weaknesses[i], weaknesses[j]);
                swap(info[i][0], info[j][0]);
                swap(info[i][1], info[j][1]);
            }
        }
    }
    cout << "Heroes sorted alphabetically.\n";
    displayAll();
}

// Case display function
void displayCase(bool toUpper) {
    for (int i = 0; i < HERO_COUNT; ++i) {
        cout << toCase(names[i], toUpper) << " | "
             << toCase(powers[i], toUpper) << " | "
             << toCase(weaknesses[i], toUpper) << " | "
             << info[i][0] << " | " << toCase(info[i][1], toUpper) << "\n";
    }
}

// Helper: Change case
string toCase(string s, bool upper) {
    for (char& c : s)
        c = upper ? toupper(c) : tolower(c);
    return s;
}

// Display all
void displayAll() {
    for (int i = 0; i < HERO_COUNT; ++i) {
        cout << names[i] << " | " << powers[i] << " | " << weaknesses[i]
             << " | " << info[i][0] << " | " << info[i][1] << endl;
    }
}
