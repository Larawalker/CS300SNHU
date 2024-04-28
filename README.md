# CS300SNHU
Final project for Analysis and Design with C++
Vector
Advantages:
•	Easy to use
•	Provides fast access to elements
Disadvantages:
•	Middle inserting or deleting is more cost
•	Resizing can be costly

Hash Table
Advantages:
•	Provides fast inserting, deleting, and lookup
•	Does not need sorting
Disadvantages:
•	Memory overhead
•	Poor performance if the function is not done properly

Tree
Advantages:
•	Automatically keeps a sorted order
•	Proficiently inserts, deletes and looks up
Disadvantages:
•	More complex
•	High memory overhead

Analysis

Based on analysis, if efficient look-up is what you want then a hash time would be the best choice due to the 0(1) performance. If the order is important to maintain then you would want a binary tree to self-sort, even though it’s a higher worst-case scenario. If memory is a priority then a vector would be a good choice as long as there is not a lot of resizing and shifting.


#include <iostream>
#include <unordered_map>
#include <vector>
#include <string>

using namespace std;

struct Course {
    string title;
    vector<string> prerequisites;
    vector<string> times;
    
};

unordered_map<string, Course> courses;

int numPrerequisiteCourses(string courseNumber) {
    if (courses.find(courseNumber) == courses.end()){
        return 0; // course not found
    }
    int totalPrerequisites = courses[courseNumber].prerequisites.size();
    for (const auto& prerequisite : courses[courseNumber].prerequisites) {
        totalPrerequisites += numPrerequisiteCourses(prerequisite);
    }
    return totalPrerequisites;
}

void printSampleSchedule(string courseNumber) {
    if (courses.find(courseNumber) == courses.end()) {
        cout << "Course not found!" << endl;
        return;
    }
    cout << "Times for Course " << courseNumber << ": ";
    for (const auto& time : courses[courseNumber].times) {
        cout << time << " ";
    }
    cout << endl;
}

void printCourseInformation(string courseNumber) {
    if (courses.find(courseNumber) == courses.end()) {
        cout << "Course not found!" << endl;
        return;
    }
    cout << "Course Information for " << courseNumber << ": " << courses[courseNumber].title << endl;
    cout << "Prerequisites: ";
    for (const auto& prerequisite : courses[courseNumber].prerequisites) {
        cout << prerequisite << " ";
    }
    cout << endl;
}

int main() {
    //populate table with course info
    courses["MATH201"] = {"Discrete Mathematics", {}, {}};
    courses["CSCI300"] = {"Introduction to Algorithms", {"MATH201"}, {"Monday 10:00 AM"}};
    courses["CSCI350"] = {"Operating Systems", {"CSCI300"}, {}};
    courses["CSCI101"] = {"Introduction to Programming in C++", {"CSCI100"}, {}};
    courses["CSCI100"] = {"Introduction to Computer Science", {}, {}};
    courses["CSCI301"] = {"Advanced Programming in C++", {"CSCI101"}, {}};
    courses["CSCI400"] = {"Large Software Development", {"CSCI301"}, {"CSCI350"}};
    courses["CSCI200"] = {"Data Structures", {"CSCI101"}, {}};
}
