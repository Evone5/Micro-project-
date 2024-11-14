# Micro-project-
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

#define MAX_ENTRIES 100
#define MAX_ENTRY_LENGTH 1000

typedef struct {
    char content[MAX_ENTRY_LENGTH];
    char timestamp[20];
} JournalEntry;

JournalEntry diary[MAX_ENTRIES];
int entryCount = 0;

void addEntry() {
    if (entryCount >= MAX_ENTRIES) {
        printf("Diary is full. Cannot add more entries.\n");
        return;
    }

    printf("Enter your journal entry:\n");
    scanf(" %[^\n]", diary[entryCount].content);

    time_t now = time(NULL);
    strftime(diary[entryCount].timestamp, 20, "%Y-%m-%d %H:%M:%S", localtime(&now));

    entryCount++;
    printf("Entry added successfully.\n");
}

void viewEntries() {
    if (entryCount == 0) {
        printf("No entries in the diary.\n");
        return;
    }

    for (int i = 0; i < entryCount; i++) {
        printf("\nEntry %d:\n", i + 1);
        printf("Timestamp: %s\n", diary[i].timestamp);
        printf("Content: %s\n", diary[i].content);
    }
}

void editEntry() {
    int index;
    printf("Enter the entry number you want to edit (1-%d): ", entryCount);
    scanf("%d", &index);

    if (index < 1 || index > entryCount) {
        printf("Invalid entry number.\n");
        return;
    }

    printf("Current entry:\n%s\n", diary[index - 1].content);
    printf("Enter the new content:\n");
    scanf(" %[^\n]", diary[index - 1].content);

    time_t now = time(NULL);
    strftime(diary[index - 1].timestamp, 20, "%Y-%m-%d %H:%M:%S", localtime(&now));

    printf("Entry updated successfully.\n");
}

void deleteEntry() {
    int index;
    printf("Enter the entry number you want to delete (1-%d): ", entryCount);
    scanf("%d", &index);

    if (index < 1 || index > entryCount) {
        printf("Invalid entry number.\n");
        return;
    }

    for (int i = index - 1; i < entryCount - 1; i++) {
        strcpy(diary[i].content, diary[i + 1].content);
        strcpy(diary[i].timestamp, diary[i + 1].timestamp);
    }

    entryCount--;
    printf("Entry deleted successfully.\n");
}

int main() {
    int choice;

    while (1) {
        printf("\nDigital Diary Menu:\n");
        printf("1. Add Entry\n");
        printf("2. View Entries\n");
        printf("3. Edit Entry\n");
        printf("4. Delete Entry\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                addEntry();
                break;
            case 2:
                viewEntries();
                break;
            case 3:
                editEntry();
                break;
            case 4:
                deleteEntry();
                break;
            case 5:
                printf("Thank you for using the digital diary. Goodbye!\n");
                exit(0);
            default:
                printf("Invalid choice. Please try again.\n");
        }
    }

    return 0;
} 
