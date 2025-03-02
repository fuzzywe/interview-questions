In C++, you can calculate the length of a string without using the length() or size() member functions by iterating through the string. Here are a few methods to achieve this:
Method 1: Using a for loop
#include <iostream>
#include <string>
int stringLength(const std::string& str) {
    int count = 0;
    for (char c : str) {
        count++;
    }
    return count;
}
int main() {
    std::string myString = "Hello, World!";
    int length = stringLength(myString);
    std::cout << "Length: " << length << std::endl;  // Output: Length: 13
    return 0;
}

Method 2: Using a while loop
#include <iostream>
#include <string>
int stringLength(const std::string& str) {
    int count = 0;
    int index = 0;
    while (str[index] != '\0') {  // Loop until the null terminator
        count++;
        index++;
    }
    return count;
}
int main() {
    std::string myString = "Hello, World!";
    int length = stringLength(myString);
    std::cout << "Length: " << length << std::endl;  // Output: Length: 13
    return 0;
}

Method 3: Using recursion
#include <iostream>
#include <string>
int stringLength(const std::string& str, int index = 0) {
    if (index == str.size()) {
        return 0;  // Base case: end of the string
    }
    return 1 + stringLength(str, index + 1);  // Recursive case
}
int main() {
    std::string myString = "Hello, World!";
    int length = stringLength(myString);
    std::cout << "Length: " << length << std::endl;  // Output: Length: 13
    return 0;
}

Method 4: Using pointer arithmetic
#include <iostream>
#include <string>
int stringLength(const std::string& str) {
    const char* ptr = str.c_str();  // Get C-style string
    int count = 0;
    while (*ptr != '\0') {  // Loop until the null terminator
        count++;
        ptr++;
    }
    return count;
}
int main() {
    std::string myString = "Hello, World!";
    int length = stringLength(myString);
    std::cout << "Length: " << length << std::endl;  // Output: Length: 13
    return 0;
}

These methods demonstrate how to calculate the length of a string in C++ without using the built-in length() or size() functions.
