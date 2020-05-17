# plurality
tested good but errors in the checking
#include <cs50.h>
#include <stdio.h>
#include <string.h>

// Max number of candidates
#define MAX 9

// Candidates have name and vote count
typedef struct
{
    string name;
    int votes;
}
candidate;

// Array of candidates
candidate candidates[MAX];

// Number of candidates
int candidate_count;

// Function prototypes
bool vote(string name);
void print_winner(void);

int main(int argc, string argv[])
{
    // Check for invalid usage
    if (argc < 2)
    {
        printf("Usage: plurality [candidate ...]\n");
        return 1;
    }

    // Populate array of candidates
    candidate_count = argc - 1;
    if (candidate_count > MAX)
    {
        printf("Maximum number of candidates is %i\n", MAX);
        return 2;
    }
    for (int i = 0; i < candidate_count; i++)
    {
        candidates[i].name = argv[i + 1];
        candidates[i].votes = 0;
    }

    int voter_count = get_int("Number of voters: ");

    // Loop over all voters
    for (int i = 0; i < voter_count; i++)
    {
        string name = get_string("Vote: ");

        // Check for invalid vote
        if (!vote(name))
        {
            printf("Invalid vote.\n");
        }
    }

    // Display winner of election
    print_winner();
}

// Update vote totals given a new vote
bool vote(string name)
{
    // to do
    for (int j = 0; j < candidate_count; j++)
    {
        if (strcmp(name,candidates[j].name) == 0 )
        {
            candidates[j].votes++;
            return true;
        }
    }
    return false;

}

// Print the winner (or winners) of the election
void print_winner(void)
{
    // to do
    int x;
    string y;
    for(int j = 0; j < candidate_count; j++)
    {
        int min=j;
        for (int i = j+1; i < candidate_count; i++)
        {
            if (candidates[i].votes < candidates[min].votes)
            {
                min = i;
            }
            if (min != j)
            {
                x = candidates[j].votes;
                candidates[j].votes = candidates[min].votes;
                candidates[min].votes = x;

                y = candidates[j].name;
                candidates[j].name = candidates[min].name;
                candidates[min].name = y;
            }
        }
    }
    printf("%s \n",candidates[candidate_count-1].name );

    for (int i = candidate_count-1; i > 0; i--)
    {
        if (candidates[i].votes == candidates[i-1].votes)
        {
            printf("%s \n",candidates[i-1].name );
        }
    }

    return;
}
