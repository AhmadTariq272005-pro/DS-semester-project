#include <iostream>
#include <stack>
#include <queue>
#include <string>
using namespace std;

// ---------------- LINKED LIST FOR TEXT ----------------
struct Node {
    string word;
    Node* next;
    Node(string w) : word(w), next(NULL) {}
};

Node* head = NULL;

// ---------------- LINKED LIST FUNCTIONS ----------------

// Insert word at end
void insertWord(string w) {
    Node* newNode = new Node(w);
    if (!head) {
        head = newNode;
        return;
    }
    Node* temp = head;
    while (temp->next) temp = temp->next;
    temp->next = newNode;
}

// Insert at position
void insertAtPosition(string w, int position) {
    Node* newNode = new Node(w);

    if (position == 1) {
        newNode->next = head;
        head = newNode;
        return;
    }

    Node* temp = head;
    for (int i = 1; temp && i < position - 1; i++)
        temp = temp->next;

    if (!temp) {
        cout << "Invalid position.\n";
        return;
    }

    newNode->next = temp->next;
    temp->next = newNode;
}

// Delete last word (for undo)
string deleteLastWord() {
    if (!head) return "";
    if (!head->next) {
        string w = head->word;
        delete head;
        head = NULL;
        return w;
    }
    Node* temp = head;
    while (temp->next->next) temp = temp->next;
    string w = temp->next->word;
    delete temp->next;
    temp->next = NULL;
    return w;
}

// Delete at specific position
void deleteAtPosition(int position) {
    if (!head) {
        cout << "Empty text.\n";
        return;
    }

    if (position == 1) {
        Node* del = head;
        head = head->next;
        delete del;
        return;
    }

    Node* temp = head;
    for (int i = 1; temp && i < position - 1; i++)
        temp = temp->next;

    if (!temp || !temp->next) {
        cout << "Invalid position.\n";
        return;
    }

    Node* del = temp->next;
    temp->next = temp->next->next;
    delete del;
}

// Edit by position
void editWordAtPosition(int pos, string newWord) {
    Node* temp = head;
    for (int i = 1; temp && i < pos; i++)
        temp = temp->next;

    if (!temp) {
        cout << "Invalid position.\n";
        return;
    }

    temp->word = newWord;
}

// Replace words
void replaceWord(string oldW, string newW) {
    Node* temp = head;
    bool ok = false;
    while (temp) {
        if (temp->word == oldW) {
            temp->word = newW;
            ok = true;
        }
        temp = temp->next;
    }
    if (!ok) cout << "Word not found.\n";
}

// Word stats
void showWordStats() {
    if (!head) {
        cout << "No words.\n";
        return;
    }

    int count = 0;
    string longest = head->word;
    string shortest = head->word;
    float totalLength = 0;

    Node* temp = head;
    while (temp) {
        int len = temp->word.length();
        totalLength += len;
        count++;

        if (len > longest.length()) longest = temp->word;
        if (len < shortest.length()) shortest = temp->word;

        temp = temp->next;
    }

    cout << "\n--- Word Statistics ---\n";
    cout << "Total Words: " << count << endl;
    cout << "Longest Word: " << longest << endl;
    cout << "Shortest Word: " << shortest << endl;
    cout << "Average Word Length: " << totalLength / count << endl;
    cout << "------------------------\n";
}

// ---------------- STACK FOR UNDO & REDO ----------------
stack<string> undoStack;
stack<string> redoStack;

// ---------------- QUEUE FOR HISTORY & WORD PROCESSING ----------------
queue<string> history;

// Convert Linked List ? Queue (FIFO text display)
queue<string> convertToQueue() {
    queue<string> q;
    Node* temp = head;
    while (temp) {
        q.push(temp->word);
        temp = temp->next;
    }
    return q;
}

// Delete FIRST word using Queue FIFO style
void deleteFirstWordUsingQueue() {
    if (!head) {
        cout << "Text empty.\n";
        return;
    }

    Node* del = head;
    head = head->next;
    delete del;

    cout << "First word deleted using Queue.\n";
}

// Display using Queue
void displayTextUsingQueue() {
    queue<string> q = convertToQueue();

    if (q.empty()) {
        cout << "(empty)\n";
        return;
    }

    cout << "\n--- Display (Queue FIFO) ---\n";
    while (!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }
    cout << "\n----------------------------\n";
}

// ---------------- MAIN ----------------
int main() {
    int choice, pos;
    string word, newWord, oldWord;

    while (true) {
        cout << "\n=== TEXT EDITOR MENU ===\n";
        cout << "1. Insert Word (LL)\n";
        cout << "2. Display Text (Queue FIFO)\n";
        cout << "3. Undo (Stack)\n";
        cout << "4. Redo (Stack)\n";
        cout << "5. Show Edit History (Queue)\n";
        cout << "6. Insert at Position (LL)\n";
        cout << "7. Delete at Position (LL)\n";
        cout << "8. Edit Word at Position (LL)\n";
        cout << "9. Replace Word (LL)\n";
        cout << "10. Delete FIRST Word (Queue)\n";
        cout << "11. Word Statistics (LL)\n";
        cout << "12. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {

        case 1:
            cout << "Enter word: ";
            cin >> word;
            insertWord(word);
            undoStack.push(word);
            history.push("Inserted: " + word);
            while (!redoStack.empty()) redoStack.pop();
            break;

        case 2:
            displayTextUsingQueue();
            break;

        case 3:
            if (!undoStack.empty()) {
                word = undoStack.top();
                undoStack.pop();
                deleteLastWord();
                redoStack.push(word);
                history.push("Undo: " + word);
                cout << "Undo successful.\n";
            } else {
                cout << "Nothing to undo.\n";
            }
            break;

        case 4:
            if (!redoStack.empty()) {
                word = redoStack.top();
                redoStack.pop();
                insertWord(word);
                undoStack.push(word);
                history.push("Redo: " + word);
                cout << "Redo successful.\n";
            } else {
                cout << "Nothing to redo.\n";
            }
            break;

        case 5:
            cout << "\n--- Edit History ---\n";
            if (history.empty()) cout << "(no history)\n";
            else {
                queue<string> temp = history;
                while (!temp.empty()) {
                    cout << temp.front() << endl;
                    temp.pop();
                }
            }
            cout << "---------------------\n";
            break;

        case 6:
            cout << "Enter word: ";
            cin >> word;
            cout << "Enter position: ";
            cin >> pos;
            insertAtPosition(word, pos);
            break;

        case 7:
            cout << "Enter position to delete: ";
            cin >> pos;
            deleteAtPosition(pos);
            break;

        case 8:
            cout << "Enter position: ";
            cin >> pos;
            cout << "Enter new word: ";
            cin >> newWord;
            editWordAtPosition(pos, newWord);
            break;

        case 9:
            cout << "Enter old word: ";
            cin >> oldWord;
            cout << "Enter new word: ";
            cin >> newWord;
            replaceWord(oldWord, newWord);
            break;

        case 10:
            deleteFirstWordUsingQueue();
            break;

        case 11:
            showWordStats();
            break;

        case 12:
            cout << "Exiting... Goodbye!\n";
            return 0;

        default:
            cout << "Invalid choice. Try again.\n";
        }
    }
}
