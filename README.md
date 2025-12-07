# student-study-planner
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main() {
    int numSessions;  // Number of study sessions to log
    char subject[50];  // Subject name (e.g., maths, physics)
    float hours;  // Hours studied in that session (now float for decimals)
    float totalHours = 0.0;  // Total study hours (now float)
    float mathsHours = 0.0, physicsHours = 0.0, ltpsHours = 0.0, biologyHours = 0.0;  // Hours per subject (now float)
    float targetMaths = 0.0, targetPhysics = 0.0, targetLtps = 0.0, targetBiology = 0.0;  // Target hours per subject
    float totalTarget = 0.0;

    // Welcome and ask for number of sessions
    printf("Welcome to the Student Study Planner!\n");
    printf("How many study sessions do you want to log? ");
    scanf("%d", &numSessions);

    if (numSessions <= 0) {
        printf("No sessions? Planning canceled!\n");
        return 0;
    }

    // Loop through each session
    for (int i = 1; i <= numSessions; i++) {
        printf("\nSession %d:\n", i);
        
        // Ask for subject
        printf("What subject did you study? (maths, physics, ltps, or biology): ");
        scanf("%s", subject);
        
        // Convert subject to lowercase for case-insensitive comparison
        for (int j = 0; subject[j]; j++) {
            subject[j] = tolower(subject[j]);
        }
        
        // Ask for hours
        printf("How many hours did you study? (1-10): ");
        while (1) {
            scanf("%f", &hours);  // Changed to %f for float input
            if (hours >= 1.0 && hours <= 10.0) {
                totalHours += hours;
                // Tally by subject (now case-insensitive)
                if (strcmp(subject, "maths") == 0) mathsHours += hours;
                else if (strcmp(subject, "physics") == 0) physicsHours += hours;
                else if (strcmp(subject, "ltps") == 0) ltpsHours += hours;
                else biologyHours += hours;
                break;
            } else {
                printf("Please enter 1 to 10 hours: ");
            }
        }
    }

    // Ask for target hours per subject
    printf("\nNow, set your study goals!\n");
    printf("Target hours for maths: ");
    scanf("%f", &targetMaths);
    printf("Target hours for physics: ");
    scanf("%f", &targetPhysics);
    printf("Target hours for ltps: ");
    scanf("%f", &targetLtps);
    printf("Target hours for biology: ");
    scanf("%f", &targetBiology);
    totalTarget = targetMaths + targetPhysics + targetLtps + targetBiology;

    // Display results
    printf("\n--- Study Planner Results ---\n");
    printf("Total sessions logged: %d\n", numSessions);
    printf("Total study hours: %.1f\n", totalHours);  // Changed to %.1f for one decimal place
    printf("Average hours per session: %.1f\n", totalHours / numSessions);
    printf("Hours by subject:\n");
    if (totalHours > 0.0) {
        printf("- maths: %.1f hours (%.1f%%)\n", mathsHours, mathsHours / totalHours * 100);
        printf("- physics: %.1f hours (%.1f%%)\n", physicsHours, physicsHours / totalHours * 100);
        printf("- ltps: %.1f hours (%.1f%%)\n", ltpsHours, ltpsHours / totalHours * 100);
        printf("- biology: %.1f hours (%.1f%%)\n", biologyHours, biologyHours / totalHours * 100);
    } else {
        printf("- maths: %.1f hours\n", mathsHours);
        printf("- physics: %.1f hours\n", physicsHours);
        printf("- ltps: %.1f hours\n", ltpsHours);
        printf("- biology: %.1f hours\n", biologyHours);
    }
    
    // Goal comparison
    printf("\n--- Goal Comparison ---\n");
    printf("Total target hours: %.1f\n", totalTarget);
    printf("Progress towards goals:\n");
    printf("- maths: %.1f / %.1f (%.1f%%)\n", mathsHours, targetMaths, targetMaths > 0 ? mathsHours / targetMaths * 100 : 0);
    printf("- physics: %.1f / %.1f (%.1f%%)\n", physicsHours, targetPhysics, targetPhysics > 0 ? physicsHours / targetPhysics * 100 : 0);
    printf("- ltps: %.1f / %.1f (%.1f%%)\n", ltpsHours, targetLtps, targetLtps > 0 ? ltpsHours / targetLtps * 100 : 0);
    printf("- biology: %.1f / %.1f (%.1f%%)\n", biologyHours, targetBiology, targetBiology > 0 ? biologyHours / targetBiology * 100 : 0);
    
    // Suggestions
    printf("\nSuggestions:\n");
    if (totalHours < totalTarget) {
        printf("- You're behind on total hours. Aim to study %.1f more hours overall.\n", totalTarget - totalHours);
    } else {
        printf("- Great job meeting or exceeding total hours!\n");
    }
    if (mathsHours < targetMaths) {
        printf("- Maths: Need %.1f more hours to reach your goal.\n", targetMaths - mathsHours);
    }
    if (physicsHours < targetPhysics) {
        printf("- Physics: Need %.1f more hours to reach your goal.\n", targetPhysics - physicsHours);
    }
    if (ltpsHours < targetLtps) {
        printf("- Ltps: Need %.1f more hours to reach your goal.\n", targetLtps - ltpsHours);
    }
    if (biologyHours < targetBiology) {
        printf("- Biology: Need %.1f more hours to reach your goal.\n", targetBiology - biologyHours);
    }
    // Find subject with least progress
    float minProgress = 1.0;
    char minSubject[50] = "";
    if (targetMaths > 0 && mathsHours / targetMaths < minProgress) {
        minProgress = mathsHours / targetMaths;
        strcpy(minSubject, "maths");
    }
    if (targetPhysics > 0 && physicsHours / targetPhysics < minProgress) {
        minProgress = physicsHours / targetPhysics;
        strcpy(minSubject, "physics");
    }
    if (targetLtps > 0 && ltpsHours / targetLtps < minProgress) {
        minProgress = ltpsHours / targetLtps;
        strcpy(minSubject, "ltps");
    }
    if (targetBiology > 0 && biologyHours / targetBiology < minProgress) {
        minProgress = biologyHours / targetBiology;
        strcpy(minSubject, "biology");
    }
    if (strcmp(minSubject, "") != 0) {
        printf("- Prioritize %s as it has the lowest progress towards your goal.\n", minSubject);
    }
    printf("Keep studying hard!\n");

    return 0;
}
