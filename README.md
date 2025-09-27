# Syirin Nabilah Hyperion Case 1

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

    #Case 2 
    #include <iostream>
#include <vector>
#include <string>
#include <limits>
using namespace std;

// User-defined mathematical reversal (no std::reverse)
// Reverse tanpa width (umum)
int reverseNumberMath(int x) {
    bool neg = (x < 0);
    if (neg) x = -x;
    int rev = 0;
    while (x > 0) {
        int d = x % 10;
        rev = rev * 10 + d;
        x /= 10;
    }
    return neg ? -rev : rev;
}

// Reverse dengan fixed width (penting untuk memastikan reversibility
// ketika ada leading zero setelah pembalikan). 
// width >= 1, misal width = 3 untuk ASCII (0..127)
int reverseWithWidth(int x, int width) {
    bool neg = (x < 0);
    if (neg) x = -x;
    int rev = 0;
    // proses width digit; jika x habis, digit = 0
    for (int i = 0; i < width; ++i) {
        int d = x % 10;   // jika x == 0, d akan 0 -> memberikan leading zeros
        rev = rev * 10 + d;
        x /= 10;
    }
    return neg ? -rev : rev;
}

// Encrypt: input string -> vector<int> (encrypted integers)
vector<int> encryptString(const string &s, int width = 3) {
    vector<int> out;
    for (char c : s) {
        int ascii = static_cast<unsigned char>(c); // 0..255 safe
        int rev = reverseWithWidth(ascii, width);
        out.push_back(rev);
    }
    return out;
}

// Decrypt: vector<int> (encrypted) -> string
string decryptVector(const vector<int> &enc, int width = 3) {
    string out;
    out.reserve(enc.size());
    for (int v : enc) {
        int ascii = reverseWithWidth(v, width);
        // cast back to char (safely)
        char c = static_cast<char>(ascii);
        out.push_back(c);
    }
    return out;
}

// Mendapatkan sebagian kata asli dari data terenkripsi
string partialDecrypt(const vector<int> &enc, int startIdx, int len, int width = 3) {
    // validasi
    if (startIdx < 0) startIdx = 0;
    if (startIdx >= (int)enc.size()) return "";
    int endIdx = startIdx + len;
    if (endIdx > (int)enc.size()) endIdx = enc.size();

    string out;
    for (int i = startIdx; i < endIdx; ++i) {
        int ascii = reverseWithWidth(enc[i], width);
        out.push_back(static_cast<char>(ascii));
    }
    return out;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    cout << "=== Mesin Misterius (Encrypt / Decrypt) ===\n";
    cout << "Pilih mode: 1 = Encrypt, 2 = Decrypt, 3 = Partial-Decrypt (dari sandi terenkripsi)\n";
    int mode;
    cin >> mode;
    cin.ignore(numeric_limits<streamsize>::max(), '\n');

    const int WIDTH = 3; // gunakan 3 digit untuk ASCII (0..127)

    if (mode == 1) {
        // Encrypt
        cout << "Masukkan teks asli (hingga spasi, atau gunakan getline):\n";
        string plain;
        getline(cin, plain);

        vector<int> enc = encryptString(plain, WIDTH);
        cout << "Encrypted integers (panjang " << enc.size() << "):\n";
        for (size_t i = 0; i < enc.size(); ++i) {
            if (i) cout << ' ';
            cout << enc[i];
        }
        cout << "\n";
    } else if (mode == 2) {
        // Decrypt: user masukkan panjang dan deret integer terenkripsi
        cout << "Masukkan jumlah elemen terenkripsi (n): ";
        int n; cin >> n;
        vector<int> enc(n);
        cout << "Masukkan " << n << " bilangan (dipisah spasi atau newline):\n";
        for (int i = 0; i < n; ++i) cin >> enc[i];

        string plain = decryptVector(enc, WIDTH);
        cout << "Hasil dekripsi (teks asli):\n" << plain << "\n";
    } else if (mode == 3) {
        // Partial decrypt: baca enc array lalu indeks dan panjang
        cout << "Masukkan jumlah elemen terenkripsi (n): ";
        int n; cin >> n;
        vector<int> enc(n);
        cout << "Masukkan " << n << " bilangan (dipisah spasi atau newline):\n";
        for (int i = 0; i < n; ++i) cin >> enc[i];

        cout << "Masukkan start index (0-based) dan length yang ingin diambil:\n";
        int start, len; cin >> start >> len;

        string part = partialDecrypt(enc, start, len, WIDTH);
        cout << "Hasil partial-decrypt (dari index " << start << ", len " << len << "):\n";
        cout << part << "\n";
    } else {
        cout << "Mode tidak dikenal.\n";
    }


    

    cout << "\nHasil setelah dibalik:\n";
    for (int i = 0; i < n; i++) {
        cout << reverseNumber(arr[i]) << " ";
    }
    cout << endl;

    return 0;
    
    }

    #Case 3

    #include <iostream>
using namespace std;

int main() {
    int green = 3, yellow = 1, red = 2;
    int cycle = green + yellow + red;

    int t;
    cout << "Masukkan waktu detik: ";
    cin >> t;

    // posisi dalam siklus
    int pos = t % cycle;

    // cukup dengan 2 if saja
    if (pos < green) cout << "Hijau\n";
    else if (pos < green + yellow) cout << "Kuning\n";
    else cout << "Merah\n";

    return 0;
}

    
