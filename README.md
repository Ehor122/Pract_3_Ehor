Практична 3
Виконав Горбач Єгор

Опис
Скільки можна сформувати чисел із р розрядів, використовуючи цифри 5 та 9, в яких три однакові цифри не стоять поруч?

Вхідні дані: ціле число р (р ≤ 30)

Вихідні дані: кількість чисел із р розрядів

Код:


#include <stdio.h>

#define MAX_P 30

// A function for calculating the number of numbers with p bits

int count_numbers(int p) {
  
    if (p == 1) return 2; // Possible numbers: 5, 9
  
    if (p == 2) return 4; // Possible numbers: 55, 59, 95, 99

   
    // Arrays for storing the number of numbers that end in 5 or 9,
   
    // without three identical digits in a row
   
    int dp5[MAX_P + 1], dp9[MAX_P + 1];

  
    // Initialization of initial values
    
    dp5[1] = 1;
    
    dp9[1] = 1;
    
    dp5[2] = 2;
    
    dp9[2] = 2;

    // Calculating values for all p from 3 to MAX_P
    
    for (int i = 3; i <= p; i++) {
    
        dp5[i] = dp9[i-1] + dp9[i-2]; // ends with 5: can have 9 before it or 9 and 9 before it
        
        dp9[i] = dp5[i-1] + dp5[i-2]; // ends with 9: can have 5 before it or 5 and 5 before it
    
    }

    // The total number of numbers with p bits
    
    return dp5[p] + dp9[p];

}

int main() {

    int p;
    
    printf("Enter the value of p: ");
    
    scanf("%d", &p);

    if (p <= 0 || p > MAX_P) {
    
        printf("Incorrect value of p. p must be in the range from 1 to %d.\n", MAX_P);
        
        return 1;
    
    }
    

    
    int result = count_numbers(p);
    
    printf("Number of numbers with %d digits: %d\n", p, result);

    return 0;
}
