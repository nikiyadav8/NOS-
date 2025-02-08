# NOS-

Q- Test

Experiment 1
1.	Aim: Create an IP Address Validator.
2.	Objective: Check if an input string is a valid IPv4 address.
3.	Details: Split the string by "." and validate each part (0-255 range).
4.	Algorithm:
Steps:
	Get Input:
o	Prompt the user to enter an IP address as a string.
	Split the String:
o	Split the input string by the dot (".") character. This will give you a list of four strings, each representing an octet (a number between 0 and 255).
	Validate Each Octet:
o	Iterate through each octet in the list.
o	Check if each octet can be converted to an integer.
o	If the conversion is successful: 
	Check if the integer is within the valid range (0 to 255).
	If the integer is outside the range, the IP address is invalid.
o	If the conversion fails, the IP address is invalid.
	Determine Validity:
o	If all octets pass the validation checks, the IP address is valid.
o	If any octet fails, the IP address is invalid.
	Display Result:
o	Print a message indicating whether the input string is a valid IP address or not.
5.	Implementation:
#include <iostream>
#include <string>
#include <vector>
#include <sstream>

using namespace std;

bool is_valid_ip(const string& ip_str) {
    vector<string> octets;
    stringstream ss(ip_str);
    string token;

    while (getline(ss, token, '.')) {
        octets.push_back(token);
    }

    if (octets.size() != 4) {
        return false;
    }

    for (const string& octet : octets) {
        try {
            int octet_int = stoi(octet);
            if (octet_int < 0 || octet_int > 255) {
                return false;
            }
        } catch (const invalid_argument& e) {
            return false;
        }
    }
    return true;
}

int main() {
    string ip_address;

    cout << "Enter an IP address: ";
    cin >> ip_address;

    if (is_valid_ip(ip_address)) {
        cout << ip_address << " is a valid IP address." << endl;
    } else {
        cout << ip_address << " is not a valid IP address." << endl;
    }
    return 0;
}

6.	Explanation:
1.	Include necessary headers:
o	iostream for input/output operations.
o	string for string manipulation.
o	vector for storing the octets.
o	sstream for string stream operations.
2.	is_valid_ip() function:
o	Takes the IP address string as input.
o	Creates a stringstream to easily extract octets.
o	Splits the string into octets using getline() with the delimiter ".".
o	Checks if the number of octets is exactly four.
o	Iterates through each octet: 
	Tries to convert the octet to an integer using stoi(). If the conversion fails (e.g., due to non-numeric characters), it's not a valid octet.
	Checks if the integer value is within the range 0-255.
o	Returns true if all octets are valid, otherwise false.
