# curly-octo-succotash
Syirin Nabilah
Hyperion
#include <iostream>
using namespace std;

int reverseNumber(int x) {
    int sign = (x < 0) ? -1 : 1;
    x = (x < 0) ? -x : x;  // ubah jadi positif dulu
    int rev = 0;

    while (x > 0) {
        int digit = x % 10;
        rev = rev * 10 + digit;
        x /= 10;
    }

    return sign * rev;
}

int main() {
    int n;
    cout << "Masukkan jumlah elemen array: ";
    cin >> n;

    int arr[n];
    cout << "Masukkan elemen array:\n";
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    cout << "\nHasil setelah dibalik:\n";
    for (int i = 0; i < n; i++) {
        cout << reverseNumber(arr[i]) << " ";
    }
    cout << endl;

    retur
