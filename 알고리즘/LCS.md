최장 공통 문자열
```
char[] a = br.readLine().toCharArray();  
char[] b = br.readLine().toCharArray();  
  
int max = 0;  
int lenA = a.length;  
int lenB = b.length;  
  
int[][] LCS = new int[lenA][lenB];  
  
for (int i = 0; i < lenA; i++) {  
    for (int j = 0; j < lenB; j++) {  
        if (a[i] == b[j]) {  
            if (i == 0 || j == 0) {  
                LCS[i][j] = 1;  
            } else {  
                LCS[i][j] = LCS[i - 1][j - 1] + 1;  
            }  
            max = Math.max(max, LCS[i][j]);  
        }  
    }  
}  
  
System.out.println(max);
```

최장 공통 부분 수열
- 1. 길이 구하기
```
char[] a = br.readLine().toCharArray();  
char[] b = br.readLine().toCharArray();  
  
int max = 0;  
int lenA = a.length;
int lenB = b.length;  
  
int[][] LCS = new int[lenA + 1][lenB + 1];  
  
for (int i = 1; i <= lenA; i++) {  
    for (int j = 1; j <= lenB; j++) {  
        if (a[i - 1] == b[j - 1]) {  
            LCS[i][j] = LCS[i - 1][j - 1] + 1;  
            continue;  
        }  
        LCS[i][j] = Math.max(LCS[i - 1][j], LCS[i][j - 1]);  
    }  
}  
  
int resultLen = LCS[lenA][lenB];  
System.out.println(resultLen);
```

- 2. 수열 구하기
```
StringBuilder sb = new StringBuilder();  
Stack<Character> st = new Stack<>();  
  
int x = lenB;  
int y = lenA;  
while (x > 0 && y > 0) {  
    if (x == 0 || y == 0) {  
        break;  
    }  
    if (LCS[y][x] == LCS[y - 1][x]) {  
        y--;  
        continue;  
    }  
    if (LCS[y][x] == LCS[y][x - 1]) {  
        x--;  
        continue;  
    }  
    st.push(b[x - 1]);  
    x--;  
    y--;  
}  
  
while (!st.isEmpty()) {  
    sb.append(st.pop());  
}  
  
System.out.println(sb);
```